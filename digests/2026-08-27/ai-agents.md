# OpenClaw 生态日报 2026-08-27

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-27 05:22 UTC

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

# OpenClaw 项目动态日报 — 2026-08-27

## 今日速览

今日 OpenClaw 仓库活跃度处于高位：24小时内新增/活跃 Issue 336 条、关闭 164 条，PR 待合并 289 条、已合并/关闭 211 条，日均吞吐量约 1,000 条更新事件，**社区贡献与维护者响应均处于健康循环**。当前无新版本发布（最新仍为 v2026.8.1-beta.3）。值得关注的是，今日 PR 提交密度显著上升（约 20+ 新 PR），且多条高优先级 P1 修复已进入"待合并"队列，稳定性修复开始加快收敛。最热门的讨论集中在新 beta 反馈、多代理稳定性、消息投递可靠性三大主题。

---

## 项目进展（今日合并/关闭的关键 PR）

以下为今日关闭或具备明确落地价值的主要 PR：

| PR | 主题 | 状态 | 影响 |
|---|---|---|---|
| [#126424](https://github.com/openclaw/openclaw/pull/126424) | fix(gateway): keep conversation delivery within agent bindings | 已关闭 | 多代理场景下会话工具误投递到其他代理的问题已修复，涉及 8 个渠道（Discord/iMessage/Matrix/Slack/Telegram 等），标记高风险（message-delivery/security-boundary） |
| [#125471](https://github.com/openclaw/openclaw/pull/125471) | fix(models): keep Claude CLI OAuth available in Control UI | 已关闭 | 修复 Gateway 重启后 Claude CLI OAuth 刷新所有权丢失的问题（XL 变更，横跨 Web UI/Gateway/Agents） |
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | 已关闭 | 安全边界加固：`security.installPolicy` 可返回 `warn`，交互式 CLI 安装需用户确认后才继续 |
| [#128995](https://github.com/openclaw/openclaw/pull/128995) | feat: make full session actions available from chat header | 已关闭 | Web UI 体验改进：聊天头部菜单补齐置顶/标记未读/设置图标/移动分组等能力 |
| [#120900](https://github.com/openclaw/openclaw/pull/120900) | feat(ui): review install policy warnings | 已关闭 | Control UI 支持审核安装策略警告（含视频证据，安全边界变更） |
| [#128371](https://github.com/openclaw/openclaw/pull/128371) | fix(release): authorize focused beta evidence | 已关闭 | 解除 beta.3 发布阻塞：允许聚焦测试证据通过 FRV 验证，为下一正式版清障 |
| [#115001](https://github.com/openclaw/openclaw/issues/115001) | Hybrid memory search spurious 1.0 similarity scores | Issue 已关闭 | 混合记忆搜索 FTS LIKE-fallback 硬编码 textScore 导致的相似度失真已修复 |

**累计进展判断**：今日合并的 PR 覆盖 4 个方向——**渠道消息投递安全性**、**模型认证状态持久化**、**UI 功能补齐**、**发布流程阻塞解除**。安全边界相关的 PR 密集关闭，说明 8.1  beta 的安全审查正在收尾。

---

## 社区热点

### 1. 新 Beta 反馈（评论 20 条）
[#125626 — OpenClaw 2026.8.1 beta feedback](https://github.com/openclaw/openclaw/issues/125626)

维护者 Patrick-Erichsen 发布的 beta 反馈收集帖持续保持热度，已积累 20 条评论。这已成为社区向官方传导 8.1 候选版问题的**主通道**，同时也标示了 beta 验证的推进节点。

### 2. Gemini 兼容性回归（评论 14 条，👍 3）
[#38327 — "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)

3 月即报告的回归至今仍处于 open 状态且持续活跃，标记为 P1 + `needs-maintainer-review`，且**尚未有修复 PR 关联**。该 Issue 跨月未决，是当前社区对 Google Vertex 集成稳定性最大的不满来源。

### 3. 多代理编排稳定性（评论 13 条）
[#43367 — Multi-agent orchestration is unstable: concurrent agents add/config overwrites, session-lock failures](https://github.com/openclaw/openclaw/issues/43367)

并发 `agents add` 导致配置互相覆盖、session-lock 失败、子任务脱离父会话等问题，P1 级标记，已有相关 PR 链接但仍需维护者 review。多代理已成为 2026 年下半年 OpenClaw 最核心的使用场景，其稳定性直接决定用户的去留。

### 4. 渠道静默丢消息（评论 12 条）
[#87561 — Define durable final fallback delivery semantics across channels](https://github.com/openclaw/openclaw/issues/87561)

由维护者 osolmaz 提交，讨论"最后一条消息投递失败时用户看到沉默"的问题。涉及的 `#845` 相关报告直指 WhatsApp 渠道的真实用户痛感——**用户最不能接受的不是错误，而是无声的失败**。

---

## Bug 与稳定性

### P0 / 发布阻断级

| Issue | 问题 | 状态 |
|---|---|---|
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | **Live Docs 超前发布版本文档**——`IsolatedSessions` 在文档中存在但 2026.3.13 尚未实现（👍 4） | OPEN，无 fix PR，`needs-live-repro` |

### P1 / 高优

| Issue | 问题 | Fix PR |
|---|---|---|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | google-vertex/gemini-3.1-pro-preview "Cannot convert undefined or null to object" | ❌ 无 |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | 多代理并发 config 覆盖 + session-lock 失败 | ⚠️ 已有 linked PR |
| [#87561](https://github.com/openclaw/openclaw/issues/87561) | 跨渠道最终 fallback 投递语义缺失 | ❌ 无 |
| [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex app-server 启动重试在替代服务器就绪前耗尽（crash loop） | ⚠️ linked PR open |
| [#113306](https://github.com/openclaw/openclaw/issues/113306) | SQLite snapshot 恢复缺乏端到端崩溃与身份保证（数据丢失风险） | ❌ 无 |
| [#114154](https://github.com/openclaw/openclaw/issues/114154) | bundle-mcp 工具通过策略检查但 agent 会话永不加载（ToolSearch 零结果） | ❌ 无 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程泄漏，zombie 累积导致运行时降级 | ❌ 无 |
| [#112259](https://github.com/openclaw/openclaw/issues/112259) | 入站消息可被静默丢弃（零 payload dispatch 无重试/死信/用户可见失败） | ❌ 无 |
| [#92241](https://github.com/openclaw/openclaw/issues/92241) | 回滚后 Gateway 持有陈旧模块路径，入站消息静默丢弃（ERR_MODULE_NOT_FOUND） | ❌ 无 |

### 值得关注的中危问题

- [#114234](https://github.com/openclaw/openclaw/issues/114234)：容器内 PID 复用导致 usage-cost 刷新锁永久冻结（P1，linked PR open）
- [#95840](https://github.com/openclaw/openclaw/issues/95840)：contextPruning cache-ttl 模式对 OpenAI 模型永远不会触发（P2，代码级确认）
- [#118793](https://github.com/openclaw/openclaw/issues/118793)：Claude CLI 会话上限错误直接终止 turn 而非触发 fallback（P1）

### 今日已修复（关闭）

- [#90361](https://github.com/openclaw/openclaw/issues/90361)：间歇性 memory_search "index metadata is missing"（标记 not-repro-on-main，社区自行 hotfix）
- [#106555](https://github.com/openclaw/openclaw/issues/106555)：chat.send 4,015 行热点重构为显式生命周期阶段（维护者 steipete 主导，代码质量基建推进）

---

## 功能请求与路线图信号

### 可能纳入 v2026.8.1 的信号

| 功能请求 | 热度 | 分析 |
|---|---|---|
| [#16555](https://github.com/openclaw/openclaw/issues/16555) 投递队列消息 TTL/过期 | 8 评论，P1 | 配合今日 #130643 Telegram 防重复修复，消息投递可靠性正在系统化解决 |
| [#40786](https://github.com/openclaw/openclaw/issues/40786) backup CLI 支持 .gitignore 风格排除 | 11 评论 |=--敏感数据暴露（.env 无法排除）+ 备份体积膨胀，安全 review 挂起中 |
| [#45415](https://github.com/openclaw/openclaw/issues/45415) MEMORY.md 大小警告/限制执行 | 5 评论 | 当前 19,770 chars 即触发静默截断，用户无感知；低成本高价值改进 |
| [#26037](https://github.com/openclaw/openclaw/issues/26037) 阿里百炼 coding plan 支持（thinking/reasoning） | 👍 4，5 评论 | 中国区用户新增需求，已有 linked PR |
| [#17840](https://github.com/openclaw/openclaw/issues/17840) 表情反应触发 agent turn（opt-in） | 7 评论 | 交互范式新颖，但 `needs-product-decision` 未决 |

### 架构级方向

[#60572 — Multi-Slot Memory Architecture](https://github.com/openclaw/openclaw/issues/60572)（👍 3）——将单一 `plugins.slots.memory` 替换为多个专用内存槽。与今日合并的 memory-core NaN-safe 修复（[PR #118750](https://github.com/openclaw/openclaw/pull/118750)）和 memory 索引保留修复（[PR #130698](https://github.com/openclaw/openclaw/pull/130698)）共同表明：**内存子系统正在经历系统性重构**，多槽架构有望在 8.x 系列落地。

---

## 用户反馈摘要

### 满意信号
- PR #120900（UI 审核安装策略警告）与 #116489（CLI 安装确认）被标记为 `proof: 🎥 video`/`proof: sufficient`——社区对安全边界的加固反馈正面。
- #74378（Windows CLI 残留 process）已关闭，Windows 平台体验持续改善。

### 核心痛点（可直接引用的用户原文）

1. **"用户看到沉默是最坏的失败"**（[#87561](https://github.com/openclaw/openclaw/issues/87561) 场景描述引发的共识）——多代理、渠道投递、回滚后遗症等 P1 问题有一个共通点：失败时用户得不到任何反馈。

2. **静默状态迁移**（[#90378](https://github.com/openclaw/openclaw/issues/90378)）："Upgrading from 5.28 → 6.1: cron store migrated to SQLite silently"——用户对无提示迁移持负面态度。

3. **MEMORY.md 静默截断**（[#45415](https://github.com/openclaw/openclaw/issues/45415)）：用户原话——"Our MEMORY.md is at 19,770 chars — 230 chars from silent truncation. We only discovered this by manually checking `wc -c`."——为典型的"无声数据丢失"案例。

4. **备份工具缺排除能力**（[#40786](https://github.com/openclaw/openclaw/issues/40786)）："Cannot exclude `.env`"——安全风险直接暴露。

5. **模型切换后"人格静默改变"**（[#79163](https://github.com/openclaw/openclaw/issues/79163)）：fallback 触发时用户无通知，会话"personality"突然变化，体验割裂。

### 一个令人担忧的模式

多个长期 open 的 P1 Bug（#38327、#92241、#83959、#97616）均标记 `clawsweeper:no-new-fix-pr` + `needs-maintainer-review`，说明 **社区已报告、维护者已知晓、但修复尚未排期**——这些是当前项目健康度最需要关注的积压点。

---

## 待处理积压（需维护者重点关注）

| 类别 | 条目 | 等待时长 | 风险 |
|---|---|---|---|
| **长期未修复的 P0 文档超前** | [#48920](https://github.com/openclaw/openclaw/issues/48920) Live Docs ahead of release | 5 个月+ | 用户按文档配置功能发现不存在，信任损耗 |
| **长期未修复的 P1 回归** | [#38327](https://github.com/openclaw/openclaw/issues/38327) Gemini 3.1-pro-preview 崩溃 | 5 个月+ | Google Vertex 用户持续受影响 |
| **长期未修复的 P1 消息丢失** | [#92241](https://github.com/openclaw/openclaw/issues/92241) 回滚后 ERR_MODULE_NOT_FOUND 静默丢消息 | 2.5 个月 | 生产环境严重事故 |
| **无 fix 的孤儿 Bug** | [#97616](https://github.com/openclaw/openclaw/issues/97616) 子进程泄漏 zombie 累积 | 2 个月 | 长期运行实例降级 |
| **搁置的设计决策** | [#60572](https://github.com/openclaw/openclaw/issues/60572) 多槽记忆架构 | 5 个月 | 功能性重构需求，等待产品决策 |
| **PR 等待过久** | [#77184](https://github.com/openclaw/openclaw/pull/77184) plugin-sdk 类型 re-export | 3.5 个月 | 低风险高价值，维护者需快速回复 |
| **标记 stale 未关闭** | [#93247](https://github.com/openclaw/openclaw/pull/93247) 诊断空闲/恢复修复 | 2.5 个月 | 被 stale 标记但实为 P1，需重新激活 |

### 额外观察

- **发布节奏**：8.1 beta 在 8 月 18 日发布后已积累大量反馈，今日 #128371（focused beta evidence）合入排除了 beta.3 的发布阻塞，**8.1 正式版预计在未来 1–2 周内推出**。
- **合并队列积压**：289 条待合并 PR 是显著积压量，其中包含多条 P1 修复（#130691、#130205、#130643 等），合并节奏需要关注。

---

*本报告基于 openclaw/openclaw GitHub 仓库公开数据自动生成，数据采集时间 2026-08-27。*

---

## 横向生态对比

好的，这是基于您提供的多项目动态摘要生成的横向对比分析报告。

---

### 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**爆发式增长与深度分化**的并行阶段。一方面，以 OpenClaw 为首的核心项目保持着极高的迭代速度与社区活跃度，其生态（如 PicoClaw、NanoClaw）正在迅速填补细分场景；另一方面，生态内部竞争格局初显，**稳定性、消息投递可靠性、上下文（记忆）管理**成为所有项目共同面临的“阿喀琉斯之踵”。值得注意的是，**“静默失败”**（用户无感知的错误）成为跨项目的高频痛点，标志着用户体验的竞争已从“功能有无”转向“过程可控与可观测”。此外，多代理编排、跨平台/网关一致性、安全边界加固是当前技术投入的三大主线。

---

### 2. 各项目活跃度对比

| 项目 | 今日Issue数 | 今日PR数 | Release情况 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 336 (新/活跃), 164 (关闭) | 289 (待合并), 211 (合并/关闭) | 无新版本 (v2026.8.1-beta.3) | **高活跃期**。合并速度快，安全审查收尾，但待合并PR积压量大，需关注合并节奏。 |
| **NanoBot** | 1 (关闭) | 17 (合并/关闭), 15 (待合并) | 无 | **架构重构期**。核心贡献者驱动，但部分PR存在冲突，sustained goal问题有多条修复路径，需协调。 |
| **Hermes Agent** | 50 (更新) | 50 (更新) | 无 | **高活跃期**。问题报告与修复速度同步，但存在多个无修复PR的P1级Bug（如stdio MCP反转），需警惕技术债。 |
| **PicoClaw** | 7 (更新) | 5 (更新) | 无 | **稳定迭代期**。修复性PR为主，社区热点聚焦IRC长消息和Web UI性能，属于体验优化范畴。 |
| **NanoClaw** | 2 (更新) | 24 (更新), 6 (合并/关闭) | 无 | **集中加固期**。外部贡献者批量提交修复PR，但存在高严重度Issue（#3568）未解决，需优先响应。 |
| **NullClaw** | 1 | 0 | 无 | **平稳维护期**。社区贡献热度低，仅一条功能增强请求，项目推进速度或成隐忧。 |
| **IronClaw** | 27 (更新), 18 (新/活跃) | 50 (更新), 48 (合并/关闭) | **v1.4.0-rc.1** | **发布冲刺期**。大量XL级PR合入，核心架构快速收敛，v1.4.0正式版可期。 |
| **LobsterAI** | 2 (新) | 16 (活动), 15 (合并/关闭) | 无 | **高产出期**。合并效率高，功能开发与UI打磨并行，项目节奏稳健健康。 |
| **Moltis** | 1 (关闭) | 2 (合并) | **20260826.01** | **小步快跑期**。反馈闭环快，Bug修复及时，但社区讨论热度低。 |
| **CoPaw** | 33 (新/活跃 18, 关闭 15) | 45 (待合并 17, 合并/关闭 28) | **v2.2.0-beta.1** | **高活跃期**。多租户Hub进入Beta，社区对桌面端稳定性和工具可用性反馈集中。 |
| **ZeroClaw** | 26 (更新), 21 (新/活跃) | 50 (更新), 47 (待合并) | 无 | **稳定化冲刺期**。接受的高优先级RFC已进入实施阶段，但待合并PR数量高，且存在安全修复（SSRF）被阻塞的情况。 |
| **TinyClaw / ZeptoClaw** | - | - | - | 无活动。 |

---

### 3. OpenClaw 在生态中的定位

OpenClaw 凭借其**绝对领先的社区规模和迭代速度**，扮演着生态“锚点”的角色。其日均约 1,000 条更新事件，是其他项目（如 IronClaw、CoPaw）的 10-20 倍，这带来了两个显著优势：
1.  **更快的Bug发现与修复循环**：今日多条涉及消息投递安全、模型认证的P1级修复被快速关闭，展现了强大的工程执行力。
2.  **生态主导权**：社区热点（多代理稳定性、Beta反馈）直接牵引着个人AI助手的技术风向标。

然而，OpenClaw 也面临着**前所未有的复杂性挑战**。其庞大的PR积压（289条）和对**跨渠道（8个）消息投递一致性**的高要求，意味着其稳定性问题可能比生态内任何项目都更早、更集中地暴露。相比之下，IronClaw（近AI）和NanoBot（学术背景）更像是**技术探索者**，在文件系统安全（TOCTOU）、MCP注册框架、Agent生命周期管理等底层架构上敢于下重注，而OpenClaw则更像一个**平台整合者**，在功能广度、渠道适配和用户体验一致性上构筑壁垒。

---

### 4. 共同关注的技术方向

*   **消息投递的“最后防线”**：多项目都在解决“**静默失败**”问题。
    *   **OpenClaw** (#87561)：定义跨渠道的最终兜底投递语义。
    *   **NanoClaw** (#3568)：系统行积压导致代理静默停止响应。
    *   **Hermes Agent** (#96097)：Telegram洪泛恢复时重复推送消息。
    *   **CoPaw** (#7321)：工具调用已结束但界面仍显示“执行中”。
    *   **共同诉求**：确保失败有明确的反馈机制，杜绝无声的数据丢失或状态错乱。

*   **上下文与记忆的系统性重构**：从“补丁”走向“架构”。
    *   **OpenClaw**：提出架构级方案“Multi-Slot Memory Architecture” (#60572)。
    *   **NanoBot**：对Agent运行链和生命周期进行重构，使Usage和推理生命周期显式化。
    *   **ZeroClaw**：RFC“会话级持久化提示附件” (#9998) 进入实施，直指长期记忆丢失痛点。
    *   **IronClaw**：关注未投影的大块MIME头导致推理开销膨胀 (#7891)。
    *   **CoPaw**：关注Prompt cache命中率（81.68% vs 对标96%）和长工具结果截断策略。
    *   **共同诉求**：核心是**控制上下文窗口的成本与有效性**，从被动截断转向主动、智能的上下文管理。

*   **多代理编排与状态一致性**：
    *   **OpenClaw** (#43367)：并发agents操作导致配置互相覆盖、session-lock失败。
    *   **Hermes Agent** (#95965-67)：跨网关Bot房间的持久化与状态同步。
    *   **NanoBot** (#5553, #5257)：sustained goal 在失败后无限续跑的死循环问题。
    *   **共同诉求**：从“能用”到“可靠”，关注并发下的状态同步、任务生命周期边界和故障恢复。

---

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **全渠道、多代理**的个人助手平台 | 寻求“一站式”解决方案的普通用户到高级用户 | 拥有庞大的**渠道适配层（8+）**和成熟的Gateway架构，强调开箱即用的广度。 |
| **IronClaw** | 深度**工作流自动化与安全执行** | 对安全、审计、复杂系统操作（Kubernetes, Docker）有高要求的开发者/运维 | 强调**文件系统安全**（TOCTOU防护）、**沙箱执行**（容器模式）和 **MCP协议**深度集成，技术深度优先。 |
| **NanoBot** | **Agent开发框架与运行时** | 希望嵌入和构建自研Agent应用的开发者 | 拥有清晰的分层架构（Agent运行时、Gateway、WebUI/TUI），代码重构活跃，更像一个**底层框架**而非终端产品。 |
| **CoPaw** | **企业级多租户Hub**与模型网关 | 团队协作、需要统一模型管理和成本控制的企业用户 | 明确向**多租户、Hub集中管理**方向发展，强调RBAC和模型路由，对齐大厂内部AI平台模式。 |
| **Hermes Agent** | **终端优先、开发者友好**的本地Agent | 熟悉CLI、需要本地/远程网关联动的开发者 | 强调**桌面端（Desktop）和CLI/TUI的体验一致性**，是跨网关（RoomLink）架构的探索者。 |
| **NanoClaw / PicoClaw** | **极简、特定场景**的轻量级Claw | 对资源占用敏感或需要极简功能的用户 | 作为生态的“补充者”，NanoClaw重安装与部署体验（超15条相关PR），PicoClaw则关注特定渠道（IRC、LINE）等长尾需求。 |
| **NullClaw** | 暂无明确差异化特性 | 开发者 | 社区热度低，功能推进缓慢，目前处于生态旁观者地位。 |

---

### 6. 社区热度与成熟度

*   **快速迭代、功能扩张期**：**OpenClaw**、**IronClaw**、**Hermes Agent**、**CoPaw**。这些项目拥有高活跃度，新功能（如IronClaw的TUI、CoPaw的多租户）频繁落地，Bug追踪和修复节奏快，但也伴随着稳定性波动和较高的PR积压。
*   **质量巩固、架构优化期**：**NanoBot**、**LobsterAI**、**Moltis**。这些项目不再追求功能数量，而是投入大量精力进行**内部重构**（如NanoBot的Agent生命周期、LobsterAI的分享链路）和**Bug修复回归测试**（如Moltis），展现出更成熟的工程化素养。
*   **社区培育、生态填充期**：**PicoClaw**、**NanoClaw**、**NullClaw**。它们作为“Claw”生态的一员，活跃度主要依赖核心贡献者或特定场景的社区反馈，功能相对单一，处于积蓄力量或被头部项目虹吸的尴尬境地。

---

### 7. 值得关注的趋势信号

1.  **可观测性与失败透明度将成为“标配”**：多个项目对“静默失败”的集中声讨，预示着一款成熟的AI助手必须提供完整的操作追踪、错误反馈和状态可视化（例如重试倒计时、明确错误原因）。这将是未来产品差异化的关键因素。

2.  **安全边界向“工具调用”与“配置”层面下沉**：除了传统的代码安全，社区开始关注因**配置错误**（如NanoClaw的邮件注入、OpenClaw的安装策略警告）或**工具设计缺陷**（如Hermes Agent的stdio MCP反转）导致的安全问题。安全审查将从代码本身扩展到配置引导、工具交互的每一个环节。

3.  **上下文管理是下一阶段的技术制高点**：从OpenClaw的“多槽记忆”架构到IronClaw的“token经济性”讨论，再到ZeroClaw的“持久化附件”，都指向同一个核心——**如何让AI在无限对话中保持低成本、高精度的记忆**。谁能率先解决这个问题，谁就能在智能体体验上取得代差优势。

4.  **企业级功能与个人隐私的博弈开始显性化**：CoPaw的多租户Hub和ZeroClaw的ZeroRelay盲中继（mTLS）是两条路线。前者追求集中管理、权限控制；后者强调隐私保护、数据传输安全。这反映了市场正在分化，无论是企业用户还是隐私敏感的个人用户，都有更明确的技术选型需求。

5.  **平台化与生态化成为主要竞争策略**：OpenClaw通过庞大的渠道和插件生态构建平台，CoPaw通过Hub模式构建企业入口。这表明单纯的“Agent”本身已不再是竞争焦点，**“Agent + 渠道 + 管理 + 安全 + 可观测”的一体化生态**才是吸引和留住用户的关键。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-27

---

## 1. 今日速览

NanoBot 过去 24 小时整体活跃度较高，核心贡献者 `chengyongru` 密集推送了 12 个 PR，项目在 Agent 生命周期、WebUI 架构和 TUI 体验三个方向均有显著推进。当日共关闭 1 个 Bug Issue（#5550，`read_session` 通配符查询返回空历史），合并/关闭 PR 17 个，当前仍有 15 个 PR 待合并，其中 4 个存在冲突需解决。无新版本发布。项目正处于架构重构的密集期（Agent 运行链、WebSocket 编排、Usage 后端等），健康度良好但仍需关注冲突与积压 PR 的处理节奏。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共合并/关闭 17 个 PR，其中核心贡献者 `chengyongru` 贡献了 12 个，涵盖 Agent 运行时、TUI/WebUI 交互、Gateway 稳定性三个维度。主要集中在以下几条关键路径：

### Agent 生命周期重构（已完成合并）
- **PR #5556** — fix(agent): complete native reasoning lifecycle — 完整修复了 provider 原生推理生命周期的关闭时机，包括在答案内容、本地工具执行、托管工具事件、流恢复和请求完成前的正确关闭顺序。同时将推理生命周期状态保持在单次 provider 请求内部，保留 hook 对 inline `<think>` 解析的所有权。[查看 PR](https://github.com/HKUDS/nanobot/pull/5556)
- **PR #5555** — refactor(agent): remove duplicate progress streaming path — 移除了未使用的 `AgentRunSpec.progress_callback` 输入及 runner 中的第二个 provider 流式状态机，将 reasoning、answer delta、tool hints 统一收口到现有的 per-run hook 路径。[查看 PR](https://github.com/HKUDS/nanobot/pull/5555)
- **PR #5546** — refactor(agent): make run usage explicit — 删除了进程级的 `AgentLoop._last_usage` 副作用通道，usage 采集改为 per-run hook 方式，`/status` 接口读取 session 级 usage。[查看 PR](https://github.com/HKUDS/nanobot/pull/5546)

### Gateway/WebUI 稳定性提升
- **PR #5544** — fix(gateway): recover degraded WebSocket listener — WebSocket 监听器在 bind 成功后正确记录运行状态，并对可恢复的监听失败执行带封顶指数退避的重绑，同时区分非瞬态 bind/config 错误。管理健康检查和 GatewayStatus 可区分不同故障层级。[查看 PR](https://github.com/HKUDS/nanobot/pull/5544)
- **PR #5548** — refactor(webui): isolate websocket application orchestration — 将重连水合逻辑迁移至 `WebUISessionProjection` 和 `WebUIOutboundProjector`，语义化出站运行时事件通过 `WebUIOutboundProjector` 路由，入站信封、请求生命周期、临时聊天、工作区策略等均完成有序编排。[查看 PR](https://github.com/HKUDS/nanobot/pull/5548)
- **PR #5543** — fix(tui): surface chat connection failures — 区分就绪初期、恢复工作、健康确认恢复、持续不可用与不可恢复服务故障五类状态；仅在连接失败后查询网关 `/health` 端点。[查看 PR](https://github.com/HKUDS/nanobot/pull/5543)

### TUI/WebUI 交互优化
- **PR #5534** — feat(tui): autocomplete skill references — TUI 支持 `$skill-name` 引用自动补全，含过滤选择器、方向键/Tab/ESC 交互、光标感知补全。[查看 PR](https://github.com/HKUDS/nanobot/pull/5534)
- **PR #5538** — refactor(tui): clarify active composer actions — 保留 `Enter` 立即发送与 `Tab` 当前回复结束后发送两种行为，更新 composer 占位提示为 `Enter send now · Tab send next`。[查看 PR](https://github.com/HKUDS/nanobot/pull/5538)
- **PR #5519** — fix(webui): compact single-pane chat header — 压缩单栏聊天头部与对话顶部间距，保持多栏模式不受影响；模型选择器新增小尺寸模型设置入口。[查看 PR](https://github.com/HKUDS/nanobot/pull/5519)
- **PR #5491** — fix(webui): keep answer text outside reasoning shell — 跨 answer → tool → answer 轮次保留每个助手回答片段；reasoning/工具活动保留在活动面板，回答片段合并为一条最终消息。[查看 PR](https://github.com/HKUDS/nanobot/pull/5491)

### 工具与性能
- **PR #5533** — fix(tools): keep find_files scans responsive — find_files 全量扫描移入 worker 线程，替换重复 pathlib 元数据调用为有预算的 `os.scandir` 遍历，分页预读后停止路径排序扫描，并支持取消传播。[查看 PR](https://github.com/HKUDS/nanobot/pull/5533)
- **PR #5557** — perf(tui): skip redundant dependency installs — 使用 `tui/package.json` 与 `tui/bun.lock` 的 SHA-256 指纹缓存成功安装结果，匹配时跳过 `bun install --frozen-lockfile`。[查看 PR](https://github.com/HKUDS/nanobot/pull/5557)
- **PR #5481** — feat(usage): add unified provider usage backend — 为 gateway 管理的 WebUI/TUI 会话中每个重试管理的 provider 尝试记录一行 content-free usage。[查看 PR](https://github.com/HKUDS/nanobot/pull/5481)

---

## 4. 社区热点

今日 PR 数量多但评论数较少（多数 PR 评论数为 undefined），没有单条 Issue/PR 出现高互动量的集中讨论。值得关注的两条线索：

- **PR #5234**（OPEN）— feat(agent): integrate mst-python as a metasearch provider — 提议引入 Meta-Search Tool（聚合 DuckDuckGo、Google、Brave、Bing 等多引擎结果，通过 RRF 融合排序）作为新搜索提供方。该 PR 自 8 月 3 日创建至今已开放 24 天，仍待合并，属于长期未解决的外部贡献。[查看 PR](https://github.com/HKUDS/nanobot/pull/5234)
- **PR #5553**（OPEN）— fix(agent): hold goal continuation after a failed completion attempt — 外贡献者 `yonghuname` 指出 sustained goal 在模型完成失败后仍会持续触发 goal-continue 消息的问题，与 #5257（shakewingo 的 bound sustained-goal continuation）构成同类问题的两条并行修复路径。[查看 PR](https://github.com/HKUDS/nanobot/pull/5553)

---

## 5. Bug 与稳定性

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| P1 | [#5553](https://github.com/HKUDS/nanobot/pull/5553) | sustained goal 在模型已完成但调用的 tool result 为错误时，runner 仍持续注入 goal-continue 消息，导致死循环式重试 | OPEN（冲突） |
| P1 | [#5257](https://github.com/HKUDS/nanobot/pull/5257) | 同类问题：无终止条件的 recurring request 被登记为 sustained goal 后永久 active；turn 空闲时 goal 延续未受控 | OPEN（冲突） |
| P1 | [#5544](https://github.com/HKUDS/nanobot/pull/5544) | WebSocket 监听器 bind 失败后进入 degraded 状态且不恢复 | 已合并 fix |
| P2 | [#5550](https://github.com/HKUDS/nanobot/issues/5550) | `read_session` 在模型使用通配符查询（`"*"`、`".*"` 或空白）时返回空历史 | CLOSED |
| P2 | [#5543](https://github.com/HKUDS/nanobot/pull/5543) | TUI 在连接失败时无法区分"初始就绪中"与"持续不可用"，用户看到误导性状态 | 已合并 fix |
| P2 | [#5339](https://github.com/HKUDS/nanobot/pull/5339) | WebSocket 路径读取临时聊天策略后等待时用户丢弃聊天，恢复后 scope 可能被持久为普通聊天 | OPEN（冲突） |

**重点风险**：sustained goal 完成失败后无限续跑的问题（#5553、#5257）已有两条修复路径且均标注冲突，提示核心维护团队需尽快协调合并策略，避免该稳定问题长期暴露在生产环境。

---

## 6. 功能请求与路线图信号

- **Meta-Search 聚合搜索**（[#5234](https://github.com/HKUDS/nanobot/pull/5234)）：引入 mst-python 聚合多引擎搜索，丰富搜索覆盖度。PR 标注为 P1、已开放 24 天但仍挂着 `conflict` 标记。考虑到该 PR 与当前代码库的融合需要协调，若维护者认可方向，大概率进入下一版本。
- **TUI 技能引用自动补全**（[#5534](https://github.com/HKUDS/nanobot/pull/5534)）：已合并，TUI 输入 `$skill-name` 时支持过滤、键盘导航与插入。
- **临时侧边对话**（[#5364](https://github.com/HKUDS/nanobot/pull/5364)）：WebUI 支持 `/side` 打开临时对话，多标签切换、独立草稿与流式状态、可并行发送。已开放 14 天并标注冲突，功能已完成度高，需维护者协调解决冲突后合入。
- **模型重试状态可视化**（[#5504](https://github.com/HKUDS/nanobot/pull/5504)）：发布脱敏的模型重试生命周期事件，TUI/WebUI 在恢复或 fallback 接管前持续展示重试倒计时与进度。同样带 `conflict` 标记。
- **Langfuse 追踪 for Codex**（[#5520](https://github.com/HKUDS/nanobot/pull/5520)）：为 Codex provider 增加 Langfuse 原生跟踪（Codex 使用 httpx + OAuth 而非 OpenAI SDK 兼容层，无法复用现有 client-swap 方案）。

---

## 7. 用户反馈摘要

- **#5550**：用户通过 `@session` 引用另一对话并要求模型检查其历史时，模型携带通配符参数（`"*"`、`".*"` 或空白）调用 `read_session` 期望获取全部消息，实际返回空。反馈已关闭，说明代码库已完成修复或该行为通过内部处理得到纠正。
- **#5553**（外部贡献者 yonghuname）：持续目标（sustained goal）在完成调用失败后仍被 runner 注入延续消息，导致模型反复尝试已失败的操作，形成负担循环。反馈直指目标生命周期边界不清晰。
- **#5339**（外部贡献者 KDB-Wind）：WebSocket 临时聊天在用户主动丢弃后，请求仍可能恢复并持久化为普通会话，涉及数据隐私与用户意图不一致的场景，值得维护者关注。

---

## 8. 待处理积压

- **[#5234](https://github.com/HKUDS/nanobot/pull/5234)（OPEN 24 天，外部贡献）**：mst-python metasearch 提供方整合 — 新搜索能力、P1 优先级、长期未合入，需维护者评估是否纳入路线图。
- **[#5364](https://github.com/HKUDS/nanobot/pull/5364)（OPEN 14 天，外部贡献）**：WebUI 临时侧边对话 — 功能完整度高、P2 优先级、带冲突标记。
- **[#5339](https://github.com/HKUDS/nanobot/pull/5339)（OPEN 16 天，外部贡献）**：WebUI 拒绝已丢弃的临时聊天消息 — 涉及数据一致性与用户意图，带冲突标记。
- **[#5520](https://github.com/HKUDS/nanobot/pull/5520)（OPEN 3 天，外部贡献）**：Codex Langfuse tracing — P2 优先级。
- **[#5504](https://github.com/HKUDS/nanobot/pull/5504)（OPEN 3 天）**：模型重试状态 UI 展示（NAN-34）— 带冲突标记。
- **[#5257](https://github.com/HKUDS/nanobot/pull/5257)（OPEN 22 天，外部贡献）**：bound sustained-goal continuation — P2、带冲突标记，与今日新 PR #5553 存在重叠，建议维护者优先协调。

---

*本日报基于 GitHub API 数据自动生成，数据截至 2026-08-27。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-27

## 1. 今日速览

项目今日活跃度极高，过去24小时内有50条Issue更新和50条PR更新，呈现出一个大型开源项目在密集迭代中的典型状态——**问题报告速度与修复速度几乎同步**。今日无新版本发布，但维护者通过PR #96095对昨日重开的桌面端多网关持久连接追踪问题（#94724）进行了快速响应修复。值得注意的是，**stdio MCP子进程存活检查逻辑反转（inverted liveness check）成为今日最严重的Bug集群**——已有5个独立Issue（#94335、#94637、#95165、#95150）报告相同根因，涉及Windows/macOS/Linux多平台，严重影响所有stdio传输方式的MCP服务器。与此同时，桌面端（Desktop）继续占据Issue和PR的最大比重（约40%），说明桌面端目前是社区使用最密集、问题暴露最多的区域。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日无直接合并的PR，但有一批高价值PR处于待合并状态，多位维护者（teknium1、dokterdok）正在积极推动关键修复和功能落地：

### 关键修复推进

| PR | 说明 | 状态 |
|---|---|---|
| [#96095](https://github.com/NousResearch/hermes-agent/pull/96095) | `hermes serve`被杀时刷新会话 + 实时压缩配置的unset语义；直接响应#94724重开后的两个问题 | 待合并，维护者teknium1提交 |
| [#96092](https://github.com/NousResearch/hermes-agent/pull/96092) | 修复空会话清理误删已归档transcript的问题（#95868） | 待合并 |
| [#96090](https://github.com/NousResearch/hermes-agent/pull/96090) | 修复fallback时`api_mode`从provider自身声明解析，而非手写检测链 | 待合并 |
| [#96097](https://github.com/NousResearch/hermes-agent/pull/96097) | 修复Telegram洪泛恢复时重复推送流式final消息 | 待合并 |

### 功能开发推进

| PR | 说明 | 状态 |
|---|---|---|
| [#95965](https://github.com/NousResearch/hermes-agent/pull/95965) / [#95966](https://github.com/NousResearch/hermes-agent/pull/95966) / [#95967](https://github.com/NousResearch/hermes-agent/pull/95967) | dokterdok提交的三层堆叠PR：跨网关Bot房间在Desktop关闭后仍可运行——从`RoomLink`（网关间定向成员turn分发）到持久异步运行组合，再到桌面端多网关Bot房间无缝体验 | 均为draft状态，needs-decision标记 |
| [#95278](https://github.com/NousResearch/hermes-agent/pull/95278) | 可选的共享指标导出器（telemetry Phase 2），向NousResearch遥测服务POST每日指标包 | 待合并，`sweeper:risk-compatibility`标记 |
| [#96087](https://github.com/NousResearch/hermes-agent/pull/96087) | Phase 1 管理/用户工具层级白名单（#20744 RFC的salvage），带可选turn预算 | 待合并，needs-decision |
| [#96088](https://github.com/NousResearch/hermes-agent/pull/96088) | 飞书特权卡片点击由操作者授权而非群组策略——修复#96045安全边界问题 | 待合并，P1安全标记 |
| [#96089](https://github.com/NousResearch/hermes-agent/pull/96089) | Slack可选频道历史上下文回填 | 待合并 |
| [#96093](https://github.com/NousResearch/hermes-agent/pull/96093) | 桌面端browser_exec工具行按前导#步骤注释命名（与CLI/TUI对齐） | 待合并 |

### 基础设施

| PR | 说明 | 状态 |
|---|---|---|
| [#96098](https://github.com/NousResearch/hermes-agent/pull/96098) | 测试套件隔离标准落地，含导入时沙箱和确定性运行时环境变量 | 已关闭（合并） |
| [#96091](https://github.com/NousResearch/hermes-agent/pull/96091) | 导出coding-agent token/成本使用量为`hermes.*`指标 | 已关闭（合并） |

**总体评估**：项目在多条战线上同时推进，尤其是跨网关RoomLink架构（#95965-95967）如果落地，将是Hermes多网关部署的一个重要能力跃升。此外，telemetry和指标导出基础设施（#95278、#96091）已开始为可观测性铺路。项目整体向前推进速度正常，但需要关注待合并PR数量（41条）是否有持续积压趋势。

---

## 4. 社区热点

### 热点一：stdio MCP子进程存活检查Bug集群（评论合计25+）

以下5个Issue报告了**完全相同的根因**——`_stdio_children_dead()`返回值逻辑反转：

| Issue | 评论 | 要点 |
|---|---|---|
| [#94335](https://github.com/NousResearch/hermes-agent/issues/94335) | 13 | 原始报告：`_stdio_children_dead()`在子进程存活时返回`True`；由#81995的fail-fast机制引入 |
| [#94637](https://github.com/NousResearch/hermes-agent/issues/94637) | 10 | Windows 11复现：所有stdio MCP服务器（ADO、GBrain、chrome-devtools）全部失败 |
| [#95165](https://github.com/NousResearch/hermes-agent/issues/95165) | 2 | 独立复现，明确标注duplicate |
| [#95150](https://github.com/NousResearch/hermes-agent/issues/95150) | 2 | 独立复现，`hermes mcp test`通过但实际调用失败 |

**用户诉求**：这组Issue共同指向一个清晰的信号——**stdio传输方式的MCP服务器是用户侧广泛使用的核心路径**，任何一个逻辑反转都能瞬间让所有依赖MCP能力的用户工作流瘫痪。5个独立报告者来自不同平台（Windows 11、macOS、Linux），说明影响面极广。截至本日报发布时，尚无修复PR，该问题已存在至少3天。

### 热点二：远程网关会话恢复失败（#93888，评论12）

Hermes Desktop向远程Gateway发送本地运行时ID，导致所有已存储会话无法恢复，用户会永久卡在"Restore failed — Session not found"。涉及`sweeper:risk-session-state`和`sweeper:risk-compatibility`两个风险标记，说明维护者已意识到这是会话状态兼容性的深层问题。

### 热点三：#94724重开——桌面端多网关持久连接（评论8）

teknium1发起的追踪问题展示了一个"已完成"战役如何在最后关头发现两个遗漏：legacy会话迁移和serve刷新间隙。该问题被重开，且维护者teknium1今日立即提交了#96095进行修复，反应迅速。

---

## 5. Bug 与稳定性

### P1 严重级

| Issue | 影响面 | 状态 |
|---|---|---|
| [stdio MCP子进程检测反转](https://github.com/NousResearch/hermes-agent/issues/94335)（#94335/#94637/#95165/#95150） | 所有使用stdio传输的MCP服务器全部不可用 | **无修复PR** |
| [Gateway SIGSEGV崩溃](https://github.com/NousResearch/hermes-agent/issues/94248)（#94248） | macOS arm64，委托worker到600秒deadline时崩溃；12份Apple crash reports | 无修复PR |
| [Desktop发送本地运行时ID到远程网关](https://github.com/NousResearch/hermes-agent/issues/93888)（#93888） | 所有远程网关的会话恢复功能不可用 | 无修复PR |
| [Telegram网关无限挂起](https://github.com/NousResearch/hermes-agent/issues/95816)（#95816） | Telegram gateway无法连接 | 被标记为duplicate |
| [中断的hermes update导致网关永久停留在旧代码](https://github.com/NousResearch/hermes-agent/issues/95294)（#95294） | 所有平台，update中断后运行中的网关不会自动修复 | 无修复PR |

### P2 中级

| Issue | 影响面 | 状态 |
|---|---|---|
| [#96073](https://github.com/NousResearch/hermes-agent/issues/96073) 辅助任务503不触发provider fallback | 供应商宕机时辅助任务降级而非切换provider | 无修复PR |
| [#95589](https://github.com/NousResearch/hermes-agent/issues/95589) Windows update后不重启桌面端 | Windows桌面端，2/2可复现，僵尸进程 | 已关闭 |
| [#95188](https://github.com/NousResearch/hermes-agent/issues/95188) 已删除的profile通过两条路径复活 | Windows，v0.20.5 | 无修复PR |
| [#95327](https://github.com/NousResearch/hermes-agent/issues/95327) 进行中的turn被后台respawn杀死 | Windows桌面端，282次reap，213次backend respawn | 已关闭 |
| [#95559](https://github.com/NousResearch/hermes-agent/issues/95559) 桌面端backend停止服务executor路由 | Windows 11，新标签页卡在"Runtime not ready" | 已关闭 |
| [#95279](https://github.com/NousResearch/hermes-agent/issues/95279) 桌面端Bots模式模型选择器无法使用 | 选择模型后页面自动重载，选择被清除 | 无修复PR |
| [#95293](https://github.com/NousResearch/hermes-agent/issues/95293) 桌面端静默丢弃返回`confirm_required`的模型切换 | contributor-tier模型无法选择 | 已关闭 |

### 今日已有关闭/修复的Bug

- [#96095](https://github.com/NousResearch/hermes-agent/pull/96095) 修复serve被杀后丢失内存会话——直接回应#94724
- [#96092](https://github.com/NousResearch/hermes-agent/pull/96092) 修复空会话清理误删归档transcript
- [#96097](https://github.com/NousResearch/hermes-agent/pull/96097) 修复Telegram洪泛恢复时重复final消息
- [#96098](https://github.com/NousResearch/hermes-agent/pull/96098) 测试套件隔离标准

### 特别关注

**#95294（中断的update导致网关永久停留在旧代码）** 与 **#95589（Windows update后不重启）** 共同揭示了一个系统性问题：**`hermes update`流程的鲁棒性不足**。多个环节（git pull之后、restart之前）一旦被中断，系统不会自愈。这应该是下一版需要着重加固的路径。

---

## 6. 功能请求与路线图信号

### 社区呼声较高且已有对应PR的功能

| 功能请求 | 对应PR | 信号 |
|---|---|---|
| [MCP工具级别的审批门控](https://github.com/NousResearch/hermes-agent/issues/49167)（#49167，评论5）——将现有终端命令审批扩展到MCP工具的外部写入操作 | 暂无直接PR | 安全敏感场景的核心需求，P3标记，但长期未落地（创建于2026-06-19） |
| [RealtimeVoiceProvider ABC接口](https://github.com/NousResearch/hermes-agent/issues/77111)（#77111，评论5）——四个竞争的双工语音PR需要一个统一接口 | 暂无；注意[#95193](https://github.com/NousResearch/hermes-agent/pull/95193)正为WebUI添加移动浏览器语音对话 | 已触发`AGENTS.md`的"3+ PR同类别时设计ABC"规则 |

### 值得关注的新信号

1. **跨网关房间架构**（#95965-95967）：dokterdok的三层堆叠PR，目标是让多网关Bot房间在Desktop关闭后依然运行。虽然目前是draft状态且标记`needs-decision`，但这是一个面向"Desktop无关性"的重要方向。
2. **遥测/指标导出**（#95278、#96091）：shared-metrics exporter和`hermes.*`指标导出，说明项目正在构建可观测性基础设施，可能为后续运营面板或用量追踪做铺垫。
3. **[内存默认值提升](https://github.com/NousResearch/hermes-agent/issues/5320)**（#5320，评论8）：`memory_char_limit`从2200字符和1375字符自动扩展，这是一个长期存在的痛点（创建于2026-04-05），用户希望更智能的默认值管理。

---

## 7. 用户反馈摘要

### 真实痛点

1. **stdio MCP是最核心的扩展路径，失效影响巨大**：多位用户在#94335/#94637的评论中详细描述了依赖MCP服务器（ADO、GBrain、chrome-devtools）的日常工作流完全中断。"这是个show-stopper"级别的评论隐含在多个报告的细节中。

2. **Windows平台的更新和恢复流程脆弱**：#95589报告"2/2可复现"的update后不重启问题；#95188报告已删除的profile通过两条路径复活。Windows用户对于更新和状态管理的可靠性评价明显偏低。

3. **Desktop Bot Mode的可用性问题集中爆发**：今日5个与Desktop Bots模式相关的Issue（#95279、#95293、#96062、#92286、#88874），涵盖了模型选择器无法使用、切换模型被静默丢弃、点击bot chat跳到sessions列表、侧边栏tab指示器缺失、profile看起来重复等**用户体验**问题。这说明Bot Mode是一个正在快速迭代但还不够成熟的功能。

4. **远程/多网关场景的会话管理是薄弱环节**：#93888（远程会话无法恢复）、#93910（macOS sleep后SSH隧道不重建）、#94724（多网关连接追踪）——这些表明用户正在尝试将Hermes部署到更复杂的拓扑中（远程Gateway、多网关共存），但会话状态的管理逻辑尚无法完全支撑。

### 满意/亮点

- 维护者对#94724的快速响应（当天提交修复PR #96095）得到了社区正面反馈。
- 多个Issue被快速标记为duplicate并合并到主追踪问题，减少了碎片化讨论。

---

## 8. 待处理积压

### 长期未解决的高价值Issue

| Issue | 创建时间 | 时效 | 说明 |
|---|---|---|---|
| [#5320](https://github.com/NousResearch/hermes-agent/issues/5320) feat(memory): 提升memory_char_limit默认值 | 2026-04-05 | 已145天 | 评论8，👍2，至今无对应PR。长期会话用户内存不足的痛点 |
| [#54945](https://github.com/NousResearch/hermes-agent/issues/54945) Mem0 OSS setup flags被顶层argparse拒绝 | 2026-06-29 | 已60天 | 文档化功能实际不可用，阻塞Mem0的OSS非交互式配置路径 |
| [#49167](https://github.com/NousResearch/hermes-agent/issues/49167) MCP工具级别审批门控 | 2026-06-19 | 已70天 | 安全敏感功能，已与另一个Issue标记为duplicate，但仍无实现 |
| [#86740](https://github.com/NousResearch/hermes-agent/issues/86740) computer-use doctor应区分CLI和gateway的Wayland环境 | 2026-08-15 | 已13天 | 诊断信息误导用户，暂无PR |

### 今日新增但需关注

| Issue | 要点 |
|---|---|
| [#96062](https://github.com/NousResearch/hermes-agent/issues/96062) 点击bot chat有时跳到sessions列表 | 创建于今日，评论1，影响约一半的bot聊天窗口 |
| [#96073](https://github.com/NousResearch/hermes-agent/issues/96073) 辅助任务503不触发provider fallback | 创建于今日，涉及供应商故障场景下的降级逻辑 |

### 待合并PR积压提示

当前有41条PR待合并。以下几条因涉及面广或需要决策，建议维护者尽早跟进：

- [#95965](https://github.com/NousResearch/hermes-agent/pull/95965) / [#95966](https://github.com/NousResearch/hermes-agent/pull/95966) / [#95967](https://github.com/NousResearch/hermes-agent/pull/95967)：跨网关RoomLink三层堆叠，均标记`needs-decision`
- [#96087](https://github.com/NousResearch/hermes-agent/pull/96087)：管理/用户工具层级白名单，涉及安全边界，标记`needs-decision`
- [#95278](https://github.com/NousResearch/hermes-agent/pull/95278)：遥测导出器，标记`risk-compatibility`，可能影响隐私敏感用户

---

## 项目健康度总评

- **活跃度**：极高。50条Issue + 50条PR在24小时内更新，说明社区使用量大、反馈积极。
- **响应速度**：良好。维护者对关键追踪问题（#94724）的反应速度很快，当日即提交修复PR。
- **痛点集中**：stdio MCP的Bug暴露了测试覆盖的一个盲区——这个逻辑反转入库后3天没有测试捕获，说明MCP子进程管理相关的单元测试需要加强。
- **风险信号**：待合并PR（41条）与开放Issue（35条）的比例偏高，如果该趋势持续，可能形成技术债。建议关注合并队列的消耗速度。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 PicoClaw 仓库在 2026-08-27 的实时数据，我为您生成了以下项目动态日报。

---

## PicoClaw 项目动态日报 (2026-08-27)

### 1. 今日速览

PicoClaw 项目今日活跃度**中等偏上**，核心贡献者与社区用户均在积极推动项目演进。过去24小时共产生 7 条 Issue 更新和 5 条 PR 更新。值得关注的是，**稳定性修复**是当前主线：一方面，社区针对 Slack 媒体上传、LINE 配置失效等具体 Bug 提交了高质量的修复补丁；另一方面，关于路由 Agent 上下文管理的修复被合并，解决了长期存在的功能缺陷。此外，社区对 Web UI 性能、IRC 长消息支持等体验问题表达了强烈诉求，是下一阶段版本迭代的重要信号。

### 2. 版本发布

今日无新版本发布，项目处于开发迭代阶段。

### 3. 项目进展

今日有 3 个 PR 被合并/关闭，标志着项目在**修复关键缺陷**上取得了实质性进展：

- **[#3316] [已合并] fix: routed-agent context management not respecting history, summarization, compression, and seahorse bootstrap**
  这是今日最重要的合并。该 PR 修复了通过分发规则路由到非默认 Agent 的会话中，无法记忆历史消息、自动压缩不生效的问题。这直接解决了 Issue #3301 中提到的核心痛点，极大提升了多 Agent 路由场景下的可用性。（[查看 PR](https://github.com/sipeed/picoclaw/pull/3316)）

- **[#3315] [已合并] Support topics in private bot chats**
  修复了 Telegram 私有机器人聊天中，当启用论坛主题模式时，PicoClaw 无法识别消息主题的问题，扩展了 Telegram 频道场景的兼容性。（[查看 PR](https://github.com/sipeed/picoclaw/pull/3315)）

- **[#3314] [已合并] fix: agent not able to execute shell command added to customAllowPatterns**
  修复了 `customAllowPatterns` 配置不生效，导致默认拒绝规则优先级过高，使得用户无法执行 `git push` 等自定义允许命令的问题，增强了系统的安全可配置性。（[查看 PR](https://github.com/sipeed/picoclaw/pull/3314)）

这些合并表明维护者正在积极处理因路由、频道适配和安全策略导致的复杂集成问题，项目整体稳定性和配置灵活性正在提升。

### 4. 社区热点

- **[Issue #3287] [Feature] Better support long messages in IRC** (评论: 8)
  该 Issue 是目前讨论最热烈的议题，尽管发布时间较早，但仍在持续获得关注。用户 `superuser-does` 指出 IRC 协议默认限制为 512 字节，导致长消息会被客户端强制分割，破坏了 AI 对话的上下文连贯性。社区正在探讨如何让 PicoClaw“理解”被分割的消息并重新组合。
  **诉求分析**: 这反映了用户对跨渠道体验一致性有较高期待，希望 PicoClaw 能智能处理不同通讯协议的技术限制，以保证 AI 交互的完整性。（[查看 Issue](https://github.com/sipeed/picoclaw/issues/3287)）

- **[Issue #3281] [BUG] Web UI chat input is very laggy when history has a little bit long** (评论: 7, 👍: 1)
  紧随其后，该 Issue 反映当会话历史较长时，Web UI 输入框出现明显卡顿，严重影响核心使用体验。这不仅是性能问题，更关系到重度用户和长时间对话场景下的产品可用性。
  **诉求分析**: 用户对前端渲染性能极其敏感，该问题可能涉及前端渲染机制或状态管理优化，是提升用户满意度的关键点。（[查看 Issue](https://github.com/sipeed/picoclaw/issues/3281)）

### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **高严重度 - 功能完全不可用**:
    - **[Issue #3338] Slack does not attach image media content**：Slack 媒体上传功能完全失败，原因是`SendMedia`构建请求参数时未设置 `FileSize`，被 SDK 直接拒绝。**已有修复 PR #3340** 待合并。（[Issue #3338](https://github.com/sipeed/picoclaw/issues/3338)）
    - **[Issue #3339] Antigravity generation returns generic 429**：Google Antigravity 模型的生成请求总是返回 429 限流错误，但认证和模型发现流程均正常，疑似存在逻辑错误或配额误判。（[Issue #3339](https://github.com/sipeed/picoclaw/issues/3339)）

- **中严重度 - 特定配置下功能异常**:
    - **[Issue #3328] [已关闭] line.settings.webhook_host / webhook_port are never read**：LINE 频道的 webhook 配置项虽已定义并写入文档，但代码中并未读取，导致用户自定义配置无效。虽然该 Issue 今日被自动标记为关闭，但**修复 PR #3329** 目前仍处于开放待合并状态，问题尚未真正解决。（[Issue #3328](https://github.com/sipeed/picoclaw/issues/3328)）
    - **[Issue #3301] [已关闭] /clear and session auto-compression don't work...**：该问题已由 PR #3316 的合并而解决，可视为闭环。

- **待确认严重度**:
    - **[Issue #3346] about RKLLM reply**：用户报告在 ARM 开发板上运行 RKLLM 模型时出现异常回复，但描述较为模糊，且发布时间极短，尚待项目方回应对话以获取更多细节。（[Issue #3346](https://github.com/sipeed/picoclaw/issues/3346)）

### 6. 功能请求与路线图信号

- **[Issue #3287] IRC 长消息支持**：社区对于在多行或长文本场景下的处理有明确需求。虽然该 Issue 尚未关联 PR，但考虑到 IRC 协议的特殊性，若 PicoClaw 计划加强 IRC 频道的专业度，该功能应被重点考虑。

- **Web UI 性能优化**：Issue #3281 虽被标记为 Bug，但核心是对 UI 渲染架构或虚拟滚动等高级特性的需求，可能推动前端性能优化成为后续版本的重要议题。

### 7. 用户反馈摘要

- **用户对 Slack 渠道的稳定性感到不满**：Issue #3338 的提交者 `octavioturra` 直接定位到代码层缺陷，指出 `SendMedia` 构建参数不完整导致 SDK 拒绝请求。这表明用户具备专业技术能力，也反映出该Bug对工作流的直接影响较大。
- **用户对 AI 服务的配置体验存在困惑**：Issue #3339 的提交者 `k3XD16` 表示已验证 OAuth 权限和模型发现均成功，但生成请求却一直失败，这种“定向失败”让用户感到十分困惑和沮丧。
- **用户渴望更真实的智能**：Issue #3287 中关于 IRC 长消息的讨论，体现了用户希望 AI 能理解被协议“切断”的上下文，而不仅仅是按行处理，这背后是对更高级自然语言处理能力的期待。

### 8. 待处理积压

以下 Issue/PR 长期未获响应或处理，需维护者重点关注：

- **[PR #3329] [开放] fix(line): warn on inert webhook_host / webhook_port instead of seeding them**
  该 PR 旨在解决已关闭 Issue #3328 中 LINE 配置无效的问题。由于 Issue 已关闭，若不合并此 PR，该 Bug 的修复将被遗漏。尽管该 PR 部分被标记为 stale，但因其直接对应一个确切的配置逻辑漏洞，建议维护者及时评估合并。（[查看 PR](https://github.com/sipeed/picoclaw/pull/3329)）
- **[Issue #3346] about RKLLM reply**：该 Issue 刚创建，但涉及 RKLLM 在端侧（ARM）的运行，属于特定硬件环境问题。为了完善对端侧模型的支持，建议尽快与用户沟通以定位问题。（[查看 Issue](https://github.com/sipeed/picoclaw/issues/3346)）

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-27

---

## 1. 今日速览

NanoClaw 过去 24 小时保持高活跃度，共产生 2 条 Issue 更新和 24 条 PR 更新，其中 18 条 PR 待合并、6 条已合并或关闭，无新版本发布。值得关注的是，同一作者 Agi-Asi 批量提交了 15 条修复类 PR，覆盖安装脚本、容器唤醒、任务日志、SDK 配置等多个稳定性问题，显示出项目正处于一轮集中的稳定性加固阶段。与此同时，新报告的 Issue #3568（系统行积压导致代理静默失联）涉及核心消息队列逻辑，严重程度较高，目前尚未有对应修复 PR，建议优先跟进。

---

## 2. 版本发布

**无**

过去 24 小时无新版本 Release。

---

## 3. 项目进展

今日 6 条 PR 已合并/关闭，以下为核心变更：

| PR | 标题 | 状态 | 说明 |
|----|------|------|------|
| [#3557](https://github.com/qwibitai/nanoclaw/issues/3557) | fix(mattermost): improve initial setup and SiteURL handling | ✅ 已合并 | 改进 Mattermost 渠道的初始配置流程与 SiteURL 处理逻辑 |
| [#3556](https://github.com/qwibitai/nanoclaw/issues/3556) | fix(mattermost): recover card thread after restart | ✅ 已合并 | 修复 Mattermost 交互式卡片在主机重启后丢失线程缓存的问题，点击历史审批卡片不再报错 |

两条 Mattermost 修复均由核心团队成员 glifocat 提交并在当日合并，直接提升了 Mattermost 渠道的稳定性与恢复能力。

**待合并的 18 条 PR 中，15 条来自 Agi-Asi 的批量修复，覆盖领域包括：**

- **安装与配置**：`~/.local/bin` PATH 顺序修复（[#3567](https://github.com/qwibitai/nanoclaw/pull/3567)）、signal-cli 探测超时（[#3563](https://github.com/qwibitai/nanoclaw/pull/3563)）、非交互式 apt 安装（[#3562](https://github.com/qwibitai/nanoclaw/pull/3562)）、launchd plist 引导（[#3561](https://github.com/qwibitai/nanoclaw/pull/3561)）、Node 版本下限提升至 22.14.0（[#3555](https://github.com/qwibitai/nanoclaw/pull/3555)）
- **容器与运行**：容器唤醒失败通知（[#3566](https://github.com/qwibitai/nanoclaw/pull/3566)）、Claude SDK 输出 token 上限修正（[#3558](https://github.com/qwibitai/nanoclaw/pull/3558)）
- **任务与日志**：task_log 行写入系列 ID（[#3564](https://github.com/qwibitai/nanoclaw/pull/3564)）
- **渠道与兼容**：跨平台 emoji 反应标准化（[#3553](https://github.com/qwibitai/nanoclaw/pull/3553)）、Node 25+ 测试断言修正（[#3554](https://github.com/qwibitai/nanoclaw/pull/3554)）
- **CLI 与文档**：无 agent 时快速失败并给出接线提示（[#3560](https://github.com/qwibitai/nanoclaw/pull/3560)）、group-scope 自动填充参数文档措辞修正（[#3559](https://github.com/qwibitai/nanoclaw/pull/3559)）、fork 仓库保留本地适配器（[#3565](https://github.com/qwibitai/nanoclaw/pull/3565)）

此外，wildcard 提交的两条 PR（[#3551](https://github.com/qwibitai/nanoclaw/pull/3551)、[#3552](https://github.com/qwibitai/nanoclaw/pull/3552)）涉及 per-group 远程 MCP 策略强制与 OneCLI 网关路由，目前处于待审核状态。

---

## 4. 社区热点

今日讨论热度最高的 Issue 是 **#574**（[链接](https://github.com/qwibitai/nanoclaw/issues/574)）：

> **Issue #574 — containers lack jq**
> 作者：ErikDeBruijn | 评论数：3 | 👍：1
> **状态**：已关闭（CLOSED）

该 Issue 提出容器内应包含 `jq` 工具用于解析 API 响应，指出当前 swarm 倾向于使用 `node -e` 进行解析存在 eval 注入风险。这条 Issue 虽创建于 2026 年 2 月，但在今日被关闭，说明维护者已对其做出处理。从安全角度看，`node -e` 执行动态代码确实存在命令注入面，使用 `jq` 作为替代是更安全的选择。

**社区诉求分析**：用户对容器工具链的完整性和安全性有明显需求，尤其是在 API 调用响应解析场景下。该 Issue 的关闭可能意味着修复已合入，建议在后续版本说明中向社区确认。

---

## 5. Bug 与稳定性

**🔴 高严重度**

| Issue/PR | 描述 | 当前状态 |
|----------|------|----------|
| [#3568](https://github.com/qwibitai/nanoclaw/issues/3568) | **待处理的 `system` 行积压导致入站队列饥饿，代理静默停止响应**。当会话累计超过 `maxMessagesPerPrompt`（默认 10）条待处理的 `system` 行时，代理对所有入站消息不再响应，且无任何错误提示 | 🔴 无修复 PR，自 2026-08-26 报告 |

**🟡 中严重度**

| Issue/PR | 描述 | 当前状态 |
|----------|------|----------|
| [#574](https://github.com/qwibitai/nanoclaw/issues/574) | 容器缺少 jq，使用 `node -e` 解析存在 eval 注入风险 | ✅ 已关闭，建议确认修复内容 |
| [#3549](https://github.com/qwibitai/nanoclaw/pull/3549) | `insertMessage()` 使用普通 INSERT，重试时触发 UNIQUE 约束错误，被记录为投递失败并反复重试，形成无限崩溃循环 | 🟡 已有修复 PR 待合并 |
| [#3550](https://github.com/qwibitai/nanoclaw/pull/3550) | 邮件 prompt 验证正则允许 shell 元字符（`;`、反引号、`$()`），且替换时未加引号，存在命令注入风险；含撇号邮箱（如 `o'brien@x.com`）会破坏 shell 行 | 🟡 已有修复 PR 待合并 |

**🟢 低严重度（安装/脚本类）**

Agi-Asi 的 15 条 PR 中多名列前茅的问题包括：signal-cli 配置锁死锁（#3563）、apt 安装 needrestart 挂起（#3562）、launchd plist 未加载时 kickstart 静默无效（#3561）、Node < 22.14.0 时 better-sqlite3 段错误（#3555）等。这些均属于安装部署路径的稳定性问题，修复 PR 已在队列中。

---

## 6. 功能请求与路线图信号

- **`jq` 工具集成**（[#574](https://github.com/qwibitai/nanoclaw/issues/574)）：虽然为 Enhancement 且优先级 Low，但涉及安全（eval 注入），已被关闭，预计已完成或即将完成。
- **MCP 策略强制**（[#3551](https://github.com/qwibitai/nanoclaw/pull/3551)、[#3552](https://github.com/qwibitai/nanoclaw/pull/3552)）：wildcard 提交的两条 PR 将 per-group 远程 MCP 策略强制化，并通过 OneCLI 网关路由，这一方向可能成为后续配置安全增强的重点。
- **容器唤醒用户通知**（[#3566](https://github.com/qwibitai/nanoclaw/pull/3566)）：用户在消息的容器反复唤醒失败时收到通知，改善用户体验，方向是更好的错误可见性。

结合当前 PR 队列，下一版本很可能重点集中在**安装流程可靠性、渠道稳定性（Signal、Mattermost）、CLI 体验改进**三个方向。

---

## 7. 用户反馈摘要

从今日活跃的 Issues 和 PR 中可提取以下用户痛点：

1. **静默失败是最令人困惑的问题**：Issue #3568 中用户描述代理"silently stops responding"（静默停止响应），无任何错误信息。这已是第二次出现类似反馈（#3566 也是关于容器"repeatedly fails to wake"时用户无感知），说明**错误可见性不足**是当前用户最常见的痛点之一。

2. **安装路径上存在多处陷阱**：来自不同作者的多个修复 PR 表明用户在安装和初次配置过程中遇到了 signal-cli 死锁（#3563）、apt 挂起（#3562）、Node 版本过低导致的数据库崩溃（#3555）、PATH 配置错误（#3567）等问题。这可能是新用户流失的主要原因。

3. **安全敏感的用户关注命令注入面**：Issue #574 的用户明确指出使用 `node -e` 解析 API 响应存在 eval 注入风险，PR #3550 也修复了电子邮件替换中的 shell 元字符注入问题。安全意识的用户在社区中活跃发声。

4. **Mattermost 集成用户对恢复能力有期待**：PR #3556 修复了重启后卡片线程丢失问题，PR #3557 改进了初始设置。这说明 Mattermost 渠道已有实际用户使用并反馈过恢复场景的问题。

---

## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 年龄 | 说明 |
|------|------|----------|------|------|
| [#3568](https://github.com/qwibitai/nanoclaw/issues/3568) | Issue | 2026-08-26 | 1 天 | 🔴 **高优先级**：系统行积压导致代理静默停止响应，无修复 PR。建议立即分配负责人 |
| [#3552](https://github.com/qwibitai/nanoclaw/pull/3552) | PR | 2026-08-26 | 1 天 | Codex MCP-only 策略强制，待核心团队审核 |
| [#3551](https://github.com/qwibitai/nanoclaw/pull/3551) | PR | 2026-08-26 | 1 天 | per-group MCP 策略与 OneCLI 网关路由，待核心团队审核 |
| [#3550](https://github.com/qwibitai/nanoclaw/pull/3550) | PR | 2026-08-26 | 1 天 | 邮件注入修复 + 验证正则加固，涉及安全问题，建议优先合并 |
| [#3549](https://github.com/qwibitai/nanoclaw/pull/3549) | PR | 2026-08-26 | 1 天 | 消息重试无限崩溃循环修复，建议优先合并 |
| [#3501](https://github.com/qwibitai/nanoclaw/pull/3501) | PR | 2026-08-24 | 3 天 | Dial 渠道文档补充（README + 变更日志），等待合并 |

**提醒**：Agi-Asi 的 15 条 PR 为批量提交，虽然彼此独立，但建议维护者集中评审以保持队列清爽；其中 #3555（Node 版本下限）和 #3558（Claude SDK token 上限）涉及运行时核心依赖，建议优先测试合并。

---

## 项目健康度总评

| 维度 | 评分（5 分制） | 理由 |
|------|---------------|------|
| 活跃度 | ⭐⭐⭐⭐⭐ | 24 条 PR/24 小时内，社区贡献者活跃 |
| 响应速度 | ⭐⭐⭐⭐ | 多数 Issue 有及时回应或在 1 天内获得修复 PR |
| 稳定性 | ⭐⭐⭐ | 存在 1 个高严重度未修复 Bug（#3568），多条 PR 修复了安装/运行时崩溃 |
| 社区参与 | ⭐⭐⭐⭐ | 外部贡献者（non-core-team）提交 PR 数量多，说明社区生态健康 |
| 版本节奏 | ⭐⭐⭐ | 无新版本发布，待合并 PR 数量较多（18 条），可能需要一次集中发布 |

**核心建议**：优先处理 #3568（静默失败高严重度），随后合并 #3549 和 #3550（注入/崩溃类），并建议在下一个版本中对 Agi-Asi 的 15 条修复进行回归测试后统一放行。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-27

## 1. 今日速览

项目在过去 24 小时内活跃度**偏低**：仅有 1 条新 Issue 提交，无新 PR、无版本发布，暂未发现代码合并或关闭动作。虽然提交量不多，但新 Issue #995 涉及 Skills 模块对符号链接（Symlink）的支持，触及功能完备性与用户体验层面，属于值得关注的增强请求。整体来看，项目处于**平稳维护期**，社区贡献热度有待提升。

---

## 2. 版本发布

昨日无新版本发布。当前最新版本仍为 `nullclaw 2026.5.29`。

---

## 3. 项目进展

**今日无 PR 合并或关闭，亦无新 PR 提交。**

无代码变更进入主干，项目核心功能推进暂缓。建议维护者关注待处理 PR 积压情况（详见第 8 节），以便保持开发节奏。

---

## 4. 社区热点

**今日唯一活跃 Issue：**

- **[#995 [enhancement] Support Skills Symlinks](https://github.com/nullclaw/nullclaw/issues/995)**
  - 作者：ivostoykov | 创建：2026-08-26 | 评论：0 | 👍：0
  - 内容摘要：请求在 `nullclaw 2026.5.29` 中支持 Skills 目录的符号链接，指出 `nullclaw skills liks`（疑为 `links` 拼写）命令会忽略 symlink，影响技能同步与更新效率。

**分析**：该 Issue 虽暂无评论与点赞，但指出了 Skills 实际使用中的**真实配置场景缺陷**——用户可能通过符号链接管理多个技能仓库或指向外部目录，当前实现无法识别此类链接，限制了灵活性。此需求为**功能增强类**，对使用 git 管理技能库或跨目录复用的用户有直接价值。

---

## 5. Bug 与稳定性

**今日无新 Bug 报告，无崩溃或回归问题出现。** 项目稳定性方面暂无新增风险信号。

> 注：Issue #995 中提及的“symlink 被忽略”可视为功能缺失而非崩溃类 Bug，暂不列入严重性问题。

---

## 6. 功能请求与路线图信号

**新功能需求：** Issue #995 — **支持 Skills 符号链接**

- **动机**：用户希望通过 symlink 实现技能目录的软链接复用，以减少同步操作（原文 `Reduces syncronisation`），并避免使用过时技能副本。
- **实现方向预估**：需在 Skills 扫描/加载逻辑中递归解析符号链接，或提供配置开关控制是否跟随 symlink，同时注意避免循环链接。
- **路线图判断**：该请求优先级中等偏下，但实现成本不高（扫描逻辑局部修改），若能得到社区 +1 支持或补充使用场景，有望进入下一个小版本（如 2026.6.x）。建议维护者在后续版本规划中评估。

---

## 7. 用户反馈摘要

来自 Issue #995 的反馈：

- **真实痛点**：用户使用 `nullclaw 2026.5.29` 管理 skills 时，符号链接被完全忽略，导致无法从 git 仓库或其他目录链接技能。
- **典型使用场景**：多环境共享技能库或将技能目录链接至同步盘/CI 输出目录，通过符号链接减少复制与同步成本。
- **满意度**：隐含对当前功能的**不满意**（功能缺失），但对项目整体无负面情绪，期望通过 enhancement 解决。
- **请求附带细节**：作者希望“拥有该功能”并表述了期望（`It would be great to have this`），无明显迫切性或抱怨语气。

---

## 8. 待处理积压

**今日无新增长时间未响应的 Issue 或 PR。**

但结合历史数据（当前 PR 积压为 0 条开放），建议维护者：

- 关注 **Issue #995** 后续讨论，若一周内无回应，可主动打上 `help wanted` 标签或给出初步实现计划，避免社区反馈石沉大海。
- 定期检查历史遗留的未关闭低活跃 Issue，保持项目健康度透明度。

---

*报告生成时间：2026-08-27 | 数据来源：NullClaw GitHub 仓库*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-27

## 1. 今日速览

IronClaw 今日活跃度极高。过去 24 小时内，项目共产生 27 条 Issue 更新（新开/活跃 18 条，关闭 9 条）和 50 条 PR 更新（合并/关闭 48 条），另有 1 个新的候选版本发布。值得关注的是，今日有大量规模化 PR（标注 `size: XL`）获得合并，涉及文件系统安全加固、容器化部署模式、TUI 终端客户端、MCP 注册框架等多个深度领域，表明项目核心架构层正在加速收敛。同时，社区报告的 Bug 数量也不少，主要集中在性能（MIME 头注入导致的推理成本膨胀）、渠道功能（Telegram 移除 503）和大尺寸轨迹下载失败等方面。总体来看，项目正处于 **v1.4.0 发布前的密集收尾冲刺期**，合并节奏和讨论热度均处于高位。

---

## 2. 版本发布

### ironclaw-v1.4.0-rc.1（2026-08-26）

**发布说明摘要：**

首个 1.4.0 候选版本，覆盖自 `ironclaw-v1.3.0` 以来的 **81 个提交**。

**新增功能：**
- **持久化通知收件箱**：运行（runs）会将权威结果和可操作门禁发布到每个用户的收件箱，通过 WebUI 通知中心呈现，审批和认证提示由此获得了持久化载体。

**迁移与注意事项：**
- 当前为 RC 版本，功能仍可能变动。建议部署在非生产环境先行验证通知收件箱的端到端流程。
- 1.4.0 正式版尚待发布；如从 1.3.x 升级，请关注随正式版发布的完整迁移指南。

来源：[Release 链接](https://github.com/nearai/ironclaw/releases)

---

## 3. 项目进展

今日合并/关闭的 PR 数量高达 48 条，覆盖多个重要功能区块。以下为主要亮点：

| 领域 | PR | 要点 |
|---|---|---|
| **文件系统安全** | [#6817](https://github.com/nearai/ironclaw/pull/6817) (`size: XL`) | 以 fd 根目录遍历方式修复本地后端 **4 个 TOCTOU 逃逸漏洞** — 路径检查与后续系统调用之间不再存在竞态窗口，属于重要的安全加固。 |
| **部署运维** | [#6533](https://github.com/nearai/ironclaw/pull/6533) (`size: XL`) | 新增**容器监督模式**，为托管部署提供容器适配的 restart/apply 路径，并显著改善裸 `os error 2` 报错体验。 |
| **终端体验** | [#6157](https://github.com/nearai/ironclaw/pull/6157) (`size: XL`) | 为 `ironclaw-reborn` 增加 **ratatui 终端客户端 (`tui`)**，作为 WebChat v2 API 的轻量 HTTP+SSE 客户端，使无浏览器环境也能获得完整体验。 |
| **MCP 体系** | [#5970](https://github.com/nearai/ironclaw/pull/5970)、[#5918](https://github.com/nearai/ironclaw/pull/5918)、[#5917](https://github.com/nearai/ironclaw/pull/5917) | MCP 注册框架三连发：**所有者作用域存储 + 注册/发现流程 + 强制宿主出口边界** — 为 MCP 服务器从“声明期能力”转向“运行期发现”奠定了基础。 |
| **Agent 循环解耦** | [#6112](https://github.com/nearai/ironclaw/pull/6112) (`size: XL`) | 分解 `canonical.rs` 的 `execute()` 巨型函数，消除重复延迟包装逻辑，降低后续扩展的维护负担。 |
| **并发修复** | [#6096](https://github.com/nearai/ironclaw/pull/6096) | 修复同一线程快速发送两条消息时**持久化/展示/执行乱序**问题（对应 Issue #6047）。 |
| **OAuth 兼容性** | [#5579](https://github.com/nearai/ironclaw/pull/5579) | 修复 OAuth 栈 4 个 wire-format 兼容性缺陷（如 `"expires_in":"3600"` 字符串类型、DCR 错误体、RFC 8414 可选端点），提升与真实世界 provider 的互操作性。 |
| **生产修复** | [#5742](https://github.com/nearai/ironclaw/pull/5742)、[#5736](https://github.com/nearai/ironclaw/pull/5736) | 修复内存提示上下文未接线共享内存信封加固、本地开发合成能力的重试路径失效两个生产级问题。 |

**评估**：这一批合并在安全性、可部署性、前端交互三个维度同时向前推进，且所有大规模 PR 均标注 `risk: low/medium`，显示工程纪律良好。加上 RC 版本发布，**v1.4.0 正式版预计很快可期**。

---

## 4. 社区热点

### 🔥 热度最高：#7732 Epic — 持久化每用户沙箱 + iron-proxy（10 条评论，持续更新）

- 链接：[Issue #7732](https://github.com/nearai/ironclaw/issues/7732)
- **背景**：Reborn 已将 `builtin.shell` 路由至 Docker 沙箱，但当前实现为“每条命令新建容器”，缺少持久用户工作区。
- **诉求**：构建一个**持久化的、每用户独立的工作计算机**，而非每次 shell 调用都销毁重建的临时环境。Epic 建议将循环执行器延迟至后续版本，优先完成持久化沙箱基础设施。
- **关联信号**：同日新增的 [Issue #7903](https://github.com/nearai/ironclaw/issues/7903)（决策 spike：在可信宿主内核后放置持久化每用户沙箱执行器）正是该 Epic 的局部深入探讨，说明社区和团队对该方向有持续投入。

### 💬 讨论焦点：#7891 — 24 KiB MIME 头致 14.3 秒推理开销（5 条评论）

- 链接：[Issue #7891](https://github.com/nearai/ironclaw/issues/7891)
- **核心事实**：两次 Gmail 读取 API 调用（各约 280 ms）引发一轮 **19.7 秒**的完整回合，其中 **19.2 秒耗费在模型推理**上。原因是 **49,152 字节未做投影的原始 MIME 头被无差别注入提示词**。
- **社区反应**：此问题精准击中“工具输出进上下文的成本控制”这一痛点，与 #7922（apply_patch 改为语法约束自由格式工具）、#7928（有界可选 JSON 视图）等形成合力，显示社区对 **token 经济性** 的强烈关注。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| **高（性能崩溃）** | [#7891](https://github.com/nearai/ironclaw/issues/7891) | 未投影的 MIME 头导致单轮推理成本从秒级膨胀至 19 秒 | 开放中，无 fix PR；#7928 提供方向性解法 |
| **高（功能阻断）** | [#7918](https://github.com/nearai/ironclaw/issues/7918) | 下载高工具调用数轨迹时返回 **HTTP 413 content too large**，阻断示例获取 | 开放中，无 fix PR |
| **中（生产故障）** | [#7912](https://github.com/nearai/ironclaw/issues/7912) | 从 Channels 设置页移除 Telegram 扩展返回 **503** | 开放中，无 fix PR |
| **中（缓存失效）** | [#7921](https://github.com/nearai/ironclaw/issues/7921) | OpenAI 系列后端缺少 `prompt_cache_key`，超过约 200 次调用后缓存命中率从 **~82% 跌至 29%** | 开放中，无 fix PR |
| **低（体验）** | [#7447](https://github.com/nearai/ironclaw/issues/7447) | Agent 在工具调用过多后陷入冗余 fetch-retry 循环，耗尽预算 | 开放中，无 fix PR |

**整体评估**：今日报告的 Bug 大多集中在上层工具结果处理与渠道管理，核心 agent 循环稳定性未出现新问题。但 #7891 和 #7921 均属于 **token 成本/缓存效率类性能隐患**，在长会话和大数据量场景下会显著劣化用户体验，值得优先投入。

---

## 6. 功能请求与路线图信号

| 功能请求 | 链接 | 对应已有工作 | 下一版本可能性 |
|---|---|---|---|
| **持久化通知收件箱** | 已随 v1.4.0-rc.1 发布 | — | ✅ 已落地 |
| **agent.md 人格编辑器（Settings UI）** | [#7895](https://github.com/nearai/ironclaw/issues/7895) | 无直接对应 PR | ⭐ 高（标注 v1.5.0） |
| **Learned-skill 提取配置入口** | [#7920](https://github.com/nearai/ironclaw/issues/7920) | 后端已存在，依赖环境变量 | ⭐ 高（标注 v1.5.0 方向） |
| **有界 JSON 工具结果视图** | [#7928](https://github.com/nearai/ironclaw/pull/7928)（开放 PR） | 直接回应 #7891 | ✅ 极可能进入 1.4.x |
| **Slack 渠道路由个人/团队 Agent** | [#4625](https://github.com/nearai/ironclaw/issues/4625) | 另见 [#7871](https://github.com/nearai/ironclaw/issues/7871)（Slack-to-console bridge Epic） | ⭐ 路线图明确 |
| **Telegram/Slack 群组与个人/机器人区分** | [#7909](https://github.com/nearai/ironclaw/issues/7909) | 无 | 路线图信号（v1.5.0） |
| **上下文管理优化（Epic）** | [#7911](https://github.com/nearai/ironclaw/issues/7911) | 与 #7921/#7891 同属上下文成本议题 | ⭐ 高优先级 |

---

## 7. 用户反馈摘要

来自今日 Issues 评论的真实用户声音：

- **人格设置门槛高**（[#7895](https://github.com/nearai/ironclaw/issues/7895)）：用户在尝试设置 agent 人格时遭遇困难，原始诉求表述为 *"me trying to set up personality with ironclaw"*——说明 CLI/文件方式对非技术用户仍然是障碍，图形化配置成为明确需求。

- **大型轨迹无法下载**（[#7918](https://github.com/nearai/ironclaw/issues/7918)）：*"preventing us from downloading the examples"*——高工具调用数的轨迹文件大小已触及 HTTP 层限制，这属于真实用户在使用高复杂度 Agent 工作流时的现实瓶颈。

- **未投影的大块内容进入提示词**（[#7891](https://github.com/nearai/ironclaw/issues/7891)）：报告者明确指出 *"zero lock contention, zero retries, zero queue delay"*，证明瓶颈完全在提示词构造侧，而非系统侧——用户对根因的定位非常精准，说明社区技术参与度较高。

---

## 8. 待处理积压

以下为长期开放、始终未获回应的关键 Issue/PR，建议维护者关注：

| 类型 | 编号 | 标题 | 持续时间 | 风险/影响 |
|---|---|---|---|---|
| Issue | [#2117](https://github.com/nearai/ironclaw/issues/2117) | ironclaw-bridge — 本地文件/MCP 桥接守护进程 | 自 2026-04-07 起（超 4 个月） | 云托管场景下无法访问本地资源的阻断问题，仍有用户等待；含 👍 1 |
| Epic | [#6369](https://github.com/nearai/ironclaw/issues/6369) | v1 遗留代码退役后的能力缺口追踪 | 自 2026-07-20 起 | 涉及生产迁移后的能力补齐，需确认是否仍有未关闭的子项 |
| Issue | [#7447](https://github.com/nearai/ironclaw/issues/7447) | Agent 工具调用过多后任务失败 | 自 2026-08-10 起 | 直接影响长任务可靠性，已多次被提及但无对应修复 PR |
| PR（开放） | [#7928](https://github.com/nearai/ironclaw/pull/7928) | 有界可选 JSON 结果视图 | 2026-08-27 新开 | 直接回应 #7891 的 token 成本问题，建议优先评审 |

---

> 本日报由 AI 分析师自动生成，基于 IronClaw (github.com/nearai/ironclaw) 公开 GitHub 数据，仅供项目健康度参考。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-27

## 1. 今日速览

LobsterAI 过去 24 小时项目活跃度较高：共产生 2 条新 Issue、16 条 PR 活动，其中 15 条已合并/关闭，仅 1 条待合并，合并效率出色。功能开发集中在分享链路分析、云端文件管理等方向，并伴随一批 UI 细节优化与工程化修复，整体项目推进稳健。今日无新版本发布，用户侧核心诉求集中在**新增聚合服务商 Synthorai 支持**及**波斯语 RTL 文本渲染**两方面。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭 15 条 PR，核心进展集中在以下几个方向：

**分享与部署分析链路（功能增强）**
- [#2555](https://github.com/netease-youdao/LobsterAI/pull/2555) 完善发布与部署分析链路：新增分享、部署、复制链接等结果事件，关联操作与最终结果，记录耗时和错误分类，增加异步部署终态跟踪与可靠上报队列，并补充测试。此项为分享/发布功能的可观测性做出重要补强。
- [#2550](https://github.com/netease-youdao/LobsterAI/pull/2550) 支持永久删除云端分享文件：新增删除接口、IPC 与客户端类型，仅允许删除已停止的分享，需文件名二次确认，删除后同步更新云端列表、状态计数和本地收藏，并处理状态冲突及服务端不兼容场景。

**UI 与交互优化**
- [#2540](https://github.com/netease-youdao/LobsterAI/pull/2540) / [#2542](https://github.com/netease-youdao/LobsterAI/pull/2542) / [#2544](https://github.com/netease-youdao/LobsterAI/pull/2544)：侧边栏资料库图标重新设计并统一风格。
- [#2548](https://github.com/netease-youdao/LobsterAI/pull/2548) 更新设置页面宽度。
- [#2539](https://github.com/netease-youdao/LobsterAI/pull/2539) 用户菜单新增每日积分礼包入口。
- [#2546](https://github.com/netease-youdao/LobsterAI/pull/2546) 修复侧边栏登录引导：延迟启动登录推广提示的自动隐藏计时器，避免与引擎启动浮层冲突。

**工程化与平台修复**
- [#2553](https://github.com/netease-youdao/LobsterAI/pull/2553) 修复智谱图标暗色模式显示。
- [#2543](https://github.com/netease-youdao/LobsterAI/pull/2543) Web 安装器时序诊断修复。
- [#2547](https://github.com/netease-youdao/LobsterAI/pull/2545) 登录引导相关修复。
- [#2556](https://github.com/netease-youdao/LobsterAI/pull/2556) 发布记录文档更新（rlog）。

**待合并（1 条）**
- [#2551](https://github.com/netease-youdao/LobsterAI/pull/2551) 修复应用更新时保留 ready 状态（[OPEN]），涉及 renderer 与 main 双领域，建议关注其合入进展。

总体而言，项目在**分享/发布功能的深度打磨**（分析链路 + 文件生命周期管理）上推进明显，同时维持了高频的 UI 细节迭代节奏。

---

## 4. 社区热点

今日最受关注的 Issue 为 **#2554「新增 Synthorai 作为内置服务商」**（[链接](https://github.com/netease-youdao/LobsterAI/issues/2554)），由用户 `cuihuan` 提交，获 1 条评论。

**核心诉求**：LobsterAI 目前内置 18 家服务商，其中 OpenRouter 已作为聚合类服务商在列。用户希望将 Synthorai（一个 key 打通多家模型的网关）也列入内置服务商，理由如下：
- 内置条目可提供默认模型列表，无需逐个手填 model ID；
- 内置条目支持 `switchableBaseUrls`，可一键切换 Anthropic / OpenAI 双协议 base URL；
- 内置条目在设置页有图标和默认 baseUrl，降低新用户配错（如结尾斜杠）的概率。

该诉求反映了用户对**更完善的聚合类服务商开箱即用体验**的期待，也侧面验证了 OpenRouter 这类内置聚合条目的模式获得认可、值得复制。项目组可评估将此类网关类服务商纳入内置体系的维护成本与收益。

另一条活跃 Issue 为 **#2541 波斯语文本支持**（[链接](https://github.com/netease-youdao/LobsterAI/issues/2541)），关注 RTL 输入、混合双向文本渲染及 ZWNJ 半空格处理，反映出非英语用户群对**国际化文本渲染质量**的需求。

---

## 5. Bug 与稳定性

今日报告并处理的稳定性/缺陷相关问题如下：

| 严重程度 | 问题 | 状态 |
|---------|------|------|
| 中 | **#2546** 侧边栏登录推广提示与引擎启动浮层计时冲突 | ✅ 已合并修复 |
| 低 | **#2553** 智谱图标暗色模式下显示异常（图标可见性问题） | ✅ 已合并修复 |
| 低 | **#2543** Web 安装器时序诊断问题 | ✅ 已合并修复 |
| 中 | **#2551** 应用更新时未保留 ready 状态（可能导致更新后状态丢失） | ⏳ 待合并（[PR #2551](https://github.com/netease-youdao/LobsterAI/pull/2551)） |

未发现崩溃级或数据安全类严重缺陷，整体稳定性良好。

---

## 6. 功能请求与路线图信号

今日收到两条新功能请求：

1. **聚合服务商 Synthorai 纳入内置支持**（[#2554](https://github.com/netease-youdao/LobsterAI/issues/2554)）— 用户明确提出希望将同一 base URL 支持 OpenAI/Anthropic 双协议的网关类服务商内置化。考虑到 LobsterAI 已有 OpenRouter 内置先例且用户认可此模式，已内置 18 家服务商的基础上再次收到此请求，项目组可考虑**建立聚合型服务商的通用接入框架**，而非逐一适配，这将从机制上降低此类需求带来的重复工作量。

2. **波斯语（Farsi）完整文本支持**（[#2541](https://github.com/netease-youdao/LobsterAI/issues/2541)）— 涉及聊天输入框 LTR 方向、混合双向文本渲染及 ZWNJ（零宽不连字符）半空格处理。这是典型的 **i18n/RTL 支持**范畴需求，若项目有国际化路线规划，可将其纳入后续迭代。

结合近期 PR（如登录引导、资料库图标等小步快跑的 UI 优化节奏），下一版本预计继续以体验打磨和平台适配为主，以上两项功能请求大概率不会进入最近一次迭代。

---

## 7. 用户反馈摘要

- **配置痛点**（[#2554](https://github.com/netease-youdao/LobsterAI/issues/2554)）：用户认为 Custom 槽位「能用但不顺心」——没有默认模型列表、没有双协议 base URL 一键切换、没有图标与默认配置，新用户易在 base URL 格式上犯错。这一反馈指向**配置引导与预设模板**的体验优化空间，是聚合服务商场景下的典型痛点。
- **国际化文本需求**（[#2541](https://github.com/netease-youdao/LobsterAI/issues/2541)）：波斯语用户在聊天输入框中遭遇 LTR 光标起始错误、混合波斯语+英语段落渲染错乱等问题，属于**非拉丁语系用户的基本可用性**问题，对面向全球用户的产品有参考价值。
- 今日无用户明确表达不满或投诉的负面反馈，社区情绪整体平稳。

---

## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 备注 |
|------|------|---------|------|
| [#2541](https://github.com/netease-youdao/LobsterAI/issues/2541) 波斯语 RTL 文本支持 | Issue | 2026-08-26 | 尚无相关 PR 认领，建议确认是否为国际化路线中的已知缺口 |
| [#2554](https://github.com/netease-youdao/LobsterAI/issues/2554) 新增 Synthorai 内置服务商 | Issue | 2026-08-26 | 建议评估聚合型服务商通用接入方案，避免逐家适配 |
| [#2551](https://github.com/netease-youdao/LobsterAI/pull/2551) 应用更新保留 ready 状态 | PR | 2026-08-26 | 已停留 1 天未合入（当日唯一待合并 PR），涉及更新机制稳定性，建议优先 review |

今日无长期未响应（超 7 天）的遗留积压项，项目响应及时性良好。以上两条新 Issue 均为昨日创建、已获初步讨论，项目组可按优先级排期跟进。

---

**健康度总评**：合入率高（15/16）、缺陷响应快、无长期积压、功能开发与 UI 打磨并行推进，项目处于健康活跃的迭代周期，建议持续维持当前节奏并关注聚合服务商需求背后的平台化机会。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 — 2026-08-27

## 今日速览

Moltis 项目今日活跃度适中，各项关键指标处于健康区间。过去24小时内，1个历史遗留的 Bug Issue 得到关闭，2个 Pull Request 被合并，其中1个直接对应上述 Bug 的修复；另有1个新的 Fastmail MCP OAuth 范围注册修复落地，系昨日新建、当日即合并的高效迭代。新版本 `20260826.01` 同日发布，包含上述修复。总体而言，项目正保持稳定的小步快跑节奏，反馈闭环迅速。

---

## 版本发布

### 20260826.01
- **发布时间**: 2026-08-26
- **关联变更**: 包含今日合并的 PR #1104（De-Preferring Models 修复）与 PR #1244（Fastmail MCP OAuth 修复）
- **破坏性变更**: 推测无破坏性变更。PR #1104 在修改行为的同时补充了 backend 与 Playwright 回归测试，且为修复已报告的 Bug，属于行为修正而非变更；但使用 **“清空偏好设置”** 功能的用户需知，该操作现在会同时移除已保存的 provider 模型偏好（此前可能静默失败）。
- **迁移注意**: 暂无特殊迁移要求。OAuth 相关修复涉及 Fastmail MCP 服务发现与新客户端注册过程，使用 Fastmail MCP 的用户建议升级后重新触发一次 OAuth 授权流程以确保以正确的 scope 重新注册客户端。

---

## 项目进展

今日合并的 2 个 PR 均与修复已有功能缺陷有关，没有新功能合入，但巩固了两处基础能力：

- **PR #1104 — fix(providers): allow replacing preferred models**  
  合并前，用户在“偏好模型”对话框中无法真正替换或清除已保存的 provider 模型偏好：对话框虽然保存了新选择，但底层并未正确替换之前的偏好记录，导致模型“去偏好化”（de-preferring）操作失效。此 PR 修复了该逻辑，并为保存、替换、清空三种路径补齐了 backend 与 Playwright 回归测试。该修复直接关闭了 3 个月前报告的 Issue #1094。
  [查看 PR](https://github.com/moltis-org/moltis/pull/1104)

- **PR #1244 — Fix Fastmail MCP OAuth scope registration**  
  修复 MCP OAuth 发现流程中对受保护资源 scope 的偏好处理：现在更倾向于使用资源端声明的 scope，而非采用授权服务器提供的更宽泛的 scope 目录；同时将所选 scope 纳入 RFC 7591 动态客户端注册。新增 Fastmail 场景的回归测试，覆盖资源发现、注册与 localhost 重定向。
  [查看 PR](https://github.com/moltis-org/moltis/pull/1244)

两个修复均配对了针对性回归测试，项目代码质量维护意识良好。相较昨日，项目在**模型偏好管理可靠性**与**MCP OAuth 互操作性**两个维度有所推进。

---

## 社区热点

今日无高热度讨论。唯一活跃条目是关闭状态下的 **Issue #1094**（De-Preferring Models Bug），该条 6 月 3 日提出，期间无评论，今日随修复关闭。尽管无互动数据，但该问题从报告到修复历时近 3 个月，反映出此前对模型偏好管理这一边缘功能投入不足——修复后社区对模型切换工作流的信心应有提升。
[查看 Issue](https://github.com/moltis-org/moltis/issues/1094)

---

## Bug 与稳定性

- **[中] 模型偏好无法替换/清除（Issue #1094）** — 已关闭，修复 PR #1104 已合并并于 v20260826.01 发布。影响用户保存、替换、清空模型偏好列表的核心操作。
  [Issue 链接](https://github.com/moltis-org/moltis/issues/1094)

- **[中] Fastmail MCP OAuth 授权范围注册异常（PR #1244）** — 已修复合并。若 Fastmail MCP 的 OAuth 发现结果中含多个 scope 目录，客户端可能会错误地注册更宽泛的 scope，可导致授权请求与资源要求不匹配。已通过优先采用受保护资源 scope 的策略解决。
  [PR 链接](https://github.com/moltis-org/moltis/pull/1244)

无新增未决 Bug、崩溃或回归报告。

---

## 功能请求与路线图信号

过去 24 小时没有新的功能请求提交。从已合并 PR 可观察到的两个路线图信号：

- **MCP 生态集成深化**：PR #1244 对 MCP OAuth 流程的精细化修整（scope 发现优先级、动态客户端注册合规），表明 Fastmail 相关 MCP 集成正处于打磨阶段，且维护者重视 OAuth 标准合规性，预计后续 MCP provider 相关迭代将以标准合规为基础。
- **模型偏好管理精细化**：PR #1104 的修复意味着模型选择工作流正在趋于完善。叠加此前保存 provider 偏好的功能，下一步可能的方向是**偏好作用域细化**（会话级 vs 全局级、按任务类型区分）。

---

## 用户反馈摘要

今日仅有 Issue #1094 的提出者（RokkuCode）作为反馈来源，且该 Bug 无评论互动。从提交内容推测用户场景：用户在打开偏好的模型对话框后，尝试取消选择或替换已保存的模型，但保存后设置未生效，导致无法真正“去偏好”某个模型。该问题持续 3 个月未被发现，侧面反映该项功能使用频率较低，或此前用户通过其他方式（如编辑配置文件）绕行。修复已发布，若用户仍有问题，预计后续会有新 Issue 提出。

---

## 待处理积压

- **无长期未处理的高优先级项目**。当前 0 个已合并待发布 PR（均随 v20260826.01 发布），0 个未合并 PR。
- 值得关注的是：Issue #1094 从报告到关闭历时 84 天。尽管这期间可能有内部排期，但用户侧无任何维护者响应记录，若类似问题再次出现，建议维护者至少给予初步回复（如“已确认，计划修复”）以避免用户长期静默等待。

---

*报告生成时间：2026-08-27 | 数据来源：Moltis GitHub 仓库（github.com/moltis-org/moltis）*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-27

**数据统计：** Issues 33 条（新开/活跃 18，关闭 15） · PR 45 条（待合并 17，已合并/关闭 28） · 新版本 1 个


## 1. 今日速览

CoPaw 项目今日维持高活跃度，24小时内产生了78条 Issue/PR 动态，且合并/关闭比例超过 60%（28/45），表明维护团队响应迅速、交付效率高。**核心看点**：v2.2.0-beta.1 发布，标志着多租户 Hub 版本进入 Beta 阶段；社区对多用户/团队协作的需求呼声持续走高，并已在版本规划中得到官方确认。与此同时，桌面端稳定性问题（任务卡死、安装阻塞、工具失效）和移动端体验优化成为今日社区反馈的两大焦点，对应修复 PR 已全部就绪或合入。


## 2. 版本发布

### v2.2.0-beta.1

- **📄 文档**：更新 scroll context manager 博客（PR #7300）
- **🔧 修复**：sanitize DashScope tool schemas，兼容 strict models（PR #7284）
- **🧪 测试**：新增定向集成测试

> **迁移注意**：该版本为 2.2 系列首个 Beta，主要引入多租户 Hub 基础能力（对齐 Issue #7318），建议团队用户提前验证多用户场景兼容性。完整 changelog 将在正式版发布时补齐。


## 3. 项目进展

今日合入的 PR 集中在四个方向，整体推进约 2~3 个百分点的测试覆盖率（累计 +10.5pp 以上）：

**稳定性与生命周期**
- [#7194 fix(workspace): startup failure cleanup cancellation-safe](https://github.com/agentscope-ai/QwenPaw/pull/7194) — 重构 workspace 启动/重载清理逻辑，避免部分初始化服务残留
- [#7319 refactor(console): track background agent runs](https://github.com/agentscope-ai/QwenPaw/pull/7319) — 后台任务接入 TaskTracker，支持状态追踪、停止与重载

**安装与 CI**
- [#7323 fix(installer): ignore NSIS caller during process checks](https://github.com/agentscope-ai/QwenPaw/pull/7323) — 修复 NSIS 卸载器误报文件占用，配合 [#6810 安装阻塞修复](https://github.com/agentscope-ai/QwenPaw/issues/6810)
- [#7293 / #7326 CI 分片](https://github.com/agentscope-ai/QwenPaw/pull/7293) + [#7326](https://github.com/agentscope-ai/QwenPaw/pull/7326) — 集成测试与夜间 E2E 按优先级分三片并行，显著缩短 CI 耗时

**测试覆盖率**
- [#7292 +5.02pp 后端单测](https://github.com/agentscope-ai/QwenPaw/pull/7292)（58.04% → 63.06%，新增 1,148 个测试）
- [#7325 +5.49pp Console 前端单测](https://github.com/agentscope-ai/QwenPaw/pull/7325)（+382 用例）
- [#7327 Console E2E 增强](https://github.com/agentscope-ai/QwenPaw/pull/7327)（新增 23 用例，预计 +6~7pp）

**工具链与数据**
- [#7190 qwenpaw-data PyPI 运行时路径](https://github.com/agentscope-ai/QwenPaw/pull/7190) — 支持 `pip install qwenpaw[qwenpaw-data]` 独立安装，附 docker-compose 演示栈


## 4. 社区热点

### 🔥 最热讨论：#6921 任务中途无提示停止
- **链接**: [Issue #6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)
- **动态**: 11 条评论，持续 15 天仍开放
- **诉求**: 多步骤任务执行时，模型在输出“Now 2.1, 3.1, 3.2. Let me do all three.”等规划性消息后无提示停止，需用户手动输入“继续”才恢复。用户已定位到大模型输出特征，说明问题可复现且与模型规划/工具调用衔接相关。
- **分析**: 这是今日最影响用户体验的 Bug，涉及 LLM 早期停止与工具调用调度的边界问题，需重点关注后续修复进展。

### 🔥 多租户功能呼声：#7318 官方发起路线图讨论
- **链接**: [Issue #7318](https://github.com/agentscope-ai/QwenPaw/issues/7318)
- **动态**: 官方（rayrayraykk）发布 2.2.0 多租户 Hub 预告，征集社区建议
- **关联**: 链接到 #2324、#5780、#4702、#6335 等多条历史需求
- **分析**: 多用户/团队协作是社区长期以来的最大诉求之一（自上月以来 #5780、#4702、#6335 陆续关闭，均与多租户相关），官方已明确纳入 2.2.0 路线图。企业用户可重点关注。


## 5. Bug 与稳定性

### 🔴 严重

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| 🔴 | [#7311](https://github.com/agentscope-ai/QwenPaw/issues/7311) | v2.1.1b2 缺少 `_qwenpaw_remote_backend` 模块，**所有工具不可用** | 开放，未指派，需紧急响应 |
| 🔴 | [#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) | 桌面端/Docker 捆绑 OpenSSL 3.0.x，运营商 DPI 重置 TLS 握手，无规避方案 | ✅ [#7328](https://github.com/agentscope-ai/QwenPaw/pull/7328) 已提 PR：Python 3.11 → 3.13，OpenSSL 3.5.x |
| 🟠 | [#7335](https://github.com/agentscope-ai/QwenPaw/issues/7335) | Prompt cache 命中率仅 81.68%（对标 OpenCode 96.02%），直接影响成本 | 开放，标记 good first issue |

### 🟡 中等

| Issue | 描述 | 状态 |
|-------|------|------|
| [#7258](https://github.com/agentscope-ai/QwenPaw/issues/7258) | 微信频道“不显示思考过程”设置无效 | ✅ 已关闭 |
| [#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206) | v2.1.1-beta.1 `/compact` 在 ratio=0.9 时必现 pydantic ValidationError（回归） | ✅ 已关闭 |
| [#7212](https://github.com/agentscope-ai/QwenPaw/issues/7212) | 超限图片导致请求崩溃而非优雅降级 | ✅ 已关闭 |
| [#7321](https://github.com/agentscope-ai/QwenPaw/issues/7321) | 工具调用已结束但界面仍显示“执行中” | 开放，视觉状态同步 bug，与 #7319 重构相关 |
| [#7310](https://github.com/agentscope-ai/QwenPaw/issues/7310) | datapaw 插件运行时缺失导致启动报错、应用卡死 | 开放，临时方案为禁用插件 |
| [#7324](https://github.com/agentscope-ai/QwenPaw/issues/7324) | 定时任务成功后收件箱推送消息丢失（3 条中缺 1 条） | 开放 |

### 🟢 轻微 / 体验类

| Issue | 描述 | 状态 |
|-------|------|------|
| [#7282](https://github.com/agentscope-ai/QwenPaw/issues/7282) | Console Markdown 列表垂直间距过大 | ✅ 已关闭 |
| [#7306](https://github.com/agentscope-ai/QwenPaw/issues/7306) | 输入框多行时焦点自动下移一行 | 开放 |
| [#7229](https://github.com/agentscope-ai/QwenPaw/issues/7229) | 本地测试运行器跳套件且误报成功 | ✅ [#7250](https://github.com/agentscope-ai/QwenPaw/pull/7250) 已合并修复 |


## 6. 功能请求与路线图信号

### 🎯 明确进入 2.2.0 路线图
- **QwenPaw Hub 多租户版**（[#7318](https://github.com/agentscope-ai/QwenPaw/issues/7318) 官方确认）— 涵盖 #5780、#4702、#6335 等多条历史企业需求，预计支持多用户管理、RBAC 权限控制

### 🚀 高可能性纳入（已有对应 PR）

| 功能需求 | 对应 PR | 说明 |
|----------|---------|------|
| **关闭流式生成自动滚动**（[#7339](https://github.com/agentscope-ai/QwenPaw/issues/7339)） | [#7340 feat(console): add chat scroll lock](https://github.com/agentscope-ai/QwenPaw/pull/7340) | 用户要求锁定视口，PR 已提交 |
| **移动端输入体验优化** | [#7334 fix(chat): improve mobile composer controls](https://github.com/agentscope-ai/QwenPaw/pull/7334) | 44px 统一按钮、底部抽屉控件 |
| **自定义提供商模型自动发现**（#7305） | [#7320 fix(provider): restore automatic model discovery](https://github.com/agentscope-ai/QwenPaw/pull/7320) | 修复 /models 发现结果不可用 |

### 💡 值得关注的新方向
- **OpenViking 长期记忆后端**（[#7252](https://github.com/agentscope-ai/QwenPaw/issues/7252)）— 用户希望基于现有 MemoryMiddleware 架构接入 OpenViking，正等待官方方向确认
- **MCP Streamable-HTTP 双协议客户端**（[#7330](https://github.com/agentscope-ai/QwenPaw/pull/7330)）— 支持 2026-07-28 新协议并回退兼容旧版，体现前瞻性
- **Prompt cache 可观测性**（[#7335](https://github.com/agentscope-ai/QwenPaw/issues/7335)）— 记录与展示命中率、提供优化建议
- **钉钉群聊上下文模式可配置**（[#7158](https://github.com/agentscope-ai/QwenPaw/issues/7158)）— 支持群聊共享/隔离上下文切换（功能已实现并被关闭）

### 🔮 已在今日 PR 中体现的其他方向
- **大工具结果上下文管控**（[#7331](https://github.com/agentscope-ai/QwenPaw/pull/7331)）— 超长单行工具结果截断前先落盘为 artifact，避免上下文膨胀
- **未知模型输出限制容错**（[#7337](https://github.com/agentscope-ai/QwenPaw/pull/7337)）— 不再默认注入 8192 tokens 上限
- **DashScope strict 模型 schema 兼容**（[#7284](https://github.com/agentscope-ai/QwenPaw/pull/7284)）— 已在 v2.2.0-beta.1 中发布


## 7. 用户反馈摘要

**核心痛点**

1. **任务卡死需手动“继续”**（#6921，11 评论）— 用户 rerbin 多次报告同一问题，已定位到模型输出特征，严重影响多步骤任务体验。该用户高频提交高质量反馈（今日 6 条 Issue），是社区最活跃的贡献者之一。
2. **移动端操作不便**（#7177）— 网页版部署首页操作入口位置不合理，手机端“停止运行”按钮误触风险高，用户反馈“每次操作都很紧张”。
3. **多行输入焦点漂移**（#7306）— Win10 桌面端输入框多行时焦点自动下移一行，影响长文本输入。
4. **后台任务列表不自动清除**（#7280）— 已完成任务残留列表中，用户不理解设计初衷，建议增加自动清除开关。
5. **选项选择需手动输入而非弹窗点选**（#7279）— 用户对比 Heremes 的点选体验，希望模型返回多选项时弹窗点选。
6. **文件上传分类逻辑混乱**（#7322）— Web 控制台选择知识库/日记分类后上传文件，实际落到工作区根目录，用户质疑“是 BUG 还是设计如此”。

**满意度信号**

- 用户 rerbin 在 #7177（平台首页优化，已关闭）中反馈的多个改进建议得到采纳，说明官方重视社区反馈闭环。
- 多租户功能从社区呼声到官方路线图，用户等待周期约 3 个月（#5780 于 7/5 提出 → 8/26 官方预告），反馈渠道运转有效。


## 8. 待处理积压

| 类型 | 编号 | 描述 | 待处理时长 | 建议 |
|------|------|------|------------|------|
| 🐛 Bug | [#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) | 任务中途无提示停止（需说“继续”才恢复） | 15 天，11 评论 | 高优先级，建议指派专人排查 LLM 停止与工具调度衔接逻辑 |
| 🐛 Bug | [#7311](https://github.com/agentscope-ai/QwenPaw/issues/7311) | v2.1.1b2 缺少 `_qwenpaw_remote_backend` 模块，所有工具不可用 | 1 天 | 紧急修复或提供 workaround |
| 🐛 Bug | [#7298](https://github.com/agentscope-ai/QwenPaw/issues/7298) | 运营商 DPI 重置 TLS 握手（OpenSSL 3.0.x） | 2 天 | ✅ PR #7328 待合入，需 CI 验证 |
| 🐛 Bug | [#7296](https://github.com/agentscope-ai/QwenPaw/issues/7296) | OpenAI Responses 多轮对话报 400 “reasoning item expired”（无状态上游） | 2 天 | 需确认上游协议兼容策略 |
| 💡 Feature | [#7252](https://github.com/agentscope-ai/QwenPaw/issues/7252) | OpenViking 长期记忆后端方向确认 | 3 天，等待回复 | 建议维护者明确表态或引导至 RFC 流程 |
| 💡 Feature | [#7335](https://github.com/agentscope-ai/QwenPaw/issues/7335) | Prompt cache 可观测性（good first issue） | 1 天 | 可引导新贡献者参与，已有数据支撑 |


> **日报编制时间**：2026-08-27 · 数据来源：[CoPaw GitHub Repository](https://github.com/agentscope-ai/CoPaw)，基于 issues、PRs、releases 动态自动聚合生成。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报

**日期：2026-08-27** | **数据来源：GitHub (zeroclaw-labs/zeroclaw)** | **分析周期：过去 24 小时**


## 1. 今日速览

ZeroClaw 在过去 24 小时内保持**高活跃度**，日均 Issue 更新 26 条（其中新开/活跃 21 条），PR 更新 50 条（其中 47 条仍待合并）。今日最值得关注的动态是**两项已被接受的高优先级 RFC 正式进入实施跟踪阶段**：Gemini Live 实时语音通道（#8780）和会话级持久化提示附件（#9998）分别创建了对应的实施 tracker（#10406、#10405）。此外，2 项此前悬置的修复（频道注册表清理 #9591、Webhook 认证边界 #9587）已被关闭，标志着相关修复的落地。项目整体正处于 **v0.8.5 稳定化冲刺**（截至 8 月 30 日）与 **v0.9.0 重大发布预研**并行的关键阶段。


## 2. 版本发布

本日无新版本发布。


## 3. 项目进展

### 今日合并/关闭的关键 PR 与 Issue

| 项目 | 类型 | 说明 |
|---|---|---|
| **PR #9725** — fix(channels): clear delivery registry when reload removes all channels | 已合并/关闭 | 此修复解决了频道重载移除所有频道后，交付注册表残留过期条目的问题，避免了幽灵投递，对应 Issue #9591 同步关闭 |
| **Issue #9587** — refactor(gateway): require authenticated webhook ingress before agent dispatch | 已关闭 | 该重构要求所有入站 Webhook 必须经过明确的认证入口边界才能调用 agent 分发，修复了 #9565 发现的三个 Webhook 处理器可被未认证消息利用的安全漏洞 |
| **Issue #10103** — ZeroCode Health 状态值在法语/西班牙语下对齐错位 | 已关闭 | 标签宽度硬编码为 11 字符导致的 i18n 显示问题已修复（S3 级） |
| **Issue #10396** — reasoning_content 在每条历史消息中被重放 | 已关闭 | OpenAI 模型提供器只在最新消息中传递推理内容的修复已合入，避免了推理上下文不必要的膨胀 |

### 整体进度

今日新开 2 个实施跟踪器（#10406、#10405），标志着**两个 RFC 正式进入落地阶段**。同时，v0.8.5 稳定化线（#9459）持续运营中，ZeroCode 整合加固（#9010）和 v0.9.0 认证/安全/网关变更队列（#7432）也保持活跃。


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 热度分析 |
|---|---|---|---|
| 1 | **#8780** — RFC: Realtime speech-to-speech channel for Gemini Live | 21 条 | 最热门议题。提案已修订至 v2，改为 broker 合同模式。该 RFC 已被正式接受（status: accepted），今日创建了实施 tracker #10406。社区对语音交互通道的关注度极高，且需求明确要求 Gemini Live 作为首个实现目标 |
| 2 | **#8692** — [Tracker]: Maintainer decision queue for RFCs and design issues | 14 条 | 维护者决策队列 tracker，持续收集需要维护者裁决的 RFC 与设计议题，目前仍有较高评论活跃度 |
| 3 | **#9600** — [Tracker]: Session-persistence contract ownership and layer ordering | 13 条 | 会话持久化合同归属问题。四个独立工作流同时修改同一合同但无明确负责人，社区对此表达了关注 |
| 4 | **#6996** — RFC: Granular sandbox policy — filesystem and network restrictions | 12 条 | 沙箱细粒度策略的 RFC 讨论热度持续，涉及应用层路径准入与 OS 层沙箱后端（Bubblewrap/Landlock/Seatbelt）的策略对齐问题 |

**社区诉求分析**：热点议题集中在**架构级决策**与**安全边界**两个方向。语音通道和会话持久化显示了社区对更丰富交互方式与更可靠记忆的需求；沙箱策略与 Webhook 认证则反映出对安全加固的持续关注。


## 5. Bug 与稳定性

按严重程度排列：

| 严重级别 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| **S0 - 数据丢失/安全风险** | **#10379** — Unable to cancel ongoing message & request for message queuing in ZeroClaw Desktop | 取消按钮被禁用/不可点击，无法终止正在进行的 AI 处理，且输入框在等待期间被锁定，可能导致数据丢失 | ⚠️ 暂无 fix PR |
| **S1 - 工作流阻塞** | #10230 — Daemon startup or reload can overflow during agent initialization | 应用 Quickstart 配置时可能触发 Tokio runtime worker 栈溢出，需复现（r:needs-repro） | ⚠️ 暂无 fix PR |
| **S1 - 工作流阻塞** | #9591 — Channel delivery registry 残留问题 | 重载移除所有频道后注册表保留过期条目 | ✅ 已修复（PR #9725 合入，Issue 已关闭） |
| **S2 - 行为降级** | #10390 — Entering an inactive Chat pane blocks ZeroCode navigation | 进入 Chat 面板会同步等待初始化，阻塞全局导航 | 状态 in-progress，暂无独立 fix PR |
| **S2 - 行为降级** | #10349 — SOP pane loading blocks ZeroCode navigation | 与上一个问题同族，RPC 挂起期间 ZeroCode 停止渲染和键盘输入 | 状态 in-progress |
| **S2 - 行为降级** | #10186 — Terminal fallback text bypasses live delivery seams | 工具调用协议重试耗尽后的兜底文本绕过实时投递合同 | ⚠️ 暂无 fix PR |
| **S3 - 次要问题** | #10103 — 法语/西班牙语下健康状态值对齐错位 | i18n 标签宽度问题 | ✅ 已修复并关闭 |

**零日安全风险**：PR #10070（file_download SSRF 加固）仍处于 blocked 状态，需维护者解除阻塞；PR #10367（技能安装符号链接竞态修复）正在等待维护者审查。


## 6. 功能请求与路线图信号

| 功能请求 | 对应 Issue/PR | 路线图信号 |
|---|---|---|
| **Gemini Live 实时语音转语音通道** | #8780 (RFC，已接受) → #10406 (实施 tracker) | ✅ 已明确纳入路线图，进入实施阶段 |
| **会话级持久化提示附件** | #9998 (RFC，已接受) → #10405 (实施 tracker) | ✅ 已明确纳入路线图，进入实施阶段 |
| **可配置 Telegram 未授权发送者提示** | #10400 | 🔶 新提出，状态 in-progress，可能进入下一版本 |
| **ZeroCode 支持点击 URL** | #10298 | 🔶 状态 in-progress，为 TUI 体验改进 |
| **PR 审查证据与作者操作边界澄清** | #10366 (RFC) | 🔶 正在修订，涉及 CI 流程改进 |
| **Microsoft Teams 频道** | #9241 (PR) | 🔶 大 PR（XL）持续开放中，需作者操作，存在较多审查反馈 |
| **ZeroRelay 安全传输（盲中继 + mTLS）** | #10142 (PR) | 🔶 大型安全基础设施 PR，需维护者审查 |


## 7. 用户反馈摘要

### 真实痛点

1. **ZeroCode TUI 导航阻塞**（#10349、#10390）：用户反馈进入 Chat 或 SOP 面板时，界面会同步等待 RPC 响应，期间无法操作。在 Chat 处于可重试的非活动状态时，`switch_mode()` 会阻塞等待 `Chat::refresh_if_inactive` 完成，导致体验劣化。

2. **ZeroClaw Desktop 无法取消进行中的消息**（#10379）：用户明确表示 UI 中有取消/停止按钮但不可点击，输入框被锁定，请求无法终止。这已升级为 S0 级别（数据丢失/安全风险）。

3. **MCP 工具结果存储冗余**（#10394）：开发者在审查代码时发现 `McpRegistry::call_tool` 将完整 `CallToolResult` 信封序列化存库，而 FastMCP 服务器同时返回 `content[].text` 和 `structuredContent` 时会重复存储，造成每份 payload 双倍占用。

4. **推理内容在历史消息中被重放**（#10396）：用户在对话中发现每次请求都会重新发送所有已完成的思考内容，既浪费 token 也向模型传递了过时的推理状态。

5. **MCP 服务器启动三次**（#10346）：有用户指出 `stdio` 传输的 MCP 服务器在每次启动时被连接/生成三次而非一次，尽管后续不会重新触发。

6. **多会话中目标和约束丢失**（#9998）：用户报告在历史截断或守护进程重启后，会话早期建立的目标和约束容易丢失，尤其是并行会话时问题最为显著。

### 值得注意的正面反馈

#9591 频道注册表残留问题的修复获得了社区确认，该问题此前可能导致频道重载后在不应投递时继续投递消息（S1）。


## 8. 待处理积压

### 长期未响应或阻塞的重要事项

| 项目 | 类型 | 等待时长 | 状态 | 建议 |
|---|---|---|---|---|
| **PR #10070** — feat(tools): gate file_download against SSRF with private-host opt-in | PR | 自 8/18 开放，已 9 天 | **status: blocked / do-not-merge**，XL 尺寸 | SSRF 安全加固的首个切片，阻塞了后续 #10072、#10075 两个堆叠 PR。建议维护者尽快介入解除阻塞或给出明确方向 |
| **PR #8965** — feat(skills): declarative auto-activation with provider switch and image-turn tool blocking | PR | 自 7/11 开放，已 47 天 | needs-author-action，XL 尺寸，依赖的基础已合入 | 该 PR 已重新堆叠到最新 master，等待作者响应上游审查意见 |
| **PR #9222** — feat(eval): per-dimension LLM-judge grader, diagnostic until calibrated | PR | 自 7/20 开放，已 38 天 | needs-author-action，XL 尺寸 | 评估器功能，设计上刻意诊断优先以防误判影响构建，但长时间停滞会拖累整体评估能力建设 |
| **PR #9248** — feat(eval): append-only run-history receipts | PR | 自 7/21 开放，已 37 天 | needs-author-action，XL 尺寸 | 同为 eval 体系的基础设施，与 #9222 同作者，建议一并跟进 |
| **PR #10142** — feat(zerorelay): secure transport with blind relay and native mTLS enrollment | PR | 自 8/19 开放，已 8 天 | needs-maintainer-review，XL 尺寸 | 大型安全传输架构 PR，替代 #9080。安全敏感且影响面广，建议优先安排审查 |
| **PR #10367** — fix(skills): prevent symlink races during install | PR | 自 8/25 开放，已 2 天 | needs-maintainer-review，risk: high | 安全修复（符号链接竞态），建议尽快审查合入 |
| **Issue #8692** — [Tracker]: Maintainer decision queue | Tracker | 自 7/4 运行至今 | 活跃，14 条评论 | 决策队列中的积压项应定期批量处理，避免成为无底洞 |

### 积压信号总结

当前最关键的积压集中在 **SSRF 加固 PR 链**（#10070 → #10072 → #10075），三项堆叠但 Base PR 仍处于 blocked 状态，这直接推迟了文件下载工具的安全加固进度。同时，**eval 体系的两项大型 PR**（#9222、#9248）已停滞一个月以上，需要维护者推动作者继续响应。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*