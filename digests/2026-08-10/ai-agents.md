# OpenClaw 生态日报 2026-08-10

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-10 00:45 UTC

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

# OpenClaw 开源项目动态日报

**日期：2026-08-10** | **数据来源：github.com/openclaw/openclaw**


## 1. 今日速览

过去 24 小时，OpenClaw 项目保持高强度迭代，共产生 **500 条 Issue 更新**（其中 428 条活跃、72 条关闭）和 **500 条 PR 更新**（319 条待合并、181 条已合并/关闭）。昨日关闭的高热度 Issue #116277（DeepSeek v4 Flash 静默回复失败，196 条评论）今日已被用户以新 Issue #121058 重新打开，说明该问题**尚未真正解决**，存在复发风险，是当前项目健康度的主要隐患。稳定性类问题（消息丢失、会话状态损坏、重启风暴）持续占据 Issue 榜前列，同时 UI/UX 类 PR 密集提交（Control UI 配对流程、模型选择器、游标约定等），显示项目正双线推进：**一边修复核心运行时可靠性，一边打磨终端用户体验**。

> 活跃度评级：**🔥🔥🔥🔥🔥 极高**（Issue 与 PR 均达单日上限 500 条，社区参与度处于峰值）


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日共合并/关闭 181 个 PR，以下为关键推进（含昨日关闭的 Issue 关联）：

| 状态 | PR/Issue | 内容 | 意义 |
|---|---|---|---|
| ✅ 已关闭 | #116277 | DeepSeek v4 Flash 静默回复失败 | 曾为社区最热 Issue（196 条评论），但关闭后问题复发（见 #121058），**修复有效性存疑** |
| 🔀 已合并 | — | 181 个 PR 合并/关闭 | 涉及文档、UI 修复、代码重构等，保持高频迭代节奏 |
| 🚧 待合并 | #121294 | fix(agents): preserve rate-limit retries without a fallback model | 修复无备用模型时限流重试次数被静默吞掉的问题，由核心维护者 steipete 提交 |
| 🚧 待合并 | #121273 | refactor: replace exec approvals lease with journal CAS | 用事务性 CAS 替代分布式租约作为变更围栏，架构层面优化 |
| 🚧 待合并 | #121300 | chore: detect export name collisions | 预防性工具，检测跨模块导出名冲突（如 `parseFrontmatter` ×4） |

**关键观察**：核心维护者 **steipete** 今日提交了至少 6 个 PR（#121289、#121298、#121273、#121300、#121292、#121294、#121091），覆盖 agents、gateway、telegram、UI 多个模块，且均已关闭/待合并，显示维护团队正在集中清理技术债与架构优化。


## 4. 社区热点

今日最受关注的问题与讨论：

### 🥇 #116277（已关闭）/ #121058（新开）— 196+19 条评论
**DeepSeek v4 Flash 静默回复失败 — 关闭后复发**
- **链接**: [#116277](https://github.com/openclaw/openclaw/issues/116277) / [#121058](https://github.com/openclaw/openclaw/issues/121058)
- **现象**: 模型静默不回复，仅发布 "No reply was generated" 通用回退消息
- **用户诉求**: 用户 sloptop-the-terrible 连续提交两个 Issue，监控 cron 仍在持续记录新故障，**用户对修复效果强烈不满**（"it keeps happening"）。该问题已从单纯 Bug 演变为**信任危机**。

### 🥈 #92201 — 21 条评论（🦪 silver shellfish）
**嵌入式 runner 流式思考签名在重放时间歇性无效（Anthropic）**
- **链接**: [#92201](https://github.com/openclaw/openclaw/issues/92201)
- **现象**: Slack 插件的嵌入式 agent runner 间歇性持久化无效的 Anthropic thinking blocks，且恢复包装器因错误文本被泛化而无法触发
- **影响**: 会话状态损坏、消息丢失，已开放近 2 个月未修复

### 🥉 #22438 — 19 条评论（🌊 off-meta tidepool）
**分层引导文件加载（Tiered bootstrap file loading）功能请求**
- **链接**: [#22438](https://github.com/openclaw/openclaw/issues/22438)
- **诉求**: 大型工作区用户每次会话加载全部引导文件浪费大量 token，希望按需分层加载。该请求已开放近 6 个月，仍处于 needs-maintainer-review 状态。

**用户情绪分析**：热点集中在 **"静默失败"** 类问题上 —— 模型不回复、工具无输出、进程静默死亡。这类问题的共同痛点是 **用户无法区分"正在思考"和"已经失败"**，导致信任度下降和排障困难。


## 5. Bug 与稳定性

今日报告/活跃的 Bug 按严重程度排序：

### 🔴 P0 — 发布阻断
| Issue | 标题 | 状态 |
|---|---|---|
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | **Live Docs 领先于发布版本**（Heartbeat IsolatedSessions 配置在文档中存在但 2026.3.13 版本不支持） | 开放，10 条评论，4 👍 |

### 🟠 P1 — 高优先级
| Issue | 标题 | Fix PR | 备注 |
|---|---|---|---|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | Silent reply failures 复发（#116277 关闭后） | ❌ 无 | **24h 内新增**，复发型，用户监控 cron 持续报告 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook 生成 CPU 100%+ 进程并阻塞 gateway RPC | ❌ 无 | 性能 + 稳定性双重问题 |
| [#111372](https://github.com/openclaw/openclaw/issues/111372) | Gateway 在 macOS 上无限 SIGTERM 重启循环（6.11→7.1-2 升级后） | ❌ 无 | 升级回归，影响 macOS 用户 |
| [#96242](https://github.com/openclaw/openclaw/issues/96242) | 至少 3 条独立路径导致 Telegram 重复消息 | ❌ 无 | 多条路径均确认 |
| [#94939](https://github.com/openclaw/openclaw/issues/94939) | 6.x 状态迁移致 MS Teams conversation-store SQLite 为空（0 字节） | ❌ 无 | 数据丢失，已标记 recovery-stuck |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程泄漏，zombie 积累致运行时劣化 | ❌ 无 | 长期运行必现 |
| [#111870](https://github.com/openclaw/openclaw/issues/111870) | @openclaw/codex 在 CLI 一次性上下文注册失败（TypeError） | ❌ 无 | 插件兼容性 |

### 🟡 P2/P3 — 中低优先级
- [#105528](https://github.com/openclaw/openclaw/issues/105528)（P1）: Windows 上 exec/read 工具静默返回空输出（**回归**）
- [#120735](https://github.com/openclaw/openclaw/issues/120735) : Telegram 贴纸仅以原始文件引用到达，无描述且未落盘 → **已有 PR #121123 修复**
- [#114211](https://github.com/openclaw/openclaw/issues/114211) : Matrix 房间 agent 可进入"无回复输出 + 重启恢复 + 过期会话重放"自循环
- [#92460](https://github.com/openclaw/openclaw/issues/92460) : 隔离 cron 完成播报丢弃显式 delivery.channel

**稳定性总体评估**：P1 级 Bug 数量多且大量集中在**消息丢失、会话损坏、资源泄漏**三大类。多个高热度 Issue（#116277、#92201）长时间悬而未决或"修复后复发"，对用户信任造成持续损耗。


## 6. 功能请求与路线图信号

今日活跃的功能请求及被纳入下一版本的可能性：

| 功能 | Issue/PR | 热度 | 潜力判断 |
|---|---|---|---|
| **分层引导文件加载** | [#22438](https://github.com/openclaw/openclaw/issues/22438) | 19 评论 | ⚠️ 开放 6 个月，仍待产品决策，社区呼声高但进展缓慢 |
| **掩码密钥系统** | [#10659](https://github.com/openclaw/openclaw/issues/10659) | 15 评论，4 👍 | ✅ 符合安全趋势；已有 [PR #120534](https://github.com/openclaw/openclaw/pull/120534)（audit admitted-run context）部分相关，值得关注 |
| **每 agent dreaming 配置** | [#67413](https://github.com/openclaw/openclaw/issues/67413) | 8 评论，5 👍 | ✅ 解决多 workspace OOM 痛点，社区认可度高 |
| **/models test-fallback 命令** | [#6599](https://github.com/openclaw/openclaw/issues/6599) | 11 评论 | ✅ 小而美，请求量高（11 评论） |
| **多槽位记忆架构** | [#60572](https://github.com/openclaw/openclaw/issues/60572) | 6 评论，3 👍 | ⚠️ 架构级变动，短期难以落地 |
| **优雅子代理超时（预警告）** | [#6625](https://github.com/openclaw/openclaw/issues/6625) | 6 评论 | ✅ 低成本高价值，已有 [PR #120190](https://github.com/openclaw/openclaw/pull/120190)（bounded resumable recovery）部分关联 |

**路线图信号**：Context-aware continuation（PR #85651，XL 规模）与分层引导文件加载（#22438）都指向同一方向 —— **上下文窗口的精细化运营**。该项目正从"能跑"迈向"高效跑"阶段。Control UI 的多个 PR（#121032、#120855、#121258 等）表明**配对流程与模型管理**是当前 UI 迭代的重点。


## 7. 用户反馈摘要

### 😠 痛点与不满
- **修复不彻底**："#116277 被关闭，但问题一直在发生，监控 cron 今天（8月9日）还在记录新故障。" —— sloptop-the-terrible（#121058）
- **静默失败难以排障**："`exec` 和 `read` 工具经常返回空输出……间歇性且与具体会话相关，子代理却正常。" —— matts524（#105528）
- **迁移引发数据丢失**："升级到 2026.6.8 后 conversation store 为空（0 字节），引用孤儿化，Bot Framework 主动发送中断。" —— adamnagus（#94939）
- **排障体验差**："插件加载器静默容忍作者缺陷，在运行时报出晦涩错误，排查耗费数小时。" —— lawong888（#78301）

### 🙂 满意与肯定
- 核心维护者 steipete 高频提交（1 天内 7+ PR），社区反馈积极（PR #121294 快速合并显示维护响应迅速）
- Issue 标签体系（impact、issue-rating、clawsweeper）运转良好，用户可通过 `diamond lobster` 等评级快速识别高优问题
- 多语言/多平台支持持续完善（Telegram 贴纸修复 PR #121123、Windows 路径问题 #105528 均有响应）

### 📊 用户画像
活跃用户包括个人开发者（self-host 场景）、企业级用户（MS Teams、Slack Enterprise Grid、k3s 容器部署）以及 **AI agent 自动提交 Issue** 的用户（#6757 "I am Wyatt, an OpenClaw agent autonomously filing this feature request"），显示项目已被 AI agent 生态积极采用。


## 8. 待处理积压

以下长期未响应的重点 Issue/PR 需维护者关注：

| 类型 | 编号 | 标题 | 开放时长 | 优先级/热度 |
|---|---|---|---|---|
| Issue | [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic thinking 签名重放失效 | ~2 个月 | P1, 21 评论, 🦪 silver shellfish |
| Issue | [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex hook 进程 CPU 打满 | ~2 个月 | P1, 18 评论, 2 👍, 🐚 platinum hermit |
| Issue | [#10659](https://github.com/openclaw/openclaw/issues/10659) | 掩码密钥系统（功能请求） | ~6 个月 | 15 评论, 4 👍, 🦞 diamond lobster |
| Issue | [#45740](https://github.com/openclaw/openclaw/issues/45740) | gh-issues skill 提示注入漏洞 | ~5 个月 | P2, 16 评论, 🐚 platinum hermit, **needs-security-review** |
| Issue | [#48920](https://github.com/openclaw/openclaw/issues/48920) | Live Docs 领先于发布版本 | ~5 个月 | **P0**, 10 评论, 4 👍 |
| Issue | [#22438](https://github.com/openclaw/openclaw/issues/22438) | 分层引导文件加载 | ~6 个月 | 19 评论, 🌊 off-meta tidepool |
| PR | [#85651](https://github.com/openclaw/openclaw/pull/85651) | Context-pressure-aware continuation（XL 规模） | ~2.5 个月 | P3, 📣 needs proof |
| PR | [#90041](https://github.com/openclaw/openclaw/pull/90041) | 子代理完成消息被 message_tool_only 吞掉 | ~2 个月 | P1, ⏳ 等待作者 |

### ⚠️ 特别提醒
- **#48920（P0）**：文档与发布版本脱节，已开放 5 个月，属于**发布阻断级**问题却一直未解决，应优先处理。
- **#45740**：gh-issues skill 将未净化的 issue body 直接注入子代理提示，涉及**安全边界**且已标记 needs-security-review，建议加快安全评审。
- **#92201 与 #91009** 均为 P1 且开放 2 个月无修复 PR，建议维护团队给出明确的时间表或 workaround 说明，避免用户长期处于"带病运行"状态。


> **总结**：OpenClaw 项目社区活跃度极高，功能迭代与 UI 打磨进展迅速。但 **P1 级稳定性问题积累过多且修复复发率高**，是当前最大隐忧。建议维护团队在推进新功能的同时，集中资源打一场"稳定性攻坚战"，优先解决 #121058（复发型静默失败）、#111372（macOS 重启循环）、#94939（数据丢失）等直接损害用户信任的问题。

---

## 横向生态对比

好的，作为一名资深技术分析师，以下是基于您提供的各项目动态摘要，为技术决策者和开发者撰写的横向对比分析报告。

---

### **个人 AI 助手与自主智能体开源生态横向对比分析报告 (2026-08-10)**

#### **1. 生态全景**

当前个人 AI 助手/自主智能体开源生态正处于**由“功能堆叠”向“稳定加固与精细运营”转型的关键阶段**。头部项目（如 OpenClaw、Hermes Agent）的社区活跃度达到峰值，但普遍面临**P1 级稳定性问题积压、关键 Bug 修复后复发**的信任危机。与此同时，安全问题（尤其是 SSRF、提示注入、白名单绕过）成为多项目（NanoBot、ZeroClaw、PicoClaw）共同关注的焦点，表明生态正从早期探索走向生产环境可用性的严苛考验。此外，开发者对上下文窗口管理、Token 消耗透明化、跨模型协作的精细化控制需求显著上升，预示着下一轮技术竞争将聚焦于效率与可靠性。

#### **2. 各项目活跃度对比**

| 项目名称 | 核心定位 | 今日 Issue 更新 | 今日 PR 更新 | 合并/关闭 PR | 新版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型自主智能体框架 | 500 (峰值) | 500 (峰值) | 181 | 无 | **🔥🔥🔥🔥🔥 (极高)** - 活跃度达上限，但大量 P1 Bug 与修复复发是主要隐患，呈“高活跃、高风险”状态。 |
| **Hermes Agent** | 面向开发者的智能体框架 | 50 | 50 (15个新PR) | 4 | 无 | **🔥🔥🔥🔥 (高)** - 迭代速度快，安全/稳定性加固明确，但会话数据丢失等 P0 问题反复出现，信任度受挫。 |
| **CoPaw** | 多模型协作 (Stitch模式) | 17 | 50 | 1 | 无 (2.1.0b2) | **🔥🔥🔥🔥 (高)** - 社区贡献积极，Bug 响应快，但合并吞吐量低（50:1），已成为主要瓶颈。 |
| **ZeroClaw** | 企业级自动化与治理 | 50 | 50 | 0 | 无 | **🔥🔥🔥🔥 (高)** - 治理RFC与安全加固讨论激烈，但PR合并率极低（0/50），维护者审查严重滞后。 |
| **IronClaw** | 多 Agent 协作与自动化 | 22 | 27 | 8 | 无 | **🔥🔥🔥 (中高)** - Bug 闭环速度加快，功能迭代与质量修复并行，路线图清晰。 |
| **NanoBot** | 轻量级 AI 助手 | 4 | 15 | 4 | 无 | **🔥🔥🔥 (中)** - 社区活跃，但遭遇**严重（安全）**漏洞（allowPatterns 绕过）且响应滞后，是当前最大减分项。 |
| **PicoClaw** | 多协议消息桥接 | 3 | 6 | 1 | 无 | **🔥🔥 (中)** - 安全加固 PR 集中涌现是积极信号，但 Matrix 等稳定性问题被 stale 关闭，处理方式欠妥。 |
| **NanoClaw** | 轻量级/容器化智能体 | 1 (新) | 16 (待合并) | 0 | 无 | **🔥🔥 (中)** - 基础设施与安全加固并行，但 PR 队列堆积（含3个月未合），存在维护响应风险。 |
| **LobsterAI** | 多模型编排中枢 | 3 | 0 | 0 | 无 | **🔥🔥 (低)** - 处于迭代平静期，但多个长期未决 Issue（4个月）指向核心可用性问题，有用户流失风险。 |
| **Moltis** | 桌面端 AI 助手 | 2 | 1 | 0 | 无 | **🔥 (低)** - 平稳运行，无重大事件，PR 质量高但推进速度偏慢。 |
| **NullClaw / TinyClaw / ZeptoClaw** | - | 0 | 0 | 0 | 无 | **无活动** - 观察是否为活跃项目，或已进入停更/维护模式。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 凭借其**超高的社区活跃度（Issue/PR 双 500 峰值）**和**核心维护者（steipete）的高频提交**，稳居该生态的**事实标准与核心参照物**地位。

*   **优势与路线**：其技术栈更侧重**全渠道（Slack、Telegram、MS Teams 等）与企业级场景的适配**，同时在架构上探索分布式租约（CAS）、精细化上下文窗口运营等前沿方向。
*   **差异与风险**：相比 Hermes Agent 更注重开发者工具的纯粹性（CLI 优先）和 CoPaw 的多模型编排（Stitch），OpenClaw 走的是**“全家桶”式平台路线**。然而，其最大的风险也在于此——**与日俱增的复杂性和 P1 级“静默失败”问题**（如 #116277 复发）正在消耗其庞大的社区信任，这在其生态位上是致命的。它今日的挣扎表明，在规模扩张后，**稳定性已成为其继续领跑的核心挑战**。

#### **4. 共同关注的技术方向**

多项目不约而同地指向以下几个技术痛点，预示着下一阶段的技术攻坚方向：

1.  **可观测性与 Token 透明化**：**NanoBot** 的 `#5266` 要求记录详细 Token 消耗；**OpenClaw** 的 `#121273` 用 CAS 替代租约以增强一致性。这表明社区不满足于“黑盒”运行，要求对智能体的每一次决策、每一分钱的计算开销有精细的掌控。
2.  **静默失败与状态一致性**：**OpenClaw**（`#116277` 复发）、**Hermes Agent**（`#82756` 会话丢失）、**PicoClaw**（`#3203` Matrix 静默死亡）以及 **CoPaw** 的 `#6839`（隐式类型转换）都指向同一类问题：**系统在异常时缺乏明确的信号反馈**，导致“假死”或“数据丢失”。这已成为影响用户信任的头号杀手。
3.  **安全默认与供应链安全**：**NanoBot**（`#5305` 白名单绕过）、**ZeroClaw**（`#9565` Webhook 未认证）、**PicoClaw**（SSRF 三连修复）、**NanoClaw**（CVE 修复）等多项目在安全事件上高度同步，表明**在 AI Agent 广泛接入外部工具和网络的背景下，安全已从附加属性变为核心生存需求**。
4.  **上下文窗口的精细化运营**：**OpenClaw** 的 `#22438`（分层引导文件）、**ZeroClaw** 的 `#7100`（Per-model 配置）、**LobsterAI** 的 `#1187`（上下文窗口自定义）都指向同一个诉求：**减少 Token 浪费，将有限的上下文窗口用在“刀刃”上**，并期望获得更灵活的配置能力。

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 关键架构/技术差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全渠道、企业级自动化、复杂工作流 | 企业、高级个人开发者、社区 | 渠道适配器矩阵、高扩展性、庞大的技能生态，正在向精细化上下文管理演进。 |
| **Hermes Agent** | 面向开发者的 API/CLI、后端能力 | 软件开发者、技术爱好者 | 强调开发者体验，提供网关、CLI、TUI、SDK 等多种交互方式，近期聚焦安全与稳定性加固。 |
| **CoPaw** | 多模型协作 (Stitch 模式) | 需要多模型协同的开发者 | 核心是“多模型编排”，能在单会话中切换不同模型分工，强调跨 Provider 兼容性。 |
| **ZeroClaw** | 企业级治理、安全策略、自动化任务 | 企业、运维、安全团队 | 高度强调治理（RFC 流程）、安全默认（防数据泄露、SSRF、Webhook 认证），技术栈偏 Rust（从 CVE 修复推断）。 |
| **IronClaw** | 多 Agent 协作、工具发现与调用 | 构建复杂 Agent 工作流的团队 | 强调工具生态（tool-search）、多 Agent 编排、批量能力并行执行，有明确的 v1.2.0 路线图。 |
| **NanoBot** | 轻量级、核心对话与工具 | 个人开发者、快速部署场景 | 追求极简与轻量，适合资源受限或快速原型验证的场景，但近期安全问题暴露了其快速迭代中的疏忽。 |

#### **6. 社区热度与成熟度**

*   **快速迭代与高热度期**：**OpenClaw、Hermes Agent、ZeroClaw、CoPaw**，这些项目社区活跃，Issue/PR 数量大，但同时面临合并瓶颈或稳定性质疑。
*   **质量巩固与集成期**：**IronClaw、PicoClaw、NanoClaw**，在满足功能需求后，开始集中提交安全加固、架构重构类 PR，显示出向高质量、高安全性演进的趋势。
*   **平静蓄力期**：**LobsterAI、Moltis 及无活动项目**，或处于重大版本发布前的沉寂，或面临社区贡献者流失的风险，需关注其后续动态。

#### **7. 值得关注的趋势信号**

1.  **“稳定性”成为核心竞争壁垒**：对于 AI Agent 开发者而言，单纯的功能堆叠已不再具有竞争力。OpenClaw 的“复发危机”和 Hermes 的“数据丢失”警示我们，**设计一套具有可观测性、可恢复性的健壮运行时，比研发新功能更能赢得用户长期信任**。
2.  **安全是不可妥协的底线**：从 NanoBot 的严重漏洞到 ZeroClaw 的 Webhook 未认证，再到多个项目对 SSRF 的集中修复，安全事件已呈常态化。未来的 Agent 框架必须将安全编码和默认安全配置作为第一优先级，否则任何功能亮点都可能因一次安全事件而灰飞烟灭。
3.  **“上下文效率”是通往 AGI 的必经之路**：各项目对上下文窗口精细化运营的集体诉求表明，在模型能力短期内难以有质的飞跃时，**通过工程手段（如分层加载、压缩、路由）来最大化有限上下文的价值**，是提升 Agent 应用体验、降低成本的现实路径，也是下一阶段技术创新的主战场。
4.  **社区治理效率影响项目命运**：ZeroClaw 和 CoPaw 极低的 PR 合并率与 OpenClaw、Hermes 的高频合并且形成鲜明对比。这提示我们，**维护者的审查和集成速度直接影响社区贡献者的积极性**，是项目能否持续健康发展的重要软实力。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-10

> 数据来源：github.com/HKUDS/nanobot | 分析时段：2026-08-09 —— 2026-08-10


## 今日速览

过去 24 小时 NanoBot 项目保持了极高的社区活跃度：新增/活跃 Issue 4 条、PR 更新 15 条（其中 4 条已合并/关闭），无新版本发布。值得高度关注的是，今日集中出现了 **2 条安全问题报告（#5305、#5306）**，均指向 `exec.allowPatterns` 白名单绕过漏洞，属于高危安全事件，建议维护者优先响应。功能开发方面，`chengyongru` 提交的 token 用量结构化记录 PR（#5299）直接呼应了用户对 token 消耗透明化的核心诉求（#5266）。另有 4 个 PR（WebUI HTTPS 提示修复、天气预报 Windows 兼容、Dream 工具集修复、Telegram 轮询监控）均在今日内完成合并/关闭，展示了项目快速迭代的节奏——整体健康度良好，但安全漏洞的响应速度将是接下来评估的重点。


## 项目进展

今日共有 **4 个 PR 被合并或关闭**，修复了多个用户可感知问题：

- **[#5304] fix(webui): explain HTTPS requirement for voice input**（已合并，chengyongru）
  修复了 Android Chrome 在非安全上下文中无法启用麦克风的问题。现在 WebUI 会明确区分“HTTP 不安全来源”与“浏览器不支持录音”，并在所有语言环境下给出可操作的 HTTPS 配置提示，同时补充了局域网可信 HTTPS 方案文档。

- **[#5307] Restore Star History chart**（已合并，Mubelotix）
  恢复 README 中的 Star 历史图表。原图表因上游项目被 GitHub 限制而移除，新提供方不受近期 GitHub 限制影响。

- **[#5308] test: strengthen user-path coverage and CI gates**（已合并，chengyongru）
  补充了交互式 CLI、WebUI 聊天分支、版本检查、路由鉴权等用户路径测试；移除了 5 个重复测试；引入 V8 覆盖率报告并加强 CI 门槛，提升项目整体稳定性保障。

- **[#4019] Add GitAgent Protocol support (agent.yaml + SOUL.md)**（已关闭，shreyas-lyzr）
  该 PR 曾尝试引入 GitAgent 协议（便携式 AI 智能体开放标准），已存在 2.5 个月后今日关闭，具体原因需维护者确认（可能是设计方向变更或超期未响应）。

**整体评估**：今日合并的 PR 集中在 WebUI 体验修复、测试体系加固和文档改善，项目在打磨用户体验和提升工程质量的路径上稳健前进。`chengyongru` 与 `chengyongru` 贡献了较多基础设施层面的改进，维护者持续投入测试与可观测性建设。


## 社区热点

- **[#5266] 关于 token 消耗过大的讨论（13 条评论）**
  用户 knoppix2 报告 NanoBot 在 2 小时内消耗了约 100 万 token 而用户无明显感知，建议记录每次调用的时间点和 token 消耗详情以便追踪。该问题获得 13 条评论，是今日讨论最活跃的话题。回应此需求，PR #5299 已提议增加结构化的 token 使用记录接口，社区诉求与解决方案正快速对接。

- **[#5295] Docker Compose 部署权限问题（5 条评论）**
  Bennett-Yang 在按 deployment.md 部署时遭遇 `entrypoint.sh: Permission denied` 导致容器启动失败。这是部署环节的常见痛点，反映了文档与镜像构建之间的不一致，可能需要调整 Dockerfile 中的文件权限或文档说明。


## Bug 与稳定性

| 严重程度 | Issue | 描述 | Fix 状态 |
|---------|-------|------|---------|
| **严重（安全）** | [#5305](https://github.com/HKUDS/nanobot/issues/5305) | `exec.allowPatterns` 白名单绕过：通过 OpenAI 兼容 API 可执行未允许的 shell 命令链 | **暂无 fix PR** |
| **严重（安全）** | [#5306](https://github.com/HKUDS/nanobot/issues/5306) | 同上问题：shell 链式命令绕过 allowPatterns 限制 | **暂无 fix PR** |
| **中等** | [#5295](https://github.com/HKUDS/nanobot/issues/5295) | Docker Compose 部署失败：`entrypoint.sh` 无执行权限 | **暂无 fix PR** |
| **低** | (已修复) | WebUI 语音输入在 HTTP 下不可用 | #5304 已合并 |
| **低** | (已修复) | 天气技能在 Windows PowerShell 下 `curl` 别名解析失败 | #5303 待合并 |
| **低** | (已修复) | Dream 记忆整合时使用了错误的工具注册表，导致调用不可用工具 | #5302 待合并 |

**安全事件说明**：两条安全 Issue（#5305、#5306）由同一研究者（YLChen-007）在同一日提交，指向同一根因——`exec.allowPatterns` 白名单可通过 shell 链式语法（如 `ls; malicious_command`）绕过。该漏洞影响面取决于用户是否配置了 `tools.exec.allowPatterns`。**截至今日暂无修复 PR**，建议维护者优先复核 `exec` 工具的输入解析逻辑，并在修复前提醒用户谨慎暴露 API。


## 功能请求与路线图信号

- **token 使用透明化** — Issue #5266 要求记录 token 消耗明细。PR #5299（chengyongru）已实现：持久化最近 50 条 token 用量记录，新增 `GET /api/settings/usage/records?day=YYYY-MM-DD` 诊断接口，并保留原有每日汇总接口。此功能很可能进入下一版本。

- **模型无关的计算机操作（computer use）** — PR #4276 提出新增 `browser` 和 `computer_use` 原生工具（支持 DOM 自动化与截屏+键鼠控制双后端），于 6 月 10 日创建，已持续 2 个月仍为待合并状态，可能存在较大的设计讨论或技术挑战。

- **Agent Plugins v1 集成** — PR #5288 计划将 Agent 插件（vendor-neutral 包格式）与 CLI 应用打通，增强可移植性，属于架构层面的演进信号。

- **GitAgent Protocol（#4019）已关闭**，可能是方向调整或社区分歧。若维护者有意推进标准化，建议在讨论区说明原因，以避免贡献者重复劳动。


## 用户反馈摘要

**正面反馈：**
- 无明确正面评论记录（数据集中未体现）

**负面反馈与痛点：**
- **Token 消耗失控**（#5266）：用户反馈 2 小时消耗百万级 token 无感知，影响运营成本。这是目前对项目最核心的经济性担忧。
- **部署门槛**（#5295）：Docker Compose 部署流程存在权限配置问题，新用户可能因此受挫，影响入门体验。
- **语音输入限制**（#5304 触发场景）：用户在局域网 HTTP 环境下无法使用语音输入，需配置 HTTPS 方可解决。

**使用场景观察：**
- Telegram 渠道出现静默轮询停摆问题（#5156、#5301），网络不稳定环境下 bot 会永久失去消息接收能力。


## 待处理积压

**安全类（最高优先级）：**
- [#5305](https://github.com/HKUDS/nanobot/issues/5305) 与 [#5306](https://github.com/HKUDS/nanobot/issues/5306) — `exec.allowPatterns` 白名单绕过漏洞，尚未分配处理。

**长期未合并的重要功能：**
- [#4276](https://github.com/HKUDS/nanobot/pull/4276) — 模型无关的 computer use 工具（创建于 6 月 10 日，已 2 个月仍在 draft/讨论中），涉及浏览器自动化与桌面控制两个新工具，功能吸引力大但技术复杂度高，建议维护者明确状态（继续推进/搁置/征求设计意见）。

**长期未响应的 PR：**
- [#4019](https://github.com/HKUDS/nanobot/pull/4019)（GitAgent 协议）今日刚被关闭，建议维护者在合适渠道解释关闭原因。
- [#5156](https://github.com/HKUDS/nanobot/pull/5156) — Telegram 轮询停滞恢复方案（7 月 29 日开启，已 12 天未合并），配套的低风险前置 PR #5301 已就绪，可加速推进。

**其他关注：**
- [#5255](https://github.com/HKUDS/nanobot/pull/5255) — 外部托管 API 服务状态显示不真实的问题（Draft 状态，更新于 8 月 9 日），涉及 WebUI 展示逻辑，价值明确但推进缓慢。

---

**项目健康度评分**：★★★★☆（4/5）
社区活跃、修复速度快，但安全漏洞响应滞后与部分 PR 长期积压是当前主要风险点。建议维护者优先处理 #5305/#5306 安全问题，并为 #4276 明确路线图。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-10

## 1. 今日速览
项目在过去 24 小时保持高活跃度：共 50 条 Issue 更新和 50 条 PR 更新。值得注意的是新提交的 PR 数量显著增长，共 15 个新 PR（#82809 至 #82834），表明核心维护者正在积极响应社区反馈。无新版本发布，但存在多个 P0/P1 级别的稳定性问题（#82756、#82770、#82818）与安全相关修复 PR（#82829、#82830、#71996），显示项目正经历一次安全与稳定性加固周期。社区讨论焦点集中在**会话数据丢失**（3 次复发）、**cron 功能增强**（两条独立 PR）以及**无障碍支持**需求上。

## 2. 版本发布
无新版本发布。当前最新版本仍为 v0.20.0（2026.8.3）。多个 Issue 提及在 v0.20.0 升级后出现 Desktop 端回归（#80560 Windows 插件崩溃、#77753 macOS 更新死锁），建议维护者在下一版本中优先处理这些升级后遗症。

## 3. 项目进展
今日有 4 个 PR 被合并/关闭，但均为较旧的 PR（如 #46634 俄语本地化未合并被关闭、#71999 为已关闭的 bug 跟踪）。真正值得关注的是以下关键修复 PR 已提交供审查：

- **会话数据丢失修复**（#82756 关联）：第 3 次出现桌面端静默删除约 65 条消息的问题，此前 #70516（308 条）和 #80763（244 条）的修复均未完全拦截此路径。这是项目稳定性的核心威胁，目前尚无直接修复 PR，但已有详细根因分析。
- **安全修复 PR 集中涌现**：
  - #82829（CLI 进程表面暴露 vault 令牌）：从 argv、子进程环境、dotenv 遍历和诊断输出中消除密钥泄露。
  - #82830（审批绕过绝对路径拼写）：拦截通过绝对路径拼写绕过硬性命令白名单的行为，该修复由 #71996 拆分而来。
  - #82818（拒绝损坏二进制文档的纯文本写入）：防止 `write_file`/`patch` 破坏 .docx/.xlsx/.pdf 等二进制文件。
- **cron 功能增强双 PR**：
  - #82826：为每个 cron 任务注入实际运行时间到 prompt。
  - #82827：通过 `trigger_on_complete` 实现响应式任务链（对应 #15831 功能请求）。
- **Infra 修复**：#82833 修复管道模式后台 shell 卡死终端的问题；#82809 将本地 llama.cpp 的空响应 400 分类为可重试的瞬时错误。
- **桌面端**：#82794 修复弹出会话窗口路由到错误 profile 的问题（解决 #82768）；#82832 将本地存储日志写入从同步全量重写改为有界快照，避免阻塞渲染流。

整体评估：项目持续修复关键稳定性和安全问题，但历史 bug 的反复出现（会话丢失 3 次复发）提示测试覆盖和修复深度仍显不足。

## 4. 社区热点
- **#26689 无障碍支持**（评论 13 · 👍 1）— 盲人 VoiceOver 用户呼吁改进 Hermes 的屏幕阅读器体验。该用户明确表示"Hermes 具有极其强大的后端和智能体生态系统，但当前 UX 对屏幕阅读器用户非常困难"，反映**高级用户因无障碍短板无法使用核心功能**的深层诉求。该 Issue 已开放近 3 个月，热度不减，属长期未解决的核心可用性缺口。

- **#82616 网关会话连续性断裂**（评论 7 · 已关闭）— 在 state.db FTS 损坏时，出现孤儿会话分叉和陈旧会话继续恢复的问题，违反"一个会话永久持续"的合约。该问题在一天内即被关闭，但对 #82770 的产生有直接影响（会话泄漏）。

- **cron 相关 bug 集群**：#66824 + #71987（均为 `repeat='forever'` 报 TypeError，评论各 6 条）— 同一个缺陷被两个不同用户分别报告，且已被标记为 duplicate。这印证了当下 cron 相关 PR（#82826/#82827）的可能动机。

- **#82756 桌面端第三次静默删除消息**（评论 2）— 用户情绪可从标题中感受到："第 3 次发生"。涉及 P0 严重级别，社区对重复出现的会话数据丢失问题感到疲惫。链接: [Issue #82756](https://github.com/NousResearch/hermes-agent/issues/82756)

## 5. Bug 与稳定性
按严重程度排列：

| 严重度 | Issue | 问题描述 | 修复状态 |
|--------|-------|---------|---------|
| **P0** | [#82756](https://github.com/NousResearch/hermes-agent/issues/82756) | Desktop 端静默删除约 65 条消息（第 3 次发生），stale ordinal + auto-attached confirm_truncate | 无直接 fix PR |
| **P0** | [#82818](https://github.com/NousResearch/hermes-agent/pull/82818) | write_file/patch 可能以纯文本写入破坏二进制文档 | fix PR 已提交 |
| **P1** | [#82770](https://github.com/NousResearch/hermes-agent/issues/82770) | 测试会话泄漏进入生产 state.db，产生 700+ 垃圾开放行 | 调查中（#82616 附带发现） |
| **P1** | [#82616](https://github.com/NousResearch/hermes-agent/issues/82616) | 网关会话连续性因 FTS 损坏而断裂 | 已关闭（可能为其他单的重复或已被追踪） |
| **P2** | [#66824](https://github.com/NousResearch/hermes-agent/issues/66824) / [#71987](https://github.com/NousResearch/hermes-agent/issues/71987) | cronjob 创建时 `<=` 类型错误，影响所有 cron 创建 | 无 fix PR，但 #82826/#82827 改造可能触及 |
| **P2** | [#82831](https://github.com/NousResearch/hermes-agent/issues/82831) | normalize_usage 错过推理令牌（usage 为 dict 时静默为 0） | 无 |
| **P2** | [#82805](https://github.com/NousResearch/hermes-agent/issues/82805) | 本地 llama.cpp 间歇性空响应 400，池化 httpx 连接复用被服务器关闭的连接 | ✅ fix PR #82809 已提交 |
| **P2** | [#80841](https://github.com/NousResearch/hermes-agent/issues/80841) | Fastmail 确认控件无法从 CLI/TUI/Matrix 完成 | 无 |
| **P2** | [#80560](https://github.com/NousResearch/hermes-agent/issues/80560) | Windows 上任意桌面插件导致 React #310 崩溃（v0.20.0 后） | 无 |
| **P2** | [#75097](https://github.com/NousResearch/hermes-agent/issues/75097) | 迭代预算分歧：AIAgent 默认 90，execute_code 仅退还一个限制器 | 无 |

## 6. 功能请求与路线图信号
- **Cron 任务链**（[#15831](https://github.com/NousResearch/hermes-agent/issues/15831)）— 请求已有 3.5 个月，今日出现对应实现 PR #82827（`trigger_on_complete`），表明**该功能正被纳入路线图**。
- **Cron 提示注入运行时间** — #82826 通过 prompt 注入运行时间，改善定时任务时间感知能力。
- **跨 Profile 子代理**（[#41889](https://github.com/NousResearch/hermes-agent/issues/41889)）— 5 条评论，1 👍，仍处于需要决策阶段。请求允许 `delegate_task` 以指定 profile 的身份运行子代理，适用于多身份/多租户场景。
- **无障碍支持**（[#26689](https://github.com/NousResearch/hermes-agent/issues/26689)）— 13 条评论，保留最高热度，尚无任何 PR 关联。
- **Kanban 零授权工人 + Godfile 消除**（[#82591](https://github.com/NousResearch/hermes-agent/issues/82591)）— 3 条评论，这是一个史诗级规划（3 部分），涉及看板工作者的安全模型设计，未来可能需要重大架构变更。
- **Job 的 `max_turns` 支持 'none'/'unlimited' 值**（PR #67696）— 待合并，扩大配置文件表达力。
- **Discord 任务论坛改为实时会话**（PR #82819）— 对应社区对"机器人单纯投递 vs. 交互式会话"的两种使用模式需求。

## 7. 用户反馈摘要
- **"桌面端静默删除消息是第三次发生了。"** — #82756 用户，连续经历数据丢失后的沮丧感。
- **"Hermes 后端极为强大，但 UX 对屏幕阅读器用户非常困难。"** — #26689 用户，说明无障碍问题正阻挡高级用户体验核心功能。
- **"相同的 bug 已被两个不同的用户报告"** — #66824/#71987 显示 cron 功能是当前用户高频操作面，但对错误类型的应对仍显不足。
- 围绕 #82828，有用户反映 **"升级到 v0.20.0 后出现的死锁/崩溃"**（#77753 macOS、#80560 Windows），提示 updater 本身在不同平台上存在兼容性风险。
- **"Google Gmail MCP 在 CLI 下验证通过，但网关进程无法使用"** — #78190 反映认证状态/凭证在**子进程边界间传递失败**的问题，这是多进程架构下常见的隐形坑。

## 8. 待处理积压
- **#26689 无障碍改进** — 开放近 3 个月，评论最多（13 条），无任何 PR 关联。盲人用户的核心使用需求持续未得到回应。
- **#41889 跨 Profile 子代理** — 开放 2 个月，5 条评论，1 👍。`delegate_task` 缺乏跨身份能力，限制了多租户工作流的实用性。
- **#46064 OpenRouter 路由模型被静默丢弃** — 开放近 2 个月，3 条评论。用户只能手改 `config.yaml` 才能使用 `openrouter/pareto-code` 等模型，工具性过滤机制存在设计缺陷。
- **PR #67696 （max_turns 支持 unlimited）** — 开放 3 周，需维护者决策。当前无法以 "unlimited" 表达关闭轮次上限，是配置表达力的明显空缺。
- **PR #71996 审批绕过修复的分拆** — 需要维护者持续推进：#82830 为本修复的第一阶段，但后续的包装器选项语法重构仍需跟进。

---

**项目健康度评估**：功能迭代活跃（今日 15 个新 PR），安全加固方向明确，但会话数据可靠性问题和升级回归问题（Windows 插件崩溃、macOS 更新死锁）构成了社区信任风险。长期开放的无障碍请求与跨 Profile 功能表明：在"深度功能"和"基础可用性"之间存在优先级平衡压力。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-10

> 数据来源：sipeed/picoclaw GitHub 仓库 | 统计窗口：2026-08-09 ~ 2026-08-10

---

## 1. 今日速览

过去 24 小时内项目活跃度较高。共产生 3 条 Issue 更新和 6 条 PR 更新，属于近期的中等偏高活跃区间。值得关注的是，安全加固和功能增强成为今日主线：3 个针对 SSRF 防护的 PR 几乎同时提交（覆盖微信、企业微信及跨渠道媒体下载），同时 Telegram 原生表格渲染的 Feature + PR 也已到位，形成了从"问题提出"到"代码落地"的完整闭环。有 1 个长期滞留的阻断性 Bug（Matrix 同步循环无重连逻辑）被标记为 stale 关闭，但该问题在社区仍有较高关注度，建议维护团队继续跟踪。

---

## 2. 版本发布

**今日无新版本发布。**

上游最新版本为 v0.2.9，该版本对应的已知问题（Matrix 同步循环 Bug）仍待修复，预计下一版本将包含本轮 SSRF 加固和表格渲染等改动。

---

## 3. 项目进展

### 已合并/关闭的 PR

| PR | 标题 | 状态 |
|----|------|------|
| [#3326](https://github.com/sipeed/picoclaw/pull/3326) | fix(web): remove duplicate pnpm lock entries | 已关闭（合并） |

该 PR 修复了 `web/frontend/pnpm-lock.yaml` 中两个完全重复的 `semver@7.8.5` 映射条目，消除了 `ERR_PNPM_BROKEN_LOCKFILE` 构建阻断。虽是修复型改动，但它直接打通了 Web 前端的 CI 流水线，为后续前端迭代清除了障碍。

### 待合并的关键 PR（高优先级）

三个 SSRF 安全加固 PR 形成了完整的防御纵深：

- **[#3322](https://github.com/sipeed/picoclaw/pull/3322)** — 在 `utils.DownloadFile` 层面为 QQ/Telegram/Discord/LINE/Slack 的所有入站附件下载启用 `BlockPrivateTargets` 防护，从根源上杜绝 SSRF 攻击面（OneBot 此前已启用，本次是补齐其他渠道）。
- **[#3323](https://github.com/sipeed/picoclaw/pull/3323)** 和 **[#3324](https://github.com/sipeed/picoclaw/pull/3324)** — 分别修复企业微信和微信公众号/微信生态的媒体下载客户端，改用 `CreateSafeHTTPClient` 并增加 URL 校验，防止重定向至 loopback 或内网地址。

这三个 PR 合在一起标志着一个明确信号：**项目正在从功能优先转向安全加固阶段**，建议维护者优先审查合并。

---

## 4. 社区热点

### 最热 Issue：[#3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix 同步循环静默死亡

- **评论数：8 | 👍 数：2 | 状态：已关闭（stale）**
- 创建于 2026-07-02，直至 2026-08-09 才被标记关闭，期间 38 天无修复动作。

**核心诉求：** Matrix 渠道的 `/sync` 长轮询在遇到网络中断或服务器重启后会永久停止工作，且进程仍保持存活状态，导致 systemd 的 `Restart=on-failure` 无法触发自动恢复。这是一种典型的"静默死亡"故障——系统看起来一切正常，实际消息通道已经失效。用户对修复的主导诉求非常明确：**建立自动重连逻辑，并在连接丢失时主动触发进程退出或告警**。

该 Issue 被 stale 关闭意味着它已经自动冻结，但**问题本身并未解决**，且项目维护者没有给出修复时间表或替代方案。

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 是否已有修复 PR |
|----------|----------|------|-----------------|
| **高（静默故障）** | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix 同步循环无重连逻辑，网络中断后通道永久失效且无任何告警，进程存活但消息断流 | ❌ 无，已 stale 关闭 |
| **中（构建阻断）** | [#3326](https://github.com/sipeed/picoclaw/pull/3326) | pnpm-lock.yaml 重复键导致 `--frozen-lockfile` 下 CI 构建失败 | ✅ 已合并 |
| **中（安全漏洞）** | [#3322](https://github.com/sipeed/picoclaw/pull/3322) | QQ/Telegram/Discord/LINE/Slack 入站媒体下载可被 SSRF 攻击（通过构造 URL 访问内网） | ✅ 待合并 |
| **中（安全漏洞）** | [#3323](https://github.com/sipeed/picoclaw/pull/3323) / [#3324](https://github.com/sipeed/picoclaw/pull/3324) | 企业微信/微信媒体下载客户端未做 URL 安全校验，存在 SSRF 风险 | ✅ 待合并 |

> **风险评估**：SSRF 漏洞属于真实可利用的安全缺陷，需要维护者尽快合并三个 PR 并发布补丁版本。Matrix 问题虽为稳定性缺陷，但由于 Issue 已冻结，需要重新开启才能推动修复。

---

## 6. 功能请求与路线图信号

### 新增功能请求

| Issue/PR | 功能 | 说明 |
|----------|------|------|
| [#3325](https://github.com/sipeed/picoclaw/issues/3325) + [#3327](https://github.com/sipeed/picoclaw/pull/3327) | **Telegram 原生富文本表格渲染** | Issue 提出后同日内即被作者转化为完整 PR，实现 GFM 表格和 HTML `<table>` 检测并利用 Telegram Bot API 10.1 的富消息能力渲染。Feature 和 PR 出自同一人（As-tsaqib），显示社区开发者有很强的自驱力。**大概率进入下一版本** |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | **IRC 长消息智能分片/合并** | 用户希望 PicoClaw 理解 IRCv3 的分片机制，将一条超长消息的各分片视为一个整体来组织语义。创建于 07-22，目前 4 条评论，尚未有对应 PR。属中优先级改进，不影响核心功能 |

### 路线图信号

- **SSRF 全面加固**是三笔提交在同一时段用相同模式（`CreateSafeHTTPClient` + `BlockPrivateTargets`/`ValidateSafeHTTPURL`）实现的事实，说明这可能是安全评审后的集中整改行动。
- **DeltaChat 清理重构**（[#3222](https://github.com/sipeed/picoclaw/pull/3222)）削减了 200 行代码，去除了 legacy 功能和密码配置方案，表明项目长期愿景是精简代码库和提升可维护性。

---

## 7. 用户反馈摘要

### 正面反馈（隐含）

- **社区响应速度快**：Telegram 表格渲染的 Feature Request（#3325）发布当天就被同一用户转化为可用的 PR（#3327），侧面反映 PicoClaw 的插件/消息处理架构对贡献者相对友好。
- **安全责任意识**：SashaMIT 连续提交 3 个安全修复 PR，说明贡献者对多协议桥接场景中的 SSRF 风险有清晰认知，也从侧面说明上游 `utils.DownloadFile` 的防 SSRF 能力已经成熟且可复用。

### 负面反馈/痛点

- **Matrix 问题用户失望**（#3203）："silent death" 描述的故障模式让用户对系统可靠性产生担忧——"进程活着但消息不走了"。用户明确提到 systemd 重启策略的失效，暗含对部署运维便利性的期望未被满足。该 Issue 被 stale 关闭而未修复，可能进一步削弱用户对维护者响应速度的信心。
- **IRC 分片处理距离"可用"仍有差距**（#3287）：用户期望 IRC 长消息能像普通长文本一样被连贯地理解和回复，但目前只能收到断开的多条消息，影响使用体验。

---

## 8. 待处理积压

### ⚠️ 高优先级提醒

| 项目 | 详情 | 积压时长 | 建议 |
|------|------|----------|------|
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix 同步循环无重连逻辑（静默死亡） | **39 天（已 stale 关闭）** | 需重新开启 Issue 并纳入里程碑，制定重连策略（指数退避 + 进程退出兜底）或提供自动化运维告警方案 |

### 中优先级

| 项目 | 详情 | 积压时长 |
|------|------|----------|
| [#3222](https://github.com/sipeed/picoclaw/pull/3222) | DeltaChat 清理重构 PR，文档较完整、-200 LOC，但已放置 38 天未合并 | 38 天 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息分片合并功能，已获 4 条讨论但无代码进展 | 19 天 |

### 维护建议

1. **优先审查并合并三个 SSRF 修复 PR**（#3322/#3323/#3324），这是安全补丁，不应长期滞留。建议确认冲突情况后统一合并。
2. **为 #3327（Telegram 表格渲染）和 #3222（DeltaChat 重构）安排 reviewer**，两者都是具有用户可见收益或代码质量收益的 PR，不要成为新的长期积压。
3. **重新激活 #3203 或明确回应关闭理由**，避免社区形成"长期已知严重 Bug 得不到修复"的认知。至少应当在 README 或 CHANGELOG 中披露该已知限制及规避方案。

---

*报告生成时间：2026-08-10 | 数据窗口：2026-08-09 ~ 2026-08-10 | 数据源：sipeed/picoclaw GitHub API*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-10** | **数据周期：2026-08-09 ~ 2026-08-10**


## 1. 今日速览

NanoClaw 项目今日活跃度处于**高位**，过去 24 小时内产生 1 条新 Issue 和 16 条待合并 PR，虽无新版本发布，但多条 PR 涉及基础设施与安全修复（CVE 修复、容器镜像发布流水线），表明项目正处于**密集迭代与加固阶段**。值得关注的是，社区贡献者 zvi-fried 和 gabi-simons 表现活跃，在代码重构、文档规范和安全性方面均有产出；而来自 brentkearney 和 ira-at-work 的两个历史 PR（#2529、#3142）均与附件投递路径修复相关，且自 5 月以来尚未合并，需维护团队关注。

**健康度评估**：整体健康，PR 队列充足但存在堆积风险（16 条待合并，其中 3 条已超过两周），安全相关修复与功能开发并行推进。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日**无 PR 被合并或关闭**，16 条 PR 全部处于待合并状态。但从提交内容上可以看到项目在以下几个方向持续推进：

| 方向 | 代表性 PR | 说明 |
|------|-----------|------|
| **容器安全加固** | [#3207](https://nanocoai/nanoclaw PR #3207) | 修复 pnpm/npm 供应链中的 `tar` 包 CVE（GHSA-23hp-3jrh-7fpw，Critical 级别） |
| **CI/CD 发布管线** | [#3208](https://nanocoai/nanoclaw PR #3208) | [core-team] 新增 Docker Hub 自动发布工作流，带 CVE 门禁 |
| **宿主/容器架构重构** | [#3214](https://nanocoai/nanoclaw PR #3214)、[#3213](https://nanocoai/nanoclaw PR #3213)、[#3212](https://nanocoai/nanoclaw PR #3212) | 统一模块生命周期钩子、通道渲染器注册、数据库迁移注册表，三连重构提升宿主侧可扩展性 |
| **CLI 功能增强** | [#3218](https://nanocoai/nanoclaw PR #3218) | 新增 `--stdin-json` 输入模式，支持有界 JSON 参数传递 |
| **渠道适配器** | [#3041](https://nanocoai/nanoclaw PR #3041)、[#3050](https://nanocoai/nanoclaw PR #3050) | Dial 渠道（SMS + AI 语音通话）仍在推进，已配套渠道选择器向导 |

此外，[#3186](https://nanocoai/nanoclaw PR #3186)（host 侧技能能力接缝）与 [#3211](https://nanocoai/nanoclaw PR #3211)（单一职责集成规则文档）等结构性改进持续铺垫中。项目整体处于**架构优化与渠道扩展并行、安全加固优先**的阶段。


## 4. 社区热点

今日最值得关注的是 **[Issue #3217](https://nanocoai/nanoclaw Issue #3217)**（install_packages 缺少 pip 渠道），该 Issue 虽为今日新开且暂无评论/点赞，但它直接指向 hardened-image 采用路径中的关键缺口，与 PR #3216（文档修订）形成强关联，具备较高的后续讨论潜力。

PR 侧活跃度最高的贡献者为 **zvi-fried**（5 条 PR：CLI 特性 + 4 条重构/文档）和 **gabi-simons**（2 条 [core-team] PR，安全与 CI），二者代表了社区外部贡献者与核心团队并行推进的格局。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 问题 | 状态 | 修复 PR |
|--------|------|------|---------|
| **高（安全）** | 容器镜像中 `tar` 包存在 Critical 级 CVE（GHSA-23hp-3jrh-7fpw），由 npm 和 pnpm 双重引入 | 待合并 | [#3207](https://nanocoai/nanoclaw PR #3207) 已提交（[core-team]） |
| **高（功能）** | Signal 渠道的附件路径未被挂载到 agent 容器，导致图片/文件附件永远无法被 Read 工具打开 | 待合并 | [#3142](https://nanocoai/nanoclaw PR #3142)（5 月提出，距今 2 周未合） |
| **中** | Signal 渠道入站附件被直接丢弃，未送达 agent | 待合并 | [#2529](https://nanocoai/nanoclaw PR #2529)（5 月提出，距今近 3 个月未合） |
| **中** | Slack 中粘贴的表格内容无法传递至 agent | 待合并 | [#3209](https://nanocoai/nanoclaw PR #3209) |
| **低（日志）** | 私信（DM）解析日志未脱敏，存在敏感信息泄露风险 | 待合并 | [#3215](https://nanocoai/nanoclaw PR #3215) |

**值得警惕**：CVE 修复 PR #3207 中明确指出，即使刷新至最新 `node:22-slim` 基础镜像，`tar 7.5.11` 仍存在，需要主动升级 pnpm 和 npm 版本才能彻底清除 — 这意味着安全加固**不可依赖纯基础镜像更新**，需显式处理。


## 6. 功能请求与路线图信号

1. **Python/pip 渠道支持**（[Issue #3217](https://nanocoai/nanoclaw Issue #3217)）：用户请求在 `install_packages` 中增加 `packages_pip` 渠道。考虑到 hardened-image 是企业采用的关键路径，此请求有较大可能被纳入下一版本，配套的文档 PR #3216 已先行提交。

2. **CLI 结构化输入**（[PR #3218](https://nanocoai/nanoclaw PR #3218)）：`--stdin-json` 特性为脚本化和自动化调用打开了空间，符合 AI 代理场景下的编程式交互需求。

3. **Dial 渠道集成**（[PR #3041](https://nanocoai/nanoclaw PR #3041) + [#3050](https://nanocoai/nanoclaw PR #3050)）：SMS + AI 语音通话渠道已进入渠道选择器，这是一项较大的功能扩展，预计为后续版本的重要卖点。

4. **附件投递链路修复**：多条 PR（#2529、#3142、#3210）围绕"附件应如何到达 agent"这一主题 — 这暗示当前附件处理机制存在系统性不足，未来版本可能重构附件投递架构。


## 7. 用户反馈摘要

- **Python 用户群受阻**：Issue #3217 提出，当 agent 依赖 pip 安装的工具时，无法走 derived-image 路径，因此也无法使用 hardened prebuilt image。这对于 Python 生态的重度用户是实际阻碍，可能迫使部分用户停留在此前未加固的镜像版本。
- **附件"静默丢失"**：从 PR #3142 和 #2529 的描述可以看出，Signal 渠道的附件（PDF、文档等）在用户视角是 *发了但 agent 看不到* — 这类静默失败对用户体验伤害较大，建议尽快合入。
- **文档误导**：PR #3216 指出当前 hardened-image 指南将 `install_packages` 描述为"Dockerfile 编辑的替代方案"，但未说明其仅覆盖 apt 和 npm，文档的准确性需要立即修正。


## 8. 待处理积压

以下为长期未合并、值得维护者关注的关键 PR：

| PR | 提出时间 | 等待时长 | 重要性 | 说明 |
|----|----------|----------|--------|------|
| [#2529](https://nanocoai/nanoclaw PR #2529) fix(signal): deliver inbound attachments | 2026-05-18（今日有更新） | 近 3 个月 | 高 | 修复 Signal 附件被直接丢弃的问题，虽今日有更新，但长时间未合并；与 #3142 有功能重叠，建议合并处理 |
| [#3142](https://nanocoai/nanoclaw PR #3142) fix(signal): forward attachments to mounted inbox | 2026-07-27 | 2 周 | 高 | 与 #2529 解决同一类问题（附件可达性），两条 PR 应择优合并或整合 |

**维护者提醒**：Signal 附件投递问题横跨近 3 个月仍未见进展，而 Slack 表格传递（#3209）、DM 日志脱敏（#3215）等同类"渠道体验"问题也在本周集中出现 — 建议从**附件投递架构**层面统一解决，而非逐渠道 patch。此外，16 条 PR 积压中多条已存在超过 1 个月（#3186、#3041、#3050），建议安排一轮集中 Review 以降低社区贡献者的等待成本。

---

*本日报由 AI 自动生成，数据截至 2026-08-10。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-10

## 1. 今日速览

过去 24 小时 IronClaw 仓库保持高度活跃：共处理 22 条 Issues（新开/活跃 15 条，关闭 7 条）和 27 条 PR（待合并 19 条，合并/关闭 8 条）。值得关注的是，今日有大量针对性修复 PR 上线——包括**emoji 短代码渲染**（#7404）、**WebUI 活动时间线排序**（#7403）、**流式 Responses API 外部工具拒绝**（#7401）、**自动化计数一致性**（#7402）以及 **outbound 发送竞态修复**（#7395）——直接回应了近期 bug_bash 中高频出现的 P1/P2 级问题。此外，tool-search 能力增强（#7409/#7410）和 Web Push 通知通道（#7398）等中大型特性 PR 也在持续推进，项目整体处于功能迭代与质量修复并行的稳健节奏。新版本发布为 0 个。值得注意的是，多个 bug_bash 遗留 P2 问题（#7345/#7346/#7348/#7349 等）在今日获得了对应修复 PR，说明缺陷闭环速度正在加快。


## 2. 版本发布

过去 24 小时无新版本发布。


## 3. 项目进展

今日合并/关闭了 8 条 PR，核心成果如下：

- **[#7171] [CLOSED] fix(skills): one DB-backed tree for every skill mount, and make a skill's own commands runnable**（关闭 #7168，属于 epic #6941 第 4 项）— 修复了技能安装后"永久消失"的严重问题（此前安装返回 `{"installed": true}` 后技能在 Settings → Skills 中不可见、无法激活）。现在每个 skill mount 都有独立数据库树，且技能自身的命令可运行。为后续 #7203（挂载虚拟文件系统）铺平道路。 - 链接: https://github.com/nearai/ironclaw/pull/7171
- **[#7387] [CLOSED] chore(deps): bump the everything-else group（12 项依赖更新）** — 常规依赖更新合并，保持工具链同步。
- **[#7022] [CLOSED] chore(deps): bump the actions group（2 项 CI actions 更新）** — CI 依赖更新。

**合并 PR 之外，今日还关闭了 7 条 Issues**，其中值得注意的是 #5522（Reborn 例程因缺少 Slack 读取能力而失败，并陷入 `capability_info` 重试循环）和 #7292（已安装工具无法使用 + runner 心跳错误）等 P1 级 QA 问题已关闭，表明相关修复已通过验证。


## 4. 社区热点

今日讨论最活跃的条目集中在 2-4 条评论区间，全部为低量级但高密度讨论：

- **[#5522] [CLOSED] Reborn routine fails when task requires reading Slack DMs**（4 条评论） — 该 Issue 在关闭前经历了从 7 月 2 日创建到 8 月 9 日关闭的完整生命周期，核心矛盾是**能力缺失检测与 capability_info 重试机制的交互缺陷**：当模型请求 Slack DM 读取能力时，系统反复重试 `capability_info` 而非明确返回"无此能力"，导致例程最终 Failed。社区讨论集中在重试退避策略和错误语义设计上。链接: https://github.com/nearai/ironclaw/issues/5522
- **[#7405] [OPEN] Improve deferred tool discovery with complete signatures and namespace-aware catalog previews**（2 条评论） — serrrfirat 提出的工具发现机制增强，直指当前 `tool_search` 返回信息不足以支撑模型做出准确调用决策的问题，附带在 100/500/1000 工具规模下保持检索质量的基线测试需求。已由 #7409/#7410 系列 PR 响应。链接: https://github.com/nearai/ironclaw/issues/7405
- **[#7407] [OPEN] Execute BatchPolicy::Parallel capability batches concurrently**（2 条评论） — 性能优化提议：代理循环已计算并行批处理策略，但生产环境的 capability 端口仍顺序执行所有批次。打通这条路径可以实现多工具调用的真正并发。链接: https://github.com/nearai/ironclaw/issues/7407
- **[#7346] [OPEN] Emoji shortcodes displayed as plain text in assistant messages**（2 条评论） — 从 bug_bash 社区反馈中迅速转化为产品修复（对应 PR #7404），讨论了 gemoji 支持范围、代码块内容保留、流式渲染时的转换时机等实现细节。链接: https://github.com/nearai/ironclaw/issues/7346


## 5. Bug 与稳定性

按严重程度排列：

**高严重度**

- **[#7400] [OPEN] `stream: true` + caller `tools[]` 在 `/api/v1/responses` 上中途失败并留下永久不可删除（"僵尸"）线程**（严重性：高，100% 可复现，影响 1.1.0-rc.1 和 1.1.0 稳定版）— 已有对应修复 PR #7401（拒绝该组合，返回稳定的 400 `param: tools`），**但注意 #7401 是"拒绝"而非"支持"**——用户需确认该行为变更是否可接受，且需验证僵尸线程清理机制是否一并处理。链接: https://github.com/nearai/ironclaw/issues/7400 | 修复 PR: https://github.com/nearai/ironclaw/pull/7401

**中严重度**

- **[#7292] [CLOSED] 已安装工具无法使用，运行失败并出现 runner 心跳错误** — 已关闭，修复已验证。链接: https://github.com/nearai/ironclaw/issues/7292
- **[#5522] [CLOSED] Reborn 例程因缺少 Slack 读取能力失败，陷入 capability_info 重试循环** — 已关闭。修复方向是让能力缺失检测更明确、重试更克制。链接: https://github.com/nearai/ironclaw/issues/5522
- **[#7348] [OPEN] Activity 工具调用与助手进度消息在聊天 UI 中顺序错乱** — bug_bash P2，已有修复 PR #7403（流式助进度保持在同 run 活动之前，最终回复保持回合结束位置）。链接: https://github.com/nearai/ironclaw/issues/7348 | 修复 PR: https://github.com/nearai/ironclaw/pull/7403
- **[#7346] [OPEN] Emoji 短代码在助手消息中显示为纯文本** — bug_bash P2，已有修复 PR #7404（在完成和流式回复中转换 gemoji 短代码，同时保留代码内容）。链接: https://github.com/nearai/ironclaw/issues/7346 | 修复 PR: https://github.com/nearai/ironclaw/pull/7404
- **[#7345] [OPEN] 代理报告 61 个自动化，而 UI 仅显示 50 个** — bug_bash P2，已有修复 PR #7402（恢复 UI 列表页 50 行限制，并新增调用方作用域的生命周期状态聚合查询）。链接: https://github.com/nearai/ironclaw/issues/7345 | 修复 PR: https://github.com/nearai/ironclaw/pull/7402
- **[#7349] [OPEN] 刷新聊天导致部分运行历史和 Activity 时间线消失** — bug_bash P2，与 #7348 相关，可能由同一消息分组逻辑问题引起。修复 PR #7403 可能同时解决此问题，但需确认。链接: https://github.com/nearai/ironclaw/issues/7349
- **[#5552] [CLOSED] 多次工具失败后运行以通用"无效结果"错误结束** — 已关闭，但问题本身暴露了错误信息颗粒度不足的设计缺陷。链接: https://github.com/nearai/ironclaw/issues/5552
- **[#5509] [CLOSED] 聊天创建延迟随对话历史积累而增长** — 已关闭。链接: https://github.com/nearai/ironclaw/issues/5509

**低严重度**

- **[#5510] [CLOSED] 无法删除旧例程** — 已关闭。链接: https://github.com/nearai/ironclaw/issues/5510
- **[#4341] [CLOSED] 代理思考链暴露给用户（Qwen3.6）** — 已关闭。链接: https://github.com/nearai/ironclaw/issues/4341
- **[#4344] [CLOSED] 代理在加载时镜像用户消息作为自己的响应（Qwen3.6）** — 已关闭。链接: https://github.com/nearai/ironclaw/issues/4344

**新增 PR 值得关注**：**[#7395] fix(outbound): close send-claim TOCTOU race and allow failed-row reopen** — 修复了发送声明中的 TOCTOU 竞态（time-of-check to time-of-use），消除了"发送行被错误标记为丢失"的问题，并允许失败行重新打开重试。属中高风险修复。链接: https://github.com/nearai/ironclaw/pull/7395


## 6. 功能请求与路线图信号

从 Issue 和 PR 中可以识别出以下路线图信号：

- **#7166 [epic, v1.2.0] Tool disclosure follow-up** — 渐进式工具披露已在 Reborn 默认启用并验证成功，该 epic 包含了后续的优化计划（微调、缓存等）。v1.2.0 已锁定包含此特性。链接: https://github.com/nearai/ironclaw/issues/7166
- **#7392 [OPEN] Experiment: 用固定的 omp 工具面替换第一方编码工具** — serrrfirat 发起的新实验：将 IronClaw 模型可见的编码工具替换为 [can1357/oh-my-pi](https://github.com/can1357/oh-my-pi@08819b279cf02ae2545e69dad7111ab48d91d35e) 的精确契约。这暗示项目可能将编码能力从内置工具转向标准化第三方接口。链接: https://github.com/nearai/ironclaw/issues/7392
- **#7405 [OPEN] 改进延迟工具发现与完整签名** + 配套 PR #7409/#7410 — 工具目录在 1000+ 工具规模下的可发现性和上下文效率是明确的性能方向。链接: https://github.com/nearai/ironclaw/issues/7405
- **#7407 [OPEN] 并行执行 BatchPolicy::Parallel 能力批次** — 性能优化已提出但尚无 PR，可能是下一个 "easy win"。链接: https://github.com/nearai/ironclaw/issues/7407
- **#7398 [PR] Web Push 浏览器推送通知 + PWA** — 将 Web 应用打造为一等通知通道，与 Slack/Telegram 并列。这是用户触达面的重要扩展。链接: https://github.com/nearai/ironclaw/pull/7398
- **#7360 [OPEN] 扩展内置与持久化写入路径的压力覆盖** — 对现有压力测试盲区的补充，防止回归。链接: https://github.com/nearai/ironclaw/issues/7360


## 7. 用户反馈摘要

从 QA bug（`joe-rlo` 的 bug_bash 系列）用户视角可见以下痛点：

- **自动化状态视图不一致**：代理声称 61 个触发，但 UI 只显示 50 个 —— 用户对"到底什么在运行"缺乏可信赖的单一视图。已有修复 PR #7402。
- **执行过程可视化差**：多工具调用时，Activity 块和进度消息顺序错乱；刷新页面即丢失历史。用户在长任务中无法追踪执行时间线。已有修复 PR #7403。
- **工具安装 ≠ 工具可用**：CoinGecko 工具安装后无法使用、运行彻底失败 —— 安装成功的反馈是"假阳性"，这直接破坏了对工具的信任。已关闭（#7292）。
- **外部认证失效后错误信息误导**：GitHub token 被撤销后，系统报"输入无法编码"或"模型暂不可用"而非引导重新认证；Slack 重连多次后进入永久"Waiting for Slack..."死状态。这两条 P2 问题（#5878、#5882）仍开放，是认证流程中值得优先修复的用户触点。
- **简单任务过度调用工具**：一个"查邮件+写入 Google Sheet"的任务产生了 124 次工具调用。代理在 base64 解码、FOIA 请求上下文分析等无关内容上耗费大量算力 —— 用户明确希望代理更"聚焦"。链接: https://github.com/nearai/ironclaw/issues/6046
- **例程自传播顾虑**：例程可创建其他例程，存在自复制自动化/无限调度循环风险（#6479）。用户对失控自动化表达了担忧。

正面信号：相关修复 PR 的上线速度（如 #7346→#7404、#7348→#7403）表明 bug_bash 反馈已形成有效闭环。


## 8. 待处理积压

以下 Issue/PR 长期未获足够关注，建议维护者优先审视：

- **[#7076] [OPEN] Install the packages the catalog already publishes**（`neo-sky`，2026-08-03 创建，时隔三个月后 rebase 到最新 main）— 新贡献者 PR，涉及包安装功能，已 rebase 解决冲突。链接: https://github.com/nearai/ironclaw/pull/7076
- **[#7020] [OPEN] chore(deps): bump tokio-tungstenite 0.29.0 → 0.30.0**（8 天未合并）— 长期挂起的依赖更新。链接: https://github.com/nearai/ironclaw/pull/7020
- **[#7262] [OPEN] chore(deps): bump wasm 组（wit-component/wit-parser）**（5 天未合并）。链接: https://github.com/nearai/ironclaw/pull/7262
- **[#6046] [OPEN] 简单邮件转 Sheet 任务产生 124 次工具调用**（2026-07-13 创建）— 代理效率问题，可能与 #7405（工具发现）相关联，可能需要更深层的性能优化。链接: https://github.com/nearai/ironclaw/issues/6046
- **[#6479] [OPEN] 例程可自创建/修改，存在自复制自动化风险**（2026-07-22 创建，仅 1 条评论）— 缺乏护栏的安全隐患，值得在 v1.2.0 中评估是否纳入。链接: https://github.com/nearai/ironclaw/issues/6479
- **[#5551] [OPEN] 自动化发送中间进度而非最终结果到 Slack**（2026-07-02 创建，1 条评论）— 行为不符合用户预期（#5551），可能影响营销/通知类用例。关联 PR #7396（渐进式预览）可能提供解决思路。链接: https://github.com/nearai/ironclaw/issues/5551
- **[#5878] [OPEN] 已撤销的 GitHub token 产生误导性错误**（2026-07-09 创建，1 条评论）— 认证失效场景的 UX 问题，恢复路径不明确，对用户操作效率影响较大（需卸载重装扩展才可恢复）。链接: https://github.com/nearai/ironclaw/issues/5878

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-10

## 1. 今日速览

过去24小时内，LobsterAI 项目活跃度处于**中等偏低**水平：新增/活跃 Issues 3 条，无新 PR 提交或合并，无新版本发布。值得关注的是，今日活跃的 Issues 均集中在**多模型协作与自定义模型切换**方向，反映出在主流模型能力趋同的当下，用户对跨模型工作流（Stitch 模式）的体验诉求正在成为核心关注点。另有两条 Issues 处于 stale 状态（超30天无实质更新），建议维护团队分批清理。整体来看，项目处于迭代周期的相对平静期，但社区讨论中透露出明确的功能演进方向。

---
## 2. 版本发布

无新版本发布。

---
## 3. 项目进展

过去24小时无 PR 被合并或关闭，项目主干代码无新增提交。

不过，从历史趋势和当前 Issue 活跃度来看，**多模型路由与自定义模型兼容性**正成为近期社区最集中的反馈方向（详见下文社区热点），这很可能成为下一个版本迭代的重点模块。建议关注项目维护者对 #2453 的响应速度，该 Issue 属于直接影响用户体验的 bug 类问题，若修复及时，预计将作为 patch 版本发布。

---
## 4. 社区热点

### 最受关注：#2453 切换自定义模型，被系统定义为不许可？
- **作者**: Alexandre0820 | **创建**: 2026-08-09 | **评论**: 1 | **👍**: 0
- **链接**: [Issue #2453](https://github.com/netease-youdao/LobsterAI/issues/2453)

该 Issue 于昨日创建即成为讨论焦点，目前评论数已在首日活跃列表中名列前茅。用户报告了一个**自定义模型标识符解析错误**的问题：当模型名称形如 `custom_1/openai/gpt-oss-20b:free` 时，系统会将其 Provider 误判为 `openai`，从而触发不认可的报错。用户明确指出这是**切换线程时才会出现的间歇性故障**，而新开线程沿用一个模型则不会触发。

**背后诉求分析**：这反映了两个深层需求：
1. **自定义模型语法的灵活性与健壮性**——用户期望 `custom_/` 前缀能作为明确的用户自定义标识，而非被系统二次解析。
2. **跨会话/线程的配置一致性**——同一模型在不同线程中表现不一致，说明会话上下文中的模型状态管理存在缺陷。

考虑到本项目定位为 AI Agent 中间层，这个问题直接影响 OpenRouter、NVIDIA 等聚合平台用户的使用体验，预计会被列为核心修复项。

---
## 5. Bug 与稳定性

| 严重程度 | Issue # | 标题 | 状态 | 有 fix PR? |
|---------|---------|------|------|-----------|
| 中 | #2453 | 切换自定义模型被误判为不许可 | 开放中，讨论进行中 | 无 |
| 高 | #1187 | 上下文窗口/输出 token 大小不支持自定义 | 已 stale，无后续进展 | 无 |
| 中 | #2132 | 跨模型子任务调用失败（网关级函数调用未注册） | 已 stale，有定位结论 | 无 |

**详细分析**：

- **#2453**：解析逻辑缺陷，导致切换模型时被错误拒绝。影响所有使用第三方模型聚合平台的用户，属于功能性 bug，暂无临时规避方案。
- **#1187**：DeepSeek 模型报 `Context overflow: prompt too large` 错误，用户明确建议增加上下文窗口和输出 token 的手动配置选项。该 Issue 已 stale（创建于 4 月 1 日），但问题未解决，随着长上下文模型普及，此问题的严重性可能会持续上升。
- **#2132**：跨模型子任务协作失败。检查结果为网关级函数调用 `call_function_gblu0nmqpcej_1` 未注册到会话列表，主任务无法感知子任务完成状态。此问题已进入定位阶段，但缺乏进展维护。

---
## 6. 功能请求与路线图信号

### 明确的路线图信号

| 功能 | 来源 Issue | 优先级判断 | 纳入下一版本可能性 |
|------|-----------|-----------|------------------|
| 上下文窗口大小自定义设置 | #1187 | 高——直接导致核心功能不可用 | 高 |
| 输出 token 数量自定义设置 | #1187 | 同上 | 高 |
| 自定义模型标识符语法 `/` 分隔符兼容 | #2453 | 高——影响自定义模型生态兼容性 | 高 |
| 跨模型子任务主动通知/联动优化 | #2132 | 中——属于架构优化而非 bug 修复 | 中 |

**分析**：#1187 中用户提出的建议（"在设置模型 api 的选项中增加上下文窗口大小设置和输出 token 设置"）技术实现成本较低，且能覆盖绝大多数主流 API 的适配需求，预计会在下一个 minor 版本中纳入。而 #2132 的解决方案涉及 Agent 间通信协议的设计层面，更偏向长期演进。

---
## 7. 用户反馈摘要

从今日活跃的 Issues 及评论中提炼真实用户反馈：

- **核心使用场景**：用户将 LobsterAI 作为多模型编排中枢，在单一会话中动态切换不同模型以完成不同子任务（如 M3 负责规划与验收、DeepSeek 负责快速生成）。这证实了项目的 Stitch 模式已成为核心使用场景。

- **痛点一（来自 #1187）**：当模型输入超出上下文窗口限制时，只会收到 "Try /reset" 的简单提示，无法通过调整窗口大小继续使用当前模型。用户期望**手动配置覆盖默认值**，而非一刀切地强制新开会话。

- **痛点二（来自 #2453）**：模型名称中的 `/` 分隔符引发解析歧义，用户表示 "在一个线程里面切换模型尤其打扰"——切换模型是一个高频动作，频繁报错严重打断工作流。

- **痛点三（来自 #2132）**：跨模型协作时，主任务无法及时感知子任务的完成状态，导致 Agent 间缺乏协调效率。用户为此提供了一套具体的改进思路（同模型内子任务通知可借鉴至跨模型场景），说明用户对 Agent 内部机制有较深理解，属于种子用户级别的深度反馈。

---
## 8. 待处理积压

### 长期未响应的重要 Issue

| Issue # | 创建时间 | 标题 | 最后更新 | 处理建议 |
|---------|---------|------|---------|---------|
| #1187 | 2026-04-01 | 建议增加上下文窗口和输出 token 设置 | 2026-08-09 | **超过4个月未解决**，涉及核心可用性，建议至少给出临时 workaround 或排期承诺 |
| #2132 | 2026-06-09 | 跨模型子任务调用问题（含修复方案） | 2026-08-09 | 用户已附带详细定位建议，需维护者评估方案可行性并回应 |

**建议**：

1. 针对 #1187，可快速在设置面板暴露 `context_window` 和 `max_tokens` 两个参数（默认读取模型 API 配置），工作量约 1-2 个 man-day。
2. 针对 #2132，用户已给出可操作的修复路径（将同模型子任务完成通知机制迁移至跨模型场景），可纳入下一迭代的技术方案评审。

---

**总体健康度评估**：项目代码活跃度处于低谷（PR 挂零），但社区讨论所反映的方向与 Agent 编排领域主流演进相符（多模型协作、上下文自适应、配置灵活性）。建议维护团队在两周内快速响应 #2453（高影响、中修复成本），并对 #1187 做出排期承诺，以缓解核心用户流失风险。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-08-10

## 今日速览

过去 24 小时内，Moltis 项目保持平稳活跃，收到 2 条新 Issue（均为 Bug 报告）和 1 个待合并的 PR，无新版本发布。值得关注的是，两项 Issue 分别涉及设置界面表单数据意外重置和 Apple Container 1.x 沙箱状态误判，均指向运行时环境与 UX 层面的可靠性问题。社区贡献者 pxmpsdev 提交了一个针对 Vault 恢复短语哈希逻辑的修复 PR（#1186），目前尚未合并，整体项目健康度良好，无阻塞性问题。

---

## 项目进展

### 待合并 PR（1 个）

**fix(vault): normalize recovery phrase before hashing（#1186）**
- 作者：pxmpsdev
- 创建时间：2026-08-09 | 最后更新：2026-08-09
- [PR 链接](https://github.com/moltis-org/moltis/pull/1186)

**变更内容**：`derive_recovery_kek` 在派生 KEK（密钥加密密钥）前对恢复短语进行标准化处理（去除连字符、转大写）。此前 Vault 解锁已支持小写或含连字符的短语（由 `recovery_key_case_insensitive` 覆盖），但存储的哈希值仍基于原始未标准化短语计算。此 PR 修复了该不一致性，确保哈希计算与解锁验证路径使用相同的标准化输入。

**项目进展评估**：该修复属于 Vault 密钥管理模块的稳健性改进，解决了潜在的用户数据可恢复性边界问题。由于需待维护者审查合并，今日项目无实质性代码合入，整体推进速度偏缓，但 PR 质量较高，合并预期明确。

---

## 社区热点

今日社区讨论热度偏低，两条新 Issue 和一条 PR 均无评论和点赞。参考：

- [Issue #1185](https://github.com/moltis-org/moltis/issues/1185)：Apple Container 1.x 沙箱启动但 Moltis 误判未运行

- [Issue #1187](https://github.com/moltis-org/moltis/issues/1187)：Heartbeat 设置界面静默重置表单未覆盖字段

- [PR #1186](https://github.com/moltis-org/moltis/pull/1186)：Vault 恢复短语标准化修复

**潜在诉求分析**：三个条目虽然无互动，但指向两个核心方向——**跨平台运行可靠性**（Apple Container 环境适配）和 **设置持久化的数据完整性**（UI 状态与实际配置同步）。这两点是桌面 AI 助手类工具在真实用户环境中最常遭遇的稳定性瓶颈，建议维护者优先规划处理。

---

## Bug 与稳定性

按严重程度排序（今日无崩溃或数据丢失级高危 Bug）：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|---------|-------|------|--------------|
| 中 | [#1185](https://github.com/moltis-org/moltis/issues/1185) | Apple Container 1.x 沙箱实际已启动，但 Moltis 误判为未运行；可能导致用户重复启动实例或错过依赖该状态的功能 | 无 |
| 低-中 | [#1187](https://github.com/moltis-org/moltis/issues/1187) | Heartbeat 设置界面仅展示表单字段对应的配置项，提交时静默重置了表单未覆盖的其他字段，用户无感知地丢失部分配置 | 无 |

**稳定性评估**：#1185 涉及 Apple 沙箱环境的状态探测逻辑，属于平台集成层缺陷；#1187 则是典型的 Web 表单未完整双向绑定问题。两者均不触发即时危机，但都可能在特定使用场景下引发数据一致性困惑，建议尽快分配修复。

---

## 功能请求与路线图信号

今日无显式的 Feature Request 提交。结合已提交 PR 推测：

- **Vault 短语容错性增强**（#1186）虽属修复，但反映了用户对恢复短语输入宽容度的期待——小写、含连字符的输入应被接受。该逻辑若被合入，将提升 Vault 在真实用户输入习惯下的可用性，建议在下一版本发布说明中突出该改进。

- 两个 Bug 的根因修复（设置表单完整同步、Apple Container 状态检测）若需触及更深层架构，可能促使维护者考虑**统一配置管理模块**或**容器运行状态抽象层**，但这些属于路线图层面的推测，目前无直接信号。

---

## 用户反馈摘要

由于今日所有条目均无评论互动，以下反馈仅基于 Issue 描述提取：

1. **#1185 作者（mikz）**：使用 Apple Container 1.x 运行 Moltis，沙箱已成功启动但界面状态未同步。典型使用场景为macOS 环境下的隔离运行需求，用户关注的是容器功能是否被正确识别和接入。

2. **#1187 作者（IlyaBizyaev）**：在配置 Heartbeat 设置时，表单仅展示了部分字段，提交后未展示字段被静默重置。用户痛点在于**配置的不可预测性**——界面未提供完整视图，且无任何警示提示用户存在未展示的会重置字段。

3. **#1186 作者（pxmpsdev）**：作为贡献者，在实现或测试 Vault 恢复流程时发现哈希与解锁路径的标准化不一致问题，主动提交修复。体现了贡献者对安全模块一致性的专业关注。

**综合洞察**：用户对 Moltis 的核心诉求集中在"所见即所得"与"状态可感知"两个体验维度——配置界面需要公示所有影响字段，运行状态需真实反映底层容器/沙箱的实际状况。这两点均值得在主版本迭代中作为 UX 改进目标。

---

## 待处理积压

今日无长期未响应的重大 Issue 或 PR 需要标记提醒（当前条目创建时间均为最近 2 天内，处于正常响应窗口内）。

建议维护者重点关注以下待办（基于发布时间与话题重要性）：

1. **#1185（Apple Container 运行状态误判）**：已发布 2 天无响应，涉及平台集成可靠性，建议 @mikz 补充日志与复现步骤后分配至容器模块维护者。
2. **#1187（Heartbeat 设置静默重置）**：建议纳入 UI 组件库的双向绑定校验规范，可标记 `good first issue` 供新贡献者认领。
3. **#1186（Vault 短语标准化修复）**：已等待 1 天无审查动态，逻辑清晰且包含测试覆盖，建议优先 review 并合并。

---

*本日报由 AI 分析师自动生成，数据来源于 Moltis GitHub 仓库，统计时间为 2026-08-10 上午 9:00 UTC。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-10

> CoPaw (github.com/agentscope-ai/CoPaw) | 数据窗口: 2026-08-09 ~ 2026-08-10


## 1. 今日速览

项目今日活跃度**中高**。过去 24 小时累计产生 17 条 Issue 更新和 50 条 PR 更新，但**合并/关闭仅 1 条**（PR #6846），大量 PR 仍处于待审查或待合并状态。Issue 侧以 Bug 报告为主（约 8 条），集中在前端渲染、模型连接、MCP 工具调用和记忆系统四大方向，其中 **Google API 连接失败（#6812）** 和 **MCP 字符串参数误转数字（#6839）** 已分别有对应修复 PR（#6844、#6854），响应速度良好。另值得注意的是，来自 lcq225 的同一份 Bug 报告被**重复提交了 5 次**（#6848-#6852），反映出前端渲染问题在 2.1.0b2 上影响面较大，提交链路也存在一定问题。社区层面，贡献者活跃度较高，多个 first-time-contributor 的首个 PR 涌入，项目整体处于**健康的社区共建阶段**，但维护侧合并速度有待提升。


## 2. 版本发布

本时段无新版本发布。当前最新版本为 **2.1.0b2**，多个 Issue 和 PR 均围绕该版本展开（如 #6852、#6840）。


## 3. 项目进展

今日合并 PR 较少，但待合并队列中已有多项关键修复准备就绪。

### 已合并 / 已关闭

| PR | 标题 | 说明 |
|---|---|---|
| [#6846](https://github.com/agentscope-ai/QwenPaw/pull/6846) | feat(providers): catalog DeepSeek V4 context windows (1M) | 为 deepseek-v4-flash / deepseek-v4-pro 添加 1M token 上下文窗口的静态目录条目，解决此前被误判为 131,072 token 导致过早触发上下文压缩的问题。**（已合并）** |

### 待合并队列亮点（已确认修复方向）

| PR | 标题 | 对应 Issue | 说明 |
|---|---|---|---|
| [#6844](https://github.com/agentscope-ai/QwenPaw/pull/6844) | fix(providers): strip unsupported Gemini schema metadata | [#6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) | 移除工具 schema 中的 `$schema` 字段，修复 Google Gemini API 拒绝请求导致 Model 'unknown' 错误 |
| [#6845](https://github.com/agentscope-ai/QwenPaw/pull/6845) | fix(chats): preserve assistant completion time | [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) | 修复历史会话重载后助手消息完成时间被重置为创建时间的问题 |
| [#6854](https://github.com/agentscope-ai/QwenPaw/pull/6854) | [codex] add localized approval purpose descriptions | [#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832) | 为权限审批卡片添加人类可读的用途描述，避免用户直接查看 PowerShell 代码 |

> 📌 **综合判断**：项目今日在**跨 Provider 兼容性**（Gemini、DeepSeek）和**前端体验细节**（时间显示、审批可读性）两个方向上有显著推进。但 50 条 PR 中仅 1 条被合并，**维护吞吐成为当前瓶颈**，部分 PR 已等待超过 2 周（#6259、#6312、#6360）。


## 4. 社区热点

### #2291 — Help Wanted 总任务列表（评论 66 条）

> 链接: [Issue #2291](https://github.com/agentscope-ai/QwenPaw/issues/2291) | 状态: 已关闭

项目贡献任务的**主索引**，持续有贡献者认领任务并通过 PR 提交成果——今日新增 PR #6312（主题/皮肤模块）、#6842（隐藏 Agent 标志）均源自该列表的任务。该 Issue 虽已关闭，但实际承担着社区任务分发的枢纽职能。

### #6281 — Web 控制台适配移动端（评论 5 条）

> 链接: [Issue #6281](https://github.com/agentscope-ai/QwenPaw/issues/6281) | 状态: OPEN

**评论量持续增长**。用户希望在移动端直接操作 Web 控制台，目前未看到对应 PR，但结合 PR #6843（SSE 流式实时输出）的推进，前端体验优化可能正被逐步纳入。

### 重复提交的同一 Bug：长文本工具输出渲染异常（#6848-#6852，5 条）

> 链接: [Issue #6851](https://github.com/agentscope-ai/QwenPaw/issues/6851) 等 | 状态: 已关闭（重复）

用户 lcq225 在 2.1.0b2 上发现：工具调用返回大量原始文本时，前端渲染器将**多行输出折叠成不可读的单一文本块**。同一报告被重复提交 5 次（#6848-#6852），说明该问题影响明显且用户反馈路径不清晰。


## 5. Bug 与稳定性

| 严重程度 | Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|---|
| 🔴 高 | [#6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) | Google API 调用失败 — Model 'unknown' | OPEN | ✅ [#6844](https://github.com/agentscope-ai/QwenPaw/pull/6844) |
| 🔴 高 | [#6839](https://github.com/agentscope-ai/QwenPaw/issues/6839) | MCP 工具将数字字符串误转为数字格式传参 | OPEN | 🔍 待确认（#6854 为相关增强） |
| 🟠 中 | [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) | 助手消息结束时间显示异常（实际 2min 显示 几秒） | OPEN | ✅ [#6845](https://github.com/agentscope-ai/QwenPaw/pull/6845) |
| 🟠 中 | [#6851](https://github.com/agentscope-ai/QwenPaw/issues/6851) (含 #6848-#6852) | 前端渲染器折叠长多行工具输出 | CLOSED (dup) | 🔍 未分配 |
| 🟡 低 | [#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847) | Qwenpaw 执行任务时被杀软拦截/强停 | OPEN | 🔍 未分配 |
| 🟡 低 | [#6853](https://github.com/agentscope-ai/QwenPaw/issues/6853) | prompts.py 误导 Agent：声称 dream 会同步写入 MEMORY.md 但未实现 | OPEN | 🔍 未分配 |

> **稳定性判断**：Google API 和 MCP 类型转换属于**高影响阻断类 Bug**，但均已快速获得修复 PR 或明确修复方向，响应速度较好。前端渲染问题虽被标为重复关闭，但实际尚未修复，且影响用户阅读体验。


## 6. 功能请求与路线图信号

| 功能请求 | 来源 Issue | 状态 | 对应 PR / 信号 |
|---|---|---|---|
| 审批时附带用途描述 | [#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832) | OPEN | ✅ PR #6854 已实现（待合并） |
| Web 控制台移动端适配 | [#6281](https://github.com/agentscope-ai/QwenPaw/issues/6281) | OPEN | 未见对应 PR |
| AI 审批描述本地化（中英文） | PR #6854 | 待合并 | 已实现 |
| 隐藏 Agent（不在 UI 选择器中显示仍可调用） | PR #6842 | 待合并 | 插件生态利好 |
| Auto-Dream 单单元失败容错重试 | [#6841](https://github.com/agentscope-ai/QwenPaw/issues/6841) | OPEN | 无对应 PR |
| ReMe4 完整路线图确认（Auto-Link、tri-modal search） | [#6840](https://github.com/agentscope-ai/QwenPaw/issues/6840) | OPEN | 等待维护者回复 |
| 子代理模型自动切换 + 共享 workspace 目录 | [#6838](https://github.com/agentscope-ai/QwenPaw/issues/6838) | OPEN | 无对应 PR |
| 会话 Fork（快照式复制上下文到新会话） | PR #6704 | 待合并 | 相关 Issue #6560 |

> **路线图信号**：6 个新功能请求中，2 个已有实现 PR（#6832 → #6854，#6560 → #6704），其余 4 个处于讨论阶段。其中 **#6840** 是对 ReMe4 完整路线图的追问，反映用户对记忆系统的关注度持续升高；**#6838** 的子代理工作区隔离问题涉及架构层面（config.json 与 chats.json 分离），短期内快速解决的可能性较低。


## 7. 用户反馈摘要

- **工具输出可读性差（#6851）**："When a tool call returns a large amount of raw text output and the agent includes it directly in the final response text…" — Windows 11 Pro 用户对前端渲染折叠长文本的体验强烈不满，第 5 次重新提交也反映了强烈的解决期望。
- **模型连接失败（#5584）**："1.1.7 的版本还可以连接，后来的版本均无法连接…其他软件均可正常对话" — 版本升级导致的回归问题，对比类描述显著提高了问题定位效率。
- **审批体验不直观（#6832）**："用户查看这些权限非常不直观，需要查看申请的 PowerShell 代码才能明白" — 安全审查与易用性的平衡诉求清晰。
- **杀软误报（#6847）**："Qwenpaw 在执行任务的时候，经常会被杀软拦截" — 安全软件对 Agent 自动化行为的误判，影响生产环境可用性。
- **上下文注入角色冲突（#6358 via PR #6360）**： 用户反馈 AgentScope 对 `role="system"` 消息的校验导致注入内容被拒绝，修复 PR 已提交 3 周有余仍未被合并。


## 8. 待处理积压

### 长期未合并的高价值 PR

| PR | 标题 | 等待天数 | 影响 |
|---|---|---|---|
| [#6360](https://github.com/agentscope-ai/QwenPaw/pull/6360) | fix: change context injection role from system to user | **19 天** | 修复 AgentScope 校验拒收 system 注入问题的关键路径，阻塞上下文注入功能 |
| [#6259](https://github.com/agentscope-ai/QwenPaw/pull/6259) | feat(security): support CIDR in no-auth host allowlist | **22 天** | 安全运维刚需，解决内网多 IP 逐个配置痛点 |
| [#6312](https://github.com/agentscope-ai/QwenPaw/pull/6312) | feat(console): configurable theme/skin module (draft) | **20 天** | 来自 #2291 任务认领，仍处于 draft 状态，需维护者提供方向性反馈 |
| [#6398](https://github.com/agentscope-ai/QwenPaw/pull/6398) | feat: add reranker support for ReMe memory search | **18 天** | 记忆检索质量提升的关键增强，配合 ReMe4 路线图 |

### 长期开放的活跃 Issue

- [#6281](https://github.com/agentscope-ai/QwenPaw/issues/6281) — Web 控制台移动端适配（已开放 21 天，持续有评论追问）
- [#5584](https://github.com/agentscope-ai/QwenPaw/issues/5584) — ascend-vllm 模型连接回归（已开放 44 天，虽已关闭但用户反馈问题严重）

### 维护者提醒

- PR #6360 与 #6259 的长时间搁置可能**削弱贡献者持续投入的积极性**，建议优先安排审查。
- lcq225 的五次重复提交提示问题提交引导流程（Issue 模板 + 查重机制）存在改进空间。


## 结语

CoPaw 正处于**功能迭代提速期**——2.1.0b2 引入 ReMe 记忆重构后带来了一批回归 Bug（Gemini 连接、时间显示、前端渲染），但社区的修复响应速度令人满意，问题从报告到修复 PR 的平均周期在 1-3 天内。比较突出的风险是**合并吞吐**：50 条 PR 中 49 条仍在等待，多集中在 1-3 周前就已准备好的修复。建议维护侧本周优先处理时间敏感型修复（#6844、#6845）和长期搁置的高价值 PR（#6360、#6259），保持社区贡献的正向飞轮运转。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是 2026-08-10 的 ZeroClaw 项目动态日报。

---

## ZeroClaw 项目动态日报 — 2026-08-10

### 1. 今日速览

ZeroClaw 项目今日保持高度活跃，尤其是在治理流程（RFC）和安全加固方面。过去24小时内，Issue 和 PR 更新量均达到 50 条，但大部分 PR 处于待合并状态（49/50），合并率极低，表明维护者审查和集成是当前瓶颈。值得注意的是，安全相关议题（如 Webhook 认证、配置热更新、凭据链验证）在今日讨论中占据主导，且多项高优先级（P0/P1）Bug 已被确认或修复。此外，没有新版本发布，但多个针对稳定性与安全性的修复 PR 正在等待合并。

---

### 3. 项目进展

今日没有 PR 被合并，但多个关键修复和功能 PR 已准备就绪，等待维护者审查：

- **安全修复（高风险）**:
    - **[PR #9868] fix(channels): guard link-enricher redirects**: 修复了链接增强器可能被重定向到公共URL的安全漏洞，通过复用共享的私有/本地主机分类器来防止SSRF攻击。 (由 Audacity88 提交)
    - **[PR #9002] fix(gateway): keep agent turns alive after viewer disconnect**: 将仪表盘 WebSocket 视为“观看者”而非“所有者”，防止客户端断开连接（如浏览器休眠、网络波动）时取消正在进行的智能体任务。 (由 IftekharUddin 提交)

- **渠道与集成（高工作量）**:
    - **[PR #8968] fix(wechat): surface iLink sendmessage body errors**: 修复微信渠道静默丢弃消息的问题，现在会正确解析并报告 `ret`/`errcode` 错误。 (由 tonsiasy 提交)
    - **[PR #9556] feat(observability): add Langfuse observer backend**: 新增 Langfuse 可观测性后端，支持将 OpenTelemetry 追踪导出到 Langfuse 云或自托管实例。 (由 jxxralf 提交)
    - **[PR #9013] refactor(config)!: move TodoWrite display config from the daemon into zerocode**: 将 `TodoWrite` 显示配置从守护进程迁移到 zerocode 客户端，将显示逻辑与核心运行时分离。 (由 tidux 提交，含破坏性变更)

---

### 4. 社区热点

今日讨论焦点集中在项目的治理效率和安全策略上，反映了社区对决策流程简化及安全默认配置的强烈诉求。

- **[Issue #6808] RFC: Work Lanes, Board Automation, and Label Cleanup** (评论: 22)
  - **诉求**: 这是一个关于工作流优化的治理 RFC，旨在简化标签系统、自动化看板，以减轻维护者负担。该议题持续获得高关注度，说明社区对当前流程的复杂性有所不满，并期望更高效的项目管理。
  - **链接**: [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

- **[Issue #7100] RFC: Per-model capability & context-window config** (评论: 12)
  - **诉求**: 用户希望为每个模型单独配置能力（如视觉支持）和上下文窗口大小，而不是依赖 provider 家族默认值，以避免模型能力误报和上下文预算错配。这反映了用户对精细化、准确配置的需求。
  - **链接**: [Issue #7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100)

- **[Issue #9397] RFC: Treat an empty WhatsApp Web `allowed_groups` as permit-none** (评论: 11)
  - **诉求**: 这是一个重要的安全默认值提案。目前 `allowed_groups` 为空时默认允许所有群组，这存在安全隐患。社区正推动将其改为“默认拒绝”，即只有显式配置的群组才能访问。该讨论反映出用户对“安全默认”原则的高度重视。
  - **链接**: [Issue #9397](https://github.com/zeroclaw-labs/zeroclaw/issues/9397)

- **[Issue #8692] [Tracker]: Maintainer decision queue for RFCs and design issues** (评论: 11)
  - **诉求**: 社区自发创建了一个“维护者决策队列”跟踪器，用于集中管理和跟踪所有待处理的 RFC 和设计问题。这侧面反映出维护者在处理大量 RFC 时存在延迟，社区希望提高决策透明度和效率。
  - **链接**: [Issue #8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)

---

### 5. Bug 与稳定性

今日报告和讨论的 Bug 主要集中在安全、资源管理和配置一致性方面。

- **严重 (S0/S1)**:
    - **[Issue #9565] [Bug]: gateway webhook handlers do not fail closed** (P0, 进行中)
      - **描述**: WhatsApp Cloud、Linq、WATI 三个 Webhook 处理器未对调用方进行认证，允许攻击者向智能体注入消息，存在数据泄露/安全风险。
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565)
    - **[Issue #9328] [Bug]: verifiable-intent evaluates constraints without verifying the credential chain** (P2, 已接受)
      - **描述**: 可验证意图（VI）的约束评估逻辑在验证凭据链之前就执行了，这是一个严重的安全漏洞。
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9328](https://github.com/zeroclaw-labs/zeroclaw/issues/9328)
    - **[Issue #9779] [Bug]: sops_dir: documented default is not honoured by the daemon, so SOPs silently never load** (P1, 已接受)
      - **描述**: 文档中声明的 `sops_dir` 默认值未被守护进程实现，导致依赖默认配置的用户的 SOP 永远不会加载，且无任何错误提示。
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9779](https://github.com/zeroclaw-labs/zeroclaw/issues/9779)

- **中等 (S2)**:
    - **[Issue #9198] [Bug]: Discord typing indicator remains stuck after dashboard daemon reload** (P2, 已接受)
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9198](https://github.com/zeroclaw-labs/zeroclaw/issues/9198)
    - **[Issue #9486] [Bug]: High-entropy detector redacts Solana wallet addresses** (P2, 已接受)
      - **描述**: 高熵检测器将合法的 Solana 钱包地址误判为敏感信息并打码，导致支付请求无法正常发送。
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486)
    - **[Issue #9284] [Bug]: config flush can overwrite concurrent writes** (P1, 已接受)
      - **修复状态**: 暂无关联修复 PR。
      - **链接**: [Issue #9284](https://github.com/zeroclaw-labs/zeroclaw/issues/9284)

- **已关闭**:
    - **[Issue #8054] System prompt tool-availability mismatch**、**[Issue #8560] browser_open hangs**、**[Issue #9192] shared_budget TOCTOU** 等 12 个问题已于今日关闭。

---

### 6. 功能请求与路线图信号

多个新功能请求和 RFC 正在进行中，其中一些已有关联的 PR，显示出较高的纳入可能性。

- **治理流程改革**:
    - **[Issue #9496] RFC: Streamline RFC scope, discussion, voting, and assignment**: 旨在简化和加速 RFC 流程。这与此前社区对决策效率的抱怨一致，预计会被认真考虑。 (P1, 高关注度)
      - **链接**: [Issue #9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)

- **安全与策略增强**:
    - **[Issue #9825] RFC: Define publish-safe exceptions for public blockchain identifiers**: 为高熵检测器定义“可发布安全”的例外，以解决合法公共区块链地址被误杀的问题。该议题直接关联 [#9486] Bug，并有 [PR #9868] 作为初步修复，是当前优先度较高的功能方向。 (P2)
      - **链接**: [Issue #9825](https://github.com/zeroclaw-labs/zeroclaw/issues/9825)

- **配置与运行时体验**:
    - **[Issue #7897] [RFC]: Apply security policy and channel config updates without full daemon reload**: 旨在实现配置热更新，避免修改配置后需要完全重启守护进程。这将是提升用户体验和运维效率的重要改进。 (P3, 高关注度)
      - **链接**: [Issue #7897](https://github.com/zeroclaw-labs/zeroclaw/issues/7897)
    - **[PR #9875] feat(agents): per-agent env vars and workspace-confined HOME for the shell tool**: 新增 per-agent 环境变量注入功能，并限制 shell 工具的 HOME 目录，提升了配置灵活性和安全性。 (新提交)
      - **链接**: [PR #9875](https://github.com/zeroclaw-labs/zeroclaw/pull/9875)

---

### 7. 用户反馈摘要

- **对“安全默认”的强烈需求**：多个 Issue（如 #9397、#9825）表明用户期望更严格的安全默认值，即使这意味着配置过程会稍显复杂。社区对“默认允许”和“无认证”等潜在安全风险非常敏感。
- **对配置有效性的困惑**：[Issue #9779] 和 [Issue #7897] 反映了用户的痛点：配置了但没有生效，或者生效需要重启整个服务。用户期望配置的“所见即所得”和更平滑的动态更新能力。
- **对项目治理效率的担忧**：多个高评论数的跟踪器（#6808、#8692）和 RFC（#9496）表明，社区对决策和审查流程的缓慢有所感知，并希望通过流程自动化或简化来提高效率。
- **误报困扰**：[Issue #9486] 的 Solana 地址被打码问题，展示了严格的安全检测在真实业务场景下可能带来的摩擦，用户希望有更智能的例外机制。

---

### 8. 待处理积压

以下为长期未解决或已暂停的重要议题，需要维护者关注：

- **[PR #8994] feat(tools): add native Home Assistant REST tool** (创建: 2026-07-11)
  - **状态**: 待作者操作，已标记为 stale-candidate。该 PR 提议添加一个原生 Home Assistant 集成，但似乎因作者未响应而停滞。
  - **链接**: [PR #8994](https://github.com/zeroclaw-labs/zeroclaw/pull/8994)
- **[Issue #8519] Reconcile cargo-audit ignores and remediate wasmtime-wasi CVEs** (P1, 已接受, 创建: 06-30)
  - **状态**: 依赖安全审计问题，涉及 wasmtime 的 CVE，已接受但超过一个月无进展。
  - **链接**: [Issue #8519](https://github.com/zeroclaw-labs/zeroclaw/issues/8519)
- **[Issue #7130] [Feature]: forbid(unsafe_code) workspace-wide** (P2, 已接受)
  - **状态**: 提升代码安全性的关键特性，已接受一个多月，无关联 PR。
  - **链接**: [Issue #7130](https://github.com/zeroclaw-labs/zeroclaw/issues/7130)

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*