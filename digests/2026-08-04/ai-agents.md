# OpenClaw 生态日报 2026-08-04

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-04 01:16 UTC

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

好的，这是 2026 年 8 月 4 日的 OpenClaw 项目动态日报。

---

# OpenClaw 项目日报 - 2026-08-04

## 1. 今日速览

OpenClaw 项目今日活跃度极高，过去 24 小时内共有 500 条 Issue 和 500 条 PR 更新，显示出庞大的社区基础和强烈的使用反馈。尽管合入/关闭率为 33.6%（168/500），略低于待合并数量，但 P0/P1 级别的严重 Bug（如 #103804，服务环境变量生成器破坏 AWS 配置）已由社区提交修复 PR，且长期存在的会话状态丢失（#44925, #116277）和消息截断问题（#84516）持续发酵，成为社区关注焦点。整体来看，项目处于快速迭代期，但在会话状态管理和消息传递可靠性方面面临较大稳定性压力。

## 2. 版本发布

今日发布了两个补丁版本，均无破坏性变更，建议升级：

- **v2026.7.1-2**
  - **修复**: 更新了 npm 插件更新机制，以兼容新版 npm 客户端返回的单例数组元数据，确保官方插件可以正确安装和更新至修订版。 (#108336)
- **v2026.7.1-1**
  - **修复**: 修复了 Codex 进度回复问题。现在应用服务器在发送进度消息后会保持运行，直到 GPT/Codex 生成权威的最终回复，而不是中途停止。 (#106961, #108487)
  - **修复**: 修复了 Memory Core 的启动修复问题，可以恢复派生的旧版索引和缓存。

**迁移建议**: 无特殊操作，常规升级即可。

## 3. 项目进展

今日无大型功能 PR 被合并，主要进展集中在 QA 测试覆盖和特定问题修复上，表明项目当前重心在于稳固既有功能。

- **QA 测试体系扩展**: 维护者 `vincentkoc` 提交了多个 PR，旨在为 Gateway 的更新和设置 RPC (#118813)、代理会话流 (#119028)、代理会话作用域连续性 (#119032) 以及实时搜索连续性 (#119031) 添加主要场景的 QA 覆盖。这表明项目正在系统性地构建产品级验证体系。
- **Telegram 长轮询修复**: PR #119037 修复了 Telegram `getUpdates` 长轮询在特定情况下会卡住 150-184 秒，远超预期 45 秒超时的问题。此修复通过将请求截止时间绑定到 body 读取，有望解决消息投递延迟问题。
- **Slack 线程上下文修复**: PR #119023 修复了在 Slack 中，当智能体开启回复线程时，用户可能丢失原始频道上下文的问题，确保了会话路由的正确性。

## 4. 社区热点

今日最热门的讨论集中在**消息丢失**和**会话状态管理**上，这已成为影响用户的核心痛点。

- **#116277 [已关闭] DeepSeek v4 Flash 静默回复失败** (评论: 100)
  - **链接**: [Issue #116277](https://github.com/openclaw/openclaw/issues/116277)
  - **诉求**: 模型（deepseek-v4-flash）在收到消息后静默失败，未生成任何回复，只向用户发送了"未生成回复"的通用提示。100 条评论表明该问题影响范围广，用户对于"静默失败"这种缺乏错误反馈的体验非常不满。

- **#116201 [开启] 实时语音工作可保留无限制的 Provider 和咨询状态** (评论: 50)
  - **链接**: [Issue #116201](https://github.com/openclaw/openclaw/issues/116201)
  - **诉求**: 实时语音会话存在资源限制问题，在慢速或突发性的 Provider/客户端行为下，会保留已废弃的咨询工作、大型 Provider 帧和未就绪的音频，缺乏硬性所有权界限。社区在探讨如何为这些资源设置硬性上限以防止内存泄漏。

- **#7707 [开启] 功能请求：按来源进行记忆信任标记** (评论: 24)
  - **链接**: [Issue #7707](https://github.com/openclaw/openclaw/issues/7707)
  - **诉求**: 用户希望根据记忆来源（用户指令、网页抓取、第三方技能）标记信任级别，以防止记忆投毒攻击。这是一个长期存在的安全需求，社区讨论热烈。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在会话状态丢失和消息传递可靠性上，多数为长期存在的 P1 问题。

**严重等级: P0**

- **[Bug]: service-env generator double-quotes values, breaking AWS_REGION hostname** (#103804)
  - **链接**: [Issue #103804](https://github.com/openclaw/openclaw/issues/103804)
  - **状态**: 开启，已有 PR #108979 待合入。
  - **详情**: 网关服务环境文件序列化器使用双引号和单引号包裹值，导致 AWS_REGION 等配置变为 `'"us-east-1"'`，被 shell 解析为字面量，破坏所有依赖 AWS 的部署。这是一个影响面极广的发布阻断问题。

**严重等级: P1**

- **[Bug]: DeepSeek v4 Flash silently fails to generate reply** (#116277)
  - **链接**: [Issue #116277](https://github.com/openclaw/openclaw/issues/116277)
  - **状态**: 已关闭（可能是重复或已在某处修复），但引发了大量讨论。
- **[Bug]: Realtime voice work can retain unbounded provider and consult state** (#116201)
  - **链接**: [Issue #116201](https://github.com/openclaw/openclaw/issues/116201)
  - **状态**: 开启，无修复 PR。
- **[Bug]: Subagent completion silently lost** (#44925)
  - **链接**: [Issue #44925](https://github.com/openclaw/openclaw/issues/44925)
  - **状态**: 开启，无修复 PR。这是4月报告的旧问题，至今未解决，社区已表达不满。
- **[Bug]: Codex-backed Telegram turns repeatedly time out** (#87744)
  - **链接**: [Issue #87744](https://github.com/openclaw/openclaw/issues/87744)
  - **状态**: 开启，无修复 PR。该问题与 v2026.7.1-1 修复的问题相关，但报告者仍在使用旧版本。
- **[Bug]: Codex app-server: long agent replies silently truncated** (#84516)
  - **链接**: [Issue #84516](https://github.com/openclaw/openclaw/issues/84516)
  - **状态**: 开启，无修复 PR。GPT-5.5 的长回复在约 1000-1100 字符处被静默截断，且无任何错误标记。

## 6. 功能请求与路线图信号

今日新增的功能请求较少，更多是既有请求的持续讨论。以下请求值得关注：

- **[Feature]: Memory Trust Tagging by Source** (#7707) - 社区呼声高，对于防范提示注入攻击至关重要，建议纳入安全路线图。
- **[Feature]: Self-hosted STT/TTS provider support in webchat** (#45508) - 用户希望 webchat 能够使用自托管的语音服务，而不是浏览器内置 API，以保护隐私并集成现有基础设施。
- **[Feature]: Add MathJax/LaTeX Support to Control UI** (#42840) - 该请求获得 10 个 👍，显示用户对科学公式展示有明确需求。

**路线图信号**: 维护者 `vincentkoc` 今日提交了多个仅用于 QA 覆盖的 PR，而 `nicknmorty` 的两个 PR (Redact exec tool result payloads #81185, 和 fix(codex) #94299) 正在等待作者更新。这表明维护者正在优先夯实稳定性，而非开发新功能。

## 7. 用户反馈摘要

- **稳定性痛点**: 用户对"静默失败"模式（模型不回复、消息被截断、子任务结果丢失）表达了强烈不满，认为这类问题严重破坏了用户体验和信任度。典型评论集中在 #116277、#44925 等 Issue。
- **配置与部署困扰**: 用户报告了 Windows 原生网关计划任务无法保持运行 (#91144) 以及 `OPENCLAW_HOME` 环境变量导致嵌套目录问题 (#45765)，这表明在不同平台上的部署和配置体验仍有待优化。
- **对项目的高度认可**: 在功能请求 #73537 中，用户明确表示 "Thank you for OpenClaw"，并分享其作为家庭和商业助手（Telegram 集成、自动化、Home Assistant 控制）的积极使用体验。这表明项目在核心功能上仍有很强的用户粘性。

## 8. 待处理积压

以下为长期未解决或被标记为需要维护者关注的重要问题，提醒维护团队优先处理：

- **P0 服务环境配置损坏**: [Issue #103804](https://github.com/openclaw/openclaw/issues/103804)，已有 PR #108979，需尽快评审合入。
- **P1 子代理结果静默丢失**: [Issue #44925](https://github.com/openclaw/openclaw/issues/44925)（自3月报告）和 [Issue #67777](https://github.com/openclaw/openclaw/issues/67777)。这组问题涉及核心的会话编排稳定性，虽有 PR 关联但均未关闭。
- **P1 回复文本静默截断**: [Issue #84516](https://github.com/openclaw/openclaw/issues/84516)，影响 Codex/OAuth 代理的长回复，目前无修复 PR。
- **P1 会话状态卡死**: [Issue #52249](https://github.com/openclaw/openclaw/issues/52249)（ACP 父子会话）和 [Issue #54488](https://github.com/openclaw/openclaw/issues/54488)（会话通道饥饿）。这些问题会导致用户必须手动刷新或等待20-30分钟才能继续对话。
- **长期安全功能请求**: [Issue #40786](https://github.com/openclaw/openclaw/issues/40786)（备份排除模式）和 [Issue #44134](https://github.com/openclaw/openclaw/issues/44134)（Google 反滥用误报）。前者涉及数据安全，后者可能导致用户账号被封禁。

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向分析报告

**报告日期**: 2026-08-04  
**覆盖项目**: OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw, NullClaw, IronClaw, LobsterAI, Moltis, CoPaw, ZeroClaw  
**无活动项目**: TinyClaw, ZeptoClaw

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从“功能堆叠”向“架构规范化与稳定性优先”转型的关键阶段**。头部项目（OpenClaw、IronClaw、ZeroClaw）在经历大规模功能迭代后，开始系统性构建 QA 测试体系、强化安全边界（凭证管理、审批授权、审计真实性）；同时，**会话状态管理与消息传递可靠性已成为所有项目的共性核心痛点**——从 OpenClaw 的静默失败、Hermes 的 Telegram 挂起、NanoClaw 的会话不可用，到 CoPaw 的 shell 超时绕过，跨项目高度一致地暴露了“智能体长期运行稳定性”这一尚未解决的根本挑战。生态整体活跃度极高（仅 11 个活跃项目单日合计约 230+ Issue 更新、680+ PR 更新），但维护者评审带宽普遍成为瓶颈，多项目出现 PR 积压与 RFC 决策延迟。

---

## 2. 各项目活跃度对比

| 项目 | Issues | PRs | Release | 合并/关闭率 | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | v2026.7.1-1/-2 | 33.6% (168/500) | 🟡 高速迭代，P0/P1 稳定性压力大 |
| **NanoBot** | 2 | 36 | 无 | 69% (25/36) | 🟢 健康，修复类 PR 占比高 |
| **Hermes Agent** | 50 | 50 | v0.20.0 (8/3) | 8% (4/50) | 🟡 发布后高压期，回归问题多 |
| **PicoClaw** | 8 | 6 | 无 | 50% (3/6) | 🟢 健康，Issue 闭环率高 |
| **NanoClaw** | 1 | 9 | 无 | 67% (6/9) | 🟢 健康，外部贡献者活跃 |
| **NullClaw** | 1 | 5 | 无 | 40% (2/5) | 🟢 正常，有长期未决 Bug |
| **IronClaw** | 45 | 50 | 无 | 36% (18/50) | 🟡 架构重构期，CI 阻塞明显 |
| **LobsterAI** | 2 | 11 | 无 | 55% (6/11) | 🟡 正常迭代，4 个月 PR 积压 |
| **Moltis** | 0 | 1 | 无 | 0% (0/1) | 🔵 低活跃，单一大型 PR 推进 |
| **CoPaw** | 22 | 50 | v2.1.0-beta.1 | — | 🟡 Beta 前密集修复，兼容性风险 |
| **ZeroClaw** | 50 | 50 | 无 | 6% (3/50) | 🟡 架构收敛期，安全加固密集 |
| **TinyClaw** | — | — | — | — | ⚪ 无活动 |
| **ZeptoClaw** | — | — | — | — | ⚪ 无活动 |

---

## 3. OpenClaw 在生态中的定位

**社区规模碾压级领先。** OpenClaw 单日 500 Issue + 500 PR 的流量是第二梯队（Hermes、IronClaw、ZeroClaw 的 50/50）的 10 倍，是长尾项目（NanoBot 2/36、PicoClaw 8/6）的百倍量级，体现出**事实标准**的社区地位。

**技术路线差异——全家桶 vs 模块化：**
- **OpenClaw** 走“一体化全家桶”路线，整合记忆系统（Memory Core）、多网关（Telegram/Slack/Discord）、Codex 代理、实时语音等全栈能力，追求“开箱即用的完整个人 AI 助手”。
- **Hermes Agent** 同样有企业级野心（v0.20 含 3,650 commits、650+ 贡献者），但更侧重多路复用网关、Profile 隔离、生命周期钩子等**企业级隔离与可观测性**。
- **NanoBot** 选择“轻量个人助手”路线，2 人核心维护（chengyongru + 社区），聚焦 WebUI 体验与 Provider 兼容性，以**极简主义**取胜。
- **IronClaw** 则是**架构激进派**，当前 Wave 3 重构（WS2/WS3）正在大规模模块化（loop_host、模型网关下沉），目标指向更彻底的组件化架构。

**核心竞争优势**：生态规模带来的插件/技能生态丰富度 + 多平台消息适配的广度 + 社区反馈驱动的快速迭代。**核心劣势**：与体积相伴的稳定性压力（P0 AWS 配置破坏、会话静默丢失），以及会话状态管理在超大规模下的可靠性挑战。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **会话状态持久化与恢复** | OpenClaw (#44925/#116277, 静默失败)、NanoClaw (#3184/#3183, transcript 丢失/冷会话回收)、Hermes (#71322, /resume 阻塞)、PicoClaw (#3301, 路由后记忆丢失)、CoPaw (#6608, 超时绕过阻塞会话) | 会话中断后无法优雅恢复、上下文丢失、消息静默失败，是**全生态最集中痛点** |
| **消息传递可靠性** | OpenClaw (#84516, 截断)、Hermes (#67498/#78052/#72454, Telegram 挂起三连)、CoPaw (#6614, 微信推送假成功)、ZeroClaw (#9718, 重复消息)、IronClaw (#7072, Markdown 渲染) | 跨渠道（Telegram/微信/飞书/Matrix）的消息投递可靠性与格式正确性普遍存在缺陷 |
| **敏感凭证安全与密钥管理** | OpenClaw (#103804, AWS 配置破坏)、ZeroClaw (#1, XOR 加密失效 171 天)、Hermes (#60551, config.yaml 写入矛盾)、IronClaw (#7041, WASM 密钥泄露)、NullClaw (#983, 凭据 argv 暴露)、Moltis (#1183, vault 集成) | 配置生成器破坏性 Bug、密钥存储加密强度不足、凭据暴露风险跨项目集中出现 |
| **工具调用权限与审批安全** | ZeroClaw (#9574, 审批授权/#9642, 审计伪造)、CoPaw (#6612, 工具权限死锁)、Hermes (#68559, profile 隔离失效) | 审批机制的身份绑定、审计真实性、权限边界隔离成为安全焦点 |
| **MCP 生态集成与生命周期** | Moltis (#1183, 受管仓库)、NanoClaw (#3092, 远程 MCP 16 天待合并)、IronClaw (#7024, 自定义认证)、PicoClaw (#3269, MCP 失败挂起) | MCP 服务器从“单点接入”走向“生命周期管理”（发现/安装/回滚/认证） |
| **模型自动降级/fallback** | CoPaw (#6659/#2199, 冷却机制)、OpenClaw (Codex 进度回复)、Hermes (provider 兼容性) | 面对 Provider 故障时的自动恢复与降级策略，是生产级 Agent 的刚需 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 全栈个人助手（多网关+记忆+语音+Codex） | 大众用户/技术爱好者，追求开箱即用 | 一体化 monorepo，Memory Core 独立子系统 |
| **Hermes Agent** | 企业级多路复用网关 + Profile 隔离 | 企业/团队，多平台统一接入 | 多路复用网关路由，生命周期钩子，强调可观测性 |
| **NanoBot** | 轻量个人助手，WebUI 极致打磨 | 个人开发者，重 UI 体验 | 极简依赖，Provider 兼容层（Responses/API 双模式） |
| **IronClaw** | 组件化架构 Agent + NEAR AI 生态 | 架构敏感型开发者 | Wave 3 大规模模块化重构（WS2/WS3），Rust 技术栈 |
| **ZeroClaw** | 安全加固 + 架构规范化的通用 Agent | 安全意识强的开发者/企业 | 高风险 RFC 驱动，v0.9.0 安全强化路线 |
| **CoPaw** | 多智能体协作 + 桌面客户端 | 网易生态用户/多智能体场景 | agentscope 框架集成，桌面 WebView2 外壳 |
| **PicoClaw** | 轻量网关 + 路由代理 | 自部署用户 | 类似 OpenClaw 但轻量化，偏嵌入式场景 |
| **NanoClaw** | 简单易用的 iMessage/频道接入 | Apple 生态用户 | 镜像硬化，iMessage 频道优先 |
| **NullClaw** | 自托管 + 本地 LLM 优先 | 隐私敏感用户 | Ollama 优先，curl 安全传输链路 |
| **LobsterAI** | Windows 桌面 + 网易云服务 | 网易用户群 | Electron 桌面，NSIS 安装器，商业化集成 |
| **Moltis** | MCP 托管管理 | MCP 生态开发者 | 专注 MCP 仓库/生命周期，vault 集成 |

---

## 6. 社区热度与成熟度分层

### 第一梯队：超大规模迭代期（单日 100+ Issue/PR）
- **OpenClaw** — 生态核心，迭代速度与稳定性压力并存，处于“功能高速扩张+稳定性债务积累”阶段
- **Hermes Agent** — 刚发布 v0.20 里程碑，处于“发布后热修复+社区验证”高峰期
- **IronClaw / ZeroClaw** — 架构重构/安全加固的密集执行期，CI 与评审带宽是瓶颈

### 第二梯队：稳步迭代期（单日 10-50 Issue/PR）
- **CoPaw** — Beta 前密集修复，功能与稳定性并重
- **NanoBot** — 质量巩固+功能累积并行，合并效率高（69%），健康度最佳
- **PicoClaw** — 中小型项目中的优秀范例（Issue 闭环率高、响应快）
- **NanoClaw** — 依赖核心团队+外部贡献者双轮驱动

### 第三梯队：低活跃/专注期（单日 <10 Issue/PR）
- **LobsterAI** — 正常迭代但有 4 个月 PR 积压
- **NullClaw / Moltis** — 单一大型 PR 推进或维护者评审周期

### 特别关注
- **TinyClaw / ZeptoClaw** — 当日无活动，需关注是否处于停摆或休眠状态

---

## 7. 值得关注的趋势信号

### 信号 1：会话生命周期管理是“未解决的圣杯”
从 OpenClaw 的 `#44925`（子代理结果静默丢失）到 NanoClaw 的 `#3183`（冷会话回收）、Hermes 的 `/resume` 阻塞——**所有项目都在同一问题上挣扎**：Agent 的长期运行稳定性。这不是单一 Bug，而是架构级挑战——需要会话持久化标准、优雅恢复机制、可观测的失败反馈。**对开发者的启示**：若能在这一方向做出突破（如标准化的会话恢复协议），将具备巨大的生态差异化空间。

### 信号 2：安全审计真实性与密钥管理成为新焦点
ZeroClaw `#9642`（审批超时被记录为拒绝，伪造审计轨迹）、`#1`（XOR 加密悬置 171 天）、OpenClaw `#103804`（配置破坏 AWS）——**安全不再只是“功能”而是“信任基础”**。审计日志的不可否认性、密钥存储的真实加密强度、配置生成器的正确性，正在成为生产级 Agent 的分水岭。

### 信号 3：MCP 从“接入”走向“管理”
Moltis 的受管仓库 PR、NanoClaw 的远程 MCP 请求、IronClaw 的自定义认证——MCP 生态正在经历从“能连就行”到“可管理、可回滚、可认证”的规范化过程。**对开发者的启示**：MCP 管理工具链（类似包管理器的体验）可能是下一代基础设施机会。

### 信号 4：跨项目 PR 积压成为普遍瓶颈
从 Hermes（46/50 待合并）到 ZeroClaw（47/50 待合并）、LobsterAI（4 个月积压）——**维护者评审带宽是当前生态最大的单点瓶颈**。社区贡献者（如 IronClaw 的 BenKurrek、ZeroClaw 的 Audacity88）表现出极高的产出质量与热情，但大量 P1 安全修复和完整实现的功能 PR 长期滞留，可能导致贡献者流失。

### 信号 5：“功能存在但不可发现”是常见体验陷阱
CoPaw `#6621`（用户 50+ 轮对话后才发现多智能体需在 PROFILE.md 显式配置）、IronClaw `#7044`（新用户面对空白 WebUI 无从下手）——**AI Agent 的能力再强，若用户不知道如何触发，也是零**。这指向“对话即配置”（IronClaw #7046）和引导式 OOBE 的下一波体验创新方向。

### 信号 6：供应商标配兼容性从“硬编码名单”走向“动态适配”
NanoBot `#5235`（Opus 5 因硬编码名单未更新被拒）、CoPaw `#6612/#6619`（agentscope 版本升级致崩溃）——模型 Provider 的发布节奏远超项目适配速度，**硬编码模型特性名单的模式正在破产**，动态获取模型能力描述/特性配置将是必然方向。

---

**结论**：个人 AI 助手/自主智能体开源生态正处于从“能做”到“能稳定做”的关键转折期。OpenClaw 凭借规模建立了生态位，但所有项目共同面临的会话稳定性、安全真实性与评审带宽问题，将是下一个阶段决定谁能从“可用”走向“可信”的核心竞争点。对于技术决策者，选择项目时建议优先评估其在会话恢复、安全审计与 MCP 管理三个维度的成熟度；对于开发者，上述共性痛点即是最大的贡献机会。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期：2026-08-04** | **数据窗口：2026-08-03 至 2026-08-04**


## 1. 今日速览

NanoBot 项目今日保持高活跃度，24小时内产生 2 条 Issue 更新和 36 条 PR 更新，其中 25 条 PR 已合并或关闭，项目合并效率较高（约 69%）。核心贡献者 chengyongru 集中处理了 WebUI 多项体验优化（i18n 审计、IME 输入稳定性、移动端键盘），arcdrake22 和 santhreal 分别围绕 provider 兼容性和边界条件修复提交了多项补丁。新功能方面，Mattermost 线程独立群组策略、mst-python 元搜索 provider 集成、跨会话搜索与 @ 提及等 PR 均处于待合并状态，值得关注。当前无新版本发布，项目处于功能累积与稳定性修复并行的迭代阶段。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日共合并/关闭 25 条 PR，核心进展集中在以下几个方面：

**WebUI 体验打磨（chengyongru 连提 4 条，全部合并）**

| PR | 内容 | 影响 |
|---|---|---|
| [#5227](https://github.com/HKUDS/nanobot/pull/5227) | 完成 WebUI 全面 i18n 审计，修正简体/繁体中文术语（`网页` → `网络`） | 提升多语言一致性 |
| [#5228](https://github.com/HKUDS/nanobot/pull/5228) | 本地触发器现在展示实际收到的触发消息 | 会话弹窗信息更透明 |
| [#5229](https://github.com/HKUDS/nanobot/pull/5229) | IME（中文输入法）输入期间不触发 textarea 自适应高度 | 修复中文输入时线程抖动 |
| [#5226](https://github.com/HKUDS/nanobot/pull/5226) | 触摸设备发送后自动收起移动端虚拟键盘 | 移动端体验优化 |

**Provider 层稳定性**

- [#5214](https://github.com/HKUDS/nanobot/pull/5214) — 修复 DeepSeek 经 Responses API 路由时 reasoning 内容因 serde 反序列化失败导致请求被拒的问题（P1）

**Gateway 与资源管理**

- [#5215](https://github.com/HKUDS/nanobot/pull/5215) — 修复 gateway 停止时 exec 会话或 MCP 子进程未清理导致的 asyncio 事件循环关闭异常（P1）

**插件系统与文档**

- [#5213](https://github.com/HKUDS/nanobot/pull/5213) — `uv tool` 环境中无 pip 时自动改用 uv 安装插件依赖
- [#5038](https://github.com/HKUDS/nanobot/pull/5038) — 新增 ModelScope（魔搭）provider 文档，含可复制 JSON 配置

**其他合并项**：cron 表达式语法预校验（[#5141](https://github.com/HKUDS/nanobot/pull/5141)）、Eden AI provider 接入（[#4861](https://github.com/HKUDS/nanobot/pull/4861)）、history.jsonl 尾部读取对非法 UTF-8 的容错（[#5221](https://github.com/HKUDS/nanobot/pull/5221)）、openai_codex 双模式支持（[#1550](https://github.com/HKUDS/nanobot/pull/1550)，从 3 月搁置至今终于合并）。

> 综合来看，项目今日在 WebUI 细节体验、provider 兼容性、资源生命周期管理三个方向均有实质性推进，且修复类 PR 占比较高，项目健康度良好。


## 4. 社区热点

今日无高讨论量热点（所有 Issue 评论数均为 0）。值得关注的 PR 按功能重要性排序：

- **[#5234](https://github.com/HKUDS/nanobot/pull/5234) — 集成 mst-python 元搜索 provider（P1，OPEN）**：聚合 DuckDuckGo、Google、Brave、Bing 等搜索引擎结果，通过 Reciprocal Rank Fusion 融合排序。搜索覆盖度是用户常见诉求，此 PR 若合入将显著提升 agent 检索能力，建议关注后续评审进展。

- **[#5233](https://github.com/HKUDS/nanobot/pull/5233) / [#5232](https://github.com/HKUDS/nanobot/pull/5232) — Mattermost 线程独立群组策略（OPEN）**：同一功能的一对孪生 PR（一个打开、一个关闭）。允许主频道与线程设置不同的 @ 提及策略，对 Mattermost 深度用户属刚需。

- **[#5211](https://github.com/HKUDS/nanobot/pull/5211) — 跨会话搜索与 @ 提及（OPEN）**：让 WebUI 用户可从 @ 面板选择历史会话，实现跨会话引用，进一步扩展会话上下文能力。

> 综合判断，社区当前关注点集中在 **搜索能力增强** 和 **渠道细化配置** 两个方向，均来自真实用户场景（信息检索深度、团队协作精细管控）。


## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | 说明 |
|---|---|---|---|
| 🔴 高 | [#5235](https://github.com/HKUDS/nanobot/issues/5235) — Anthropic Opus 5 请求因 `omit_temperature` 子串列表未含 `"opus-5"` 而被 API 拒绝 | OPEN，暂无 fix PR | Opus 5 已完全弃用 temperature 参数，需更新过滤列表 |
| 🟡 中 | [#5190](https://github.com/HKUDS/nanobot/issues/5190) — 前端模块脚本因 MIME 类型 `text/plain` 加载失败 | CLOSED（今日关闭） | 已解决，详情见 Issue 链接 |

另有两条已合并的 P1 修复值得注意：DeepSeek reasoning 序列化失败（[#5214](https://github.com/HKUDS/nanobot/pull/5214)）和 Gemini 回放时未签名工具调用导致 400 错误（[#5230](https://github.com/HKUDS/nanobot/pull/5230)，OPEN 状态待合并）。

> 整体评估：当前 Bug 积压压力较小（仅 1 条 OPEN），Opus 5 兼容问题影响面限于 Anthropic 最新模型用户，建议尽快补充 `"opus-5"` 至过滤列表。


## 6. 功能请求与路线图信号

| 功能需求 | 来源 | 状态 | 进入下一版本的可能性 |
|---|---|---|---|
| 跨会话搜索与 @ 提及 | PR [#5211](https://github.com/HKUDS/nanobot/pull/5211) | OPEN，待 review | 中高 — 功能已完成实现且非破坏性，若评审顺利可进入下个版本 |
| mst-python 元搜索 provider | PR [#5234](https://github.com/HKUDS/nanobot/pull/5234) | OPEN，待 review | 中 — 涉及新依赖引入，需评估维护成本 |
| Mattermost 线程独立群组策略 | PR [#5233](https://github.com/HKUDS/nanobot/pull/5233) | OPEN，待 review（孪生 PR #5232 已关闭） | 中高 — 属于现有 Mattermost 支持的合理延伸 |
| 空闲会话归档供 Dream 处理 | PR [#5231](https://github.com/HKUDS/nanobot/pull/5231) | OPEN，待 review | 中 — 解决 Dream 记忆机制对短空闲会话的盲区 |
| Gemini 回放时剔除未签名工具调用 | PR [#5230](https://github.com/HKUDS/nanobot/pull/5230) | OPEN，待 review（P1 修复） | 高 — 修复跨 provider 模型切换的硬错误 |

> 路线图信号：项目正向 **多 provider 兼容性深化** + **WebUI 交互精细化** 双线推进。mst 元搜索和跨会话引用若合入，将明显增强 NanoBot 作为个人 AI 助手的实用性和信息整合能力。


## 7. 用户反馈摘要

- **Opus 5 用户**（[#5235](https://github.com/HKUDS/nanobot/issues/5235)）：升级到最新 Claude Opus 5 后所有请求被 API 拒绝，且原因是代码中维护的模型名单未跟上 Anthropic 发布节奏——由于 `omit_temperature` 的子串列表是硬编码的，每次新模型发布都可能产生兼容问题。这提示开发者**考虑将模型特性配置从硬编码改为动态获取或配置化**，或建立更及时的模型发布跟踪机制。

- **Mattermost 深度用户**（[#5233](https://github.com/HKUDS/nanobot/pull/5233)）：在已支持 Mattermost 的基础上进一步要求细化控制——线程内是否需要 @ 提及才能触发机器人。此类需求说明用户已将 NanoBot 深度集成到日常团队协作流中，对渠道行为有精细化管控预期。

- **前端部署用户**（[#5190](https://github.com/HKUDS/nanobot/issues/5190)，已关闭）：浏览器因 MIME 类型错误拒绝加载 JS 模块，是典型静态文件服务配置问题。该 Issue 今日关闭，但需确认修复是文档级（引导用户正确配置）还是代码级（自动设置 Content-Type）。


## 8. 待处理积压

| 项目 | 类型 | 搁置时长 | 备注 |
|---|---|---|---|
| [#5235](https://github.com/HKUDS/nanobot/issues/5235) Opus 5 temperature 参数过滤缺失 | Bug | 1 天 | 建议尽快修复，影响所有 Opus 5 用户 |
| [#5234](https://github.com/HKUDS/nanobot/pull/5234) mst-python 元搜索 provider | PR | 1 天 | 新增功能，等 review |
| [#5233](https://github.com/HKUDS/nanobot/pull/5233) Mattermost 线程群组策略 | PR | 1 天 | 等 review；注意与关闭的 #5232 内容重复，需确认合并意图 |
| [#5211](https://github.com/HKUDS/nanobot/pull/5211) 跨会话搜索与 @ 提及 | PR | 3 天 | 功能价值高，建议尽快安排 review |
| [#5230](https://github.com/HKUDS/nanobot/pull/5230) Gemini 回放剔除未签名工具调用 | PR | 1 天 | P1 修复，建议优先处理 |

> 整体评估：当前 backlog 中出现多项 OPEN 状态的 P1 高优 PR，建议维护团队本周内安排集中 review，避免高优修复长期滞留未合并状态。


*本日报由 AI 分析师自动生成，数据来源为 NanoBot GitHub 仓库公开信息。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-04


## 1. 今日速览

Hermes Agent 在 v0.20.0（The Herald Release）发布后进入了高强度迭代期。过去 24 小时活跃度极高：50 条 Issue 更新（41 条活跃/新开）、50 条 PR 更新（46 条待合并），标志着发布后社区反馈密集涌现，同时也伴随大量回归验证和缺陷报告涌入。新版本 v2026.8.3 的发布是今日最大事件，但从 Issue 数据来看，社区在 Windows 路径处理、Telegram 网关连接、配置隔离等方面暴露了多项需要快速响应的稳定性问题。项目整体处于"发布后热修复+社区验证"的高峰期，维护者响应速度将直接影响社区信心。


## 2. 版本发布

### Hermes Agent v0.20.0（v2026.8.3）— "The Herald Release"

- **发布日期：** 2026 年 8 月 3 日
- **版本对比：** 自 v0.19.0 以来累计约 3,650 次提交、~1,400 个合并 PR、~5,200 个文件变更（+559K/-405K 行）、关闭约 1,200 个 Issue、650+ 贡献者

> **版本代号解读：** Hermes（赫尔墨斯）是希腊神话中众神的信使，此代号寓意该版本"传递"了大规模的功能更新与社区修复成果，也暗示 v0.20 是承上启下的重要里程碑。

> ⚠️ **注意：** Releases 页面对该版本的详细变更日志未完整展开（被截断），以下分析多基于 Issue/PR 推断。

### 值得关注的破坏性/兼容性风险点（基于社区反馈）

| 风险领域 | 相关 Issue | 状态 |
|---------|-----------|------|
| **Windows 原生路径回归** — `search_files` 绝对路径失败、敏感路径守卫失效 | #67629, #78079 | 已有修复 PR |
| **Telegram 网关连接挂起** — v0.20.0 中 gateway 进程内连接永久挂起 | #78052, #67498, #72454 | 多起重复报告，无统一修复 |
| **read_file 二进制误判回归** — 1000 字节截断破坏多字节 UTF-8 字符 | #76886（声称回归自 0.19.1） | 待修复 |
| **会话恢复/压缩边界行为变更** | #71322, #69847 | 待验证 |

**迁移建议：** 升级前建议备份 config.yaml 与 .env，尤其是 Windows 用户和重度 Telegram 网关用户。如遇 Telegram 连接问题，可暂时保留 v0.19.x 版本，或回退至 #63309 的 TELEGRAM_FALLBACK_IPS 方案（但 #67498 报告该方案在 0.18.2 上无效——需关注后续修复）。


## 3. 项目进展

今日合并的 PR 较少（4 个），但其中两个值得特别关注：

### 已合并/关闭 PR

| PR | 内容 | 意义 |
|----|------|------|
| [#78005](https://github.com/NousResearch/hermes-agent/pull/78005) `[CLOSED]` | **feat(skills): 新增 index-excluded 可见性状态** — 第三态：从发现索引隐藏但可精确加载；在 prompt 组装、skills_list、slash 命令发现、--skills 预加载等场景统一生效 | 为技能管理引入细粒度控制，解决技能冗余人问题（参见 #64392） |
| [#77944](https://github.com/NousResearch/hermes-agent/pull/77944) `[CLOSED]` | **fix(session): repair_message_sequence 中丢弃空 tool_calls** — 修复 DeepSeek v4 等严格提供方在长会话（~370K-395K tokens）中 HTTP 400 "empty array" 问题 | 直接修复 #77921，对长会话稳定性意义重大；#78071 继续跟进相关 sanitize 缺口 |

### 值得注意的待合并 PR

- [#78086](https://github.com/NousResearch/hermes-agent/pull/78086) — **将 webhook 和模型 API key 移出 config.yaml**，通过 `.env` 的 `key_env` 引用管理。直击安全痛点（参见下面 #60551 中"Agent 被拒写 config.yaml"的矛盾），若能合并将改善密钥管理模型。
- [#78087](https://github.com/NousResearch/hermes-agent/pull/78087) — 修复 relay 会话栈损坏。PR 描述为模板占位（未填具体内容），需关注完善。

**整体评估：** 项目在 3,650 次提交的体量下，"广度优先、深度修复"策略明显——新功能（skill 状态、i18n）与关键 bug 修复并行推进。但大量 PR 处于待合并状态（46/50），合并积压可能成为未来瓶颈。


## 4. 社区热点

今日讨论最活跃的 Issue（均为 7+ 评论）：

### 1. [#30220](https://github.com/NousResearch/hermes-agent/issues/30220) — 后台自我改进审查在 memory/skill/user 存储之间错误分类内容
- **标签：** `comp/agent`, `tool/memory`, `tool/skills`, `sweeper:risk-session-state`
- **评论数：** 7
- **用户诉求：** `_spawn_background_review` 系统（周期性分叉子代理审查对话并保存学习成果）对内容的归类存在系统性偏差，可能将本应写入 memory 的内容误存为 skill，或反之，导致 Agent 行为出现不可预测变化。
- **点评：** 这是"AI Agent 自我进化"机制的核心正确性问题，直接影响用户对 Agent 长期行为可控性的信任。若 Agent 在无监督下存储了错误归类的信息，错误会被"放大"而非"纠正"。虽创建于 5 月，但讨论热度持续，标签中的 `sweeper:risk-session-state` 暗示其与会话状态完整性直接相关——值得优先处理。

### 2. [#76886](https://github.com/NousResearch/hermes-agent/issues/76886) — read_file 将含截断多字节字符的有效 UTF-8 文本误判为二进制
- **标签：** `comp/tools`, `tool/file`, `regression`
- **评论数：** 7
- **用户画像：** Obsidian 笔记重度用户，升级 0.19.1 后笔记无法打开
- **技术细节：** `read_file` 使用 `head -c 1000` 采样，当第 1000 字节恰好切断一个多字节 UTF-8 字符时，采样结果包含非法 UTF-8 序列，被误判为二进制。
- **点评：** 教科书级的边界 bug，但用户影响面巨大（任何包含中文、日文、emoji 的文件都有触发风险）。7 条评论可能包含复现方案或补丁建议。标签 `needs-decision` 意味着维护者尚未定夺修复方向（是否改用 `head -c 4000` 或使用 Python 原生采样）。

### 3. [#67498](https://github.com/NousResearch/hermes-agent/issues/67498) — Telegram 网关卡在 "Connecting to Telegram (attempt 1/8)"，py-spy 显示所有线程空闲
- **标签：** `platform/telegram`, `P1`, `sweeper:risk-message-delivery`
- **评论数：** 7，👍 1
- **关键信息：** 即使用户已应用 #63309/#64370 的 `TELEGRAM_FALLBACK_IPS` 方案，问题依旧；py-spy 显示线程**未被阻塞**而是**全部空闲**——这是一个微妙的状态，暗示死锁并非 socket 阻塞，而是事件循环/异步任务调度的 bug（如某个 await 永远不返回）。
- **点评：** 与 #78052（v0.20.0 中 gateway 进程内挂起）和 #72454（`Application.initialize()` 挂起）形成问题簇，是当前**最高优先级**的稳定性问题。3 个独立 Issue 描述同一症状的不同变体，强烈暗示根因在共享的 Telegram 适配器初始化路径。P1 标记合理。

### 4. [#39043](https://github.com/NousResearch/hermes-agent/issues/39043) — Signal 适配器：原生引用/回复、编辑、远程删除和已读回执支持
- **标签：** `comp/gateway`, `platform/signal`, `P3`, `needs-decision`
- **评论数：** 7，👍 2（今日最高 👍）
- **用户诉求：** Signal 适配器缺乏 signal-cli 的多个端到端能力：出站引用/回复、时间戳 ID、编辑 Agent 自己的消息、远程删除/撤销、已读回执。
- **点评：** 这是**功能完整性**诉求——Signal 用户面临的核心痛点不是"消息能收到"，而是"agent 像普通用户一样能与人类正常对话"。虽然 P3 优先级，但 2 个 👍 表明存在一定社区需求。`needs-decision` 标签意味着维护者尚未明确是否/何时纳入路线图。

### 5. [#29771](https://github.com/NousResearch/hermes-agent/issues/29771) — 扩展凭据池到搜索后端（Tavily / Exa）
- **评论数：** 5
- **用户诉求：** `credential_pool.py` 对任意 provider 都接受 `load_pool(provider)` 字符串，但搜索/网页后端（Tavily、Exa、Brave Free、Firecrawl 等）尚未接入。用户希望搜索 API key 也能使用凭据池轮换。
- **点评：** 符合 Agent 长期运行场景下的凭据轮换需求——多个搜索 key 自动故障转移/负载均衡，避免因单一 key 配额耗尽导致 Agent 中断。是"生产环境 Agent"的必备能力。


## 5. Bug 与稳定性

按严重程度排列：

### P1（严重，影响核心消息通道或数据安全）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#67498](https://github.com/NousResearch/hermes-agent/issues/67498) | Telegram 网关卡死（py-spy 显示线程空闲）— 绕过方案无效 | **无 fix PR**；与 #78052 重复 |
| [#78052](https://github.com/NousResearch/hermes-agent/issues/78052) | Telegram 网关 v0.20.0 中永久挂起；但独立 adapter 脚本可正常连接——问题**只在 gateway 进程内**触发 | **无 fix PR** |
| [#69216](https://github.com/NousResearch/hermes-agent/issues/69216) | Windows 11 上 uv 安装后"not found"（管理脚本使用 `iex` 安装到 AppData 但无法找到） | **无 fix PR**；新用户装机严重阻碍 |

### P2（重要，影响特定场景或平台）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#76886](https://github.com/NousResearch/hermes-agent/issues/76886) | read_file 1000 字节采样破坏 UTF-8 多字节字符 → 误判二进制 | **无 fix PR** |
| [#67629](https://github.com/NousResearch/hermes-agent/issues/67629) | search_files Windows 绝对路径被 MSYS 改写为 `/d/`，原生 rg 无法解析 | **无 fix PR** |
| [#64392](https://github.com/NousResearch/hermes-agent/issues/64392) | 重复技能名称在 list/prompt/skill_view 三种行为不一致 | **无 fix PR**；#78005 部分改善 |
| [#10376](https://github.com/NousResearch/hermes-agent/issues/10376) | Profile 隔离不完整：`--clone` 复制记忆文件、Agent 可跨 profile 读取 | **无 fix PR**；涉及隐私/数据边界 |
| [#60551](https://github.com/NousResearch/hermes-agent/issues/60551) | patch/write_file 拒绝写 config.yaml；但 `hermes config set` 将列表键写成字符串标量 | **无 fix PR** |
| [#68559](https://github.com/NousResearch/hermes-agent/issues/68559) | 多路复用网关忽略路由 profile 的 terminal 后端，Docker profile 继承本地后端 | **无 fix PR**；安全边界风险 |
| [#73692](https://github.com/NousResearch/hermes-agent/issues/73692) | `agent.disabled_toolsets: [browser]` 同时删除 `web_search`，两处实现行为不一致 | **无 fix PR** |
| [#71322](https://github.com/NousResearch/hermes-agent/issues/71322) | `/resume` 对所有 v23 迁移前的会话（NULL chat_id）永久阻塞 | **已关闭**（未标注修复方式，需确认） |
| [#72454](https://github.com/NousResearch/hermes-agent/issues/72454) | python-telegram-bot `Application.initialize()` 挂起（#63309 回归） | **无 fix PR** |
| [#78072](https://github.com/NousResearch/hermes-agent/issues/78072) | 自定义 provider 的 `model.provider` 被设为显示名称（如 `custom:9router`）而非运行时名称 | **无 fix PR** |
| [#78022](https://github.com/NousResearch/hermes-agent/issues/78022) | webhook 平台端口冲突时陷入重连循环，gateway 不退出 | **无 fix PR** |
| [#76902](https://github.com/NousResearch/hermes-agent/issues/76902) | Desktop 设置 `TERMINAL_CWD` 为 home 目录，SubdirectoryHintTracker 扫描整个 home 子树找 AGENTS.md（性能与隐私问题） | **无 fix PR** |
| [#78071](https://github.com/NousResearch/hermes-agent/issues/78071) | `sanitize_api_messages` 未过滤缺失/空 `tool_call_id` 的 tool 消息 | **已关闭** |

### P3（低严重度/需复现）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#77618](https://github.com/NousResearch/hermes-agent/issues/77618) | Desktop 要求 macOS 12+，macOS 15 用户无法运行（矛盾？） | **无 fix PR**；描述过于简略 |
| [#75329](https://github.com/NousResearch/hermes-agent/issues/75329) | Desktop 语音对话仅第一轮生效，后续不采集麦克风 | **无 fix PR** |
| [#78078](https://github.com/NousResearch/hermes-agent/issues/78078) | Desktop 状态栏显示两个重复的 gateway 状态指示器 | **duplicate** |
| [#78029](https://github.com/NousResearch/hermes-agent/issues/78029) | 错误仓库提交的无效 issue | 已标记 invalid |

### 特别关注的回归趋势

1. **Telegram 问题簇：** #67498（0.18.2）→ #72454（0.19.0）→ #78052（0.20.0），持续 3 个版本未根治，且有"独立 adapter 正常、gateway 内挂起"的新线索。这是**发布阻断级**问题（P1），建议维护者立即交叉审查三份报告。
2. **Windows 路径苦手：** #67629（search_files）、#78079（敏感路径守卫失效）、#78082（content-hash 对称性）集中暴露了 Windows 原生化不足——跨平台路径规范化是反复出现的主题。


## 6. 功能请求与路线图信号

### 今日新提出的功能请求

| Issue | 描述 | 潜力评估 |
|-------|------|---------|
| [#78061](https://github.com/NousResearch/hermes-agent/issues/78061) | **工具间二进制内容管道：** 允许工具消费前一个工具的输出，无需模型重新发射内容。当前 MCP 工具返回二进制内容无法直接传给 `vision_analyze`/`write_file`，模型需重打整个 payload | 中等。技术上是"工具间数据流"的架构改进，但可能引入状态管理复杂度；`needs-decision` 未标注 |
| [#77367](https://github.com/NousResearch/hermes-agent/issues/77367) | **OMP 综合分析：** LSP、AST、`xd://`、安全、SQLite、冲突检测等多模块增强 | 低。过于宽泛，更像提案集而非具体需求；`ras-indo` 在 v0.19.1 的代码基础上分析了"实际差距"，但可实施性存疑 |
| [#77744](https://github.com/NousResearch/hermes-agent/issues/77744) | **状态栏上下文百分比增量刷新：** 工具循环中每次 tool call 响应后立即更新状态栏（当前仅最终 assistant 响应后更新） | 高。小改进、明确收益（用户对长任务期间的上下文消耗有实时感知）；`comp/tui` 范围内，实现成本低 |
| [#68859](https://github.com/NousResearch/hermes-agent/issues/68859) | **工具重试语义：** 在生命周期钩子中暴露 attempt count、retry count、工具间关系 | 中。对 telemetry/observability 价值大，但设计需谨慎避免破坏现有钩子契约 |

### 结合已有 PR 的可能纳入版本

- **#78005（已合并）index-excluded skill 可见性** — 直接缓解 #64392 的 "重复技能名在 list/prompt/skill_view 不一致" 问题。这是**已进入代码库**的功能，后续版本会对用户可见。
- **#78086（待合并）API key 移出 config.yaml** — 如果是被接受的方向，将解决 #60551 的一半矛盾（config 写入被拒 + 明文 key 存储风险）。
- **#65102（待合并）会话身份早期解析** — 让 API 发起的 turn 使用与 Telegram/Discord 相同的平台身份与工具集。这可能是对 #71322（/resume 问题）和 #78034（Matrix 线程会话 churn）的架构级修复。

### 社区最想看到什么（基于 👍 和讨论热度）

1. **Signal 完整原生消息能力**（#39043，👍 2）— "Agent 像真人一样发消息"的诉求。
2. **多路复用网关的 profile 隔离**（#68559，👍 2）— 安全边界 + 配置一致性的双重期待。
3. **后台自我改进的正确性**（#30220，7 评论）— 用户对 "AI 自我修改" 的信任红线。


## 7. 用户反馈摘要

### 真实用户痛点

- **"我更新了 agent 镜像后，我的 Obsidian 笔记打不开了。它们是纯 UTF-8 markdown，更新前一切正常。"** — [#76886](https://github.com/NousResearch/hermes-agent/issues/76886)，升级导致生产力工具直接失效，用户第一反应是"文件坏了"而非"工具坏了"，信任成本极高。

- **"我设置了 `agent.disabled_toolsets: [browser]` 来省浏览器 schema 的钱，结果它把我最常用的 `web_search` 也带走了。"** — [#73692](https://github.com/NousResearch/hermes-agent/issues/73692)，配置的隐性副作用比显式行为更伤害用户体验。

- **"Hermes 已经提供 `pre_tool_call`/`post_tool_call` 生命周期钩子，但没有重试计数。我无法判断一个工具调用是第一次尝试还是重试——这对我的 telemetry 管道是致命缺陷。"** — [#68859](https://github.com/NousResearch/hermes-agent/issues/68859)，中大型企业用户的 observability 诉求。

- **"同一个 Matrix 线程里的回复被路由到了不同的 Hermes session ID。这破坏了上下文连续性，尽管线级线程是存在的。"** — [#78034](https://github.com/NousResearch/hermes-agent/issues/78034)，多平台网关用户的会话一致性焦虑。

- **"我 drag & drop 安装了 macOS 15 版本，结果 'can't run'。"** — [#77618](https://github.com/NousResearch/hermes-agent/issues/77618)，安装体验对非技术用户是门槛。描述过于简略，需追问细节。

- **"信号适配器已经能用，但无法编辑自己的消息、无法远程删除、无法发引用回复——我需要的是'ag 像人一样聊天'，不是'能收到消息就行'。"** — [#39043](https://github.com/NousResearch/hermes-agent/issues/39043)，功能完整性与"产品化"之间的鸿沟。

### 满意点（间接信号）

- 用户愿意用 py-spy 做深度调试（#67498），说明技术型用户对项目质量有较高期待。
- 650+ 贡献者、~1,400 个合并 PR 的历史数据显示社区参与度健康。
- 大部分 P2 问题有**清晰的技术分析**（如 #67629 明确 MSYS 路径改写与原生 rg 的矛盾），说明用户群体专业度高。

### 不满意信号

- **Telegram 问题连续 3 个版本未根治** — 社区耐心在消耗。多个用户反复报告同一症状、反复被标记 duplicate，可能引发挫败感。
- **Windows 问题占比异常高** — 从安装（#69216）、路径（#67629）、敏感路径守卫（#78079）、BOM 解析（#65124）、content hash（#78082）到 lane 重复（#71889），Windows 用户体验碎片化严重。


## 8. 待处理积压

| 类型 | 编号 | 描述 | 已开放 | 优先级 | 建议 |
|------|------|------|--------|--------|------|
| Issue | [#30220](https://github.com/NousResearch/hermes-agent/issues/30220) | 后台自我改进内容错误分类 | ~75 天 | P2 | 创建于 5/22，热度持续，影响 Agent 自主学习正确性。建议尽快分配 owner 并明确修复方向（memory/skill 分类逻辑需要重新审视） |
| Issue | [#10376](https://github.com/NousResearch/hermes-agent/issues/10376) | Profile 隔离不完整（--clone 复制记忆 + 跨 profile 读取） | ~111 天 | P2 | 创建于 4/15，超过 3 个月未解决。隐私边界问题在 AI 助手场景中是信任基石，长期未响应可能流失安全敏感用户 |
| Issue | [#78061](https://github.com/NousResearch/hermes-agent/issues/78061) | 工具间二进制内容管道 | 1 天 | P3 | 新需求但架构影响面大，建议在路线图讨论中明确是否考虑 |
| PR | [#78087](https://github.com/NousResearch/hermes-agent/pull/78087) | fix(relay): 恢复损坏的会话栈 | 1 天 | — | PR 描述为模板占位（Fixes # 未填），说明作者提交不完整。维护者需要催促进补，否则会话损坏问题无法被评估 |
| PR | [#53958](https://github.com/NousResearch/hermes-agent/pull/53958) | 可配置 `warn_after_compressions` 阈值 | ~37 天 | P3 | 长期滞留，功能简单但能解决用户长会话中反复压缩警告的痛点。合并积压的表征 |
| PR | [#63789](https://github.com/NousResearch/hermes-agent/pull/63789) | macOS 26 spawn-helper 权限修复 | ~22 天 | P3 | 影响 macOS 用户终端功能，等待过久可能错过下一波 macOS 用户 |
| Issue | [#29771](https://github.com/NousResearch/hermes-agent/issues/29771) | 凭据池扩展到搜索后端 | ~75 天 | P2 | 生产环境 Agent 的刚需，已有 `load_pool` 机制但未接入搜索服务，改动范围应可控，建议纳入短期路线图 |

**特别提醒：** 上述 Telegram 问题簇（#67498/#78052/#72454）虽非"无响应"而是"未解决"，但若下一版本仍未包含修复，建议发布前在 release notes 中明确已知问题，避免用户重复踩坑。


### 健康度总结

Hermes Agent 处于**"发布后高压期"**：功能迭代速度快（v0.19→v0.20 间隔仅为单月）、社区贡献活跃，但发布质量控制的短板开始显现——大量回归（UTF-8 截断、Windows 路径）和长期未愈的顽疾（Telegram 挂起、profile 隔离）对用户体验造成了负面影响。建议维护者在下一个版本（v0.20.1 hotfix）中优先处理 P1/P2 级缺陷，同时在发布流程中增加 Windows 与 Telegram 的回归测试。项目整体仍处于高速上行轨道，但"稳"与"快"的平衡需要更精细的节奏把控。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-04** | **数据统计周期：2026-08-03 至 2026-08-04**


## 1. 今日速览

PicoClaw 在过去 24 小时内保持了较活跃的社区参与度：共产生 8 条 Issue 更新和 6 条 PR 更新，其中 3 个新 PR（#3316、#3315、#3314）集中于路由代理上下文管理、Telegram 私聊话题支持和命令白名单修复，显示出对核心功能的持续完善。今日新开 Issues 数量较少（3 个），且有多达 5 个历史 Issue 被关闭（其中多数为 stale 标记后解决），整体积压问题正在消化中。值得注意的是，多个新 PR 由同一位贡献者（j-v）提交，同时解决了此前报告的 dispatch 路由相关问题（Issue #3301），形成了有效的 issue-PR 闭环。项目整体健康度良好，虽无新版本发布，但功能修复与社区反馈处理均处于正常节奏。

**活跃度评估：中高** — 无大规模功能发布，但 Issue 关闭率高，新 PR 针对性强，社区贡献者活跃。


## 2. 版本发布

过去 24 小时暂无新版本发布。当前最新版本为 0.3.1。


## 3. 项目进展

> 说明：今日合并/关闭的 PR 多为 stale（已超 14 天未更新）后被自动关闭或合并，非近期活跃工作，但仍能反映项目的主要演进方向。

回顾近期合并/关闭的 PR，可以观察到以下进展方向：

| PR | 关联 Issue | 功能/修复内容 | 状态 |
|---|---|---|---|
| [#3273](https://github.com/sipeed/picoclaw/pull/3273) | #3272 | 在 WebUI 和 Launcher 中添加日语（`ja`）本地化支持，完整翻译 `en.json` 全部 968 行，并注册 `dayjs/locale/ja` | 已关闭（stale） |
| [#3267](https://github.com/sipeed/picoclaw/pull/3267) | — | 修复 antigravity token 刷新时 scope 传递错误，解决 `PERMISSION_DENIED` 错误 | 已关闭（stale） |
| [#3202](https://github.com/sipeed/picoclaw/pull/3202) | — | 修复 `NormalizeAgentID`/`NormalizeAccountID` 中 ID 规范化时首尾下划线未剥离的问题 | 已关闭（stale） |

结合今日新开的 PR，可以将项目当前进展归纳为**三大推进方向**：

1. **路由代理上下文管理**（[#3316](https://github.com/sipeed/picoclaw/pull/3316)）：修复 dispatch 规则路由到特定 agent 后，会话记忆丢失、自动压缩/摘要失效的问题。该 PR 直接回应用了 Issue #3301 的用户反馈，实现了从问题报告到修复提案的快速闭环。
2. **Telegram 话题支持增强**（[#3315](https://github.com/sipeed/picoclaw/pull/3315)）：在私聊机器人聊天中支持 Telegram 的 `IsTopicMessage` 话题模式，使启用话题模式的私聊机器人也能正确识别话题上下文。
3. **命令白名单修复**（[#3314](https://github.com/sipeed/picoclaw/pull/3314)）：修复 `customAllowPatterns` 不生效的问题，此前自定义允许的 shell 命令（如 `git push`）仍被默认拒绝规则拦截。

整体来看，项目正在**密集完善 agent 路由与上下文管理机制**，同时兼顾本地化、Telegram 适配和工具调用可靠性。


## 4. 社区热点

### 🔥 今日最受关注的 Issue

**[#3281](https://github.com/sipeed/picoclaw/issues/3281) — Web UI 聊天输入在历史记录较长时严重卡顿**（3 条评论，1 👍，仍为 OPEN）

这是一个典型的性能回归问题。用户报告在 PicoClaw 0.3.1 版本中，当单个会话内聊天历史积累到一定长度后，Web UI 输入框响应变得极其迟滞。该 Issue 已存在两周（创建于 7/21），且迄今为止**没有关联的修复 PR**，值得项目方优先关注。

### 💬 其他活跃讨论

**[#3301](https://github.com/sipeed/picoclaw/issues/3301) — 路由到非默认 agent 的会话中 /clear 和自动压缩失效**（1 条评论，OPEN）— 已于今日获得 PR #3316 跟进，社区反馈得到快速响应。

### 用户诉求分析

从讨论来看，社区当前**最集中的痛点是代理路由功能的上下文管理不完善**。无论是 dispatch 路由后的记忆丢失（#3301）还是长历史导致的 UI 卡顿（#3281），归根结底都指向**会话上下文处理机制的健壮性不足**。


## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | **MCP 服务器连接失败会导致 agent 循环挂起**，使聊天界面完全停止回复用户 | OPEN，无关联 fix PR |
| 🟡 中 | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | **Web UI 长历史记录下输入卡顿**，影响核心聊天体验 | OPEN，无关联 fix PR |
| 🟡 中 | [#3301](https://github.com/sipeed/picoclaw/issues/3301) | **路由到非默认 agent 时 /clear 与自动压缩失效** | OPEN，已有 fix PR [#3316](https://github.com/sipeed/picoclaw/pull/3316) 待合并 |
| 🟢 低 | [#3314](https://github.com/sipeed/picoclaw/pull/3314) | **`customAllowPatterns` 不生效**，默认拒绝规则覆盖自定义允许规则 | 已提交修复 PR，待合并 |

### 特别关注

- [#3269](https://github.com/sipeed/picoclaw/issues/3269) 是当前**最严重的稳定性问题**：一旦 MCP 服务器连接失败，agent 循环将无限挂起，用户无法正常使用聊天功能。该问题自 7/20 报告以来已持续两周，至今仍无修复 PR，建议维护者优先排查。
- [#3281](https://github.com/sipeed/picoclaw/issues/3281) 同样已存在两周且无修复进展，涉及 Web UI 核心交互体验，严重性较高。


## 6. 功能请求与路线图信号

### 已有关联 PR 的功能请求（可能进入下一版本）

| 功能请求 | 关联 PR | 分析 |
|---|---|---|
| [#3272](https://github.com/sipeed/picoclaw/issues/3272) 日语本地化 | [PR #3273](https://github.com/sipeed/picoclaw/pull/3273) | 完整翻译已提交，主文档已有日文版，WebUI 补齐后有望在下个版本正式纳入 |
| Telegram 私聊话题支持 | [PR #3315](https://github.com/sipeed/picoclaw/pull/3315) | 针对启用话题模式的 Telegram 私聊机器人，属增量功能增强 |

### 尚无关联 PR 的功能请求

**[#3276](https://github.com/sipeed/picoclaw/issues/3276) — Launcher 支持外部 systemd 管理的 gateway**：用户希望 headless 部署时 Launcher 能检测并适配 systemd 托管的 gateway，避免 WebUI 的 Start/Stop 按钮尝试接管外部进程。该请求涉及架构层面的生命周期管理，短期内可能不易落地，但反映了**服务器端无头部署场景的切实需求**，建议维护者评估。

### 路线图信号

综合来看，下一版本可能包含：**日语本地化、Telegram 话题增强、路由 agent 上下文修复、自定义命令白名单修复**。此外，**MCP 连接失败时的容错处理**（#3269）应是当前最优先的稳定性修复项。


## 7. 用户反馈摘要

### 典型使用场景

- **Headless 服务器部署**（如 Ubuntu VM）：用户 honbou 将 `picoclaw gateway` 和 Launcher 均作为 systemd 服务运行，以实现开机持久化和自动重启，但对 Launcher 尝试接管 gateway 生命周期感到不便（[#3276](https://github.com/sipeed/picoclaw/issues/3276)）。
- **多平台接入**：用户 j-v 在 Discord 和 Telegram 上同时使用 PicoClaw，并配置 dispatch 规则将不同类型消息路由到不同 agent（[#3301](https://github.com/sipeed/picoclaw/issues/3301)）。

### 用户痛点

1. **路由后上下文丢失**（#3301）：agent 不记住先前消息，自动压缩从不触发 — *“didn't remember anything from previous messages, and auto-compaction never triggered regardless of the number of messages"*
2. **UI 性能退化**（#3281）：历史稍长后输入框卡顿，影响日常使用体验。
3. **连接失败无容错**（#3269）：MCP 连接失败导致整个聊天服务无响应，用户被"静默"中断。
4. **配置项反直觉**（#3268）：`exec` 工具的 `action` 参数被标记为必填，但实际绝大多数调用都是默认的 `"run"`，导致无谓的失败。

### 满意之处

- 社区反馈响应速度良好：Issue #3301 报告后当天即收到 PR #3316 的修复跟进。
- 本地化推进积极：主文档已有日文翻译，社区贡献者也愿意补齐 WebUI 的翻译工作（#3272、PR #3273）。


## 8. 待处理积压

> 以下为长期未获得足够关注或响应的问题，按风险程度排列。

| 优先级 | Issue/PR | 状态 | 备注 |
|---|---|---|---|
| 🔴 高 | [#3269](https://github.com/sipeed/picoclaw/issues/3269) MCP 连接失败导致 agent 循环挂起 | 已 OPEN 15 天，无 fix PR | **最严重稳定性问题**，建议维护者立即关注 |
| 🟡 中 | [#3281](https://github.com/sipeed/picoclaw/issues/3281) Web UI 长历史输入卡顿 | 已 OPEN 14 天，无 fix PR | 核心体验问题，一直未有人认领 |
| 🟡 中 | [#3276](https://github.com/sipeed/picoclaw/issues/3276) Launcher 适配 external gateway | 已 CLOSED，但未真正解决 | 可能是 stale 自动关闭，需求依然存在 |
| 🟢 低 | PR [#3316](https://github.com/sipeed/picoclaw/pull/3316)、[#3315](https://github.com/sipeed/picoclaw/pull/3315)、[#3314](https://github.com/sipeed/picoclaw/pull/3314) | 3 个新 PR 等待 review | 均为活跃贡献者 j-v 与 genuss 提交，建议尽快 review 合并 |

### 维护者行动建议

1. **优先处理 #3269** — MCP 连接失败的容错机制缺失是当前最大的用户可见风险。
2. **Review 今日新提交的 3 个 PR** — 其中 #3316 与 #3314 均直接修复用户报告的 Bug，建议快速合并。
3. **对 #3281 进行性能排查** — 关注 Web UI 在长上下文下的渲染性能，可能需要虚拟滚动或消息裁剪策略。
4. **评估 #3276 的 un-stale 处理** — 该功能请求具有实际部署价值，若暂无开发计划，建议在 Issue 中明确说明路线图排期。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期**: 2026-08-04 | **数据窗口**: 过去24小时 (2026-08-03 ~ 2026-08-04)


## 1. 今日速览

NanoClaw 在过去 24 小时内保持中高活跃度，核心维护团队（core-team 标签贡献显著）与外部贡献者均有产出。本日共处理 9 条 PR（6 条已合并/关闭，3 条待合并），1 条新 Issue 上报，无新版本发布。值得关注的是，外部贡献者 OowhitecatoO 提交了 2 条针对对话会话稳定性与冷会话保留策略的修复 PR，目前均处于待合并状态，反映出社区对 Agent 会话生命周期管理的真实需求。此外，团队完成 Agent 镜像安全加固的重新固定（re-pin），并合并了多条关于 iMessage 频道、审批卡片界面与 engagement 策略的功能/修复 PR。项目整体处于健康迭代状态，但需留意 #3179 号 Node.js 运行时兼容性报错以及 #3092 号远程 MCP 服务器支持长期未合并。


## 2. 版本发布

**无新版本发布。** 但 [#3182](https://github.com/nanocoai/nanoclaw/pull/3182) 已将 Agent 镜像重新固定至硬化版本（hardened-2026-08-02），虽不构成版本号更新，但属于重要的基础设施安全变更，建议用户在下一次版本发布中关注此变更的包含情况。


## 3. 项目进展

今日合并/关闭的 PR 中，以下几条对项目推进有实质性意义：

- **[#3182](https://github.com/nanocoai/nanoclaw/pull/3182) [合并] Agent 镜像重新固定至 hardened-2026-08-02**：核心团队维护，Agent 镜像基础层已更新为 2026-08-02 构建的加固版本（611MB → 621MB）。PR 明确说明 NanoClaw 内容层 digest 未变更（`ai.echo.image.upstream.digest` 保持一致），因此属纯基础安全加固，无功能变化风险。

- **[#3181](https://github.com/nanocoai/nanoclaw/pull/3181) [合并] iMessage 频道：首条消息即显式启用指定线路**：修复了 iMessage 频道需额外配置才能激活的问题——现在用户向已分配的线路发送第一条消息即自动完成 opt-in，降低了上手门槛。

- **[#3180](https://github.com/nanocoai/nanoclaw/pull/3180) [合并] 更新流程：显式提示硬化镜像迁移**：改进了 `update` 命令的用户提示，使升级到硬化镜像的过程更透明，减少用户困惑。

- **[#3137](https://github.com/nanocoai/nanoclaw/pull/3137) [合并] 修复 engagement 一致性 + 暴露自助接线控制**：该 PR 横跨约一周（7/26 → 8/03）后合并，涉及三点：累积消息作为上下文但不触发持续容器跟随轮次、允许 group 级 Agent 检查其接线配置并申请更新 engagement 策略、拒绝非法 JavaScript engagement 正则表达式。

- **[#3143](https://github.com/nanocoai/nanoclaw/pull/3143) [合并] 保留已解析审批卡片内容**：审批卡片在被处理后仍保留标题与请求详情，按钮替换为静默化的决策与执行者（或超时状态），原始内容得以持久化。

- **[#3178](https://github.com/nanocoai/nanoclaw/pull/3178) [关闭] 误开仓库**：发起人主动关闭，无代码变更。


## 4. 社区热点

本日社区讨论热度整体不高，唯一的新 Issue（#3179）获得 1 条评论，暂无高讨论量的线程。值得关注的外部贡献集中在两条待合并的 PR 上（见下）：

- **[#3184](https://github.com/nanocoai/nanoclaw/pull/3184) [待合并] 修复 Claude 会话恢复：transcript 缺失时轮换新会话而非继续死会话**：作者 OowhitecatoO 指出，当存储的续接会话 transcript 文件不存在时，用户下一条消息会直接报错 `No conversation found with session ID: <uuid>` 且会话永久卡死。此修复将该场景转为自动轮换新会话，避免用户中断。

- **[#3183](https://github.com/nanocoai/nanoclaw/pull/3183) [待合并] 修复 group-init：固定 cleanupPeriodDays 防止保留清理回收冷会话**：同一作者修复了一个冷会话被过早回收的问题——当用户消息发到一个静默超过 30 天的频道时，同样因 `No conversation found` 报错。修复通过固定 `cleanupPeriodDays` 参数确保保留清理不会误删冷会话。

两条 PR 的诉求重合度极高：**NanoClaw 的会话生命周期管理存在稳定性缺陷**——会话因 transcript 缺失或清理策略误伤而不可用。这可能是当前社区最关心的实际痛点。


## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 |
|---------|------|------|
| **高** | **[#3179](https://github.com/nanocoai/nanoclaw/issues/3179) Node.js 兼容性**：`SyntaxError: The requested module 'node:util' does not provide an export named 'styleText'`。在启动 Basics 阶段即崩溃（9 秒内），影响所有使用 `@clack/core@1.2.0` 依赖的用户。疑似运行环境 Node.js 版本过低（`styleText` 需 Node.js ≥ 20.12），或依赖升级后未同步环境 | 无针对性修复 PR；可通过升级 Node.js 或回退 `@clack/core` 版本绕过 |
| **中** | **[#3184](https://github.com/nanocoai/nanoclaw/pull/3184) 会话 transcript 缺失导致死会话**：存储的续接 transcript 不存在时，会话永久不可用 | 已有修复 PR 待合并 |
| **中** | **[#3183](https://github.com/nanocoai/nanoclaw/pull/3183) 冷会话被清理回收**：静默超 30 天的频道发消息即报错，会话被保留清理误删 | 已有修复 PR 待合并 |
| **低** | **[#3143](https://github.com/nanocoai/nanoclaw/pull/3143) 审批卡片解析后内容丢失**（已修复）：已合并，按钮替换后原始内容不保留 | 已解决 |


## 6. 功能请求与路线图信号

- **[#3092](https://github.com/nanocoai/nanoclaw/pull/3092) [待合并已 16 天] 支持远程 Streamable HTTP MCP 服务器**：这是当前最值得关注的待合并功能 PR，由外部贡献者 amit-shafnir 提交（7/19 创建，已超两周）。该功能将显著扩展 NanoClaw 的 MCP 集成能力，使 Agent 可连接远程 HTTP MCP 服务器而不仅限于本地。长期未合并的原因未在 PR 中说明，建议核心团队关注或给出反馈，避免贡献者流失。

- **会话生命周期管理（冷会话轮换、保留策略）**：来自 [#3184](https://github.com/nanocoai/nanoclaw/pull/3184) 和 [#3183](https://github.com/nanocoai/nanoclaw/pull/3183) 的信号表明，社区对会话自动轮换、清理策略可配置化有明确需求。这两条 PR 如果合并，将改善整体稳定性。


## 7. 用户反馈摘要

- **[#3179](https://github.com/nanocoai/nanoclaw/issues/3179) 用户 benjamin920102 反馈 **：在 Jupyter 环境（`/home/jovyan/nanoclaw-v2`，pnpm 管理依赖）中启动 NanoClaw 时直接崩溃，报错指向 `@clack/core@1.2.0` 的 `styleText` 导入失败。这是环境兼容性问题——`styleText` 为 Node.js 20.12+ 的实验性 API，该用户的环境显然低于此版本。此反馈提醒核心团队应关注 Node.js 版本下限的声明与校验，或在启动时给出更友好的错误提示。

- **外部贡献者 OowhitecatoO 的两次提交** 均直接来源于真实使用场景中的会话报错（`No conversation found with session ID: <uuid>`），表明这类错误在实际使用中发生频率不低、影响明确（用户发送的消息直接丢失且无回复），且用户自修复意愿强。

- **总体反馈**：本日无明显的正面或负面产品反馈，社区用户更多表现为“遇到问题 → 自主修复 → 提交 PR”的积极参与模式。


## 8. 待处理积压

| 项目 | 类型 | 等待时长 | 状态 |
|------|------|---------|------|
| **[#3092](https://github.com/nanocoai/nanoclaw/pull/3092) 远程 Streamable HTTP MCP 服务器支持** | Feature PR | 16 天（7/19 创建） | 待合并，无最近评论，建议核心团队主动与作者沟通或加速评审 |
| **[#3179](https://github.com/nanocoai/nanoclaw/issues/3179) `node:util` `styleText` 导出错误** | Bug | 1 天 | 新上报，暂无官方响应，建议维护者确认对 Node.js 版本的下限要求并做出文档声明或依赖锁定 |
| **[#3184](https://github.com/nanocoai/nanoclaw/pull/3184) 缺失 transcript 时轮换会话** | Fix PR | 1 天 | 待合并，内容与 #3183 关联，建议一并评审 |
| **[#3183](https://github.com/nanocoai/nanoclaw/pull/3183) 固定 cleanupPeriodDays 防止冷会话被回收** | Fix PR | 1 天 | 待合并，与 #3184 有共同主题，建议一并评审 |

---

**数据来源**：[NanoClaw GitHub 仓库](https://github.com/nanocoai/nanoclaw)（2026-08-04）


</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-04

## 1. 今日速览

NullClaw 在过去 24 小时内保持稳定的活跃度：1 条新 Issue（调度器未授权问题）与 5 条 PR 更新（2 条已关闭、3 条待合并）。核心亮点集中在 ArcanePivot 提交的两条网络传输安全修复（#983、#982），分别针对提供商代理请求与 Telegram Bot API 代理场景，显示项目在代理与安全硬化路径上持续推进。mtdphn 之前提出的流式工具调用两项 PR（#964、#965）于今日关闭，相关能力可能已整合至主分支。整体项目健康度良好，无新版本发布，社区讨论热度中等。

---

## 3. 项目进展

**今日关闭（2 条）：**

- **PR #964** [CLOSED] — **Enable native API-level tool calls during streaming**（作者: mtdphn）
  - 该 PR 解决流式请求中 API 级工具调用增量（tool-call deltas）未被保留在 `StreamChatResult` 的问题，使 Agent 能够执行纯流式工具响应。关闭说明此项能力已合入主线，对依赖流式工具调用的用户是重要体验提升。

- **PR #965** [CLOSED] — **Structured streaming tool-call support for SSE parser**（作者: mtdphn）
  - 作为 #964 的配套修复，为 SSE 解析器增加结构化流式工具调用支持，处理服务器在 `delta.content` 中输出模型 XML 的场景。两项 PR 同时关闭，标志着流式工具调用路径已完成端到端整合。

**今日新增待合并（3 条）**

- **PR #983** [OPEN] — **fix(providers): use pinned curl path for proxied requests**（作者: ArcanePivot）
  - 将非流式提供商 POST 请求路由到已有的安全 curl 路径（当存在 pinned resolve 条目时），并将凭据头（credential headers）移出 argv，复用权限为 0600 的临时头文件。该改动增强代理场景下请求的安全性，降低凭据泄露风险。

- **PR #982** [OPEN] — **fix(telegram): use curl transport for explicit proxies**（作者: ArcanePivot）
  - 当 `channels.telegram.accounts.<id>.proxy` 显式配置时，将 Telegram Bot API POST 请求路由至已有的 curl 传输层；直连场景仍保留原生 HTTP 传输，并遵循代理路径上的每请求超时设置。这修复了 live channel probe 中已发现的代理路径不一致问题。

- **PR #956** [OPEN] — **ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group**（作者: dependabot[bot]）
  - 常规依赖更新，将 Docker 基础镜像从 Alpine 3.23 升至 3.24，属低风险 CI 维护。

**整体评估：** 两项流式工具调用 PR 关闭意味着核心能力已合入；两项代理路由安全修复（#983、#982）指向网络层深度优化，项目在网络传输安全和兼容性上向前迈进了一步。

---

## 4. 社区热点

**Issue #915** [OPEN] — **[bug] Problem with scheduler unauthorized**（作者: scabros）
- 👍 1 | 💬 4 条评论 | 创建于 2026-05-15，最近更新 2026-08-03
- **摘要：** 用户运行 NullClaw（Ubuntu 系统，Ollama 外部主机同网段，qwen3.6:27b on RTX 3090）。LLM 本身及工具调用基本正常，但调度器（scheduler）在 Telegram 聊天及 Web 端均无法工作。
- **分析：** 该 Issue 持续近三个月仍在活跃讨论，属于长期未解决的中高影响问题。4 条评论表明用户与维护者之间已有多次往返（可能是调试信息交换）。调度器是自动化任务的关键路径，后台运行失效会直接影响核心使用场景。
- **链接：** [Issue #915](https://github.com/nullclaw/nullclaw/issues/915)

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🔴 高 | #915 | **调度器 unauthorized** — 在 Telegram/聊天界面均无法运行调度器，已持续近 3 个月（创建 2026-05-15，更新 08-03），评论 4 条 | 仍开放，无关联 fix PR |
| 🟡 中 | #982 | **Telegram Bot API 代理路径未走 curl 传输** — 显式配置代理时请求路径不一致，可能导致代理场景下连接失败或超时 | 修复 PR 已提交，待合并 |
| 🟡 中 | #983 | **提供商代理请求凭据可能泄漏至 argv** — 非流式提供商 POST 请求在代理场景下未复用安全 curl 路径，凭据头存在 argv 暴露风险 | 修复 PR 已提交，待合并 |

**小结：** 今日无新增已确认的高严重 Bug 报告。#983 与 #982 两条修复 PR 均在代理/网络传输层面提升安全性与稳定性，是此前问题（如 #915 类似网络配置问题）的关联性预防措施。

---

## 6. 功能请求与路线图信号

**潜在纳入下一版本：**

- **流式工具调用（Streaming Tool Calls）** — #964 与 #965 今日关闭，标志此项能力大概率已出现在主分支中。需要 API 级工具调用的 Agent 场景（如实时工具响应）将在下个正式版本中获得完整支持。
- **代理网络路径硬化** — #983 与 #982 展示了明确方向：所有显式代理请求统一走 curl 传输层，保证凭据安全、超时一致、DNSSEC 级别的 pinned resolve 支持。这对企业级部署（必须走代理出口）有直接价值，预期会随这两个 PR 合入而体现在下个版本中。

**暂无明显新功能请求信号**——今日仅有的 #915 为 Bug 报告，未涉及新功能提案。

---

## 7. 用户反馈摘要

| 来源 | 用户反馈要点 |
|------|-------------|
| Issue #915 | 用户在 RTX 3090 + qwen3.6:27b 环境下，LLM 推理及工具调用整体正常，但调度器功能不可用（Telegram 与 Web 端均受影响），表明核心功能体验良好，但自动化调度模块存在明显短板 |
| PR #982 | 创作者指出 "live channel probe already" 存在代理路径不一致的问题，暗示维护者已知晓 Telegram 代理边界场景下的行为偏差，正在补全 |

**场景洞察：** 典型用户为自托管 + 外部 LLM（Ollama）+ Telegram 接入的中小型部署。性能和模型兼容性满意度高，但调度器可靠性是用户痛点，若长期未修复可能影响用户续用意愿。

---

## 8. 待处理积压

| 类型 | 编号 | 标题 | 创建时间 | 最近更新 | 天数 | 备注 |
|------|------|------|---------|---------|------|------|
| ⚠️ Issue | #915 | [bug] Problem with scheduler unauthorized | 2026-05-15 | 2026-08-03 | **81 天** | 长时间无 fix PR，需维护者介入排查或标记优先级 |
| ⚠️ PR | #956 | ci(deps): bump alpine from 3.23 to 3.24 | 2026-06-15 | 2026-08-03 | **50 天** | Dependabot 自动 PR，长期未合并，建议尽快处理避免 CI 依赖过期 |

**维护者提醒：**
1. #915 已持续开放 81 天，虽无大量复现报告，但调度器为高影响核心功能，建议优先定位根因（可能与认证层 session 处理或与外部 Ollama host 的网络鉴权有关）。
2. #956 为低风险 CI 依赖更新，积压接近 2 个月，建议按常规合并节奏尽快处理，避免基础镜像安全补丁过期。

---

*本报告基于 NullClaw GitHub 仓库公开数据生成，数据采集时间窗口为 2026-08-03 至 2026-08-04（24 小时）。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-08-04

---

## 1. 今日速览

IronClaw 在过去 24 小时内维持了极高的开发活跃度：共产生 45 条 Issue 更新（36 条新开）和 50 条 PR 更新（32 条待合并），Wave 3 架构重构的多条大型 PR 集中推进。今日无新版本发布，但值得关注的是，近期提交集中在 Reborn 架构分层（WS2/WS3）、CI 门禁可靠性修复和扩展生命周期管理上，同时 bug_bash 产出了一批 P1/P2 用户可见问题。健康度总体良好：核心团队交付节奏稳定，但 CI 计划器（Reborn test planner）的多个缺口正在阻塞大 PR 合入，是当前最大瓶颈。

---

## 3. 项目进展

> 今日无新版本发布，此部分聚焦已合并/关闭的 PR 与推进的架构工作。

**已合并/关闭的重点 PR：**

| PR | 内容 | 影响 |
|---|---|---|
| [#7064](https://github.com/nearai/ironclaw/pull/7064) | **模型网关与工具披露迁入 loop_host**（WS3/WS4 重构，XL） | 纯移动 + 两行 `layer =` 变更，零测试损失；完成 PROPOSAL §6.7.2 的模型网关下沉目标 |
| [#7040](https://github.com/nearai/ironclaw/pull/7040) | **关闭 WS2 遗留项与 WS2.1 跟进**（L） | 三行 WS2 检查项收盘；修正了其中两行过时的声明 |
| [#7070](https://github.com/nearai/ironclaw/pull/7070) | **修复主分支 E2E 覆盖率**（M） | 自 #6876 以来变红的 5 个 WebUI v2 E2E 测试全部修复；含两个生产行为修正（SSE keep_alive 游标、admin 加载重试） |
| [#7024](https://github.com/nearai/ironclaw/pull/7024) | **注册时解析自定义 MCP 认证**（XL） | 在包定义被接收前解析认证；`Auto` 模式改为无凭证握手，成功即解析为 `NoAuth` |
| [#7049](https://github.com/nearai/ironclaw/pull/7049) | **每周三生产发布策略文档** | 确定了周一至周一 sprint 节奏、周一 RC 切版、周二 QA、周三发布的自愿流程 |
| [#7023](https://github.com/nearai/ironclaw/pull/7023) | **依赖批量升级**（6 项：base64/toml/rstest 等） | 保持依赖新鲜度，无破坏性变更 |

**Wave 3 整体进展判断：** 今日有多达 7 个 WS3 相关 PR 处于 open 状态（#7084、#7065、#7094、#7096、#7080、#7090、#7064 已合并），已覆盖 sandbox lane 合并、MCP 契约翻转、secrets 消费者收紧、skill-install executor 迁移等关键行。WS2 已基本收盘，WS3 进入密集执行阶段。

---

## 4. 社区热点

**#6284 — [CLOSED] 错误可恢复性终局 Epic（15 评论）**
[链接](https://github.com/nearai/ironclaw/issues/6284)

该 Epic 定义了"每次运行中错误必须满足可恢复契约"的五项要求（运行存活、模型可见、携带原因与成功路径、模型获得行动回合、不报告非成功状态）。虽已关闭，但作为顶层架构纲领，其关闭意味着各项子任务已分配到各工作流。这是理解当前大量"错误处理"相关 PR 的上下文锚点。

**#7087 — Reborn PR 测试计划器对特定路径硬失败（3 评论）**
[链接](https://github.com/nearai/ironclaw/issues/7087)

该问题直接阻塞了 Wave 3 的 `wit/` 移动 PR #7084（18/46 变更路径被错误标记）。社区核心成员 BenKurrek 已在该 PR 中附带修复（`1f66b58`），属于"发现问题→当场解决"的高效模式。但同类问题 #7060、#7083 显示 Reborn 范围分类器的路径覆盖逻辑存在系统性缺陷。

**#7077 — 一次厂商授权覆盖所有共享账户的扩展（PR，2 评论）**
[链接](https://github.com/nearai/ironclaw/pull/7077)

修复 #7069（Google 服务重复认证，bug_bash_P1）。用户侧诉求强烈：多次授权同一 Google 账户是明显的体验痛点，该 PR 直接从架构层面解决（vendor recipe 合并），而非打补丁。

**分析：** 今日社区讨论焦点集中在 **（a）** Reborn 架构重构的 CI 基础设施阵痛、（**b**）认证体验的一致性、（**c**）错误恢复的契约化。三者都指向同一个方向：项目正在从"功能堆叠"转向"架构规范化"阶段，短期阵痛显现在 CI 工具链上。

---

## 5. Bug 与稳定性

### P1 级

| Issue | 描述 | 状态 |
|---|---|---|
| [#7074](https://github.com/nearai/ironclaw/issues/7074) | **多工具会议研究在获取日历数据后失败** — 模型尝试调用不可用函数 | 无 fix PR |
| [#7069](https://github.com/nearai/ironclaw/issues/7069) | **Google 服务需重复认证** — 每项服务单独走 OAuth 流程 | ✅ [#7077](https://github.com/nearai/ironclaw/pull/7077) 已提交修复 |
| [#7041](https://github.com/nearai/ironclaw/issues/7041) | **[QA] WASM guest 诊断可通过运行时/模型/tracing 泄露可检测密钥** | 无 fix PR；#7048（stacked）可能相关 |

### P2 级

| Issue | 描述 | 状态 |
|---|---|---|
| [#7071](https://github.com/nearai/ironclaw/issues/7071) | 每次流式更新都显示 "Reconnecting" 状态 | 无 fix PR |
| [#7075](https://github.com/nearai/ironclaw/issues/7075) | 运行失败后智能体忽略用户追问，继续之前的失败任务 | 无 fix PR |
| [#7073](https://github.com/nearai/ironclaw/issues/7073) | 智能体向用户暴露内部工具名和投递路由细节 | 无 fix PR |
| [#7072](https://github.com/nearai/ironclaw/issues/7072) | Telegram 消息渲染原始 Markdown 而非格式化文本 | 无 fix PR |

### CI/工具链缺陷（阻塞性）

| Issue | 描述 | 状态 |
|---|---|---|
| [#7087](https://github.com/nearai/ironclaw/issues/7087) | Reborn 测试计划器对 `.claude/` 等路径硬失败 | ✅ 已在 [#7084](https://github.com/nearai/ironclaw/pull/7084) 中附带修复 |
| [#7081](https://github.com/nearai/ironclaw/issues/7081) | Docker fail-closed 测试门禁未接线（`IRONCLAW_REQUIRE_DOCKER_TESTS` 从未设置） | 无 fix PR |
| [#7085](https://github.com/nearai/ironclaw/issues/7085) | `check-version-bumps.sh` 在 macOS 上静默跳过版本交叉检查（BSD sed 不支持 `\+`） | 无 fix PR |
| [#7060](https://github.com/nearai/ironclaw/issues/7060) | 平台拥有的 WIT/扩展包变更无法通过 Reborn 范围分类器 | 无 fix PR |
| [#7083](https://github.com/nearai/ironclaw/issues/7083) | `crates/extensions/` 下 5 个 crate 对覆盖率工具完全不可见 | ✅ [#7094](https://github.com/nearai/ironclaw/pull/7094) 声称解决 |

### 其他功能性缺陷

| Issue | 描述 | 状态 |
|---|---|---|
| [#7082](https://github.com/nearai/ironclaw/issues/7082) | `builtin.skill_install` 内联多文件安装不可达；URL 安装静默丢弃 files/source 字段 | 无 fix PR（CodeRabbit 在 [#7080](https://github.com/nearai/ironclaw/pull/7080) 中发现） |
| [#7068](https://github.com/nearai/ironclaw/issues/7068) | Hosted MCP 的 `destructiveHint` 省略时默认为 `false`，与 MCP 规范（默认 `true`）不符 | 无 fix PR |
| [#7078](https://github.com/nearai/ironclaw/issues/7078) | 共享供应商 OAuth 范围上限是仓库级而非调用者级 | 无独立 fix PR（由 #7077 放大） |

---

## 6. 功能请求与路线图信号

**明确的功能请求：**

- **[#7097](https://github.com/nearai/ironclaw/issues/7097) — 计费页添加支持升级路径**（p2/feedback）：用户不确定 NEAR AI 计费问题由谁处理。该请求虽然直接实现成本低，但涉及跨团队职责定义，需产品侧确认。

- **[#7044](https://github.com/nearai/ironclaw/issues/7044) — 频道优先上手体验**（epic）：新用户面对空白 WebUI 不知从何开始。当前已有配套原型 PR [#6994](https://github.com/nearai/ironclaw/pull/6994)（OOBE 自动化任务原型，UI-only），释放了强烈信号：**下一版本很可能包含全新用户引导流程**。

- **[#7046](https://github.com/nearai/ironclaw/issues/7046) — 从 AI 对话配置所有工具/频道/扩展**（epic）：将配置体验从 WebUI 迁移到对话界面。与 #6941（技能自创建/自选择）、#7088（自定义 MCP 注册暴露给模型）形成合力，**"对话即配置"可能是 IronClaw 下一阶段的核心体验主题**。

- **[#6941](https://github.com/nearai/ironclaw/issues/6941) — 模型可自创建、发现、选择、使用高回报技能**（epic）：从 #6565 拆出的子集，包含技能描述符索引、漂移生命周期、分级安全裁决等 5+ 个大型验收标准。该方向与 #7046 互补，是中长期能力目标。

**路线图信号判断：** 结合 PR #7049（每周三发布策略）和 #6994（OOBE 原型），8 月中旬的版本大概率包含：**新用户引导流程（carousel + agent-mode pill）、认证体验修复（#7077）、扩展生命周期管理增强（#6957）**。

---

## 7. 用户反馈摘要

**认证体验（来自 #7069）：**
> "每个 Google 服务都要求单独认证，即使用户已多次完成 Google 授权流程" —— 用户对重复 OAuth 流程明确不满。这是 bug_bash_P1 中最贴近日常使用场景的痛点。

**流式连接不稳定感（来自 #7071）：**
> 每次流式响应块都显示 "Reconnecting"，尽管流式传输持续成功。状态指示器在块之间反复闪烁。 —— 该问题伤害用户对连接稳定性的信任感，即便实际功能正常。

**错误恢复缺口（来自 #7075）：**
> 运行失败后（如 "model provider was unavailable"），智能体忽略用户的追问并恢复之前的失败任务。 —— 用户期望失败后能自然切换话题，但智能体仍固执于旧任务。这与 #6284 Epic 的"每次错误必须让模型获得行动回合"目标直接相关，说明该契约尚未在运行时完全落地。

**信息泄露观感（来自 #7073）：**
> 智能体在用户可见回复中暴露内部工具名称和投递路由逻辑。 —— 用户期望"简单、友好"的解释，对技术细节暴露表示不适。

**技能安装行为不一致（来自 #7082，CodeRabbit 发现）：**
> 内联多文件安装不可达；URL 安装会静默丢弃 files/source/source_url。 —— 属于"接受输入但不消费"的静默失败模式，用户在技能安装时会发现功能"不工作"但无明确报错。

**Markdown 渲染缺失（来自 #7072）：**
> Telegram 消息将 Markdown 语法作为纯文本显示。 —— 渠道层的基础格式能力缺失，影响日常沟通效率。

---

## 8. 待处理积压

**长期未合并的 PR：**

- **[#5598](https://github.com/nearai/ironclaw/pull/5598) — `chore: release`（7 月 3 日创建，仍在 open）**：`ironclaw_common` 0.4.2→0.5.0（⚠ breaking）、`ironclaw_skills` 0.3.0→0.4.0（⚠ breaking）。搁置超过一个月。结合 #7049 的周三发布策略，该 PR 可能需要按新策略重新走流程。

- **[#6957](https://github.com/nearai/ironclaw/pull/6957) — `feat(reborn-ironhub): manage installed package lifecycle`（7 月 31 日创建）**：持久化有界、脱敏的 IronHub 安装回执，添加 `ironhub.status` 和 `ironhub.update` 操作。等待合入中，是扩展生命周期管理方向的核心能力。

- **[#6994](https://github.com/nearai/ironclaw/pull/6994) — WebUI OOBE 原型（8 月 1 日创建）**：rebase 后等待 review，无阻塞但需要设计评审确认。

**需要维护者关注的 Issue：**

- **CI 工具链的系统性缺陷（#7087/#7081/#7085/#7060/#7083）**：已有多人（BenKurrek、theredspoon）连续报告 Reborn 范围分类器和门禁接线问题。建议安排一次专门的 CI 基础设施冲刺集中修复，否则每条大 PR 都会触发"planner gap"类问题。

- **[#7041](https://github.com/nearai/ironclaw/issues/7041) — WASM guest 诊断的密钥泄露风险**：QA 发现的安全问题，目前无直接 fix PR，建议优先评估。

- **[#7091](https://github.com/nearai/ironclaw/issues/7091) — WS8: HostRuntimeServices 上 3 个无调用者的公共 builder 方法**：建议在 Wave 4 的清理工作中处理（或删除，或标记 `#[doc(hidden)]`）。

---

*数据来源：[IronClaw GitHub 仓库](https://github.com/nearai/ironclaw)，统计窗口 2026-08-03 至 2026-08-04。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-04

## 1. 今日速览

项目今日保持中等活跃度：过去 24 小时共有 2 条 Issue 更新和 11 条 PR 更新，其中 6 条 PR 已合并/关闭（含 4 条今日新提交），5 条仍待合并。今日无新版本发布。值得关注的是，多标签 PR 集中在 `renderer`、`docs`、`main`、`cowork` 等核心区域，其中 4 条来自同一位贡献者（liuzhq1986）且存在 revert 操作，可能与内部协调节奏有关。另有 5 条 PR（#1208、#1209、#1212、#1214）自 4 月以来一直处于 open 状态，形成积压。整体来看，项目处于正常迭代状态，基础设施类 PR（依赖升级、NSIS 修复）和功能类 PR（活动筛选、推荐活动）并行推进。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 呈现两条主要推进线索：

**功能增强线：**

- **侧边栏多代理任务活动筛选**（[PR #2418](https://github.com/netease-youdao/LobsterAI/pull/2418)，已合并）：新增受 Codex 启发的任务活动筛选按钮，支持在多个代理间快速定位需关注的任务，为多代理协作场景提供更高效的任务管理入口。
- **启动积分活动**（[PR #2419](https://github.com/netease-youdao/LobsterAI/pull/2419)，已合并）：为 Windows 桌面客户端新增可配置的启动积分活动体验，面向网易获客拉新场景，包含活动弹窗、新会话页持久入口及登录延续逻辑，说明项目在商业化/用户增长侧有所动作。
- **NSIS 安装器存活进程清理加固**（[PR #2420](https://github.com/netease-youdao/LobsterAI/pull/2420)，已合并）：修复 Windows 安装/升级过程中因 Stop-Process 仅执行一次而导致的进程残留问题，改为在每轮轮询中重复终止并记录进程细节日志，提升安装器可靠性。

**疑似协调操作**：liuzhq1986 在今日提交了 [PR #2422](https://github.com/netease-youdao/LobsterAI/pull/2422)（fix btw tools）→ [PR #2423](https://github.com/netease-youdao/LobsterAI/pull/2423)（Revert "Liuzhq/fix btw tools"）→ 两者均已关闭，可能是误提交后主动撤回，也可能代表该修复方案被整体推翻，需要维护者确认后续计划。

整体来看，项目在 Windows 平台稳定性、多代理交互效率及用户增长侧均有实际推进。


## 4. 社区热点

今日最受关注的内容为**「导出为 Markdown」功能**的 Issue 与配套 PR 联动：

- [Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213)（功能建议）：用户 MaoQianTu 提出为会话详情页添加导出为 Markdown 的功能，当前仅支持导出为图片，导致引用、整理、分享不便。该 Issue 获得 1 条评论支持。
- [PR #1214](https://github.com/netease-youdao/LobsterAI/pull/1214)（待合并）：同一用户提交了完整实现，复用现有 `buildDisplayItems` 和 `buildConversationTurns` 生成 Markdown，工具调用以摘要+代码块呈现并自动截断，头部包含会话标题、导出时间等信息。

Issue 与 PR 同日出现且互相呼应，说明用户不满足于停留在建议层面，而是直接给出了实现方案；可能被优先纳入下一版本评审。

另一热点是 [#1206 Kimi2.5 模型重复回复问题](https://github.com/netease-youdao/LobsterAI/issues/1206)，该问题为私有化部署用户遇到的行为异常，影响文档分析任务的流畅性，评论区已有 1 条互动，反映出私有化部署场景下的稳定性需求。

## 5. Bug 与稳定性

| 严重程度 | 问题 | 状态 | Fix PR |
|---|---|---|---|
| 中 | **Kimi2.5 模型分析文档时重复回复当前动作**（[Issue #1206](https://github.com/netease-youdao/LobsterAI/issues/1206)）：私有化部署环境下，文档分析任务拆分为源码分析和编译流程时反复提示同一步骤，用户无法判断是卡住还是正常等待。切换模型后恢复，但当前任务必现。 | Open，已标记 stale | 暂无 |
| 中 | **[PR #2420 已修复] NSIS 安装器进程残留**：Stop-Process 仅执行一次导致进程可逃过轮询检测，安装/升级可能遇到"文件被占用"类问题。 | 已合并修复 | [PR #2420](https://github.com/netease-youdao/LobsterAI/pull/2420) |
| 中 | **[PR #1209 待合并] Chrome 自动化标记残留**：`--disable-blink-features=AutomationControlled` 由外部注入（残留 user data、外部配置、环境变量）导致 web-search 功能被 Chrome 拦截。修复方案为拦截该 flag 并提示用户清理环境。 | Open，已标记 stale | [PR #1209](https://github.com/netease-youdao/LobsterAI/pull/1209) |

当前无崩溃级或数据丢失类严重问题。

## 6. 功能请求与路线图信号

- **导出为 Markdown**（[Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213) / [PR #1214](https://github.com/netease-youdao/LobsterAI/pull/1214)）：实现完整、与现有代码结构高度复用，被合并的可能性较高；如果进入下一版本，将显著提升会话数据的可移植性和二次编辑效率。
- **Co-work 手动重试按钮**（[PR #1208](https://github.com/netease-youdao/LobsterAI/pull/1208)）：针对 429/网络故障/服务端错误提供一键重试，解决用户需要手动重发上一条消息的痛点。该 PR 已附带完善的错误分类模块（`RETRYABLE_ERROR_KEYS`），设计完成度较高，但已 stale 悬置 4 个月，建议维护者明确排期或关闭。
- **自定义模型供应商上限扩展**（[PR #1212](https://github.com/netease-youdao/LobsterAI/pull/1212)）：将自定义供应商从 10 个扩展至 20 个，解决高级用户在保留旧配置与添加新供应商之间的冲突。改动集中在 renderer 层，风险较低，也处于 stale 状态。

这三项功能需求均来自活跃用户使用场景，且 PR 已就绪，建议维护者尽快评审合并，避免社区贡献者流失。

## 7. 用户反馈摘要

- **Kimi2.5 重复回复**（[Issue #1206](https://github.com/netease-youdao/LobsterAI/issues/1206)）：用户在私有化部署环境中无法判断"是出 bug 还是需要继续等待"，暴露了当前模型状态提示机制的不足——建议增加动作状态的非重复性展示或"等待中"的明确指示。
- **导出为 Markdown**（[Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213)）：用户明确表达"截图或手动复制操作繁琐，且图片格式不便于后续编辑和检索"，说明知识管理型用户对会话数据二次加工有较强需求。
- **自定义供应商上限**（[PR #1212](https://github.com/netease-youdao/LobsterAI/pull/1212)）：用户"保留旧自定义配置的同时切换新供应商"受阻，反映出多模型供应商管理在真实工作流中的刚需。

## 8. 待处理积压

以下高价值 PR/Issue 已长期悬置（均自 4 月 1 日起未获响应，已被标记为 stale）：

**PR 积压（均有完整实现，等待评审）：**

- [PR #1208](https://github.com/netease-youdao/LobsterAI/pull/1208)：Co-work 手动重试按钮——已含错误分类模块设计（120 天+）
- [PR #1209](https://github.com/netease-youdao/LobsterAI/pull/1209)：web-search Chrome flags 拦截修复——根因分析完整，附来源排查表（120 天+）
- [PR #1212](https://github.com/netease-youdao/LobsterAI/pull/1212)：自定义模型供应商上限 10→20——改动集中、风险低（120 天+）
- [PR #1214](https://github.com/netease-youdao/LobsterAI/pull/1214)：导出为 Markdown 功能——与 Issue #1213 联动，设计完整（120 天+）

**Issue 积压：**

- [Issue #1206](https://github.com/netease-youdao/LobsterAI/issues/1206)：Kimi2.5 重复回复——影响私有化部署的文档分析体验，无 fix PR（120 天+）
- [Issue #1213](https://github.com/netease-youdao/LobsterAI/issues/1213)：导出为 Markdown——已有完整实现 PR 待合并（120 天+）

**依赖升级自动 PR：**

- [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)：electron 40.2.1 → 43.2.0 跨大版本升级（含 electron-builder），需评估破坏性变更。该 PR 已悬置 120+ 天

**维护者建议**：4 月 1 日当天集中产生的这批 PR/Issue 距今已超过 120 天，若长期不响应社区贡献，可能影响项目在 AI 助手开源社区中的活跃度和贡献者留存度。建议优先评审上述已就绪的 PR，或明确关闭并说明理由，避免 stale 标签掩盖有效工作量。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-04

> 数据采集周期：2026-08-03 至 2026-08-04 | 数据来源：GitHub API

---

## 1. 今日速览

Moltis 项目过去 24 小时整体活跃度处于**中低水平**，具体表现为：无新 Issue 提交、无 Issue 关闭、无版本发布，仅新增 1 条待合并 PR（#1183）。值得关注的是，该 PR 涉及 MCP 托管仓库集成的核心功能扩展，涵盖凭据管理、SSH 传输、vault 生命周期集成等多个子系统，工作量较大，是近期项目推进的重点方向。活跃度放缓可能意味着团队正处于 PR 评审和合并周期，而非功能停滞期。

---

## 3. 项目进展

过去 24 小时**无已合并或关闭的 PR**，无功能性代码合入主干分支。当前唯一活跃的 PR 为：

**#1183 — feat(mcp): add managed repository bundles**（[链接](https://github.com/moltis-org/moltis/pull/1183)）
- **作者**：penso | **创建**：2026-08-02 | **更新**：2026-08-03
- **状态**：待合并（OPEN）
- **内容**：该 PR 为 MCP 服务器引入"受管 Git 仓库包"机制，支持发现、预览、安装、更新、回滚和移除操作。同时包含 HTTPS 凭据支持、受管 SSH 传输（pinned）、vault 生命周期集成，以及基于导入仓库的 MCP 配置支持。该 PR 还简化了 Web 端 onboarding 流程。

**项目健康度评估**：虽然 24 小时内无新合并，但 #1183 自 8 月 2 日创建至今持续活跃更新，说明项目维护者正在积极迭代这一重大功能。建议在下个版本发布中重点关注此 PR 何时进入合并队列。

---

## 4. 社区热点

**当前周期内唯一活跃 PR**：

- **#1183**（[链接](https://github.com/moltis-org/moltis/pull/1183)）：该 PR 聚焦于 MCP 服务器的集中式生命周期管理——从发现到回滚的完整链条。社区对该功能的关注点可能集中在：MCP 服务器安装/更新/回滚的一致性和安全性。一个值得关注的信号是该 PR 同时涉及 vault 集成，说明用户对凭据安全管理的需求正在上升，尤其是当 MCP 需要访问私有 Git 仓库时。

> 由于当前无 Issue 提交或评论，今日社区讨论热度偏低。项目氛围偏向"开发专注期"。

---

## 5. Bug 与稳定性

**过去 24 小时报告 Bug 数：0**

无新 Bug 提交、无崩溃报告、无回归问题。项目在该维度处于稳定状态。

---

## 6. 功能请求与路线图信号

当前无新增功能请求 Issue。但结合 PR #1183 观察，以下方向可能进入下一版本路线图：

| 信号 | 来源 | 判断依据 | 潜在影响 |
|------|------|----------|----------|
| MCP 服务器生命周期管理 | PR #1183 | 覆盖发现→卸载全流程，且支持回滚 | 未来可能成为 MCP 生态的标准管理方式 |
| 多类型 Git 凭据支持 | PR #1183 | HTTPS 凭据 + pinned SSH + vault 集成 | 用户对安全性和灵活性的双重诉求 |
| Web onboarding 简化 | PR #1183 | 明确"simplify web onboarding"目标 | 降低新用户上手门槛 |

可以合理推判，MCP 托管管理将是下一版本的核心模块。

---

## 7. 用户反馈摘要

过去 24 小时**无可提取的用户评论或 Issue 讨论**。

从 PR #1183 的变更范围反推需求背景：用户痛点可能集中于——（a）MCP 服务器的安装过程分散、难以统一管理；（b）Git 凭据配置繁琐且不安全；（c）版本升级后难以回滚。该 PR 的提出与上述诉求高度契合，侧面验证了这些需求的真实性。

---

## 8. 待处理积压

**过去 24 小时无新增积压**。当前唯一待处理事项为 PR #1183，等待维护者评审与合并。

---

**整体项目健康度评价**：

| 维度 | 状态 | 说明 |
|------|------|------|
| 🔵 活跃度 | 中低 | 无 Issue/版本活动，单一 PR 在开发中 |
| 🟢 稳定性 | 良好 | 无 Bug 报告、无回归 |
| 🟡 关键路径 | 推进中 | #1183 为大型 PR，合并周期可能较长 |

**建议关注点**：PR #1183 的评审进展；下周是否有新版本发布计划；MCP 管理功能是否会带来破坏性变更（如配置格式变化）。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-04

> CoPaw (github.com/agentscope-ai/CoPaw) · 数据窗口: 2026-08-03 至 2026-08-04


## 1. 今日速览

过去 24 小时项目保持**高活跃度**：共产生 22 条 Issue 更新与 50 条 PR 更新，并发布 v2.1.0-beta.1 新版本。值得关注的是，Issue 侧出现了多起与 `agentscope 2.0.4.post1` 兼容性相关的崩溃报告（#6612、#6619），以及围绕 `spawn_subagent` 的参数处理缺陷（#6588）引发的重复 PR；同时，CI 基础设施的稳定性问题（如 fork PR 的 real-behavior-proof 检查失败）也得到了快速修复。社区反馈呈现两极：一方面，用户对功能缺失（如多智能体引导、任务产出物目录结构）提出建设性意见；另一方面，Shell 命令超时、UI 冻结等稳定性问题持续困扰用户。总体来看，项目正处在 **Beta 发布前的密集修复与功能收尾阶段**。


## 2. 版本发布

### v2.1.0-beta.1

**发布时间**: 2026-08-03

**更新亮点**:
- **fix(chat)**: 修复新聊天中残留旧频道身份信息导致上下文串扰的问题
- **feat(inbox)**: 待审批请求到达时侧边栏 inbox 图标抖动提醒，并新增按类型区分颜色的徽章圆点

**破坏性变更**: 无明确标注。

**迁移注意事项**: 属于 Beta 版本，建议在测试环境验证后使用。


## 3. 项目进展

今日合并/关闭的 PR 有效推进了以下方向的修复与功能完善：

| 方向 | PR | 说明 |
|------|----|----|
| **CI 可靠性** | [#6653 fix(ci): fence-aware section extraction](https://github.com/agentscope-ai/CoPaw/pull/6653) | 修复 real-behavior-proof 检查将 fenced Evidence 块完全剥离的问题（修复 #6626） |
| | [#6654 cap playwright below 1.62](https://github.com/agentscope-ai/CoPaw/pull/6654) | 解决 macOS 桌面验证超时无输出的问题，解除 release 阻塞 |
| | [#6646 fetch PR body via API for fork PRs](https://github.com/agentscope-ai/CoPaw/pull/6646) | 修复 fork PR 的 CI 检查因 `pull_request_target` 事件剥离 PR body 而失败的问题（修复 #6563），保障社区贡献流程顺畅 |
| **桌面端** | [#6579 use bundled Python for script execution](https://github.com/agentscope-ai/CoPaw/pull/6579) | 执行生成的 Python 脚本时改用内置解释器，避免依赖系统 Python（对应 Issue #6160） |
| **Agent 参数处理** | [#6609 Fix spawn subagent schema](https://github.com/agentscope-ai/CoPaw/pull/6609) | 修正 `spawn_subagent` 的参数 schema，使 `batch` 等可选参数在单任务调用时不再被误判为必填（对应 #6588） |
| **Windows 稳定性** | [#6203 bound and hide Windows tasklist probe](https://github.com/agentscope-ai/CoPaw/pull/6203) | 为 Windows 下 PID 存活探测的 `tasklist` 调用增加超时与窗口隐藏，避免无界阻塞与弹窗 |

在 PR 中，**模型自动降级/fallback 机制**（#6659、#2199）与 **Skill 列表加载瘦身**（#6650）是推进较深的功能增强，前者引入冷却机制避免反复击穿故障模型，后者将 Skill 列表 API 从 MB 级全量内容改为轻量摘要 + 按需详情，直接回应了慢网络下的加载失败问题（#6633、#6635）。


## 4. 社区热点

1. **[#6537 Skill tags disappear on restart](https://github.com/agentscope-ai/CoPaw/issues/6537) — 11 条评论 (已关闭)**
   - 现象：Skill Pool UI 设置的标签在重启后丢失，但 `skill.json` 已正确保存。
   - 根源：启动或构建时 manifest 对账阶段将标签覆盖。
   - 热度原因：数据未丢失但 UI 状态丢失，涉及用户核心配置的持久化信任问题，回归自 #3270。

2. **[#6649 Support GPT-5.6 prompt caching parameters](https://github.com/agentscope-ai/CoPaw/issues/6649) — 8 条评论**
   - 诉求：在 Responses API provider 中支持 `prompt_cache_key`、`prompt_cache_options`、`prompt_cache_breakpoint` 参数，降低多轮对话延迟与成本。
   - 热度原因：直接关系到 Agent 循环的推理成本与速度，属于 LLM 接入层的关键能力。

3. **[#6588 `spawn_subagent` treats empty `batch` placeholders as batch mode](https://github.com/agentscope-ai/CoPaw/issues/6588) — 6 条评论**
   - 现象：单任务调用时，部分 Responses 兼容模型会返回空 `batch` 占位符，被误判为批处理模式。
   - 热度原因：虽是小参数问题，但真实影响单任务调用的正确性，且已引发两个修复 PR（#6595、#6658），说明修复方案仍在讨论中。


## 5. Bug 与稳定性

按严重程度排列：

**🔴 高危（核心功能不可用/会话阻塞）**

- **[#6608 Long-running shell commands bypass timeout and block feishu session](https://github.com/agentscope-ai/CoPaw/issues/6608)** — 长时间运行的 `execute_shell_command` 绕过 `shell_command_timeout`，阻塞飞书会话 1.5 小时（含孤儿子进程）。**暂无 fix PR，需优先关注。**
- **[#6612 Incompatible with agentscope 2.0.4.post1: proactive crashes + tool-permission deadlock](https://github.com/agentscope-ai/CoPaw/issues/6612)** — 与当前 `agentscope 2.0.4.post1` 不兼容，导致 proactive 子系统崩溃与工具权限死锁。
- **[#6619 "ToolCallBlock has no field extra_content" crash in openai_chat_model_compat](https://github.com/agentscope-ai/CoPaw/issues/6619)** — 同样源于 agentscope 版本升级后的字段缺失，影响流式响应解析。

**🟠 中危（功能受损/体验严重下降）**

- **[#6647 Desktop UI goes fully black when WebView2 crashes](https://github.com/agentscope-ai/CoPaw/issues/6647)** — WebView2 进程崩溃后 UI 全黑，无恢复路径，用户只能强制关闭。
- **[#6635 / #6633 Console & Skills pages fail on slow networks](https://github.com/agentscope-ai/CoPaw/issues/6635)** — 所有 API 响应未压缩且体积达 MB 级，前端 30 秒固定超时导致页面加载失败；**PR #6650 已提交瘦身方案**。
- **[#6614 WeChat cron pushes never delivered (ret=-2 context_token invalid)](https://github.com/agentscope-ai/CoPaw/issues/6614)** — 微信定时推送静默失败 8 天，任务显示 success 但实际未送达，已消耗约 44M tokens。

**🟡 低危（功能缺陷/体验瑕疵）**

- **[#6565 Multi-line commands collapsed + PIPE background process hangs](https://github.com/agentscope-ai/CoPaw/issues/6565)** — 引号外换行被折叠为空格导致语法错误；Linux PIPE 模式下后台进程卡住。
- **[#6589 `execute_shell_command` huge output freezes UI](https://github.com/agentscope-ai/CoPaw/issues/6589)** — 数万行 stdout 一次性渲染阻塞 UI 主线程。

**✅ 已关闭（含修复）**

- **#6537 Skill tags disappear on restart** — 已定位根因（manifest 对账覆盖），已关闭。
- **#6655 Console 通道不渲染审批提示** — 已关闭。
- **#6626 Real behavior proof CI gate strips fenced Evidence** — 已由 PR #6653 修复。


## 6. 功能请求与路线图信号

| Issue | 诉求 | 对应 PR/路线图信号 |
|-------|------|------------------|
| [#6649 GPT-5.6 prompt caching](https://github.com/agentscope-ai/CoPaw/issues/6649) | 支持 prompt 缓存参数，降低多轮成本 | 暂无直接 PR，但属 provider 层通用能力，预计后续版本会跟进 |
| [#6643 任务产出物按任务分目录](https://github.com/agentscope-ai/CoPaw/issues/6643) | 产出物不堆在 media 目录，按任务隔离 | **PR #6651**（Files 管理 REST API）是前置基础设施，两者可协同落地 |
| [#6642 拖入文件直接读取原路径](https://github.com/agentscope-ai/CoPaw/issues/6642) | 免上传/复制，直接读原路径文件 | 与 #6643 属同源诉求：减少 media 目录文件堆积 |
| [#6659 model fallback with cooldown](https://github.com/agentscope-ai/CoPaw/pull/6659) | 模型自动故障切换 + 冷却机制 | 已在 PR 阶段，修复 #2199、#1327、#2089 |
| [#6651 Files REST API](https://github.com/agentscope-ai/CoPaw/pull/6651) | 补齐文件/文件夹管理 6 个缺失操作 | 为 Files 页面提供完整后端能力，推动前端文件管理页面落地 |
| [#6657 sandbox constraint reporting](https://github.com/agentscope-ai/CoPaw/pull/6657) | 后端无法执行的沙箱配置应显式报告 | 消除安全配置静默失效的隐患 |

**线路图信号**：任务产出物管理（#6643、#6642）+ Files API（#6651）的组合，暗示项目正在向更完善的文件管理和工作区组织方向演进。


## 7. 用户反馈摘要

- **正向反馈**：
  - 用户对 `spawn_subagent` 参数问题的快速响应持肯定态度——该 Issue 仅 4 天就催生了两个修复 PR（#6595、#6658），体现了项目对社区反馈的重视。
  - 已有用户尝试使用 QwenPaw 进行 50+ 轮多智能体对话，说明该功能有真实使用场景和深度用户。

- **主要痛点/不满**：
  - **多智能体协作引导缺失**（#6621）：有用户完成 50+ 轮对话后才发现需在 `PROFILE.md` 中显式写入调用指令才能激活其他 Agent，且官方文档未明确说明，导致大量无效调试。**这是典型"功能存在但不可发现"的体验问题。**
  - **静默失败**（#6614 微信推送）：任务显示 `success` 但实际未送达，用户 8 天未收到推送且损失大量 token，这类"假成功"对信任打击极大。
  - **环境兼容性焦虑**（#6612、#6619）：`qwenpaw` 与 `agentscope` 版本不同步导致的崩溃，让用户对依赖链稳定性产生顾虑。
  - **shell 命令执行可靠性**（#6608、#6589）：超时绕过、UI 冻结、孤儿进程，影响自动化场景的可控性。
  - **目录组织混乱**（#6643、#6642）：media 目录堆积大量文件，拖入文件需要先上传复制再读取，用户认为这与其他桌面 Agent 工具相比体验倒退。


## 8. 待处理积压

**长期未响应的 Issue（按创建时间排序）**

- **[#2199 feat(model-fallback) — 自 2026-03-24 开启](https://github.com/agentscope-ai/CoPaw/pull/2199)** — 模型自动降级功能 PR 已存在 4+ 个月，今日出现新 PR #6659 与其功能重叠，建议维护者明确合并策略，避免重复劳动。

- **[#5930 feat: structured run outcome to SSE — 自 2026-07-10 开启](https://github.com/agentscope-ai/CoPaw/pull/5930)** — 为 API 自动化场景补充对话结束的结构化原因（如 loop 检测），Java 服务驱动 QwenPaw 时无法感知对话失败。已近一个月未合并，对 API 使用者影响较大。

- **[#6160 独立 Python 运行环境 — 自 2026-07-16 开启，今日已关闭](https://github.com/agentscope-ai/CoPaw/issues/6160)** — 已由 PR #6579 解决（使用内置 Python），但描述中桌面版调用系统全局 Python 的默认行为值得在发布说明中强调。

- **[#6302 unify provider discovery/model metadata/routing — 自 2026-07-21 开启](https://github.com/agentscope-ai/CoPaw/pull/6302)** — 大型重构 PR，统一 Provider 发现、模型元数据与路由，需关注 review 进度以避免长期分叉。

**⚠️ 需要维护者决策**：
- Issue #6588（`spawn_subagent` 空 batch 误判）已有 **两个** PR（#6595、#6658）提供不同修法，建议尽快合入其一并关闭另一个，避免社区贡献者困惑。


## 项目健康度总评

| 维度 | 状态 | 说明 |
|------|------|------|
| **活跃度** | 🟢 极高 | 22 Issues / 50 PRs / 1 Release 单日更新量 |
| **响应速度** | 🟢 良好 | 多个 Issue 在 1-3 天内即有对应 fix PR |
| **版本节奏** | 🟢 正常 | Beta 发布推进中，CI 修复同步跟进 |
| **兼容性风险** | 🟠 偏高风险 | `agentscope 2.0.4.post1` 引入多处崩溃（#6612、#6619），需在 2.1.0 正式版前完成适配 |
| **社区信任** | 🟡 需加强 | 静默失败（微信推送）、UI 黑屏、环境兼容问题侵蚀用户信心 |
| **积压趋势** | 🟡 可控 | #2199 与 #6659 功能重叠需决策，#5930 合并周期偏长 |

**下一工作日关注重点**：
1. `agentscope 2.0.4.post1` 兼容性修复是否有新 PR 出现；
2. #6608（shell 超时绕过）是否被分配修复；
3. #6659 与 #2199 的合并决策，避免社区重复贡献；
4. v2.1.0-beta.1 的安装验证 Issue #6656 是否全部通过。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-04

## 1. 今日速览

ZeroClaw 项目过去 24 小时保持高度活跃：50 条 Issue 更新和 50 条 PR 更新，表明社区参与度和开发节奏均处于高位。值得关注的是，**高风险 RFC 密集进入维护者评审队列**（#8303 Goal mode、#9488 统一附件架构、#9598 SOP 权限契约），同时 **一批安全相关修复 PR 聚集在 P1 优先级**（#9720 响应缓存边界、#9606 OpenAI 代理、#9574 审批响应授权），显示项目正集中处理安全与架构基础工作。无新版本发布，积压 PR 待合并数达 47 条，维护者合并带宽可能成为瓶颈。总体来看，项目处于**架构收敛与安全加固并行**的阶段，社区讨论热度高，但需警惕待合并 PR 积压带来的交付延迟风险。


## 2. 版本发布

过去 24 小时无新版本发布。


## 3. 项目进展

过去 24 小时仅有 3 个 PR 被合并/关闭（共 50 条 PR 更新），项目推进速度受限于维护者评审带宽。以下为今日值得关注的进展：

**已关闭/合并：**
- **#6641** [已关闭] 回合级 OTel 追踪关联 —— 将 `llm.call` / `tool.call` / `memory.*` 跨度嵌套到单一回合追踪下。该功能从 5 月 13 日创建至今历时近 3 个月，属于 Observability 体系的重要基础设施完善，关闭表明实现已落地。

**推进中的关键 PR（等待合并）：**
- **#9720** [P1] 强制响应缓存请求边界 —— 在观察者或模型提供商看到最终请求之前，对临时请求应用 `before_llm_call` 钩子，并将本地全响应缓存限制为确定性请求。**安全相关，高优先级。**
- **#9574** [P1] 授权审批响应者 —— 将待处理的 Telegram、Slack、Lark 和 Matrix 工具审批绑定到发起提示的聊天或房间，确保审批回复来自授权身份。**安全关键修复。**
- **#9606** [P1] 为 OpenAI Responses API 启用运行时代理 —— 修复代理配置在 Responses API 路径下未生效的问题。
- **#9069** [XL] 仪表盘按代理显示后端和内存计数 —— 经过 rebase 后语义改进：失败的句柄报告 `unavailable` 状态（而非误导性的 `0`），未知 `?agent=` 别名返回 404。

**关键观察：** 今日关闭的 Issue 仅 7 条，大量 PR 处于 `needs-author-action` 状态（约 14/50），作者响应滞后可能成为交付瓶颈。


## 4. 社区热点

### 最热 Issue：RFC: Goal mode v1 — bounded foreground Matrix work（#8303）
- **评论数：** 11 | 👍 1 | 状态：OPEN | 创建：2026-06-24（已持续 41 天）
- **核心诉求：** 用户需要一种持久化机制，使 ZeroClaw 能够跨多个代理回合追求有界用户目标。该 RFC 提出了第一个实现边界，但包含了重启交接、广泛通道准入、模型发起控制等复杂问题。
- **链接：** https://github.com/zeroclaw-labs/zeroclaw/issues/8303

### 次热 Issue：维护者决策队列追踪器（#8692）
- **评论数：** 8 | 状态：OPEN | 创建：2026-07-04（已持续 31 天）
- **核心诉求：** 作为 RFC、设计问题、发布策略问题和协调追踪器的活动决策队列，需要维护者或代码所有者关注。该追踪器的高评论量表明**社区对 RFC 决策效率的不满** —— 多份 RFC 长期停留在 `needs-maintainer-review` 状态（如 #8303、#9488、#7232、#6998、#9598、#9621）而未被推进。
- **链接：** https://github.com/zeroclaw-labs/zeroclaw/issues/8692

### 高交互 Issue：Turn-level OTel trace correlation（#6641，今日关闭）
- **评论数：** 8 | 状态：CLOSED | 创建：2026-05-13 | 更新：2026-08-03
- **分析：** 该 Issue 的评论包含对贡献者 @alexandme 的致谢，社区协作氛围良好。关闭表明这一长期需求已落地。
- **链接：** https://github.com/zeroclaw-labs/zeroclaw/issues/6641

---

### 热门 PR：fix(runtime): enforce response cache request boundaries（#9720）
- **评论数：** 未统计 | P1 | 创建：2026-08-04（今日新开）
- **核心内容：** 与 #9721（Unix 信号清理）和 #9722（保留硬件超时错误上下文）同一天提交，三者均来自 Audacity88，风格一致，建议维护者批量评审。
- **链接：** https://github.com/zeroclaw-labs/zeroclaw/pull/9720


## 5. Bug 与稳定性

### 严重级（P1 / S1-S2）：

| ID | 标题 | 严重度 | 状态 | Fix PR |
|---|---|---|---|---|
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS 桌面应用可重新打开空白或无窗口 | S1 - 工作流阻塞 | OPEN，`r:needs-repro`，`needs-author-action` | 无 |
| [#9642](https://github.com/zeroclaw-labs/zeroclaw/issues/9642) | 超时的审批被记录为明确的运营商拒绝 | **P1，伪造审计轨迹** | CLOSED（in-progress, follow-up） | 无公开 PR |
| [#9718](https://github.com/zeroclaw-labs/zeroclaw/issues/9718) | Telegram 通道在模型同时发出 tool_call 和 content 时传递重复消息 | S2 - 降级行为 | OPEN（今日创建） | 无 |
| [#6157](https://github.com/zeroclaw-labs/zeroclaw/issues/6157) | Nextcloud Talk 使用错误的机器人消息 API | S3，但 **risk:high** | OPEN，`blocked` | 无 |

### 安全相关高亮：

- **#9642（已关闭）** —— 审批超时被记录为显式拒绝，**伪造审计轨迹**。严重性极高，关闭状态为 `in-progress` 与 `follow-up`，需确认是否已有修复方案。
- **#9720（P1，今日新 PR）** —— 响应缓存请求边界，防止缓存污染跨请求数据。
- **#9574（P1，等待合并）** —— 审批响应者授权，防止未授权身份批准工具调用。
- **#1（CRITICAL，已关闭）** —— XOR 密码无法为存储的密钥提供真正加密。该 Issue 自 2 月 14 日创建，今日仍在更新（`needs-author-action`），**核心安全问题悬而未决超过 5 个月**，需重点跟进。
- **#9472（等待评审）** —— 停止将 `vi_verify` 注册为模型可调用工具，防止未签名凭据绕过安全边界。

### 稳定性观察：
- **#9642 的审计伪造问题**属于安全关键 Bug，虽然已关闭，但缺乏对应的修复 PR 可见，建议维护者补充说明。
- **#7527 macOS 空白窗口**长期处于 `needs-repro` 状态，用户已等待近 2 个月，建议维护者主动联系复现。

---

## 6. 功能请求与路线图信号

### 高风险 RFC（多份集中在 `needs-maintainer-review`）：

| ID | 标题 | 领域 | 状态 | 信号强度 |
|---|---|---|---|---|
| [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | Goal mode v1 — bounded foreground Matrix work | Agent 持久目标执行 | OPEN，**已 41 天**，11 评论 | 高 |
| [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488) | 统一 Web 聊天和通道的附件架构 | 通道/网关/安全 | OPEN，8 评论 | 高 |
| [#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598) | SOP 能力权限契约 | 安全/架构 | OPEN（目标 v0.9.0） | 高 |
| [#9621](https://github.com/zeroclaw-labs/zeroclaw/issues/9621) | 分阶段选择加入产品遥测 | 可观测性/隐私 | OPEN | 中 |
| [#6998](https://github.com/zeroclaw-labs/zeroclaw/issues/6998) | Schema 验证的内存整合，带有限回退 | 记忆/提供商 | OPEN | 中 |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | 工作区相对禁止路径模式和可选 `.zeroclawignore` | 安全/配置 | OPEN，`needs-author-action` | 中 |
| [#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232) | 结构化可观测性增强 | 可观测性 | OPEN，`needs-maintainer-review` | 中 |

### v0.9.0 追踪器信号：
- **#7432** v0.9.0 认证、安全、网关和破坏性变更队列 —— 该里程碑包含多个 P1 安全修复（#9574、#9606、#9720）和上述 RFC，**v0.9.0 预计将是安全强化版本**。

### 其他功能请求：
- **#7759** [P1] 将网关 WebSocket 生命周期与代理回合生命周期解耦 —— 支持断线重连后继续后台回合，已接受。
- **#9005** 将活动交互工具上下文注入代理提示 —— 已接受。
- **#8134** 在 `channels.session_ttl_hours` 后重置过期通道会话 —— 已接受（risk:high）。
- **#8132** 用 Rust→Wasm 框架替换 React/Vite Web UI 构建 —— P3 RFC，社区有 👍 1，长期立项中。

### 判断：
- **短期纳入（v0.9.0）：** 安全相关的 #9598（SOP 权限契约）和 #9621（产品遥测）有可能随 v0.9.0 发布。
- **中期候选：** #8303（Goal mode）和 #9488（统一附件架构）是最大的架构变更，需要更多维护者投入才能落地。
- **可能被搁置：** #8132（React→Wasm 替换）和 #8367（能力感知文档）为 P3 低优先级，短期内难以进入开发队列。

---

## 7. 用户反馈摘要

### 真实用户痛点：

**1. 安全审计可靠性（来自 #9642 评论）**
> "一个超时的审批被记录为明确的运营商拒绝……**这伪造了审计轨迹**。列表中的其他一切都降低印象，但这改变了日志记录人类行为的真实性。"

→ 用户关注审计日志的不可否认性，超时应与主动拒绝区分。

**2. 渠道重复消息（来自 #9718）**
> "当 LLM 返回同时包含 tool_calls 数组和填充的 content 字段的响应时，Telegram 通道会传递两者——导致向用户发送重复消息。"

→ 简单的边界条件缺陷，期望通道层做防御性去重。

**3. Telegram 工作流阻塞（来自 #6002，已关闭）**
> "我向 Telegram 发送 'Hi'，zeroClaw 捕获消息并发送给 llama.cpp，llama.cpp 处理……但未明确寻址到助手。"

→ 通道发起的对话可能缺少正确的助手寻址上下文。

**4. macOS 桌面应用问题（来自 #7527）**
> "安装后 zeroclaw 应用无法检测授予的权限，然后失去响应，显示空白页面。退出并重启应用后，窗口甚至消失了。"

→ P1 工作流阻塞，但复现困难。

**5. 工作区内敏感文件保护（来自 #8424）**
> "工作区内部文件如 `rust-toolchain.toml`、`.cargo/config.toml`、`.env` 和 `config.yaml` 不受 `forbidden_paths` 机制保护。"

→ 安全边界覆盖不足，需扩展路径过滤能力。

**6. Nextcloud Talk 集成不可用（来自 #6157）**
> "Nextcloud Talk 响应消息失败，因为使用了错误的机器人消息 API。"

→ 集成质量问题（`blocked` 状态已持续多日，无进展）。

### 社区协作观察：

- **#6641** 中对 @alexandme 的公开致谢表明贡献者协作良好，正向反馈有助于社区活跃度。
- 多位贡献者（Audacity88、IftekharUddin、JordanTheJet、Project516）持续产出，是项目核心力量。


## 8. 待处理积压

### 长期未响应的关键 Issue：

| ID | 标题 | 创建时间 | 等待时长 | 阻塞原因 |
|---|---|---|---|---|
| [#1](https://github.com/zeroclaw-labs/zeroclaw/issues/1) | XOR 密码提供不了真实的密钥加密 | 2026-02-14 | **171 天** | 严重程度 CRITICAL（CWE-327），高危安全债务，`needs-author-action` |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS 桌面应用可打开空白或无窗口 | 2026-06-12 | **53 天** | S1 工作流阻塞，等待复现信息 |
| [#6157](https://github.com/zeroclaw-labs/zeroclaw/issues/6157) | Nextcloud Talk 使用错误的机器人消息 API | 2026-04-27 | **99 天** | 集成不可用，标记 `blocked` 但无进展 |
| [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | RFC: Goal mode v1 | 2026-06-24 | **41 天** | 等待维护者评审 |
| [#7108](https://github.com/zeroclaw-labs/zeroclaw/issues/7108) | 改进缓存 Rust 构建和 CI 关键路径 | 2026-06-02 | **63 天** | 已接受但无对应 PR |

### 等待作者响应的 PR（`needs-author-action`，可能拖延）：

| ID | 标题 | 等待时长 | 风险 |
|---|---|---|---|
| [#8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713) | file_download SSRF 门禁（允许私有主机选择加入） | 31 天 | **risk:high**，安全关键 |
| [#9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) | 授权审批响应者 | 4 天 | **P1**，risk:high |
| [#9606](https://github.com/zeroclaw-labs/zeroclaw/pull/9606) | OpenAI Responses API 代理支持 | 3 天 | **P1**，risk:high |
| [#9069](https://github.com/zeroclaw-labs/zeroclaw/pull/9069) | 仪表板每代理后端 + 内存计数 | 21 天 | size: XL |
| [#9472](https://github.com/zeroclaw-labs/zeroclaw/pull/9472) | vi_verify 注销为模型可调用工具 | 8 天 | 安全相关 |

### 维护者建议：

1. **优先处理 #1（XOR 加密）** —— 已悬置 5 个多月且为 CRITICAL 级别。该项目是 AI 代理框架，密钥存储安全直接关系到用户数据安全，建议维护者主动接入推进。
2. **批量评审 Audacity88 的多个 PR（#9720、#9721、#9722、#9623、#9484 等）** —— 该贡献者产出质量稳定，且多为安全修复，可显著降低 P1 隐患。
3. **回应 #8692 追踪器诉求** —— 社区通过该追踪器表达了 RFC 决策效率的关切。建议每周设置固定时间批量推进 RFC 评审。
4. **关注 #7108（CI 优化）** —— PR CI 需 15-20 分钟，严重影响迭代速度，可作为提升交付效率的切入点。

---

*本日报基于 ZeroClaw GitHub 仓库（zeroclaw-labs/zeroclaw）2026-08-04 公开数据生成，数据截至 2026-08-04 当日更新。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*