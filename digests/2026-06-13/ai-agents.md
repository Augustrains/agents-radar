# OpenClaw 生态日报 2026-06-13

> Issues: 500 | PRs: 486 | 覆盖项目: 13 个 | 生成时间: 2026-06-13 02:03 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw 项目数据，为您生成 2026-06-13 的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-13

## 1. 今日速览

今日 OpenClaw 项目社区活跃度极高。过去24小时内，共产生 **500 条 Issue 与 486 条 PR 互动**，显示开发与用户反馈都处于高频状态。两个新的补丁版本（`v2026.6.6` 和 `v2026.6.6-beta.2`）已发布，核心亮点是**大幅收紧安全边界**，覆盖了沙箱、代码执行、消息通道等多个领域。此外，社区关注的**内存泄漏**、**会话混乱**等关键 Bug 及多项功能请求仍在激烈讨论中。

- **项目健康度评估**：⭐⭐⭐⭐ (高度活跃，安全加固积极，但关键 Bug 仍需尽快解决)
- **社区活跃度**：极高，Issue/PR 响应迅速。
- **发布节奏**：快速，针对安全问题进行点发布。

## 2. 版本发布

过去24小时发布了 **2 个新版本**：

- **v2026.6.6** 与 **v2026.6.6-beta.2**：
    - **核心更新内容**：两个版本均标示为安全边界大幅收紧。涉及领域广泛，包括：
        - **消息安全**：`transcripts`（会话记录）、`MCP stdio`、`Codex HTTP access`、`loopback tools`（回环工具）。
        - **平台安全**：`Discord moderation`（Discord 管理）、`Teams group actions`（Teams 组操作）。
        - **进程与环境隔离**：`sandbox binds`（沙箱绑定）、`host environment inheritance`（主机环境继承）、`native search policy`（原生搜索策略）、`elevated sender checks`（提权发送者检查）、`deleted-agent ACP bypasses`（已删除代理 ACP 绕过）。
        - **执行安全**：`exec` 权限。
    - **破坏性变更**：根据发布说明推测，这些安全收紧可能会导致一些依赖旧有宽松安全策略的配置、脚本或第三方插件失效。特别是沙箱绑定、主机环境继承和 MCP 相关功能。
    - **迁移注意事项**：用户在升级后，应重点检查：
        1. 所有自定义 `sandbox` 配置，确保容器绑定和权限设置符合新要求。
        2. 任何通过 `exec` 工具执行的脚本或命令，可能需要重新评估和配置执行审批。
        3. 检查 Discord、Teams 等渠道管理机器人相关设置，部分权限可能需要重新赋予。

## 3. 项目进展

今日有 **142 个 PR 被合并/关闭** (包括 `v2026.6.6` 版本)，显示项目推进速度很快。以下是一些重要的合并/关闭 PR：

- **功能性修复与拓展**：
    - `#92571` (OPEN): **修复**会话记忆中的重复条目，提升对话质量。
    - `#92357` (CLOSED): **修复**混合搜索（关键字+向量）在 CJK 语言环境下可能丢失搜索结果的问题。
    - `#92308` (CLOSED): **修复** Windows 路径解析问题，改善跨平台兼容性。
    - `#92348` (CLOSED): **修复**飞书（Feishu）Channel 插件中的事件处理问题，防止因特定事件导致网关重启。
    - `#92335` (CLOSED): **修复** exec-approval 的快速路径（YOLO 模式），使其在有节点 socket token 时也能正常工作。
    - `#92427` (CLOSED): **增强** Workshop 技能描述的字数上限（从 160 提升至 500），改善用户体验。
    - `#92319` (CLOSED): **新增** `workboard_delete` 工具和 CLI 命令，完善了工作板管理功能。
    - `#92390` (CLOSED): **修复**出站消息路由问题，确保仅支持 `direct` 聊天的 Channel（如微信）不会错误地创建 `group` 会话。
    - `#92435` (CLOSED): **优化**网关重启策略，`browser.profiles` 配置项变更不再触发 SIGUSR1 重启。
    - `#92396` (CLOSED): **修复** Moonshot/Kimi 模型在长对话中的 `reasoning_content is missing` 400 错误。
    - `#88446` (CLOSED): **增强** Codex 聊天规划功能，新增 `/codex plan` 控制命令。
    - `#92229` (CLOSED): **修复** `doctor preview` 命令对 Channel 密钥引用的解析问题。
    - `#92566` (CLOSED): **修复**插件生命周期清理问题，确保在 leader 进程退出后能正确回收资源。

- **CI/CD 与工程基础设施**：
    - `#92557` (OPEN): 新增 PR 工作流，用于验证 ClawHub 插件包元数据，提升插件生态质量。
    - `#92311` (OPEN): 拆分 ClawHub 插件发布路径，引入更安全的 Bootstrap 流程，增强发布安全性。

**项目总结**：项目在修复 Bug、提升稳定性和优化开发者体验方面有明显进展。安全加固是本次更新的主旋律。

## 4. 社区热点

今日讨论最激烈的 Issue 反映了用户在**安全、稳定性、功能缺失**三方面的核心诉求：

1.  **[#25592] 工具调用间文本泄露 (Text between tool calls leaks)** (评论: 32)
    - **链接**: [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
    - **诉求**: 当 Agent 在工具调用之间产生内部处理文本（如错误信息、确认消息）时，这些文本会被错误地发送到前端聊天频道，造成严重的 UX 问题。这是一个用户高度关注的安全/隐私问题。

2.  **[#9443] 请求提供预构建 Android APK** (评论: 25)
    - **链接**: [Issue #9443](https://github.com/openclaw/openclaw/issues/9443)
    - **诉求**: 用户希望官方能提供预编译的 Android APK 版本，而不是仅提供源码。这表明对移动端正式使用的需求非常迫切。

3.  **[#32473] Control UI 需要 HTTPS 或 localhost 安全上下文** (评论: 17)
    - **链接**: [Issue #32473](https://github.com/openclaw/openclaw/issues/32473)
    - **诉求**: 用户在 VPS 上使用 Docker 部署时，遇到了 Web UI 的设备身份认证问题。这暴露出在非 localhost 环境下，尤其是通过代理或 VPN 访问时，部署和配置门槛较高。

4.  **[#91588] 网关进程内存泄漏，RSS 从 350MB 增长至 15.5GB** (评论: 9)
    - **链接**: [Issue #91588](https://github.com/openclaw/openclaw/issues/91588)
    - **诉求**: 这是一个严重程度为 **P0** 的性能问题。连续运行数天导致网关内存膨胀直至被 OOM 杀死，严重影响生产环境的长期稳定性。用户急需官方定位 root cause 和修复。

## 5. Bug 与稳定性

今日报告的 Bug 中，以下问题严重程度较高：

- **P0**:
    - `#91588`: **网关内存泄漏** (RSS 从350MB到15.5GB)。最严重的稳定性问题。**暂无 Fix PR**。
    - `#91778`: **`memory_search` 功能异常**。自 v2026.6.1 起，向量搜索的索引元数据丢失。**暂无 Fix PR**。

- **P1**:
    - `#91588` (见上)
    - `#25592`: **工具调用间文本泄露**。安全与 UX 问题。**暂无 Fix PR**。
    - `#22676`: **Signal 守护进程重启时的竞态条件**。导致孤儿进程和消息发送失败。**暂无 Fix PR**。
    - `#32296`: **会话上下文混乱**。Agent 回复的是上一条消息而非当前消息。**暂无 Fix PR**。
    - `#29387`: **Agent 目录下的 Bootstrap 文件被忽略**。仅工作空间目录的文件生效。**暂无 Fix PR**。
    - `#57326`: **CLI 路径绕过问题**。即使在最新代码上依然存在。**暂无 Fix PR**。
    - `#31583`: **`exec` 工具不继承技能环境变量**。回归性 Bug。**暂无 Fix PR**。
    - `#83184`: **心跳触发回复导致系统状态“pendingFinalDelivery”卡死**。**暂无 Fix PR**。
    - `#88951`: **消息重复**。升级后出现。**暂无 Fix PR**。
    - `#38327`: **Google Vertex 模型报错“Cannot convert undefined or null to object”**。回归性 Bug。**暂无 Fix PR**。

- **P2 (回归/重要问题)**:
    - `#84644`: **Windows node 连接后无命令**。回归性 Bug。**暂无 Fix PR**。
    - `#38439`: **Webchat 头像 API 返回 404**。回归性 Bug。**暂无 Fix PR**。
    - `#32473`: **Control UI 安全上下文问题**。**暂无 Fix PR**。

## 6. 功能请求与路线图信号

除了安全与稳定性外，社区还在积极推动以下新功能，这些很可能成为下一阶段路线图的一部分：

- **高优先级**：
    - `#22438`: **分级的 Bootstrap 文件加载**。用户希望精细化控制 Agent 的上下文窗口，避免浪费 Token。已有 **PR #92396** 关联，但需求本身的实现较为复杂。
    - `#18160`: **Cron 任务的直接执行模式**。用户希望 Cron 任务能直接执行简单命令，跳过复杂的 LLM AgentTurn 流程，提升可靠性和效率。这反映了对开箱即用、简单任务的优化需求。
    - `#27445`: **子 Agent 完成通知的路由优化**。允许主 Agent 更好地编排多步工作流，而不是直接将子 Agent 结果通知到聊天频道。

- **中优先级**：
    - `#12602`: **Slack Block Kit 支持**。丰富 Agent 响应形式。
    - `#35203`: **多 Agent 协作增强**。涉及能力描述、共享黑板、分层记忆和 Token 成本治理。这是一个大型 RFC，表明社区正在为更复杂的多 Agent 场景做准备。
    - `#16670`: **引导向导应包含记忆/Embedding**。反映新用户设置门槛问题。
    - `#33329`: **为所有隐式服务发现机制增加配置开关**。提升系统启动稳定性和可控性。

## 7. 用户反馈摘要

- **满意度**:
    - **安全加固**: 用户对最新版本的安全更新（收紧安全边界）表示认可（尽管可能存在向上兼容问题）。
    - **活跃维护**: 大量 Issue 在短时间内获得开发者回复和标记，社区对维护响应速度感到满意。

- **痛点与不满意**：
    - **移动端体验差**: `#9443` 表明缺少预编译 APK 是用户使用移动端的一大障碍。
    - **部署门槛高**: `#32473` 和 `#31331` (Docker + 沙箱绑定) 显示非标准环境和 Docker 部署存在较多的配置困难。
    - **关键 Bug 影响生产**: `#91588` (内存泄漏)， `#32296` (会话混乱) 等 Bug 严重影响了用户的日常使用和长期运行稳定性。
    - **功能文档与实际不符**: `#11665` 指出 `/hooks/agent` 的 `sessionKey` 文档描述与实际行为不符，影响开发者信任。
    - **Token 成本担忧**: `#14785` (工具 Schema 开销) 和 `#22438` (Bootstrap 加载) 显示用户对 Token 消耗非常敏感，有强烈的优化需求。

## 8. 待处理积压

以下 Issue 存在时间较长，影响范围广/程度严重，但暂时没有明确的 Fix PR 或审查停滞，需要维护者重点关注：

1.  **`#25592` (2026-02-24)**: **工具调用间文本泄露**。P1，安全 X 消息丢失，评论数最高(32)。这对产品安全形象影响极大，建议优先处理。
2.  **`#22676` (2026-02-21)**: **Signal 守护进程竞态条件**。P1，影响消息传递和系统稳定性（Crash Loop）。
3.  **`#18160` (2026-02-16)**: **Cron 任务直接执行模式**。虽然是一个Feature Request，但社区活跃度极高（👍: 11），且应用场景广泛，建议下一版本中予以考虑。
4.  **`#32296` (2026-03-02)**: **会话上下文混乱**。P1，这是最影响用户聊天体验的 Bug 之一，需要尽快修复。
5.  **`#13583` (2026-02-10)**: **预响应强制执行钩子**。P1，为金融/安全等高风险场景设计，社区讨论热度高。虽无 Fix PR，但反映了部分用户对安全管控的深层需求。
6.  **`#13616` (2026-02-10)**: **添加配置/状态的备份恢复工具**。长期缺乏统一的标准方法，对用户运维是一个不小的风险。

---
以上是今日的 OpenClaw 项目日报。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将基于您提供的各项目日报，为您生成一份全面的横向对比分析报告。

---

### 个人 AI 智能体开源生态分析报告 | 2026-06-13

#### 1. 生态全景

截至2026年6月13日，个人AI智能体/自主智能体开源生态呈现出 **“头部项目主导，功能与安全并重”** 的快速发展态势。**OpenClaw** 与 **NanoBot** 凭借其活跃的社区、高速的迭代和突出的核心能力，稳居生态第一梯队。生态整体关注点正从“如何构建一个Agent”向“如何构建一个**可靠、安全、可感知上下文**的Agent”转移。**性能稳定性（如内存泄漏、消息丢失）与安全性（如权限控制、沙箱隔离）** 是所有成熟项目的共同攻坚方向。此外，Agent的**记忆、长对话连贯性与多Agent协作**已成为社区普遍期望的核心功能，而非加分项。跨渠道集成、本地化部署（移动端、桌面端）和更细粒度的用户权限控制，则是下一阶段用户体验和商业化落地的关键战场。

#### 2. 各项目活跃度对比

| 项目名称 | Issues 更新数 | PR 更新数 | 版本发布 | 项目健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 486 | **是** (v2026.6.6 & beta.2) | ⭐⭐⭐⭐⭐ (高度活跃，安全加固积极) |
| **NanoBot** | 6 (新) | 30 | 无 | ⭐⭐⭐⭐⭐ (高度活跃，核心功能迭代迅猛) |
| **Hermes Agent** | 50 | 50 | 无 | ⭐⭐⭐⭐ (高度活跃，桌面端与平台适配是重心) |
| **IronClaw** | 50 | 50 | 无 | ⭐⭐⭐⭐ (极高活跃度，Reborn引擎密集开发与UI打磨) |
| **CoPaw** | ~50 | ~50 | 无 (准备 v1.1.12b1) | ⭐⭐⭐⭐ (高度活跃，专注于稳定性回归修复和性能提升) |
| **PicoClaw** | 5 (新) | 14 | **是** (Nightly) | ⭐⭐⭐⭐ (活跃，权限控制和协议完善是话题中心) |
| **LobsterAI** | 1 (新) | 11 (关闭) | **是** (v2026.6.11 分支合并) | ⭐⭐⭐⭐ (稳定，社区贡献专注于防内容丢失等细节体验) |
| **NanoClaw** | 5 (更新) | 9 (新) | 无 | ⭐⭐⭐ (高度活跃，安全加固与核心框架扩展性并重) |
| **ZeroClaw** | 14 (新) | 33 (新) | 无 (v0.8.0 后修复期) | ⭐⭐⭐ (高活跃度，聚焦v0.8.0架构重塑后的Bug修复) |
| **NullClaw** | 1 (新) | 3 (新) | 无 | ⭐⭐⭐ (中等活跃，处在稳定性与 Bug 修复的密集期) |
| **Moltis** | 3 (新) | 无 | 无 | ⭐⭐ (中等活跃，社区讨论前瞻性强，但无代码合并) |
| **TinyClaw** | 无 | 无 | 无 | 🌑 (无活动) |
| **ZeptoClaw** | 无 | 无 | 无 | 🌑 (无活动) |

#### 3. OpenClaw 在生态中的定位

**OpenClaw** 在生态中扮演着 **“安全与功能双驱动的引领者”** 角色。

- **优势**：
  - **安全先行**：今日发布的 `v2026.6.6` 版本将“安全边界大幅收紧”作为核心更新，覆盖沙箱、代码执行、消息通道等六大领域。在生态普遍讨论安全问题时，OpenClaw 已率先将其转化为系统性、强制性的版本更新，体现了最高的安全严肃性。
  - **社区规模与成熟度**：OpenClaw 的 Issue/PR 数量级（500/486）远超其他项目（多数在50级别），表明其拥有最庞大的用户和贡献者基础，生态成熟度极高。
  - **生态扩展性**：与 `LobsterAI`（协作用户端）的深度整合，证明了其 Agent 核心的中枢地位及强大的开放能力。

- **技术路线差异**：
  - 相比之下，**NanoBot** 正在通过引入 `tools.audit` 审计模块来建立可观测性，但其侧重点在于“让开发者能看得到”，而非系统性强制的安全边界；**NanoClaw** 的安全加固（容器降权、包年龄检查）虽然方向一致，但尚处于 PR 阶段，未形成发布版本。OpenClaw 则通过快速且强硬的版本发布，将安全声明直接落地为用户必须面对的现实。
  - **IronClaw** 和 **Hermes Agent** 更侧重于 **“Agent 运行时的感知与交互体验”**，例如让 LLM 知道自己的运行时上下文（`IronClaw #4828`）或修复桌面端崩溃（`Hermes Agent #45226`），其技术重心在于优化人机交互的细腻度和环境适配，而非OpenClaw的全局安全架构加固。

#### 4. 共同关注的技术方向

多个项目不约而同地涌现出以下核心需求，这已构成行业共识的技术方向：

1.  **Agent 内存与上下文管理 (Memory & Context Window)**
    - **涉及项目**: **NanoBot** (Issue #4044 “短期记忆丢失”, #4307 “回合后整合抹掉回复”) , **OpenClaw** (Issue #25592 “工具调用间文本泄露”), **IronClaw** (PR #4836 “运行时上下文切片”)
    - **核心诉求**: Agent 无法有效管理和感知自身的长对话上下文，导致“失忆”、回复错乱、输出泄露等问题。用户急需更聪明的上下文窗口截断算法、外部记忆检索机制以及清晰的状态管理。

2.  **Agent 权限分级与沙箱安全**
    - **涉及项目**: **OpenClaw** (v2026.6.6 版本安全加固), **PicoClaw** (Issue #3114 “渠道权限分级”), **NanoClaw** (Issue #2711 `create_agent` MCP 工具无权限控制, PRs #2748/#2749 安全容器)
    - **核心诉求**: 用户不满足于“全有或全无”的授权模式，渴望按**对话类型**（私聊/群组）、**行为等级**（读/写/执行）进行精细化控制。同时，强烈要求通过沙箱和最小权限原则，限制 Agent 对主机环境的影响，防止恶意代码执行。

3.  **本地化与离线部署**
    - **涉及项目**: **OpenClaw** (Issue #9443 “请求提供预构建 Android APK”), **NullClaw** (Issue #952 “Ollama 本地模型回答不完整”), **Moltis** (Issue #1102 “本地语音引擎”)
    - **核心诉求**: 用户对移动端（特别是 Android）、本地模型的集成度和易用性有强烈的“开箱即用”需求。预编译版本、完善的 Ollama/llama.cpp 集成、甚至本地语音识别，都是降低使用门槛、提升隐私保护的关键。

#### 5. 差异化定位分析

| 维度 | **OpenClaw** | **NanoBot** | **Hermes Agent** | **IronClaw** | **CoPaw** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **核心定位** | 企业级安全中枢与全能型 Agent 框架 | 高度开放、面向社区贡献者的低代码 Agent 开发平台 | 极致桌面体验与多平台消息代理 | 高性能、高协同性的 Agent 推理/调度引擎 (Reborn) | 面向C端的全能AI助手，强调协作与UI表现 |
| **目标用户** | 开发者、企业、安全敏感用户 | 独立开发者、AI应用构建者、爱好者 | 日常用户、多平台社交重度用户 | 开发者、追求极致性能和复杂工作流的用户 | 普通消费者、强调生产力与创意协作的用户 |
| **技术核心** | **安全是最高优先级**。权威的沙箱、消息、代码执行控制。功能全面但谨慎。 | **社区驱动、快速迭代**。通过 `tools.audit` 引入可观测性，但更侧重于LLM调用链路的可追溯性。 | **桌面优先、多平台是资产**。注重GUI体验、桌面应用崩溃修复、平台适配器稳定性。 | **架构创新、性能为王**。统一 `agent turn engines` 减少代码冗余，通过 `DeferredBusy` 等机制优化高并发下的消息调度。 | **用户体验与模型兼容性**。桌面端打包优化、数学公式渲染、模型降级（视觉模型转文本）、BI插件等。 |
| **社区生态** | 规模最大，生态最完备（有LobsterAI等专用客户端）。 | 增长迅速，社区贡献活跃，PR和Issue讨论质量高。 | 规模中等，但在桌面端和多平台用户粘性高。 | 社区讨论深入，贡献高阶（参与架构RFC讨论）。 | 用户基础庞大，社区贡献多集中在UI/UX细节和汉化上。 |

#### 6. 社区热度与成熟度

- **快速迭代阶段 (功能与规模并重)**:
  - **OpenClaw**: 核心库成熟，但围绕安全的验证和功能拓展仍在高速进行。
  - **NanoBot**: 处于功能爆发期，社区贡献者众多，不断引入新Provider（如TTS多供应商）和新功能（如WhatsApp@提及）。
  - **PicoClaw**: 正在积极完善权限协议和WebSocket客户端对接，生态集成能力快速提升。

- **质量巩固阶段 (稳定与修复为重)**:
  - **IronClaw**: Reborn引擎大版本发布后，全团队（包括安全审计）都在进行密集的Bug修复、UI打磨和安全审计，属于典型的“大版本后固化期”。
  - **CoPaw**: `v1.1.11` 系列引入回归问题后，团队采用“版本修补-验证-再修复”的策略，修复动作密集，属于“发布后善后期”。
  - **NullClaw / ZeroClaw**: 均处于小范围的 Bug 修复和配置优化阶段，社区热度相对平稳但代码活动集中。
  - **Hermes Agent**: 桌面端问题（Windows崩溃）和多平台适配器Bug（Telegram、Slack、Matrix）是修复重心，正在解决“长尾”兼容性问题。

- **前沿探索阶段 (议题/概念验证)**:
  - **Moltis**: 虽然代码活动少，但其社区提出的“Kubernetes原生沙箱”和“本地语音识别”都是极具前瞻性的功能概念，引领了未来的可能性讨论。

#### 7. 值得关注的趋势信号

1.  **“静默失败”是用户体验的头号杀手**：无论是 OpenClaw 的文本泄露、NanoBot 的记忆丢失还是 IronClaw 的工具调用后状态错乱，这些 **“系统不报错，但行为不对”** 的静默型Bug是社区极度反感的焦点。开发者应建立更加全面的对话状态追踪和异常报告机制，宁可显示“我不知道”或“处理失败”，也不要给用户一个看似正确但逻辑错误的回复。

2.  **Agent 的“自我感知”能力成为新的技术高地**：IronClaw 的“让LLM感知运行时上下文（渠道、授权、时间）”和 NanoBot 的“上下文窗口整合”思路，都指向同一个方向：**Agent 需要更好的“心智模型”来理解“我是谁”、“我所处的环境是什么”以及“刚才发生了什么”**。这是解决长对话连贯性和环境适应的关键所在。

3.  **“安全性”从开发者责任变为内置特性**：OpenClaw 的强硬安全版本、PicoClaw 和 NanoClaw 的权限分级讨论，预示着**安全性不再是可选的配置项，而是 Agent 框架的核心承诺**。未来的优秀 AI 智能体项目，必然是默认安全的。这标志着整个行业从“功能优先”迈向了“安全与发展并重”的新阶段。

4.  **“审计与可观测性”从运维工具演进为 AI 纠错与调试的基石**：NanoBot 的 `tools.audit` 模块和 IronClaw 的记录 MCP 拒绝/授权失败的 PR，是这一趋势的体现。因为 AI 系统的非确定性，传统的日志已不足以诊断问题。**对 Agent 每一步“思考”和“行动”的精确记录与回放，正成为开发和调试不可或缺的一部分**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 NanoBot (github.com/HKUDS/nanobot) 项目数据，于 2026-06-13 生成的项目动态日报。

---

# NanoBot 项目动态日报 | 2026-06-13

## 1. 今日速览

NanoBot 项目在过去24小时内呈现出**高度活跃**的状态。核心开发团队、社区贡献者与用户之间的互动频繁：共有 30 条 Pull Request 被创建或更新，其中 9 条已被合并/关闭，表明项目迭代速度极快。同时，Issue 列表中涌现出 6 条新动态，其中包含 3 个新报告的 Bug，反映出项目在快速发展的同时，也面临着稳定性与用户体验方面的新挑战。值得注意的是，多位用户报告了与“记忆”和“上下文管理”相关的关键性问题，这表明该项目在长对话和Agent持久化能力上遇到了瓶颈。

## 2. 版本发布

无。项目在过去24小时内未发布新的正式版本。当前代码库正在通过大量 PR 进行快速迭代，距上次发布可能暂时没有形成稳定的里程碑。

## 3. 项目进展 (今日合并/关闭的 9 个 PR)

今日合并/关闭的 PR 主要集中在**可观测性**、**稳定性修复**和**核心功能优化**三大块，标志着项目正在向更成熟的方向迈进。

-   **可观测性 (Observability) 的初步建立**：
    -   [PR #4319](https://github.com/HKUDS/nanobot/pull/4319) 和 [PR #4318](https://github.com/HKUDS/nanobot/pull/4318) 被合并。这两个 PR 引入了 `tools.audit` 审计模块，为Agent的工具调用行为提供了可观测性。这意味着开发者未来能够更好地调试、监控和记录Agent的行动，是项目向生产环境部署迈出的重要一步。

-   **核心调度与资源管理修复**：
    -   [PR #4304](https://github.com/HKUDS/nanobot/pull/4304) (fix(cron)) 被合并。该修复确保由Cron任务派生的子Agent任务执行完毕后，主Cron任务才会标记为完成。这修复了在自动化任务流程中可能出现的任务状态不准确问题，提升了任务调度的可靠性。
    -   [PR #4321](https://github.com/HKUDS/nanobot/pull/4321) (fix: advance dream cursor) 被合并。该修复解决了当“Dream”功能被禁用时，`dream_cursor` 无法推进，导致提示词（prompt）日渐臃肿的问题。这个修复对于长期运行的服务非常关键，能有效控制上下文窗口的增长，避免不必要的Token消耗。
    -   [PR #4303](https://github.com/HKUDS/nanobot/pull/4303) (fix(mcp)) 被合并。该修复解决了当 `streamableHttp` MCP (Model Context Protocol) 服务器会话断开重连时，因异步任务冲突导致的程序崩溃问题。

-   **配置架构优化**：
    -   [PR #4314](https://github.com/HKUDS/nanobot/pull/4314) (Break config schema dependency) 被合并。这是一项架构级别的重构，打破了配置模式对工具运行时模块的强依赖。这提升了项目的代码组织性和可维护性，为后续更复杂的工具扩展打下了基础。

**总结**：项目通过合并这些 PR，系统性解决了多个 “内存泄漏” 和 “任务可靠性” 问题，并引入了关键的自动化工具审计能力。整体健壮性和可调试性有显著提升。

## 4. 社区热点

今日最受关注的 Issue 和 PR 反映了社区对**上下文窗口管理**和**记忆能力**的强烈关切。

-   **#4044 `short term memory loss`**：[Issue #4044](https://github.com/HKUDS/nanobot/issues/4044) 是今日最热的讨论点之一（5条评论）。用户 `bjoshuanoah` 详细描述了NanoBot最基本的“短期记忆丢失”问题：Agent问了你一个问题，你回答了，它却像没问过一样。该 Issue 深入分析了根因，认为是系统提示词（如 SOUL.md, USER.md, MEMORY.md）以及上下文窗口压力共同作用的结果。这直指AI Agent项目的核心痛点——长对话连贯性。社区对此高度关注，因为它直接影响到用户体验的根本。

-   **#4307 `Post-turn consolidation wipes the agent‘s own delivery message`**：[Issue #4307](https://github.com/HKUDS/nanobot/issues/4307) 是另一个关于上下文管理的严重问题。用户 `MARJORIESHA-pBAD` 报告，当 `context_window_tokens` 设置得比较保守时（如40k），Agent在长时间思考/多轮工具调用生成的超大上下文（100k+ tokens）在“回合后整合（consolidation）”时，会错误地抹掉Agent自己最终发送的信息。这导致用户后续的提问失去了上下文，对话体验断裂。

**分析**：社区讨论的焦点已从“能否完成任务”转向了“如何更好地完成复杂、长对话任务”。**记忆管理和上下文窗口的智能处理**被视为当前最重要的功能缺口和性能瓶颈。这不仅仅是Bug报告，更是对未来产品路线的强烈呼声。

## 5. Bug 与稳定性

今日报告的Bug全部与**对话管理和API兼容性**相关，按严重程度排列如下：

1.  **严重性：高**
    -   **#4307** `Post-turn consolidation wipes the agent’s own delivery message` (严重性: 高，已确认无fix PR)。该Bug会直接导致用户在长对话中丢失关键上下文，严重破坏用户体验。目前暂无对应的修复PR。
    -   **#4044** `short term memory loss` (严重性: 高，已确认无fix PR)。这是Agent的“失忆”问题，属于系统性的架构难题，影响用户体验的根基。该问题自5月28日提出，长期未关闭，说明修复难度较大。

2.  **严重性：中**
    -   **#4203** `Bug: find_legal_message_start 在用户消息后跟着孤立工具结果时会丢弃所有消息` (状态：已关闭)。该Bug是一个具体的代码逻辑缺陷，会导致在特定消息序列下所有消息被丢弃。已经被修复（通过检索关联的PR #3984修复）。
    -   **#4309** `nanobot serve: /v1/chat/completions always returns zero usage tokens` (状态：开放，新报告)。该Bug是一个API实现缺陷。虽然不影响对话功能，但对于需要Token计费的部署场景是致命缺陷。目前该Issue无评论，也无修复PR，需关注。

3.  **严重性：低**
    -   **#4305** `Multiple custom providers` (状态：已关闭，是一个功能请求)。用户提出支持多个自定义Provider。该问题在提出后很快被关闭，可能是由于其讨论价值大于Bug严重性。

**总结**：最令人担忧的是 **#4044** 和 **#4307** 这两个核心记忆/上下文问题，它们影响着Agent智能的“连续性”，是决定NanoBot能否从“玩具”进化为“工具”的关键瓶颈。

## 6. 功能请求与路线图信号

-   **多Provider支持**：用户 `smurfix` 在 [#4305](https://github.com/HKUDS/nanobot/issues/4305) 中提出需要多于一个的自定义和OpenAI Provider。虽然该 Issue 已被关闭，但社区贡献者 `La-Volpe` 的 [PR #4313](https://github.com/HKUDS/nanobot/pull/4313) 正试图通过 WebUI 实现 Provider 配置，这很可能被纳入后续版本。这表明“灵活性和鲁棒性”的用户需求正在增长。
-   **SDK 能力增强**：社区贡献者 `Re-bin` 的 [PR #4296](https://github.com/HKUDS/nanobot/pull/4296) 正在扩展 Python SDK，增加更丰富的运行时控制。这表明项目正从单一聊天界面，转向支持开发者二次集成和构建复杂应用的平台化方向。
-   **TTS 多提供商支持**：`tobrien` 的 [PR #4316](https://github.com/HKUDS/nanobot/pull/4316) 正在为TTS功能增加多提供商支持（OpenAI, Groq, ElevenLabs）。这是增强产品体验的重要一步，可能成为下一个版本中的亮眼功能。
-   **WhatsApp 提及功能**：社区用户 `tiagosantosvdl` 提交的 [PR #4317](https://github.com/HKUDS/nanobot/pull/4317) 为WhatsApp频道增加了@提及功能。这是针对具体聊天场景的实用功能，方向很好。

## 7. 用户反馈摘要

-   **核心痛点**：用户在 [#4044](https://github.com/HKUDS/nanobot/issues/4044) 中描述了最令人沮丧的体验：“Nanobot 总是像第一次见到你一样”。一位用户评论道，“这让我感觉不是在和AI对话，而是在不断重复回答一个健忘的机器人”。这揭示了当前系统在处理长期关系记忆上的短板。
-   **性能担忧**：在 [#4307](https://github.com/HKUDS/nanobot/issues/4307) 中，用户发现在长工具调用后（100k tokens），上下文窗口的整合机制会“吃掉”Agent的输出，导致用户后续无法接话。这表明模型在处理超长思维链和复杂工作流后，面临着严重的资源管理难题。
-   **功能性不满**：用户 `alx1379` 在 [#4309](https://github.com/HKUDS/nanobot/issues/4309) 中指出，API 返回的 token 用量始终为零。虽然不致命，但暴露出API实现不完善的问题，对于注重成本监控的用户来说是重要的功能缺失。

## 8. 待处理积压

主要积压在核心系统的稳定性与健壮性上。

-   **待回应的核心 Bug**：
    -   **#4044 `short term memory loss`** (自5月28日提出，23天未关闭)：这是最严重，也是最难解决的架构性问题。需要核心开发者评估并制定长期的解决方案路线图，如引入摘要记忆、向量检索等外部记忆系统。
    -   **#4307 `Post-turn consolidation wipes agent’s own delivery message`** (新报告但已获关注)：紧随 #4044 之后的第二大上下文管理问题，其根因和修复方案可能与 #4044 相关联。

-   **等待合并的 Bug 修复**：
    -   有多个由 `yu-xin-c` 提交的针对**内存管理**、**输入校验**的安全性和稳定性修复PR（如 #4256, #4119, #4053 等）已经开放了数天至数周。这些是解决**数据根因**的关键修复，项目维护者应优先考虑合并或给予反馈。
        -   [PR #4256](https://github.com/HKUDS/nanobot/pull/4256): fix(memory): keep history cursor monotonic
        -   [PR #4119](https://github.com/HKUDS/nanobot/pull/4119): fix(exec): block relative symlink workspace escapes (安全相关)
        -   [PR #4053](https://github.com/HKUDS/nanobot/pull/4053): fix(tools): keep read-only roots out of write paths (安全相关)

**分析师建议**：项目维护者应**立即组织评审** #4044 和 #4307，并公开一个解决记忆和上下文问题的**长期路线图**。同时，应优先合并 `yu-xin-c` 提交的一系列修复PR，它们是解决当前诸多 Bug 和数据不一致性的基石。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 Hermes Agent 项目数据，我为您生成了 2026年6月13日的项目动态日报。

---

# Hermes Agent 项目动态日报 - 2026-06-13

## 1. 今日速览

今日 Hermes Agent 项目社区活跃度极高，24小时内产生了50条 Issue 和50个 PR，表明社区参与度和问题反馈非常积极。项目修复集中在**桌面客户端崩溃、多平台网关适配器Bug**以及**核心Agent与工具的稳定性问题**上。其中，一个长期存在的 **“输出截断”Bug** 引发了广泛讨论，成为社区焦点。尽管没有新版本发布，但维护者已针对多个高优先级问题（如 Windows 桌面端 GPU 崩溃）提交了修复 PR，项目修复工作进展迅速。

## 2. 版本发布

**无**

## 3. 项目进展

今日有5个 PR 被合并或关闭，虽然数量不多，但部分解决了关键性问题，并推进了新功能。
- **[PR #44890] [已关闭]** 修复了桌面端会话恢复时，因未处理压缩链而创建新会话，导致无法加载原有会话的 Bug。提升了会话持久性的可靠性。
- **[PR #44893, #44895, #44899] [待合并]** 这三个由 `Zazzles2908` 贡献的 PR 针对**看板（Kanban）**功能进行了重要修复，包括：父任务取消后子任务不再被阻塞、已完成任务不会重发、以及调度器不再因“假性阻塞”而误判。这些修复对于看板驱动的多智能体工作流至关重要。
- **[PR #44896] [待合并]** 降低了 WhatsApp 适配器的默认去抖延迟，将其与 Telegram 适配器的响应速度对齐，这将显著改善 WhatsApp 用户的交互体验。
- **[PR #44898] [待合并]** 修复了网关（Gateway）在 systemd 重启策略下，因僵尸进程导致确定性崩溃循环的问题，增强了服务的稳定性。

项目整体在**修复桌面端、网关和看板模块的核心稳定性问题**上取得了明确进展。

## 4. 社区热点

今日最受关注的 Issue 是 [#7237](NousResearch/hermes-agent Issue #7237) **“[Bug]: Error: Response truncated due to output length limit”**，该问题获得了 **41条评论和5个👍**。

- **诉求分析**：该 Bug 指出，当 Agent 生成较长回复时，会被“输出长度限制”截断。这个问题在 CLI、Telegram、Discord 等多种交互终端上均有出现，因此吸引了大量用户的讨论。
- **社区影响**：这是一个**直接影响用户实际使用体验**的严重问题。用户无法获得完整的AI回复，尤其是在处理复杂任务或生成长篇文档时。这反映出社区对**长文本生成稳定性和可靠性**有非常高的期望，并且当前默认配置下的限制可能过于保守。此问题已成为社区核心痛点，需要维护者优先关注和解决。

## 5. Bug 与稳定性

今日报告的Bug涵盖范围广泛，按严重程度排列如下：

- **严重 (P1)**:
    - **[[Bug] 桌面端 Windows 平台频繁崩溃](NousResearch/hermes-agent Issue #45226)**: 在 Windows 上，Hermes Desktop 因 GPU 进程崩溃而不断闪退。**已有修复 PR [#45341](NousResearch/hermes-agent PR #45341)** 提交，通过添加 `--no-angle` 标志和 `HERMES_DESKTOP_DISABLE_GPU` 环境变量来解决。
    - **[[Bug] Gateway 泄漏 VIRTUAL_ENV 导致子进程环境污染](NousResearch/hermes-agent Issue #23473)**: 这是一个长期存在的严重问题，Gateway 将自身的 venv 泄露到所有子进程中，导致在项目中运行 `uv sync` 等命令时会破坏 Hermes 自身的环境。

- **中等 (P2)**:
    - **[[Bug] Telegram 富文本表格被错误渲染](NousResearch/hermes-agent Issue #45323)**: Telegram 消息中的 Markdown 表格会被格式化器重写为无序列表。
    - **[[Bug] Matrix 网关因日志移除，中断后丢失助理消息](NousResearch/hermes-agent Issue #43936)**: 由于 `.jsonl` 日志被移除，SQLite 状态数据库成为唯一持久层，但在特定中断场景下会丢失消息。
    - **[[Bug] 原生 MiniMax 提供商 MCP 工具参数嵌套数组处理错误](NousResearch/hermes-agent Issue #44976)**: 在使用 MiniMax-M3 模型时，MCP 工具参数中的嵌套单元素数组会被错误折叠，导致调用失败。
    - **[[Bug] Windows 本地文件读取失败](NousResearch/hermes-agent Issue #17999)**: `read_file` 工具在 Windows 下无法访问非 C 盘的文件。
    - **[[Bug] 评估/学习曲线工具 (AX/SOM) 元素边界始终为零](NousResearch/hermes-agent Issue #44763)**: 在 macOS 上，`computer_use` 功能因元素坐标为零而无法正常工作。
    - **[[Bug] Slack 机器人之间消息被静默丢弃](NousResearch/hermes-agent Issue #30091)**: 即使配置了 `allow_bots=all`，Hermes 也无法看到来自其他 Slack 应用的消息。

- **较低优先级 (P3)**:
    - **[[Bug] Skills 工具路径解析失败](NousResearch/hermes-agent Issue #45307)**: `_find_skill()` 无法正确解析 `category/skill` 这种格式的路径。
    - **[[Bug] MCP OAuth 流程在探测失败后仍会轮询30秒](NousResearch/hermes-agent Issue #44866)**: 导致 OAuth 流程失败时的响应体验极差。
    - **[[Bug] 终端软换行导致字符显示错误](NousResearch/hermes-agent Issue #45272)**: 流式输出时，终端软换行会打断单词。

## 6. 功能请求与路线图信号

用户提出了多个期望的新功能：

- **核心需求**：
    - **[接入看板到桌面应用](NousResearch/hermes-agent Issue #41222)**: 用户希望将看板功能集成到桌面 GUI 中，以减少从 CLI 切换的不便。
    - **[桌面 GUI 界面优化](NousResearch/hermes-agent Issue #44140)**: 功能包括自动滚动、修复侧边栏遮挡滚动条问题、自定义会话分组。这反映了用户对桌面端体验完善度的较高要求。
    - **[跨平台统一会话历史](NousResearch/hermes-agent Issue #45275 & #44140)**: 用户希望在桌面应用上能看到来自 Telegram 等其它平台的会话记录。

- **新功能与扩展**：
    - **[Signal 适配器增强](NousResearch/hermes-agent Issue #39043)**: 希望 Signal 网关支持原生回复、编辑和远程删除消息。
    - **[类人记忆架构](NousResearch/hermes-agent PR #44897)**: 有开发者提交了 PR，提议增加类似人类的记忆层级，如工作记忆和语义记录。

- **路线图信号**：从这些请求和已在进行的 PR（如 #44891 看板键命名辅助、#16769 Nostr 适配器、#44897 记忆架构）来看，项目未来的发展方向可能更侧重于：
    1.  **桌面客户端的完善与整合**：提升 GUI 体验并整合核心功能。
    2.  **多平台覆盖**：持续增加新的通信平台（如 Nostr）支持。
    3.  **智能体能力进化**：探索更复杂的记忆架构和多智能体协作机制（如看板）。

## 7. 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出以下用户反馈：

- **核心痛点**：
    - **长回复被截断**：这是目前最强烈的负面反馈，直接影响核心体验。用户需要能流畅处理长任务的 Agent。
    - **桌面端体验不佳**：从 Windows 崩溃到界面交互（如无自动滚动）的问题，说明桌面端的稳定性与用户体验是亟待提升的重要环节。
    - **平台适配有短板**：Windows 文件路径问题、Slack 机器人互通信问题以及 Telegram/MiniMax 等提供商的特定 Bug，表明各平台的适配深度和测试覆盖度仍有待加强。

- **满意与期望**：
    - **对“看板”功能期望高**：用户对看板功能寄予厚望，认为它是多智能体工作流的强大工具，并期望将其无缝集成到日常使用的桌面应用中。
    - **跨平台协同是刚需**：用户希望能够在一个地方管理所有会话，这表明“统一入口”是个人AI助手产品走向成熟的关键。

## 8. 待处理积压

以下为高优先级或长期未解决的 Issue，可能阻碍用户或开发者正常使用，值得维护者优先关注：

- **[Issue #23473] Gateway 泄露 VIRTUAL_ENV 环境变量 (P1)**: **严重**。该问题从5月11日就存在，至今已超过一个月，对在 IDE 或复杂开发环境中使用 Hermes 的开发者影响巨大。虽然维护复杂，但一旦修复将极大改善开发者的使用体验。
- **[Issue #17999] Windows 本地 File & Terminal 工具不可用 (P2)**: **范围广**。影响所有 Windows 原生用户，严重限制了他们在日常任务中使用 Hermes 的能力。此问题已存在超过一个半月，急需解决。
- **[Issue #7237] 长回复输出截断 (P2/热度极高)**: **社区呼声强烈**。虽然严重程度定级不高，但当前是社区最关注的 Issue。需要评估是否是配置问题，或存在更底层的输出缓冲区限制，并给出明确的解决方案或临时对策。

---

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，以下是基于您提供的GitHub数据生成的PicoClaw项目日报。

---

# PicoClaw 项目动态日报 | 2026-06-13

**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师
**数据来源:** GitHub (github.com/sipeed/picoclaw)

---

## 1. 今日速览

项目今日活跃度**极高**，尤其在社区讨论和代码提交方面。过去24小时内，共有5个新Issue和14个PR被创建，显示出强劲的开发动力。社区围绕**权限控制**、**协议完善**和**新模型适配**展开了热烈讨论，同时维护者也积极修复了多个关键Bug。项目整体健康度良好，正朝着更健壮、更易扩展的方向迈进。

## 2. 版本发布

- **nightly 自动构建 (v0.2.9-nightly.20260613.c362114c)**
  - **内容**: 这是一个基于`main`分支的自动化每日构建版本。
  - **状态**: **不稳定**，仅供测试使用。
  - **变更日志**: [完整变更记录](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
  - **分析师点评**: 此次发布无特定破坏性变更或迁移指南，但用户应谨慎在生产环境部署nightly版本。

## 3. 项目进展 (已合并/关闭的PR)

今日共有3个PR被合并或关闭，主要集中在代码健壮性和问题修复：

- **[PR #2551] (已关闭) refactor: 标准化渠道标识并解耦名称与提供商类型**
    - **作者**: cytown
    - **摘要**: 这是一个重要的架构重构。它将渠道名称(配置文件中的键)与渠道类型(如Telegram, Discord)解耦，允许同一种提供商运行多个实例。这解决了消息总线与代理分发逻辑中的识别问题。
    - **意义**: 显著提升了项目的**可扩展性**，为未来支持更复杂的渠道配置和路由打下了基础。
    - **链接**: [PR #2551](https://github.com/sipeed/picoclaw/pull/2551)

- **[PR #3113] (已合并) fix(channels): 检查 toChannelHashes 中的 JSON 序列化错误**
    - **作者**: chengzhichao-xydt
    - **摘要**: 修复了`pkg/channels/manager_channel.go`中三个被静默忽略的JSON序列化/反序列化错误。
    - **意义**: **提升了稳定性**，避免了因配置序列化失败而导致数据丢失或哈希计算错误的潜在风险。
    - **链接**: [PR #3113](https://github.com/sipeed/picoclaw/pull/3113)

- **[PR #3112] (已合并) fix(tools): 处理 toolloop 工具调用参数中的 JSON 序列化错误**
    - **作者**: chengzhichao-xydt
    - **摘要**: 修复了`pkg/tools/toolloop.go`中`json.Marshal`错误被静默忽视的问题，该问题可能导致工具调用参数在对话历史中丢失。
    - **意义**: **保障了数据完整性**，确保工具调用数据在复杂交互中能够被正确记录和传递。
    - **链接**: [PR #3112](https://github.com/sipeed/picoclaw/pull/3112)

## 4. 社区热点

- **[Issue #2984] 为Pico WebSocket客户端添加明确的“回合完成”信号**
    - **作者**: Brook-sys
    - **热度**: 评论2条，👍 2个
    - **分析**: 这是社区对外部客户端集成的核心诉求。开发者希望有一个确定性的事件来标记AI代理对用户消息的完整响应结束，而不是依靠组合`typing.stop`等事件来推断。这反映了项目生态向**平台化**发展的趋势。
    - **链接**: [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)

- **[Issue #3114] & [Issue #3109] 渠道权限分级控制**
    - **作者**: v2up-32mb
    - **热度**: 两个Issue均为今日新开，代表了强相关的社区声音。
    - **分析**: 用户非常清晰地提出了在Telegram渠道中，按**对话类型(私聊/群组/频道)** 进行**权限分级**的需求。这是对现有`allow_from`白名单机制的重要补充，旨在解决“不同场景下需要不同危险操作权限”的安全边界问题。这是一个高价值、高优先级的功能请求。
    - **链接**: [Issue #3114](https://github.com/sipeed/picoclaw/issues/3114), [Issue #3109](https://github.com/sipeed/picoclaw/issues/3109)

## 5. Bug 与稳定性 (按严重程度排列)

- **[高] [Issue #3111] Gemini 3.5 Flash 工具执行失败**
    - **作者**: Giordano10
    - **描述**: 使用`gemini-3.5-flash`模型时，工具/技能执行会返回400错误。原因是后端的响应模式与Google API新的Agentic推理要求不兼容。
    - **状态**: 已报告，**尚无修复PR**。
    - **链接**: [Issue #3111](https://github.com/sipeed/picoclaw/issues/3111)

- **[中] [Issue #3110] Telegram Forum话题回复默认到#General**
    - **作者**: Giordano10
    - **描述**: 在Telegram Forum模式下，机器人虽然能在正确的话题内显示“正在输入...”，但最终消息却错误地发送到默认的话题`#General`。
    - **状态**: 已报告，**尚无修复PR**。
    - **链接**: [Issue #3110](https://github.com/sipeed/picoclaw/issues/3110)

- **[中] [Issue #3012] Evolution功能持续消耗Token**
    - **作者**: xpader
    - **描述**: 当启用Evolution功能时，即使没有新交互，系统每分钟也会持续消耗Token，可能造成不必要的开销。
    - **状态**: 这是一个积压的Bug，**尚无修复PR**。
    - **链接**: [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

## 6. 功能请求与路线图信号

- **权限分级控制** (Issue #3114 & #3109) 是今日最强烈的路线图信号。该需求已有详细的场景分析和对比，易于实现。考虑到已有PR #2917(新渠道)在讨论，此功能很可能成为下一个小版本的重点。
- **完善Pico WebSocket协议** (Issue #2984) 与 **PR #3116** (修复turn.done生命周期) 相关联，后者已经提交。这表明项目团队采纳了社区建议，正在积极完善外部集成接口，这是项目向**开发平台**演进的关键一步。
- **远程Pico WebSocket模式** (PR #3118) 是一个新的功能演进，允许`picoclaw agent`命令通过WebSocket连接到远端实例。这暗示了项目在**分布式部署和远程管理**方面的探索。

## 7. 用户反馈摘要

- **正面反馈**: 用户对项目的迭代速度和社区粘性表示认可。例如，Issue #2984 的提出者Brook-sys提出的协议完善建议，很快就被PR #3116跟进，体现了项目对社区贡献的重视。
- **痛点与需求**:
    - **安全性**: 多位用户(如v2up-32mb, Giordano10)持续表达对**精细权限控制**的强烈需求，特别是在多租户或群组场景下。
    - **兼容性**: 用户Giordano10报告了与最新模型Gemini 3.5 Flash及Telegram Forum功能的兼容性问题，表明项目需要持续投入精力适配最新的平台API。
    - **稳定性**: 用户xpader上报的“Evolution持续消耗Token”问题已存在一周，可能影响部分用户的资源开销，建议优先排查。

## 8. 待处理积压

- **功能/稳定性相关:**
    - **PR #2964 (Feat/image input compression)**: 开放超过两周的待合并PR，增加图像压缩功能，可能解决了Vision流水线中的资源消耗问题。应尽快审核。
        - **链接**: [PR #2964](https://github.com/sipeed/picoclaw/pull/2964)
    - **PR #2917 (feat: add NEAR AI Cloud provider)**: 开放超过三周的新模型提供商支持PR，长时间未合并可能阻碍希望使用该平台的用户。
        - **链接**: [PR #2917](https://github.com/sipeed/picoclaw/pull/2917)

- **Bug修复相关:**
    - **Issue #3012 (Continuous consumption of tokens every minutes when evolution is enabled)**: 已存在一周以上，影响用户实际体验和成本，建议优先处理。
        - **链接**: [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NanoClaw 项目 2026-06-12 至 2026-06-13 数据生成的动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-13

**项目名称:** NanoClaw (nanocoai/nanoclaw)
**核心领域:** AI 智能体框架 / 个人 AI 助手
**数据报告周期:** 2026-06-12 00:00 - 2026-06-13 00:00 (UTC)

---

### 1. 今日速览

项目在本报告期内活动**高度活跃**，尤其集中在 PR 的密集提交与问题的深度讨论上。过去24小时内产生了 **9 个新的 Pull Request** 和 **5 个 Issue 更新**，其中安全加固和功能扩展是两大核心主线。社区反馈聚焦于系统稳定性（如消息丢失、会话阻塞）和权限安全控制（如 MCP 工具滥用）。总体来看，项目正处在 **功能快速迭代与安全稳定性深度优化并行** 的关键阶段。

---

### 3. 项目进展

本报告期内，项目**无** PR 被合并或关闭，但提交了 9 个新的 PR，指向了数个关键改进方向：

- **安全性与权限加固 (关键进展):**
    - **[#2748]** 提出了默认对 Agent 容器进行强化：`--cap-drop=ALL`、`--no-new-privileges` 和 `--pids-limit 2048`。这是一项根本性的安全改进，能显著降低容器逃逸或资源耗尽攻击的风险。
    - **[#2749]** 增加了 npm 包安装的安全门槛：由 Agent 发起的 `install_packages` 请求，在管理员批准后，会检查包是否发布超过 3 天，阻止安装过新的、可能存在风险的包。这直接响应当前软件供应链安全问题。

- **核心功能与架构优化:**
    - **[#2745]** 和 **[#2746]** 引入了可选的“持久化内存框架”和“Agent 能力接口”的概念。这表明项目正在为 Provider 层构建更标准化的能力模型，为未来实现 Agent 记忆、跨平台能力复用等高级特性奠定基础。
    - **[#2747]** 推进了与 OneCLI 服务的集成，涉及 SDK 升级和凭证挂载，表明项目在 B 端/企业级集成能力上持续投入。

- **稳定性修复 (积极跟进):**
    - **[#2670]** 针对 `poisoned-resume crash loop`（会话因损坏的恢复数据而持续崩溃）提出了修复方案，解决了此类致命循环的核心 bug。
    - **[#2750]** 试图根治 `outbound.db` 在容器被杀死后出现损坏的长期问题，解决了消息发送的持久化稳定性。

**项目整体向前迈出了一大步，尤其是安全架构的强化和核心框架的扩展性方面，显示出项目正在向更成熟、更安全的企业级应用演进。**

---

### 4. 社区热点

本周期内社区互动虽总量不大，但讨论质量较高，集中在三个核心议题上：

- **Issue #2506: `send_message dedup silently drops responses` (评论最多, 需求明确)**
    - **链接:** [Issue #2506](https://github.com/nanocoai/nanoclaw/issues/2506)
    - **诉求分析:** 用户 `mshirel` 精确指出了在并发/高频场景下，Agent 回复被静默丢弃的严重 Bug。这并非简单网络波动，而是去重逻辑 (`send_message dedup`) 和轮询环 (`poll-loop`) 设计上的缺陷。背后的诉求是**对 Agent 交互可靠性和时序一致性的高要求**，这是任何生产级 AI 助手的基础。社区对此问题关注度很高，期待有明确的修复指向。

- **PR #2748 / #2749 (安全性, 反响积极)**
    - **链接:** [PR #2748](https://github.com/nanocoai/nanoclaw/pull/2748), [PR #2749](https://github.com/nanocoai/nanoclaw/pull/2749)
    - **诉求分析:** 这两条 PR 直接响应了社区对安全性的普遍焦虑。`boazdori` 提交的这两项变更属于“防御纵深”（defense-in-depth）策略，是提升用户对项目信任度的关键举措。它们表明项目维护者**对 Agent 权限、供应链安全等问题有清醒认知**，并能迅速转化为具体的防御代码。

- **Issue #2711: `create_agent MCP tool is ungated` (权限风险, 强烈关注)**
    - **链接:** [Issue #2711](https://github.com/nanocoai/nanoclaw/issues/2711)
    - **诉求分析:** 用户 `jonazri` 发现了一个严重的安全风险：`create_agent` 这个本应“仅管理员可用的”MCP 工具，实则是无权限控制的。这是安全基线问题，背后反映的是社区对 **MCP 工具生命周期和权限模型**的审视。该 Issue 的创建，实际上为项目重构权限体系提供了强有力的需求支撑。

---

### 5. Bug 与稳定性

以下按严重程度排列本报告期内的活跃 Bug：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| **严重 (Critical)** | [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) | `send_message` 去重逻辑在并发场景下**静默丢弃 Agent 回复**，导致客户端超时。直接影响核心交互可用性。 | 无 |
| **严重 (Critical)** | [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) | Agent 会话**缺乏单次工具调用超时机制**，一个挂起的 MCP 工具会阻塞整个会话长达 30 分钟。 | 无 |
| **高 (High)** | [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) | `create_agent` MCP 工具**未进行任何权限校验**，任何容器均可调用。属于严重的安全缺口。 | 无 |
| **中 (Medium)** | [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) | 当 LLM 预算耗尽时，Gateway 返回模拟的 200 成功响应，导致 Agent SDK 误认为是正常回复并**静默丢弃**，用户无感知。 (`_已于今日关闭_`) | 无 |

**关键洞察:** 今日报告的 Bug 多与**可靠性、安全性的系统性设计缺陷**有关，而非简单的代码逻辑错误。其中 `#2506` 和 `#2668` 代表了核心功能稳定性上的两个最大威胁。

---

### 6. 功能请求与路线图信号

- **新功能请求:**
    - **([#2632](https://github.com/nanocoai/nanoclaw/issues/2632))** `Clarify status of Telegram agent-swarm` : 用户请求明确 v2 版本对于“Telegram Agent 群组/多 Bot”特性的支持状态。这表明**多 Agent 协同**和**复杂渠道集成**是社区迫切需要的功能。
    - **([#2745](https://github.com/nanocoai/nanoclaw/pull/2745)) & ([#2746](https://github.com/nanocoai/nanoclaw/pull/2746))** `opt-in persistent memory` & `agent-surfaces capability seam` : 这两条 PR 本身正是功能请求的落地实现。它们预示着下一版本的核心方向将是**Agent 持久化记忆**和**统一的能力接口**。

- **路线图信号:**
    - 结合最新 PR，可以判断项目接下来的重点可能包含：
        1.  **安全加固 (安全基线)** ：容器运行时权限最小化、软件包供应链校验。
        2.  **框架扩展 (能力底座)** ：`Agent Capability Seam` 将为插件化、跨 Provider 能力共享奠定基础。
        3.  **用户体验提升 (记忆)** ：`Persistent Memory` 将显著提升 Agent 的上下文理解能力和个性化程度。

---

### 7. 用户反馈摘要

从 Issue 评论和描述中可以提炼出以下用户痛点与诉求：

- **对可靠性的极度渴望:**
    > Issue #2506 的用户写道：“...when two turns complete less than 60 seconds apart...responses are silently dropped.” 这种“静默失败”是最让用户困扰的行为，用户强烈需要一个健壮的、可预期的消息传递机制。

- **对安全性的焦虑:**
    > Issue #2711 的用户报告：“...documented/described as admin-only, but it is exposed to **every** container...” 安全缺口不再是理论问题，而是社区用户在实际测试中发现的实际问题，这凸显了现有权限模型的脆弱。

- **对复杂特性的迁移困惑:**
    > Issue #2632 的用户表示：“...trying to plan a v1 to v2 migration for a fork that uses the old `/add-telegram-swarm` feature, and the current state is a little ambiguous.” 这表明用户对 v2 版本的功能兼容性和演进路线感到困惑，文档和沟通需要加强。

---

### 8. 待处理积压

本报告期内未发现长期未回应的“僵尸”Issue 或 PR。所有活跃的 Issue 和 PR 均得到及时响应。但以下两个 PR 虽新，但因涉及核心架构变更，值得特别关注其合并进度：

- **[#2670](https://github.com/nanocoai/nanoclaw/pull/2670) `fix(agent-runner): self-heal poisoned-resume crash loop`** : 已于6月1日提交，至今仍未合并。由于该 PR 解决了导致会话永久死循环的致命问题，其长时间未合并可能对部分用户造成持续困扰。建议项目维护者重点评估并推进。
- **[#2745](https://github.com/nanocoai/nanoclaw/pull/2745) & [#2746](https://github.com/nanocoai/nanoclaw/pull/2746)**: 这两个 PR 作为新的功能骨架，与 `#2747`、`#2748`、`#2749` 等多个 PR 在同一日密集提交，可能存在一定依赖关系。维护者需要协调好它们的合并顺序，避免代码冲突或功能不完整。

---
**分析师结论:** NanoClaw 项目处于健康的快速发展期，社区活跃度源于用户对生产级 AI 助手框架的严苛需求。当前最优先的路线应是 **解决 `#2506` 和 `#2668` 两个核心稳定性问题，同时合并 `#2670` 修复，并稳步推进由 `#2748` 和 `#2749` 引领的安全加固工作**。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 NullClaw 项目数据，生成以下 2026-06-13 的项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-13

## 1. 今日速览

今日 NullClaw 项目活跃度中等偏上。社区主要聚焦于 **bug 修复与稳定性增强**，共有 3 个待合并的 Pull Request (PR) 正在处理，重点关注了配置灵活性、错误处理以及 Discord 集成稳定性。同时，一个关于本地模型（Ollama）输出不完整的 **新 Bug** 被报告，引发了社区对模型集成质量的关注。今日无新版本发布，项目维护者正在密集处理现有 PR，代码库处于快速迭代的“修复阶段”。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无已合并或关闭的 PR，所有 3 个 PR 均处于 **待合并** 状态。但这些 PR 代表了项目向前迈进的关键步骤：

- **配置系统增强 (#949)**：PR `fix: make queue_mode configurable from config.json` 旨在提升项目的可配置性。它允许用户通过 `config.json` 文件设置新会话的默认队列模式（`queue_mode`），并将 `QueueMode` 枚举重构为单一数据源，减少了代码冗余和维护成本。这是对 Agent 核心行为进行精细控制的重要改进。
- **错误处理优化 (#951)**：PR `fix(agent_runner): suppress stderr initialization logs on agent failure` 针对 Agent 进程失败时的错误输出进行了优化。之前的实现会将 Agent 的初始化日志（如内存规划、MCP 服务器注册等）错误地发布到频道中，造成用户困惑。此修复明确限制了当 Agent 异常退出时，不会输出这些与正常响应无关的日志，显著提升了 Agent 的鲁棒性和用户体验。
- **Discord 集成稳定性 (953)**：PR `fix(discord): recover closed gateway sockets` 专门针对 Discord 平台的连接稳定性。它修复了在重连清理过程中关掉网关套接字时的竞争条件，并增加了对卡在 `HELLO` 事件之前的重连过程进行健康检查的机制，防止无限期挂起。这表明项目正在积极解决生产环境中不同平台的连接问题。

**总结**：项目正在系统性地解决 3 个关键领域的问题：**核心配置、Agent 可靠性 和 平台集成稳定性**。尽管尚未合并，但代码质量和对细节的关注是积极的信号。

## 4. 社区热点

今日社区讨论的热点主要集中在 **本地模型集成** 的相关问题上。

- **热点 Issue：#952 `[bug] Local model using ollama returns incomplete answers`**
  - **分析**：用户 `bloodgroup-cplusplus` 报告了使用 Ollama 运行本地 Gemma 模型时，Agent 的回答不完整。这是今日唯一被报告的 Issue，目前暂无评论和点赞，但问题性质比较严重（核心功能异常）。该问题背后反映了社区对 **本地化部署和模型兼容性** 的强烈诉求。用户期望 Agent 能无缝对接主流的本地模型运行框架（如 Ollama），并保持输出的完整性。

## 5. Bug 与稳定性

今日报告了一个 Bug，暂无严重度评分，但涉及核心功能，需要重点关注。

- **严重（核心功能异常）**：
    - **[BUG] 本地模型（Ollama）回答不完整 (#952)**
      - **描述**：使用 `ollama pull gemma` 后启动 Agent，Agent 无法输出完整的句子。
      - **状态**：Open，无评论，无关联 PR。
      - **链接**：[https://github.com/nullclaw/nullclaw/issues/952](https://github.com/nullclaw/nullclaw/issues/952)
      - **判断**：此 Bug 直接影响了 Agent 作为对话助手的核心价值。可能原因包括：Ollama 响应流解析错误、Token 长度限制、或模型输出后处理逻辑缺陷。**当前无对应的 fix PR**，需要维护者尽快定位根因。

## 6. 功能请求与路线图信号

目前没有用户明确提出的新功能请求，但从已有的 PR 中可以看出项目的演进方向：

- **更精细的配置控制**：PR #949 直接响应了用户（或开发者）需要更灵活控制 Agent 行为的诉求。`queue_mode` 的可配置化暗示了项目可能正在准备支持如 `FIFO`（先进先出）、`Random`（随机）、`Latest`（最新）等不同队列调度策略，这将是 Agent 性能优化的一个重要方向。
- **Agent 输出的“洁净度”和准确性**：PR #951 的修复表明项目非常重视 Agent 输出的质量，避免将非预期的系统日志混淆为用户可见的响应。这符合一个**生产级 AI 助手**的标准。
- **高可用性与平台稳定性**：PR #953 对 Discord 连接重连机制的增强，是项目走向成熟的关键信号。这暗示了团队正在努力确保 Agent 能在 7x24 小时运行，并能优雅地从网络故障中恢复。

**路线图信号**：**项目目前的重心并非开发新功能，而是夯实基础**——提升可配置性、优化开发者体验与错误处理、并增强平台集成层的健壮性。下一版本的发布很可能将包含这些修复。

## 7. 用户反馈摘要

由于今日活跃的讨论较少，代表性反馈主要来自 Issue #952：

- **核心痛点**：用户因本地模型无法正常工作而感到困扰。用户已经按照文档步骤操作（下载模型、启动 Agent），但未能获得预期体验。这构成了一个 **“入门即失败”** 的用户体验问题，可能影响新用户的留存。
- **使用场景**：用户明显是希望利用本地模型（Gemma，通过 Ollama）进行私有化、低成本的 AI 交互。这是目前 AI 助手领域最热门的使用场景之一。
- **满意度**：明确的不满意。用户通过详细的截图提交了 Bug，说明其足够重视该项目，但核心功能的失败可能会动摇其使用信心。

## 8. 待处理积压

今日无长期未响应的积压 Issue 或 PR。

**综述**：NullClaw 正处于一个健康的、以稳定性为导向的迭代周期。社区和开发者都在集中精力解决核心 Bug 和提升健壮性。虽然缺少新功能进展，但当前的修复工作为未来的功能开发奠定了坚实的基础。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw 项目 GitHub 数据生成的 2026-06-13 项目动态日报。

***

### IronClaw 项目日报 - 2026-06-13

**分析师**：AI 智能体与个人 AI 助手领域开源项目分析师

---

#### 1. 今日速览

IronClaw 项目今日保持**极高活跃度**，24小时内完成了50个 Issue 和50个 PR 的更新，社区和核心团队的贡献密集。项目重心明确集中在 **Reborn** 引擎的体验打磨和稳定性提升上，尤其是在 `DeferredBusy` 消息处理、用户授权持久化、附件功能集成以及 Slack 渠道拓展等关键领域。尽管没有新版本发布，但大量 PR 的合并和待定状态表明项目正在进行一次重要的架构演化和 Bug 修复浪潮。安全审计和 CI/CD 基础设施的改进也在同步推进。

#### 3. 项目进展

今日项目在多个核心功能线上取得显著进展，通过合并和关闭重要 PR，系统架构和用户体验均有提升。

- **核心架构与消息处理**：核心开发者 **henrypark133** 关闭了关于 `DeferredBusy` 消息处理的多个关键 Issue（[#4817](https://github.com/nearai/ironclaw/issues/4817)、[#4831](https://github.com/nearai/ironclaw/issues/4831)、[#4832](https://github.com/nearai/ironclaw/issues/4832)、[#4833](https://github.com/nearai/ironclaw/issues/4833)），并提交了全新的 PR [#4838](https://github.com/nearai/ironclaw/pull/4838)，**推翻了**此前复杂的自动排空策略，转向更简洁的“明确拒绝，用户重试”模式，这标志着项目在复杂状态管理上的一次重要反思和简化。同时，PR [#4812](https://github.com/nearai/ironclaw/pull/4812)（`DeferredBusy` 排空）和 PR [#4836](https://github.com/nearai/ironclaw/pull/4836)（运行时上下文切片）的开启，表明项目架构正在向更透明、更可观测的方向演进。
- **用户授权与持久化**：PR [#4835](https://github.com/nearai/ironclaw/pull/4835) 解决了社区热议的“跨线程始终允许”问题（[#4825](https://github.com/nearai/ironclaw/issues/4825)），将用户在一次对话中的“始终允许”授权扩展到该用户与同一智能体的所有对话中，显著提升了用户体验。
- **用户体验 (UX) 修复**：开发团队 **sunglow666** 报告并关闭了多达19个 Reborn UI 相关的 Bug，这些 Bug 广泛涉及 Sidebar 功能、`PINNED` 状态、模型选择器、链接行为、消息显示、草稿保存、SSO 流程等多个方面。这表明经过前期密集的功能开发后，项目目前正经历一轮集中的 UI/UX 问题修复和打磨阶段。
- **安全与合规**：开发者 **zmanian** 推进了安全审计基础架构，合并了关于记录 MCP 直接租赁拒绝（PR [#4561](https://github.com/nearai/ironclaw/pull/4561)）、授权续期失败（PR [#4562](https://github.com/nearai/ironclaw/pull/4562)）以及能力调用扇出限制（PR [#4568](https://github.com/nearai/ironclaw/pull/4568)）的 PR，增强了系统的可审计性和风险控制能力。
- **测试与 CI/CD**：PR [#4773](https://github.com/nearai/ironclaw/pull/4773) 建立了 Reborn 运行时的 QA 轨迹录制/回放机制，为提高测试覆盖率和可靠性打下基础。PR [#4829](https://github.com/nearai/ironclaw/pull/4829) 则旨在优化 CI 流程，消除冗余工作流，并将 Reborn 测试纳入更深的夜间测试。

#### 4. 社区热点

今日社区讨论最热烈的议题集中在 **Reborn 引擎的体验一致性和模型行为**上。

- **核心问题：运行时信息缺失**：Issue [#4828](https://github.com/nearai/ironclaw/issues/4828)（Surface connected channels...）吸引了关注，因为其论及的“模型（LLM）对自身所处的运行环境（如已连接的渠道、消息传递状态等）一无所知”这一问题，是导致许多用户困惑的根本原因。用户发现在完成 Slack 账户连接后，模型依然无法正确地发送消息，这背后正是模型缺乏运行时上下文“心智模型”的体现。该 Issue 直接催生了 PR [#4836](https://github.com/nearai/ironclaw/pull/4836)，显示出社区反馈对项目发展方向有直接影响。
- **用户痛点：LLM 的时间感知缺失**：Issue [#4796](https://github.com/nearai/ironclaw/issues/4796)（LLM lacks awareness of current date/time）明确指出，模型在回答时间敏感问题时（如日程安排）会假设错误的时间，这直接导致其在“任务/提醒”类功能上不可用。该问题将低层次的 API 设计（没有自动注入时间）与高层次的功能体验（日程管理不可靠）直接关联起来，是典型的用户体验瓶颈。
- **热点 Bug：工具调用失败后状态错乱**：Issue [#4762](https://github.com/nearai/ironclaw/issues/4762)（Failed tool workflow causes follow-up messages...）描述了在工具调用失败后，对话状态和信息顺序出现不一致的严重问题。这表明在 Reborn 引擎的错误处理流程中，状态机可能存在未覆盖的边界情况，影响了对话的连续性和可靠性。

#### 5. Bug 与稳定性

今日报告了较多 Bug，主要集中于 Reborn 体验和系统稳定性方面，按严重程度排列：

- **（严重）安全依赖项警报**：Issue [#4824](https://github.com/nearai/ironclaw/issues/4824) 报告了 `cargo-deny` CI 因新发现的 `postgres` crate 安全公告（RUSTSEC）而失败。这是一个全局性阻塞问题，影响所有分支和 PR，需立即升级依赖库。**已有 Issue 但无对应 Fix PR。**
- **（高）工具调用失败导致状态不一致**：Issue [#4762](https://github.com/nearai/ironclaw/issues/4762) 报告工具工作流失败后，后续消息和活动排序错乱。此问题直接影响核心对话流程的可靠性。**当前无关闭的 Fix PR。**
- **（中）工作区路径重复**：Issue [#4759](https://github.com/nearai/ironclaw/issues/4759) 报告使用相对路径创建文件时，路径被错误地重复。这会干扰需要文件系统操作的自动化工作流。**当前无关闭的 Fix PR。**
- **（低-中）多个 UI 交互与反馈问题**：一系列由 **sunglow666** 报告的 UI 问题，如附件警告持久化（[#4720](https://github.com/nearai/ironclaw/issues/4720)）、草稿丢失（[#4724](https://github.com/nearai/ironclaw/issues/4724)）、界面闪烁（[#4719](https://github.com/nearai/ironclaw/issues/4719)）等，已被修复并关闭。
- **（低）新 Bug 报告**：今日新增了多个 UI/UX 相关的 Bug，如删除运行中对话无反馈（[#4823](https://github.com/nearai/ironclaw/issues/4823)）、附件警告在亮色主题下看不清（[#4819](https://github.com/nearai/ironclaw/issues/4819)）等，目前均处于 OPEN 状态，尚未有 Fix PR。

#### 6. 功能请求与路线图信号

从今日活跃的 PR 和 Issue 中，可以观察到未来功能演进方向：

- **增强运行时透明度**：PR [#4836](https://github.com/nearai/ironclaw/pull/4836) 和 PR [#4835](https://github.com/nearai/ironclaw/pull/4835) 表明，**让 LLM 感知其运行时上下文（渠道、授权、时间等）** 是当前最重要的设计方向，很可能优先进入下一版本。
- **附件功能集成**：由 **ilblackdragon** 发起的一系列 PR（[#4738](https://github.com/nearai/ironclaw/pull/4738)、[#4655](https://github.com/nearai/ironclaw/pull/4655)、[#4670](https://github.com/nearai/ironclaw/pull/4670), [#4668](https://github.com/nearai/ironclaw/pull/4668)、[#4654](https://github.com/nearai/ironclaw/pull/4654)）正在全栈推进附件功能，从格式注册、字节存储、透传到前端 UI。这是一个大型功能（Track 2, 3, 6），考虑到 PR 数量和复杂度，**附件上传与模型交互**很可能是一个里程碑式的版本目标。
- **Re-examine 与 QA 路径**：PR [#4773](https://github.com/nearai/ironclaw/pull/4773) （轨迹录制回放）和 PR [#4837](https://github.com/nearai/ironclaw/pull/4837) （空回复时自动追问）的开启，暗示项目正在**系统性提升 Reborn 引擎的对话质量和可测试性**，这将是确保 Reborn 引擎达到生产级质量的关键。
- **Slack 渠道深度集成**：PR [#4777](https://github.com/nearai/ironclaw/pull/4777) 和 [#4778](https://github.com/nearai/ironclaw/pull/4778) 聚焦于解决 Slack 集成的断连重连和状态同步问题，表明**将 Slack 作为生产级渠道进行深度集成**是近期路线图的优先事项之一。

#### 7. 用户反馈摘要

从今日的 Issues 评论和报告中，可以提炼以下用户痛点：

- **“为什么又说我连接了，但就是发不了消息？”**：用户报告在完成 Slack 连接后，模型仍然无法发送消息。此问题反映的是系统缺乏对模型进行“运行时状态”通知的机制。
- **“我刚允许它访问，换了个窗口又要我允许一遍？”**：用户对“始终允许”的跨线程失效感到困惑，这是导致用户对授权系统产生不信任感的典型缺陷。PR [#4835](https://github.com/nearai/ironclaw/pull/4835) 正在解决此问题。
- **“我问它明天有什么安排，它给我一个错误的日期。”**：用户期望 AI 助手能理解“今天”、“明天”等时间概念，但 LLM 的默认行为是猜测，导致日程类功能无法使用。
- **“工具失败后，整个对话就乱了。”**：当进行文件下载等工具操作失败后，后续的对话逻辑和消息显示顺序出现问题，严重影响用户对系统稳定性的评价。

#### 8. 待处理积压

以下为需要维护者关注的重要长期未决项：

- **新版本发布 PR 长期开放**：PR [#3708](https://github.com/nearai/ironclaw/pull/3708) (“chore: release”) 从2026-05-16起已开放近一个月，且包含 API 破坏性变更。反复的变更加之 CI 安全检查（[#4824](https://github.com/nearai/ironclaw/issues/4824)）失败，可能导致版本发布长期延迟，阻碍使用者获取最新功能和修复。**这是当前最关键的积压项。**
- **核心 CI 检查失败**：Issue [#4824](https://github.com/nearai/ironclaw/issues/4824) 报告的 `cargo-deny` 失败**严重阻塞了所有 PR 的合入**，应作为最高优先级处理，升级或规避依赖库的安全问题。
- **大型功能 PR 长期开放**：多个与附件功能相关的大规模 PR（如 [#4738](https://github.com/nearai/ironclaw/pull/4738)、[#4655](https://github.com/nearai/ironclaw/pull/4655)、[#4654](https://github.com/nearai/ironclaw/pull/4654)）以及安全相关的 PR（[#4561](https://github.com/nearai/ironclaw/pull/4561)）从6月上旬起开放至今，虽然活跃但未合入主分支。这可能表明其代码审查或集成测试的复杂度较高，需要更多精力推动。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是为您生成的 LobsterAI 项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-13

## 1. 今日速览

过去24小时，LobsterAI 项目活跃度**高**，核心关注点为 **2026.6.12 版本的发布与稳定性修复**。项目成功合并了发布分支，引入了 **Computer Use MVP、实时语音输入、以及 HTML/图片 Artifact 共享**等多项重大功能。同时，团队修复了多个关键问题，包括对已停止流的模型元数据展示和同名的包模型选择问题。社区方面，几个由 `MaoQianTu` 提交的关于防止内容丢失的 PR 在今日被关闭，显示出社区贡献者正重点关注用户体验的细节打磨。

## 2. 版本发布

*无新版本发布。* 昨日（2026-06-12）合并的 `release/2026.6.11` 分支 (PR #2158) 是近期最重要的版本更新，主要内容包括：
- 新增 **Computer Use MVP** 和内置的 Computer Use 工具包。
- 为 coworK 提示词添加了 **实时 ASR（自动语音识别）语音输入**功能。
- 增加了 **HTML Artifact 公共分享模式选择**。
- 支持 **图片和 SVG Artifact 分享**。

## 3. 项目进展

今日合并/关闭了11个 PR，主要集中在 **错误修复** 和 **发布管理** 上，巩固了昨日的版本发布。

- **发布管理**:
    - **[PR #2158]** [CLOSED] `chore(release): merge release/2026.6.11 into main`: 正式将 2026.6.11 版本分支合并入主分支，标志着该版本所有功能的整合完成。[netease-youdao/LobsterAI PR #2158](https://github.com/netease-youdao/LobsterAI/pull/2158)

- **功能修复与完善 (Cowork/OpenClaw)**:
    - **[PR #2154]** [CLOSED] `fix(cowork): show model metadata after stopped streams`: 修复了手动停止流式响应后，模型元数据不显示的问题，改善了用户查看已停止回复的体验。[netease-youdao/LobsterAI PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154)
    - **[PR #2153]** [CLOSED] `fix(cowork): preserve same-name package model selection`: 修复了在 OpenClaw 模型规范化过程中，同名的包（package）模型和自定义模型的选中状态会丢失或混淆的问题。[netease-youdao/LobsterAI PR #2153](https://github.com/netease-youdao/LobsterAI/pull/2153)
    - **[PR #2155]** [CLOSED] `fix(voice-input): prevent duplicate realtime ASR starts`: 修复了 cowork 语音输入流程中可能导致重复启动实时 ASR 的竞态条件问题。[netease-youdao/LobsterAI PR #2155](https://github.com/netease-youdao/LobsterAI/pull/2155)

- **功能修复 (其他)**:
    - **[PR #2156]** [CLOSED] `fix(computer-use): bump runtime to 1.0.7`: 更新了 Computer Use 的运行环境到 1.0.7 版本，包含了对意外退出的诊断优化。[netease-youdao/LobsterAI PR #2156](https://github.com/netease-youdao/LobsterAI/pull/2156)
    - **[PR #2157]** [CLOSED] `fix(media): 修正文生图保存图片的扩展名`: 修复了保存 AI 生成的图片时，文件扩展名与图片真实格式不符的问题（如 PNG 内容被保存为 .jpg），增强了兼容性。[netease-youdao/LobsterAI PR #2157](https://github.com/netease-youdao/LobsterAI/pull/2157)

- **社区贡献 (细节体验优化)**: 社区贡献者 `MaoQianTu` 提交的一系列针对内容丢失的修复 PR 均在今日被关闭，显著提升了用户界面操作的安全性。
    - **[PR #1473]** [CLOSED] `fix: 创建Agent弹窗关闭时添加未保存确认，防止内容静默丢失` [netease-youdao/LobsterAI PR #1473](https://github.com/netease-youdao/LobsterAI/pull/1473)
    - **[PR #1474]** [CLOSED] `fix: Agent设置面板关闭时添加未保存确认，防止配置静默丢失` [netease-youdao/LobsterAI PR #1474](https://github.com/netease-youdao/LobsterAI/pull/1474)
    - **[PR #1475]** [CLOSED] `fix: MCP服务器配置弹窗关闭或按Escape时添加未保存确认，防止配置静默丢失` [netease-youdao/LobsterAI PR #1475](https://github.com/netease-youdao/LobsterAI/pull/1475)
    - **[PR #1476]** [CLOSED] `fix: 切换会话或导航视图时输入框草稿立即持久化，防止内容丢失` [netease-youdao/LobsterAI PR #1476](https://github.com/netease-youdao/LobsterAI/pull/1476)
    - **[PR #1477]** [CLOSED] `fix: 重新编辑历史消息时添加覆盖确认，防止当前输入内容静默丢失` [netease-youdao/LobsterAI PR #1477](https://github.com/netease-youdao/LobsterAI/pull/1477)

## 4. 社区热点

今日社区讨论热度较低，但以下 Issue 和 PR 值得关注：

- **[Issue #1]** [CLOSED] `hit API error with OpenAI API Type`: 此 Issue 是项目中唯一有评论的，共7条。虽然今日已关闭，但反映了用户在使用非官方、非标准的 API（如 MiniMax）并配置为 OpenAI 类型时遇到的兼容性问题。这表明用户对灵活配置不同 AI 后端有强烈需求，但也暴露了在处理非标准 API 时的潜在缺陷。[netease-youdao/LobsterAI Issue #1](https://github.com/netease-youdao/LobsterAI/issues/1)

- **[PR #1446]** [OPEN] `fix(openclaw): 修复网关反复启动失败导致的无限重启循环`: 此 PR 虽然已经标记为 `stale`，但其描述的“应用瘫痪”场景非常严重，任何用户都可能遇到，是潜在的社区痛点。[netease-youdao/LobsterAI PR #1446](https://github.com/netease-youdao/LobsterAI/pull/1446)

## 5. Bug 与稳定性

今日无新报告的严重 Bug。今日修复的Bug集中在以下方面：

- **中等级别**:
    - **图片扩展名错误 (PR #2157)**: 保存 AI 生成的 PNG 图片时，文件后缀可能是 .jpg 或 .webp，影响图片的正常使用。
    - **已停止流响应无元数据 (PR #2154)**: 手动中断 AI 回复后，无法看到模型等元数据信息。
    - **同名模型选择状态丢失 (PR #2153)**: 当存在同名的包模型和自定义模型时，模型选择状态可能被错误地同步或丢失。
- **低等级别**:
    - **重复启动语音识别 (PR #2155)**: 偶发性问题，可能导致系统资源浪费。
    - **多个弹窗未保存内容丢失 (PR #1473, #1474, #1475)**: 社区贡献修复的一系列细节问题，提升了 UI 交互的稳定性。

## 6. 功能请求与路线图信号

今日无新增功能请求。但从合并的 PR 和版本发布内容来看，以下方向是清晰的路线图信号：

- **Computer Use 能力**: 内置 Computer Use 工具包和提升运行时版本，表明该项目正在积极构建 AI 代理操作计算机的能力。
- **语音交互**: 实时 ASR 语音输入的支持，是提升协作（Cowork）模式交互体验的重要一步。
- **Artifact 分享**: 对 HTML 和图片 Artifact 的分享支持，表明项目在“结果导出”和“协作展示”上持续投入。`PR #2157` 修复图片扩展名问题，也佐证了这一方向。

## 7. 用户反馈摘要

从唯一的活跃 Issue (#1) 来看，用户 `simson2010` 的反馈揭示了以下痛点：
- **痛点**：尝试使用非 OpenAI 标准的 API（如 MiniMax）并模拟 OpenAI 接口时，遭遇了难以解析的 `invalid params` 错误。这表明项目的 API 兼容性验证有待加强。
- **使用场景**：用户希望利用更便宜或特定性能的第三方 API 服务，但配置过程不顺畅。
- **满意度**：用户为此创建了一个 Issue，但没有点赞，说明提供的信息可能未能完全解决问题，或问题已通过其他方式解决（Issue已关闭）。核心诉求是更稳定的 API 适配。

## 8. 待处理积压

以下 PR 已经 **停滞超过2个月**，可能面临合并冲突或被遗忘的风险。这些都是经过社区评审的修复性工作，建议维护者关注。

- **[PR #1446]** `fix(openclaw): 修复网关反复启动失败导致的无限重启循环` - 严重性：**高**，可能导致应用崩溃。[netease-youdao/LobsterAI PR #1446](https://github.com/netease-youdao/LobsterAI/pull/1446)
- **[PR #1448]** `fix(i18n): Agent 设置页面删除按钮及技能选择器显示英文` - 严重性：**中**，影响非英文用户的体验。[netease-youdao/LobsterAI PR #1448](https://github.com/netease-youdao/LobsterAI/pull/1448)
- **[PR #1449]** `feat(cowork): 定时任务多次执行记录折叠分组展示` - 严重性：**低**，功能优化请求。[netease-youdao/LobsterAI PR #1449](https://github.com/netease-youdao/LobsterAI/pull/1449)
- **[PR #1453]** `fix(skills): 修复已停用技能仍被注入对话提示词的问题` - 严重性：**高**，功能性 Bug。[netease-youdao/LobsterAI PR #1453](https://github.com/netease-youdao/LobsterAI/pull/1453)
- **[PR #1454]** `fix(scheduled-tasks): 不重复模式清空日期后点击创建任务按钮无响应` - 严重性：**高**，功能性 Bug。[netease-youdao/LobsterAI PR #1454](https://github.com/netease-youdao/LobsterAI/pull/1454)
- **[PR #1456]** `fix(shortcuts): 修复快捷键设置缺少重复检测的问题` - 严重性：**中**，设置功能 Bug。[netease-youdao/LobsterAI PR #1456](https://github.com/netease-youdao/LobsterAI/pull/1456)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的 Moltis 项目数据生成的 2026-06-13 项目动态日报。

---

## Moltis 项目日报 | 2026-06-13

**分析师点评：** 今日项目活跃度中等，社区讨论主要集中在三个新提出的或更新的议题上，涉及关键的功能扩展和Bug修复。虽然没有新的版本发布和PR合并，但社区贡献者明确提出了安全性强化和本地化能力提升的重要需求，显示出项目生态的健康发展。

### 1. 今日速览

- 项目过去24小时内无新的版本发布或PR合并，开发节奏趋于平稳，重点可能转向了内部开发或新问题的评估。
- 社区提交了3个新的或活跃的 Issue，其中包括1个明确的Bug报告和2个功能请求，体现了用户社区的积极参与。
- 功能请求的讨论非常具有前瞻性，分别指向了**Kubernetes原生沙箱**（用于提升Agent执行的安全性）和**本地语音识别**（降低延迟和依赖），这反映了用户对Agent安全性和自主性提升的迫切需求。
- 一个关于Fastmail MCP（模型上下文协议）认证的Bug报告被提出，但尚未有对应的修复PR，建议维护者关注。

### 2. 版本发布

无

### 3. 项目进展

**无。** 今日没有已合并的Pull Requests，因此没有新的功能或修复被合并到主分支。

### 4. 社区热点

今日讨论最活跃的Issue主要有两个：

1.  **#1118 [Feature]: Add Kubernetes-native sandbox backend with runtimeClassName support**
    - **链接：** [Issue #1118](https://github.com/moltis-org/moltis/issues/1118)
    - **分析：** 该Issue提出了一个极具战略价值的想法，即引入Kubernetes原生的沙箱后端。用户希望利用Kubernetes的`runtimeClassName`功能，将Agent执行的代码隔离在如Kata Containers或gVisor这样的虚拟机级别沙箱中。这直接回应了“执行LLM生成的不可信代码”这一核心安全挑战，如果被采纳，将显著提升Moltis在企业级和敏感环境中的信任度。

2.  **#1102 [Feature]: Add FunASR/SenseVoice as local STT engine**
    - **链接：** [Issue #1102](https://github.com/moltis-org/moltis/issues/1102)
    - **分析：** 该请求呼吁集成FunASR或SenseVoice作为本地语音转文字引擎。用户强调了其极低的延迟（SenseVoice-Small处理10秒音频仅需约70ms）和原生流式推理能力。这背后是用户对**更低的云端依赖、更快的响应速度以及更好的离线体验**的追求，这将是Moltis在智能体领域保持竞争力的关键特性。

### 5. Bug 与稳定性

- **#1115 [Bug]: Fastmail MCP Authorisation**
    - **严重程度：** **高**
    - **链接：** [Issue #1115](https://github.com/moltis-org/moltis/issues/1115)
    - **状态：** 未关闭，无关联修复PR。
    - **分析：** 用户报告了在使用Fastmail的MCP（模型上下文协议）集成时遇到认证问题。MCP是Moltis与外部服务互动的关键协议，该Bug可能直接影响用户配置邮件服务的功能。由于是认证问题，可能涉及API密钥、OAuth流程或权限范围，需要优先排查。

### 6. 功能请求与路线图信号

结合今日的Issues，可以清晰地看到社区对以下两个方向的强烈需求，很可能会被纳入后续版本的路线图：

1.  **Kubernetes企业级部署与安全增强（#1118）：** 该请求明确指向了企业级用户的痛点。配合`runtimeClassName`的支持，Moltis可以无缝嵌入到现有的Kubernetes生态中，利用成熟的容器安全解决方案来隔离Agent行为，是走向生产环境的关键一步。
2.  **本地语音交互能力（#1102）：** 继大洋彼岸的“Local-first”、“On-device AI”趋势后，社区对更低延迟、更私密的语音交互的需求日益增长。引入FunASR/SenseVoice不仅能提升响应速度，还能降低对云服务的依赖，实现完全离线的语音助手体验。

### 7. 用户反馈摘要

- **痛点/使用场景：**
    - **安全问题：** 用户在#1118中明确指出，当前Moltis的Agent在“执行LLM生成的不可信代码”时存在安全风险，这一痛点非常真实且普遍。
    - **交互延迟：** 在#1102的请求中，用户期望SenseVoice等模型能提供“超快”的语音识别，以提升对话体验的实时性。
- **不满意的地方：**
    - 在Bug #1115中，用户试图配置Fastmail的MCP集成，但遇到了认证故障，这意味着当前版本的MCP集成在外部服务认证方面可能存在稳定性或兼容性问题，导致用户体验受阻。

### 8. 待处理积压

- **#1115 [Bug]: Fastmail MCP Authorisation**
    - 该Bug报告的认证问题直接关系到核心功能“外部服务集成”的可用性。建议**维护者尽快与Fastmail API文档核对**，或要求用户提供更详细的错误日志，以便快速定位问题。该问题自2026-06-11创建，已两天未分配，需要引起注意。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是为您生成的 CoPaw 项目 2026年6月13日 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-06-13

## 今日速览

CoPaw 项目在过去24小时内保持高度活跃。Issue与PR更新总量接近50条，社区参与度强劲。尽管无新版本发布，但团队在Bug修复和版本发布准备工作上投入了大量精力，核心聚焦于缓解v1.1.11系列版本引入的稳定性与回归问题。值得关注的是，`AgentScope 2.0` 后端迁移的讨论正逐步走向具体实施路径，且多个高价值功能（如外观模型降级、DataPaw插件）已进入审查阶段，预示着项目架构与功能集即将迎来重要更新。

## 项目进展

今日团队在问题修复和预发布质量保障上取得了显著进展，合并了多个关键PR，为下一个正式版铺平了道路。

- **版本打标与发布准备**：
    - **PR #5159 (已合并)**: 修正了版本号格式，将版本从 `1.1.12.beta1` 调整为 `1.1.12b1`，这是在为下一个beta版本做最后准备。
    - **PR #5121 (已合并)**: 引入“发布验证关卡（Release Verification Gate）”，这是一个CI/CD流程的强化，确保构建产物（如Docker镜像）在发布前能通过端到端的启动与健康检查，此举将显著提升未来版本的稳定性。

- **UI与前端体验修复**：
    - **PR #5144 (已合并)**: 修复了长期记忆配置丢失的严重Bug，通过在UI层面强制渲染折叠面板内的表单元素，解决了因用户未展开面板而导致的配置无法保存的问题。
    - **PR #5147 (已合并)**: 修复了Coding Mode下刷新页面后Session丢失，回退到第一个Session的回归问题。
    - **PR #5154 (已合并)**: 修复了自动记忆搜索工具在UI上显示结果异常的Bug（Issue #5098），优化了搜索结果表格的样式。

- **环境修复**：
    - **PR #5022 (已合并)**: 强化了Agent工作区路径的安全验证，防止用户将工作区设置在QwenPaw管理的敏感目录（如 `plugins`, `secrets`）内，提升了系统安全性。

## 社区热点

今日社区讨论的热点主要集中在新功能的请求和用户对近期Bug的反馈上。

1.  **[Issue #5064] Agent创建定时任务无法触发 (bug)**
    - **链接**: [Agentscope-ai/QwenPaw Issue #5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)
    - **热度**: 评论数11，是今日讨论最热烈的问题。
    - **诉求**: 用户在会话中指示Agent创建定时任务，任务创建过程无报错，但到达时间后无法自动触发，且无法手动编辑。这暴露了Agent驱动任务执行链路中的核心断点，是影响Agent自主工作能力的关键Bug。

2.  **[Issue #4727] [Breaking Change]后端向AgentScope 2.0迁移 (开发讨论)**
    - **链接**: [Agentscope-ai/QwenPaw Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)
    - **热度**: 长期存在的讨论帖，持续有10条评论，获2个赞。
    - **诉求**: 社区对QwenPaw依赖的底层架构升级高度关注。尽管这是一个破坏性变更，但用户的呼声很高，期待借此获得新架构、新API带来的性能提升和功能拓展。

3.  **[Issue #5156] 建议支持 kimi-for-coding (功能请求)**
    - **链接**: [Agentscope-ai/QwenPaw Issue #5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)
    - **热度**: 3条评论，反映出用户对模型接入多样性的需求。
    - **诉求**: 已付费订阅Kimi Coding套餐的用户，无法直接在QwenPaw中使用该能力，只能走标准API。这提示项目需要考虑对特殊“API套餐”或“专业版”模型的白名单支持，以提升付费用户的粘性。

## Bug 与稳定性

今日报告的Bug主要围绕 `v1.1.11` 系列的回归问题和稳定性缺陷，严重程度较高。

- **严重 - 进程膨胀与内存泄漏**:
    - **Issue #5138**: 报告Windows客户端在运行后进程数持续增加，内存占用可达90%以上。这是一个严重的性能退化问题，可能导致用户无法正常使用。
    - **Issue #5155**: Docker环境部署的 `v1.1.11` 版本出现自动宕机重启。

- **严重 - 功能回归**:
    - **Issue #5163**: 用户确认 `v1.1.11.post2` 相比 `v1.1.10` 存在回归，导致 Gemini 模型的工具调用（Tool Calling）功能失效。
    - **Issue #5140 (已关闭)**: 报告 `v1.1.11.post2` 附件下载仍有Bug，docx/pdf等非纯文本文件下载报404错误。该问题已被标记为已关闭，可能已在内部修复。

- **中低 - UI/渲染问题**:
    - **Issue #5148 (已关闭)**: 网页UI渲染数学公式时，根号显示异常（被显示为一行）。
    - **Issue #5161**: 长对话后客户端无响应，可能涉及上下文管理或内存泄漏。
    - **Issue #5162**: 对话思考逻辑陷入死循环。
    - **Issue #5165**: 使用官方打包脚本生成的Windows安装包启动后白屏，原因是引用了不存在的Python模块 (`qwenpaw.app.api`, `qwenpaw.app.middleware`)。 **注意**: 已有修复PR #4900在处理类似问题。

## 功能请求与路线图信号

- **Agent协作与能力扩展**:
    - **Issue #5139**: 呼声较高的功能，建议参考WorkBuddy、九文Swarm等，为CoPaw添加原生Agent团队/集群协作能力，以解决复杂任务。
    - **PR #5067 (审查中)**: 提出“Agent OS Driver”概念，旨在统一抽象外部能力（如MCP、A2A协议），这可能是实现Agent协作和生态扩展的核心基础设施。

- **开发者体验与平台支持**:
    - **Issue #5164**: 用户建议完善桌面版的系统托盘、开机自启、后台常驻等“服务”能力，使其更像一个成熟的本地应用。
    - **PR #5153 (开放中)**: 将Tauri客户端的“即时窗口”启动优化移植到pywebview客户端，提升Windows用户的启动体验。

- **新功能预警**:
    - **PR #5069 (审查中)**: 为纯文本模型提供“视觉模型降级”能力。当主模型不支持图像/视频时，可配置一个辅助模型将内容转为文本。这个PR若被合并，将极大扩展模型兼容性。
    - **PR #4622 (审查中)**: 提交了一个名为 `DataPaw` 的数据分析插件，包含12个BI技能，旨在增强Agent在数据分析领域的专业能力。

## 用户反馈摘要

- **痛点**: 用户对于Agent生成的定时任务**无法正常触发**表示困惑 (`#5064`)，这直接动摇了Agent作为生产力工具的可靠性。此外，近期版本（`1.1.11`）的**稳定性问题**（内存泄漏、宕机）是用户反映最强烈的负面体验。
- **场景**: 用户明确提出了将QwenPaw用于**生产环境**（Docker部署 `#5155`）和作为**本地工具**（`#5165` 打包为exe）的需求，这表明项目正从小众尝鲜走向严肃应用。
- **满意/不满意**:
    - **满意**: 用户对视觉模型降级 (`PR #5069`)、更好的CI (`PR #5121`) 等工程改进表示欢迎。
    - **不满意**: 部分用户对“bug修了但引入新bug”的循环感到沮丧，如附件下载问题 (`#5140`) 和Gemini tool calling回归 (`#5163`) 的反复出现。

## 待处理积压

- **[Issue #4727] [Breaking Change] 后端向AgentScope 2.0迁移**
    - **链接**: [Agentscope-ai/QwenPaw Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)
    - **状态**: 已存在超过半个月，虽有关联讨论，但至今没有明确的PR与之关联。鉴于其Breaking Change的属性和社区高度关注，维护团队需要尽快给出明确的Roadmap或时间表。

- **[PR #4622] DataPaw 数据分析插件**
    - **链接**: [Agentscope-ai/QwenPaw PR #4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)
    - **状态**: 已提交三周，处于“Under Review”状态。这是一个由社区贡献的复杂度高、功能完整的插件。如果长时间不合并或给出明确反馈，可能会打击贡献者的积极性。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeroClaw 项目 GitHub 数据，我为您生成了 2026-06-13 的项目动态日报。

---

## ZeroClaw 项目日报 - 2026-06-13

### 1. 今日速览

ZeroClaw 项目今日进入 **v0.8.0 发布后的密集修复与迭代期**，社区活跃度极高。24 小时内产生 **33 条 PR** 和 **14 条 Issue**，显示出维护团队与社区正积极处理新版本引入的各类 Bug 与遗留技术债务。核心热点集中在**架构统一**（特别是 `agent turn engines` 的合并）、**用户体验优化**（Dashboard 不可用、Session 管理）以及 **平台兼容性修复**（Windows/macOS/Docker）。虽然有大量 PR 积压（29 条待合并），但关键修复已迅速生成 PR，项目整体向 **v0.8.1** 稳定推进，但仍需关注积压维护。

### 3. 项目进展 (重要 PR/Issues 合并与关闭)

今日虽有 **4 条 PR/Issues 被合并/关闭**，但其中部分为验证性或配置更新。最值得关注的是架构层面和修复层面的进展：

*   **核心架构重塑开始落地**：备受关注的 **RFC #7415** 所提出的“统一三个 agent turn engines”计划，已通过 PR **#7540** 进入实施阶段。该 PR 将 `run_tool_call_loop`、`Agent::turn_streamed_with_steering_state` 和 `Agent::turn` 合并为一个，旨在消除代码冗余并统一行为逻辑。这是 `v0.8` 以来最重要的内部架构改进之一。
*   **关键 Bug 修复**：`v0.8.0` 版本的几个严重问题已有对应的修复 PR：
    *   **Gateways Dashboard 不可用 (#7523)**: 不是平台 Bug，而是构建流程未正确触发的错误。已通过提升构建文档和修复 Docker 构建的 PR **#7529** 和 **#7534** 来解决。
    *   **MCP Tools 不可见 (#7263)**: `mcp.enabled` 默认开启后，但工具未出现在 agent 列表中。已有修复 PR **#7547** 待合并。

### 4. 社区热点

今日讨论最热门的是此前遗留的架构问题及其实现：

*   **[RFC #7415] Unify the three agent turn engines**: 该项目内部的重大重构议案。虽然创建于 6月9日，但今日通过维护者指令直接产生了实现 PR **#7540**。社区对此关注度高，因为是影响所有用户场景的核心变更，评论中对其实现方式进行了讨论，但已无阻滞。
*   **[PR #7548] Chore/01.5 cargo cleanup**: 一个规模巨大的杂务清理 PR，涉及数十个模块与 Provider。虽然不引入新功能，但它旨在优化项目依赖和构建流程，是项目健康度维护的重要信号。
*   **[Issue #7523] Dashboard not available**: 这是新用户使用 `v0.8.0` 后遇到的第一个门槛问题。虽然 Issue 本身评论不多，但由于它是 S1级别的阻塞问题，引起维护团队在数小时内快速响应并创建了修复 PR。

**核心诉求**：社区对新版本的可用性和易用性非常敏感，`Dashboard` 这类基础功能不可用会严重打击新用户信心。架构层面的重构虽然不直接可见，但维护者的果断处理表明了其长期致力于代码质量和可维护性的决心。

### 5. Bug 与稳定性

今日报修了大量的 S1（工作流阻塞）级别 Bug，主要集中在 macOS、Windows、Docker 等平台兼容性及核心流程上。

| 严重程度 | 组件 | Bug 描述 | 链接 | Fix PR 状态 |
| :--- | :--- | :--- | :--- | :--- |
| **S1 - Blocked** | web dashboard | v0.8.0 macOS Homebrew 安装后 Dashboard 不可用 | [[#7523]](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | 已提交 PR [#7529] & [#7534] |
| **S1 - Blocked** | runtime/daemon | Windows `zeroclaw quickstart` 失败 | [[#7537]](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | 无 |
| **S1 - Blocked** | runtime/daemon | macOS App 安装后窗口消失、无响应 | [[#7527]](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | 无 |
| **S1 - Blocked** | gateway/api | `ask_user` 工具直接在 WebSocket 会话中失败 | [[#7542]](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | 无 |
| **S1 - Blocked** | Docker | `cargo web build` 因缺少 g++ 失败 | [[#7533]](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) | 已提交 PR [#7534] |
| **S2 - Degraded** | gateway/api | V3 路径使用 `data_dir` 作为 agent 的工作区 | [[#7541]](https://github.com/zeroclaw-labs/zeroclaw/issues/7541) | 无 |

**总结**：`v0.8.0` 的发布虽然带来了新架构，但在打包和跨平台部署上存在较多的兼容性问题。macOS 和 Windows 上的核心安装流程存在 Bug，需要优先解决。

### 6. 功能请求与路线图信号

今日收到多个明确的新功能请求，部分与已有 PR 相关联，可能被纳入 `v0.8.1` 或 `v0.9.0`：

*   **[#7543] Multi-session support in Gateway web chat UI**: 用户要求 Gateway 前端支持多会话管理（新建、切换、删除等）。这是一个高优先级用户体验功能，符合 `v0.8.x` 增强产品可用性的主线。
*   **[#7539] llama.cpp model router**: 用户希望为 `llamacpp` provider 添加模型路由功能，以便快速切换本地模型。这会增强本地使用场景的灵活性。
*   **[#7531] Streaming card messages for QQ/DingTalk/WeChat/Feishu**: 用户希望这些即时通讯渠道支持流式卡片消息，以减少 AI 响应时用户等待的焦虑感。这是针对特定通信渠道的体验优化。
*   **已有 PR 信号**：
    *   **PR #7429** (feat(plugins): add wasmtime dependency) 正在进行中，表示从 Extism 迁移到 wasmtime 的计划正在按部就班推进，这是路线图上的重要一步。
    *   **PR #7524** (feat(channels/discord): derive gateway intents from config) 通过配置化替代硬编码，提升了 Discord 渠道的可维护性。

### 7. 用户反馈摘要

从 Issues 评论和描述中，可以提炼出以下用户痛点：

*   **“我照着手册安装，但 Dashboard 就是打不开”** (#7523, #7527): 这是最大的挫败感来源。用户按照官网步骤操作，但核心 Web UI 无法渲染，严重影响首次使用体验。
*   **“在 macOS 上，按 Cmd+C 却退出了程序”** (#7529的关联 Issue #7528): 一个严重的快捷键冲突，破坏了 Mac 用户最熟悉、最基本的复制粘贴操作，极其影响日常使用。
*   **“`quickstart` 命令在 Windows 上完全不能用，我也不知道哪里错了”** (#7537): 阻止了新用户在 Windows 平台上进一步探索。异常信息不友好 (`no map-keyed/list section at peer-groups`)，对新手极不友好。
*   **“子代理不能继承工作目录”** (#7263): 对于希望使用“子代理开发”模式的用户来说，这是一个工作流完全阻塞的问题。
*   **“为什么编译 Docker 还需要我手动安装 C++ 编译器？”** (#7533): 对于部署自动化流程来说，这是一个构建实践上的瑕疵，增加了部署复杂度。

### 8. 待处理积压

以下是一些长期未解决或等待响应的关键项目，需要提醒维护者关注：

*   **高风险长期待合并 PR**:
    *   **[PR #7429] feat(plugins): add wasmtime dependency** (已创建4天，+42h未更新): 这是一个将决定未来插件生态走向的核心依赖变，需要尽快对其进行代码审查以推进后续的 wasmtime 迁移工作。
    *   **[PR #6842] feat(providers): add NEAR AI Cloud provider** (已创建23天): 一个已经被标记为风险中等的重要 provider 集成 PR，长时间未被合并或关闭，社区贡献者可能需要反馈。
*   **阻塞性 Issue 无修复 PR**:
    *   **[Issue #7537] zeroclaw quickstart 失败 (Windows)**
    *   **[Issue #7527] macOS app not work**
    *   **[Issue #7542] `ask_user` 工具在 Gateway WebSocket 会话失败**
    *   **[Issue #7541] V3 路径使用 data_dir 作为工作区**

这些是当前项目稳定性和用户满意度的主要堵点，建议优先排查并创建修复 PR。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*