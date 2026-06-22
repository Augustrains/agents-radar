# OpenClaw 生态日报 2026-06-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-22 02:30 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw 项目数据，我为您生成了 **2026-06-22** 的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-22

### 1. 今日速览

项目今日处于 **高度活跃** 状态，代码库与社区讨论都呈现出密集的态势。过去 24 小时内，项目收到了约 **500 条 Issues** 和 **500 个 PRs** 的更新，其中新提交的 PR 和活跃问题占比极高，表明开发者和用户正在积极贡献和反馈。然而，项目的待处理积压也相当可观，大量新开的 Issues 和 PRs 尚待维护团队审阅。总体来看，OpenClaw 正处于一个快速迭代、功能丰富但稳定性挑战并存的阶段，社区需求旺盛，但维护者需要投入大量精力来消化这些贡献和修复回归问题。

### 2. 版本发布

**无新版本发布。** 最新版本仍为 **v2026.6.10-beta.1**，该版本于近日发布，主要修复了会话状态、子代理交付和模型别名等核心稳定性问题。

### 3. 项目进展

今日有 **24 个 PR** 被合并或关闭，标志着项目向前迈进了一小步。以下是几个重要的推进：

- **会话状态与可靠性修复：**
    - **`#95636`** `fix(otel): set logBodies=true in default content capture policy` - 修复了诊断-OTel 插件无法正确导出日志正文的问题，解决了 OTLP 日志在 Loki 中不可检索的问题。
    - **`#95635`** `fix(logging): extract OTLP log body for message-first calls` - 与上述 PR 类似，进一步修复了日志记录管道，确保日志消息正文能被正确提取。
- **平台兼容性与上游修复：**
    - **`#68936`** `Autofix: add PR review autofix pipeline + Windows daemon` - 合并了一个大型自动化流水线，引入了 PR 审查自动修复和 Windows 后台守护程序，有助于提升开发效率。
- **其他修复：**
    - **`#70046`** `fix(cron): support HH:MM time-only strings in --at; apply --tz to time-only input` - 改善了 `cron` 命令的用户体验，支持更灵活的 `--at` 参数格式。
    - **`#89897`** `fix(cli): replace hardcoded "--" with FLAG_TERMINATOR constant in getCommandPathInternal` - 修复了 CLI 可能存在子命令解析不一致的潜在问题。

这些合并显示，项目正在稳定地解决一些具体的技术债务和 bug，但相对于庞大的新问题输入，合并速度仍有提升空间。

### 4. 社区热点

今日讨论最激烈的问题主要集中在 **会话状态损坏、消息丢失和回归问题** 上，反映出用户对核心稳定性的高度关注。

1.  **`#86538`** **[Bug]: Session write-lock timeouts block subagent delivery lanes** (12 条评论，Diamond Lobster)
    - **链接**: [https://github.com/openclaw/openclaw/issues/86538](https://github.com/openclaw/openclaw/issues/86538)
    - **分析**: **最热门问题**。会话写入锁超时是阻塞子代理交付、导致交付失败的根本原因。用户要求提供更完善的诊断工具，以便在锁争用发生时能够快速定位。此问题揭示了分布式锁机制在高并发场景下的脆弱性。

2.  **`#86519`** **[Bug]: Agent repeats identical replies 2-10x on Telegram after 5.20 update** (10 条评论，Diamond Lobster)
    - **链接**: [https://github.com/openclaw/openclaw/issues/86519](https://github.com/openclaw/openclaw/issues/86519)
    - **分析**: **高关注度的回归问题**。用户报告在更新后，Telegram 通道上的代理会重复发送相同回复，从 8-10 次减少到 2-3 次但仍未完全修复，表明该 Bug 的修复具有挑战性。用户对这类直接影响交互体验的回归问题容忍度低。

3.  **`#95623`** **[Bug]: tool_use.id sanitizer (#61254) misses OpenAI-responses composite id on cross-provider failover replay → Anthropic 400 bricks session** (7 条评论，Platinum Hermit)
    - **链接**: [https://github.com/openclaw/openclaw/issues/95623](https://github.com/openclaw/openclaw/issues/95623)
    - **分析**: **新上报的高危临界 Bug**。工具调用 ID 消毒器在不同提供商（如 OpenAI→Anthropic）间的故障转移场景下存在缺陷，会导致会话被 `400` 错误锁死。用户已 **提出修复 PR `#95634`**，这是一个紧急且明确的修复信号。

### 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题数量大，严重性高。核心问题集中在 **会话状态、消息丢失、回归和崩溃** 四大类。

- **P0/P1 关键问题 (Diamond Lobster / Platinum Hermit)**
    1.  **`#95623`** **[Bug]**: 跨提供商故障转移时，工具调用 ID 消毒不完整导致会话永久损坏。
        - **严重性**: 🔴 **阻塞性**
        - **状态**: **已有修复 PR `#95634`**，是当前最高优先级。

    2.  **`#95495`** **[Bug]**: 升级后静默移动了记忆存储位置，未提供迁移警告，导致用户必须重新嵌入所有文件。
        - **严重性**: 🔴 **数据隐私与迁移风险**
        - **状态**: 待 Product Decision。

    3.  **`#95248`** **[Bug]**: `release_lane` 诊断操作对持有声明的活跃工作者无效，导致 Telegram 通道卡死，需重启网关。
        - **严重性**: 🔴 **服务不可用**
        - **状态**: 待 Product Decision。

    4.  **`#93375`** **[Bug]**: Telegram 轮询在遇到网络超时后进入静默崩溃循环，健康监控无法自动恢复。
        - **严重性**: 🔴 **自动化恢复失效**
        - **状态**: 待修复。

    5.  **`#92415`** **[Bug]**: `/model` 切换后，会话内部模型快照未刷新，影响后续所有操作。
        - **严重性**: 🔴 **会话状态污染**
        - **状态**: **已有打开的关联 PR**，待合并。

- **P2 稳定性问题 (Diamond Lobster / Platinum Hermit)**
    1.  **`#93905`** **[Bug]**: `/usage` 命令在 Telegram 中失效（回归）。
        - **链接**: [https://github.com/openclaw/openclaw/issues/93905](https://github.com/openclaw/openclaw/issues/93905)
        - **状态**: 已有关联 PR。

    2.  **`#92273`** **[Bug]**: 工具搜索模式 (`mode: "tools"`) 静默破坏了压缩前内存刷新，导致持久记忆丢失。
        - **链接**: [https://github.com/openclaw/openclaw/issues/92273](https://github.com/openclaw/openclaw/issues/92273)
        - **状态**: 已有打开的关联 PR。

### 6. 功能请求与路线图信号

用户社区提出了多个有建设性的功能请求，其中一些与现有的 PR 方向一致，有望被纳入未来版本。

1.  **`#90354`** **[Feature]: Add bounded/validated append semantics for pre-compaction memory flush**
    - **链接**: [https://github.com/openclaw/openclaw/issues/90354](https://github.com/openclaw/openclaw/issues/90354)
    - **信号**: **高价值改进**。用户主动提出为内存刷新增加大小限制、写入后验证和静默失败处理，这是对现有功能的主动防御性增强，预计会被采纳。

2.  **`#90916`** **[Feature]: Topic-session families for one assistant across multiple named context lanes**
    - **链接**: [https://github.com/openclaw/openclaw/issues/90916](https://github.com/openclaw/openclaw/issues/90916)
    - **信号**: **路线图级功能**。用户提出了“主题-会话族”的概念，允许单个助手在不同的上下文中工作，同时共享记忆。这涉及到深层次的会话架构变更，可能被标记为未来版本的功能。

3.  **`#91212`** **[Bug]**: `delivery-recovery` 恢复机制在通道传输层就绪前启动，导致消息丢失。
    - **链接**: [https://github.com/openclaw/openclaw/issues/91212](https://github.com/openclaw/openclaw/issues/91212)
    - **信号**: **与现有 PR 对齐**。该 Bug 与长期存在的 **`#46303`** PR（`fix: drain inbound debounce buffer and followup queues before SIGUSR1 reload`）有很强的关联性。如果 `#46303` 被合并，可能同时解决这一问题。

### 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出用户的以下核心诉求：

- **对稳定性和数据安全的焦虑**: “升级后记忆被静默搬迁了，我不得不重新嵌入 1500 个文件，这让我不敢再轻易升级了。” —— 用户`fenglanhua` (#95495) 的反馈反映了对升级过程中数据安全的高度不信任。
- **对复杂问题的耐心消耗**: “运行在 DigitalOcean 上的体验让我足够失望，决定放弃使用了。成本不值得为了这个体验。” —— 用户`abenarroch` (#88087) 在长期遭遇后台任务和 cron 问题后表达了强烈的离开意愿，这是项目需要警惕的用户流失信号。
- **对核心交互回归的强烈不满**: “更新后，我的 Telegram 机器人像复读机一样回复同一句话 8-10 次，这根本无法使用！” —— 用户`w3-design1` (#86519) 的反馈代表了对严重影响日常使用体验的回归问题的零容忍。
- **对功能缺失的渴望**: “我需要一个助手在多个主题下工作，而不是每次对话都混在一起。这才是真正的个人助手。” —— 用户`ghitafilali` (#90916) 对更高级会话管理功能的渴望，代表了社区对项目架构深度演进的需求。

### 8. 待处理积压

下面列出几项长期未响应或状态停滞的重要 Issue 和 PR，提醒维护团队关注。

1.  **`#86612`** **[Bug]: Docker gateway container restart loop** (Diamond Lobster，5月25日起)
    - **链接**: [https://github.com/openclaw/openclaw/issues/86612](https://github.com/openclaw/openclaw/issues/86612)
    - **积压原因**: 该 Docker 配置相关的崩溃问题已存在近一个月，尚无修复 PR 或明确的解决方案。对于新用户的上手体验是致命打击。

2.  **`#88087`** **[Bug]: Poor UX for long-running background tasks + silent cron wake failures** (Platinum Hermit，5月29日起)
    - **链接**: [https://github.com/openclaw/openclaw/issues/88087](https://github.com/openclaw/openclaw/issues/88087)
    - **积压原因**: 用户已因此问题放弃使用，但 Issue 本身仍开放，等待维护者关注。这是一个重要的信任修复信号。

3.  **`#67080`** **PR: feat(plugins): narrow gateway route loads from manifests** (Size: L, P1, 4月15日起)
    - **链接**: [https://github.com/openclaw/openclaw/pull/67080](https://github.com/openclaw/openclaw/pull/67080)
    - **积压原因**: 这是一个重要的架构性 PR，旨在优化插件的加载和路由。它等待作者回复已超过两个月，可能因为复杂度高或作者失联。考虑鼓励其他贡献者接手或做最终决策。

4.  **`#46303`** **PR: fix: drain inbound debounce buffer and followup queues before SIGUSR1 reload** (Size: XL, P1, 3月14日起)
    - **链接**: [https://github.com/openclaw/openclaw/pull/46303](https://github.com/openclaw/openclaw/pull/46303)
    - **积压原因**: 该 PR 旨在解决热重载时的消息丢失问题，是一个长期困扰社区的痛点。它悬而未决了超过三个月，但随着社区对类似问题（如`#91212`）的关注增加，重新审视并推动其合并变得愈发重要。

---

## 横向生态对比

好的，作为资深技术分析师，我将基于您提供的各项目2026-06-22动态，为您呈现一份横向对比分析报告。

---

### **AI 智能体与个人助手开源生态全景分析报告 (2026-06-22)**

#### **1. 生态全景**

当前，个人AI助手与自主智能体开源生态呈现 **“内部分化、集体攻坚”** 的态势。以 **OpenClaw** 为旗舰的成熟项目正经历“成长的阵痛”，社区贡献井喷但核心稳定性承压，反映了从功能堆叠到质量巩固阶段的关键转型。与此同时，**ZeroClaw、LobsterAI** 等后起之秀在 **安全加固** 和 **上下文管理** 等细分领域积极创新，试图解决上一代系统遗留的顽疾。值得注意的是，安全事件（如MCP绕过、SSRF防护弱化）和核心体验回归（如消息丢失、工具调用失效）已成为跨项目的共同痛点，标志着用户对 **可靠性与安全性** 的刚性需求已超越对新功能的追逐。

#### **2. 各项目活跃度对比**

| 项目名称 | Issues 更新数 | PRs 更新数 | 新版本发布 | 今日健康度 | 综合评价 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| OpenClaw | ~500 | ~500 | 无 | **关注** | 高度活跃但稳定性承压，社区贡献与回归Bug并存，维护者面临挑战。 |
| NanoBot | 高 (至少10个活跃议题) | 14 (合并/关闭) | 无 | **良好** | 活跃且高效，针对安全漏洞和关键Bug的响应迅速，修复与功能开发并重。 |
| Hermes Agent | 50 | 50 | 无 | **良好** | 危机应对典范，高效处理Gemini退役事件，密集修复安全与稳定性问题。 |
| PicoClaw | 中 (多个长期Bug) | 29 (合并/关闭) | v0.3.0-nightly | **良好** | 大扫除式进展，一次性合并大量PR，为v0.3.0版本发布做最后冲刺。 |
| NanoClaw | ~2 (均为新开) | 3 (合并/关闭) | 无 | **警惕** | 进入安全审计期，多个高严重性设计漏洞被曝光，修复工作尚未开始。 |
| NullClaw | 1 | 0 | 无 | **沉寂** | 项目活跃度降至冰点，核心Bug无人响应，处于停滞状态。 |
| IronClaw | 5 | 29 | 无 | **良好** | 高活跃度，聚焦于“Reborn”版本稳定性修复及CI/CD深度优化，工程基建扎实。 |
| LobsterAI | 15 (关闭旧议题) | 0 | 无 | **停滞** | 大量修复已关闭但无关联PR，可信度存疑。新安全漏洞(SSRF)待处理，潜在风险高。 |
| CoPaw | 18 | 36 | 无 | **关注** | “先污染后治理”，v1.1.12引入多项核心回归，但社区响应和修复速度同样迅速。 |
| ZeptoClaw | ~1 | 1 | 无 | **优秀** | 完成重量级CI门禁，项目治理健康，焦点明确，堪称精而美。 |
| ZeroClaw | ~50 | ~50 | 无 | **优秀** | 高度组织化，路线图清晰（v0.8.x版本系列），积极吸纳社区贡献，安全与稳定性是重点。 |
| TinyClaw | 0 | 0 | 无 | **休眠** | 过去24小时无任何活动。 |
| Moltis | 0 | 0 | 无 | **休眠** | 过去24小时无任何活动。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 在个人AI助手和智能体生态中扮演着 **“众矢之的”和“基准平台”** 的双重角色。

- **优势**：其 `github.com/openclaw/openclaw` 拥有无可争议的社区规模和贡献量，是生态中最活跃、功能最全面的项目之一。其“会话状态”、“子代理交付”等核心概念已成为行业通用术语。
- **劣势**：今日数据显示，其成功也带来了“规模诅咒”。单日500+ Issue/PR 的更新量远超其他项目，导致维护响应不及时，大量高优Bug（如会话锁死、消息丢失）长期积压。相比 **IronClaw** 的工程化深耕或 **ZeptoClaw** 的极致聚焦，OpenClaw 的代码库显得 **臃肿且日益不稳定**。
- **技术路线差异**：与 **ZeroClaw** 的“先规划后开发”（采用明确的追踪器与里程碑）不同，OpenClaw 更偏向“社区推动式”，新功能快速涌入，但随之而来的回归问题也更为严重。相比 **NanoBot** 选择重点突破（如MCP安全），OpenClaw 则试图覆盖更广的技术栈，导致资源分散。
- **社区规模：毫无疑问的NO.1**，其社区评论和贡献者活跃度是生态中最高的，这也解释了为何它既是创新的温床，也是Bug的温床。

#### **4. 共同关注的技术方向**

多个项目不约而同地指向了以下几个核心方向：

- **1. 安全与信任（SaaS化与自主Agent的鸿沟）**
    - **涉及项目**：**NanoBot、NanoClaw、LobsterAI、ZeroClaw**。
    - **具体诉求**：**MCP 安全边界绕过**（NanoBot #4435）、**A2A 附件符号链接攻击**（NanoClaw #2828）、**SSRF 防护弱化**（LobsterAI #2181）、**凭证管理**（ZeroClaw #6613）。这表明随着Agent自主性（自我修改、工具调用）的提升，传统的“沙箱”概念已不足以应对新威胁。

- **2. 稳定性与可靠性（不再是“能用”，而是“始终能用”）**
    - **涉及项目**：**OpenClaw、CoPaw、Hermes Agent**。
    - **具体诉求**：**消息/会话状态丢失或损坏**（OpenClaw #86538, #95623）、**工具调用失败/重复**（CoPaw #5354, OpenClaw #86519）、**热重载丢消息**（OpenClaw #46303）。用户对“功能正确性”的不满已超过对“新功能”的渴望。

- **3. 上下文管理与记忆（告别窗口咒语）**
    - **涉及项目**：**CoPaw、ZeroClaw、OpenClaw**。
    - **具体诉求**：**引入“滚动（Scroll）”式上下文**（CoPaw PR #5321）、**压缩后记忆丢失**（OpenClaw #92273）、**Topic-Session 分离**（OpenClaw #90916）。社区正从被动地“记忆”转向主动地“管理”上下文。

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全功能通用智能体 | 开发者、技术爱好者 | 高开放性，模块化插件系统，社区驱动，但复杂度高。 |
| **NanoBot** | 轻量级MCP集成 | 开发者、集成者 | “小核心”思想，专注于MCP工具的安全与高效集成。 |
| **Hermes Agent** | 企业级网关与容器化部署 | 企业用户 | 强调安全隔离与合规性，拥有强大的会话沙箱和提供商管理。 |
| **ZeptoClaw** | 超轻量级、边缘部署 | 嵌入式、物联网 | **极致压缩二进制体积** (<7.5MB)，适用于机器人等资源受限场景。 |
| **CoPaw** | 移动端优先、零代码UI | 普通用户、非开发者 | 强调易用性，支持移动端适配和ZeroCode管理界面。 |
| **ZeroClaw** | 基础架构稳定，版本化路线图 | 严肃开发者、运维人员 | 采用**追踪器（Tracker）** 机制管理版本，工程化程度高，稳定性优先。 |
| **NullClaw** | 原型/实验性质 | 个人爱好者 | 活跃度极低，定位不明，目前处于事实上的停滞状态。 |

#### **6. 社区热度与成熟度分层**

- **Tier S (快速迭代与高影响力):** **OpenClaw, ZeroClaw, Hermes Agent, CoPaw**。这些项目拥有庞大的用户基础和/或活跃的贡献者群体，每日有大量的代码进和和社区讨论，但稳定性挑战也最为严峻。
- **Tier A (质量巩固与工程深耕):** **NanoBot, IronClaw, PicoClaw, ZeptoClaw**。这些项目正从“功能堆叠”转向“质量巩固”。它们可能在总活跃度上略逊于Tier S，但在代码质量、CI/CD、社区治理上更为出色，Bug修复速度更快。
- **Tier B (探索与停滞):** **NanoClaw, LobsterAI, NullClaw, TinyClaw, Moltis**。这些项目反映出开源生态的另一面：有的（NanoClaw, LobsterAI）正在经历严格的安全审计，处于“阵痛期”；有的（NullClaw, TinyClaw, Moltis）则因资源、方向或社区问题而陷入停滞或休眠。

#### **7. 值得关注的趋势信号**

- **“安全左移”是刚需**：**NanoClaw (#2828)** 和 **LobsterAI (#2181)** 的案例表明，Agent 的**横向通讯（A2A）** 和 **纵向配置（MCP审批）** 都存在严重的设计级漏洞。开发者应当预见并防范“Agent互信”带来的放大效应。**将安全审计提前到设计阶段，而非发布后修补**，将成为主流。
- **“能用”与“好用”的分界线：稳定性**：**OpenClaw (#86519)** 等项目中用户因核心功能回归而离开的反馈（“升级后我不能用了”），标志着社区容忍度已从“Bug多”转为“功能失效”。一个不能稳定执行核心任务（如发送消息、工具调用）的AI助手，无论有多少新特性，都将被用户弃用。
- **“MCP”既是创新引擎，也是安全敞口**：**NanoBot (#4435)** 和 **ZeroClaw (#7756)** 的动态揭示了 MCP 协议的双刃剑效应。它极大地扩展了Agent能力，但其安全边界、认证方式和兼容性是未来生态必须解决的共同难题。
- **边缘计算与轻量化是蓝海**：**ZeptoClaw** 的成功表明，在“大模型即服务”的喧嚣之外，对**离线、低功耗、隐私优先**的个人AI助手的市场需求真实存在。将Agent模型压缩至7.5MB是一个明确的技术和商业信号。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是根据您提供的 NanoBot 项目数据生成的 2026-06-22 项目动态日报。

---

## NanoBot 项目动态日报 | 2026-06-22

### 1. 今日速览

今日项目活跃度极高。尽管无新版本发布，但 Issue 和 PR 的更新数量均远超常规水平，显示出社区和开发者团队的密集投入。核心亮点集中在**两项高优先级的 MCP 安全修复**、**针对 Anthropic API 流式响应的关键 Bug 修复**，以及**三项已关闭的 PR**（涉及 TTS 新系统和配置系统的环境变量解析优化）。整体来看，项目正在快速吸收社区反馈，并针对安全性和稳定性进行紧急加固。

### 2. 版本发布

无。

### 3. 项目进展

今日有 **14 个 PR 被合并或关闭**，显著推动项目进步。最重要的进展包括：

- **TTS 与配置系统**：`#4316` feat(tts): add TTS configuration system with multi-provider support 已合并。该项目现在拥有一个支持 OpenAI、Groq (Orpheus) 和 ElevenLabs 的多提供商 TTS 系统，并通过 WebUI 和配置文件暴露设置。
- **环境变量解析**：`#4323`, `#4324`, `#4325` 这三个 PR 被合并，修复了转录（Transcription）和 WebUI 设置模块中环境变量模板（`${VAR}`）未被正确解析的问题。这解决了因密钥未正确加载而导致的静默失败问题，提升了配置系统的可靠性。
- **`tool_use` ID 重复修复**：`#4444` PR 已为 `#4442` Bug 提供了首次修复。该项目正以高优先级处理因流式响应中 `tool_use` ID 重复导致会话“中毒”的关键问题。

### 4. 社区热点

今日社区讨论最活跃的议题集中在**安全性和稳定性**。

- **`#4435` 与 `#4434` - MCP 安全绕过漏洞**: 这两个议题引发了高度关注，它们揭露了 `enabledTools` 白名单配置存在绕过风险，可能导致意外的资源和提示（prompt）能力暴露给模型。**链接**: [#4435](https://github.com/HKUDS/nanobot/issues/4435), [#4434](https://github.com/HKUDS/nanobot/issues/4434)
- **`#4442` - `tool_use` ID 重复导致会话“中毒”**: 用户报告了一个严重 Bug，即流式响应中重复的 `tool_use` ID 会导致整个会话失效，模型“静默”无响应。该问题迅速获得了两个修复 PR (`#4444` 和 `#4443`)，体现了社区对“对话体验”的重视。**链接**: [#4442](https://github.com/HKUDS/nanobot/issues/4442)
- **`#4408` - 钩子（Hook）并发安全问题**: 用户 `waelantar` 报告了 `Nanobot.run()` 的钩子不是并发安全的，这是一个影响系统可靠性的架构级问题。**链接**: [#4408](https://github.com/HKUDS/nanobot/issues/4408)

**分析**：社区对安全边界的严谨性和会话可靠性的要求很高。MCP 安全漏洞和会话“中毒”问题直接威胁到部署在生产环境的 Agent 的稳定性和数据安全，因此获得了最高的讨论优先级。

### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

**高严重性**
- **[Bug] Duplicate tool_use ids in streamed responses poison a session** (`#4442`, OPEN)：会话“中毒”导致 API 400 错误，Agent 静默停止。**已有修复 PR**: `#4444` (OPEN), `#4443` (OPEN)。**链接**: [#4442](https://github.com/HKUDS/nanobot/issues/4442)
- **[Security] MCP `enabledTools` allowlist bypass** (`#4435` & `#4434`, OPEN)：白名单绕过可导致未授权的资源或提示被暴露给模型。**已有修复 PR**: `#4436` (OPEN)。**链接**: [#4435](https://github.com/HKUDS/nanobot/issues/4435), [#4434](https://github.com/HKUDS/nanobot/issues/4434)

**中严重性**
- **[Bug] Nanobot.run() per-run hooks are not concurrency-safe** (`#4408`, CLOSED)：已关闭，通常意味着已被实施修复或确认为异步框架的限制。**链接**: [#4408](https://github.com/HKUDS/nanobot/issues/4408)

**低严重性**
- **[Enhancement] 性能优化：`estimate_prompt_tokens` 冗余 tiktoken 编码** (`#4420`, CLOSED)：已关闭的性能优化请求，但其指出的问题（运行时反复对不变的工具定义进行tiktoken编码）对高性能场景有参考价值。**链接**: [#4420](https://github.com/HKUDS/nanobot/issues/4420)

### 6. 功能请求与路线图信号

- **高优先级/已有 PR**:
    - **MCP 安全加固**：`#4436` PR 已经提交，旨在封堵 `enabledTools` 的白名单绕过漏洞，预计会很快被合并到下一版本中。
    - **`search_history` 工具**：`#4440` 功能请求与 `#4439` PR 相关联，旨在提供一个只读工具来检索 `memory/history.jsonl`。这表明社区希望 Agent 能自主访问历史摘要，而非依赖开发者手动注入。
    - **Heartbeat 模型覆盖**：`#4431` 请求为 Heartbeat 服务提供独立的模型配置，允许使用更便宜或专用的模型，这是对成本优化和生产部署的明确信号。

- **低优先级/待定**:
    - **Mattermost 支持**：`#1011` 是一个已存在数月之久的请求，要求支持 Mattermost 作为通讯渠道，获得了 4 个 👍，反映了对特定平台的需求。
    - **Telegram 富文本消息**：`#4413` 功能请求要求支持 Telegram Bot API 10.1 的 `sendRichMessage`，该功能已在 `#4422` 中实现并关闭，社区的需求已得到满足。

### 7. 用户反馈摘要

- **痛点与Bug**：用户报告的最严重痛点是与 Anthropic 流式 API 的兼容性问题，特别是 `tool_use` ID 重复导致的“会话锁死”，这直接影响了 Agent 的可用性。另一个关键痛点是 MCP 安全配置的预期行为与实际行为不符（`enabledTools: []` 未能拒绝所有能力），这引发了用户对安全性和数据控制的担忧。
- **场景与需求**：用户 `waelantar` 连续提出了钩子并发安全（`#4408`）和 `search_history` 工具（`#4440`）的需求，表明他正在构建一个需要高可靠性和长期记忆的复杂 Agent 应用。用户 `codeLong1024` 从自己的 `nanobee` 项目中发现了性能瓶颈，并主动向上游提报，展示了社区驱动的优秀协作模式。
- **正面反馈**：TTS 功能和配置系统（`#4323` 等）的合并，以及 Telegram `sendRichMessage` 功能（`#4422`）的实现，满足了社区对多媒体和富文本交互的期待。

### 8. 待处理积压

以下两项长期未决但有价值的议题/PR值得维护者关注：

- **`#1011` - Mattermost Bot 及 `#4092` - OpenAI 兼容工具调用解析**：`#1011` 是一个请求 Mattermost 支持的老议题，已获得 4 个 👍，但至今未有实现。`#4092` PR 计划修复 OpenAI 兼容 API 的解析问题（`#4059`, `#4061`），但已开启超过三周未合并，可能存在冲突或需要复核。
- **`#3869` - DeepSeek 消息硬化与 `#4145` - Weather Skill**：这两个 PR 也处于待合并状态超过一个月。DeepSeek 修复对使用该模型的用户至关重要，而 Weather Skill 是官方技能示例的重要补充。**链接**: [#1011](https://github.com/HKUDS/nanobot/issues/1011), [#4092](https://github.com/HKUDS/nanobot/pull/4092), [#3869](https://github.com/HKUDS/nanobot/pull/3869), [#4145](https://github.com/HKUDS/nanobot/pull/4145)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 Hermes Agent 项目 2026年6月22日 数据生成的动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-22

## 1. 今日速览

今日项目活跃度极高，24小时内产生了50条Issue和50条PR，核心聚焦于 **Google Gemini CLI 退役后遗症**的最终解决方案。项目组迅速响应社区危机，已合并/提交了多项关键PR，旨在移除已被谷歌封禁的旧提供程序，并修复由其引发的一系列连锁Bug。同时，安全与稳定性修复仍是今日重点，多个P1级别的安全问题已得到修复。整体来看，项目正处于一次重要的“排雷”与基础设施升级期，社区参与度与维护效率均处于高位。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

今日项目在解决紧急问题和清理技术债务上取得了实质性进展，多个关键PR被合并或进入审查流程。

-   **关键修复与合并**：
    -   **彻底解决 Gemini CLI 危机**: PR #50492 (`feat(providers): remove google-gemini-cli + google-antigravity OAuth providers`) 已提交，计划完全移除已被谷歌封禁的旧OAuth提供程序。这是一个重大决策，标志着项目彻底告别旧时代，并为新提供程序让路。
    -   **安全漏洞修复**:
        -   PR #50531 (`fix(gateway): close both cross-session HERMES_SESSION_* leak vectors`) 已提交，修复了一个P1级安全漏洞，防止会话令牌在子进程中泄漏。
        -   PR #15008 (`fix(tools): escalate SIGTERM→SIGKILL on browser daemon + periodic orphan reap`)**（今日合并）**，该PR修复了旧的浏览器孤儿进程收割器漏洞，并为浏览器守护进程增加了强制终止机制，增强了系统健壮性。
        -   PR #50489 (`feat(process): escalate SIGTERM→SIGKILL on host-pid termination after grace`)**（今日合并）**，为主机进程增加了类似的SIGKILL升级机制，防止进程因僵死而泄漏。
    -   **质量提升**:
        -   PR #50497 (`fix(banner): don't advertise toolsets/skills the agent wasn't given`)**（今日合并）**，修复了CLI横幅错误显示未加载工具的问题，提升了用户体验的真实性。
        -   PR #50538 (`fix(cron): improve cron session title reliability`) 已提交，修复了cron任务会话标题生成的多个问题。

-   **项目整体进展**：项目正通过“移除旧代码 + 强化安全边界 + 修复并发Bug”的组合策略，清除由于外部服务变更（如谷歌弃用Gemini CLI）带来的技术债务。这为引入更稳健的Google Antigravity新提供程序铺平了道路，项目健康度正在快速恢复。

## 4. 社区热点

今日社区讨论的核心议题高度集中，主要由 **Google Gemini CLI 服务终止**事件驱动。

1.  **Google Antigravity 遗留问题汇总**: Issue #50530 (`[Bug]: google-antigravity 遗留 P2 集成问题汇总`) 是今日最受关注的讨论帖之一，汇总了新提供程序的三大核心Bug（子代理崩溃、并发掉线、400错误），反映了社区在从旧服务迁移到新服务时遇到的真实阵痛。
2.  **Gemini CLI 退役引发的连锁反应**: Issue #29294 (`google-gemini-cli provider: Gemini CLI / Code Assist sunsets`) 获得了今日最高的8个👍，表明大量用户受此影响。而 Issue #49701 和 #49705 则详细描述了该提供程序完全失效的状况，社区急需一个明确的解决方案。
3.  **功能需求讨论**: Issue #8950 (`feat: add missing messaging channels`) 虽有5条评论，但热度相对分散。社区更关心的是“现有功能能否继续使用”这个基础问题。

**分析**：社区对平台稳定性的诉求远高于新功能需求。用户的焦点已经从“我想用什么模型”转向了“我当前配置的模型还能不能用”。

## 5. Bug 与稳定性

今日报告了大量Bug，按严重程度排列如下：

-   **P1（严重）**:
    -   **跨会话信息泄漏 (已修复)**: Issue #50531 对应的PR已提交，修复了`HERMES_SESSION_*`环境变量在工具子进程泄漏给其他并发会话的安全漏洞。
-   **P2（高）**:
    -   **Google Antigravity 集成问题 (调查中)**: Issue #50530 报告了子代理崩溃、并发掉线和400错误等多个核心功能受损问题。**已有移除旧提供程序的PR (#50492) 提交，但针对Antigravity的修复可能需要更多PR**。
    -   **OpenRouter 免费模型失败 (排查中)**: Issue #49983 报告使用免费模型时返回HTTP 404错误。
    -   **桌面端“思考”开关异常 (已报告)**: Issue #50449 报告了桌面端推理开关回弹和配置文件写入错误的问题。
    -   **MCP OAuth 超时 (调查中)**: Issue #50485 报告了OAuth认证流程因超时时间设置过短而频繁失败。
    -   **TUI 会话未记录工作目录 (已报告)**: Issue #50438 导致桌面端无法按工作空间对TUI会话进行分组。
    -   **Matrix E2EE 配置失败 (已报告)**: Issue #47759 报告在Windows上安装Matrix扩展时出错。
-   **P3（中）**:
    -   **OpenAI Codex 图片生成失败 (已报告)**: Issue #49008 报告了`tool_choice`参数被服务器拒绝。
    -   **重复会话标题导致崩溃 (已报告)**: Issue #50537 报告了自动生成的重复标题导致`ValueError`。
    -   **终端路径问题 (即将修复)**: PR #50534 已提交，修复了`hermes`命令在子shell的PATH中不可用的问题。
    -   **补丁工具损坏Unicode (已修复)**: PR #50540 已提交，修复了补丁工具在处理Unicode字符时可能导致数据损坏的长期问题。

## 6. 功能请求与路线图信号

-   **#50526** `feat(skills): add importance-search`: 提议新增一个按信号强度而非搜索顺序排序的多源搜索技能。**该项目有一定创新性，但优先级可能不高。**
-   **#50240 & #50293** `feat(self-escalation): Dynamic thinking ON/OFF toggle`: 用户提出让模型根据任务复杂度自动开关推理功能的“自我升级”机制。这反映了用户对API成本优化的强烈需求，**有可能被纳入下一版本的考虑范围**。
-   **#50539** `feat: expose explicit runtime event streams`: 提议暴露运行时事件流，以便仪表盘和TUI等观察者获取更细粒度的状态信息。**这是一个清晰的后端重构信号，有利于插件生态发展**。
-   **#47614** `feat(terminal): add CubeSandbox backend`: 提议增加一个新的安全容器执行后端。**这表明社区对代码执行的隔离性有持续需求**。

## 7. 用户反馈摘要

-   **痛点与不满**：
    -   **外部依赖的脆弱性**：多位用户对Google Gemini CLI的突然停止服务感到困扰，并明确表示希望项目能更主动地应对此类变化。例如 Issue #44943 和 #50338 表达了“必须尽快支持新服务”的紧迫感。
    -   **配置复杂性**：Issue #14327 的用户希望实现按平台配置不同模型，而非使用全局单一模型，这是一个典型的高级用户需求。
    -   **桌面端体验**：Issue #50167 的用户希望在关闭窗口时最小化到系统托盘而非完全退出，这表明桌面应用的使用场景正在从一次性任务向持久化后台服务转变。
-   **满意度**：项目维护者对安全漏洞的快速响应（如PR #50531、#50489）和对核心Bug的及时修复获得了正向反馈，虽然没有直接体现在评论中，但议题的迅速关闭是积极的信号。

## 8. 待处理积压

-   **#8919** `Bug: custom provider config ignored at runtime` (**创建于2026-04-13，P1**): 一个严重的P1级Bug，涉及自定义提供程序配置被忽略。尽管是旧Issue，但若仍未解决，将严重影响用户自定义和自托管部署。**建议维护者重新评估**。
-   **#8950** `feat: add missing messaging channels` (**创建于2026-04-13**): 一个积压许久的功能请求，随着项目向多平台发展，添加IRC、LINE等渠道的呼声会再次升高。**建议在路线图中明确排期**。
-   **#31135** `Proposal: Self-Hosted Mem0 as Memory Provider` (**创建于2026-05-23**): 一个关于支持自托管Mem0的提案，社区有相关的PR尝试但无人跟进。**若团队资源允许，这是增强隐私和本地化能力的好方向**。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是为您生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

今日项目活跃度**极高**，主要集中在大量历史PR的合并清理，共合并/关闭了29个PR，表明项目正在推进一个重大的版本整合与代码清理工作。同时，发布了一个新的夜间构建版本。社区方面，关于“进化”功能持续消耗Token的Bug (#3012) 仍是讨论焦点，但过去24小时内未出现新的重大Bug报告。整体来看，项目正处于从v0.2.9向v0.3.0过渡的关键阶段，代码库正在经历显著的优化和功能收尾。

## 2. 版本发布

**新版本：`v0.3.0-nightly.20260622.287853ab`**
- **类型**: 夜间构建版本
- **链接**: [v0.3.0-nightly.20260622.287853ab](https://github.com/sipeed/picoclaw/releases/tag/v0.3.0-nightly.20260622.287853ab)
- **更新内容**: 这是自动化构建的夜间版本，包含了**从 `v0.3.0` 标签以来 `main` 分支上的所有最新变更**。鉴于今日合并了大量PR，此版本可能包含了许多关键的修复和新功能。
- **破坏性变更**: **未知**。官方警告此版本可能不稳定，建议谨慎使用。由于是夜间构建，可能包含尚未完全测试的破坏性变更。
- **迁移注意事项**: 如果您从 `v0.2.9` 或更早版本升级至此夜间版，请注意配置格式可能已发生变化（详见PR #2766关于V3配置格式的变更），建议先备份配置文件。建议在测试环境验证后再用于生产。

## 3. 项目进展

今日是项目取得重大进展的一天，一次性合并了大量长期积累的PR，表明项目正在进行一次集中的代码清理和功能整合。主要进展包括：

- **核心稳定性与性能提升**: 合并了多个关键修复PR，显著增强了系统的健壮性。
    - `#2906`: 修复了消息总线的背压处理问题，并改善了健康检查的可视性，防止系统在高负载下崩溃。
    - `#2907`: 修复了JSONL存储在崩溃后的元数据漂移问题，确保了数据一致性。
    - `#2905`: 修复了回退链上下文处理逻辑，使过期请求能立即停止，避免不必要的资源消耗。
    - `#2913`: 优化了JSONL会话索引的克隆和TTL刷新机制，提升了缓存命中时的性能。

- **功能完善与开发者体验**: 多项新功能和改进已合并，为v0.3.0发布做准备。
    - `#2891`: 新增“恢复出厂设置”功能，为用户提供了在配置损坏时的恢复路径。
    - `#2752`, `#2831`, `#2832`: 合并了系列PR，重构了模型配置工作流，包括Provider选择和模型表单、模型获取与目录支持以及真实的连接测试功能。
    - `#2673`: 增加了跨平台的串口工具支持，扩展了硬件交互能力。
    - `#2587`: 为Pico Web聊天添加了端到端流式传输和更友好的滚动体验。
    - `#2833`: 增加了真实的连接性验证，改进了测试连接功能的可靠性。

- **文档与构建**: 对文档和构建流程进行了全面同步和修复。
    - `#2766`: 将所有文档同步至V3配置格式，为新版本的用户提供准确指南。
    - `#2487`: 修复了Windows平台的构建问题，确保了跨平台支持。

**总结**: 今日合并的29个PR覆盖了从底层数据一致性到前端用户体验，再到文档和构建流程的方方面面，标志着项目在稳定性和功能完备性上迈出了坚实的一大步。`v0.3.0` 版本的轮廓已基本清晰。

## 4. 社区热点

- **\[BUG\] `#3012`**: [Continuous consumption of tokens every minutes when evolution is enabled](https://github.com/sipeed/picoclaw/issues/3012)
    - **动态**: 问题自6月5日提出以来持续活跃，是社区讨论的焦点之一。拥有5条评论，是过去24小时内未关闭的Issue中讨论最多的。
    - **诉求**: 用户 `xpader` 报告，启用“进化”功能后，即使没有交互，每分钟也会持续消耗API Token。这直接关系到用户的使用成本，是一个严重的功能Bug。用户提供了详细的环境信息（MiniMax, FreeBSD, v0.2.9）。
    - **分析**: 这是一个与“进化”功能核心逻辑相关的性能/资源管理问题。考虑到“进化”是PicoClaw的特色功能，此Bug的优先级应该很高。目前尚未有PR关联此Issue，但今日合并的大量PR中有部分涉及后台任务管理（如`#2906`关于背压处理），或许能提供解决思路。

## 5. Bug 与稳定性

- **\[严重\] \[OPEN\] `#3012`**: [进化功能持续消耗Token](https://github.com/sipeed/picoclaw/issues/3012)
    - **描述**: 启用进化功能后，后台程序每分钟都在消耗Token。
    - **严重程度**: 严重（直接影响用户成本和功能正常使用）。
    - **状态**: 待解决。已有详细复现步骤，但无关联修复PR。

- **\[中\] \[OPEN\] `#3090`**: [Safari iOS <16.4 上控制面板无法工作](https://github.com/sipeed/picoclaw/issues/3090)
    - **描述**: 用户报告在较旧版本的iOS Safari上无法使用PicoClaw控制面板。
    - **严重程度**: 中（仅影响特定旧版本浏览器用户）。
    - **状态**: 待确认和修复。社区已标记为 `stale`，但考虑兼容性，仍值得关注。

- **\[已修复\] `#3044`**: [Matrix 用户ID包含冒号时 `allow_from` 失败](https://github.com/sipeed/picoclaw/issues/3044)
    - **描述**: 在使用标准Matrix用户ID格式（包含冒号）时，`allow_from` 配置不生效。
    - **严重程度**: 高（功能Bug，会错误地拒绝合法用户）。**已关闭**，可能是通过今日合并的某些PR间接修复。

- **\[已修复\] `#3041`**: [`mcp add` 命令错误解析全局标志](https://github.com/sipeed/picoclaw/issues/3041)
    - **描述**: `mcp add` 命令由于禁用标志解析，导致全局标志被错误解析为位置参数，从而破坏HTTP/SSE配置。
    - **严重程度**: 高（功能Bug，影响MCP工具的使用）。**已关闭**，同样是今日合并浪潮中的受益者。

## 6. 功能请求与路线图信号

- **\[NEW\] `#3093`**: [请求支持 SimpleX 或 Tox 网关](https://github.com/sipeed/picoclaw/issues/3093)
    - **地区**: 用户 `Damian-o2` 提出了对隐私通讯协议SimpleX、Wire或Tox的支持需求。
    - **信号**: 反映了社区中对去中心化、高隐私通讯渠道的需求。考虑到PicoClaw已经支持了Matrix、Telegram等，此请求符合项目扩展通讯渠道的长期路线图。
    - **可能性**: 短期内被采纳的可能性较低。这通常是一个较大功能，需要设计适配器。但可以作为`v0.4.0`或更高版本的备选功能。

- **\[进行中/已完成\]**: 从今日合并的PR可以看出，**模型配置工作流的改进** (`#2752` 系列) 和 **“恢复出厂设置”** (`#2891`) 是已被采纳并实现的功能请求。这表明项目维护者积极参与社区需求，并逐步将其落地。

## 7. 用户反馈摘要

- **投诉/痛点**:
    - **Token消耗问题** (#3012): 用户 `xpader` 正在遭遇“进化”功能无节制的Token消耗，是当前最突出的用户痛点。
    - **兼容性问题** (#3090): 用户在旧版iOS设备上无法访问管理面板，影响了使用体验。
    - **配置问题** (#3041, #3044): 用户遇到命令行参数解析错误和渠道访问控制配置问题，反映出软件在配置健壮性方面存在改进空间。

- **满意/肯定**:
    - 虽然今日合并的PR主要来自内部贡献者，但其规模和覆盖面的广度（性能、稳定性、功能、文档）表明项目**正在快速发展并认真解决已知问题**。这对于社区用户而言是一个积极的信号。

## 8. 待处理积压

- **`#3012` [OPEN]**: [进化功能持续消耗Token](https://github.com/sipeed/picoclaw/issues/3012)
    - **状态**: 自创建以来已有17天，虽标记为活跃，但未见修复PR。此Bug是社区投诉的核心，应被列为 **最高优先级处理**。

- **`#3093` [OPEN]**: [请求支持 SimpleX 或 Tox 网关](https://github.com/sipeed/picoclaw/issues/3093)
    - **状态**: 相对较新，更像一个前瞻性功能请求。维护者可以评估其社区支持度（目前仅1个👍），并决定是否将其纳入路线图讨论。

- **`#3090` [OPEN, stale]**: [Safari iOS <16.4 上控制面板无法工作](https://github.com/sipeed/picoclaw/issues/3090)
    - **状态**: 被标记为 `stale`，但这是一个影响部分用户的兼容性问题。维护团队应明确是否将继续支持此特定场景。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于您提供的NanoClaw GitHub数据生成的2026年6月22日项目动态日报。

---

# NanoClaw 项目动态日报 | 2026年6月22日

## 1. 今日速览

今日项目整体活跃度**较高**，主要体现在安全问题的集中披露以及多项修复性PR的持续推进。过去24小时内有**2个**新安全问题被提交，且均未关闭，表明项目进入了一个安全审计期。同时，有**3个**PR被合并/关闭，其中包括一个对容器环境的修复和一个实验性的测试PR，而另外**3个**待合并PR则聚焦于提升系统稳定性和首次用户体验。没有新版本发布，社区焦点从功能新增转向了漏洞修补与健壮性加固。

## 2. 版本发布

无

## 3. 项目进展

今日有 **3 个** PR 被合并或关闭，标志着项目在以下方面取得了进展：

- **容器兼容性修复（#2168）**：由 `kpscheffel` 提交的关于 `fix(container)` 的PR已关闭。该修复解决了在根用户无权限的Docker（rootless Docker）环境中，代理容器无法正确通过 `host.docker.internal` 连接到主机上 OneCLI 服务的问题。这是一个长期存在的、影响特定环境部署稳定性的Bug，其合并解决了企业在非标准容器环境下的部署痛点。
- **首次启动体验优化（#2825）**：由 `amit-shafnir` 撰写的关于 `fix(setup)` 的PR已合并。该修复解决了用户在初次设置时，由于服务启动后套接字（`data/cli.sock`）尚未就绪导致“第一步”对话失败的问题。这直接提升了新用户的首次使用成功率。
- **测试性提交（#2829）**：`fingongr` 提交的标签为 `follows-guidelines` 的PR已被关闭。虽然内容标记为实验性（“eee”），但其关闭表明项目维护者正在清理非功能性或测试性的代码提交。

**整体判断**：项目在修复积压的稳定性Bug（如#2168）上取得了实质性进展，并开始关注用户入门体验的微小但关键的痛点（#2825）。

## 4. 社区热点

今日社区关注焦点集中在**两个未关闭的高危安全漏洞（Issue）** 上，它们均未收到评论，但已引起分析师的高度警觉：

- **#2828 - 符号链接攻击（Symlink Attack）**：该漏洞报告了NanoClaw的A2A（Agent-to-Agent）附件转发功能存在安全缺陷。如果目标Agent被攻击者控制或注入了恶意提示（prompt-injected），它可以将其挂载的 `inbox/` 目录替换成指向主机文件系统的符号链接。当另一个Agent发送文件时，该文件可能会被写入攻击者指定的任意路径，突破会话沙箱。**链接**： [Issue #2828](https://github.com/nanocoai/nanoclaw/issues/2828)
- **#2827 - 审批流程绕过（Approval Smuggling）**：该漏洞指出，`add_mcp_server` 的审批流程存在缺陷。审批卡片仅显示MCP服务器的名字和基本信息，而隐藏了实际的 `args`（参数）和 `env`（环境变量）运行时配置。恶意Agent可以“夹带”危险的参数和环境变量，诱使用户批准一个看似无害的服务，从而绕过安全审查。**链接**： [Issue #2827](https://github.com/nanocoai/nanoclaw/issues/2827)

**背后诉求**：这两个安全问题的核心诉求是**信任边界**与**数据完整性**。开发者YLChen-007正在迫使社区面对Agent间通信（A2A）以及自我修改（Self-modification）流程中存在的严重安全隐患。这反映了随着Agent自主性增强，安全审计必须从代码执行范围深入到数据流向和用户界面欺骗的层面。

## 5. Bug 与稳定性

今日报告的 Bug 全部为**高严重性安全漏洞**，暂无已报告的功能性崩溃或回归问题。

| 严重程度 | 问题编号 | 描述 | 状态 | 是否有Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [#2828](https://github.com/nanocoai/nanoclaw/issues/2828) | A2A附件转发跟随符号链接，可将文件写出到会话根目录外 | **新开（开放）** | 无 |
| **严重** | [#2827](https://github.com/nanocoai/nanoclaw/issues/2827) | `add_mcp_server` 审批流程隐藏运行时参数和环境变量，允许审批夹带 | **新开（开放）** | 无 |

**分析**：这两个Bug均属于设计层面的逻辑漏洞，而非简单的代码错误。修复可能需要引入：
1.  对A2A文件转发路径进行严格的规范化（Resolve）和安全检查，禁止解析出目标根目录之外的路径。
2.  在审批界面上**强制展开**并清晰展示所有运行时参数与环境变量，用户必须确认后才能执行。

## 6. 功能请求与路线图信号

今日无新的功能请求 Issue。但有两个待合并的 PR 提供了潜在的路线图信号：

- **#2826 - 技能更新机制优化**：`Koshkoshinsk` 提交的PR旨在将一个可选的技能更新步骤变为**更具强制性的提示**，并在重新应用配置时重建容器。这暗示了项目计划加强对用户技能版本的管理，以避免用户因疏忽而错过上游的关键修复。
- **#2830 - 死服务自清理**：`amit-shafnir` 提交的PR旨在自动清理那些二进制文件已被删除的“幽灵”服务注册。这指向了项目在**运行时的自我清理和状态一致性**方面的改进意愿，是提升系统鲁棒性的重要信号。

**判断**：短期内，路线图可能优先于**安全修复**和**基础架构健壮性**，而非新功能。这两个PR若能合并，将是方向性的胜利。

## 7. 用户反馈摘要

从 Issues 数据中，我们可以提炼出潜在的用户痛点或场景：

- **安全是首要关切**：报告安全漏洞的开发者（YLChen-007）通过详细的漏洞描述，暗示了其在使用或审计 NanoClaw 的 A2A 和 MCP 管理功能时，发现了严重的信任模型缺陷。这表明有用户正在对项目进行深度的安全测试，可能来自安全社区或需要合规性部署的企业用户。
- **部署环境的异质性**：PR #2168（已合并）的修复表明，社区用户（`kpscheffel`）正在各种Docker配置（尤其是rootless模式）下使用NanoClaw，并遇到了连接问题。这反映出用户部署环境的多样性，项目需要覆盖更广泛的容器化场景。
- **首次体验不佳**：PR #2825（已合并）的修复直接回应了用户“首次聊天”失败的痛点。这是一个典型的“新用户激活”问题，表明早期用户可能在安装后立即遭遇失败，导致挫败感。修复后会显著提升项目的第一印象。

## 8. 待处理积压

需要提醒维护者关注以下长期未响应的重要 Issue 或 PR：

- **#2795 - 新技能提案（已开放5天）**：`leetwito` 提出的“`/add-clidash`” 只读CLI仪表盘技能PR已开放5天，尚无任何评论。这代表了一位外部贡献者的工作，可能因安全问题的集中出现而被忽略。如果该技能符合项目规划，应给予反馈，否则应礼貌关闭以避免贡献者等待。**链接**： [PR #2795](https://github.com/nanocoai/nanoclaw/pull/2795)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的NullClaw项目数据，生成2026年6月22日的项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

过去24小时内，NullClaw项目活跃度处于**较低水平**。社区活动主要集中在单个Bug报告上，未合并任何Pull Request或发布新版本。尽管报告的问题较为严重（高频错误），但项目核心开发节奏放缓，未见明显的代码推进或功能迭代。当前项目健康度**一般**，需关注核心Bug的修复进度及社区维护响应。

- **活跃度评估**: ⭐ (1/5) - 沉寂期

## 2. 版本发布

- **无**。过去24小时内未发布新版本。

## 3. 项目进展

- **无**。过去24小时内没有合并或关闭任何Pull Request，技术栈与代码库无可见更新。

## 4. 社区热点

- **[Bug] error: NoResponseContent (Issue #967) | 热度: 高**
  - **链接**: [Issue #967](https://github.com/nullclaw/nullclaw/issues/967)
  - **分析**: 这是当前唯一活跃的Issue，虽然评论数少，但因其报告的高频核心错误而具有较高关注价值。用户`svier0`遭遇了超过50%概率的`NoResponseContent`错误，直接导致对话无响应。该问题直指模型推理响应的稳定性，是影响用户体验的关键痛点。尽管当前讨论不热烈，但错误本身的严重性可能暗示模型接入层或推理引擎存在普遍性问题。

## 5. Bug 与稳定性

- **严重**: `NoResponseContent` 错误 (Issue #967)
  - **严重程度**: **Critical (严重)**
  - **描述**: 在Windows 11上，使用`v2026.5.29`版本与`Agnes-2.0-Flash`模型交互时，超过50%的概率（21次中出现12次）程序返回`error: NoResponseContent`。用户提及相同模型与API Key在`picocl...`（推测为其他客户端）上工作正常，暗示该问题可能存在于NullClaw客户端特定的请求/响应处理逻辑中。
  - **是否已有修复PR**: 否，尚未关联任何PR。

## 6. 功能请求与路线图信号

- **无**。当前没有新功能请求或讨论。项目当前的首要信号是**修复现有Bug**，而非新增特性。

## 7. 用户反馈摘要

- **核心痛点**:
  - **响应稳定性差**: 用户`svier0`高频遇到的`NoResponseContent`错误是最大痛点。即使使用正常工作的模型和API Key，NullClaw仍会返回空内容，导致应用无法使用。
  - **上下文不清晰**: 用户操作`nullclaw agent -m`后，仅有`info(memory):`的日志输出，随后立即报错。这反映出错误信息不充分，用户难以定位问题（是网络超时、模型参数问题还是客户端内部异常）。
- **用户诉求**: 期望开发团队能排查并修复与模型响应的解析或内部错误处理相关的问题，并提供更详细的错误上下文（如HTTP状态码、超时时间等）。

## 8. 待处理积压

- **[Bug] error: NoResponseContent (Issue #967)**
  - **创建时间**: 2026-06-20
  - **最后更新**: 2026-06-21
  - **链接**: [Issue #967](https://github.com/nullclaw/nullclaw/issues/967)
  - **提醒**: 该Issue自创建后约24小时未有官方回复或进展标记。鉴于其高严重性和复现率，建议项目维护者尽快介入，确认问题、分配负责人，并公开优先级评估。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目 GitHub 数据生成的 2026-06-22 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

今日项目活跃度较高，共处理了 5 个 Issue 和 29 个 PR，显示出核心团队与社区贡献者均保持高频率的沟通与开发迭代。核心方向集中在 **“Reborn”版本的稳定性修复、CI/CD 基础设施优化、以及新功能（如 Workbench 连接器、学习系统、并发执行）的持续集成**。值得关注的是，一个关于 NEAR AI MCP 设置问题的 Bug (##4925) 已被修复关闭，而团队正在通过 Issue #5119 进行为期一周的本地“吃自己的狗粮”活动，系统性地发现和追踪可用性问题。CI 方面，大量 PR 致力于解决缓存、网络重试和任务并行化问题，以提升开发协作体验。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

过去 24 小时内有多个重要 PR 被合并，推动了项目在功能和基础设施上的显著进步：

- **修复：NEAR AI MCP 配置状态误报** (PR #4990, Issue #4925)：已合并。修复了 `nearai.web_search` 虽然可用但仍显示“需要设置”的 UI 错误，改善了用户体验。由 `think-in-universe` 提交。
  - [PR #4990](https://github.com/nearai/ironclaw/pull/4990) | [Issue #4925](https://github.com/nearai/ironclaw/issues/4925)

- **功能：一次性定时触发器** (PR #5065)：已合并。新增 `TriggerSchedule::Once{at}` 变体，支持一次性触发任务，扩展了自动化系统的能力。由 `henrypark133` 提交。
  - [PR #5065](https://github.com/nearai/ironclaw/pull/5065)

- **CI 优化：解决 Rust 缓存回收问题** (PR #5118)：已合并。核心团队解决了因`per-crate`缓存键导致的多缓存争抢、重新下载和构建失败的痛点。新的共享缓存机制将显著提升 CI 效率。
  - [PR #5118](https://github.com/nearai/ironclaw/pull/5118)

- **CI 优化：提取平台兼容性测试** (PR #5113)：已合并。将 64 个 crate 测试矩阵中的跨平台任务分离到独立的 workflow 中，提升了并行能力和测试输出的清晰度。
  - [PR #5113](https://github.com/nearai/ironclaw/pull/5113)

- **CI 优化：为 crates.io 网络故障添加重试** (PR #5115)：已合并。通过设置 `CARGO_NET_RETRY`，增强了 CI 对 crates.io 短暂网络故障的容错能力。
  - [PR #5115](https://github.com/nearai/ironclaw/pull/5115)

- **CI：将 Reborn E2E 测试纳入合并队列** (PR #4830)：已合并。确保了 Reborn 更改在合并前必须通过严格的端到端测试，提升了主分支的稳定性。
  - [PR #4830](https://github.com/nearai/ironclaw/pull/4830)

## 4. 社区热点

虽然今日没有评论数异常高的 Issue/PR，但以下 Issue 反映了社区关注的特定方向：

- **Issue #5119: IronClaw Reborn Local Dogfooding Findings 06/22/2026 - 06/28/2026**：由核心成员 `think-in-universe` 发起的为期一周的内部“吃自己的狗粮”活动。这是一个信号，表明团队正在非常认真地对待 Reborn WebUI 的可用性体验。该 Issue 将作为追踪启动、配置、模型设置等问题的中心，后续会产生大量子 Issue。这反映出社区和开发者对 Reborn 版本顺利落地的高度期待。
  - [Issue #5119](https://github.com/nearai/ironclaw/issues/5119)

## 5. Bug 与稳定性

今日报告的 Bug 数量有限，严重等级较高的问题已被修复。长期存在的 E2E 失败问题依然待解决。

- **已修复：Google OAuth Token 未及时刷新** (Issue #5071, PR #4990? 或相关修复) **[风险: 高]**：已关闭。该 Bug 会导致使用 GSuite 的用户因令牌过期而频繁需要重新认证。核心团队已通过主动刷新 refresh token 的机制解决。具体修复可能包含在后续的特定 PR 中。
  - [Issue #5071](https://github.com/nearai/ironclaw/issues/5071)

- **已修复：NEAR AI MCP 显示错误的“需要设置”状态** (Issue #4925, PR #4990) **[风险: 中]**：已关闭。这是一个直接的 UI/UX Bug，已通过修复状态投影逻辑解决。
  - [Issue #4925](https://github.com/nearai/ironclaw/issues/4925)

- **长期存在：夜间端到端测试失败** (Issue #4108) **[风险: 高]**：自2026-05-27起持续未解决。该 Issue 报告称 Nightly E2E 测试失败，尤其是涉及 Extension 的部分。此问题严重阻碍了自动化质量门禁，需要维护者高度关注和修复。
  - [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

## 6. 功能请求与路线图信号

今日的功能请求与即将落地的功能高度匹配：

- **自动化系统：添加“已完成”摘要卡** (Issue #5117)：用户 `henrypark133` 提出了为自动化页面添加已完成任务的计数卡片。有意思的是，这位用户也是此前提交自动化相关核心功能（PR #5065）的开发者。这表明该功能是经过深思熟虑的，很可能在未来的小版本中实现，以完善自动化管理面板。
  - [Issue #5117](https://github.com/nearai/ironclaw/issues/5117)

## 7. 用户反馈摘要

从 Issue #4925 (NEAR AI MCP 设置问题) 的 1 条评论中可以提炼出以下痛点：

- **用户痛点：** 用户在初步安装和配置后，UI 状态与系统实际可用状态不一致，导致困惑。这说明在用户可见的状态指示方面，Reborn 版本仍有改进空间，团队需要确保“就绪”状态与实际能力对齐。

## 8. 待处理积压

以下 Issue/PR 长期处于开放状态，值得维护者关注：

- **Issue #4108: Nightly E2E failed**：如前所述，该问题已影响主分支稳定性近一个月，是当前最重要的积压待办。
  - [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

- **PR #2927: fix(channels): wire load_startup_active_channels for first-run fallback**：一个规模巨大的 XL 级 PR，已存在近 2 个月。尽管今日有更新，但长期未合并意味着其在处理复杂的通道初始化逻辑。任何在“首次运行”和通道激活方面的 Bug 可能都与它有关。
  - [PR #2927](https://github.com/nearai/ironclaw/pull/2927)

- **Dependabot 批量更新 PRs**：包括 PR #4002, #5116, #4876 等大量由 Dependabot 自动创建的依赖更新 PR。虽然其中一些较新的 PR 已合并，但像 PR #4002 (16个Actions更新) 已存在约一个月仍未合并。此类更新通常风险较低，但长期积压可能带来安全隐患或阻碍其他特性开发。建议核心团队成员定期批量处理。
  - [PR #4002](https://github.com/nearai/ironclaw/pull/4002)
  - [PR #5116](https://github.com/nearai/ironclaw/pull/5116)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据您提供的 LobsterAI GitHub 数据生成的 2026-06-22 项目动态日报。

---

# LobsterAI 项目动态日报 - 2026-06-22

## 1. 今日速览

今日项目整体活跃度**中等**。核心开发活动以**关闭历史遗留 Issue** 为主，24 小时内关闭了 14 个旧 Issue，但未有新的 Pull Request 合并或新版本发布。值得注意的是，社区提交了一个**新的安全相关 Issue (#2181)**，指出项目默认配置存在 SSRF 防护弱化风险，这可能是当前最值得关注的问题。从大量已关闭的旧 Issue 内容来看，项目近期可能经历了一轮集中的 Bug 修复与功能补全，但问题修复后的回归测试和版本发布尚未跟上。

## 2. 版本发布

无

## 3. 项目进展

今日无新的 Pull Request 被合并或关闭。主要进展体现在**关闭了 14 个标记为 `stale` 的旧 Issue**，表明项目维护者正在进行清理工作。这些关闭的 Issue 涵盖了功能请求、Bug 报告和 CI 修复等多个方面，虽然未通过 PR 体现，但反映出项目组正在对历史积压问题进行梳理和决策。

## 4. 社区热点

今日最引人注目的 Issue 是唯一一个**新开的**安全相关 Issue:

- **[Security] LobsterAI restores private-network browser access by default and weakens the bundled OpenClaw SSRF guard [#2181](https://github.com/netease-youdao/LobsterAI/issues/2181)**
  - **作者**: YLChen-007
  - **诉求**: 报告了一个严重的安全问题。Issue 指出 LobsterAI 的浏览器设置层默认启用了 `ProxyCompatible` 模式，并且在没有存储明确策略时，会序列化相关配置，从而**恢复了默认的对内网浏览器的访问权限，并削弱了集成的 OpenClaw SSRF 防护**。
  - **分析**: 这是一个**高优先级**的安全漏洞。SSRF (Server-Side Request Forgery) 防护的弱化可能导致攻击者利用 AI 助手作为代理，访问和攻击内部网络资源。此 Issue 目前没有评论，但应引起维护者的高度重视。

## 5. Bug 与稳定性

今日关闭的 14 个 Issue 中，有大量是此前报告的 Bug，严重程度多为中等，主要涉及功能逻辑和 UI/UX 问题。以下是按严重程度排列的关键 Bug 回顾：

- **严重 - 功能逻辑错误**:
  - **禁用技能后仍被调用 [#1500](https://github.com/netease-youdao/LobsterAI/issues/1500)**: 禁用技能后，其 ID 仍保留在 `activeSkillIds` 中，导致下次对话时继续生效。这是一个典型的“状态不同步” Bug。
  - **Agent 设置面板保存技能列表后不同步 [#1502](https://github.com/netease-youdao/LobsterAI/issues/1502)**: 修改 Agent 技能并保存后，当前会话的 `activeSkillIds` 不更新，需切换 Agent 才能生效。
  - **设置 - IM 机器人必填校验缺失 [#1504](https://github.com/netease-youdao/LobsterAI/issues/1504)**: `popo` 的 AES Key 未做必填校验，空值可保存成功。
  - **定时任务 IM 通知静默失败 [#1506](https://github.com/netease-youdao/LobsterAI/issues/1506)**: 未选择 IM 会话即可提交定时任务，导致通知静默失败。
  - **GitHub Copilot OAuth Token 静默丢失 [#1516](https://github.com/netease-youdao/LobsterAI/issues/1516)**: 关闭 Settings 面板时未取消 OAuth 轮询，认证成功后 Token 会丢失。

- **中等 - 功能缺失/UI 问题**:
  - **QQ Bot 白名单设置缺少添加输入框 [#1512](https://github.com/netease-youdao/LobsterAI/issues/1512)**: 无法通过 UI 配置 QQ 群组白名单。
  - **声明条款内容规范不统一 [#1513](https://github.com/netease-youdao/LobsterAI/issues/1513)**: 条款页面存在序号重复、括号不完整等问题。

- **低严重 - CI/基础设施**:
  - **修复 Labeler 权限错误 [#1518](https://github.com/netease-youdao/LobsterAI/issues/1518)**: 修复了 CI 中的 `label` workflow 权限问题，并补充了 lint 策略。

**目前所有 Bug 均已被关闭，但未见与之关联的修复 PR。这意味着 Bug 可能已被修复，但相关代码还未通过 PR 形式合并到主分支，或者维护者认为此 Bug 在当前版本中已被解决。**

## 6. 功能请求与路线图信号

今日关闭的 14 个 Issue 中，包含了数个用户提出的功能请求，这些请求集中在**提升信息管理效率**上，可能成为下个版本改进的方向：

- **会话颜色标注 [#1525](https://github.com/netease-youdao/LobsterAI/issues/1525)**: 用户期望通过颜色标注区分不同类型会话。
- **批量导出会话 [#1528](https://github.com/netease-youdao/LobsterAI/issues/1528)**: 用户希望在批量模式下能导出选中的多个会话。
- **本地使用统计面板 [#1532](https://github.com/netease-youdao/LobsterAI/issues/1532)**: 用户希望在设置页面查看本地会话和消息的统计数据。
- **消息收藏/书签功能 [#1537](https://github.com/netease-youdao/LobsterAI/issues/1537)**: 用户希望标记和收藏重要的 AI 回复消息。
- **会话标签分类与筛选 [#1541](https://github.com/netease-youdao/LobsterAI/issues/1541)**: 用户希望为会话添加标签以便于组织和管理。

**信号分析**: 这些功能请求高度一致，都指向了“**从基础对话工具向生产力平台进化**”的方向。这表明 LobsterAI 的重度用户（如开发者、研究者）正在产生更深层次的数据管理需求。这些功能被标记为 `stale` 后关闭，值得关注项目组是否会将其纳入 Roadmap。

## 7. 用户反馈摘要

- **正面反馈（间接）**: 用户将 LobsterAI 与 OpenClaw 进行对比（如 Issue #1509: “同样的提示词给到Openclaw里相同的模型，就能很好的理解和生成”），虽然这是一个 Bug 报告，但也侧面说明了用户对模型理解能力有较高期望，且认为 LobsterAI 的基座模型与竞品相比存在能力差距。
- **负面反馈/痛点**:
  - **过程不透明**: Issue #1509 中用户抱怨“技能文件生成”过程“阻塞且无展示”，用户无法感知操作进度，产生焦虑。
  - **状态不同步**: Issue #1500 和 #1502 揭示了界面状态与实际运行状态不同步的问题，导致用户操作后无法获得预期效果，体验割裂。
  - **静默失败**: Issue #1506 和 #1516 中，系统在出错时没有给用户任何反馈（IM 通知不送达、Token 丢失），导致用户对系统可靠性产生怀疑。
  - **功能缺失**: 大量功能请求 Issue (参考章节 6) 反映了用户对会话管理、信息回溯、数据导出等高级功能的迫切需求。

## 8. 待处理积压

- **[高优先级] [Security] LobsterAI restores private-network browser access by default and weakens the bundled OpenClaw SSRF guard [#2181](https://github.com/netease-youdao/LobsterAI/issues/2181)**
  - **状态**: OPEN
  - **无响应时间**: 创建于 2026-06-21，至今 1 天。
  - **提醒**: 这是一个新的、无评论的**严重安全漏洞**。建议项目维护者立即给予回应，评估风险并启动修复流程。这是目前积压问题中风险最高的一个。

- **历史 Bugs 关联缺失**: 今日关闭的 14 个 Issue (如 #1500, #1502 等) 均未标注对应的修复 PR。这可能导致信息断层，提醒维护者，如果在更早的 PR 中已修复这些 Bug，应回补 Issue 关联；如果尚未修复，则不应直接关闭。此问题虽已关闭，但处理逻辑不清晰，积压了潜在的风险。

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 CoPaw GitHub 数据生成的 2026-06-22 项目动态日报。

---

# CoPaw 项目日报 - 2026-06-22

## 今日速览

今日 CoPaw 项目活跃度极高，共处理 18 条 Issues 和 36 条 PRs。社区贡献热情显著，大量 PR 集中在前端移动端适配和 Bug 修复上，但同时也伴随着大量的 Bug 报告，尤其是在新版本 `v1.1.12` 中引入了多个回归问题。项目整体状态为**高活跃、高产出，但稳定性有待加强**。核心团队与社区贡献者正在协同处理消息队列、文件预览、移动端适配等多个关键领域的问题。

## 版本发布
无新版本发布。

## 项目进展

今日合并/关闭的 PR 数量虽不多（4 条），但质量较高，并有多条处于 Review 状态的核心功能 PR 在持续推进。

- **核心稳定性修复**：
    - **PR #5270** ([链接](agentscope-ai/QwenPaw PR #5270))：**已关闭**。合并了包含 64 个测试用例的 Sprint 3 集成测试套件，覆盖 ACP 运行器、插件系统、安全性等关键模块，为项目质量提供了坚实保障。
    - **PR #3831** ([链接](agentscope-ai/QwenPaw PR #3831))：**已关闭**。新增向量模型连接测试功能，完善了模型配置的可用性校验。

- **关键功能推进**：
    - **PR #5321** ([链接](agentscope-ai/QwenPaw PR #5321))：**[Under Review]**。引入名为 “scroll” 的革命性上下文管理策略，使用 SQLite 持久化对话历史，允许模型按需召回过去任意轮次的对话，有望彻底解决上下文窗口限制问题。这是一个重大的功能创新。

- **Bug 修复进展**：
    - **PR #5371** ([链接](agentscope-ai/QwenPaw PR #5371))：**新开**。核心贡献者 `zhaozhuang521` 提交了针对**消息队列串台 (Issue #5354)** 的修复方案，通过在入队时绑定 Agent ID 来解决消息发送混乱问题。
    - **PR #5324** ([链接](agentscope-ai/QwenPaw PR #5324))：**新开**。修复了 `send_file_to_user` 在 `v1.1.12` 后图片不显示的回归 Bug (Issue #5320)，根源在于文件响应头设置不当。
    - **PR #5357** ([链接](agentscope-ai/QwenPaw PR #5357))：**新开**。修复了嵌入式模式下会话切换卡死的 Bug，与 Issue #5354 的部分问题相关。

## 社区热点

今日社区讨论聚焦于升级后的体验问题和消息队列新功能的稳定性。

1.  **Issue #5262** ([链接](agentscope-ai/QwenPaw Issue #5262), 评论: 8)
    - **诉求**：**长期积怨的回归问题**。每次升级后，用户手动禁用的内置技能会重新变为启用，严重影响用户自主权。这已是该用户第二次提交此 Issue，说明开发团队此前未能根除该问题，社区对此表示不满。

2.  **Issue #5329** ([链接](agentscope-ai/QwenPaw Issue #5329), 评论: 5)
    - **诉求**：**移动端交互缺失**。用户通过手机浏览器访问，发现侧边栏进入简洁模式后无法切换 Agent，导致移动端操作基本不可用。此 Issue 直接催生了今日的多条移动端适配 PR。

3.  **Issue #5354** ([链接](agentscope-ai/QwenPaw Issue #5354), 评论: 4)
    - **诉求**：**新功能导致的核心流程崩溃**。新引入的消息队列功能在切换对话/Agent 时导致“串台”和“切不回去”的问题，严重破坏了核心聊天体验。此 Issue 已获得核心贡献者的快速响应（PR #5371）。

## Bug 与稳定性

**高严重度**

- **消息队列串台及会话切换卡死 (Issue #5354, #5358)**：`v1.1.12.post1` 版本的核心回归，严重影响聊天流程。已有对应的修复 PR (#5371, #5357)。
- **文件预览功能退化 (Issue #5320, #5370)**：`send_file_to_user` 工具在升级后发送图片不显示或返回 404，导致 Agent 与用户互动功能受损。已有修复 PR (#5324)。
- **飞书群聊必须 @ 才响应 (Issue #5353)**：`v1.1.12` 中群聊配置失效，无论设置如何都必须 @ 智能体，破坏了正常的自动化工作流。**此 Bug 已被关闭**，但未提及具体修复 PR，需确认其修复方式是否彻底。
- **DeepSeek 模型 Thinking 卡死 (Issue #5328, #5333)**：用户报告在使用 DeepSeek 模型时，Agent 在 Thinking 过程中卡死，需要手动干预。此问题影响主流且受欢迎的模型，对用户信心打击较大。

**中严重度**

- **自定义 OpenAI 兼容 API 不支持 function calling (Issue #5345)**：限制了平台的可扩展性，对于使用非标准 (但兼容 OpenAI API) 服务的用户是个障碍。
- **API `/api/console/chat` 静默丢弃消息 (Issue #5344)**：当 Agent 忙碌时，通过 API 发送的消息会被返回 200 但实际丢弃，这是一种静默失败，对于自动化调用不友好。
- **内置技能升级后重置 (Issue #5262)**：长期问题，严重损害用户对版本升级的信任感。
- **智谱 API 模型级连接测试失败 (Issue #5330)**：供应商级别测试通过但模型级别失败，表明模型路由或名称解析存在逻辑 bug。

## 功能请求与路线图信号

- **移动端适配 (高频请求)**：这是今日最强烈的信号。多条 Issue (#5329, #5360) 和 9 个 PR (#5361, #5362, #5363, #5364, #5366, #5367, #5368, #5369, #5334) 都围绕移动端适配展开。这表明**移动端体验是下一版本必须解决的核心痛点**。
- **稳定性优先于新功能 (Issue #5360)**：社区核心成员明确提出“在添加新功能前，先使核心应用稳定”，这很可能反映了开发团队与部分高级用户的共识。项目的下一步可能进入一个“稳定期”。
- **上下文管理革新 (PR #5321)**：“scroll”上下文管理器 PR 是一个标志性的功能请求，它试图从根本上解决 Agent 长期对话中的上下文遗忘问题。如果通过 Review，将成为项目的重要竞争壁垒。
- **其他明确的功能请求**：
    - **智能体办公室交互增强 (Issue #5327)**：希望在 Agent 管理页面直接发起对话。
    - **模型自动故障转移 (Issue #5351)**：利用已存在的 `routing_chat_model` 实现模型 fallback 机制。
    - **工具结果大小硬限制 (Issue #5342)**：防御性编程，防止上下文爆炸。
    - **记忆搜索的时效性排序 (Issue #5316)**：提升记忆系统的实用性。

## 用户反馈摘要

- **满意与期待**：用户对“消息队列”的引入表示认可（“极大的提高了效率”），认为它是一个不错的进展。同时，社区对移动端适配的呼声极高，今天大量 PR 的提交表明开发者在积极响应。
- **不满与失望**：用户对**版本升级导致核心功能退化**感到非常沮丧。特别是“技能禁用状态丢失”和“图片发送失败”这类非新增功能的回归，严重削弱了用户对版本迭代的信任。多个用户指出，与 DeepSeek 等模型的兼容性问题长期存在，影响了实际使用。

## 待处理积压

- **Issue #5262 ([链接](agentscope-ai/QwenPaw Issue #5262))：技能状态升级重置**。此问题已第二次被提出，是长期存在的用户痛点，**强烈建议**在下一个版本中给予明确修复并增加回归测试。
- **PR #5040 ([链接](agentscope-ai/QwenPaw PR #5040))：`jobs.json` 解析容错**。该 PR 提出时间较长 (2026-06-09)，旨在修复单个任务格式错误导致整个任务系统崩溃的问题。虽然后续 PR (#5347) 提出了另一种迁移式修复方案，但此 PR 代表的“运行时容错”思路可能更优雅。维护者需决策合并方向，以彻底解决 Issue #4835。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 ZeptoClaw (github.com/qhkm/zeptoclaw) GitHub 数据生成的 2026-06-22 项目动态日报。

---

# ZeptoClaw 项目动态日报 - 2026-06-22

## 1. 今日速览

项目今日活跃度正常，社区活动主要集中在代码质量与持续集成（CI）流程的最终优化。过去24小时内，**最后两个关于二进制体积控制门禁（binary size gate）的议题（Issue #537）和拉取请求（PR #611）均已关闭**，标志着该项目在保持“轻量级”核心优势的CI基础设施构建上取得关键性进展。无新版本发布，社区讨论趋于平静，更多是围绕已解决议题的收尾工作。总体来看，项目处于基础设施打磨的“冲刺”尾声阶段。

## 2. 版本发布

无

## 3. 项目进展

今日有1个重要的 PR 被合并/关闭，标志着项目CI流程的里程碑式完成：

- **[PR #611] chore(ci): promote binary-size to PR gate at 7.5MB** (已关闭)
  - **作者**: qhkm
  - **链接**: [PR #611](https://github.com/qhkm/zeptoclaw/pull/611)
  - **内容**: 该 PR 将已存在的“二进制体积检查”步骤正式提升为**所有 PR 的准入检查门禁**。具体改动包括：移除了该检查仅在推送到主分支时运行的`if:`条件判断，并将二进制体积阈值从7MB调整至**7.5MB**。
  - **项目意义**: 此举将“能装进机器人”这一核心设计原则（项目称为“战略护城河”）从人工评估转变为自动化的硬性门槛。**任何 PR 如果导致编译后的 zeptoclaw 可执行文件（脱去调试信息后）超过 7.5MB，将直接被 CI 拦截，无法合并。** 这显著增强了项目应对未来代码膨胀的韧性，是维护项目长期健康度的关键一步。此 PR 的关闭直接关联并最终解决了之前提交的 Issue #537。

## 4. 社区热点

今日无讨论热烈的议题。所有相关议题和PR均已闭环，社区焦点已从讨论“是否要加门禁”转向接受和实施“门禁已就位”的事实。

## 5. Bug 与稳定性

今日无新 Bug 报告。所有活跃议题均属内部优化（chore）类型，不涉及功能缺陷或稳定性回归。

## 6. 功能请求与路线图信号

近期无新功能请求。从已关闭的 Issue #537 和 PR #611 来看，项目短期路线图的重点是**完成核心CI基础设施的构建**，特别是围绕“二进制体积”这一关键指标。这表明项目在功能开发之外，非常注重工程规范和长期可维护性，是项目健康度极高的信号。

## 7. 用户反馈摘要

从 Issue #537 的描述中可以提炼出项目维护者（同时也是主要用户）的核心痛点：
- **痛点**: 担忧每一次代码提交（PR）都会导致“无意识的臃肿”，以零碎的方式侵蚀“6MB”这一战略性体积优势，最终破坏项目在资源受限环境中（如机器人）的定位。
- **诉求**: 需要一个自动化的、在早期（PR阶段）就能介入的防护机制来遏制代码膨胀。

解决方案（PR #611）的落地直接回应了此痛点，预计将获得项目忠实用户的正面评价。

## 8. 待处理积压

无。所有与二进制体积检查相关的积压工作今日已完成。项目维护者的下一步工作重点预计将转向其他待办事项，例如新功能的开发或其他技术债务的清理。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeroClaw 项目数据，我为您生成了 2026年6月22日 的项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-22

## 1. 今日速览

今日 ZeroClaw 项目活跃度处于 **高亢期**，社区贡献与维护者响应均十分积极。过去24小时内，Issue 与 PR 的总计处理量均达到 50 条，且新提交占比高。项目进入 **v0.8.x 系列的密集发布准备阶段**，多个面向 v0.8.2、v0.8.3 里程碑的任务追踪器（Tracker）正在被积极创建与更新，体现了清晰的项目规划。同时，社区对安全增强（SSRF、凭证管理）和核心功能（工具调用、MCP 集成）的回归修复贡献显著，表明项目正从快速功能迭代转入稳定性和安全性强化期。

## 2. 版本发布

过去24小时内无新版本发布。项目正在进行 **v0.8.0** 的稳定版推广（参见 #7112），并已规划好 **v0.8.1**（集成队列 #6970）以及 **v0.8.2**（WASM 插件 #7314、技能平台 #7852）和 **v0.8.3**（多个子追踪器 #8070, #8071, #8072）的详细路线图。

## 3. 项目进展

今日合并/关闭的重要 PR 主要聚焦于修复关键的功能缺陷和推进零代码管理界面的易用性。

- **关键合并/关闭 PR**:
    - **#7912** `fix(whatsapp_storage): store app-state mutation MACs raw, not JSON-wrapped` - **[已合并]** 修复了 WhatsApp 通道的关键配对问题，解决了因数据存储格式错误导致的状态同步失败。这直接移除了一个可能阻碍 WhatsApp 用户部署的阻塞点。
    - **#7857** `fix(zerocode): skip queue-paused hint when backlog is empty` - **[已合并]** 修复了 ZeroCode 管理界面一个易用性问题，避免了在无待处理消息时错误显示“队列暂停”状态，提升了用户体验。
    - **#8089** `[Bug]: Docker and Debian Dockerfile builds fail due to missing aardvark-sys build.rs` - **[已关闭]** 快速解决了 Docker 构建失败的问题，保证了项目的持续集成和部署能力。

- **重要进展**:
    - 随着多个跟踪器（如 #8070, #8071, #8072）的创建，项目维护者 **Audacity88** 明确划分了 v0.8.3 的工作范围，标志着项目正式进入了下一个里程碑的冲刺阶段。
    - 社区成员 **Nillth** 提交了多个关于可观测性（#8065, #8066）和安全架构（#8063）的 PR，尽管尚未合并，但这些高质量的 PR 表明项目在基础架构层面获得了重要的社区贡献。

## 4. 社区热点

- **#6808** `RFC: Work Lanes, Board Automation, and Label Cleanup` (评论: 11)
    - **诉求**: 这是一条关于项目治理和开发流程的 RFC（请求评议）。社区核心贡献者 **Audacity88** 提出的关于如何更高效地组织工作任务、自动化看板管理和清理标签体系的建议。高评论数表明核心团队和贡献者对优化项目协作方式有强烈的兴趣和讨论意愿。

- **#2503** `[Feature]: where is napcat channel` (评论: 9)
    - **诉求**: 用户 **irunmyway** 急切地希望集成 OneBot/NapCat 协议通道。这是社区对扩展项目连接性的直接需求，表明 ZeroClaw 的用户群体渴望连接更多异构的即时通讯/机器人平台。尽管该 Issue 已存在数月，但持续活跃，反映了此需求的紧迫性。

- **#5287** `[Feature]: Local-First Mode for Small Models ...` (评论: 3，👍: 2)
    - **诉求**: 用户 **ThirDecade2020** 强烈号召为小模型/本地模型设计“紧凑模式”，以减少提示词膨胀、防止内部指令泄露。获得高赞和持续讨论表明，社区中有相当一部分用户希望 ZeroClaw 能更好地支持本地、隐私优先、资源受限的运行场景，而不仅仅是追求云端大模型的最强能力。

## 5. Bug 与稳定性

今日报告的 Bug 中，严重程度为 **S1（工作流受阻）** 的问题依然存在，但已有对应的修复 PR 正在审查。

- **S1 - 工作流受阻**
    - **#7756** `[Bug]: native/MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turns` - 一个核心功能问题：MCP 工具在特定模型（如 OpenAI Reasoning 和 Anthropic）上无法使用。影响面广。**（无 fix PR）**
    - **#6361** `[Bug]: context_compression drops assistant(tool_calls) and tool(result) entirely for OpenAI-compatible providers...` - 一个顽固的回归，导致与兼容 OpenAI 接口的供应商（如 MiniMax）进行多轮对话时出现工具循环。标为 `in-progress`。**（开发中）**
    - **#8089** `[Bug]: Docker and Debian Dockerfile builds fail due to missing aardvark-sys build.rs` - 阻断整个构建流程。**（已于 2026-06-21 关闭）**
    - **#4879** `[Bug]: Gemini CLI OAuth is simply not working` - Gemini 提供商认证问题，阻止用户使用该服务。**（无 fix PR）**
    - **#8094** `[Bug]: Anthropic provider added in Quickstart is unavailable in chat until reset` - 影响新用户快速启动体验，被作者标记为 **S0（数据丢失/安全风险）**，虽然描述看起来更像是功能故障而非数据丢失，但需高度关注。**（无 fix PR）**

- **S2 - 性能降级**
    - **#6360** `[Bug]: Prompt Caching does not work with telegram` - 提示缓存功能在 Telegram 通道上失效，导致响应变慢和成本增加。**（无 fix PR）**

- **稳定性与回归修复**
    - **#7836** `fix(channels/orchestrator): use resolved agent config for strict_tool_parsing and parallel_tools` - **[OPEN PR]** 修复了导致通道对话中工具解析和并行工具配置失效的问题，这是 v0.8 系列中一个关键的配置传递回归。
    - **#8079** `fix(channels): add env-based credential fallback for OpenAI STT provider` - **[OPEN PR]** 通过增加环境变量回退，提升了 OpenAI 语音转文字功能的配置灵活性和健壮性。

## 6. 功能请求与路线图信号

新提出的功能请求显示出社区对 **安全性** 和 **外部集成** 的强烈需求，这些信号很可能被纳入后续版本的规划。

- **安全增强（高优先级信号）**:
    - **#6613** `[Feature]: Allow setting, and default to, a much stronger pairing code than 6 numeric digits` - 要求增强配网码强度。这与 #5918（SSRF 保护）、#5919（环境变量访问白名单）等未关闭的安全 Issue 一起，构成了 v0.8.2 WASM 插件计划（#7314）的重要组成部分。
    - **#5918** 和 **#5919** 仍为 Open 状态，并更新于昨日。它们是插件系统的安全基础，预计将在 v0.8.2 中被优先解决。

- **外部集成与可观测性**:
    - **#8072** `[Tracker]: v0.8.3 channels, providers, and config behavior` - 新发布的追踪器明确了将集成的通道和提供商列为 v0.8.3 的工作重点。
    - **#6641** 和 **#6642** 关于 OpenTelemetry (OTel) 追踪的增强（如捕获完整 prompt/completion），由社区成员 **JordanTheJet** 提出并有望被上游化。这表明社区对监控和调试能力有着持续的需求。

- **用户界面与体验**:
    - 多个关于 **ZeroCode** 管理界面的 PR（如 #7999, #8064, #7857）和 **CLI**（如 #7856）的微调和修复，表明项目正在着力打造更友好、更具可操作性的管理工具。这与 v0.8.3 追踪器（#8070）中“operator-facing surfaces”的方向完全一致。

## 7. 用户反馈摘要

从 Issue 和 PR 的评论中可以提炼出以下用户痛点和使用场景：

- **痛点：新手引导与预期不符** (#8094)：“快速启动后，添加的模型在仪表盘显示，但在聊天窗口不可用，直到重置。” - 这表明 `quickstart` 的流程存在缺陷，严重影响了新用户的首次使用体验。
- **痛点：配置“隐形”与缺少反馈** (#2503, #7808 推断)：
    - 用户找不到 NapCat 通道的选项，抱怨“希望增加选项”。
    - 用户使用 CLI 输入密码时完全没有任何视觉反馈，直到按下回车键才知情（#7808 通过 #7856 修复）。这表明项目的配置选项发现和交互反馈需要大幅提升。
- **场景：本地/隐私优先部署** (#5287)：用户明确表达了希望 ZeroClaw 在小型、本地模型上也能良好运行的诉求，并详细规划了如何减少提示词膨胀和防止系统提示泄露。这是一个典型的“企业级”或“高级用户”用例。
- **场景：集成自有工具链** (#2467, #6641, #6642)：用户（**MexHigh, JordanTheJet**）表达了希望将 ZeroClaw 的 Webhook 系统、可观测性数据集成到他们现有的工作流（如自定义消息格式、OpenTelemetry 后端）中。这表明 ZeroClaw 作为 AI 基础设施，正在被整合进更复杂的 DevOps 环境中。

## 8. 待处理积压

以下 Issue 长期未解决且影响较广，需要维护者给予关注或社区协助。

- **#4879** `[Bug]: Gemini CLI OAuth is simply not working`（创建于 2026-03-28，更新于 2026-06-21）
    - **链接**: [Issue #4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879)
    - **影响**: 所有希望使用 Gemini 服务的用户被完全阻塞。严重性 **S1**。已近3个月无修复 PR，考虑到 Gemini 提供商在用户中的流行度，这应被视为高优先级积压。

- **#2503** `[Feature]: where is napcat channel`（创建于 2026-03-02，更新于 2026-06-21）
    - **链接**: [Issue #2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503)
    - **影响**: 长期未得到肯定的路线图回复，导致关注此功能的QQ/OneBot用户社区缺乏明确预期。虽然新开追踪器 #8072 可能包含此通道，但最好能在此 Issue 中给予明确回复。

- **#6074** `audit: track 153 commits lost in bulk revert c3ff635 for recovery`（创建于 2026-04-24，更新于 2026-06-21，状态: `in-progress`）
    - **链接**: [Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)
    - **影响**: 这是项目历史上的一个重大事故，涉及153个提交的丢失。尽管标为 `in-progress`，但却迟迟没有看到实质性的合并进展或承诺恢复的列表。这不仅仅是代码问题，更是对社区贡献感的伤害，需要更透明和积极的沟通。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*