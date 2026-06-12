# OpenClaw 生态日报 2026-06-12

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-12 02:10 UTC

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

好的，这是为您生成的 OpenClaw 项目2026年6月12日动态日报。

---

# OpenClaw 项目动态日报 – 2026-06-12

## 1. 今日速览

今日项目活跃度极高，共处理 **500 条 Issues** 和 **500 条 PRs**，显示出社区巨大的参与热情。然而，近 **78%** 的 PR 仍处于待合并状态，**95%** 的活跃 Issues 处于开放状态，表明项目维护团队的合并和响应速度面临挑战。虽然今日无新版本发布，但大量针对关键Bug（如会话状态混乱、信号守护进程竞态条件、系统提示词注入问题）的修复PR已被提交，以及围绕安全矩阵、子代理工具权限和分层上下文加载等重大功能提案正在推进，项目核心架构正在经历深度打磨。社区关注点集中在安全、稳定性、多平台支持和自动化编排上。

## 2. 版本发布

无

## 3. 项目进展

今日暂无已合并的 PR 完全关闭。但从提交的 PR 来看，项目在以下关键领域取得了显著进展：
- **多 Agent 与编排：** 新增了 `toolsAllow` 参数以限制子代理的工具使用范围 (PR #78441)，并暴露了嵌入式运行器的准备阶段耗时 (PR #78381)，为更精细的编排和监控奠定了基础。
- **安全与审计：** 提交了“安全矩阵运行时事实审计模型” (PR #92086)，旨在形式化建模安全策略，标志着项目安全架构迈出了体系化的一步。
- **AI 辅助功能增强：** 针对 `claude-bridge` 添加了应用服务器框架扩展 (PR #86655)，以原生支持 Anthropic 模型；同时，修复了 OpenRouter 模型响应摘要的累积问题 (PR #92300)。
- **开发与部署体验：** 提交了一个自动化 PR 审查修复管道 (PR #68936)，显示了项目在自动化 DevOps 流程上的探索。同时，修复了 Windows 路径在 QMD 命令中的兼容性问题 (PR #92308) 和 `cron edit` 命令可能丢失时区配置的问题 (PR #92295, #92304)。

## 4. 社区热点

今日最受关注、讨论热度最高的是以下几个议题：

1.  **跨平台 Clawdbot 应用 (Issue #75)**
    - **链接:** [openclaw/openclaw Issue #75](https://github.com/openclaw/openclaw/issues/75)
    - **背景:** 社区强烈要求为 Linux 和 Windows 提供官方的桌面 Clawdbot 应用，以实现与 macOS 类似的完整功能集。
    - **分析:** 该议题持续近半年，始终是社区最热话题（109条评论，79个👍）。这表明用户对原生桌面应用的渴望远超 Web UI 或 CLI，追求更稳定、集成度更高的本地体验。缺乏官方支持可能阻碍了项目在更广泛的企业用户中的采用。

2.  **会话上下文混乱 (Issue #32296)**
    - **链接:** [openclaw/openclaw Issue #32296](https://github.com/openclaw/openclaw/issues/32296)
    - **背景:** 用户报告 Agent 会回复上一条消息而不是当前消息，导致对话严重错乱。
    - **分析:** 这是一个直接影响用户体验的高优先级（P1）“铂金级”Bug。它暴露出项目在会话管理（Session State）和上下文跟踪（Context Tracking）上存在根本性缺陷，如果不修复，将严重动摇用户对 Agent 可靠性的信心。

3.  **预构建 Android APK (Issue #9443)**
    - **链接:** [openclaw/openclaw Issue #9443](https://github.com/openclaw/openclaw/issues/9443)
    - **背景:** Android 用户强烈要求提供预编译好的 APK 文件，而不是让用户自行从源代码构建。
    - **分析:** 这是从“开发者”到“普通用户”转变过程中的典型痛点。用户希望“开箱即用”，而不是面对复杂的构建流程。该请求虽被标记为 P2，但其高评论量和普遍性表明，降低终端的接入门槛是项目走向大众化的关键一步。

## 5. Bug 与稳定性

今天报告了多个严重的 Bug，按严重程度排列如下：

- **会话上下文混乱 (P1 #32296):** Agent 回复前一条消息。**无修复 PR。** (影响：会话状态、消息丢失)
- **信号守护进程竞态条件 (P1 #22676):** SIGUSR1 重启时导致孤儿进程和发送失败，与通信模块的稳定性直接相关。**有相关 PR (#39182) 但可能引入了新问题 (#40611)。** (影响：消息丢失、崩溃循环)
- **系统提示词注入问题 (P1 #29387):** `AgentDir` 中的引导文件被忽略，可能导致用户配置的上下文失效。**无修复 PR。** (影响：会话状态、安全)
- **LLM 请求神秘失败 (P1 #91363):** 隔离的 cron 任务在“模型调用开始”阶段持续失败，严重影响自动化任务的可靠性。**无修复 PR。** (影响：会话状态、消息丢失、认证提供方)
- **嵌入式运行器停止 (P1 #40540):** `openclaw update` 命令在 Windows 上因 EBUSY 错误失败，影响大版本升级体验。**无修复 PR。** (影响：其他)
- **编辑 WebSocket URL 清除令牌 (P2 #41545):** 仪表盘 UI 的一个易用性BUG，可能导致用户连接失败。**无修复 PR。** (影响：会话状态、认证提供方)
- **缓存保留配置被忽略 (P2 #37966):** 对于通过 LiteLLM 代理的 Anthropic 模型，`cacheRetention` 设置无效，导致 Tokens 消耗增加。**无修复 PR。** (影响：认证提供方)

## 6. 功能请求与路线图信号

今天社区提出了多项有意义的功能请求，部分已有相关 PR 跟进：

- **跨平台原生 App (Feature #75):** 如前所述，呼声极高。虽然暂无对应 PR，但这是项目走向成熟必须攻克的关卡。
- **秘密遮蔽与沙箱化 (Feature #10659, #6731):** “Masked Secrets” 提案和“安全/非安全 ClawdBot”提案都指向同一个核心痛点：**Agent 对 API 密钥等敏感信息的可见性和访问控制**。这是提高企业信任度的关键。
- **分层引导文件加载 (Feature #22438):** 该功能请求已有一个**相应的 PR (#22439)**，旨在通过“分层加载”机制，按需注入上下文，从而节省 Tokens。这是一个直接改善用户成本和效率的实用功能，很可能被纳入下一版本。
- **安全矩阵审计模型 (PR #92086):** 这个 PR 不仅是一个 Bug 修复，更是在构建一个系统化的安全策略框架。它被精确地标记为“security”，是项目安全体系的基石，具有重要的路线图意义。
- **多 Agent 协作增强 (RFC #35203):** 这是一个宏大的 RFC，提出了能力画像、共享黑板、分层记忆和 Token 成本治理等概念。它反映了社区对复杂多 Agent 协作场景的深度探索需求，是项目未来发展的一个重要方向。

## 7. 用户反馈摘要

从今日的 Issue 评论中可以提炼出以下用户声音：

- **“开箱即用”的强烈诉求:** 用户在等待预构建的 Android APK，不想自己编译。同时，Linux/Windows 原生应用的缺失也让部分用户感到失望。
- **对稳定性的深切担忧:** 出现会话上下文错乱、cron 任务无故失败、系统更新阻塞等问题，让用户感到沮丧，并对 Agent 的可靠性产生怀疑。
- **安全是首要关切:** 用户明确要求保护 API 密钥不被 Agent 读取，以及希望有更精细的文件系统访问控制（如 `tools.fileAccess`）和命令执行的黑名单机制。这表明在消费级应用之外，安全问题正成为专业用户的核心考量。
- **对“过度自动化”的抱怨:** 子 Agent 无法关闭完成通知 (Issue #8299) 的反馈，说明用户希望在获得自动化便利的同时，保留对工作流细节的控制权，而非被 AI 的每一个动作“轰炸”。

## 8. 待处理积压

以下是一些长期未解决或未得到有效回应的重要议题和 PR，需要项目维护者特别关注：

1.  **跨平台应用 (Issue #75):** 项目最老、最热的议题之一。维护者应就此给出一个明确的时间表或技术方案，以安抚社区情绪。
2.  **Docker + Sandbox 工作区访问问题 (Issue #31331):** 这是一个阻碍 Docker 用户上手使用的关键问题，且自3月初提出后一直处于开放状态，没有任何被解决的迹象。维护者需提供临时工作区或立即着手修复。
3.  **PR #22439 (分层引导文件加载) 和 PR #18860 (工具列表 Hook):** 这两个 PR 都已存在一段时间，且有详尽的实现方案，亟待维护者进行 Code Review 和合并决策。它们代表着社区对改进核心功能的重要贡献。
4.  **预构建 APK 请求 (Issue #9443):** 与 Issue #75 类似，是降低用户门槛的刚需。维护者应考虑将其列为短期目标，例如先提供一个由 CI 自动构建的、无签名的 Debug APK。

---

## 横向生态对比

好的，作为资深技术分析师，以下是根据您提供的2026年6月12日各开源项目动态数据生成的横向对比分析报告。

---

### **AI 智能体开源生态横向对比分析报告 (2026-06-12)**

#### **1. 生态全景**

2026年6月12日，个人AI助手与自主智能体开源生态呈现出 **“大版本迭代后的密集修补期”** 与 **“核心能力从单机向多Agent编排演进”** 的双重特征。头部项目如OpenClaw、ZeroClaw处于功能快速扩张后的稳定性承压阶段，暴露出大量与多Agent交互、上下文管理及模型兼容性相关的严重Bug。与此同时，社区对更细粒度的权限控制、跨平台原生体验以及更低成本的自动化运行（如Token预算、本地模型支持）提出了迫切需求。整体生态正从“尝鲜”走向“实用”，稳定性与安全性成为决定项目能否获得主流采用的关键胜负手。

#### **2. 各项目活跃度对比**

| 项目名称 | 今日Issues (新/更新) | 今日PRs (新/更新) | 版本发布 | 健康度评估 | 关键特征 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~500 (高) | ~500 (高) | 无 | **高风险** | 吞吐量极高，但合并率低(22%)，Bug积压严重，社区呼声与维护能力脱节。 |
| **NanoBot** | 4 | 19 | 无 | **健康** | 高效维护，6个PR快速合并，对关键Bug (MCP崩溃) 响应迅速。 |
| **Hermes Agent** | >40 (极高) | >40 (极高) | 无 | **高活跃，中风险** | 问题与PR均极多，暴露多处P2级核心功能Bug (重复回复、审批失效)，维护者正积极跟进部分修复。 |
| **PicoClaw** | 6 | 31 | Nightly Build | **健康，迭代快** | 18个PR合并，修复了`allowed_cidrs`绕过等安全漏洞和多个通道稳定性问题。 |
| **NanoClaw** | 2 | 15 | 无 | **健康，聚焦基础设施** | 9个PR合并，专注于多Bot、审批回调、容器生命周期等底层平台基础设施。 |
| **NullClaw** | 1 | 0 | 无 | **低活跃，需关注** | 社区无代码贡献，仅有1个关于本地模型集成问题的Bug报告，项目有停滞迹象。 |
| **IronClaw** | 30 | 47 | 无 | **冲刺阶段，高活跃** | “Reborn”版本QA冲刺，合并25个PR，大量Bug修复和自动化测试建设，积极应对社区反馈。 |
| **LobsterAI** | N/A | N/A | 无 | **高活跃，功能扩展** | 18个PR合并，新增“Computer Use”重大功能，并修复了OOM等稳定性问题。 |
| **TinyClaw** | 0 | 0 | 无 | **无活动** | 代码库在报告周期内无任何变动。 |
| **Moltis** | 1 | 1 | 无 | **正常偏低** | 聚焦于WhatsApp消息投递和Fastmail集成的细节Bug修复。 |
| **CoPaw** | 33 | 42 | 2个补丁 (v1.1.11) | **高活跃，稳定性待提升** | 快速发布补丁修复回归bug，但仍有多起桌面客户端崩溃/进程溢出等严重问题。 |
| **ZeptoClaw** | 0 | 0 | 无 | **无活动** | 代码库在报告周期内无任何变动。 |
| **ZeroClaw** | 50 | 50 | v0.8.0 发布 | **高活跃，新版本阵痛期** | 爆发大量S1级Bug（多Agent、模型兼容性、配置适配），核心功能受到严重阻塞。 |

#### **3. OpenClaw 在生态中的定位**

*   **社区规模与影响力**：OpenClaw是生态中**无可争议的流量中心**。其单日500条Issue/PR的吞吐量远超市面上其他所有项目，暗示其拥有最庞大的用户和贡献者基础。
*   **技术路线与优势**：作为稳定版本，今日其核心进展集中在 **安全审计模型** (PR #92086) 和 **子代理工具权限精细化管理** (PR #78441)，表明其在多Agent安全治理和可观测性方面走在最前列。这是其区别于NanoBot等项目的核心优势。
*   **主要短板**：**维护速度严重跟不上社区增长**。78%的PR和95%的Issue处于开放状态，远超同侪。这说明项目核心团队在应对社区贡献和Bug修复上面临巨大瓶颈。相比之下，NanoBot、PicoClaw等项目在合并效率上表现更好。
*   **竞争态势**：ZeroClaw的v0.8.0大版本在多Agent和配置管理上提供了更具颠覆性的创新，但随之而来的是更高的稳定性风险。OpenClaw则扮演着“稳定基石”的角色，其依赖庞大的社区生态和插件，但创新速度受到维护瓶颈的制约。

#### **4. 共同关注的技术方向**

| 共同方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **多Agent协作与编排** | **OpenClaw** (子代理工具权限) <br> **NanoClaw** (多Bot基础设施) <br> **ZeroClaw** (Delegate代理模式) <br> **LobsterAI** (多Agent协作需求) <br> **CoPaw** (Swarm团队协作请求) | 需求从单一对话转向复杂的工作流编排，包括：子代理权限隔离、跨Agent上下文共享、任务分配与结果汇总、自动化审批流程。 |
| **模型/提供商兼容性** | **OpenClaw** (OpenRouter, Claude Bridge) <br> **NanoBot** (本地模型超时，多自定义提供商) <br> **Hermes Agent** (模型自动路由) <br> **PicoClaw** (模型幻觉检测) <br> **ZeroClaw** (Gemini, Anthropic兼容性Bug) <br> **NullClaw** (本地模型输出不完整) | 本地模型（Ollama、LM Studio）支持不足、超时配置不合理；流式/异步模型调用不稳定；对多模型切换和自动路由有强烈需求。 |
| **安全性/权限控制** | **OpenClaw** (安全矩阵模型，秘密遮蔽) <br> **NanoClaw** (CLI上下文持久化) <br> **PicoClaw** (`allowed_cidrs`绕过) <br> **ZeroClaw** (`risk_profile`, `allowed_tools`冲突) <br> **CoPaw** (密钥隔离) | Agent对API密钥、文件系统、Shell命令的访问控制颗粒度不够细；审批流程缺乏上下文信息或容易失效；对“人类监督”这一安全机制的信任度不足。 |
| **跨平台/原生体验** | **OpenClaw** (Linux/Windows原生App、Android APK) <br> **CoPaw** (桌面端SSL/崩溃/内存问题) <br> **IronClaw** (WebUI稳定性修复) | 用户强烈要求摆脱终端，获得“开箱即用”的稳定原生桌面和移动端体验。桌面端的稳定性（尤其是Windows版）是普遍痛点。 |
| **上下文与成本管理** | **OpenClaw** (分层引导文件加载) <br> **Hermes Agent** (Token成本治理) <br> **ZeroClaw** (默认预算不足、压缩器丢数据) <br> **CoPaw** (Token统计、上下文压缩) <br> **LobsterAI** (回复重复浪费Token) | 用户对Token消耗高度敏感，要求更智能的上下文窗口管理、更透明的Token使用统计和更有效的记忆压缩策略，以控制运行成本。 |

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型平台，生态庞大 | 社区开发者、重度使用者、插件作者 | 模块化，强依赖社区贡献，维护压力大。 |
| **NanoBot** | 轻量级、高效、易用的聊天机器人框架 | 希望快速集成AI到现有通讯平台的个人/团队 | 快速迭代，对用户反馈响应快，SDK扩展友好。 |
| **Hermes Agent** | 纯文本终端AI Agent（CLI/TUI/桌面） | 追求极致效率和技术控制的开发者 | 聚焦命令行和桌面体验，深度集成代码编辑和系统操作。 |
| **PicoClaw** | 多通道、多平台、嵌入式场景 | 希望在不同IM/硬件上运行智能体的嵌入开发者 | 强调通道兼容性（飞书、WhatsApp），信号守护进程机制稳定。 |
| **NanoClaw** | 多租户、多Bot、平台级基础设施 | 构建AI SaaS平台或企业级服务的高级开发者 | 架构追求高度抽象和扩展性，支持多Bot实例和审批回调注册表。 |
| **ZeroClaw** | 多Agent、新配置Schema、高度可配置 | 勇于尝鲜的有经验的Agent开发者 | 一次部署多个Agent，拥有彻底重写的配置系统，但稳定性风险高。 |
| **IronClaw** | “Reborn”版本功能迭代与QA | 对生产环境可用性要求高的企业用户或开发者 | 重心在于自动化测试和质量保证，为“生产就绪”版本冲刺。 |
| **LobsterAI** | 企业级协作（Cowork）与办公自动化 | 需要AI辅助进行多人协作和复杂办公任务的团队 | 强调“协同工作”场景，新增“Computer Use”功能，可操作桌面应用。 |
| **CoPaw** | 桌面端强交互、AI辅助编程与助手 | 桌面端用户，特别是需要与本地环境（文件、项目）深度交互的开发者 | 与Rust原生桌面客户端（Tauri）结合紧密，聚焦桌面稳定性与本地集成。 |
| **Moltis** | 跨平台轻量级AI助手 | 希望在所有常用IM（WhatsApp, Signal等）上拥有个人助手的一般用户 | 聚焦单Agent的多通道接入，架构追求轻便。 |

#### **6. 社区热度与成熟度**

*   **快速迭代阶段 (高风险高回报)**：
    *   **ZeroClaw**：新版本发布后Bug井喷，但这也是功能创新的阵痛期。社区极度活跃，但用户信心受到考验。
    *   **IronClaw**：“Reborn”版本的QA冲刺阶段，代码改动频繁，Bug量大，但目标是提升版本成熟度。

*   **质量巩固与体验优化阶段**：
    *   **PicoClaw**：在稳定迭代的基础上，积极修复安全漏洞和通道稳定性Bug，社区讨论理性，指向具体的技术细节和UX改善。
    *   **NanoBot**：高效、有序地维护，核心功能稳步增强，同时在用户痛点上（如Stream超时）迅速响应，社区满意度较高。
    *   **NanoClaw**：专注于更难的基础设施建设（多Bot、审批、容器），虽然活跃度不如一线项目，但其贡献的架构价值对生态长期发展至关重要。

*   **功能扩展与生态构建阶段**：
    *   **LobsterAI**：通过合并重大功能 (Computer Use) 快速扩展能力边界，产品化程度高。
    *   **CoPaw**：在用户期待的“Agent自动化”与“桌面稳定性”之间艰难平衡，既有功能激进，也有Bug修复。

*   **停滞/低活跃阶段**：
    *   **NullClaw, TinyClaw, ZeptoClaw**：这些项目在报告周期内几乎没有社区或开发活动，可能已接近维护终点或被其它项目取代。

#### **7. 值得关注的趋势信号**

1.  **“多Agent”不再是概念，而是步入“可用性”审判期**：ZeroClaw的`delegate`代理Bug和ZeroClaw/OpenClaw对子Agent权限的精细化管理，都指向一个事实：实现稳定、安全、可控的多Agent协作是当前最大的技术门槛和用户痛点。能率先解决此问题的项目将赢得下一阶段的竞争。

2.  **“成本与效率”成为新的战斗前线**：Token预算不足、Steam超时、上下文压缩丢数据、重复回复浪费Token……这些报告不再是边缘反馈，而是规模化使用后的必然结果。这要求项目不仅要有聪明的AI，更要有**聪明的“成本控制”系统**，如动态上下文压缩、模型自动降级路由、透明化的Token统计面板。

3.  **从“AI Chat”到“AI as a Service”的平台化转向**：NanoClaw的“多Bot通道”和“审批决议回调注册表”以及ZeroClaw的“Dashboard节点管理”，都表明生态开始向**平台化（PaaS）**演进。开发者不再满足于做一个聊天机器人，而是要构建能运行多种Agent、具备监控、审核、路由能力的平台。

4.  **本地部署的“双刃剑”**：社区对Ollama、LM Studio等本地模型的支持期望日益增长（NanoBot、NullClaw、CoPaw均有反馈），这表明用户对数据隐私和控制权有真实需求。但同时，这也暴露了本地模型在稳定性、兼容性和推理效果上的巨大短板，给开发者带来了新的适配和测试挑战。

5.  **企业级安全需求正在下渗到开源项目**：从OpenClaw的安全矩阵模型到ZeroClaw的`risk_profile`再到PicoClaw的`allowed_cidrs`，安全已从可选功能变为核心特性。API密钥保护（Secrecy masking）、职责分离（带上下文的审批窗口）、细粒度文件/命令访问控制等企业级安全诉求，正在成为所有严肃的个人AI助手项目的标配。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 NanoBot 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，以下为您生成 2026-06-12 的项目动态日报。

---

# NanoBot 项目动态日报 | 2026-06-12

## 1. 今日速览

今日项目活跃度**极高**。过去24小时内，共有19个Pull Request (PR) 被更新，其中6个已成功合并/关闭，这表明核心开发团队的代码合并和审查效率很高。社区提交了4个新的或更新的Issue，其中2个已关闭，问题响应及时。`enhancement` 和 `bug` 相关的讨论是今日热点，特别是围绕 **MCP 崩溃**、**Sandbox 兼容性** 和 **SDK 扩展** 的核心议题。整体来看，项目正处于功能快速迭代和稳定性持续加固的并行阶段。

## 2. 版本发布

*无新版本发布。*

## 3. 项目进展

今日共有6个PR被合并或关闭，标志着关键功能的稳步推进和重要Bug的修复。

- **Sandbox 兼容性修复**: **PR #4236** 针对 Ubuntu 24.04 及更新Linux发行版上 `bwrap` sandbox 因非特权用户命名空间限制而失败的问题，已通过审查并关闭。这对于扩大 NanoBot 在不同Linux环境下的部署范围至关重要。
- **Slack 频道管理增强**: **PR #4289** 合并，新增 `groupRequireMention` 配置项。该功能允许将 Slack `allowlist` 模式下的频道设置为**仅当@提及机器人时才响应**，解决了用户在多频道环境下对噪音控制的需求。
- **消息分片稳定性修复**: **PR #4257** 合并。修复了 `split_message` 函数在分割长文本时可能切裂代码块（fenced-code-block）导致渲染错误的问题。这提升了与代码交互的鲁棒性。
- **转录提供商扩展**: **PR #4281** 合并。成功集成 **SiliconFlow** 作为新的转录提供商，使用户拥有了除现有方案外的更多选择，体现了项目在生态兼容性上的投入。
- **Stream 超时可配置**: **PR #4020** 关闭。此PR使流式传输的空闲超时时间（`stream-idle timeout`）变为每个提供商可配置，替代了单一的环境变量。这对于应对像 `Ollama` 或 `LM Studio` 这类响应较慢的本地模型非常友好。
- **代码重构与清理**: **PR #4298, #4297** 合并，推测为工作区特性（Worktree）的研究性文档提交。**PR #4294** 是重要的代码库清理工作，**将 Electron 桌面应用从核心主仓库中移除**，表明项目正专注于核心引擎和WebUI的打磨，桌面应用将以独立形式发展。

## 4. 社区热点

今日最活跃的讨论集中在 **Stream 超时配置** 和 **多自定义提供商支持** 上。

- **`#4020` [CLOSED] - 流式超时可配置**: 该PR虽然在今天关闭，但在此之前引发了大量讨论。社区用户，尤其是使用本地模型的开发者，对90秒的硬编码超时普遍感到不满。该PR的合并是社区长期诉求的直接回应，体现了项目对开发者反馈的重视。
- **`#4305` [OPEN] - 多自定义提供商需求**: 该Issue提出需要一个更灵活的方式来配置**多个自定义 OpenAI 兼容提供商**。与之关联的 `#3239` PR 也仍然开放。这反映了用户在使用多个不同API（如企业内部API、不同云服务商）时的强烈需求，是社区普遍关注的功能空白。链接: `#4305`

## 5. Bug 与稳定性

今日报告和修复了多个稳定性问题，其中 MCP 崩溃问题最为严重。

- **严重**: **`#4302` [OPEN] - Nanobot Gateway MCP重连后崩溃**。这是今日报告的**最严重Bug**。用户在MCP会话断开重连后，Gateway级进程直接崩溃，影响核心服务可用性。**已有修复PR `#4303`** 提出，旨在关闭跟踪的生成器以避免垃圾回收时的崩溃。链接: `#4302`, `#4303`
- **中等**: **`#4236` [CLOSED] - Bwrap Sandbox在Ubuntu 24.04上失败**。已通过审查并关闭，但此问题影响了特定Linux发行版上的安全沙箱功能，具有平台级影响。
- **中等**: **`#4306` [OPEN] - 孤立的工具结果（Orphaned Tool Results）**。此PR旨在修复状态历史中可能残留无效 `tool_call_id` 的问题，这会导致与OpenAI/Anthropic等严格API的兼容性问题。链接: `#4306`
- **常规**: **`#4257` [CLOSED] - 消息分割破坏代码块**。已修复。

## 6. 功能请求与路线图信号

今日涌现了多个有潜力的功能请求，其中一些已有对应的PR在推进。

- **高可能性纳入**: **`#4305` [OPEN] - 多自定义提供商支持**。需求清晰且强烈，已有同主题的 `#3239` PR 正在开发中，有望成为下一版本的重点特性。
- **高可能性纳入**: **`#4299` [OPEN] - 将Cron计划任务绑定到会话**。该PR目标是让Cron任务作为会话的一部分执行，这能极大提升自动化任务与用户交互流程的整合度。这是一个相对高阶的功能增强。
- **稳定性增强**: **`#4304` [OPEN] - Cron任务等待子代理完成**。此PR针对Cron任务产生的子代理未完成就被标记为完成的问题，旨在修复一个隐蔽但关键的逻辑缺陷。
- **SDK 扩展**: **`#4296` [OPEN] - 扩展Python SDK运行时控制**。该PR将SDK从简单的 `bot.run()` 抽象扩展为更丰富的开发者API，这对于高级用户和集成场景意义重大。

## 7. 用户反馈摘要

- **痛点1 - 本地模型兼容性**: 用户 `eldar702` 在 `#4020` 中提出，90秒的流式超时对于 `LM Studio`、`Ollama` 等本地模型过于严苛，导致在稍复杂的任务上频繁中断。该痛点已通过PR解决，体现了项目对非云用户的重视。
- **痛点2 - 版本信息不可见**: 用户 `viblo` 在 `#4233` 中建议在WebUI上显示版本号，以便快速确认是否已更新。这表明用户对版本管理和升级有明确需求。
- **痛点3 - 动态工具结果兼容性**: 用户 `tangtaizong666` 在 `#4306` 中修复了“孤立的工具结果”问题，这虽非用户直接报告，但反映了维护者对项目在高级AI API兼容性上的严格要求。

## 8. 待处理积压

以下为需要维护者重点关注、长期未关闭或停滞的重要Issue/PR。

- **`#3538` [OPEN] - 为Gateway添加启动/停止/重启命令**。创建于4月29日，一个基础但重要的运维功能。该PR长期未合并，可能需要维护者对实现方案进行二次评估。链接: `#3538`
- **`#3239` [OPEN] - 支持多个自定义 OpenAI 兼容提供商**。与今日热点Issue `#4305` 相关，但其本身为PR。该功能需求虽非今日提出，但社区呼声极高，建议加快审查进度。

---
**分析师总结**: NanoBot 项目今日表现出健康的社区生态和高效的维护节奏。核心功能（Sandbox、SDK、Provider）稳步推进，同时对用户反馈的高优先级Bug（如MCP崩溃、Stream超时）响应迅速。当前最大的功能缺口和社区热点是“多自定义提供商支持”，建议项目方优先推动此项。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于你提供的 Hermes Agent 数据生成的 2026-06-12 项目动态日报。

---

# Hermes Agent 项目日报 | 2026-06-12

## 1. 今日速览

今日项目保持极高的活跃度，主要体现为大量新增的 Issue 和 PR。过去24小时内，社区提交了超过40个新的或活跃的 Issue，并创建了同等数量的 Pull Request，显示了极旺盛的贡献热情。项目健康度整体良好，但存在一些影响核心体验的 Bug 和稳定性问题正在被集中处理。关键动态包括：针对 Discord 断线后 Cron 任务失效、WebSocket 超时、桌面端更新失败等问题的修复 PR 已被提交，表明维护者正在快速响应社区反馈。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

过去24小时内有6个 PR 被合并或关闭，以下是其中重要的推进项：

- **RTL文本显示支持**：合并了两个 PR ([#44169](https://github.com/NousResearch/hermes-agent/pull/44169) 和 [#44065](https://github.com/NousResearch/hermes-agent/pull/44065))，为桌面聊天界面增加了自动检测并正确渲染阿拉伯语、希伯来语等从右至左（RTL）文本方向的功能，提升了多语言用户的体验。
- **桌面端稳定性修复**：合入了 PR [#43660](https://github.com/NousResearch/hermes-agent/pull/43660)，修复了桌面端在应用重载后丢失正在编辑的草稿的问题。
- **CLI-桌面兼容性**：合入了 PR [#40674](https://github.com/NousResearch/hermes-agent/pull/40674)，修复了 CLI 版本与桌面应用版本不一致时导致桌面启动失败的问题，并限制了桌面日志的无限制增长。
- **飞书平台支持**：合入了 PR [#44192](https://github.com/NousResearch/hermes-agent/pull/44192)，为飞书平台增加了CardKit v1 流式卡片支持，实现了 AI 回复在飞书聊天中的“打字机”效果。

## 4. 社区热点

今日讨论热度最高的 Issue 和 PR 反映了社区聚焦的几个核心领域：

1.  **模型自主路由 (#16525)**：这个有7条评论和3个👍的 Feature Request 持续受到关注。核心诉求是希望 Agent 自身能根据任务的复杂度，自主切换底层模型（例如从快速便宜的模型切换到更强大的付费模型）。这表明社区对 Agent 的自主性和成本控制提出了更高要求。

2.  **认证与审核问题 (#37812)**：关于桌面应用中审批/手动确认弹窗不渲染的 Bug，有7条评论和4个👍，是所有 Bug 中反响最强烈的。这表明用户对“人类监督”这一安全机制非常在意，其失效会严重影响信任感。

3.  **工具暴露不一致 (#38945)**：另一个高讨论度的 Bug，用户反映桌面/TUI 会话无法可靠地暴露已配置的 MCP 工具（如 Todoist），但 CLI 却可以。这种不一致性会影响工作流效率，用户希望体验能与 Claude Code 或 Codex 等工具看齐。

4.  **构建环境问题 (#44121)**：`npm ci` 在 npm 11 下因为 lock 文件版本不匹配而失败的问题获得了6条评论，这是一个影响所有新贡献者的拦路虎，维护者需尽快修复。

## 5. Bug 与稳定性

今日报告的 Bug 覆盖面很广，按严重程度排列如下：

- **P1 (严重, 高危)**：
    - [#44585](https://github.com/NousResearch/hermes-agent/issues/44585): **Cron 任务可继承临时付费模型并持续扣费**。这是一个严重的财务安全问题，即使操作员试图暂停/停止任务，Cron 任务仍可能使用付费模型进行推理，导致意外支出。

- **P2 (高, 影响核心功能)**：
    - [#44497](https://github.com/NousResearch/hermes-agent/issues/44497): **Agent 对同一条用户消息生成重复回复**。这是一个对话逻辑 BUG，会严重干扰用户体验。
    - [#44499](https://github.com/NousResearch/hermes-agent/issues/44499): **桌面端忽略用户指明的 BrowserOS MCP，强制使用内置浏览器工具**。这违反了用户的显式配置意图，属于工具调度 Bug。
    - [#44541](https://github.com/NousResearch/hermes-agent/issues/44541): **Discord 重连后 Cron 任务投递失败**。已有 PR [#44599](https://github.com/NousResearch/hermes-agent/pull/44599) 尝试修复。
    - [#44560](https://github.com/NousResearch/hermes-agent/issues/44560): **`model.options` 处理程序同步阻塞导致 WebSocket 超时**。已有 PR [#44598](https://github.com/NousResearch/hermes-agent/pull/44598) 尝试修复。
    - [#44580](https://github.com/NousResearch/hermes-agent/issues/44580): **`hermes update` 在桌面端重建失败时仍报告成功**。已有 PR [#44591](https://github.com/NousResearch/hermes-agent/pull/44591) 尝试修复。
    - [#44121](https://github.com/NousResearch/hermes-agent/issues/44121): **新环境下 `npm ci` 因 lock 文件问题失败**。影响开发者 onboarding。

- **P3 (中低, 影响特定场景)**：
    - [#44562](https://github.com/NousResearch/hermes-agent/issues/44562) & [#41693](https://github.com/NousResearch/hermes-agent/issues/41693): 桌面端因工具返回异常数据导致前端 `tapClientLookup` 索引越界崩溃。这是两个相似但独立的渲染器崩溃问题。
    - [#44543](https://github.com/NousResearch/hermes-agent/issues/44543): Windows 桌面端 `/undo` 命令无效。
    - [#44557](https://github.com/NousResearch/hermes-agent/issues/44557): Hermes Studio 更新器死锁问题。
    - [#44582](https://github.com/NousResearch/hermes-agent/issues/44582): `pre_tool_call` 插件钩子在 Agent 执行工具时未被调用。

## 6. 功能请求与路线图信号

除了模型自动路由 [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) 和 Xiaomi MiMo 令牌计划 [#14285](https://github.com/NousResearch/hermes-agent/issues/14285) 这两个长期需求外，今日出现了几个值得关注的新方向，并有对应的 PR 在推进：

- **`.hermes/.env` 变量注入 MCP 子进程**：Issue [#44548](https://github.com/NousResearch/hermes-agent/issues/44548) 提出 `.env` 文件的环境变量应自动传播到 MCP 服务器子进程，以减少凭证重复配置。这是一个明确的 UX 改善需求。
- **Agent 自动重试格式错误的工具调用**：PR [#44587](https://github.com/NousResearch/hermes-agent/pull/44587) 提出，当本地量化模型产生格式错误的工具调用时，Agent 应能自动重试。这直接针对社区常见的“小模型生成不稳定”问题，有很高的被采纳可能性。
- **远程控制面板**：PR [#44382](https://github.com/NousResearch/hermes-agent/pull/44382) 增加了通过网关远程控制 CLI 端人工干预提示（如批准/拒绝）的功能。这表明项目正在探索更高级的远程 Agent 管理与协作场景。

## 7. 用户反馈摘要

- **满意度**：用户对多语言支持（RTL文本）和多平台集成（如飞书流式卡片）的快速实现表示满意并积极参与贡献。
- **痛点**：
    - **工具生态体验不一致**：多处反馈桌面/TUI 与 CLI 在工具（如 MCP）的使用体验上存在差异，用户期望在所有界面上获得一致的可靠性。
    - **更新机制脆弱**：至少两个 Bug ([#44580](https://github.com/NousResearch/hermes-agent/issues/44580), [#44557](https://github.com/NousResearch/hermes-agent/issues/44557)) 指向更新的失败或死锁，这是影响所有用户的通用问题。
    - **核心功能稳定性**：重复回复、审批弹窗失效、Cron 任务出Bug等P2问题直接损害了用户对 Agent 可靠性的信任。
- **使用场景**：用户普遍在真实工作流中使用 Hermes，包括通过 MCP 连接 TODO 等任务管理工具、通过 Cron 执行定时任务、以及通过各种平台（Discord, 飞书）进行交互。

## 8. 待处理积压

以下为长期未获响应或解决的重要 Issue，建议维护者优先关注：

- **#16525 Feature: 模型自动路由**：自 4 月 27 日提出，反响热烈（+3），至今无维护者反应。该功能能极大提升 Agent 的实用性和成本效率。
- **#37812 Bug: 桌面端手动审批弹窗不渲染**：自 6 月 3 日提出，反响强烈（+4），同样没有后续。这是一个影响安全信任的严重 UX Bug。
- **#38945 Bug: 桌面/TUI MCP 工具暴露不一致**：也是迫切需要解决的痛点，影响了重度 MCP 用户的日常使用。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw GitHub 数据生成的 2026-06-12 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-12

## 1. 今日速览

今日项目活跃度极高，共处理 **31 个 PR**（其中 18 个已合并/关闭）和 **6 个 Issues**（其中 3 个已关闭）。社区和核心开发者的协作与修复工作非常密集，尤其是在消息通道的稳定性和安全性方面。同时，一个旨在重构多代理协作机制的大型功能 PR `#2937` 仍在审阅中，表明项目正在向更复杂的分布式架构演进。总体来看，项目处于稳定迭代与关键 Bug 修复并行的健康状态。

## 2. 版本发布

### 🚀 Nightly Build v0.2.9-nightly.20260612.413d3749
*   **链接**: [查看完整更新日志](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
*   **详情**: 这是一个自动化构建的测试版本，可能不稳定。包含了截至 `main` 分支 `413d3749` 提交的所有最新代码。
*   **注意事项**: 不建议在生产环境使用，仅用于尝鲜和测试。

## 3. 项目进展

今日共合并/关闭 18 个 PR，其中有几项核心改进值得关注：

*   **通道消息稳定性修复**:
    *   `#2957` [CLOSED] **fix(channels): prevent tool_calls from being dropped during streaming** - 修复了在流式传输过程中，`tool_calls` 消息被错误丢弃的问题，这对依赖工具调用的工作流至关重要。
    *   `#2956` [CLOSED] **fix: preserve channel enabled state when merging security.yml** - 修复了加载 `.security.yml` 配置时覆盖了 `config.json` 中通道启用状态的问题，解决了用户配置的意外重置。
    *   `#2934` [CLOSED] **fix(channels): allow whatsapp native mode with use_native flag** - 修复了 WhatsApp 通道原生模式（使用 whatsmeow）无法正常工作的配置检测问题。

*   **模型兼容性与正确性**:
    *   `#2947` [CLOSED] **fix: correct claude-sonnet-4.6 model ID to use hyphens** - 修正了 Claude Sonnet 4.6 模型的默认 ID，解决了因 API ID 格式错误导致 404 的问题。

*   **安全性与健壮性**:
    *   `#2955` [CLOSED] **fix: verify process identity in singleton PID check** - 修复了单例模式下的 PID 检查漏洞，确保检查到的 PID 确实属于 PicoClaw 进程，而非被其他进程复用的 PID，防止启动失败或冲突。
    *   `#3080` [CLOSED] **[Security] PicoClaw launcher `allowed_cidrs` bypass** - 安全警报：修复了首次运行设置期间，可以绕过 `allowed_cidrs` 限制进行同主机回环代理的安全漏洞。

*   **开发质量提升**:
    *   `#3060` [CLOSED] **fix: use %w for error wrapping** - 修复了错误处理中未使用 `%w` 进行正确包装的问题，提升了代码可维护性和错误追踪能力。

## 4. 社区热点

今日社区讨论最活跃的议题主要集中在以下两个方面：

1.  **异步子代理消息重复 (`#3094`)**: 该 Issue 提出，当使用 `spawn` 工具异步执行子代理时，飞书/Telegram 等通道会收到两次内容相同但排版不同的消息。这引发了用户对任务管理 UX 的讨论，核心诉求是**希望子代理的输出能被更优雅地集成到主代理的最终回复中，而不是作为两条独立消息推送**。
    *   **链接**: [sipeed/picoclaw Issue #3094](https://github.com/sipeed/picoclaw/issues/3094)

2.  **模型幻觉与能力检测 (`#3108`)**: 用户报告当使用不支持视觉功能的模型（如 `deepseek/deepseek-v4-flash`）进行图片描述时，模型会产生与图片无关的“幻觉”内容。这暴露了**模型能力（特别是多模态能力）与实际调用之间的检测缺失问题**，用户希望 PicoClaw 能主动感知模型限制，避免此类无效调用。
    *   **链接**: [sipeed/picoclaw Issue #3108](https://github.com/sipeed/picoclaw/issues/3108)

## 5. Bug 与稳定性

今日报告的 Bug 依严重程度排列如下：

1.  **高危 - 安全性**:
    *   `#3080` [CLOSED] **`allowed_cidrs` 绕过漏洞**: PicoClaw 启动器的 `allowed_cidrs` 在第一轮设置时可能被同主机回环代理绕过。**已有修复 PR 合并**。
        *   **链接**: [sipeed/picoclaw Issue #3080](https://github.com/sipeed/picoclaw/issues/3080)

2.  **中危 - 功能异常**:
    *   `#2954` [CLOSED] **不支持32位Android系统**: 被标记为 `stale` 后关闭。
    *   `#2958` [CLOSED] **`tool_calls` 消息在连续请求中被丢弃**: 影响 pico 通道的 WebSocket 交互。**已有修复 PR (`#2957`) 合并**。
        *   **链接**: [sipeed/picoclaw Issue #2958](https://github.com/sipeed/picoclaw/issues/2958)
    *   `#3094` [OPEN] **异步子代理导致消息重复**: 影响部分通道的 UX，暂无明确修复 PR。
        *   **链接**: [sipeed/picoclaw Issue #3094](https://github.com/sipeed/picoclaw/issues/3094)
    *   `#3108` [OPEN] **模型幻觉**: 使用无视觉能力的模型描述图片时产生幻觉。暂无明确修复 PR。
        *   **链接**: [sipeed/picoclaw Issue #3108](https://github.com/sipeed/picoclaw/issues/3108)

3.  **低危 - 兼容性**:
    *   `#2472` [OPEN] **Windows 路径分隔符不兼容**: `list_dir` 功能因 Go 的 `os.Root` 要求使用前向斜杠 (`/`) 而失败。这是一个长期存在的跨平台问题。
        *   **链接**: [sipeed/picoclaw Issue #2472](https://github.com/sipeed/picoclaw/issues/2472)

## 6. 功能请求与路线图信号

*   **Agent 协作基础设施** (`#2937`): 这是一个大型的开放 PR，旨在为 PicoClaw 引入内部的 Agent 协作总线。该功能将允许不同代理之间通过邮箱和隔离的会话历史进行通信，是迈向复杂多代理编排的关键一步。虽然今天没有合并，但其持续的活跃状态表明这是项目路线上一个重要的方向。
    *   **链接**: [sipeed/picoclaw PR #2937](https://github.com/sipeed/picoclaw/pull/2937)

## 7. 用户反馈摘要

*   **来自 `#3094`**：用户 `v2up-32mb` 对子代理异步执行的消息格式表示了不满。他/她期望子代理的原始输出应该由主代理进行“消化”和“润色”后统一输出，而不是直接推送给用户，这反映了用户对**工作流编排结果的专业性和一致性**有更高期待。
*   **来自 `#3108`**：用户 `afjcjsbx` 在使用模型时遇到了直觉上的误解（期待图片描述），但模型不支持。这暗示，除了修复幻觉问题外，用户也期待一个更智能的**模型能力探测与任务预检查机制**，以便在任务开始前就被告知“此模型无法执行该任务”。

## 8. 待处理积压

以下 Issue 或 PR 长期未得到响应或解决，需要维护者关注：

*   `#2472` [OPEN] **Windows `list_dir` 路径问题**: 自 2026-04-10 提出，至今已有两个月。虽然问题明确，但可能由于优先级或实现复杂性，一直没有进展。Windows 用户的文件系统交互体验会因此受损。
    *   **链接**: [sipeed/picoclaw Issue #2472](https://github.com/sipeed/picoclaw/issues/2472)
*   `#2937` [OPEN] **Agent 协作总线**: 这是一个庞大的功能 PR，自 2026-05-24 提出后已开放近三周，且评论数未知（数据未提供）。如此大规模的重构可能需要更细致的代码审查和社区讨论。
    *   **链接**: [sipeed/picoclaw PR #2937](https://github.com/sipeed/picoclaw/pull/2937)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-12

---

## 1. 今日速览

过去24小时内，NanoClaw 项目维持**高活跃度**，共处理 15 条 PR（其中 9 条已合并/关闭）和 2 条 Issue。社区贡献者 gavrielc 和团队集中交付了一批平台基础设施增强，包括**多机器人通道实例维度**、**审批决议回调注册表**、**Webhook 原始路由注册**等功能，显示项目正加速构建多租户/多bot场景的底层能力。同时，一个已持续 20 天的 Signal 适配器文档 PR 与一个安全相关的 CLI 上下文持久化 PR 仍未合并，值得注意。无新版本发布。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共合并/关闭 9 条 PR，项目在以下方向取得实质性推进：

### 🏗️ 平台基础设施（多 bot 与通道扩展）
- **#2733** - `feat(channels): native channel-instance dimension — multi-bot substrate`  
  [已合并] 引入了原生通道实例维度，为一条通道上运行多个 bot 提供了底层支持。这是多租户架构的关键基础设施。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2733)
- **#2739** - `feat(webhook-server): raw-route registry — non-Chat-SDK webhooks become an append`  
  [已合并] 新增原始路由注册机制，允许非 Chat SDK 的 Webhook 被追加处理，扩展了项目与外部系统的集成能力。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2739)

### ✅ 审批与交付体系增强
- **#2734** - `feat(delivery): getDeliveryAction read side for the action registry`  
  [已合并] 为行动注册表添加了读端查询接口。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2734)
- **#2737** - `feat(approvals): approval-resolved callback registry — modules observe resolution additively`  
  [已合并] 新增审批决议回调注册表，允许模块以累加方式观察审批结果，提升了系统的可观测性和扩展性。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2737)
- **#2735** - `fix(chat-sdk-bridge): record the acting user on resolved approval cards`  
  [已合并] 修复：在已解决的审批卡片上记录实际操作用户。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2735)

### 🔧 容器生命周期与错误修复
- **#2736** - `fix(host-sweep): grace period for freshly-woken containers with stale processing claims`  
  [已合并] 为刚唤醒的、带有过期处理声明的容器增加宽限期，避免误终止。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2736)
- **#2740** - `feat(container): per-group idle timeout — clean exit for ephemeral sessions`  
  [已合并] 为每组容器引入独立的空闲超时机制，临时会话可干净退出。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2740)

### 🐛 关键 Bug 修复
- **#2738** - `fix(session-manager): writeOutboundDirect opens outbound.db read-only — command-gate denials never deliver`  
  [已合并] 修复了 writeOutboundDirect 以只读模式打开 outbound.db 的严重 bug，该 bug 导致命令网关拒绝响应被静默丢弃。此修复直接关联 Issue #2495。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2738)

### 🧪 交互体验改进
- **#2741** - `fix(setup): auto-submit handoff context as Claude's first prompt`  
  [已合并] 修复交互式设置流程中，传递给 Claude 的上下文未被自动提交的问题——现在它会自动作为 Claude 的第一条用户消息出现。  
  [链接](https://github.com/qwibitai/nanoclaw/pull/2741)

**小结**：今日项目在**多 bot 通道、审批框架、容器生命周期、Webhook 集成**四个维度均有显著推进，尤其是 #2733 和 #2739 暗示项目正在构建更灵活的多机器人运营架构。

---

## 4. 社区热点

### 🔥 热点 Issue
**#1356 `Agent memory system redesign`**  
- 作者：Ordinath | 创建于 2026-03-23 | 评论：2 | 👍：6  
- 这是目前社区反响最热烈（6个👍）的 Issue，讨论了当前基于 MEMORY.md + 卫星 markdown 文件的记忆系统在~54个文件、~83KB规模下的扩展瓶颈。  
- 诉求核心：需要更全面、可扩展的智能体记忆系统设计。该项目已持续近3个月未关闭，说明设计复杂度高或社区仍在等待原型。  
[链接](https://github.com/qwibitai/nanoclaw/issues/1356)

### ⚡ 热点 PR
**#2742 `feat(recipes): the PR Factory`**  
- 作者：gavrielc | 创建于今日 | 状态：待合并 | 点赞：0  
- 这是一个**“技能配方”**（recipe）PR，理论上每个 PR 提交后，PR Factory 会自动启动一个专用 worker agent，在 Slack 线程中完成审查、测试计划并等待人工批准。这代表了项目在**自运维/自动化代码审查**方向上的探索，一旦合并可能改变项目协作模式。  
[链接](https://github.com/qwibitai/nanoclaw/pull/2742)

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| **严重** | #2495（相关 PR #2738） | `writeOutboundDirect` 以只读模式打开 outbound.db，所有 INSERT 静默失败，命令网关拒绝响应被丢弃 | ✅ 已由 PR #2738 修复并合并 |
| **中等** | #2743（OPEN） | `ncl wirings create` 跳过 `agent_destinations` 副作用，导致 agent 发送到新聊天时消息被丢弃 | ❌ 待合并（无评论） |
| **中等** | #2744（OPEN） | Signal 适配器静默丢弃 agent 的 `add_reaction` 输出，并忽略入站反应信封 | ❌ 待合并（无评论） |
| **安全** | #2611（OPEN） | CLI 审批后 `CallerContext` 未持久化，可能导致权限上下文丢失 | ❌ 待合并（无评论，已搁置 18 天） |

**修复亮点**：  
- PR #2738 直接解决了 Issue #2495 中报告的严重 bug（只读数据库写入），说明项目对用户报告 bug 的响应速度为 **~28 天**（Issue 创建于 5月15日，修复在 6月11日合并）。
- PR #2736 修复了 host-sweep 中容器生命周期的竞态条件，增强生产环境稳定性。

---

## 6. 功能请求与路线图信号

### 潜在纳入下一版本的功能

| 功能 | 参考 PR/Issue | 分析 |
|------|------------|------|
| **多 bot 同一通道** | #2733（已合并） | 原生通道实例维度已落地，后续可能引来多 bot 路由、消息去重等配套功能 |
| **自动代码审查（PR Factory）** | #2742（待合并） | 如果合并，说明项目正式引入「Agent 辅助代码审查」工作流，可能下个版本包含此 recipe |
| **安全：CLI 上下文持久化** | #2611（待合并） | 安全审计发现的修复，对于有审批工作流的生产部署至关重要，预计下个版本会优先处理 |
| **Signal 适配器完整支持** | #2744（OPEN）+ #2685（OPEN） | 反应、群组打字指示器等 Signal 专属能力正在补齐，完成后 Signal 将成为全功能通道 |

### 长期路线图信号
- **#1356 记忆系统重设计**：至今未分配或未进入开发阶段，但6个点赞表明用户对记忆扩展性有强烈需求，可能成为 v0.8 或 v0.9 的核心议题。
- **#2742 PR Factory**：若合并，意味着项目正在向「Agent 驱动的 DevOps 工作流」扩展，而不仅仅是聊天机器人平台。

---

## 7. 用户反馈摘要

> **痛点：**  
> - **Issue #2495**（已修复）报告中描述了 `writeOutboundDirect` 只读打开数据库导致命令网关拒绝被完全静默丢弃的严重问题。用户感到“命令没有返回任何响应”（silently drops），这对调试和信任度影响较大。  
> - **PR #2743**（未修复）反映了另一个静默丢消息的 bug：`ncl wirings create` 创建连接后，新的聊天对话中 agent 消息被丢弃。这可能是配置流中的常见陷阱，用户可能不知情地配置失效。

> **使用场景：**  
> - **Issue #1356** 讨论中设想的记忆系统使用场景包括：在 ~54 个文件、83KB 规模下的智能体长期记忆。说明项目正在从小规模个人助手走向具备持续记忆的中型部署。

> **满意点：**  
> - 今日合并的 9 个 PR 中，大部分来自同一个贡献者（gavrielc），且包含详细的需求分析和自用例验证。社区协作效率较高。  
> - **PR #2741** 修复了 setup 流程中“手递手上下文给 Claude 但 Claude 不行动”的问题，解决了用户在安装配置阶段的一个关键交互卡点。

---

## 8. 待处理积压

### ⏳ 长期未响应的关键 Issue/PR

| 编号 | 标题 | 创建时间 | 最后更新 | 天数 | 建议 |
|------|------|----------|----------|------|------|
| **#1356** | Agent memory system redesign | 2026-03-23 | 2026-06-11 | 81 天 | 设计讨论已停滞近3个月，建议维护者组织一次会议或发表 RFC，澄清设计方向 |
| **#2611** | [security] fix(cli): preserve caller context after approval | 2026-05-25 | 2026-06-11 | 18 天 | 安全相关修复，建议优先审查合并，避免上线后出现权限逃逸 |
| **#2685** | docs(signal): group typing, outbound reactions, quote-reply fix | 2026-06-04 | 2026-06-11 | 8 天 | 文档/功能 PR，等待维护者审查已有 8 天，建议合并以解锁 Signal 通道完整能力 |
| **#2744** | fix(signal): deliver agent reactions and forward inbound reactions | 2026-06-11 | 2026-06-11 | <1 天 | 新提交的 Signal 功能修复，建议评估合并顺序 |

### 特别提醒
- **PR #2743**（wirings create 丢消息）：今日刚提交，但问题类型与已修复的 #2495 类似（静默丢数据），建议快速纳入审查队列。
- **PR #2732**（host + agent-runner 安全审计修复）：提交于今日，涉及容器生命周期和 docker kill 回退等多处加固，对于生产部署尤其重要。

---

*报告生成时间：2026-06-12 | 数据来源：[NanoClaw GitHub](https://github.com/qwibitai/nanoclaw)*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NullClaw 项目 2026年6月12日数据生成的日报。

---

## NullClaw 项目动态日报 | 2026-06-12

### 1. 今日速览

- **项目活跃度评估：低**。今日项目整体活跃度较低，无新版本发布，也无新的 Pull Request（PR）提交或合并。
- **社区反馈出现**：社区提交了 1 个关于本地模型与 Ollama 集成的 Bug（Issue #952），指出该功能存在响应不完整的问题，是今日唯一的社区动态。
- **代码库状态稳定**：过去24小时无代码改动被合并，项目处于稳定但稍显停滞的状态。核心功能开发可能进入间歇期，或者团队正在处理更复杂的后台任务。

### 2. 版本发布

**无**

今日无新版本发布。

### 3. 项目进展

**无**

今日无任何 Pull Request 被合并或关闭。项目代码库与昨日相比无实质进展。

### 4. 社区热点

**单一热点：本地模型输出不完整**
- **Issue #952**: `[bug] Local model using ollama returns incomplete answers`
  - **链接**: `nullclaw/nullclaw` Issue #952
  - **摘要**: 用户 `bloodgroup-cplusplus` 报告称，在使用 Ollama 拉取并运行本地模型后，NullClaw Agent 的回复始终不完整（非完整句子）。用户提供了截图尝试复现该问题。
  - **分析**: 这是今日唯一的社区互动。该 Issue 暂无评论和点赞，但与“本地模型”这一核心功能直接相关，是社区对模型集成质量的关键反馈。背后诉求是希望项目在适配主流本地推理框架（如 Ollama）时，能保证基础的响应完整性和可靠性。该问题若得不到及时解决，可能会影响用户对本地部署这一核心特性的信心。

### 5. Bug 与稳定性

**Bug 报告（1项）**

| 严重程度 | 问题描述 | 详情 | 状态 |
| :--- | :--- | :--- | :--- |
| **中等** | 本地模型（通过Ollama）输出不完整 | #952 报告了使用Ollama拉取的模型（如Gemma）时，Agent返回不完整的句子。这可能会导致用户无法正确理解AI的意图或行动结果。 | 待确认，无Fix PR |

### 6. 功能请求与路线图信号

- **无新功能请求**：今日未提交正式的新功能请求（Feature Request）。
- **潜在信号**：Issue #952 虽为 Bug 报告，但背后反映出用户对“本地模型稳定性”和“与Ollama集成完整性”的潜在期待。项目团队若将此 Bug 定性为集成层面的缺陷，修复过程可能会涉及优化token生成逻辑或模型提示词，这可以视为对本地模型模块的一次改进，可能指向下一版本对Ollama支持的完善。

### 7. 用户反馈摘要

- **主要痛点**: 用户在使用顺滑流程（pull model -> start agent）后，发现回答不完整，这是用户体验上的直接打击。这表明当前的Ollama集成存在显性缺陷，影响了对话的可用性。
- **使用场景**: 用户明确展示了对“本地模型”+“Ollama”这一典型本地部署组合的青睐。他选择了Gemma模型，代表了社区对开源可商用模型的偏好。
- **满意程度**: 对该集成功能的当前体验表示**不满意**。问题在创建Issue后仍待解决，用户可能处于等待状态。

### 8. 待处理积压

- **Issue #952 缺乏响应**: 作为24小时内唯一的活跃Issues，目前无维护者回应，也暂无任何人进行标记。尽管问题尚不严重，但长期未响应可能导致用户社区感到被忽视，降低贡献热情。
- **（假设性）**：如果项目此前存在关于“Ollama响应超时”或“流式输出中断”的类似问题，建议维护者优先查看并关联此Issue。目前暂无其他明显的长期积压项。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的IronClaw GitHub数据，生成2026年6月12日的项目动态日报。

---

## IronClaw 项目日报 | 2026-06-12

### 1. 今日速览

今日IronClaw项目活跃度极高，核心团队正全力推进“Reborn”版本的稳定性与功能完善。过去24小时内，社区与核心贡献者提交了47条PR（其中25条已合并/关闭）和30条Issue（其中13条已关闭），显示出项目正在快速迭代。近期工作的重心集中在“Reborn”版本的生产就绪（Production Readiness）上，具体包括：修复了大量UX/UI Bug、完善了Slack集成与路由、强化了自动化测试体系，并开始着手解决长期存在的配置即代码（Configuration-as-Code）问题。项目健康状况良好，正处于关键的“从测试到生产”的冲刺阶段。

### 2. 版本发布

**无**。过去24小时内无新版本发布。

### 3. 项目进展

今日合并/关闭的PR和Issue显示出项目在多条战线上取得了实质性进展，尤其是“Reborn”版本的可用性得到了显著提升。

- **测试体系建设 (QA & E2E):**
    - **PR #4786** 将主分支代码提升至QA分支，为更广泛的测试做准备。
    - **PR #4769** 为`ironclaw-reborn`二进制文件新增了**22个确定性端到端测试**，覆盖5大用例，无需外部服务或API密钥即可运行，极大地提升了自动化回归测试能力。
    - **Issue #4775** 创建了“Reborn的自动化QA”史诗级任务（Epic），规划了从单元测试到现场测试的完整自动化测试路径。

- **Slack集成与核心路由修复:**
    - **PR #4782** 修复了WebUI中的Slack交付默认设置无法生效的问题，根源在于使用了两个独立的`FilesystemOutboundStateStore`实例。现已统一状态存储。
    - **PR #4753** 解决了Slack审批流程中的关键路由问题，现在用户可以直接在Slack线程中回复“approve”来完成审批，无需复杂的绑定流程。
    - **PR #4777** 修复了Slack重新连线的循环问题，现在WebUI会正确反映Slack的连接状态。

- **后端功能修复与增强:**
    - **PR #4784** 修复了当能力（Capability）运行时不可用时，整个代理循环会崩溃的问题。现在会将其作为普通工具失败处理，增强了系统的鲁棒性。
    - **Issue #4771** 作为后续任务，计划为操作员日志添加基于运行/线程的过滤功能，提升调试体验。

- **自动化与流程优化:**
    - **PR #4757** 修复了从“自动化（Automations）”页面点击触发任务（triggered run）导航至聊天页面时出现空白的问题，现在能正确加载。
    - **PR #4780** 引入了外发交付目标（outbound targets）的概念，在创建触发器和例程时向模型提供更明确的指引，避免模型盲目推断支持Slack等外部服务。

### 4. 社区热点

今日最受关注的Issues主要围绕“Reborn”新版本的初体验Bug和用户体验问题。这些讨论反映出社区对新版本抱有很高期望，但同时对于其稳定性和易用性提出了较高要求。

- **`#4703` [Open] NEAR AI模型选择器保存显示名称而非模型ID**: 该问题由社区用户`sunglow666`报告并获得了2条评论。这是一个典型的数据一致性bug，会导致后续推理调用失败。它直接影响了用户配置模型时的核心体验，引起了广泛关注。
    - **链接**: [Issue #4703](https://github.com/nearai/ironclaw/issues/4703)

- **`#4761` [Open] 代理在重复工具失败后停止工作，而非恢复**: 另一个由`sunglow666`报告的高价值反馈，深刻揭示了当前系统在处理错误时的脆弱性。需求是代理应具备更强的容错和自愈能力，而不是遇到失败就挂起，这暴露出当前工作流编排的不足。
    - **链接**: [Issue #4761](https://github.com/nearai/ironclaw/issues/4761)

- **`#4764` [Open] 拒绝Shell审批后工具调用挂起且无用户反馈**: 此问题聚焦于审批流程的交互设计缺陷。当用户“拒绝”一个操作时，系统没有给出清晰的反馈，导致用户无法判断下一步操作。这直接影响了用户对代理行为的可控性和信任感。
    - **链接**: [Issue #4764](https://github.com/nearai/ironclaw/issues/4764)

### 5. Bug 与稳定性

今日报告的Bug主要集中在`Reborn`版本的代理运行逻辑、UI交互和认证/配置上。大部分Bug已有对应的修复PR或正在积极讨论中。

| 严重程度 | Issue ID | 摘要 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **高** | `#4761` | 代理在工具重复失败后停止工作 | Open | 核心能力问题，影响可靠性 |
| **高** | `#4783` | 无凭证的WASM扩展能力调用失败（“network”错误） | Open | 严重阻碍了WASM扩展的使用 |
| **中** | `#4751` | 大请求因代理工具参数超过16384字节限制而失败 | Open | 影响大型应用的构建与使用 |
| **中** | `#4762` | 失败的工具工作流导致后续消息和活动顺序不一致 | Open | 影响对话的连贯性和可预期性 |
| **中** | `#4703` | NEAR AI模型选择器保存显示名称而非模型ID | Open | 已有**PR #4772**进行修复 |
| **低** | `#4759` | 工作空间路径在使用相对路径时出现重复 | Open | 路径处理逻辑问题 |
| **低** | `#4770` | 刷新页面后工具活动可能停止更新（SSE重连问题） | Open | 影响实时性体验，但为偶发问题 |
| **低** | `#4764` | 拒绝Shell审批后工具调用挂起且无用户反馈 | Open | 交互体验问题 |
| **低** | `#4748` | 代码块中的“换行/不换行”切换按钮无效 | Open | 前端UI Bug |

### 6. 功能请求与路线图信号

今日提出的功能请求显示了项目从“能用”向“好用”演进的用户期待。

- **史诗级功能：配置即代码**: 核心开发者`ilblackdragon`提出的**Issue #3036**（`[EPIC] Configuration-as-Code for IronClaw Reborn`）是目前最具有前瞻性的功能请求。它旨在为运营商提供声明式配置能力，解决当前手动编辑分散配置（`.env`、JSON、启动参数）的痛点，为大规模部署和自动化运维铺路。这表明项目已开始在架构层面思考企业级部署的复杂性。
    - **链接**: [Issue #3036](https://github.com/nearai/ironclaw/issues/3036)

- **全局“始终允许”设置**: 用户`think-in-universe`在**Issue #4776**中提出，当前对工具权限的管理过于零散，需要一个全局的“始终允许”开关，以简化高频、可信工具的使用流程。这与`PR #4780`和`#4779`中提出的“外发目标”概念相呼应，都旨在优化模型与外部系统的交互模型。
    - **链接**: [Issue #4776](https://github.com/nearai/ironclaw/issues/4776)

### 7. 用户反馈摘要

从今日的Issue评论和创建语境中，可以提炼出以下用户痛点和使用场景：

- **配置体验差**: 用户普遍反映`Reborn`的初始设置和配置过程令人困惑。`#4683`提到无效配置只给出“驱动不可用”的泛化错误，`#4703`和`#4705`则具体指出了模型选择和SSO配置中的Bug。用户期望更清晰的错误提示和更流畅的引导。
- **稳定性担忧**: 用户`sunglow666`多次报告代理执行中断（`#4761`）、数据一致性（`#4762`）和功能不响应（`#4759`, `#4770`）等问题，表明用户对新版本的稳定性持观望态度。代理在遇到失败后不能自愈让用户感到不放心。
- **缺乏透明度和控制**: `#4764`（拒绝后无反馈）和`#4701`（HTTP请求审批信息不充分）表明用户期望对代理行为有更深入、更透明的控制感。当下的审批流程简单粗暴，缺乏必要的上下文信息。
- **易用性细节待打磨**: `#4750`（工作区文件在UI中不可发现）和`#4748`（代码块换行无效）等小问题暴露了UI/UX在细节层面仍需打磨，以提升日常使用的“顺手”程度。

### 8. 待处理积压

- **长期未响应的CI问题**: **Issue #4108** (`Nightly E2E failed`) 自2026-05-27创建以来，虽由机器人（`github-actions[bot]`）报告，但至今无任何维护者或社区成员评论。这看起来是一个长期的CI稳定性问题，可能被团队视为“常态”而忽略了其信号。需要维护者关注并评估其影响的测试范围，避免潜在的功能回退无人察觉。
    - **链接**: [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

- **长期未合并的重大发布PR**: **PR #3708** (`release`) 自2026-05-16开放至今，是一个包含API破坏性变更（`ironclaw_common`, `ironclaw_skills`）的新版本发布PR。长期未合并会阻塞社区其他开发者的升级路径，并可能导致主分支与发布版本之间的差距越来越大。建议项目维护者评估合并此PR的时机。
    - **链接**: [PR #3708](https://github.com/nearai/ironclaw/pull/3708)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的LobsterAI GitHub数据，我将为您生成一份结构清晰、数据驱动的项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-06-12

### 1. 今日速览

LobsterAI 项目在 **2026-06-11** 的活动中表现出 **高度活跃** 的状态。核心团队在 **24小时内合并了18个PR**，主要集中在 **Cowork 模块的功能增强**（如实时语音输入、上下文压缩优化）和 **系统稳定性修复**（如网关超时、内存泄漏）。新发布的 `Computer Use` 计算机操作功能是一项重大的能力扩展。此外，社区提交的 Issue 反映了对 **多智能体协作**和**Token 使用效率**的持续关注。总体来看，项目在**稳定推进新功能**与**修复技术债务**之间取得了良好平衡。

### 2. 版本发布

- **今日无新版本发布。**

### 3. 项目进展

今日项目向前迈进了重要一步，核心团队高效地合并了多个重要PR，具体表现为：

- **核心功能增强（Cowork 模块）**：
    - **实时语音输入 (Realtime ASR)**：为 Cowork 语音输入增加实时 ASR 模式，通过 WebSocket 流式传输音频并实时回填识别文本，显著提升了语音交互体验。（#2148）
    - **上下文连续性优化**：改进了 OpenClaw 压缩聊天历史后的上下文连续性，通过新增 `LobsterAI` 所有的连续性层，使智能体能在历史压缩后更可靠地继续执行任务。（#2145）
    - **启动与超时问题修复**：修复了用户停止消息时，已停止的启动轮次仍会发送消息的问题（#2147）；并解决了在部分网关上模型同步超时（30s → 90s）的问题，提升了多模型环境下的稳定性。（#2152）
- **重大能力扩展**：新增了 **Computer Use MVP**。这是一个内置的“计算机使用”套件，允许智能体通过内置 MCP 服务器与 Windows 桌面应用交互（如启动应用、截图、输入文字、点击等），将 AI 能力从对话框扩展到操作系统层面。（#2143）
- **新功能特性**：
    - **HTML分享方式选择**：支持用户在创建HTML分享时选择“分享码”或“公开访问”模式，并支持对已分享内容更新访问方式，提升了内容分享的灵活性。（#2146）
    - **文件分享能力**：为项目增加了文件分享的基础能力。（#2151）
- **Bug 修复与稳定性**：
    - **修复 OpenClaw 内存溢出**：为 OpenClaw 网关进程设置了明确的 V8 旧生代空间上限，减少了长时间、多频道运行场景下的 OOM（内存溢出）崩溃。（#2149）
    - **修复 NSIS 安装器与引擎加载页**：修复了 Windows 平台安装器（NSIS）的破坏性初始化问题，并重新设计了引擎加载页面。（#2142）
    - **修复认证门户链接**：更新了门户回退和升级链接，指向新的 LogsterAI 门户域名。（#2144）

### 4. 社区热点

- **最受关注的 Issue**：
    - **[#1462 [OPEN] 许愿：期望每个agent能够单独绑定模型、期望有正式的多agent协作能力](https://github.com/netease-youdao/LobsterAI/issues/1462)**：尽管是4月初的“老”Issue，但在6月11日仍有更新，且拥有2条评论。用户对“每个Agent可单独绑定模型”和“多Agent小组协作”的呼声很高，这表明社区对 **更精细化的模型管理和高级的多智能体编排** 有强烈需求。
    - **[#2121 [OPEN] 对一个现象的疑问（怀疑是bug）](https://github.com/netease-youdao/LobsterAI/issues/2121)**：用户报告了AI回复重复文字的现象，并担心这会造成Token浪费。这反映了社区对 **成本意识和模型输出质量** 的敏感度较高。

**诉求分析**：上述Issue揭示了社区的深层需求已从单一聊天功能，转向 **企业级/创作级应用**：用户希望像管理团队一样管理Agent，并追求更高的效率和成本控制。

### 5. Bug 与稳定性

- **严重程度：中**
    - **[Issue #2121] [OPEN] 回复重复文字现象**：用户怀疑是Bug，可能导致Token浪费。目前无PR关联，但结合今日合并的多个Cowork修复，推测项目团队正在重点优化模块的稳定性和输出质量。（[链接](https://github.com/netease-youdao/LobsterAI/issues/2121)）

- **已修复**：
    - **网关超时导致消息丢失**：`#2152` 已修复，将预发送模型同步超时从30秒延长至90秒。
    - **OpenClaw 服务进程 OOM 崩溃**：`#2149` 已修复，显式设置进程堆内存上限。
    - **启动停止竞态条件**：`#2147` 已修复，防止停止操作后仍发送消息。
    - **知识套件UI问题**：`#2150` 已修复，确保专家套件（Expert Suite）的控件保持粘性（固定定位），避免滚动时消失。

**总体趋势**：开发团队在今日投入了大量精力修复与 **Cowork 模块核心稳定性** 相关的 bug，这对提升长期运行和复杂任务的可靠性至关重要。

### 6. 功能请求与路线图信号

- **高可能性被纳入**：
    - **多Agent协作**：Issue `#1462` 请求的“多agent小组/房间模式”是社区的热门需求。结合今日合并的 `Computer Use` 和 `ASR` 等复杂能力，可以预见 LobsterAI 正在构建一个更强大的 Agent 编排平台，多Agent协作很可能是下一阶段的重点路线图。
    - **HTML分享功能**：`#2146` 的合并表明团队正在系统性地构建内容分享生态，从“分享码”到“公开访问”的切换是这一趋势的明确信号。
- **可能性中等**：
    - **单Agent绑定模型**：同样是 `#1462` 提出的需求。当前项目通过 `area: main` 和 `area: renderer` 协同工作，实现模型级别的独立配置技术上是可行的，但优先级可能低于多Agent协作。

### 7. 用户反馈摘要

- **正面/积极**：
    - 用户 `orion0608` 在 Issue `#1462` 中明确表示 LobsterAI 的“同IM渠道多实例”功能很实用，并认可其交互体验优于竞争对手（如阿里Hiclaw）。
    - 今日大量快速合并的PR，特别是 `Computer Use` 这样的重磅功能，间接反映了团队对用户需求（自动化、效率）的积极响应。

- **负面/痛点**：
    - **Token浪费焦虑**：用户 `nbjoe` 在 Issue `#2121` 中明确表达了对AI重复回复导致Token浪费的担忧，这是C端用户在成本感知上的一个普遍痛点。
    - **功能缺失**：用户 `orion0608` 的“许愿”贴体现了当前版本在“精细化Agent管理”和“高级协作”能力上的不足。

### 8. 待处理积压

- **需重点关注的老Issue**：
    - **[#1462 [OPEN] [stale] 许愿：期望每个agent能够单独绑定模型、期望有正式的多agent协作能力](https://github.com/netease-youdao/LobsterAI/issues/1462)**
        - **创建时间**：2026-04-04
        - **状态**：`stale`，但近期有更新
        - **建议**：尽管标为 `stale`，但其内容与项目当前展示的Agent能力扩展方向高度相关。项目维护者可以考虑发起一个社区讨论或发布一个RFC（征求意见稿），以明确多Agent协作的规划路线图，安抚期待已久的用户。

- **需关注的老PR**：
    - **[#1459 [OPEN] [stale] feat(skills): 技能 hover 时展示完整描述 Tooltip](https://github.com/netease-youdao/LobsterAI/pull/1459)**
        - **创建时间**：2026-04-03
        - **状态**：`stale`，已详细描述实现方案
        - **建议**：这个PR已经提供了完整的技术方案（`SkillTooltip.tsx`），是一个对用户体验有明显提升的非侵入式改进。建议维护者尽快Review并合并，以解决技能描述“截断看不清”的长期痛点。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报（2026-06-12）。

---

# Moltis 项目动态日报 | 2026-06-12

## 1. 今日速览

今日项目活跃度处于**正常偏低**水平。过去24小时内，社区提交了1个关于Fastmail MCP授权的新Bug报告，同时有一项针对WhatsApp消息投递问题的修复 PR 被提交。没有新版本发布。整体来看，项目在细节修复和问题排查上有所进展，但缺少重大功能合并或里程碑推进。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无已合并或关闭的重要 PR。社区提交了一个关键的 PR，标志着项目在 WhatsApp 集成稳定性上的主动改进：

- **PR #1116**：修复了WhatsApp聊天中，当发送者开启了隐私功能（`@lid` 聊天）时，智能体回复消息被静默丢弃的问题。此前，消息能在UI中显示，但无法到达用户手机。该PR通过重写Push Notification (PN) JID确保消息投递。该PR目前处于等待审核合并状态。
  - [查看PR](https://github.com/moltis-org/moltis/pull/1116)

## 4. 社区热点

今日唯一活跃的讨论集中在 **Bug Issue #1115** 上。该问题涉及 Fastmail MCP 授权认证失败，虽然仅有1条评论和1位作者，但作为新报告，它获得了高度关注。
- **核心诉求**：用户在使用Fastmail MCP（可能指邮件服务）时遇到授权流程障碍，导致无法正常使用与邮件相关的AI功能。这表明集成的第三方服务认证逻辑可能存在兼容性或配置问题。
- [查看Issue](https://github.com/moltis-org/moltis/issues/1115)

## 5. Bug 与稳定性

今日报告的Bug严重程度为**中等**，暂未发现崩溃或回归问题。

- **[中] 集成认证故障：** **Issue #1115** 报告 Fastmail MCP 授权失败。这可能导致用户无法使用邮件智能体或相关功能。目前尚无关联的修复PR。
  - [查看Issue](https://github.com/moltis-org/moltis/issues/1115)

- **已提交修复：** 今日**未关闭**任何Bug，但 **PR #1116** 针对的是“消息投递丢包”的隐式Bug（用户可能无法察觉但在日志中表现为无送达回执），该问题已被开发者定位并修复。

## 6. 功能请求与路线图信号

今日未发现明确的新功能请求。但从提交的修复 PR 可以管窥项目对**消息投递可靠性**和**隐私保护兼容性**的持续投入，这可能是短期路线图上的重点之一。

## 7. 用户反馈摘要

今日反馈数量有限，主要来自 Issue 报告：
- **用户痛点**：用户对 Fastmail 集成授权受阻感到困扰（Issue #1115）。另外，在WhatsApp隐私模式下，智能体回复的静默丢失对用户而言是糟糕的体验（PR #1116 所解决的问题）。
- **使用场景**：用户正在尝试将Moltis接入其Fastmail邮箱，或在WhatsApp中与智能体进行私密对话。

## 8. 待处理积压

今日无长期未响应的重要Issue或PR。所有待处理项（1个Bug和1个PR）均为24小时内创建的最新内容。

---
*报告生成时间: 2026-06-12 UTC*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的CoPaw项目数据，我为您生成了以下项目动态日报。

---

# CoPaw 项目动态日报 | 2026-06-12

## 1. 今日速览

今日CoPaw项目处于**高活跃度**状态，社区贡献与问题反馈非常密集。24小时内共产生33条Issue更新和42条PR更新，并发布了两个补丁版本。项目核心开发工作聚焦于**Runtime 2.0架构重构**和**Agent OS Driver统一抽象层**等重大特性，同时社区用户反馈了大量关于**桌面客户端稳定性**（SSL错误、进程溢出、卡顿）和**UI/UX体验**（附件下载、记忆搜索展示）的问题。新版本v1.1.11.post2快速响应并解决了一部分回归Bug，但仍有多个关键问题待解决。

## 2. 版本发布

今日发布了两个补丁版本，主要聚焦于小范围修复。

- **v1.1.11.post2**: 该版本主要包含一个UI样式修复，将工具卡片标题截断为单行并显示省略号（`ellipsis`），优化了界面显示效果。
    - **更新内容**: `style: truncate tool card titles to single line with ellipsis`
    - **注意事项**: 不包含破坏性变更，为常规补丁升级。

- **v1.1.11.post1**: 该版本主要为版本号变更，并回滚了一个导致问题的修复（`Revert "fix(pack): compile-check discord after conda-unpack"`）。
    - **更新内容**: `chore: bump version`， `Revert fix`
    - **迁移注意事项**: 建议用户直接升级至最新的`v1.1.11.post2`版本。

## 3. 项目进展

今日合并/关闭了多个重要PR，标志着项目在稳定性和功能完整度上取得进展：

- **桌面端稳定性增强**: PR #5125 `fix(desktop): harden Tauri Windows CI against crates.io fetch failures` 通过优化CI流程，增强了Windows桌面客户端的构建可靠性，间接解决了因依赖下载失败导致的构建/启动问题。
- **重大架构设计讨论**: PR #5088 `feat: initial governance & sandbox interface disscussion` 被合并或进行了关键讨论，标志着项目开始探索沙盒与治理接口，为未来更安全的Agent执行环境打下基础。
- **安全问题修复**: PR #5028 `fix(security): isolate keychain master key per install` 合并了关于隔离Keychain主密钥的修复，提升了不同安装实例间的凭证安全性，这是一个重要的安全改进。
- **UI与国际化改进**: 合入了多个“first-time-contributor”的PR，如PR #5133 `feat(ui): apply AionUi design language to Console layout`（视觉语言升级）和PR #5136 `feat(i18n): tradução pt-BR completa do workspace QwenPaw`（葡萄牙语本地化），表明项目社区生态活跃，且在持续优化用户体验和全球化的覆盖面。

## 4. 社区热点

今日讨论最热烈的议题集中在**桌面客户端稳定性问题**和**新功能需求**。

1.  **Issue #5106**: `[Bug]: 新版Tauri端SSL证书错误+无限进程占满内存致黑屏；旧版PyInstaller端也无法正常启动`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/issues/5106](https://github.com/agentscope-ai/QwenPaw/issues/5106)
    - **分析**: 该Issue获得7条评论，反映了部分Windows用户在升级新版后遇到的**严重崩溃问题**（内存耗尽、黑屏），且回退旧版也无法使用，是当前最紧急的稳定性问题。用户期望能尽快修复。

2.  **Issue #5064**: `[Bug]: 由agent生产的定时任务, 无法正常触发`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/issues/5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)
    - **分析**: 8条评论，表明Agent自主生成的定时任务功能存在重大缺陷，任务无法触发且无法编辑。用户对Agent的“自动化”能力提出了根本性质疑。

3.  **Issue #5086**: `[Bug]: OpenSSL 3.5 回归 bug 导致 Desktop 无法启动`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/issues/5086](https://github.com/agentscope-ai/QwenPaw/issues/5086)
    - **分析**: 该Issue精确定位了桌面端无法启动的根因为OpenSSL 3.5的回归Bug，展现了社区用户的技术深度。虽已关闭，但其根因分析与前面#5106问题高度相关，可能是同一问题在不同环境下的表现。

## 5. Bug 与稳定性

今日报告的Bug主要集中在**桌面端崩溃**、**新版本功能回归**和**配置持久化**三个方面。

| 严重程度 | Issue # | 描述 | 状态 | Fix PR 关联 |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) | 新版Tauri桌面端SSL证书错误+无限进程导致内存耗尽/黑屏 | **开放** | 无 |
| **Critical** | [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) | Windows客户端进程持续增加，内存占用90%+ | **开放** | 无 |
| **High** | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | v1.1.11.post2 附件下载错误，`docx/pdf`等报错404 | **开放** | 无 |
| **High** | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | v1.1.9/1.1.10连接本地千问3.6模型后对话无响应 | **已关闭** | 可能已在后续版本修复 |
| **Medium** | [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | OpenSSL 3.5回归bug导致桌面端无法启动 | **已关闭** | 社区已定位 |
| **Medium** | [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) | “记忆搜索”工具在UI上的搜索结果展示为空/错误 | **开放** | 无 |
| **Low** | [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) | 向量模型配置在未展开卡片时保存会丢失 | **开放** | 无 |

## 6. 功能请求与路线图信号

社区对功能的期待非常广泛，部分需求与正在开发中的PR高度吻合。

- **高优先级信号**:
    - **对话队列与Token统计**：Issue #5103 提出引入类似“openclaw”的输入队列和Token统计功能。PR #5130 `feat(chat): add per-turn token and context usage popover` 已开放，正好对应了Token统计需求，**极有可能被纳入下一个版本**。
    - **引用/回复功能**：Issue #5110 期望增加类似Perplexity的“引用文本进行追问”功能，表明用户有更深度的对话交互需求。

- **中期路线图信号**:
    - **Agent团队协作(Swarm)**: Issue #5139 请求原生支持多Agent团队协作，类似于WorkBuddy专家团队。
    - **上下文压缩优化**: Issue #5063 建议集成Headroom做上下文压缩；Issue #5122 提出了上下文压缩统计数据与实际不一致的问题。这表明在“节省Token”这一核心痛点上有强烈社区声音。
    - **Agent OS Driver**: PR #5067 `feat(driver): introduce Agent OS Driver` 正处于开发审查中，旨在统一MCP/A2A/ACP等外部能力，这将是项目架构演进的重大方向。

## 7. 用户反馈摘要

从今日的Issue和评论中，可以提炼出以下几点用户核心反馈：

- **痛点：桌面版稳定性是首要问题**。多位用户报告了Windows桌面客户端无法启动、死机、内存溢出的“灾难级”问题，严重影响了正常使用。用户对新版Tauri客户端的质量表示担忧。
- **痛点：新版本UI变动带来的“不习惯”和“倒退”**。更新至v1.1.11后，用户抱怨附件无法下载（#5102, #5140）、模型选择器缺少Ollama选项（#5108）、记忆搜索展示错误（#5098）等，感觉是新UI的Regression。
- **诉求：Agent自动化能力需要加强**。Agent创建的定时任务无法正常工作（#5064），并且Agent ReAct循环中的可观测性（Langfuse trace）是碎片化的（#5127），这表明Agent自动化流程的可靠性和监控能力是用户非常看重的。
- **满意：社区响应速度快**。用户反映的“附件下载”问题在v1.1.11.post1/post2版本中有所修复（尽管仍有残留问题），说明项目组在快速响应。

## 8. 待处理积压

以下为长期未响应或可能被忽视的重要问题，提醒维护者关注：

1.  **Issue #4727**（开放/9评论）: `[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/issues/4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)
    - **分析**: 这是社区提出的、也是项目自身规划的**重大架构升级**。虽然有PR #5078 (Runtime 2.0) 在推进，但原Issue已开放超过两周，需项目维护者给出更明确的迁移时间表和影响评估。

2.  **PR #4622**（开放/Under Review）: `plugin(datapaw): add data-analysis plugin with 12 BI skills`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/pull/4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)
    - **分析**: 这是一个非常有价值的插件PR，但已开放超过三周，且处于“正在审查”状态。应加快审查进度，以丰富项目的生态能力，并为“Agent OS Driver”等新架构提供实践案例。

3.  **Issue #3817**（已关闭/5评论）: `[Question]: 新版本长期记忆向量模型设置配置失效`
    - **链接**: [https://github.com/agentscope-ai/QwenPaw/issues/3817](https://github.com/agentscope-ai/QwenPaw/issues/3817)
    - **分析**: 虽然已关闭，但该问题指出的“重启后配置丢失”的根因（启动初始化覆盖）是**架构性bug**。今日又出现类似的配置丢失问题(#5137)，表明该根因可能未彻底修复。维护者应重新审视该问题的修复方案，确保不再复发。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的ZeroClaw项目数据，生成2026年6月12日的项目动态日报。

---

# ZeroClaw 项目日报 | 2026-06-12

## 1. 今日速览

ZeroClaw 社区在 v0.8.0 大版本发布后进入密集的修补与功能完善期。过去24小时，项目呈现 **高活跃度**：共有50个Issues和50个PR被更新，其中不乏影响用户工作流的S1级严重性Bug。尽管昨日无任何Issue被关闭，但有2个关键PR被合并，表明维护团队正在积极解决构建和配置持久化等紧迫问题。社区讨论焦点集中在**多Agent交互**（如Delegate代理模式）、**模型兼容性**（特别是Gemini和Anthropic）以及**工具（MCP/Shell）的执行安全与拦截**上。

## 2. 版本发布

### v0.8.0 正式版发布

一个里程碑式的大版本。核心亮点是一个守护进程（Daemon）现在可以运行多个命名Agent，每个Agent拥有独立的工作空间、内存、模型提供商、安全策略、通信渠道和人格。这一切由一个重写的配置Schema进行协调，并支持自动迁移先前版本的配置。

- **发布链接**: [v0.8.0 Release](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.8.0)
- **主要新特性**:
    - **多Agent支持**: 单Daemon多实例，每个Agent配置完全独立。
    - **重写配置Schema**:
        - 引入强类型别名条目。
        - 支持`providers`, `agents`, `channels`等条目的级联删除。
    - **安全与工具增强**:
        - 改进了`risk_profile`配置的解析和应用。
        - 强化了`delegate`代理模式的权限检查。
- **破坏性变更 / 迁移注意**:
    - **配置格式变更**: 旧版本的配置文件不会被丢弃，但需要进行一次性的自动迁移。建议用户备份配置后，运行 `zeroclaw config migrate` 进行升级。
    - **API路由更新**: Gateway API的部分端点（如管理排程任务）已更新，可能需要更新您的集成脚本。Issue #6891 正是由于UI未适配新版API导致编辑失败。
    - **默认超时/预算调整**: 上下文窗口默认预算（`max_context_tokens=32000`）在复杂场景下可能不足（见Issue #5808）。用户可能需要根据自身系统提示和工具数量进行调整。

## 3. 项目进展

过去24小时内，有2个关键PR被合并，解决了发布构建和配置编辑的关键问题：

- **PR #7520 (已关闭/合并)**: **fix(ci): install cross g++ for ARM glibc release builds**
    - **内容**: 修复了在ARM架构（`aarch64`, `armv7`）上使用glibc的Release构建失败的问题，确保v0.8.0版本能正确分发到所有支持的平台。
    - **链接**: [PR #7520](https://github.com/zeroclaw-labs/zeroclaw/pull/7520)

- **PR #7519 (已关闭/合并)**: **fix(config): persist [[mcp.servers]] per-field edits via natural-key dirty-path walker**
    - **内容**: 修复了MCP服务器配置在逐个字段编辑后无法正确持久化到磁盘的问题。这是个重要的稳定性修复，解决了用户自定义MCP配置丢失的潜在隐患。
    - **链接**: [PR #7519](https://github.com/zeroclaw-labs/zeroclaw/pull/7519)

此外，PR #7522 (修复二进制文件读取问题) 和 PR #7517 (修复子Agent会话继承问题) 也已提交，正处于审查或待合并状态，表明项目在快速回应用户反馈。

## 4. 社区热点

社区讨论最激烈的议题集中在两个核心领域：**AI行为逻辑** 和 **工具系统冲突**。

- **热点 Issue #7470: [Bug]: delegate agentic mode rejects empty risk_profile.allowed_tools...**
    - **热度**: 7条评论，尽管是昨日创建，但迅速成为焦点。
    - **诉求**: 用户 `vrurg` 在构建复杂的多Agent协作工作流（如代码审查、研究报告）时，发现 `delegate` 代理模式存在严重的权限门控Bug。当目标Agent的`risk_profile.allowed_tools`为空时，委托会直接失败；同时，使用同一个`risk_profile`的文件门控会阻止访问权限更严格的子Agent。这直接 **阻塞了多Agent协作的核心功能**。
    - **链接**: [Issue #7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **热点 Issue #5849: [Feature]: Dream Mode — Periodic Memory Consolidation & Reflective Learning**
    - **热度**: 17条评论，历史最高。社区对这一“梦境模式”的讨论非常激烈。
    - **诉求**: 建议引入一个在Agent空闲时运行的轻量级后台进程，用于整合日常记忆、反思近期交互并更新长期知识。这反映了用户对Agent更类人、更智能的记忆管理能力的渴望，旨在解决长期对话中上下文窗口和记忆碎片化的问题。
    - **链接**: [Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)

## 5. Bug 与稳定性

昨日报告的Bug数量众多，且严重性极高。以下按严重程度排列：

| 严重程度 | Issue ID | 标题摘要 | 说明 | 是否有Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **S0 - 数据丢失/安全风险** | [#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) | consecutive OOM in wsl2 | 在WSL2上连续内存溢出导致进程被系统杀死，可能导致数据丢失。 | 无 |
| **S1 - 工作流阻塞** | [#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470) | delegate agentic mode rejects empty risk_profile... | **核心的多Agent委托功能被阻塞。** | 无 |
| **S1 - 工作流阻塞** | [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | Default 32k context budget exceeded on iteration 1 | 默认上下文窗口在第一轮LLM调用时就超出预算，导致每轮都触发预裁剪，使得Agent无法正常工作。 | 无 |
| **S1 - 工作流阻塞** | [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | context_compression drops assistant(tool_calls)... | 上下文压缩器丢数据，导致兼容OpenAI的提供商（如MiniMax）工具循环报错。 | 无 |
| **S1 - 工作流阻塞** | [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) | Shell tool calls refused at autonomy level = "full" | 即使在完全许可模式（`autonomy level="full"`）下，Shell工具也无法调用。 | 无 |
| **S1 - 工作流阻塞** | [#6678](https://github.com/zeroclaw-labs/zeroclaw/issues/6678) | Skill tools rejected by Anthropic API | 自定义Skill工具因命名规则（包含`.`）导致Anthropic API返回400错误。 | 无 |
| **S1 - 工作流阻塞** | [#6891](https://github.com/zeroclaw-labs/zeroclaw/issues/6891) | Scheduled Jobs edit error API 422 | 从Dashboard编辑排程任务返回422错误，因为UI表单没有适配v0.8.0的新API。 | 无 |

**总结**: 当前Bug集中爆发于新版本的 **配置适配**、**高级或多Agent工作流** 以及 **特定模型提供商兼容性**。这些Bug对依赖核心功能（如委托、Shell执行、排程任务）的用户有致命影响。

## 6. 功能请求与路线图信号

社区新提出的功能请求显示出对未来Agent自主性和系统可观测性的期待。

- **[潜在下一版本] Issue #5849 (Dream Mode)**: “梦境模式”是社区呼声最高的功能。虽然非常超前，但它代表了AI Agent的下一个进化方向。如果其价值被认可，可能会作为v0.9.0或v1.0的核心特性被纳入路线图。
- **[路线图方向] Issue #6346 & #6390 ([Feature]: node CLI + remote daemon registration)**: 这两项功能旨在将ZeroClaw从单机工具扩展为一个多机、分布式的Agent集群。这表明项目方已有更宏大的架构演進规划，Dashboard节点管理和CLI注册功能是第一步。
- **[功能补全] Issue #6914 (feat: enforce allowed_tools in main loop)**: 和前面的Bug #7470类似，用户希望在所有代码路径上强制执行工具的允许/拒绝列表，而不仅仅是在UI层面过滤。这是对**安全模型实施一致性的强烈需求**。

## 7. 用户反馈摘要

从最新的Issues评论中，我们可以提炼出用户的真实反馈：

- **痛点: 多Agent协作成本高**：
    > “Delegating from one agent to an **agentic** target fails when the target's ... is empty.” — *vrurg (Issue #7470)*
    > 用户尝试构建“研究者-审查者-发布者”的多Agent流水线，但被Bug和复杂的权限配置卡住。这表明项目虽然有雄心，但在易用性和可靠性上仍有巨大提升空间。

- **痛点: 默认配置不适用于复杂场景**：
    > “With the default `agent.max_context_tokens = 32000`, the **first** LLM iteration... already exceeds budget by ~3.3x” — *JordanTheJet (Issue #5808)*
    > 这说明默认值的设定未能充分考虑到用户实际使用的系统提示和工具数量。用户需要更智能的上下文管理，而不是“一刀切”的限制。

- **亮点 / 功能满意**:
    > 来自 Issue #6760 ([Feature]: Update Documentation for Docker) 的评论展示了用户愿意花时间编写并分享Docker配置YAML，这一方面体现了社区的活跃和互助精神，另一方面也暗示官方在Docker化部署方面的文档指引仍需加强。

- **改进建议: 更细致的权限控制**:
    > 多个Issues (如 #7470, #6914, #6434) 都围绕`allowed_tools`, `risk_profile`, `autonomy` 等安全权限配置展开。用户认为当前的权限系统过于“全有或全无”，希望在“完全允许”和“完全禁止”之间有更细粒度的控制，例如基于路径、命令或工具的临时审批机制。

## 8. 待处理积压

以下Issue和PR长期未得到维护团队的官方回复或更新，可能造成用户困惑或社区贡献者流失。

- **Issue (长期不更新)**:
    - **#5542 (OOM in WSL2)**: 严重程度S0，但处于 `r:needs-repro` 状态且自4月9日创建以来没有更新。对WSL2用户影响极大。
    - **#5903 (MCP stdio child process leak)**: 严重Bug，自4月19日创建后未被标记为`in-progress`，也未有官方回复。
- **PR (需要作者或维护者行动 - `needs-author-action`)**: 这批PR堆积严重，涉及多个核心组件（cron, providers, skills），拖久了会增加合并冲突风险，并打击外部贡献者积极性。
    - **#5516** (fuzz targets)
    - **#5661** (cron delivery flags)
    - **#5892** (providers/runtime blockers)
    - **#6038** (cron lock)
    - **#6085** (config defaults)
    - **#6143** (universal skill registry) - XL size
    - **#6190** (OTel spans)
    - **#6230** (cron whatsapp delivery)
    - **#6288** (systemd unit name)
    - **#6303** (Gemini turn order fix)
    - **#6318** (compaction hook)
    - **#6362** (context compressor)

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*