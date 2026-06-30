# OpenClaw 生态日报 2026-06-30

> Issues: 404 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-30 02:01 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的OpenClaw项目数据，以下是生成的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-30

## 1. 今日速览

项目今日社区活跃度**极高**，过去24小时内产生了**404条Issue**（新开/活跃340条）和**500条PR**（待合并446条）。虽然有大量待处理工作，但维护者正通过PR积极修复关键Bug，正在推动项目稳定性提升。未见新版本发布，但核心关注点集中在**网关可靠性、提供商兼容性、集群稳定性以及SQLite存储迁移**等重大基础设施改进上。社区反馈强烈，多个P1级Bug和功能请求正在等待产品决策。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

尽管PR积压较多，但今日仍有多个关键修复被合并或进入最终审查阶段，显示出项目核心团队在推进稳定性与功能演进。

- **[#96625] refactor: flip sessions and transcripts to sqlite storage** (状态: 👀 准备好供维护者审查)
    - **作者**: jalehman
    - **影响力**: **极高**。这是一个非常重大的架构变更，将整个会话存储从JSON文件迁移到SQLite。这将大幅提升大规模部署下的性能和可靠性，并解决长期存在的并发写入和状态丢失问题。
    - **链接**: https://github.com/openclaw/openclaw/pull/96625

- **[#90239] Add session history family lookup** (状态: 👀 准备好供维护者审查)
    - **作者**: simplyclever914
    - **影响力**: **高**。此PR解决了会话历史在`reset`后被切断的问题，通过引入“家族”查询，使得跨重置会话的连续上下文对话成为可能。
    - **链接**: https://github.com/openclaw/openclaw/pull/90239

- **[#97952] fix(codex): require admin for native controls** (状态: 👀 准备好供维护者审查)
    - **作者**: eleqtrizit
    - **影响力**: **中**。修复了Codex运行时中敏感操作缺少权限校验的安全漏洞，巩固了项目的安全边界。
    - **链接**: https://github.com/openclaw/openclaw/pull/97952

- **[#97889] fix(discord): guard JSON.parse against malformed API response bodies** (状态: 👀 准备好供维护者审查)
    - **作者**: lsr911
    - **影响力**: **中**。修复了Discord频道因API返回畸形JSON导致整个进程崩溃的严重稳定性问题。
    - **链接**: https://github.com/openclaw/openclaw/pull/97889

## 4. 社区热点

**[#75] Linux/Windows Clawdbot Apps** 
- **评论数**: 110 | 👍: 81
- **核心诉求**: 这是项目历史上呼声最高的功能请求之一。用户期望OpenClaw能像支持macOS、iOS和Android一样，正式支持Windows和Linux桌面端应用。这表明社区对全平台覆盖的强烈渴望。
- **链接**: https://github.com/openclaw/openclaw/issues/75

**[#94518] DeepSeek cache hit rate <10% after 6.x upgrade**
- **评论数**: 6 | 👍: 8
- **核心诉求**: 用户对升级后DeepSeek缓存命中率从正常水平暴跌至10%以下感到沮丧。评论数不多，但**点赞数高**，表明大量用户受到了同一问题的困扰。此问题对使用DeepSeek模型的用户影响巨大，可能增加其API使用成本并降低响应速度。
- **链接**: https://github.com/openclaw/openclaw/issues/94518

**[#79077] Support for Telegram bot-to-bot and guest-bot modes**
- **评论数**: 8 | 👍: 8
- **核心诉求**: 社区对拥抱最新的Telegram平台特性（如机器人间通信）表现出浓厚兴趣，这表明用户希望在Telegram上实现更复杂、自动化的交互模式，而非仅仅是人与机器人的对话。
- **链接**: https://github.com/openclaw/openclaw/issues/79077

## 5. Bug 与稳定性

今日报告的Bug主要集中在**会话状态丢失、提供商兼容性和集群稳定性**上。

- **[#97877] empty-error-retry blocked by hadPotentialSideEffects — silent terminal failure** (Severity: P1)
    - **摘要**: 一个非常隐蔽的Bug：当会话中任何工具调用后遭遇短暂5xx错误，重试逻辑会因一个保护机制被错误触发而失效，导致任务静默失败。这严重影响了Agent的鲁棒性。**已有对应Fix PR ([#97966])**。
    - **链接**: https://github.com/openclaw/openclaw/issues/97877

- **[#91363] Isolated cron consistently fails with “LLM request failed”** (Severity: P1)
    - **摘要**: 这是一个持续一个月的长期稳定性问题。隔离的Cron任务在启动阶段就失败，从未真正向LLM发起请求。这对依赖定时自动化任务的用户来说是关键阻塞点。
    - **链接**: https://github.com/openclaw/openclaw/issues/91363

- **[#86538] Session write-lock timeouts block subagent delivery lanes** (Severity: P1)
    - **摘要**: 会话级别的写锁超时会导致整个多Agent系统中的`subagent`输送通道阻塞，这是一个严重的集群性能瓶颈问题。
    - **链接**: https://github.com/openclaw/openclaw/issues/86538

- **[#95121] [Regression] Codex OAuth/Appserver turns spend ~28s after prompt.submitted for tiny gpt-5.5 replies** (Severity: P2)
    - **摘要**: 用户报告了一个严重的**回归**问题，在升级后，即使是极小的请求，通过Codex的OAuth路径处理也需要大约28秒的延迟，极大影响了用户体验。
    - **链接**: https://github.com/openclaw/openclaw/issues/95121

## 6. 功能请求与路线图信号

近期功能请求呈现出**向集群化、SDK化和全平台覆盖**发展的趋势。

- **预计纳入下一版本**:
    - **[#80213] Skill author-defined setup hook**: 允许Skill作者定义安装后脚本。PR [#96625] (SQLite存储迁移) 的实现可能为此类“生命周期钩子”提供基础。
    - **[#81913] Expose stable plugin SDK surface**: 社区迫切需要一个稳定的插件SDK，以促进插件生态的发展。该请求与此前众多PR中对内部模块进行解耦的努力方向一致，很可能成为下个阶段的开发重点。

- **路线图信号**:
    - **[#80176] JSONL session-replay harness**: 提出构建回放测试框架，这是提升项目测试质量和回归捕获能力的重要信号，可能作为长期质量保障体系建设的一部分。
    - **[#81061] Hook: before_route_inbound_message**: 提出用于“通道桥接/代理”的预处理钩子。这表明社区正探索将OpenClaw用作更复杂的消息路由中枢，驱动的场景是跨平台消息聚合与转发。

## 7. 用户反馈摘要

- **对SQLite迁移的期待与担忧**: PR [#96625] 中的讨论（尽管未列出详细内容）反映了社区对解决JSON存储性能与并发问题的**广泛期待**，但也可能混杂着对数据迁移兼容性和稳定性的担忧。
- **Telegram功能的强劲需求**: Issue [#79077] (支持机器人间通信) 的用户评论中，用户明确描述了“Host a podcast interview with two bots in a supergroup”的用例，揭示了用户期待构建复杂、多Agent自动化对话场景的强烈需求。
- **对“静默失败”的零容忍**: 多个P1级Bug（如#97877, #80520）都描述了“静默失败”的场景，用户评论中透露出极大的困扰，他们希望系统在出错时能提供清晰的诊断信息，而不是让消息石沉大海。
- **Mac用户的特定痛点**: Issue [#80036] (Chrome MCP在macOS上超时) 和 [#81934] (macOS更新后多个功能失效) 表明macOS用户遇到了特定的集成问题，对macOS平台的版本稳定性要求较高。

## 8. 待处理积压

- **关键Bug（P1）长期未决**:
    - **[#74586] AM embedded run aborts memory_search tool calls** (更新: 29天前): 一个长期存在的、影响核心插件功能的P1级Bug，需要尽快有明确的修复PR或产品决策。
    - **[#80520] Telegram messages silently dropped** (更新: 42天前): 影响Telegram用户核心体验的P1级Bug，至今未有明确的Fix PR关联。

- **长期待审功能PR**:
    - **[#12581] feat(hooks): emit session prune lifecycle event** (创建: 4个月): 一个关于会话修剪生命周期的功能PR，长期处于等待作者回复状态。该功能对插件生态的高级交互很有价值，维护者应考虑主动跟进或关闭。
    - **[#94422] fix(channels): drop reasoning deltas that are a sub-string of the current buffer** (状态: 📣 需要佐证): 一个优化流式推理结果的PR已提交12天，目前仍需更多证据。建议维护者尽快介入审查或引导提供测试用例。

---

## 横向生态对比

好的，作为资深技术分析师，现根据您提供的2026年6月30日各项目动态，为您呈上个人AI助手与AI智能体开源生态的横向对比分析报告。

---

### **个人AI助手与AI智能体开源生态横向对比分析报告 (2026-06-30)**

#### **1. 生态全景**

当前个人AI助手与自主智能体开源生态呈现 **“高基数下的高速分化与演进”** 态势。一方面，以OpenClaw、NanoBot、CoPaw为代表的头部项目社区活跃度爆棚，日处理PR/Issue量达数十甚至数百条，显示出惊人的社区参与度和迭代速度。另一方面，生态内部正围绕**部署规模（单机 vs. 集群）、通信协议（去中心化 vs. 传统IM）、模型集成深度（缓存优化、降级策略）** 等维度快速分化，不同项目致力于解决不同层次的用户痛点。虽然项目整体健康度极高，但P1级Bug的积压和用户对“静默失败”、“高成本”的抱怨也表明，生态正从“能用”向“好用、可靠、低成本”阶段艰难跨越。

#### **2. 各项目活跃度对比**

| 项目 | Issues 数 | PR 数 | Release | 健康度评估 | 核心阶段 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 404 (340新/活跃) | 500 (446待合并) | 无 | 极高活跃，高压 | **快速发展与质量攻坚期** |
| **NanoBot** | 7条更新 | 33 (10合并/关闭) | 无 | 高活跃，健康 | **功能增强与体验优化期** |
| **Hermes Agent** | 50 | 50 | 无 | 极高活跃，压力大 | **Bug修复与多平台适配期** |
| **LobsterAI** | 40条更新 | 40 (39合并/关闭) | v2026.6.29 | 高效迭代，健康 | **稳定性修复与版本发布期** |
| **PicoClaw** | 3条更新 | 3 (0合并) | 无 | 中等活跃，稳定 | **功能收尾与等候合入期** |
| **NanoClaw** | 1个新Bug | 7 (2合并) | 无 | 活跃，健康 | **安全与渠道修复并进期** |
| **CoPaw (QwenPaw)** | 29 | 50 (18合并) | 无 | **极高活跃，高产出** | **密集修复与功能强化期** |
| **NullClaw** | 1个新Bug | 3 (1合并) | 无 | 低活跃，稳定 | **小步迭代与通道问题解决期** |
| **ZeroClaw** | 50 | 50 | 无 | **极高活跃，讨论激烈** | **核心特性重构与新版本冲刺期** |
| **TinyClaw / Moltis** | 0 | 0 | 无 | **静默** | 停滞 |
| **IronClaw** | 数据缺失 | 数据缺失 | 无 | 未知 | - |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 凭借其 **“企业级”和“集群级”** 的定位，在生态中扮演着“集大成者”与“基础设施层”的双重角色。

-   **优势与差异**：
    -   **规模与复杂度高**：日处理Issue/PR数量为生态之首（404/500），社区规模与反馈量巨大，但其问题复杂度也最高（如会话写锁超时、集群稳定性）。
    -   **技术路线前沿**：倾向于根本性的架构变更，如PR[#96625]的**SQLite存储迁移**，旨在解决大规模部署下的性能和并发问题，而非小修小补。这与NanoBot追求轻量、PicoClaw追求协议多样性形成鲜明对比。
    -   **安全与生态集成**：注重安全漏洞（如Codex原生控制权限）和生态兼容性（如DeepSeek缓存问题）。
-   **与同类对比**：
    -   **vs. NanoBot**：OpenClaw更像一个**操作系统**，关注底层架构与大规模集群；而NanoBot更像一个**功能强大的桌面应用**，关注单机体验与成本优化（如Token压缩）。
    -   **vs. CoPaw**：两者都在处理大量问题，但OpenClaw问题更偏“基础设施” (gateway可靠性， session管理)，而CoPaw问题更偏“模型兼容性和协作体验”（DeepSeek 400错误，飞书长消息）。
    -   **vs. LobsterAI**：LobsterAI是OpenClaw的**商业/集成化变体**，通过版本发布（v2026.6.29）将OpenClaw的核心能力打包成更稳定、更易用的产品。

#### **4. 共同关注的技术方向**

多个项目不约而同地涌现出以下需求，代表了生态的集体发展方向：

-   **深度模型集成与成本优化**：
    -   **涉及项目**：**OpenClaw** (`DeepSeek cache hit rate`)、**ZeroClaw** (`kimi-code reasoning`)、**CoPaw** (`DeepSeek V4 reasoning error`, `模型自动降级`)、**PicoClaw** (`Bedrock prompt caching`)。
    -   **核心诉求**：用户不满足于“能连上模型”，而是要求**稳定、低成本、高性能**的模型调用。这包括缓存优化、推理（Reasoning）模式兼容、以及降级/容错策略。

-   **渠道/IM稳定性与功能完整性**：
    -   **涉及项目**：**Hermes Agent** (`Telegram ghosting`)、**NullClaw** (`Telegram idle-die`)、**NanoClaw** (`Discord attachment drop`)、**CoPaw** (`Feishu long message fail`)、**ZeroClaw** (`Telegram channel config`)、**OpenClaw** (`Telegram msg silently dropped`)。
    -   **核心诉求**：渠道（特别是Telegram和Discord）的稳定性是普遍痛点。用户期望渠道能够**长期可靠运行、支持多媒体消息、与核心Agent状态同步**。渠道适配不再是“有就行”，而是需要“好用且稳定”。

-   **Agent 上下文一致性与会话管理**：
    -   **涉及项目**：**ZeroClaw** (`System prompt vs tool list mismatch`)、**CoPaw** (`Subagent infinite polling`)、**OpenClaw** (`Session write-lock timeouts`, `Session history family lookup`)。
    -   **核心诉求**：随着Agent变得更复杂（多Agent、多工具），系统提示词、工具列表、会话状态的一致性成为瓶颈。用户渴望一个**智力上“稳定”的Agent**，其行为和记忆逻辑在不同入口、不同模式下都保持清晰、可预测。

#### **5. 差异化定位分析**

| 维度 | OpenClaw | NanoBot | Hermes Agent | CoPaw | ZeroClaw | LobsterAI |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **核心定位** | 企业级智能体集群操作系统 | 高性能单机AI助手 | 多平台、多通道消息中枢 | 商业级智能体协作平台 | 下一代智能体运行时（WASM） | OpenClaw的商业/集成版 |
| **目标用户** | 专业开发者、运维、大型团队 | 个人开发者、极客、高级用户 | 社区运营、多渠道用户 | 企业团队、IM协作深度用户 | 探索者、安全研究人员 | 中小团队、商业用户 |
| **技术特色** | 集群架构、SQLite迁移、回放测试 | 极致轻量、Token压缩、成本优化 | ACP客户端、安全加固、多IM适配 | 即时通讯深度集成、模型降级、SDK | WASM沙箱、A2A发现、OWASP集成 | 系统化版本管理、Cowork模块、预装插件 |
| **关注重点** | 可靠性、大规模、通用架构 | 成本、速度、用户体验 | 兼容性、稳定性、多平台体验 | 稳定性、模型快速适配、协作工作流 | 插件生态、安全、未来协议 | 稳定性、集成度、用户体验 |

#### **6. 社区热度与成熟度**

-   **极高热度 / 快速迭代期**：**OpenClaw、CoPaw、ZeroClaw**。这些项目Issue/PR数量巨大，处于功能爆炸式增长和核心架构重构阶段。社区充满活力但也伴随着大量Bug和噪音。
-   **高热度 / 功能与质量巩固期**：**NanoBot、Hermes Agent、LobsterAI、NanoClaw**。这些项目活跃度很高，但更侧重于修复Bug、优化体验和增强周边功能（如WebUI、安全、插件）。LobsterAI通过版本发布已进入质量巩固期。
-   **中等 / 稳定发展期**：**PicoClaw、NullClaw**。项目维护者较少，主要依赖社区贡献进行小范围的功能增强和Bug修复，节奏相对稳定。
-   **静默 / 停滞期**：**TinyClaw、Moltis、IronClaw**。过去24小时无活动，社区活跃度低，项目可能处于暂停维护或成熟稳定状态。

#### **7. 值得关注的趋势信号**

1.  **“Agent-to-Agent (A2A)”与“智能体编排”需求爆发**：ZeroClaw的A2A发现协议RFC ([\#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)) 和 Hermes Agent的通用ACP客户端请求 ([\#5257](https://github.com/NousResearch/hermes-agent/issues/5257)) 共同指向了**智能体之间的互联互通与编排**。这不再是单一体能做什么，而是多个智能体如何协同工作。这为用户构建复杂的自动化工作流和网状服务提供了可能。

2.  **从“堆砌功能”到“工程化治理”**：大量P1级Bug（会话写锁、静默失败、凭据泄露）和长期积压的PR表明，许多项目正在经历“技术债”的阵痛期。LobsterAI的系统化版本修复、ZeroClaw的OMPAS集成和CI审计，都预示着生态正在觉醒，开始重视**代码质量、可观测性和安全性**等工程化实践。

3.  **成本是影响用户选择的关键杠杆**：DeepSeek缓存问题、NanoBot的Token压缩PR、OpenClaw的上下文压缩提议，都说明了**API使用成本已成为用户选择模型和平台的核心决策因素**。未来，能够提供“最高性价比智能体服务”的项目将获得更多用户青睐。

4.  **桌面端与全平台覆盖仍是未竟之地**：OpenClaw社区对Windows桌面应用的超高呼声 ([\#75](https://github.com/openclaw/openclaw/issues/75)) 和ZeroClaw的桌面控制RFC ([\#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)) 表明，**用户渴望AI助手突破API的束缚，走向桌面自动化、GUI交互**。这将是从“聊天机器人”进化为“数字员工”的关键一跃，也是未来项目竞争的制高点。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 NanoBot 项目数据，生成 2026 年 6 月 30 日的项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-30

**项目名称:** NanoBot (github.com/HKUDS/nanobot)
**报告周期:** 2026-06-29 至 2026-06-30
**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

NanoBot 项目今日保持高活跃状态，社区贡献和代码迭代节奏强劲。过去 24 小时内，项目共收到 **33 条 Pull Request (PR)**，其中 **10 条已被合并或关闭**，显示出项目团队对社区贡献的高效接纳与处理能力。同时，**7 条 Issue 更新** 中包含了 **4 个新报告的 Bug**，表明项目在快速发展的同时，功能稳定性仍是用户和贡献者关注的重点。尽管无新版本发布，但大量针对性能优化、安全增强和新功能的 PR 正在积极推进，为下一次发布积蓄能量，项目整体健康度极高。

### 2. 版本发布

本报告周期内无新版本发布。

### 3. 项目进展

今日项目进展显著，主要围绕性能优化、安全加固和 WebUI 体验提升展开。

-   **性能与成本优化 (核心):**
    -   PR [#4581](https://github.com/HKUDS/nanobot/pull/4581) 和 [#4588](https://github.com/HKUDS/nanobot/pull/4588) (作者: `hamb1y`) 是两项重量级的性能优化 PR，旨在**大幅减少上下文/输入令牌 (Input Tokens) 的消耗**。通过对工具调用输出的压缩、修剪和处理，项目有望显著降低推理成本，并允许低上下文窗口模型进行更长的对话。
    -   PR [#4589](https://github.com/HKUDS/nanobot/pull/4589) (作者: `aiguozhi123456`) 通过优化 Dream 记忆模块的提示词，引入**记忆卫生指令**，旨在遏制 `MEMORY.md` 文件的膨胀，进一步提升长期记忆的效率。

-   **安全与稳定性加固:**
    -   PR [#4596](https://github.com/HKUDS/nanobot/pull/4596) (作者: `axelray-dev`) 修复了流式文件编辑跟踪器中一个严重的 **ID 污染 Bug (Issue #4595)**，防止了会话中毒问题，这是对核心功能稳定性的重要修复。
    -   PR [#4594](https://github.com/HKUDS/nanobot/pull/4594) (作者: `axelray-dev`) 修复了`ExecTool`路径提取的安全漏洞 (Issue #4592)，防止通过 `curl --output=/etc/passwd` 等命令绕过工作区限制，加强了沙箱逃逸防护。
    -   PR [#4584](https://github.com/HKUDS/nanobot/pull/4584) (作者: `xiaweiwei67-stack`) 修复了 MCP 服务器 URL 中凭据泄露的日志安全问题，增强了敏感信息保护。

-   **WebUI 与用户体验:**
    -   PR [#4600](https://github.com/HKUDS/nanobot/pull/4600) (作者: `Re-bin`) 对 WebUI 的**提示词导航栏（Minimap）进行了重构和美化**，提升了用户浏览长对话时的体验。
    -   PR [#4587](https://github.com/HKUDS/nanobot/pull/4587) 和 PR [#4586](https://github.com/HKUDS/nanobot/pull/4586) (作者: `boogieLing`) 为 WebUI 带来了**Markdown 导出**功能和默认显示**会话时间戳**的改进，丰富了用户数据管理的选择。

-   **功能扩展:**
    -   PR [#4598](https://github.com/HKUDS/nanobot/pull/4598) (作者: `04cb`) 为 GitHub Copilot 提供商增加了**企业/GHE 端点覆盖**的支持，拓宽了项目的企业应用场景。
    -   PR [#4591](https://github.com/HKUDS/nanobot/pull/4591) (作者: `chengyongru`) 引入了**会话绑定的本地触发器**，允许用户通过文件系统队列为特定会话创建外部触发事件，增强了项目与外部系统的集成能力。

### 4. 社区热点

-   **最活跃讨论：** [Issue #660](https://github.com/HKUDS/nanobot/issues/660)
    -   **状态：** 已关闭
    -   **热度：** 15 条评论，5 个 👍
    -   **分析：** 这是一个长期存在的争议性问题，用户在质疑项目“超轻量级”的定位，因为其 Docker 镜像同时依赖 Python 和 Node.js。该问题最终被关闭，但拥有 5 个 👍 表明“轻量化”是社区中一部分用户的真实痛点。项目的技术选型（全栈能力）与部分核心用户群的期望（极致轻量）之间存在认知差异。

-   **当日 Bug 讨论：** [Issue #4599](https://github.com/HKUDS/nanobot/issues/4599)
    -   **状态：** 开放
    -   **难度：** 新报告，影响新用户
    -   **分析：** 安装脚本在 TUI 界面阶段直接崩溃，是影响新用户上手体验的严重问题。在已有 23 个待合并 PR 的情况下，该问题的优先级应高于大部分功能增强。

### 5. Bug 与稳定性

本日报告的 Bug 集中在功能逻辑和安全性上，按严重程度排列如下：

1.  **严重 - 安装引导崩溃:**
    -   [Issue #4599](https://github.com/HKUDS/nanobot/issues/4599) - 默认 Linux 安装脚本在 TUI 界面立即崩溃，阻止新用户安装。
    -   **状态：** 无对应修复 PR。

2.  **严重 - 会话中毒 (有修复PR):**
    -   [Issue #4595](https://github.com/HKUDS/nanobot/issues/4595) - `apply_final_call_ids` 错误覆盖非文件编辑工具（如 `read_file`）的 `tool_call.id`，导致会话中毒，后续所有请求都会失败。
    -   **状态：** 已有关联修复 PR [#4596](https://github.com/HKUDS/nanobot/pull/4596)。

3.  **中等 - 沙箱逃逸风险 (有修复PR):**
    -   [Issue #4592](https://github.com/HKUDS/nanobot/issues/4592) - `ExecTool` 的路径提取正则表达式未能识别 `=` 后的绝对路径，导致用户可通过 `--output=/etc/passwd` 写入任意路径。
    -   **状态：** 已有关联修复 PR [#4594](https://github.com/HKUDS/nanobot/pull/4594)。

4.  **中等 - 提示词缓存失效:**
    -   [已关闭 Issue #4222](https://github.com/HKUDS/nanobot/issues/4222) - `max_messages` 截断和紧凑机制导致消息前缀持续变化，使提示词缓存失效，增加了推理成本。该问题虽已关闭，但今日的 PR #4581 和 #4588 似乎是针对此问题的系统级解决方案。

### 6. 功能请求与路线图信号

-   **自动推理力度升级 (Issue #4419):** 用户请求根据问题复杂度自动调整模型的`reasoningEffort`参数。该项目已初步支持该参数，此提议旨在使其智能化。
    -   **路线图信号:** **强**。与优化成本和提升模型效率的核心目标高度契合，预计不久将有相关 PR 跟进。

-   **GitHub Copilot 企业版支持 (Issue #4220):** 由 PR #4598 解决，确认该功能已被纳入当前迭代，即将落地。

-   **子Agent 模型预设 (PR #4291):** 允许子Agent 使用与父 Agent 不同的模型。该 PR 已开放近 3 周，表明社区对 Agent 内部灵活性的需求正在增长，预计将成为未来版本的重要特性。

### 7. 用户反馈摘要

-   **痛点声音:** 核心用户对“**轻量化**”的定义存在分歧。Issue #660 的持续讨论表明，部分追求极致简洁的用户对项目依赖 Node.js 感到不满。尽管开发团队可能认为这是提供丰富 WebUI 的必要代价，但这仍是项目需要面对的定位沟通问题。
-   **场景反馈:** 从 Issue #4592 和 #4595 可以看出，用户正在**深入使用 NanoBot 的高级功能**（如受限执行环境、流式编辑），并发现了边界情况下的漏洞。这表明项目已从简单的聊天机器人向真正的 Agent 平台演进，用户使用深度在增加。
-   **不满情绪:** Issue #4599 反映的新用户安装体验不佳是直接的负面反馈，这会直接降低项目初期的留存率。

### 8. 待处理积压

以下为“长期未响应”但工作正向前推进的重要 PR/Issue，提醒维护者关注：

-   **功能请求:**
    -   [PR #4291](https://github.com/HKUDS/nanobot/pull/4291) - `feat(spawn): allow subagents to use configurable model presets` - **已开放 19 天**，功能价值高，涉及核心 Agent 逻辑，需尽快评审与合并，以明确路线图。
    -   [PR #4293](https://github.com/HKUDS/nanobot/pull/4293) - `fix(agent): add pending_queue to process_direct for subagent result injection` - **已开放 19 天**，修复了 Cron 任务等直接调用场景下子 Agent 结果注入的 Bug，对自动化场景至关重要。

-   **技术债务:**
    -   [Issue #4419](https://github.com/HKUDS/nanobot/issues/4419) - `Feature: Automatic reasoning effort escalation` - 虽无直接 PR，但代表了社区对“智能动态调优”的期望，具有前瞻性。建议将其标记为 `future` 或 `help wanted` 以引导社区贡献。
    -   [PR #4581](https://github.com/HKUDS/nanobot/pull/4581) & [#4588](https://github.com/HKUDS/nanobot/pull/4588) - 这两个高性能优化 PR 虽然新提交，但影响巨大，应作为**最高优先级**进行评审、合并并计划发布。它们是解决 Issue #4222 等长期问题的关键。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 Hermes Agent 项目数据生成的 2026-06-30 项目动态日报。

---

# Hermes Agent 项目动态日报
**日期**: 2026-06-30
**分析师**: AI 智能体与开源项目分析师

## 1. 今日速览

过去24小时内，Hermes Agent 项目保持着极高的社区活跃度，Issues 和 PR 均达到50条，表明项目正处于密集的迭代和问题修复阶段。虽然暂无新版本发布，但项目组处理了大量关于 BUG 修复和功能优化的 PR，特别是在安全、跨平台兼容性（Windows/macOS）和多平台集成（Telegram、Slack、Feishu 等）方面。社区反馈的热点集中在**网关可靠性、多提供商支持以及桌面端体验**上，显示用户正将本项目用于更复杂、更多样化的生产环境。

## 2. 版本发布

*无。*

## 3. 项目进展

今日项目在代码质量和稳定性方面取得了显著进展，以下为今日已合并/关闭的重要 PR 所推动的改进：

- **安全性加固**: PR #55352 修复了调试日志可能泄露凭据信息的安全问题；PR #55339 强制所有子进程调用使用 UTF-8 编码，解决了 Windows 平台的崩溃问题。
- **网关稳定性**: PR #54773 修复了飞书消息网关在令牌过期后无法自动刷新并重试的问题；PR #55346 同步了网关侧日志记录上下文，提高了调试效率。
- **桌面端与 TUI**: PR #55343 修复了语音输入在忙碌会话中的重入竞态问题，提升了 TUI 的响应性；PR #55337 修复了 Windows 下 `git` 二进制路径过长导致的桌面端功能异常。
- **配置与工具**: PR #55336 清理了保存凭据时的控制字符，修复了配置管理的潜在错误；PR #55338 改进了浏览器工具，通过模拟真实键盘事件，解决了 React/Vue 等框架无法检测到输入内容的问题。

## 4. 社区热点

今日社区讨论高度集中，主要围绕以下两个议题：

- **通用 ACP 客户端**: Issue [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) “通用的 ACP 客户端用于多智能体 CLI 编排” 获得了 **18个赞** 和 **13条评论**，是今日讨论度最高的话题。社区强烈希望 Hermes 不仅是一个 ACP 服务器，更能作为一个通用客户端，去编排包括 Claude 在内的多种 ACP 兼容智能体，这反映了用户对“智能体编排”和“模型无关性”的迫切需求。
- **Telegram 消息格式问题**: 两个关于 Telegram 的 Bug 报告均获得了高关注：
    - Issue [#50775](https://github.com/NousResearch/hermes-agent/issues/50775) “Telegram macOS 客户端上的视觉鬼影/文本重叠” 获得了 **4个赞**，反馈了 v0.17.0 版本中流式消息更新的严重显示问题。
    - Issue [#53632](https://github.com/NousResearch/hermes-agent/issues/53632) “定时任务破坏了Telegram中的富消息表格” 显示了特定功能在具体平台上的适配问题。

## 5. 稳定性与Bug报告

今日涌现大量 Bug 报告，按严重程度排列如下：

**P1 级别（严重）**:
- **凭据池读取问题** [Issues #20591]: `credential_pool` 未能正确读取 `.env` 文件，导致使用来自父进程的、可能过期的环境变量。影响范围大，涉及安全与准确性。*(暂无对应修复 PR)*

**P2 级别（高）**:
- **TUI 模式退出** [Issues #27282]: macOS 上 TUI 模式下的 Python 网关意外退出。*(暂无对应修复 PR)*
- **网关在 ZFS 文件系统上损坏 state.db** [Issues #55305]**: 这是一个严重的数据持久化问题，影响数据库的完整性。*(已有关联 PR？)*
- **Telegram 消息劫持/重叠** [Issues #50775]**: 流式更新导致的视觉 Bug。*(暂无对应修复 PR)*
- **工具参数截断** [Issues #55314]**: 在将大整数（如 Discord/Telegram ID）作为参数时，通过 `float` 转换导致精度丢失，数据被破坏。*(暂无对应修复 PR)*
- **Discord 语音 TTS 无声音** [Issues #16693]**: 尽管日志显示成功，但用户听不到声音。*(暂无对应修复 PR)*

**P3 级别（中/低）**:
- `reasoning_effort` 参数在自定义提供商上被静默丢弃 [Issues #55276]。
- `/clear` 命令导致 WSL 终端卡死 [Issues #32207]。
- TTS 播放后麦克风激活延迟 [Issues #51265]。

**已有修复 PR 的 Bug**:
- 凭据泄露的日志问题 [#55352]。
- Windows 平台编码问题 [#55339]。
- 语音转录竞态问题 [#55343]。
- WebSocket 消息过大导致 OOM 崩溃 [#55345]。

## 6. 功能请求与路线图信号

- **配置化推理温度 (Temperature)**: Issue [#17565] 要求用户可配置 LLM 的 temperature 参数，以解决硬编码值导致的“严重幻觉”问题。这是优化模型输出质量的核心需求，预计将很快被纳入开发路线图。
- **对话框宽度可调**: Issue [#55287] 请求在桌面端增加聊天宽度（composer-width）调节功能。这是提升用户体验的细节性需求，实现难度不高，可能随下次桌面端版本更新。
- **压缩上下文命令**: Issue [#31684] 提出的 `compress_context` 指令，允许用户手动压缩对话上下文以节省 Token。这表明用户正在经历长对话带来的 Token 消耗压力，是一个实用性很强的功能。
- **DeepSeek 集成**: Issue [#38065] 请求在桌面端提供 DeepSeek 选项，反映出社区对更丰富、多样化模型提供商的需求。

## 7. 用户反馈摘要

- **核心痛点**: “可靠性”是今日反馈的焦点。用户报告了网关因网络波动 (ZFS, 令牌过期)、平台限制 (Telegram, Discord) 以及内部逻辑错误 (凭据读取、子进程编码) 导致的各类不稳定问题。
- **功能需求**: 用户不再满足于简单的聊天，而是渴望一个 **“智能体的指挥中心”** (如 [#5257])，能够编排不同模型、执行复杂任务。
- **使用场景**: 从异常报告来看，社区正将 Hermes 用于更多样化、更接近生产环境的场景，包括 **持久化服务** ([#43196])、**跨平台消息集成** (Telegram, Discord, Slack, Feishu) 以及 **桌面日常使用** (MacOS, Windows)。
- **满意度**: 尽管 Bug 众多，社区通过提交高质量的 Issue（包含复现步骤和环境报告）和 PR 表现出极高的参与度与建设性，对该项目的发展寄予厚望。

## 8. 待处理积压

以下 Issue/PR 已存在较长时间，可能阻塞了部分用户的体验，建议维护者优先关注：

- **[~2个月] [Issue #5257]**: 通用 ACP 客户端。虽然热度极高，但自4月5日创建以来尚未进入开发阶段。如果此功能被接受，其解决方案将是项目向“智能体中心”转型的关键一步。
- **[~1.5个月] [Issue #24039]**: 辅助回退链应复用 `fallback_providers` 配置而不是保持硬编码列表。这是一个设计架构问题，影响所有使用回退功能用户的定制化体验。
- **[~2个月] [PR #12794]**: 子智能体模型/提供商覆盖。该 PR 已存在超过2个月未合并，可能是一个大型特性，其进度影响了依赖此功能的社区成员进行二次开发。
- **[~2个月] [Issue #16693]**: Discord VC TTS 无声音。这是一个影响特定用户的体验 Bug，长时间未解决可能会降低部分核心用户的满意度。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据您提供的PicoClaw项目数据，生成了以下项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-30

## 1. 今日速览

过去24小时内，PicoClaw项目活跃度中等，主要集中在社区反馈和功能开发的收尾阶段。**Issues方面**，共更新3条，其中1个与iOS兼容性相关的旧Bug已关闭，但新增了一个关于火山引擎豆包模型工具调用异常的Bug，可能需要关注。**Pull Requests方面**，有3个重要的功能增强PR（Delta Chat网关、Bedrock提示缓存、Token用量跟踪）均处于待合并状态，表明项目正在积极扩展新功能和提升性能。尽管无新版本发布，但多个核心功能已准备好合入，预示着下一版本将有显著更新。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无PR被合并或关闭，但项目有3个重要的功能PR处于待合并状态，它们是项目近期向前迈进的核心驱动力，若合并将显著提升项目的生态系统集成能力和性能表现：

- **PR #3063: feat: add deltachat gateway** - 此PR增加了对Delta Chat网关的支持。Delta Chat是一个基于电子邮件协议的即时通讯工具，该功能的引入将为用户提供一种去中心化、注重隐私的通信选择，拓展了PicoClaw的连接渠道。
    - 链接: `sipeed/picoclaw PR #3063`
- **PR #3163: feat(bedrock): leverage Converse prompt caching via cache points** - 此PR利用了AWS Bedrock的提示缓存功能。通过在系统提示、工具定义和消息中设置缓存点，可以显著降低大规模对话和工具调用场景下的推理成本（读取成本约为输入的0.1倍），对于使用AWS Bedrock作为后端的用户来说，是一项重要的成本优化。
    - 链接: `sipeed/picoclaw PR #3163`
- **PR #3156: feat(pico): emit per-turn LLM token usage on finalized message** - 此PR实现了在Pico频道上逐轮次发送最终的LLM Token用量信息。这使下游应用可以精确追踪每次对话的输入/输出Token消耗，对于进行用量监控和成本核算非常有价值。
    - 链接: `sipeed/picoclaw PR #3156`

## 4. 社区热点

今日最受关注的议题是 **Issue #3093**，该Issue请求增加对 **SimpleX** 或 **Tox** 等去中心化通信协议的支持。该问题目前已获得4条评论和1个👍，讨论热度持续。用户对去中心化、端到端加密的通讯协议表现出强烈兴趣，结合已提交的Delta Chat网关PR (PR #3063)，社区正在推动PicoClaw成为一个连接更多非传统、注重隐私的IM生态系统的桥梁。

- **讨论区：** `sipeed/picoclaw Issue #3093`

## 5. Bug 与稳定性

今日报告了一个新的Bug，同时有一个旧Bug被关闭，整体稳定性风险可控，但新Bug需重点关注：

- **中危：** **Issue #3153: [BUG] Volcengine Doubao Seed tool calls occasionally leak as `<seed:tool_call>` text** (新开)。该Bug影响使用火山引擎豆包模型的用户，在特定情况下，工具调用结果会以原始文本形式返回给用户，而非正确执行。这会导致AI助手输出异常的代码片段，严重影响用户体验。目前尚无对应的修复PR，需要开发团队尽快排查。
    - 链接: `sipeed/picoclaw Issue #3153`
- **已解决：** **Issue #3090: [BUG] Panel does not work on Safari on iOS versions below 16.4** (已关闭)。这是一个在旧版iOS Safari上无法使用控制面板的兼容性问题，已于今日关闭，说明该问题已被修复或标记为不再支持。

## 6. 功能请求与路线图信号

用户提出的功能请求主要集中在增强连接选项和提升模型使用体验上：

| 功能请求/信号 | 来源 | 分析 |
| :--- | :--- | :--- |
| **去中心化IM网关** | Issue #3093 | 用户希望集成SimpleX、Tox或Wire。结合PR #3063 (Delta Chat网关) 和讨论热度，**去中心化、隐私优先**的通信网关很可能是下一阶段的重点开发方向。实现一个后，很可能通过类似的模式扩展支持更多同类协议。 |
| **模型相关** | Issue #3153 | 火山引擎豆包模型的工具调用Bug暴露了用户对该特定模型或类似国产模型的深度使用需求。修复此Bug将是支持这些模型稳定运行的前提，后续也可能需要加强对此类模型的测试。 |

## 7. 用户反馈摘要

从今日的Issues评论中，可以提炼出以下用户反馈：

- **iOS兼容性痛点：** 用户 `3m377` 报告了旧版iOS Safari上的面板无法工作的问题。这表明部分用户仍在使用旧版操作系统，且对WebUI的跨平台兼容性有明确要求。虽然该问题已被标记为关闭，但可能意味着项目不再支持某些过时的浏览器版本。
- **模型工具调用问题：** 用户 `ms8great` 详细描述了火山引擎豆包模型工具调用失败的场景，并给出了清晰的复现步骤。这反映了用户在使用特定第三方模型时遇到了阻碍，且工具调用的稳定性是关键的用户体验痛点。

## 8. 待处理积压

以下Issue或PR处于待合并或长期未响应状态，提醒维护者关注：

- **待合入功能PR：** **PR #3063** (增加Delta Chat网关)、**PR #3163** (Bedrock提示缓存) 和 **PR #3156** (逐轮Token跟踪)。这三个PR已经准备就绪，且功能互补，建议尽快组织审查和合并，以推动下一版本的发布。
    - 链接: `sipeed/picoclaw PR #3063`
    - 链接: `sipeed/picoclaw PR #3163`
    - 链接: `sipeed/picoclaw PR #3156`

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 NanoClaw 项目 GitHub 数据生成的 2026-06-30 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-30

## 1. 今日速览
今日项目总体活跃度较高，呈现“修复与功能并进”的态势。虽然无新版本发布，但社区贡献活跃，共有7个 PR 处于活跃或合并状态。核心进展集中在**安全漏洞修复**（如符号链接逃逸）、**Discord 适配器的功能补全与问题修复**，以及**提高新用户设置体验**的优化。同时，一个关键的 Discord 附件丢失 Bug 被报告，热度较高，需要社区关注。

## 2. 版本发布
暂无。

## 3. 项目进展
今日有 2 个 PR 成功合并/关闭，解决了代码质量与功能完整性问题，使项目整体更稳定、完备。

- **[已关闭] #2882: fix(ncl): default messaging-groups create instance to channel_type**
  - **状态**: 已合并
  - **摘要**: 修复了 `ncl messaging-groups create` 命令因数据库 `NOT NULL` 约束失败的问题。开发者遗漏了 `instance` 字段的声明，导致 SQL 插入语句出错。
  - **影响**: 修复了一个直接导致用户无法通过 CLI 创建消息组的回归性Bug，保障了命令行工具的基础功能正常。
  - **链接**: [nanocoai/nanoclaw PR #2882](https://github.com/qwibitai/nanoclaw/pull/2882)

- **[已关闭] #2883: feat: voice-notify v3 意图分流 + kill-switch**
  - **状态**: 已合并
  - **摘要**: 完成了语音播报功能的第三次迭代升级，引入了意图分流和运行时关闭开关。现在播报会更智能，根据消息类型（如操作、静默、导航、技术状态、通知）进行差异化播报，并跳过代码块和长表格。
  - **影响**: 提升了语音通知的用户体验，减少了无效和冗余播报，提供了更好的可配置性（通过 `VOICE_SUMMARY_VERSION=off` 关闭）。
  - **链接**: [nanocoai/nanoclaw PR #2883](https://github.com/qwibitai/nanoclaw/pull/2883)

## 4. 社区热点

- **热点 Issue: [#2888] Discord (and likely other url-only chat-sdk adapters) drop image/file attachments**
  - **热度**: 今日唯一新开的 Issue，且有 1 条评论，显示该问题引起用户立即关注。
  - **分析**: 用户报告了一个严重且易复现的体验问题：在 Discord 上发送图片或文件时，Agent 只能看到文件名和元数据（`att.fetchData`），而无法访问实际内容。相比之下，Telegram 渠道工作正常。根因已指向 `chat-sdk-bridge.ts` 中的数据获取逻辑缺陷。
  - **诉求**: 用户的核心诉求是“一致性”。期望 Discord 能像 Telegram 一样，让 Agent 具备解析图片、文档等多模态输入的能力。这是一个影响广泛的通道能力缺失问题。
  - **链接**: [nanocoai/nanoclaw Issue #2888](https://github.com/qwibitai/nanoclaw/issues/2888)

- **高关注 PR: [#2884] feat(discord): add Discord channel adapter + fix Gateway approval-button routing**
  - **热度**: 虽然无直接评论，但其描述与 #2888 形成了直接关联。
  - **分析**: 该 PR 刚提交（创建于6月29日），旨在“添加Discord通道适配器”并“修复网关批准按钮路由”。这表明社区已经在积极解决 Discord 集成的问题，但 #2888 提到的附件内容是其中尚未覆盖的关键功能点。社区可能对如何整合这两个 PR 的更新有所讨论。
  - **链接**: [nanocoai/nanoclaw PR #2884](https://github.com/qwibitai/nanoclaw/pull/2884)

## 5. Bug 与稳定性

- **严重 Bug: Discord/URL-only Chat SDK 附件丢失**
  - **详情**: Issue #2888 报告。在 Discord 等渠道中，Agent 无法接收用户发送的图像或文件内容。
  - **严重程度**: **高**。直接破坏了核心的多模态交互能力，严重影响用户体验。
  - **是否有修复 PR**: **尚无**。目前仅有问题报告，尚未有关联的修复 PR。

- **安全漏洞修复 (待合并): PR #2880 - 收件箱符号链接逃逸**
  - **详情**: 修复 CWE-59 类型的漏洞（符号链接跟随攻击），防止被攻陷的 Agent 通过在其 Session 目录中预置符号链接，在主机侧写入文件时越权覆盖任意文件。
  - **严重程度**: **高**。直接涉及主机安全，是一个严重的安全加固。
  - **状态**: 已有修复 PR (#2880) 待合并。
  - **链接**: [nanocoai/nanoclaw PR #2880](https://github.com/qwibitai/nanoclaw/pull/2880)

- **配置Bug: 单Provider安装时，新注册Agent获取401错误**
  - **详情**: PR #2886 修复。当用户连接新渠道并选择“连接新 agent”时，系统总是使用内置默认 Provider，导致在单一Provider部署中配置不匹配而出现 401 认证错误。
  - **严重程度**: **中**。影响部署配置的灵活性，导致新用户在特定场景下直接失败。
  - **状态**: 已有修复 PR (#2886) 待合并。

- **功能Bug (已修复): `ncl messaging-groups create` 命令失败**
  - **详情**: PR #2882 修复。一个因数据库迁移未同步代码而导致的 `NOT NULL` 约束错误。
  - **严重程度**: **中**。导致 CLI 工具核心功能不可用。
  - **状态**: 已合并。

## 6. 功能请求与路线图信号

- **Discord 深度集成**: PR #2884（Discord 通道适配器 + 修复）和 Issue #2888（附件支持）共同指向社区对**稳定且功能完整的 Discord 集成**有强烈需求。这是项目在跨平台 Agent 协作方向上必须跨越的关键障碍。**预测**：此功能很可能成为下一个小版本（v0.x）的核心更新内容。

- **Slack Socket Mode 设置优化**: PR #2885 和 #2837 表明社区在持续改进 Slack 通道的易用性。该 PR 将 Socket Mode 的引导集成到了主流配置流程中，使得非技术用户也能更简单地设置 Slack 集成。这表明项目正朝着**更友好的用户体验**方向发展。
  
- **监控面板功能**: PR #2871（Dashboard Pusher with OpenCode support）展示了一个辅助功能的开发方向。该项目旨在通过 HTTP POST 方式将系统状态快照发送到监控仪表盘。虽然只是一个独立的推送器，但暗示了项目可能在未来**加强运维和可观测性**。

## 7. 用户反馈摘要

- **痛点**: **Discord 附件支持缺失是当前最明确的用户痛点**。用户 `eagansilverpathmarketing` 在 Issue #2888 中明确指出，Agent 在 Discord 中无法感知图片/文件内容，只能看到文件名，导致交互体验割裂。这表明即使基础通道能工作，若核心的多媒体支持缺失，用户仍会感到不满。
- **使用场景**: 从聚合的 PR 描述看，用户和开发者正在利用 NanoClaw 构建多渠道、多模式的 Agent，包括 Slack（Socket Mode）、Discord（Gateway Mode）、以及语音播报等场景。这说明用户群倾向于将 NanoClaw 作为**统一的 Agent 交互前端**。

## 8. 待处理积压

- **安全修复 PR #2880**: `fix(security): contain inbox symlink escapes in attachment writes (#2828)`
  - **等待时间**: 2 天
  - **重要性**: **高**。这是一个阻止潜在严重安全漏洞的修复，应被优先审查和合入。
  - **链接**: [nanocoai/nanoclaw PR #2880](https://github.com/qwibitai/nanoclaw/pull/2880)

- **核心功能扩展 PR #2871**: `feat(dashboard): add dashboard pusher with OpenCode support`
  - **等待时间**: 3 天
  - **重要性**: **中**。这是一个新功能，可能改变项目运维生态，需要仔细评估与现有架构的兼容性。
  - **链接**: [nanocoai/nanoclaw PR #2871](https://github.com/qwibitai/nanoclaw/pull/2871)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，这是 NullClaw 项目在 2026年6月30日的每日动态日报。

---

## NullClaw 项目动态日报 - 2026-06-30

### 1. 今日速览

项目今日活跃度中等，主要集中在代码库的质量提升和依赖更新上。**`Telegram` 通道在空闲后停止响应**的 Bug 报告（#972）是今日最值得关注的用户反馈，但尚未引起广泛讨论。**开发者 `vernonstinebaker` 提交了关于流式推理中原生工具调用（#971）和命令行交互优化（#970）的两个重要 PR**，显示项目正向更完善的用户体验迈进。此外，一个持续两周的 CLI 交互优化 PR（#960）已被合并，以及一个常规的 Docker 基础镜像升级 PR（#956）仍在等待审查。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日项目取得了实质性的代码进步，完成了一项重要的用户体验改进：

- **CLI 交互体验提升（已合并）**：由 `vernonstinebaker` 提交的 **PR #960** 已被合并。该 PR 为 `nullclaw agent` 的交互式 REPL 添加了一个小型的、无内存分配的行编辑器。现在用户在使用命令行模式时，可以正常使用方向键、Home/End 等按键进行历史命令导航和文本编辑，解决了过去控制字符直接打印在屏幕上的问题。这显著提升了终端用户的交互体验。
  - 链接：[PR #960](https://github.com/nullclaw/nullclaw/pull/960)

### 4. 社区热点

今日社区讨论较少，热度最高的是新提交的 Bug 报告：

- **Issue #972：Telegram 通道空闲后无响应**
  - 链接：[Issue #972](https://github.com/nullclaw/nullclaw/issues/972)
  - **作者反馈**：用户报告称，`Telegram` 通道在正常工作一天后，到第二天早晨就会“消亡”不再响应。但后端的 `nullclaw` 核心进程似乎仍在正常运行（执行 `ping` 命令能获得正常响应）。
  - **诉求分析**：该问题指向了一个潜在的**连接保活或会话管理缺陷**。用户推测是 Telegram API 侧断开了连接或 Token 过期，而 NullClaw 的 `Telegram` 通道适配器未能正确检测并重连。这是影响日常使用稳定性的关键问题，社区对此的关注度可能会逐渐升高。

### 5. Bug 与稳定性

今日报告的 Bug 严重程度为**高**，因为它直接影响了用户一种核心交互通道的可用性。

- **[高] Issue #972：Telegram 通道在空闲一段时间后停止响应**
  - **状态**：新开，待确认
  - **链接**: [Issue #972](https://github.com/nullclaw/nullclaw/issues/972)
  - **描述**：`Telegram` 通道在隔夜后无响应，后端进程状态正常。暂时无关联的修复 PR。

### 6. 功能请求与路线图信号

虽然没有直接的功能请求 Issue，但从今天提交的 PR 中，我们可以看出项目正朝着以下方向发展：

- **流式推理增强**：**PR #971** 提出的“原生工具调用”功能值得关注。它旨在解除流式传输过程对原生工具调用的限制。如果被合并，将允许支持原生工具的 AI 提供商（如某些 OpenAI 兼容服务）在流式输出时也能正确调用工具（如函数调用），而不是回退到较慢的“提示注入”格式。这有望优化延迟并提升流式响应质量。
  - 链接：[PR #971](https://github.com/nullclaw/nullclaw/pull/971)
- **开发者体验 (DX) 优化**：今日合并的 **PR #960** 和已提交的 **PR #970** 都聚焦于改善 CLI 工具的使用感受，表明项目维护者重视终端输入体验。

### 7. 用户反馈摘要

- **痛点**：用户 `i11010520` 报告了 `Telegram` 通道的不稳定性。从描述来看（“die away”），这对他/她的日常使用造成了明显中断。他/她已经确认后端服务本身是健康的，这将问题定位到了通道层的实现，是非常有价值的初步排查。
- **使用场景**：用户使用 NullClaw 通过 `Telegram` 进行交互，这通常用于个人助理或家庭自动化的通知与查询场景，通道稳定性至关重要。

### 8. 待处理积压

需要注意，有一个由自动化工具 `dependabot` 提交的依赖更新 PR 已等待超过两周且尚未被处理，建议维护者在安全窗口内及时审查：

- **[OPEN] PR #956：Docker 基础镜像 Alpine 版本从 3.23 升级至 3.24**
  - **状态**：开放中，等待审查
  - **创建时间**：2026-06-15
  - **链接**: [PR #956](https://github.com/nullclaw/nullclaw/pull/956)
  - **重要性**：虽然是常规依赖更新，但长期不合并可能导致项目构建环境与官方安全补丁脱节，建议尽快审查合并。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是为您生成的 LobsterAI 项目动态日报（2026-06-30）。

---

# LobsterAI 项目动态日报 | 2026-06-30

## 今日速览

今日项目活跃度**极高**，主要受 `2026.6.29` 版本发布驱动。过去24小时内，项目经历了密集的代码合并和问题修复流程，共处理了 **40 条 PR**，其中 **39 条已合并/关闭**，显示出高效的迭代节奏。社区反馈主要集中在 **OpenClaw 集成稳定性**与**用户交互体验问题**，而本次新版本正有针对性地解决了多个关键稳定性 Bug。整体来看，项目正处于一个快速迭代、重点修复核心功能的良性发展阶段。

## 版本发布

### [LobsterAI 2026.6.29](https://github.com/netease-youdao/LobsterAI/releases/tag/v2026.6.29) （2026-06-29 发布）

本次版本是针对 OpenClaw 模块和协作体验的一次重要稳定性更新，并未引入破坏性变更，用户可以平滑升级。

**主要更新内容：**

- **OpenClaw 集成稳定性提升**：
    - **修复 Agent 身份/记忆分裂问题**：修复了在特定场景下 Agent 的引导空间 (bootstrap workspace) 与任务工作目录 (task cwd) 混淆的 Bug。
    - **保留用户轮次缓存**：优化了用户会话缓存的稳定性，减少了因序列化问题导致的对话中断。
    - **保留定时任务(Cron)运行历史**：改进了定时任务历史记录的同步逻辑，避免重复或破坏性替换。
    - **插件审批权限路由**：将插件审批流程正确路由到 Cowork 权限系统。

- **协作功能 (Cowork) 修复**：
    - **清理导航轨道预览**：修复了对话导航轨道上不必要的预览内容显示。
    - **恢复对话轨道修复**：针对发布流程中的意外回滚，重新应用并恢复了对话轨道的导航、悬停样式和懒加载功能。

**迁移注意事项：** 无。

## 项目进展

本次版本发布及相关的合并 PR 标志着项目在 **核心稳定性和基础体验** 上迈出了重要一步。

- **OpenClaw 深度修复**：项目团队通过一批高度关联的 PR（如 [#2227](https://github.com/netease-youdao/LobsterAI/pull/2227), [#2219](https://github.com/netease-youdao/LobsterAI/pull/2219), [#2220](https://github.com/netease-youdao/LobsterAI/pull/2220)）系统性地解决了 OpenClaw 集成中的多个稳定性问题，涵盖了 Agent 状态保持、任务执行上下文隔离、以及定时任务的一致性。这表明项目正在努力将 OpenClaw 打造成一个更可靠的 AI Agent 运行时。
- **协作体验迭代**：通过 [#2222](https://github.com/netease-youdao/LobsterAI/pull/2222) 及其相关回滚和重应用 PR，团队展示了严谨的发布流程。最终修复了对话轨道的视觉和交互体验，包括清理预览、增加显示长度，提升了后台协作的易用性。
- **IM 插件生态扩展**：合并了 [#2182](https://github.com/netease-youdao/LobsterAI/pull/2182) 和 [#2198](https://github.com/netease-youdao/LobsterAI/pull/2198) 等 PR，升级并预装了包括 **钉钉、飞书、企业微信、QQ、Discord** 在内的多个 IM 插件，降低了用户接入多平台的成本，扩展了 OpenClaw 的应用场景。

## 社区热点

- **#2079 [执行结果窗口滚动到顶端会假死](https://github.com/netease-youdao/LobsterAI/issues/2079)**
    - **诉求分析**：这是一个可复现的、影响核心操作流程的严重Bug。用户无法在任务执行完毕后正常查看结果，极大地影响了使用体验。该 Issue 从5月30日提出至今未被修复，是社区关注的焦点。
- **#2121 [重复输出文字浪费 Token](https://github.com/netease-youdao/LobsterAI/issues/2121)**
    - **诉求分析**：用户对 Token 消耗非常敏感。此 Issue 报告了“Claw”可能存在的重复输出问题，直接关联到用户的经济成本。用户急切希望明确这是 Bug 还是配置问题，并寻求解决方案。
- **#2120 [任务预输入与时长优化建议](https://github.com/netease-youdao/LobsterAI/issues/2120)**
    - **诉求分析**：该 Issue 包含多项与开发者工作流相关的建议，涉及任务连续性、运行时长和UI优化。尤其是“预输入任务”和“延长单次任务超时”的诉求，表明用户正将 LobsterAI 用于更复杂的、长时间运行的数据处理任务，并希望工具能更好地支持此类开发场景。

## Bug 与稳定性

按严重程度排列：

1.  **严重** [#2079 执行结果窗口滚动到顶端会假死](https://github.com/netease-youdao/LobsterAI/issues/2079)
    - **状态**：未关闭，已有一定的讨论。目前无关联的修复 PR。
    - **影响**：阻断用户查看任务输出，是严重的产品质量问题。
2.  **中高** [#2121 重复输出文字浪费 Token](https://github.com/netease-youdao/LobsterAI/issues/2121)
    - **状态**：未关闭，用户寻求确认是否是 Bug。
    - **影响**：导致用户Token被浪费，增加使用成本，损害产品口碑。
3.  **一般** [#1386 分享长图内容不全](https://github.com/netease-youdao/LobsterAI/issues/1386)
    - **状态**：长期未关闭（Stale），无相关修复 PR。
    - **影响**：影响内容分享功能的完整性，降低社交传播体验。
4.  **一般** [#1390 定时任务无法更新（偶现）](https://github.com/netease-youdao/LobsterAI/issues/1390)
    - **状态**：长期未关闭（Stale），无相关修复 PR。
    - **影响**：自动化任务管理功能的核心交互受阻，影响中度用户。

**特别关注**：虽然 [#1434](https://github.com/netease-youdao/LobsterAI/issues/1434) 和 [#1389](https://github.com/netease-youdao/LobsterAI/issues/1389) 等国际化问题已被标记为“Stale”后关闭，但 [#1389](https://github.com/netease-youdao/LobsterAI/issues/1389) 仍然为 Open 状态，与国际用户体验相关，需要维护者关注。

## 功能请求与路线图信号

- **#2131 [支持 hermes agent](https://github.com/netease-youdao/LobsterAI/issues/2131)**
    - **信号**：用户对集成第三方 Agent 框架（hermes）有明确需求。这为 LobsterAI 的生态扩展提供了方向。
- **#2120 [任务预输入与运行时长优化](https://github.com/netease-youdao/LobsterAI/issues/2120)**
    - **信号**：反映了用户从“单次对话”向“持续工作流”转变的需求。建议中提到的“任务队列”和“延长执行时间”很可能成为未来优化方向，尤其对于数据处理等长耗时场景。结合近期对于 OpenClaw 定时任务的修复，该功能被纳入下一版本的概率较高。
- **UI 布局优化**：在[#2120](https://github.com/netease-youdao/LobsterAI/issues/2120)中，用户基于自己的高分辨率屏幕提出了UI布局的改进建议（如调整技能界面为3列），这表明用户对沉浸式和可定制的界面有期待。

## 用户反馈摘要

通过分析 Issues 评论，可以提炼出以下真实用户声音：

- **痛点**：
    - **“任务执行器假死”**：`fcinfo` 用户报告在5月27日后版本中操作结果窗口时会假死，这是一个明确且令人沮丧的体验问题。
    - **“Token被浪费”**：`nbjoe` 用户正在用 Claw 监控脚本，对重复输出导致的额外Token消耗非常在意，并提出了“脚本还在进行但监控停止了”的问题，涉及任务超时机制。
    - **“积分月底清零”**：`zjk648491625` 用户对订阅积分月底清零的规则感到惊讶和不满，为商业模式和积分策略敲响了警钟。
- **使用场景**：
    - **数据库监控**：用户正在使用 LobsterAI 运行数据获取脚本，并将其用于长时间监控任务，显示其在自动化运维领域的潜力。
- **期望**：
    - **无缝工作流**：用户希望能在任务运行时预输入下一个任务，以提升连续性。
    - **更稳定的长时间任务**：用户不希望任务因系统默认超时而被打断。

## 待处理积压

- **[#2079] [OPEN] 执行结果窗口滚动到顶端会假死**
    - **标签**：严重Bug
    - **说明**：自5月30日提出，已有近一个月未修复。此Bug严重影响用户体验，应作为最优先处理事项。
    - **链接**：https://github.com/netease-youdao/LobsterAI/issues/2079

- **[#1388] [OPEN] [stale] 邮箱配置-点击测试连通性后，一直没反应**
    - **标签**：Stale, 中型Bug
    - **说明**：一个长期的待处理问题，涉及核心功能（邮箱集成）的不可用。尽管被标记为 Stale，但未关闭，说明尚未被彻底解决。
    - **链接**：https://github.com/netease-youdao/LobsterAI/issues/1388

- **[#1386] [OPEN] [stale] 【会话-分享】分享长图内容不全**
    - **标签**：Stale, 中型Bug
    - **说明**：与用户分享体验直接相关的长期问题，建议优先排期修复。
    - **链接**：https://github.com/netease-youdao/LobsterAI/issues/1386

- **[#1277] [OPEN] chore(deps-dev): bump the electron group...**
    - **标签**：Dependency Update (Dependabot)
    - **说明**：由 Dependabot 提出的依赖更新 PR，已存在近3个月未合并。虽然不会直接影响运行时功能，但长期不合并可能导致安全隐患和兼容性问题。建议定期审查并合并此类依赖更新。
    - **链接**：https://github.com/netease-youdao/LobsterAI/pull/1277

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据提供的CoPaw (QwenPaw) 项目数据，为您生成2026年6月30日的项目动态日报。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-06-30

## 1. 今日速览

今日项目活跃度极高，社区贡献踊跃。过去24小时内，项目共产生**29条Issue**和**50条PR**，开发者与用户之间的互动非常频繁。虽然无新版本发布，但PR池中积累了**32条待合并请求**，表明大量功能修复和新特性正处于临界点，亟待合并。社区讨论焦点集中在**模型兼容性（DeepSeek）、工具调用UI显示、以及IM通道集成**等实际使用痛点上。整体来看，项目生态健康，社区参与度高，但维护者面临较大的PR审查和合并压力。

## 2. 版本发布

（无新版本发布）

## 3. 项目进展

今日有**18条PR**被合并或关闭，标志着项目在多个方面取得实质性进展：

- **Bug修复**:
    - **[PR #5628]**: 修复了工具调用结果卡片计数始终显示为1的Bug (`#5624`)，通过统一使用标准化显示文本来统计行数，确保了`read_file`、`glob_search`等工具计数正确。
    - **[PR #5601]**: 修复了IM通道（如飞书、企业微信）无法收到工具审批通知的问题，通过在基础通道中添加`send_approval_notification`方法，恢复了审批事件的通知功能。
- **文档与架构**:
    - **[PR #5614]**: 更新了上下文管理文档，将原来的“背包”类比替换为“滚动策略”解释，并详细记录了新的滚动上下文实现、架构及存储布局。
    - **[PR #5621]**: 在安全文档中新增了“沙箱”章节，详细说明了内核级执行隔离的工作原理、支持平台（macOS Seatbelt, Linux Bubblewrap）以及与工具/文件防护的关系。
- **核心功能迭代**:
    - **[PR #5515]**: 更新了`@agentscope-ai/chat`依赖至最新beta版本，启用了新一代聊天UI能力，包括用户消息导航锚点变体。

## 4. 社区热点

今日最热门议题主要集中在模型兼容性和稳定性上，反映出社区对模型服务成本和容错的高度关注。

1.  **[Issue #3891]**: DeepSeek 前缀缓存命中率偏低（~95%），优化空间巨大
    - **热度**: 5条评论，获👍1个。
    - **链接**: `agentscope-ai/QwenPaw Issue #3891`
    - **诉求详情**: 该Issue深度剖析了使用QwenPaw接入DeepSeek模型时，前缀缓存命中率仅为95%所带来的巨大成本差异（缓存未命中成本是命中的4-10倍）。用户期望能优化缓存策略，降低API调用成本。这反映了用户在选择模型时对**成本效益**的高度敏感。

2.  **[Issue #5573]**: DeepSeek V4 thinking 模式在 OpenAI 兼容端点上的两类 400 错误
    - **热度**: 3条评论。
    - **链接**: `agentscope-ai/QwenPaw Issue #5573`
    - **诉求详情**: 用户发现通过非官方OpenAI兼容端点使用DeepSeek V4时，存在两类400错误：流式传输中`reasoning_content`缺失未兜底、工具Schema中`null`类型未清洗。该Issue由用户“豆包2.1pro”生成，并附带了实际验证后的修改方案，体现了社区高度的**自愈能力**和**问题解决导向**。

3.  **[Issue #4873]**: 同时开两个subagent会导致主agent无限快速轮询
    - **热度**: 3条评论。
    - **链接**: `agentscope-ai/QwenPaw Issue #4873`
    - **诉求详情**: 用户描述了同时启动两个后台subagent任务会导致主agent高频轮询、消耗大量LLM请求，且无法从飞书侧打断。这直接影响了**多任务并发**和**IM通道交互**的体验，是用户在使用复杂自动化工作流时的核心痛点。

## 5. Bug 与稳定性

今日报告的Bug数量较多，以下是按严重程度排列的关键问题：

- **严重 (影响核心功能)**:
    - **[Bug #4873]**: 同时启动两个SubAgent导致主Agent无限快速轮询，影响任务正常执行与中断。
        - **状态**: 已有 **PR #5633** 和 **PR #5524** 尝试修复。
    - **[Bug #5573]**: DeepSeek V4在非官方OpenAI端点上的流式数据和Schema类型错误，可能导致对话中断或请求失败。
        - **状态**: 讨论中，用户已提供初步修复思路。
    - **[Bug #5561]**: 飞书机器人回复长信息失败，只能以文件形式发送。影响IM通道基本可用性。
        - **状态**: 讨论中。

- **中等 (影响特定功能/用户体验)**:
    - **[Bug #5587]**: Qwen-Image Tool安装错误。
        - **状态**: 讨论中。
    - **[Bug #5624/#5626]**: 工具调用结果卡片计数始终显示为1（前端显示问题，已修复）。
        - **状态**: **已修复**，对应PR #5628和#5632。
    - **[Bug #5505]**: MiniMax-M3图片安全审核错误导致后续视觉请求被错误缓存并剥离。
        - **状态**: **已关闭** (修复合并)。

## 6. 功能请求与路线图信号

用户提出了多项功能请求，与项目发展方向高度相关：

- **高优先级 / 可能纳入近期版本**:
    - **[Feature #5572]**: **支持模型自动降级**：当主模型配额耗尽、调用失败或超时，自动切换到备选模型。该请求直接关联到用户对服务稳定性和连续性的核心需求，且已有多个讨论。已有 **PR #5527** (动态切换) 及 **PR #5571** 相关讨论，是v2.0.0路线图中的重要考量。
    - **[Feature #5342]**: **执行层工具结果硬上限**：作为防御上下文爆炸的深度防御，防止LLM调用失败时工具结果无限累积。已有 **PR #5510** 进行实现，表明维护者已采纳此建议。

- **中优先级 / 社区呼声高**:
    - **[Feature #5615]**: **纯文本模型支持图片自动转文字描述**：使用备用视觉模型自动为纯文本模型描述图片，极大地提升了用户使用不同模型时的无缝体验。
    - **[Feature #5588]**: **记忆搜索支持专用Reranker模型**：实现两阶段检索，提升记忆搜索精度。
    - **[Feature #5630]**: **支持自定义Telegram BaseURL**：满足部分地区用户访问Telegram的本地化需求。

## 7. 用户反馈摘要

- **痛点与不满意**:
    - **模型成本与稳定性**: `#3891` 对DeepSeek缓存命中率不满，`#5573` 对特定模型的兼容性问题感到困扰，`#5572` 则反映了因模型单点故障导致任务中断的普遍焦虑。
    - **IM协作体验**: `#4873` 和 `#5561` 反映了SubAgent任务管理和飞书长消息发送方面的糟糕体验，用户期望更稳定、更直观的IM交互。
    - **性能与卡顿**: `#5555` 用户直接抱怨“越来越卡顿了”，同时 `#5591` 用户对控制台日志中大量的`GET /api/console/inbox/events`请求感到烦躁，提示前端性能或API调用逻辑可能存在优化空间。
- **满意与期望**:
    - **社区参与度高**: 用户 `Zhanyuan23333` (`#5573`) 不仅报告了问题，还通过“豆包”生成了修复代码并验证，体现了社区强大的技术力量和共建热情。
    - **文档期盼**: `#5621` 沙箱文档和 `#5614` 上下文管理文档的更新，表明用户关注项目的**安全机制**和**核心技术原理**，并对此类系统性文档有明确需求。

## 8. 待处理积压

- **[Issue #2587]**: 长期存在的关于性能或具体功能的问题（假设）。**说明**：老Issue待处理。
- **[PR #5442]**: `fix(mission): integrate mission mode with Runtime v2 architecture`. 此PR试图连接“任务模式”与新的架构，但已存在6天仍未合并，可能遇到架构冲突或需要更多审查。建议维护者关注其进展，避免与其他架构重构类PR产生严重冲突。
- **[PR #5438 & #5434]**: 两个大型前端单元测试PR（M3-B和M3-A），覆盖了Inbox和Settings等核心模块，累计超过300个测试用例。虽已存在一周，但合并优先级可能低于功能修复。建议尽早合并以提升代码库质量属性，并为后续重构提供安全保障。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeroClaw 项目 2026-06-30 的数据，现为您呈上项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-30

## 1. 今日速览

ZeroClaw 项目今日呈现**极高活跃度**，过去 24 小时内产生了 50 条 Issue 更新与 50 条 PR 更新。社区在核心功能（智能体循环、工具调用、提供商适配）和安全性（OWASP 集成、WASM 沙箱）上讨论激烈，表明项目正处于向 **v0.8.2 和 v0.8.3** 版本冲刺的关键阶段。尽管暂无新版本发布，但大量 PR 的提交与修复（特别是针对 OpenAI 兼容性的兼容性修复）显示团队正在积极解决用户反馈的痛点。今日的讨论焦点集中在 **系统提示词与工具列表的一致性**、**WASM 插件运行时** 以及 **OpenAI 推理模型（Reasoning）集成** 上。

## 2. 版本发布

无。

## 3. 项目进展

今日关闭/合并的 PR 较少，但有一项关键修复值得关注：
- **修复 OpenAI 兼容提供商工具调用问题**：PR [#8512](https://github.com/zeroclaw-labs/zeroclaw/pull/8512) 修复了在与严格的 OpenAI 兼容后端（如 llama.cpp）交互时，因 `tool_calls` 消息中的 `content` 字段为空字符串 `""` 而非 `null` 导致的 `400 Bad Request` 错误。该 PR 虽未合并，但其修复方向（*omit empty assistant tool-call content*）直接回应了社区长期以来的使用瓶颈。
- **基础设施与持续集成（CI）增强**：PR [#8129](https://github.com/zeroclaw-labs/zeroclaw/pull/8129) 和 [#8485](https://github.com/zeroclaw-labs/zeroclaw/pull/8485) 均在积极开发中。前者将 `cargo audit` 集成至 PR 门禁，后者则试图统一并优化 Docker 镜像构建流程。这表明项目在功能迭代的同时，非常重视工程化和供应链安全。

## 4. 社区热点

1.  **高热度 Issue: 系统提示词与工具列表不匹配**
    - **Issue** [#8054](https://github.com/zeroclaw-labs/zeroclaw/issues/8054)（评论 9）: 用户 `perlowja` 提交的核心 Bug。问题在于，当通过不同入口点（WebSocket、网关、/think 端点）与智能体交互时，系统提示词中的工具可用性与实际提供给模型的工具集不一致。这直接影响了诸如 Claude 等推理模型的行为，因为它们会依赖系统提示词来判断自己是否拥有工具。该 Issue 是 [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) 的延续，说明这是一个顽固且广泛存在的问题。

2.  **具有挑战性的 RFC: 桌面电脑使用（Computer-use）能力**
    - **RFC** [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)（评论 6）: 社区成员 `NiuBlibing` 提出的重磅功能请求。希望 ZeroClaw 的智能体能像 OpenAI Codex 或其他类似项目一样，具备控制本地桌面的能力（截屏、模拟鼠标键盘）。这标志着用户不再满足于纯文本或 API 交互，开始追求更高级的 AI 代理能力。

**诉求分析**: 社区当前的深层诉求集中在 **“智能体的上下文感知一致性”** 与 **“扩展智能体的物理世界互动能力”**。前者从 #8054 可见一斑——用户希望 ZeroClaw 作为一个框架，能解决不同入口点、不同模型、不同模式（工具调用与非工具调用）下的上下文割裂问题；后者则反映在 #6909 中，用户希望将代理能力从“聊天/编码”扩展到“桌面自动化”这一更广阔的应用场景。

## 5. Bug 与稳定性

**严重程度：高 (P1)**

- **Issue [#5600]**: **使用 kimi-code 提供商进行流式工具调用报错**。S1 工作流阻塞，当启用 thinking 功能时，API 返回 `400 Bad Request`，提示 `reasoning_content` 缺失。**（无相关修复 PR）**
- **Issue [#8054]**: **系统提示词中的工具信息不匹配**。S1 工作流阻塞，影响所有入口点。紧随 PR [#8053] 修复后的补充，是一个更深层次的设计问题。
- **Issue [#8505]**: **Telegram 频道无法配置**。S1 工作流阻塞，用户使用 quickstart 后，Telegram bot 无响应。**（无相关修复 PR）**

**严重程度：中 (P2)**

- **Issue [#8410]**: **频道任务缺少“无回复”状态**。S2 降级行为，导致本应静默的后台任务（如“检查新邮件，没有则保持沉默”）依然会发送一条可见回复。
- **Issue [#7904]**: **`always-inject` 技能标记在紧凑提示模式下失效**。S2 降级行为，影响了依赖特定技能前置注入的高级用户。
- **Issue [#8334]**: **`zeroclaw skills install` 命令在多代理环境下找不到正确的 `data_dir`**。S2 降级行为，导致新用户“即装即用”的体验受损。

**总体情况**：今日报告的 Bug 数量较多，但半数以上有对应的 Issue 或 PR 在进行跟踪。P1 级别的 Bug 主要集中在 **提供商兼容性** 和 **运行时上下文一致性** 上，这是项目成熟度提升过程中的典型痛点。

## 6. 功能请求与路线图信号

- **Agent-to-Agent (A2A) 发现协议**：RFC [#7218] 提议定义 `/.well-known/agent-card.json` 规范，以实现多智能体发现。结合讨论，该功能大概率会被纳入 **v0.8.3** 路线图。
- **桌面计算机使用**：RFC [#6909] 虽未直接关联到 PR，但代表了未来扩展方向。由于涉及底层输入控制，实现复杂度高，可能作为 **v0.9.0** 或更高版本的候选功能。
- **Web 看板内应用升级**：RFC [#8170] 提议的从 Web 看板直接进行应用重启升级的功能已有对应的 PR [#8173] 在开发中。这极有可能被纳入 **v0.8.2** 或 **v0.8.3**。

## 7. 用户反馈摘要

- **痛点**:
    - **OpenAI 兼容服务/本地模型兼容性差**：Issue #5600、#7756 和 PR #8512 均体现了用户在使用非 OpenAI 官方 API（如 kimi, llama.cpp）时遇到的各类兼容性问题，尤其是针对新特性（如 `reasoning`）。框架在兼容性方面仍有提升空间。
    - **配置与管理复杂**：Issue #8505 表明，即使是按文档操作（quickstart），用户也难以成功配置频道。Issue #8334 则反映了 CLI 工具在复杂部署场景下的配置逻辑缺陷。配置层仍是新用户的主要门槛。
- **满意点**:
    - 社区对 **WASM 插件系统**的进展反应积极，RFC [#6140]、#7497、#8135 和 PR #8491 讨论热烈且具建设性，表明开发者社群对这一新架构寄予厚望。
    - 对 **OWASP 集成** 类功能（如 Issue #8056、#8057 和 PR #8129）表示欢迎，认为项目在安全合规方面迈出了重要一步。

## 8. 待处理积压

1.  **Issue [#6074]**: **审计丢失的 153 个提交**。这是一个长期遗留的审计任务，优先级 P2。虽然暂时不影响功能，但为了项目健康和代码可追溯性，提醒维护者尽快安排时间进行梳理和恢复规划。
    - Link: [https://github.com/zeroclaw-labs/zeroclaw/issues/6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)
2.  **Issue [#5600]**: 使用 kimi-code 提供商的流式工具调用报错。这是一个 S1 阻塞性 Bug，已存在多日（创建于 4 月 10 日），且目前无直接修复 PR。对于 kimi 提供商的使用者来说，该问题严重影响使用体验。
    - Link: [https://github.com/zeroclaw-labs/zeroclaw/issues/5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)
3.  **PR [#8149]**: 解决 WASM 插件主机中 Mutex 因 panic 而被毒死 (poison) 的问题。该 PR 标记为 `needs-author-action`，但修复了插件稳定性中一个非常关键的问题。如果作者未能及时响应，建议维护者考虑接手或关闭此 PR。
    - Link: [https://github.com/zeroclaw-labs/zeroclaw/pull/8149](https://github.com/zeroclaw-labs/zeroclaw/pull/8149)

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*