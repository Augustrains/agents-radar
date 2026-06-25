# OpenClaw 生态日报 2026-06-25

> Issues: 403 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-25 02:00 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 OpenClaw 项目 2026-06-25 的 GitHub 数据生成的每日项目动态日报。

---

# OpenClaw 项目动态日报 (2026-06-25)

## 1. 今日速览

今日 OpenClaw 项目活动量保持高位，社区贡献和核心开发并进。过去24小时内，共处理了 403 条 Issue 和 500 条 PR，项目仓库处于高度活跃状态。核心进展方面，围绕会话/转录存储的 SQLite 迁移（Path 3）已有 PR 提交，标志着关键架构升级进入收尾阶段。同时，社区针对 Telegram 通道的粘性问题提交了多个改进 PR，SIGUSR1 重启竞态条件（#22676）等关键 Bug 仍在等待修复。项目整体健康状况良好，但长期存在的安全与稳定性 Bug 积压风险需要关注。

## 2. 版本发布

项目在今日发布了两个新版本，主要聚焦于通道控制能力的增强和模型路由的可靠性提升。

- **v2026.6.11-beta.1**
    - **内容**：
        - **更强的通道控制**: 新增 Slack Relay 模式、原生 Mattermost `/oc_queue` 支持，以及每个 DM 独立的模型覆盖配置，使通道操作更易于自动化和调优。(感谢 @sjf-oa, @amknight, @xydigit-zt, @thomaszta, @gandalf-at-lerian)
    - **破坏性变更/迁移注意**: 未明确说明。

- **v2026.6.10**
    - **内容**：
        - **自动快速模式**: 在简短的对话轮次中，OpenClaw 可自动启用快速模式，并在长时间运行后恢复至正常模式，具有边界回落和交付行为。(感谢 @alexph-dev, @vincentkoc)
        - **更可靠的模型路由**: 改进了 Zai 模型的综合路由能力。
    - **破坏性变更/迁移注意**: 未明确说明。

## 3. 项目进展

今日有 66 个 PR 被合并或关闭，项目在多条线上取得实质性进展，尤其集中在核心架构和关键 Bug 修复上。

- **核心架构升级**: 维护者 @jalehman 提交了 PR #96625，旨在完成追踪中的 Issue #88838，将**会话元数据和转录事件存储全面切换至 SQLite**。这标志着 OpenClaw 在数据持久化和访问模式上迈出了重要一步，预计将提升稳定性和可维护性。
- **关键 Bug 修复与合并**:
    - **代码共享优化 (PR #96231)**:  合并了`[codex] Reuse scoped runtime plugin registries`，旨在优化启动后的热路径性能，减少插件注册的重复工作。
    - **提供商错误分类 (PR #96619)**:  合并了`fix(agents): classify upstream transport errors as fallback-worthy`，解决了提供商上游错误（如 500、超时）无法触发模型回落（fallback）的长期问题，增强了系统的鲁棒性。
    - **LINE 通道音频支持 (PR #96616)**: 合并了`fix(line): forward FileMessage fileName...`，修复了 LINE 通道对音频文件格式的识别问题。
- **长期功能推进**: PR #77127 `feat(tools/write): add append mode for agent writes` 已从关闭状态恢复并进入 `ready for maintainer look` 阶段，该 PR 旨在解决 `write` 工具无法追加的痛点，是解决数据丢失问题 #40001 的关键功能，意义重大。

## 4. 社区热点

今日最受关注的议题反映了社区对**跨平台支持、功能完整性以及核心稳定性**的强烈诉求。

- **【长期诉求】Linux/Windows Clawdbot Apps (#75)**: 该 Issue 以 109 条评论和 80 个赞位居榜首，持续关注对官方客户端跨平台支持。社区对 Linux 和 Windows 原生应用的需求极其旺盛，这已成为项目的长期热点。
- **【功能讨论】Tiered bootstrap file loading (#22438)**: 该讨论热度不减（17条评论），用户希望引入层级化的引导文件加载机制来优化上下文窗口和 Token 使用。这代表了中高级用户对精细控制 Agent 行为的普遍需求。
- **【回归 Bug】Telegram richMessages 渲染问题 (#95554)**: 尽管已关闭，但该 Issue 在社区中引发了关注（评论6条，2个赞）。用户报告 v2026.6.9 版本中 Telegram 富消息模式导致段落换行和表格渲染异常，对日常使用体验影响较大，社区反馈迅速。

## 5. Bug 与稳定性

过去24小时内，Bug 报告主要集中在回归问题、会话状态损坏和内存泄漏等方面。其中，许多高优先级 Bug 已有 PR 在修复中，但仍有部分严重问题积压。

- **高度紧急（P1，已有修复 PR 或活跃处理中）**:
    - **Steer mode 注入失败 (#48003)**:  `messages.queue.mode: "steer"` 无法在会话轮次中注入消息。已有相关 PR 在跟进。
    - **子代理锁死 (#95833)**:  `stuckSessionAbortMs` 超时后无法释放 `.jsonl.lock` 文件，导致会话永久性损坏。此问题严重影响用户体验，需紧急关注。
    - **网关内存泄漏 (#87109)**:  macOS 上网关空闲状态内存增长至 1073MB+，导致 cron 任务静默失败。此问题可能影响平台稳定性，需持续追踪。
    - **Thinking 块签名错误 (#94228)**:  在原生 Anthropic 路径上，长时间工具调用会话会因 `thinking` 块签名无效而永久性损坏。这是一个根源性问题。

- **高度紧急（P1，尚未有明确修复）**:
    - **Signal 守护进程重启竞态 (#22676)**:  SIGUSR1 重启时因未等待旧进程退出，导致孤立进程和消息发送失败。该问题已存在数月，对高可用性部署构成威胁。
    - **控制 UI 安全上下文要求 (#32473)**:  在非 HTTPS 环境下，控制台 UI 因安全策略要求设备身份而无法使用，影响非本地部署场景。
    - **引导文件路径错误 (#29387)**:  放置于 `agentDir` 中的引导文件被静默忽略，导致 Agent 配置失效。

- **中优先级（P2，值得关注）**:
    - **Webchat 头像 404 (#38439)**:  回归 Bug，Webchat 中 Agent 头像加载失败。
    - **Google Chat 群组消息静默忽略 (#58514)**:  Google Chat 空间消息被静默丢弃，仅 DM 工作正常。
    - **附件文件名泄露 (#96621)**:  有修复 PR，解决向 Telegram 发送文件时，文件名携带内部缓存后缀的隐私泄露问题。

## 6. 功能请求与路线图信号

今日的功能请求揭示了社区对**精细权限控制、增强的自动化和跨平台体验**的持续渴求。

- **高优先级 / 可能纳入下个版本**:
    - **`write` 工具追加模式 (#40001)**: 已有 **PR #77127** 正在冲刺合并。这是解决长期数据丢失问题的关键功能，预计会被优先纳入下一个稳定版本。
    - **Slack Block Kit 支持 (#12602)**: 社区对于更丰富的 Slack 交互（如按钮、表单）有明确需求。考虑到 v2026.6.11-beta.1 刚增强了 Slack 通道控制，该功能可能成为下一个开发周期的重点。
    - **Telegram 反应触发 (#17840)**:  用户希望表情符号反应能够触发 Agent 响应，实现互动式轮询等场景。这是一个具体的交互优化请求，可能具有较高的开发优先级。

- **中期 / 路线图上值得关注**:
    - **能力基础的权限系统 (#12678)**:  提出为技能和工具设置默认拒绝的高风险操作权限。这反映了专业用户对安全合规的更高要求，可能成为后续版本的安全特性重心。
    - **文件系统沙盒化 (#7722)**:  期望通过配置文件限制 Agent 的文件系统访问权限。这是对安全性的深度诉求，可能会与路径级权限 (#39979) 结合设计。

## 7. 用户反馈摘要

从今日的 Issue 评论和讨论中，可以提炼出以下用户痛点与场景：

- **“性能与内存是首要担忧”**:  用户 `Tanklive` 详细描述了网关内存泄漏导致“cron 任务静默失败——无输出、无推送、无错误上报”的困境。这是真实生产环境中极其棘手的稳定性问题，用户感到沮丧和忧虑。
- **“升级带来的隐形成本过高”**:  用户 `fenglanhua` 在 Bug #95495 中报告，升级到 v2026.6.9 后，memory store 被静默迁移且无任何警告，导致其需要“重新嵌入 1499 个文件”。用户对此表示“非常麻烦”，强调了变更透明度和迁移工具的重要性。
- **“配置层面需要更精细的控制”**:  社区成员 `amknight`（贡献者）提出的 Slack relay 模式、`882soft` 提出的层级化引导文件加载等，都反映了高级用户希望从“能用”到“好用”，对 Agent 行为有更深度的控制和优化能力。
- **“安全与隐私是不可退让的底线”**:  Bug #91804 和 #39847 中，用户 `Kloz813` 报告了“内部推理泄漏”，`p3nchan` 报告了“内部元数据回声污染”。这类问题严重影响用户信任，被社区视为 **P1 级** 回归问题，反馈非常严厉。

## 8. 待处理积压

以下为长期未响应或处理缓慢，但对项目健康度有显著影响的重要 Issue 和 PR，提请维护者关注。

- **【Issue #75 - 跨平台应用】**:  从2026年1月1日持续至今的社区最高呼声。虽有 P2 标签，但其 80 个赞和 109 条评论已证明其优先级。若项目计划拓展用户基础，此为必须解决的问题。
- **【Issue #22676 - Signal 重启竞态】**:  悬挂超过4个月的 **P1 级 Bug**，直接导致部署不稳定。此问题需要尽快投入资源进行修复，以避免影响关键用户。
- **【PR #77127 - Write 工具追加模式】**:  该 PR 已存在近2个月，虽已重新激活，但需尽快完成评审。其关联的 `data-loss` 问题 #40001 对用户数据安全构成严重威胁。
- **【PR #92037 - on-exit cron 调度器】**:  一个广受期待且修改了大量代码（size: XL）的特性 PR。作为“监听命令退出触发任务”的新调度机制，它将极大扩展 OpenClaw 的自动化边界。该 PR 需要更多评审和测试，以避免错过下一个版本周期。

---

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我将基于您提供的 2026-06-25 各项目动态，为您呈上一份横向对比分析报告。

---

### 个人 AI 助手与自主智能体开源生态全景 (2026-06-25)

今日生态整体呈现出 **“高度活跃、安全与规模化并进、竞争与分化加剧”** 的态势。以 OpenClaw 生态（OpenClaw, PicoClaw, NanoClaw, ZeroClaw, Hermes Agent）为核心，项目不仅修复了大量长期存在的 Bug，更在向企业级安全（OIDC, RBAC, MCP 加固）、多智能体编排（ACP 协议）和规模化部署（垃圾回收、网关空闲检测）等方向密集发力。然而，**Token 效率优化** 成为跨项目的最大共识痛点，而 **跨平台支持**（尤其 Windows、Linux 原生客户端）和 **多机器人/多租户管理** 则是社区最急迫的功能诉求。值得警惕的是，多个项目存在安全漏洞被批量报告和修复的情况（如 MCP 安全绕过、SSRF），表明生态正从“能用”向“安全、高效、易用”转变，这一阶段对维护者的响应速度和架构前瞻性提出了极高要求。

### 各项目活跃度对比

| 项目名称 | Issues (新/活跃) | PRs (新/待合) | 版本发布 | 健康度评估 | 主要状态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 403 条 (极高) | 500 条 (极高) | 2 个 (Beta + 正式) | 🟢 良好 | 核心架构升级（SQLite迁移）、大量Bug修复与功能合并。 |
| **NanoBot** | 62 条 (高) | 26 个待合并 | 无 | 🟡 警惕 | 安全加固（MCP）、Telegram兼容性争议、新渠道集成。待合并PR积压。 |
| **Hermes Agent** | 50 条 (高) | 50 条 (高) | 无 | 🟢 良好 | Token效率优化（懒加载Schema）是社区第一热点；多Agent编排方向明确。 |
| **PicoClaw** | 12个安全Issue(已关) | 8 个待合并 | 无 | 🟢 良好 | 一次性修复12个安全漏洞，反应迅速；但待合并PR（含新网关）积压两周。 |
| **NanoClaw** | 低 | 2 个合并/关闭 | 无 | 🟡 健康 | 核心修复（路径遍历）、多机器人功能上线后回调（待澄清）。 |
| **IronClaw** | 15+ 条 (高) | 9 个待合并 | 无 | 🟢 良好 | 运行时严重熔断（`lease_expired`）已定位并修复；内存层重构里程碑合并。 |
| **LobsterAI** | 1条 (低) | 41 个合并/关闭 | 无 | 🟢 健康 | 大规模历史PR清理，内部质量改进，功能迭代放缓。 |
| **CoPaw** | 23条 (高) | 44 个待合并 | 无 | 🟡 警惕 | 社区反馈极高但合并吞吐量低，前端性能瓶颈是最大Bug。 |
| **ZeroClaw** | 100+ 条 (极高) | 10+个待合并 | 无 | 🟢 良好 | 企业级安全特性成社区焦点（OIDC, RBAC）；大量功能性PR待合并。 |
| **TinyClaw** | 0 | 1 个合并 | 无 | 🟢 良好 | 沉寂但稳定，完成重要的Windows兼容性修复。 |
| **NullClaw, Moltis, ZeptoClaw** | - | - | - | ⚪ 静默 | 过去24小时无活动。 |

### OpenClaw 在生态中的定位

OpenClaw 无疑处于该生态的 **绝对核心** 和 **基准参照** 地位。
- **优势**: 项目成熟度最高，社区规模（Issues/PRs 量级）远超其他项目。它定义了“Channel-Agent-Provider”的基础架构模式，其他项目如 NanoClaw, PicoClaw 均被视为其“衍生”或“轻量级”变体。今日其核心的 SQLite 迁移（Path 3）标志着其在数据持久化和可维护性上的领先地位。
- **技术路线差异**: OpenClaw 倾向于 **“功能全面、高度可配置”** 的“重型”路线。相比之下，其他项目要么追求更轻量的核心（如 TinyClaw），要么在特定维度上寻求突破（如 Hermes Agent 的多Agent编排、ZeroClaw 的企业级安全）。
- **社区规模**: OpenClaw 的每日 Issue/PR 处理量（900+）反映出社区体量和开发者活跃度均是断崖式领先。它不仅是生态的“心脏”，也是新议题（如跨平台客户端、Telegram 粘性、内存泄漏）的“发源地”，其他项目常跟进或针对同一问题给出更专注的解决方案。

### 共同关注的技术方向

1.  **Token 效率与成本优化**:
    - **涉及项目**: **Hermes Agent (#6839, #4379)**, **OpenClaw (#40001, #77127)**。
    - **具体诉求**: 强烈要求实现“懒加载工具 Schema”以减少每次 API 调用的固定Token开销，以及为 `write` 工具增加“追加模式”以避免浪费Token重写全部内容。这是所有依赖 LLM API 的项目的核心痛点。

2.  **企业级安全与身份认证**:
    - **涉及项目**: **ZeroClaw (#5982, #7141)**, **OpenClaw (#48003)**, **NanoBot (#4434, #4435)**, **PicoClaw (12个安全Issue)**。
    - **具体诉求**: 从细粒度权限控制（基于角色的权限控制 RBAC、基于消息发送者的权限）、标准化身份认证（OIDC），到工具层（MCP）的权限强制和绕过漏洞修复，安全已成为社区最关切的“天花板”。

3.  **跨平台与多终端支持**:
    - **涉及项目**: **OpenClaw (#75 - 长期诉求)**, **NanoBot (#4479 - PWA)**, **TinyClaw (#281 - Windows 修复)**, **IronClaw (macOS, Windows)**。
    - **具体诉求**: 对 **Linux 和 Windows 原生客户端** 的需求持续高涨。此外，移动端的体验（PWA、iOS输入框问题）也开始被更多用户提及。

4.  **多Agent/多租户编排**:
    - **涉及项目**: **Hermes Agent (#5257)**, **NanoClaw (#2852)**, **ZeroClaw (#5982, #8226)**。
    - **具体诉求**: 项目开始从单一 Agent 向“多Agent编排枢纽”演进，同时，为了服务不同用户或业务线，“单实例多租户”的部署能力需求日益凸显。

5.  **消息通道扩展与兼容性**:
    - **涉及项目**: **PicoClaw (#3063)**, **NanoBot (#4502 - Webhook)**, **Hermes Agent (#3725)**, **OpenClaw (Telegram, Slack etc.)**。
    - **具体诉求**: 社区积极为项目添加新的消息通道（如 DeltaChat、Webhook、Rocket Chat），同时解决现有通道的兼容性问题（如 Telegram 富文本格式在不同客户端的异常显示）。

### 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 | 核心差异点 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **全能型** 个人AI中枢 | 高级用户、开发者、自部署爱好者 | 模块化，核心+插件 | 生态最完备，功能最全面，社区驱动。 |
| **Hermes Agent** | **多Agent** 编排与协作 | 需要管理多种底层AI Agent的用户 | 网关+Agent+Provider | 定位为“Agent的Agent”，强调统一调度和Token效率。 |
| **ZeroClaw** | **企业级** 安全与基础设施 | 企业团队、运维人员 | 强调安全隔离与认证 | 专注于RBAC、OIDC、供应链安全等企业级特性。 |
| **NanoBot** | **轻量、快速集成** | 个人开发者、低资源环境用户 | 强调轻量和快速上手 | 体积小，依赖少，支持PWA和Webhook集成。 |
| **IronClaw** | **高性能、底层架构** | 核心开发者、性能敏感场景 | 高度模块化和可插拔 | 关注内核解耦、内存管理、运行时稳定性（`Reborn`）。 |
| **CoPaw** | **前端体验**优先 | 追求UI/UX的用户 | 前端较重，Rust/Tauri | 关注聊天界面的交互细节，但后端架构合并速度是关键短板。 |

### 社区热度与成熟度

- **快速迭代阶段 (核心爆款)**: **OpenClaw, Hermes Agent, ZeroClaw, IronClaw**。这些项目 Issues 和 PR 活跃度极高，核心开发者和社区贡献者同步发力，新功能和 Bug 修复迭代迅速，具有最高的行业关注度。
- **质量巩固与安全加固阶段**: **PicoClaw, NanoBot**。这些项目在经历了初期功能爆发后，现正集中精力处理安全漏洞、修复兼容性问题和清理积压的PR，以提升稳定性和用户信任度。
- **内部整合与清理阶段**: **LobsterAI**。项目维护者正进行大规模的历史仓库清理，合并大量的修复PR，功能迭代节奏放缓，属于“蓄力期”。
- **平稳维护 / 沉寂**: **CoPaw (高反馈低合并), NanoClaw (功能回调), TinyClaw, NullClaw, Moltis, ZeptoClaw**。这些项目要么社区反馈与官方响应速度不匹配（CoPaw），要么核心功能出现反复（NanoClaw），要么长期缺乏更新。

### 值得关注的趋势信号

1.  **“Token 意识”成为架构前设**: 开发者不再仅关注功能是否实现，而是开始评估每一个功能（如Schema注入、系统提示词固定开销）对 Token 消耗的影响。**未来，Token 效率工程师或角色将出现，项目文档中也需要明确给出“Token 消耗评估”**。

2.  **企业级需求催生专业分化**: 社区不再满足于单一的“个人AI助手”。关于多租户、RBAC、OIDC、审计日志、供应链安全的讨论密集涌现。这表明该生态正显著受到 **B 端（企业、团队）用户的关注**，为项目商业化奠定了基础。

3.  **安全漏洞的“批量发现”模式**: 安全研究员（如 `YLChen-007`）高效地在不同项目中（PicoClaw, NanoBot）利用相似手法发现并报告了同一类安全漏洞（MCP权限绕过、SSRF）。这提醒所有项目，一个项目中的安全修复，需要立即在其他项目中同步检查。

4.  **从“个人助手”到“系统底座”的定位转变**: OpenClaw 正变得越来越像一个“个人操作系统”，管理着文件、定时任务、认证、网关等多重角色。**AI 智能体正从“聊天伙伴”演变为“数字生命体的操作系统”，这将是接下来一年最核心的架构演进方向。**

**对 AI 智能体开发者的参考价值**：
- **立即行动**: 检查并修补 MCP 及相关工具的权限绕过和 SSRF 漏洞。
- **优先规划**: 将 **Token 懒加载** 和 **跨平台客户端** 作为下一版本的最高优先级特性。
- **前瞻布局**: 研究并试点 **多Agent编排协议（ACP）** 和 **企业级身份认证（OIDC）**，为更复杂的应用场景做好准备。
- **谨慎选择**: 在选择依赖的项目时，应关注其“修复 Bug 和合并 PR 的周期”，而不是仅看其“Star 数”。一个健康的生态应是“社区能报，维护者能修”的高效闭环。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 GitHub 数据，生成 NanoBot 项目 2026-06-25 的动态日报。

---

## NanoBot 项目动态日报 | 2026-06-25

### 1. 今日速览

NanoBot 项目今日活跃度**极高**，共产生 62 条 Issue 及 PR 更新。社区围绕 **Telegram 消息格式兼容性问题**（#4488, #4505, #4495）、**MCP 安全策略绕过**（#4434, #4435）以及广泛的**移动端 Bug 修复**与**新渠道集成**（Mattermost, Webhook）展开了密集的讨论与开发。项目在**稳定性修复**与**功能增强**两条线上并进，但待合并 PR 积压较多（26 个），维护团队的审查与合并效率将是未来几日关注重点。

### 2. 版本发布

**无**。过去24小时无新版本发布。上一个稳定版推测为 `v0.2.2`（基于 Issue #4470 及 #4500 提及）。

### 3. 项目进展

今日共有 18 个 PR 被合并或关闭，项目在以下方面取得关键进展：

- **安全加固（MCP）**: **YLChen-007** 报告了两个严重的 MCP 权限绕过漏洞（#4434, #4435），指出 `enabledTools` 配置为 `[]` 时未能阻止资源（Resources）和提示（Prompts）的暴露。对应的修复 PR **#4436** 和 **#4452** 已完成，并正处于待合并状态，这是项目安全性的重大改进。
- **新功能合并**:
    - **Kimi Coding 计划支持**: **#4464** 被合并，为订阅用户新增了 `kimi_coding` 专属模型提供商。
    - **OpenCode 模型集成**: **#4475** 被合并，新增了 `opencode_zen` 和 `opencode_go` 两个提供商，扩展了模型选择范围。
- **细节修复**:
    - **WebUI 显示优化**: **#4487** 被合并，修复了 WebUI 中多文件 `apply_patch` 编辑记录显示不全的问题。
    - **多端兼容性**: **#4463** 被关闭，标志着对 Kimi Coding 计划的支持完成。

**项目整体向前迈进了重要一步**，特别是在安全模型和第三方模型提供商集成方面，但大量修复 PR 仍停留在“待合并”状态，项目的实际交付能力有待提升。

### 4. 社区热点

- **Telegram 消息格式争议**: 这是今日绝对的焦点。围绕 PR **#4505**（`fix(telegram): add rich_message config option`）和 **#4495**（`fix(telegram): add config toggle for Bot API 10.1`），社区反馈热烈。用户 **anrew1001** 的 Bug 报告（#4499）和 **chengyongru** 的报告（#4488）指出，启用 Bot API 10.1 富文本格式后，**Telegram Web 版和 Telegram X 客户端无法正常显示消息**，显示为空白或“不支持的格式”。这表明 **API 升级与客户端生态的不完全兼容**是当前最突出的用户体验痛点，开发者正在提供配置选项来缓解此问题。

- **MCP 安全漏洞讨论**: **#4434** 和 **#4435** 两则安全问题由同一作者 **YLChen-007** 提交，虽然评论数不多（各 1 条），但技术含量极高，直接指出了代理核心安全机制的实现缺陷。它们代表了社区中高阶用户对**项目安全模型完整性的深度审视**，其提出的“绕过问题”如果得不到解决，将对依赖 MCP 控制权限的企业级用户造成严重风险。

### 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 | 关联 Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | #4434, #4435 | **MCP 权限绕过**：`enabledTools: []` 未能阻止资源与提示暴露。 | 待 Review | #4436, #4452 |
| **高** | #4500 | **WebUI 导航与状态错误**：首页发送不跳转、重连后流式卡死、停止按钮无效。 | 待确认 | 未发现公开 PR |
| **高** | #4488 | **Telegram Web 兼容性回归**：富文本格式导致 Web 版消息无法显示。 | 待合并 | #4505, #4495 |
| **中** | #4497 | **钉钉渠道超时与格式丢失**：`httpx.ConnectTimeout` 及 `richText` 类型消息被丢弃。 | 待合并 | #4501 |
| **中** | #4499 | **Telegram 频道空消息**：Agent 回复在 Telegram 客户端显示为空气泡。 | 待排查 | 未发现公开 PR |
| **低** | #4470 | **Telegram 换行符丢失与消息闪烁**：`v0.2.2` 中的显示问题。 | 待确认 | 未发现公开 PR |

### 6. 功能请求与路线图信号

- **安全审计与信任信号**：**#4503** 提议在 README 中添加外部信任徽章（HVTracker），反映了社区对项目**供应链安全与透明度**的更高期待。
- **Web 钩子 & 企业集成**：PR **#4502** 提出为网关添加 Webhook 触发器，结合已并发的 PR **#4459**（Mattermost 支持），显示了项目从个人助手向**企业级消息和工作流集成平台**演进的明确趋势。
- **PWA 与移动端体验**：**#4479** 提出的 PWA 支持、侧边栏滑动手势及 **#4388** 修复的 iOS 输入框放大问题，表明 **移动端 WebUI 体验优化**仍是下一阶段的重点方向。
- **技能组织优化**：PR **#4504** 提出支持在子目录中组织技能文件，这是一个反映用户技能数量增长后**对更好的文件管理能力**的迫切需求的信号。

### 7. 用户反馈摘要

- **正面反馈**：无明确正面评价，更多是问题反馈和功能请求。
- **核心痛点**：
    1.  **“看似轻量，实则臃肿”**：Issue #660 的用户 **besoeasy** 尖锐地指出，项目声称“超轻量”却依赖 Node.js，与描述矛盾，引发了对项目定位的质疑（👍 5 个，反映出不少用户的共鸣）。
    2.  **“更新成了负优化”**：多位用户（#4470, #4499, #4488）反馈 **v0.2.2** 版本引入了 Telegram 相关的显示回归问题，表明新功能（富文本）的上线缺乏充分的客户端兼容性测试。
    3.  **“配置不当，安全漏洞”**：用户 **YLChen-007** 的 MCP 漏洞发现，展示了专业用户对安全配置的深度使用和验证，而漏洞则暴露了文档与实际实现之间的差距。

### 8. 待处理积压

- **长期未响应的关键 Issue**：
    - **#660**：[OPEN] “超轻量”项目名不副实（创建于 2026-02-14，评论 11 条）。该 Issue 关于项目核心定位的争议已持续**超过 4 个月**，至今未被维护者正式回应或解决，是社区信任的一个潜在风险点。
    - **#4388**：[CLOSED] iOS Safari 输入框放大问题。虽然已被关闭，但该问题在移动设备上复现，影响用户体验，需要确认修复是否彻底。

- **高优先级待合并 PR**（这些 PR 解决了当日最严重的问题，应优先审查合并）：
    1.  **#4436 & #4452**：解决 MCP 安全绕过漏洞。
    2.  **#4505 & #4495**：解决 Telegram Web/Telegram X 兼容性问题。
    3.  **#4501**：解决钉钉渠道超时和消息丢失问题。
    4.  **#4493**：解决 Xiaomi MiMo ASR 转录失败的 Bug。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-06-25

---

## 1. 今日速览

项目整体活跃度**极高**。过去24小时内，共有 **50条 Issue 更新**（其中新开/活跃39条，关闭11条）和 **50条 PR 更新**（待合并38条，已合并/关闭12条）。社区讨论焦点集中在 **Token 开销优化**（尤其是高频的懒加载工具 Schema 和固定开销分析）、**多 Agent 编排/ACP 协议**、以及 **流式/网关稳定性** 三方面。新版本无发布，但多个高价值 PR（如 TUI 启动优化、智能审批作用域修复）已被合入主分支。

---

## 2. 版本发布

**无**（过去24小时无新 Release）

---

## 3. 项目进展

### 已合并/关闭的重要 PR（12条）

| PR 编号 | 标题 | 类型 | 对应 Issue | 影响 |
|--------|------|------|------------|------|
| #52246 | fix(soul): installers seed real default persona | Bug | — | 新安装用户不再获得空 SOUL.md 模板，而是真实 Hermes 人格种子 |
| #52232 | fix(tui): route /learn through command.dispatch | Bug | #51829 | 修复桌面 GUI (TUI) 中 `/learn` 命令只显示 ack 而不触发 LLM 的 bug |
| #52207 | feat(gateway): scale-to-zero idle detection (Phase 0) | Feature | — | 网关侧空闲检测 + 休眠唤醒行为层，为托管实例的自动扩缩容奠基 |
| #52243 | (salvage of #52207) scale-to-zero Phase 0 合入 | Feature | — | 与 #52207 相同功能，由 maintainer 重新基于 `main` 提交 |
| #52245 | fix(tui): prevent spurious npm install on every launch | Bug | — | TUI 依赖检查从全字段比较改为稳定性哈希，消除每次启动重装 npm 的浪费 |
| #52158 | fix(cli-code-format): code fences mangled during streaming | Bug | — | 修复流式输出时 strip 模式错误删除代码围栏反引号的问题 |
| #51136 | fix(Docker): lazy install optional deps in official image | Bug | #49445, #50205 | Docker 镜像中可选依赖（如 Firecrawl）现在可正常懒安装 |
| #51069 | [CLOSED duplicate] Support project .mcp.json | Feature | — | 重复需求，标记为已有关注 |
| #46762 | fix(Telegram flood-control retry) | Bug | — | Telegram 富消息流控下重试忽略 `retry_after` 的问题已修复 |
| #42449 | fix(delegate_task context corruption) | Bug | — | 子代理通过全局单例污染父代理 context_length 的严重 bug 已修复 |
| #44515 | fix(Desktop Update stuck) | Bug | — | 桌面端更新管理器因后台进程卡在 1/3 的问题已修复 |
| #51829 | [CLOSED] /learn ack但无LLM | Bug | — | 与 #52232 配套关闭 |

**项目整体向前迈进**：在 **TUI/CLI 稳定性**（npm 启动、代码围栏、/learn 命令）、**网关层**（空闲检测、Telegram 流控）、**安全模型**（credential 丢失修复、智能审批作用域）以及 **Docker 生态**（懒安装可选依赖）四个方向均有实质性推进。

---

## 4. 社区热点

### 🔥 最活跃 Issue（评论数 Top 3）

| Issue | 标题 | 评论 | 👍 | 核心诉求 |
|-------|------|------|-----|---------|
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | Lazy Tool Schema Loading | **28** | 14 | 每次 API 调用都注入全部工具 Schema（~3500-5000 tokens），用户希望实现**懒加载**——只有真正用到某个工具集时才注入其 Schema，大幅减少 token 开销。 |
| [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) | Token overhead: 73% fixed overhead | **16** | 0 | 用户通过仪表盘实测发现 **73% 的 API 调用是固定开销（约13.9K tokens）**，与 #6839 互相印证。 |
| [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) | openai-codex fails where official CLI works | **12** | 3 | 在相同 macOS 机器和网络上，官方 Codex CLI 可正常工作，但 Hermes 的 `openai-codex` provider 反复失败，用户需要排查。 |

### 🔥 最受关注 Issue（👍 Top 3）

| Issue | 👍 | 标题 |
|-------|-----|------|
| [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) | **16** | 通用 ACP 客户端支持多 Agent CLI 编排 |
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | **14** | 懒加载工具 Schema — 两阶段 Tool 注入 |
| [#3725](https://github.com/NousResearch/hermes-agent/issues/3725) | **10** | Rocket Chat 网关支持 |

**分析**：
- **Token 开销是社区头号痛点**。两个高热度 Issue 直指同一个问题：Hermes 当前每次调用都发送完整工具 Schema 和大量固定开销，对于自托管/本地模型用户尤其敏感。  
- **ACP 多 Agent 编排**（#5257）获16个 👍 且持续讨论11条，显示用户期望 Hermes 从一个单体 Agent 演变为**多 Agent 编排枢纽**，能统一协调 Claude Code、Copilot、Cline 等不同编码 Agent。

---

## 5. Bug 与稳定性

### 🔴 P1 — 严重

| Issue | 标题 | 根因/影响 | 是否有 Fix PR |
|-------|------|-----------|--------------|
| [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) | OpenAI-Codex credential pool drops newly added credential | 认证凭据轮转时 `auth.json` 重写导致新凭据丢失 | 暂无 |
| [#52197](https://github.com/NousResearch/hermes-agent/issues/52197) | Gateway cross-process agent-cache invalidation stalls Discord heartbeats | 清理缓存时持锁导致 asyncio 循环阻塞 → Discord 心跳超时 → 断连 | 暂无 |

### 🟡 P2 — 中

| Issue | 标题 | 是否有 Fix PR |
|-------|------|--------------|
| [#52244](https://github.com/NousResearch/hermes-agent/issues/52244) | Windows 上 Hermes One 输出 UTF-8 截断/乱码 | 暂无 |
| [#52160](https://github.com/NousResearch/hermes-agent/issues/52160) | 双次压缩后 Anthropic 请求首个 role 为 assistant 被拒 | 暂无 |
| [#52212](https://github.com/NousResearch/hermes-agent/issues/52212) | 非编辑平台（QQ/微信/Signal等）静默丢弃工具进度消息 | 暂无 |
| [#52228](https://github.com/NousResearch/hermes-agent/issues/52228) | 显式 provider 辅助任务遇到 429 速率限制时绕过降级链 | **[PR #52251](https://github.com/NousResearch/hermes-agent/pull/52251)** 已提交 |
| [#52216](https://github.com/NousResearch/hermes-agent/issues/52216) | BrokenPipeError 跳过传输层连接池重建 | 暂无 |
| [#33801](https://github.com/NousResearch/hermes-agent/issues/33801) | 密钥脱敏系统在写入文件前替换内容，破坏 Python/Shell 语法 | 暂无 |

### 🟢 P3 — 低

| Issue | 标题 |
|-------|------|
| [#52235](https://github.com/NousResearch/hermes-agent/issues/52235) | Windows 桌面端 v0.17.0 PageDown 键导致 UI 异常 |
| [#52141](https://github.com/NousResearch/hermes-agent/issues/52141) | Kanban 工具 `kanban_create/list` 对主 Agent 不可用 |
| [#36216](https://github.com/NousResearch/hermes-agent/issues/36216) | Hindsight 在会话结束时丢弃缓冲轮次（`retain_every_n_turns > 1`） |
| [#33389](https://github.com/NousResearch/hermes-agent/issues/33389) | `auxiliary.vision.provider: gemini` 配置不生效，回退到主 provider |

---

## 6. 功能请求与路线图信号

| 请求 | 链接 | 可能纳入下一版本的信号 |
|------|------|----------------------|
| **Lazy Tool Schema Loading** | [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | ✅ 已有社区仪表盘数据支撑（#4379），且与 PR [#22648](https://github.com/NousResearch/hermes-agent/pull/22648) (Ollama Cloud 插件化工具集) 路线吻合 |
| **通用 ACP 客户端编排** | [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) | ✅ 获16个 👍，与 Hermes 多 Agent 战略方向一致，有具体设计 |
| **Rocket Chat 网关** | [#3725](https://github.com/NousResearch/hermes-agent/issues/3725) | ✅ 获10个 👍，实现范围小（<50行），社区热情高 |
| **per-channel 显示覆盖** | **[PR #52248](https://github.com/NousResearch/hermes-agent/pull/52248)** | ✅ 已提交 PR，有望快速合入 |
| **可延续的 Cron 任务** | **[PR #52250](https://github.com/NousResearch/hermes-agent/pull/52250)** | ✅ 已在 merge 队列中，`maintainer` 直接提交 |
| **确定性 Skill 路由** | **[PR #52247](https://github.com/NousResearch/hermes-agent/pull/52247)** | ✅ 新 PR，设计清晰，范围精准（仅4文件） |
| **俄罗斯语/多语言本地化** | [#52137](https://github.com/NousResearch/hermes-agent/issues/52137) | ⏳ 多个本地化请求出现（法、中、葡、俄），社区规模扩大信号 |
| **可配置内存后端** | [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) | 🔮 高阶用户诉求，但涉及系统提示层改造，优先级待评估 |

---

## 7. 用户反馈摘要

### 积极反馈
- **功能建议质量高**：用户 `Bichev` 不仅报 Bug 还**附上了完整的监控仪表盘实现**（[hermes-dashboard](https://github.com/Bichev/hermes-dashboard)），并用数据证明 73% token 为固定开销，属于高质量的社区贡献。  
- **新手体验有改善信号**：PR [#52246](https://github.com/NousResearch/hermes-agent/pull/52246) 的合入意味着新用户安装后将获得**有灵魂的默认人格**，而不是空模板——这对首次使用体验是质的提升。

### 痛点与不满
- **Token 浪费持续困扰自托管用户**。多位用户在 #6839 和 #4379 中表达了“本地模型跑不起，资源全浪费在固定开销上”的挫败感。  
- **Windows 常态化问题**。同一天出现 3 个 Windows 专属 Bug（UTF-8 截断 #52244、PageDown UI 异常 #52235、更新后网关持久窗口 #52239），显示 **Windows 平台稳定性仍需大幅改善**。  
- **安全 vs 可用性的权衡**。智能审批模式（#46544）在“安全”与“正常维护操作”之间的冲突，让用户觉得 `recommended` 模式“实际上不可用”。PR [#47705](https://github.com/NousResearch/hermes-agent/pull/47705) 有望缓解此矛盾。

### 使用场景
- **多 Agent 编排**（#5257）：高级用户希望 Hermes 成为“Agent 总指挥”，统一调用 Claude Code/ Copilot/ Cline 等不同 Agent 完成复杂任务。  
- **企业级接入**：Rocket Chat 网关（#3725）的持续拥戴显示 Hermes 正从个人工具向团队协作场景延伸。  
- **Token 敏感场景**：本地模型、按量计费 API 用户对每一次 API 调用的 Token 效率极为敏感。

---

## 8. 待处理积压

### 重要 Issue 长期无回应

| Issue | 创建时间 | 最后回应 | 风险等级 | 建议 |
|-------|----------|----------|----------|------|
| [#36216](https://github.com/NousResearch/hermes-agent/issues/36216) | 2026-06-01 | 2026-06-24 | ⚠️ 中 | Hindsight 数据丢失 bug，`retain_every_n_turns` 用户可能无感知丢失回忆数据，建议分配 P1 |
| [#33389](https://github.com/NousResearch/hermes-agent/issues/33389) | 2026-05-27 | 2026-06-24 | ⚠️ 中 | Vision provider 配置不生效，影响 Gemini 用户的视觉能力 |
| [#17945](https://github.com/NousResearch/hermes-agent/issues/17945) | 2026-04-30 | 2026-06-24 | ⚠️ 中 | `delegate_task` HTTP 404，阻塞“自动研究”高级特性，已有重试逻辑但未根治 |
| [#33801](https://github.com/NousResearch/hermes-agent/issues/33801) | 2026-05-28 | 2026-06-25 | ⚠️ 高 | 密钥**内容层**脱敏破坏 Python/Shell 语法，执行工具静默失败——**安全与可用性冲突**，需要架构级修复 |
| [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) | 2026-05-04 | 2026-06-24 | 🔴 高 | 凭据丢失（P1），多进程场景下认证系统有数据竞争 |

### 需维护者确认的 PR

| PR | 标题 | 创建时间 | 备注 |
|----|------|----------|------|
| [#8427](https://github.com/NousResearch/hermes-agent/pull/8427) | Vertex AI (Gemini) 企业级 provider | 2026-04-12 | **已等待 2.5个月**，企业用户急切需要 GCP 集成 |
| [#22648](https://github.com/NousResearch/hermes-agent/pull/22648) | Ollama Cloud 插件化 Web/视觉 provider | 2026-05-09 | 与 #8427 同属“新 provider 接入”路线，但冲突重基后需再次 review |
| [#48475](https://github.com/NousResearch/hermes-agent/pull/48475) | 展示 Z.AI 账户配额用量 | 2026-06-18 | 较小但实用功能，可快速合入 |

---

**日报总结**：Hermes Agent 正处于**高速迭代期**，社区贡献活跃（50 Issue / 50 PR 单日），但 Token 效率优化是**用户最大共识痛点**。安全与可用性之间的平衡、Windows 平台适配、以及多 Agent 编排是未来三个关键方向。建议维护者优先推进 **Lazy Tool Schema** 的决策/设计评审（#6839），并加速 **Vertex AI**（#8427）和 **Ollama Cloud**（#22648）两个长时间待审 PR。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于提供的数据生成的 PicoClaw 项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-06-25

### 1. 今日速览

过去24小时，PicoClaw 项目处于**高密度维护与安全修复**模式。项目团队集中处理了由安全研究员提交的 **12个安全相关 Issue**（已全部关闭），表明项目对安全漏洞的响应速度很快。尽管没有新功能发布，但在代码库稳定性和安全性方面取得了显著进展。此外，有 **8个 Pull Request** 处于待合并状态，涵盖了新网关（DeltaChat）、生命周期修复以及多个兼容性优化，显示出社区贡献的活跃度。整体项目健康度良好，但积压的 PR 需尽快审阅合并。

### 2. 版本发布

无。

### 3. 项目进展

尽管今天没有合并 PR，但以下 **8个待合并的 PR** 是项目向前迈进的关键信号，它们涵盖了功能、修复和稳定性提升：

-   **新功能**:
    -   `#3063` [OPEN] feat: add deltachat gateway - 新增对 DeltaChat 消息协议的支持，扩展了项目的通信渠道。
-   **生命周期与核心流程修复**:
    -   `#3116` [OPEN] fix(pico): complete turn.done lifecycle signaling - 完善了 Pico 客户端的轮次结束生命周期信号，解决了请求ID丢失等问题，这是对核心交互流程的重要补充。
-   **兼容性与稳定性修复**:
    -   `#3165` [OPEN] fix(openai_compat): recover Seed XML tool calls - 恢复了对火山引擎豆包（Seed）的XML格式工具调用的支持。
    -   `#3166` [OPEN] fix(openai_compat): use structured logger for native_search warning - 修复因日志打印错误导致的编译失败问题。
    -   `#3168` [OPEN] fix(model): handle error response read failures - 改进了模型列表获取失败时的错误处理，避免返回空信息。
    -   `#3169` [OPEN] fix(evolution): skip cold path for heartbeat turns - 优化了进化（Evolution）模块，避免在心跳检测上浪费Token。
-   **Bug 修复**:
    -   `#3115` [OPEN] Fix inline data URL media extraction for generic tool output - 修复了通用工具输出中包含 `data:image/...;base64,...` 字符串时导致会话历史错乱的Bug。
-   **新能力**:
    -   `#3118` [OPEN] Add remote Pico WebSocket mode to picoclaw agent - 为 `picoclaw agent` 命令增加远程 WebSocket 模式，允许连接到远程PicoClaw实例。

**小结**: 项目正通过多项修复和新功能稳步推进，尤其是在OpenAI兼容层和核心生命周期方面，修复了多个影响用户体验的质量问题。

### 4. 社区热点

-   **热点 Issue**:
    -   `#2404` [CLOSED] [Feature] Add in config to send streaming HTTP request (`sipeed/picoclaw Issue #2404`)
        -   **分析**: 该 Issue 获得了 **13条评论**，是评论数最多的。它请求在配置文件中增加对 `streaming: true` 的支持，以使 PicoClaw 能够以流式方式与后端LLM（如 OpenAI）交互。这反映了社区对**实时、低延迟**交互体验的强烈需求，这是 AI 助手产品的基础功能。尽管该 Issue 已关闭，但其核心诉求很可能已被采纳或规划。

-   **PR 讨论**:
    -   `#3063` [OPEN] feat: add deltachat gateway (`sipeed/picoclaw PR #3063`)
        -   **分析**: 这是一个已存在两周的 PR，虽然评论数为空，但 DeltaChat 本身是一个与电子邮件网络交互的去中心化即时通讯协议。该 PR 的引入表明社区有探索**多样化、去中心化通信方式**的兴趣，值得维护者关注其进展。

### 5. Bug 与稳定性

过去24小时内，共关闭了 **12个安全相关 Issue**。按严重程度排列如下，均为**高危/严重**级别，且已全部修复或关闭。

-   **严重安全漏洞 (已关闭)**: 这些漏洞由研究员 `YLChen-007` 提交，均涉及敏感权限绕过或信息泄露。
    -   **SSRF/网络请求绕过**:
        -   `#3078`: `web_fetch` 可通过配置的 HTTP 代理绕过 SSRF 防护。
        -   `#3074`: `web_fetch` 可通过 ISATAP IPv6 地址绕过 SSRF 防护，访问本地/私有网络。
    -   **权限/策略绕过**:
        -   `#3082`: 飞书（Feishu）频道的上下文回复功能绕过了 `allow_from` 权限检查。
        -   `#3081`: `cwd` 符号链接竞争条件允许 `exec` 在未授权目录执行。
        -   `#3079`: `exec` 命令白名单可通过 `jq` 绕过，泄露环境变量。
        -   `#3076`: 企业微信（WeCom）群组触发策略可被绕过，使未提及机器人的群消息也能被处理。
        -   `#3068`: MQTT 频道的 `allow_from` 授权可通过伪造 `client_id` 绕过。
    -   **控制平面/会话劫持**:
        -   `#3072`: Launcher 首次设置密码存在 CSRF 漏洞，可导致本地控制平面被接管。
        -   `#3071`: 已认证的 WebSocket 客户端可通过 `/reload` 端点触发未授权的配置重载。
        -   `#3073`: LINE Webhook 签名验证可被重放攻击，导致重复事件执行。
        -   `#3075`: 本地仓库 `skills/` 目录下的元数据会自动加载到系统提示词中，存在注入风险。

**项目健康度评估**: 一次性大规模修复多个安全漏洞，说明项目进行了**安全审计**或收到了安全研究员的负责任披露。这对项目的长期健康和用户信任至关重要。

### 6. 功能请求与路线图信号

-   **流式输出**: `#2404` 对 `streaming` 配置的支持需求非常强烈。虽然没有对应的 PR，但这是提升用户体验的关键功能，很可能已在计划中。
-   **PageAgent 对 MVVM 框架的支持**: `#3167` 用户询问了 PageAgent 对 Vue 等现代前端框架的适配方案。这是一个重要的生态扩展方向，表明用户希望 AI Agent 能在复杂的业务系统中发挥作用。目前暂无 PR 回应。
-   **新网关**: `#3063` (DeltaChat) 和 `#3118` (远程 Pico WebSocket) 表明社区正在探索更多的连接方式，扩展 PicoClaw 的应用边界。这些新特性可能会在下一个版本中与用户见面。

### 7. 用户反馈摘要

-   **用户 `Wavekip` (Issue #3167)**: 用户正在 Vue + Element UI 的企业后台项目中测试 PageAgent。用户理解 PageAgent 的核心价值，但指出其目前可能无法很好地适配 `v-model`、组件内部状态和 watcher 等 MVVM 架构特有的机制。这表明在**复杂、动态的单页应用（SPA）场景下**，PageAgent 的 DOM 操作能力存在局限性，用户期望有针对这类架构的专门适配方案。

### 8. 待处理积压

-   **风险项：长期未响应的核心功能 PR**
    -   `#3063` [OPEN] feat: add deltachat gateway - **创建于 2026-06-08，已停滞 17 天。**
        -   **建议**: 此 PR 引入了重要的新特性，但已长时间未被处理。为避免社区贡献者流失，建议维护者尽快安排代码审查。
    -   `#3118` [OPEN] Add remote Pico WebSocket mode - **创建于 2026-06-12，已停滞 13 天。**
        -   **建议**: 同样的，该 PR 代表了项目架构的重要扩展能力，长期未合并可能会阻碍依赖于此功能的后续开发。
    -   `#3116` [OPEN] fix(pico): complete turn.done lifecycle signaling - **创建于 2026-06-12，已停滞 13 天。**
        -   **建议**: 此修复完善了核心的生命周期管理，是提升系统稳定性的关键。长时间挂起可能影响使用 Pico 客户端的用户。
    -   `#3115` [OPEN] Fix inline data URL media extraction - **创建于 2026-06-12，已停滞 13 天。**
        -   **建议**: 该 Bug 会导致会话历史错乱，影响用户查看历史记录。建议优先审查合并。

**总结**: 项目核心维护团队在过去24小时展现出了对**安全问题的极高响应度**。然而，对于已提交、有明确价值且等待许久的社区贡献 PR，需要同样高效地推动审核与合并，以维持社区的积极性和项目的迭代速度。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的 NanoClaw 项目数据生成的 2026-06-25 项目动态日报。

---

## NanoClaw 项目动态日报 | 2026-06-25

### 1. 今日速览

今日项目活跃度极高。核心开发者在**安全加固**、**多机器人实例**及**架构扩展**方面提交了大量 PR，显示出项目正在为生产级部署做积极准备。虽然有一个关于“多 Telegram 机器人”功能的用户诉求 (#2852) 与一上午被合并后又重开的 PR (#2849/#2853) 存在关联，暗示了社区功能需求的迫切性，但总体来看，项目目前正处于一个高强度的功能迭代与安全加固周期，健康度良好。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日共合并/关闭了 **2 个** PR，项目在以下几个方面取得了重要进展：

- **安全修复与加固**：`#2799 [CLOSED]` 已合并，该 PR 修复了一个关键路径遍历漏洞 (CVE-2026-29611)，严格限制了 `send_file` 功能的文件读取范围，防止了被注入后的任意文件读取风险。这对保障运行时的沙箱安全至关重要。
- **功能特性：多Telegram机器人**：`#2849 [CLOSED]` 被合并，标志着“单实例支持多Telegram机器人”的功能得以实现。该特性允许用户通过 `TELEGRAM_BOT_TOKEN_<SUFFIX>` 环境变量，在一个 NanoClaw 进程中运行多个独立的 Telegram 机器人。然而，该 PR 在合并后又被重新打开（见 `#2853`），原因尚不明确，值得后续关注。

### 4. 社区热点

今日社区关注的焦点明确指向 **多机器人实例支持** ：

- **Issue #2852**：用户 `Kwisss` 询问“多Telegram机器人”功能。用户表示该功能曾经存在后被移除，并指出虽然有“实例”支持，但 Claude 无法使其工作，询问该功能是否会再次实现。这直接反映了用户对多账号、多场景并发管理的强烈需求。
- **PR #2849 / #2853**：`grantland` 提交了实现该功能的 PR `#2849`，并已被合并。但随后又提交了几乎相同的 PR `#2853` 并重新打开。这种“合并-重开”的模式可能是由于合并后的代码存在缺陷或需要额外的配置修复，项目维护者可能正在紧急处理相关问题。

### 5. Bug 与稳定性

今日未报告明确的崩溃或回归 Bug，但有两项重要的稳定性与可靠性修复 PR 在进展中：

- **严重 - 测试基础设施不稳定**：`#2851 [OPEN]` 指出了测试框架中的一个严重问题——“废弃的轮询循环”会窃取后续测试的消息，导致测试结果不可靠。该 PR 提供了一个修复方案，以提升测试套件的健壮性。
- **中等 - macOS 代理 API 连接失败**：`#2854 [OPEN]` 解决了在 macOS 使用 Rancher Desktop 时，所有代理 API 调用失败的问题。根本原因是 OneCLI SDK 的网关 CA 包在容器中无法挂载。这影响了 macOS 用户的开发体验。

### 6. 功能请求与路线图信号

今日的功能请求信号明显指向 **扩展性与集成增强** ，多项活跃 PR 预示了下一版本可能包含以下特性：

- **远程MCP服务器支持**：`#2847 [OPEN]` 提出了支持通过 HTTP/SSE 连接到远程 MCP (Model Context Protocol) 服务器的功能，将使 NanoClaw 能够调用非本地的外部服务和数据源。
- **原生Matrix端到端加密**：`#2844 [OPEN]` 是一个重要的重构，用基于 `matrix-bot-sdk` 和原生 Rust 加密绑定的原生适配器，替换了旧有的 WASM 加密桥接，旨在提供稳定、持久的 E2EE (端到端加密) 支持。
- **新增“学习”技能**：`#2843 [OPEN]` 提出了一个 `/learn` 技能，允许用户从任何来源（如目录、URL、粘贴板内容）蒸馏出可重用的技能，这将是项目在“知识管理”和“自我进化”方向上的一个有力补充。

### 7. 用户反馈摘要

今日的用户反馈主要集中在以下方面：

- **痛点：多机器人功能反复**：用户 `Kwisss` 在 Issue #2852 中的反馈表明，多 Telegram 机器人功能经历了“有-移除-有(但不可用)”的过程，这给用户造成了困扰。用户明确表示，如果官方不能稳定提供，他们将“另寻他处”(look elsewhere)。
- **使用场景：Docker-in-Docker**：`#2846 [OPEN]` 修复中提到的对 Docker-in-Docker 的支持，暗示了用户有在代理容器内部再次使用 Docker 或 Podman/nerdctl 等容器工具的需求，这是一种高级的 CI/CD 或开发环境场景。
- **使用场景：参数化查询**：`#2845 [OPEN]` 修复为 `q.ts` 工具添加了位置参数传递，这表明用户正在使用 NanoClaw 进行更复杂的数据操作，需要直接在 CLI 语法中支持 SQL 参数化查询，以提升安全性和便利性。

### 8. 待处理积压

目前在多个以**安全加固**为主题的 PR 上存在积压，这些 PR 来自贡献者 `sturdy4days`，提交于数天前且至今未获得合并或评审反馈。这些修复对于项目的安全性和稳定性至关重要：

- **`#2800 [OPEN]`**：修复 `ncl groups create/update` 命令的目录遍历漏洞 (CWE-22) 和镜像标签固定问题，防止创建跨越预期的 Agent 组。
- **`#2801 [OPEN]`**：对 `safeParseContent` 进行加固，防止路由器在处理 JSON 原始值（如数字、布尔值）时出现逻辑错误。
- **`#2802 [OPEN]`**：对 `ncl` 套接字传输进行安全加固，包括客户端超时、响应缓冲区限制和服务端失败-关闭等机制。
- **`#2750 [OPEN]`**：修复因容器被杀导致 `outbound.db` WAL (预写式日志) 损坏，以及因热日志轮询竞争导致的数据丢失问题，这是一个长期存在的关键稳定性问题。

**建议：** 项目维护者应优先评审并合并上述 `sturdy4days` 的安全加固 PR 队列，以降低潜在风险。同时，应尽快对“多 Telegram 机器人”功能的“合并-重开”情况进行说明，以避免社区用户因困惑而流失。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是根据您提供的 IronClaw 项目 GitHub 数据生成的 2026-06-25 项目动态日报。

---

# IronClaw 项目动态日报 — 2026-06-25

## 1. 今日速览

今日项目活跃度极高，社区修复与核心开发工作同步密集推进。核心亮点在于成功定位并修复了 `Reborn` 运行时在 2026-06-24 发生的严重熔断故障（大规模 `lease_expired`），相关 `fix` PR 已迅速提交。此外，`Reborn` 内存层重构（`#3537`）迎来里程碑式进展，其核心 PR `#5163` 已被合并。同时，社区报告了一批新的 Bug，主要集中在 `Reborn WebUI` 的工具权限与 UI 体验一致性上。总体而言，项目正处于“修复合并、架构演进与密集测试”的高度活跃周期。

## 2. 版本发布

**无。** 过去 24 小时内未发布任何新版本。

## 3. 项目进展

- **内存层重构（`#3537`）迈出关键一步**：核心 PR `#5163` 已被合并。该 PR 将 `Reborn` 的内存层从内核中解耦，并抽取为两个独立的、与供应商无关的 crate（`ironclaw_memory` 和 `ironclaw_memory_native`），为未来内存系统的可插拔和可扩展性奠定了基础。
    - [PR #5163 - feat(memory): model memory as a userland extension (#3537)](https://github.com/nearai/ironclaw/pull/5163)

- **修复 2026-06-24 运行时熔断故障**：针对昨天发生的 `Reborn` 运行时大规模超时和冻结问题，团队迅速定位了根因并提交了修复 PR `#5204` 和 `#5206`，分别解决 NEAR AI 调用超时和 WASM 执行占用 Tokio 工作线程的问题。
    - [PR #5204 - fix(reborn): bound NEAR AI provider calls below the runner lease](https://github.com/nearai/ironclaw/pull/5204)
    - [PR #5206 - fix(reborn): stop WASM execution from starving the tokio worker pool](https://github.com/nearai/ironclaw/pull/5206)

- **CI 回归**：PR `#5193` 被合并，修复了因 CI 配置文件（YAML）重复键和测试用例遗漏导致的 `main` 分支 CI 失败问题，确保了代码库的健康状态。
    - [PR #5193 - fix(ci): restore green main — duplicate workflow key + missed spawn_subagent test ignore](https://github.com/nearai/ironclaw/pull/5193)

## 4. 社区热点

- **#5169: 捆绑技能因 API 关键词触发安全拦截**：此问题成为今日最受关注的社区 Bug。用户在全新安装的 `Reborn` 上，因捆绑技能中包含 `Authorization`、`Bearer` 等正常 API 词汇而触发提示安全拒绝列表，导致会话意外中断，体验极差。反映了模型安全策略与产品功能之间的潜在冲突。
    - [Issue #5169 - Bundled skills trip the prompt-safety vocabulary denylist](https://github.com/nearai/ironclaw/issues/5169)

- **#5190 - #5192, #5196: 多起 WebUI 工具审批流程 Bug**：社区成员 `sunglow666` 报告了一系列关于 `Reborn WebUI` 中工具权限设置的 Bug，如“拒绝后仍请求授权”、“权限设置为‘每次询问’时批准失败”、“禁用工具后助手调用无关工具”等。这表明 WebUI 的工具权限生命周期管理是一个亟待完善的核心环节。
    - [Issue #5192 - [Reborn] Denying a tool approval can still lead to additional tool approval requests](https://github.com/nearai/ironclaw/issues/5192)
    - [Issue #5196 - [Reborn] “Ask each time” tool permission may fail with authorization error](https://github.com/nearai/ironclaw/issues/5196)

## 5. Bug 与稳定性

- **严重 Bug：运行时大规模冻结与超时**（已修复）
    - **描述**：`Reborn` 运行时在并发场景下出现约 4 分钟的全流程冻结，随后进程重启并伴随大量 `lease_expired` 错误。根因是 NEAR AI 调用缺乏超时控制与 WASM 执行阻塞 Tokio 线程池。
    - **PR**：[#5204](https://github.com/nearai/ironclaw/pull/5204), [#5206](https://github.com/nearai/ironclaw/pull/5206)

- **中等 Bug：WebUI 多租户日志不可访问**（已有 Fix PR）
    - **描述**：多租户用户在 WebUI 中无法查看操作日志，影响了 UI 端的调试和多租户运营。
    - **PR**：[#5199 - fix(reborn): allow web ui logs for multi-tenancy users](https://github.com/nearai/ironclaw/pull/5199)

- **中等 Bug：WebUI 工具审批流程异常**（无 Fix PR）
    - **描述**：当工具被设为“禁用”或“每次询问”时，助手行为异常，可能做出预期外的工具调用或重复发起审批请求，导致流程混乱。
    - **Issues**：[#5192](https://github.com/nearai/ironclaw/issues/5192), [#5196](https://github.com/nearai/ironclaw/issues/5196), [#5197](https://github.com/nearai/ironclaw/issues/5197)

- **低严重 Bug：WebUI 令牌无效时表现异常**（无 Fix PR）
    - **描述**：使用无效的 UI 承载令牌进入应用，UI 外壳正常加载，但后续操作无响应，未弹出明确的认证错误提示。
    - **Issue**：[#5190 - [Reborn WebUI] Invalid UI bearer token enters app but later actions do not respond](https://github.com/nearai/ironclaw/issues/5190)

## 6. 功能请求与路线图信号

- **Reborn 托管观测性**：开发者 `serrrfirat` 提出了 `Reborn` 托管环境下的可观测性需求（Issue #5182），期望在二进制之外能获得有意义的日志和故障诊断。考虑到多个核心贡献者也对类似痛点有贡献，此功能很可能在下一版本中被规划。
    - [Issue #5182 - [enhancement, scope: channel/cli] Reborn hosted observability](https://github.com/nearai/ironclaw/issues/5182)

- **内存功能持续集成**：在 `#5163` 合并后，贡献者 BenKurrek 立即提交了跟进 PR `#5205` 和 `#5165`，分别聚焦于“宿主拥有上下文清理”和“可选原生内存种子注入”。这表明内存层的功能完善是近期的开发重点，并可能在接下来的小版本中持续交付。
    - [PR #5205 - feat(memory): host-owned context sanitization + boundary allowlist + profile read facade](https://github.com/nearai/ironclaw/pull/5205)
    - [PR #5165 - feat(reborn): optional native memory seeding on the composition build path](https://github.com/nearai/ironclaw/pull/5165)

## 7. 用户反馈摘要

- **满意度**：核心开发者对于 2026-06-24 熔断故障的快速响应（24小时内提交修复 PR）展现了高度的技术责任感和迭代效率，是积极信号。
- **痛点**：多个用户报告了 WebUI 工具权限和审批流程的 Bug (`#5192`, `#5196` 等)，表明该功能的实现与用户期望的行为仍有差距，稳定性与用户引导是主要痛点。
- **使用场景**：一个常见使用场景是创建自动化任务来监控 GitHub 仓库动态 (Issue #4986, #5192 的复现 Prompt)。用户期望助手能准确理解意图并可靠执行，任何审批流程的异常都会严重破坏该场景的体验。

## 8. 待处理积压

- **#4986: Recurring automation can become permanently blocked waiting for tool approval**：此 Issue 已存在 8 天，描述了一个可能导致自动化流程永远阻塞的严重问题。鉴于工具审批流程正是当前社区反馈的集中痛点，建议项目维护者优先关注并评估该问题。
    - [Issue #4986 - [bug] [Reborn] Recurring automation can become permanently blocked waiting for tool approval](https://github.com/nearai/ironclaw/issues/4986)

- **#4108: Nightly E2E failed**：该 Issue 已存在近一个月，由 GitHub Actions 自动上报。虽然可能是偶发性故障，但持续未结可能掩盖了更多回归问题。建议维护者确认其根本原因或添加跳过/重试逻辑，以避免干扰正常的 CI 信号监控。
    - [Issue #4108 - Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的数据，为您生成一份关于LobsterAI项目的动态日报。

---

# LobsterAI 项目动态日报 (2026-06-25)

## 1. 今日速览

项目今日活跃度极高，主要体现为大量历史PR的集中合并与关闭，而非新功能的涌现。过去24小时内，共有**43条PR更新**，其中**41条已合并/关闭**，2条待合并，表明项目维护者正在进行一次大规模的代码库清理和稳定化工作。相比之下，Issue活跃度较低，仅1条长期未解决的Bug被重新标记。总体而言，项目当前阶段侧重于**内部质量改进和Bug修复**，功能迭代节奏暂时放缓，健康度良好但处于“消化”阶段。

## 2. 版本发布

*无新版本发布。*

## 3. 项目进展

今日项目取得了显著的稳定性进展，主要集中在 **OpenClaw 网关**、**CoWork 协作模式**和 **IM 即时消息** 等核心模块。大量来自 `fisherdaddy` 和 `liuzhq1986` 的PR被合并，修复了多个长期存在的问题。

**核心修复包括：**
- **OpenClaw 网关稳定性**：修复了因GitHub Copilot令牌刷新导致网关重启的问题 (#2043)，并优化了网关在macOS/Linux下的启动方式，避免了Electron将Node脚本误判为应用路径的错误 (#2195, #2196)。
- **引擎循环与Token消耗**：修复了工具循环在中断时持续消耗Token的Bug (#2049, #2051)，以及会话冻结问题 (#2047)，这对降低用户在大模型使用中的成本至关重要。
- **CoWork 协作模式**：优化了历史兜底机制，避免了最终助手前缀重复的问题 (#2197)，并收紧了短最终答案的宽限期 (#2058)。
- **其他稳定性**：修复了会话`patch`超时导致的聊天阻塞 (#2050)、更新后微信Bug (#2086)、LLM流式输出空数据 (#2048) 等问题。

**共有41个PR被合并/关闭，这相当于将所有近期积累的热修复和优化一次性合入主线，大幅提升了项目主干的健壮性。**

## 4. 社区热点

今日讨论热度最高的是 **Issue #1394：定时任务不重复执行后被自动删除**。该Issue已有一个多月历史，但在今日被维护者标记为`[stale]`（陈旧的）并更新了状态，说明开发团队已经开始关注并可能计划处理此问题。

- **链接**: [Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)
- **诉求分析**: 用户的核心诉求是 **“可编辑的、一次性任务”** 的持久化保存。用户希望创建一个“仅运行一次”的任务，执行完毕后保留其配置以便未来编辑复用，而不是自动删除。这反映出用户对LobsterAI的定位已从简单的自动化执行工具，延伸到**工作流的编排与管理平台**，期望任务具备状态管理和版本复用的能力。

## 5. Bug 与稳定性

今日修复了大量历史Bug，但也存在一个关键的、长期未解决的Bug。

| 严重程度 | Bug 描述 | 链接 | 是否有 Fix PR？ |
| :--- | :--- | :--- | :--- |
| **高** | 不重复执行的定时任务在运行一次后会被**永久删除**，用户期望保留任务配置。 | [Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394) | 暂无 |
| **中** | 修复：工具循环被中止后持续消耗Token（Token燃烧）。 | [PR #2049](https://github.com/netease-youdao/LobsterAI/pull/2049) | 已合并 ✅ |
| **中** | 修复：OpenClaw网关因Copilot令牌刷新而重启。 | [PR #2043](https://github.com/netease-youdao/LobsterAI/pull/2043) | 已合并 ✅ |
| **中** | 修复：会话`patch`超时导致聊天发送阻塞。 | [PR #2050](https://github.com/netease-youdao/LobsterAI/pull/2050) | 已合并 ✅ |
| **低** | 修复：LLM流式输出中包含空数据。 | [PR #2048](https://github.com/netease-youdao/LobsterAI/pull/2048) | 已合并 ✅ |
| **低** | 修复：CoWork模式下历史兜底导致助手前缀重复。 | [PR #2197](https://github.com/netease-youdao/LobsterAI/pull/2197) | 已合并 ✅ |

## 6. 功能请求与路线图信号

- **定时任务的持久化与编辑**：Issue #1394 是一个强烈的功能请求信号。虽然当前没有PR直接关联，但该Issue的活跃和`Open`状态表明，其被纳入后续版本开发的可能性正在增加。这可能是未来`Scheduler`模块迭代的重点方向。
- **模型与环境支持**：从历史PR中可看出，项目持续关注模型生态。例如，PR #2102 合入了对 `mimo v2.5` 模型的支持，并修复了用户自定义上下文窗口的配置问题。这表明项目致力于保持对主流和新模型的前沿兼容性。

## 7. 用户反馈摘要

- **用户痛点**：Issue #1394 的用户明确表达了对于一次性任务自动删除的不满，称“**这次跑过之后也许下次还需要用**”。这表明用户需要一个更灵活的任务管理机制，而不是一次性的“发射后不管”。
- **用户场景**：用户正在使用LobsterAI进行日常的、周期性的任务编排，希望通过“不重复”的选项创建一份可复用、可调整的“任务模板”。
- **满意点**：虽然今日无直接的正面表扬，但合并大量修复PR意味着开发团队正在积极响应用户反馈（如“Token燃烧”问题），这间接提升了用户对项目解决问题的信心。

## 8. 待处理积压

当前最主要的积压问题为 **Issue #1394**，该问题已存在近3个月，且涉及用户核心数据（任务配置）的持久化安全。建议维护者在接下来的迭代中优先评估此问题，并规划对应的`fix`或`feat`分支。

- **问题**: 定时任务（不重复）执行后自动删除
- **链接**: [Issue #1394](https://github.com/netease-youdao/LobsterAI/issues/1394)
- **状态**: Open，已被标记为 `[stale]`
- **提醒**: 此问题若长期不解决，可能影响用户对`Scheduler`功能的信任度，并降低低频率、高价值任务的使用体验。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据您提供的 TinyClaw (TinyAGI/tinyagi) 项目数据，为您呈上 2026-06-25 的项目动态日报。

---

## TinyClaw 项目日报 | 2026-06-25

### 1. 今日速览

今日项目活跃度较低，过去24小时未产生新的 Issue 讨论和版本发布。项目状态稳定，主要进展集中在昨日合并的 `#281` PR 上，该 PR 修复了多个关键的 Windows 平台兼容性问题。总体来看，项目处于一次小幅但重要的健康度修复之后，社区交流平静，核心开发活动不活跃。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日项目向前推进的唯一步骤是 Pull Request `#281` 被合并并关闭。该 PR 解决了 CLI 工具在原生 Windows 环境下（非 WSL）无法运行的三个关键 Bug，显著提升了项目的跨平台可用性。

-   **PR #281 (已合并/关闭): fix: Windows cross-platform support in CLI**
    -   **贡献者**: mperkins0155
    -   **核心修复**:
        1.  **修复了 Windows 下 `import.meta.url` 返回路径 `/C:/Users/...` 导致 `MODULE_NOT_FOUND` 的问题**：通过改进路径解析逻辑，消除多余斜杠，确保 Node.js 能正确加载模块。
        2.  **修复了其他两个未在摘要中详细说明的 Windows 特有 Bug**。
    -   **意义**: 解决了项目早期版本中 Windows 用户入门门槛高的问题，使 TinyClaw 能够覆盖更广泛的开发者群体，是项目从“Mac/Linux only”向“真正跨平台”迈出的关键一步。

### 4. 社区热点

今日无活跃的 Issue 或 PR 讨论。已关闭的 PR `#281` 是近期唯一受到关注的 PR，其“跨平台支持”的核心诉求反映了社区对于提升 Windows 使用体验的潜在需求。由于该项目目前阶段参与者较少，社区讨论氛围冷静。

### 5. Bug 与稳定性

今日无新报告的 Bug。昨日合并的 PR `#281` 已经修复了此前存在的 Windows 专用 CLI Bug，这些问题已归类为“已解决”。

当前无已知、待修复的严重稳定性问题。

### 6. 功能请求与路线图信号

今日未收到新的功能请求。PR `#281` 的顺利合并表明当前项目的阶段性重点在于优化现有基础设施的稳定性和兼容性，而非引入全新功能。下一个版本预计会主要包含此次的 Windows 修复，以及此前可能积压的其他小规模修复。

### 7. 用户反馈摘要

今日无新的用户反馈。从已关闭的 PR `#281` 的提交历史来看，贡献者 `mperkins0155` 的核心痛点是：“在原生 Windows 上使用 `tinyagi` 时，因路径解析逻辑导致 CLI 根本无法启动”。这表明早期的用户或贡献者已尝试在 Windows 环境部署，但遇到了阻碍。该 PR 的合并将直接解决这一痛点。

### 8. 待处理积压

当前项目 Issue 和 PR 积压量为零。项目维护状态良好，无长期未响应的重要议题需提醒关注。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的CoPaw项目GitHub数据，我为您生成了以下项目动态日报。

---

# 🤖 CoPaw 项目动态日报 | 2026-06-25

**项目名称:** CoPaw (github.com/agentscope-ai/CoPaw)
**数据时间范围:** 2026-06-24 至 2026-06-25 (UTC)
**分析师:** AI 智能体 & 个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

今日CoPaw项目社区活跃度较高。Issue数量激增，达到23条，但大部分为新的Bug报告与功能请求，关闭率仅有34.8%。PR方面，合并/关闭活动相对平淡（6/50），但待合并PR高达44条，反映出项目团队内部有大量代码变更等待处理。社区讨论主要集中在**自定义模型提供商兼容性、用户消息时间戳设计、以及前端性能问题**上。整体来看，项目处于**高社区反馈、低合并吞吐**的状态，建议团队优先处理高危Bug和积压PR。

---

### 2. 版本发布

**无新版本发布。**

---

### 3. 项目进展

今日项目向前迈进的步伐较为缓慢，仅有少数重要PR被合并或关闭。

- **[修复] 用户消息时间戳设计改进 (PR #5498, CLOSED)**
  - **摘要:** 该PR将当前日期信息从静态的系统环境上下文中移除，改为动态地添加到每条用户消息的前缀中。这解决了长会话中系统时间信息可能过时的问题，并能提升提示缓存的稳定性。
  - **影响:** 改善多轮对话的用户体验和AI对时间感知的准确性。
  - **链接:** [PR #5498](https://github.com/agentscope-ai/QwenPaw/pull/5498)

- **[修复] 构建失败与基础功能回归 (PR合并未知，但从Issue关闭推断)**
  - **摘要:** 多个已关闭的Bug (如 #5373 Shell特殊字符解析、#5264 飞书群聊回复问题) 表明对应的修复PR已被合入。
  - **影响:** 恢复了Shell命令执行和飞书频道消息交互的核心功能。
  - **相关链接:** [Issue #5373](https://github.com/agentscope-ai/QwenPaw/issues/5373), [Issue #5264](https://github.com/agentscope-ai/QwenPaw/issues/5264)

---

### 4. 社区热点

今日社区讨论最活跃的话题集中在模型集成与用户体验设计上。

1.  **讨论热点：自定义OpenAI兼容提供商的工具调用问题**
    -   **Issue:** [#5345 [Bug]: Custom OpenAI-compatible providers (e.g. OMLX) don't support function calling](https://github.com/agentscope-ai/QwenPaw/issues/5345) (8条评论)
    -   **分析:** 此Bug报告是今日最活跃的Issue。用户在使用非标准OpenAI兼容API（如OMLX）时，无法触发函数调用。Ollama原生支持，说明可能是QwenPaw在解析自定义提供商API响应时存在缺陷。这暴露了项目在**模型供应商兼容性层**上的一个薄弱环节，限制了用户的选择范围，可能是一个影响广泛的普遍性问题。

2.  **设计讨论：用户消息的时间戳应如何放置？**
    -   **Issue:** [#5455 [Question]: Why not make the current time a per-user-message prefix…](https://github.com/agentscope-ai/QwenPaw/issues/5455) (4条评论)
    -   **分析:** 该Issue引发了关于“当前时间”应放置在环境上下文（静态）还是用户消息前缀（动态）的深入讨论。这直接关系到AI模型对时间信息的理解准确性以及提示缓存的效率。该讨论在一天内迅速产生了修复PR（#5498），反映出社区对该问题的共识度较高。

---

### 5. Bug 与稳定性

今日报告的Bug数量较多，以下按严重程度列出关键问题：

**严重 (高)**
- **报告: 前端在大会话/大量工具调用时崩溃**
  - [#5479] [Bug]: 大会话文件（>500KB）打开报错：渲染此页面时发生了意外错误 (2条评论)
  - [#5401] [Bug]: Console: session with large tool-use history fails to render (3条评论)
  - **分析:** 社区连续报告了两个导致前端完全崩溃的Bug，均与渲染大量数据（文本或工具调用）有关。这表明前端在处理大规模会话数据时存在**内存或渲染性能瓶颈**，是该版本最严重的稳定性问题。
   - **链接:** [#5479](https://github.com/agentscope-ai/QwenPaw/issues/5479), [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401)

- **报告: 多通道/多Agent身份错乱**
  - [#5456] [Bug]: Wrong agent identity for channel-built requests (2条评论)
  - **分析:** 用户在使用非默认Agent时，上下文中的Agent ID被错误设置为“default”。这是一个严重的**逻辑错误**，可能导致用户在与不同Agent对话时，模型行为完全混乱。
   - **链接:** [#5456](https://github.com/agentscope-ai/QwenPaw/issues/5456)

**中等**
- **报告: Python环境问题与安装后无法启动**
  - [#5379] [Bug]: 通过Python命令安装后启动，直接报错Internal Server Error (5条评论)
  - [#5317] [Question]: window tauri下，找不到python了 (已关闭)
  - **分析:** 这类与环境配置相关的错误对新用户极不友好，会严重影响项目的入门体验。**链接:** [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379)

- **报告: 模型兼容性问题**
  - [#5472] [Bug]: 用opencode go套餐里的glm系列模型报错 (1条评论) — **已有Fix PR #5496**
  - [#5373] [Bug]: Shell command execution fails to parse shell special characters (已关闭)
  - **分析:** 对特定模型（GLM）和系统指令（Shell）的兼容性修复已跟进。
  - **链接:** [#5472](https://github.com/agentscope-ai/QwenPaw/issues/5472)

**低 (UI/UX)**
- **报告: 前端排版与UI问题**
  - [#5480] 长消息排版错乱、[#5501] 发送按钮对不齐、[#5476] 移动端无法切换智能体。
  - **分析:** 这些是影响用户日常使用体验的“刺”。虽然不致命，但会降低专业度。

---

### 6. 功能请求与路线图信号

用户近期提出了多个有价值的功能请求，部分已有对应PR，反映出项目可能的发展方向。

1.  **支持通过PyPI安装插件** — **高潜力**
    - **请求:** [#5484 feat: Support installing plugins via pip from PyPI](https://github.com/agentscope-ai/QwenPaw/issues/5484) (1条评论)
    - **对应PR:** [#5492](https://github.com/agentscope-ai/QwenPaw/pull/5492) (已创建)
    - **分析:** 这是一个非常重要的生态建设功能。将插件系统从目前仅支持ZIP扩展至标准PyPI，将极大降低第三方开发者贡献和用户安装插件的门槛，是项目走向成熟的关键一步。该PR为第一时间提交，说明开发者对此需求高度认同。

2.  **支持OpenAI Response Format API**
    - **请求:** [#5489](https://github.com/agentscope-ai/QwenPaw/issues/5489) (1条评论)
    - **分析:** 这表明有用户希望使用OpenAI最新的响应格式，用于结构化的输出或流式处理。这是一个前沿需求，可能对特定场景的用户有吸引力。

3.  **优化MCP工具名称显示**
    - **请求:** [#5231](https://github.com/agentscope-ai/QwenPaw/issues/5231) (1条评论)
    - **分析:** 用户希望MCP工具在界面显示人类可读的原始名称，而调用时使用清洗后的名称。这有助于提升聊天界面的易用性和可读性。

---

### 7. 用户反馈摘要

从今日的Issues评论中，可以提炼出以下用户反馈：

- **痛点多发于兼容性与性能：** 用户报告的问题高度集中在三个方面：**1) 非标准OpenAI API的兼容性** (`#5345`，用户表达了对“自定义提供商支持不完整”的失望)；**2) 大型会话的性能瓶颈** (`#5479`, `#5401`，用户反馈页面直接崩溃，影响正常使用)；**3) 高内存占用** (`#5441`，用户抱怨“刚启动，什么都没做，内存占用已经1.4g了”)。
- **特定使用场景的受阻：** 飞书和钉钉的渠道用户遇到了功能性问题 (`#5264`, `#5177`)，显示出多平台适配仍有待完善。
- **安装与入门障碍：** 新用户遇到了内网安装白屏 (`#5497`) 和Python环境找不到等问题 (`#5317`, `#5379`)，反映出文档和开箱即用体验需要优化。
- **积极贡献的社区：** 社区不仅提出问题，还积极参与设计讨论 (`#5455`)，并贡献了高质量的功能代码 (`#5484` -> `#5492`)，显示出社区的积极性和健康度。

---

### 8. 待处理积压

以下是需要社区维护者关注的长期未解决或重要的积压问题：

- **长周期PR待定**
  - **[环境]** [PR #4669 feat(desktop): add tauri auto updater](https://github.com/agentscope-ai/QwenPaw/pull/4669)
    - **状态:** 创建于2026-05-25，距今整1个月，更新于2026-06-24，仍处于Open状态。
    - **重要性:** 高。Tauri桌面端自动更新功能对于桌面用户至关重要，确保用户能够方便地获取最新功能和修复。此PR长期未合并，可能意味着架构或构建流程上存在阻碍。

- **重要功能请求无明确回应**
  - **[功能]** [Issue #5231 [Feature]: MCP 工具名称在聊天界面显示原始名称，以及文件卡片默认展开优化](https://github.com/agentscope-ai/QwenPaw/issues/5231)
    - **状态:** 创建于2026-06-16，已有1条评论，但官方无明确回复。
    - **重要性:** 中。优化UI体验的合理请求。长期未回应可能会打击用户的贡献热情。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是为您生成的 ZeroClaw 项目 2026-06-25 日报。

---

## ZeroClaw 项目动态日报 — 2026-06-25

### 1. 今日速览

项目今日保持 **极高活跃度**，24小时内产生100条Issue与PR更新，社区参与热情高涨。安全与架构相关的大规模特性讨论（如OIDC认证、RBAC、WASM插件生态）占据了主导地位，表明项目正从核心功能向企业级安全和可扩展性迈进。值得关注的是，关于Telegram频道的功能性Bug修复（如图片处理、提及模式）和大量针对OpenRouter模型后备及本地认证等功能性PR的提交，显示出社区对实际使用场景的强烈关注。维护者在积极回应Issues，但大量待合并PR也暗示了维护者带宽可能面临挑战。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无PR被合并到主分支，但多个重要PR处于待合并状态，其中一些修复了紧急Bug，标志着项目在稳定性和功能上的持续改进：

- **`#8285` [OPEN]**: 修复了`delegate`（委派）模式下，被委派的子Agent未继承父Agent的`SecurityPolicy`，导致工具权限绕过的安全漏洞。这是对多层级Agent安全隔离的关键修复。
- **`#7771` [OPEN]**: 显著改进了可观测性，确保 `channel`、`agent_alias` 和 `turn_id` 等关键元数据在Agent生命周期的所有事件中都能正确传递，为链路追踪提供坚实基础。
- **`#8145` [OPEN]**: 在18+个频道中统一了“正在输入”状态的正确实现，并修复了`ack`反应过早发出的问题，改善了终端用户的交互体验。
- **`#8033` [OPEN]**: 重构了`zeroclaw onboard`命令，将其转化为一个对话式、基于聊天的设置向导，极大地降低了新用户的上手门槛。
- **`#7723` 和 `#7958` [OPEN]**: 两个PR均修复了Telegram群组中`mention_only`模式的痛点：当用户回复Bot自己的消息时，现在可以正确触发机器人响应，无需再@提及。

### 4. 社区热点

今日讨论最活跃的Issue主要围绕两大主题：**安全架构** 和 **插件生态**。

- **`#5982` [Feature]: Per-sender RBAC for multi-tenant agent deployments (9条评论)**
  链接：`zeroclaw-labs/zeroclaw Issue #5982`
  核心诉求：用户迫切需要一个基于消息发送者的细粒度权限控制模型，以实现单一实例服务多类用户（如客户、运维、开发者），并隔离其工作空间和工具集。这表明项目正被用于更复杂的多租户场景，社区希望获得商业级的安全能力。

- **`#7141` [Feature]: OIDC Authentication Provider support (6条评论)**
  链接：`zeroclaw-labs/zeroclaw Issue #7141`
  核心诉求：作为企业级安全的关键拼图，用户希望集成标准的OIDC身份认证，以对接企业已有的身份系统（如Keycloak、Okta），消除对本地密码的依赖。

- **`#8177` RFC: Supply chain signing - hardware PGP, hermetic builds, and SLSA provenance (5条评论)**
  链接：`zeroclaw-labs/zeroclaw Issue #8177`
  核心诉求：社区对软件供应链安全的关注度极高。该RFC提出了构建工件（二进制、容器镜像）的硬件签名、可重现构建、SLSA溯源等一系列安全加固方案，反映了项目作为关键基础设施的定位。

### 5. Bug 与稳定性

今日报告了多个与安全、性能和数据一致性相关的严重Bug。

- **严重（S1/S2级别）**
    - **`#8151` [CLOSED] deferred image attachment loses its re-loadable reference in cached history**: 工作流受阻。用户发送图片后，Agent因故推迟处理，但后续请求时Agent却无法“看到”该图片。该问题已在当日被关闭，修复方式值得关注。
    - **`#7733` [OPEN] mcp_bundles is parsed and shown in Config but never enforced at runtime**: 安全配置静默失效。`mcp_bundles`的权限隔离配置在解析后未被运行时强制执行，这意味着用户以为的安全隔离实际上是“no-op”，是严重的功能与预期不符的缺陷。
    - **`#7623` [OPEN] delegate to a Codex/OAuth sub-agent still fails**: 委派子Agent时，API Key依然会泄漏，导致需要不同认证的底层模型调用失败。这是对跨Agent认证隔离的持续挑战。

- **中等（S3级别）**
    - **`#5514` [OPEN] Agent request appends each subsequent image in each request on Telegram**: 用户在Telegram发送多张图片时，每张图片都会触发一个独立的Agent请求，而非合并处理。这不仅造成体验割裂，也浪费了Token资源。

### 6. 功能请求与路线图信号

社区提出的新功能请求与项目的发展路线图高度契合。

- **可能进入下一版本**
    - **OpenRouter Model Fallbacks**: `#8138` 和对应的PR `#8141`、`#8207` 请求支持OpenRouter的原生模型降级阵列。由于已有多个PR实现，该功能集成度极高，很可能被快速合并。
    - **Per-agent Custom Environment Variables**: `#8226` 请求为不同Agent配置不同的环境变量和密钥，以解决多租户场景下的工具配置隔离问题。这是对`#5982` RBAC功能的补充。
    - **Local Username/Password AuthProvider**: `#8076` 作为`#7141` OIDC的子任务，请求一个无需外部IdP的本地认证方案，以满足小型部署或开发环境需求。

- **长期路线图信号**
    - **“Everything is a plugin”**: `#6489` 提出了一个宏伟的架构愿景，将所有集成（频道、AI提供商、内置工具）统一到插件目录下。这将是项目未来的重大重构方向。
    - **WASM-first Plugin Runtime**: `#8135`、`#8187`、`#7822` 等多个RFC和Issue集中探讨了以WebAssembly为核心的插件运行时，涵盖能力、生命周期钩子和安全分发，表明WASM将是项目插件生态的核心技术栈。

### 7. 用户反馈摘要

- **痛点**:
    - **Telegram频道的图片处理问题**: 用户对发送多图时的“一次请求一张”和“图片在历史中丢失”的行为表达了不满，这严重影响了基础的多模态交互体验。 (`#5514`, `#8151`)
    - **MCP子进程泄漏**: 用户报告`heartbeat`机制会导致MCP stdio子进程持续泄漏，如果不重启守护进程，系统资源终将被耗尽。 (`#5903`)
- **使用场景**:
    - **多租户部署**: 多个用户 (如`metalmon`, `susyabashti`) 表达了对多租户安全隔离功能的强烈需求，他们希望用一个实例服务不同的用户群体或业务线。 (`#5982`, `#8226`)
    - **企业级集成**: 用户希望与标准企业身份系统（OIDC）和基础设施（如OpenRouter）集成，这表明ZeroClaw正被评估用于更正式的生产环境。 (`#7141`, `#8138`)

### 8. 待处理积压

以下是一些长期未关闭但至关重要的问题，建议维护者优先关注。

- **`#5607` [Feature] pre-hook skip gates for cron jobs and SOP triggers (状态: blocked)**
  链接：`zeroclaw-labs/zeroclaw Issue #5607`
  **重要性**: 中等 (P2) | **积压原因**: 被标记为`blocked`。该功能允许为定时任务添加轻量级前置检查，是实现运维自动化和条件触发的基础能力。其阻塞依赖关系需要被识别和解决。

- **`#5903` [Bug] MCP stdio child processes accumulate on daemon (状态: accepted)**
  链接：`zeroclaw-labs/zeroclaw Issue #5903`
  **重要性**: 高 (P1) | **积压原因**: 尽管被接受，但目前尚无关联的修复PR。这是一个明确的资源泄漏Bug，会导致守护进程长期运行后不稳定，应优先分配维护者资源进行修复。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*