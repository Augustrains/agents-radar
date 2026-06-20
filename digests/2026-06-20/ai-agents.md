# OpenClaw 生态日报 2026-06-20

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-20 02:03 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，现根据您提供的OpenClaw项目数据，为您生成2026年6月20日的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026年6月20日

### 1. 今日速览

过去24小时内，OpenClaw项目社区活动极为活跃。尽管仅有1个新版本发布，但Issues和PR的更新量均达到了500条的高位，显示出社区在发现问题、提交修复方面的高参与度。当前，项目面临大量P0/P1级高优先级Bug，主要涉及内存泄漏、会话隔离失败、数据丢失等核心稳定性和可靠性问题，项目健康度面临严峻挑战。维护团队需要集中精力处理这批积压的严重问题，并加快PR的合并速度，以稳定社区信心。

### 2. 版本发布

- **v2026.6.9-beta.1**: 发布了最新的测试版本。
    - **主要内容**: 重点改进了Telegram消息的传递功能，包括支持更丰富的HTML格式、保留Markdown和Sticker路径、更准确地渲染进度草稿和命令输出，并修复了Mentions和消息队列在传递路径上的问题。
    - **破坏性变更/迁移注意事项**: 本次为Beta版本，建议用户谨慎升级。目前无明确破坏性变更披露。

### 3. 项目进展

过去24小时内，共有 **51个PR被合并或关闭**。以下是几个关键的进展：

- **修复关键Bug**:
    - `[Bug]: Messages on v2026.6.8 no longer supported on telegram web` (#93794): 该影响广泛的Telegram Web回归问题已被关闭，表明修复已合并。
    - `Slack thread session generates responses but fails to deliver to Slack` (#78061): 这个长期存在的Slack消息投递失败问题已被关闭，一个重要的沟通渠道障碍被清除。

- **功能与基础设施推进**:
    - `fix(cli): sync official plugins during update --all` (#94084): 修复了 `openclaw plugins update --all` 命令未正确同步官方插件及处理更新频道的问题。 [链接](https://github.com/openclaw/openclaw/pull/94084)
    - `fix(cli): coerce boolean retry.jitter to number` (#93978): 修复了配置中 `retry.jitter` 被设置为布尔值时导致Gateway启动崩溃的严重问题。 [链接](https://github.com/openclaw/openclaw/pull/93978)
    - `docs: add direct Kubernetes manifest apply path` (#93544): 更新了Kubernetes部署文档，增加了直接通过YAML配置文件部署的方式，简化了部署流程。 [链接](https://github.com/openclaw/openclaw/pull/93544)

### 4. 社区热点

今日社区讨论的焦点集中在 **系统稳定性和数据安全** 上，以下是讨论最热烈的问题：

1.  **核心会话/转录SQLite迁移跟踪** ([#88838](https://github.com/openclaw/openclaw/issues/88838), 31条评论): 开发者社区高度关注核心会话状态向SQLite的迁移进度。该问题作为一个“追踪”大本营，汇集了拆分迁移为小PR的讨论，表明社区对避免大规模高风险重构的审慎态度，并希望深度参与此架构变更。

2.  **严重：Gateway内存泄漏** ([#91588](https://github.com/openclaw/openclaw/issues/91588), 13条评论): 这是一个影响广泛的P0级问题。用户报告Gateway进程RSS占用在2-3天内从350MB飙升至15.5GB，最终导致OOM崩溃和反复重启。这引发了大量用户的共鸣和恐慌，很多人担心自己的服务会在无人值守时挂掉。

3.  **Telegram Web消息不兼容** ([#93794](https://github.com/openclaw/openclaw/issues/93794), 5条评论, 8个👍): 尽管该问题已关闭，但因其影响广泛（所有Telegram Web用户）且拥有多个点赞，反映了用户对核心通道功能稳定性的高要求。

### 5. Bug 与稳定性

过去24小时活跃的Bug主要集中在**会话状态损坏、消息丢失和进程崩溃**三大领域。按严重程度排列如下：

- **P0 (灾难性)**:
    - `Critical: Gateway Memory Leak` (#91588): Gateway内存泄漏导致OOM崩溃。**已有社区讨论，暂无明确修复PR。** [链接](https://github.com/openclaw/openclaw/issues/91588)
    - `memory-core Dreaming silently deletes daily memory files` (#84882): 核心记忆模块的相关操作会静默删除用户的日常记忆文件，导致数据丢失。**已有相关PR，等待审核。** [链接](https://github.com/openclaw/openclaw/issues/84882)
    - `Upgrading from 5.28 → 6.1: cron store migrated silently... causing channel errors` (#90378): 升级过程静默破坏了cron作业配置。**问题复杂，仍处于讨论阶段。** [链接](https://github.com/openclaw/openclaw/issues/90378)

- **P1 (严重)**:
    - `A single stalled agent session blocks the entire Gateway event loop` (#84903): 会话隔离失败，单个会话卡死会拖垮整个Gateway。 [链接](https://github.com/openclaw/openclaw/issues/84903)
    - `Matrix channel dispatch broken in v2026.6.1 - TypeError` (#90325): Matrix通道回归性崩溃。 [链接](https://github.com/openclaw/openclaw/issues/90325)
    - `Isolated cron consistently fails with "LLM request failed"` (#91363): 隔离cron任务无法执行。 [链接](https://github.com/openclaw/openclaw/issues/91363)
    - `Tool Search silently breaks the pre-compaction memory flush ... durable memories are lost` (#92273): 工具搜索功能导致记忆丢失。 [链接](https://github.com/openclaw/openclaw/issues/92273)

### 6. 功能请求与路线图信号

社区在稳定性之外，对功能扩展有着强烈诉求，部分请求已有关联PR，有望进入后续版本：

- **Per-agent memory-wiki vault configuration** ([#63829](https://github.com/openclaw/openclaw/issues/63829), 9个👍): 用户希望为多智能体系统中的每个智能体配置独立的记忆维基，而非共享全局库。这是一个在复杂工作流中呼声很高的需求。
- **Topic-session families** ([#90916](https://github.com/openclaw/openclaw/issues/90916)): 提出“话题-会话族”的概念，允许同一AI助手在不同话题下拥有独立的上下文记忆。这反映了用户对更精细化、更结构化的对话管理的追求。

- **可能被纳入下版本的信号**:
    - 解决记忆问题的 `fix(memory-wiki): prevent distinct titles from silently overwriting each other` (#93843) PR正在等待维护者审核。 [链接](https://github.com/openclaw/openclaw/pull/93843)
    - 提升模型兼容性的 `fix(llm): honor cacheRetention for LiteLLM-proxied Anthropic models` (#92665) PR也处于等待审核状态。 [链接](https://github.com/openclaw/openclaw/pull/92665)

### 7. 用户反馈摘要

- **痛点与不满**:
    - **“升级即灾难”**: 多位用户（如 #90378, #90325, #90213）抱怨从v5.28升级到v6.1时遇到了静默数据迁移、通道功能崩溃等回归问题，这不仅打乱了工作流，还造成了信任危机。
    - **“孤立无援”**: 用户对 `doctor --fix` 命令无法解决问题（#90213）感到沮丧，当自动化修复失败时，他们缺乏有效的后续手段。
    - **“警报疲劳”**: 用户反馈cron任务的热重载和重试机制会带来大量无效的“失败”通知（#90595），严重干扰了正常运维。
- **使用场景**:
    - **生产环境部署**: 大量用户（如 #85333, #91588）在云端生产环境中使用OpenClaw，对稳定性和性能退化极其敏感。
    - **多通道集成**: 用户活跃使用Telegram、Slack、Matrix、飞书等多个通道，任何单一通道的故障都会影响其Agent服务的可用性。
    - **复杂自动化工作流**: 通过cron和subagent编排复杂任务（如#92369）被频繁提及，表明OpenClaw正被用于构建超越简单聊天的自动化系统。

### 8. 待处理积压

以下为长期未得到有效响应或推进的重要Issue，对项目稳定性构成潜在威胁：

1.  **`memory-core Dreaming silently deletes daily memory files`** ([#84882](https://github.com/openclaw/openclaw/issues/84882), P0): 数天前报告的**数据丢失**问题。尽管有关联PR，但依然处于开放状态。这是首要解决的P0问题，项目必须尽快推进修复，以消除用户对数据安全的根本性担忧。

2.  **`A single stalled agent session blocks the entire Gateway event loop`** ([#84903](https://github.com/openclaw/openclaw/issues/84903), P1): 会话隔离失败的问题已存在一个月，影响整个Gateway的可用性。持续的悬而未决会破坏OpenClaw作为多智能体平台的信任基础。

3.  **`Timeout compaction can report success but leave Codex channel session unrecoverable`** ([#89374](https://github.com/openclaw/openclaw/issues/89374), P1): 核心的“压缩”功能可能失败，导致会话不可恢复。此问题与多个其他会话状态类问题（如#92043）高度相关，可能表明底层架构存在系统性缺陷，需要维护团队深入研究。

---

## 横向生态对比

好的，作为资深技术分析师，现根据您提供的各项目动态日报，为您呈上2026年6月20日的个人AI助手/自主智能体开源生态横向对比分析报告。

---

## 个人AI智能体开源生态横向分析报告 | 2026年6月20日

### 1. 生态全景

当前，个人AI助手与自主智能体开源生态正经历一场 **“由爆发式创新向生产级可靠性”的转型阵痛期**。一方面，以OpenClaw、Hermes Agent和ZeroClaw为代表的项目社区极度活跃，在功能迭代（如多通道集成、异步任务编排、高级权限模型）上竞争激烈；另一方面，大量涌现的P0/P1级Bug（如内存泄漏、数据丢失、会话隔离失败）表明，**稳定性与安全性已成为制约项目从“炫酷演示”走向“可靠生产”的关键瓶颈**。社区共识正从“能否做到”转向“能否稳定运行”，对模型回退机制、会话持久化、凭证安全管理的需求空前强烈。

### 2. 各项目活跃度对比

| 项目名称 | 新Issue | 新PR | 新Release | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | 1 (beta) | **危机并存**: 社区巨大，但P0/P1 Bug成堆，维护压力巨大。 |
| **Hermes Agent** | 50 | 50 | 1 (v0.17.0) | **高活跃，有隐忧**: 发布大版本，但关键Bug修复不彻底（如Gemma 4兼容性）。 |
| **ZeroClaw** | 50 | 50 | 0 | **非常活跃，进展稳健**: Bug修复速度快，大型功能PR推动中。 |
| **CoPaw** | 11 | 17 | 0 | **健康，社区响应快**: Bug报告后很快有对应PR，形成良好闭环。 |
| **NanoBot** | 10 | 33 | 0 | **活跃，维护高效**: PR合并率高，Bug修复及时。 |
| **PicoClaw** | 4 | 7 | 1 (nightly) | **良好，潜力待释放**: 有长期积压问题需解决，大型PR (Agent协作) 待评审。 |
| **NanoClaw** | 0 | 5 | 0 | **稳定推进**: 无新Issue，但PR代表重要进展（Apple Container）。 |
| **IronClaw** | 3 | 30 | 0 | **高密度协作**: 架构深化期，PR多但合并决策需加快。 |
| **LobsterAI** | 1 | 0 | 1 | **发布后平稳期**: 清理旧Issue，社区讨论新的宏大设想。 |
| **NullClaw** | 3 | 1 | 0 | **稳定维护期**: 解决特定平台兼容性问题。 |
| **TinyClaw** | 0 | 0 | 0 | **无活动** |
| **Moltis** | 0 | 0 | 0 | **无活动** |
| **ZeptoClaw** | 0 | 0 | 0 | **无活动** |

### 3. OpenClaw在生态中的定位

**OpenClaw是当前生态的“绝对核心参照”与“风暴之眼”。**
- **优势**: 拥有碾压级的社区规模（日更500条Issues/PRs），成为事实上的基础设施。其`memory-core`、`Gateway`等核心概念被多个项目借鉴。本次发布的`v2026.6.9-beta`对Telegram体验的改进，是其深耕核心通道能力的体现。
- **技术路线差异**: OpenClaw更强调多通道Hub（Telegram、Slack、Matrix等）和强大的插件生态系统。相较于Hermes Agent侧重桌面端原生体验，OpenClaw更像一个“Agent服务器”。
- **挑战**: **稳定性危机正在侵蚀其领导地位**。内存泄漏（#91588）、数据静默丢失（#84882）等P0问题若持续不解决，将驱动用户和贡献者流向稳定性更佳的项目，如ZeroClaw或CoPaw。

### 4. 共同关注的技术方向

1.  **模型回退与可靠性**:
    - **涉及项目**: NanoBot (#4287), ZeroClaw (#5844)
    - **具体诉求**: 当主模型返回空响应、超时或质量不佳时，系统需能智能、无缝地切换到备用模型，而非直接报错。
2.  **Agent身份认证与凭证安全**:
    - **涉及项目**: Hermes Agent (#4656), PicoClaw (#3114), NanoClaw (PR #2605)
    - **具体诉求**: 社区不满足于简单的API Key管理，开始探索“零知识凭证代理”、按工具/对话类型进行权限分级控制、以及从父级Agent继承权限等更复杂的信任模型。
3.  **会话状态持久化与数据安全**:
    - **涉及项目**: OpenClaw (#88838), Hermes Agent (#49307), ZeroClaw (#7907, #7941)
    - **具体诉求**: 从对SQLite迁移的审慎讨论，到对“静默删记忆”、“升级后状态损坏”的恐慌，社区核心诉求是数据不丢失、状态可恢复。
4.  **多模态与附件支持**:
    - **涉及项目**: PicoClaw (#348), LobsterAI (已发布)
    - **具体诉求**: 用户已不满足于纯文本交互，希望Agent能处理、生成并共享图片、文档（Word, PDF）、代码等多种文件类型。

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键词 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **多通道Hub + 插件生态** | 运营多平台Agent的开发者、团队 | Gateway, Session, Plugin, Memory-Wiki |
| **Hermes Agent** | **桌面端AI伙伴** | 个人高级用户、创意工作者 | Desktop App, Agent Skill, Context Compression |
| **ZeroClaw** | **安全、可观测的生产级Agent** | 企业、基础设施运维 | OIDC, SOP, Rust, 高可靠性 |
| **CoPaw** | **易用、快速迭代的AI工具箱** | 普通开发者和AI爱好者 | AgentScope, UI友好, 社区驱动修复 |
| **NanoBot** | **轻量、模块化的Bot框架** | 追求灵活定制的开发者 | Subagent, Cron, MCP, 模型回退 |
| **PicoClaw** | **嵌入式/轻量化Agent** | 对资源占用敏感的开发者 | 轻量, Windows/ARM兼容, WebSocket |
| **IronClaw** | **下一代（Reborn）架构探索** | 前沿技术探索者、核心贡献者 | Reborn, 并发调度, 外部工具标准化 |
| **LobsterAI** | **AI协作者与内容生成** | 内容创作者、协作团队 | Artifact共享, 语音输入, 项目级记忆 |

### 6. 社区热度与成熟度

- **第一梯队 (快速迭代，挑战与机遇并存)**: **OpenClaw**（社区体量巨大，但稳定性是阿喀琉斯之踵）, **Hermes Agent**（版本迭代快，宏观能力强，微观Bug多）。它们代表了 “功能领先” 的阵营。
- **第二梯队 (快速迭代，稳健推进)**: **ZeroClaw**（修复高效，新功能明确），**CoPaw**（社区反馈闭环好），**NanoBot**（维护效率高）。它们代表了 “质量优先” 的阵营，正通过快速响应抢夺用户。
- **第三梯队 (稳定维护或扩展期)**: **PicoClaw**, **NanoClaw**, **IronClaw**, **LobsterAI**，**NullClaw**。这些项目或有重大功能在等待评审，或在特定领域深耕，暂不处于风口浪尖。

### 7. 值得关注的趋势信号

1.  **“从工具到队友”的范式转变**: LobsterAI的 #2180 “AI协作者”提案和Hermes的“技能提取”功能（Ironclaw #5061 借鉴）共同指向：用户不再满足于仅执行指令的Agent，而是期望一个能 **管理复杂工作流、自主生成技能、拥有项目级上下文记忆的“AI队友”**。这对记忆架构、任务编排能力提出了全新要求。
2.  **移动端/Mac端体验成为差异化战场**: PicoClaw对Windows兼容性的修复、NanoClaw引入Apple Container、Hermes Agent的桌面端体验优化、CoPaw对移动端UI的改进，都表明**跨平台体验（特别是Android Termux、macOS、移动Web）正成为开发者选择项目的重要考量**。谁能提供更原生的体验，谁就能赢得更多“个人”用户。
3.  **安全信任的“零知识”化**: Hermes Agent的“凭证代理守护进程”提案（#4656）和PicoClaw的对话类型权限分级（#3114）表明，社区对Agent安全的焦虑正从“防外部攻击”转向 **“防Agent误操作/内部泄密”** 。未来，能否提供更精细、更隔离的权限模型，将成为评估Agent系统成熟度的关键指标。

---

**结论**: 2026年6月20日，AI智能体生态正处于一个关键的十字路口。**下半年的主旋律将是“稳定性与安全性”的军备竞赛**。能够率先解决内存泄漏、数据一致性和模型回退等核心难题的项目，将在新一轮竞争中脱颖而出。对于开发者而言，**优先选择“Bug修复快、架构清晰、对数据安全有明确承诺”的项目（如ZeroClaw, CoPaw）将比单纯追求功能的丰富度更有利于长期的生产力。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot 项目数据生成的 2026-06-20 项目动态日报。

---

# NanoBot 项目日报 - 2026年6月20日

## 1. 今日速览

本项目今日整体状态**非常活跃**。过去24小时内，社区贡献和项目维护工作十分密集，共有10个Issues和33个PR被更新。其中，PR的合并/关闭数量（19个）超过了待合并数量（14个），显示维护团队正在高效地处理社区提交的代码。尽管没有新的版本发布，但多个重要的Bug修复和功能增强PR已被合并，项目健康度良好。社区讨论聚焦于**模型回退机制**、**异步任务处理**以及**Telegram Bot新功能集成**等方向。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日项目取得了显著进展，共有 **19** 个 PR 被合并或关闭，推进了多个关键模块。主要进展包括：

- **Bug修复**：
    - **MCP连接稳定性**：修复了 `streamableHttp` MCP传输层超时问题，避免了因连接无响应导致的任务无限等待（[#4230](https://github.com/HKUDS/nanobot/pull/4230)）。
    - **会话管理**：修复了 `delete_session` 未能清理旧路径遗留文件，可能导致历史记录“复活”的Bug（[#4246](https://github.com/HKUDS/nanobot/pull/4246)）。
    - **飞书（Feishu）通道**：修复了通过 WebSocket 接收卡片消息时无法正确解析内容的Bug，确保复杂消息格式能正常显示（[#4342](https://github.com/HKUDS/nanobot/pull/4342)）。
    - **OpenAI图像编辑**：修复了在使用OpenAI模型进行图像编辑时，路由和文件上传逻辑错误的问题（[#4394](https://github.com/HKUDS/nanobot/pull/4394)）。
    - **图像剥离通信**：修复了当模型不支持图像输入而自动剥离图片时，发送错误的文本提示信息的问题（[#4345](https://github.com/HKUDS/nanobot/pull/4345)）。
    - **MCP进度通知**：修复了因未识别 `notifications/progress` 消息类型而导致Pydantic校验失败的Bug（[#4052](https://github.com/HKUDS/nanobot/pull/4052)）。
- **功能增强**：
    - **文件系统工具开关**：增加了 `tools.file.enable` 配置项，允许管理员按需启用或禁用内置的文件系统工具，提高了部署的灵活性（[#4138](https://github.com/HKUDS/nanobot/pull/4138)）。
    - **Discord通道重写**：合并了对Discord通道的重写工作（[#2655](https://github.com/HKUDS/nanobot/pull/2655)），预计将显著提升其稳定性和功能丰富度。

这些进展表明项目不仅在修复社区反馈的问题，也在持续优化核心功能和扩展通道支持。

## 4. 社区热点

今日讨论最活跃、关注度最高的话题主要集中在以下方面：

- **模型回退机制优化**: Issue [#4287](https://github.com/HKUDS/nanobot/issues/4287) “空响应不触发回退” 得到了广泛关注，社区用户 `glebov` 报告了当主模型返回空回复时，项目未能正确利用备用模型，导致服务中断。这暴露了现有回退逻辑的不足。关联的 Issue [#4389](https://github.com/HKUDS/nanobot/issues/4389) “为回退模型单独设置上下文窗口” 也反映了社区对更精细化、更可靠的模型切换策略的迫切需求。
- **异步任务与人类参与循环**：PR [#4411](https://github.com/HKUDS/nanobot/pull/4411) “[enhancement] feat(agent): add SuspendTurn...” 提出了一种让工具能够暂停当前回合以等待异步或人工介入的机制。这触及了复杂工作流和准自主 Agent 场景的核心痛点，显示社区开发者正在努力推动 Agent 从“即时响应”向更灵活的“异步协作”模式演进。
- **Telegram 新功能集成**：用户 `madIlama` 提出的 Issue [#4413](https://github.com/HKUDS/nanobot/issues/4413) “Telegram Bot API 10.1 rich messages” 紧跟平台更新，社区对该功能表现出兴趣，反应了用户对在 Telegram 上获得更佳消息排版和交互体验的期望。

## 5. Bug 与稳定性

今日报告的 Bug 大多已有对应的修复 PR，修复效率较高。按严重程度排列如下：

- **[严重] 模型空响应不触发回退** ([#4287](https://github.com/HKUDS/nanobot/issues/4287)): 主模型在高峰期返回空回复时，系统错误地将其归类为“不可回退”错误，导致服务不可用。这是一个严重的稳定性问题，暴露了fallback机制的缺陷。**目前处于待讨论状态，无明确修复PR。**
- **[中] 心跳任务结果发错频道** ([#4418](https://github.com/HKUDS/nanobot/issues/4418)): 用户 `orrinwitt` 报告，由定时任务（Heartbeat）触发的消息会被发送到最近活跃的聊天频道，而不是当初添加任务的频道。这会导致重要信息错位，影响用户体验。**已提为Feature Request，尚无修复PR。**
- **[中] 升级后旧版心跳逻辑异常** ([#4410](https://github.com/HKUDS/nanobot/issues/4410)): 用户升级后，即使心跳任务没有产生有意义的消息，系统也会默认发送一条空或例行通知。与PR [#4412](https://github.com/HKUDS/nanobot/pull/4412) 试图解决的“抑制例行通知”问题直接相关。**已有对应的修复PR ([#4412](https://github.com/HKUDS/nanobot/pull/4412))。**
- **[低] 升级后LLM调用超时** ([#4013](https://github.com/HKUDS/nanobot/issues/4013)): 用户从0.1.5升级到0.2.0后，遇到了“stream stalled for more than 90 seconds”的错误。该问题影响工作连续性，但起因复杂，可能与新版本配置或provider响应有关。**已被关闭。**

## 6. 功能请求与路线图信号

用户提出了多个有价值的功能请求，其中一些已有相应的PR实现，可能被优先纳入下一个版本。

- **模型推理力度自动调节** ([#4419](https://github.com/HKUDS/nanobot/issues/4419)): 用户 `orrinwitt` 希望支持根据不同任务自动调整模型的`reasoningEffort`参数，以在响应速度和质量之间取得平衡。这是一个很前沿的需求，反映了社区对模型调用精细控制的需求。
- **子Agent多模式结果汇总** ([#4414](https://github.com/HKUDS/nanobot/pull/4414)): PR [#4414](https://github.com/HKUDS/nanobot/pull/4414) 新增了 `aggregated` 结果模式，允许调度多个子Agent后，将结果汇总后再发送。这非常适合需要并行处理数据并最终合并的场景。
- **子Agent指定模型** ([#4415](https://github.com/HKUDS/nanobot/pull/4415)): PR 允许在 `spawn` 工具中指定子Agent使用的模型，为“混合专家”模式提供了基础。
- **Cron任务模型预设** ([#4416](https://github.com/HKUDS/nanobot/pull/4416)): PR 通过支持为Cron任务指定模型预设，使得后台任务可以使用与主对话不同的模型配置，增强了灵活性。

以上几个PR均来自维护者或核心贡献者，且围绕“Subagent”和“Cron”等核心功能，预计将在下个版本中发布。

## 7. 用户反馈摘要

- **满意的地方**：
    - 用户在 `#4013` 中特别提到旧版本 `0.1.5post2` 的WebUI“非常好用”，并表示感谢。
    - 对于已修复的Bug，用户在 `#4374` (项目工作空间读写不对称) 等Issue中表达了积极的反馈。

- **不满意/痛点**：
    - **升级后遗症**：从 `#4013` 和 `#4410` 可以看出，用户在升级版本时遇到了一些回归问题，体验断崖。
    - **回退机制不可靠**：`#4287` 和 `#4389` 共同指向了一个核心问题：当前的模型回退机制在应对空响应、上下文窗口不匹配等实际场景时表现不佳，是用户最大的痛点。
    - **配置复杂性**：`#4287` 提到用户将 `keepAlive: 300` 等一系列配置配置在“备用”模型上，这反映出当前配置模型回退的逻辑不够直观，对用户有较高的心智负担。

## 8. 待处理积压

以下为长期未响应或可能被忽略的重要议题，提醒维护者关注：

- **活跃待合并 PR**:
    - **XMPP通道** ([#1945](https://github.com/HKUDS/nanobot/pull/1945)): 一个全新的、提供XMPP支持的PR，自3月份提出后一直处于开放状态，已持续了3个多月。如果感兴趣，项目可能需要评估其内部质量、测试覆盖率和维护成本，以决定是否合并。
    - **Dream模式范围控制** ([#3591](https://github.com/HKUDS/nanobot/pull/3591)): 允许用户关闭或限制Dream功能的影响范围，以避免自动知识合并导致的技能漂移。这是一个对高级用户非常重要的控制选项，PR自5月2日提交后一直未合并。
    - **心跳手动触发** ([#3590](https://github.com/HKUDS/nanobot/pull/3590)): 允许用户手动触发心跳任务，用于调试或即时执行。同样自5月初起一直待处理。

确保这些PR得到及时的三元（Review/Comment/Close）判断，将有助于鼓励长期贡献者。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的Hermes Agent GitHub数据，以下是为您生成的2026年6月20日项目动态日报。

---

# Hermes Agent 项目日报 | 2026年6月20日

## 1. 今日速览

Hermes Agent 项目今日继续保持极高的社区活跃度。过去24小时内，项目收到50条Issue和50个PR，并发布了里程碑式的新版本 **v0.17.0**。社区讨论焦点集中在探索AI Agent身份认证安全机制、与新一代模型（如Gemma 4）的兼容性问题，以及桌面应用的用户体验细节上。值得关注的是，关于Gemma 4在Ollama后端下无法正常工作的Bug再次被用户提报，表明该问题在最新版本中仍未得到完全解决，项目稳定性方面存在一定隐患。

- **活跃度评估**: 极高 (🔥) - 每日Issue/PR数量均超50，社区贡献者众多。

## 2. 版本发布

- **版本**: **[v2026.6.19] Hermes Agent v0.17.0 (v2026.6.19)**
- **发布说明**:
    - `v0.17.0` 紧随 `v0.16.0` 发布，是一次重大的功能迭代版本，代号“The Reach Release”。
    - 项目经历了约1,475次提交、800+个PR合并和300+个Issue关闭。
    - 主要方向：在 `v0.16.0` 将Hermes推向桌面后，`v0.17.0` 似乎进一步拓展了其“触达”能力，但具体细节需查阅完整发布日志。
- **破坏性变更**: 未提供详细信息，鉴于如此大量的代码变更，建议用户在升级前仔细阅读完整发布说明。
- **迁移注意事项**: 由于变更量巨大，建议用户在非生产环境充分测试后，再进行大规模部署。务必关注配置文件和数据库模式的潜在变化。

## 3. 项目进展

尽管面临一些Bug挑战，但项目整体向前的步伐坚定不移。今日合并/关闭的重要PR主要聚焦于**平台适配**和**系统稳定性**的修复上：

- **Anthropic OAuth 修复**: PR [#49356](https://github.com/NousResearch/hermes-agent/pull/49356) 修复了Anthropic OAuth授权码交换过程中因请求端点错误（`platform.claude.com`）而失败的Bug，解决了影响用户认证流程的关键问题。
- **macOS Bootstrap 更新**: PR [#47070](https://github.com/NousResearch/hermes-agent/pull/47070) 修复了macOS版本重复构建和安装失败的“陈旧Bootstrap”问题，并通过安装印记和`app.asar`内容比对来避免重复操作，提升了macOS用户的更新体验。
- **Agent 行为修复**: PR [#45971](https://github.com/NousResearch/hermes-agent/pull/45971) 修复了Anthropic模型在部分流式传输失败后，返回不完整数据引发的`IndexError`，增强了Agent在处理API异常时的鲁棒性。
- **功能提案推进**: 一个新的大型功能 PR [#49037](https://github.com/NousResearch/hermes-agent/pull/49037) “first-class projects” 被提出，旨在建立以Project、Repo、Lane为核心的会话管理体系，并让后端成为会话树的权威来源，这将是桌面端体验的一次重要重构。

## 4. 社区热点

今日社区讨论的焦点集中在两个方向：

1.  **“零知识”凭证代理 (Credential Proxy Daemon)**:
    - **Issue**: [#4656](https://github.com/NousResearch/hermes-agent/issue/4656) (11条评论)
    - **核心诉求**: 尽管项目已实施PID命名空间隔离等安全措施，但用户仍然担忧凭证泄露风险。该Feature Request提出构建一个“零知识”的HTTP/HTTPS代理，让Agent子进程无需直接接触凭证，代表了社区对Agent安全边界的深入思考和更高期望。

2.  **Ollama + Gemma 4 兼容性问题**:
    - **Issue**: [#45924](https://github.com/NousResearch/hermes-agent/issue/45924) (5条评论) 和 [#49297](https://github.com/NousResearch/hermes-agent/issue/49297) (3条评论)
    - **核心诉求**: 用户报告在MacBook等设备上通过Ollama使用Gemma 4 12B模型时，Hermes Agent无法正常工作，报错`Response truncated`等。尽管相关Bug [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) 已被关闭且已有修复性PR [#41694](https://github.com/NousResearch/hermes-agent/pull/41694)，但用户投诉在最新版v0.17.0中问题依然存在。这表明修复方案可能未覆盖所有场景，或存在回归，引发了用户的强烈不满和重复提交。

## 5. Bug 与稳定性

今日报告的Bug数量众多，以下按严重程度排列：

- **P1 (关键)**:
    - **[Bug]: Context compression causes answer repetition + new instruction loss** ([#49307](https://github.com/NousResearch/hermes-agent/issues/49307)) - 上下文压缩机制导致模型重复回答并丢失用户新指令，这个问题直接影响了核心Agent体验，非常关键。
    - **[Bug]: 背景桌面应用启动后，停止自动跳转的界面** ([#49345](https://github.com/NousResearch/hermes-agent/issues/49345)) - 桌面版“启动网关”按钮无效，阻碍用户核心功能。
    - **[Fix]: Nous Portal access token resilience** (PR [#49351](https://github.com/NousResearch/hermes-agent/pull/49351)) - 修复了Nous Portal的token刷新和回退机制，影响所有使用该服务的用户认证。

- **P2 (重要)**:
    - **[Bug]: delegate_task model override ignored** ([#49332](https://github.com/NousResearch/hermes-agent/issues/49332)) - 子任务模型覆盖失效，导致用户无法为不同任务指定不同模型，并可能产生意外费用。
    - **[Bug]: hermes + gemma 4 12b** ([#45924](https://github.com/NousResearch/hermes-agent/issues/45924)) - 与P1级Bug [#49297](https://github.com/NousResearch/hermes-agent/issues/49297) 类似，该模型兼容性问题持续困扰用户。
    - **[Bug]: WhatsApp bridge dependencies fail after docker recreate** ([#36641](https://github.com/NousResearch/hermes-agent/issues/36641)) - Docker环境下WhatsApp集成在容器重建后依赖安装失败，影响Docker用户的连续性。
    - **[Bug]: Strict providers reject leaked timestamp** ([#47868](https://github.com/NousResearch/hermes-agent/issues/47868)) - Hermes向严格遵守OpenAI协议的服务商泄露了非标准字段。PR [#48523](https://github.com/NousResearch/hermes-agent/issues/48523) 指出了一个类似的更根本性问题。

## 6. 功能请求与路线图信号

- **即将被纳入的功能**: 讨论最多的 **凭证代理守护进程** ([#4656](https://github.com/NousResearch/hermes-agent/issues/4656)) 代表了社区对安全性的高优先级需求，很可能被纳入后续版本规划。
- **有望进入下一版本的功能**:
    - **支持 Zulip 平台**: Issue [#49229](https://github.com/NousResearch/hermes-agent/issues/49229) 和PR #3335表明Zulip集成已就绪，有望作为核心平台在下一个版本中上线。
    - **多语言i18n支持**: PR [#38846](https://github.com/NousResearch/hermes-agent/pull/38846) 提出支持15种语言，并且最新的PR [#49339](https://github.com/NousResearch/hermes-agent/pull/49339) 已完成了中文的全面翻译，显示该项目正在积极为全球社区做准备。
    - **持久化Webhook会话**: PR [#49353](https://github.com/NousResearch/hermes-agent/pull/49353) 支持Webhook的持久化会话，允许外部系统的重复事件路由到同一个Hermes会话中，增强了平台间的集成深度。

## 7. 用户反馈摘要

从今日的Issues中可以提炼出以下用户反馈：

- **痛点**:
    - **“回滚式”Bug**: 用户报告提及，即使一些修复性PR存在，实际问题（如 Gemma 4 兼容性）在最新版本中依然存在，让用户感到沮丧。([#49297](https://github.com/NousResearch/hermes-agent/issues/49297))
    - **桌面端体验不佳**: 令人“无法阅读”的滚动跳动 ([#47795](https://github.com/NousResearch/hermes-agent/issues/47795))、链接预览触发系统弹窗 ([#47500](https://github.com/NousResearch/hermes-agent/issues/47500))、中文输入干扰 ([#49326](https://github.com/NousResearch/hermes-agent/issues/49326)) 等，表明桌面端用户体验仍有不少粗糙之处。
    - **上下文压缩反作用**: 用户反馈上下文压缩后，AI不仅重复已回答内容，还丢失了用户新输入的指令，这直接损害了对话的连贯性和有效性。([#49307](https://github.com/NousResearch/hermes-agent/issues/49307))

- **使用场景**:
    - **本地优先**: 用户希望用本地模型（如Gemma 4）驱动Agent，追求隐私和低成本。([#45924](https://github.com/NousResearch/hermes-agent/issues/45924))
    - **安全敏感场景**: 用户对Agent的凭证管理提出极高要求，希望实现“零信任”架构。([#4656](https://github.com/NousResearch/hermes-agent/issues/4656))

## 8. 待处理积压

以下为长期未得到响应或解决的重要Issue，提醒维护者关注：

1.  **长期未响应的Bug**: Issue [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) “CLI --global model switch does not persist/clear model.base_url” 自5月中以来已有6周，仍为OPEN状态，该问题影响用户通过CLI配置自定义模型提供商的体验。
2.  **长期未响应的Feature**: Issue [#32159](https://github.com/NousResearch/hermes-agent/issues/32159) “Support ordered failover chains for web search/extract backends” 自5月底提出，是一个提升工具链可靠性的重要功能请求，但尚无官方回应。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-20

## 1. 今日速览

项目整体活跃度较高，过去24小时内产生了4个新 Issue 和7个 PR 更新，并发布了一个新的夜间构建版本。社区焦点集中在 **Windows 平台的路径兼容性 Bug**、**Telegram 渠道的细粒度权限控制**以及 **多模态/文件附件支持** 等方向。虽然 Issue 关闭数为0，但 PR 的持续提交和更新表明核心开发工作仍在积极推进。项目健康度良好，但部分长期遗留的 Bug 和功能请求（如 #2472, #348）仍需重点关注。

## 2. 版本发布

- **新版本**: `v0.3.0-nightly.20260620.287853ab`
- **类型**: Nightly Build（自动构建，可能不稳定）
- **更新说明**: 这是一个针对即将发布的 v0.3.0 版本的自动化夜间构建。该版本包含 `main` 分支上的最新代码，具体变更日志请查看：[Compare v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)。
- **破坏性变更**: 夜间构建版本未明确标注破坏性变更，使用时建议参考 `main` 分支的最新提交，并注意测试关键功能。

## 3. 项目进展

过去24小时内，有1个 PR 被合并，主要修复了一个配置中断的问题：

- **[已关闭] #2956: fix: preserve channel enabled state when merging security.yml** ([链接](https://github.com/sipeed/picoclaw/pull/2956))
  - **进展**: 修复了一个关键 Bug，即当用户通过 `security.yml` 添加凭证（如 Telegram token）时，会错误地将 `config.json` 中已配置为 `enabled: true` 的通道覆盖为禁用状态。此合并确保了安全配置合并后，通道的启用状态能够得到保留，提升了配置的一致性和用户体验。

## 4. 社区热点

- **[Bug] #2472: [BUG] list_dir returns "invalid argument" on Windows** ([链接](https://github.com/sipeed/picoclaw/issues/2472))
  - **活跃度**: ★★★★★ (评论 6, 👍 1)
  - **分析**: 该 Issue 持续活跃并拥有最多评论。它暴露了 PicoClaw 在 Windows 平台上的一个路径处理缺陷：`list_dir` 工具函数未能将 Windows 的反斜杠路径分隔符转换为 Go `os.Root` 要求的正斜杠，导致操作失败。这直接影响了 Windows 用户的核心文件操作体验，是平台兼容性的重要待修复点。

- **[增强请求] #348: [Feature] General Attachment Support** ([链接](https://github.com/sipeed/picoclaw/issues/348))
  - **活跃度**: ★★★★☆ (评论 4, 被标记为高优先级和路线图)
  - **分析**: 此 Issue 被标记为高优先级且属于项目路线图，反映了社区对多模态能力的强烈渴望。用户希望 PicoClaw 能处理通过 Telegram、Discord 等渠道发送的各类文件（文本、图片、音视频）。尽管该 Issue 创建较早，但其“路线图”标签表明它仍在项目规划中，是实现更智能交互的关键一步。

## 5. Bug 与稳定性

过去24小时内没有新增严重 Bug，但一些长期存在的 Bug 问题需要关注：

- **[严重] [Windows 兼容性] #2472: list_dir 路径分隔符错误** ([链接](https://github.com/sipeed/picoclaw/issues/2472))
  - **状态**: 未关闭，无关联 fix PR。严重阻碍 Windows 用户使用核心文件浏览功能。
  
- **[中等] #3150: [BUG]它给自己整失忆了** ([链接](https://github.com/sipeed/picoclaw/issues/3150))
  - **状态**: 新建 Issue，描述不清晰（缺少运行环境、复现步骤等），但暗示可能的内存或会话管理问题。需要作者补充详细信息。

- **[中等] #3074 (通过 PR #3143 修复): web_fetch SSRF 防护绕过** ([链接](https://github.com/sipeed/picoclaw/pull/3143))
  - **状态**: 有 fix PR ([#3143](https://github.com/sipeed/picoclaw/pull/3143)) 正在等待合并，该 PR 通过识别 ISATAP IPv6 字面量中内嵌的私有 IPv4 地址，修补了 `web_fetch` 功能中的 SSRF 防护漏洞。

## 6. 功能请求与路线图信号

- **[高优先级] #348: 通用附件支持** ([链接](https://github.com/sipeed/picoclaw/issues/348))
  - 该请求被标记为“路线图”，是项目明确的中期目标。社区对其有持续需求。
- **[高关注度] #3114: Telegram 对话类型权限分级控制** ([链接](https://github.com/sipeed/picoclaw/issues/3114))
  - 请求实现对私聊、群组、频道不同对话类型的权限分级控制，以防止在群组中误执行危险操作（如 `exec`）。此请求获得一个 👍，代表了社区对安全性的重视。目前尚无直接的 PR 关联，但可能被纳入后续的安全增强迭代中。

## 7. 用户反馈摘要

- **Windows 用户痛点**: 在 Issue #2472 的讨论中，用户对在 Windows 上使用 `list_dir` 失败感到困扰，这直接影响了日常开发脚本的执行。用户期盼能尽快修复合平台兼容性问题。
- **安全诉求**: Issue #3114 的提出者明确表达了在 Telegram 群组中安全管理 PicoClaw 能力的诉求，不希望因为配置不当导致机器人被滥用为“命令执行后门”。
- **配置困惑**: 已合并的 PR #2956 暗含了用户在过去配置 PicoClaw 安全凭证时的困惑：为什么添加了 token 后，机器人反而“失活”了。该修复解决了这个易用性问题。

## 8. 待处理积压

以下 Issue 和 PR 长期未更新或未得到维护者回应，建议重点关注：

- **[长时未合并 PR] #2937: Feat/agent collaboration** ([链接](https://github.com/sipeed/picoclaw/pull/2937))
  - **创建时间**: 2026-05-24 | **标签**: `stale`
  - **分析**: 这是一个重大功能 PR，旨在引入“代理协作总线”，实现多智能体间的通信。尽管更新于昨日，但已标记为 `stale`，可能需要项目核心维护者进行评估和代码审查，以决定是否将其合并到 `main` 分支。
- **[长时未关闭 Issue] #348: 通用附件支持** ([链接](https://github.com/sipeed/picoclaw/issues/348))
  - **创建时间**: 2026-02-17 | **标签**: `priority: high`, `type: roadmap`
  - **分析**: 作为路线图中的高优先级需求，此 Issue 自创建以来已过去4个月，建议项目组考虑排期，并在相关讨论中更新进展和计划，以安抚社区期待。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，这是根据您提供的NanoClaw GitHub数据生成的2026年6月20日项目动态日报。

---

## NanoClaw 项目动态日报 | 2026-06-20

### 1. 今日速览

NanoClaw 项目当前状态活跃，主要体现在 Pull Request (PR) 的提交与讨论上。过去24小时内虽然无新 Issue 或版本发布，但有 5 个 PR 处于开放状态，其中包含重要的功能修复与架构扩展，显示出开发团队正在积极推动多项改进。社区贡献者活跃，主要聚焦于提升核心功能的可靠性（如审批流程、Discord 集成）和引入新运行时支持（Apple Container）。项目整体健康度良好，维护者需关注大量积压的 PR，特别是早期提交的历史 PR。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无 PR 被合并或关闭，但以下开放 PR 代表了项目即将取得的重要进展：

- **修复审批流程数据持久化 (PR #2820)**：`caburi00` 提交的修复旨在解决审批记录中 `channel_type`、`platform_id` 等关键字段缺失的问题。此问题会导致审批列表功能异常，修复后将大幅提升企业内部审批流程的可用性和可追溯性。
- **实现Discord长消息分片 (PR #2812)**：`axnjxn415` 修复了 Discord 适配器在处理超过 2000 字符的长回复时直接截断的缺陷。通过引入 `splitForLimit` 分片器，现在会将长回复拆分为多条消息发送。这显著改善了用户体验，避免信息丢失。
- **引入 Apple Container 运行时 (PR #2809)**：`hidenwalker` 提交了一个重大的基础设施功能，支持在 macOS 环境下使用 Apple Container 作为运行时，并实现对远程 OneCLI 网关的一等支持。这标志着 NanoClaw 在跨平台、跨架构部署上迈出了关键一步，为 macOS 用户和需要远端 Agent 管理的场景提供了可能。

**项目向前迈进总结**：虽然修复尚未合入主分支，但核心功能 (审批、Discord) 的可靠性问题已找到明确解决方案，同时项目架构正在向更多样化的运行时环境扩展。

### 4. 社区热点

当前社区讨论热度最高的是 **PR #2605** (继承父级Agent权限)。尽管无最新评论，但该 PR 已存在近一个月并仍在持续更新，表明该功能（权限继承）是社区用户关注的重点。用户普遍期待 Agent 间的权限模型能够更灵活、更安全，而不是为每个子 Agent 重复配置。该 PR 通过 OneCLI 实现权限继承的尝试，正是对这一痛点的回应。

链接：[PR #2605: feat: inherit parent agent permissions via OneCLI](https://github.com/nanocoai/nanoclaw/pull/2605)

### 5. Bug 与稳定性

今日报告了一个新的功能性 Bug，并有一个旧的 Bug 已被修复（待合并）。按严重程度排列如下：

1.  **[严重] 审批流程数据丢失 (PR #2820)**：
    - **问题**：`requestApproval()` 进程在选定审批人之前创建了审批记录，且从未记录卡片最终的投递位置，导致 `channel_type`, `platform_id`, `platform_message_id` 等关键字段为 `NULL`。这直接影响 `approvals list` 功能的正确性，属于流程设计缺陷。
    - **状态**：已有修复 PR ([PR #2820](https://github.com/nanocoai/nanoclaw/pull/2820)) 待合并。

2.  **[中等] Discord 长消息被截断 (PR #2812)**：
    - **问题**：当 Discord 回复超过 2000 字符时，消息被强制截断，导致信息不完整。
    - **状态**：已有修复 PR ([PR #2812](https://github.com/nanocoai/nanoclaw/pull/2812))，通过分片发送解决问题。

### 6. 功能请求与路线图信号

- **Apple Container 运行时 (PR #2809)**：这是一个明确的路线图信号，表明项目正在探索或即将支持在 macOS 原生容器环境中运行 Agent。这意味着更紧密的 macOS 集成、更低的资源开销以及对未来可能出现的 Apple Silicon 优化的准备。此功能极有可能被纳入下一个正式版本。
- **安全与信任评分 (PR #2819)**：`mseep-ai` 的 PR 旨在分享一个安全更新并请求添加其平台徽章。虽然这是一个外部平台的推广行为，但也反映了社区对项目安全性透明度的需求。项目方在是否采纳此第三方信誉体系时需审慎评估。

### 7. 用户反馈摘要

从提交的 PR 描述和摘要（代表了开发者和用户的痛点）中，可以提炼出以下用户反馈：

- **审批流体验**：用户发现审批记录关键信息缺失，导致无法追踪审批项的最终去向。用户期望审批流程能完整、准确地记录所有操作上下文。
- **消息传输完整性**：在 Discord 等平台上，用户反馈长消息被截断，导致通知、报告或代码片段丢失。用户期望 Agent 能够智能地处理信息长度限制，保障消息的完整传达。
- **权限管理复杂性**：用户（Agent 开发者）希望简化权限管理，能从父级 Agent 继承已有权限，避免重复劳动和配置错误。

### 8. 待处理积压

- **PR #2605**：`feat: inherit parent agent permissions via OneCLI`
    - **状态**：已开放 27 天，最后一次更新是昨天（6月19日）。
    - **重要性**：高。权限继承是提升 Agent 生态系统可用性和可维护性的核心功能。长期未被评审或合并可能导致重大功能分支与主分支差异过大，增加未来合并冲突风险。
    - **行动建议**：维护者应优先安排该 PR 的 Code Review，确定其设计是否与现有架构兼容，并推动其进入合并流程。

链接：[PR #2605](https://github.com/nanocoai/nanoclaw/pull/2605)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NullClaw 项目数据，现呈上 2026-06-20 的项目动态日报。

---

# NullClaw 项目日报 | 2026-06-20

## 1. 今日速览

今日项目活跃度较低。过去24小时内，共更新3个Issue和1个PR，无新版本发布。关键进展是修复了一个关于本地Ollama模型回答不完整的Bug（#952），该问题已被关闭；同时一个针对Android/Termux平台HTTP库修复的PR（#966）已提交，等待合并。社区讨论主要围绕平台兼容性问题（Android Termux）和中国大陆用户的服务集成（飞书）展开。整体来看，项目处于稳定维护期，核心团队在持续解决用户反馈的平台适配与功能缺陷。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无PR被合并，但有一个重要的功能修复PR处于待合并状态，这代表了项目在平台兼容性上的一个关键推进。

- **PR #966 - 修复 Android/Termux 平台 HTTP 问题**：由社区贡献者 `vernonstinebaker` 提交的PR，旨在解决 Zig 0.16 标准库在 `aarch64-linux-android` (Termux) 环境下因缺少 `/etc/resolv.conf` 导致 DNS 解析失败（`NameServerFailure`）的问题。该PR将标准库 HTTP 请求通过 `curl` 进行路由，以绕过这一环境限制。若合并，将直接修复Issue #868 中提到的构建失败问题，并为后续Android端的稳定运行扫清障碍。

## 4. 社区热点

今日讨论最活跃的是 **Issue #484 - 飞书无法联网查询**。该问题自3月13日开启，至今已持续3个多月，获得了3条评论。虽然评论数不多，但其持续时间长，且涉及“飞书”这一特定于中国大陆市场的办公协作平台，反映了用户对本地化集成和网络环境适配的强烈需求。

- **链接**: [飞书无法联网查询 #484](nullclaw/nullclaw Issue #484)
- **诉求分析**: 该Issue背后可能反映了两个核心需求：
    1.  **网络环境兼容性**: 用户可能身处复杂的网络环境（如公司内网、需要代理），导致空壳应用的联网查询功能失效。
    2.  **平台集成深度**: 用户希望空壳能直接调用飞书API或读取飞书内容，而不仅仅是简单的网络请求。这是一个功能需求信号。

## 5. Bug 与稳定性

今日无新Bug被报告，但长期存在的Bug #868因对应的修复PR #966的出现而获得关注。按严重程度排列如下：

1.  **[中] Bug #868 - Zig构建在Android/Termux上失败** (已存在约2个月)
    -   **问题描述**：在 `aarch64` 架构的 Android Termux 环境下，使用 Zig 0.16.0 进行 `ReleaseSmall` 构建时失败，错误为 `AccessDenied on options.zig linkat`。
    -   **状态**：仍然开放，但已有对应的修复PR #966 提交。PR试图从根本上解决其更深层的HTTP库问题，但Issue本身描述的构建失败是否能被PR完全解决，尚需验证。评论中反馈“评论: 2”，显示关注度有限。
    -   **链接**: [Bug #868](nullclaw/nullclaw Issue #868)

2.  **[低] Bug #952 - 本地Ollama模型回答不完整** (已关闭)
    -   **问题描述**：使用Ollama加载本地模型时，Agent输出的答案不完整。
    -   **状态**：已于今日关闭。虽未提供具体修复细节，但问题已解决，表明项目团队对关键功能缺陷响应及时。
    -   **链接**: [Bug #952](nullclaw/nullclaw Issue #952)

## 6. 功能请求与路线图信号

- **平台兼容性（路线图强信号）**: **PR #966** 明确指出当前 Zig 标准库在特定平台（Android/Termux）的HTTP行为存在缺陷。这一PR及关联的 **Issue #868** 共同揭示了项目对扩展支持非标准Linux环境（特别是移动端）的强烈需求。这很可能被纳入下一个版本的路线图中，以提升项目的移动端可用性和覆盖面。
- **本地化集成（用户需求信号）**: **Issue #484** 中关于飞书的联网查询请求，是一个潜在的新功能需求信号。虽然当前讨论不活跃，但它体现了特定地区（中国大陆）用户希望空壳能与主流办公软件深度集成的诉求。未来版本可能会考虑增加对飞书、钉钉等平台的原生或代理支持。

## 7. 用户反馈摘要

从今日的Issue和PR评论中，可以提炼出以下用户痛点：

- **移动端开发体验不佳**：用户`NOTJuangamer10`在 **Issue #868** 中详细描述了在Android Termux上使用Zig构建失败的过程，显示出开发者用户在使用非主流环境（如手机上的终端）进行开发或部署时遇到的障碍。
- **本地模型体验待优化**：用户`bloodgroup-cplusplus`反馈的 **Issue #952** 表明，虽然空壳支持Ollama等本地模型，但在回答完整性和输出流畅度上仍有提升空间，这是追求隐私和本地化部署用户的关键痛点。
- **特定地区用户的服务可访问性**：用户`emmettlu`在 **Issue #484** 中遇到的“飞书无法联网查询”问题，反映了在中国大陆互联网环境下，网络访问的限制和代理的复杂性是用户使用空壳服务的常见障碍。

## 8. 待处理积压

以下为待维护者重点关注的长期未解决事项：

- **Issue #868 - Zig build fails on Android/Termux** (已存在58天)
    - **状态**: 开放，有PR #966 待合并。
    - **优先级**: 较高。该问题直接影响在移动端（尤其是通过Termux）构建和使用空壳的开发者。PR #966 是修复该问题的关键一步，建议维护者优先审阅并合并，以消除阻碍。
    - **地址**: [Bug #868](nullclaw/nullclaw Issue #868)

- **Issue #484 - 飞书无法联网查询** (已存在99天)
    - **状态**: 开放，长期未响应。
    - **优先级**: 中等。该问题虽非错误，但涉及特定地区的核心功能缺失。长期积压可能会影响该地区用户的信任度和留存率。建议维护者在下一版本规划中评估该需求的可行性。
    - **地址**: [飞书无法联网查询 #484](nullclaw/nullclaw Issue #484)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 IronClaw 项目数据，我为您生成了 2026-06-20 的项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-20

## 今日速览

IronClaw 项目今日保持高度活跃，核心团队与社区贡献者合力推进了多项关键进展。在 **Reborn** 架构的深化落地和基础设施优化上，项目迈出了坚实一步：Google OAuth 令牌自动续期、并发执行调度器以及多平台消息接入（Slack/Telegram）等核心 PR 已进入待合并阶段。同时，项目在质量保障和 CI 性能上也持续投入，如引入 Reborn 依赖闭包测试和 Mold 链接器优化。社区反馈聚焦于审批流程的优化，特别是大命令显示问题，而开发者则集中精力构建统一的特性标志和权限控制体系。

**活跃度评估：高**。过去 24 小时内有 3 个新 Issue 和 30 个 PR 更新，显示出极高的协作密度。

## 版本发布
无

## 项目进展

过去一天，项目在 **Reborn 架构** 的几个关键领域取得了实质性突破，多个重量级 PR 被合并或标记为待合并：

- **开发者体验与效率**：`#5019` (Projects 页面前端接入) 和 `#5064` (修复合并遗留问题) 的合并，标志着 Reborn 的 Projects 功能模块已完成前后端全线贯通。`#5097` 和 `#5096` 的合并加强了开发规范，将自动化工作流基准测试纳入了 QA 回溯系统，提升了代码质量和可靠性。
- **基础设施与性能**：`#5090` 的合并将 Mold 链接器扩展到更多 Rust CI 任务，预期可显著缩短构建时间。`#5092` 完成了 `sccache` 与现有缓存策略的 A/B 对比实验，为后续进一步提升 CI 效率提供了数据支持。
- **功能深化（待合并）**：多项重头功能已处于待合并状态，预计近期会合入主分支：
    - **认证与并发**：`#5087` 实现了 Google OAuth 令牌的预过期自动刷新，解决了用户需要频繁重连的问题。`#5085` 引入了 `TurnRunScheduler`，将 Reborn 执行器从串行升级为可配置并发的模型，为提升吞吐量奠定基础。
    - **外部集成**：`#5093` (Slack) 和 `#5100` (Telegram) 的 PR 通过基于扩展状态的消息入口重构，意味着 Reborn 的第三方平台集成正走向标准化和模块化。
    - **AI 能力**：`#5061` 引入了 Hermes 风格的技能提取与自我进化机制，允许 Reborn 从成功的交互中学习并生成可重用的技能，这是一个重要的 AI 自主性信号。

## 社区热点

社区讨论的核心集中在 **审批流程（Approval Modal）** 的可用性上，这是影响用户体验的直接痛点。

- **Issue #5078 [CLOSED]：大命令审批模态框难以操作**。该 Issue 由社区用户 `sunglow666` 报告，指出当执行大型 shell 命令时，命令内容会占据整个审批弹窗，导致用户难以看到执行动作的上下文和审批按钮。该问题已关闭，但未显示关联 PR，说明可能已通过其他方式（如 UI 调整）快速修复。此 Issue 反映了 **“安全性与易用性”** 之间的平衡是 AI Agent 工具的关键挑战。
    - 链接: [nearai/ironclaw Issue #5078](https://github.com/nearai/ironclaw/issues/5078)

## Bug 与稳定性

- **严重**：`#4108` **Nightly E2E 持续失败**。这是一个持续了近一个月的长期未解决的关键问题。自动化的 nightly E2E 测试持续失败，威胁到项目主干代码的稳定性。尽管近期有大量 QA 相关的 PR 被合并，但此问题的未解决状态仍是项目稳定性的一个重大风险信号。
    - 链接: [nearai/ironclaw Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

- **轻度**：`#5088` **Shell 审批提示语义错误**。社区用户 `think-in-universe` 报告了一个 UI/UX 问题：Shell 审批弹窗有时会将某些操作（如 `read`）错误地显示为 `reads`，这可能对用户造成误导。该问题是更广泛审批优化父 Issue `#4879` 的一部分，表明项目正在系统地梳理审批环节的细节。
    - 链接: [nearai/ironclaw Issue #5088](https://github.com/nearai/ironclaw/issues/5088)

## 功能请求与路线图信号

Issues 和 PR 清晰地勾勒出 Reborn 架构下一阶段的演进方向：

- **统一特性标志系统 (Feature Flag System)**：Issue `#5091` 提出了为 Reborn 建立一个统一的特性标志系统，以实现动态切换、按用户/租户进行目标群体控制和灰度发布。这标志着项目已开始考虑成熟的企业级应用需求和更精细化的功能管理能力。该 Issue 来自核心成员 `ilblackdragon`，很可能被纳入近期开发计划。
    - 链接: [nearai/ironclaw Issue #5091](https://github.com/nearai/ironclaw/issues/5091)

- **精细化权限控制**：`#5062` (待合并) **按工具权限覆盖模型**。此 PR 引入了允许用户对单个工具进行“始终允许”、“每次询问”或“禁用”的权限设置。这与 `#5078` 的社区痛点一脉相承，是改进审批体验、赋予用户更多控制权的关键举措。

- **外部工具集成标准化**：`#5094`、`#5099` 等 PR 正在构建一个符合 OpenAI API 标准的 **外部工具响应流程**，包括模型列表、模型验证和工具调用回路。这表明 Reborn 正在努力成为一个更开放、兼容性更强的 AI Agent 平台。

## 用户反馈摘要

近期的 Issues 和 PR 评论揭示了用户在使用 IronClaw 时的具体场景和潜在痛点：

- **对透明度的认可与挑战**：用户 `sunglow666` 在 `#5078` 中反馈，审批弹窗能显示实际执行的命令是“有帮助的”(helpful)，但“内容过长”又带来了新的审查困难。这说明用户**既希望知道 Agent 在做什么，也希望审查界面是友好且易用的**。
- **对界面语义准确性的期望**：`#5088` 中用户明确指出 `reads` 提示是“误导性的”(misleading)，这说明用户对 Agent 行为和 UI 提示的语义一致性有较高要求，不希望被不准确的信息干扰判断。

## 待处理积压

| 编号 | 类型 | 标题 (摘要) | 创建时间 | 更新时间 | 重要性 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **#4108** | Issue | **Nightly E2E failed** | 2026-05-27 | 2026-06-19 | **严重** | 长期未解决的关键稳定性问题，威胁主干代码。 |
| **#4002** | PR | **build(deps): bump the actions group across 1 directory with 16 updates** | 2026-05-24 | 2026-06-19 | 中等 | 依赖更新 PR 已存在近一个月仍未合并，可能存在兼容性问题待解决，或需要手动干预。 |
| **#4829** | PR | **ci: retire dormant reborn-integration workflow, add Reborn suites to nightly deep CI** | 2026-06-12 | 2026-06-19 | 中等 | CI 重构 PR 已开启一周，对提升测试覆盖率和清理冗余有重要意义，需推进审查与合并。 |

**分析师评论**：`#4108` 和 `#4002` 这类长期未决的 Issue/PR 是项目健康度的潜在隐患。尤其是 **Nightly E2E 失败**，应作为最高优先级问题进行定位和修复，以避免在大量新功能合入后引入难以追溯的回归问题。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是为您生成的 LobsterAI 项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-20

## 1. 今日速览

今日 LobsterAI 项目表现平稳，活跃度中等。主要亮点为发布了 **2026.6.18** 版本，重点升级了 Artifact 共享能力，支持了更广泛的文件类型。社区方面，新增了 1 个具有前瞻性的功能请求 Issue，讨论热度开始酝酿。过去 24 小时内关闭了 3 个早期（4月）报告的、标记为“stale”的 Bug Issue，表明项目正在清理积压的历史问题。但过去 24 小时无任何 PR 合并，项目推进节奏在版本发布后有所放缓。

## 2. 版本发布

- **新版本：LobsterAI 2026.6.18**
  - **发布时间：** 2026-06-18
  - **核心更新内容：**
    - **Artifact 共享能力升级：** 这是本版本的最大亮点。从此，在 LobsterAI 中生成的 Artifact（产物）不再局限于特定格式，现已支持共享 **Word、PPT、Excel、PDF、Markdown 以及 Mermaid** 等多种文件类型。这极大提升了 AI 产出的可用性和协作效率，使项目从单一的代码/文本生成，向通用的内容协作平台迈进了一步。
    - **语音输入修复：** 修复了语音输入相关问题，仅保留实时语音识别（ASR）功能。
  - **破坏性变更与迁移注意事项：** 无。
  - **链接：** [LobsterAI 2026.6.18 Release](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.18)

## 3. 项目进展

过去24小时内，项目没有合并或关闭任何 Pull Request。主要进展体现在昨日（6月19日）对一批旧 Issue 的批量关闭处理上。这表明项目团队在发布新版本后，正在进行一轮日常的维护和清理工作，重点关注那些可能已经过时或在新版本中已被修复的问题。

## 4. 社区热点

今日社区最受关注的 Issue 是昨日新开的 #2180，尽管目前评论数为 0，但其内容具有很高的讨论价值。

- **Issue #2180 [OPEN]：构建“AI 协作者”表单**
  - **作者：** woxinsj
  - **核心内容：** 提出了一份名为 `openclaw-ai-collaborator-proposal.md` 的详细提案，建议将项目（OpenClaw）从一个低层级工具集升级为面向“懂技术的非精英程序员”的 **AI 协作者平台**。核心功能包括：
    1.  引入**自然语言命令栏**，降低操作门槛。
    2.  构建**任务调度控制台**，实现跨模型编排。
    3.  引入**项目级记忆**，实现长时间、跨会话的上下文保持。
  - **背景分析：** 该提案超越了传统的 Agent 或 Copilot 范畴，旨在建立一个能管理复杂工作流、拥有长期记忆的 AI 队友。这反映了社区用户对“智能体”深度集成和自主性的更高期待，可能预示着未来功能规划的新方向。
  - **链接：** [Issue #2180](https://github.com/netease-youdao/LobsterAI/issues/2180)

## 5. Bug 与稳定性

今日无新增 Bug 报告。但值得关注的是，昨日（6月19日）批量关闭了 3 个来自 4 月初的老 Issue，它们均标记为“stale”（过期）。这些 Bug 属于中等严重程度的用户体验问题，可能已在近期的版本迭代中被修复。

- **[CLOSED] #1471：切换会话/视图时输入框草稿丢失**
  - **问题描述：** 用户在 Cowork 输入框输入文字后，若在 300ms 的去抖（debounce）时间内切换会话或视图，未发送的草稿内容会因组件卸载而丢失。
  - **严重程度：** ⭐⭐ 中等（影响用户输入体验和数据安全）。
- **[CLOSED] #1472：重新编辑历史消息时覆盖当前输入框内容无确认提示**
  - **问题描述：** 用户在输入框中已有未发送内容时，点击历史消息的“重新编辑”，会直接覆盖现有内容且无任何确认提示，导致用户输入丢失。
  - **严重程度：** ⭐⭐ 中等（属于典型的 UI/UX 交互缺陷，可能导致数据丢失）。
- **[CLOSED] #1487：会话中调用 Python 脚本出现问题**
  - **问题描述：** 用户在本地使用 30B 模型时，在 LobsterAI 会话中调用 Python 脚本的功能异常，而同样的配置在其他 CLI 或环境中可以正常工作。
  - **严重程度：** ⭐⭐⭐ 较高（影响核心代码执行功能的可用性）。

## 6. 功能请求与路线图信号

- **#2180 “AI 协作者”平台提案：** 这是今日最重要的功能信号。它提出了一个宏大的愿景，将项目从一个工具集提升为一个具备项目级记忆、跨模型编排能力的 AI 队友。如果此功能被采纳，将是项目路线的重大转折点，预计会成为下一阶段（如 Q3/Q4）的核心战略方向。
- **Artifact 共享能力升级（已发布）：** 最新版本中已实现的支持共享 Word、PPT、Excel 等多类型文件的功能，直接回应了用户在跨格式内容协作上的强烈需求，预计将提升工作流集成度。

## 7. 用户反馈摘要

- **积极反馈：** 无直接评论，但 **#2180** 提案的提交本身就是一个积极的信号，表明有深度用户愿意为项目提出宏大的改进蓝图，希望看到项目的长期发展。
- **问题/痛点：**
  - **Bug #1471 & #1472：** 暴露出用户在**输入体验**方面的痛点。草稿丢失和内容被无提示覆盖是开发效率的杀手，用户期望组件在处理未保存状态时能更智能或提供更多确认。
  - **Bug #1487：** 用户抱怨“同样的技能在 Claude Code CLI 和其他地方都正常”，这揭示了项目在**跨环境兼容性**和**本地模型支持**方面存在潜在问题，可能导致用户对平台的可靠性产生怀疑。

## 8. 待处理积压

当前无此类问题。过去24小时内对积压的旧 Issue 进行了清理，这是一个积极信号。当前唯一的 Open Issue (#2180) 是昨日新建的功能需求，尚在讨论初期，不属于积压问题。建议维护者关注该 Issue 的讨论走向，并及时给予回应。

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

好的，作为CoPaw开源项目的AI分析师，我将根据您提供的GitHub数据，生成一份结构清晰、数据驱动的项目动态日报。

---

# CoPaw 项目日报 (2026-06-20)

**项目名称:** CoPaw (AgentScope AI)
**数据时间范围:** 2026-06-19 ~ 2026-06-20 (约24小时)
**报告生成时间:** 2026-06-20

---

### 1. 今日速览

项目今日社区活跃度**极高**，共产生11条Issue和17条PR，显示出社区参与热情高涨。核心动态集中在三方面：一是多位社区贡献者（尤其是`lecheng2018`和`nguyenthanhthe`）针对近期报告的严重Bug提交了修复PR，项目响应速度较快；二是UI/UX相关功能请求（如侧边栏切换、模型排序）与已有PR形成了良好的闭环，社区需求与开发进度匹配度高；三是关于核心组件（ChromaDB、Console API）的稳定性修复取得进展，两个影响较大的Bug（索引膨胀、UI卡死）均已有关联修复PR。整体来看，项目正处于快速迭代和Bug修复并行推进的健康状态。

### 2. 版本发布

无

---

### 3. 项目进展

过去24小时内，项目团队合并或关闭了6个PR，修复了关键问题，并推动了两项重要功能进入待合并状态。项目整体在稳定性和功能性上迈出了坚实一步。

**已合并/关闭的里程碑PR:**

- **修复ChromaDB索引无限膨胀问题 (`#5332`)**: 针对长期困扰用户的`#4795`问题，`lecheng2018`提交的修复PR已被合并。该PR引入了索引压缩、清除及超时保护机制，从根源上解决了向量数据库无限制增长导致的崩溃问题。这是提升项目长期运行稳定性的关键一步。
    - **链接**: [#5332](https://github.com/agentscope-ai/QwenPaw/pull/5332)
- **修复Cron任务因繁忙被跳过问题 (`#5241`)**: 同样是`lecheng2018`贡献，将APScheduler的`misfire_grace_seconds`默认值从60秒提升至3600秒。这对于常运行长时间Agent任务的用户是重要的体验优化。
    - **链接**: [#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241)
- **修复多Agent协作技能触发失败 (`#5179`)**: 针对团队协作英文/中文关键词不足的问题进行了修复，提升了Agent遵循用户指令的可靠性。
    - **链接**: [#5179](https://github.com/agentscope-ai/QwenPaw/pull/5179)
- **修复Agent回复超时导致界面冻结 (`#5242`)**: 为`agent.reply()`增加了超时保护，避免了因LLM API卡顿导致整个进程挂起。
    - **链接**: [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242)

**新增的待合并功能PR:**

- **在折叠侧边栏中切换Agent (`#5334`)**: 直接响应了Issue `#5329`的需求，是移动端体验的重要改进。
    - **链接**: [#5334](https://github.com/agentscope-ai/QwenPaw/pull/5334)
- **支持模型列表自定义排序 (`#5336`)**: 响应了Issue `#5267`，允许用户在设置中调整模型顺序，提升了高频用户的使用效率。
    - **链接**: [#5336](https://github.com/agentscope-ai/QwenPaw/pull/5336)

---

### 4. 社区热点

今日社区讨论热度主要集中在Bug报告和UI改进请求上。

- **Bug讨论焦点：Agent卡死与UI状态异常**
    - **`#5328`**: 用户`bob-geek11`报告Agent在DeepSeek模型上“思考”时卡死，需要手动干预，且已创建相关UI状态错误的Issue `#5333`。这引出了对**流式响应与UI状态同步**的质疑，评论显示其他用户也对此问题深有共鸣。社区的关注点从单独的Bug转向了底层SSE事件同步机制。
        - **链接**: [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328), [#5333](https://github.com/agentscope-ai/QwenPaw/issues/5333)
    - **修复PR**: `nguyenthanhthe` 已提交PR `#5335` 专门修复`#5333`中所述的后端异常未向UI推送失败事件的问题。
        - **链接**: [#5335](https://github.com/agentscope-ai/QwenPaw/pull/5335)
- **功能请求热点：移动端体验优化**
    - **Issue `#5329`**: 用户`bob-geek11`在移动端浏览器使用Backend，核心痛点是在紧凑的UI下无法切换Agent，这直接反映了**移动端适配的迫切需求**。该Issue获得了积极的社区反馈和迅速响应的PR `#5334`，形成了良好的社区-开发闭环。
        - **链接**: [#5329](https://github.com/agentscope-ai/QwenPaw/issues/5329)
    - **PR `#5334`**: `lecheng2018`高效响应，使折叠侧边栏图标可点击并提供弹窗切换Agent。
        - **链接**: [#5334](https://github.com/agentscope-ai/QwenPaw/pull/5334)

---

### 5. Bug 与稳定性

今日报告的Bug主要集中在近期版本升级后的回归问题和特定模型兼容性上，其中大部分已有对应的修复PR。

| 严重程度 | Issue 标题 | 问题描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **高** | `#5320`: Agent卡死，文本框状态异常 | Agent提交指令后卡死，但UI显示为可提交状态，而非“停止”模式。 | 已有PR `#5335` 修复 |
| **高** | `#5328`: Agent在DeepSeek模型中思考时卡死 | 使用DeepSeek时，Agent在thinking状态卡死，需要手动停止后继续。 | 待排查 (可能与流式处理或特定模型接口有关) |
| **中** | `#5320`: `send_file_to_user`发送图片不显示 | v1.1.12升级后，通过该命令发送图片，聊天窗口不显示图片（显示为空白），但飞书等渠道正常。 | 已有PR `#5324` 修复 |
| **中** | `#5330`: Zhipu供应商模型测试连接失败 | 供应商级别API测试成功，但旗下所有模型的测试连接均失败。 | 已有PR `#5339` 修复 (核心是消息格式兼容问题) |
| **低** | `#5319`: Console频道始终显示“已回答已停止” | 用户重装重启后解决，可能是偶发的UI状态同步问题。 | 已关闭（用户自解决） |

---

### 6. 功能请求与路线图信号

除了已出现对应PR的UI改进请求外，今日社区还提出了以下值得关注的功能请求：

- **智能体办公室交互性增强 (`#5327`)**: 用户希望在智能体办公室页面直接与各个Agent进行对话，而无需切换视图。这表明社区对**多Agent管理与实时监控**有着更高层次的交互需求。该请求可能涉及较大的UI与后端改动，是路线图中一个值得评估的信号。
    - **链接**: [#5327](https://github.com/agentscope-ai/QwenPaw/issues/5327)
- **实时UI更新与语音通知 (`#5322`)**: 用户`xyxy`提出当通过API向Console发送消息时，UI应实时更新而非手动刷新。此功能对于构建自动化工作流和多Agent协作**用户体验**至关重要。作者已提交关联PR `#5331`，该PR极有可能被纳入下一个版本。
    - **链接**: [#5322](https://github.com/agentscope-ai/QwenPaw/issues/5322), [#5331](https://github.com/agentscope-ai/QwenPaw/pull/5331)
- **新贡献者模式 (`#5340`)**: 一位新贡献者`rankaiyx`提交了PR，提议将模型工厂中的格式丢弃检测从“黑名单”改为“白名单”模式。这虽然是一个修复，但也暗示了开发者对**代码健壮性和可预测性**的追求。
    - **链接**: [#5340](https://github.com/agentscope-ai/QwenPaw/pull/5340)

---

### 7. 用户反馈摘要

从今日的Issues和评论中，可以提炼出以下核心用户声音：

- **“移动端是硬伤”**: 用户`bob-geek11`的多个Issue（#5329, #5328, #5333）都从侧面反映了移动端使用体验的巨大差距。无论是Web还是Tauri，UI适应性、交互流程度都是当前最大的痛点。
- **“升级有风险，回滚需谨慎”**: 用户`zjccjz869` 反馈升级到v1.1.12后，之前正常的图片发送功能失效。这反映了用户对**版本升级的稳定性**高度敏感，也暴露出热修复可能存在回归风险。
- **“底层机制需要更透明”**: 多个关于Agent“卡死”的讨论（#5328, #5333）表明，用户对Agent内部状态（特别是Thinking阶段）的感知是缺失的。当系统未响应时，用户希望看到明确的进度或错误提示，而非静默等待或手动干预。
- **“社区贡献者高效给力”**: 以`lecheng2018`和`nguyenthanhthe`为代表的社区贡献者，能够在一天内针对多个并发问题同时提交修复和功能PR，体现了CoPaw社区强大的活力和技术深度。

---

### 8. 待处理积压

以下为历史遗留但今日未有更新、仍需维护者重点关注的问题：

- **Issue `#4795`: 向量索引膨胀 (已修复)**
    - **状态**: 核心Bug已于今日由PR `#5332`修复并合并，但鉴于其严重性（37G磁盘占用），建议维护者在下一个版本发布说明中明确提及此修复，并引导受影响的用户进行数据清理。同时，关注merge后续是否有新的衍生问题。
    - **链接**: [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795), [#5332](https://github.com/agentscope-ai/QwenPaw/pull/5332)
- **PR `#5321`: Scroll Context Manager (`niceIrene`)**
    - **状态**: 一个前期提交的重要功能PR，引入了替代原生压缩的“滚动”上下文管理策略，并修复了Agent配置解析Bug。目前由Code Owner (Under Review) 审查中，未有新评论。建议维护者安排时间推进代码审查或给予作者反馈。
    - **链接**: [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)
- **Issue `#5317`: Tauri下 `python` 命令缺失**
    - **状态**: 用户`HQ1363`报告Tauri客户端找不到内置的Python环境，导致自定义Skill无法运行。该问题已持续2天，对依赖Python脚本的用户影响较大，但暂无后续更新或指派。建议维护者优先排查路径绑定或虚拟环境隔离问题。
    - **链接**: [#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是根据您提供的 ZeroClaw 项目数据生成的 2026-06-20 项目动态日报。

***

# ZeroClaw 项目动态日报 | 2026-06-20

## 1. 今日速览

今日 ZeroClaw 项目活跃度极高，24小时内产生了50条Issue和50条PR，社区贡献与核心开发并行推进。尽管暂无新版本发布，但项目在多个关键领域有重大进展：**v0.8.0 预编译二进制缺失频道功能的回归 bug 引发社区高度关注**，同时围绕身份认证（OIDC）、WebSocket 生命周期管理、用户引导界面（onboard）和 Discord 交互组件等核心功能，均有大型 PR 提出或合并。Bug 修复方面，针对运行时状态持久化、成本配置热加载、流式输出重复等问题有快速响应，显示出项目维护团队对稳定性和用户反馈的高度重视。整体评估为 **“非常活跃，进展稳健”**。

## 2. 版本发布

无

## 3. 项目进展

今日合并/关闭的重要 PR 主要体现了对核心基础设施和用户体验的改进：

- **Discord 交互组件 (PR #7965 - 已合并)**: 完成了 Discord 频道的按钮、选择菜单、弹窗、工具审批流和自动补全等交互组件支持，极大提升了 Discord 渠道的功能完整性和用户体验。
- **运行时架构优化**: **PR #8033** 将废弃的 `zeroclaw onboard` 重做为基于聊天的交互式设置助手，降低了新用户上手门槛。**PR #8037** 开始为 OpenAI Responses API 提供者添加关键测试，提升了代码质量。
- **会话持久化基础设施**: **PR #8001** 引入了 `SopRunStore` 特质和内存后端，为标准操作程序（SOP）的持久化、并发控制和可观测性奠定了基础。
- **成本与配置修复**: **PR #8004** 修复了成本预算配置只能在启动时冻结，无法热加载的问题。**PR #8005** 修复了容器基础镜像引用被废弃导致构建失败的问题。

## 4. 社区热点

- **#7787 [Bug] v0.8.0 预编译二进制缺失 Slack/Discord 频道功能**: **热度最高 (6条评论)**
  这是一个严重的回归问题，因为官方发布的 v0.8.0 二进制文件未包含 Slack 和 Discord 频道支持，而 v0.7.5 是正常的。社区用户发现即使配置正确，也无法使用 Slack。**这直接影响了升级用户的正常使用，是当前最受关注的 P1 级问题**。目前尚无直接的修复 PR 链接。([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7787))

- **#5844 [Bug] 系统提示过于强调记忆 (memory)**: **6条评论**
  用户反馈系统提示过度关注历史记忆，而忽略当前输入的 prompt，特别是在 cron 任务场景下，导致输出与用户意图不符。这是一个长期存在且影响广泛的功能问题，需要调整提示词优化策略。([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5844))

- **#7141 [Feature]: OIDC 认证提供者支持**: **5条评论**
  作为 v0.9.0 目标的一部分，该 RFC 提议引入可插拔的认证提供者架构，支持 OIDC。这显示了社区对生产级安全性的强烈需求。([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7141))

- **#7965 [PR] Discord 交互组件 (已合并)**: 该 PR 的合并是今日最大的里程碑之一，大幅增强了 Discord 频道的交互能力。([链接](https://github.com/zeroclaw-labs/zeroclaw/pull/7965))

## 5. Bug 与稳定性

今日报告了多个严重 Bug，主要集中在数据一致性和运行时行为上。目前均有对应的修复 PR 提出。

| 严重程度 | Issue # | 描述 | 状态 | 修复 PR |
| :--- | :--- | :--- | :--- | :--- |
| **P1 - 阻塞** | #7907 | 重命名 Agent 时，**在配置持久化前就移动了外部状态**，可能导致数据丢失或不一致。 | 已修复 | #7941 (作为镜像问题修复) |
| **P1 - 阻塞** | #7941 | 删除 Agent 时，存在与#7907 **相同的持久化前状态清理缺陷**。 | 已修复 | #7941 |
| **P1 - 阻塞** | #6037 | **Cron 任务可被重复触发**：如果任务运行时间超过调度轮询间隔，会导致多个实例同时运行。 | 待处理 | 无 |
| **P1 - 阻塞** | #8014 | **流式输出内容重复**：在本地工具调用前，叙述性文本会出现重复。 | 有修复 PR | [#8014](https://github.com/zeroclaw-labs/zeroclaw/pull/8014) |
| P2 | #8004 | **成本预算配置在启动时被冻结**，无法通过修改配置实时生效。 | 已修复 | [#8004](https://github.com/zeroclaw-labs/zeroclaw/pull/8004) |
| P2 | #8009 | **HMAC 工具收据 (receipt) 未在所有 Agent 执行路径中生效**，包括 ACP、WebSocket 和 CLI。 | 有修复 PR | [#8009](https://github.com/zeroclaw-labs/zeroclaw/pull/8009) |
| P2 | #4721 | ZeroClaw 将日志输出到 **stdout 而非 stderr**，干扰了标准输出内容的重定向和管道操作。 | 待处理 | 无 |

## 6. 功能请求与路线图信号

- **OIDC 认证提供者 (#7141)**: 已明确标记为 **v0.9.0** 目标，是未来安全性升级的核心。
- **统一斜杠命令注册表 (#7929)**: 提议将 Web UI、`zerocode` TUI 和频道运行时三套独立的手写命令注册表统一为一个服务端目录，是重要的人机交互体验改进。
- **对话式 onboard 界面 (#8034 & PR #8033)**: 该功能已通过 **PR #8033** 实现并合并，将纳入下个版本。对新手极其友好。
- **存储受限部署的临时文件清理 (#7996)**: 针对低配置设备（如树莓派）提出的特性，表明社区关注边缘/嵌入式部署场景。
- **Docker 镜像包含文档 (#7950)**: 用户希望 Agent 本身能获取 ZeroClaw 文档，以便回答用户关于配置和功能的问题，这将是提升帮助体验的有趣思路。

## 7. 用户反馈摘要

- **痛点**: **v0.8.0 预编译二进制缺失频道功能 (#7787)** 是最响亮的用户痛点，直接阻碍了用户升级。用户不得不回退到 v0.7.5。
- **体验问题**: **系统过于强调记忆 (#5844)** 导致在 cron 任务中输出不相关的内容，这是用户对 Agent 行为可控性提出的明确诉求。
- **配置痛点**: **日志输出到 stdout (#4721)** 是一个持续的用户体验问题，影响了 CLI 工具的正常使用。有用户尝试通过 `2>/dev/null` 规避，但这并非长久之计。
- **构建痛点**: **Termux 用户无法在 Android 上安装 (#7911)**，暴露出对非标准 Linux (aarch64) 平台的支持缺失。

## 8. 待处理积压

以下 Issue 和 PR 存在时间较长或缺乏响应，提醒维护者关注：

- **#5869 [P1 - Blocked] security: rumqttc 依赖导致 RUSTSEC 安全风险**: 自 4月18日开启以来，由于 `rumqttc` 依赖版本过旧，项目存在多个已知安全漏洞。状态为 `blocked`，依赖上游库更新，需持续关注。([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5869))
- **#6693 [XL - High Risk] feat(memory): 添加“梦境模式”**: 该 PR 提出了周期性内存整合的宏大特性，已开启一个多月，但状态为 `needs-author-action`，需要作者更新或回复。其子 PR #7797 也在等待其合并。([链接](https://github.com/zeroclaw-labs/zeroclaw/pull/6693))
- **#6893 [XL - High Risk] feat(infra): 多数据库会话后端**: 支持 Postgres, Oracle 等，是大型企业级特性，已提出近一个月，需要更多评审和讨论。([链接](https://github.com/zeroclaw-labs/zeroclaw/pull/6893))
- **#4721 [P2] zeroclaw 日志输出到 stdout**: 长期存在的用户体验问题，虽然影响不大，但修复难度低且能显著提升 CLI 体验。([链接](https://github.com/zeroclaw-labs/zeroclaw/issues/4721))

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*