# OpenClaw 生态日报 2026-08-19

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-19 00:30 UTC

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

# OpenClaw 项目动态日报 — 2026-08-19

## 1. 今日速览

过去24小时项目保持高强度运转：共产生 500 条 Issue 更新（93%为活跃讨论）和 500 条 PR 更新（76%待合并），无新版本发布。值得关注的是，**事件循环阻塞**（#124788）、**SQLite 迁移/清理卡死**（#112423、#112395）等底层稳定性问题持续发酵，多个 P0/P1 级 Bug 已进入维护者审查或已有对应修复 PR。与此同时，以 steipete 为代表的维护者提交了一批高质量重构 PR（如统一插件重试运行时 #126065），显示项目在**稳定性加固**与**架构清理**双线推进。今日有 35 个 Issue 关闭、119 个 PR 合并/关闭，代谢健康。

- **活跃度**：★★★★★（极高，Issue/PR 均满 500 条采样上限）
- **项目健康度**：⚠️ 中等偏下 — 大量 P1 钻石龙虾级 Bug 积压，多个集中在会话状态/消息丢失/崩溃循环等核心路径
- **当前重点**：SQLite 状态层稳定性、Gateway 事件循环阻塞、CLI 迁移兼容性


## 2. 版本发布

过去 24 小时无新版本发布（最新版本停留在 2026.8.1-beta.2）。但从 Issue 趋势看，beta.2 的**事件循环周期性阻塞**（#124788）已引发社区对发布质量的关注。


## 3. 项目进展（今日合并/关闭的 PR）

**安全加固 🛡️**
- **安装策略警告确认机制落地**（#116489 已合并，关联 #120900）— 外部 `security.installPolicy` 命令现可返回 `warn`，授权操作者可在 CLI/UI 中审查可疑插件/技能安装并明确确认继续。横跨 CLI、Control UI、Gateway，是 7 月以来的重要安全特性交付。
- **Beam 抓取新增 SSRF 防护**（#123848）— 防止配置的接收端将带 bearer token 的请求体重定向到任意源。

**核心 Bug 修复（对应 Issue 已关闭）**
- **CLI 预检损坏状态库**（#101290 关闭）— 健康检查命令在 Gateway 运行期间可能触发 SQLite 损坏（"database disk image is malformed"）。该 P0 已在 main 分支定位并修复。
- **claude-cli 压缩路径失效**（#103231 关闭）— `ownsNativeCompaction` 假设对 `claude -p` 会话不成立，导致会话增长超 200% 且所有恢复路径静默失败。

**架构清理**
- **Telegram 测试解耦**（#125986）— 移除测试专用 `ForTest` 符号对生产缓存的重置依赖。

> **进度评估**：今日合入的 PR 集中在安全边界（安装策略、SSRF）和核心状态管理修复，与 Issue 热点高度匹配。但 381 个待合并 PR 的长期积压仍是瓶颈。


## 4. 社区热点 🔥

| 排名 | Issue/PR | 评论数 | 关注焦点 |
|------|----------|--------|----------|
| 1 | [#77598 – 开发 agent 行为持续观察](https://github.com/openclaw/openclaw/issues/77598) | 23 | 社区对**自主 agent 开发模式**的浓厚兴趣与围观（24小时观察日志） |
| 2 | [#112423 – SQLite 大事务清理阻塞事件循环](https://github.com/openclaw/openclaw/issues/112423) | 17 | 大转录归档在 Gateway 线程全量物化+压缩+I/O，**直接影响所有用户**的卡顿问题 |
| 3 | [#101290 – CLI 启动预检损坏状态库](https://github.com/openclaw/openclaw/issues/101290) | 15 | 已关闭但讨论热度高，反映**数据损坏类问题**的用户焦虑 |
| 4 | [#38327 – Gemini 3.1 模型调用报错](https://github.com/openclaw/openclaw/issues/38327) | 14 | 2026.3.2 回归，google-vertex/gemini-3.1-pro-preview 全量不可用 |
| 5 | [#79902 – SQLite 转录/会话 seams 功能请求](https://github.com/openclaw/openclaw/issues/79902) | 14 | 高级用户希望通过 SQLite 直接构建，绕开不透明 blob |

**诉求分析**：社区最强烈的两个信号 = **① 事件循环/性能稳定性**（多个钻石龙虾集中在同一根因）；**② 状态层透明化与数据安全**（SQLite 直接访问、快照语义、迁移可观测性）。两者都直指数据库优先运行时（database-first runtime）的成熟度。


## 5. Bug 与稳定性（按严重程度）

### 🔴 P0 — 阻塞发布

| Issue | 状态 |
|-------|------|
| [CLI 启动预检损坏状态库](https://github.com/openclaw/openclaw/issues/101290) | ✅ 已修复关闭 |
| [6.11→7.1 升级后 Gateway 无法启动（迁移表/租约空）](https://github.com/openclaw/openclaw/issues/112395) | ⚠️ 未修复，需产品决策 |

### 🟠 P1 — 核心路径故障

| Issue | 状态 |
|-------|------|
| [大 SQLite 转录清理阻塞事件循环](https://github.com/openclaw/openclaw/issues/112423) | 🔧 已有 PR #126035 待审查 |
| [SQLite 快照恢复缺少崩溃/身份保证](https://github.com/openclaw/openclaw/issues/113306) | 待维护者审查，需产品决策 |
| [Codex app-server 启动重试耗尽](https://github.com/openclaw/openclaw/issues/83959) | 卡在 `clawsweeper-recovery-stuck` |
| [Matrix 房间 agent 死循环/陈旧会话重放](https://github.com/openclaw/openclaw/issues/114211) | 待产品决策，需 info |
| [6.x 迁移致 Teams 会话库为 0 字节](https://github.com/openclaw/openclaw/issues/94939) | ⚠️ 关联 PR 打开 |
| [Windows 原生 Gateway 计划任务无法保持运行](https://github.com/openclaw/openclaw/issues/91144) | ⚠️ 关联 PR 打开 |
| [beta.2 事件循环每 10 分钟阻塞 ~100s](https://github.com/openclaw/openclaw/issues/124788) | 🔧 PR #126087 已修复重启恢复误报；主阻塞待查 |
| [重启后 usage-cost 刷新锁不可释放（容器 PID 复用）](https://github.com/openclaw/openclaw/issues/114234) | ⚠️ 关联 PR 打开 |
| [嵌入式助手阶段重试缺失（长轮次整体失败）](https://github.com/openclaw/openclaw/issues/117609) | ⚠️ 关联 PR 打开 |
| [Feishu 流式全量更新延迟回归](https://github.com/openclaw/openclaw/issues/91941) | ⚠️ 关联 PR 打开 |

### 🟡 P2 — 功能受损（节选）
- [DeepSeek V4 Flash 不完整轮次](https://github.com/openclaw/openclaw/issues/88657) — payloads=0, tools=2, stopReason=stop（5.27 回归）
- [Cron 迁移静默改 delivery.mode，频道报错](https://github.com/openclaw/openclaw/issues/90378)
- [主动记忆注入致 prompt 缓存命中率 99.9%→22%](https://github.com/openclaw/openclaw/issues/91223)

**观察**：今日修复 PR 高度聚焦在事件循环阻塞（#126035）、重启恢复（#126087）、子代理完成路由（#126032）等**根因相同或相邻**的问题上，主维护者 steipete 正在系统性地清剿回合管理/会话状态层的架构债。


## 6. 功能请求与路线图信号 📡

| 信号 | 来源 | 判断 |
|------|------|------|
| **插件重试运行时统一**（shared plugin retry runtime） | PR #126065（维护者 steipete） | 已就绪待审查，预计随下个 minor 合入 |
| **`agents set-default` CLI 命令** | PR #114036 | 就绪待审查，将解除删除默认 agent 的死锁 |
| **模型条目的目录元数据播种**（pin 尺寸字段时避免降级为文本模型） | PR #126068 | 新开 PR，修复配置加载时的隐性降级 |
| **会话目录刷新风暴治理**（web-ui） | PR #123535 | 就绪待作者，提升多会话页面的性能体验 |
| **Codex 隔离式 Computer Use 包更新** | PR #126080（stacked on #125883） | 新开，需 proof |
| **FaceTime 实时语音桥**（实验性插件） | PR #119291 | 新功能探索，需等待产品决策 |
| **宿主配置画像与一致性工具**（RFC 0023） | PR #114636 | 大 PR（XL）等待决策，建议关注 RFC |

下一版本（2026.8.1 stable）最可能纳入：**插件重试统一**、**会话清理防阻塞**、**模型配置播种修复**、**重启恢复体验改进**。值得关注的是 #125528（Claude CLI thinking 级别端到端修复）与 #125471（Claude CLI OAuth 刷新归属修复）组成的 **Claude CLI 修复系列**，期待合入。


## 7. 用户反馈摘要 💬

**最痛的点：**
1. **"无法解释的卡顿"成为新常态** — "gateway 事件循环阻塞 100 秒，WebSocket 全断，/ready 不响应"（#124788），用户反馈"每分钟都在发生，我不得不考虑回退版本"。
2. **升级恐惧症** — 6.11→7.1 升级后 Gateway 直接无法启动（#112395）；5.28→6.1 升级后 cron 静默变更且频道报错（#90378）——"升级就像抽奖"（多位用户共鸣）。
3. **会话状态丢失的多样性** — 从 CLI 预检损坏 DB（#101290），到迁移致 Teams 会话库 0 字节（#94939），再到 Matrix 陈旧会话重放（#114211），用户反复强调"**对话历史是最高优先级资产**"。

**被点赞最多的功能需求：**
- [#38327 回归问题获 3 👍](https://github.com/openclaw/openclaw/issues/38327) — 用户对"低版本能用、升级就坏"的模式越来越敏感
- [#77467 MiniMax OAuth 无法刷新获 3 👍](https://github.com/openclaw/openclaw/issues/77467) — 2 小时后强制重新认证，实际不可用
- [#10687 动态模型发现获 3 👍](https://github.com/openclaw/openclaw/issues/10687) — 静态目录无法跟上 OpenRouter 快速迭代


## 8. 待处理积压 ⏳

### 长期未响应/卡死的高价值 Issue（`clawsweeper-recovery-stuck` 标记）

| Issue | 创建时间 | 卡住天数 | 阻塞原因 |
|-------|----------|----------|----------|
| [#83959 Codex 启动重试耗尽](https://github.com/openclaw/openclaw/issues/83959) | 2026-05-19 | 92天 | 需产品决策 |
| [#94939 Teams 会话库 0 字节](https://github.com/openclaw/openclaw/issues/94939) | 2026-06-19 | 61天 | 关联 PR 打开，但 recovery-stuck |
| [#91144 Windows 计划任务不保持运行](https://github.com/openclaw/openclaw/issues/91144) | 2026-06-07 | 73天 | 关联 PR 打开，但 recovery-stuck |
| [#90098 大附件处理栈溢出](https://github.com/openclaw/openclaw/issues/90098) | 2026-06-04 | 76天 | 关联 PR 打开，但 recovery-stuck |
| [#111498 Anthropic 恢复后工作区迁移死锁](https://github.com/openclaw/openclaw/issues/111498) | 2026-07-19 | 31天 | 需维护者审查+产品决策 |

### 维护者关注建议
1. **#111498** 和 **#112395** 同属"迁移/恢复预检"类问题，建议合并根因分析。
2. **#88488 / #102534**（Cron 定时器永久停止触发）连续两周无维护者响应，涉及计划任务的核心可用性。
3. **待合并 PR 积压 381 个**，其中至少 20 个标有 `ready for maintainer look` 且为 P1/P2 关键修复（如 #126035、#126087、#126032），建议本周优先处理。

---

*本日报由 AI 分析师基于 2026-08-19 凌晨 GitHub 数据自动生成，链接均指向 openclaw/openclaw 仓库。*

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告

**日期：** 2026-08-19  
**分析范围：** OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、IronClaw、LobsterAI、Moltis、CoPaw、ZeroClaw（含 4 个无活动项目）

---

## 1. 生态全景

个人 AI 智能体开源生态正处于 **从"可用"向"可信"跃迁的关键阶段**。各项目不约而同地将重心从功能堆叠转向**稳定性加固、架构抽象与安全边界重构**——OpenClaw 在清剿事件循环阻塞与 SQLite 状态层缺陷，NanoClaw 在推进数据库异步化与运行时驱动抽象，CoPaw 在批量关闭 2.1.0 遗留 Bug。与此同时，**跨会话记忆、多通道一致性、Agent 自主性与异常路径恢复**成为全行业共同的技术攻坚点，反映出用户对智能体从"聊天玩具"升级为"自主生产力工具"的期待已形成共识。MCP（Model Context Protocol）生态与多引擎支持（dsh、hermes-agent 等）的渗透加速了这一进程——智能体不再依附于单一模型或单一运行时。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 版本发布 | 活跃度 | 健康度 | 阶段判定 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500（满采样） | 500（满采样） | 无（最新 2026.8.1-beta.2） | ★★★★★ | ⚠️ 中等偏下（P0/P1 积压、事件循环阻塞） | 广度扩张与稳定性瓶颈并存 |
| **NanoBot** | 9 | 26 | 无 | ★★★☆☆ | ✅ 良好（Issue-PR 闭环快） | 社区协作驱动的稳步迭代 |
| **Hermes Agent** | 50 | 50 | v0.20.4 | ★★★★☆ | ✅ 良好（但 PR 堆积 41:9） | 桌面端主导的快速迭代期 |
| **PicoClaw** | 6 | 4 | 无 | ★★☆☆☆ | ✅ 良好（stale 标记需关注） | 功能扩充与社区反馈消化期 |
| **NanoClaw** | 3 | 39 | 无 | ★★★★☆ | ✅ 良好（核心团队驱动、工程规范） | 主动架构演进期 |
| **IronClaw** | 22 | 39 | v1.3.0-rc.2 | ★★★★☆ | ✅ 良好（rc.2 修复升级崩溃） | 版本候选收尾 + 1.4.0 规划期 |
| **LobsterAI** | 9 | 20 | 2026.8.18 | ★★★☆☆ | ✅ 回升（批量清理 stale PR） | 技术债清理与功能合并期 |
| **Moltis** | 2（关闭） | 5（合并） | 20260818.08 / .06 | ★★☆☆☆ | ✅ 良好（积压清理出色） | 平稳迭代期 |
| **CoPaw** | 46 | 50 | 无（最新 2.1.0） | ★★★★☆ | ⚠️ 中等（PR 积压、MCP 双 Bug 悬而未决） | 2.1.0 收尾 + 贡献者活跃期 |
| **ZeroClaw** | 50 | 50 | 无 | ★★★★☆ | ⚠️ 攻坚期（多为 risk:high 待审 PR） | 安全加固与架构重构期 |
| **NullClaw / TinyClaw / ZeptoClaw** | 0 | 0 | — | — | — | 休眠/停更 |

> **说明：** OpenClaw 与 ZeroClaw 的 Issue/PR 数均触达 50 采样上限，实际活跃度可能更高；但 OpenClaw 的 P0/P1 Bug 密度显著高于其他项目。

---

## 3. OpenClaw 在生态中的定位

### 优势
- **社区规模遥遥领先**：Issue/PR 双满采样（各 500 条），是第二名（CoPaw/ZeroClaw 各 50 条）的 10 倍，生态号召力与用户基础无可匹敌。
- **功能广度业界领先**：横跨 CLI、Control UI、Gateway、多通道（Telegram、Matrix、Feishu、Teams）、多模型（Gemini、DeepSeek、Claude）及 SQLite 状态层，是生态中"全家桶"程度最高的项目。
- **维护者投入强度高**：尽管 Bug 积压严重，但 steipete 等核心维护者在当日提交了 3+ 个相邻根因的高质量修复 PR（事件循环、会话状态、子代理路由），展现出系统性的清剿能力。

### 技术路线差异
- **数据库优先（database-first）**：OpenClaw 将 SQLite 作为状态层基础，所有会话、转录、快照均围绕 SQLite 构建。这是一把双刃剑——用户可直接访问数据（回应用户对 seams 的诉求），但 SQLite 的并发限制与阻塞写入成了当前最大的稳定性瓶颈（#112423、#124788）。
- **底层稳定性优先级低于功能扩张**：OpenClaw 的部分 P0 级缺陷存活时间远超同类项目。例如 #101290 在已关闭后才获社区广泛关注（说明修复滞后于用户感知），#112395 的升级崩溃至今未修复。

### 社区对比
与 NanoClaw 的 **核心团队集中驱动** 不同，OpenClaw 的社区呈 **大规模、分散、快速反馈** 特征——93% 的 Issue 为活跃讨论而非孤立报告，用户参与度和问题深挖能力强；但也带来了更高的噪音与更严格的 review 需求。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 | 本质 |
|---|---|---|---|
| **事件循环 / 异步阻塞** | OpenClaw（#124788 阻塞 ~100s）、IronClaw（#7714 写连接饿死）、CoPaw（#7102 冻结 10 分钟） | 单一大事务/IO 拖垮整个 Gateway 或会话 | 异步架构的审计与优化是共同瓶颈 |
| **SQLite / 数据库状态层** | OpenClaw（迁移损坏、清理卡死）、Moltis（heartbeat 配置整体重置）、NanoClaw（DB 异步化）、LobsterAI（外键约束级联） | 数据完整性、迁移安全、事务隔离 | 状态层是智能体的"记忆中枢"，其健壮性决定可信度 |
| **跨会话记忆与持久目标** | OpenClaw（proactive memory 注入）、Hermes（#88715 profile 身份）、ZeroClaw（#8303 Goal mode）、IronClaw（#7185 跨对话记忆）、NanoBot（#5372 ViBo） | 记忆跨回合、跨通道、跨重启保持一致 | 智能体能否从"会话工具"进化为"自主个体" |
| **多通道一致性** | OpenClaw（Teams 迁移 0 字节）、Hermes（桌面↔远程 gateway）、CoPaw（控制端停止飞书会话）、PicoClaw（LINE/IRC 配置失效） | 不同入口（CLI/Web/IM/桌面）行为对齐，身份不串线 | 多入口是标配，入口之间的状态一致性是深水区 |
| **MCP 生态集成** | CoPaw（#6470/5900 streamable_http）、Hermes（#89566 CIMD）、NanoClaw（#3322 You.com MCP）、LobsterAI（#1631 模板） | 工具发现、会话复用、连接稳定性 | MCP 正在成为智能体与外部世界交互的标准协议 |
| **安全边界加固** | OpenClaw（installPolicy 确认、SSRF）、ZeroClaw（Google STT 密钥泄露、KeySource trait）、CoPaw（沙盘 UV Run）、NanoBot（#4797 fork bomb 风险） | 防止误操作或恶意构造导致数据泄露与资源耗尽 | 安全是可信智能体的刚需，也是商业化前提 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|---|---|---|---|
| **OpenClaw** | 全功能覆盖（多通道、多模型、CLI/UI/API） | 开发者 + 高级用户，追求"开箱即用的全能助手" | SQLite-first 状态层、事件驱动 Gateway、插件化技能系统 |
| **NanoBot** | 轻量部署、WebUI/TUI 双前端、AgentLoop 后台任务 | 个人开发者、快速原型验证 | 模块化架构，社区 PR 高度活跃，注重跨平台（尤其 Windows） |
| **Hermes Agent** | 桌面端优先（Desktop App）、项目级 Agent、MCP 客户端 | 桌面工作流深度用户、macOS/Windows | Multiplex 多路复用架构（profile/transport/control 分层）、OAuth MCP |
| **PicoClaw** | TUI 友好、多通道（Discord/Telegram/IRC/LINE）、Raspberry Pi 部署 | 嵌入式设备与终端重度用户 | TUI-first、轻量级的 Claw 生态替代品 |
| **NanoClaw** | 平台级智能体运行时（Agent-based），Webex 等企业通道 | 企业 IM 集成、团队协作场景 | 集中式数据库异步化重构中、Session 驱动抽象、Docker 内置运行时 |
| **IronClaw** | 沙箱安全、自动化运行、memory 记忆、多模型（NEAR AI 生态） | 安全性敏感的任务自动化用户（NEAR 生态关联） | Reborn 运行时、沙箱化 E2E、基于运行时证据的确定性评估 |
| **LobsterAI** | 跨平台桌面客户端、多 Agent 管理、dsh 引擎 | 网易生态用户，Windows/macOS 桌面端重度用户 | 基于 OpenClaw 的 UI 增强壳层，引入 dsh 实验性引擎 |
| **Moltis** | 个人 AI 助手、自托管、Podman 沙箱 | 自托管与容器爱好者（尤其 Podman） | 滚动日期版本、Files library + Settings 浏览器、多容器支持 |
| **CoPaw** | 多通道聊天（飞书/QQ/Matrix）、Creator 插件、智能体协作 | 中国开发者为主，偏 To B 场景 | 2.1.0 稳定期、社区贡献者活跃、Pro 商业化信号 |
| **ZeroClaw** | 安全敏感部署、渠道任务、跨平台（Windows 支持欠缺） | 对密钥安全、自主 Agent 能力有高要求的开发者 | 安全审计优先、多界面（Web/TUI/渠道）并行、RFC 驱动设计 |

---

## 6. 社区热度与成熟度

### 第一梯队：快速迭代期（每日 40+ Issue/PR 更新）
- **OpenClaw**：规模最大，但也承受最大 Bug 积压压力。处于"功能广、债务深"的典型扩张阵痛期。
- **Hermes Agent / CoPaw / ZeroClaw / NanoClaw**：均处于高投入的主动演进期。Hermes 在桌面端承受新平台压力；CoPaw 在清理 2.1.0 遗留；ZeroClaw 聚焦安全与架构重构；NanoClaw 是唯一"核心团队集中驱动型"项目。

### 第二梯队：质量巩固期（每日 5-20 条更新）
- **IronClaw**：v1.3.0 候选版本发布，升级崩溃快速修复，正迈向稳定基线。
- **LobsterAI / Moltis**：清理历史 stale PR 与 Bug，处于"存量治理为主、增量谨慎"的巩固期。
- **NanoBot / PicoClaw**：社区贡献者驱动，PR 规模较小但闭环快，处于健康但低调的上升期。

### 休眠项目
**NullClaw / TinyClaw / ZeptoClaw**：过去 24 小时零活动。在活跃度分化明显的生态中，这类小项目面临贡献者流失与维护断档风险。

---

## 7. 值得关注的趋势信号

1. **"异常路径韧性"成为新的竞速赛道**。多个项目同时出现"单点故障（一个图片 URL、一个大事务、一次网络抖动）拖垮整个会话/系统"的 Bug——CoPaw 的 #7110（403 图片挂死会话）、OpenClaw 的 #112423（大转录阻塞事件循环）、IronClaw 的 #7714（写连接饿死）——这反映出**智能体的容错设计仍未跟上其功能复杂度**。能系统性解决这一问题的项目将获得显著差异化优势。

2. **跨会话记忆与持久目标是下一代智能体的核心战场**。ZeroClaw 的 Goal mode RFC、IronClaw 的跨对话记忆失败、Hermes 的 profile 身份问题、OpenClaw 的主动记忆注入——这些不是孤立需求，而是同一趋势的不同侧面：**用户期望智能体是"有连续性的个人助理"，而非"每次重新自我介绍的工具"**。记忆层的统一、可靠、可验证将成为 2026 年下半年的核心技术赛道。

3. **"多引擎"与"多运行时"不再可逆**。LobsterAI 集成 dsh、CoPaw 提供多个 Provider、Hermes 支持 OAuth MCP、NanoClaw 做 Session 驱动抽象——智能体运行时（Agent runtime）正在从"绑定单一模型"走向"模型无关 / 引擎可替换"。这降低了用户对单一供应商的依赖，但也要求架构层面做出更彻底的抽象（NanoClaw 的 `drivers/` 目录与数据库异步化是典型代表）。

4. **安全不再是与功能并列的选项，而是前置条件**。ZeroClaw 的密钥泄露修复、NanoBot 的 fork bomb 风险、OpenClaw 的 installPolicy 确认机制、CoPaw 的沙箱 UV 路径问题——**几乎每个项目都有未解决的安全债务**，且用户的容忍阈值在急剧收窄（ZeroClaw 用户直接卸载、NanoBot 用户一个月持续追问）。能系统性完成安全审计并显式公开安全响应流程的项目，将赢得用户信任的护城河。

5. **社区协作形态正在分层**。上层的 OpenClaw 像"操作系统"（基础设施 + 生态），中层的 CoPaw / Hermes / ZeroClaw 像"发行版"（围绕特定场景做深度集成），下层的 PicoClaw / NanoBot 像"轻量工具"（针对特定环境优化）。这意味着 **底层项目不必面面俱到，但应聚焦一个场景做到无可替代**；而最上层的项目则必须优先解决稳定性，否则会让整个生态对"功能丰富但不可信"产生疲惫。

---

*报告完毕。如需对任一项目/方向做深度拆解，可提供具体索引。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-19

## 1. 今日速览

NanoBot 项目在过去24小时内保持高度活跃，共产生 9 条 Issue 更新（6 条新开/活跃，3 条已关闭）和 26 条 PR 更新（20 条待合并，6 条已合并/关闭）。项目整体健康度良好，社区贡献者对 AgentLoop 后台任务生命周期管理、WebUI/TUI 修复等主题表现出高度关注。值得注意的是，有多对 Issue-PR 形成了一一对应的直接修复链路，显示出高效的社区协作响应机制。当前有 5 个 PR 处于待合并状态且已存在冲突标记（`[conflict]`），可能需要维护者介入解决。

## 2. 版本发布

过去24小时内无新版本发布。

## 3. 项目进展

今日关闭/合并的 6 个 PR 主要集中于 WebUI 和 TUI 的体验优化：

| PR | 内容 | 状态 |
|---|---|---|
| [#5433](https://github.com/HKUDS/nanobot/pull/5433) | 修复 Windows 平台上 exec 输出截断测试的确定性等待问题（测试稳定性） | 已合并 |
| [#5427](https://github.com/HKUDS/nanobot/pull/5427) | TUI 保持输入框始终可见并聚焦，优化点击交互，增加视觉区分度 | 已合并 |
| [#5432](https://github.com/HKUDS/nanobot/pull/5432) | TUI 在 API 凭证过期（HTTP 401）后自动刷新，并去重并发刷新请求 | 已合并 |
| [#5358](https://github.com/HKUDS/nanobot/pull/5358) | WebUI 新增轻量级跨会话消息传递功能，为每个持久会话分配稳定的服务器端 `@handle`，支持跨会话文本消息发送 | 已合并 |

此外，今日提交的一批新 PR 涵盖先前提案所对应的实现，包括 `socks://` 代理 URL 支持（[#5435](https://github.com/HKUDS/nanobot/pull/5435)）、Mattermost 系统消息过滤（[#5434](https://github.com/HKUDS/nanobot/pull/5434)）、AgentLoop 后台任务异常捕获与清理（[#5431](https://github.com/HKUDS/nanobot/pull/5431)、[#5430](https://github.com/HKUDS/nanobot/pull/5430)），均对应今日提出的新 Issue，修复速度值得关注。

## 4. 社区热点

最受关注的 Issue 为 **[#5149 [bug] no audio?](https://github.com/HKUDS/nanobot/issues/5149)**，共获得 6 条评论，持续时长超过三周仍未关闭。该问题涉及 WhatsApp 频道无法发送音频文件，相关日志显示 `neonize.utils.ffmpeg` 发出警告，推测与 ffmpeg 处理流程有关，尚未有对应的 fix PR。

此外，[#4797](https://github.com/HKUDS/nanobot/issues/4797)（shell 子进程无资源限制）虽创建已逾一个月，但在昨日获得新评论，说明安全议题持续受到社区关注。

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | 对应 PR |
|---|---|---|---|
| **高** | [#4797](https://github.com/HKUDS/nanobot/issues/4797) `ExecTool._spawn()` 子进程无 ulimit/cgroup/CPU/内存限制，LLM 可触发 fork bomb 等耗尽系统资源 | 已开放 44 天，仍无 fix | 无 |
| **中** | [#5429](https://github.com/HKUDS/nanobot/issues/5429) `AgentLoop.schedule_background()` 完成回调不检索异常，后台任务异常被静默吞掉 | 新开，待合入 | [#5431](https://github.com/HKUDS/nanobot/pull/5431) |
| **中** | [#5425](https://github.com/HKUDS/nanobot/issues/5425) 自定义 OpenAI 兼容提供商使用 `socks://` 代理时请求在到达提供商前失败 | 新开，待合入 | [#5435](https://github.com/HKUDS/nanobot/pull/5435)，另见[#5426](https://github.com/HKUDS/nanobot/pull/5426)（存在两个重复 PR，需维护者协调合并） |
| **中** | [#5417](https://github.com/HKUDS/nanobot/issues/5417) Windows 上 WebUI 因网关拒绝 venv PID 交接而退出 | 已关闭（对应 PR 待合入） | [#5415](https://github.com/HKUDS/nanobot/pull/5415) |
| **中** | [#5428](https://github.com/HKUDS/nanobot/issues/5428) `AgentLoop` 在会话任务结束后保留空的 active-task 组，长运行实例内存泄漏 | 新开，待合入 | [#5430](https://github.com/HKUDS/nanobot/pull/5430) |
| **低** | [#5149](https://github.com/HKUDS/nanobot/issues/5149) WhatsApp 无法发送音频消息 | 开放 22 天，无 fix | 无 |

**维护者注意**：[#5425](https://github.com/HKUDS/nanobot/issues/5425) 对应的修复出现了两个重复 PR（[#5426](https://github.com/HKUDS/nanobot/pull/5426) 由 Issue 提交者直接发起、[#5435](https://github.com/HKUDS/nanobot/pull/5435) 由其他贡献者提交），建议尽快协调合并方案。

## 6. 功能请求与路线图信号

- **Spend Firewall（花费防火墙）**：Issue [#5409](https://github.com/HKUDS/nanobot/issues/5409) 提出增加混合型 LLM 花费防火墙，防止用户无限循环导致预算失控。该建议来自社区对商业化转型的关注，尚未有对应 PR，值得维护者评估其优先级。
- **持久记忆集成（ViBo）**：Issue [#5372](https://github.com/HKUDS/nanobot/issues/5372) 提议集成 ViBo 记忆系统为 Agent 提供跨会话持久记忆，该 Issue 已被关闭，但所反映的“跨会话记忆”需求是社区持续关注的方向。
- **MCP 工具 Schema 预算**：PR [#5388](https://github.com/HKUDS/nanobot/pull/5388) 以增强模式新增模型可见 MCP 工具 schema 的字节预算控制（默认关闭、确定性子集选择），有助于在大模型上下文窗口限制下管理工具使用。
- **跨会话消息传递**：PR [#5358](https://github.com/HKUDS/nanobot/pull/5358) 已合并，未来考虑持续改进该功能的配额策略。

## 7. 用户反馈摘要

- **安全反馈**：有用户明确指出 `ExecTool._spawn()` 对子进程无资源限制，LLM 可能被诱导运行 `yes > /dev/null &` 或 fork bomb 耗尽系统资源，当前仅有超时限制（Issue [#4797](https://github.com/HKUDS/nanobot/issues/4797)）。此问题从 7 月初开放至今已逾一个月，社区持续关注但无对应修复。
- **音频文件发送问题**：用户反馈 nanobot 在 WhatsApp 上无法发送音频文件，虽能接收，但发送端 ffmpeg 相关警告信息表明可能存在转码或路径处理问题（Issue [#5149](https://github.com/HKUDS/nanobot/issues/5149)）。
- **Windows 平台体验**：多个 Windows 相关 Issue 表明该平台仍存在兼容性问题，包括虚拟环境 PID 交接失败、`curl` 别名冲突等。社区贡献者已积极提交对应修复（如 [#5415](https://github.com/HKUDS/nanobot/pull/5415)、[#5341](https://github.com/HKUDS/nanobot/pull/5341)），但用户核心诉求仍是“开箱即用”的 Windows 体验。
- **社区建议未被采纳但具有一定参考价值**：部分第三方[功能提案](https://github.com/HKUDS/nanobot/issues/5372)被关闭，提示维护者在商业化过程中需制定明确的社区贡献接受标准。

## 8. 待处理积压

以下 Issue 和 PR 长期未获响应或存在冲突标记，建议维护者近期优先关注：

### Issues


1. **[#4797](https://github.com/HKUDS/nanobot/issues/4797)** — 「shell 子进程无资源限制」已开放 44 天，属于安全缺口，建议尽快安排修复计划。
2. **[#5149](https://github.com/HKUDS/nanobot/issues/5149)** — 「WhatsApp 无法发送音频」已开放 22 天且有 6 条评论，无 assignee、无 fix，社区热度持续上升。

### PRs（存在冲突标记，需维护者协调处理）

| PR | 内容 | 备注 |
|---|---|---|
| [#4880](https://github.com/HKUDS/nanobot/pull/4880) | 默认将 `restrict_to_workspace` 设为 `True`（安全增强，对应 Issue #4796） | 开放超 1 个月，安全相关需尽快处理 |
| [#5257](https://github.com/HKUDS/nanobot/pull/5257) | 限制持续目标的空闲延续（fix，p2，含冲突标记） | 开放 14 天 |
| [#5420](https://github.com/HKUDS/nanobot/pull/5420) | WebUI 回合可观测性与安全恢复（含冲突标记） | 新提交即带冲突，建议立即处理 ⚠️ |

### 重复 PR 协调

- **socks:// 代理支持**：[#5426](https://github.com/HKUDS/nanobot/pull/5426) 与 [#5435](https://github.com/HKUDS/nanobot/pull/5435) 内容重合，需选择其一保留。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报

**日期：** 2026-08-19  
**数据窗口：** 2026-08-18 ~ 2026-08-19（24小时）


## 1. 今日速览

过去 24 小时项目保持高活跃度：共产生 50 条 Issue 更新（新开/活跃 39、关闭 11）和 50 条 PR 更新（待合并 41、合并/关闭 9）。值得关注的是 PR 待合并数量显著高于已合并数量（41:9），表明维护团队正在集中处理一批提交，合并压力较大。v0.20.4 补丁版本发布，聚合了自 v0.20.3 以来约 74 个 PR，为下游用户提供了稳定基线。桌面端（Desktop）相关 Issue 和 PR 占据了较大的关注份额，涉及 CPU 占用、连接路由、MCP 会话等横切多个组件的问题，反映出桌面端已成为用户使用的主要入口，也承担了最多的稳定性压力。此外，多个 Issue 与 PR 之间存在直接关联（如 #89131 ↔ 审批超时、#89576 ↔ 会话固定），说明社区的反馈正在快速转化为修复。


## 2. 版本发布

### v0.20.4 (v2026.8.18) — 2026-08-18 发布

> 补丁版本。该标签将 v0.20.3 以来合并的约 74 个 PR 汇总为一个稳定的带标签版本，供下游消费者（Docker 镜像、托管部署、全新安装）使用。

**更新内容要点：**
- 自 v0.20.3 以来约 74 个 PR 的累计修复与功能改进
- 面向 Docker 镜像、托管部署及全新安装的稳定基线

**破坏性变更：** 补丁版本，预期无破坏性变更。

**迁移注意事项：** 下游消费者应更新部署标签至 `v2026.8.18` 以获取累计修复。


## 3. 项目进展

今日合并/关闭的 PR 中，以下对项目整体推进有明确贡献：

**桌面端 UI 修复（已合并/关闭）：**
- [#89572 feat(desktop): SESSIONS/BOTS tabs lose the ✕](https://github.com/NousResearch/hermes-agent/pull/89572) — 解决了持久导航标签页上的悬停关闭按钮问题（修复 #89546），改为右键菜单和 ⌘K 控制显隐，选择跨启动持久化。该 PR 还捡取了 #89551 的提交。
- [#89551 fix(desktop): hide hover close buttons on Sessions and Bots tabs](https://github.com/NousResearch/hermes-agent/pull/89551) — 隐藏持久导航标签的悬停 × 关闭按钮，保留普通可关闭面板标签的关闭功能。

**自动化维护：**
- [#89580 fmt(js): `npm run fix` auto-fix](https://github.com/NousResearch/hermes-agent/pull/89580) — 自动格式化 PR（机器人提交），CI 通过后自动合并，维持代码风格一致性。

**认证与安全相关（代码已提交但尚未合入 main）：**
- [#89566 feat(mcp): CIMD client identification for OAuth MCP](https://github.com/NousResearch/hermes-agent/pull/89566) — 使 Hermes 在 OAuth MCP 服务器上通过 CIMD 机制识别自身，为 MCP 生态提供更完善的客户端识别能力（捡取自 #84050）。**该 PR 尚未合并**，位于待合并队列中。

**总体评估：** 由于 41 条 PR 仍处于待合并状态，项目目前处于大批量提交的堆积期。一旦合并，将带来 MCP 会话管理、跨平台稳定性、桌面 UI 等多方面的改进。


## 4. 社区热点

**🔥 最热 Issue：Skills Index 过期（评论 54 条）**
- [#66616 [skills-index-watchdog] Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) — 自动探针检测到 Skills Hub 依赖的索引文件已过期 29.8 小时（阈值 26 小时）。该 Issue 自 7 月 18 日创建至今已持续一个月，54 条评论表明社区对文档/索引更新延迟的持续关注，这直接影响开发者的使用体验。

**🔍 高关注桌面端问题：**
- [#88275 Renderer process burns 40-70% CPU at idle](https://github.com/NousResearch/hermes-agent/issues/88275) — 自 8 月初起，macOS Intel 上 Hermes Desktop 的渲染进程持续占用 40-73% CPU，导致热降频。用户不得不通过 `desktop.disable_gpu=true` 部分缓解。涉及 Electron 40.10.2 的桌面构建。关联性能 PR #89578（星图渲染循环休眠）已提交。

**📌 核心架构争议：**
- [#88715 Multiplex: profile identity is late-bound across transport, session, storage, and control paths](https://github.com/NousResearch/hermes-agent/issues/88715) — 该问题指出 Hermes 在多路复用场景下，profile 身份在传输、会话、存储和控制路径上各自独立推导，缺乏统一的 canonical 身份定义点。涉及 5 个不同的 sweeper/风险标签，属于当前架构演进的关键节点，可能成为未来重构的核心议题。

**分析：** 社区诉求集中在两块：一是桌面端的实际使用体验（CPU 占用、连接切换、标签管理），二是架构层面的确定性（profile 身份、会话隔离）。两者都反映出 Hermes 在从"单机工具"走向"多通道、多身份、可编排的 Agent 平台"的成长阵痛。


## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高优（P2，有明确影响面）

| Issue | 描述 | Fix PR |
|-------|------|--------|
| [#89131 Bot Mode drops per-profile Cloud alias](https://github.com/NousResearch/hermes-agent/issues/89131) | Bot Mode 在 v2 连接注册表激活后不保留桌面端 per-profile 的 Cloud 别名，导致启动本地后端而非预期的托管 agent | 无 |
| [#89576 Desktop MCP health probe opens a second HTTP session and evicts the live one](https://github.com/NousResearch/hermes-agent/issues/89576) | MCP 健康检查每次都新开 Streamable HTTP 会话，对于官方 Slack MCP 这类单会话服务会导致当前会话失效 | **有** → [#89581 复用 live HTTP 会话](https://github.com/NousResearch/hermes-agent/pull/89581) |
| [#88715 Multiplex: profile identity is late-bound](https://github.com/NousResearch/hermes-agent/issues/88715) | 多路复用场景下 profile 身份在不同层独立推导，可能导致状态错乱 | 无（架构级问题） |
| [#89346 shared primary profile routes reload session history from the root store](https://github.com/NousResearch/hermes-agent/issues/89346) | 共享主 profile 路由到次级 profile 时，会话历史从根存储重新加载，导致分裂会话 | 无 |
| [#89415 Credential pool caches provider cooldown; mid-cooldown credit top-up is never re-probed](https://github.com/NousResearch/hermes-agent/issues/89415) | 认证池缓存了提供商冷却状态，用户在冷却期间充值后不会被重新探测 | 无 |
| [#73403 Windows ACP adapter hangs when executing terminal tool](https://github.com/NousResearch/hermes-agent/issues/73403) | Windows 上 ACP 客户端驱动的本地终端初始化和文件操作可能无限挂起 | 已在 #69083 提交修复，但尚未合并 |
| [#89111 Gateway approval prompts time out on remote Windows desktop clients](https://github.com/NousResearch/hermes-agent/issues/89111) | 远程 Windows 桌面客户端上的网关审批提示无法将用户批准回传至网关 | 无 |
| [#89579 Startup notification to home channel not sent after server reboot](https://github.com/NousResearch/hermes-agent/issues/89579) | 服务器重启后（非计划内）不发送启动通知；标注为重复 Issue | 无 |

### 🟡 中优（P3）

| Issue | 描述 | Fix PR |
|-------|------|--------|
| [#88895 gateway.error.log no rotation + slack socket-mode reconnect traceback spam](https://github.com/NousResearch/hermes-agent/issues/88895) | 日志无限增长，已观测到 141MB / 268,086 次重复 traceback | 无 |
| [#89561 `hermes config set` stores composite values (lists/mappings) as strings](https://github.com/NousResearch/hermes-agent/issues/89561) | CLI 无法从 shell 脚本化写入复合配置值 | 无 |
| [#89516 minimax-oauth provider missing `api_key_env_vars`](https://github.com/NousResearch/hermes-agent/issues/89516) | 环境变量名称错误导致错误提示信息中引用了错误的变量名 | 无 |

### 🔵 其他已关闭 Bug
- [#89546 Desktop hover close buttons on persistent navigation tabs](https://github.com/NousResearch/hermes-agent/issues/89546) → **已修复**（#89572/#89551）
- [#89568 cron display format cannot self re-parse](https://github.com/NousResearch/hermes-agent/pull/89568) → **有修复 PR**（待合并）
- [#89571 cron due-scan must not dispatch a one-shot past its grace window](https://github.com/NousResearch/hermes-agent/pull/89571) → **有修复 PR**（待合并）


## 6. 功能请求与路线图信号

| 功能请求 | Issue/PR | 被纳入下一版本的可能性 |
|----------|----------|----------------------|
| **Desktop Projects 持久化 Agent** | [#89567 feat(projects): add persistent agents for Desktop projects](https://github.com/NousResearch/hermes-agent/pull/89567) | **高** — 已有完整 PR，设计明确（复用会话 + 保留 prompt cache），符合桌面端场景需求 |
| **xAI 1080p 视频生成** | [#89549 Issue](https://github.com/NousResearch/hermes-agent/issues/89549) + [#89569 PR](https://github.com/NousResearch/hermes-agent/pull/89569) | **高** — 文档已列出但插件限制为 720p，属于能力差距，PR 已提交 |
| **Cron 内存工具** | [#18885 allow memory provider tools in cron jobs](https://github.com/NousResearch/hermes-agent/issues/18885) | **中** — 已开放 3 个月有余，与内存维护自动化场景相关，但长期未获优先级提升 |
| **路由管理** | [#89304 Desktop profile alias to target remote gateway profile](https://github.com/NousResearch/hermes-agent/issues/89304) + [#88680 preserve route identity end-to-end](https://github.com/NousResearch/hermes-agent/issues/88680) | **中** — 与 #88715 的架构方向一致，但属于更大范围的重构 |
| **状态栏连接切换** | [#88307 Always-visible connection picker in status bar](https://github.com/NousResearch/hermes-agent/issues/88307) | **中低** — 改善本地↔SSH 切换体验，但需要桌面端设计调整 |
| **Nix home-manager 模块** | [#84178 feat(nix): home-manager module](https://github.com/NousResearch/hermes-agent/pull/84178) | **中** — PR 已存在超过一周，等待维护者决策；Nix 用户社区对此有需求 |
| **Sticky quota-aware credential routing** | [#89573 feature PR](https://github.com/NousResearch/hermes-agent/pull/89573) | **中** — 针对 Codex 凭证池的配额感知路由，减少不必要的凭证切换，已提交 PR 但需评估复杂度 |
| **MCP 目录扩展** | [#89583 add Pin Seeker to MCP catalog](https://github.com/NousResearch/hermes-agent/pull/89583) | **高** — 低风险，扩充 MCP 生态覆盖面 |
| **入站消息钩子** | [#84580 supported inbound message hook with sender and message IDs](https://github.com/NousResearch/hermes-agent/issues/84580) | **中** — 已有讨论但缺少设计文档；涉及 API 设计决策 |


## 7. 用户反馈摘要

**积极反馈：**
- **MCP 会话复用修复**（[#89581](https://github.com/NousResearch/hermes-agent/pull/89581)）：用户 Sha01in 在提交修复 PR 的同时提交了对应的 Issue（#89576），说明了清晰的复现路径（Slack MCP），并主动提供了 PR 修复方案，体现了社区的高参与度。
- **桌面端项目 Agent 功能**（[#89567](https://github.com/NousResearch/hermes-agent/pull/89567)）：PR 提交者 fangliquanflq 此前还提交过 Windows ACP 挂起问题（#73403），表明同一用户活跃在多个垂直场景。该 PR 承诺在不丢失上下文的前提下持久化项目对话，且保留 prompt-cache 前缀，符合实际使用场景的需求。

**用户痛点：**
- **Windows 平台稳定性仍是短板**：多线程线索指向 Windows 上的终端初始化（[#73403](https://github.com/NousResearch/hermes-agent/issues/73403)）、_post_turn_goal_continuation 缺失（[#62202](https://github.com/NousResearch/hermes-agent/issues/62202)）和审批流程超时（[#89111](https://github.com/NousResearch/hermes-agent/issues/89111)）等问题，持续影响 Windows 用户群。
- **桌面端在 Intel Mac 上资源占用严重**：CPU 占用 40-73%（[#88275](https://github.com/NousResearch/hermes-agent/issues/88275)）是一个长期存在且用户已自行排查的高质量问题。
- **复杂配置场景学习成本高**：profile 身份在多个层独立解析（[#88715](https://github.com/NousResearch/hermes-agent/issues/88715)）、配置脚本化能力不足（[#89561](https://github.com/NousResearch/hermes-agent/issues/89561)）均是资深用户才可能遇到的深层问题。
- **Cron 作业环境变量识别问题尚未解决**：[#59030](https://github.com/NousResearch/hermes-agent/issues/59030)（no_agent cron 使用过期凭证）自 7 月 5 日起未有处理迹象，需要维护者的关注。


## 8. 待处理积压

以下为长期未响应或仅有少量维护者参与的重要 Issue/PR：

| 项目 | 创建时间 | 最后活跃 | 备注 |
|------|----------|----------|------|
| [#66616 Skills index stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) | 2026-07-18 | 2026-08-19 | 50+ 条评论说明讨论热度高，但缺乏官方响应或明确的修复计划，已持续 >1 个月 |
| [#59030 no_agent cron jobs deliver with stale os.environ credentials](https://github.com/NousResearch/hermes-agent/issues/59030) | 2026-07-05 | 2026-08-18 | 创建 45 天，缺少维护者回复，涉及定时任务环境变量安全性，值得优先关注 |
| [#18885 allow memory provider tools in cron jobs](https://github.com/NousResearch/hermes-agent/issues/18885) | 2026-05-02 | 2026-08-19 | 创建已 3.5 个月，讨论持续但缺少官方决策 |
| [#84580 inbound message hook with sender and message IDs](https://github.com/NousResearch/hermes-agent/issues/84580) | 2026-08-12 | 2026-08-18 | 涉及 API 设计决策，尚未有官方回复 |
| [#84178 feat(nix): home-manager module](https://github.com/NousResearch/hermes-agent/pull/84178) | 2026-08-12 | 2026-08-19 | PR 已存在超过一周，待维护者评审；Nix 用户社群明确表达了这一需求 |

**建议：**
1. **优先排查 #66616**：Skills Index 持续过期直接影响所有用户的使用体验（文档和函数索引不可用），且已频繁出现多次。应至少更新自动化脚本中的探针时间窗口或增加重建频率。
2. **处理 #59030**：环境变量凭证过期问题在 cron 定时任务场景中可能造成生产事故，建议将 `no_agent` 分支中的环境变量刷新逻辑提前至短路径判断之前。
3. **尽早决策 #88715 路线图**：该问题涉及 5 个不同 sweeper/风险标签，说明跨模块影响广泛。如果下一代架构规划中已包含 profile 身份的集中化设计，应向社区披露时间表，否则应至少在文档中明确当前的推荐配置方式。


*本日报由 AI 分析师自动生成，数据来源：NousResearch/hermes-agent GitHub 仓库。所有链接指向对应 Issue/PR 详情页面。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-19

## 今日速览

过去24小时内，PicoClaw 项目保持了中等偏活跃的社区节奏：6条 Issue 更新（5条活跃、1条关闭）与4条 PR 更新（2条待合并、2条已关闭），未发布新版本。值得关注的是，已存在近四个月的 **#806 WebUI 功能请求** 在近日持续收获社区互动，反映出用户对降低使用门槛的迫切需求；同时，**#3339 Antigravity 提供商 429 错误** 是过去24小时内新出现的高优先级 Bug。整体来看，项目处于功能扩充与社区反馈消化并行的阶段，维护者的响应速度基本及时，但存在几个标记为 `stale` 的 PR 和 Issue 等待更积极的处理。

---

## 项目进展

今日无新版本发布，但有两个值得关注的 PR 动态（均处于待合并状态，存在 `stale` 标签）：

### 修复与功能推进

- **[PR #3314] Fix: agent not able to execute shell command added to customAllowPatterns**
  作者：j-v | 更新：2026-08-18 | 状态：待合并
  该 PR 修复了 `customAllowPatterns` 配置不生效的 Bug——默认拒绝规则在 `guardCommand` 中始终优先，导致用户显式允许的 `git push` 等命令仍被拦截。这是对 agent 权限控制机制的关键修复，直接影响用户在自定义安全策略下的实际使用体验。

- **[PR #3329] fix(line): warn on inert webhook_host / webhook_port instead of seeding them**
  作者：ex-takashima | 更新：2026-08-18 | 状态：待合并
  针对 Issue #3328（LINE 通道的 `webhook_host` / `webhook_port` 配置声明了但从未被读取），此 PR 选择在用户设置无效配置时给出警告而非静默忽略，是提升配置可诊断性的良好实践。

### 已合并/关闭的 PR

- **[PR #1158] feat: add anthropic-messages protocol for native Anthropic API format**（已关闭，Fixes #269）
  该 PR 为 PicoClaw 增加了对 Anthropic 原生 Messages API（`/v1/messages`）的支持，解决了仅兼容 Anthropic 原生格式的服务无法使用的问题。值得注意的是，该 PR 创建于 2026-03-06，经过五个多月在今日关闭——合并前的长周期可能反映了协议兼容性测试的复杂度，但其合入显著拓宽了支持的 LLM 提供商范围。

- **[PR #3317] feat(providers): log prompt cache tokens in LLM response debug output**（已关闭）
  在 LLM 响应调试日志中增加了对 prompt 缓存 token 的记录，对 DeepSeek 等提供商的成本追踪和调试有实际意义。

**总体评估**：项目在提供商协议兼容性（Anthropic 原生格式）和可观测性（缓存 token 日志）方面获得了实质性进展，同时 Agent 权限配置修复的合入将进一步增强安全策略的可用性。

---

## 社区热点

### 最热门讨论：#806 [Feature] Add webUI support

- 创建于 2026-02-26，五个月后依然活跃，今日收到新评论
- 评论数：9 | 👍 数：8（过去24小时新增评论和点赞）
- 链接：https://github.com/sipeed/picoclaw/issues/806

该 Issue 提出为 PicoClaw 开发浏览器端的 Web UI，以降低非技术用户的使用门槛。尽管 TUI 对终端用户友好，但 Web UI 被认为是触达更广泛用户群体的最直观路径。**8 个 👍 和持续数月的讨论表明这是社区呼声最高的功能请求之一**，且已被标注为 `roadmap` 类型，加入高优先级增强队列。

### 技术细节讨论：#3287 [Feature] Better support long messages in IRC

- 创建于 2026-07-22，更新于 2026-08-18，评论数：6
- 链接：https://github.com/sipeed/picoclaw/issues/3287

IRC 协议默认限制消息长度为 512 字节，超长消息会被自动切分，PicoClaw 目前无法正确识别切分后的多段消息为同一整体。6 条评论的讨论反映了 IRC 通道使用者对此行为的影响有较高关注度。

**热点分析**：社区关注的焦点集中在**扩展用户触达面**（Web UI）和**通道协议完整性**（IRC 长消息处理）两大方向，前者代表对用户群体扩展的期待，后者代表对现有通道质量深化的需求。

---

## Bug 与稳定性

### 高优先级（新出现，需关注）

- **[#3339] Antigravity generation returns generic 429 despite valid OAuth scopes and successful model discovery**（[链接](https://github.com/sipeed/picoclaw/issues/3339)）
  创建于 2026-08-17，更新于 2026-08-18，评论：1
  严重程度：🔴 高 — Google Antigravity 提供商的身份验证和模型发现正常，但所有生成请求返回 429（资源耗尽）。由于响应中不包含配额详情，用户无法区分是配额耗尽还是错误处理逻辑问题。**这是过去24小时内新出现的 Provider 兼容性 Bug，建议优先排查。**

### 中优先级（带 `stale` 标签的遗留 Bug）

- **[#3301] /clear and session auto-compression don't work in chats routed to non-default agent via dispatch rules**（[链接](https://github.com/sipeed/picoclaw/issues/3301)）
  创建于 2026-07-29，已被标记 `stale`
  涉及 Raspberry Pi 环境下 Discord/Telegram 通道中 dispatch 路由到非默认 Agent 时的会话清理与自动压缩失效问题。功能型缺陷，建议在后续迭代处理。

- **[#3328] line.settings.webhook_host / webhook_port are never read**（[链接](https://github.com/sipeed/picoclaw/issues/3328)）
  创建于 2026-08-11，已有对应修复 PR [#3329](https://github.com/sipeed/picoclaw/pull/3329) 待合并。配置项无效但无任何警告提示属于设计层面的遗漏，修复合入后问题将得到闭环。

### 已关闭

- **[#3292] CPU usage too high when focus on input box in chat interface**（[链接](https://github.com/sipeed/picoclaw/issues/3292)）
  已关闭，无明显后续活动。此问题可能已通过其他方式解决或认定为环境相关问题。

---

## 功能请求与路线图信号

- **Web UI 支持（#806）**：属 `roadmap` 类型，8 个 👍 表明社区需求强烈。虽然目前无对应 PR，但持续的评论互动和 `Refactoring now` 标签暗示**这可能是项目重构期的核心方向之一**。预计有望在未来大版本中看到相关进展。

- **IRC 长消息支持（#3287）**：功能改进请求，6 条评论表明对 IRC 通道消息处理的关注有一定浓度，目前无关联 PR。

- **Prompt cache tokens 日志输出（PR #3317）**：已合并，对成本敏感的用户是实用的改进。此类可观测性提升类的需求在社区中反馈良好，未来可能围绕 token 使用优化有更多功能扩展。

---

## 用户反馈摘要

- **配置可发现性问题**：Issue #3328 暴露了配置项存在但无效且无警告的体验问题。用户 qing-wang 专门提交了带完整代码引用的证据链报告，反映了社区对配置可靠性的重视。

- **权限控制的实际痛点**：PR #3314 的提出者 j-v 在 Issue #3301 中报告 dispatch 路由相关问题，同时又在 PR #3314 中修复 `customAllowPatterns` 不生效问题，表明 **Agent 权限控制和多 Agent 路由是当前用户配置复杂场景的核心摩擦点**。

- **非技术用户门槛**：Issue #806 的持续热度表明，虽然 TUI 对开发者友好，但社区中已形成对 Web UI 的明确期望，希望 PicoClaw 能覆盖更广泛的用户群体。

- **Provider 兼容性的实际体验**：#3339 中用户验证了 OAuth 范围和模型发现均正常，却在生成阶段遇到 429，这种非预期行为可能影响用户对 Antigravity 支持质量的评价。IRC 长消息问题（#3287）则关注跨消息边界的语义完整性。

---

## 待处理积压

以下事项长期未获得充分响应或进展缓慢，建议维护者关注：

- **[#806] WebUI 支持**（[链接](https://github.com/sipeed/picoclaw/issues/806)）— 5个月+，8个 👍，已经属于 `roadmap`，但需要更明确的进度透明度和节点规划，建议发布一个 roadmap 说明。

- **[#3287] IRC 长消息支持**（[链接](https://github.com/sipeed/picoclaw/issues/3287)）— 近1个月，6 条评论，无维护者回应记录。IRC 仍是重要通道，建议至少给出方案确认的回复。

- **[PR #3314] customAllowPatterns 修复**（[链接](https://github.com/sipeed/picoclaw/pull/3314)）— 自 2026-08-03 起已 16 天未合并，且被打上 `stale` 标签。该 PR 直接影响 Agent 安全策略的可用性，建议尽快 review 和合并。

- **[PR #3329] line webhook 配置警告修复**（[链接](https://github.com/sipeed/picoclaw/pull/3329)）— 关联 #3328 的修复性 PR，提交于 08-11，如今已 8 天，同为 `stale` 状态。此类「小但有用」的修复建议定期批量处理防止积压。

---

**总结**：PicoClaw 项目今日整体健康度良好，社区活跃度中等偏上。项目在 Provider 协议扩展（Anthropic 原生格式）和可观测性（缓存 token 日志）方面收获实质进展；Web UI 是社区呼声最高的演进方向，而 Agent 权限配置和 Provider 兼容性是当前用户反馈中集中出现的技术摩擦点。建议维护者优先解决 #3339 这一新出现的高优先级 Bug，并尽快处理两个 `stale` 状态的修复型 PR（#3314、#3329），避免功能修复长期搁浅。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期**: 2026-08-19  
**数据窗口**: 2026-08-18 ~ 2026-08-19 (UTC)

---

## 1. 今日速览

NanoClaw 项目今日活跃度**极高**，过去24小时产生了 39 条 PR 更新与 3 条 Issue 活动，属于近期少有的高强度协作日。项目维护团队（core-team）持续推进基础设施层重构，围绕 **Session 运行时驱动抽象（#3306/#3307）** 与 **集中式数据库异步化改造（#3321-#3337 系列）** 两条主线展开了大规模 PR 操作，且已有多条 PR 完成合并闭环。与此同时，社区侧通过 Webex 适配器（#3343）与 You.com 工具集成（#3322）贡献了新的功能扩展。值得关注的是，核心团队 PR 的密集程度显著高于社区 PR，项目正处于**主动架构演进期**，而非单纯的修修补补阶段。

---

## 2. 版本发布

**无新版本发布。**

过去24小时内无 Releases 更新，项目仍处于当前版本的持续迭代周期中。但请注意，以下已合并 PR 包含 **BREAKING 变更**，预计将在下一正式版本发布时产生迁移影响：

- **PR #3325** `[BREAKING] refactor(db): adopt async central database seam` (已合并)
- **PR #3334** `[BREAKING] refactor(db): adopt async central database safely` (待合并)

涉及迁移的 Issue 已在 #2868 中有过提示，建议维护者在下一个 Release 中明确记录迁移路径。

---

## 3. 项目进展

今日关闭/合并了 **16 条 PR**，核心推进方向集中在以下三块：

### 3.1 集中式数据库异步化改造（核心工作）

由 `moshe-nanoco` 主导，通过一组按序提交的 PR 完成了集中式数据库从同步到异步的完整过渡：

| PR | 标题 | 状态 | 作用 |
|---|---|---|---|
| [#3321](https://github.com/nanocoai/nanoclaw) | refactor(db): centralize the central database path | ✅ 已合并 | 收敛数据库路径管理 |
| [#3323](https://github.com/nanocoai/nanoclaw) | refactor(db): make central SQL portable | ✅ 已合并 | 消除 SQL 方言硬编码 |
| [#3324](https://github.com/nanocoai/nanoclaw) | refactor(db): add async central database seam | ✅ 已合并 | 引入异步接口层 |
| [#3325](https://github.com/nanocoai/nanoclaw) | **[BREAKING]** refactor(db): adopt async central database seam | ✅ 已合并 | 全面切换至异步 API |
| [#3326](https://github.com/nanocoai/nanoclaw) | fix(db): close async concurrency races | ✅ 已合并 | 修复异步并发竞态 |
| [#3330](https://github.com/nanocoai/nanoclaw) | test(db): run central suites through the driver | ✅ 已合并 | 测试迁移至驱动层 |

该系列剩余 PR（#3332-#3337）虽尚未合并，但基础路径已打通，项目数据库层具备**后端可插拔**能力，为未来的远程数据库后端（如 PostgreSQL、MySQL）铺平道路。

### 3.2 Session 运行时驱动抽象

由 `gavrielc` 提交的 [#3306](https://github.com/nanocoai/nanoclaw)（新增 `src/drivers/` 目录，以 Docker 为内置实现的 Session 运行时驱动层）与 [#3307](https://github.com/nanocoai/nanoclaw)（将 host 的完整会话生命周期——spawn、adoption、supervision、stop、restart/rebuild——路由至驱动层）为后续支持非 Docker 运行时（如本地进程、远程容器、WASM 等）奠定了基础。**纯增量**设计保证了兼容性（全量 1672 测试通过），是今日最核心的架构级 PR。

### 3.3 安全性加固（多项）

- [#3339](https://github.com/nanocoai/nanoclaw) — 存储的登录凭据无法验证时**默认拒绝**而非放行
- [#3340](https://github.com/nanocoai/nanoclaw) — `pending_approvals` 增加实例标识，确保同一 bot 身份处理完整流程
- [#3341](https://github.com/nanocoai/nanoclaw) — Slack 服务从凭据签发方推导，修复多实例部署下的凭据错配风险

总体而言，项目今日完成了数据库层的一次**系统性升级**，并初步确立了运行时驱动架构，前进幅度显著。

---

## 4. 社区热点

今日社区讨论热度相对集中在 Issue 区，评论/反应量普遍偏低（大部分 PR 无评论），但以下条目值得关注：

| 条目 | 类型 | 热度信号 | 核心诉求 |
|---|---|---|---|
| [#3338](https://github.com/nanocoai/nanoclaw) Codex WebSocket 静默超时 | 🔥 Issue (OPEN) | 2条评论 | 用户 `ionescu77` 发现 **Codex CLI 的5分钟 WebSocket 空闲超时内部重试机制对 NanoClaw 不可见**，导致一条 Telegram 请求最长可静默10分钟。核心诉求：将底层超时/重试事件向上透出，至少让 NanoClaw 知道"底层在重试"而非"卡死了" |
| [#2868](https://github.com/nanocoai/nanoclaw) `/update-skills` 静默无效 | Issue (已关闭) | 1条评论 | 报告 `/update-skills` 对已安装的 channel 不刷新适配器代码与依赖，与 CHANGELOG 引导相悖。今日关闭说明该问题已有结论 |
| [#3194](https://github.com/nanocoai/nanoclaw) `/update-nanoclaw` 假成功 | Issue (已关闭) | 无评论 | 更新流程在验证通过前即切换运行目录，存在四个可导致不可恢复失败的窗口。今日关闭，需关注修复方案 |

**社区心态观察**：`#3338` 是当前最活跃的未解决问题。用户并非报告 WebSocket 本身的问题，而是**对透明度的诉求**——"底层在做什么应该让我知道"。这反映了用户对故障诊断能力的期待在上升。

---

## 5. Bug 与稳定性

按严重程度排列：

### 高严重度

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#3338](https://github.com/nanocoai/nanoclaw) | Codex WebSocket 空闲超时导致 Telegram 请求最长静默 **10 分钟**，且无任何提示。影响所有依赖 Codex Responses API 的用户 | ⚠️ 无 fix PR |
| [#3194](https://github.com/nanocoai/nanoclaw) | `/update-nanoclaw` 在验证通过前切换运行目录，包含四个失败窗口（SQLite 数据库、gitignored 配置、外部组件变更无法回滚） | ✅ 已关闭（需确认修复方案） |

### 中严重度

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#2868](https://github.com/nanocoai/nanoclaw) | `/update-skills` 对已安装的 channel 不刷新代码/依赖，静默跳过 | ✅ 已关闭 |
| [#3341](https://github.com/nanocoai/nanoclaw) | Slack 安装 token 由账户服务签发、在托管 Slack 服务消费，但代码中两者无关联，多实例部署时存在凭据错配风险 | 🔧 Fix PR 待合并 |
| [#3339](https://github.com/nanocoai/nanoclaw) | 存储的登录凭据无法验证时被当作"已通过"，存在安全隐患 | 🔧 Fix PR 待合并 |

### 低严重度

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#3326](https://github.com/nanocoai/nanoclaw) | 异步数据库并发竞态 | ✅ 已修复并合并 |

---

## 6. 功能请求与路线图信号

| 信号 | 来源 | 分析 |
|---|---|---|
| **Webex REST Polling 适配器** | PR [#3343](https://github.com/nanocoai/nanoclaw) `feat(channels): add webex-poll REST polling adapter` | 社区用户 `sfakam` 提交了企业级通信平台 Cisco Webex 的轮询式适配器（无需入站 webhook），面向防火墙受限的企业环境。若被合并，将扩展 NanoClaw 在**企业 IM 矩阵**中的覆盖 |
| **You.com MCP 工具集成** | PR [#3322](https://github.com/nanocoai/nanoclaw) `skills: add /add-youdotcom-tool` | 新增独立工具技能，接入 You.com 的 MCP 服务。反映出社区对于 **MCP（Model Context Protocol）生态**的兴趣持续升温 |
| **数据库后端可插拔** | PR 系列 #3321-#3337 | 虽然属于基础设施而非用户直接可见的功能，但异步化 + 驱动抽象完成后，**远程数据库后端将成为可选项**，对多机部署与高可用场景意义重大 |
| **非 Docker 会话运行时** | PR [#3306](https://github.com/nanocoai/nanoclaw) | 驱动层的引入意味着未来可能出现本地进程、Kubernetes Pod 或远程主机的 Session 运行方式，但目前尚处于框架搭建阶段 |

**判断**：Webex 与 You.com 相关 PR 若符合项目 skill 规范（均标注 `follows-guidelines`），进入下一版本的可能性较高。

---

## 7. 用户反馈摘要

| 来源 | 用户反馈 | 深度解读 |
|---|---|---|
| [#3338](https://github.com/nanocoai/nanoclaw) 评论 | 用户 `ionescu77` 明确指出了一个**可复现的静默窗口**：Codex CLI 内部重试机制正常运作，但 NanoClaw 对此无感知，导致用户看到的现象是"发了一条消息，10分钟无响应" | 暴露了**抽象层之间可观测性的断层**。用户已掌握底层机制（Codex CLI 的5分钟超时策略），这说明该用户技术素养较高，对项目期望也更高——"底层在重试"和"系统卡死"需要有区分度的反馈 |
| [#2868](https://github.com/nanocoai/nanoclaw) 评论 | 用户 `glifocat` 指出 `/update-skills` 的静默跳过行为**与 CHANGELOG 指引矛盾**——更新日志让用户"重新运行 `/add-<channel>`"来获取新代码，但实际 `update` 命令不会执行刷新 | 用户对**文档与行为的一致性**有着明确期待。文档引导用户走了一条实际走不通的路，这类问题会消耗用户信任 |
| [#3194](https://github.com/nanocoai/nanoclaw) 描述 | 用户 `glifocat`（同一报告者）将更新失败窗口拆解为四个具体场景：Git 之外、SQLite 之外、配置之外、外部组件——逐一列出了**回滚策略的盲区** | 显示用户已经对项目的更新机制做过**深入代码级分析**，而不是表面的 bug 报告。这类用户是项目的宝贵资产 |

**共性**：用户对透明度和可恢复性要求较高，倾向于给出**分析性反馈**而非简单报错。

---

## 8. 待处理积压

### 高优先级

| 条目 | 创建时间 | 已等待 | 说明 |
|---|---|---|---|
| [#3338](https://github.com/nanocoai/nanoclaw) Codex WebSocket 超时不可见 | 2026-08-18 | 1 天 | 新开 Issue，但涉及核心 UX 问题（静默超时），尚无 PR。建议核心团队尽快确认，考虑将 Codex CLI 的重试事件通过事件总线透出 |

### 中优先级

| 条目 | 创建时间 | 已等待 | 说明 |
|---|---|---|---|
| [#3306](https://github.com/nanocoai/nanoclaw) Session 驱动层 | 2026-08-17 | 2 天 | 核心 PR，虽已有配套 #3307/#3308 待合并，但 **#3308 依赖 #3306**，需尽快推进合并以避免分支分叉扩大 |
| [#3307](https://github.com/nanocoai/nanoclaw) 会话生命周期接入 | 2026-08-17 | 2 天 | 依赖 #3306 |

### 低优先级

| 条目 | 创建时间 | 已等待 | 说明 |
|---|---|---|---|
| [#3342](https://github.com/nanocoai/nanoclaw) Slack 频道邀请处理策略变更 | 2026-08-18 | 1 天 | 行为变更（拒绝而非通知），建议在 CHANGELOG 中明确标注，避免用户困惑 |
| 数据库迁移系列 (#3332/#3333/#3335/#3337) | 2026-08-18 | 1 天 | 与已合并的 #3321-#3326 同系列，应尽快完成合并以收敛分支 |

---

## 附加观察：项目健康度评估

| 维度 | 评分 (5分制) | 说明 |
|---|---|---|
| **代码活跃度** | ✅ 5/5 | 39 条 PR 更新 / 日属于非常活跃的水平 |
| **社区参与度** | ⚠️ 3/5 | 社区 PR 仅 2 条（#3343, #3322），其余全部为核心团队提交；Issue 侧讨论量偏少 |
| **工程质量** | ✅ 4.5/5 | 大规模重构保持了"全量测试通过"（1672 测试），且 PR 内容结构清晰、描述深入 |
| **基础设施进展** | ✅ 5/5 | 数据库异步化 + 驱动抽象两大架构级改造持续推进 |
| **文档同步** | ⚠️ 2.5/5 | 存在文档与行为不一致的问题（#2868 已关闭但影响仍在），BREAKING 变更的迁移说明尚未见更新 |

**风险提示**：核心团队在 24 小时内提交了超过 10 条数据库相关 PR，说明该模块正在经历**密集重构期**。提醒用户关注此区域的回归风险，建议维护团队在重构完成后尽快发布一个中间版本以便早期验证。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-08-19

## 1. 今日速览

IronClaw 项目昨日继续保持高强度迭代节奏：24 小时内共产生 22 条 Issue 更新和 39 条 PR 更新，并发布了 `v1.3.0-rc.2` 候选版本。项目正处于 **v1.3.0 收尾与 v1.4.0 规划并行**的关键阶段——一方面`1.3.0-rc.1`升级崩溃问题被快速定位并在 rc.2 中修复，另一方面大量围绕 v1.4.0 的 Epic 设计讨论（设计系统治理、沙箱化、Mnesis 记忆提供者集成等）正在密集开展。社区活跃度高，核心贡献者（henrypark133、serrrfirat、sergeiest 等）持续推进着大型重构与新增功能，项目整体健康度良好，但 v1.3.0 正式发布的稳定性验证仍是当前焦点。


## 2. 版本发布

### ironclaw-v1.3.0-rc.2（2026-08-18）

**修复内容：**

- **升级崩溃修复**：从 1.2.x 升级时，rc.1 中存在的"未知字段 `activation_state`"导致的启动崩溃循环（Issue #7720）已修复。rc.2 现在能正确接受并保留已发布扩展的 `activation_state` 字段。
- **Reborn 运行时 SSH 支持**：规范 Reborn 运行时镜像再次支持可选的、仅公钥 worker SSH（端口 2222）。

**迁移注意事项：** 从 1.2.x 升级的用户应直接使用 rc.2 而非 rc.1，以避免启动崩溃。已有 rc.1 部署需手动更新。


## 3. 项目进展

### 已合并/关闭的 PR 亮点

| PR | 内容 | 影响 |
|---|---|---|
| [#7734](https://github.com/nearai/ironclaw/pull/7734) | 完成两个停滞的半成品测试模块提取（`executor/tests.rs` 12,790 行、`capability_port.rs` 11,302 行），共迁移 **317 个测试，0 行生产代码** | 大幅提升代码可维护性 |
| [#7713](https://github.com/nearai/ironclaw/pull/7713) | 测试 PR：在 `qa-automation-preview` 上端到端执行 `/benchmark` 路径，首次运行 enterprise 类型套件 | 验证基准测试基础设施 |

### 重要进展中的 PR

- **[#7491](https://github.com/nearai/ironclaw/pull/7491)** — omp 核心工具契约：模型可见的编码工具面收敛为 6 个精确名称（`read`/`write`/`edit`/`glob`/`grep`/`bash`），移除旧文件工具与派生 `builtin__*` 拼写。这是 Issue #7392 的切片 1-4，涉及面广、已开放一周，值得关注。
- **[#7650](https://github.com/nearai/ironclaw/pull/7650)** — 自动化运行结果从"答案语义评判"转向"基于运行时证据的确定性评估"，直接对焦 Issue #6879（自动化运行不稳定）。
- **[#7735](https://github.com/nearai/ironclaw/pull/7735)** — 为可下载对话产物添加运行计时证据（每次推理耗时、每工具耗时、调用次数），让 bug 报告携带定量数据。

**整体判断：** 项目正持续推进"能力响应规范化"（#7627 系列）、自动化可靠性提升、以及 WebUI 设计系统三大主线，结构性重构较多，但均有低风险标签。


## 4. 社区热点

### 最受关注 Issue

**[#7185](https://github.com/nearai/ironclaw/issues/7185) — Memory not reliably recalled across conversations**（已关闭，2 条评论）

> 多人在 7/23 周会上独立观察到：一个对话中建立的信息无法在后续对话中可靠召回。来自不同角色（Devon/法务等）的反馈均指向该问题。

**分析：** 这是影响真实用户的关键痛点，直接关联"长期记忆"这一核心价值。该 Issue 虽已关闭，但解决质量值得维护团队在日后的用户反馈中持续验证。

### 最活跃 PR

**[#7491](https://github.com/nearai/ironclaw/pull/7491) — omp 核心工具契约（Issue #7392，切片 1-4）**

> 模型现在获得一个统一的编码工具面（6 个精确名称），消除新旧工具面并存带来的歧义。

**分析：** 这是"用第三方契约替换第一方编码工具"的实验性举措，背后诉求是**减少模型对工具名称的混淆**，提升工具调用的确定性。切分为 4 个切片说明这是一个周期较长的结构性变更，涉及面大，受到核心贡献者重点关注。


## 5. Bug 与稳定性

### 高严重度

**[#7720](https://github.com/nearai/ironclaw/issues/7720) — `1.3.0-rc.1` 升级后启动崩溃循环**（已修复 ✅）

> 从 1.2.x 升级后，`1.3.0-rc.1` 在组合阶段退出码 1，崩溃循环直到重启策略放弃，worker HTTP/SSH 端口全部失效。原因：v2 扩展安装行中的未知字段 `activation_state`。

**状态：** 已在 `1.3.0-rc.2` 中修复。高严重度但已闭环。

**[#7714](https://github.com/nearai/ironclaw/issues/7714) — libSQL 单一共享写连接饿死资源治理日志（已关闭）**

> PinchBench 147 任务压测中，delta journal 反复 ~40s 等待写连接，随后级联触发 `authority invalidated → journal replacement → durable-state reload` 循环，约每 40s 一次，失败预留释放、永久预留泄漏。

**状态：** 已关闭，但"永久预留泄漏"的影响面需要回归验证。

### 中低严重度

| Issue | 问题 | 状态 |
|---|---|---|
| [#7726](https://github.com/nearai/ironclaw/issues/7726) | `IRONHUB_MANIFEST_URL` 名义上可配置，实际被编译期白名单硬编码限制，自托管 catalog 无法使用 | 无 fix PR |
| [#7727](https://github.com/nearai/ironclaw/issues/7727) | Catalog `capabilities` 工件被标记为必填但从未被读取——下载/摘要校验/写入安装包后即丢弃 | 无 fix PR |
| [#7185](https://github.com/nearai/ironclaw/issues/7185) | 跨对话记忆召回不可靠（社区长时间反馈） | 已关闭，但需持续验证 |


## 6. 功能请求与路线图信号

### v1.4.0 方向（来自 Epic Issue）

| 方向 | Issue | 说明 |
|---|---|---|
| **记忆提供者集成** | [#7731](https://github.com/nearai/ironclaw/issues/7731) — Mnesis Spike | 集成 Mnesis 作为记忆提供者 |
| **沙箱化** | [#7732](https://github.com/nearai/ironclaw/issues/7732) — Sandboxing Solution with CLIs | E2E 沙箱化 |
| **设计系统治理** | [#7733](https://github.com/nearai/ironclaw/issues/7733) — DESIGN.md 治理与主题改造 | 设计原则、令牌分类、可访问性标准等 |
| **可恢复状态与配置解耦** | [#7467](https://github.com/nearai/ironclaw/issues/7467) — Reborn 持久状态与 profile 解耦 | profile 切换导致数据"消失"问题 |
| **用量统计日志** | [#6837](https://github.com/nearai/ironclaw/issues/6837) — growth/usage 最小化 info 日志 | 当前 52 个 `info!` 调用全部为基础设施/管道，零业务指标 |

### 值得关注的新增功能 PR

- **[#7724](https://github.com/nearai/ironclaw/pull/7724) — WebUI 语音输入（NEAR AI Whisper）**：麦克风录入 → 宿主端转写 → 光标处插入，不自动发送；浏览器不持有推理凭据。低风险、体验提升明显，可能被社区广泛使用。
- **[#7728](https://github.com/nearai/ironclaw/pull/7728) — Google Docs 语义编辑工具**：新增 4 个语义能力（结构化检查、锚定批量编辑、表格填充、确定性验证），保留 11 个遗产工具。


## 7. 用户反馈摘要

**正面反馈：**

- 无明确正面反馈记录在今日数据中，但多数 PR 为行为保持的重构（"**0 production lines**"），说明核心维护者对回归风险控制严格。

**痛点与诉求：**

1. **跨对话记忆不可靠**（#7185，已关闭）：多名测试者独立确认，对 AI 助手的核心价值影响直接。
2. **Slack 私信连接体验**（[#7681](https://github.com/nearai/ironclaw/issues/7681)）：未关联用户在共享频道 @机器人时，连接提示对全频道可见，且需手动多步骤操作（"what's the link to connect you?"）。对应 PR [#7682](https://github.com/nearai/ironclaw/pull/7682) 已提交，改为私密通知 + 一键连接。
3. **自动化运行不稳定**（#6879）：同一存储提示词有时成功有时产生无用输出，小模型（DeepSeek V4 Flash）上尤其明显。审计确认是结构性问题而非模型噪声——**触发器触发被当作普通交互式聊天轮执行**。
4. **任务调用过多工具后无法完成**（#7447）：agent 陷入冗余 fetch-retry 循环（4 轮近重复的 GitHub 查询），烧光工具调用/轮次预算。


## 8. 待处理积压

### 长期未响应的 Issue

| Issue | 创建时间 | 天数 | 最后更新 | 备注 |
|---|---|---|---|---|
| [#3676](https://github.com/nearai/ironclaw/pull/3676) — 安全文档重构（PR） | 2026-05-15 | 96 天 | 2026-08-18 | 5 月基于 v1 单体编写，已从当前 main 重建，但仍未合并，需关注 |

### 需要关注的长期开放 Issue

| Issue | 创建时间 | 天数 | 说明 |
|---|---|---|---|
| [#6837](https://github.com/nearai/ironclaw/issues/6837) — 用量统计 info 日志 | 2026-07-29 | 21 天 | 无 `info!` 级别业务指标 |
| [#7038](https://github.com/nearai/ironclaw/issues/7038) — Storybook + 设计系统 | 2026-08-03 | 16 天 | 有完整提案包（PR #7257），等待核心团队审查 |
| [#6994](https://github.com/nearai/ironclaw/pull/6994) — OOBE 自动化任务原型 | 2026-08-01 | 18 天 | 已在 flag 后实现，待合并 |

### 持续未合入的重要 PR

- **[#7491](https://github.com/nearai/ironclaw/pull/7491)**（omp 核心工具契约）— 已开放 8 天，切片 1-4 规模大，涉及模型可见行为变更，建议尽快推进审查。
- **[#7686](https://github.com/nearai/ironclaw/pull/7686)** 与 **[#7711](https://github.com/nearai/ironclaw/pull/7711)** — 能力响应规范化栈（#7627 计划）的第 1/最终 PR，环环相扣，若延误会阻塞后续工作。


> **分析师注：** 项目处于 v1.3.0 发布候选阶段，rc.2 的升级崩溃修复是积极信号；v1.4.0 方向明确（记忆、沙箱、设计系统），但多个大型 Epic 并行可能分散核心维护者注意力。建议优先合并 [#7491](https://github.com/nearai/ironclaw/pull/7491) 以收敛模型可见工具面，并在 rc.2 验证通过后尽快推进正式版发布。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报

**日期：** 2026-08-19  
**数据窗口：** 2026-08-18 至 2026-08-19（UTC）

---

## 1. 今日速览

过去 24 小时，LobsterAI 项目保持高度活跃，共产生 9 条 Issue 更新和 20 条 PR 更新，并发布了 2026.8.18 版本。新版本通过 PR #2510 合并了 23 个提交、涉及 57 个文件的变更（`+7,004/-39`），核心亮点是引入了可选的实验性 DeepSeek Harness (dsh) 引擎集成，并改进了模型加载与定时任务历史功能。值得关注的是，今日合并/关闭的 17 条 PR 中包含多个自 4 月以来长期搁置的 `stale` PR（如 #1583、#1597、#1615 等），表明项目维护者正在集中清理历史积压，对社区贡献进行大规模收编与合并，项目健康度显著回升。当前仍有 3 条 PR 等待合并，9 条 Issue 处于开放状态，其中多数为历史遗留问题，需持续关注。


## 2. 版本发布

### LobsterAI 2026.8.18（2026-08-18 发布）

**主要更新内容：**
- **dsh 引擎集成**: 引入可选的实验性 DeepSeek Harness 集成（PR #2502），并更新 dsh 至 rc.7（PR #2509）
- **dsh 进程启动器**: 新增 dsh 进程管理能力（PR #2502 后续提交）
- **模型加载改进**: 修复服务器模型加载遇到瞬时故障后的重试机制（PR #2508）
- **定时任务历史修复**: 限制 cron 运行历史页面大小，修复网关最大限制问题（PR #2507）
- **Sidebar 搜索优化**: 将任务搜索移至头部操作区，统一多平台 UI 风格（PR #2481）
- **Artifact 自动预览开关**: 新增设置项，允许用户禁用自动预览（PR #2425）
- **多 Agent 任务过滤器**: 新增任务活动过滤器，便于跨 Agent 查找待处理任务（PR #2418）

**破坏性变更与迁移注意：**
- 本次发布增加了 `cron.runs` 历史分页逻辑，对依赖一次性拉取全部运行记录的第三方脚本可能产生行为变化
- dsh 引擎为实验性功能，默认关闭，需在设置中手动启用
- 未发现涉及数据迁移或配置格式不兼容的破坏性变更


## 3. 项目进展

今日合并/关闭的 17 条 PR 涵盖多个方面，标志着项目在功能完善和技术债务清理上均取得明显进展：

### 核心功能合并

| PR | 内容 | 影响 |
|---|---|---|
| [#2510](https://github.com/netease-youdao/LobsterAI/pull/2510) | **Release: 2026.8.17 合入 main**（23 commits, +7,004/-39） | 将 dsh 引擎集成、模型加载改进、定时任务历史修复等批量合入主分支，是版本发布前的关键里程碑 |
| [#2508](https://github.com/netease-youdao/LobsterAI/pull/2508) | **修复模型加载失败后长期空白的问题** | 增加退避重试机制，避免网络瞬断导致整个会话期间模型列表为空，显著提升体验稳定性 |
| [#2507](https://github.com/netease-youdao/LobsterAI/pull/2507) | **限制 cron 运行历史页大小** | 解决大历史请求可能超 OpenClaw 网关限制的问题，内部自动分页，保证功能可用性 |
| [#2481](https://github.com/netease-youdao/LobsterAI/pull/2481) | **Sidebar 任务搜索移至头部** | 统一 macOS/Windows 的视觉与交互体验，新增诊断与回归测试覆盖 |

### 历史积压清理（stale PR 合并）

| PR | 提出时间 | 内容 |
|---|---|---|
| [#1597](https://github.com/netease-youdao/LobsterAI/pull/1597) | 2026-04-09 | 启用 SQLite 外键约束，修复 `cowork_messages` 和 `user_memory_sources` 级联删除失效的数据残留问题 |
| [#1615](https://github.com/netease-youdao/LobsterAI/pull/1615) | 2026-04-10 | 改进会话导出功能：支持中文角色标题、增加元信息（Agent 名/更新时间/消息数）、消息时间戳、修复 tool_result 截断、支持 ESC 关闭、新增复制到剪贴板 |
| [#1621](https://github.com/netease-youdao/LobsterAI/pull/1621) | 2026-04-10 | 定时任务完成后推送 OS 原生系统通知（macOS/Windows/Linux），修复 `pollOnce()` 首次执行不触发回调的 bug，Closes #1620 |
| [#1626](https://github.com/netease-youdao/LobsterAI/pull/1626) | 2026-04-10 | **P0 Blocker 修复**：移除 OpenClaw 新版已废弃的 `skipMissedJobs` 配置字段（两处），解决网关启动失败和弹框闪烁问题 |
| [#1629](https://github.com/netease-youdao/LobsterAI/pull/1629) | 2026-04-11 | 新增用户头像设置功能（预置头像选择 + 本地图片上传），含 6 款 SVG 预置头像 |
| [#1631](https://github.com/netease-youdao/LobsterAI/pull/1631) | 2026-04-11 | MCP 模块新增"快速添加模板"：提供 File System、SQLite、Brave Search 三款模板快捷按钮 |
| [#1583](https://github.com/netease-youdao/LobsterAI/pull/1583) | 2026-04-08 | 技能管理新增「最近使用」Tab 与使用次数统计，修复 auto-routing 场景漏统计的检测逻辑缺陷 |
| [#1626](https://github.com/netease-youdao/LobsterAI/pull/1626) | 2026-04-10 | 网关非法配置修复（如上） |

### 积压功能落地（4 个月后终入主线）

特别是 #1621（定时任务系统通知）和 #1615（会话导出增强）等 PR，从 4 月提出至今历经约 4 个月终被合并，说明了社区提交的长期价值在本次清理中得到体现。


## 4. 社区热点

今日最活跃的议题集中在以下几条（均已标记 `stale`，但评论仍有更新）：

### 1. [#1628 - 优化模型选择器 UI 及统一会话工具栏样式](https://github.com/netease-youdao/LobsterAI/pull/1628)
- **状态**: OPEN（待合并）
- **热度**: 3 条待合并 PR 中最受关注，关注度高
- **内容**: 重构模型选择器组件，新增供应商图标展示（套餐模型 CubeIcon、自定义品牌图标）、图像模型语言标签、超长名称截断与悬停完整显示；下拉面板改用 `ReactDOM.createPortal` + 自适应宽度（min 180px / max 280px）；修复多页面下拉面板被裁剪问题
- **分析**: 该 PR 讨论持续活跃，主要围绕模型选择器的视觉呈现与交互细节优化，社区对 UI/UX 精致度有持续追求，且该 PR 已标记待合并，预计近期将进入主线

### 2. [#1634 - 全局搜索修复与搜索体验升级](https://github.com/netease-youdao/LobsterAI/pull/1634)
- **状态**: OPEN（待合并）
- **内容**: 修复搜索范围被当前 Agent 隐式限制的 Bug（后端按 agentId 查询 + 前端 filter 双重过滤）；修复 Redux 中 sessions 内容因 `loadSessions` 调用时机不同而不稳定的问题；搜索结果直接从 `listSessions()` 拉取全量数据；同时升级搜索面板 UX
- **分析**: 该 PR 聚焦"全局搜索实际只能搜到当前 Agent"的隐性缺陷，用户预期与实际行为矛盾的反馈可能自 4 月起就已存在（最早提交 2026-04-11），属于刚需级修复

### 3. [#1614 - 建议增加 hermes-agent 作为可选 AI 引擎](https://github.com/netease-youdao/LobsterAI/issues/1614)
- **状态**: OPEN，评论 2 条
- **热度**: 今日仍有更新，社区对多引擎支持存在持续兴趣
- **内容**: 用户建议将 hermes-agent 作为可选 AI agent 引擎，类似 openclaw
- **分析**: 结合 dsh 引擎集成（已进入 2026.8.18 版本），说明社区对多引擎/多后端支持的诉求强烈且持续。dsh 集成可能部分满足此类需求方向

### 4. [#1620 - 定时任务完成后推送系统通知](https://github.com/netease-youdao/LobsterAI/issues/1620)
- **状态**: OPEN，但有对应 PR #1621 已合并关闭（CLOSED）
- **分析**: Issue 提出的需求在今日已被合并的 PR #1621 实现并关闭，属于需求到实现的高效闭环


## 5. Bug 与稳定性

今日无新开 Bug Issue（9 条均为更新），但有 2 条长期遗留 Bug 待处理（均带有 `stale` 标记）：

### 高优先级

#### 1. [#1587 - 更新最新版本首次启动崩溃](https://github.com/netease-youdao/LobsterAI/issues/1587)
- **报告时间**: 2026-04-09
- **状态**: OPEN，评论 1 条，今日有更新
- **影响**: 用户更新版本后首次启动即闪退，属 P0 级阻断问题
- **当前**: 仍无对应修复 PR 提交

#### 2. [#1589 - 会话功能、定时任务功能均无法正常进行](https://github.com/netease-youdao/LobsterAI/issues/1589)
- **报告时间**: 2026-04-09
- **状态**: OPEN，评论 1 条，今日有更新
- **环境**: macOS Intel，版本 2026.04.08
- **影响**: 两个核心功能（会话 + 定时任务）同时异常
- **当前**: 无对应修复 PR

### 中优先级

#### 3. [#1622 - 无法添加自定义模型](https://github.com/netease-youdao/LobsterAI/issues/1622)
- **报告时间**: 2026-04-10
- **状态**: OPEN，评论 2 条

#### 4. [#1627 - 稍复杂任务客户端崩溃](https://github.com/netease-youdao/LobsterAI/issues/1627)
- **报告时间**: 2026-04-10
- **状态**: OPEN，评论 2 条
- **附有日志**: 显示 WebSocket 连接和会话列表请求相关

#### 5. [#1617 - 技能删除后列表未同步更新（已删除技能残留）](https://github.com/netease-youdao/LobsterAI/issues/1617)
- **报告时间**: 2026-04-10
- **状态**: OPEN，评论 1 条
- **内容**: 删除技能后前端 UI 状态未刷新，重启仍残留，提示"Skill not found"。
- **关联**: 该 Issue 的最新状态是在今日被更新为 stale，但配套修复 PR #1597（SQLite 外键约束）已合并，可能相关（因数据库级联失效导致），合并 dsh 后此问题可能有所改善

### 低优先级

#### 6. [#1586 - 切换语言后部分内容未翻译](https://github.com/netease-youdao/LobsterAI/issues/1586)
- 涉及"关于→条款"页面和"工具风格"设置项未跟随英文切换

#### 7. [#1632 - 切换本地模型后原有 skill 不可用，如何安装？](https://github.com/netease-youdao/LobsterAI/issues/1632)
- 用户在使用本地模型时遇到 skill 兼容性疑问


## 6. 功能请求与路线图信号

### 已被纳入开发流程的信号

| 功能需求 | 状态 | 证据 |
|---|---|---|
| **dsh（DeepSeek Harness）引擎集成** | 已发布（2026.8.18） | 多 PR 支持（#2502、#2509、#2506），实验性可用 |
| **定时任务系统通知** | 已合并（PR #1621） | Issue #1620 已关闭，功能落地 |
| **MCP 快速添加模板** | 已合并（PR #1631） | File System / SQLite / Brave Search 三模板 |
| **用户头像设置** | 已合并（PR #1629） | 预置/上传双模式 |
| **技能"最近使用"统计** | 已合并（PR #1583） | 含 auto-routing 场景修复 |

### 值得关注的开放功能请求

1. **hermes-agent 作为可选 AI 引擎**（[#1614](https://github.com/netease-youdao/LobsterAI/issues/1614)）: 社区对多引擎/多后端支持的需求持续存在，今日 dsh 引擎的落地验证了该方向的可行性，hermes-agent 可能成为下一个候选。

2. **全局搜索修复**（[#1634 PR](https://github.com/netease-youdao/LobsterAI/pull/1634)）: 已提交详细修复方案（全局范围+搜索面板 UX 升级），处于待合并状态，预计近期进入主线。

3. **模型选择器 UI 优化**（[#1628 PR](https://github.com/netease-youdao/LobsterAI/pull/1628)）: 包含供应商图标、自适应宽度等，同样待合并。

4. **新增引擎自动唤醒/切换机制**: 有用户在 issue 中表达对深层引擎配置、切换的期望（如 #1632 本地模型 skill 兼容问题），可以推测后续版本将引入更灵活的引擎管理界面。


## 7. 用户反馈摘要

### 核心痛点

1. **技能管理体验不足**（#1617、#1632）
   - UI 不同步：删除技能后列表不刷新，需要重启且仍然显示，与后端实际状态不一致，严重困惑
   - 本地模型 skill 适配：切换本地模型后原 skill 失效，安装指引不明确

2. **任务可见性与通知缺失**（#1620 评论区）
   - 任务执行完成后须回到应用窗口查看运行记录，对长期任务的执行进度感知弱，容易错过关键时刻
   - 对通知卡片点击唤起主窗口有明确期待

3. **多引擎支持诉求**（#1614）
   - 用户参考 openclaw 的生态，希望 hermes-agent 作为可选项，期望更大的架构灵活性和引擎选择的自由度

4. **历史 Bug 长期未修复导致信任损耗**（#1587、#1589 评论区）
   - 自 4 月至今已 4 个月的启动崩溃和会话问题仍开放，且今日被标记 `stale`，用户可能担心项目维护热情和响应速度

### 正面信号

- 今日 6 条 PR 标记为 `stale` 后仍被合并，社区贡献者积极性可能被激励
- #1621（定时任务通知）从提出到合并闭环，响应链清晰

### 对维护者的启示

- 被标记 `stale` 的 Issue 若在长期得不到回复，容易让贡献者流失；今日合并的 6 条 `stale` PR 是一个积极信号，但需要同步对对应 Issue 进行状态更新与致谢，否则 PR 合并但 Issue 仍 stale 会让用户感到困惑
- #1587 和 #1589 两个跨越 4 个月的 P0 级 Bug 仍未解决，用户信任成本在上升


## 8. 待处理积压

### 长期未响应的关键 Issue

| Issue | 创建时间 | 内容 | 备注 |
|---|---|---|---|
| [#1587](https://github.com/netease-youdao/LobsterAI/issues/1587) | 2026-04-09 | 更新后首次启动崩溃（附日志） | P0 级，超 4 个月 |
| [#1589](https://github.com/netease-youdao/LobsterAI/issues/1589) | 2026-04-09 | 会话与定时任务功能均异常（macOS Intel） | P0 级，超 4 个月 |
| [#1617](https://github.com/netease-youdao/LobsterAI/issues/1617) | 2026-04-10 | 技能删除后列表不刷新，重启仍残留 | 前端状态同步问题 |
| [#1622](https://github.com/netease-youdao/LobsterAI/issues/1622) | 2026-04-10 | 无法添加自定义模型（测试失败） | 配置/模型加载问题 |
| [#1627](https://github.com/netease-youdao/LobsterAI/issues/1627) | 2026-04-10 | 复杂任务致客户端崩溃（附完整日志） | 稳定性问题 |

以上均为今日被标记 `stale` 或更新至 8-18 的 Issue。

### 待合并 PR（3 条）

| PR | 创建时间 | 内容 | 建议 |
|---|---|---|---|
| [#1628](https://github.com/netease-youdao/LobsterAI/pull/1628) | 2026-04-10 | 模型选择器 UI 重构 + 下拉面板裁剪修复 | 建议尽快 review 合并，涉及多个页面体验 |
| [#1634](https://github.com/netease-youdao/LobsterAI/pull/1634) | 2026-04-11 | 全局搜索 Bug 修复 + 搜索 UX 升级 | 高价值，建议优先处理 |
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | 2026-04-02 | dependabot electron 依赖升级（40.2.1 → 43.4.0） | 跨大版本升级，需关注兼容性；实际 2026.8.17 已合并 #2510，建议检查是否需同步 |

### 对维护者的提醒

1. **P0 级 Bug 优先处理**： #1587 和 #1589 自 4 月起已超过 4 个月未修复，今日均被标记 `stale`。建议优先分配资源修复并回应用户，避免社区信任进一步流失
2. **与合并 PR 联动更新 Issue**： #1620 已被 #1621 修复，建议关闭 Issue 以保持后台数据准确
3. **检查 dsh 集成文档完整性**： #2506 仅包含 setup 说明，后续可补充使用指南、配置文件示例与常见问题，帮助社区尽快上手实验性新功能

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 — 2026-08-19

## 今日速览

过去24小时内，Moltis 完成了2个 Issue 的关闭和5个 PR 的合并，同时发布了2个新版本（`20260818.08`、`20260818.06`），均为滚动日期版本，无破坏性变更。项目今日的活跃度处于平稳状态：提交节奏集中在既有的功能合并和 Bug 修复上，没有出现大规模的新功能引入，也没有高讨论度的社区话题。最值得关注的是两个长期挂起的 PR 获得了合并——Podman 沙箱逃生舱口支持和 OpenAI reasoning 工具调用路由优化——标志着遗留问题正在加速清理。

---

## 版本发布

### `20260818.08` / `20260818.06`
- **链接**: [Releases 页面](https://github.com/moltis-org/moltis/releases)
- **更新内容**: 两个版本均为滚动日期版本，包含过去48小时内合并的修复，预计覆盖以下变更：
  - `fix(gateway)`: heartbeat.update 参数行为修正（PR #1209）
  - `fix(sandbox)`: Podman escape hatches 支持（PR #1106）
  - `fix(readme)`: 星标历史图表修复（PR #1211）
  - 新增 managed Files library 和 Settings 浏览器（PR #1206）
- **破坏性变更**: 无
- **迁移注意事项**: 若您之前使用 `heartbeat.update` API 修改配置，请注意该接口现已按 patch 语义处理，未提供的字段将保留原值而非重置为默认值（详见 PR #1209）。

---

## 项目进展

今日共有5个 PR 被合并/关闭，涵盖两个重要方向：

**功能推进**：
- [PR #1206 — Add managed Files library and Settings browser](https://github.com/moltis-org/moltis/pull/1206) — 新增持久化的文件库，支持认证的流式上传/下载/移动/删除 API，并附带只读挂载支持（Docker、Podman、Apple Container）。同时引入 Finder 风格的 Settings 浏览器，提升配置管理的可视化。
- [PR #1198 — Route OpenAI reasoning tool calls through Responses API](https://github.com/moltis-org/moltis/pull/1198) — 当请求同时包含 function tools 与 `reasoning_effort` 时，自动走 Responses API，保留纯 Chat Completions 路径以兼容其他 providers。

**修复与清理**：
- [PR #1209 — fix(gateway): treat heartbeat.update params as a patch](https://github.com/moltis-org/moltis/pull/1209) — 修复 `heartbeat.update` 将整个配置重置为默认值的严重行为问题。
- [PR #1211 — fix(readme): restore broken star history chart](https://github.com/moltis-org/moltis/pull/1211) — 修复 README 中星标历史图表因 GitHub API 限制而无法加载的问题，切换到替代数据源。
- [PR #1106 — fix(sandbox): support Podman escape hatches](https://github.com/moltis-org/moltis/pull/1106) — 为 Podman 沙箱添加显式的 host-socket 直通和特权嵌套 Podman 逃生舱口，并改进 rootless Podman 诊断。

整体来看，项目在文件管理能力、容器兼容性和配置 API 健壮性三个方向均有实质性推进。

---

## 社区热点

今日讨论热度整体不高，评论最多的条目是：

- [Issue #1095 — Podman is not working via moltis](https://github.com/moltis-org/moltis/issues/1095)（2条评论）— 该 Issue 今日已关闭，但历史评论中包含了用户对 Podman 兼容性的详细描述。此前因缺乏 rootless 模式支持导致报错，现已由 PR #1106 修复。

虽然今日无高热度讨论，但 #1095 的关闭标志着容器支持方面一个持续两个多月的用户痛点得到解决，对使用 Podman 的开发者社区是积极信号。

---

## Bug 与稳定性

今日关闭了2个 Bug Issue，按严重程度排列：

**中等级别**：
- [Issue #1187 — Heartbeat settings UI silently resets fields not represented by the form](https://github.com/moltis-org/moltis/issues/1187) — 用户通过 UI 修改心跳设置时，表单未覆盖的字段会被静默重置为默认值，可能导致配置丢失。**已有修复**：PR #1209 已合并，将 `heartbeat.update` 语义从「整体替换」改为「部分更新」（patch）。

**低等级别（已修复）**：
- [Issue #1095 — Podman is not working via moltis](https://github.com/moltis-org/moltis/issues/1095) — 沙箱在 Podman 环境下无法启动。**已有修复**：PR #1106 已合并。

**稳定性评估**：今日无新增 Bug 报告，无崩溃或回归。两个已关闭的 Bug 均带有对应修复 PR，闭环情况良好。

---

## 功能请求与路线图信号

今日无新功能请求。但有两个重要方向值得关注：

1. **云服务集成**: [PR #1210 — Tesla Fleet API connector（处于 Open 状态）](https://github.com/moltis-org/moltis/pull/1210) 新增了特斯拉车队数据只读适配器，将车辆数据同步到本地快照存储。这个 PR 展示了 Moltis 作为「个人 AI 助手」在物联网/车辆数据接入方向的可能性。虽然该 PR 今日尚未合并，但考虑到作者为项目核心贡献者 `penso`，被纳入下一版本的概率较高。

2. **文件管理能力**: PR #1206 的合并标志着 Moltis 开始建立持久化的文件库抽象，这为后续扩展更多文件类型、云存储同步等场景打下了基础。

---

## 用户反馈摘要

今日关闭的两个 Bug 反映出的用户痛点：

- **配置丢失风险**: Issue #1187 的作者 [@IlyaBizyaev](https://github.com/IlyaBizyaev) 指出通过 UI 编辑设置时，未被表单覆盖的字段会被静默重置。这表明用户对配置的可预期性有较高要求，也希望 UI 操作不会产生「意外的副作用」。修复后该行为将更符合直觉（patch 而非 replace）。

- **容器环境的碎片化**: Issue #1095 的作者 [@RokkuCode](https://github.com/RokkuCode) 在原报告中详细描述了 Podman 环境下沙箱无法启动的问题。修复后不仅添加了逃生舱口，还改善了 rootless 模式的诊断信息——后者对用户排查问题非常有帮助。

整体评价：用户对 Moltis 的配置系统稳定性有期待，且希望项目能覆盖更多运行环境。

---

## 待处理积压

**当前值得关注的 Open PR**：
- [PR #1210 — Tesla Fleet API connector](https://github.com/moltis-org/moltis/pull/1210)（创建于 2026-08-18，1天未合）— 新功能 PR，建议维护者关注代码审查进度和测试覆盖情况。

**长期未响应的历史 Issue**：
- 当前无长时间未关闭的重大 Issue。积压清理情况良好，两个最老的 Bug（#1095 创建于6月3日）已于今日闭环。

**提醒**：如果项目维护者希望提升 Issue 追踪效率，可关注 #1095 和 #1187 的关闭是否已在 Release 说明中明确标注，以帮助用户确认升级后问题已解决。

---

*报告生成时间: 2026-08-19 | 数据来源: [Moltis GitHub Repository](https://github.com/moltis-org/moltis)*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-19

*数据来源：github.com/agentscope-ai/CoPaw*

---

## 1. 今日速览

过去 24 小时 CoPaw 项目保持了**高活跃度**：共产生 46 条 Issue 更新（新开/活跃 30 条、关闭 16 条）和 50 条 PR 更新（待合并 31 条、已合并/关闭 19 条），无新版本发布。值得注意的是，社区贡献者非常活跃 — 本日 PR 中大量来自 `first-time-contributor`，且多个 PR 带有 `Under Review` 标签，说明维护团队正在积极评审外部提交。Issue 侧呈现「稳定期收尾」特征：一批 7 月中旬至 8 月初提交的旧 Issue（如 #4001、#5584、#6457、#6794）在今日集中关闭，表明 2.1.0 的修复工作接近尾声。与此同时，社区关注的焦点集中在**多步骤任务中断、MCP 连接稳定性、沙盘安全问题**三大方向。项目整体健康度良好，但 PR 队列（31 条待合并）存在一定积压。


## 2. 版本发布

今日无新版本发布。

> 最新版本仍为 **v2.1.0**（及 2.1.0 beta 迭代线）。社区围绕 2.1.0 的反馈持续涌入，建议维护团队关注下文中 Bug 与稳定性板块的 P0/P1 问题，为 2.1.1 或 2.2.0 的排期提供依据。


## 3. 项目进展

今日无直接 merge 到 main 的 PR（19 条已合入/关闭的 PR 中多数为贡献者主动关闭或维护者 reject），但**评审进展显著**。以下 PR 值得关注：

**评审中（接近合入）：**

- **[#6990] fix(skill): Reduce file IO for system files & skills files via file cache — READY TO MERGE**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6990)）— 作者 Leirunlin 明确标注 [READY TO MERGE]。该 PR 为系统提示词与技能文件引入进程级缓存，减少重复文件读取与 frontmatter 解析，预期可降低每次查询的系统开销。这是性能优化方向的重要改进。

- **[#7097] fix(skill): remove skill bound duplication — do not merge**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/7097)）— 作者同样为 Leirunlin，虽标注 [do not merge]（可能用于测试或进一步讨论），但解决的问题是 workspace 技能覆盖 built-in 技能的优先级回归，属于重要的正确性修复。

- **[#6764] feat(CI): gate main mergeability on required checks**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6764)）— 该 PR 针对「main 分支无门禁、测试失败也能合入」的流程漏洞（援引 #6418 因三个测试任务失败仍被合入），如合入将显著提升主干稳定性。

**值得关注的新提交：**

- **[#7112] feat: isolated local QwenPaw Pro control plane**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/7112)）— 引入 opt-in 的本地多租户控制面（`qwenpaw app --pro`），该方向信号强烈，可能预告 Pro 商业化版本的技术预演。

**合入的修复（来自已关闭 PR）：**

- **[#7069] fix(console): render data-URL images in historical messages on session reload**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/7069)）— 修复会话重载后历史消息中 data-URL 图片无法显示的问题（对应 #7051）。

- **[#7072] feat(console): background chat task list API**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/7072)）— 为后台任务增加列表查询 API，是多智能体协作的基础设施补充（对应 #7056）。

- **[#7064] fix(cli): sync top-level text on cron update --text for agent jobs**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/7064)）— 修复 cron 任务更新 prompt 时顶层文本未同步的问题（对应 #7048）。


## 4. 社区热点

**🔥 今日最热 Issue：**

**1. [#6684] 增加频道的重试功能**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6684)）— 10 条评论
> 用户使用自建 Matrix 频道时，QwenPaw 启动速度快于 Matrix 服务导致连接失败，且无重试/健康检测机制，每次服务器重启后需手动重新保存频道。该 Issue 已延续两周讨论，反映了**频道层连接健壮性**是自托管用户的核心痛点。

**2. [#6921] 多步骤任务无提示自行停止**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6921)）— 8 条评论
> 用户反馈执行多步骤任务时，Agent 在输出 "Now 2.1, 3.1, 3.2. Let me do all three." 等规划后就停止，且无任何提示，需用户说「继续」才能恢复。已有 8 条讨论，社区对「Agent 自主规划下一步但未执行就中断」的行为模式较为关注，涉及 Agent 循环的内部状态问题。

**3. [#7102] Freeze more than 10 minutes long**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7102)）— 7 条评论
> 用户报告 QwenPaw Desktop 2.1.0 搭配 GLM 5.3 时出现超过 10 分钟的完全无响应（无 token 输出、思考过程也冻结）。标注 `need-info`，尚待更多日志信息。

**4. [#7011] Console stop request can cancel an active Feishu session under multiple UI sessions**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7011)）— 7 条评论
> 多 UI 会话下，Console 的停止请求会错误取消活跃的飞书会话。作者 djj532 提供了更新后的直接证据（会话身份在 UI 会话间串线），是比较严重的**多通道/多会话隔离**问题。

**社区贡献者活跃度：** 今日 PR 中 suantea 一人贡献 4 条（#7064、#7066、#7069、#7072），为今日最活跃的社区贡献者。


## 5. Bug 与稳定性

按严重程度排列：

**🔴 P0 — 崩溃/完全不可用**

- **[#7082] Model 'unknown' execution failed: `_StructuredOutputDynamicClass` is not fully defined**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7082)）— 新开。Console 通道下 Agent/工具包初始化即失败，根因是 Pydantic 模型未完整定义（需 `model_rebuild()`）。影响所有使用结构化输出的用户。**尚无对应 PR。**

- **[#7063] Agent 执行工具调用时必现崩溃**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7063)）— 已关闭。`_acting(tool_call)` 返回 coroutine 但被 `async for` 遍历，导致 `TypeError`。**已关闭，但关闭原因未明确标注为已修复**（可能是重复报告或已在其他 PR 中修复），建议确认。

- **[#7110] 对话上下文中包含无法下载的图片链接，整个会话不可用**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7110)）— 新开。单个 403 图片 URL 即可让整个会话挂死，只能 `/clear`。属于**单点故障**设计缺陷。**尚无对应 PR。** *该 Issue 同时被 #7087（PR）所覆盖，该 PR 提出在请求模型前本地化远端媒体 URL，值得关注。*

**🟠 P1 — 功能中断/数据异常**

- **[#7011] Console 停止请求可取消活跃飞书会话（多 UI 会话下）**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7011)）— 多会话身份串线，导致 AI 会话被误终止。**尚无对应 PR。**

- **[#7074] 正常运行崩溃，需刷新页面才能重启，频次高发**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7074)）— 用户报告频繁崩溃，已附日志（session.py 状态恢复异常）。标注 `need-info`。

- **[#7102] 冻结超过 10 分钟**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7102)）— GLM 5.3 下完全冻结。标注 `need-info`，需更多日志。

- **[#7005] Enabling Sandbox causes UV Run to fail**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7005)）— 沙盘启用后 `uv run` 无法写入 `~/.cache/uv`，用户自行添加 `Write(~/.cache/uv/**)` 策略作为 workaround。**已有对应 PR #7116**（覆盖路径 `~` 展开修复），值得优先推进。

- **[#6921] 多步骤任务自行停止无提示**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6921)）— 非崩溃但影响核心体验的 Agent 行为异常。

- **[#7076] qwenpaw-creator: LLM 模型配置报错 404**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7076)）— 使用最新 2.1.0 时 Creator 插件的模型配置接口返回 404。

**🟡 P2 — 体验/兼容性问题**

- **[#7065] 多轮对话后无法查看早期聊天记录**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7065)）— 已关闭（可能为重复报告）。
- **[#7009] Pod 终止误报（Cloudflare Tunnel + monitor 插件）**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7009)）— 已关闭。平台自动检测误判反代/挖矿进程，误杀 Pod。

> **系统性观察：** 今日 Bug 报告中有 4 条直接与「外部服务交互失败后的降级处理」相关（#7110 图片 403、#7005 沙盘目录限制、#6470 MCP transport 硬编码、#6921 Agent 中断后不恢复）。项目整体对**异常路径的韧性不足**，建议在下一迭代投入系统性改进。


## 6. 功能请求与路线图信号

**高潜力纳入下一版本的功能：**

| 功能请求 | Issue | 关联 PR / 信号 |
|---|---|---|
| **插件 API 增加 system_prompt 权限** | [#7052](https://github.com/agentscope-ai/QwenPaw/issues/7052) | 企业用户有明确的隐私诉求（不想让最终用户看到公司提示词） |
| **按 agent/会话级配置 reasoning_effort** | [#7062](https://github.com/agentscope-ai/QwenPaw/issues/7062) | 用户需要为不同角色设置不同思考深度，目前只能全局配置 |
| **技能池导入增加搜索/过滤** | [#7090](https://github.com/agentscope-ai/QwenPaw/issues/7090) | 技能数量达数百后翻找困难，体验改进成本低、收益明确 |
| **单条消息删除** | [#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001) | 今日已关闭，3 个多月的老需求大概率已在最新版实现或进入排期 |
| **频道重试/健康检测** | [#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684) | 自托管用户刚需，讨论 10 条持续两周，建议排入 2.1.1 |
| **智能体协作同一会话窗口** | [#6925](https://github.com/agentscope-ai/QwenPaw/issues/6925) | 当前每次协作都新建会话且需切换智能体查看，交互割裂 |
| **文件预览可关闭** | [#7039](https://github.com/agentscope-ai/QwenPaw/issues/7039) | 用户更习惯点击即下载，需提供开关选项 |
| **后台聊天任务列表 API** | [#7072](https://github.com/agentscope-ai/QwenPaw/pull/7072) 已合入 | 对应 #7056，多智能体编排基础设施逐步完善中 |

**路线图信号：** PR #7112 引入的 `qwenpaw app --pro` 本地隔离控制面是重要信号 — 该项目可能在向**企业多租户/商业化方向**演进。结合 #7052（企业提示词隐私）、#7112 的 tenant-scoped 凭据管理，可以判断项目团队正在为企业版铺路。


## 7. 用户反馈摘要

**核心痛点：**

- **Agent 自主性不足：** 「经常在规划好下一步就停止…需要说『继续』才会继续任务」（[#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)）— 多步骤任务中断且无提示，严重削弱 Agent 的「自主执行」价值主张。

- **异常路径恢复能力差：** 「消息记录里出现一个没法访问的图片链接，这个会话下面就彻底挂掉了」（[#7110](https://github.com/agentscope-ai/QwenPaw/issues/7110)）；「每次服务器启动后都需要手动重新保存一次频道才能恢复连接」（[#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684)）— 用户对「单点故障拖垮整个会话/连接」的设计较为不满。

- **界面信息架构：** 「思考和调用工具占了满屏，结果藏在思考过程中」（[#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260)）— 用户更关注 Agent 交付的结果而非过程细节，希望可以折叠思考过程。

- **安全担忧：** 「Malware Bytes found Trojan Loader in Desktop Version」( [#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775) ) — 英文用户对 Windows 桌面版的杀软误报感到困惑，并明确表示「在得到团队回复前卸载」。安全误报的响应时效值得关注。

**正面反馈：**

- 「更新到 2.1.0 版本后确实发现很多改善，比如**公式显示正常了**」（[#7039](https://github.com/agentscope-ai/QwenPaw/issues/7039)）— 渲染修复获得了认可。
- 社区贡献者活跃度高，多位 `first-time-contributor` 提交的 PR（#7061、#7064、#7066、#7069、#7071、#7072）质量扎实且直击真实痛点，说明项目的贡献文档和架构对新人足够友好。


## 8. 待处理积压

**⚠️ 长期未响应的关键 Issue：**

| Issue | 创建时间 | 持续时间 | 重要性 | 说明 |
|---|---|---|---|---|
| **[#6470] MCP transport 硬编码 SSE，streamable_http 服务器无法连接**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6470)） | 2026-07-26 | **24 天** | 🔴 高 | 影响所有使用 Streamable HTTP 传输协议的 MCP 用户；`mcp_stateful_client.py` 硬编码 `sse_client`，已定位到具体代码位置，但至今无对应 PR。 |
| **[#5900] MCP streamable_http 会话终止后不自动重连**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/5900)） | 2026-07-09 | **41 天** | 🔴 高 | 会话中断后 MCP 客户端永久跳过，无自动重连。与 #6470 同为 MCP 稳定性短板。 |
| **[#6775] Malware Bytes 误报 Trojan Loader**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6775)） | 2026-08-07 | **12 天** | 🟠 中 | 安全误报直接影响用户信任，用户已卸载软件并等待官方回应。建议防病毒厂商申诉或发布澄清说明。 |
| **[#6683] qwenpaw-creator 安装失败：顶层模块命名冲突**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6683)） | 2026-08-04 | **15 天** | 🟠 中 | 插件 `utils` 目录与系统 `utils` 模块冲突。已定位根因但无对应 PR。 |
| **[#6800] 智能邮箱管理助手 PR**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6800)） | 2026-08-07 | **12 天** | 🟢 待评估 | 12 天无维护者评论。功能价值高（邮件自动分类/回复/推送），建议维护者给出明确反馈。 |

**📋 PR 积压提醒：**

- 当前 31 条 PR 待合并中，最早可追溯到 7 月 28 日的 **[#6515] Volcengine Agent Plan & MiMo V2.5 新 provider**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6515)）— 已等待 22 天。该 PR 基于新 provider 架构重构，涉及面广可以理解，但建议给出明确状态更新。
- **#6617 Retry-After cap（待合并，已 19 天）**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6617)）— 修复 429 重试策略的重要 PR，标注 Under Review 且已被关闭过（需确认是否已合入）。
- 多数 `first-time-contributor` PR 都在等待首次 review，建议维护团队考虑对标记 `Under Review` 的 PR 设置 SLA 以保持贡献者热情。


### 附：项目健康度总结

| 指标 | 状态 | 评价 |
|---|---|---|
| 社区活跃度 | 🟢 极佳 | 46 Issue + 50 PR 日更新，贡献者参与度高 |
| 问题响应速度 | 🟡 中等 | 新 Issue 大多当天有 `need-info` 标注，但老 Issue（#6470 #5900）存在超 3 周未响应 |
| PR 评审效率 | 🟡 待提升 | 31 条 PR 待合并，最早 22 天前提交；多天无维护者评论 |
| Bug 修复进度 | 🟢 良好 | 2.1.0 类问题（#4001 #5584 #7063 等）批量关闭，说明修复在推进 |
| 风险信号 | 🟠 注意 | MCP 相关 2 个高龄高优 Issue 未解决；Agent 自主中断、沙盘路径等 P0/P1 新问题持续出现 |

*日报生成时间：2026-08-19 | 数据覆盖窗口：2026-08-18 00:00 UTC — 2026-08-19 00:00 UTC*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 ZeroClaw 项目（github.com/zeroclaw-labs/zeroclaw）在 2026 年 8 月 19 日的 GitHub 数据生成的项目动态日报。

---

### ZeroClaw 项目动态日报 (2026-08-19)

#### 1. 今日速览

ZeroClaw 项目今日处于 **高活跃度、高压力的攻坚阶段**。过去 24 小时内，Issue 和 PR 更新均达到 50 条，但核心焦点集中在 **安全加固** 与 **架构重构** 上。大量 `risk:high` 且带有 `do-not-merge` 标签的 PR 正在等待维护者审查，表明项目正在进行大规模的内部治理和稳定性提升，而非单纯的功能迭代。值得关注的是，今日有一项针对 **Google STT API 密钥泄露** 的紧急修复 PR (#10107) 被提交，凸显了项目在安全细节上的快速响应。尽管新版本发布为 0，但多项核心功能的 RFC 讨论（如 Goal mode、Session-scoped 附件）已进入尾声，预示着未来可能有重大版本更新。

#### 2. 版本发布

N/A - 过去 24 小时内无新版本发布。

#### 3. 项目进展

今日合并/关闭的 PR 数量较少（4 条），但其中包含一项关键修复：

- **内存管理修复**：[PR #10009](https://github.com/zeroclaw-labs/zeroclaw/pull/10009) `fix(memory): key conversation autosave suppression on turn origin` 已合并。该 PR 修复了对话自动保存逻辑中的一个缺陷——原本通过嗅探提示词中的合成前缀（如 `[cron:`）来决定是否跳过保存，但该过滤器依赖于位置且易被绕过。此修复将决定权改为基于回合来源（turn origin），提升了记忆存储的准确性和可靠性。

这表明项目在持续优化核心 agent 循环的稳定性。除此之外，大量待合并的 PR（46 条）仍然堆积，其中包含多个被标记为 `do-not-merge` 的重大重构（如 config 迁移、provider 重构），短期内项目重心仍是内部治理。

#### 4. 社区热点

今日讨论热度最高的议题主要集中在**长期存在的架构性问题**上，社区对项目的发展方向有深度参与：

- **[RFC: Goal mode v1](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)** (评论: 22): 这是讨论最激烈的 Issue。用户 `vrurg` 提议引入一种持久的、有界的目标模式，允许 agent 跨多个回合追求一个用户目标。讨论焦点在于如何在首版中界定范围，避免将重启交接、渠道准入、异步子任务等复杂概念全部耦合进来。这反映了用户对 ZeroClaw 作为 **自主agent** 而非简单聊天机器人的更高期待。
- **[Bug: 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** (评论: 17): 这是一个长期存在的严重稳定性问题。Windows 11 用户 `NiuBlibing` 报告了大量测试失败，源于 Unix-only 命令、路径语义和控制台编码。由于 CI 仅在 Linux 上运行，此问题一直未被发现，引发了社区对 **跨平台测试覆盖** 的广泛担忧。
- **[Feature: Unify slash-command registries](https://github.com/zeroclaw-labs/zeroclaw/issues/7929)** (评论: 8): 用户指出 Web UI、ZeroCode TUI 和渠道运行时之间的斜杠命令列表存在严重漂移，导致功能不一致。这是一个典型的 **架构一致性** 诉求，希望项目能够统一入口，降低维护成本和使用困惑。

#### 5. Bug 与稳定性

今日报告的 Bug 中，安全问题尤为突出，且均已有相应的修复 PR：

- **严重 (P1) - 凭据泄露风险**:
  - [PR #10107](https://github.com/zeroclaw-labs/zeroclaw/pull/10107) `fix(channels): keep Google STT API keys out of URLs` (今日提交): 修复了 Google 语音转文字 API 密钥可能出现在 URL 中的问题，防止密钥通过代理日志和监控记录泄露。**修复 PR 已提交**。
  - [Issue #8542](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) `MCP/tool-schema cloning drives unbounded RSS growth`: 跟踪了 agent 循环中因工具模式克隆导致的内存无限增长问题，可能导致 OOM。**修复中**，相关 PR #8633 已解决其上游问题。

- **中等 (P2) - 功能异常**:
  - [Issue #8410](https://github.com/zeroclaw-labs/zeroclaw/issues/8410) `channel tasks need a first-class intentional no-reply outcome`: 渠道任务在条件不满足时（如“无新邮件时保持沉默”）仍会发送可见回复，需要引入“有意不回复”的机制。
  - [Issue #8134](https://github.com/zeroclaw-labs/zeroclaw/issues/8134) `Reset stale channel sessions`: `session_ttl_hours` 配置参数未被实现，导致过期会话历史不会被截断，增加 token 消耗和响应延迟。

#### 6. 功能请求与路线图信号

今日的 Issues 和 PR 强烈暗示了下一版本的方向，主要集中在**持久化、个性化和安全**三个维度：

- **持久化目标与上下文**:
  - [Issue #9998](https://github.com/zeroclaw-labs/zeroclaw/issues/9998) `RFC: Session-scoped persistent prompt attachments`: 提出将会话目标/约束“钉”在会话上，防止因历史修剪或守护进程重启而丢失。这是对 agent 长任务处理能力的补全。
  - [Issue #8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) `RFC: Goal mode v1`: 正如前文所述，这是实现跨回合目标的核心设计。

- **配置与个性化下沉**:
  - [PR #9013](https://github.com/zeroclaw-labs/zeroclaw/issues/9013) `refactor(config)!: move TodoWrite display config from the daemon into zerocode`: 表明项目正在将显示、界面相关的配置从核心 daemon 中剥离，下沉到客户端层，这与“统一斜杠命令注册表 (#7929)”的诉求一脉相承，旨在让核心更稳定，边缘更灵活。

- **安全加固**:
  - [PR #9194](https://github.com/zeroclaw-labs/zeroclaw/pull/9194) `feat(secrets): extract KeySource trait + FileKeySource backend`: 旨在抽象主加密密钥的来源，为更灵活的密钥管理（如 KMS、环境变量）打基础。
  - Bug #8519 持续跟踪 `wasmtime-wasi` 的 CVE 修复，表明项目对供应链安全的重视。

#### 7. 用户反馈摘要

- **痛点：跨平台体验差**。Issue #7462 的讨论中，Windows 用户的挫败感很强，认为项目“在 Windows 上是二等公民”，因为 CI 不跑 Windows 测试导致大量问题无法被提前发现。
- **痛点：功能不一致导致的困惑**。Issue #7929 中，用户抱怨同一个命令在不同界面（Web/TUI/渠道）的行为和可用性不同，增加了学习和使用成本。
- **诉求：真正的自主性**。Issue #8303 和 #9998 的讨论表明，用户不再满足于简单的问答，而是希望 ZeroClaw 能够像一个真正的“agent”一样，记住目标、跨回合执行任务，并在长时间运行中保持状态。

#### 8. 待处理积压

以下问题和 PR 长期未得到充分响应，可能成为项目发展的瓶颈，需维护者特别关注：

- **高风险 PR 堆积**：大量标记为 `risk:high` 且 `do-not-merge` 的 PR（例如 #10003, #9013, #9194）已等待超过 3 周。这些是可能改变架构或涉及安全的重磅更新，长期搁置不仅会导致代码冲突，也会让贡献者感到挫败。
- **[Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 测试失败**：作为长期存在的 P1 问题，讨论热度高但进展缓慢。这不仅是技术债，更影响了项目的声誉和用户基础拓展。
- **[Issue #8858](https://github.com/zeroclaw-labs/zeroclaw/issues/8858) Audit existing drift surfaces**: 该 tracker 旨在审计代码库中的“漂移”问题（如文档与实现不一致），反映了项目在快速发展中产生的内部一致性问题，工作量巨大，需要系统性解决。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*