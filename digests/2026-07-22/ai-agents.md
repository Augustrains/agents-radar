# OpenClaw 生态日报 2026-07-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-22 01:18 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是依据您提供的OpenClaw项目数据生成的2026年7月22日项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-07-22

### 1. 今日速览
今日OpenClaw项目社区活跃度极高，问题（Issues）与合并请求（PRs）更新量均达到500条，呈现爆发式增长。大量P1级别的Bug与高价值的功能请求正在被激烈讨论，显示出项目正处于快速迭代与关键问题攻坚阶段。开发重心集中在安全加固（如密钥遮蔽、文件系统沙箱）、稳定性修复（如数据库损坏、消息丢失）以及扩展性提升（如子代理权限管理、新平台适配）。新版本发布沉寂，但背后是维护团队对现有问题的集中攻关。

### 2. 版本发布
无新版本发布。

### 3. 项目进展
今日有**163条PR**被合并或关闭，表明项目开发管线运转高效，许多积压的修补和功能正被快速整合。以下是几条关键进展：

- **核心安全修复**：PR `#105884` `fix(vydra): apply request policy to media generation requests` 修复了Vydra媒体生成请求可能绕过用户代理和私有网络策略的问题，这是一项具有高安全风险的修补，对保护用户数据安全至关重要。
- **稳定性增强**：PR `#89039` `fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError` 解决了在SDK重试期间，由于会话写锁释放导致的静默消息丢失问题。此修复直接关系到用户在长对话中的消息可靠性。
- **平台兼容性**：PR `#112353` `fix(macos): direct Gateway TLS pins protect operator traffic` 为macOS上的Gateway直接连接提供了TLS证书锁定支持，增强了控制面板和WebChat等运营商流量的安全性。
- **新工具/适配**：`#102228` 和 `#102296` 等多个大型PR正在推进 **ClawHub** 包管理功能的落地，包括安装、状态查看和移除。这表明OpenClaw正努力构建一个标准化的技能/插件分发生态系统。

### 4. 社区热点
今日讨论焦点高度集中在**安全性、数据持久化和模型兼容性**三大主题上。

1.  **#10659: 密钥遮蔽系统** (15条评论，4👍)
    - **链接**: [Issue #10659](https://github.com/openclaw/openclaw/issues/10659)
    - **诉求**: 强烈要求引入“遮蔽密钥”机制，让AI代理能使用API密钥但无法读取其原始值，以防止提示注入攻击导致凭证泄露。
    - **分析**: 这是社区对安全的最高优先级诉求。大量高优Issue（如#85030, #88562）都涉及凭证和权限问题，反映出用户对于“代理”行为不可控的普遍担忧。

2.  **#101290: 数据库损坏Bug** (13条评论，1👍)
    - **链接**: [Issue #101290](https://github.com/openclaw/openclaw/issues/101290)
    - **诉求**: 报告了在macOS上`openclaw.sqlite`数据库在网关运行时反复损坏的回归Bug，指向特定版本（2026.6.6）的健康检查命令。
    - **分析**: 这是一个严重级别为P0的数据丢失问题。虽然评论数不是最高，但影响面广且讨论深入，用户提供了详细的复现步骤，社区正积极寻求根本原因。

3.  **#85030: MCP工具注入失败Bug** (11条评论，5👍)
    - **链接**: [Issue #85030](https://github.com/openclaw/openclaw/issues/85030)
    - **诉求**: 用户报告在通过`sessions_spawn`生成子代理时，`bundle-mcp`配置的工具集（MCP tools）无法被注入，导致子代理只能使用内置工具。
    - **分析**: 这是对OpenClaw核心扩展能力的一次关键考验。子代理想完全继承父代理的扩展工具集是用户构建复杂自动化流程的基础，该问题阻碍了多代理协作场景。

### 5. Bug 与稳定性
今日报告的Bug主要集中在以下高风险领域，多为回归问题，严重程度极高：

- **`[P0]` 数据库崩溃** (#101290): `CLI startup preflight can corrupt the live state DB`。macOS下的数据损坏问题，暂无对应修复PR。
- **`[P1]` 静默消息丢失** (#53408): `Write/exec tool parameters silently dropped after long conversations`。长对话后工具参数静默丢失，严重影响任务执行。**(已有修复PR #89039)。**
- **`[P1]` 认证失败** (#95612): `cli-backend agent runs against anthropic return 401`。Claude CLI代理身份验证失败，影响开发者体验。
- **`[P1]` CVE/回归** (#108473): `cron tool schema breaks llama.cpp tool-calling`。cron工具定义中的正则表达式破坏了llama.cpp的工具调用，属于回归问题。
- **`[P1]` 子代理输出泄露** (#90840): `Subagent run completion is delivered to chat user as raw worker output`。子代理的原始输出错误地发送给了用户，可能导致内部信息泄露。

### 6. 功能请求与路线图信号
- **安全堡垒**：大量P1/P2增强请求围绕**文件系统沙箱** (#7722)、**技能权限清单** (#12219)和**基于能力的权限模型** (#12678)展开。社区对“零信任”代理架构的需求极高。
- **开发者体验**：**插件热重载** (#14438) 和**会话快照** (#13700) 是开发者高频痛点。这些功能若被采纳，将极大提升开发调试效率。
- **平台拓展**：**Telegram Business Bot** (#20786)和**Antigravity CLI** (#84527) 是向新平台扩展的信号。其中#84527已有5.4的PR讨论，说明维护者已开始行动。
- **审计与成本**：**按模型计费日志** (#13219) 功能请求虽评论不多，但反映了企业级应用的关键需求。

### 7. 用户反馈摘要
- **核心痛点**：“我的子代理不听使唤，拿不到MCP工具，还会泄露内部输出。”—— 用户在使用`sessions_spawn`构建多代理工作流时，感到控制力不足和信息安全风险高。
- **使用场景**：“我想知道谁在飞书群里发了消息，但不想因此给代理看遍整个公司通讯录。”—— 用户（#13751）清晰表达了精细化权限控制的场景需求，要求最小权限原则。
- **满意点**：“`/new` 和 `/reset` 之后看不到新会话用了什么模型和思维模式，有点懵。”—— 用户（PR #89277）提出了一个用户体验改善点，表明用户对基础功能稳定后，开始追求更丰富的信息反馈。
- **不满情绪**：“更新一年多，每次都要手动备份，心里没底。”—— 多个用户反复提出备份恢复和更安全的自动更新机制（#13616， #14526），反映出对数据持久化和灾难恢复的持续担忧。

### 8. 待处理积压
- **长期未决的高价值特性**：
    - **#7722** `Feature Request: Filesystem Sandboxing Config (tools.fileAccess)` (创建于2026-02-03)：这是最经典的安全增强请求之一，至今无明确跟进，但标签显示`needs-product-decision`。
    - **#13751** `Feishu plugin: remove dependency on contact:contact.base:readonly` (创建于2026-02-11)：该请求关注点非常具体，影响Feishu用户的隐私，至今仍处于`needs-product-decision`状态。
- **挂起的核心修复PR**:
    - **#112441** `chore(i18n): refresh native locales` (创建于2026-07-21)：一个看似平凡但影响所有非英语用户的跨平台本地化同步PR，目前无维护者审查。
    - **#89039** `fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError`：修复了一个高影响的消息丢失Bug，且已被主维护者贴上“ready for maintainer look”标签，应优先处理。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，基于您提供的 2026-07-22 各项目动态摘要，我为您呈现以下横向对比分析报告。

---

### **AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-07-22)**

#### **1. 生态全景**

今日，AI 智能体开源生态呈现出 **高度活跃、分化加速、安全与稳定性成为发展矛盾焦点** 的态势。头部项目（如 OpenClaw、Hermes Agent、ZeroClaw）正处于密集的功能迭代与核心架构重构期，社区贡献与 Bug 报告呈现爆发式增长。虽然新版本发布暂时放缓，但“零信任”安全架构、多代理协作、模型上下文协议（MCP）的实用化等方向已成为全行业共同攻坚的核心。与此同时，部分外围项目（如 Moltis）活跃度下降，而特定领域的项目（如 CoPaw、NanoBot）则在快速修复由新版本引入的 Bug，体现出生态正从“功能优先”的早期探索阶段，正式迈入“质量与安全并重”的深水区。

#### **2. 各项目活跃度对比**

| 项目名称 | Issues 更新数 | PRs 更新数 | 今日发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~500 | ~500 | 无 | **极高**：爆发式增长，处于关键问题攻坚与安全加固阶段。 |
| **NanoBot** | 9 (关闭) | 33 (22合并) | 无 | **高**：密集的Bug修复与安全加固，响应速度快。 |
| **Hermes Agent** | 50 | 50 | 无 | **极高**：功能扩展与大规模Bug修复并行，社区讨论热烈。 |
| **PicoClaw** | 4 (关闭) | 3 (合并) | 无 | **中等偏高**：积极修复与功能增强，社区反馈得到快速闭环。 |
| **NanoClaw** | 1 (新) | 12 (活跃) | 无 | **中等**：技术债务清理中，社区贡献活跃但增速平稳。 |
| **NullClaw** | 0 | 0 | 无 | **静默**：无任何活动。 |
| **IronClaw** | 41 | 50 | v1.0.0-rc.1 | **极高**：重构冲刺期，里程碑版本发布，核心架构剧变。 |
| **LobsterAI** | 1 (活跃) | 10 (5合并) | 无 | **高**：功能打磨与稳定性提升，社区反馈响应迅速。 |
| **TinyClaw** | 0 | 0 | 无 | **静默**：无任何活动。 |
| **Moltis** | 0 | 1 (Dependabot) | 无 | **低**：仅依赖维护，社区活跃度极低，处于平稳维护期。 |
| **CoPaw** | 41 | 50 | v2.0.1-beta.1 | **极高**：新版本发布后Bug集中爆发与修复，社区高度聚焦。 |
| **ZeptoClaw** | 0 | 0 | 无 | **静默**：无任何活动。 |
| **ZeroClaw** | 50 | 50 | 无 | **极高**：安全漏洞（S0）、工作流阻塞（S1）Bug与高价值RFC并存。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 作为生态中**最核心的参照项目**，其定位和社区规模具有显著优势：
- **社区规模与活跃度**：OpenClaw 的日更 Issue 和 PR 数量（各约500条）在所有项目中遥遥领先，显示出其拥有最庞大、最活跃的开发者与用户社区。这使其成为生态中最重要的“意见领袖”和功能风向标。
- **技术路线**：其开发重心明确偏向 **企业级安全与稳定性**，如密钥遮蔽、文件系统沙箱、子代理权限管理。相比之下，Hermes Agent 更侧重于 Agent 的 **长期会话稳定性和行为分析**，而 ZeroClaw 则聚焦于 **SOP（标准操作程序）驱动的安全代理架构**。
- **生态位**：OpenClaw 扮演着 **“基础设施提供者”** 的角色。它不仅是个人助手，其 `ClawHub` 包管理功能正在将自己打造成一个技能/插件分发生态系统，类似于 AI 智能体世界的“应用商店”，其演进方向对其他项目有重大影响。

#### **4. 共同关注的技术方向**

以下技术需求在多个项目中涌现，是生态发展的普遍痛点：

| 共同技术方向 | 具体诉求 | 涉及项目 |
| :--- | :--- | :--- |
| **零信任安全架构** | 密钥遮蔽、文件系统沙箱、精细化工具/技能权限控制、子代理隔离。 | OpenClaw (#10659, #7722)、NatanoBot (#4987, #5013)、Hermes Agent (#25083)、ZeroClaw (#8279, #9247)、CoPaw (#6079) |
| **多代理协作控制** | 子代理工具继承、输出隔离、`sessions_spawn` 的可靠性、MCP 工具的跨代理复用。 | OpenClaw (#85030)、Hermes Agent (#67187)、ZeroClaw (#8279) |
| **模型兼容性与上下文管理** | 推理模型内容暴露、工具调用格式泄漏、Agent 无限循环、跨会话上下文污染。 | NanoBot (#4934)、Hermes Agent (#68979)、CoPaw (#6299, #6241)、PicoClaw (#3153) |
| **用户体验与易用性** | 可配置的记忆系统、UI 性能（卡顿、漂移）、会话管理（快照/恢复）、文档与实际配置不符。 | OpenClaw (#89277, #13700)、Hermes Agent (#68920, #68964)、NanoClaw (#2236, #1530)、ZeroClaw (#8505, #8718) |
| **可观测性与调试** | 模型调用日志、Token 用量追踪、成本审计、行为分析。 | OpenClaw (#13219)、Hermes Agent (#60417, #46366)、NatanoBot (隐性需求) |

#### **5. 差异化定位分析**

| 项目名称 | 功能侧重 | 目标用户 | 技术架构差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **全能型生产力平台** | 追求稳定、安全与可扩展的企业开发者和高级个人用户。 | 最庞大、最成熟的架构，生态杠杆效应强。强调整合能力（ClawHub）和平台安全。 |
| **NanoBot** | **轻量级 Agent 快速启动与调试** | 关注快速实验、原型开发和模型测试的开发者。 | 架构相对轻量，核心逻辑在 Nanobot 网关层。修复速度极快，注重工具调用协议的健壮性。 |
| **Hermes Agent** | **深度 Agent 行为分析与自省** | 希望了解 Agent 内部机制、构建高可靠性任务的应用开发者。 | 强调“可恢复性”和“行为分析”，如在 Desktop 端推出行为洞察卡。TUI 和 Desktop 是其特色。 |
| **PicoClaw** | **多 IM 渠道的 Bot 适配器** | 主要在中国市场（微信、钉钉、飞书）部署 Bot 的用户。 | 专注于消除特定平台（如飞书）的兼容性壁垒，解决 IM 平台特有的 Bug。 |
| **NanoClaw** | **亚洲市场渠道集成先驱** | 希望快速接入 LINE 等亚洲特有渠道的社区用户。 | 高度依赖社区贡献（Skill）来填补官方生态位，目前处于早期功能拓展阶段。 |
| **ZeroClaw** | **SOP 驱动的安全代理与多租户场景** | 对 Agent 权限、工作流合规、SOP 有严格要求的企业/运维人员。 | 引入了独特的“SOP（标准操作程序）” 和 “Target Mode（目标模式）” 概念，架构与安全策略强耦合。 |
| **IronClaw** | **新一代 Agent 运行时重构 (Reborn)** | 愿意接受颠覆性变更、追求最新架构的前沿用户和项目集成方。 | 核心团队正推动从零开始的 `v1.0.0-rc.1` 重构，架构向 `CompositeRootFilesystem` 和密封进程授权演进。 |

#### **6. 社区热度与成熟度**

- **快速迭代与新增功能阶段（极高活跃度）**：**OpenClaw, Hermes Agent, ZeroClaw, IronClaw, CoPaw**。这些项目正处于功能快速叠加和大规模 Bug 修复期，PR 和 Issue 数量巨大，适合愿意参与前沿开发、追随最新功能或需要解决特定 Bug 的开发者。
- **质量巩固与稳定性提升阶段（高活跃度）**：**NanoBot, LobsterAI, PicoClaw**。这些项目在版本发布后，正积极清理 Bug 和安全问题，提升体验，修复速度和对社区反馈的响应速度是核心指标。适合寻求稳定版用户。
- **技术债务清理与维护阶段（中等活跃度）**：**NanoClaw**。项目增长放缓，核心工作在于审查和合并社区长期遗留的 PR，解决部署和配置问题。对于新用户入场，需注意其配置复杂性和文档一致性。
- **项目停滞或休眠阶段（无活动）**：**Moltis, NullClaw, ZeptoClaw, TinyClaw**。这些项目长期无活跃开发，社区贡献为零。除非有重大重启，否则不建议新用户或开发者投入精力。

#### **7. 值得关注的趋势信号**

基于今日的社区动态，以下趋势值得行业关注：

1.  **“零信任代理”成为刚需**：用户已经不再满足于“智能”，而是要求 Agent **“安全可控”**。密钥隔离、最小权限原则（如原子粒度的工具过滤）、动作前确认（如 sudo 权限）被反复提及，反映出 AI Agent 从“玩具”向“生产工具”转型过程中，安全是最大的绊脚石。

2.  **MCP 协议进入实用与健壮性考验期**：多个项目（Hermes, ZeroClaw, OpenClaw）都报告了与 MCP 工具连接、参数传递和进程管理相关的 Bug。这表明 MCP 作为标准协议已被广泛集成，但其在复杂网络环境、长时间运行下的健壮性、子进程资源回收等问题，已成为制约其大规模应用的关键瓶颈。

3.  **社区驱动的渠道生态正在形成**：从 NanoClaw 的 LINE 支持，到 PicoClaw 的中国 IM 平台深耕，再到 ZeroClaw 对新平台的探索，都表明单一项目无法覆盖所有平台。项目正在通过“技能市场”、RFS 流程等方式，将渠道集成的工作下放给社区，预示着 AI 智能体渠道将走向“长尾化”的生态模式。

4.  **Agent 行为可观测性需求从“专业”走向“通用”**：对 Token 用量、成本、推理过程、决策链路的追踪请求，不再仅由高级开发者提出。随着 Agent 被应用于更多关键场景，普通用户也希望能“看到 Agent 在想什么”，这推动了像 Hermes Agent 的行为洞察卡和 ZeroClaw 的评估框架等功能的诞生。

5.  **架构重构成为应对复杂性的必然选择**：无论是 IronClaw 的“Reborn”全盘重构，还是 OpenClaw 的 `ClawHub` 包管理，或是 ZeroClaw 的 SOP 架构，都表明为了应对日益增长的 Agent 复杂性和安全需求，底层架构的重构或升级已经不再罕见，而成为头部项目保持竞争力的必要手段。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的NanoBot项目数据，现生成2026年7月22日的项目动态日报。

---

# NanoBot 项目动态日报 | 2026-07-22

## 1. 今日速览

过去24小时，NanoBot 项目社区活跃度极高，代码合并与Bug修复节奏明显加快。共有 **33个PR** 被处理（其中22个已合并/关闭），并关闭了 **9个Issue**，显示出维护团队对社区反馈的高响应速度。值得关注的是，**安全性（API密钥明文存储、文件系统操作）** 和 **稳定性（session无限增长、工具调用循环）** 成为本次更新的两大核心主题。整体而言，项目正处于一个密集的修复与加固周期，为下一个功能发布版本奠定了坚实基础。

## 2. 版本发布

**无新版本发布。**

项目在过去24小时内没有发布新的Release版本。当前的开发活动主要集中在 `main` 分支的缺陷修复和功能预研上。

## 3. 项目进展

在核心功能与架构层面，项目取得了显著进展，尤其是在工具调用协议和数据持久化方面。

- **工具结果隔离与修复**：PR [#4663](https://github.com/HKUDS/nanobot/pull/4663) 被合并，该PR是修复Issue [#4058](https://github.com/HKUDS/nanobot/issues/4058) 的解决方案。它实施了严格的工具结果隔离机制，自动丢弃缺失、重复或未知的`tool_call_id`，防止了协议层面的数据污染和潜在死循环，提升了网关层的健壮性。
- **安全加固**：
    - 文档层面，PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) 更新了 `SECURITY.md`，正式推荐使用环境变量引用方式存储API密钥，以取代存在风险的明文存储。
    - 配置写入层面，PR [#4984](https://github.com/HKUDS/nanobot/pull/4984) 通过 **原子写入（temp+replace）** 方式保存 `config.json`，防止写入过程中崩溃导致配置文件损坏。
    - 文件系统访问层面，PR [#4987](https://github.com/HKUDS/nanobot/pull/4987) 引入了基于已打开文件句柄的工作区校验，以抵抗TOCTOU（Time-of-check Time-of-use）攻击，显著增强了`read_file`、`write_file`等工具的安全性。
- **新Provider支持**：PR [#4965](https://github.com/HKUDS/nanobot/pull/4965) 已被合并，正式将 **ModelScope** 作为内置模型提供商。用户现在可以直接通过其OpenAI兼容接口调用Qwen、DeepSeek等开源模型。
- **会话管理修复**：PR [#4941](https://github.com/HKUDS/nanobot/pull/4941) 解决了会话元数据读取的回归问题，确保新旧路径下的session文件都能被正确加载，避免了WebUI重启后工作区信息丢失的问题。

## 4. 社区热点

今日最具讨论热度的议题聚焦于**代理工具的循环**和**推理模型的兼容性**，反映了用户对Agent可靠性和模型生态覆盖的迫切需求。

- **Issue [#4864](https://github.com/HKUDS/nanobot/issues/4864) [Open]:** “`<tool_call> <function=complete_goal>` 导致无限循环”。该Issue获得了1个赞和4条评论。用户报告了一个严重的回归Bug：`complete_goal`工具因网关层错误地将参数解析为纯字符串（而非JSON）而反复报错，导致Agent陷入死循环。这暴露了近期更新中工具参数序列化逻辑的兼容性问题，是影响Agent任务完成度的高优问题。
- **Issue [#4934](https://github.com/HKUDS/nanobot/issues/4934) [Open]:** “Qwen模型暴露了思考/推理内容”。用户反馈使用Qwen系列模型（如`qwen3.6-flash`）时，模型的内部推理过程被错误地输出为聊天响应的一部分，影响了用户体验。对此，社区迅速响应，PR [#5023](https://github.com/HKUDS/nanobot/pull/5023) 已提交以修复此问题，通过在`_MODEL_THINKING_STYLES`中为Qwen模型添加`enable_thinking`配置，实现了对推理内容的可控输出。

## 5. Bug 与稳定性

今日报告的Bug主要集中在安全、资源泄漏和工具执行逻辑上，多数已有对应的修复PR。

| 严重程度 | Bug描述 | Issue链接 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **P1 (高)** | `complete_goal`工具因参数解析错误导致Agent无限循环 | [#4864](https://github.com/HKUDS/nanobot/issues/4864) | 待处理 |
| **P1 (高)** | Qwen模型暴露推理过程内容 | [#4934](https://github.com/HKUDS/nanobot/issues/4934) | 已有PR [#5023](https://github.com/HKUDS/nanobot/pull/5023) |
| **P2 (中)** | `except BaseException` 误捕获`KeyboardInterrupt`和`SystemExit` | [#4788](https://github.com/HKUDS/nanobot/issues/4788) | 已关闭 |
| **P2 (中)** | `read_file`加载大文件导致OOM | [#4785](https://github.com/HKUDS/nanobot/issues/4785) | 已关闭 |
| **P2 (中)** | `Session.messages`列表无限增长，导致资源泄漏 | [#4787](https://github.com/HKUDS/nanobot/issues/4787) | 已关闭 |
| **P3 (低)** | Exec sessions关闭后未清理子进程，产生孤儿进程 | [#4794](https://github.com/HKUDS/nanobot/issues/4794) | 已关闭 |
| **P3 (低)** | API密钥以明文形式存储在配置文件中 | [#4803](https://github.com/HKUDS/nanobot/issues/4803) | 已通过PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) 在文档层解决 |

另外，PR [#4987](https://github.com/HKUDS/nanobot/pull/4987) 和 [#4663](https://github.com/HKUDS/nanobot/pull/4663) 虽然以PR形式出现，但本质是在修复深层安全漏洞和协议缺陷，也应视为重要的稳定性提升。

## 6. 功能请求与路线图信号

社区对功能的需求呈现 **“可控性”** 和 **“扩展性”** 两大趋势。

- **Agent行为控制**：用户[xiakj](https://github.com/HKUDS/nanobot/issues/5013)提出在执行shell命令前需要**用户确认**，以增加安全屏障。这说明用户希望在生产环境中对Agent的自主操作有更细颗粒度的控制。
- **会话与模型绑定**：PR [#4866](https://github.com/HKUDS/nanobot/pull/4866) 提出将**模型预设绑定到会话**，允许不同会话使用不同的模型配置。这为多模型、多场景应用奠定了基础，很可能被纳入下一个大版本的功能列表。
- **渠道集成**：Issue [#4911](https://github.com/HKUDS/nanobot/issues/4911) 要求渠道（如语音频道）能够调用Agent的工具，暗示了社区对**多模态交互**和**渠道能力拓展**的渴望。
- **技能系统增强**：PR [#5018](https://github.com/HKUDS/nanobot/pull/5018) 提出支持**显式加载技能上下文**，使开发者能更精确地控制哪些技能对Agent可用，提升了系统的模块化与灵活度。

## 7. 用户反馈摘要

从Issue和PR评论中，可以提炼出以下用户心声：

- **痛点明确且强烈**：多位用户（如 `Asem-D`, `The-Markitecht`）在报告中用“totally unusable”、“endless loop”等强烈措辞描述其遇到的问题，表明工具循环和性能问题是当前体验的最大障碍。
- **注重隐私与安全**：用户 `hamb1y` 连续提交了多个关于安全与资源泄漏的issue (`#4803`, `#4785`, `#4787`)，其细致入微的检查和清晰的报告风格，反映出社区对项目安全性、健壮性有极高的期待和要求。
- **中文社区用户存在感增强**：Issue [#5013](https://github.com/HKUDS/nanobot/issues/5013) 和 PR [#5022](https://github.com/HKUDS/nanobot/pull/5022) 的作者均为中文用户，其需求（shell确认、取消目标）直接反映了中文开发者社区在实际部署中遇到的典型问题。
- **对性能敏感**：`The-Markitecht`用户在Issue [#4867](https://github.com/HKUDS/nanobot/issues/4867) (已关闭)中强烈抱怨了与Ollama集成时的性能瓶颈（每轮增加60秒延迟），凸显了本地模型推理性能优化对提高用户体验的重要性。

## 8. 待处理积压

以下为值得维护团队重点关注、但仍处于开放状态的重要工作项。

- **高优先级修复**：
    - **`complete_goal`无限循环**：Issue [#4864](https://github.com/HKUDS/nanobot/issues/4864) 是影响任务完成的严重Bug，目前尚无对应的修复PR，需要优先排查。
    - **`/stop`命令对子代理进程的清理**：PR [#5021](https://github.com/HKUDS/nanobot/pull/5021) 尝试修复此问题，但仍在开放中。该问题确保了Agent在被中断时不会留下残留进程，是系统稳定性的关键。
- **长期未合并的功能**：
    - **WebUI定制化**：PR [#4399](https://github.com/HKUDS/nanobot/pull/4399) (创建于6月18日) 提出了隐藏特定UI设置项的功能，以简化非技术用户界面。该PR已存在冲突，需要维护者协调解决，它代表了项目向“易用性”迈进的明确信号。
    - **Shell命令执行的安全防护**：PR [#4594](https://github.com/HKUDS/nanobot/pull/4594) (创建于6月29日) 尝试修复Shell工作区防护的绕过漏洞，是安全领域的重要一环，需要尽快处理合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的Hermes Agent项目数据，我为您生成了2026年7月22日的项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-22

## 今日速览

Hermes Agent 项目今日整体活跃度**极高**，处于密集开发与社区反馈的爆发期。过去24小时内，项目仓库迎来了50个新Issue和50个新PR，尽管无新版本发布，但在问题处理、功能演进和Bug修复方面均有大量动作。社区讨论热情高涨，主要集中在三大方向：**内存/技能系统的可配置性与安全**、**桌面版与TUI的长期会话稳定性**，以及**MCP（模型上下文协议）工具连接的健壮性**。同时，多个P1/P2级别的严重Bug被报告并已有对应的修复PR提交，显示出项目团队对稳定性的高度重视和快速响应能力。总体来看，项目正处于**功能密集扩展与大规模Bug修复并行**的活跃阶段。

## 项目进展

今日尽管没有发布新版本，但项目通过合并多个关键PR取得了实质性的前进。

- **Windows平台稳定性修复**：PR [#68997](https://github.com/NousResearch/hermes-agent/pull/68997) 被成功合并，彻底解决了Windows系统下 `git probe` 因进程清理不当导致的死锁问题。该修复统一了多个调用点的进程管理逻辑，是解决Windows平台兼容性的重要一步。
- **MCP连接与测试健壮性提升**：PR [#68896](https://github.com/NousResearch/hermes-agent/pull/68896) 被合并，修复了一个仅在CI环境中偶发的测试失败，通过将MCP断路器的时间基准修正为单调时钟，提升了测试环境的可靠性。
- **桌面版UI/UX修复**：PR [#69019](https://github.com/NousResearch/hermes-agent/pull/69019) 已提交，旨在修复长时间运行的桌面会话中，对话记录出现漂移的视觉问题。这表明项目在关注核心功能的同时，也在积极打磨用户体验。
- **多项功能与修复进行中**：数十个新PR在今日被创建，涵盖了代理会话恢复、行为分析、压缩逻辑、MCP工具发现等关键领域。其中，PR [#68766](https://github.com/NousResearch/hermes-agent/pull/68766) 旨在解决代理在供应商服务暂时中断时的会话恢复问题，直击核心可靠性痛点。

## 社区热点

今日社区讨论热度集中在几个关键的系统缺陷和功能诉求上。

1.  **MCP服务器重新连接后工具丢失** (Issue [#67187](https://github.com/NousResearch/hermes-agent/issue/67187))
    - **热度**: 7条评论，已关闭。这是过去24小时内讨论最热烈的问题之一。
    - **诉求**: 用户报告，当Streamable HTTP MCP服务器被“停放”后，即使代理成功重新连接并协商了新的MCP会话，其注册的工具也无法恢复。这直接导致代理在重启后无法调用这些服务器的任何功能，对依赖外部工具的自动化场景构成重大障碍。

2.  **记忆系统与技能系统的深度改造需求** (Issues [#47349](https://github.com/NousResearch/hermes-agent/issue/47349), [#25083](https://github.com/NousResearch/hermes-agent/issue/25083))
    - **热度**: 分别有13条和7条评论。
    - **诉求**: 这是社区对Agent核心架构的深度讨论。
        - **#47349** 提出应将硬编码的 `MEMORY.md` 重命名为 `rules.md`，并让记忆后端变得可配置，允许用户直接使用 `honcho/fact_store` 等外部系统。
        - **#25083** 则要求增加“不可变/受保护技能”功能，防止Agent在未经用户明确许可的情况下修改或删除安全规则等关键技能。
        - 这两个Issue共同反映了社区对**更精细、更安全的Agent行为控制**的强烈渴望，不再满足于“全有或全无”的权限模式。

3.  **桌面版/TUI会话泛滥问题** (Issue [#68920](https://github.com/NousResearch/hermes-agent/issue/68920))
    - **热度**: 4条评论。
    - **诉求**: 用户发现当设置了 `max_concurrent_sessions` 限制后，桌面版或TUI的应用会在后台泄漏活动的Session租约文件，最终导致新的会话无法启动，即使实际只有一个会话在活动。这是一个典型的“可用性”Bug，影响用户正常使用。

## Bug 与稳定性

今日报告的Bug数量较多，且涉及多个严重级别。

### 严重 (P1)
- **Worker进程死锁** ([#68915](https://github.com/NousResearch/hermes-agent/issue/68915)): 当Agent通过Shell `&` 在后台启动一个长时间运行的进程时，Worker进程会陷入永久性死锁，无法恢复。**尚无关联修复PR**，风险极高。
- **桌面版更新导致数据库损毁** ([#68474](https://github.com/NousResearch/hermes-agent/issue/68474)): 在Windows上更新至v0.19.0后，`state.db`（SQLite会话数据库）被完全填充为null bytes，导致所有会话数据丢失。**尚无关联修复PR**，这是一个影响数据安全的严重回归。

### 中等 (P2)
- **MCP服务器工具未注册** ([#67187](https://github.com/NousResearch/hermes-agent/issue/67187)): 已解决。
- **会话资源泄漏** ([#68920](https://github.com/NousResearch/hermes-agent/issue/68920)): **尚无关联修复PR**。
- **大数据库文件磁盘I/O饱和** ([#68858](https://github.com/NousResearch/hermes-agent/issue/68858)): 在v0.19.0上，大型`state.db`的压缩操作可能导致磁盘I/O饱和并阻塞网关关闭。
- **Discord命令同步失败** ([#68963](https://github.com/NousResearch/hermes-agent/issue/68963)): 斜杠命令同步遇到HTTP 429错误后不重试，直到重连才恢复。
- **Thread消息顺序错乱** ([#68979](https://github.com/NousResearch/hermes-agent/issue/68979)): 在桌面版长线程中，压缩后用户最近的消息被错误地堆叠到线程底部。

### 较低 (P3)
- **桌面版Rust→V8 IPC桥崩溃** ([#65868](https://github.com/NousResearch/hermes-agent/issue/65868)): macOS上持续崩溃。
- **Thai文字在TUI中显示异常** ([#68990](https://github.com/NousResearch/hermes-agent/issue/68990)): 流式渲染时组合字符丢失或重复。
- **PDF等文件无法打开** ([#68937](https://github.com/NousResearch/hermes-agent/issue/68937)): macOS上点击文件链接会回退到在Finder中显示而非直接打开。

## 功能请求与路线图信号

今日社区提出的功能请求呈现出从“功能可用”向“可控、智能、可扩展”演进的趋势。

- **核心架构演进**
    - **可配置记忆后端** ([#47349](https://github.com/NousResearch/hermes-agent/issue/47349)): 允许用户选择记忆存储方式，具备很高的优先级，很可能纳入下一版规划。
    - **不可变技能保护** ([#25083](https://github.com/NousResearch/hermes-agent/issue/25083)): 提升Agent安全性和可控性的关键需求，可能进入路线图。
    - **插件可扩展 `send_message`** ([#64900](https://github.com/NousResearch/hermes-agent/issue/64900)): 使平台插件能自定义消息发送的Schema和处理逻辑，符合社区期望的开放式架构。

- **工具与界面改进**
    - **原子粒度工具过滤** ([#68964](https://github.com/NousResearch/hermes-agent/issue/68964)): 用户期望能精确控制单个函数的启用/禁用，而非只能控制整个工具集。
    - **TUI `/compress` 支持输入排队** ([#61042](https://github.com/NousResearch/hermes-agent/issue/61042)): 在后台压缩过程中允许用户继续输入，提升TUI使用体验。
    - **桌面版支持搜索时区** ([#68970](https://github.com/NousResearch/hermes-agent/issue/68970)): 改善设置界面的易用性。

- **新功能与集成**
    - **通过 `send_message` 向Atomic Hermes发送消息** ([#68951](https://github.com/NousResearch/hermes-agent/issue/68951)): 打破桌面端与移动端的壁垒。
    - **行为分析与洞察卡** ([#60417](https://github.com/NousResearch/hermes-agent/pull/60417)): PR已存在，旨在提供定性行为分析，可能成为独特卖点。
    - **对 Cron 任务记录耗时和Token用量** ([#46366](https://github.com/NousResearch/hermes-agent/pull/46366)): 已有PR，为自动化任务提供监控基础。

## 用户反馈摘要

从今日的Issue评论中，可以提炼出以下用户痛点和使用场景：

- **“我就是想正常工作”**：Windows用户对更新后数据库丢失数据感到沮丧，表明桌面版的稳定性和升级流程仍需加强。
- **“请给我更多控制权”**：社区反复提及希望自己决定哪些记忆被注入、哪些技能不能被修改、哪些工具函数可以被调用。他们似乎想把Agent从“全能但模糊的工具”变成“安全可控的工艺匠人”。
- **“别再死锁了”**：Worker死锁和MCP工具丢失是最让用户愤怒的Bug，因为它们直接导致代理无法完成任何工作，完全丧失生产力。用户需要Agent在没有人为干预的情况下也能从故障中恢复。
- **“丝滑的体验很重要”**：Desktop/TUI中的界面漂移、输入阻塞等问题，虽然不致命，但严重影响了用户的沉浸式体验。用户希望即使在处理长时间对话时，也能有流畅的界面交互。
- **“想要更好的集成”**：用户希望桌面代理能直接与Atomic Hermes（移动端）通信，暗示了用户希望拥有一个跨平台、无缝连接的Agent生态。

## 待处理积压

以下为一些长期未响应或“需要决策”的重要Issue/PR，提醒维护者关注：

- **Issue [#34385](https://github.com/NousResearch/hermes-agent/issue/34385) (P3, **needs-decision**)**: 自5月底报告以来一直未决的并发场景下Kanban DB索引损坏问题。这是一个影响多Worker协作稳定性的核心问题。
- **Issue [#53819](https://github.com/NousResearch/hermes-agent/issue/53819) (P3, **needs-decision**)**: 同样是Kanban DB在高并发下的损坏问题，讨论已深入到根因分析，但尚未有明确解决方案。
- **PR [#62993](https://github.com/NousResearch/hermes-agent/pull/62993) (P2, **needs-repro**)**: 一个大规模的安全加固PR，涉及TLS、XML解析、Shell注入等多个方面，自7月12日起一直处于开放状态，需要复现和审查。
- **Issue [#23207](https://github.com/NousResearch/hermes-agent/issue/23207) (P3)**: 自5月以来用户关于如何在Ollama中使用Web搜索的提问，至今未解决。这反映了文档或功能集成上的一个缺口。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 PicoClaw 项目数据生成的 2026-07-22 项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-07-22

### 1. 今日速览

今日 PicoClaw 项目活跃度较高，呈现“问题与修复齐飞”的状态。24小时内关闭了4个Issue和3个PR，表明维护团队正在积极清理积压问题。社区围绕 Google OAuth 策略合规、Web UI 性能以及飞书（Feishu）消息类型等方向提交了多项修复（#3280、#3282、#3279）。尽管无新版本发布，但多项关键的 Bug 修复和功能增强代码已经合入主干，项目健康度良好，修复速度跟上社区反馈节奏。

### 2. 版本发布

无

### 3. 项目进展

今日有3个 Pull Request 被合并或关闭，其中几项关键合并提升了项目的稳定性和功能边界：

-   **修复机器人名称硬编码**：PR #303 [CLOSED] 已被合并。该修复解决了 Telegram 和钉钉（DingTalk）频道中机器人欢迎语和回复标题被硬编码为“PicoClaw”的问题。现在，用户可以通过配置 `bot_name` 字段自定义机器人身份，使其与 `soul.md` 设置的个性化人格保持一致，增强了品牌和角色扮演能力。
-   **引入策略化的系统执行节点**：PR #3282 [CLOSED] 已被合并。这是一个重量级的功能增强，引入了 `system.exec.v1` 节点。该功能允许以高安全策略（策略门控）的方式执行系统命令，包括限制可执行文件、工作目录、环境变量、超时和输出大小。这为构建更安全的自动化工作流和沙箱环境提供了基础能力。
-   **修复 PR #3222 的后向兼容性**：PR #3233 [CLOSED] 已被合并。该项目进展确保了近期功能的修改不会破坏现有用户的配置和使用体验，体现了项目对稳定性的重视。

### 4. 社区热点

今日主要讨论集中在 **Google OAuth 策略合规** 和 **Seahorse 摘要中的工具调用格式泄漏** 两个问题上。

-   **[BUG] Antigravity OAuth login now blocked by Google** (Issue #3278 [CLOSED])
    -   **链接**: [Issue #3278](https://github.com/sipeed/picoclaw/issues/3278)
    -   **分析**: 该问题虽已被关闭，但引发了社区对第三方认证合规性的担忧。用户 `honbou` 报告称，`antigravity` 提供者的 OAuth 登录流程被 Google 新政策阻止。该问题指出了项目需要跟进上游 OAuth 安全规范的紧迫性，并直接促成了修复 PR #3280 的提交。

-   **[BUG] Volcengine Doubao Seed tool calls occasionally leak as text** (Issue #3153 [CLOSED])
    -   **链接**: [Issue #3153](https://github.com/sipeed/picoclaw/issues/3153)
    -   **分析**: 这是一个关于字节跳动豆包模型工具调用异常的 Bug，在关闭前吸引了5条评论。用户反馈工具调用结果有时会以原始 `<seed:tool_call>` 文本的形式暴露给用户，而非被正确执行。此问题与 PR #3279 (fix seahorse 泄漏) 相关，表明社区正在深入解决模型接口的格式处理问题。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在连接稳定性、OAuth 认证和 UI 性能上，其中部分已有直接修复。

| 严重程度 | 问题描述 | Issue | 状态 | Fix PR 状态 |
| :--- | :--- | :--- | :--- | :--- |
| **高** | **Matrix 同步循环无重连逻辑**：网络中断或服务器重启后，同步永久死亡，进程不退出导致 systemd 无法自动重启。 | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | OPEN | 无对应 PR |
| **高** | **Google OAuth 登录被策略阻止**：`antigravity` 提供者登录不符合 Google 最新 OAuth 2.0 政策。 | [#3278](https://github.com/sipeed/picoclaw/issues/3278) | CLOSED | 已关闭，**修复PR [#3280](https://github.com/sipeed/picoclaw/pull/3280) 待合并** |
| **中** | **Web UI 聊天输入延迟**：对话历史稍长时，输入框响应严重卡顿。 | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | OPEN | 无对应 PR |
| **中** | **反重力 (Antigravity) 提供者 `INVALID_ARGUMENT` 回归**：`main` 分支上的回归问题，`tool_schema_transform "simple"` 不再适用。 | [#3274](https://github.com/sipeed/picoclaw/issues/3274) | CLOSED | 已关闭，直接在 `main` 修复。 |
| **低** | **钉钉聊天预览显示固定文本**：聊天列表预览始终显示“PicoClaw”而非实际回复内容。 | [#3255](https://github.com/sipeed/picoclaw/issues/3255) | OPEN | 无对应 PR |

### 6. 功能请求与路线图信号

-   **使用 `vodozemac` 替换 `libolm` (Issue #3088)**：这是一个待处理的、高优先级的旧 Issue（Stale），旨在替换已停止维护且不安全的 `libolm` 库，转向官方替代品 `vodozemac`。目前仍有社区关注（9条评论），该功能请求是提升端到端加密安全性的关键一步。
-   **可配置的模型默认回退链 (PR #3200)**：该 PR 处于待合并状态（Open），它旨在为 Web UI 添加一个可配置的默认模型回退链功能。用户可以通过 API 设置默认模型、备用模型并对它们排序。这直接响应了用户对高可用性和成本控制的需求，有望在未来版本中落地。

### 7. 用户反馈摘要

-   **痛点**：
    -   **OAuth 认证失败**：用户 `honbou` 反映 `antigravity` 提供者的认证流程在远程和 headless 环境下几乎无法正常工作，且失败后会消耗授权码，导致流程必须完全重来，体验极差。该反馈直接促成了 PR #3280 的诞生。
    -   **UI 性能**：用户 `xpader` 报告 Web UI 在长期对话后输入卡顿，这影响了核心聊天体验。
    -   **工具调用格式泄漏**：用户 `ms8great` 反馈在特定模型下工具调用失败，暴露出底层数据格式化问题，可能导致用户看到难以理解的原始文本。
-   **使用场景**：
    -   用户 `MrTreasure` 在使用钉钉时，期望机器人有更个性化的身份展示，间接反映出项目在 IM 机器人品牌定制方面的需求。
    -   用户 `lc6464` 提交的 PR #3200 表明，在复杂生产环境中，用户对模型调用的故障转移和成本控制有明确需求。

### 8. 待处理积压

以下为长期未得到响应的重要 Issue 或 PR，建议维护者关注：

-   **[Feature] use vodozemac instead of libolm** (Issue #3088)
    -   **链接**: [Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)
    -   **状态**: Open, Stale (已打开42天)
    -   **提醒**: 这是提升项目安全性的核心需求，建议尽快纳入开发计划。尽管标有 `stale`，但其 `priority: high` 的标签不应被忽略。

-   **[BUG] Matrix sync loop has no reconnection logic** (Issue #3203)
    -   **链接**: [Issue #3203](https://github.com/sipeed/picoclaw/issues/3203)
    -   **状态**: Open (已打开20天)
    -   **提醒**: 对于任何依赖 Matrix 实时通信的用户，这是一个严重的稳定性问题。目前尚无对应的 PR，需要尽快评估并设计重连机制。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NanoClaw (github.com/qwibitai/nanoclaw) 数据生成的 2026-07-22 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-07-22

## 1. 今日速览

过去24小时，NanoClaw 项目维持了**中等偏上**的活跃度。核心看点包括：**12个PR** 处于活跃状态，表明社区贡献热情高涨，且集中在功能修复与文档建设上。尽管没有新版本发布，但多个长期悬而未决的 PR（如 #2236, #1530）在今日获得了更新，显示维护团队正在积极清理技术债务。一个值得关注的**新 Issue（#3096）** 提出了将 LINE 整合为通信渠道的请求，这符合项目路线图中拓展亚洲市场的信号。

## 2. 版本发布

无。

## 3. 项目进展

今日有 **3个PR被合并/关闭**，主要集中在基础设施维护和社区流程优化：

- **[CLOSED] PR #3095 - docs: rewrite branch maintenance guide**  
  由核心团队成员关闭。此次合并更新了项目分支维护文档，适配了新的 `registry-branch` 模型，有助于降低新贡献者的上手门槛，提升协作效率。
- **[CLOSED] PR #3114 - Langfuse tracing skill**  
  此 PR 可能是在不引入源代码变更的情况下，完成了对 Langfuse 可观测性工具的集成技能投票。
- **[CLOSED] PR #3116 - [follows-guidelines] sync pr**  
  此 PR 看似是一个与主分支同步的例行操作，被关闭可能意味着合并或放弃。

**整体进展**：项目核心代码库（onecli、whatsapp 等）的修复仍在推进，同时社区通过关闭流程性 PR，维护了项目贡献规范的执行。

## 4. 社区热点

- **最受关注 Issue: #3096 - feat: Add /add-line skill for LINE Official Account channel support**  
  [Issue #3096](https://github.com/nanocoai/nanoclaw/issues/3096)  
  在过去24小时获得了 **3条评论**，是目前新 Issue 中讨论度最高的。作者 `joshm1230212` 基于 README 中的 `RFS (Request for Skills)` 流程，正式提议增加 LINE 渠道支持。这反映了社区对**亚洲市场（日本、台湾、泰国）本地化**的强烈渴望，用户正在主动填补官方未覆盖的生态位。

- **高关注度 PR #3115 - fix(onecli): block legacy Gmail API routes**  
  [PR #3115](https://github.com/nanocoai/nanoclaw/pull/3115)  
  这是由 `[core-team]` 成员提出的重要修复。它通过 OneCLI 全局阻止了废弃的 Gmail API 路由，防止用户配置文件被覆盖。该 PR 显示出核心团队在**主动加固项目安全性**，并对已有用户进行平滑迁移考虑。

## 5. Bug 与稳定性

今日无新增 Bugs 报告。但几个**长期存在且今日被更新**的 PR 表明了稳定性工作的进展：

- **严重（待修复）: PR #1530 - fix: add SELinux :z label to Docker volume mounts**  
  [PR #1530](https://github.com/nanocoai/nanoclaw/pull/1530)  
  该 PR 今天获得了更新。它在 Fedora/RHEL 等 SELinux 强制的系统上至关重要，没有它，Docker volume 挂载会导致权限拒绝。此问题若未修复，会严重阻碍使用这些发行版的用户部署 NanoClaw。

- **中等（待修复）: PR #2236 - fix(container): align WORKDIR with actual group mount path**  
  [PR #2236](https://github.com/nanocoai/nanoclaw/pull/2236)  
  该 PR 今日也获得了更新。它修复了容器运行时默认工作目录 (`WORKDIR`) 与实际挂载 Agent 组路径 (`/workspace/agent`) 不匹配的问题，导致 Agent 工作区不可见。这会严重影响容器化部署场景的用户体验。

- **特定渠道 Bug：PR #3113 - fix(whatsapp): stage inbound media**  
  [PR #3113](https://github.com/nanocoai/nanoclaw/pull/3113)  
  修复了 WhatsApp 频道入站媒体文件无法被容器正确读取的问题。这是对特定渠道体验的优化。

## 6. 功能请求与路线图信号

- **高概率加入下一版本：** `LINE` 频道支持 (Issue #3096) 和 `Dial` 频道支持 (PR #3050) 是最明确的路线图信号。这两个功能都直接关系到 NanoClaw 在即时通讯生态中的覆盖面。

- **可观测性集成：** PR #3114 (Langfuse tracing) 表明社区对集成成熟的 LLM 应用可观测性工具有需求，这很可能被纳入项目标准技能库。

- **国际化：** PR #2950 (添加繁体中文 README) 和 Issue #3096 (LINE 支持) 共同指向了项目正在积极拥抱海外（尤其是东亚）社区。

## 7. 用户反馈摘要

- **痛点：文档与实际不一致。** 从 Issue #2236 和 #1530 的长期存在可以看出，用户在使用 Docker 和特定 Linux 发行版时，遭遇了文档未覆盖或默认配置与实际运行环境不匹配的“坑”。

- **痛点：渠道兼容性不足。** Issue #3096 的作者明确表示，现有渠道注册表中缺乏 LINE 的支持，而他/她需要搭建 `@chat-adapter/line` 这样的包。这体现了用户希望“开箱即用”覆盖更多主流通讯平台。

- **需求：安全与配置管理。** PR #3115 (OneCLI) 和 PR #3111 (Telegram URL 保护) 的提出，反映了用户实际部署中会遇到的安全和配置冲突问题，例如系统 PostgreSQL 与 OneCLI 的端口冲突（PR #3112），以及 Telegram Markdown 解析器的奇怪行为。

## 8. 待处理积压

以下为**长期未响应**但已由用户提出解决方案（即存在 open PR）的关键 Issue，提醒维护团队优先关注：

1.  **SELinux 兼容性 (PR #1530)**  
  创建于 2026-03-29，已有明确的修复方案 (`:z` 标签)。长期未合并会阻塞大批 Linux 用户。  
  [PR #1530](https://github.com/nanocoai/nanoclaw/pull/1530)

2.  **容器 WORKDIR 路径错误 (PR #2236)**  
  创建于 2026-05-03，这是一个影响所有容器化部署的基础错误，已有完整修复逻辑。  
  [PR #2236](https://github.com/nanocoai/nanoclaw/pull/2236)

3.  **WhatsApp 媒体处理回归 (PR #2896)**  
  创建于 2026-06-30，这是一个合并了 PR #2895 后发现的**高优先级回归**，影响审批流程。  
  [PR #2896](https://github.com/nanocoai/nanoclaw/pull/2896)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是为 2026-07-22 生成的 IronClaw 项目动态日报。

---

# IronClaw 项目日报 — 2026-07-22

## 1. 今日速览

项目状态：**高度活跃，重构冲刺期**。过去24小时内，项目共处理了91项事务（41个Issues + 50个PRs），并发布了`ironclaw-v1.0.0-rc.1`候选版本。核心团队正全力推进“Reborn”架构的最终落地，尤其在运行时存储统一、授权模型精炼和可恢复性模型方面有多个大型PR合并与推进。社区讨论主要围绕`v1.0.0-rc.1`的重大变更以及“Reborn”架构的完整发布计划展开。

## 2. 版本发布

- **`ironclaw-v1.0.0-rc.1`** (Release Notes & Artifacts)
    - **发布日期**: 2026-07-20
    - **性质**: 里程碑式的候选版本，包含对Agent运行时、存储、扩展宿主和Web UI的**从零开始的重建**。这不是0.29.x系列的增量更新。
    - **核心变化**: `ironclaw`二进制文件现已替换为重构后的CLI。v1单体应用现在构建为`ironclaw`。
    - **影响**: **破坏性变更**。所有基于旧架构的配置、技能、工具和扩展可能都需要迁移。强烈建议所有用户和贡献者仔细阅读**迁移指南**（如已提供）并开始在生产环境外的沙盒中进行测试。
    - **后续**: 团队将根据此RC版本的反馈进行修复和优化，直至正式版`v1.0.0`发布。

## 3. 项目进展

核心团队在“Reborn”架构合并上取得了关键进展，多个XL规模PR被合并或推进：

- **运行时存储统一**：
    - **PR #6442** ([OPEN] nearai/ironclaw PR #6442): 将生产运行时存储统一到`CompositeRootFilesystem`下，移除了对底层libSQL/Postgres文件系统类型的直接暴露，简化了生产环境配置。
    - **PR #6430** ([CLOSED] nearai/ironclaw PR #6430): **已合并**。移除了所有内存中的ratchet存储，将其迁移至文件系统支持的存储，提升了数据持久性和可靠性。
- **授权模型精炼**：
    - **PR #6432** ([CLOSED] nearai/ironclaw PR #6432): **已合并**。实现了“证人”（witness）始终存在和路由矩阵，使函数调用分发完全依赖授权“证人”。这是`authorize()`合并工作的关键后续。
    - **PR #6438** ([OPEN] nearai/ironclaw PR #6438): 进一步扩展，将生产环境的调度器请求替换为密封的`Authorized`分发，并引入`ProcessAuthorizedContinuation`以支持持久化进程的重新授权。
- **模型可恢复性**：
    - **PR #6437** ([OPEN] nearai/ironclaw PR #6437): 这是一个关键的质量改进PR。它将模型可修复的错误（如请求失败、沙箱计划失败）路由至类型化的恢复路径，确保模型能获取错误原因并有机会重试，而非直接崩溃。直接呼应了**Issue #6284** ([OPEN] nearai/ironclaw Issue #6284)的史诗目标。
- **QA与测试**：
    - **PR #6439** ([OPEN] nearai/ironclaw PR #6439): 引入了通用Mock LLM适配器，将42条采集的QA轨迹转化为可执行的参数化测试，显著增强了回归测试能力。
    - **PR #6422** ([OPEN] nearai/ironclaw PR #6422): 建立了完整LLM调用轨迹采集机制，为后续的调试和性能分析奠定了基础。

**项目健康度**：核心功能重构接近尾声，已进入稳定性打磨和QA测试阶段。

## 4. 社区热点

- **#6389 ([OPEN] nearai/ironclaw Issue #6389)**: **`Phase 4: collapse build_local_runtime + build_production_shaped`**
    - **热点分析**: 该Issue在24小时内收集了10条评论，讨论如何合并本地和生产环境的两套运行时构建路径。这反映了社区对**简化部署配置**和**统一开发与生产一致性**的强烈诉求。评论中，核心贡献者`ilblackdragon`正在阐述如何通过`DeploymentConfig`参数化一个单一的`build_runtime`函数，解决当前配置复杂且容易出错的问题。

- **#6434 ([OPEN] nearai/ironclaw Issue #6434)**: **`Seal process re-dispatch — re-mintable process-lifetime authority`**
    - **热点分析**: 此Issue紧跟`authorize()`合并工作，是授权模型精炼的最后一块拼图。它提出通过“密封进程重新分发”来删除松散的`CapabilityDispatchRequest`。评论虽少但讨论深入，核心开发者在设计如何让进程在重启后还能保持对资源的访问权限，这是构建**长时间运行、有状态的Agent**的关键。

## 5. Bug 与稳定性

- **重大 / 待修复**:
    - **PR #6437** ([OPEN] `fix(reborn): make model-visible failures recoverable`): 旨在解决模型遇到错误后无法恢复的问题，直接关联长期存在且优先级高的**Epic #6284**。尚未合并，但已有明确的修复方案。
    - **PR #6425** ([OPEN] `fix(webui): restore SSE streams across navigation`): 修复Web UI中SSE流在导航时断开的问题。这是一个影响用户体验的常见回归问题，已有PR在等待审查。

- **安全更新**:
    - **PR #6440** ([OPEN] nearai/ironclaw PR #6440) 和 **PR #6196** ([CLOSED] nearai/ironclaw PR #6196): Dependabot自动发起了对前端依赖库`dompurify`的更新（从3.2.3更新至3.4.12），这是一个用于防御XSS攻击的库。**请尽快合并PR #6440**以确保用户安全。

## 6. 功能请求与路线图信号

- **#6433 ([OPEN] nearai/ironclaw Issue #6433)**: **`Feature: Dedicated custom instructions / master prompt section`**
    - **诉求**: 用户请求增加类似ChatGPT/Claude的“自定义指令”/“主提示词”UI功能，以便持久化个性化设置，避免每次对话重复输入。
    - **路线图信号**: 这是用户驱动的常见需求。考虑到`v1.0.0-rc.1`已发布，此功能很可能被视作v1.1或v2的重要UX改进。社区贡献者`sergeiest`已提交此请求，若有相应PR出现，将加速其落地。

- **#6434 ([OPEN] nearai/ironclaw Issue #6434)** 和 **#6389 ([OPEN] nearai/ironclaw Issue #6389)**: 这两个Issues虽然技术上属于重构，但其目标是提升架构的简洁性和可维护性，这间接响应了社区对**“更易配置、更轻量级”Agent**的诉求。这符合项目的长期架构演进方向。

## 7. 用户反馈摘要

- **安全性**：用户对`dompurify`安全更新的快速响应表示认可。
- **配置复杂性**：从**#6389**的讨论来看，用户（尤其是运维和高级用户）对当前`build_local_runtime`和`build_production_shaped`的冗余配置感到困惑，支持将其合并为统一的、参数化的构建函数。
- **模型可恢复性**：**#6284**史诗级Issue下，多位贡献者表达了“模型在遇到50%的随机错误后就崩溃”的痛点，对**PR #6437**的修复方案表示期待。

## 8. 待处理积压

- **#5503 ([OPEN] nearai/ironclaw PR #5503)**: **`[ Experiment ] Add compact Google extension capabilities`**
    - **状态**: 自2026-07-01以来无新活动，超过2周。
    - **提醒**: 这是一个实验性PR，增加了Google扩展的简洁能力。其“实验”标签和长时间未更新，可能表示其优先级较低或遇到阻塞。建议维护者更新其状态或关闭。

- **#5563 ([OPEN] nearai/ironclaw PR #5563)**: **`feat(webui): design system tokens + /playground`**
    - **状态**: 大型PR，来自新贡献者`achalvs`。自2026-07-02创建，已近3周且评论数较少。
    - **提醒**: 这是一个对Web UI未来发展有益的设计系统PR。考虑到`v1.0.0-rc.1`刚发布，团队注意力可能集中在核心功能上。建议核心维护者花时间审查并给出明确反馈，无论是鼓励继续开发还是暂缓，以保持社区贡献者的积极性。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据 LobsterAI (github.com/netease-youdao/LobsterAI) 在 2026-07-22 的项目数据生成的每日动态日报。

---

# LobsterAI 项目动态日报 | 2026-07-22

## 1. 今日速览

今日项目活跃度较高，主要体现在 Pull Request (PR) 的密集处理上，共有 10 条 PR 更新，其中 5 条已成功合并/关闭。核心开发团队正在积极推进多个关键领域的修复与改进，特别聚焦于多模态模型切换的体验一致性和 Artifacts 功能的权限管理。尽管 Issue 活动相对平静（仅 1 条活跃），但该 Issue 与社区反馈的问题高度相关，并已有对应的修复 PR，体现了项目对用户反馈的快速响应。整体来看，项目处于功能打磨与稳定性的提升阶段。

## 2. 版本发布

无

## 3. 项目进展

今日项目闭环处理了 5 个 PR（已合并或关闭），主要推进了以下功能与修复：

- **浏览器注释 (Cowork) 功能完善**：合并了 `#2371`，该 PR 对 Cowork 功能进行了多项优化，包括支持无评论但包含样式修改的注释、在 UI 中展示元素修改前后的值、优化标注状态同步以及修复清理草稿注释时残留的 webview 标注状态。这标志着 Cowork 注解功能从基础可用向精细体验迈进了一大步。
- **Artifacts 分享与部署流程优化**：合并了 `#2370` 和 `#2369`。`#2370` 统一了 Artifact 在分享和部署时的订阅权限拦截逻辑；`#2369` 则细化了分享流程，区分了“创建”和“更新”权限，避免了弹窗自动创建分享的干扰，并增加了停止服务和权限更新的成功反馈。这些改动显著提升了 Artifact 在协作和发布场景下的用户体验和逻辑严谨性。
- **OpenClaw Token 代理与 SSE 截断修复**：合并了 `#2372`，修复了 OpenClaw Token 代理 (Proxy) 在处理 Server-Sent Events (SSE) 时可能出现的数据截断问题，提升了长文本或流式传输下网络代理的兼容性与稳定性。
- **Windows 静默更新功能**：合并了 `#2368`，实现了 Windows 平台上利用 NSIS 安装程序的静默更新能力。安装过程将通过后台启动并自动提权，用户无需等待交互式安装向导，应用更新后可自动重启，显著改善了 Windows 用户的升级体验。
- **图片附件与模型能力同步**：提交了修复 PR `#2373`，该 PR 旨在解决今日活跃 Issue `#1861` 中描述的问题，确保图片附件（base64/文件路径）能根据所选模型是否支持视觉能力（Vision）进行实时动态同步，是解决当前社区热点问题的关键一步。

## 4. 社区热点

今日最受关注的议题是 **Issue #1861: 图片附件不随模型切换重新处理（supportsImage 状态不同步）** ([链接](https://github.com/netease-youdao/LobsterAI/issues/1861))。

- **诉求分析**：该 Issue 详细描述了在多模态大模型切换时（如从非视觉模型切换到视觉模型，或反之），图片附件的处理状态（base64 编码或文件路径）无法同步更新的问题。这直接导致了用户在使用视觉模型时无法正确发送图片内容，或非视觉模型收到无用的 base64 数据，严重影响了对话流程和模型输出质量。这是多模态大模型客户端中一个核心且用户感知极强的交互痛点。

- **响应情况**：令人欣喜的是，开发团队 `yaodong-shen` 已提交了对应的修复 PR `#2373`，这表明该问题已被高度重视，并有望在下一个版本中得到解决。

## 5. Bug 与稳定性

今日无新报告的严重 Bug。今日合并的 PR 中包含了稳定性相关的修复：

| Bug 描述 | 严重程度 | 相关 PR | 状态 |
| :--- | :--- | :--- | :--- |
| **S**：OpenClaw Token 代理（SSE 截断） | 中等 | [#2372](https://github.com/netease-youdao/LobsterAI/pull/2372) | **已修复 (已合并)** |
| **C**：草稿注释关闭后，Webview 状态残留 | 低 | [#2371](https://github.com/netease-youdao/LobsterAI/pull/2371) | **已修复 (已合并)** |
| **B**：Windows 更新显示交互安装向导 | 低 (体验) | [#2368](https://github.com/netease-youdao/LobsterAI/pull/2368) | **已优化 (已合并)** |

## 6. 功能请求与路线图信号

- **永久隐藏侧边栏广告**：PR `#2374` ([链接](https://github.com/netease-youdao/LobsterAI/pull/2374)) 提议在“设置”中添加一个永久隐藏侧边栏广告横幅的开关，解决用户只能临时关闭广告的问题。这表明项目团队在考虑提升免费用户或不喜欢广告用户的体验，可能与用户增长或商业化策略调整有关。该 PR 目前为 OPEN 状态，已被标记为 `area: renderer`，值得关注其是否会被纳入后续版本。
- **依赖更新长期积压**：三条来自 `dependabot[bot]` 的 PR（`#1279`, `#1280`, `#1281`）旨在升级 `cross-env`, `react-dom`, `vite` 等核心依赖，但已停滞超过3个月。虽然未引起社区热议，但这些依赖的长期未更新可能成为潜在的安全或兼容性风险。项目后续路线图应包含定期的依赖更新计划。

## 7. 用户反馈摘要

从 **Issue #1861** 的反馈来看，用户 `btc69m979y-dotcom` 是一位对产品细节要求较高且有明确多模型使用经验的用户。他提出的问题描述极为清晰，不仅指出问题现象，还总结了三种具体场景（非视觉→视觉、视觉→非视觉、提示不更新），并给出了预期行为。这反映了该类用户的核心痛点：**在不同模型间无缝切换，并能获得符合该模型能力的即时且正确的内容处理体验。** 用户对交互一致性的要求已经超越了功能可用性的层面。

## 8. 待处理积压

以下为长期未响应的 Issue 或 PR，建议维护团队关注：

*   **依赖更新 PRs**：
    *   [#1279] chore(deps-dev): bump cross-env from 7.0.3 to 10.1.0 ([链接](https://github.com/netease-youdao/LobsterAI/pull/1279)) - **已停滞 111 天**
    *   [#1280] chore(deps): bump react-dom from 18.3.1 to 19.2.4 ([链接](https://github.com/netease-youdao/LobsterAI/pull/1280)) - **已停滞 111 天**
    *   [#1281] chore(deps-dev): bump vite from 5.4.21 to 8.0.9 ([链接](https://github.com/netease-youdao/LobsterAI/pull/1281)) - **已停滞 111 天**
    *   **建议**：Review 并合并或关闭这些长期积压的依赖更新 PR，以保持项目依赖的健壮性。

---

**总结**：本日 LobsterAI 项目状态“健康”，开发节奏紧凑。团队在同时推进用户体验（图片同步、注释优化、广告隐藏）、功能完善（Artifacts流程）和平台特性（Windows静默更新）等多个方面的改进。社区反馈的核心Bug已快速得到修复，项目展现出了良好的响应能力和成熟的工程化迭代水准。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 (2026-07-22)

## 1. 今日速览

今日项目整体活跃度较低。过去24小时内无新Issue报告或关闭，也无新版本发布。项目的主要动态是一条由Dependabot自动提交的依赖更新PR，旨在将文档构建工具Astro从7.0.9升级至7.1.3。目前该项目处于相对平稳的维护阶段，社区贡献和核心开发活动节奏有所放缓。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

**待合并 PR：**
- **[#1161] chore(deps): bump astro from 7.0.9 to 7.1.3**：此PR由依赖管理机器人自动提交，旨在将`/docs`目录下的文档构建依赖`astro`从7.0.9版本升级至7.1.3。此举旨在跟进上游修复与改进，确保项目文档构建环境的稳定与安全。目前该PR尚处于开放状态，等待人工审查与合并。该操作属于常规的依赖维护，不涉及功能特性或Bug修复。
    - [PR #1161](https://github.com/moltis-org/moltis/pull/1161)

## 4. 社区热点

今日社区讨论处于静默状态。唯一活跃的PR (#1161) 是由自动化工具发起的，未产生任何人工评论或讨论。目前无社区热点或活跃的议题。

## 5. Bug 与稳定性

今日无新报告的Bug、崩溃或回归问题。项目稳定性状态未见异常。

## 6. 功能请求与路线图信号

今日无新的功能请求提出。结合现有PR分析，项目当前路线图信号不明确，主要活动集中在依赖维护上。

## 7. 用户反馈摘要

今日无用户反馈提交。

## 8. 待处理积压

- **待合并PR**：PR #1161 (`chore(deps): bump astro from 7.0.9 to 7.1.3`) 处于待合并状态。建议维护者尽快审查并合并，以保持文档构建环境的安全性与兼容性。
    - [PR #1161](https://github.com/moltis-org/moltis/pull/1161)

目前无长期未响应的重要Issue。项目积压任务较少，健康度良好，但需关注活跃度下降的趋势，以避免项目冷却。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的CoPaw项目GitHub数据，我为您生成2026年7月22日的项目动态日报。

---

## CoPaw 项目动态日报 | 2026-07-22

### 1. 今日速览

CoPaw (QwenPaw) 项目今日社区高度活跃，共有41条Issue和50条PR更新，显示出强劲的社区参与度。项目发布了 **v2.0.1-beta.1** 修复版本，同时治理（Governance）、上下文管理（Scroll）和OMP工作流等核心模块的PR被合并，标志着项目正在从2.0.0版本的初期铺开向稳定性和架构优化阶段迈进。但针对2.0版本性能和上下文丢失问题的用户反馈仍值得高度关注。

### 2. 版本发布

-   **v2.0.1-beta.1**: 今日发布了该小版本。
    -   **更新内容**:
        -   **修复**: 修复了Tauri桌面应用入口点使用绝对路径的问题，确保跨平台兼容性。
        -   **修复**: 修复了`memoryspace`模块中`_saved_tool_refs`方法未捕获`OSError`的潜在崩溃问题。
        -   **其他**: 版本号提升至2.0.1b1。
    -   **破坏性变更**: 无。
    -   **迁移注意事项**: 这是一个小版本修复更新，用户可直接升级。

### 3. 项目进展

今日有多项重大PR被合并/关闭，标志着项目核心功能取得关键进展：

-   **核心架构与治理**: 
    -   `#6190 [CLOSED]` **fix(governance): auto-register tools via @tool_descriptor**：统一了工具注册机制，使治理白名单、UI配置等从单一元数据源派生，大幅降低了维护成本。
    -   `#6270 [CLOSED]` **feat: support user editable agent mode**：支持用户直接编辑Agent模式，增强了灵活性和自定义能力。
    -   `#5882 [CLOSED]` **feat(omp): integrate OMP workflow modes**：合入了OMP工作流模式（UltraQA, Ralph等），并增强了`spawn_subagent`功能，是Agent协作模式的重要扩展。

-   **用户体验与稳定性**:
    -   `#6262 [CLOSED]` **feat(agents): add one-click copy of agent configuration**：新增一键复制Agent配置功能，优化了用户配置管理体验。
    -   `#6183 [CLOSED]` **feat(logging): make rotation limits configurable**：使日志轮转大小和备份数可配置，提升了系统的管理性。

-   **安全与沙箱**:
    -   `#5088` & `#5546 [CLOSED]` **feat: initial governance & sandbox interface / generalize governance policy pattern**：完成了治理与沙箱接口的前期讨论和策略模式泛化，为构建更强的安全沙箱奠定了基础。
    -   `#6079 [CLOSED]` **fix: ASK user for permission for sudo**：在执行sudo操作前向用户请求许可，增强了系统安全性。

项目整体正从功能快速添加期，过渡到架构整合、安全加固和体验优化的阶段。

### 4. 社区热点

今日社区讨论最活跃的议题主要集中在两个核心矛盾：**2.0版本带来的性能退化** 和 **Agent循环/上下文污染**。

-   **#2291 [CLOSED]**：[🐾 Help Wanted: Open Tasks — Come Contribute!](https://github.com/agentscope-ai/QwenPaw/issues/2291) (评论: 65)
    -   **分析**：该项目长期存在的“任务认领”帖子始终保持最高热度，说明社区贡献者活跃，项目维护者也在积极引导外部贡献。许多新提交的PR（如 `#6312`）即源于此。

-   **#6257 [CLOSED]**：[[Bug]: Multiple tool calls produce identical thinking output](https://github.com/agentscope-ai/QwenPaw/issues/6257) (评论: 13)
    -   **分析**：用户反馈多工具调用时“思考”内容重复，这直接影响了Agent的智能表现，是社区高度关注的核心能力bug。

-   **#6299 [CLOSED]**：[[Bug]: Deleted session records persist in history.db...](https://github.com/agentscope-ai/QwenPaw/issues/6299) (评论: 3)
    -   **分析**：该Issue详细描述了删除会话后数据残留、序列号冲突导致**跨会话上下文污染**的严重问题。这揭示了2.0版本`Scroll`上下文管理模式的深层设计缺陷，是导致“串会话”的根本原因。对应的修复PR `#6068` 已被标记为重要。

### 5. Bug 与稳定性

今日报告的Bug问题中，以下问题最为关键：

| 严重程度 | Issue ID | 问题描述 | 状态 | 修复/关联PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | #6299 | **删除会话后数据残留，导致序列冲突和跨会话上下文污染**（`history.db`设计缺陷） | 已关闭 | PR #6068 (已修复，正在审查) |
| **严重** | #6307 | **v2.0版本相比v1.x，每次简单对话响应增加了约2秒的固定开销** | 未关闭 | 暂无直接修复PR，需要持续关注 |
| **高** | #6257 | 单轮多工具调用时，所有工具的“思考”内容完全重复 | 已关闭 | 需确认是否由特定PR修复 |
| **高** | #5860 | **2.0版本频繁出现对话进度丢失和无限循环** | 已关闭 | 描述了多个2.0版本的严重稳定性问题 |
| **中** | #6241 | Agent连续轮次重复输出，且`memory_search`工具陷入死循环（框架层缺重复检测） | 已关闭 | 与 #5657（循环检测机制增强）相关联 |
| **中** | #6314 | `RemoteProtocolError: peer closed connection...` （QwenPaw主动关闭连接） | 已关闭 | 用户反馈，需确认是否已解决 |

### 6. 功能请求与路线图信号

用户提出的新功能需求中，以下方向可能与项目路线图相符：

-   **UI交互增强**:
    -   `#6297 [OPEN]` [希望能在对话中直接拖拽上传图片、PDF和office文档](https://github.com/agentscope-ai/QwenPaw/issues/6297)
    -   `#6281 [OPEN]` [希望Web 控制台适配移动端](https://github.com/agentscope-ai/QwenPaw/issues/6281)
    -   `#6083 [OPEN]` [Desktop 窗口增加工作区产出物快捷访问按钮](https://github.com/agentscope-ai/QwenPaw/issues/6083)
    -   **分析**：用户对文件交互和移动端/桌面端快捷操作的呼声很高。虽然已有PR `#6284` (QwenPaw Creator) 尝试文件创作链路，但基础的文件拖拽上传是更通用的需求。

-   **模型与上下文控制**:
    -   `#6318 [OPEN]` [支持按 conversation 级别指定模型](https://github.com/agentscope-ai/QwenPaw/issues/6318)
    -   `#6283 [OPEN]` [在每次发给大模型的会话上下文基础上，自动附加当前真实时间信息](https://github.com/agentscope-ai/QwenPaw/issues/6283)
    -   **分析**：用户希望获得更精细的控制。PR `#5992` (Add per-session model overrides) 已经与 `#6318` 的需求完全对应，意味着该功能很可能被纳入下个版本。

-   **Core架构特性**:
    -   `#6286 [CLOSED]` [Feature Request: Support disabling or customizing built-in tool descriptions](https://github.com/agentscope-ai/QwenPaw/issues/6286)
    -   **分析**：核心用户关注Token成本，希望禁用不用的内置工具描述。这与治理（Governance）模块方向的PR `#6190` 高度契合，说明项目已在着手解决此类问题。

### 7. 用户反馈摘要

-   **主要痛点**:
    -   **2.0版本性能倒退**：用户 `lululau` 在`#6307`中明确指出，升级到v2.0后每次响应有约2秒的“固定开销”，严重影响了体验。这是从1.x升级用户最显著的负面反馈。
    -   **上下文污染**：用户 `arcol` 在`#6299`中详细描述了因`history.db`设计问题导致的“串会话”、“新对话丢失”等严重问题，虽然已“被AI修复”，但过程痛苦，反映了该问题的隐蔽性和破坏性。
    -   **Agent失控**：用户 `MCQSJ` 在`#5860`和用户 `z13645719`在`#6241`中均报告了Agent出现“无限循环”或“重复输出”的问题，表明Agent的循环检测机制仍有待加强。

-   **满意/场景**:
    -   **对更多工作流模式的期待**：PR `#5882` (OMP工作流模式) 获得合并，表明社区对高级Agent编排和协作模式有强烈需求。
    -   **安全意识的提升**：PR `#6079` (为sudo请求许可) 和 `#5088` (治理接口) 的推进，表明项目和安全贡献者正在积极解决用户对Agent权限和安全的担忧。

### 8. 待处理积压

以下为需要维护者关注的长期未响应或关键待审核工作：

-   `#6083 [OPEN]` [Desktop 窗口增加工作区产出物快捷访问按钮](https://github.com/agentscope-ai/QwenPaw/issues/6083)
    -   **情况**：已开放一周，获得3条评论，是对桌面端体验的重要改进建议，至今未收到官方回复或指派。
-   `#5992 [OPEN]` [Add per-session model overrides](https://github.com/agentscope-ai/QwenPaw/pull/5992)
    -   **情况**：由首次贡献者提交的“per-session模型切换”PR，与社区新功能需求`#6318`完全吻合，但已开放10天，至今处于未分配审查者状态，可能打击贡献者积极性。
-   `#6307 [OPEN]` [v2.0 introduces ~2s fixed overhead...](https://github.com/agentscope-ai/QwenPaw/issues/6307)
    -   **情况**：这是一个影响所有2.0版本用户核心体验的关键性能回归问题，目前仅有用户报告，尚未有团队成员的官方回复或分析。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，以下是根据您提供的ZeroClaw项目数据生成的2026-07-22项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-07-22

## 1. 今日速览

ZeroClaw 项目在7月22日继续保持极高的社区活跃度。虽然无新版本发布，但过去24小时内产生了50个Issue和50个PR的更新，显示出强大的开发与讨论动能。项目当前聚焦于三大核心领域：**安全性与稳定性加固**（包括子代理权限绕过、MCP僵尸进程、RSS内存泄漏等严重Bug的修复）、**功能扩展**（特别是OpenAI兼容API、语音对话通道、目标驱动作业模式等重量级RFC提案）以及**架构整理**（SkillForge组件遗留、通道边界清理等）。总体来看，项目处于功能快速迭代与核心架构重构并行的高效开发期。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

过去24小时内，共有9个PR被合并或关闭，标志着以下重要进展：
- **安全性框架推进**：**#9086** (结构性安全审计管道 RFC) 在获得足够的社区反馈后已关闭，表明团队可能已采纳了该方向，后续会有相应设计实现。
- **组件测试与稳定性**：**#8756** (使Windows平台的媒体标记测试可移植) 被合并，提升了跨平台的测试可靠性。**#9120** (SOP路由在错误条件下依然评估分支的Bug) 被关闭，该修复将显著提升标准操作程序执行的正确性。
- **渠道功能完善**：**#7082** (Mattermost WebSocket监听模式) 被关闭，预计该特性即将合并，为用户提供更实时的交互方式。
- **评估与测试基础设施**：一组由 `IftekharUddin` 提出的PR已被合并，包括**#9248** (追加式运行历史收据) 和**#9244** (种子化与分级的隔离内存测试)，增强了Eval框架的追踪和断言能力，标志着项目对质量保障的持续投入。

**里程碑信号**：**#8288** “SOP里程碑：守护进程拥有的SOP控制平面达到5/5” 状态为 “in-progress”，表明SOP这一核心功能正在向完全形态冲刺。

## 4. 社区热点

以下Issue/PR在过去24小时内获得了最高的社区关注度（评论数）：

- **[#8505] [Bug]: Telegram Channel 无法配置 (S1严重性)**
    - **链接**: [Issue #8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)
    - **热度**: 6条评论
    - **分析**: 此Bug被评为S1级别（工作流阻塞），用户报告即使按照快速启动指南配置，Telegram Bot仍然无法响应。评论中提到可能与“channels doctor”组件的诊断结果有关。这直接关系到用户的核心体验（IM通道是Agent的主要交互入口），修复优先级极高。同时，相关的 **#9242** (端到端Telegram设置指南) PR已被提交，旨在从文档层面解决问题，但根本性的Bug修复仍需关注。

- **[#8226] [Feature]: 为内置Git操作添加类型化的每Agent Git身份**
    - **链接**: [Issue #8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)
    - **热度**: 6条评论
    - **分析**: 该Feature Request旨在解决多租户场景下的身份、参数和令牌隔离问题。底层诉求是用户希望在一个ZeroClaw实例中运行多个Agent，每个Agent能使用自己的Git身份进行代码提交、分支管理等操作，且不互相干扰。这反映了用户对 **生产级、多Agent协作场景** 的迫切需求。

## 5. Bug 与稳定性

过去24小时内报告了多个严重级别的Bug，按严重程度排列如下：

- **S0 - 数据丢失/安全风险**:
    - **[#9247] [Bug]: Shell 工具工作区边界绕过**
        - **描述**: Shell工具未能强制遵守工作区边界，通过符号链接可以访问工作区外的文件。
        - **链接**: [Issue #9247](https://github.com/zeroclaw-labs/zeroclaw/issues/9247)
        - **分析**: 这是一个严重的安全漏洞，直接突破了沙箱机制。目前尚无Fix PR，需要立即关注。
    - **[#8279] [Bug]: 子代理绕过父级工具允许列表**
        - **描述**: `delegate`工具不会过滤父级的工具集，子Agent可以调用父级策略禁止的工具。
        - **链接**: [Issue #8279](https://github.com/zeroclaw-labs/zeroclaw/issues/8279)
        - **分析**: S0安全Bug，可能导致越权操作。虽已有2条评论但尚无明确Fix PR，是项目安全性的一大隐患。

- **S1 - 工作流阻塞**:
    - **[#8505] Telegram 渠道无法配置**
        - **链接**: [Issue #8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)
        - **分析**: 见“社区热点”章节。此Bug影响用户入门与核心功能使用。

- **S2 - 行为降级**:
    - **[#8731] [Bug]: Stdio-based MCP 服务器积累为僵尸进程**
        - **描述**: MCP子进程未能被正确回收，长时间运行会积累大量僵尸进程。
        - **链接**: [Issue #8731](https://github.com/zeroclaw-labs/zeroclaw/issues/8731)
        - **分析**: 影响系统稳定性，属于资源泄漏问题。已有 `in-progress` 标签，表明修复正在进行。
    - **[#8642] [Bug]: MCP/工具模式克隆导致Agent循环中RSS无限增长**
        - **描述**: 工具模式的频繁克隆导致内存无限增长，是WSL2下OOM的核心原因之一。
        - **链接**: [Issue #8642](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)
        - **分析**: 可能导致长时运行服务耗光内存。问题是 `in-progress`，表明团队正着手修复。
    - **[#8718] [Bug]: `zeroclaw config init` 生成的配置文件被守护进程拒绝**
        - **描述**: 默认配置模板自带错误，导致语音转文字功能静默失效。
        - **链接**: [Issue #8718](https://github.com/zeroclaw-labs/zeroclaw/issues/8718)
        - **分析**: 这是严重的开箱即用体验问题。默认配置不正确会让新用户感到困惑。

## 6. 功能请求与路线图信号

- **高优先级（P1）**:
    - **[#8505] Telegram 渠道修复**：虽为Bug，但修复此功能是当务之急。
- **RFC/长期功能（P2）**:
    - **[#8303] 目标模式**：实现有界自主会话的“目标模式”，是构建持久化Agent任务的关键。
    - **[#8603] OpenAI Chat Completions 兼容层**：需求非常强烈，能让ZeroClaw接入Open WebUI、LobeChat等流行前端。对应的**PR #8486**已在开发，纳入下个版本的可能性极高。
    - **[#8780] 语音对话通道**：提出为Gemini Live等构建实时语音通道。这是多模态交互的前沿方向，虽然P2但展示了项目对未来交互方式的探索。
    - **[#8568] 多Agent混合模型 (MoA)**：允许用户选择“法官”模型，由多个“参考”模型提供分析。这是一个极具吸引力的高级功能，能显著提升复杂任务的完成质量。
- **清理与内部重构（P2/P3）**:
    - **[#8309] SkillForge 组件修复或移除**：这个自动技能发现引擎目前是“孤立”的，社区在讨论是真正集成它还是移除代码。这反映了项目在发展过程中如何处理早期探索性功能。

## 7. 用户反馈摘要

- **积极反馈**：在 **[#8568]** (MoA特性)中，用户提到“从moltis迁移过来，ZeroClaw具备了我所需的大部分能力”，并仅提出了一项缺失的特性（模型切换便利性）。这表明ZeroClaw的功能集已经能够满足从其他平台迁移过来的高级用户。
- **痛点反馈**:
    - **文档与实例不符**：**#8810** 用户表述尖锐，指出Telegram文档中的例子是“错误的”，直接导致了 `channels doctor` 报错，并批评这种“草率的输出”。这提示项目需要加强文档的审查和测试。
    - **配置陷阱多**：**#8718** 中用户指出通过 `config init` 创建的配置文件本身存在问题，导致新用户陷入“静默失败”的困境，这是一种极不友好的用户体验。
    - **学习曲线陡峭**：**#8505** 和 **#8810** 显示，即使有快速的启动指南，用户在配置Telegram这样基础的功能时仍会遇到阻碍，说明某些配置逻辑或文档流程可以进一步简化。

## 8. 待处理积压

- **[#9240] save_dirty 静默丢弃包含句点的配置键**
    - **链接**: [Issue #9240](https://github.com/zeroclaw-labs/zeroclaw/issues/9240)
    - **描述**: 用户尝试保存如 `gpt-4.1` 或 `claude-3.5-sonnet` 等模型特定配置时，写入操作会静默失败，因为点号被错误地解析为路径分隔符。
    - **提醒**: 此Bug影响所有模型配置（尤其是代价、速率限制等），且静默失败的特性使其难以被察觉，但会导致配置永久丢失。这是一个中等风险但影响面很广的配置系统错误，需要优先安排修复。

- **[#8638] feat(skills)!: 用git-catalog --skill选择器替换内置 ClawHub 源**
    - **链接**: [PR #8638](https://github.com/zeroclaw-labs/zeroclaw/pull/8638)
    - **描述**: 一个带有破坏性变更的重构PR，移除硬编码的ClawHub技能源，转向更通用的Git仓库。目前状态为 `needs-author-action`（等待作者更新），长期搁置可能会导致相关代码与主分支冲突加剧，增加合并难度。维护者需要关注作者或社区来推动此PR。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*