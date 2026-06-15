# OpenClaw 生态日报 2026-06-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-15 02:29 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目的分析师，我为您呈上 OpenClaw 项目 2026-06-15 的每日动态报告。

---

# OpenClaw 项目动态日报 | 2026-06-15

## 1. 今日速览

今日项目活跃度极高，社区反馈与开发者修复进入“白热化”阶段。过去24小时内共有500条Issue和500条PR更新，但**待合并PR高达425条**，修复积压严重，表明维护团队面临严峻的交付压力。**重大故障 (P0/P1)** 仍是社区讨论焦点，特别是 **Gateway 事件循环阻塞**、**会话静默截断** 和 **MCP工具传播失败** 三大高影响力 Bug 引发了大量讨论。好消息是，新版本 `v2026.6.8-beta.1` 已发布，重点增强了 Telegram 和 WhatsApp 渠道的可靠性。总体而言，项目处于 **“高活跃度，高修复需求，高积压”** 的强健状态，但维护瓶颈不容忽视。

## 2. 版本发布

### v2026.6.8-beta.1 - 渠道稳定性与丰富性提升

- **发布链接**: [v2026.6.8-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.1)
- **主要更新**:
    - **Telegram 渠道增强**: 原生支持发送富文本，包括表格、列表和可展开的引用块。后台 CLI 交付方式得到了改进，并且移除了旧的草稿迁移机制，使数据边界更安全。
    - **WhatsApp 渠道增强**: 信道交付更加健壮，不易受网络波动影响。
- **破坏性变更/迁移注意事项**:
    - 由于移除了旧的草稿迁移机制，任何依赖旧草稿架构的自动化脚本或插件可能需要进行适配。
    - Telegram 富文本的引入可能改变部分用户预期的消息格式，建议用户检查并调整相关配置。

## 3. 项目进展

今日共有75个PR被合并或关闭，项目在以下方面取得显著进展：

- **安全性与访问控制**:
    - **[PR #93128]**: 修复了一个安全问题，`ancestor context file walk` 在寻找配置文件时不再遍历用户主目录以上的系统目录，防止了敏感信息泄露。
    - **[PR #93127]**: 修复了 `sessions_yield` 工具在配置中被 `deny` 后仍可被调用的漏洞，确保工具策略严格执行。
- **核心稳定性修复**:
    - **[PR #93077, #92970, #92964]**: 三个PR协同修复了 Gateway 的 `sessions.describe` 接口在处理多Agent场景时返回错误会话数据的问题，确保每个Agent只能访问自己的全局会话。
    - **[PR #92943]**: 解决了 `memory-core` 在外部重索引后，Gateway 使用旧 SQLite 句柄导致状态不一致的 Bug。
- **渠道兼容性**:
    - **[PR #92340]**: 新增了对飞书 (Feishu) 会议邀请事件的处理能力，将其转为会话上下文，增强了企业协作场景的兼容性。
    - **[PR #90330]**: 解决了部分模型（如 ChatGPT Codex）在流式响应时缺少 `content-type` 头导致的传输失败问题。

整体来看，项目在解决高优先级的安全和会话管理问题上迈出了坚实的一步。

## 4. 社区热点

今日讨论最热烈的是**三个“铂金级”Bug**，它们共同指向了会话管理的核心瓶颈：

1.  **[#84903] - Gateway 事件循环阻塞**: 单个Agent的挂起导致整个Gateway瘫痪。用户 `Sylaaaaas` 详细描述了模型调用锁争用导致多用户会话完全停止的现象。**这被认为是项目当前最严重的架构问题**。
    - *链接*: [openclaw/openclaw Issue #84903](https://github.com/openclaw/openclaw/issues/84903)
2.  **[#84516] - Codex 长回复被静默截断**: 用户 `olegchatgpt401-sys` 报告在无头模式下，Agent回复在约1000字符处被无声截断，无任何错误提示。这表明Codex集成存在严重的输出处理缺陷，导致用户丢失信息。
    - *链接*: [openclaw/openclaw Issue #84516](https://github.com/openclaw/openclaw/issues/84516)
3.  **[#85030] - MCP工具无法注入子Agent**: 核心问题在于，通过配置注册的MCP（Model Context Protocol）工具无法被 `sessions_spawn` 创建的会话继承，导致子Agent功能受限。**这直接影响了插件的可扩展性和多Agent工作流的可靠性**。
    - *链接*: [openclaw/openclaw Issue #85030](https://github.com/openclaw/openclaw/issues/85030)

**社区诉求**: 用户希望项目团队优先解决这些 **“断路型”** 问题，特别是 `#84903`（事件循环隔离）和 `#84516`（回复完整性），因为它们严重破坏了产品的可用性和可信度。

## 5. Bug 与稳定性

以下为今日报告的BUG（按严重程度降序排列）：

| 严重程度 | Key | 标题 | 要点 | 是否有 Fix PR? |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | #84882 | memory-core 静默删除记忆文件 | 数据丢失问题。Dreaming流程错误地删除了每日记忆文件。 | 无 |
| **P1** | #84903 | 单Agent挂起阻塞整个Gateway事件循环 | **核心架构问题**。Agent隔离失败，对所有会话产生影响。 | 无 |
| **P1** | #84516 | Codex长回复在1000-1100字符处静默截断 | 数据丢失。模型输出被无声截断，严重影响信息传递。 | 无 |
| **P1** | #85030 | MCP工具无法注入子Agent会话 | 功能缺失。破坏了多Agent工作流和插件扩展机制。 | 无 |
| **P1** | #85103 | 模型回退链在Provider配额耗尽时失效 | 可用性问题。在遭遇API限制时，备选模型无法自动接管。 | 无 |
| **P1** | #85251 | Codex会话在`turn/started`后无响应 | 会话卡死。需等待360秒的卡死恢复机制才能自动恢复。 | 无 |
| **P1** | #85126 | 控制UI创建会话时自动选择了错误的认证配置 | 行为异常。默认配置错误，导致用户无法使用预期模型。 | 无 |
| **P1** | #92460 | 孤立Cron任务完成通知丢失渠道信息 | 监控缺失。Cron任务执行完毕后无法推送通知。 | **[#93110]** (PR已提交, 使用新的传递仓库解决) |

**总结**: 今日BUG主要集中在**会话管理、消息完整性、模型执行和插件扩展**四大领域。P0/P1级别的BUG数量众多，且多为系统级问题，短期内对用户体验有巨大影响。

## 6. 功能请求与路线图信号

- **[#93125] 性能优化**: **`compaction.fallbacks`**。一个高热度PR，提议为模型压缩（Compaction）加入有序的回退链，如 `["gpt-4o-mini", "claude-3-haiku"]`。当主要压缩模型失败时，自动切换，防止会话无限增大。此功能响应了用户对可靠性的核心诉求，**极有可能被纳入下一个版本**。
    - *PR链接*: [openclaw/openclaw PR #93125](https://github.com/openclaw/openclaw/pull/93125)

- **[#92105] 用户体验**: **`memory-wiki 可配置页面组`**。用户 `qiaokuan1992` 提出允许用户自定义 `memory-wiki` 的页面分组、目录和递归扫描方式，以替代当前的硬编码逻辑。这体现出社区对知识管理功能的定制化需求日渐增长。
    - *Issue链接*: [openclaw/openclaw Issue #92105](https://github.com/openclaw/openclaw/issues/92105)

## 7. 用户反馈摘要

从热门Issue的评论中，我们可以提炼出以下真实的用户痛点：

- **对“黑箱”操作的强烈不满**: 关于**回复截断 (`#84516`)** 和**会话静默被杀 (`#84536`)** 的Bug，用户普遍表达了困惑和挫败感。用户宁可看到明确错误，也不愿面对无声的失败。
- **对“升级恐慌”的焦虑**: **DeepSeek Prompt Cache失效 (`#91016`)** 导致用户一小时烧掉6美元。用户对升级后可能出现**意外成本激增**高度敏感，批评升级路径不够平滑，缺乏预警机制。
- **“卡顿和崩溃远比其他问题更致命”**: 尽管社区提出了许多功能请求，但用户在`#84903`、`#85251`等High-severity Bug下的讨论更热烈，说明**系统的流畅性与稳定性是用户最核心的诉求**，远高于对新功能的渴望。

## 8. 待处理积压

以下为长期未响应、但影响重大的待处理项，恳请维护团队优先关注：

- **[#45494] (P1, 2026-03-13)**: **Cron Agent在API持续故障时静默超时**。已积压3个月。当LLM API返回500错误时，Agent作业会耗尽其完整的超时窗口，而不是快速失败。这导致资源被长时间浪费。
    - *链接*: [openclaw/openclaw Issue #45494](https://github.com/openclaw/openclaw/issues/45494)
- **[#77467] (P1, 2026-05-04)**: **MiniMax Portal OAuth Token无法自动刷新**。OAuth认证是接入高级模型的桥梁，此问题导致用户必须每2小时手动重新认证，非常影响体验。
    - *链接*: [openclaw/openclaw Issue #77467](https://github.com/openclaw/openclaw/issues/77467)
- **[#83090] (P1, 2026-05-17)**: **Discord群组回复回归问题**。新版引入的负载错误和循环发送问题，严重影响Discord用户正常使用。
    - *链接*: [openclaw/openclaw Issue #81484](https://github.com/openclaw/openclaw/issues/81484)

---

## 横向生态对比

好的，作为您的资深技术分析师，以下是根据今日各项目动态生成的横向对比分析报告。

---

### 2026-06-15 个人AI助手开源生态横向对比分析报告

**报告日期：** 2026-06-15
**分析师：** 资深技术分析师

#### 1. 生态全景

今日，个人AI助手/自主智能体开源生态呈现出**“高度活跃，冰火两重天”**的态势。一方面，以成为通用平台为目标的**核心项目（如 OpenClaw, ZeroClaw）正面临架构演进与稳定性之间的巨大张力**，社区在享受功能快速迭代的同时，也承受着严重的Bug（如事件循环阻塞、会话截断）带来的信任危机。另一方面，**面向特定场景或有专精领域的项目（如 NanoBot, IronClaw）则展现出更快的Bug修复速度和更清晰的产品演进路线**，社区满意度相对更高。整体来看，生态正从早期的“功能竞赛”阶段，快速过渡到 **“安全、稳定、易用”驱动的质量巩固与精细化发展阶段**。

#### 2. 各项目活跃度对比

| 项目名称 | 活跃状态 | 新 Issues | 新 PRs | 合并PRs | 新版本 | 健康度评估 | 核心动态关键词 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 极高 | ~500条更新 | ~500条更新 | 75 | v2026.6.8-beta.1 | 高活跃，高积压，高风险 | **架构危机** (事件循环阻塞), **安全修复**, 渠道增强 |
| **NanoBot** | 高 | 少量(质量高) | 27 | 27 | 无 | 健康，迭代高效 | **核心重构** (循环依赖), **体验优化** (文档/移动端), **Bug潜伏** |
| **Hermes Agent** | 高 | 50条更新 | 50条更新 | 7 | 无 | 高活跃，安全事件频发 | **安全漏洞** (凭证窃取), **会话污染**, 平台兼容性修复 |
| **PicoClaw** | 中等 | 5 | 8 | 5 | 有 (nightly) | 健康，但存在功能回归 | **功能回归** (web_search), **稳定性修复** (TTS/FS), 新架构探索 |
| **NanoClaw** | 极高 | 7 (含3个Security) | 11 | 5 | 无 | 高活跃，安全警钟 | **安全漏洞集中曝光**, **预算体验修复**, **多提供商架构** |
| **NullClaw** | 低 | 1 | 0 | 0 | 无 | 静默，待关注 | **功能请求** (Azure身份认证) |
| **IronClaw** | 极高 | 38 | 43 | 多个关键PR | 无 | 高活跃，安全债沉重 | **Shell审批绕过** (5个漏洞), **附件功能** (重要突破)，**自举工程** |
| **LobsterAI** | 中等偏低 | 0 | 0 | 1 | 无 | 平稳，但有积压 | **关键Bug修复** (幽灵任务), **功能PR长期搁置** |
| **Moltis** | 低 | 1 | 0 | 0 | 无 | 维护停滞 | Docker修复待合并，新特性待评估 |
| **CoPaw** | 高 | 15 | 9 | 0 | 无 | 高活跃，稳定性退化 | **回归Bug** (Gemini), **桌面体验** (启动慢), **国际化贡献** |
| **ZeroClaw** | 极高 | 42更新 (28关闭) | 50 (47待合并) | 多项 | 无 | 高迭代，功能膨胀 | **核心架构统一**, **体验冲刺** (Quickstart), **海量集成** |

#### 3. OpenClaw 在生态中的定位

- **优势：** OpenClaw 是生态中**功能最全面、设计最复杂、社区规模最大**的项目之一。它的核心参照地位体现在其“全功能通用平台”的野心，支持包括 `sessions_spawn`、`MCP`、`memory-core` 等复杂特性，生态位类似于AI agent界的“Kubernetes”。
- **技术路线差异：** 与NanoBot的轻量、灵活和ZeroClaw的“快速集成”不同，OpenClaw更强调**企业级的架构设计和可扩展性**。这导致其开发周期长，版本升级（如beta版本发布）伴随的破坏性变更和回归Bug也更频繁。
- **社区规模对比：** 从每日Issue/PR更新量（500条）来看，其社区活跃度和规模远超其他项目。然而，高活跃度也伴随着**巨大的维护者压力**。这体现在高达 **425个待合并PR** 上，这是生态中其它项目所没有的严重积压，直接导致了社区对修复响应速度的不满。

#### 4. 共同关注的技术方向

多项目在以下方向同时发力，反映出行业共识：

- **安全与审批模型 (OpenClaw, Hermes Agent, NanoClaw, IronClaw, ZeroClaw):**
    - **具体诉求：** 模型执行的工具、文件访问、shell命令需要更细粒度和更安全的审批机制，防止绕过和权限提升。尤其 `shell` 工具的审批逻辑是当前最薄弱环节（IronClaw 发现多条绕过路径）。
- **MCP (Model Context Protocol) / Provider 扩展性 (OpenClaw, NanoClaw, ZeroClaw):**
    - **具体诉求：** 急需标准化和简化第三方工具、模型提供商的集成方式。OpenClaw的MCP工具无法被子Agent继承、NanoClaw的`add_mcp_server`隐藏参数、ZeroClaw的`allowed_tools`委托Bug，均指向了这方面的痛点。
- **会话管理与长上下文处理 (OpenClaw, CoPaw, Hermes Agent):**
    - **具体诉求：** 解决会话静默截断、模型无响应、上下文压缩导致信息丢失（CoPaw）等问题。用户对“黑箱”操作（如静默截断）极度不满，期望明确的错误提示和可靠的长对话支持。
- **内存与状态管理 (OpenClaw, ZeroClaw, Hermes Agent):**
    - **具体诉求：** 提供更可靠的长期记忆（Dream模式）、状态隔离（会话污染）和数据一致性（幽灵任务）。这是Agent迈向自主化、持续运行的基础。
- **多平台与国际化 (CoPaw, PicoClaw, ZeroClaw, LobsterAI):**
    - **具体诉求：** 支持更多通讯渠道（如Zalo, QQ, Slack）和语言（如越南语），并针对特定平台（Windows, macOS）进行优化。

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能平台，企业级特性 | 高级用户、开发者、寻求一站式方案的团队 | 复杂、可插拔、参考实现，但维护成本高 |
| **NanoBot** | 开发者友好，CLI/WebUI 优先 | 开发者、希望快速集成的个人用户 | 后端架构简洁（Python），API兼容OpenAI，开发效率高 |
| **Hermes Agent** | 多通道，强Agent能力 | 追求Agent原生体验的用户，社区贡献者 | 社区驱动强，迭代快，但近期安全事件多 |
| **PicoClaw** | 轻量，面向特定边缘/嵌入式 | 硬件黑客、嵌入式开发者 | 聚焦轻量级实现，可能是其他项目的减配版或特定场景优化 |
| **NanoClaw** | 安全敏感，全新架构探索 | 对安全有极端要求的开发者 | 聚焦“运营商”抽象和静态许可，安全是第一设计原则 |
| **IronClaw** | AI Native 工程，自举 | 自身团队和追求前沿工作流的团队 | “用AI构建AI”的模式，强调开发者体验和自动化 |
| **ZeroClaw** | 快速集成，生态扩展 | 希望低成本接入大量模型和IOT设备的用户 | “兼容性冲刺”模式，社区贡献集成快，但稳定性挑战大 |
| **CoPaw (QwenPaw)** | 桌面自动化，强关联通义系 | 中国市场和通义模型用户 | 依托通义模型生态，侧重Agent Computer Use功能 |
| **LobsterAI / Moltis / NullClaw** | 特定场景或维护期 | 小众用户或早期测试者 | 项目活跃度低，处于维护或功能沉淀阶段，可作为功能参考 |

#### 6. 社区热度与成熟度

- **快速迭代，功能扩张期 (高活跃，挑战大):**
    - **OpenClaw, ZeroClaw, IronClaw, CoPaw:** 这些项目每日处理大量Issue和PR，版本发布或功能合并频繁，是生态创新的主要来源。但伴随而来的是**安全债、技术债务和稳定性的巨大挑战**，用户面临“功能丰富但不可靠”的窘境。
- **质量巩固，精细打磨期 (高活跃，体验佳):**
    - **NanoBot, PicoClaw:** 这类项目虽然更新量不及第一梯队，但合并率高，Bug修复快，核心开发方向明确，社区反馈积极，用户体验更佳。是希望“开箱即用”的更稳妥选择。
- **低活跃，维护或停滞期:**
    - **LobsterAI, Moltis, NullClaw:** 这些项目社区互动极少，功能更新缓慢，存在大量积压PR/Issue。表明项目可能处于低度维护状态或已经失去开发动力。

#### 7. 值得关注的趋势信号

1.  **安全已成为“生死存亡”的议题：** 今日多个项目（IronClaw, NanoClaw, Hermes Agent）同时爆发了涉及审批绕过、凭证窃取、沙箱逃逸的高危安全漏洞。这明确警示：**AI Agent 的“代理”属性使其安全风险远高于传统应用，设计一个神经质的、不可绕过的审批模型是所有开发者的第一要务。** “功能丰富但充满漏洞”的Agent产品将迅速被社区抛弃。

2.  **“静默失败”是用户体验的毒药：** 无论是会话截断、预算耗尽无响应，还是工具调用缺失，社区普遍反映出对“黑箱”操作的零容忍。**明确的成功/失败信号、清晰的错误信息和优雅的降级逻辑，是维护用户信任的基石。**

3.  **AI 开发正向“自举”演进：** IronClaw 团队提出的“AI Native 工程”路线图是一个强烈信号。**使用AI助手来加速CI/CD、代码审查、测试和版本发布本身，正在从概念走向实践。** 这预示着未来的开源项目将不再仅仅是AI的使用者，更是AI的实践者和加速器。

4.  **“服务集成”成为差异化竞争的核心：** ZeroClaw 一天内为10+个新服务提供集成支持，CoPaw 收到对Zalo的集成请求。在基础Agent能力趋于同质化的今天，**谁能更快速、更简单地集成用户已有的服务生态（云服务、IoT设备、企业工具），谁就能赢得下一阶段的竞争。**

5.  **用户体验下沉，国际化需求浮现：** 从ZeroClaw的“全量Docker镜像”到CoPaw的“越南语支持”，再到各大项目对移动端、CLI易用性的持续优化，都表明项目正从“仅为技术人员打造”转向 **“面向全球更广泛用户群体的普惠化”**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的 NanoBot GitHub 数据生成的 2026-06-15 项目动态日报。

***

# NanoBot 项目动态日报 | 2026-06-15

## 1. 今日速览

今日NanoBot项目状态**高度活跃**，核心团队（`chengyongru`）主导了大量关键性重构与功能完善工作。在过去24小时内，合并/关闭了27个Pull Request（PR），显示出极高的代码迭代效率。社区交互方面，Issues数量不多但质量高，暴露了两个值得关注的Bug。整体来看，项目正处于从功能快速扩张向**稳定性和健壮性**过渡的阶段，同时兼顾了开发者体验优化与WebUI的用户体验打磨。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

过去24小时内，项目在多个关键领域取得了显著进展，共有27个PR被合并或关闭。以下是核心推进方向：

- **核心架构与稳定性的重大重构：**
    - **解决工具配置循环依赖**：`#4314` 通过将共享的Pydantic配置基类迁移到独立的 `config_base` 模块，成功打破了工具配置模式的循环导入问题。这是一个深层次的架构改进，提升了代码的可维护性与可测试性。
    - **配置快速失败**：`#4275` 实现了对于无效配置文件（无法解析、迁移或验证）的快速失败处理，显著提高了部署时的排错效率。
    - **会话作用域修正**：`#4274` 和 `#4299` 分别修正了提示词历史和定时任务（Cron）的会话作用域。前者确保历史记录按会话精准隔离，后者将Cron任务绑定到其发起会话，避免了在统一会话模式下数据错乱，是智能体行为一致性的重要改进。

- **关键功能增强：**
    - **桌面端与WebUI增强**：`#4210` 修复了桌面端重启后的令牌和WebSocket回放问题，并支持了流式回复的桌面通知。
    - **Agent逻辑完善**：`#4269` 确保智能体在耗尽工具迭代次数后，能向用户提供一个更友好的最终状态提示，而不是仅仅显示通用预算耗尽消息。
    - **飞书(Lark)通道优化**：`#4277` 实现了`lark_oapi` SDK的懒加载，优化了飞书通道在网关启动时的性能。

- **文档与用户体验：**
    - **优化新手上路**：`#4177` 对文档入口进行了大规模重写，区分了不同用户路径（无背景搭建、快速CLI、WebUI等），极大地降低了新用户的入门门槛。
    - **WebUI移动端适配**：`#4339` 显著改善了WebUI在移动设备上的显示效果，包括间距、安全区域和布局调整。

## 4. 社区热点

尽管今日社区讨论热度不高，但有两个开放式Issue引起了核心关注：

- **`#4309` [Bug] 零Token使用量问题**：核心API端点 `/v1/chat/completions` 始终返回零Token用量，这对于需要监控成本的用户（如开发者或企业用户）是**一个严重的功能性缺陷**。虽然评论较少，但该问题直接影响NanoBot作为OpenAI兼容服务的可用性和透明度。
- **`#4345` [Bug] 图像剥离回退导致幻觉**：这是一个非常巧妙的Bug。当模型拒绝处理图片时，程序会剥离图片再次请求。但此处没有正确处理上下文，模型可能会**“脑补”**出它从未见过的图片内容，甚至泄露本地文件路径。这暴露了智能体错误恢复逻辑中的一个潜在**安全隐患和幻觉风险**，引发了社区对AI行为鲁棒性的关注。

## 5. Bug 与稳定性

今日报告的Bug数量少但严重程度高，涉及核心功能和智能体行为：

| 严重程度 | Issue # | 问题描述 | 当前状态 | 修复PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | `#4309` | `/v1/chat/completions` 接口返回硬编码的零Token使用量。 | 开放 (2026-06-12) | 暂无 |
| **高** | `#4345` | 图片剥离回退机制导致模型产生“幻觉”，并可能泄露文件路径。 | 开放 (2026-06-15) | 暂无 |
| 低 | `#4333` | `claude-opus-4-8`模型因API废弃参数`temperature`导致请求失败400。 | **已关闭** | (已在同日内修复并合并) |

**分析**： `#4333` 问题已快速解决，体现了团队对高优先级问题的响应速度。而`#4309`和`#4345`已开放多日或今日新开，可能需要维护者优先处理，尤其是`#4345`的幻觉和路径泄露问题，具有潜在风险。

## 6. 功能请求与路线图信号

- **`#4262` [已关闭] 使用 `botIcon`**：请求在Agent模式启动时显示自定义图标，而非默认的“puppy”。虽然已关闭，但这类“小打磨”需求反映了用户对个性化体验的追求。
- **`#4138` [已合并] 文件系统工具的开关**：为内置文件系统工具增加了 `tools.file.enable` 配置开关。这并非用户直接请求，而是开发者主动提供的增强，旨在提升安全性和部署灵活性（例如，只允许通过MCP Server访问文件系统）。
- **WebUI自动化管理视图 (`#4330`)**：这是一个未合并的PR，意图为WebUI增加自动化（Automations）管理界面。这暗示了项目正从“单任务Agent”向“可长期运行的、自动化业务流程执行平台”演进，是路线图上的一个强烈信号。

## 7. 用户反馈摘要

- **痛点与Bug：**
    - **集成客户端的开发受阻** (`#4309`): 用户 `alx1379` 指出，由于Token用量始终返回0，导致任何依赖用量监控的客户端或成本追踪工具都无法正常工作。这对于企业级部署是致命缺陷。
    - **真实的虚假信息风险** (`#4345`): 用户 `BearMett` 发现了严重的功能性安全漏洞：智能体的错误恢复机制可能导致它“凭空捏造”视觉信息，这种“幻觉”对用户是误导性的，且文件路径泄露带来了隐私风险。
- **开发体验：**
    - **对可用性的积极反馈**：通过`#4177`、`#4339`等一系列PR，可以推断新用户对于文档引导和移动端使用体验的改善有潜在需求。

## 8. 待处理积压

- **`#4293` [开放] Agent `pending_queue` 修复**：该PR旨在修复子代理（Subagent）结果注入的逻辑。由于涉及核心Agent循环，代码变更较为复杂，已开放4天尚未合并。该问题对于依赖多Agent协作的复杂任务至关重要，建议维护者优先跟进审查。
- **`#4344` / `#4343` / `#4337` [开放] 核心代码库重构与增强**：包括配置和Agent循环边界重构 (`#4344`)、拒绝未知工具参数 (`#4343`)、忽略空负载 (`#4337`)。这些均为核心代码的改进，建议尽快合并以避免长期分支带来的冲突风险。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

## Hermes Agent 项目动态日报
**日期:** 2026-06-15
**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

### 1. 今日速览

过去24小时内，Hermes Agent 项目社区活动异常活跃，共产生50条 Issue 和50条 PR 更新，显示项目正处于高频迭代期。核心开发者和社区贡献者正集中精力解决一系列关键问题，主要包括：**安全加固**（特别是凭证存储和跨配置泄露）、**核心稳定性修复**（会话污染、消息丢失、超时等问题）以及**用户体验优化**（桌面应用、CLI、Windows 兼容性）。尤其值得注意的是，项目中涌现了多个涉及安全问题的深度报告，表明项目在快速扩张后正进入安全与质量巩固阶段。整体来看，项目健康度良好，社区反馈积极，但需警惕积压的P1/P2级 Bug 对用户基础体验的影响。

### 2. 版本发布

*无*

### 3. 项目进展

今日共有 **7 个 PR 被合并或关闭**，主要集中在系统稳定性和小范围的 Bug 修复上。值得关注的进展包括：

- **用户体验优化:** PR [#24793](https://github.com/NousResearch/hermes-agent/pull/24793) 被合并，将 CLI/配置中 Agent 的默认最大对话轮次（max-turns）从 90 提升至 100，以适应用户日益增长的长对话需求。
- **macOS 兼容性修复 :** PR [#46395](https://github.com/NousResearch/hermes-agent/pull/46395) 被关闭，修复了 macOS 系统下 `write_file` 等工具无法写入 `/tmp` 等临时目录的 Bug，这是对特定平台用户非常友好的修复。
- **配置与部署优化:** PR [#46305](https://github.com/NousResearch/hermes-agent/pull/46305) 和 [#46315](https://github.com/NousResearch/hermes-agent/pull/46315) 致力于提升 systemd 网关服务的稳定性，通过标准化 PATH 变量解决不同环境下服务重启报错的问题。

这些修复表明项目正在积极处理社区反馈的边缘情况和平台兼容性问题，向着更成熟、更稳定的方向迈进。

### 4. 社区热点

今日社区讨论的焦点集中在 **潜在的安全问题**和**核心功能缺陷**上：

1.  **安全问题讨论（评论1）:**
    - **[Issue #46413](https://github.com/NousResearch/hermes-agent/issues/46413):** 报告了 Desktop 的文件预览功能存在安全风险，无法阻止对 Hermes 凭证文件（如 `auth.json`）的读取。
    - **[Issue #46411](https://github.com/NousResearch/hermes-agent/issues/46411):** 指出了 `read_file` 工具存在跨配置文件的凭证窃取漏洞，一个配置文件的 Agent 可以读取另一个配置文件的凭证存储。
    - 这两条 Issue 在短时间内获得关注，虽然评论数不多，但严重性高，直接关系到用户的数据安全，预计将很快引起维护者高度关注。

2.  **功能/体验优化讨论（评论 4-5）:**
    - **[Issue #46192](https://github.com/NousResearch/hermes-agent/issues/46192):** 用户要求为 CLI 中 `base_url` 设置添加“保持（Keep）”选项，避免每次输入都需复制粘贴完整 URL。此需求获得4条评论，反映了用户对配置流程简化的普遍期望。
    - **[Issue #44560](https://github.com/NousResearch/hermes-agent/issues/44560):** 一个影响 WebSocket 连接的P2级 Bug 获得5条评论。该问题导致特定情况下（如配置了响应慢的自定义提供商）界面卡死和超时，是影响桌面/网页应用体验的关键点。

### 5. Bug 与稳定性

今日报告的 Bug 数量较多，按严重程度排列如下：

- **P1 (严重):**
    - **[#46310](https://github.com/NousResearch/hermes-agent/issues/46310):** [Bug]: Matrix 媒体消息发送路径会在每条消息时重新进行完整的 E2EE 初始化，导致激增流量下接收方一次性密钥耗尽并静默丢包。**已有修复 PR [#46407](https://github.com/NousResearch/hermes-agent/pull/46407)。**
    - **[#46303](https://github.com/NousResearch/hermes-agent/issues/46303):** [Bug]: 并发会话（尤其是 Desktop 应用）会污染彼此的内存注入和 Git 工作区，导致会话隔离失效。
    - **[#43083](https://github.com/NousResearch/hermes-agent/issues/43083):** [Bug]: 密码输入被 `***` 替换后，模型在读取历史对话时解析失败，导致第二次工具调用出错。

- **P2 (中等):**
    - **[#46332](https://github.com/NousResearch/hermes-agent/issues/46332):** [Bug]: Windows 平台下，Cron 任务执行 `.sh` 脚本失败，因为系统错误地选择了 WSL bash 或 Git Bash，且路径处理不当。**已有修复 PR [#46364](https://github.com/NousResearch/hermes-agent/pull/46364)。**
    - **[#44560](https://github.com/NousResearch/hermes-agent/issues/44560):** [Bug]: `model.options` 处理程序在做同步 HTTP 调用时阻塞，导致 WebSocket 超时。
    - **[#40480](https://github.com/NousResearch/hermes-agent/issues/40480):** [Bug]: Desktop 应用的下拉菜单中不显示用户手动添加的自定义提供商模型。

- **P3 (轻微):**
    - **[#46131](https://github.com/NousResearch/hermes-agent/issues/46131):** [Bug]: 搭配 Ollama 使用推理模型时返回空内容。
    - **[#46304](https://github.com/NousResearch/hermes-agent/issues/46304):** [Feature]: 希望增加选项隐藏模型切换器中未配置的提供商。

这些 Bug 的快速上报，尤其是P1级问题的出现和**即时修复 PR**的提交，展现了社区贡献者极高的响应速度和项目旺盛的生命力。

### 6. 功能请求与路线图信号

社区提出的功能请求主要集中在提升易用性、平台兼容性和生态集成上。与现有 PR 结合分析，以下功能可能最具落地潜力：

- **Windows 深度集成:** Feature [#46349](https://github.com/NousResearch/hermes-agent/pull/46349) 提议为 Hermes 网关添加原生 Windows 服务后端。考虑到 Windows 用户群体和日益暴露的兼容性问题（如 Issue #46332），此功能极有可能被纳入下一个小版本，以稳固 Windows 平台体验。
- **GBrain 内存集成:** Feature [#46253](https://github.com/NousResearch/hermes-agent/issues/46253) 希望将 GBrain 作为官方内存提供者插件。结合项目近期对内存和插件系统的更新，这类将社区优秀工具标准化集成的请求，很符合项目当前的发展方向，有望被采纳。
- **UI 与配置优化:**
    - **[#46192](https://github.com/NousResearch/hermes-agent/issues/46192) (Keep 选项):** 低风险、高易用性的改进，很可能被快速实现。
    - **[#44757](https://github.com/NousResearch/hermes-agent/issues/44757) (会话合并):** 体现了用户对长任务管理场景的深度需求，是一个有潜力的中等规模功能。

### 7. 用户反馈摘要

从今日的 Issue 和 PR 评论中，我们可以提炼出以下关键用户反馈：

- **正面声音：**
    - **现有功能价值高:** 用户在提交 PR #46352（添加缺失的.env示例）时，表明用户正在主动完善文档和配置，说明他们已经深度使用并认可产品价值。
    - **贡献意愿强:** 多个 Issue（如[#45103](https://github.com/NousResearch/hermes-agent/issues/45103)、[#44140](https://github.com/NousResearch/hermes-agent/issues/44140)）的提交者明确表示“**我愿意自己实现并提交 PR**”，这是社区健康度和项目吸引力的最佳证明。

- **负面反馈 / 痛点：**
    - **安全顾虑:** 用户 wgu9 接连提交两个安全漏洞（#46413, #46411），体现出对凭证和隐私安全的高度不信任与担忧。
    - **性能退化:** [#46090](https://github.com/NousResearch/hermes-agent/issues/46090) 报告“Agent 在基本任务上变得极其缓慢”，表明部分用户可能正遭遇非预期的性能瓶颈（可能由上下文增长或内存泄漏导致）。
    - **平台兼容性困扰:** Windows 用户（#38963, #46332）和 macOS 用户（#46395）均遇到了平台特定的问题，表明跨平台测试和适配仍需加强。

### 8. 待处理积压

以下为一些关键但可能被忽视的 Issue/PR，提醒维护者关注：

- **[#23094](https://github.com/NousResearch/hermes-agent/issues/23094) (关联):** Feature: 使回退（fallback）模型的会话粘滞性可配置。该请求于5月10日提出，作者提供了完整用例，但至今无后续更新。这是一个对精细控制迁移策略用户有价值的功能。
- **[#12020](https://github.com/NousResearch/hermes-agent/issues/12020) (关联):** Feature: 希望增加开关以禁止 API 返回 `hermes.tool.progress` 等内部事件。该问题自4月18日存在，涉及与 OpenAI 兼容接口的互操作性，是一个会影响 API 用户集成体验的痛点。
- **所有 P1 级 Bug（#46310, #46303, #43083）:** 这些 Bug 直接破坏核心功能或服务安全，应作为最高优先级任务处理，特别是 [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) 的会话污染问题，在 Desktop 应用中影响巨大。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-06-15

## 1. 今日速览
昨日项目活跃度较高，共产生 5 条 Issue 和 8 条 PR，其中 5 个 PR 已合并/关闭，1 个新版本（nightly）发布。社区贡献集中在稳定性修复（TTS、文件系统）和结构化日志重构，同时曝出一个关键功能回归（`web_search` 在 `.security.yml` 迁移后静默失效）。整体项目健康度良好，但积压问题（尤其是 Matrix 用户 ID 错误、MCP 解析 bug）仍需关注。

## 2. 版本发布
- **nightly 构建** (`v0.2.9-nightly.20260615.13a38bd1`)  
  自动构建，可能不稳定，建议谨慎使用。  
  🔗 更新日志：https://github.com/sipeed/picoclaw/compare/v0.2.9...main

## 3. 项目进展
今日合并/关闭的 5 个 PR 集中在代码质量与稳定性提升：

| PR | 内容 | 状态 |
|----|------|------|
| #2904 | 修复 agent 循环重载时的 panic 与 goroutine 残留 | ✅ 已关闭 |
| #3121 | OpenAI 兼容层：`log.Printf` → 结构化日志 | ✅ 已合并 |
| #3122 | `appendJSONLRecords` 中捕获文件 `Close()` 错误 | ✅ 已合并 |
| #3123 | 文件系统操作：显式忽略目录 fd 的 `Close()` 错误 | ✅ 已合并 |
| #3124 | TTS 错误路径：处理 `io.ReadAll` 失败时的信息退化 | ✅ 已合并 |

这些修复提升了 I/O 错误处理的严谨性与日志一致性，减少了资源泄漏可能性，属于稳健的 infra 级别改进。

## 4. 社区热点
- **#3041** — `mcp add` 误解析全局标志，导致 http/sse 服务添加失败（评论 1，👍0）  
  用户 `carlosprados` 报告了参数解析 bug，这直接影响 CLI 可编程性与第三方 MCP 集成。虽无大量评论，但属于功能性阻塞问题，值得优先解决。  
  🔗 https://github.com/sipeed/picoclaw/issues/3041

- **#3118** — 添加远程 Pico WebSocket 模式（OPEN，👍0）  
  作者 `jp39` 提交了 agent 的远程控制功能，允许通过 `--remote ws://...` 连接已有进程，这是通往分布式/远程 agent 架构的关键一步，社区关注度可能因使用场景而提升。  
  🔗 https://github.com/sipeed/picoclaw/pull/3118

## 5. Bug 与稳定性
按严重程度排列：

| 严重度 | Issue | 摘要 | Fix PR |
|--------|-------|------|--------|
| 🟥 高 | #3125 | `web_search` 工具在 `.security.yml` 迁移后静默返回空结果 | 无 |
| 🟧 中 | #3044 | `allow_from` 对 Matrix 用户 ID 中包含冒号的情况无效，消息被静默拒绝 | 无 |
| 🟧 中 | #3041 | `mcp add` 误解析 `--no-color` 等全局标志到位置参数，破坏 http/sse 添加 | 无 |
| 🟨 低 | #3090 | Panel 在 iOS < 16.4 的 Safari 上不工作 | 无 |

其中 #3125 是架构升级带来的功能回归，直接影响用户体验，建议紧急定位。其余 bug 虽已 stale 但尚未被修复。

## 6. 功能请求与路线图信号
- **#3120** (OPEN) — 添加 `RegisterChannelSettings` 钩子，支持第三方通道注册，无需 fork 项目。这预示未来可扩展性增强，可能纳入 v0.3 路线图。  
  🔗 https://github.com/sipeed/picoclaw/pull/3120

- **#3118** — 远程 WebSocket agent 模式，若成熟可成为 agent 架构核心能力。  
  🔗 https://github.com/sipeed/picoclaw/pull/3118

- **#2978** (已关闭) — 请求添加 omniroute 作为 provider，但因 stale 关闭。用户希望获得“如何添加自定义 provider”的文档指引，可作为文档改进信号。

## 7. 用户反馈摘要
- **Matrix 用户 ID 兼容性痛点**（#3044）: 标准 Matrix 格式 `@localpart:domain` 在 `allow_from` 中无法工作，用户不得不寻找变通方案或在配置中使用非标准 ID。这反映了对协议标准合规性的期望。
- **MCP 添加失败**（#3041）: 用户 `carlosprados` 提供了完整复现步骤与输出，显示 `--no-color` 被错误当作 MCP 服务名称，属于参数解析 bug，影响多参数场景下的生产力。
- **TTS 错误信息退化**（#3124）: 之前 `io.ReadAll` 错误被丢弃，导致诊断信息丢失，现已修复，用户将获得更清晰的错误反馈。

## 8. 待处理积压
- **#2975** — [stale] 将回复机器人的行为视为 @at 提及（Telegram 群组），创建于 2026-05-30，已近 2 周未更新。  
  🔗 https://github.com/sipeed/picoclaw/pull/2975

- **#3044** — Matrix 用户 ID 冒号兼容性 bug，创建于 2026-06-07，每日有新评论但无 fix PR。  
  🔗 https://github.com/sipeed/picoclaw/issues/3044

- **#3041** — MCP 参数解析 bug，创建于 2026-06-07，影响功能可用性但无进展。  
  🔗 https://github.com/sipeed/picoclaw/issues/3041

- **#3090** — Safari iOS < 16.4 面板兼容性问题，跨平台兼容性缺陷，无修复迹象。  
  🔗 https://github.com/sipeed/picoclaw/issues/3090

---

**项目健康度评分：★★★★☆（4/5）**  
社区贡献活跃，代码质量改进持续，但功能回归和积压 bug（尤其是 Matrix / MCP）需维护者优先调度资源修复。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NanoClaw 项目在 2026-06-15 的 GitHub 数据生成的动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-15

## 1. 今日速览

今日项目活跃度**极高**，尤其是在安全与核心功能改进方面。过去24小时内，社区提交了7个新Issue，其中**3个严重级别的安全漏洞**被集中报告，这需要维护者高度关注。同时，开发侧响应迅速，共发起11个PR，其中5个已成功合并/关闭，包括针对预算耗尽静默丢消息（#2751）的关键修复。尽管无新版本发布，但项目在安全加固、新提供商运营商（Provider Operator）架构以及Codex集成方面取得了实质性进展，显示了项目正在向更健壮、更可扩展的方向演进。

## 2. 版本发布

*N/A - 过去24小时内无新版本发布。*

## 3. 项目进展

今日有 **5 个 PR 被合并或关闭**，标志着项目在以下几个关键方向取得进展：

- **修复核心用户痛点：预算耗尽无响应**：PR #2759 已被合并，该PR解决了 Issue #2751 中报告的“预算用尽时 LLM 回合被静默丢弃”问题。修复后，当预算或 Token 用尽时，用户将**明确收到错误提示**，而不是体验“已读不回”。这对于提升用户体验至关重要。
- **奠定未来架构基石：运营商驱动提供商选择**：PR #2756 已完成合并。这是一个功能合并，引入了运营商驱动的提供商选择、切换和记忆迁移能力。这标志着 NanoClaw 从单一提供商向可插拔、用户可控的多个AI提供商模型迈出了关键一步。
- **基础设施优化：CLI 工具数据化安装**：PR #2758 被合并，将全局 Node CLI 工具的安装方式从硬编码的 Dockerfile 改为数据驱动的 `cli-tools.json` 清单。这会简化容器构建过程，并为未来扩展提供了更清晰的管理方式。
- **文档修复与自动化**：PR #2769 和 #2764 均已关闭。这些针对文档的 PR 修复了 `CLAUDE.md` 中过时的文件路径，并在 `add-codex` 技能文档中补充了交互式认证步骤的说明，旨在减少 AI 编码助手的误导。

## 4. 社区热点

今日最值得关注的热点是**安全漏洞集中报告**。由用户 **YLChen-007** 提交的 3 个安全议题 (Issues) 构成了今日社区讨论的核心，尽管当前评论数为0，但其严重性不言而喻。

- **#2760 [Security] 通过 `send_file` 绝对路径处理任意本地文件泄露** ([链接]())
- **#2761 [Security] 通过未认证的回环 Webhook 绕过本地网关审批** ([链接]())
- **#2762 [Security] `add_mcp_server` 审批流程允许隐藏参数 (`args` 和 `env`) 被批准** ([链接]())

**分析**：
这些议题揭示了项目在安全设计上的三个薄弱环节：
1.  **权限控制**：`send_file` 工具缺乏对文件系统读取范围的有效限制，攻击者可利用绝对路径读取任意文件。
2.  **认证机制**：本地网关的 Webhook 没有验证发送方身份，攻击者可以通过本地回环接口模拟合法事件，绕过审批流程。
3.  **可见性**：MCP 服务器添加流程中，未被显示的 `args` 和 `env` 参数可能被恶意利用，导致用户在不知情的情况下批准了危险操作。

虽然目前没有公开的激烈讨论，但这些问题对于一个旨在成为个人AI助手的项目来说是致命的，社区和维护者间的积极互动与快速响应预计将在未来几天内展开。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **严重 - 安全漏洞**：
    - **#2760**：`send_file` 工具允许任意文件读取。状态：**有安全隐患，待修复**。
    - **#2761**：本地网关审批绕过。状态：**有安全隐患，待修复**。
    - **#2762**：MCP服务器添加流程隐藏参数。状态：**有安全隐患，待修复**。
- **中等 - 功能缺陷**：
    - **#2768**：Claude 提供商未启用提示缓存，导致对话昂贵且低效。状态：**待修复**。
    - **#2767**：Telegram 频道使用了过时的 Markdown 清理器，应适配上游原生 MarkdownV2。状态：**待修复**。
- **低 - 静默错误**：
    - **#2751**：预算用尽时用户收不到回复，相关 PR #2759 已修复此问题。状态：**已修复**。

## 6. 功能请求与路线图信号

结合今日的 PR，项目路线图的清晰信号如下：

- **多提供商架构**：PR #2756（运营商驱动提供商选择）的合并，表明项目正在积极构建一个**插件化的AI后端**。这很可能是下一版本的核心特性。
- **Codex 深度集成**：PR #2757 (Codex v2) 和 #2770 (Codex 文件事件) 展示了项目在集成 **Codex 作为完整AI提供商**方面的雄心，目标是利用 Codex 的洞察能力来增强助手功能。
- **基础设施可维护性**：PR #2758 (CLI工具数据化管理) 的合并，暗示项目团队正在通过**标准化和简化**基础设施来提升开发效率。

这些信号表明，NanoClaw 正从单一的 Claude 绑定转向一个更灵活、可以运行多种「代理-提供商」(agent-provider) 的通用平台。

## 7. 用户反馈摘要

从今日的 Issues 描述中，可以提炼出一些用户痛点：

- **对安全性的关注**：用户 **YLChen-007** 发布了3个安全问题，其角色可能是一个安全研究人员或对该领域有高度敏感性的开发者。其深层诉求是：**个人AI助手必须默认安全**，本地部署不应该意味着放弃安全原则。
- **对AI辅助体验的反馈**：用户 **assapin** 报告的 `#2751` 描述了“AI助手不回复了”的场景，这是一个非常直接的**用户体验痛点**。用户希望系统在有问题时能明确告知，而不是沉默。该用户的反馈直接促成了 #2759 的修复。
- **对上游依赖更新的跟进**：用户 **chiptoe-svg** 指出的 Telegram 清理器问题 `#2767`，表明有一类用户（可能是技能或频道开发者）对**与上游库保持同步和最佳实践**有较高要求。
- **对文档准确性的需求**：用户 **glifocat** 报告了文档中的死链接 `#2763`，并立即贡献修复 PR `#2764`，体现了社区成员对**项目文档的健康度**有较高期望。

## 8. 待处理积压

- **#2732 [OPEN] Harden host + agent-runner from health audit findings** ([链接]())
    - **创建时间**: 4天前 (2026-06-11)
    - **更新时间**: 昨日有更新
    - **分析**：这是一个来自健康审计的结果，涉及 `host` 和 `agent-runner` 的加固，涉及19个文件。虽然功能重要，但与今日新报告的3个高优安全Issue相比，其优先级可能需要重新评估。这可能会与那些新问题产生交叉或冗余，维护者需要评估此PR是否已经解决了部分或全部今日报告的安全问题。
- **#2750 [OPEN] fix: recover stale outbound.db journals after container kills** ([链接]())
    - **创建时间**: 3天前 (2026-06-12)
    - **更新时间**: 昨日有更新
    - **分析**：该PR解决了容器杀死后数据库日志恢复的问题，非常关键。尽管暂时未合并，但其持续获得更新，表明开发者正在积极解决此问题。

---
**总结**：今日是 NanoClaw 项目在**安全性**和**核心体验**上接受全面考验的一天。社区贡献既包含痛苦的漏洞披露，也包含快速的修复 PR。项目响应迅速，对首要的体验问题（预算耗尽无响应）已给出修复。对于安全议题，预计未来48小时内会有紧急的补丁或安全公告。团队在引入重要新功能（多提供商架构、Codex集成）的同时，必须优先解决这些潜在的安全风险，以维持社区对项目的信任。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的NullClaw项目数据生成的2026年6月15日项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-15

## 1. 今日速览

今日项目活跃度处于**较低水平**，主要变动为一条新的功能增强Issue。过去24小时内，项目**无**新版本发布、**无**Pull Request提交或合并，**无**任何Issue被关闭。整体来看，社区贡献和核心开发活动在近24小时内较为沉寂，但新增的Issue表明用户对云服务认证方式的扩展需求正在浮现。

## 2. 版本发布

无。

## 3. 项目进展

**无推进。** 今日未合并或关闭任何Pull Request，项目整体代码库和功能集未向前迈出实质性步伐。

## 4. 社区热点

*   **Issue #955: [enhancement] Identity based authentication support for Azure OpenAI LLM Provider**
    *   **链接**: [nullclaw/nullclaw Issue #955](https://github.com/nullclaw/nullclaw/issues/955)
    *   **热度分析**: 这是今日唯一的活跃议题，尽管暂无评论，但其提出的“基于身份的认证”是一个典型的用户痛点。诉求背后反映了当企业Azure订阅存在安全策略限制（如禁用API Key）时，用户希望利用`az CLI`登录的开发人员凭据（通过`DefaultTokenCredential`）无缝集成Azure OpenAI服务的需求。这不仅是功能请求，也是提升项目在企业级安全环境下的兼容性的关键信号。

## 5. Bug 与稳定性

**无。** 今日未报告任何新的Bug、崩溃或回归问题。

## 6. 功能请求与路线图信号

*   **Issue #955: 身份认证扩展**
    *   **摘要**: 要求为Azure OpenAI LLM Provider增加基于身份的认证支持，使用`DefaultTokenCredential`。
    *   **分析**: 这是一个明确的**路线图信号**。目前NullClaw可能仅支持API Key认证，而该请求直接指向了更现代化、更安全的无密钥认证方式。结合Azure生态的普及度，此功能大概率会被纳入下一个版本的规划中。维护者应认真评估其对Azure Provider模块的开发优先级。

## 7. 用户反馈摘要

*   **用户痛点**: 用户 `kunalk16` 明确指出了在严格安全策略的Azure订阅下使用NullClaw的障碍：API Key可能被禁用。他/她希望项目能适配企业级开发环境的安全习惯（即使用`az login`后的本地凭据）。
*   **使用场景**: 企业内部开发人员使用NullClaw作为AI助手，连接到受管制的Azure OpenAI资源。
*   **满意度**: 未表达对现有功能的不满，更多是希望扩展以适配其特定环境。

## 8. 待处理积压

**无。** 当前未发现长期未响应或无人维护的重要Issue/PR。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 IronClaw (github.com/nearai/ironclaw) 项目数据生成的 2026-06-15 项目动态日报。

---

## IronClaw 项目动态日报 | 2026-06-15

### 1. 今日速览

今日项目活跃度极高，社区驱动迹象明显。过去24小时内，共有 **38 条 Issue** 和 **43 条 PR** 被更新，显示开发与反馈循环非常密集。值得注意的是，**安全相关**的 Issue 报告激增，涉及 `shell` 工具和 `write_file` 函数的多个审批绕过漏洞，这已成为当前社区关注的焦点。虽然当日无新版本发布，但多个大型 PR（如附件功能、Slack 产品适配器）正在推进，为下一版本奠定了基础。**项目健康度评级：高活跃，需重点关注安全债。**

### 2. 版本发布

无

### 3. 项目进展

今日项目在基础设施和核心功能上取得了显著进展，关键合并/关闭的 PR 如下：

- **附件功能 (Attachment) 取得关键进展：** 大型 PR **#4738** 已合并，该 PR 为 Reborn WebChat v2 SPA 实现了附件上传的用户体验。同日，**#4871** 进一步扩展了该功能，为具备视觉能力的模型添加了图片附件支持。这两个 PR 标志着 #4644 提出的“通用附件”路线图取得了决定性进展。
  - [#4738: feat(reborn): attachment web UX on the WebChat v2 SPA](https://github.com/nearai/ironclaw/pull/4738)
  - [#4871: feat(attachments): image attachment support for vision-capable models](https://github.com/nearai/ironclaw/pull/4871)
- **安全与审批流程修复：** PR **#4844** 已合并，修复了 Slack 通道中审批与认证路由过滤的bug，防止了错误的处理逻辑。PR **#4835** 正在进行中，致力于修复跨线程的持久化审批作用域问题，使“始终允许”设置能更好地跨会话生效。
  - [#4844: fix(slack): filter delivered gate routes by raw gate string](https://github.com/nearai/ironclaw/pull/4844)
  - [#4835: fix(approvals): persist "always allow" across threads](https://github.com/nearai/ironclaw/pull/4835)
- **运行时环境优化：** PR **#4836** 已合并，为模型提供了关于当前连接通道、投递目标状态的感知能力，增强了模型对运行上下文的理解。
  - [#4836: feat(runtime-context): surface connected channels, delivery state, and run origin](https://github.com/nearai/ironclaw/pull/4836)

整体而言，项目正向 **Reborn 平台功能完善**（附件、上下文感知）和**安全加固**两个方向稳步迈进。

### 4. 社区热点

今日社区讨论热度最高的是安全相关议题，开发者 `YLChen-007` 集中报告了多个 `shell` 工具审批绕过漏洞，成为绝对焦点：

- **热点分析：** 用户 `YLChen-007` 深入研究了 `shell` 工具的审批分类机制，报告了**5个**独立但相关的安全问题（#4861 - #4865）。核心诉求是：当前基于命令前缀的简单风险分类逻辑存在严重缺陷，可以通过 `env`、`sort --compress-program`、换行符等多种方式绕过，执行 `rm -rf` 等高危命令而无需用户显式确认。这表明社区对项目的**安全模型和信任边界**提出了严峻挑战。
- **链接：**
  - [#4861: Approval Bypass in shell Tool...Newline-Chained Destructive Commands...](https://github.com/nearai/ironclaw/issues/4861)
  - [#4862: IronClaw shell Tool Approval Bypass via GNU sort --compress-program](https://github.com/nearai/ironclaw/issues/4862)
  - [#4863: High-risk shell approval bypass via transparent env/shell wrappers](https://github.com/nearai/ironclaw/issues/4863)
  - [#4864: Shell approval wrapper bypass allows high-risk commands to inherit prior auto-approval](https://github.com/nearai/ironclaw/issues/4864)
  - [#4865: Shell approval boundary bypass via transparent env /bin/sh -c wrapper](https://github.com/nearai/ironclaw/issues/4865)

### 5. Bug 与稳定性

今日报告的 Bug 集中在以下方面，按严重程度排列：

- **严重 (Security) - `shell` 工具审批绕过：** 如上所述，多份报告揭示了高风险的安全漏洞，可能导致恶意代码未经授权执行。**目前暂无专门的 fix PR 链接。**
  - 相关 Issue: #4861, #4862, #4863, #4864, #4865
- **严重 (Security) - `write_file` 沙箱逃逸：** Issue **#4797** 报告了 `write_file` 工具可通过符号链接逃逸沙箱，写入限制目录之外的文件。**该问题仍处于开放状态。**
  - [#4797: write_file sandbox can be escaped through a dangling final symlink](https://github.com/nearai/ironclaw/issues/4797)
- **主要 (功能异常) - Google Calendar OAuth 流程错误：** Issue **#4884** 报告用户在 Reborn 中使用 Google Calendar 扩展时，认证流程导向了错误的 access token 请求，而非引导用户完成标准的 OAuth 流程，导致功能不可用。
  - [#4884: [Reborn] Google Calendar auth prompt requests access token...](https://github.com/nearai/ironclaw/issues/4884)
- **主要 (功能异常) - Reborn Shell 命令审批对话不透明：** Issue **#4852** 指出，用户在审批 shell 命令时，弹窗中仅显示“请求使用 builtin.shell”，而不显示将要执行的具体命令，导致用户无法做出知情决策。
  - [#4852: [Reborn] Shell command is not visible in approval dialog...](https://github.com/nearai/ironclaw/issues/4852)
- **一般 (Web UI) - WebChat v2 在非本地主机 HTTP 下发送失败：** Issue **#4874** 报告了 WebChat v2 SPA 在通过 IP 或主机名访问时，发送消息会报 `Illegal invocation` 错误，影响本地网络测试。
  - [#4874: Bug: WebChat v2 chat send fails with "Illegal invocation"...](https://github.com/nearai/ironclaw/issues/4874)

### 6. 功能请求与路线图信号

今日的功能请求主要来自核心团队，指向明确的产品路线图方向：

- **AI Native 工程效率：** 核心开发者 `think-in-universe` 提出了一个宏大的计划 **#4878**，目标是让 IronClaw 团队自身成为“AI-native”工程团队，使用 IronClaw 自身来加速开发流程。该计划分解出多个子任务，包括：
  - **自动化代码审查** (#4880)
  - **PR Preview 部署** (#4881)
  - **云端编码代理工作流** (#4882)
  - **测试覆盖率追踪** (#4883)
- **信号分析：** 这标志着项目正从“为用户构建 AI 助手”转向“用 AI 助手构建自身”，这是一个非常积极的信号，预示着未来版本将在 CI/CD、代码质量和开发者体验上有巨大飞跃。这些功能很可能会被优先纳入下一版本或作为长期路线图的一部分。

### 7. 用户反馈摘要

从 Issue 评论和报告内容中可以提炼出以下用户痛点：

- **安全感缺失：** 用户对`shell`工具的审批机制极度不信任。报告者 `YLChen-007` 通过详尽的分析证明，当前的审批模型是“表面功夫”，无法提供实质性的安全防护。用户的根本诉求是：**审批系统必须具有神经质的（paranoid）安全性，而不是基于简单的字符串匹配。**
- **配置困惑与误导：** 用户 `sunglow666` 报告了多个 UI 误导性问题，例如在未配置任何 LLM 提供商时，NEAR AI 提供商却被错误地标记为“Active” (#4857)，以及在 Google Calendar 认证时被引导至错误的 token 请求流程 (#4884)。这表明用户期望 UI 状态与实际后端配置严格一致，且认证流程必须有清晰的用户引导。
- **调试信息可见性不足：** Issue **#4852** 反映了用户希望在批准命令前看到完整命令的强烈需求。缺乏足够上下文是影响用户信任和决策的一个重要阻碍点。

### 8. 待处理积压

以下 Issue 和 PR 已存在较长时间且状态未更新，建议维护者优先关注：

- **安全问题积压：** 今日集中报告的 `shell` 审批绕过 (#4861-#4865) 和 `write_file` 沙箱逃逸 (#4797) 应立即提上日程并给予回应或分配修复。安全问题在开源项目中具有最高优先级。
  - [#4861: ...Newline-Chained Destructive Commands...](https://github.com/nearai/ironclaw/issues/4861)
  - [#4797: write_file sandbox can be escaped...](https://github.com/nearai/ironclaw/issues/4797)
- **长期依赖更新 PR：** PR **#3708** (版本发布) 和数个由 `dependabot` 发起的依赖更新 PR (如 #4002, #4499, #4498, #4032) 长期处于开放状态。合并这些 PR 可以减少技术债务，避免因依赖过时而引发的兼容性问题。
  - [#3708: chore: release](https://github.com/nearai/ironclaw/pull/3708)
  - [#4002: build(deps): bump the actions group...](https://github.com/nearai/ironclaw/pull/4002)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 开源项目的分析师，以下是为您生成的 2026年6月15日 项目动态日报。

---

# LobsterAI 项目动态日报 - 2026-06-15

## 1. 今日速览

项目近期活跃度 **中等偏低**。在过去24小时内，Issues 和 PRs 的更新均为对旧条目（原建于4月初）的标记或状态更新 (`[stale]`)，无新提交或新问题。有一项 PR (#1465) 从待合并状态变为已关闭，修复了一个关于定时任务的关键数据残留 Bug。整体来看，项目核心开发活动（尤其是新功能推进）有所放缓，社区反馈与质量修复仍在进行中。

## 2. 版本发布
无

## 3. 项目进展

今日项目取得了一项重要进展：一个针对定时任务系统的 Bug 修复 PR 被合并/关闭。

- **[CLOSED] PR #1465: fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现**
  - **作者**: linlihua
  - **状态**: 已关闭 / 已合并
  - **摘要**: 此 PR 解决了用户反复删除定时任务，但重启应用后幽灵任务依旧出现的问题（关联 Issue #1359）。根本原因是删除流程仅移除了网关侧任务，而本地 SQLite 中关联的会话记录未被清理。修复方案是在删除逻辑中补充了对本地 `cowork_sessions` 表的清理，杜绝了数据残留。
  - **意义**: 此修复提升了定时任务系统的数据一致性与用户操作的可靠性，排除了一个长期困扰用户的稳定性问题。
  - **链接**: [netease-youdao/LobsterAI PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)

## 4. 社区热点

今日无非常活跃的讨论。当前开放的三个功能 PRs (#1429, #1430, #1431) 和两个 UI Issues (#1434, #1435) 均处于长时间未更新状态（自4月初起），未产生新的评论或互动。这反映出社区当前关注度或讨论热情较低。

唯一被合并的 PR (#1465) 是 Bug 修复，但其背后反映的用户痛点（数据残留、幽灵会话）曾是社区关注的热点。

## 5. Bug 与稳定性

今日未报告新的 Bug。项目中仍存在两个已知但未修复的 UI 问题，严重程度较低。

- **[OPEN] Issue #1434: 语言为中文时，搜索无数据显示英文提示**
  - **严重程度**: 低 (UI/UX 展示问题)
  - **摘要**: 当 LobsterAI 语言设置为中文，在 Agent 技能页搜索无结果时，提示文字和按钮仍显示英文，与整体语言设置不一致。
  - **待解决**: 是，长期未更新。
  - **链接**: [netease-youdao/LobsterAI Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)

- **[OPEN] Issue #1435: 创建自定义 Agent 时，名称过长超出弹框**
  - **严重程度**: 低 (UI/UX 体验不佳)
  - **摘要**: 新建自定义 Agent 时，输入过长名称会超出弹框边界，显示不友好。
  - **待解决**: 是，长期未更新。
  - **链接**: [netease-youdao/LobsterAI Issue #1435](https://github.com/netease-youdao/LobsterAI/issues/1435)

## 6. 功能请求与路线图信号

今日无新功能请求。目前项目中有三个功能类 PR 正在等待合并，它们共同构成了 Cowork 功能的体验增强方向，可能指向下一版本的重点：

- **PR #1429**: 会话内消息搜索与高亮 (mark.js)
- **PR #1430**: 会话运行期间阻止系统休眠
- **PR #1431**: 会话运行计时器

这些功能增强了 Cowork 模块的用户体验（搜索、防中断、进度感知）。鉴于它们已存在数月仍未合并，其是否列入近期路线图尚不确定。

## 7. 用户反馈摘要

今日无新增用户反馈评论。从历史 Issues 中可以提炼出的核心用户痛点包括：

- **数据残留问题**（PR #1465 已修复）: 删除定时任务后，重启应用仍能看到已删除任务的“幽灵”记录，导致用户操作无效、困惑且需要反复删除。此问题破坏了对项目管理功能的信任。
- **国际化/本地化不完整**（Issue #1434）: 在中文语言环境下出现英文界面，表明项目的国际化工作存在遗漏或未完全覆盖所有UI场景，影响中文用户的使用流畅性。
- **UI/UX 细节粗糙**（Issue #1435）: 输入框内容溢出弹框，属于基础的 UI 防溢出边界处理问题，反映了对边缘情况的测试和打磨不足。

## 8. 待处理积压

以下三项 PR 和两项 Issue 已积压超过两个月，处于 `[stale]` 状态，可能已被开发者遗忘或搁置。建议维护团队评估其优先级并做出处理决策：

- **[OPEN] [stale] PR #1429**: feat(cowork): 会话内消息搜索与高亮
  - 链接: [netease-youdao/LobsterAI PR #1429](https://github.com/netease-youdao/LobsterAI/pull/1429)
- **[OPEN] [stale] PR #1430**: feat(cowork): 会话运行期间自动阻止系统休眠
  - 链接: [netease-youdao/LobsterAI PR #1430](https://github.com/netease-youdao/LobsterAI/pull/1430)
- **[OPEN] [stale] PR #1431**: feat(cowork): StreamingActivityBar 右侧显示会话运行计时器
  - 链接: [netease-youdao/LobsterAI PR #1431](https://github.com/netease-youdao/LobsterAI/pull/1431)
- **[OPEN] [stale] Issue #1434**: 中文环境下提示英文问题
  - 链接: [netease-youdao/LobsterAI Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)
- **[OPEN] [stale] Issue #1435**: 新建自定义Agent名称过长UI溢出
  - 链接: [netease-youdao/LobsterAI Issue #1435](https://github.com/netease-youdao/LobsterAI/issues/1435)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 (2026-06-15)

## 1. 今日速览
- **总体状态**：项目处于平稳维护期，24小时内无新版本发布，无PR合并/关闭。
- **活跃度评估**：中等偏低。1个新Issue提交，2个待合并PR（含1个自动化依赖更新，1个Dockerfile修复），无重大功能合并或社区热烈讨论。
- **关键信号**：新提交的Feature Request (#1123) 提出了引入纯Rust内存后端以优化边缘压缩，若实现将提升极端场景下的性能与资源效率。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日无任何PR被合并或关闭，项目进展停滞。两个待合并PR（#1122, #1121）尚未获得审查或合并操作，项目整体推进速度暂缓。

## 4. 社区热点
今日无产生评论或点赞的Issues/PRs，社区讨论活跃度极低。未发现用户间互动或技术讨论。

## 5. Bug 与稳定性
今日无新Bug报告。PR #1122 (`fix: drop VOLUME declarations that shadow the home bind mount`) 针对Dockerfile中`VOLUME`声明与宿主绑定挂载冲突的病理级问题提供了修复。该修复虽未标记为Bug，但解决了可能导致部署不可预期的配置问题，建议维护者优先处理该PR以确保容器部署稳定性。

## 6. 功能请求与路线图信号
- **新功能请求**：Issue [#1123](https://github.com/moltis-org/moltis/issues/1123) 提议将纯Rust实现的`turbovec`作为替代内存后端，用于极端边缘压缩场景。该需求预设项目未来需支持更高效的内存管理或边缘设备，但对路线图影响待定。
- **路线图判断**：当前所有功能请求均处于“已提交未讨论”状态，暂无明确规划信号。

## 7. 用户反馈摘要
今日无用户就Issues/PRs发表评论或提出疑问，无法提炼用户痛点或满意度信息。

## 8. 待处理积压
- **PR #1122**（Dockerfile修复）：未合并，建议维护者尽快审查以避免容器部署风险。
- **PR #1121**（依赖更新）：自动依赖更新（esbuild 0.25.12 → 0.28.1），虽非破坏性变更，但长期未合并可能引入安全或兼容性风险。
- **Issue #1123**（新功能请求）：已提交1天，尚无维护者回复，若项目有碎片化路线图管理，建议明确优先级。

> 项目今日健康度中等，维护响应速度略低于预期。建议优先处理PR #1122以消除部署隐患，并对新功能请求给予初步反馈以保持社区活跃度。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 CoPaw (QwenPaw) 项目数据，我为您生成了以下项目动态日报。

---

# CoPaw (QwenPaw) 项目日报 | 2026-06-15

**项目地址:** [github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)

## 1. 今日速览

项目在过去24小时内保持了**高活跃度**。社区提交了15个新Issue和9个待合并的PR，主要集中在功能增强、Bug反馈和桌面端体验优化上。尽管没有新版本发布，但多个“首次贡献者”提交的修复补丁显示了社区的健康成长。当前项目已进入**v1.1.11.post2**阶段，社区反馈存在一些回归性问题，例如Gemini工具调用失败和本地模型提供商显示异常，需要维护团队重点关注。同时，对国际化（越南语）和多平台适配（Zalo、Wayland）的呼声较高。

## 2. 版本发布

**无。** 过去24小时内未有新版本发布。

## 3. 项目进展

今日未合并任何PR，但有多条重要的待合并PR，展示了项目在多个方向的进展：

- **Windows桌面自动化：** PR #5187 提交了一项新功能，使用 UIA (UI Automation) 方式为 Windows 端实现了桌面GUI自动化。Agent 可以像人类一样截图、点击、输入，并结合 Tauri 的控制模式让用户实时看到操作过程。这是一个重要的里程碑，标志着项目在 Agent 计算机使用 (Computer Use) 能力上的突破。
  - 链接: [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)

- **国际化与社区建设：** 有3个来自首次贡献者的PR (#5186, #5175, #5176, #5178, #5179, #5180) 被提交，涵盖了越南语界面支持、会话过滤功能、以及定时任务/心跳机制的修复。这表明项目收到了来自更广泛地区的贡献，社区正在形成。
  - 越南语支持 PR: [#5186](https://github.com/agentscope-ai/QwenPaw/pull/5186), [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175)
  - 会话过滤功能: [#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178)

- **请求负载可扩展性：** PR #5188 为前端 SDK 添加了 `requestPayload transforms` 功能，允许插件在发送请求前修改请求体，提升了架构的可扩展性。
  - 链接: [#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188)

- **定时任务修复：** PR #5180 针对社区报告的定时任务超时和无自主上下文的问题提出了修复方案，通过增加超时时间和添加自主上下文提示来提升任务执行的稳定性。
  - 链接: [#5180](https://github.com/agentscope-ai/QwenPaw/pull/5180)

## 4. 社区热点

**#5156: 建议支持 kimi-for-coding / 加入 uv 白名单**
- **链接:** [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)
- **热度:** 5条评论
- **分析:** 此Issue是今日社区讨论的焦点。用户付费订阅了Kimi的“Coding”套餐，但因QwenPaw仅支持官方Kimi API，导致套餐能力无法使用，产生了“付费但无法集成”的痛点。用户强烈希望项目能在“uv”白名单中加入对Kimi特殊接入方式的支持。这反映了用户对于**将已有付费服务无缝对接到自建AI助手**的强烈需求，以及对官方API限制的无奈。

**#5161: 长对话后 QwenPaw 无响应**
- **链接:** [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161)
- **热度:** 3条评论 (含作者更新)
- **分析:** 这是一个影响核心体验的严重问题。当对话轮次多、上下文变长时，客户端会卡死并停止响应。这很可能是上下文窗口管理或内存泄漏导致的，是用户在实际使用高频场景下最直接的负面反馈。

## 5. Bug 与稳定性

以下 Bug 按严重程度排列：

- **严重: Gemini 工具调用回归 (Issue #5163)**
  - **描述:** 从 v1.1.10 升级到v1.1.11.post2后，Gemini模型的工具调用功能失效。这是一个典型的版本回归问题，表明最新的代码修改可能破坏了与Gemini模型的兼容性。
  - **状态:** 待处理，无关联修复PR。
  - **链接:** [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163)

- **严重: 上下文压缩导致信息完全丢失 (Issue #5171)**
  - **描述:** 当Agent的人设文件token数超过保留阈值时，上下文压缩机制会将所有内容（包括人设文件）清除，导致Agent“失忆”，任务中断。这是一个逻辑缺陷，而非性能问题，会严重破坏Agent的长期协作能力。
  - **状态:** 待处理，无关联修复PR。
  - **链接:** [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)

- **中等: Tauri桌面端启动极慢 (Issue #5047)**
  - **描述:** 用户反馈从Python打包切换到Tauri后，Windows桌面端启动时间从1-2分钟暴增至十几分钟，且有多次无响应现象。此问题已存在数日，对Windows用户影响极大。
  - **状态:** 持续未解决，维护者应优先排查。
  - **链接:** [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047)

- **中等: 钉钉频道会话未注册到前端 (Issue #5177)**
  - **描述:** 通过钉钉Channel发送消息后，Agent能正常回复，但前端Console的会话列表中看不到该对话。这是多渠道消息同步的Bug，会导致用户无法在统一UI界面上管理外部渠道的对话。
  - **状态:** 待处理，无关联修复PR。
  - **链接:** [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177)

- **低: 宠物功能在Wayland下异常 (Issue #5183) & 安装包白屏 (Issue #5165) & 插件安装弹窗 (Issue #5181)**
  - **状态:** 均为特定场景或系统环境下的Bug，已报告待处理。
  - **链接:** [#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183), [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165), [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)

## 6. 功能请求与路线图信号

- **信号强 (已有相关PR):** 
  - **Agent上下文时间戳 (Issue #5185):** 用户要求在Agent上下文中注入实时时间戳（HH:MM:SS），而非仅有日期。此功能对依赖时间的Agent任务至关重要，且用户希望避免额外调用工具的开销。此功能实现相对简单，有望被快速采纳。
  - **定时/心跳任务优化 (PR #5180):** 社区贡献者已提交修复，直接对应 Issue #5174 中报告的定时任务/心跳机制缺陷。这表明该功能会在近期被修复。
  - **越南语 (PR #5186, #5175):** 两个越南语翻译PR已被提交，表明项目正在吸引东南亚地区的用户和贡献者，国际化是明确的社区需求。

- **信号中 (需求明确，待评估):**
  - **Kimi for Coding 集成 (Issue #5156):** 反映了用户对“付费增值服务”集成的渴望，是一个极具商业价值和用户黏性的需求。
  - **飞书流式卡片优化 (Issue #5167):** 用户对长回复场景下的流式刷新体验提出批评，这是一个优化问题，需求明确。
  - **统一模型配置 (Issue #5182):** 建议将文本、图像、视频模型的配置统一化，降低用户使用门槛。

- **信号弱 (新需求，待观察):**
  - **Zalo Bot 支持 (Issue #5168):** 来自越南用户的请求，希望集成越南最流行的通讯应用Zalo。结合越南语PR，项目在东南亚市场的潜力正在显现。

## 7. 用户反馈摘要

- **正面反馈:**
  - 用户对飞书流式卡片的打通表示感谢，认为“终于把这条路打通了”。
  - 多位“首次贡献者”积极提交代码，说明项目文档和社区氛围较好，能吸引外部开发者。

- **负面反馈与痛点:**
  - **“付费却用不了”:** 用户已订阅Kimi coding套餐，但因项目不支持而无法接入，体验到“付费的难受”。
  - **“体验降级”:** Tauri桌面端启动从“一两分钟变成十几分钟”，属于严重的体验降级。
  - **“核心功能失效”:** 长对话无响应 (Issue #5161)、上下文压缩导致失忆 (Issue #5171) 直接导致任务无法完成，是用户最不满意的部分。
  - **“回归Bug”:** 升级后Gemini工具调用功能失效，让用户对项目版本稳定性产生担忧。
  - **“频繁弹窗”:** 插件依赖安装失败导致的死循环弹窗，对桌面用户造成干扰。

## 8. 待处理积压

- **Issue #5047: Windows Tauri 桌面端启动特别慢**
  - **创建于:** 2026-06-09
  - **严重性:** 高 (严重影响用户体验)
  - **最后更新:** 2026-06-15 (今日有更新，但仍未解决)
  - **链接:** [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047)

- **Issue #5163: Gemini工具调用回归**
  - **创建于:** 2026-06-12
  - **严重性:** 高 (导致主流模型功能失效)
  - **状态:** 未分配，无关联PR，维护者需尽快定位复现。
  - **链接:** [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163)

- **Issue #5171: 上下文压缩导致信息丢失 (严重 Bug)**
  - **创建于:** 2026-06-13
  - **严重性:** 高 (导致Agent失忆，任务中断)
  - **状态:** 逻辑缺陷，需设计评审。
  - **链接:** [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于ZeroClaw项目2026年6月15日数据生成的每日项目动态日报。

---

## ZeroClaw 项目动态日报 | 2026-06-15

### 1. 今日速览

ZeroClaw 项目今日活跃度极高，核心开发与社区贡献双线并行。过去24小时内，社区提交了50个PR，其中大部分（47个）处于待合并状态，表明团队正在处理大量的变更；同时有42个Issue被更新，其中28个已关闭，显示出高效的跟进速度。项目正从多个“Compatibility Sprint”中整合成果，今天的主要焦点是修复 Bug、完善配置体验以及实现之前 RFC 中的设计。尽管没有新版本发布，但大量代码正在排队等待进入主分支，项目健康度良好，处于功能快速迭代期。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日项目推进显著，多项关键修复和功能已合并或取得重大进展：

- **核心架构统一**：RFC #7415（统一三种代理回合引擎）已被关闭，其通过一个合并PR (#7540) 成功执行，消除了 `run_tool_call_loop`、`turn_streamed` 和 `Agent::turn` 之间的重复逻辑。这是一个重要的内部重构，为后续开发提供了更稳定的基础。
- **配置与开发者体验 (DX) 增强**：
    - **PR #7594**（已合并）：实现了类型驱动的配置别名选择器，消除了大量的硬编码路径。这一内部变更简化了配置框架，为未来添加新配置项铺平了道路。
    - **PR #7614、#7612**：修复了安装脚本对musl libc的检测，并同步了中文 (zh-CN) 的本地化文件，提升了非英语用户和特定环境的部署体验。
    - **PR #7637**、**#7609**、**#7610**：改进了 Quickstart 流程，包括自动规范化 agent 别名、实时校验输入以及在 channel 设置中提示 webhook 端口，降低了新用户的入门门槛。
- **功能落地**：PR #7666 和已合并的 PR #7384，为计划任务（Cron Jobs）增加了通过 HTTP API（即Dashboard）进行暂停/恢复（Pause/Resume）的功能，补全了任务管理的关键一环。
- **社区贡献集成**：多个由社区贡献者（如 `theonlyhennygod`）提出的功能请求 Issue 被关闭，这些 Issue 涉及添加 Arcee AI、Inception Labs、Lambda AI、Featherless AI、Upstage Solar 等新模型供应商，以及 Sonos、Shazam、Spotify、Philips Hue、8Sleep 等智能设备/服务集成。这表明 ZeroClaw 的插件/集成生态正在快速扩展。

### 4. 社区热点

今日社区最关注的议题集中在**安全性策略**和**功能缺失**两个方面：

1.  **[Hot] 安全与委托模式 Bug (#7470)**：`[Bug]: delegate agentic mode rejects empty risk_profile.allowed_tools...` 是一个严重级别为 S1（工作流阻塞）的 Bug。它暴露了委托（Delegate）模式下两个耦合的行为问题：当目标 Agent 的 `allowed_tools` 为空时，委托会被拒绝；以及配置了不兼容的 `risk_profile` 导致更严格的委托目标也无法执行。该 Issue 有 7 条评论，并被标记为 p1 和 `status:in-progress`，同时已有相关的文档补丁 PR #7592 被提交，表明团队正在积极解决此问题。
    - 链接：zeroclaw-labs/zeroclaw Issue #7470

2.  **[Hot] 用户呼声最高的功能需求 (#3642)**：`[Feature]: Provide a "full" docker image`。这是一个有13条评论的已关闭Issue。用户要求提供一个包含“所有”功能标志（如WhatsApp）的 Docker 镜像，以降低非技术用户的使用门槛。该Issue虽然已关闭，但背后反映的“易用性”诉求是社区的核心关注点。
    - 链接：zeroclaw-labs/zeroclaw Issue #3642

3.  **批量回滚的审计追踪 (#6074)**：`audit: track 153 commits lost in bulk revert...`。该项目仍在追踪一次历史回滚事件，该事件丢失了153个已审查和合并的提交。虽有2条评论，但状态为 `status:in-progress`，表明维护者们对代码历史的完整性非常负责。
    - 链接：zeroclaw-labs/zeroclaw Issue #6074

### 5. Bug 与稳定性

今日报告了多个Bug，按严重程度排列如下：

- **S1 - 工作流阻塞**:
    - **#7470**: 委托模式中的 `allowed_tools` 拒绝问题。**已有修复 PR** (相关文档修复 #7592) 和主 bug fix (推测在 `#7608 / #7640` 或相关PR中)。
        - 链接：zeroclaw-labs/zeroclaw Issue #7470
- **S2 - 行为降级**:
    - **#6856**: 在 channel (模式v3) 响应中，`show_tool_calls` 选项缺失。**状态：进行中**。这表明配置选项在不同版本间的迁移存在遗漏。
        - 链接：zeroclaw-labs/zeroclaw Issue #6856
- **其他重要Bug**:
    - **#7617 (PR)**: 修复了在配置中写错TOML层级（如 `[providers.models.zai.default.default]`）导致所有提供者配置被静默丢弃的问题。此修复通过抛出警告来防止用户踩坑。
        - 链接：zeroclaw-labs/zeroclaw PR #7617
    - **#7616 (PR)**: 修复了当使用 Groq 提供商时，因为其不兼容 `reasoning_content` 字段文本而导致处理失败的问题。
        - 链接：zeroclaw-labs/zeroclaw PR #7616
    - **#7640 (PR)**: 修复了在委托时，OAuth 供应商的凭据会错误地回退到主 Agent 全局凭据的问题，这可能导致 API 密钥不匹配。
        - 链接：zeroclaw-labs/zeroclaw PR #7640
    - **#5892 (PR)**: 这是一个大型的、悬而未决的 PR，修复了两个生产环境阻塞问题：`tool_choice` 被错误地设为空，以及产生孤立的 `tool_use` 响应。
        - 链接：zeroclaw-labs/zeroclaw PR #5892

### 6. 功能请求与路线图信号

从今日的 Issues 和 PRs 来看，以下方向是未来版本的重点：

- **极高的集成/提供商扩展性**：社区贡献者 `theonlyhennygod` 在一天内提交了关于 10 个以上新提供商和智能家居工具的 Issue，并且均已关闭（通常意味着有 PR 对接）。这强烈表明项目正采纳一波“兼容性冲刺”，快速拓展生态系统。
- **安全性/隔离性**：RFC #6293（通过 Unix Socket 实现气隙执行模式）持续受到关注。这是一个高风险、高级别的功能，旨在将 ZeroClaw 拆分为离线和在线进程，以实现类似飞地（enclave）的安全模型。这可能是 `v0.80` 或更后版本的核心安全特性。
- **易用性优化**：`full docker image` (#3642)、`Nix flake` 改进 (#6906)、Docker 文档更新 (#6760) 和 Quickstart 的一系列改进，都指向了降低用户部署和使用难度的明确信号。
- **核心 Agent 功能**：PR #6693 (`feat(memory): add dream mode`) 是一项极大型的未合并 PR，它为内建了周期性的记忆整合功能。虽然目前被标记为需要作者行动，但一旦合并，将显著增强 Agent 的长期记忆能力。

### 7. 用户反馈摘要

- **正面反馈**：用户 `MushiTheMoshi` 在 Bug 报告 #6847 中表达了对项目的赞赏：“First of all thanks for all the hardwork done here. Greatly appreciated. Best tool out there. Wishing way more stars.” 这表明核心产品在社区中认可度很高。
- **核心痛点**：
    - **易用性门槛**：Issue #3642 提出的“full docker image”问题，以及 Docker 文档的更新需求（#6760），反映了非技术用户和开发者在使用时的挫败感。即使功能强大，繁琐的配置也在阻碍用户。
    - **配置陷阱**：多个 Bug（如 #7617、#6856）暴露了 TOML 配置的静默失败问题，用户容易因为写错层级或漏掉字段而遭遇意想不到的行为。
    - **渠道集成问题**：WhatsApp ( #6847 ) 和 QQ ( #5662 ) 渠道都报告了严重的问题（无法显示QR码、语音消息重复处理），影响了关键通信渠道的可用性。

### 8. 待处理积压

以下是最需要注意的关键待办事项：

1.  **生产环境阻塞性 Bug (PR #5892)**：修复 `tool_choice` 和 `orphaned tool_use` 的 PR。虽然创建了一个多月，但状态为 `needs-author-action`，这阻碍了多个依赖该行为的提供商的稳定运行。
    - 链接：zeroclaw-labs/zeroclaw PR #5892

2.  **大型功能 PR 等待开发者激活**：
    - **Dream Mode (#6693)**：一个极大型 (`size: XL`) 的记忆功能增强，目前需要作者回应 (`needs-author-action`)。
    - **MCP/插件路径对齐 (#7549)**：修复 CLI 安装的插件路径与运行时扫描路径不匹配的问题。
        - 链接：zeroclaw-labs/zeroclaw PR #6693
        - 链接：zeroclaw-labs/zeroclaw PR #7549

3.  **待解决的高风险 RFC**：**空气间隙执行模式 (#6293)**。这是一个重要的安全架构变更，目前状态为 `status:blocked`（或 `needs-maintainer-review`），可能需要维护者决定其具体实现路径。
    - 链接：zeroclaw-labs/zeroclaw Issue #6293

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*