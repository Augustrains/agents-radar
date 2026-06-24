# OpenClaw 生态日报 2026-06-24

> Issues: 187 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-24 01:58 UTC

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

好的，根据您提供的 OpenClaw 项目 GitHub 数据，我为您生成了 2026-06-24 的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-24

## 1. 今日速览

今日 OpenClaw 项目活跃度 **极高**。过去24小时内产生近700条议题与合并请求更新，其中新开活跃议题138条，待合并的Pull Request积压高达466条。社区在持续发现和报告严重Bug的同时，也涌现了大量功能需求和技术讨论，特别是在会话状态持久化、模型兼容性和系统稳定性方面。尽管无新版本发布，但大量待处理的PR表明核心团队与社区贡献者正在积极修复问题和推进新功能，项目进入高强度的迭代与维护期。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日有 **34** 个Pull Request被合并或关闭，主要进展集中在以下几个方面：

- **核心稳定性修复**：多个关于会话状态丢失、子代理死锁、状态迁移失败等关键问题的PR被合并，如修复子代理在中断后释放锁的`#95833`关联PR，以及解决跨后端模型切换上下文丢失的关联PR。
- **功能集成与优化**：一个重大的实时语音扩展（`#96173`）被提出，新增了本地实时语音和听写支持。同时，针对记忆索引、Telegram频道响应、Cron任务中断处理等问题均有修复PR被合并。
- **插件与SDK完善**：为插件SDK新增了`inbound_activity`钩子（`#79855`），并修复了插件钩子和工具闭包状态保存问题（`#78075`），增强了第三方开发能力。

## 4. 社区热点

今日社区讨论最热烈的问题集中在以下几个方面：

1.  **核心会话SQLite迁移** (#88838): 该议题以 **35条评论** 高居榜首。开发者们深入探讨了通过“accessor seam”方式将核心会话/转录文件迁移至SQLite的第三阶段方案。用户关注点在于迁移过程的平滑性、数据一致性以及对现有工作流的影响。该议题仍处于开放状态，表明这是一个长期且复杂的核心架构变更。
2.  **iMessage响应延迟追踪** (#96148): 以 **17条评论** 紧随其后。社区正在追踪并试图重现iMessage源回复的延迟问题，并评估新引入的检测手段的有效性。这表明用户对消息传递的实时性有较高要求。
3.  **Anthropic思考块签名无效** (#92201): 此Bug收到 **14条评论**。用户报告在Slack插件中，从Anthropic流式传输的“thinking”签名块在重放时间歇性失效，并且由于错误信息被泛化，导致恢复机制失效。这暴露了与第三方模型交互时数据一致性和错误处理上的缺陷。
4.  **Cron定时器全局状态污染** (#90991, 已关闭): 此问题虽已关闭，但讨论热度不减。用户通过详细的环境描述和复现步骤，指出Cron定时器触发会污染全局运行时状态，造成系统级过载。该问题的关闭通常意味着修复已被合并或已找到解决方案。

## 5. Bug 与稳定性

今日报告的Bug数量众多，按严重程度排列如下：

- **P1 级别（严重）**:
    - [嵌入式代理：流式Anthropic思考块签名无效，恢复逻辑因错误泛化而失效](https://github.com/openclaw/openclaw/issues/92201) (评论: 14)
    - [180秒压缩超时设计缺陷，导致合法长压缩任务反复失败](https://github.com/openclaw/openclaw/issues/92043) (评论: 10)
    - [子代理完成投递失败，因请求者会话非活跃且转录被锁定](https://github.com/openclaw/openclaw/issues/92076) (评论: 8)
    - [卡住会话恢复机制错误地中断长时间运行但活跃的代理](https://github.com/openclaw/openclaw/issues/88870) (评论: 6)
    - [原生Anthropic路径回放历史“thinking”块会损坏长工具调用线程](https://github.com/openclaw/openclaw/issues/94228) (评论: 5)
    - **[锁未释放Bug]子代理中止过程未能释放`.jsonl.lock`，导致会话永久损坏** (https://github.com/openclaw/openclaw/issues/95833) (评论: 4，**已有修复PR**)

- **P2 级别（中等）**:
    - [Ollama远程提供商在聊天会话中无法消费流式数据](https://github.com/openclaw/openclaw/issues/94251) (评论: 5)
    - [DeepSeek V4 Flash 产生不完整回合](https://github.com/openclaw/openclaw/issues/88657) (评论: 10)
    - [Telegram 的富文本消息破坏段落分隔和表格渲染](https://github.com/openclaw/openclaw/issues/95554) (评论: 4)
    - [自动更新后，运行的网关可能引用旧的哈希包导入](https://github.com/openclaw/openclaw/issues/85844) (评论: 6)
    - **[6.9版本回归]Dreaming功能运行但不提升记忆，UI显示异常** (https://github.com/openclaw/openclaw/issues/96118，**已关闭**)
    - [6.x版本状态迁移导致频道会话存储SQLite为空，破坏主动消息发送](https://github.com/openclaw/openclaw/issues/94939) (评论: 3)
    - [DeepSeek缓存命中率在6.x版本升级后低于10%](https://github.com/openclaw/openclaw/issues/94518) (评论: 3)

## 6. 功能请求与路线图信号

今日涌现的新功能请求，结合已有PR，预示着未来版本的演进方向：

- **实时语音与交互**: `#96173` PR 提出了“本地实时语音扩展”，这是一个重大信号，表明社区对原生、自托管的实时语音交互功能有强烈需求。未来的`local-realtime-voice`扩展很可能成为官方支持的选项。
- **系统优化与管理**:
    - [允许压缩提供商是MCP服务器](https://github.com/openclaw/openclaw/issues/96156): 该请求将内存压缩功能从插件扩展到MCP，大幅提升了灵活性和可定制性，可能是下个版本关于Memory插件重构的重要方向。
    - [工作板卡片删除/移除API](https://github.com/openclaw/openclaw/issues/92314): 反馈了Workboard插件管理能力的不足，亟需补充删除功能。
    - [支持全局SSRF策略配置](https://github.com/openclaw/openclaw/issues/93068): 用户希望有一个统一的入口来管理网络访问策略，这可能推动一个安全治理层的抽象。
    - [会话命名功能](https://github.com/openclaw/openclaw/issues/93422): `/label`和`/new <name>`命令的请求表明用户在多会话管理场景下的痛点，该功能有望在WebChat/Control UI中实现。
- **跨平台与第三方集成**:
    - [升级Cloudflare AI Gateway提供商至REST API](https://github.com/openclaw/openclaw/issues/91945): 用户主动要求跟进厂商API变更，这体现了社区对维护和更新集成能力的积极性。
    - [Telegram引用/回复作为一等公民](https://github.com/openclaw/openclaw/issues/88032): 用户希望Telegram的引用回复功能能成为一个持久、稳固的交互契约，而非临时补丁。

## 7. 用户反馈摘要

从今日的议题和评论中，可以提炼出用户的核心反馈：

- **痛点聚焦**:
    - **“莫名其妙就坏了”**：用户在谈论`#92201`（Anthropic签名无效）和`#92043`（压缩超时）等问题时，表达了因错误信息不明确（被泛化导致恢复失效）而产生的困惑和挫败感。错误处理和用户提示的清晰度亟待提升。
    - **“升级有风险”**：`#94251`（Ollama流式消费失败）、`#94939`（状态迁移导致SQLite空）、`#94518`（DeepSeek缓存命中率骤降）等议题表明，版本升级是当前用户最大的稳定性风险点。用户反馈多集中在“升级前能工作，升级后反而坏了”。
    - **“长任务不可靠”**：`#92043`（压缩超时）、`#95833`（子代理锁未释放）、`#88870`（错误中断长代理）等问题反复出现，表明系统中涉及长时间运行的任务（如深度分析、长文档处理）的执行和恢复机制非常脆弱，用户失去耐心。

- **使用场景**:
    - **工作助理与自动化**: 用户使用OpenClaw处理深度代码审查、多步骤工作流等复杂任务（`#88870`）。
    - **跨平台通信中枢**: 多个用户同时使用Feishu、Telegram、Discord、MS Teams等多个渠道与OpenClaw交互，对消息的实时性、格式正确性和上下文连续性要求极高。
    - **模型多样性与成本控制**: 用户积极探索DeepSeek、Ollama、NVIDIA Build等成本更低的替代模型，但对兼容性和性能（如缓存命中率）高度敏感。

## 8. 待处理积压

以下议题和PR长期未得到响应或解决，建议维护团队重点关注：

- **安全相关**:
    - [`exec`私有局域网访问失败](https://github.com/openclaw/openclaw/issues/94032) (P2, 评论: 7): 用户提出的`exec`命令无法访问局域网主机的问题，涉及网络隔离与安全边界，需要安全审查。
    - **[RFC] Agent调度API与非伪造来源** (https://github.com/openclaw/openclaw/issues/71712) (P2, 评论: 5): 这是一个涉及安全与功能增强的重要提议，讨论了近两个月，需要产品决策。
    - [工具错误信息应包含失败原因和重试确认](https://github.com/openclaw/openclaw/issues/46548) (P2, 评论: 5): 长期存在的用户体验问题，至今“等待维护者审查”。

- **功能请求**:
    - [跨后端模型切换时保留对话上下文](https://github.com/openclaw/openclaw/issues/79047) (P2, 评论: 5): 这是一个非常有价值的跨平台特性，但方案复杂，需要产品层面的深入讨论。
    - [支持全局SSRF策略配置](https://github.com/openclaw/openclaw/issues/93068) (P2, 评论: 3): 用户明确提出了改进网络策略管理的需求。

- **长期未解决问题**:
    - [为Control UI添加MathJax/LaTeX支持](https://github.com/openclaw/openclaw/issues/42840) (P2, 评论: 8): 创建于三个月前，获得7个赞，是社区呼声较高但一直被搁置的功能请求。
    - [让压缩提供商可以是MCP服务器](https://github.com/openclaw/openclaw/issues/96156) (P2, 评论: 3): 这是一个极具创新性的提议，但技术实现和范围影响较大，需要维护者评估。

---

## 横向生态对比

好的，作为资深技术分析师，现根据您提供的 2026-06-24 各项目动态，为您呈现一份横向对比分析报告。

---

### **2026-06-24 个人 AI 智能体与开源助手生态横向分析报告**

#### **1. 生态全景**

当前个人 AI 智能体与助手开源生态正处于 **“高强度的功能迭代与质量打磨并存”** 的关键阶段。整个生态呈现出两大核心特征：**一是社区贡献极为活跃**，各项目周均 PR 和 Issue 数量居高不下，表明开发者对自托管、高可控的 AI 助手方案有强烈且持续的兴趣；**二是用户需求已从“能否工作”转向“能否稳定、安全、低成本地工作”**。性能优化（Token 开销）、系统可靠性（锁竞争、状态持久化）以及安全治理（供应链签名、凭证隔离）成为顶级热点，标志着该生态正从早期的探索期迈入成熟期。

#### **2. 各项目活跃度对比**

| 项目 | Issues 更新 (新开/活跃) | PRs 更新 (开放/合并) | 新版本 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~700 | 466 待合并, 34 已合并 | 无 | **极高** - 核心框架，社区规模最大，迭代最密集，但积压严重。 |
| **NanoBot** | 11 (7活跃) | 39 (32待合并, 7已合并) | 无 | **高** - 快速迭代，社区贡献热情高，侧重 Provider 兼容与 UI。 |
| **Hermes Agent** | ~50 | ~50 (8 已合并) | 无 | **高** - 聚焦性能与安全深度优化，代码审查活跃。 |
| **PicoClaw** | 1 (新严重Bug) | 17 (6 已合并) | 无 | **高** - 密集开发冲刺，侧重平台兼容与安全加固。 |
| **NanoClaw** | 1 (关键Bug) | 10 (8 已合并) | 无 | **高** - 基础设施重构期，依赖升级与架构推进顺利，但安全配置有隐患。 |
| **NullClaw** | 1 (已关闭) | 1 (关键PR长期搁置) | 无 | **低** - 活跃度低，核心功能 PR 长期未合并。 |
| **IronClaw** | 21 | 42 (19 已合并) | 无 | **高** - Reborn 版本密集开发，功能与稳定性并行推进。 |
| **LobsterAI** | 1 (未解决) | 11 (5 已合并) | 无 | **中** - 基础设施修复积极，但旧版致命Bug未被解决。 |
| **Moltis** | 0 | 1 (已合并) | 无 | **低** - 平稳维护期，活跃度偏低。 |
| **CoPaw** | 88 | 28 已合并 | v1.1.12.post2 | **高** - 批量清理技术债务，但新Bug报告频繁，体验稳定性待提升。 |
| **TinyClaw** | 0 | 0 | 无 | **无活动** |
| **ZeptoClaw** | 0 | 0 | 无 | **无活动** |
| **ZeroClaw** | 89 | 多待合并 | 无 | **极高** - 安全与架构讨论是核心，新功能推进积极。 |

#### **3. OpenClaw 在生态中的定位**

*   **核心参照与生态基石**：OpenClaw 凭借其巨大的社区规模和近700条的日更新量，无可争议地是整个生态的 **“核心参照”** 和功能集成的基准。它的架构决策和功能实现（如会话状态、子代理模型）直接影响着其他派生或仿效项目。
*   **技术路线差异**：与 **Hermes Agent** 深度绑定 Anthropic 模型并侧重量化性能优化不同，OpenClaw 展现出更广泛的 **多模型兼容性**（同时处理 DeepSeek、Ollama 问题）。与 **NanoBot** 在易用性（WebUI 是热点）上竞争，但 OpenClaw 的社区规模和问题复杂度远高于 NanoBot，更像是一个 **企业级框架** 而非轻量级工具。
*   **社区规模对比**：OpenClaw 的社区规模是 **断层级别** 的。其 Issue/PR 数量（近700）远超其他项目（如 Hermes Agent 的 50 条）。这种巨大的规模既带来了最丰富的功能和最广泛的兼容性测试，也带来了最复杂的积压和维护挑战。**LobsterAI** 和 **CoPaw** 等国内项目则显示出在特定区域或场景（如国内大模型接入）的本地化优势。

#### **4. 共同关注的技术方向**

多个项目不约而同地聚焦于以下技术难题，反映了行业的普遍痛点：

*   **稳定性与状态管理**：
    *   **涉及项目**：OpenClaw (`#88838` SQLite迁移)、NanoBot (`#4473` 工具ID重复)、IronClaw (`#5148` 心跳自锁)、ZeroClaw (`#8054` 工具可用性不一致)
    *   **共同诉求**：解决会话状态持久化、并发竞争、死锁等问题，确保长时间运行任务的可靠性。
*   **性能与Token优化**：
    *   **涉及项目**：Hermes Agent (`#6839` 惰性加载, `#4379` 开销量化)、IronClaw (`#5149` 渐进式工具披露)
    *   **共同诉求**：通过减少不必要的 Token 消耗（如工具 Schema 注入）来降低 API 调用成本，尤其适用于本地模型和高频调用场景。
*   **安全与隐私治理**：
    *   **涉及项目**：Hermes Agent (`#43083` 密码擦除)、PicoClaw (`#3161` 模式守卫)、ZeroClaw (`#8177` 供应链签名)
    *   **共同诉求**：从凭证管理、命令执行安全到软件供应链完整性，寻求更系统化的安全防护方案。
*   **跨平台与渠道兼容**：
    *   **涉及项目**：PicoClaw (`#3162` WhatsApp重连)、OpenClaw (`#92201` Slack与Anthropic)、ZeroClaw (`#8128` DingTalk流式)
    *   **共同诉求**：确保不同通信渠道（Telegram, Slack, DingTalk）的长连接稳定性、消息格式正确性及实时性。

#### **5. 差异化定位分析**

| 项目 | 核心定位 | 功能侧重 | 目标用户 | 技术架构 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 全功能AI助手框架 | 极致的多模型/渠道兼容、高度可定制 | 高级开发、自托管爱好者 | 模块化、插件化、庞大的社区驱动 |
| **Hermes Agent** | 高性能、安全优先的 Agent | Token开销优化、安全边界、与Anthropic深度绑定 | 对成本和安全性敏感的专业开发者 | 深度优化、精细化控制、集成度高 |
| **NanoBot** | 轻量、易用的开发平台 | Provider生态、WebUI体验、MCP集成 | 快速原型开发者 | 轻量级、对PR响应快、社区贡献门槛低 |
| **IronClaw** | 面向NEAR AI生态的Reborn版本 | UI现代化（Slack配置迁移）、E2E测试 | NEAR AI平台用户、希望拥抱新架构的开发者 | 架构重构中，功能与稳定性并行 |
| **CoPaw** | 面向国内用户的全能助手 | 内置技能、Cron任务、记忆管理 | 国内用户、寻求“AI管家”的个人用户 | 功能丰富但维护压力大，技术债务积累快 |
| **ZeroClaw** | 企业级安全与多Agent编排 | 供应链安全、底层Wasm沙箱、多委派模式 | 企业开发者、对安全和合规要求高的用户 | 安全至上、架构前瞻、决策过程严谨 |

#### **6. 社区热度与成熟度**

*   **快速迭代阶段（社区高度活跃，Bug与功能齐飞）**：
    *   **OpenClaw, NanoBot, PicoClaw, IronClaw, ZeroClaw**。这些项目每日有大量的 PR 和 Issue 涌入，功能开发和在途修复并行，社区贡献者与核心团队互动紧密。`OpenClaw` 和 `ZeroClaw` 尤其处于“高流量”模式。
*   **质量巩固阶段（重点解决稳定性、清理技术债务）**：
    *   **Hermes Agent, CoPaw**。这些项目不再追求海量新功能，而是将重点放在性能优化（Hermes的Token分析）、安全加固和修复长期存在的 Bug（CoPaw批量合并历史PR）。社区讨论更集中在如何“用好”而非“如何新增”。
*   **平稳/维护阶段（活跃度较低）**：
    *   **NullClaw, Moltis, LobsterAI**。这些项目活动较少，主要进行补丁式修复或单个功能增强。虽然可能有稳定的用户基础，但社区增长和演化动力不足。

#### **7. 值得关注的趋势信号**

*   **“记账式”性能优化**：开发者不再仅凭感觉优化，而是通过 **精确量化 Token 消耗**（如 Hermes Agent `#4379`）来驱动决策。这预示着未来 AI 智能体开发的“效率导向”将进入精细化、数据驱动的时代。
*   **从“功能安全”到“供应链安全”**：以 ZeroClaw `#8177` 为代表，社区开始关注更上游的软件供应链攻击链。这是 AI 智能体被用于企业核心流程后，对合规和安全提出的必然要求。**开发者应开始思考如何为自己的 Agent 构建可信的交付管道**。
*   **“Agent 编排”成为下一个前沿**：Hermes Agent 的 ACP 泛化提议、ZeroClaw 的多委派模式以及 CoPaw 的多 Agent 协作问题，都指向一个趋势：**未来的智能体不是孤立的，而是需要像一个分布式系统一样被编排和管理**。理解并设计 Agent 之间的通信、授权与协作协议将成为重要能力。
*   **“平台兼容性”是双刃剑**：多模型、多渠道的兼容性是项目吸引用户的核心卖点，但也带来了巨大的 Bug 和技术债（如 OpenClaw 的大量 Provider 兼容性问题）。这个趋势提醒开发者，**拥抱生态的同时，必须建立强大的回归测试和自动化兼容性测试体系**，否则项目将被碎片化问题拖垮。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的NanoBot GitHub数据生成的2026-06-24项目动态日报。

---

## NanoBot 项目动态日报 | 2026-06-24

### 1. 今日速览

今日NanoBot项目活跃度极高，尤其在Pull Request方面。过去24小时内共计提交了39条PR，其中32条仍处于开放待合并状态，显示出社区贡献热情高涨，同时维护者审阅压力较大。Issues方面，11条更新中，新开或活跃的7条，主要集中在WebUI体验、新模型提供商支持和核心循环稳定性上。无新版本发布，但大量针对Bug修复和功能增强的PR正在排队，预示着下一次发布的规模可能不小。项目整体处于**快速迭代与社区共建**的健康状态。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

过去24小时内，共有7个PR被合并或关闭，标志着以下重要进展：

- **Git与工作区支持强化**：`[CLOSED] PR #4393` (yu-xin-c) 合入了针对 git命令在`restrictToWorkspace`模式下从子目录运行的端到端回归测试，确保此前修复（#4375, #4380）的稳定性。
- **内存上下文修复**：`[CLOSED] PR #4387` (yu-xin-c) 合入了对内存引导机制的修复，确保在项目级工作区配置中能正确回退到默认的`SOUL.md`和`USER.md`文件。
- **MCP测试稳定性及Provider修复**：
    - `[CLOSED] PR #4417` (yu-xin-c) 优化了流式HTTP超时回归测试，使用可解析的URL，避免因DNS问题导致测试不稳定。
    - `[CLOSED] PR #4443` (michaelxer) 针对流式响应中重复`tool_use` ID导致会话“永久性损坏”的问题提供了修复方案并已合并。
    - `[CLOSED] PR #4474` (zpljd258) 专门修复了与Kimi Coding端点对接时，并行`tool_use` ID重复的问题。
- **WebUI PWA支持初步尝试**：`[CLOSED] PR #4458` (zpljd258) 提交了添加PWA支持的PR，虽被标记为`invalid`，但显示了社区对该功能的强烈需求，后续演化为新的PR。

**总体评估**：项目在修复关键Bug（如重复tool_use ID导致会话中断）和完善工作区、内存等核心系统方面的进展是扎实而及时的。MCP和Provider的修复直接关系到用户的使用稳定性和模型扩展性。

### 4. 社区热点

今日讨论和关注度最集中的是以下两个议题，核心诉求均与**用户体验和模型可靠性**相关。

1.  **WebUI渲染问题（#4465, #4470）**
    -   `[OPEN] Issue #4470` (chengyongru): Telegram客户端存在换行符丢失和消息闪烁/持续编辑的显示Bug。该问题引发了`PR #4472` (axelray-dev) 的紧急修复尝试。
    -   `[OPEN] Issue #4465` (ZhouJ-sh): WebUI将AI模型的`<thinking/>`标签作为可见文本渲染，泄漏了模型的控制信息，破坏了用户体验。该问题已有对应的`PR #4466` (ZhouJ-sh) 进行修复。

    **分析**：这两个问题都直接影响了用户与助手交互的最终体验。前者是不同终端（Telegram）的适配问题，后者是AI原生内容（推理过程）在前端的解析展示问题。社区对UI/UX的一致性和可靠性有很高期待。

2.  **工具调用循环与ID重复（#2298, #4473）**
    -   `[OPEN] Issue #2298` (alekwo): 这是一个长期Issue（创建于3月），讨论了使用小/本地模型时，NanoBot容易陷入“无限工具调用循环”的问题。这表明模型能力不足时，缺乏有效的断路与重试逻辑。
    -   `[CLOSED] Issue #4473` (zpljd258): 报告了与Kimi Coding端点对接时，并行工具调用ID重复导致API报错的问题。该问题已被`PR #4474`迅速修复并合并。

    **分析**：`#2298` 代表了AI Agent领域的一个普遍性痛点：如何优雅地处理模型幻觉或失败。`#4473` 则是一个典型的Provider兼容性问题，经社区报告后快速定位并解决，体现了项目对多模型生态的重视和响应效率。

- **热门链接**：
    -   [Issue #4470: Telegram显示Bug](https://github.com/HKUDS/nanobot/issues/4470)
    -   [Issue #4465: WebUI thinking标签渲染Bug](https://github.com/HKUDS/nanobot/issues/4465)
    -   [Issue #2298: 无限工具调用循环](https://github.com/HKUDS/nanobot/issues/2298)
    -   [Issue #4473: 工具ID重复](https://github.com/HKUDS/nanobot/issues/4473)

### 5. Bug 与稳定性

今日报告的Bug主要集中在WebUI、Provider兼容性和核心Agent循环上，按严重程度排列如下：

-   **[严重] 聊天会话损坏**：`PR #4443`修复的流式响应中`tool_use` ID重复问题，可导致后续所有API调用失败，永久损坏会话。已有修复PR并合并。
-   **[高] 工具调用无限循环**：`Issue #2298` 提出，使用小模型时极易触发，严重影响Agent任务的完成率。**尚无对应的修复PR**。
-   **[高] Telegram消息显示异常**：`Issue #4470`报告了换行不识别和消息闪烁两个严重回归Bug。已有`PR #4472` (axelray-dev) 提出修复方案。
-   **[中] WebUI<thinking>标签泄露**：`Issue #4465`报告，使AI的内部思考过程暴露给用户。已有`PR #4466` (ZhouJ-sh) 提出修复方案。
-   **[中] iOS Safari界面缩放**：`PR #4471` (chengyongru)正在修复一个iOS Safari浏览器下，输入框自动缩放导致界面扭曲的Bug。
-   **[中] Dream功能光标停滞**：`PR #4481` (axelray-dev) 修复了一个Bug，即当Dream功能被禁用时，其内部光标不会前进，导致后续重新启用时上下文膨胀。
-   **[低] 配置保存丢失**：`PR #4478` (yorkhellen) 修复了保存配置时，`DreamConfig.cron`字段意外被移除的问题。

### 6. 功能请求与路线图信号

今日用户提出的新功能请求主要集中在以下方面，部分已有对应的PR，很可能进入下一版本：

-   **新模型/Provider接入**：`Issue #4475` (zpljd258) 提出增加OpenCode Zen和OpenCode Go两个新的、针对编程优化的低成本模型提供商。对应的`PR #4476`已开放。`Issue #4463` (zpljd258) 请求支持Kimi的付费“编程计划”端点，背后的`PR #4464`也已提。
    -   **路线图信号**：项目正在积极拓展“编程助手”定位，通过与更多针对代码场景优化且成本效益高的模型合作，增强其核心竞争力。
-   **WebUI移动端与PWA支持**：`Issue #4479` / `PR #4480` (zpljd258) 提出了完整的PWA（渐进式Web应用）支持和移动端侧边栏滑动手势。这是继`PR #4458`被关闭后的再次尝试，表明社区对此需求非常强烈。
-   **Deep Dream功能改进**：`Issue #4467` (songsong-hui) 提出Dream功能不应每次运行都创建新的skill文件，而应更新现有的，以避免重复。这是一个实用的工作流优化请求。`PR #4477` (chengyongru) 实现了生命周期感知的Wiki记忆写入器，也是对Dream功能的增强。
-   **Dream上下文控制**：`PR #4481` (axelray-dev) 除了修复Bug外，也部分解决了Dream禁用导致上下文膨胀的问题，这是一个稳定性的增强需求。

### 7. 用户反馈摘要

-   **痛点**：
    -   使用本地**小模型时易陷入死循环**（`#2298`），导致任务无法完成，体验很差。
    -   **升级后引入回归Bug**，如`#4410` (CLOSED) 中用户抱怨升级后即使设定不说话，Agent也会无故发送消息；`#4470`的Telegram显示Bug也影响了使用体验。
    -   **Dream功能不够智能**，用户`songsong-hui`（`#4467`）表达了对其总是创建重复文件而非更新既有技能的不满，这会污染工作区，维护成本高。
-   **满意与期望**：
    -   从`#4473`的快速关闭和`#4410`的解决来看，社区对Bug的**响应速度是满意的**。
    -   用户对**接入更多、更廉价的模型源**（如OpenCode系列）表现出积极态度，这表明社区用户群体对成本和模型多样性非常敏感。
    -   对**WebUI的移动端体验改进**（PWA、侧滑手势）有持续且强烈的呼声。

### 8. 待处理积压

以下是一些值得关注但长期未被解决或合并的重要Issue/PR：

-   **[长期未回应] Issue #2298**: “Breaking endless tool calling loops”。这个核心痛点自3月提出，已有5条评论，但至今没有看到来自项目维护者的实质性回应或分配到里程碑。这可能是影响部分用户（尤其自托管用户）留存率的关键问题。
-   **[长期开放PR] PR #3732** (NearlCrews): “fix(providers): require api_base before local provider wins on keyword match”。该PR试图解决local provider通过关键词匹配“劫持”云模型的问题。它已经开放了近一个半月，且非常重要，但尚未合并。这可能涉及到架构设计的复杂决策，但长期搁置会增加用户配置Provider时的困惑和错误风险。

**建议**：维护者可优先对`#2298`和`#3732`给予官方回应，例如分享设计思路、接受社区贡献的修复方案或解释延期原因，以避免社区贡献者的积极性受挫。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-06-24

## 1. 今日速览

今日项目活跃度极高，Issues 和 PR 更新数均达到 50 条，反映了社区强烈的参与度和维护者积极响应的状态。核心关注点集中在**性能优化（Token 开销、延迟 Schema 加载）**、**安全性加固（URL 授权、凭证隔离）** 以及**平台稳定性（Windows 控制台、Telegram 消息循环）** 三大领域。虽然没有新版本发布，但多个长期悬而未决的 Issue（如 Termux 上的 Rust 源码编译问题）和关键 Bug 在今天被关闭，表明项目正在稳步解决历史债务。代码审查和合并活动密集，项目健康度良好。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日有 8 个 PR 被合并或关闭，主要集中在以下几个关键领域，显著提升了项目的稳定性和安全性：

- **安全性增强**：PR #51621 被合并，为 `browser_navigate` 和 `web_extract` 工具添加了**显式 URL 意图守卫**，防止模型在用户未授权的情况下被动访问链接，解决了一个重要的安全边界问题。PR #51604 则通过作用域隔离解决了多路复用网关模式下 Anthropic 凭证读取错误的问题。
- **Windows 平台稳定性**：PR #41028 和 PR #49615 针对 Windows 网关后台运行时的“幽灵控制台窗口”问题提供了解决方案，通过修改 uv 虚拟环境的启动器，实现了真正的无窗口后台运行。
- **移动端兼容性**：合并了 PR #39152 和 PR #48626，彻底解决了 **Termux（Android Linux 环境）** 上 `hermes update` 因找不到预编译的 uv 二进制文件而触发长达数十分钟的 Rust 源码编译，并可能导致低内存设备 OOM 的问题。新逻辑会优先使用 PATH 中的 uv 或跳过此项依赖。

## 4. 社区热点

今日讨论热度最高的三个议题揭示了社区对项目**核心性能**和**安全隐私**的深切关注：

1.  **#6839 [Feature: Lazy Tool Schema Loading]** (评论: 26)
    这是社区讨论最激烈的话题。用户指出，每次 API 调用都注入所有（50+）工具的完整 Schema，导致每次调用浪费约 3,500-5,000 Tokens。提案建议采用“两阶段工具注入”，即在规划阶段仅发送工具的“签名”以节省 Token，在模型实际执行时再发送完整 Schema。这反映了用户对**降低本地模型使用成本**和**提升 API 调用效率**的强烈诉求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/6839)

2.  **#4379 [Token overhead analysis: 73% fixed overhead]** (评论: 15)
    与 #6839 一脉相承，用户通过自建仪表盘量化分析，发现每次 API 调用中**73% (~13.9K Tokens) 是固定开销**。这为 #6839 的优化方向提供了精确的数据支撑，进一步将社区的讨论焦点凝聚到了 Token 优化上。
    [链接](https://github.com/NousResearch/hermes-agent/issues/4379)

3.  **#43083 [Passwords get replaced by *** but model fails on second tool call]** (评论: 8)
    该 Bug 报告了严重的安全与功能矛盾：虽然系统用 `***` 替换了密码，但模型回溯自身对话历史时，再次看到 `***` 时无法执行需要密码的第二次工具调用。社区正在激烈讨论如何实现“**防御性地从对话历史中擦除凭证，同时不影响工具的再次执行**”。
    [链接](https://github.com/NousResearch/hermes-agent/issues/43083)

## 5. Bug 与稳定性

今日报告的 Bug 中，有数个达到了 P1（高）严重等级，并部分已有修复 PR：

- **P1 - 高**
    - **#43083 (密码回读失败)**: 高优先级的安全与功能冲突 Bug。**暂无已关联的 fix PR**，但讨论热烈。
    - **#48648 (Telegram 无限消息循环)**: 流式响应超过 4096 字符限制时，网关陷入无限嵌套回复循环。**已有相关修复方向的讨论**，暂无直接 fix PR。
    - **#47237 (Telegram 重复用户消息)**: 网关在临时提供商故障后，会持久化重复的用户消息，可能导致 agent 行为错乱。**暂无关联 fix PR**。
    - **#51579 (Docker 迁移导致 .env 被清空)**: 每次容器启动时，自动化配置迁移会将 `$HERMES_HOME/.env` 清空，导致 Telegram 网关失效。这是一个回归问题。**暂无关联 fix PR**。

- **P2 - 中**
    - **#38387 (Windows 空白控制台窗口)**: 已有 fix PR #41028 和 #49615 被合并。
    - **#51560 (后备提供商配置被静默清空)**: `hermes config set` 命令存储 JSON 字符串有误，导致后备链为空。**暂无关联 fix PR**。
    - **#50005 (桌面网关断连无离线模式)**: 网关 WebSocket 断开后，桌面应用无任何降级策略，直接卡死。**暂无关联 fix PR**。

- **P3 - 低**
    - **#51045 (Nous Portal 返回 500)**: OpenAI GPT-5.5 通过 Nous Portal 调用时持续返回 Azure 后端错误。
    - **#51578 (computer_use 无法发现 Qt6 应用)**: 在 Arch Linux 上，`computer_use` 无法发现像 FreeCAD 这样的 Qt6 应用。
    - **#42083 (支付错误检测不全面)**: 未将 502/503/504 等状态码识别为支付错误。

## 6. 功能请求与路线图信号

- **Token 优化**：`#6839` (惰性加载) 和 `#4379` (开销分析) 是本日的焦点。鉴于其高讨论度（26 条评论、14 个 👍），这**极有可能**成为下一版本的核心优化方向。
- **Agent Client Protocol (ACP) 泛化**：`#5257` (通用 ACP 客户端) 提议让 Hermes 能够编排其他 ACP 支持的编码 Agent（如 Claude Code），而非仅作为 IDE 集成的 Server。该提案获得了 16 个 👍，反映了社区对**多 Agent 编排**的兴趣。
- **混合语义搜索**：有两个 PR (`#44093` 和 `#51125`) 都为 `session_search` 功能添加了基于向量嵌入的语义搜索，以取代目前仅支持关键词搜索的 FTS5。虽然 `#51125` 被关闭（可能是重复提交），但 `#44093` 仍处于开放状态，表明项目组**正在认真考虑**此项增强。
- **新的 LLC 提供商 (Ollama Cloud)**：`#22648` 提议将 Ollama Cloud 作为新的插件化搜索提供商，此 PR 已经过重构并仍在持续迭代。

## 7. 用户反馈摘要

- **性能痛点**：多个用户（如 `jarviszomine` 和 `Bichev`）精确量化了 Token 浪费问题，并提供了仪表盘等数据工具，表现了资深用户对成本效率的极致追求。
- **安全困惑**：`nnnarvaez` 报告的密码问题 (`#43083`) 生动展示了安全措施（`***` 替换）如何意外地在实际使用中导致功能失效，这是一个设计上的两难问题。
- **平台适配苦恼**：Windows 用户（`dontcallmejames`）和 Termux 用户（`aliatx2017`）分别报告了后台运行和编译安装的痛点，反映出跨平台兼容性是阻碍部分用户流畅体验的关键。好消息是今日针对 Termux 的问题已被修复。
- **功能需求**：`flowforgelab` 和 `AIalliAI` 提出的通用 ACP 客户端和混合搜索功能，代表了社区希望 Hermes 从一个**单一的交互接口**进化为更强大、更智能的**Agent 编排中心**和**长期记忆体**的期望。

## 8. 待处理积压

以下是一些长期未解决或需要维护者关注的重要条目：

- **#19566 [OpenAI-Codex 凭证池在轮换中丢失凭证] (P1)**: 自 5月4日创建以来长期开放，涉及敏感的认证和会话状态管理风险。虽然今日有更新，但问题仍未解决。需要维护者深入调查。
    [链接](https://github.com/NousResearch/hermes-agent/issues/19566)
- **#35357 [Tirith 审批门无法覆盖非 Shell 工具] (P3)**: 虽然是 P3，但安全相关，讨论的是人工审批系统的重大漏洞（`send_message`, `write_file` 等工具绕过审批）。已在 5月30日被报告，至今未有关联修复 PR，值得关注。
    [链接](https://github.com/NousResearch/hermes-agent/issues/35357)
- **#8427 [添加 Vertex AI 提供商] (P3)**: 这是一个大型 PR，早在 4月12日提出，用于支持谷歌的 Vertex AI。虽然今天是活跃的（有更新），但其庞大的代码变更和可能存在的分歧使其合并前景不明，但若合入将显著扩大 Hermes 的企业级用例。
    [链接](https://github.com/NousResearch/hermes-agent/pull/8427)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的PicoClaw项目数据，我已生成2026年6月24日的项目动态日报。

---

# PicoClaw 项目动态日报 | 2026年6月24日

## 1. 今日速览

今日PicoClaw项目活跃度**极高**，主要体现在Pull Request (PR) 数量激增，共计17条，其中包含大量由核心贡献者如danmobot和正则维护者提交的修复与新功能。虽然无新版本发布，但PR的密集提交和合并表明项目正处于**密集开发冲刺阶段**，重点关注稳定性（安全、连接、文件系统）和平台兼容性（Windows、Android、AWS）。Bug报告方面，今日新增了一个关于Android/Termux环境下进程钩子崩溃的严重问题，但已有其他关键修复被合并。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭了6个重要PR，涵盖了从基础架构（错误处理、代码规范性）到核心功能（平台兼容性、AI API兼容性）的改进。

- **核心稳定性与代码质量**：
    - **PR #3059** [已关闭]：显式处理了在错误路径和重试循环中可能被忽略的`Close()`错误，增强了代码的健壮性，解决了资源泄露的潜在风险。
    - **PR #3054** [已关闭]：修复了`LINEChannel.Send`中未检查的`sync.Map`类型断言，防止了因类型不匹配导致的panic崩溃，提升了消息通道的稳定性。
    - **PR #3047** [已关闭]：恢复了会话详情页查看完整历史记录（JSONL）的功能，同时保证了会话列表的加载性能。

- **平台兼容性**：
    - **PR #3162** [已关闭]：修复了WhatsApp通道的WebSocket自动断开问题，引入了自动重连（含指数退避）和异步消息处理机制，显著提升了WhatsApp通道的可靠性。
    - **PR #3015** [已关闭]：关闭了一个关于Windows下QQ频道Token获取超时的stale bug报告，表明该问题可能已通过其他方式解决或被认定为环境问题。

- **AI API兼容性**：
    - **PR #3154** [已关闭]：针对字节跳动豆包（Doubao）模型进行修复，解决了其将工具调用以`<seed:tool_call>` XML格式嵌入`message.content`中的非标准行为，确保PicoClaw能正确解析并处理这些调用。

**总结**：项目在24小时内完成了多项关键修复，覆盖了代码质量、多平台通信和AI模型兼容性，整体向前迈进稳固的一步。

## 4. 社区热点

今日社区的讨论焦点并非某个Issue，而是由**danmobot**和**loafoe**等核心贡献者提交的一系列高价值PR。这些PR虽评论数少，但内容涉及安全、新功能和性能优化，反映了项目核心开发团队的活跃。

- **PR #3160** [待合并]：《fix(auth): reject cross-site launcher setup requests》
    - **链接**: [sipeed/picoclaw PR #3160](https://github.com/sipeed/picoclaw/pull/3160)
    - **分析**: 这是一个重要的安全修复，旨在防止跨站请求伪造（CSRF）攻击，保护首次启动的仪表盘密码设置。它通过检查浏览器发送的`Sec-Fetch-Site`等头信息来验证请求来源。这体现了项目对Web界面安全性的重视。

- **PR #3161** [待合并]：《fix(exec): keep deny patterns active for custom allow rules》
    - **链接**: [sipeed/picoclaw PR #3161](https://github.com/sipeed/picoclaw/pull/3161)
    - **分析**: 此PR修复了一个执行命令的安全逻辑漏洞。之前，自定义允许规则会完全绕过拒绝模式检查。现在，即使命令匹配了允许规则，拒绝模式仍会生效，以防止绕过安全策略执行危险操作（如通过`jq`读取环境变量）。这显著提升了`exec`工具的安全性。

**总结**：社区热点集中在通过PR引入的安全加固和功能增强上，表明项目正向更成熟、更安全的方向演进。

## 5. Bug 与稳定性

今日新增一个严重Bug，同时另一项关于连接稳定性的修复已合并。

- **严重 Bug**:
    - **Issue #3164** [开启]：《Process hooks crash gateway on Android/Termux (v0.2.9, config v3)》
        - **链接**: [sipeed/picoclaw Issue #3164](https://github.com/sipeed/picoclaw/pull/3164)
        - **严重程度**: 高
        - **描述**: 在Android/Termux环境下，启用进程钩子（JSON-RPC over stdio）会导致网关在启动2秒内崩溃，即使是“hello world”最小钩子程序也会触发。这表明进程钩子在Android平台存在严重的兼容性或竞态条件问题。
        - **状态**: 无修复PR关联，待维护者复现并定位。

- **已修复的连接问题**:
    - **PR #3162** [已关闭]：修复了WhatsApp WebSocket连接断开后无法重连的问题，通过异步处理和自动重连逻辑提升了稳定性。
    - **PR #2888** [已关闭]：关闭了一个关于工具配置加载图片反应的stale PR。

## 6. 功能请求与路线图信号

今日无新的功能请求Issues，但多个PR揭示了项目的未来功能方向。

- **新功能开发**:
    - **PR #3118** [待合并]：《Add remote Pico WebSocket mode to picoclaw agent》
        - **信号**: 该高频PR正在为`picoclaw agent`添加远程WebSocket模式，允许PicoClaw与远程Pico设备通过WebSocket通信。这表明项目正在从本地交互向远程、分布式架构扩展。
    - **PR #3163** [待合并]：《feat(bedrock): leverage Converse prompt caching via cache points》
        - **信号**: 为AWS Bedrock集成提供prompt缓存支持，可大幅降低大语言模型调用成本并减少延迟。这是一个重要的性能优化和成本控制功能。
    - **PR #3157** [待合并]：《feat: add Android ADB remote operations tool》
        - **信号**: 新增实验性Android ADB远程操作工具，提供截图、UI层级、点击、滑动等固定原语。这明确表明PicoClaw正在扩展其平台控制能力，向更广泛的操作系统自动化迈进。

**总结**：项目路线图信号明确，正朝着**远程交互**、**成本优化**和**跨平台设备控制**三个方向推进。

## 7. 用户反馈摘要

从今日的Issues评论中可以提炼出以下用户痛点：

- **Windows平台兼容问题**：Issue #3015（已关闭）反映用户在使用Windows构建版本时遭遇了QQ频道连接失败（Token超时），虽然问题已标记为已关闭，但这指出了PicoClaw在非Linux平台（特别是Windows）上仍存在与云端服务交互的潜在问题。
- **Android/Termux环境不稳定**：Issue #3164 报告了进程钩子功能在Android/Termux上的完全不可用（直接崩溃），这是一个严重的功能缺失，对于希望在移动设备上使用高级功能的用户来说阻碍较大。
- **核心功能巩固**：用户似乎更关注基础功能的稳定而非新功能。WhatsApp的重连修复（PR #3162）和exec工具的安全加固（PR #3161）都是为了解决现有用户的实际痛点。

## 8. 待处理积压

以下为长期未得回应的重要PR/Issue，可能成为进展瓶颈，提醒维护者关注：

- **PR #2975** [待合并]：《feat(telegram): treat reply to bot message as mention in group chats》
    - **链接**: [sipeed/picoclaw PR #2975](https://github.com/sipeed/picoclaw/pull/2975)
    - **状态**: 自2026年5月30日开启，已近一个月。
    - **说明**: 这是一个合理的功能请求，旨在改善Telegram群聊中机器人的交互体验。该PR等待维护者审查和合并，其长时间搁置可能影响Telegram渠道用户的使用满意度。

- **Issue #3164** [开启]：《Process hooks crash gateway on Android/Termux (v0.2.9, config v3)》
    - **链接**: [sipeed/picoclaw Issue #3164](https://github.com/sipeed/picoclaw/pull/3164)
    - **状态**: 刚创建一天，但严重性高。
    - **说明**: 建议维护者尽快尝试复现并定位原因，这可能是由于平台特定的文件路径、进程管理或信号处理方案不当引起的。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是为您生成的 NanoClaw 项目动态日报，基于 2026-06-24 的 GitHub 数据。

---

# NanoClaw 项目动态日报 | 2026-06-24

## 1. 今日速览

本项目今日活跃度较高，主要围绕 **基础设施重构** 和 **依赖升级** 两大主题展开。虽然无新版本发布，但合并了多达 **8 个 Pull Requests**，其中核心团队集中完成了对 **Chat SDK 4.29.0** 的全链路升级，并显著推进了 **扩展点架构** 的设计。同时，社区提交的 **Slack Socket Mode** 支持已成功合入主分支，这是提升本地开发体验的重要功能。然而，一个关于 **端口绑定** 的关键 Issue 揭示了安全配置上的潜在问题，值得关注。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

项目在过去 24 小时内完成了大量至关重要的基础设施合并，整体向前迈进了一大步。

- **核心依赖统一升级 (Chat SDK 4.29.0)**：开发者 `gabi-simons` 主导完成了一次全链路的依赖版本升级，从主分支（#2834）、到 `channels`（#2835）、再到 `providers`（#2836）分支的依赖均已对齐到 `@chat-adapter/*` 和 `chat` 4.29.0 版本。这是确保所有适配器（Adapters）与核心通信桥（Bridge）兼容性的关键步骤，为后续功能开发奠定了坚实基础。
- **Slack Socket Mode 支持正式上线**：广受期待的 Slack Socket Mode（#2837）已被成功合并到 `channels` 分支（#2839）。该功能允许 Slack 连接通过**出站 WebSocket** 工作，不再需要公开的 HTTPS 端点，极大地简化了本地开发、NAT 后面主机的部署流程。这是提升开发者体验的一个重要里程碑。
- **扩展点架构迈出关键一步**：开发者 `foxsky` 提交的 “Generic inert extension-point seams”（#2841 & #2842）已提交并持续跟进。该 PR 定义了一套通用的注册/应用（registerX/applyX）接口，在不改变现有行为的前提下，为下游 Fork 或未来的插件系统提供了标准的挂载点。这显示了项目架构的前瞻性和可扩展性规划。
- **性能改进与用户体验修复**：
    - 针对 `update-nanoclaw` 命令的流程进行了修复（#2826），确保技能（Skill）更新不再是可选项，并会在重新应用时重建容器，防止用户错过关键更新。
    - 一项针对容器性能的 PR（#2771）仍在积极讨论中，提议为 Agent 容器增加 `--shm-size=1g` 和 `--init` 参数，以解决 Chromium 浏览器因共享内存不足而崩溃的常见问题。

## 4. 社区热点

今日最受关注的讨论聚焦于 **Slack Socket Mode** 的集成流程。

- **#2840 [OPEN] Nanoclaw v2 binds port 3000 of external host ip for slack**
  - **作者**: sirpy
  - **链接**: [Issue #2840](https://github.com/nanocoai/nanoclaw/issues/2840)
  - **分析**: 这是一个非常关键的用户反馈。用户指出，尽管安装指南推荐创建隧道到 3000 端口以实现安全连接，但当前版本的 NanoClaw 却默认在**外部主机的 3000 端口**上进行绑定（bind）。这与隧道设计的初衷完全矛盾，导致安全风险。**核心诉求**是立即解决端口绑定问题，恢复隧道机制的安全价值。该问题目前尚无评论和回复，需项目方高度重视。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在**安全配置**层面，严重程度较高。

- **[严重] Issue #2840：Slack 连接端口绑定问题**
    - **问题**：NanoClaw v2 在外部 IP 上绑定 3000 端口，与手册推荐的隧道（Tunnel）安全方案冲突，直接暴露了服务端口。这属于安全配置错误。
    - **状态**：新开且无回应（0 评论）。
    - **已有 Fix PR**：暂无。

## 6. 功能请求与路线图信号

- **“Reject with reason…” 审批机制**：PR #2832 (`feat(approvals): reject with reason`) 提出了一种更人性化的模块审批流程。当审批者拒绝一个请求时，可以附带简短原因，使 AI Agent 能够理解拒绝背景并做出适应性调整。这标志着项目正在从简单的 “批准/拒绝” 二元决策向更复杂的**协作反馈循环**演进，有望成为用户界面交互的重要增强点。
- **Manifest Model Router Provider**：PR #2838 (`feat(providers): add Manifest model router provider`) 表明社区正在探索更灵活的大模型路由机制。虽然具体细节未明，但这是构建多模型、多提供商架构的典型信号，可能被纳入未来版本的能力集。

## 7. 用户反馈摘要

- **痛点确认**：Issue #2840 中，用户 `sirpy` 明确指出了 **NanoClaw v2 部署后的安全配置缺陷**。用户严格按照最佳安全实践（使用隧道）操作，却发现系统行为与安全期望相悖，这是一种严重的信任危机。反馈表明文档（指导使用隧道）与实际代码行为（绑定外网IP）之间存在脱节。
- **无正面反馈**：今日轮次中未发现来自用户的明确满意反馈或成功案例分享。

## 8. 待处理积压

- **PR #2771: `perf(container): --shm-size=1g + --init for agent containers`**
  - **作者**: `ankushchadha`
  - **状态**: 已开放 9 天，最后更新于昨日。
  - **链接**: [PR #2771](https://github.com/nanocoai/nanoclaw/pull/2771)
  - **摘要**: 这是一个解决使用内置浏览器时容器稳定性问题的常用最佳实践。尽管讨论可能仍在进行中，但该 PR 长时间未合并可能会影响大量依赖于 `agent-browser` 技能的用户体验。建议项目维护者尽快给出最终决定（合并/拒绝/要求修改）。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，现根据您提供的NullClaw GitHub数据，为您呈现2026年6月24日的项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-24

## 1. 今日速览

今日项目整体处于**平稳维护**阶段，社区活跃度较低。过去24小时内，项目成功关闭了1个关于“NoResponseContent”错误的Bug Issue，但对开发者社区的贡献者而言，有一个已存在近3个月的重大功能PR（#783）仍处于待合并状态，这是项目当前最主要的前进动力。无新版本发布，表明项目当前聚焦于质量修复和功能整合。

## 3. 项目进展

- **Bug修复推进**：成功关闭了Issue #967，该问题报告了在高频使用特定模型时出现的“NoResponseContent”错误，这有助于提升Agent功能的响应稳定性。
- **核心功能待整合**：PR #783 仍处于开启状态，该PR是一个重量级功能更新，引入了**Cron子代理引擎**、**JSON CLI输出**及**安全加固**。今日该PR获得了新的更新（2026-06-23），说明贡献者仍在积极维护。该PR的合并将标志着项目正式具备定时任务调度和执行能力，是向生产级AI Agent迈进的关键一步。

## 4. 社区热点

今日社区焦点较为单一，全部集中在已关闭的Bug Issue #967上。

- **Issue #967 [CLOSED]**: [bug] error: NoResponseContent
  - **链接**: [NullClaw Issue #967](nullclaw/nullclaw Issue #967)
  - **分析**: 该Issue在关闭前获得了2条评论，作者详细描述了在Windows 11系统下，使用`Agnes-2.0-Flash`模型时，超过50%的对话都会触发“error: NoResponseContent”。用户明确指出“同样的模型同样的apikey，我在picoclaw（推测为其他客户端）上没问题”，这强烈暗示了**NullClaw核心客户端在处理特定模型响应时存在兼容性或超时处理问题**。尽管该Issue已被关闭，但其描述的复现路径（高频、特定模型、高延迟）是值得维护者回溯测试的重要场景，以防未来类似模型更新后再次触发。

## 5. Bug 与稳定性

今日仅报告并关闭了1个Bug，严重程度较高，但已解决。

- **严重问题 - 已修复**:
  - **Issue #967**: `error: NoResponseContent`
    - **严重性**: **高** (影响超半数用户对话，且为高频复现)
    - **描述**: 在Windows环境下，使用`Agnes-2.0-Flash`模型时，客户端无法正常解析或获取AI响应内容。
    - **状态**: **已关闭** (CLOSED)
    - **Fix PR**: 未关联到具体PR，推测为直接提交或通过其他方式修复。

## 6. 功能请求与路线图信号

尽管今日无新功能请求提交，但PR #783 的持续存在是下一版本路线图最重要的信号。

- **#783 feat(cron): cron subagent...** : 该PR代表了社区开发者对**定时自动化**（Cron）和**可编程化操作**的强烈需求。它不仅仅是一个新功能，更是为NullClaw赋予了“主动执行”和“后台任务管理”的能力。核心功能点包括：
    1.  **定时调度引擎**：支持基于数据库的调度器，可执行技能、Agent和Shell任务，并支持时区偏移。
    2.  **可编程输出**：`--json`输出模式，为外部系统集成和自动化运维提供了标准接口。
    3.  **安全强化**：隐式包含了对Cron任务执行时的安全考量。
    - **预测**: 该PR一旦合并，几乎肯定会成为下一个正式版本（v2026.7.x）的核心亮点，将NullClaw从一个“即时问答工具”升级为“可计划、可维护的AI自动化后端”。

## 7. 用户反馈摘要

从今日关闭的Issue #967的评论中，可以提炼出以下用户反馈：

- **痛点**: 用户最直接的痛点是**可靠性问题**。模型调用的失败率高达50%以上，使得产品在实际使用中基本不可信任。用户特别强调“同样的模型和API Key在另一个客户端上工作正常”，这说明问题不在于模型或API，而在于NullClaw客户端本身。
- **用户画像**: 该用户技术背景较强（知道如何获取日志、对比不同客户端），对性能敏感（测量了27秒的响应速度），且有明确的生产或日常使用诉求。
- **满意度**: 鉴于该Bug被及时修复并关闭，用户对项目维护者的**响应速度和问题解决能力**应当是满意的。但该Bug本身暴露了客户端在**错误处理和模型兼容性**上的短板。

## 8. 待处理积压

当前项目最重要的积压项是功能性PR的长期未合并。

- **PR #783 (OPEN)**: feat(cron): cron subagent, run history, JSON output, security hardening
  - **作者**: yanggf8
  - **状态**: **已开启 79 天** (自2026-04-07)
  - **链接**: [NullClaw PR #783](nullclaw/nullclaw PR #783)
  - **提醒**: 这是当前社区贡献的最重要的新功能PR，涉及面广、改动量大。长期未合并可能冷却贡献者的热情。建议项目维护者：
    1.  在PR中给出明确的审查意见或期望的修改方向。
    2.  如果这项功能与项目主路线图冲突，应正式声明并关闭PR，避免悬而未决。
    3.  由于该PR今日仍有更新，说明贡献者仍在积极跟进，这是一个积极的信号，维护者应尽快安排合并或给出具体反馈。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 IronClaw 项目 2026-06-24 的数据生成的日报。

---

# IronClaw 项目动态日报 | 2026-06-24

## 今日速览

IronClaw 项目今日活跃度极高，尤其在代码合并和功能交付方面表现强劲。过去24小时内，共有 **42 条 PR 更新**，其中 **19 条已合并/关闭**，显示出团队在核心功能和修复上的推进速度。Issue 方面，虽有 **21 条更新**，但大量为自动化测试（Canary）任务，真正由社区或用户报告的 Bug 和功能请求仍占一定比例，表明项目处于密集迭代期。整体而言，项目状态健康，社区与核心团队的交互集中在 Reborn 版本的稳定性与用户体验打磨上。

## 版本发布

- **无**

## 项目进展

今日项目在多个关键领域取得了实质性进展，共合并了 19 个 PR，以下是重点合并内容，标志着 Reborn 版本在稳定性、安全性和功能完整性上迈出了重要一步。

- **Reborn 自动化管理**：`#5122` 和 `#5121` 分别新增了 Reborn 自动化的**删除**与**暂停/恢复**支持。对应 PR `#5133` 已合并，为 WebUI v2 提供了基础的管理能力。
    - 链接：[Issue #5122](https://github.com/nearai/ironclaw/issues/5122) | [Issue #5121](https://github.com/nearai/ironclaw/issues/5121) | [PR #5133](https://github.com/nearai/ironclaw/pull/5133)
- **首次运行设置体验**：`#4592` 关闭，该 Issue 旨在为全新安装的用户提供通过 WebUI v2 API 完成提供商、模型等基础设置的标准化流程，无需手动编辑配置文件。这显著降低了新用户的上手门槛。
    - 链接：[Issue #4592](https://github.com/nearai/ironclaw/issues/4592)
- **Slack 集成重构**：`#5152` 合并，完成了将 Slack 设置从 TOML 配置文件迁移到 WebUI 界面的工作。这极大地简化了 Slack 功能的配置流程，是 Reborn 架构现代化的重要一步。
    - 链接：[PR #5152](https://github.com/nearai/ironclaw/pull/5152)
- **Google 扩展稳定性**：`#4969` 合并，修复了谷歌扩展（如 Drive、Docs）在令牌失效时返回模糊错误的问题。现在，当遇到 `401` 错误时，会明确触发 `auth_required` 流程，而不是以 `operation_failed` 告终，提升了与其他组件的协作性。
    - 链接：[PR #4969](https://github.com/nearai/ironclaw/pull/4969)
- **日历功能 E2E 测试**：`#5155` 合并，为 Reborn 的日历功能添加了端到端测试线束，能够模拟完整的安装、认证与功能调用流程，这将有助于防止未来出现回归问题。
    - 链接：[PR #5155](https://github.com/nearai/ironclaw/pull/5155)

## 社区热点

今日最受关注的 PR 和 Issue 集中在**系统稳定性**和**用户界面体验**上，反映了项目正从功能堆叠转向质量打磨阶段。

1.  **[#5068] [OPEN] WebUI 工具权限与自动批准设置**： 这是一个 XL 尺寸的 PR，评论数最多。它力图补齐 Reborn WebUI 中关于工具权限（每次询问/始终允许/禁用）的配置面板。这直接回应了用户对 AI Agent 控制权的核心诉求，社区关注度高。
    - 链接：[PR #5068](https://github.com/nearai/ironclaw/pull/5068)

2.  **[#5169] [OPEN] 捆绑技能触发提示词安全列表**： 此问题报告了一个严重的用户体验问题：因捆绑技能中包含“Authorization”等常见 API 词汇，触发了模型安全词过滤，导致正常请求失败，并错误地提示为“临时系统问题”。该问题误导性强，影响用户信任度。
    - 链接：[Issue #5169](https://github.com/nearai/ironclaw/issues/5169)

3.  **[#5149] [OPEN] 上下文管理：渐进式工具披露**： 此 PR 针对一个性能痛点：每次模型调用都会发送所有 ~91 个工具 schema，导致 Token 消耗巨大、延迟高。此 PR 提出了一种标记控制的渐进式工具披露方案，被视为解决 NEAR AI 接口性能和超时问题的关键。
    - 链接：[PR #5149](https://github.com/nearai/ironclaw/pull/5149)

## Bug 与稳定性

今日 Bug 类 Issue 报告和修复活动频繁，稳定性仍是团队关注重点。

- **严重 - [#5169] [OPEN] 捆绑技能触发安全词列表导致请求失败**： 用户使用干净默认设置启动 Reborn 时，因内置技能包含API关键字（如"Bearer"），被错误地判定为不安全并拒绝服务，误导用户以为是系统问题。**暂无对应 Fix PR。**
    - 链接：[Issue #5169](https://github.com/nearai/ironclaw/issues/5169)

- **严重 - [#5148] [OPEN] 任务调度器心跳自锁**： 当执行器处于状态更新过渡期时，调度器的心跳机制可能因获取同一个异步锁而导致死锁，造成正在运行的任务永久卡住。**暂无对应 Fix PR。**
    - 链接：[Issue #5148](https://github.com/nearai/ironclaw/issues/5148)

- **中等 - [#5147] [OPEN] Flaky 测试阻塞合并队列**： 测试 `trigger_poller_does_not_submit_turn_for_unpaired_actor` 存在约 30% 的失败率，已导致 PR 被意外踢出合并队列。这是一个典型的 CI 稳定性问题，需优先处理。
    - 链接：[Issue #5147](https://github.com/nearai/ironclaw/issues/5147)

- **中等 - [#3733] [OPEN] 无效 Gmail Token 显示成功通知**： 用户输入错误的 Google OAuth Token 后，系统仍显示“配置成功”的 Toast 通知，造成误导。**暂无对应 Fix PR。**
    - 链接：[Issue #3733](https://github.com/nearai/ironclaw/issues/3733)

- **中等 - [#5157] [OPEN] Railway 部署中设置页面缺少推理配置**： 在 Railway 托管环境下，设置页面的推理(Inference)部分有时不显示。**暂无对应 Fix PR。**
    - 链接：[Issue #5157](https://github.com/nearai/ironclaw/issues/5157)

## 功能请求与路线图信号

今日未发现全新的用户功能请求，更多是对现有功能的增强和优化，部分已有对应 PR 在推进。

- **用户界面与控制**：
    - **扩展管理** (`#5146`)：用户请求在扩展页面增加“停用”按钮。这是一个明显的 UI 设计缺口。
    - **提供商信息显示** (`#5144`)：用户要求在提供商卡片中显示 NEAR AI 的默认 Base URL，而非显示 `None`，以增强信息透明性。
    - **工具权限设置** (`#5068`)： 社区对精细控制 AI 工具权限的需求强烈，对应的 PR 正在推进中。
- **开发者与系统体验**：
    - **停止跟踪 `dist` 目录** (`#5167`)： 核心贡献者提出不应该将构建产物 `dist` 提交到 Git 仓库，这会造成 PR 不必要的变更和混乱。这是一个明确的技术债务清理请求。

## 用户反馈摘要

从今日的 Issue 和评论中，可以提炼出几个典型的用户痛点：

1.  **误导性的错误信息**： 用户对 `#5169` 描述的“安全词误杀”和 `#3733` 描述的“无效令牌却显示成功”感到困惑。用户期望系统能给出清晰、准确的状态反馈，而非模糊或错误的提示。真实用户反馈：“The rejection is misrepresented as a 'temporary system issue'...”
2.  **不一致的 UI/UX**： 用户发现 Gmail 认证界面在不同会话中表现不一致（`#3732`），有时显示 OAuth 链接，有时要求手动输入令牌。这表明前端逻辑存在碎片化问题。
3.  **核心功能出人意料的缺陷**： 用户报告日历扩展 `list_events` 返回的是最旧的事件而非即将到来的事件（`#4640`），这完全违背了用户预期，属于明显的功能设计缺陷。
4.  **模型行为不可控**： 用户尝试让 Claude 创建自动化任务时，模型未能正确调用 `trigger_create` 工具，反而执行其他无关操作后报告“工具不可用”（`#5151`）。这表明 AI 模型在复杂任务场景下的行为仍有待优化和引导。

## 待处理积压

以下是一些长期未解决或在关键路径上的 Issue 与 PR，建议维护团队重点关注。

- **[#4108] Nightly E2E failed**： 每日 E2E 测试持续失败，这是一个关于持续集成健康度的红色警报。虽然可能是环境问题，但应优先排查解决。
    - 链接：[Issue #4108](https://github.com/nearai/ironclaw/issues/4108)
- **[#4640] [bug] Reborn gsuite google-calendar list_events 返回无序事件**： 该问题自6月9日报告以来未解决，影响日历功能的实用性，对用户感知价值影响大。
    - 链接：[Issue #4640](https://github.com/nearai/ironclaw/issues/4640)
- **[#3732] [bug] Gmail auth gate 显示不一致的 UI**： 此问题提出已超过一个月，作为核心集成功能，其不一致的UI体验影响使用流畅度。
    - 链接：[Issue #3732](https://github.com/nearai/ironclaw/issues/3732)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的 GitHub 数据生成的 2026-06-24 项目动态日报。

---

# LobsterAI 项目日报 — 2026年6月24日

## 今日速览

今日项目活动集中在代码合并与基础设施优化上，展现了良好的开发活跃度。总计有 11 条 Pull Request (PR) 更新，其中 5 条已成功合并或关闭，6 条仍处于待合并状态。开发团队重点清理了与 OpenClaw 网关及定时任务相关的技术债，并新增了对 LiteLLM 网关的支持，增强了项目的 AI 模型兼容性。然而，社区中一个关于 4.1 版本导致服务完全瘫痪的严重 Bug 仍未被响应，这构成了当前项目稳定性的主要风险点。

## 版本发布

*无。项目在过去24小时内没有发布新版本。*

## 项目进展

今日有5个重要的 PR 被合并或关闭，展示了项目在特定方向上的稳健推进：

- **核心功能增强: 持久化行动计划** (`#2192`)
  - **内容**: 新增了持久的“计划模式”确认流程。现在，在协作（Cowork）会话中，AI 生成的计划会保持活跃，直到用户明确确认执行或调整。此举增强了用户对复杂任务执行流程的控制感。
  - **影响**: 提升了 Cowork 功能的成熟度和用户体验。
  - **链接**: [PR #2192](https://github.com/netease-youdao/LobsterAI/pull/2192)

- **稳定性与维护: OpenClaw 网关多项修复** (`#2188`, `#2189`, `#2190`, `#2191`)
  - **内容**: 开发者 `btc69m979y-dotcom` 和 `liuzhq1986` 共同完成了一系列针对底层 OpenClaw 网关和定时任务系统的修复。涉及：
    1.  **修复 CRON 任务会话同步** (#2190): 解决了多次运行同一 CRON 任务时，会话会重复创建的问题。
    2.  **迁移遗留 CRON 存储** (#2189): 在启动时自动检测并迁移旧版本的 CRON 任务数据，防止数据丢失。
    3.  **明确调度任务启动状态** (#2191): 优化了任务和历史标签页的 UI，清晰展示了启动、加载、就绪和错误状态。
    4.  **记录日志与优化** (#2188): 合并了相关的日志优化。
  - **影响**: 这些修复显著提高了定时任务功能的稳定性和数据迁移的平滑性，对 OpenClaw 网关的用户至关重要。
  - **链接**: [PR #2190](https://github.com/netease-youdao/LobsterAI/pull/2190), [PR #2189](https://github.com/netease-youdao/LobsterAI/pull/2189), [PR #2191](https://github.com/netease-youdao/LobsterAI/pull/2191), [PR #2188](https://github.com/netease-youdao/LobsterAI/pull/2188)

- **新功能: 集成 LiteLLM 作为 AI 网关提供者** (`#2193`)
  - **内容**: 新增了 [LiteLLM](https://litellm.ai) 作为 AI 网关的接入选项。用户只需配置一个 LiteLLM 代理地址，即可通过统一的 OpenAI 兼容接口访问超过 100 个 LLM 提供商，无需新增依赖。
  - **影响**: 这极大地扩展了用户可以选择的 AI 模型范围，降低了因单一模型服务商限制而带来的使用风险。
  - **状态**: 待合并。
  - **链接**: [PR #2193](https://github.com/netease-youdao/LobsterAI/pull/2193)

## 社区热点

- **最受关注 Issue: 4.1 版本启动崩溃** (`#1400`)
  - **详情**: 用户 `danielmonlite` 报告了一个严重的启动崩溃问题。从 3.30 版本升级到 4.1 版本后，LobsterAI 会陷入无限重启循环，完全无法使用。同时，还附带报告了在升级前，自定义 LLM 配置无法与 web-search 功能协同工作的问题。
  - **分析**: 此 Issue`在过去24小时内被更新，虽然创建已有两个多月，但表明该 Bug 可能仍然存在于某些特定环境或配置中，是一个影响系统可用性的严重问题。用户急切地提供了自己的联系方式，表明问题已影响其正常使用。
  - **链接**: [Issue #1400](https://github.com/netease-youdao/LobsterAI/issues/1400)

## Bug 与稳定性

| 严重程度 | Bug 描述 | 关联 Issue | 关联 PR | 状态 |
| :--- | :--- | :--- | :--- | :--- |
| **致命** | 从 3.30 升级到 4.1 后，服务陷入无限重启循环，完全瘫痪。 | [#1400](https://github.com/netease-youdao/LobsterAI/issues/1400) | 无 | **未解决 (已标记 stale)** |
| **高** | 自定义配置 LLM (如 qwen3.5-plus) 因与 web-search 模块冲突而无法调用。 | [#1400](https://github.com/netease-youdao/LobsterAI/issues/1400) | 无 | **未解决 (已标记 stale)** |
| **低** | 旧版 CRON 任务持久化存储格式需要迁移，否则可能导致数据读取异常。 | 无 | [#2189](https://github.com/netease-youdao/LobsterAI/pull/2189) | **已修复 (已合并)** |
| **低** | CRON 任务多次运行时，会话缓存未正确复用，导致日志和会话混乱。 | 无 | [#2190](https://github.com/netease-youdao/LobsterAI/pull/2190) | **已修复 (已合并)** |

## 功能请求与路线图信号

- **更强的 AI 模型兼容性**: `PR #2193` 引入对 LiteLLM 的支持，是项目向“提供更灵活的 AI 后端接入方式”这一方向迈出的坚实一步。这响应了用户希望在单一应用内自由切换不同模型提供商的潜在需求，很可能被纳入下一个版本。
- **更优的用户控制流程**: `PR #2192` 的“持久化行动计划”功能，表明项目正在探索如何赋予用户对 AI 生成的任务计划有更精细的控制，而不仅仅是简单的接受或拒绝。

## 用户反馈摘要

- **核心痛点**: 用户 `danielmonlite` 的反馈揭示了升级路径不稳定和功能模块间存在冲突（LLM 配置与 web-search）的痛点。升级导致服务完全瘫痪是**最严重的负面使用体验**。
- **使用场景**: 用户提到“自定义配置的LLM - qwen3.5-plus”，显示用户会依赖外部或特定模型而非默认配置，期待高度的定制性和模型选择自由。

## 待处理积压

以下为创建于2026年4月3日、至今仍处于打开状态且无实质性响应的 Issue/PR，可能已被项目团队忽略，需要及时跟进：

- **[致命Bug] 4.1版本严重bug，网关反复启动失败** (`#1400`)
  - **关键性**: 极高，直接影响用户正常使用。
  - **建议**: **立即**安排开发人员复现和修复，并回滚社区反馈。
  - **链接**: [Issue #1400](https://github.com/netease-youdao/LobsterAI/issues/1400)

- **[安全修复] 修复请求安全性问题** (`#1401`)
  - **关键性**: 高，涉及用户数据传输安全。
  - **建议**: 审查并合并此 PR，以避免潜在的安全漏洞。
  - **链接**: [PR #1401](https://github.com/netease-youdao/LobsterAI/pull/1401)

- **[Bug修复] 多选附件只能添加最后一个文件** (`#1402`)
  - **关键性**: 中，影响文件上传功能的完整性。
  - **建议**: 安排合并。
  - **链接**: [PR #1402](https://github.com/netease-youdao/LobsterAI/pull/1402)

- **[UI/UX改进] 定时任务创建界面的时间控件优化** (`#1404`)
  - **关键性**: 低，属于体验优化。
  - **建议**: 作为备选改进，可在后续迭代中合并。
  - **链接**: [PR #1404](https://github.com/netease-youdao/LobsterAI/pull/1404)

- **[Bug修复] 定时任务通知渠道列表为空** (`#1406`)
  - **关键性**: 中，影响定时任务的通知功能。
  - **建议**: 安排合并。
  - **链接**: [PR #1406](https://github.com/netease-youdao/LobsterAI/pull/1406)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-06-24

## 1. 今日速览

Moltis 项目今日整体活跃度较低。过去24小时内无新Issues提交或关闭，也无新版本发布。唯一值得关注的活动是合并并关闭了 PR #215，该PR为项目新增了“send_image”工具，增强了技能向Telegram等频道发送图片的能力。项目整体处于稳定的功能迭代期，社区讨论趋于平静，无明显的Bug或稳定性报告。项目健康度良好，但开发节奏有所放缓。

## 2. 版本发布

（无）

## 3. 项目进展

**PR #215 合并/关闭：新增图片发送工具**

- **标题**：feat(tools): add send_image tool for channel image delivery
- **状态**：已关闭（已合并）
- **作者**：maximilize
- **链接**：[Moltis PR #215](https://github.com/moltis-org/moltis/pull/215)

**核心功能推进**：
- 新增 `send_image` 工具，允许技能（skills）将本地图片文件（支持PNG、JPEG、GIF、WebP格式）发送到Telegram等频道目标。
- 复用了项目现有的截图处理管线：返回一个 `data:` URI 格式的图片数据，存放在 `screenshot` 键中，由聊天运行器（chat runner）自动拾取并发送。
- 支持可选的 `caption` 参数，允许为图片添加文字说明。

**项目意义**：
该PR标志着Moltis在多媒体消息传递能力上的重要补充。此前项目主要支持文本和截图，此次新增直接发送本地图片的功能，使得基于Moltis构建的AI助手能够更灵活地与用户进行视觉交互，例如发送图表、照片或生成的内容。这提升了项目在Telegram等频道场景下的实用性和用户体验。

## 4. 社区热点

今日无活跃讨论或高互动量的Issues/PRs。项目社区目前保持平稳，可能由于近期无重大变更或Blocking问题，开发者与使用者均未产生大量讨论。

## 5. Bug 与稳定性

过去24小时内**未报告任何新的Bug**。项目在稳定性方面表现良好，无已知的重大回归或崩溃问题。

## 6. 功能请求与路线图信号

**无明显新功能请求**。结合PR #215的合并来看，项目当前在**多媒体传递**方向（特别是图片处理与频道适配）有所侧重。这可能是未来版本的一个潜在路线图信号：进一步增强与外部平台的集成能力（如支持更多图片格式、视频或文件发送），并优化截图/图片处理管线。

## 7. 用户反馈摘要

过去24小时内无新Issues，因此无直接的用户反馈可供分析。从PR #215的设计来看，此前的用户或开发者可能提出了“需要更灵活的图片发送方式，而不仅限于截图”的需求，本次PR正是对这一需求的响应。

## 8. 待处理积压

**过去24小时内无新增积压。** 项目长期未响应的Issues/PRs数量维持在较低水平，维护者响应及时。建议定期审查旧的开放Issues（如有），以保持社区参与度。

---

**总结**：Moltis 项目今日发展平稳，通过合并 PR #215 在多媒体交互能力上迈出了坚实一步。项目代码库健康，社区无重大异常。建议开发者关注下一步如何利用该工具扩展更多实际场景。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为一位AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的CoPaw项目数据，生成一份结构化的2026年6月24日项目动态日报。

---

## CoPaw 项目动态日报 | 2026-06-24

### 1. 今日速览

今日CoPaw项目社区异常活跃，共处理了88条Issue与PR。得益于一次性合并了大量的历史遗留PR（主要来自贡献者`aqilaziz`），项目核心稳定性和功能细节得到了显著提升。同时，社区反馈也集中在两个核心痛点上：**定时任务（Cron）执行异常**和**持续的UI/UX问题**。新发布的v1.1.12.post2版本主要包含路径优化和文件预览改进。整体来看，项目进入了一个“清理技术债务，聚焦用户体验”的关键阶段，社区对功能的深度使用正在暴露出大量边缘情况。

### 2. 版本发布

**v1.1.12.post2** 已在过去24小时内发布。

*   **更新内容**:
    *   修复：删除当前会话后，自动导航至新会话，避免空白界面。
    *   功能增强：控制台与聊天界面中的文件预览功能现在支持相对路径，提升了在复杂部署场景下的兼容性。
    *   （后续日志截断，推测为更多微小的bug修复）

*   **破坏性变更**: 无。
*   **迁移注意事项**: 此版本为post2补丁版本，无破坏性变更，用户可正常更新。

### 3. 项目进展

在过去24小时内，共有 **28个PR被合并/关闭**，项目取得重大进展。特别值得注意的是贡献者 `aqilaziz` 在5月份提交的一系列重要PR于今日被批量合并，标志着大量历史技术债务得到解决。

*   **核心机制修复**:
    *   **Cron定时任务修复集**: 合并了`#4303`, `#4304`等多个PR，从根本上解决了定时任务在“非共享会话”下执行ID错误、以及在“共享会话”模式下因并发导致的冲突问题，预计将大幅减少相关Bug。
    *   **Shell命令执行优化**: 合并`#4331`和`#4337`，修复了子进程环境变量注入问题，并优化了Node、Python等本地命令的查找路径，提升了Skill执行的可靠性。
*   **前端体验与API升级**:
    *   **分页功能上线**: 合并`#4338`和`#4336`，聊天列表和聊天历史API均支持分页，为大用户量的场景提供了性能保障。
    *   **UI交互优化**: `#4345`为代码块增加了折叠功能，`#4326`修复了用户消息未进行Markdown渲染的问题，`#4308`则优化了模型错误的展示方式，使错误信息更直观。
*   **平台兼容与文档**:
    *   **Matrix协议修复**: `#5059`修复了端到端加密房间内媒体文件无法下载的问题。
    *   **Windows兼容性**: `#5417` (待合入) 提出了针对Windows Python 3.12+ `ProactorEventLoop` 下Uvicorn崩溃的修复方案，对于Windows用户至关重要。

**项目整体向前迈出了一大步，从“功能可用”向“运行稳定、体验顺滑”迈进。**

### 4. 社区热点

过去24小时内，最受关注的Issue主要围绕**更新后状态丢失**和**定时任务失效**两大问题：

*   **#5262 [Bug]: 每次升级之后，被禁用的内置技能又会重新变回启用** (12条评论)
    *   **链接**: [Issue #5262](https://github.com/agentscope-ai/QwenPaw/issues/5262)
    *   **诉求分析**: 这是一个典型的**用户配置持久化**问题。用户明确指出这是一个“2.0”版本的回归Bug，说明开发者此前试图修复但未彻底解决。这反映出项目在升级迁移流程中，未能妥善处理用户自定义的禁用/启用状态，影响了用户对内置功能（如`docx`, `xlsx`）的管控权，导致期望行为与实际不符。

*   **#5064 [Bug]: 由agnet生产的定时任务, 无法正常触发** (12条评论)
    *   **链接**: [Issue #5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)
    *   **诉求分析**: 定时任务是Agent实现“自主性”的关键功能。此Bug表明Agent创建的定时任务在到达设定时间后**静默失败**，且任务本身无法被手动编辑。这不仅仅是功能异常，更是对用户信任的打击。尽管今日合并了大量Cron相关PR，但该Issue的长期存在说明问题非常顽固，社区对此表现出高度关注。

### 5. Bug 与稳定性

今日报告的Bug数量较多，以下按严重程度排列：

*   **严重 (核心功能瘫痪)**:
    *   **#5416 [Bug]: 思考输出与上下文截断** (4条评论) - **影响范围**：用户完全看不到Agent回复。**状态**：无修复PR。
    *   **#5379 [Bug]: 安装后启动报错Internal Server Error** (2条评论) - **影响范围**：应用完全不可用。**状态**：有对应**修复PR #5417**正在Review。

*   **中等 (功能异常/丢失)**:
    *   **#5402 [Bug]: Dream Task执行失败** (4条评论) - **影响范围**：关键“晚间回顾”任务无法执行。
    *   **#5456 [Bug]: 非默认Agent身份错误** (2条评论) - **影响范围**：多Agent协作场景下身份混淆，可能导致权限问题。
    *   **#5398 [Bug]: Cron调度器停止分发任务** (5条评论) - **影响范围**：所有定时任务失效，**状态**：无明确修复PR，但今日合并的Cron相关PR（#4303等）可能已解决此问题。
    *   **#5373 [Bug]: Shell命令无法解析特殊字符** - **影响范围**：Agent执行shell命令能力受限，无法使用管道、重定向等基础功能。

*   **低等 (UI/兼容性瑕疵)**:
    *   **#5421 [Bug]: 切换Agent/聊天窗口严重卡顿** (2条评论) - 影响用户体验流畅度。
    *   **#5401 [Bug]: 大量工具调用历史导致前端崩溃** (2条评论) - 影响深度使用Agent的用户。
    *   **#5403 [BUG]: 浏览器自动填充劫持搜索框** (2条评论) - 影响模型配置页面的正常使用。

### 6. 功能请求与路线图信号

用户提出的新功能请求呈现“**稳定核心、补齐短板**”的趋势，同时也有对前沿功能的探索。

*   **高优先级/可能纳入下一版本**:
    *   **#5441 / #5439 [Feature]: 启动时内存占用优化** - 用户反馈刚启动占用1.4G，要求优化。这通常是用户**普遍且强烈**的诉求，可能会推动开发者进行性能摸底和内存泄漏排查。
    *   **#5360 [Feature]: 在添加新功能前先稳定核心应用** - 该Issue获得关注，反映了用户对近期功能迭代速度过快导致Bug增多的忧虑。开发者可能会考虑将此建议纳入规划，设立一个“稳定版本”周期。
    *   **#5316 [Feature]: 记忆搜索增加时效性排序** - 结合已存在的`#3995`关于记忆管理的Feature Request，**“记忆系统的智能化”** 已成为社区持续关注的热点，很可能成为下一个阶段的核心优化方向。

*   **低优先级/长期规划**:
    *   **#5427 [Feature]: Kimi Coding模型支持** - 特定模型提供商的需求，可能需要插件或新增Provider逻辑。
    *   **#5453 [Feature]: LaTeX公式渲染支持** - 学术用户的垂直需求，可通过语法高亮插件扩展实现。

### 7. 用户反馈摘要

从今日的Issues评论中，可以提炼出如下用户反馈：

*   **痛点聚焦**:
    *   **“升级焦虑”**：每次升级后都必须重新进行个性化配置（如禁用内置技能 #5262），这种“一夜回到解放前”的体验严重影响了用户对项目的信任。
    *   **“黑盒操作”**：定时任务失效（#5064, #5398）且Agent无法解释原因，用户感到困惑和不可控。Agent的“可解释性”和“可调试性”是当前的一大短板。
    *   **“资源吞噬”**：刚启动就占用1.4G内存（#5441），对于普通用户硬件配置是巨大挑战，感觉“臃肿”。

*   **使用场景**:
    *   **自动化与生产力**：用户（如`tina0501853`, `Aoki-7`）正在使用CoPaw进行日常工作记忆回顾、定时任务编排等“AI管家”场景，对任务稳定执行有极高的要求。
    *   **开发辅助**：用户（如`howyoungchen`）在尝试将CoPaw用于多Agent的开发工具链中，对Agent身份识别、上下文管理等核心细节非常敏感。
    *   **多平台部署**：用户（如`wangfei010313`）在Windows和Linux上运行，对特定平台的兼容性问题（如Windows下的Uvicorn崩溃）非常关注。

*   **满意度诉求**:
    *   用户对CoPaw的**Agent能力**和**插件生态**是认可的，但随着深度使用，对基础的**稳定性、易用性和性能**提出了更高的要求。
    *   用户社区是**专业且积极的**，能够准确地反馈问题根因（如`#5262`指出是升级流程问题）并提供初步解决方案的思路。

### 8. 待处理积压

*   **关键未修复Bug**:
    *   **#5262 [Bug]: 升级后内置技能重置** - 已存活7天，社区反映强烈，急需提出根本性修复方案。
    *   **#5064 [Bug]: Agent生成的定时任务失效** - 已存活14天，是Cron任务领域的核心疑难问题，尽管今天合并了多个Cron PR，仍需密切关注其是否真正得到解决。
    *   **#5328 [Bug]: Agent在思考过程中卡死** - 已存活5天，影响使用DeepSeek等需要长思考模型的用户，是流式处理中的典型难题。

*   **高质量待合并PR**:
    *   **#5417 [PR] 修复Windows Uvicorn崩溃** - 修复了一个影响Windows用户的严重Runtime Error，解决了项目一大准入障碍，应优先Review并合并。
    *   **#5368 [PR] 提升SkillPool移动端响应式布局** - 解决移动端体验痛点，与用户Feedback高度契合，值得尽快合并。

*   **开发建议**:
    *   建议维护者关注 **#5360 [Feature]: Stabilize the core app before adding new features**，考虑在下个版本迭代周期中，专门设立一个“稳定性冲刺”阶段，集中精力修复上述积压的Bug，并优化内存等性能指标。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 ZeroClaw 开源项目分析师，以下是基于您提供的数据生成的 2026-06-24 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-24

## 今日速览

项目今日整体活跃度 **极高**，社区提交与维护者响应均处于活跃状态。过去24小时内，代码仓库产生了 **89 条** Issues 与 PRs 的更新，表明项目正处于一个密集的开发与迭代周期。安全与架构相关的议题（如供应链签名、插件沙箱、密钥管理）成为当前关注的核心。新功能方面，涉及 **DingTalk 流式消息**、**应用内升级** 以及 **多 Agent 编排模式** 的 RFC 和 PR 在积极推进，显示了项目对生产环境易用性与安全性的双重重视。

## 版本发布

**无**。项目在过去24小时内未发布任何新版本。

## 项目进展

今日无重要PR合并，但多个关键功能的实现已处于待合并状态，表明项目进展加速，距离下一里程碑更近一步。

- **应用内升级功能完整实现**: 为响应 `[RFC #8170]`，`#8173` PR 已将 Web 仪表盘侧边栏的版本标签升级为一个完整的应用内升级入口，支持检测、展示更新日志、下载、替换二进制文件及自动重启。该功能实现了零停机升级的核心流程，对生产环境运维是重大利好。
- **渠道体验优化（流式消息与响应感知）**: **`#8128` (DingTalk流式消息支持)** 与 **`#8145` (早期确认反应与文档化无操作打字提示)** 两个待合并PR，分别旨在解决长任务响应延迟的感知问题。`#8128` 通过流式输出降低等待焦虑，`#8145` 则确保多渠道下用户能尽快收到“消息已收到”的反馈。
- **插件系统安全加固**: **`#8172`** PR 正在推进，旨在让运行时插件加载器实际执行已配置的签名策略，而非当前版本中忽略签名检查的 `Disabled` 模式。这是对 `[Issue #5919]` 所暴露的安全风险的直接回应。

## 社区热点

今日讨论热度最高的议题聚焦于 **供应链安全** 和 **系统架构与安全策略** 的顶层设计。

1.  **`#8177` (RFC: 供应链签名 - 硬件PGP, 可重现构建 与 SLSA provenance) (讨论: 4条)**
    - **链接**: [Issue #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)
    - **诉求**: 社区成员 `ConYel` 提出基于 **硬件安全密钥**、**多方仲裁**、**离线签名** 的硬核供应链安全方案，目标对标 StageX 模型。这展示了社区对软件供应链攻击链的高度警惕，希望 ZeroClaw 成为安全实践的标杆。
2.  **`#6913` (RFC: 插件系统目标冲突问题) (讨论: 3条)**
    - **链接**: [Issue #6943](https://github.com/zeroclaw-labs/zeroclaw/issues/6943)
    - **诉求**: 该RFC提出了一个架构性的激烈讨论——是否应 **放弃 Extism**，转而直接使用 **Wasmtime 组件模型**。讨论揭示了 `FND-001` 文档中不同章节对插件技术选型存在矛盾承诺，社区希望维护者尽快明确官方立场，避免资源浪费。

## Bug 与稳定性

今日报告的Bug主要集中在渠道集成与TUI体验方面，其中一项影响较大。

- **S1 - 工作流阻塞**:
    - **`#8151` (延迟图片附件在缓存历史中丢失引用；机器人后续否认看到过图片)**: `channel`
        - **状态**: 未关闭 | **已有修复PR**: `#8153` (已待合并)
        - **链接**: [Issue #8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151)
        - **分析**: 该Bug严重损害了用户在异步对话场景下的体验。机器人先确认消息后，却在后续交互中“失忆”，这会导致严重的用户信任问题。好在已有修复PR `#8153` 处理此问题。
- **S2 - 行为退化**:
    - **`#8193` (ZeroCode TUI 会话未接收到已发现的 MCP 工具)**: `zerocode/tui`
        - **状态**: 已关闭
        - **链接**: [Issue #8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)
        - **分析**: Gateway API 能看见MCP工具但TUI不可用，暴露出 Gateway-TUI 间数据同步的缺陷。问题已关闭表明已修复或被拦截。
    - **`#8236` (voice_wake.rs 缺少 `subject` 字段，破坏 `--all-features` 构建)**: `channel`
        - **状态**: 未关闭
        - **链接**: [Issue #8236](https://github.com/zeroclaw-labs/zeroclaw/issues/8236)
        - **严重性**: 中等。目前影响手动启用所有特性编译的构建。

## 功能请求与路线图信号

新功能请求集中于 **Agent 精细化配置** 与 **系统运维可操作性** 两个方面，这些信号很可能被纳入v0.9.0或后续版本的规划。

1.  **`#8228` (DingTalk 渠道流式消息支持)**: `enhancement`
    - **链接**: [Issue #8228](https://github.com/zeroclaw-labs/zeroclaw/issues/8228)
    - **信号强度**: 高。已有 **已关闭的 `#7531`** 作为平台化方案的前序探索，且 `#8142` (改善响应时间任务) 在跟进，表明这已成为渠道团队的重点工作。
2.  **`#8226` (支持按 Agent 配置自定义环境变量)**: `enhancement`
    - **链接**: [Issue #8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)
    - **信号强度**: 高。结合 `#5919` (环境变量访问限制) 与 `#6923` (独立委派模式)，可预见 **Agent 安全边界与配置隔离** 是下一个版本的架构主题之一。
3.  **`#8238` (为专家Agent切换添加独立的委派模式)**: `enhancement`
    - **链接**: [Issue #8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238)
    - **信号强度**: 中高。明确要求专家Agent能运行在 **独立的策略和工具集** 下，是对 `#7514` 跨配置委派的深化。这将成为企业级多Agent编排的基础能力。

## 用户反馈摘要

从今日活跃的Issue评论中，可以提炼出以下几个典型用户声音：

- **运维人员的声音**: `#8177` 的发起者 `ConYel` 直接引用了业界最顶尖的供应链安全标准 StageX，并批评 ZeroClaw 当前CI流程缺乏硬性和可验证的签名步骤。这反映出 **高级用户和运维工程师对项目安全性抱有极高期望**，并将 ZeroClaw 定位为需要满足金融级安全合规的基础设施组件。
- **新用户的痛点**: `#8125` (自动在快速入门中设置 yolo 风险配置文件) 的请求背后，反映了 **新用户在配置安全策略时的挫败感**。用户希望开箱即用，而不是立刻被安全策略限制住。这提示维护者需思考如何平衡“默认安全”与“上手即用”。
- **平台开发者的观察**: `#8054` (系统提示中的工具可用性应与所有入口点的实际有效工具匹配) 的提出者 `perlowja` 指出，同一个问题在上述 `#8193` 中被证实存在于多个入口点（通道、WebSocket、多模态）。这说明 **架构层面的数据一致性问题正在引发跨平台的体验分裂** 。

## 待处理积压

以下是一个长期未关闭的重要 Issue，建议维护者评估其优先级。

1.  **`#6074` (审计：追踪在批量回滚中丢失的 153 次提交)**
    - **创建**: 2026-04-24 | **状态**: `OPEN` (已标为 `in-progress` 和 `accepted`)
    - **链接**: [Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)
    - **重要性**: **极高**。该问题指向一次错误操作导致的大量代码丢失，虽然当前已恢复，但审计工作尚未完成。这直接关系到项目代码的完整性与历史可追溯性，是影响项目健康的重大技术债务。持续的 `in-progress` 状态暗示该工作可能由于优先级被长期搁置。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*