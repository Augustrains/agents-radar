# OpenClaw 生态日报 2026-06-10

> Issues: 452 | PRs: 492 | 覆盖项目: 13 个 | 生成时间: 2026-06-10 02:03 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的OpenClaw项目2026年6月10日的数据，我为您生成了以下项目动态日报。

---

## OpenClaw 项目动态日报 | 2026年6月10日

### 1. 今日速览

今日OpenClaw项目社区活跃度极高，呈现出“高产出、高关注”的态势。过去24小时内，项目处理了452条Issue和492条Pull Request（PR），显示出强大的社区协作能力。**核心关注点集中在稳定性与安全性**，大量Issue与PR聚焦于修复“消息泄露”、“会话挂起”和“性能回归”等关键问题。同时，项目发布了两个新版本，重点优化了QQ机器人（QQBot）和MCP工具的执行结果。整体来看，项目正处于密集迭代和修复阶段，对Bug的响应速度较快，但许多高优先级议题仍处于等待决策或审查状态，需核心团队加强推进。

### 2. 版本发布

项目在今日发布了两个版本，核心修复内容一致，具体如下：

*   **v2026.6.5 (稳定版) & v2026.6.5-beta.6 (测试版)**
    *   **发布说明**: [查看详情](https://github.com/openclaw/openclaw/releases)
    *   **核心更新**:
        1.  **QQ机器人改进**: 修复了模型在回复时可能将内部推理/思考过程（`<thinking>`标签）泄露到群聊或频道的问题，确保了对外输出的信息纯净。
        2.  **MCP工具结果格式化**: 增强了对MCP工具返回结果的处理能力，现在会强制转换`resource_link`、`resource`、`audio`等资源类型为正确格式，并修复了对格式异常图片的处理。
    *   **破坏性变更**: 无明确声明的破坏性变更。
    *   **迁移注意事项**: 尽管无破坏性变更，但QQBot用户务必更新并验证消息内容是否被正确过滤。MCP工具的开发者应检查新版本对资源处理逻辑的变更，确保工作流兼容。

### 3. 项目进展

过去24小时内，共合并/关闭了137个PR，主要进展包括：

*   **会话稳定性提升**: PR [#91801](https://github.com/openclaw/openclaw/pull/91801) 修复了会话挂起后恢复的问题，确保在运行被中止后，会话通道能被正确释放。
*   **消息传递可靠性增强**: PR [#91803](https://github.com/openclaw/openclaw/pull/91803) 为iMessage频道增加了远程媒体暂存功能，避免了在插件分发前的路径问题。PR [#91674](https://github.com/openclaw/openclaw/pull/91674) 修复了后台执行事件因心跳冷却机制而被丢弃的问题，确保用户能收到所有后台任务的完成通知。
*   **配置文件与系统集成**: PR [#89858](https://github.com/openclaw/openclaw/pull/89858) 修复了systemd单元的服务范围冲突，解决了在用户和系统范围同时安装时Gateway启动可能失败的问题。
*   **Bug修复与边缘情况处理**: PR [#91796](https://github.com/openclaw/openclaw/pull/91796) 扩展了模型目录，加入了对 Claude Haiku 4.5 的支持。PR [#91794](https://github.com/openclaw/openclaw/pull/91794) 修复了当心跳功能被禁用时，单次定时任务被错误标记为“跳过”的问题。

总体来看，项目在修复用户报告的各类Bug上投入了大量精力，尤其是围绕会话管理、消息传递和系统集成的稳定性问题。

### 4. 社区热点

*   **讨论最激烈**: **Issue #25592**: “工具调用间的文本泄露到消息频道”。
    *   [链接](https://github.com/openclaw/openclaw/issues/25592)
    *   **诉求**: 这是社区长期关注的核心UX问题。当Agent在调用多个工具之间产生了内部处理文本（如错误处理、状态更新），这些本应隐藏的文本会错误地发送到Slack、iMessage等外部频道，对用户造成严重信息干扰。该Issue已累计29条评论，被标记为P1（高优先级）和“钻石龙虾”评级，虽有部分修复PR，但根源问题仍未彻底解决。

*   **回归问题高度关注**: **Issue #88312**: “2026.5.27版本：Codex服务端的回合完成确认回归”。
    *   [链接](https://github.com/openclaw/openclaw/issues/88312)
    *   **诉求**: 用户报告从2026.5.27版本开始，一个已被修复的回归问题再次出现，导致多工具代理任务频繁失败，并显示“Codex stopped before confirming the turn was complete”错误。此问题严重影响使用ChatGPT Plus（Codex）服务的用户，反映了回归测试流程可能存在漏洞。

### 5. Bug 与稳定性

今日报告的Bug和稳定性问题主要集中在以下几个方面，按严重程度排列：

| 严重程度 | 问题摘要 (Issue #) | 是否有 Fix PR | 备注 |
| :--- | :--- | :--- | :--- |
| **高** | [Bug]: Codex应用服务端回合完成确认再次回归 (#88312) | PR [#91590](https://github.com/openclaw/openclaw/pull/91590) 尝试修复 | 严重影响依赖Codex服务的用户，属于回归问题。 |
| **高** | [Bug]: 运行时发生 `EmbeddedAttemptSessionTakeoverError` 错误，导致Discord会话失败 (#86508) | PR [#91797](https://github.com/openclaw/openclaw/pull/91797) 提出方案 | 影响Discord频道使用体验，导致回复被撤回。 |
| **中** | [Bug]: Gateway堆内存随时间无限增长，在长期运行后因OOM被杀死 (#89315) | 暂无明确Fix PR | 对服务器部署的稳定性构成严重威胁，可能导致服务中断。 |
| **中** | [Bug]: 会话写锁超时阻塞子代理交付通道 (#86538) | PR [#91802](https://github.com/openclaw/openclaw/pull/91802) 尝试修复 | 导致多会话、多代理场景下的消息丢失或延迟。 |
| **中** | [Bug]: WhatsApp长模型调用后会话挂起 (#84569) | PR [#91800](https://github.com/openclaw/openclaw/pull/91800) 部分相关 | 影响WhatsApp用户的长查询体验，可能导致回复永不送达。 |

### 6. 功能请求与路线图信号

*   **高优先级功能**: **Issue #48003**: “Steer模式无法在会话中注入消息”。这个问题非常关键，直接关系到“交互式控制”的用户体验。虽有PR关联，但被标记为“钻石龙虾”级别，说明实现复杂且影响广泛。
*   **用户强烈呼吁**: **Issue #42840**: “为控制UI添加MathJax/LaTeX支持”。该请求获得6个👍，显示用户对数学公式展示有强烈需求，尤其是在学术和科研场景下。
*   **路线图信号**: **PR #81851**：`claude-cli-interactive`后端。虽然该PR状态为“需要证据”，且规模庞大，但它代表了社区对让Claude在本地运行并实现交互式流式推理的强烈探索意愿，这可能是未来Agent发展的重要方向。

### 7. 用户反馈摘要

*   **主要痛点**: 用户普遍对“消息泄露”问题感到困扰，包括内部思考过程（Issue #25592）、工具调用痕迹（Issue #44905）和错误信息（Issue #39406）泄露到公共频道，这严重影响了Bot的专业形象和用户体验。
*   **部署与兼容性**: Docker用户报告了容器内沙箱权限问题（Issue #31331），Linux用户遭遇了systemd服务冲突（PR #89858），RISC-V架构用户也遇到了兼容性问题（Issue #54253），表明项目在非标准环境下的部署仍有待优化。
*   **配置与预期不符**: 多个用户反映配置文件行为与预期不符，如`auth.order`选项被忽略（Issue #46031）、`XDG_CONFIG_HOME`变量未生效（Issue #53628），以及变更HOME路径导致配置丢失（Issue #54634），这增加了用户的使用成本和学习曲线。
*   **正面反馈**: 用户对项目的“高效”和“强大功能”表示认可（Issue #54253），对新特性如 `claude-cli-interactive`（PR #81851）表现出浓厚兴趣，反馈社区创新活力强。

### 8. 待处理积压

*   **高优先级长期待处理问题**:
    *   **Issue #25592** (P1, 钻石龙虾): 工具调用间文本泄露。问题已存在超3个月，至今无彻底解决方案，是社区呼声最高的待解决问题之一。
    *   **Issue #44905** (P1, 钻石龙虾): Discord泄露内部工具调用痕迹。与#25592类似，是另一个关键的“消息泄露”问题。
    *   **Issue #31331** (P1, 钻石龙虾): Docker环境下的工作空间访问问题。这是Docker用户的核心阻碍，涉及安全与权限，但积压超过3个月。

*   **长期未更新的PR**:
    *   **PR #81851**: `claude-cli-interactive`后端。该PR自5月14日提出后，虽有更新但状态始终为“需要证据”，核心维护者尚未介入审查，可能是一个高价值但方向待定的探索性功能。

**分析师点评**：OpenClaw项目正处在一个关键的增长期，社区参与度极高，但同时也面临稳定性挑战。建议核心团队优先处理“消息泄露”和“会话稳定性”类的高优先级积压问题，以稳固用户基础。同时，对于诸如`claude-cli-interactive`等高讨论度的探索性PR，应尽快给出明确的方向性反馈，以引导社区创造力。

---

## 横向生态对比

好的，作为资深技术分析师，现根据您提供的2026年6月10日各项目动态摘要，为您生成一份横向对比分析报告。

---

## **个人AI助手与自主智能体开源生态横向对比分析报告 (2026-06-10)**

### 1. 生态全景

今日，个人AI助手/自主智能体开源生态呈现出**高度活跃、分化加剧、安全与稳定性成为主旋律**的态势。头部项目如OpenClaw、IronClaw、ZeroClaw等日处理数百条Issue/PR，社区参与度极高，正处于密集迭代期。各项目在追求功能丰富性的同时，均面临由“消息泄露”、“会话挂起”、“模型兼容性”等问题带来的严峻稳定性挑战。**安全审计成为今日的突出热点**，PicoClaw和NullClaw均出现了针对性的安全漏洞报告与修复，标志着生态正从“功能优先”向“生产就绪”的成熟阶段过渡。此外，跨Agent协作、任务通知、多模型支持等高级功能成为多个项目的共同探索方向，预示着智能体生态正在向更复杂、更自动化的协作网络演进。

### 2. 各项目活跃度对比

| 项目名称 | 活跃度评估 | Issue 更新 | PR 更新 | 新版本发布 | 核心关注点 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **极高** | 452条 | 492条 | 有 (v2026.6.5) | 稳定性、安全、消息泄露 | 高产出，但高优先级Bug待解决 |
| **IronClaw** | **极高** | 较高 (约50+)* | 较高 (约48+)* | 无 | Reborn生产就绪、安全审计、测试 | 密集重构，健康快速迭代 |
| **ZeroClaw** | **高** | 50条 | 50条 | 无 | 运行时稳定性、安全加固 | 积极修复，待合并PR多 |
| **NanoBot** | **高** | 6条 | 23条 | 无 | 模型兼容性、上下文污染 | 贡献者活跃，修复迅速 |
| **Hermes Agent** | **高** | 50条 | 50条 | 无 | 平台兼容性、Telegram集成 | 功能打磨，稳定性提升 |
| **CoPaw** | **高** | 37条 | 35条 | 有 (v1.1.11-beta.2) | 前端性能、模型兼容性 | 积极迭代，社区讨论热度高 |
| **PicoClaw** | **高** | 15条 (安全) | 5条 (合并) | 有 (Nightly) | **安全审计**、授权绕过 | 面临严重安全挑战，响应迅速 |
| **NanoClaw** | **中** | 1条 | 43条 | 无 | 代码清理、关键修复 | 技术债务清理阶段 |
| **LobsterAI** | **较高** | 1条 | 4条 (合并) | 无 | 任务通知、跨模型协作 | 功能开发与快速迭代中 |
| **NullClaw** | **高** | 5条 | 8条 | 无 | Bug修复、平台集成 | 维护效率高，项目健康 |
| **Moltis** | **无活动** | - | - | - | - | -
| **TinyClaw** | **无活动** | - | - | - | - | -

*注：IronClaw的Issue/PR数据为估算值，原文提及“共约98条”。

### 3. OpenClaw 在生态中的定位

*   **生态核心参照**：OpenClaw 是整个生态中当之无愧的**旗舰和参照项目**，其 Issue/PR 数量远超其他项目，社区规模最大，功能最为全面。它是许多衍生项目（如 NanoClaw, PicoClaw）的功能和架构基准。
*   **技术路线**：OpenClaw 采用“**大而全**”的路线，集成了对几乎所有主流消息平台（Slack, Discord, Telegram, iMessage 等）和 LLM Provider 的支持。其核心优势在于功能完整性和强大的社区生态系统。相比之下，其他项目更倾向于在某些方面进行**垂直深耕或差异化**。
    *   **优势**：功能最为丰富、社区资源最多、文档和教程相对完善。
    *   **劣势**：复杂度高导致 Bug 数量多，对资源消耗较大，部署和配置门槛相对较高。今日报告显示其核心的“消息泄露”和“会话稳定性”问题积压已久，反映了大型项目维护的挑战。
*   **社区规模**：从 Issue/PR 数量看，OpenClaw 社区规模至少是第二梯队项目的 **5-10 倍**，是生态中最具影响力的项目。

### 4. 共同关注的技术方向

生态中的多个项目不约而同地涌现出以下技术和功能需求，代表了行业趋势：

1.  **跨模型/多运行时支持**：
    *   **涉及项目**：**NanoBot, NanoClaw, LobsterAI, ZeroClaw**。
    *   **具体诉求**：用户和开发者们不再满足于绑定单一模型提供商。NanoBot 和 ZeroClaw 社区积极修复 GPT-5 系列等新模型的兼容性问题。NanoClaw 社区提出了更具前瞻性的“多运行时抽象层”提案，期望平台能与 Claude、Codex、本地模型等任意 SDK 解耦。LobsterAI 用户则聚焦于“跨模型子任务协作”的稳定性。这表明“**模型中立**”已成为下一代智能体平台的核心要求。

2.  **Agent 协作与自动化工作流**：
    *   **涉及项目**：**OpenClaw, IronClaw, NanoClaw, LobsterAI, CoPaw, Hermes Agent**。
    *   **具体诉求**：社区对“多 Agent 协作”的呼声极高。具体表现为：NanoClaw 的“技能市场”和“GitAgent 协议支持”，LobsterAI 和 Hermes Agent 对“跨模型任务调用与通知”的讨论，CoPaw 用户建议的“学习循环”机制，以及 OpenClaw 社区对“Telegram Guest Bots 多 Bot 协作”的强烈期待。这标志着生态正从“单助手”向“多智能体协同工作流”演进。

3.  **稳定性与可靠性工程**：
    *   **涉及项目**：**OpenClaw, ZeroClaw, NanoBot, PicoClaw**。
    *   **具体诉求**：这是今日所有项目的共同痛点。主要表现为：**会话挂起与恢复**（OpenClaw, ZeroClaw）、**消息泄露**（OpenClaw）、**上下文污染**（NanoBot）、**内存泄漏**（OpenClaw）、**Cron 任务可靠性**（ZeroClaw, NullClaw）。这反映了社区对智能体作为“生产工具”的可靠性要求正在急剧提升。

4.  **安全与权限控制**：
    *   **涉及项目**：**PicoClaw, NullClaw, ZeroClaw, IronClaw**。
    *   **具体诉求**：PicoClaw 今日爆发的安全审计报告（SSRF、CSRF、授权绕过等）是最大警钟。NullClaw 修复了 PII 脱敏误报和 Telegram 配对码安全问题。ZeroClaw 讨论了对子进程的内存限制（防 OOM）和 MCP 工具权限控制。这表明，**随着 Agent 能力的增强，其安全风险敞口也在同步放大**，安全已从“可选项”变为“必选项”。

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全方位、多平台、高功能密度 | 技术发烧友、追求功能完备的开发者 | 庞大插件/渠道生态，社区驱动的“大熔炉” |
| **IronClaw** | 企业级、生产就绪、安全治理 | 企业用户、需要审计和多租户的场景 | “Reborn”架构重构，强调查用、安全和可观测性 |
| **ZeroClaw** | 运行时稳定、安全加固、自动化（Cron） | 重视稳定性和自动化的运维/开发者 | 在安全（MCP权限、子进程限制）和自动化（Cron）上投入显著 |
| **NanoBot** | 本地优先、记忆系统、WebUI体验 | 注重隐私、运行本地模型的个人用户 | 独特的“Dream”机制和`history.jsonl`记忆管理，强调用户对记忆的控制权 |
| **Hermes Agent** | 平台兼容性、Telegram集成、macOS体验 | 跨平台用户、Telegram日常用户 | 精细化的 Provider 适配，对 macOS 和 Telegram 有独特优化 |
| **CoPaw** | 国内本地化、前端体验、浏览器自动化 | **国内用户**、对本地化要求高的开发者 | 针对国内模型（如Qwen）和云服务做了大量适配，前端使用Tauri |
| **PicoClaw** | 安全、轻量级、渠道授权 | 对安全有极高要求的场景 | 专注于安全防御，安全审计发现是双刃剑，暴露问题但倒逼加固 |
| **NanoClaw** | 基于OpenClaw的精简与技能生态 | 寻求更轻量、更易上手的开发者 | 通过“技能市场”和“直接运行模式”降低使用门槛 |

### 6. 社区热度与成熟度

*   **快速迭代阶段（“功能探索与扩展”期）**：
    *   **OpenClaw, IronClaw, CoPaw, ZeroClaw**。这些项目 Issue/PR 数量巨大，功能频繁更新，社区讨论活跃。但同时 Bug 数量也较多，稳定性是主要挑战。它们正在快速填充功能边界，但对生产环境的打磨仍在进行中。

*   **质量巩固阶段（“稳定性与安全加固”期）**：
    *   **PicoClaw, NullClaw, NanoBot**。这些项目在经历了早期的功能扩张后，开始将重心转向修复安全漏洞、解决核心Bug、清理技术债务。其活跃的Bug报告和迅速的修复响应，是项目走向成熟的明确信号。

### 7. 值得关注的趋势信号

*   **“模型中立”是下一阶段的入场券**：NanoClaw 和 NanoBot 社区的动向表明，智能体平台的核心竞争力不再仅仅是绑定某个最强的模型，而是提供一个**稳定、高效、安全**的“模型运行时编排层”。开发者更关心的是平台的可靠性、可扩展性和安全性，而非对单一模型的深度依赖。
*   **“安全”正在从“特性”转变为“基线”**：PicoClaw 的 Security Audit 事件是今日最重要的警钟。它揭示了智能体“读取网络”、“执行代码”等能力背后巨大的攻击面。对于任何打算将AI Agent用于生产环境或处理敏感数据的团队来说，**安全设计和审计必须是开发流程的一部分，而非事后补救**。
*   **Agent 协作正走向“企业工作流”**：对 Cron 任务、跨模型子任务、Agent 间通信、任务结果通知等功能的密集关注，预示着AI Agent正在从“聊天助手”演变为**自动化工作流引擎的底层基础设施**。这要求项目在调度、状态管理、失败重试、监控告警等方面提供企业级的能力。
*   **“可观测性”成为运维刚需**：IronClaw 和 CoPaw 社区对 Langfuse、OpenTelemetry 的讨论，揭示了开发者不仅需要功能强大的Agent，更需要**可追踪、可审计、可调试**的工具链来理解和优化其行为。这对于构建复杂的、多步的Agent工作流至关重要。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 NanoBot 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 2026-06-10 项目动态日报。

---

# NanoBot 项目动态日报 | 2026-06-10

## 1. 今日速览

项目今日活跃度**极高**，主要体现在 PR 提交和 Issue 报告的密集程度上。过去 24 小时内共有 **23 个 PR** 和 **6 个 Issue** 被更新，表明社区贡献者非常活跃，正在积极修复 Bug 和推进新功能。项目核心聚焦于**稳定性修复**、**模型兼容性**（特别是 GPT-5 系列）以及**用户体验优化**。虽然没有新版本发布，但大量的待合并 PR 预示着下一次版本发布将包含重量级改进。目前有 13 个 PR 处于待合并状态，需关注维护者的审查和合并进度。项目整体健康度**良好**，社区协作紧密。

## 2. 版本发布

- **无**。本次日报周期内无新版本发布。

## 3. 项目进展

过去 24 小时内，项目有 **10 个 PR 被合并或关闭**，标志着多个重要功能点和修复进入主分支。以下是关键进展：

- **WebUI 功能增强**：
    - `[WebUI] feat(webui): add assistant reply fork-from-here (#4208)` [已关闭]: 为 WebUI 增加了“从此处分支”的功能，允许用户从某条 AI 回复处创建新的对话，极大地增强了对话管理的灵活性。

- **文档与开发者体验**：
    - `[docs] docs: make onboarding friendlier for beginners (#4177)` [已关闭]: 重新整理了项目文档，为新用户提供了更清晰的入门路径，降低了上手门槛。

- **梦想与身份管理**：
    - `[feat] feat(dream): allow users to decide whether dream can edit USER.md and SOUL.md or not (#3400)` [已关闭]: 允许用户通过配置控制“Dream”机制是否能够修改 `USER.md` 和 `SOUL.md` 这类核心身份文件，给予用户更多控制权，保护个人设定免受自动化修改。

- **GitAgent 协议支持**：
    - `[feat] Add GitAgent Protocol support (agent.yaml + SOUL.md) (#4034)` [已关闭]: 新增了对 GitAgent Protocol 的支持，使得 NanoBot 能够更好地与其他兼容该标准的 AI Agent 生态进行交互，提升了项目的可移植性和标准化程度。

- **核心逻辑改进**：
    - `[feat] Improve tool call validation strictness (#4190)` [已关闭]: 加强了对模型返回工具调用的参数验证，避免了因参数格式错误导致的潜在问题，提升了工具调用的鲁棒性。

这些合并的 PR 表明，NanoBot 不仅关注基础能力的稳定，也在不断打磨用户体验、文档和生态兼容性。

## 4. 社区热点

今日最受关注的讨论集中在以下几个议题：

1.  **`history.jsonl` 上下文污染 (Issue #4259)**
    - **链接**: [Issue #4259](https://github.com/HKUDS/nanobot/issues/4259)
    - **热度**: 2 条评论，技术分析详实。
    - **核心诉求**: 开发者 `chxuan` 提交了一份极为详细的 Bug 报告，指出 `history.jsonl` 机制存在严重缺陷：在不同会话间，由于“Dream”机制未能正确处理，导致会话历史记录（`# Recent History`）被跨会话注入，造成上下文污染。该 Issue 通过数据流分析清晰指出了问题所在，引发了社区对“Dream”机制数据隔离性的深入讨论。

2.  **GPT-5 系列模型兼容性 (Issue #4261 & PR #4268 & PR #4263)**
    - **链接**: [Issue #4261](https://github.com/HKUDS/nanobot/issues/4261), [PR #4268](https://github.com/HKUDS/nanobot/pull/4268), [PR #4263](https://github.com/HKUDS/nanobot/pull/4263)
    - **热度**: 1 个 Issue 和 2 个并行 PR。
    - **核心诉求**: 随着 GPT-5.x 的推出，其 API 将 `max_tokens` 参数替换为 `max_completion_tokens`。社区迅速响应，`mraad` 报告了此不兼容问题。随后，两位贡献者 `04cb` 和 `axelray-dev` 几乎同时提交了 PR 来修复此问题，展现了社区解决问题的快速响应能力。这也是今日 PR 数量激增的主要原因之一。

3.  **IdleCompact 机制缺陷 (Issue #4264)**
    - **链接**: [Issue #4264](https://github.com/HKUDS/nanobot/issues/4264)
    - **核心诉求**: 用户 `imkuang` 指出了 `idleCompact` 的问题：在对话过程中，用户最后的纠正和正确结果常常被排除在摘要范围外（当前机制会忽略最后8条消息），导致历史记录`history.jsonl` 中保留了错误的中间结论。这直接影响了模型长期记忆的准确性。

## 5. Bug 与稳定性

今日报告的 Bug 涵盖核心逻辑和前端体验，按严重程度排列如下：

- **高：`history.jsonl` 跨会话注入 (Issue #4259)**
    - **描述**: “Dream”机制在进行跨会话历史总结时，未能正确隔离不同会话的上下文，导致 A 会话的总结被注入 B 会话的 Prompt，是严重的上下文污染问题。
    - **关联 PR**: 暂无，但 Issue 分析清晰，预计很快会有修复 PR。
    - **链接**: [Issue #4259](https://github.com/HKUDS/nanobot/issues/4259)

- **高：GPT-5 系列模型请求失败 (Issue #4261)**
    - **描述**: 使用 `custom` 或 `openai-compat` 驱动调用 GPT-5.x 模型时，因使用了被废弃的 `max_tokens` 参数而失败。
    - **关联 PR**: 两个并行修复 PR： [PR #4268](https://github.com/HKUDS/nanobot/pull/4268), [PR #4263](https://github.com/HKUDS/nanobot/pull/4263)
    - **链接**: [Issue #4261](https://github.com/HKUDS/nanobot/issues/4261)

- **中：`idleCompact` 总结不准确 (Issue #4264)**
    - **描述**: `idleCompact` 机制因忽略最后 8 条消息，导致总结出的历史记录丢失了用户最终纠正和正确的结果，从而污染长期记忆。
    - **关联 PR**: 暂无
    - **链接**: [Issue #4264](https://github.com/HKUDS/nanobot/issues/4264)

- **低：WebUI 会话内容丢失 (PR #4267)**
    - **描述**: WebUI 存在一个偶发性 Bug，导致部分 AI 回复在前端渲染时被丢弃，虽然后端已正确保存。
    - **关联修复**: 已有 PR 修复。 [PR #4267](https://github.com/HKUDS/nanobot/pull/4267)

- **低：`botIcon` 在 Agent 模式启动时未立即生效 (Issue #4262)**
    - **描述**: 进入 Agent 模式时，首次显示的图标是默认的 "puppy"，而非用户配置的 `botIcon`。
    - **关联 PR**: 暂无
    - **链接**: [Issue #4262](https://github.com/HKUDS/nanobot/issues/4262)

## 6. 功能请求与路线图信号

- **每个会话独立模型 (Issue #4253)**: 用户 `rombert` 提出希望能在不同会话中切换不同的模型预设（如快速/付费 vs. 私密/廉价）。这是一个非常强烈的需求信号，表明用户角色复杂，对 AI Agent 使用场景有细粒度控制的需求。目前暂无对应 PR，可能作为未来的重要功能。
- **Agent 模式初始化显示自定义图标 (Issue #4262)**: 用户 `mraad` 提议 Agent 模式启动时立即显示用户配置的 `botIcon`。这是一个小但提升体验的易用性改进，预计会被快速采纳。
- **版本检查改为“按需点击” (PR #4255)**: `JiajunBernoulli` 提交了一个重构 PR，将启动时的实时 PyPI 版本检查改为在“设置”页面点击触发。这符合“最小化后台开销”的设计哲学，很可能被合并。

## 7. 用户反馈摘要

- **用户 `rombert` 的工作流**: “我在两个预设模型间切换：一个快（OpenRouter），一个私有廉价（本地llamacpp）。” 这揭示了高级用户对**任务驱动的模型切换**的真实需求，他们需要平衡速度、成本和隐私。
- **用户 `imkuang` 的痛点**: 在一次对话中，用户反复纠正模型，但 `idleCompact` 的错误总结导致历史记录保留了**错误的中间步骤**，丢失了正确的最终结论。用户认为“这与基于Token预算压缩会话的机制不同，后者在会话进行中动态处理。” 这反映出用户期望的压缩机制是**会话感知的**，并能理解对话的最终结论。
- **用户 `chxuan` 的深度分析**: 该用户不只是报告 Bug，而是通过**数据流分析**的方式，精确指出了 `ContextBuilder.build_system_prompt()` 中“未做会话隔离”的代码级问题。这表明社区中有**非常高技术水平的贡献者**，能帮助团队快速定位核心问题。

## 8. 待处理积压

以下为长期未响应的关键 Issue 或 PR，需要维护者重点关注：

1.  **PR #4119: `fix(exec): block relative symlink workspace escapes`**
    - **状态**: 已开启 10 天
    - **重要性**: **高 (安全相关)**。该 PR 修复了一个可通过符号链接（symlink）逃逸工作空间的安全漏洞。
    - **链接**: [PR #4119](https://github.com/HKUDS/nanobot/pull/4119)

2.  **PR #4193: `test: add memory lifecycle harness`**
    - **状态**: 已开启 6 天
    - **重要性**: **高 (测试基建)**。该 PR 为内存生命周期（Memory lifecycle）添加了脚本化的测试工具，对于保障核心记忆机制的稳定性至关重要。维护者 `yu-xin-c` 提交了多个此类测试 PR，需要及时审查。
    - **链接**: [PR #4193](https://github.com/HKUDS/nanobot/pull/4193)

3.  **Issue #4061: `Bug: OpenAI-compatible text-format tool calls are not parsed into structured tool calls`**
    - **状态**: 已开启 12 天
    - **重要性**: **中 (广泛兼容性)**。该 Bug 导致部分 OpenAI 兼容的服务提供商（如一些代理服务）无法正常使用工具调用功能，限制了 NanoBot 的生态系统兼容性。
    - **链接**: [Issue #4061](https://github.com/HKUDS/nanobot/issues/4061)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于提供的数据生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026年06月10日

## 1. 今日速览

Hermes Agent 项目今日**活跃度极高**，社区贡献者积极提交代码与报告问题，体现了项目的健康生态。过去24小时内，共有50条 Issue 更新和50条 PR 更新，讨论热度主要集中在为 Telegram、macOS 及各平台提供更精细化的功能支持与 Bug 修复。值得注意的是，虽无新版本发布，但针对 macOS 更新流程、Gateway 稳定性及桌面端体验的修复与反馈占据了今日动态的核心，显示出项目在**提升生产环境稳定性和用户体验**方面的重点投入。

## 2. 版本发布

*无。*

## 3. 项目进展

今日虽无 PR 被正式合并，但大量高质量 PR 的提交标志着项目在多个关键方向上取得实质性进展。这些推进主要集中在以下方面：

- **稳定性与平台兼容性修复**：多个 PR 针对 macOS 和 Gateway 的特定问题进行修复。例如，[PR #43181](https://github.com/nousresearch/hermes-agent/pull/43181) 修复了 `hermes update` 后 LaunchAgent 已卸载但无法恢复的问题；[PR #43199](https://github.com/nousresearch/hermes-agent/pull/43199) 修复了 macOS 上重启 Gateway 时通知缺失的问题；[PR #43222](https://github.com/nousresearch/hermes-agent/pull/43222) 引入了 Provider 降级机制，以应对连续“流枯竭”(stale-stream) 问题。
- **特定 Provider 的兼容性优化**：[PR #42890](https://github.com/nousresearch/hermes-agent/pull/42890) 修复了 Gemini Provider 对原生资源模型 ID 的处理；[PR #43187](https://github.com/nousresearch/hermes-agent/pull/43187) 修复了 Bedrock Provider 对 `profile` 配置的忽视问题；[PR #43163](https://github.com/nousresearch/hermes-agent/pull/43163) 修复了使用 `gpt-5.x` 系列模型时因参数不匹配导致的崩溃。
- **新功能与生态集成**：一个名为 Unforgit 的内存提供者插件被提交（[PR #43190](https://github.com/nousresearch/hermes-agent/pull/43190)），进一步丰富了 Hermes Agent 的记忆功能生态。同时，[PR #43194](https://github.com/nousresearch/hermes-agent/pull/43194) 为 Google Workspace 集成增加了 Apps Script OAuth 权限，扩展了自动化场景。
- **性能与资源清理**：[PR #43212](https://github.com/nousresearch/hermes-agent/pull/43212) 引入了一个状态清理机制，用于清除平台事件产生的“幽灵”会话行，减少数据库冗余。

这些进展共同表明，项目正在从功能追逐转向**打磨细节、强化稳定性与提升平台兼容性**，向着更成熟的生产级应用迈进。

## 4. 社区热点

今日社区讨论热度最高的议题反映了用户对 **Telegram 集成深度**和**高级自动化工作流**的迫切需求。

- **Telegram Guest Bots 与 Bot-to-Bot 协作**：[Issue #21587](https://github.com/nousresearch/hermes-agent/issues/21587)（评论: 9）是今天的流量担当。用户 `Editorenbici` 强烈建议利用 Telegram 最新 API 的11项新特性，特别是“Guest AI Bots”功能，以实现多 Agent 间的快速协作。这超出了简单的聊天机器人范畴，指向了**构建可交互的 Agent 团队**的愿景。
- **密码脱敏与模型自我认知 Bug**：[Issue #43083](https://github.com/nousresearch/hermes-agent/issues/43083)（评论: 6）揭示了“防御性脱敏”(Defence-in-depth) 在日志记录时的一个微妙 Bug。当模型查看自己的历史对话时，密码被替换为 `***`，导致它在进行第二次工具调用时因参数不匹配而失败。这暴露了安全策略与Agent 认知能力之间的冲突，是 Agent 可靠性的一个核心难题。
- **macOS 更新流程 Bug**：[Issue #42006](https://github.com/nousresearch/hermes-agent/issues/42006)（评论: 5）突出了 macOS 用户的痛点，即在执行 `hermes update` 后，Gateway 因 `launchd` 作业状态管理不当而无法重启，需要用户手动介入。这直接触发了多个相关 PR 的提交，表明社区对这一稳定问题的强烈不满与积极应对。

## 5. Bug 与稳定性

今日报告的 Bug 涵盖多个方面，按严重程度排列如下：

**P1（严重）**:
- **密码脱敏导致模型推理失败**：[Issue #43083](https://github.com/nousresearch/hermes-agent/issues/43083) – 模型查看历史时，密码脱敏字符 `***` 导致后续工具调用失败。暂无直接修复 PR。
- **Cron 传递目标解析失败**：[Issue #43014](https://github.com/nousresearch/hermes-agent/issues/43014) – 使用 `deliver=origin` 的 Cron 任务无法解析交付目标，导致任务失败。暂无直接修复 PR。

**P2（中）**:
- **macOS Gateway 更新后无法重启**：[Issue #42006](https://github.com/nousresearch/hermes-agent/issues/42006) – 已有修复 PR：[PR #43181](https://github.com/nousresearch/hermes-agent/pull/43181) 和 [PR #43199](https://github.com/nousresearch/hermes-agent/pull/43199)。
- **`session_search` 可检索到巨大的压缩上下文**：[Issue #43175](https://github.com/nousresearch/hermes-agent/issues/43175) – 可能导致上下文处理异常。暂无直接修复 PR。
- **Gemini Provider 返回 HTTP 400/404**：[Issue #43026](https://github.com/nousresearch/hermes-agent/issues/43026) – 与 Hermes 内部 HTTP 客户端兼容性问题。修复 PR：[PR #42890](https://github.com/nousresearch/hermes-agent/pull/42890) 可能提供缓解。
- **Cron 作业注入脚本输出导致扫描问题**：已有修复 PR [PR #43223](https://github.com/nousresearch/hermes-agent/pull/43223)。
- **`launchd` 重启标记缺失**：修复 PR [PR #43199](https://github.com/nousresearch/hermes-agent/pull/43199)。

**P3（低）**:
- **Desktop UI 问题**：包括侧边栏排序、用户消息被裁剪、会话未刷新、图标主题不兼容等（[Issue #42516](https://github.com/nousresearch/hermes-agent/issues/42516), [#42992](https://github.com/nousresearch/hermes-agent/issues/42992), [#42962](https://github.com/nousresearch/hermes-agent/issues/42962), [#43122](https://github.com/nousresearch/hermes-agent/issues/43122)）。
- **配置项不生效**：`auxiliary.title.enabled` ([#41744](https://github.com/nousresearch/hermes-agent/issues/41744)) 和 `failure_limit` 配置 ([#42924](https://github.com/nousresearch/hermes-agent/issues/42924)) 被硬编码覆盖。

## 6. 功能请求与路线图信号

虽然今日无新版本发布，但社区提出的功能请求和相关的 PR 为未来路线图提供了清晰信号：

- **可配置性与本地化**：`command description override` ([#13107](https://github.com/nousresearch/hermes-agent/issues/13107)) 和 `per-tool enable/disable` ([#31375](https://github.com/nousresearch/hermes-agent/issues/31375)) 的呼声很高，表明用户对**更精细的控制粒度**有强烈需求。
- **本地 Provider 体验优化**：`Default quiet mode for Ollama` ([#43028](https://github.com/nousresearch/hermes-agent/issues/43028)) 和 `'local' provider overlay support` ([#43052](https://github.com/nousresearch/hermes-agent/issues/43052)) 表明，随着本地模型（如 Ollama, vLLM）的普及，用户希望 Hermes Agent 能为其提供开箱即用的**更流畅、更少打扰的体验**。
- **协作与工作流 Agent**：[Issue #21587](https://github.com/nousresearch/hermes-agent/issues/21587) 提出的 Telegram 多 Bot 协作功能，加上 [Issue #42896](https://github.com/nousresearch/hermes-agent/issues/42896) 对 Kanban Review 流程的改进请求，共同指向了**让 Hermes Agent 成为更强大的协作平台**的长期方向。
- **“放飞”模式（Full YOLO Mode）**：[Issue #42921](https://github.com/nousresearch/hermes-agent/issues/42921) 要求在设置了自动批准后，依然能执行某些高风险操作（如 `execute_code`），这反映了**资深用户对极致自动化与控制权的渴望**。

## 7. 用户反馈摘要

从今日的讨论中，可以提炼出以下几类用户的真实声音：

- **资深/开发者用户**：对安全与稳定性的要求极高。
    - *痛点*：`Passwords get replaced by *** but model reads back...` 暴露了安全机制与Agent可靠性的矛盾，用户 `nnnarvaez` 发现了一个深层交互逻辑Bug。
    - *诉求*：`Feature request: Option to disable execute_code approval prompts (full YOLO mode)`，用户 `Th0rgal` 表达了在信任环境中完全摆脱确认提示，实现“所见即所得”自动化的强烈愿望。

- **macOS/Docker 运维用户**：聚焦于更新部署流程的流畅性。
    - *痛点*：`macOS: launchd_restart missing bootout...` 和 `HERMES_DASHBOARD_PUBLIC_URL not respected...` 直接影响了他们的工作流，导致部署后需要额外的手动干预。
    - *满意*：社区快速响应了这些问题，提交了修复 PR（见第5部分），显示出健康项目对用户痛点的敏捷反馈机制。

- **多语言用户**：关注国际化与跨平台体验。
    - *痛点*：`Feature request: support command description override via config.yaml` 反映了非英语用户对多语言支持的本能需求。
    - *场景*：`[Bug]: Context-file scanner: bare token "praxis" in known_c2_framework pattern causes false positives (German "Praxis" = medical practice)`，用户 `langelchristian23-dev` 报告了一个因文化差异导致的误报问题，凸显了全球化产品在模式匹配时需要考虑的语言歧义。

## 8. 待处理积压

以下为长期开放或近期需要关注的重要 Issue，尚无直接的修复 PR。

- **[B] 密码脱敏导致模型失败**：[Issue #43083](https://github.com/nousresearch/hermes-agent/issues/43083) (P1) – 这是一个核心逻辑Bug，直接关系到 Agent 的可靠执行，优先级极高，需尽快分析并设计修复方案。
- **[B] Cron 交付目标解析失败**：[Issue #43014](https://github.com/nousresearch/hermes-agent/issues/43014) (P1) – 作为自动化核心组件，Cron 功能的故障会严重影响用户信心，应尽快解决交付目标解析逻辑。
- **[B] Honcho memory plugin 挂起**：[Issue #34070](https://github.com/nousresearch/hermes-agent/issues/34070) (P3，但长期未决) – 这是一个冷启动时的回归性问题，已存在超10天，影响了使用 Honcho 作为记忆插件的用户，建议维护者纳入 Bug 修复计划。
- **[B] `auxiliary.title.enabled` 配置失效**：[Issue #41744](https://github.com/nousresearch/hermes-agent/issues/41744) (P3) – 与配置系统相关的长期 Bug，虽然影响范围有限，但“配置不生效”对用户体验的负面影响不容忽视。
- **[安全性] 安全审计建议**：多个安全性相关的 Issue 如 [#37968](https://github.com/nousresearch/hermes-agent/issues/37968) (Cron 环境隔离)，[#43146](https://github.com/nousresearch/hermes-agent/issues/43146) (C2 模式误报) 仍处于开放状态。随着项目成熟，这些安全问题应被赋予更高的处理优先级。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw 项目数据生成的 2026-06-10 项目动态日报。

---

## PicoClaw 项目日报 | 2026-06-10

### 1. 今日速览

今日 PicoClaw 项目迎来了一次大规模的安全审计更新，活跃度极高。社区安全研究员 YLChen-007 集中提交了 15 个与安全相关的 Issue，覆盖了 SSRF 绕过、权限提升、CSRF 等多个方面，显示出项目在安全防护上的巨大挑战。与此同时，项目核心团队也积极响应，提交了多个修复补丁以应对部分已暴露的安全问题。尽管 Issue 和 PR 数量激增，但项目维护者的快速反应和清晰的修复路线图，体现了项目在快速迭代中对于安全性的重视，整体项目健康度处于“高压但可控”的状态。

### 2. 版本发布

- **Nightly Build (v0.2.9-nightly.20260610.b9a8fad6)**
  - 这是一个自动化的夜间构建版本，可能不稳定，仅供测试使用。
  - **变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
  - **注意事项**: 使用前请备份数据，并注意可能存在的安全漏洞（参见今日安全报告）。

### 3. 项目进展

今日有 5 个 PR 被合并或关闭，项目在以下方面取得了实质性进展：

- **配置健壮性提升**: PR #3064 修复了配置迁移时因类型断言检查不严格可能导致的 panic 问题，提升了系统的稳定性。
- **核心模型兼容性**: PR #2940 和 PR #2942 被合并，分别修复了 `claude-opus-4-7` 模型因 `temperature` 参数弃用而报错，以及 `claude-sonnet-4.6` 默认模型 ID 格式错误的问题，确保了对最新 Anthropic 模型的兼容。
- **跨 Agent 协作基础设施**: PR #2937 的合并是一个重要的里程碑。该 PR 引入了 Agent 协作总线，为 Agent 之间提供了初始化的通信能力，为构建更复杂的多 Agent 工作流奠定了基础。
- **文档更新**: PR #3086 更新了微信二维码，确保社区沟通渠道的畅通。
- **其他修复**: 修复了 Web UI 显示会话历史不完整、上下文压缩配置不生效、流式传输中工具调用消息被错误过滤等多个长期存在的问题。

### 4. 社区热点

今日社区讨论最活跃的议题是 **安全审计报告**。

- **Issues #3068 - #3082** (15 个)：由用户 `YLChen-007` 创建的一系列安全问题。虽然单个 Issue 评论不多，但作为一个事件集群，它们引发了社区对 PicoClaw 安全模型的大范围关注。这些报告非常专业，详细描述了漏洞细节、利用方法和潜在影响，包括：
    - **SSRF 防护绕过**：通过 `198.18.0.0/15` 特殊IPv4地址、ISATAP IPv6、环境配置的HTTP代理等方式绕过 `web_fetch` 工具的限制。
    - **权限提升与授权绕过**：Feishu、MQTT、WeCom 等渠道的 `allow_from` 检查可以被绕过；`exec` 工具的 `cwd` 存在符号链接竞争条件；Launcher 的 `allowed_cidrs` 存在绕过风险。
    - **认证与CSRF**：Launcher 首次设置存在 CSRF 漏洞；已认证的 WebSocket 客户端可以触发配置重载。

这些报告的集中出现，表明项目需要进行一次全面的安全架构审视。

- **Issues #2404**: 关于在配置文件中添加 `streaming` 开关的提议，虽然创建较早，但至今仍有 11 条评论，说明社区对支持原生流式 HTTP 请求有持续且强烈的需求。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在安全漏洞方面，严重程度普遍较高。

- **严重**:
    - `exec` 命令白名单可通过 `jq` 绕过进行环境变量泄露 (#3079)。**已有修复 PR #3087** 尝试处理相对路径问题，但未完全覆盖此漏洞。
    - `web_fetch` 工具存在多种 SSRF 绕过方式 (#3074, #3077, #3078)，可导致内部网络信息泄露。**已有修复 PR #3085** 尝试解决 `198.18.0.0/15` 绕过问题。
    - 多个渠道的 `allow_from` 授权规则可以被绕过，导致未授权用户可与 Agent 交互 (#3068, #3076, #3082)。
    - Launcher 首次设置存在 CSRF 漏洞，可导致本地控制面被接管 (#3072)。
- **中等**:
    - 历史记录中多次用户输入的消息只能看到最后一条 (#2796)。**已有修复 PR #2990** 处于待合并状态。

### 6. 功能请求与路线图信号

- **高潜力功能**:
    - **流式 HTTP 请求支持**：Issue #2404 请求在配置中添加 `streaming: true` 以支持像 OpenAI Python 客户端那样的流式交互。这是一个呼声很高的功能，虽无直接关联 PR，但很可能被纳入下一版本的路线图。
    - **DeltaChat 网关**: PR #3063 新增了 DeltaChat 网关支持，这是一个去中心化通信平台，表明项目正在探索更多样化的集成方式。目前处于开放状态。
    - **NEAR AI Cloud 提供商**: PR #2917 增加了对 NEAR AI Cloud 提供商的支持，这是一个支持可信执行环境（TEE）的 AI 云平台，符合未来对安全和去中心化计算的需求。
    - **使用 `vodozemac` 替代 `libolm`**: Issue #3088 建议用维护更安全的新库替换已弃用的 `libolm` 加密库，这将对所有依赖加密的渠道产生积极影响。

### 7. 用户反馈摘要

- **痛点**:
    - **安全担忧**: 今日大量的安全报告是用户对项目安全性的最直接反馈，尤其是 `web_fetch` 和 `exec` 这类高权限工具的防护不足。
    - **配置问题**: 用户 `EverestSnow` 报告的历史消息显示不完整的问题 (#2796) 影响了基本使用体验。
    - **模型兼容性**: 用户 `LegendAlessandro-Liguori` 遇到的 Anthropic 模型兼容性问题 (#2939) 表明项目需要更及时地跟进上游 API 变化。
- **使用场景**:
    - **企业/团队协作**: 多个关于渠道（Feishu、WeCom、LINE）授权绕过的问题，说明项目已被用于敏感的团队协作场景，对安全细粒度控制有较高要求。
    - **自动化**: 关于 `exec` 工具的安全漏洞报告，表明用户正在利用 PicoClaw 执行系统命令来实现复杂的自动化任务。

### 8. 待处理积压

以下 Issue 和 PR 长期未得到响应或处理，建议维护者关注：

- **Issue #2984**: [Feature] 为 Pico WebSocket 客户端添加明确的回合结束信号。该功能对于外部客户端集成至关重要，已存在约一周且获得 1 个 👍。
- **PR #2917**: feat(provider): add NEAR AI Cloud provider。该 PR 创建于三周前，是一个高质量的新功能贡献，建议进行代码审查。
- **PR #2983**: fix(agent): retry empty llm response。修复了 OpenAI 兼容提供商返回空响应时的重试问题，对稳定性有直接帮助，已开放超过一周。
- **PR #2988**: fix(agent): use summarize_token_percent config for context compression。修复了上下文压缩配置不生效的 Bug，对配置项的正确性至关重要。

**安全报告批量处理**：今日由 `YLChen-007` 提交的 15 个安全 Issue 是最重要的待处理积压，需要项目核心团队优先评估、分配修复任务并给出响应时间表。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 NanoClaw 项目数据生成的 2026-06-10 项目动态日报。

---

## NanoClaw 项目动态日报 — 2026-06-10

### 1. 今日速览

今日项目活跃度极高。虽然 Issue 端仅有 1 条更新，但 PR 侧迎来了 43 条记录的集中处理，其中合并/关闭了 39 个 PR，表明项目维护团队正在进行大规模的代码库清理和版本整合。待合并的 PR 中出现了两项关键优化：飞书（Feishu）渠道的生产环境 Bug 修复，以及 Telegram 通道的安全加固。整体来看，项目处于一个“大扫除”与“关键修复”并行的状态，工作量巨大但方向明确。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日合并/关闭的 39 个 PR 主要集中在文档完善、功能清理和运维优化上，显示出项目在长期迭代后正在收拢技术债务。

-   **核心机制演进**：
    -   **PR #212** (已关闭)：新增了由 Lit + Vite 构建的 WebUI 控制面板，提供 11 个功能标签页，标志着项目向图形化管理迈出一大步。
    -   **PR #1285** (已关闭)：新增 `NANOCLAW_DIRECT_RUNNER` 环境变量，允许 Agent 在不启动 Docker 容器的情况下运行。这为资源受限的环境和快速调试提供了重要选项。
    -   **PR #1309** (已关闭)：实现了技能市场与注册系统，提供了从 GitHub 仓库发现、安装和管理技能的 CLI 命令，标志着“技能”生态开始平台化。

-   **可观测性与调试**：
    -   **PR #1202** (已关闭)：增加了 Agent 追踪（Trace）的可观测性。每一次 Agent 调用、工具使用、Token 消耗等都会被记录，并可通过本地 Web UI 查看，极大提升了排查复杂行为的效率。
    -   **PR #337** (已关闭)：增加了 Prompt 追踪日志功能，可记录内外部 Prompt/响应流程到 JSONL 文件，支持可配置的脱敏和截断。

-   **安全与审计**：
    -   **PR #214** (已关闭)：添加了全面的安全审计文档，涵盖了 SDK 凭据隔离和网络出口等关键发现。
    -   **PR #1333** (已关闭)：在日志中加入了构建时元数据（Git 提交、分支、时间戳），有助于追踪不同版本的运行表现。

**小结**：项目今日完成了大量早期积压的、具有里程碑意义的功能合并（如 WebUI、直接运行模式、技能市场），表明项目管理正从功能堆叠阶段转向整合与稳定阶段。

### 4. 社区热点

今日最受关注的无疑是 **Issue #1690**，它是过去24小时内唯一的活跃 Issue，且获得了 3 个 👍。

-   **[#1690] Multi-runtime agent SDK abstraction (Claude + Codex + local models)**
    -   **链接**: [nanocoai/nanoclaw Issue #1690](https://github.com/qwibitai/nanoclaw/issues/1690) *(实际链接为 nanocoai/nanoclaw)*
    -   **作者**: chiptoe-svg
    -   **分析**: 该 Issue 提出了一个极具前瞻性的架构升级：将项目核心与具体的大模型/Agent SDK 解耦。提案者设计了一个 `AgentRuntime` 接口，允许用户将不同厂商的 SDK（如 Claude、Codex）甚至本地模型，像安装 Channel 一样作为“技能”安装。这反映了社区中部分高级用户不满足于绑定单一底层模型，期望项目能成为“Agent 的瑞士军刀”，具备更强的灵活性和未来兼容性。该项目极有可能成为 NanoClaw 下一阶段的核心发展方向。

### 5. Bug 与稳定性

今日报告了一个高优先级的线上 Bug，并且其修复 PR 已经被创建。

-   **严重**：
    -   **[#2718] fix(feishu): cleanup zombie active_cards when agent-runner exits abnormally** (已合并)
        -   **链接**: [nanocoai/nanoclaw PR #2718](https://github.com/qwibitai/nanoclaw/pull/2718)
        -   **描述**: 修复了一个飞书（Feishu）渠道的生产环境 Bug：当 Agent Runner 进程被超时杀死后，飞书交互式卡片会无限期（长达 50 分钟以上）显示“运行中”。原因是清理卡片状态的逻辑只存在于 SDK 的正常完成事件中。该 PR 通过在其他异常退出路径上增加清理逻辑，修复了此问题，对飞书用户的使用体验有显著改善。

-   **中等 (安全)**：
    -   **[#2722] [OPEN] fix(telegram): use CSPRNG for pairing codes and lock down store permissions**
        -   **链接**: [nanocoai/nanoclaw PR #2722](https://github.com/qwibitai/nanoclaw/pull/2722)
        -   **描述**: 修复了 Telegram 通道配对码生成的安全性漏洞。原有 `generateCode` 使用可预测的 `Math.random()`，攻击者可据此推断出未来或历史上的有效配对码，进而获得对聊天群的注册权限。此 PR 将其切换为 `crypto.randomInt`，属于重要的安全加固。

### 6. 功能请求与路线图信号

今日无新增功能请求，但 **Issue #1690** 是社区提出的重量级路线图信号。

-   **高潜力纳入路线图**：
    -   **多运行时支持**：即 **Issue #1690** 的核心诉求。社区已有人做出了原型（抽象层），表明技术上可行。该功能将极大扩展 NanoClaw 的适用场景，使其成为一个通用的 Agent 编排器，而不仅仅是一个 Claude 封装器。如果项目维护者认同该方向，可能会在未来版本中将其作为核心特性进行规划和开发。

### 7. 用户反馈摘要

-   **痛点与改进期望**:
    -   用户体验到因进程异常退出导致的“假死”状态（PR #2718），这反映了系统在状态管理和错误处理方面仍有提升空间。
    -   高级用户不满足于单一模型，希望平台底层能够灵活切换和组合不同的 Agent 运行时（Issue #1690），体现了对“模型无关”架构的强烈需求。

-   **满意点**:
    -   技能（Skills）模式深入人心。无论是通过 `/add-*` 命令安装渠道（Issue #1690），还是设置开发环境（PR #1161）、实现审核流程（PR #1245），用户都倾向于用“技能”来解决问题，表明此设计模式的易用性已被验证。

### 8. 待处理积压

-   **需关注的安全加固 PR**:
    -   **[#2722] [OPEN] fix(telegram): use CSPRNG for pairing codes and lock down store permissions**
        -   **链接**: [nanocoai/nanoclaw PR #2722](https://github.com/qwibitai/nanoclaw/pull/2722)
        -   **状态**: 待合并。由于涉及Telegram渠道的配对安全，建议维护者优先处理并合并。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于您提供的GitHub数据为 **NullClaw** 项目生成的 **2026-06-10** 日报。

---

# NullClaw 项目动态日报 | 2026-06-10

## 1. 今日速览

在过去24小时内，NullClaw项目展现出极高的活跃度和维护效率。共有5个Issues得到更新，其中4个已关闭；8个PR被处理，其中7个已合并或关闭。项目团队集中修复了三个近期报告的Bug：**PII误报**、**Telegram无打字指示器**、**自定义OpenAI兼容提供商回退**，并合并了一次大规模的功能性PR（跨内存事件流）。**整体评估：项目健康度优，周活跃度极高（主要是修复和功能优化）。** 社区贡献者（如 `raskevichai`, `vernonstinebaker`, `DonPrus`）表现活跃，项目维护者响应迅速。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的PR主要集中在**Bug修复**和**平台集成**两个方向，项目稳定性显著提升。

- **核心Bug修复：**
    - `raskevichai` 贡献的PR #940解决了 **自定义OpenAI兼容提供商**配置无效的问题，确保系统会正确查询提供商的实际模型列表而非回退到硬编码的Claude模型。
    - `raskevichai` 贡献的PR #939修复了 **`compact_context` 标志**形同虚设的问题，现在该配置项可以正确控制对话历史是否自动压缩。
    - `raskevichai` 贡献的PR #943修复了 **Telegram内联按钮无打字指示器**的问题，提升了交互体验。
- **功能优化：**
    - `vernonstinebaker` 贡献的PR #945修复了 **PII脱敏误将系统时间/日期识别为电话号码**的误报问题，通过添加 `isDateLike()` 检查来规避。
    - `vernonstinebaker` 贡献的PR #946实现了 **按工具过滤器组（`tool_filter_groups`）生成系统提示**，而非无差别地包含所有工具，这有助于减少token消耗并提升模型专注度。
- **平台集成：**
    - `EvoLinkAI` 贡献的PR #947将 **Evolink** 添加为一级OpenAI兼容提供商，丰富了后端的模型选择。
- **长期功能合并：**
    - `DonPrus` 的PR #711（跨内存事件流）在经过长时间的开发后终于被合并。这是一个重要的架构性更新，为多Agent实例间的记忆同步提供了基础，预示着未来版本可能支持跨Agent协作。

## 4. 社区热点

今日无单一议题引发大量评论，但以下三个PR的合并代表了社区最关心的方向。

- **#940 [CLOSED] fix(models): query base_url for custom OpenAI-compatible providers**
    - 链接: [PR #940](https://github.com/nullclaw/nullclaw/pull/940)
    - **分析与诉求：** 这表明社区对**使用外部或自定义模型后端**有强烈需求。用户不希望被锁定在单一模型提供商，这个修复直接响应了“配置灵活性”的诉求，是提升项目可扩展性的关键一步。

- **#945 [CLOSED] fix(redaction): reject ISO date/time patterns as false-positive phone matches**
    - 链接: [PR #945](https://github.com/nullclaw/nullclaw/pull/945)
    - **分析与诉求：** 该议题由 `vernonstinebaker` 报告并修复。PII脱敏是隐私保护的核心功能，但其误报（将`date`命令的输出脱敏）严重影响了Agent执行系统命令时的可用性。社区对此类**实用性Bug**的关注度很高。

- **#711 [CLOSED] Feat/cross memory**
    - 链接: [PR #711](https://github.com/nullclaw/nullclaw/pull/711)
    - **分析与诉求：** 虽然这是一个早期的PR，但其合并标志着项目底层架构的重大变化。社区中关于“Agent如何记住并用好信息”的讨论一直很多，此PR通过事件流为**跨实例记忆同步**提供了原语，是满足社区对“更有记忆的Agent”诉求的重要实践。

## 5. Bug 与稳定性

今日报告的Bug数量为1个（新开的 #941）。其余4个为已关闭的旧Bug，目前已由相应的PR修复。

- **[严重] #941 [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens**
    - 链接: [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)
    - **严重程度：** **高**。这是一个功能完全失效的Bug。计划任务（Cron Job）被标记为完成但Agent子进程未启动，导致任务结果无法传递到Telegram。
    - **修复情况：** **已有PR**。社区贡献者 `DonPrus` 已经提交了PR #948（`fix cron agent delivery attribution`），专门针对此问题进行处理，目前状态为 **待合并**。这表明项目团队对关键Bug的响应速度非常快。

- **[中] #944 [CLOSED] PII redactor falsely matches date/time output as phone numbers**
    - PII脱敏误报问题，已在PR #945中得到修复。

- **[低] #937 [CLOSED] Dead flag in agent config**
    - `compact_context` 标志无效问题，已在PR #939中得到修复。

## 6. 功能请求与路线图信号

- **新功能请求：** 无明确的新功能请求Issue被开设。
- **路线图信号：**
    - **多提供商支持增强：** PR #947（Evolink集成）和PR #940（自定义提供商修复）表明，**广泛的AI后端兼容性**正在成为项目的核心优势。
    - **跨Agent记忆与协作：** PR #711（跨内存事件流）的合并是一个强烈的信号，表明`DonPrus`和项目维护者正在积极探索**基于事件驱动的多Agent记忆同步**。这很可能成为下一版本迭代的主线功能之一。
    - **Agent任务可靠性：** 针对Cron Job的Bug (#941) 及其对应的修复PR (#948) 表明，确保**Agent后台任务**的可靠执行是当前阶段的重点工作。

## 7. 用户反馈摘要

- **痛点：** 用户 `weissfl` 经历了 **Cron Job Agent完全不可用** 的严重问题，这直接打击了用户在自动化场景下的使用信心。
- **使用场景：** 用户 `weissfl` 正在尝试使用 `schedule` 功能设置定时Agent任务（`job_type: "agent"`），并通过Telegram接收结果，这是一个典型的“自动化工作流”场景。
- **满意点：** 从多个Bug（#936, #937, #942, #944）的快速修复和关闭来看，社区贡献者对项目维护者的响应速度和质量应该是比较满意的。特别是 `raskevichai` 和 `vernonstinebaker` 两位贡献者，他们不仅报告了问题，还提交了高质量的修复代码。

## 8. 待处理积压

- **[严重] PR #948 [OPEN] fix cron agent delivery attribution**
    - 链接: [PR #948](https://github.com/nullclaw/nullclaw/pull/948)
    - **建议：** **强烈建议维护者优先审核并合并此PR。** 它直接解决了当前唯一开放的严重Bug（#941），该Bug破坏了Cron Job Agent的核心功能。延迟合并将使受影响的用户持续无法使用此功能。

- **[建议] Issues with low user engagement but long creation time:**
    - 无此类型Issue需要特别提醒。所有超过一周的旧Issue（#936, #937, #941, #942, #944）均已通过Corresponding的PR得到解决。项目积压清理情况良好。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 IronClaw GitHub 数据，我为您生成 2026-06-10 的项目动态日报。

---

## IronClaw 项目动态日报 — 2026-06-10

### 1. 今日速览

今日 IronClaw 项目保持**极高活跃度**。过去 24 小时内，Issues 和 PR 的更新量巨大（共约 98 条），主要集中在 **Reborn 生产环境就绪**、**WebUI v2 测试覆盖率**、以及**安全审计与治理**三大方向。尽管当日无新版本发布，但项目正经历密集的代码重构、功能增强和测试补全阶段，为重大版本发布做准备。核心贡献者和社区成员均积极参与，显示出项目健康、快速迭代的良好态势。

### 2. 版本发布

无。

### 3. 项目进展

今日合并/关闭了 5 个 PR 和 5 个 Issues，标志着以下关键进度的完成：

- **自动化与运营基础**：
    - `#4591 [CLOSED]` [Operator command-plane foundation](https://github.com/nearai/ironclaw/issues/4591)：建立了 Reborn 的运维命令行基础，为后续的配置、诊断和生命周期管理 API 铺平了道路。
    - `#4447 [CLOSED]` [Close OpenAI-compatible API migration](https://github.com/nearai/ironclaw/issues/4447)：完成了 OpenAI 兼容 API 的迁移收尾工作，通过了兼容性与安全测试，是项目向 Reborn 架构迈进的关键里程碑。
- **前端测试覆盖**：
    - `#4604 [CLOSED]` [Reborn WebUI v2 E2E test](https://github.com/nearai/ironclaw/issues/4604)：承认了缺乏浏览器驱动的全栈 E2E 测试，表明项目开始正视并解决可测试性问题。
    - `#4609 [CLOSED]` [Audit & test authentication parity for WebChat v2](https://github.com/nearai/ironclaw/issues/4609)：完成了对 WebUI v2 认证机制的审计和测试，确保了与 v1 版的身份验证能力对等。
- **新工具引入**：
    - `#4669 [CLOSED]` [Added thermo-nuclear code quality review skill](https://github.com/nearai/ironclaw/pull/4669)：合并了一个新的、极其严格的代码审查技能，旨在提升项目整体的代码结构和质量，体现了团队对代码品质的追求。

**总结**：项目在核心架构（Reborn）的收尾、运维能力、测试覆盖率和开发流程改进上均取得了实质性进展。

### 4. 社区热点

今日社区讨论的焦点主要集中在以下几个议题：

- **Reborn 生产就绪** (`#3026`)：作为 Reborn 版本上线前的终极父 Issue，其 3 条评论虽然不算多，但讨论的价值极高，涉及生产流量切换、图构建、验证和回滚等关键决策。它代表了社区对项目最终交付的关切。
- **Strict-mode LLM 兼容性 Bug** (`#4642`)：这个问题引起了开发者的关注，因为它直接影响了与主流 LLM 提供商的集成。用户反馈说，当使用严格的 LLM Provider 时，工具调用会因为 `null` 值与 Schema 校验失败而中断。这暴露了 Reborn 在 Schema 验证上的一个边界情况，是集成其他 AI 模型的核心痛点。
- **安全审计与治理**：一组由 `zmanian` 提交的 PR（`#4561, #4562, #4563, #4565`）围绕安全审计日志进行了大量修补，包括记录 MCP 授权拒绝、认证延续失败、凭据泄露和敏感数据外泄等事件。这说明社区和安全维护者正在积极构建一个可审计、可观测的安全框架，这通常是大型企业部署的刚需。
- **项目规模化与代码健康**：`#4666` 和 `#4665` 关于文件过大（>3000行）的 Issue 被提出，并被标记为追踪 Issue。这反映社区和个人开发者对代码库长期健康和可维护性的关注，是项目走向成熟的重要信号。

### 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题按严重程度排列如下：

- **高 - 集成阻断**:
    - **`#4548`** [[Bug] Chat completion request serializes duplicate top-level `model` field](https://github.com/nearai/ironclaw/issues/4548)：当请求中包含 tools 时，请求体中会序列化出两个 `model` 字段，导致 DeepSeek API 返回 400 错误。这是一个严重的集成 Bug，直接影响了 DeepSeek 支持。**当前无 fix PR**。
    - **`#4640`** [[Bug] Reborn gsuite google-calendar list_events returns oldest/unordered events](https://github.com/nearai/ironclaw/issues/4640)：Google Calendar 的 `list_events` 功能由于缺少默认的下限时间参数，导致返回了“最旧”的日程，且排序错误。这严重影响了用户体验。**当前无 fix PR**。

- **中 - 功能异常**:
    - **`#4642`** [[Bug] Strict-mode providers' null-for-unset-optionals rejected by capability-port validation](https://github.com/nearai/ironclaw/issues/4642)：与主流 LLM Provider 工具调用的 Schema 兼容性问题，影响广泛。**当前无 fix PR**。
    - **`#4587`** [[Bug] Cannot configure Minimax provider](https://github.com/nearai/ironclaw/issues/4587)：用户无法配置 Minimax Provider，因为密钥元数据读取失败。**当前无 fix PR**。

- **低 - 安全与代码健康**:
    - `#4585` **[] Reborn auth evidence should carry tenant identity**：认证凭据缺少租户信息，阻碍了多租户相关的验证。**当前无 fix PR**。
    - `#4666` & `#4665`：文件过大，接近或超过代码库规定的标准，有引发可维护性问题的风险。

### 6. 功能请求与路线图信号

今日活跃的功能请求如下，它们可能成为下一版本的重点：

- **下一代功能特性 (P0/P1)**
    - **`#4647`** [[Enhancement] Unified (omni) search](https://github.com/nearai/ironclaw/issues/4647)：提议在 Reborn WebUI v2 中实现跨线程、技能、扩展和记忆的全局搜索。这是一个重大功能，将极大提升用户体验。
    - **`#4644`** [[Enhancement] Universal attachments across all channels](https://github.com/nearai/ironclaw/issues/4644)：旨在统一跨所有频道的附件处理，解决当前附件在 Reborn (v2) 中静默丢弃的问题。关联的 PR `#4654` 和 `#4670` 已经开始实施，标志着该功能请求正在被积极接纳。
    - **`#4625`** [[Enhancement] Slack channel-routed personal and team agents](https://github.com/nearai/ironclaw/issues/4625)：提出将 Slack 作为一个统一的“频道优先”交互入口，支持个人和团队 Agent。这显示了项目向产品化、多 Agent 协作平台发展的信号。
    - **`#4628`** [[Enhancement] Admin-shared tools and skills with per-user auth](https://github.com/nearai/ironclaw/issues/4628)：提出“管理员预配置、用户按需使用”的企业级工具和技能管理模式，这是多租户场景下的刚需。

- **路线图信号**：从 `#3026` 的讨论以及 `#4591` 的关闭可以看出，**“使 Reborn 具备生产就绪能力”是当前最核心的路线图方向**。同时，大量关于安全审计（`#4561` 等系列 PR）和多租户（`#4585`, `#4628`）的讨论表明，安全和企业级特性正在从功能请求转向实际开发。

### 7. 用户反馈摘要

从今日的 Issues 和评论中，可以提炼出以下用户痛点与期望：

- **集成痛苦**：用户在使用第三方 AI 服务（如 DeepSeek、Minimax）和 Google 服务（Calendar）时，遇到了直接的与 Schema 校验或功能逻辑相关的硬性 Bug，导致无法正常使用。这反映出 Reborn 在跨 Provider 和服务的兼容性测试上还存在盲区。
- **期待“多 Agent”生态**：从 `#4625` 关于 Slack 多 Agent 路由的提议可以看出，用户不满足于只与一个聊天机器人对话，而是期望一个能支持团队协作、个人助手共存的平台级体验。
- **关注可观测性与安全**：大量关于安全审计的 PR（`#4561` 等）虽然主要来自核心贡献者，但它们间接反映了用户（特别是企业用户）对于可审计、可追踪的安全能力的高度关注，这通常是部署到生产环境的关键前提。
- **对代码健康的不安**：`#4666` 和 `#4665` 被提出，表明社区已经开始主动关注代码库的“技术债”（如文件过大），并期望维护者能持续进行重构以保持代码的清晰性和可维护性。

### 8. 待处理积压

- **关键依赖项等待合并**：**`#3708` (Release PR)** 已经等待了近 25 天。这个 PR 包含了 `ironclaw_common` 和 `ironclaw` 的重大版本更新，其长期开放可能阻塞了依赖这些新版 crate 的其他开发和测试工作。维护者应优先处理此 PR。
- **长期未闭环的 Epic**：**`#3026` (Reborn production wiring and cutover readiness)** 作为重要的父 Issue，虽然近期有增加子 Issue，但自身已存在超过 40 天。需要持续关注其最终状态，确保所有依赖的子任务被有效推进和关闭。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的LobsterAI GitHub数据，我为您生成了2026年6月10日的项目动态日报。

---

### LobsterAI 项目动态日报 | 2026年6月10日

**分析师点评：** 今日项目活跃度**较高**，Pull Request（PR）合并/关闭速度快，显示开发团队积极响应用户需求并推进内部优化。社区讨论聚焦于多Agent协同的**跨模型任务调用**和**任务完成通知**，这两者均是提升用户体验和生产力的关键点。整体项目健康度良好。

---

### 1. 今日速览

*   **协作机制成焦点**：社区高度关注跨模型子任务协作的稳定性与反馈机制，Issue #2132 揭示了当前实现中的一个潜在缺陷。
*   **任务通知功能完善**：多项PR集中在“任务完成通知”功能上，从核心实现到Bug修复，表明该功能即将进入稳定发布阶段。
*   **数据备份功能波动**：功能“数据备份与迁移”在一小时内经历了“发布”和“关闭”的快速迭代，可能存在紧急问题需修复。
*   **修复持续进行**：除了新功能，团队也在积极修复导出和代码复制等常规Bug，保持产品稳定性。
*   **社区响应积极**：PR在创建后迅速被合并（多为同一天），体现了高效的内部协作和代码审查流程。

### 3. 项目进展

今日有4个PR被合并/关闭，推进了以下关键领域：

*   **任务完成通知机制成熟**：这是今日最显著的进展。
    *   **[已合并] PR #2130**: 添加了基础的任务完成通知功能，包括通用设置开关、隐私安全的系统通知以及macOS/Windows的任务栏徽章。这是提升后台运行体验的重要功能。
    *   **[已合并] PR #2134**: 进一步增强了该机制。它允许从后台的系统通知中恢复（Restore）LobsterAI主窗口，并确保在通知处理器就绪后再打开目标窗口，解决了一个关键的时序问题。此外，还修复了macOS通知中心点击无响应的问题。
*   **数据备份功能初现**：
    *   **[已合并] PR #2136**: 引入了“数据备份与迁移”功能，为核心数据的安全性提供了保障。
    *   **[已关闭] PR #2135**: 临时关闭了数据备份功能。这暗示PR #2136中可能发现了未预料的副作用或稳定性问题，团队选择暂时回滚以进行后续优化。

**整体来看**，项目在“任务完成通知”这一用户体验优化上取得了实质性突破，工程完整度很高。数据备份功能则处于“试水-发现问题-回滚”的快速迭代周期中。

### 4. 社区热点

*   **热点 Issue #2132: 跨模型子任务调用问题**
    *   **链接**: [Issue #2132](netease-youdao/LobsterAI Issue #2132)
    *   **诉求分析**: 用户 `woxinsj` 提出了一个极其专业且典型的AI Agent协作痛点：主任务模型（如M3）擅长规划，子任务模型（如DeepSeek）擅长快速执行，但两者之间的通信和状态同步存在问题。用户还深入分析了根因，指出“`call_function_...`”是一个“网关级函数调用”，并非由系统创建的子任务（`sessions_spawn`），导致主任务无法知晓其完成状态。这背后反映了用户对**异构模型可靠协作**的迫切需求，希望构建一个稳定、高效的Agent工作流。

### 5. Bug 与稳定性

*   **严重 Bug：跨模型子任务协作状态丢失**
    *   **报告**: Issue #2132
    *   **描述**: 用户通过深入排查，发现跨模型子任务（网关级函数调用）完成后，主任务无法收到通知，导致任务流中断。
    *   **严重程度**: **高**。该问题直接破坏了多Agent协作的核心逻辑，影响用户构建复杂工作流。
    *   **修复状态**: 尚无关联的Fix PR，但Issue本身提供了详细的根因分析和修复建议，对开发者极具价值。

### 6. 功能请求与路线图信号

*   **Hermes Agent支持 (Issue #2131)**: 用户询问是否支持“Hermes Agent”。
    *   **信号分析**: 这表明社区中有一批用户关注特定Agent框架或协议的兼容性。由于暂无更多讨论和关联PR，短期内纳入路线图的可能性较低，但可以作为未来扩展性的一个潜在方向。
*   **跨模型子任务协作优化 (Issue #2132)**: 用户不仅报告Bug，还提出了两个具体的优化方案（1. 借鉴同模型通知机制；2. 子任务主动通知主任务）。
    *   **信号分析**: 这是一个非常强烈的**路线图信号**。该问题指出了当前架构在跨模型通信上的一个明显短板。结合今日已合并的“任务完成通知”相关PR，可以预判，**下一版本很可能包含对跨Agent/跨模型任务通知机制的深度修复和优化**。这将是使LobsterAI成为一个可靠的多Agent平台的关键一步。

### 7. 用户反馈摘要

*   **深入的技术洞察**: 用户 `woxinsj` (Issue #2132) 是典型的**高级用户或开发者**。他们不仅报告问题，还自行进行了源码级别的排查（通过检查`call_function_`调用不在`sessions_list`中），并给出了具体的修复和优化思路。这种高质量的反馈对项目发展极具价值。
*   **前瞻性需求**: 用户 `wtgoku-create` (Issue #2131) 提出了对未来Agent生态兼容性的期待，反映了用户希望LobsterAI能成为一个开放、可扩展的Agent平台。

### 8. 待处理积压

*   **待处理的重要Issue**: **Issue #2132**。虽然昨日创建，但因其涉及多Agent协作的核心缺陷，且已有详尽分析，应被列为最高优先级进行讨论和修复。
*   **待合并PR**: **PR #2133**。该PR旨在修复导出和代码复制Bug，属于稳定性维护。鉴于今日从PR创建到合并的速度很快，该PR预计也将在短期内得到处理。

**总结**：LobsterAI正处于一个积极的功能开发和问题修复周期中。任务通知功能的完善是其迈向成熟的多Agent工作平台的重要一步。社区对跨模型协作的深度讨论，为项目未来的架构演进指明了清晰的方向。当前主要风险点在于数据备份功能的稳定性以及跨模型协作的核心缺陷。

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的CoPaw (GitHub: agentscope-ai/CoPaw) 项目数据，我将为您生成一份2026年6月10日的项目动态日报。

---

# CoPaw 项目日报 | 2026-06-10

## 1. 今日速览

今日CoPaw项目呈现出**高度活跃**的状态。过去24小时内，社区贡献者提交了35个PR，并围绕37个Issue展开了密集讨论。项目不仅发布了新的Beta版本（v1.1.11-beta.2），在**前端交互体验优化**、**模型兼容性修复**及**安全增强**方面取得了显著进展，解决了多个用户反馈的痛点问题。特别值得关注的是，关于**引入“学习循环”机制**和**迁移至AgentScope 2.0**的讨论热度很高，预示着项目未来可能迎来重大架构升级。总体而言，项目社区生态健康，核心团队响应迅速，正处于一个积极迭代、快速前进的时期。

## 2. 版本发布

项目昨日发布了 **v1.1.11-beta.2** 版本。

- **发布链接**: [Releases v1.1.11-beta.2](https://github.com/agentscope-ai/CoPaw/releases/tag/v1.1.11-beta.2)
- **主要更新内容**:
    - **功能**: `feat(browser)`: 为浏览器控制功能增加了**页面坐标点击支持**，提升了自动化操作的精确性 (PR #4905)。
    - **修复**: `fix(browser)`: 修复了跨浏览器切换时的CDP超时参数和**浏览器配置文件隔离**问题，提升了多浏览器场景的稳定性 (PR #4905)。
- **破坏性变更**: 本次发布无明确的“破坏性变更”声明或需要特别关注的迁移注意事项。

## 3. 项目进展

昨日合并/关闭了15个PR，主要围绕以下方面推进：

- **核心架构与稳定性**:
    - **AgentScope 2.0 迁移**: 虽然`#4727` Issue仍为Open状态，但社区已围绕该计划展开讨论，这是项目后端架构升级的关键一步。
    - **CI/测试基础设施**: 合并了多个与CI相关的PR（`#5056`, `#5054`, `#5058`），包括移除重复工作流、完成端到端(E2E)测试集成管线，以及新增60个集成测试用例，显著提升了代码质量和项目健壮性。
- **安全与功能增强**:
    - **安全增强**: PR `#5043` 合并，添加了 **OpenSandbox 插件**。该插件通过MCP协议集成了沙箱运行能力，可在隔离环境中执行shell命令或不可信代码，显著提升了Agent使用的安全性。
    - **用户体验提升**: PR `#5050` 合并，将系统主题切换图标从“计算机”改为“太阳”，提升了UI的直观性。
- **生态与集成**:
    - **通过MCP集成OpenSandbox**: 引入了安全执行环境。
    - **技能自进化框架**: PR `#4857`（已合并）增强了技能创建流程，支持后台创建及自进化技能，这是迈向“学习循环”的重要一步。

## 4. 社区热点

今日讨论热度最高的议题集中在社区对项目未来发展的期望，以及对新模型和功能的急切需求。

- **`#5017` [Feature]: 建议关注 Hermes Agent 的发展**: 该Issue获得了10条评论和3个点赞，是今日最热话题。用户`tecgic`（[链接](https://github.com/agentscope-ai/CoPaw/issues/5017)）高度赞扬CoPaw本地化体验的同时，建议项目借鉴 Hermes Agent 的**学习循环 (Learning Loop)** 机制，让Agent能自动从行为中创建并迭代技能。这反映了用户对**Agent自主进化能力**的迫切需求，也预示着CoPaw未来可能向更强的自动化和智能体方向演进。
- **`#5003` [Bug]: 使用阿里coding plan qwen3.7-plus会一直卡住**: 该Bug报告（[链接](https://github.com/agentscope-ai/CoPaw/issues/5003)）获得了8条评论，表明用户在实际使用特定模型（如通义千问）进行编码任务时遇到了严重阻塞，这影响了核心工作流。用户期待快速修复。

## 5. Bug 与稳定性

昨日报告的Bug数量较多，涉及多个方面，按严重程度排列如下：

**严重**:
- **`#5045` [Bug]: DeepSeek API 因 Tool 名称包含点号被拒绝**: 核心Agent功能受阻，因为`PAT`批量授权系统的Tool命名（`pat.batch_plan`）不符合DeepSeek API的`^[a-zA-Z0-9_-]+$`正则规则。**(已关闭，疑似修复中)** ([链接](https://github.com/agentscope-ai/CoPaw/issues/5045))
- **`#5034` [Bug]: MCP 工具名称包含非法字符导致 OpenAI API 报错 400**: 与`#5045`类似，MCP服务中的工具名如 `pat.batch_plan` 也因点号导致API调用失败。**(已关闭，已有修复PR)** ([链接](https://github.com/agentscope-ai/CoPaw/issues/5034))

**中/低等**:
- **`#5015` [Bug]: Windows Desktop 版本前端加载不流畅**: 任务执行时CPU激增，会话切换卡顿，影响日常使用体验。（[链接](https://github.com/agentscope-ai/CoPaw/issues/5015)）
- **`#4989` [Bug]: 1.1.9/1.1.10 版本使用本地部署千问模型无响应**: 一个影响特定版本和模型配置的重大回归问题。（[链接](https://github.com/agentscope-ai/CoPaw/issues/4989)）
- **`#5044` [Bug]: Tauri 桌面版外部链接无法打开 & 文件下载被阻止**: 架构问题导致桌面版功能受限。（[链接](https://github.com/agentscope-ai/CoPaw/issues/5044)）
- **`#5042` [Bug]: Windows下无法打开 C盘外的代码目录**: 功能受限，影响使用非C盘作为工作目录的用户。（[链接](https://github.com/agentscope-ai/CoPaw/issues/5042)）

## 6. 功能请求与路线图信号

用户提出了多项有价值的功能请求，部分已有对应的PR，未来可能被纳入路线图：

- **视觉模型回退（Visual Model Fallback） (#4992)**: 用户建议增加独立的视觉模型配置，当主模型不支持多模态时自动调用，解决纯文本模型无法处理图片的问题。这是一个高价值且实现思路清晰的功能请求。 ([链接](https://github.com/agentscope-ai/CoPaw/issues/4992))
- **记忆系统自进化 (#4994)**: 用户`rescodexa`建议项目参考主流Agent的分层记忆系统框架，增强记忆系统的自进化能力。这与`#5017`中关于“学习循环”的讨论相呼应，共同指向了Agent自我提升的核心方向。 ([链接](https://github.com/agentscope-ai/CoPaw/issues/4994))
- **可观测性集成 (#4057, #5009)**: 多位用户（`lin01109`, `flyrae`）希望CoPaw能集成Langfuse、OpenTelemetry、Arize等可观测性平台，用于监控、追踪和调试Agent行为。这显示了企业级用户对平台可观测性的强烈需求。 ([链接](https://github.com/agentscope-ai/CoPaw/issues/4057)), ([链接](https://github.com/agentscope-ai/CoPaw/issues/5009))
- **零配置免费模型 / OAuth一键认证 (#5049)**: 对应的PR `#5049` 已关闭，表明官方已经在计划或实现“开箱即用”的免费模型体验。这必将降低新用户的上手门槛，吸引更多用户。

## 7. 用户反馈摘要

从Issue评论中可以看出，用户整体对CoPaw的体验是满意的，但也存在明显痛点：

- **正面反馈**:
    - 用户`tecgic`在`#5017`中赞扬CoPaw“**国内用起来特别舒服——本地化做得很到位，设置清晰无门槛，开箱即用**”，这是项目优秀的本地化体验得到认可的明证。
- **核心痛点**:
    - **前端性能问题**: 多位用户（`#5015`, `#4917`, `#4792`）反馈前端（尤其是会话切换、流式输出时）存在严重卡顿问题，导致“**系统级性能崩溃**”，影响基本使用。
    - **模型兼容性与配置问题**: 用户在使用多种模型（如DeepSeek, KimiCode, 本地部署千问）时遭遇兼容性问题（`#5045`, `#5013`, `#4989`）和配置Bug（`#4666`，`#4937`），说明模型集成层的鲁棒性有待加强。
    - **桌面端体验降级**: 切换到Tauri后，启动慢（`#5047`）和功能受限（`#5044`）成为Tauri桌面版用户的突出抱怨。
- **特色反馈**:
    - 用户`MacBeth`在`#5045`中不仅报告了DeepSeek API的兼容性Bug，还深入分析了根因（Tool name格式不匹配），体现了较高的技术水平，这种高质量的反馈对项目非常有帮助。
    - 用户`lihxiao`在`#5025`和`#4988`中详细报告了 `submit_to_agent` 功能的文件路径Bug，并给出了复现步骤和根因分析，对开发者定位和修复问题极有价值。

## 8. 待处理积压

以下为核心或长期未解决的重要Issue/PR，建议项目维护者关注：

- **`#4727` [Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0** (创建于2026-05-27): 这是项目目前最重要的架构升级议题，虽然讨论热烈，但状态仍为`OPEN`，需要核心团队给出更明确的计划和进展。 ([链接](https://github.com/agentscope-ai/CoPaw/issues/4727))
- **`#4669` feat(desktop): add tauri auto updater** (OPEN, 自2026-05-25): 为Tauri桌面版添加自动更新功能是解决`#5044`等问题的关键，但该PR仍处于Open状态，建议尽快推进。([链接](https://github.com/agentscope-ai/CoPaw/pull/4669))
- **`#4057` [Question]: Support AgentScope tracing initialization** (创建于2026-05-06): 关于可观测性的早期讨论，虽已有一个月，但关联的`#5009` Issue显示用户持续关注。需要官方对可观测性路线图给出回应。([链接](https://github.com/agentscope-ai/CoPaw/issues/4057))

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是为您生成的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-10

## 1. 今日速览
ZeroClaw 项目今日处于**高活跃度**状态，社区贡献和核心开发者在多个关键领域持续发力。过去24小时内，项目共产生50条 Issue 和50条 PR 更新，呈现出典型的“高产”模式。虽然无新版本发布，但大量高优先级（P1）的 Bug 修复和功能增强 PR 已进入待合并状态，表明项目团队正在为下一个重要版本进行密集的代码整合与质量打磨。主要关注点集中在运行时稳定性（内存、Cron、SubAgent）、安全增强（MCP工具权限、子进程资源限制）以及多通道（Telegram、Matrix）的兼容性修复上。

## 2. 版本发布
**无**

## 3. 项目进展
过去24小时，项目重点推进了以下关键修复与功能，整体向更稳定、更安全的架构迈进：

- **运行时与工具栈稳定性修复：**
    - **PR #7444** (待合并): 修复了 zerocode Dashboard 在加载、错误及活动会话状态下的标签显示问题，提升了用户体验。
    - **PR #7442** (待合并): 修复了并行执行 SubAgent 和 Delegate 时无法可靠返回结果的问题，对分布式代理场景至关重要。
    - **PR #7440** (待合并): 优化了上下文窗口管理，在系统提示词超出预算时跳过无效的历史记录修剪，避免无限循环。
    - **PR #7348** (待合并): 修复了 `catch_up_on_startup` 配置无效的问题，现在当该选项禁用时，启动时不会再执行积压的 Cron 任务。

- **渠道与Provider适配修复：**
    - **PR #7423** (待合并): 修复了 OpenAI兼容的 Provider（如 OpenRouter）在多轮对话中丢失 `reasoning` 字段的关键问题，确保推理过程可追踪。
    - **PR #7349** (待合并): 修复了 Matrix 渠道在 `reply_in_thread` 开启时，会将自身消息锚点误作为对话中断边界的 Bug。
    - **PR #7350** (待合并): 为独立的 Azure OpenAI Provider 接入了 `reasoning_effort` 参数，使其能控制推理模型的输出深度。

- **开发体验与文档优化：**
    - **PR #7365** (待合并): 对项目官方手册（`mdBook`）进行了大规模重写，使其结构更清晰，并重构了 Provider/配置的文档生成方式。
    - **PR #7443** (待合并): 更新了 `CODEOWNERS` 文件，用以反映贡献者角色的变动，维护项目治理结构。

## 4. 社区热点
- **[Issue #4710 - A better LOGO of Zeroclaw] (已关闭)**
    - **链接:** [Issue #4710](https://github.com/zeroclaw-labs/zeroclaw/issues/4710)
    - **分析:** 该 Issue 收获了19条评论，是今日讨论最热烈的话题，并最终被关闭。这反映了社区成员对项目品牌形象的强烈热情和参与感。虽然功能层面无实质影响，但此类议题有助于增强社区凝聚力。

- **[Issue #5862 - Agent 不知道可以添加 Cron]**
    - **链接:** [Issue #5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)
    - **分析:** 这是一个典型的“交互鸿沟”问题。用户期望通过自然语言指令让ZeroClaw设置定时任务，但Agent的内部能力（`zeroclaw cron`）未能正确暴露或与用户的意图匹配。该问题提示维护者需要优化 Agent 的工具调用提示和内部能力感知。

- **[Issue #6034 - 单/多轮对话丢失用户消息]**
    - **链接:** [Issue #6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034)
    - **分析:** 这是一个S1（工作流阻塞）级别的Bug，用户通过自定义API与本地模型Qwen3.5对话时遇到400错误。此类问题直接影响到使用本地或非标准提供商的核心用户群，是项目稳定性的关键痛点。

- **[Issue #6037 - Cron 任务可被重复触发]**
    - **链接:** [Issue #6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037)
    - **分析:** 一个高风险Bug，指出如果Cron任务执行时间超过调度轮询间隔，会被重复启动，导致资源轰炸。该问题已标记为“进行中”，说明核心开发团队已着手解决。社区对此类影响生产环境稳定性的问题反应强烈。

## 5. Bug 与稳定性
**高优先级 (P1 / 高风险):**

- **内存与上下文管理：**
    - **Issue #5844:** 系统提示词过分强调记忆，导致在Cron作业等场景下忽视当前Prmopt。`[状态: 已接受]`
    - **Issue #5808:** 默认32k上下文预算在第一次迭代时就被系统提示和工具定义超支，导致持续预修剪，工作流被阻塞。`[状态: 已接受]`
- **运行时与通道阻塞：**
    - **Issue #6034:** 单/多轮对话丢失用户消息（400错误）。`[状态: 已接受]`
    - **Issue #6646:** Telegram 通道下 `web_search_tool` 和 `web_fetch` 工具无法触发。`[状态: 已接受]` **已有对应修复 PR #7438。**
    - **Issue #6721:** `tool_search` 不在自动批准列表中，导致 MCP 工具通过 webhook 加载时静默挂起120秒后自动拒绝。`[状态: 已接受]`
    - **Issue #6037:** Cron 任务可被重复触发。`[状态: 进行中]`

**中优先级 (P2 / 中风险):**

- **Provider 兼容性问题：**
    - **Issue #6584:** OpenAI兼容 Provider 无法解析 `reasoning` 字段，只识别 `reasoning_content`。`[状态: 已接受]` **已有对应修复 PR #7423。**
- **配置与安全：**
    - **Issue #6876:** `risk_profile.allowed_tools` 配置无法约束 MCP 工具的使用，存在设计或文档缺口。`[状态: 已接受]`
    - **Issue #6862:** Gateway SPA 为未实现的 `/api/*` 路由错误返回 `index.html`，导致 Dashboard 崩溃。`[状态: 已接受]`
- **zerocode TUI 体验：**
    - **Issue #7376:** Dashboard 隐藏了不可用/错误状态，且将历史会话错误标记为活跃。`[状态: 已接受]` **已有对应修复 PR #7444。**
    - **Issue #7377:** 深色主题可继承终端不可读的前景色，影响可读性。`[状态: 已接受]`
    - **Issue #7378:** macOS 下 Cmd-C 复制操作会触发退出快捷键。`[状态: 已接受]`

## 6. 功能请求与路线图信号
- **安全与多租户：**
    - **Issue #5982:** 提出为单实例 ZeroClaw 增加基于发送者的 RBAC（角色权限控制），隔离不同用户的工作空间和工具集。`[需作者操作]` 这是一个重大功能，暗示可能考虑企业级部署场景。
    - **Issue #6916:** 提议对 shell/skill 子进程执行添加内存限制，防范 OOM 攻击。`[已接受]` 与安全性增强方向一致。
- **架构重构：**
    - **Issue #5937:** 提出重构 Provider 架构，统一 `reqwest` 客户端管理和模型参数构建。`[已接受]` 这表明项目正在解决代码库中的历史遗留问题，提升可维护性。
- **渠道与配置优化：**
    - **Issue #6378:** 希望 Discord Bot 能在特定频道中响应，类似 Matrix 的 `allowed_rooms` 配置。`[已接受]` 这反映了用户对精细化渠道控制的需求。
    - **Issue #7248:** 提议持久化 Provider返回的缓存输入令牌，并纳入成本核算。`[已接受]` 对运营成本敏感的用户尤为重要。

## 7. 用户反馈摘要
- **痛点：** “Agent不知道它能做某事”是核心痛点。用户期望通过自然语言直接操作，但Agent内部能力未能打通，导致体验断裂（#5862）。
- **稳定性抱怨：** 多用户反馈在 Telegram（#6646）、自定义API（#6034）等渠道上使用工具或对话时出现阻塞或错误，对稳定性有较高期待。
- **使用场景：** 用户正在将 ZeroClaw 用于定时任务（#6037, #5844），这表明该项目已从一个单纯对话机器人向自动化代理演进。
- **硬件需求：** 在 Docker 容器中运行本地模型（如 llama.cpp, Qwen）并暴露给 ZeroClaw 是一个常见的部署场景，因此 Provider 兼容性和错误信息的意义重大。
- **正向反馈：** 社区对品牌建设（#4710 Logo）和功能增强（#5982 RBAC, #6378 频道白名单）表现出积极兴趣，说明用户不仅仅是使用者，更是生态共建者。

## 8. 待处理积压
- **Issue #5862 [Agent不识别Cron能力]:** 自2026-04-18创建，已有12条评论。核心问题在于 Agent 的能力边界未被正确传达给用户和自身。虽已标记为需作者操作且阻塞，但作为高频交互痛点，**建议核心维护团队**尽快评估并确定修复方案，如改进系统提示词或增加工具内省能力。
- **Issue #5775 [按技能区分安全权限]:** 一个高风险的功能增强请求，自2026-04-15起被标记为需“作者操作”，并处于阻塞状态。考虑到项目目前对安全性的高度重视（多个相关Issue和PR），此功能若能与现有安全架构整合，将填补一个重要的功能缺口。
- **Issue #5982 [多租户 RBAC]:** 功能规模较大，自2026-04-22创建后因缺少作者反馈而阻塞。作为企业级场景的核心需求，**建议专人跟进**，评估其与主干路线的契合度，并引导社区贡献者完成设计或关闭。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*