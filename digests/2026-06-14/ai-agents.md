# OpenClaw 生态日报 2026-06-14

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-14 02:13 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的OpenClaw项目GitHub数据，我已为您生成以下项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-14

## 📊 今日速览

今日OpenClaw项目社区活跃度极高，过去24小时内共有500条Issue和500条PR的更新，呈现出“高产但动荡”的状态。一方面，两个新的Beta版本（v2026.6.8-beta.1和v2026.6.7-beta.1）发布，主要集中在Telegram和WhatsApp等消息渠道的可靠性与富文本支持上，体现了项目对交付稳定性的重视。另一方面，新报告的Bug数量激增，其中**P0级内存泄漏**、**会话状态丢失**和**安全注入**等严重问题尤为突出，表明随着功能的快速迭代，系统稳定性正面临严峻考验。社区对于多Agent编排、跨会话记忆持久化以及细粒度成本控制的需求呼声很高。

## 🚀 版本发布

- **[v2026.6.8-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.1)**
  - **发布日期**: 2026-06-14
  - **核心亮点**:
    - **Telegram频道增强**: 支持发送富文本（表格、列表、可展开引用块），优化了通过CLI后端发送的可靠性，并引入了更安全的富媒体边界处理。
    - **WhatsApp频道增强**: 频道交付更加稳定。
  - **关键标签**: `channel: telegram`, `channel: whatsapp`, `稳定性`, `富文本`
  - **注意**: 这是一个Beta版本，建议用户在不影响生产环境的测试实例上先行验证。

- **[v2026.6.7-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.7-beta.1)**
  - **发布日期**: 2026-06-13
  - **核心亮点**:
    - **多渠道交付收紧**: 优化了Slack、Telegram的消息投递，包括同频道最终结果持久化、`image`工具对附件的支持、可展开引用块等。
    - **性能与可靠性**: 改进了静默回复、进度草稿和分页操作结果的处理。
  - **关键标签**: `channel: slack`, `channel: telegram`, `性能`, `可靠性`

## 🛠️ 项目进展

今日合并/关闭了192个PR，主要进展集中在以下方面：

- **消息渠道修复**:
  - **Telegram**: PR [#92801](https://github.com/openclaw/openclaw/pull/92801) 修复了HTML标签格式问题，提升了Telegram Web客户端的兼容性。
  - **WhatsApp**: PR [#92095](https://github.com/openclaw/openclaw/pull/92095) 修复了Docker重建/升级后需要重新链接WhatsApp的P1级回归问题，确保登录状态持久化。
  - **QQBot**: PR [#92823](https://github.com/openclaw/openclaw/pull/92823) 修复了媒体发送失败后被误报为成功的问题。
  - **飞书**: PR [#92814](https://github.com/openclaw/openclaw/pull/92814) 修复了动态Agent绑定后路由未能及时更新的问题。
  - **Mattermost**: PR [#80599](https://github.com/openclaw/openclaw/pull/80599) 修复了DM回复上下文丢失的问题（长期PR，今日有重要更新）。

- **核心稳定性与性能**:
  - **子Agent/ACP**: PR [#92804](https://github.com/openclaw/openclaw/pull/92804) 修复了`final_only`模式下，跨工具调用界限的文本累积问题。
  - **Gateway**: PR [#90490](https://github.com/openclaw/openclaw/pull/90490) 增加了Gateway重启后的会话恢复重试机制，提升了系统鲁棒性。
  - **内存与索引**: PR [#92833](https://github.com/openclaw/openclaw/pull/92833) 优化了`corpus=all`时的内存和Wiki搜索性能，将其改为并发执行，避免超时。
  - **浏览器工具**: PR [#92834](https://github.com/openclaw/openclaw/pull/92834) 和 [#88059](https://github.com/openclaw/openclaw/pull/88059) 合并了浏览器截图的全页和元素捕获的 `--labels` 功能增强。

## 🔥 社区热点

今日讨论最热烈的Issue主要集中在核心功能的严重Bug上，反映出用户对系统稳定性的迫切需求。

1.  **[[Bug]: Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925)**
    - **热度**: 19条评论，1个👍，被评为“钻石龙虾 (diamond lobster)”。
    - **诉求**: 用户报告子Agent任务在多种失败模式下（如完成通知失败、Agent自我删除）静默丢失，无重试、无通知、无自动重启。这是对任务执行可靠性的根本质疑。
    - **分析**: 虽然Issue已存在数月，但今日仍有活跃讨论。这表明该问题在复杂的多Agent工作流中持续存在，且修复优先级很高。

2.  **[[Bug]: Feishu monitor state cleanup incomplete](https://github.com/openclaw/openclaw/issues/48183)**
    - **热度**: 18条评论，被评为“钻石龙虾 (diamond lobster)”。
    - **诉求**: 用户详细报告了飞书插件中的一个潜在内存泄漏问题，原因是Monitor状态清理时，Map条目在HTTP服务器完全关闭前就被删除了。
    - **分析**: 用户提供了清晰的复现步骤和根因分析，此类高质量反馈是项目进步的宝贵财富。

3.  **[[Bug]: OpenClaw returns "run Error : LLM Request Failed" on RISC-V64 System](https://github.com/openclaw/openclaw/issues/54253)**
    - **热度**: 14条评论，4个👍，被评为“银贝壳 (silver shellfish)”。
    - **诉求**: 用户尝试在RISC-V架构上运行OpenClaw，但在安装后调用LLM时失败。这反映了社区对新兴硬件平台支持的兴趣。
    - **分析**: 虽然这是一个相对小众的架构，但获得4个赞表明OpenClaw用户群体技术背景深厚，且对多平台支持有期待。

## 🐛 Bug 与稳定性

| 严重程度 | Issue 标题 | 是否有 Fix PR | 摘要 |
| :--- | :--- | :--- | :--- |
| **P0** | [Critical: Gateway Memory Leak](https://github.com/openclaw/openclaw/issues/91588) | 否 | Gateway进程内存泄漏严重，RSS从350MB飙升至15.5GB，导致OOM被杀死。这是当前最严重的问题。 |
| **P1** | [Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925) | 否 | 子Agent任务静默丢失，无任何恢复机制。 |
| **P1** | [gh-issues skill: untrusted issue body injected](https://github.com/openclaw/openclaw/issues/45740) | 否 | `gh-issues`技能存在安全注入风险，恶意的Issue内容可直接注入到子Agent提示中。 |
| **P1** | [message.send schema overexposes](https://github.com/openclaw/openclaw/issues/43015) | 是 (PR #92804 间接相关) | `message.send` 模型过度暴露高级字段，导致GPT模型自动填充错误数据。 |
| **P1** | [Cron scheduled trigger contaminates global runtime](https://github.com/openclaw/openclaw/issues/90991) | **已关闭** | 一个影响全局运行时状态的Cron定时器导致的系统过载问题已被修复。 |
| **P1** | [Session write-lock timeouts block subagent](https://github.com/openclaw/openclaw/issues/86538) | 否 | 会话写锁超时阻塞了子Agent的交付通道，影响并发操作。 |

**总结**：今日的Bug报告呈现 **“双高”** 趋势：**高严重性**（P0/P1）和**高影响力**（`impact:session-state`, `impact:message-loss`, `impact:security`）。特别是内存泄漏和子Agent静默失败问题，是当前项目稳定性的最大威胁。

## 💡 功能请求与路线图信号

1.  **会话生命周期管理的延续性需求**:
    - 用户对`/new`和`/reset`命令丢失上下文感到困扰。Issue [#45608](https://github.com/openclaw/openclaw/issues/45608) 提议在重置前执行“Agentic内存刷新”，Issue [#40418](https://github.com/openclaw/openclaw/issues/40418) 请求自动会话记忆保存与综合。这表明用户希望从“无状态”的会话体验向“有状态”的连续协同演进。
    - **PR信号**: 无直接对应PR，但PR [#91824](https://github.com/openclaw/openclaw/pull/91824) 增加了`sessions_spawn`工具的使用指南，旨在让模型更频繁地使用子Agent，这与会话管理优化方向一致。

2.  **成本控制与透明度**:
    - Issue [#42475](https://github.com/openclaw/openclaw/issues/42475) 请求在Gateway层面增加**每个Agent的成本预算**功能，以防无限制的花费。
    - Issue [#46252](https://github.com/openclaw/openclaw/issues/46252) 报告成本仪表板**忽略归档文件**，导致每日消费统计严重偏低。
    - **分析**: 随着OpenClaw在生产环境中使用增多，成本和资源管理变得更加重要。这些功能请求是项目从“能用”走向“好用”的必经之路。

3.  **更精细的权限与安全模型**:
    - Issue [#39979](https://github.com/openclaw/openclaw/issues/39979) 提出替换二进制级别的Exec白名单，改为**路径级别的RWX权限映射**（类似Unix DAC），以实现更细粒度的文件系统安全控制。
    - Issue [#7707](https://github.com/openclaw/openclaw/issues/7707) 提议对内存条目进行**来源信任标记**，以防御通过不可信来源（如网页）进行的内存投毒攻击。
    - **分析**: 安全相关功能请求的质量很高，表明用户不仅关注功能实现，更关注Agent行为的安全性边界。

## 👂 用户反馈摘要

- **“子Agent不可靠”**: 用户`IIIyban`详细描述了子Agent任务被静默丢弃的多种场景，情绪上表现出对系统可靠性的不信任。这已成为影响高级用户构建复杂自动化流程的核心障碍。
- **“配置管理混乱”**: 用户`AntiMoron`报告“内存管理一片混乱”，提及不同使用者实例表现不一致，暗示了配置扩散、无法同步的问题，这会严重阻碍团队协作场景的推广。
- **“成本黑洞”**: 用户`PabloDaVa`指出`/new`后的费用没有计入成本仪表盘，这可能导致用户低估实际花销。这种“隐藏成本”容易引发财务纠纷和用户信任危机。
- **“Windows更新困难”**: 用户`rainar-sun`报告`openclaw update`命令在Windows上因`EBUSY`错误而失败。这是对多平台用户体验的考验，尤其是对于非Linux用户，更新流程的顺畅至关重要。
- **“浏览器工具不够完善”**: 用户`ibadukefan`基于详实的自动化测试，提出了7项浏览器工具改进建议，包括CSS选择器支持和权限不足时的错误提示。这表明高级用户正在将OpenClaw应用于真实世界的自动化场景，并对其提出了更高的要求。

## 📋 待处理积压

以下为长时间未得到有效响应或解决的重要Issue和PR，提醒维护团队关注：

1.  **长期存在的P1级Bug**:
    - [#44925](https://github.com/openclaw/openclaw/issues/44925) (子Agent静默丢失) - 创建于2026-03-13，影响核心稳定性，至今无Fix PR
    - [#45740](https://github.com/openclaw/openclaw/issues/45740) (gh-issues安全注入) - 创建于2026-03-14，存在严重安全风险，无Fix PR
    - [#48003](https://github.com/openclaw/openclaw/issues/48003) (Steer模式失效) - 创建于2026-03-16，导致关键功能不可用，无Fix PR

2.  **停滞的关键PR**:
    - [#46794](https://github.com/openclaw/openclaw/pull/46794) (设备配对绑定安全) - 创建于2026-03-15，`status: ⏳ waiting on author`，已等待作者响应3个月。该PR涉及安全边界，需尽快推进或标记为挂起。
    - [#86655](https://github.com/openclaw/openclaw/pull/86655) (Claude Bridge扩展) - 创建于2026-05-25，`status: ⏳ waiting on author`。这是一项重大功能扩展，长期等待可能打击贡献者的积极性。

**总结**: 积压问题中，**安全漏洞**和**核心工作流（子Agent）的不可靠性**是最大的技术债务。同时，部分大型PR因作者失联而陷入停滞，建议维护者对这类PR进行内部评估，决定是接手完成还是正式关闭。

---

## 横向生态对比

好的，作为资深技术分析师，以下是根据您提供的2026-06-14各项目动态摘要生成的横向对比分析报告。

---

### AI智能体与个人AI助手开源生态横向对比报告 (2026-06-14)

#### 1. 生态全景

当前，AI智能体与个人AI助手开源生态呈现 **“核心动荡、外围繁荣、精细化与平台化并进”** 的态势。以OpenClaw及其衍生项目（PicoClaw, NanoClaw等）为核心的“Claw生态”占据了绝对主流，但OpenClaw自身的稳定性问题（P0内存泄漏、子Agent静默失败）正成为整个生态的“阿喀琉斯之踵”。与此同时，NanoBot、Hermes Agent等非Claw系项目在特定场景（如WebUI、桌面体验、平台集成）上快速迭代，试图差异化突围。社区共同的关注点从“功能有无”转向“对话可靠性、记忆持久性和成本可控性”，标志着整个行业正从实验性部署迈向生产级应用的关键转折点。

#### 2. 各项目活跃度对比

| 项目名称 | Issues (24h) | PRs (24h) | 版本发布 | 健康度评估 | 核心状态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (更新) | 500 (更新) | 2个Beta | **高风险** | 高速迭代与严重稳定性危机并存 |
| **NanoBot** | 5 (2新) | 19 (5合并) | 无 | **良好** | 高强度修复与功能并行推进，响应迅速 |
| **Hermes Agent** | 50 (43新) | 50 (2合并) | 无 | **亚健康** | 社区需求高涨，但维护吞吐不足，积压严重 |
| **PicoClaw** | 1 (新) | 5 (合并) | 1个Nightly | **健康** | 稳定迭代，积极吸纳社区贡献，优化体验 |
| **NanoClaw** | 1 (无效) | 15 (14合并) | 无 | **健康** | 核心团队强驱动，技术迭代密集，但社区反馈稀缺 |
| **NullClaw** | 1 (更新) | 1 (新) | 无 | **中等** | 聚焦关键Bug修复，等待维护者决策 |
| **IronClaw** | 少量 | 22 (5合并) | 无 | **活跃** | 核心团队冲刺Slack稳定性与附件功能 |
| **LobsterAI** | 4 (新) | 5 (新) | 无 | **停滞** | 所有活动标记为“stale”，核心维护可能放缓 |
| **Moltis** | 1 (新) | 1 (新) | 无 | **专注** | 聚焦单一严重Bug的修复，社区响应积极 |
| **CoPaw** | 8 (更新) | 8 (更新) | 无 | **活跃** | 版本发布后出现Bug报告与贡献高峰，社区活跃 |
| **ZeroClaw** | ~92 (更新) | ~92 (更新) | 无 | **高风险** | 极高活跃度，架构重构与高优先级Bug修复并行 |
| **TinyClaw, ZeptoClaw** | 0 | 0 | 无 | **静默** | 24小时内无活动 |

#### 3. OpenClaw在生态中的定位

- **核心领导地位：** OpenClaw是整个生态的绝对核心和参照系。其衍生的“Claw”系列项目（PicoClaw, NanoClaw, ZeroClaw等）占据了报告项目的一半以上，且技术路线高度一致，形成了一个庞大的“Claw生态体系”。
- **优势：** 拥有最庞大的社区和最多的功能迭代（今日发布2个Beta版本），尤其在**多渠道（Telegram, WhatsApp等）消息投递**和**子Agent（ACP）编排**方面积累了深厚的经验。
- **致命短板：** 今日爆发的**P0级内存泄漏**和长期存在的**子Agent任务静默丢失**，是其最大的技术债务和社区信任危机。其“高产但动荡”的状态，给整个Claw生态带来了不稳定性风险。
- **技术路线差异：** OpenClaw强调**CLI后端+多渠道分发**的“管道”模式；而NanoBot、Hermes Agent更侧重于**WebUI/TUI桌面体验**和**模型提供商管理**；Moltis则专注于**MCP协议集成**。

#### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 / 信号 |
| :--- | :--- | :--- |
| **会话/记忆管理** | OpenClaw, Hermes Agent, CoPaw, NanoClaw, ZeroClaw | 会话状态持久化、跨会话记忆整合（“Dream Mode”）、上下文压缩优化、记忆污染防御。 |
| **成本控制与透明度** | OpenClaw, NanoBot | 细粒度成本预算、消费仪表盘准确性、Token消耗可视化。 |
| **桌面/Web UI体验** | OpenClaw, NanoBot, Hermes Agent, ZeroClaw, LobsterAI | Rich Chat Surface、自动滚动、原生通知、配置面板完善、反向代理支持。 |
| **平台/渠道集成** | OpenClaw, Hermes Agent, ZeroClaw, NullClaw, Moltis | 新消息平台接入（Zalo, Discord）、富消息支持、MCP OAuth兼容性（Notion, Linear）、JIRA集成。 |
| **Agent执行可靠性** | OpenClaw, NanoClaw, NullClaw, IronClaw, CoPaw | 子Agent静默失败、Cron任务可靠性、中断恢复、死锁与崩溃循环修复。 |
| **安全与权限模型** | OpenClaw, Hermes Agent | 路径级别权限映射、内存来源信任标记、安全注入防御、TLS证书支持。 |

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型Agent管道，多渠道、多模型、子Agent编排 | 追求灵活性和功能全面的开发者 | CLI/Hub为中心，插件化(Claw Studio) |
| **NanoBot** | 桌面端+CLI双界面，强大的WebUI和管理视图 | 注重GUI体验和易用性的开发者/团队 | 前后端分离，WebUI功能强大，MCP配置直观 |
| **Hermes Agent** | 桌面端/终端用户体验，集成第三方平台（如Copilot） | 高级个人用户，追求从终端到桌面的一体化 | 核心是CLI/TUI，桌面端为社区贡献 |
| **PicoClaw/NanoClaw** | OpenClaw的轻量版、优化版或特定增强版 | 寻求更稳定/特定功能（如备份）的Claw用户 | 精简核心或加强特定模块（如备份、Agent Runner） |
| **IronClaw** | 企业级Slack集成，实时协作工作流 | 重度依赖Slack的团队和企业 | 围绕Slack进行深度优化，强调消息投递的可靠性 |
| **NullClaw** | “无状态”/“极简”的Agent框架 | 对状态管理有特殊要求的开发者 | 技术架构强调简洁和单一职责 |
| **LobsterAI/CoPaw** | 专注于Cowork（协作）和技能（Skills）管理 | 注重团队协作和技能生态的用户 | 以“技能”和“协作会话”为核心抽象 |
| **ZeroClaw** | 下一代全能型Agent，WASM和本地推理支持 | 前沿技术探索者，对本地化、插件化有极致追求 | 强调WASM插件、OCI容器化、Rust实现 |

#### 6. 社区热度与成熟度

- **快速迭代 & 高活跃 (高风险):** **OpenClaw, ZeroClaw**。Issue和PR数量激增，社区极度活跃，但伴随大量高优先级Bug，项目处于“边飞边修”状态。
- **快速迭代 & 健康: NanoBot, PicoClaw, NanoClaw**。有明确的迭代节奏，维护者响应迅速，社区贡献有序，Bug修复及时。
- **活跃但吞吐不足: Hermes Agent, CoPaw**。社区需求旺盛，讨论热烈，但合并/关闭PR速度跟不上问题报告速度，易积累技术债务。
- **质量巩固阶段: IronClaw, NullClaw**。正在集中精力解决特定的严重Bug或打磨核心功能（如附件、Slack集成），而非疯狂扩张新功能。
- **停滞或静默: LobsterAI, TinyClaw, ZeptoClaw, Moltis**。项目活动极少，可能处于维护状态或用户群体较小。

#### 7. 值得关注的趋势信号

1.  **“可靠性压倒一切”：** 从OpenClaw的P0内存泄漏到NanoClaw的崩溃循环，再到NullClaw的use-after-free，社区对Agent执行可靠性的关注度已超越功能数量。开发者应**优先投资于服务稳定性 (SLA)、容错机制和可观测性**，而非盲目堆叠新功能。
2.  **“有状态Agent”是未来：** 记忆持久化、上下文压缩、会话恢复等需求（Dream Mode）在所有项目中频繁出现。这表明市场不再满足于“一问一答”的对话机器人，而是需要**拥有长期记忆、能从经验中学习、能无缝恢复工作状态的自主Agent**。
3.  **“成本可见”是生产前提：** 对细粒度成本控制和仪表盘准确性的要求，标志着AI Agent正从个人玩具走向企业级资源。开发者必须将**成本核算作为系统的一个内置模块**，而非事后才考虑的问题。
4.  **“平台化 / Plugin化”成为增值点：** 从Moltis的MCP集成，到ZeroClaw的WASM动态库，再到NullClaw的JIRA连接器，Agent的能力边界正在通过标准化的“连接器”或“插件”扩展。构建一个**健壮的、安全的、易于发现的插件生态**将成为项目的核心竞争力。
5.  **“桌面端战场”日趋激烈：** NanoBot、Hermes Agent和OpenClaw的派生项目（如CoPaw）都在桌面端UI上发力。未来的竞争将不仅仅是后端能力的比拼，更是**端侧用户体验、交互设计和对本地算力利用效率**的较量。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-14

## 1. 今日速览

NanoBot 项目过去24小时进入高密度补丁与功能合并期，社区活跃度显著提升。共处理 **19 条 PR**（待合并 14 条，已合并/关闭 5 条）和 **5 条 Issue**（新开/活跃 2 条，已关闭 3 条）。核心进展集中在 **MCP 服务器稳定性修复**、**WebUI 启动性能优化**、**TUI 交互原形**以及 **Anthropic 模型兼容性更新**两大方向。此外，**TTS 多供应商支持** 和 **自动化管理视图** 两大新功能PR已提交，预示着v0.2.x路线图正在加速落地。无新版本发布，但当日合并/关闭的5条PR均为重要修复类贡献，项目整体健康度良好，维护响应及时。

## 2. 版本发布

**无**

---

## 3. 项目进展

过去24小时内，以下 **5 条 PR 被合并/关闭**，推进了多项关键修复与功能升级：

| PR # | 标题 | 状态 | 影响 |
|------|------|------|------|
| #4098 | [codex] Fix exec workspace symlink guard and path precedence | ✅ 已合并 | 修复了 ExecTool 中相对符号链接逃逸工作区漏洞 (#4072) 以及 `pathAppend` 优先级问题 (#4083)，增强安全性及工具路径查找可靠性 |
| #4326 | fix(memory): summarize full session tail during idle compaction (#4264) | ✅ 已合并 | 修复 `idleCompact` 只总结最后8条消息外的历史导致错误记录的问题，改为基于全未合并会话尾部进行总结 |
| #4327 | Fix WebUI startup blocking on slow gateway routes | ✅ 已合并 | 将慢路径HTTP处理移出事件循环、避免完整 JSONL 读取、仅抓取已安装 CLI 应用而非完整远程目录，显著提升 WebUI 启动响应速度 |
| #4314 | Break tool config schema import cycle | ✅ 已合并 | 重构工具配置导入循环，将共享 Pydantic 基础迁移至独立模块，解决编译时循环依赖问题，利于插件化配置扩展 |
| #4313 | Feat(webui): config.json/webui parity | ✅ 已合并 | 大幅缩小 WebUI 设置面板与 `config.json` 之间的功能差距，新增 temperature、tool limits、dream、channels 等配置写入端点 |

**关键前进**：代码安全与稳定性方面获得直接加固，WebUI体验优化进入细化阶段，TUI、TTS、自动管理等重量级功能正在排队等待审查合并。

---

## 4. 社区热点

### 📍 #193 (已关闭) — Ollama API support?
- **链接**: [#193](https://github.com/HKUDS/nanobot/issues/193)
- **评论**: 15 | **创建**: 2026-02-06 → 2026-06-13 关闭
- **分析**：作为历史最久的开放讨论之一，该Issue在2026年2月提出，经历近4个多月才正式关闭。用户明确询问除vLLM之外是否支持Ollama API。关闭状态暗示可能已在代码中实现或明确决定不优先支持，但从长达15条评论和长期未响应来看，社区对本地轻量推理的需求非常强烈。可能需要维护者在release note或文档中说明决策理由。

### 📍 #4333 (New, 0评论) — Anthropic provider sends deprecated temperature to opus-4-8 / Fable → 400
- **链接**: [#4333](https://github.com/HKUDS/nanobot/issues/4333)
- **评论**: 0 (刚创建)
- **分析**：刚提交但已触发紧急fix PR #4334，说明核心API兼容性问题直接影响所有使用Claude Opus 4-8及以上模型的用户。因无评论，目前尚未有社区讨论，但怀疑很快会吸引受影响用户。

### 📍 #4322 (活跃) — NameError: session_key not defined after merge
- **链接**: [#4322](https://github.com/HKUDS/nanobot/issues/4322)
- **评论**: 1
- **分析**：用户在合并 `main` 到 `fix/prompt-caching` 分支后遇到启动时崩溃。属于分支合并引入的回归性bug，影响开发者和早期采用者试用prompt caching特性。已有确认的根本原因分析，但尚未出修复PR。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue # | 标题 | 状态 | 修复PR? |
|--------|---------|------|------|---------|
| ⛔️ 破环性 | #4333 | Anthropic provider温度参数导致全部请求400 | 新开 | ✅ #4334 (等待审查) |
| ⛔️ 启动崩溃 | #4322 | 合并后 `session_key` 未定义导致启动异常 | 活跃 | ❌ 未提交 |
| 🐛 功能异常 | #4264 | idleCompact只总结最后8条外的历史(已关) | 已关闭 | ✅ #4326已合并 |
| 🐛 安全 | #4083 | pathAppend不遵守可执行查找优先级(已关) | 已关闭 | ✅ #4098已合并 |
| 🐛 运行时崩溃 | #4302 | MCP server `_close_server` 因generator GC崩溃 | 已关闭 | ✅ #4303 (待合并) |

**关键分析**：
- #4333 虽然刚提出，但直接影响所有使用新Claude模型的正常请求，被修复PR #4334立即锁定，预计很快合并。
- #4322 尚未有修复PR，且是分支合并引入，可能需要在合并策略上加严格测试。
- 核心稳定性方向：MCP 连接管理与 Anthropic 模型兼容性成为当日突发风险点。

---

## 6. 功能请求与路线图信号

| 需求 | Issue/PR | 分析 | 纳入候选 |
|------|----------|------|----------|
| **WebUI自动管理视图** | #4330 (PR) | 新增自动化管理界面，支持列表、筛选、运行、暂停/恢复、删除自动操作。这是WebUI功能完整度的重要拼图，优先级高。 | ✅ 高概率纳入v0.2.x |
| **子代理可配置模型预设** | #4291 (PR) | 子代理可使用与父代理不同的LLM预设（provider, model, temperature），通过spawn时指定。对复杂多Agent编排场景非常实用。 | ✅ 有望纳入 |
| **TTS多供应商系统** | #4316 (PR) | OpenAI / Groq / ElevenLabs三供应商TTS配置，通过WebUI API持久化。用户语音助理体验的关键组件。 | ✅ 有望纳入 |
| **内置文件系统工具可配开关** | #4138 (PR) | 允许管理员关闭所有内置文件系统工具，只让模型通过MCP Server访问远程沙盒。对安全部署重要。 | ✅ 高概率 |
| **WebUI反向代理子路径支持** | #4328 (PR) | 允许在 `/nanobot/` 这样的子路径下正常运行WebUI。企业化部署刚需。 | ✅ 高概率 |
| **Ollama API支持** | #193 (已关) | 用户强烈期盼本地推理支持，但未明确纳入Roadmap。已有4个月未更新。 | ⚠️ 待评估 |

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的用户真实声音：

- **#4264（已修复）** 用户 `imkuang` 描述了一个典型使用场景：用户不断纠正模型错误，最终模型给出正确结果结束对话，但idleCompact只总结除了最后8条消息之外的历史，导致正确结果未被保存。反映了**对话压缩机制与真实纠错工作流不匹配**的痛点。
- **#4322（活跃）** 用户 `professionelle-hypnose` 反馈合并分支后立即崩溃且无恢复手段，表明分支管理策略可能不够友好，需要更完善的合并后验证流程。
- **#4333（新开）** 用户 `Ulef1005` 遇到所有请求被400拒绝，这类**部署即不可用**的体验会显著降低用户对模型的信任和项目的可靠性评价。
- **#4303（待合并）** 用户 `michaelxer` 遇到 MCP server session 终止并重连时进程崩溃，此类**背景静默崩溃**对长时运行服务尤为致命。

总体反馈指向 **稳定性的实际运行场景** 是用户最关心的，其次是对 **配置灵活性** 和 **本地部署支持** 的长期诉求。

---

## 8. 待处理积压

以下 Issue 或 PR 长期未获响应或进展缓慢，建议维护团队重点关注：

| 项目 | 时长 | 状态 | 风险 | 推荐操作 |
|------|------|------|------|----------|
| [#193] Ollama API support | 已关闭(但用户诉求未明确定位) | 关闭 | 缺乏明确路线图说明，社区可能失望 | 在 README 或官网 FAQ 明确说明支持/不支持的原因与计划 |
| [#4138] 内置文件系统工具开关 | 创建16天 | 待审查 | 与安全加固直接相关 | 应尽快安排 review，已在 #4098 安全工作之上 |
| [#4291] 子代理模型预设 | 创建3天 | 待审查 | 新设计特性，影响后期多Agent编排 | 建议加入 v0.2.0 milestone，并邀请早期反馈 |
| [#4083] pathAppend 优先级问题 (已关) | 已修复 | 已合并 | 无 | 提醒文档更新应包括安全配置指南 |
| 无自动分配里程碑的开放 PR 集群 | 所有14条待合并PR均未附加 milestone | 持续 | 可能导致功能碎片化、合并节奏混乱 | 建议每个 PR 关联一个大小版本目标 |

---

**总结**：NanoBot 在 2026-06-14 呈现出 **高强度的修复与功能并行推进** 状态，社区活跃度处在近期高点。主要风险的 Anthropic 兼容性问题已在出现后数小时内被 PR 锁定，显示出维护团队响应迅速。WebUI 与 CLI 的双跃进（自动化视图、TUI、TTS）表明产品化正在加速。建议团队尽快清理 **#4322 和 #4333** 两个影响运行的 bug，并在未来一周安排对 **#4138、#4291、#4316** 等重量级功能 PR 的 review。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 Hermes Agent GitHub 数据生成的 2026-06-14 项目动态日报。

---

# Hermes Agent 项目日报 | 2026-06-14

## 今日速览

今日项目活动异常活跃，社区参与度极高。`Issues` 和 `PR` 的 24 小时更新量均达到 50 条，反映了开发者和用户的高频互动。尽管有 43 个新 `Issues` 涌入，但关闭率仅为 14%，积压工作正在增加。值得注意的是，`PR` 的合并/关闭率极低（4%），大量改进和新功能仍在等待审核。项目整体处于“高需求、低吞吐”阶段，社区对 **Web/Desktop UI**、**Telegram 富消息** 和 **记忆管理** 等方面表现出强烈的关注和反馈。

## 版本发布

**无**。本日无新版本发布。

## 项目进展

今日合并或关闭的 PR 数量有限，但解决了两个关键问题，并预热了一个重要功能：

1.  **修复 macOS 测试环境问题**
    - **PR #45826 (已关闭)**: 解决了 `macOS` 上因 `/private` 路径解析和配置守卫优先级导致的文件工具测试失败问题。虽然这是一个测试修复，但它确保了核心文件操作功能在 Mac 平台上的可靠性。
    - **链接**: `https://github.com/NousResearch/hermes-agent/pull/45826`

2.  **关键 Bug 修复落地**
    - **PR #29205 (已关闭)**: 修复了当会话从 Codex Responses API 回退到原生 Anthropic 时，因末尾存在助手预填充（assistant prefill）导致 Anthropic 拒绝请求的 P1 级 Bug。这直接提升了多提供商切换的稳定性。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/29205`
    - **PR #27988 (已关闭)**: 修复了 Codex Responses 适配器在 Azure Foundry 上将完整的 `final_answer` 错误映射为 `finish_reason="incomplete"` 的 P1 级 Bug。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/27988`

3.  **社区贡献的桌面增强**
    - **PR #45895 (开放)**: 一位社区贡献者提交了一个“Rich Chat Surface”的 PR，旨在为桌面端提供一个成熟的聊天界面，目标是让 Hermes 成为一个“一体化”客户端。
    - **链接**: `https://github.com/NousResearch/hermes-agent/pull/45895`

## 社区热点

今日社区讨论的核心热点集中在 **桌面端/终端用户体验** 和 **平台新特性的集成** 上。

1.  **#501 [CLOSED]: Web UI 网关功能请求**
    - **评论: 14 | 👍: 1**
    - **核心诉求**: 用户急切需要一个本地运行的浏览器界面，与 CLI 和现有第三方平台并行使用。这是与 Claude Artifacts 等竞品功能对齐的缺失一环。该 Issue 虽已关闭，但其 14 条评论表明社区对此功能有高度共识和讨论。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/501`

2.  **#10771 [OPEN]: 自动记忆整合功能请求**
    - **评论: 8 | 👍: 5**
    - **核心诉求**: 用户希望引入类似 Claude Code “Auto Dream” 的机制，自动清理、去重和优化 Agent 的记忆文件，解决因“昨天”、“上周”等相对日期随时间推移而失效的“记忆污染”问题。该请求获得了最高赞，是社区对长期上下文稳定性的核心关切。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/10771`

3.  **#44428 [OPEN] & #45864 [OPEN] & #45854 [OPEN]: Telegram Bot API 10.1 支持**
    - **总评论: 7 | 👍: 4**
    - **核心诉求**: 这是一个需求集群。Telegram 在 6月11日发布了支持富文本（表格、数学公式、表格等）的 Bot API 10.1，社区立即提出了三个相关 Issues，要求 Hermes 尽快跟进。这显示了用户对利用平台最新功能提升 Agent 表达能力的强烈渴望。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/44428`, `https://github.com/NousResearch/hermes-agent/issues/45864`, `https://github.com/NousResearch/hermes-agent/issues/45854`

## Bug 与稳定性

今日报告了多个影响可用性的 Bug，按严重程度排列如下：

- **[P1] - 严重**
    - 无新增。但今日合并了此前报告的 P1 级回退和适配器错误，表明稳定性修复正在推进。

- **[P2] - 高**
    - **#44666**: 配置中 `providers:` 下的 `api_key_env` 字段被静默忽略，导致自定义提供商认证失败。
    - **#31155**: 配置中的 `delegation.model` 被忽略，子代理始终继承父模型，限制了分层调用的灵活性。
    - **#43586**: 类似问题，`model:` 块中的 `provider: custom` 和 `key_env` 组合导致 API key 被忽略，总是发送错误的 `no-key-required`。
    - **#42405**: 内存容量满后触发 `replace` 操作，因匹配失败进入无限重试循环，导致 Agent 无响应。
    - **#23975**: 在上下文压缩进行时，新的网关消息会中断压缩过程，导致回退标记损坏。已有 **PR #45872** 尝试修复此问题。
    - **#45877**: Cron 任务在后台审查阶段阻断了 `read_file` 和 `search_files` 等只读工具，影响自动任务执行。
    - **#45813**: GitHub Copilot 提供商（非ACP）持续返回 `HTTP 400` 错误。
    - **#45674**: 当 `mcp_servers` 配置为字符串而非字典时，`hermes mcp list` 命令会崩溃。
    - **#45792**: Docker 内的 Hermes 无法正确理解其环境，存在路径或权限问题。

- **[P3] - 一般**
    - **#42366 & #45913**: 桌面端/TUI 聊天界面无法自动滚动，且在输出时输入框会消失。这是一个严重影响用户体验的回归问题。已有 **PR #44927** 被标记为重复项，提议增加一个可选的自动跟随开关。

- **已有修复 PR 的 Bug**:
    - **#23975**: 中断导致回退标记损坏 -> **PR #45872 (开放)**
    - **#45782**: 本地 Ollama 端点 `model.base_url` 被静默忽略 -> **PR #45869 (开放)**

## 功能请求与路线图信号

今日的功能请求与社区关注点高度一致，部分功能已有关联 PR 在推进：

1.  **记忆管理是核心诉求**:
    - **#10771**: 自动记忆整合是当前最受欢迎的功能请求。虽然尚无直接 PR，但这几乎是社区共识的方向，预计会进入下一版本的 backlog。
    - **#19245**: 崩溃后会话搜索失败，孤立的 JSON 文件无法恢复。这指向了更健壮的状态持久化需求。
    - **#33907**: 上下文压缩创建了孤立的会话，且未写入 `state.db`。这与上述问题相关。

2.  **Telegram 富消息全面支持 (已纳入下一版本)**:
    - **#44428, #45864, #45854**: 多个请求集中指向 Telegram Bot API 10.1。这是一个功能追赶项，很可能在短时间内被采纳并开发。

3.  **桌面端 / TUI 体验优化 (已有 PR)**:
    - **#45913**: 自动滚动和会话大纲定位不准是桌面端的紧迫问题。
    - **PR #45895**: “Rich Chat Surface” 是一个雄心勃勃的社区 PR，暗示用户对“开箱即用”的成熟桌面聊天体验有强烈需求。
    - **PR #45866**: 桌面原生通知功能也已提交 PR，表明桌面端的完善工作在并行推进。

4.  **更多集成与功能**:
    - **#45867**: 有 PR 提议增加 **OpenRouter Fusion** 支持。
    - **#45912**: 用户请求为 WhatsApp/Telegram 添加预设键盘输入，以简化“审批”等交互流程。

## 用户反馈摘要

- **核心痛点**: “桌面端/TUI 滚动问题”是今日用户抱怨最集中的地方，被多位用户独立报告（#42366, #45913），并已有相关 Issue 被标记为重复（#44927）。用户想要一个能像常规聊天应用一样流畅滚动的界面。
- **使用场景**: 从 **#44428 (Telegram 富消息)** 和 **#45854 (sendRichMessage 工具)** 可以看出，用户在使用 Hermes 生成并分享包含复杂格式（表格、数学公式）的内容，这对其在线沟通场景至关重要。
- **配置困惑**: **#44666** 和 **#43586** 表明，`custom` 提供商的 API Key 配置方式存在混淆和 Bug，用户期望配置能“见到即所得”。
- **积极反馈**: 社区贡献活跃，如 **#45895** (Rich Chat Surface) 和 **#45866** (原生通知) 表明高级用户正在积极尝试填补项目自身的功能空白。

## 待处理积压

以下 Issue 和建议长期未得到充分响应，需要维护者关注：

1.  **#33907 [OPEN] [P2]**: “上下文压缩创建了孤立的会话”，作为一个 P2 Bug，自5月28日提出后仅有2条评论，尚未有实质性进展。这可能导致用户的数据丢失或状态错乱。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/33907`

2.  **#22417 [OPEN] [P3]**: “Showcase: 紫鸾/CPRC 场域健康引擎的演进记录”。这是一个与 ThinkCheck 推理评估引擎集成的第三方 Showcase，自5月9日提出后仅有2条评论。这可能是一个有价值的集成案例，值得官方进行查看和响应，以鼓励社区生态。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/22417`

3.  **#19245 [OPEN] [P2]**: “崩溃后 session_search 返回空，孤立的 session JSON 无法恢复”。与 #33907 高度相关，同样指向了状态管理的健壮性问题。缺乏关注可能导致类似的用户数据丢失问题被反复报告。
    - **链接**: `https://github.com/NousResearch/hermes-agent/issues/19245`

---
*报告结束时间：2026-06-14 23:59 UTC*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 PicoClaw 项目 2026-06-14 动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-14

## 1. 今日速览
项目今日活跃度较高。过去24小时内，共有1个新的Nightly版本发布，代码库合并/关闭了5个Pull Request (PR)，并处理了1个新Issue。社区贡献主要集中在**Bug修复**（尤其是代码质量提升和边缘情况处理）以及**新功能推进**（如图像压缩、Agent模式拓展）。项目在稳定版本迭代的同时，积极吸纳社区贡献，整体健康度良好。

## 2. 版本发布
- **`nightly` 版本更新 (v0.2.9-nightly.20260614.cf67dd38)**
  - **内容**: 这是一个自动化构建的Nightly版本，包含截至当日的所有最新提交。
  - **破坏性变更**: 无明确声明。Nightly版本可能不稳定，建议仅在测试环境使用。
  - **迁移注意事项**: 从`v0.2.9`版本升级到此版本无需特殊迁移步骤，但请关注潜在的不稳定因素。
  - **更新日志**: [查看完整变更](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展
- **Bug修复与代码质量提升**:
  - **[PR #3065] 已合并**: 修复了`pkg/seahorse`模块中数据库关闭错误被忽略的问题，提升了代码健壮性。
  - **[PR #3066] 已合并**: 修复了多个模块中临时文件关闭错误被忽略的问题，提高了文件操作的安全性和稳定性。
  - **[PR #3117] 已合并**: 修复了`agent`模式下，当模型不支持视觉时，图像处理请求出现幻觉的Bug（关联Issue #3108）。该PR将媒体相关的请求路由到配置的图像模型，从根本上解决了问题。
  - **[PR #3119] 已合并**: 为TTS（文本转语音）功能添加了对OpenRouter模型`voice`和`response_format`参数的支持，并实现了自动重试回退机制，提升了多模型兼容性。

- **功能与特性推进**:
  - **[PR #2964] 代码已更新**: 这是一个重要的新功能PR - “图像输入压缩”。它引入了可配置的多级图像压缩策略。虽然尚未合并，但其作者在今日更新了代码，表明该功能正在积极开发中。
  - **[PR #3118] 待合并**: 新增了`picoclaw agent`的远程WebSocket模式，允许Agent通过WebSocket与PicoClaw实例连接，扩展了Agent的使用场景。

- **国际化贡献**:
  - **[PR #2935] 已合并**: 完成了对繁体中文（zh-TW）的完整文档和前端i18n支持，有助于项目在中文地区的推广。

## 4. 社区热点
- **[Issue #3012] 持续吐槽**: 该Issue关于“开启Evolution功能后每分钟持续消耗Token”的问题，获得了3条评论，是近期讨论的焦点。尽管是旧Issue（6月5日创建），但用户`xpader`在FreeBSD环境下遇到的这个严重资源消耗问题，可能尚未有明确结论，社区持续关注中。
  - **链接**: [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

## 5. Bug 与稳定性
1.  **严重**:
    - **[Issue #3012] Token持续消耗**: 核心功能Bug。用户报告在FreeBSD系统上，启用`Evolution`功能后，即使没有用户交互，系统也会每分钟消耗Token。该问题影响用户体验和成本，目前尚未有Fix PR关联。
      - **链接**: [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

2.  **中等**:
    - **[Issue #3108] 图像描述幻觉 [已关闭]**: 当模型不支持视觉功能时，图像描述请求会输出无关内容。此问题已通过合并**PR #3117**得到修复。
      - **链接**: [Issue #3108](https://github.com/sipeed/picoclaw/issues/3108) | [PR #3117](https://github.com/sipeed/picoclaw/pull/3117)

3.  **轻微/代码质量**:
    - **[PR #3065 & #3066] 未处理Error**: 多个地方忽略了`Close()`方法的错误返回。这些都已通过合并对应的PR修复，解决了潜在的代码警告和资源泄露风险。
      - **链接**: [PR #3065](https://github.com/sipeed/picoclaw/pull/3065) | [PR #3066](https://github.com/sipeed/picoclaw/pull/3066)

## 6. 功能请求与路线图信号
- **图像处理能力提升**: **PR #2964 (图像输入压缩)** 是一个非常明显的信号。社区贡献者`afjcjsbx`正在推动为图像管道增加可配置的压缩策略。这旨在解决图片过大导致模型API调用失败或成本过高的问题。该PR极有可能被纳入下一个稳定版本。
- **Agent远程化**: **PR #3118 (远程WebSocket模式)** 表明，开发者希望将Agent从本地执行扩展到远程控制。这为未来实现更复杂的自动化工作流和分布式部署提供了可能，很可能成为项目下一步发展的重点之一。

## 7. 用户反馈摘要
- **痛点**: 用户`xpader`在 **Issue #3012** 中反映的Token持续消耗问题，是目前最突出的用户痛点。在FreeBSD这一特定平台上，该问题尤为严重，影响了PicoClaw作为后台服务的可用性。用户对“开启即被消耗”的逻辑表示困惑和不满。
- **需求**: 用户`not-the-author`通过 **PR #3119** 解决了TTS语音在多模型下的兼容性问题，这反映了用户对使用不同模型提供商（如OpenRouter）的灵活性的需求。用户希望PicoClaw能更好地适配不同AI平台的特性。

## 8. 待处理积压
- **[Issue #3012] Token持续消耗**: 自6月5日创建至今已超过一周，仅有3条评论，且没有明确的修复计划或PR。考虑到此问题影响严重，建议项目维护者优先调查并给出解决方案或临时工作区，以避免影响FreeBSD等用户群体的体验。
  - **链接**: [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-06-14

## 1. 今日速览

过去24小时，NanoClaw 项目继续保持高位活跃，共处理15条 Pull Request（其中14条已合并/关闭），但社区互动极少（仅1条错误提交的 Issue，0条评论）。核心贡献者 **ddaniels** 主导了大部分合并工作，涉及多项功能修复与增强，特别在 **Signal 集成**、**Agent Runner 稳定性** 和 **备份恢复** 方面有大量落地。项目整体处于 **强迭代 + 低社区反馈** 的健康但略显“内向”的状态——技术推进密集，但用户参与度不足，需警惕长期缺乏外部验证的风险。

## 2. 版本发布

无新版本发布。近24小时无 Release 活动。

## 3. 项目进展

过去24小时合并/关闭了14条 PR，重点集中在以下三个方向：

### 3.1 Signal 集成全面升级（ddaniels）
- **#2203** — 双向 Signal 反应（Reaction）支持，代理可调用 `add_reaction` MCP 工具将 emoji 发送至目标消息。  
- **#2071** — 非音频附件通过收件箱路径路由，Signal 用户可发送 PDF、文档、图片等任意文件类型，代理在 `/workspace/inbox/<msgId>/<name>` 读取。  
- **#2040** — 支持出站附件，`signal-cli` 的 `send` JSON-RPC 现在可附带 `attachments` 参数。  
- **#2070** — `extractAttachmentFiles()` 函数接受主机路径附件，原生通道适配器（Signal等）不再依赖 base64 内联数据。  
- **#2072** — Ollama 多模态模型支持 `images` 字段，代理可以通过工作区相对路径向多模态模型传递图像。

> 三条 PR 共同构成了 Signal 通道附件处理的完整闭环，从入站附件路由到出站附件发送，再到多模态模型消费，Signal 集成已具备生产级能力。

### 3.2 Agent Runner 稳定性与容灾（ddaniels）
- **#2670** — 修复毒化恢复崩溃循环：当会话恢复时发现损坏的 `thinking`/`redacted_thinking` 块导致无限 crash-loop，PR 通过更健壮的检测与自我修复机制解决该问题。  
- **#2277** — 修复轮询循环中路由上下文冻结问题：初始批次提取 `RoutingContext` 后未随 follow-up 消息刷新，导致 cron 任务后聊天消息调度错误。  
- **#2267** — 修复 Agent-to-Agent 回复路由到错误会话：`findSessionByAgentGroup` 总是排序到最新会话，导致多会话场景下回复“分脑”。  
- **#2692** — 轮询循环重试瞬态 5xx API 错误（如 `529 Overloaded`），错误暴露后通知而非静默丢弃。  
- **#2084** — 日备份系统：每日快照所有备份相关状态，支持本地 + 可选 S3 存储后端，提供全量或按代理恢复的 CLI。

> 5条 PR 构成了近期稳定性投入的主线，agent-runner 的可靠性、容灾能力和错误处理得到全面补强。

### 3.3 核心底层架构（omri-maya）
- **#2754** — 新增 `onExchangeComplete` provider 钩子 + 斜杠命令中断机制，允许外部系统在交换完成后执行自定义逻辑。  
- **#2747** — SDK 从 0.5.0 → 2.2.1，同时注入凭据存根挂载和机器可检查 pin。  
- **#2746** — 新增 Agent-Surfaces 能力接口，provider 可以通过声明式注册声明自身能力，填充 `agent.surfaces` 元数据。  
- **#2745** — 可选持久化内存支架，provider 可通过 `usesMemoryScaffold` 获得持久化内存存储。

> 这三条 PR 构建了 provider 可扩展性的新底层框架——能力声明、持久化内存、交换钩子——为未来自定义 provider 的丰富性奠定基础。

**总体评估**：过去24小时，项目在 **Signal 集成（从基础支持到高阶特性）**、**Agent Runner 稳定性（5个关键修复）**、**底层架构扩展性（3个新能力框架）** 三个维度取得了显著进展。特别是备份系统（#2084）的加入，标志着项目运维成熟度提升了一个台阶。

## 4. 社区热点

**过去24小时无实质性社区讨论。** 唯一的 Issue #2755 是用户 eranshir 提交的错误发布（posted in wrong repo）。所有 PR 作者均为核心团队人员（ddaniels、omri-maya），无外部贡献者参与。这说明项目目前仍以核心开发者推动为主，社区参与度有待提升。

## 5. Bug 与稳定性

**过去24小时未报告新的 Bug。** 但以下今日合并的 PR 直接修复了若干严重的运行时稳定性问题：

| Issue/PR | 严重程度 | 问题描述 | 修复状态 |
|----------|----------|----------|----------|
| #2670 | **高** | 毒化会话恢复导致 Agent Runner 无限崩溃循环 | 今日合并 |
| #2692 | **高** | 瞬态5xx API错误被终端化，静默丢失消息 | 今日合并 |
| #2277 | **中** | 轮询循环路由上下文冻结，导致 cron 后聊天消息调度错误 | 今日合并 |
| #2267 | **中** | Agent-to-Agent 回复路由到错误会话（多会话分脑） | 今日合并 |
| #2732 | **中** | 主机+Agent Runner 健康审计发现的多个安全问题（持续运行 crash-loop、MAX_CONCURRENT_CONTAINERS 缺失等） | 待合并 |

> 关键观察：今天合并的多数 PR 都指向 agent-runner 的稳定性问题，且这些问题在 Issue 跟踪系统中已有对应编号（#2669），说明项目正在系统性地消除运行时故障根源。建议关注 **#2732**（OPEN），该 PR 针对的健康审计问题涉及容器生命周期安全，优先级应提升。

## 6. 功能请求与路线图信号

**过去24小时无用户提交的功能请求。** 但从今日合并的 PR 可以推断出项目的未来方向：

1. **Signal 集成进入生产阶段**：所有基础附件处理能力（入站、出站、多模态）已就绪，下一步可能关注 Signal 加密协议深度集成或群组支持。
2. **Provider 框架扩展性提升**：`onExchangeComplete` 钩子 + 能力声明 + 持久化内存，暗示项目计划支持更复杂的多 provider 协作场景（如：A provider 处理图像，B provider 处理文字）。
3. **运维自动化**：备份系统（#2084）标志着项目在向“可运维 生产环境”演进，后续可能跟进监控告警、自动升级等运维能力。

## 7. 用户反馈摘要

**过去24小时无实际用户反馈。** 唯一的 Issue #2755 为错误提交。建议项目团队关注如何鼓励用户通过 Issue 或讨论区反馈真实使用体验——0 条实质性用户反馈意味着项目在缺少外部验证的情况下快速迭代，存在“实现可能偏离用户真实需求”的风险。

## 8. 待处理积压

**过去24小时无新增长期未响应 Issue/PR。** 但以下待合并的 PR 值得关注：

- **#2732** [OPEN] — Harden host + agent-runner from health audit findings（创建于2026-06-11，已待处理3天）；该 PR 涉及容器生命周期安全加固，包括 `MAX_CONCURRENT_CONTAINERS` 控制、`docker kill` 回退等，应为当前优先级最高的待合并 PR。

**长期建议**：项目目前的核心开发者（ddaniels、omri-maya）贡献集中度过高（15条 PR 全部来自这两人），建议适当引入外部贡献者或划分低难度 Issue 以降低单点风险。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据NullClaw项目2026-06-13至2026-06-14（数据统计截止于2026-06-14）的GitHub数据生成的每日项目动态日报。

---

# NullClaw 项目动态日报 | 2026-06-14

## 1. 今日速览

近日（6月13日-14日），NullClaw项目活跃度中等，社区焦点集中在**关键Bug修复**和**功能扩展**两个方向。项目当前有1个高价值PR提交，旨在修复一个影响Agent定时任务投递消息的**严重内存安全问题 (use-after-free)**，对应了持续两周的Issue #941。同时，社区对一个 **JIRA集成工具** 的功能请求（Issue #914）继续保持关注。整体来看，项目正在积极解决稳定性问题以巩固核心功能，同时倾听社区对平台扩展性的需求。

## 2. 版本发布

**无** - 过去24小时内无新版本发布。

## 3. 项目进展

**关键进展：Agent定时任务消息投递 Bug 已获修复PR**

- **[PR #954 (OPEN)] Fix: one-shot cron jobs silently fail to deliver messages (use-after-free in OutboundMessage.channel)**
  - **作者**：vernonstinebaker
  - **状态**：待合并
  - **摘要**：此PR针对Issue #941报告的长期问题（Agent类型定时任务完成后，消息无法通过Telegram等渠道投递）提供了修复。作者定位到根因是`OutboundMessage.channel`属性上的**use-after-free（释放后使用）** 漏洞。该PR是项目近期最重要的代码贡献之一，直接解决了因内存管理问题导致的核心功能失效。
  - **项目意义**：一旦合并，将显著提升`schedule`功能中“agent”类型任务的可靠性，修复了静默失败的严重Bug，标志着项目在稳定性上迈出关键一步。

## 4. 社区热点

- **热点 Issue: #941 - Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens**
  - **热度分析**：该Issue创建于5月底，在过去24小时内（6月13日）被更新了**7条评论**，是近期讨论最热烈的议题。用户集中反馈了Agent定时任务在`delivery_mode: "always"`下功能异常的问题。
  - **背后诉求**：用户期望**基础自动化功能的可靠性**。当配置了明确的投递参数后，任务执行结果应该被可靠地送达。当前“静默失败”的行为严重违背了用户对“定时任务+Agent+消息推送”这一常用自动化场景的预期，社区对此感到困惑和失望。

- **热点 Issue: #914 - [enhancement] Create JIRA access tool**
  - **热度分析**：虽然仅有1条评论，但作为“enhancement”类Issue，它代表了社区对平台**集成能力**的明确需求。
  - **背后诉求**：用户希望NullClaw能成为一个连接不同工作流的枢纽。将项目管理和开发工作流（JIRA）与AI Agent的能力结合，是一个典型的“连接器”场景。这反映了用户不仅仅满足于内部对话，更希望Agent能操作外部SaaS工具，提升实际生产力。

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#941](nullclaw/nullclaw Issue #941) | Agent类型定时任务执行后不产生子进程，消息无法通过任何渠道（Telegram等）投递，表现为**静默失败**。 | **已有修复PR** ([#954](nullclaw/nullclaw PR #954))，待合并 |
| 中等 | - | 过去24小时内未报告新的崩溃或回归问题。 | - |

**分析师点评**：项目中存在一个已持续两周的严重Bug，目前已有高质量的修复PR。维护者应优先审查并合并此PR，以止血并恢复用户信心。

## 6. 功能请求与路线图信号

- **[Issue #914] Create JIRA access tool**：这是一个明确的功能请求，旨在创建一个工具使Agent和Workflow能与JIRA安全交互。
  - **纳入下版本可能性**：**高**。此类“工具调用”（Tool Calling）能力是当前AI Agent平台的标准配置。结合社区需求和项目向“平台化”发展的趋势，此功能很可能被纳入下一阶段路线图。维护团队可以此评估是否需要引入新的“Connector”或“Tool”抽象层。

## 7. 用户反馈摘要

- **主要痛点**：
  - **可靠性问题**：用户配置了Agent+定时任务+Telegram投递链，但任务“静默失败”。用户@weissfl提交的Issue #941详细描述了配置步骤和结果，明确指出`schedule`功能中的`agent`模式存在严重缺陷。这直接削弱了用户对平台核心功能的信任。
  - **缺乏可观测性**：任务标记为“completed”但子进程未启动，表明系统内部状态与实际执行状态存在偏差。用户无法获得清晰的错误日志或状态提示来诊断问题。

- **满意之处**：目前Issues和PR中未收集到正面的用户反馈，项目当前处于**修复关键Bug、重建信任**的阶段。

## 8. 待处理积压

- **[Issue #914] Create JIRA access tool** (创建于 **2026-05-13**，距今 **32天**)
  - **状态**：Open，仅有1条评论。
  - **提醒**：作为与项目扩展性高度相关的功能请求，虽然讨论热度不高（可能由于用户还在观察稳定性问题的解决），但此Issue已存在超过一个月。建议维护者进行标签管理（如：`status/needs-triage`），或发布声明说明该功能的时间表或优先级，以避免社区对项目发展方向感到不确定。

---

**报告总结**：NullClaw项目正处于一个关键转折点。技术上，一个严重的Bug已被定位并获得修复PR，项目稳定性的主要障碍即将被清除。战略上，对JIRA等外部工具的集成呼声渐起，预示着平台向“AI工作流枢纽”发展的潜力。下一步，维护者应尽快合并PR #954并发布补丁版本，以稳定核心功能，随后可着手规划并回应社区的功能请求，推动项目进入新的增长阶段。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是根据您提供的 IronClaw GitHub 数据生成的 2026-06-14 项目动态日报。

---

## IronClaw 项目日报 | 2026-06-14

### 今日速览

项目今日活跃度极高，PR 活动量是 Issues 的 10 倍以上，表明核心团队正集中精力推进重大功能开发与 Bug 修复。核心贡献者 (`core`) 主导了所有关键 PR，特别是针对 Slack 集成稳定性和附件功能的持续攻坚。尽管有 17 个 PR 处于待合并状态，但合并/关闭速度（5个）尚可，整体项目处于快速发展阶段。值得注意的是，`#3708` 版本发布 PR 也在活跃更新中，预示新版本即将到来。

---

### 版本发布

- **无新版本发布。**

---

### 项目进展

今日合并/关闭了 5 个 PR，均为与附件（Attachments）功能相关的核心基础工作，标志着该项目已进入收尾阶段：

1.  **附件功能栈核心基础设施完成**：PR `#4654`、`#4655`、`#4668`、`#4670` 和 `#4672` 已被合并。这分别完成了附件格式注册表、Reborn 转录合同中的附件引用、基于 `MountView` 的存储层、字节到转录附件的桥接，以及 WebChat v2 的内联上传。这标志着附件功能的**后端核心管线已全线贯通**。

2.  **项目进展加速**：随着附件核心栈的关闭，剩余的 4 个相关 PR（`#4675`、`#4676`、`#4738`、`#4777`）均为该功能的收尾和上层应用工作。这为下一阶段将附件能力开放给模型提供了坚实基础。

---

### 社区热点

今日讨论最活跃的 PR 集中在 **Slack 集成稳定性** 和 **附件功能** 两大领域，由核心开发者主导。

-   **[PR #4839] fix: preserve invocation identity across auth-gate re-dispatch (Slack re-approval loop)**：此 PR 旨在修复 Slack 场景下反复要求用户重新授权的循环 Bug。其描述详细分析了根本原因，并提出了复杂的解决方案，反映了该问题的严重性和修复难度。这是今日最受关注的修复工作。
-   **[PR #4838] Explicit gate-open feedback for busy threads (no parking)**：此 PR 提出了一个新的“忙时拒绝”策略，替换了旧的“延迟-排空”机制。它直接改变了用户与繁忙线程的交互方式，从“后台重试”变为“明确拒绝并提示用户重试”，是一个重要的行为变更。
-   **附件功能系列 PR (`#4675`, `#4676`, `#4738`)**：这些 PR 持续推动附件功能从“能用”演进到“好用”和“可见”。社区关注点在于如何让模型真正理解并使用附件，及前端如何呈现。

---

### Bug 与稳定性

-   **（严重）[Issue #4108] Nightly E2E failed**：每日 E2E 测试持续失败，从 5月27日至今超过两周未解决。这是一个关键的稳定性信号，表明主干代码可能存在严重的回归问题。
    -   **是否有修复PR：无**。尽管多个 PR 正在修复特定场景的 Bug，但并未直接关联到此 E2E 失败的根本原因。

-   **（高）[PR #4839] Slack re-approval-loop fix**：此 PR 明确标记为解决一个在生产环境（Slack QA）观测到的严重用户问题，即“连续四次授权门控”的情况。该修复已被合并到 `#4845` Issue 的关联逻辑中。

-   **（中）[PR #4844] filter delivered gate routes by raw gate string**：修复了 `gate_kind_filter` 函数中的一个导致内存分配错误的 Bug。
-   **（中）[PR #4843] single-flight gate delivery per run_id**：修复了 Slack 授权流程中消息可能被重复处理的 Bug。
-   **（中）[PR #4840] surface missing-credential auth gate before the approval gate**：修复了授权流程中错误的顺序问题，防止用户批准一个无法执行的操作。

---

### 功能请求与路线图信号

-   **Slack 集成稳定性**：一系列针对 Slack 的修复 PR（`#4839`, `#4843`, `#4844`）表明，改善 Slack 作为分发渠道的健壮性是当前**最高优先级的短期路线图**。
-   **附件功能**：`#4644` 系列 PR 的合并，标志着经过长期开发的附件功能即将进入 **Beta 阶段**。下一个版本极有可能包含此功能。PR `#4777` 和 `#4738` 则分别关注了其在 WebUI 和前端的集成，标志着向全面可用迈进。
-   **Reborn (重生/重试) 机制**：`#4838` 和 `#4841` 两个 PR 正在重构 Reborn 的核心行为。`#4841` 专注于消除“运行崩溃”类的终端错误，提高系统的容错性；`#4838` 则调整了并发控制策略。这暗示项目正在为**更可靠、更具韧性的生产环境运行**做长期准备。
-   **运行时上下文增强**：`#4836` PR 为模型提供了更丰富的运行时上下文（连接的频道、投递状态、运行来源）。这表明项目正致力于**增强模型的感知能力**，使其能做出更好的自主决策。

---

### 用户反馈摘要

当日无新的 Issues 评论。现有 Issues/Comments 未提供具体的用户场景或不满表达。从 Bugs/PR 描述中可以推断出以下痛点：

-   **Slack 重复授权**：用户在 Slack 上调用需要 OAuth 授权的能力时，会遭遇多次、无休止的授权请求，严重影响体验。
-   **线程繁忙无反馈**：当系统正在处理一个长时间任务时，用户的后续消息会被系统内部处理，用户得不到任何明确“忙”或“稍后再试”的反馈，导致困惑。
-   **授权流程中断**：当能力缺少凭证时，系统仍会要求用户先批准操作，然后再提示缺少凭证，导致批准操作被浪费，造成负面体验。

---

### 待处理积压

1.  **[Issue #4108] Nightly E2E failed**
    -   **状态**：`OPEN`，持续 18 天
    -   **严重性**：**极高**。每日回归测试持续失败，团队应优先分配资源排查根本原因。
    -   **链接**：https://github.com/nearai/ironclaw/issues/4108

2.  **[PR #3708] chore: release**
    -   **状态**：`OPEN`，持续 29 天
    -   **影响**：包含 `ironclaw_common` 和 `ironclaw_skills` 的 Breaking Changes，及 `ironclaw` 的多版本号跳跃。该 PR 长期未合并会导致其他功能集成困难，并让社区依赖的 API 产生分歧。
    -   **链接**：https://github.com/nearai/ironclaw/pull/3708

3.  **[PR #4264] feat(gateway): add routine create endpoint**
    -   **状态**：`OPEN`，持续 14 天
    -   **原因**：由新贡献者 (`contributor: new`) 提交，可能因代码审查周期较长或被更高优先级的任务（如 Slack Bug 修复）阻塞。
    -   **链接**：https://github.com/nearai/ironclaw/pull/4264

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI GitHub 数据，我为您生成了 2026-06-14 的项目动态日报。

---

## LobsterAI 项目动态日报
**日期**: 2026-06-14
**分析师**: AI Expert

### 1. 今日速览

过去24小时内，LobsterAI 项目活跃度处于 **中等偏下** 水平。具体表现为：有少量新的 Issue 和 PR 被创建，但暂无新的版本发布。值得注意的是，所有最近的活动（包括4个Issue和5个PR）均处于 **“stale”（已过时）** 状态，表明项目的核心维护工作可能暂时放缓，或社区反馈存在一定积压。尽管有一些针对技能（Skills）和 MCP 界面的修复 PR 在近期被合并，但项目整体向前推进的步伐似乎有所减缓。

### 2. 版本发布

无

### 3. 项目进展

过去24小时内，有两个关键 PR 被关闭/合并，它们代表了项目在用户体验层面的重要修复：

-   **[#1466] fix(mcp): modal close button unreachable when content grows tall** （已关闭）
    -   **链接**: [PR #1466](https://github.com/netease-youdao/LobsterAI/pull/1466)
    -   **分析**: 修复了 MCP 服务器表单在内容较多时，关闭/取消按钮因滚动问题而无法点击的 UI Bug。这显著改善了用户配置 MCP 服务器的体验。
-   **[#1467] fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS** （已关闭）
    -   **链接**: [PR #1467](https://github.com/netease-youdao/LobsterAI/pull/1467)
    -   **分析**: 修复了在 macOS 系统上快捷键面板仍显示 `Ctrl` 而非 `Cmd(⌘)` 的平台兼容性问题。此改动提升了 Mac 用户的操作直观性和一致性。

以上两项合并代表了项目在过去两天内对用户界面细节和跨平台体验的优化。

### 4. 社区热点

过去24小时内，社区讨论热度较为分散，并无单一 Issue 或 PR 成为绝对热点。所有活跃的 Issue 和 PR 评论数均在1-2条之间。这反映出当前社区更倾向于提交问题或贡献代码，而非进行大规模的公开讨论。

尽管如此，以下 Issue 反映了用户在实际使用中的普遍诉求：

-   **[#1443] 有计划支持新版本的openclaw吗？**
    -   **链接**: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)
    -   **热度**: 有2条评论，是当前讨论最多的 Issue。
    -   **诉求分析**: 用户提出了向上游依赖 `openclaw` 进行适配的需求。这表明项目依赖的第三方库发生了破坏性变更，用户期望项目团队能及时跟进，以保证项目的可用性和稳定性。这是关乎项目生态健康的重要信号。

### 5. Bug 与稳定性

今日报告了3个处于 **“open”** 状态的 Bug，均为 `stale` 状态，且暂无对应的修复 PR。按严重程度排列如下：

1.  **[严重] [Issue #1443] 有计划支持新版本的openclaw吗？**
    -   **链接**: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)
    -   **描述**: 因上游依赖 `openclaw` 更新带来了 breaking change，导致用户无法正常启动项目。此问题直接影响用户体验，属于 **阻断性** Bug。
    -   **修复状态**: 未标记修复。

2.  **[中等] [Issue #1439] 上传技能已停用，对话中仍然可以调用**
    -   **链接**: [Issue #1439](https://github.com/netease-youdao/LobsterAI/issues/1439)
    -   **描述**: 用户停用技能后，在对话中仍能通过关键字触发。这属于 **逻辑错误**，可能在多技能场景下造成意外行为，影响模型路由的准确性。
    -   **修复状态**: 未标记修复。有趣的是，[PR #1445](https://github.com/netease-youdao/LobsterAI/pull/1445) 正着手修复技能重复导入的问题，但似乎未触及此功能启用/停用的逻辑错误。

3.  **[中等] [Issue #1437] 创建定时任务时，清空日历后点击创建按钮无响应**
    -   **链接**: [Issue #1437](https://github.com/netease-youdao/LobsterAI/issues/1437)
    -   **描述**: 创建定时任务时，特定操作序列（选择不重复 -> 清空日历 -> 点击创建）导致按钮失效且无任何错误提示。这属于 **功能性缺陷**，用户体验不佳。
    -   **修复状态**: 未标记修复。

### 6. 功能请求与路线图信号

-   **[功能请求] [Issue #1443] 适配新版本 openclaw**
    -   **链接**: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)
    -   **信号分析**: 这是当前最强烈的外部依赖适配需求。该请求的优先级可能很高，因为它直接决定了部分用户的系统能否正常运行。项目路线图应优先考虑对此进行跟进和发布。

-   **[功能优化] [PR #1440] 重新设计已选技能标签的展示位置**
    -   **链接**: [PR #1440](https://github.com/netease-youdao/LobsterAI/pull/1440)
    -   **信号分析**: 项目团队内部（`gongzhi-netease`）已有明确的代码贡献，旨在优化 Cowork 功能中技能选择的 UI 交互。此项改进有望解决 `#1439` 和 `#1442` 中用户提到的技能管理混乱问题。这暗示团队正在积极思考如何提升 Cowork 模块的用户体验。

-   **[功能扩展] [PR #1441] 扩展工件预览管线 (HTML, React, Mermaid)**
    -   **链接**: [PR #1441](https://github.com/netease-youdao/LobsterAI/pull/1441)
    -   **信号分析**: 这是一个来自社区（`febugcoder`）但经过项目组修复的 PR，旨在为 Cowork 会话增加强大的内容预览能力。这是对 Cowork 功能的 **重大增强**，如果合并，将使 LobsterAI 成为更具竞争力的 AI 协作平台。

### 7. 用户反馈摘要

-   **痛点 1: 技能管理混乱**
    -   **反馈**: 用户 `devilszy` 在 `#1439` 和 `#1442` 中反馈了技能启用/禁用逻辑不符预期，并且在 Agent 对话中技能引用状态展示不一致。
    -   **分析**: 用户对 Agent 的技能选择、展示和调用机制存在困惑，期望一个更明确、更稳定的技能触发和展示逻辑。

-   **痛点 2: UI 交互有缺陷**
    -   **反馈**: 用户 `xuzx-code` 在 `#1437` 中反馈了创建定时任务时出现的无响应 Bug。
    -   **分析**: 用户期望项目具有良好的边界情况处理和清晰的错误反馈机制，即使是零碎的操作步骤也不应导致功能完全失效。

-   **痛点 3: 依赖版本滞后**
    -   **反馈**: 用户 `Juzisuan965` 在 `#1443` 中提出了对 `openclaw` 版本的适配担忧。
    -   **分析**: 用户作为早期采用者，对项目依赖的更新非常敏感。他们期望项目能快速响应上游变更，否则将面临无法使用的风险，这会直接影响他们对项目的信任度。

### 8. 待处理积压

以下为长期未响应或处于停滞状态的重要 Issue 和 PR，提醒维护者关注：

1.  **[严重] [Issue #1443] 有计划支持新版本的openclaw吗？** （创建于 2026-04-03）
    -   **链接**: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)
    -   **备注**: 这是一个可能影响用户上线的阻塞性问题，已存在两个多月未获官方回应。

2.  **[功能增强] [PR #1441] feat(artifacts): add extensible preview pipeline for HTML, React and Mermaid** （创建于 2026-04-03）
    -   **链接**: [PR #1441](https://github.com/netease-youdao/LobsterAI/pull/1441)
    -   **备注**: 一个已经解决冲突并修复了5个 Bug 的重大功能 PR，但已停滞超过两个月，等待项目维护者的最终 Review 和合并。

3.  **[Bug 修复] [Issue #1439] 上传技能已停用，对话中仍然可以调用** （创建于 2026-04-03）
    -   **链接**: [Issue #1439](https://github.com/netease-youdao/LobsterAI/issues/1439)
    -   **备注**: 逻辑层面的 Bug，影响技能使用的可靠性。已有 PR [#1440](https://github.com/netease-youdao/LobsterAI/pull/1440) 和 [#1445](https://github.com/netease-youdao/LobsterAI/pull/1445) 尝试优化相关机制，但本 Issue 的核心问题仍有待确认及修复。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 | 2026-06-14

## 1. 今日速览

过去24小时内，Moltis 项目活动集中在解决一个关键 Bug 上，活跃度处于**中等水平**。项目收到一个关于 **MCP OAuth 授权流程在实际服务（如 Notion, Linear）中失败**的严重 Bug 报告，并已由同一作者提交了修复 PR。目前该 Bug 尚无官方合并修复，但社区响应迅速，问题定位清晰。无新版本发布，项目整体处于“紧急修复”状态。

## 2. 版本发布

无

## 3. 项目进展

- **无已合并 PR**。今日唯一提交的 PR (#1120) 正等待审查和合并。该 PR 直接针对今日报告的严重 Bug (#1119)，一旦合并，将修复 Moltis 在集成 Notion、Linear 等主流 MCP 服务器时的 OAuth 认证流程，对提升项目与其他第三方服务的兼容性至关重要。

## 4. 社区热点

- **最活跃 Issue: [#1119] MCP OAuth fails with `invalid_target`**  
  *链接: https://github.com/moltis-org/moltis/issues/1119*  
  该 Issue 是今日讨论的绝对焦点。用户 `xzavrel` 报告了在添加 Notion 和 Linear 的 MCP 服务器时，OAuth 授权流程因 `resource_metadata` 参数而失败。该问题直接影响了用户整合主流生产力工具的能力，因此引发了关注。作者在发现问题后迅速定位了根因（`fetch_resource_metadata()` 函数处理逻辑不当），并立即提交了修复 PR，展现了社区的主动性。

## 5. Bug 与稳定性

- **严重 Bug: MCP OAuth 认证失败**
  - **描述**: 当 MCP 服务器的 `WWW-Authenticate` 头部包含 `resource_metadata` 参数时（例如 Notion, Linear），OAuth 流程报错 `invalid_target`，导致无法完成服务授权。
  - **影响范围**: 影响所有通过 OAuth 集成的 MCP 服务器，特别是使用了较新标准的服务。
  - **状态**: 已有 **修复 PR (#1120)** 待合并，但官方尚未合并。严重程度高，建议维护者优先处理。

## 6. 功能请求与路线图信号

今日无新功能请求。但 Issue #1119 及 PR #1120 实际上暴露了现有 MCP 集成模块在协议兼容性上的一个缺口。该项目可能需要在后续版本中增强对 MCP OAuth 规范中 `resource_metadata` 等可选参数的支持，以兼容更多第三方服务。

## 7. 用户反馈摘要

- **使用痛点**: 用户 `xzavrel` 在使用 Moltis 连接主流的 Notion 和 Linear MCP 服务时遭遇了阻塞性问题。这表明 OAuth 流程的鲁棒性不足，在处理非标准协议的变体时容易出错。用户通过提交 Issue 和代码修复的方式表达了强烈的改进需求。

## 8. 待处理积压

- **[#1120] fix(mcp): use direct fetch for resource_metadata URL from WWW-Authenticate**  
  *链接: https://github.com/moltis-org/moltis/pull/1120*  
  这是针对今日最严重 Bug 的 **修复 PR**。目前无评论，状态为 `[OPEN]`。建议项目维护者尽快审查并合并此 PR，以解决用户无法使用关键第三方服务的痛点。

---

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据提供的 CoPaw 项目数据生成的 2026-06-14 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-06-14

## 今日速览

今日项目活跃度**极高**。过去24小时内，Issues 与 PR 更新均达8条，呈现出发行版发布后典型的社区反馈与贡献高峰。社区一方面积极报告影响日常使用的 Bug（如聊天无响应、上下文丢失），另一方面也提出了多项功能增强请求（如支持新的模型平台、添加新语言和渠道）。特别值得注意的是，一位贡献者（`ly-wang19`）在一天内提交了4个修复 PR，覆盖从上下文管理到备份机制的多个缺陷，显示出社区对项目稳定性的关注和积极贡献。项目整体处于从新功能扩张到稳定性与体验优化的转型期。

## 版本发布

今日无新版本发布。

## 项目进展

今日有2个 PR 被合并/关闭，标志着特定功能的最终落地：

- **#2498 [CLOSED] fix(agents): use console language when creating agent and fallback unsupported langs**：这是一个重要的修复，解决了新创建的 Agent 始终默认使用英文、且提示词（Persona MD）文件始终复制中文版本的 Bug。该 PR 确保新 Agent 会继承用户的界面语言设置，并为不支持的语言提供优雅降级。这份贡献由社区成员 `Alneys` 完成，历经数月终被合并，是项目国际化的重要一步。
- **#4969 [CLOSED] feat(skill): Add skill tag batch download**：该 PR 由 `Leirunlin` 提交，为技能的批量下载功能增加了按标签（Tag）筛选的能力。这解决了 Issue #2961 中社区提出的需求，提升了用户管理和复用技能资产的效率。

项目在用户体验一致性和技能管理功能上取得了实质性进展。

## 社区热点

今日讨论热度最高的议题集中在用户体验和功能覆盖上：

1. **[#5047] Windows Tauri 桌面端启动特别慢**：该 Issue 自6月9日创建以来持续活跃，共获3条评论。用户报告从 Python 打包切换至 Tauri 后，启动时间从1-2分钟骤增至十几分钟，且易进入无响应状态。这反映了桌面端重构带来的性能回退问题，是当前影响重度 Windows 用户的**首要体验痛点**。 [链接](https://agentscope-ai/QwenPaw Issue #5047)

2. **[#5156] 建议支持 kimi-for-coding / 加入 uv 白名单**：该 Issue 获得了4条评论，是今日评论数最多的议题之一。用户 `wjt0321` 详细阐述了其诉求：已订阅 `kimi-for-coding` 套餐的用户无法在 QwenPaw 中使用该套餐，只能调用标准 API。这暴露了项目在**第三方模型接入策略**上的局限性，可能阻碍已付费用户的转化。 [链接](https://agentscope-ai/QwenPaw Issue #5156)

## Bug 与稳定性

今日报告的 Bug 问题较为集中，且已有部分对应的修复 PR 在审查中（`Under Review`）。按严重程度排序如下：

- **[严重] #5172 [CLOSED] 聊天总出现问完问题没反应一直等待**：用户 `kfrtiamo` 报告了一个严重影响日常使用的问题：对话闲置一段时间后，再次提问会陷入无限等待，必须手动停止。用户强调，此 Bug 在通过 QQ、微信等无法手动停止的渠道使用时将导致“直接嘎了”。该 Issue 已被关闭，但未提及具体修复，需密切关注是否随新版本发布。 [链接](https://agentscope-ai/QwenPaw Issue #5172)

- **[高] #5174 [Bug]: 定时任务和心跳机制的缺陷是吗？**：用户 `YUZHU5109` 报告了 Cron Agent 和心跳 Agent 的核心功能缺陷：Cron Agent 无法产出知识文件，心跳 Agent 不执行知识提取任务。这表明**自动化任务系统的可靠性**存在根本性问题。 [链接](https://agentscope-ai/QwenPaw Issue #5174)

- **[中] #5171 [Bug]: 上下文压缩保留缺少按条数保留或排除人设文件，导致信息完全丢失**：用户 `MCQSJ` 报告了上下文压缩机制的一个逻辑缺陷：当 Agent 的人设文件 (Profile) 大于压缩阈值时，压缩会导致**上下文完全清空**，从而中断任务。这是一个需要谨慎处理的数据丢失问题。 [链接](https://agentscope-ai/QwenPaw Issue #5171)

- **修复 PR 在审**：
    - **#5038**: 修复 `LightContextManager.pre_reply` 在处理空消息列表 (`msg == []`) 时的 `IndexError` 崩溃问题。 [链接](https://agentscope-ai/QwenPaw PR #5038)
    - **#5041**: 修复备份功能中，单个文件不可读导致**整个备份失败**的问题。 [链接](https://agentscope-ai/QwenPaw PR #5041)
    - **#5040**: 修复 Cron 任务配置文件中单个任务格式错误导致**所有任务加载失败**的问题。 [链接](https://agentscope-ai/QwenPaw PR #5040)
    - **#5035**: 修复 `llama.cpp` 版本号解析使用固定宽度切片，在版本号超过4位数时解析失败的潜在 Bug。 [链接](https://agentscope-ai/QwenPaw PR #5035)

## 功能请求与路线图信号

今日新增的功能请求呈现出明显的**国际化**和**平台扩展**趋势：

1. **#5169 [Feature Request] Add Vietnamese (vi) interface language**：用户 `biencuong` 请求添加越南语界面。这通常意味着项目在越南用户群体中有了一定规模的使用基础。 [链接](https://agentscope-ai/QwenPaw Issue #5169)

2. **#5168 Add official Zalo Bot channel support**：用户 `lamnguyen3119` 要求添加 Zalo 机器人渠道支持。Zalo 是越南最流行的社交平台之一，这与 #5169 的语言请求同频，强烈暗示**越南市场是下一个重要的增长点**。 [链接](https://agentscope-ai/QwenPaw Issue #5168)

3. **#5156 [Feature]: 建议支持 kimi-for-coding / 加入 uv 白名单**：如前所述，这是一个关于模型平台接入策略的典型请求。如果项目能提供更灵活的 “自选 API 模式” 而非仅限标准 API，将能吸引更多付费用户。 [链接](https://agentscope-ai/QwenPaw Issue #5156)

此外，**PR #5170** (`perf(agents): cache PROFILE.md reads on the agent-list endpoint`) 显示社区正在关注性能优化，该 PR 建议对 Agent 列表查询接口进行缓存，以减轻磁盘I/O压力。这可能是未来性能优化方向的一个信号。 [链接](https://agentscope-ai/QwenPaw PR #5170)

## 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出以下用户声音：

- **“桌面端体验降级明显”**：多位 Windows 用户反馈，从 Python 版本切换到 Tauri 版本后，启动速度严重下降（#5047）。这是当前最集中的负面反馈。
- **“高调宣传的功能不可用”**：用户指出，定时任务和心跳机制等核心自动化功能存在缺陷，无法按预期执行知识提取等重任务（#5174），这损害了项目的核心价值主张。
- **“付费套餐用户被忽视”**：已订阅第三方模型（如 Kimi Coding）套餐的用户，感觉自己的付费能力无法在项目内充分利用，抱怨项目接入策略过于死板（#5156）。
- **“基础对话交互不够稳定”**：对话闲置后无响应问题（#5172）被用户形容为“一直存在”的“严重问题”，直接影响了用户对项目可靠性的信心。

## 待处理积压

以下为长期未关闭或值得关注的重要议题，提醒维护者关注：

1. **[高关注度] Issue #5047: Windows Tauri 桌面端启动特别慢**：创建已逾5天，虽已有3条评论，但尚未看到官方或社区的针对性修复 PR。该问题涉及底层框架迁移，解决难度可能较高，但用户抱怨强烈，建议优先投入资源。 [链接](https://agentscope-ai/QwenPaw Issue #5047)

2. **[新晋贡献者 PR] #5037, #5038, #5040, #5041**：社区贡献者 `ly-wang19` 提交了4个高价值的 Bug 修复 PR，目前均为 `Under Review` 状态。这些 PR 覆盖了浏览器检测、上下文管理、任务加载、备份功能等多个方面，建议尽快完成审查与合并，以稳定代码库并鼓励社区贡献。 [链接1](https://agentscope-ai/QwenPaw PR #5037) | [链接2](https://agentscope-ai/QwenPaw PR #5038) | [链接3](https://agentscope-ai/QwenPaw PR #5040) | [链接4](https://agentscope-ai/QwenPaw PR #5041)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 ZeroClaw 项目数据生成的 2026-06-14 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-14

## 1. 今日速览

项目今日保持极高活跃度，过去 24 小时内共产生 92 条 Issue/PR 更新。社区讨论热烈，尤其在“代理协作”、“架构统一”和“用户体验”三个方向上。开发团队正在密集处理多个高优先级 Bug（尤其是 WebSocket 会话和 Web 仪表盘相关问题），并积极推进数个重量级 RFC（如“原生动态链接库插件系统”和“OCI 容器注册表”）。尽管无新版本发布，但项目正处在一个功能重构与基础架构升级的关键阶段，整体健康度良好，但稳定性风险较高。

## 3. 项目进展

过去 24 小时，项目在合并/关闭重要 PR 方面取得进展，关键推进如下：

*   **架构统一与流程优化：**
    *   [PR #7398](https://github.com/zeroclaw-labs/zeroclaw/pull/7398) **已合并**：实现了定时任务 (`cron`) 的暂停/恢复功能，允许在不删除任务的情况下动态启用或禁用，增强了任务调度的灵活性。
    *   [Issue #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) **已关闭**：关于“统一三个代理轮转引擎”的 RFC（基于 [PR #7540](https://github.com/zeroclaw-labs/zeroclaw/issues/7415#issuecomment-4690480530)）已完成实施。这标志着代理核心执行逻辑的简化与统一，是向更稳定、更可维护架构迈出的重要一步。
    *   [Issue #6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) **已关闭**：澄清了 `risk_profile.allowed_tools` 配置对 MCP 工具的限制问题，确认其为设计意图并更新了文档，消除了用户困惑。

*   **关键 Bug 修复：**
    *   [Issue #6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723) **已关闭**：修复了 OpenAI 原生 provider 硬编码 120 秒超时，忽略用户配置 `timeout_secs` 的问题。已提交 [PR #????] 进行修复。
    *   [Issue #7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378) 和 [Issue #7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) **已关闭**：修复了 ZeroCode TUI 在 macOS 下的 `Cmd-C` 退出冲突和深色主题文本不可读的问题。
    *   [PR #7549](https://github.com/zeroclaw-labs/zeroclaw/pull/7549) **已提交**：修复了 CLI 安装的 WASM 插件因路径不匹配而不可见的关键 Bug，并提供了旧数据迁移支持。

## 4. 社区热点

本期社区焦点主要集中在以下几个议题：

1.  **“Dream Mode” 功能预热：** [Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) 作为评论数最多的 Issue（18条），引发了关于“空闲期内存整合与反思学习”的广泛讨论。这反映了社区对更智能、更具记忆持久性代理的强烈期望，是项目长期路线图的重要信号。

2.  **架构讨论走向前沿：**
    *   [Issue #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) (RFC: 统一代理引擎，4条评论) 和 [Issue #7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) (RFC: 原生动态库插件系统，3条评论) 尽管评论数不高，但均为深度架构讨论，吸引了核心贡献者和维护者的参与。这显示出社区正从用户功能需求转向驱动项目底层架构演进。
    *   **分析：** 社区活跃的核心力量正从单一用户转向开发者与架构师，他们关注项目的可扩展性、模块化和解耦，这是开源项目走向成熟的关键标志。

## 5. Bug 与稳定性

过去 24 小时内报告了多个高严重性 Bug，现有分支的回归问题尤其值得关注。以下是按严重程度排列的关键 Bug：

*   **S1 - 工作流阻塞：**
    *   **[Bug #7563]**: `canvas-store` 在 WS 聊天/ACP 会话中的回归问题，导致 Web UI 的 `/canvas` 页面空白。**状态：** 已报告，待处理。
    *   **[Bug #7542]**: `ask_user` 工具在 Web 仪表盘 WebSocket 会话中立即失败，提示“Channel closed”。**状态：** 已有 [PR #7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588) 提交修复。
    *   **[Bug #7527]**: macOS 应用安装后不可用，无法检测权限，窗口消失。**状态：** 已报告，待处理。
    *   **[Bug #7523]**: Web 仪表盘在 macOS 上 `cargo web build` 后不可用。**状态：** 已报告，待处理。
    *   **[Bug #7507]**: `zeroclaw quickstart` 在非 TTY 环境下陷入无限重绘循环，输出高达 4.3GB。**状态：** 已关闭，已修复。

*   **S2 - 行为降级：**
    *   **[Bug #7539]**: `llama.cpp` 模型默认设置不佳，用户难以快速切换模型。**状态：** 已报告，已有功能请求 [Feature #7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)。

## 6. 功能请求与路线图信号

本周的功能请求呈现明显的“AI 精细化”和“平台扩展”趋势。

*   **有望纳入 v0.8.1 或后续版本的新功能：**
    *   **[Feature #5849]**: **Dream Mode** (内存整合与反思学习)：评论数最高，社区期待度高，极可能成为下一阶段的核心功能。
    *   **[Feature #7521]**: **`file_read` 工具支持非 UTF-8 编码**：解决了一个现实世界中频繁遇到的痛点，实现成本较低，有望快速合并。
    *   **[Feature #7518]**: **WhatsApp Web 消息反应**：提升用户体验，与 Telegram/Discord 等渠道对齐，价值明确。
    *   **[Feature #7543]**: **Web 会话侧栏（多会话支持）**：基础 UI 改进，显著提升 Web 聊天界面的可用性。
    *   **[Feature #7531]**: **QQ/DingTalk/微信/飞书的流式卡片消息**：优化国内用户实时交互体验，减少等待焦虑。

*   **已与现有 PR 关联的长期路线图信号：**
    *   **插件系统变革**：[RFC #7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) (原生动态库插件) 和 [RFC #7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) (OCI 容器注册表) 正在重新定义插件的存储、分发和发现机制，这将是未来几个版本的核心变革方向。

## 7. 用户反馈摘要

- **痛点：**
    - **稳定性与版本兼容性**：用户 `luckbyte` 和 `swellee` 报告 macOS 版本无法正常使用，提示用户“运行 `zeroclaw` 前请仔细阅读 [README](https://github.com/zeroclaw-labs/zeroclaw)”和“遇到问题请提交 Issue”。 (`#7523`, `#7527`)
    - **文档与实际行为不符**：`perlowja` 指出 `risk_profile.allowed_tools` 对 MCP 工具无效的情况，尽管是设计如此，但文档的缺失导致用户困惑和配置浪费。 (`#6876`)
    - **企业级部署障碍**：用户 `nick-pape` 报告 OpenAI provider 硬编码超时，导致长时间任务失败，这限制了其在企业级关键任务场景中的应用。 (`#6723`)
    - **本地化用户体验**：`metalmon` 指出 `file_read` 无法正确处理非 UTF-8 (如中文Windows-1251) 文件，这对非英语用户的工作流造成干扰。 (`#7521`)

- **积极反馈与场景：**
    - `abdulhakam` 在 `#7539` 中积极反馈 `llama.cpp` 的本地使用体验，并提出了合理的改进建议，体现社区对本地化部署的支持。
    - 多位用户 (`Audacity88`, `singlerider`, `JordanTheJet`) 积极提交详细的 Bug 报告和 PR，表明社区贡献者与维护者之间的协作非常深入。

## 8. 待处理积压

以下长期未获响应或进展缓慢的 Issue/PR 需要维护者关注，以避免社区贡献者流失或功能缺口扩大：

*   **[Feature: Dream Mode] (#5849)**: 自 4月18日提出，社区讨论热烈，但目前尚无明确的实现计划或 RFC 更新。应安排时间进行技术评审。
*   **高重要性且长期阻塞的 PR：**
    - **[PR #5797]**: 为自定义推理提供商添加 TLS 证书支持。自4月16日提出，5月标记为“无作者响应”，但仍处于开放状态。这是一个对私有化部署非常重要的功能。
    - **[PR #6667]**: (feat/skills: background review fork + skill_manage tool)。这是一个 XL 大小的 PR，也是技能系统演进的关键一步，但自5月14日提交后进展缓慢。需要评估其与 [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)（Prompt触发安装）等同类功能的整合策略。
*   **标签为 `needs-maintainer-review` 的 RFC：**
    - **[RFC #7420]**: 原生动态库插件系统。
    - **[RFC #7497]**: OCI 容器注册表插件发现。
    - **提醒：** 这两个 RFC 属于重大架构决策，需要维护者团队尽早给出方向性意见，以避免开发工作的浪费。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*