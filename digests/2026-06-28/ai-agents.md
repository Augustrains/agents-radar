# OpenClaw 生态日报 2026-06-28

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-28 02:07 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 OpenClaw 项目数据生成的 2026-06-28 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-28

## 1. 今日速览
OpenClaw 项目今日活跃度极高，社区生态表现强劲。过去24小时内，项目共产生500条 Issue 和500条 PR 更新，显示出一个庞大且积极的开源社区。高频的 Issue 创建（487条活跃）表明用户正积极探索和报告问题，但关闭率较低（13条），暗示维护者需加快处理节奏。PR 方面，大量待合并项（451条）可能成为主要瓶颈。值得注意的是，**会话状态一致性、内存泄漏和子代理管理**仍是社区最关注的核心痛点，多个高讨论度的 Issue 均围绕这些主题。

-   **项目健康度评估**：🟡 **高热度，但维护压力巨大**。社区贡献活跃，但 Issue 和 PR 积压严重，维护者响应和合并能力亟待提升。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
过去24小时内，有 49 个 PR 被合并或关闭。以下是其中最关键的几个，代表了项目在稳定性和架构方面的进步。

-   **修复会话死锁与资源泄漏**：`#95833` [已关闭] 修复了子代理中止时未能释放 `.jsonl.lock` 文件锁，导致会话永久中断的严重问题。`#95915` [已关闭] 则解决了嵌入式运行中止后，堆内存未释放及写锁残留的问题，有效避免了内存泄漏和会话卡死。
-   **推进托管市场目录功能**：`#95969` [开放中] 和 `#95964` [已关闭] 是“托管市场目录”功能栈的关键部分。`#95964` 已合并，实现了将市场目录快照持久化到状态管理，这是构建插件/技能分发生态系统的关键一步。
-   **修复 CLI 与嵌入式运行的路径问题**：`#57326` [讨论中] 的修复 PR 虽未提及编号，但其作为高优先级 Issue 的推进，解决了部分助手路径绕过 CLI 调度的问题，有助于提升命令行工具的一致性和安全性。

**总结**：项目在**核心稳定性**（死锁、内存泄漏）和**生态架构**（托管市场）上取得了实质性进展。

## 4. 社区热点
过去24小时内，以下 Issue 和 PR 引发了最热烈的讨论，反映出社区的集体关切。

-   **🎯 [Issue #58450]：Agent承诺跟进后无任何实际行动**
    -   **链接**：[`#58450`](https://github.com/openclaw/openclaw/issues/58450)
    -   **分析**：这是一个“社交工程”层面的 Bug。Agent 在对话结束时通过自然语言承诺“我会查一下资料然后给你回复”，但实际上没有启动任何后台任务。用户感到被欺骗，凸显了 AI 行为透明度和可验证性的深层需求。评论数最高，说明此问题普遍且令人困扰。

-   **🎯 [Issue #92201]：Embedded runner流式thinking签名间歇性无效**
    -   **链接**：[`#92201`](https://github.com/openclaw/openclaw/issues/92201)
    -   **分析**：此问题涉及 Anthropic 模型特有的流式思考签名，在回放时因校验失败导致错误。更关键的是，由于错误文本被泛化，恢复机制无法触发。这暴露了系统在处理**供应商特定协议**时的脆弱性，以及**错误处理分层**的设计缺陷。用户 CarlCapital 的细节报告非常专业，反映了其高端用户群的技术深度。

-   **🎯 [Issue #50090]：社区技能开发与 ClawHub 生态**
    -   **链接**：[`#50090`](https://github.com/openclaw/openclaw/issues/50090)
    -   **分析**：这篇更像是一篇社区宣言而非简单的 Bug 报告。用户 `ocdlmv1` 详细阐述了当前技能插件与 ClawHub 的承诺与实现之间的巨大鸿沟。这不仅是功能需求，更是对项目**开发者体验和生态建设方向**的集中关切。

**小结**：社区热点集中在 **AI 行为的可信度**、**特定模型供应商的兼容性**以及**第三方开发生态系统的成熟度**上。

## 5. Bug 与稳定性
过去24小时内报告的 Bug 主要集中在会话管理和跨组件集成上。以下按严重程度排序：

| 严重程度 | Issue | 摘要 | Fix PR状态 |
| :--- | :--- | :--- | :--- |
| **严重 (Crash/Data Loss)** | `#63216` | 同一会话键重复硬重置，即使在高预留token下也不断溢出，构成崩溃循环。 | 无 |
| **严重 (Crash/Data Loss)** | `#95915` (已关闭) | 嵌入式运行中止后，堆内存未释放，写锁持续存在。 | **已修复** |
| **高 (Functionality Broken)** | `#95833` (已关闭) | 子代理中止无法释放 `.jsonl.lock`，永久性破坏会话。 | **已修复** |
| **高 (Functionality Broken)** | `#66443` | 溢出恢复机制会重复`role=user`消息，放大对话文本，加速下一次溢出。 | 无 |
| **高 (Functionality Broken)** | `#62505` | 编码 Agent 在 `2026.4.2` 版本后完全无法完成任务。这是一个严重回归问题。 | 无 |
| **中 (Behavior/Usability)** | `#65538` | UI 无障碍性（Accessibility）Bug：屏幕阅读器会逐个朗读流式传输的 token。 | 无 |
| **中 (Behavior/Usability)** | `#65624` | Mattermost 插件默认使用明文回调 URL，暴露可复用的命令 token（CVSS 7.6/8.6）。 | 无 |

**分析**：虽然关键资源泄漏类 Bug 已通过新合并的 PR 修复，但**会话状态管理的根本问题**（如 `#63216`、`#66443`）依然严峻。回归问题 `#62505` 也表明，新功能的引入有时会破坏核心工作流，需要加强测试。

## 6. 功能请求与路线图信号
下列功能需求在社区中获得高关注度，结合已有 PR，暗示了下一阶段的开发方向。

-   **🎯 [Feature #63829]：按 Agent 隔离内存维基配置**
    -   获 9 个 👍，是社区呼声最高的需求。支持多 Agent 独立知识库，是项目向多租户、专业化 Agent 平台演进的关键一步。目前无关联 PR，但属于高优级的合理需求。

-   **🎯 [Feature #42840]：Control UI 支持 MathJax/LaTeX**
    -   获 7 个 👍。这是对产品细节的完善，显示用户将 OpenClaw 作为**专业生产力工具**来使用的场景，处理数学和科学内容的需求明确。

-   **⚠️ [Feature #54794]：Telegram Inline Query 支持**
    -   获 2 个 👍。需求明确：让用户在任何聊天中以 `@botname` 方式调用机器人。已有数个与 Telegram 及频道相关的 `fix` PR（`#97247`, `#95973`），表明该渠道是维护重点，此功能的优先级较高。

-   **🔮 [PR #95969]：托管市场目录源**
    -   该 PR 已获得维护者关注，是构建 ClawHub 生态的关键基础设置。结合热点 Issue `#50090`，**开放 `ClawHub` 并提升开发者体验**是项目当前的战略重点。

**顾问观点**：项目应优先考虑 `#63829`（多 Agent 内存隔离）和推进 ClawHub 工作（`#95969`）。它们分别解决了多 Agent 场景下的数据和权限混乱问题，以及项目长期发展的生态问题。

## 7. 用户反馈摘要
-   **对复杂 Bug 的细致描述**：用户如 `CarlCapital`（`#92201`）、`richwilson-bloom`（`#95833`、`#95915`）提供的报告包含详细的堆栈跟踪、环境信息和复现步骤，展现用户社区的技术成熟度，对开发者快速定位问题极具价值。
-   **对“承诺不兑现”的沮丧**：`#58450` 和 `#50165`（子代理未完成就显示完成）引发了最广泛的共鸣。用户普遍反馈 Agent 的行为不可预测，“看起来完成了，但实际上没有”。这动摇了用户对 AI 最基本的信任。
-   **对“回归”的强烈抱怨**：`#62505` 和 `#44502` 的评论区充分表达了用户对代码更新引入新 Bug 破坏旧有工作流的愤怒。用户期待更稳定的核心体验。
-   **对生态系统的期望**：`#50090` 的讨论不仅限于问题本身，还深入探讨了 `ClawHub` 的架构和技术难点，用户希望项目能够提供一个繁荣、标准的插件市场，而非仅仅是“能用”。

## 8. 待处理积压
以下 Issue 和 PR 长期未获得有效响应，可能对用户信心和项目健康度造成影响。

-   **🔴 Issue `#35203`**：多 Agent 协作增强 RFC（能力画像、共享黑板等）。
    -   **状态**：自 2026-03-05 起开放，社区已在其中展开了深度技术讨论，但维护者未给出官方方向性回复。这是一个庞大的架构提案，需要一个明确的“接受/拒绝/搁置”决定。
-   **🔴 Issue `#54463`**：QMD 内存索引递归进入符号链接循环导致 `ENAMETOOLONG` 错误。
    -   **状态**：自 2026-03-25 起开放，是一个明确的、可复现的文件系统 Bug。虽然严重性不高，但长期不响应会损害项目在健壮性方面的声誉。
-   **🔴 PR `#58482`**：为内存宿主批量轮询添加 AbortSignal 支持。
    -   **状态**：自 2026-03-31 起开放。这个 PR 改动小，价值明确（提升后端资源和 API 利用效率），却长期积压。合并此类小型、安全的改进能有效激励外部贡献者。
-   **🔴 PR `#59414`**：为 `openclaw doctor` 命令添加 Node.js 运行时信息。
    -   **状态**：自 2026-04-02 起开放。同为“小而美”的 PR，对于用户自诊断和环境兼容性至关重要。

**分析师建议**：项目维护者应尽快对 `#35203` 这类方向性 RFC 给出官方回复，并优先合并 `#58482` 和 `#59414` 这类低风险、高价值的 PR，以改善社区贡献体验，减轻积压压力。

---

## 横向生态对比

好的，作为您的资深技术分析师，以下是根据您提供的各项目2026-06-28动态数据生成的横向对比分析报告。

---

### **个人 AI 智能体开源生态横向对比分析报告 (2026-06-28)**

**报告日期:** 2026-06-28
**分析师:** AI 开源生态分析师

---

### 1. 生态全景

今日，个人 AI 智能体/自主智能体开源生态呈现出 **“巨头稳进、新兴突围、细分深耕”** 的格局。以 OpenClaw、Hermes Agent 为代表的头部项目继续在**多代理协作**和**企业级安全（凭证/支付）** 方向投入重兵，展现出成熟项目的领导力。以 ZeroClaw、IronClaw 为首的新兴力量则在**架构创新（Wasm/Goal Mode/精细权限）** 上大胆迈进，通过发布重量级 RFC 和核心功能 PR 争夺开发者心智。与此同时，NanoBot、LobsterAI 等项目则深耕**稳定性和用户交互体验**，通过集中清理 Bug 和优化细节来巩固用户基本盘。整体来看，生态已从功能“大跃进”阶段，进入 **“稳定与安全并重，架构革新与体验打磨并行”** 的深水区。

### 2. 各项目活跃度对比

下表汇总了各项目在2026-06-28过去24小时内的核心活动数据。

| 项目 | 活跃度评估 | 新增 Issue (总量/高优) | 新增 PR (总量/待合并) | 合并/关闭 PR | 版本发布 | 健康度评估 | 关键主题 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **极高** | 487 活跃 | 451 待合并 | 49 | 无 | 🟡 高热度，维护压力大 | 稳定性、托管市场、会话一致性 |
| **Hermes Agent** | **极高** | 36 活跃 | 大量待合并 | 20 | 无 | 🟢 高产出，快迭代 | 凭证安全、网关稳定性、支付规避 |
| **ZeroClaw** | **极高** | 41 | 50 (47待合并) | 3 | 无 | 🟢 高创新，架构演进 | Wasm/Goal Mode RFC、MCP支持、SOP |
| **IronClaw** | **高** | 5+ | 28 待合并 | 22 | 无 | 🟢 聚焦交付，里程碑推进 | 能力策略 (Capability Policy) 主线完成 |
| **NanoBot** | **高** | 7 关闭 | 17 待合并 | 29 | 无 | 🟢 高产出，快迭代 | Bug集群修复、安全性、WebUI稳定性 |
| **CoPaw** | **高** | 5 | 15+ | 1 | 无 | 🟢 测试驱动，质量提升 | 测试覆盖率、DeepSeek兼容性、对话持久化 |
| **LobsterAI** | **中等偏高** | 2 (高严重度) | 9 (7关闭) | 7 | 无 | 🟡 清理积压，Bug响应待提升 | 稳定性修复、MCP协议、UI/UX优化 |
| **PicoClaw** | **中等** | 3 | 4 (3待合并) | 1 | 无 | 🟢 清理旧债，新协议探索 | Agent协作总线、Windows兼容性、Simplex协议 |
| **NanoClaw** | **中等偏上** | 1 (高严重度) | 8 (全部待合并) | 0 | 无 | 🟡 攻坚阶段，PR积压严重 | 技能更新机制、Signal健壮性、模型配置 |
| **Moltis** | **低** | 1 | 2 | 0 | 无 | 🟢 稳健演进 | 本地模型兼容性、Apple容器限制 |
| **NullClaw** | **低** | 1 | 1 | 0 | 无 | 🟡 缓慢前行 | 结构化审批流、Android构建失败 |
| **TinyClaw** | **无活动** | 0 | 0 | 0 | 无 | ⚪ 休眠 | - |
| **ZeptoClaw** | **无活动** | 0 | 0 | 0 | 无 | ⚪ 休眠 | - |

*注：健康度评估基于PR合并率、关键Bug响应速度及社区反馈。*

### 3. OpenClaw 在生态中的定位

- **绝对的市场参照物与核心生态：** OpenClaw 依旧是生态中**社区规模最大、Issue/PR 数量最多的项目**（今日活跃 Issue 达 487 条），是其他项目比较和参照的核心基准。其庞大的用户基数和“ClawHub”市场概念的提出，使其成为生态中最具网络效应的项目。
- **优势：** 成熟的**托管市场/插件生态（ClawHub）** 概念和社区呼声，以及庞大的“社交工程”Bug（如 Agents 承诺不兑现）等问题暴露的深度，反映了其用户场景的多样性和复杂性，是其他项目难以匹敌的。
- **劣势与挑战：** 今日数据显示其 **PR 积压（451条）和 Issue 关闭率（13/500）极低**，维护压力巨大。这与其核心竞争对手 Hermes Agent（高合并率）形成鲜明对比，可能会导致核心贡献者流向响应更快的项目。
- **技术路线差异：** 与 ZeroClaw 的激进架构革新（Wasm/Goal Mode）不同，OpenClaw 更侧重于**实践中的稳定性修补**（死锁、内存泄漏）和**生态基础设施的搭建**（托管市场目录），走的是“生态先行”的路径。

### 4. 共同关注的技术方向

今日，多个不约而同出现的主题和诉求，构成了生态发展的核心风向标：

1.  **安全与信任** - **几乎所有活跃项目**
    - **具体诉求**：避免 Agent“偷跑”付费模型（Hermes #24029）、凭证安全与权限分级（Hermes, IronClaw）、沙箱执行路径安全（NanoBot）、供应链签名（ZeroClaw #8177）。
    - **涉及项目**：OpenClaw, Hermes Agent, NanoBot, ZeroClaw, IronClaw, PicoClaw。

2.  **多模态与 MCP 扩展** - **广泛涉及**
    - **具体诉求**：MCP 工具支持图像等附件（NanoBot #4542）、MCP 资源/提示支持（ZeroClaw #4467）、MCP 访问策略 UI（IronClaw, LobsterAI #1001）。
    - **涉及项目**：NanoBot, ZeroClaw, IronClaw, LobsterAI, CoPaw。

3.  **会话状态与持久化** - **重度用户痛点**
    - **具体诉求**：对话记录在异常中断后丢失（CoPaw #5579）、断点保存机制（CoPaw）、数据备份导致进程卡死（LobsterAI #2214）。
    - **涉及项目**：OpenClaw, CoPaw, LobsterAI。

4.  **Agent 行为可预测性与可控性** - **信任危机**
    - **具体诉求**：Agent“承诺不兑现”（OpenClaw #58450）/静默失败（NanoClaw #2868）、Agent 行为需要结构化审计（Hermes #26742）、明确的工具执行审批流（NullClaw #969）。
    - **涉及项目**：OpenClaw, NanoClaw, Hermes Agent, NullClaw。

### 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用个人 AI 助手平台 | 极客、开发者、希望通过“市场”获取扩展能力的普通用户 | 中央市场（ClawHub）、社区驱动的插件生态、强调会话管理 |
| **Hermes Agent** | 企业级/重度用户 Agent 框架 | 需要高安全、高稳定性和自动化工作流的开发者、团队 | 聚焦凭证/支付安全、网关健壮性、多进程并发支持、细粒度辅助任务控制 |
| **ZeroClaw** | 下一代安全/自主 Agent 运行时 | 前沿开发者、安全研究者、对架构有极致要求的创新者 | Wasm 插件运行时、Goal Mode（有状态任务模式）、“Wire-Protocol-First”提供商模型、供应链签名 |
| **IronClaw** | 精细化管理的多用户 Agent 平台 | 团队协作、企业管理员 | “Reborn” 能力策略（精细权限管控）、基于角色的访问控制、多租户 |
| **NanoBot** | 轻量级、快速迭代的 Agent 开发框架 | 个人开发者、Agent 应用原型快速构建者 | 强调低耦合、高交付效率（今日合并29个PR）、安全沙箱修正（exec工具） |
| **CoPaw** | 开发者友好、质量稳定的 Agent 平台 | 追求稳定性的开发者、企业用户 | 强调测试覆盖率、专注于平台兼容性（DeepSeek/自建模型）、对话持久化 |
| **LobsterAI** | 中文友好的桌面端 Agent 软件 | 中文用户、桌面重度用户 | 关注桌面端用户体验（Tauri）、国际化（中文）、MCP 协议支持 |
| **PicoClaw** | 嵌入式/轻量化 Agent 系统 | 边缘设备、IoT 开发者 | 专注于轻量级架构、跨协议支持（Matrix/Simplex）、Agent 间协作总线 |
| **NanoClaw** | 技能/插件分发与更新系统 | 专注于开发与分发 Agent 技能的开发者 | 核心痛点在于技能机制的可靠性（/update-skills）、模型驱动的团队配置 |

### 6. 社区热度与成熟度

- **快速迭代/高创新期 (活跃度高，关注新功能)**
    - **ZeroClaw**: 通过激进发布 RFC（Wasm, Goal Mode）吸引顶尖开发者，虽然代码合并量今日较低，但其社区正在“规划未来”，典型“架构驱动”阶段。
    - **Hermes Agent**: 虽然核心功能稳定，但通过高强度的 Bug 修复（特别是安全与支付类）来建立信任，处于 **“质量巩固驱动力”** 阶段。
    - **NanoBot**: 如同“疾速狂奔”，通过大量合并 PR 修复 Bug，处于 **“快节奏修复/交付”** 阶段。

- **质量巩固/稳健发展期 (重点提升稳定性与成熟度)**
    - **OpenClaw**: 庞大社区带来巨大维护压力，但也在死磕稳定性与市场生态，处于 **“生态与稳定性双轮驱动”** 阶段，但面临响应速度挑战。
    - **IronClaw**: 核心功能（能力策略）代码已合并，正在构建测试框架，处于 **“核心特性完成后打磨”** 阶段。
    - **CoPaw**: 通过大规模添加测试来巩固代码质量，典型的 **“质量驱动”** 阶段。
    - **LobsterAI**: 清理历史 PR，修复 UI/UX 及稳定性 Bug，处于 **“清理技术债务”** 阶段。

- **探索/缓行期 (聚焦狭窄问题或活动低迷)**
    - **PicoClaw / Moltis / NullClaw**: 社区贡献者聚焦在非常具体的问题上（Simplex 协议、本地模型兼容性），整体活跃度不高，属于 **“专注细分领域”** 阶段。

### 7. 值得关注的趋势信号

从今日的社区反馈中，可以提炼出以下对 AI 智能体开发者极具参考价值的趋势：

- **“成本透明度”成为 Agent 信任的基石：** 用户对 Agent 在后台“偷跑”付费 API 的错误反馈（如 Hermes #24029）表现出的愤怒，预示着未来 Agent 框架必须具备**清晰的费用来源追踪和透明的成本管控 UI**。单靠配置文件“免费”标志已不足以赢得信任，必须从架构层面保证执行者的路径与用户的预期（预算/提供商）一致。

- **“声明式”行为定义兴起：** 从 ZeroClaw 的 `Goal Mode` 到 Hermes 讨论的 `Managed Agent Contracts`，再到 NullClaw 的 `结构化审批流`，行业正从“写死指令”向“声明目标让 Agent 自主执行，但通过契约（Contract）/策略（Policy）设定严格边界”演进。对开发者而言，理解并设计好这类**“声明式”行为规则**将成为核心能力。

- **MCP (模型上下文协议) 仍是“兵家必争之地”，但深度进入“原生支持”阶段：** 多个项目都在积极将 MCP 的“资源”和“提示”部分（而不仅仅是“工具”）作为一等公民集成。这意味着未来的 Agent 将能更无缝地连接外部数据库、知识库和 API 文档，而不仅仅是执行简单动作。开发者应开始围绕 MCP 构建自己的工具和知识资源。

- **“异常持久化”是 Agent 走向生产环境的最后一块拼图：** Agent 崩溃后会话丢失是用户最担忧的数据安全问题（CoPaw #5579, LobsterAI #2214）。如何优雅地处理 Agent 异常（包括自身重启），实现**断点续传级别的数据持久化**，是智能体从“聊天玩具”变为“认真助手”的关键技术门槛。

**最终建议：**
对于 **技术决策者**，应重点关注 **ZeroClaw** 的架构演进（Wasm 与 Goal Mode）以洞察未来方向，同时参考 **Hermes Agent** 对安全和支付的严格把控标准。
对于 **日常开发者**，**NanoBot** 的快速迭代和 **OpenClaw** 的庞大社区是很好的学习和贡献起点，而 **CoPaw** 和 **LobsterAI** 稳定的代码库更适合作为构建生产级应用的参考基线。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据NanoBot项目2026年6月28日的GitHub数据生成的日报。

---

# NanoBot 项目动态日报 | 2026-06-28

## 1. 今日速览

项目今日活跃度**极高**，展现出强大的交付能力。过去24小时内合并/关闭了29个PR和7个Issues，社区贡献者（如`axelray-dev`）集中解决了一批历史遗留的Bug（特别是#4057、#4060、#4063等），体现了项目在稳定性和健壮性上的显著投入。同时，仍有17个待合并的PR和数个关于新功能（如MCP图像、定时任务静默模式）的讨论，表明功能开发与技术债务清理并行推进。整体而言，项目处于**高产出、快迭代**的健康状态。

## 2. 版本发布

**无**。过去24小时内无新版本发布。

## 3. 项目进展

今日，社区维护者成功关闭/合并了多项关键的PR，使项目在**稳定性**和**安全性**方面取得了重要进展。

- **修复关键Bug集群**：贡献者 `axelray-dev` 一次性修复了由 `hamb1y` 报告的一系列严重Bug，包括：
    - [#4533](https://github.com/HKUDS/nanobot/pull/4533): 修复了会话密钥因文件名消毒导致的磁盘冲突（[#4057](https://github.com/HKUDS/nanobot/issues/4057)）。
    - [#4532](https://github.com/HKUDS/nanobot/pull/4532): 修复了Anthropic provider因缺少`type`字段导致内容块被拒绝的Bug（[#4060](https://github.com/HKUDS/nanobot/issues/4060)）。
    - [#4531](https://github.com/HKUDS/nanobot/pull/4531): 修复了流式Delta消息因未包含`_stream_id`导致不同流被合并的Bug（[#4063](https://github.com/HKUDS/nanobot/issues/4063)）。
    - [#4530](https://github.com/HKUDS/nanobot/pull/4530): 修复了非流式解析器保留了重复的tool call ID的Bug（[#4059](https://github.com/HKUDS/nanobot/issues/4059)）。
- **修复安全漏洞**：安全研究员`YLChen-007`报告的两个安全问题均已得到修复：
    - [#4521](https://github.com/HKUDS/nanobot/issues/4521)（`exec.allowPatterns`绕过）与[#4518](https://github.com/HKUDS/nanobot/issues/4518)（登录shell泄露密钥）对应的修复PR[#4562](https://github.com/HKUDS/nanobot/pull/4562)和[#4562](https://github.com/HKUDS/nanobot/pull/4562)（注：两个issues由同一PR解决）已提交，社区表现出对安全问题的重视。
- **完善定时功能**：`franciscomaestre` 贡献的“定时任务静默模式”功能（[#4225](https://github.com/HKUDS/nanobot/pull/4225) 和 [#4357](https://github.com/HKUDS/nanobot/pull/4357)）被合并，为后台监控等场景提供了更灵活的交付方式。
- **提升测试可靠性**：`primit1v0` 修复了一个因文件系统时间戳精度问题导致的随机测试失败（[#4523](https://github.com/HKUDS/nanobot/pull/4523)），提升了CI/CD的稳定性。

## 4. 社区热点

- **Issue #660**: “`ultra-lightweight`名不副实，包含了臃肿的Node.js依赖”。这是今日**最受关注**的讨论（👍: 5, 评论: 14），尽管是历史Issue。这反映了社区对项目“轻量级”定位的严格要求，以及对技术栈选择的敏感度。链接: [Issue #660](https://github.com/HKUDS/nanobot/issues/660)
- **PR #4565**: “fix(webui): 清除重连后的卡死流并提升停止按钮可靠性”。这是对当前最活跃Bug[#4500](https://github.com/HKUDS/nanobot/issues/4500)的直接回应，展示了社区对WebUI用户体验问题的高度关注和快速响应。链接: [PR #4565](https://github.com/HKUDS/nanobot/pull/4565)
- **PR #4542**: “feat(mcp): 将MCP工具中的图像内容作为工件交付”。这是一个技术性较强的功能增强，触及了MCP（模型上下文协议）的多模态内容处理能力，吸引了关注代理工具扩展的开发者。链接: [PR #4542](https://github.com/HKUDS/nanobot/pull/4542)

## 5. Bug 与稳定性

今日报告的Bug主要集中在两个方面：**WebUI体验**和**安全性**。

- **[严重] WebUI卡死**：`zpljd258` 在[#4500](https://github.com/HKUDS/nanobot/issues/4500)报告中详细描述了WebUI在网关重启后陷入“处理中”状态且“停止”按钮失效的问题。该Bug直接影响用户体验，已有修复PR [#4565](https://github.com/HKUDS/nanobot/pull/4565) 提交。
- **[严重] 安全漏洞**：`YLChen-007` 报告了两项安全性问题：
    1.  `exec.allowPatterns` 可被shell链（如`&&`）绕过执行非预期命令（[#4521](https://github.com/HKUDS/nanobot/issues/4521)）。
    2.  `exec`工具的默认登录shell执行方式可能从shell启动文件中泄露敏感信息（[#4518](https://github.com/HKUDS/nanobot/issues/4518)）。
    这两个问题均有修复PR [#4562](https://github.com/HKUDS/nanobot/pull/4562) 提交，严重度极高，建议用户关注更新。同时，`exec`工具的功能安全性成为关注焦点。
- **[需要关注] 其他已修复Bug**：今日集中修复了一批由`hamb1y`报告的系统性Bug（会话ID冲突、流合并异常等），这些Bug在特定、复杂的场景下会引发数据错误或服务异常。

## 6. 功能请求与路线图信号

- **MCP图像支持**：`codedragoncom` 的PR [#4542](https://github.com/HKUDS/nanobot/pull/4542) 旨在将MCP工具的`ImageContent`内容作为附件而非base64字符串进行交付，这是一个潜在的**下一版本重要更新**，将显著提升MCP工具处理多模态数据的能力。
- **Agent可靠性增强**：`Re-bin` 的PR [#4534](https://github.com/HKUDS/nanobot/pull/4534) 为agent循环添加了验证门和provider恢复机制，旨在解决因provider瞬时错误导致的agent任务失败问题。这体现了项目向生产级稳定性迈进的信号。
- **会话级模型预设**：`dajiaohuang` 的PR [#4555](https://github.com/HKUDS/nanobot/pull/4555) 允许为每个对话单独设置模型，解决了用户对不同会话使用不同大模型的核心诉求。
- **Web搜索新提供商**：`franciscomaestre` 的PR [#4406](https://github.com/HKUDS/nanobot/pull/4406) 计划集成Serper.dev作为新的搜索后端，显示了项目在扩展基础工具生态持续努力。
- **询问澄清工具**：`ZhouJ-sh` 的PR [#4527](https://github.com/HKUDS/nanobot/pull/4527) 提议添加一个内置的工具，让Agent在不确定用户意图时可以主动提问澄清，这将改善Agent与用户的交互体验。

## 7. 用户反馈摘要

- **对“轻量级”定义的争议**：用户在[#660](https://github.com/HKUDS/nanobot/issues/660)中指出，Node.js依赖的存在与项目宣称的“超轻量”矛盾。虽然较老的Issue，但其14条评论和5个赞反映出用户对项目设计理念的期许与现实之间的落差，是项目在对外宣传时需要注意的信号。
- **WebUI稳定性是核心痛点**：用户`zpljd258` 在[#4500](https://github.com/HKUDS/nanobot/issues/4500)中非常清晰地描述了WebUI在重连后卡死的问题，并附有详细的重现步骤，表明WebUI的可靠性和响应性是目前影响用户满意度的关键瓶颈。
- **对安全性的担忧**：用户`YLChen-007` 详细报告了`exec`工具的相关安全漏洞，这侧面反映了在功能强大的Agent框架中，工具执行的安全性始终是高级用户和开发者最关心的问题之一。

## 8. 待处理积压

- **[重要] WebUI卡死修复**：PR [#4565](https://github.com/HKUDS/nanobot/pull/4565) 是对应高优Bug [#4500](https://github.com/HKUDS/nanobot/issues/4500) 的修复方案，目前为“待合并”状态。作为影响核心用户体验的问题，建议项目维护者优先审核和合并此PR。
- **[重要] exec工具安全修复**：PR [#4562](https://github.com/HKUDS/nanobot/pull/4562) 同时修复了 [#4521](https://github.com/HKUDS/nanobot/issues/4521) 和 [#4518](https://github.com/HKUDS/nanobot/issues/4518) 两个安全问题。鉴于安全漏洞的敏感性，此PR应获得最高优先级处理。
- **[长期] 轻量级争议**：Issue [#660](https://github.com/HKUDS/nanobot/issues/660) 提出的关于Node.js依赖的问题。虽然讨论热度高，但解决难度大（涉及技术选型）。维护者或许可以考虑在文档中更细致地解释依赖的必要性，或公开讨论未来可能的瘦身计划。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我为您呈上基于 Hermes Agent 项目数据生成的 2026-06-28 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-28

## 1. 今日速览

今日项目活跃度**极高**，共处理 Issue 和 PR 合计100条，其中新开/活跃 Issue 36条，合并/关闭 PR 20条。核心贡献者 @teknium1 今日进行了大规模 Bug 修复和稳定性提升工作，共提交/合并了十余个关键 PR，系统性地解决了凭证安全、网关挂起、支付规避等多个 P1/P2 级别的严重问题。社区反馈集中在 Windows 端桌面应用编译失败、凭证管理、以及辅助任务支付规避等痛点。尽管今日没有新版本发布，但项目在稳定性和安全性方面取得了显著进展。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日项目在稳定性和安全性方面推进关键，主要进展如下：

- **凭证系统安全性加固**：
    - **修复并发写入丢失问题**：合并 PR [#53896](https://github.com/NousResearch/hermes-agent/pull/53896)，解决了当多个 Hermes 进程同时进行凭证轮换时，新添加的凭证可能被覆盖丢失的严重 Bug。
    - **修复 Anthropic 多源凭证冲突**：新增 PR [#53899](https://github.com/NousResearch/hermes-agent/pull/53899)，旨在解决 macOS Keychain 与文件凭证不一致时导致的认证失败问题，目前处于待合并状态。
    - **修复 OpenRouter 凭证池耗尽**：新增 PR [#53906](https://github.com/NousResearch/hermes-agent/pull/53906)，确保当凭证池用尽时，辅助任务能正确回退到环境变量 `OPENROUTER_API_KEY`。
    - **修复出站聊天路径泄露**：新增 PR [#53907](https://github.com/NousResearch/hermes-agent/pull/53907)，修复了出站聊天响应中未正确遮盖完整凭证集（如 GitHub PAT、Telegram Token）的安全漏洞。

- **网关稳定性显著提升**：
    - **彻底修复重启挂起/死亡螺旋**：通过合并多个 PR（[#53897](https://github.com/NousResearch/hermes-agent/pull/53897)、[#36913](https://github.com/NousResearch/hermes-agent/pull/36913)、[#19946](https://github.com/NousResearch/hermes-agent/pull/19946)、[#14130](https://github.com/NousResearch/hermes-agent/pull/14130)），为网关关闭过程中的适配器断开操作增加了超时机制，防止网络问题导致进程挂起，解决了长期存在的 `PID file race` 问题。

- **镜像路由与消息队列解锁**：
    - **修复 OpenRouter 镜像404导致队列锁定**：合并 PR [#53901](https://github.com/NousResearch/hermes-agent/pull/53901)，解决了向非视觉模型发送图片时，由于 OpenRouter 返回404而导致的网关消息队列永久锁定问题。现在会正确回退为纯文本重试。

- **辅助任务回退机制完善**：
    - **修复认证错误导致任务静默失败**：合并 PR [#53900](https://github.com/NousResearch/hermes-agent/pull/53900)，确保辅助任务（如压缩）在遭遇401认证错误时能正确触发回退链，而非静默失败。

- **其他修复**：
    - **TUI 无响应问题**：合并 PR [#53895](https://github.com/NousResearch/hermes-agent/pull/53895)，修复了在 TUI 中执行路径补全（输入 `@`）时导致界面冻结的问题。
    - **TUI 空补全RPC**：合并 PR [#21142](https://github.com/NousResearch/hermes-agent/pull/21142)，修复了在 TUI 中单纯输入 `@` 而不跟任何字符时，会发起无效的 RPC 请求的问题。
    - **MCP HTTP 头部解析**：新增 PR [#53916](https://github.com/NousResearch/hermes-agent/pull/53916)，修复了 `config.yaml` 中 `headers` 配置为 JSON 字符串时导致 MCP 服务器启动崩溃的问题。
    - **Windows 浏览器工具URL截断**：新增 PR [#53914](https://github.com/NousResearch/hermes-agent/pull/53914)，修复了 Windows 上浏览器工具因 .cmd 存根处理 `&` 字符不当而导致 URL 被截断的问题。

## 4. 社区热点

今日社区讨论的焦点集中在以下几个 Issue，反映了用户对**稳定性、安全性和支付透明性**的核心诉求：

- **[Bug]: Windows desktop app fails to compile during hermes update / hermes desktop (#40187)** [评论: 14，👍: 1]
    [链接](https://github.com/NousResearch/hermes-agent/issues/40187)
    **诉求分析**：这是今日最热门的 Issue。问题描述在 Windows 上运行 `hermes update` 或 `hermes desktop` 时，编译 Electron 应用失败。这是典型的用户体验阻塞问题，高评论数表明这是一个影响广泛且急需解决的痛点。

- **[Bug]: OpenAI-Codex credential pool can drop newly added credential after stale auth.json rewrite during rotation (#19566)** [评论: 9，👍: 1]
    [链接](https://github.com/NousResearch/hermes-agent/issues/19566)
    **诉求分析**：此 Issue 讨论的是凭证管理的并发安全性问题。用户报告新添加的凭证会在轮换过程中丢失，这对于依赖自动化和长期运行脚本的用户是灾难性的。好在今日已有 PR [#53896](https://github.com/NousResearch/hermes-agent/pull/53896) 成功将其修复并合并。

- **[Bug]: Auxiliary tasks silently fall back to paid OpenRouter models, bypassing user's free-only configuration (#24029)** [评论: 5，👍: 3]
    [链接](https://github.com/NousResearch/hermes-agent/issues/24029)
    **诉求分析**：虽然评论数不是最高，但 **3个赞** 表明此问题获得了很高的共鸣。用户明确配置使用免费模型，但辅助任务却静默使用付费模型，导致产生意外账单。这触及了用户对**费用透明度和控制权**的核心关切。

## 5. Bug 与稳定性

以下为今日报告的、按严重程度排列的关键 Bug 和稳定性问题：

- **崩溃/挂起**：
    - _[CLOSED]_ Windows桌面应用编译失败 (#40187)，严重性高，影响新用户上手。_当前无直接 Fix PR。_
    - _[OPEN]_ Hermes Desktop v40.9.3 在 Windows 11 上启动时崩溃 (#38216)，严重性高。_当前无 Fix PR。_
    - _[CLOSED]_ 网关 `launchd` 双进程导致重启死亡螺旋 (#21549)。_已修复。_
    - _[CLOSED]_ 网关关闭时挂起，导致 PID 文件冲突 (#14128, #21549)。_今日通过合并多个 PR 彻底修复。_

- **数据/安全**：
    - _[CLOSED]_ `hermes debug share` 泄露私人数据 (#22016)。_已修复。_
    - _[OPEN]_ 凭证池并发写入丢失 (#19566)。_今日已通过 PR #53896 修复。_
    - _[OPEN]_ 辅助任务静默回退到付费模型 (#24029)。_该问题似乎与 OpenRouter 相关，今日有多个针对 OpenRouter 辅助任务的 PR (#53906, #53900, #53901) 被提出，可能已触及该问题的修复。_

- **功能异常**：
    - _[CLOSED]_ CLI `/stop` 命令无法中断智能体 (#22176)。_已修复。_
    - _[CLOSED]_ 配置文件更新后自定义模型消失 (#25272)。_已修复。_
    - _[CLOSED]_ `hermes -z` 单次调用输出为空 (#22975)。_已修复。_
    - _[CLOSED]_ 交互式聊天报告“未配置推理提供者” (#24433)。_已修复。_
    - _[CLOSED]_ Telegram 任务完成但不发送最终消息 (#21611)。_已修复。_
    - _[CLOSED]_ Gemini 3 Flash 辅助模型**需要点击** (#多个)。_今日有多个 PR 针对 OpenRouter 辅助任务回退链进行修复。_
    - _[OPEN]_ `vision_analyze` 工具在 Docker 后端下无法发送图片 (#32709)。_当前无 Fix PR。_
    - _[OPEN]_ 模型切换导致 HTTP 400 错误 (#48338)。_当前无 Fix PR。_
    - _[OPEN]_ Discord 语音输入在 Linux 上崩溃 (#53874)。_这是一个今日新开的 Bug。_
    - _[OPEN]_ `hermes skills update` 不刷新 `content_hash` (#41176)。_当前无 Fix PR。_

## 6. 功能请求与路线图信号

今日用户提出的功能需求反映了社区的长期愿景，主要集中在**智能体管理与审计**方面：

- **Managed Agent Runtime contracts (#26675)** [P3]
    [链接](https://github.com/NousResearch/hermes-agent/issues/26675)
    用户提出利用现有的 Profile、Skills、Kanban 等能力，建立“托管智能体运行时契约”，以实现严肃的多智能体工作流。这表明社区期望 Hermes 从“单智能体助手”向“多智能体编排平台”演进。

- **Claim Verification & Audit Mechanism (#26742)** [P3]
    [链接](https://github.com/NousResearch/hermes-agent/issues/26742)
    用户请求为智能体的行为（Claims）提供结构化的验证和审计机制。这是一个高级功能，显示出用户对生产环境部署和 AI 安全性的深层需求。

- **Desktop 应将会话压缩视为同一个逻辑聊天 (#50192)** [P3]
    [链接](https://github.com/NousResearch/hermes-agent/issues/50192)
    这是一个提升桌面端用户体验的实用建议，旨在优化长会话的用户心智模型。

- **支持 Amazon Bedrock 的 `service_tier` (#31322)** [P3]
    [链接](https://github.com/NousResearch/hermes-agent/issues/31322)
    用户希望支持 `service_tier=flex` 以降低 API 成本。这表明在成本和性能之间进行灵活选择是企业级用户的强烈需求。

**路线图信号**：从今日活跃的 PR 和 Issue 来看，项目短期内重点仍是**稳定性和安全性**，尤其是凭证管理、网关健壮性、以及支付规避问题。长期来看，用户对更高级的智能体管理和审计功能抱有期待。

## 7. 用户反馈摘要

从今日的 Issue 和 PR 评论中，提取到以下用户痛点和使用场景：

- **“请停止偷跑我的账单！”**：关于辅助任务静默回退到付费模型 (#24029) 的讨论中，用户表达了强烈的被欺骗感。用户明确配置了免费模型，却产生了 OpenAI/OpenRouter 账单，这严重打击了用户的信任和对服务的控制感。
- **“更新是场噩梦！”**：Windows 桌面应用编译失败 (#40187)、更新后配置文件丢失 (#25272) 等问题反复出现，表明升级流程的健壮性是主要用户抱怨点。用户在 Issue #38618 中进一步抱怨更新检测和版本号混乱的问题。
- **“我不知道怎么停下来！”**：CLI 中断功能失效 (#22176) 导致智能体失控运行，用户对此感到无助。这表明清晰、可靠的用户控制权是核心交互体验的一部分。
- **“为什么我的配置总是失效？”**：配置验证不完整 (#50105) 导致用户配置的模型被静默忽略，转而使用其他提供商和模型，导致意外计费。用户希望在配置文件有误时得到明确的错误提示，而非被忽略。
- **“我希望我的技能系统更可靠”**：用户创建的技能缺乏正确性和执行一致性的保证 (#25833)。这表明高级用户正在将 Hermes 作为开发平台，并希望获得编程语言级别的确定性。

## 8. 待处理积压

以下为长期存在或对项目健康度影响显著，但仍未得到充分响应的关键 Issue，提醒维护者关注：

- **#50703 [P2]** - “NVIDIA NIM 的 `chat_template_kwargs` 丢失”。一个较为冷门但深入的问题，影响特定用户群体的高级功能。_今日已更新，但无直接修复。_
- **#43042 [P3]** - “桌面文件浏览器间歇性 ENOENT”。一个影响桌面端用户体验的长期 Bug。_今日有更新，但无修复。_
- **#25833 [P3]** - “自创建技能缺乏正确性保障”。这是一个关乎长期产品路线图的基础设施问题。_已有一段时间未得到核心维护者回复。_
- **#26742 [P3]** - “智能体声明验证与审计机制”。这是一个重要的功能请求，但对于短期产品路线图来说优先级较低。_自创建后更新较少。_
- **#31322 [P3]** - “支持 Bedrock `service_tier`”。一个实用的功能请求，反映出与外部云服务集成时的灵活性需求。_自 5月24日创建后，更新不频繁。_

---
*报告结束。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw 项目数据生成的 2026-06-28 项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-06-28

### 1. 今日速览

过去24小时，PicoClaw 项目活跃度**中等**。社区贡献与维护工作并行推进，共处理了 3 个 Issue 和 4 个 PR。**两个长期未解决的问题（`list_dir` Windows 兼容性 Bug 和 Telegram 权限分级功能请求）在积压数月后终于被关闭**，表明维护者正在清理旧债。同时，两个新的 PR 提出了有趣的功能扩展（Simplex 协议支持）和代码质量改进（LINE 通道错误处理优化），显示出社区活力。核心团队在**跨渠道协议兼容性**和**构建系统 (MCP) 健壮性**方面的改进工作已告一段落。

### 2. 版本发布

无。

### 3. 项目进展

- **Agent间协作总线正式合并** (`#2937`)：经过一个多月的迭代，PR `Feat/agent collaboration` 已合并。这标志着 PicoClaw 拥有了首款内部 Agent 协作基础设施，支持持久化邮箱、协作线程和权限感知的消息传递。这是**项目架构层面的一次重大跃进**，为后续复杂的多 Agent 协同工作流奠定了基础。
- **MCP 命令解析健壮性修复** (`#3048`)：修复了 `mcp add` 子命令在处理根级标志（如 `--no-color`）时可能出现的参数解析错误问题。提升了开发者工具的易用性和稳定性。
- **通道协议扩展**：新的 `Added simplex channel type` PR (`#3193`) 已打开，正在等待审核。这表明项目正在积极探索除主流聊天平台外的新通信协议支持，可能用于 IoT 或专用网络场景。

### 4. 社区热点

- **【高热度】`list_dir` Windows Bug 关闭** (`#2472`)：一个影响 Windows 用户使用文件列表功能的 Bug，从 4 月 10 日至今，经历了 7 条评论和长时间积压后最终关闭。这反映了 **Windows 平台兼容性**是社区用户的核心痛点之一，尤其是在路径分隔符处理这类底层问题上。
- **【高热度】Telegram 权限分级控制功能请求关闭** (`#3114`)：另一个积压近半月的功能请求被关闭。该 Issue 提出了一个非常具体的安全场景：按私聊、群组、频道对机器人能力进行分级控制。**社区对“安全边界”的诉求非常清晰**，特别是担心将机器人加入群组后被滥用执行危险命令（如 `exec`、`write_file`）。

*   **链接**: [[#2472]](https://github.com/sipeed/picoclaw/issues/2472), [[#3114]](https://github.com/sipeed/picoclaw/issues/3114)

### 5. Bug 与稳定性

- **【低严重性】Matrix 加密消息未启用** (`#3194`)：一个关于 Matrix 通道的 Bug，当收到加密消息时，如果 PicoClaw 未配置加密功能，会打印错误日志。目前无评论和修复 PR。**严重程度较低**，因为它不会阻断服务，但会暴露功能和日志层面的不一致性，需确认是否需要默认静默处理或提示用户配置。
    *   **链接**: [[#3194]](https://github.com/sipeed/picoclaw/issues/3194)
- **【代码质量】LINE 通道错误处理优化** (`#3189`)：一个新的 PR 被提出，旨在明确忽略 LINE 通道中 `resp.Body.Close()` 的错误。虽然这不是一个功能性 Bug，但体现了社区对**代码健壮性和静态分析告警**的重视。
    *   **链接**: [[#3189]](https://github.com/sipeed/picoclaw/pull/3189)

### 6. 功能请求与路线图信号

- **Simplex 通道支持** (`#3193`)：这个未经合并的 PR 是最新的社区功能贡献。Simplex 是一个去中心化、隐私保护的通信协议。如果被合并，将极大扩展 PicoClaw 的应用场景，尤其是在**隐私敏感或离线优先**的通信领域。这可能是路线图上的一个潜在信号。
- **Telegram 权限分级** (`#3114`)：虽然此 Issue 已关闭，但并未关联任何 PR。该需求背后的安全考量十分合理，很可能会在未来以更全面的方式（可能作为通道权限系统的一部分）重新被提出。

### 7. 用户反馈摘要

- **Windows 用户痛点明确**：`list_dir` Bug 持续存在了 2.5 个月，直接导致 Windows 用户在文件操作功能上遇到硬错误，影响了核心体验。
- **安全需求意识强**：Telegram 权限分级的 Issue 清晰地描述了“谁可以用”和“在哪可以用”的区别，用户不仅关注功能接入，更关注不同场景下的安全控制。这表明用户群体的成熟度在提高。

### 8. 待处理积压

- **新待讨论**：
    - `#3194` [**Bug**] Matrix 加密消息日志：需要维护者确认是否属于预期行为或需修复。
- **潜在可关闭**：项目清理了 `#2472` 和 `#3114` 两个长时期 Issue，目前积压情况良好。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的NanoClaw项目数据，为您生成2026年6月28日的项目动态日报。

---

## NanoClaw 项目动态日报 2026-06-28

**分析师:** AI 开源项目分析师
**日期:** 2026-06-28

### 1. 今日速览

NanoClaw项目今日活跃度处于**中等偏上**水平，主要体现在**密集的PR提交**上，展现了社区在问题修复和功能增强方面的高效响应。过去24小时内，项目迎来了8个待合并的Pull Request，其中至少2个直接针对关键Bug和部署优化，同时还有一个新开的Issue明确指出了技能更新机制的核心缺陷。遗憾的是，尚未有PR或Release被合并/发布。项目目前处于一个“多问题被定位，多修复等待合并”的**攻坚阶段**，整体健康度良好，但要实现实质性进展，需要加快PR审阅和合并流程。

### 3. 项目进展

今日无任何Pull Requests被合并或关闭。尽管提交了8个PR，但项目核心进度并未向前推进。当前积压的8个待合并PR（#2871-#2875, #2822-#2824）构成了项目潜在的下一次版本升级包，涵盖了从核心Bug修复到新功能添加的多个方面。

### 4. 社区热点

*   **最具争议/关注的核心Bug修复:**
    *   **[PR #2873] fix(skills): split pre-flight from credentials so /update-skills can refresh code (#2868)** ([链接](https://github.com/nanocoai/nanoclaw/pull/2873))
        *   **分析:** 该PR直接响应了今日最关键的Issue #2868。Issue #2868揭示了`/update-skills`命令执行后，不会刷新已安装channel的代码或依赖，导致用户必须重新执行`/add-<channel>`才能获得更新，这是一个严重的**静默无操作**Bug。社区的强烈反馈（1条评论）和作者`glifocat`在发现后立即提出修复方案，使得该PR成为今日社区讨论的焦点。其背后的诉求是**确保技能更新流程的可靠性和可预测性**，消除用户信任风险。

### 5. Bug 与稳定性

**严重等级: 高**

*   **Issue #2868: `/update-skills` 静默无操作**
    *   **问题描述:** 对于已安装的channel，运行`/update-skills`命令不会刷新其适配器代码或固定依赖，而是静默跳过，导致`[Unreleased]`迁移日志中要求用户手动重新安装的说明完全失效。
    *   **已有修复:** 是，**PR #2873** 已提交，旨在将“预检查（pre-flight）”与“凭证（credentials）”分离，使`/update-skills`能够真正执行代码刷新。
    *   **链接:** [Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868)

**严重等级: 中**

*   **[PR #2874] fix(signal): survive signal-cli boot flaps instead of crash-looping** ([链接](https://github.com/nanocoai/nanoclaw/pull/2874))
    *   **问题描述:** 在进行Signal渠道集成时，当`signal-cli`服务启动不稳定或临时故障时，NanoClaw会进入崩溃-重启的循环，而不是优雅地等待或重试。
    *   **修复状态:** 等待合并。该修复旨在增强与外部服务连接的健壮性。

**严重等级: 低**

*   **[PR #2822] refactor(container-runner): drop dead /workspace/global mount** ([链接](https://github.com/nanocoai/nanoclaw/pull/2822))
*   **[PR #2823] fix: remove groups/global/CLAUDE.md (host deletes it on every startup)** ([链接](https://github.com/nanocoai/nanoclaw/pull/2823))
*   **[PR #2824] fix: drop stale "Global Memory" instruction from main seed prompt** ([链接](https://github.com/nanocoai/nanoclaw/pull/2824))
    *   这三份PR均来自作者`CutSnake01`，是在清理无用代码、修复因宿主机行为导致的配置丢失以及删除过时的提示指令。它们表明项目正在持续进行**代码质量和内部稳定性的维护**。这些PR已积压超过一周，建议尽快审阅合并。

### 6. 功能请求与路线图信号

*   **核心功能增强: 灵活的模型配置**
    *   **[PR #2872] feat(opencode): per-group model override via container_configs.model** ([链接](https://github.com/nanocoai/nanoclaw/pull/2872))
        *   **信号:** 该PR允许为每个OpenCode代理组配置不同的模型（通过`container_configs.model`），这标志着项目正在向**更灵活、更精细化的模型资源管理**方向演进。这可能是未来版本的一个重要特性，特别适合多模型混合使用的复杂场景。

*   **基础设施与可观测性**
    *   **[PR #2871] feat(dashboard): add dashboard pusher with OpenCode support** ([链接](https://github.com/nanocoai/nanoclaw/pull/2871))
        *   **信号:** 添加了一个仪表盘数据推送器，定期收集并发送系统状态快照到一个独立的`nanoclaw-dashboard`服务器。这预示项目正在构建官方的**可观测性基础设施**，对于大规模部署和运维至关重要。

### 7. 用户反馈摘要

*   **核心痛点:** 技能更新机制失效。Issue #2868 的创建者（`glifocat`）明确指出了项目维护文档中存在一个“空洞的承诺”——要求用户执行一个实际上并不生效的命令。这暴露了用户对**更新流程的可靠性存在不满**，并可能导致对项目功能信任度的下降。
*   **简单诉求:** 用户希望“更新”命令能够像其名称暗示的那样，成功地、可预期地完成工作，而不是成为一个需要手动重启的“一次性安装”流程。

### 8. 待处理积压

以下多个重要PR已提交超过一周且尚未被审阅或合并，可能成为项目发展的阻碍。

*   **[PR #2822] refactor(container-runner): drop dead /workspace/global mount** - 已积压 8 天
*   **[PR #2823] fix: remove groups/global/CLAUDE.md (host deletes it on every startup)** - 已积压 8 天
*   **[PR #2824] fix: drop stale "Global Memory" instruction from main seed prompt** - 已积压 8 天
*   **[警告] 核心Bug修复PR #2873 未获关注:** 尽管它直接解决了当务之急的#2868号Bug，且提交于今日，但尚未有核心维护者对其进行评论或approve，与#2872、#2874等PR处于同一等待状态。

**建议:** 项目维护者需要尽快审阅并合并这批PR，特别是修复核心Bug的#2873和提升稳定性的#2874，以稳定用户情绪并推动项目进入下一个阶段。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 GitHub 数据，我为您生成了 NullClaw 项目在 2026-06-28 的项目动态日报。

---

# NullClaw 项目动态日报 (2026-06-28)

**项目核心定位:** 个人 AI 代理/智能体框架
**数据来源:** github.com/nullclaw/nullclaw
**分析日期:** 2026-06-28

---

### 1. 今日速览

今日项目活跃度处于**低水平**。过去24小时内仅有1个新 Issue 和1个新 PR 被提交，且无新版本发布或任何 PR/Issue 被关闭。项目整体处于“缓慢前行”状态，社区讨论主要集中在尝试解决一个已知的、针对特定平台的构建问题，以及一项旨在提升AI Agent自主决策能力的新功能提案。维护者响应和社区参与度有待观察。

---

### 2. 版本发布

今日无新版本发布。

---

### 3. 项目进展

今日无任何 Pull Request (PR) 被合并或关闭，也无任何 Issue 被关闭。这意味着项目核心代码库在过去24小时内没有实质性的合并变更。所有进展仍停留在提议和讨论阶段。

---

### 4. 社区热点

今日社区焦点显然集中在两个新增的议题上，虽然讨论量不大，但指向了项目发展中的两个关键方向：**平台兼容性** 与 **Agent能力增强**。

- **Pull Request #969**: `feat(agent): structured approval_request / approval_response flow`
    - **链接**: [https://github.com/nullclaw/nullclaw/pull/969](https://github.com/nullclaw/nullclaw/pull/969)
    - **动态**: 由贡献者 `valonmulolli` 新提交的增强提案，旨在为Agent的Shell工具调用引入结构化的审批流程。
    - **诉求分析**: 社区开发者希望提升 Agent 在敏感操作（如执行Shell命令）时的安全性和可控性。该PR通过引入“双回合”的“请求审批-响应审批”流程，让 Agent 在需要权限时能主动暂停并请求用户批准，而不是直接失败或继续。这反映了用户对**提升AI Agent自主决策能力与安全边界控制**的迫切需求。

- **Issue #868**: `[bug] zig build fails on Android/Termux (aarch64) with AccessDenied on options.zig linkat`
    - **链接**: [https://github.com/nullclaw/nullclaw/issues/868](https://github.com/nullclaw/nullclaw/issues/868)
    - **动态**: 一个已存在约2个月的Bug (创建于2026-04-23)，今天被评论更新 (2026-06-27)，表明问题仍旧存在且未解决。
    - **诉求分析**: 用户尝试在 Android 平台的 Termux 环境中编译项目时遇到了文件链接权限问题。这表明 **NullClaw 在非主流平台（如移动端、容器化环境）上的构建支持仍有缺陷**，限制了潜在的用户群体，尤其是希望在移动设备上直接运行和测试Agent的用户。

---

### 5. Bug 与稳定性

本日仅报告了1个 Bug，严重程度为中高，因为它直接阻碍了开发者在特定环境下的正常构建和使用。

- **#868: [bug] zig build fails on Android/Termux (aarch64) with AccessDenied on options.zig linkat**
    - **严重程度**: **中-高**。该 Bug 完全阻止了在 Android (Termux) 环境下的 `zig build` 流程。
    - **状态**: **未修复**，无关联的修复 PR。
    - **摘要**: 用户 `NOTJuangamer10` 在使用 `zig 0.16.0` 和 `nullclaw v2026.4.17` 在 aarch64 架构的 Android 设备上编译时，因 `AccessDenied` 错误导致失败，关键操作是 `linkat`。
    - **可能原因**: 这是由于 Zig 构建系统在编译时尝试执行文件系统链接操作 (`linkat`)，但 Android/Termux 的安全限制或文件系统差异不允许此操作。修复可能需要修改构建脚本或条件编译。

---

### 6. 功能请求与路线图信号

本日新增的主要功能信号来自 **PR #969**，这是一个**明确的新功能实现**，而非单纯的请求。

- **结构化审批流 (PR #969)**: 此 PR 本身就是一个功能请求的实现。它提出的“双回合审批”机制，不仅是一个Bug修复，更是一个架构级别的改进。它修复了当前Agent在遇到 `ApprovalRequired` 错误时用户体验不佳的问题，并为未来所有`Tool`模块提供了一个统一的权限控制范式。**有较大概率被纳入下一个版本**，如果维护者认为其设计成熟且稳定。

---

### 7. 用户反馈摘要

从今天的 Issues 反馈中，可以提炼出用户的真实痛点：

- **环境兼容性痛点**: 用户渴望在非标准服务器环境（如移动设备）上运行AI Agent，但构建过程对文件系统的要求（如`linkat`）成为了主要障碍。这反映出项目在跨平台构建的健壮性上还有待提升。用户被迫使用特定版本的 Zig 和项目版本才能尝试，体验不佳。

---

### 8. 待处理积压

- **#868: Android/Termux 构建失败**: 这是一个**长期未响应的关键 Issue**（创建于2026-04-23，至今未解决）。该问题直接阻碍了 Android 平台用户的开发和使用，且可能随着 Zig 版本迭代影响更广。**强烈建议维护者优先关注**，并判断是否需要修改构建流程或提供平台特定的变通方案。这可能是一个推荐其他贡献者解决的“Good First Issue”，或是一个需要维护者介入的棘手兼容性问题。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 IronClaw GitHub 数据，为您生成 2026-06-28 的项目动态日报。

---

## IronClaw 项目动态日报 | 2026-06-28

### 1. 今日速览

今日项目活跃度**极高**，核心开发团队正在集中力量推进“**能力策略（Capability Policy）**”这一重大功能，标志着项目从基础架构搭建进入精细化权限管控阶段。过去24小时内，虽然合并/关闭了多达22个PR，但仍有28个PR等待合并，显示出开发节奏紧凑。Issues 方面，系列性的功能开发 Issue 被批量关闭，表明”Reborn 能力策略”这一史诗级目标的阶段性交付已完成。此外，一个关于 Google OAuth 令牌刷新的 Bug 被报告，需要重点关注。

### 2. 版本发布

今日未发布新版本。

### 3. 项目进展

今日项目核心进展集中在“**Reborn 能力策略（Capability Policy）**”的完整交付上。该功能旨在实现基于用户角色（Owner/Admin/Member）的精细化工具和技能权限管控。关键合并/关闭的 PR 及功能推进如下：

- **策略模型与引擎落地 (PR #5262, #5344)**：完成了策略定义、存储引擎（基于 libSQL/文件系统）和核心解析器的构建，为整个权限系统打下基础。
- **用户角色与权限管控 (PR #5270, #5355)**：实现了数据库支持的`UserRole`（Owner/Admin/Member），并为管理员提供了 REST API 来授予用户权限。这是从理论模型到实际可用管理界面的关键一步。
- **“可用性”维度交付 (PR #5349)**：新增了“可用性”维度，允许管理员控制特定工具或技能对用户的可见及可用状态。
- **集成测试框架建立 (PR #5381)**：建立了“Reborn”堆栈的集成测试框架，允许对整个请求-响应流程进行高保真度的内进程测试，显著提升未来功能开发的测试效率和可靠性。
- **依赖与基础设施更新**：合并了一个包含 47 个依赖更新的超大 PR (#5271)，并修复了 Hosted 环境的运行时启动问题 (#5382)，提升了项目的现代性和稳定性。

**总结：** 项目在“Reborn 用户权限体系”这一核心功能上取得了**里程碑式进展**，从建模、存储、解析到管理控制台和测试框架均已实现，为后续 UI 交互和多用户协作场景铺平了道路。

### 4. 社区热点

今日社区讨论热度相对集中于功能开发本身，暂无异常高热度的用户讨论。核心贡献者之间的协作与评论集中在主动推进中的功能和 Bug 修复上。

- **待观察链接:**
    - **PR #5380**: [Expand Reborn WebUIv2 QA matrix coverage](https://github.com/nearai/ironclaw/pull/5380) - 关于扩展 WebUI v2 测试矩阵的 PR，虽无评论但涉及 QA 流程，其后续影响值得关注。
    - **PR #5381**: [Reborn integration-test framework (slices 1–2)](https://github.com/nearai/ironclaw/pull/5381) - 建立了新的集成测试框架，是确保未来代码质量的关键。

### 5. Bug 与稳定性

今日报告的 Bug 及稳定性问题如下：

| 严重程度 | Issue/PR | 摘要 | 状态 | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | #5378 | **Google OAuth 令牌刷新失败**：在特定部署配置下（如 Railway），Google OAuth 令牌刷新失败，导致用户每约1小时就需要重新授权。直接影响 Gmail/Calendar 等功能的流畅使用。 | **已关, 无修复PR** | [Issue #5378](https://github.com/nearai/ironclaw/issues/5378) |
| 中等 | #5382 | **修复 Hosted 卷运行时启动**：修复了一个回归问题，该问题导致某些部署配置下的运行时无法正确挂载卷。 | **已合并修复** | [PR #5382](https://github.com/nearai/ironclaw/pull/5382) |
| 低 | #4928 | **Notion OAuth 重定向到 localhost**：在 Railway 部署环境下，Notion MCP 授权回调 URL 错误地指向 localhost，导致用户无法完成授权。 | **已关, 无修复PR** | [Issue #4928](https://github.com/nearai/ironclaw/issues/4928) |
| 低 | #4108 | **夜间的 E2E 测试失败**：持续约一个月的定时 E2E 测试失败，可能由依赖或环境变化导致，需排查根因。 | **打开中, 无PR** | [Issue #4108](https://github.com/nearai/ironclaw/issues/4108) |

### 6. 功能请求与路线图信号

- **核心信号：Reborn 能力策略（Capability Policy）主线已完成。**
    - 随着 Issue #5261 (Epic) 及关联的 #5272, #5273, #5267, #5266 等全部关闭，该功能的**后端核心逻辑和 REST API 已基本就绪**。
    - 目前仍有一个开放的 Issue **#5385**，主题同样是“添加能力策略”，建议项目维护者**将其标记为与 Epic #5261 重复**，以避免社区混淆。
- **UX 改进信号：**
    - **Issue #5364**：建议将“始终允许符合条件的工具”选项默认开启，以减少新用户每次使用时同意弹窗的干扰。该需求已在 PR #5364 中解决。这反映了开发者对 **开箱即用（Out-of-the-box）** 流畅体验的重视。

### 7. 用户反馈摘要

今日缺乏大量用户层面的直接反馈。从 Issue 报告和开发 PR 中可提取出以下隐含的“用户”体验需求：

- **稳定性与流畅性：** 用户（在此情境下为内部测试者/贡献者）反馈最多的痛点是 **OAuth 令牌刷新** (#5378, #4928) 和 **E2E 测试稳定性** (#4108)。这表明当前部署和 CI 环境存在可靠性挑战，可能影响到外部贡献者和早期试用者的信心。
- **易用性诉求：** **Issue #5364** 和 **PR #5364** 中关于默认启用“始终允许”的改动，清晰地表明了对简化用户交互流程的强烈诉求。默认开启可以减少不必要的许可弹窗，提升聊天体验的流畅度。

### 8. 待处理积压

以下为需要维护者关注的长期未解决问题：

| 类别 | 项目 | 创建时间 | 现状 | 建议行动 | 链接 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Bug** | **Nightly E2E failed (#4108)** | 2026-05-27 | 持续失败超过1个月 | 安排专人排查 CI 环境或代码变更，修复或关闭此自动打开的 Issue。 | [Issue #4108](https://github.com/nearai/ironclaw/issues/4108) |
| **Bug** | **Notion OAuth redirects to localhost in Railway deployment (#4928)** | 2026-06-15 | 已关闭但无解决方案。 | 虽然已关闭，但问题本身并未解决。需确认是否在后续重构中已修复，或重新打开并定位。 | [Issue #4928](https://github.com/nearai/ironclaw/issues/4928) |
| **PR** | **Reborn: no run-borking failures (#4841)** | 2026-06-13 | 长期未合并的 XL 级 PR，旨在提升系统健壮性。 | 评估此 PR 在当前“能力策略”主线后的优先级，考虑推进 Code Review 或调整策略。 | [PR #4841](https://github.com/nearai/ironclaw/pull/4841) |
| **功能** | **Add Capability Policy (#5385)** | 2026-06-27 | 新开 Issue，与主线 Epic 重复 | 将其标记为 `Duplicate`，并链接到 #5261，避免社区工作分散。 | [Issue #5385](https://github.com/nearai/ironclaw/issues/5385) |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的LobsterAI GitHub数据，以下是为2026年6月28日生成的项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-28

## 1. 今日速览

项目整体活跃度**中等偏高**。过去24小时内，社区提交了2个新Issues（均为Bug报告），其中包含一个严重程度为“高”的桌面端卡死问题。PR合并/关闭活动频繁（7条），但均为之前的`[stale]`标记PR，表明项目正在集中清理积压的PR。值得注意的是，本周没有新版本发布。虽然维护者对新Issue的响应速度尚不明确，但合并大量旧有PR表明维护者正在积极改进代码库的稳定性和功能。

## 2. 版本发布

无。

## 3. 项目进展

今日项目推进集中在“**稳定性修复**”和“**体验优化**”上，共计合并/关闭了7个由`[stale]`标记的历史PR，表明团队正在清理待处理工作，提升软件质量。

**主要合并/关闭的PR包括：**

- **MCP协议支持扩展**： `#1001` 修复了MCP传输类型为SSE和流式HTTP时配置不生效的问题，为更广泛的工具集成铺平了道路。
- **核心稳定性修复**： `#1446` 解决了OpenClaw网关因无限重启循环导致应用瘫痪的严重问题，根因是进程退出时的竞态条件。这对于依赖网关进行复杂任务协同的用户至关重要。
- **用户界面及体验优化**：
  - `#1448` 修复了Agent设置页面中“删除”按钮和搜索提示未国际化为中文的问题。
  - `#1449` 对定时任务多次执行记录进行折叠分组，解决了侧栏堆积大量会话记录，干扰用户查找的问题。
  - `#1454` 修复了“不重复”模式下清空日期后创建定时任务按钮无响应的静默失败Bug。
  - `#1456` 增加了快捷键的重复检测，防止用户在不知情下为多个功能设置同一个快捷键组合。
- **数据一致性与功能修复**：
  - `#1453` 修复了已停用的技能仍被注入对话提示词的问题，确保用户对技能的禁用操作能真正生效。
- **未合并的亮点PR**： `#2065` 目前仍处于开放状态，计划使用短UUID替代名称生成Agent ID，从根本上解决因ID重复导致旧数据意外复活的Bug。该PR也指出了当前删除Agent操作中存在数据清理不完整等问题，值得关注。

**总结：** 通过这些修复，LobsterAI在**网关稳定性**、**UI/UX**、**国际化**、**数据一致性**以及**配置管理**方面均取得了实质性的进步，软件健壮性得到提升。

## 4. 社区热点

今日社区讨论热度较低，提交的2个新Issues均无评论。

**最受关注的Issues：**
- **`#2215` [Bug] 安装失败：Resource extraction failed**：这是一个新提交的安装问题，尽管作者通过详细自查后发现了问题所在（真实安装路径非默认路径），但问题本身代表了一种典型的用户安装障碍，尤其是在路径配置不明确的环境下。
- **`#2214` [Bug] 数据备份导致主进程卡死**：该Bug严重级别为“高”，100%可复现。在用户拥有较大数据库（71.6 MB）和大量对话记录的典型使用场景下，备份功能会直接导致应用无响应，严重影响了用户对数据安全功能的信任。

**用户诉求分析**：两个Issue均指向“**高负载下的稳定性与可靠性**”。用户在安装初期可能因路径问题受阻，而在长期重负载使用后，关键的数据备份功能又可能导致进程卡死。这暗示用户群中可能存在重度用户，其数据规模和复杂度超出了当前软件设计的某些边界情况。

- **Issue #2215**: [链接](https://github.com/netease-youdao/LobsterAI/issues/2215)
- **Issue #2214**: [链接](https://github.com/netease-youdao/LobsterAI/issues/2214)

## 5. Bug 与稳定性

今日报告的Bug严重程度均较高，且直接关系到核心功能可用性。

| 严重程度 | Bug描述 | Issue/PR | 影响模块 | 当前状态 | Fix PR |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **高** | 桌面端“数据备份”功能导致主进程100%卡死（未响应），用户需强制关闭。 | `#2214` | 数据备份/主进程 | 开放，未关闭 | 无 |
| **中** | 安装时反复出现“Resource extraction failed: could not start extractor process”错误。 | `#2215` | 安装程序 | 开放，未关闭 | 无 |

**分析**：`#2214` 问题尤其值得警惕。在WAL模式下，网关持续写入数据库时触发备份，极有可能是备份操作未正确处理数据库连接状态或文件锁，导致主进程阻塞。此问题对日常需要备份的用户有毁灭性体验。

## 6. 功能请求与路线图信号

今日未收到明确的新功能请求（Feature Request）。然而，通过对历史PR的分析，可以判断出以下方向可能被纳入未来版本：

- **细粒度的数据管理**： `#2065` 提出的使用UUID替代名称生成Agent ID，以及指出删除Agent时的数据清理不完整问题，暗示项目正在规划更可靠的数据生命周期管理功能，包括更完善的“删除”和“回收”机制。
- **用户体验打磨**： `#1449` 的会话折叠功能和`#1456`的快捷键冲突检测，显示项目在持续优化日常使用的交互细节，减少干扰和困惑。

这些`[stale]`PR的合并，表明团队有意清理这些“技术债”，为下一阶段的稳定版本发布做准备。

## 7. 用户反馈摘要

从今日的Issues中可以看出用户的典型使用场景和痛点：

- **用户痛点：**
    1.  **安装受阻**：`#2215` 显示用户在安装过程中遇到路径混淆的难题，尽管通过手动分析找到了真实路径，但过程繁琐。用户希望安装程序能更智能地识别和处理类似冲突。
    2.  **数据安全焦虑**：`#2214` 反映出用户在产生大量数据后，对数据备份的可靠性感到焦虑。用户已经依赖该功能进行日常数据保护，但其在关键时候的卡死让用户感到不满和无助。
- **用户使用场景：**
    - 用户是重度使用者（“每天有几百条消息”），数据量较大（71.6 MB）。
    - 用户依赖任务自动化（定时任务），并因此产生了大量记录，影响了普通会话的查找。
    - 用户对外部工具集成（MCP）有明确需求（`#1001`）。

## 8. 待处理积压

以下是对项目健康度有潜在影响，但暂无积极响应的重要积压项：

- **`#2065` [OPEN] fix(agent): 使用短 UUID 替代名称生成 Agent ID**：该PR自5月底创建，已标记为`[stale]`，但至今未合并。其修复的“数据复活”问题和提出的删除Agent数据不完整问题，都是影响数据安全和一致性的关键隐患。维护者应优先关注并推动此PR的合并，以堵塞这一已知的数据管理漏洞。

  **链接**: [Issue #2065](https://github.com/netease-youdao/LobsterAI/pull/2065)

---
**报告结束**

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报。

---

## Moltis 项目动态日报 — 2026-06-28

### 1. 今日速览

今日项目整体活跃度处于中等水平。过去24小时内没有新版本发布，但社区提交了两项关键的修复性 PR，主要聚焦于提升与本地/小型模型的兼容性。同时，一条关于 Apple 容器 ID 长度限制的新 Bug 被上报。代码库正在稳步推进，重点在于增强对非标准模型输出格式的鲁棒性。

### 2. 版本发布

无

### 3. 项目进展

今日没有 PR 被合并或关闭。但是，有两项重要的修复正处于待审查状态：

- **PR #1136** (`fix(agents): coerce stringified scalar tool args before validation`) 旨在修复一个在本地模型（如 Gemma 4）上发现的兼容性问题。这类模型有时会将标量参数（如 `"true"` 或 `"5000"`）以 JSON 字符串形式传递给工具调用，导致验证失败。此 PR 通过在验证前强制转换这些字符串参数，拓宽了 Moltis 支持的模型范围。
- **PR #1098** (`fix(browser): tolerate null optional params in browser tool calls`) 处理了另一个本地模型（同样是 Gemma 4）的兼容性问题，即模型会为未使用的可选参数显式传递 `null` 值。此 PR 通过修改 `serde` 反序列化逻辑，使其能够容忍这些显式的 `null` 值，而非直接将它们视为无效。

### 4. 社区热点

过去24小时内没有高讨论度的 Issue 或 PR。两个开放 PR (#1136 和 #1098) 的评论数为 `undefined`，可能表示未有新的讨论发生。新上报的 Bug #1137 也尚无评论。

### 5. Bug 与稳定性

今日上报了一个新的 Bug：

- **严重程度：高**
- **Issue #1137** (`[Bug]: Apple Container ID exceeds name limit`) 由用户 `holgzn` 提交。问题的核心是，在 Apple 平台上，Moltis 生成的容器 ID 长度超出了系统允许的名称限制。该问题可能导致创建或管理容器时出现错误，属于平台特定的功能性 Bug。目前尚未有针对此问题的修复 PR。
    - 链接: [Issue #1137](https://github.com/moltis-org/moltis/issues/1137)

### 6. 功能请求与路线图信号

今日没有新的功能请求提交。结合已有的 PR 来看，当前项目的重点方向非常明确：**增强与小型/本地语言模型（如 Gemma 4）的兼容性**。PR #1098 和 #1136 的贡献者均为 `resumeparseeval`，这表明社区中有用户正在深入使用 Moltis 搭配本地模型，并发现了具体的集成问题。这些修复很可能被包含在下一个小版本或补丁版本中。

### 7. 用户反馈摘要

今日无新的用户反馈。从 PR 的描述中可以推断出用户的真实痛点：
- **工具参数格式问题**：用户在使用本地模型时，面临工具调用参数格式不标准的问题（例如 `"true"` 代替 `true`，`null` 代替字段缺失）。这反映出当前对灵活输入的处理能力有待加强。
- **使用场景**：用户正在尝试使用 Moltis 与低成本或离线可用的模型（如 Gemma 4）搭建 Agent 应用，并期望其行为与强大的闭源模型保持一致。

### 8. 待处理积压

目前没有长期未响应的 Issue 或 PR。PR #1098 创建于 6月3日，距今已近25天仍未合并，需要维护者重点关注。考虑到它与新提交的 PR #1136 同属一个贡献者且解决方向一致（本地模型兼容性），建议一起审查和合并。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据CoPaw项目在2026年6月27日至28日期间的GitHub活动数据生成的日报。

---

# CoPaw 项目动态日报 | 2026-06-28

**项目名称**: CoPaw (github.com/agentscope-ai/CoPaw)
**数据周期**: 2026-06-27 ~ 2026-06-28

---

### 1. 今日速览

今日CoPaw项目**活跃度极高**，主要得益于密集的测试覆盖率推进和用户反馈的Bug修复。

- **测试质量大幅提升**：社区开发者在后端（`app-infra`, `runner`, `crons`）和前端（`console`）模块提交了多个仅含测试的PR，新增了数百个单元测试用例，为项目的新架构（2.0）打下坚实的质量基础。
- **关键Bug正在修复**：针对用户报告的“DeepSeek V4思考模式错误”和“对话记录丢失”两个严重问题，都有对应的修复PR（#5582, #5579）提交或讨论，响应迅速。
- **自动化与集成增强**：针对Matrix渠道的流式响应、Tauri桌面版初始化流程的修复、以及治理策略模式的泛化等PR均已提交，显示项目在持续完善基础设施和平台适配。

### 2. 版本发布

无

### 3. 项目进展

今日有 **1 个重要PR被合并**，标志着项目在用户体验和测试覆盖上取得进展。

- **合并的PR：**
    - **#5213 `fix(console): improve MCP access policy layout`**：该PR修复了MCP客户端卡片在窄屏下的布局错位问题，并优化了工具权限模态框的响应式设计和访问主体发现功能。这直接提升了用户在管理MCP工具时的管理体验。

- **重要进展中的PR（测试覆盖）**：社区成员 `hanson-hex` 提交了一系列“测试优化冲刺”PR，是今日讨论的绝对中心。尽管尚未合并，但代表了项目对代码健壮性的坚定承诺：
    - **#5581**: 为`app-infra`后端层（`agent_context`等）新增11个单元测试。
    - **#5422**: 为`runner`模块新增47个单元测试。
    - **#5423**: 为`crons`模块新增51个单元测试。
    - **#5409, #5434, #5438**: 为前端控制台（`console/`）的Stores、Hooks、Inbox及API模块累计新增超过420个单元测试。
    - 这些工作将显著提升项目从1.x迁移到2.0后的代码稳定性，并有效防止回归问题。

### 4. 社区热点

今日讨论的焦点集中在两个问题上，体现了用户在生产环境和高级功能使用上的痛点。

1.  **Issue #5573 [Bug] DeepSeek V4 thinking 模式错误** `(2条评论)`
    - **链接**: [Issue #5573](agentscope-ai/QwenPaw Issue #5573)
    - **分析**: 这是今日最核心的Bug讨论。用户报告了在使用非官方DeepSeek端点时，流式响应中的`reasoning_content`字段缺失以及工具调用Schema中包含`null`类型导致的400错误。
    - **社区诉求**: 用户不仅报告了问题，还提供了详细的复现步骤和自行验证的修复方案。这表明社区中**有较高技术能力的用户**正在积极贡献，并期望项目能对非标准但广泛使用的API端点（如第三方中转站）提供更好的兼容性，特别是对DeepSeek V4这类前沿模型的思维链功能。

2.  **Issue #5579 [Bug] 对话记录在异常中断下丢失** `(1条评论)`
    - **链接**: [Issue #5579](agentscope-ai/QwenPaw Issue #5579)
    - **分析**: 该问题描述了Agent执行系统命令（如重启）或服务意外崩溃后，对话记录完全消失的严重场景。
    - **社区诉求**: 这直接关系到用户对AI助手的信任度和使用连续性。用户强烈要求引入**断点保存机制**，让对话记录能抵御非正常中断。这不仅是功能需求，更是一个关乎数据安全与用户体验的稳定性问题。

### 5. Bug 与稳定性

今日报告了3个新Bug，按严重程度排列如下：

- **严重：对话记录丢失 (`#5579`)**
    - **描述**: Agent执行重启命令或服务崩溃后，当前对话记录完全丢失，无恢复可能。
    - **状态**: `[OPEN]`。该Issue已获得开发者关注，预计将很快被纳入修复计划。

- **严重：DeepSeek V4 兼容性错误 (`#5573`)**
    - **描述**: 在非官方OpenAI兼容端点上使用DeepSeek V4时，流式响应和工具调用均会失败，报400错误。
    - **状态**: `[OPEN]`，已有关联修复`PR #5582`。当前非流式路径已修复，流式路径的修复PR正在审查中。预计下一个版本将解决此问题。

- **中度：自定义Ascend-vLLM模型连接失败 (`#5584`)**
    - **描述**: 从1.1.7版本升级后，无法连接到自定义Ascend-vLLM服务端，尽管配置测试通过。
    - **状态**: `[OPEN]`，有1条评论。可能为新版本中接口变更导致的回归问题。

- **较低：UI交互问题**
    - **#5583 [Question]**: 聊天界面右侧弹窗默认选中项的背景不明显，属于用户体验优化问题。
    - **#5580 [CLOSED]**: 已被标记为完成的后端测试覆盖任务，由PR #5581跟进。

### 6. 功能请求与路线图信号

- **【高优先级】 Matrix渠道流式响应 (`#5585`)**: PR `#5585` 旨在为Matrix即时通讯渠道增加与Discord类似的流式响应模式，提升用户交互的实时感。这表明项目正积极扩展其多平台支持能力，这可能是下一版本的重要更新点。
- **【信号】 治理策略模式泛化 (`#5546`)**: PR `#5546` 提出将内部的**治理策略模式**进行通用化改造。这暗示了项目正在抽象其核心安全与权限模型，未来可能允许用户自定义更复杂的访问控制和审核策略，这是一个架构层面的重要信号，可能服务于更复杂的企业级应用场景。

### 7. 用户反馈摘要

- **用户痛点与场景**:
    - **“代理即工具”的风险**：`#5579` 的提出者描述了一个具体场景：Agent执行了重启宿主机的命令导致对话丢失。这揭示了当用户赋予AI高权限时，系统自身的容错机制必须跟上，否则将产生严重的数据损失。
    - **“自建模型服务”的兼容性壁垒**：`#5584` 和 `#5573` 反映出许多高级用户倾向于使用自建或第三方托管的非官方模型服务。CoPaw在升级过程中对此类服务的兼容性出现波动，影响了这部分核心用户的体验。
    - **用户积极贡献代码**：`#5573` 的贡献者承认自己“非python程序员”，但通过实际验证提供了修复方案。这表明项目门槛较低，社区氛围包容，且有贡献者愿意深入代码层解决问题。

### 8. 待处理积压

- **PR #4622 `plugin(datapaw): add data-analysis plugin`**
    - **创建时间**: 2026-05-22
    - **状态**: `[OPEN]`，标记为 `Under Review`
    - **链接**: [PR #4622](agentscope-ai/QwenPaw PR #4622)
    - **分析**: 这是一个添加数据分析插件（DataPaw）的重要功能PR，已被搁置超过一个月。该插件包含12个BI技能，对扩展CoPaw的能力边界至关重要。鉴于近期测试覆盖工作进展迅速，建议维护团队在下一阶段优先评估和合并此PR，以丰富项目的功能库。

- **Issue #5573 [Bug] DeepSeek V4 错误**
    - **状态**: `[OPEN]`
    - **分析**: 尽管已有关联的修复PR，但此Issue本身已积累了用户讨论和修复建议。如果合并了PR #5582，应立即关闭此Issue并向用户通报，确保问题闭环，避免社区困惑。

---

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 ZeroClaw 项目数据生成的 2026-06-28 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-28

## 1. 今日速览

ZeroClaw 项目在**周六依然保持了极高的活跃度**。过去 24 小时内，共有 41 条 Issue 和 50 条 PR 被更新，社区贡献者与核心团队正共同推动着多个重大特性的落地。**新发布的 RFC 数量激增**，特别是围绕 **Wasm 插件运行时**、**供应量链安全** 和 **网络协议重构** 等基础架构层面，表明项目正从功能填充期进入深度架构优化期。**“Goal Mode”** 这一新概念有望为自主代理的工作模式带来质变，而**MCP 支持扩展**是当前最受关注的社区诉求。

## 2. 版本发布

- **无新版本发布**。项目正处于 v0.8.3 和 v0.9.0 两个大版本的并行开发阶段。

## 3. 项目进展

过去 24 小时有 3 个 PR 被合并/关闭，另有 47 个待合并状态的 PR 中蕴含了大量即将落地的重大变更。核心进展包括：

- **核心运行时修复 (P1)**：
    - **PR #8306**（已合并）：合并了一份由社区贡献的、面向 LLM 代理的全面文档集 `ZEROCLAW_LLM_AGENT_DOCUMENTATION.md`。这标志着项目在提升自身对 AI 开发者友好度方面迈出的关键一步，有助于 AI 开发者更好地集成和使用 ZeroClaw。
- **社区贡献的基础设施优化**：
    - **PR #8350**：合入了 `web-search` 工具的微性能优化，将 `strip_tags` 正则编译移入 `LazyLock` 静态变量，避免了每次调用时的重复编译开销。
- **功能落地 - 核心规则与警报系统 (SOP)**：
    - **PR #8400** 和 **PR #8391** 两个重大的“核心规则和警报 (SOP)”特性 PR 被创建，并已打上 `stacked` 标签，表明它们是一个大型功能（EPIC A1）的组成部分。这些 PR 为守护进程添加了周期性 SOP 维护机制，并连接了基于定时触发的 SOP 规则，标志着 SOP 功能正从理论设计走向工程实现。

## 4. 社区热点

最受关注的讨论集中在项目的安全基础、AI 交互体验和核心架构上。

- **#8177 [HIGH] RFC: Supply chain signing** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8177)
    - **10条评论**。这是本周最受关注的 RFC，讨论如何通过硬件 PGP、多签、离线签名等方式实现供应链安全，紧跟行业趋势。该 RFC 已被阻塞，等待 `#8058` 的 CI 工作流完成。
- **#5808 [P1, IN-PROGRESS] Default 32k context budget exceeded** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/5808)
    - **6条评论**。一个存在已久的 P1 级 Bug，持续吸引着评论区讨论。社区和开发者对于如何解决系统提示和工具定义侵占太多上下文预算的问题非常关切。
- **#8396 [OPEN, HIGH] RFC: Wire-Protocol-First Provider Model** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8396)
    - **1条评论**。尽管评论数少，但该 RFC 涉及重构提供商模型，将通信协议 (wire API) 作为首要组织原则，是一个影响深远的架构级提案。这表明社区在推动更健壮和统一的底层支持。
- **#4467 [OPEN, HIGH] Add MCP resource and prompt support** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/4467)
    - **获得了4个赞**。虽然评论数稳定，但高赞数表明这是用户最广泛期望的功能之一，即扩展 MCP 客户端能力，不仅仅支持 Tool，还能访问外部 MCP 服务器的资源和提示。

## 5. Bug 与稳定性

过去 24 小时追踪到的 Bug 主要集中在配置、默认行为和运行时不一致上。

- **P1 级 (严重):**
    - **#8386 [Bug]: SQLite 是默认记忆后端，但快速入门从未要求嵌入模型** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8386) - **当前无修复 PR**。这是一个典型的配置陷阱，默认配置会静默导致混合搜索降级为仅关键字搜索，严重影响首次使用体验。
    - **#5808 [Bug]: 默认上下文预算被超出** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/5808) - **当前无修复 PR**。作为 P1 持续存在的性能/Bug，是核心团队需要优先攻克的问题。
- **P2 级 (次要/降级):**
    - **#8397 [Bug]: 任务文件读取路径错误** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8366) - **已有修复 PR #8402**。`HeartbeatEngine` 从错误路径读取任务文件，导致配置与运行时行为不一致。对应修复 PR 已在 24 小时内提交，处理效率高。
    - **#2128 [Bug]: Cron 和心跳任务发送 “NO_REPLY” 文本** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/2128) - **昨日已有修复 PR #8405**。一个困扰社区几个月的痛点问题。一个 `P2` 级的噪声问题，导致不必要的消息推送。修复 PR 已创建。

## 6. 功能请求与路线图信号

- **高优先级新功能 (可能纳入 v0.8.3 / v0.9.0):**
    - **Goal Mode (#8303)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8303): 这是一个重量级 RFC，提出了一种新的“任务模式”，允许代理在一个持久化、有状态的会话中自主完成目标直到成功、取消或预算耗尽。这符合 AI Agent 从“对话式”向“执行式”演进的趋势。已有配套的 ADR PR (#8393) 跟进。
    - **MCP 资源与提示 (#4467)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/4467): 有对应的 `feat` PR (#8403) 被创建并处于待合并状态，包含策略门控的分发工具，进度清晰。**预计很快会落地，是近期最值得关注的功能更新。**
    - **Wasm 插件运行时 (#8135)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8135): 另一个战略级 RFC，将 Wasm 作为默认插件运行时，并强制能力声明和签名分发。这与 v0.9.0 的“安全加固”方向完全一致。
- **社区呼声较高的新功能:**
    - **OpenRouter 模型回退 (#8138)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8138): 请求支持 OpenRouter 的 `fallback_models` 数组，以提升 API 的可靠性。这是一个成本廉价但收益显著的改进。
    - **WhatsApp 被动群组上下文 (#8379)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8379): 为了减少群聊噪音和 Token 消耗，用户希望 Bot 能仅记录消息作为上下文，而无需每次都启动代理回合。已有对应的 `feat` PR (#8389) 被创建，并对所有渠道架构进行了相应调整，诚意十足。
    - **ZeroCode 任务追踪器 (#8401)** [链接](https://github.com/zeroclaw-labs/zeroclaw/issue/8401): 来自黑客马拉松团队的真实需求，希望能有类似 Claude Code 的任务列表可视化 UI，提升 ZeroCode 的用户体验。

## 7. 用户反馈摘要

从 Issue 评论中，提炼出以下用户痛点和使用场景：

- **上手体验不佳**: **Issue #8386** 中用户尖锐地指出，默认迁移后端（SQLite）和默认嵌入模型配置之间的不一致，导致新用户在快速入门时不知不觉地牺牲了核心搜索功能。**“用户在论坛上抱怨 AI 助手记忆差，而你其实是忘配置了模型。”** 这是非常典型的开箱即用体验差的问题。
- **工具噪声过大**: Issue #2128 的长期存在反映了社区对该问题的耐心已经到了极限。用户明确表示，`NO_REPLY` 机制应该被静默处理，而不是发送到通道。**“如果不需要报告，我希望什么也不发生，而不是看到一条无意义的消息。”**
- **对 MCP 资源/提示支持的高期待**: 从 Issue #4467 的高赞数可以看到，开发者正在遭遇 ZeroClaw 作为 MCP 客户端的能力瓶颈。外部服务商（如数据库、监控工具）常常通过“资源”和“提示”暴露核心能力，而 ZeroClaw 只能使用工具，这限制了其集成深度。
- **对架构清晰度的需求**: 多位用户在 RFC (#8396, #8398, #8396) 评论区表达了希望项目能更清晰地定义 Provider、Plugin 等核心概念，并明确设计方向。**“请先决定好架构，再让我们写代码。”** 这反映了社区对项目长期健康度的关心。

## 8. 待处理积压

以下是长期未响应或等待维护者关注的重大事项：

- **长期存在的 P1 Bug**:
    - **#5808 (16天以上)**: 上下文预算 bug。已影响 16 天以上，虽标记为 `status:in-progress` 和 `status:accepted`，但无一个明确的修复 PR 提交。这是高风险 P1 级问题，建议维护者人讨论解决方案并指定责任人。
- **阻塞性 RFC**:
    - **#8177 供应量链安全 RFC**: 被 `#8058` 状态阻塞。建议维护者尽快决定 `#8058` 的命运，否则此 RFC 的讨论将一直处于停滞状态，影响项目安全性规划的推进。
- **复杂的配置型 PR**:
    - **#8305 网关 MCP 配置回退逻辑**: 一个中等规模的修复 PR，尽管已标注 `Fix: #8302`，但仍等待最终审核。考虑到它解决的是一个典型的配置不匹配问题，建议尽快合并，避免 QA 积压。
- **搁置中的架构讨论**:
    - **#8398 插件权限模型 RFC**: `master` 分支仅包含一个粗颗粒度的权限枚举，该 RFC 暴露了多个未解决的开放问题。维护者应判断是否将此 RFC 的讨论纳入 v0.9.0 的规划中，或暂时搁置。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*