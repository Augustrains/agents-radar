# OpenClaw 生态日报 2026-08-14

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-14 00:54 UTC

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

# OpenClaw 项目日报 — 2026-08-14

## 1. 今日速览

OpenClaw 项目今日保持高强度社区活跃度，过去 24 小时处理了 500 条 Issue 更新及 500 条 PR 更新。值得关注的是 **Issue 关闭率仅为 32.6%**（163/500），而 **PR 合并/关闭率则低至 21.2%**（106/500），反映出维护者审查带宽正面临较大压力，大量 PR 处于待审查状态（394 条待合并）。稳定性问题仍是社区关注焦点，**消息丢失**（message-loss）和**会话状态异常**（session-state）是今日讨论度最高的两个标签，出现在超过 15 条高热度 Issue 中。核心痛点多集中在 **subagent 编排可靠性**、**投递队列静默失败** 和 **cron 任务在特定 LLM 下的性能退化** 三方面。

---

## 2. 版本发布

过去 24 小时无新版本发布。当前可追踪的活跃修复批次集中在 `2026.7.1-2` 版本之后，涉及 `dev` 更新通道的 pnpm 兼容性故障（#123073）以及模型 fallback 后回复不投递的回归（#121605，已关闭，但需验证修复是否进入正式版）。

---

## 3. 项目进展

过去 24 小时共关闭/合并 106 个 PR，虽总体比例不高，但在以下方面有值得关注的推进：

**关键修复确认关闭：**

- **PR #123208**（已合并）— 修复 `models.list` 在聊天正常时却永久返回空列表的 bug。根因是 owner binding-flag 不匹配。该问题直接影响 Control UI 的模型选择器，属于 P1 高优修复。
- **PR #123381**（已合并）— 修复 Control UI 在 "All agents" 视图下为所选具体 agent 创建自动化时抛出 `AgentSelectionRequiredError` 的问题。
- **PR #123392** / **PR #123400**（已合并）— 修复 CI 中 Codex 测试分片所有权重复与丢失问题，恢复 `main` 分支的完整测试通过状态。

**处于待审查但形态已清晰的重要 PR：**

- **PR #120794** — 修复无界通道上下文数组/对象刷爆模型 prompt 的问题。由 `sanitizeContextJsonValue` 的审查反馈直接推动，对 token 消耗和上下文管理有直接影响，但当前标注 `📣 needs proof`，尚未收到确认用例。
- **PR #123397** — 统一服务端压缩门控定义，修复 OpenAI WebSocket 传输在压缩被拒后的恢复逻辑。与 #123398 配合可解决原生 OpenAI 用户 turn 反复失败问题。
- **PR #123378** — 修复无系统属主时插件清单不可用的问题（多 agent 安装场景）。标注 `👀 ready for maintainer look`。

总体而言，项目在前端 UI 细节与 CI 基础设施方面有小步修复推进，但**核心运行时稳定性的主要 PR 仍卡在维护者审查环节**，包括 5 月即提出的安全加固 PR #82950（至今已积压近三个月）。

---

## 4. 社区热点

过去 24 小时讨论热度最高的 Issue 反映了几个核心社区诉求：

### 热点 1：静默失败问题的持续发酵 — Issue #121058（92 条评论）
**链接：** https://github.com/openclaw/openclaw/issues/121058

已关闭的 #116277 未能真正解决静默回复失败问题。监控 cron 在 issue 关闭后仍持续记录新日志（含 8 月 9 日当天）——被追踪到 **"no queued reply payload"** 模式。社区对此高度关注：**issue 已关闭但问题仍在生产环境反复出现**，用户对修复有效性产生了怀疑。这可能是今日评论量最高的 issue。

### 热点 2：记忆信任分级 — Issue #7707（48 条评论）
**链接：** https://github.com/openclaw/openclaw/issues/7707

用户 `LumenLantern` 提出的功能请求：按来源（用户指令、网页抓取、第三方技能）为 agent 记忆条目打上信任级别标签。核心动机是**防御记忆投毒攻击**——恶意指令隐藏在不可信内容（如网页、第三方集成）中影响后续行为。该 issue 自 2 月提出至今已持续讨论半年，评论 48 条，被标注 `needs-security-review` 和 `needs-product-decision`，说明这是一个有安全影响的产品决策，社区讨论持续活跃但尚未落地。

### 热点 3：工具调用间隙的文本泄漏到消息通道 — Issue #25592（48 条评论 | 1 👍）
**链接：** https://github.com/openclaw/openclaw/issues/25592

Agent 在工具调用之间产生的内部处理文本（错误处理、处理确认、叙述等）被路由到了已激活的消息通道（Slack、iMessage 等），**形成可见消息，污染用户会话**。这对 UX 有显著负面影响——内部日志和失败执行结果不应推送为聊天消息。属于 P1 + `impact:session-state` + `impact:security` 的综合问题。

### 热点 4：Cron agent 在 DeepSeek 上停转 — Issue #121953（16 条评论）
**链接：** https://github.com/openclaw/openclaw/issues/121953

`[cron:<jobId> <name>] ` 前缀导致 DeepSeek API 边缘将该请求视为低优先级，使得 cron agent turn 停转数十秒至数分钟。**该问题揭示了模型提供方对消息前缀的差异化处理可能影响 OpenClaw 核心功能**，对多供应商兼容性有参考价值。

### 热点 5：多代理编排不稳定 — Issue #43367（13 条评论 | 1 👍）
**链接：** https://github.com/openclaw/openclaw/issues/43367

并发 `agents add` 导致配置覆写、session-lock 失败、子任务脱离父会话运行等系统性多代理不稳定的报告。该问题提出于 3 月，持续更新至 8 月，说明**多代理可靠性是长期存在但尚未根治的痛点**。

---

## 5. Bug 与稳定性

过去 24 小时报告的 Bug 按严重程度分级如下：

### 🔴 P0 / 亟需关注

| Issue | 标题 | 状态 | 标签 |
|-------|------|------|------|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | Silent reply failures despite #116277 closed | OPEN，92 评论 | message-loss，影响面最大 |
| [#123073](https://github.com/openclaw/openclaw/issues/123073) | `dev` 通道更新失败（EUNSUPPORTEDPROTOCOL on workspace:*） | OPEN，P1 | 升级通道直接不可用 |
| [#115421](https://github.com/openclaw/openclaw/issues/115421) | Schema 降级恢复隔离/清空状态 DB (cron jobs lost) | OPEN，P1 | data-loss，已 linked PR 但未合入 |

### 🟠 P1 / 高优（均有修复 PR 或清晰 repro）

| Issue | 标题 | 状态 | 备注 |
|-------|------|------|------|
| [#51028](https://github.com/openclaw/openclaw/issues/51028) | Session lane starvation (followup drain 20-30min) | OPEN，6 评论 | 影响 Discord/WhatsApp 等所有通道 |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 刷新超时（10s）| OPEN，9 评论 | cron/heartbeat 在刷新期间失败 |
| [#97983](https://github.com/openclaw/openclaw/issues/97983) | iOS/WebChat 消息不触发回复 | OPEN，9 评论 | 官方 iOS 应用核心链路问题 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | Hook/tool 子进程泄漏 → zombie 累积 | OPEN，7 评论 | 运行时逐渐降级，需要用户干预 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | Cron agent 在 DeepSeek 上停转 | OPEN，16 评论 | 与提供商前缀处理相关 |
| [#121605](https://github.com/openclaw/openclaw/issues/121605) | 模型 fallback 后回复从不投递（回归）| CLOSED | 值得验证修复是否真正进入发布版 |

### 🟡 P2 / 中优先

- [#43747](https://github.com/openclaw/openclaw/issues/43747) — "Memory management is in chaos"：同一团队 3 人使用，各自记忆存储机制不一致（SQLite vs 其他），反映**记忆子系统的实现分歧**。
- [#114612](https://github.com/openclaw/openclaw/issues/114612) — `memory_index_chunks` 和 `memory_embedding_cache` 表无保留策略，磁盘将随时间被填满，生产实例已有证据。
- [#95610](https://github.com/openclaw/openclaw/issues/95610) — OpenAI 模型路径下每轮动态注入（message tool hint + 易变 system prompt 段）**破坏了自动前缀缓存**，影响 token 成本。
- [#107814](https://github.com/openclaw/openclaw/issues/107814) — `gpt-5.3-codex-spark` 发出空参数的工具调用，被 schema 校验拒绝。

### ⚪ 基础设施/CI

- [#123400](https://github.com/openclaw/openclaw/pull/123400) 与 [#123392](https://github.com/openclaw/openclaw/pull/123392)（均已合并）— 修复 CI 分片所有权审计故障。虽不直接影响用户，但恢复 `main` 全量测试对合入质量保障有积极意义。

---

## 6. 功能请求与路线图信号

社区今日提出的功能请求多集中于以下方向：

**可能在近期进入里程碑：**

- **Issue #7707 — 记忆信任分级（Memory Trust Tagging）**：已存在 48 条讨论、6 个月未闭案，被多个安全相关标签覆盖。结合社区对记忆投递安全的持续关注，预计会进入较短周期路线图。相关线索：`needs-security-review` 与 `needs-product-decision` 的同时存在意味着需要一个产品层面的决策。
- **Issue #16555 — 投递队列消息 TTL/过期**：与投递队列恢复（#121058 等）问题呼应，增加 TTL 可防止陈旧条目在 gateway 重启后刷屏。该 issue 自 2 月提出，已有 6 条评论，在静默失败类问题持续发酵的背景下，此方向可能获得更多权重。
- **Issue #45758 — YAML 配置文件支持**：从 3 月 14 日提出至今持续获得讨论（8 条评论，2 👍）。社区用户在 DevOps 场景中更习惯 YAML，属于 UX 改善类需求。

**可能被下一版本吸收的 PR 信号：**

- **PR #123008 — 共享 Composer 组件**：重构 New Session 与 Active Chat 共用同一个 prompt composer，使 `/new` 获得与活跃会话一致的斜杠命令、`$skill` 补全、IME/键盘处理、附件等能力。预计进入 mid-term 里程碑。
- **PR #121562 — 托管向导设置回执内联渲染**：将设置流程的确认/取消状态以紧凑的只读回执形式呈现，提升 UI 反馈一致性。与 #114173（系统 agent 设置 QR 码）和 #119343（Gateway 自管 QR 会话）构成一个完整的设置流程 UX 改进套件。
- **PR #118169 — Signal 账户设置 QR 码关联/发现**（含 #119344 合并）——Signal 通道的 setup 体验正在经历系统性优化，预计在 2026.8 或 2026.9 版本落地。

**处于早期讨论、但代表用户心智模型变化：**

- **Issue #45771 — 内建感知节奏的限速**：来自长期用户 `o-shabashov`，希望 OpenClaw 自动感知 API 消耗节奏并主动限速。该需求在高度自动化场景中自然出现，但目前仍未进入核心路线图讨论，等待产品决策信号。
- **Issue #46058 — 聊天优先的 Android 面**：有用户已在独立 fork 验证了 chat-first 移动端体验，但明确表示**不请求上游合入整包**，而是询问维护者对窄场景适配上游化的态度。该信号值得关注但短期内不太可能成为官方方向。

---

## 7. 用户反馈摘要

根据今日活跃 Issues/PR 评论，提炼以下真实用户反馈：

**高频痛点（已有多人报告或集中讨论）：**

1. **消息静默丢失是最痛的问题**：Issue #121058 的直接描述是 "#116277 closed，但问题仍在发生"。（来自 `sloptop-the-terrible`）。结合 #44925（"no retry, no notification, no auto-restart"）、#67777（"silently lost"）和 #85714（agent 忘记调用投递工具后回复滞留），**多个高热度 issue 都指向同一个核心结论：失败场景缺乏可观测性与兜底机制**。用户在评论中频繁表达"这让我无法信任系统在无人值守时正常工作"的焦虑。

2. **子代理编排不可靠**：#44925（"Subagent completion silently lost"）、#43367（"makes multi-agent runs unreliable in practice"）和 #47975（"main session becomes unresponsive"）都指向同一类问题——**子代理在超时、并发、或会话失联时不通知父会话**。上游 3 月提出至今仍被关注，用户期望至少有一个可观测的状态和可靠的自动重启机制。

3. **多通道消息路由脏数据**：#25592（工具调用间隙的内部文本泄漏到聊天通道）和 #41165（Telegram DM 仍然落入主会话）反映了**通道隔离和消息过滤的不足**。尤其在群聊/多 agent 场景下，内部处理数据不应推给用户。

4. **升级/更新路径脆弱**：#123073（dev 渠道 EUNSUPPORTEDPROTOCOL）、#78493（sudo update 后混合属主、doctor 覆盖配置）、#42273（backup create 停滞）共同构成了**更新与运维链路的负面体验**。其中 #78493 来自 macOS LaunchAgent 场景，影响了自动化升级的信任度。

5. **iOS/WebChat 可靠性**：#97983（消息已 append 到 transcript 但不触发回复）——核心移动端链路在该 issue 中存在 3 个月以上未解决，用户包括开发者和非技术用户（官方 iOS 是其首选入口），响应需求急迫。

**对新增功能的正面反馈：**

- **#44431（已关闭）** 浏览器工具 7 项改进（来自真实世界自动化测试）——虽已关闭，但评论区的肯定反映出真实世界验证对产品方向的价值。
- **PR #123288**（会话活动指示器）在 UI 细节上获得社区积极的视觉反馈，评论区无实质争议。
- **#105342（已关闭）** exec 输出以图片渲染的问题——用户肯定该问题的修复方向（以文本渲染），但需要验证合入后是否触发回归。

**一个值得注意的矛盾信号：**

- **#43747 "Memory management is in chaos"** 是一个非常有趣的社区信号：团队三人各自使用同一版本 OpenClaw，**记忆存储的实现路径不同**（同一版本被不同运行环境差异化表现）。这暗示即使是"官方功能"，其跨平台/跨安装表现的一致性仍然是痛点。

---

## 8. 待处理积压

以下为长期未闭案的重要 Issue 或 PR，需要维护者优先释放审查带宽：

### 🔴 高优先级积压

| 编号 | 标题 | 提出日期 | 关键标签 | 备注 |
|------|------|----------|----------|------|
| [#82950](https://github.com/openclaw/openclaw/pull/82950) | fix(security): 防止不安全审批模式挂起命令授权 | 2026-05-17 | security, availability | **卡在 needs-proof 近 3 个月**，涉及正则灾难性回溯，直接影响授权可靠性 |
| [#72015](https://github.com/openclaw/openclaw/issues/72015) | active-memory 阻塞回复 + QMD 启动过载 | 2026-04-26 | crash-loop | 带完整复现和现场数据，无对应 PR |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 刷新在 cron/heartbeat 中失败 | 2026-06-02 | message-loss | 已 linked PR 但未合入，auth-provider 优先级高 |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用间隙文本泄漏到消息通道 | 2026-02-24 | security, session-state | 48 条评论说明社区需求明确，停留在 needs-product-decision |

### 🟡 中优先级积压

| 编号 | 标题 | 提出日期 | 关键标签 | 备注 |
|------|------|----------|----------|------|
| [#41165](https://github.com/openclaw/openclaw/issues/41165) | Telegram DM 落入主会话（#40519 后仍存在）| 2026-03-09 | diamond lobster | 已有 linked PR 但状态不明确，需推进 |
| [#115421](https://github.com/openclaw/openclaw/issues/115421) | Schema 降级恢复隔离/清空状态 DB | 2026-07-28 | data-loss | linked PR 未合入，数据安全高危 |
| [#54488](https://github.com/openclaw/openclaw/issues/54488) | Session lane starvation（20-30 分钟阻塞）| 2026-03-25 | diamond lobster | 磁盘上最老的阻塞类 bug 之一，影响面大 |
| [#91456](https://github.com/openclaw/openclaw/issues/91456) | Telegram DM 发送超时后通道仍被 guard（已关闭）| 2026-06-08 | diamond lobster | 虽已关闭但属于防御性修复，建议回看验证覆盖范围 |

### ⚪ 需决策的信号

| 编号 | 标题 | 提出日期 | 关键标签 | 建议 |
|------|------|----------|----------|------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 记忆信任分级 | 2026-02-03 | security, product-decision | 建议将产品决策会议排期，明确是否纳入路线图 |
| [#95759](https://github.com/openclaw/openclaw/issues/95759) | ACP sessions_spawn 静默失败（0 bytes transcript）| 2026-06-22 | message-loss | 涉及 ACP 生态完整性，建议分配 owner 跟进 |
| [#54488](https://github.com/openclaw/openclaw/issues/54488) | Session lane starvation | — | — | 需要维护者给出明确修复时间线，否则将持续被社区提及 |

---

> **分析师总结**：OpenClaw 在 AI Agent 基础设施方向持续获得高密度社区输入，核心问题集中在**可观测性不足导致的静默失败**。项目健康度中等偏上，但 394 条待合并 PR 的积压导致关键修复无法及时流入稳定通道。建议维护者优先释放安全与数据完整性类 PR 的审查，并在下个版本中明确回应社区对交付可靠性和消息投递保障的集体诉求。针对 #121058 等反复出现的"修了未修好"类问题，建议在 issue 模板中强制要求补充**修复后的验证时间段**与**失败现场日志**，以提升闭环效率。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：** 2026-08-14
**分析范围：** OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、NullClaw、IronClaw、LobsterAI、TinyClaw、Moltis、CoPaw、ZeptoClaw、ZeroClaw（共 13 个项目，其中 2 个无活动）


## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于**从"功能堆叠"向"工程化与安全加固"转型的关键阶段**。核心体现为三个特征：首先，**稳定性压倒新功能**——各项目（OpenClaw、NanoBot、ZeroClaw）的 PR 合并率普遍偏低（21%~50%），大量修复积压在审查环节，说明维护者带宽已跟不上社区输入，质量问题成为普遍瓶颈；其次，**供应链安全成为集体关注点**——NanoClaw 将镜像签名验证升级为强制门禁、ZeroClaw 合并 gateway 路径穿越修复、CoPaw 排查插件权限漏洞，安全不再只是单点补丁而是系统性工程；第三，**架构收敛信号明确**——IronClaw 将 ACP 从核心目标降级为众多 driver 之一、NanoBot 推进会话数据原子化、ZeroClaw 重构会话持久化契约，各项目开始收敛此前"百花齐放"的架构探索，向可维护、可扩展的成熟形态靠拢。整体生态呈现"高活跃、高积压、高安全敏感"的三高态势。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 | Release | 健康度评估 |
|------|------------|---------|-----------|---------|-----------|
| **OpenClaw** | 500 | 500 | 106 PR（21.2%）/163 Issue | 无 | ⚠️ **高活跃、高积压**：394 条 PR 待合并，安全 PR #82950 积压近 3 个月，消息丢失问题反复出现 |
| **NanoBot** | 12 | 31 | 9 PR | 无 | ✅ **优秀**：Cron 致命崩溃 8 小时内获 3 轮修复 PR，71% Bug 已有修复，响应速度最快 |
| **Hermes Agent** | 50 | 50 | 4 PR | **v0.20.1** | 🟡 **高活跃但质量承压**：TUI P1 问题持续 23 天无修复，656 个 PR 打包进补丁版本 |
| **PicoClaw** | 3 | 9 | 3 PR（关闭旧依赖更新） | 无 | 🟡 **平稳但响应偏慢**：Web UI 输入延迟 24 天未修复，前端构建阻塞 9 天待合并 |
| **NanoClaw** | 2 | 19 | 13 PR | **v2.2.0** | ✅ **工程纪律最佳**：供应链安全 CI 全线升级，核心团队主导，但外部社区参与度偏低 |
| **NullClaw** | — | — | — | — | ⚪ **无活动** |
| **IronClaw** | 50 | 50 | 多 PR（约 10 个） | **v1.2.0** | ✅ **战略推进清晰**：Epic #7482 完成 17 个子任务拆解，性能优化四连发，但用户侧 Bug（PDF MIME 25 天）未闭环 |
| **LobsterAI** | 1 | 11 | 5 PR | 无 | 🟡 **UI 重构活跃，测试积压明显**：5 条当日 PR 全部合入，但 4 条 3 月提交的 stale PR 悬而未决 |
| **TinyClaw** | — | — | — | — | ⚪ **无活动** |
| **Moltis** | 1 | 4 | 0 PR | 无 | 🟡 **维护响应积极但功能评审滞后**：3 个修复 PR 已就绪待合入，大型功能 PR #1190 3 天无评审 |
| **CoPaw** | ~70 | ~22 | 19 PR | **v2.1.0** | ✅ **快速迭代**：QwenPaw OS Shell 发布，但任务中断、安全报告等核心痛点集中 |
| **ZeptoClaw** | — | — | — | — | ⚪ **无活动** |
| **ZeroClaw** | 50 | 50 | 9 PR | 无 | ✅ **安全加固密集**：两个 P1 安全/并发修复合入，RFC 决策队列建立，v0.9.0 前集中加固 |

**活跃度分层：**
- **第一梯队（日更新 >50）**：OpenClaw、Hermes Agent、IronClaw、CoPaw、ZeroClaw
- **第二梯队（日更新 10-50）**：NanoBot、NanoClaw、LobsterAI、PicoClaw、Moltis
- **无活动**：NullClaw、TinyClaw、ZeptoClaw（可能已停止维护或处于休眠期）


## 3. OpenClaw 在生态中的定位

**生态位：** OpenClaw 是当前个人 AI 智能体赛道中**社区规模最大、讨论密度最高**的项目，单日 500 条 Issue + 500 条 PR 更新远超第二名（IronClaw、ZeroClaw 均为各 50 条）。其历史包袱也最大——394 条待合并 PR、静默失败问题半年内反复出现，反映大型开源项目在规模扩张后的典型治理困境。

**技术路线差异：**
| 维度 | OpenClaw | 对标竞品 |
|------|----------|----------|
| **核心架构** | 多 Agent 编排 + subagent 体系 + 全通道接入（Slack/iMessage/Telegram/Discord/WhatsApp） | NanoBot 更轻量；IronClaw 走"内核"路线（kernel + 外部 harness）；ZeroClaw 重 Matrix 生态 |
| **存储层** | 记忆子系统实现分歧（SQLite vs 其他），团队用户反馈"Memory management is in chaos" | NanoBot 依赖 JSONL 文件，正推进原子写；ZeroClaw 重构会话持久化契约；CoPaw 自研 ReMe 记忆系统 |
| **部署模式** | 本地优先，但支持 Control UI/多云模型 | CoPaw 有桌面版（QwenPaw OS Shell）；IronClaw 云托管；NanoClaw 强调 CLI 自动化 |
| **AI 供应商策略** | 多模型聚合，但与 DeepSeek 有兼容问题；OpenRouter session_id 支持待定 | Hermes Agent 也面临 DeepSeek 兼容性；IronClaw 已支持 Sonnet-5（NEAR AI Cloud）；CoPaw 关注阿里云百炼 |

**社区规模对比：**
- **Star 与贡献者密度**：OpenClaw 的 Issue/PR 日更新量是第二名的 10 倍，社区参与度断层领先
- **维护者带宽**：OpenClaw 日均处理 500 条 PR 更新，但合并率仅 21%，说明维护者数量与社区规模不匹配
- **用户信任度**：OpenClaw 因静默失败问题反复，社区信任度承压（"这让我无法信任系统无人值守时正常工作"）；NanoClaw 和 IronClaw 用户信任度相对更高（供应链安全机制完善 + 工程纪律强）


## 4. 共同关注的技术方向

### 方向一：消息投递可靠性与可观测性（最强烈信号）
- **涉及项目**：OpenClaw（#121058 静默回复失败 92 评论）、NanoBot（#5373 Cron 调度器持久化死亡）、Hermes Agent（#62142 verification-stop 丢弃流式回答）、ZeroClaw（#9674 会话队列序列化修复）、PicoClaw（Web UI 输入延迟）
- **核心诉求**：失败场景缺乏可观测性；静默丢失零容忍；异常需"可见、可追、可自动恢复"。
- **行业启示**：**消息投递的"至少一次 + 死信队列/重试"/"失败即报告"机制正成为下一代智能体的标配**。

### 方向二：供应链安全与依赖治理
- **涉及项目**：NanoClaw（签名验证强制门禁 + CSPRNG 配对码）、ZeroClaw（gateway 路径穿越修复 + Zhipu 凭据 fail-closed）、CoPaw（插件权限模型漏洞排查）、IronClaw（上游仓库迁移导致 sandbox build 失败）
- **核心诉求**：Agent 镜像签名验证、依赖版本固定、安全默认值（fail-closed）、上游迁移影响隔离。
- **行业启示**：**智能体安全从"应用层逻辑"下沉到"供应链基础设施"层面**。

### 方向三：长期记忆与上下文管理
- **涉及项目**：OpenClaw（记忆信任分级 #7707 48 评论 + 记忆存储实现分歧）、NanoBot（会话数据原子化）、ZeroClaw（记忆生命周期策略解耦 #6850 + session 持久化契约）、IronClaw（跨会话记忆不可靠 #7185）、CoPaw（ReMe 记忆系统 + ViBo 提案）、Hermes Agent（本地零依赖记忆层提案 #85418）
- **核心诉求**：记忆需要分级信任（防投毒）；跨会话可靠召回；存储一致性（避免"同一版本不同行为"）；记忆索引有生命周期管理（防磁盘爆满）。
- **行业启示**：**记忆正从"功能特性"升级为"系统级基础设施"**，信任分级和持久化契约是下一阶段主战场。

### 方向四：Web/桌面/移动端体验一致性
- **涉及项目**：Hermes Agent（TUI 覆盖层 23 天未修 + 桌面端 split-brain）、PicoClaw（Web UI 长历史卡顿）、CoPaw（Windows 桌面 TUI 连接失败）、OpenClaw（iOS/WebChat 消息不触发回复）、LobsterAI（UI 三视图统一）
- **核心诉求**：多端体验一致性；桌面端与 CLI 行为统一；移动端核心链路可靠。
- **行业启示**：**智能体从"API 优先"走向"全端覆盖"，但桌面/移动端仍是重灾区**。

### 方向五：多 Agent 编排与子任务可靠性
- **涉及项目**：OpenClaw（多代理编排不稳定 #43367 + subagent 编排可靠性）、CoPaw（任务中断 #6921 + 无限循环 #6768）、IronClaw（Epic #7482 可插拔 agent loops）、Hermes Agent（cron 任务锁定失效模型）
- **核心诉求**：子代理超时/失联时需通知父会话；任务执行边界定义（max_iterations 服务端强制）；可观测的当前任务状态。
- **行业启示**：**多 Agent 编排的"失败传播语义"是当前最不成熟的技术黑盒**。


## 5. 差异化定位分析

| 项目 | 定位 | 目标用户 | 核心架构特征 | 关键差异化 |
|------|------|----------|-------------|-----------|
| **OpenClaw** | 通用型全通道 AI 助手 | 技术爱好者 → 专业开发者 | 单二进制 + 多通道适配 + subagent 编排 + 插件系统 | 渠道覆盖最广（iMessage/WhatsApp/Discord/Telegram 等）；社区最大；生态最完整 |
| **NanoBot** | 轻量级会话即文档式助手 | 个人用户、小型团队 | 文件系统为底 + WebUI 为中心 + MCP 生态 | 会话原子化写入、Cron 健壮性、会话间 @引用（协作画布）；响应速度最佳 |
| **Hermes Agent** | 开发者工具型 Agent | 桌面端重开发者 | 桌面应用 + TUI + Cron + Webhook + 浏览器自动化 | 浏览器自动化（browser_exec）和插件体系；桌面端体验为核心场景 |
| **PicoClaw** | 超轻量嵌入式 Agent | 嵌入式/低资源场景 | Go 语言单机版 + Web 前端 | 极简部署、Arm 友好；但 Web 前端性能和功能覆盖偏弱 |
| **NanoClaw** | CLI 优先的自动化 Agent | DevOps/脚本化使用 | CLI 为主要交互面 + 模板化 Agent 组 + WebUI + ACP | 供应链安全最严格（签名验证门禁）；自动化/脚本场景深度优化 |
| **IronClaw** | 智能体调度与安全内核 | 企业级多 Agent 部署 | WASM 工具 + Pluggable Agent Loops（kernel 模式） + 沙箱 | **"内核"路线**——不自研 agent loop，做调度/安全/审计底座；可接入 claude-code/pi/codex |
| **LobsterAI** | 桌面端+Web 混合的 OpenClaw 衍生 | 桌面效率用户 | Electron + React + SQLite + IPC | UI 统一化（skills/MCP/kits 三视图融合）；签到/积分等运营功能 |
| **CoPaw** | 桌面操作系统级 AI 助手 | 普通消费者 → 专业用户 | 桌面环境（QwenPaw OS Shell）+ 插件市场 + 云同步 | **桌面 OS 化**——不是"聊天窗口"而是"AI 操作系统"；中文社区活跃 |
| **ZeroClaw** | 安全优先的多协议 Agent 网关 | 企业/安全敏感用户 | Rust 实现 + Matrix 深度集成 + 多方协议 + 严格权限契约 | **Rust 安全红线** + RFC 决策流程制度化；Agent Plugins 1.0 标准支持 |
| **Moltis** | AI 网关+连接器生态 | 集成开发者 | CalDAV + 多渠道历史连接器 + 持久化层 | **连接器生态**方向；原子快照/全文搜索；provider-neutral 设计 |


## 6. 社区热度与成熟度

| 阶段 | 项目 | 特征 |
|------|------|------|
| **快速迭代期**（功能密度>稳定性） | **CoPaw** | 每 1-2 个月发布大版本；OS Shell 等重量级新特性快速落地；Bug 修复与功能并行 |
| | **NanoClaw** | 供应链安全 CI 密集重构（8 PR/天）；安全修复日级响应；但外部社区参与度低 |
| **质量巩固期**（稳定性>新功能） | **NanoBot** | 7 个 Bug 中 5 个在 24h 内获得修复 PR（71%）；Cron 修复三轮迭代；会话原子化推进 |
| | **ZeroClaw** | 安全修复集中合入；RFC 决策队列制度建立；v0.9.0 破坏性变更前加固 |
| | **IronClaw** | 性能优化系列（测量→削减→合并）；Epic 拆解执行；v1.2.0 稳定版发布 |
| **规模治理期**（高活跃+高积压） | **OpenClaw** | 处理量大但合并率低（21%）；安全 PR 积压 3 个月；静默失败反复 |
| | **Hermes Agent** | 656 个 PR 打包进补丁版本；TUI P1 23 天未修；质量追赶速度慢 |
| **平稳维护期** | **LobsterAI** | UI 重构集中推进；但 4 条 3 月 stale PR 积压；测试覆盖补全中 |
| | **Moltis** | 维护者响应积极（3 修复 PR 当日提交）；功能评审积压风险 |
| | **PicoClaw** | 依赖自动更新正常；核心功能请求响应慢；整体节奏偏缓 |
| **休眠/停滞** | **NullClaw / TinyClaw / ZeptoClaw** | 无任何活动，需关注维护者状态 |


## 7. 值得关注的趋势信号

### 信号一："内核化"架构路线崛起
IronClaw 的 Epic #7482（Pluggable Agent Loops）将 ACP 从核心目标降级为 "one driver implementation"，明确将"循环执行"外包给 claude-code/pi/codex，自研聚焦调度、安全、审计。**这标志着个人 AI 智能体正从"一站式全栈"走向"分层解耦"**——上层 Agent 界面与底层调度安全分离。对开发者的启示：评估智能体方案时，"通用内核 + 可插拔 harness"可能比"全栈统一"更具长期演进优势。

### 信号二：供应链安全从"建议"走向"强制门禁"
NanoClaw 将签名验证从"建议性检查"升级为"强制门禁"，并将发布者签名直接作为审批依据（#3241）。ZeroClaw 的 gateway 路径穿越修复和 Zhipu 凭据 fail-closed 同样收紧兼容层边界。**"不可伪造的签名作为审批依据"正在成为智能体供应链的标准安全模式**。对开发者的启示：部署 AI 助手时应关注镜像/插件签名机制，而不仅是功能清单。

### 信号三：记忆信任分级将成为标配
OpenClaw 的 #7707（记忆信任分级，48 评论、6 个月）与 Hermes Agent 的 #85418（零依赖 Agent 记忆层）、ZeroClaw 的 #6850（记忆生命周期解耦）不约而同指向同一方向：**记忆需要按来源分级（用户指令 > 网页抓取 > 第三方技能），防御记忆投毒攻击**。对开发者的启示：在 AI 智能体应用中设计记忆时，应内置来源标记（source-tagging）和信任级别（trust-level）字段，否则后续攻击面将难以修复。

### 信号四：自动化场景的"可停止性"（Stoppability）
CoPaw 因任务"无限循环"导致账户余额耗尽（#6652 修复），IronClaw 则讨论执行树迭代预算归属（#9323），OpenClaw 对 subagent 编排可靠性提出质疑（#43367）。**"如何安全地停止一个失控的 Agent"正在成为与"如何启动 Agent"同等重要的设计命题**。对开发者的启示：默认应为所有循环/递归调用设置硬上限（如 max_iterations 服务端强制），并在 UI 层提供一键停止。

### 信号五：跨项目 Bug 类型高度趋同
各项目独立报告的 Top Bug 高度一致——**静默失败、会话状态损坏、Windows 兼容性、MCP 工具 schema 预算（token 膨胀）、上下文缺失**。这说明这些问题非个别项目缺陷，而是**当前 AI 智能体技术栈的系统性短板**。对开发者的启示：在选择技术栈时，优先评估其在这些"已知短板"上的解决方案成熟度，而非只关注功能特性。

### 信号六：上游生态迁移的连锁影响
Moltis 因上游仓库从 steipete 迁移到 openclaw 导致两处依赖失效（sandbox build 全量失败 + wacrawl 技能安装失败），OpenClaw 生态的影响力正在通过"被依赖"间接传导到下游项目。**个人 AI 智能体的依赖网络正在形成中心化结构，OpenClaw 既是核心参照也是单点风险**。对开发者的启示：在构建基于 OpenClaw 生态的项目时，应主动 pin 住依赖版本，建立上游监控和快速迁移预案。


**总结判断：** 个人 AI 助手开源生态正经历从"社区驱动创新"到"工程化收敛"的关键过渡期。OpenClaw 作为生态锚点，其积压问题既是挑战也是机遇——若能有效释放审查带宽，将加速全生态成熟；NanoClaw、ZeroClaw、IronClaw 在安全与架构纪律上的投入则为生态提供了"工程标准"参照。对技术决策者的建议：**关注安全性投入力度（NanoClaw/ZeroClaw 为标杆）、评估多 Agent 编排可靠性（全生态最短板）、追踪"内核化"与"记忆分级"两大趋势**——这三点将决定未来 6-12 个月个人 AI 智能体的能力天花板。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-14

---

## 1. 今日速览

NanoBot 昨日（2026-08-13）活动异常活跃，共产生 12 条 Issue 更新和 31 条 PR 更新，创近期单日新高。核心贡献者 dajiaohuang 和 chengyongru 为主力，密集提交了针对会话管理（session）、MCP 模式、Cron 调度和 Matrix 集成的高质量修复。值得关注的是，Cron 调度器持久化失败致命bug、会话文件归档/合并截断、以及 `exec.allowPatterns` 安全绕过三个关键问题均有对应修复PR，项目健康度正在快速回升。暂无新版本发布，但多个已合入修复预计将在下一个版本中集中释放。社区讨论热度集中在 Telegram 贴纸、MCP Apps 展示和 WebUI 交互体验上，整体项目活跃度和维护响应速度均处于优秀水平。

---

## 3. 项目进展

### 已合入/关闭的修复（9 条 PR合并/关闭）

**核心稳定性修复：**

| PR | 说明 | 状态 |
|---|---|---|
| [#5374](https://github.com/HKUDS/nanobot/pull/5374) / [#5375](https://github.com/HKUDS/nanobot/pull/5375) | **Cron 调度器持久化失败致命崩溃修复**（两个提交，后者追加测试） | ✅ 已合入 |
| [#5384](https://github.com/HKUDS/nanobot/pull/5384) | **WebUI 恢复仅含 transcript 的会话历史** — 修复侧边栏无法发现无 JSONL 备份的历史会话的回归，且允许直接打开/删除 | ✅ 已合入 |
| [#5381](https://github.com/HKUDS/nanobot/pull/5381) | **WebUI 原生工作区文件夹选择器**（macOS/Windows/Linux），仅对 loopback 本地连接开放 | ✅ 已合入 |

> 注：#5374→#5375→#5376 经历了三轮迭代，反映维护者对 Cron 修复非常重视，最终版本（#5376）保留为 OPEN，等待合入确认。

**其他关闭的 PR：**
- [#4550](https://github.com/HKUDS/nanobot/pull/4550) — `fix(cron): per-run session key`（修复 cron 运行间上下文串扰，#4082）
- [#4556](https://github.com/HKUDS/nanobot/pull/4556) — `feat(dream): model_override 接入`（#4029）

### 推进会话管理安全基线

昨日提交的 [#5383](https://github.com/HKUDS/nanobot/pull/5383)（会话文件访问串行化）、[#5382](https://github.com/HKUDS/nanobot/pull/5382)（Windows `os.replace` 重试）、[#5380](https://github.com/HKUDS/nanobot/pull/5380)（文件容量归档失败状态回滚）、[#5379](https://github.com/HKUDS/nanobot/pull/5379)（会话合并避免有损截断）虽尚未合入，但这四者合在一起意味着 **会话读写将从"尽力而为"走向"原子、可回滚、跨平台稳定"**，这是底层数据完整性的重大跃升。

### 结论

项目在极端活跃的一天内，同时推进了 **Cron 健壮性、会话数据完整性、Windows 兼容性、WebUI 历史会话发现** 四条关键链路，整体成熟度明显上了一个台阶。

---

## 4. 社区热点

### 🏆 讨论热度 TOP 3

| 排名 | Issue / PR | 评论数 | 主题 |
|---|---|---|---|
| 1 | [#5358](https://github.com/HKUDS/nanobot/pull/5358) — `feat(webui): session collaboration via mentions` | 31条 PR 全部计入最活跃列表 | WebUI 通过 @通知 实现会话间协作 |
| 2 | [#5383](https://github.com/HKUDS/nanobot/pull/5383) — `fix(session): serialize canonical file access` | 最受关注的底层修复 | 会话文件锁与并发安全 |
| 3 | [#5373](https://github.com/HKUDS/nanobot/issues/5373) — Cron 调度器持久化失败致命崩溃 | 1 (Issue) | 一次磁盘错误杀死全部定时任务 |

### 分析

**#5358（会话协作）** 是最具产品想象力的提案：为每个持久会话分配稳定且服务端拥有的 `@name`，用户可在 composer 中 @ 另一个会话，让 Agent 跨会话引用上下文。这实质上将 WebUI 从"单会话聊天"推向"多会话协作画布"，是产品形态的重要探索。

**#5373（Cron 致命崩溃）** 虽只有一个 Issue 评论，但催生了 3 个 PR（#5374/#5375/#5376），是社区公认的高危 bug — 一句 "single persistence failure permanently kills the scheduler" 道出了定时任务用户的真实恐惧。维护者对 #5376 加了 `priority: p2` 与测试覆盖，显示了足够的诚意。

**#5383（会话锁）** 是昨日 PR 中涉及面最广的底层改动，统一了多实例 `SessionManager` 对同一 canonical 目录的并发读写，是长会话稳定性的地基工程。

---

## 5. Bug 与稳定性

按严重度排列：

### 🔴 高危（安全 / 数据丢失）

| Issue | 描述 | 状态 |
|---|---|---|
| [#5306](https://github.com/HKUDS/nanobot/issues/5306) | **`exec.allowPatterns` shell 链绕过** — 通过构造链式命令可绕过白名单执行任意命令（安全通告） | ✅ 已关闭（修复已合入） |
| [#5378](https://github.com/HKUDS/nanobot/issues/5378) | **文件容量归档失败后会话状态已变异** — 归档抛错后内存中的会话已丢弃溢出消息，后续保存无法恢复 | 🔧 已有修复PR [#5380](https://github.com/HKUDS/nanobot/pull/5380) |
| [#5377](https://github.com/HKUDS/nanobot/issues/5377) | **合并截断后游标却越过整批消息** — 被截断的消息后缀在下次合并时永远丢失 | 🔧 已有修复PR [#5379](https://github.com/HKUDS/nanobot/pull/5379) |

### 🟡 中危（功能不可用 / 崩溃）

| Issue | 描述 | 状态 |
|---|---|---|
| [#5373](https://github.com/HKUDS/nanobot/issues/5373) | **Cron 调度器在单次持久化失败后永久死亡** — `_arm_timer()` 在 try/finally 之外，异常逃逸后不再 tick | 🔧 已有修复PR [#5376](https://github.com/HKUDS/nanobot/pull/5376) |

### 🟢 低危（体验 / 一致性）

| Issue | 描述 | 状态 |
|---|---|---|
| [#5368](https://github.com/HKUDS/nanobot/issues/5368) | WebUI 在 Agent turn 进行中显示 copy/fork，与运行状态矛盾 | 暂无 PR |
| [#5366](https://github.com/HKUDS/nanobot/issues/5366) | Agent 活动文本硬编码英文，不随界面语言切换（i18n） | 暂无 PR |

### ⚠️ Windows 特有

| Issue | 描述 | 状态 |
|---|---|---|
| —（PR覆盖） | `os.replace()` 在 Windows 上遭遇瞬时 `[WinError 5]`，导致 gateway 崩溃（已在 #5382 中证实出现 2 次：2026-08-11 15:44 与 18:45 CDT） | 🔧 修复PR [#5382](https://github.com/HKUDS/nanobot/pull/5382) |

> **总评：** 昨日报告的 7 个 bug 中，5 个有直接修复 PR（#5380/#5379/#5376/#5382/#5385），修复率达到 71%，维护者响应速度优秀。**无未覆盖的高危 bug。**

---

## 6. 功能请求与路线图信号

| Issue | 功能 | 已有对应PR？ | 纳入下一版本可能性 |
|---|---|---|---|
| [#5251](https://github.com/HKUDS/nanobot/issues/5251) | MCP Apps 主机支持（`io.modelcontextprotocol/ui`），在 WebUI 中展示 MCP App UI | ✅ [#5386](https://github.com/HKUDS/nanobot/pull/5386) — `feat(mcp): preserve MCP Apps result metadata` | ⭐ 高（PR已提交，核心元数据已打通，UI 渲染是下一步） |
| [#5289](https://github.com/HKUDS/nanobot/issues/5289) | Telegram 贴纸发送 + 机器人主动消息反应该 | ✅ [#5387](https://github.com/HKUDS/nanobot/pull/5387) — `feat(telegram): support reusable sticker replies` | ⭐ 高（PR已提交） |
| [#5298](https://github.com/HKUDS/nanobot/issues/5298) | 大型 MCP 工具集场景下，为模型可见的 schema 设置预算 | ✅ [#5388](https://github.com/HKUDS/nanobot/pull/5388) — `feat(agent): budget model-visible MCP schemas`（默认关闭，opt-in） | ⭐ 高（PR已提交，默认关闭属保守路线） |
| [#5350](https://github.com/HKUDS/nanobot/issues/5350) | 新增 QwenCloud 提供商路径（与现有 DashScope 并行） | ❌ 无 | 中（纯新增，非 bug，优先级可能让位于修复） |
| [#4841](https://github.com/HKUDS/nanobot/issues/4841) | Matrix 设备跨签名信任 + SAS 验证 | ✅ [#5385](https://github.com/HKUDS/nanobot/pull/5385) — `fix(matrix): complete Element SAS request flow` | ⭐ 高（PR已提交） |
| [#5372](https://github.com/HKUDS/nanobot/issues/5372) | ViBo 记忆系统集成提议 | ❌ 无 | 低（第三方推广性提交） |

### 路线图信号

三条并行的功能线展示了 NanoBot 的产品方向：
1. **渠道丰富化** — Telegram 贴纸 + Matrix SAS 完成，补齐主流 IM 体验差异
2. **MCP 生态深入** — schema 预算（大工具集）+ Apps 元数据保留（富交互）
3. **WebUI 协作化** — 会话 ≈ 文档，支持互相 @ 引用（#5358）

---

## 7. 用户反馈摘要

### 痛点与诉求

**1. 多会话用户对上下文崩溃零容忍（#5373）**
> "The cron scheduler can die silently and permanently: a single persistence failure ... raises out of the timer task" — 用户处于"一次磁盘错误＝所有定时任务静默中断"的极端脆弱场景，且无任何告警。该问题直接在 8 小时内获得 3 轮修复 PR，虽未最终合入但响应速度令人满意。

**2. 大 MCP 工具集用户面临上下文预算压力（#5298）**
> 用户明确反馈 `ToolRegistry.get_definitions()` 随着 MCP 工具数量增长，模型输入 token 被大规模 schema 占据。提案要求"budget model-visible MCP schemas"——即牺牲少数工具可见性，换取主任务上下文空间，已收到 PR #5388 响应，方案为确定性子集选择，默认关闭以兼容存量。

**3. Matrix 重度用户遭遇信任中断（#4841）**
> 某管理员在启用 `e2eeEnabled` + `sasVerification` 后发现 bot 设备在 Element 所有客户端上显示为 untrusted，且无干净路径消除警告。该 issue 已开放 38 天，昨日终于收到修复 PR #5385 *(接受 Element 请求 + 完成 SAS 流程)*，是社区最期待的合入之一。

**4. Windows 用户高频崩溃（PR #5382）**
> 贡献者 albatrossflyon-coder 在同一 gateway.log 中发现两次 `[WinError 5]` 崩溃（均在 heartbeat cron 的 session 保存时），说明 Windows 上的会话保存并非一次性偶发事件。虽然代码中已有 fsync 逻辑，但 `os.replace` 在 Windows 上的瞬时拒绝未做重试，修复PR已提交。

### 满意点

- dajiaohuang 同时提交 5 个 PR（#5385/#5386/#5387/#5388/#5379/#5380）覆盖矩阵、MCP、Telegram、会话完整性四个方向，且均附带测试，社区对维护者的专注度和代码质量持续给出好评（通过持续活跃的 issue-close 节奏可见）。

---

## 8. 待处理积压

### ⚠️ 长期未响应（>30 天）且影响用户的关键项

| 条目 | 创建时间 | 已开放天数 | 状态 |
|---|---|---|---|
| [#4841](https://github.com/HKUDS/nanobot/issues/4841) — Matrix SAS 验证缺失 | 2026-07-07 | 38 天 | ✅ **昨日已获 PR #5385，等待 review/merge** |
| [#4549](https://github.com/HKUDS/nanobot/pull/4549) — heartbeat 独立模型配置 | 2026-06-26 | 49 天 | 🟡 OPEN，git 历史已有冲突标记（conflict flag），需 rebase 后合入 |
| [#4551](https://github.com/HKUDS/nanobot/pull/4551) — heartbeat 共享会话配置 | 2026-06-26 | 49 天 | 🟡 OPEN，同上，待 rebase |

### 📌 建议维护者关注

1. **#4549/#4551 两个 heartbeat PR 已停留 49 天**，且都带 `conflict` 标签，说明 core 代码已发生较大变化。如果仍然期望 heartbeat 可配置化为商业化部署（如降低成本）的一部分，建议尽快安排 rebase 或关闭并标记为"由其他方案替代"。
2. **#5358（会话协作）虽是大热功能**，但 PR 描述中隐含"token-free deletion"、"fail-closed"等复杂语义，建议维护者在合入前充分讨论并发、权限边界与身份命名规则，避免为后续会话安全留下隐患。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-14

*数据来源：NousResearch/hermes-agent GitHub 仓库*

---

## 1. 今日速览

过去24小时内，Hermes Agent 项目保持**高热度的社区活跃度**：共产生50条 Issue 更新（45条活跃/新开，5条关闭）和50条 PR 更新（46条待合并，4条已合并/关闭）。项目发布了 **v0.20.1 补丁版本**，打包了自 v0.20.0 以来约 656 个 PR 的滚动更新。值得关注的是，项目同时存在 P0/P1 级 bug 未解决（如 TUI 覆盖层不可见、会话状态损坏等），但修复 PR 的提交速度较快，表明维护团队响应积极。**整体判断：项目活性极高，但长期存在的质量问题（特别是 TUI 与桌面端）仍需关注。**

---

## 2. 版本发布

### v0.20.1 (v2026.8.13) — 补丁版本

- **发布日期：** 2026年8月13日
- **性质：** Patch release，将自 v0.20.0 以来合并的 ~656 个 PR 打包为稳定标签，供下游消费者（Docker 镜像、托管部署、按标签安装的用户）使用。
- **破坏性变更：** 未明确列出，作为补丁版本建议用户正常升级。
- **迁移注意事项：** 无特殊说明。建议用户升级后关注桌面端与 TUI 相关 issue（见下文），因为部分已知问题（如 #69592、#52339）在 v0.20.x 中仍存在。

---

## 3. 项目进展

今日合并/关闭的 PR 数量较少（4条），但结合 v0.20.1 发布，项目整体向前迈进了显著一步——**656 个 PR 的滚动合并是项目长期积累的成果，覆盖了从功能性修复到安全硬化的广泛改进**。

值得注意的近期合并/状态更新的 PR 包括：

| PR | 说明 | 状态 |
|---|---|---|
| [#85707](https://github.com/NousResearch/hermes-agent/pull/85707) | `fix(cache): establish typed tool-schema boundary before planned_tools[-1]` —— 修复原生工具缓存路径中未规范化工具模式即添加 `cache_control` 标记的问题 | ✅ 已关闭 |
| [#85710](https://github.com/NousResearch/hermes-agent/pull/85710) | `fix(cron): reuse secret cache and clarify home delivery` —— 优化 cron 任务的外部密钥源刷新逻辑，复用进程缓存，避免每次触发时强制刷新所有后端 | ✅ 已关闭 |
| [#85705](https://github.com/NousResearch/hermes-agent/pull/85705) | 无效 PR（错误仓库） | ✅ 已关闭 |

当前有 46 条 PR 处于待合并状态，涵盖安全修复、网关改进、插件系统增强等多个方向，说明项目仍处于密集开发期。

---

## 4. 社区热点

### 最受关注 Issue 排行

| Issue | 评论数 | 核心讨论点 |
|---|---|---|
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) — Skills index is stale or degraded | 25 | 自动化探针发现 Skills Hub 索引文件 29.8 小时未更新（限制 26 小时），状态降级。持续近一个月未修复，社区关注度较高 |
| [#84834](https://github.com/NousResearch/hermes-agent/issues/84834) — Webhook Revolution — graph-gated repair campaign (EPIC) | 16 | 大规模 Webhook 表面修复战役（5×2×3 矩阵），覆盖入口、执行、投递、配置、管理 UI、部署与文档，属于系统性改进计划 |
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) — /sessions 和 /models 覆盖层不可见 | 12 | **P1 级** TUI 问题，影响核心工作流（切换会话/模型），持续 3 周+ 未解决 |
| [#83390](https://github.com/NousResearch/hermes-agent/issues/83390) — DeepSeek 辅助标题生成 HTTP 400 | 9 | 特定 provider 兼容性问题，社区有用户 +1 |
| [#4438](https://github.com/NousResearch/hermes-agent/issues/4438) — 富电子表格技能（xlsx/csv）功能请求 | 8 | 长期开放的功能请求（自4月），社区有持续讨论 |

### 分析

社区讨论热度集中在两类诉求：**（1）基础设施稳定性**（索引过期、TUI 核心功能不可用）；（2）**平台适配与扩展**（DeepSeek 兼容、Webhook 全面修复、Signal/Telegram 适配增强）。值得一提的是，EPIC issue #84834 表明项目正在规划一次 Webhook 子系统的大规模重构，覆盖面极广，值得关注后续进展。

---

## 5. Bug 与稳定性

### P0 级

暂无新增 P0 级 Bug 报告。

### P1 级

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | TUI 中 `/sessions`、`/models` 覆盖层在加载 ambient widgets 后不可见，会话恢复和模型切换功能不可用。**持续 3 周+** | 开放，无 fix PR |
| [#62142](https://github.com/NousResearch/hermes-agent/issues/62142) | verification-stop 可能丢弃流式最终答案和 cron 报告，导致用户看到的回复不完整 | 开放，无 fix PR |

### P2 级（新增/活跃）

| Issue | 描述 | 是否有 fix PR |
|---|---|---|
| [#85215](https://github.com/NousResearch/hermes-agent/issues/85215) | Cron 任务锁定已失效模型且忽略 fallback_providers，连续数日报 402 错误 | 无 |
| [#83427](https://github.com/NousResearch/hermes-agent/issues/83427) | `browser_exec` 崩溃：PYTHONPATH 指向 Hermes venv 时 pydantic_core ModuleNotFoundError（桌面端） | 无 |
| [#85614](https://github.com/NousResearch/hermes-agent/issues/85614) | Slack 机器人对等 ID 早期投递校验与最终授权不匹配 | 无 |
| [#83851](https://github.com/NousResearch/hermes-agent/issues/83851) | 中文 Windows 系统 GBK 编码导致网关崩溃 | 无 |
| [#85658](https://github.com/NousResearch/hermes-agent/issues/85658) | 中断的命令采用另一会话的工作目录 | 无 |
| [#52339](https://github.com/NousResearch/hermes-agent/issues/52339) | 终端更新重建桌面应用但 `/Applications/Hermes.app` 残留旧版本（split-brain 状态） | 无 |

### 已关闭

- [#35838](https://github.com/NousResearch/hermes-agent/issues/35838) — `models.dev` 不可达时 `get_provider_info()` 阻塞（标记为重复）
- [#81639](https://github.com/NousResearch/hermes-agent/issues/81639) — `_canonicalize_api_tool_calls` 修改已持久化历史，导致会话永久卡在仅推理响应（标记为重复）

**关注点：** 多个 P2 级 Bug 集中在 Windows 平台与 **桌面端**，这与此前发布的 v0.20.1 未提及桌面端已知问题有关。建议维护团队优先排查桌面端相关回归。

---

## 6. 功能请求与路线图信号

### 新增功能请求（过去24小时）

| Issue/PR | 描述 | 潜在纳入版本判断 |
|---|---|---|
| [#85418](https://github.com/NousResearch/hermes-agent/issues/85418) | 本地优先、零依赖的 Agent 记忆层提案，对标 Honcho，基于 Hermes 构建 | 属重大架构型功能，需 `needs-decision` 决策，短期纳入可能性低 |
| [#85723](https://github.com/NousResearch/hermes-agent/pull/85723) | 文档站添加日文语言支持（`ja-JP`） | 已提交 PR，纳入可能性较高 |
| [#85725](https://github.com/NousResearch/hermes-agent/pull/85725) | 插件技能命令自动补全（TUI/CLI） | 已提交 PR，与现有插件体系兼容，纳入可能性高 |

### 路线图信号

- **EPIC #84834（Webhook Revolution）** 标志着网关层将有一轮系统性重构，涉及配置、管理 UI、部署与文档，涉及面广，但规划明确。
- **记忆层探索**（#85418）表明社区对更强大的记忆能力有需求，但尚处于提案阶段。
- 多个 `needs-decision` 标签的 PR/Issue（如 #39043 Signal 适配增强、#84317 Telegram 冷启动选项、#85710 cron 密钥缓存）等待维护者决策，属于路线图待定项。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提取的真实反馈：

- **积极反馈：** 用户在 #85418 中对社区成员 DavidMetcalfe 表示感谢，提到 `--autoConnect` 修复了 Chrome DevTools 空白配置文件问题，并"彻底解决"。
- **核心痛点：**
  - **TUI 基本功能不可用**（#69592）——用户界面在默认配置下失效，严重影响使用体验。
  - **桌面端与 CLI 行为不一致**（#52339，#85693）——用户期望桌面应用与 CLI 行为一致，但实际存在 split-brain 状态和功能缺失（如 `computer_use` 工具）。
  - **平台适配问题**——Windows 中文环境（GBK 编码）、DeepSeek 响应格式不兼容等，影响特定用户群体。
  - **数据丢失风险**（#62142）——流式回答被丢弃，用户看到不完整的回复，影响信任感。
- **满意点：** 未发现明确的满意反馈。但从 Issue 评论数下降来看，部分问题可能已通过其他渠道解决。

---

## 8. 待处理积压

### 长期未解决的重要 Issue

| Issue | 创建时间 | 持续天数 | 状态 | 备注 |
|---|---|---|---|---|
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 2026-07-18 | 27天 | 开放，degraded | Skills 索引过期，自动化探针持续告警 |
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | 2026-07-22 | 23天 | 开放，P1 | TUI 核心功能不可用，无 fix PR |
| [#4438](https://github.com/NousResearch/hermes-agent/issues/4438) | 2026-04-01 | 135天 | 开放 | 富电子表格技能功能请求，长时间未纳入路线图 |
| [#33049](https://github.com/NousResearch/hermes-agent/issues/33049) | 2026-05-27 | 79天 | 开放 | 凭据池 TTL 硬编码，需配置化 |
| [#39043](https://github.com/NousResearch/hermes-agent/issues/39043) | 2026-06-04 | 71天 | 开放，needs-decision | Signal 适配器完整功能支持 |

### 长期未响应的 PR

| PR | 创建时间 | 持续天数 | 状态 |
|---|---|---|---|
| [#35601](https://github.com/NousResearch/hermes-agent/pull/35601) | 2026-05-31 | 75天 | 开放，security，待 review |
| [#52289](https://github.com/NousResearch/hermes-agent/pull/52289) | 2026-06-25 | 50天 | 开放，P2，待 review |
| [#64866](https://github.com/NousResearch/hermes-agent/pull/64866) | 2026-07-15 | 30天 | 开放，P2，待 review |

### 维护者提醒

1. **P1 级 Issue #69592 已持续 23 天**，影响了 TUI 核心工作流，建议优先分配资源处理。
2. **Skills 索引告警（#66616）** 已持续 27 天，虽为 P3，但自动化探针持续告警消耗维护者注意力。
3. 多个安全相关 PR（#35601、#83787、#82758）已等待较长时间，鉴于其 security 属性，建议尽快安排 review。

---

> **报告日期：** 2026-08-14 | **生成方式：** 基于 GitHub 数据自动分析，人工审校
> **声明：** 本报告所有链接均指向公开 GitHub 数据，供项目参与者和社区参考。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-14** | **数据来源：github.com/sipeed/picoclaw**


## 1. 今日速览

PicoClaw 项目在过去 24 小时内呈现中高活跃度：共产生 3 条新 Issue 和 9 条 PR 更新，无新版本发布。值得关注的是，今日有 3 个旧的依赖更新 PR（#3304、#3305、#3306）被关闭，同时 6 个新的 PR 被提交并处于待审查状态，其中 5 个为 Dependabot 自动依赖更新，1 个为 Web 前端锁文件修复。社区热点方面，一个关于 Web UI 输入延迟的 Bug 报告（#3281）获得了 5 条评论，是最受关注的问题。两个新功能请求分别涉及 Whisper 语音转写模型扩展和子代理工具模型动态覆盖。总体来看，项目依赖维护自动化运行正常，但核心功能开发节奏相对平稳，需注意 Web 前端性能和子代理灵活性方面的问题。


## 2. 版本发布

过去 24 小时内无新版本发布，项目当前无最新 Releases。上一个已知版本为 0.3.1（根据 Issue #3281 中用户报告的环境信息）。建议关注后续依赖更新合并后的版本号变化。


## 3. 项目进展

今日共有 3 个 PR 被关闭（均为已过期/被替换的依赖更新 PR），无代码合并。主要变化如下：

| PR | 状态 | 内容 | 说明 |
|---|---|---|---|
| [#3304](https://github.com/sipeed/picoclaw/pull/3304) | 关闭 | bump anthropic-sdk-go 1.55.1→1.61.0 | 被更新的 #3334 取代 |
| [#3305](https://github.com/sipeed/picoclaw/pull/3305) | 关闭 | bump bedrockruntime 1.53.3→1.56.2 | 被更新的 #3336 取代 |
| [#3306](https://github.com/sipeed/picoclaw/pull/3306) | 关闭 | bump aws-sdk-go-v2/config 1.32.25→1.32.33 | 被更新的 #3335 取代 |

**重要发现**：这三个旧 PR 均在 2026-07-30 创建，但在 8 月 13 日被关闭，同一天 Dependabot 提交了更高版本的对应更新（#3334、#3335、#3336）。这说明：

1. **依赖维护策略**：项目方采用了"关闭旧 PR、接受新 PR"的方式，保持依赖版本始终为最新。
2. **代码进展**：今日无实际代码合并，但前一天的 [#3318](https://github.com/sipeed/picoclaw/pull/3318)（修复 pnpm-lock.yaml 损坏问题）仍处于打开状态，需要维护者重点关注——锁文件损坏会直接影响 Web 前端的构建流程。


## 4. 社区热点

### 最热 Issue：#3281 Web UI 输入延迟问题

- **链接**：[Issue #3281](https://github.com/sipeed/picoclaw/issues/3281)
- **标签**：`[BUG]`
- **状态**：OPEN | 评论 5 条 | 👍 1
- **提出时间**：2026-07-21（已持续 23 天）

**摘要**：用户报告当会话历史较长时，Web UI 的聊天输入框出现明显卡顿。该问题在 v0.3.1 版本上复现，影响 chat 输入框的日常使用体验。

**社区诉求分析**：该 Issue 是本月最活跃的 Bug 报告，已经积累了 5 条评论。虽然获得 👍 数量不高（1），但持续 23 天未关闭表明这是一个真实且可复现的问题。从使用场景来看，PicoClaw Web UI 的用户会进行多轮对话，积累较长历史后输入卡顿会严重降低协作效率。目前尚未看到相关的修复 PR，此问题可能需要 Web 前端团队优先处理。


## 5. Bug 与稳定性

### 严重程度：中

| Issue/PR | 问题描述 | 严重程度 | 修复状态 |
|---|---|---|---|
| [#3281](https://github.com/sipeed/picoclaw/issues/3281) | Web UI 聊天输入框长历史卡顿 | 中 — 日常功能受损，但不影响后端核心逻辑 | **未修复**，暂无关联 PR |
| [#3318](https://github.com/sipeed/picoclaw/pull/3318) | `web/frontend/pnpm-lock.yaml` 存在重复键，导致前端构建失败（`ERR_PNPM_BROKEN_LOCKFILE`） | 高 — 阻塞前端构建流程 | **已有修复 PR**，待合并 |

**Web 前端构建阻塞问题详解**：PR [#3318](https://github.com/sipeed/picoclaw/pull/3318) 指出 `pnpm-lock.yaml` 中 `semver@7.8.5` 在 `packages:` 和 `snapshots:` 两处重复出现，使 pnpm 拒绝加载该文件。该问题会导致前端构建流水线直接失败。修复 PR 由外部贡献者 nuestraai 提交，已经解决了问题，但需要维护者尽快审查合并。


## 6. 功能请求与路线图信号

今日收到 2 个新的功能请求，都值得关注：

### 请求一：[#3331](https://github.com/sipeed/picoclaw/issues/3331) — 扩展 Whisper 语音转写模型支持

- **提交者**：stanislavvv（2026-08-13）
- **核心诉求**：当前 ASR 功能仅支持名称含 `"*-whisper-*"` 的模型，但 Whisper 模型"太旧且慢"，用户希望支持任何提供 `/audio/transcriptions` 端点的模型。
- **建议方案**：在模型配置或语音配置中添加 `whisper-transcription: true` 标志，强制 asr.go 走 Whisper 路径。
- **路线图信号**：**中高**。语音交互是 AI 助手的重要使用场景，支持更广泛、更新的 ASR 模型能显著提升用户体验。实现成本不高（加一个配置项 + 修改路由逻辑），且有明确的用户需求支撑。

### 请求二：[#3330](https://github.com/sipeed/picoclaw/issues/3330) — delegate/spawn/subagent 工具支持动态模型覆盖

- **提交者**：v2up-32mb（2026-08-13）
- **核心诉求**：当前 `delegate`、`spawn`、`subagent` 工具在调用时无法指定模型，模型由配置静态决定——`delegate` 用目标 agent 的配置模型，`spawn` 用主 agent 的 `defaultModel`。
- **影响范围**：限制了多模型编排的灵活性，用户无法在 Agent 交互过程中动态切换不同模型来处理不同子任务。
- **路线图信号**：**中**。从 Agent 编排的角度，这是一个合理且必要的增强。在 AI Agent 需要根据任务复杂度动态选模型的场景中，该功能能大幅提升系统灵活性。但需要评估 API 设计变更的影响面，预计工作量中等。


## 7. 用户反馈摘要

### 来自 Issue #3281 的评论洞察

- **使用场景**：用户使用 PicoClaw Web UI 进行多轮对话式开发协作，长历史会话是常态，而非边缘场景。
- **核心痛点**：会话历史累积后输入框卡顿，影响日常操作流。交互响应延迟直接削弱了"AI 辅助"本应带来的效率提升。
- **满意度**：总体偏不满意。该问题持续 23 天未修复，用户可能需要临时绕道使用本地客户端或缩短会话长度来规避。
- **待改进方向**：Web 前端需要针对长列表/长历史场景做性能优化，包括但不限于虚拟滚动、输入框防抖、历史消息懒加载等。

### 来自 PR #3318 的反馈

- 外部贡献者 nuestraai 主动发现并修复了锁文件损坏问题，说明社区有活跃的贡献者愿意投入修复基建问题，这是项目健康度的一个积极信号。


## 8. 待处理积压

以下 Issue/PR 需要维护者关注处理：

| 项目 | 链接 | 等待天数 | 说明 |
|---|---|---|---|
| [PR #3318](https://github.com/sipeed/picoclaw/pull/3318) | pnpm-lock 修复 | 9 天 | **加急**：阻塞前端构建，已有修复方案，等待合并 |
| [Issue #3281](https://github.com/sipeed/picoclaw/issues/3281) | Web UI 输入延迟 | 24 天 | 已持续超 3 周，评论 5 条，建议给出修复时间表 |
| [PR #3332](https://github.com/sipeed/picoclaw/pull/3332) | bump aws-sdk-go-v2 1.42.0→1.43.4 | 1 天 | Dependabot 依赖更新，建议尽快审查 |
| [PR #3333](https://github.com/sipeed/picoclaw/pull/3333) | bump mautrix 0.27.0→0.29.0 | 1 天 | 跨 minor 版本更新，需关注破坏性变更 |
| [PR #3334](https://github.com/sipeed/picoclaw/pull/3334) | bump anthropic-sdk-go 1.55.1→1.62.0 | 1 天 | minor 版本跨 6 个版本，建议审查 release notes |
| [PR #3336](https://github.com/sipeed/picoclaw/pull/3336) | bump bedrockruntime 1.53.3→1.57.1 | 1 天 | 跨 4 个版本，需关注兼容性 |


## 项目健康度总结

| 维度 | 评分 | 说明 |
|---|---|---|
| 社区活跃度 | ⭐⭐⭐☆ | 8 月 13 日有多个新 Issue/PR 提交，但核心贡献者参与度一般 |
| 依赖维护 | ⭐⭐⭐⭐ | Dependabot 正常运转，自动更新+替换旧 PR 的策略执行良好 |
| Bug 响应效率 | ⭐⭐☆☆ | #3281 已 24 天未修复，#3318 已 9 天待合并 |
| 功能迭代速度 | ⭐⭐⭐☆ | 今日无新代码合并，整体节奏平稳 |
| 项目可持续性 | ⭐⭐⭐⭐ | 有外部贡献者参与（#3318、#3330），社区生态健康 |

**维护者行动建议**：(1) 立即审查合并 #3318，恢复前端构建能力；(2) 为 #3281 的修复制定时间表或在 Issue 中给出回应，安抚用户；(3) 评估 6 个待处理依赖 PR，优先处理跨 minor 版本更新的 #3333 和 #3334。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-14

## 1. 今日速览

今日 NanoClaw 仓库活跃度极高，24 小时内 PR 更新达 19 条，标志着 **v2.2.0 发布后进入密集加固与集成验证阶段**。核心团队（`[core-team]` 标记）围绕 **agent 镜像签名验证流水线** 展开了大规模 CI 重构（涉及 #3236-#3243 共 8 条 PR），将签名验证从"建议性检查"升级为"强制门禁"，并尝试将发布者签名直接作为审批依据。功能侧，**Agent Plugins 1.0.0 目录格式迁移主线已合入**（#3220、#2909），标志着模板功能完成架构升级；同时修复了 Telegram 配对码 CSPRNG 安全漏洞（#3229）。Issue 侧仅 2 条更新，其中 1 条已关闭，整体问题追踪健康。项目正处于 **"发布后加固 + 供应链安全强化"** 的关键阶段，工程纪律和自动化程度显著提升。

---

## 2. 版本发布

### v2.2.0

**核心变更**：模板化（template-stamped）Agent 组现在支持**原地更新插件**。当某个组已携带模板的插件时，再次执行 `ncl groups create --template <ref>` 将触发原地更新而非创建重复 Agent。**干跑（dry run）模式**会打印所有插件所属的变更面（插件文件、技能、MCP 服务器配置等）的更新计划。

**破坏性变更**：版本号升至 2.2.0，属于 minor 版本，不引入已知破坏性变更。但需注意：模板功能的底层目录结构已迁移至 **Agent Plugins 1.0.0 格式**（见 PR #3220），任何手动维护模板目录的部署需按新规范调整。

**迁移注意事项**：
- 若使用旧版模板格式，建议先备份插件目录再执行 `ncl groups create --template` 触发迁移式更新。
- Agent 镜像已重固定至 `hardened-2026-08-13`（PR #3236），镜像体积从 620,725,759 → 620,769,684 字节（+44KB），携带了 NanoClaw 自身内容变更（非仅基础镜像刷新），生产环境建议滚动更新。

---

## 3. 项目进展

今日共合并/关闭 13 条 PR，按影响面分类如下：

### 🏗️ 核心功能（已合入主线）
- **Agent 模板 → Agent Plugins 1.0.0 格式迁移（#3220，已合）**：引擎级格式迁移，包含 stamp-time symlink/caps/secret 安全加固。这是模板功能的架构性重构，后续所有模板相关功能均基于此。
- **Setup 向导模板流程与首 Agent 打标（#2909，已合）**：在 `#3220` 之上叠加了 14 个 setup 侧文件（+927/-52），使新用户可通过向导直接使用模板。
- **插件 MCP 工作目录支持（#3231，已合）**：Codex 与 opencode 两个 provider 的配置写入器均已支持插件 MCP 的 `cwd` 字段，配合 registry 端改动完整落地该能力。
- **每个 MCP 服务器的 per-server disabledTools（#2624，已合）**：在 `McpServerConfig` 中添加每服务器级工具禁用配置，精细化 MCP 权限控制。

### ⚠️ 安全修复
- **Telegram 配对码 CSPRNG 替代 Math.random()（#3229，已合）**：配对码空间从 4 位数字扩大至 5 位，使用 `crypto.randomInt`。安全等级显著提升。

### 🔧 数据与配置修复
- **DB 迁移 021：为既有 wirings 回填 channel destinations（#3145，已合）**：无痛迁移，保留自定义本地名称。
- **发布流水线：v2.2.0 版本更新（#3237，已合）**。

### 🤖 CI/供应链安全（核心团队）
- **`verify-agent-image` 工作流运行在每次 PR 上（#3238，已合）**：移除 `paths:` 过滤，使验证成为必需状态检查的前提。
- **通过 `repository_dispatch` 打开 agent 镜像升级 PR（#3240，已合）**：实现"AWS 侧验证/提升镜像 → GitHub 侧开 PR"的凭据隔离闭环。
- **固定发布者身份及分架构 attestation 验证（#3158，已合）**：此前签名验证因变量不存在而总是被跳过，现已接入真实发布者身份。
- **Agent 镜像重新固定至 hardened-2026-08-13（#3236，已合）**。
- **签名验证结果门禁实验（#3241，已合）**：将发布者签名作为 pin bump 的审批依据，默认关闭（需 `AGENT_IMAGE_AUTO_APPROVE=true` 才实际生效），当前为"只报告不审批"的观察模式。

### 📋 总结
项目在 24 小时内完成了 **供应链安全管线从"形同虚设"到"强制门禁"的跃迁**，同时 Agent 模板的架构升级主线全部收口。核心团队在 CI 工程化上的投入密度非常高，项目整体前进约 1.5 个 sprint 的工作量。

---

## 4. 社区热点

**今日讨论最集中的主题是供应链安全 CI 改造**，核心团队 8 条 PR 形成了一条完整的技术链。其中：

- **PR #3241**（签名作为审批依据） 是今日最具争议性的设计：将"最后人工步骤"的门禁从"无法独立验证的点击"改为"不可伪造的签名"。它默认关闭并以报告模式运行，暗示团队希望先收集数据再全量铺开。
- **PR #3243**（Open，auto-merge 失败不应判定为验证失败） 与 **#3242 / #3239**（两条明确标注 DO NOT MERGE 的活体测试 PR） 展示了团队的工程方法：**用"一次性草稿 PR"在真实环境中验证新门禁的完整路径**，而非依赖本地模拟。

社区（非核心团队）侧，**Issue #3235**（webhook/bot 发送者触发无界审批卡）是今天唯一新增的 bug 报告，0 评论但问题描述清晰，属于自动化场景下的真实痛点（详见第 5 节）。

**从评论互动量看**：#3234 有 1 条评论，其余 Issue/PR 基本没有外部讨论。今日活跃度集中在内部工程线上，社区外部参与度相对平淡。

---

## 5. Bug 与稳定性

### 严重程度：高（安全）
- **Telegram 配对码使用 Math.random()（#3229，已合）**：可预测的配对码可被暴力枚举，导致未授权配对。**已在今日修复**，改用 CSPRNG 并将熵从 10^4 提升至 10^10 量级。

### 严重程度：中（功能缺陷）
- **模板化 Agent 组 ID 缺少 `ag-` 前缀（#3234，已关闭）**：`ncl groups create --template` 生成的组 ID 是裸露的 UUID，而 `--folder` 路径生成 `ag-<uuid>`。这导致 OneCLI 的 `ensureAgent` 会拒绝以数字开头的裸 UUID，使 spawn 失败。**已关闭**，修复大概率已随 v2.2.0 发布或即将合入。
- **webhook/bot 发送者触发无界审批卡（#3235，Open）**：当群组的 `unknown_sender_policy = 'request_approval'` 时，自动化发送者（平台 webhook、其它 bot）的每条消息都产生一张审批卡。对周期性 webhook 而言，审批队列无限增长，手动批准无意义，拒绝也不持久（下一条消息又会产生新卡）。**暂无 fix PR**，需要产品决策：应识别 bot 身份并跳过审批，或为同一发送者合并审批请求。

### 严重程度：低（CI 工程）
- **`verify-agent-image` 的 auto-merge 步骤误判作业结论（#3243，Open）**：auto-merge 失败（草稿 PR、`allow_auto_merge=off`、瞬时 API 错误）被判为验证失败，与镜像质量无关。已有 PR 修复中。

---

## 6. 功能请求与路线图信号

### 可能进入下一版本（已有实现/PR 支撑）
- **Agent 镜像签名作为审批依据（#3241）**：目前是观察模式，若数据表现良好，可能在 v2.3.0 中默认开启。这是供应链安全的重要信号。
- **插件 MCP 工作目录支持（#3231）**：已合入。后续可能的扩展是 runtime 侧落地更多 provider。
- **per-server disabledTools（#2624）**：已合入。为复杂 MCP 拓扑提供了精细控制手段，预计会被安全审计类用户广泛采用。

### 未来可能方向
- **Issue #3235 所暗示的 "bot/自动化发送者身份识别"**：如果审批策略要区分人类与自动化发送者，需要引入 sender 身份分类框架——这可能在 v2.3.0 的 messaging 模块中作为一个新特性出现。

---

## 7. 用户反馈摘要

今日 Issue 评论互动极少（仅 #3234 有 1 条评论），以下是基于新增 Issue 与 PR 描述的提炼：

- **模板用户在升级后遇到了 UUID 前缀问题（#3234）**：用户使用 `--template` 创建工作流时，生成的组无法被下游 agent spawn 流程接受。这是一个"新功能引入 → 实际使用中被坑"的典型反馈，说明**模板功能的测试覆盖在 OneCLI 集成层面存在缺口**。
- **自动化场景下的审批疲劳（#3235）**：用户（pentar69）在集成平台 webhook 时发现审批机制不区分消息来源的"人性"。这暴露了审批策略设计的**语义缺口：`request_approval` 针对的是"未知人类"，而非"未知发送者"**。诉求是让系统理解"程序性消息"与"人类消息"的本质差异。
- **CI 工程侧的"狗粮"测试（#3239/#3242）**：核心团队通过 DO NOT MERGE 的真实链路测试来验证门禁，体现了对工程质量的严谨态度——这在社区视角是加分项。

---

## 8. 待处理积压

### ⚠️ 近期需关注

| 编号 | 类型 | 标题 | 创建 | 最后活跃 | 风险 |
|------|------|------|------|----------|------|
| [#3235](https://github.com/nanocoai/nanoclaw/issues/3235) | Issue | 未知发送者审批无界生成 | 2026-08-13 | 2026-08-13 | 中 — 自动化集成用户持续受影响 |
| [#3243](https://github.com/nanocoai/nanoclaw/pull/3243) | PR | verify-agent-image: auto-merge 判定错误 | 2026-08-13 | 2026-08-13 | 低 — CI 误报，但有 PR 在修 |

### ⏳ 长期未响应（超过 90 天）

| 编号 | 类型 | 标题 | 创建 | 最后活跃 | 说明 |
|------|------|------|------|----------|------|
| [#2420](https://github.com/nanocoai/nanoclaw/pull/2420) | PR | /add-hindsight — Hindsight 记忆 MCP 包装器 | 2026-05-11 | 2026-08-13 | 93 天未合；功能完整（含 bundled MCP wrapper），疑似等待核心团队 review 排期 |
| [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) | PR | 未知斜杠命令回退为正常聊天 | 2026-05-08 | 2026-08-13 | 98 天未合；**修复了一个静默吞消息的 bug**，风险中等，社区侧有明确收益 |
| [#3218](https://github.com/nanocoai/nanoclaw/pull/3218) | PR | CLI 支持有界 JSON stdin | 2026-08-09 | 2026-08-13 | 功能完整，为 CLI 自动化提供关键能力，已 5 天未获 review |

### 📌 维护者提醒
- **#2420 与 #2346 的延迟已超过 3 个月**——这两条 PR 都属于"社区贡献、功能完整、无争议改动"，建议核心团队安排一次补审，避免社区贡献者流失。
- **#3218** 是近期社区提交中技术含金量较高的一条（有界输入处理），值得优先 review。

---

**报告生成时间**：2026-08-14 | 数据源：[NanoClaw GitHub](https://github.com/nanocoai/nanoclaw)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-14

> **数据窗口:** 2026-08-13 至 2026-08-14（基于 50 Issues / 50 PR 更新样本）


## 1. 今日速览

IronClaw 在过去 24 小时呈现**高活跃度**，核心焦点清晰集中在 **Epic #7482 "Pluggable agent loops"** 的落地拆解上——该 Epic 在今日被系统性地拆分为约 17 个可独立交付的实施子任务（#7606–#7624），标志着项目从架构讨论正式转入执行阶段。同时，**v1.2.0 正式发布**（RC3 稳定晋级），并伴随一批性能优化 PR（事件合并、心跳日志削减、触发器和出站写入精简），表明项目在稳定性和规模能力上同时发力。值得关注的是，今日涌现多个用户反馈的真实 Bug（MCP 认证卡死、GitHub 扩展假连接、Sonnet-5 500 错误），社区反馈渠道畅通，但部分高优先级问题（PDF MIME 类型错误）仍未关闭。


## 2. 版本发布

### 🚀 IronClaw v1.2.0（2026-08-13 发布，PR #7625 合并）

| 项目 | 详情 |
|---|---|
| **版本** | `1.2.0`（由 `1.2.0-rc.3` 稳定晋级） |
| **发布 PR** | [chore(release): promote 1.2.0-rc.3 to 1.2.0](https://github.com/nearai/ironclaw/pull/7625) |
| **变更范围** | 合并 RC1–RC3 的全部 changelog 条目，更新 manifest 与 lockfile |

**核心变更内容：**
- **RC3 修复：** 运行时容器镜像预装 `curl`，使容器内 HTTP 健康检查可正常执行（此前编排器探测 worker 时因缺少 curl 而失败）
- **RC1–RC2 功能集：** 完整包含（Release Notes 中注明为 "complete RC1 feature set"），具体细节需参考 RC1/RC2 的发布说明

**破坏性变更与迁移注意事项：** 无明确说明。作为稳定版晋级，建议用户正常执行升级流程并验证健康检查链路。


## 3. 项目进展（今日合并/关闭的关键 PR）

### 🔶 核心架构：Pluggable Agent Loops（Epic #7482）

这是今日最重要的战略进展。**Epic #7482 从讨论阶段进入全面拆解实施阶段**——17 个实施子任务被创建并快速关闭（大部分在数小时内完成绑定决策记录）。关键里程碑为 **M0 阶段（Spike）**：

- **PR #7606 [CLOSED]:** [Spike: iron-proxy placeholder-swap end-to-end in the Docker sandbox lane (#7482 M0)](https://github.com/nearai/ironclaw/issues/7606) — 证明该 Epic 风险最高的假设：在 Docker 沙箱中实现 `iron-proxy` 的占位符替换端到端流程

> ⚠️ **注意：** 这些子任务大部分以 Issue 形式存在并"关闭"（代表设计绑定决策已记录完毕），真正意义上的代码实现仅 **PR #7624 [OPEN]**（v0: ACP harness executor）被标记为"当前唯一需要动手实施的工作项"。

### 🔧 性能优化系列（serrrfirat 主导）

| PR | 标题 | 要点 |
|---|---|---|
| [#7628](https://github.com/nearai/ironclaw/pull/7628) | perf(processes): remove heartbeat journal churn | 停止为心跳追加 journal 行（#7591 的保守子集），减少 Postgres 写放大 |
| [#7629](https://github.com/nearai/ironclaw/pull/7629) | perf: reduce trigger and outbound state writes | 将 trigger 运行历史清理从每次 Running-row 更新移至首次 fire claim |
| [#7631](https://github.com/nearai/ironclaw/pull/7631) | perf(events): coalesce runtime milestone writes | 创建共享的 CoalescingEventSink，合并主机运行时事件、循环里程碑等持久化写入 |
| [#7630](https://github.com/nearai/ironclaw/pull/7630) | perf(stress): measure per-turn Postgres writes | 新增 `db-write-measurement` 压力测试预置，量化每次用户轮次的 Postgres 写入量 |

**意义：** 四个性能 PR 构成递进关系——先测量（#7630）、再削减（#7628/#7629）、再合并（#7631），与 Issue **#7591（性能 Epic）** 形成闭环。

### 📄 文档与 CI 加固（doc-truth 系列）

- **PR #7376 [CLOSED]:** [ci(check-guidance): extend the reference gate to the docs/ surface](https://github.com/nearai/ironclaw/pull/7376) — 将路径引用检查扩展到整个 docs/ 目录，包括中文镜像和内部契约文档
- **PR #7378 [OPEN]:** [test(docs): doc-fact contract tests for CLI, manifest, and Responses claims](https://github.com/nearai/ironclaw/pull/7378) — 为 CLI 和 manifest 的文档声明添加确定性契约测试

### 🛠️ 功能修复与增强

- **PR #7163 [CLOSED]:** [feat(documents): edit docx/xlsx/pptx structurally, render PDF from HTML](https://github.com/nearai/ironclaw/pull/7163) — 实现结构化 Office 文档编辑和 PDF 渲染（此前 #7109 只做了破坏性写入保护）
- **PR #7581 [CLOSED]:** [fix(extensions): refresh bundled MCP state after auth](https://github.com/nearai/ironclaw/pull/7581) — 修复 OAuth 发现后扩展示状态未刷新的问题
- **PR #7531 [CLOSED]:** [fix(loop): make repeated-call detection advisory-only](https://github.com/nearai/ironclaw/pull/7531) — 将重复调用检测从硬限制改为仅警告
- **PR #7590 [CLOSED]:** [fix(live-canary): align the bundled-skill marker owner with the runtime mint](https://github.com/nearai/ironclaw/pull/7590) — 修复 Live Canary 中技能快照验证失败的根因

**综合评估：** 项目在性能优化、稳定性修复、文档质量三线并进，且引入了测量驱动的优化方法论（#7630），整体工程成熟度提升明显。

**PR #7184 (Nostr):** [feat: Nostr host functions for WASM tools (reborn)](https://github.com/nearai/ironclaw/pull/7184)（新贡献者，待审查中）


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 热度与诉求分析 |
|---|---|---|---|
| 🥇 | [#7482 Epic: Pluggable agent loops](https://github.com/nearai/ironclaw/issues/7482) | 6 | **核心争议点：** IronClaw 是否应该继续自己实现 agent loop 和 tool 代码，还是变为调度/安全/审计的 **kernel**，将循环执行交给外部 harness（claude-code、pi、codex）。评论中已产生 7 条**绑定决策**（binding decisions），直接决定后续架构走向。**社区核心诉求：**将通用 agent 能力外包、自研聚焦差异化 |
| 🥈 | [#6257 PDF MIME 类型错误](https://github.com/nearai/ironclaw/issues/6257) | 4 | 用户报告发送/生成 PDF 时报 `Invalid value (attachments.mime_type)` 错误，已开放 25 天未关闭，社区持续关注修复进展 |
| 🥉 | [#2117 ironclaw-bridge 本地文件桥接](https://github.com/nearai/ironclaw/issues/2117) | 2 | 云托管场景下用户无法访问本地文件（Obsidian vault、本地项目目录），社区强烈期望此能力，👍 数最高（1） |
| / | [#7185 跨会话记忆不可靠](https://github.com/nearai/ironclaw/issues/7185) | 2 | 多位测试者独立观察到上下文无法在后续会话中被可靠召回，涉及实际使用场景的核心体验 |
| / | [#7621–#7624 四个 #7482 子实施任务](https://github.com/nearai/ironclaw/issues/7621) | 各 1 | 虽为内部拆解任务，但体现了社区对 #7482 推进节奏的关注 |

**简析：** 今日社区讨论高度集中于 #7482 Epic 的绑定决策过程；真正来自用户侧的痛点集中在 PDF 处理（#6257）和本地文件访问（#2117）。


## 5. Bug 与稳定性

> 按严重程度从高到低排列。

| 严重度 | Issue | 描述 | 状态 | 对应修复 |
|---|---|---|---|---|
| 🔴 高 | [#7626 自定义 MCP 认证卡死](https://github.com/nearai/ironclaw/issues/7626) | 用户连接需要浏览器/邮件验证的 MCP 时，IronClaw 卡住无响应 | **OPEN**（今日新增） | 未发现对应 PR |
| 🔴 高 | [#7589 Sonnet-5 500 错误](https://github.com/nearai/ironclaw/issues/7589) | NEAR AI Cloud 上 Sonnet-5 已连续三天返回 500 错误 | **CLOSED**（今日） | 关联 nearai/cloud-api#920，属上游服务问题 |
| 🟡 中 | [#6257 PDF MIME 类型错误](https://github.com/nearai/ironclaw/issues/6257) | 发送/生成 PDF 时报 `Invalid value (attachments.mime_type)` | **OPEN**（25 天） | 未发现对应 PR，值得关注 |
| 🟡 中 | [#7627 GitHub 扩展假连接](https://github.com/nearai/ironclaw/issues/7627) | 输入任意凭据（如 "1"）后 GitHub 扩展仍显示已连接 | **OPEN**（今日新增） | 未发现对应 PR |
| 🟢 低 | [#7185 跨会话记忆不可靠](https://github.com/nearai/ironclaw/issues/7185) | 前一个会话建立的信息在后续会话中无法可靠召回 | **OPEN**（10 天） | 未发现对应 PR，可能与 memory 子系统架构相关 |

**特别关注：** 今日新开的两个 Bug（#7626、#7627）均涉及**认证流程**（MCP 浏览器认证、扩展凭据验证），可能与近期安全加固（#7482 中的安全不变量）相关，建议维护团队重点排查。**PR #7581**（[扩展 MCP 认证后状态刷新](https://github.com/nearai/ironclaw/pull/7581)）可能部分缓解此类问题，但针对 #7626 和 #7627 的直接修复尚未出现。


## 6. 功能请求与路线图信号

### 🔥 路线图级信号

| 信号来源 | 功能方向 | 分析 |
|---|---|---|
| **Epic #7482** 子任务全量拆解（#7606–#7624） | **可插拔 Agent Loops** | 已产生 7 条绑定决策。值得特别关注的是：**#7624 明确 v0 只做 claude-code 适配**（"dev-only yolo"），pi 和 codex 适配器留待后续阶段；**#7482 中 ACP 从"核心目标"降级为 "one driver implementation"**。这是**路线图重大修正**——ACP 不再作为战略架构，而是众多 harness driver 之一 |
| **Issue #2117**（👍 1，已开放 4 个月) | **ironclaw-bridge 本地文件/MCP 桥接守护进程** | 虽已长时间未实施，但属于典型的用户刚需场景。建议维护者评估是否与 #7482 的"外接 harness"方向协同落地——若 agent 跑在云端而文件存在本地，此 bridge 的价值在 #7482 框架下将**更加凸显** |
| **PR #7184**（新贡献者） | **Nostr 主机函数**（WASM 工具） | 新贡献者 Kampouse 实现 Nostr 签名等能力。属于小众但明确的方向扩张，值得关注是否纳入 v1.3 |
| **PR #7513**（新贡献者） | **ACP serve 命令**（stdio 流式支持） | 与 Epic #7482 中 ACP 降级的决定可能产生冲突，需维护者明确此 PR 的定位 |
| **PR #7633**（新的，XL 级） | **Unbound turns 设计**（#7562） | 线程作为协调器工作单元、内核剥离回复路由，是架构级变更 |

### 🧩 功能请求（来自 Issue）

- **#7580:** [在 Web UI 中暴露 IronClaw Reborn 版本号](https://github.com/nearai/ironclaw/issues/7580) — 低成本、高可发现性的 UI 改进，建议快速跟进
- **#7482 系列:** 部分子任务也包含可用户感知的新能力（如 #7623 的 `ic` CLI、#7621 的模型直通）

### ⚖️ 冲突风险

**PR #7513（ACP serve 命令）** 与 Epic #7482 中 "ACP 降级为众多 driver 之一" 的决定存在张力。若 #7513 先于 #7482 落地，可能造成 ACP 维护成本重复投入。建议维护者明确先后关系。


## 7. 用户反馈摘要

### 真实痛点

| 反馈来源 | 痛点 | 场景描述 | 情绪 |
|---|---|---|---|
| [#6257](https://github.com/nearai/ironclaw/issues/6257)（25天未关闭） | PDF 附件的 MIME 类型校验失败 | 用户尝试发送/生成 PDF 文件时持续报错，无法完成基本操作。原始报告来自 Slack 的 `#x-ai-product-feedback` 频道，说明此问题已传播到社区 | 🔴 不满（等待过久） |
| [#7185](https://github.com/nearai/ironclaw/issues/7185) | 跨会话记忆不可靠 | 用户在多个会话中建立的信息（上下文）在后续对话中无法被召回。涉及法律（Devon）等专业场景，代理"忘记"用户信息会导致实际工作断裂 | 🟡 焦虑 |
| [#2117](https://github.com/nearai/ironclaw/issues/2117)（4个月未解决） | 云托管后本地文件无法访问 | 用户从云主机无法访问本地 Obsidian vault 等资源，blocker 级别的使用障碍 | 🟡 期待（👍 1） |
| [#7580](https://github.com/nearai/ironclaw/issues/7580) | Web UI 不显示版本号 | 用户想确认自己运行的版本但找不到入口，反映 UI 可发现性不足 | 🟢 中性 |

### 使用场景亮点

- **本地知识库场景：** #2117 中提到的 Obsidian vault 访问需求，说明部分用户将 IronClaw 作为本地优先的知识管理工具使用
- **专业领域辅助：** #7185 中提到的法律场景（Devon），说明 IronClaw 已进入专业工作流
- **跨平台开发场景：** #7482 中想要的 claude-code / pi / codex 集成，代表用户有"保留自己熟悉的上层 Agent 界面、用 IronClaw 做安全与调度底座"的真实需求


## 8. 待处理积压

### ⚠️ 需重点关注的遗留问题

| 类型 | 编号 | 标题 | 开放时长 | 说明 |
|---|---|---|---|---|
| Issue | [#6257](https://github.com/nearai/ironclaw/issues/6257) | PDF MIME 类型错误 | 25 天 | 直接阻塞用户基本操作，无对应 PR，应优先处理 |
| Issue | [#2117](https://github.com/nearai/ironclaw/issues/2117) | ironclaw-bridge 本地文件/MCP 桥接 | **4 个月** | 高需求但长时间未实施。建议与 #7482 统筹规划 |
| Issue | [#7185](https://github.com/nearai/ironclaw/issues/7185) | 跨会话记忆不可靠 | 10 天 | 影响核心体验，需要深入分析 memory 子系统设计 |
| PR | [#7184](https://github.com/nearai/ironclaw/pull/7184) | Nostr 主机函数（WASM 工具） | 9 天 | 新贡献者，无维护者反馈。需要明确预期，避免贡献者失速 |
| PR | [#7020](https://github.com/nearai/ironclaw/pull/7020) | tokio-tungstenite 0.29→0.30 依赖升级 | 11 天 | 已有一段时间的依赖更新，应检查是否有冲突或待测试 |
| PR | [#7262](https://github.com/nearai/ironclaw/pull/7262) | wasm 组依赖升级（wit-component 0.254→0.256） | 8 天 | 与 WASM 工具链相关，建议关注兼容性 |

---

*本日报基于公开 GitHub 数据分析生成，数据窗口为 2026-08-13 至 2026-08-14（部分 Issue/PR 更新日期回溯至此前）。所有链接均指向具体 GitHub 页面，便于进一步追溯。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-14

## 今日速览

过去24小时内，LobsterAI 项目共产生 1 条 Issue 更新与 11 条 PR 更新，整体活跃度**中高**。值得关注的是，今日有 **6 条 PR 被关闭（其中 5 条为当日创建并合并）**，主要集中在渲染层 UI 重构（skills/MCP/kit 三视图统一、cowork 管理界面重构）及签到活动 evergreen 化改造，说明团队正在同步推进界面架构统一与运营功能迭代。与此同时，4 条 3 月底提交的 PR 仍在积压中（均已 stale），其中 3 条为测试补全类 PR，建议维护团队优先处理。测试覆盖补全工作正在持续进行中（Issue #1162 / PR #1165），项目健康度呈稳中有升态势。

## 版本发布

无新版本发布。

## 项目进展

今日共有 **5 条 PR 合并/关闭**，均于当日创建并完成合并，推进速度很快，聚焦于前端 UI 架构优化与运营功能迭代：

| PR | 内容 | 状态 |
|---|---|---|
| [#2488](https://github.com/netease-youdao/LobsterAI/pull/2488) | Refactor/cowork btw and management UI — cowork 管理界面重构 | 已关闭 |
| [#2487](https://github.com/netease-youdao/LobsterAI/pull/2487) | refactor(skills): merge skills and mcp views into unified skills-and-connectors view — 将 Skills 与 MCP 视图合并为统一的 skills-and-connectors 页面 | 已关闭 |
| [#2486](https://github.com/netease-youdao/LobsterAI/pull/2486) | refactor(mcp): unify MCP card/detail UI with kits and skills styling — 提取共享 CardOverflowMenu 组件，新增 McpCard 与 McpDetailModal，重构 McpManager 列表/详情流程 | 已关闭 |
| [#2485](https://github.com/netease-youdao/LobsterAI/pull/2485) | feat(activity): support evergreen daily check-in — 签到活动从一次性活动改为常驻形态，补充状态自动刷新，积分入口改跳网页 | 已关闭 |
| [#2484](https://github.com/netease-youdao/LobsterAI/pull/2484) | Feat/enterprise edition — 企业版（内容待补充） | 已关闭 |

**解读**：今日合并 PR 全部由 `fisherdaddy` 和 `btc69m979y-dotcom` 提交，说明这些工作是同一批并行推进的 UI 统一化改造。值得关注的有两点：① **Skills/MCP/Kit 三大模块的卡片样式、菜单组件和排版规范完成统一**，提升了交互一致性和代码复用性；② **签到活动从一次性活动改为常驻（evergreen）形态**，产品运营层面新增了常驻用户激励入口。

**里程碑意义**：企业版（#2484）虽 PR 内容为空，但标签包含 `area: main`、`area: openclaw` 等多个核心模块，该 PR 已关闭说明企业版架构工作可能已启动或合入，建议后续版本留意企业版功能落地。

## 社区热点

- **Issue #1162 — [openclawMemoryFile 与 openclawLocalTimeContextPrompt 补充 Vitest 单元测试](https://github.com/netease-youdao/LobsterAI/issues/1162)** — 该 Issue 创建于 3 月 31 日，今日有 1 条新评论，为长时间悬而未决的测试覆盖议题重新获得了关注。其核心诉求是：`openclawMemoryFile.ts`（记忆文件核心管理模块）与 `openclawLocalTimeContextPrompt.ts`（时间上下文 Prompt 生成）此前**零测试覆盖**，而记忆管理模块涉及 SQLite 迁移、工作区切换同步等多处高风险逻辑。关联 PR [#1165](https://github.com/netease-youdao/LobsterAI/pull/1165) 已提交 75 个 Vitest 单元测试，但同样处于 stale 状态。

- **PR #1163 — [定时任务"立即运行"交互反馈补全](https://github.com/netease-youdao/LobsterAI/pull/1163)** — 创建于同日但内容详实，针对定时任务交互体验的四大根因（缺少 loading 状态、IPC 层同步阻塞、15 秒轮询延迟、右键菜单样式不一致）逐一提出解决方案。该 PR 长期处于 OPEN + stale 状态，但讨论涉及的用户体验问题——"点击后无反馈，容易导致重复点击"——仍是核心痛点。

## Bug 与稳定性

今日无新提交的 Bug 报告。但以下 **stale 状态的 PR** 涉及已知功能性缺陷，需关注：

| 严重程度 | 问题 | 状态 | 说明 |
|---|---|---|---|
| 中 | [#1163](https://github.com/netease-youdao/LobsterAI/pull/1163) 定时任务"立即运行"无交互反馈，状态需最长 15 秒轮询才能刷新 | OPEN + stale | 已有修复 PR 但尚未合入，建议优先处理 |
| 中 | [#1232](https://github.com/netease-youdao/LobsterAI/pull/1232) 定时任务首次执行（`previousRunAtMs === 0`）时结果不推送至 UI | OPEN + stale（当日有更新） | 根因清晰（pollOnce 条件判断缺陷），修复代码已就绪 |
| 低 | [#1166](https://github.com/netease-youdao/LobsterAI/pull/1166) 自定义 Agent 名称允许重复提交，导致列表歧义 | OPEN + stale | 修复方案为 renderer 层增加重名校验，待合入 |

## 功能请求与路线图信号

- **常驻签到活动**（[PR #2485](https://github.com/netease-youdao/LobsterAI/pull/2485)）— 已从一次性活动改为 evergreen 形态，说明团队正在增强用户日常活跃激励机制。未来可能持续在积分体系、活动入口、多活动并行展示上继续迭代。
- **Skills/MCP/Kits 三视图统一**（[PR #2487](https://github.com/netease-youdao/LobsterAI/pull/2487) / [#2486](https://github.com/netease-youdao/LobsterAI/pull/2486)）— 合并了 skills 与 MCP 页面，统一了卡片样式与交互组件。下一步可能继续深化"skills-and-connectors"大统一概念，将更多插件/连接器管理纳入该视图。
- **企业版**（[PR #2484](https://github.com/netease-youdao/LobsterAI/pull/2484)）— 已关闭，虽细节未公开，但涉及 main 与 openclaw 核心区域，应为企业级功能和部署形态在做底层准备。
- **OpenClaw 技能键按 frontmatter name 匹配**（[PR #2483](https://github.com/netease-youdao/LobsterAI/pull/2483)）— 修复目录名与 frontmatter name 不一致导致 UI 开关失效的问题。这条修复对技能管理体验很重要，预计将进入下一版本。

## 用户反馈摘要

- **测试覆盖缺失影响信心**（Issue #1162）：用户（开发者）指出 `openclawMemoryFile.ts` 涉及 SQLite 迁移、工作区切换记忆同步等高风险逻辑，但此前完全没有测试保护。这反映出贡献者对核心模块稳定性存在顾虑，75 个测试的补齐将大幅提升后续修改的信心。

- **定时任务交互痛点**（PR #1163）：用户明确描述了"点击立即运行后界面无任何反馈 → 等待最长 15 秒轮询 → 容易导致重复点击"的糟糕体验链条。高频重复操作场景下缺少即时反馈是该问题被长期保留的核心原因。

- **Agent 重名困惑**（PR #1166）：创建自定义 Agent 时后端未校验重名，用户被迫手动搜查已有同名 Agent 进行甄别，说明名称唯一性校验是 Agent 创建流程的必需约束。

## 待处理积压

以下共 **4 条 PR / 1 条 Issue** 处于 long-stale 状态，其中 3 条为 3 月 31 日提交的测试补全，极不建议继续延后，否则可能遭受解冲突成本；另有 1 条功能修复：

**测试补全类（无冲突风险，建议加速合入）**

- [PR #1156](https://github.com/netease-youdao/LobsterAI/pull/1156) — 为 commandSafety 与 coworkMemoryJudge 补充 Vitest 单元测试（两个高安全相关性模块）
- [PR #1165](https://github.com/netease-youdao/LobsterAI/pull/1165) — 为 openclawMemoryFile 与 openclawLocalTimeContextPrompt 新增 75 个 Vitest 测试
- [Issue #1162](https://github.com/netease-youdao/LobsterAI/issues/1162) — 对应上述 PR 的跟踪 Issue，评论数 1，已 stale

**功能修复类（影响用户体验与数据一致性）**

- [PR #1163](https://github.com/netease-youdao/LobsterAI/pull/1163) — 定时任务"立即运行"交互反馈补全，优化更新状态实时同步（含 IPC 层 async 化改造）
- [PR #1232](https://github.com/netease-youdao/LobsterAI/pull/1232) — 修复定时任务首轮执行结果不推送 UI 的问题
- [PR #1166](https://github.com/netease-youdao/LobsterAI/pull/1166) — 防止自定义 Agent 名称重复

**建议**：在推进 UI 重构的同时，4 条 stale PR 的核心代码均已就绪且冲突面积可控，若持续搁置，将在下轮大版本迭代中面临 rebase 成本陡增的风险。

---

> 📅 本日报由 AI 分析师自动生成，数据截至 2026-08-14T00:00:00Z，来源：[LobsterAI GitHub 仓库](https://github.com/netease-youdao/LobsterAI)。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-14

**数据窗口**: 2026-08-13 至 2026-08-14 | **数据来源**: github.com/moltis-org/moltis


## 1. 今日速览

Moltis 项目今日保持稳定的开发节奏：24小时内共产生 1 条 Issue 和 4 条 PR，均处于开放/活跃状态，无新版本发布。值得关注的是，维护者 Lstarsky0 集中提交了 3 个修复类 PR（#1191、#1192、#1194），全部针对 macOS 兼容性和上游组织迁移引发的构建问题，显示出对开发者体验的快速响应。新报告的 Issue #1193 指向一个只在全量测试套件下出现的 flaky test，属于典型的并发压力下的时序问题，严重性中等。社区方面，PR #1190（新增 CalDAV/渠道历史连接器）体量较大，正在等待评审，是当前最具功能性价值的待合并贡献。整体来看，项目处于健康的"修复与扩展并行"阶段。

**活跃度评估**: 中高（4个PR+1个Issue/24h，维护者响应积极）


## 2. 版本发布

过去 24 小时内无新版本发布（最新 Release 保持前序版本）。值得注意的是，当前有 4 个已提交 PR 正在等待合并，若 #1191 和 #1192 的修复顺利合入，预计会在下一个 patch 版本中解决 macOS 与 openclaw 重定向相关的构建/安装问题。


## 3. 项目进展

今日无 PR 被合并或关闭，4 个开放 PR 构成当前主要的项目推进方向：

| PR | 类型 | 推进内容 | 关键影响 |
|----|------|----------|----------|
| [#1194](https://github.com/moltis-org/moltis/pull/1194) | 修复 | macOS bash 3.2 空数组展开保护 | 修复 `just local-validate-full` 在 macOS 上因 `set -euo pipefail` 下空数组展开导致的崩溃，提升本地开发体验 |
| [#1190](https://github.com/moltis-org/moltis/pull/1190) | 功能 | 新增 CalDAV 与多渠道历史连接器 | 引入 provider-neutral 持久化层、原子快照、投影与受限本地全文搜索；新增只读 CalDAV 数据集，以及 Slack/Discord/Matrix/Teams 消息历史数据集（不复制渠道凭据）。同时新增 prompt 相关能力——这是自上次发布以来最大规模的功能性 PR |
| [#1192](https://github.com/moltis-org/moltis/pull/1192) | 修复 | wacrawl 技能安装路径指向 openclaw 组织 | 修复 Go install 回退因上游仓库迁移（steipete/wacrawl → openclaw/wacrawl）而失败的问题 |
| [#1191](https://github.com/moltis-org/moltis/pull/1191) | 修复 | gogcli 模块路径指向 openclaw 组织 | 修复 `moltis sandbox build` 在每一个预构建镜像上失败的问题，根因是 gogcli 迁移到 openclaw 组织后 `go.mod` 路径变更 |

**整体评估**: 功能性推进主要依赖 #1190（连接器扩展），而 #1191/#1192/#1194 三个修复 PR 代表着对工具链稳定性的集中投入，尤其是解决上游仓库迁移（steipete → openclaw）带来的连锁影响。


## 4. 社区热点

今日无单条讨论特别激烈的 Issue/PR（#1193 尚为 0 评论，#1194/#1191/#1192 评论数均为 0）。不过从 PR 提交密度来看，**PR #1192 和 #1191 形成了"同一根因、不同位置"的修复组合**——上游仓库从 `steipete` 迁移至 `openclaw` 组织，导致两处依赖（技能安装 + 沙箱构建）同时失效。这反映出上游生态变动对下游项目的连锁影响，也是社区协作中常见的迁移阵痛。另一值得关注的是 PR #1190（大型功能 PR），其覆盖面广（CalDAV + 4 个渠道 + 持久化），但尚未获得评论，可能存在评审积压的风险。


## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 | 修复 PR |
|----------|------|------|---------|
| 中 | **#1193 Flaky test**: `fanout_is_bounded_and_times_out_a_hung_endpoint` 在全量测试套件下间歇性失败（3 次全量运行中失败 2 次），仅在负载较高时触发，空闲 10 核 macOS 上复现 | 开放中，无评论，未分配 | 暂无 |
| 中 | **#1191 `moltis sandbox build` 全量失败**: 所有预构建镜像构建失败，因为 `go install github.com/steipete/gogcli/cmd/gog@latest` 在 openclaw 迁移后无法解析 | 已有修复 PR 开放中 | [#1191](https://github.com/moltis-org/moltis/pull/1191) |
| 低 | **#1192 `wacrawl` 技能安装失败**: Go install fallback 因模块路径迁移而失效 | 已有修复 PR 开放中 | [#1192](https://github.com/moltis-org/moltis/pull/1192) |
| 低 | **#1194 macOS 本地校验脚本崩溃**: `just local-validate-full` 无 PR 参数时因 bash 3.2 空数组展开而立即失败 | 已有修复 PR 开放中 | [#1194](https://github.com/moltis-org/moltis/pull/1194) |

**分析**: #1193 的 flaky test 虽不阻塞发布，但指向 push fanout 超时机制在系统级负载下的潜在竞争条件，建议维护者关注测试的时序假设（timeout assertion）是否需要在高并发环境下放宽。相比之下，#1191 是当前影响面最大的功能性 bug（sandbox build 全量不可用），修复 PR 已就绪。


## 6. 功能请求与路线图信号

今日无新功能请求类 Issue。但开放中的 PR #1190 释放了强烈的路线图信号：

- **连接器生态扩展**: CalDAV（只读）与 Slack、Discord、Matrix、Teams 四类渠道的消息历史连接器，均采用 provider-neutral 设计，不复制渠道凭据——这是 Moltis 从"实时网关"向"历史上下文 + 日历感知"双向延伸的一步。
- **数据持久化能力**: 原子快照（atomic snapshots）、调度（scheduling）、投影（projections）、受限本地全文搜索——这组基础设施是未来支持离线/长期记忆类 Agent 场景的必要条件。
- **Prompt 增强**: 新增 prompt 相关内容暗示连接器数据将直接服务于 Agent 上下文构建。

结合当前项目定位（AI 智能体网关），**PR #1190 如果合入，将显著拓宽 Moltis 在企业知识库与团队协作场景下的接入能力**，建议维护者优先安排评审。


## 7. 用户反馈摘要

今日 Issue/PR 评论区暂无明显用户反馈（所有条目评论数均为 0 或 undefined）。从 PR 提交本身可间接推断：

- **macOS 开发者体验仍是持续痛点**: #1194 的作者在 macOS 上执行本地校验直接崩溃，且 root cause 为 bash 3.2 兼容性，反映了项目在跨平台脚本健壮性上仍有提升空间。
- **对上游迁移的敏感度**: 两个独立问题（#1191、#1192）均源于开源生态中的仓库迁移，说明 Moltis 的安装/构建链路对上游依赖的固定（pinning）不够严格，用户（包括 CI 和本地开发者）会直接受到上游变动影响。


## 8. 待处理积压

| 项目 | 类型 | 持续时间 | 状态 | 建议 |
|------|------|----------|------|------|
| [#1190](https://github.com/moltis-org/moltis/pull/1190) 大型连接器功能 PR | PR | 创建于 08-11，已持续 3 天 | 开放、0 评论 | ⚠️ 需要维护者优先评审。这是当前最大的功能增量（约覆盖 5 种连接器 + 持久化层 + prompt），长时间无评审可能引发贡献者流失风险 |
| [#1193](https://github.com/moltis-org/moltis/issues/1193) Flaky test | Issue | 创建于 08-13 | 开放、0 评论 | 建议标记 `good first issue` 或分配给熟悉 push fanout 模块的维护者，避免进入长期未处理的 flaky 黑洞 |

---

**总结**: Moltis 项目健康度良好，维护者响应积极（24h 内提出 3 个修复 PR），功能性扩展（#1190）正在评审窗口。最大的短期风险是 #1191 导致 sandbox build 全量失败但修复合入节奏尚未明确；中期需关注 #1193 的 flaky test 所反映的并发时序鲁棒性问题。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，我是您指定的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 CoPaw 项目（github.com/agentscope-ai/CoPaw）在 2026-08-14 的 GitHub 数据生成的项目动态日报。

---

# CoPaw 项目动态日报 | 2026-08-14

## 1. 今日速览

CoPaw 项目今日活跃度极高，处于快速迭代状态。过去 24 小时内，Issue 与 PR 的更新总量接近百条（92 条），显示出强大的社区参与度和维护团队的高效响应。项目核心进展集中在 **v2.1.0 正式版的发布**（带来了全新的 QwenPaw OS Shell 桌面环境），以及对 **安全漏洞**（特别是插件权限模型）和 **长期记忆（ReMe）功能** 的密集修复与增强。虽然社区反馈热烈，但安全问题与任务中断类 Bug 仍是当前用户最关切的痛点。

## 2. 版本发布

项目今日正式发布了 **v2.1.0** 版本，这是自 v2.0.0 桌面版以来的又一次重大更新。

- **[v2.1.0 - 正式版](https://github.com/agentscope-ai/CoPaw/releases/tag/v2.1.0)**
  - **核心亮点：QwenPaw OS Shell**。这是一个全新的桌面环境，支持在可移动、可调整大小的窗口中打开应用，并集成了启动器、任务栏、通知中心和已保存的布局功能。
  - **应用中心整合**：已安装应用与市场应用现在在 App Center 中共享同一个目录，统一了管理入口。
  - **其他**：该版本还包含了对聊天、记忆（Memory）和网站文档等模块的一系列修复与改进（由 v2.1.0-beta.x 版本累积而来）。
  - **⚠️ 破坏性变更与迁移**：当前发布说明中未明确列出破坏性变更。但鉴于引入了 OS Shell 这样的重量级新特性，建议用户在升级前**备份** `~/.qwenpaw` 或对应配置目录，并关注官方升级指南。

- **[v2.1.0-beta.5](https://github.com/agentscope-ai/CoPaw/releases/tag/v2.1.0-beta.5)** (预发布)
  - 作为 v2.1.0 正式版发布前的最后一个测试版，主要包含一些 Bug 修复，如处理类字典模型响应、简化长期记忆指导等。

## 3. 项目进展

今日合并/关闭的 19 个 PR 展示了项目在稳定性和新功能上的双向推进：

- **任务控制与稳定性**：
  - **[fix(mission): enforce max_iterations server-side in MissionGate (#6652)](https://github.com/agentscope-ai/CoPaw/pull/6652)**：这是一个重要的修复。它解决了任务模式下，控制器 LLM 可以无限分发子代理直到账户余额耗尽的问题，现在服务端将强制执行 `max_iterations` 配置。
  - **[fix(chats): add pagination to chat history and enable GZip compression (#6636)](https://github.com/agentscope-ai/CoPaw/pull/6636)**：修复了长聊天记录加载导致的 30 秒超时问题，通过分页和 GZip 压缩显著提升了聊天历史的加载性能。
- **渠道与依赖**：
  - **[feat(channels): install optional dependencies on demand (#6387)](https://github.com/agentscope-ai/CoPaw/pull/6387)**：合并了按需安装渠道 SDK 的 PR，这将使核心安装包更轻量。
- **记忆与上下文**：
  - **[fix: make Auto-Dream integration resilient (#6884)](https://github.com/agentscope-ai/CoPaw/pull/6884)**：使自动梦想集成对 LLM 的结构化输出更具鲁棒性，避免因单次失败导致整个任务崩溃。

**结论**：项目本周期的开发重心正在从单纯的功能堆叠转向**精细化打磨**，包括服务端强制执行、性能优化和容错处理，这是项目走向成熟的标志。

## 4. 社区热点

今日最热门的讨论集中在以下几个议题：

- **[Issue #6921: 任务执行中无提示中断，需手动“继续”](https://github.com/agentscope-ai/CoPaw/issues/6921)** (6 条评论)
  - **诉求**：用户反馈在规划好下一步后，智能体会无提示地停止，而不是继续执行。这是影响任务自动化流畅度的关键体验问题。
- **[Issue #6973: 支持阿里云百炼 token plan](https://github.com/agentscope-ai/CoPaw/issues/6973)** (5 条评论)
  - **诉求**：用户希望 CoPaw 能接入阿里云百炼的计费方案，表明社区对国内云服务商和计费模式有明确的集成需求。
- **[Issue #6811: OpenAI Responses 续写摘要忽略思考禁用设置](https://github.com/agentscope-ai/CoPaw/issues/6811)** (5 条评论，已关闭)
  - **诉求**：这是一个技术性 Bug，反映高级用户对模型调用细节（如 `disable_thinking`）的控制需求，同时指出了 UI 误报错误信息的问题。
- **[Issue #6992/#6993: 重大架构漏洞与安全问题](https://github.com/agentscope-ai/CoPaw/issues/6992)** (3+1 条评论，其中一个已关闭)
  - **诉求**：这是今日最严重的议题。社区用户上报了端口暴露和 API 无鉴权等严重安全漏洞，虽然被标记为无效，但引发了大量关注。这提醒项目方需要更清晰的安全边界声明和沟通。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **严重（安全问题）**：
  - **[Issue #6916: 插件可静默创建定时任务并注入消息](https://github.com/agentscope-ai/CoPaw/issues/6916)** (已关闭)：关于权限模型漏洞的报告，插件可在无用户确认下执行持久化操作。
  - **[Issue #6992: 端口暴露、API无鉴权](https://github.com/agentscope-ai/CoPaw/issues/6992)** (已关闭)：虽然是误报，但凸显了用户对网络暴露和API安全的忧虑。**关联 PR:** 暂无，但项目方应以文档或配置默认值的方式消除此类顾虑。
- **高（功能阻断/严重异常）**：
  - **[Issue #6921: 任务无提示中断](https://github.com/agentscope-ai/CoPaw/issues/6921)**：影响核心任务流程，需要“继续”才能执行。**关联 PR:** 暂无，是当前最需要关注的稳定性问题之一。
  - **[Issue #6768: 任务完成后进入无限循环](https://github.com/agentscope-ai/CoPaw/issues/6768)** (已关闭)：导致会话阻塞数小时，根因是子代理不断派发任务。
  - **[Issue #7008: Anthropic 模型误审核图片导致会话中断](https://github.com/agentscope-ai/CoPaw/issues/7008)**：模型端安全审核误判，导致长会话中断，用户体验受损。
- **中（功能缺陷/体验不佳）**：
  - **[Issue #6951: 压缩后聊天记录不可见](https://github.com/agentscope-ai/CoPaw/issues/6951)**：上下文压缩策略导致了用户界面层的数据丢失（虽然数据仍在历史库中）。
  - **[Issue #6955: 启动概率性崩溃](https://github.com/agentscope-ai/CoPaw/issues/6955)**：Windows 和 pip 安装环境下，启动时崩溃，且无明确报错。
  - **[Issue #7007: Windows Desktop TUI 连接失败](https://github.com/agentscope-ai/CoPaw/issues/7007)**：打包版的 TUI 无法启动 ACP 后端。

## 6. 功能请求与路线图信号

社区对功能的需求呈现出多元化和专业化趋势，部分请求已有对应的 PR 跟进：

- **集成与生态**：
  - **[Issue #6973: 支持阿里云百炼 token plan](https://github.com/agentscope-ai/CoPaw/issues/6973)**：云服务集成的本地化需求。
  - **[Issue #6882: 怎么集成 CopilotKit](https://github.com/agentscope-ai/CoPaw/issues/6882)**：希望与前端 Copilot 框架集成，扩展应用场景。
- **用户体验增强**：
  - **[Issue #6970: 可嵌入的聊天界面与增强的会话筛选](https://github.com/agentscope-ai/CoPaw/issues/6970)**：建议提供无侧边栏的聊天界面，方便嵌入，并增强 session 列表查询功能。
  - **[Issue #7002: 服务器端代理客户端](https://github.com/agentscope-ai/CoPaw/issues/7002)**：希望在个人电脑上安装一个轻量级代理，连接服务器上的 CoPaw 核心，解决桌面端臃肿和数据同步问题。
  - **[Issue #6995: 注入当前渠道到Shell环境变量](https://github.com/agentscope-ai/CoPaw/issues/6995)**：小但实用的功能，方便外部脚本感知调用来源。
- **路线图信号**：
  - **[PR #6960: Pawport - 从其他 Agent 导入配置/技能/插件](https://github.com/agentscope-ai/CoPaw/pull/6960)**：该 PR 显示了 CoPaw 有意降低从其他 AI Agent（如 Codex, Qoder）迁移的门槛，是构建生态的重要一步。
  - **[Issue #7003: 内存优化方案 ViBo](https://github.com/agentscope-ai/CoPaw/issues/7003)**：虽然被关闭，但表明了社区对长上下文窗口成本的关注，项目方在记忆优化上的投入（如 ReMe）与此诉求一致。

## 7. 用户反馈摘要

- **最核心痛点**：**任务执行过程不透明且不稳定**。顶部评论区反复出现“无提示就停止”、“无限循环”、“会话被阻断”等描述（如 #6921, #6768），这表明在复杂多步骤任务下，智能体的自主决策和异常处理机制仍需加强，用户对“自动驾驶”的信任度因此受到影响。
- **对安全性的高度敏感**：关于安全漏洞的报告虽未证实，但传播极快，说明用户高度关注项目的安全性，特别是在涉及插件和网络暴露时。
- **中文社区活跃且反馈具体**：大量高质量的中文 Issue（如 #6951, #6955, #7008）不仅描述了现象，还提供了日志和详细分析，帮助开发者快速定位问题，是社区健康的积极信号。

## 8. 待处理积压

以下为长期未关闭但重要的问题，建议维护者优先关注：

- **[Issue #6047: 升级后新聊天会话重新打开旧会话](https://github.com/agentscope-ai/CoPaw/issues/6047)** (07-13 创建，已关闭)：虽然已关闭，但涉及升级后数据一致性问题，建议确认修复方案的完备性。
- **[Issue #6100: 升级后工作区丢失](https://github.com/agentscope-ai/CoPaw/issues/6100)** (07-14 创建，已关闭)：同样为升级引发的配置被覆盖问题，与 #6047 同属升级路径上的风险，应保持关注。
- **[PR #6302: 统一 Provider 发现与模型路由](https://github.com/agentscope-ai/CoPaw/pull/6302)** (07-21 创建)：该 PR 是一个大型重构，涉及模型元数据、路由和Agent控制，长时间未合并可能意味着存在设计分歧或开发资源受限。该功能的完成度直接影响多模型管理的体验，值得重点关注。
- **[Issue #6585: 聊天界面“已接收字符”动态显示无开关](https://github.com/agentscope-ai/CoPaw/issues/6585)** (07-30 创建，已关闭)：UI 细节优化类需求，涉及用户注意力干扰问题，属于提升体验的好机会。

---
**日报结束**

*数据来源：CoPaw GitHub 仓库 (agentscope-ai/CoPaw) 在 2026-08-14 的公开活动数据。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-14

---

## 1. 今日速览

ZeroClaw 在过去 24 小时保持**高活跃度**：共产生 50 条 Issue 更新和 50 条 PR 更新，主要集中在安全加固、架构治理与开发者体验三大方向。安全类工作占据显著比重——包括 gateway 文件系统资产路径穿越修复（#9969，已合并）、Zhipu 兼容提供商凭据完整性修复（#9968）、以及会话队列序列化修复（#9674，已合并）等多项高风险 patch 落地。架构层面，多个 RFC 进入维护者评审队列（#8692 决策追踪、#8303 Goal mode v1、#9487 会话所有权），显示出 v0.9.0 在会话持久化、权限契约和工具策略上的深度设计正在收敛。值得关注的是，CI 基础设施在 Blacksmith runner 适配和 rust-cache 提供商感知方面有密集投入（#9962, #9980, #9985），体现项目对构建效率和可扩展性的重视。整体来看，项目处于**v0.9.0 破坏性变更前夜的集中加固期**，安全修复和架构决策双线推进，社区参与度高。

---

## 2. 版本发布

过去 24 小时内无新版本发布。

---

## 3. 项目进展

今日共合并/关闭 9 个 PR，以下为关键合并：

| PR | 标题 | 核心贡献 | 影响面 |
|---|---|---|---|
| [#9969](https://github.com/zeroclaw-labs/zeroclaw/pull/9969) | fix(gateway): contain filesystem dashboard assets | 对文件系统后端仪表盘资产路径进行 **canonicalize 解析 + 解析时根目录检查**，拒绝符号链接逃逸；修复了因客户端多字节编码映射到同一文件而导致的路径穿越风险 | **P1 安全修复**（已合并） |
| [#9674](https://github.com/zeroclaw-labs/zeroclaw/pull/9674) | fix(infra): preserve session queue serialization during eviction | 在 session-slot map 仍处于锁定时注册请求，防止空闲驱逐在 pending count 可见前移除已选槽位；引入 RAII guard 跟踪 pending 注册 | **P1 并发正确性修复**（已合并） |
| [#9709](https://github.com/zeroclaw-labs/zeroclaw/pull/9709) | fix(tts): clean up Edge TTS temp output on every error path | 修复 Edge TTS 临时文件在输出读取失败路径上的泄漏 | 稳定性改进（已合并） |
| [#9932](https://github.com/zeroclaw-labs/zeroclaw/pull/9932) | ci(codeql): drop rust/hard-coded-cryptographic-value | CodeQL 配置新增 query-filters，排除对 `cfg(test)` 代码产生 27 个全假阳性告警的查询规则 | CI 噪音削减（已合并） |
| [#9639](https://github.com/zeroclaw-labs/zeroclaw/pull/9639) | docs(architecture): document provider routing lifecycle | 新增 source-grounded 的提供商路由生命周期文档，涵盖 profile 构造、hint 路由、重试/回退顺序、冷却、流式恢复、no-replay 边界和 requested-vs-served 归因 | 架构文档补全（已合并） |
| [#9980](https://github.com/zeroclaw-labs/zeroclaw/pull/9980) | ci(docker): sticky-disk layer cache for PR image builds on Blacksmith | 为 PR 镜像构建引入粘性磁盘层缓存，缓解 GitHub 10GB/repo 缓存上限的抖动问题 | CI 基建优化（已合并） |
| [#9705](https://github.com/zeroclaw-labs/zeroclaw/pull/9705) | fix(config): allow config set on existing hyphenated cron aliases | 修复 `zeroclaw config set cron.<alias>.name` 拒绝含连字符的已加载 cron 任务的问题 | 配置 UX 修复（已合并） |
| [#9984](https://github.com/zeroclaw-labs/zeroclaw/pull/9984) | ci: rust-cache useblacksmith path validation | 临时验证 PR，确认 Blacksmith runner 上的缓存路径可用 | CI 验证（已关闭） |

**整体推进判断**：两个 P1 安全/正确性修复（#9969, #9674）的合入是今日最实质的进展，直接消除了 gateway 路径穿越和会话队列竞态两个高风险问题。此外，多个 CI 基建 PR 的连续合入表明项目在规模化构建效率上的投入正在加速。

---

## 4. 社区热点

### 讨论热度 Top 3

| Issue | 标题 | 评论数 | 焦点 |
|---|---|---|---|
| [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | RFC: Goal mode v1 — bounded foreground Matrix work | 20 | 跨多轮 agent 交互的有界目标模式设计，此前提案因耦合重启交接、扩展通道准入、Web 和异步子工作等问题被要求拆分 |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) | RFC: per-execution confirmation tier for high-risk shell commands | 18 | 高风险 shell 命令的分级确认策略 + Claude Code 风格命令模式策略（allow/ask/deny），已完成第三版修订 |
| [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) | Tracker: Maintainer decision queue for RFCs and design issues | 13 | RFC/设计问题决策队列追踪器，作为维护者审批的前置缓冲 |

### 背后的诉求分析

- **#8303（Goal mode v1）**：社区对"有界前台 Matrix 工作"的核心诉求是——agent 需要一种**持久化的、跨多个轮次**的目标追求机制，而非一次性 prompt。讨论焦点在于如何在不引入过度复杂性的前提下定义执行边界。20 条评论反映这是一个**设计层面分歧较大**的 RFC，维护者需要审慎评估范围划分。
- **#7155（shell 命令分级确认）**：这是**安全与可用性的经典权衡**。用户需要高风险的 shell 操作在每次执行前有明确的确认层级，但又不希望过度打扰。第三版修订将范围收窄到 reconciled shell-policy contract，表明设计正在趋于收敛。
- **#8692（维护者决策队列）**：评论量高说明社区对 **RFC 审批流程的可见性和确定性**有强烈需求。半年前提出的 RFC 仍在等待决策，社区希望有一个公共的决策队列来确保推进节奏。

---

## 5. Bug 与稳定性

### 已关闭 / 已修复

| Issue | 标题 | 严重度 | 修复 PR | 说明 |
|---|---|---|---|---|
| [#9389](https://github.com/zeroclaw-labs/zeroclaw/issues/9389) | unauthenticated POST /api/pair keys lockout on attacker-supplied header | **P1** | 待确认 | 未认证的配对端点将锁定状态绑定到攻击者可控的 header 上，可能被用于 DoS |
| [#9643](https://github.com/zeroclaw-labs/zeroclaw/issues/9643) | wit/VERSIONING.md 未将"向现有枚举添加变体"分类为破坏性变更 | P1 | 已修复 | 导致所有旧版编译插件无法实例化 |
| [#9366](https://github.com/zeroclaw-labs/zeroclaw/issues/9366) | WhatsApp Web 接受 `approval_timeout_secs` 但从不读取 | P2 | 已修复 | 配置项存在但无效果 |

### 仍开放的高风险 Bug

| Issue | 标题 | 严重度 | 状态 |
|---|---|---|---|
| [#9328](https://github.com/zeroclaw-labs/zeroclaw/issues/9328) | verifiable-intent 在验证凭据链前先求值约束 | **P2, risk:high** | in-progress, 已接受 |
| [#9929](https://github.com/zeroclaw-labs/zeroclaw/issues/9929) | headless SOP step turns 获得 session path 但从未持久化到 session store | **P1, risk:high** | blocked, 已接受 |

### 新增 Bug（近 48 小时开启）

| Issue | 标题 | 严重度 | 说明 |
|---|---|---|---|
| [#9951](https://github.com/zeroclaw-labs/zeroclaw/issues/9951) | WeChat 频道代码及其 51 个 lib 单元测试从未在 CI 中编译或执行 | P2 | 该功能在**任何** CI feature 组合中均未启用 |
| [#9978](https://github.com/zeroclaw-labs/zeroclaw/issues/9978) | DeepSeek Harness 设计思路（post-#7155 权限/沙箱路线图） | 非 Bug | 设计参考比照 |

**风险提示**：#9929 的 headless SOP session 持久化缺失属于 **S2（降级行为）** 且已被接受，但处于 blocked 状态——需要 #9600（session 持久化契约所有权）先落地才能推进。

---

## 6. 功能请求与路线图信号

### 高概率进入 v0.9.0 的功能（基于 PR 活跃度和 Issue 状态）

| 功能 | 对应 Issue/PR | 当前状态 | 预计影响 |
|---|---|---|---|
| **会话持久化契约重构** | [#9600](https://github.com/zeroclaw-labs/zeroclaw/issues/9600)、[#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) | tracker 已建立，4 个独立工作流需协调 | 高——涉及 runtime、gateway、web、channel 四层 |
| **SOP 能力权限契约** | [#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598) | Rev 3 已提交，分为临时路径和完全共享路径 | 中——影响 SOP 子轮的能力授权 |
| **统一 slash 命令注册表** | [#7929](https://github.com/zeroclaw-labs/zeroclaw/issues/7929) | needs-author-action | 中——消除 web UI/ZeroCode TUI/频道运行时三套命令定义漂移 |
| **OpenRouter session_id 传递** | [#9631](https://github.com/zeroclaw-labs/zeroclaw/issues/9631) | blocked, needs-author-action | 中——降低 prompt-cache miss 带来的成本 |
| **Agent Plugins 1.0 标准支持** | [#9810](https://github.com/zeroclaw-labs/zeroclaw/issues/9810) | RFC 评审中 | 高——可能成为 v0.9.0 的重要新能力 |
| **图像降级而非丢弃** | [#9887](https://github.com/zeroclaw-labs/zeroclaw/issues/9887) | blocked, 已接受 | 中——改善 multimodal 体验 |
| **Agent 便携式导出** | [#9986](https://github.com/zeroclaw-labs/zeroclaw/pull/9986) | 新 PR（2026-08-13） | 中——跨安装迁移 agent 工作流 |

### 值得关注的新信号

- **PR #9968**（fix(providers): preserve compatible-provider integrity）——Zhipu 凭据无法生成有效 JWT 时直接将其作为 bearer token 转发（fail-open），修复为 fail-closed。这与 #7155 的权限策略方向一致，表明**兼容提供商的安全边界正在被收紧**。
- **PR #9986**（feat(agents): export portable bundle）——这是一个新方向：将 agent 导出为可移植 bundle（manifest + config closure + workspace tree），方便跨实例迁移。暗示项目在**多实例部署和可移植性**上的关注度提升。

---

## 7. 用户反馈摘要

- **成本痛点（#9631）**：用户明确表示"通过 OpenRouter 的 agent 对话不必要地昂贵——单次对话产生数十个 LLM 请求，系统 prompt 和工具 schema 每次都被重放"。**核心诉求是让 ZeroClaw 对 provider 的缓存机制（如 session_id）友好**，直接关联用户的云成本。
- **移动端体验（#9895）**：Telegram `/model` 选择器在移动端"笨重"，用户需要**按提供商分组 + 分页**的内联键盘选择器。这是典型的移动端 UX 改进诉求，已有 accepted 状态。
- **错误配置的可发现性（#9942 PR）**：`vi_verify` 工具被隐藏时，运营者仅在 runtime trace 中收到通知——但当 `observability.log_persistence = "none"` 时该 trace **没有任何 sink**。修复方向是让通知通过 config surface 触达运维人员。
- **安全与可用性的平衡（#7155, #9968）**：多个安全相关讨论的核心张力是——**用户希望默认安全（fail-closed），但希望在可控范围内保留灵活性**。Zhipu 凭据 fail-open 的问题暴露了兼容层的一个潜在盲区。
- **插件生态信号（#9810）**：用户希望 ZeroClaw 支持 **Agent Plugins 1.0 标准**（vendor-neutral），以便加载社区插件包。这指向用户对**可扩展生态**的需求正在增长。

---

## 8. 待处理积压

### 长期未决的高优先级 RFC/Feature

| Issue | 标题 | 创建时间 | 已逾时 | 状态 | 阻塞因素 |
|---|---|---|---|---|---|
| [#5907](https://github.com/zeroclaw-labs/zeroclaw/issues/5907) | Opt-in LSP support for ZeroCode coding workflows | 2026-04-19 | **117 天** | needs-author-action | 等待作者补充设计细节 |
| [#6850](https://github.com/zeroclaw-labs/zeroclaw/issues/6850) | RFC: Decouple memory lifecycle policy from storage backends | 2026-05-22 | **84 天** | needs-author-action | 等待作者回应维护者评审意见 |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) | RFC: per-execution confirmation tier for high-risk shell commands | 2026-06-03 | **72 天** | needs-maintainer-review | 第三版已提交，等待维护者决策 |
| [#6998](https://github.com/zeroclaw-labs/zeroclaw/issues/6998) | Schema-validated memory consolidation with bounded fallback | 2026-05-29 | **77 天** | needs-author-action | 等待作者补充方案细节 |
| [#9323](https://github.com/zeroclaw-labs/zeroclaw/issues/9323) | Define execution-tree iteration budget ownership | 2026-07-24 | **20 天** | needs-author-action | 等待作者明确执行树迭代预算的归属方 |

### 维护者提醒

- **#8692（决策队列 tracker）** 是当前 RFC 积压的集中协调面。有多个 RFC 处于 needs-maintainer-review 已达数周（如 #7155, #9487），建议维护者优先在 #8692 中排出明确的决策时间线，以避免社区等待过久导致贡献动力下降。
- **#5907（LSP 支持）** 已积压近 4 个月，虽然功能本身为 opt-in enhancement，但若长期无实质推进，建议明确标记为 deferred 或 close，避免"僵尸 issue"。
- **#9420（Anthropic OAuth profiles 支持）** 是一个 large 规模 PR，已有一个月余未合入，当前为 needs-author-action——若功能方向确认无误，建议加快评审节奏。

---

*数据来源：[ZeroClaw GitHub Repository](https://github.com/zeroclaw-labs/zeroclaw) | 报告周期：2026-08-13 至 2026-08-14*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*