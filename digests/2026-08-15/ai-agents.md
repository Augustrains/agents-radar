# OpenClaw 生态日报 2026-08-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-15 00:30 UTC

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

# OpenClaw 项目动态日报 — 2026-08-15

## 1. 今日速览

过去24小时，OpenClaw 项目保持非常高的活跃度：共更新 500 条 Issue 和 500 条 PR，其中新增/活跃 Issue 489 条，待合并 PR 405 条。今日无新版本发布。最受关注的 Issue #121058（静默回复失败反复出现）在 #116277 关闭后仍持续复现，已积累 94 条评论，社区关注度显著。同时，多个 P0/P1 级稳定性问题（内存泄漏、CPU 占用飙升、消息静默丢失）仍在积压中，修复 PR 多数处于待合并状态，项目整体处于"高活跃、高积压"状态。虽然今日无发布，但 PR 侧出现了多笔测试精简和重构提交（#123903、#123902、#123895），说明维护者正在着力改善代码库健康状况。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭了 95 个 PR，亮点包括：

- **#116489 (已合并)** — `feat(security): require acknowledgement for install policy warnings`：为安装策略警告引入确认机制，外部 `security.installPolicy` 命令可返回 `warn`，支持授权操作者在继续安装前审查可疑插件/技能的风险信息。这是安全边界上的重要增强。
- **#120981 (已关闭)** — `fix(sessions): preserve transcript ownership after key canonicalization`：修复了会话密钥规范化后，陈旧 transport-specific 会话密钥导致创建重复 `session_nodes` 占位符、破坏会话归属的问题。
- **#123895 (已关闭)** — `refactor(gateway): consolidate pairing completion tests`：合并分散的配对完成测试，移除冗余/模拟测试，收紧测试覆盖。
- **#123863 (已关闭)** — `fix(memory): report truthful index outcomes for empty workspaces`：修复空工作区执行 `memory index` 时误报成功的问题，现在会如实反馈缺少 `memory/` 目录。

此外，多位维护者（`steipete`、`clawsweeper`）提交了多笔测试精简和重构 PR（#123903、#123902、#123896 等），表明项目在功能迭代的同时，也在积极清理技术债和重复测试，整体代码库健康度在持续改善。

## 4. 社区热点

1. **[#121058] Silent reply failures still recurring after #116277 closed** — 94 条评论，0 👍
   链接：https://github.com/openclaw/openclaw/issues/121058

   这是今日最热 Issue。用户报告 #116277 关闭后静默回复故障依然不断发生，监控 cron 持续记录到新案例（含今日 2026-08-09 一条）。核心诉求是：**问题被关闭了，但实际问题没有解决**。社区对"关闭≠修复"的现象表达强烈不满，维护者需要重新打开此 Issue 或给出明确的解决时间表。

2. **[#91588] Gateway 内存泄漏 — RSS 从 350MB 膨胀至 15.5GB** — 24 条评论，1 👍
   链接：https://github.com/openclaw/openclaw/issues/91588

   长期存在的 P0 问题。Gateway 进程 2-3 天内从 ~350MB 膨胀至 15.5GB 后被杀，引发反复 `launchd-handoff` 重启循环。已标记 `clawsweeper:no-new-fix-pr`，长时间无修复 PR，社区持续关注。

3. **[#91009] Codex PreToolUse hook 产生 CPU 密集型进程并阻塞 Gateway RPC** — 20 条评论，2 👍
   链接：https://github.com/openclaw/openclaw/issues/91009

   Codex 工具调用可能触发多个短生命周期 `openclaw-hooks` 进程，每个消耗 100%+ CPU，阻塞 Gateway RPC。作为 P1 问题，同样标注 `clawsweeper:no-new-fix-pr`，迟迟没有修复方案。

4. **[#48003] Steer 模式无法在主线会话中途注入消息** — 19 条评论，4 👍
   链接：https://github.com/openclaw/openclaw/issues/48003

   P1 级别，已有根因分析（`9889c6da5` 引入的 `KeyedAsyncQueue` 回归）。有 4 个 👍，用户期待度高，但当前仅标记 `clawsweeper:linked-pr-open`，进展有限。

## 5. Bug 与稳定性

### 🔴 P0 级

- **[#91588] Gateway 内存泄漏导致 OOM 崩溃**（6月9日创建，至今无修复 PR）
  链接：https://github.com/openclaw/openclaw/issues/91588

- **[#48920] Live Docs 领先于发布版本**（3月17日创建，P0 发布阻断）
  链接：https://github.com/openclaw/openclaw/issues/48920
  Docs 中的 `IsolatedSessions` 配置在最新版 2026.3.13 中不存在，用户按文档操作即报错。

- **[#119270] 文件工具剥离目标路径前导 @ 符号，静默写入/删除错误文件**（8月4日创建，P0，已标记 `clawsweeper:bulk-filed`）
  链接：https://github.com/openclaw/openclaw/issues/119270

### 🟠 P1 级（重点）

- **[#121953] Cron agent 在 DeepSeek 上因 `[cron:...]` 前缀被降优先级而停滞**
  链接：https://github.com/openclaw/openclaw/issues/121953
  DeepSeek API 对以 `[cron:` 开头的首条用户消息使用较低优先级 edge 服务，导致 cron 任务停滞数十秒到数分钟。已有相关 PR（`clawsweeper:linked-pr-open`）。

- **[#91009] Codex PreToolUse hook CPU 密集型进程阻塞 Gateway RPC**
  链接：https://github.com/openclaw/openclaw/issues/91009

- **[#48003] Steer 模式无法中途注入消息**（3月16日创建）
  链接：https://github.com/openclaw/openclaw/issues/48003

- **[#47975] 子代理会话完成后面主线会话无响应**
  链接：https://github.com/openclaw/openclaw/issues/47975

- **[#123557] ACP session/new 的 cwd 未传播到 Gateway chat.send**（8月14日创建，`fix-shape-clear` + `queueable-fix`，修复路径明确）
  链接：https://github.com/openclaw/openclaw/issues/123557

- **[#123073] dev 频道更新失败 — EUNSUPPORTEDPROTOCOL**（8月13日创建，修复路径明确）
  链接：https://github.com/openclaw/openclaw/issues/123073
  `openclaw update` 在 dev 频道因 pnpm `workspace:*` 协议失败。升级器使用 npm 但仓库要求 pnpm。

### 🟡 消息丢失/静默失败类（影响面广）

- [#121058] 静默回复失败反复出现（94 评论，今日热点）
- [#50093] WhatsApp 断线重连后错过消息
- [#86012] LINE 消息因 reply token 过期静默丢失
- [#92186] WhatsApp 群聊自动回复模式仅投递最新回复
- [#113181] Cron delivery.mode="none" + 隔离 agent → 静默无操作

## 6. 功能请求与路线图信号

以下功能请求在过去24小时仍保持活跃讨论，结合已有 PR 判断：

**可能进入下一版本：**

- **[#6757] Agent 自主触发上下文压缩（self-compact tool）** — 8 评论，2 👍
  链接：https://github.com/openclaw/openclaw/issues/6757
  已有 `pr-open` 标记，compaction 相关 PR 活跃（#123903、#123737），此功能有落地可能。

- **[#10687] 完全动态模型发现（OpenRouter 等）** — 10 评论，3 👍
  链接：https://github.com/openclaw/openclaw/issues/10687
  目前模型发现近乎静态，用户需要动态拉取快速变化的模型目录。3 个 👍 表明需求明确。

- **[#54373] 上下文溯源（Context Provenance）元数据** — 8 评论，1 👍
  链接：https://github.com/openclaw/openclaw/issues/54373
  RFC 类 Issue，为注入上下文段添加来源/易变元数据。目前仅讨论阶段。

**UI/UX 优化信号明显：**

- **[#75947] UI 质量更新（基于 UX 评分）** — 8 评论，2 👍
- **[#71142] Control UI 可配置上传大小限制** — 8 评论
- **[#123276] 新会话使用文件夹分组默认值（PR 已提交）** — 说明 UI 改进在进行中

**稳定性/运维向：**

- **[#73537] 为发布添加生产就绪稳定性标签** — 8 评论，2 👍
  用户明确希望知道哪些版本适合生产环境。
- **[#13219] 每模型用量日志（成本追踪）** — 8 评论，1 👍

## 7. 用户反馈摘要

- **"关闭不等于修复"情绪上升**：#121058 中用户对 #116277 关闭后问题仍存在表达强烈不满，是今日社区负面情绪最集中的 Issue。
- **生产环境用户焦虑明显**：#91588（内存泄漏 OOM）、#123799（生产环境需要升级/回退指引）等 Issue 表明有用户在生产环境中依赖 OpenClaw，对稳定性问题高度敏感。其中 #123799 明确请求"安全升级/回退指引"，值得维护者优先回应。
- **多平台消息丢失是高频痛点**：WhatsApp、LINE、Matrix、Telegram 均有消息静默丢失或格式异常的 Issue，渠道稳定性是用户核心关切。
- **配置文档与实际行为不一致**：#48920（Docs 领先发布）、#121083（SecretRef `provider: "default"` 隐式别名未文档化）表明文档滞后或超前于代码，增加用户试错成本。
- **积极反馈**：#73537 中用户称赞 OpenClaw "已成为我们家庭和业务工作流的一部分"，在提出需求的同时表达了对项目的认可。

## 8. 待处理积压

### 长期未修复的高优先级 Issue

| Issue | 级别 | 创建时间 | 标签 | 备注 |
|-------|------|----------|------|------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏 OOM | P0 | 2026-06-09 | `no-new-fix-pr`, `needs-maintainer-review` | 已持续 2 个月+ |
| [#48920](https://github.com/openclaw/openclaw/issues/48920) Docs 领先于发布 | P0 | 2026-03-17 | `no-new-fix-pr` | 发布阻断级，已 5 个月 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) Codex hook CPU 100% | P1 | 2026-06-06 | `no-new-fix-pr` | 已 2 个月+ |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) Steer 模式无法中途注入 | P1 | 2026-03-16 | `linked-pr-open` | 已 5 个月，有根因分析 |
| [#47975](https://github.com/openclaw/openclaw/issues/47975) 子代理会话导致主线无响应 | P1 | 2026-03-16 | 无 fix 标签 | 已 5 个月 |
| [#50093](https://github.com/openclaw/openclaw/issues/50093) WhatsApp 重连后消息丢失 | P2 | 2026-03-19 | `no-new-fix-pr` | 已 5 个月 |

### 值得关注的老旧 P2/P3（可能被遗漏）

- [#53628](https://github.com/openclaw/openclaw/issues/53628) `${XDG_CONFIG_HOME}` 安装技能时未解析（3月创建，14 评论）
- [#54409](https://github.com/openclaw/openclaw/issues/54409) Feishu 串行队列使 collect 模式失效（3月创建）
- [#54463](https://github.com/openclaw/openclaw/issues/54463) QMD 内存索引符号链接循环 ENAMETOOLONG（3月创建）
- [#75403](https://github.com/openclaw/openclaw/pull/75403) 打字指示器 fire-and-forget 导致残留（5月创建，`waiting on author`，已超过 3 个月无更新）

---

**总结**：OpenClaw 项目今日处于高活跃状态，Issue/PR 处理量大，维护者积极合并安全增强（#116489）和测试重构。但 P0/P1 级稳定性问题积压时间过长（部分达 5 个月），且"关闭但未修复"的 Issue 引发社区情绪波动。建议维护者优先处理 #121058 的复开或给出明确回应，同时为严重积压的 P0/P1 Issue 设置修复时间表，以缓解社区焦虑、提升项目健康度信号。

---

## 横向生态对比

好的，作为一名资深技术分析师，基于您提供的2026-08-15各项目动态，我为您生成以下横向对比分析报告。

***

# 个人 AI 智能体开源生态横向对比分析报告 (2026-08-15)

## 1. 生态全景

今日，个人 AI 智能体开源生态呈现出 **“龙头高活跃、梯队分化、核心聚焦稳定性与工程化”** 的态势。以 OpenClaw 为首的核心项目保持着极高的迭代速度，但社区情绪因长期未决的稳定性问题（内存泄漏、消息丢失）而波动。与此同时，生态内部出现了明确的分化：一部分项目（如 IronClaw、NanoBot）正积极重构架构、巩固工程基础；另一部分项目（如 PicoClaw、TinyClaw）则以小步快跑的方式在细分领域（边缘设备、特定渠道）精耕细作。跨项目的共同信号表明，社区的核心关注点已从“功能堆砌”转向 **“生产环境可靠性”**、**“架构可扩展性”** 及 **“开源协议与生态互操作性”**。

## 2. 各项目活跃度对比

| 项目名称 | Issues (新开/更新) | PRs (新增/待合并) | Release | 健康度评估 | 一句话点评 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 489 (活跃) | ~500 (405待合并) | 无 | ⚠️ 高活跃，高积压 | 生态龙头，但被P0/P1级稳定性问题困扰，“关闭≠修复”引发社区不满。 |
| **IronClaw** | 25 (9关闭) | 46 (23合并) | 无 (1.2.0合并回主干) | ✅ 良好 | 聚焦 v1.3.0 “自动化可靠性”史诗级重构，架构演进有序，PR合并率高。 |
| **ZeroClaw** | 33 (3关闭) | 50 (3合并) | 无 | ⚠️ 高活跃，审阅瓶颈 | 大量RFC处于待审阅状态，合并率低（6%），维护者带宽成主要瓶颈。 |
| **CoPaw** | 50 (38关闭) | 41 (15合并) | 无 (v2.1.0为近期焦点) | ✅ 良好 | 高吞吐、快响应，但2.1.0版本存在会话管理与插件隔离的潜在回归问题。 |
| **NanoBot** | 3 (2关闭) | 22 (8合并) | 无 | ✅ 良好 | 高效的Bug修复闭环（当天报告当天修复），WebUI升级是当前重心。 |
| **Hermes Agent** | 50 | 50 (~46待合并) | 无 | ⚠️ 高产但合并通道拥塞 | 大规模重构（Discord战役）与平台对齐，但Windows桌面端稳定性问题悬而未决。 |
| **LobsterAI** | 2 (新开) | 22 (合并) | ✅ 2026.8.14 | ✅ 良好 | 发版稳定，主要进行UI/UX打磨与内部技能集成修复。 |
| **PicoClaw** | 1 (活跃) | 9 (4待合并) | 无 | ✅ 稳定迭代 | 专注边缘设备场景，核心Bug（MCP挂起）已有修复PR，处于健康清理期。 |
| **NanoClaw** | 2 (新开) | 11 (8待合并) | 无 | 🟡 中等 | 供应链安全是亮点，但功能型PR积压严重，旧硬件兼容性问题初现。 |
| **Moltis** | 0 | 1 (待合并) | 无 | 🟡 低活跃，深水区 | 核心开发仍在进行（连接器基础设施），但社区讨论几乎停滞。 |
| **NullClaw** | 0 | 1 (已合并) | 无 | ✅ 平稳 | 小步快跑，解决特定部署痛点（如只读工作区），社区互动低。 |
| **TinyClaw / ZeptoClaw** | - | - | - | ⚪ 无活动 | 24小时内无任何动态，可能处于休眠或集中开发阶段。 |

## 3. OpenClaw 在生态中的定位

*   **绝对龙头与“事实标准”**：OpenClaw 的 Issue 和 PR 数量是其他项目的10倍以上，是生态中当之无愧的“流量中心”。它不仅是用户最多的项目，也因其庞大的API和技能生态，成为许多衍生项目（如PicoClaw、NanoClaw）的兼容目标或功能参照。
*   **技术路线**：OpenClaw 走的是“大而全”的平台化路线，支持几乎所有主流渠道（WhatsApp, LINE, Telegram等），并拥有强大的 Gateway 架构和丰富的扩展机制。
*   **优势**：生态最丰富、社区支持最广、功能更新最快。
*   **劣势**：复杂度带来的稳定性挑战严峻。相较于 IronClaw 从“自动化可靠性”底层重构，或 NanoBot 在WebUI上的精细打磨，OpenClaw 的“高活跃、高积压”状态暴露了其**在技术债管理和发布质量管理上的短板**。其P0级问题（如内存泄漏）积压数月，与IronClaw快速合并修复PR、NanoBot当天闭环Bug形成鲜明对比。

## 4. 共同关注的技术方向

*   **自动化与定时任务的“确定性”与“可靠性”**：
    *   **涉及项目**：**IronClaw** (#6879)、**OpenClaw** (#121953)、**ZeroClaw** (#9842)、**PicoClaw** (#3269)。
    *   **具体诉求**：自动化和定时任务频繁出现无响应、静默失败、误报成功等问题。社区不再接受“碰运气”式的执行，而是要求有契约、有验证、有确定性结果的“结构化执行”机制。

*   **上下文管理（压缩、索引、溯源）**：
    *   **涉及项目**：**CoPaw** (#6951)、**OpenClaw** (#6757, #54373)、**NullClaw** (#986)。
    *   **具体诉求**：上下文压缩不应破坏用户可见的完整记录（CoPaw）；需要更智能的上下文压缩触发机制和上下文溯源元数据（OpenClaw）；底层存储路径应具备可配置性以适配不同部署环境（NullClaw）。

*   **跨平台兼容性与老旧硬件支持**：
    *   **涉及项目**：**ZeroClaw** (#7462)、**NanoClaw** (#3245)、**LobsterAI** (#1153)。
    *   **具体诉求**：Windows 平台测试失败（ZeroClaw）、旧CPU（无AVX2）上运行崩溃（NanoClaw）、特定API的URL拼接错误（LobsterAI）。这表明项目的用户群体已不再局限于开发者的主流现代环境，对更广泛的生产和消费级硬件/OS兼容性提出了要求。

*   **生态互操作性与标准协议支持**：
    *   **涉及项目**：**ZeroClaw** (#8603)、**CoPaw** (#944)、**IronClaw** (#7665)。
    *   **具体诉求**：ZeroClaw用户希望其成为OpenAI Chat Completions协议的drop-in后端以接入现有生态（Open WebUI等）；CoPaw用户要求兼容仅支持Responses API的提供商；IronClaw为Hosted MCP端点引入OAuth。**“接入标准，而非创造标准”** 成为扩大用户基础的关键。

*   **安全边界的精细化与可配置化**：
    *   **涉及项目**：**OpenClaw** (#116489)、**ZeroClaw** (#7155, #9574)、**NanoClaw** (#3243)。
    *   **具体诉求**：从OpenClaw的安装策略警告，到ZeroClaw的高风险命令确认和高风险命令屏蔽，再到NanoClaw的供应链签名验证，生态正从“默认信任”转向 **“默认验证、精细授权”** 的安全模型。

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全渠道、功能全面的个人AI管家 | 技术爱好者、重度个人用户、希望“开箱即用”的尝鲜者 | 单一进程的 Gateway 架构，通过丰富的适配器连接所有渠道。 |
| **IronClaw** | 面向团队的自动化工作流与协作 | 团队、企业用户、重视可预测性的运营人员 | 强调“结构化自动化契约”，正在推进 unbound-turns 模型，架构上更注重确定性和审计性。 |
| **ZeroClaw** | 高安全、高配置性的个人/团队助手 | 安全敏感用户、开发者、需要深度定制的用户 | 模块化设计，丰富的RFC和策略引擎（如IAM、网络策略）。 |
| **NanoBot** | WebUI体验极致、轻量级助手 | 追求现代化UI/UX的普通用户、开发者 | 高亮WebUI交互，有向TypeScript终端UI迁移的长期目标。 |
| **CoPaw** | 数据分析（DataPaw）、多模态、插件生态 | 数据科学家、内容创作者、国内用户 | 深度集成 AgentScope 生态，强项在于数据处理和国产模型/渠道支持。 |
| **Hermes Agent** | 开发者工具、桌面端优先、Discord | 开发者、Discord重度用户、桌面端效率追求者 | 高度工程化的代码库，有“god-file”分片等激进重构，桌面客户端是重要入口。 |
| **PicoClaw / NanoClaw** | 轻量级、特定硬件或场景 | 边缘设备爱好者、NAS/软路由玩家、低配硬件用户 | PicoClaw 基于Go，主打低资源占用；NanoClaw 则聚焦于供应链安全和agent镜像分发。 |
| **Moltis** | 多渠道持久化连接（日历、邮件等） | 信息聚合与知识管理需求强的用户 | 核心是构建统一的“连接器基础设施”以持久化外部数据。 |

## 6. 社区热度与成熟度

*   **快速迭代期（功能驱动）**：**OpenClaw**、**Hermes Agent**、**CoPaw**。这些项目Issue/PR数量巨大，新功能层出不穷，但伴随而来的是稳定性波动和技术债积累。
*   **质量巩固期（稳定性/架构驱动）**：**IronClaw**、**NanoBot**、**ZeroClaw**。项目正从“能跑”向“跑得好”过渡。IronClaw重构自动化机制，NanoBot打磨WebUI与修复深层次Bug，ZeroClaw则在大量RFC中寻求架构共识。这些项目的合并率或闭环速度更能体现工程成熟度。
*   **稳定迭代期（细分深耕）**：**LobsterAI**、**PicoClaw**、**NullClaw**。项目已具备稳定用户群，更新频率稳定，主要进行功能优化和特定问题修复。
*   **沉寂/休眠期**：**TinyClaw**、**ZeptoClaw**。24小时内无活动，社区热度较低。

## 7. 值得关注的趋势信号

1.  **从“功能竞赛”转向“可靠性军备竞赛”**：IronClaw 和 ZeroClaw 的实践表明，头部项目正在将投资重点从“能做什么”转向“能否可靠地做”。`确定性`、`原子性`、`审计`、`结构化契约` 成为架构关键词。对开发者而言，这意味着在选择框架时，其工程化能力（如测试覆盖、CI/CD、合并策略）将变得与功能列表同等重要。

2.  **“标准接入”成为生态扩张的胜负手**：ZeroClaw 的 Chat Completions profile 提案极具代表性。个人AI助手若想成为基础设施，必须学会与现有生态（如Open WebUI）讲同一种语言。**兼容性策略**将是未来用户增长的关键变量。

3.  **安全是“信任”的基石，而非“功能”**：从NanoClaw的供应链签名验证到ZeroClaw的审批人身份绑定，安全实践正从应用层下沉到基础设施层。零信任理念正在开源智能体生态中落地生根。

4.  **垂直场景与硬件差异化正在形成**：PicoClaw 面向低资源设备，Moltis 聚焦连接器持久化。未来生态将不会是“一家独大”，而是由通用平台（OpenClaw）和多个垂直领域的“小而美”项目（PicoClaw, Moltis等）共同构成。

5.  **文档与实际行为的一致性是社区信任的“隐形杀手”**：OpenClaw (#48920)、Hermes (#85622) 和 LobsterAI 的案例都表明，文档超前或滞后于代码会剧烈消耗社区信任，其破坏力不亚于严重的Bug。对于开发者而言，将“文档即代码”的实践纳入CI/CD是提升项目专业度的关键。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-15

## 今日速览

NanoBot 项目过去 24 小时保持较高活跃度：3 条 Issue 更新（1 新开 / 2 已关闭），22 条 PR 更新（14 条待合并 / 8 条已合并或关闭），无新版本发布。核心进展集中在两个方向：一是 WebUI 交互体验的密集迭代（拖拽分组、会话协作、多语言本地化、粒子背景等 6+ 个 WebUI PR 并行推进），二是稳定性修复（Anthropic 流式超时语义修正、Windows 文件替换重试、会话保存竞态防护）。值得关注的是 `#5391` 和 `#5392` 在一天内完成了从 Bug 报告到修复 PR 合并的闭环，体现了高效的响应机制。项目整体健康度良好，但存在 14 条待合并 PR 的积压趋势，且多个 PR 标注 `conflict`，需要维护者及时处理合并冲突。

**活跃度评估**：🔥🔥🔥🔥（较高）— 24 小时 25 条动态，核心贡献者持续投入。


## 项目进展

### 已合并/关闭的重要 PR（8 条）

| PR | 标题 | 类型 | 说明 |
|---|---|---|---|
| [#5392](https://github.com/HKUDS/nanobot/pull/5392) | fix(anthropic): treat stream idle timeout as inactivity only, not total time | Bug 修复 | **修复 #5391**：将 `NANOBOT_STREAM_IDLE_TIMEOUT_S` 从总超时改为仅空闲超时，避免长时间活跃生成被中断。从 Issue 报告到合并仅数小时。 |
| [#5393](https://github.com/HKUDS/nanobot/pull/5393) | feat(webui): polish sidebar and session transitions | WebUI 改进 | 从 #5358 拆分出的独立 UI 改进：侧边栏层级优化、标签页扁平化、文件夹展示、过渡动画增强。 |
| [#5395](https://github.com/HKUDS/nanobot/pull/5395) | feat(webui): refine conversation groups and shared shapes | WebUI 改进 | 统一会话分组术语、支持拖拽进/出分组、简化删除确认样式、引入共享形状缩放。 |
| [#5390](https://github.com/HKUDS/nanobot/pull/5390) | Agent/knowledge graph | 功能/Chore | 知识图谱相关，描述精简，需关注后续详细内容。 |
| [#4689](https://github.com/HKUDS/nanobot/pull/4689) | feat(providers): surface OAuth status and expiry warnings | 功能 | **关闭（标记 invalid）**：OAuth 状态和过期警告功能，因冲突被标记为无效，建议后续重新提出。 |
| [#5018](https://github.com/HKUDS/nanobot/pull/5018) | feat(skills): support explicit context loading | 功能 | **关闭（标记 conflict）**：支持显式上下文加载的 skills 功能，因冲突关闭，建议解决冲突后重新提交。 |

### 项目整体推进

- **WebUI 交互成熟度显著提升**：今日合并的 #5393 和 #5395 与待合并的 #5389、#5367、#5371、#5356、#5358 形成了完整的 WebUI 体验升级矩阵，覆盖会话组织、多语言、协作、权限控制等多个维度。
- **稳定性回归修复加速**：Anthropic 流式超时问题（#5392）从报告到合并当天完成，说明维护者对高影响 Bug 响应迅速。
- **TypeScript 终端 UI 持续推进**：#4329 已开放 2 个月仍在活跃更新，作为长期项目正在稳步推进。


## 社区热点

### 最受关注

| 排名 | Issue/PR | 标题 | 评论数 | 分析 |
|---|---|---|---|---|
| 1 | [#5161](https://github.com/HKUDS/nanobot/issues/5161) | refactor: narrow file-level Pyright suppressions | 1（待合并 PR #5396 引用） | 代码质量基础设施改进。PR #5158 启用 `strict` 检查后留下 31 个文件级抑制指令，#5396 正逐文件细化。社区对类型安全重视度高。 |
| 2 | [#5391](https://github.com/HKUDS/nanobot/issues/5391) | NANOBOT_STREAM_IDLE_TIMEOUT_S 被当作 Anthropic 流总超时 | 0（当天即被 #5392 修复） | 影响生产环境的实际问题。配置项语义与预期不符，导致长时间生成被误杀。虽无评论但合并速度说明关注度极高。 |
| 3 | [#5378](https://github.com/HKUDS/nanobot/issues/5378) | file-cap archive failure mutates session before persistence | 0 | 会话状态一致性问题：归档回调失败时内存态已被修改，下次成功保存会丢失溢出数据。目前无修复 PR。 |

### 社区诉求分析

- **WebUI 体验是当前最大热点**：6+ 个 PR 并行推进（#5389、#5367、#5371、#5356、#5358、#5340），开发者群体对 Web 端操作效率、视觉体验、协作能力需求强烈。
- **稳定性 > 新功能**：两个 Bug Issue 均当天获得修复或讨论，社区对生产环境可靠性问题高度敏感。


## Bug 与稳定性

| 严重程度 | Issue | 标题 | 状态 | 修复 PR |
|---|---|---|---|---|
| 🔴 高 | [#5391](https://github.com/HKUDS/nanobot/issues/5391) | Anthropic 流式超时被当作总超时，杀死长时活跃生成 | **已修复** | [#5392](https://github.com/HKUDS/nanobot/pull/5392) 已合并 |
| 🟡 中 | [#5378](https://github.com/HKUDS/nanobot/issues/5378) | file-cap 归档失败改变会话内存态，持久化后丢失数据 | 待处理 | 暂无 |
| 🟡 中 | [#5271](https://github.com/HKUDS/nanobot/pull/5271) | 后台任务保存可能覆盖 `/new` 后的新会话（p0 级 PR） | **待合并** | 自身即修复 PR |
| 🟢 低 | [#5382](https://github.com/HKUDS/nanobot/pull/5382) | Windows `os.replace()` 偶发 PermissionError 导致崩溃 | **待合并** | 自身即修复 PR |

**稳定性总结**：最严重的 Anthropic 流式超时问题已当日闭环。`#5378` 的会话状态一致性问题值得关注——归档回调失败会导致数据丢失，目前无修复方案。Windows 平台的文件替换重试和后台任务覆盖保护均在待合并队列中。


## 功能请求与路线图信号

| 功能方向 | 相关 PR | 状态 | 纳入下一版本可能性 |
|---|---|---|---|
| **WebUI 会话拖拽分组** | [#5389](https://github.com/HKUDS/nanobot/pull/5389) | 待合并 | ⭐⭐⭐⭐ 高，功能完整且已适配新布局 |
| **WebUI 会话协作（@提及）** | [#5358](https://github.com/HKUDS/nanobot/pull/5358) | 待合并（conflict） | ⭐⭐⭐ 中高，需先解决冲突 |
| **WebUI 多语言本地化** | [#5367](https://github.com/HKUDS/nanobot/pull/5367) | 待合并 | ⭐⭐⭐⭐ 高，覆盖 10 种语言 |
| **WebUI 设置流程优化** | [#5356](https://github.com/HKUDS/nanobot/pull/5356) | 待合并（conflict） | ⭐⭐⭐ 中高 |
| **WebUI 粒子动画背景** | [#5340](https://github.com/HKUDS/nanobot/pull/5340) | 待合并（conflict） | ⭐⭐ 中，视觉优化类 |
| **MCP SDK v2 迁移** | [#5179](https://github.com/HKUDS/nanobot/pull/5179) | 待合并 | ⭐⭐⭐⭐ 高，基础设施升级 |
| **市场 skills 可覆盖内置** | [#5309](https://github.com/HKUDS/nanobot/pull/5309) | 待合并 | ⭐⭐⭐ 中高 |
| **天气 Skill 示例** | [#4145](https://github.com/HKUDS/nanobot/pull/4145) | 待合并 | ⭐⭐ 中（示例贡献，维护压力小） |
| **TypeScript 原生终端 UI** | [#4329](https://github.com/HKUDS/nanobot/pull/4329) | 待合并 | ⭐⭐⭐ 中长期战略方向 |

**路线图信号**：下一版本似乎将聚焦 WebUI 体验的全面升级（多语言 + 拖拽 + 协作 + 设置优化），同时 MCP SDK v2 迁移是重要的技术基建改进。WebUI 相关 PR 数量之多（6+ 条）表明这是当前开发重点。


## 用户反馈摘要

1. **流式超时配置语义困惑**（#5391）：用户期望 `NANOBOT_STREAM_IDLE_TIMEOUT_S`（默认 90s）仅限制空闲，但实际被用作总超时，长时间活跃生成被中断。此问题已修复，但暴露了配置项命名与行为一致性问题，可能影响其他 provider 的同类配置。

2. **会话数据一致性担忧**（#5378）：归档失败导致内存态被修改、数据可能丢失，反映出用户对数据安全的高度重视。目前无修复，建议维护者优先处理。

3. **WebUI 多语言需求**（#5367）：覆盖 10 种语言的本地化 PR 获得积极评价，说明 NanoBot 用户群体国际化程度较高。

4. **WebUI 管理效率痛点**（#5389、#5358）：拖拽分组和 @提及协作功能直击多会话管理痛点，用户对 Web 端操作效率有明确诉求。


## 待处理积压

| 类型 | 条目 | 已开放时长 | 优先级建议 | 提醒 |
|---|---|---|---|---|
| PR | [#4329](https://github.com/HKUDS/nanobot/pull/4329) TypeScript 终端 UI | 63 天 | 中 | 长期开放但持续更新，若纳入路线图请明确排期 |
| PR | [#4145](https://github.com/HKUDS/nanobot/pull/4145) 天气 Skill 示例 | 75 天 | 低 | 示例类贡献积压过久，建议合并或明确拒绝 |
| Issue | [#5378](https://github.com/HKUDS/nanobot/issues/5378) file-cap 归档状态一致性 | 2 天 | **高** | 数据丢失风险，建议尽快分配修复 |
| PR | [#5271](https://github.com/HKUDS/nanobot/pull/5271) 会话保存竞态（p0） | 9 天 | **高** | p0 级 PR 已开放 9 天，建议优先 review |
| PR | 3 个标注 `conflict` 的 PR（#5356/#5358/#5340） | 2-4 天 | 中 | 冲突积压会阻塞 WebUI 功能主线的合并进度 |
| PR | [#5382](https://github.com/HKUDS/nanobot/pull/5382) Windows replace 重试 | 2 天 | 中 | Windows 用户稳定性改进，建议尽快合并 |

---

*本报告基于 NanoBot (github.com/HKUDS/nanobot) 公开数据生成，数据截止 2026-08-15。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报

**日期：** 2026-08-15
**数据来源：** github.com/nousresearch/hermes-agent


## 1. 今日速览

项目今日活跃度极高，过去24小时内有50条Issue更新和50条PR更新，呈现典型的"高产社区"状态，但其中绝大多数（超过30条）是**Discord Omniscience 战役**的系列功能子Issue（由同一位作者 andrexibiza 批量提交），属于有组织的功能推进而非自然涌现。真正值得关注的核心信号有三：一是**Windows Desktop 客户端连续两次更新后崩溃**（P1，已并存在对应修复PR），二是**外部记忆提供程序违背"additive"契约**的缺陷争议（#85622, 10条评论），三是**技能索引新鲜度探针持续告警**（#66616, 31条评论，状态degraded）。今日无新版本发布，合并/关闭的PR仅4条，但积压的待合并PR达到46条，合并通道存在一定拥塞。综合判断：项目在有序推进大规模重构与平台对齐，但稳定性（尤其Windows桌面端）与合并效率是当前两大隐忧。


## 2. 版本发布

过去24小时内无新版本发布（最新 Releases: 无）。但结合现有Issue信息，**Windows Desktop 客户端在 2026-07-31 和 2026-08-14 连续两次更新后均出现崩溃**（详见 Bug 与稳定性 部分），提醒维护者关注既有发布管线的质量门禁，可考虑热修复版本。


## 3. 项目进展

今日合并/关闭的 PR 共 4 条，其中有实质内容的有：

- **[#77285 [CLOSED] fix(tts): rewrite xAI streaming against the real WebSocket protocol](https://github.com/NousResearch/hermes-agent/pull/77285)** — 重写了 `XAIStreamer`，使其对接真实的 xAI WebSocket TTS 协议。此前 #73862 落地的版本"无法在任何代码路径上产生音频"（#73985），该 PR 为"救火式"修复，直接解决了语音功能不可用的问题。
- **[#86556 [CLOSED] feat(memory): cloud memory — dual-write state.db to MySQL/MariaDB](https://github.com/NousResearch/hermes-agent/pull/86556)** — 将本地 SQLite 双写到远端 MySQL/MariaDB，实现跨机器、跨区域的会话记忆。SQLite 仍为运行时真相源；远端不可用时行为完全回退为纯本地。

另有两条被标记为 CLOSED/duplicate 的 PR（#86368），属于重复提交的清理。整体而言，今日合并的实质内容有限，但 xAI TTS 修复是用户可感知的重大改进。


## 4. 社区热点

今日讨论度最高的条目如下：

- **[#78647 [CLOSED] [EPIC — COMPLETE] All Gods Must Die: 20/20 killed](https://github.com/NousResearch/hermes-agent/issues/78647)** — 76条评论，今日关闭。
  这场仓库级"god-file 分片"史诗战役宣告完结——20 个巨型文件全部分片完成，且已确立"god files 只分不合并"的长期政策。这是架构层面的重要里程碑，标志着代码库可维护性进入新阶段。

- **[#66616 [OPEN] [skills-index-watchdog] Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** — 31条评论，仍开放。
  自动新鲜度探针已持续告警，索引已落后 29.8 小时（限制 26h）。长时间未修复表明 CI 管线的技能索引重建/部署环节存在系统性延迟，社区对文档/技能导航的可靠性表示担忧。

- **[#85622 [OPEN] 外部记忆提供程序抑制内置 MEMORY.md/USER.md 注入](https://github.com/NousResearch/hermes-agent/issues/85622)** — 10条评论。
  文档明确承诺"additive, never replacing"，但 `mode: both` 下内置记忆注入被抑制。这是文档与实现不符的契约违背问题，社区反应较强。

- **Discord Omniscience 战役（#79564 及其 30+ 子Issue）** — 每个子Issue均带有测试证据（如 "16 passed"、"19 passed"），由其协调者 andrexibiza 批量提交。诉求清晰：将 Hermes 的 Discord 表面能力与官方 API v10 全面对齐，覆盖自动补全、组件鉴权、语音消息验证、路由矩阵、恢复游标、线程权限、附件路由与有界读取、流式投递状态机等。

综合来看，社区最关注的是**契约一致性与自动化管线健康度**。


## 5. Bug 与稳定性

按严重程度排列：

**P1（严重）**
- **[#86223 bug(desktop): Windows 桌面客户端连续两次更新后崩溃](https://github.com/NousResearch/hermes-agent/issues/86223)** — 后端退出码 1，无法自重启，"Reopen Hermes to finish" 提示，更新管线回退 Git 路径后触发 WinError 32 锁链。属于发布质量事故，且已影响两代版本。已有两个关联修复 PR 在途：
  - [#86555 fix(desktop-update): wait for rebuilt executable before relaunch](https://github.com/NousResearch/hermes-agent/pull/86555)
  - [#86269 fix(update): rebuild Desktop after release artifact loss](https://github.com/NousResearch/hermes-agent/pull/86269)

**P2（中等）**
- **[#86510 read_file: total_lines 对无尾换行文件 off-by-one](https://github.com/NousResearch/hermes-agent/issues/86510)** — 5 行有换行 + 1 行无换行时 `total_lines` 报 5 实为 6，读窗口到 EOF 时展示截断。已标记 duplicate，无修复 PR。
- **[#86513 file_tools: 读去重/写陈旧检查 stat 的是宿主机文件系统](https://github.com/NousResearch/hermes-agent/issues/86513)** — 对远程/容器后端，host 侧 os.path 判断全部失效，导致错误去重和伪陈旧误报。无修复 PR。
- **[#86482 cron scheduler: create_execution 失败导致任务永久滞留 running 集合](https://github.com/NousResearch/hermes-agent/issues/86482)** — 异常路径无清理，"already running — skipping" 每 tick 重复。无修复 PR。
- **[#86483 state: Telegram topic 迁移在 BEGIN IMMEDIATE 内执行 executescript](https://github.com/NousResearch/hermes-agent/issues/86483)** — 隐式 COMMIT 破坏原子性，部分失败丢失绑定。无修复 PR。

**P3（低）**
- 其余为 P3 级问题（如 #60260 Desktop approval bar 不渲染、#83845 Dashboard PATH 缺失等），多为边缘场景，暂不展开。

**稳定性观察：** 今日无新增 P0 级别崩溃；但 P1 的 Windows 桌面故障已持续两天未修复，且关联 PR 仍处于 OPEN 状态，建议优先推进合并。


## 6. 功能请求与路线图信号

- **Discord Omniscience 战役（#79564）大规模推进** — 一日内新增 12+ 子Issue（#86535~#86554 区间），覆盖自动补全、组件鉴权、语音消息验证、路由矩阵、命令注册表同步、交互 ACK、线程权限、附件路由、流式投递状态机、论坛投递、主动投递等。每个子Issue均带测试通过的证据，且对应实现 PR（如 #86550）已提交。该项目几乎可以确定会进入下一版本，且看起来已是 90% 完成态。

- **[#86554 [Feature]: Desktop 语义化关键词强调色](https://github.com/NousResearch/hermes-agent/issues/86554)** — 面向暗色/低对比度主题，加入语义化颜色以强化可读性。有需求但暂无响应，属于小型低风险改进。

- **[#86553 feat(delegation): 批量子代理 prompt-cache 错峰启动（Claude Code v2.1.229 移植）](https://github.com/NousResearch/hermes-agent/pull/86553)** — `delegation.prefix_stagger_seconds` 让第一批子代理错峰启动，使首个子代理的 prompt 填充缓存、其余命中缓存，显著降低成本。移植自 Claude Code，属成本优化型功能。

- **[#86552 feat(terminal): 本地后端每条命令硬性内存上限](https://github.com/NousResearch/hermes-agent/pull/86552)** — `terminal.memory_limit_mb`，防止构建进程打爆整机内存。同样移植自 Claude Code v2.1.233。

- **#67798 生命周期钩子应用于所有执行面** — 仍为 open 状态，被标记 needs-decision，说明 Gateway 与 CLI/TUI/Cron 等执行面在会话生命周期语义上存在分歧，决策尚未落地。

- **#62944 单网关多 Agent（已 rebase）** — 长时间积压的重磅 PR，涉及大量组件，仍可视为后续架构演进的重要信号。


## 7. 用户反馈摘要

- **Windows 桌面端用户（aKa368）强烈不满：** "The desktop client is broken after the last 2 consecutive updates" — 连续两次更新都崩，用户对发布质量失去信心，且 WinError 32 锁链和 "Reopen to finish" 的引导体验被认为极不友好。核心诉求：**发布回归测试必须覆盖 Windows 更新路径。**

- **契约违背引发质疑（TeaShaman-cyber）：** 文档声称外部记忆提供程序是"additive"，实际 `mode: both` 下内置 MEMORY.md/USER.md 注入被抑制。用户评论语气克制但措辞尖锐："contradicts documented 'additive, never replacing' contract" — 这类文档与实现脱节的问题最伤社区信任。

- **文档/技能导航不稳定（nousbot-eng 探针）：** 技能索引持续陈旧（29.8h 超限），用户依赖 `/docs/skills` 发现与检索技能，时间延迟将直接影响下游使用体验。

- **桌面端小功能的真实场景（homerhzfeng92）：** 预览面板无地址栏，用户无法手动输入 URL。"There is no way for the user to type or paste a URL" — 这是典型的高频但易被忽视的日常使用场景，虽为 P3，反映了桌面端交互细节仍有待补齐。

- **开发者社区对"有组织推进"反馈积极：** Discord Omniscience 系列Issue均带测试证据和明确互锁，这种工程化风格在评论中获得较高信任度。


## 8. 待处理积压

| 类型 | 编号 | 标题 | 摘要 | 状态 |
|------|------|------|------|------|
| Bug | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 技能索引持续陈旧（degraded） | 自动化探针已告警多日，索引落后近 30 小时，CI 重建/部署管线疑似有系统性延迟 | 已开放 28 天，需维护者介入排查流水线 |
| Bug | [#86510](https://github.com/NousResearch/hermes-agent/issues/86510) | read_file total_lines off-by-one | 文件无尾换行时行数少报 1，读窗口至 EOF 截断 | 无 fix PR，待分配 |
| Bug | [#86513](https://github.com/NousResearch/hermes-agent/issues/86513) | file_tools 对远程/容器后端 stat 宿主机文件系统 | 读去重/写陈旧检查在远程场景全部失效 | 无 fix PR，待分配 |
| Bug | [#86482](https://github.com/NousResearch/hermes-agent/issues/86482) | cron 任务 create_execution 失败后永久滞留 running 集合 | "already running — skipping" 每 tick 重复 | 无 fix PR，待分配 |
| Bug | [#86483](https://github.com/NousResearch/hermes-agent/issues/86483) | Telegram topic 迁移中 executescript 破坏事务原子性 | 隐式 COMMIT 导致部分失败丢失绑定 | 无 fix PR，待分配 |
| PR | [#71354](https://github.com/NousResearch/hermes-agent/pull/71354) | Git-Bash MCP 后门绕过 Windows 防护（安全） | Windows 下 bash.exe/sh.exe 未被识别为 shell，恶意 MCP 载荷可绕过 exfil/persistence 防护 | 开放 21 天，需安全 review |
| PR | [#62944](https://github.com/NousResearch/hermes-agent/pull/62944) | 单网关多 Agent（rebase 版） | 重大架构升级，涉及 20+ 组件，社区期待度高但需广泛评审 | 开放 34 天至今未合并，建议排期讨论 |
| Feature | [#67798](https://github.com/NousResearch/hermes-agent/issues/67798) | 生命周期钩子共享运行时契约 | HookRegistry 由 Gateway 持有，CLI/TUI/Cron 等执行面无法复用 | needs-decision 状态，已开放 26 天 |

---

*日报完。本报告基于 GitHub 公开数据生成，所有链接均指向 NousResearch/hermes-agent 原始 Issue/PR。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-15** | **数据周期：2026-08-14 → 2026-08-15** | **数据源：sipeed/picoclaw**

---

## 1. 今日速览

过去 24 小时项目活跃度处于**中高水平**：共产生 3 条 Issue 更新（1 条活跃）和 9 条 PR 更新（4 条待合并），无新版本发布。核心事件是 **PR #3337 针对 #3269 中 MCP 连接失败导致 Agent 循环挂起的问题提交了修复**，且该 PR 与活跃 Issue 直接对应，形成"Issue 报告 → PR 修复"的快速闭环。另有 4 个陈旧（stale）Issue/PR 被自动清理关闭，维护者正在积极收敛积压项。deltachat 重构 PR（#3222）仍在持续更新中，属于长期推进的架构优化工作。整体来看，项目处于**修复与清理并行的健康迭代阶段**。

---

## 2. 版本发布

过去 24 小时无新版本发布。

> 注：Issue #3269 中用户使用的是 `picoclaw nightly (git: 2cf030d2)` 构建，建议关注后续 nightly 或正式版发布以获取 MCP 挂起修复。

---

## 3. 项目进展

今日无 PR 被合并，但有 5 个 PR 被关闭（含 stale 自动关闭），4 个仍在开放中。**值得关注的是 3 个对应功能性提交的 PR 已处于关闭状态，但需注意这些关闭发生在数据统计周期内，可能为合并后关闭，也可能是因 stale 或冲突被关闭**，具体需要核实关闭原因。

### 已关闭的 PR 中推进的功能（请维护者确认关闭原因）：

- **#3270 — DashScope TTS 与微信语音消息支持**：新增阿里云 DashScope 语音合成 Provider 和微信音频文件发送能力（涉及 `pkg/audio/tts/dashscope_tts.go` 新文件）
- **#3279 — 修复 seahorse 导致工具调用格式泄漏至 LLM 消息的问题**：修复 `partsToReadableContent` 中工具调用格式混入用户消息的 Bug
- **#3283 — DingTalk 渠道图片消息支持**：新增图片消息接收/下载、token 缓存等能力

### 仍在推进的开放 PR：

- **#3222 — deltachat 渠道重构重构**：删减约 200 行代码，移除遗留特性、统一官方中继列表、重命名 API 字段，目标是提升维护性与安全性，**已开放超过 1 个月，需关注审核进度**
- **#3319 — exec 工具超时与布尔选项修复**：修复 `exec` 工具忽略单次运行的 `timeout` 参数、以及 `background`/`pty` 被错误声明为字符串的问题
- **#3200 — 可配置模型默认回退链**：Web UI 中可配置默认模型及回退顺序，后端 API 持久化，**开放已近 1.5 个月**

---

## 4. 社区热点

### 最热 Issue：#3269 — MCP 服务器连接失败导致 Agent 挂死

- **状态**: OPEN | **评论**: 5 | **👍**: 1
- **链接**: [sipeed/picoclaw Issue #3269](https://github.com/sipeed/picoclaw/issues/3269)
- **背景**: MCP 服务器不可达时，`AgentLoop.Run` 直接向调用方返回错误，导致聊天界面完全停止响应。
- **分析**: 虽评论数不算高，但该问题直击 AI Agent 的核心稳定性（聊天界面卡死对用户影响极大），且已有对应 PR #3337 提交，属于社区关注焦点。
- **社区回应**: 用户 `kuzmichus` 在 8 月 14 日（报告后约 25 天）提交了修复 PR #3337。

### 讨论度较高的陈旧 Issue：

- **#3308 — Code Review: SeaHorse/Channel Manager/Hooks 并发问题**（评论 2 条）：社区成员主动对核心组件做了并发安全性、goroutine 泄漏和性能审查，体现了社区对代码质量的关注。但当前已被标记为 stale 并关闭。"Hey team! First off, huge congrats on PicoClaw—building a native Go AI assistant that runs on $10 hardware with <10MB RAM and sub-second boot times is seriously awe..." 评论情绪积极正面。
- **#3307 — Telegram 渠道缺少会话管理命令**（评论 2 条）：Web UI 已有完整的会话管理，Telegram 用户却无法列出、切换或删除会话。

### 观点：

#3269 凸显了外围生态（MCP 服务器）故障向核心会话传导的架构脆弱性；#3308 则显示了社区对 PicoClaw 在资源限制下实现高性能的认可，同时也关注内部实现质量。两个方向（稳定性 + 代码质量）是社区当前最关心的话题。

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🔴 高 | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP 服务器连接失败导致 Agent 循环挂起，聊天界面完全停止响应 | 有修复 PR [#3337](https://github.com/sipeed/picoclaw/pull/3337) 提交，待审核 |
| 🟡 中 | PR [#3319](https://github.com/sipeed/picoclaw/pull/3319) | `exec` 工具的单次运行 `timeout` 参数被忽略，总是使用全局配置；`background`/`pty` 被声明为字符串（实际应为布尔值） | 修复 PR 开放中 |
| 🟡 中 | PR [#3279](https://github.com/sipeed/picoclaw/pull/3279)（已关闭） | seahorse 的 `partsToReadableContent` 导致工具调用格式泄漏到 LLM 用户消息中 | 修复已提交（需确认是否已合并） |

**稳定性判断**：#3269 是当前最值得关注的高影响 Bug，好在已有修复提交。MCP 是 PicoClaw 生态的重要组件，此问题的解决将大幅提升会话可靠性。

---

## 6. 功能请求与路线图信号

| 功能需求 | 来源 | 状态 | 可能纳入版本判断 |
|---------|------|------|----------------|
| **模型默认回退链** | PR [#3200](https://github.com/sipeed/picoclaw/pull/3200) | OPEN（约 1.5 个月） | 对提升用户体验有价值，但长期未合并，需维护者确认是否纳入 |
| **DashScope TTS 与微信语音** | PR [#3270](https://github.com/sipeed/picoclaw/pull/3270)（已关闭） | 待确认是否合并 | 若已合并，将扩展音频输出渠道，增强多模态能力 |
| **DingTalk 图片消息** | PR [#3283](https://github.com/sipeed/picoclaw/pull/3283)（已关闭） | 待确认是否合并 | 完善 DingTalk 渠道的消息类型支持 |
| **Telegram 会话管理命令** | Issue [#3307](https://github.com/sipeed/picoclaw/issues/3307) | CLOSED（stale） | 用户明确期望 Telegram 与 Web UI 拥有同等的会话管理能力，但已被自动关闭，需维护者重新评估是否排期 |

**路线图判断**：当前信号集中在**渠道功能完善**（微信语音、钉钉图片、Telegram 会话管理）与**模型配置灵活性**（回退链）两个方向，反映了用户对多通道体验一致性的需求。

---

## 7. 用户反馈摘要

### 正面反馈：
- 来自 #3308 的评论对 PicoClaw 在 **$10 硬件、<10MB RAM、亚秒级启动**条件下运行 Go AI 助手表示称赞（"seriously awesome"），体现项目在边缘设备 AI 上的差异化优势获得社区认可。

### 痛点与需求：
- **MCP 故障无降级机制**（#3269）：用户"chat interface stops replying to users entirely"，说明对外部服务依赖缺少容错/超时设计。
- **渠道能力不对等**（#3307）："The Web UI has a full session management system... However, there is no equivalent capability from Telegram"，用户希望所有聊天渠道体验一致。
- **Bailian/DashScope 用户需要 TTS**（#3270）：提交者实现了阿里云 DashScope TTS 并配套微信语音发送，说明用户对国内云平台集成有实际需求。

---

## 8. 待处理积压

| 项目 | 类型 | 等待时长 | 建议 |
|------|------|---------|------|
| [#3222 — deltachat 渠道重构](https://github.com/sipeed/picoclaw/pull/3222) | PR | 43 天（7/3 创建） | 重构涉及 -200LOC 与安全改进（移除密码硬编码），长期未审核将累积合并冲突风险，建议维护者尽快 review |
| [#3200 — 模型默认回退链](https://github.com/sipeed/picoclaw/pull/3200) | PR | 45 天（7/1 创建） | 开放已超 1.5 个月，虽标记为 stale 但仍在开放状态，需明确是否纳入排期 |
| [#3269 — MCP 失败致 Agent 挂起](https://github.com/sipeed/picoclaw/issues/3269) | Issue | 26 天（7/20 创建，8/14 有 PR） | 已有修复 PR #3337 提交，请尽快安排 review/merge 以解决高影响稳定性问题 |
| [#3308/#3307](https://github.com/sipeed/picoclaw/issues/3308) | Issues | 已 stale 关闭 | 虽已自动关闭，但反馈内容有实际价值（并发审查建议、Telegram 会话管理），建议维护者手动重新打开或记录至 roadmap |

---

## 总结

PicoClaw 目前处于**稳定迭代**阶段：核心 Bug（MCP 挂起）已有修复提交、渠道功能在持续扩展、stale 清理机制在帮助维护者收敛长期积压。**需要维护者重点关注**：① 尽快审核 #3337 修复并合并；② 推进 #3222 和 #3200 两个长期开放 PR；③ 评估是否将 #3307（Telegram 会话管理）重新纳入计划。整体项目健康度良好，但需注意渠道能力和体验的一致性建设。

---

*本日报由 AI 自动生成，数据基于 2026-08-14 至 2026-08-15 时间窗口内的 GitHub 活动。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-15

*数据来源: github.com/nanocoai/nanoclaw | 覆盖窗口: 2026-08-14 至 2026-08-15*


## 1. 今日速览

今日 NanoClaw 项目活跃度处于**中高水平**。过去24小时内，Issue 侧新增 2 条（2条均为新开，无关闭），PR 侧更新 11 条，其中**8 条仍待合并、3 条已关闭**。核心团队今日执行了一轮供应链签名验证机制的"实弹演练"（PR #3242/#3244），虽按计划关闭未合并，但验证了 verify → approve-agent-image → cosign 独立验证的整条自动化链路。修复类 PR 持续密集提交（今日新增 4 条 fix 类 PR），涵盖 Node 版本检测、cron 解析容错、Windows 容器清理兼容性、附件处理等方向。值得关注的是，两条新 Issue 均指向上游基础依赖（Node.js 与 Bun 运行时）对旧硬件的兼容性问题，提示项目对老旧环境的支持存在隐患。


## 2. 版本发布

**无新版本发布。** 项目当前停留在上一版本，无更新内容、破坏性变更或迁移说明。


## 3. 项目进展

今日核心团队关闭了 3 条 PR，其中 2 条按计划关闭未合并（供内部验证用）、1 条正式合并。项目整体向前推进了以下方向：

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#3243](https://github.com/nanocoai/nanoclaw/pull/3243) | [core-team] verify-agent-image: arming auto-merge is not a verdict | ✅ 已关闭（合并） | **核心修复。** 修正了验证作业中 `enable auto-merge` 作为最后一步可能因 draft/API 错误导致整个验证误报失败的逻辑问题。这是供应链安全链路的关键补丁。 |
| [#3242](https://github.com/nanocoai/nanoclaw/pull/3242) | [core-team] DO NOT MERGE — live-fire test of the signature approver | ⛔ 已关闭（未合并） | 内部实弹演练，验证签名验证全链路，按计划关闭。 |
| [#3244](https://github.com/nanocoai/nanoclaw/pull/3244) | [core-team] DO NOT MERGE — live-fire the signature approver (take 2) | ⛔ 已关闭（未合并） | 第二轮实弹演练，验证在 draft 状态下验证作业可正常通过，按计划关闭。 |

**关键进展**：`#3243` 的合入意味着 CI 验证链路不再因 `auto-merge` 这类与镜像本身无关的操作而误报失败。这一修复对供应链安全自动化有实质性意义——现在"验证通过"才是真正的结论，而非流水线最后一步是否成功。


## 4. 社区热点

今日无高讨论量或高评论热度的 Issue/PR（新条目均为 0 评论，历史条目评论数据未更新）。值得关注的信号主要来自两个"实弹演练" PR（[#3242](https://github.com/nanocoai/nanoclaw/pull/3242)、[#3244](https://github.com/nanocoai/nanoclaw/pull/3244)）——核心团队围绕镜像签名验证机制在进行多轮内部测试，说明该项目对其 agent 镜像供应链安全的重视程度很高，后续可能推出更严格的镜像发布策略。


## 5. Bug 与稳定性

今日报告 2 条新 Bug，按严重程度排列：

| 严重程度 | Issue | 问题 | 状态 |
|---|---|---|---|
| 🔴 高 | [#3245](https://github.com/nanocoai/nanoclaw/issues/3245) | **预构建 agent 镜像中的 Bun 二进制要求 CPU 支持 AVX2 指令集**，在旧款 Intel Atom/Tremont/Elkhart Lake 处理器上直接 SIGILL 崩溃。该问题影响面较广——`NANOCLAW_HARDENED_IMAGE=true`（向导默认推荐）在任何无 AVX2 的硬件上均不可用。 | ⚠️ 尚无 fix PR |
| 🟡 中 | [#3248](https://github.com/nanocoai/nanoclaw/issues/3248) | **setup.sh 的 "Node missing or too old" 分支存在逻辑缺陷**——当检测到 Node 版本过旧时，`install-node.sh` 因检测到"已有 Node"而短路跳过安装，最终导致安装流程未能真正解决版本过旧问题。 | ✅ 已有 fix PR [#3249](https://github.com/nanocoai/nanoclaw/pull/3249) |

**此外**，今日还有 4 条待合并的修复类 PR 与稳定性相关，值得关注：

- **PR [#3247](https://github.com/nanocoai/nanoclaw/pull/3247)** — cron 字符串格式错误时，当前逻辑每次调度 tick 都会重复报错；修复后将为已失效的 cron 做"退役"处理
- **PR [#3246](https://github.com/nanocoai/nanoclaw/pull/3246)** — 孤儿容器清理在 Windows 上因 POSIX 单引号格式不兼容而静默失效；修复后可在 Windows 上正常工作
- **PR [#3230](https://github.com/nanocoai/nanoclaw/pull/3230)** — 修复卸载文档指向已废弃的数据/env 镜像的误导性问题
- **PR [#2427](https://github.com/nanocoai/nanoclaw/pull/2427)** / **PR [#2752](https://github.com/nanocoai/nanoclaw/pull/2752)** — Discord 附件（图片/文本）无法以可读形式到达 agent 的修复方案（两条长期未解决的问题，详见下文积压章节）


## 6. 功能请求与路线图信号

今日无新功能请求 Issue。但两条待合并的功能性 PR 持续更新中，信号较强：

| PR | 类型 | 说明 | 等待时长 |
|---|---|---|---|
| [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) | **新渠道（Feature Skill）** | 新增 **Dial 渠道适配器**（SMS + AI 语音通话），这是全新渠道集成，意味着 NanoClaw 可能将触达扩展到语音/SMS 通信场景 | **32 天** |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | **新渠道（Feature Skill）** | 在渠道选择器与向导中正式加入 **Dial** 选项（`runChannelSkill` 模型）——与上面 #3041 配套 | **32 天** |

这两条 PR 配合共同引入一个完整的 Dial 渠道支持能力。**已等待 32 天仍未合入**，如果项目计划在下个版本加入语音/SMS 渠道，这两条 PR 应该在近期被推进合并。


## 7. 用户反馈摘要

今日新增 Issue 中，用户反馈的核心痛点集中在**运行环境兼容性**：

- **用户 `sergeykad`**（[#3245](https://github.com/nanocoai/nanoclaw/issues/3245)）报告在 Intel Celeron J6413/N5105 等低成本低功耗设备上运行预构建镜像时遭遇 SIGILL 崩溃，根据其描述，这类设备（Tremont/Elkhart Lake 架构，无 AVX2）在 NAS、软路由、迷你主机场景非常普遍。诉求指向项目需要提供 baseline x64 或条件检测机制。
- **用户 `glifocat`**（[#3248](https://github.com/nanocoai/nanoclaw/issues/3248)）指出 Node 版本检测逻辑存在断链——检测判定"过旧"，但安装脚本却不实际安装新版本，最后以陈旧环境继续运行。用户在描述中逐一标注了相关代码行，已给出明确修复路径。

两条反馈的共同点在于：**项目对环境的假设比实际用户环境要"新"**——AVX2 指令集和 Node ≥ 20 都构成了隐性的硬件/软件门槛，而这在用户的部署场景中不被满足。如果项目目标是覆盖更多消费级硬件和低端设备，这两类问题值得在路线图中被纳入考量。


## 8. 待处理积压

以下为长期未闭合的重要 Issue/PR，建议维护者关注：

| 类型 | 编号 | 标题 | 等待时长 | 备注 |
|---|---|---|---|---|
| 🔴 PR | [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) | fix: stage inbound attachments that expose only a url (Discord) | **64 天** | Discord 附件（文本/图片）无法被 agent 读取的问题，长期未合并。 | 
| 🔴 PR | [#2427](https://github.com/nanocoai/nanoclaw/pull/2427) | fix: attachment issues | **95 天** | 与 #2752 同一领域的附件问题修复（关闭 #2426），已近 3 个月。两条 PR 功能上有重叠部分，建议维护者尽快协调合并或关闭。 |
| 🟡 PR | [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) | feat(channels): add Dial channel adapter (SMS + AI voice calls) | **32 天** | 新渠道集成，等待超一个月无合入动作。 |
| 🟡 PR | [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | feat(setup): add Dial to the channel picker + wizard/skills | **32 天** | 与 #3041 配套的向导侧支持。 |
| 🟡 Issue | — | *（无长期未响应的 Issue）* | — | 当前 Issue 积压较少，维护及时。 |

**重点提醒**：附件问题在 Discord 渠道上已连续存在 2-3 个月（#2752 于 6 月 12 日创建，#2427 可追溯到 5 月 12 日），且两个 PR 相互关联但均未合入，建议维护团队协调讨论设计方案，尽快给出结论，避免长期分叉。


## 项目健康度总评

| 维度 | 状态 |
|---|---|
| **Issue 响应速度** | ✅ 良好（新 Issue 当日/次日即有反馈，部分已有修复 PR） |
| **PR 合并速度** | ⚠️ 一般（修复类 PR 合入速度尚可，但渠道类功能 PR 平均等待超 30 天） |
| **Bug 修复动向** | ✅ 积极（今日 4 条新修复 PR，核心供应链修复已合并） |
| **社区活跃度** | 🟡 中等（无高讨论量条目，但提交频率稳定） |
| **供应链安全** | ✅ 良好的自动验证链路已建立，今日演练验证通过 |

**重要趋势**：NanoClaw 在供应链安全上投入明显（多轮签名验证演练、验证逻辑修复），同时修复 PR 的code review 流程较完善（每条 PR 均附带规范标签）。风险点在于**功能型 PR 长期积压**（30-95 天不等）和 **旧硬件支持不足** 两个方向。后者若持续存在，可能在用户基数扩大后成为负面口碑因素。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-15

## 1. 今日速览

过去24小时内，NullClaw 项目活跃度较低。**无新增 Issue（新开 0 / 关闭 0）**，仅有 **1 条 PR 活动**（#986，且已关闭）。**无新版本发布**。核心进展集中在 SQLite 内存数据库路径可配置化改进，该 PR 已合入主分支（关闭状态），为只读工作区部署场景提供关键灵活性。整体来看，项目处于平稳迭代阶段，社区交互热度一般，开发节奏偏向小步快进的稳定性维护方向。

---

## 2. 版本发布

**今日无新版本发布。** 最新 Releases 无更新，建议关注后续主分支累积的变更是否会催生 0.x 系列小版本发布。

---

## 3. 项目进展

### 合并/关闭 PR 分析

**#986 — GEN-548: make SQLite memory database path configurable**  
*作者: gently-whitesnow | 创建/更新: 08-14 | 状态: 已关闭（合并）*  
🔗 [查看 PR](https://github.com/nullclaw/nullclaw/pull/986)

**核心变更：**
- 新增 `memory.database_path` 配置项，用于 SQLite 主内存引擎
- 该配置为空时，保持原有 `<workspace>/memory.db` 默认位置
- 支持相对路径（基于工作区解析）与绝对路径（面向只读工作区部署）
- 配置说明已同步至示例/文档文件

**项目意义：**  
这一改动解决了特定部署环境下（如容器化、只读文件系统、多实例隔离）数据库路径不可控的问题。虽不涉及架构性重构，但属于**部署灵活性和可运维性**的实质性提升，填补了配置体系中的一个已知空白。项目整体向前迈出的幅度不大，但方向明确——持续打磨工程化能力。

---

## 4. 社区热点

**今日无高讨论量 Issue 或 PR。** 唯一活跃的 PR #986 已在当日完成合并/关闭，未形成多轮讨论（评论数: undefined，👍: 0）。社区整体处于静默期，无明显的需求争吵或方向性辩论。

---

## 5. Bug 与稳定性

**今日无新增 Bug、崩溃或回归问题报告。** 零缺陷报告日，从稳定性角度属于健康信号。若从谨慎角度看，也可能意味着社区使用量有限或问题未被触发，建议结合近一周 Issue 趋势综合判断。目前无待处理的 P0/P1 缺陷。

---

## 6. 功能请求与路线图信号

**今日无新增功能请求 Issue。**  
从 PR #986 的合并来看，可以捕捉到一个明确的路线图信号：**部署配置弹性的持续增强**。该改动大概率来源于实际用户或内部开发在只读工作区（如 CI 环境）中的真实痛点，预计下一版本（若有）将包含此功能。值得关注的是，内存数据库路径的配置化可能只是第一步，后续可能延伸出共享内存、外部数据库连接等更多存储选项需求。

---

## 7. 用户反馈摘要

**今日无可用 Issue 评论数据。** 无新增用户反馈可提炼。此部分暂缺，建议在社区活跃期（如功能发布后）加强评论挖掘，以更准确地捕捉用户对配置复杂度、默认行为兼容性等方面的真实态度。

---

## 8. 待处理积压

**今日无新增积压项。** 当前无长期未响应的 Issue 或 PR 浮出水面。建议维护者定期清理长期未更新的旧 Issue（如超过 90 天无维护者回应的），以避免隐性积压。同时，鉴于今日 PR #986 快速合并，可以推断当前的维护者响应周期保持在高效水平（创建到关闭 < 24 小时）。

---

> **健康度评估：** ★★★☆☆（中等偏上）  
> 零新缺陷 + 单 PR 快速合入 → 稳定可控。但社区互动极低、无版本释放，项目增长动能略显不足。建议下一步可关注：① 推进更高频的里程碑版本发布；② 在 Release Notes 中强化对 #986 这类工程化改进的对外宣传，提升社区感知度。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-15

---

## 1. 今日速览

IronClaw 在过去 24 小时保持高强度迭代节奏：共处理 25 条 Issue 和 46 条 PR，其中 9 条 Issue 关闭、23 条 PR 完成合并。**v1.3.0 自动化可靠性（epic #6879）是今日最集中的工作主线**，共有 6 条相关联的子 Issue 和 4 条关联 PR 活跃推进。Q1 的 bug bash 反馈也持续涌入，暴露了 Slack/Telegram 渠道集成和扩展隔离方面的若干 P2 级问题。整体项目健康度为**良好**——核心重构（unbound-turns 模型切换）的 71 条款一致性审计已通过，且 1.2.0 发布线已合并回主分支，版本收敛有序。

---

## 2. 版本发布

**今日无新版本发布。** 相关工作动态：

- PR [#7657](https://github.com/nearai/ironclaw/pull/7657) 已将验证过的 `release/2026-08-11`（IronClaw 1.2.0）合并回 `main`，包括 1.0/1.1→1.2 启动迁移、Windows 文件系统/冒烟修复、release artifact 升级 canary 等。
- PR [#7663](https://github.com/nearai/ironclaw/pull/7663)（OPEN）正在将 1.2 的独立验证修复前向移植到当前 `main`：线程索引投影修复、Windows 文件系统/冒烟可靠性、干净的 Windows JSON 输出、以及运行时 `curl` 健康检查。

---

## 3. 项目进展

今日合并/关闭的高价值 PR：

| PR | 标题 | 状态 | 关键推进 |
|---|---|---|---|
| [#7562](https://github.com/nearai/ironclaw/pull/7562) | unbound-turns 设计 + 阶段 1（prepared-context 接受门、unbound 运行通道、kernel 绑定引用删除） | ✅ 合并 | 为后续无界轮次模型奠定基础 |
| [#7658](https://github.com/nearai/ironclaw/pull/7658) | Telegram 迁移 DC 上的 2FA 门槛识别 + 登录码到达位置提示 | ✅ 合并 | 修复 linked-device QA 第一天的两个核心缺陷 |
| [#7652](https://github.com/nearai/ironclaw/pull/7652) | 生产 DB 写入工作负载测量 | ✅ 合并 | 为 DB 写压力 epic #7591 提供基线数据 |
| [#7665](https://github.com/nearai/ironclaw/pull/7665) | 支持 origin-scoped hosted MCP OAuth | ✅ 合并 | 为 MKT1 的 hosted MCP 端点提供受控 OAuth 支持 |
| [#7666](https://github.com/nearai/ironclaw/pull/7666) | 扩展卡片与安装结果"说真话"（QA #7660 + 安装引导） | ✅ 合并 | 修复扩展 UI 误导性状态展示 |
| [#7668](https://github.com/nearai/ironclaw/pull/7668) | 扩展 provider 认证诊断信息透传 | ✅ 合并 | 将 GitHub provider 错误码/消息穿过 WASM、ABI、capability 等全路径 |

**自动化可靠性（#6879）** 主线下，今日 6 条子 Issue 全部处于 OPEN 状态且有对应 PR 推进：确定性无投递结果（[#7647](https://github.com/nearai/ironclaw/issues/7647) ↔ [#7651](https://github.com/nearai/ironclaw/pull/7651)）、预检授权与 standing approval lease（[#7646](https://github.com/nearai/ironclaw/issues/7646)）、模型 profile 锁定（[#7645](https://github.com/nearai/ironclaw/issues/7645)）、arming 前契约验证（[#7644](https://github.com/nearai/ironclaw/issues/7644)）、语义执行结果持久化（[#7650](https://github.com/nearai/ironclaw/pull/7650)）。这套设计表明团队正在系统性地将自动化从"碰运气"改造为"结构化契约 + 确定性投递"的工程体系。

**unbound-turns 训练**：PR [#7634](https://github.com/nearai/ironclaw/pull/7634)（OPEN，XL）完成了向 prepared-context turns 模型的全面切换，包含 71 条款一致性审计。

---

## 4. 社区热点

**今日讨论最集中的两个议题：**

**① 自动化执行可靠性（#6879）** — 这是贯穿 v1.3.0 的核心痛点。Issue 作者 serrrfirat 指出："**同一个存储的 prompt，有时成功有时完全无产出，尤其在 DeepSeek V4 Flash 等小模型上**"，并明确审计结论为**结构性缺陷**而非模型噪声：trigger fire 被当作普通交互式聊天轮次执行。这一洞察驱动了整套"结构化执行契约"设计。相关 PR 讨论围绕 `[SILENT]` 确定性抑制、per-model pinning、preflight grants 等展开，反映出社区对**自动化可预测性**的强烈诉求。

**② 插件化内存（#7664）** — serrrfirat 提出的 MCP-backed 内存提供者方案（[PR #7661](https://github.com/nearai/ironclaw/pull/7661)）将 IronClaw 内存从编译期工厂分支改用**配置绑定**，以 Mnesis Core 为首个消费者。这是架构层面的开放化信号，社区关注点在于"记忆系统可替换"的能力是否会被纳入 v1.3.0。

其余高活跃条目集中在 QA bug bash 反馈（Slack 状态显示错误 #7660、Telegram MP4 附件失败 #7662）。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 P2 | [#7662](https://github.com/nearai/ironclaw/issues/7662) | **Telegram MP4 附件上传失败** — `attachments.mime_type` 报 `invalid_value`，即使文件已被识别为 `video/mp4` | 待修复，无对应 PR |
| 🔴 P2 | [#7660](https://github.com/nearai/ironclaw/issues/7660) | **Slack UI 显示 "Reconnect" 和 "Finish Setup"** — 即使连接实际正常且可用 | 已有 fix PR [#7666](https://github.com/nearai/ironclaw/pull/7666)（已合并） |
| 🟡 P2 | [#7659](https://github.com/nearai/ironclaw/issues/7659) | **扩展状态跨用户泄漏** — 非当前用户安装的扩展显示为已安装 | 待修复，无对应 PR |
| 🟡 P2 | [#7667](https://github.com/nearai/ironclaw/issues/7667) | **Telegram 手机模式登录码提示不准确** — `sentCode.type_` 未反映实际投递方式，用户收不到验证码 | 待修复，无对应 PR |
| 🟢 低 | [#7655](https://github.com/nearai/ironclaw/pull/7655) | CI 集成测试覆盖率阈值重新固定 | ✅ 已修复 |

---

## 6. 功能请求与路线图信号

**明确进入 v1.3.0 范围：**

- **结构化自动化执行契约**（#6879 的子集）：确定性 no-delivery 抑制（[#7647](https://github.com/nearai/ironclaw/issues/7647)）、preflight grants 与 standing approval lease（[#7646](https://github.com/nearai/ironclaw/issues/7646)）、per-automation LLM model pinning（[#7645](https://github.com/nearai/ironclaw/issues/7645)）、arming 前语义验证（[#7644](https://github.com/nearai/ironclaw/issues/7644)）—— 这些共同将自动化从"不可预测的 prompt 执行"升级为"有契约、有验证、有确定结果"的工程化机制。
- **插件化内存（[#7664](https://github.com/nearai/ironclaw/issues/7664)）**：MCP-backed memory provider，配置绑定而非编译期分支。PR #7661 已开，可能进入 v1.3.0。
- **WebUI 结构化 Ask User 卡片（[#7653](https://github.com/nearai/ironclaw/issues/7653)）**：OMP 风格、模型可调用的 `ask` 工具。

**值得关注的设计系统工作**：

- [#7637](https://github.com/nearai/ironclaw/issues/7637) 类型化 design-system 组件边界、[#7639](https://github.com/nearai/ironclaw/issues/7639) 共享 InlineNotice 组件、[#7638](https://github.com/nearai/ironclaw/issues/7638) 用全局 toast 替换阻塞式 alert —— 这些虽非功能新特性，但反映前端代码质量持续提升。

---

## 7. 用户反馈摘要

- **自动化不可靠是最大用户痛点**（#6879）："同一个 stored prompt 有时成功有时什么也不产出"，尤其在 DeepSeek V4 Flash 上。用户期望自动化有可预测的输出，而不是"碰运气"。
- **DOCX 生成损坏问题**（[#6869](https://github.com/nearai/ironclaw/issues/6869)，已关闭）：用户 Davin Basi 反馈 IronClaw 生成标记过的 NDA .docx 文件时，Word 无法打开。对比 ChatGPT/Claude 可轻松完成此任务——这是一个用户可感知的能力差距。
- **用户级 LLM 模型选择缺失**（[#7183](https://github.com/nearai/ironclaw/issues/7183)，已关闭）：来自 Champions 周会的营销团队反馈——模型选择仅限管理员，普通用户无法自选。虽然此 Issue 已关闭，但 v1.3.0 中"per-automation model pinning"（#7645）部分回应了此需求。

---

## 8. 待处理积压

| 类型 | 链接 | 创建时间 | 备注 |
|---|---|---|---|
| ⚠️ PR | [#7379](https://github.com/nearai/ironclaw/pull/7379) — docs-live 分支部署方案 | 08-07 | 已 8 天未合并，doc-truth 系列 4/5 |
| ⚠️ PR | [#7378](https://github.com/nearai/ironclaw/pull/7378) — doc-fact 契约测试 | 08-07 | 已 8 天未合并，doc-truth 系列 3/5 |
| ⚠️ PR | [#7255](https://github.com/nearai/ironclaw/pull/7255) — APDD 治理框架评估 | 08-05 | 已 10 天未合并，文档型 PR，风险评估低 |
| ⚠️ PR | [#7456](https://github.com/nearai/ironclaw/pull/7456) — Reborn 持久存储 profile-agnostic | 08-10 | 已 5 天未合并，涉及 sandbox/CI/依赖，跨领域 PR 可能需要更多 review |
| ⚠️ PR | [#7628](https://github.com/nearai/ironclaw/pull/7628) — 移除 heartbeat journal churn | 08-13 | 性能优化，与 #7591 DB 写压力 epic 相关 |
| ⚠️ Issue | [#7647](https://github.com/nearai/ironclaw/issues/7647) | — | 自动化确定性 no-delivery 机制 — 有配套 PR #7651 |

**维护者关注建议**：doc-truth 系列（#7378、#7379）已停滞 8 天，如果这两个 PR 合入，将显著提升文档与真实行为的一致性保障；PR #7456 涉及存储层 profile 重构，是较大的架构改动，建议加速 review 以避免与后续 unbound-turns 工作产生冲突。

---

*本日报由 AI 自动生成，数据截至 2026-08-15T00:00:00Z。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-15

> 数据统计区间：2026-08-14 至 2026-08-15（UTC）

---

## 1. 今日速览

LobsterAI 项目今日活跃度**较高**。过去 24 小时内，项目发布了 1 个新版本（2026.8.14），合并/关闭了 22 个 PR，另有 5 个 PR 待合并。合并的 PR 主要聚焦于 cowork 会话体验优化（UI 折叠逻辑、badge 弹窗定位）、OpenClaw 技能启用的键名修复、账户积分图标样式调整及 i18n 文案改进。新开 Issues 仅 2 条，其中一条为功能请求（"快更新 v4pro"），另一条为历史测试补充任务的再次活跃。整体项目健康度良好，发版节奏稳定，社区讨论活跃度呈中等水平。


## 2. 版本发布

**LobsterAI 2026.8.14**（发布于 2026-08-14）

**更新内容：**
- `feat(sidebar)`：支持签到与 Banner 轮播（[#2411](https://github.com/netease-youdao/LobsterAI/pull/2411)，作者 @btc69m979y-dotcom）
- `feat(sidebar)`：新增多智能体任务活动筛选器（[#2418](https://github.com/netease-youdao/LobsterAI/pull/2418)，作者 @liuzhq1986）
- `feat(sidebar)`：侧边栏移动端相关调整（Release notes 截断，详情见[发布页](https://github.com/netease-youdao/LobsterAI/releases)）

**破坏性变更与迁移注意事项：** 发布说明未标注任何破坏性变更。若遇异常，建议查阅 [Release 完整页面](https://github.com/netease-youdao/LobsterAI/releases) 获取更多信息。


## 3. 项目进展

今日合并/关闭的 22 个 PR 中，值得关注的重点推进如下：

| 方向 | PR | 说明 |
|------|-----|------|
| **cowork 会话体验** | [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) | 修复会话回合在等待父协程恢复时提前折叠的问题——现在必须等到有回答内容后才折叠 |
| **cowork 会话体验** | [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) | 修复 badge 弹窗超出视口边界的问题，确保弹窗正确显示在后续消息之上 |
| **cowork 会话体验** | [#2490](https://github.com/netease-youdao/LobsterAI/pull/2490) | 支持在 artifact 面板中预览浏览器批注截图，替代原先的通用图片预览弹窗 |
| **OpenClaw 技能修复** | [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491) | 修复技能 UI 开关静默失效的问题——改为按 frontmatter name 键控 skills.entries（[#2483](https://github.com/netease-youdao/LobsterAI/pull/2483) 为另一作者同日提交的同功能修复，已合并） |
| **UI / 排版** | [#2495](https://github.com/netease-youdao/LobsterAI/pull/2495) | 上调默认 UI/代码字体大小，附带一次性迁移 |
| **账户** | [#2492](https://github.com/netease-youdao/LobsterAI/pull/2492) / [#2494](https://github.com/netease-youdao/LobsterAI/pull/2494) | 积分图标颜色对齐与新版样式替换 |
| **i18n** | [#2497](https://github.com/netease-youdao/LobsterAI/pull/2497) | 改进 cowork goal 与 steer 的文案措辞 |
| **主分支合并** | [#2498](https://github.com/netease-youdao/LobsterAI/pull/2498) | 将 `release/2026.7.30` 合并入 main（67 commits，264 文件变更，+24,736/−4,253），引入 Team Edition 账户与配额流、Skills 与 Connectors 体验刷新 |

**总体评估：** 社区版（开源）主分支今日持续推进，老版本 release 分支向 main 合并是较大的一次增量，说明 2026.7.30 版本积累的变更已完整回归主线。项目在 cowork 交互细节、OpenClaw 集成正确性方面保持高频迭代。


## 4. 社区热点

| 条目 | 类型 | 评论数 | 说明 |
|------|------|--------|------|
| [#2489](https://github.com/netease-youdao/LobsterAI/issues/2489) | Issue（功能请求） | 1 | 用户 @nimamasl114514 发出 "快更新v4pro！"，表达对 v4 Pro 版本的支持期待 |
| [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154) | Issue（测试补充） | 1 | 明确提出为 `commandSafety` 与 `coworkMemoryJudge` 补充 Vitest 单元测试的诉求，评论区 1 条讨论 |
| [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) | PR（待合并） | 截至统计窗口未再增加 | 新增"设置→通用"中永久隐藏侧边栏广告 Banner 的开关，回应了此前 [#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) 的用户请求 |

**诉求分析：** 热点集中在两块：(1) 用户对 v4 Pro 版本的迫切期待（Issue #2489 虽内容简短但反映用户对项目未来的关注与催促）；(2) 对广告展示控制权的诉求将持续存在——PR #2374 仍未合并，意味着用户目前只能暂时关闭单个 Banner，无法永久禁用。


## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 |
|----------|----------|------|
| 🟢 低 | **OpenClaw 技能 UI 开关静默失效**（[#2491](https://github.com/netease-youdao/LobsterAI/pull/2491) / [#2483](https://github.com/netease-youdao/LobsterAI/pull/2483)）：目录名与 frontmatter name 不一致时，UI 开关无效果，属于静默逻辑错误 | 已有 fix PR 合并 |
| 🟢 低 | **cowork 回合提前折叠**（[#2499](https://github.com/netease-youdao/LobsterAI/pull/2499)）：回合在等待父协程恢复时被错误折叠显示为失败 | 已有 fix PR 合并 |
| 🟢 低 | **badge 弹窗定位**（[#2496](https://github.com/netease-youdao/LobsterAI/pull/2496)）：弹窗可能超出视口边界或被后续消息遮挡 | 已有 fix PR 合并 |
| 🟢 低 | **buildOpenAIChatCompletionsURL 拼接错误**（[#1153](https://github.com/netease-youdao/LobsterAI/pull/1153)）：Google Gemini baseURL 以 `/v1` 结尾时 URL 拼接缺少 `/` 分隔符 | 仍 open（stale 标记） |
| ⚪ 信息 | 今日无新增高危 Bug、崩溃或回归报告发布 | — |

**整体评估：** 项目今日无高危缺陷报告，三个低严重度问题均在同日完成修复并合并。


## 6. 功能请求与路线图信号

| 请求 | 类型 | 当前状态 | 纳入下一版本的可能性 |
|------|------|----------|---------------------|
| **永久隐藏侧边栏广告 Banner**（[#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) → [PR #2374](https://github.com/netease-youdao/LobsterAI/pull/2374)） | 用户体验设置 | PR 已 open，待合并 | 高——实现已完成，应在 2026.8.x 后续版本或 v4 中合入 |
| **为 commandSafety 与 coworkMemoryJudge 补充测试**（[#1154](https://github.com/netease-youdao/LobsterAI/issues/1154)） | 测试覆盖 | Issue open，暂无关联 PR | 中——两个模块为核心安全/质量关卡（command 执行、记忆写入），应纳入后续迭代 |
| **v4 Pro 发布**（[#2489](https://github.com/netease-youdao/LobsterAI/issues/2489)） | 版本期待 | 等待官方计划 | 视项目路线图/商业化进度而定 |

**路线图信号：** 代码库中已出现 Team Edition 账户/配额流（[#2498](https://github.com/netease-youdao/LobsterAI/pull/2498)）这类商业化能力的代码合并，结合用户对"v4 Pro"的催促，说明项目在开源版之外正在推进面向团队/企业级的能力建设，下一步版本可能包含多用户/配额管理等功能。


## 7. 用户反馈摘要

- **对广告的控制权诉求明确**：用户对侧边栏 Banner 仅能"一次性关闭"感到不便，要求提供**永久关闭**选项（[#2342](https://github.com/netease-youdao/LobsterAI/issues/2342)），已获 PR 实现但尚未合并。
- **对 v4 Pro 版本的迫切期待**：用户 @nimamasl114514 在 [#2489](https://github.com/netease-youdao/LobsterAI/issues/2489) 中直接催促"快更新v4pro！"，显示了核心用户群体的版本升级意愿。
- **安全/质量模块的测试诉求**：社区用户（@MaoQianTu）主动提交了为 `commandSafety` 和 `coworkMemoryJudge` 补充测试的 Issue，明确阐述了两个模块误判可能导致的破坏性后果（如误执行 `rm -rf`, 或大量无关内容写入记忆），体现了用户对安全可靠性的关注。
- **无负面体验抱怨**：今日 Issues 中暂无明显的使用体验负面反馈。

**总体评价：** 用户反馈以功能/版本期待为主，无对现有功能的系统性不满。社区对项目安全机制较为关注。


## 8. 待处理积压

| 类型 | 条目 | 创建时间 | 最近更新 | 积压时长 | 说明 |
|------|------|----------|----------|----------|------|
| Issue | [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154) — 为 commandSafety/coworkMemoryJudge 补充 Vitest 测试 | 2026-03-31 | 2026-08-14 | ~4.5月 | 涉及核心安全模块，建议优先响应 |
| PR | [#1153](https://github.com/netease-youdao/LobsterAI/pull/1153) — 修复 Gemini /v1 路径 URL 拼接错误 | 2026-03-31 | 2026-08-14 | ~4.5月 | 明确的 bug fix，测试场景清晰，等待 review |
| PR | [#1155](https://github.com/netease-youdao/LobsterAI/pull/1155) — 会话内页内搜索（Ctrl+F） | 2026-03-31 | 2026-08-14 | ~4.5月 | 高价值 UX 功能，实现完整，建议 review |
| PR | [#1228](https://github.com/netease-youdao/LobsterAI/pull/1228) — 会话"标记为未读"功能 | 2026-04-01 | 2026-08-14 | ~4.5月 | 功能完整，已合并至 release 分支？有待确认 |
| PR | [#1231](https://github.com/netease-youdao/LobsterAI/pull/1231) — AgentCreateModal Escape 关闭支持 | 2026-04-01 | 2026-08-14 | ~4.5月 | UX 一致性改进 |
| PR | [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) — 永久隐藏侧边栏广告 Banner | 2026-07-21 | 2026-08-14 | ~3.5周 | 已有用户诉求，建议尽快合并 |

**维护者提醒：** 多条自 2026-03-31 起的 PR/Issue 被标记为 stale 后仍在等待处理，涉及安全测试（#1154）、明确的 bug 修复（#1153）及高价值功能（#1155、#1228）。建议在下一个版本规划中优先清算这批积压，以提升社区参与者的贡献积极性。另注意 [#1231](https://github.com/netease-youdao/LobsterAI/pull/1231) 与 [#1228](https://github.com/netease-youdao/LobsterAI/pull/1228) 状态标记为 CLOSED，但功能落地情况需在 main 分支中进一步确认。

---

*本日报由 LobsterAI GitHub 数据自动生成，数据统计窗口为 2026-08-14 至 2026-08-15（UTC）。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报

**日期：2026-08-15** | **数据窗口：2026-08-14 至 2026-08-15**  
**数据版本**: 基于 2026-08-15 数据快照分析

---

## 1. 今日速览

**项目活跃度：低但聚焦**。过去 24 小时内无新 Issue 提交、无 Issue 关闭，Issue 生态处于静默状态；PR 侧仅有 1 条待合并 PR #1190（连接器基础设施），该 PR 由核心维护者 penso 提交，更新于昨日，说明核心功能开发仍在推进但节奏放缓。近期无新版本发布，项目可能正处于大版本迭代的前置积累期——PR #1190 所引入的连接器持久化层大概率是下一版本的核心地基。整体来看，项目处于“开发深水区、社区讨论清淡”的阶段，需要关注长期未合并 PR 对贡献者积极性的潜在影响。

---

## 2. 版本发布

**今日无新版本发布。** 上一次发布信息未在数据窗口内呈现，建议关注 PR #1190 合并后的版本规划公告。

---

## 3. 项目进展

**关键 PR 推进情况**（今日无合并/关闭的 PR，但以下 PR 有状态更新）：

| PR | 状态 | 更新内容 | 影响评估 |
|----|------|----------|----------|
| [#1190](https://github.com/moltis-org/moltis/pull/1190) — Add durable calendar, channel, and email connectors | 🟡 待合并 | 昨日（08-14）有更新，作者为 penso | 若合并，将为 Moltis 引入**持久化连接器层**，支持日历（CalDAV）、邮件（Gmail/ Himalaya v2）和频道历史的原子快照、调度、投影及本地全文搜索能力 |

**里程碑意义解读**：该 PR 是典型的“基础设施型”改动——它不直接面向最终用户，而是为多提供方连接建立统一持久化框架。值得关注的技术亮点：① **Provider-owned schemas**（数据模型归各提供方所有，而非平台统一强加），这对生态扩展至关重要；② **无凭据复制**（no copied credentials），直接回应了安全审计中的常见痛点；③ **Provider-scoped trust** 机制的引入，意味着连接器权限边界将被显式声明。

> ⚠️ 该 PR 已开放 4 天且评论数未知，建议维护团队评估是否需要追加 Reviewer 以避免长期滞留。

---

## 4. 社区热点

**今日无高讨论量议题。** 目前唯一活跃的 PR #1190 评论数未披露（数据字段为 undefined），这本身是一个信号——该 PR 缺乏社区讨论声音，可能存在以下风险：
- 设计方案未经过充分社区评审，尤其是“Provider-owned schemas”与 Moltis 现有数据模型的一致性需要额外确认；
- 潜在的 breaking changes 未被提前广而告之。

**建议**：维护者可主动在 PR 内 @ 相关模块的活跃贡献者，发起一次架构评审。

---

## 5. Bug 与稳定性

**今日无新增 Bug 报告。** Issue 生态在 24 小时内无新开、无关闭、无活跃更新。项目当前没有公开的崩溃/回归问题暴露。但需注意：**Issue 静默不一定等于系统稳定**，结合 PR #1190 涉及“原子快照”和“调度”能力，下一阶段建议重点回归测试定时任务场景的数据一致性。

---

## 6. 功能请求与路线图信号

**今日无用户提交的新功能需求。**

**路线图前瞻信号（基于 PR #1190）**：该 PR 明确指向三个功能域——**持久化日历连接、频道历史、邮件连接**。结合“bounded local full-text search”（有界本地全文搜索）的引入，可以推测：

- **短期（下一版本）**：本地搜索能力将显著增强，用户将能离线检索历史消息与日历条目；
- **中期（1-2 个版本后）**：多提供方连接器将成为标准 API，第三方开发者可基于 Provider-owned schemas 构建自定义连接器；
- **潜在破坏性变更**：若该 PR 触及配置格式或连接器注册机制，现有用户的连接配置可能需要迁移。

---

## 7. 用户反馈摘要

由于过去 24 小时无 Issue 评论活动，今日无直接的用户之声可引用。但从 PR #1190 的设计意图可以侧面推断用户侧的隐性诉求：

| 推断诉求 | 证据 | 对应设计 |
|----------|------|----------|
| **连接稳定性** | 用户多次配置连接后丢失/失效 | 原子快照 + 调度机制 |
| **数据安全边界** | 用户对连接器存储凭据存有疑虑 | 无凭据复制 + Provider-scoped trust |
| **离线检索需求** | 用户希望不依赖云端 API 也能搜索历史 | Bounded local full-text search |

> 建议在 PR #1190 合并后，发布一篇 Changelog 解释上述设计决策如何解决既有痛点，以回应社区关切。

---

## 8. 待处理积压

**当前唯一的 PR (#1190) 已处于待合并状态 4 天**，值得重点关注：

| 项目 | 详情 |
|------|------|
| PR [#1190](https://github.com/moltis-org/moltis/pull/1190) | 作者: penso；创建: 08-11；最后更新: 08-14；已开放 4 天 |
| **积压风险** | ① 评论数为 undefined，说明未形成评审对话；② 涉及多模块（calendar/email/channel）的跨切面改动，若无充分 review 可能引入隐性回归；③ 长期搁置会延迟依赖该 PR 的后续工作 |
| **紧急度** | 中 — 基础设施型 PR 不应在开发分支上停留过久 |

**其他**：Issue 侧无长期未响应的公开议题。

---

*本报告由 AI 分析师自动生成，数据来源：Moltis GitHub 仓库（数据快照 2026-08-15）。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-15

*数据周期: 2026-08-14 至 2026-08-15 | 数据来源: github.com/agentscope-ai/CoPaw*


## 1. 今日速览

CoPaw 项目昨日至今日活跃度处于**较高水平**，共产生 50 条 Issue 更新和 41 条 PR 更新，但**无新版本发布**。Issue 关闭率较高（76%，38/50），表明维护团队响应迅速；PR 待合并数量较多（26 条待合并 vs 15 条已合并/关闭），存在一定积压。社区讨论集中在几个关键痛点上：**多 UI 会话间的会话身份串扰**（#7011）、**MCP 工具在 2.0 升级后失效**（#6405）、**QwenPaw Creator 插件导致其他插件全部失效**（#7025）、以及 **Scroll 上下文压缩后聊天记录不可见**（#6951）。值得关注的是，多名贡献者（如 Ferrum360）在同一天内连续提交多轮 PR，显示外部贡献活跃度良好。项目整体呈现"**高吞吐、快响应、积压可控**"的健康态势。


## 2. 版本发布

过去 24 小时内无新版本发布。当前可关注的最新版本为 **v2.1.0**（社区反馈中已有多位用户提及，推测为近期发布版本）。与之相关的已知兼容性问题包括：AgentScope 2.0.4.post1 与 QwenPaw 2.0.1 的兼容性崩溃（#6612），以及 MCP 工具在 2.0 升级后提示 Tool not found（#6405），建议维护者尽快推进 agentscope 2.0.6 的依赖升级 PR（#6908）。


## 3. 项目进展

今日合并/关闭的 PR 中，以下几项值得关注：

| PR | 内容 | 状态 |
|----|------|------|
| [#7030](https://github.com/agentscope-ai/QwenPaw/pull/7030) / [#7031](https://github.com/agentscope-ai/QwenPaw/pull/7031) | **技能系统动态加载 + 自动卸载 + frontmatter 修复** — 新增 load_skill/unload_skill/check_skill_status 工具链、AutoUnloadHook（每 5 轮自动卸载闲置技能）、修复 frontmatter description 读取与 lazy skill 路径问题 | 已关闭（后在 #7033 重新提交并保持 OPEN，可能是重推） |
| [#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) | **OneBot 渠道入站媒体本地化** — 将 OneBot 的图片、音视频、文件在进入 Agent 前统一解析并下载到受管本地存储，对齐 AgentScope 2.0 DataBlock 管线 | 已合并 |
| [#6943](https://github.com/agentscope-ai/QwenPaw/pull/6943) | **插件渠道交互式配置器恢复** — 恢复对插件渠道 `get_configurator()` 的支持，使用临时 FastAPI 应用加载插件 HTTP 路由 | 已合并 |
| [#2105](https://github.com/agentscope-ai/QwenPaw/pull/2105) | **Whisper 本地语音转文字安装文档** — 补充 `--extras whisper` 安装说明（中英文） | 已关闭 |

**综合评估：** 今日合入的 PR 主要推进了**渠道层（OneBot 媒体处理、插件配置器）**和**技能系统基础设施**（动态管理、自动卸载）两大方向，属于"地基加固"性质的工作。技能系统相关 PR 在关闭后立即重新提交，表明作者在根据 Review 反馈迭代中。


## 4. 社区热点

今日讨论热度最高的几个议题反映出用户的集中诉求：

**[#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) — Console 停止请求可取消活跃的飞书会话（多 UI 会话身份串扰）**（5 条评论，OPEN）
> 作者在更新中纠正了最初的描述，新证据表明**两个 UI 会话之间会话身份值发生交叉后**，Console UI 的停止请求直接取消了一个活跃的飞书会话。这是一个**严重的多会话隔离问题**，涉及 2.1.0 版本的核心会话管理机制。

**[#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) — 升级 2.0 后 MCP 工具总是提示 Tool not found**（6 条评论，CLOSED）
> 用户报告升级 2.0 后 MCP 工具的 naming convention 变为 `[mcp-key]__[tool_name]`，但调用时总是找不到。Docker 版 2.0.0.post3 环境。该问题已关闭，但结合 #6958（FastMCP 数据重复写入）和 #7016（工具调用 404），**MCP 工具链在 2.x 上仍存在多个不稳定点**。

**[#7025](https://github.com/agentscope-ai/QwenPaw/issues/7025) — QwenPaw Creator 插件导致所有其他插件失效**（4 条评论，OPEN）
> 安装 QwenPaw Creator 插件后，所有其他插件全部失效。这是一个**插件隔离性**问题，安装一个插件不应影响其他插件的正常运行。

**[#6951](https://github.com/agentscope-ai/QwenPaw/issues/6951) — Scroll 压缩后重新进入会话，压缩前聊天记录不可见**（3 条评论，CLOSED）
> 默认 scroll 策略触发自动压缩后，重新进入会话时压缩前的原始消息不再显示，仅剩内部 eviction index。**上下文压缩不应破坏用户可见的完整 transcript**——这是一个与"压缩只应影响模型输入"理念直接相关的体验问题。

**需求信号：** 多条高讨论度 Issue 集中在 **对话管理体验** 上——单条消息删除（#4001，4 条评论）、会话拆分（#4436）、定时任务不投递（#2554），反映出用户对更精细的对话控制能力有持续且强烈的需求。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 修复状态 |
|--------|-------|------|----------|
| 🔴 严重 | [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | 多 UI 会话间身份串扰，Console 停止请求可取消活跃的飞书会话（2.1.0） | 无 PR，排查中 |
| 🔴 严重 | [#7025](https://github.com/agentscope-ai/QwenPaw/issues/7025) | QwenPaw Creator 插件导致所有其他插件失效 | 无 PR，排查中 |
| 🟠 中等 | [#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016) | 流式会话中工具调用 offload 接口返回 404 "Tool call not found"（2.1.0） | 无 PR，排查中 |
| 🟠 中等 | [#6951](https://github.com/agentscope-ai/QwenPaw/issues/6951) | Scroll 压缩后重新进入会话，压缩前聊天记录不可见 | 已关闭（修复或转内部处理，需确认） |
| 🟡 一般 | [#6958](https://github.com/agentscope-ai/QwenPaw/issues/6958) | FastMCP 返回结构化数据时 tool result 文件写入两份重复数据（2.1.0 b4） | ✅ 已有 PR [#6969](https://github.com/agentscope-ai/QwenPaw/pull/6969)（Under Review） |
| 🟡 一般 | [#6806](https://github.com/agentscope-ai/QwenPaw/issues/6806) | Windows 上 QwenPaw Creator 无法保存模型配置 — 每次报 "Internal Server Error" | 已关闭（附 AI 辅助根因分析） |

**值得注意的稳定性信号：** 多个问题集中在 2.1.0 版本（#7011、#7016、#6958）和 Creator 插件（#6806、#7025）上，提示 2.1.0 可能存在**会话管理和插件隔离方面的回归**。另外 [#6197](https://github.com/agentscope-ai/QwenPaw/issues/6197) 作为较早关闭的 Issue 提示 `nvidia-smi` 挂起可能导致桌面版启动卡死，这类启动阶段的鲁棒性问题值得关注。


## 6. 功能请求与路线图信号

结合今日活跃的 Issue 与 PR，以下功能需求可能在后续版本中落地：

| 需求 | 来源 | 对应 PR | 判断依据 |
|------|------|---------|----------|
| **动态技能加载/卸载** | 社区多轮推动 | [#7033](https://github.com/agentscope-ai/QwenPaw/pull/7033)（OPEN，二次提交） | 作者今日连续提交 3 轮迭代（#7029 → #7031 → #7033），说明正在积极 Review 中，落地概率高 |
| **按会话模型覆盖（per-session model overrides）** | #2763（/models 切换命令）等 | [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)（OPEN，Under Review） | 涉及模型路由的核心 PR，覆盖面广，合并后体验提升明显 |
| **会话标题自动同步** | 用户对会话管理的持续诉求 | [#7032](https://github.com/agentscope-ai/QwenPaw/pull/7032)（OPEN） | 配合 auto-memory 提升会话可扫读性 |
| **DataPaw 原生应用运行时** | 数据分析场景 | [#6940](https://github.com/agentscope-ai/QwenPaw/pull/6940)（OPEN，首次贡献者） | 首次贡献者提交的较大功能，需要维护者重点 Review |
| **本地 GGUF 模型零配置运行** | #6433（2 条评论） | — | 仍处于"零配置本地模型"早期需求阶段，暂无 PR 对应 |

**路线图信号：** 技能系统是本阶段最活跃的领域，`skill-system` 相关 PR 在同一主题上出现了三次迭代（#7029/#7031/#7033），加之 #7025 暴露的插件冲突问题，说明技能/插件体系正处于**架构重构的活跃期**。此外，Provider 统一发现与路由（[#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)，OPEN）仍挂在队列中，该项完成后有望一并解决 #944、#2737 等 Responses API 兼容类问题。


## 7. 用户反馈摘要

从今日 Issues 评论中提炼的真实声音：

**安装与更新体验：**
- "每次都要卸载后再安装太麻烦了" — [#2846](https://github.com/agentscope-ai/QwenPaw/issues/2846) 和 [#3464](https://github.com/agentscope-ai/QwenPaw/issues/3464) 两条 Issue 都在呼吁桌面端支持直接自动更新。这一诉求已存在 4 个月（分别创建于 4/2 和 4/16），至今仍未解决，**是用户最持久的痛点之一**。
- 同一 Issue 还提到 Windows 任务栏显示 Python 图标而非 CoPaw 图标，属于品牌/体验细节问题。

**后台运行（daemon 模式）：**
- "qwenpaw app 只能前台运行，没有真正的后台/守护模式，导致通过 SSH 或脚本启动时命令一直卡住不返回" — [#7010](https://github.com/agentscope-ai/QwenPaw/issues/7010)。对于服务器部署和自动化运维场景是**刚需能力缺口**。

**上下文压缩的透明性问题：**
- "上下文压缩应只影响模型输入，不应破坏用户可见的完整 transcript" — [#6951](https://github.com/agentscope-ai/QwenPaw/issues/6951)。用户对压缩策略的**可预期性和数据安全**有较高要求。

**Channel 渠道使用体验：**
- "The Channel tool does not prompt for approval when required. This makes it impossible to determine whether the tool is being called normally or if it is stuck or pending approval" — [#6819](https://github.com/agentscope-ai/QwenPaw/issues/6819)。审批流程的**可视性不足**会影响用户对系统状态的判断。

**文档与文案细节：**
- "'Stop Running'写成'Stopp Running' 文案错别字很多！速速改！" — [#7040](https://github.com/agentscope-ai/QwenPaw/issues/7040)。虽是低优先级，但在意细节的用户已经开始关注文案质量。


## 8. 待处理积压

以下问题长期未得到明确响应或修复，建议维护者关注：

| 项目 | 创建时间 | 状态 | 建议 |
|------|----------|------|------|
| [#2846](https://github.com/agentscope-ai/QwenPaw/issues/2846) — 桌面端自动更新 + 任务栏图标 | 2026-04-02 | 已关闭（约 4 个月前） | 功能至今未见落地，社区诉求持续。如有 Roadmap 安排，建议在对应 Release 的 changelog 中明确 |
| [#944](https://github.com/agentscope-ai/QwenPaw/issues/944) — 支持仅兼容 Responses API 的 OpenAI-compatible 提供商 | 2026-03-08 | 已关闭（5 个月前） | 与 #3002（GPT-5.3-codex 请求 400）和 #2737 同源，是 **Responses API 兼容性** 的一揽子问题，建议通过 [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)（统一 Provider 发现与路由）一并根治 |
| [#7010](https://github.com/agentscope-ai/QwenPaw/issues/7010) — 缺少真正的后台/守护模式 | 2026-08-14 | 已关闭 | 服务器部署场景的刚需，关闭原因未明确说明，建议确认是否已有内部支持方案 |
| [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) — per-session model overrides（Under Review） | 2026-07-12 | 待合并（超一个月） | 功能本身与社区多次提到的 `/models`、跨 Provider 切换诉求高度呼应，建议尽快完成 Review |
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — 统一 Provider 发现、模型元数据、路由与 Agent 控制 | 2026-07-21 | 待合并（超三周） | 牵涉面较大，建议拆分或明确时间表，避免长期阻塞 |

---

*本日报由 AI 自动生成，数据截至 2026-08-15。所有链接均指向 agentscope-ai/QwenPaw 仓库。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-15

> 数据周期：2026-08-14 至 2026-08-15（基于 GitHub 活动时间戳自动聚合）


## 1. 今日速览

ZeroClaw 仓库过去 24 小时保持**高活跃度**：33 条 Issue 更新（30 条活跃/新开、3 条关闭），50 条 PR 更新（47 条待合并、3 条已合并/关闭）。核心讨论仍集中在三大主题：**运行时安全决策管线（RFC #7142、PR #9996）、插件 egress 网络策略基础（PR #9137/#9580）、以及 Agent 评估框架的落地（Issue #7065/#9967）**。值得关注的新信号包括：代理导出便携包（PR #9986）、ZeroCode 转录复制菜单（PR #9994）、以及 Telegram 模型选择器的增强（Issue #9895）。此外，两个新提交的修复 PR（#9999 输出截断分类、#10002 Google Workspace camelCase 校验）显示社区对细节正确性的关注度正在上升。项目整体处于 **v0.8.5 稳定化窗口期内（截至 8 月 30 日，Issue #9459）**，安全与兼容性修复仍是主线。


## 2. 版本发布

过去 24 小时无新版本 Release。


## 3. 项目进展

过去 24 小时合并/关闭的 PR 共 3 条，公开数据中可见以下两条关闭的 Issue 对应的工作已落地：

| PR/Issue | 标题 | 状态 | 影响 |
|---|---|---|---|
| [#6663](https://github.com/zeroclaw-labs/zeroclaw/issues/6663) (CLOSED) | feat(telegram): show tool-call progress during partial streaming | 已关闭 | Telegram 通道在 `stream_mode = "partial"` 下支持工具调用进度更新（`update_draft_progress`），消除工具执行期间草稿消息无反馈的体验空白。 |
| [#9982](https://github.com/zeroclaw-labs/zeroclaw/issues/9982) (CLOSED) | [Proposal] Hosted memory — ViBo Cloud API | 以 wontfix 关闭 | 营销类 proposal，未进入产品路线图。 |

此外，两个重量级 PR 今日有实质推进（虽未合并，但状态更新至 8 月 14/15 日，且均为 `needs-author-action` 等待作者响应）：

- **[#9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) fix(channels): authorize approval responders** — 将 Telegram/Slack/Lark/Matrix 工具审批绑定到发起对话的聊天/房间，并验证回复者身份是否被适配器的活动对等解析器允许。这修复了**审批回复可能被任意身份接受**的安全漏洞，是 P1 级修复。
- **[#9996](https://github.com/zeroclaw-labs/zeroclaw/pull/9996) fix(security): make action budget accounting atomic** — 在包装工具进入副作用边界前原子地预留发送者作用域的动作预算容量，防止并行调用联合超过 `max_actions_per_hour`。这是对安全策略执行并发正确性的关键修复。

**里程碑进度**：v0.8.5 稳定化窗口（[Issue #9459](https://github.com/zeroclaw-labs/zeroclaw/issues/9459)）推进正常，每周切割发布就绪工作。


## 4. 社区热点

今日讨论热度集中在以下 RFC/设计提案（评论数排序）：

1. **[#8303 RFC: Goal mode v1 — bounded foreground Matrix work](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)**（评论 22，👍 1）
   - 诉求：ZeroClaw 需要一种**跨多轮 agent turn 持久化地追求有界用户目标**的机制。作者明确反对将重启交接、广播通道准入、Web 和异步子工作全部塞进首个交付中，强调**有界的前台工作**优先。
   - 信号：社区对目标导向的 agent 行为有明确需求，但更关注**渐进式交付**而非大爆炸式重构。

2. **[#7155 RFC: Per-execution confirmation tier for high-risk shell commands](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)**（评论 20）
   - 诉求：为高风险 shell 命令增加按执行确认层，并引入 Claude Code 风格的命令模式策略（allow/ask/deny）。维护者已确认范围收缩至 shell 策略契约本身。
   - 信号：安全策略的**可操作性**（如何落地为可配置策略而非抽象原则）是社区持续关注的核心。

3. **[#8603 RFC: ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)**（评论 19）
   - 诉求：ZeroClaw 目前仅通过 WebSocket、ACP 和每个通道的 webhook 暴露 agent 能力，而 OpenAI Chat Completions 协议的客户端（Open WebUI、LobeChat、Continue.dev、Aider、LangChain、OpenAI SDK 等）无法直接接入。
   - 信号：**生态互操作性**（支持标准协议）是社区呼声最高的功能方向之一。

4. **[#7141 RFC: Pluggable inbound authentication and canonical principals](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)**（评论 16，Rev 8）
   - 诉求：可插拔入站认证 + 规范化主体标识。已进入 IAM 里程碑，更新至 Rev 8，显示讨论深度较高。

5. **[#7462 Bug: 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)**（评论 15）
   - 诉求：Windows 11（简体中文、代码页 936）上 74 个测试失败，CI 仅跑 Linux，未能捕获。这是**跨平台兼容性欠债**的典型信号。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 标题 | 描述 | 修复状态 |
|---|---|---|---|---|
| **S1 — 工作流阻断** | [#9421](https://github.com/zeroclaw-labs/zeroclaw/issues/9421) | Incomplete terminal responses can be reported as successful | Provider 可能在未给出可信最终答案的情况下结束回合，但运行时/委派层仍向调用方展示成功。涉及 `provider:reliable`、`provider:anthropic`、`tool:delegate`。 | ⚠️ 已有修复 PR：[#9999](https://github.com/zeroclaw-labs/zeroclaw/pull/9999)（今日提交）— 将精确的 `finish_reason: "length"` 分类为输出 token 限制终止失败，拒绝不完整的非流式文本。 |
| **S1 — 工作流阻断** | [#9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) | fix(channels): authorize approval responders | 工具审批未被绑定到发起对话的聊天/房间，任何有权限的身份可能批准其他上下文的审批。 | 待合并（`needs-author-action`） |
| **S2 — 行为降级** | [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 74 test failures on Windows | CI 仅 Linux；Windows 11 简体中文代码页 936 上有 74 个测试失败（Unix-only 命令、路径语义、控制台编码）。 | 无 fix PR |
| **S2 — 行为降级** | [#9759](https://github.com/zeroclaw-labs/zeroclaw/issues/9759) | bug(quickstart): reject duplicate enabled webhook ports | Quickstart 可暂存多个新通道条目，两个 webhook 别名可能被赋予相同的启用端口（默认 8090），导致冲突。 | 无 fix PR（PR #9605 引入后遗留） |
| **S3 — 轻微问题** | [#9983](https://github.com/zeroclaw-labs/zeroclaw/issues/9983) | Fallback model without vision incorrectly reports cause of error | 支持视觉的 provider 回退到不支持视觉的 provider 时，请求必然失败，但错误消息未指出真正原因（回退模型无视觉能力）。 | 无 fix PR |
| **测试基础设施** | [#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965) | cron custom-shell test hits ETXTBSY under parallel runtime gate | cron 自定义 shell 测试在并行运行时门控下遭遇 ETXTBSY 竞态，导致无关 PR 出现红色必需检查。 | 无 fix PR |
| **安全策略** | [#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486) | High-entropy detector redacts Solana wallet addresses | 高熵检测器将 Solana 钱包地址误判为高熵 token 并脱敏，且 `high_entropy_tokens=false` 无法在通道路径上停止该行为。Telegram 场景受影响。 | 无 fix PR |
| **内存后端** | [#9919](https://github.com/zeroclaw-labs/zeroclaw/issues/9919) | fix(memory): reject Qdrant in builder-only factory without storage config | `create_memory_with_builders` 在无存储配置时将 Qdrant 静默路由到 MarkdownMemory 回退，可能选中错误的持久化层。 | 无 fix PR（Issue 本身描述了修复方案） |


## 6. 功能请求与路线图信号

### 高概率进入下一版本（已有实现 PR 在途）

| 功能 | Issue/PR | 信号强度 |
|---|---|---|
| **Goal mode v1 — 有界前台 Matrix 工作** | [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)（RFC，22 评论，status: accepted） | ★★★ 已接受。明确"有界前台工作"优先，社区共识强。 |
| **Chat Completions profile** | [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)（RFC，19 评论） | ★★★ 生态互操作需求呼声最高，接入 OpenAI 协议客户端生态将显著扩大用户群。 |
| **Agent 导出便携包** | [#9986](https://github.com/zeroclaw-labs/zeroclaw/pull/9986)（feat(agents): export to portable bundle） | ★★★ 已有完整实现 PR（manifest + config closure + workspace tree），待作者响应。 |
| **ZeroCode 转录复制菜单** | [#9994](https://github.com/zeroclaw-labs/zeroclaw/pull/9994)（feat(zerocode): add transcript copy context menu） | ★★★ 今日提交，UI 体验改进，低风险。 |
| **Provider-grouped Telegram /model 选择器** | [#9895](https://github.com/zeroclaw-labs/zeroclaw/issues/9895)（Feature，status: accepted） | ★★☆ 已接受。移动端 /model 命令可用性改进。 |
| **Discord 按角色授权** | [#9970](https://github.com/zeroclaw-labs/zeroclaw/issues/9970)（Feature，status: in-progress） | ★★☆ 多租户/团队场景刚需：`allowed_role_ids` 加性叠加到现有用户 ID 白名单。 |
| **共享 egress 策略基础** | [#9137](https://github.com/zeroclaw-labs/zeroclaw/pull/9137)（feat(plugins): shared egress policy foundation） | ★★☆ 为插件系统提供网络出口策略基础，依赖 #9580。 |

### 路线图信号（RFC/设计阶段）

- **统一包/能力/配置/运行时状态目录契约**（[#9346](https://github.com/zeroclaw-labs/zeroclaw/issues/9346)，RFC，status: accepted）— 产品级目录整合。
- **运行时拥有的会话 + 传输表面适配器**（[#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)）与 **统一附件架构**（[#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)）— 两者为关联 RFC，定义运行时边界与 Web/通道附件统一。
- **分阶段可选产品遥测**（[#9621](https://github.com/zeroclaw-labs/zeroclaw/issues/9621)）— 为维护者提供功能使用数据以支持决策。
- **Agent 评估框架**（[#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065) + [#9967](https://github.com/zeroclaw-labs/zeroclaw/issues/9967) tracker）— 从"无评估方式"到"可重复评估机制"，是长期质量保障的基石。

### 已否决/关闭

- **ViBo Cloud 托管内存**（[#9982](https://github.com/zeroclaw-labs/zeroclaw/issues/9982)）— wontfix，营销类 proposal。


## 7. 用户反馈摘要

| 反馈来源 | 核心诉求/痛点 | 场景 | 项目回应 |
|---|---|---|---|
| [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) Chat Completions profile | "Clients that speak the OpenAI Chat Completions protocol — Open WebUI, LobeChat, Continue.dev, Aider, LangChain, the OpenAI SDK, and many others" 无法接入。 | 用户已有 OpenAI 生态工具链，希望 ZeroClaw 作为 drop-in 后端。 | RFC 讨论中，19 条评论。 |
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 测试失败 | "CI does not catch this because the Test job only runs on Linux" + 简体中文 Windows 环境下代码页 936 引发控制台编码问题。 | 简体中文 Windows 用户/贡献者被排除在 CI 保障之外。 | P1，accepted，无 fix PR。 |
| [#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486) Solana 地址被脱敏 | "An agent with a Solana MCP server cannot state a wallet address. Every address in an outbound Telegram message is replaced with `[REDACTED_HIGH_ENTROPY_TOKEN]`。" 且 `high_entropy_tokens=false` 无法绕过。 | 加密货币/Web3 场景下 Telegram 通道输出被破坏。 | P2，accepted，无 fix PR。 |
| [#9983](https://github.com/zeroclaw-labs/zeroclaw/issues/9983) 视觉回退错误消息误导 | "the messaging does not show that it is due to the fallback model lacking vision" — 用户被误导去排查错误的方向。 | 使用带视觉的主模型 + 不带视觉的回退模型时，视觉请求全部失败且原因不明。 | 新提交，S3，低优先级。 |
| [#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965) ETXTBSY 测试竞态 | "a red required check does not appear on unrelated PRs" — CI 基础设施问题浪费贡献者时间。 | 并行运行时测试门控下 cron 自定义 shell 测试遭遇 ETXTBSY。 | P1，accepted，无 fix PR。 |
| [#9895](https://github.com/zeroclaw-labs/zeroclaw/issues/9895) Telegram /model 选择器 | "it is still cumbersome on mobile when many routes are configured" — 文本命令在移动端多路由场景下笨重。 | 移动端 Telegram 用户切换 provider/model 的可用性改进。 | P2，accepted。 |


## 8. 待处理积压

### 长期未决的高优先级 Issue（P1，无 fix PR）

| Issue | 标题 | 创建 | 最后更新 | 摘要 |
|---|---|---|---|---|
| [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | RFC: Pluggable inbound authentication and canonical principals | 2026-06-03 | 2026-08-14 | Rev 8。OIDC 与可插拔 provider。已到 IAM 里程碑但 72 天未落地。 |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) | RFC: Per-execution confirmation tier for high-risk shell commands | 2026-06-03 | 2026-08-14 | 维护者已确认范围，但无实现 PR。 |
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 74 test failures on Windows | 2026-06-10 | 2026-08-14 | 无 fix PR。跨平台 CI 欠债持续 65 天。 |

### 等待维护者审阅，且最近有更新

| Issue/PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) | RFC: ZeroClaw Chat Completions profile | `needs-maintainer-review` | 19 条评论，社区关注度高但缺乏裁决。 |
| [#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) | RFC: Runtime-owned conversation sessions | `needs-maintainer-review` | 14 条评论，与 #9488/#9600 有归属边界关联。 |
| [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488) | RFC: Unified attachment architecture | `needs-maintainer-review` | 14 条评论，与 #9487 配套。 |
| [#6971](https://github.com/zeroclaw-labs/zeroclaw/issues/6971) | RFC: Security posture, credential boundaries, universal ingress policy | `needs-maintainer-review` | 11 条评论，安全策略总纲。 |
| [#6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) | RFC: Provenance, conversation binding, reply contract for internal turns | `needs-maintainer-review` | 11 条评论，已完成 Rev 2 重写。 |
| [#9621](https://github.com/zeroclaw-labs/zeroclaw/issues/9621) | RFC: staged opt-in product telemetry | `needs-maintainer-review` | 3 条评论，帮助维护者做功能取舍决策。 |

### 等待作者响应的 PR（needs-author-action，可能阻塞合并）

| PR | 标题 | 说明 |
|---|---|---|
| [#9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) | fix(channels): authorize approval responders | P1 安全修复。 |
| [#9137](https://github.com/zeroclaw-labs/zeroclaw/pull/9137) | feat(plugins): add shared egress policy foundation | 依赖 #9580。 |
| [#9126](https://github.com/zeroclaw-labs/zeroclaw/pull/9126) | feat(plugins): validate typed instance config | XL 规模。 |
| [#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443) | feat(matrix): add single-message progress drafts | XL 规模，48 天未合。 |
| [#9707](https://github.com/zeroclaw-labs/zeroclaw/pull/9707) | fix(config): migrate bare vision_model_provider | L 规模。 |
| [#9713](https://github.com/zeroclaw-labs/zeroclaw/pull/9713) | feat(runtime): expose token accounting on history-trim events | XL 规模。 |
| [#9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420) | fix(anthropic): support stored OAuth profiles | XL 规模，20 天未合。 |
| [#9839](https://github.com/zeroclaw-labs/zeroclaw/pull/9839) | feat(security): block direct spellings of irreversible destructive commands | P1。 |
| [#9986](https://github.com/zeroclaw-labs/zeroclaw/pull/9986) | feat(agents): export an agent to a portable bundle | 新提交，XL 规模。 |
| [#9842](https://github.com/zeroclaw-labs/zeroclaw/pull/9842) | feat(cron/heartbeat): state the delivery contract to autonomous turns | P1。 |

### 阻塞的 Issue

- **[#9788](https://github.com/zeroclaw-labs/zeroclaw/issues/9788) Report the active shell dialect in the system prompt**（status: blocked，P3）— 被更高优先级工作阻塞，搁置中。

---

**项目健康度评估**：Issue 关闭率（3/33 ≈ 9%）偏低，PR 合并率（3/50 ≈ 6%）处于低水位，叠加 47 条待合并 PR 的积压，表明**维护者审阅带宽是当前瓶颈**。积极信号是：安全与兼容性修复（#9574、#9996）持续推进，且新提交的 PR（#9999、#10001、#10002）均针对具体细节问题，显示社区贡献质量稳定。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*