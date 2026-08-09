# OpenClaw 生态日报 2026-08-09

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-09 00:43 UTC

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

# OpenClaw 项目动态日报 — 2026-08-09

> 数据来源：github.com/openclaw/openclaw | 数据窗口：2026-08-08 ~ 2026-08-09（实时）

---

## 1. 今日速览

OpenClaw 社区在 2026-08-09 展现出**高活跃度**：过去 24 小时产生 1000 条 Issue/PR 更新（各 500 条），其中新开/活跃 Issue 451 条（90.2%），关闭 49 条；PR 待合并 322 条（64.4%），合并/关闭 178 条。今日发布两个补丁版本（v2026.6.33 / v2026.6.34），核心方向为**浏览器与网络安全边界加固**。但需注意：**高优先级（P0/P1）Bug 存量较多**，尤其是内存泄漏（#91588）、网关启动失败（#108435）和消息静默丢失类问题（#116277、#44925），且多个 P0 尚无关联修复 PR，是当前项目健康度的主要风险点。社区讨论焦点集中在**消息送达可靠性**和**会话状态管理**两大主题。

---

## 2. 版本发布

### v2026.6.34（最新）

- **核心变更：** 加强浏览器与网络边界安全
  - 沙箱化浏览器路由（#97958）
  - 可信 DNS 目标（#38290）
  - 自定义浏览器来源（#103075）
  - 回环 Provider 端点（#110693），拒绝不安全访问路径
- **致谢：** @eleqtrizit, @brunowowk, @mosidevv, @pgondhi987
- **迁移注意事项：** 若使用自定义浏览器来源或回环端点，需检查现有配置是否适配新的安全策略

### v2026.6.33

- **核心变更：** 网络与密钥边界加固
  - Provider 流、Discord REST 响应、浏览器抓取、OAuth 路径、日志等场景增加响应大小上限（#96989, #95412, #99428）
  - Telegram 凭据从诊断信息中移除
- **致谢：** @wangmiao0668000666, @Alix-007
- **迁移注意事项：** 涉及日志格式变化，依赖诊断日志的自动化工具需适配

---

## 3. 项目进展（今日合并/关闭的 PR）

由于数据窗口内未明确标注"今日合并"的 PR 列表，以下基于状态变更（closed）及当前待合并的高价值 PR 进行说明：

**已关闭（178 条）**，代表性包括：

- **#120730** `fix(cron): resolve timer scheduling infinite loops and dropped timeouts`：修复 cron 计时器无限循环与超时丢失两个稳定性 Bug，属关键基础设施修复。

**待合并高价值 PR（322 条待合并中，以下为最值得关注）：**

| PR | 说明 | 评级 | 阻塞因素 |
|---|---|---|---|
| [#119981](https://github.com/openclaw/openclaw/pull/119981) | 新版 TypeScript 节点向后兼容旧版 Gateway，解决分段协议升级中节点无法连接的问题 | 🐚 platinum hermit | 等待维护者审查 |
| [#120575](https://github.com/openclaw/openclaw/pull/120575) | 防止轮询已完成的 exec 进程在后续心跳中重复出现完成通知 | 🐚 platinum hermit | 等待维护者审查 |
| [#120622](https://github.com/openclaw/openclaw/pull/120622) | 修复较新 legacy CLI assistant 可复活较旧 assistant 并造成终端上下文使用来源混淆的问题 | 🐚 platinum hermit | 等待维护者审查 |
| [#120434](https://github.com/openclaw/openclaw/pull/120434) | 记录运行结束工作树清理结果，并验证 Workboard 脏保留 | 🦐 gold shrimp | 等待作者 |
| [#120727](https://github.com/openclaw/openclaw/pull/120727) | 为云 Worker 会话提供实时桌面观察器（Labs 功能），使运维者可观看/协助 agent 在租用服务器上的工作 | 🧂 unranked krab | 等待作者 |

> **总体判断：** 核心代码库在**消息投递、会话恢复、进程生命周期管理**等方面有持续投入，但**大量高评级 PR 卡在"等待作者"或"等待维护者审查"阶段**，合并节奏偏慢，可能成为社区贡献者的主要挫败点。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|---|---|---|---|
| 1 | [#116277](https://github.com/openclaw/openclaw/issues/116277) DeepSeek v4 Flash 静默失败，仅返回通用回退消息（已关闭） | 179 | 模型调用失败时无明确错误提示，用户期望有降级策略和告警 |
| 2 | [#7707](https://github.com/openclaw/openclaw/issues/7707) 按来源标记记忆信任等级 | 31 | 防记忆中毒：区分用户指令/网页抓取/第三方技能来源，防止恶意指令注入影响后续行为 |
| 3 | [#44925](https://github.com/openclaw/openclaw/issues/44925) 子代理完成静默丢失，无重试、无通知 | 24 | 子代理任务编排失败模式过多，用户期望有明确重试/通知机制 |
| 4 | [#91588](https://github.com/openclaw/openclaw/issues/91588) P0 网关内存泄漏 350MB→15.5GB 导致 OOM 崩溃 | 22 | 严重稳定性问题，影响长时间运行部署 |
| 5 | [#80319](https://github.com/openclaw/openclaw/issues/80319) QA 工具默认套件混淆 Codex 原生工具与 OpenClaw 动态工具 | 17 | 社区 Clarify 类需求：明确工具差异，避免误报 |

---

## 5. Bug 与稳定性

### 🔴 P0 级（紧急）

| Issue | 描述 | 关联修复 PR |
|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | 网关内存泄漏，RSS 从 350MB 涨至 15.5GB，反复 OOM 崩溃 | ❌ 无，待维护者处理 |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 更新至 2026.7.1 后网关无法启动（systemd/ollama/手动均失败，报 `gateway did not start`） | ❌ 无，待维护者处理 |
| [#112395](https://github.com/openclaw/openclaw/issues/112395) | 6.11→7.1 升级后迁移预检阻塞网关，迁移表和租约均为空（回归） | ❌ 无 |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | Playwright CDP 会话未处理的断言错误导致整个网关崩溃 | ❌ 无 |

### 🟠 P1 级（高）

| Issue | 描述 | 关联修复 PR |
|---|---|---|
| [#116277](https://github.com/openclaw/openclaw/issues/116277) | DeepSeek v4 Flash 静默回复失败（已关闭） | ✅ 已关闭（需确认处理方式） |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成静默丢失，无重试/通知/自动重启 | ❌ 无，但 [#120601](https://github.com/openclaw/openclaw/pull/120601) 可防止 `sessions_yield` 在子代理仍运行时唤醒请求者 |
| [#106231](https://github.com/openclaw/openclaw/issues/106231) | 循环检测阻止 exec 但未终止卡住的 agent 运行，资源持续消耗 | ❌ 无 |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败可导致 agent 卡住数小时，无告警且未轮换 profile | ❌ 无 |
| [#98435](https://github.com/openclaw/openclaw/issues/98435) | MCP 回环传输在网关重启后不自动重新握手，`recovered=1` 具有误导性 | ❌ 无 |
| [#87327](https://github.com/openclaw/openclaw/issues/87327) | 隔离 agent 在 runtime-plugins 阶段卡住，cron 任务静默失败（2026.5.22） | ❌ 无 |
| [#114020](https://github.com/openclaw/openclaw/issues/114020) | 升级到 2026.7.2-beta.4 后飞书/Telegram 频道消息派发失败：`runChannelInboundEvent requires runDispatchLifecycle` | ❌ 无 |

### 🟡 值得关注（回归/稳定性）

- [#38327](https://github.com/openclaw/openclaw/issues/38327) 2026.3.2 与 google-vertex/gemini-3.1-pro-preview 搭配时出现 `Cannot convert undefined or null to object`
- [#87109](https://github.com/openclaw/openclaw/issues/87109) 网关空闲堆内存增长至 1073MB+，cron 任务在内存压力下静默失败
- [#91144](https://github.com/openclaw/openclaw/issues/91144) Windows 原生 CLI 网关 Scheduled Task 无法保持运行，前台窗口正常

---

## 6. 功能请求与路线图信号

### 高潜力（已有 PR 支撑或设计讨论）

| 需求 | 来源 Issue | 对应 PR/进展 |
|---|---|---|
| 内存授权（Memory Authorization）契约 | [#90916](https://github.com/openclaw/openclaw/issues/90916) | [#120760](https://github.com/openclaw/openclaw/pull/120760)、[#120773](https://github.com/openclaw/openclaw/pull/120773) 已提交，为后续身份感知内存策略做铺垫 |
| 本地市场订阅（Marketplace watches） | — | [#110438](https://github.com/openclaw/openclaw/pull/110438) 已提交，支持用户持久跟踪应用条目变更 |
| 云 Worker 桌面观察器（Labs） | — | [#120727](https://github.com/openclaw/openclaw/pull/120727) 已提交，解决无头云会话不可见问题 |
| Nephesh 梦境来源标记 | — | [#113896](https://github.com/openclaw/openclaw/pull/113896) 已提交，支持 `DREAMS.md` 中区分虚构与现实经历 |

### 中期关注（Discussion 阶段）

- [#7707](https://github.com/openclaw/openclaw/issues/7707) **记忆信任标签：** 社区呼声高（31 评论），且 #90916 的 memory-auth 契约可为其提供底层机制，有较强纳入路线图的可能
- [#10687](https://github.com/openclaw/openclaw/issues/10687) **完全动态模型发现（OpenRouter 等）：** 当前模型列表静态，用户无法快速使用新模型
- [#49740](https://github.com/openclaw/openclaw/issues/49740) **cron 自动重试：** 用户明确反馈每日 cron 失败要等 24 小时才能重试的痛点
- [#71195](https://github.com/openclaw/openclaw/issues/71195) **macOS Talk 模式接入 OpenAI Realtime：** 目标将对话延迟从 1.7–4.9s 降至亚秒级

---

## 7. 用户反馈摘要

### 核心痛点

- **消息静默丢失是最高频抱怨：** 涉及 DeepSeek 回复失败（#116277）、子代理完成丢失（#44925）、Slack 回复未投递（#96692）、WhatsApp 并发回复仅最新一条被投递（#92186）等。用户对"面板显示回复但渠道未收到"的行为尤为不满，认为这比无响应更糟。
- **内存/资源泄漏导致服务不可用：** #91588（350MB→15.5GB）和 #87109（空闲 558MB→1GB+）均指向网关内存管理存在系统性缺陷，且 cron 任务在内存压力下靜默失败，用户无法获知任务已失败。
- **升级回归频繁：** #108435（7.1 网关无法启动）、#114020（7.2-beta.4 飞书消息派发失败）、#108265（7.1 飞书流式渲染极慢）均为升级引入的回归，用户对升级风险存在顾虑。

### 积极信号

- 社区对安全边界改进有正向反馈（如 v2026.6.33/34 的发布内容）。
- 多个高难度/高价值 PR 正在推进（如 #120727 云桌面观察器），显示项目在**可观测性**方面有前瞻布局。
- 用户对功能请求的响应质量认可（如 #90916 的 topic-session 讨论深入）。

---

## 8. 待处理积压

### 长期未响应的 P0/P1 问题

| Issue | 创建时间 | 天数 | 说明 |
|---|---|---|---|
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | 2026-03-13 | ~149 天 | Playwright 断言错误崩溃网关，P1，无 fix PR |
| [#48810](https://github.com/openclaw/openclaw/issues/48810) | 2026-03-17 | ~145 天 | 压缩重试产生孤儿 fork，破坏链重建，P2 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026-03-06 | ~156 天 | Vertex/Gemini 回归，P1，13 条评论后仍待处理 |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 2026-02-06 | ~184 天 | 动态模型发现增强请求，P2，10 评论无结论 |

### 卡在"等待作者"的高价值 PR

| PR | 评估 | 等待时间 |
|---|---|---|
| [#119817](https://github.com/openclaw/openclaw/pull/119817) | 修复 hook 触发的心跳唤醒针对性，XL 级别 | 3 天 |
| [#113901](https://github.com/openclaw/openclaw/pull/113901) | 修复托管网关更新时 profile 错用问题，M 级别 | 15 天 |
| [#109163](https://github.com/openclaw/openclaw/pull/109163) | 修复 PowerShell exec 输出 BOM 渲染为文本，M 级别 | 24 天 |
| [#110438](https://github.com/openclaw/openclaw/pull/110438) | 本地市场订阅功能，XL 级别 | 22 天 |

> **维护者行动建议：** 优先处理卡在"等待作者"超过 2 周的 PR，协助作者完成收尾或明确关闭原因；同时关注 #91588（内存泄漏）和 #108435（升级后网关无法启动）这两个 P0 级问题，它们直接影响用户升级意愿和项目口碑。

---

*本日报由 AI 自动生成，数据基于 GitHub API 实时拉取。如需进一步分析或有特定关注点，请随时告知。*

---

## 横向生态对比

好的，作为资深技术分析师，基于您提供的 2026-08-09 各项目社区动态，我生成以下横向对比分析报告。

---

### 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于 **"从单点工具向平台化基础设施"演进的关键阶段**。主流项目（如 OpenClaw、IronClaw、Hermes Agent）均已进入高活跃度迭代期，核心关注点正从基础的对话能力转向**消息投递可靠性、会话状态管理、多用户协作与安全边界加固**。跨项目频繁出现的“静默失败”、“内存泄漏”和“权限绕过”问题，表明社区对系统的 **稳定性与健壮性** 提出了更高要求。同时，向 **团队级协作平台**（共享会话、审批流、多渠道触达）演进的趋势已现端倪。

---

### 2. 各项目活跃度对比

| 项目 | Issues (新开/活跃) | PRs (待合并/关闭合并) | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 451 / 49 | 322 / 178 | 2 个补丁 (v2026.6.33/34) | 🟡 **中风险**：P0 Bug（内存泄漏、网关崩溃）存量多，高价值 PR 合并积压。 |
| **Hermes Agent** | 38 / 12 | 32 / 18 | 无 | 🟡 **中风险**：核心痛点持续修复，但 P1 桌面冻结及更新体验问题突出。 |
| **IronClaw** | 6 / 24 | 18 / 32 | 无 | 🟢 **优秀**：架构迁移收尾，大批量关闭 Issue，新功能方向明确（Web Push等）。 |
| **NanoBot** | 5 / 0 | 5 / 4 | 无 | 🟢 **良好**：社区驱动开发闭环快（token诊断），但需关注 P0 数据一致性 PR。 |
| **NanoClaw** | 5 / 3 | 3 / 3 | 无 | 🟢 **良好**：Bug 响应迅速（Discord 审批修复），渠道扩展持续。 |
| **CoPaw** | 18 (未关闭) | 47 / 3 | 无 | 🟡 **中风险**：合并吞吐量低，积压严重，Docker 版本核心功能不可用。 |
| **ZeroClaw** | 48 / 2 | 48 / 2 | 无 | 🟡 **中风险**：安全类 P1/P0 问题密集（权限绕过、配置失效），协议层需加固。 |
| **PicoClaw** | 2 / 1 | 4 / 0 | 无 | 🟢 **良好**：修复方向明确（WhatsApp, 缓存），但合并节奏偏慢。 |
| **Moltis** | 1 / 1 (关闭) | 0 / 1 | 无 | 🟢 **稳定修复期**：长期 Bug 修复，社区反馈平稳。 |
| **LobsterAI** | 1 / 0 | 2 / 1 | 无 | 🟡 **沉闷**：活跃度低，Issue/PR 大量 stale，项目维护节奏放缓。 |
| **NullClaw / TinyClaw / ZeptoClaw** | - | - | - | ⚪ **无活动** |

---

### 3. OpenClaw 在生态中的定位

*   **优势**：
    *   **社区规模与活跃度绝对领先**：Issue/PR 数量级远超其他项目，是生态的绝对核心与风向标。
    *   **版本迭代节奏最快**：高频补丁发布（v2026.6.33/34），对安全与稳定性问题响应迅速。
    *   **功能广度与深度兼备**：从浏览器沙箱到消息边界加固，技术栈覆盖全面，代表了该领域的技术前沿。
*   **技术路线差异**：相较于 Hermes Agent 在桌面端体验的侧重或 IronClaw 向平台化的激进转型，OpenClaw 更偏向于构建**安全、稳定的核心网关与运行时**。其近期工作重心在 **网络边界加固** 和 **消息送达可靠性**，显示出“基础优先”的防御性策略。
*   **社区对比**：其社区不仅是用户，更是重要的代码贡献者（多个 P1/P0 修复 PR 来自社区）。然而，巨大的流量也带来了挑战，大量高评级 PR 卡在“等待维护者审查”，可能导致社区贡献者挫败感，是其当前最大风险。

---

### 4. 共同关注的技术方向

多个项目不约而同地聚焦于以下技术难点，表明这些是当前行业的普遍痛点：

1.  **消息/任务静默失败与可靠性**：
    *   **涉及项目**：OpenClaw、NanoBot、ZeroClaw、CoPaw
    *   **具体诉求**：OpenClaw 面临子代理完成丢失、DeepSeek 静默失败；NanoBot 关注后台任务数据覆盖；ZeroClaw 的 cron 任务输出被丢弃；CoPaw 的 MCP 超时阻塞。核心诉求是**可观测的、可重试的、有明确状态的事件投递机制**。

2.  **内存泄漏与资源管理**：
    *   **涉及项目**：OpenClaw、CoPaw、NanoClaw
    *   **具体诉求**：OpenClaw 网关内存从 350MB 涨至 15.5GB；CoPaw 前端空闲 CPU 占 20%；NanoClaw 的 Docker 数据库锁竞争。这要求在**长时间运行的常驻进程**中进行更精细的资源生命周期管理。

3.  **会话状态与上下文管理**：
    *   **涉及项目**：OpenClaw、Hermes Agent、ZeroClaw
    *   **具体诉求**：聚焦在会话压缩（Hermes Agent）、fork/分支状态一致性（Hermes Agent）、后台任务与新建会话的状态冲突（NanoBot）、以及用户退出界面是否中断任务（ZeroClaw）。**如何无缝、无损地在不同生命周期和入口点间传递会话状态** 是共同挑战。

4.  **安全边界与权限控制**：
    *   **涉及项目**：OpenClaw、ZeroClaw、Hermes Agent、PicoClaw
    *   **具体诉求**：从 OpenClaw 的浏览器沙箱化、ZeroClaw 的审批权限绕过、Hermes Agent 的 ANSI 脱敏绕过，到 PicoClaw 的 MCP OAuth 支持。**在赋予 agent 更多自主性的同时，如何构建多层、可验证的安全边界** 是所有项目的核心信条。

5.  **模型/服务接入的标准化与可观测性**：
    *   **涉及项目**：NanoBot、LobsterAI、CoPaw、NanoClaw
    *   **具体诉求**：NanoBot 对 token 消耗的细粒度监控；LobsterAI 集成 LiteLLM 统一网关；CoPaw 更换搜索 Provider；NanoClaw 支持远程 MCP。**摆脱供应商锁定、统一接入层、并对成本/性能进行可视化监控** 成为开发者共性需求。

---

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全功能个人 AI 助手中枢（消息、浏览器、多模态） | 高级开发者、追求最新功能的早期采用者 | 强健的网关 + 沙箱化执行环境，生态最丰富 |
| **IronClaw** | 团队级 AI 助手平台（共享会话、多渠道通知） | 团队、企业级用户 | 正在经历史诗级 Reborn 架构重构，强调安全模型与多用户协作。 |
| **Hermes Agent** | 桌面优先的深度集成 Agent（本地优先、UI 完善） | 专业个人用户、知识工作者 | 重桌面端（Tauri），提供丰富的原生体验，与系统深度集成。 |
| **NanoBot** | 轻量级、高性价比的 Chatbot 框架 | 开发者、追求简单部署与低成本运营 | 模块化架构，以代码优先，部署轻量，社区活跃但规模较小。 |
| **ZeroClaw / CoPaw** | 特定场景/协议深度优化的 Agent（SOP自动执行 / 国内厂商对接） | 有特定平台或业务流需求的企业用户 | 深入特定集成（如 WhatsApp、国内云厂商），在垂直场景功能强大。 |
| **NanoClaw / PicoClaw** | 渠道扩展优先（多IM集成 / 轻量级多通道） | 需要广泛连接聊天平台的用户 | 作为 OpenClaw 的生态补充，架构轻量，专注于连接器与通道适配。 |
| **Moltis / LobsterAI** | 沙箱环境工具链 / 教育或特定领域平台 | 对沙箱安全、特定领域有要求的用户 | 利基市场定位，分别强调沙箱兼容性和特定生态集成。 |

---

### 6. 社区热度与成熟度

*   **第一梯队（快速迭代期）**：**OpenClaw、IronClaw、Hermes Agent**。这三大项目拥有活跃的社区、庞大的 PR 流和明确的技术路线图。OpenClaw 体量最大但有积压风险，IronClaw 正处于架构转型的关键期，Hermes Agent 则在巩固桌面端体验。
*   **第二梯队（质量巩固期）**：**NanoBot、NanoClaw、CoPaw、ZeroClaw**。这些项目保持较高的 Bug 响应速度，社区参与度也不错，但体量和影响力小于第一梯队。它们正通过完善测试、修复深层次 Bug 来巩固其特定生态位。
*   **第三梯队（稳定维护/观察期）**：**PicoClaw、Moltis、LobsterAI**。这些项目活跃度有明显波动，PicoClaw 和 Moltis 处于修复期，而 LobsterAI 则有项目停滞风险，需要维护者注入新的活力。

---

### 7. 值得关注的趋势信号

1.  **从“个人框”到“团队基础设施”**：IronClaw 的共享会话、OpenClaw 的审批流、NanoClaw 的审批按钮，均表明 agent 正从单用户工具升级为**多人在线协作的基础设施**。这对权限模型（如 ZeroClaw 的群聊权限漏洞）和状态管理（多用户上下文隔离）提出了全新挑战。
2.  **安全与信任成为首要考量**：安全相关讨论在各大项目中占比显著提升。特别是 ZeroClaw 的“配置看起来安全但实际不安全”问题，反映了仅依赖配置项已不足以建立信任，未来需要**可验证的安全执行环境**（如 OpenClaw 的沙箱化）和**更严格的代码/技能审计机制**（如 Hermes Agent 的技能扫描）。
3.  **“后台自主运行”是硬需求**：用户不再满足于对话式交互，而是要求 agent 能根据 cron 或 SOP 在后台自主完成任务（ZeroClaw、NanoClaw、OpenClaw）。这要求系统具备**强健的后台任务调度、故障恢复和结果通知机制**，而当前的静默失败问题正是此方面的短板。
4.  **成本与可观测性紧密绑定**：NanoBot 的 token 诊断功能、OpenClaw 和 CoPaw 的内存泄漏问题，都指向同一个趋势：**开发者希望为 agent 的每一次行动（API 调用、资源占用）买单都能看到明细**。强大的成本监控和性能剖析能力将成为吸引重度用户的关键卖点。
5.  **标准化接入层成为刚需**：无论是 LobsterAI 集成 LiteLLM、CoPaw 更换 AnySearch、还是 NanoClaw 支持远程 MCP，都表明开发者厌倦了碎片化的集成。**将模型（LLM）、工具（MCP）、和渠道（Slack/Telegram等）通过标准化协议解耦**，是构建可维护、可扩展的 agent 应用的必然趋势。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-09

> 数据窗口：2026-08-08 至 2026-08-09 | 数据源：HKUDS/nanobot GitHub 仓库


## 1. 今日速览

过去 24 小时 NanoBot 社区活跃度处于**中高水平**：5 条 Issue 全部为新开且保持开放状态，9 条 PR 中有 4 条已被合并/关闭，项目交付节奏良好。值得关注的是，今日存在 **两条高度相关的线索**：Issue #5266（token 消耗异常）在引发社区讨论（13 条评论）后，已有一条配套 PR #5293（per-iteration token 诊断）被合并，且有后续 PR #5299 继续补全该功能的 WebUI 展示层——这是一个典型的由用户反馈驱动、迅速进入实现阶段的闭环案例。此外，一条 P0 级会话数据竞争条件修复 PR #5271 仍处于待合并状态，建议维护者优先关注。整体来看，项目正在围绕 **token 可观测性** 和 **稳定性加固** 两条主线稳步推进。


## 2. 版本发布

**无版本发布。** 过去 24 小时无 Releases 更新。


## 3. 项目进展

今日合并/关闭 4 条 PR，核心看点为 **token 可观测性链路的打通**：

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#5293](https://github.com/HKUDS/nanobot/pull/5293) | feat(usage): log per-iteration token diagnostics | 已合并 | 为每个 agent 迭代单独记录 token 消耗明细，直接回应 Issue #5266 的诊断需求。是构建完整 token 可视化体系的基础设施。 |
| [#5296](https://github.com/HKUDS/nanobot/pull/5296) | refactor: remove verified dead code | 已合并 | 移除 19 个仓库内部死代码单元和 11 个仅测试可达的生产路径，保留 6 个 API 敏感单元待后续兼容决策。项目健康度提升。 |
| [#5294](https://github.com/HKUDS/nanobot/pull/5294) | fix(webui): prevent image hover clipping | 已合并 | 修复 WebUI 中图片 hover 放大时边缘被容器裁剪的视觉问题，同时保留缩放光标和键盘焦点环。 |
| [#5252](https://github.com/HKUDS/nanobot/pull/5252) | feat(webui): add temporary chat mode | 已关闭 | 新增「临时聊天」模式，支持多轮对话但不落盘持久化，适合非敏感临时性会话场景。关闭状态可能意味着已转入其他分支或计划调整。 |

**项目整体向前推进情况**：token 诊断能力已进入核心代码库（#5293），但如前所述，完整的用户侧闭环（#5299）仍待合并（详见第 4 节），预计下个版本将具备「按会话/按迭代回溯 token 消耗」的能力。同时死代码清理（#5296）降低了后续维护成本。


## 4. 社区热点

| 条目 | 类型 | 评论数 | 热度分析 |
|---|---|---|---|
| [#5266 Logs about token consumption (too many tokens are burned)](https://github.com/HKUDS/nanobot/issues/5266) | Issue | **13** | 今日最热。用户报告 "2 小时内消耗数百万 token 且无明显用户活动"，属成本敏感型诉求。该 Issue 创建于 8/6，经过 2 天讨论发酵，已直接催生 #5293 的合并和 #5299 的提交，是今日最典型的社区驱动开发案例。 |
| [#5297 mcp增加oauth网页授权功能](https://github.com/HKUDS/nanobot/issues/5297) | Issue | 2 | 配置网页授权类 MCP server（如 xmind）时无发完成，诉求是支持 OAuth 网页授权并可通过 gateway 远程访问。 |
| [#5295 docker compose 部署 entrypoint.sh 权限错误](https://github.com/HKUDS/nanobot/issues/5295) | Issue | 2 | 部署阻塞性 Bug，`docker compose logs` 直接报 `Permission denied`，容器退出 code 2，影响新用户快速体验。 |
| [#5271 session 陈旧后台任务覆盖数据](https://github.com/HKUDS/nanobot/pull/5271) | PR（待合并） | — | 虽然评论数未提供，但标签含 `priority: p0`，属数据一致性级事故，值得关注（详见第 5 节）。 |


## 5. Bug 与稳定性

今日报告 2 个 Bug，另有 1 条 P0 级修复 PR 待合并，按严重程度排列如下：

| 严重度 | 条目 | 描述 | 是否有 Fix PR |
|---|---|---|---|
| **P0（数据一致性）** | [PR #5271](https://github.com/HKUDS/nanobot/pull/5271)（*待合并*） | 后台任务（如 `maybe_generate_webui_title`）持有 Session 引用跨越 `await` 期间，若用户执行 `/new` 触发 `session.clear()` → `save()` → `invalidate()`，后台任务随后保存会**覆盖新会话数据**。 | 本条即为修复 PR，尚未合并 |
| **P1（部署阻塞）** | [Issue #5295](https://github.com/HKUDS/nanobot/issues/5295) | docker compose 部署时 `entrypoint.sh` 报 `Permission denied`，容器启动失败（exit code 2）。属新用户入门阻塞问题。 | 暂无 |
| **P1（进程崩溃）** | [Issue #5300](https://github.com/HKUDS/nanobot/issues/5300) | 远程 MCP 返回 HTTP 530 时，异常处理路径触发 `RuntimeError: Attempted to exit cancel scope in a different task`，导致网关进程崩溃/卡死、任务泄漏、CPU 异常飙升。MCP 连接失败**未隔离**，单点故障导致整体不可用。 | 暂无 |

> **维护者关注建议**：PR #5271 为 P0 数据覆盖问题，建议尽快安排 review 与合并 — 该问题影响所有使用 `/new` 切换会话的用户，且属于静默数据丢失类型，风险极高。Issue #5300 的 MCP 故障隔离问题则涉及架构级韧性问题，建议优先排期。


## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 状态信号 |
|---|---|---|
| **Token 消耗详细日志（按调用/按迭代）** | [Issue #5266](https://github.com/HKUDS/nanobot/issues/5266) | **已落地**：核心日志（#5293）已合并；WebUI 展示（[PR #5299](https://github.com/HKUDS/nanobot/pull/5299)）待合并 |

**预计将被纳入下一版本的功能**：

- **WebUI 展示近期 token 消耗明细**（PR #5299，待合并）：以有界列表形式持久化近期 token 使用记录，包含 source/session 上下文、agent 迭代、请求工具等信息，并在 WebUI 展示 input/output/cached token 细分。
- **MCP OAuth 网页授权**（Issue #5297）：用户在配置需 OAuth 网页授权的 MCP server（如 xmind）时遇到阻碍，建议评估支持 OAuth 授权流程。
- **大型 MCP 工具集的 schema 瘦身预算**（Issue #5298）：当注册大量 MCP 工具时，全部 schema 传入 provider 会导致上下文开销过大，建议为模型可见的 MCP schema 设置“预算”机制。该功能与 token 成本优化的大方向一致，落地可能性较高。

**新特性信号（非功能请求，来自已合并 PR）**：
- **临时聊天模式**（PR #5252）已实现，为非持久化的多轮对话场景提供了支持。


## 7. 用户反馈摘要

综合今日 Issues 及评论内容，提炼以下真实用户声音：

**🔥 核心痛点：Token 成本不可见**

> "I notice that nanobot consumes enormous amount of tokens. Like million just in some 2 hours without any noticable activity for the user."

这是今日最强烈的用户声音（Issue #5266，13 条评论）。用户的诉求本质是 **成本可观测性**：不知道哪次调用、哪个环节消耗了 token，就无法针对性地优化。从合并 PR 的速度来看，维护者已迅速响应。建议在 WebUI 层（#5299）合并后，将该能力重点宣传。

**🧩 使用场景一：Docker 部署受阻**

> "docker compose logs -f nanobot-gateway reported: cannot open /usr/local/bin/entrypoint.sh: Permission denied"

该用户严格按照 deployment.md 执行却失败（Issue #5295），属 **新用户入门体验** 问题，可能涉及镜像构建或挂载权限配置，建议维护者复现并更新部署文档或修复镜像。

**🔌 集成场景短板：MCP 生态支持不足**

- OAuth 网页授权缺失（#5297）：用户希望接入 xmind 等需要 OAuth 的 MCP server 但无法完成，反映 MCP 集成能力仍需补全。
- MCP 连接故障**未隔离**（#5300）：单点故障导致网关崩溃和 CPU 飙升至异常水平，影响用户体验和部署稳定性。

**🛠 开发者的主动贡献**：今日 5 条 PR 由 4 位不同作者提交，社区参与度良好。


## 8. 待处理积压

| 条目 | 类型 | 创建时间 | 等待时长 | 建议 |
|---|---|---|---|---|
| [PR #4276 feat: model-agnostic computer use (computer_use + browser tools)](https://github.com/HKUDS/nanobot/pull/4276) | PR | 2026-06-10 | **约 2 个月** | 功能量大（跨桌面 + 浏览器两类后端），涉及面广，评审成本高。建议维护者拆分评审或明确阶段性计划，避免长期悬置拖延功能落地。 |
| [PR #5206 fix: log streamed responses exactly once](https://github.com/HKUDS/nanobot/pull/5206) | PR | 2026-08-01 | 8 天 | 修复流式响应日志重复打印问题，改动量小、风险低，建议尽快 review 合并。 |
| [PR #5271 fix: prevent stale background task saves from overwriting session data](https://github.com/HKUDS/nanobot/pull/5271) | PR | 2026-08-06 | 3 天 | **P0 数据一致性**，见第 5 节，建议立即安排评审。 |
| [Issue #5266 token 消耗异常](https://github.com/HKUDS/nanobot/issues/5266) | Issue | 2026-08-06 | 3 天 | 核心 PR 已合并，建议保留 Issue 至 #5299 合并后由用户验证关闭，形成完整闭环。 |


## 附：项目健康度速览

| 指标 | 数值 | 评估 |
|---|---|---|
| Issue 新建/关闭比 | 5:0 | 反馈涌入，需关注处理速度 |
| PR 合并/关闭比 | 4:9 | 合并效率尚可，因有 1 条关闭非合并 |
| 待合并 PR 数量 | 5 | 中等积压，建议优先处理 P0（#5271） |
| 待处理长期 PR | 2（#4276 两个月、#5206 八天） | 长期积压风险信号 |
| 今日贡献者数 | 8 人（Issue + PR 作者去重） | 社区活跃，参与度高 |

*报告生成时间：2026-08-09 | 数据截止 2026-08-08 24:00 UTC*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-09

## 1. 今日速览

项目维持高活跃度，过去 24 小时内有 50 条 Issue 更新（38 条活跃/新开，12 条关闭）和 50 条 PR 更新（32 条待合并，18 条已合并/关闭）。今日无新版本发布。当前讨论焦点集中在会话状态持久化（fork/branch 时推理字段丢失、压缩预算计算）、桌面端更新与平台兼容性（Windows/npm/Electron）、以及安全边界（技能内容扫描、ANSI 序列绕过令牌脱敏）。值得注意的信号：**12 条 Issue 已关闭**、**3 个推理字段修复 PR 已合并**——社区对 `#57240` 和 `#73624` 的多个修复方案已落地，长期痛点正被系统性清除。

## 2. 版本发布

过去 24 小时内无新版本发布。

## 3. 项目进展

**合并/关闭的 PR 中，今日最关键的推进是会话推理字段完整性修复。** 三个 PR（#82116、#82109、#57248）相继合并，共同解决了两个长期问题：

- **PR #82116** — 修复压缩预算将过期推理（stale reasoning）计入尾部预算，避免 19–24% 的压缩预算浪费在没有任何适配器回放的块上（Closes #73624）。
- **PR #82109** — 修复 fork/branch 会话时推理字段双重编码丢失的问题（Closes #57240），保障 CLI/TUI 分支写入时结构化推理列被正确复制。
- **PR #57248** — 与 #82109 同根因的独立修复，合并后确保 `get_messages()` 返回的推理字段在 fork 路径中保持一致。

其他推进的功能包括：

- **PR #82113（已合并）** — 修复桌面端 HUD 区域被工具块和通知挤占的问题，确保用户等待的回复不被挤出视野。
- **PR #82106（已合并）** — 桌面端 cron 编辑器交付方式从下拉单选改为多选复选框组，与调度器已支持的逗号分隔多目标格式对齐（salvage #73886）。
- **PR #82066（已合并）** — Anthropic OAuth 订阅计费指纹移植，保持消息历史增长时提示缓存有效，避免计费漂移。
- **PR #45014（已合并）** — 后台自我改进审查（Self-improvement review）的工具集可从配置控制，不再硬编码 memory/skills。

整体来看，**会话状态可靠性与桌面端体验是今日的主线**，多个 PR 从不同角度（压缩预算、fork 语义、HUD 布局、cron 多目标）提升了当前体验的稳定性。

## 4. 社区热点

**最活跃的 Issue 是 #63047（18 条评论）** —— 桌面应用在 macOS 27 beta 上发送约 5 条消息后完全无响应（包括设置界面）。这是 `#40692` 打字卡顿问题之外的更严重 UI 冻结，用户只能等待"解冻"或强制退出。该问题已持续近一个月，仍然开放。

**紧随其后是安全相关的 #78515（6 条评论）** —— 后台审查（background_review）写的技能默认跳过内容扫描（`guard_agent_created` 默认关闭），而这些技能会被注入到每个会话的系统提示词中。提交者明确将其作为纵深防御加固项而非漏洞声明，但社区的关注度体现了对 agent 自主生成代码信任边界的担忧。

**#81969（6 条评论）** 的情绪化标题（"scared to update because every other update bricks everything!"）反映了**更新可靠性问题对用户信任的侵蚀**——用户抱怨"每次其他更新都把一切搞坏，不断丢失配置需重来"。该问题与 #75778（更新交接产生重复 `hermes-setup` 实例）、#62171（npm 12 破坏 Linux 桌面更新）共同指向**更新链路稳定性是当前用户最直接的痛点**。

**#40801（6 条评论）** 继续吸引关注——cron 脚本路径守卫拒绝引用默认 profile 脚本目录的 profile-scoped 作业，这是 #32091 的反向场景，已开放两个月。

**PR 侧，`feat(browser): Browser Use CLI 3.0 mode`（#81958）已开放一天即获大量标签**，强调它是一个"单一 `browser_exec` 驱动覆盖所有 CDP 后端"的统一模式，可能成为浏览器工具链的重要简化。

## 5. Bug 与稳定性

按严重程度排列：

**P1 — 桌面端完全冻结（#63047）**
macOS 27 beta 上发送 ~5 条消息后 UI 完全无响应（含设置）。无 fix PR。已开放 27 天，累计 18 条评论，是需要优先关注的稳定性问题。

**P1 — 更新反复破坏环境（#81969）**
用户报告每两个版本就出现破坏性更新，导致配置丢失、需重新配置。无 fix PR，但 #75778（重复 `hermes-setup` 实例）在机制上解释了部分更新失败现象。**另有 3 个 PR 正在解决更新链路的 Windows/npm 兼容问题**（详见下条）。

**P1 — 桌面更新产生重复 updater 实例（#75778）**
macOS 上点击 Update 产生两个 `hermes-setup` 进程，第二个因 marker 冲突失败，其"失败窗口"掩盖了仍在运行的真实更新。无直接 fix PR。

**P1 — 压缩后 agent flush 不采纳 live continuation（#82001）**
会话被压缩关闭时仍持续写入的客户端，agent turn 会以 `session_persistence_failed` 失败并出现误导性的"full disk"对话框。根因是会话身份交接间隙。无 fix PR，昨日新开。

**P2 — 压缩清空人类可见的历史消息（#70846）**
上下文化压缩为 agent 裁剪上下文时，人类用户也失去了阅读早期对话的能力，影响事后记录与文档化。带 1 个 👍，无 fix PR。

**P2 — DeepSeek V4 Flash 0731 无限推理循环（#78807）**
当提示词开放/模糊或文件结构异常时，模型重复推理循环。无 fix PR。

**P2 — FTS 索引损坏无自动恢复（#63386）**
macOS 上 `hermes doctor` 检测到 `state.db` FTS 索引损坏，影响会话搜索与 handoff 状态。无 fix PR。

**P2 — lifecycle_guard 拒绝 ELF 二进制路径（#81322）**
终端命令包含 ELF 二进制路径（如 venv python）时抛出 `embedded null byte` 错误，良性命令被错误拒绝。无 fix PR。

**P2 — podman + SELinux：技能目录不可访问（#82074）**
自动挂载的 `~/.hermes/skills` 目录缺少 `:z` 重标记选项，rootless Podman + SELinux enforcing 下容器内无法读取。标记为 duplicate。

**P2 — 安全的 ANSI 序列绕过令牌脱敏（#81012）**
完整 CSI/SGR 序列（如 `\x1b[32m sk-xxx \x1b[0m`）可绕过 prefix masking——`_mask_control_split_tokens` 仅剥离 ESC 字节，留下 `[32m` 粘在令牌头部，字面量 `m` 导致整个令牌泄露。**安全边界问题，无 fix PR。**

**P3 — 桌面端 fork 按钮间歇性消失（#81846）**
需 reopen 会话才能恢复；无 fix PR，需复现。

## 6. 功能请求与路线图信号

- **浏览器工具统一（PR #81958）**：Browser Use CLI 3.0 模式，用单个 `browser_exec` 驱动替代 12 个 `browser_*` 工具。标记为 P3 但已附带 security/compatibility 风险评估，若合入将是浏览器能力的重大简化。
- **cron 作业在当前会话中运行（PR #81448）**：支持 `session_target: "current"`，让模型驱动的 cron 作业通过 gateway 路由在当前会话中执行，并保持路由连续性。已标 needs-decision，仍待维护者决策。
- **Claude Agent SDK 作为一等运行时（PR #65982）**：将官方 SDK 作为 Hermes 运行时（订阅 OAuth、fail-closed 防 metered billing），标记 `needs-decision` 已近一个月。若合入将打通 Anthropic 订阅用户的完整 SDK 能力。
- **内置内存生命周期管理（#78307）**：为 `MEMORY.md`/`USER.md` 增加检查、健康、去重、整合、冲突检测等一等公民 UX。标 needs-decision。
- **统一内容搜索（#49103）**：Cmd+K 中搜索文件、会话、技能。1 条评论，开放近两个月。
- **ToolCallStormBreaker（#35573）**：抑制重复 tool-call 循环（RFC 已开 2 个月）。相关新 bug #78807（DeepSeek 无限推理循环）或可为其提供新的现实依据。

## 7. 用户反馈摘要

**更新体验最伤信任。** #81969 直言"every other update breaks everything"，累计的配置丢失迫使反复重配。结合 #75778（重复 updater 实例）、#62171（npm 12 稳定版破坏 Linux 桌面）、#43997（npm 11 警告尚未修复）、#66978（每次 TUI 启动都跑 `npm install`），**更新与安装链路形成了密集的负面体验集群**。用户在 #81969 中特别强调"not giving me confidence in the product especially from a reputable..."，信任修复需要维护者对更新流程做系统性加固，而非单点修补。

**压缩机制的副作用开始被重视。** #70846 的诉求很实际："impossible to go back and read what you did earlier... for documentation later"——压缩应为 agent 省上下文，但不能剥夺人类阅读历史的能力。这与 #82001（压缩后 session 交接失败）共同构成了对压缩流程的体验质疑。

**安全边界关注度上升。** #78515 虽是"不是声称漏洞"的加固说明，但"技能未经扫描进入每个会话系统提示词"的观察获得 6 条评论，说明社区对规则引擎下 agent 自主行为的信任约束有真实需求。`#81012` 的 ANSI 绕过则是脱敏机制的具体漏洞，安全团队应优先评估。

**积极信号**：桌面端 HUD 空间优化、cron 多选交付、推理字段完整性修复的合并均收到正面反馈（PR 标签均为 `P2`/`P3` 但快速被处理），说明维护者对社区反馈的响应速度在提升。

## 8. 待处理积压

**高关注度未定问题：**

- **#63047**（P1、18 条评论、27 天）— macOS 27 桌面完全冻结，无 fix PR。这是当前评论最多且严重程度最高的未解决 bug。
- **#78515**（P3 security、6 条评论、5 天）— 技能内容扫描默认关闭。建议安全团队尽快决策是否调整默认值。
- **#40801**（P2、6 条评论、64 天）— cron 脚本路径守卫反向误拒。开放超两月，需明确行为预期。
- **#35573**（RFC、5 天前仍活跃）— ToolCallStormBreaker 已开放 71 天，仅有 2 条评论。如认可其必要性，建议并入 #78807 的修复方案一并设计。

**长时间未合并的关键 PR：**

- **PR #65982**（claude-agent-sdk provider）— 已开放 24 天、标 `needs-decision`。涉及会话状态、消息投递、安全边界、兼容性四重风险扫描（blast-broad），需维护者权衡合入成本。若合入将显著扩展 Anthropic 用户的使用方式。
- **PR #27040**（voice_server gateway）— 已开放 85 天。泛语音网关平台，涉及 4 项风险扫描。如果路线图不包含此方向，建议明确关闭或转由外部维护。
- **PR #81448**（cron 当前会话运行）— 昨日新开、标 `needs-decision`。若决策延迟，可能与其他 cron 功能更新产生冲突。

---

*日报生成时间：2026-08-09 | 数据来源：NousResearch/hermes-agent GitHub 仓库*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-09

> 数据窗口：2026-08-08 00:00 UTC 至 2026-08-09 00:00 UTC（基于 GitHub 更新记录）


## 1. 今日速览

过去 24 小时 PicoClaw 保持中等活跃度：共更新 7 项（2 个活跃 Issue、1 个关闭 Issue、4 个待合并 PR），无新版本发布。值得关注的是，两个新提交的 PR（#3320、#3321）均为本周内创建且直指实际故障——WhatsApp 通道因客户端版本过旧被服务器拒绝（405），以及 agent 动态上下文位置导致 prefix caching 失效，说明维护者和社区正集中解决影响真实用户的问题。另有 2 个历史 PR（#3222、#3193）仍在等待审查合并，已悬置超过一个月，存在积压倾向。整体项目状态良好，修复活跃但合并节奏偏慢。


## 2. 版本发布

无新版本发布。上次发布信息请参考 GitHub Releases 页面。


## 3. 项目进展

过去 24 小时无 PR 被合并或关闭，因此没有代码实际进入主分支。但有两个值得注意的待合并 PR 反映了即将推进的工作：

| PR | 内容 | 状态 |
|---|---|---|
| [#3320](https://github.com/sipeed/picoclaw/pull/3320) | 升级 `whatsmeow` 依赖，修复 WhatsApp 通道因客户端版本过旧被拒绝连接（`Client outdated (405)`），恢复原生 WhatsApp 通道 | 待合并，创建于 08-07 |
| [#3321](https://github.com/sipeed/picoclaw/pull/3321) | 将每次请求的动态上下文块（当前时间、运行时、会话、发送者）从系统消息前部移到对话历史之后，以保留 prefix caching 的有效性 | 待合并，创建于 08-07 |

若这两项合并，将直接修复 WhatsApp 通道不可用的故障，并提升长对话场景下 LLM API 的缓存命中率，降低延迟和成本。

此外，已有 PR 的更新动态：`#3222`（deltachat 重构）和 `#3193`（新增 simplex 通道）均在昨日更新后仍无新评论或审查动作，等待维护者介入。


## 4. 社区热点

**[#3287 — Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)**
- 状态：OPEN，创建于 07-22，4 条评论
- 背景：IRCv3 协议默认单条消息限制 512 字节，超长消息会被客户端自动拆分。用户要求 PicoClaw 将拆分后的消息当作完整消息处理。
- 分析：这是聊天适配层的协议语义问题，涉及 IRC 消息重组逻辑。4 条评论说明用户有实际使用场景，且该问题已被标记为 stale，暗示讨论热度已过峰。但从产品角度，IRC 仍是被支持的渠道，核心体验不应被忽略。

**[#3302 — Support OAuth 2.1 for MCP servers](https://github.com/sipeed/picoclaw/issues/3302)**
- 状态：OPEN，创建于 07-30，2 条评论
- 背景：用户引用已有 issue #2546，要求 MCP servers 支持 OAuth 2.1 认证。
- 分析：MCP（Model Context Protocol）生态正快速演进，OAuth 2.1 是新版 MCP 安全规范的核心要求。该请求被标记为 "Nice-to-Have"，但如果 MCP 是路线图重点，此需求可能被优先纳入。


## 5. Bug 与稳定性

过去 24 小时仅 1 个 Bug 相关 Issue 关闭，另有 2 个 PR 直接针对已知故障：

**中高严重度**

- **[#3320 — WhatsApp `Client outdated (405)` 故障](https://github.com/sipeed/picoclaw/pull/3320)**：WhatsApp 服务端拒绝当前客户端版本，导致连接建立后约 5 秒即断开且不重连，通道"死亡"。作者 `grrowl` 已提交依赖升级 PR，修复方案明确，待合并。
- **[#3321 — Prefix caching 失效](https://github.com/sipeed/picoclaw/pull/3321)**：动态上下文块位于 system message 中、全部对话历史之前。由于 prefix caching 基于位置敏感，任何前置 token 的变化（如当前时间）都会使整个缓存失效，导致长对话场景下每次请求都需重新计算。作者已提出修复方案。

**已关闭**

- **[#3292 — 聊天界面输入框聚焦时 CPU 占用过高](https://github.com/sipeed/picoclaw/issues/3292)**：状态已切换为 CLOSED（关闭于 08-08）。无关联修复 PR 可见，建议维护者确认关闭原因（已修复或转入内部跟踪）。

**低严重度**

- **[#3287 — IRC 长消息被拆分](https://github.com/sipeed/picoclaw/issues/3287)**：功能缺陷，非崩溃类，但影响 IRC 渠道的实际可用性。


## 6. 功能请求与路线图信号

| Issue/PR | 类型 | 潜在纳入版本 | 信号强度 |
|---|---|---|---|
| [#3302 — MCP OAuth 2.1](https://github.com/sipeed/picoclaw/issues/3302) | 功能增强 | 视 MCP 路线图优先级而定；若 #2546 已在规划，此请求自然合并 | 中 |
| [#3287 — IRC 长消息重组](https://github.com/sipeed/picoclaw/issues/3287) | 协议适配 | 待维护者回应；已有 stale 标签 | 中低 |
| [#3193 — 新增 simplex 通道](https://github.com/sipeed/picoclaw/pull/3193) | 新通道 | 若被合并，将是新渠道扩展；示例代码已含描述模板 | 中（依赖合并） |

**对下一版本的预判**：基于当前活跃 PR 内容，下一版本很可能包含 WhatsApp 通道恢复（#3320）、agent 缓存效率优化（#3321），以及可能合并的 deltachat 重构（#3222）和 simplex 通道（#3193）。其中 #3222 删减约 200 行代码、删除密码邮件配置等行为属于**破坏性变更**（需用户迁移到 jsonrpc secret 方式），依惯例可能随主版本或 minor 版本发布。


## 7. 用户反馈摘要

- **WhatsApp 通道故障影响直接**（PR #3320）：用户 `grrowl` 报告通道"完全不可用"（native WhatsApp channel stays dead），且明确指出根因——固定版本的 `whatsmeow` 库因版本过旧被服务端拒绝。反馈具有较强技术深度，直接给出修复路径，体现社区用户的专业度。
- **开发者关注基础设施效率**（PR #3321）：关于 prefix caching 的 PR 从内部机制层面优化 API 调用成本，说明已有用户在大规模或高频场景下使用，且对 token 成本和延迟敏感。
- **长消息场景需求**（Issue #3287）：IRC 用户认为被拆分的消息破坏了对话连续性，期望 PicoClaw 做语义重组。目前该 Issue 被标记为 stale，用户期待可能未得到充分回应。
- **MCP 生态跟进**（Issue #3302）：用户主动引用已有 issue 推进 OAuth 支持，显示社区对 MCP server 安全标准的关注在提升。


## 8. 待处理积压

以下为长期未响应或悬置时间较长的重要项，建议维护者关注：

| 项 | 创建时间 | 最后更新 | 说明 |
|---|---|---|---|
| [#3193 — simplex 通道支持](https://github.com/sipeed/picoclaw/pull/3193) | 2026-06-27 | 2026-08-08 | 已创建 43 天，无审查反馈。新渠道扩展有助于扩大 PicoClaw 覆盖面 |
| [#3222 — deltachat 重构](https://github.com/sipeed/picoclaw/pull/3222) | 2026-07-03 | 2026-08-08 | 已创建 37 天，清理大量 legacy 代码（-200 LOC），含破坏性变更，需及时评估 |
| [#3287 — IRC 长消息](https://github.com/sipeed/picoclaw/issues/3287) | 2026-07-22 | 2026-08-08 | 已被标记 stale，需明确是否排期或关闭 |

> 提示：以上 PR/Issue 均有用户活跃跟进，长期积压可能影响社区信任度。建议在下一个项目例会中评估优先级。


**总结**：PicoClaw 当前最紧迫的动作为合并 #3320 和 #3321 两项修复，随后评估 #3222 和 #3193 的合并窗口以释放新版本。项目整体健康度良好，社区参与质量较高，但合并节奏需要加快以避免积压恶化。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：** 2026-08-09  
**数据窗口：** 2026-08-08 至 2026-08-09（UTC）


## 1. 今日速览

NanoClaw 在过去 24 小时内维持了较高的社区活跃度，共产生 **8 条 Issue 更新**（5 新开 / 3 关闭）和 **6 条 PR 更新**（3 待合并 / 3 已合并或关闭）。值得关注的是，**Discord 审批按钮点击无效**这一严重影响核心协作流程的 Bug 已被定位并提交修复 PR（[#3185](https://github.com/nanocoai/nanoclaw/pull/3185)，待合并），该修复针对 webhook 交互中 `custom_id` 分隔符解码错误。与此同时，**Mattermost 频道集成**在一日内提交了新版本 PR（[#3202](https://github.com/nanocoai/nanoclaw/pull/3202)），表明渠道扩展仍在积极推进。总体而言，项目当前处于 **活跃开发 + 快速 Bug 响应** 的健康状态，核心协作链路问题在 24 小时内即获修复方案。


## 2. 版本发布

无新版本发布。


## 3. 项目进展

今日合并/关闭的 PR 展示了渠道集成与基础设施层的持续完善：

- **[PR #2776 — feat: support remote HTTP/SSE MCP servers](https://github.com/nanocoai/nanoclaw/pull/2776)（已关闭/合并）**  
  扩展 `McpServerConfig` 为联合类型，同时支持 stdio 与远程 HTTP/SSE MCP 服务器。新增 `McpServerRemoteConfig`（含 `type`、`url`、`headers` 等字段），并更新 `ncl groups config add-mcp-server` 命令支持 `--type`、`--url` 等参数。**意义：** 打破本地 stdio 限制，可对接远程 MCP 服务，对多机部署和外部服务集成有重要价值。

- **[PR #2777 — feat: add /add-strava skill for official Strava MCP](https://github.com/nanocoai/nanoclaw/pull/2777)（已关闭/合并）**  
  新增 `/add-strava` 技能，通过 HTTP transport 接入官方 Strava MCP 端点，包含基于宿主侧的 OAuth 流程（`scripts/strava-oauth.ts`）与 token 自动刷新模块。**意义：** 扩展了可集成的外部服务生态，为运动健康类 Agent 场景提供开箱支持。

- **[PR #3199 — Add Mattermost channel integration (v2 ChannelAdapter)](https://github.com/nanocoai/nanoclaw/pull/3199)（已关闭/合并）**  
  基于 v2 `ChannelAdapter` 架构全新实现 Mattermost 频道接入，取代了已失效的旧 PR #546。**意义：** 在 v2 架构下补齐了 Mattermost 支持，团队协作类渠道矩阵进一步完善。

> **小结：** 三合三关的节奏中，PR #2776 与 #2777 在同日合并并非偶然——二者均为 **clementdecoligny** 提交，表明远程 MCP 支持与 Strava 技能可能是有规划的功能批次。Mattermost v2 适配器的合入则为后续 PR #3202 的更新版奠定了基础，渠道支持整体正在向 v2 架构对齐。


## 4. 社区热点

今日最受关注的话题集中在 **Discord 审批按钮失效** 问题上，该 Bug 直接阻断多方协作流程中的核心审批动作：

- **[Issue #3201 — Discord approval button clicks not registering](https://github.com/nanocoai/nanoclaw/issues/3201)（已关闭，2 条评论）**  
  用户在 Discord 中点击审批卡片上的 Approve 按钮后，投票未被记录（仍显示 "0 by [user]"），请求最终被拒绝。该问题来自 `ncl groups config update` 指令后的多方确认环节，直接影响团队协作场景下的配置变更审批。社区反馈集中，已关闭（相关修复见 PR #3185）。

- **[PR #3185 — fix(discord): strip \n delimiter in webhook interaction custom_id](https://github.com/nanocoai/nanoclaw/pull/3185)（待合并，与 #3201 联动）**  
  该 PR 定位了根因：Chat SDK bridge 在解析原始 HTTP-interaction（webhook）时按 `:` 分割 `custom_id`，但 Discord 在按钮交互中会在 `custom_id` 尾部附加 `\n` 分隔符，导致解码错位。修复将剥离该分隔符，使审批按钮能正确映射到选项。**当前最需要社区/维护者关注的 PR，建议尽快合入。**（特别说明：该 PR 的作者为 omerh，不隶属于组织，注意遵循 CLA 流程。）

> **分析：** 审批按钮 Bug 触及多方协作（multi-agent）场景的信任根基。即使功能本身已实现，按钮点击无效会显著削弱用户对协作流程的信心，且社区给出的复现路径清晰，修复方案明确，有望在下个版本中解决。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 | 对应修复 |
|---|---|---|---|---|
| **高** | [#3201](https://github.com/nanocoai/nanoclaw/issues/3201) | Discord 审批按钮点击无响应，导致审批流程完全不可用 | 已关闭 | [PR #3185](https://github.com/nanocoai/nanoclaw/pull/3185) 待合并 |
| **高** | [#3177](https://github.com/nanocoai/nanoclaw/issues/3177) | Docker 跨挂载文件系统上 session 数据库锁竞争激烈（29,000+ readonly 错误），导致消息投递失败 | 已关闭 | 已修复（未知方式） |
| **中** | [#3206](https://github.com/nanocoai/nanoclaw/issues/3206) | 含路径分隔符的消息 ID（如 Google Chat）导致入站附件被静默丢弃 | 待确认 | 无 |
| **中** | [#3203](https://github.com/nanocoai/nanoclaw/issues/3203) | codex provider 发出未声明的 `file` ProviderEvent，`/add-codex` 在 main 上 typecheck 失败，生成的图片也会被丢弃 | 待确认 | 无 |
| **低** | [#3204](https://github.com/nanocoai/nanoclaw/issues/3204) | `add-opencode` SKILL.md 仍指示编辑 Dockerfile 中已不存在的 `ARG`/`RUN` 块，文档与代码不同步 | 待确认 | 无 |
| **低** | [#2528](https://github.com/nanocoai/nanoclaw/issues/2528) | Signal 频道中图片/PDF 附件从宿主到容器不可达 | 长期未解决（自 2026-05-18） | 无 |

**小结：** 高严重度问题（#3201、#3177）均在 24 小时内闭环，说明维护者对核心链路的关注度很高。但 #3206（附件静默丢弃）与 #3203（typecheck 失败）今日新开且暂无响应，建议尽快确认并排期。尤其 #3203 会导致代码生成类 Agent 产出图片不可用，影响面不小。此外，#2528 已持续近三个月且评论数为 0，值得维护者主动介入。


## 6. 功能请求与路线图信号

- **[Issue #3205 — Support persistent group-scoped OneCLI secret assignment](https://github.com/nanocoai/nanoclaw/issues/3205)（新开）**  
  诉求为 spawn-time 多用户场景下，为 Agent 分配 OneCLI 凭证需要持久化的按组（per-group）模型。当前存在两条设计方向互相矛盾且均无落地，用户期望明确统一。若能纳入路线图，将提升企业级多租户安全性。

- **[PR #3202 — Add Mattermost channel integration](https://github.com/nanocoai/nanoclaw/pull/3202)（新开，开放中）**  
  在 #3199 合并后重新提交的 Mattermost 集成版本（基于当前 ChannelAdapter 契约），闭合 #1379 需求。若合入，NanoClaw 频道矩阵将覆盖 Slack / Discord / Telegram / Mattermost / Signal / Google Chat 等主流 IM。

- **[PR #2877 — feat(telegram): native rich rendering via Bot API 10.1 sendRichMessage](https://github.com/nanocoai/nanoclaw/pull/2877)（开放中，自 2026-06-28 起）**  
  利用 Telegram Bot API 10.1 的 `sendRichMessage` 能力实现原生富文本渲染，目标提升 Telegram 端消息展示质量。已挂起一月有余，建议维护者予以关注评估。

> **路线图信号：** 远程 MCP 支持（#2776）已合入，将为 `/add-strava` 等外部服务技能铺路；Mattermost 二度提交表明社区对该渠道的持续需求；OneCLI 按组凭证模型若成行，将显著增强多用户场景的安全治理能力。


## 7. 用户反馈摘要

- **协作审批体验受损（#3201）：** 用户在 Discord 点击 Approve 后无任何变化，且请求最终被拒。该路径是多人协作时修改组配置的必经环节，此次故障直接导致流程中断。用户对功能本身的依赖度较高，Bug 影响感知强烈。
- **跨平台挂载的稳定性（#3177）：** 用户明确报告 SQLite DELETE journal 模式无法跨 Docker 挂载传播，导致大量 readonly 错误与间歇性投递失败（29,000+ 错误）。该问题在 macOS/Linux 上普遍出现，严重制约了 Docker 部署方案的可靠性。修复后用户未进一步反馈，可视为已解决。
- **长期未解决的 Signal 附件问题（#2528）：** 用户于三个月前报告 Signal 频道图片/PDF 无法在 Agent 容器中打开，至今无响应。考虑到 Signal 是隐私敏感场景常用渠道，该问题应纳入修复排期。
- **Mattermost 集成需求持续存在（#3202/#1379）：** 用户两次提交 Mattermost 集成（先 v1 后 v2），说明企业级团队协作中对 Mattermost 有明确需求，且在架构升级后主动适配了新契约，展现了较高的参与意愿。


## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 挂起时长 | 说明 |
|---|---|---|---|---|
| [Issue #2528](https://github.com/nanocoai/nanoclaw/issues/2528) | Bug（Signal 附件不可达） | 2026-05-18 | ~83 天 | 长期未响应，影响 Signal 频道基本可用性 |
| [PR #2877](https://github.com/nanocoai/nanoclaw/pull/2877) | 功能（Telegram 富渲染） | 2026-06-28 | ~42 天 | 已标注 follows-guidelines，待维护者审阅 |
| [PR #3185](https://github.com/nanocoai/nanoclaw/pull/3185) | Bug 修复（Discord 审批） | 2026-08-04 | 5 天 | 针对 #3201 的修复，建议优先合并 |
| [Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) | Bug（codex provider typecheck） | 2026-08-08 | 1 天 | 导致 `/add-codex` 无法通过编译，待确认 |
| [Issue #3206](https://github.com/nanocoai/nanoclaw/issues/3206) | Bug（Google Chat 附件丢弃） | 2026-08-08 | 1 天 | 附件静默丢失，需尽快确认 |


**结束语：** 过去 24 小时 NanoClaw 社区活跃度良好，高优 Bug 闭环迅速，渠道扩展与应用生态（Strava、Mattermost）同步推进。需重点关注 #3203 与 #3206 两个新开 Bug 的响应速度，以及 PR #3185 的合并节奏，确保协作链路的及时恢复。长期积压的 **#2528（Signal 附件）** 建议在下一轮维护中优先排期。整体项目健康度 **良好**，维持在高活跃区间。

---
*本报告由 AI 分析师生成，数据来源为 NanoClaw GitHub 仓库公开信息。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-09

## 1. 今日速览

过去24小时项目活跃度处于高位：共产生30条Issue更新（其中6条新开/活跃，24条关闭）和50条PR更新（其中18条待合并，32条已合并/关闭），无新版本发布。Reborn架构迁移战役进入批量收尾阶段——单日内关闭24个Issue中绝大多数为Reborn系列跟踪项（#3280、#3286、#3287等），同时Web Debug Inspector系列全部关闭（#7225、#7226），标志着这两个大型项目进入收尾。值得关注的是，昨日集中提交了多个核心PR：Web Push通知通道（#7398）、Slack/Telegram共享会话（#7397）、以及新的Epic #7392（用omp工具面替换自研编码工具），项目正同时向通知生态、多用户协作、工具标准化三个方向发力。


## 2. 版本发布

无新版本发布。注意IronClaw仍在Reborn架构迁移过程中，近期无release属正常节奏；相关里程碑见`v1.1.0`（#7218 Web Debug Inspector Epic）。


## 3. 项目进展

**今日合并/关闭的重要PR：**

- **#7377** [已合并] feat!: a run acts as its invoker — remove shared-route subject binding — 核心安全模型变更，让"运行"以调用者身份执行，是后续共享会话等功能的基石，同时包含多智能体审计的全部整改项。
- **#7382** [已合并] feat(stress): scripted tool-call workload with durable write read-back —— 解决#7360第一阶段，为压力测试增加确定性工具调用序列和持久化读回验证。
- **#7389** [已合并] fix(live-qa): verify triggered Slack delivery through the two-lane contract —— 修复 `#7157` 合并后live-qa持续失败的问题。
- **#7393** [已合并] test(disclosure): measure the Core delivery pair in the wide-catalog benchmark —— 基准测试补全。
- **#7280** [已合并] test(inspector): add browser, security, and operator coverage —— Inspector完整测试覆盖。
- **#6938** [已合并] fix(skills): the model chooses the skill, not a keyword scorer —— 重要设计变更：模型选择技能，而非宿主关键词打分。

**关键影响：** #7377的合并标志着运行身份模型全面切换到"以调用者身份运行"，配合#7397（共享会话）和#7398（Web Push），说明项目正向"一个agent服务多人、多渠道触达"的产品形态迈进——这是一次架构级的范式迁移。


## 4. 社区热点

**最热门Issue（评论数最多）：**
- **#3280** [已关闭] Add ProductWorkflow and InboundTurnService facade — 7条评论。虽是跟踪项，但作为Reborn产品面门面层核心，汇集了多个依赖项的链接，是迁移拓扑的关键节点。
- **#6989** [开放中] Token accounting: hybrid provider-usage + tail estimates — 5条评论。修复token估算缺陷，从"内容引用字符串长度"改为实际内容，属于计费正确性同级别问题，社区关注度高。

**最热门PR：**
- **#7398** [开放中] feat(web-push): browser push notifications + PWA — 项目首个第一方Web推送通道，目标是成为与Slack/Telegram平级的通知渠道，涉及RFC 8030/8291/8292完整实现。
- **#7397** [开放中] Presence-based shared conversations for Slack & Telegram — 基于#7377的acting-identity模型实现共享会话。

**热点诉求分析：** 今日热点集中在"多渠道触达"与"多用户协作"两个方向上。社区对Web Push和共享会话的高关注（两者均为XL级PR）表明用户已不满足于单机单用户的聊天机器人形态，而期望IronClaw成为团队协作基础设施。


## 5. Bug 与稳定性

**按严重程度排列：**

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| P1 | #6989 | Token估算缺陷：从 `content_ref.as_str().len()` 估算而非实际内容长度，直接影响计费准确性 | 🟡 开放中，有讨论 |
| P1 | #7391 | 安全问题：`SafetyLayer::validate_input` / `scan_inbound_for_secrets` 在实时Reborn turn路径上无调用者——文档声称的"检测泄露"关卡实际未生效 | 🟡 开放中，新提交 |
| P2 | #7352 | Gate投影身份重复：同一run上多个审批/认证gate生成相同投影ID，导致通知串线 | 🟢 有fix PR开放中 |
| P2 | #7395 | Send-claim TOCTOU竞态：CAS失败后错误分类，已允许失败行重开 | 🟢 有fix PR开放中 |
| P2 | #7341 | SS迁移后的attachment读取回归 | 🟢 已修复（PR开放中） |

**已修复（今日关闭的bug类）：** #7225、#7226（Inspector安全/浏览器覆盖完成）、#4382（OAuth gate重复触发）、#3905（用户级工具安装）。


## 6. 功能请求与路线图信号

**新功能请求：**
- **#6939** [开放中] Migration tool：将legacy agent（Hermes/Openclaw）的配置和记忆迁移到IronClaw——降低切换成本，商业上重要的用户留存手段。
- **#7392** [新Epic] Replace first-party coding tools with the pinned `omp` tool surface——将编码工具替换为社区通用契约，拥抱标准化。

**可能纳入下一版本的信号：**
- Web Push (#7398) 与 Shared Conversations (#7397) 均已提交PR，若评审顺利大概率进入v1.1.0或v1.2.0。
- 技能选择从"宿主关键词打分"改为"模型选择" (#6938) 已合并，是技能系统走向智能化的方向性变更。

**路线图判断：** 项目正在经历三重转型：(1) 从单通道到多通道/多端触达；(2) 从单用户到多用户共享会话；(3) 从自研工具到社区标准（omp）。这三者共同指向"团队级AI助手平台"的产品定位。


## 7. 用户反馈摘要

- **迁移成本痛点（#6939）：** 用户明确反馈从Hermes/Openclaw迁移到IronClaw需从零开始，配置、记忆全部丢失，"several users would resist starting over"。这是典型的转换成本障碍，尚无PR响应，值得产品侧重视。
- **安全承诺与实现差距（#7391）：** 用户对照文档发现 `docs.ironclaw.com/security` 描述的"Validate, Sanitize, Detect Leaks"数据流在实时路径上无调用者——安全文档描述与实际实现不一致，用户主动探查并提交issue。
- **技能安装后消失（#7171 PR描述）：** 用户安装技能后收到 `{"installed": true}` 但技能从设置中消失、无法激活——该问题已有修复PR。
- **限制审批/Auth门重复触发（#4382）：** 用户对同一provider多次触发OAuth门感到困扰，期望"设置一次永不再问"——该问题已修复。


## 8. 待处理积压

**长期未响应的重点事项：**

- **#6939**（迁移工具）— 创建于2026-07-31，已有9天。有2条评论但无PR认领。用户明确表达迁移成本是采用阻碍，建议尽快排期。
- **#7218**（Web Debug Inspector Epic）— 创建于2026-08-05，虽相关PR均在推进，但Epic本身无评论、无人更新状态。子任务已全部关闭，建议维护者及时更新Epic状态以免失联。
- **#7391**（SafetyLayer无调用者）— 创建于昨日，涉及安全文档与实现不符，尚无认领回应。**安全类问题建议优先响应。**

**PR积压提示：**
- **#7029 → #7048 → #7028 → #7395 → #7394** — theredspoon的栈式PR链（共5个PR），涉及outbound delivery claim、WASM诊断清理等。依赖关系复杂（#7029依赖#7028，等），且#7395标记为[contributor: new]，建议维护者安排review批次以避免长时间滞留。

---

**项目健康度总结：** 活跃度优秀（大量合并/关闭），Reborn迁移进入收尾、Inspector完工、安全模型(#7377)落地三大里程碑同日达成。新增方向（Web Push、共享会话、omp工具替换）表明项目正从"个人助手框架"向"团队级AI平台"演进。需关注：P1级token估算bug、安全文档不符问题（#7391）、以及新贡献者栈式PR的review积压。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报

**日期：** 2026-08-09  
**数据窗口：** 过去 24 小时（截至 2026-08-08 数据快照）

---

## 1. 今日速览

LobsterAI 项目今日处于**低活跃度**状态，过去 24 小时仅有 1 条 Issue 更新和 3 条 PR 更新，无新版本发布。值得注意的是，当前所有活跃的 Issue 和 PR 均已被标记为 `stale`（陈旧），其中最早的 Issue #1192（自定义默认配置）和 PR #1193（SQLite 写入优化）已搁置超过 4 个月，说明项目维护节奏有所放缓。不过，PR #2193（集成 LiteLLM 作为 AI 网关提供商）在昨日被关闭，以及 PR #2294（TakoAPI 目录徽章）仍在开放中，表明社区协作仍在持续。项目健康度整体**中等偏下**，需关注积压问题的处理节奏。

---

## 2. 版本发布

**无新版本发布。**  
上一次 release 信息不在本次数据窗口内，暂无更新内容、破坏性变更或迁移注意事项可报告。

---

## 3. 项目进展

今日**关闭/合并 1 条 PR**，另有 2 条 PR 仍在待合并状态：

| PR | 状态 | 内容 | 项目推进意义 |
|---|---|---|---|
| [#2193](https://github.com/netease-youdao/LobsterAI/pull/2193) `[CLOSED]` | 已关闭 | 集成 **LiteLLM** 作为 AI 网关提供商，用户可通过 OpenAI 兼容端点访问 100+ LLM 提供商，复用现有 `chatWithOpenAICompatible` 处理器，无新增依赖 | 扩大了模型接入生态，增强了项目作为 AI Agent 平台的兼容性，是近期较重要的功能扩展 |
| [#1193](https://github.com/netease-youdao/LobsterAI/pull/1193) `[OPEN]` | 待合并 | 消除 SQLite 写入放大问题——当前每次行变更都会触发全量 `db.export()` + `fs.writeFileSync()`，该 PR 引入 debounce + 批量事务机制 | 潜在的性能优化，若合可将大幅降低持久化开销，提升长时间运行场景下的稳定性 |
| [#2294](https://github.com/netease-youdao/LobsterAI/pull/2294) `[OPEN]` | 待合并 | 在 README 中添加 TakoAPI 开放 Agent 目录徽章 | 提升项目在 AI Agent 生态中的可见度与可发现性 |

**整体判断：** 今日项目中活跃的 PR 多处于搁浅状态，仅 #2193 有了结论（关闭而非合并），项目实质性的代码推进有限。

---

## 4. 社区热点

今日活跃度整体不高，相对讨论较多的是以下条目：

### Issue [#1192](https://github.com/netease-youdao/LobsterAI/issues/1192)：自定义已有工具的默认配置（`[stale]`）
- **作者：** duzhen1996
- **创建时间：** 2026-04-01，最后更新 2026-08-08（新增评论）
- **评论数：** 1
- **核心诉求：** 用户希望为内置工具（如 browser）预设**默认配置**（例如无头模式启动），因为依靠大模型指令跟随不可靠——模型经常忽略"无头模式"的指令。
- **背后分析：** 此类需求反映了 Agent 工具使用中一个共性问题：**用户希望获得确定性的工具行为**，而非依赖 LLM 每次生成时的随机行为。这指向了项目在"工具配置预置"能力上的欠缺，值得产品层面重视。

---

## 5. Bug 与稳定性

今日**无**新 Bug、崩溃或回归问题报告。  
值得注意的是，PR #1193（SQLite 写入优化）正在修复一个潜在的**性能/稳定性隐患**：当前 `SqliteStore.save()` 在每次行变更时都对整个内存数据库执行全量导出与磁盘写入，这在数据量增大或写入频繁时可能会导致明显的性能退化和 IO 放大。该 PR 已被标记为 `stale`，**建议维护者优先评估并推动合并**。

---

## 6. 功能请求与路线图信号

| 信号来源 | 需求描述 | 可能纳入版本判断 |
|---|---|---|
| Issue [#1192](https://github.com/netease-youdao/LobsterAI/issues/1192) | 允许用户直接硬编码工具的默认配置（如 browser 的无头模式），不依赖 LLM 指令 | **中高可能性**——这是一个实用性极强、痛点明确的需求；实现成本相对可控（增加配置项或配置文件支持），且与项目"可定制 Agent"的定位高度契合，建议团队排期考虑 |
| PR [#2193](https://github.com/netease-youdao/LobsterAI/pull/2193)（已关闭） | LiteLLM 多供应商接入 | 功能已完成代码实现，关闭原因未注明，是否会在后续版本中重新合入需澄清 |

---

## 7. 用户反馈摘要

从 Issue #1192 及其评论中可提炼以下真实用户声音：

- **核心痛点：** 大模型指令跟随不稳定，在需要确定性执行（如浏览器无头模式）时无法可靠生效。用户原话："大模型的指令跟随经常不好，没法无头模式启动"，流露出对 LLM 随机性的**不信任感**。
- **期望方向：** 用户希望拥有**更底层的控制权**——"直接写死一个默认配置"，这反映出部分用户更倾向于显式配置而非自然语言交互，提示项目需要提供**介于"全自动"与"全手动"之间的折中配置层**。
- **使用场景参考：** 用户提到"有时候我不想被打扰"，表明其使用场景涉及**无人值守或后台运行**，这类场景对工具行为确定性有较高的要求。

---

## 8. 待处理积压

以下条目长期未被响应，提醒维护者关注：

| 条目 | 类型 | 搁置时长 | 备注 |
|---|---|---|---|
| [Issue #1192](https://github.com/netease-youdao/LobsterAI/issues/1192)：自定义已有工具的默认配置 | Issue | 4+ 个月（自 2026-04-01） | 用户在上周（08-08）有新的评论互动，说明诉求仍然存在且有活跃用户关注 |
| [PR #1193](https://github.com/netease-youdao/LobsterAI/pull/1193)：SQLite 写入放大优化 | PR | 4+ 个月（自 2026-04-01） | 性能优化价值明确，长时间未合入可能导致后续合并冲突或社区兴趣降低 |
| [PR #2294](https://github.com/netease-youdao/LobsterAI/pull/2294)：TakoAPI 目录徽章 | PR | 1 个月（自 2026-07-08） | 低风险文档类 PR，合并成本极低，有助于提升项目曝光 |

**建议：** 优先推进 #1193 的技术评审，对 #1192 给予明确态度（是否排期），#2294 可直接快速合并以维护社区贡献者的积极性。

---

*本日报由 AI 自动生成，数据来源：[netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI) GitHub 仓库公开数据。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-09

## 今日速览

过去24小时内，Moltis 项目保持中等活跃度：新增1条 Bug 报告（Apple Container 沙箱检测误判），1条长期悬置的 Docker 工具链 Bug（#1096）被关闭，同时合并关闭了对应的修复 PR #1105（Docker 沙箱文件系统回退机制）。无新版本发布。整体来看，项目处于**稳定修复期**，核心关注点集中在沙箱环境下的工具兼容性上。

---

## 项目进展

**已合并/关闭 PR：**

- **#1105 [CLOSED] Fix Docker sandbox filesystem tool fallback** — 作者: penso（2026-06-05 创建，2026-08-08 更新） [链接](https://github.com/moltis-org/moltis/pull/1105)
  
  该 PR 为此前困扰用户近两个月的 Docker 沙箱文件系统工具失效问题（#1096）提供了系统性修复：为沙箱内 Read/Write/Edit/MultiEdit 操作增加回归测试覆盖，并在网关进程无法访问宿主机挂载路径时回退为容器内直接操作，同时保留直接宿主路径的缺失列表语义。这一修复意味着：

  1. Docker 沙箱环境中核心文件工具将恢复可用，**修复了#1096号Bug**（相应Issue今日已关闭）
  2. 增加了回归测试覆盖（/home/sandbox 和 workspace/data 路径），防止未来回归
  3. 沙箱工具链的健壮性得到显著提升

  > 📌 值得注意的是，该PR从创建到合并经历了约2个月（6月5日→8月8日），说明项目存在一定的PR处理延迟。

---

## 社区热点

**当前关注焦点：#1185 [Bug]** — Apple Container 1.x 沙箱检测误判 [链接](https://github.com/moltis-org/moltis/issues/1185)

- 作者 mikz 于 2026-08-08 提交，目前0评论、0👍
- 核心问题：Apple Container 1.x 沙箱进程**实际已在运行**，但 Moltis 将其误判为未运行状态
- 背后诉求：这反映用户对 **macOS 沙箱环境集成可靠性**的需求提升。类似 #1096 在 Docker 上的问题，现在 macOS 平台也出现类似的"工具与沙箱生命周期不同步"问题。这可能指向一个系统性问题：**Moltis 对各类沙箱环境的进程检测机制尚未做到跨平台统一**。

---

## Bug 与稳定性

| 严重程度 | Issue | 摘要 | 状态 |
|---------|-------|------|------|
| 🟡 中等 | [#1185](https://github.com/moltis-org/moltis/issues/1185) | Apple Container 1.x 沙箱运行但被误判为未运行 | 待处理，暂无 PR 关联 |
| ✅ 已修复 | [#1096](https://github.com/moltis-org/moltis/issues/1096) | Docker 环境下 Read/Write/Edit 工具失效 | 今日关闭，修复已合入 PR #1105 |

**分析：**
- #1185 的严重程度暂定为中等——因为它**不直接导致文件操作失败**，但会导致客户端侧出现状态误判（例如无法正确刷新UI、触发多余的启动流程等）。
- #1096 的关闭是今日最大的稳定性提升节点，解决了用户在 Docker 中无法使用核心工具的问题，历时约2个月。
- **风险提示**：#1185 与已修复的 #1096 在性质上高度相似（沙箱环境下的工具生命周期管理），建议维护者评估是否在根因上有共通之处，避免未来出现类似的第三例（如 Podman 或其他沙箱运行时的同类问题）。

---

## 功能请求与路线图信号

今日无新功能请求。但从 PR #1105 的实现细节中可提取以下路线图信号：

- **沙箱跨平台兼容性**被提上议程：Docker 修复完成后，macOS Apple Container 又出现检测问题，**下一阶段可能将沙箱生命周期管理作为独立模块重构**
- **回归测试的扩展**：PR #1105 新增的沙箱路径回归测试覆盖可能成为后续所有沙箱修复的标准测试模板
- **无新版本发布**，下一次版本迭代可能仍需等待 #1185 的处理结果

---

## 用户反馈摘要

今日用户反馈有限，但两条数据提供了有价值的信号：

1. **mikz（#1185）**：选择了 macOS 上的 Apple Container 1.x 作为沙箱环境，这说明**用户对 Moltis 的本地沙箱隔离能力有明确需求**，即使容器方案已有，仍希望原生 Apple Container 栈能正常工作。

2. **IlyaBizyaev（#1096，6月提交）**：在 Docker 环境中使用核心工具受挫约2个月，期间无追问（Issue 页无讨论记录）。这种情况应引起警惕——**沉默不代表满意，可能意味着用户已暂时转向其他工具或绕行方案**。

> ⚠️ 建议维护者在 #1096 关闭后主动联系该用户确认修复是否彻底解决问题，并邀请其确认回归测试覆盖是否满足实际使用场景。

---

## 待处理积压

| 类别 | 编号 | 说明 | 等待时间 | 优先级建议 |
|------|------|------|---------|-----------|
| Issue | [#1185](https://github.com/moltis-org/moltis/issues/1185) | Apple Container 沙箱状态误判 | 1天（新） | 高。类似问题曾在Docker上爆发，建议尽快响应，防止 macOS 用户群体放大 |
| Issue | （沿用 #1096 关闭） | — | — | — |
| PR | 无 | 当前无待合并PR | — | — |

**维护者提醒：**
1. **PR 处理周期过长**：PR #1105 从提交到合并历时2个月，远超健康项目的迭代节奏（通常1-2周）。建议检查当前PR积压情况和人力分配。
2. **Issue 响应速度**：#1096 悬置2个月才被修复，#1185 目前尚无 `triage` 标签，建议尽快打标签并指派负责人。
3. **平台覆盖策略**：Docker 和 Apple Container 相继出现同类沙箱工具兼容问题，建议在下一个 minor 版本中**将沙箱生命周期检测模块统一重构**，从根本上降低跨平台维护成本。

---

*本报告由 AI 分析师自动生成，数据截至 2026-08-09 00:00 UTC。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-09

## 1. 今日速览

CoPaw 在过去 24 小时保持高度活跃，共产生 18 条 Issue 更新和 50 条 PR 更新。Issue 方面以 Bug 报告为主（11 个 Open Bug），另有 4 个功能/增强请求；PR 方面待合并数量高达 47 条，但今日合并/关闭仅 3 条，合并吞吐量偏低。值得关注的是，多条高价值修复 PR（MCP 超时、前端动画 CPU 占用、审批路由字段、KeyError `__aiter__`）已同日提交，显示维护者与社区对近期集中暴露的稳定性问题响应迅速。整体项目健康度良好，但 PR 积压和 Docker 版本可用性问题值得警惕。

---

## 2. 版本发布

今日无新版本发布。当前最新版本为 v2.1.0-beta.2（Desktop/Tauri），社区已围绕该版本报告了多个问题（详见 Bug 与稳定性章节），建议维护者尽快推进 2.1.0 正式版的发布节奏。

---

## 3. 项目进展

今日合并/关闭的 PR 共 3 条，均为直接修复社区报告的 Bug：

| PR | 内容 | 关联 Issue |
|---|---|---|
| [#6836](https://github.com/agentscope-ai/QwenPaw/pull/6836) `fix(mcp): wire read_timeout_seconds into MCP SDK ClientSession` | 修复 MCP 客户端会话未正确应用 `read_timeout_seconds` 配置的问题，消除流式 HTTP MCP 请求无限挂起的风险 | [#6822](https://github.com/agentscope-ai/QwenPaw/issues/6822) |
| [#6835](https://github.com/agentscope-ai/QwenPaw/pull/6835) `fix(llm): resolve KeyError '__aiter__' during auto-title generation` | 修复非流式 provider 响应（dict 或纯文本）导致的聊天自动标题生成崩溃 | [#6813](https://github.com/agentscope-ai/QwenPaw/issues/6813) |
| [#6778](https://github.com/agentscope-ai/QwenPaw/pull/6778) `blog: agent memory upgrade practice` | 将代理内存升级实践指南从 `docs/` 迁移至站点输入目录，完善文档体系 | — |

**待合并高价值 PR 速览**（共 47 条，以下为最值得关注的）：

- [#6825](https://github.com/agentscope-ai/QwenPaw/pull/6825) `fix(mcp): apply configured timeout to client sessions` — 与 #6836 同源修复，提交更早但未合并，建议确认是否冗余
- [#6834](https://github.com/agentscope-ai/QwenPaw/pull/6834) `fix(console): pause offscreen infinite animations` — 直接修复#6828 的 20% 空闲 CPU 问题
- [#6833](https://github.com/agentscope-ai/QwenPaw/pull/6833) `fix(approvals): pass channel routing fields in driver gate` — 修复审批通知未送达正确渠道的问题
- [#6830](https://github.com/agentscope-ai/QwenPaw/pull/6830) `fix(memory): align compression and toolkit lifecycle` — 系统性修复 MemoryMiddleware 状态管理问题
- [#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817) `feat: integrate AnySearch web search` — 新增搜索引擎 provider，替代 Tavily

---

## 4. 社区热点

### 最热 Issue：Docker 版本插件/应用市场不可用
[#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) — **9 条评论**，v2.0.1 Docker 版本插件市场与应用市场始终提示"维护中"。该问题直接阻断 Docker 用户的扩展能力，评论数居今日之首，说明影响面较广，建议优先排查 Docker 镜像的 marketplace 服务地址配置。

### 次热 Issue：OpenAI Responses 续写摘要阻塞主对话
[#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) — **5 条评论**，Scroll 淘汰旧对话轮次时，同步请求主模型生成续写摘要，而带推理能力的模型此调用会阻塞主对话，且误报 60 秒取消为格式错误。该问题本质是**异步任务错误地占用了同步通道**，涉及架构层面的设计取舍。

### 热门 PR：Tavily 搜索被替代引发关注
[#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817) — AnySearch 作为内置搜索 provider 集成，**替换 Tavily**。该 PR 同时附带 MCP env-ref 空值绑定修复，属于"功能+修复"复合型贡献，社区对搜索 provider 的替换较为敏感，建议在合并说明中明确迁移路径。

---

## 5. Bug 与稳定性

### 严重级别：高

| Issue | 描述 | 影响面 | Fix PR |
|---|---|---|---|
| [#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) | OpenAI Responses 续写摘要忽略 `disable_thinking`，且 60 秒取消被误报为格式错误，阻塞主对话 | 使用 OpenAI Responses provider + 推理模型的用户 | 无 |
| [#6822](https://github.com/agentscope-ai/QwenPaw/issues/6822) | streamable HTTP MCP 瞬时断连后，自动重连无法恢复活跃对话，永久阻塞 | 使用远程 MCP 工具的用户 | ✅ [#6825](https://github.com/agentscope-ai/QwenPaw/pull/6825) / [#6836](https://github.com/agentscope-ai/QwenPaw/pull/6836) |
| [#6814](https://github.com/agentscope-ai/QwenPaw/issues/6814) | macOS 上打开 Scroll `history.db`（SQLite WAL 模式）触发 **SIGBUS** 崩溃（`sqlite3WalFindFrame`） | macOS 用户，打开 Scroll 历史记录时 | 无 |
| [#6828](https://github.com/agentscope-ai/QwenPaw/issues/6828) | Console 前端空闲时持续重绘（~20% CPU），根源为无限 CSS 动画（ai-copilot-blink + antd load-more spinner） | 所有 Desktop (Tauri) 用户，影响 UI 流畅度 | ✅ [#6834](https://github.com/agentscope-ai/QwenPaw/pull/6834) |

### 严重级别：中

| Issue | 描述 | Fix PR |
|---|---|---|
| [#6821](https://github.com/agentscope-ai/QwenPaw/issues/6821) | thinking-mode 模型（DeepSeek V4 系列）多轮对话时 `reasoning_content` 未回传，触发 400 BadRequestError | 无 |
| [#6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) | Gemini provider 发送含 `$schema` 字段的工具 schema 被 API 拒绝 | [#6809](https://github.com/agentscope-ai/QwenPaw/pull/6809) `fix(providers): sanitize Chat Completions content for strict providers` |
| [#6813](https://github.com/agentscope-ai/QwenPaw/issues/6813) | `consume_model_response` 对 dict 子类抛 `KeyError: '__aiter__'`，自动标题生成失败 | ✅ [#6835](https://github.com/agentscope-ai/QwenPaw/pull/6835) |
| [#6820](https://github.com/agentscope-ai/QwenPaw/issues/6820) | 前端 UI 在模型全部输出完成后才一次性显示，无流式渲染 | 无 |

### 严重级别：低

| Issue | 描述 |
|---|---|
| [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) | 助手消息结束时间显示异常（实际思考 2 分钟，页面显示几秒） |
| [#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) | Windows 安装/更新时未终止占用安装目录的进程，NSIS 弹出多个文件锁定错误 |
| [#6831](https://github.com/agentscope-ai/QwenPaw/issues/6831) | macOS Desktop 本地 Whisper 显示 `ffmpeg: disabled`，PATH 未包含 `/opt/homebrew/bin` |

---

## 6. 功能请求与路线图信号

### 已有 PR 支撑、大概率纳入下一版本：

1. **AnySearch 搜索引擎集成**（[#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817)）— 新增 SearchProvider + MCP，替换 Tavily，对应 [#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) 中"新增内置 provider"的方向
2. **NVIDIA NIM provider**（[#6526](https://github.com/agentscope-ai/QwenPaw/pull/6526)）— 已提交 12 天仍在待合并，建议维护者评估
3. **OpenAI Responses prompt caching**（[#6668](https://github.com/agentscope-ai/QwenPaw/pull/6668)）— 面向 GPT-5.6+ 的性能优化
4. **SSE 结构化运行结果**（[#5930](https://github.com/agentscope-ai/QwenPaw/pull/5930)）— 为 Java 等 API 自动化场景提供对话失败检测能力，已提交 30 天

### 暂无对应 PR、值得关注的新需求：

- [#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832) **审批时附带用途描述** — 用户在审批弹窗中无法直接理解 PowerShell 代码含义，建议 AI 用一句话说明审批用途。该需求影响审批体验，实现成本低，与 [#6833](https://github.com/agentscope-ai/QwenPaw/pull/6833) 的审批路由修复可一并考虑
- [#6827](https://github.com/agentscope-ai/QwenPaw/issues/6827) **删除对话时可选清理临时文件** — 对话删除后 agent 创建的临时文件成为孤立文件，建议提供清理选项。该需求涉及数据安全与磁盘管理，属于实用的运维性功能
- [#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) **Volcengine Agent Plan 与 Xiaomi MiMo API** — 新增两个国内云厂商 provider，已开放 13 天，社区有明确需求

---

## 7. 用户反馈摘要

### 真实痛点

1. **Docker 版本功能缺失严重**（[#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782)）："插件市场、应用市场始终提示维护中，无法使用" — Docker 用户被切断扩展能力，该问题已持续 2 天并获 9 条评论，可能为镜像内服务地址配置错误
2. **Windows 更新体验差**（[#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810)）："自动更新时报错卡死，只能强制退出"、"NSIS 连续弹出不止 4 个错误" — 更新前未检测并终止占用安装目录的进程，用户被迫手动卸载重装
3. **前端交互不透明**（[#6820](https://github.com/agentscope-ai/QwenPaw/issues/6820)）："全部完成了才显示出" — UI 无流式输出，用户无法感知模型实时处理状态，这与 [#4558](https://github.com/agentscope-ai/QwenPaw/issues/4558)（长文本输出 CPU 飙升）共同指向前端渲染管线需要系统性优化
4. **审批内容不直观**（[#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832)）："需要查看申请的 PowerShell 代码才能明白" — 用户期望一眼判断审批是否安全

### 使用场景延伸

- [#6821](https://github.com/agentscope-ai/QwenPaw/issues/6821) 显示已有用户在多轮对话中使用 DeepSeek V4 等 thinking-mode 模型，`reasoning_content` 回传问题直接阻断此类场景
- [#6819](https://github.com/agentscope-ai/QwenPaw/issues/6819) 用户通过截图反馈 Channel 工具在需要审批时无视觉提示，无法区分"正常调用"与"卡在审批"

---

## 8. 待处理积压

### 长期未响应的关键 PR（超过 7 天未合并）：

| PR | 提交时间 | 状态 | 说明 |
|---|---|---|---|
| [#5930](https://github.com/agentscope-ai/QwenPaw/pull/5930) `feat: add structured run outcome to SSE response` | 2026-07-10（**30 天**） | OPEN | API 自动化场景的关键增强，Java 服务无法感知对话失败 |
| [#6103](https://github.com/agentscope-ai/QwenPaw/pull/6103) `ci(coverage): raise frontend vitest thresholds` | 2026-07-14（**26 天**） | OPEN | 前端覆盖率门槛从 5% 提升至当前基线 22%，防止测试代码被静默删除 |
| [#6526](https://github.com/agentscope-ai/QwenPaw/pull/6526) `feat: Add NVIDIA NIM provider support` | 2026-07-28（**12 天**） | OPEN | 新增 NVIDIA NIM 模型 provider |
| [#6528](https://github.com/agentscope-ai/QwenPaw/pull/6528) `fix: resolve agent.json corruption (#6520)` | 2026-07-28（**12 天**） | OPEN | agent.json 相对路径解析错误 |
| [#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615) `fix(config): handle corrupted agent config and invalid JSON` | 2026-07-31（**9 天**） | OPEN | 损坏的配置文件导致应用启动崩溃 |
| [#6569](https://github.com/agentscope-ai/QwenPaw/pull/6569) `fix(console): suppress EIO/EPIPE print errors after detached TTY` | 2026-07-30（**10 天**） | OPEN | 终端关闭后后台进程持续报错 |
| [#6586](https://github.com/agentscope-ai/QwenPaw/pull/6586) `fix(mcp): recover stale server sessions` | 2026-07-30（**10 天**） | OPEN | MCP 服务器重启后会话恢复 |

### 长期未关闭的 Issue：

- [#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490)（Volcengine + Xiaomi MiMo 内置 provider）— 已开放 **13 天**，5 条评论，有明确功能定义但无对应 PR
- [#4558](https://github.com/agentscope-ai/QwenPaw/issues/4558)（长文本输出 CPU 飙升）— 已开放 **81 天**，今日因 [#6828](https://github.com/agentscope-ai/QwenPaw/issues/6828)（空闲时 CPU 20%）而被关闭，但后者仅修复了"空闲时"的动画问题，**"输出过程中"的渲染性能问题仍未解决**

---

## 项目健康度总结

| 维度 | 状态 | 说明 |
|---|---|---|
| **社区活跃度** | 🟢 高 | 24h 内 18 Issue + 50 PR，多个 First-time contributor 参与 |
| **Bug 响应速度** | 🟢 优秀 | MCP 超时、KeyError、CPU 动画问题均在 24h 内获得 fix PR |
| **PR 合并效率** | 🟡 偏低 | 50 条 PR 仅合并 3 条，47 条待合并，其中 [#5930](https://github.com/agentscope-ai/QwenPaw/pull/5930) 积压 30 天 |
| **Docker 可用性** | 🔴 存疑 | [#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) 中 Docker 版本核心功能不可用，需紧急排查 |
| **架构稳定性** | 🟡 中等 | MCP 会话管理（#6822）、OpenAI Responses 续写（#6811）、SQLite WAL 崩溃（#6814）均指向需要架构层加固的环节 |

**给维护者的建议**：优先处理 Docker marketplace 故障（#6782）和 macOS SIGBUS 崩溃（#6814）；尽快合并 MCP 超时双 PR（#6825/#6836）避免重复工作；对积压超过 2 周的 PR（#5930、#6103、#6526）给出明确合并计划或关闭原因，以维持贡献者积极性。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-09

> 数据周期：2026-08-08 至 2026-08-09 | 数据来源：GitHub Issues / PRs / Releases

---

## 1. 今日速览

过去24小时内，ZeroClaw 社区活跃度处于**高位**。Issue 侧新开/活跃 48 条、关闭 2 条，PR 侧待合并 48 条、合并/关闭 2 条，均达到 GitHub 数据返回上限（50条），表明实际流量或更高；所有条目均带 `status:no-stale` 标记，说明项目处于持续开发期，无沉寂议题。今日无新版本发布，但 **#9494 已关闭（合入）**，由 @Lusitaniae 提交的「Cron 启动的 headless SOP 运行」修复已落地，是今日最核心的进展。安全类 Issue（P0/P1）占据主导——包括 Telegram 群聊越权响应（#9348）、forbidden_paths 配置失效（#9815）、成本上报失效（#9816）等，安全侧需高度关注。另观察到两起与 Solana 钱包地址被高熵检测器误删除（#9486、#9825）相关的重复反馈，社区对误报问题有明确诉求。

---

## 2. 版本发布

过去24小时内无新版本发布。

> 注：#9853 正在推进 `aardvark-sys` 和 `zeroclaw-robot-kit` 两个 crate 的移除，涉及 crates.io 发布链路（#9381），预计下一个版本将伴随该清理工作，可能引入破坏性变更。

---

## 3. 项目进展

**核心合入：**

- **#9494 [已关闭] fix(sop): drive cron-started headless runs** — @Lusitaniae 提交，修复 cron 触发的 SOP 运行被搁置（`ExecuteStep` 仅停留在待处理状态）的问题。由 @JordanTheJet 接手并推出延续 PR **#9841**，额外修复了评审中发现和复查时的五个缺陷。解决了 SOP 自动模式的核心阻断问题。[PR #9494](https://github.com/zeroclaw-labs/zeroclaw/pull/9494) / [PR #9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841)

**合并的文档/基础设施变更：**

- **#9798 [已关闭] docs(sop): document which agent executes SOP steps** — 文档补丁，后被 #9841 取代（因运行时修复改变了临时行为）。[PR #9798](https://github.com/zeroclaw-labs/zeroclaw/pull/9798)

**方向总结：** 今日合入内容集中在 **SOP 自动执行链路**打通，加上 #9853（移除两个独立硬件 crate）和 #9580（网络防护基元迁移）等重构工作持续推进，项目整体在向**架构收敛**（合并同类 crate、集中安全控制）和**自动化可靠性**（SOP/CI）两个方向稳步前进。

---

## 4. 社区热点

**热点一：#8043 / #9803 — 硬件 crate 收敛的 RFC 讨论**

- [#8043 RFC: Retire the standalone aardvark-sys crate](https://github.com/zeroclaw-labs/zeroclaw/issues/8043)（评论 11，已关闭，8月8日仍有更新）
- [#9803 RFC: Retire the standalone zeroclaw-robot-kit crate](https://github.com/zeroclaw-labs/zeroclaw/issues/9803)（评论 2，新开于 8月7日，8月8日有更新）

#8043 获得 11 条评论，且已关闭（说明已形成结论并进入执行阶段）；#9803 作为其镜像提案，讨论则在进行中。两者的核心诉求一致：**缩减 workspace 中意义不大的独立 crate，统一到 zeroclaw-hardware**。`#9853` 已实际动工删除这两个 crate，说明社区讨论已转化为落地行动。

**热点二：#8424 — Workspace 内的文件保护诉求（11条评论）**

[Issue #8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) 提出当前 `forbidden_paths` 机制只能阻断 workspace **外部**路径，而像 `rust-toolchain.toml`、`.cargo/config.toml`、`.env` 等**工作区内**敏感文件无法被保护。目前处于 `needs-author-action` 状态，等待作者补充细节。该提案与 #9815（`forbidden_paths` 对 workspace 下路径完全不可达）形成呼应，说明**配置保护的可用性**是社区关注焦点。

**热点三：#8054 — 系统提示工具可用性与各入口点不一致（10条评论）**

[Issue #8054](https://github.com/zeroclaw-labs/zeroclaw/issues/8054) 指出核心 bug（系统提示告知推理模型"无可用工具"）虽已在直接 runtime 路径修复（#8053），但**同一类问题在其他入口点仍然存在**（channels、gateway、WebSocket、多模态、/think）。风险等级 P1，属于跨组件一致性问题。

---

## 5. Bug 与稳定性

**P0 级：**

- 无新增 P0 Issue。现有 P0 PR **#9571**（移除 WATI channel，XL 尺寸）仍处于待合入状态，涉及 CI、容器、安装器等大量文件变更。[PR #9571](https://github.com/zeroclaw-labs/zeroclaw/pull/9571)

**P1 级（按安全影响排序）：**

- **[S1 安全] #9348 — WhatsApp business 模式回复所有私聊和群组** — 配置显示为锁定实际全开放，`allowed_groups` 为空数组时放行所有群组。已有社区讨论但暂无 fix PR。[Issue #9348](https://github.com/zeroclaw-labs/zeroclaw/issues/9348)
- **[安全] #9815 — `forbidden_paths` 对 allowed_roots 或 workspace 下所有路径不可达** — `is_path_allowed` 在 allowed-root 检查时直接返回，根本不会走到 forbidden-path 比对逻辑。已 `accepted`，暂无 fix PR。[Issue #9815](https://github.com/zeroclaw-labs/zeroclaw/issues/9815)
- **[成本] #9816 — Anthropic provider 费用恒为 $0.00，日/月预算上限永不触发** — 每条 usage 记录写入 `cost_usd: 0.0`，预算控制形同虚设。已 `accepted`。[Issue #9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)
- **[安全] #9387 — Telegram/Slack/Lark/Matrix 交互式审批响应接受任意群成员** — 安全审计发现，权限校验缺失。`status:in-progress`，需跨四个 channel 修复。[Issue #9387](https://github.com/zeroclaw-labs/zeroclaw/issues/9387)
- **[功能] #8559 — 退出 Web 聊天窗口后 agent 停止工作** — S1 级别工作流阻断，用户退出界面即打断 agent 循环，无法后台继续任务。[Issue #8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)
- **[可靠性] #9390 — emergency stop 是仅 CLI 写的状态文件，无任何运行时路径读取** — 安全审计确认该功能形同虚设。[Issue #9390](https://github.com/zeroclaw-labs/zeroclaw/issues/9390)
- **[可靠性] #9340 — CLI 创建的 cron 任务输出被硬编码为 None** — 作业正常运行但结果被丢弃，且 run 状态记录为 `ok`，无任何提示。[Issue #9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340)
- **[可靠性] #8731 — stdio MCP 服务进程积累为僵尸进程** — 长时间运行后大量子进程未被回收，`in-progress` 状态。[Issue #8731](https://github.com/zeroclaw-labs/zeroclaw/issues/8731)
- **[测试] #9834 — zeroclaw-runtime 测试间歇性失败** — 进程级共享状态（turn_streamed receipts + model_switch）导致，已 `accepted`。[Issue #9834](https://github.com/zeroclaw-labs/zeroclaw/issues/9834)

**已有关联修复 PR：**

- **#9805 SOP 自动模式运行永不执行、卡死** — 已有 PR #9841 修复。[Issue #9805](https://github.com/zeroclaw-labs/zeroclaw/issues/9805)
- **#9390 emergency stop 无运行时读取** — 暂无 fix PR。
- **#9843 zerocode 长生命周期客户端 CPU 旋转** — 已关闭，标记 `r:needs-repro`。[Issue #9843](https://github.com/zeroclaw-labs/zeroclaw/issues/9843)

---

## 6. 功能请求与路线图信号

| 功能请求 | 相关 PR / 状态 | 是否可能进入下一版本 |
|---|---|---|
| **OpenAI 兼容 chat completions 端点**（#8550） | 无相关 PR；P2、`in-progress` | 可能性中。社区（Open WebUI、LobeChat 等）对标准协议接入有明确需求 |
| **Workspace 内敏感文件保护**（#8424） | 无相关 PR；`needs-author-action` | 可能性中高。与 #9815 同源，安全板块优先级高 |
| **简化 Web 工具集为 3 个动词**（#9824） | 无相关 PR；P1 tracker | 可能性中高。属于 agent 工具面收敛方向，与架构调整同步 |
| **Telegram 多消息模式**（#8445） | 无相关 PR；`in-progress` | 已有同类 PR #9772（per_user_session），说明 channel 层在活跃迭代，可能性中高 |
| **通过 CLI i18n 输出 status**（#7099） | 无相关 PR；P3 | 可能性低。P3 优先级长期未动 |
| **MCP 嵌入式资源 blob 物化**（#9179） | 无相关 PR；`in-progress` | 可能性中。依赖 #9580（网络防护重构）合并后推进 |

**路线图信号：** 今日最强信号是 **#9824**（简化 web 工具面）和 **#8424**（workpsace 内文件保护），二者均为 P1/P2 高优先级，标志着 agent 安全边界从「通道层」向「工作区内部」延伸。

---

## 7. 用户反馈摘要

- **对安全配置的信任感下降（严重）：** 多条 Issue 指向「配置显示安全但实际不安全」的问题。#9348 中用户明确表达担忧：*「A config that reads as locked down behaves as fully open, so an operator who believes they configured an allowlist gets an agent that replies to every inbound message」*。#9815 同样揭示了 `forbidden_paths` 配置「写了等于没写」的现状。此类问题比单纯的功能 bug 更影响用户对项目的信任。
- **高熵检测器误杀正常使用场景（重复反馈）：** #9486 与 #9825 连续两期反馈 Solana 钱包地址被强制替换为 `[REDACTED_HIGH_ENTROPY_TOKEN]`。用户反馈即便设置 `high_entropy_tokens=false`，在 channel 路径上依然被删除。这严重影响了 agent 在支付/金融场景中的可用性。#9825 明确指出这是**误报而非 bug**——检测器工作正常，但设计目标本身存在问题。建议维护者优先考虑为区块链地址类数据建立白名单或启发式豁免。
- **「后台运行」能力是用户刚需：** #8559 中用户反馈「退出聊天窗口即停止 agent 工作」为 S1 级阻断。结合 #9805 和 #9340，多条线索指向同一结论：**任务的 headless/后台执行能力是当前最大的使用痛点之一**，涉及 cron、SOP、web dashboard 三个入口。
- **Telegram 群聊场景需要更细粒度权限控制：** #9772 反馈当前 Telegram 群会话硬编码为 `Sender` 粒度，多人协作时无法在同一会话内区分不同用户上下文。#9387 则从安全角度揭示了审批接受任意成员响应的漏洞。两者结合，**telegram 群聊的会话隔离与权限模型**将成为近期 channel 层重点。

---

## 8. 待处理积压

**长期未闭合的重要 Issue：**

- **#5514 [P2] Telegram 媒体组分批为一次多模态调用** — 创建于 4月8日，已持续 4 个月，`in-progress`，无 fix PR。[Issue #5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)
- **#6663 [P2] Telegram partial streaming 模式下展示工具调用进度** — 创建于 5月14日，近 3 个月，`in-progress`，无 fix PR。[Issue #6663](https://github.com/zeroclaw-labs/zeroclaw/issues/6663)
- **#7099 [P3] zeroclaw status 输出接入 CLI i18n** — 创建于 6月2日，`in-progress`，P3 优先级长期未处理。[Issue #7099](https://github.com/zeroclaw-labs/zeroclaw/issues/7099)

**长期未合并的大 PR：**

- **#8337 [XL] herdr agent 上报集成** — 创建于 6月26日，已 44 天，无近期更新，是否需要维护者介入？[PR #8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)
- **#9265/#9266/#9268/#9272 Anthropic server-side fallback 系列四连 PR** — 创建于 7月22-23日，全部标记 `stacked`，系列 PR 依赖链较长，需整体评审。[PR #9265](https://github.com/zeroclaw-labs/zeroclaw/pull/9265)
- **#9248 [XL] eval run-history receipts** — 创建于 7月21日，`needs-author-action`，需要作者补充后推进。[PR #9248](https://github.com/zeroclaw-labs/zeroclaw/pull/9248)

**长期未合入的 P0/P1 安全类 PR：**

- **#9571 [P0/XL] 移除 WATI channel** — 创建于 7月30日，安全相关（移除废弃通道减少攻击面），XL 尺寸导致评审周期长。[PR #9571](https://github.com/zeroclaw-labs/zeroclaw/pull/9571)
- **#9410 [P1/S] 默认禁用命令审计日志** — 创建于 7月26日，S 尺寸但已两周未合入，涉及安全默认值，建议优先处理。[PR #9410](https://github.com/zeroclaw-labs/zeroclaw/pull/9410)

---

*报告完*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*