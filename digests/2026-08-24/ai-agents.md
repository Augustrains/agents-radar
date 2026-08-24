# OpenClaw 生态日报 2026-08-24

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-24 00:31 UTC

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

**日期：** 2026-08-24  
**数据窗口：** 过去 24 小时  
**数据来源：** github.com/openclaw/openclaw


## 1. 今日速览

OpenClaw 在过去 24 小时内保持了极高的社区活跃度：共有 **500 条 Issue 更新**（新开/活跃 456 条，关闭 44 条）和 **500 条 PR 更新**（待合并 404 条，合并/关闭 96 条）。当日无新版本发布，但 **P0 级 SQLite 损坏复发问题**（#126821） 和 **totalTokens 膨胀修复不完整问题**（#125333） 持续发酵，成为社区关注焦点。值得关注的是，**安全与凭证相关的修复占当日合并 PR 的较大比重**（安装策略确认、凭据契约可退出、OAuth 所有权保留等），显示项目组正在系统性地加固安全边界。Release validation（#125626）仍在进行中，beta.3 发布被一个发布验证流程阻塞（PR #128371）。


## 2. 版本发布

当日无新版本发布。Release validation #125626（v2026.8.1-beta.2）仍在进行中，说明测试流程遇到了阻塞（见 PR #128371 的描述：发布验证流程要求全组通过，但冻结候选中包含已重跑通过的 Slack 测试）。


## 3. 项目进展

过去 24 小时内有 **96 个 PR 被合并或关闭**，以下是值得关注的重要合并：

| PR | 标题 | 影响领域 | 说明 |
|---|---|---|---|
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | 安全 / CLI / 插件安装 | **安全加固里程碑。** `security.installPolicy` 命令可返回 `warn` 状态，交互式 CLI 安装时要求操作员确认风险后继续，同时 UI 侧配套 PR（#120900）也已合并。 |
| [#126424](https://github.com/openclaw/openclaw/pull/126424) | fix(gateway): keep conversation delivery within agent bindings | Gateway / 多 Agent / 消息投递 | 修复多 Agent 场景下会话工具可跨绑定投递消息的严重问题，涉及 Discord、Slack、Telegram 等全渠道。 |
| [#123975](https://github.com/openclaw/openclaw/pull/123975) | fix(scripts): clean up tsgo process trees on timeout or signal | 构建工具 / 进程管理 | tsgo 包装器现在通过托管进程管理器运行，并提供可配置的超时看门狗，避免遗留卡死的编译进程树。 |
| [#128371](https://github.com/openclaw/openclaw/pull/128371) | fix(release): authorize focused beta evidence | 发布流程 | 解决 beta.3 发布阻塞：允许在冻结候选只变更了已重跑通过的测试时，使用聚焦验证证据而非全组验证。 |
| [#128423](https://github.com/openclaw/openclaw/pull/128423) | fix(gateway): preserve mixed media failure receipts | Gateway / 媒体投递 | 修复混合媒体消息中，失败附件的错误信息被静默丢弃的问题。 |
| [#125471](https://github.com/openclaw/openclaw/pull/125471) | fix(models): keep Claude CLI OAuth available in Control UI | 认证 / Control UI | 修复 Gateway 重启后 Claude CLI OAuth 丢失刷新所有权的问题。 |
| [#120900](https://github.com/openclaw/openclaw/pull/120900) | feat(ui): review install policy warnings | 安全 / Control UI | 管理员可在 Control UI 中审查安装策略警告并明确继续安装。 |

**整体判断：** 项目正在系统性地推进安全加固（安装确认、凭据隔离、OAuth 修复）、多 Agent 消息投递边界修复，以及 UI/UX 优化（Workboard 折叠、目录刷新风暴治理）。安全相关改动占比明显提升。


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 主题 | 背后诉求 |
|---|---|---|---|---|
| 1 | [#125626](https://github.com/openclaw/openclaw/issues/125626) | 18 | v2026.8.1-beta.2 release validation | 社区测试者协作验证 beta 版本，确保发布质量 |
| 2 | [#119796](https://github.com/openclaw/openclaw/issues/119796) | 15 | Windows vitest teardown EBUSY 错误 | Windows 平台测试稳定性问题，agent 状态 SQLite 句柄未释放 |
| 3 | [#121953](https://github.com/openclaw/openclaw/issues/121953) | 13 | Cron agent 在 DeepSeek 上 stall | **模型兼容性问题，** `[cron:...]` 前缀在 DeepSeek API 被降级处理，导致任务长时间停滞 |
| 4 | [#109490](https://github.com/openclaw/openclaw/issues/109490) | 12 | 客户端委派工具 `terminate:true` 中断 turn | 代理发送进度消息后无法继续执行后续工作，**消息丢失**问题 |
| 5 | [#39476](https://github.com/openclaw/openclaw/issues/39476) | 12 | A2A sessions_send 回叫导致重复消息 | 多 Agent 互调时消息重复投递 |
| 6 | [#6599](https://github.com/openclaw/openclaw/issues/6599) | 11 | 请求 `/models test-fallback` 命令 | 用户在等待真实故障前验证 fallback 链配置 |
| 7 | [#89278](https://github.com/openclaw/openclaw/issues/89278) | 10 | Codex OAuth 刷新超时（>10s） | **回归问题：** OAuth 探测成功但 cron/heartbeat 刷新超时 |
| 8 | [#97616](https://github.com/openclaw/openclaw/issues/97616) | 9 | 僵尸子进程累积 | 长期运行后系统性能下降 |
| 9 | [#126821](https://github.com/openclaw/openclaw/issues/126821) | 6 | **P0:** SQLite 损坏在重建后 15-24h 内复发 | 用户已重建 5 次数据库仍无法解决，是当前最严重问题 |
| 10 | [#125333](https://github.com/openclaw/openclaw/issues/125333) | 4 | **P0:** totalTokens 膨胀修复不完整 | 修复只覆盖 `api === "cli"` 路径，memory-flush 路径仍是未防护的棘轮 |

**热点分析：** 讨论最集中的话题是 **beta 版本验证**（#125626）和 **消息丢失/管道问题**。DeepSeek 模型兼容性（#121953）成为新的热点，说明用户正在更广泛地使用非 OpenAI 模型。此外，**P0 级 SQLite 损坏复发**（#126821）虽然评论数不高，但严重程度最高。


## 5. Bug 与稳定性

### P0 级（严重阻塞）

| Issue | 标题 | 状态 | Fix PR | 说明 |
|---|---|---|---|---|
| [#126821](https://github.com/openclaw/openclaw/issues/126821) | SQLite 损坏在重建后 15-24h 内复发（2026.8.1-beta.2, WSL2） | 开放 | 无 | 5 天 5 次事件，包括 "paralyzed gateway" 模式拒绝所有服务但不退出 |
| [#125333](https://github.com/openclaw/openclaw/issues/125333) | totalTokens 膨胀修复不完整，memory-flush 路径未防护 | 开放 | 无 | #123065 的修复只覆盖 `api === "cli"` 路径 |
| [#108520](https://github.com/openclaw/openclaw/issues/108520) | iOS 应用更新后 Talk Mode 和聊天完全失效 | 开放 | 无 | Gateway 连接正常但无任何功能 |

### P1 级（功能回归/消息丢失）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#126246](https://github.com/openclaw/openclaw/issues/126246) | Telegram 持久化投递卡在 `send_attempt_started`，重启后丢失 | 开放 | 无 |
| [#127948](https://github.com/openclaw/openclaw/issues/127948) | WhatsApp 群组回复在引用缓存过期后渲染为空白气泡 | 开放 | 无 |
| [#125838](https://github.com/openclaw/openclaw/issues/125838) | QQBot slash 命令（/think, /status）无回复 | 开放 | 无 |
| [#111944](https://github.com/openclaw/openclaw/issues/111944) | Codex commentary 未投递到 Telegram | 开放 | 无 |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 刷新超时（>10s） | 开放 | 无 |
| [#112668](https://github.com/openclaw/openclaw/issues/112668) | sessions_yield abort-settle 超时导致子代理公告丢失 | 开放 | 无 |

### 回归类问题

- **Codex 客户端中断**（#86214）：大图像请求期间客户端关闭，导致 turn 中断，疑似与 `logs_2.sqlite` 增大有关。
- **上下文使用率跳跃**（#108215）：从 57% 降至 13% 且无压缩记录，提示 token 统计存在不确定性。
- **Windows 原生 CLI Scheduled Task**（#91144）：前台窗口正常但 Scheduled Task 不保持运行。

### 已关闭的稳定性问题

当日关闭了 44 个 Issue，其中包括 #119796（Windows vitest EBUSY）、#109490（客户端委派工具中断）、#112246（session-key tombstone 永久化）、#111969（回复栅栏无限期等待）等。


## 6. 功能请求与路线图信号

| 功能请求 | Issue | 相关 PR | 是否可能纳入下版本 |
|---|---|---|---|
| **安装策略警告确认机制** | — | [#116489](https://github.com/openclaw/openclaw/pull/116489)（已合并） | ✅ 已落地 |
| **UI 安装策略警告审查** | — | [#120900](https://github.com/openclaw/openclaw/pull/120900)（已合并） | ✅ 已落地 |
| **/models test-fallback 命令** | [#6599](https://github.com/openclaw/openclaw/issues/6599) | 无 | ⚠️ 高点赞（1）+ 明确需求，但无 PR |
| **每 Agent MCP 服务器隔离** | [#72591](https://github.com/openclaw/openclaw/issues/72591) | 无 | ⚠️ 安全相关 + 资源优化，优先级可能提升 |
| **slash command 描述 i18n** | [#79458](https://github.com/openclaw/openclaw/issues/79458) | 无 | 中低可能性 |
| **Kubernetes 部署文档改进** | [#91455](https://github.com/openclaw/openclaw/issues/91455) | 无 | 中可能性 |
| **UI 质量全面重构** | [#75947](https://github.com/openclaw/openclaw/issues/75947) | 多个 UI 优化 PR | ⚠️ 渐进式推进中 |
| **composer 暂存 slash 命令参数** | — | [#123356](https://github.com/openclaw/openclaw/pull/123356)（开放） | ✅ 进行中 |
| **Workboard 列折叠** | — | [#128115](https://github.com/openclaw/openclaw/pull/128115)（开放） | ✅ 进行中 |


## 7. 用户反馈摘要

### 真实痛点

1. **SQLite 损坏循环**（#126821）：用户报告 5 天内发生 5 次数据库损坏，即使 VACUUM INTO 重建后 15-24 小时内依然复发。这已严重打击用户对 beta 稳定性的信心。

2. **修复"修一半"的问题**（#125333）：用户指出 totalTokens 膨胀修复只覆盖了一个 API 路径，剩余路径仍可能导致 token 计数无限增长。类似的还有 #118673 指出 `model.completed` 事件缺少 `stopReason` 导致截断不可诊断。

3. **多 Agent 消息投递混乱**：（#39476, #96692, #111358, #115400）多个用户报告 `sessions_send`/A2A 在不同场景下出现重复消息、消息丢失、投递到错误渠道等问题，说明多 Agent 通信仍是痛点区域。

4. **DeepSeek 兼容性**（#121953）：`[cron:...]` 前缀被 DeepSeek API 降级处理，导致 cron 任务卡顿数十秒至数分钟。这阻断了用户向非 OpenAI 模型迁移的路径。

5. **Channel 特定 Bug 频发**：QQBot 无回复（#125838）、WhatsApp 空白气泡（#127948）、Telegram 卡在 `send_attempt_started`（#126246）— 全渠道覆盖面广，但每个都有特定根因。

### 用户积极反馈

- **安全加固获认可**：安装策略确认机制（PR #116489, #120900）和凭据契约可退出（PR #128077）等安全改进获得了社区关注。
- **UI 优化持续推进**：Workboard 折叠（PR #128115）、目录刷新风暴治理（PR #123535）等 PR 获得了 maintainer 的积极回应。

### 新出现的使用场景

- **AI Agent 代发 Issue**：Issue #124911 由 Scott Hanselman 的代理代发（"Filed by Tony, Scott Hanselman's OpenClaw agent"），说明用户开始使用 OpenClaw 的代理能力来管理 GitHub 交互。


## 8. 待处理积压

### 长期未解决的高优先级问题

| Issue | 提出时间 | 严重度 | 说明 |
|---|---|---|---|
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | 2026-03-08 | P1 | A2A sessions_send 重复消息，5 个月未解决 |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | 2026-06-02 | P1 | Codex OAuth 刷新超时，2.5 个月未解决 |
| [#78493](https://github.com/openclaw/openclaw/issues/78493) | 2026-05-06 | P1 | `sudo openclaw update` 导致混合所有权，3.5 个月 |
| [#79451](https://github.com/openclaw/openclaw/issues/79451) | 2026-05-08 | P1 | tools.deny 未在 claude-cli 后端生效（安全） |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 2026-06-29 | P1 | 僵尸子进程累积 |
| [#118028](https://github.com/openclaw/openclaw/issues/118028) | 2026-08-02 | P1 | AbortSignal.any() 信号身份丢失 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | 2026-08-11 | P1 | **DeepSeek Cron stall（新热点）** |

### 等待维护者审查的 PR

| PR | 标题 | 状态 | 等待时间 |
|---|---|---|---|
| [#126960](https://github.com/openclaw/openclaw/pull/126960) | test(e2e): share canonical auth store reader | 👀 ready for maintainer look | 3 天 |
| [#127083](https://github.com/openclaw/openclaw/pull/127083) | fix: preserve auth ownership when onboarding config write fails | 👀 ready | 3 天 |
| [#127059](https://github.com/openclaw/openclaw/pull/127059) | fix: preserve legacy workspace during onboarding | 👀 ready | 3 天 |
| [#127060](https://github.com/openclaw/openclaw/pull/127060) | fix(setup): reject message with onboarding options | 👀 ready | 3 天 |
| [#128115](https://github.com/openclaw/openclaw/pull/128115) | feat(ui): add collapsible Workboard columns | 👀 ready | 1 天 |
| [#128401](https://github.com/openclaw/openclaw/pull/128401) | fix(discord): honor explicit component attachment filenames | 👀 ready | 1 天 |
| [#128425](https://github.com/openclaw/openclaw/pull/128425) | fix(tui): preserve queued messages when reselecting current session | 待审查 | 当日 |

### 维护者关注建议

1. **P0 SQLite 损坏复发**（#126821）是当前最紧急问题，建议最高优先级处理。
2. **totalTokens 膨胀修复不完整**（#125333）表明 #123065 的修复覆盖不全面，需要补全。
3. **多个 P1 消息丢失问题**（Telegram、WhatsApp、QQBot）有集中在渠道适配层的趋势，建议排查是否有共同根因。
4. **DeepSeek Cron stall**（#121953）是新出现的热点，可能影响使用非 OpenAI 模型的用户群体扩大。

---

*本日报由 AI 自动生成，数据基于 github.com/openclaw/openclaw 公开仓库。*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**日期：** 2026-08-24
**数据窗口：** 过去 24 小时


## 1. 生态全景

个人 AI 助手开源生态正处于 **"高吞吐迭代 + 安全加固 + 架构收敛"** 三重并行阶段。以 OpenClaw 为首的头部项目保持着每日数百条 Issue/PR 的超高活跃度，而 NanoBot、IronClaw、ZeroClaw 等中坚力量也处于密集开发期。从各项目合并的 PR 来看，**安全加固**（SSRF 防护、安装策略确认、凭据隔离、OAuth 修复）成为 2026 年下半年的系统性主题。同时，多项目不约而同地出现 **配置"看似生效实则无效"** 的投诉集群（Hermes Agent #93263、OpenClaw #125333、NanoClaw #3457），指向验证/规范化链路存在共性技术债。生态整体呈现 **"头部扩张、中部追赶、尾部收敛"** 的分层竞争格局。


## 2. 各项目活跃度对比

| 项目 | 新 Issues | 新 PRs | 合并/关闭 PRs | Release | 健康度 | 活跃阶段 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 456 活跃 / 44 关闭 | 404 待合并 / 96 关闭 | 96 | 无 | ⚠️ 一般（2 个 P0） | 快速迭代 + 安全加固 |
| **Hermes Agent** | 32 活跃 | 49 待合并 | 1 | 无 | ⚠️ 一般（并行工具丢失） | 快速迭代 + Bug 集中爆发 |
| **NanoClaw** | 6 新 | 49 待合并 / 20 关闭 | 20 | 无 | 🟡 中（3 High） | 密集开发期（PR stack） |
| **IronClaw** | 9 新 | 18 待合并 / 5 关闭 | 5（dependabot） | 无 | ✅ 良好 | 核心功能推进 + CI 重建 |
| **ZeroClaw** | 50 更新 | 50 更新 | 5 | 无 | ✅ 良好 | 架构 RFC 讨论期 |
| **NanoBot** | 1 新 / 1 关闭 | 14 待合并 / 5 合并 | 5 | 无 | ✅ 良好 | 稳定迭代 |
| **CoPaw (QwenPaw)** | 5 新 | 7 待合并 / 8 关闭 | 8 | 无 | ⚠️ 一般（内存泄漏） | 功能收尾 + 修复集中期 |
| **Moltis** | 2 新 / 1 关闭 | 6 待合并 | 0 | 无 | 🟡 中（崩溃级 Bug） | 密集修 bug 阶段 |
| **PicoClaw** | 0（2 stale 关闭） | 2 待合并 / 5 合并 | 5 | 无 | ✅ 良好 | 平稳收敛 |
| **NullClaw** | 1 新 | 0 | 0 | 无 | 🟡 中（并发挂起） | 开发间歇期 |
| **LobsterAI** | 0（4 stale 关闭） | 0（3 stale 关闭） | 3 | 无 | 🟢 稳定但停滞 | 低活跃清理期 |
| **TinyClaw** | — | — | — | — | — | 无活动 |
| **ZeptoClaw** | — | — | — | — | — | 无活动 |


## 3. OpenClaw 在生态中的定位

**生态绝对头部，规模碾压级领先。** OpenClaw 单日 500 条 Issue + 500 条 PR 的数据，是 Hermes Agent（50+50）的 10 倍、NanoClaw（6+50）的近 2 倍（PR 侧）、IronClaw（9+23）的 22 倍（Issue 侧）。社区规模、贡献者数量、用户反馈量均处于断层第一。

**优势：**
- **全渠道覆盖广度**：Discord、Slack、Telegram、WhatsApp、QQBot 等全渠道适配，构建了最完整的消息层生态
- **安全加固的系统性**：单日集中合并安装策略确认、凭据契约、OAuth 所有权保留多个安全 PR，展示了头部项目对安全基线的重视
- **多 Agent / A2A 协议先发**：会话投递边界修复、A2A 回调去重正在推进，兼顾单体与多智能体两种形态

**技术路线差异：** 与 Hermes Agent 聚焦桌面/TUI 体验、IronClaw 专注持久化沙箱不同，OpenClaw 走的是 **"Gateway 为中心的全渠道路由 + 插件化生态 + 企业级安全"** 的路线。其 Gateway 层设计成为多数同类项目的参照系。

**核心风险：** P0 级 SQLite 损坏复发（#126821）和 totalTokens 膨胀修复不完整，提示其数据持久化层存在深层次架构问题，beta.3 版本发布持续受阻，可能影响用户信任。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **配置/设置的"静默失效"** | Hermes Agent（#93263 聚类 14 Issue）、OpenClaw（#125333）、NanoClaw（#3457）、LobsterAI（#1202） | 用户配置被规范化剥离、静默丢弃，或修复只覆盖部分路径，导致"看似生效实则无效"。**四个项目同时爆发，是生态级技术债** |
| **多 Agent 消息投递可靠性** | OpenClaw（#39476/#126424）、Hermes Agent（#93251）、Moltis（#1231）、NullClaw（#991） | A2A 重复消息、会话工具跨绑定投递、并行工具调用结果丢失、MCP 客户端失效后工具桥挂起 |
| **模型兼容性扩展** | OpenClaw（#121953 DeepSeek Cron stall）、IronClaw（#85388 DeepSeek 峰谷计价）、Hermes Agent（#85388 同 PR）、LobsterAI（#1199 模型级 token 配置） | 非 OpenAI 模型（尤其 DeepSeek）的使用正在快速普及，但前缀处理、计价逻辑、兼容性适配滞后 |
| **OAuth / 凭据安全加固** | OpenClaw（#125471/#128077）、NanoClaw（#3492）、IronClaw（#7829 Gmail 弹窗秒消失）、CoPaw（#7066 refresh_token 持久化）、LobsterAI（#1202 key 泄漏） | 认证弹窗生命周期、refresh_token 持久化、凭据隔离与所有权保持，是安全投入最集中的区域 |
| **会话持久化与恢复** | OpenClaw（#126821 SQLite 损坏）、Hermes Agent（#93361 会话存活）、CoPaw（#7217 上次逻辑复现）、NanoClaw（#3455 poll-loop 心跳）、ZeroClaw（#9487 RFC） | 数据库损坏、会话状态残留、恢复机制不完善，多项目在会话全生命周期管理上遇到瓶颈 |
| **SSRF / 安全边界** | PicoClaw（#3322/#3323/#3324 多通道 SSRF 加固）、IronClaw（#7810 沙箱凭据绑定）、Moltis（#1230 fail-closed）、ZeroClaw（#6996 沙箱策略） | 从通道层到沙箱层的纵深安全防御是各项目共同的优先级 |


## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 关键架构特征 |
|---|---|---|---|
| **OpenClaw** | 全渠道个人 AI 助手框架 | 开发者、企业、重度自托管用户 | Gateway 中心化路由，强调多 Agent / A2A 互操作 |
| **Hermes Agent** | 桌面优先的 Agent 运行时 | 桌面端专业用户、macOS/Linux | 强调 Desktop + TUI + 多进程协调，Bot Mode 小组协作 |
| **IronClaw** | 沙箱优先的自主 Agent 平台 | 企业、安全敏感场景 | 持久化每用户沙箱（Docker 路由 + 凭据代理），CI 工程化优秀 |
| **NanoBot** | 轻量级多通道 Agent 网关 | 个人开发者、Docker 部署者 | 进程按角色分离（agent/webui/gateway），强调 turn 级恢复 |
| **NanoClaw** | 轻量级 Multi-Channel SDK | 嵌入式/移动场景开发者 | Chat SDK 深度集成，镜像安全 pinned，github polling 免端口模式 |
| **ZeroClaw** | 架构驱动的标准化 Agent 平台 | 开发者、插件生态贡献者 | 以 RFC 驱动架构决策，WASM 插件化 + Agent Plugins 1.0 标准采纳 |
| **CoPaw (QwenPaw)** | LLM 优先的 Agent 框架 | Python 开发者、多文档处理场景 | Skill-System 运行时热插拔，多项目目录绑定 |
| **Moltis** | 本地嵌入 & 调度增强 | ChatGPT-Next-Web 系用户 | GGUF 本地嵌入、定时任务回传、MCP 客户端管理 |
| **PicoClaw** | 嵌入式/轻量通道适配 | 极简部署需求 | 全渠道 SSRF 统一防护，前缀缓存优化 |
| **NullClaw** | 单机运行 Agent | Proxmox/容器用户 | 多实例协调，MCP stdio 锁竞争 |
| **LobsterAI** | 企业协作 Agent | 网易生态用户 | COWORK 集成，Agent 管理界面优化 |


## 6. 社区热度与成熟度

**第一梯队 — 快速迭代期（日 PR >20）：**
OpenClaw、Hermes Agent、NanoClaw、IronClaw

这批项目保持极高吞吐，但呈现出**两种节奏**：
- OpenClaw / Hermes Agent：**大流量 + 高 Bug 密度**，修复与新增并行，beta 验证流程成为瓶颈
- NanoClaw / IronClaw：**有序的 PR stack 开发**（如 NanoClaw 的 3 层 Chat SDK stack、IronClaw 的 CI 四轨重建），体现了较强的工程治理能力

**第二梯队 — 质量巩固期（日 PR 5-15）：**
ZeroClaw、NanoBot、CoPaw、Moltis、PicoClaw

- ZeroClaw 处于 **RFC 驱动架构收敛期**，设计文档讨论多于代码合并
- NanoBot / PicoClaw 节奏稳健，以修复合入为主
- CoPaw / Moltis 处于 **Bug 密集修复阶段**（内存泄漏、崩溃、连接中断），但社区响应速度快

**第三梯队 — 低活跃/停滞期：**
NullClaw（开发间歇）、LobsterAI（近 5 个月无新功能）、TinyClaw、ZeptoClaw（无活动）


## 7. 值得关注的趋势信号

1. **"配置静默失效"成为生态级信任危机**：四个独立项目同时涌现用户投诉——配置项被规范化剥离、修复仅覆盖部分路径、"看似生效实则无效"。这暗示开源 AI Agent 框架普遍缺乏**配置验证与可观测性**（设置后应有明确反馈或测试命令，如 OpenClaw #6599 请求的 `/models test-fallback` 命令即是最佳实践）。开发者应检查自己的框架是否具备配置回读验证机制。

2. **DeepSeek / 非 OpenAI 模型的"二等公民"处境正在改变**：OpenClaw 的 DeepSeek Cron stall、IronClaw 的 DeepSeek 峰谷计价 PR，以及 LobsterAI 的模型级 token 配置，共同指向 **多模型供应商支持已从"能用"转向"好用"** —— 需要处理前缀兼容、计价差异化、上下文窗口配置等精细节。选择框架时应评估其对目标模型的适配深度。

3. **安全加固从"通道层"向"凭据层"与"钩子层"纵深演进**：PicoClaw 补齐全通道 SSRF 防护、IronClaw 实现沙箱凭据代理（命令只见占位符）、Moltis 讨论 fail-closed 钩子策略——**安全正在从网络边界下推到运行时与数据流内部**。对开发者而言，框架是否支持安全钩子的 fail-closed 语义、凭据是否可隔离到代理层，将成为选型的重要考量。

4. **多 Agent / A2A 互操作的"野蛮生长"已触及瓶颈**：OpenClaw（重复消息、跨绑定投递）、Hermes Agent（并行工具结果丢失）、Moltis（MCP 客户端失效）同时爆发通信可靠性问题。**从"互通"到"可靠互通"的跳跃需要更严谨的消息契约与回退机制**，这是下一阶段多 Agent 框架差异化竞争的关键战场。

5. **"带外操控"（Out-of-Band Control）成为新能力方向**：PicoClaw 和 NanoClaw 同一天出现了手机配对远程操控桌面 Agent 的 PR（gbr/1 协议），IronClaw 的 GitHub polling 免端口模式也在推进——**"无公开端口接入"与"远程观测/操控"正在成为 Agent 运维的新刚需**，面向 NAT/防火墙后用户的价值主张逐渐明确。

---

*本报告基于各项目 2026-08-24 GitHub 公开数据自动生成，覆盖 13 个 AI Agent 开源项目。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-24

## 1. 今日速览

NanoBot 项目在过去 24 小时保持高度活跃，共产生 2 条 Issue 更新（1 开 1 关）和 19 条 PR 更新（14 条待合并，5 条已合并/关闭），无新版本发布。核心贡献者 chengyongru 与 Re-bin 持续高产出，覆盖配置编辑器统一、TLS 性能优化、Channel 扩展等多个方向。值得关注的是，PR 合并率约 26%（5/19），且有一批高质量 PR 处于待合并状态（如 #5498、#5497、#5495），预计未来数日将迎来功能密集落地。整体项目健康度良好，社区提交活跃，但需注意待合并 PR 的积压问题。


## 2. 版本发布

过去 24 小时无新版本发布。


## 3. 项目进展

今日共合并/关闭 5 个 PR，涉及功能新增与代码清理：

- **[#5491] fix(webui): keep answer text outside reasoning shell**（已合并）— 修复 WebUI 中推理内容与答案文本混排问题，将答案片段合并为最终消息，同时保留媒体-only 答案与 fork 边界的原始消息计数。提升多轮对话展示准确性。
- **[#5492] feat(cli): expose nanobot process identities**（已合并）— 将 CLI 进程按角色命名（`nanobot-agent`、`nanobot-webui`、`nanobot-gateway`），TUI 子进程标识为 `nanobot-tui`，并保留 Windows 下 `nanobot.exe` 身份。改善进程管理与运维可观测性。
- **[#5475] refactor: remove remaining dead code**（已合并）— 移除零消费的运行时/设置/渠道/测试辅助代码、未使用的 `websocket-client` 依赖，收窄 WebUI/TUI 导出符号。降低维护成本与依赖面。
- **[#5445] fix(docker): persist OAuth client data**（已合并）— 将 XDG 应用数据指向挂载的实例目录，确保 `nanobot` 非 root 用户下 OAuth 凭据可写，容器替换后凭据可持久化。修复 Docker 部署关键痛点。
- **[#5420] feat(runtime): add user-controlled turn recovery**（已合并）— 为中断的 WebSocket turn 增加侧车检查点持久化，WebUI/TUI 提供显式 **Continue** / **Dismiss** 恢复入口，不自动恢复。已持久化的最终答案可直接恢复，无需再次模型调用。

**关键信号**：多个合并 PR 集中在 WebUI 修复与 Docker 部署体验优化上，说明项目正积极回应用户反馈；`turn recovery` 功能合入标志着运行时健壮性迈出重要一步。


## 4. 社区热点

今日社区讨论热度整体不高，相关 Issue 评论区持平，最有讨论价值的条目：

- **[#5444] [bug] Failed to ogin OpenAI via OAuth in Docker**（已关闭，2 条评论）— 该 Issue 于 8 月 19 日创建，今日关闭，与今日合并的 PR #5445（Docker OAuth 数据持久化）直接对应。用户反馈 Docker 中通过 OAuth 登录 OpenAI 失败，社区通过 PR 形式快速定位并修复，体现了典型的"用户报障→开发者响应→修复合入"闭环。

其余 PR/Issue 评论数均为 0，社区深度讨论较少。


## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 状态 | 说明 |
|---------|-----------|------|------|
| 🔴 高 | **[#5444] Failed to ogin OpenAI via OAuth in Docker** | 已关闭 | Docker 中 OAuth 登录失败，根因是 OAuth 凭据在非 root 用户下不可写。已有对应修复 PR [#5445] 合入。 |
| 🟡 中 | **[#5496] fix(agent): time out no-tools model requests** | 待合并 PR | `AgentRunner` 中超时保护未覆盖 no-tools 请求，可能造成 turn 挂起占用会话锁。PR 已提交。 |
| 🟡 中 | **[#5500] fix(codex): reuse TLS contexts across requests** | 待合并 PR | Codex provider 每次请求重建 TLS 上下文导致请求无响应（py-spy 显示 10 秒卡顿）。PR 提供了缓存方案。 |
| 🟢 低 | **[#5490] fix(webui): clarify aggregate turn token usage** | 待合并 PR | WebUI 中多模型调用轮次的 token 用量展示有歧义，需区分累计输入与最终请求上下文。 |
| 🟢 低 | **[#5499] fix(tui): avoid saving empty sessions** | 待合并 PR | 在空文件夹打开 TUI 会静默创建空会话并同步到工作区，需改为发送首条消息后才持久化。 |

**风险评估**：两项中等级 Bug（#5496、#5500）均已提交修复 PR 但尚未合并，建议维护者优先审查，避免会话阻塞与性能问题影响用户体验。


## 6. 功能请求与路线图信号

- **[#5493] [enhancement] 增加 html，.txt .md 文档等预览**（新开，0 评论）— 用户建议使用原生 `iframe + srcdoc` 实现 HTML 字符串预览，声称安全且自带沙箱隔离。面向 Channel 组件。该请求实现成本较低，且与 WebUI 渲染能力直接相关，社区响应概率较大，有望纳入后续版本；但当前尚未有对应 PR。

**路线图信号**：
- **配置编辑器统一**：PR #5497（共享完整编辑器契约）与 #5498（Agent TUI 中的统一 onboarding）均由 chengyongru 提交，二者存在依赖关系，表明项目正在推进"一次配置、多渠道一致"的编辑器架构，是近期核心方向。
- **原生 Linear Agent Channel**：PR #5495 引入 OAuth + PKCE、SQLite 去重队列与 WebUI 设置流，是继 Matrix 之外又一个原生渠道，渠道生态持续扩展。
- **MCP 体系深化**：#5386（保留 MCP Apps 结果元数据）、#5388（预算模型可见 MCP schema）虽未合并但持续活跃，MCP 工具链的精细化管控是长期方向。


## 7. 用户反馈摘要

- **Docker OAuth 痛点**：Issue #5444 暴露了 Docker 部署中 OAuth 凭据无法持久化的问题，社区快速响应并合入修复 PR #5445。修复后容器替换不再丢失登录状态，直接提升 Docker 部署可用性。
- **文档预览需求**：Issue #5493 来自中文用户（john00010），提出在 Channel 中增加 HTML/txt/md 预览能力，并给出明确技术方案（iframe + srcdoc）。说明部分用户社区对静态文档快速预览有真实场景需求（如查看日志或共享文档）。
- **TUI 空会话问题**：PR #5499 指出在空白目录打开 TUI 会意外创建空会话并同步工作区元数据，属于影响日常使用体验的细节问题。


## 8. 待处理积压

以下 PR 长期未合并，建议维护者关注：

| 条目 | 创建时间 | 积压天数 | 说明 |
|------|---------|---------|------|
| **[#5388] feat(agent): budget model-visible MCP schemas** | 2026-08-13 | 11 天 | MCP 工具 schema 字节预算控制，防止模型上下文膨胀。功能完整且有测试覆盖，可能与近期 MCP 方向 PR 存在交互，需评估优先级。 |
| **[#5386] feat(mcp): preserve MCP Apps result metadata** | 2026-08-13 | 11 天 | 保留 MCP Apps 结构化结果元数据，避免模型上下文被文本化结果稀释。与 #5388 同属 MCP 精细化方向，建议合并评审。 |
| **[#5385] fix(matrix): complete Element SAS request flow** | 2026-08-13 | 11 天 | 完成 Element SAS 验证流程，涉及现代 `m.key.verification.request` 事件兼容。功能完整，但 Matrix 渠道使用率有限，优先级可能较低。 |
| **[#5152] fix(subagent): mark partial completion results** | 2026-07-28 | 27 天 | 标记子代理未完成结果，防止模型误判。已积压近一个月且多次更新，建议维护者明确处理计划。 |

---

*本日报基于 GitHub 公开数据自动生成，数据截至 2026-08-24。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-08-24

## 今日速览

项目今日保持高活跃度：过去24小时内产生50条Issue更新（32条活跃）和50条PR更新（49条待合并），延续了近期的高吞吐状态。值得关注的是，今日出现了一个显著的Bug集中爆发周期——大量Issue在8月23-24日集中提交，涵盖工具结果丢失（#93251）、会话状态异常（#93087）、跨平台同步停滞（#93107）等多个领域，且多数伴随对应的修复PR，表明开发团队响应迅速。与此同时，社区围绕"配置键被静默丢弃"（#93263，pain-miner汇总）和"Bot Mode可靠性"（#93091）两大主题形成了明确的问题聚类。**项目核心风险集中在会话状态一致性与并行工具调用可靠性**，但整体修复节奏健康。另有一个值得警惕的信号：**安全相关Issue (#93364, #91931) 指向依赖链中存在已知漏洞**，需要优先关注。

## 项目进展

今日合并/关闭的PR数量较少（1条），但活跃的待合并PR（49条）反映了多个重要的功能与修复正在推进。

**已合并/关闭：**

- 暂无显著PR合并记录；今日关闭的主要为Issue。

**关键待合并PR（按主题聚类）：**

- **会话恢复与连接可靠性（#91276问题簇综合修复）** — [#93361](https://github.com/NousResearch/hermes-agent/pull/93361) 由teknium1提交，整合了8项修复，使桌面端会话在网关重启、休眠唤醒和WS断开后均能存活，通过取消挂起的reap和静默替代过期runtime来消除reap风暴。
- **Bot Mode组解散遗留脏数据** — [#93373](https://github.com/NousResearch/hermes-agent/pull/93373) 与 [#93372](https://github.com/NousResearch/hermes-agent/pull/93372) 同时提交（分别来自helix4u和chelsealong），均针对成员列表已归零时组解散后会残留"0 bots"空行的问题，展示了社区与维护者的协同修复。
- **Cron运行历史HTTP暴露** — [#93365](https://github.com/NousResearch/hermes-agent/pull/93365) 将已有的执行历史查询能力通过HTTP API暴露，补全了 `/api/jobs` 仅附加 `latest_execution` 的功能缺口。
- **CI无限时任务修复** — [#93370](https://github.com/NousResearch/hermes-agent/pull/93370) 为最后一个无界CI任务添加超时限制（移植自nearai/ironclaw的修复），防止资源浪费。
- **DeepSeek峰谷计价支持** — [#85388](https://github.com/NousResearch/hermes-agent/pull/85388) 实现DeepSeek 8月16日生效的峰谷费率卡，涉及计费模块的时段逻辑。
- **MCP优雅关闭** — [#82892](https://github.com/NousResearch/hermes-agent/pull/82892) 将MCP服务器关闭移至executor，避免在asyncio事件循环线程上同步阻塞15秒。

**项目整体推进评估：** 会话管理、Bot Mode可靠性、安全加固与依赖审计是当前开发主线，项目正通过系统性修复（多PR协同）来弥合"桌面体验-网关-会话持久化"间的断裂带。

## 社区热点

**1. Skills索引过期（长期热点，84条评论）** — [#66616](https://github.com/NousResearch/hermes-agent/issues/66616)

自动化探针持续报告Skills Hub索引过期（29.8小时 vs 26小时限制），该Issue已持续一个月以上且评论数远超其他所有问题。说明这是一个反复出现的自动化流程稳定性问题，社区关注度极高但修复进展缓慢。

**2. `hermes update` 破坏安装（P1，9条评论）** — [#83529](https://github.com/NousResearch/hermes-agent/issues/83529)

用户报告通过 `hermes update` 更新后安装被彻底破坏（Debian Trixie环境）。属于灾难性故障，反馈强烈。今日有相关PR (##93364的姊妹PR) 修复更新流程中上游pull失败仍返回退出码0的问题，可能与此相关。

**3. macOS钥匙串每次更新后重复弹窗（7条评论）** — [#91115](https://github.com/NousResearch/hermes-agent/issues/91115)

本地重建的桌面应用签名变化导致钥匙串ACL不匹配，每次启动均弹窗。影响macOS桌面用户体验，且Python更新器无法修复，需要协调桌面端与CLI更新流程。

**4. 并行工具调用≥4个时全部结果丢失（P1，2条评论）** — [#93251](https://github.com/NousResearch/hermes-agent/issues/93251)

虽然评论数不多，但严重程度高（P1）：单条消息携带4个及以上并行工具调用时，所有结果均返回"[Result unavailable]"。这直击Agent核心可靠性，可能导致复杂任务整体失败。

**5. 配置键被静默丢弃（pain-miner聚类，1条评论）** — [#93263](https://github.com/NousResearch/hermes-agent/issues/93263)

由teknium1汇总的跨支持渠道挖掘出的痛点集群：合法的文档化配置键在规范化/验证过程中被静默丢弃，用户的设置"看似生效实则无效"，需通过协议抓包或400错误才能发现。涵盖14个未解决的Issue和6个PR的规模，反映这是一个系统性问题而非孤立Bug。

## Bug 与稳定性

按严重程度排序：

**高严重度（P1）：**

- **并行工具批处理≥4个调用全部丢失** — [#93251](https://github.com/NousResearch/hermes-agent/issues/93251)（已关闭，修复完成）；关联：#55626也报告了工具结果丢失问题。
- **`hermes update` 破坏安装** — [#83529](https://github.com/NousResearch/hermes-agent/issues/83529)（仍开启）；关联修复PR：[#93033](https://github.com/NousResearch/hermes-agent/pull/93033) 修复上游pull失败时错误返回exit code 0的问题。

**中严重度（P2）：**

- **malformed SQLite schema 逃逸WAL-reset探针导致持久化关闭** — [#93087](https://github.com/NousResearch/hermes-agent/issues/93087)（已关闭）；修复已合入main。
- **Mattermost跨平台同步游标漂移导致消息停滞** — [#93107](https://github.com/NousResearch/hermes-agent/issues/93107)（已关闭）；两处适配器Bug导致消息漏发，需网关重启恢复。
- **`wait()`/`read_log()` 吞掉完成通知** — PR [#93368](https://github.com/NousResearch/hermes-agent/pull/93368) 修复中，影响桌面/TUI的自主完成投递。
- **会话.列表精确标题查找跳过归档行** — [#93056](https://github.com/NousResearch/hermes-agent/issues/93056)（已关闭）；导致Bot Mode误判"无规范会话"并生成重复问候。
- 多个`lifecycle_guard`漏洞/误报（[#89964](https://github.com/NousResearch/hermes-agent/issues/89964)、[#85557](https://github.com/NousResearch/hermes-agent/issues/85557)、[#86010](https://github.com/NousResearch/hermes-agent/issues/86010)、[#80260](https://github.com/NousResearch/hermes-agent/issues/80260)、[#78028](https://github.com/NousResearch/hermes-agent/issues/78028)、[#92372](https://github.com/NousResearch/hermes-agent/issues/92372)）— 均为网关生命周期防护的正则/语法误报与绕过问题，多数已关闭修复，但[#89964](https://github.com/NousResearch/hermes-agent/issues/89964)提出间接执行路径（systemd-run、at、dbus）仍可绕过。

**低严重度（P3）：**

- **Docker沙箱session ID含冒号导致挂载失败** — [#93044](https://github.com/NousResearch/hermes-agent/issues/93044)（已关闭）；Telegram DM默认session ID含冒号，导致绑定挂载路径无效。
- **Langfuse SDK插件占位API Key静默失败** — [#92984](https://github.com/NousResearch/hermes-agent/issues/92984)（已关闭）；初始化不报错但从不发送数据。
- **桌面端Bot Mode远程组删除残留空行** — [#93345](https://github.com/NousResearch/hermes-agent/issues/93345)（仍开启）；对应PR [#93373](https://github.com/NousResearch/hermes-agent/pull/93373) 和 [#93372](https://github.com/NousResearch/hermes-agent/pull/93372) 已在修复。

**安全相关：**

- **npm audit: nanoid <3.3.18 DoS漏洞** — [#93364](https://github.com/NousResearch/hermes-agent/issues/93364)（仍开启）；vite/sanitize-html传递依赖引入，peer-dep冲突导致阻塞。
- **`hermes update` 保留漏洞传递依赖 + nanoid@3.3.17固定** — [#91931](https://github.com/NousResearch/hermes-agent/issues/91931)（仍开启）；升级后仍报告9个已知漏洞。

## 功能请求与路线图信号

**1. Bot Mode可靠性程序** — [#93091](https://github.com/NousResearch/hermes-agent/issues/93091)

kshitijk4poor提出的综合方案：类型化失败原因、信封TTL、注意力徽章、leader路由的群组房间、重试会话策略。多个相关PR（[#93369](https://github.com/NousResearch/hermes-agent/pull/93369)、[#93361](https://github.com/NousResearch/hermes-agent/pull/93361)、[#93372](https://github.com/NousResearch/hermes-agent/pull/93372)）已在今日提交/更新，表明该议题正在快速转化为代码。

**2. Cron运行历史HTTP暴露** — 对应PR [\#93365](https://github.com/NousResearch/hermes-agent/pull/93365)

将已有的执行历史查询接口通过API暴露，为任务编排和外部系统集成提供基础。这条路线信号值得关注。

**3. 临时子会话生命周期删除** — [#93341](https://github.com/NousResearch/hermes-agent/issues/93341)

提议为已完成的临时ephemeral子会话增加生命周期自动删除，区别于已有的父链接/列表过滤功能。这是会话管理向自动化方向演进的信号。

**4. 模型选择标签页增加模型描述与定价** — [#93360](https://github.com/NousResearch/hermes-agent/issues/93360)

桌面端功能请求，在模型选择界面显示实时模型描述与定价信息。偏向用户体验细节，可能进入后续桌面版本。

**5. Cron失败生命周期钩子** — PR [#82901](https://github.com/NousResearch/hermes-agent/pull/82901)

增加`cron_job_failed`事件，使shell hooks、webhooks、插件可以立即获得程序化失败信号，无需轮询`jobs.json`。修复 #82353。已经过长时间review，有望在近期合并。

**6. DeepSeek峰谷计价** — PR [#85388](https://github.com/NousResearch/hermes-agent/pull/85388)

从8月16日起DeepSeek启用峰谷计费（峰值=2倍谷值），已实现完整费率卡逻辑。此PR已搁置数周，可能因为涉及计费准确性的测试验证而延迟。

## 用户反馈摘要

**高频痛点聚类：**

- **配置"看似生效实则无效"** — [#93263](https://github.com/NousResearch/hermes-agent/issues/93263) 汇总了用户设置被静默丢弃的广泛投诉，如 `custom_providers`的`max_output_tokens`被规范化剥离（[#93085](https://github.com/NousResearch/hermes-agent/issues/93085)）。用户必须通过数据包抓取或400错误才能发现，反馈语气明显受挫："I set it and it does nothing." 这是最影响信任度的问题类别。
- **工具结果静默丢失** — 多个Issue（如[#93251](https://github.com/NousResearch/hermes-agent/issues/93251)、[#55626](https://github.com/NousResearch/hermes-agent/issues/55626)）指向工具结果"[Result unavailable]"问题。并行调用批次≥4时100%丢失、复合tool_call ID（`call_xxx|fc_yyy`）导致全部丢弃，用户描述"the work of the whole turn is lost"，对复杂任务自动化是致命打击。
- **更新流程不安全感** — [#83529](https://github.com/NousResearch/hermes-agent/issues/83529) 报告"刚收到更新提示，尝试更新后灾难性失败"，且[#93033](https://github.com/NousResearch/hermes-agent/pull/93033) PR揭示了上游pull失败但返回成功退出码的缺陷，用户对更新流程的信任度降低。
- **跨平台/跨端体验断裂** — Mattermost同步停滞（[#93107](https://github.com/NousResearch/hermes-agent/issues/93107)）、macOS钥匙串弹窗（[#91115](https://github.com/NousResearch/hermes-agent/issues/91115)）、Windows桌面次配置文件会话被默认视图隐藏（[#92944](https://github.com/NousResearch/hermes-agent/issues/92944)）、Bot Mode遗留空行（[#93345](https://github.com/NousResearch/hermes-agent/issues/93345)）等，反映了桌面/TUI/网关多端协同下的体验割裂。
- **`chat -Q` 安静模式不安静** — [#93220](https://github.com/NousResearch/hermes-agent/issues/93220) 用户expectation是"只输出最终响应"，但Reasoning框和工具进度diff仍泄漏到stdout。细节问题的反馈，说明用户对输出可预测性有较高要求。

**正面信号：**

- 用户对修复速度的感知：多个Issue在提交后数小时内即被标记为duplicate并关联修复PR（如[#93044](https://github.com/NousResearch/hermes-agent/issues/93044)、[#93056](https://github.com/NousResearch/hermes-agent/issues/93056)），社区活跃度较高且维护者对Issue分流迅速。

## 待处理积压

**长期未响应/未解决的重要Issue：**

- **Skills索引持续过期（84条评论，已开放37天）** — [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) 虽由自动化探针生成，但一个持续一个月的自动化流程故障长期未修复，可能影响文档站点的用户访问体验。建议优先调查工作流失败原因。

- **`hermes update` 灾难性失败（开放14天，P1）** — [#83529](https://github.com/NousResearch/hermes-agent/issues/83529) P1级别且严重影响用户更新路径，目前看来需要跨模块排查。与[#91931](https://github.com/NousResearch/hermes-agent/issues/91931)（更新后残留漏洞依赖）共同指向更新流程存在系统性缺陷，而不仅是单一命令Bug。

- **macOS钥匙串反复弹窗（开放4天，P2）** — [#91115](https://github.com/NousResearch/hermes-agent/issues/91115) 涉及Python更新器与macOS桌面端签名的交叉问题，修复方案需要跨模块设计（更新器如何感知桌面端签名变化），保持开放状态合理，但影响长尾macOS用户。

**需维护者关注的信号：**

- **Config键静默丢弃问题（pain-miner聚类）** — [#93263](https://github.com/NousResearch/hermes-agent/issues/93263) 涉及14个未解决Issue和6个PR规模，建议作为系统性技术债专项处理，而非逐个修补。

- **长期未合并的PR：** [#85388](https://github.com/NousResearch/hermes-agent/pull/85388)（DeepSeek峰谷计价）和[#82901](https://github.com/NousResearch/hermes-agent/pull/82901)（Cron失败钩子）均开放超过10天尚待review，涉及计费与任务编排等关键路径，建议给予明确回应或加速评估。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-24** | **数据来源：github.com/sipeed/picoclaw**


## 1. 今日速览

PicoClaw 过去 24 小时整体活跃度趋于平稳，社区提交趋于收敛。Issue 侧无新议题产生，2 条此前标记为 stale 的功能请求在今日被自动关闭，表明维护者或系统已对旧议题作出收尾处理。PR 侧保持相对活跃，共 7 条更新，其中 5 条已合并或关闭，2 条仍处于开放状态——合并的 PR 中包含多项针对多平台（微信、企微、Telegram 等）的 SSRF 安全加固修复，以及一项针对前缀缓存（prefix caching）的性能优化，项目整体质量在稳步提升。值得关注的是，有一项新增的开放 PR 为桌面 Agent 引入了手机配对控制能力，预示着项目在远程操控与跨设备协作方向的探索正在推进。


## 2. 版本发布

**无新版本发布。**


## 3. 项目进展（今日合并/关闭的 PR）

过去 24 小时内有 5 条 PR 完成合并或关闭，集中反映了项目在安全加固与性能优化两方面的推进：

- **[#3322] fix(channels): block private targets on inbound media downloads**（已合并）  
  作者：SashaMIT  
  为 QQ、Telegram、Discord、LINE、Slack 等通道的入站附件下载补齐了 SSRF 防护（`BlockPrivateTargets`），防止恶意构造的媒体 URL 访问内网地址。此项修复覆盖了此前 OneBot 已具备但其他通道缺失的安全能力，属于统一安全基线的补齐。  
  🔗 https://github.com/sipeed/picoclaw/pull/3322

- **[#3323] fix(wecom): use CreateSafeHTTPClient for media downloads**（已合并）  
  作者：SashaMIT  
  企业微信通道的媒体下载改用安全 HTTP 客户端，修复了重定向可触达 loopback/私有主机的隐患。  
  🔗 https://github.com/sipeed/picoclaw/pull/3323

- **[#3324] fix(weixin): use CreateSafeHTTPClient for media downloads**（已合并）  
  作者：SashaMIT  
  与 #3323 同源的修复，针对微信公众号通道的媒体下载做同样的 SSRF 加固。  
  🔗 https://github.com/sipeed/picoclaw/pull/3324

- **[#3321] fix(agent): move dynamic context after history to preserve prefix caching**（已合并）  
  作者：grrowl  
  将每请求动态上下文块从系统消息中移至对话历史之后，避免因前缀 token 变动导致前缀缓存全部失效。该优化可显著降低长对话场景下的推理延迟与成本。  
  🔗 https://github.com/sipeed/picoclaw/pull/3321

- **[#3320] fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)"**（已合并）  
  作者：grrowl  
  升级 `whatsmeow` 依赖，修复 WhatsApp 通道因客户端版本过期而被服务器拒绝连接（405）的问题，恢复该通道的可用性。  
  🔗 https://github.com/sipeed/picoclaw/pull/3320

> 合并 PR 小结：本轮 5 条合并中有 4 条为 Bug/安全修复，1 条为性能优化。安全方面横跨微信、企微、QQ、Telegram 等多个通道的 SSRF 防护已同步补齐；WhatsApp 通道恢复可用；Agent 推理前缀缓存得到有效利用。项目在通道安全一致性与运行稳定性方面迈进了扎实一步。


## 4. 社区热点

过去 24 小时暂无高热度的讨论或争议性议题。

- 今日关闭的 [#3302（支持 MCP 服务器 OAuth 2.1）](https://github.com/sipeed/picoclaw/issues/3302) 与 [#3325（Telegram 表格富文本渲染）](https://github.com/sipeed/picoclaw/issues/3325) 均属于被 stale 机制自动关闭的旧需求，分别经过 4 条与 2 条评论的讨论后未获得推进，现已关闭。这说明这两项需求在当前维护优先级中偏低，或等待社区进一步推动。

- 新开放的 PR [#3344（手机配对远程 Agent 操控）](https://github.com/sipeed/picoclaw/pull/3344) 是当前唯一的新增活跃 PR，涉及新协议（gbr/1）与手机配对功能，尚需观察社区反馈。


## 5. Bug 与稳定性

今日无新报告 Bug。近期修复项回顾如下：

| 严重程度 | 问题描述 | 状态 | 修复 PR |
|---------|---------|------|---------|
| 高 | WhatsApp 通道连接后约 5 秒被服务器断开，报 `Client outdated (405)`，通道持续不可用 | ✅ 已修复 | [#3320](https://github.com/sipeed/picoclaw/pull/3320) |
| 中 | 多个通道（QQ/Telegram/Discord/LINE/Slack）入站媒体下载存在 SSRF 风险（可访问 loopback/内网地址） | ✅ 已修复 | [#3322](https://github.com/sipeed/picoclaw/pull/3322) |
| 中 | 微信通道媒体下载可被重定向至私有主机 | ✅ 已修复 | [#3324](https://github.com/sipeed/picoclaw/pull/3324) |
| 中 | 企业微信通道媒体下载存在同类 SSRF 隐患 | ✅ 已修复 | [#3323](https://github.com/sipeed/picoclaw/pull/3323) |


## 6. 功能请求与路线图信号

今日关闭的 2 条 stale 功能请求如下：

- **[#3302] 支持 MCP 服务器的 OAuth 2.1**（已关闭）  
  用户 sunboy0523 提出为 MCP 服务器接入 OAuth 2.1 认证支持，标明为 "Nice-to-Have / Enhancement" 而非核心功能。该请求已存在近 1 个月，社区讨论有限，短期内纳入路线图的概率较低，但 OAuth 2.1 本身是多 Agent 生态的重要演进方向。  
  🔗 https://github.com/sipeed/picoclaw/issues/3302

- **[#3325] Telegram 表格富文本渲染**（已关闭）  
  用户 As-tsaqib 指出 Telegram 通道目前仅通过 `sendMessage` HTML/MarkdownV2 发送消息，结构化 Markdown 表格退化为纯文本或代码块，未利用 Telegram Bot API 10.1 引入的原生表格 UI。属于体验增强类需求，目前未获维护者明确回应。  
  🔗 https://github.com/sipeed/picoclaw/issues/3325

**路线图信号**：新开放 PR [#3344](https://github.com/sipeed/picoclaw/pull/3344) 引入手机配对远程操控桌面 Agent 的能力，该方向若被接受，将把 PicoClaw 从纯聊天机器人框架向"可远程操控的 Agent 平台"延伸，或成为下一阶段的重要能力储备。


## 7. 用户反馈摘要

- **WhatsApp 通道不可用（已恢复）**：用户 grrowl 在 [#3320](https://github.com/sipeed/picoclaw/pull/3320) 中反馈 WhatsApp 通道因客户端版本过期持续不可用（连接后约 5 秒即被断开且不重连），该问题已通过依赖升级修复。

- **Telegram 表格体验欠缺**：用户 As-tsaqib 在 [#3325](https://github.com/sipeed/picoclaw/issues/3325) 中反馈 Telegram 消息中的 Markdown 表格未能以 Telegram 原生表格 UI 呈现，期待利用 Bot API 10.1 的富文本能力提升展示效果。

- **MCP OAuth 2.1 诉求**：用户 sunboy0523 在 [#3302](https://github.com/sipeed/picoclaw/issues/3302) 中提出 MCP 服务器需支持 OAuth 2.1 认证，以满足更安全的授权流程，但该需求目前社区参与度有限。


## 8. 待处理积压

- **[#3222] refactor(deltachat): cleanup implementation, documentation -200LOC**（开放中，已超 8 周）  
  作者 trufae 于 2026-07-03 提交的 DeltaChat 通道重构 PR，涉及删除遗留特性、引用官方 relay 列表、移除密码式邮箱配置（改为 jsonrpc 密钥管理）等，代码量缩减约 200 行。该 PR 已挂起超 1.5 个月，建议维护者尽快审阅，以避免长期分叉带来合并冲突成本。  
  🔗 https://github.com/sipeed/picoclaw/pull/3222

---

**总结**：PicoClaw 今日无新版本发布，24 小时内以修复合并为主，安全加固（SSRF）横跨多通道、WhatsApp 通道恢复、Agent 前缀缓存优化均已落地；2 条 stale 功能请求自动关闭，新开放的手机配对 PR 值得关注。项目整体健康度良好，合并节奏稳定。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-24

## 1. 今日速览

NanoClaw 项目今日活跃度极高，24小时内共产生 6 条 Issue 更新和 50 条 PR 更新，其中 PR 更新数量显著超出日常水平，表明项目正处于密集开发期。核心维护团队（core-team）在 Chat SDK 升级、pnpm 依赖门控和 typing-indicator 生命周期等方面进行了大规模重构（以 PR stack 形式提交），同时社区贡献者提交了若干高价值修复。值得关注的是，今日新增的 3 个 Issue（#3498、#3497、#3455）均涉及 macOS 兼容性和会话稳定性问题，其中有 2 个被标记为高严重度且无自动恢复机制，建议维护者优先排查。总体而言，项目处于高速迭代通道，但稳定性问题需要及时消化。

---

## 2. 版本发布

今日无新版本发布（最新 Release 停留在 v2.3.0，即 PR #3495）。

⚠️ **注意**：PR #3496（[链接](https://github.com/nanocoai/nanoclaw/pull/3496)）明确指出，自 2026-08-21 起新增的 hardened 安装已因镜像 label 校验失败而无法完成 setup，该 PR 作为临时止损方案已被合并（CLOSED）。若你正在部署新环境，请确保使用包含此修复的最新镜像。

---

## 3. 项目进展

今日共合并/关闭 20 个 PR，以下为关键进展：

### 3.1 Chat SDK 4.32.0 升级与 typing-indicator 机制（核心改动）
- **PR #3490**（[链接](https://github.com/nanocoai/nanoclaw/pull/3490)）、**PR #3491**（[链接](https://github.com/nanocoai/nanoclaw/pull/3491)）、**PR #3492**（[链接](https://github.com/nanocoai/nanoclaw/pull/3492)）构成一个 3 层 PR stack（`main` 分支）：
  - **#3490**：将 chat core 依赖从 4.29.0 升级至 4.32.0，并锁定所有 Chat SDK 相关 channel skill 的版本（避免漂移）
  - **#3491**：新增 channel adapter 声明 typing-indicator 生命周期的能力，为不同渠道（如 WhatsApp 25 秒上限）提供精细控制
  - **#3492**：将 pnpm 的 `minimumReleaseAge` 门控从 `pnpm:` key 中提出并启用，附带回归测试
- 对应的 `channels` / `providers` 分支 twin PR（#3465、#3466、#3467、#3468、#3469、#3470、#3471）部分已合并，部分待处理。注意 **channels twin 需先于 main stack 合并**，否则会导致 registry 与主仓库不一致。

### 3.2 镜像 pin 修复（停止损失）
- **PR #3496**（[链接](https://github.com/nanocoai/nanoclaw/pull/3496)）：将镜像重新 pin 到 `hardened-2026-08-23`，并允许良性 lock 漂移。这一合并解决了 8 月 21 日以来新安装环境无法 setup 的问题。

### 3.3 其他已合并 PR
- **PR #3495**（[链接](https://github.com/nanocoai/nanoclaw/pull/3495)）：v2.3.0 release PR（版本bump + changelog 整理）

---

## 4. 社区热点

今日社区讨论集中在两个方向：

### 4.1 Discord approval 卡片按钮失效（#3456）
- **Issue #3456**（[链接](https://github.com/nanocoai/nanoclaw/issues/3456)）在 1 天内获得 1 条评论即被关闭。问题描述：`ask_question` 卡片构建器中按钮同时设置 `id` 和 `value`，导致 Discord 的 `custom_id` 冗余，每次点击都解析为错误选项，造成静默拒绝 + 重复发送。严重度为 high。虽然已关闭，但使用者需要确认修复版本已发布。

### 4.2 PR stack 机制引发的讨论
多位 core-team 成员（amit-shafnir、gavrielc）提交了带有 "Stack 1/3"、"Stack 2/3" 标记的 PR。这种 PR 链模式需要合并顺序正确（从底部向上），否则 CI 和代码审查会混乱。社区成员或外部贡献者若有类似结构需求，可参考 PR #3490（[链接](https://github.com/nanocoai/nanoclaw/pull/3490)）中的描述了解约定。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| **High** | #3455（[链接](https://github.com/nanocoai/nanoclaw/issues/3455)） | poll-loop 心跳在 claim 与首个 SDK 事件之间未更新，导致 claim-stuck watchdog（60 秒）误杀正常繁忙的 turn，且**无自恢复机制**，会永久阻塞会话回复 | Open，无修复 PR |
| **High** | #3456（[链接](https://github.com/nanocoai/nanoclaw/issues/3456)） | Discord approval/ask_question 卡片按钮参数冗余导致功能不可用 | 已关闭（修复已合并） |
| **Medium** | #3457（[链接](https://github.com/nanocoai/nanoclaw/issues/3457)） | `insertMessage()` 使用 plain INSERT，重试投递同一 message id 会触发 UNIQUE 约束崩溃，表现为重复报错 | Open，无修复 PR |
| **Medium** | #3498（[链接](https://github.com/nanocoai/nanoclaw/issues/3498)） | macOS 上 `path.resolve()` vs `realpath` 混淆导致 update 控制器直接退出 0 而不执行 | Open，无修复 PR |
| **Medium** | #3497（[链接](https://github.com/nanocoai/nanoclaw/issues/3497)） | `better-sqlite3@13` 在 Node <22.14.0 上打开数据库即段错误，影响 macOS 用户 | Open，可考虑提升 Node 版本下限 |

### 特别注意
- #3497 和 #3498 均来自同一作者 brentkearney，且同为 macOS 相关问题，建议维护者统筹处理，或考虑在 setup 脚本中增加 macOS 兼容性测试。
- #3455 的高严重度 + 无自恢复特性可能导致用户会话永久卡死，建议优先处理。

---

## 6. 功能请求与路线图信号

### 6.1 明确的新功能 PR（已提交）
- **PR #3494**（[链接](https://github.com/nanocoai/nanoclaw/pull/3494)）：新增 Build Remote Agent（gbr/1 协议）手机配对适配器，允许手机旁观桌面 agent 运行。作者 LinespottingPrivate 提交，目前 Open 状态。
- **PR #3489**（[链接](https://github.com/nanocoai/nanoclaw/pull/3489)）：Codex provider 的结构化 setup-driver 认证，增强第三方 provider 接入能力。
- **PR #3355 / #3356**（[链接](https://github.com/nanocoai/nanoclaw/pull/3355)）：新增 Cursor Agent SDK 支持（skill + provider payload），但已滞留 5 天，可能需要更多 review 关注。

### 6.2 长期未合并的功能项（可行性信号）
- **PR #2301**（[链接](https://github.com/nanocoai/nanoclaw/pull/2301)）：添加 GitHub 轮询模式（无端口）集成，自 5 月 6 日提交至今已 3 个月未合并。适用于 NAT/防火墙后方的用户，有明确需求场景。
- **PR #3142**（[链接](https://github.com/nanocoai/nanoclaw/pull/3142)）：Signal 插件的附件转发修复，自 7 月 27 日提交，等待合并。

---

## 7. 用户反馈摘要

- **Discord 用户（DawoudIO）**：报告 approval 卡片不可用时明确指出"every click resolves to the wrong option"，说明问题直接影响核心审批流程，且产生了重复消息的连带效应——用户体验受损明显。
- **macOS 安装者（brentkearney）**：连续提交两个 macOS 相关 bug（update 控制器空转、better-sqlite3 段错误），反映出 macOS 作为开发环境的占比不可忽视，但当前兼容性测试覆盖不足。
- **Session 中断问题（DawoudIO）**：#3455 描述"retries repeat the exact same failure"，说明错误恢复路径本身无效，会给运维带来极大的排查负担。

---

## 8. 待处理积压

以下 Issue/PR 已存在较长时间且未获维护者响应，建议优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 等待天数 | 备注 |
|------|------|------|----------|----------|------|
| PR | #2301（[链接](https://github.com/nanocoai/nanoclaw/pull/2301)） | GitHub polling mode + OneCLI secret merge | 2026-05-06 | 110 天 | 功能完整，适合 NAT 用户 |
| PR | #2537（[链接](https://github.com/nanocoai/nanoclaw/pull/2537)） | pre-commit hooks（prettier/eslint/typecheck/vitest） | 2026-05-18 | 98 天 | 提升代码质量基础设施 |
| PR | #3142（[链接](https://github.com/nanocoai/nanoclaw/pull/3142)） | Signal 附件路径修复 | 2026-07-27 | 28 天 | 明确 bug 修复 |
| PR | #3355（[链接](https://github.com/nanocoai/nanoclaw/pull/3355)） | /add-cursor agent provider skill | 2026-08-19 | 5 天 | 新集成，需 review |

**维护者建议**：今日 PR 数量激增（50 条），但积压的 PR 中 #2301 和 #2537 已存在超 3 个月，建议在下一个 release 周期前清理一轮旧积压，避免社区贡献者流失。

---

*报告生成时间：2026-08-24 | 数据来源：NanoClaw GitHub Repository*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-24

**数据统计周期：** 2026-08-23 ~ 2026-08-24 | **数据来源：** GitHub

---

## 1. 今日速览

NullClaw 项目过去 24 小时整体活跃度中等偏低。仅有 1 条新 Issue 上报（[#991](https://github.com/nullclaw/nullclaw/issues/991)），系一个关于 MCP stdio 调用在 Proxmox 启动器锁下无限挂起的并发/死锁问题，已获 2 条评论，社区有一定关注但热度有限。PR 方面无任何新提交或合并，版本发布亦为空。总体判断：项目处于相对平稳期，核心维护活动集中在 issue 排查，社区反馈量处于低位。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

过去 24 小时无 PR 被合并或关闭，项目无新功能落地或代码变更进入主干。结合当前 Issue 活跃度来看，项目当前正处于开发间歇期，建议关注后续几日的 PR 活动以判断下一轮迭代节奏。

---

## 4. 社区热点

**唯一活跃 Issue：[#991 — MCP stdio calls can hang indefinitely behind the Proxmox launcher lock](https://github.com/nullclaw/nullclaw/issues/991)**

- 作者：locke1979 | 创建于 2026-08-23 | 评论 2 条
- **核心诉求：** 当独立运行的 `nullclaw agent` 尝试调用已被长期运行的 gateway 进程持有的 stdio MCP 服务器时，进程会无限期挂起，阻塞在 Proxmox 启动器的锁机制上。
- **使用场景：** Proxmox CT 环境中运行 NullClaw 2026.8.22，使用只读 Proxmox MCP 桥（148 个工具），同时运行 `nullclaw-gateway.service` 和独立 `nullclaw agent`。

社区对该问题的关注集中在进程间锁的竞争条件上，反映了多实例部署场景下资源互斥管理存在瓶颈。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | Fix PR 状态 |
|---------|-------|------|------------|
| 高 | [#991](https://github.com/nullclaw/nullclaw/issues/991) | MCP stdio 调用在 Proxmox launcher 锁下无限挂起 | ❌ 无修复 PR |

**技术要点：** 当两个 NullClaw 进程（gateway 与独立 agent）共享同一 stdio MCP 服务器时，launcher 的锁文件机制未正确处理锁已被占用的情形，导致第二次调用永久阻塞。这属于**并发环境下的稳定性缺陷**，可能影响多实例部署的用户。虽为个例报告，但若复现范围扩大，将直接影响依赖 Proxmox MCP 集的用户。

---

## 6. 功能请求与路线图信号

今日无新增功能请求。Issue [#991](https://github.com/nullclaw/nullclaw/issues/991) 虽属于缺陷报告，但其根因涉及 **stdio MCP 服务器的进程间锁管理策略**，未来或将推动以下方向的改进：

- **锁机制的容错处理：** 对锁已被占用的 stdio MCP 服务器进行超时处理或优雅降级，而非无限等待；
- **多实例协调能力：** 支持同一 MCP 服务器的多客户端共享，或引入锁等待时间可配置化。

建议维护者关注该 Issue 的进展，若收到更多类似报告，应优先安排锁机制的修复。

---

## 7. 用户反馈摘要

来自 Issue [#991](https://github.com/nullclaw/nullclaw/issues/991) 的评论反馈显示：

- **用户痛点：** 在容器化环境（Proxmox CT）中同时运行 gateway 和独立 agent 是常见的使用方式，但目前多进程共享 MCP 资源存在缺陷，导致需要手动干预（如重启服务或释放锁）才能恢复；
- **使用场景：** 148 个工具的只读 Proxmox MCP 桥配置较复杂，用户倾向于让 gateway 常驻管理 MCP 连接，而按需调用独立 agent 执行任务——该模式一旦触发锁冲突即挂起；
- **满意之处：** 报告描述详尽，附带了完整的环境、版本和复现步骤，说明用户对项目有一定容忍度并愿意提供高质量反馈。

---

## 8. 待处理积压

**当前无长期未响应的重要 Issue 或 PR。**

> ⚠️ **风险提示：** 今日唯一活跃 Issue（#991）目前处于无维护者回复的状态。该问题涉及高严重度的并发缺陷，若超过 72 小时无官方回应，建议标记为需优先处理，防止用户因长时间无响应而产生流失。

---

**项目健康度评估：** 稳定 ████████░░ 8/10

- ✅ 社区报告质量高，反馈规范
- ✅ 无版本回退或急性回归问题
- ⚠️ 并发模块存在潜在稳定性风险
- ⚠️ 维护者响应速度待观察（当前 1 个未响应 Issue）

*本报告由 AI 自动生成，数据截至 2026-08-24 00:00 UTC。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-24

## 1. 今日速览

IronClaw 过去 24 小时保持高度活跃：**9 条新 Issue 与 23 条 PR 更新**，其中 18 条 PR 待合并、5 条已关闭。核心开发集中在三大方向：**持久化沙箱运行时**（#7732 epics 推进、#7810 凭据绑定落地）、**CI 基础设施重建**（四条并行轨道 T1-T4：#7821、#7817、#7819、#7809 齐头并进）、以及**基于用户真实数据的建议生成**（#7812/#7833 配套推进）。值得关注的是，三条来自 Slack 产品反馈渠道的 Issue（#7828/#7829/#7830）报告了 **Gmail、Slack、Notion 第三方集成安装/认证失败**，指向扩展生态的稳定性短板。项目整体健康度良好，主干功能迭代与工程质量修复双线并进。

---

## 3. 项目进展

今日无正式合并 PR（5 条关闭均为 dependabot 依赖更新），但 **18 条待合并 PR 中有 4 条核心功能/基建推进**，值得重点关注：

### 核心功能推进（待合并）

| PR | 规模/风险 | 内容 | 状态 |
|---|---|---|---|
| [#7810](https://github.com/nearai/ironclaw/pull/7810) | XL / low | **沙箱凭据绑定**：完成每用户持久沙箱运行时，通过托管代理实现 `gh` 等 CLI 的直接凭据中介——命令只见随机占位符，代理仅在 `api.github.com` 调用时替换真实 token | 待合并 |
| [#7833](https://github.com/nearai/ironclaw/pull/7833) | M / low | **建议生成基于用户真实数据**：关闭 #7812，将建议生成的硬编码能力白名单改为用户自己的只读已授权工具，使建议卡片能读取 Gmail 等实际内容 | 待合并 |
| [#7818](https://github.com/nearai/ironclaw/pull/7818) | XL / low | **后台子代理模式**（slice 2b+2c）：receipt 生成、逐子级投递、激活与修复扫描，为 #7788 启用的后台模式补齐生产者侧 | 待合并 |
| [#7826](https://github.com/nearai/ironclaw/pull/7826) | XL / low | **Hub 包安装修复**：解决 4 个目录项安装失败问题（legacy `capabilities.json` 强制、出口预算误绑、schema 引用不匹配） | 待合并 |

### CI 基础设施重建（四轨并行，均为待合并）

- **T1** [#7821](https://github.com/nearai/ironclaw/pull/7821)（XL/medium）：单一 setup-rust 复合组件，统一 toolchain pin、mold 链接器与构建配置
- **T2** [#7817](https://github.com/nearai/ironclaw/pull/7817)（XL/medium）：nextest 测试管道，全失败信号，PR 解除节流
- **T3** [#7819](https://github.com/nearai/ironclaw/pull/7819)（XL/medium）：PR/队列检查收敛，增加 planner drift 守卫与 PR 时 default-features clippy
- **T4** [#7809](https://github.com/nearai/ironclaw/pull/7809)（XL/low）：规范化 preflight 门禁，worktree 安全钩子，自打印 REPRO

另有两个**实验性 THROWAWAY PR**（[#7838](https://github.com/nearai/ironclaw/pull/7838)、[#7839](https://github.com/nearai/ironclaw/pull/7839)）专门用于验证 nextest 管道的 CI 行为（因为主 PR #7817 的 CI 因 diff 只触及 CI 配置文件而跳过了所有 Rust 测试通路），合并后即关闭。

> **整体评估**：CI 四轨重建项目（#7798/#7799/#7800/#7801）正在密集推进，预计将为项目带来显著的工程效率提升；沙箱与建议生成的用户数据打通标志着产品从"能力展示"走向"数据驱动"的关键转折。

---

## 4. 社区热点

今日讨论最集中的 Issue 是 **#7732**（[链接](https://github.com/nearai/ironclaw/issues/7732)），9 条评论，这是持久化沙箱的 epic 跟踪 Issue，涵盖了当前对每用户持久沙箱 + iron-proxy 的完整规划，并明确**推迟** loop executors。社区讨论围绕沙箱架构的演进路径展开，且 #7810 正是该 epic 的落地实现之一。

另一个值得关注的热点是 PR **#7831**（[链接](https://github.com/nearai/ironclaw/pull/7831)，Design System Phase 3a 基础——Chromatic 可视化回归通道 + 缺失的 design-token 轴），由 regular contributor rdisandro 提交，首次为 WebUI 重皮肤引入可视化回归测试面，预示着 WebUI 即将迎来大规模样式更新。

---

## 5. Bug 与稳定性

今日共报告 **4 条 Bug/集成故障**，均来自端用户反馈，无崩溃级问题：

| 严重程度 | Issue | 描述 | 是否有 fix PR |
|---|---|---|---|
| **高** | [#7830](https://github.com/nearai/ironclaw/issues/7830) | **Notion 扩展无法安装**：用户在 IronClaw 中安装 Notion 工具失败 | 无，待调查 |
| **高** | [#7829](https://github.com/nearai/ironclaw/issues/7829) | **Gmail WebUI 认证弹窗秒消失**：扩展注册表中配置 Gmail 时，Google 认证弹窗出现约 1 秒即消失，导致设置无法完成 | 无，待调查 |
| **中** | [#7828](https://github.com/nearai/ironclaw/issues/7828) | **NEAR Foundation 账户 Slack 设置阻塞**：至少一个 `@near.foundation` 账户无法完成 Slack 连接 | 无，待调查 |
| **中** | [#7826](https://github.com/nearai/ironclaw/pull/7826) | **Hub 包安装失败**（4 个目录项）：legacy `capabilities.json` 强制、出口预算误绑定、schema 引用不匹配 | ✅ PR #7826 已修复 |

> **分析**：Gmail/Notion/Slack 三类集成配置失败集中出现，可能指向扩展注册表中 OAuth 流程的共性问题（弹窗生命周期、回调路由或 token 存储）。建议维护者优先排查扩展认证框架层。

---

## 6. 功能请求与路线图信号

### v1.4.0 Epic 明确推进

[#7732](https://github.com/nearai/ironclaw/issues/7732) 作为 v1.4.0 的 epic，明确规划了**持久化每用户沙箱 + iron-proxy** 的完整架构，当前实现状态：
- ✅ 已落地：`builtin.shell` 通过 Docker 路由（#7810 进一步实现了 gh 凭据绑定）
- ⏳ 待做：`/workspace` 按 `(tenant, user)` 持久化、loop executors 推迟

### 新功能信号

| 信号 | 来源 | 说明 |
|---|---|---|
| **建议生成接入用户数据** | Issue [#7812](https://github.com/nearai/ironclaw/issues/7812) + PR [#7833](https://github.com/nearai/ironclaw/pull/7833) | 建议卡片不再基于硬编码白名单，而是用户已授权的真实工具数据。大概率进入下一版本 |
| **工具可用性过滤** | Issue [#7836](https://github.com/nearai/ironclaw/issues/7836) | 模型可见的工具面应过滤掉"当前部署中无法执行"的能力，避免注定失败的调用。PinchBench 已有实测数据支撑 |
| **沙箱出口认证原生支持** | Issue [#7825](https://github.com/nearai/ironclaw/issues/7825) | 将 GitHub 专用 credential carve-out 升级为通用 iron-proxy + host credential broker 方案 |
| **WebUI 设计系统 Phase 3** | PR [#7831](https://github.com/nearai/ironclaw/pull/7831) | 引入 Chromatic 可视化回归 + 设计 token 轴，为 WebUI 重皮肤铺路 |

---

## 7. 用户反馈摘要

今日来自 Slack 产品反馈渠道的 3 条 Issue（#7828/#7829/#7830）与 2 条 triage Issue（#7827/#7832）集中反映了**端用户配置第三方集成的真实痛点**：

- **Gmail 设置失败**："弹出窗口（我猜是 Google 账户认证）出现大约 1 秒就消失了"——认证弹窗生命周期异常，用户无法完成 OAuth 流程
- **Notion 无法安装**："Notion 工具不想安装到我的 IronClaw"——安装流程存在未知阻断
- **Slack 设置阻塞**："无法在我的 NEAR Foundation 账户 IronClaw 中设置 Slack"——特定组织账户下连接失败

此外，PR #7833 的评论指出此前的建议生成"只能看到你*有* Gmail，但从未读过一条消息"，反映了用户对建议**个性化与数据驱动**的期待。

---

## 8. 待处理积压

| 类型 | 编号 | 持续时间 | 说明 |
|---|---|---|---|
| PR | [#7020](https://github.com/nearai/ironclaw/pull/7020) | 22 天 | tokio-tungstenite 0.29→0.30 依赖升级，长期未合并 |
| PR | [#7255](https://github.com/nearai/ironclaw/pull/7255) | 19 天 | APDD 治理框架评估文档，由 regular contributor 提交，review 周期较长 |
| PR | [#7516](https://github.com/nearai/ironclaw/pull/7516) | 12 天 | WebUI 操作员面新增 IronHub agent 链接面板（new contributor neo-sky），仍在 review 中 |
| Issue | [#7732](https://github.com/nearai/ironclaw/issues/7732) | 6 天 | v1.4.0 epic 持续活跃，9 条评论，讨论热络 |

**维护者提醒**：#7020 的 tokio-tungstenite 升级已搁置超过三周，如无兼容性问题建议尽快合并或明确关闭原因；#7255 的 governance 评估文档等待时间较长，建议加速 review 以避免贡献者流失。

---

*本日报数据截至 2026-08-24，来源：IronClaw GitHub 仓库。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-24

**数据统计周期**：2026-08-23 00:00 — 2026-08-24 00:00


## 1. 今日速览

过去24小时内，LobsterAI 项目的 GitHub 动态集中在**历史遗留问题的收尾**：4 条 Issues 与 3 条 PR 全部处于关闭/合并状态，且均标记为 stale（过期）。无新 Issue 开启、无新 PR 提交、无新版本发布。这表明项目当前处于**低活跃度清理期**——社区近5个月的反馈（集中在4月1日提交）被统一归档处理，但其中多个问题（如模型 key 泄漏、NIM 群名 bug）在关闭前已有对应修复 PR 落地。项目健康度整体稳定，但**没有新功能开发和迭代信号**，建议关注后续发布节奏。

> 注：所有条目更新于 2026-08-23，创建于 2026-04-01，距今已近5个月，非当日新增。


## 2. 版本发布

无新版本发布。


## 3. 项目进展

过去24小时内有 3 个 PR 被关闭/合并，全部为 stale 状态（创建于 2026-04-01）：

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#1197](https://github.com/netease-youdao/LobsterAI/pull/1197) | Feature/Agent 管理页面交互优化 | CLOSED | 优化 Agent 管理页面交互路径，解决删除操作层级过深问题；基于旧 PR #1176 修复主分支冲突 |
| [#1199](https://github.com/netease-youdao/LobsterAI/pull/1199) | feat(model): add context window and token settings | CLOSED | 新增模型级上下文窗口与最大 Token 配置，持久化至设置并在模型列表中展示，同步注入 Cowork/OpenClaw 配置 |
| [#1201](https://github.com/netease-youdao/LobsterAI/pull/1201) | [Bug] NIM 超大群消息中 teamTypeNum 硬编码错误修复 | CLOSED | 一行修复 `nimGateway.ts` 中 teamTypeNum 硬编码错误，关联 Issue #1200 |

**项目推进程度评估**：两个功能向 PR（Agent 管理交互优化、模型级 token 配置）已合并，意味着下一版本有望包含这两项用户可感知的改进。Bug 修复 PR 保证了即时通讯场景下群名解析的正确性。**但需注意**：所有 PR 从创建到关闭跨越近5个月，实际合并时间点与关闭时间可能不一致，需确认这些改动是否已进入主线分支。


## 4. 社区热点

由于过去24小时内无活跃讨论，以下为被关闭 Issues 中最受关注的内容：

**[#1202] agent 泄漏 model key 信息（安全风险）** — 评论 2 条
- 链接：https://github.com/netease-youdao/LobsterAI/issues/1202
- 核心诉求：用户向 agent 询问 key 配置信息，agent 不仅透露配置文件位置，还进一步暴露环境变量中的模型 key，存在严重安全泄漏。
- **热点分析**：这是本周最值得关注的安全类反馈。Agent 的 prompt 设计未注入"敏感信息不披露"的安全指令，属于系统性防护缺失。当前无对应修复 PR，需要维护者优先处理。

**[#1198] 网关重启进度条消失，状态不可知** — 评论 2 条
- 链接：https://github.com/netease-youdao/LobsterAI/issues/1198
- 核心诉求：网关重启至一半时进度条消失，后续对话全部报"模型不可用"，且浏览器服务识别存在不确定性。
- **热点分析**：反映重启流程的用户体验和状态反馈设计缺陷，用户无法判断是正常等待还是异常卡死。

其余两个 Issues（#1196 工作目录强制生成 6 个文件、#1200 NIM teamTypeNum 硬编码错误）评论数均为 2，属于典型的使用体验和功能性 Bug。


## 5. Bug 与稳定性

过去24小时内共报告 4 个 Bug（全部为 stale 关闭状态），按严重度排列如下：

| 严重度 | Issue | 描述 | 是否有修复 PR |
|---|---|---|---|
| 🔴 **严重（安全）** | [#1202](https://github.com/netease-youdao/LobsterAI/issues/1202) | agent 可被诱导泄漏模型 key 信息，存在敏感信息泄漏风险 | ❌ 无 |
| 🟠 **高** | [#1200](https://github.com/netease-youdao/LobsterAI/issues/1200) | NIM 超大群中 `teamTypeNum` 硬编码错误导致群名获取失败 | ✅ [#1201](https://github.com/netease-youdao/LobsterAI/pull/1201)（已关闭） |
| 🟡 **中** | [#1198](https://github.com/netease-youdao/LobsterAI/issues/1198) | 网关重启进度条消失，状态不可知，后续对话报"模型不可用" | ❌ 无 |
| 🟢 **低** | [#1196](https://github.com/netease-youdao/LobsterAI/issues/1196) | 强制在工作目录生成 6 个 Agent 配置文件，目录混乱 | ❌ 无 |

**特别提醒**：#1202 的 model key 泄漏问题目前仍无修复 PR，且涉及安全合规，建议维护方尽快评估 prompt 加固方案，防止用户 API 密钥被套取。


## 6. 功能请求与路线图信号

已关闭 PR 中的功能改进：

- **[#1199](https://github.com/netease-youdao/LobsterAI/pull/1199) 模型级上下文窗口与 Token 配置**：为每个模型单独设置 contextWindow 和 maxTokens，并在直连聊天中生效，同时同步至 Cowork/OpenClaw 配置。这是提升高级用户可控性的明确信号。
- **[#1197](https://github.com/netease-youdao/LobsterAI/pull/1197) Agent 管理页面交互优化**：将删除操作从"卡片→详情面板"缩短为一步直达，降低操作成本。

上述两项功能若已合并至主线，将成为下一版本的主要用户可见更新。

结合已关闭 Issue #1196（用户希望参考 Cursor 设计全局 agents.md），社区对 **Agent 配置文件的心智模型**仍有优化空间，后续可考虑支持全局与项目级配置分离。


## 7. 用户反馈摘要

综合 Issues 评论与描述：

- **满意点**：用户对 Agent 管理页面交互优化的方向表示认可（PR #1197 为二次提交），说明社区对提升操作效率持欢迎态度。
- **痛点 1 — 目录污染**（#1196）：强制在工作目录生成 AGENTS.md、USER.md 等 6 个文件，用户反馈"太乱了，删了还要重建"，期望建立公共配置或隐藏目录。
- **痛点 2 — 状态不透明**（#1198）：重启期间无进度反馈，用户无法区分正常等待与故障，直接影响可用性判断。
- **痛点 3 — 安全担忧**（#1202）：用户主动测试并成功套取模型 key 信息，安全防护需前置。
- **真实使用场景**：NIM 群聊场景下 @机器人获取群名失败（#1200），修复方案仅一行，但阻塞了群聊功能体验。

整体用户情绪偏向**功能可用性期待**，无激烈负面反馈。


## 8. 待处理积压

以下问题长期未获明确响应或修复，建议维护团队关注：

| 类型 | 条目 | 描述 | 待处理时长 | 建议 |
|---|---|---|---|---|
| Issue | [#1202](https://github.com/netease-youdao/LobsterAI/issues/1202) | agent 泄漏 model key 信息 | 近5个月 | **最高优先级**，需 prompt 安全加固，防止密钥被套取 |
| Issue | [#1198](https://github.com/netease-youdao/LobsterAI/issues/1198) | 网关重启进度条消失 | 近5个月 | 优化重启状态机，设置超时反馈 |
| Issue | [#1196](https://github.com/netease-youdao/LobsterAI/issues/1196) | 工作目录强制生成 6 个 Agent 配置文件 | 近5个月 | 可参考 PR #1199 的配置思路，引入全局/项目级配置分离机制 |

此外，**所有已关闭条目均标记为 stale**，建议维护方在关闭前确认修复是否已实际合入主线，避免"静默关闭"导致用户困惑。


**项目健康度总结**：功能开发与 Bug 修复在5月前已有产出，但当前观测窗口内无新 blood。核心风险集中在安全防护（#1202）和状态反馈（#1198）两个方向。建议保持每月至少一轮 issue 定期清理与状态同步，以维持社区信任。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-24

## 今日速览

过去24小时内，Moltis 项目保持中等活跃度：**3 条 Issue 更新**（2 条新开、1 条已关闭），**6 条 PR 全部处于待合并状态**，无新版本发布。值得关注的是，今日 PR 全部为 **bug 修复与稳定性改进**，覆盖内存嵌入编码器崩溃、MCP 客户端失效、递归打包 sidecar 缺失等关键问题，其中 `#1236` 直接修复了一个**可导致整个进程被终止的严重内存 bug**。Issue 方面，一个 **TLS+ALPN 协商导致 WebSocket 连接断裂** 的问题（#245）获得社区关注，而一项安全相关的 fail-closed 钩子策略请求（#1230）已正式关闭。项目整体处于**密集修 bug、补稳定性**的阶段，社区反馈的多个深层问题正在被逐一解决。

## 版本发布

过去24小时内无新版本发布。

---

## 项目进展

今日无 PR 被合并或关闭，**6 条 PR 全部处于待审查状态**。但从 PR 内容来看，项目正在推进以下关键改进：

- **`#1236`** — 修复本地 GGUF 内存嵌入编码器在超长 token 输入时导致整个 Moltis 进程崩溃的问题。该修复通过限制批次大小确保非因果编码器的完整输入适配上下文窗口。*（作者: rubenssoto — [查看 PR](https://github.com/moltis-org/moltis/pull/1236)）*
- **`#1231`** — 修复 MCP 服务器重启后工具桥持续使用已关闭客户端的问题。这会**导致活跃对话在服务器重启后工具调用失效**，直到下一次轮次重建注册表。*（作者: IlyaBizyaev — [查看 PR](https://github.com/moltis-org/moltis/pull/1231)）*
- **`#1234`** — 修复预构建发布版和 Docker 镜像中递归打包的 sidecar 文件（如 `quick_validate.py`）路径解析失败的问题。*（作者: IlyaBizyaev — [查看 PR](https://github.com/moltis-org/moltis/pull/1234)）*
- **`#1226`** — 为定时任务输出增加 `deliver_to_current_chat` 传递快捷方式，确保调度输出返回到发起对话的聊天渠道，同时保留话题/线程路由能力。*（作者: rubenssoto — [查看 PR](https://github.com/moltis-org/moltis/pull/1226)）*
- **`#1235`** — 规范化内置内存后端配置名称（`sqlite` → `builtin`），统一序列化逻辑。*（作者: rubenssoto — [查看 PR](https://github.com/moltis-org/moltis/pull/1235)）*
- **`#1233`** — 新增可选的 WhatsApp 文档摄取功能（下载并持久化入站文档字节），让代理能够实际访问文件内容。*（作者: rubenssoto — [查看 PR](https://github.com/moltis-org/moltis/pull/1233)）*

**整体判断**：尽管今日无合并，但待合并 PR 全部指向实际用户痛点，且修复方案针对性强。特别是 `#1236`（进程崩溃）和 `#1231`（MCP 工具失效）解决了两个会直接影响用户体验的严重问题，一旦合并将显著提升系统稳定性。

---

## 社区热点

### 1. Issue #245 — TLS+ALPN 导致 WebSocket 连接 405（2 条评论）
[查看 Issue](https://github.com/moltis-org/moltis/issues/245)

**背景**：当 Moltis 启用 TLS 时，ALPN 协议列表中的 `h2` 优先级过高，导致**全新浏览器连接协商出 h2 协议**，而 WebSocket 升级请求返回 405。已有标签页因 TLS 会话复用而幸免，但**每次页面刷新或新开标签页都会触发此问题**。

**社区反应**：该 Issue 最早创建于 2026-02-26，但今天仍有更新，说明问题在最新版本中依然存在。两条评论反映了用户对**WebSocket 在现代浏览器环境下的稳定性**有较高诉求。这是一个浏览器-TLS-ALPN 协议协商的底层问题，修复可能涉及调整 ALPN 协议优先级或对 WebSocket 升级请求做特殊处理。

**诉求分析**：用户期望在使用 TLS 的生产环境中，WebSocket 功能能够开箱即用——这是一个**直接影响生产可用性**的问题。

### 2. Issue #1230 — 安全钩子 fail-closed 策略（已关闭，1 条评论）
[查看 Issue](https://github.com/moltis-org/moltis/issues/1230)

**背景**：社区成员 `kantorcodes` 提出，Moltis 的 `BeforeToolCall` 等修改型钩子在运行时失败时**默认继续执行**（fail-open），这对作为安全边界的钩子来说是不够的。建议增加 opt-in 的 **fail-closed** 策略，当钩子执行失败（如 shell 钩子超时）时应阻断执行。

**结果**：该 Issue 已在今日关闭。其内容与 PR #1226（在传递解析中保留规范地址、拒绝错误路由）在安全思路上有呼应，说明项目正逐步强化安全边界。

---

## Bug 与稳定性

| 严重程度 | Issue/PR | 问题描述 | 状态 |
|---------|----------|---------|------|
| 🔴 **严重（进程崩溃）** | [PR #1236](https://github.com/moltis-org/moltis/pull/1236) | 本地 GGUF 嵌入编码器在 chunk/query 超过 512 tokens 时可**终止整个 Moltis 进程** | 待合并 ✅ |
| 🟠 **高（功能不可用）** | [Issue #245](https://github.com/moltis-org/moltis/issues/245) | TLS 下 ALPN 协商 h2 导致 WebSocket 升级返回 405，**刷新页面即断连** | 开放，无修复 PR |
| 🟠 **高（工具失效）** | [PR #1231](https://github.com/moltis-org/moltis/pull/1231) | MCP 服务器重启后，活跃对话工具调用**持续使用已关闭的客户端** | 待合并 ✅ |
| 🟡 **中（功能异常）** | [Issue #1224](https://github.com/moltis-org/moltis/issues/1224) | 共享 Slack 频道中工具停止工作（详情待补充） | 开放，无评论 |
| 🟡 **中（资源缺失）** | [PR #1234](https://github.com/moltis-org/moltis/pull/1234) | 预构建/Docker 中递归打包的 sidecar 文件路径解析失败 | 待合并 ✅ |
| 🟢 **低（配置不一致）** | [PR #1235](https://github.com/moltis-org/moltis/pull/1235) | 内置内存后端名称 `sqlite` 与可编辑配置值 `builtin` 不一致 | 待合并 ✅ |

**关键发现**：`#1236` 描述的是一个 **critical 级 bug**——当用户查询较长文档时，本地嵌入模型可直接击穿进程。该问题已被修复且 PR 待合并，机制明确（`n_batch` 超出 `n_ctx` 限制）。`#245` 则是一个**长期未解决**的协议层问题，自 2 月报告至今仍未关闭。

---

## 功能请求与路线图信号

### 1. 安全钩子 fail-closed 策略 → 已关闭（#1230）
用户希望 Moltis 在安全钩子执行失败时**默认阻断而非放行**。Issue 虽已关闭，但该需求可能已在内部路线图中被接受——建议维护者明确说明处理结果。这可能成为下一版本的安全增强点。

### 2. WhatsApp 文档摄取（#1233）
[查看 PR](https://github.com/moltis-org/moltis/pull/1233) 新增了 `download_inbound_do...` 配置项，按账户启用文档字节的下载与持久化。这是**用户明确需要的功能**——当前代理只能看到文档的标题和 MIME 元数据，无法获得实际内容。

### 3. 定时任务输出回传（#1226）
[查看 PR](https://github.com/moltis-org/moltis/pull/1226) 通过 `deliver_to_current_chat` 快捷方式，让定时任务输出**回到发起对话的聊天渠道**。这填补了调度任务与聊天会话之间的体验断裂，预期在 cron 功能用户中受欢迎。

**预判**：结合已有 PR，WhatsApp 文档摄取和定时任务输出回传**大概率进入下一版本**。安全钩子 fail-closed 虽已关闭，但作为安全核心需求，有较大概率在后续迭代中实现。

---

## 用户反馈摘要

| 来源 | 用户声音 | 关键洞察 |
|------|---------|---------|
| [Issue #245](https://github.com/moltis-org/moltis/issues/245) | *"WebSocket connections silently break on any fresh browser connection"* | TLS 环境的 WebSocket 稳定性是刚需，问题存在 6 个月仍未解 |
| [Issue #1230](https://github.com/moltis-org/moltis/issues/1230) | *"runtime hook failures currently degrade to continuation"* | 用户将钩子视为安全边界，接受 fail-open 意味着安全隐患 |
| [Issue #1224](https://github.com/moltis-org/moltis/issues/1224) | *"Tools stop working in shared Slack channels"* | 共享频道场景的工具可用性问题，可能是多租户/权限相关的边缘案例 |
| [PR #1234](https://github.com/moltis-org/moltis/pull/1234) | *"sidecar file 'scripts/quick_validate.py' not found in bundled skill"* | 预构建产物与源码行为不一致，影响发布版用户的技能创建体验 |

**共性**：用户最关心的是**生产环境下的可靠性**——无论是 TLS+WS 的协议层问题、钩子失效时的安全策略，还是打包资源的完整性。这些反馈也印证了 Moltis 正被较多地用于实际生产部署。

---

## 待处理积压

### 需关注的重要开放项

1. **[Issue #245](https://github.com/moltis-org/moltis/issues/245)（开放 6 个月）** — TLS+ALPN 导致 WebSocket 断连。**长期未修复**，影响所有启用 TLS 的生产环境用户，建议提升优先级。

2. **[Issue #1224](https://github.com/moltis-org/moltis/issues/1224)（开放 3 天，无评论）** — 共享 Slack 频道工具失效。尚无任何维护者回应，作为 bug 报告，建议至少确认复现并提供临时绕过方案。

3. **[PR #1226](https://github.com/moltis-org/moltis/pull/1226)（待合并 3 天）** — 定时任务输出回传。功能价值明确且实现完整，等待审查时间较长，建议尽快安排 reviewer。

4. **[PR #1231](https://github.com/moltis-org/moltis/pull/1231)（待合并 2 天）** — MCP 客户端失效修复。影响所有使用 MCP 服务器的用户，建议优先审查。

---

**总结**：Moltis 今日处于**稳定的 bug 修复节奏**中，社区反馈的主要痛点均有对应 PR 在途。最大隐患是 TLS+WebSocket 问题（#245）长期无主，建议项目维护者评估 PR #1236、#1231、#1234 三个修复的合并优先级，为下一个版本铺路。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# 🤖 CoPaw 项目动态日报 — 2026-08-24

> **数据口径**：过去 24 小时（2026-08-23 ~ 2026-08-24），数据来源为 GitHub 公开仓库。CoPaw 为 QwenPaw 的社区分支，本文以下使用 QwenPaw 指代主项目。

---

## 1. 📊 今日速览

项目今日活跃度**中等偏高**。过去 24 小时有 **5 条新 Issue** 和 **15 条 PR 更新**，其中 7 条 PR 待合并、8 条 PR 已关闭/合并。值得注意的信号：**「内存无限增长至 20GB+」**（#7222）、**「reload 后插件注册丢失」**（#7221）以及 **「对话中途停止后，下一次对话完全复现上一次逻辑」**（#7217）三条高价值 Bug 报告同时涌入，指向核心稳定性问题；同时，**skill-system 系列 PR（#7031/#7033/#7027/#7030/#7032）批量关闭**，表明该功能已完成正式合并。新版本发布数为 0，项目处于功能收尾与修复集中期。

**整体健康度**：⚠️ 一般（Bug 密度较高，但社区响应速度较快，多数 Issue 在 24h 内获得维护者或社区成员回复）。

---

## 3. 🚀 项目进展 — 今日合并/关闭的重要 PR

今日无新 Release，但有 **8 条重要 PR 关闭/合并**，覆盖四个关键方向：

### 3.1 Skill-System 动态技能加载（重点）
| PR | 说明 | 状态 |
|---|---|---|
| [#7033](https://github.com/agentscope-ai/QwenPaw/pull/7033) feat(skill-system): dynamic skill loading + auto-unload + frontmatter fix | 核心实现：技能可在运行时动态加载/卸载，修复 frontmatter 解析路径 Bug | ✅ 已合并 |
| [#7031](https://github.com/agentscope-ai/QwenPaw/pull/7031) 同上（并行 PR） | 与 #7033 内容一致的封闭 PR，确认最终合入路径 | ✅ 已关闭 |
| [#7027](https://github.com/agentscope-ai/QwenPaw/pull/7027) feat: auto-title-sync + skill-system cleanup | 会话标题自动同步 + 清理临时备份文件 | ✅ 已合并 |
| [#7032](https://github.com/agentscope-ai/QwenPaw/pull/7032) / [#7030](https://github.com/agentscope-ai/QwenPaw/pull/7030) feat(auto-title-sync) | 标题随 auto-memory 自动刷新，提升聊天历史可扫描性 | ✅ 已合并 |

> 🎯 **意义**：Skill-System 从「静态加载」→「运行时动态管理」，补上了 AI Agent 框架中「插件热插拔」的关键拼图，直接支撑后续工作区级插件能力的快速迭代。**#7221 的 Bug 报告恰好在同一时间出现，可能与本次重构引入的回归有关**（详见第 5 节）。

### 3.2 命令行修复
- [#6616](https://github.com/agentscope-ai/QwenPaw/pull/6616) **fix(cli): build a valid user message for the headless task command** — 修复 `qwenpaw task` 无法执行任务的Bug（`Msg.content` 类型不匹配）。首次贡献者提交，已合并。

### 3.3 Token 用量管护
- [#6220](https://github.com/agentscope-ai/QwenPaw/pull/6220) **fix(token_usage): don't persist an unseeded cache on shutdown** — 修复 TokenUsageBuffer 在未加载磁盘缓存时仍强制刷盘导致数据污染的问题。

### 3.4 Windows 兼容性
- [#6203](https://github.com/agentscope-ai/QwenPaw/pull/6203) **fix(utils): bound and hide the Windows tasklist liveness probe** — 为 Windows 进程探活命令增加超时与隐藏窗口（首次贡献者，已合并）。

---

## 4. 🔥 社区热点 — 讨论最活跃的 Issue/PR

### 🥇 #7221 — reload 后插件注册丢失（3 评论，热度最高）
[agentscope-ai/QwenPaw Issue #7221](https://github.com/agentscope-ai/QwenPaw/issues/7221)

**诉求**：`MultiAgentManager.reload_agent()` 在执行零宕机配置热更新后，会**丢失插件工作区级注册**（runtime hooks、modes、slash commands），必须重启才能恢复。由于 Zero-downtime reload 是运维高可用场景的核心能力，该 Bug 直接影响生产环境的配置变更流程。

**分析**：问题指向 `qwenpaw/app/multi_agent_manager.py` 的模块级状态管理。结合今日 Skill-System 合并的 PR 时间线，**疑似重构后 reload 路径未同步适配新注册机制**，建议维护者尽快确认关联性。

### 🥈 #7222 — 内存无限增长至 20GB+（2 评论）
[agentscope-ai/QwenPaw Issue #7222](https://github.com/agentscope-ai/QwenPaw/issues/7222)

**诉求**：qwenpaw-backend 运行 2 天后内存从数百 MB 攀升至 **20.7GB**，拖垮整机，且已排除与已知启动泄漏（#9）同源。复现条件是「重度文档处理负载 + 不重启进程」。

**分析**：运行时内存累积问题通常涉及缓存未清除、事件循环引用泄漏或大对象残留。**这是项目当前最严重的稳定性隐患**，同类长连接型 Agent 服务在此类场景下的内存泄漏往往是随用随涨，越晚修复越难定位。

---

## 5. 🐞 Bug 与稳定性 — 按严重程度排列

| 严重度 | Issue | 描述 | 是否已有 Fix PR |
|---|---|---|---|
| 🔴 **高** | [#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222) | 内存无界增长至 20GB+（运行 2 天），并非启动泄漏，而是运行时累计 | ❌ 暂无 |
| 🔴 **高** | [#7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) | **Peer closed connection without sending complete message body**（incomplete chunked read），长文本推理场景高频触发 | ❌ 暂无（用户等待官方确认超时机制） |
| 🟠 **中** | [#7221](https://github.com/agentscope-ai/QwenPaw/issues/7221) | reload_agent() 丢失插件工作区注册 | ❌ 暂无（但与今日合并 PR 存在时序关联） |
| 🟠 **中** | [#7217](https://github.com/agentscope-ai/QwenPaw/issues/7217) | 中途停止对话后，下一次对话完全复现上一次推理（无视新问题） | ❌ 暂无 |
| 🟡 **低-** | [#6220](https://github.com/agentscope-ai/QwenPaw/pull/6220) | Token 未播种直接刷盘（已修复） | ✅ 已合并 |

> ⚠️ **特别关注 #7218**：用户反馈「自定义模型那边 180 秒超时，但 QwenPaw 在 130-140 秒就断开」，暗示框架侧存在**隐式超时或上游关闭连接的竞争条件**。长推理 + 自定义模型用户在等待响应时会被过早踢出，对生产可用性影响极大，且目前**尚无任何维护者回应**（1 条评论来自用户自己）。

---

## 6. 💡 功能请求与路线图信号

### 趋势判断：工作区级（Workspace-Scoped）能力是当前主线

| PR/Issue | 功能 |
|---|---|
| [#7183](https://github.com/agentscope-ai/QwenPaw/pull/7183)（OPEN） | **Skills 工作区级 always-on 预加载**：为专业 Agent 的固定行为提供常驻指令 |
| [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)（OPEN） | **Session-scoped 多项目目录**：一个对话绑定多个项目目录（首个为 primary），文件工具和 shell 默认 `cwd` 基于 primary 解析 |
| #7221（Bug） | reload 后插件工作区注册丢失 —— 从侧面印证工作区级功能已是用户高频使用路径 |

这三条信号共同指向：**用户希望 Agent 在不同工作区/项目上下文之间切换时，插件与技能绑定关系能够持久化、可热更新**。若 #6976（多项目目录）进入主干，配合 #7183（always-on 技能），将构成「专业工作流」的基本框架。

> 🎯 建议维护者关注：**#6976 已开放 11 天无评论**，但功能定义清晰、与现有架构契合度高，可能存在实现复杂度较高的顾虑，建议与 #7221 一并评估。

---

## 7. 🗣️ 用户反馈摘要

从今日 Issue 评论中提炼的真实用户痛点：

| 来源 | 核心反馈 |
|---|---|
| [#7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) | **「我问了 qwenpaw，没有这样的设置啊？有吗？」** — 用户疑似在查阅文档后仍无法找到超时配置项，对框架是否暴露了超时控制存在困惑。说明**超时相关配置的可发现性不足**，或框架存在未文档化的隐式超时。 |
| [#7217](https://github.com/agentscope-ai/QwenPaw/issues/7217) | 对话中断后状态残留，下一次对话完全复现上一次的思考链路 —— **会话状态清理机制存在缺陷**，用户对「为什么我问什么它都按上次的答」感到困惑。 |
| [#7224](https://github.com/agentscope-ai/QwenPaw/issues/7224) | 俄语用户询问如何将 **Aider CLI 作为 Agent 接入 QwenPaw**。说明社区对「外部 CLI 工具作为子 Agent」存在真实需求，当前缺乏官方集成文档。 |
| [#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222) | 用户愿意提供完整日志与复现环境 —— 表明社区奉献度较高，且该问题确实影响重负载用户。 |

**正面信号**：尽管 Bug 多，但**用户愿意主动提供完整报错文件**（#7218）、**提供复现环境**（#7222），说明核心用户对项目有耐心与信心。

---

## 8. ⏳ 待处理积压 — 长期未响应的重要议题

| 议题 | 搁置天数 | 重要性 | 建议 |
|---|---|---|---|
| [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976) feat: session-scoped multi project directories | **11 天**（8/13 创建，无评论） | 🔴 高 —— 用户对多项目工作流的核心诉求，与 #7183/#7221 形成完整功能闭环 | 建议维护者给出评审意见或状态说明，避免核心功能 PR 失温 |
| [#7066](https://github.com/agentscope-ai/QwenPaw/pull/7066) fix(drivers): persist rotated refresh_token for OAuth2 auth-code providers | 8 天（Under Review） | 🟠 中 —— MCP OAuth2 旋转 refresh_token 不持久化，远程 MCP 服务器（如 XMind）会在 5 分钟窗口外过期 | 长时间处于 Under Review 状态，建议安排 Reviewer 时间 |
| [#7183](https://github.com/agentscope-ai/QwenPaw/pull/7183) feat(skills): workspace-scoped always-on loading | 4 天（无评论） | 🟠 中 —— 与 #7221 直接关联（工作区级技能加载），建议优先关联审查 | 建议与 #7221 一并评估，避免 Bug 修复与功能开发脱节 |

---

## 📌 分析师评估总结

1. **Skill-System 合并是本周项目最大推进**，但**伴随而来的工作区级生命周期 Bug（#7221）是紧跟着的「报应」** —— 热更新机制与注册表管理需一并加固。
2. **内存泄漏（#7222）与断连 Bug（#7218）是阻碍生产部署的两大拦路虎**，前者可能需要在缓存层与事件循环引用上做系统性排查。
3. **社区正从「单项目使用」转向「多项目工作流」**，多目录会话、工作区级技能、外部 Agent 集成是未来 1-2 个版本的明显主线。
4. **建议维护者优先行动**：
   - 🔴 为 #7222 启动内存泄漏专项排查；
   - 🔴 明确 #7218 的超时控制语义（暴露配置还是修竞争条件）；
   - 🟡 对 #6976 给出评审时间表，避免 11 天无回应的 PR 流失去动力；
   - 🟡 调研 #7224（Aider CLI 集成）的文档需求，考虑新增官方集成指南。

---

*本日报由 AI 自动生成，数据截至 2026-08-24 00:00 UTC。所有链接指向 GitHub 原始 Issue/PR。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据 ZeroClaw 仓库 2026-08-24 日数据生成的项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-08-24

## 1. 今日速览

ZeroClaw 项目今日保持**高活跃度**，技术讨论与代码提交均十分密集。过去 24 小时内，Issue 与 PR 更新各达 50 条，显示社区参与度极高。当前开发重点集中在**架构层面的 RFC 讨论**（如会话持久化、附件架构、WASM 插件化）与**运行时稳定性修复**（如文件系统监听、计划任务策略、Provider 生命周期）。虽然今日无新版本发布，但多条高价值 PR（如 #10217 文件系统监听修复）已合并，且多条大型重构 PR（如 #10246、#10289）处于开放状态，预示着项目正在进行深层次的结构优化与治理规范化。

## 2. 版本发布

今日无新版本发布 (Releases: 0)。

## 3. 项目进展

今日合并/关闭的 PR 数量较少（5 条），但其中包含关键修复，标志着项目在稳定性上迈出坚实一步。

- **修复文件系统监听器** ([#10217](https://github.com/zeroclaw-labs/zeroclaw/pull/10217))：由 `JordanTheJet` 贡献，已关闭。该 PR 修复了文件系统通道监听器在空闲时会阻塞 Tokio 运行时工作线程的问题，该问题已在 v0.8.4 的 Alpine 复现（对应 Issue #9666）。此修复对于提升 supervisor 关闭和重载的响应性是关键改进。

此外，多条高优先级 PR 正在推进中，虽未合并但进展显著：

- **重构：移除遗留节点传输** ([#10289](https://github.com/zeroclaw-labs/zeroclaw/pull/10289))：由 `Audacity88` 提交，旨在删除无调用方的遗留 HMAC 节点传输协议及相关配置，简化运行时架构。
- **核心修复：向会话暴露已配置的通道** ([#10246](https://github.com/zeroclaw-labs/zeroclaw/pull/10246))：由 `Audacity88` 提交，解决了基于通道的工具无法访问为所选代理授权的通道的问题。

## 4. 社区热点

今日最热门的讨论集中在两个高关注度的架构 RFC 上，均获得了大量评论，反映出社区对核心架构演进方向的深度关切。

- **#9487 - RFC: 运行时拥有的会话与传输层适配器** ([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9487))：**25条评论**。该 RFC 讨论了会话生命周期的所有权和传输层的抽象问题。
- **#9488 - RFC: 面向 Web 聊天和频道的统一附件架构** ([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9488))：**19条评论**。该 RFC 讨论如何统一不同渠道的附件处理。

**背后的诉求**：这两个大型 RFC 均涉及项目最核心的 `runtime`、`channel` 与 `gateway` 边界问题。高评论数表明社区对于诸如“谁拥有会话状态”、“如何统一处理消息附件”等基础架构问题存在广泛且深入的探讨。这与 #9600 (会话持久化契约所有权追踪器) 等 Tracker 相关联，显示出维护团队正试图通过正式流程（RFC）来收敛这些关键决策。

## 5. Bug 与稳定性

今日无新报告的 P0 级崩溃性 Bug，但存在几个 P1/P2 级别的稳定性问题，多数已有对应的修复 PR。

- **测试环境不稳定性 (P1)**：
    - **Hailo 测试日志关联失败** ([#10272](https://github.com/zeroclaw-labs/zeroclaw/issues/10272))：并行测试下，Hailo 集成测试会捕获其他测试发出的事件，导致非确定性失败。该问题与 PR [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109)（新增 Hailo-Ollama 支持）相关，需要在合并前解决测试隔离问题。

- **运行时功能缺陷 (P2)**：
    - **Cron 作业上下文缺失** ([#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105))：Agent 在由 cron 触发时，无法获取触发它的消息上下文，导致无法完成关联操作。状态为 `blocked`，目前仅有少量评论，可能需要更多关注。
    - **RPC/session 通道暴露** ([#10246](https://github.com/zeroclaw-labs/zeroclaw/pull/10246))：虽然是个 PR，但其修复的问题是一个核心 Bug——会话无法访问已配置的通道。该 PR 已创建但尚未合并。

- **已修复 (合并)**：
    - **文件系统监听器阻塞** ([#9666](https://github.com/zeroclaw-labs/zeroclaw/issues/9666))：对应的修复 PR [#10217](https://github.com/zeroclaw-labs/zeroclaw/pull/10217) 已合并，问题已解决。

## 6. 功能请求与路线图信号

今日新提交的 RFC 对未来的功能方向提供了强信号，主要集中在插件生态和自动化治理方面。

- **全面 WASM 插件架构** ([#10076](https://github.com/zeroclaw-labs/zeroclaw/issues/10076))：由 `NiuBlibing` 提出，该 RFC 描述了一个更宏大的 “一切皆插件” 蓝图，涵盖 hook、backend、capability 层。这可能会成为未来版本的核心特性。
- **加载 Agent Plugins 1.0 标准包** ([#9810](https://github.com/zeroclaw-labs/zeroclaw/issues/9810))：由 `NiuBlibing` 提出，该 RFC 旨在支持 vendor-neutral 的 `agent-plugins.org` 1.0.0 标准，允许加载社区打包的 `plugin.json` + `skills/` + `mcp.json` 包。这与 #10076 结合，表明项目正积极向标准化、可插拔生态演进。
- **网关支持原样透传消息** ([#10050](https://github.com/zeroclaw-labs/zeroclaw/issues/10050))：用户 `belumume` 提议新增一个网关路由，允许不经过 Agent 推理，直接将消息原样发送到已配置的频道。

这些功能请求与现有大量 `[status: accepted]` 的通道添加请求（如 Twilio SMS #6427, Zulip #6437）等共同构成了丰富的路线图。

## 7. 用户反馈摘要

从今日的 Issue 讨论中可以提炼出一些用户的核心痛点：

- **配置安全与灵活性**：用户 `rakaarwaky` 在 #8424 中表达了保护工作区内敏感文件（如 `.env`、`config.yaml`）的需求，认为当前的 `forbidden_paths` 机制不够用，需要支持工作区相对路径模式及 `.zeroclawignore` 文件。
- **连接稳定性与易用性**：
    - 用户 `tidux` 在 #6754 中反馈 ACP 网桥的自动配对流程过于脆弱，依赖一次性代码，缓存与目录绑定，在运维场景下易失败。
    - 用户 `irunmyway` 在 #2503（已关闭）中寻找 napcat/onebot 通道而不得，反映特定平台用户对集成功能的渴求。
- **真实场景的误报**：用户 `bitsbyritik` 在 #9825 中报告了一个安全检测器的“误报”案例——公链地址被高熵启发式算法误判为泄密而删改，导致支付请求 URL 无法使用。这个问题很有价值，指出了安全功能在真实场景下需要更精细的豁免机制。

## 8. 待处理积压

以下 Issue/PR 长期处于讨论或阻塞状态，建议维护者重点关注。

- **长期未决的关键架构 RFC**：
    - **#6996** ([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6996))：细粒度沙箱策略（文件系统与网络限制），自 2026-05-28 以来长期处于 `in-progress`，等待维护者审核。
    - **#6850** ([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6850))：将内存生命周期策略与存储后端解耦，同样自5月已来长期开放且需要作者行动。

- **状态为 `blocked` 的活跃工作**：
    - **PR #10169** ([链接](https://github.com/zeroclaw-labs/zeroclaw/pull/10169))：ADR-014 关于插件网络出口权限的文档，被阻塞。
    - **PR #9999** ([链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9999))：对 OpenAI 兼容 Provider 的终止响应分类，上游依赖 #9447，需要按序合并。
    - **Issue #9703** ([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9703))：关于异步子任务监管的“目标模式 v3” RFC，目前状态为 `blocked`。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*