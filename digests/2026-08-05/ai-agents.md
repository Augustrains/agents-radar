# OpenClaw 生态日报 2026-08-05

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-05 01:18 UTC

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

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 OpenClaw 项目动态日报（2026-08-05）。

---

# OpenClaw 项目动态日报 — 2026-08-05

## 1. 今日速览

OpenClaw 项目今日社区活跃度极高，24小时内共有500条Issue和500条PR更新，其中新开/活跃Issue 458条，待合并PR 389条。项目目前面临**严重的稳定性挑战**，大量高优先级（P1）Bug集中在**消息丢失（message-loss）**、**会话状态（session-state）损坏**及**崩溃循环（crash-loop）** 问题上，且许多关键问题长期未决。虽然有大量PR（389条）在等待合并，但今日暂无新版本发布，核心维护者可能需要加快对关键Bug修复的审查和合并节奏。

## 2. 版本发布

- **无**。今日没有发布新版本。

## 3. 项目进展

今日没有PR被合并或关闭（根据提供数据，111条已合并/关闭但未展示具体条目），整体项目处于**高吞吐、低消化**的状态。最突出的进展是社区提交了大量修复PR，但均处于待审查状态。值得关注的已提交PR（等待审查）包括：

- **[PR #119396] fix(qa): stop zombie-only gateway process groups**：由维护者 `vincentkoc` 提交，修复QA测试中因僵尸进程导致误报的问题，体现对基础设施健壮性的持续关注。
- **[PR #118681] fix(agents): bounded memory flush before recovery compaction**：修复了会话压缩前不执行内存刷新的问题，直接回应了多项与数据丢失相关的Issue。
- **[PR #119023] fix(slack): preserve channel context in bot-opened threads**：修复Slack渠道中bot开启回复线程时丢失频道上下文的问题，改善了用户体验。

**结论**：项目进展主要依靠社区驱动的PR提交，但合并速度是当前瓶颈。维护者需要优先处理与高优Bug（特别是数据丢失类）相关的PR。

## 4. 社区热点

今日讨论热度最高的当属 **[Issue #116277] (CLOSED) DeepSeek v4 Flash silent reply failure**，评论数高达 **104** 条。该问题描述了模型静默失败且仅回复通用回退信息的情况，引发了大量用户共鸣和讨论。尽管该Issue已被关闭，但高评论数表明用户对模型回复可靠性的焦虑。

其次，**[Issue #116201] (OPEN) Realtime voice work can retain unbounded provider and consult state** 有59条评论。作为P1级Bug，它讨论的是实时语音功能中资源未被正确清理的问题。修复该问题有助于提升长时间运行时的稳定性。

此外，多个关于**子代理（Subagent）结果静默丢失**的Issue（如 #44925, #67777）评论数持续上升，成为社区讨论的焦点。

**分析**：社区最大的情绪集中在对**“静默失败”**和**“工作丢失”**的强烈不满。这不仅是技术Bug，更影响了用户对AI助手核心信任度。

## 5. Bug 与稳定性

今日报告和讨论的Bug数量庞大，主要集中在以下几个严重等级：

**🔴 严重 (P1, 涉及消息/数据丢失)**
- **[Issue #116277]**: DeepSeek v4 Flash 静默无回复。已关闭，但影响大。
- **[Issue #44925] & [Issue #67777]**: 子代理完成结果静默丢失。这两个老Issue仍为 OPEN 状态，且均有高评论数，说明核心问题未解。**暂无直接关联的 fix PR**。
- **[Issue #115326]**: 崩溃循环熔断器导致 Discord/WhatsApp 永久抑制，恢复路径失效。已关闭。
- **[Issue #115908]**: 会话记录投影在持续写入下可能活锁，阻塞主线程。**暂无关联 fix PR**。

**🟠 高 (P1, 影响会话状态/可用性)**
- **[Issue #118846]**: 网关主线程从启动即被插件元数据快照和文件系统状态查询占满，导致本地RPC死亡。**暂无关联 fix PR**。
- **[Issue #111498]**: 主Agent被持久化的工作区状态迁移阻塞，导致Anthropic认证恢复后无法工作。
- **[Issue #119263]**: Agent数据库 v14->v15 迁移失败，导致网关无法启动。这是升级阻断问题，需要高度关注。**暂无关联 fix PR**。
- **[Issue #119333]**: Codex 工具 `request_user_input` 在 Default 模式下暴露但运行时被拒绝，模型可能产生错误调用。

**🟡 中 (P2, 影响特定功能/体验)**
- **[Issue #97616]**: Hook/工具子进程泄漏，导致僵尸进程积累和运行时性能下降。
- **[Issue #116010]**: 所有持久化会话上下文被强制限制在128k，无视模型配置。

**总结**：项目稳定性处于**红色警报**状态。大量P1级Bug集中在数据/消息丢失和会话状态混乱上，且修复进展缓慢。

## 6. 功能请求与路线图信号

- **[Issue #48788] feat: centralized filename encoding utility**：该Issue提出在多编码环境下统一处理文件名。已有PR (#48578) 修复了部分问题，但更全面的方案仍在讨论中。
- **[Issue #45508] Self-hosted STT/TTS provider support in webchat**：用户希望webchat的语音功能能自托管，而不是依赖浏览器API。
- **[Issue #44431] Browser tool: 7 improvements from real-world automation field test**：用户基于9个邮箱提供商注册的实战经验，提出了7项浏览器工具改进。
- **[Issue #79168] Content-based prompt injection scanning on tool output**：社区对安全性的关注度提升，要求在工具输出层面增加对提示注入的检测。
- **[Issue #46058] Chat-first Android surface**：用户正在独立开发Android前端，并希望与官方协同。

**信号**：**稳定性修复是当前第一优先级**。新功能方面，**安全增强（防注入）**、**更好的浏览器自动化体验**和**自托管语音**是值得关注的方向。维护者可能考虑将这些高赞（👍）的需求纳入下一个版本规划。

## 7. 用户反馈摘要

- **对静默失败非常失望**：Issue #116277 的104条评论是最大信号。用户表示：“DeepSeek v4 Flash 总是失败，并且给出的回退信息让人以为是我的网络问题。”
- **对恢复机制不满**：Issue #115326 提到文档中的恢复命令 `channels.start` 是无效的，这加重了用户在遇到问题时的挫败感。
- **对子代理调度缺乏信心**：Issue #44925 和 #67777 的讨论指出，在复杂的多任务场景中，结果静默丢失导致用户对自动化工作流失去信任。
- **对性能瓶颈的抱怨**：Issue #118846 中，用户反馈网关启动即高占用CPU，影响了所有依赖本地RPC的操作。有人回复：“这导致我的所有自动化脚本都晚了几分钟才跑完。”

## 8. 待处理积压

以下Issue和PR长期未得到有效推动，需要维护者优先关注：

- **[Issue #44925] (2026-03-13 创建)**：子代理完成结果静默丢失。P1级，23条评论，2个👍。
- **[Issue #67777] (2026-04-16 创建)**：子代理完成交付丢失。P1级，10条评论。
- **[Issue #48788] (2026-03-17 创建)**：中央文件名编码工具，P3但20条评论，讨论热烈。
- **[PR #118681] (2026-08-03 提交)**：修复压缩前内存刷新的问题，与数据丢失直接相关，等待审查。
- **[PR #83988] (2026-05-19 提交)**：修复Telegram TTS文本“churn”问题，长时间停滞不前。

**分析师建议**：维护者应优先处理**大量与数据丢失相关的PR和Issue**，澄清修复计划，以恢复社区信心。当前389个待合并PR的积压数量也预示着更大的维护风险。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期**: 2026-08-05  
**数据窗口**: 2026-08-04 00:00 UTC — 2026-08-05 00:00 UTC


## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态整体呈现**“高活跃、高迭代、高并发”**的三高态势。头部项目（OpenClaw、Hermes Agent、IronClaw）日均处理 50-100 条 Issue/PR 更新，社区贡献密度达到历史高位，表明该领域已成为开源世界最热门的赛道之一。生态正在从“大而全的一体化平台”向**“多功能模块化 + 多通道适配 + 多模型兼容”**方向分化演进。与此同时，**稳定性（数据丢失、静默失败）与安全性（API Key 泄漏、越权访问）**已成为跨项目的共性痛点，严重挑战用户对 AI 助手的核心信任。值得关注的是，各项目在渠道扩展、模型接入、WebUI 打磨和架构治理等维度呈现明显的差异化竞争态势，生态尚未出现“赢者通吃”的垄断格局。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 | 新版本 | 健康度 | 核心特征 |
|------|------------|---------|-----------|--------|--------|----------|
| OpenClaw | 458 新开/活跃 | 389 待合并 | 111 合并/关闭* | 无 | 🔴 紧急 | 高吞吐、低消化，P1 数据丢失 Bug 堆积 |
| Hermes Agent | 50 开启 | 46 待合并 | 4 | 无 | 🟢 健康 | 高并发贡献，P0 缓存隔离修复快速响应 |
| IronClaw | 38 新开/活跃 | 32 待合并 | 约 70+ | 无 (rc.1 冲刺) | 🟢 健康 | WS0-10 架构重构批量落地，RC 发布攻坚 |
| NanoBot | 约 15 活跃 | 19 合并 | 19 | 无 | 🟡 良好 | WebUI 打磨期，安全 Issue 30 天未解 |
| CoPaw | 28 (11 关闭) | 50 (22 合并) | 22 | v2.1.0-beta.1 | 🟡 关注 | 高活跃、时区修复链路完整，但桌面端回归 |
| ZeroClaw | 约 90 开放/推进 | 2 关闭 | 2 | 无 | 🟡 关注 | 设计评审密集、合并吞吐低，3 个 S0 安全 Bug |
| PicoClaw | 3 | 4 (2 合并) | 2 | 无 | 🟢 稳定 | 中等活跃，2 个功能 PR 待审 |
| NanoClaw | 0 | 5 (1 合并) | 1 | 无 | 🟢 稳定 | Dial 渠道（SMS+语音）整合推进中 |
| LobsterAI | 约 5 活跃 | 10+ 合并 | 10 合并 | 8.3 合入 main | 🟡 关注 | 安全 Issue #1202 停更 4 个月后复燃 |
| NullClaw | 0 | 1 待合并 | 0 | 无 | 🟢 稳定 | 低活跃，grok-cli provider 搁置 7 天 |
| Moltis | 0 | 1 (dependabot) | 0 | 无 | 🟢 稳定 | 低活跃，依赖更新为主 |
| TinyClaw | — | — | — | — | ⚪ 无活动 | 24h 零更新 |
| ZeptoClaw | — | — | — | — | ⚪ 无活动 | 24h 零更新 |

*OpenClaw 数据按“已合并/关闭但未展示条目”估计。IronClaw 合并数据根据 PR 明细估算。


## 3. OpenClaw 在生态中的定位

### 优势

- **社区规模呈断崖式领先**：24h 内 500 条 Issue + 500 条 PR 更新，是第二名（IronClaw/Hermes Agent）的 5-10 倍，生态影响力与社区动员能力在同类项目中无出其右。
- **渠道覆盖广度最大**：Discord、Slack、WhatsApp、Telegram 等主流渠道均已深度集成，且针对渠道特有场景（如 Slack bot 线程上下文）持续优化。
- **多模型/多 Provider 兼容能力强**：涵盖 DeepSeek、Anthropic、本地模型等，社区持续贡献新模型适配（非官方模型更新响应快）。
- **功能矩阵完整**：子代理（Subagent）、实时语音、Web 搜索、浏览器自动化、MCP 工具，覆盖面远超同类。

### 技术路线差异

OpenClaw 走的是 **“网关- Runner- 渠道”一体化架构**，强调开箱即用、多通道同时服务。相比之下：IronClaw 侧重**可恢复性契约与架构治理**（显式错误传播、WS0-10 重构），Hermes Agent 强调**多租户隔离与缓存安全**，而 ZeroClaw 则在**协议兼容层（Chat Completions profile）与全工具权限模型**上押注。

### 核心短板

**稳定性与信任危机**。大量 P1 级 Bug（消息丢失、会话状态损坏、崩溃循环）长期未修复，389 个 PR 积压待合并，核心维护者消化能力远跟不上社区提交速度。相比之下 IronClaw 的“错误恢复契约”已达成 100% 恢复率目标，NanoBot 的 Bug 平均修复周期在 1-3 天，OpenClaw 若不能在短期内遏制质量问题，将面临用户向竞品迁移的风险。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|----------|
| **数据/消息丢失防护** | OpenClaw、Hermes Agent | OpenClaw: 子代理结果静默丢失 (#44925)；Hermes Agent: 缓存键跨会话共享 (#78941) |
| **多租户隔离与越权防护** | Hermes Agent、ZeroClaw | Hermes: 内存操作绕过钩子系统 (#34352)；ZeroClaw: Agent 可横向越权读其他 Agent 数据 (#9646/#9647) |
| **API Key/敏感信息防护** | NanoBot、LobsterAI、ZeroClaw | NanoBot: `os.environ` 跨 Provider 泄漏 (#4784)；LobsterAI: Agent 可被诱导泄露模型 Key 信息 (#1202)；ZeroClaw: webhook 未 fail-closed (#9565) |
| **MCP 工具错误语义统一** | NanoBot (MCP 错误信封被误判为成功, #5237)、PicoClaw (MCP 连接失败导致挂起, #3269) | 协议层歧义导致 Agent 行为不可预测 |
| **长会话/上下文性能** | PicoClaw (Web UI 长历史卡顿, #3281)、OpenClaw (128k 强制截断, #116010) | 上下文管理策略缺乏精细化配置 |
| **静默失败/不可观测性** | OpenClaw (DeepSeek 静默无回复, #116277)、Hermes Agent (成本少报 37%, #78953)、ZeroClaw (历史裁剪无 token 计量) | 用户无法判断 Agent 真实状态，信任受损 |
| **多模型并行/调度** | CoPaw (多模型同时跑, #6455)、NullClaw (grok-cli provider, #981) | 从单一模型绑定走向多模型自由切换与协同 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|------|---------|---------|-------------|
| **OpenClaw** | 多渠道一体化的通用 AI 助手 | 追求开箱即用、多平台同时接入的个人/团队用户 | 网关-Runner-渠道一体化，简单直接但稳定性代价高 |
| **Hermes Agent** | 多租户安全、企业级部署、插件生态 | 需要多用户隔离与生产环境可靠性的技术团队 | Rust 核心 + 插件系统，会话隔离与缓存安全为第一优先级 |
| **IronClaw** | 可恢复性、架构治理、WASM 沙箱 | 对错误恢复和系统韧性有严格要求的高级开发者 | 强类型 Rust，WS0-10 架构重构，错误传播契约显式化 |
| **NanoBot** | WebUI 体验打磨、快速 Bug 响应 | 重视交互体验和快速迭代的个人开发者 | Python 轻量架构，当日报告当日修复的敏捷响应 |
| **CoPaw** | 桌面端体验、集成 AgentScope 生态 | 偏好原生桌面客户端的个人用户 | AgentScope 生态 + Tauri 桌面壳 + PyInstaller 打包 |
| **ZeroClaw** | 协议兼容、安全模型、目标驱动的自主执行 | 需要高度可控、可审计行为的专业用户 | RFC 驱动设计，OpenAI 协议兼容层，全工具权限层级 |
| **PicoClaw** | 轻量/嵌入式场景、成本可观测性 | 在资源受限边缘环境运行的用户 | Go 实现，强调轻量与 Provider 成本透明度 |
| **NanoClaw** | 渠道扩展（SMS/语音） | 需要电话渠道能力的企业用户 | 聚焦渠道适配层、定时任务精度、Webhook 可靠性 |
| **LobsterAI** | 中文用户、商业产品化、积分体系 | 中国市场的 C 端用户 | Electron 桌面客户端，商业功能集成度高 |
| **NullClaw** | 极简、多 CLI provider 聚合 | 已在本地使用多种 CLI 工具的核心开发者 | 复用 codex-cli 模式的轻量派发架构 |


## 6. 社区热度与成熟度分层

### 第一梯队：高热度主导者

| 项目 | 日更新量 | 阶段判断 | 核心特征 |
|------|---------|---------|----------|
| OpenClaw | ~1000 | 快速扩张期，但失速风险高 | 社区提交量远超消化能力，质量与信任正在承压 |
| IronClaw | ~100 | 版本冲刺 + 架构重构期 | 高强度开发节奏（v1.1.0-rc.1 攻坚），架构治理驱动 |
| Hermes Agent | ~100 | 健康快速迭代期 | 贡献响应闭环良好，P0/P1 修复 24h 内有 PR 跟进 |

### 第二梯队：质量巩固期

| 项目 | 日更新量 | 阶段判断 | 核心特征 |
|------|---------|---------|----------|
| CoPaw | ~78 | 功能迭代与稳定性加固并行 | 时区修复链路完整，但 Beta 桌面端回归需警惕 |
| NanoBot | ~33 | 体验打磨期 | WebUI 精细化投入大，Opus 5 当日修复值得肯定 |
| ZeroClaw | ~100 | 设计评审密集、合并偏慢 | RFC 讨论热烈但落地不足，48 个 PR 积压 |
| LobsterAI | ~14 | 版本发布稳定期 | 8.3 版本合入 main，但对安全 Issue 响应滞后 |

### 第三梯队：稳定/观望期

| 项目 | 日更新量 | 阶段判断 | 核心特征 |
|------|---------|---------|----------|
| PicoClaw | ~7 | 稳定推进期 | 2 个功能 PR 待审是关键变量 |
| NanoClaw | ~5 | 渠道整合期 | Dial（SMS+语音）是最大增量看点 |
| NullClaw / Moltis | ~1 | 低活跃守成期 | 单 PR 搁置反映维护响应偏慢 |
| TinyClaw / ZeptoClaw | 0 | 静默期 | 24h 无活动，需关注是否存活 |


## 7. 值得关注的趋势信号

### 信号一：安全从“建议”升级为“硬门槛”

**数据支撑**：ZeroClaw 暴露 3 个 S0 级安全漏洞（webhook 未认证、Agent 越权读取全库知识）；Hermes Agent 的 P0 缓存隔离修复获得最高优先级；LobsterAI 安全 Issue 停更 4 个月后复燃被视作“耻辱标记”。

**判断**：多租户隔离、敏感信息防泄漏、越权访问防护已成为生态竞争的新分水岭。开发者选型时应将安全模型与隔离能力列为第一评估维度，而非仅看功能丰富度。未来 6-12 个月内，缺乏安全纵深设计的项目将显著掉队。

### 信号二：“静默失败”成为信任杀手

**数据支撑**：OpenClaw 的 DeepSeek 静默无回复获 104 条评论；Hermes Agent 的 Telegram 轮询静默停滞；PicoClaw 的 MCP 故障导致 Agent 循环挂起无提示；NanoBot 的 MCP 错误被误判为成功导致的超时等待。

**判断**：用户对“AI 静默出错”的容忍度正在逼近零界点。IronClaw 的“可恢复性契约”——运行必须存活、模型必须看到错误、看到的内容必须包含原因与成功条件——可能成为行业标准模板。开发者应优先投资可观测性（日志、指标、错误语义）与显式错误传播机制。

### 信号三：协议兼容层正在成为“入场券”

**数据支撑**：ZeroClaw 的 Chat Completions profile RFC 获 16 条评论成为今日最热；OpenClaw 的 500 条 Issue 中大量涉及渠道/模型适配；NanoBot 快速跟进 Anthropic Opus 5 支持当日修复；NullClaw 扩展 grok-cli provider。

**判断**：生态正在走向“模型无关、协议兼容、渠道自由”的开放架构。AI 助手不再绑定单一模型或协议，标准化接入层（OpenAI 协议兼容、MCP 工具规范）的完成度将决定项目能吸收多少外部生态红利。开发者应选择协议开放、模型适配快的项目降低锁定风险。

### 信号四：上下文管理成为成本与体验的双重瓶颈

**数据支撑**：CoPaw 用户要求支持 GPT-5.6 prompt caching 降本（13 条评论）；OpenClaw 被指强制 128k 截断无视模型配置；ZeroClaw 新增历史裁剪 token 计量 PR；PicoClaw 用户主动提交缓存 Token 统计补全（2 个 PR）。

**判断**：Token 成本透明化与精细化上下文控制已成为刚需。项目在缓存键隔离、成本统计准确性、上下文预算可配置性上的投入力度，将直接影响用户的多模型采用意愿和成本控制能力。

### 信号五：桌面端/边缘部署体验将成差异化战场

**数据支撑**：CoPaw 的 v2.1.0-beta.1 桌面端 Python 子进程崩溃（PYTHONHOME 注入）与浏览器 SDK 不可用，一周内连续出现且无 workaround，引发对 Tauri+PyInstaller 打包方案的系统性质疑；PicoClaw 的 OAuth 远程环境登录问题获合并修复；LobsterAI 投入 6 个 PR 优化 Windows 安装程序与登录流程；Hermes Agent 的桌面更新器在受管环境不可用。

**判断**：桌面端体验（安装、更新、登录、路径管理、子进程环境）是多数项目尚未完全解决的短板。在云服务同质化背景下，桌面端的稳定性和与本地文件系统的无摩擦集成，将成为开源 AI 助手维持用户粘性的关键壁垒。


## 结论与建议

**对技术决策者**：若追求最丰富的功能与最大社区生态，OpenClaw 仍是不二之选，但需为稳定性风险预留预案；若将生产安全与多租户隔离置于首位，Hermes Agent 与 IronClaw 更值得押注；若重视协议兼容与生态互操作，ZeroClaw 的方向前瞻性最强。

**对开发者贡献者**：当前生态最大的“价值洼地”在于——OpenClaw 的 389 个待合并 PR、ZeroClaw 的 48 个待合并 PR、以及各项目普遍存在的安全修复缺口。主动提交高质量的稳定性/安全类补丁，是迅速建立社区影响力的最佳路径。

**对生态观察者**：未来 3 个月的关键看点是——OpenClaw 是否能遏制质量下滑（发布 1-2 个稳定版）、IronClaw 能否完成 v1.1.0 正式发布并兑现可恢复性承诺、以及 ZeroClaw 的 Chat Completions 协议层能否落地，这三大事件将重新定义生态格局。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-05

## 1. 今日速览

项目今日活跃度较高。过去 24 小时累计处理 33 项议题/PR 更新，其中 19 项 PR 成功合并或关闭，GitHub Actions 队列运转顺畅。WebUI 视觉优化与修复类 PR 占据今日合并主力（约 42%），表明项目正处于用户体验打磨阶段。功能侧亦有重要动态：[PR #5236] 修复了 Anthropic Opus 5 的支持，直接对应今日被关闭的 [Issue #5235]——从"报告"到"修复"仅用时约 1 天，响应速度值得肯定。但当前仍存在一条**安全级别 Issue（#4784）**已悬置近 30 天未解决，涉及 API 密钥跨 Provider 泄漏，需要维护者重点关注。整体项目健康度良好，除该安全项外无其他致命隐患。

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的主要 PR 及对应的项目推进如下：

### 功能演进
- **[PR #5236] fix(anthropic): support Opus 5 effort controls** *(p1)* — 用模型家族版本阈值替代硬编码排除列表，支持 Claude Opus 5 的 adaptive thinking 与 `output_config.effort` 参数。解决了 Opus 5 因温度参数被废弃导致的所有请求被 API 拒绝的问题。直接关闭 [Issue #5235]。
- **[PR #5210] feat(webui): support trusted proxy bootstrap auth** *(p1, 已关闭)* — 为 `/webui/bootstrap` 添加基于可信上游代理（如 Cloudflare Tunnel + Access）的免令牌认证路径，适用于企业级部署场景。

### WebUI 交互与视觉打磨（今日合并 8 项相关 PR）
- **[PR #5239] feat(webui): add integrated Vite dev mode** *(p1)* — 新增 `nanobot webui --dev` 一键启动网关与 Vite dev server（含 HMR），降低贡献者前端开发门槛。
- **[PR #5244]** markdown 渲染修复：prompt rail 预览支持 Assistant 回答的 Markdown 渲染（用户消息保持纯文本）。
- **[PR #5245]** 时间戳 tooltip 样式统一：替换原生浏览器 title，改用 WebUI 共享 tooltip 组件并支持键盘可达性。
- **[PR #5243]** 自动化触发器标记从消息体移至 footer 时间戳旁，悬停可查看来源自动化名称。
- **[PR #5241]** 内联 token 高亮优化：使用更醒目的 `#ef8e30` accent 色与 semibold 字重。
- **[PR #5240]** 浮动控件样式统一重构（不改变语义）。
- **[PR #5242] fix(commands)**: 拒绝未注册的斜杠命令而非将其转发给 LLM，并对拼写错误提供最近命令建议。

### 渠道修复
- **[PR #5223] fix(wecom):** 企业微信文件名清理后为空时的回退处理（已关闭）。
- **[PR #5222] fix(telegram):** 修复代码块语言标签中特殊字符（如 `c++`、`objective-c`）导致的代码块截断问题（已关闭）。
- **[PR #5248] fix(matrix):** 为 Continuwuity 兼容性在房间加入时发送非空 POST body（待合并）。

### 整体评估
项目在 WebUI 交互规范和视觉一致性上投入了大量精力，说明该部分代码已进入稳定期的精细化打磨阶段。Anthropic Opus 5 的快速修复体现了对模型更新动态的敏锐跟踪。

---

## 4. 社区热点

今日讨论最集中的议题是：

- **[Issue #5237]** — MCP 工具返回 `isError: false` 的业务错误信封（如 `{"code": 404, "msg": "data not exist"}`）时，agent 将其视为成功调用，导致 LLM 无法知晓调用失败、一直等待直到工具超时。这是**语义层面的协议歧义**，直指 MCP 错误处理机制的核心缺陷，1 条评论表明社区对此有共鸣，但目前尚无对应修复 PR。

- **[Issue #4784]** — Provider API 密钥通过全局 `os.environ` 环境污染在 Provider 间泄漏（gateway 型用赋值、非 gateway 型用 `setdefault`），存在严重安全隐患。该 Issue 有 2 条评论（更新时间是 8 月 4 日，说明讨论还在持续），安全级别问题长期未解决，社区耐心可能正在消耗。

- **[PR #5156] fix(telegram): recover from silently stalled polling** — 修复 Telegram 轮询在代理网络闪断后静默停滞的问题（生产环境实测）。该问题在 [#5171] 中被报告，目前该 PR 仍待合并（p2），评论区反映这是真实生产痛点。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue / PR | 描述 | 状态 |
|--------|-----------|--------|------|
| 🔴 高 | [#4784] | Provider API 密钥经 `os.environ` 跨 Provider 泄漏（gateway 类型会直接覆盖其他 Provider 的密钥） | OPEN 30 天+，无修复 PR |
| 🟠 中 | [#5247] | Matrix bot 被邀请进房间时不自动加入：nio `Api.join()` 发送空 body 被 Continuwuity 拒绝（`M_BAD_JSON`） | OPEN，已有 [PR #5248] 待合并 |
| 🟠 中 | [#5235] | Anthropic Opus 5 因温度参数被弃用导致所有请求被 API 拒绝 | CLOSED — 已由 [PR #5236] 修复（当日完成） |
| 🟡 低 | [#5237] | MCP 业务错误信封（`isError: false`）被误判为成功调用，agent 持续等待直至超时 | OPEN |
| 🟡 低 | [#5223] | 企业微信下载文件名清理后为空字符，写入目标变成目录本身 | CLOSED — [PR #5223] 已合入 |
| 🟡 低 | [#5222] | Telegram 消息中代码块语言含特殊字符（`c++` 等）时被截断 | CLOSED — [PR #5222] 已合入 |

整体来看，项目对 Bug 的响应速度较快（Opus 5 当天报告当天修复），但 [#4784] 的长期悬置构成稳定性隐患。

---

## 6. 功能请求与路线图信号

### 已实现/即将实现的需求
- **Telegram 自定义 Bot API 端点**（[PR #4919] → 对应 Issue #4702）：支持自建 Bot API server 或企业网关，含 `api_base` 字段。**目前仍处于 OPEN 状态，已存在约 3 周**。
- **Mattermost 线程独立群组策略**（[PR #5233]）：在现有 Mattermost 支持上增添 `groupPolicyInThread` 配置项，区分线程与主频道的提及要求，并同步至 WebUI。
- **mst-python 元搜索集成**（[PR #5234]）：聚合 DuckDuckGo、Google、Brave、Bing 等多引擎结果，采用 RRF 融合，作为新的 Web 搜索 Provider。
- **会话工具权限模型重构**（[PR #5238]）：移除请求级 `Tool.available()` 层，让会话工具可以搜索/读取该用户所有持久化会话。**注意：这是对 #5211 引入的授权抽象的回退**，合并后将改变工具权限语义。

### 路线图信号
- 从 PR 密集度来看，**Telegram 渠道的稳定性**（轮询恢复 + 自定义端点）是当前社区最关注的方向。
- WebUI 的持续打磨（今日 8 项相关 PR）表明该项目可能正处于 1.0 稳定版发布前的 UI 收尾阶段。

---

## 7. 用户反馈摘要

- **Anthropic 用户（whisperity）**：报告 Opus 5 配置被拒时提供了详细的版本追溯（"released 2026-07-24"）和代码定位（`omit_temperature` 子串列表缺失 `"opus-5"`），属于高信息量 bug 报告。同一用户还提交了 `memory/.cursor` 与 `memory/history.jsonl` 未被 git 跟踪的问题（[#5246]），表明作为 Power User 对文件级别的细节较为敏感。
- **MCP 工具用户（Lucky314159）**：对业务错误信封的语义提出了明确预期——"LLM never learns the call failed, so it cannot re-invoke"，说明用户在真实场景中依赖 MCP 工具的容错逻辑，而当前实现与文档定义的错误处理链路存在出入。
- **Telegram 轮询停滞（来自 #5156 的生产案例）**：日志完全静默、进程存活但收不到任何消息，是"静默故障"类问题，对用户体验影响极大，用户必须手动重启才能恢复。

---

## 8. 待处理积压

维护者需关注以下长期未响应或有冲突风险的重要条目：

1. **[Issue #4784]（OPEN 30 天）Provider API 密钥跨 Provider 泄漏** — 安全级别问题，涉及全局环境污染，建议优先分配修复。
2. **[PR #4919]（OPEN 22 天）Telegram 自定义 Bot API 端点** — 社区明确需求（对应 Issue #4702），目前无冲突标记但长期未合入。
3. **[PR #1776]（存在 conflict 标记）Telegram group_mode 配置字段修复** — 该 PR 创建于 3 月 9 日，现已标记为冲突，需处理合并冲突或关闭替换。
4. **[PR #5184]（存在 conflict 标记）Quick Chat 与 Temporary Chat 功能** — 新增两个聊天模式，已打开 6 天，与近期 WebUI 变更（如 #5240/#5244）有冲突，需协调合并顺序。
5. **[Issue #5246]（whisperity 报告）memory 目录 .gitignore 规则导致内存文件意外入库** — 虽非紧急 bug，但涉及知识库文件的版本管理正确性，容易触发其他用户的 git 误操作。

---

*报告生成时间：2026-08-05 | 数据窗口：2026-08-04 00:00 UTC ~ 2026-08-05 00:00 UTC*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-05

## 今日速览

项目在过去24小时保持极高活跃度：50条Issue更新（全部处于开启状态，无关闭）与50条PR更新（46条待合并，4条已关闭/合并）。新开Issue中近半数（约12条）涉及高优先级或P2级Bug，集中在缓存污染、生命周期守卫崩溃、Feishu消息投递失败等生产环境问题；与此同时，对P0级缓存键隔离缺陷的修复PR（#78959）已提交并获积极跟进，社区贡献者响应迅速。值得关注的是，今日有两条安全依赖更新PR（#78992、#78998）聚焦于修复 `brace-expansion` 与 `undici` 的已知漏洞，前者被标记为重复。整体来看，项目处于“高活跃度、高并发贡献、快速迭代”的健康状态，但Bug积压与PR待合并数量较高，维护者审阅压力显著。

## 项目进展

今日共有 **4 个 PR 被合并或关闭**，其中值得关注的实质性变更为：

- **`feel(aux): 修复显式自定义回退端点使用主模型的问题`**（[PR #78988](https://github.com/NousResearch/hermes-agent/pull/78988)，已关闭）— 修复了 #78948 中 `resolve_provider_client()` 将主模型的模型名发往自定义回退端点的问题，消除了回退标题生成时的 404 错误。关闭时标记为重复，可能与另一条 PR 重复或并入其他修复。
- **`fix(deps): 更新 brace-expansion 与 undici 至补丁版本`**（[PR #78992](https://github.com/NousResearch/hermes-agent/pull/78992)，已关闭）— 修复 `brace-expansion` DoS 漏洞（GHSA-rgw5-rvv9-x895）以及 `undici` 的 5 个安全公告。关闭时标记为重复，可能被根覆盖更新（@skaisser 的 `fix(doctor)` PR）取代。

**关键 PR 推荐重点跟踪：**

- **`fix(cache): 按会话范围限定 prompt_cache_key，阻止跨会话缓存桶共享`**（[PR #78959](https://github.com/NousResearch/hermes-agent/pull/78959)，P0）— 修复 #78941 中 `prompt_cache_key` 仅由静态请求前缀（系统指令+工具模式）寻址、缺少会话/租户维度的问题。不同会话共享相同系统提示和工具集时（不同用户、不同项目）会发生跨会话缓存桶共享。对多租户部署至关重要，已获得 P0 标签并快速被审阅。

- **`fix(kanban): 在整个网关分派周期内强制执行 max_in_progress`**（[PR #78995](https://github.com/NousResearch/hermes-agent/pull/78995)）— 修复 #78122 中 `max_in_progress` 按板独立执行而非网关级限制的回归问题。

- **`fix(state): 验证 FTS 重建写入路径；溢出待处理容量`**（[PR #78323](https://github.com/NousResearch/hermes-agent/pull/78323)）— 修复深层 FTS 损坏时一次性重建可能错误报告成功但重试写入仍失败的问题。


## 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|-------|----------|--------|----------|
| 1 | [#64182 插件接口扩展—社区点子追踪（2026年7月）](https://github.com/NousResearch/hermes-agent/issues/64182) | 21 | 社区长期排队的 PR 作者需要一个稳定的插件接口扩展参考计划；来自 Discord 社区线程，目标是让贡献者能发布稳定的公共插件 API |
| 2 | [#34352 解决多租户 Hermes 问题](https://github.com/NousResearch/hermes-agent/issues/34352) | 14 (👍 2) | 内存操作完全绕过钩子系统导致无法实现租户隔离，不 fork 核心就无法修复；作者称已在生产环境运行数月修复 |
| 3 | [#76886 read_file 将合法 UTF-8 文本误报为二进制（0.19.1 回归）](https://github.com/NousResearch/hermes-agent/issues/76886) | 10 | `read_file` 使用 `head -c 1000` 采样时若切断了多字节字符会误判为二进制文件；影响 Obsidian 笔记等纯文本场景 |
| 4 | [#16004 max tool-call 迭代耗尽时可配置的有界自动继续](https://github.com/NousResearch/hermes-agent/issues/16004) | 9 | 在 ACP/VS Code 与长驻网关会话中，工具调用预算耗尽后代理停止自主工作，等待人工介入 |
| 5 | [#54204 允许创建后将现有会话移动到不同项目](https://github.com/NousResearch/hermes-agent/issues/54204) | 8 (👍 3) | 桌面端侧边栏需要跨项目移动会话的功能 |

**洞察**：社区讨论热度集中在 **多租户隔离（#34352）**、**插件生态建设（#64182）** 与 **工具调用可靠性（#16004、#76886）**。多租户问题已获得生产环境验证的修复方案，但迟迟未合并，是当前社区最大的诉愿之一。


## Bug 与稳定性

### 严重级别排列（按优先级）

| 级别 | Issue | 描述 | 状态 |
|------|-------|------|------|
| **P0** | [#78941 配套PR #78959](https://github.com/NousResearch/hermes-agent/pull/78959) | `prompt_cache_key` 跨会话共享缓存桶 | ✅ 已有 fix PR |
| **P1** | [#76435 网关重连循环+桌面更新器不可用](https://github.com/NousResearch/hermes-agent/issues/76435) | Discord 网关重连循环超过 1000 次导致 token 重置；桌面更新器显示 `managed outside` 错误 | ⚠️ 无对应 PR |
| **P2** | [#76886 read_file 将 UTF-8 文本误判为二进制（回归）](https://github.com/NousResearch/hermes-agent/issues/76886) | `head -c 1000` 切断多字节字符导致文本误判为二进制 | ⚠️ 无对应 PR |
| **P2** | [#78942 lifecycle_guard NUL 字节导致崩溃（不完整修复 #76762）](https://github.com/NousResearch/hermes-agent/issues/78942) | NUL 字节路径导致 `ValueError: embedded null character` 崩溃 | ✅ 已有 fix PR #78994 |
| **P2** | [#78974 lifecycle_guard 在 HOME 不可解析时崩溃](https://github.com/NousResearch/hermes-agent/issues/78974) | `RuntimeError: Could not determine home directory` 导致所有终端命令失败 | ✅ 已有 fix PR #78982 |
| **P2** | [#78975 Feishu cron 投递失败 [99992402]](https://github.com/NousResearch/hermes-agent/issues/78975) | `receive_id_type="thread_id"` 不是有效的 Feishu API 值 | ✅ 已有 fix PR #78989 |
| **P2** | [#78948 辅助客户端将主模型发送至自定义回退端点（404）](https://github.com/NousResearch/hermes-agent/issues/78948) | `resolve_provider_client()` 配对主模型+自定义端点导致 404 | ✅ 已有 fix PR #78988（已关闭，标记重复） |
| **P2** | [#78953 辅助任务行 cache_read_tokens=0，成本少报约 37%](https://github.com/NousResearch/hermes-agent/issues/78953) | 与 #71578 相同的判别器：`billing_provider` 未设置为真实 provider | ⚠️ 无对应 PR |
| **P2** | [#78862 推理模型非流式超时导致 cron 任务死亡](https://github.com/NousResearch/hermes-agent/issues/78862) | 600 秒推理下限与 600 秒 cron 不活动限制竞争，回退从不介入 | ⚠️ 无对应 PR |
| **P2** | [#78888 检查点 git add -A 因 root 拥有的 node-compile-cache 中止](https://github.com/NousResearch/hermes-agent/issues/78888) | `DEFAULT_EXCLUDES` 缺少 `node-compile-cache/` 导致受影响目录零检查点 | ⚠️ 无对应 PR |
| **P3** | [#78122 max_in_progress 按板而非网关范围执行（回归）](https://github.com/NousResearch/hermes-agent/issues/78122) | 网关为每个板独立调用 `dispatch_once()`，各板独立计数 | ✅ 已有 fix PR #78995 |
| **P3** | [#78514 多路模式 Feishu 事件去重按 profile 独立导致重放事件被处理两次](https://github.com/NousResearch/hermes-agent/issues/78514) | 每个 profile 独立的去重缓存导致重放事件重复处理 | ⚠️ 无对应 PR |
| **P3** | [#75801 OpenCode Go 流式响应无 finish_reason 导致 4 次虚假重连](https://github.com/NousResearch/hermes-agent/issues/75801) | SSE 正常结束但无 `finish_reason` 被误判为中断；桌面端剥离流式回答 | ⚠️ 无对应 PR |
| **P3** | [#78847 桌面端文件夹附件路径被消息内容覆盖](https://github.com/NousResearch/hermes-agent/issues/78847) | 发送文件夹附件+消息时，消息内容覆盖已发送的文件夹路径 | ⚠️ 无对应 PR |
| **P3** | [#78946 桌面状态栏上下文使用量指示器在 0.20.0 缺失](https://github.com/NousResearch/hermes-agent/issues/78946) | `context_max` 未在 0.20.0 网关 + 0.17.0 桌面 UI 组合上浮出 | ⚠️ 无对应 PR |

### 稳定性趋势判断

今日集中出现了多个围绕 **lifecycle_guard** 的崩溃类问题（#78942、#78974），表明 #76762 的安全修复覆盖仍不完整，是一个持续性安全隐患区域。同时 **#78953 成本少报 37%** 的问题直接影响用户计费透明度，需要尽快关注。整体上，社区贡献者修复速度快（#78942 和 #78974 均在 24 小时内获得对应修复 PR），项目修复响应机制运转良好。


## 功能请求与路线图信号

### 高潜力候选功能（已有 PR 支持）

| 功能 | Issue | 对应 PR | 复杂度/影响 |
|------|-------|---------|------------|
| 工具间通过引用消费先前的工具输出 | [#78061](https://github.com/NousResearch/hermes-agent/pull/78090) | [PR #78090](https://github.com/NousResearch/hermes-agent/pull/78090) | P3，有界保留、提示词紧凑提示，能显著增强工具链能力；社区长期诉求 |
| `hermes://chat/new` 深链接支持工作区会话 | — | [PR #70568](https://github.com/NousResearch/hermes-agent/pull/70568) | P3，外部应用可打开指定工作区聊天，提升桌面端可集成性 |
| 机器人商店信任指数（x402 结算真相） | — | [PR #64303](https://github.com/NousResearch/hermes-agent/pull/64303) | P3，加入 FastMCP 的付费承诺完整性验证/入门/免费试用能力 |
| 看板 `amend` 命令：编辑任务标题/正文 | [PR #61702](https://github.com/NousResearch/hermes-agent/pull/61702) | 同左 | P3，补齐看板 CLI 编辑能力 |
| 编码安全 lint（针对 Windows 的检查） | [#66668](https://github.com/NousResearch/hermes-agent/issues/66668) | 暂无 | 已搁置，等待合并触发条件 |
| 配置可续的有界自动继续（工具预算耗尽后） | [#16004](https://github.com/NousResearch/hermes-agent/issues/16004) | 暂无 | P2，提升长时运行场景可用性 |
| 可信发送者 UID 信封，用于共享网关会话 | [#69961](https://github.com/NousResearch/hermes-agent/issues/69961) | 暂无 | P3，跨平台共享会话的身份认证，涉及 Discord/Telegram 等 |
| 桌面端可配置的快捷入口默认“发送到”目标 | [#78250](https://github.com/NousResearch/hermes-agent/issues/78250) | 暂无 | P3，简单 UX 改进 |

### 版本发布候选判断

当前待合并 PR 中，**#78959（P0 缓存隔离）** 和 **#78995（kanban 网关级限制）** 属于缺陷修复且优先级高，很可能进入下一个 patch 版本。**#70568 深链接** 与 **#78090 工具结果引用** 属于功能增强，可能需要进入次版本。

### 值得关注的路线图信号

- **多租户/会话隔离** 持续成为社区焦点（#34352、#78959），两项都涉及内存或缓存绕过核心分离机制
- **Telegram 特性对齐运动**（[#78791](https://github.com/NousResearch/hermes-agent/issues/78791)）被标记为 meta-issue，将所有 Telegram 子问题互锁，释放出对平台一致性补齐的信号
- **工具链自我消费（tool result reference）** 方向获得 PR 支撑，如果合并，将显著提升复杂工作流中工具的协同能力


## 用户反馈摘要

**正面反馈：**
- 技术用户对插件的热情持续高涨，Discord 社区线程 (2026-07-04) 产出了 21 条评论的插件接口扩展追踪（#64182），并已有贡献者基于该讨论提交了 MCP 目录 PR（#64303）
- 用户可以快速反馈回归问题（#76886 在更新后当天即报告），说明升级渠道畅通、反馈链路短

**痛点与不满：**

1. **多租户隔离缺失严重影响生产部署**（#34352）— “Memory operations bypass the hook system entirely, making tenant isolation impossible without forking core” — 用户已自行修复并运行数月，但上游迟迟未跟进
2. **检查点功能在生产中失效**（#78888）— 因 root 拥有的缓存目录导致 `git add -A` 中止，受影响目录零检查点，数据安全风险高
3. **桌面端更新器在受管环境下不可用**（#76435）— 显示 “managed outside...” 错误，更新路径断裂
4. **工具误判为二进制文件**（#76886）— 回归问题导致日常笔记文件无法打开，影响核心使用场景
5. **自定义视觉提供商集成困难**（#44349、#76602）— `custom:` 前缀解析与 `base_url` 配置存在两个独立的 401 鉴权问题，配置体验不佳
6. **成本核算与提供商实际账单偏差约 37%**（#78953）— 用户反馈本地成本显示与提供商计费差距大，影响对模型成本的控制能力

**使用场景亮点：**
- Obsidian 笔记 + `read_file` 工具（#76886）
- Windows 11 上安全敏感本地部署的便携/隔离模式需求（#46199）
- VS Code/ACP 中长时运行自主工作的自动继续机制（#16004）
- 将卡片视图集成到 Feishu DM 线程中自动投递 cron 任务结果（#78975）


## 待处理积压

| 类型 | Issue/PR | 时长 | 备注 |
|------|----------|------|------|
| **功能长期未响应** | [#478 学习卡片技能（Study Deck Skill）](https://github.com/NousResearch/hermes-agent/issues/478) | 5 个月（2026-03-06 创建，👍 4） | 功能需求生命周期长，有实际用户价值但一直无维护者回复 |
| **生产级修复待合并** | [#34352 多租户问题修复方案](https://github.com/NousResearch/hermes-agent/issues/34352) | 2.5 个月（👍 2），作者称已生产验证 | 缺 `needs-decision` 标签，等待维护者决策 |
| **PR 长期未审阅** | [#47583 feat(safety): 拒绝读取含密钥的凭据文件](https://github.com/NousResearch/hermes-agent/pull/47583) | 7 月 17 日创建至今，标注 `sweeper:risk-platform-windows` 与 `sweeper:blast-moderate` | 安全增强型 PR，涉及 Windows 平台风险，长时间未获处理 |
| **PR 持续跟进中** | [#67934 使用原生 Ollama 标签进行本地模型发现](https://github.com/NousResearch/hermes-agent/pull/67934) | 7 月 20 日创建，作者已多次 rebase | 标记 duplicate，但作者持续跟进 |
| **文档矛盾** | [#78254 快速开始称 Nous Portal“免费”，Portal 页面却显示需要订阅](https://github.com/NousResearch/hermes-agent/issues/78254) | 创建 2 天 | 低优先级但直接影响新用户体验，容易被忽略 |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期**: 2026-08-05  
**数据窗口**: 2026-08-04（过去24小时）

---

## 1. 今日速览

PicoClaw 项目在过去24小时内保持中等活跃度：共产生3条 Issue 更新和4条 PR 更新，无新版本发布。值得关注的是，社区提交的2个新 PR（#3299 Exa 搜索集成、#3317 提示缓存日志增强）正处于待审查阶段，显示外部贡献者的参与意愿在提升。同时，两个持续困扰用户的问题——MCP 连接失败导致的 Agent 循环挂起（#3269）和 Web UI 聊天延迟（#3281）——仍在开放中，且均获得了社区关注（各1个 👍），是项目当前稳定性的主要隐患。值得注意的是，今日有2个 PR（#3280、#3251）和1个 Issue（#3182）被打上 `stale` 标签并关闭，说明维护者正在清理长期未活跃的积压项，项目治理有正向信号。总体而言，项目活跃度健康，功能开发与 Bug 修复并行推进，但核心稳定性问题需要维护者优先关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

过去24小时有2个 PR 被合并/关闭，虽均标记为 `stale`，但合并内容具有实际价值：

| PR | 内容 | 影响 |
|---|---|---|
| [#3251](https://github.com/sipeed/picoclaw/pull/3251) | **修复 Anthropic 提示缓存 Token 使用量统计** — 在 `pkg/providers/anthropic/provider.go` 和 `pkg/providers/anthropic_messages/provider.go` 中捕获被丢弃的缓存相关 Token 指标 | ✅ 已合并。此修复使运营者能够检查提示缓存是否生效，对控制 Anthropic API 成本具有直接帮助。 |
| [#3280](https://github.com/sipeed/picoclaw/pull/3280) | **修复浏览器 OAuth 登录在真实环境下的回调问题** — 解决了 headless/远程环境下认证码被烧毁、流程需完全重启的四个独立根因 | ✅ 已合并。对远程部署场景的用户体验有显著改善。 |

**综合评估**：这两个 PR 分别填补了可观测性（缓存用量统计）和可用性（OAuth 登录）方面的空白，虽为存量修复，但项目基础设施在稳步完善。值得注意的是，新提交的2个开放 PR（#3299、#3317）正处于早期审查阶段，尚未被标记为 `stale`，结合其功能性（新增搜索 Provider、调试输出增强），如果审查顺利，下一版本可能包含这些变更。

---

## 4. 社区热点

今日活跃讨论集中在两个开放 Bug Issue 上，均为3条评论、各获1个 👍：

**[#3281 Web UI 聊天输入延迟（历史消息较长时）](https://github.com/sipeed/picoclaw/issues/3281)** — `[BUG]`  
- 作者报告：当单个会话历史消息变长后，输入框出现明显卡顿，影响正常使用。
- 环境：PicoClaw 0.3.1、Go 1.25.11、Web 端。
- **诉求分析**：这属于典型的**前端渲染性能问题**（可能是 DOM 节点过多或状态更新未优化）。评论区的讨论主要集中在复现路径和性能瓶颈推测上。该 Issue 自7月21日创建以来已两周，尚未有 fix PR 关联，社区对该问题的关注度正在累积。

**[#3269 MCP 服务器连接失败导致 Agent 循环挂起](https://github.com/sipeed/picoclaw/issues/3269)** — `[BUG]`  
- 作者报告：MCP 连接失败时，Agent 循环挂起，整个聊天界面停止响应用户。
- 环境：nightly 构建版本、Qwen3 模型。
- **诉求分析**：这属于**可靠性/容错性缺陷**，直接影响生产环境使用。MCP 服务不可达是常见运维场景，当前行为导致整个对话服务不可用，严重程度较高。评论中大概率包含日志分析和超时机制讨论。

**综合判断**：社区当前最关心的两大议题是 `Web UI 性能` 和 `MCP 容错性`，两者都直接影响日常使用体验，维护者应优先响应。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP 连接失败 → Agent 循环挂起 → 聊天界面完全停止响应 | **开放**，无关联 fix PR。此问题影响所有使用远程 MCP 服务器的用户，为稳定性最高优先级。 |
| 🟠 中 | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | Web UI 输入框在长历史会话中出现严重延迟 | **开放**，无关联 fix PR。属性能回归或前端累积问题。 |
| ⚪ 低（已关闭） | [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Android 版本无法启动服务、无法修改路径 | 已关闭（`stale`）。因长期无活跃讨论被自动关闭，如仍有人遇到此问题建议重新开启或提交新 Issue。 |

**风险评估**：当前存在2个未修复的功能性 Bug，其中 #3269 属于阻断性问题。项目健康度受到一定影响，建议维护者本周内给出 #3269 的响应（至少确认复现或给出临时规避方案）。

---

## 6. 功能请求与路线图信号

当前有2个开放 PR 展示了明确的功能扩展方向：

- **[#3299 添加 Exa 原生 Web 搜索 Provider](https://github.com/sipeed/picoclaw/pull/3299)（由 kesku 提交）** — 新增 `tools.web` / `web_search` 中 Exa 作为原生 Provider，支持 `d/w/m/y` 时间过滤。该 PR 自7月26日创建，今日仍在待审查中。**若合并**，PicoClaw 将新增一个高质量的搜索后端选项，这符合扩展工具生态的项目定位。

- **[#3317 在 LLM 响应调试输出中记录提示缓存 Token](https://github.com/sipeed/picoclaw/pull/3317)（由 vmuliadi-astro 提交，今日新开）** — 在 Gateway 的 `LLM response` 调试行中补充缓存 Token 信息，兼容 DeepSeek（经 Cloudflare AI Gateway）等 Provider 的缓存元数据。**若合并**，将与已合并的 #3251 形成互补，进一步完善可观测性体系。

**路线图信号分析**：近期提交的 PR 集中在下游 Provider 兼容性和可观测性增强两个方向，反映出实际用户对成本管控和调试能力的需求在上升。目前无大型架构层面的路线图信号。

---

## 7. 用户反馈摘要

从今日活跃的 Issues 评论中提炼的用户痛点：

| 痛点 | 来源 | 场景分析 |
|---|---|---|
| **MCP 故障导致整体不可用** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | 用户部署了多个 MCP 服务器（可能包括本地与远程），当某一个连接失败时，整个 Agent 循环卡死，所有对话被迫中断。用户期望的合理行为是：单个 MCP 故障应可跳过或降级，不影响核心聊天功能。 |
| **Web UI 在长会话下交互迟滞** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | 用户习惯在同一会话中持续对话（而非频繁新建会话），随历史累积，输入出现肉眼可见的延迟，直接降低使用流畅度。 |
| **OAuth 登录在远程/无头环境不可用** | [#3280](https://github.com/sipeed/picoclaw/pull/3280) 的 Problem 描述 | 该 PR 已解决此问题，但侧面反映出不少用户在 headless 服务器/远程开发机上运行 PicoClaw，对完善的认证流程有硬性需求。 |
| **成本可见性不足** | [#3251](https://github.com/sipeed/picoclaw/pull/3251)、[#3317](https://github.com/sipeed/picoclaw/pull/3317) | 多位用户主动提交 PR 完善缓存 Token 统计，说明运营者希望精确掌握 API 成本构成，当前日志信息不够透明。 |

**总体满意度**：功能性问题（Bug）和体验问题（性能）是当前不满的主要来源，而社区通过提交高质量 PR 来弥补缺陷的正向行为值得肯定。

---

## 8. 待处理积压

以下 Issue/PR 长期未获维护者响应，建议关注：

**⚠️ 高优先级积压**

- **[#3269 MCP 连接失败导致挂起](https://github.com/sipeed/picoclaw/issues/3269)** — 自7月20日创建，16天无维护者回应。属于高严重性 Bug，沉默时间越长，用户信任损失越大。
- **[#3281 Web UI 长时间历史卡顿](https://github.com/sipeed/picoclaw/issues/3281)** — 自7月21日创建，15天无官方回应。建议至少确认问题并给出临时缓解建议。

**🔄 待审查 PR**

- **[#3299 Exa Web 搜索 Provider](https://github.com/sipeed/picoclaw/pull/3299)** — 已开放10天，处于待审查状态。功能完整、有测试且来自社区高质量贡献，建议维护者安排 review，避免进入 `stale` 状态。
- **[#3317 调试输出补充缓存 Token](https://github.com/sipeed/picoclaw/pull/3317)** — 新提交，需要尽快安排初轮审查。

**📋 已关闭的遗留问题（可追溯）**

- **[#3182 Android 版本无法启动服务](https://github.com/sipeed/picoclaw/issues/3182)** — 因 stale 自动关闭，但 Android 移动端适配可能是潜在需求方向，如在路线图中无相关规划，建议在 Release Notes 中明确说明。

---

*本日报由 AI 自动生成，数据来源于 GitHub 公开仓库 `sipeed/picoclaw` 的 Issues 与 Pull Requests 元数据。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期**: 2026-08-05  
**数据窗口**: 2026-08-04 至 2026-08-05  
**数据来源**: [github.com/qwibitai/nanoclaw](https://github.com/qwibitai/nanoclaw)

---

## 1. 今日速览

过去24小时 NanoClaw 项目处于**中低活跃度**状态。虽然 Issues 侧无任何新开或关闭记录，但 PR 侧有 5 条更新，其中一条核心团队 PR (#3154) 已关闭（合并），其余 4 条处于待合并状态。值得关注的是，两条与“Dial 渠道集成”相关的功能 PR（#3041、#3050）在创建三周后于昨日获得更新，表明维护者正在推进该特性的合入准备工作。此外，一条 Discord 审批按钮修复 PR（#3185）和一条技能架构重构 PR（#3186）于昨日新开，项目在渠道适配和代码架构层面均有持续投入。整体来看，项目处于**功能开发与整合期**，暂无版本发布和新的用户反馈涌入。

---

## 2. 版本发布

**无**。过去24小时内无新版本发布。

---

## 3. 项目进展

今日有 1 条核心 PR 被合并（关闭），另有 4 条待合并：

### 🔒 已合并

| PR | 标题 | 合并方向 |
|---|---|---|
| [#3154](https://github.com/nanocoai/nanoclaw/pull/3154) | fix(agent-runner): give scheduled tasks current run time | 修复 |

**关键推进**：该 PR 解决了定时任务在执行时获取的是“创建时间”而非“实际运行时间”的问题。修复后，任务在执行时将以 `process_after`（有效调度时间）渲染 `time` 字段，同时为遗留数据保留创建时间作为回退。此外，新增了 `current_time`（含星期几），由 agent-group 的时区配置生成。**该修复对依赖定时任务时间精确性的自动化场景（如定时报告、周期性操作）有直接帮助。**

### ⏳ 待合并

| PR | 标题 | 状态 |
|---|---|---|
| [#3185](https://github.com/nanocoai/nanoclaw/pull/3185) | fix(discord): strip `\n` delimiter in webhook interaction custom_id | 待合并（新开） |
| [#3186](https://github.com/nanocoai/nanoclaw/pull/3186) | refactor: add host seams for skill-owned capabilities | 待合并（新开） |
| [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) | feat(channels): add Dial channel adapter (SMS + AI voice calls) | 待合并（昨日更新） |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | feat(setup): add Dial to the channel picker + wizard/skills | 待合并（昨日更新） |

**整体判断**：两条 Dial 渠道 PR 的昨日更新暗示维护者正在积极审阅或要求修改，若合并通过，NanoClaw 将新增 SMS + AI 语音通话渠道，是项目渠道矩阵的一个重要扩展。Discord 修复 PR 与 #3154 同属稳定性修复方向，项目近期在“正确性”上投入明显。

---

## 4. 社区热点

今日无 Issues 活动，PR 侧评论量均为 0（无讨论热度）。但以下 PR 值得关注其背后的诉求：

- [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) + [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)（Dial 渠道）：这两条 PR 由同一作者（OmriBenShoham）在 7 月 14 日创建，昨日同时获得更新，说明维护者正在推进合入。**背后的用户诉求**：扩展 NanoClaw 的渠道覆盖到电话/SMS 场景，使 AI 助手能通过语音和短信与用户交互。

- [PR #3186](https://github.com/nanocoai/nanoclaw/pull/3186)（host seams 重构）：标题标记为 `refactor, follows-guidelines`，摘要模板表明作者遵循了项目贡献指南。**诉求**：为“技能拥有的能力”（skill-owned capabilities）添加宿主隔离层，可能是为后续多宿主部署或沙箱能力打基础。

---

## 5. Bug 与稳定性

今日报告 1 个新 Bug 修复 PR，另有 1 个已合入的稳定性修复：

| 严重度 | 问题 | 状态 | 修复 PR |
|---|---|---|---|
| **高** | Discord 上审批卡片所有按钮点击均被解析为“拒绝”——用户在 `ask_question`/审批卡片上点击“批准”时，实际操作被错误地当作拒绝。根因是 webhook 交互路径解码 `custom_id` 时未处理 `\n` 分隔符 | ✅ 已有修复 PR [#3185](https://github.com/nanocoai/nanoclaw/pull/3185) | 待合并 |
| **中** | 定时任务执行时获取的是任务创建时间而非实际运行时间 | ✅ 已合入修复 [#3154](https://github.com/nanocoai/nanoclaw/pull/3154) | 已关闭 |

**分析**：Discord 审批 Bug 直接影响用户操作结果（批准变拒绝），属于高影响问题，建议维护者优先合并 #3185。定时任务时间问题已修复，无进一步行动项。

---

## 6. 功能请求与路线图信号

今日无新 Issues，无直接的功能请求。但结合 PR 动态，可识别以下路线图信号：

| 信号 | 来源 | 可能纳入版本 |
|---|---|---|
| **Dial 渠道（SMS + AI 语音通话）** | PR #3041 + #3050 同时更新，表明维护者在推进 | 下一版本（可能性较高） |
| **技能宿主隔离能力** | PR #3186 提出 `host seams` 概念 | 未来架构演进方向（中期） |

**判断**：Dial 渠道若合并，将是 NanoClaw 从纯文本渠道向语音/短信渠道延伸的重要一步。`host seams` 重构则表明项目在为更灵活的部署形态（多宿主、边缘部署）做准备。

---

## 7. 用户反馈摘要

今日无 Issues 评论和讨论，无法提取新的用户反馈。基于现有 PR 内容，可提炼以下间接信号：

- **Discord 审批流程不可用**（来自 #3185）：用户在实际使用中遇到“每次点击批准都被拒绝”的问题，说明审批/确认流程在 Discord 上的可靠性是用户的真实痛点，且该问题直接影响工作流效率。
- **定时任务的准确性需求**（来自 #3154）：用户依赖定时任务执行周期操作，时间偏差会导致结果错误。修复后任务将基于实际调度时间渲染，改善了自动化场景的可靠性。

---

## 8. 待处理积压

以下 PR 已存在较长时间且尚未合并，建议维护者关注：

| 项目 | 创建时间 | 已等待 | 说明 |
|---|---|---|---|
| [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) Dial channel adapter | 2026-07-14 | 22 天 | 功能完整（SMS + AI 语音），昨日有更新，预计在审阅后期 |
| [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) Dial channel picker + wizard | 2026-07-14 | 22 天 | 与 #3041 配套，需同步合入 |
| [PR #3186](https://github.com/nanocoai/nanoclaw/pull/3186) host seams 重构 | 2026-08-04 | 1 天 | 新开，建议尽早分配 reviewer |
| [PR #3185](https://github.com/nanocoai/nanoclaw/pull/3185) Discord 审批修复 | 2026-08-04 | 1 天 | 高影响 Bug，建议优先评审 |

> **维护者提醒**：Discord 审批 Bug（#3185）涉及用户操作结果错误，建议优先合入；Dial 渠道两条 PR 已等待三周，建议明确合并或关闭的结论，避免长期悬挂。

---

## 项目健康度评估

| 维度 | 状态 | 说明 |
|---|---|---|
| **Issue 响应** | 🟡 稳定 | 24h 内无新 Issue，无积压恶化 |
| **PR 流转** | 🟢 健康 | 有合入、有新开、有更新，流转正常 |
| **Bug 修复** | 🟢 积极 | 2 个稳定性修复在 24h 内处于活跃状态 |
| **功能推进** | 🟢 有进展 | Dial 渠道整合信号明确 |
| **社区活跃** | 🟡 平静 | 无 Issue 讨论，无 PR 评论，但开发侧活跃 |

**总结**：NanoClaw 项目当前处于稳定的功能开发期，核心维护团队在渠道扩展和稳定性修复上双线推进。建议关注未来 48-72 小时内 Dial 渠道 PR 是否合入，以及 Discord 修复的评审进度。

---
*本日报由 AI 分析师自动生成，数据截至 2026-08-05。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-05

## 1. 今日速览

NullClaw 项目在过去24小时内整体活跃度处于**低水平**，但有一条值得关注的 PR 正处于待合并状态。具体来看：Issues 方面**零更新**，既无新开亦无关闭；PR 方面仅 1 条更新（#981），且该 PR 自 7 月 29 日创建以来已搁置一周仍未获得合并，暗示维护者响应周期偏长。无新版本发布。综合来看，项目当前处于**安静的稳定期**，核心贡献者可能正集中精力处理 #981 的评审工作。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日无 PR 被合并或关闭，主要进展集中在一条**待合并**的 PR：

- **[#981 [OPEN] feat(provider): add grok-cli provider for xAI Grok CLI](https://github.com/nullclaw/nullclaw/pull/981)** — 作者: valonmulolli | 更新: 2026-08-04
  - **摘要**: 新增基于 CLI 的 provider，将请求委托给本地 `grok`（xAI Grok）命令行工具，复用现有 `codex-cli` / `gemini-cli` / `claude-cli` provider 的 spawn-per-request 模式。该 provider 为**可选**，依赖 `grok` CLI 安装与认证。
  - **项目意义**: 若合并，NullClaw 将新增 xAI 阵营的模型接入能力，意味着继 OpenAI、Google、Anthropic 之后，项目正式拓展至 xAI 生态。这是继已有三家 CLI provider 后的一次**横向生态扩展**，将直接扩大项目的模型覆盖面与用户群。
  - **当前状态**: 创建已 7 天，最后一次更新为昨天（8月4日），但尚未获得合并。关注维护者是否会在近期放行。

## 4. 社区热点

今日社区讨论极为平静，无活跃讨论的 Issue 或 PR。唯一存在讨论量的 #981 评论数仍未披露（显示为 undefined），但鉴于其创建至今已一周，若评论区有技术细节讨论，建议维护者优先回应。**诉求分析**: 该 PR 的核心诉求是**拥抱多元模型生态**，在已有三家 CLI provider 基础上补齐 xAI 空缺，侧面反映社区对"多模型自由切换"的持续期待。

## 5. Bug 与稳定性

今日无 Bug 报告、崩溃或回归问题。

## 6. 功能请求与路线图信号

今日无新功能请求提出。从 #981 看，**多 provider 生态扩展**是当前清晰的主线信号——继 codex、gemini、claude 之后，grok 的加入将形成四足鼎立之势。结合项目历史，以下方向可能被纳入后续版本：

- 更多 CLI/API provider 接入（如本地模型 llama.cpp、Ollama 等）
- provider 动态发现与热插拔机制（当 provider 数量增多后，管理体验将成为痛点）
- 统一的多 provider 基准测试 / 质量对比工具

## 7. 用户反馈摘要

今日无新 Issues 产生，暂无直接用户反馈可提炼。基于 #981 的提交动机，可间接反映部分用户的**实际使用场景**：他们可能已在本地使用 `grok` CLI 工具，希望 NullClaw 能作为统一入口聚合多种 AI 后端，而非锁定单一供应商。若该 PR 合并，预计会吸引 xAI 生态的开发者关注本项目。

## 8. 待处理积压

以下为值得维护者关注的长期未决事项：

- **[#981 feat(provider): add grok-cli provider for xAI Grok CLI](https://github.com/nullclaw/nullclaw/pull/981)** — 自 2026-07-29 创建，已 **7 天**未合并。该 PR 代码量适中、模式成熟（复用既有 CLI provider 架构），合并风险应较低。**建议**: 维护者若能安排一次 review 并给出明确结论（合并/需修改），将显著提升外部贡献者的参与信心。若因设计决策需延后，建议在评论区留言说明规划，避免贡献者长期悬置。

---

*报告生成时间: 2026-08-05 | 数据覆盖: 过去 24 小时 | 项目健康度评估: 🟢 稳定（维持现状，待 PR 激活）*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-05

## 1. 今日速览

过去 24 小时项目活跃度极高，共产生 50 条 Issue 更新和 50 条 PR 更新，其中新开/活跃 Issue 38 条、待合并 PR 32 条，整体处于大版本迭代（v1.1.0-rc.1）密集攻坚期。今日工作高度集中于三大主线：**Re 架构工作流（WS0-10）的批量落地与收尾**、**v1.1.0-rc.1 发布前 Windows 平台阻塞缺陷修复**（#7197、#7200 已合并，第四个阻塞 #7200 当日关闭），以及**可恢复性契约（error-recoverability endgame，#6284）的最终达成与关闭**。值得关注的是，大量 "doc-truth audit" 发现的问题（#7144-#7147、#7151）表明架构治理类 issue 形成批量产出、集中提交（如 #7156、#7161、#7159 单日合并），同时外部贡献者（theredspoon、Kampouse、thisisjoshford）持续贡献，项目健康度整体向好。CI 配置昨日出现一次回归（#7119 已快速关闭）。无新版本发布。

---

## 2. 版本发布

过去 24 小时无新版本发布。当前版本线停留在 `ironclaw-v1.1.0-rc.1`（`ae1dc1178ace23a345e941dd17eb0e93...`），项目组正密集修复该 RC 的 Windows 平台阻塞缺陷（已修复 2/4）：#7197（Windows 身份变量传递）、#7200（Windows `icacls` 污染 stdout），另有 2 个 Windows 阻塞问题待定位。

**⚠️ 发布风险预警**：#7178 明确指出 **`1.0.0-rc.1` → `1.1.0-rc.1` 的启动迁移尚非无损**，且 #7198（对应 PR，XL 级，核心成员提交）已完成修复代码的 PR 提交，正在等待合并验证。

---

## 3. 项目进展

### 架构重构（Reborn Restructure）
WS0-10 批量推进，核心目标为拆除 god crate、落实目标架构 #3773。当日新增多篇 doc-truth audit 报告（#7144-#7147），并迅速转化为实施 PR 合并：

| PR | 内容 | 规模（LOC） | 状态 |
|---|---|---|---|
| [#7156](https://github.com/nearai/ironclaw/pull/7156) | 四项 enforcement 缺陷修复：同层边清单、composition 绝对 LOC 上限、D-E vendor 普查、ratchet slack（含 sabotage testing） | 未知 | ✅ 已关闭 |
| [#7161](https://github.com/nearai/ironclaw/pull/7161) | WS10：loud 路径键控门禁转换为 inventory 键控 | XL | ✅ 已关闭 |
| [#7159](https://github.com/nearai/ironclaw/pull/7159) | WS5：通过端口反转切断 `conversations -> turns` 依赖（寄存器 4→3） | XL | ✅ 已关闭 |
| [#7160](https://github.com/nearai/ironclaw/pull/7160) | WS3：mcp 与 sandbox 切至窄 reserve/reconcile/release 端口 | XL | ✅ 已关闭 |

新开关键 Issue：#7145（extension_host → loops 重分层）、#7151（composition 门槛被分母稀释的治理漏洞）。

### v1.1.0 发布阻断修复
- #7200（当日关闭）：修复 Windows `icacls` 写入污染 CLI stdout 的问题——**v1.1.0-rc.1 的第四个 Windows 阻塞缺陷，比此前任何一次 run 走得更远。**

### 核心功能与文档
- PR #7167（已关闭）：修复 bin-only crate 的 per-package clippy 硬错误（`--lib` 标志问题），保证 CI 不误报。
- 新增 Nostr 宿主函数（PR #7184，OPEN）：为 WASM 工具沙箱整合 BIP-340 Schnorr 签名能力。
- 积压的 IronHub 文档（PR #6965，OPEN）与 IronHub 集成（#6731）推进中。

---

## 4. 社区热点

### 最热 Issue：#6284 — 可恢复性契约终局
[Issue #6284](https://github.com/nearai/ironclaw/issues/6284) 获 15 条评论，为铁杆 epic。提出理想化的错误恢复契约（运行必须存活、模型必须看到错误、看到的内容必须包含原因与成功条件、模型必须获得行动回合、不得上报非成功状态），已于 8 月 4 日关闭——**暗示该契约达成 100% 错误恢复率目标已实现或至少被认为达成。**

### 评论量 3-4 条的热门议题：
1.  [#6524](https://github.com/nearai/ironclaw/issues/6524)（已关闭）：Hermetic 能力与关键用户旅程测试平台——解决"每个支持的能力是否都有确定性覆盖"这一机械问题。
2.  [#7119](https://github.com/nearai/ironclaw/issues/7119)（已关闭）：clippy 因 package-set 而异导致 main 变红——快速定位并处理。
3.  [#6752](https://github.com/nearai/ironclaw/issues/6752)（OPEN）：实例删除失败后重登录卡在"Loading your agents..."——疑似后端 bug。
4.  [#7145](https://github.com/nearai/ironclaw/issues/7145)（OPEN）：架构工作流下一阶段的技术路线讨论。
5.  [#7194](https://github.com/nearai/ironclaw/issues/7194)、[#7193](https://github.com/nearai/ironclaw/issues/7193)、[#7192](https://github.com/nearai/ironclaw/issues/7192)、[#7191](https://github.com/nearai/ironclaw/issues/7191) 四个由 ilblackdragon 提交，覆盖 outbound 投递目标、自动化手动触发、WebUI 消息乱序、`builtin.time` 相对偏移计算缺失四大产品/工具议题，每个皆标有 size 与 risk。

---

## 5. Bug 与稳定性

按严重程度排序如下：

### 发布阻塞（RC 阻断）
| Issue | 描述 | Fix PR | 状态 |
|---|---|---|---|
| #7200（Windows） | `icacls` 写入 CLI stdout，导致 Windows 端 v1.1.0-rc.1 冒烟失败 | 已合并 | ✅ 已解决 |
| #7197 | Windows 身份变量未传给 release smoke（已修复，范围已收敛） | 已合并 | ✅ 已解决 |
| 另 2 个 Windows 缺陷 | 尚未定位/提报 | 无公开 PR | ❌ 待处理 |
| [#7178](https://github.com/nearai/ironclaw/issues/7178)（迁移） | 1.0.0-rc.1 → 1.1.0-rc.1 启动迁移非无损（会丢线程/消息等） | [#7198](https://github.com/nearai/ironclaw/pull/7198) OPEN | ⏳ 待合并 |

### 功能正确性 / 回归
| Issue | 问题描述 | 严重程度 | Fix PR |
|---|---|---|---|
| [#7185](https://github.com/nearai/ironclaw/issues/7185) | 跨会话记忆不可靠（多个测试者报告） | 高（影响核心价值主张） | 无 |
| [#7180](https://github.com/nearai/ironclaw/issues/7180) | Web 抓取随机失败，agent 倾向用 http 工具而非 web_search | 中 | 无 |
| [#7168](https://github.com/nearai/ironclaw/issues/7168) | agent 安装的 skill 不可见：写入路径与发现路径不一致 | 中（影响扩展性） | 无（已关闭状态？） |
| [#7192](https://github.com/nearai/ironclaw/issues/7192) | WebUI 乐观消息渲染在 agent 输出下方 | 低-中（UX） | 无 |
| [#7115](https://github.com/nearai/ironclaw/issues/7115) | Docker entrypoint 用已废除的环境变量判断迁移，文档不可执行 | 中 | 无 |
| [#7119](https://github.com/nearai/ironclaw/issues/7119) | 代码风格 clippy 与 package-set 相关变红 | 低（CI-only） | ✅ #7167 |

### 性能与可观测性缺陷
| Issue | 问题描述 | 影响 |
|---|---|---|
| [#7103](https://github.com/nearai/ironclaw/issues/7103) | Latency-trace 字段在关闭时仍计算（字节数开销） | 每次工具调用均受影响 |
| [#7146](https://github.com/nearai/ironclaw/issues/7146) | **121 处** `target = "…"` 误用为字段而非元数据目标——事件对过滤器不可见 | 高：日志/监控失真 |
| [#7104](https://github.com/nearai/ironclaw/issues/7104) | Extractors 将"无文本"报告为 Failed（非 Empty），误导模型 | 中：模型被判错方向 |

---

## 6. 功能请求与路线图信号

### 高优先级（Label: P1 / epic）
- **#7193**: Automation run-now（手动触发）缺失——模型、WebUI、产品面均不可用，管理面只有 list/pause/resume/rename/delete。对应 PR：#7193 已提出完整实施方案（触发域 + 产品面 + capability + WebUI），示意 P2，L 级、风险中。
- **#7194**: 管理员允许的共享 channel 应可作为 outbound 投递目标——Slack `send_message` 可枚举 channel 但无法作为最终回复路由目标，属宿主投递层能力空缺。
- **#6565 / #6941**: Skill 自发现、路由与激活（#6941 为 #6565 的可执行子集）。Issue #6565 描述诊断已更新，仍在开放中。可参考外部建议 #7199（见下方）作为配套数据支撑。

### 强劲信号
- **IronHub 集成**（#6731，epic）：将工具/技能从编译期列表变为运行时市场，支持签名与来源校验——已有 PR #6965（文档三页）。

---

## 7. 用户反馈摘要

### 跨会话记忆（#7185）——高满意度减分项
> 多位测试者独立观察到某一会话确立的上下文在后续会话中无法可靠召回。法务领域试用者（经 Tobias 转述）认为 agent 无法访问信息。

需求：需要跨会话持续记忆或显式的可管理会话上下文导入机制。

### Web 抓取不稳定（#7180）——功能效用打折
> 部分网站抓取成功、部分失败、用户侧无法识别模式；另有用户观察 agent 倾向使用 http 工具而非 web_search 取数。

根因猜测：文档解析链路对部分站点输出"无文本"（见 #7104），或检索与抓取的 url 选择策略偏差。

### 技能选择可观测性（#7199，社区建议）——数据驱动调优方向
> 追踪"候选技能存在但未被选择"与"已选择且改变了最终答案"两类事件，避免 retriever 只看到"选错"数据。

这是对 #6565 skill 路由体系的有益补充：缺失"未被选中的候选"轨迹会让路由评估信号失真。建议优先将其吸收为 skill 评估验收标准的一环。

### 模型选择权限（#7183）——管理员单点瓶颈
> 想自己调节 LLM 模型，但只有管理员能改（管理员=认知负担）。

请求：per-user LLM 配置（当前仅 admin-only）。

### 付款与身份服务拆分诉求（#7105）
> 用户反馈支付相关 issue 持续出现，建议将 identity/session 与 org payments/credits 从 cloud API 拆出为独立服务。

---

## 8. 待处理积压

### 亟待关注（长期未响应/未关闭）
| # | Issue | 已开放 | 风险说明 |
|---|---|---|---|
| [#6752](https://github.com/nearai/ironclaw/issues/6752) | 实例删除失败+"Loading your agents..."卡死 | 7/28 至今（8天） | 影响安全（删除流程不完整）与登录体验；无 assignee、无 PR |
| [#7185](https://github.com/nearai/ironclaw/issues/7185) | 跨会话记忆不可靠 | 8/4 | 核心价值主张受损、多位 Champion 反馈；尚无 fix PR |
| [#6947](https://github.com/nearai/ironclaw/issues/6947) | `classify-test-scope.sh` 将 `ironclaw_product` 错误归类为 legacy-only | 7/31 | CI 测试作用域判定失真，影响所有涉及该 crate 的 PR 测试覆盖 |
| [#7115](https://github.com/nearai/ironclaw/issues/7115) | Docker entrypoint 用废弃环境变量做迁移判断 | 8/4 | 用户跟文档执行会跳迁移、产生脏状态 |

### 长期开放的老 Epic
- [#3773](https://github.com/nearai/ironclaw/issues/3773)（5/19 至今）：目标 crate 架构落地——仍在进行中的大 epic，日常 PR 多由此驱动，暂无风险，但需留意战线过长导致 v1.2.0 延期风险。

### CI/CD 积压开放 PR
- [#7140](https://github.com/nearai/ironclaw/pull/7140)（dependabot）：8 项依赖升级（含 base64 0.22→0.23、rstest 等），L 级、风险低——持续未合并有累积退化风险。

---

> **总体评价**：项目当前处于 v1.1.0-rc.1 发布冲刺与架构重构并行的高强度阶段，整体节奏快、CI 门禁与治理审计并行驱动，但需关注迁移无损性（#7178）、跨会话记忆（#7185）等核心价值主张问题，以及那 121 处 tracing 错误写法（#7146）的可观测性缺口。外部贡献者活跃度良好，新增的 Nostr host functions 与代理设置忽略诊断均为真实使用场景驱动。若无新版本发布预期在一周内完成，建议优先合并 #7198 并完成剩余 2 个 Windows 阻塞修复。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-05

## 今日速览

过去24小时项目保持活跃，共产生14条动态。**PR合流节奏显著加快**，10条PR被合并/关闭（含8.3版本发布流程的6条合入），3条PR等待合并。**值得高度关注的是，Issue #1202（Agent泄漏模型Key敏感信息）在停更4个月后于8月4日重新被更新**，且目前仍处于开放状态，安全风险尚未修复。此外，#2374（隐藏侧边栏广告）的持续开放和#1205（会话重命名失败提示）的推进表明社区对体验细节有持续需求。版本发布方面，8月3日更新已合入主干。整体而言，项目处于**高频迭代、社区活跃、但安全修复滞后**的状态。

## 版本发布

今日无新版本发布。但PR #2430（[Release: 2026.8.3](https://github.com/netease-youdao/LobsterAI/pull/2430)）已将 `release/2026.8.3` 分支合入 `main`，说明 **8月3日版本已完成发布流程**。根据PR描述，该版本主要包含以下更新：

- 新增原生积分奖励活动
- 优化首次运行登录体验
- 新增 Artifact 自动预览控制开关
- 改进模型错误处理
- 提升 Windows 安装程序可靠性

> 注意：用户需知晓该版本涉及登录流程和预览行为变更，建议查看更新日志确认使用习惯是否受影响。

## 项目进展

今日合并/关闭的PR中，**6条与2026.8.3版本发布直接相关**，覆盖以下功能推进：

| PR | 内容 | 状态 |
|---|---|---|
| [#2424](https://github.com/netease-youdao/LobsterAI/pull/2424) | **恢复积分活动核心逻辑**：回滚此前提交，恢复订阅积分重置、500积分领取流程（IPC/UI/资源），并恢复活动状态透传 | 已合并 |
| [#2427](https://github.com/netease-youdao/LobsterAI/pull/2427) | **积分活动素材本地化打包**：将启动积分海报和CTA图片打包至客户端，弹窗由本地资源渲染，服务端仍控制可用性/时机/奖励发放 | 已合并 |
| [#2428](https://github.com/netease-youdao/LobsterAI/pull/2428) | **积分活动分析字段完善**：上报完整登录跳转URL、包含服务端/网络/登录失败错误信息、Electron认证IPC返回登录URL，并补充测试 | 已合并 |
| [#2425](https://github.com/netease-youdao/LobsterAI/pull/2425) | **新增Artifact自动预览开关**：用户可关闭文件自动预览，保留手动预览功能 | 已合并 |
| [#2426](https://github.com/netease-youdao/LobsterAI/pull/2426) | **模型过载错误独立分类**：将provider过载/容量错误从通用限流消息中拆分，以准确提示用户（配合OpenClaw限流文案覆盖） | 已合并 |
| [#2429](https://github.com/netease-youdao/LobsterAI/pull/2429) | **登录页UI优化** | 已合并 |

此外，依赖升级方面也完成多个合并：Electron系列（#1277，升级至43.2.0）、@headlessui/react（#1282）、React 18→19（#1283）、react-syntax-highlighter（#1284）。**关注React 19升级是否引发兼容性回归**是后续观察点。

## 社区热点

今日最值得注意的社区事件是 **Issue #1202（[【bug】agent泄漏model key信息](https://github.com/netease-youdao/LobsterAI/issues/1202)）在沉寂4个月后被重新激活**，当前仍为OPEN状态。该Issue报告了严重的安全隐患：Agent可被诱导透露配置文件中模型Key的路径及环境变量信息，存在敏感信息泄露风险。评论数1条，虽不算多，但涉及安全问题且长期未修复，社区关注度可能上升。

PR #2374（[feat: add permanent setting to hide sidebar ad banner](https://github.com/netease-youdao/LobsterAI/pull/2374)）也值得关注，它试图解决侧边栏广告只能临时关闭、无法永久隐藏的体验问题，当前为OPEN状态。该PR关联了Issue #2342，若合入将改善免费用户的日常使用体验。

## Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 修复状态 |
|---|---|---|---|
| **高** | [Issue #1202](https://github.com/netease-youdao/LobsterAI/issues/1202) | Agent可被诱导泄露模型Key的环境变量/文件路径等敏感信息 | **无关联fix PR，仍开放** |
| 中 | [PR #1205](https://github.com/netease-youdao/LobsterAI/pull/1205) | 会话重命名失败被静默吞掉（输入框关闭但标题未变更），用户无感知 | 有PR待合并，已含本地化toast提示与重试机制 |

**安全风险提示**：Issue #1202 自4月1日创建至今已超过4个月，期间未有关联修复PR，属于**长期未响应的安全漏洞**。考虑到LobsterAI定位为AI助手客户端，key管理直接关系用户云端资源安全，建议维护者优先跟进。

## 功能请求与路线图信号

当前社区功能需求集中在以下方向，且大多已有PR在推进：

1. **广告控制**（#2374）：用户希望永久隐藏侧边栏广告，当前仅支持临时关闭。此功能与免费用户日常体验强相关，若合入将直接影响满意度。
2. **错误反馈可感知**（#1205）：要求重命名等操作失败时给予明确UI提示，而非静默失败。属于通用体验优化，常作为质量指标之一。
3. **积分活动系统完善**（#2424/#2427/#2428）：已合入的积分奖励功能，后续可能继续迭代活动规则、UI细节以及分析埋点。

> 基于以上，广告隐藏开关（#2374）和会话重命名错误提示（#1205）有较大概率被合入下一版本（2026.8.x 或 2026.9）。

## 用户反馈摘要

从Issue #1202可见，用户关注点在于 **AI助手的权限边界与数据安全**。该Issue要求agent不应主动暴露配置文件路径、环境变量名称等敏感信息，反映出用户对"AI可能被提示词注入或社会工程学利用"的担忧。此外，评论区的存在也暗示用户可能已在讨论缓解措施或补充更多利用场景。此反馈指向的产品方向是：**AI行为需具备更严格的安全边界控制**，建议产品侧考虑加入敏感信息过滤/屏蔽策略。

来自PR #2374的诉求则相对温和，用户希望增加一个开关以彻底禁用广告展示，减轻干扰，本质上是对**非订阅用户使用体验的优化需求**。

## 待处理积压

以下为长期未合入/响应的PR及Issue，建议维护者安排时间处理：

| 类型 | 编号/链接 | 说明 | 搁置时长 |
|---|---|---|---|
| Issue（安全） | [#1202](https://github.com/netease-youdao/LobsterAI/issues/1202) | Agent泄漏model key信息，无关联修复PR | 4个月+（创建于4月1日，8月4日被更新） |
| PR | [#1205](https://github.com/netease-youdao/LobsterAI/pull/1205) | 会话重命名失败无提示，PR已就绪待合并 | 4个月+（创建于4月1日） |
| PR | [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) | 永久隐藏侧边栏广告的开关 | 2周+（创建于7月21日） |
| PR | [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | Electron 40→43依赖升级（含electron-builder） | 4个月+（创建于4月2日，今日被更新） |

> **优先建议**：安全类Issue #1202应尽快分配负责人，评估Agent配置读取与输出过滤逻辑，修复方案建议包含提示词注入防护与敏感信息过滤两层。同时#1205和#2374均为改善用户体验的小改动，合入成本不高，建议提速处理。

---

*数据统计周期：2026-08-04 至 2026-08-05 | 数据来源：LobsterAI GitHub 仓库*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-08-05

## 1. 今日速览

Moltis 项目在过去 24 小时内整体活跃度处于**低水平**：无新的 Issue 提交或关闭，仅新增 1 条依赖更新 PR（#1184），无版本发布。团队工作节奏平缓，当前无阻塞性开发任务或紧急问题。项目处于健康但不活跃的状态，核心维护节奏趋稳，社区参与度有待观察。

---

## 2. 版本发布

**无新版本发布。** 上一个版本相关信息未在本次数据中提供，建议持续关注 Releases 页面获取后续更新。

🔗 https://github.com/moltis-org/moltis/releases

---

## 3. 项目进展

### 今日无合并或关闭的 PR

唯一的 PR #1184 由 dependabot 自动发起，目前处于**待合并**状态，尚未合入主分支。该 PR 不涉及功能开发，属于日常依赖维护。

**今日未推进任何功能开发或修复工作。** 鉴于 PR 为自动化提交且无冲突迹象，预计维护者将在例行审查后合并。

🔗 [#1184: chore(deps-dev): bump undici from 7.28.0 to 7.29.0 in /website](https://github.com/moltis-org/moltis/pull/1184)

---

## 4. 社区热点

**今日无高热度讨论。** 唯一活跃条目为 PR #1184（dependabot 自动更新），无人工评论、无 👍 反应。该 PR 将 **undici** 从 7.28.0 升级至 7.29.0，作用于 `/website` 目录。undici 是 Node.js 生态中重要的 HTTP 客户端库，其版本更新通常包含安全补丁或性能优化，虽然当前无社区讨论热度，但该升级对网站依赖安全性具有积极意义。

🔗 [#1184](https://github.com/moltis-org/moltis/pull/1184)

---

## 5. Bug 与稳定性

**今日无新报告的 Bug、崩溃或回归问题。** 项目当前稳定性状态良好，无需紧急修复事项。

---

## 6. 功能请求与路线图信号

**今日无新功能请求或路线图线索。** PR #1184 仅涉及依赖升级，不暗示任何新功能方向。若需了解近期路线图，建议查看项目 README 或 Projects 面板。

---

## 7. 用户反馈摘要

**今日无用户评论或反馈可用。** 项目社区交互较少，缺乏可直接引用的用户声音。建议关注后续 Issue 讨论以获得一手反馈。

---

## 8. 待处理积压

### 需要关注的待合并 PR

- **[#1184] chore(deps-dev): bump undici from 7.28.0 to 7.29.0 in /website** — 已等待 1 天（创建于 2026-08-04），由 dependabot 自动提交。该 PR 属于常规依赖更新，无明显风险，建议维护者尽快审查合并，避免依赖积压。

🔗 https://github.com/moltis-org/moltis/pull/1184

---

## 总结

Moltis 项目今日处于**低活跃、高稳定**状态：无新问题、无功能变动、无版本发布，唯一条目为自动化依赖更新。项目健康度良好，但社区参与度偏低。对于关注该项目进展的用户，建议持续跟踪后续 PR 合并节奏及版本发布计划，以判断项目下一阶段的活跃周期何时启动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报 — 2026-08-05

## 1. 今日速览

CoPaw 项目过去24小时活跃度极高，总计产生 28 条 Issue 更新和 50 条 PR 更新，其中 Issue 关闭率约 39%（11/28），PR 合并/关闭率约 44%（22/50）。当前有 **17 个开放 Issue** 和 **28 个待合并 PR**，社区贡献热度持续走高，出现了多个 first-time-contributor 提交的 PR。今日无新版本发布，但针对 v2.1.0-beta.1 的 **两项严重稳定性 Bug 报告（#6697、#6698）** 值得高度关注，涉及桌面端 Python 子进程崩溃及浏览器 SDK 功能不可用。整体来看，项目处于功能迭代与稳定性加固并行的高活跃阶段，社区反馈渠道畅通，维护者响应速度较快。


## 2. 版本发布

过去 24 小时内无新版本发布。当前最新版本仍为 **v2.1.0-beta.1**（Beta），其安装验证 Issue（[#6656](https://github.com/agentscope-ai/QwenPaw/issues/6656)）已于今日关闭。


## 3. 项目进展

今日有 6 个 PR 被合并/关闭（不含依赖机器人操作），核心进展集中在以下三个方向：

**时间戳/会话时区修复（关键路径）**

- [#6685 fix(timestamp): improve timestamp handling in agentscope_msg_to_message](https://github.com/agentscope-ai/QwenPaw/pull/6685)：修复 #6301——naive UTC 时间戳被误当作本地时区的问题，已合并。
- [#6309 fix(chats): convert session timestamps across timezones](https://github.com/agentscope-ai/QwenPaw/pull/6309)：AgentScope 消息时间戳统一转换逻辑，已关闭。
- [#6618 fix(console): remove forced UTC timestamp normalization in session list](https://github.com/agentscope-ai/QwenPaw/pull/6618)：配合后端修复去除前端的强制 UTC 归一化，已关闭。

> 这三个 PR 构成了一条完整的 **"会话时间戳时区处理"修复链路**（后端→转换层→前端展示），说明团队在处理跨时区用户体验问题上采取了系统性方案，而非单点 patch。相关 Issue #6301 也已随之关闭。

**CI/集成测试基础设施加固**

- [#6678 fix(ci): install Playwright Chromium for the integration suite](https://github.com/agentscope-ai/QwenPaw/pull/6678)：集成测试中 Chromium 可执行文件缺失的修复。
- [#6679 test(integration): align import-local with #6487 and widen a flaky poll window](https://github.com/agentscope-ai/QwenPaw/pull/6679)：解决 `/import-local` 403 确定性问题与轮询窗口过窄。
- [#6686 test(integration): fix chrome contract mismatches and add missing p-tier markers](https://github.com/agentscope-ai/QwenPaw/pull/6686)：修复 CI 测试分级缺失导致的覆盖空洞。

> 这三个 PR 均来自同一贡献者（yutai78786），针对 CI 管线的覆盖缺口和跨平台确定性失败进行了集中修复，对项目健康度提升有直接价值。

**Console 配置同步修复**

- [#6682 fix(console): sync legacy max_iters when saving iteration limit](https://github.com/agentscope-ai/QwenPaw/pull/6682)：修复迭代次数上限保存后 `max_iters` 与 UI 值不同步的问题。

> 整体评价：今日合并的 PR 以 Bug 修复为主，核心价值在于**修复了会话时区处理链路**和**加固了 CI 基础设施**。🏗️ 项目在稳定性和工程质量上的投入明显增加，此外仍有一批高价值 PR（如 #6628、#6629、#6691）处于开放状态，后续进展值得关注。


## 4. 社区热点

今日最受关注的 Issue 集中体现了 **桌面/通道场景下的安全审批可达性** 与 **多模型协作效率** 两大核心痛点：

- **[#6655 Console 通道不渲染安全审批提示（已关闭，12 条评论）](https://github.com/agentscope-ai/QwenPaw/issues/6655)**：在 console 通道下执行 `rm`/`del` 等高风险命令时，审批请求不渲染为终端可读提示，Agent 等待 300 秒超时被拒但用户全程无感知。这是**安全机制在特定通道下的可用性缺陷**，评论区讨论十分热烈。
- **[#6649 支持 GPT-5.6 prompt caching 参数（开放，13 条评论）](https://github.com/agentscope-ai/QwenPaw/issues/6649)**：用户 Sam 希望 Agent 循环的多轮对话复用缓存前缀以降低延迟和成本，涉及 `prompt_cache_key` 等参数透传。这是对**成本优化能力**的明确诉求。
- **[#6455 一个 Agent 同时使用多个模型跑（开放，3 条评论）](https://github.com/agentscope-ai/QwenPaw/issues/6455)**：用户 rerbin 提出需要让多个模型独立运行并汇总结果，用于**文件修改、事实核验等需要交叉验证的场景**。

> 此外，**WeChat（iLink）通道**成为今日高频问题区域，出现 3 个相关 Issue（详见下文 Bug 与稳定性部分），提示该通道近期改动可能带来了新的回归，需要维护团队重点关注。


## 5. Bug 与稳定性

### 🔴 严重（新版本阻断级，无 workaround）

- **[#6697 v2.1.0b1 桌面版注入 PYTHONHOME 导致所有 Python 子进程崩溃（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6697)**：Windows 10 下升级至 v2.1.0-beta.1 后，每个 Python 子进程启动即崩溃，报 `encodings ModuleNotFoundError`。影响 Agent 执行任何 Python 工具/脚本的能力，严重性极高，暂未见对应 fix PR。
- **[#6698 v2.1.0b1 浏览器 SDK open() 始终报 WireProtocolError（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6698)**：Windows 11 下浏览器工具连接成功但每次 open 均失败（Target crashed）。影响所有依赖浏览器自动化的技能，严重性高，暂无对应 fix PR。

> 以上两个问题均集中在 **v2.1.0-beta.1（Tauri 桌面版）**，且均由同一用户 AT8051 报告。该版本可能存在系统性的桌面端回归问题，建议维护者尽快复现并评估 **hotfix 或紧急发布 v2.1.0-beta.2** 的必要性，同时排查 Tauri shell + PyInstaller 后端的打包与运行时环境配置。

### 🟠 中等（功能受限，有 workaround 或已定位）

- **[#6695 仅使用微信通道时审批提示不可达（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6695)**：`rm`、`kill` 等门控命令的审批请求在纯 WeChat 通道下无法审批（console-only 对话框，5 分钟自动拒绝）。与 #6655 同属一类问题。
- **[#6696 微信 iLink 一次性 token 被打字指示器消费，回复被拒（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6696)**：`context_token` 被 typing indicator 消耗后，实际回复被服务器拒绝（ret=-2），导致"正在输入"状态卡死。这两个问题均无修复 PR。
- **[#6690 cron pause/resume 状态重启后丢失（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6690)**：只改 APScheduler 内存未持久化到 repo，重启后 enabled 状态丢失。**已有对应 fix PR [#6691](https://github.com/agentscope-ai/QwenPaw/pull/6691) 在审。**
- **[#6687 OpenRouter 多模态探测覆盖文档能力为 false（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6687)**：显式探测结果错误地覆盖了已从 OpenRouter 读取的图像/视频支持声明。
- **[#6683 App Center 安装 qwenpaw-creator 失败（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6683)**：插件顶层 `utils` 模块命名冲突导致加载失败。**已有对应 fix PR [#6688](https://github.com/agentscope-ai/QwenPaw/pull/6688) 在审。**

### 🟡 低严重度（体验问题或边缘场景）

- **[#6624 Scroll 自动压缩不触发记忆流程（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6624)**：自动压缩未触发 `summarize_when_compact`，手动 `/compact` 可触发。**已有对应 fix PR [#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629) 在审。**
- **[#6674 免费模型 429 限流导致任务中断（开放）](https://github.com/agentscope-ai/QwenPaw/issues/6674)**：`deepseek-v4-flash` 等免费模型频繁 429，建议改进限流处理。


## 6. 功能请求与路线图信号

| 功能请求 | Issue 链接 | 状态 | 是否已有 PR/纳入迹象 |
|---|---|---|---|
| GPT-5.6 prompt caching 参数支持 | [#6649](https://github.com/agentscope-ai/QwenPaw/issues/6649) | 开放 | 无对应 PR，但评论数 13 条，热度高 |
| 产物按任务分目录存放 | [#6643](https://github.com/agentscope-ai/QwenPaw/issues/6643) | 开放 | 无对应 PR，与 #6642 同源 |
| 频道启动重试机制 | [#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684) | 开放 | **已有 PR [#6689](https://github.com/agentscope-ai/QwenPaw/pull/6689)（feat(channels): retry transient startup failures）**，大概率纳入下个版本 |
| 全局规则文件（类似 .agent/.claude） | [#6694](https://github.com/agentscope-ai/QwenPaw/issues/6694) | 开放 | 无对应 PR，需求明确，涉及产品设计决策 |
| 按需加载 Skills（避免全量注入 system prompt） | [#6699](https://github.com/agentscope-ai/QwenPaw/issues/6699) | 开放 | 无对应 PR，但有量化数据支撑（27+ skills 消耗 8k-10k tokens），具备优化价值 |
| 多模型并行/汇总运行 | [#6455](https://github.com/agentscope-ai/QwenPaw/issues/6455) | 开放 | 无对应 PR，涉及核心执行引擎改动 |
| 添加 Volcengine Agent Plan 与小米 MiMo 内置 Provider | [#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) | 开放 | 无对应 PR，为新增 provider 配置，实现成本低 |
| 拖入文件直接引用原路径而非上传复制 | [#6642](https://github.com/agentscope-ai/QwenPaw/issues/6642) | 已关闭 | 被关闭原因待确认，可能为 duplicate 或已拒绝 |
| ReMe 记忆搜索增加 reranker（后端） | — | — | **已有 PR [#6398](https://github.com/agentscope-ai/QwenPaw/pull/6398)（feat: add reranker support for ReMe memory search）**，在审中，可能在 v2.2 落地 |
| 对话命令参数脱敏 | — | — | **已有 PR [#6692](https://github.com/agentscope-ai/QwenPaw/pull/6692)**，修复日志中明文记录命令参数的问题，方向明确 |

> 综合来看，**"频道稳定性"与"上下文/记忆优化"**是当前最清晰的两条路线图信号：前者有 PR #6689 的启动重试作为直接响应，后者则有 #6699 的按需加载和 #6398 的 reranker 两个方向的探索。


## 7. 用户反馈摘要

以下反馈提炼自今日活跃的 Issue 评论：

- **安全审批在非 Web UI 通道下存在严重可用性缺陷**：多位用户（rerbin、huyj1890）反映 console 和 WeChat 通道下审批提示不渲染或不可达，Agent 超时静默。用户认为这是"致命"的体验问题——**安全机制本身反而阻塞了任务执行且不给出任何提示**。
- **文件处理体验绕弯路**：用户 rerbin 连续提出 3 个相关 Issue（#6642、#6643、#6583），核心诉求一致——**文件拖入应直接读原路径而非先复制到 media 目录、产物应分目录存放、文件名应完整展示**。说明当前文件处理流程在桌面场景下明显违背用户直觉，且 media 目录的混乱已成为实际痛点。
- **社区对免费模型成本敏感**：用户 lt91888 表示"日常使用免费 deepseek-v4-flash 整体体验很好"，但 429 限流频繁导致任务中断。侧面反映**低成本模型接入是重要的用户增长场景**，但稳定性还需要配套的重试/降级策略来支撑。
- **"全局系统提示词"被反复提及**：用户 CreatorEdition 在 #6694 中建议类似 `.agent`/`.claude` 的全局规则文件，认为缺少顶层 system prompt 会导致部分提示词"无法生效"。这可能反映了**多层级 prompt 合并机制存在歧义或缺陷**。
- **用户对桌面端新版本信心受挫**：AT8051 连续报告两个 v2.1.0-beta.1 的阻断级 Bug（#6697、#6698），表明 **Beta 版本的稳定性把关仍需加强**，Tauri 桌面端的打包和运行时隔离需要更充分的回归测试。
- **DeepSeek 系列模型兼容性持续被关注**：xiaoman770521 报告 DeepSeek thinking mode 多轮对话中 `reasoning_content` 缺失，且 retry 机制只对首次生效。说明 **DeepSeek 系多轮对话的 reasoning 内容处理**仍需进一步适配。


## 8. 待处理积压

以下问题长期未闭环，建议维护者优先关注：

| 编号 | 类型 | 标题 | 创建时间 | 天数 | 备注 |
|---|---|---|---|---|---|
| [#4947](https://github.com/agentscope-ai/QwenPaw/issues/4947) | Feature | ADD Kanban Board for Playground Multi-agents | 2026-06-03 | 63 天 | 已关闭，但持续 63 天未处理，说明 Playground 相关功能路线优先级较低 |
| [#6455](https://github.com/agentscope-ai/QwenPaw/issues/6455) | Feature | 一个 Agent 同时使用多个模型跑 | 2026-07-24 | 12 天 | 核心执行引擎特性，需要架构级设计，建议在路线图中明确排期 |
| [#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) | Feature | 添加 Volcengine 与小米 MiMo 内置 Provider | 2026-07-27 | 9 天 | 实现成本低，可快速合入，但目前无维护者响应 |
| [#5906](https://github.com/agentscope-ai/QwenPaw/issues/5906) | Bug | 防重复功能误判（Doom loop 假阳性） | 2026-07-09 | 27 天 | 今日关闭，但曾持续 27 天未推进，提示防重复检测算法的鲁棒性检查可能不够充分 |
| [#6374](https://github.com/agentscope-ai/QwenPaw/issues/6374) | Bug | Token usage 持久化失败后不重试 | 2026-07-22 | 14 天 | 今日关闭，从报告到关闭历时 14 天，期间无活跃讨论，说明该问题可能已通过其他 PR 侧修复 |

> ⚠️ 另外值得注意：**[PR #4267](https://github.com/agentscope-ai/QwenPaw/pull/4267)（Mac OS 文件路径白名单安全机制）** 自 2026-05-13 创建至今已超 80 天仍未合并或关闭，涉及安全关键功能，建议维护团队明确其状态（继续推进或关闭并说明原因），避免社区贡献者的工作长期悬置。

---

*本报告由 AI 自动生成，数据来自 CoPaw GitHub 仓库公开信息。*
*报告生成时间：2026-08-05*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-05

> 数据窗口：2026-08-04 12:00 UTC — 2026-08-05 12:00 UTC（按 GitHub 更新日期统计）


## 1. 今日速览

ZeroClaw 在数据窗口内保持高活跃度，共产生 100 条 Issues/PR 更新，其中绝大部分（96%）仍处于开放或进行中状态，仅有 2 个 Issue 和 2 个 PR 关闭。值得注意的是一些重量级 RFC（包括 #8603 Chat Completions profile、#7155 工具权限层级、#9488 附件架构）在更新窗口中均获得新一轮评审推进，且多个核心志愿者持续贡献评论；但 **未合并 PR 积压 48 个**，其中多数已标记 `needs-author-action`（等待作者回复），合并吞吐量偏低，可能成为项目健康度的主要隐忧。新版本发布为 0，项目正处于一个**密集设计与评审、但合并节奏较慢**的阶段。


## 2. 版本发布

无新版本发布。


## 3. 项目进展

> 数据窗口内 PR 关闭/合并 2 个（合计）。以下为本次窗口内 **新提交** 或 **显著推进** 的 PR（均未合并，处于待评审或待作者行动状态）——本项目当前合并吞吐量偏低，此处展示的是代码贡献的推进方向：

- **PR #9723** — `fix(tool-call-parser): parse DeepSeek DSML and <|tool_call|> envelopes`，由 savioruz 于 2026-08-04 新提交，解决 DeepSeek 系列模型输出非 OpenAI 风格工具调用时原始文本透传给用户的解析缺陷。[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9723)
- **PR #9713** — `feat(runtime): expose token accounting on history-trim events`，由 Project516 提交，为历史裁剪事件补充 token 计量（回应 #9619），改善长会话上下文预算的可观测性。[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9713)
- **PR #9715** — `fix(infra): make JSONL session migration retry-safe`，由 Audacity88 提交，为 JSONL 会话迁移增加事务锁和原子提交，消除重试竞态。[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9715)
- **PR #9754** — `fix(channels): gate Slack lifecycle localization helpers`，由 Audacity88 提交，将 Slack 生命周期本地化工具链锁到 `channel-slack` 特性之后（小规模、低风险）。[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9754)
- **PR #9757** — `fix(providers/anthropic): deliver tool-result images as nested blocks`，由 leomem 提交，修复 Anthropic 工具返回图片无法到达模型的问题。[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9757)

**重要说明**：由于本次窗口内合并关闭仅 2 个且未在活跃评论榜单中，无法精确锁定合并对象。但可以确认：**#8568 MoA 虚拟模型提供者** 与 **#8586 webhook 通道消息分发重构** 两个 RFC/重构 Issue 被标记为 CLOSED——它们已完成评审使命或后续以 PR 形式落实到代码中。


## 4. 社区热点

以下为数据窗口内评论数最多的活跃 Issues（附诉求分析）：

- **#8603 — RFC: ZeroClaw Chat Completions profile**（16 评论，评论区持续更新至 2026-08-04）。这是在为 OpenAI Chat Completions 协议（Open WebUI、LobeChat、Continue.dev、Aider、LangChain、OpenAI SDK 等客户端）提供第一方网关适配层。**社区诉求**：引入标准协议接入层、让成熟 AI 前端生态无缝对接 ZeroClaw，同时保持 ACP/WebSocket 通道作为高级接口。[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)
- **#8303 — RFC: Goal mode v1（有界前台矩阵工作）**（14 评论）。目标是给 ZeroClaw 提供跨多轮（multi-turn）的有界用户目标执行能力，并明确第一版实现边界（不包含重启交接、广播通道准入、模型发起控制等）。**社区诉求**：长任务自主执行与结构化编排。[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)
- **#7155 — RFC: 高危 shell 命令逐次确认 + Codex 风格策略模式（allow/ask/deny）**（13 评论，8 月 4 日更新 Rev 2）。将原先仅针对 shell 的命令策略，推广为**统一的全工具权限层**。**社区诉求**：在 Agent 自主性和用户安全之间建立细粒度可配置的信任边界。[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)
- **#9488 — RFC: Web 聊天与渠道的统一附件架构**（12 评论）。**社区诉求**：统一各渠道附件上传/引用/存储链路，避免 Web 与渠道各自为政。[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)

**观察**：热点集中在**协议兼容层、工具调用权限模型、跨渠道架构统一**三大方向，说明社区关注点正从“可用性”转向“生产级可控性”与“生态互操作”。


## 5. Bug 与稳定性

按严重程度从高到低排列（均来自近期提交、且已通过 Issues 进入跟踪队列）：

| 严重级别 | Issue | 描述 | 状态 / 修复 PR |
|---|---|---|---|
| **S0** | [#9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565) | **Gateway webhook 未 fail-closed**（WhatsApp Cloud、Linq、WATI），表现为攻击者可未认证直接向 Agent 投递消息（源码级验证） | 已标记 `status:in-progress`，跟踪中 |
| **S0** | [#9647](https://github.com/zeroclaw-labs/zeroclaw/issues/9647) | **知识图谱无 per-agent 归属**：任何 Agent 可读取/修改其他 Agent 的知识（全局共享图） | 已标记 `status:accepted`，后续修复 |
| **S0** | [#9646](https://github.com/zeroclaw-labs/zeroclaw/issues/9646) | **会话/频道读写工具缺乏归属校验**（sessions_list/history/send、discord_search 等），Agent 可横向越权 | 已标记 `status:accepted`，后续修复 |

### 其余分类：
- 高风险（P1，已接受/处理中）：[#9647]、[#9646]、[#9565]（上述）。
- 中风险（P0/P1，开发中）：PR #9362 修复浏览器工具截图路径逃逸（任意文件写入，已提交 PR）。PR #9320 修复 cron Agent 无界运行导致锁永挂。PR #9304 修复带 reasoning 的 tool turn 在兼容接口上被拒绝后未禁用 reasoning 重试。PR #9313 修复微信通道在入队前持久化游标导致崩溃丢消息。


## 6. 功能请求与路线图信号

以下 RFC 已进入活跃评审，结合维护者标记（`needs-maintainer-review` / `accepted`）可判断其有望进入后续里程碑：

| RFC / 功能 | 核心内容 | 当前状态 | 预估纳入版本 |
|---|---|---|---|
| [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) — Chat Completions profile | 提供 OpenAI 协议兼容网关 | 评审中（16 评论） | 方向明确，预计 v0.10+ |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) — 全工具权限层级 | 将 allow/ask/deny 模型扩展到所有工具 | 评审中（Rev 2，13 评论） | 预计 v0.9.x 安全架构的一部分 |
| [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488) — 统一附件架构 | 跨渠道附件上传/存储/引用统一 | 评审中（12 评论，新增关闭的 #8568 为相关合并参考） | 预计 v0.10+ |
| [#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) — 会话归属权与传输适配层 | 会话持久化契约的运行时所有权 | 评审中（Rev 2，已与 #9488/#9600 锁定边界） | 预计 v0.10+ |
| [#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100) — Per-model 能力与上下文窗口配置 | 模型多模态能力、上下文预算显示 | 评审中（P1，7 评论） | 可能加快，UI 依赖此配置 |

另注意：**#8132**（React→Rust/Wasm 前端重构）与 **#7822**（WASM 插件生命周期钩子）虽处于 `needs-author-action` 低活跃状态，但属于长期架构方向，值得关注。


## 7. 用户反馈摘要

基于 Issues 评论区提炼的真实反馈：

- **通用协议接入需求非常明确**（#8603）：用户在评论中反复提及 Open WebUI、LobeChat 等成熟前端无法直接使用 ZeroClaw，只能“退而求其次走 WebSocket 自研客户端”，已构成采用阻力。
- **安全模型诉求：从工具级走向策略级**（#7155）：多名用户表示“不是不信任 Agent，而是希望系统能给出可解释、可审计的确认路径”。当前全有或全无的粗粒度授权被批评为“开箱即用的隐患”。
- **对架构纠缠的抱怨**（#9487/#9488 评论）：Web 端与会话层、渠道层耦合过深，导致新渠道接入成本高、回归风险不可控，社区希望向“运行时所有权 + 适配层”方向收敛。
- **对维护响应速度的隐性不满**：`needs-author-action` 在活跃 RFC 中大量存留（如 #6850、#6971、#8424），说明作者跟进不及时已成为流程瓶颈。


## 8. 待处理积压

以下 Issue/PR 长期未获作者响应（标记 `needs-author-action`），建议维护者通过 bot 提醒或主动介入：

| 项目 | 类型 / 标签 | 等待时长（自创建） | 说明 |
|---|---|---|---|
| [#6850](https://github.com/zeroclaw-labs/zeroclaw/issues/6850) — 存储后端的生命周期策略解耦 | RFC | 75 天 | 核心架构议题，无作者行动，阻塞记忆子系统优化 |
| [#6971](https://github.com/zeroclaw-labs/zeroclaw/issues/6971) — 安全 UX、凭据边界与隔离默认值 | RFC | 70 天 | 跨域安全设计文档，长期搁置 |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) — 工作区相对路径禁止与 .zeroclawignore | RFC | 38 天 | 工作区文件保护，作者未动作 |
| [#8398](https://github.com/zeroclaw-labs/zeroclaw/issues/8398) — 插件权限、配置与密钥模型 | RFC | 39 天 | 插件系统待决策的关键开放问题 |
| [#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822) — WASM 插件生命周期钩子订阅 | RFC | 49 天 | 插件生态能力扩展，未推动 |

**建议**：为上述超 30 天未获作者响应的 RFC 设置 bot 自动提醒（`@author` 并标记 `stale`）；对已满 60 天的 RFC，考虑由维护者**代为接续推动**或正式打回，避免设计讨论长期悬置。


**总体健康度评估**：项目社区讨论热度与设计深度处于高位，安全与互操作议题的重视程度值得肯定；但 **PR 合并吞吐量偏低（48 个待合并）、多个 P0/P1 安全 Bug 已被确认但仍未有修复 PR、以及 5 个以上 RFC 作者失联**是当前最主要的三个风险信号。若维护团队能集中合并一批已通过的 PR（A2A 客户端 #9324、WASM 沙箱评测 #9214、cron 超时 #9320 等），并推进安全 Bug 修复，项目有望在下一版本中实现质量与架构双提升。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*