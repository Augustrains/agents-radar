# OpenClaw 生态日报 2026-08-16

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-16 00:31 UTC

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

好的，这是 2026-08-16 的 OpenClaw 项目动态日报。

---

### OpenClaw 项目动态日报 (2026-08-16)

#### 1. 今日速览

OpenClaw 项目今日活跃度极高，过去24小时内产生了500条Issue和500条PR更新，显示出庞大的社区使用量和强烈的反馈意愿。尽管新版本发布节奏平稳（今日发布1个Beta版），但Issue和PR的积压数量巨大，且大量高优先级（P1）问题处于“待维护者评审”或“等待作者回复”状态，这暗示维护团队的响应速度可能成为社区发展的瓶颈。值得注意的是，今日涌现多个关于**消息丢失**和**会话状态管理**的回归性Bug报告，提示近期更新可能在核心稳定性方面引入了新问题。

#### 2. 版本发布

- **v2026.8.1-beta.2** ([发布链接](https://github.com/openclaw/openclaw/releases))
    - **核心亮点**:
        - **Secret egress host binding:** 引入新的安全机制，将共享存储的密钥（Secret）绑定到精确的HTTPS目标主机。这将使未绑定的哨兵替换在明文出口前即失败关闭，从而增强整体安全性。
        - **GPT-5.6 Ultra 支持:** 新版本将支持 GPT-5.6 Ultra 模型，并可能引入相关的运行时切换机制。
    - **影响与注意**: 该版本为Beta版，主要引入安全增强和新模型支持。由于涉及安全边界的变更，建议用户在升级后重点测试密钥管理和模型调用相关功能。

#### 3. 项目进展

今日共有54个PR被合并或关闭。从关闭的PR来看，项目在**安全策略**和**Web UI体验**方面有显著推进：

- **安全策略落地**: PR `#116489` (feat(security): require acknowledgement for install policy warnings) 和 `#120900` (feat(ui): review install policy warnings) 被合并。这两个PR共同构建了“安装策略警告”功能，允许管理员在安装可疑插件或技能前进行审查和确认，标志着OpenClaw在供应链安全方面迈出了实质性一步。
- **UI 健壮性修复**: PR `#124264` (fix(ui): reject blank required strings in Control UI update readers) 被合并。该PR修复了Control UI在更新配置时可能接受空字符串导致错误的问题，提升了配置操作的安全性。

整体来看，项目在安全、UI易用性方面持续迭代，但核心运行时稳定性的修复进展相对缓慢。

#### 4. 社区热点

今日讨论热度最高的Issues集中在**消息丢失**和**会话状态异常**这两个老大难问题上：

- **[Issue #121058] (关闭) [P1] Silent reply failures still recurring after #116277 closed — no queued reply payload** ([链接](https://github.com/openclaw/openclaw/issues/121058)): 该问题以96条评论成为今日最热Issue。尽管被标记为关闭，但用户 `sloptop-the-terrible` 明确指出问题在 #116277 修复后依然存在，监控系统持续记录到失败。这揭示了**修复无效**的严重情况，可能导致社区对项目修复能力的信任危机。
- **[Issue #116201] [P1] Realtime voice work can retain unbounded provider and consult state** ([链接](https://github.com/openclaw/openclaw/issues/116201)): 该问题以66条评论位居第二。用户 `vincentkoc` 指出实时语音会话存在资源未绑定、状态无限增长的问题，在慢速或不稳定的provider环境下可能导致内存泄漏或状态错乱。
- **共性分析**: 这两大热点背后反映的是用户对**核心通信链路可靠性**的极高要求。消息丢失和状态错乱直接影响到智能体的可用性，是阻碍其投入生产环境的关键障碍。社区对此类问题的反馈非常激烈。

#### 5. Bug 与稳定性

今日报告的Bug数量众多，按严重程度排列如下：

- **P1 严重问题**:
    - **消息丢失/重复**: 多个Issue指向此问题，如 [#121058](https://github.com/openclaw/openclaw/issues/121058) (静默回复失败), [#90944](https://github.com/openclaw/openclaw/issues/90944) (sessions_yield 恢复回复未送达), [#80498](https://github.com/openclaw/openclaw/issues/80498) (子代理完成通知过早或重复)。这些问题均无明确的已关联修复PR。
    - **会话状态异常**: [#86684](https://github.com/openclaw/openclaw/issues/86684) 指出子代理唤醒时错误触发父会话压缩，可能导致数据丢失。该问题有`linked-pr-open`标签，但尚无具体PR被合并。
    - **性能回归**: [#119087](https://github.com/openclaw/openclaw/issues/119087) 报告网关冷启动时间在1 vCPU环境下回退2.5倍，属于严重影响轻量级部署的回归问题。
    - **更新/迁移故障**: [#123073](https://github.com/openclaw/openclaw/issues/123073) 指出dev频道的更新因依赖协议不匹配而失败，阻碍了开发者测试最新代码。
    - **配置覆盖/数据丢失**: [#78493](https://github.com/openclaw/openclaw/issues/78493) 报告了sudo更新导致文件所有权混乱，进而引发配置被覆盖的风险。

- **P2 中等问题**:
    - 主要集中在**上下文窗口膨胀** ([#67419](https://github.com/openclaw/openclaw/issues/67419))、**SQLite数据库无限增长** ([#114612](https://github.com/openclaw/openclaw/issues/114612))、**特定渠道（Feishu, Telegram, Matrix）的功能缺陷** ([#77685](https://github.com/openclaw/openclaw/issues/77685), [#120735](https://github.com/openclaw/openclaw/issues/120735), [#122625](https://github.com/openclaw/openclaw/issues/122625))。
    - 这些问题中有不少被标记为`clawsweeper-recovery-stuck`，表明自动化机器人也无法推进，可能需要人工介入。

**结论**: 今日Bug报告呈现出“多点开花”的局面，核心问题集中在消息投递和会话状态管理上，且许多问题处于僵局状态，缺乏有效的修复PR跟进。

#### 6. 功能请求与路线图信号

尽管Bug修复压力巨大，社区仍提出了新的功能需求，预示着未来的发展方向：

- **安全性增强**: Issue [#7707](https://github.com/openclaw/openclaw/issues/7707) 提议“Memory Trust Tagging by Source”，即为内存条目添加来源信任标签，以防止通过网页或第三方技能进行的提示注入攻击。这与官方近期在安全方面的动作（如secret binding、install policy warnings）方向一致，**极有可能被纳入后续版本的规划中**。
- **开发者体验**: Issue [#6599](https://github.com/openclaw/openclaw/issues/6599) 提议增加 `/models test-fallback` 命令，用于主动测试模型回退链是否配置正确，避免在真实故障时才暴露问题。这是一个高价值的运维工具需求。
- **配置灵活性**: Issue [#45758](https://github.com/openclaw/openclaw/issues/45758) 提议支持 YAML 配置文件格式，以满足更广泛用户的习惯。
- **自治行为控制**: Issue [#45771](https://github.com/openclaw/openclaw/issues/45771) 提议内置“节奏感知速率限制”，防止自主Agent循环耗尽API配额。这与近期对子代理和自主行为的关注相符。

#### 7. 用户反馈摘要

- **核心痛点**: “消息又丢了”和“状态又乱了”是用户反馈中最刺耳的声音。多个高热度Issue直指核心通信问题，且存在修复不彻底（如 #121058）、修复引入新问题（如 #86684）的情况，这极大地消耗了用户的耐心。
- **升级顾虑**: 多个Issue（如 #83337, #94939）表明用户对升级充满顾虑。插件与核心版本漂移、状态数据迁移失败等问题，使得“升级”变成了一项高风险操作。
- **部署环境多样性挑战**: 从Windows的`node.exe`进程残留（#74378）、macOS的`launchd`配置错误（#90711）到低配容器的性能回退（#119087），反映出OpenClaw在不同部署环境下的兼容性和性能表现差异较大，是阻碍其被更广泛采用的门槛。

#### 8. 待处理积压

以下问题和PR长期未获有效推进，建议维护者重点关注：

- **长期未决的P1 Issue**:
    - [Issue #25592](https://github.com/openclaw/openclaw/issues/25592): 工具调用之间的文本泄漏到消息频道。这是一个严重的UX和隐私问题，自2月以来一直开放，状态为`needs-product-decision`。
    - [Issue #91009](https://github.com/openclaw/openclaw/issues/91009): Codex PreToolUse hook导致CPU占用和网关RPC停滞。此问题严重影响了Codex集成的稳定性，且处于`recovery-stuck`状态。
    - [Issue #43374](https://github.com/openclaw/openclaw/issues/43374): 多Agent并发时所有LLM API调用同时超时。这听起来像一个内部连接池或事件循环阻塞问题，影响核心功能。

- **长时间未合并的关键PR**:
    - [PR #85183](https://github.com/openclaw/openclaw/pull/85183): 旨在保留用户配置意图的更新机制。自5月22日创建以来，一直处于`waiting on author`状态，对于升级体验至关重要，但进展缓慢。
    - [PR #86540](https://github.com/openclaw/openclaw/pull/86540): 修复锁存后子代理交付问题。该PR直接关联到多个“消息丢失”类Issue，但3个月过去仍未合并。

---

## 横向生态对比

好的，这是基于您提供的 2026-08-16 各开源项目社区动态生成的横向对比分析报告。

---

### 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**高速发展与深度分化**的十字路口。一方面，以 OpenClaw 为代表的头部项目社区规模庞大，但已显现出**核心稳定性成为瓶颈**的迹象，大量关于消息丢失、状态错乱的 P1 级 Issue 涌入，对维护团队的响应和修复能力构成严峻考验。另一方面，一批新兴项目（如 NanoBot、IronClaw、Moltis）正处于**活跃的功能迭代期**，在稳定性、性能优化和特定平台集成上表现抢眼，试图通过差异化定位（如轻量级、高性能、垂直场景）在 OpenClaw 的阴影下寻找突破口。社区对**会话持久性、跨平台互操作性、成本控制和部署灵活性**的需求已成为普遍共识，是推动下一阶段技术演进的核心动力。

### 2. 各项目活跃度对比

| 项目 | Issues 更新 | PRs 更新 | Releases | 一次性健康度评估 | 活跃阶段 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500+ | 500+ | 1 (Beta) | **⚠️ 危机**：社区活跃度极高，但严重 Bug 堆积、修复无效、积压严重，信任度面临挑战。 | 生态成熟，但稳定性危机 |
| **NanoBot** | 2 (1新) | 16 (7合并) | 0 | **✅ 健康**：修复与功能并进，PR 质量高，有明确的重构方向，在稳定中扩展外围。 | 稳定核心 + 功能扩张 |
| **Hermes Agent** | 50 (9关闭) | 50 (3关闭) | 0 | **⚠️ 存在短板**：社区活跃，桌面端是迭代重点，但安全边界与平台兼容性问题（尤以Windows为甚）持续暴露。 | 快速迭代，平台兼容性待解 |
| **PicoClaw** | 0 | 2 | 0 | **🟡 停滞风险**：活跃度低，两个关键 PR（WhatsApp修复、API成本优化）被标记为stale，维护响应迟缓。 | 维护节奏放缓 |
| **NanoClaw** | 0 | 22 (3关闭) | 0 | **✅ 健康**：核心团队高活跃，快速开发频道适配（Telegram）、权限、跨会话上下文等，工程化纪律好。 | 快速功能迭代 |
| **NullClaw** | 1 (新) | 1 (新) | 0 | **✅ 健康**：小步快跑，提交质量扎实，但社区热度低。 | 小步快跑 |
| **IronClaw** | 27 (21关闭) | 12 (5合并) | 0 | **✅ 健康**：核心重构与性能优化收尾，合并效率高，有完善的审查后追踪机制。 | 核心重构与优化 |
| **LobsterAI** | 18 (多为stale关闭) | 6 | 0 | **⚠️ 趋冷**：活跃度偏低，长期问题（付费服务稳定性、记忆缺失）未解决，维护节奏放缓。 | 维护节奏放缓 |
| **TinyClaw** | 0 | 0 | 0 | N/A - 无活动 | 不活跃/新项目 |
| **Moltis** | 0 | 6 (3合并) | 0 | **✅ 健康**：由核心成员稳定推进，合并效率高，聚焦外部集成（Coder、Slack）和架构优化（OpenAI API路由）。 | 功能累积冲刺 |
| **CoPaw (QwenPaw)** | 9 | 11 | 0 | **✅ 高响应**：Bug 报告与修复同日跟进，反馈回路通畅，但 PR 审查（11:0 待合并）可能成为瓶颈。 | 高响应迭代，审查有瓶颈 |
| **ZeroClaw** | 50 | 50 | 0 | **✅ 结构性强**：高度关注 RFC 与架构讨论，Anthropic 回退支持已落地，但决策队列是主要风险，影响长期进展。 | 密集设计决策与代码审查 |

### 3. OpenClaw 在生态中的定位

OpenClaw 是生态中当之无愧的**核心参照与“超级应用”**，拥有远超其他项目的社区规模和用户基础（单日500+ Issue/PR 即为例证）。其优势在于建立了庞大的**插件、技能和渠道生态**，并持续引入安全增强（如 Secret egress binding、安装策略警告），体现出平台级的安全视野。然而，其技术路线也因**包罗万象**而变得复杂，导致**核心运行时（消息传递、会话管理）的稳定性成为最突出的短板**。与 IronClaw 通过“unbound-turns”和写放大削减进行底层性能重构不同，OpenClaw 的修复更像是“打地鼠”，许多高热度 Issue（如消息丢失）存在修复不彻底甚至引入新回归的情况。这使得它在面对追求“开箱即用、极致稳定”的开发者时，可能会被如 NanoBot（更专注的 WebUI 体验）或 IronClaw（更强的工程治理）等更“锋利”的竞品分流。

### 4. 共同关注的技术方向

- **会话持久性与状态管理**：
    - **涉及项目**：OpenClaw、NanoBot、Hermes Agent、LobsterAI、NullClaw。
    - **具体诉求**：核心痛点是消息丢失、会话状态错乱和跨会话/重启后的记忆缺失。例如，OpenClaw 的多个 P1 Bug、NanoBot 的 Consolidation游标Bug、Hermes Agent 的 "Persistent Session Memory" 长寿命 Issue，以及 LobsterAI 的 "Agent 记忆体系" 产品建议，都指向同一个方向：**让 Agent 会话在复杂、长时间运行和跨平台场景下保持绝对可靠和可追溯**。

- **模型/Provider 接入的灵活性与互操作性**：
    - **涉及项目**：ZeroClaw、Moltis、CoPaw、Hermes Agent。
    - **具体诉求**：社区既需要接入更多 Provider（如 CoPaw 对 OpenAI Responses API、Moltis 对 OpenAI 推理工具的路由、ZeroClaw 对 Anthropic 的深度支持），也强烈希望自身能被标准客户端接入。ZeroClaw 呼声最高的 RFC（#8603）正是为了兼容 OpenAI Chat Completions 协议，而 Moltis 新增 OrcaRouter 网关提供商也体现了这一趋势。**标准化、可插拔的 Provider 层**是共同目标。

- **成本优化与性能**：
    - **涉及项目**：PicoClaw、NullClaw、IronClaw、CoPaw。
    - **具体诉求**：用户对 API 成本和上下文窗口膨胀问题非常敏感。PicoClaw 的前缀缓存优化、NullClaw 的工具输出压缩、IronClaw 的写放大削减（史诗级 #7591）以及 CoPaw 的 WebUI 虚拟滚动请求，都明确指向 **token 消耗、存储开销和长任务性能**是决定生产级体验的关键因素。

### 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构/路线差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全栈式个人 AI 助手平台 | 追求功能全面的个人开发者、研究者 | 单体应用，拥有最庞大的插件/技能生态；技术栈广泛，但架构复杂度引发稳定性挑战。 |
| **NanoBot** | 精致、稳定的 Web 端 AI 助手 | 注重交互体验和团队协作的开发者 | 高度聚焦 WebUI 渲染和交互（侧边栏、拖拽、会话协作），追求端到端的用户体验一致性。 |
| **Hermes Agent** | 跨平台桌面优先的 AI 助手 | 重度桌面用户（尤其 Windows/macOS） | 以桌面客户端为核心阵地，积极扩展本地化、浏览器预览等原生体验，但在平台兼容性上仍需打磨。 |
| **NanoClaw** | 高度模块化的频道机器人网关 | 需要在 Telegram、Discord 等多频道部署 bot 的开发/运维者 | 设计上以 Channel Adapter 为核心，通过自注册机制实现高度解耦和热启动，平台迁移方向明确。 |
| **IronClaw** | 高性能、重工程治理的 Agent 运行时 | 对性能、可靠性和代码质量有严苛要求的技术团队 | 架构演进激进（如 unbound-turns、符号级依赖边界），追求极致性能和代码内省，工程文化浓厚。 |
| **CoPaw (QwenPaw)** | 面向特定云服务/模型生态优化的助手 | 深度使用特定云生态（如 Volcengine Ark）的开发者 | 针对特定 Provider 的 API 特性进行极其细致的适配和修复（如 `view_video` 结果传递），优化路径更垂直。 |
| **ZeroClaw** | 社区驱动、设计审慎的 Agent 框架 | 关注架构演进、希望参与决策的技术型用户 | 通过 RFC 机制驱动核心架构演进（会话所有权、附件架构），节奏稳健，注重设计一致性和长期健壮性。 |
| **Moltis** | 面向任务的集成型 Agent | 工作流自动化场景的开发者（Slack、Coder等） | 聚焦于外部工具链的深度集成（沙箱、协作平台、数据连接器），并持续优化模型 API 的路由逻辑。 |
| **LobsterAI** | OpenClaw 的国产化/定制发行版 | 需要本地化服务（如网易模型）或特定功能的开发者 | 跟随 OpenClaw 内核，但存在配置、模型路由等服务端的深度定制，其社区反馈也反映了国内用户的独特需求。 |

### 6. 社区热度与成熟度

- **第一梯队（海量社区，快速迭代，稳定性危机）**：**OpenClaw**。社区规模一骑绝尘，但维护资源相对紧缺，导致大量高价值 PR/Issue 积压，正处于“消耗社区红利”的危险阶段。

- **第二梯队（活跃社区，同步迭代）**：**Hermes Agent**、**NanoClaw**、**IronClaw**、**CoPaw**。这些项目社区活跃度高，开发迭代快，且各有侧重（桌面端、频道、架构、响应速度），处于功能快速累积期，部分已展现出不俗的工程化能力。

- **第三梯队（聚焦质量或特定领域）**：**NanoBot**、**Moltis**、**ZeroClaw**。社区规模中等，但非常健康。NanoBot 在稳定核心并小心扩展；Moltis 由核心团队高效推进；ZeroClaw 则致力于社群驱动的顶层设计，质量意识强于速度。

- **第四梯队（蛰伏/低活跃）**：**PicoClaw**、**LobsterAI**、**NullClaw**、**TinyClaw**、**ZeptoClaw**。这些项目活跃度低，或处于维护停滞期（PicoClaw、LobsterAI），或因尚在早期而声量不大（NullClaw、TinyClaw、ZeptoClaw）。

### 7. 值得关注的趋势信号

1.  **“稳定性”成为差异化护城河**：OpenClaw 的案例表明，当功能堆叠到达一定程度，**消息可靠性、会话一致性等“隐形”能力将成为用户选择的关键**。IronClaw 的重构、NanoBot 的“高响应修复率”都在积极拥抱这一趋势，这为开发者提供了绝佳的切入点——能在核心运行时层面提供极致稳定性的项目将极具价值。

2.  **从“工具”到“协作平台”的演进**：NanoBot 的会话协作（Mentions）、Hermes Agent 的 AI 辅助会话分组、IronClaw 的 Trajectory benchmark，这些高频需求预示着**AI 助手正从单点工具转向支持多人协作、可评估、可回溯的“团队级”基础设施**。

3.  **开发者体验（DX）的权重提升**：ZeroClaw 的 AI 辅助 PR 审查提议、IronClaw 对 CI 竞态（ETXTBSY）的修复、OpenClaw 的 `/models test-fallback` 请求，均表明**社区开始要求工具链本身具备更高的智能化与健壮性**。这不仅是功能需求，更是对项目成熟度的评判标准。

4.  **特定场景的深度集成是突破口**：在通用助手红海竞争下，Moltis 在远端沙箱（Coder）、CoPaw 在特定云厂商（Volcengine Ark）的深耕，以及 NanoClaw 对 Telegram 生态的重注，展示了**通过垂直场景绑定来构建用户粘性和不可替代性**是一条清晰的发展路径。

5.  **下一代交互形态的预研**：OpenClaw 对实时语音状态的关注和 ZeroClaw 对 Gemini Live 语音通道的 RFC，预示着**从纯文本/文件交互向实时多模态交互（尤其是语音）的转移**是生态下一步关注的焦点，尽管距离成熟落地尚有距离。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-16

## 1. 今日速览

NanoBot 项目在过去24小时内保持中等偏上的活跃度。共产生2条 Issue 更新（1 新开、1 关闭）及 16 条 PR 更新（9 条待合并、7 条已合并/关闭）。虽无新版本发布，但多个涉及 WebUI 交互、会话数据一致性及文件状态生命周期的 Bug 修复已完成合并，项目整体稳定性正在持续增强。值得关注的是，三条大功能 PR（侧边会话、拖拽整理、会话协作）均带 `conflict` 标签，预示着 WebUI 布局重构方向上的并行工作存在一定的整合挑战。

## 2. 版本发布

本日无新版本发布。

---

## 3. 项目进展

本日共 **7 条 PR 被合并/关闭**，主要覆盖以下方面：

### ✨ 新功能（2项）
| PR | 内容 | 状态 |
|---|---|---|
| [#5328](https://github.com/HKUDS/nanobot/pull/5328) | **新增 OrcaRouter 网关提供商** | 已合并 |
| [#5399](https://github.com/HKUDS/nanobot/pull/5399) | **WebUI 模型预设显示名称优化**：区分显示标签与稳定命令名，支持编辑时显示稳定名称，并完成多语言本地化 | 已合并 |

### 🐛 Bug 修复（5项）
| PR | 内容 | 优先级 |
|---|---|---|
| [#5371](https://github.com/HKUDS/nanobot/pull/5371) | 修复 WebUI 在 Agent 回合运行中显示复制/分叉操作的冲突信号问题 | p2 |
| [#5369](https://github.com/HKUDS/nanobot/pull/5369) | 修复插件技能目录缓存未在包变更后重新验证的安全问题 | p2（security） |
| [#5370](https://github.com/HKUDS/nanobot/pull/5370) | 限制 FileStateStore 按会话的文件状态生命周期，修复高基数会话下无界增长问题 | p2 |
| [#5376](https://github.com/HKUDS/nanobot/pull/5376) | 修复 Cron 调度器在持久化失败时静默终止的严重问题 | p2 |
| [#5397](https://github.com/HKUDS/nanobot/pull/5397) | 修复 WebUI 侧边栏范围选择、运行计时归属及回合身份保持 | p2 |

> 此外，[#5369](https://github.com/HKUDS/nanobot/pull/5369) 还修复了一个安全问题：插件包替换后旧缓存目录仍可被读取，涉及权限绕过风险。

**整体判断**：项目本日在稳定性修复上投入显著，尤其对会话数据一致性、文件状态管理和调度器健壮性进行了加固。同时新网关提供商（OrcaRouter）的加入扩展了多模型接入能力。项目正处于“稳定核心 + 扩展外围”的健康发展阶段。

---

## 4. 社区热点

本日暂无单条议题引发大量评论的“爆点”。综合关注度较高的条目如下：

| 条目 | 类型 | 关注原因 |
|---|---|---|
| [#5377](https://github.com/HKUDS/nanobot/issues/5377) | Bug（开放） | `Consolidator.archive()` 截断输入但会话游标越过整个批次，造成消息丢失。已有配套修复 PR，属当前最热门的活跃问题 |
| [#5358](https://github.com/HKUDS/nanobot/pull/5358) | 功能 PR | 会话协作（mentions）——扩展 composer 提及选择器以引用对等会话，是 WebUI 多人协作场景的前沿探索 |
| [#5291](https://github.com/HKUDS/nanobot/pull/5291) | 功能 PR | 持久化子代理（subagent）完整会话记录——填补调试追溯空白，回应了用户对子代理过程透明性的需求 |

**背后诉求分析**：社区对会话完整性和过程透明性需求明确升温——无论是 Issue #5377 中数据截断的报错，还是 PR #5291 对子代理全过程记录的诉求，都指向“数据不丢失、过程可追溯”这一核心期望。

---

## 5. Bug 与稳定性

### 🔴 高严重度

| Issue | 描述 | 状态 |
|---|---|---|
| [#5377](https://github.com/HKUDS/nanobot/issues/5377) | **Consolidation 截断存档输入但游标越过完整批次**：`Consolidator.archive()` 将格式化对话截断到模型输入 token 预算，但调用方仍将 `Session.last_consolidated` 推进至整个原始消息批次之后。超出截断部分的消息后缀将永久丢失 | ✅ 已有修复 PR [#5379](https://github.com/HKUDS/nanobot/pull/5379)，待合并 |

### 🟡 中严重度（已有修复，已合并）

| 类别 | 描述 | 修复 PR |
|---|---|---|
| 调度器 | Cron 持久化失败（磁盘满/权限变更/文件锁定）时调度器静默死亡 | [#5376](https://github.com/HKUDS/nanobot/pull/5376) ✅ |
| 会话状态 | 后台任务保存可能覆盖 `/new` 后的新会话 | [#5271](https://github.com/HKUDS/nanobot/pull/5271)（待合并） |
| 文件状态 | FileStateStore 无界增长 + 会话生命周期后状态残留 | [#5370](https://github.com/HKUDS/nanobot/pull/5370) ✅ |
| 插件安全 | 缓存技能目录在包替换后仍在受限项目中可读 | [#5369](https://github.com/HKUDS/nanobot/pull/5369) ✅ |
| WebUI | Agent 运行中显示复制/分叉操作的冲突完成信号 | [#5371](https://github.com/HKUDS/nanobot/pull/5371) ✅ |

### 🟢 低严重度

- [#5368](https://github.com/HKUDS/nanobot/issues/5368) WebUI 复制/分叉操作在回合运行中显示 —— 已关闭，由 [#5371](https://github.com/HKUDS/nanobot/pull/5371) 修复

---

## 6. 功能请求与路线图信号

### 已进入 PR 阶段的功能

| 功能 | PR | 信号强度 |
|---|---|---|
| **会话协作/提及（Mentions）** —— 为持久化会话分配服务端 `@name`，支持提及同组会话 | [#5358](https://github.com/HKUDS/nanobot/pull/5358) | 中等（已开放 4 天，带冲突标记） |
| **侧边临时会话** —— `/side` 命令，支持标签切换和并行发送 | [#5364](https://github.com/HKUDS/nanobot/pull/5364) | 中等（带冲突标记） |
| **拖拽式会话整理** —— 会话排序和分组 | [#5389](https://github.com/HKUDS/nanobot/pull/5389) | 中等（带冲突标记） |
| **模型预设统一命名** —— 设置唯一规范名称并支持重命名 | [#5400](https://github.com/HKUDS/nanobot/pull/5400) | 中等（新开） |
| **DashScope 原生协议** —— 解锁原生思维链等完整参数面 | [#5398](https://github.com/HKUDS/nanobot/pull/5398) | 较高（网关提供商持续扩展） |
| **持久化子代理会话记录** —— 完整保存推理过程与会话内容 | [#5291](https://github.com/HKUDS/nanobot/pull/5291) | 较高（已开放 9 天，时间较长） |
| **WebUI 变更重连安全** —— 断线重连后自动重试挂起变更 | [#5401](https://github.com/HKUDS/nanobot/pull/5401) | 中等（新开） |

### 预判

WebUI 交互体验是当前功能开发的最大热点。三条带 `conflict` 标签的 PR（#5358、#5364、#5389）表明会话管理布局正在经历较大的结构性重构——三者涉及同一模块的并行开发，合并顺序将直接影响最终 API 形态，建议维护者优先协调合并时序，避免返工。

---

## 7. 用户反馈摘要

本日无新增评论（Issue #5377 有 2 条评论但数据中未展示内容）。从提交的 PR 和 Issue 描述中可提取以下用户的隐含反馈信号：

| 反馈来源 | 用户诉求/痛点 |
|---|---|
| [#5377](https://github.com/HKUDS/nanobot/issues/5377) | 用户明确指出：consolidation 过程“截断了输入但游标越过完整批次”，导致部分消息被静默丢弃。**用户期望**：要么完整保留所有消息，要么对截断部分做明确标注 |
| [#5291](https://github.com/HKUDS/nanobot/pull/5291) | 用户（贡献者）指出子代理运行结束后“只有最终结果渲染公告，完整会话凭空消失”，**期望**：审查子代理全部工具调用、结果和推理过程 |
| [#5271](https://github.com/HKUDS/nanobot/pull/5271) | 用户遭遇后台任务保存覆盖 `/new` 新会话的问题，**期望**：生命周期替换时旧后台工作被正确废弃 |
| [#5376](https://github.com/HKUDS/nanobot/pull/5376) | 用户发现 Cron 调度器在持久化失败时“永久死亡”且无提示，**期望**：单次错误不应影响调度器存活 |
| [#5399](https://github.com/HKUDS/nanobot/pull/5399) | 用户反馈模型预设编辑时“显示名称”与“命令名称”混淆的体验问题 |

**整体满意度**：社区贡献者对问题的定位和修复都比较精准，PR 质量整体较高（多数带测试覆盖），说明项目对贡献者的开发体验维护得较好。

---

## 8. 待处理积压

### ⚠️ 待合并的高优修复

| 条目 | 创建时间 | 等待时长 | 说明 |
|---|---|---|---|
| [#5271](https://github.com/HKUDS/nanobot/pull/5271) `p0, conflict` | 08-06 | **10 天** | 阻止过期后台任务覆盖会话数据 —— **P0 级问题，已等待 10 天**。涉及 `/new` 后数据被覆盖的风险，建议优先安排审查合并 |
| [#5379](https://github.com/HKUDS/nanobot/pull/5379) | 08-13 | 3 天 | 修复 Issue #5377（consolidation 截断丢失消息），目前是项目最活跃的 bug 修复 PR |

### 📋 长期待关注

| 条目 | 创建时间 | 等待时长 | 说明 |
|---|---|---|---|
| [#5291](https://github.com/HKUDS/nanobot/pull/5291) | 08-07 | 9 天 | 子代理会话持久化 —— 功能完整，但已等待较久，建议维护者确认是否纳入下个里程碑 |
| [#5364](https://github.com/HKUDS/nanobot/pull/5364) | 08-13 | 3 天 | 侧边临时会话 —— 与 #5389、#5358 存在界面布局冲突，建议三者在同一版本窗口中协调合并 |

### 🔍 需关注的风险信号

- **三条 WebUI 功能 PR 相互冲突**（#5358、#5364、#5389），均带 `conflict` 标签。建议维护者尽快确立会话管理模块的架构方向，避免并行开发导致的返工损耗。
- **P0 级 PR #5271 等待 10 天**可能暗示核心模块的审查带宽存在瓶颈。

---

*本报告基于 GitHub 公开数据生成，所有链接指向 HKUDS/nanobot 仓库相应条目。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-16

## 1. 今日速览

过去24小时项目保持中等偏高活跃度：共处理 50 条 Issues（41 条活跃，9 条关闭）和 50 条 PR（47 条待合并，3 条已关闭/合并），无新版本发布。值得关注的是，稳定性修复占据主导——多个 Windows 平台更新/自锁 Bug（#83569、#87331）已关闭或进入讨论尾声，但同属风险密集区的新问题仍在持续暴露，尤其是 CLI 审批面板不渲染（#87183）和桌面端二次启动杀死后端（#87295）等 P1/P2 缺陷。与此同时，桌面端功能开发显著加速——今日新增了 URL 工具栏（#87332）、土耳其语本地化（#87305）和"运行中≠忙碌"状态修复（#87330）等多项 PR，显示桌面端是当前迭代重点。压缩策略方面也有值得关注的开源贡献（#87326 提出 lean tail mode 并附带评测数据）。整体项目健康度中等：社区贡献活跃，但安全边界与平台兼容性问题仍是持续性短板。

## 2. 版本发布

过去 24 小时无新版本发布。当前最新版本为 v0.20.1（社区 Issues 中多次提及，如 #87329、#87200）。

## 3. 项目进展

今日无 PR 合并，3 条 PR 被关闭/合并，其中值得关注的是：

- **[#87317] feat(desktop): Skills tab hub browser + full-skill detail pane** — 将技能管理整合到统一界面，新增 Hub 浏览与详情面板，移除 Browse Hub 独立标签页。该 PR 已被关闭，具体是否合并至 main 需要进一步确认，但方向显示桌面端技能管理体验在持续迭代，与 #66616 的 skills-index 健康度问题形成呼应。

待合并 PR 中值得关注的进展方向：

- **[#87333] fix(computer-use): placeholder-id targeting + macOS zero-display diagnosis** — 修复模型发出的 `pid=0/window_id=0` 占位符导致应用级截屏失效的问题，并添加 macOS 零显示器捕获诊断逻辑。
- **[#87326] feat(compression): lean tail mode + compaction recall eval harness** — 提出一项压缩策略优化：`tail_mode="lean"` 在保留 token 缩减至 0.30x 的同时，平均召回率反而提升了 22.5 个百分点（68.3% @ 49K vs 45.8% @ 162K，基于四条 50 万 token 真实会话），并首次引入了永久性的压缩召回评估框架（`evals/compaction/`）。
- **[#85318] fix(webhook): bind signatures to explicit provider schemes** — 将 webhook 签名验证从"根据请求头推断"改为"按显式 provider scheme 绑定"的验证器注册表，关闭 #47451、#80327 两个安全 Issue。
- **[#77008] fix(security): write BWS disk cache encrypted-only, migrate legacy plaintext** — 修复 Bitwarden Secrets Manager 磁盘缓存明文存储所有秘密值的问题，改为仅加密写入 AES-GCM 格式并自动迁移存量数据。

## 4. 社区热点

- **[#78647] Large-file decomposition: 20/20 done**（79 评论，已关闭）— 大型 god-file 分片史诗任务宣告 20/20 全部完成。社区对该项重构方针（"all god files are sharded, never reverted"）讨论充分，0 个 👍 但持续四周的高评论量显示这是一次重大架构变更。
- **[#66616] Skills index is stale or degraded**（37 评论，开放中）— 自动巡检发现技能索引已 29.8 小时未更新（阈值 26h），状态降级为 degraded。此问题持续一个月仍未解决，且直接关系到技能功能可用性，社区耐心正在消耗。
- **[#83683] Desktop restart reaps the live gateway**（32 评论，已关闭）— Windows 桌面端重启后强制杀死消息网关且不重新拉起的回归问题，涉及微信、QQ、Telegram 多平台，已关闭（修复方式待确认），社区反馈强烈。
- **[#8457] Persistent Session Memory with Cross-Session Search & Auto-Compression**（21 评论，开放中）— 要求会话记忆在网关重启后仍然存活，并支持跨会话搜索与自动压缩。该 Issue 已悬浮四个月仍在讨论，是社区对长期记忆能力的高频诉求。

## 5. Bug 与稳定性

今日报告/活跃的 Bug 按严重程度排列：

### P1（严重）

- **[#87183] CLI approval panel never renders**（8/15 新开）— `relay_runtime` 导入 `gateway.run` 导致环境变量 `HERMES_EXEC_ASK=1` 泄漏，危险命令审批面板永不渲染，命令永久挂起。与 #83626/#63183 同属环境变量泄漏家族。⚠️ 暂无对应 fix PR。
- **[#87331] Desktop auto-update can wipe the desktop build on Windows**（8/16 新开）— 强制重试时忽略 venv 锁、`hermes.exe` 隔离失败降级为警告后继续执行、ZIP 回退覆盖安装目录，三重失误叠加可致桌面构建被完全清除。⚠️ 暂无对应 fix PR，标记为 duplicate。

### P2（重要）

- **[#87295] Desktop: second launch silently kills running app's backend**（8/15 新开）— 重复启动桌面端（dock 图标或 `hermes desktop`）会静默杀死当前运行的后端进程，连接状态显示"已断开"。影响连接状态可见性与正在进行中的任务。⚠️ 暂无对应 fix PR。
- **[#87200] Desktop: subagent timeout leaves indicator stuck**（8/15 新开）— 子代理超时后，"computing… / 1 Alt ajan" 指示器卡死直至应用重启，Windows 10 可复现，标记 needs-repro。⚠️ 暂无对应 fix PR。
- **[#87292] Timeout with slow local models**（8/15 新开）— 本地慢速模型（>16 TPS）出现两类超时：WinError 10053 连接中断与 Provider 无响应。影响本地模型用户的日常使用。⚠️ 暂无对应 fix PR。
- **[#87329] OAuth callback port collision on headless host**（8/16 新开）— `hermes mcp login` 单次调用发出两个授权 URL 后即报端口已占用，导致无头服务器上的交互式 MCP 登录完全不可用。标记为 #5344 的回归。⚠️ 暂无对应 fix PR。
- **[#81048] Approval timeout misattributed as explicit user denial**（8/7 新开，仍活跃）— 危险命令审批超时被错误记录为用户明确拒绝，安全审计语义失真。该 Issue 已挂起 9 天未关闭。⚠️ 暂无对应 fix PR。

### P3（一般）

- **[#84551] detect_dangerous_command does not unwrap timeout / bash -c wrappers**（8/12 新开）— 将危险命令包裹在 `timeout` 或 `bash -c` 中即可绕过审批门禁。安全分类器需要扩展包装命令解包逻辑。⚠️ 暂无对应 fix PR。
- **[#84350] `hermes kanban show` crashes with closed database**（8/12 新开）— 纯文本模式下显示任务详情抛 `sqlite3.ProgrammingError`。标记为 duplicate。⚠️ 暂无对应 fix PR。

### 今日关闭的 Bug（9 条）

包括 #83683（桌面端重启杀死网关）、#82001（压缩后会话状态不同步）、#83569（Windows 更新自锁 cryptography）、#69107（TUI 陈旧历史拒绝有效序号）等。其中 #83569 和 #83683 属于高频痛点，关闭意味着用户可感知的稳定性提升。

## 6. 功能请求与路线图信号

今日活跃的功能请求集中在以下方向：

### 桌面端体验（明显是当前迭代重点）

- **URL 预览导航**（#87332 + #63598 双 PR 同日提交）— 为桌面端内嵌浏览器预览添加前进/后退/地址栏/刷新控件，并限制仅 HTTP(S) 协议。两个 PR 功能高度重叠，维护者需协调合并策略。这可能意味着该功能会被快速纳入下一版本。
- **土耳其语本地化**（#87305）— 完整新增 `tr.ts` 本地化文件，跟随已有 `ja.ts` / `ar.ts` 模式。若被合入，标志着桌面端 i18n 框架逐步成熟。
- **"运行中不是忙碌"语义修复**（#87330）— 将提交按钮与 busy 状态绑定到目标会话而非前台会话，支持 Worker 会话运行的同时在 Staff 会话继续输入。这解决了多会话用户的关键阻碍。
- **Skills Hub 浏览器**（#87317）— 技能管理与发现的一体化界面，已被合并（或关闭）。反映技能生态的持续投资。

### 会话与记忆

- **AI 辅助会话分组**（#87297）— 新增持久化会话组，支持 CLI 分组管理、按组限定搜索和 AI 主动建议分组的 "session-librarian" 工作流。类似功能在其他 agent 产品中已有落地，是 Hermes 会话能力的重要补充。
- **持久化会话记忆**（#8457）— 已活跃 4 个月，要求记忆跨重启存活的诉求持续升温，但目前尚无对应实现 PR。

### 压缩与上下文优化

- **Lean tail mode + 评测框架**（#87326）— 通过真实会话评测数据（+22.5 分召回）论证了更激进的保留策略的可行性，为后续压缩默认策略调优提供数据基础。

### 配置与部署

- **Termux 原生安装路径**（#86986）— 社区用户提出让 Termux 的 `pkg install/upgrade` 成为 Android 上的官方推荐安装方式，以解决当前多种安装方式共存导致的碎片化问题。

## 7. 用户反馈摘要

- **Windows 平台更新之痛**：用户 Halldrix 在 #83569 中描述 `hermes update` 在 Windows 上每次 bump `cryptography` 必然失败，即使没有网关/桌面端/REPL 在运行——"更新进程自身 import cryptography 导致 `_rust.pyd` 映射进地址空间，任何 cryptography 升级都会报 os error 5"。这类更新自锁问题与 #87331 的"更新可删除整个桌面构建"共同说明：Windows 更新链路仍是体验短板。
- **审批超时的语义问题**：Red-MPL 在 #81048 中指出"审批超时被记录为用户拒绝"，"Red-decision semantics require silence to remain silence"—审计日志中不应出现未发生的明确用户操作。这涉及安全审计的信任根基。
- **桌面端多实例问题**：YappLeCunt 在 #87295 中抱怨"第二次启动桌面端（dock 图标或 `hermes desktop`）会静默杀死后端进程"，Electron 窗口还在但连接状态已断开。用户对"静默破坏"的容忍度极低。
- **技能索引降级**：#66616 已持续一个月未修复，索引仍超龄（29.8h > 26h 限制）。直接依赖 Skills Hub 的用户受影响，但该问题一直停留在 P3 级别未获足够重视。
- **移动端/本地模型用户的声音**：BadWolf-63 在 #87292 中反馈本地慢速模型（>16 TPS）频繁超时，两种错误交替出现。本地推理场景的时间预算与云端不同，需要相应的超时策略。

## 8. 待处理积压

### 🔴 高优先级（P1/P2 且超一周未响应）

- **[#81048] Approval timeout misattributed as explicit user denial**（P2，8/7 新开，已 9 天）— 安全审计语义失真，无 fix PR。安全相关不应拖延。
- **[#51327] Hermes Desktop silently fails from .desktop launcher**（P1，6/23 新开，已 54 天）— Linux 桌面端启动器静默失败，Electron sandbox setuid 缺失，无任何错误提示。影响 Linux 桌面用户的基本使用。⚠️ 今日仍未看到进展。

### 🟡 中优先级（P2/P3 长期未关闭）

- **[#66616] Skills index is stale or degraded**（P3，7/18 新开，已 29 天）— 自动巡检持续报错，索引构建流水线可能存在问题。虽标记为 P3，但技能功能是 Hermes 差异化能力，建议提升优先级。
- **[#8457] Persistent Session Memory with Cross-Session Search & Auto-Compression**（P3，4/12 新开，已 126 天）— 社区 4 个月持续讨论的头部需求，目前无对应实现 PR 或路线图声明。建议维护者明确表态或排期。
- **[#75584] Windows update fails after interrupted install**（P2，7/31 新开，已 16 天）— `hermes.exe` 丢失 + `node_modules` ENOTEMPTY + 桌面端"UPDATE DIDN'T FINISH"，与 #87331 同属 Windows 更新健壮性缺陷。

### 🟢 低优先级（P3 超一个月）

- **[#4178] python-olm build fail**（3/31 新开，已 138 天）— 更新时报编译错误但"看起来不影响运行"，用户 kazamak 已给出完整日志，但问题长期无人跟进。低影响问题也应有明确归属。

---

*数据来源：[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)，统计周期 2026-08-15 ~ 2026-08-16。报告生成时间 2026-08-16。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-16** | **数据来源：github.com/sipeed/picoclaw**


## 1. 今日速览

PicoClaw 项目在过去 24 小时内整体活跃度处于**中等偏低水平**：无新 Issue 提交、无新版本发布，仅有 2 条 PR 更新，且均为标记为 `[stale]` 的旧 PR（创建于 8 月 7 日，最后更新于 8 月 15 日）。这两条 PR 分别针对 **WhatsApp 通道不可用（客户端版本被拒）** 和 **API 成本优化（前缀缓存失效）** 两个实际问题，目前均处于待合并状态，等待维护者审核。社区讨论趋近于零，项目当前处于**维护节奏放缓期**。


## 2. 版本发布

**今日无新版本发布。**

上一版本信息暂缺，建议关注 Releases 页面获取后续更新。


## 3. 项目进展

今日无 PR 被合并或关闭，但有 **2 条待合并 PR** 值得关注，分属两个关键方向：

- **[#3321] fix(agent): move dynamic context after history to preserve prefix caching**
  - 作者：grrowl ｜ 创建于 2026-08-07 ｜ [链接](https://github.com/sipeed/picoclaw/pull/3321)
  - **核心改动**：将 `## Current Time`、`## Runtime`、`## Current Session`、`## Current Sender` 等动态上下文块从 system message 头部移至对话历史之后。
  - **解决的问题**：原实现导致每次请求都使前缀缓存全部失效（动态块在头部，任何 token 变化都会使历史部分的缓存不可用），显著增加 API 成本。调整后缓存命中率将大幅提升，**对高频调用用户的 API 账单优化效果明显**。

- **[#3320] fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)"**
  - 作者：grrowl ｜ 创建于 2026-08-07 ｜ [链接](https://github.com/sipeed/picoclaw/pull/3320)
  - **核心改动**：升级 `go.mau.fi/whatsmeow` 依赖版本，绕过 WhatsApp 官方的客户端版本校验。
  - **解决的问题**：当前固定的 whatsmeow 版本被 WhatsApp 服务器拒绝（`Client outdated (405)`），导致连接在约 5 秒后被断开且无重连机制，**原生 WhatsApp 通道目前已处于完全不可用状态**。

> ⚠️ 两条 PR 标记为 `[stale]`，意味着已超过一段时间未获维护者响应，存在被自动关闭的风险。


## 4. 社区热点

今日无活跃讨论（0 条 Issue 更新、0 条新评论）。

仅有的 2 条 PR 更新来自同一作者 grrowl，且均被标记为 stale，反映出**社区中可能已有用户遇到相关问题但缺乏聚集讨论的渠道**。两条 PR 背后的共性诉求是**让 PicoClaw 在真实生产环境中稳定运行**——无论是通过依赖升级保持通道活性，还是通过缓存优化降低成本。


## 5. Bug 与稳定性

今日无新 Bug 报告。但根据 PR #3320 的描述，存在一个**未记录在 Issues 中的已知严重 Bug**：

| 严重程度 | 问题描述 | 影响范围 | 修复 PR |
|---------|---------|---------|--------|
| 🔴 **严重** | WhatsApp 原生通道完全不可用，连接被服务端拒绝（`Client outdated 405`），且无自动重连 | 所有使用 WhatsApp 通道的用户 | [#3320](https://github.com/sipeed/picoclaw/pull/3320)（待合并） |
| 🟡 **中等** | 前缀缓存全部失效，导致 API 请求成本显著上升 | 高频调用 LLM API 的用户 | [#3321](https://github.com/sipeed/picoclaw/pull/3321)（待合并） |

> 注：这两个问题均通过 PR 直接修复，未走 Issue 流程，建议维护者补充 Issue 记录以便追踪。


## 6. 功能请求与路线图信号

今日无新功能请求。但 PR #3321 暗示了 PicoClaw 的 API 使用策略正在向**成本效率优化**方向演进——动态上下文的位置调整将直接影响 token 消耗，这可能是继功能完备性之后的下一优化重点。同时，PR #3320 表明**通道稳定性和依赖及时更新**应被纳入路线图的持续维护项。


## 7. 用户反馈摘要

今日无新评论可提取。基于 PR 描述推断的用户反馈信号：

- **WhatsApp 用户**：存在“通道静默失效”的体验痛点——连接在 5 秒后被静默丢弃，且无自动重连或错误提示，用户可能长时间无感知。建议后续补充**断线重连与错误通知机制**。
- **API 成本敏感用户**：动态上下文在前导致缓存频繁失效的问题若长期存在，用户将面对不必要的成本支出。PR #3321 的修复将直接惠及此类用户。
- **维护者响应预期**：两条 PR 已存在 9 天且标记为 stale，社区对维护者响应速度的耐心可能正在耗尽。


## 8. 待处理积压

| 项目 | 类型 | 待处理时长 | 状态 | 关注建议 |
|------|------|-----------|------|---------|
| [#3321](https://github.com/sipeed/picoclaw/pull/3321) fix(agent): 调整动态上下文位置以保留前缀缓存 | PR | 9 天 | 待合并，已 stale | ⚠️ 涉及 API 成本优化，建议优先审阅 |
| [#3320](https://github.com/sipeed/picoclaw/pull/3320) fix(deps): 升级 whatsmeow 以修复 WhatsApp 405 | PR | 9 天 | 待合并，已 stale | ⚠️ WhatsApp 通道当前不可用，建议紧急审阅 |

**维护者建议**：
1. **立即处理 #3320**：WhatsApp 通道不可用属于 P0 级故障，建议优先审阅合并（或给出明确反馈）。
2. **同步审阅 #3321**：两个 PR 同源且改动互不冲突，可一并处理。
3. **考虑补录 Issue**：将上述两个问题从 PR 描述中提取为正式 Issue，方便社区追踪和讨论。
4. **关注 stale 策略**：确认 stale bot 的自动关闭时限，避免有效贡献被误关。

---

*报告生成时间：2026-08-16 | 数据窗口：2026-08-15 ~ 2026-08-16*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-16** | **数据周期：2026-08-15 至 2026-08-16**


## 1. 今日速览

NanoClaw 今日处于**高活跃开发状态**。过去 24 小时内共有 22 条 PR 更新，其中 19 条待合并、3 条已关闭/合并，核心团队（gavrielc）连续提交了 10+ 个功能开发 PR，涵盖频道适配器能力扩展、权限拦截机制、跨会话上下文等基础设施模块。无新版本发布、无新 Issue 开启，也未报告新的用户侧 Bug，项目处于**快速功能迭代期**，工程化纪律良好（所有核心 PR 均带 `[follows-guidelines]` 标签）。值得关注的是，持续数月的 **Discord 附件处理 PR #2752** 仍未合并，且 `Telegram 频道集成`（PR #3269）与 `Telegram Markdown 渲染修复`（PR #3250）同日出现，建议维护者评估两者可协同合并。


## 3. 项目进展

今日合并/关闭 3 项，核心进展集中在基础设施稳定性和正确性修正：

- **PR #3268（已关闭）** — [修复 poll-loop 泄漏问题](https://github.com/nanocoai/nanoclaw/pull/3268)：`runPollLoop` 仅在迭代间隙检查 `config.signal`，而循环通常停在 `processQuery` 的常开 stream 上，导致循环中止后活动查询及其 500ms 跟随轮询器泄漏。提交包含根因修复和后续清理，属稳定性关键修复。

- **PR #37（已关闭）** — [项目改名 + Telegram 替换 WhatsApp](https://github.com/nanocoai/nanoclaw/pull/37)：将 `nanoclaw` 更名为 `dotclaw` 并全面替换 WhatsApp 集成为 Telegram bot。该 PR 自 2 月创建后长期搁置，今日最终关闭，标志着**平台方向的重大转向落地**——值得注意：该 PR 标题中使用了 `DotClaw` 名称，而其余活动 PR（#3269、#3250）均明确指向 Telegram 而非 WhatsApp，表明项目已从 WhatsApp 转向 Telegram 生态。

- **PR #3263（待合并）** — [频道注册表热启动机制](https://github.com/nanocoai/nanoclaw/pull/3263)：新增 `startChannelAdapter(key)` 方法，使新增注册的适配器实例可在运行时热启动，避免重启整个容器。该 PR 虽未合并，但极大增强了频道适配器的运维灵活性。


## 4. 社区热点

今日活跃讨论集中在 22 个 PR 中，最值得关注的三个讨论热点（按评论数排序）：

1. **PR #3269（评论最多）** — [Telegram 频道集成](https://github.com/nanocoai/nanoclaw/pull/3269)：新增 `@chat-adapter/telegram` 适配器，包含配对流程和 Markdown 清理器，并接入 `src/channels/index.ts` 自注册。这是社区呼声最高的频道扩展方向，值得注意该 PR 未带 `[follows-guidelines]` 标签，或为外部贡献。

2. **PR #37** — [改名 + Telegram 迁移](https://github.com/nanocoai/nanoclaw/pull/37)：虽然是关闭状态，但作为 6 个月前提出的大规模重构，其关闭本身值得关注——项目方向从 WhatsApp 转向 Telegram 的决策靴子落地。

3. **PR #3250** — [Telegram Markdown 加粗渲染为斜体修复](https://github.com/nanocoai/nanoclaw/pull/3250)：`telegram-markdown-sanitize.ts` 为兼容旧版 converter 的 workaround，实际把 `**bold**` 降级成了 `_italic_`。该 PR 链接 `@chat-adapter/telegram` 的修复方案，建议与 #3269 协同审查。

**核心诉求**：社区对 **Telegram 生态的支持**（PR #3269、#3250、#37）表现为最高优先级，同时对 **Discord 附件处理**（PR #2752）的诉求已持续多月，背后是真实用户对多频道生产环境的强烈需求。


## 5. Bug 与稳定性

今日无新 Issue 提交，但 PR 中暴露并修复了以下稳定性问题（按严重程度排列）：

| 严重程度 | 问题描述 | 状态 |
|---------|---------|------|
| 🔴 **高** | [PR #3268](https://github.com/nanocoai/nanoclaw/pull/3268)：poll loop 泄漏——循环中止后活动查询及其 500ms 跟随轮询器持续运行，消耗资源 | **已关闭（修复）** |
| 🟠 **中高** | [PR #3254](https://github.com/nanocoai/nanoclaw/pull/3254)：冲积 context（trigger=0）行导致任务行被挤出批次——`getPendingMessages` 只取最新 N 行，导致任务被 context 挤掉 | **待合并** |
| 🟠 **中高** | [PR #3255](https://github.com/nanocoai/nanoclaw/pull/3255)：多机器人同一房间时投递目标解析错误——按平台地址的 fallback 取到任意兄弟实例的行 | **待合并** |
| 🟡 **中** | [PR #3251](https://github.com/nanocoai/nanoclaw/pull/3251)：API rate-limiting 期间心跳文件不更新，导致误杀正常运行的容器（stall 30+ 分钟） | **待合并** |
| 🟡 **中** | [PR #3252](https://github.com/nanocoai/nanoclaw/pull/3252)：无 heartbeat 文件的空闲容器被绝对上限 kill 永久豁免 | **待合并** |
| 🟢 **低** | [PR #3253](https://github.com/nanocoai/nanoclaw/pull/3253)：group reasoning effort 未在 model config 中生效 | **待合并** |
| 🟢 **低** | [PR #3259](https://github.com/nanocoai/nanoclaw/pull/3259)：skill-apply 步骤标题序号错误显示（heading 序数未剥离） | **待合并** |


## 6. 功能请求与路线图信号

基于 PR 推断，以下功能**已在开发中**，极可能纳入下个小版本：

1. **Telegram 全面支持** — [PR #3269](https://github.com/nanocoai/nanoclaw/pull/3269)（频道适配器）+ [PR #3250](https://github.com/nanocoai/nanoclaw/pull/3250)（Markdown 渲染修复）+ [PR #37](https://github.com/nanocoai/nanoclaw/pull/37)（平台切换），三条 PR 均指向 Telegram 优先级提升，建议维护者合并评估。

2. **频道适配器能力扩展** — [PR #3261](https://github.com/nanocoai/nanoclaw/pull/3261)：`setTyping` 增加状态行与状态类型（auto/agent）、`setThreadTitle`、`setSuggestedPrompts`，并将这些能力设为可选项以兼容无法渲染的平台。

3. **Channel SDK 桥接层增强** — [PR #3262](https://github.com/nanocoai/nanoclaw/pull/3262)：为 DM 形态增加 app-context 捕获和 DM-thread 规范化，使平台可支持 DM 线程感知。

4. **跨会话上下文（Cross-session context）** — [PR #3257](https://github.com/nanocoai/nanoclaw/pull/3257)：为多会话 agent groups 提供上下文 fan-out、DM 回填与回显剪枝，并新增 `ncl sessions history` 命令。

5. **权限策略细化** — [PR #3260](https://github.com/nanocoai/nanoclaw/pull/3260)：新增 `decline_notify` 未知发送者策略（礼貌拒绝 + 一行 owner FYI），以及 [PR #3266](https://github.com/nanocoai/nanoclaw/pull/3266) 的频道注册卡片拦截器 seam。

6. **容器调度栈强化** — [PR #3256](https://github.com/nanocoai/nanoclaw/pull/3256)（`detached_at` 迁移 022）、[PR #3265](https://github.com/nanocoai/nanoclaw/pull/3265)（`suppressCreatedNotify` 选项）。


## 7. 用户反馈摘要

今日无新 Issue 评论，从 PR 描述中提炼核心用户场景与痛点（间接反馈）：

- **Discord 用户（PR #2752）**：粘贴的文本（自动转为 `message.txt`）和图片永远无法被 agent 读取，用户只能看到 `[file: message.txt]`/`[image: foo.png]` 占位符。该问题自 6 月 12 日提交以来已搁置 2 个月未合并。

- **Telegram 用户（PR #3250）**：所有 agent 发出的 `**bold**` 在 Telegram 上渲染为 **_italic_**，且**加粗彻底丢失**——这是肉眼可见的体验降级。

- **多机器人混合场景（PR #3255）**：同一房间存在多个 bot 身份时，投递系统将消息发送给错误的实例，说明多实例部署并非边缘场景，而是真实用户实际使用的配置。

- **长时间运行容器（PR #3251）**：API 限流 30+ 分钟期间，心跳文件不更新导致正常容器被误杀——这是生产环境用户会遇到的严重稳定性问题。

- **Discord 附件问题（PR #2752）**：自 6 月至今未合并，影响所有使用 Discord 渠道的用户，是本项目**最痛的用户体验缺口**。

**对以上 PR 的建议**：合并 Telegram 相关 PR（#3269、#3250、#37）；优先合并稳定性修复类 PR（#3254、#3255、#3251）；明确 #2752（Discord）的合并时间表或替换为 #3269 的 Telegram 方案。


## 8. 待处理积压

以下 Issue/PR 长期未获响应，需维护者关注：

| 类型 | 编号/标题 | 创建时间 | 搁置时长 | 状态 |
|------|----------|---------|---------|------|
| 🔴 **PR** | [#2752 Discord 附件阶段化处理](https://github.com/nanocoai/nanoclaw/pull/2752) | 2026-06-12 | **2 个月+** | 待合并，长期无活跃讨论 |
| 🟡 **PR** | [#37 改名 + 平台迁移](https://github.com/nanocoai/nanoclaw/pull/37) | 2026-02-02 | 6 个月+ | 今日关闭（合并），建议发布变更说明 |
| 🟢 **待合并队列** | 19 个待合并 PR（含今日新增 15 个） | 多为 2026-08-15 | 1 天 | 积压信号：数量庞大，建议分批处理 |

**维护者行动建议**：优先合并 Telegram 生态与稳定性修复（#3268、#3254、#3255、#3251）；明确 #2752（Discord）的合并时间表或替换为 #3269 的 Telegram 方案；将 19 个待合并 PR 按依赖关系分批（建议按 A1-A8 的 PR 编号顺序推进，它们之间存在明显的前置依赖关系）。


*本日报基于 NanoClaw GitHub 仓库公开数据自动生成，数据统计截止 2026-08-16。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-16

*数据窗口：2026-08-15 至 2026-08-16 | 数据来源：GitHub NullClaw/NullClaw 仓库*


## 1. 今日速览

项目当日活跃度偏低但方向明确：24小时内新增 1 个 Issue（功能请求）和 1 个 PR（性能优化），均处于开放状态，无版本发布。值得关注的是，PR #987 针对本地工具密集型长任务的循环优化属于**架构级改进**（系统提示词分段缓存 + 工具输出压缩），预计对长上下文场景有显著收益；而 Issue #988 提出的代理支持是**连接层基础能力**的补全需求。总体而言，项目处于"小步快跑"阶段，社区讨论热度不高但提交质量扎实，未出现阻塞性问题。


## 2. 版本发布

今日无新版本发布，无迁移注意事项。


## 3. 项目进展

**合并/关闭 PR：无**

**待合并 PR（1 条）：**

- **[#987 feat(agent): loop hygiene for long local tool-heavy runs](https://github.com/nullclaw/nullclaw/pull/987)** — 作者：vernonstinebaker
  - **核心改进：**
    - 系统提示词拆分为**稳定前缀 + 动态时间戳尾部**，并引入 `stablePrefixHash` 提高缓存命中率
    - 新增 `result_compress.zig` 对工具输出进行压缩后再注入历史记录（观察者日志仍保留完整输出）
    - 增加逐轮相同调用的循环检测（"per-turn identical-call lo..."）
  - **项目意义：** 该 PR 直接针对 agent 在本地工具密集场景下的**上下文膨胀**与**重复调用**两大痛点，属于性能与成本优化层面的实质性推进。若合并，将显著提升长任务稳定性和 token 效率，并为后续支持更复杂工具链奠定基础。


## 4. 社区热点

今日仅 1 条 Issue 和 1 条 PR，均无评论互动，讨论热度低。值得关注的是：

- **[Issue #988: 为 providers 添加 HTTP(s) 与 SOCKS5 代理支持](https://github.com/nullclaw/nullclaw/issues/988)**（作者：anpic）
  - 虽无评论，但该需求具有普遍性——无论是企业内网环境、跨地域访问还是隐私保护场景，代理支持都是生产部署的常见前置条件。这条 Issue 目前没有任何 `👍`，说明尚未引起广泛关注，但**实用性不可忽视**。

> 注：由于 PR #987 评论字段为 undefined，无法获取其讨论详情。


## 5. Bug 与稳定性

**今日新报告 Bug：无**

项目当前无已知崩溃、回归或严重稳定性问题。PR #987 中包含的循环检测（identical-call loop）可视为对潜在死循环/重复执行问题的预防性加固，非紧急修复。


## 6. 功能请求与路线图信号

| 请求 | 类型 | 来源 | 可能纳入版本？ |
|------|------|------|---------------|
| **HTTP(s)/SOCKS5 代理支持** | 网络层能力补充 | [Issue #988](https://github.com/nullclaw/nullclaw/issues/988) | 评估中 — 当前无对应实现 PR；属于基础设施类需求，通常优先级中等，取决于维护者对部署场景的重视程度 |
| **工具输出压缩**（已在 PR #987 实现） | 性能优化 | [PR #987](https://github.com/nullclaw/nullclaw/pull/987) | 高概率随下个版本发布（P0 级优化） |
| **系统提示词稳定性缓存**（已在 PR #987 实现） | 性能优化 | [PR #987](https://github.com/nullclaw/nullclaw/pull/987) | 高概率随下个版本发布 |

**路线图信号：** PR #987 暗示当前开发重点在 **long-horizon agent 任务稳定性/性价比优化**；Issue #988 则指向**下游 provider 接入的灵活性**。两相结合，可推测下一迭代方向为"让 agent 在真实网络环境与长任务中更可靠、更经济"。


## 7. 用户反馈摘要

**直接评论反馈：无**（两个条目均 0 评论）

**间接信号分析：**
- Issue #988 的提交者 anpic 需要一个**开箱即用的代理配置选项**，推测其使用场景为受限网络环境（企业代理/防火墙内）或需要匿名访问外部 API——典型用户画像为**有生产部署需求的个人开发者或小团队**。
- PR #987 作者 vernonstinebaker 关注**长任务运行成本与稳定性**，该 PR 的粒度（函数级重构、压缩算法引入）表明作者对代码质量与可维护性有较高要求，推测其正在运行大规模的本地工具链 agent 工作负载。


## 8. 待处理积压

**高优先级：**

- 无长期未响应的阻塞性问题或 PR

**中优先级（提醒关注）：**

- **[Issue #988 代理支持](https://github.com/nullclaw/nullclaw/issues/988)**：1 天内未获任何响应（Label 标签、维护者评论、👍 均无）。建议维护者评估该需求优先级并给出明确 roadmap 回应，避免社区贡献者因反馈缺失而流失。
- **[PR #987](https://github.com/nullclaw/nullclaw/pull/987)**（开放已超 24 小时）：虽非"长期"，但该类架构级改进若长期搁置将增加合并成本。建议维护者尽快安排 code review。

---

*本报告由 AI 分析师基于 GitHub 公开数据自动生成，数据截止 2026-08-16 00:00 UTC。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-16

## 1. 今日速览

IronClaw 在过去 24 小时内保持高位运行：27 条 Issue 更新（21 条关闭）与 12 条 PR 更新（5 条合并/关闭）表明项目正处于核心重构与性能优化的关键收尾窗口。本日最显著的特征是 **围绕 `#7591` 性能史诗的系列 Tier 1/Tier 2 Issue 批量关闭**（#7593、#7595、#7596、#7597、#7599），配套的 PR #7628（heartbeat 去抖动）和 #7629（触发/出站写放大削减）已合并，显示优化工作正从问题定义快速推进到落地。另一信号是 **“unbound-turns”大重构完成**（PR #7634 合并），伴随 4 个架构审查后置 Issue（#7671–#7674）被打开，说明核心团队在合并大型 PR 后依然保持谨慎的追责机制。整体活跃度评级：**高**，项目健康度：**良好**。

## 2. 版本发布

过去 24 小时无新版本发布。最新 Releases 无。

## 3. 项目进展

本日合并的 PR 集中在两个方向：

**方向一：写放大与存储层优化（对应 #7591 史诗）**

- **PR #7628** (merged, M, risk: low): `perf(processes): remove heartbeat journal churn` — 实现了 #7591 中保守安全的 heartbeat 子集：停止每个 heartbeat 追加 `ProcessJournalKind::Heartbeat` 行（对应 #7593），同时将 turn-runner heartbeat 间隔拉宽至 15 秒。该 PR 为后续 #7599（5s→15-20s 间隔放宽）铺平道路。见 [PR #7628](https://github.com/nearai/ironclaw/pull/7628)。
- **PR #7629** (merged, M, risk: low): `perf: reduce trigger and outbound state writes` — 将 trigger run-history 的 prune 从每次 Running 行更新时触发改为仅在首次 fire claim 时执行（对应 #7595），移除了死代码 `advance_subscription_cursor` durable-offset API（对应 #7597）。见 [PR #7629](https://github.com/nearai/ironclaw/pull/7629)。
- **PR #7676** (closed/merged, L, risk: low): `perf(threads): coalesce thread index touches` — 将 bursty 的 per-thread 活跃触摸合并为有界的线程索引写入（对应 #7596），flush 最新 pending 时间戳以保证终态线程恢复侧栏优先级，并通过单调 CAS 保持多 worker 正确性。见 [PR #7676](https://github.com/nearai/ironclaw/pull/7676)。
- **PR #7677** (OPEN — 今日新增): `perf(threads): fold message lookup indexes into message rows` — 将消息查找键作为索引投影直接存入消息条目，替代每消息 1-3 个 sibling 行写入，同时保留 legacy sibling 行回退路径。这是顺着 #7596 逻辑自然延伸出的进一步存储优化。见 [PR #7677](https://github.com/nearai/ironclaw/pull/7677)。

**方向二：Unbound-turns 重构落地**

- **PR #7634** (merged, XL, risk: low): `feat(unbound-turns): complete the switchover to prepared-context turns` — 完成到 unbound-turns 模型的完全切换，交付了设计文档 #7633 中记录的每一个 follow-up，并对两份设计文档进行了 71 条款一致性审计，所有分歧要么关闭要么明确记录。该 PR 堆叠在 #7562 之上。见 [PR #7634](https://github.com/nearai/ironclaw/pull/7634)。

**其他合并项**：

- **PR #7670** (merged, XS, CI): `chore(agents): refresh codebase knowledge graph` — 每日自动刷新 codebase-memory 快照。见 [PR #7670](https://github.com/nearai/ironclaw/pull/7670)。
- **PR #7641** (OPEN — archive parity-blocked skill bundles)：将 17 个 parity 阻塞的 skill 包从构建扫描路径移至 `docs/internal/archived-skills/`，保留恢复条件。该 PR 是技能生态整理的一部分，合入后可缩小 CI 构建面。见 [PR #7641](https://github.com/nearai/ironclaw/pull/7641)。

**尚在等待合并的高价值 PR**：

- **PR #7651** (OPEN, XL, risk: low): `feat(automations): add deterministic no-result suppression` — 要求 `trigger_create` 必须由模型从用户措辞中推导出 `result_delivery`（仅通知匹配/变更/结果的显式意图选中抑制，中性措辞确定性回退到 `deliver`）。见 [PR #7651](https://github.com/nearai/ironclaw/pull/7651)。
- **PR #7678** (OPEN, XL, risk: low): `perf(capabilities): persist invocation state at gate and terminal edges` — 将 capability 调用状态保持 worker-local，仅在 completed/failed/approval-blocked/auth-blocked 边界原子物化，避免 journal 排队和 claimed 转换，保持 lease-fenced 跨 worker 恢复。见 [PR #7678](https://github.com/nearai/ironclaw/pull/7678)。
- **PR #7679** (OPEN, XL, risk: low): `fix(live-qa): stop harness bugs reddening green canary runs` — 修复 Live Canary 连续 30/30 次红跑的 3 个 harness 缺陷（其中 `qa_10h_slack_email_hallucination_guard` 等用例在 durabl 证据成立时被 liveness proxy 误标红）。见 [PR #7679](https://github.com/nearai/ironclaw/pull/7679)。

## 4. 社区热点

**今日最热的 Issue 是 #467 —— Trajectory benchmark system for agent quality evaluation**（4 条评论，创建于 3 月，今日 8/15 仍被更新）。该 Issue 提议构建一个通过真实 agent loop 运行真实用户场景、再用硬性断言 + LLM-as-judge 双层标准进行轨迹评估的基准系统。它被持续关注的原因在于：这是项目迈向“可度量”的关键基础设施，对模型选型、能力比较、回归验证都有直接价值。

在该 Issue 下，讨论集中在四层评估设计的细节：硬性断言覆盖工具选择/响应内容/成本/时延，LLM-as-judge 处理相对判断，两条腿走路的实现方式，以及相对/硬性标准的配比问题。这块工作若落地，将有望让 IronClaw 的能力评估从“用例跑通”升级为“质量可量化”。

近期虽无新评论，但该 Issue 持续在 8/15 被 touch，说明团队内部仍在积极跟进。见 [Issue #467](https://github.com/nearai/ironclaw/issues/467)。

此外，**PR #7491**（omp core-tool 契约 + 引擎 + 基准测试臂，XL 体量，已挂 5 天仍开放）也持续受到关注。该 PR 将模型侧 coding 工具表面收敛为六个确切的裸名称（`read/write/edit/glob/grep/bash`），删除旧文件工具和 `builtin__*` 拼写。这是一次较大的表面积变更，社区关注点在于其对现有 skill 兼容性的影响。见 [PR #7491](https://github.com/nearai/ironclaw/pull/7491)。

## 5. Bug 与稳定性

以下按严重程度排列今日报告的 Bug / 稳定性问题：

**高严重度**

- **#7675** `[OPEN] E2E: qa_6c gmail-to-sheet flake cascades across the whole provider-contracts session` — 两个问题：`qa_6c_gmail_to_sheet_live_chat` 的间歇性资源类能力失败（live Gmail/emulate 腿间歇返回泛化错误），以及单个 flake 导致整个 provider-contracts 会话级联红化。属于测试基础设施问题，但会掩盖真实的回归信号。尚无 fix PR 指配。见 [Issue #7675](https://github.com/nearai/ironclaw/issues/7675)。

**中严重度**

- **#7671** `[OPEN] Capability dispatch stack pressure: kernel sandbox path still near the test-stack edge` — 从 #7634 审查中带出的 follow-up：`LoopCapabilityPort` 装饰链被编译成单个超大 poll frame，溢出了默认 2 MiB 测试线程栈。f1f396cd8 已通过 chain-boxing 每个 port delegation 修复了该套件，但 Issue 仍在追踪 kernel sandbox 路径是否已彻底脱离边界。见 [Issue #7671](https://github.com/nearai/ironclaw/issues/7671)。
- **#7673** `[OPEN] BudgetLedger accounting refinements: truncated-launch reconciliation and charge durability` — 从 #7634 审查带出：截断启动窗口会双重计费（`try_charge_invocations(visible_calls.len())` 先于 `invoke_batch` 执行，随后截断路径再次计费）。两个缺口均保守方向（过度计数 → 更早停止；绝不超上限）。无 fix PR。见 [Issue #7673](https://github.com/nearai/ironclaw/issues/7673)。

**低严重度 / 已修复**

- **#6726** `[CLOSED] extension host: register_generic_channel_outbound_targets can be a no-op` — 该函数可被替换为 no-op 且所有测试层仍通过，作为 #6681 审计（52 个 mutant：39 个被捕获、12 个不可行）中唯一的存活 mutant。已关闭，大概率已修复或删除。见 [Issue #6726](https://github.com/nearai/ironclaw/issues/6726)。
- **#5237** `[CLOSED] Reborn hosted debug logging floods Railway with Cranelift/Wasmtime DEBUG output` — 生产环境设置 `IRONCLAW_REBORN_LOG=debug` 时被 Wasmtime/Cranelift 编译器 DEBUG 日志淹没。已关闭。见 [Issue #5237](https://github.com/nearai/ironclaw/issues/5237)。

**Live Canary 全红事件（同日重大稳定性事件）**

PR #7679 揭示了一个关键事实：**Live Canary 已连续 30/30 次全红，但其中大部分是 harness 缺陷而非产品缺陷**。四个根因：3 个 harness bug 误杀了正确的产品行为 + 1 个 liveness 代理误判。该 PR 正在修复这些 harness 问题，确保 Canary 从“红噪”中恢复其信号价值。详见 [PR #7679](https://github.com/nearai/ironclaw/pull/7679)。

## 6. 功能请求与路线图信号

**Trajectory benchmark（#467）** 是为量化和可观测性铺路的基础设施需求，短期内可能进入实施阶段（已挂着 5 个月，8/15 仍活跃）。值得关注的信号是它可能构成下一个 milestone 的评估基线。

**Typed ToolChoice（#7672）** 从 #7634 审查带出：`LoopModelRequest` 的 `tool_choice: Option<String>` 在多 provider 编码器（rig_adapter/bedrock/nearai_chat/gemini_oauth/codex_chatgpt/openai_codex_provider）中用作字符串匹配（"auto"/"required"/"none"），超载了模式字符串和工具名。建议替换为类型化枚举。该建议若被采纳，将消除一批字符串匹配类 bug。见 [Issue #7672](https://github.com/nearai/ironclaw/issues/7672)。

**Architecture tests: symbol-level allowlist（#7674）** 从 #7634 审查带出：现有依赖边界测试只守 crate 级别，不约束具体符号。建议为 openai-compat→threads 边界的入口符号（accept door 的 seed vocabulary 和唯一 validator）增加符号级 allowlist。这是对依赖边界治理的一次细粒度升级。见 [Issue #7674](https://github.com/nearai/ironclaw/issues/7674)。

**从 #7634 审查带出的 4 个 follow-up Issue（#7671–#7674）** 意味着合并后审查文化正在动作化——每个风险点都被显式跟踪而非口头讨论。

**PR #7651** 的 deterministic no-result suppression（自动化结果交付的确定性抑制）若合并，将改善 automations 这类功能在真实用户场景下的可预期性。

**PR #7516**（operator surface for IronHub agent link，新贡献者 neo-sky）仍在开放队列中。它补齐了 WebUI 侧的关键运维路径——当前用户只能通过 CLI 获取 IronHub register URL 和安装 hub 合约共享密钥，部署无法通过 WebUI 完成 agent 链接。见 [PR #7516](https://github.com/nearai/ironclaw/pull/7516)。

## 7. 用户反馈摘要

- **Canary 连续 30 次红跑的检出与响应（#7679）** 显示维护方对假阳性容忍度低，在排查后迅速定位到 harness 层缺陷并提 PR 修复。用户（观测者）对此类纠偏动作普遍持正面态度，因为“红噪”会显著消耗排错时间。
- **Telegram forum-topic 覆盖缺口（#6829）** 在关闭时附带说明了：回复 forum topic 中的消息必须携带 `message_thread_id`，否则消息会落入 supergroup 被错误受众看到。该反馈指向 channel/web 层一个容易被忽略但影响真实使用的细节。
- **#6821（IronHub 搜索误读）** 的关闭表明自由文本匹配被修复——之前向 agent 询问“show me what I can install from IronHub”时，agent 仅报 3 个工具（真实签名目录有 18 个），甚至列出了 20 个非目录条目。这是用户可感知的严重质量缺陷；已关闭暗示修复已并入某条主线（如 #6780 的 preview build）。
- **多篇 Issue 在关闭时均带有 1 条评论**，且大多数是 8/15 当天的更新，这反映出维护团队在批量清账时有系统性的注释记录习惯，便于追溯关闭理由。

## 8. 待处理积压

以下 Issue/PR 或长期未积极更新，或等待特定里程碑/决策：

- **#467 Trajectory benchmark system** — 3 月创建至今 5 个月，虽在今天仍被 touch，但一直没有实施 PR。作为可能纳入下一里程碑的评估基础设施，需要维护者给出明确的时间表或移出 backlog 的决策。见 [Issue #467](https://github.com/nearai/ironclaw/issues/467)。
- **#5588 reborn: track QA-discovered production follow-ups removed from PR #5380** — 7/3 创建，已有 0 评论，但在 8/15 被关闭。该 Issue 原本用于跟踪从 QA 矩阵 PR 中剥离的生产行为变更，关闭时未留下实施 PR 的链接，存在“后续动作丢失”的风险，建议维护者核实这些变更是否已在其他 PR 中覆盖。见 [Issue #5588](https://github.com/nearai/ironclaw/issues/5588)。
- **PR #7491**（omp core-tool 契约 + 基准臂，XL 体量）已挂 5 天仍开放，它是 #7392 Issue 的 slice 1-4。该 PR 若合入将移除旧工具表面（不做 flag 隐藏），这需要各 related workstream 的同步配合。见 [PR #7491](https://github.com/nearai/ironclaw/pull/7491)。
- **PR #7516**（IronHub WebUI 运维入口）— 新贡献者 neo-sky 的早期 PR，自 8/12 开放至今，尚无 reviewer 动作。见 [PR #7516](https://github.com/nearai/ironclaw/pull/7516)。

---

> 报告基于 2026-08-15 至 2026-08-16 的公开 GitHub 数据自动生成。所有链接均可点击访问原始 Issue/PR。如需进一步细节，可查阅对应 Epic（#7591、#7633、#4775）或浏览 [IronClaw 仓库主页](https://github.com/nearai/ironclaw)。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-16

## 今日速览

过去24小时内，LobsterAI 项目共产生 18 条 Issue 更新和 6 条 PR 更新，无新版本发布。**项目整体活跃度中等偏低**：大部分 Issue 和 PR 均为 stale 标签下的批量关闭或停滞状态，真正意义上的新讨论极少。值得关注的是，当前共有 **4 个 PR 处于待合并状态**（其中 3 个为 dependabot 自动依赖更新，1 个为人工提交的功能修复），以及 **2 个 Issue 仍处于开放状态**，均涉及用户实际使用中的核心痛点。项目社区讨论热度趋冷，需警惕维护节奏放缓的信号。

## 版本发布

无新版本发布。

## 项目进展

今日无 PR 被合并。当前等待合并的 PR 包括：

* **#1879** `fix: preserve manually-added plugin load paths on config sync`（OP EN→CLOSED 状态不明）— 修复 LobsterAI 在同步 openclaw.json 配置时，会静默丢弃用户手动添加的插件加载路径的问题。如果合并，将改善社区插件（如 memory-lancedb-pro）的兼容性。[链接](https://github.com/netease-youdao/LobsterAI/pull/1879)
* **#2234** `fix(openclaw): cron yield descendant finalization`（状态 CLOSED）— 修复 cron 任务中父子 agent 完成事件传递问题，覆盖普通会话/cron 并行/cron 串行三种子 agent 场景。[链接](https://github.com/netease-youdao/LobsterAI/pull/2234)

另有 3 个依赖更新 PR（trufflehog、actions/checkout、paths-filter、actions/stale）处于待合并状态，均来自 dependabot，属于常规 CI 依赖升级。整体而言，**项目核心功能在本周期内没有实质性代码推进**。


## 社区热点

过去24小时内，社区讨论热度整体较低。虽有多条 Issue 更新，但绝大部分为 stale 机器人自动关闭，非真实活跃讨论。

* **Issue #1903** `会员登录频繁失败`（唯一处于开放状态的活跃 Issue）— 用户报告会员登录持续失败，导致无法使用网易付费模型。该 Issue 自 5 月 7 日创建以来已持续 3 个月未获解决，反映了用户对付费服务稳定性的关注。[链接](https://github.com/netease-youdao/LobsterAI/issues/1903)

* **Issue #2046** `OpenClaw/LobsterAI产品建议：Agent 记忆体系`（另一处于开放状态的 Issue）— 用户提交了长篇产品建议，核心诉求是 Agent 记忆能力不足，目前过度依赖用户手动维护。建议按优先级排列了 5 项改进方案，体现出用户对 Agent 跨 session 记忆的强烈需求。[链接](https://github.com/netease-youdao/LobsterAI/issues/2046)

值得关注的是，一批由用户 @woxinsj 提交的技术分析类 Issue（如 #2039、#2040、#2041）此前引发了较多讨论，但均已被关闭，表明此类深度技术讨论未得到持续跟进。


## Bug 与稳定性

过去24小时内未发现新增 Bug 报告，但存在以下历史遗留问题仍处于开放状态：

| 严重程度 | Issue# | 问题描述 | 状态 | 是否已有修复 PR |
|---------|--------|---------|------|---------------|
| 🔴 高 | #1903 | 会员登录频繁失败，用户无法使用付费模型 | 开放（5月7日创建） | 无 |
| 🟠 中 | #1849 | 追问时出现无限 NO_REPLY，任务被提前标记完成但模型仍在输出 | 已关闭（stale） | 未知 |

此外，PR #1879 修复了配置同步时丢失用户手动插件路径的问题，PR #2234 修复了 cron yield 子任务未正确驱动父 agent 的问题，均已成为待合并状态，但尚未被正式合并，相关修复仍停留在 PR 层面。


## 功能请求与路线图信号

以下功能请求值得关注，可能纳入下一版本规划：

1. **Agent 记忆体系增强**（Issue #2046）— 用户提交了详细建议，核心诉求包括：将 session 标题/元数据持久化到文件系统供 Agent 读取、支持跨 session 历史对话的自动感知和检索。这项工作与另一批用户的深度分析（如 #2040 中提到的"记忆缺失"短板、#2041 中记忆系统的思考）相互呼应，建议维护者重点评估。[链接](https://github.com/netease-youdao/LobsterAI/issues/2046)

2. **增加 Hermes Agent 集成**（Issue #1880）— 用户期望参照 Open WebUI 的接入方式，将 Hermes Agent 与 OpenClaw 集成到 LobsterAI 中。[链接](https://github.com/netease-youdao/LobsterAI/issues/1880)

3. **增加 OpenHuman 引擎支持**（Issue #2016）— 用户建议集成 OpenHuman 引擎。[链接](https://github.com/netease-youdao/LobsterAI/issues/2016)

4. **UI 优化请求**（Issue #1836）— 用户反馈界面相比竞品"过丑"，建议进行专业设计重新美化。[链接](https://github.com/netease-youdao/LobsterAI/issues/1836)


## 用户反馈摘要

* **付费服务稳定性存疑**：Issue #1903 反映网易会员登录频繁失败，影响用户使用付费模型的能力。该问题持续 3 个月未解决，后续是否已通过其他渠道处理需进一步核实。

* **记忆缺失是核心痛点**：Issue #2046 的反馈指出，Agent 无法自动感知、检索、关联历史对话，"每个新对话 session 独立存在"，导致跨 session 使用中出现"大量信息丢失和重复劳动"。这与 Issue #2040/#2041 中用户对 OpenClaw"记忆缺失"和"记忆系统瓶颈"的分析形成一致。

* **配置同步破坏性较强**：PR #1879 揭示了配置同步机制会静默丢弃用户手动添加的插件路径，对依赖社区插件的用户有实际影响。

* **模型调用策略受限**：Issue #1988 反映模型调用时，阿里百炼 coding plan 的 qwen3.6-plus 会被强制路由到网易自带模型并提示无额度，修改配置文件也无法覆盖系统强制行为。


## 待处理积压

以下为长期未响应或未解决的重要 Issue，建议维护者优先关注：

1. **Issue #1903** `会员登录频繁失败` — 开放 3 个月+，影响付费用户体验，严重程度高。[链接](https://github.com/netease-youdao/LobsterAI/issues/1903)

2. **Issue #2046** `Agent 记忆体系产品建议` — 开放 2 个月+，包含详实的用户调研和功能建议，是重要的产品方向参考。[链接](https://github.com/netease-youdao/LobsterAI/issues/2046)

3. **PR #1879** `preserve manually-added plugin load paths` — 等待合并 3 个月+，修复社区插件路径丢失问题。[链接](https://github.com/netease-youdao/LobsterAI/pull/1879)

4. **PR #2234** `cron yield descendant finalization` — 修复 cron 场景下父子 agent 协作的关键问题，等待合并 1.5 个月+。[链接](https://github.com/netease-youdao/LobsterAI/pull/2234)

5. **Issue #1988** `qwen3.6-plus 强制路由到网易模型` — 已 stale 关闭，但模型可配置性问题属于核心功能缺陷，建议主动回查。[链接](https://github.com/netease-youdao/LobsterAI/issues/1988)

---

*本日报基于 GitHub 公开数据自动生成，数据截至 2026-08-16。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报

**日期：2026-08-16**  
**数据来源：** [moltis-org/moltis](https://github.com/moltis-org/moltis)  
**数据窗口：** 2026-08-15 至 2026-08-16


## 1. 今日速览

Moltis 项目今日整体保持高活跃度，过去 24 小时内有 6 条 PR 更新，其中 3 条已合并/关闭、3 条待合并，显示出稳定的开发节奏和良好的合并效率。当日无新 Issues 产生，也没有新版本发布，项目处于“功能快速累积、版本待整合”的冲刺阶段。值得关注的是，所有 PR 均由核心成员 penso 提交，覆盖 Coder 沙箱支持、Slack 任务卡片、OpenAI API 路由优化等多个方向，表明项目正在积极扩展外部集成能力并优化既有架构。


## 2. 版本发布

过去 24 小时内没有新的版本发布，暂无更新内容或迁移注意事项。


## 3. 项目进展

今日有 3 个 PR 完成合并/关闭，另有 3 个待合并，核心进展如下：

- **[#1196] 修复 ClawHub 技能搜索结果 [已合并]** — 解决了技能搜索中元数据请求导致的 RPC 超时问题，并通过所有者限定（owner-qualified）引用机制优化了技能详情的下载与安装流程。这是对技能市场功能的稳定性修复，直接改善用户搜索体验。
- **[#1197] 命令面板一键发起 Agent 对话 [已合并]** — 在命令面板中追加“Ask agent”快捷操作，创建新会话并立即发送查询，同时在全局聊天中捕获来源会话。这一交互改进降低了 Agent 功能的使用门槛，提升日常操作效率。
- **[#1198] OpenAI 推理工具调用路由至 Responses API [已合并]** — 当内置 OpenAI 请求同时携带函数工具与 `reasoning_effort` 时自动路由到 Responses API，而保持 Chat Completions 的既有行为不变。这是对模型供应商兼容性的架构级优化，为后续推理能力扩展铺路。

**尚未合并**的 3 个 PR 集中在 Coder 工作区支持（#1199）、日历/邮件/频道连接器（#1190）以及 Slack 原生任务卡片（#1195），分别对应远程开发环境、外部数据源接入和渠道交互三大方向。


## 4. 社区热点

过去 24 小时内各 PR 均未获得高密度讨论或评论，但以下 PR 因涉及外部服务集成而具有较高关注度：

- **[#1199] 添加 Coder 远程工作区沙箱支持** — 通过 Coder REST API 创建临时工作区，并通过 WebSocket 执行命令，支持模板、预设参数、TTL 等配置。该 PR 将 Moltis 从本地执行扩展至远程沙箱场景，对需要在隔离环境中运行 Agent 代码的用户具有吸引力。
- **[#1195] Slack 原生实时任务卡片** — 在 Slack 响应流中直接渲染任务卡片，并设计不透明会话 ID 以保护隐私。反映了用户对“在常用聊天工具中直接管理 Agent 任务”的诉求。

讨论热度不高可能与 PR 均由核心成员提交、评审流程以代码审查为主有关，但两个 PR 的外部集成属性值得注意。


## 5. Bug 与稳定性

- **[#1196] ClawHub 技能搜索超时问题 [已修复并合并]** — 原问题为：逐条请求技能元数据导致搜索请求超过 RPC 超时阈值，现已通过直接消费搜索元数据并将所有者限定引用贯穿全流程修复。由于该 PR 已在今日合并，问题应已得到解决。


## 6. 功能请求与路线图信号

当前无新 Issues 提交，但 3 个待合并的 PR（#1199、#1190、#1195）指向了明确的路线图信号：

- **远程/隔离执行环境**（#1199）：Coder 沙箱支持意味着 Moltis 将可部署于临时工作区，适配多云/零信任的开发场景。
- **外部数据源连接**（#1190）：日历（CalDAV）、邮件（Gmail/Himalaya）、频道历史等只读数据集的持久化与搜索能力，暗示项目正在构建“连接器生态”，并向更复杂的工作流自动化方向演进。
- **渠道内交互**（#1195）：Slack 原生任务卡片展示了与即时通讯工具深度整合的方向，后续可能推广至其它渠道。

上述 PR 若顺利合并，预计将成为下一版本的核心亮点。


## 7. 用户反馈摘要

过去 24 小时内无 Issues 评论可供提炼。从 PR 内容推断，用户侧的主要需求集中在：**更快的技能搜索体验**（#1196）、**更低的 Agent 使用门槛**（#1197）以及**与既有开发/协作工具链的无缝集成**（#1199、#1195）。


## 8. 待处理积压

以下 3 个重要 PR 正处于待合并状态，建议维护者关注评审进度：

- **[#1199] 添加 Coder 远程工作区沙箱支持**（opened 2026-08-15，last updated 2026-08-15）— 涉及沙箱后端的完整实现，包含配置与文档，属于较大规模的集成功能，建议尽快安排评审。
- **[#1190] 添加持久化的日历、频道与邮件连接器**（opened 2026-08-11，last updated 2026-08-15）— 已开放 5 天仍未合并，涉及连接器持久化与安全设计，可能因范围较大需要更多审查时间。
- **[#1195] 添加 Slack 原生实时任务卡片**（opened 2026-08-15，last updated 2026-08-15）— 与 UI/渠道层交互相关，建议与 #1199 一并规划评审优先级。

无长期未响应的 Issues 或 PR，项目积压管理健康。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-16

## 1. 今日速览

过去24小时 CoPaw 项目保持高活跃度：新增/活跃 Issues 9 条，新增 PR 11 条（全部待审查），0 个版本发布。值得关注的是，今日 Issue 全部集中在 `v2.1.0` 的功能缺陷与体验问题，呈现"高报告、高修复率"的状态——如 #7048 的 cron 更新 bug 已在同日收到对应 fix PR（#7055），#7059/#7060 的视频 tool-result 丢失缺陷也在当日有修复 PR（#7061）跟进。项目响应速度快，但社区积压 PR 达 11 条且零合并，审查吞吐存在瓶颈。长期未关闭的功能请求（如 #3915）仍在等待排期，社区潜在不满情绪可能积累。

## 2. 版本发布

无新版本发布（最新版本停留于 v2.1.0，2026-08-15 前发布）。

## 3. 项目进展

今日无 PR 被合并或关闭，但以下新提交的 PR 展示了项目正在推进的重点方向：

- **#7061** `fix(video): deliver tool-result videos on OpenAI Responses API` — 针对 #7059/#7060 的即时修复，解决 OpenAI Responses API（如 Volcengine Ark）下 `view_video` 工具结果静默丢失和死门控问题（由 #6495 引入）。
- **#7055** `fix(cli): sync top-level text on agent cron --text update (#7048)` — 修复 agent 类型 cron job 的 `--text` 参数静默失效问题。
- **#7057** `fix(shell): add user-local bin dirs to subprocess PATH` — 修复 QwenPaw 守护进程在 systemd/Docker 环境下子进程 PATH 不完整、无法找到用户级 CLI（如 `gh`、`cmake`）的问题。
- **#6940** `feat(pawapp): add native DataPaw app runtime and durable analysis workspace` — 引入 DataPaw 原生应用运行时与持久化分析工作区，属较大型功能推进。

另有 #7033（动态技能加载）、#6302（统一 provider 发现/路由）、#7001（Matrix 群组会话隔离）等仍在审查中的 PR 持续更新。

## 4. 社区热点

- **[#6476] Matrix 端到端加密不可用（已关闭）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/6476)
  3 条评论，8月15日最后更新后关闭。核心诉求：`matrix-nio` 依赖 olm 库但 QwenPaw 自动安装失败（系统层 `apt install libolm-dev` 成功、`uv pip install matrix-nio[e2e]` 成功但装的是 vodozemac 而非 olm），用户在讨论中给出了详细的三步安装排查记录。该 Issue 今日被关闭，推测已有有效 workaround（或维护者判断非内核缺陷）。
- **[#3915] Console WebUI 虚拟滚动支持（活跃 3.5 个月）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/3915)
  👍 1，创建于 4 月 28 日，今日仍有评论更新。长对话场景下全量 DOM 渲染导致严重卡顿，用户诉求为虚拟滚动或分页渲染。该 Issue 长期未关闭且无对应 PR，可能受 #7049（CHATS 分页 PR）部分覆盖但未完全解决。

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🔴 高 | [#7059](https://github.com/agentscope-ai/QwenPaw/issues/7059) | `view_video` 工具结果对模型完全不可见（无报错、静默失败），影响所有 OpenAI Responses API 系 provider | ✅ [#7061](https://github.com/agentscope-ai/QwenPaw/pull/7061) 已提交 |
| 🔴 高 | [#7060](https://github.com/agentscope-ai/QwenPaw/issues/7060) | `view_video` 内联文件大小硬编码 2MB，`max_inline_media_bytes` 设置对视频无效，大视频直接退化为纯文本占位符 | ✅ [#7061](https://github.com/agentscope-ai/QwenPaw/pull/7061) 已提交 |
| 🟠 中 | [#7053](https://github.com/agentscope-ai/QwenPaw/issues/7053) | OAuth2 刷新令牌不轮换 + 无主动续期，远程 MCP 服务器（如 XMind）永久降级至手动重新认证 | ❌ 无 |
| 🟠 中 | [#7048](https://github.com/agentscope-ai/QwenPaw/issues/7048) | `qwenpaw cron update --text` 返回成功但 prompt 实际未更新（agent 类型任务） | ✅ [#7055](https://github.com/agentscope-ai/QwenPaw/pull/7055) 已提交 |
| 🟠 中 | [#7051](https://github.com/agentscope-ai/QwenPaw/issues/7051) | Console 对话重开图片附件丢失（后端 data URL 与前端缩略图不同步） | ❌ 无 |
| 🟡 低 | [#6476](https://github.com/agentscope-ai/QwenPaw/issues/6476) | Matrix E2E 加密不可用（olm 依赖问题） | ✅ 今日已关闭 |

## 6. 功能请求与路线图信号

| 功能请求 | 对应 Issue | 对应 PR（若有） | 下版本纳入可能性 |
|---|---|---|---|
| 插件 API 增加 `system_prompt` 权限控制 | [#7052](https://github.com/agentscope-ai/QwenPaw/issues/7052) | ❌ 无 | 中等——企业级使用场景明确，实现成本低 |
| Web UI 恢复"原生上下文策略"选项 | [#7058](https://github.com/agentscope-ai/QwenPaw/issues/7058) | ❌ 无 | 高——后端仍支持 `native` 策略，仅缺 UI 入口 |
| 后台任务完成回调/通知机制 | [#7056](https://github.com/agentscope-ai/QwenPaw/issues/7056) | ❌ 无 | 中等——Webhook/通知基础设施需新增，但需求真实（当前需手动轮询） |
| `view_video` 最大内联文件大小可配置 + Files API | [#7060](https://github.com/agentscope-ai/QwenPaw/issues/7060) | ✅ 部分被 #7061 覆盖 | 高——已有 PR 基础，仅需扩展配置项 |
| CHATS 接口 limit/before 分页 | — | ✅ [#7049](https://github.com/agentscope-ai/QwenPaw/pull/7049) | 高——PR 已提交，预期较快合并 |

## 7. 用户反馈摘要

- **视频工具链体验是今日最大痛点**（#7059、#7060）：`view_video` 在两个路径上失败——静默丢弃或强制文本占位，用户无法区分"视频太大被忽略"与"视频正常加载但结果未送达"，排查成本高，直接影响模型多模态感知能力。
- **企业场景下对控制力的需求集中**（#7052、#7053）：插件侧希望隐藏系统提示词（不想让终端用户看到），远程 MCP OAuth 会话持续掉线需要频繁人工介入，说明当前身份与权限模型的颗粒度不足以支撑组织级部署。
- **CLI 与 UI 的一致性受质疑**（#7048、#7058）：`cron update --text` 返回成功但未生效、UI 移除 native 上下文策略入口，用户感觉"被静默降级"，反馈中带有明显不满情绪。
- **WebUI 长对话性能持续为社区长期未愈的痛点**（#3915）：虽已有 #7049 分页 PR，但该 Issue 已存活 3.5 个月，用户等待周期偏长。

## 8. 待处理积压

| 类型 | 编号 | 标题 | 存活时间 | 备注 |
|---|---|---|---|---|
| Issue | [#3915](https://github.com/agentscope-ai/QwenPaw/issues/3915) | Console WebUI 虚拟滚动 | ~3.5 个月 | 长期未关闭，虽有相关 PR 但仍需维护者明确排期或给出路线图反馈 |
| Issue | [#6476](https://github.com/agentscope-ai/QwenPaw/issues/6476) | Matrix E2E 加密不可用 | ~3 周 | 今日已关闭，建议在 Release 说明中确认修复方案 |
| PR | [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) | 统一 provider 发现、模型元数据与路由 | ~4 周 | 大型重构型 PR（跨 4 个子系统），需重点审查，长期处于 open 状态 |
| PR | [#6623](https://github.com/agentscope-ai/QwenPaw/pull/6623) | ACP 通知竞争条件修复 | ~2 周 | 已标记 "Under Review"，解决即时消息丢失问题，建议优先合并 |

---

> 📊 **项目健康度评估**：社区反馈回路通畅，bug 修复 PR 大多当天提交；但 PR 合并速度跟不上提交速度（11:0 待合并比例），长期停留的审查瓶颈若持续，可能拖慢 v2.2.0 的发布节奏。建议维护者优先安排 #7061、#7055 两个 bugfix PR 的合并，并考虑对 #6302 大型重构 PR 拆分为可独立合入的阶段。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是基于 ZeroClaw 开源项目 2026-08-16 日 GitHub 数据生成的动态日报。

---

## ZeroClaw 项目动态日报 — 2026-08-16

### 1. 今日速览

ZeroClaw 项目今日维护活动活跃，**积压的 RFC 与设计讨论成为核心焦点**。虽然新版本发布为0，但共有 50 条 Issue 和 50 条 PR 产生更新，表明项目正处于密集的设计决策与代码审查期。社区讨论集中在四个高优先级 RFC 上（OpenAI 兼容性、运行时会话所有权、附件架构、内部触发对话），这些讨论将决定项目下一阶段的架构方向。此外，多项 P1 级别的 Bug 修复 PR（如 Cron 任务卡死、配置风险模型）仍在等待作者响应或维护者合并。项目整体健康度良好，但维护者需加速处理决策队列以推动关键特性落地。

---

### 2. 版本发布

无新版本 Release。

---

### 3. 项目进展

今日有 4 个 Issue 被关闭，6 个 PR 被合并/关闭（其中 4 个为合并）。主要进展集中在 **Anthropic 提供商可靠性** 和 **SOP 能力**方面。

- **Anthropic 服务器端回退功能合入 (`#9262`, `#9263`, `#9265`, `#9266`)**：这是一个由 4 个 PR 组成的堆叠合并，标志着 ZeroClaw 对 Anthropic 大模型回退机制的完整支持。
    - **PR #9262** 将 Anthropic 的安全拒绝（HTTP 200 + `stop_reason: "refusal"`）识别为类型化错误，而非空成功。
    - **PR #9263** 在客户端可靠性层上，将上述类型化错误路由至客户端回退条目，实现自动重试切换。
    - **PR #9265** 增加了对 Anthropic **服务器端**回退的客户端选择开关（`server_fallback_models` 配置项）。
    - **PR #9266** 实现了解析服务器端回退的响应信号（实际服务模型和迭代次数），并将其传递给上层。
    - **PR #9268** 作为该堆栈的最后一块，在频道编排器中向用户展示安全回退通知。
    - **综合影响**：这一系列合并显著增强了 Anthropic 服务的稳定性与用户体验，确保了在模型拒绝或服务降级时，对话能够通过备用模型继续，且用户能获知实际情况。这直接响应了社区对“可靠提供者”的诉求。

---

### 4. 社区热点

今日讨论最激烈的 Issue 无疑是对项目架构产生深远影响的 **RFC 提案**。评论数最高的 Top 3 均为开放中的 RFC，且更新日期都在昨日或今日，说明讨论仍在持续。

- **#8603 [RFC] ZeroClaw Chat Completions profile (评论: 20)**
    - **链接**: [Issue #8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) (请替换为完整 URL)
    - **诉求**: 社区对使用标准 OpenAI Chat Completions 协议连接 ZeroClaw 的呼声很高。该 RFC 旨在让 Open WebUI、LobeChat、Continue.dev 等主流客户端能零成本接入 ZeroClaw。
    - **分析**: 这是增加项目互操作性和用户基础的关键需求。评论数最高表明该功能是社区的强力诉求，但 `needs-maintainer-review` 标签说明等待维护者定夺。

- **#9487 [RFC] Runtime-owned conversation sessions and transport surface adapters (评论: 17)**
    - **链接**: [Issue #9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) (请替换为完整 URL)
    - **诉求**: 重新定义运行时与会话的生命周期所有权，并通过传输适配器统一 WebSocket、ACP 等不同入口的会话管理。
    - **分析**: 这是核心架构层面的重构提案，涉及安全问题（`security`标签）和高风险（`risk:high`），是**长期演进的核心讨论**。评论活跃度高说明维护者与贡献者在深入磨合边界情况。

- **#9488 [RFC] Unified attachment architecture for web chat and channels (评论: 16)**
    - **链接**: [Issue #9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488) (请替换为完整 URL)
    - **诉求**: 统一 Web 和各大频道（Channel）的附件上传、存储与分发架构，解决各渠道处理不一致问题。
    - **分析**: 此 RFC 与 #9487 同属一个系列的架构升级，旨在解决数据处理的碎片化现状。评论数与其关联性相符。

---

### 5. Bug 与稳定性

今日报告和进行中的 Bug 中，有 3 个 P1（高优先级）问题值得关注，均已有 fix PR，但部分处于阻塞状态。

- **[P1] Cron 任务可能卡死 (Issue #9320)**
    - **链接**: [Issue #9320 (PR)](https://github.com/zeroclaw-labs/zeroclaw/pull/9320) (请替换为完整 URL)
    - **状态**: 已有修复 PR（`fix(cron): bound agent job runs with a wall-clock timeout`）。
    - **详情**: 若无超时机制，Cron 任务可能因 Provider 无响应或工具卡死，导致任务锁无法释放，后续任务永久阻断。**PR 目前需要作者行动（`needs-author-action`），阻塞中。**

- **[P1] macOS 桌面应用窗口空白 (Issue #7527)**
    - **链接**: [Issue #7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) (请替换为完整 URL)
    - **状态**: 已关闭（原因非Bug，可能为重复或用户操作问题，文中提及 `needs-repro`）。
    - **详情**: 用户报告在 macOS 15.7.7 上安装后无法检测权限，应用无响应且重启后窗口消失。该 Issue 已关闭，但若为误报关闭，则可能存在未暴露的兼容性问题。

- **[P1] 测试环境存在竞态条件 (Issue #9965)**
    - **链接**: [Issue #9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965) (请替换为完整 URL)
    - **状态**: 已接受的 Task（`status:accepted`）。
    - **详情**: `cron custom-shell` 测试在并行运行时触发 `ETXTBSY` 错误，导致无关 PR 的 CI 检查失败（红点）。这属于**影响开发者体验的基建问题**，需要重构测试以消除竞态。

---

### 6. 功能请求与路线图信号

社区诉求与项目路线图的交汇点集中在 **扩展接入方式** 与 **增强人机交互（HITL）** 上。

- **OpenAI 兼容层 (Issue #8603)**：如前所述，这是呼声最高的功能。鉴于评论热度，预计维护者会优先推进或将其纳入下一里程碑。
- **实时语音通道 (Issue #8780)**：该 RFC 计划支持 Gemini Live 的实时语音对话，并重写为代理（broker）契约。这是一个前沿的、高风险的特性请求。与现有的 “Speak-to-Speak” 路线图信号一致，但可能距离实际发布仍有距离。
- **Agent Plugins 1.0 标准支持 (Issue #9810)**：加载 `plugin.json + skills/` 的行业标准插件包。这表明项目有意构建更丰富的第三方生态，目前处于提案阶段，`needs-author-action`，等待作者补充信息。
- **AI 辅助 PR 审查 (Issue #9330)**：作为 `enhancement` 目标，利用 CI 结果触发 AI 初审，人工拥有最终审批权。该提案旨在缓解维护者审查压力，并已被标记为 `needs-author-action`。

---

### 7. 用户反馈摘要

- **对互操作性的强烈需求**: 用户在 **#8603** 中明确表达了希望使用 ChatGPT 类客户端（如 Open WebUI, LobeChat）连接 ZeroClaw 的需求，这直接反映了用户希望将 ZeroClaw 融入现有 AI 工具链的痛点。
- **Cron 功能可用性差**: 用户 touhidurrr 在 **#7762** 中抱怨 Cron 功能两个核心问题：**文档完全缺失**，以及**无法为不同的 Cron 任务指定不同的模型**（例如使用便宜的模型执行任务），这增加了使用成本与操作门槛。
- **对误报的困扰**: 用户在 **#9825** 中指出，安全机制（泄漏检测器）因高熵启发式算法误伤公开的区块链地址，导致付款链接无法发送。这反馈了**安全策略过于激进会牺牲功能可用性**的平衡问题。
- **桌面端体验不佳**: 用户 swellee 在 **#7527** 中报告了 macOS 桌面应用严重卡顿和窗口丢失的问题，虽已关闭，但 S1（工作流阻断）的严重度表明**桌面端的稳定性仍是需要持续关注的薄弱环节**。

---

### 8. 待处理积压

以下 Issue 或 PR 长期处于活跃但未决状态，建议维护者关注，以推动决策或清理。

- **#8692 [Tracker] Maintainer decision queue for RFCs** (更新于 08-15)
    - **链接**: [Issue #8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) (请替换为完整 URL)
    - **风险**: 这是一个维护者决策的**总管跟踪器**，积压了众多 RFC 的设计决策。当前大量 RFC（如 #6954, #6971, #9103）都在等待 `needs-maintainer-review` 或 `needs-author-action`。该队列的堵塞是项目推进的最大风险，**建议维护者优先处理队列中的高讨论量 RFC**，以明确方向，释放贡献者生产力。

- **#7108 [CI] improve cached Rust builds** (更新于 08-15)
    - **链接**: [Issue #7108](https://github.com/zeroclaw-labs/zeroclaw/issues/7108) (请替换为完整 URL)
    - **风险**: 中等——虽然已有 `status:accepted`，但过去 3 个月无实质推进。与此相关的 **#7126** (forbid unsafe_code) 也处于同样状态。这表明 CI 优化和代码安全强化方面的进展缓慢。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*