# OpenClaw 生态日报 2026-06-26

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-26 02:02 UTC

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

好的，这是为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-26

## 1. 今日速览

项目今日呈现出极高的社区活跃度，共更新 1000 条 Issue 和 PR。核心状态为 **“高产但积压严重”**：一方面有大量功能请求和 Bug 报告涌入（新开 Issue 475个），另一方面合并/关闭的 PR 数量（94个）远低于待处理数量（406个），显示出审核流程可能存在瓶颈。安全、数据丢失和会话状态相关问题仍是社区关注的核心焦点。今日无新版本发布，大量问题处于待处理状态，项目整体健康度评分 **中等偏低**，需要维护者集中精力处理积压。

## 2. 版本发布

**无**。过去24小时内无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 数量为 94 个，以下是其中一些关键进展：

*   **新增本地实时语音与听写功能 (Local Realtime Voice & Dictation)**
    *   **PR #96173** (已合并): 新增了 `local-realtime-voice` 扩展，该扩展基于 `gateway-relay` 传输层，集成 Whisper STT、Ollama 聊天和 Kokoro TTS，提供了一个免费、自托管的实时语音和听写解决方案。
    *   **PR #96876** (已关闭): 在 #96173 的基础上，增加了将语音对话路由至主代理循环的选项，使得语音会话可以复用与文本聊天相同的工具、子代理和文件写入能力。

*   **用户体验与稳定性修复**
    *   **PR #94857** (待审核): 将默认的进度草稿标签从“甲壳类/航海”术语（如 `Lobstering`）替换为中性的技术术语（如 `Thinking`），改善了用户理解度。
    *   **PR #96636** (待审核): 修复了 `edit` 工具在模糊匹配时，会因归一化整个文件而导致无关行被重写的 Bug，提升了代码编辑的精确性。
    *   **PR #81364** (待审核): 新增了在安装社区插件和技能前检查 ClawHub 信任度的机制，以阻止恶意或不安全的发布，增强了生态安全性。

**总结**：项目在扩展功能和修复特定 Bug 方面取得了进展，但绝大多数修复仍处于等待审核或需要更多证据的状态。

## 4. 社区热点

以下 Issue 和 PR 在过去 24 小时内引发了最活跃的讨论，反映了社区的核心关切：

*   **#58450 - 代理“空头支票”问题 (评论: 15, 👍: 3)**
    *   **链接**: [Issue #58450](https://github.com/openclaw/openclaw/issue/58450)
    *   **诉求**：用户强烈不满代理经常做出诸如“我会检查项目记忆并回复”的承诺，但实际上并未启动任何后台操作。这造成了用户期望与实际行为不符的**信任危机**。社区对此问题共识度高，希望得到解决。

*   **#63216 - 会话的硬重置风暴 (评论: 11, 👍: 3)**
    *   **链接**: [Issue #63216](https://github.com/openclaw/openclaw/issue/63216)
    *   **诉求**：用户报告在特定群组会话中，尽管配置了高容错阈值（`reserveTokensFloor`），代理仍然会因上下文溢出而反复进行硬重置，并导致引导上下文被重复注入。这是一个严重的稳定性问题，严重影响了长会话或群聊场景下的用户体验。

*   **#53599 - 浏览器扩展远程中继功能被移除 (评论: 6, 👍: 5)**
    *   **链接**: [Issue #53599](https://github.com/openclaw/openclaw/issue/53599)
    *   **诉求**：这是一个用户情绪强烈的“回归”报告。v2026.3.22 移除了 Chrome 扩展的中继 WebSocket 服务器，且替换方案仅支持本地主机，无法跨机器工作。这直接导致了许多依赖此功能进行远程管理的**托管服务提供商无法使用**。

## 5. Bug 与稳定性

今日报告的 Bug 问题较为集中，涉及数据安全、会话状态和核心功能崩溃，按严重程度排列如下：

*   **高危：系统稳定性与资源耗尽**
    *   **#91009** `Codex PreToolUse` 原生钩子导致高 CPU 占用和 Gateway RPC 卡死 (P1, **无 Fix PR**)
    *   **#54155** Gateway 内存泄漏: 4天内从 389MB 增长至 14.7GB (P1, **无 Fix PR**)
    *   **#55334** `sessions.json` 无界增长导致 Gateway OOM (P1, **无 Fix PR**)

*   **高危：功能与数据完整性**
    *   **#51429** 工作路径被硬编码为 `/Users/wangtao`，导致所有用户目录创建异常 (P2, **无 Fix PR**) - *这是一个非常低级的错误，严重影响用户首次体验。*
    *   **#53540** LLM 生成大参数工具调用时，因耗时超过请求超时，触发“网络连接丢失”错误 (P1, **无 Fix PR**)
    *   **#53599** Chrome 扩展远程中继 WebSocket 服务器被移除，导致跨机器代理功能回归 (P1, **无 Fix PR**)

*   **中危：行为错误与回归**
    *   **#49876** Cron 会话在工具调用失败时，会生成幻觉输出而非干净地失败 (P1, **无 Fix PR**)
    *   **#52130** Telegram 重试抖动类型不匹配导致重启风暴 (P1, **无 Fix PR**)
    *   **#43747** 回归：内存管理混乱，不同用户的行为不一致 (P2, **无 Fix PR**)

**小结**：大量高优先级的 Bug 没有关联任何修复 PR，表明项目在解决核心稳定性问题上的投入严重不足，这可能是最需要关注的风险点。

## 6. 功能请求与路线图信号

*   **社区技能生态与 ClawHub (#50090)**: 用户高度关注社区技能和 ClawHub 生态的成熟度。当前“承诺与现实之间的差距”很大，开发者希望能有完善的标准、审核和发布机制。**已有关联的 PR #81364 正在尝试解决信任问题。**

*   **多渠道消息可靠回传 (#54531)**: 用户强烈要求修复来自 Telegram、Discord 等渠道的回复消息无法正确返回原频道的 Bug。这是一个**高频刚需**，关系到多平台部署的可用性。**(无关联 Fix PR)**

*   **多索引嵌入记忆与模型故障切换 (#63990)**: 生产环境用户希望记忆系统能支持多嵌入模型，并实现智能故障切换，避免因单一模型失败导致整个 RAG 功能不可用。这是一个**成熟的架构优化请求**。

*   **强制回复到原始渠道 (Force reply to originating channel) (#54531)** 和 **未绑定作用域清除 (clearUnboundScopes) 问题 (#51396)** 等问题，也反映出用户对多通道集成和细粒度权限控制的迫切需求。

## 7. 用户反馈摘要

*   **痛点与不满**：
    *   “我今天刚安装的最新版，结果 OpenClaw 建了一个 `/Users/wangtao` 的文件夹... 这位 wangtao 是谁？” - **#51429** (对低质量代码合入的震惊与不满)
    *   “我的连接从来没稳定超过24小时...体验非常糟糕。” - **#54531** (对消息传递可靠性极度不满)
    *   “我们团队的三个人的记忆管理方式都不一样。” - **#43747** (对行为不一致的困惑)
    *   “这是一个**信任和安全问题**。用户收到了看似合理但实际是编造的虚假报告。” - **#49876** (对代理幻觉问题的严重关切)

*   **使用场景与期望**：
    *   用户希望 cron 任务在失败时能**静默失败**，而不是产生误导性信息，这在使用于监控告警场景时至关重要 (**#49876**)。
    *   托管服务提供商依赖 Chrome 扩展的远程中继能力来管理远端浏览器，该功能的移除对他们来说是**毁灭性的** (**#53599**)。
    *   用户在长对话和群组聊天中，期望记忆和上下文管理更加可预测和稳定 (**#63216, #50165**)。

## 8. 待处理积压

以下 Issue 和 PR 已存在较长时间且对项目至关重要，但至今仍未获得维护者的明确回应或解决方案，提醒关注：

*   **#51429 - 工作路径硬编码 Bug** (创建于 2026-03-21)
    *   **链接**: [Issue #51429](https://github.com/openclaw/openclaw/issue/51429)
    *   **影响**: P2，极差的开箱体验，可能导致非技术用户弃用。

*   **#50090 - 社区技能发展生态** (创建于 2026-03-19)
    *   **链接**: [Issue #50090](https://github.com/openclaw/openclaw/issue/50090)
    *   **影响**: 关乎社区活力和项目长远发展的核心问题，需要明确的路线图。

*   **#55334 - sessions.json 无界增长导致 OOM** (创建于 2026-03-26)
    *   **链接**: [Issue #55334](https://github.com/openclaw/openclaw/issue/55334)
    *   **影响**: P1，严重威胁服务稳定性和可用性，是生产环境部署的一大障碍。

*   **PR #50463 - 为未知工具提供更友好的错误提示** (创建于 2026-03-19)
    *   **链接**: [PR #50463](https://github.com/openclaw/openclaw/pull/50463)
    *   **影响**: 一个小的改动，但能极大改善新手用户和弱模型的使用体验，长期积压。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我将根据您提供的各项目动态摘要，为您生成一份横向对比分析报告。

---

### AI 智能体开源生态横向对比分析报告 (2026-06-26)

**核心洞察：** 当前个人 AI 智能体开源生态正经历从“功能竞赛”向“工程化与安全收敛”的剧烈转型。各项目普遍面临因快速迭代导致的稳定性、安全性与架构债务问题，社区反馈焦点已从“能做什么”转向“能否可靠地运行”。OpenClaw 凭借其庞大的社区规模和深厚的插件生态，依然是生态的核心参照系，但正深受“高积压低响应”的维护瓶颈困扰。而以安全与平台化为导向的项目（如 ZeroClaw、IronClaw）和专注于特定场景优化的项目（如 NanoBot、CoPaw），则代表了生态演进的两种不同路径。

---

#### 1. 生态全景

当前个人 AI 智能体开源生态呈现 **“繁荣与阵痛并存”** 的态势。一方面，社区贡献活跃，新功能和新应用场景（如实时语音、多代理协作）不断涌现；另一方面，多数主流项目均暴露出严重的稳定性隐患，包括内存泄漏、进程泄漏、会话状态混乱和高优先级的权限绕过漏洞。社区的声音高度集中在 **安全、可靠性和资源管理** 上，这标志着生态正从早期的“原型验证”阶段，正式迈入追求 **“生产就绪”** 的“工程化”阶段。各项目在修复架构迁移带来的兼容性问题的同时，也开始前瞻性地规划企业级特性，如供应链安全和细粒度权限策略。

#### 2. 各项目活跃度对比

| 项目名称 | Issues 活动 | PR 活动 | 版本发布 | 健康度评估 | 核心状态描述 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 极高 (1000条) | 极高 (406待处理) | 无 | 中等偏低 | **高产但严重积压，核心稳定性与安全性成疑** |
| **NanoBot** | 高 (高度安全相关) | 高 (40个PR) | 无 | 中等 | **安全审计期，维护者响应快，但漏洞密集** |
| **Hermes Agent** | 高 (50条) | 高 (50条) | 无 | 高 | **高活跃度，专注稳定性修复，Bug修复效率高** |
| **PicoClaw** | 中等 | 高 (19 PRs, 依赖为主) | 无 | 中等 | **代码质量改进期，但社区反馈和核心进展平淡** |
| **NanoClaw** | 中等 (1个热点) | 非常高 (16个PR) | 无 | **较高** | **交付能力强，功能与安全性并重，社区活跃** |
| **NullClaw** | 无 | 无 | 无 | - | **不活跃** |
| **IronClaw** | 极高 (50条) | 极高 (50条) | 无 | 中等 | **高强度开发中，平台化战略清晰，但Bug丛生** |
| **LobsterAI** | 低 | 中 (9个PR合并) | 无 | **较高** | **快速迭代与修复期，稳定性得到显著增强** |
| **TinyClaw** | 无 | 无 | 无 | - | **不活跃** |
| **Moltis** | 无 | 无 | 无 | - | **不活跃** |
| **CoPaw** | 极高 (27条) | 极高 (50条) | 无 | 中等 | **架构迁移阵痛期，Bug密度高，但修复响应迅速** |
| **ZeptoClaw** | 无 | 无 | 无 | - | **不活跃** |
| **ZeroClaw** | 高 | 极高 (高积压) | 冲刺中 | **较高** | **高强度发布冲刺，安全与架构是核心，积压严重** |

#### 3. OpenClaw 在生态中的定位

- **生态核心参照系**：OpenClaw 凭借其 **1000条** 的惊人月活跃问题量，无疑是生态中规模最大、社区最活跃的项目。它是创新功能（如本地实时语音）、插件生态（ClawHub）和社区技能多样性的主要策源地。
- **优势**：**品牌效应和社区网络效应**是其最大的护城河。任何新的功能或修复，在 OpenClaw 上测试和验证后，常常会扩散到其他衍生项目。
- **技术路线差异**：OpenClaw 倾向于提供 **“大而全”** 的解决方案，鼓励社区贡献，这使得它功能丰富，但也导致了复杂的依赖和较高的维护成本。
- **致命弱点**：**极高的积压率**（406个PR待处理）和 **对关键Bug响应的迟缓**（大量P1 Bug无关联Fix PR）是其最突出的问题。这导致其生产环境的可靠性受到严重质疑，用户信任正面临考验。
- **社区规模对比**：OpenClaw 的社区规模远超其他项目，其问题讨论的多样性体现了最广泛的用户需求，但也因此导致了维护者精力分散，无法聚焦。

#### 4. 共同关注的技术方向

- **安全模型（ZeroClaw, NanoBot, Hermes Agent, NanoClaw）：**
    - **具体诉求：** 严格、不可绕过的工具调用权限控制。
    - **代表案例：** ZeroClaw （`delegate`绕过父策略）、NanoBot （`exec`工具绕过）、NanoClaw （文件路径穿越修复）。

- **资源管理/泄漏（OpenClaw, CoPaw, ZeroClaw, IronClaw）：**
    - **具体诉求：** 解决长时间运行导致的内存泄漏、进程泄漏和会话文件无界增长。
    - **代表案例：** CoPaw （`browsers_use` Chrome进程泄漏）、ZeroClaw （MCP stdio子进程泄漏）、OpenClaw （Gateway内存泄漏、`sessions.json` 无界增长）、IronClaw （锁竞争优化）。

- **会话状态与上下文稳定性（OpenClaw, IronClaw, CoPaw）：**
    - **具体诉求：** 修复会话硬重置、数据丢失、消息重复、历史同步混乱等问题。
    - **代表案例：** OpenClaw（硬重置风暴）、IronClaw（批准后执行失败导致循环）、CoPaw（子代理历史同步重复）。

- **平台兼容性与适配（Hermes Agent, NanoBot, CoPaw, ZeroClaw）：**
    - **具体诉求：** 提升在Windows、Linux、不同IM平台（Telegram, Discord, 飞书）和特定LLM提供商（Kimi, Qwen）上的稳定性和功能完整性。
    - **代表案例：** NanoBot（Windows服务支持）、Hermes Agent（Telegram/Discord网关失联）、CoPaw（Linux浏览器兼容性问题）。

#### 5. 差异化定位分析

| 维度 | OpenClaw | ZeroClaw | NanoBot | Hermes Agent | CoPaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **核心定位** | **最大、最开放的通用Agent平台** | **企业级、安全优先的平台** | **轻量、注重安全的开发助手** | **注重生产就绪的稳定Agent** | **面向多模型、快速落地的Agent** |
| **目标用户** | 广泛开发者、社区贡献者 | 对安全合规、长期稳定运行有高要求的生产环境用户 | 开发者、对安全敏感的个人用户 | 追求稳定性和跨平台能力的团队和个人 | 需要快速集成多种模型（如Qwen）的团队 |
| **架构策略** | “大而全”，依赖社区生态（ClawHub） | 强调Wasm、硬件安全、供应链安全 | 轻量核心，安全审计驱动 | 稳健演进，专注于修复核心基础设施 | 快速适配AgentScope 2.0新架构 |
| **当前挑战** | **维护瓶颈，社区规模带来的质量失控风险** | **高积压使发布流程不畅，架构变革有阵痛** | **安全漏洞密集，有顾此失彼的风险** | **功能推进稳健，但无突出亮点** | **架构迁移带来大量兼容性问题** |

#### 6. 社区热度与成熟度

- **第一梯队（高活跃度，快速迭代）：OpenClaw, IronClaw, ZeroClaw, CoPaw**
    - 这些项目日处理Issue和PR数量均在两位数以上。OpenClaw 和 ZeroClaw 面临核心Bug积压和版本发布困难，**处于“高速迭代与债务积累并行”** 的阶段。IronClaw 和 CoPaw 则在修复大量Bug的同时，积极推动架构和平台化功能，**处于“阵痛转型期”**。

- **第二梯队（高交付，质量巩固期）：NanoClaw, LobsterAI, Hermes Agent**
    - 这些项目的PR合并率较高，且合并的PR多为直接针对报告Bug的Fix或成熟的功能增强。社区反馈与代码交付形成良好闭环，**处于“解决历史问题，提升质量”** 的阶段，项目健康度相对更高。

- **第三梯队（低活跃度）：PicoClaw, NanoBot, NullClaw, TinyClaw, Moltis, ZeptoClaw**
    - 这些项目近期活跃度低，或社区反馈主要停留在讨论层面，缺乏核心进展。例如PicoClaw的PR大部分是Dependabot的自动化更新。**处于“维护或停滞”** 状态。

- **特殊梯队：NanoBot**
    - 其活跃度虽高，但内容高度集中在安全问题上，更像是一次集中的、由社区驱动的 **“安全审计与修补”** 事件，而非普通的迭代开发。

#### 7. 值得关注的趋势信号

1.  **供应链安全成为刚需**：ZeroClaw 的硬件PGP和SLSA溯源提案，以及 NanoClaw 对订阅OAuth认证的优先支持，表明 AI Agent 作为可能持有用户敏感数据和API Key的基础软件，其供应链安全已从后端开发者延展至普通用户社区。这是一个重要的行业信号，预示着未来的Agent将和操作系统一样重视签名与验证。

2.  **“审批”交互机制被重新设计**：IronClaw 和 NanoClaw 的 Issue 与 PR 共同指向了“拒绝批准后的重试”、“多管理员审批”和“带理由的拒绝”。这表明简单的“Allow/Deny”二元审批已无法满足用户需求，**“有状态、可协商、高可用”的人机协作审批流** 将成为下一代Agent的核心交互范式。

3.  **Wasm作为一致性的插件运行时**：ZeroClaw 的“Wasm元年”计划，呼应了行业内对安全、可移植、跨语言插件的追求。如果成功，它将彻底改变目前 Agent 插件生态依赖特定语言（如Python, Go, Rust）和运行时的碎片化局面，为构建一个类似VS Code的“统一Agent插件市场”奠定基础。

4.  **从“记忆压缩”到“持久化上下文管理”**：CoPaw 的“滚动上下文管理器”PR（引入SQLite持久化和按需召回）是一个革命性思路，直接挑战了当前主流的“无限上下文窗口”或“暴力压缩”方案。这表明社区开始思考如何通过 **外挂式、持久化的记忆系统** 来彻底解决长会话和个性化记忆的难题。

5.  **开发体验的“去GUI化”趋势**：NanoClaw 的 “add-clidash”技能和 IronClaw 的自动化任务均指向了 **Agent与命令行、DevOps任务的深度融合**。这表明AI Agent正被越来越多地用于自动化运维、代码审查和数据报告生成等无需图形界面的“后台”场景，其价值评估维度正在从“对话流畅度”转向“任务完成率”。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 NanoBot 开源项目分析师，现将基于 2026-06-26 的 GitHub 数据生成项目动态日报如下。

---

### NanoBot 项目动态日报 | 2026-06-26

**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

今日 NanoBot 项目表现出 **高活跃度**，但核心焦点集中在 **安全议题** 上。过去 24 小时内，社区提交了 40 个 PR，其中 16 个已被合并或关闭，显示项目维护者响应迅速。然而，高达 9 个新开的 Issues 直接与安全漏洞相关（特别是 `exec` 工具和 MCP 配置的绕过问题），标志着项目正经历一次集中的 **安全审查与加固期**。尽管没有新版本发布，但修复安全漏洞的 PR 已迅速跟进，表明项目正从“功能推进”转向“安全收敛”阶段。社区贡献者 `YLChen-007` 成为今日最活跃的议题提交者，揭示了系统性的安全风险。

### 2. 版本发布

- **无新版本发布。**

### 3. 项目进展

今日合并/关闭了 16 个 PR，主要涉及安全修复、Bug 修复和部分功能增强。关键进展如下：

- **安全加固：** 成功修复了一系列安全漏洞。
    - **MCP 工具过滤绕过：** PR [#4524](https://github.com/HKUDS/nanobot/pull/4524) 已被合并（标记为 duplicate/fix），解决了 `enabledTools` 配置无法正确过滤资源和提示（Resources & Prompts）的问题。同时，Issues [#4519](https://github.com/HKUDS/nanobot/issues/4519), [#4517](https://github.com/HKUDS/nanobot/issues/4517), [#4434](https://github.com/HKUDS/nanobot/issues/4434), [#4435](https://github.com/HKUDS/nanobot/issues/4435) 均已关闭，表明此类绕过问题已获修复。
    - **文件系统读写权限：** PR [#4099](https://github.com/HKUDS/nanobot/pull/4099) 已被合并，修复了 `extra_allowed_dirs` 被错误地当作可写根目录的问题（Issue #4073），增强了文件系统工具的安全性。
    - **钉钉 (DingTalk) 适配器修复：** PR [#4493](https://github.com/HKUDS/nanobot/pull/4493) 已被合并，修复了钉钉适配器中的富文本格式支持和超时问题（Issue #4497）。

- **功能修复与体验优化：**
    - **上下文窗口修复：** Issue [#4242](https://github.com/HKUDS/nanobot/issues/4242) 被关闭，修复了禁用“梦境(Dream)”功能后，聊天历史仍被注入系统提示词的问题，这将更有效地控制模型上下文。
    - **WebUI 语音转录兼容性：** PR [#4493](https://github.com/HKUDS/nanobot/pull/4493) 解决了 WebUI 在使用小米 MiMo ASR 服务时，因音频格式不兼容导致的转录失败问题。

### 4. 社区热点

今日社区讨论的绝对焦点是 **安全**。贡献者 `YLChen-007` 提交了 9 个安全问题，涉及 `exec` 工具和 MCP 配置的多个绕过向量，引发了社区的广泛关注。

- **最热议题：** [#4518](https://github.com/HKUDS/nanobot/issues/4518) - `[Security] Default login-shell execution in `exec` reintroduces secrets from shell startup files`
  - **分析：** 此议题指出 `exec` 工具默认以 login shell 执行命令，会重新加载 `.bashrc` 等文件，可能暴露环境中的敏感密钥。这被认为是一个严重的隐私泄露风险，获得了 1 个 👍 和社区的高度关注。它暴露了安全策略与便捷性之间的典型冲突。
- **系统性安全报告：** 以 `YLChen-007` 为首，社区系统性地揭示了 `exec.allowPatterns` 配置的多个绕过方式（如通过 shell 命令链 `;`, `||` 绕过 #4514；通过注释尾缀绕过 #4515；通过包装工具前缀绕过 #4516），这表明社区正在进行深度的安全审计。

**社区诉求：** 社区强烈要求项目维护者重新设计 `exec` 工具的安全模型，从简单的“模式匹配”升级为更健壮的“命令解析与沙箱执行”机制，以彻底封堵绕过路径。

### 5. Bug 与稳定性

今日报告的 Bug 绝大多数为高危安全 Bug。按严重程度排列如下：

- **严重级别 (Critical):**
    - `exec` 工具存在系列安全绕过漏洞：
        - `allowPatterns` 可通过 shell 命令链绕过 (**#4514**)、注释后缀绕过 (**#4515**)、工具包装前缀绕过 (**#4516**)。**已有 fix PR #4526**。
        - 默认使用 login shell 执行，可能泄露密钥 (**#4518**)。
        - 通过 OpenAI 兼容 API 也能实现命令链绕过 (**#4520**)。
        - 以上问题均无 fix PR 提及。

- **高级别 (High):**
    - Windows 系统下，`--background` 后台模式与 `/restart` 命令协作异常 (**#4511**)。**无 fix PR**。
    - 使用 `nssm` 设置成系统服务后，`/restart` 命令导致端口占用或服务状态异常 (**#4513**)。**无 fix PR**。

- **低级别 (Low):**
    - Telegram Web 版本收到“不支持消息类型”的提示 (**#4488**)。**已关闭**，推测已修复。

### 6. 功能请求与路线图信号

今日用户提出的功能请求偏向于提升用户体验和系统鲁棒性：

- **PWA 与移动端体验：** 用户 `zpljd258` 提出了为 WebUI 添加 PWA 支持和移动端侧边栏手势滑动的功能（**#4479**），并提交了 PR **#4494**。该功能直接提升移动端体验，被采纳的可能性很高。
- **追问/澄清工具：** 用户 `ZhouJ-sh` 提出增加 `ask_clarification` 工具（**#4508**），允许 Agent 在收到模糊或高风险指令时，主动向用户提问确认。这是一个AI Agent设计中提升安全性和交互质量的关键特性。
- **子Agent增强：** 多项已提交并处于开放状态的 PR（如 #4414, #4415, #4416）正在推进子Agent的聚合结果模式、模型覆盖支持、定时任务预设等。这表明 **子Agent系统** 是当前版本迭代的重点方向之一。

### 7. 用户反馈摘要

- **主要痛点：安全配置复杂且易绕过。** `exec.allowPatterns` 配置项被证明是“纸老虎”，社区通过多个案例证明了其可以被轻易绕过。用户 `YLChen-007` 指出“该实现将任何匹配视为通过”，这反映了用户对于现存安全机制的不信任感。
- **体验问题：Windows 平台支持薄弱。** 用户 `Quincy-Zh` 详细描述了在 Windows 下使用后台模式和系统服务的具体缺陷，包括 `/restart` 后的端口冲突、状态不一致等问题。这表明项目在跨平台，尤其是 Windows 平台的稳定性和功能完整性上需要加强。
- **满意之处：** 钉钉（DingTalk）适配器问题被迅速定位并修复（#4497 → #4493），体现了维护者对特定平台用户反馈的响应速度。

### 8. 待处理积压

- **未响应的安全漏洞：** Issue **#4514**, **#4515**, **#4516** 和本文未列出的 #4520, #4521 等一系列 `exec` 工具绕过问题，虽然已有部分修复 PR（如 #4526），但尚未全部关闭。这些是最高优先级，需要官方尽快确认并发布修复版本。
- **Windows 稳定性 Bug：** Issue **#4511** (--background 问题) 和 **#4513** (nssm 服务问题) 已提交超过 24 小时，尚未获得官方回复或分配。这对于 Windows 用户的日常使用影响较大，建议维护者尽快分析。
- **长期未关闭的 Issue:** Issue **#143** (文件系统工具未强制执行 `restrict_to_workspace`) 创建于 2026-02-05，虽然在今日被标记为已关闭，但其存在时间长达数月，反映出某些安全策略的回溯性修复滞后。今天有类似的 #4073 被修复，但需要确认 **#143** 的修复是否彻底。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是为您生成的 **Hermes Agent 项目 2026-06-26 动态日报**。

---

# Hermes Agent 项目动态日报 | 2026-06-26

## 1. 今日速览

项目今日处于 **高活跃度** 状态，社区积极响应，社区与核心团队协作处理了多个 P1 级别问题，项目在“生产就绪”的稳定性轨道上持续迭代。核心亮点包括：
- **安全与稳定性并重**：社区修复了 Docker 环境下的符号链接递归权限问题 (`chown`) 以及 Windows 平台的子进程编码问题，提升了跨平台安全性。
- **核心功能修复**：解决了长期困扰用户的“推理模型思考超时”问题，避免了误触发上下文压缩导致的历史记录丢失。
- **平台鲁棒性加强**：修复了 Telegram 和 Discord 等平台网关的偶发“静默失联”问题，包括 TCP 连接保持与事件循环阻塞。
- **积压问题清理**：社区驱动的更新 (`hermes update`) 导致的桌面应用崩溃问题已在今天被彻底解决并关闭。
- **社区贡献热络**：今日共处理 50 条 Issue 和 50 条 PR，其中涌现了多个修复同类 Bug 的 PR，显示出社区对项目质量的高度投入。

## 2. 版本发布

**无**。 项目今日无新版本发布。

## 3. 项目进展 (重要 PR 合并与关闭)

今日项目在修复关键 Bug 和提升稳定性方面取得显著进展，多个高风险问题被成功关闭。

- **修复推理模型思考超时导致的误报与数据丢失**。 `#52272` (已合并) 和 `#52795` (已关闭) 解决了当 o1、DeepSeek R1 等推理模型因长时间思考导致连接超时时，系统错误地将原因归类为“上下文溢出”，从而触发压缩并删除历史对话的关键 Bug。现在超时会被正确识别，并给出更友好的操作指引。
- **修复桌面应用更新后因依赖缺失而崩溃**。 `#52764` (已关闭) 与 `#52735` (已关闭) 确认了 `hermes update` 在 `git pull` 增加新依赖后未正确打包的问题。相关修复 PR 正在审查中。
- **修复平台网关的稳定性问题**。 `#52197` (已关闭) 和 `#52761` (已关闭) 解决了 Discord 网关因代理缓存清理操作阻塞事件循环，导致心跳包丢失、机器人“掉线”的问题。 `#48495` (已关闭) 和 `#52744` (已关闭) 则修复了 Telegram 网关在长轮询模式下因 TCP 连接进入 `CLOSE-WAIT` 状态而“静默死机”的严重 Bug。
- **修复 Cron 任务调度器对部分任务丢失的恢复机制**。 `#52671` (已关闭) 改进了 `restore_cron_jobs_if_emptied` 逻辑，使其能检测并恢复部分任务丢失的情况，而不仅仅是全部丢失。此修复对依赖工具创建的 Cron 任务 (如桌面端调度程序) 的用户至关重要。

## 4. 社区热点

今日社区讨论集中在 **安全边界**、**跨平台体验** 和 **开发体验** 上。

1.  **#2626 (OPEN): [Feature]: credential proxy daemon** **评论：11**
    - **诉求**: 这是对安全性的深度讨论 (由 pr #30179 推进)。社区期望一个零知识的 HTTP/HTTPS 代理，将凭证管理从 Agent 隔离出来，即使在沙箱被攻破的情况下也能保护 API Key。这反映了社区对更高级别生产环境安全的迫切需求。
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/4656

2.  **#38240 (OPEN): [Bug]: Skills index is stale or degraded** **评论：12**
    - **诉求**: 自动化健康检查模块持续报警，Skiill 索引文件 (skills-index.json) 无法正常构建 (至少需要 30 个技能，当前为 0)。虽然这是一个核心基础设施问题，但开发者可能已习以为常，导致其长期 open。这是项目文档和技能生态的健康度红灯。
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/38240

3.  **#52735 (CLOSED): [Bug]: Desktop app crashes on launch** **评论：9**
    - **诉求**: 一个因更新导致的严重问题，影响了大量 Windows 和桌面用户。用户遭遇应用立即崩溃，反馈非常积极，迅速升级为 P1 并关闭。这突显了桌面客户端自动更新机制的脆弱性，是用户活跃度和问题响应速度的证明。
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/52735

## 5. Bug 与稳定性

今日报告的 Bug 集中在 **平台兼容性**、**核心数据处理** 和 **安全性** 方面。

| 严重程度 | 问题标题 (Issue #) | 状态 | 描述 |
| :--- | :--- | :--- | :--- |
| **P1** | Docker symlinked chown (pr #52789) | **已有 Fix PR** | Docker 阶段2的所有权修复 (`chown`) 会跟随符号链接递归，可能将 `$HERMES_HOME` 意外地指向并修改系统级文件，存在安全风险。 |
| **P1** | Docker 终端路径泄漏 (pr #48137) | 已关闭 | Windows 原生 Docker 后端会向 Linux 容器暴露完整的 Windows 路径，导致挂载异常。 |
| **P2** | Feishu 表格降级为纯文本 (#52786) | **新开/Duplicate** | 飞书适配器将所有 Markdown 表格降级为纯文本，破坏了排版功能。此 Issue 被标记为重复，但说明用户反馈集中。 |
| **P2** | Nix 构建失败 (#43810) | OPEN | `extraPythonPackages` 选项与已存在的依赖包冲突会导致构建硬失败，阻碍 NixOS 用户使用插件。 |
| **P3** | 技能存档器误归档活跃技能 (#29912) | OPEN | `curator` 在自动合并技能时，可能将正在被功能依赖的关键技能归档，导致功能不可用。 |

## 6. 功能请求与路线图信号

社区对新功能的需求主要集中在 **平台体验增强** 和 **开发者工具链** 上。

- **高优先级信号**：`##39691` **工具输出压缩** (评论: 8, 👍: 10): 对比现有对话级压缩，社区强烈需求在工具 (Tool) 层面进行压缩，以减少 Token 消耗并提升 Agent 在复杂任务中的性能。这是对 Agent 效率的核心优化请求，很可能被纳入下个小版本。
- **平台集成**：`#8552` **Slack Block Kit 支持** (评论: 8, 👍: 9) 和 `#44428` **Telegram 10.1 富消息支持** (评论: 7): 用户期望 Agent 在聊天平台上的展示效果更好，尤其是支持 Markdown 表格等富文本格式。`#27922` (OPEN) 和 `#52790` (OPEN) 已开始对飞书和通用 Markdown 表格进行支持，此路线图信号清晰。
- **国际化**：`#52137` **俄语本地化** (评论: 5): 继法语、中文、葡萄牙语后，俄语本地化请求出现，表明社区对多语言 UI 的强烈且持续的需求。

## 7. 用户反馈摘要

- **桌面更新体验**：用户 `louquillio`, `kroehrs` 在 issue #52764, #52735 中描述了因 `hermes update` 导致应用崩溃的痛苦经历。这暴露了 `git pull` + 打包流程的缺陷，用户期望更稳健的自动更新机制。
- **网关稳定性焦虑**：用户在 `#48495` 和 `#52197` 中描述了 Telegram/Discord 机器人“静默死机”的状态，这是一种最令人困惑的体验——服务仍在运行，但已无法接收消息。此系列修复将大幅提升用户对长连接稳定性的信心。
- **配置/数据持久化困惑**：用户 `Freffles` 在 issue `#48248` 中指出 `billing_provider` 等配置在会话中写入一次后无法修改，导致中途切换模型后仪表盘显示不匹配。这反映了用户对配置动态修改和状态一致性的需求。
- **对安全性的关注**：高级用户 (如 dsr-restyn) 在 issue `#4656` 中深入讨论了通过凭证代理来隔离凭证，反映了生产环境中对“零信任”架构的追求。

## 8. 待处理积压

- **#38240 - Skills Index is stale or degraded** (P3, 12 comments, open for 23 days)：核心文档/技能索引构建失败，影响新用户和文档访问。虽然是一个已知问题，但作为基础设施问题，建议提升优先级，否则将长期影响项目生态感知。
- **#28004 - Telegram typing indicator stuck** (P2, 6 comments, open for 39 days)：虽然 P2，但会影响用户体验的细腻度。`_keep_typing` 循环的竞态条件修复似乎因复杂而延迟。
- **#29912 - Curator may archive active skills** (P1, 7 comments, open for 36 days)：这是一个 P1 级别的功能风险，可能导致技能库不可用。至今无明确的修复 PR，可能需要维护者介入协调。
- **#46260 - Windows installer fails** (P2, 7 comments, open for 12 days)：Windows 安装问题，虽然已有用户 AI 辅助分析，但无 PR 关联，可能因定位困难而卡住。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的PicoClaw项目GitHub数据，现生成2026年6月26日的项目动态日报。

---

## PicoClaw 项目动态日报 | 2026年6月26日

### 1. 今日速览

今日项目整体**活跃度较高**，社区贡献与维护者修复活动并行。**Pull Request 提交量（19条）显著增长**，但大部分为依赖项自动更新（Dependabot）请求。核心团队的修复工作集中在**稳定性与代码健壮性**上，合入了多项针对错误处理、资源泄露和日志的修复。社区讨论热度集中在**将libolm替换为vodozemac**（#3088）这一安全相关的功能请求上，显示出用户对依赖安全性的关注。新版本发布方面处于停滞状态，当前版本（v0.2.9之后）仍在构建中。

### 3. 项目进展

今日共有 **6 个 PR 被合并或关闭**，主要推进了以下改进：

- **运行稳定性修复**
    - **[PR #3169] fix(evolution): skip cold path for heartbeat turns**：修复了当“演化”功能开启时，定时心跳检查会错误触发冷路径，导致不必要的token消耗的问题。这是对**Issue #3012**中报告的“token持续消耗”问题的直接修复。作者: Alix-007.
    - **[PR #3168] fix(model): handle error response read failures**：改进OpenAI兼容模型列表获取失败时的错误处理，当读取非200响应的错误体失败时，返回具体的读取错误信息，而非空或误导性的HTTP错误。作者: Alix-007.
    - **[PR #3166] fix(openai_compat): use structured logger for native_search warning**：修复`openai_compat`包中一处未定义`log`的构建失败问题，使用项目已有的结构化日志替代`log.Printf`，提升了代码质量。作者: Alix-007.

- **代码健壮性修复**
    - **[PR #3092] fix(skills_install): add ok checks for version and force type assertions**：为技能安装过程中的类型断言增加了`ok`检查，防止因非预期类型值导致的静默失败和令人困惑的用户体验。作者: chengzhichao-xydt.
    - **[PR #3045] fix(identity): allow_from fallthrough for Matrix user IDs with colon**：修复了Matrix频道中，标准用户ID（如`@alice:example.com`）因解析逻辑缺陷而被`allow_from`配置错误拒绝的问题。作者: chengzhichao-xydt.

### 4. 社区热点

- **热度最高：安全问题与架构升级讨论**
    - **[Issue #3088] [Feature] use vodozemac instead of libolm** ([链接](sipeed/picoclaw Issue #3088))
        - **状态**: OPEN / **评论数**: 3 / **👍**: 2
        - **分析**: 这是今日社区反馈最强烈的单一议题。用户`pbsds`提出将已无人维护且不安全的`libolm`替换为其官方替代品`vodozemac`，并获得了2个👍。这表明项目社区对基础安全依赖非常敏感，且倾向于采用官方推荐的现代化解决方案。该议题虽然创建于6月9日，但热度持续，是社区希望项目推进的重要信号。

- **活跃修复讨论：Token消耗问题**
    - **[Issue #3012] [BUG] Continuous consumption of tokens every minutes when evolution is enabled** ([链接](sipeed/picoclaw Issue #3012))
        - **状态**: **今日已关闭** / **评论数**: 5
        - **分析**: 该Bug在关闭前获得了5条评论，说明问题确实影响了用户。其修复PR **[#3169]** 在今天被合并，这是一个非常积极的信号，表明项目从用户报告问题到修复关闭的周期效率较高。

### 5. Bug 与稳定性

今日没有报告新的严重Bug。主要关注点在于 **“稳定性修复”**组件的合入，这通常意味着项目正从面对Bug到进行内部质量优化的阶段转变。

- **已修复并关闭（严重程度：中等）**
    1. **Token持续消耗**：`evolution`功能开启后，心跳检查导致每分钟消耗token。 (#3012) -> **[FIX PR #3169] 今日已合并**
    2. **构建失败**：`openai_compat`包中存在未定义的`log`变量导致无法编译。 -> **[FIX PR #3166] 今日已合并**
    3. **身份验证失效**：Matrix频道用户因ID格式问题被`allow_from`错误拒绝。 -> **[FIX PR #3045] 今日已合并**
- **已提交修复（审查中）**
    - 资源泄露：`agent`进程中`base64 encoder`在`io.Copy`失败后未关闭，可能导致缓冲区泄漏。 -> **[PR #3170] 待合并**
    - 潜在Panic：LINE频道`Send`方法中，`sync.Map`类型断言缺少`ok`检查，有潜在panic风险。 -> **[PR #3171] 待合并**

### 6. 功能请求与路线图信号

- **高优先级信号：安全依赖升级**
    - **[Issue #3088] 替换 libolm 为 vodozemac**：这是一个明确且重要的**安全性与技术债务**相关功能请求。虽然PR#3088本身是Issue，但尚未有对应PR。然而，`dependabot`今日发起了多个Go依赖升级的PR，表明项目正在主动进行依赖管理。但直接替换核心加解密库是一项重大变更，可能会被纳入下一个**次要版本或大版本规划**中。

- **新功能扩展：新通信渠道与远程模式**
    - **[PR #3063] feat: add deltachat gateway** ([链接](sipeed/picoclaw PR #3063))：目前仍为OPEN状态，添加DeltaChat作为新的通信渠道，显示了PicoClaw向去中心化通信生态扩展的意图。
    - **[PR #3118] Add remote Pico WebSocket mode** ([链接](sipeed/picoclaw PR #3118))：提供`agent`命令的远程模式，允许通过WebSocket连接。这是一个重要的架构功能，支持开发者将PicoClaw作为远程服务调用。

### 7. 用户反馈摘要

- **痛点**：
    - 有用户在`evolution`模式下遇到了**高昂且不必要的Token消耗**，影响低预算或长时间运行的用户体验。（#3012）
    - 用户`dhensen`报告了一个关于**定时任务Cron触发渠道错误**的问题，但该问题似乎最终被标记为过期并关闭，可能未完全解决或用户未提供足够信息。（#1757）
- **使用场景**：
    - 用户`dhensen`使用PicoClaw在**Raspberry Pi Zero**上运行，连接**Telegram**，并尝试创建**定时任务**。这展示了PicoClaw在低功耗边缘设备上的实际部署场景。
- **期望**：
    - 社区明确希望项目**采用更现代、更安全的底层依赖**，如`vodozemac`，显示出用户对项目长期健康度的关注超过了对新功能的急迫需求。（#3088）

### 8. 待处理积压

- **核心功能请求待响应**：
    - **[Issue #3088] 替换 libolm 为 vodozemac** ([链接](sipeed/picoclaw Issue #3088))：已获得社区关注并标记为`priority: high`，但尚无PMC或核心贡献者的正式回复或PR关联。维护者应考虑给出接受/拒绝的明确答复或路线图规划，以回应社区关切。

- **长期未审查的 PR**：
    - **[PR #3063] feat: add deltachat gateway** ([链接](sipeed/picoclaw PR #3063))：自6月8日起已开放超过两周，目前无审查进展。虽然DeltaChat用户群可能较小，但作为新渠道功能，长时间未处理会被社区视为对社区贡献不够重视的信号。
    - **[PR #3118] Add remote Pico WebSocket mode** ([链接](sipeed/picoclaw PR #3118))：自6月12日起开放，目前也无审查进展。这个PR提供了对开发者非常有用的远程调用能力，停滞可能阻碍有远程调用需求的用户参与贡献。

---

**分析师总结**：今日项目展示了强大的**内部代码质量改进**驱动力，通过修复一系列Bug和进行依赖升级来提升稳定性。社区的声音集中在**安全与依赖管理**上，这是一个良性信号。然而，**待合并的14个PR（包括2个重要功能请求和多个Dependabot更新）** 形成了一个小瓶颈，需尽快审查和合并，特别是`vodozemac`替换和远程模式这两个能显著提升项目号召力的贡献。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 GitHub 数据生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-26

## 1. 今日速览

NanoClaw 项目今日整体活跃度**极高**，尤其是在代码合并与功能交付方面。过去24小时内，项目共处理了16个 Pull Request，其中11个已被合并或关闭，显示出强大的交付能力。社区贡献者的参与度显著，多个由社区提交的重要 Bug 修复和功能（如权限设置、容器资源限制）被合并入主分支。然而，待合并 PR 仍有5个，主要集中在日志优化和架构迁移修复等细节打磨上，表明项目在快速迭代中兼顾了代码质量。此外，一个关于审批权限支持多管理员的 Issue 引发了讨论，反映了用户对工具灵活性和可用性的深层需求。

## 2. 版本发布

**无**。过去24小时内无新版本发布。

## 3. 项目进展

今日项目进展显著，核心围绕着 **功能增强、稳定性修复和安全性加固** 三大主线。共11个 PR 被成功合并，以下是关键进展：

- **审批机制增强**：PR #2832 正式合并，引入了“带理由的拒绝”功能。现在用户在拒绝审批时，可以附加简短说明，帮助 Agent 理解拒绝原因并调整策略，从而提升了人机协作的效率。
  - [PR #2832](nanocoai/nanoclaw PR #2832)

- **容器资源管理**：PR #2856 合并，新增了可选的 CPU 和内存限制功能。通过设置 `CONTAINER_CPU_LIMIT` 和 `CONTAINER_MEMORY_LIMIT` 环境变量，可以防止单个 Agent 容器占用过多宿主机资源，这对于多 Agent 部署场景至关重要。
  - [PR #2856](nanocoai/nanoclaw PR #2856)

- **认证与安全性**：
    - PR #2855 合并，实现了订阅优先的认证策略。系统将优先使用 Claude 订阅的 OAuth 认证，并在失败时自动回退至 API 密钥，同时向管理员发出告警，提升了系统的健壮性和可用性。
    - PR #2817 合并，是一个重要的安全修复。它强制限制了 `send_file` 功能的文件读取范围只能在工作空间（workspace）内，并增加了对符号链接（symlinks）的检查，有效防止了路径穿越攻击。
  - [PR #2855](nanocoai/nanoclaw PR #2855)
  - [PR #2817](nanocoai/nanoclaw PR #2817)

- **聊天体验与架构优化**：
    - PR #2472 和 PR #2471 合并，为 Slack 集成带来了“每条消息独立线程”的模式。现在在 Slack 私聊中，每一条顶级消息都可以开启一个独立会话，解决了之前所有消息挤在同一个会话中的混乱问题。
    - PR #2830 合并，修复了一个服务注册的“僵尸”问题。当删除 NanoClaw 项目目录而未运行卸载脚本时，系统会自动清理掉对应的注册服务，避免了后台进程的累积。
  - [PR #2472](nanocoai/nanoclaw PR #2472)
  - [PR #2471](nanocoai/nanoclaw PR #2471)
  - [PR #2830](nanocoai/nanoclaw PR #2830)

- **新技能与工具**：
    - PR #2843 合并，新增 `/learn` 技能。该技能可以从任意来源（如目录、URL、粘贴文本）提炼并生成一个可复用的 Skill，极大地简化了用户的技能创建流程。
  - [PR #2843](nanocoai/nanoclaw PR #2843)

## 4. 社区热点

今日社区讨论热度最高的是 **#2857** 号 Issue。该 Issue 提出当前审批功能只能请求单一管理员，如果该管理员不可用，审批流程将陷入僵局。用户建议让 Agent 能够重新请求其他管理员，或允许拥有机器访问权限的管理员通过 CLI 直接批准。这反映了在团队协作场景下，用户对审批流程**灵活性和高可用性**的强烈诉求。虽然该 Issue 尚未有明确的 PR 响应，但它与今日合并的“带理由的拒绝”功能（PR #2832）共同指向了未来审批模块的演进方向。
  - [Issue #2857](nanocoai/nanoclaw Issue #2857)

## 5. Bug 与稳定性

今日未有新 Bug 报告。当前合并的 PR 主要修复了以下几个关键的稳定性与兼容性问题：

- **严重**：PR #2859 修复了数据迁移脚本在早期版本（v1.1.0）上运行会因缺失 `is_main` 列而崩溃的 Bug，这可能导致全新的 v2 数据库无法创建，属于严重的**数据迁移兼容性问题**。
  - [PR #2859](nanocoai/nanoclaw PR #2859)

- **中等**：PR #2854 修复了 macOS 环境下因临时目录路径问题导致的 **Agent 无法连接到 API** 的错误。该问题在特定容器运行时（如 Rancher Desktop）上频繁出现。
  - [PR #2854](nanocoai/nanoclaw PR #2854)

- **中等**：PR #2813 修复了 CLI 中 **Socket 响应计数不准确**的问题，特别是当响应包含多字节 UTF-8 字符时，旧的基于字符数的限制可能失效。
  - [PR #2813](nanocoai/nanoclaw PR #2813)

## 6. 功能请求与路线图信号

- **审批流程的高可用性**：Issue #2857 提出的“审批支持多管理员”请求，与 PR #2832（带理由的拒绝）结合，构成了审批模块未来的完整规划。预计在后续版本中，将看到 Agent 能自动寻路到下一个可用管理员的功能。
  - [Issue #2857](nanocoai/nanoclaw Issue #2857)

- **CLI 衍生工具**：PR #2858 是对 PR #2795 的修复和跟进，后者提出了“`/add-clidash`”技能，可以从 CLI 实时数据生成仪表盘。这显示社区正积极探索将 NanoClaw 的 Agent 能力与系统运维工具深度结合。
  - [PR #2858](nanocoai/nanoclaw PR #2858)
  - [PR #2795](nanocoai/nanoclaw PR #2795)

## 7. 用户反馈摘要

本次日报周期内，直接的用户反馈主要源于 Issue #2857。其核心痛点是：
- **单点故障**：当唯一的审批人（Admin）不在线时，Agent 无法继续工作，导致流程阻塞。
- **操作不便利**：希望通过 CLI 等方式直接审批，而非必须通过消息卡片，满足 “有机器访问权限” 管理员的批量化、自动化操作需求。

## 8. 待处理积压

以下 PR 已开启一段时间但尚未合并，建议维护团队予以关注：

1.  **#2824 [OPEN] fix: 删除主提示词中的“全局记忆”指令** - 创建于6月20日，状态停滞。该 PR 旨在清理 Agent 核心提示词中过时的指令，可能影响 Agent 的响应行为。尽管作者标注了 `follows-guidelines`，但未能获得足够关注进行合并。
  - [PR #2824](nanocoai/nanoclaw PR #2824)

2.  **#2795 [OPEN] feat: 添加 `/add-clidash` 技能** - 创建于6月17日，有替代 PR #2858。维护者需要决定是合并这个原始 PR 还是新的修复版本，以确保社区贡献的连续性。
  - [PR #2795](nanocoai/nanoclaw PR #2795)

---
*生成时间: 2026-06-26 | 数据来源: github.com/qwibitai/nanoclaw*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据您提供的 IronClaw 项目 GitHub 数据生成的 2026 年 6 月 26 日项目动态日报。

---

### IronClaw 项目动态日报 — 2026-06-26

**项目名称:** IronClaw (github.com/nearai/ironclaw)
**分析日期:** 2026-06-26
**分析师:** AI 开源项目分析师

---

### 1. 今日速览

截至 2026 年 6 月 26 日，IronClaw 项目活动**极其活跃**。过去 24 小时内，项目产生了 50 条 Issue 和 50 条 PR，显示出社区和核心团队的高强度贡献。虽然无新版本发布，但项目在 **Reborn 平台**的**【策略与政策】 (Policy) 体系**、**内存管理**以及**基础设施稳定性**方面取得了显著进展。**“Rejection of Denial”**、**“Always approve” 失效**和**自动化运行挂起**是当前最令人关注的 Bug 集群，直接影响了用户体验和自动化系统的可靠性。此外，一个涉及 47 个依赖项更新的批量 PR 也预示着底层技术栈的持续演进。

### 2. 版本发布

*无*

### 3. 项目进展 — 重大功能推进

今天，项目在稳定性与核心功能落地上迈出了关键几步，多份大型 PR 已完成合并或处于深度审查阶段。

- **稳定性与基础设施修复:**
    - **PR #5281 (OPEN)**：由核心贡献者发起，旨在修复 CI 管道中的系统性失败和“伪”不稳定测试，以解除 `main` 分支的阻塞状态。这是保障其他开发工作顺畅进行的基础。
    - **PR #5255 (CLOSED)**：优化了文件系统 CAS `put` 操作的数据库往返次数，从 3 次降低到 1 次，显著提升了写入性能与效率。 *[链接](https://github.com/nearai/ironclaw/pull/5255)*
    - **PR #5234 (OPEN)**：移除了持久化存储层中不必要的每记录 `tokio::sync::Mutex`，以解决高并发下的锁竞争问题。 *[链接](https://github.com/nearai/ironclaw/pull/5234)*

- **Reborn 平台的“政策”体系落地:**
    - **PR #5277 (OPEN)**：实现了用户在平台层面“可用性” (Availability) 的解析器（对应 Issue #5267）。这是构建细粒度、基于角色的能力和工具权限控制体系的关键一环。 *[链接](https://github.com/nearai/ironclaw/pull/5277)*
    - **PR #5270 (OPEN)**：引入了数据库支持的用户角色体系 (`Owner > Admin > Member`) 及 WebChat-v2 的管理员门控，为管理员管理用户权限提供了基础框架。 *[链接](https://github.com/nearai/ironclaw/pull/5270)*
    - **PR #5247 (OPEN)**：在批准 UI 卡片中添加了指向“设置-工具”全局自动批准的入口，提升了用户发现和配置全局权限的易用性。 *[链接](https://github.com/nearai/ironclaw/pull/5247)*

- **内存系统与外设支持:**
    - **PR #5205 (OPEN)**：作为实现 #3537 的核心 PR，将模型内存重构为用户态扩展。该 PR 引入了**扩展清单 V2**、**源感知信任机制**和**本地文档存储**支持，是 Reborn 平台内存能力的一次深刻重构。 *[链接](https://github.com/nearai/ironclaw/pull/5205)*
    - **PR #4997 (CLOSED)**：为 `download_file` 工具增加了从 PDF、PPTX、DOCX、XLSX 等二进制文件中提取文本内容的能力，显著扩展了 Agent 处理实际工作文档的能力。 *[链接](https://github.com/nearai/ironclaw/pull/4997)*

### 4. 社区热点 — 高讨论度 Issue 与 PR

今日讨论焦点集中在**工具权限管理**和**自动化系统的可靠性**上，这些直接关系到核心用户体验。

- **#5192 [OPEN]：「批准拒绝」后仍会触发更多批准请求**
    - **分析**: 用户 `sunglow666` 报告了一个违反直觉的行为：当用户拒绝一个工具调用后，系统可能继续请求批准其他工具。这表明批准机制在处理被拒绝后的流程上存在缺陷，可能导致循环或无限等待，用户体验极差。
    - **链接**: [Issue #5192](https://github.com/nearai/ironclaw/Issue/5192)

- **#5276 [OPEN]：计划自动化任务失败——「未绑定线程」**
    - **分析**: 一个名为“Daily IronClaw PR Digest”的自动化任务持续以 0% 成功率运行失败。错误信息“No thread attached”表明系统在计划任务执行时未能成功创建或关联一个会话线程，导致运行记录孤立无输出。这是自动化系统的一个严重稳定性问题。
    - **链接**: [Issue #5276](https://github.com/nearai/ironclaw/Issue/5276)

- **#5242 [CLOSED]：本地 WebUI 用户查看工具页面时出现权限错误**
    - **分析**: Issue #5242 报告了一个基础但严重的问题：普通 WebUI 用户无法访问“设置 -> 工具”页面，并看到“Operater-only”的错误。这直接影响了用户手动管理工具权限的能力，是用户“开箱即用”体验的一个重要障碍。
    - **链接**: [Issue #5242](https://github.com/nearai/ironclaw/Issue/5242)

- **#5196 [OPEN]：“每次都询问”权限模式下，授权错误导致重复审批**
    - **分析**: 报告了一种“死循环”式体验：用户在“每次都询问”模式下批准工具后，工具执行失败并返回“授权错误”，随后系统再次请求授权。这导致用户陷入“批准-失败-再批准”的循环中，核心问题是工具执行流水线与授权状态管理之间存在脱节。
    - **链接**: [Issue #5196](https://github.com/nearai/ironclaw/Issue/5196)

### 5. Bug 与稳定性 — 按严重程度排序

本周 Bug 报告密集，主要集中在 Reborn 平台的交互与功能缺陷上。

| 严重程度 | Bug 描述 | Issue | 关联 Fix PR |
| :--- | :--- | :--- | :--- |
| **严重** | 自动化任务 (`Daily IronClaw PR Digest`) 100% 执行失败，错误“No thread attached”。 | [#5276](https://github.com/nearai/ironclaw/Issue/5276) | 无 |
| **严重** | 拒绝批准后，系统仍可能发起新的批准请求。 | [#5192](https://github.com/nearai/ironclaw/Issue/5192) | 无 |
| **中** | “Approve &alway allow” 功能不生效，权限无法持久化到设置。 | [#5243](https://github.com/nearai/ironclaw/Issue/5243) | 无 |
| **中** | “Ask each time” 模式下的批准后执行失败，导致重复请求授权。 | [#5196](https://github.com/nearai/ironclaw/Issue/5196) | 无 |
| **中** | 批准门打开时发送新消息，导致警告和消息状态丢失。 | [#5210](https://github.com/nearai/ironclaw/Issue/5210) | 无 |
| **低** | 输入框在等待 Agent 响应时冻结，无法输入新的消息。 | [#5208](https://github.com/nearai/ironclaw/Issue/5208) | 无 |
| **低** | 新生成的流式响应不会自动滚动到可视区域。 | [#5211](https://github.com/nearai/ironclaw/Issue/5211) | 无 |
| **低** | 内部 skill 激活/预算调试消息暴露在聊天 UI 中。 | [#5191](https://github.com/nearai/ironclaw/Issue/5191) | 无 |
| **低** | 日志页面无法滚动，导致超出屏幕的日志不可见。 | - | [#5278](https://github.com/nearai/ironclaw/PR/5278) (已修复) |
| **低** | “日志”链接HTML路径错误，导致404。 | - | [#5275](https://github.com/nearai/ironclaw/PR/5275) (已修复) |

### 6. 功能请求与路线图信号

今日 Issue 揭示了项目中正在进行的两项重大战略方向性功能开发：

- **“Capability Policy” 管理与多用户体系:**
    - **讯号**: #5261 系列及其子 Issue (#5274, #5272, #5266, #5268 等) 明确指向了建立一套完整的、面向企业的能力和工具权限管理框架。
    - **分析**: 功能包括：`Admin REST 管理接口`、`可用性解析器`、`四维策略`（配置、身份、审批、可用性）、`多用户本地认证`以及`角色化管理`。这些都是“平台化”、“企业级”产品的关键垫脚石，极有可能会集成在下一个大版本中。

- **“Personal Memory & Self-Learning” 系统:**
    - **讯号**: #5260 与 #5264 详细描述了 Reborn 平台的个人记忆与自学习系统蓝图。
    - **分析**: 系统目标包括：可靠的记忆提取、安全的作用域管理、过期和自策展机制。计划支持原生 SQL 存储后台和第三方集成。核心 PR #5205 已经落地了扩展清单 V2 等基础架构，表明该项目已进入具体实施阶段，是 Reborn 平台区别于其他 AI Agent 的核心竞争力。

### 7. 用户反馈摘要

从今日的 Issues 中可以清晰感受到用户在做“Dogfooding”（内部产品试用）时遭遇的 **挫折感**：

- **“批准”流程的混乱**：用户（`sunglow666`）多次报告“Approval”相关的失败、重复和未预期行为。核心痛点在于“我批准了，但工具却没执行”、“我拒绝了，但它又在请求”以及“我说了始终允许，但你忘了”。这表明审批机制的**确定性和可预期性**是当前用户体验的最大短板。
- **“自动化”系统的不可靠**：用户 `loopstring` 报告了一个计划任务 **100% 失败** 的严重问题。虽然该用户可能是开发者，但此类问题会严重侵蚀用户对“自动化”这个核心功能的信任。
- **新用户“开箱即用”体验不佳**：问题 #5242（普通用户无法查看工具设置）和 #4980（空态无引导）表明，对于刚接触 Reborn平台的新用户，缺乏明确的引导和清晰的界面来理解和配置其能力边界。

### 8. 待处理积压

以下 Issue/PR 已经存在一段时间或至关重要，值得维护者关注：

1.  **[严重] Issue #5192**:
    - **内容**: 拒绝批准后仍会触发新的批准请求。
    - **重要性**: 极高，严重影响审批流程的可靠性和用户对系统的信任。
    - **链接**: [Issue #5192](https://github.com/nearai/ironclaw/Issue/5192)

2.  **[严重] Issue #5276**:
    - **内容**: 计划自动化任务 0% 成功率。
    - **重要性**: 极高，直接关涉核心自动化功能，需立即排查。
    - **链接**: [Issue #5276](https://github.com/nearai/ironclaw/Issue/5276)

3.  **[中] Issue #5219**:
    - **内容**: 在 `Gate` 生命周期重构后，强化 `Activity Identity` 一致性保障。
    - **重要性**: 中，虽为后续工作，但关乎数据一致性和日志审计的准确性，是一个架构性的持久化任务。
    - **链接**: [Issue #5219](https://github.com/nearai/ironclaw/Issue/5219)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI 项目数据，我已生成以下项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-06-26

## 1. 今日速览

- **整体活跃度评估：较高。** 项目在过去24小时内完成了9个Pull Request的合并/关闭，展现了强大的开发与维护节奏。这些PR主要集中于 `OpenClaw` 框架的稳定性修复、 `Cowork` 协作模式的体验优化，以及设置与构建层面的加固。
- 尽管没有新版本发布，但项目团队正在密集解决近期报告的问题，包括定时任务开关的Bug，这表明项目正处于一个积极的“快速迭代与修复周期”。
- 社区层面相对平静，主要贡献来自核心开发团队，反映了项目当前处于内部驱动开发的阶段。

## 2. 版本发布

- **无。**

## 3. 项目进展

今日合并的9个PR显示了项目在多个关键领域的进展：

- **OpenClaw 框架稳定性与集成（核心）：** 这是今日修复的重点。多个PR协同工作，旨在提升 `OpenClaw` 扩展与插件的健壮性。
    - **扩展加载修复：** PR [#2203](https://github.com/netease-youdao/LobsterAI/pull/2203) 修复了预编译本地扩展条目问题，确保本地 `ask-user` 和 `media` 扩展能被正确加载。
    - **插件白名单管理：** PR [#2202](https://github.com/netease-youdao/LobsterAI/pull/2202) 将浏览器插件纳入 `OpenClaw` 管理白名单，防止在严格配置下浏览器控制功能失效。
    - **子代理状态同步：** PR [#2201](https://github.com/netease-youdao/LobsterAI/pull/2201) 修复了在 `sessions_yield` 后，主会话与子代理会话（subagent）历史同步中的信息去重问题，避免了GLM看到重复的回复。PR [#2199](https://github.com/netease-youdao/LobsterAI/pull/2199) 则修复了父会话结束后，对仍在运行的子代理会话的轮询机制，确保状态更新不丢失。
    - **渠道插件预装：** PR [#2198](https://github.com/netease-youdao/LobsterAI/pull/2198) 预装了 `OpenClaw` 官方的 QQ 和 Discord 频道插件，并修复了相关环境变量索引问题，简化了用户多平台配置流程。
- **Cowork 协作模式体验优化：**
    - **计划模式图标更新：** PR [#2205](https://github.com/netease-youdao/LobsterAI/pull/2205) 使用主题感知的SVG组件替换了计划模式的图标，提升了UI一致性。
    - **计划标签解析修复：** PR [#2204](https://github.com/netease-youdao/LobsterAI/pull/2204) 修复了计划标签（`proposed_plan tags`）的解析逻辑，优先处理块级标签，避免标签泄露到消息中。
    - **流式响应抖动处理：** PR [#2200](https://github.com/netease-youdao/LobsterAI/pull/2200) 通过将微小的长度倒退视为流抖动而非新片段，解决了Qwen等模型在计划模式下可能产生重复消息的问题。
- **设置与系统集成加固：**
    - **开机自启同步修复：** PR [#2206](https://github.com/netease-youdao/LobsterAI/pull/2206) 修复了“开机自启”设置与操作系统状态不同步的问题，并增加了诊断日志和本地化错误提示。

**项目向前迈进总结：** 今日的PR显著提升了 `OpenClaw` 框架的可靠性和插件生态的完整性，同时优化了多代理协作（Cowork）场景下的用户体验。这些修复属于“修桥补路”型工作，虽然不引人注目，但对提升项目底层的稳定性和扩展性至关重要。

## 4. 社区热点

- **今日最受关注 Issue：[#1392](https://github.com/netease-youdao/LobsterAI/issues/1392) “定时任务开关点击无反应，无法关闭”**
  - **讨论热度：** 1条评论，1个作者反馈。
  - **分析：** 此Issue虽然由用户 `zqgittest` 在4月份提交，但今天被标记为“活跃”（更新时间变为2026-06-25），可能意味着维护者开始介入或重新评估。用户报告了一个具体的交互Bug：部分定时任务的开关无法点击关闭。附带的截图清晰地暴露了问题点。该Bug直接影响用户对任务的控制，属于 **功能缺陷**。社区对此问题的关注，反映了用户对任务调度功能的依赖以及对其稳定性的要求。

## 5. Bug 与稳定性

今日未报告新的Bug Issue。但根据今日合并的PR，可以推断之前存在一些已修复或正在修复的稳定性问题：

- **[严重] 子代理会话状态同步重复**：PR [#2201](https://github.com/netease-youdao/LobsterAI/pull/2201) 修复了 `OpenClaw` 中子代理会话结束时的历史同步问题，可能导致GLM看到重复的回复。**状态：已有Fix PR并合并。**
- **[严重] 子代理轮询中断**：PR [#2199](https://github.com/netease-youdao/LobsterAI/pull/2199) 修复了父会话结束后，对子代理的轮询可能中断的问题，可能导致状态更新延迟或丢失。**状态：已有Fix PR并合并。**
- **[中等] 计划模式消息重复**：PR [#2200](https://github.com/netease-youdao/LobsterAI/pull/2200) 修复了因流式响应抖动导致Cowork计划模式产生重复消息的问题。**状态：已有Fix PR并合并。**
- **[低] 扩展/插件加载失败**：PR [#2203](https://github.com/netease-youdao/LobsterAI/pull/2203) 修复了本地扩展预编译失败问题；PR [#2202](https://github.com/netease-youdao/LobsterAI/pull/2202) 修复了浏览器插件因白名单限制而无法使用的问题。**状态：已有Fix PR并合并。**
- **[待确认] 定时任务开关Bug**：Issue [#1392](https://github.com/netease-youdao/LobsterAI/issues/1392) 报告了一个未解决的功能Bug，目前 **尚未关联Fix PR**，需要维护者进一步跟进。

## 6. 功能请求与路线图信号

今日新增的Issues和PR中未出现明确的功能请求。但从已合并的PR可以看出项目的发展方向：

- **OpenClaw生态系统预装：** PR [#2198](https://github.com/netease-youdao/LobsterAI/pull/2198) 预装了QQ和Discord插件，这是一个强烈的信号：**下一版本的LobsterAI将更加重视与第三方IM平台的集成**，这可能作为“开箱即用”的特性被包含在内。
- **对非标准模型（如Qwen）的兼容性优化：** PR [#2200](https://github.com/netease-youdao/LobsterAI/pull/2200) 专门针对“Qwen plan mode”进行了优化，这表明项目路线图中可能包含 **对更多第三方/国产大语言模型的特别支持与兼容性修复**。

## 7. 用户反馈摘要

- **Issue [#1392](https://github.com/netease-youdao/LobsterAI/issues/1392) 评论分析：** 用户反馈“部分任务开关无法点击”，并提供了截图。这反映了用户在使用任务调度功能时遇到的 **交互障碍**。用户期望每个开关都是有效且响应迅速的。此反馈突显了 **UI/UX的可靠性和一致性** 是用户非常在意的部分。虽然只有一条反馈，但直击痛点。

## 8. 待处理积压

- **[重要] Issue #1392：“定时任务开关点击无反应”**：此Issue创建于2026-04-03，今天（2026-06-25）被标记为活跃。尽管社区评论不多，但这是一个直接影响核心功能使用的Bug。建议维护者在下一轮迭代中优先处理此问题。已经有一系列修复Cowork和OpenClaw的PR被合并，表明团队有较高的修复效率，希望这个历史遗留的UI问题能尽快得到解决。

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 CoPaw (QwenPaw) 项目 2026-06-26 数据生成的每日项目动态日报。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-06-26

## 1. 今日速览

今日项目社区活跃度极高，共产生 27 条 Issue 更新和 50 条 PR 更新。Bug 修复类 Issue 占据了绝大多数，但社区贡献者响应迅速，多起严重或回归性 Bug 均有对应的 PR 正在处理或已被合并。项目正经历从 AgentScope 1.0 到 2.0 的架构迁移阵痛期，大量 PR 集中在适配新 Runtime 和修复迁移导致的兼容性问题。此外，社区对前端体验、模型兼容性和系统资源管理方面的反馈非常集中，反映出用户基数扩大后对稳定性和可用性的更高期待。

## 2. 版本发布
*无新版本发布。*

## 3. 项目进展

今日项目向前推进主要集中在解决 AgentScope 2.0 迁移带来的兼容性问题和修复关键 Bug。以下为已合并或确定推进的重要 PR：

- **[PR #5542]** `test(e2e): adapt for agentscope 2.0 — drop Plan Mode, fix selectors and fixtures`：这是一个重要的里程碑，标志着 e2e 测试套件已完全适配新的 AgentScope 2.0 架构。它移除了被废弃的 Plan Mode，修复了多个 P0 级别的测试失败，为后续开发提供了可靠的回归保障。
- **[PR #5443]** `fix(tui): restore ACP commands and inline approvals`：修复了 TUI 在 AgentScope 2.0 迁移后丢失的核心 ACP (Agent Communication Protocol) 命令、状态显示和内联审批功能，恢复了关键的用户交互能力。
- **[PR #5471]** `feat: generalize match pattern`：完成了匹配模式的泛化改进，可能提升了意图识别或插件匹配的灵活性，具体影响需进一步观察变更内容。
- **[PR #5534]** `refactor(readme): add trending badge`：为项目 README 增加了趋势徽章，提升了项目的可见度和传播性。

## 4. 社区热点

今日社区讨论最为热烈、反应最多的问题是 **`browser_use` 模块的资源泄漏问题**。

- **[Issue #5520]** `[Bug]: browser_use stop() leaves Chrome renderer processes running, causing memory leak (regression from #2733 / PR #2843)` - 平均评论: 1，但此 Issue 关联到了历史 Bug [#2733] 和其修复 PR，表明这是一个严重的回归问题，直接导致系统内存随着 Start/Stop 操作而持续泄漏。社区对资源管理的敏感性很高。
    - *链接: https://github.com/agentscope-ai/QwenPaw/issues/5520*
- **[Issue #5539]** `[Bug]: 心跳任务偶尔会执行失败，显示被用户打断` - 平均评论: 1，但提及了核心功能的可靠性问题。用户质疑 120 秒超时导致复杂 heartbeat 任务被硬中断，这直接影响了任务的可靠性。
    - *链接: https://github.com/agentscope-ai/QwenPaw/issues/5539*

**分析：** 社区用户的深层诉求是**系统稳定性和可靠性**。无论是浏览器自动化导致的资源耗尽，还是内建任务的超时中断，都指向了用户对 CoPaw 作为一个稳定运行平台的期望。这些问题影响了用户长时间运行或执行复杂任务的场景。

## 5. Bug 与稳定性

今日报告的 Bug 数量多且涉及面广，按严重程度排列如下：

| 严重程度 | Issue | 摘要 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| **严重 (Critical)** | [#5520] | `browser_use stop()` 导致 Chrome 子进程泄漏，引发内存泄漏 (Regression) | **是** ([PR #5536]) |
| **严重 (Critical)** | [#5379] | 通过 Python 安装后启动即报 `Internal Server Error`，影响新用户尝试。 | 无 |
| **高 (High)** | [#5505] | MiniMax 图片安全审核错误被 `rejects_media=True` 误判缓存，导致后续视觉请求被剥离。 | **是** ([PR #5535]) |
| **高 (High)** | [#5480] | 前端 Console 长消息排版错乱，CSS 重绘缺失。 | **是** ([PR #5538]) |
| **高 (High)** | [#5479] | 大会话文件 (>500KB) 打开导致前端崩溃。显示性能问题。 | 无 |
| **中 (Medium)** | [#5403] | 浏览器自动填充错误地劫持了模型配置页面的搜索框。 | 无 |
| **中 (Medium)** | [#5528] & [#5529] | Linux 上因 IME 包裹的默认浏览器启动失败；`/new` 指令与技能自动补全冲突。 | **部分** ([PR #5526] 已修复 browser 启动问题) |
| **低风险** | [#5345] | 自定义 OpenAI 兼容提供商不支持 function calling。 | **已关闭** (无关联 PR，可能已解决) |
| **低风险** | [#5541] | Ollama 无法访问 Cloud 模型，配置后无响应。 | 无 |

- **[PR #5536]** `fix: kill orphaned Chrome renderer processes on browser stop`：精准针对 [#5520] 的回归 Bug。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5536*
- **[PR #5535]** `fix: don't cache content moderation errors as rejects_media`：精准针对 [#5505] 的缓存误判 Bug。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5535*
- **[PR #5538]** `fix(chat): preserve assistant markdown newlines`：精准针对 [#5480] 的前端渲染问题。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5538*
- **[PR #5526]** `fix(browser): handle env-wrapped Exec in Linux default-browser detection`：精准针对 [#5528] 的 Linux 兼容性问题。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5526*
- **[PR #5457]** `fix: cap the file size of send_file_to_user`：回应了文件传输可能带来的风险和性能问题。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5457*

## 6. 功能请求与路线图信号

社区提出了多项功能请求，其中部分已有相关 PR 在处理：

- **[Issue #5342]** `[Feature]: hard cap on tool result size at execution layer`: 用户希望在执行层对工具结果大小设置硬限制，以防御因 LLM 调用失败导致上下文爆炸的场景。这是一个非常务实且重要的稳定性增强需求。
    - *链接: https://github.com/agentscope-ai/QwenPaw/issues/5342*
- **[Issue #5484]** `[Feature]: Support installing plugins via pip from PyPI`: 用户建议支持通过 pip 从 PyPI 安装插件，认为当前仅通过 ZIP 包安装的方式不符合 Python 生态习惯。
    - *链接: https://github.com/agentscope-ai/QwenPaw/issues/5484*
- **[PR #5321]** `feat(context): scroll context manager — durable history + recall REPL`: 一个非常有前瞻性的 PR，引入了基于 SQLite 的持久化历史记录和按需调用 REPL 的上下文管理策略，旨在替代传统的上下文压缩。若合并，将彻底改变 CoPaw 处理长对话的方式。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/5321*

**路线图信号：** 社区的需求正从“能用”转向“好用且稳定”。**运行时的鲁棒性**（如：工具结果大小限制、内存泄漏修复）和**生态扩展性**（如：pip 安装插件）是下阶段的重要方向。

## 7. 用户反馈摘要

从今日的 Issues 中，可以清晰地看到用户在不同场景下的痛点和诉求：

- **新用户入门障碍：** 通过 `pip install` 后启动直接报 `Internal Server Error` ([#5379])，严重影响新用户的首次体验和留存率。
- **对稳定性的焦虑：** 用户报告了多个导致系统崩溃或资源泄漏的问题，如打开大文件崩溃 ([#5479])、Chrome 进程泄漏 ([#5520])，这引发了用户对 CoPaw 作为生产环境工具的担忧。
- **模型兼容性痛点：** 自定义供应商 function calling 支持不完整 ([#5345])、特定模型（如 MiniMax, GLM）在安全审核后出现逻辑错误 ([#5505])、甚至神秘地无法访问 Ollama Cloud 模型 ([#5541])，表明模型适配的覆盖面和质量仍需提升。
- **交互体验的细节不满：**
    - 前端排版问题 ([#5480]、[#5501]) 影响了基本的阅读体验。
    - `/new` 指令与技能自动补全冲突 ([#5529]) 直接干扰了用户操作。
    - 无法删除或编辑单条对话 ([#5503]) 让用户感到交互上缺少灵活性。
- **积极贡献者：** 出现多位首次贡献者（first-time contributor），积极提交 PR 修复他们遇到的 Bug，例如 [#5536]、[#5538]、[#5526]、[#5537] 等，反映出社区氛围良好，用户愿意参与共建。

## 8. 待处理积压

以下是一些值得维护者关注的长期未响应或重要的 Issue/PR：

- **[PR #4041]** `feat(desktop): add Tauri tray behavior`: 这个旨在为桌面版增加系统托盘功能的 PR 已经开放超过 50 天，目前状态为 `Under Review`。它对于提升桌面版用户体验至关重要，建议安排 Review 以决定是否合并。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/4041*
- **[PR #4622]** `plugin(datapaw): add data-analysis plugin with 12 BI skills`: 一个包含 12 个 BI 技能的数据分析插件，也是一个开放超过 30 天且标签为 `Under Review` 的 PR。该项目展示了 CoPaw 的插件生态潜力，建议评估合并以丰富插件库。
    - *链接: https://github.com/agentscope-ai/QwenPaw/pull/4622*
- **[Issue #5162]** `[Bug]: 对话思考逻辑进入死循环`: 该 Issue 从 6 月 12 日至今已存在两周，虽有一些讨论但缺乏根本性的解决方案或明确的状态更新。这可能导致用户在使用 Agent 时遇到未知的中断问题。
    - *链接: https://github.com/agentscope-ai/QwenPaw/issues/5162*

**项目健康度评估：** 项目处于 **活跃且剧痛的转型期**。社区贡献活跃度极高，Bug 修复响应迅速是积极信号。但问题密度高，尤其集中在 AgentScope 2.0 迁移导致的兼容性问题上，表明此次架构变动的测试覆盖面或代码兼容性尚有提升空间。维护者需要优先稳定平台核心功能（如 `browser_use` 内存泄漏、新用户安装报错），以尽快完成这次架构升级的平稳过渡。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeroClaw 项目数据，现为您生成 2026-06-26 的项目动态日报。

---

## ZeroClaw 项目动态日报 | 2026-06-26

### 1. 今日速览

今日 ZeroClaw 项目处于**高强度开发与发布冲刺**阶段。过去 24 小时内，Issues 和 PR 的数量均处于高位，活跃度 **极高**，社区贡献者和核心维护者都在集中处理与 **v0.8.2 版本发布**相关的收尾工作。目前，项目正面临 **49 个 PR 待合并**的高积压状态，显示出大量的修复和功能已准备就绪，亟需合并。安全性和稳定性是当前社区最关注的焦点，尤其是 `delegate` 工具绕过父策略的严重 Bug 和 MCP 进程泄漏问题的修复进展。

### 2. 版本发布

- **无新版本发布。** 项目当前的主要状态是为 `v0.8.2` 版本的发布做最后冲刺，相关版本号升级和更新日志的 PR（#8234）已经在审核流程中。

### 3. 项目进展

尽管版本未更新，但代码库层面有显著推进，主要围绕漏洞修复和为 `v0.8.2` 版本扫清障碍。

- **关键 Bug 修复：**
    - **修复了代理解除代理（delegate）绕过父节点工具白名单的安全漏洞 (PR #8279):** 该问题被标记为 S0 级安全风险，今日已被关闭。修复确保子代理不能调用父级策略未授权的工具。这是对系统权限模型的关键加固。
    - **修复了 Kimi Code 提供商的端点回归问题 (PR #8154):** 解决了工作流受阻的 S1 级 Bug，将错误的 API 端点指向了正确地址，恢复了对 Kimi Code 服务的兼容。
    - **修复了 Telegram 媒体组分发逻辑 (PR #7873):** 解决了发送多张图片时会产生多个重复回复的问题，现在会将媒体组作为单次代理请求处理，改善了用户体验。

- **功能与增强：**
    - **推进了应用内升级与自动重启功能 (PR #8173):** 一个大型 PR，实现了从 Web 仪表板检测、展示发布说明、下载并应用更新的完整流程，解决了用户需要手动离开仪表板进行更新的痛点。
    - **新增了频道会话 TTL 清理机制 (PR #8139):** 为频道会话增加了基于生存时间（TTL）的自动清理功能，防止因会话历史无限增长导致的内存和性能问题。

- **版本里程碑进展：**
    - 核心跟踪器 #8071 (v0.8.3 运行时) 和 #8181 (v0.8.2 发布支持) 仍在活跃，表明项目正在快速推进并细分任务，以确保下一版本的高质量交付。

### 4. 社区热点

今日讨论最热烈的议题均围绕**安全性与架构演进**。

1.  **议题 #6808: RFC: 工作流泳道、面板自动化与标签清理** (评论: 11)
    - **链接:** [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)
    - **核心诉求:** 该 RFC 旨在建立一套更清晰的项目管理流程，通过“工作流泳道”和自动化看板来分类和组织工作，并清理冗余的 Issue 标签。这表明项目在追求代码质量的同时，也在努力优化自身的开发流程，以应对越来越多的贡献者和 Issue。
2.  **议题 #8177: RFC: 供应链安全 - 硬件 PGP、密闭构建与 SLSA 溯源** (评论: 8)
    - **链接:** [Issue #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)
    - **核心诉求:** 这是对项目供应链安全的一次重大构想，建议引入硬件 PGP 密钥、多签、脱机签名等高强度措施，以保护容器镜像和发布二进制文件的安全。这反映了社区对软件供应链攻击的高度警惕和对项目可信赖度的强烈要求，是项目走向企业级的关键一步。
3.  **议题 #6165: RFC: 通过外部集成实现更轻量的 ZeroClaw 核心** (评论: 5)
    - **链接:** [Issue #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)
    - **核心诉求:** 建议使用 Skills 系统来替代硬编码的集成（如 Jira, GitHub），让核心变得更加模块化和轻量。这是一个持续性的架构辩论，反映了社区对于是让项目“功能全面”还是“精简可扩展”有着长期的思考。

### 5. Bug 与稳定性

今日报告的 Bug 中，安全问题最为突出，其次是数据丢失和构建问题。

- **严重 (S0/高风险):**
    - **[已关闭] 议题 #8279: Delegate 绕过父级工具白名单** (已修复)
        - **摘要:** 子代理可以调用被父策略禁止的工具，是严重的安全漏洞。
    - **议题 #5903: MCP stdio 子进程在守护进程中泄漏** (已接受)
        - **摘要:** 默认启用心跳时，每次心跳都会泄漏一个 MCP 子进程，长时间运行会消耗大量系统资源。
    - **议题 #8312: `fill-translations` 泄露修复留下陈旧条目，导致数据二次泄露** (P1)
        - **摘要:** 翻译修复工具本身存在 Bug，修复后遗留了错误数据，导致已修复的泄漏文本被反复写入文件，造成静默数据丢失。

- **中等 (S1/S2/高风险):**
    - **[已关闭] 议题 #8234: Kimi Code 端点返回 404** (已修复)
        - **摘要:** 关键工作流被阻塞的回归问题已解决。
    - **[已关闭] 议题 #8236: `voice_wake.rs` 缺少 `subject` 字段，导致 `--all-features` 构建失败** (已修复)
        - **摘要:** 构建系统上的编译错误已修复。
    - **议题 #8327: 原生工具调用中的 `[IMAGE:...]` 标记被作为纯文本发送，膨胀 Token 数**
        - **摘要:** 对于使用原生工具调用的用户（如配合 `llama.cpp`），图像数据会以 Base64 文本形式传输，导致 Token 消耗激增，成本和延迟增加。
    - **议题 #8334: `skills install` 命令目标路径与多代理运行时不匹配** (P2)
        - **摘要:** `zeroclaw skills install` 命令安装的技能文件处于运行时无法加载的路径，导致“安装即无法使用”的尴尬局面。

### 6. 功能请求与路线图信号

多个功能请求已经与 **v0.9.0** 计划关联，表明它们受到维护者的重视。

- **`delegate` 模式增强 (#7743, #8238):** 社区要求一个更灵活的“独立委派模式”，允许在委派子代理时使用子代理自身的策略和工具集，而不仅仅是父级的筛选副本。这与 #8279 的 Bug 修复密切相关，旨在建立一个更安全、更强大的多代理协作模型。
- **Wasm 元年计划 (#7497, #8132, #8135, #8187):** 一系列关于 **WebAssembly 优先**的 RFC 和 Issue 正在密集讨论，目标是将 Wasm 作为默认的插件运行时，并用 Rust 重写 Web UI。这是一个重大的架构迁移方向，信号强烈，很可能在未来几个版本中逐步实施，旨在彻底消除对 Node.js 的构建时依赖。
- **“目标驱动”模式 (#8303):** 用户希望 ZeroClaw 能支持一种“有界自主工作”模式，能够为代理设定一个目标，并让它持续工作直到完成、失败或预算耗尽，而不是仅支持单次对话或定时任务。这是一个符合 AI Agent 演进方向的重要需求。
- **`SkillForge` 功能的未来 (#8309):** 一个长期未激活的自动技能发现和集成功能引发了讨论，社区和贡献者正在评估是继续完善还是移除该功能，以避免代码未使用而形成负担。

### 7. 用户反馈摘要

从今日的 Issue 评论中，可以提炼出以下真实的用户痛点：

- **对安全性的焦虑:** 在 #8279 中，用户报告 `delegate` 可以绕过父级工具白名单的做法，被评价为“S0 - 数据丢失/安全风险”，这直接反映了用户对多代理场景下权限隔离的极度不信任。用户不仅需要“委派”功能，更需要“安全可控的委派”。
- **对提供者兼容性的高要求:** 用户 jparga 在 #8154 中报告 Kimi Code 提供商回归问题，并明确指出“working URL is ...”，用户愿意主动提供验证信息，说明其对特定模型提供商的依赖很深，且对此类回归问题容忍度低。
- **对“开箱即用”体验的挫折感:** 问题 #8334 和 #8309 都揭示了用户对“干净”和“工作”状态的追求。技能安装后不被加载 ( #8334 ) 和旧功能未被妥善处理 ( #8309 )，都让新用户或准备使用该功能的用户感到困惑，并损害了项目的易用性声誉。
- **对资源消耗的抱怨:** 问题 #8327 中对图像标记被当作文本处理的报告，直接指向了 Token 成本的高涨。这表明用户不仅关注功能，也深度关注底层实现带来的效率和经济性问题。

### 8. 待处理积压

- **高优先级 Bug 等待修复:**
    - **议题 #5903: MCP stdio 子进程泄漏** 状态已接受，影响范围广（守护进程长期运行），但尚无对应的修复 PR。这是一个严重的稳定性隐患，特别是在生产环境中。
        - **链接:** [Issue #5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903)
    - **议题 #6165: 关于轻量级核心的 RFC** 持续未决，讨论已经持续了两个月。这是一个长期的架构分歧，维护者需要做出最终决定，以明确项目方向并激励或平息相关的社区讨论。
        - **链接:** [Issue #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)

- **等待关键审查的 PR:**
    - **PR #8234: 版本升级到 v0.8.2** 作为版本发布的最后一步，此 PR 阻塞了所有后续的发布流程。其审批速度直接影响版本交付时间表。
        - **链接:** [PR #8234](https://github.com/zeroclaw-labs/zeroclaw/pull/8234)
    - **PR #8173: Web 仪表板应用内升级** 这是一个大型和重要的功能，目前有 49 个待合并 PR，该 PR 需要更多维护者的审查，以确保安全性和兼容性，之后才能合并。
        - **链接:** [PR #8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173)

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*