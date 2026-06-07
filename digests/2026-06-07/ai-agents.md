# OpenClaw 生态日报 2026-06-07

> Issues: 301 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-07 02:10 UTC

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

好的，作为 OpenClaw 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 GitHub 数据，生成 2026-06-07 的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

项目今日整体活跃度极高，呈现出典型的版本迭代前期特征：Bug 报告与代码修复齐飞。过去 24 小时共处理 301 条 Issues（新开与关闭数量持平）和 500 条 PR（大量待合并）。最显著的趋势是围绕 v2026.6.x 系列的回归问题集中爆发，尤其集中在 **OpenAI/ChatGPT Responses 传输层**、**Codx 运行环境**、**深度求索 (DeepSeek) 缓存失效**和 **Cron 触发器**等方面。社区正投入大量精力修复这些高优问题，同时也在探索更完善的**会话管理**和**安全边界**特性。项目整体处于高强度迭代的“修复与加固”阶段。

## 2. 版本发布

**无新版本发布。**
数据中提到的两个版本（`v2026.6.5-beta.2` 和 `v2026.6.5-beta.1`）均为前一天（2026-06-05）发布，内容一致，主要亮点仅有一条：
- **QQBot**: 在交付消息前剥离模型的推理/思考框架标记，防止原始 `<thinking>` 内容泄漏到频道回复中。 (#89913, #90132) 感谢 @openperf。

**提示**: 当前稳定版 `v2026.6.1` 存在多个严重回归问题，建议用户在后续 hotfix 或 `v2026.6.2` 发布前谨慎升级。

## 3. 项目进展

今日合并/关闭了多个关键修复，但仍有大量工作积压。主要进展体现在：
- **代码质量与基础设施**: 修复了 CLI 配置向导中 `Gateway token` 明文回显问题 (#91059)，并添加了 macOS 实时中继模式的原型支持 (#91026)。
- **核心功能加固**: 修复了 Gemini API 中空 `groundingMetadata` 导致的崩溃问题 (#91058)，并开始着手解决长期存在的`toolsAllow` 策略在子代理中无法传递的问题 (#78441)。
- **长期积压推进**: 一些被搁置的旧 PR 如 Telegram 空文本消息发送 (#88810)、缺失本地代理认证的快速失败 (#68280) 等获得了新的关注并正在等待审查。

**总体感觉**: 项目修复进展能跟上 Bug 报告的速度，但“等待作者响应”或“等待维护者审查”的 PR 积压显示出审查能力目前是主要瓶颈。

## 4. 社区热点

今日讨论最激烈的问题集中在 **v2026.6.1 版本的严重回归**：

- **[Bug] OpenAI ChatGPT Responses 传输失败** (#90083): 这是当前最受关注的 Bug 之一。用户报告在升级后，`openai/gpt-5.4` 和 `gpt-5.5` 模型的推理完全失效，错误代码为 `invalid_provider_content_type`。14条评论，3个点赞，大量用户受此影响。**核心诉求**: 期望核心传输层尽快修复此问题。
  [🔗 Issue #90083](https://github.com/openclaw/openclaw/issues/90083)

- **[Bug] Codex 应用服务器回合完成停滞** (#88312): 另一个 P1 级别的回归，报告在 `2026.5.27` 版本中，Codex 环境下的多工具代理回合经常失败。此问题被认为是之前已修复 Bug (#84076) 的复发，表明修复未彻底。**核心诉求**: 希望彻底解决 Codx 环境的稳定性问题，避免同一 Bug 反复出现。
  [🔗 Issue #88312](https://github.com/openclaw/openclaw/issues/88312)

- **[Bug] 升级 2026.6.1 导致 DeepSeek Prompt Cache 失效** (#91018): 用户报告升级后与 DeepSeek 的 Prompt Cache 交互完全中断，每小时额外烧掉约 6 美元。这是一个严重的经济影响 Bug。**核心诉求**: 用户要求立即修复或提供降级方案，避免持续的经济损失。
  [🔗 Issue #91018](https://github.com/openclaw/openclaw/issues/91018)

- **[Bug] Cron 定时触发器污染全局运行时状态** (#90991): 用户报告一个看似普通的 Cron 任务会错误地影响全局运行时，导致整个系统间歇性过载。这指向了一个更深层的架构问题。**核心诉求**: 开发者希望确保 Cron 任务的执行环境得到充分隔离，不会影响主进程的稳定性。
  [🔗 Issue #90991](https://github.com/openclaw/openclaw/issues/90991)

## 5. Bug 与稳定性

今日 Bug 报告数量多且集中，稳定性问题严峻。以下按严重程度排列：

| 级别 | 关键 Bug | Issue | 状态 |
| :--- | :--- | :--- | :--- |
| **P1** | OpenAI/ChatGPT Responses 传输失败 | [#90083](https://github.com/openclaw/openclaw/issues/90083) | 开放，无关联PR |
| **P1** | Codex 回合完成停滞（回归） | [#88312](https://github.com/openclaw/openclaw/issues/88312) | 开放，无关联PR |
| **⚠️严重** | 升级后 DeepSeek Prompt Cache 失效（经济损失） | [#91018](https://github.com/openclaw/openclaw/issues/91018) | 开放，无关联PR |
| **P1** | Cron 触发污染全局状态 | [#90991](https://github.com/openclaw/openclaw/issues/90991) | 开放，无关联PR |
| **P1** | 子代理宣布操作进入 OpenAI API-Key 路由 | [#90925](https://github.com/openclaw/openclaw/issues/90925) | 开放，无关联PR |
| **P1** | Feishu 流式卡片显示异常并截断内容 | [#88929](https://github.com/openclaw/openclaw/issues/88929) | 开放，无关联PR |
| **P1** | Gateway 因缺少凭据而挂起 | [#90886](https://github.com/openclaw/openclaw/issues/90886) | 开放，无关联PR |
| **P2** | WebChat 上传图片后 `read` 工具无法读取 | [#90964](https://github.com/openclaw/openclaw/issues/90964) | 已关闭，已修复 |
| **P2** | `exec` 工具在 WSL2 上触发 Gateway 重启 | [#90428](https://github.com/openclaw/openclaw/issues/90428) | 开放 |
| **P2** | 生命`cycle:end`事件缺少关键字段 | [#66534](https://github.com/openclaw/openclaw/issues/66534) | 已关闭，已修复 |

**今日已修复的 Bug**:
- `read` 工具无法读取 WebChat 上传的图片 (#90964)
- Gemini API 空 `groundingMetadata` 崩溃 (#91058)
- 多个旧版、已标记为 `stale` 的 Issue 被关闭。

## 6. 功能请求与路线图信号

- **主题会话家族 (Topic-Session Families)** (#90916): 这是一个关注度很高的请求，用户希望为同一 AI 助手创建多个独立的“话题语境”，以便在不同主题下进行隔离对话。这超出了现有会话管理的能力，是一个重要的路线图信号，表明社区对更精细的上下文管理有需求。

- **本地模型作为一等公民** (#89265): 随着本地模型质量提升，用户要求提升对本地推理提供者的支持力度，使其获得与云端 API 同样的头等支持。

- **带限制的预压缩内存刷写** (#90354): 用户希望为大型会话压缩前的内存写入操作增加硬性护栏（如大小限制、验证等），防止模型写入过大或错误的数据。这反映了用户对内存系统健壮性的担忧。

- **会议电路断路器** (#62615): 建议为“不健康”的会话（如连续失败）增加熔断机制，防止资源浪费。这表明用户对大模型会话的容错性和资源管理期望更高。

## 7. 用户反馈摘要

- **不满/痛点**:
  - **v2026.6.1 稳定性极差**: 至少 3 个 P1 级别的回归问题直接影响了核心推理功能和财务成本。“升级即崩溃”的风险显著，社区情绪紧张。
  - **Codx 环境可靠性低**: 多工具调用场景下频繁失败，且修复后容易复发，用户体验受损。
  - **普通用户配置门槛高**: 多个 Issue (如 #61009, #90509) 表明，理解 `exec` 工具路由、`auth-profiles` 等底层概念对普通用户来说过于复杂，配置文档与运行时行为不一致。
  - **记忆/内存系统不透明**: 用户对 `MEMORY.md` 的存在检查、`claw-mem0` 的可用性检测感到困惑 (#90203, #57256)，认为相关状态是“假阳性”或“无法正常使用”。

- **肯定/期望**:
  - 社区对快速修复 Bug 的能力有信心（例如多个 P1 Bug 报告后很快有相关联的 PR）。
  - 对独立的“话题语境” (#90916) 等功能请求表现出强烈兴趣，期望项目能更快提供更强大的会话管理能力。
  - 用户对 @openperf 等社区贡献者的工作表达了感谢，表明社区互助氛围良好。

## 8. 待处理积压

- **高优先级开放 Issue**:
  - **#90991** [P1] Cron 触发污染全局状态：长期存在且影响范围广，需要立即分配资源调查和修复。
  - **#90925** [P1] 子代理 AI 宣布操作路由错误：影响使用 OAuth 登录 OpenAI 的用户，是重要的身份认证和路由问题。
  - **#88929** [P1] Feishu 流式显示错误：影响大量中文用户，是重要的渠道可用性问题。
  - **#64267, #61009** [P1/P2] AI 内部思考泄漏：安全相关问题，尽管已历时较久，但需要持续关注。

- **长期悬而未决的功能请求**:
  - **#11955** [P2] 内存/上下文改进：这是一个宏大的功能请求集合，已开放超过 4 个月，评论活跃度下降，容易成为“僵尸 Issue”。维护者应该考虑将其拆分为更具体的、可执行的小 Issue。
  - **#45508** [P2] 自托管 TTS/STT：该请求符合本地化趋势，但进展缓慢，可能不是当前阶段的优先事项。

**总结**: 项目当前正处在一个关键的稳定化阶段。尽管社区活跃，贡献积极，但 v2026.6.1 带来的大量回归问题严重影响了用户体验和信任度。当务之急是集中精力修复所有 P1 级别的 Bug，特别是 OpenAI 传输层、Codx 环境和 DeepSeek 缓存问题。在版本稳定性达到健康水平之前，应警惕引入任何新的、复杂的功能。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我将基于您提供的各项目动态日报，为您呈现一份横向对比分析报告。

---

### **AI 智能体与个人 AI 助手开源生态全景 (2026-06-07)**

当前，个人 AI 助手开源生态正处于一个“**密集迭代与支柱性重构**”的关键阶段。一方面，以 **OpenClaw** 和 **CoPaw** 为代表的成熟项目正经历着因快速演进带来的“成长阵痛”——大量回归性 Bug 集中爆发，暴露出核心模块（如传输层、上下文管理）在架构升级中的稳定性短板。另一方面，以 **ZeroClaw**、**IronClaw** 和 **NanoClaw** 为代表的新锐力量正全力投入新特性（如 WASM 插件、确定性工作流引擎、多渠道适配）的构建，展现出强大的创新活力。整体来看，生态正从“能用”向“好用、易用、稳定”过渡，**安全、性能、开发体验与平台深度集成**成为了社区关注的焦点。

### **各项目活跃度对比**

下表汇总了各项目在 2026-06-07 的核心活动指标，以反映其活跃程度与健康状况。

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 | 核心主题 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 301 | 500 | 无 | ⚠️ **关注** | 回归 Bug 大爆发，核心模块稳定待定 |
| **NanoBot** | 7 | 24 | 无 | ✅ **良好** | 渠道稳定、上下文管理、安全加固 |
| **Hermes Agent** | 50 | 50 | 无 | ⚠️ **关注** | macOS 兼容性、多平台适配 Bug 集中 |
| **PicoClaw** | ~10 (新增) | 15 | 有 (Nightly) | ✅ **强劲** | 代码健壮性修复(防Panic、泄漏) |
| **NanoClaw** | ~4 (新增) | 14 (3 合并) | 无 | ✅ **良好** | Slack/Signal 适配、MCP 协议扩展 |
| **NullClaw** | 0 | 0 | 无 | 🟢 **静默** | 无活动 |
| **IronClaw** | ~8 | 31 (10 合并) | 无 | ✅ **强劲** | “Reborn”核心重构、Codex 模块开发 |
| **LobsterAI** | 1 | 2 (合并) | 无 | ✅ **良好** | 批量导出、任务管理优化 |
| **TinyClaw** | 0 | 0 | 无 | 🟢 **静默** | 无活动 |
| **Moltis** | 3 | 0 | 无 | 🔵 **低活跃** | 社区反馈期，核心推进慢 |
| **CoPaw** | 11 | 0 | 无 | ⚠️ **关注** | v1.1.10 版本回归 Bug 频发 |
| **ZeptoClaw** | 2 | 1 | 无 | ✅ **良好** | CI 流水线与二进制体积优化 |
| **ZeroClaw** | 39 | 50 | 无 | ✅ **极其活跃** | WASM 插件系统、安全模型加固、新集成 |

*注：`OpenClaw` 和 `Hemres Agent` 拥有超大规模社区，其 Issue/PR 基数较大，绝对数量高是正常现象。*

### **OpenClaw 在生态中的定位**

- **优势**: 作为“核心参照”项目，OpenClaw 拥有生态中最庞大的社区（Issue/PR 数量遥遥领先）、最丰富的渠道集成和功能模块，是领域的“旗舰”。
- **技术路线差异**: 相比追求极致轻量（如 ZeptoClaw）、特定场景深化（如 IronClaw 的 Codex 模块、LobsterAI 的定时任务）或新范式探索（如 Hermes Agent 的确定性工作流），OpenClaw 走的是“大一统”路线，力图成为一个全能型的 Agent 框架。
- **社区规模对比**: OpenClaw 的社区规模是其他项目的 10-100 倍。这种规模带来的是快速的问题响应和大量的第三方贡献，但同时也带来了更复杂的沟通成本和更高的回归风险。**当前其 v2026.6.1 版本的严重回归问题，正是其快速迭代、复杂性膨胀所付出的代价。**

### **共同关注的技术方向**

多个项目今日同时涌现出相似的技术需求，预示了未来生态发展的几个关键方向：

1.  **更强的上下文与状态管理**：
    - **涉及项目**: **OpenClaw** (#90916 主题会话家族), **NanoBot** (#4222 缓存失效), **LobsterAI** (#4937 压缩配置忽略模型参数), **Hermes Agent** (#5354 确定性工作流引擎)
    - **诉求**: 用户不满于简单的对话截断，要求更精细的上下文隔离、有效的提示缓存机制、可控制的压缩策略，以及对确定性、可预测执行模式的需求。

2.  **桌面与跨平台体验优化**：
    - **涉及项目**: **Hermes Agent** (#37505 Intel Mac 兼容性, #40831 macOS launchd)、**NanoBot** (#4218 WebUI Cron 管理)、**CoPaw** (#4971 会话侧边栏)、**LobsterAI** (#2120 UI 布局优化)
    - **诉求**: 用户对“开箱即用”的桌面体验和一致的跨平台行为要求越来越高，包括架构兼容、统一的管理界面、以及对高DPI等显示问题的修复。

3.  **安全与精细权限控制**：
    - **涉及项目**: **ZeroClaw** (#6914 工具白名单、#5775 技能权限)、**NanoBot** (#2533 MCP 访问控制、#4123 SSRF 防护)、**PicoClaw** (#2965 URL 安全修复)
    - **诉求**: 随着 Agent 能力变强，用户对安全隔离（沙箱）、敏感操作（工具、脚本、文件系统）的访问控制、以及外部资源请求的审查提出了更高要求。

4.  **生态集成与适配器增强**：
    - **涉及项目**: **CoPaw** (#4886 MAX Messenger), **NanoBot** (#4220 GitHub Copilot Enterprise)、**Hermes Agent** (#40910 AGIone provider)、**IronClaw** (#4509 Slack 路由)
    - **诉求**: 除了持续拓展新的消息平台（渠道），生态正转向对 **深度集成**（如飞书/钉钉的高级功能、Copilot 的企业版）和 **新LLM Provider**（如本地模型、非主流 API）的支持。

### **差异化定位分析**

| 维度 | 旗舰平台 (OpenClaw, ZeroClaw) | 专业场景 (IronClaw, Hermes Agent) | 极致轻量 (ZeptoClaw, PicoClaw) | 特定渠道与易用 (NanoBot, NanoClaw) |
| :--- | :--- | :--- | :--- | :--- |
| **目标用户** | 开发者、高级用户、企业部署 | 需要复杂工作流(Git操作、Code Review)或确定性任务的团队 | 资源受限设备(树莓派、机器人)、嵌入式 | 优先满足即时通讯(WhatsApp, Slack, Telegram)集成的个人与社区 |
| **技术架构** | 大而全，功能驱动，追求最大灵活性 | 场景驱动，强调“Codex”模块和工作流引擎（Reborn） | 极致精简，以“能在机器人上运行”为最高原则 | 轻量快速，重点优化特定渠道的稳定性和“开箱即用”体验 |
| **核心功能差异** | 完整的 Agent 开发生命周期 | 深度的审批流、任务编排、API 兼容层 | 最小化二进制体积，严格CI门槛 | 多用户内存隔离、MCP 访问控制、快速适配各种 IM |
| **当前阶段** | 稳定性修复 | 核心重构与功能开发 | 精细化运维与性能调优 | 渠道功能补齐与 Bug 修复 |

### **社区热度与成熟度**

- **高速迭代与功能先行阶段**:
    - **ZeroClaw、IronClaw、NanoBot**： 这些项目正在积极整合大量新功能（WASM, Codex, Copilot 支持），PR 合并速度很快，社区充满活力。但大量新功能也意味着潜在的不稳定性。
- **质量巩固与修复阶段**:
    - **OpenClaw、CoPaw、Hermes Agent**： 这些项目因前期的快速迭代，近期进入了一个 Bug 集中爆发期。社区主要讨论围绕“回归问题”和“如何降级”，开发者团队正全力修复。**这是成熟的标志，也是痛苦的过程。**
- **维护优化与社区静默**:
    - **ZeptoClaw、LobsterAI、PicoClaw**： 项目进入功能稳定、关注运维细节（CI、二进制体积）的阶段。社区仅特定用户在有新需求时才会活跃。
    - **NullClaw、TinyClaw、Moltis**： 无明显活动，可能是进入了维护模式或项目方向调整期。

### **值得关注的趋势信号**

1.  **“平台化” vs “场景化”的分化加剧**：以 OpenClaw、ZeroClaw 为代表的“平台派”试图囊括所有功能，而 IronClaw 的 Codex、Hermes Agent 的确定性工作流则代表了“场景派”的深度耕耘。对于开发者而言，选择平台意味着获得更通用的基础能力和更大的社区，但需要承受更高的复杂性；选择场景专用项目则能快速满足特定业务需求。
2.  **本体论与上下文管理成核心挑战**：几个大项目的 Bug 都指向了同一个痛点——**Agent 的上下文管理**。如何优雅地管理长期对话、隔离不同话题（主题会话家族）、维护跨会话的记忆，同时控制成本（提示缓存失效），是 AI 智能体从“玩具”走向“生产力工具”必须跨越的鸿沟。
3.  **安全从“附加”变为“必需”**：从简单的 API Key 管理，到精细的 MCP 工具访问控制、SSRF 防护、乃至 WASM 沙箱，生态正在建立一套 **“零信任”的 Agent 安全模型**。这意味着未来的 Agent 开发者在构建能力的同时，必须将安全性作为底层架构的一部分来考量，而非事后修补。
4.  **轻量级与边缘计算是重要的差异化方向**：ZeptoClaw 和 PicoClaw 对二进制体积的执着，表明 AI 智能体正在向资源受限的边缘设备（树莓派、机器人、IoT 网关）渗透。对于有离线或本地部署需求的用户，这类项目提供了关键的价值。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，这是为您生成的 NanoBot 项目动态日报。

---

## NanoBot 项目动态日报 | 2026-06-07

### 1. 今日速览

今日项目活跃度极高。过去24小时内，共处理了7个Issue和24个Pull Request，显示出社区参与度与开发节奏的显著加快。主要进展集中在三个方向：**渠道稳定性**（WhatsApp、微信）、**上下文管理**（提示缓存、截断逻辑）以及**安全加固**（SSRF防护、工作区逃逸）。此外，社区对新功能的需求强烈，尤其是**WebUI的Cron作业管理**和**GitHub Copilot企业版支持**。总体来看，项目正处于一个Bug修复与新功能密集落地的快速迭代期，健康度良好。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日有10个PR被合并或关闭，标志着多项重要功能的落地和关键Bug的修复：

- **渠道稳定与功能增强**:
    - `#2555` [WhatsApp] 修复重连后因旧连接导致消息重复处理的问题。([PR #2555](https://github.com/HKUDS/nanobot/pull/2555))
    - `#2528` [WhatsApp] 修复启动时重复处理历史消息的问题。([PR #2528](https://github.com/HKUDS/nanobot/pull/2528))
    - `#2529` [WhatsApp] 增加对语音消息的下载与转录支持。([PR #2529](https://github.com/HKUDS/nanobot/pull/2529))
- **安全与权限**:
    - `#2533` 新增 **per-MCP-server 的访问控制** (`allowFrom`)，允许限制敏感工具为特定用户。([PR #2533](https://github.com/HKUDS/nanobot/pull/2533))
- **核心功能与基础设施**:
    - `#2968` 实现**用户级内存隔离** (`per_user_memory`)，解决多用户环境下上下文混淆的问题。([PR #2968](https://github.com/HKUDS/nanobot/pull/2968))
    - `#2532` 新增 **Serper.dev** 作为谷歌搜索的提供商。([PR #2532](https://github.com/HKUDS/nanobot/pull/2532))
    - `#4209` 修复与部分兼容性API（如Agnes AI）进行图像生成时的`response_format`参数不兼容问题。([PR #4209](https://github.com/HKUDS/nanobot/pull/4209))
    - `#4195` 改进了桌面Shell和WebUI的共享界面，为未来的桌面版本做准备。([PR #4195](https://github.com/HKUDS/nanobot/pull/4195))
- **稳定性修复**:
    - `#4228` 修复自定义提供商在流式响应中丢弃空`reasoning_content`的问题。([PR #4228](https://github.com/HKUDS/nanobot/pull/4228))
    - `#4211` 关闭：修复SDK使用stdio MCP时在关闭阶段引发的`RuntimeError`。([Issue #4211](https://github.com/HKUDS/nanobot/pull/4211))

这些合并显示出项目不仅在开发新特性，也在同时巩固稳定性和安全性，整体向前迈出了坚实的一步。

### 4. 社区热点

今日最受社区关注的议题是 #4222 关于**上下文管理导致缓存失效**的问题，以及 #4220 关于**GitHub Copilot企业版支持**的功能请求。尽管#2573 (#2573 Copilot登录失败)积累了9个反应，但因其已被关闭，活跃度下降。

- **#4222 [Bug] 上下文缓存持续失效**：用户`imkuang`报告`max_messages`截断和`microcompact`机制导致每次对话都会改变发送给LLM的消息前缀，从而完全破坏了提示/前缀缓存的效用。这是对长对话场景下性能和成本的重大关切，目前已获得开发者直接回应。 ([Issue #4222](https://github.com/HKUDS/nanobot/issues/4222))

- **#4220 [增强] 添加GitHub Copilot企业/业务支持**：用户`gqcao`提出，当前只支持GitHub Copilot个人版，而使用GitHub Enterprise Server的企业用户需要不同的API端点。该请求反映了企业级部署的真实需求。 ([Issue #4220](https://github.com/HKUDS/nanobot/issues/4220))

- **#4218 [增强] 请求WebUI的Cron作业管理**：用户`Sdky`指出，虽然CLI的cron功能完善，但WebUI中缺乏管理界面，用户必须手动编辑`config.json`，增加了出错风险。社区希望WebUI能够像管理Provider、模型那样管理Cron任务。 ([Issue #4218](https://github.com/HKUDS/nanobot/issues/4218))

### 5. Bug 与稳定性

| 严重程度 | Issue ID | 描述 | 状态 | Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | `#4222` | `max_messages`截断逻辑导致提示缓存持续失效，严重影响长对话的效率和成本。 | OPEN | 暂无 |
| **中** | `#4211` | SDK使用stdio MCP时，在关闭阶段出现`RuntimeError`，虽然不影响主要功能，但造成异常警告。 | **已关闭** | - |
| **中** | `#4223` | 微信渠道在session过期后，进入永久静默的死循环，不再尝试重新扫码恢复。 | OPEN | **[PR #4223](https://github.com/HKUDS/nanobot/pull/4223)** |
| **低** | `#4105` | 自定义提供商在返回空的`reasoning_content`（如DeepSeek）时，该字段会被错误地丢弃。 | OPEN | **[PR #4227](https://github.com/HKUDS/nanobot/pull/4227)** & **[PR #4228](https://github.com/HKUDS/nanobot/pull/4228)** (已合) |

**新报告的Bug**：`#4222` (缓存失效) 是对稳定性和性能影响最大的新报告问题。

### 6. 功能请求与路线图信号

- **强烈信号**:
    - **WebUI Cron管理** (`#4218`): 社区呼声高，且已有对应的PR `#4225` (新增cron的 silent 模式和“锁接收者”功能)。该PR的合并将直接为WebUI的Cron管理功能铺平道路。
    - **GitHub Copilot企业版支持** (`#4220`): 吸引企业用户的关键功能。
- **中等信号**:
    - **WhatsApp增强** (`#4226`): 已经有一个待合并的PR，增加了转发消息检测、启动保护和应用联系人处理，显示出该渠道正在快速完善。
    - **AssemblyAI转录** (`#4224`): 增加新的转录提供商，为用户提供更多选择。

结合已闭/合并的PR，**Cron作业功能增强**和**渠道功能拓展**（尤其是WhatsApp和WeChat）很可能是下一版本的重点。

### 7. 用户反馈摘要

- **痛点**:
    - **微信渠道稳定性**：用户`DreamShepherd2006`提交的PR (#4223) 直接说明了微信频道可能永久静默的严重体验问题。此前用户可能只能通过重启应用来解决。
    - **缓存失效**：用户`imkuang`对`max_messages`截断逻辑的深入分析表明，高级用户对后台的上下文管理机制非常关注，因为它直接影响API成本和响应质量。
    - **兼容性**：报告#4167和#4105的用户表明，社区正在尝试将NanoBot与更广泛的第三方API（如Agnes AI, DeepSeek）集成，兼容性问题成为常见痛点。
- **满意点**:
    - **多用户功能的推进**：`per_user_memory` (PR #2968)和`MCP访问控制` (PR #2533) 的合并，回应了多用户部署场景下的核心需求，提升了运营者的满意度。
    - **响应速度**：从`#4105`和`#4220`等issue的提出到有对应的PR出现，表明开发者团队对用户反馈的响应是及时的。

### 8. 待处理积压

- **重要 PR 等待审查/合并**:
    - `#4094` (渠道发送持久化与流身份修复): 已开启8天，关联多个关键Bug ( #4062, #4063, #4064)，修复WebSocket消息丢失和流标识问题，对稳定性至关重要。
    - `#4033` (聊天发送者身份上下文): 开启10天，旨在让NanoBot区分同一频道内的多用户，是提升Discord等场景体验的重要特性。
    - `#4123` (MCP SSRF防护): 开启7天，阻止对不安全HTTP URL的探测，是安全增强的重要一环。

- **长期未响应 Issue**:
    - 未发现长期无人问津的Issue。所有新Issue均在上报后24小时内得到了状态更新（如关闭、打标签或标记为打开），显示项目维护者跟进比较及时。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的Hermes Agent (NousResearch/hermes-agent) GitHub数据，现呈上2026年6月7日的项目动态日报。

---

# Hermes Agent 项目日报 | 2026年6月7日

## 1. 今日速览

今日项目活动水平**极高**，Issue和PR更新数均达到50条，显示出社区与开发团队的高频互动。新版本方面无发布，但大量针对macOS、桌面端和核心网关的Bug修复和高优先级PR被提出，表明项目正经历一轮密集的质量巩固期。社区活跃度较高，围绕**确定性工作流引擎**和**macOS兼容性问题**的讨论最为热烈。总体来看，项目正处于功能迭代向稳定化过渡的攻坚阶段，健康度良好但存在一些亟待解决的兼容性及稳定性问题。

## 2. 版本发布

无。

## 3. 项目进展

过去24小时内有11个PR被合并或关闭，标志着项目在以下方面取得进展：
- **文档与可用性**：`#35565` [CLOSED] 修正了Google Workspace技能的OAuth设置指南，提升了新手配置的准确性。`#40774` [CLOSED] 澄清了Signal平台对工具进度通知的支持情况，改善了跨平台用户文档的准确性。
- **跨平台稳定修复**：`#38358` [CLOSED] 修复了因缺失`--workspace web`标志导致`hermes update`在Windows多workspace仓库上失败的问题。`#22961` [CLOSED] 修复了仪表盘(Web UI)中`vision_analyze`工具结果错误显示为用户消息的界面问题。
- **核心模块修复**：`#34827` [CLOSED] 修复了并发工具调用在检查点前的副作用导致状态竞态条件的Bug。`#31193` [CLOSED] 修复了QQ Bot在断线重连时陷入空转导致CPU占用100%的严重问题。

这些关闭的PR表明项目正稳步修复包括跨平台、UI、核心并发及机器人稳定性在内的关键问题。

## 4. 社区热点

- **热点 Issue: `#5354` [Feature]: Deterministic Workflow Engine (Lobster-style Implementation)**
    - **链接**: [NousResearch/hermes-agent Issue #5354](https://github.com/NousResearch/hermes-agent/issues/5354)
    - **分析**: 该Issue获得了8条评论和8个👍，是今日讨论最热烈的议题。社区核心诉求是为Hermes Agent增加一个可选的确定性工作流引擎，以避免LLM在重复性任务（如监控PR、轮换API密钥）中带来的不必要的Token消耗和延迟。这表明高级用户希望Hermes能更高效地处理确定性任务，而不仅仅是依赖其强大的自主推理能力。社区对“Lobster-style”实现的强烈兴趣暗示了对轻量级、可预测执行模式的偏好。

- **热点 Issue: `#37505` [Bug]: Hermes Desktop macOS DMG is arm64-only and fails on Intel Macs**
    - **链接**: [NousResearch/hermes-agent Issue #37505](https://github.com/NousResearch/hermes-agent/issues/37505)
    - **分析**: 此Bug获得6条评论，突显了macOS桌面端用户基数庞大但存在架构兼容性问题。Intel Mac用户因官方DMG仅提供arm64版本而无法启动应用，这是一个影响范围较广的可用性问题。社区对此的积极反馈表明，对通用二进制（Universal Binary）版本的支持呼声很高。

## 5. Bug 与稳定性

今日报告了大量Bug，按严重性排列如下：

| 严重程度 | Issue ID | 标题 | 状态 | 修复PR |
| :--- | :--- | :--- | :--- | :--- |
| **P1 (Critical)** | `#40831` | macOS 26: PR #40581 hardcodes user/<uid> launchd domain... | OPEN | `#40878` [OPEN] |
| | `#40490` [CLOSED] | CLI input locks up unrecoverably on lazy-dep install prompt... | CLOSED | 已合并 |
| **P2 (High)** | `#38412` | Desktop "Remote gateway" can't connect over WebSocket... | OPEN | 无 |
| | `#39281` | Hermes fails to work using gemma4 with ollama backend... | OPEN | 无 |
| | `#40250` | Terminal escape sequences leaking into response output... | OPEN | 无 |
| | `#40818` | DingTalk proactive messaging does not work... | OPEN | 无 |
| | `#40877` | approval timeout is interpreted by LLM as system failure... | OPEN | 无 |
| | `#40885` | Telegram: user message jumps... during agent processing... | OPEN | 无 |
| **P3 (Medium)** | `#6718` | Background Process Auto-Notifications Not Delivering... | OPEN | 无 |
| | `#40101` | mnemosyne-hermes Plugin: NOT installed... | OPEN | 无 |
| | `#40820` | Desktop installer fails on macOS when path contains spaces... | OPEN | 无 |
| | `#40843` | Camofox HTTP client ignores browser.command_timeout... | OPEN | `#40886` [OPEN] |

**趋势分析**: **macOS相关的兼容性和配置问题**（`#40831`， `#38412`， `#40820`）是今日Bug的核心焦点。此外，**多平台消息适配器**（DingTalk, Telegram, Slack）的稳定性问题也集中爆发，暴露出组件复用和配置管理的脆弱性。

## 6. 功能请求与路线图信号

- **高度契合社区需求**: **`#5354`（确定性工作流引擎）** 和 **`#40873`（音频直通支持）** 这两个Feature请求，均与现有的PR方向一致，有较大概率被纳入后续版本。
- **UI与用户体验增强**:
    - `#40484` (文件树支持删除) 和 `#40890` (`--effort`/`--reasoning` CLI标志) 是提升用户控制力和效率的直接需求，实现成本相对较低，可能被快速采纳。
    - `#40873` (音频直通) 和 `#13529` (Agent活动API和情绪状态暴露) 代表了用户对更丰富交互和更深层次Agent监控的探索需求，路线图优先级取决于项目定位。
- **新Provider集成**: PR `#40910` (AGIone provider) 和 `#40876` (Cursor provider integration) 表明社区和开发团队正积极拓展Hermes的模型支持生态，这将是未来一段时间内的持续主题。

## 7. 用户反馈摘要

- **核心痛点**: **macOS桌面版兼容性堪忧**是用户反馈最集中的痛点，Intel Mac用户被排除在外，且近期更新还引入了新的launchd域问题。**配置管理与权限问题**（如路径含空格、WebSocket拒绝连接）也造成大量困扰。
- **使用场景**: 社区用户已将Hermes广泛集成到Telegram, Discord, DingTalk, Home Assistant等多个平台，并对用于需要**重复执行**（监控、轮换）和**确定性**任务的场景有强烈需求。
- **满意度**: 用户对Hermes的自主推理和工具调用能力基本认可，但**稳定性和跨平台一致性**方面的体验直接影响满意度。`#39281` (gemma4 with ollama) 突出显示了与本地新模型集成时可能出现的“开箱即用”问题。
- **改进建议**: 用户建议包括：改进下载链接的架构支持，为CLI增加更多粒度控制（如`--effort`），以及优化长时间运行会话的时间感知能力（PR `#40881`）。

## 8. 待处理积压

- **长期未响应的关键 Issue**:
    - `#13529` (Agent Activity API & Emotional State Exposure): 创建于4月21日，是一个深度功能请求，涉及Agent状态API暴露，仍为OPEN状态，需要项目维护者评估其优先级和实现方案。
    - `#32217` (SSRF check blocks web tools inside NVIDIA OpenShell sandbox): 创建于5月25日，影响在特定沙盒环境中的用户，问题明确但尚无对应PR，可能由于环境特殊性导致修复优先级不高。

- **未关联修复PR的High Severity Bug**:
    - `#38412` (Desktop "Remote gateway" WebSocket connect fails): 创建于6月3日，对桌面端远程连接体验至关重要，目前无PR，需尽快介入。
    - `#39281` (Hermes fails with gemma4 on ollama): 影响与流行本地模型的兼容性，无PR，应优先排查。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

今日项目活跃度极高，呈现出社区贡献与内部开发齐头并进的良好态势。`chengzhichao-xydt` 贡献了一系列针对代码稳健性的防御性修复补丁，覆盖了多个模块的潜在 panic 和资源泄漏问题。同时，`jcafeitosa` 提交了代号为“EXM”和“EX”的一系列新功能需求，暗示项目正在规划交易和交易所连接相关的高级特性。值得注意的是，一个关于 Windows 平台下 QQ 频道连接失败的 Bug 已被报告，但尚未有修复 PR 关联。整体来看，PicoClaw 不仅在修复现有问题，也在为未来的扩展（如金融交易）铺路，项目健康度强劲。

## 2. 版本发布

- **Nightly 版本**: `v0.2.9-nightly.20260607.7d2b0c2a`
  - **说明**: 这是一个自动化构建的测试版本，可能包含不稳定因素，仅供测试使用。
  - **变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

**行动建议**: 生产环境用户建议继续使用稳定版。开发者和测试者可将此版本用于功能验证。

## 3. 项目进展

今日共有 **15 个 PR 被合并/关闭**，项目在多条战线上取得了关键进展：

- **核心稳定性提升**: `chengzhichao-xydt` 合入了一系列 PR，系统性地修复了：
  - **goroutine 泄漏**: 修复了 `Manager.Reload()` 在重载配置时未取消旧分发任务，导致协程泄漏的问题。([PR #3014](https://github.com/sipeed/picoclaw/pull/3014), [PR #3016](https://github.com/sipeed/picoclaw/pull/3016))
  - **潜在 Panic**: 修复了在 Slack、飞书、LINE 等多个渠道及配置模块中，因未检查类型断言或 nil 值而可能引发的崩溃。([PR #3021](https://github.com/sipeed/picoclaw/pull/3021), [PR #3022](https://github.com/sipeed/picoclaw/pull/3022), [PR #3018](https://github.com/sipeed/picoclaw/pull/3018), [PR #3019](https://github.com/sipeed/picoclaw/pull/3019))
  - **资源完整性**: 优化了base64编码和自更新流程中的错误处理，防止在IO错误下产生损坏的输出文件。([PR #3017](https://github.com/sipeed/picoclaw/pull/3017), [PR #3023](https://github.com/sipeed/picoclaw/pull/3023))

- **新功能与优化**:
  - **Slack 渠道增强**: 合并了 PR，改进了 Slack 消息格式化和渠道路由，包括新增跳闸/忽略过滤功能。([PR #3020](https://github.com/sipeed/picoclaw/pull/3020))
  - **工具安全性修复**: 修复了 `restrict_to_workspace` 安全限制下，`exec` 工具错误地将无协议前缀的 URL（如 `wttr.in/Beijing?T`）识别为绝对路径的问题。([PR #2965](https://github.com/sipeed/picoclaw/pull/2965))

**项目迈向**：通过对多个关键模块的 Golang 代码质量修复，项目的整体健壮性和安全性得到显著增强，为后续开发更复杂的功能（如交易特性）奠定了基础。

## 4. 社区热点

今日社区讨论的热点主要集中在两项议题：

1.  **Agent-to-Agent 通信** (#2929)
    - **活跃度**: 3条评论，2个👍赞。
    - **诉求**: 用户 `afjcjsbx` 提出当前多Agent模式（`spawn`, `subagent`）是单向的，缺乏让 Agents 作为对等体进行直接通信的一流机制。这反映出社区对更复杂、更灵活的协作代理模式有明确的需求。
    - **链接**: [Issue #2929](https://github.com/sipeed/picoclaw/issues/2929)

2.  **WhatsApp 编译支持** (#2625)
    - **活跃度**: 8条评论（该 Issue 存在时间较长，但仍在近期有互动）。
    - **诉求**: 用户 `duckida` 提出，Raspberry Pi 等 arm64 设备的默认预编译版本不包含 WhatsApp 支持，导致用户难以便捷更新。这暴露出预构建发布物对特定平台需求的覆盖不足。
    - **链接**: [Issue #2625](https://github.com/sipeed/picoclaw/issues/2625)

## 5. Bug 与稳定性

今日报告的 Bug 数量不多，但质量较高：

- **严重 - Windows QQ 频道连接失败** ([Issue #3015](https://github.com/sipeed/picoclaw/issues/3015))
  - **现象**: Windows 版本 `picoclaw gateway` 启动时，因获取 `bots.qq.com` 的访问令牌超时而失败，导致 QQ 频道连接异常。
  - **影响**: 影响 Windows 用户使用 QQ 渠道功能。
  - **状态**: **OPEN**，目前无关联修复 PR。需要优先级评估。

- **其他已修复的稳定性问题**:
  - **goroutine 泄漏** (**已修复** via [PR #3014](https://github.com/sipeed/picoclaw/pull/3014) & [PR #3016](https://github.com/sipeed/picoclaw/pull/3016))
  - **多处 nil 指针 panic** (**已修复** via [PR #3021](https://github.com/sipeed/picoclaw/pull/3021) & [PR #3022](https://github.com/sipeed/picoclaw/pull/3022))

## 6. 功能请求与路线图信号

今日涌现了大量新增功能请求，呈现出向**金融交易**领域进军的鲜明信号：

- **交易/金融模块（EXM & EX 系列）**: 用户 `jcafeitosa` 一次性提交了 **8 个** 关于交易所连接和交易 CLI 的 Issue。
  - **CLI 结构**: 建议新增 `clawtrade` 命令，包含 `trade`, `backtest`, `agent`, `status` 子命令。 ([#3032](https://github.com/sipeed/picoclaw/issues/3032))
  - **CI/CD 自动化**: 建议搭建 GitHub Actions 流水线进行测试、构建和 lint。 ([#3031](https://github.com/sipeed/picoclaw/issues/3031))
  - **核心消息系统**: 提出 `ClawHub` 消息类型定义。 ([#3030](https://github.com/sipeed/picoclaw/issues/3030))
  - **交易所连接**: 包含风险管理器接口 ([#3029](https://github.com/sipeed/picoclaw/issues/3029))、高性能锁无关订单簿 ([#3027](https://github.com/sipeed/picoclaw/issues/3027)) 以及 Binance 交易所的 REST ([#3026](https://github.com/sipeed/picoclaw/issues/3026)) 和 WebSocket ([#3025](https://github.com/sipeed/picoclaw/issues/3025)) 连接器实现。这些特性都要求遵循 TDD（测试驱动开发）和高性能标准。

**潜在路线图**: 这批 Issue 的结构和编号（如 EXM-001, EX-001）显示了明确的规划，这是否意味着 PicoClaw 将从一个通用的 AI Agent 框架，延伸出针对量化交易或金融分析的子项目？这些特性若被纳入，将是路线图上的重大转折。

## 7. 用户反馈摘要

- **痛点**:
  - **编译版本边缘支持不足**: 用户的反馈 (#2625) 再次表明，自动构建的预编译版本对非主流平台或特定功能的支持是普及过程中的绊脚石。社区希望官方能提供更多针对性的“全功能”编译版本。
  - **高级协作机制缺失**: 高级用户感觉当前的多Agent能力有限，渴望对等通信这种更灵活的原语。
- **使用场景**:
  - 个人开发者使用树莓派 (Raspberry Pi) 作为轻量服务器运行 PicoClaw，并将其与 WhatsApp 集成，这代表了边缘侧 AI 助手的典型用例。
  - 新一批 Issue 暗示了在量化交易中使用 AI Agent 进行策略回测或执行的可能性。

## 8. 待处理积压

- **问题 #2625**: [Provide compiled builds with WhatsApp support](https://github.com/sipeed/picoclaw/issues/2625)
  - 这是一个被标记为 `stale` 的旧 Issue，但仍有社区关注。虽然 PR [#1112](https://github.com/sipeed/picoclaw/pull/1112) 解决了协议识别问题，但核心的“为 arm64 提供 WhatsApp 支持”的编译需求仍未解决。维护团队应考虑在构建系统中增加对此类特定功能的编译配置。
- **PR #2935**: [docs(i18n): add Traditional Chinese (zh-TW) locale and READMEs](https://github.com/sipeed/picoclaw/pull/2935)
  - 这是一个已开放两周的文档翻译 PR，且已被标记为 `stale`。作为一个面向全球的开源项目，国际化支持至关重要。建议维护者尽快审查并合并，以避免挫伤外部贡献者的积极性。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是为您生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

今日项目活跃度较高，共处理了 **14 条 Pull Request**，其中 **3 条已合并/关闭**，**11 条待合并**。社区贡献集中爆发，尤其是针对 **Slack、Signal 适配器**以及**容器运行**的修复，表明项目正在解决早期用户遇到的核心集成与部署问题。虽然有两个新 Issue 报告了安装引导流程和命令执行的缺陷，但社区已迅速提交了相关的修复 PR，展现了良好的协作生态。**大量历史 PR 仍在积压**（共 11 条），可能成为项目健康度的一个隐患。

## 3. 项目进展

今日合并/关闭的 **3 条 PR** 对项目起到了关键的维护和加固作用：

- **技能库规范化**：**PR #2698** 和 **PR #2696** 由同一贡献者合并，旨在对技能库进行全面“改造”，使其符合一套升级维护的新规范。这包括为每个技能添加测试、确保导入路径与核心库重命名后保持一致、添加 `REMOVE.md` 等。这显著提升了项目结构的健壮性和技能的可维护性。
  - 链接: [#2698](https://github.com/nanocoai/nanoclaw/pull/2698)
  - 链接: [#2696](https://github.com/nanocoai/nanoclaw/pull/2696)
- **防止消息重复**：**PR #2697** 被合并，引入了主机单实例锁，解决了因多个进程同时运行（如开发模式和安装服务）而导致的**重复消息投递**问题。这是一个关键的生产环境稳定性修复。
  - 链接: [#2697](https://github.com/nanocoai/nanoclaw/pull/2697)

## 4. 社区热点

今日讨论最活跃的区域集中在Slack和Signal通道适配器的修复上。

- **热点 1：Slack Socket Mode 适配**：**Issue #2703**（报告安装引导后 `chat hi` 命令挂起）和 **PR #2702**、**#2700**（修复 Slack 适配器使用 Socket Mode）共同构成了一个热点。社区核心矛盾在于：项目的官方“推荐安装路径”仍停留在早期的 HTTP Webhook 模式，而代码库的其他部分已转向更易于本地开发和调试的 **Socket Mode**。用户遵循旧文档会遇到严重错误，而社区贡献者正积极通过 PR 来纠正这个文档与代码之间的偏差。
  - 链接: [#2703](https://github.com/nanocoai/nanoclaw/issues/2703)
  - 链接: [#2702](https://github.com/nanocoai/nanoclaw/pull/2702)
  - 链接: [#2700](https://github.com/nanocoai/nanoclaw/pull/2700)

- **热点 2：Signal 适配器功能缺失**：贡献者 `cfis` 今天提交了三条针对 Signal 适配器的 PR (**#2695, #2694, #2693**)，修复了图片附件无法读取和私信消息被静默丢弃等核心功能缺陷。这表明 Signal 用户的社区需求正在被积极满足，但同时也暴露了该适配器初始版本的成熟度不足。
  - 链接: [#2695](https://github.com/nanocoai/nanoclaw/pull/2695)
  - 链接: [#2694](https://github.com/nanocoai/nanoclaw/pull/2694)
  - 链接: [#2693](https://github.com/nanocoai/nanoclaw/pull/2693)

## 5. Bug 与稳定性

今日报告的 Bug 主要影响新手首次体验和 Signal 用户，严重程度中等。

- **严重 (Critical)**：
  - **安装引导流程缺陷**：Issue #2703 报告，按照**推荐**路径安装后，`pnpm run chat hi` 命令会**挂起 120 秒**并超时退出，原因是 `cli/local` 未被正确连接，但安装完成时却诱导用户使用该命令。这是一个严重影响新用户 onboarding 体验的 Bug。贡献者已提交 PR #2702 初步定位了问题根源（Slack 适配问题）。
    - 链接: [#2703](https://github.com/nanocoai/nanoclaw/issues/2703)
  - **Signal 私信丢失**：Issue #2694 指出 Signal 适配器因未正确设置 `isMention`/`isGroup` 标志，导致所有来自 Signal 的**私信 (DM) 被静默丢弃**。贡献者已提交 **PR #2694** 进行修复。
    - 链接: [#2694](https://github.com/nanocoai/nanoclaw/pull/2694)

- **中等 (Medium)**：
  - **重建命令逻辑错误**：Issue #2701 报告，当 `packages_apt` 和 `packages_npm` 均为空时，`ncl groups restart --rebuild` 命令会报错“无包可安装”。逻辑上，`--rebuild` 应跳过包安装，这是一个违反直觉的设计缺陷，但影响范围有限。
    - 链接: [#2701](https://github.com/nanocoai/nanoclaw/issues/2701)

## 6. 功能请求与路线图信号

- **Signal 适配器增强**：PR #2693 添加了 `/add-google-contacts-tool` 技能，这标志着一个新趋势，即将 Google Workspace 工具（如 Gmail, GCal, GPeople）通过 MCP 协议集成进来。这可能是项目向**更强大的个人助理**方向发展的一个路线图信号。
  - 链接: [#2693](https://github.com/nanocoai/nanoclaw/pull/2693)
- **MCP 协议扩展**：积压 PR **#2208** 提议支持 HTTP 和 SSE 传输的 MCP 服务器。今天关于 Google Contacts 工具和 Signal 适配器的功能都依赖于 MCP，这项底层能力的扩展将是未来支持更多外部服务的基础。
  - 链接: [#2208](https://github.com/nanocoai/nanoclaw/pull/2208)

## 8. 待处理积压

目前有 **11 条** Pull Request 处于待合并状态，其中多条已开启超过一个月，可能已进入“僵尸”状态。需特别关注以下几条：

- **关键 Bug 修复**：`cfis` 提交的关于 `poll-loop` 的 **PR #2531** 和 **PR #2184**，以及关于`container-runner`的 **PR #2230** 和 **PR #2349** 处于开启状态已超过一个月。这些修复涉及会话处理、容器安全等底层稳定性，优先级应提高。
  - 链接: [#2531](https://github.com/nanocoai/nanoclaw/pull/2531)
  - 链接: [#2184](https://github.com/nanocoai/nanoclaw/pull/2184)
  - 链接: [#2230](https://github.com/nanocoai/nanoclaw/pull/2230)
  - 链接: [#2349](https://github.com/nanocoai/nanoclaw/pull/2349)
- **MCP 功能增强**：**PR #2208** 作为一项重要的功能增强，其整合周期过长可能会阻碍后续关联功能的开发。
  - 链接: [#2208](https://github.com/nanocoai/nanoclaw/pull/2208)

---
*报告生成时间: 2026-06-07*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的IronClaw项目数据，现呈上2026-06-07的项目动态日报。

---

## IronClaw 项目动态日报 (2026-06-07)

### 1. 今日速览

今日IronClaw项目活跃度极高，主要由核心贡献者推动。**过去24小时内，共有31个PR被更新，其中10个被合并或关闭，显示了强劲的代码推进速度。** 项目进展主要集中在 **“Reborn”重构** (包括子代理、渠道路由、扩展生命周期) 和 **“Codex”模块** (包括端点、审批、偏好) 的功能开发上。虽然新开Issues数量不多，但一个持续的Nightly E2E测试失败问题值得关注。整体来看，项目处于快速迭代期，健康状况良好。

### 2. 版本发布

*无新版本发布。*

### 3. 项目进展

今日多个重要PR被合并或关闭，标志着项目在多个关键领域取得实质进展：

- **Reborn 架构推进：**
    - [#4508 [CLOSED] [codex] Gate repeated-call stops behind warning](https://github.com/nearai/ironclaw/pull/4508) 重构了“重复调用”的处理机制，将其从直接停止变为警告，对用户体验和模型行为控制更为精细。
    - [#4509 [CLOSED] [size: XL] Add Slack channel subject routing](https://github.com/nearai/ironclaw/pull/4509) 新增了多尺寸的Slack频道主题路由功能，增强了渠道的灵活配置。
    - [#4486 / #4485 [CLOSED] docs(reborn): subagent + compaction unified design](https://github.com/nearai/ironclaw/pull/4486) 合并了关于“子代理”和“上下文压缩”的统一设计文档，为复杂的后台任务和长对话管理奠定了架构基础。

- **CI与工具链优化：**
    - [#4520 [CLOSED] ci: keep Reborn-only PRs out of legacy tests](https://github.com/nearai/ironclaw/pull/4520) 优化了CI流程，将仅影响“Reborn”的PR与遗留测试隔离，将显著提高开发效率和CI可靠性。

- **核心功能修复：**
    - [#4523 [OPEN] fix(host_api): round-trip system sentinel...](https://github.com/nearai/ironclaw/pull/4523) 修复了一个关键的序列化/反序列化不对称问题，该问题可能导致LLM设置功能失败 (`service_unavailable`)。此PR虽未合并，但已被提出，表明项目对稳定性的高度关注。

### 4. 社区热点

今日讨论最为活跃和受关注的PR主要来自核心贡献者，体现了团队内部的高强度协作。虽然没有大量的社区外部互动，但以下PR因其复杂度和对项目路线图的重要性而突出：

- **[#4522 [OPEN] feat(llm): scaffold tool_args.rs shared parsing primitives](https://github.com/nearai/ironclaw/pull/4522)**：该PR作为RC3/M9阶段A的一部分，着手构建LLM提供商解析框架的基础工具。其重要性在于为后续统一提供商的参数解析（解决RC1审计问题）铺平道路。开发者正积极构建这一能力。
- **[#4511 [OPEN] [size: XL] [codex] Add outbound preference facade contracts](https://github.com/nearai/ironclaw/pull/4511)**：此PR为“Codex”模块添加出站偏好门面合约，其“XL”尺寸和“core”贡献者标签表明这是一个复杂且关键的功能，旨在为未来的产品工作流提供高度可配置的出站行为。

社区（主要是内部和贡献者）的关注点集中在 **“Reborn”重构的集成** 和 **“Codex”新功能** 上，旨在将项目从一个基础框架演变为一个更智能、更具产品化能力的平台。

### 5. Bug 与稳定性

今日报告了一个中等严重程度的稳定性问题：

- **[#4108 [OPEN] Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)** (严重程度: 中)：由CI机器人自动报告的Nightly端到端测试失败。失败的工作流是“Full E2E / E2E (extensions)”。虽然该Issue已存在数日，但未能及时关闭，表明问题的根因可能比较复杂。**目前尚无明确的fix PR与此Issue直接关联**，需要项目维护者重点关注，以避免回归。

此外，**PR #4523** 直接修复了可能导致 `service_unavailable` 的API中的Bug，此修复正待合并，是维持核心稳定性的关键。

### 6. 功能请求与路线图信号

虽然纯功能请求的Issues不多，但从大量活跃的PR可以清晰地看到项目路线图的执行方向：

- **“Reborn” 产品化**： (PR #4519, #4516, #4517) 正在为WebUI添加会话能力端点、线程删除功能，并实现配置文件的首次启动种子化。这些功能表明“Reborn”正在从实验阶段走向可用。
- **“Codex” 智能模块**： (PR #4186, #4510) 正在开发本地开发审批门户和Slack渠道管理功能。这表明“Codex”正被构建为一个强大的审批和工作流管理系统。
- **OpenAI 兼容性**： (PR #4489, #4495) 正在添加OpenAI兼容的产品引用和路由聊天补全功能。这是一个强烈的信号，表明项目计划在**保持与主流API标准的兼容性**方面进行投资，以吸引更广泛的用户和工具生态。

**结论：** 下一版本（如果有）将是一个重大的功能版本，核心是“Reborn”的产品化落地和“Codex”的工作流能力强化，并可能提供OpenAI API的兼容层。

### 7. 用户反馈摘要

今日无新增Issues或PR评论提供直接的用户反馈。所有活跃的讨论和代码贡献主要来自项目核心团队和常规贡献者。项目当前阶段似乎更侧重于**内部架构重构和核心功能开发**，而不是收集外部用户的使用反馈。当“Reborn”模块和“Codex”功能达到更稳定的阶段后，预计会有更多的用户参与和反馈。

### 8. 待处理积压

以下Issue/PR需要维护者关注：

- **[#4108 [OPEN] Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)**：如上所述，一个持续数日的Nightly测试失败，且没有明确定义的修复路径，这是一个潜在的风险点。
- **[#4002 [OPEN] chore(deps): bump the actions group...](https://github.com/nearai/ironclaw/pull/4002)**：一个来自 Dependabot 的 PR，过去数月未合并，建议安全性更新。长期积压的依赖更新可能导致安全风险，建议定期合并。
- **[#3981 [OPEN] [size: M] test: cover runtime HTTP redaction markers](https://github.com/nearai/ironclaw/pull/3981)**：一个由“new”贡献者提出的测试增强PR，旨在覆盖运行时HTTP标签。长时间未处理可能打击新贡献者的积极性。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI 项目数据，我为您生成了 2026-06-07 的项目动态日报。

---

# LobsterAI 项目动态日报 (2026-06-07)

## 1. 今日速览

今日项目活跃度**中等偏低**。过去24小时内没有新版本发布，但有2个重要的历史Pull Request被合并关闭，为项目带来了批量导出和定时任务管理方面的实质进展。社区反馈方面，用户提交了1个新Issue（#2120），提出了多项建设性建议。值得注意的是，项目存在一个由5个陈旧Issue组成的 **“无保存确认”Bug系列**，近期被重新激活讨论，但尚未有修复PR与之关联，这可能成为用户配置体验的隐患。

## 2. 版本发布

无

## 3. 项目进展

今日有2个历史Pull Request被合并，标志着两个重要功能的正式落地：

- **批量会话导出功能（#1529）**：由社区贡献者 `MaoQianTu` 开发。该功能在批量模式（cowork）下新增了导出按钮，允许用户将选中的多个会话一键导出为一个结构化的JSON文件。这极大地提升了用户的数据备份和迁移能力。
- **定时任务归属功能（#1530）**：由团队成员 `gongzhi-netease` 开发。针对多Agent场景，此功能在新建定时任务时增加了Agent选择器，允许用户指定任务归属于哪个Agent。这解决了之前所有任务隐式归属于 main Agent导致的混乱问题，使得任务管理和权限划分更加清晰。

这两个PR的合并使得项目在**数据自主权**和**任务精细化管理**方面迈出了重要一步，整体健康度有所提升。

## 4. 社区热点

今日最受关注的Issue是 #2120 **“建议”**，由用户 `nbjoe` 提交。该Issue在24小时内获得了1条评论，并一口气提出了3项具体建议。虽然点赞数为0，但其内容质量高，直击用户日常使用中的痛点，引发了维护者的讨论。

**核心诉求分析**：
1.  **任务预输入**：借鉴同类产品，用户在运行当前任务时可以预输入下一个任务，以提高工作流的连续性。
2.  **延长任务运行时长**：用户在进行长时间的数据监控脚本时，遭遇了 `terminated` 提示，认为单次任务的运行时长限制影响了开发工作。
3.  **UI布局优化**：在高分辨率屏幕（2560*1600）下，技能界面双列布局视觉效果不佳，建议改为三列。

这表明用户对LobsterAI的定位已从简单的对话助手，向**自动化工作流平台**和**专业开发工具**演进。用户开始关注任务编排、长时间运行稳定性以及高DPI适配等进阶体验。

- 链接：[建议 #2120](https://github.com/netease-youdao/LobsterAI/issues/2120)

## 5. Bug 与稳定性

今日无新Bug报告。然而，一个由社区贡献者 `MaoQianTu` 在4月份集中报告的 **“未保存确认”Bug系列（#1468, #1469, #1470）** 在今天被自动标记为陈旧（stale）并触及了评论更新，虽然未修复，但再次引起了关注。该系列包含3个高度相似的问题：

1.  **创建Agent弹窗 (#1468)**：关闭弹窗时，已填写的Agent名称、系统提示词等会静默丢失。
2.  **Agent设置面板 (#1469)**：修改配置后直接关面板，修改内容会静默丢失。
3.  **MCP服务器配置弹窗 (#1470)**：配置环境变量（如API Key）后，通过X、Cancel、Escape键关闭弹窗，配置会静默丢失。

**严重程度评估：高**。该Bug系列直接导致用户可能因为一个无意间的操作而丢失大量配置工作，尤其是`MCP服务器配置`涉及API Key等敏感信息，静默丢失会带来极差的用户体验，且极易引发用户不满。目前，**没有关联的修复PR**，这是一个不容忽视的稳定性问题。

- 链接：[Bug #1468](https://github.com/netease-youdao/LobsterAI/issues/1468)
- 链接：[Bug #1469](https://github.com/netease-youdao/LobsterAI/issues/1469)
- 链接：[Bug #1470](https://github.com/netease-youdao/LobsterAI/issues/1470)

## 6. 功能请求与路线图信号

今日收到的功能请求主要来自 #2120，其中**“任务预输入”**和**“延长单次任务时长”**两项需求，与项目近期合并的PR `#1530 (定时任务归属)` 和 `#1529 (批量导出)` 的价值导向一致，都是朝着**更强大的任务编排和工作流自动化**方向前进。

- **信号解读**：虽然这些是用户建议，但它们非常契合LobsterAI从“聊天机器人”向“AI Agent平台”转型的战略。**“任务预输入”** 类似于任务队列，能有效提升工作流连续性，很可能被项目团队评估并纳入后续版本的 `cowork` 或 `scheduledTask` 模块中。**“延长任务时长”** 则可能涉及底层运行时优化或增加配置选项，对于价值用户（如开发者）而言至关重要。

## 7. 用户反馈摘要

从近期Issues的评论中可以提炼出以下用户痛点和使用场景：

- **数据丢失恐惧**：多个关于“无保存确认”（#1468，#1469，#1470）的Bug报告被顶起，反映出用户对在配置复杂的Agent和MCP服务器时丢失工作的强烈担忧。
- **稳定性焦虑**：用户 `xuzhiwu123` 报告了**进程无故中断**的问题（#1495），且获得了1个点赞，表明该问题并非个例。用户正在疑惑这是客户端Bug还是大模型问题，这种不确定性会严重影响用户对产品的信任度。
- **专业用户场景显现**：用户 `nbjoe`（#2120）的使用场景是非常典型的**开发者利用AI Agent监控数据抓取脚本**。这表明LobsterAI已经吸引了具备编程能力的深度用户，他们对产品的稳定性、任务时长、以及多任务编排能力提出了更高要求。

## 8. 待处理积压

以下Issue具有较高重要性但长时间没有实质进展，需要项目维护者重点关注：

1.  **“无保存确认”Bug系列 (#1468, #1469, #1470)**：这三个Bug自4月4日创建至今已超过2个月，虽然被标记为陈旧，但被许多用户看到（评论数）。这是典型的用户体验问题，修复成本不高但影响力巨大。建议尽快分配资源修复。
2.  **进程无故中断 (#1495)**：此问题关乎产品的核心稳定性。自4月7日创建以来只有1条评论且无人解决。建议维护者主动联系用户 `xuzhiwu123` 获取更多日志或复现步骤，排查是客户端（如资源限制）还是模型端（如超时）的问题。
3.  **任务显示完成但未返回 (#1496)**：与 #1495 同属稳定性问题。该Bug可能影响核心使用流程，同样缺乏关注。建议合并分析，排查是否与任务调度或UI状态更新有关。
    - 链接：[Bug #1496](https://github.com/netease-youdao/LobsterAI/issues/1496)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目 2026-06-07 动态日报。

---

## Moltis 项目日报 | 2026-06-07

### 1. 今日速览
项目今日活跃度较低，24小时内未合并任何PR或发布新版本，主要活动集中在社区反馈环节。共收到3条新Issue，其中包含2个Bug报告和1个功能请求，但均未获得广泛讨论。整体来看，项目处于相对平静的开发阶段，社区反馈的Bug主要集中在功能模块的可用性上，暂无严重或阻塞性问题上报。

### 2. 版本发布
无

### 3. 项目进展
无

### 4. 社区热点
今日暂无讨论特别活跃或获得较多点赞评论的议题。所有新开Issue均无评论或仅有1条（#1112），且点赞数均为0。这表明社区尚未对新提出的问题进行深入探讨。

### 5. Bug 与稳定性
今日共报告2项Bug，严重程度均为中等，主要影响特定功能模块的交互体验，暂无紧急修复PR。

- **[Bug] Docker环境下禁用认证功能无效** : 用户报告在Docker部署中，关闭认证的配置未生效。这直接影响部署安全性，属于关键配置问题。
  - **链接**: [Issue #1112](https://github.com/moltis-org/moltis/issues/1112)
- **[Bug] 归档Cron任务会话无可见效果** : 用户执行归档操作后，界面没有任何视觉反馈或状态变化。属于UI/UX层面的功能故障。
  - **链接**: [Issue #1111](https://github.com/moltis-org/moltis/issues/1111)

### 6. 功能请求与路线图信号
社区提出了一项新功能请求，旨在优化Cron任务的管理体验：

- **[Feature] 新增静默Cron任务的关键字** : 用户希望引入类似 `NO_REPLY` 的关键词，用于在Cron任务执行时抑制特定的通知消息。这表明用户对减少Cron任务带来的信息噪音有明确需求，可能成为版本迭代中改进Cron系统的一部分。
  - **链接**: [Issue #1110](https://github.com/moltis-org/moltis/issues/1110)

### 7. 用户反馈摘要
由于今日Issue均无深入讨论，用户反馈主要来自其摘要描述：
- **痛点**：用户在使用Docker部署和Cron基础功能时遇到了“配置不生效”和“操作无反馈”的问题，这直接影响了核心功能的可用性和用户体验。
- **使用场景**：用户正在使用标准的Docker部署模式，并依赖Cron功能进行日常会话管理。用户期望能按需调整安全策略（认证开关）并有效管理历史会话（归档）。

### 8. 待处理积压
今日无新增待处理积压项。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据您提供的CoPaw项目数据，生成了以下项目动态日报。

---

# CoPaw 项目动态日报 | 2026年6月7日

## 今日速览

今日CoPaw项目的社区活跃度**较高**，主要集中在Bug修复和功能建议上。24小时内收到了11个Issue更新，但无任何PR提交或合并，表明项目目前可能处于**问题高发反馈期**或**版本迭代的间歇期**。社区用户对新版本(v1.1.10)的稳定性表现出强烈关注，尤其在Windows兼容性、特定模式下的会话切换以及本地模型支持方面出现了多个回归性Bug。此外，用户对于会话管理和执行交互提出了明确的体验改进需求，项目健康度评估为 **“关注”**状态，需尽快响应并修复关键问题。

## 版本发布

**无**。近24小时内无新版本发布。

## 项目进展

**无**。过去24小时内没有任何Pull Requests被提交、合并或关闭。这意味着项目核心代码的推进暂时停滞，开发团队可能正在处理今日集中涌现的Bug或进行内部评审。

## 社区热点

今日最受关注的Issue是 **#4937 [Bug]: `/compact` 命令忽略模型配置的 `max_input_length`**，该问题自6月3日提出后持续活跃，拥有5条评论。用户 `Timqt` 报告，即使为MiniMax M3模型配置了512K的上下文窗口，`/compact`命令仍然使用128K的默认值进行压缩，导致模型能力无法完全发挥。此问题与已关闭的 **#4661**（关于记忆压缩配置未生效）高度相关，反映出**上下文压缩逻辑与模型配置的解耦问题**是当前用户普遍遇到的痛点，属于高优先级需要修复的缺陷。

- **链接**: [Issue #4937](agentscope-ai/QwenPaw Issue #4937) | [Issue #4661](agentscope-ai/QwenPaw Issue #4661)

## Bug 与稳定性

今日报告了7个Bug，其中多个为高严重性问题。按严重程度排列如下：

1.  **[高] Issue #4988: Windows 路径超限**：Session文件名因重复拼接ID导致 `MAX_PATH` 溢出。这是一个在v1.1.10版本中出现的回归性Bug，严重阻碍Windows用户使用，**亟需修复**。
    - **链接**: [Issue #4988](agentscope-ai/QwenPaw Issue #4988)

2.  **[高] Issue #4987: Coding Mode 会话切换失败**：在v1.1.10中，Coding Mode下切换会话总是不成功，此为v1.1.9中的正常工作流。该Bug会严重影响在编程模式下的工作效率。
    - **链接**: [Issue #4987](agentscope-ai/QwenPaw Issue #4987)

3.  **[高] Issue #4989: 本地部署模型无响应**：v1.1.9 及 v1.1.10版本使用本地 `千问3.6-27B` 模型时，提交问题后系统无回复且无报错日志。在v1.1.5.post2版本中正常工作，这是一个严重的新版本回归问题，**可重现性高**。
    - **链接**: [Issue #4989](agentscope-ai/QwenPaw Issue #4989)

4.  **[中] Issue #4990: 企业微信工具调用信息关闭后报错**：在企业微信频道中，关闭工具调用的返回信息后，会错误地返回“抱歉，我无法回答你的问题”。
    - **链接**: [Issue #4990](agentscope-ai/QwenPaw Issue #4990)

5.  **[中] Issue #4985: 文件删除命令显示不换行**：属于交互显示问题，影响用户体验但不影响核心功能。
    - **链接**: [Issue #4985](agentscope-ai/QwenPaw Issue #4985)

6.  **[低] Issue #4937: `/compact` 命令忽略模型配置**：未遵从用户明确配置，属于功能性Bug。
    - **链接**: [Issue #4937](agentscope-ai/QwenPaw Issue #4937)

7.  **[低] Issue #4984: 聊天频道无法审批**：用户已自行确认是未查看文档导致的误报，已关闭。
    - **链接**: [Issue #4984](agentscope-ai/QwenPaw Issue #4984)

*注：以上Bug目前均无对应的Fix PR。*

## 功能请求与路线图信号

用户今日提出了3个新功能请求，主要聚焦于**用户体验和渠道扩展**：

1. **Issue #4971: 会话管理改进**：用户 `henryliuwork` 建议增加一栏会话侧边栏，实现一键切换，当前需要点击两次才能切换，操作繁琐。这是一个**高价值、低成本的UI改进**，很可能被纳入下一个版本。
    - **链接**: [Issue #4971](agentscope-ai/QwenPaw Issue #4971)

2. **Issue #4986: Shell/文件执行实时交互反馈**：用户 `rescodexx` 参考Cursor/WorkBuddy，提出在执行Shell命令或写文件时，需要实时显示交互信息，而不是让用户感觉“卡住了”。这是对**智能体执行过程透明化**的强烈需求，代表了AI助手向“协作者”演进的关键信号。
    - **链接**: [Issue #4986](agentscope-ai/QwenPaw Issue #4986)

3. **Issue #4886: 支持MAX Messenger渠道**：来自俄语用户的请求，希望接入俄语区主流IM平台，以完善“Every channel”概念，可能对**开拓俄罗斯市场**具有战略意义。
    - **链接**: [Issue #4886](agentscope-ai/QwenPaw Issue #4886)

## 用户反馈摘要

- **正面反馈**：用户在Issue #4984中通过社区提问最终自己找到了解决方案（`/approval approve` 命令），并对项目的支持表达了感谢。
- **负面/痛点反馈**：
    - **版本升级问题**：用户普遍在从旧版本（如v1.1.5.post2, v1.1.7）升级到新版本后遇到问题，例如模型驱动不工作、上下文压缩配置失效等。这表明**版本升级的兼容性测试**需要加强。
    - **配置困惑**：多位用户对上下文压缩的配置方式感到困惑，特别是在全局配置消失、仅剩模型配置后，配置仍不生效。这暴露了**配置逻辑和文档清晰度**的不足。
    - **交互体验**：用户明确指出了会话切换繁琐、执行过程无反馈、文件删除命令显示不友好等问题，表明用户对产品的交互细节有较高期待。

## 待处理积压

- **Issue #4937: `/compact` 命令 Bug**：已开放4天，评论数较多，与核心功能“上下文管理”相关且与 #4661 问题属于同一类，需维护者尽快介入确认并分配优先级。
- **长期未响应 Issue**：根据数据概览，当前无明确标记为长期未响应的重要Issue。但需要关注**所有今日新增且无开发人员回复的Bug**，特别是Issue #4988, #4987, #4989这三个严重回归问题，防止其变为积压。

---

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，现根据您提供的ZeptoClaw项目GitHub数据，生成2026年6月7日的项目动态日报。

---

## ZeptoClaw 项目动态日报 | 2026年6月7日

### 1. 今日速览

今日项目活跃度适中，主要围绕**二进制体积优化与CI看门狗**这一核心议题展开。昨日有2个相关的 Issue 更新（1个关闭，1个新开），以及1个待合并的PR。项目团队正在积极推进将二进制体积作为PR合并的硬性门槛，以维持“能在机器人上运行”的战略优势。整体来看，项目处于**精细化运维和性能调优阶段**，社区反馈主要集中在二进制体积的监控粒度与门槛设定上。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

**PR状态更新：**
- **#611 [OPEN] chore(ci): promote binary-size to PR gate at 7.5MB**
  - **进展**：该PR旨在将已有的`binary-size` CI任务从仅对主分支生效，转变为对所有PR的直接门槛。目前PR已打开，正在等待合并。它标志着项目对二进制体积的监控从“事后审查”升级为“事前阻断”。
  - **链接**：[PR #611](https://github.com/qhkm/zeptoclaw/pull/611)

**Issue状态更新：**
- **#612 [CLOSED] chore(perf): audit ~800KB binary-size drift since 6.2MB low water mark, tighten gate to 7MB**
  - **进展**：该Issue已关闭，但它与PR #611 密切相关。它指出当前二进制体积（6.98MB）距离7MB战略目标仅有21KB余量，因此建议将CI门槛收紧至7MB。该Issue的关闭表明团队已接受其分析结论。
  - **链接**：[Issue #612](https://github.com/qhkm/zeptoclaw/issues/612)

**项目迈进总结：**
虽然PR #611还未合并，但其打开的讨论和关联Issue的关闭表明，项目团队正在**迅速响应并采纳社区/内部关于二进制体积优化的建议**。CI策略从“观察”到“干预”的转变，是保障项目轻量化、嵌入式部署能力的关键一步。

### 4. 社区热点

- **讨论焦点：二进制体积CI门槛的设定**
  - 当前讨论集中在PR #611（门槛为7.5MB）与新开Issue #629（建议为aarch64目标设置7MB门槛）的矛盾点上。
  - **#629 [OPEN] chore(ci): add aarch64 binary-size gate at 7MB**
    - **诉求**：作者（qhkm）指出，项目真正的“机器人护城河”在于aarch64架构（如树莓派、Jetson），而目前的CI门槛是针对x86_64的11MB。用户希望为aarch64单独设置一个更严格的7MB门槛，以真正保证轻量化。
    - **链接**：[Issue #629](https://github.com/qhkm/zeptoclaw/issues/629)
  - **分析**：社区（主要来自维护者自身）的深层诉求是 **“指标与实际目标匹配”** 。仅仅设置一个能过编译的门槛是不够的，门槛的阈值必须与产品的核心战略（低资源设备部署）对齐。这是一个关于CI策略精细化管理的高质量讨论。

### 5. Bug 与稳定性

**今日无新增Bug、崩溃或回归问题报告。**

项目当前状态稳定，未发现严重问题。

### 6. 功能请求与路线图信号

- **功能请求：为 aarch64 平台设置独立的二进制体积CI门槛**
  - **来源**：Issue #629
  - **状态**：新开，尚未有PR关联。
  - **预测**：考虑到 #612 和 #611 的快速迭代，此功能请求（优化CI策略）大概率会被采纳并进入下一版本或CI配置中。它明确了“一刀切”的门槛设定方式需要根据不同架构进行差异化处理，是CI策略的重要完善。

### 7. 用户反馈摘要

虽然项目是个人AI助手，但目前活跃的反馈来源主要是项目维护者（qhkm）自身对自己项目的审查和优化。

- **痛点/关注点**：二进制体积膨胀的监控力度不足。项目经历了大约**800KB**的体积漂移（从6.2MB到6.98MB），而针对不同架构（x86_64 vs aarch64）的性能和体积特性，需要有不同的优化和门槛策略。
- **使用场景**：用户（即维护者）非常清晰地认知到项目需要运行在资源受限的机器人硬件（树莓派、Jetson）上的场景，二进制体积是此场景下的关键KPI。
- **满意/不满意**：团队对自动化工具有依赖（CI），但对工具的门槛值设定不够精确感到不满意，并正在积极修正。

### 8. 待处理积压

- **#611 [OPEN] chore(ci): promote binary-size to PR gate at 7.5MB**
  - **积压原因**：PR已经打开6天，无进展。
  - **风险**：随着新Issue #629的提出，PR #611设定的7.5MB门槛可能很快就不符合最新的（aarch64专用的7MB）战略规划。如果不及时更新或处理，可能导致CI策略不一致。**建议维护者快速决策**：是合并#611后立即跟进#629，还是直接修改#611以纳入aarch64的差异化门槛。
  - **链接**：[PR #611](https://github.com/qhkm/zeptoclaw/pull/611)

**项目健康度评估：** 优。虽然专注于纯技术优化（CI流程与性能指标），但方向明确，反馈闭环迅速。无重大外部用户反馈问题，项目处于良性维护状态。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，各位ZeroClaw社区成员，以下是2026年6月7日的项目动态日报。

---

## ZeroClaw 项目动态日报 – 2026-06-07

### 1. 今日速览

过去24小时内，ZeroClaw项目保持极其活跃的状态。**Issue更新达39条，PR更新达50条**，显示出强大的社区参与度和开发推进力。核心开发团队正聚焦于 **v0.8.x** 系列的稳定性和新功能开发，尤其在 **WASM插件系统**、**安全模型加固** 及 **Web仪表盘** 方面有显著进展。尽管有大量代码在流动，但Bug修复的响应速度很快，许多关键问题（S0/S1级）在报告后迅速得到修复并合并。整体项目健康度非常高。

### 2. 版本发布

**无新版本发布。** 多个Tracker Issue显示项目正在积极冲刺 **v0.8.0**、**v0.8.1**、**v0.8.2** 和 **v0.8.3** 里程碑，预示未来几周会有密集的版本迭代。

### 3. 项目进展

今日关闭/合并的PR主要集中在**Bug修复**和**小幅功能增强**上，为大型功能落地扫清障碍。

**已合并/关闭的重要PR (精选):**
- **[#7334] fix(channels/telegram): clamp zero draft update interval** (已合并): 修复了Telegram频道在`draft_update_interval_ms`设置为0时导致消息过度编辑刷新的问题。这是一个快速响应的S2级Bug修复。
    - 链接: [PR #7334](https://github.com/zeroclaw-labs/zeroclaw/pull/7334)
- **[#7297] feat(gateway): per-request agent dispatch for POST /webhook via ?agent=** (已合并): 为Webhook端点增加了按请求选择不同代理（Agent）的能力，提升了Webhook集成的灵活性。
    - 链接: [PR #7297](https://github.com/zeroclaw-labs/zeroclaw/pull/7297)
- **[#7281] fix(policy): stop path guard false-positives on heredoc bodies and non-path tildes** (已合并): 修复了安全策略中路径检查的误报问题，这对于维护命令行工具的安全性至关重要。
    - 链接: [PR #7281](https://github.com/zeroclaw-labs/zeroclaw/pull/7281)

**关键进展:**
- **WASM插件系统成型:** 一系列由`theonlyhennygod`提交的PR（[#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335), [#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337), [#7336](https://github.com/zeroclaw-labs/zeroclaw/pull/7336)）为WASM插件引入了沙箱隔离、资源限制、网络出口控制、工具命名空间和签名模式，标志着ZeroClaw的插件系统正从“可用”迈向“生产级安全”。
- **Web UI功能扩展:** 大型PR [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) 正在开发中，旨在为MCP、Skills、Plugins和Providers提供首屏仪表盘管理标签页。

### 4. 社区热点

今日讨论最活跃的议题主要集中在**安全增强**和**新集成**上。

1.  **OAuth与OIDC认证支持:** `#5601` (评论7) 和 `#7141` (评论4) 是社区对改进认证体验的核心诉求。用户希望摆脱静态API Key，转向更现代的OAuth和OIDC认证方式，特别是针对Ollama Cloud、Kimi等第三方服务。
    - 链接: [Issue #5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)
    - 链接: [Issue #7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)
2.  **工具调用安全与控制:** `#6914` (评论3) 和 `#6915` (评论3) 讨论了对`allowed_tools`的强制执行以及技能（Skill）执行期间的临时工具提权。这反映出社区对Agent安全性的高度关注，希望在不牺牲功能的前提下，实施更细粒度的工具访问控制。
    - 链接: [Issue #6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914)
    - 链接: [Issue #6915](https://github.com/zeroclaw-labs/zeroclaw/issues/6915)

### 5. Bug 与稳定性

今日报告及修复的Bug集中在**渠道、配置和核心运行时**，团队响应迅速。

| 严重程度 | Issue/PR ID | 标题 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **S0 - 数据丢失/安全风险** | [#7252](https://github.com/zeroclaw-labs/zeroclaw/issues/7252) | session/kill can rehydrate killed ACP sessions | **已关闭(已修复)** | 高危Bug，修复快速 |
| **S1 - 关键功能中断** | [#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068) | Telegram channel can receive Codex scratchpad | **已关闭(已修复)** | 影响Telegram用户体验 |
| **S2 - 性能降级** | [#7332](https://github.com/zeroclaw-labs/zeroclaw/issues/7332) | Telegram partial streaming accepts zero draft update interval | **已关闭(已修复)** | 通过PR #7334修复 |
| **S2 - 性能降级** | [#7133](https://github.com/zeroclaw-labs/zeroclaw/issues/7133) | path-policy false-positive on ~ tokens | **已关闭(已修复)** | 通过PR #7281修复 |
| **S2 - 性能降级** | [#7197](https://github.com/zeroclaw-labs/zeroclaw/issues/7197) | Web toolbar loads very slowly on Windows | **已关闭(已修复)** | - |
| **S2 - 性能降级** | [#7151](https://github.com/zeroclaw-labs/zeroclaw/issues/7151) | Observability tool_call telemetry leaks onto chat WebSocket | **已关闭(已修复)** | - |
| **S2 - 性能降级** | [#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) | Web UI "Clear all" only wipes frontend | **已关闭(已修复)** | - |

### 6. 功能请求与路线图信号

今日的功能请求和讨论显示出几个明确的路线图信号：

- **WASM插件生态爆发:** 多个PR（[#7325](https://github.com/zeroclaw-labs/zeroclaw/pull/7325), [#7326](https://github.com/zeroclaw-labs/zeroclaw/pull/7326), [#7327](https://github.com/zeroclaw-labs/zeroclaw/pull/7327), [#7328](https://github.com/zeroclaw-labs/zeroclaw/pull/7328), [#7331](https://github.com/zeroclaw-labs/zeroclaw/pull/7331), [#7333](https://github.com/zeroclaw-labs/zeroclaw/pull/7333)）提交了新的WASM插件，涵盖图像生成、音乐生成、地理编码、语法检查、工作流触发和插件远程注册表。这强烈表明 **v0.8.x 系列将重点打造一个丰富的、自托管的插件生态系统**。
- **开发者体验与配置管理:** Issue [#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184)（将翻译文件移至子模块）和PR [#7298](https://github.com/zeroclaw-labs/zeroclaw/pull/7298)（Config标签页UI与zerocode统一）表明项目在持续关注和改进开发者和高级用户的配置、构建和i18n体验。
- **集成深度与广度:** PR [#7256](https://github.com/zeroclaw-labs/zeroclaw/pull/7256) 对飞书（Feishu）渠道进行了大规模加固，增加了反应、草稿流、用户会话等高级功能。这表明ZeroClaw不仅追求集成数量，更注重每个集成的深度和质量。

**可能纳入下一版本的功能:**
- **WASM插件沙箱与远程注册表** (#7335, #7333): 几乎可以肯定将作为v0.8.2的核心特性。
- **MCP仪表盘** (#7229, #7320): v0.8.3里程碑的核心，旨在简化MCP服务管理。
- **OIDC认证** (#7141): 作为安全架构的一部分，预计会在v0.9.0路线图中。
- **多套件订阅方式OAuth登录** (#5601): 用户呼声高，但尚无直接对应的PR，可能优先级低于OIDC。

### 7. 用户反馈摘要

- **安全沙箱获得认可:** 用户`singlerider`和`alex-nax`连续提交多个安全和策略相关的Issue和PR，表明高级用户对ZeroClaw的灵活性（如技能隔离、工具白名单）很满意，但同时也期望更强的安全边界。
- **渠道体验反馈积极:** 用户`kanmars`为飞书渠道提交了大型PR（#7256），这通常意味着该用户（或背后的组织）是活跃的飞书重度用户。他们对现有集成“能用”，但期望“好用”，贡献代码是最高级别的认可。
- **Windows用户体验问题:** 用户`NiuBlibing`报告了多个与Web UI和Windows上工具栏加载的问题（#7197），这表明Windows用户群体在增长，但平台体验仍有优化空间。

### 8. 待处理积压

以下是一些长期开放但重要的Issue，提醒维护者关注：

- **[#5601] [Feature]: Add subscription-native OAuth support...** (创建于2026-04-10): 作为最早的认证增强请求之一，已标记为`blocked`，社区反馈高。其解决方案可能与#7141 OIDC支持存在重叠，建议评估是否可被OIDC方案覆盖。
    - 链接: [Issue #5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)
- **[#5775] feat(skills): per-skill security permissions** (创建于2026-04-15): 与已经解决的#6915（技能工具提权）紧密相关。`#6915`解决了工具的问题，但脚本和命令的隔离仍悬而未决。这是一个重要的安全功能，建议评估进展。
    - 链接: [Issue #5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775)
- **[#5908] [Feature]: GitHub Actions CI / CD Container Builds and Releases for Debian** (创建于2026-04-19): 持续集成/交付的容器化是一个基础设施问题，虽然已标记为`blocked`，但对降低用户部署门槛至关重要。建议评估阻塞原因。
    - 链接: [Issue #5908](https://github.com/zeroclaw-labs/zeroclaw/issues/5908)

---
**日报生成时间**: 2026-06-07
**数据来源**: [ZeroClaw GitHub Repository](https://github.com/zeroclaw-labs/zeroclaw)

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*