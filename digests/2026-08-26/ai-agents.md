# OpenClaw 生态日报 2026-08-26

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-26 00:32 UTC

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

# OpenClaw 项目动态日报 — 2026-08-26

## 今日速览

过去24小时内项目保持高强度迭代：共产生 500 条 Issue 更新（新开/活跃 437 条，关闭 63 条）和 500 条 PR 更新（待合并 256 条，合并/关闭 244 条），整体活跃度极高。P0/P1 级问题持续浮现，尤其集中在 SQLite 损坏复发（#126821）、消息丢失（#127710, #127948）与会话状态管理领域；同时仍有大量长期积压的 P2/P3 功能请求（如 #45758 YAML 配置、#16670 记忆设置引导）等待维护者决策。社区讨论热度集中于 beta 版本反馈（#125626）、数据库无限增长（#114612）和子代理投递可靠性（#67777）等核心稳定性议题。今日无新版本发布。

---

## 版本发布

今日无新版本发布（当前 beta: `v2026.8.1-beta.3`）。

---

## 项目进展

今日合并/关闭了 244 个 PR，其中值得关注的重要合并/关闭包括：

### 已关闭/合并
- **[#129626] refactor(state): retire six dead shared-state tables at schema v10** — `steipete` 移除了共享状态数据库（`state/openclaw.sqlite`）中 6 个生产代码完全不读写的死表（`agent_model_catalogs`、`android_notification_recent_packages`、`command_log_entries`、`diagnostic...`），schema 升级至 v10，简化了数据库结构。
- **[#129638] fix: keep session catalog mirroring within isolated profiles** — 修复了使用命名/迁移状态 profile 时，内部后台消费者仍可能选中进程用户 HOME 会话目录条目的问题。
- **[#120176] refactor(ios): share voice permission support** — 合并了 iOS 端语音权限支持的共享实现。
- **[#125471] fix(models): keep Claude CLI OAuth available in Control UI** — 修复了 Gateway 重启后 Claude CLI OAuth 因遗留 `auth.profiles["anthropic:claude-cli"]` 条目导致刷新所有权丢失的问题。
- **[#129371] fix: agent-created automations appear under the session creator** — 修复了通过 agent automations 工具创建的自动化，后续运行被错误记录为系统或 agent 活动的问题。
- **[#128371] fix(release): authorize focused beta evidence** — 解决了 beta.3 发布阻塞：官方发布者只接受全量 Release Validation 清单通过，但冻结候选仅修改了已复核的 Slack 测试，失败的遗留项已重跑成功。

### 待合并（有潜力）
- **[#129636] fix(exec): scope reusable approvals to their working directory** — 修复可复用执行审批可在不同工作目录被复用的问题（安全边界修复，P1）
- **[#129386] fix: preserve unread reminder for open sessions** — 修复标记为未读的提醒在当前会话中立即消失的问题（P1）
- **[#129670] feat(secrets): agent-requested credentials the model never sees** — 允许用户向 agent 提供 API 密钥而不进入会话/模型上下文（P1，安全增强）
- **[#129633] fix(webhooks): keep TaskFlow child actions within the owning session** — 修复 webhook TaskFlow 可将托管任务投影附加到无关的 ACP/子代理运行的问题

整体来看，项目在数据库清理、OAuth 可靠性、安全审批边界等领域持续推进，但大量修复仍停留在待合并状态（256 个），合并积压值得关注。

---

## 社区热点

### 讨论最活跃的 Issues

1. **[#125626] OpenClaw 2026.8.1 beta feedback**（18 评论）— beta 版本集中反馈帖，测试目标为最新 beta.3，社区正密集验证。
   https://github.com/openclaw/openclaw/issues/125626

2. **[#80319] QA tool-defaults suite conflates Codex-native tools with OpenClaw dynamic tool parity**（17 评论）— 关于 QA 测试框架将 Codex 原生工具与 OpenClaw 动态工具混为一谈的架构讨论，已确认是 QA harness/mock-provider 问题而非广泛的 Codex 运行时工具丢失。
   https://github.com/openclaw/openclaw/issues/80319

3. **[#79902] [Feature]: Add companion-friendly SQLite transcript/session seams on top of database-first runtime**（14 评论，👍 2）— 社区对数据库优先运行时之上添加 SQLite 会话/转录接口的强烈需求，便于高级用户构建基于规范运行时状态的集成。
   https://github.com/openclaw/openclaw/issues/79902

4. **[#67777] [Bug]: Subagent completion delivery can be lost on direct-announce timeout, drain, or orphan prune**（13 评论，P1）— 子代理完成投递在忙碌通道/超时/重启条件下可能丢失的严重可靠性问题，社区持续跟进。
   https://github.com/openclaw/openclaw/issues/67777

5. **[#114612] [memory-core] SQLite unbounded growth: memory_index_chunks + memory_embedding_cache tables have no retention policy**（9 评论，P2）— 生产实例中 `memory_index_chunks` 和 `memory_embedding_cache` 表无限增长将填满磁盘，社区提供了字段证据。
   https://github.com/openclaw/openclaw/issues/114612

### 分析
社区焦点集中在三大方向：**（1）数据持久层可靠性**（SQLite 增长/损坏、会话状态一致性），**（2）消息/子代理投递可靠性**，**（3）可扩展性/可观测性**（SQLite 接口、模型成本暴露）。beta 版本反馈帖的高互动表明用户正积极验证 v2026.8.1，但同时也意味着 beta 质量的把关压力较大。

---

## Bug 与稳定性

### P0 — 严重
- **[#126821] SQLite corruption recurs on pristine rebuilt DBs within 15–24h**（8 评论，`clawsweeper-recovery-stuck`）— 2026.8.1-beta.2 WSL2 环境，纯净重建的数据库在 15-24 小时内复发 freelist miscount，5 天内 5 次事件，包括"瘫痪网关"模式（拒绝所有服务但从不退出）。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/126821

### P1 — 高
- **[#127710] prepared-model-runtime fails closed on transient generation churn**（5 评论）— 生产环境 25-agent 网关两天内出现两种消息丢失模式：一次指纹漂移永久卡死网关 + owner-commit 竞争静默丢消息。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/127710
- **[#127948] WhatsApp group replies render as BLANK bubbles when quote cache expires**（5 评论）— 回复延迟超过 CACHE_TTL_MS (10分钟) 时，发送的消息携带有效引用键但空引用正文，渲染为完全空白的气泡。**有 linked PR。**
  https://github.com/openclaw/openclaw/issues/127948
- **[#97616] OpenClaw leaks unreaped hook/tool child processes**（9 评论，P1）— hook/tool 执行泄漏未回收子进程导致僵尸进程累积和运行时劣化，被标记回归。**无 fix PR。** 注意 [PR #98539] 正在修复进程树清理问题。
  https://github.com/openclaw/openclaw/issues/97616
- **[#67777] Subagent completion delivery can be lost on direct-announce timeout/drain/orphan prune**（13 评论）— 子代理完成投递在多种条件下丢失。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/67777
- **[#126246] Telegram durable outbound deliveries stuck in send_attempt_started**（5 评论）— agent 运行成功但 Telegram 回复滞留在 `send_attempt_started`，重启后丢失。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/126246
- **[#126631] Sandbox skills bind-mount creates root-owned /workspace/.openclaw**（5 评论）— 导致沙箱用户 uid 1000 无法写入。**有 linked PR。**
  https://github.com/openclaw/openclaw/issues/126631
- **[#126900] maxActiveTranscriptBytes loops compaction forever**（5 评论）— 压缩后转录仍超阈值则永远循环压缩，阻塞会话通道。**有 linked PR。**
  https://github.com/openclaw/openclaw/issues/126900
- **[#125570] Skill Workshop update overwrites live skill's description**（5 评论）— 应用更新提案时覆盖实时技能的 description 字段，静默破坏技能路由。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/125570

### P2 — 中
- **[#114612] SQLite unbounded growth: memory_index_chunks + memory_embedding_cache**（9 评论）— 无保留策略的数据库增长将填满磁盘。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/114612
- **[#48709] Gemini 2.5 Pro: textSignature bloat + think tags + mixed text/tool failures**（6 评论）— 三问题叠加导致会话上下文膨胀、运行中止和静默投递失败。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/48709
- **[#92633] memory_search corpus=all times out while individual corpora succeed**（9 评论）— 全语料搜索持续 15s 超时，而单独搜索各语料均成功。**无 fix PR。**
  https://github.com/openclaw/openclaw/issues/92633

### 回归标记
- #126821, #97616, #119401 被标记为回归（此前正常工作）。

---

## 功能请求与路线图信号

### 可能被纳入下一版本（已有 linked PR）
- **Agent-requested credentials the model never sees**（[PR #129670]）— 允许用户向 agent 传递 API 密钥而不进入会话/模型上下文，安全增强，可能进入 2026.8.2。
- **Claude CLI OAuth 保留修复**（[PR #125471] 已合并）— 已解决 OAuth 刷新所有权问题。

### 高呼声需求（无 PR，等待决策）
- **[#67413] Per-agent dreaming configuration**（9 评论，👍 5）— 逐个 agent 配置记忆 dreaming 的需求，当前所有 workspace 同时 dreaming 导致内存峰值和 OOM 风险。
  https://github.com/openclaw/openclaw/issues/67413
- **[#79902] SQLite transcript/session seams**（14 评论，👍 2）— 在数据库优先运行时之上提供 SQLite 会话/转录接口。
  https://github.com/openclaw/openclaw/issues/79902
- **[#45758] Support YAML as config file format**（9 评论，👍 2）— 长期需求，YAML 在 DevOps 工具链中更可读。
  https://github.com/openclaw/openclaw/issues/45758
- **[#16670] Onboarding Wizard 应包含 Memory/Embedding 设置**（9 评论）— 新用户常因未配置 embedding provider 而无法使用 `memory_search`，开箱即用体验的关键改进。
  https://github.com/openclaw/openclaw/issues/16670
- **[#26037] Ali Bailian coding plan support (thinking/reasoning enabled)**（6 评论，👍 4）— 阿里云百炼 Codex 计划支持深度思考模式。
  https://github.com/openclaw/openclaw/issues/26037
- **[#9016] Expose OpenRouter usage cost to agent runtime**（8 评论）— 按消息暴露 OpenRouter 成本，便于 agent 附加到回复中。
  https://github.com/openclaw/openclaw/issues/9016
- **[#39343] Image batching/media group buffering at gateway layer**（5 评论）— Telegram/Line 相册多图场景需要网关层批量缓冲，避免 agent 逐张回复轰炸。
  https://github.com/openclaw/openclaw/issues/39343

### 可访问性改进
- **[#9637] Add accessibility config option to disable emojis and unicode symbols in TUI**（6 评论）— 屏幕阅读器用户需要禁用 emoji/unicode 符号的选项。
  https://github.com/openclaw/openclaw/issues/9637
- **[#95601] Request for VoiceOver-friendly chat history**（5 评论，👍 2）— macOS VoiceOver 用户请求聊天历史可访问性改进，用户特别感谢 v2026.6.9 中剩余用量显示靠近模型选择器的改进。
  https://github.com/openclaw/openclaw/issues/95601

---

## 用户反馈摘要

### 真实痛点
1. **数据库增长焦虑**：用户 `ralf003` 提供了生产实例字段证据（2026.7.2-b...），`memory_index_chunks` 和 `memory_embedding_cache` 表每轮记忆提取循环都增长，不受会话维护修剪覆盖，最终将填满磁盘。（#114612）

2. **Beta 版本可靠性担忧**：用户 `liemnhoang` 在 #126821 中详细描述了 5 天内 5 次 SQLite 损坏事件，包括"瘫痪网关"模式——拒绝所有服务但从不退出，且发生在纯净重建、完整 PRAGMA integrity_check 通过的数据库上。

3. **子代理工作丢失**：用户在 #6625 中反馈子代理达到 `runTimeoutSeconds` 时被立即杀死，所有未保存工作丢失——"代码、研究、分析、生成的内容，任何东西"。请求超时前 N 秒注入系统消息预警。

4. **记忆功能入口不透明**：用户在 #16670 中指出 onboarding wizard 完全不提 embedding provider 配置，没有配置 `memorySearch` 时 `memory_search` 无法工作，新用户开箱即用的核心功能受阻。

5. **多用户生产扩展受阻**：用户 `richwilson-bloom`（#96477）在 Slack/Telegram 多用户生产负载下遭遇单写者会话文件锁瓶颈，请求放宽会话写锁。

6. **Dreaming 内存峰值**：多个用户报告所有工作区同时 dreaming 导致 6GB MemoryMax 被超过并触发 OOM 杀死（#67413），且无法单独禁用某 agent 的 dreaming。

7. **静默失败模式**：多个 bug 报告描述了"静默失败"模式——回复不送达（#127948 空白气泡、#126246 send_attempt_started 卡死、#127710 指纹漂移）、QA 自检误报通过（PR #129661）、文件复制无反馈（PR #129617）。这类问题严重削弱用户对系统的信任。

### 满意点
- 用户 `xiaopinpin-music` 感谢 v2026.6.9 将剩余用量信息移至模型选择器附近的改进，认为这对 VoiceOver 用户很有意义（#95601）。
- 用户 `100yenadmin` 在 #80319 中认可团队对 QA 问题的架构分析并进行了澄清。

---

## 待处理积压

### 长期未响应/卡住的重要 Issue（标记 `clawsweeper-recovery-stuck` 或长期无更新）

1. **[#126821] SQLite corruption recurs on pristine rebuilt DBs（P0）** — 创建于 2026-08-20，最新更新 2026-08-25，仍无 fix PR。数据库损坏是最严重的稳定性问题，建议优先处理。
   https://github.com/openclaw/openclaw/issues/126821

2. **[#97616] Zombie process accumulation（P1）** — 创建于 2026-06-29，近两个月仍无 fix PR。进程泄漏导致运行时劣化，影响长期运行的网关稳定性。
   https://github.com/openclaw/openclaw/issues/97616

3. **[#67777] Subagent completion delivery loss（P1）** — 创建于 2026-04-16，已 4 个月无修复进展。
   https://github.com/openclaw/openclaw/issues/67777

4. **[#48709] Gemini 2.5 Pro textSignature bloat（P2）** — 创建于 2026-03-17，5 个月无 fix PR。Gemini 用户的会话可靠性持续受影响。
   https://github.com/openclaw/openclaw/issues/48709

5. **[#80178] resolveCliAuthEpoch invalidates every live CLI session** — 创建于 2026-05-10，`fix-shape-clear` 状态但无明确修复方案。
   https://github.com/openclaw/openclaw/issues/80178

6. **[#71335] sync.watch should default to false in gateway mode** — 创建于 2026-04-25，`fix-shape-clear`，网关模式泄漏 1,292 个 chokidar 文件描述符。
   https://github.com/openclaw/openclaw/issues/71335

7. **大量 `clawsweeper:needs-maintainer-review` + `needs-product-decision` 标记的 Issue**（如 #79902、#67413、#51441、#77298 等）— 这些 Issue 已积累数周至数月，等待维护者产品决策，建议安排批量 triage 会议清理。

### 待合并 PR 积压
- 当前有 256 个 PR 待合并，其中多个关键修复（#129636 安全审批、#129386 未读提醒、#129670 密钥安全传递）等待维护者 review。合并积压可能导致修复延迟进入正式版本。

---

*本日报由 AI 分析师基于 GitHub 数据自动生成。所有数据截至 2026-08-26。*

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期：2026-08-26**
**数据窗口：2026-08-25 ~ 2026-08-26（24小时）**


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从“功能堆叠”向“架构治理+安全加固”转型**的关键阶段。头部项目（OpenClaw、ZeroClaw、CoPaw）日 PR/Issue 动态均超 50 条，高频迭代已成为标配，但社区讨论重心正从“增加功能”转向“如何在不破坏稳定性的前提下安全地扩展”——SQLite 损坏、子代理消息丢失、工具隔离越权、配置热更新等**可靠性/安全性议题**占据了 P0/P1 级问题的主导位置。同时，一个显著的新兴信号是：**“家庭边缘计算网格”（利用闲置设备组建分布式 Agent 网络）在同一天内被至少 4 个项目（PicoClaw #3345、NanoClaw #3538、NullClaw #994、ZeroClaw #10360）的独立用户提出**，表明多设备协同正成为社区自下而上的共同想象。整体而言，生态正处于“夯实基础、探索边界”的并行阶段。


## 2. 各项目活跃度对比

| 项目 | Issues（新开/活跃） | PR（待合并） | PR（合并/关闭） | Release | 健康度评级 | 阶段判断 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 437 | 256 | 244 | 无 | ★★★★☆ | 高强度迭代，合并积压严重 |
| **ZeroClaw** | 38 | 49 | 1 | 无 | ★★★★☆ | 安全加固密集，PR 合流瓶颈 |
| **CoPaw** | 19 | 21 | 29 | v2.1.1-beta.3 | ★★★★☆ | 快速迭代，Bug 闭环及时 |
| **NanoClaw** | 5 | 待统计（大量 core-team PR） | 16 | 无 | ★★★★☆ | 安全漏洞集中暴露期 |
| **IronClaw** | 35 | 13 | 11 | 无 | ★★★★☆ | CI 基建与功能推进并重 |
| **LobsterAI** | 1 | 少量 | 9 | 2026.8.25 + 2026.8.21 | ★★★★☆ | 功能密集迭代，社区反馈少 |
| **NanoBot** | 5 | 10 | 14 | 无 | ★★★★★ | 高频迭代、P1 快速响应 |
| **Hermes Agent** | ~50（含 PR） | ~14 | 14 | 无 | ★★★☆☆ | 跨平台问题积压，修复跟进中 |
| **Moltis** | 2 | 4 | 1 | 无 | ★★★☆☆ | 谨慎推进，沙箱后端扩展期 |
| **PicoClaw** | 4 | 1 | 0 | 无 | ★★★☆☆ | 低活跃，Bug 收敛期 |
| **NullClaw** | 1 | 0 | 0 | 无 | ★★☆☆☆ | 观察窗口期，等待响应 |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 0 | 无 | — | 24h 无活动 |


## 3. OpenClaw 在生态中的定位

**社区规模与迭代强度：** OpenClaw 以日 500 条 Issue + 500 条 PR 的动态量级，在生态中处于**绝对头部位置**，活跃度约为第二梯队（ZeroClaw/CoPaw/IronClaw）的 10 倍以上。其 256 条待合并 PR 的积压量也从侧面反映了社区贡献规模已超出维护者带宽。

**技术路线差异：**
- **与 ZeroClaw 相比**：ZeroClaw 采用 Rust/WASM-first 架构，强调“security-first”和安全边界治理（RFC 驱动）；OpenClaw 以 Node.js/TypeScript 为主，更侧重**功能广度与集成深度**（Claude CLI OAuth、WhatsApp 渲染、Telegram 持久投递等），在渠道适配和端到端可靠性上面临更大复杂度。
- **与 CoPaw 相比**：CoPaw 更偏重“开箱即用的桌面应用”路线（Tauri 封装、Windows 分发）；OpenClaw 则定位为**可编程的网关/运行时骨架**，受众更偏向开发者和高级自托管用户。
- **与 Hermes Agent 相比**：Hermes 聚焦桌面端本地优先体验（macOS/Windows 原生应用）；OpenClaw 为云端网关模式优化更深。

**优势：** 渠道适配广度（Slack/Telegram/WhatsApp/iOS 等）、社区规模、Schema 演进（数据库 v10）带来的扩展性。**劣势：** 合并积压导致修复延迟进入正式版；SQLite 层反复出现损坏（P0 #126821）对信任度有侵蚀。


## 4. 共同关注的技术方向

| # | 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|---|
| 1 | **数据持久层可靠性** | OpenClaw（#126821/#114612）、CoPaw（#7288）、Hermes（#94428） | SQLite 损坏/无限增长/上下文溢出，需保留策略与崩溃恢复 |
| 2 | **消息/子代理投递可靠性** | OpenClaw（#67777/#127710）、NanoBot（#5529）、IronClaw（#3311） | 超时/重启条件下消息不丢失、子代理完成通知不静默吞掉 |
| 3 | **工具执行安全边界** | ZeroClaw（#9947/#10369）、NanoClaw（#3543/#3532）、OpenClaw（#129636） | 命令注入防护、代理间隔离（cron/工具作用域）、网络出口管控 |
| 4 | **沙箱/隔离后端多元化** | Moltis（#1118/#1199）、ZeroClaw（#8132）、NullClaw（#994） | K8s/Coder/WASM/远程后端，支持不可信代码与多设备协同 |
| 5 | **配置热更新（免重启）** | ZeroClaw（#10297）、CoPaw（#7218…） | 配置变更即时生效，不影响运行中会话 |
| 6 | **本地/边缘 LLM 兼容性** | Hermes（#87697）、ZeroClaw（#8999）、OpenClaw（#48709） | Ollama/本地模型流式中断、上下文格式干扰、token 膨胀 |
| 7 | **家庭边缘计算网格** | PicoClaw（#3345）、NanoClaw（#3538）、NullClaw（#994）、ZeroClaw（#10360） | 闲置设备组成 worker 网络，signed receipts 实现可信协作 |
| 8 | **成本可观测性** | OpenClaw（#9016）、IronClaw（#7891） | 单次回复/请求级模型成本暴露，优化 token 载荷 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 全渠道网关 + 运行时 | 开发者/自托管/多通道重度用户 | Node.js/TS；数据库优先（SQLite）；Schema v10；多 profile 隔离 |
| **ZeroClaw** | 安全优先的 Agent 运行时 | 安全敏感型企业/多代理部署 | Rust 核心；WASM 方向；RFC 驱动治理；执行树迭代预算 |
| **CoPaw (QwenPaw)** | 桌面端开箱即用 | 普通用户/非技术用户 | Tauri 桌面壳 + Web Console；Qwen 模型深度集成；微信/Telegram 开箱 |
| **NanoBot** | 轻量、多渠道、可嵌入 | 个人开发者/小型团队 | 模块化设计；MCP 生态拥抱；TUI/WebUI 双界面 |
| **Hermes Agent** | 本地优先桌面 Agent | macOS/Windows 个人用户 | 原生应用（Electron-like）；FDA/Keychain 权限管理；本地模型优先 |
| **NanoClaw** | 技能驱动的 Agent 扩展 | 开发者/深度定制用户 | 技能（Skill）系统为核心；Shell 注入安全隐患；core-team 高强度重构 |
| **IronClaw** | 企业级协作/通知中心 | 团队/多用户部署 | 扩展能力载荷 + 持久化沙箱；通知中心重构；CI 基建投资 |
| **LobsterAI** | 知识管理 + 产物管理 | 内容创作者/知识工作者 | 网易云音乐出品；资料库（Library）为核心；商业化数据基建 |
| **Moltis** | 工具链兼容性 + 远程沙箱 | 开发者/DevOps | 多工具兼容（Brave/OpenAI schema/Fastmail OAuth）；沙箱后端插件化 |
| **PicoClaw / NullClaw / TinyClaw / ZeptoClaw** | 超轻量/边缘部署 | 资源受限设备/极客 | 低内存占用（MB 级）；Docker/WASM 适配器；家庭网络部署为目标 |


## 6. 社区热度与成熟度分层

### 第一层：快速迭代期（日 PR 合并 > 10，高频发布）
- **OpenClaw**、**CoPaw**、**NanoClaw**、**NanoBot**、**LobsterAI**
- 特征：功能推进快、Bug 闭环快、社区活跃度高

### 第二层：质量巩固期（日 PR 合并 5~15，以修复/基建为主）
- **ZeroClaw**、**IronClaw**、**Hermes Agent**
- 特征：新增功能放缓，重点攻克安全边界、跨平台兼容性、CI 质量

### 第三层：谨慎推进期（日 PR 合并 < 5，以评估/探索为主）
- **Moltis**、**PicoClaw**
- 特征：评估外部 PR、方向探索、逐步收编贡献

### 第四层：观察窗口期（24h 几乎无代码产出）
- **NullClaw**、**TinyClaw**、**ZeptoClaw**
- 特征：等待核心维护者响应关键 Issue，社区投入度待观察


## 7. 值得关注的趋势信号

**1. “安全边界”从附加品变为第一公民。** ZeroClaw 的 S0/S1 安全追踪体系、NanoClaw 的 shell 注入漏洞（#3543）、OpenClaw 的审批作用域修复（#129636）——三大项目在同一天内均出现安全边界缺口报告或修复，表明 **Agent 工具执行的安全模型尚未成熟**，是整个行业需要投入的方向。

**2. 家庭边缘计算网格成为“分布式 Agent”的民间共识。** 同日 4 个独立项目的用户提出相似提案（利用闲置设备组建计算网格），说明社区对 **Agent 算力分布式化** 有未被满足的自下而上需求。对开发者而言，这是潜在的差异化机会——尤其结合 WASM 与签名收据机制。

**3. 本地/小型 LLM 兼容性成为隐藏的“大众需求”。** Hermes（Ollama 流取消）、ZeroClaw（本地小模型被流式数据混淆）、OpenClaw（Gemini textSignature 膨胀）——**不同架构的项目都在为本地模型集成付出成本**。随着用户对数据隐私与成本敏感度的提升，深度优化本地推理路径将成为竞争分水岭。

**4. “静默失败”比“显式报错”更伤用户信任。** 用户在多个项目中报告了无错误提示的消息丢失（OpenClaw #127948、Hermes #90428、NanoBot #5516）。**可观测性（可操作的错误信息、成本暴露、运行状态可见）已成为用户满意度核心要素**，而非附加体验。

**5. 更新机制本身的“破坏性”正在制造用户流失风险。** Hermes（macOS 权限重置、Windows 更新死锁）、CoPaw（Windows 文件锁）、NanoClaw（更新误伤本地自定义代码）——**“平滑、非破坏性更新”成为桌面端 Agent 的隐形技术债**。能率先系统性解决此问题的项目将获得显著用户黏性优势。

---

*本报告由 AI 技术分析师基于 2026-08-26 各项目 GitHub 公开数据自动生成，数据源包括 OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、NullClaw、IronClaw、LobsterAI、TinyClaw、Moltis、CoPaw、ZeptoClaw、ZeroClaw 等 13 个项目。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期：2026-08-26**  
**数据窗口：2026-08-25 至 2026-08-26**  
**数据来源：github.com/HKUDS/nanobot**


## 1. 今日速览

NanoBot 项目今日活跃度**高**。过去 24 小时内有 5 条 Issue 更新（全部活跃），24 条 PR 更新（其中 14 条已合并/关闭，10 条待合并），无新版本发布。项目正处于**高频迭代期**，尤其是 Telegram 通道（2 个相关 PR）、TUI/WebUI 交互优化（3 个相关 PR）和工具执行安全性/性能（2 个相关 PR）三大方向。值得注意的是，社区贡献者占比高（dangzitou、Re-bin、KDB-Wind、nolanchic、zpljd258 等外部开发者），项目生态健康度良好。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日合并/关闭了 **14 个 PR**，核心亮点如下：

| 方向 | PR | 说明 |
|------|-----|------|
| **Telegram 消息归属** | [#5541](https://github.com/HKUDS/nanobot/pull/5541) | 群组消息现在会带发送者显示名（回退链：first name → username → 数字 ID），修复 #1091 |
| **Codex 提示缓存稳定性** | [#5540](https://github.com/HKUDS/nanobot/pull/5540) | 在 fallback 和图片重试路径中传播稳定的 session 身份，`prompt_cache_key` 仅由该身份派生，无身份则不发送该字段 |
| **find_files 扫描性能** | [#5533](https://github.com/HKUDS/nanobot/pull/5533) | 完整扫描移入 worker，用预算化的 `os.scandir` 替代重复的 pathlib 元数据调用，分页前瞻后停止路径排序扫描，支持取消传播 |
| **后台子代理等待语义** | [#5529](https://github.com/HKUDS/nanobot/pull/5529) | 普通 pending-message 保持非阻塞，仅在正常 no-tool 响应就绪时通过独立 rendezvous 等待后台子代理，统一 300 秒超时 |
| **需求驱动文档检索** | [#5525](https://github.com/HKUDS/nanobot/pull/5525) | `grep` 默认变为按需内容检索工具，返回带 5 行上下文的有界匹配片段，PDF/DOCX/XLSX/PPTX 增量扫描并提供稳定定位符 |
| **WebUI 拖拽会话整理** | [#5389](https://github.com/HKUDS/nanobot/pull/5389) | 支持独立会话和侧边栏分组间的拖拽排序，拖一个会话到另一个上可创建分组（带 conflict 标记） |
| **exec_session 非轮询等待** | [#5526](https://github.com/HKUDS/nanobot/pull/5526) | 工具更名为 `exec_session`（7 字段 schema），新增 `until_exit` + `timeout_ms`，agent 等待完成不再需要轮询 |
| **TUI/样式微调** | [#5534](https://github.com/HKUDS/nanobot/pull/5534) / [#5530](https://github.com/HKUDS/nanobot/pull/5530) / [#5538](https://github.com/HKUDS/nanobot/pull/5538) | 技能引用自动补全（`$skill-name`）、短转录保持顶部对齐、组合器占位符改为 `Enter send now · Tab send next` |

**小结**：项目今日在**性能、安全与交互体验**三条线上同时推进。尤其是 `find_files` 性能修复（p1）和 exec_session 非轮询机制，直接回应了长任务场景的稳定性问题。TUI 技能补全、拖拽分组等交互优化表明项目在打磨日常使用体验。


## 4. 社区热点

### 最受关注 Issue

**[#5505 — [enhancement] Add AnySearch as a web search provider](https://github.com/HKUDS/nanobot/issues/5505)**
- 评论：3 | 👍：0 | 活跃讨论中
- **背景**：AnySearch 团队主动提交集成请求，计划通过 PR 将 AnySearch 接入 nanobot 的 `web_search` 工具。
- **分析**：这是典型的**上游服务方主动集成**信号。搜索提供方的竞争正在加剧——同方向已有已合并的 mst-python PR（[#5234](https://github.com/HKUDS/nanobot/pull/5234)），AnySearch 提供 API/MCP/Skill 三种集成方式（支持匿名配额、key 可选）。如果 nanobot 计划在 web_search 领域建立一个 provider 生态，这类 PR 应优先 review。

### 讨论持续发酵

**[#5532 — [bug] missing import of "mask_session_key" in autocompact.py](https://github.com/HKUDS/nanobot/issues/5532)**
- 评论：1 | 真实报错场景（含日志）

**[#5516 — Telegram: rich messages never render when streaming is enabled](https://github.com/HKUDS/nanobot/issues/5516)**
- 评论：1 | 已有对应修复 PR（[#5531](https://github.com/HKUDS/nanobot/pull/5531)）


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| **P1** | [#5533](https://github.com/HKUDS/nanobot/pull/5533) | find_files 全量扫描导致响应延迟/卡顿 | ✅ 已合并 |
| **P1** | [#5536](https://github.com/HKUDS/nanobot/pull/5536) | restricted shell 在无 sandbox 时无法 fail-closed（symlink/命令替换绕过路径检查），修复 #4072 | 🟡 待合并 |
| **P2** | [#5532](https://github.com/HKUDS/nanobot/issues/5532) | `autocompact.py` 缺少 `mask_session_key` 导入，触发用户查询时报错 | 🟡 有 1 条评论，无 fix PR |
| **P2** | [#5516](https://github.com/HKUDS/nanobot/issues/5516) | Telegram streaming + rich_messages 互斥，rich 消息永远不渲染 | 🟡 修复 PR [#5531](https://github.com/HKUDS/nanobot/pull/5531) 待合并 |
| **P2** | [#5527](https://github.com/HKUDS/nanobot/issues/5527) | `unifiedSession` 下 WebUI 侧边栏标题始终 "Untitled"（标题生成在共享 session，渲染在 per-chat session） | 🟡 修复 PR [#5528](https://github.com/HKUDS/nanobot/pull/5528) 待合并 |
| **P2** | [#5539](https://github.com/HKUDS/nanobot/pull/5539) | ToolLoader 日志仍用 printf-style `%s`，需改为 Loguru-compatible `{}` | 🟡 待合并 |

**趋势判断**：今日 Bug 集中在两个系统性问题：(1) 长任务执行路径（find_files 扫描、后台子代理等待）的卡顿与超时；(2) 会话抽象层（unifiedSession）引入的状态错位。前者已有合入修复，后者尚未完全闭环。


## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 对应 PR/状态 | 纳入下一版本可能性 |
|----------|------|-------------|-------------------|
| **AnySearch 搜索 Provider** | Issue [#5505](https://github.com/HKUDS/nanobot/issues/5505) | 待提交 PR | ⭐⭐⭐（团队主动+多集成方式） |
| **WebUI 会话结束通知铃声** | Issue [#5524](https://github.com/HKUDS/nanobot/issues/5524) | 无 PR | ⭐（优先级偏低，属体验优化） |
| **Session focus 持久化** | PR [#5537](https://github.com/HKUDS/nanobot/pull/5537) | 待合并，修复 #3292 | ⭐⭐⭐（已有完整实现 + 修复闭环） |
| **MCP 就绪重试** | PR [#5535](https://github.com/HKUDS/nanobot/pull/5535) | 待合并（关联 NAN-43） | ⭐⭐⭐（直接提升多轮稳定性） |
| **mst-python 元搜索** | PR [#5234](https://github.com/HKUDS/nanobot/pull/5234) | 待合并（conflict，已挂 23 天） | ⭐⭐⭐（功能完整但需解决冲突） |

**值得注意**：以 `Linear issue: NAN-XX` 作为 PR 描述的贡献者（chengyongru）出现频率明显升高，可能与核心维护者有直接或间接联系，这类 PR 被合并的概率较大。


## 7. 用户反馈摘要

从今日 Issues/PR 中提炼的真实用户声音：

- **长任务等待是核心痛点**（Issue [#5524](https://github.com/HKUDS/nanobot/issues/5524)）：用户在等待 agent 执行工具调用、文件编辑、shell 命令时"只能盯着屏幕"，页面没有完成提示，期望有通知铃声。说明 nanobot 已实际承载长耗时任务场景。
- **搜索 Provider 社区生态在形成**（Issue [#5505](https://github.com/HKUDS/nanobot/issues/5505)）：AnySearch 团队以"API/MCP/Skill 三种集成方式"主动接入，侧面反映 nanobot 在 agent 工具链中的地位正在提升。
- **Telegram 场景存在真实使用摩擦**（Issue [#5516](https://github.com/HKUDS/nanobot/issues/5516) + PR [#5541](https://github.com/HKUDS/nanobot/pull/5541)）：群组消息归属和 rich 消息渲染问题说明 Telegram channel 有实际用户在使用，且对消息格式有较高要求。
- **unifiedSession 的语义混乱**（Issue [#5527](https://github.com/HKUDS/nanobot/issues/5527)）：用户报告标题丢失问题，根因是共享 session 和 per-chat session 的职责划分不清晰——建议维护者在文档中明确 unifiedSession 模式下 session 的生命周期模型。


## 8. 待处理积压

⚠️ **长时间未响应的重要项**（按滞留时长排列）：

| 时间 | 项目 | 类型 | 说明 |
|------|------|------|------|
| **24 天** | PR [#5234](https://github.com/HKUDS/nanobot/pull/5234) — mst-python 元搜索 provider | 增强/新 provider | P1 级 feature，已标记 conflict，功能完整（RRF 融合多引擎结果），长时间未处理可能打击贡献者积极性 |
| **29 天** | PR [#5152](https://github.com/HKUDS/nanobot/pull/5152) — 子代理部分完成结果标记 | 回归修复 | 已标记 conflict，`subagent_remaining_count` 元数据设计需维护者决策 |
| **23 天** | PR [#5389](https://github.com/HKUDS/nanobot/pull/5389) — WebUI 拖拽分组 | 功能 | 已合并 ✅（此前积压已解除） |

**建议**：优先处理 [#5234](https://github.com/HKUDS/nanobot/pull/5234) 的 conflict 问题，若 mst-python 与即将接入的 AnySearch 存在功能重叠，需尽快明确 web_search provider 的长期架构方向（多 provider 共存？优先级排序？）。


*报告生成时间：2026-08-26 | 数据窗口：过去 24 小时 | 项目整体健康度：🟢 优秀（高频迭代、社区活跃、P1 问题快速响应）*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，我为您呈现这份基于 2026-08-26 数据的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-08-26

## 1. 今日速览

Hermes Agent 项目今日活跃度极高，过去24小时内共有 100 条 Issues 和 PRs 更新，显示出旺盛的社区参与度和开发迭代节奏。值得关注的是，更新内容高度集中在 **macOS/Windows 桌面端更新与权限问题、多网关/会话状态管理、以及本地 LLM (Ollama) 集成稳定性** 三大核心痛点。虽然今日没有新版本发布，但有一批针对已知顽疾（如 macOS 权限重置、Windows 更新挂起）的 “salvage” PR 被提交，表明维护团队正积极清理历史技术债。整体项目健康度良好，尽管存在一些高危 Bug（如 P1 的 Windows MCP 调用失败），但社区响应和修复 PR 的跟进速度较快。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

尽管没有新 Release，但今日有 14 个 PR 被合并或关闭，标志着多项关键修复和功能推进。特别值得关注的是由 `teknium1` 提交的一批 “salvage” PR，它们将此前被关闭但仍有价值的 PR（如 #85416, #78037, #79871 等）的补丁重新应用到最新的 main 分支上，有效地避免了工作的丢失并解决了遗留问题。

**关键合并/关闭 PR 分析：**

- **[#95130] fix(relay): drain active turns before popping session scope on shutdown**：这是一个重要的稳定性修复，解决了网关在关闭时因作用域（scope）未按 LIFO 顺序弹出而导致的崩溃问题 (DAN-3063)。
- **[#95127] fix(desktop): stop packaged preview opens from succeeding invisibly**：修复了桌面端预览功能“假成功”的问题，现在打开预览操作需要渲染进程确认，避免了后续调用超时。
- **“Salvage” 系列 PR（#95131, #95069, #95129）**：这些 PR 分别修复了 **macOS 终端权限在每次 Python 补丁更新后重置**、**Windows 应用内更新器死锁** 以及 **Windows 更新时 cua-driver 无限期挂起** 的问题。这些修复直接回应了社区中长期存在的痛点，显著提升了桌面端的更新体验和系统稳定性。

这些合并表明项目不仅关注新功能开发，也在着力巩固现有功能的稳定性和用户体验，特别是针对桌面端和跨平台兼容性的“顽疾”进行系统性修复。

## 4. 社区热点

今日讨论热度最高的议题清晰地指向了 **更新机制对用户环境的“破坏性”**。

- **[#66616] Skills index is stale or degraded** (评论: 97)：虽然这是一个自动化探针报告的问题，但其极高的评论数表明开发者对技能索引（Skills Index）的可靠性非常关注。这直接关系到 Agent 的功能可用性，任何索引过期或降级都可能被社区视为严重的服务质量事件。
- **[#52010] macOS Full Disk Access (FDA) revoked after every update** (评论: 21)：这是社区痛点最集中的体现。用户 `dizhaky` 详细描述了每次更新桌面应用后，macOS 的全盘访问权限都会被撤销，需要手动重新授权，严重影响了自动化流程和用户体验。该问题被标记为 P2，且有相关 PR (#95131) 进行了修复尝试。
- **[#87697] Hermes Client cancels local LLM streams after ~1.5s** (评论: 11)：这个问题非常关键，因为它直接关系到核心 Agent 功能与本地模型（Ollama）的兼容性。用户 `jayambede` 指出，最近的更新导致客户端在推理阶段就取消了流式连接，使得本地模型完全不可用，这很可能引发了本地优先（local-first）用户的强烈不满。

**背后诉求分析**：这些热点背后是用户对 **“无缝、非破坏性”更新** 的强烈渴望。无论是权限、配置还是与外部服务的连接，都不应因软件更新而被重置或破坏。同时，核心引擎与主流本地推理服务（如 Ollama）的兼容性测试需要被高度重视。

## 5. Bug 与稳定性

今日提交的 Bug 中，桌面端更新和会话管理问题占据了主导，并按严重程度排列如下：

**高严重级别 (P1)：**
- **[#94906] Windows: native stdio MCP client ... every call fails**：**平台/功能完全不可用**。在 Windows 上，所有 stdio 类型的 MCP 工具调用全部超时失败。这是影响面极大的问题，目前没有直接的修复 PR 链接。

**中高严重级别 (P2)，且有修复 PR：**
- **[#52010] macOS FDA revoked after every update**：经典顽疾，影响安全和自动化。已有修复 PR **#95131** 提出，核心思路是检测不稳定的解释器路径并固定它，值得关注。
- **[#94906] Windows ... 'subprocess has exited'**：同属 Windows 平台问题，导致 MCP 工具不可用。
- **[#95003] xAI rejects requests ... `tool_search` is reserved**：与特定提供商（xAI）的兼容性问题，只要启用了工具搜索，所有请求都会被拒绝。用户 `SOTO729` 通过 `👍` 获得了 7 个赞同，说明这是一个普遍需求。
- **[#95069] Windows in-app updater deadlock**：更新器自身死锁，导致无法升级。修复 PR 已在列。
- **[#95129] Windows auto-update refreshes cua-driver again**：回响 11 分钟挂起的老问题，新的修复 PR 旨在更安全地处理。
- **[#91115] macOS keychain prompt after update**：与 #52010 类似，是代码签名改变引起的权限问题。

**中低严重级别 (P2/P3) 与回归问题：**
- **[#87697] Ollama stream cancelled**：核心功能与本地模型的兼容性回归。
- **[#94516] Desktop Bot Mode: "Cronjobs are unavailable..."**：一个明确的回归，导致所有机器人无法创建定时任务。已被关闭。
- **[#90428] Messages sent to WS-detached session silently dropped**：网络闪断后，消息静默丢失，无任何错误提示，对用户信心影响较大。
- **[#93617] Slack concurrent turns clobber native stream**：并发场景下的数据竞争，导致 Slack 插件产生重复消息。

**结论**：项目当前最大的稳定性挑战集中在 **Windows 平台（MCP、更新流程）** 和 **macOS 桌面端的权限保持** 上。虽然有修复 PR，但它们多处于待合并状态，能否在下一个版本中彻底解决是社区关注的焦点。

## 6. 功能请求与路线图信号

今日提交的功能请求显示出用户对 **自主性、可观测性和可定制性** 的追求：

- **[#95028] Hermes Authority Execution Layer**：这是一个非常宏大的架构提案。作者 `andrexibiza` 认为当前的 12 个 Issue 其实是同一个底层缺陷，并提出一个“权威执行层”的架构来一揽子解决。虽然目前是 P3 且需要决策，但这类深入的技术讨论可能预示着项目未来架构的演进方向。
- **[#95005] Verified local cold archive**（配套 PR #94428）：用户希望 `hermes sessions archive` 能够提供**本地、可验证的冷归档**，而不仅仅是软标记。这表明用户对数据的所有权和控制权有更高的要求，不仅仅满足于把数据藏在数据库里。
- **[#93382] Adaptive explanation policy**：用户 `kvnloo` 希望引入自适应的解释策略，根据不同的交互场景（如结构化输出、MCP Apps、内联可视化）动态调整 Agent 的解释方式，以提升学习型交互的体验。
- **[#84000] Chrome Extension backend for shared browser control**：此需求旨在解决浏览器自动化中遇到验证码（如 Cloudflare）时的难题，希望通过浏览器扩展的方式实现“人机协同”控制。

**路线图信号**：结合待合并的 PR，一些功能请求已经有了初步实现：
- `feat(sessions): add verified local cold archive` (**#94428**)
- `feat(i18n): Adicionar suporte ao Português do Brasil` (**#92590**)
- `feat(gateway): expose active provider in runtime footer` (**#95135**)

这些迹象表明，项目正在向 **更深度的用户定制（i18n）、更透明的运行状态（provider 显示）以及更可靠的数据管理（归档）** 方向稳步前进。

## 7. 用户反馈摘要

从今日的 Issues 中，可以提炼出以下真实的用户声音：

- **“不要在更新时破坏我的配置”**：多位用户（#52010, #91115, #74973）都报告了更新后配置或权限丢失的问题。用户 `dizhaky` 的详细描述和 `MelloMesh` 的遭遇（更新成功但网关已死且未注册）都表明，更新过程的“静默破坏”是最损害信任的。
- **“本地模型支持是刚需”**：用户 `jayambede` 在 #87697 中详细描述了 Ollama 流被取消的问题，并提到了 `<unused49>` token 循环，这表明有相当一部分用户深度依赖本地 LLM，对他们来说，核心 Agent 与本地推理服务的兼容性优先级最高。
- **“错误应该被看见”**：#90428 中用户 `A2chitect` 提到消息发送失败时“没有错误”、“乐观气泡”，这比明确的错误提示更令人困扰。同样，#95054 中提到 Ollama 回退条目“静默”失败，用户希望至少能看到诊断信息。
- **“细节决定体验”**：#95134 (PR) 给出了一个非常具体的 UI 反馈，用户 `EdderTalmor` 认为自 `--composer-width` 改变后，长文阅读体验下降，而要求增加“聊天宽度”设置。这表明用户对界面细节的舒适度非常敏感。

## 8. 待处理积压

以下问题长期存在或影响重大，但今日没有对应的修复 PR 更新，需要维护者特别关注：

- **[#94906] Windows: native stdio MCP client fails (P1)**：这是目前唯一的 P1 级别问题，且影响面是整个 Windows 平台的 MCP 生态，急需介入。目前没有关联的修复 PR。
- **[#64322] Tool loop guardrail hard-stop silently halts task**：已存在超过一个月，它描述了一个“假死”问题——Agent 的防护机制在“死后”没有给模型留出恢复的余地，需要用户手动干预。这种体验会严重损害用户对 Agent 自主完成长任务的信心。
- **[#87671] Kanban stop-nudge misfires inside delegate_task children**：该问题描述了一个可能导致子任务“越权”并“过早完成父任务”的严重逻辑错误，且有 7 起生产事故记录。虽然已有相关 Issue 被标记，但修复的复杂度和风险可能较高，需要持续关注。
- **[#67619] Feature: Provide safe structured execution context**：这是一个长期的开发者体验改进请求，希望能为快速命令提供标准化的上下文环境，至今没有进展。

---

**项目健康度评估**：尽管面临一些棘手的跨平台兼容性和更新体验问题，但社区的活跃度、PR 的响应速度以及针对关键问题的“Salvage”努力，都表明 Hermes Agent 项目处于一个非常健康且迭代迅速的发展阶段。首要任务是尽快合并并验证针对 Windows 和 macOS 更新问题的修复 PR，以安抚并巩固核心用户群体。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-26

> 数据来源：github.com/sipeed/picoclaw | 统计周期：2026-08-25 至 2026-08-26

---

## 1. 今日速览

过去24小时内，PicoClaw 项目保持中等活跃度：4条 Issue 更新（全部为活跃状态，零关闭）、1条待合并 PR、无新版本发布。值得关注的是，多条"stale"标记的 Issue 在昨日产生了新的评论活动（如 #3281、#3269），说明维护者或社区正在重新审视积压问题。来自 Slack 集成的图片上传 Bug（#3338）已有一对一的修复 PR（#3340）处于待合并状态，修复路径清晰。此外，社区出现了一个方向性的新提案——面向家庭边缘计算的低功耗 Worker 模式（#3345），这可能为项目未来的产品定位打开新的想象空间。整体来看，项目处于"功能稳定、Bug 收敛、社区探索新方向"的阶段。

---

## 2. 版本发布

**无新版本发布。**

上一已知版本仍为 v0.3.1（nightly 构建更新至 commit 2cf030d2）。对于依赖版本更新的用户，建议持续关注项目 Releases 页面。

---

## 3. 项目进展

**核心进展：Slack 媒体上传修复 PR 等待合并**

- **[#3340] fix(slack): set FileSize on media upload params** — 由 octavioturra 提交的修复，精确对应 Issue #3338 中报告的 Slack 媒体上传失败问题。该 PR 为 `slack.UploadFileParameters` 补上了 `FileSize` 字段，规避了 slack-go SDK 因文件长度为 0 而拒绝上传的问题。此 PR 为纯修复性质，不涉及迁移风险，预计将顺利合入。

**整体评估：** 过去24小时没有其他 PR 被合并或关闭，项目在此统计周期内处于小幅推进状态。修复 PR 对应精确的社区反馈，说明项目的 Bug 反馈—修复链条运转正常。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 👍 | 核心诉求 |
|------|----------|--------|-----|----------|
| 1 | [#3281] Web UI 输入卡顿 | 7 | 1 | 长对话历史下 Web UI 输入框严重卡顿 |
| 2 | [#3269] MCP 连接失败导致 Agent 挂起 | 7 | 1 | MCP 服务器故障时聊天界面停止响应 |
| 3 | [#3338] Slack 媒体上传失败 | 2 | 0 | Slack 图片上传始终报文件大小为 0 的错误 |
| 4 | [#3345] 轻量级 Worker 模式提案 | 0 | 0 | 在低资源设备上运行 PicoClaw 的探索 |

**分析：** 社区讨论热度集中在两个"体验级"Bug 上——Web UI 输入卡顿（#3281）和 MCP 连接失败后的界面挂起（#3269），两者都直接影响用户的核心使用体验。值得注意的是，这两条 Issue 均已存在一个月以上且曾被标记为 stale，昨日重新获得评论，可能是维护者开始着手处理或社区用户催促的信号。新提案 #3345 虽尚无评论，但其提出的"轻量级 Worker 模式"切中了边缘设备（RISC-V/ARM/MIPS 开发板、旧 Android 手机）分布式部署的痛点，是项目值得重点评估的方向。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 问题描述 | 修复状态 |
|--------|-------|----------|----------|
| 🔴 高 | [#3269] | **MCP 服务器连接失败导致 Agent 循环挂起，聊天界面完全停止响应**。仅在 nightly 构建（2cf030d2）中验证 | 无修复 PR，需重点跟进 |
| 🟠 中 | [#3281] | **Web UI 输入框在对话历史稍长时严重卡顿**。影响 v0.3.1 正式版，影响面较大 | 无修复 PR，待定位 |
| 🟡 低 | [#3338] | **Slack 媒体上传始终失败**（file size cannot be 0） | ✅ 已有 PR #3340 待合并 |

**风险评估：** #3269 的影响最为严重——MCP 连接失败属于外部服务异常场景，不应导致整个 Agent 挂起，这在生产环境中属于可靠性缺陷。建议维护者优先排查 agent loop 中 MCP 连接错误处理路径。 #3281 作为输入卡顿问题，虽不影响已有对话输出，但长期使用会显著恶化交互体验，建议在下一个版本前修复。

---

## 6. 功能请求与路线图信号

**核心提案：[#3345] 轻量级 PicoClaw Worker 模式**

该提案由 kvnloo 提出，核心构想是让 PicoClaw 工作在资源受限设备（约 10–20 MB 可用内存）上，作为分布式 Agent 网络中的轻量 Worker 节点。具体而言：

- 用户手中通常有多台低功耗设备（树莓派、老旧 Android 手机、RISC-V/ARM/MIPS 开发板）加一台性能较强的 PC
- 提案希望 PicoClaw 能够在这种异构设备组合中运行，让弱设备承担轻量任务，强设备负责重型计算
- 目前尚无实现方案，属早期探索

**当前信号：** 此提案与前几日发布的 Multi-Agent 架构（如有）在方向上可能形成互补。长远来看，若 PicoClaw 定位为"可运行在任何设备上的 Agent 框架"，该提案与项目的开源、轻量特性高度契合，值得纳入路线图讨论。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的真实用户声音：

- **Web UI 输入框卡顿是普遍痛点**（#3281）：用户在会话历史积累到一定长度后（具体长度未明），输入过程出现明显延迟。评论中用户确认问题可稳定复现，且发生在 0.3.1 正式版上，说明这是正式版本存在的性能缺陷，非边界场景。
- **外部服务故障不应拖垮整个 Agent**（#3269）：用户在 MCP 服务器不可用时观察到对话界面完全无响应。用户的核心使用场景是"可以容忍单次 Agent 调用失败，但不能接受整个对话不可用"——这反映了对 Agent 框架容错能力的基本期望。
- **Slack 集成对媒体支持有刚需**（#3338）：用户明确指出错误根因（`file.upload.v2: file size cannot be 0`），并主动定位到 `SendMedia` 构建参数缺 `FileSize` 字段，说明用户具备一定技术能力且有实际使用场景中的明确痛点，此类精确反馈有利于项目快速修复。

---

## 8. 待处理积压

以下为长期未解决的重要问题，提醒维护者关注：

| 条目 | 创建时间 | 已存在 | 状态 | 备注 |
|------|----------|--------|------|------|
| [#3269] Agent 挂起（MCP 连接失败） | 2026-07-20 | 37 天 | 已标记 stale | 严重度最高的未修复 Bug，曾重新活跃 |
| [#3281] Web UI 输入卡顿 | 2026-07-21 | 36 天 | 已标记 stale | 影响正式版用户，重新获得评论 |
| [#3340] Slack 媒体上传修复 PR | 2026-08-17 | 9 天 | 待合并 | 修复明确，建议尽快 review 并合入 |
| [#3338] Slack 媒体上传 Bug | 2026-08-17 | 9 天 | 已标记 stale | 需等待 #3340 合入后验证关闭 |

**建议：** #3269 和 #3281 均已存在超过一个月且影响核心体验，此前被 stale-bot 标记后昨日重新活跃，建议维护者趁此契机明确排期或人工标注处理状态，避免社区形成"反馈无人理"的印象。#3340 的修复代码量小、风险低，应优先合入以关闭 #3338。

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期**: 2026-08-26  
**数据窗口**: 2026-08-25 ~ 2026-08-26 (24h)

---

## 1. 今日速览

NanoClaw 过去 24 小时保持中等偏上活跃度：5 条新 Issues（全部由 glifocat 提交的安全问题）与 50 条 PR 动态形成鲜明对比——Issues 集中在 add-dial/add-vercel 等技能的安全边界缺陷，而 PR 侧则呈现大规模 core-team 驱动的重构与修复潮（Slack handoff、codex composer、项目文档合成等均已有合并动作）。整体来看，项目处于**密集加固期**：安全问题被快速暴露，修复 PR 迅速跟进（如 #3525 Fix blind agent-scope prompt 直接回应 #3532 所在系列问题），但已关闭 PR 中无对应这些新 Issue 的直接修复，存在 1-2 天响应窗口。版本发布为零，系正常节奏。

---

## 2. 版本发布

**无新版本发布**。

---

## 3. 项目进展

今日 16 个 PR 被合并/关闭，核心推进集中在以下三块：

### 3.1 Slack 集成增强（#3545/#3544）
- [PR #3545](https://github.com/nanocoai/nanoclaw/pull/3545) `[core-team] fix(slack): add explicit room handoffs` —— 新增显式 Slack 房间交接工具，支持多 agent 选择；host 端解析真实机器人提及并校验自我/未知/重复/外部/原始提及输入；停止房间创建时自动提及所有参与者，保留投递链路。该功能直接强化了多 agent 协作场景下的 Slack 会话管理能力。

### 3.2 Codex 与项目文档合成重构（#3536/#3537/#3539）
- [PR #3536](https://github.com/nanocoai/nanoclaw/pull/3536) `[core-team] fix(compose): inline every instruction source into one project document` —— 修复 Claude Code 更新引入的安全门禁导致外部 symlink 导入需审批、拒绝一次即持续禁用的严重问题；改为将全部指令源内联到单一项目文档。
- [PR #3537](https://github.com/nanocoai/nanoclaw/pull/3537) / [#3539](https://github.com/nanocoai/nanoclaw/pull/3539) `[core-team] refactor(codex): keep the spec, drop the duplicated composer` —— 删除 Codex 重复的 composer 实现，统一走 trunk 共享 composer；修复 `cli_scope: disabled` 时被错误派发 `ncl tasks` 手册的问题（该命令 host 端直接拒绝）。

### 3.3 Agent 运行环境修复（#3540）
- [PR #3540](https://github.com/nanocoai/nanoclaw/pull/3540) `[core-team] fix(opencode): run the agent session in the agent workspace` —— 修复 OpenCode agent 项目文档遍历失败（cwd 在镜像 WORKDIR `/workspace/group`，为 agent workspace 的兄弟目录而非父目录）。

### 3.4 其他已关闭 PR
- [#2656](https://github.com/nanocoai/nanoclaw/pull/2656) `fix(add-mnemon)` —— 将 mnemon setup 移入 index.ts main()（entrypoint.sh 被 host 覆盖导致 hooks 从未注册）。

**整体判断**: 项目在 CI 基础设施、多 agent 会话管理和文档合成链路三个层面均有实质加固，且 core-team 高频协作、分工明确，属于健康迭代节奏。

---

## 4. 社区热点

今日无高评论/高 👍 的 Issues（均为 0 评论 0 👍），PR 侧评论数不可见。但从 PR 类型分布看：

- **core-team 主导的修复/重构**仍是主力（约 60%），外部贡献者（wakqasahmed、witek、OmriBenShoham、jumprope-jesse）集中在具体 bug 修复和 Slack 线程策略等长尾需求。
- [PR #3311](https://github.com/nanocoai/nanoclaw/pull/3311) `fix(agent-runner): route scheduled-task errors to the operator`（8月18日创建，今日仍在更新）—— 修复计划任务批次无路由字段导致错误消息无法投递的问题，属于基础设施正确性修复，说明社区关注任务可靠投递。
- [PR #2431](https://github.com/nanocoai/nanoclaw/pull/2431) `Conditional thread policy for Slack adapter`（5月12日创建，今日仍有更新）—— 按 DM/频道区分线程策略，反映真实使用场景中对 Slack 消息形态的差异化需求，长期受关注。

**背后诉求**：外部贡献者关注**具体场景下的行为正确性**（Slack 线程、计划任务错误投递），而 core-team 聚焦**架构统一与安全边界**。两者互补，社区参与度健康。

---

## 5. Bug 与稳定性

以下按严重程度排列（高→低）：

| 严重度 | Issue | 描述 | Fix PR 状态 |
|--------|-------|------|-------------|
| 🔴 高 | [#3543](https://github.com/nanocoai/nanoclaw/issues/3543) | `add-dial` 中 email 未加引号直接拼入 shell 命令行 —— 含单引号/元字符的邮箱可注入 shell，且可通过校验 | 无直接 fix；[#3525](https://github.com/nanocoai/nanoclaw/pull/3525) 修复了关联的"盲人 agent-scope 提示"问题但未覆盖此注入 |
| 🔴 高 | [#3532](https://github.com/nanocoai/nanoclaw/issues/3532) | `add-*-tool` 的 agent 范围限定仅覆盖已存在的 groups —— 之后新建的 group 默认获得工具权限 | 无对应 fix PR |
| 🟠 中 | [#3535](https://github.com/nanocoai/nanoclaw/issues/3535) | `add-vercel` 向每个 session 目录 rsync 真实技能副本 —— 阻塞 spawn 时 symlink 同步，且 pin 到过期技能 | 无对应 fix PR |
| 🟠 中 | [#3529](https://github.com/nanocoai/nanoclaw/issues/3529) | `update-nanoclaw` 技能刷新误判所有 channel 导入来自技能 —— 本地自定义 adapter 被覆盖或无退出机制 | 无对应 fix PR |
| 🟡 低 | [#3529 Case 1](https://github.com/nanocoai/nanoclaw/issues/3529) | 同一 Issue 中的本地 adapter 破坏更新流程（阻塞更新） | 同上 |

**补充**：[PR #3542](https://github.com/nanocoai/nanoclaw/pull/3542) `fix: clear container_status drift at startup adoption` 与 [PR #3452](https://github.com/nanocoai/nanoclaw/pull/3452) `fix(update): give captured update commands a real output buffer` 均为稳定性修复，尚未合并。

**评估**：今日 5 条 Issues 全部来自 glifocat 一人，且集中在 add-* 系列技能与更新流程，显示出**技能体系（skill system）在安全与生命周期管理上存在系统性缺口**，建议维护者将该系列问题统筹处理。

---

## 6. 功能请求与路线图信号

### 6.1 明确的功能请求

- [Issue #3538](https://github.com/nanocoai/nanoclaw/issues/3538) —— **隔离容器作为可选的家庭边缘 worker**：用户 kvnloo 提出让 NanoClaw 利用家庭闲置 PC/NAS/服务器作为 worker 节点，而非购买 GPU 或云资源。这是对分布式/异构算力调度的功能需求，与当前单 Docker host 模型形成对比。

### 6.2 可能进入下一版本的能力（依据已有 PR）

| 功能 | PR | 状态 | 说明 |
|------|-----|------|------|
| **本地 Web 聊天频道** | [#3298](https://github.com/nanocoai/nanoclaw/pull/3298) | OPEN，core-team | 无需外部账号即可聊天的内置频道，降低新用户试用门槛，或将纳入下一版本 |
| **结构化 host 健康检查** | [#3482](https://github.com/nanocoai/nanoclaw/pull/3482) | OPEN，core-team | 单次只读调用返回安装状态与内容，解决"空安装 vs 损坏安装"的判别难题 |
| **Setup 驱动协议 (`nanoclaw.driver.v1`)** | [#3485](https://github.com/nanocoai/nanoclaw/pull/3485) | OPEN，core-team | 允许外部程序程序化驱动安装向导，与 [#3486 catalog-preseeds](https://github.com/nanocoai/nanoclaw/pull/3486)、[#3487 --tz](https://github.com/nanocoai/nanoclaw/pull/3487) 构成一组完整的外部配置注入能力 |
| **lease-id 认领与重启竞争保护** | [#3528](https://github.com/nanocoai/nanoclaw/pull/3528) | OPEN，core-team | 基于三个兄弟分支的汇聚，提升 runner 生命周期管理的健壮性 |

**趋势判断**：core-team 正在推进 **host 可编程性（setup driver, health API）** 与**渠道去外部依赖（本地 web chat）**，对应"降低部署门槛"与"增强可运维性"两条路线。边缘 worker 方案大概率不会进入近期版本，但值得观察。

---

## 7. 用户反馈摘要

- **glifocat（Issue #3529）**：作为自定义 adapter 的作者，实际遇到了 **update 流程误伤本地代码** 的痛点——"I have an adapter that lives in my tree. I wrote it. There is no `.claude/skills/add-<n>...`"（技能刷新把它当作技能来源并覆盖/校验失败），且**没有 opt-out 选项**。这反映出**本地定制与自动更新之间的冲突**是真实场景下的高频痛点。
- **glifocat（Issue #3535）**：add-vercel 技能将真实技能副本 rsync 到每个 session 目录（而非 symlink），导致**技能更新无法自动同步**，必须手动重新执行技能。该问题暴露技能分发的复制模式与 symlink 模式的行为差异。
- **glifocat（Issue #3532）**：权限范围设定仅覆盖创建时的 groups，**后续新增 group 自动获得工具权限**——权限模型在时间维度上存在"默认开放"的隐患。

**综合**：反馈主要来自**深度用户/开发者**（glifocat），核心诉求是**技能系统的可预测性**（更新、分发、作用域），以及对**权限边界在时间维度上的严格性**（新实体不应默认获得旧权限）。

---

## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 最后更新 | 说明 |
|------|------|----------|----------|------|
| [#2431](https://github.com/nanocoai/nanoclaw/issues/2431) Conditional thread policy for Slack | PR | 2026-05-12 | 2026-08-25 | 已存活 3 个月；功能简单但涉及 adapter 接口变更，可能与 core-team 正在进行的 Slack 重构（#3545）存在冲突或重叠，需维护者判断是否合并或确认 superseded |
| [#2656](https://github.com/nanocoai/nanoclaw/pull/2656) add-mnemon setup 修复 | PR | 2026-05-31 | 2026-08-25 | 今日已合并，从积压中清除 |
| [#3525](https://github.com/nanocoai/nanoclaw/pull/3525) Fix the blind agent-scope prompt | PR | 2026-08-25 | 2026-08-25 | OPEN；直接回应 agent-scope 系列问题（#3532 等），但今日作者明确将其与 OneCLI 凭据修复解耦，等待 review |
| [#3484](https://github.com/nanocoai/nanoclaw/pull/3484) setup: keep pasted auth secrets out of argv | PR | 2026-08-23 | 2026-08-25 | OPEN；安全相关（凭据出现在 argv 中），建议优先 review |
| [#3311](https://github.com/nanocoai/nanoclaw/pull/3311) scheduled-task 错误路由 | PR | 2026-08-18 | 2026-08-26 | OPEN；已存活 8 天，今日仍在更新，涉及 #3223 修复，需关注推进进度 |

**维护者提醒**：
1. [#3543](https://github.com/nanocoai/nanoclaw/issues/3543) 为 **shell 注入漏洞**（高严重度），建议 24 小时内安排修复；
2. 5 条新 Issue 全部来自同一用户、同一技能体系，建议批量评估统一修复方案，避免逐个 PR 零散处理；
3. setup 系列 PR（#3484-#3487）彼此关联，建议整体 review 而非分散合并。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-26

*数据窗口：2026-08-25 至 2026-08-26 | 数据来源：github.com/nullclaw/nullclaw*


## 1. 今日速览

NullClaw 项目今日整体活跃度处于**低位**：过去 24 小时仅 1 条新 Issue 提交，无新 PR、无版本发布。当前唯一新 Issue 提出了一个颇有分量的架构级构想——利用现有 RuntimeAdapter 与 signed receipts 构建家庭边缘网格，这反映出社区对 NullClaw 在多设备协同方向上的兴趣渐增。短期来看，项目进入了一个观察窗口期，核心维护者的响应节奏将决定本周社区活跃度的走向。

- **新 Issue：1** | **新 PR：0** | **新 Release：0**
- 项目当前整体处于**功能讨论 > 代码产出**的阶段


## 2. 版本发布

今日无新版本发布。建议关注此前已发布版本的后续反馈，等待积累足够的修复与改进后再规划下一个版本。


## 3. 项目进展

**今日无 PR 被合并或关闭。** 项目推进速度暂时放缓，无新代码进入主干。建议维护者关注此前的待合并 PR（见第 8 节），尽快清理积压以保持迭代节奏。


## 4. 社区热点

### 唯一焦点：#994 家庭边缘网格架构构想

- **Issue:** [#994 Household edge mesh using RuntimeAdapter workers and signed receipts](https://github.com/nullclaw/nullclaw/issues/994)
- **作者:** kvnloo | **创建:** 2026-08-25 | **评论:** 0 | **👍:** 0

这是今日唯一的社区声音。作者提出利用 NullClaw 现有的 **RuntimeAdapter + Peripheral vtables + Docker/WASM 适配器 + 硬件发现 + 隧道 + 通道** 等已具备的基础能力，将家中闲置的 PC、笔记本组织成一个边缘计算网格。核心机制设想是通过 **signed receipts（签名收据）** 实现 Worker 间可信协作。

**背后诉求分析：** 虽然该 Issue 目前尚无互动，但其核心诉求与 NullClaw 的定位高度一致——**让闲置硬件发挥作用，延续项目"轻量、严格资源控制"的设计哲学**，将项目从"单一设备上的 AI 助手"推向"家庭级分布式 AI 网络"。这可能是 NullClaw 下一个重要方向的分水岭级讨论，值得维护者认真回复并引导讨论。


## 5. Bug 与稳定性

今日无新的 Bug 或崩溃报告。项目稳定性状态良好。


## 6. 功能请求与路线图信号

### 已提交的功能请求

| 信号 | 来源 | 说明 |
|------|------|------|
| **家庭边缘网格（Household Edge Mesh）** | [#994](https://github.com/nullclaw/nullclaw/issues/994) | 结合 RuntimeAdapter、signed receipts 构建多设备协同网络 |

### 路线图判断

该请求虽未与任何具体 PR 关联，但作者明确指出"NullClaw already has unusually good primitives"，这一观察值得重视——说明项目的底层抽象已具备相当的通用性和可组合性。**该功能若被纳入路线图，将是 NullClaw 从"单机 AI 助手"到"分布式 AI 平台"的关键跃迁**，同时保持项目一贯的"tiny runtime + 严格尺寸/内存目标"理念。建议维护者评估其与现有 Long-Term 目标的兼容性，并在 Issue 中留下初步反馈。


## 7. 用户反馈摘要

今日暂无来自 Issues/PRs 评论的用户反馈。唯一的新 Issue 由 kvnloo 提出，其表述方式表明该作者对 NullClaw 代码库有深入了解——精准列举了 RuntimeAdapter、Peripheral vtables、Docker/WASM 适配器等具体组件——属于**深度用户而非新手**。这传递了一个积极信号：**项目的核心抽象设计正在吸引有能力的开发者在此基础上构建更高层的应用**。


## 8. 待处理积压

以下为长期未响应的内容提醒维护者关注（基于历史数据推断，今日无新增）：

| 类型 | 编号 | 说明 | 建议 |
|------|------|------|------|
| Issue | #994 | 家庭边缘网格提案（今日新开，零回应） | 核心维护者尽快回复初步技术评估，避免高质量提案因冷处理而流失贡献者 |
| PR | *待查* | 从近期合并节奏来看，可能存在等待 review 的 PR | 建议集中 review 并合并积压 PR，恢复项目迭代频率 |

> ⚠️ 注：因本次仅提供 24 小时快照数据，无法获取完整的长期未响应清单。完整积压排查请依赖项目看板或历史数据。


## 项目健康度评估

| 维度 | 评分（5分制） | 说明 |
|------|:---:|------|
| 代码活跃度 | ★★☆☆☆ | 24h 无 PR/Release，处于低活跃期 |
| 社区参与度 | ★★☆☆☆ | 唯一新 Issue 无评论互动 |
| Issue 响应速度 | — | 新 Issue 尚在 24h 响应窗口内，待观察 |
| 项目方向感 | ★★★★☆ | 新提案与核心架构高度契合，路线图信号清晰 |

**总结：** NullClaw 今日处于低产出、高潜力的观察期。新提交的 #994 是一个值得高度重视的架构级提案，将对项目定位产生深远影响。建议维护者在 48 小时内给出初步回应，以把握社区势能。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-26

> 数据来源：github.com/nearai/ironclaw | 统计周期：2026-08-25 ~ 2026-08-26


## 1. 今日速览

过去 24 小时 IronClaw 项目动态密集，**Issues 更新 39 条**（新开/活跃 35 条，关闭 4 条），**PR 更新 24 条**（待合并 13 条，已合并/关闭 11 条），无新版本发布。核心信号包括：**持续性 Bug 的修复面（CI 提速、Telegram 设备绑定指引、通知中心清理）推进有力**，同时有一批值得重视的**性能回归报告（#7891、#7892）**和一个**呼声较高的新功能请求（#7895 个性设置 UI）**。需要特别关注的是，**Telegram 个人账户绑定问题（#7853/#7862）在修复后仍有衍生问题（#7887）**，以及 **Agent 循环陷入死循环（#7892）** 这类直接影响用户体验的中高风险 Bug。整体活跃度评估为 **高**，社区反馈与维护者响应均在 24 小时内完成。


## 2. 版本发布

无新版本发布。


## 3. 项目进展

今日合并/关闭的 PR 共 11 条，其中有 6 条为实质性代码/CI 变更，1 条为核心功能实现：

- **[#7817] ci: nextest test pipeline, full-failure signal, PR unthrottle (T2)** — 已合并。将顺序 per-binary `cargo test` 循环替换为 `cargo-nextest`，单次运行报告全部失败用例，并适度提升 PR 并行度，显著缩短 `Tests (Reborn)` 工作流耗时。 (#7799)
- **[#7809] ci: canonical preflight — 统一的 gate 列表、worktree-safe hooks、自打印 REPRO (T4, tasks 1-5)** — 已合并。`scripts/preflight-gates.sh` 成为唯一确定性 gate 清单，供本地、pre-push hook 与 CI 共用。 (#7801)
- **[#7819] ci: PR/queue check convergence** — 已合并。移除三类已知的 queue-only 失败，并在 PR 阶段新增两项此前仅存在于 merge queue 的检查（default-features clippy 等）。 (#7800)
- **[#7861] fix(extensions): restore device-link guidance on install/activate paths** — 已合并。修复 Telegram 设置流程中“个人账户绑定”无工具可用的引导缺失问题（#7853 的直接修复）。
- **[#7846] refactor(notifications): retire legacy approval fallback** — 已合并。移除旧版 `threads?needs_approval=true` 查询、兼容层和 localStorage 状态，通知中心完全依赖 durable inbox。 (#7706)
- **[#7820] test: scope-isolation suite consolidation probe (T2 follow-up)** — 已合并。测量驱动的测试套件整合探针，参考 #7799。
- **[#7818] feat(subagent): background mode — 实现 R2 后台子代理的生产端** — 已合并。包含收据生成、子级投递、激活与修复扫描（slices 2b+2c），配套前置 #7788。

**整体评估**：以 CI 基建为核心的 T2/T3/T4 系列已全部落地，这意味着开发体验与 CI 稳定性有实质改善；通知中心重构、Telegram 修复和后台子代理均按路线图推进。项目合并节奏健康，核心成员（henrypark133, italic-jinxin）持续高输送。


## 4. 社区热点

最受关注的 Issues（以评论数排序）：

- **#7732 [Open] Epic: Persistent per-user sandbox with iron-proxy（9 条评论）** — 持续一个月的 roadmap Epic，讨论持久化用户沙箱与 iron-proxy 设计，当前仍开放。表明社区对 **本地沙箱生命周期与 workspace 持久化** 有较高期待。
- **#7799 [Closed] CI expedite T2: nextest pipeline（4 条评论）** — 今日已合并，社区曾关心 CI 提速问题，现已闭环。
- **#7862 [Open] Telegram 设备绑定报错（3 条评论）** 与 **#7853 [Open] Telegram 个人账户绑定无法完成（2 条评论）** — 同源问题，用户在实际环境（Railway 实例）中遭遇绑定失败，且错误提示含混。
- **#7891 [Open] 扩展能力载荷 49KB 未投影进 prompt，单轮耗时 19.7s（2 条评论）** — 此性能问题讨论度上升，社区对 **LLM 推理成本与负载瘦身** 关注明显。

**需求信号**：Telegram 绑定问题连续两天被提及，且已有一个修复 PR（#7861）合入，但衍生问题 #7887 仍开放 — 说明当前修复尚未完全覆盖设备绑定场景，需继续跟踪。


## 5. Bug 与稳定性

按严重程度排列：

### 高风险（影响核心运行或数据完整性）

- **[#7892] [风险: 中] Agent 循环死循环 — 15 次查找同一能力却从不调用，单轮耗时 123s** — 未合并 fix。模型发布 31 次能力调用但只有 4 种不同参数组合，且无终止护栏，可能导致资源耗尽。当前无关联 PR。
- **[#7891] [风险: 中] 未投影的扩展能力载荷（49KB MIME 头）导致 19.7 秒推理** — 未合并 fix。两次 `gmail.get_message` 调用导致 14.3s 额外推理成本。属于可量化性能回归，建议设置 prompt 载荷上限。
- **[#7888] 多实例确认：获取日志卡死无响应** — 未合并 fix。用户已在两个独立实例复现，直接影响运维排障能力。

### 中风险（影响功能完整性）

- **[#7862] Telegram 设备绑定失败，错误信息无指引（`api_id/api_hash` 未配置时）** — 已有 PR #7861 合入修复 install/activate 路径，但 #7887 指出 **lookup 路径仍会临时拼装指令**，需补充修复。
- **[#7853] Telegram 个人账户绑定无法完成（缺工具）** — #7861 已修复引导，但仍需用户验证。

### 低风险 / 体验类

- **[#7880] 通知中心加载时无骨架屏** — 已有对应 PR #7883（待合并）。

**整体评估**：今日无高危崩溃或数据丢失类 Bug，但两个中风险性能问题值得优先关注，尤其是 Agent 循环死循环，建议尽快提供终止护栏。


## 6. 功能请求与路线图信号

- **[#7895] 在 Settings UI 中增加 agent 个性设置（agent.md）编辑器** — 新请求，用户明确表达配置个性时遇到困难。与现有 `agent.md` 相关，**有可能并入 v1.4.0 的 WebUI 工作**。
- **[#7889] RFC: Scheduler 增加可选远程边缘 worker** — 面向多主机部署场景，诉求清晰但优先级未定。若采纳将扩展部署模型，建议评估与现有 sandbox worker 的协同。
- **[#7885] 增加 OpenSSF Scorecard workflow 配置** — 已有关联 PR #7886（待合并），此为安全合规类请求，实施成本低，有望合入。
- **[#7867] WebUI composer 语音输入** — 已在 roadmap 中，属于体验增强。
- **[#7871] Epic: Slack-to-console 桥接 + 富交互 Slack UX** — 新 Epic，说明社区对 Slack 作为操作面板的期望提升；与 #4625 形成互补。

**路线图信号**：当前活跃 Epic 集中在 **Design System（#7781/#7782/#7038/PR #7831）** 和 **通知中心扩展（#7872~#7876）**，两个方向均已有 PR 在途。新功能请求中，**个性设置 UI 与远程 worker** 可能会被讨论纳入下一迭代。


## 7. 用户反馈摘要

从 Issues 评论中提炼的真实反馈：

- **Telegram 设备绑定错误信息含混**：多个用户在 Railway 实例上反馈绑定失败，且错误提示只说 “Something went wrong”，无法定位到 `api_id/api_hash` 未配置的根因。(#7862)
- **扩展安装/激活引导不完整**：Agent 会主动提出绑定个人 Telegram，但实际无工具可用 — 说明引导逻辑与实际能力**不一致**，已由 #7861 修复引导层，但底层设备绑定能力仍待完善。(#7853)
- **个性设置入口不够直观**：用户引用推文表示 “me trying to set up personality with ironclaw”，并明确提出希望有专门编辑器而非手动编辑文件。(#7895)
- **日志获取卡死**：多实例复现，影响用户排查问题，期望紧急修复。(#7888)


## 8. 待处理积压

| 编号 | 标题 | 类型 | 关键信号 |
|---|---|---|---|
| [#7491](https://github.com/nearai/ironclaw/issues/7491) | feat(coding): omp core-tool contract + engines + benchmark arm（PR, 开放中） | 大型 PR | 已开放 15 天，待合并，涉及核心 coding 工具面重构 |
| [#7831](https://github.com/nearai/ironclaw/issues/7831) | Design System Phase 3a foundation — Chromatic lane + 缺失 token 轴（PR, 开放中） | 大型 PR | 视觉回归基建，阻塞后续 UI reskin |
| [#7516](https://github.com/nearai/ironclaw/issues/7516) | feat(webui): operator surface for IronHub agent link（PR, 开放中） | 新贡献者 PR | 开放 14 天，涉及 secrets，需维护者评估 |
| [#7884](https://github.com/nearai/ironclaw/issues/7884) | fix: 用 wall-clock 占用上限解锁卡死线程（PR, 开放中） | 修复 PR | 与 #7892 相关，值得参考 |
| [#7732](https://github.com/nearai/ironclaw/issues/7732) | Epic: Persistent per-user sandbox with iron-proxy | Epic | 评论数最多（9 条），已更新但未关闭，建议明确时间表 |

**对维护者的提醒**：#7491 与 #7831 两个大型 PR 长期未合并，可能阻碍后续迭代；#7888（日志卡死）建议优先给出回应或临时 workaround；#7889 的远程 worker RFC 建议给予方向性回复，避免社区预期悬置。


## 附：健康度总览

| 指标 | 数值 | 信号 |
|---|---|---|
| 新开/活跃 Issues | 35 | 高，社区活跃 |
| 关闭 Issues | 4 | 中，积压风险仍高 |
| 待合并 PR | 13 | 中高，需关注合并节奏 |
| 已合并/关闭 PR | 11 | 强，合并通道畅通 |
| 新版本发布 | 0 | 正常（无固定发布周期） |
| 高风险未修复 Bug | 2（#7892、#7888） | 需优先处理 |

*报告生成时间：2026-08-26 | 所有链接均指向 GitHub。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-26

> LobsterAI 是网易有道开源的 AI 智能体与个人 AI 助手项目，涵盖跨平台桌面应用、本地产物管理、协同工作流等能力。本日报基于近 24 小时 GitHub 动态生成。

---

## 1. 今日速览

过去 24 小时 LobsterAI 项目保持**高活跃度**：共发布 2 个版本（2026.8.25 与 2026.8.21），合并/关闭 9 个 PR，主要集中于资料库（Library）产物管理体验优化、设置页模型目录新增、埋点分析与转化归因体系完善三大方向。新开 Issue 仅 1 条（微信群扩容请求），社区的代码贡献节奏明显快于问题反馈节奏。项目整体处于**功能迭代密集期**，平均每 2.5 小时有一个 PR 被处理，值得关注。

---

## 2. 版本发布

### LobsterAI 2026.8.25（昨日发布）
- **核心变更**：
  - `feat(library)`：增强跨平台缩略图与本地产物生命周期管理
  - `feat(library)`：优化本地产物预览与操作体验
  - 另有 `feat: library` 基础能力更新（PR #2513）
- **破坏性变更**：无
- **迁移注意**：本地产物预览类型中 HTML 网页与本地服务已拆分为独立展示类型（见 PR #2533），若有第三方依赖 artifact 类型判断的逻辑需同步调整

### LobsterAI 2026.8.21（前日发布）
- **核心变更**：
  - `feat(dsh)`：为 enable toggle 与 workbench 打开行为新增使用分析
  - `chore`：更新 dsh 至 0.1.1-rc.1
  - `refactor(dsh)`：重构使用分析相关代码结构
- **破坏性变更**：无
- **迁移注意**：dsh 版本已从 rc 走向稳定，建议跟随升级

---

## 3. 项目进展

### 资料库（Library）体验重构 — 核心推进项

| PR | 标题 | 状态 | 影响面 |
|----|------|------|--------|
| [#2531](https://github.com/netease-youdao/LobsterAI/pull/2531) | fix(library): 修复本地产物后台刷新闪烁 | 已合并 | 核心体验修复：拆分首次加载/后台刷新/分页追加状态，避免整页骨架回退；新增按资料 ID 批量查询接口，实现定向更新 |
| [#2533](https://github.com/netease-youdao/LobsterAI/pull/2533) | fix(artifacts): 区分网页与本地服务的预览展示 | 已合并 | 交互优化：HTML 网页与本地服务采用不同图标和文案，明确类型语义 |
| [#2529](https://github.com/netease-youdao/LobsterAI/pull/2529) | feat(analytics): 完善资料库埋点与发布转化归因 | 已合并 | 数据能力：新增 6 类行为埋点，支持发布 CTA 到付费状态的 7 天末次触点归因 |

### 设置与模型管理

| PR | 标题 | 状态 | 影响面 |
|----|------|------|--------|
| [#2530](https://github.com/netease-youdao/LobsterAI/pull/2530) | feat(settings): add plan model catalog | 已关闭（合并） | 设置页新增 plan 模型目录页签，支持按分类展示价格目录，含加载诊断 |

### 其他修复

| PR | 标题 | 状态 | 影响面 |
|----|------|------|--------|
| [#2532](https://github.com/netease-youdao/LobsterAI/pull/2532) | fix(sidebar): fade out login promo tip | 已关闭（合并） | 登录推广提示 5 秒后淡出，并清理 auth 状态变更时的定时器 |
| [#2534](https://github.com/netease-youdao/LobsterAI/pull/2534) | Release/2026.8.20 | 已关闭 | 版本发布分支合回 |

**总体判断**：今日合入的 PR 表明项目正在**系统性地打磨资料库（本地产物管理）的用户体验**，同时为商业化信号埋点（发布转化归因）做数据基建。从合并速度看（9/11 当日关闭），团队的评审和合入效率很高，项目处于健康的快速迭代阶段。

---

## 4. 社区热点

**今日最受关注：Issue #2536 — 微信群已满人**

- [Issue #2536](https://github.com/netease-youdao/LobsterAI/issues/2536)（OPEN）
- 作者：MurrayHubert | 创建：2026-08-25 | 评论：1

用户反馈微信群已满，请求新开微信群。这侧面说明 **LobsterAI 的社区用户基数在增长**，现有的微信群的容量已经不足以承载活跃用户。诉求虽是"拉群"这一小事，但背后反映的是用户对项目有较高的参与意愿，建议项目方尽快新增微信群并同步到 README，避免社区热情降温。

---

## 5. Bug 与稳定性

暂无新增严重 Bug 报告。今日合并的 PR 中包含对以下**体验性问题**的修复：

| 问题描述 | 严重程度 | 修复 PR | 状态 |
|---------|---------|---------|------|
| 本地产物后台刷新时出现整页骨架屏闪烁 | 中（体验回归） | [#2531](https://github.com/netease-youdao/LobsterAI/pull/2531) | ✅ 已合入 2026.8.25 |
| 登录推广提示长期固定展示，干扰侧边栏使用 | 低 | [#2532](https://github.com/netease-youdao/LobsterAI/pull/2532) | ✅ 已合入 2026.8.25 |
| HTML 网页与本地服务预览图标/文案混淆 | 低（信息传达） | [#2533](https://github.com/netease-youdao/LobsterAI/pull/2533) | ✅ 已合入 2026.8.25 |

未发现崩溃、数据丢失或安全类高危问题。

---

## 6. 功能请求与路线图信号

今日暂无新的功能请求 Issue。但从合并的 PR 可看出以下**路线图信号**：

| 信号 | 依据 | 可能纳入版本 |
|------|------|-------------|
| **商业化数据基建** | PR #2529 实现发布 CTA → 付费的 7 天末次触点归因 | 已进入 2026.8.25 |
| **模型价格目录可配置化** | PR #2530/2535 在设置页新增 plan model catalog | 已进入 2026.8.25，后续可能扩展自定义模型 |
| **本地产物生命周期闭环** | PR #2524 增强生命周期管理 + PR #2531 定向更新 | 持续迭代中 |
| **会话分支（Session Fork）** | PR #1159 仍处于 OPEN 状态，功能已实现待评审 | 可能纳入下个大版本 |

---

## 7. 用户反馈摘要

今日唯一 Issue（[#2536](https://github.com/netease-youdao/LobsterAI/issues/2536)）为社区基础设施诉求：用户希望新增微信群。暗示社区活跃度增长，用户对项目有持续跟进意愿。

除此之外，今日的 PR 高频提交者（liugang519、liuzhq1986）主导了资料库体验优化和模型目录功能，说明**核心维护团队正在按规划推进产品路线图**，社区外部贡献（非 dependabot）暂无新增。

---

## 8. 待处理积压

以下为长期未响应、值得维护者关注的事项：

| 类型 | 编号 | 标题 | 搁置时长 | 备注 |
|------|------|------|---------|------|
| PR | [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | chore(deps-dev): bump the electron group（electron 40→43，electron-builder） | 自 2026-04-02 起，约 5 个月 | 依赖升级，建议尽快评审，涉及 Electron 大版本跨越可能影响构建稳定性 |
| PR | [#1159](https://github.com/netease-youdao/LobsterAI/pull/1159) | feat(cowork): add session fork（会话分支） | 自 2026-03-31 起，约 5 个月 | 功能已实现且摘要完整，长期未评审，建议排期合入或明确关闭原因 |
| Issue | — | 微信群扩容需求 | 昨日新开 | 建议 1-2 周内响应 |

> ⚠️ **维护者提醒**：#1277 的 electron 依赖更新已跨越 3 个大版本（40→43），拖得越久升级成本越高；#1159 的 session fork 是一个完整实现的功能 PR，长时间悬置可能造成贡献者流失。

---

*本日报数据基于 2026-08-26 从 GitHub 拉取的 LobsterAI (netease-youdao/LobsterAI) 项目公开信息。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-26

## 1. 今日速览

过去24小时内，Moltis 项目整体活跃度处于**中高水平**：共产生2条Issue更新（1条新开、1条关闭）和5条PR更新（4条待合并、1条已合并关闭），无新版本发布。值得关注的是，当日有多个针对**工具链兼容性修复**（Brave搜索参数、OpenAI schema兼容、Fastmail OAuth）和**沙箱后端扩展**（Kubernetes、Coder）的PR在流，同时一个涉及**共享Slack频道工具失效**的Bug已被关闭。从PR合并/关闭数量（仅1条）来看，项目当前处于**密集开发提交与评审并行**阶段，未出现明显的社区讨论爆发点，但技术栈扩展方向（沙箱后端多元化）信号清晰。

---

## 2. 版本发布

**无新版本发布。** 最近一次Release信息未在本次数据范围内提供，建议关注项目Releases页面追踪后续版本动态。

---

## 3. 项目进展

今日合并/关闭了1条PR，另有4条PR处于待合并状态，整体呈现多条功能分支并行推进的态势：

| PR | 状态 | 推进内容 |
|---|---|---|
| [#1243](https://github.com/moltis-org/moltis/pull/1243) fix(cron): preserve delivered channel context | ✅ 已关闭 | 修复定时消息（如WhatsApp）发送后，后续追问丢失上下文的问题。将发送文本作为assistant消息追加至目标对话，提升跨渠道会话连贯性 |
| [#1245](https://github.com/moltis-org/moltis/pull/1245) fix(tools): validate Brave search parameters | 📋 待合并 | 仅在使用Brave作为搜索提供方时暴露对应本地化参数，并在请求构造前做标准化处理；不支持的市場回退至`ALL` |
| [#1232](https://github.com/moltis-org/moltis/pull/1232) fix(tools): make object schemas OpenAI-safe | 📋 待合并 | 解决OpenAI严格工具schema下，未指定的patch/map字段被强制发送null/空值的问题 |
| [#1244](https://github.com/moltis-org/moltis/pull/1244) Fix Fastmail MCP OAuth scope registration | 📋 待合并 | 在MCP OAuth发现过程中优先使用受保护资源作用域，并纳入RFC 7591动态客户端注册；附Fastmail回归测试 |
| [#1199](https://github.com/moltis-org/moltis/pull/1199) Add Coder remote workspace sandbox support | 📋 待合并 | 新增Coder沙箱后端，通过REST API创建临时workspace，支持模板/preset/参数/TTL等；扩展远程沙箱生态 |

**解读**：项目正在同步推进**工具链健壮性修复**（3条）与**沙箱后端多元化**（已有Kubernetes提出、Coder实现中），这表明Moltis在巩固现有功能质量的同时，正积极拓展运行环境适配边界。

---

## 4. 社区热点

今日讨论最活跃的是 **[#1118](https://github.com/moltis-org/moltis/issues/1118) Add Kubernetes-native sandbox backend with runtimeClassName support**（2条评论，1个👍）。

- **诉求分析**：该Issue提议为Moltis添加Kubernetes原生沙箱后端，通过`runtimeClassName`支持Kata Containers、gVisor等VM级隔离运行时。核心痛点是**当前执行环境无法安全运行不可信的LLM生成代码/命令**，用户希望利用K8s生态获得更细粒度的隔离能力。该需求与同日活跃的PR #1199（Coder远程沙箱）方向一致，共同指向**沙箱后端多样化的核心路线图**。

其余条目今日均无有效评论，社区讨论氛围未形成明显热点。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | 说明 |
|---|---|---|---|
| **高** | [#1224](https://github.com/moltis-org/moltis/issues/1224) Tools stop working in shared Slack channels | ✅ 已关闭（8月25日更新） | 共享Slack频道中工具调用的功能性问题，当前已关闭，但关闭原因（已修复/重复报告/wontfix）在摘要中未明确；若为修复落地，需在版本发布中予以验证 |
| **中** | PR #1245（Brave参数）、#1232（OpenAI schema）、#1244（Fastmail OAuth） | 🔧 修复中 | 三者皆为工具链兼容性缺陷，已提供修复PR并有回归测试覆盖，等待维护者合并 |

**整体判断**：当前无未处理的严重Bug积压；3条功能修复处于待合并状态，建议优先评审合并以尽快消除已知兼容性问题。

---

## 6. 功能请求与路线图信号

**新功能请求（1条）**：
- [#1118](https://github.com/moltis-org/moltis/issues/1118)：Kubernetes沙箱后端 + `runtimeClassName`支持，建议与#1199（Coder沙箱）合并评估，两者共同指向**沙箱后端插件化架构**。

**已实现/进行中的功能信号**：
- PR #1199 已实现Coder远程沙箱，说明**远程/云原生沙箱**是当前明确推进方向
- PR #1232 表明项目正在**适配OpenAI严格工具schema**，可能为兼容Codex等客户端做准备

**预测**：下个版本（Minor或Patch）大概率包含沙箱后端扩展（至少Coder）与OpenAI schema兼容修复；Kubernetes后端是否纳入取决于维护者对#1118的响应优先级。

---

## 7. 用户反馈摘要

- **对沙箱隔离能力的迫切需求**（源：#1118）：用户明确表达了对VM级隔离（Kata/gVisor）的向往，强调“Moltis代理执行来自不可信LLM的代码”，表明当前隔离机制不足以支撑其生产级安全预期。
- **共享频道工具失效**（源：#1224）：用户在共享Slack场景中遇到工具完全不可用的阻断性问题，反映了**团队协作场景**（共享频道）对工具稳定性的高敏感度；该Issue已关闭，用户是否对解决过程满意暂未可知。
- **工具参数的可用性改进**（源：#1245、#1232）：对搜索引擎参数暴露、MCP环境变量结构、patch字段声明的修复，反映了**多模型客户端兼容性**是用户实际使用中的常见痛点。

---

## 8. 待处理积压

**⚠️ 重要提醒 #1118**：该功能请求自2026-06-12创建至今已超过2个月，累计仅2条评论，无维护者正式回应标签，但同日存在相关PR方向（#1199），建议维护者尽快给出**官方路线图层面答复**（是否考虑/排期/设计建议），避免用户诉求悬置。

**📋 长期待审PR**：
- [#1199](https://github.com/moltis-org/moltis/pull/1199)（Coder沙箱）：8月15日创建，已超10天未合并，涉及新后端接入，建议安排设计评审
- [#1232](https://github.com/moltis-org/moltis/pull/1232)（OpenAI-safe schemas）：8月22日创建，涉及核心工具schema变更，建议尽快确认兼容性影响后合并

---

*本报告基于Moltis GitHub仓库实时数据生成，所有链接均可直接跳转访问。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-26

> CoPaw 保持高速迭代节奏，24 小时内 33 条 Issue 更新、50 条 PR 更新、1 个新版本发布。社区活跃度高，问题反馈及时，维护团队响应迅速，项目健康度良好。


## 1. 今日速览

过去 24 小时，CoPaw 项目保持高度活跃的开发和社区互动节奏：共产生 33 条 Issue 更新（新开/活跃 19 条，关闭 14 条）和 50 条 PR 更新（待合并 21 条，已合并/关闭 29 条），并发布了 v2.1.1-beta.3 补丁版本。社区反馈主要集中在 **性能问题（长对话卡顿、内存增长）、微信渠道设置失效、MCP 连接恢复** 等方面，同时也有大量产品体验优化建议（UI 文案、交互细节）。值得注意的是，**长对话渲染掉帧/卡顿** 成为今日 Bug 类 Issue 中讨论最集中的主题，已有多条相关报告和追踪，反映出 Console 前端性能优化是当前用户最急迫的诉求之一。整体来看，项目版本迭代快、社区反馈闭环及时，健康度良好。


## 2. 版本发布

### v2.1.1-beta.3

- **链接**: https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.1-beta.3
- **主要内容**:
  - chore(console): 将 @agentscope-ai/chat 依赖锁定至 1.1.72（PR #7257），确保前端组件版本一致性
  - docs(loop-engineering): 修复文档中 `PluginAPI` 大小写为 `PluginApi`（PR #7269），统一 API 命名规范
  - test(integration): 扩展集成测试覆盖范围（内容截断，未完全展示）

- **破坏性变更**: 无
- **迁移注意事项**: 此版本为依赖锁定和文档修正的补丁版本，无特殊迁移要求。建议 Console 用户关注依赖更新后的前端行为是否正常。

> 由于 Release Notes 展示不完整（截断），更多变更细节可访问 Release 页面查看。


## 3. 项目进展

过去 24 小时共有 29 条 PR 被合并/关闭，虽多数为长期挂起后的收尾或依赖更新，但以下几条值得关注：

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#7261](https://github.com/agentscope-ai/QwenPaw/issues/7261) | Agent 间运行后 SSE 序列化失控循环（100% CPU + 内存无限增长） | 已关闭 | 严重的稳定性问题被解决，为 v2.1.1-beta.2 的关键修复 |
| [#7258](https://github.com/agentscope-ai/QwenPaw/issues/7258) | 微信频道"不显示思考过程"设置无效 | 已关闭 | 渠道功能缺陷得到修复 |
| [#7228](https://github.com/agentscope-ai/QwenPaw/issues/7228) | 应用市场已安装应用悬停时仍显示"安装"按钮 | 已关闭 | UI/UX 细节修复 |
| [#7013](https://github.com/agentscope-ai/QwenPaw/issues/7013) | 为 Chat 增加统一工具面板、Web 服务预览与交互式终端 | 已关闭 | 较大功能改进被合并/关闭，具体实现需要跟进对应 PR |
| [#7129](https://github.com/agentscope-ai/QwenPaw/issues/7129) | Console 长会话 + 流式输出时浏览器渲染掉帧 | 已关闭 | 前端性能问题得到解决 |

此外 [#7276](https://github.com/agentscope-ai/QwenPaw/pull/7276) 将 agentscope 依赖升级至 2.0.7，[#7257](https://github.com/agentscope-ai/QwenPaw/pull/7257) 锁定 chat 组件版本 1.1.72，均有助于提升整体稳定性。

**项目整体进展**: 版本已迭代至 v2.1.1-beta.3，在快速推进功能的同时，对已报告的高优先级 Bug 进行了及时修复（SSE 失控、微信渠道设置等）。CI 测试并行化（PR #7293 待合并）、单元测试覆盖率提升（PR #7292，+5.02pp 至 63.06%）等基础设施改进也在持续推进中，项目整体健康度良好。


## 4. 社区热点

### 🔥 最热门 Issue

1. **[#338 — 建议添加 webhook 功能](https://github.com/agentscope-ai/QwenPaw/issues/338)**（评论 9，👍 1）
   持续近 6 个月仍保持高度关注，用户希望 CoPaw 能以 webhook 方式对外提供异步 API 能力（发送消息→返回 key→轮询/回调获取回答），这一需求场景表明越来越多的用户希望将 CoPaw 集成到自己的自动化工作流中。

2. **[#7258 — 微信频道"不显示思考过程"设置无效](https://github.com/agentscope-ai/QwenPaw/issues/7258)**（评论 6）
   用户在 web 版 2.1 中发现微信渠道中该设置不生效，实际仍输出思考过程。这是一个较为直观的功能缺陷，涉及渠道行为一致性问题。该 Issue 已在 24 小时内被关闭（修复完成或定位到原因）。

3. **[#6524 — MCP 后端重启后客户端无法自动恢复](https://github.com/agentscope-ai/QwenPaw/issues/6524)**（评论 6）
   使用 `streamable_http` 连接远程 MCP Server 时，服务端重启导致 session 失效，客户端仍复用旧的 `mcp-session-id`，需要手动执行 `list mcp` 才能恢复。这是一个影响 MCP 使用体验的中长期问题（已存在约 1 个月），仍处于开放状态。

### 🌟 值得关注

- **[#7261 — SSE 序列化失控循环](https://github.com/agentscope-ai/QwenPaw/issues/7261)**（评论 4）：Agent 间运行后触发 100% CPU + 内存无限增长，属于严重稳定性问题，但已在 24 小时内被快速关闭（修复完成）。

- **[#7259 — 寻求 Windows 内存快速增长报告](https://github.com/agentscope-ai/QwenPaw/issues/7259)**（👍 1）：维护者主动发起求助，寻求 Windows 上 `qwenpaw-backend.exe` 卡在"Thinking"状态时内存快速增长的复现报告，表明维护团队在主动推进特定平台问题的修复。


## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🟥 **严重** | [#7285](https://github.com/agentscope-ai/QwenPaw/issues/7285) | 长对话性能降级严重（v2.1.1b2），电脑卡顿 2s/帧 | 已关闭 |
| 🟥 **严重** | [#7261](https://github.com/agentscope-ai/QwenPaw/issues/7261) | SSE 序列化失控循环（100% CPU + 内存无限增长） | 已关闭（已修复） |
| 🟧 **高** | [#7258](https://github.com/agentscope-ai/QwenPaw/issues/7258) | 微信渠道"显示思考过程"设置无效 | 已关闭（已修复） |
| 🟧 **高** | [#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) | Desktop (Tauri) 内置 OpenSSL 3.0.x，某些运营商网络 TLS 握手被重置 | 开放中，建议升级 CI 至 Python 3.13 |
| 🟧 **高** | [#7296](https://github.com/agentscope-ai/QwenPaw/issues/7296) | OpenAI Responses 多轮对话报错 400 (referenced reasoning item expired) | 开放中（无状态上游） |
| 🟧 **高** | [#7288](https://github.com/agentscope-ai/QwenPaw/issues/7288) | 大 MCP 结果在活跃轮次绕过滚动压缩导致模型上下文溢出 | 开放中 |
| 🟨 **中** | [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) | MCP 后端重启后客户端无法自动恢复 | 开放中（近 1 个月无修复） |
| 🟨 **中** | [#7291](https://github.com/agentscope-ai/QwenPaw/issues/7291) | qwenpaw-creator Windows 11 拉取示例项目报错 | 开放中 |
| 🟨 **中** | [#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) | Windows 安装/更新未终止占用进程导致文件锁错误 | 开放中（近 3 周） |
| 🟨 **中** | [#7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) | 长文本推理时出现 "incomplete chunked read" 报错 | 开放中 |
| 🟩 **低** | [#7282](https://github.com/agentscope-ai/QwenPaw/issues/7282) | Markdown 列表渲染垂直间距过大 | 开放中 |

**值得关注**：
- `#7298` 涉及桌面端 TLS 兼容性问题，虽影响范围有限（特定运营商网络），但影响的是用户连接自托管 HTTPS 端点的核心场景，建议在下一个版本优先修复。
- `#7296` 对使用无状态上游（如 OpenCode Zen、Go Muse Spark）的多轮对话场景有直接影响，是 Responses API 兼容性的重要缺口。
- `#6524` 已存在近 1 个月仍未关闭，MCP 相关的稳定性问题需要维护团队更多关注。


## 6. 功能请求与路线图信号

| Issue/PR | 需求 | 热度 | 分析 |
|---|---|---|---|
| [#338](https://github.com/agentscope-ai/QwenPaw/issues/338) — Webhook 功能 | 通过 webhook 实现异步消息交互（发送→key→轮询/回调） | 评论 9 👍 1 | 持续近 6 个月，是呼声最高的功能请求之一。反映用户希望将 CoPaw 接入自有工作流的强烈需求 |
| [#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196) — 推理过程默认折叠 | 默认折叠思考过程，减少视觉干扰 | 评论 3 👍 1 | 已关闭。思考过程展示是当前高频反馈点，已有多个相关 Issue（#7258/#7196），PR #7163（session 级 thinking 模式）正在推进 |
| [#7182](https://github.com/agentscope-ai/QwenPaw/issues/7182) — 工作区级 Skill 预加载策略 | 基于工作区配置 Skill 的 `on_demand`/`preload` 加载策略 | 评论 4 | 典型的高级用户需求，针对以特定 Skill 为核心的工作区场景优化首轮体验 |
| [#7287](https://github.com/agentscope-ai/QwenPaw/issues/7287) — 零侵入"皮肤网关" | 通过 CSS 注入等方式实现主题/皮肤定制 | 评论 1 | 由 AI Agent 撰写的建议文档，方向新颖但社区基础尚浅，短期内预计不会被采纳 |
| [#7294](https://github.com/agentscope-ai/QwenPaw/pull/7294) — 按像素限制的图片缩放 | 可选开启 `QWENPAW_MAX_IMAGE_PIXELS` 图片缩放 | PR | 针对 provider 图片像素限制的实用增强，默认关闭，对现有行为无影响 |
| [#7013](https://github.com/agentscope-ai/QwenPaw/issues/7013) — 统一工具面板/Web 终端 | Chat 页面提供工具面板、Web 服务预览、交互式终端 | 评论 3 | 已关闭。属于较大的产品功能建议，短期内可能不会在核心版本中实现 |

**路线图信号**: 会话级 thinking 模式（PR #7163）和 Session thinking 级别持久化是当前开发中的重点功能；MCP 相关改进仍在持续；CI/测试基础设施的持续投入（#7292、#7293）表明项目在追求更高质量的代码保障。


## 7. 用户反馈摘要

### 痛点

- **长对话卡顿问题突出**: 用户 MCQSJ 在 [#7285](https://github.com/agentscope-ai/QwenPaw/issues/7285) 中描述"生成 1-2 分钟后电脑鼠标 2s 刷新 1 帧"，且在一台 i5-12450H + RTX 3060 配置的机器上仍复现。ErickCharles 在 [#7129](https://github.com/agentscope-ai/QwenPaw/issues/7129) 中通过 WPR 内核追踪定位到 Chrome 渲染主线程阻塞，明确了是前端渲染问题。多位用户反馈此问题，说明影响面较广。

- **模型上下文/连接问题**: xiaohushi512 在 [#7266](https://github.com/agentscope-ai/QwenPaw/issues/7266) 中反馈 subAgent 任务找错文件夹的问题——在 A 路径的项目文件夹执行 subAgent，却去 B 路径（普通 Agent 默认路径）查找资料。这反映了 Agent 工作目录隔离的缺陷。

- **MCP 连接稳定性**: ruijie-shilu 在 [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) 中对 MCP 后端重启后无法自动恢复表示困惑，需要手动操作才能重新连接。

### 满意/点赞

- **积极的社区协作**: 维护者 rayrayraykk 主动发起 [#7259](https://github.com/agentscope-ai/QwenPaw/issues/7259) 寻求 Windows 内存问题复现报告，用户 elain0205 迅速跟进并提供了详细的复现条件。这种良性互动值得肯定。

- **快速的问题修复**: 多个高优先级 Bug（#7261、#7258、#7285）在 24 小时内被关闭，说明维护团队对严重问题响应迅速。

### 用户期望

- rerbin 在 [#7280](https://github.com/agentscope-ai/QwenPaw/issues/7280) 中希望已完成的后台任务自动清除（或在设置中提供选项），认为当前"已完成任务堆积在列表中"的设计不够合理。
- rerbin 在 [#7279](https://github.com/agentscope-ai/QwenPaw/issues/7279) 中建议模型返回多个选项时用弹窗而非文本输入，认为"Hermes 的弹窗点选更直观"。


## 8. 待处理积压

### 长期未响应的 Issue

| Issue | 创建时间 | 持续时间 | 优先级判断 |
|---|---|---|---|
| [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) — MCP 后端重启后无法自动恢复 | 2026-07-28 | ~1 个月 | **高** — 影响 MCP 用户体验的核心稳定性问题，且已有明确复现步骤 |
| [#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) — Windows 安装/更新文件锁错误 | 2026-08-07 | ~3 周 | **中** — 影响 Windows 用户的安装/更新体验；已有用户明确反馈安装失败 |
| [#7218](https://github.com/agentscope-ai/QwenPaw/issues/7218) — 长文本推理 "incomplete chunked read" | 2026-08-23 | ~3 天 | **中** — 影响自定义模型场景，可能与超时设置相关 |
| [#6273](https://github.com/agentscope-ai/QwenPaw/issues/6273) — 统一任务跟踪和同会话并发语义 | 2026-07-20 | ~1 个月 | **中** — 框架语义层面的问题，需架构层面决策 |

### 长期挂起的 PR

| PR | 创建时间 | 持续时间 | 分析 |
|---|---|---|---|
| [#2773](https://github.com/agentscope-ai/QwenPaw/pull/2773) — 技能自进化引擎 | 2026-04-01 | ~5 个月 | 长期挂起（已标记 Under Review），属于较大功能，可能涉及复杂设计决策 |
| [#1228](https://github.com/agentscope-ai/QwenPaw/pull/1228) — read_media 工具 | 2026-03-11 | ~5.5 个月 | 首次贡献者提交，功能完整但长期未合并，建议维护者明确给出反馈或加速评审 |
| [#1525](https://github.com/agentscope-ai/QwenPaw/pull/1525) — cron 隔离无效持久化计划 | 2026-03-15 | ~5.5 个月 | 功能完善的 bugfix，但合并状态长期未定，建议维护者跟进 |

### 新提交但需关注的 PR

| PR | 提交时间 | 分析 |
|---|---|---|
| [#7299](https://github.com/agentscope-ai/QwenPaw/pull/7299) — 前端拒绝冲突的聊天负载 | 2026-08-25 | 首次贡献者提交，修复 TaskTracker 未执行新 payload 的问题 |
| [#7293](https://github.com/agentscope-ai/QwenPaw/pull/7293) — CI 集成测试并行化分片 (p0/p1/p2) | 2026-08-25 | 基础设施改进，缩短测试时间、提高 CI 效率 |
| [#7190](https://github.com/agentscope-ai/QwenPaw/pull/7190) — qwenpaw-data PyPI 安装 + docker-compose demo | 2026-08-21 | 使 qwenpaw-data 可独立安装运行（无需源码 checkout），对开发者友好 |

---

**总结**: CoPaw 项目处于快速迭代期，版本发布频繁，社区反馈活跃，维护者对高优先级问题响应迅速。长对话前端性能、MCP 连接稳定性和 Windows 安装体验是当前用户最关注的三个方向。建议维护者重点关注 #6524（MCP 恢复）、#6810（Windows 安装锁文件）等长期未关闭问题的修复进展，同时对长期挂起的 PR（#2773、#1228 等）给出明确的决策反馈。整体来看，项目健康度较高，发展势头良好。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-26

> 数据覆盖周期：2026-08-25 ~ 2026-08-26（24小时）

---

## 1. 今日速览

**整体活跃度：高度活跃 🔥**

过去24小时内，ZeroClaw 项目共有 **50 条 Issue 动态**（38 条活跃 / 12 条关闭）和 **50 条 PR 动态**（49 条待合并 / 1 条已关闭），新提交 PR 数量达到 **20+ 条**，覆盖安全加固、运行时修复、功能扩展与 CI 治理四个主线。项目当前处于 **v0.8.x 向 v0.9.0 过渡**的关键阶段，安全类问题（尤其是工具隔离与跨代理越权）占据核心议题，同时社区自下而上的"治理密集"趋势明显——大量 **RFC、tracker 与 follow-up issue** 表明项目正经历从功能驱动到架构治理驱动的转型。值得注意的信号：**安全类 S0/S1 问题持续出现且有修复 PR 跟进**（如 cron 越权 #9947 与工具错误信息丢失 #10357/#10364），项目健康度总体良好，但需警惕 **PR 积压 49 条**可能带来的合并压力。

---

## 2. 版本发布

**无新版本发布。**

上一已知版本为 **v0.8.4**（RFC #6808 标注），当前主要版本轨道为 `master`。追踪 v0.9.0 的 breaking-change 队列位于 tracker [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)。

---

## 3. 项目进展

今日**无 PR 被合并**（仅 1 条关闭），但 24 小时内新提交的 PR 洪流揭示了项目即将推进的方向。以下为实质性且有明确推进意义的待合并 PR：

| PR | 内容 | 影响 |
|---|---|---|
| [#10369](https://github.com/zeroclaw-labs/zeroclaw/pull/10369) | `feat(runtime)!: bound skill HTTP egress` — 禁止代理/重定向、钉住目标地址、限制回包 1MiB | 安全增强；带 `!` breaking-change 标记 |
| [#10351](https://github.com/zeroclaw-labs/zeroclaw/pull/10351) | `feat(runtime): enforce execution-tree iteration budgets` — 实现 #9323 的迭代预算所有权 | 直接落实已接受 RFC，解决 `ToolLoop.shared_budget` 长期被 `None` 问题 |
| [#10367](https://github.com/zeroclaw-labs/zeroclaw/pull/10367) | `fix(skills): prevent symlink races during install` — 改用目录句柄相对路径打开 | 修复 skill 安装 TOCTOU 竞态漏洞 |
| [#10363](https://github.com/zeroclaw-labs/zeroclaw/pull/10363) | `fix(dist): include Git channel in official artifacts` | 回应 #10138 的 Docker 镜像缺 Git Channel 问题 |
| [#10364](https://github.com/zeroclaw-labs/zeroclaw/pull/10364) | `fix(runtime): keep detailed tool output when a short error is also set` | 直接关联今日新 Issue #10357 |

**里程碑意义**：#10351 与 #10369 落地后，ZeroClaw 的**运行时边界控制**（执行树预算 + 工具网络出口）将同时获得强化，这与项目 `security-first` 定位完全对齐。

---

## 4. 社区热点

### 🔥 最热议题：#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup
- **链接**：[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)
- **热度**：24 条评论（今日最高），Rev. 26，持续更新中
- **状态**：已批准（Ratified）/ 正在实施
- **诉求分析**：这是一份**治理型 RFC**，讨论如何优化维护者的工作路由和自动化板管理。持续 3 个月、26 次修订，说明社区对**项目治理流程本身**有强烈参与意愿——维护负担正成为社区关注焦点。

### 🧵 高讨论量 RFC 集群
| Issue | 标题 | 评论 | 关键信号 |
|---|---|---|---|
| [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) | Maintainer decision queue for RFCs | 14 | 维护者决策积压追踪器，需关注 |
| [#9103](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) | separate authoritative memory storage from optional enrichment | 14 | 架构重构，涉及 memory backend，风险高 |
| [#8396](https://github.com/zeroclaw-labs/zeroclaw/issues/8396) | wire protocol first-class in provider construction | 12 | 协议层改造，风险高 |

**规律**：社区热点集中在对**项目治理透明度和架构演进方向**的讨论，而非单一功能兴奋点。

---

## 5. Bug 与稳定性

### 🔴 严重（S0 — 数据丢失 / 安全风险）

| Issue | 状态 | 是否有修复 PR |
|---|---|---|
| [#9206](https://github.com/zeroclaw-labs/zeroclaw/issues/9206) (CLOSED) — agent cron 间歇性将工作目录解析为 `/` | 已关闭 | ✅ 已解决 |
| [#9947](https://github.com/zeroclaw-labs/zeroclaw/issues/9947) — cron 工具未按代理隔离，任何代理可读写删他人任务 | OPEN / in-progress / accepted | ⚠️ 未见定向 fix PR，但 #10351 可能部分缓解 |

### 🟠 中等（S1 — 工作流受阻 / S2 — 行为退化）

| Issue | 影响 | 状态 |
|---|---|---|
| [#10357](https://github.com/zeroclaw-labs/zeroclaw/issues/10357) (NEW) — 工具执行错误路径丢失详细错误体，代理只见 "HTTP 400" | S1，影响代理排错能力 | ✅ 已有 PR [#10364](https://github.com/zeroclaw-labs/zeroclaw/pull/10364) |
| [#9872](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) — bounded delegate 将文件系统解析到委派方工作区 | S2，隔离缺陷 | OPEN / accepted |
| [#10257](https://github.com/zeroclaw-labs/zeroclaw/issues/10257) (CLOSED) — cron update --command 在 agent jobs 上写入未用列 | S2 | ✅ 已关闭 |

### 🟡 轻微（S3 / 体验）

- [#10103](https://github.com/zeroclaw-labs/zeroclaw/issues/10103) — ZeroCode Health 面板法语/西语对齐问题（good first issue）

**关键发现**：#9947 的 cron 越权问题是当前**最严重且尚未有修复 PR** 的开放安全问题，且仍为 in-progress 状态，需保持关注。

---

## 6. 功能请求与路线图信号

### 🔮 本周新增的高价值功能请求（可能进入 v0.9.0）

| Issue/PR | 功能 | 趋势判断 |
|---|---|---|
| [#10360](https://github.com/zeroclaw-labs/zeroclaw/issues/10360) (NEW RFC) | **家庭边缘计算网格**：pull workers + 签名回执的多机协作 | 大胆且契合本地优先路线，但风险高，短期内可能停留在 RFC 讨论阶段 |
| [#10297](https://github.com/zeroclaw-labs/zeroclaw/issues/10297) | **动态工具注册表刷新**：结构配置变更后无需重启 daemon 即可刷新工具 | 高实用价值，与 #10351 的执行树改进形成生态 |
| [#10306](https://github.com/zeroclaw-labs/zeroclaw/issues/10306) | **web/ TypeScript 纳入强制 CI** | 开发者体验/CI 治理改进，大概率被接受 |
| [#10138](https://github.com/zeroclaw-labs/zeroclaw/issues/10138) | **Git Channel 打入官方 Docker 镜像** | ✅ 已有 PR [#10363](https://github.com/zeroclaw-labs/zeroclaw/pull/10363)，接近落地 |
| [#10346](https://github.com/zeroclaw-labs/zeroclaw/issues/10346) (NEW RFC) | 网关/channel 复用 MCP registry 缓存模式（当前每次启动连接 3 次） | 明确的性能优化，风险中，值得关注 |

### 📌 路线图信号
- **v0.9.0 的 auth/安全/网关破坏性变更队列**（tracker [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)）持续推进，当前大量 RFC 的 `breaking-change` 标记均指向该版本。
- 社区对于 **WebAssembly 优先、去 Node.js** 的讨论仍在持续（#8132），但目前处于等待作者响应状态。

---

## 7. 用户反馈摘要

### 🎯 真实痛点

1. **配置变更需要重启 daemon 才能生效** — [#10297](https://github.com/zeroclaw-labs/zeroclaw/issues/10297)"ZeroCode can save configuration changes successfully while the running daemon and existing agent sessions..." 反映用户对热更新能力的期望。

2. **本地小模型被流式数据混淆** — [#8999](https://github.com/zeroclaw-labs/zeroclaw/issues/8999)：用户使用 Ollama + llama3.2 进行简单问候，模型将输入识别为协议/日志负载。**这暴露了流式上下文对本地小模型不友好的深层问题**，影响 ZeroCode 在低算力环境下的可用性。

3. **代理排错体验差** — [#10357](https://github.com/zeroclaw-labs/zeroclaw/issues/10357)：工具调用失败后，代理只能收到 "HTTP 400" 这类裸状态码，无法理解失败原因，"leaving agents with only a bare status"。**核心诉求是让代理在失败时获得可操作的错误信息。**

### 👍 积极信号

- 跨代理隔离问题（#9947、#9872）被社区主动、详细地报告，说明用户对**安全边界有清晰预期**，且在真实多代理环境中进行了验证。
- 法语/西语本地化对齐问题（#10103）被标记为 good first issue，显示社区对**国际化质量的细粒度关注**。

---

## 8. 待处理积压

### ⚠️ 需维护者关注

| 项目 | 类型 | 等待时长 | 状态/原因 |
|---|---|---|---|
| [#10042](https://github.com/zeroclaw-labs/zeroclaw/issues/10042) — MSRV CI 系统依赖安装超时 | CI 问题 | 10天 | 已关闭，但 CI 稳定性需持续观察 |
| [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) — native Hailo-Ollama 支持 | PR | 40天 | `do-not-merge`，风险中，体积 XL，需维护者审阅 |
| [#10142](https://github.com/zeroclaw-labs/zeroclaw/pull/10142) — ZeroRelay 安全传输 | PR | 7天 | `needs-author-action`，高风险的 XL 级 PR |
| [#9447](https://github.com/zeroclaw-labs/zeroclaw/pull/9447) — Anthropic 不完整终止响应分类 | PR | 30天 | `needs-author-action`，需作者更新 |
| [#9527](https://github.com/zeroclaw-labs/zeroclaw/pull/9527) — CI 工具链升级到 1.98.0 | PR | 28天 | `needs-author-action`，例行工具链升级被阻塞 |
| [#10370](https://github.com/zeroclaw-labs/zeroclaw/pull/10370) — 加固 Copilot 凭据缓存 | PR | 今日新增 | `do-not-merge` + `needs-maintainer-review`，高风险的凭据持久化改动 |

### 🧊 长期未响应的 Issue

- [#8132](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)（Rust/WASM web UI 原型评估）— 创建于 6/22，`needs-author-action`，已有 9 条评论但作者未继续推进，WebAssembly 路线可能陷入停滞。

---

## 📊 项目健康度总结

| 维度 | 评级 | 说明 |
|---|---|---|
| **社区活跃度** | ⭐⭐⭐⭐⭐ | 50+50 条动态/日，讨论深入且高质量 |
| **安全性** | ⚠️ 需关注 | 多个 S0/S1 安全问题暴露，大部分已有跟进，但 #9947 仍缺少修复 |
| **PR 合并效率** | ⚠️ 瓶颈 | 49 条 PR 待合并，其中含多条 `do-not-merge` 与 `needs-maintainer-review`，维护者带宽是潜在瓶颈 |
| **治理成熟度** | ⭐⭐⭐⭐ | RFC 流程执行良好，tracker 体系完善，但治理本身消耗了大量社区注意力 |
| **用户满意度** | ⭐⭐⭐⭐ | 本地小模型兼容性与配置热更新是主要不满点，其余反馈积极 |

---

*报告生成时间：2026-08-26 | 数据源：[ZeroClaw GitHub Repository](https://github.com/zeroclaw-labs/zeroclaw)*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*