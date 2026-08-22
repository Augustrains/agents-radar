# OpenClaw 生态日报 2026-08-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-22 00:29 UTC

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

# OpenClaw 项目动态日报 — 2026-08-22

## 今日速览

过去24小时，OpenClaw 仓库保持高度活跃：共500条 Issue 更新（488条新开/活跃，12条关闭）和500条 PR 更新（383条待合并，117条已合并/关闭）。无新版本发布，但多个针对 `v2026.8.1-beta.2` 的验证正在推进中。值得关注的是，P0 级问题（Gateway 内存泄漏、SQLite 持久化损坏）仍在积压，另有数个涉及会话状态和消息丢失的高优先级 Bug 已关联修复 PR，显示维护团队正在积极应对稳定性挑战。整体来看，项目处于高吞吐的密集开发期，但**几个长期存在的 P0/P1 稳定性问题尚未解决，是项目健康度的主要隐患**。


## 版本发布

过去24小时**无新版本发布**。当前处于 `v2026.8.1-beta.2` 验证周期，相关进展见下文。


## 项目进展

过去24小时有 **117 条 PR 被合并或关闭**，主要推进方向包括：

- **多频道消息可靠性修复**：`#126424`（keep conversation delivery within agent bindings，已关闭）修复了多代理操作者在使用会话工具时发现消息被发送到错误频道的问题，覆盖 Discord、Telegram、Slack、飞书等16+频道。
- **模型认证恢复**：`#125471`（keep Claude CLI OAuth available in Control UI，已关闭）修复了 Gateway 重启后 Claude CLI OAuth 失去刷新所有权的问题。
- **流式响应失败传播**：`#127662`（fail streaming responses when agent runs fail，已关闭）修复了代理运行失败但用户仍收到成功响应的误导性问题。
- **测试与安全加固**：`#127708` 清理了重复的测试断言；`#116489`（require acknowledgement for install policy warnings，已关闭）为安装策略警告增加了确认机制。

重点合并项对会话状态、消息送达和认证链路均有关键修复，但多数属于缺陷修补，未出现大的新功能落地。


## 社区热点

今日讨论最活跃的 Issue 集中在平台稳定性与数据一致性问题：

1. **`#91588`（评论 23，👍1，P0）— Gateway 内存泄漏致 OOM 崩溃**：[链接](https://github.com/openclaw/openclaw/issues/91588)  
   RSS 从启动时 350MB 增长至 15.5GB，2-3 天内触发 OOM kill，引发 `launchd-handoff` 重启循环。该问题自 6/9 创建至今仍在开放，社区关注度高。

2. **`#91009`（评论 22，👍2，P1）— Codex PreToolUse hook 进程 CPU 占满并阻塞 Gateway RPC**：[链接](https://github.com/openclaw/openclaw/issues/91009)  
   `openclaw-hooks relay --provider codex --event pre_tool_use` 每次调用消耗 ~100%+ CPU，导致工具调用链路阻塞。

3. **`#87744`（评论 18，👍4，P1）— Codex 支持的 Telegram 轮次超时**：[链接](https://github.com/openclaw/openclaw/issues/87744)  
   模型完成工作但 `turn/completed` 始终不达，用户收不到最终结果——影响 Telegram 会话可靠性。

4. **`#125626`（评论 18，👍0，P2）— Release validation: v2026.8.1-beta.2**：[链接](https://github.com/openclaw/openclaw/issues/125626)  
   维护者发起的公开验证工作单，社区成员可参与测试反馈。

5. **`#53628`（评论 14，👍1，P3）— `${XDG_CONFIG_HOME}` 在安装技能时未展开**：[链接](https://github.com/openclaw/openclaw/issues/53628)  
   Docker 部署场景下环境变量未被解析，安装流程受阻。

**核心诉求**：社区对 **长时间运行的稳定性**（内存泄漏、进程泄漏、SQLite 损坏）最为关切，其次是**消息送达可靠性**（turn/completed 不达、重复回复、参数丢失）。这两类问题的评论数和 👍 数均显著高于功能类需求。


## Bug 与稳定性

### P0 级（严重崩溃/数据损坏）

| Issue | 描述 | 时间 | 状态 |
|---|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏 350MB→15.5GB，OOM 崩溃循环 | 6/9 创建，6/22 更新 | 开放，无 fix PR |
| [#126821](https://github.com/openclaw/openclaw/issues/126821) | SQLite 损坏反复出现（5天5次），含"瘫痪模式"拒绝所有服务但不退出 | 8/20 创建 | 开放，需复现，无 fix PR |
| [#125333](https://github.com/openclaw/openclaw/issues/125333) | totalTokens 膨胀在 beta.2 仍复现，修复仅覆盖 `api === "cli"` 路径 | 8/17 创建 | 开放，无 fix PR |

### P1 级（消息丢失/核心功能故障）

| Issue | 描述 | 时间 | 状态 |
|---|---|---|---|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook CPU 100% 阻塞 Gateway | 6/6 创建 | 开放，无 fix PR |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex 轮次永不达 turn/completed，Telegram 无响应 | 5/28 创建 | 开放，无 fix PR |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | write/exec 工具参数在长对话后静默丢失 | 3/24 创建 | 开放，无 fix PR |
| [#126246](https://github.com/openclaw/openclaw/issues/126246) | Telegram 持久化外发卡在 send_attempt_started，重启后丢失 | 8/19 创建 | 开放，无 fix PR |
| [#86612](https://github.com/openclaw/openclaw/issues/86612) | Docker Gateway 在特定配置下重启循环 | 5/25 创建 | 开放，source-repro，无 fix PR |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程泄漏导致 zombie 累积 | 6/29 创建 | 开放，无 fix PR |
| [#108215](https://github.com/openclaw/openclaw/issues/108215) | 上下文占用从 57% 突降至 13%，无压缩记录 | 7/15 创建 | 开放，source-repro，无 fix PR |
| [#126631](https://github.com/openclaw/openclaw/issues/126631) | Sandbox skills bind-mount 创建 root 所有目录 | 8/20 创建 | 开放，linked PR |

### 已有修复 PR 的 Bug

| Issue | 描述 | 修复 PR |
|---|---|---|
| [#127176](https://github.com/openclaw/openclaw/issues/127176) | Windows 上 CLI 与 Node Host 设备元数据不一致 | [#127712](https://github.com/openclaw/openclaw/pull/127712)（fingerprint 容错） |
| [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram 贴纸不可用 | 已有 linked PR，未合并 |
| [#97826](https://github.com/openclaw/openclaw/issues/97826) | sendVideo 大视频宽高比错误 | 已有 linked PR，未合并 |

**趋势观察**：内存/进程泄漏、SQLite 损坏、消息丢失三类问题构成当前稳定性的三大主题。多个 P0/P1 已开放数周甚至数月，虽有 `clawsweeper` 标签标注，但**尚缺实际修复 PR**，需持续关注。


## 功能请求与路线图信号

今日活跃功能需求主要围绕：

1. **会话管理能力增强**
   - [#52640](https://github.com/openclaw/openclaw/issues/52640)：长任务持久状态面板（Discord 优先）
   - [#55249](https://github.com/openclaw/openclaw/issues/55249)：会话标签/昵称
   - [#51028](https://github.com/openclaw/openclaw/issues/51028)：会话按"最后有意义活动"排序

2. **频道交互体验升级**
   - [#88154](https://github.com/openclaw/openclaw/issues/88154)：Slack Modal 表单支持
   - [#53890](https://github.com/openclaw/openclaw/issues/53890)：Telegram 默认外发 topic 绑定
   - [#42840](https://github.com/openclaw/openclaw/issues/42840)：Control UI 中 MathJax/LaTeX 渲染（👍10，呼声高）

3. **配置与运维优化**
   - [#50199](https://github.com/openclaw/openclaw/issues/50199)：技能优先级配置
   - [#51336](https://github.com/openclaw/openclaw/issues/51336)：错误消息中展示上游 API 提供商名称（利于排障）
   - [#45771](https://github.com/openclaw/openclaw/issues/45771)：内置速率限制感知

**路线图信号**：`#40982`（提升 CLI 3 分钟无输出 watchdog 上限）和 `#41366`（持久化自然语言规则学习）均已关联开放 PR，显示维护者已接受相关提案，**大概率进入下一版本范围**。`#42840` 虽评论与 👍 数双高，但暂未获 maintainer 标签，纳入路线图仍待观察。


## 用户反馈摘要

从今日 Issues 评论中提炼的真实反馈：

**高满意度方向：**
- 社区对 `v2026.8.1-beta.2` 验证流程（#125626）的透明性给予积极评价，多名用户在 release-validation 工作单中贡献测试结果。
- [#127712](https://github.com/openclaw/openclaw/pull/127712) 的修复思路（"一次瞬时漂移不应永久卡死 Gateway"）得到了评论区的认可。

**主要不满与痛点：**
- **长对话后工具参数静默丢失**（#53408，👍2）：用户反馈"write/exec 工具在 15+ 轮后开始丢参数"，严重干扰编码类任务。
- **模型切换/长会话静默失败**（#58957，👍2）："切换模型后无任何错误提示，用户无法判断是上下文超限还是配置问题"。
- **自定义路径被硬编码覆盖**（#51429）：用户反映安装最新版后工作区被设为 `/Users/wangtao`，质疑"有人把个人路径合并进了发布代码"——虽然该 Issue 已积压 5 个月，但评论区的情绪仍较激烈。
- **消息送达时效性**（#53008）："一次内存压缩阻塞了主通道 10 分钟，所有 Telegram 消息排队等待"，对实时交互体验影响明显。
- **WhatsApp 群组静默**（#124458 关联）：`sendReadReceipts=false` 导致群组消息完全不可达，"为了隐藏已读状态付出了失去群组通信的代价"。

**使用场景观察**：用户以 **Telegram / Discord / 飞书等 IM 频道接入** 和 **Codex/Claude CLI 模型后端** 为主，对「长时间无人值守运行」和「多频道消息可靠性」有强依赖，这与当前 bug 高发区域高度重合。


## 待处理积压

以下 Issue/PR 长期未获有效响应或修复，建议维护团队优先排查：

| 编号 | 描述 | 严重度 | 创建时间 | 备注 |
|---|---|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏致 OOM | P0 | 2026-06-09（已 74 天） | 评论 23，最活跃 P0，无 fix PR |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex turn/completed 永不达 | P1 | 2026-05-28（已 86 天） | 👍 4，Telegram 无响应 |
| [#51429](https://github.com/openclaw/openclaw/issues/51429) | 硬编码路径进入发布代码 | P2 | 2026-03-21（已 154 天） | 社区情绪强烈，需官方回应 |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后工具参数静默丢失 | P1 | 2026-03-24（已 151 天） | 👍 2，影响编码类任务 |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | Playwright 断言错误致 Gateway 崩溃 | P1 | 2026-03-13（已 162 天） | `not-repro-on-main`，需进一步验证 |
| [#83598](https://github.com/openclaw/openclaw/issues/83598) | Claude CLI OAuth 刷新仍断主通道 | P1 | 2026-05-18（已 96 天） | 用户称"修复未达预期" |
| [#127712](https://github.com/openclaw/openclaw/pull/127712) | catalog worker fingerprint 容错 | P1 | 2026-08-22（今日新开） | 待维护者审查，涉及会话状态 |

**积压特征**：多为 3 个月前创建的 P1 级稳定性问题（会话状态、消息丢失、OAuth），部分已被 `clawsweeper` 标记但修复推进缓慢。建议维护者对此类核心链路问题设置明确的修复 SLA，避免社区信任流失。


*本日报由 AI 分析师基于 GitHub 公开数据自动生成，仅供参考。*

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向分析报告

**报告日期：2026-08-22 | 数据窗口：2026-08-21 ~ 2026-08-22**


## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于**高速迭代与稳定性阵痛并存**的阶段。头部项目（OpenClaw、Hermes Agent、NanoClaw）以每日数十至数百条 Issue/PR 的吞吐量密集推进，但**长期存在的 P0/P1 稳定性问题**（内存泄漏、消息丢失、会话状态不一致）普遍积压，揭示出"功能扩张速度 > 稳定性消化能力"的结构性矛盾。同时，**多项目不约而同地向架构规范化收敛**——NanoBot 定义类型化 usage 契约、IronClaw 推进 CI 基础设施重构、Hermes Agent 聚焦"可证明的正确行为"，显示生态正从"野蛮生长"进入"精细化治理"的过渡期。安全与隐私（沙箱逃逸、密钥脱敏、数据驻留合规）成为跨项目的高频议题，而渠道体验一致性（Telegram/WhatsApp/ Slack 等）与长任务可靠性则是用户最普遍的核心诉求。


## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | 合并/关闭 | Release | 健康度评估 |
|------|-----------|---------|----------|---------|-----------|
| **OpenClaw** | 500 | 500 | 117 合并/关闭 | 无（beta.2 验证中） | ⚠️ 高风险：P0 内存泄漏/SQLite 损坏长期积压 |
| **Hermes Agent** | 50 | 50 | 1 合并 | ✅ v0.20.5（8/19） | 🟡 高活跃，合并通道积压（49 待合并） |
| **NanoClaw** | 1 | 24 | 11 合并/关闭 | 无 | 🟢 健康：迭代极快，架构演进清晰，少量协调性问题 |
| **NanoBot** | 5 | 37 | 23 合并/关闭 | 无 | 🟢 健康：合并效率高，结构重构有序 |
| **ZeroClaw** | 50 | 50 | 0 合并 | 无 | 🟡 注意：安全类 PR 堆积，0 合并需关注 |
| **IronClaw** | 4 | 16 | 16 合入/关闭 | 无（forward-port 已合入 1.3） | 🟢 健康：CI 改造推进有力，2 个 XL PR 待深入评审 |
| **LobsterAI** | 2 关闭 | 13 | 12 合并/关闭 | ✅ 2026.8.21 已并入 main | 🟢 良好：4.5 个月积压 PR 集中清理 |
| **CoPaw** | 部分 | 部分 | 15 | 无（v2.1.1-beta 迭代中） | 🟡 注意：工具调用 404/compact 回归等核心稳定性隐患 |
| **Moltis** | 2 | 8 | 1 合并 | 无 | 🟢 稳定收敛：修复占比高，1 个 5 个月积压 PR |
| **PicoClaw** | 1 | 4 | 4 合并/关闭 | 无 | 🟢 健康：积压清理良好（2 个 6 个月 PR 已合入） |
| **NullClaw** | 0 | 1 | 0 | 无 | 🟡 低活跃：平稳但社区冷淡 |
| **TinyClaw** | — | — | — | — | ⚪ 无活动 |
| **ZeptoClaw** | — | — | — | — | ⚪ 无活动 |


## 3. OpenClaw 在生态中的定位

**社区规模与影响力：** OpenClaw 以单日 500 条 Issue + 500 条 PR 的体量遥遥领先（次席 Hermes Agent 与 ZeroClaw 各约 50 条），是生态中**毫无争议的头部项目**，其 Issue 讨论度和社区参与深度（单 Issue 最高 23 条评论）也远超同类。

**技术路线：** 多频道聚合（16+ IM 平台）+ 多模型后端（Claude CLI/Codex 等）+ 网关架构。与 NanoClaw（Telegram 多实例 + attach surface 契约）、Hermes Agent（证明/状态一致性）、ZeroClaw（沙箱安全模型 + 插件隔离）相比，OpenClaw 的差异化在于**广度优先**——频道覆盖最全、集成面最广，但代价是稳定性风险面同步扩大。

**核心矛盾：** 尽管吞吐量最高，其 P0 级问题（Gateway 内存泄漏 350MB→15.5GB、SQLite 5 天 5 次损坏）已积压 74 天以上仍无修复 PR，这在生态中属于**最严重的稳定性欠账**。相比之下，IronClaw 当天创建的 CI 改造 Issue 当天即有配套 PR，NanoBot 的 bug 修复平均 1-2 天内合入。OpenClaw 的"高吞吐-低闭合"模式若持续，可能面临社区信任流失风险。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 | 热度评估 |
|---------|---------|---------|---------|
| **长时间运行稳定性** | OpenClaw（内存泄漏 #91588）、NanoBot（cron 任务消耗 token #5407）、CoPaw（空闲进程卡死 #6780）、Hermes Agent（macOS 休眠后无响应 #89083） | 内存/进程泄漏、OOM 崩溃、空闲后卡死、后台任务资源消耗 | 🔥🔥🔥🔥🔥 |
| **消息送达可靠性** | OpenClaw（turn/completed 不达 #87744、消息丢失）、Moltis（共享 Slack 频道工具失效 #1224）、ZeroClaw（流式输出 #10166） | 消息不达、静默丢弃、频道投递错误、流式输出可感知 | 🔥🔥🔥🔥 |
| **会话状态一致性** | OpenClaw（SQLite 损坏、参数丢失 #53408）、Hermes Agent（压缩边界缺陷 #88758）、NanoBot（Dream 游标卡死 #5441）、CoPaw（记忆串扰 #7193） | 状态持久化、上下文压缩/丢失、记忆串扰、游标不推进 | 🔥🔥🔥🔥🔥 |
| **安全与权限模型** | ZeroClaw（沙箱逃逸 #10165、高风险命令绕过 #10164）、Hermes Agent（NTLM 凭据泄漏 #91928、密钥脱敏 #77162）、NanoBot（Slack 重定向校验 #5414） | 沙箱隔离、命令白名单、密钥脱敏、下载安全 | 🔥🔥🔥🔥 |
| **MCP/连接健壮性** | CoPaw（MCP 重启无法恢复 #6524）、NanoBot（Notion MCP 连接失败 #1168） | MCP server 重启自动重连、连接失败可诊断 | 🔥🔥🔥 |
| **CI/基础设施规范化** | IronClaw（T1-T4 CI expedite）、ZeroClaw（CI 文档不一致 #10074）、NanoClaw（CI required check 修复 #3430） | 统一 CI 门禁、修复覆盖率误报、加速合并队列 | 🔥🔥🔥 |
| **渠道体验一致性** | OpenClaw（Slack Modal、Telegram topic）、ZeroClaw（WhatsApp push_name #10200）、NanoClaw（send_card 按钮丢失 #3426）、Moltis（WhatsApp Markdown/文件持久化） | IM 平台原生能力适配、格式转换、文件流转 | 🔥🔥🔥 |
| **合规与数据驻留** | NullClaw（Eden AI 欧盟合规接入 #990）、OpenClaw（上游 API 提供商名称展示 #51336） | GDPR 合规、数据驻留地要求、多供应商网关 | 🔥🔥 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|---------|---------|----------------|
| **OpenClaw** | 多频道聚合 + 多模型后端，广度优先 | 追求"全家桶"的中高级用户 | 中央 Gateway + 16+ 频道适配器；插件生态 |
| **Hermes Agent** | 桌面端 + 云 Agent + 深度可靠性（证明/状态一致性） | 桌面重度用户、企业级部署 | 桌面应用 + 本地 Gateway + 云服务混合架构；"可证明的正确行为"理念 |
| **NanoClaw** | 多实例部署 + 模板化 Agent 创建 + driver 契约 | 企业/团队用户，Slack 深度用户 | registerChannelAdapter 模式 + SessionExecSpec 契约 + Registry 集成 |
| **NanoBot** | 轻量级多通道助手 + memory/dream 机制 + WebUI/TUI | 轻量自托管用户、开发者 | 流式传输重试 + 类型化 usage 契约 + 轨迹记录后端 |
| **ZeroClaw** | 安全沙箱 + 插件隔离 + ZeroRouter/ZeroCode | 安全敏感用户、开发者 | 沙箱逃逸防护 + 插件子进程隔离 + 多路由协议 |
| **IronClaw** | Rust 原生 + 企业级 CI + 通知中心/收件箱 + WebUI 设计系统 | 企业开发者、Rust 技术栈用户 | Rust 实现 + forward-port 分支策略 + durable inbox |
| **LobsterAI** | 客户端 + DSH 运行时 + 定时任务 + Library 模块 | 桌面工具用户（Windows/macOS） | 桌面客户端 + DeepSeek Harness + IPC 层分析事件 |
| **CoPaw** | 上下文压缩 + 记忆搜索 + 审批流程 + 钉钉集成 | 中文用户、团队协作场景 | HookContext 注入 + 记忆搜索 + 多用户 Hub |
| **Moltis** | WhatsApp 深度集成 + 定时任务 + 浏览器隐身 | 小型团队、WhatsApp 重度用户 | 平台级适配（WhatsApp 原生格式转换）+ cron 输出回传 |
| **PicoClaw** | 轻量 Go 实现 + WebFetch 增强 + 多协议兼容 | 轻量部署、Go 技术栈用户 | Go 语言 + Anthropic Messages API + GitHub Trees API |
| **NullClaw** | 多供应商网关接入 + 合规 | 合规敏感用户、多模型聚合需求 | OpenAI 兼容层 + 欧盟数据驻留支持 |


## 6. 社区热度与成熟度分层

### 第一梯队：快速迭代期（高吞吐 + 功能扩张为主）

| 项目 | 特征 | 风险信号 |
|------|------|---------|
| **OpenClaw** | 单日 1000 条更新，生态最大 | P0 问题 74+ 天未修复，稳定性欠账最深 |
| **Hermes Agent** | 单日 100 条更新，架构议题深度讨论 | 49 条 PR 积压，合并通道拥堵 |
| **NanoClaw** | 单日 25 条更新，核心团队全覆盖 | PR 依赖顺序问题（#3397 revert），协调需改进 |
| **ZeroClaw** | 单日 100 条更新，安全加固密集 | 0 PR 合并，安全修复堆积，release 久未发布 |
| **CoPaw** | 单日 70 条更新，核心功能回归需关注 | 工具调用 404、compact 回归，影响核心链路 |

### 第二梯队：质量巩固期（中低吞吐 + 稳定性/体验优化为主）

| 项目 | 特征 | 亮点 |
|------|------|------|
| **NanoBot** | 单日 42 条更新，合并效率 62% | 类型化 usage 契约 + 轨迹后端，架构规范化先行者 |
| **IronClaw** | 单日 20 条更新，CI 基础设施主动重构 | 当天创建 Issue 当天配套 PR，响应速度标杆 |
| **LobsterAI** | 单日 15 条更新，积压清理显著 | 4.5 个月积压 PR 集中合入 |
| **Moltis** | 单日 10 条更新，修复占比高 | 稳定收敛，社区贡献者活跃 |
| **PicoClaw** | 单日 5 条更新，积压清理良好 | 2 个 6 个月 PR 集中合入 |

### 第三梯队：低活跃/停滞期

| 项目 | 特征 |
|------|------|
| **NullClaw** | 单日 1 条 PR，社区互动冷淡 |
| **TinyClaw / ZeptoClaw** | 24 小时无任何活动 |


## 7. 值得关注的趋势信号

### 信号一："可证明的正确行为"成为下一代可靠性标准
Hermes Agent 的"证明/状态/身份一致性"议题集群（#90866、#90049、#90144、#90145）、NanoBot 的类型化 usage 契约（#5478）、IronClaw 的权威化 CI 门禁（#7809）不约而同指向同一方向——**从"行为正确"走向"可验证的正确"**。对开发者的启示：在设计 Agent 系统时，应尽早引入类型化契约、可审计轨迹和权威化门禁，而非事后补救。

### 信号二：安全模型从"外围防护"走向"内生一致"
ZeroClaw 暴露的"delegate 绕过 block_high_risk_commands"与"父路径 allowlist 不生效"是同一安全机制的双向缺陷（#10164 + #10165）；Hermes Agent 强化 NTLM 路径拒绝（#91928）；NanoBot 修复 Slack 重定向校验（#5414）。**安全策略需要单一事实来源**，且委托/继承路径必须行为一致——这是所有多租户/多 delegate 架构的共同挑战。

### 信号三：渠道体验从"能用"走向"原生"
WhatsApp Markdown 转换（Moltis #1220）、WhatsApp push_name 可配置（ZeroClaw #10201）、Telegram 多实例支持（NanoClaw #3436）、Slack Modal 表单（OpenClaw #88154）——**每个 IM 平台的原生能力边界正在成为 Agent 体验的竞争焦点**。开发者应关注各渠道的"能力指纹"（支持哪些交互原语），并在 bridge 层对能力缺失做显式降级而非静默丢弃（NanoClaw #3426 的教训）。

### 信号四：CI/基础设施成为项目健康度的先行指标
IronClaw 的 CI expedite 系列（T1-T4）与 ZeroClaw 的 CI 文档不一致修复（#10074）表明，**合并通道效率、测试覆盖率准确性、门禁一致性**正成为社区评估项目健康度的关键指标。合并等待超过 30 天的 PR（Hermes Agent #54396/#58146、Moltis #468）已引发社区不满。

### 信号五：数据驻留与合规成为硬性选型约束
NullClaw 的 Eden AI 接入 PR（#990）明确以"欧盟境内 + 单一 API Key"为核心诉求，OpenClaw 用户要求在错误消息中展示上游 API 提供商名称（#51336）以支撑排障与合规审计。**GDPR 等法规正从"加分项"变为"准入门槛"**，多供应商网关 + 区域性节点将成趋势。

### 信号六：长时间无人值守运行的可靠性是最大痛点
OpenClaw 的内存泄漏、Hermes Agent 的 macOS 休眠后无响应、CoPaw 的空闲后进程卡死、NanoBot 的 cron 任务在禁用后仍消耗 token——**用户对 Agent 的期望已从"交互式工具"升级为"7×24 小时自主运行的服务"**。这要求架构设计必须考虑：内存增长的收敛性、休眠/唤醒的状态恢复、后台任务的资源可见性。

### 信号七：长任务可观测性与断点恢复成为刚需
OpenClaw 的"上下文占用突降无压缩记录"（#108215）、ZeroClaw 的"进程退出导致回合内容丢失"（#10121）及修复 PR #10197、CoPaw 的"审批流程对无人值守任务不友好"（#7198）共同指向：**用户需要知道 Agent "正在做什么、做了什么、为什么中断"**，并能在中断后精确恢复。NanoClaw 的 attach surface 契约（#3429，driver 描述 exec argv）正是此方向的架构级探索。


## 总结

| 维度 | 结论 |
|------|------|
| **生态阶段** | 从"功能竞赛"转向"稳定性 + 架构规范化"的过渡期 |
| **最大风险** | 头部项目（OpenClaw、ZeroClaw）的稳定性欠账与合并积压 |
| **最佳实践** | IronClaw 的"当天问题当天 PR"、NanoBot 的"类型化契约先行" |
| **开发者建议** | 关注"可证明的正确行为"（类型化契约、可审计轨迹、权威化 CI），在渠道 bridge 层做显式降级而非静默丢弃，优先解决长时间运行的稳定性与断点恢复 |

---
*本报告由 AI 分析师基于 2026-08-22 各项目 GitHub 公开数据自动生成，仅供参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-22

## 今日速览

NanoBot 项目在过去24小时内保持**高活跃度**，共产生 5 条 Issue 更新和 37 条 PR 更新，其中 23 条 PR 已合并或关闭，合并效率较高。值得关注的是，社区在**流式传输重试机制**（#5454）、**Dream 内存游标推进**（#5441）等领域提交了针对性的 bug 修复，同时一个涉及**多搜索源聚合**的新 provider 集成 PR（#5234）已进入待合并状态。项目整体趋向成熟，代码库在持续清理死代码（#5475），并围绕**类型化 usage 契约**和**轨迹记录后端**进行结构性重构。无新版本发布。

## 项目进展

今日合并/关闭的 PR 集中在以下几大主题，反映出项目正从功能扩展转向**稳定性加固**与**内部架构规范化**：

**🛠️ 环境修复：**
- **#5477** (`fix(webui): keep iOS PWA controls inside safe area`) — 修复 iOS PWA 控件出界问题，恢复 `viewport-fit=auto`，并同步主题色，提升移动端体验。
- **#5476** (`feat(tui): render LaTeX as Unicode`) — 在 TUI 中以 Unicode 渲染 LaTeX 数学公式，支持流式及历史回复，同时保留货币、Shell 变量等内容的原样输出。

**🔐 安全性强化：**
- **#5414** (`fix(slack): validate file downloads across redirects`) — 修复 Slack 文件下载在重定向链中缺乏校验的安全隐患，防止恶意 URL 重定向。

**🐛 关键 Bug 修复：**
- **#5407** (`fix(cron): retire persisted heartbeat/dream system jobs when disabled`) — 修复在配置中禁用 heartbeat/dream 后，持久化 cron 任务仍在触发并消耗 token 的回归问题。
- **#5442** (`fix(dream): advance cursor when tool errors were recovered`) — 修复 Dream 任务在工具错误被模型自愈后仍被判定为"未完成"、导致内存游标卡死并重复处理同一历史批次的问题，直接解决了 #5441。

**🧹 架构清理与重构：**
- **#5478** (`refactor(providers): define typed LLM usage contract`) — 定义不可变类型化 LLMUsage 契约，统一 OpenAI、Anthropic、Bedrock 等多 provider 的 usage 语义。
- **#5479** (`feat(trajectory): add unified provider usage backend`) — 为每次重试或 fallback 的 provider 调用记录轨迹行，为成本核算奠定基础。

整体来看，项目的核心改进方向是：**提升可靠性**（修复 cron 和 Dream 相关回归）与**统一内部契约**（usage 与轨迹），为未来版本在可观测性和成本控制上的能力做铺垫。


## 社区热点

24小时内最受关注的技术讨论集中在**模型切换机制**与 **MCP 连接兼容性**两个方向上：

- **Issue #5198** — *"Not possible to change models in a specific session unless reconfiguring the entire instance"*（4 条评论）
  用户 `whisperity` 指出无法在会话中灵活切换模型，`/model` 命令未能生效。该 Issue 已存在近一个月后于今日关闭，但讨论反映了不少用户对 **SaaS 级模型切换体验**（如 Cloud 服务中点击切换模型）的期待，这一诉求恰好与当前 WebUI/Agent 交互的设计方向相关。

- **Issue #1168** — *"Nanobot 连接 Notion MCP失败！"*（2 条评论）
  中文用户 `silence-breaker` 报告连接 Notion MCP 持续失败，但同样的 API 在 Claude 中可正常使用。此类 MCP 兼容性问题虽属个案，但说明 **MCP 生态兼容性**仍是社区成员实际使用中的主要摩擦点之一。

- **PR #5234** — *"feat(agent): integrate mst-python as a metasearch provider"*（OPEN，待合并）
  该 PR 引入 Meta-Search Tool（MST），聚合 DuckDuckGo、Google、Brave、Bing 等多搜索引擎结果并通过 RRF 算法融合排序，目标是为 agent 提供覆盖更广的搜索结果。这代表社区对**多源搜索增强**的明确兴趣，合入后可能提升 agent 的信息获取质量。


## Bug 与稳定性

按严重程度排列：

| 严重度 | Issue / PR | 描述 | 是否已有修复 PR |
|---|---|---|---|
| **高（P1）** — 功能核心路径 | [#5454](https://github.com/HKUDS/nanobot/issues/5454) | 流式 provider 中，一旦内容已开始流式输出，后续的 `server_error` 事件将**跳过重试逻辑**，导致对话中断。影响 Codex 等流式 provider 的稳定输出。 | ✅ 已有 PR 处理 |
| **中（P2）** — 功能异常 | [#5441](https://github.com/HKUDS/nanobot/issues/5441) | Dream 任务在工具错误被恢复后仍被判定为"未完成"，导致 `.dream_cursor` 永远不推进，后续每次运行都会重复处理相同历史批次，**重复编辑/重复执行**，浪费 tokens。 | ✅ 已合并于 #5442 |
| **中（P2）** — 后台任务管理 | [#5463](https://github.com/HKUDS/nanobot/issues/5463) | DingTalk 入站消息通过 `asyncio.Task` 转发，但任务生命周期缺少**终态观察者**，后台任务可能无人管护。 | ⚠️ 暂未匹配到修复 PR |

> 另注：PR #5457 (Open) `fix(channels): scope dispatcher exception boundary to message processing` 修复了单条消息处理异常导致整个 outbound 分发协程停止的潜在问题，属于同类稳定性加固，正在等待合并。


## 功能请求与路线图信号

- **多搜索源聚合** — PR #5234（Open）引入 MST 聚合搜索，说明 Agent 的信息检索能力正在从单一引擎向**多源融合**演进，预计将在后续版本中带来更优的检索质量。
- **技能手动调用模式** — PR #5405（Open）`feat(skills): support manual-only invocation` 支持通过 `disable-model-invocation: true` 将技能限定为**仅用户手动调用**，适合部署、发布等副作用明显的操作，避免模型自行调用。
- **Provider 轨迹记录与用量统计**（#5479 合入的用法记录后端，以及 #5478 的类型化 usage 契约）可能为下一版本的 **token 成本追踪**功能铺平道路。
- **TUI 中 LaTeX 渲染**（#5476 已合并）是终端用户呼声较高的体验改进，后续有望继续扩展数学公式与代码高亮支持。


## 用户反馈摘要

- **“模型不能动态切换”是当前最集中的体验痛点**（#5198）：用户希望像商业 SaaS AI 一样，在会话中随手点击模型标签即可切换模型，而不是必须修改配置重启实例。该 Issue 今日已关闭，但讨论中体现的交互期待值得在 WebUI 迭代中持续关注。
- **MCP 连接失败排查困难**（#1168）：中文用户反馈 Notion MCP 连不上，API 校验无误但无法定位原因。类似问题在 Discord 中也有讨论，建议维护者补充更详细的 MCP 连接调试日志与 FAQ 文档。
- **默认配置下 cron 任务意外消耗 token**（PR #5407 所修）：此前用户将 `gateway.heartbeat.enabled` 设为 `false` 后，持久化的定时任务仍在继续执行，浪费 token 且难以察觉。这是用户对**资源成本可见性**关注度的直接体现。

---

## 待处理积压

| 项目 | 详情 | 建议 |
|---|---|---|
| **[#5463](https://github.com/HKUDS/nanobot/issues/5463)** | DingTalk 后台任务无终态观察者（OPEN，0 条评论） | 新增 Issue，等待维护者指派。建议补充任务异常时的重试与清理策略 |
| **[#5420](https://github.com/HKUDS/nanobot/pull/5420)** (Open, conflict) | `feat(webui): add turn observability and safe recovery` — 为 WebUI 增加用户轮次可观测性与安全恢复能力，但标记为 **conflict**，需解决冲突后合并 | 该 PR 对提升 WebUI 对长任务的可见性有较大价值，建议维护者协助解决冲突 |
| **[#5379](https://github.com/HKUDS/nanobot/pull/5379)** (Open) | `fix(memory): preserve full consolidation input` — 修正 memory consolidation 流程的输入保留问题 | 已 Open 9 天，建议 reviewer 尽快关注，避免与未来的 memory 重构冲突 |

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，统计时间范围为 2026-08-21 至 2026-08-22。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-22

*数据周期：2026-08-21 ~ 2026-08-22 | 数据来源：NousResearch/hermes-agent GitHub 仓库*


## 1. 今日速览

Hermes Agent 在过去 24 小时内保持高强度迭代节奏：共产生 50 条 Issue 更新和 50 条 PR 更新，其中新开/活跃 Issue 46 条，待合并 PR 49 条。发布补丁版本 v0.20.5（v2026.8.19），滚动纳入自 v0.20.4 以来约 323 个 PR。**值得关注的信号**：(1) 架构类议题(#90866、#90049、#90144、#90145、#91911)持续聚焦于“证明/状态/身份一致性”这一核心可靠性主题；(2) 围绕 Gemini 模型 session 标题生成故障（#91927）出现了快速闭环——当日报告、当日即有修复 PR（#91933）；(3) 合并等待队列庞大（49 条），部分 PR 已在数周前提交，合并通道存在一定积压。整体项目活跃度极高，社区贡献者参与广泛。


## 2. 版本发布

### v0.20.5 (v2026.8.19) — Patch Release

- **发布日期：** 2026-08-19
- **性质：** 补丁版本，稳定标签
- **内容：** 滚动收纳自 v0.20.4 以来约 323 个合并 PR，面向下游消费者（Docker 镜像、托管部署、新安装）提供稳定版本锚点。
- **破坏性变更：** 无明确标注。
- **迁移注意事项：** 预期为平滑升级；建议部署前检查 `CHANGELOG` 中有关配置项变动说明（若有）。
- **链接：** [v2026.8.19 Release](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.8.19)


## 3. 项目进展

过去 24 小时内合并/关闭的 PR 数量有限（1 条），重点进展体现在活跃 PR 的持续迭代和架构方向的一致推进上。

### 已合并 PR

| PR | 标题 | 说明 |
|---|---|---|
| [#85373](https://github.com/NousResearch/hermes-agent/pull/85373) | fix(desktop): surface actionable error when Nous Cloud agent returns 503 | 修复桌面端连接 Nous 云 Agent 时后端返回 502/503/504 错误仅显示通用提示、缺乏可操作指引的问题，对应 Issue #85335 |

### 架构主题的持续集中推进

多个高评论数 Issue 在本周保持了活跃更新，集中在**状态可证明性**和**部署一致性**两大主题上。这批架构议题（#90866、#90049、#90144、#90145、#88683、#91230）虽然在 PR 层面尚未看到大规模合并，但其讨论深度和跨组件影响范围表明项目正在向更严谨的可靠性模型收敛——从“正确行为”走向“可证明的正确行为”。


## 4. 社区热点

### 最热 Issue TOP 3（按评论数）

| Issue | 标题 | 评论数 | 状态 |
|---|---|---|---|
| [#78647](https://github.com/NousResearch/hermes-agent/issues/78647) | [COMPLETE] Large-file decomposition: 20/20 done | 78 | CLOSED |
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | [skills-index-watchdog] Skills index is stale or degraded (degraded) | 72 | OPEN |
| [#79564](https://github.com/NousResearch/hermes-agent/issues/79564) | Discord Feature Parity & Alignment Campaign (API v10) — meta-issue | 9 | OPEN |

**热点诉求分析：**

- **#78647（史诗完成）** — god-file 分片史诗（20/20 完成）正式关闭，反映了 2026-08 确立的“god files are sharded, never reverted”长期策略落地。78 条评论说明该重构工程规模大、讨论充分。
- **#66616（技能索引退化）** — 由自动化探针发现 `/docs/api/skills-index.json` 索引已 29.8 小时未更新（阈值 26h），当前状态 `degraded`。72 条评论表明该问题持续受到社区关注，原因可能涉及 CI 工作流不稳定或定期任务中断。
- **#79564（Discord 功能对齐战役）** — meta-issue 持续获得关注，显示社区对 Discord 平台功能完整性的诉求较强。


## 5. Bug 与稳定性

### 高优先级（P1/P2）Bug

| Issue | 标题 | 严重度 | 有无修复 PR |
|---|---|---|---|
| [#91927](https://github.com/NousResearch/hermes-agent/issues/91927) | Session title generation fails with Gemini models due to default thinking tokens consuming max_tokens budget | P2 | **有** — [#91933](https://github.com/NousResearch/hermes-agent/pull/91933) |
| [#89083](https://github.com/NousResearch/hermes-agent/issues/89083) | Desktop: chat window permanently unresponsive after macOS sleep/wake (half-open WebSocket never detected) | P2 | 未标记 |
| [#91675](https://github.com/NousResearch/hermes-agent/issues/91675) | Windows: gateway start prints ✓ then dies after 6s liveness poll | P2 | 未标记 |
| [#91684](https://github.com/NousResearch/hermes-agent/issues/91684) | Desktop approval responds 4001 "session not found" when routed to non-owning local gateway | P2 | 未标记 |
| [#90200](https://github.com/NousResearch/hermes-agent/issues/90200) | GitHub automation split authority: metadata writes succeed while object writes fail (403) | P2 | 未标记 |

**值得关注的稳定性问题：**

- **#88758 / #88740（压缩边界缺陷）** — 关于 durable row-ID watermark 在 replay cleanup、alternation repair、child/CLI/ACP restore 等边界条件下被丢弃的问题。属于会话状态一致性的深层缺陷，修复范围横跨多个子系统。
- **#91916（Python 3.14 兼容性）** — `DaemonThreadPoolExecutor` 因 CPython 3.14 中 `_worker()` 签名变更而崩溃，已标记为重复项并关闭。社区对 Python 3.14 的兼容准备仍然敏感。
- **#91664（安全相关 PR）** — 为桌面端文件 artifact 增加右键“Open Containing Folder”功能，标记了安全边界和 Windows 平台风险。

### 安全相关

- **#91928（NTLM 凭据泄漏修复）** — 文件工具（`read_file`/`write_file`/`patch`）现在拒绝 Windows NT 命名空间路径。移植自 Claude Code v2.1.234 的加固措施，及时且高价值。
- **#77162（密钥脱敏缺失）** — tool-result → provider egress 路径上的精确值密钥脱敏缺失，尚处开放状态。


## 6. 功能请求与路线图信号

### 明确的路线图信号（Architecture / Innovation 类别 Issue）

| Issue | 提议 | 可能合并的 PR |
|---|---|---|
| [#90866](https://github.com/NousResearch/hermes-agent/issues/90866) | 让可观察状态从源头到副作用全程携带证明 | 暂无直接 PR |
| [#90049](https://github.com/NousResearch/hermes-agent/issues/90049) | 将“虚假成功”作为一等缺陷类，引入类型化完成证明 | 暂无直接 PR |
| [#91911](https://github.com/NousResearch/hermes-agent/issues/91911) | Bot Mode 身份/能力/投递/取消统一为单一控制平面 | 暂无直接 PR |
| [#91230](https://github.com/NousResearch/hermes-agent/issues/91230) | 将“精确对象完成验证”确立为 Hermes 第六条法则 | 暂无直接 PR |

### 用户驱动的功能请求

- **#91260（多 profile 多 bot 流水线）** — IM 入口无法驱动真实的多 bot 流水线，用户期待跨 profile 的 SOUL handoff 真正可用。
- **#91740（Bot Mode 会话可浏览性）** — 从 Bots 页签跳转到 Sessions 后，bot 会话全部消失且无处浏览。属于可用性缺口。

### 可能纳入下个版本的功能 PR（基于准备状态判断）

- **#91935（桌面端插件贡献区域）** — 功能完整，当日新开。
- **#91934（浏览器预览关闭按钮）** — 体验改进，改动小，合入门槛低。
- **#73006（Obsidian 显式 vault 选择）** — 功能完整且有向后兼容设计，等待时间较长（7 月 28 日已开）。


## 7. 用户反馈摘要

### 真实痛点与场景

- **macOS 休眠唤醒后聊天窗口永久无响应**（#89083）— 用户描述详实：发消息无响应、无报错、无重试，只能开新窗口或重开应用。对桌面端日常使用影响明显。
- **Windows 网关启动假成功**（#91675）— 打印 ✓ 后 6 秒死亡。用户追踪到 `schtasks /run` 路径，属于 #84185 修复的后续回归。
- **Gemini 标题生成产生乱码**（#91927）— 测试模型 `gemini-2.5-flash`/`gemini-3.6-flash` 时标题被截断为 ````` ```json ```` ```、`{` 等噪声。社区反馈积极，当日即有修复。
- **Gmail 转发邮件正文丢失**（#43054）— 仅返回顶层 MIME 部分，嵌套/转发的邮件内容被丢弃。已开放两个月，仍未见进展。
- **机器人会话在 Sessions 页签中消失**（#91740）— “切换页签后所有 bot 聊天记录消失”，影响日常检索。

### 满意点

- 社区对 **快速响应** 给予了正反馈：Gemini 标题问题当天报告、当天修复 PR 提交。
- **#85373**（云 Agent 503 错误提示优化）获得了正面评价基调，用户期待更可操作的错误信息。


## 8. 待处理积压

### 长期未响应/未合并的重要 PR（>30 天）

| PR | 标题 | 提交日期 | 天数 | 备注 |
|---|---|---|---|---|
| [#54396](https://github.com/NousResearch/hermes-agent/pull/54396) | fix(gateway): prefer systemd scope for timeout check | 2026-06-28 | 55 天 | 有回归测试，标记 blast-moderate |
| [#58146](https://github.com/NousResearch/hermes-agent/pull/58146) | fix: reset auth cooldowns across profiles | 2026-07-04 | 49 天 | 标记 P2 + security 风险，值得优先评审 |
| [#65784](https://github.com/NousResearch/hermes-agent/pull/65784) | fix(disk-cleanup): fail closed across Git and filesystem boundaries | 2026-07-16 | 37 天 | 安全相关，fail-closed 设计 |
| [#73006](https://github.com/NousResearch/hermes-agent/pull/73006) | feat: support explicit Obsidian vault selection | 2026-07-28 | 25 天 | 功能完整，已有测试 |

### 长期未关闭的高评论 Issue

- **#43054（Gmail 嵌套 MIME 丢失）** — 开放 74 天，3 条评论仍无维护者回应。用户等待时间已较长。
- **#66616（技能索引退化）** — 开放 35 天，72 条评论，自动化探针持续标记 `degraded`。此类机器人维护类问题值得专门的流程改进。

### 合并通道积压提醒

当前 49 条待合并 PR 中有多个 **P2 安全/稳定性相关** PR 已等待超过 30 天（#58146、#65784），建议维护者优先安排评审。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-22**  
**数据窗口：2026-08-21 至 2026-08-22**


## 1. 今日速览

PicoClaw 项目今日活跃度中等偏上，过去24小时内共有 **5 项更新**（1 条 Issue + 4 条 PR）。**4 条 PR 全部完成合并/关闭**，无待处理合并请求，合并效率良好。最值得关注的是 **4 条合并 PR 中有 2 条来自 2 月/3 月创建的长期挂起 PR**（#647、#714 等待约 6 个月），表明维护者正在清理历史积压。新 Issue #3342 提出了一个有趣的产品思路——可选的 "轮次结束后转向" 模式，暗示社区对对话中断行为的关注。当前无新版本发布，项目整体处于**稳定迭代 + 积压清理**阶段，健康度良好。


## 2. 版本发布

本日无新版本发布。最近一次版本信息请参考此前发布记录。


## 3. 项目进展

今天合并/关闭了 4 个 PR，覆盖 **工具能力增强** 和 **协议兼容性扩展** 两个方向：

### 3.1 WebFetchTool 文本提取能力增强（#647）— [链接](https://github.com/sipeed/picoclaw/pull/647)

> 状态：✅ 已合并（创建于 2026-02-22，等待约 6 个月）

- **HTML 实体解码**：正确处理 `&amp;`、`&lt;`、`&gt;`、`&quot;` 等编码字符
- **内容结构保持**：为块级元素添加换行符，保证提取文本的可读性
- **影响**：显著提升从网页获取内容的质量，对依赖 WebFetchTool 的 agent 工作流是实质改进

### 3.2 Anthropic 原生 Messages API 协议支持（#1158）— [链接](https://github.com/sipeed/picoclaw/pull/1158)

> 状态：✅ 已合并 | Fixes #269

- 新增 `anthropic-messages` 协议前缀，支持 `/v1/messages` 端点
- **解决了仅支持 Anthropic 原生 API 格式的代理服务无法接入的问题**
- 扩展了项目的 LLM 服务兼容性矩阵

### 3.3 Skills 安装/重装 CLI 重构（#714）— [链接](https://github.com/sipeed/picoclaw/pull/714)

> 状态：✅ 已合并（创建于 2026-02-24，等待约 6 个月）

- 新增 `reinstall` 子命令（强制覆盖）
- 支持 `repo@branch` 语法和可选子路径
- 生产环境安装改用 GitHub Trees API 获取完整目录
- 重复安装时给出错误提示并附带解决建议

### 3.4 AGENTS.md 文档优化（#1182）— [链接](https://github.com/sipeed/picoclaw/pull/1182)

> 状态：✅ 已合并

- 将 AGENTS.md 重构为"原则优先"指南，供 AI Agent 和贡献者参考
- 以 `go.mod` 为 Go 版本唯一事实来源

**总评**：今日合并的 4 个 PR 涵盖工具质量、协议扩展、CLI 体验和文档规范四个维度，项目在**实用性和生态兼容性**上都有实质推进。


## 4. 社区热点

今日唯一的新 Issue **#3342** 尚未产生讨论热度，但值得关注其主题方向——这反映了社区对 **agent 对话中断行为** 的持续关注。

**核心内容回顾**：[Issue #3342](https://github.com/sipeed/picoclaw/issues/3342)

> 当 agent 仍在处理第一个任务时，用户发送第二条消息，当前设计会将其视为"中途修正"——跳过任务 #1 剩余的 tool calls（标记为 "Skipped due to queued user message."），直接注入消息 #2 继续执行。

这一行为虽然灵活，但**可能造成任务 #1 的工作被意外丢弃**。提案希望新增一个可选的 "after-turn" 转向模式：**将 busy 状态下收到的消息排队，待当前轮次完成后再处理**。

**分析**：该 Issue 虽然评论数为 0，但反映了真实使用场景中的痛点——用户在 agent 工作时经常忍不住追加指令，而当前实现可能造成已执行工作的浪费。这类设计讨论对未来版本的用户体验有重要参考价值。


## 5. Bug 与稳定性

今日无新报告的 Bug、崩溃或回归问题。合并的 4 个 PR 中不涉及缺陷修复，均为功能增强和文档优化。需注意 #1158 和 #714 属于较大变更（协议新增 + CLI 重构），建议关注后续是否有回归报告。


## 6. 功能请求与路线图信号

### 新需求

- **[#3342] Opt-in "after-turn" steering mode** — [链接](https://github.com/sipeed/picoclaw/issues/3342)  
  用户请求可选的"轮次结束后转向"模式：在 busy 状态下收到的消息先排队，不打断当前轮次的 tool calls。该功能请求若被采纳，将改善多任务交互体验，对提升用户满意度有较高价值。

### 路线图信号分析

结合今日合并的 PR 和近期动态，以下方向值得关注：

| 方向 | 信号来源 | 可能性评估 |
|------|---------|-----------|
| **协议兼容性扩展** | #1158（Anthropic Messages API）合并 | 高——维护者正在持续扩大 LLM 服务兼容 |
| **交互模式优化** | #3342（after-turn 模式） | 中——需维护者评估设计复杂度与收益 |
| **工具链打磨** | #647（WebFetchTool 改进）、#714（skills CLI 重构） | 高——工具质量和 CLI 体验是持续优化重点 |


## 7. 用户反馈摘要

本日无新增 Issue 评论数据。从 Issue #3342 的描述可提炼的用户痛点：

> **痛点**：agent 处理长任务时，用户追加的消息会导致当前任务被中断，已执行的 tool calls 被标记为跳过，造成工作浪费。这暗示用户**期望更"排队式"的交互模式**，而非一刀切的中断机制。

由于今日无活跃讨论，更多用户反馈请关注后续数据。


## 8. 待处理积压

今日合并了 4 个 PR，其中 2 个为 6 个月以上的长期挂起 PR（#647、#714），**积压清理进展良好**。但仍需关注以下长期未响应事项：

| 编号 | 类型 | 主题 | 创建时间 | 说明 |
|------|------|------|---------|------|
| [#269](https://github.com/sipeed/picoclaw/issues/269) | Issue | Anthropic 原生 API 兼容性 | 早期 | ✅ 已由 PR #1158 解决 |
| — | — | 其他长期挂起 PR | — | 今日无数据，建议维护者定期审视超过 3 个月未响应的 Issue/PR |

**建议**：继续对 3 个月以上未处理的 Issue/PR 进行系统性清理，可参考今日合并 #647 和 #714 的做法，集中排期处理历史积压。


## 总结

| 维度 | 评价 |
|------|------|
| **活跃度** | 中等偏上（5 项更新/24h） |
| **合并效率** | 4/4 PR 全部合并，无积压 |
| **项目健康度** | ⭐⭐⭐⭐（稳定迭代，积压清理中） |
| **风险关注** | 大变更（#1158、#714）需观察回归；#3342 交互改进待评估 |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-22** | **数据窗口：2026-08-21 ~ 2026-08-22**


## 1. 今日速览

NanoClaw 今日活跃度**极高**，24 小时内产生 24 条 PR 更新，集中在 Telegram 多实例支持、Dial 频道修复与 CI 稳定性三大战线。核心团队（`core-team` 标签）贡献了绝大多数 PR，显示项目处于密集迭代期。值得关注的是，`amit-shafnir` 单人提交了 6 个相关联的 PR（#3428/#3435/#3436/#3437/#3438/#3431），围绕 Telegram 命名实例与设置向导展开系统性改造；`zvi-fried` 则主导了 6 个修复类 PR（#3401-#3404/#3424/#3430），聚焦 registry 兼容性与 CI 基础设施。今日合并/关闭 11 个 PR，其中包含 Mattermost 频道集成（#3202）与 attach surface 契约设计（#3429）两个里程碑级成果。唯一的 Issue #3426 指向 `send_card` 按钮被 bridge 静默丢弃的文档误导问题，属于用户体感层面的缺陷。**总体评价：项目健康度良好，迭代节奏快，但 PR 积压（13 个待合并）需关注。**


## 2. 版本发布

**无新版本发布。** 最近一次发布仍为上一周期版本，当前项目处于快速迭代的 pre-release 阶段，多个功能分支正在汇聚。


## 3. 项目进展

今日合并/关闭了 11 个 PR，其中以下几项显著推进了项目能力边界：

| PR | 标题 | 类型 | 意义 |
|----|------|------|------|
| [#3202](https://nanocoai/nanoclaw PR #3202) | **Add Mattermost channel integration** | Feature | **里程碑级**：新增第 N 个聊天平台适配器，沿用 `slack.ts` 模式通过 `registerChannelAdapter` 注册，基于社区 `chat-adapter-mattermost` 封装。Mattermost 与 Slack 同属企业级团队协作工具，这标志着 NanoClaw 在自托管/企业通讯平台的覆盖进一步扩大 |
| [#3429](https://nanocoai/nanoclaw PR #3429) | **feat(drivers): ratify the attach surface — a driver describes its exec argv** | Feature/Contract | 定义 `SessionExecSpec { bin, argsTty, argsPlain }` 契约，让 driver **描述**而非**操作** exec 调用。这是交互式工具附着终端到活跃会话的基础能力，为后续 REPL、调试器等场景铺路 |
| [#3403](https://nanocoai/nanoclaw PR #3403) | **fix(matrix): use a refresh-safe ESM patch** | Fix | Matrix 适配器在 Node 22 下因 extensionless ESM imports 失败，现改为提交 pnpm patch 并在每次安装时自动重放，**彻底解决 Node 22+ 兼容性** |
| [#3424](https://nanocoai/nanoclaw PR #3424) | **ci: test registry-backed skills** | CI | 新增 CI 流程：发现所有从 channels/providers 拉取的 add-* skill，在固定 registry 快照上运行完整构建与测试，**填补了 skill 与 registry 集成测试的空缺** |
| [#3430](https://nanocoai/nanoclaw PR #3430) | **fix: restore stable CI required check** | CI | 修复 Node 版本矩阵导致的 `ci` required check 失效问题，恢复 CI 门禁有效性 |

**整体评估**：今日合并内容覆盖「新平台（Mattermost）+ 架构契约（attach surface）+ 基础设施加固（CI/ESM 补丁）」，是多线并进的实质性推进。


## 4. 社区热点

**今日无高讨论量 Issue/PR**——所有条目评论数为 0 或未标注。但以下 PR 因**关联性**值得关注：

**[#3396](https://nanocoai/nanoclaw PR #3396) + [#3428](https://nanocoai/nanoclaw PR #3428)（模板创建 Agent 的完整链路）**
- #3396 为聊天内 `create_agent` 工具增加 `template` 参数，并新增 `ncl templates list` 只读命令，可浏览本地模板目录或公共注册表索引。
- #3428 是该功能的 Slack 侧配套：Slack 创建流程端到端携带模板引用。PR 自身注释了一个**重要的流程问题**——它取代的 #3397 因「在其声明顺序之前被合并」（实际是 #3397 依赖 #3396 的 trunk 代码，但先于 #3396 被合并）导致在分支上被 revert（ffd9d9b1）。这暴露了**多 PR 依赖合并顺序的管理问题**，值得核心团队注意。

**背后的用户诉求**：企业用户希望在聊天界面直接基于模板/配方创建 Agent，而无需离开对话上下文。该功能若落地，将显著降低 Agent 的创建门槛。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 描述 | 状态 |
|--------|------|------|
| 🔴 **功能误导（High）** | **[Issue #3426](https://nanocoai/nanoclaw Issue #3426)**：`send_card` 文档承诺支持 `actions`（按钮），但 bridge 自 #2265 起丢弃所有无 `url` 的 action。Agent 看到按钮消失、读取 `fallbackText`（"for platforms without card support"）后，**错误地将责任归咎于平台**——实际是 bridge 层静默丢弃。文档与实现不一致，且误导 Agent 做出错误诊断 | **OPEN**，暂无 fix PR。属于「文档-实现脱节」类问题，且是 AI 行为误导，建议优先处理 |
| 🟠 **行为缺陷（Medium）** | **[PR #3434](https://nanocoai/nanoclaw PR #3434)**：轮询类适配器不应打开 webhook 服务器，但当前行为相反 | 已有 fix PR（#3434，待合并） |
| 🟠 **用户体验（Medium）** | **[PR #3431](https://nanocoai/nanoclaw PR #3431)**：Telegram 设置向导中配对卡片显示 6 位数字，但实际配对码位数不一致 | 已有 fix PR（#3431，待合并） |
| 🟡 **兼容性（Low-Medium）** | **[PR #3403](https://nanocoai/nanoclaw PR #3403)**：Matrix 适配器在 Node 22 下因 ESM 导入格式失败 | 已合并 ✅ |
| 🟡 **消息 ID 错误（Medium）** | **[PR #3287](https://nanocoai/nanoclaw PR #3287)**：`getMessageIdBySeq()` 返回 `messages_in.id` 原值，但该值**并非**平台消息 ID（需剥离 agent-group 后缀），导致消息 ID 语义错误 | 待合并（8/17 创建，仍在开放） |

**观察**：今日修复集中在「渠道适配器行为一致性」与「CI 基础设施」，但 #3426 作为用户可感知的 AI 误导问题，建议提升优先级。


## 6. 功能请求与路线图信号

今日无新功能请求 Issue，但从 PR 中可辨识出清晰的路线图信号：

| 信号 | 来源 | 可能性判断 |
|------|------|-----------|
| **Telegram 多实例支持**（`TELEGRAM_INSTANCES` 环境变量 + 实例绑定配对） | [#3436](https://nanocoai/nanoclaw PR #3436) + [#3435](https://nanocoai/nanoclaw PR #3435) + [#3438](https://nanocoai/nanoclaw PR #3438) + [#3437](https://nanocoai/nanoclaw PR #3437) | **高**——4 个 PR 构成完整功能集，且 amit-shafnir 连续操作，预计下一版本落地 |
| **聊天内基于模板创建 Agent** | [#3396](https://nanocoai/nanoclaw PR #3396) + [#3428](https://nanocoai/nanoclaw PR #3428) | **高**——双端（核心+Slack）已实现 |
| **Driver 描述 exec argv（attach surface）** | [#3429](https://nanocoai/nanoclaw PR #3429) 已合并 | 已落地，后续交互式工具可依赖此契约 |
| **Registry 集成测试规范化** | [#3424](https://nanocoai/nanoclaw PR #3424) 已合并 | 已落地，为 skill 生态质量兜底 |


## 7. 用户反馈摘要

今日唯一 Issue **#3426**（[链接](https://nanocoai/nanoclaw Issue #3426)）蕴含了丰富的真实用户痛点：

- **关键痛点**：Agent 依赖 `fallbackText` 来诊断平台能力，但该文本是「平台不支持卡片」的通用提示，与「bridge 丢弃按钮」的实际情况不符。用户看到的是：Agent 说「平台无法渲染按钮」，但实际是 NanoClaw 的 bridge 层静默过滤了无 `url` 的 action。
- **深层诉求**：用户希望 **bridge 层的转换行为对 Agent 透明**，至少应通过某种机制（如修改 `fallbackText` 内容或提供降级提示）让 Agent 能区分「平台不支持」与「bridge 丢弃」。当前的静默行为导致 AI 产生**错误的因果推理**，进而给出误导用户的结论。
- **间接反馈**：该 Issue 同时反映 `send_card` 的文档承诺与实际能力不符，用户在文档-实现不一致时处于被动。

**建议**：核心团队应评估是否在 bridge 层对无 `url` action 的丢弃行为增加显性信号（例如在传递给 Agent 的 metadata 中标注丢弃原因），或在文档中明确说明该限制。


## 8. 待处理积压

以下 PR/Issue 已开放较长时间，建议维护者关注：

| 条目 | 创建时间 | 状态 | 说明 |
|------|----------|------|------|
| [PR #3287](https://nanocoai/nanoclaw PR #3287) | 2026-08-17（5 天） | OPEN | 修复 message ID 语义错误（需剥离 agent-group 后缀）。已关联 Issue #3153，但 5 天未合并，可能阻塞下游依赖 |
| [PR #3396](https://nanocoai/nanoclaw PR #3396) | 2026-08-20（2 天） | OPEN | 聊天内模板创建 Agent（核心功能）。**注意**：其配套 PR #3428 指出 #3397 曾因「依赖 #3396 却先被合并」导致 revert，说明该 PR 的合并顺序敏感，建议尽快审核以免连锁问题 |
| [Issue #3426](https://nanocoai/nanoclaw Issue #3426) | 2026-08-21（1 天） | OPEN | `send_card` 按钮被静默丢弃且文档误导 Agent 归因平台。暂无 fix PR，且影响 AI 行为正确性，建议在下一迭代安排 |


## 附：项目健康度快速评估

| 维度 | 状态 | 说明 |
|------|------|------|
| 迭代速度 | 🟢 极快 | 24 小时 24 条 PR，核心团队全天候活跃 |
| 合并/关闭比 | 🟡 中 | 11/24 合并或关闭，待合并积压 13 个——需关注 backlog 累积 |
| 协调性 | 🟡 需关注 | #3397 依赖顺序失误导致 revert 的流程问题；#3429 与 #3432 同属 Dial 相关但分散在多人手中 |
| 用户反馈响应 | 🟡 中等 | Issue #3426 尚无 assignee 或 fix PR，但间隔仅 1 天，仍在合理窗口内 |
| 架构演进 | 🟢 健康 | attach surface 契约（#3429）、driver exec argv 描述化，均为支撑后续交互式能力的基础设计 |

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-22

## 今日速览

项目今日活跃度处于**低位**。过去24小时内无新 Issue 开启或关闭，也无可合并的 PR 或版本发布，整体处于平稳沉寂期。唯一的动静是 #990 提交了一条新 PR，将 Eden AI 加入 OpenAI 兼容网关提供商列表。该 PR 本身不包含新代码逻辑，而是复用已有的 `OpenAiCompatibleProvider` 基础设施，属于配置扩展型变更，风险较低。由于今日无合并、无关闭、无新版本，项目核心代码库保持稳定，但社区互动也相对冷淡，暂无需要紧急处理的事项。

---

## 项目进展

今日**无 PR 被合并或关闭**，核心代码库无新增提交进入主干。唯一进展是 #990 的提交，为项目新增一个可通过统一网关访问的第三方提供商选项，但尚未并入主分支。

---

## 社区热点

今日唯一活跃的 PR 是 **#990**，由 MVS-source 于 2026-08-21 提交：

- **#990** [OPEN] feat(providers): add Eden AI as an OpenAI-compatible gateway — [链接](https://github.com/nullclaw/nullclaw/pull/990)

该 PR 的核心动因是用户希望通过**单一 API Key 访问多个上游供应商**，同时要求服务商位于**欧盟境内**以满足数据驻留合规要求。Eden AI 作为网关服务，恰好同时满足这两个条件。该 PR 明确引用 #922（NEAR AI Cloud 与 Atlas Cloud 的接入）作为模板，说明这是一种**模式化扩展**，社区已存在多起类似需求。目前评论数与讨论热度均为 0，尚未引发广泛讨论。

---

## Bug 与稳定性

今日**无新报告的 Bug、崩溃或回归问题**。

---

## 功能请求与路线图信号

- **多供应商网关接入** — #990 延续了 #922 开启的“以 OpenAI 兼容层接入第三方网关”模式，暗示项目正在将提供商生态从单一内置实现向“插件化/网关化”演进。用户对 **欧盟合规** 与 **一 Key 多服务** 的需求若持续增加，未来可能推动更多区域性网关接入，甚至影响路线图决策。

---

## 用户反馈摘要

今日无新增 Issue 评论。从 #990 的提交说明中可提炼的用户诉求为：

- **合规诉求**：用户明确关注服务商的**数据驻留地（欧盟）**，表明在 AI 工具链选型中，GDPR 等法规合规已成为硬性约束，而非可选加分项。
- **体验诉求**：希望用**一个 API Key 统一路由到各类上游模型供应商**，降低密钥管理与切换成本。

---

## 待处理积压

以下为长期未获维护者回应的 PR，建议关注：

- **#990** — 无人 review、无 maintainer 响应，虽非核心变更，但搁置时间越长，与主分支冲突的风险越高。建议维护者明确并快速评估。

> 注：当前仓库其余 Issue/PR 队列未见其他长期未响应的阻塞性事项；整体积压压力较小。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-22

**数据窗口**：2026-08-21 至 2026-08-22（24h）

---

## 1. 今日速览

IronClaw 今日活跃度显著提升，核心贡献者 henrypark133 与 serrrfirat 主导的 "CI expedite"（T1-T4）系列与 sandbox 凭据中介工作构成了主要进展——四项 CI 基础设施追踪 Issue（#7798-#7801）在同一日内全部创建并配套了对应 PR（#7809）。项目同时完成了两条 1.3 分支的 forward-port 修复（IRONCLAW_REBORN_WORKSPACE_ROOT 环境变量与 clippy 1.98 lint 修复），两条 PR 均已合入。sandbox 的 GitHub CLI 凭据中介功能经历了三轮迭代（#7805-#7807 连续被关闭后，#7810 以扩大范围重新打开），反映出该功能为高风险高迭代区域。社区侧，WebUI 设计系统（Storybook + design-system catalog）与通知中心收件箱化两条长期线路持续向纵深推进。总体健康度良好：24 小时内 4 个 Issue 被关闭、16 个 PR 合入/关闭，CI 基础设施的改善将直接降低后续所有 PR 的等待时间与回归风险。

---

## 2. 版本发布

过去 24 小时无新版本发布。

值得注意的是，两条 forward-port 修复（#7804、#7805）已合入 `release/2026-08-17` 分支，该分支当前的 lint 阻塞问题已解除，预计近期会有补丁版本发布。

---

## 3. 项目进展

### 今日合并/关闭的重要 PR：

| PR | 内容 | 影响 |
|---|---|---|
| [#7804](https://github.com/nearai/ironclaw/pull/7804) | **fix(workspace)**：将 `IRONCLAW_REBORN_WORKSPACE_ROOT` 环境变量覆盖 forward-port 至 1.3 版本 | 修复了 1.3 分支上重定向 workspace 根目录失效的回归 |
| [#7805](https://github.com/nearai/ironclaw/pull/7805) | **fix(ci)**：将 clippy 1.98 lint 修复 forward-port 至 1.3 分支 | 解除了 `release/2026-08-17` 分支所有 PR 的 CI 阻塞（此前所有 PR 都因 `chunks_exact` 报错失败） |
| [#7797](https://github.com/nearai/ironclaw/pull/7797) | **docs(guidance)**：整个仓库的 agent-guidance 审计——修复漂移、精简 21.5k 行、将测试统一到 AGENTS.md 约定 | 由 13 个并行审计器执行，是项目文档与 AI 协作基础设施的重大清理 |
| [#7803](https://github.com/nearai/ironclaw/pull/7803) | **fix(telegram)**：保持配对生成的 Telegram 机器人活跃，即使缺少个人设备凭据时 | 修复了个人设备凭据缺失时配对机器人的可用性问题 |
| [#7796](https://github.com/nearai/ironclaw/pull/7796) | **fix(sandbox)**：失败的 Railway 审计追加操作现在保留暂存的捕获与代理以便重试 | 沙箱审计可靠性增强 |

### 关键推进方向：

- **CI 基础设施重构**：T1-T4 四个追踪 Issue（[#7798](https://github.com/nearai/ironclaw/issues/7798)、[#7799](https://github.com/nearai/ironclaw/issues/7799)、[#7800](https://github.com/nearai/ironclaw/issues/7800)、[#7801](https://github.com/nearai/ironclaw/issues/7801)）定义了 setup-rust 复合操作、nextest 流水线、PR/队列收敛、canonical preflight 四个方面的改造。其中 T4 的 PR [#7809](https://github.com/nearai/ironclaw/pull/7809) 已实现 `preflight-gates.sh` 作为唯一权威门禁列表，预计将大幅减少 CI 与本地 pre-push 钩子的偏差。

- **sandbox 凭据中介**：三个连续版本的 PR（#7805→#7806→#7807→#7810）逐步将 GitHub CLI 凭据管理引入沙箱进程路径。最新版 #7810 扩大了范围，包含 per-user 托管出口与调用归因，是 sandbox 安全性的一次重大升级。

- **通知中心收件箱化**：[#7699](https://github.com/nearai/ironclaw/pull/7699)（已合入）将审批、鉴权、阻塞运行事件推入持久化用户收件箱；[#7700](https://github.com/nearai/ironclaw/pull/7700)（待合并）则从 Process Journal 推导运行最终结论，两条配合将完整替代现有仅限审批的提醒机制。

---

## 4. 社区热点

### 今日讨论最活跃的议题

| 议题 | 评论数 | 关注点 |
|---|---|---|
| [#7801](https://github.com/nearai/ironclaw/issues/7801) CI expedite T4: canonical preflight | 3 | CI 门禁的权威化与 worktree-safe hooks 设计 |
| [#7799](https://github.com/nearai/ironclaw/issues/7799) CI expedite T2: nextest pipeline | 3 | 测试架构从顺序执行到并行化的迁移，以及失败信号的完整性改进 |
| [#7798](https://github.com/nearai/ironclaw/issues/7798) CI expedite T1: setup-rust composite | 2 | 将 43 处散落的 rust-toolchain 调用收敛为一个复合操作 |

**背后诉求分析**：这四条 Issue 全部由核心贡献者 henrypark133 在同一天创建，且每条都配有对应的实现 PR。社区的讨论集中在具体的实现方案与层间交互设计（preflight 门禁的分层策略、nextest 的 JUnit 失败汇总等），而非方向性争论——说明 CI 改造的总体路线已获认可，讨论重点落在如何把方案落到代码上。这是典型的"由设计共识导致的实施密集期"信号。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 |
|---|---|---|
| **中** | [#7783](https://github.com/nearai/ironclaw/issues/7783) LLM 超时策略缺陷：structured-output 最终化使用**非流式** HTTP 客户端，一次传输停摆会先吃掉 60 秒总墙钟预算，再被外层 75 秒终结时间杀死——重试预算根本无法适配截止期限 | **已关闭** |
| **中** | [#7808](https://github.com/nearai/ironclaw/issues/7808) 内存写入路径缺陷：在**任何**外部内存 provider 绑定之前，写入路径需要先实现 redaction + taint 元数据——目前`按原样`输出对话内容（含可能敏感内容） | **打开中**，是 #7664（可插拔内存）的前置阻塞项 |
| **低** | [#7715](https://github.com/nearai/ironclaw/issues/7715) Telegram 连接流程缺乏 bot 与个人账号之间的同意/选择机制（QA bug，Railway 实例） | **已关闭** |
| **低** | [#7805](https://github.com/nearai/ironclaw/pull/7805) `release/2026-08-17` 分支所有 PR 因 clippy 1.98 的 `chunks_exact` lint 失败（已 forward-port 修复） | **已修复** |

**值得注意**：中风险 #7783 被关闭但Issue 列表显示其被关闭时评论数为 1——计划中应有配套的修复 PR。建议维护者确认该修复是否已落地。

---

## 6. 功能请求与路线图信号

| 功能 | 对应 Issue/PR | 状态分析 |
|---|---|---|
| **可插拔内存（Mnesis 为首个消费者）** | [#7664](https://github.com/nearai/ironclaw/issues/7664) / PR #7661（草稿） | 追踪中。[#7808](https://github.com/nearai/ironclaw/issues/7808) 刚被提出作为其前置条件（redaction + taint 元数据）。策略决策已记录于 8/21。**预计：进入下一版本的可能性高**，但需先解决写路径安全问题 |
| **WebUI 设计系统（Storybook + catalog）** | [#7257](https://github.com/nearai/ironclaw/pull/7257) / [#7750](https://github.com/nearai/ironclaw/pull/7750) | 各自是 Phase 1 的不同部分（#7257 为纯文档提案，#7750 为实际集成）。#7750 已在 main 上重建，序列化状态干净。**预计：可能进入下一版本** |
| **用户收件箱（durable inbox）** | Epic [#7687](https://github.com/nearai/ironclaw/issues/7687) / PR #7699（已合入）+ #7700（打开） | 服务端已就绪并合入，客户端消费 PR 待合并。**预计：下一版本大概率包含** |
| **OOBE 建议始终开启** | [#7802](https://github.com/nearai/ironclaw/pull/7802) | 移除环境变量开关，改为默认挂载。简化配置面。**预计：将在近期合入** |
| **Xquik hosted MCP 绑定** | [#7811](https://github.com/nearai/ironclaw/pull/7811) | 由新贡献者 kriptoburak 提交，以 OAuth 2.1 + PKCE 替代浏览器 cookie 方式获取 Twitter/X 数据。**预计：作为扩展包纳入当前版本，非主线功能** |

---

## 7. 用户反馈摘要

今日无新增的用户体验评论，从已有数据可提炼出以下持续存在的用户痛点：

1. **LLM provider 传输停摆的"静默失败"**（#7783）：结构化输出最终化的非流式请求在 stall 时无中间信号，用户直到 60-75 秒后才会感知到失败——这在交互式场景中会使用户感觉"卡死"。

2. **外部内存绑定的隐私缺口**（#7808）：用户（以及维护者）对于把对话原样发送给第三方内存 provider 存在顾虑——需要先有 redaction 能力才能安心启用该功能。

3. **Telegram 个人账号与 bot 的混淆**（#7715）：连接流程中用户无法选择连接模式，且不清楚自己连接的是哪个账号——已在合入的修复（#7803）中缓解，但仍在跟踪中。

4. **CI 排队等待时间长**：多个 PR 标题中出现 "unthrottle"、"queuetime" 等词汇，以及 T2 的 `max-parallel` 解除节流计划，说明当前 PR 合并排队等待已成为社区的普遍痛点。

---

## 8. 待处理积压

| 类别 | 项目 | 等待天数 | 状态说明 |
|---|---|---|---|
| **PR** | [#7456](https://github.com/nearai/ironclaw/pull/7456) fix(reborn): durable storage profile-agnostic | 12 天 | 核心重构 PR，将 Reborn 配置文件根目录改为 profile-agnostic——涉及存储布局变更，需要仔细评审。已有持续更新 |
| **PR** | [#7491](https://github.com/nearai/ironclaw/pull/7491) feat(coding): omp core-tool contract | 11 天 | 将编码工具统一为 6 个精确名称（`read`/`write`/`edit`/`glob`/`grep`/`bash`），移除旧工具面。核心工具契约变更，影响面大 |
| **PR** | [#7700](https://github.com/nearai/ironclaw/pull/7700) feat(notifications): publish authoritative run outcomes | 5 天 | 与已合入的 #7699 配套，等待合并 |
| **Issue** | [#7687](https://github.com/nearai/ironclaw/issues/7687) [epic] 通知中心→durable user inbox | 5 天 | 前端完成，PR #7699 已合入，等待 #7700 后关闭 |
| **Issue** | [#7664](https://github.com/nearai/ironclaw/issues/7664) 可插拔内存（Mnesis） | 8 天 | 等待 #7661（provider crate）与 #7808（redaction 前置）解决后推进 |
| **PR** | [#7516](https://github.com/nearai/ironclaw/pull/7516) feat(webui): operator surface for IronHub agent link | 10 天 | 由外部贡献者 neo-sky 提交（亦是 Mnesis 作者），需要更多 reviewer 关注 |

**维护者提醒**：#7456 与 #7491 两个 XL PR 等待时间已超 10 天且持续更新——它们分别触及存储布局与编码工具契约，建议排期深入评审。另注意 #7516 与 #7664 的作者同为外部贡献者 neo-sky，其提交质量较高，建议给予及时反馈以维持社区参与度。

---

**项目健康度综合评估**：CI 基础设施的主动重构、分支问题的快速 forward-port、以及外部贡献者的持续参与表明项目生态良好。当前的主要风险点在于两个超 10 天的 XL 核心重构 PR（#7456、#7491）——它们既是路线图的关键节点，也是评审瓶颈。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-22

## 1. 今日速览

今日项目热度较高，共处理 15 项事务（2 个 Issue 关闭 + 12 个 PR 合并/关闭 + 1 个 PR 待合并）。核心里程碑为 `release/2026.8.21` 分支合并进 main，标志着包含 DeepSeek Harness (DSH) 0.1.1-rc.1 运行时升级、Windows 集成可靠性改进和匿名分析埋点的新版本正式发布。与此同时，四项自 4 月以来因社区贡献的 PR（定时任务排序、IM 会话重建、Cowork 性能优化等）在停滞数月后于今日被统一合入，极大消减了技术债。此外，资料库（Library）模块的多项体验优化与国际化修复也在今日完成合入。仅剩一条关于定时任务"不通知"投递模式的 PR 仍处于待合并状态，等待维护者推进。

- 活跃度：**高**（24小时内15项事务处理）
- 项目健康度：**良好**（长期积压 PR 清理效果显著，但遗留的开放 PR 需尽快处理）


## 2. 版本发布

**今日无新版本发布。**

但 PR #2519 (`Release: 2026.8.21`) 已将 `release/2026.8.21` 分支合并至 main，实际交付内容包括：

- **DSH 运行时升级**：DeepSeek Harness 更新至 `0.1.1-rc.1`
- **Windows 集成可靠性改进**
- **隐私友好的分析埋点**：DSH 启用开关与工作台使用情况分析

⚠️ 破坏性变更/迁移注意：新版引入了 renderer 侧的分析事件上报服务（`src/renderer/services/dshAnalytics.ts`），若您基于 IPC 层的 DSH analytics 事件自行封装了埋点逻辑，需将此部分迁移至 renderer 侧新服务，原 `src/main/ipcHandlers/dsh/analytics.ts` 中的相关逻辑已被移除。详见 PR #2518。


## 3. 项目进展

### 今日核心推进

**🎉 长期积压 PR 集中清理（4 月至 8 月）**

| PR | 说明 |
|---|---|
| [#1215](https://github.com/netease-youdao/LobsterAI/pull/1215) | 修复 IM `setConfig` 时聊天处理器未重建、平台凭据保存不生效的问题 |
| [#1218](https://github.com/netease-youdao/LobsterAI/pull/1218) | 重构定时任务列表排序规则，解决新建任务随机插入列表中间的问题 |
| [#1219](https://github.com/netease-youdao/LobsterAI/pull/1219) | 消除 Cowork 会话列表与详情页在流式输出时的无效重渲染（React.memo + 合并 useSelector） |
| [#1220](https://github.com/netease-youdao/LobsterAI/pull/1220) | 消除 `recentChats`/`conversationSearch` 的 N+1 查询问题 |

> 这四条 PR 均于 2026-04-01 前后创建，经约 4 个半月后集中合入，说明项目维护节奏正在提速，社区贡献得到了有效吸收。对用户而言，**定时任务排序**和**聊天性能**将获得可感知的提升。

**📦 Library 资料库体验优化（今日重点）**

- [#2514](https://github.com/netease-youdao/LobsterAI/pull/2514)：优化本地产物预览弹窗、区分空态与筛选无结果态、搜索框一键清空、修复发布额度弹窗占位符重复替换问题
- [#2517](https://github.com/netease-youdao/LobsterAI/pull/2517)：完善文件分享与收藏交互——分享时保留 Unicode 文件名、收藏状态即时更新与失败回滚、统一额度限制弹窗样式

**📊 DSH 相关（随 8.21 版本交付）**

- [#2515](https://github.com/netease-youdao/LobsterAI/pull/2515)：为 DSH 启用开关和工作台打开事件增加使用分析
- [#2516](https://github.com/netease-youdao/LobsterAI/pull/2516)：更新 DSH 依赖至 `0.1.1-rc.1`
- [#2518](https://github.com/netease-youdao/LobsterAI/pull/2518) 与 #2515 配合，将分析事件上报移至 renderer 侧

**🌐 i18n & UX 修复**

- [#1224](https://github.com/netease-youdao/LobsterAI/pull/1224)：修复 `CoworkPromptInput` 硬编码中文（`'输入文件'` → `i18nService.t()`）、Agent 弹窗新增 Escape 关闭、删除操作防重复点击，关闭 Issue [#1223](https://github.com/netease-youdao/LobsterAI/issues/1223)


## 4. 社区热点

今日活跃讨论的 Issue 有限，但有两条已关闭的 Issue 反映出社区的集中诉求：

| Issue / PR | 讨论热度 | 核心诉求 |
|---|---|---|
| [#1217](https://github.com/netease-youdao/LobsterAI/issues/1217)（Bug：偶发重启网关，2 条评论） | 用户报告 Windows 环境下每天 3-5 次间歇性网关重启，已附带完整日志（`lobsterai-logs-20260401-180401.zip`）。此问题已关闭（stale），未标记已修复，**需求未充分满足**。 |
| [#1223](https://github.com/netease-youdao/LobsterAI/issues/1223)（i18n 硬编码 + Agent 弹窗 UX，2 条评论） | 用户深入使用后发现中文硬编码污染了英文提示词，同时建议弹窗补上 Escape 关闭和防重复点击，已通过 [#1224](https://github.com/netease-youdao/LobsterAI/pull/1224) 完整修复。 |

**诉求分析**：i18n 与多语言体验是目前用户关注的焦点之一，好在相关修复已落地。


## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 |
|---|---|---|
| 🟠 中 | [#1217](https://github.com/netease-youdao/LobsterAI/issues/1217)：Windows 下每天 3-5 次**偶发网关重启**（时间集中在 18:00 前后；版本 2026.3.26） | 已关闭（stale），**未见关联 fix PR**，建议维护者关注是否存在已知问题或需用户验证新版是否已修复 |
| 🟢 低 | [#1223](https://github.com/netease-youdao/LobsterAI/issues/1223)：i18n 硬编码 + 弹窗交互缺陷（三条子问题） | ✅ 已由 [#1224](https://github.com/netease-youdao/LobsterAI/pull/1224) 修复并合入 |


## 6. 功能请求与路线图信号

- **DSH 使用分析（已落地）**：PR #2515/#2518 表明 8.21 版本已为 DSH 启用开关和工作台打开增加匿名分析埋点。参考通用惯例，下一阶段大概率会补充功能使用率看板（如 `view_dsh_workbench` 成功/失败错误码追踪）。
- **本地产物管理精简**：PR #2514 移除了资料库删除文件及相关任务入口，倾向将本地产物操作收敛为“预览 + 打开”，产品定位更聚焦，跨平台一致性会更好。
- **Unicode 文件名增强**：PR #2517 为分享打包加入了 Unicode 文件名保留（仅替换不安全字符），考虑了多语言/跨平台场景，是国际化方向的持续投入。


## 7. 用户反馈摘要

- 一位 Windows 10 用户提交了大量日志（`lobsterai-logs-20260401-180401.zip`），报告偶发网关重启影响日常使用，**提供了完整的复现概率与版本信息**，但响应与修复状态不明确，这类对稳定性有直接影响的反馈值得进一步跟进。
- 英文用户（MaoQianTu）明确指出了硬编码中文对提示词的污染问题，说明**国际化/本地化已进入真实用户使用场景**。同时其主动为弹窗交互（Escape 关闭、防重复点击）补充了改进建议，并通过 PR 自行实现，是高质量的社区贡献。


## 8. 待处理积压

**⏳ 待合并 PR（1 条）**

- [#1550](https://github.com/netease-youdao/LobsterAI/pull/1550)（自 2026-04-07 起待合并，已 4.5 个月）：定时任务投递模式为"不通知"时，去除发送给网关的 `channel`/`to` 字段。该 PR 解决了通过会话/IM 创建的定时任务在触发执行时网关报 `"Channel is required when multiple channels are configured"` 的问题，而 UI 手动创建的任务则正常。根因清晰（两条创建路径构建 delivery 对象的方式不同），风险可控。**鉴于今日其他长期积压 PR 已全部合入，建议尽快评估并合并此 PR，彻底清理历史遗留。**

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 开源项目动态日报

**日期：2026-08-22 | 数据窗口：2026-08-21 至 2026-08-22**

---

## 1. 今日速览

Moltis 项目保持中等偏上的活跃度。过去 24 小时内共有 10 项互动（2 个 Issue，8 个 PR），全部为 8 月 20-21 日间新开或更新，说明社区贡献节奏稳定。值得注意的信号：**“活跃时段（active_hours）配置不生效”的小集群问题**（Issue #1223 + PR #1208）正在被系统性地修复，这表明维护者与用户对定时调度能力有实质需求。此外，WhatsApp 集成和浏览器隐身模式（Obscura stealth）均有功能改进被提交——修复型 PR 占比高、新增功能型 PR 占比低，说明项目当前处于**稳定收敛阶段**。无新版本发布。

---

## 2. 版本发布

无新版本发布（最新 Release 日期未知）。当前所有变更仍在 `main` 分支积累，预计近期会有一次小版本发布以汇集上述修复。

---

## 3. 项目进展

过去 24 小时**合并/关闭的 PR 较少（仅 1 个）**，主要进展体现在新提交的 PR 上：

| PR | 状态 | 作用域 | 说明 |
|---|---|---|---|
| [#1220](https://github.com/moltis-org/moltis/pull/1220) | ✅ 已合并 | WhatsApp | **Markdown 转 WhatsApp 原生格式**：出站消息自动转换格式，保留原始 Markdown 在会话历史和 Web UI 中。对重度使用 WhatsApp 通道的用户体验提升明显。 |
| [#1228](https://github.com/moltis-org/moltis/pull/1228) | 🟡 待合并 | WhatsApp | **入站文件持久化**：下载入站文档/照片到本地会话媒体接口，为本地工具提供稳定的 `local_path`（20 MB 限制，无额外依赖）。修复了仅暴露文件名/MIME 元数据的痛点。 |
| [#1227](https://github.com/moltis-org/moltis/pull/1227) | 🟡 待合并 | Browser | **Obscura 隐身模式默认开启**：新增 `tools.browser.obscura_stealth` 配置项（默认 `true`），提升浏览器工具的隐私默认值。 |
| [#1226](https://github.com/moltis-org/moltis/pull/1226) | 🟡 待合并 | Cron | **定时任务输出回传**：将定时任务的输出投递到触发该任务的原始聊天中，而非固定地址。大幅改善定事情报推送场景的可用性。 |
| [#1225](https://github.com/moltis-org/moltis/pull/1225) | 🟡 待合并 | i18n | **繁体中文（zh-TW）全面优化**：重构 `connectors.ts`，统一术语并补全缺失翻译。 |

**整体判断**：项目正在稳步推进“对话助手实际落地”所需的基础设施——WhatsApp 双向文件流转（#1228）、定时任务结果回传（#1226）、出站消息格式兼容（#1220），这些都是真实用户高频诉求。

---

## 4. 社区热点

今日并无评论数或反应数较高的“爆款”Issue/PR，但有两个值得关注的信号：

**[Issue #1223](https://github.com/moltis-org/moltis/issues/1223) — heartbeat active_hours 配置对默认配置无效**

- 由 `Lstarsky0` 提交，详细分析了 `ActiveHoursConfig` 默认值（`08:00`–`24:00`）的语法与实际语义的冲突（`end: "24:00"` 被解析后永远过滤不了任何时段）。
- 该 Issue 与 [PR #1208](https://github.com/moltis-org/moltis/pull/1208) 直接相关（PR 声明 Closes #1205，但实际覆盖了本次报告的所有 active_hours 问题）。说明社区用户**确实在使用心跳/定时功能时遇到了配置失效**，且已有对应修复，值得关注合并进度。

**[PR #1220](https://github.com/moltis-org/moltis/pull/1220)（已合并）— WhatsApp Markdown 渲染**

- 虽无大量显式反应，但这是当天唯一被合并的 PR，侧面说明 WhatsApp 通道体验是当前迭代主线之一。用户场景：模型生成的内容无法在 WhatsApp 端正确换行/加粗。

---

## 5. Bug 与稳定性

今日报告的 Bug 数量较少（2 个），按严重程度排列：

| 严重度 | Issue | 问题描述 | Fix PR 状态 |
|---|---|---|---|
| 🔴 高 | [#1224](https://github.com/moltis-org/moltis/issues/1224) | **共享 Slack 频道中工具停止工作**（Tools stop working in shared Slack channels） | ❌ 暂无对应 PR |
| 🟡 中 | [#1223](https://github.com/moltis-org/moltis/issues/1223) | **active_hours 配置无效**：默认配置永不抑制任何时段；用户设置 `end: "24:00"` 同样失效 — `is_within_active_hours` 先解析 `end` 再做特判，逻辑顺序有问题 | ✅ [PR #1208](https://github.com/moltis-org/moltis/pull/1208) 已提交待合并 |

> ⚠️ **重点关注 #1224**：共享频道是 Slack 企业用户的常见使用场景（多团队共用频道），工具失效意味着核心 Agent 能力在多人协作环境中完全不可用。目前尚无补丁，建议维护者优先排查通道权限获取逻辑。

---

## 6. 功能请求与路线图信号

今日没有独立的 Feature Request Issue，但可以从 PR 中提炼以下路线图信号：

| 信号 | 来源 | 方向判断 |
|---|---|---|
| **WhatsApp 入站文件持久化**（#1228） | PR | 强化 WhatsApp 作为完整 AI 助手通道的能力，补全媒体流转闭环 |
| **定时任务结果回传至原始聊天**（#1226） | PR | 围绕 “cron 触发的 Agent 任务” 完善回传语义，疑似为“定时投递摘要/周报”场景铺路 |
| **Obscura 隐身模式默认开启**（#1227） | PR | 默认安全/隐身会成为项目共识，不排除后续对所有工具通道统一默认隐私保护 |
| **Windows 支持（shell hooks 使用 cmd.exe）**（[PR #468](https://github.com/moltis-org/moltis/pull/468)） | 长期 PR | Windows 原生支持是持续积压需求，建议维护者评估是否纳入下一里程碑 |

---

## 7. 用户反馈摘要

基于 Issue 正文提炼：

- **配置文档与实际行为不一致**（#1223）：用户仔细阅读了文档（“midnight = always on until end of day”），照做后发现不生效。此类文档-实现偏差问题会消耗用户信任。
- **共享频道工具失效**（#1224）：用户先行搜索了已有 issue 并确认未报告过，且声明使用最新版，行为规范。预期该用户对项目后续跟进速度有较高期待。
- **WhatsApp 文件处理细节**（#1228 PR 的动机）：此前本地工具只能拿到文件名/MIME 而拿不到文件内容，严重限制了基于文件的 Agent 能力，社区有明确诉求。

整体用户情绪：**积极贡献者居多**——2 个 Issue 中 1 个附带了详细分析（#1223），PR 提交者有多位老面孔（rubenssoto 三天内提交 4 个 PR），表明核心贡献者社区活跃、有归属感。

---

## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 最后更新时间 | 备注 |
|---|---|---|---|---|
| [PR #468](https://github.com/moltis-org/moltis/pull/468) — Windows shell hooks | PR | 2026-03-23 | 2026-08-21 | **积压近 5 个月**（共 152 天），作者已实测通过（Windows 10 + v0.9.10），CI 通过。期间有多次更新，属于“可用但未合并”状态。建议维护者明确回应是否纳入路线图。 |
| [Issue #1224](https://github.com/moltis-org/moltis/issues/1224) — 共享 Slack 频道工具失效 | Bug | 2026-08-21 | 2026-08-21 | 高严重度但尚无响应，建议 48 小时内至少给一个 triage 意见。 |

> 另外提醒：PR #1208（active_hours 修复）与 Issue #1223 互动密切，建议尽快合并并关联关闭，避免形成双份工作。

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，面向维护者与社区贡献者，仅供参考。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据 CoPaw 项目 2026-08-22 的 GitHub 数据生成的项目动态日报。

---

# CoPaw 项目动态日报 - 2026-08-22

## 1. 今日速览

CoPaw 项目今日活跃度**极高**，24小时内 Issues 和 PR 更新总量达70条，处于高强度迭代状态。项目当前正处在 **v2.1.1-beta** 的开发和稳定性加固阶段，社区反馈大量集中于工具调用可靠性、记忆系统性能与审批流程体验优化。核心开发团队反应迅速，针对多个关键 Bug（如工具调用404、上下文压缩失败）已有或即将有修复 PR。同时，社区贡献者活跃，涌现了多个高质量的功能 PR（如钉钉群共享上下文、按 Agent 归因 Token 用量），显示出良好的开源生态健康度。

## 2. 版本发布

今日无新版本发布（最新版本仍为 v2.1.1-beta.1）。但注意到 PR #7200 `chore: bump the version to v2.1.1b2` 已关闭，预示着小版本迭代正在进行中。

## 3. 项目进展

今日合并/关闭了15个 PR，主要集中在**质量保障**和**基础组件**方面：

- **测试基础设施修复 (质量保障)**：
  - [#7205 [CLOSED] test(coverage): fix Windows integration coverage always reading 0](https://github.com/agentscope-ai/QwenPaw/pull/7205)：修复了 Windows 集成测试覆盖率长期误报为0的问题，并增加了失败保护机制，提升了 CI 的可靠性。
- **控制台性能优化 (体验提升)**：
  - [#7176 [CLOSED] perf(console): keep long chat sessions responsive](https://github.com/agentscope-ai/QwenPaw/pull/7176)：优化了长对话场景下 Console 的响应速度，主要解决了流式输出时 Markdown 重复解析和滚动卡顿问题。
- **多用户支持架构 (重大功能)**：
  - [#7112 [CLOSED] feat(hub): add self-hosted multi-user Hub with local and Docker runtimes](https://github.com/agentscope-ai/QwenPaw/pull/7112)：合并了自托管多用户 Hub 功能，允许在隔离环境中运行多个 QwenPaw 实例，是项目向多用户/团队协作方向迈进的重要一步。

此外，团队正在积极处理多个高价值 PR（如 #7190 qwenpaw-data 安装与演示体验提升），虽未合并，但进展顺利。

## 4. 社区热点

今日讨论最热烈的 Issue 反映了用户对**核心工具链稳定性**的担忧：

- **[#6524 [Bug] MCP 后端重启后客户端无法自动恢复](https://github.com/agentscope-ai/QwenPaw/issues/6524)** (6条评论)：该问题获得最高关注度。用户反馈 MCP Server 重启后，QwenPaw 仍复用失效的 session-id，导致工具调用失败。这暴露出 MCP 连接管理的健壮性不足，是阻碍高级用户深度使用的关键痛点，社区强烈希望实现自动重连机制。

其他高热度需求包括：
- **审批流程优化** (来自 `rerbin` 用户的多个 Issue，如 #7198、#7196)：用户集中反馈审批弹窗和推理过程展示对夜间无人值守任务的干扰，希望有更智能的默认策略和折叠选项。
- **自定义工具开发** ([#7204 [Question] qwenpaw怎么增加自定义tool啊](https://github.com/agentscope-ai/QwenPaw/issues/7204))：开发者对扩展性的需求强烈，希望有更清晰的指南。

## 5. Bug 与稳定性

今日报告的 Bug 较多，按严重程度排列如下：

- **高严重度（核心功能失效）**：
  - [#7016 [Bug] 工具调用404](https://github.com/agentscope-ai/QwenPaw/issues/7016): 流式会话中工具调用返回404，导致功能不可用。目前**未有直接关联的 fix PR**，需要高度关注。
  - [#7206 [Bug] v2.1.1-beta.1: /compact 总是失败](https://github.com/agentscope-ai/QwenPaw/issues/7206): 2.1.1-beta.1 版本中的回归问题，手动压缩上下文时触发 pydantic 校验错误。
  - [#7210 [Bug] 工具配置全部启用但函数 schema 未注入](https://github.com/agentscope-ai/QwenPaw/issues/7210): 工具面暴露不一致，可能导致 Agent 无法调用已配置的工具。

- **中严重度（功能异常）**：
  - [#7156 [Bug] embedding health check 超时](https://github.com/agentscope-ai/QwenPaw/issues/7156): 硬编码的5秒超时导致在慢速后端上误判，导致向量召回降级。
  - [#7193 [Bug] 搜索记忆错乱](https://github.com/agentscope-ai/QwenPaw/issues/7193): 多会话间记忆串扰，可能引发 Agent 行为混乱。
  - [#7136 [Bug] 非 ASCII 文件名显示为乱码](https://github.com/agentscope-ai/QwenPaw/issues/7136)：影响中文等非英文文件名显示。

- **稳定性问题**：
  - [#6780 [Question] 空闲后进程卡死](https://github.com/agentscope-ai/QwenPaw/issues/6780)
  - [#6427 [Bug] WebView2 渲染进程启动崩溃](https://github.com/agentscope-ai/QwenPaw/issues/6427)

**已有修复 PR 的 Bug**：
- **Title 生成受推理影响** (PR #7187) 修复了标题生成可能包含思考文本的问题。
- **注入上下文被持久化** (PR #7211) 修复了通过 HookContext 注入的上下文被错误地保存为可见历史的问题。

## 6. 功能请求与路线图信号

今日用户提出的功能需求集中在以下几个方面，且有相关 PR 支持，**极有可能**被纳入后续版本：

- **审批流程与 UI 个性化**：多个 Issue（#7196、#7198、#7203）要求对推理过程、工具调用信息的显示进行控制，并优化审批模式。这反映了用户对 Agent **可观测性**和**可控性**的更高要求。
- **媒体文件上传限制细分**：[#7201 [Feature] 按提供商拆分媒体大小限制](https://github.com/agentscope-ai/QwenPaw/issues/7201) 建议将单一的上传大小限制拆分为图片、视频、音频独立的配置，以更好适配不同模型提供商的能力。
- **钉钉群共享上下文 (已有 PR)**：PR #7208 支持钉钉群聊内共享会话上下文，这是一个明确的协作功能增强，预计会受到团队用户欢迎。
- **Token 用量归因 (已有 PR)**：PR #7207 实现在 Token 用量页面按 Agent 维度进行统计，提升了资源管理和成本核算的精细度。

## 7. 用户反馈摘要

- **核心痛点**：MCP 连接不稳定、审批流程对无人值守任务不友好、上下文压缩功能存在回归、工具调用偶发404。
- **体验诉求**：用户（尤其是重度用户 `rerbin`）对界面信息的“视觉干扰”非常敏感，希望所有过程信息（推理过程、工具调用）均可配置化显示/折叠，主张界面极简主义。
- **积极反馈**：用户对“记忆搜索”的期望很高（如 Issue #7193 中提到的场景），一旦出现问题（如记忆串扰），会严重影响任务执行，但也从侧面说明该功能已被深度使用。
- **功能期待**：社区对自定义工具（#7204）、多文件上传（#4855 已关闭，可能已实现）等扩展性功能有持续需求。

## 8. 待处理积压

以下为长期未响应或仍处于开放状态的重要 Issue/PR，建议维护团队关注：

- **Critical Issue**：
  - [#6524 MCP 重启后无法自动恢复](https://github.com/agentscope-ai/QwenPaw/issues/6524)（自7月28日起，讨论度高，可能阻塞部分用户）
- **长期未合并的 Feature PR**：
  - [#5992 [PR] Add per-session model overrides](https://github.com/agentscope-ai/QwenPaw/pull/5992)：自7月12日起，该功能对高级用户很有吸引力，可能处于评审积压状态。
  - [#6399 [PR] Add reranker UI config panel](https://github.com/agentscope-ai/QwenPaw/pull/6399)：自7月23日起。
- **较旧的 Bug**：
  - [#6427 WebView2 崩溃](https://github.com/agentscope-ai/QwenPaw/issues/6427)（自7月24日，影响 Desktop 用户）
  - [#6430 启动挂起](https://github.com/agentscope-ai/QwenPaw/issues/6430)（自7月24日，影响 Desktop 用户）

**分析师建议**：优先处理 #7016 工具调用404和 #7206 compact失败这两个高优回归问题，并尽快对 #6524 MCP 重连机制给出明确的修复计划或时间表。同时，可考虑将 #7196/#7198 等关于“审批与显示策略”的需求纳入短期迭代，以提升核心用户体验。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-22


## 1. 今日速览

过去24小时内，ZeroClaw 项目保持着较高的社区活跃度。共产生 50 条 Issue 与 50 条 PR 更新，但值得注意的是新版本发布为 0，且过去24小时内没有 PR 被合并（三个关闭/合并条目中实际多数为关闭）。从 Issue 趋势来看，**安全问题持续集中爆发**：围绕沙箱逃逸（#10165）、高风险命令绕过（#10164）、插件 DNS 阻塞（#10199）以及 ZeroCode 进程退出导致数据丢失（#10121）等形成了多条高优级（p0/p1）讨论。项目议题整体集中在运行时安全模型、日志桥接、WhatsApp 渠道增强与 CI 加固几个方向，核心维护者（如 Audacity88、JordanTheJet）重度参与，社区侧也有多名新贡献者提交了针对性修复 PR。整体判断：**项目处于安全加固与渠道功能并行的快节奏迭代期，但近期无 release 发布，大量高优级修复仍在等待合并。**


## 2. 版本发布

**无新版本发布。** 项目已有一段时间未推出 release，大量已接受的修复（如 #10164 的安全策略绕过修复）仍未通过正式版本交付到用户手中。


## 3. 项目进展

过去24小时内**没有 PR 被合并**（仅 3 条关闭/合并记录，其余 47 条仍待合并）。已关闭/合并的 3 条记录中，有一条在 Issue 侧（#10074 文档修正已关闭）。值得关注的已关闭 Issue 与当前待合并 PR 进展：

| 类型 | 编号 | 核心内容 | 状态 |
|------|------|---------|------|
| Issue 关闭 | [#10074](https://github.com/zeroclaw-labs/zeroclaw/issues/10074) | 修正 SECURITY.md 中已过时的 CI 文档，与实际容器检查保持一致 | ✅ 已关闭 |
| PR 待合并 | [#10203](https://github.com/zeroclaw-labs/zeroclaw/pull/10203) | 为 `log` facade 添加 tracing 桥接，修复 WhatsApp 等依赖日志丢失 | 🟡 等待作者响应 |
| PR 待合并 | [#10204](https://github.com/zeroclaw-labs/zeroclaw/pull/10204) | 修复 Rust 1.98 下的 `chunks_exact` 诊断 | 🟡 待合并 |
| PR 待合并 | [#10093](https://github.com/zeroclaw-labs/zeroclaw/pull/10093) | 隔离 manifest 安装的插件子进程环境 | 🟡 待合并 |

**项目整体推进评估：** 尽管合并节奏放缓，但大量 XL 级别的 PR 仍活跃在队列中，包括 [#10142](https://github.com/zeroclaw-labs/zeroclaw/pull/10142)（ZeroRelay 安全传输）、[#10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146)（插件激活逻辑渠道实例）与 [#9645](https://github.com/zeroclaw-labs/zeroclaw/pull/9645)（ZeroRouter 预设），说明重大特性仍在积极开发中。


## 4. 社区热点

本周社区的关注焦点集中在**一条核心安全讨论与一个持续被讨论的功能改进**上：

**🔥 最热 Issue：#10165 — [independent delegate 绕过 block_high_risk_commands](https://github.com/zeroclaw-labs/zeroclaw/issues/10165)**
- 3 条评论 | 风险等级：S0（数据丢失/安全风险） | 严重度：p1
- 一个独立的 delegate 即使自身配置了 `block_high_risk_commands = true`，在执行高风险命令（如 `rm`）时依然能够绕过该限制。这与 #10164（父路径上配置 allowlist 不生效）形成呼应——**同一安全机制的正反两条路径都存在缺陷**，社区对沙箱策略的一致性问题表现出高度关注。

**💬 次热点：#10074 — [SECURITY.md 文档与实际 CI 不一致](https://github.com/zeroclaw-labs/zeroclaw/issues/10074)**
- 3 条评论 | 类型：文档/CI | 已关闭
- 社区成员发现安全文档描述的 CI 校验流程在 4 月已被移除，但文档未同步更新。快速获得维护者回应并已关闭，展示了良好的文档维护响应速度。

**📢 值得关注趋势：** 渠道相关功能讨论升温。包括 [#10200](https://github.com/zeroclaw-labs/zeroclaw/issues/10200)（WhatsApp 显示名称）、[#10138](https://github.com/zeroclaw-labs/zeroclaw/issues/10138)（Git Channel 进入 Docker 镜像）与 [#10140](https://github.com/zeroclaw-labs/zeroclaw/issues/10140)（iMessage 语音转写），表明社区对多渠道体验一致性的诉求在持续增强。


## 5. Bug 与稳定性

### 🔴 S0 — 数据丢失/安全风险

| Issue | 标题 | 状态 |
|-------|------|------|
| [#10165](https://github.com/zeroclaw-labs/zeroclaw/issues/10165) | Independent delegate 绕过 `block_high_risk_commands`，仅使用自身 risk_profile | 待复现，无修复 PR |
| [#10121](https://github.com/zeroclaw-labs/zeroclaw/issues/10121) | 进程退出导致 Code/ACP 部分回合内容完全丢失（S0） | 已有修复 PR [#10197](https://github.com/zeroclaw-labs/zeroclaw/pull/10197)，XL 规模，仍在待合并 |
| [#10162](https://github.com/zeroclaw-labs/zeroclaw/issues/10162) | 插件安装后配置种子阶段失败不可重试，可能导致安装状态不一致 | 设计中，无修复 PR |
| [#10066](https://github.com/zeroclaw-labs/zeroclaw/issues/10066) | SOP 引擎在记录输出 schema 拒绝前即推送后续步骤执行（workflow blocked） | 已接受，无修复 PR |

### 🟠 S1 — 工作流受阻

| Issue | 标题 | 状态 |
|-------|------|------|
| [#10061](https://github.com/zeroclaw-labs/zeroclaw/issues/10061) | 被拒绝的图像残留在上下文中，毒化后续回合 | 已接受，无修复 PR |
| [#10230](https://github.com/zeroclaw-labs/zeroclaw/issues/10230) | Quickstart 在 daemon 运行中应用时导致栈溢出，中止 Tokio worker | 待复现，新报告 |

### 🟡 S2 — 功能降级（部分代表）

| Issue | 标题 | 状态 |
|-------|------|------|
| [#10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068) | 交互会话上下文被硬限制在 32k tokens，忽略配置的 131072 | 进行中 |
| [#10116](https://github.com/zeroclaw-labs/zeroclaw/issues/10116) | 超大工具结果字节级从中间切断（保留头尾），应溢出到文件 | 已接受，无 PR |
| [#10164](https://github.com/zeroclaw-labs/zeroclaw/issues/10164) | `block_high_risk_commands = false` 不生效，allowlist 内命令仍被封锁 | 已接受，无 PR |

**值得关注的修复 PR（仍在等待合并）：**
- [#10197](https://github.com/zeroclaw-labs/zeroclaw/pull/10197)（XL）— 持久化被打断的 ACP/Code 回合进度，直接解决 #10121 的数据丢失问题
- [#10236](https://github.com/zeroclaw-labs/zeroclaw/pull/10236)（M）— 桌面端 daemon 日志，限制捕获上限 8 MiB，防止日志无限增长


## 6. 功能请求与路线图信号

| 功能请求 | 链接 | 潜在纳入版本信号 |
|---------|------|-----------------|
| **默认开启流式回复**（`stream_mode` 默认改为 `partial`） | [#10166](https://github.com/zeroclaw-labs/zeroclaw/issues/10166) | 已标记 `status:accepted`，p2。社区对渠道回复延迟有明确不满，下一版本可能纳入 |
| **默认启用 stall 看门狗** | [#10168](https://github.com/zeroclaw-labs/zeroclaw/issues/10168) | 已接受，与 #10166 配套的稳定性改进 |
| **WhatsApp Bot 显示名称可配置** | [#10200](https://github.com/zeroclaw-labs/zeroclaw/issues/10200) | **已有实现 PR** [#10201](https://github.com/zeroclaw-labs/zeroclaw/pull/10201)，需求响应迅速，随时可合入 |
| **iMessage 语音消息转写** | [#10140](https://github.com/zeroclaw-labs/zeroclaw/issues/10140) | 已接受，对齐 Telegram/Slack/Discord 已有功能 |
| **ZeroCode 日志文本可选中/复制** | [#10086](https://github.com/zeroclaw-labs/zeroclaw/issues/10086) | 进行中，UX 改进方向 |
| **Option-Backspace 单词删除**（macOS 用户） | [#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059) | 标记为 `good first issue`，适合新贡献者参与 |
| **Git Channel 完全编译进 Debian 镜像** | [#10138](https://github.com/zeroclaw-labs/zeroclaw/issues/10138) | 待维护者审核，需评估镜像体积影响 |

**路线图信号：** 默认开启流式输出（#10166）+ 默认启用 stall 看门狗（#10168）组合表明下一版本将重点改善**渠道回复的实时性与可靠性**；WhatsApp push_name 的快速 PR 响应（#10201）说明渠道配置灵活性是当前迭代重点。


## 7. 用户反馈摘要

**真实痛点：**

1. **安全配置一致性困惑**（#10165、#10164）：rawlink 指出 delegate 的 `risk_profile` 不生效与父路径的 allowlist 不生效是同一机制的两面。用户在 sandbox 上配置了 `block_high_risk_commands = false` 并放行 `rm`，但命令仍被执行引擎硬拦截。**核心诉求：安全策略需要单一事实来源，且 delegate 与父路径行为应完全一致。**

2. **渠道回复体验**（#10166）：JordanTheJet 反映默认 `StreamMode::Off` 导致所有渠道在回合完成前不输出任何内容，对话体验"像旧式 API 而非聊天机器人"。

3. **进程退出即数据丢失**（#10121）：用户在 Code/ACP 回合未完成时如果退出 ZeroCode 或 daemon 终止，已经看到的流式文本和工具调用全部消失。这影响了他们日常使用 AI 编程助手的信任感。

4. **日志丢失**（#10202）：vikng-dev 指出基于 `log` crate 的依赖（如 whatsapp-rust）在 `zeroclaw-log` 安装 tracing subscriber 后没有任何输出，**修复 PR 已经提交但暂未合并**。

5. **插件安装不可重试**（#10162）：如果配置种子阶段在 I/O 错误后失败，插件状态停留在"已安装但未配置"的中间态，用户无法安全地重试。

**正面反馈：** ZeroCode 文件浏览器和健康标签的翻译/布局修复（PR #10108、#10117 等）得到了快速响应和细致打磨，社区对这类 UX 小修持积极态度。


## 8. 待处理积压

### ⚠️ 高优级长期未合并 PR

| PR | 内容 | 等待时间 | 风险 |
|----|------|---------|------|
| [#9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) | 为 Telegram/Slack/Lark/Matrix 审批响应者绑定授权 | **22 天**（7月31日创建） | 安全相关（p1），`needs-author-action` |
| [#9645](https://github.com/zeroclaw-labs/zeroclaw/pull/9645) | ZeroRouter 预设 + 设备流登录（XL） | **21 天**（8月1日创建） | p1，`needs-author-action`，涉及新 provider |
| [#9637](https://github.com/zeroclaw-labs/zeroclaw/pull/9637) | CI 依赖审查：临时豁免 React Router RSC 漏洞（XL） | **21 天** | 标记 `do-not-merge`，需要安全审查 |

### 📌 长期未响应 Issue

| Issue | 标题 | 等待时间 |
|-------|------|---------|
| [#10058](https://github.com/zeroclaw-labs/zeroclaw/issues/10058) | ZeroCode 文件搜索模式忽略行/页导航 | 5 天，已有进行中状态 |
| [#10143](https://github.com/zeroclaw-labs/zeroclaw/issues/10143) | 提供商调用计费生命周期不完整 | 3 天，仍标记为进行中 |

### 🧹 维护者提醒

- **#10230（Quickstart 栈溢出）** 是新报告的 S1 问题，尚无响应，建议优先确认。
- **日志桥接 PR（#10203）** 与 **WhatsApp push_name PR（#10201）** 均标记 `needs-author-action`——若维护者能在 8 月 22-23 日前回复，这两个功能有望快速合入下一版本。
- **安全类 PR 的堆积**值得警惕：多个安全修复（#10197、#10093）已在队列中待合并多日，考虑到本周暴露出的沙箱一致性问题（#10165、#10164），建议维护团队评估合并优先级。

---

*本报告由 ZeroClaw 开源项目分析师 AI 自动生成，数据截至 2026-08-22。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*