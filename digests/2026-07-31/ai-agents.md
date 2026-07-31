# OpenClaw 生态日报 2026-07-31

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-31 01:26 UTC

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

# OpenClaw 项目动态日报 — 2026-07-31

## 今日速览

OpenClaw 项目过去 24 小时保持极高度活跃，Issues 和 PR 各约 500 条更新，其中新开/活跃 Issue 484 条，待合并 PR 417 条。社区讨论热度集中于**消息丢失、会话状态管理和安全边界**三大主题。今日 0 个新版本发布，但 P0/P1 级问题仍有多项处于长期未解决状态（如 Gateway 内存泄漏 #91588 持续 53 天未关闭），表明项目在功能迭代速度与稳定性之间面临平衡压力。PR 侧有多个针对既有问题的修复提交，但大量 PR 处于 "needs proof" 或 "waiting on author" 状态，合并管线存在一定积压。

---

## 版本发布

**今日无新版本发布。**

考虑到有数个 P0/P1 级稳定性问题（内存泄漏、崩溃循环）已积压多日且社区呼声较高，版本发布节奏可能正在为包含这些修复的版本做准备。

---

## 项目进展

今日虽无新版本，但多个 PR 推进了关键修复：

- **#116605（已关闭/已合并）**：修复 Code Mode 在 Gateway 重启后无法恢复的问题——当重启后配置禁用 Code Mode 时，in-flight 的 replay-safe 运行不再被错误中止。这是对"重启恢复"场景的重要完整性修复。
- **#116600**：修复 edit 工具 fuzzy matching 会静默规范化未目标行上 Unicode 字符（如 CJK 全角标点、破折号、智能引号）的问题，避免非目标内容被意外改写。
- **#116216**：修复并发 WebSocket acquire 时共享会话缓存被覆盖的问题，该问题可能导致 `previous_response_id` 延续链断裂而损坏后续 turn。
- **#102173**：修复工具调用前隐藏的 assistant 文本被当作已展示文本在下一次 turn 中重播的问题，直接影响消息渠道用户体验。
- **#116584（automerge armed）**：修复通过 agent command 或隔离 cron 选择的 Ollama 模型其 thinking level 被 `ollama/*` 通配策略错误拒绝或降级的问题。

整体来看，项目今日在**会话状态完整性**（restart recovery、cache 覆盖、文本重播）和**工具执行准确性**（Unicode 保留、thinking level 保留）方面有明确推进，但在更大体量的架构性改进（如 #102261 的 Codex 交互模式对齐）上仍在等待验证与合并。

---

## 社区热点

| 议题 | 评论数 | 核心诉求 |
|------|--------|----------|
| [#25592: Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592) | 38 | 内部处理文本（错误处理、处理确认、叙述）被错误路由到 Slack/iMessage 等消息渠道，造成严重的 UX 问题。已有 PR #102173 针对性修复 |
| [#91588: Gateway Memory Leak — RSS grows from 350MB to 15.5GB](https://github.com/openclaw/openclaw/issues/91588) | 22 | P0 级内存泄漏，正常使用 2-3 天 RSS 从 350MB 膨胀至 15.5GB，触发 OOM kill 和反复重启循环。已持续 53 天未解决 |
| [#115326: Crash-loop breaker suppresses Discord/WhatsApp permanently](https://github.com/openclaw/openclaw/issues/115326) | 20 | 崩溃循环保护器导致 Discord/WhatsApp 被永久抑制，文档提供的恢复路径 `channels.start` 失败（WebSocket 1006） |
| [#22438: Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438) | 17 | 大型工作区用户希望按需分级加载 bootstrap 文件，避免子代理和 cron 任务浪费 context 预算 |
| [#102175: Embedded prompt cache breaks across boundaries](https://github.com/openclaw/openclaw/issues/102175) | 16 | 长会话中提示缓存命中在跨 room-event、授权、队列、压缩、恢复和 Responses continuation 边界时丢失，模型可见的工具清单在 44 个 turn 间发生变化 |

**热点分析**：社区最集中的诉求是 **"代理消息行为的可控性"**——哪些文本应该发到渠道、哪些应该保持内部，以及**系统稳定性**——内存泄漏、崩溃循环恢复、缓存破坏这些问题直接影响真实使用。这些问题的共同特征是：不一定导致功能完全不可用，但会导致不可预测的行为，对依赖自动化代理的用户极为困扰。

---

## Bug 与稳定性

### P0 级

| Issue | 描述 | 状态 |
|-------|------|------|
| [#91588: Gateway 内存泄漏 (350MB→15.5GB, OOM 崩溃)](https://github.com/openclaw/openclaw/issues/91588) | RSS 持续增长直至被 OOM killer 终止，触发 launchd-handoff 重启循环。持续 53 天 | 无 fix PR |
| [#48920: Live Docs 超前于发布版本](https://github.com/openclaw/openclaw/issues/48920) | 文档中的 IsolatedSessions 配置在实际版本 2026.3.13 中不存在，文档与发布脱节 | 无 fix PR |

### P1 级

| Issue | 描述 | 是否已有 fix PR |
|-------|------|----------------|
| [#115326: 崩溃循环保护器永久抑制 Discord/WhatsApp](https://github.com/openclaw/openclaw/issues/115326) | 文档恢复路径 channels.start 失败 (WebSocket 1006) | 否 |
| [#102175: 嵌入式提示缓存跨边界失效](https://github.com/openclaw/openclaw/issues/102175) | 同会话中 prompt cache 命中在多个边界处断裂 | 否 |
| [#29387: agentDir 中 bootstrap 文件被静默忽略](https://github.com/openclaw/openclaw/issues/29387) | 仅 workspace 目录的文件被注入 system prompt，per-agent 目录无效 | 否 |
| [#48003: Steer mode 不注入消息到主会话](https://github.com/openclaw/openclaw/issues/48003) | `messages.queue.mode: "steer"` 失效，消息排队到 turn 结束 | 否 |
| [#40001: Write 工具缺少 append 模式](https://github.com/openclaw/openclaw/issues/40001) | 隔离 cron 会话覆写共享文件导致静默数据丢失 | 否 |
| [#51429: 硬编码工作路径被合并发布](https://github.com/openclaw/openclaw/issues/51429) | 代码中硬编码了 `/Users/wangtao` 路径，新安装用户工作区被设为此目录 | 否 |
| [#51396: clearUnboundScopes 无条件剥离 operator 权限](https://github.com/openclaw/openclaw/issues/51396) | 2026.3.13 回归：非本地 token-auth 客户端的 operator 作用域被错误清除 | 否 |

多个 P1 级 bug 在 3 月报告后已持续近 5 个月，处于 **needs-maintainer-review + needs-product-decision** 状态，这可能反映维护者对该等问题的产品方向决策存在分歧或资源不足。

### 近期值得注意的新 Bug

- [#116201: Realtime voice 可无限持有 provider 和 consult 状态](https://github.com/openclaw/openclaw/issues/116201)（7月30日新开，P1）：语音会话缺少硬性资源上限，慢速/突发性 provider 行为可导致超量状态保留。无 fix PR。

---

## 功能请求与路线图信号

### 高热度功能提案

| Issue | 诉求 | 信号强度 |
|-------|------|----------|
| [#42475: 每代理成本预算执行（gateway 级）](https://github.com/openclaw/openclaw/issues/42475) | 在 gateway 调度前强制每日/月度 token 成本上限 | ⭐⭐⭐ 运维刚需，与 #39807（计费 402 无限重试）形成呼应 |
| [#22358: 子代理完成后扩展钩子](https://github.com/openclaw/openclaw/issues/22358) | `post_subagent_complete` 钩子，自动生成轨迹文件 | ⭐⭐ 工作流自动化的自然延伸 |
| [#27445: 子代理完成通知的 announceTarget 选项](https://github.com/openclaw/openclaw/issues/27445) | 子代理完成后通知作为 user-message 触发而非直接到渠道 | ⭐⭐ 与 #22358 同属子代理编排增强 |
| [#80213: Skill 作者自定义 setup 钩子](https://github.com/openclaw/openclaw/issues/80213) | SKILL.md frontmatter 中增加 setup.script，安装/更新后执行 | ⭐⭐ 生态建设方向 |
| [#20786: Telegram Business Bot 支持](https://github.com/openclaw/openclaw/issues/20786) | 支持 business_message / business_connection 更新类型 | ⭐⭐ 渠道扩展需求 |

### 与已有 PR 匹配的功能请求

- **#22438（Tiered bootstrap file loading）** 是 #29387 的架构性解决方案方向——对 bootstrap 加载机制的不满正在催生更大的设计变更。
- **#25592（工具调用间文本泄漏到消息渠道）** 已有 PR #102173 修复，处于 "ready for maintainer look"。
- **#102261（Interactive parity with Codex runtime: ask-user-question · plan mode · goal mode）** 是一个 XL 规模的 PR，为所有会话引入 Codex 风格的三类交互原语，涵盖 ask-user-question、plan mode 和 goal mode，说明项目有意将 Codex 原生体验推广至全部会话，目前在等 proof。

---

## 用户反馈摘要

- **数据丢失是最高频痛点**：#40001（write 覆写）、#48810（压缩重试产生孤儿 fork 破坏链重建）、#49876（cron 会话幻觉输出而非干净失败）均涉及不同程度的数据完整性问题。#40001 获 diamond lobster 评分，用户明确表达"silent data loss"是最不可接受的错误类型。
- **告警信息不达渠道**：#54531（回复未发送到原始渠道）、#50739（system event 在 lane 拥塞时排在 LLM 请求之后）反向印证了 #25592 的问题——"什么该发到渠道"的信息分发控制是用户关注的焦点。
- **本地模型支持意愿强**：#116606 改进 LM Studio 引导流程、#116584 修复 Ollama thinking 保留，两个 PR 均获维护者参与，表明本地模型方向在持续投入。
- **多代理资源治理呼吁**：#35203（能力画像+共享黑板+分层记忆+成本治理）、#48874（共享 LLM + 隔离会话）、#67413（per-agent dreaming 配置，获 5 👍）指向同一个方向——多代理场景下的资源隔离与治理亟需系统化方案。
- **配置升级断裂感**：#102138/#102163/#102170 系列（google provider 旧配置升级后静默丢失）和 #102180（openai session 路由 stale）表明用户对升级后配置兼容性高度敏感。多个修复PR均已就绪，但部分处于 waiting on author 状态。

---

## 待处理积压

### 需维护者立即关注

| Issue/PR | 关键信息 | 积压时长 |
|----------|----------|----------|
| [#91588: Gateway 内存泄漏 P0](https://github.com/openclaw/openclaw/issues/91588) | 反复 OOM，53 天无 fix PR | 53 天 |
| [#115326: 崩溃保护器永久抑制渠道 P1](https://github.com/openclaw/openclaw/issues/115326) | 恢复路径失效，用户无法自救 | 3 天（但影响严重） |
| [#114534/RSS 类内存问题群组](https://github.com/openclaw/openclaw/issues/91588) | 与 #91588 同类的 gateway 资源管理问题还有多个 | 数周至数月 |

### 长期未响应的关键 Issue

| Issue | 关键信息 | 积压时长 |
|-------|----------|----------|
| [#29387: agentDir bootstrap 文件被忽略](https://github.com/openclaw/openclaw/issues/29387) | 用户配置不生效，获 5 👍 | 5 个月 |
| [#40001: Write 工具无 append 模式](https://github.com/openclaw/openclaw/issues/40001) | 静默数据丢失，获 diamond lobster 评分 | 5 个月 |
| [#51429: 硬编码工作路径被合并发布](https://github.com/openclaw/openclaw/issues/51429) | 严重质量问题但无响应 | 4 个月 |
| [#51396: 权限剥离回归](https://github.com/openclaw/openclaw/issues/51396) | 影响所有非本地 token-auth 客户端 | 4 个月 |
| [#47910: 按失败类型隔离 provider 回退](https://github.com/openclaw/openclaw/issues/47910) | 同一会话中 5,206+ 次失败请求无退避 | 4.5 个月 |

### 等待 author 响应的 PR

| PR | 状态 | 等待原因 |
|----|------|----------|
| [#102166: 标记空 tool-error turn 为不可投递](https://github.com/openclaw/openclaw/pull/102166) | ⏳ waiting on author | 需补充更多信息 |
| [#102213: formatProviderModelRef 前缀剥离修复](https://github.com/openclaw/openclaw/pull/102213) | 📣 needs proof | 缺少验证证据 |
| [#97646: flushPendingToolResults 延迟一个事件循环 tick](https://github.com/openclaw/openclaw/pull/97646) | 📣 needs proof | 需要验证修复效果 |

---

**总结**：OpenClaw 项目社区活跃度极高，功能迭代方向明确（会话状态管理、多代理编排、本地模型支持），但长期存在的 P0/P1 稳定性问题（内存泄漏、数据丢失、配置兼容性）仍未得到及时修复，且多个关键 PR 卡在等待验证或作者响应阶段，合并管线效率有待提升。建议维护团队优先处理积压的 P0/P1 稳定性问题，并为一组相互关联的数据完整性修复（#40001 + #48810 + #49876）制定整体解决方案。

---

## 横向生态对比

# 2026-07-31 个人 AI 助手开源生态横向对比分析报告

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**高速扩张与结构性分化并存**的阶段。以 OpenClaw 为代表的头部项目维持极高社区活跃度（日均 500+ Issue/PR 更新），但 P0 级稳定性问题（内存泄漏、数据丢失）长期积压，暴露了"功能迭代速度与工程质量平衡"的普遍困境。与此同时，一批差异化竞争者（IronClaw、NanoClaw、Moltis、LobsterAI）分别在架构重构、安全加固、企业级功能、轻量化部署等维度切入，生态呈现**多极竞争、局部收敛**的态势。跨项目的共性需求——**会话状态隔离、消息分发控制、成本治理、多代理编排、安全边界**——正成为驱动下一轮技术演进的核心议题。值得警惕的是，多个项目在"会话状态管理""文本泄漏到渠道"等基础问题上反复出现同类 Bug，表明该领域仍缺乏成熟的最佳实践范式。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 待合并 PR | Release | 健康度评估 |
|------|------------|---------|----------|---------|-----------|
| **OpenClaw** | ~484 活跃 | ~417 待合并 | 417 | 无 | ⚠️ 极高度活跃，但 P0 问题积压 53 天未解，合并管线积压严重 |
| **Hermes Agent** | 50 | 50 | 大量（含撤回/重复清理） | ✅ v0.19.1 | 🟢 高频迭代，维护者积极清理重复 PR，项目健康 |
| **IronClaw** | 40（34 活跃） | 50（29 待合并） | 29 | 无 | 🟢 架构重构 Wave 0 启动，安全 Issue 需关注 |
| **NanoClaw** | 2 新开 | 19（7 合并） | 12 | 无 | 🟢 安全加固与镜像优化同步推进，良性循环 |
| **CoPaw (QwenPaw)** | 25（18 活跃） | 50（24 待合并） | 24 | 无 | 🟢 合并效率高，维护者响应快 |
| **LobsterAI** | 0 | 10（8 合并） | 2 | ✅ 2026.7.29 | 🟢 合并为主，核心团队高效推进，企业级方向明确 |
| **ZeroClaw** | 15 | 50（0 合并） | 50 | 无 | 🔴 高活跃但合并为 0，积压风险积聚 |
| **NanoBot** | 7（5 活跃） | 50（17 待合并） | 17 | 无 | 🟢 架构升级（SQLite 迁移）推进中，回归修复收尾 |
| **Moltis** | 2 新开 | 4（1 合并） | 3 | 无 | 🟡 中等活跃，安全修复与可观测性建设并进 |
| **PicoClaw** | 7（4 活跃） | 17（12 待合并） | 12 | 无 | 🟡 中高活跃，功能请求等待周期较长 |
| **ZeptoClaw** | 0 | 1（0 合并） | 1 | 无 | 🔴 低活跃，核心安全修复 PR 8 天无评审 |
| **NullClaw / TinyClaw** | 0 | 0 | — | — | ⚪ 无活动 |

---

## 3. OpenClaw 在生态中的定位

- **社区规模与影响力**：OpenClaw 以日均 500+ Issue/PR 的体量遥遥领先（IronClaw 40/50、CoPaw 25/50），是生态内无可争议的**流量中心与参照基准**。其问题讨论（如 #25592 文本泄漏、#91588 内存泄漏）常成为其他项目社区引用或对齐的对象。

- **技术路线特征**：OpenClaw 采用**单体架构 + 广泛渠道适配**（Slack/iMessage/Discord/WhatsApp/Telegram 等），强调"开箱即用"的消费级体验。而 IronClaw 正通过 Wave 0 架构重构（移除通配重导出、目录迁移）走向**模块化/可组合**路线，NanoClaw 则在构建容器化、供应链安全强化（镜像签名验证、按需安装 CLI）的**交付物标准化**路线。

- **与差异化竞争者的差距**：
  - **稳定性信任赤字**：OpenClaw 的 P0 内存泄漏（53 天未修复）、多个 P1 问题积压 5 个月，正在侵蚀其"生产可用"的信用。相比之下，IronClaw 对安全问题标注 suggested_P0/P1 并立即响应（#6900/#6866），NanoBot 在 24 小时内集中关闭 5 个 P1 回归修复，反映了更高效的问题响应机制。
  - **工程纪律对比**：IronClaw 的架构重构采用"先基线后迁移+shrink-only 棘轮"的度量护栏策略，ZeroClaw 的 Webhook 鉴权修复采用 fail-closed 原则，而 OpenClaw 在数据完整性类问题（#40001 write 覆写、#48810 孤儿 fork）连续出现同类事故，工程治理明显滞后于其社区规模。
  - **生态互操作方向**：ZeroClaw 的 OpenAI Chat Completions 兼容适配器（#8603/#8550）与 Hermes Agent 的 MCP HTTP 服务托管（#43633）均向"开放协议"方向演进，而 OpenClaw 的 Codex 交互模式对齐（#102261）更多是"对齐上游模型体验"，缺乏双向互操作主动性。

**结论**：OpenClaw 仍是生态的**用户入口与场景定义者**，但若不解决稳定性债务和合并管线积压，其"参照系"地位可能被 IronClaw（架构质量）、ZeroClaw（互操作标准）等蚕食。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|---------|---------|
| **会话状态隔离与消息分发控制** | OpenClaw、Hermes Agent、CoPaw、NanoClaw | ① 工具调用间内部文本泄漏到消息渠道（OpenClaw #25592）；② 后台记忆/上下文与用户主动输入的边界（Hermes #31584）；③ 多会话 UI 数据完整性与指令漂移（CoPaw #6558）；④ 定时任务回复路由错误（NanoBot #3106）；⑤ 渠道无关的会话管理命令缺失（PicoClaw #3307） |
| **安全边界与凭据隔离** | OpenClaw、Hermes Agent、Moltis、ZeptoClaw、ZeroClaw、NanoClaw | ① 子进程环境变量继承导致凭据泄露（ZeptoClaw #645）；② Vault 端点缺少认证（Moltis #1177）；③ Webhook 鉴权可绕过（ZeroClaw #9565）；④ Teams 插件导入副作用加载 .env 破坏配置隔离（Hermes #62935）；⑤ 权限剥离回归（OpenClaw #51396）；⑥ 镜像签名验证形同虚设（NanoClaw #3158） |
| **成本治理与资源配额** | OpenClaw、Hermes Agent、IronClaw | ① 每代理 token 成本上限（OpenClaw #42475）；② 工具失败无限重试放大成本（Hermes #32827）；③ 网关内存泄漏导致资源失控（OpenClaw #91588）；④ Exec 会话输出内存上界（NanoBot #5150） |
| **多代理编排与资源隔离** | OpenClaw、IronClaw、NanoClaw、CoPaw | ① 子代理完成后扩展钩子/通知（OpenClaw #22358/#27445）；② 同一 agent-group 容器重复生成（NanoClaw #3119）；③ 跨用户内存泄漏（IronClaw #6900）；④ 父会话审批级别未被子会话继承（CoPaw #6506） |
| **MCP 生态集成** | OpenClaw、PicoClaw、CoPaw、Hermes Agent、Moltis | ① OAuth 2.1 认证支持（PicoClaw #3302 反复提交）；② MCP 服务器重启后客户端无法自动恢复（CoPaw #6524）；③ 工具名非法字符破坏 OpenAI 兼容 API（CoPaw #6557）；④ MCP HTTP 服务托管与认证（Hermes #43633） |
| **提示缓存与上下文管理** | OpenClaw、NanoBot、ZeroClaw | ① 提示缓存在多个边界丢失（OpenClaw #102175）；② 上下文压缩持久化（NanoBot #5172）；③ 对话历史与长期记忆分离（ZeroClaw #9048）；④ 工具调用格式泄漏到 LLM 摘要（PicoClaw #3279） |
| **本地模型与轻量化部署** | OpenClaw、PicoClaw、NanoBot、CoPaw、ZeroClaw | ① Ollama thinking level 保留（OpenClaw #116584）；② LM Studio 引导流程改进（OpenClaw #116606）；③ 在 $10 硬件上运行、<10MB RAM（PicoClaw #3308 用户评价）；④ Termux 平台时区问题（NanoBot #5187）；⑤ 本地模型流式输出误读为日志（ZeroClaw #9325） |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 | 核心差异化 |
|------|---------|---------|---------|-----------|
| **OpenClaw** | 全功能个人 AI 助手，多渠道消息代理 | 大众消费者、自动化重度用户 | 单体 + 广泛渠道适配 | 渠道覆盖面最广、社区规模最大、功能迭代最快 |
| **Hermes Agent** | 企业级 Agent 服务器、MCP/技能生态 | 开发者、企业内部部署 | 模块化、配置驱动，支持多种协议 | 强调安全边界（配置隔离、记忆安全）与企业级集成（Teams/Feishu/企业微信） |
| **IronClaw** | 大规模多租户部署、安全隔离 | 企业/团队级、多用户部署 | Rust 模块化，目标架构 Wave 0 重构中 | 强调多用户隔离、SSO、部署安全，重视工程质量与度量 |
| **NanoClaw** | 容器化、供应链安全、镜像分发 | 运维、有部署标准化需求的组织 | 容器优先、镜像签名验证、按需安装 | 供应链安全与镜像体积优化是最大标签 |
| **CoPaw (QwenPaw)** | 消费级 AI 助手，强 UI/UX 打磨 | 大众用户、中文社区 | Python 单体 + Web/桌面 UI | 依托 Qwen 生态，注重桌面端体验与多模态（computer-use） |
| **LobsterAI** | 桌面应用、企业版多账户隔离 | 桌面端用户、企业客户 | Electron/Tauri + 多平台 | 企业版账户隔离、活动运营体系（签到）、Windows 安装体验 |
| **ZeroClaw** | 本地优先、互操作标准 | 隐私敏感用户、本地模型部署者 | 本地模型优先 + OpenAI 兼容适配器 | 强调本地隐私、生态互操作（Open WebUI/LobeChat） |
| **NanoBot** | 轻量级会话代理（Telegram/WhatsApp） | Telegram/WhatsApp 重度用户 | Python 轻量架构，SQLite 迁移中 | 轻量、部署简单、回归修复节奏快 |
| **Moltis** | 多平台渠道代理 + 可观测性 | 需要监控反馈的部署者 | 中等复杂度，插桩/OTLP 支持 | 可观测性/反馈收集基础设施是差异化亮点 |
| **PicoClaw** | Go 语言、极轻量、低资源占用 | 嵌入式/低配硬件爱好者 | Go 原生，<10MB RAM | 极致轻量化、亚秒级启动，面向 $10 硬件场景 |
| **ZeptoClaw** | 运行时安全与进程管理 | 关注安全性的开发者 | 关注运行时凭据隔离与进程资源管理 | 安全边界+资源生命周期管理是核心价值 |

---

## 6. 社区热度与成熟度

### 第一梯队：极高度活跃、快速迭代期（日均 >50 条更新）

- **OpenClaw**：功能迭代速度最快，但稳定性债务累积、合并管线积压严重，处于"高产出高风险"阶段。社区讨论质量高（深度问题/复现细节），但维护者响应速度与问题积压不成正比。
- **IronClaw**：架构重构与功能推进并行的关键转型期，社区互动集中在 Epic 层面，工程质量意识强。处于从"功能可用"向"体验稳定"过渡。
- **CoPaw**：UI/UX 打磨与核心功能扩展同步，维护者响应快（当日合并多个修复），社区反馈集中但正循环。
- **ZeroClaw**：高活跃但合并为 0，处于"提交爆发-合并瓶颈"的危险区间。社区对架构级 RFC 关注度高，但执行层滞后。

### 第二梯队：中高活跃、质量巩固期（日均 10-50 条更新）

- **NanoBot**：回归修复集中收尾 + 架构升级（SQLite）推进中，项目健康度良好，响应速度稳定。
- **Hermes Agent**：v0.19.1 发布后 PR 队列清理中，维护者积极处理撤回/重复 PR。社区讨论集中于安全边界与配置体验。
- **NanoClaw**：安全加固与镜像优化并进，问题与修复同步推进的良性循环，社区贡献者持续活跃。

### 第三梯队：中等活跃、生态补充期（日均 <10 条更新）

- **Moltis**：安全修复、可观测性、渠道增强三线并进，处于从功能开发转向运维体系建设的过渡期。
- **PicoClaw**：功能请求持续涌现（OAuth 2.1 反复提交）但合并节奏慢，面临贡献者热情流失风险。
- **LobsterAI**：高效的合并主导型项目，核心团队驱动为主，社区外部贡献占比较低。

### 第四梯队：低频活跃、等待关键决策期（日均 ≤1 条更新）

- **ZeptoClaw**：唯一的核心安全修复 PR 等待 8 天无评审，社区响应速度是最大短板。
- **NullClaw / TinyClaw**：无活动，处于休眠期。

---

## 7. 值得关注的趋势信号

### 信号一：安全边界成为"默认要求"而非加分项

2026-07-31 单日，**6 个活跃项目**同时报告了安全相关缺陷（OpenClaw 权限回归、Hermes 配置隔离破坏、Moltis Vault 未认证、ZeptoClaw 凭据泄露、ZeroClaw Webhook 绕过、NanoClaw 签名验证失效）。这一密度表明：**安全不再是各自为战的孤立议题，而是决定用户是否将数据委托给 Agent 的底线能力**。对开发者而言，应在架构设计之初就将"最小权限 + 凭据隔离 + 认证强制 + fail-closed 默认"作为不可协商的工程纪律。

### 信号二：会话状态管理的"同一困境"正在跨项目复制

OpenClaw 的文本泄漏（#25592）、Hermes 的记忆权威性争议（#31584）、CoPaw 的会话数据完整性（#6558）、NanoBot 的回复路由错误（#3106）——**四个项目在同一个根本问题上各自挣扎**：Agent 的"内部状态"与"外部可见行为"之间缺少标准化的分层机制。这一反复出现的困境表明，Agent 的会话模型需要从"单一消息流"演化为"多层级上下文（内部推理/外部回复）的显式分离"。这是开源社区产生通用解决方案（如 IP-AGENT 消息协议或新的上下文框架）的机会窗口。

### 信号三：成本感知从"运维烦恼"升级为"架构决策依据"

OpenClaw 的每代理成本预算（#42475）、Hermes 的无限重试成本放大器（#32827）、NanoBot 的 Exec 输出内存上界（#5150）、PicoClaw 的提示缓存降本（#3163）——**成本治理正在从 UI 层面的显示指标走向运行时架构的硬约束**。未来的 Agent 框架需要在"任务完成度"与"资源消耗"之间建立量化的博弈平衡，而不仅是事后贴账单。这对设计长任务执行（auto-run、cron、子代理编排）的开发者尤为重要。

### 信号四：MCP 生态的"最后一公里"问题浮现

OAuth 2.1 支持反复提交（PicoClaw #2546→#3302）、服务器重启后客户端不自动恢复（CoPaw #6524）、工具名非法字符破坏 API 兼容性（CoPaw #6557）、MCP HTTP 服务托管（Hermes #43633）——MCP 作为 Agent 工具互操作标准已进入广泛采用期，但**认证、健壮性、开放访问**三个 layer 仍不成熟。这是为 MCP 生态提供基础设施（代理/网关/认证服务）的创业或贡献窗口。

### 信号五：本地模型与轻量化从"边缘尝试"走向"主流分支"

OpenClaw（Ollama/LM Studio 专项修复）、NanoBot（Termux 支持）、ZeroClaw（本地模型流式输出修复）、PicoClaw（$10 硬件运行）、CoPaw（本地模型需求）——**本地优先已不再是极客爱好者的副线，而是用户对隐私、成本和离线可用性的明确要求**。尤其是 ZeroClaw 报告"本地小模型将用户输入误读为日志"的问题，揭示了 Agent 框架在"模型行为差异"适配上的不足。对开发者而言，支持"一个框架适配从云端旗舰到本地 3B 模型的全部光谱"将是差异化竞争力。

### 信号六：多代理编排的资源治理成为新战场

IronClaw 的跨用户内存泄漏（#6900）、NanoClaw 的容器重复生成（#3119）、CoPaw 的子会话权限继承断裂（#6506）、OpenClaw 的子代理完成通知（#22358/#27445）——**"多代理协作"正从概念走向生产实践，但资源隔离、状态继承和生命周期管理的标准化解决方案尚未出现**。这将是继"渠道适配"之后的下一轮框架竞争焦点。

---

## 结语

个人 AI 助手开源生态在 2026 年中已从"百花齐放的探索期"进入"质量与治理的分化期"。OpenClaw 的社区规模仍然是无可争议的流量中心，但 IronClaw 的工程纪律、ZeroClaw 的互操作野心、Moltis 的可观测性投入、PicoClaw 的资源效率等差异化路线正在为生态建立多样化的生存策略。对于技术决策者，**短期内关注 OpenClaw 合并管线疏通与 P0 修复进度**，**中期跟踪 IronClaw 的 Wave 0 架构落地与 ZeroClaw 的 OpenAI 兼容适配器**，**长期把握"会话状态分层""成本硬约束""安全默认优先""MCP 基础设施"四个趋势性机会**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**报告日期**: 2026-07-31  
**数据区间**: 2026-07-30 至 2026-07-31（部分历史数据回溯）

---

## 1. 今日速览

项目在过去24小时内保持了较高的社区活跃度，共产生7条Issue更新（5条新开/活跃、2条关闭）和50条PR更新（17条待合并、33条已合并/关闭），无新版本Release发布。核心开发集中于修复**Telegram轮询静默挂死**（#5171）、**Termux平台时区数据库缺失**（#5187）、**WebUI Quick Chat功能落地**（#5181/#5182/#5184）等关键问题。值得关注的是，一批高优先级（P1）回归修复PR（#5136、#5145、#5147、#5150、#5151）在今日集中关闭，标志着上一轮稳定性问题的修复已进入收尾阶段；同时一项**将会话存储从JSONL迁移至SQLite的重大架构变更**（#5173）已提交待审，预计将对项目后续扩展性产生深远影响。当前未见阻塞性风险或社区争议，整体项目健康度良好，合并节奏保持稳定。

---

## 2. 版本发布

**无新版本发布**（最新Release暂无更新）。  
近期值得关注的、可能纳入下一版本的能力已在PR阶段活跃：包括SQLite会话存储迁移（#5173）、Telegram自定义Bot API地址（#4919）及WebUI Quick Chat（#5184）等。建议维护者关注上述PR合并进度，评估是否纳入下一版本规划。

---

## 3. 项目进展

今日共合并/关闭33个PR，重点进展如下：

### 🎯 核心稳定性修复（本批回归修复全部关闭）
- **[#5136] `finish_reason='length'` 空白内容错误路由修复**（P1，合并）— 修复当LLM响应因长度截断且携带工具调用时，错误触发空响应重试而非长度恢复的逻辑。关联Issue #5133。
- **[#5150] Exec会话输出内存上界约束**（P1，合并）— 对stdout/stderr保留固定头部/尾部预算，防止长任务输出导致内存膨胀。
- **[#5151] 空闲会话锁释放**（P1，合并）— 采用 `WeakValueDictionary` 存储会话锁，避免长期运行进程中锁对象累积导致的内存泄漏。
- **[#5147] 配对审批在存储瞬时故障下保留**（P1，合并）— 修复 `pairing.json` 读取瞬时失败时误清空全部已批准发送者的问题。
- **[#5145] CI稳定化与加速**（P1，合并）— 用stdin门控就绪握手替代依赖时序的exec会话超时测试，并批量安装渠道依赖。

### 🆕 功能推进
- **[#5172] 保留Responses推理状态与上下文压缩**（合并）— 采纳OpenAI ARC-AGI-3报告中两项Responses API能力：完整保留回放加密推理项等不透明输出项链，并实现上下文压缩持久化。
- **[#5181] WebUI持久化Quick Chat入口**（合并）— 新增固定WebSocket会话的Quick Chat入口，不混入常规主题列表。
- **[#5182] WebUI侧边栏选中态复用重构**（合并）— 统一顶层导航、会话、设置的选中高亮逻辑，为Quick Chat铺路。

### 🚧 待合并关键PR
- **[#5173] 会话存储从JSONL迁移至SQLite**（新提交）— 使SQLite成为唯一运行时会话存储，首次启动事务性导入旧JSONL文件，保留JSONL作为回滚备份。涉及迁移策略，建议维护者重点评审数据安全与回滚方案。

---

## 4. 社区热点

- **[#5185] Nanobot在响应中返回工具调用代码**（新开1天，1评论，截图附证）— 用户报告模型突然开始将工具调用代码直接输出在回复中，而非正确执行。该问题当前无明确复现步骤，可能涉及模型行为变化或解析逻辑回归，建议优先排查近期合并的PR #5136是否引入相关副作用。

- **[#5171] Telegram轮询静默挂死且永不恢复**（新开1天，0评论，已有修复PR）— 用户在生产环境观察到网络抖动后轮询永久停止、日志无任何输出、消息在服务端堆积。该问题与PR #5156（Telegram轮询自愈，今日待合并）直接对应，用户诉求与修复方案匹配度极高，建议优先推进合入。

- **[#5149] WhatsApp无法发送音频消息**（新开3天，3评论）— 用户反馈可正常接收但无法发送音频文件，日志提示 `neonize.utils.ffmpeg WARNING`，疑似格式转换或编码路径问题。当前无明确修复PR，建议维护者定位ffmpeg调用链，确认是否有已知依赖版本不兼容。

---

## 5. Bug 与稳定性

高优先级（影响面广/阻断使用）：

| 严重程度 | Issue/PR | 说明 | 修复状态 |
|---------|----------|------|---------|
| 🔴 高 | [#5171] Telegram轮询静默挂死 | 瞬时网络故障后轮询永久停止且无日志输出，进程存活但消息不再接收 | **已有修复PR [#5156]待合并** |
| 🔴 高 | [#5187] Termux平台启动失败 | 时区数据库缺失导致配置校验失败（`timezone` 校验错误），无法启动`webui` | **已有修复PR [#5189]待合并** |
| 🟠 中 | [#5185] 响应中返回工具调用代码 | 模型输出中出现工具调用代码而非执行结果，影响用户体验且无明确复现路径 | 无修复PR，需排查 |
| 🟠 中 | [#5149] WhatsApp无法发送音频 | 可接收不可发送，ffmpeg警告出现于日志中，涉及完整音频链路 | 无修复PR，需定位 |
| ⚪ 待观察 | [#3106] 定时任务工具调用完成但无最终回复 | 集中出现在gpt模型配置中，gml-4.7不受影响，可能与模型差异或超时设置相关，持续观察中 | 无修复PR，建议验证 |

---

## 6. 功能请求与路线图信号

- **会话存储架构升级（高信号）**: PR [#5173]提出将JSONL迁移至SQLite，可显著提升并发读取、会话管理与数据完整性能力，并为后续Dream剪枝等功能提供更可靠支撑。该变更涉及数据迁移，建议纳入下一版本并在Changelog中提供明确迁移指引。

- **Telegram自定义API地址（持续活跃）**: PR [#4919]（项目14天）支持接入自建Bot API或企业网关。该PR已标记P2优先级且在持续更新，建议维护者明确表示接纳意愿并推动评审，避免长期悬置消耗社区热情。

- **WebUI Quick Chat + 临时会话（新方向）**: PR [#5184]同时加入持久化Quick Chat与仅内存历史的Temporary Chat，配合今日已合并的#5181/#5182，表明WebUI交互形态正从纯会话列表转向更灵活的多模态入口。

---

## 7. 用户反馈摘要

- **生产环境网络韧性诉求强**: Issue #5171反馈者描述"不稳定的代理"直接导致Telegram机器人永久失联，强调了对通道层自愈能力的强烈需求；#4791（已关闭）也从Dos维度提出了限速需求，表明用户对通道层健壮性关注度持续走高。

- **平台兼容性预期提升**: #5187中用户"为什么不在Termux里试试？"的表述反映了社区对移动端/轻量环境运行AI助手的好奇与期待，时区问题的修复虽是小事，但直接影响新用户的第一印象。

- **功能迭代速度与稳定性平衡**: #5185"突然开始"的表述在多个Bug报告中高频出现（如#5149的"will not send"），用户对模型行为变化的敏感性提示项目在快速迭代中需加强回归测试覆盖，尤其是涉及LLM响应解析链路的核心逻辑。

---

## 8. 待处理积压

以下PR存在**合并冲突**，已标记 `conflict` 状态，长期未合入，请维护者关注：

- **[#4551] 心跳共享会话配置**（42天，冲突）— 为Heartbeat添加 `isolated_session` 配置，关闭时共享目标渠道会话。功能最终形态较明确（实现#1899），建议解决冲突后推进合入。
- **[#4819] 会话锁弱引用替换**（25天，冲突）— 将 `WeakValueDictionary` 替换为普通dict，修复锁被GC提前回收的并发隐患。注：该修复与今日合并的#5151目的一致（均针对会话锁），建议评估两者关系，考虑关闭其中一个以避免重复修复。

其他长期未响应Issue：

- **[#3106] 定时任务完成但无最终回答**（已开放3个月+）— 使用gpt模型配置定时任务，工具步骤完成却无最终回复。近期有更新但无维护者反馈，建议明确是否为模型行为差异或需新增重试/恢复策略，避免用户等待过久。

---

*报告完毕。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-31

> **报告周期：** 2026-07-30 至 2026-07-31 | 数据来源：NousResearch/hermes-agent GitHub 仓库
> **关键提醒：** 本报告由 AI 智能体与个人 AI 助手领域开源项目分析师自动生成。其核心受众是 AI Agent 领域的研发人员、技术决策者与项目维护者，故在样本选择与解读上更侧重于代码架构、安全边界与协议实现，而非产品运营维度。

---

## 1. 今日速览

Hermes Agent 项目在 7 月 30 日至 31 日的 24 小时内保持了**高强度的活跃度**：共更新 50 条 Issue 和 50 条 PR，并发布了一个重要的补丁版本 v0.19.1（合并自 v0.19.0 以来的 1,000+ PR）。社区讨论集中在**会话状态隔离**（session-state hygiene）、**配置安全边界**（profile secret isolation）与 **Windows 兼容性** 三个技术深水区，反映出项目在上游依赖推进与多平台适配过程中的阵痛。值得关注的是，今日关闭的 PR 中有一半标记为 "Retracted"（作者撤回）或 "Duplicate"（重复），说明维护者正在积极清理重复工作、压缩 PR 队列。整体而言，项目处于**高频迭代、社区参与度高、但需警惕技术债累积**的健康活跃状态。

---

## 2. 版本发布

### v2026.7.30 — Hermes Agent v0.19.1

- **类型：** Patch Release
- **核心内容：** 将 v0.19.0 以来的约 1,000+ 个 PR 汇总为一个稳定标签，面向下游消费者（Docker 镜像、托管部署、全新安装）。
- **无破坏性变更。** 官方未在 release notes 中提及任何迁移注意事项或行为变化，定位为纯稳定性收口版本。

> **分析师注：** 该版本是"滚动发布"策略的体现。对于依赖 pip/GitHub 直接拉取的用户，建议关注 v0.19.1 是否包含近期重要的 bug fix（如 `桌面应用更新器 PID 误判` 问题），若缺失可暂时维持 main 分支跟踪。

---

## 3. 项目进展（今日合并/关闭的 PR）

今日仅关闭了 3 个 PR，其中一个为作者撤回，另一个为重复提交，实际合并进度有限。但结合 Release 收口的背景，可以判断项目在**短期收敛 PR 队列、稳定主干**：

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#75105](https://github.com/NousResearch/hermes-agent/pull/75105) | fix(mcp): recover cached server after terminal OAuth startup failure | CLOSED (已合并) | 修复 MCP 服务器在终端 OAuth 启动失败后缓存未清除、导致后续发现流程停滞的问题。**这是今日唯一技术性合并。** |
| [#75113](https://github.com/NousResearch/hermes-agent/pull/75113) | Retracted | CLOSED (撤回) | 作者主动撤回，未提供理由。 |
| [#75103](https://github.com/NousResearch/hermes-agent/pull/75103) | fix(kanban): throttle repeated same-reason respawn_guarded events | CLOSED (标记为 duplicate) | 与 [#41805](https://github.com/NousResearch/hermes-agent/issues/41805) 对应的修复有重复提交，统一到另一条 PR 中。 |

**进展评估：** 今日合并量偏低属正常波动。建议关注 [#75103](https://github.com/NousResearch/hermes-agent/pull/75103) 的对应主线 PR 是否已进入合并队列，以及今日大量 OPEN 的 PR 后续合并速度。

---

## 4. 社区热点（高讨论量议题）

以下议题今日获得了最高的评论热度（评论数 ≥ 4），反映了社区的核心关注点：

### #31584 — [Feature]: 将 memory-context 视为后台上下文，而非权威用户消息内容
- **链接：** [Issue #31584](https://github.com/NousResearch/hermes-agent/issues/31584)
- **评论数：** 10 | **创建：** 2026-05-24
- **热度理由：** 涉及 Agent **记忆安全与提示词注入** 的核心机制。用户要求区分"后台记忆"与"用户主动输入"，避免恶意记忆污染指令。
- **分析：** 该议题已开放 2 个月，评论数持续增长，说明其设计讨论仍未收敛。与 #39372（后台运行污染会话列表）属同类关切——**会话与记忆的边界隔离**已是社区公认的架构级痛点。

### #37968 — fix(cron): 隔离网关审批与环境污染
- **链接：** [Issue #37968](https://github.com/NousResearch/hermes-agent/issues/37968)
- **评论数：** 8 | **创建：** 2026-06-03
- **热度理由：** 提交者给出 CVSS v3.1 6.3 / v4.0 7.0 的评级，指出 cron 调度在网关审批时环境变量污染存在**完整性破坏**风险（C:N/I:H/A:N）。
- **分析：** 该 Issue 标题以 `fix(cron)` 开头，疑似由维护者或机器人发出，但 `needs-decision` 标签表明尚未定论。建议关联 #75101（cron 执行台账作用域修复 PR）查看是否覆盖此问题。

### #74942 — 桌面应用更新器 PID 误判（Windows）
- **链接：** [Issue #74942](https://github.com/NousResearch/hermes-agent/issues/74942)
- **评论数：** 5 | 👎: **2（今日新增）** | **创建：** 2026-07-30
- **热度理由：** 新提交 bug，影响 Windows 用户更新流程。更新引导程序在检查 PID 时将自己识别为"另一个运行实例"，导致更新中断。评论中的 👎 表明用户对此体验不满。
- **分析：** 这是今日新开 Issue 中热度与负面反馈最高的一条，优先关注 Windows 平台的 P1 级问题。

### #67347 / #27804 / #72269
- 均积累了 4–5 条评论，分别涉及 **子代理模型配置引导**、**邮件网关主题隔离** 与 **技能自改进的失败误判**，反映用户对配置友好性与平台插件的行为边界期待较高。

---

## 5. Bug 与稳定性

以下为按严重程度（P1 > P2 > P3）与修复状态排列的今日活跃 Bug 清单：

| 严重级 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| **P1** | [#74942](https://github.com/NousResearch/hermes-agent/issues/74942) | Windows 桌面更新器 PID 误判自身为新实例 | **暂无 fix PR**，高优关注 |
| **P2** | [#72269](https://github.com/NousResearch/hermes-agent/issues/72269) | 后台自改进审查可将未解决失败写成已验证技能 | 暂无 |
| **P2** | [#62935](https://github.com/NousResearch/hermes-agent/issues/62935) | Teams 插件导入副作用加载外部 .env 破坏配置隔离 | 暂无 |
| **P2** | [#62401](https://github.com/NousResearch/hermes-agent/issues/62401) | Matrix 网关在 macOS arm64（E2EE 关闭）被强制构建 python-olm | 暂无 |
| **P2** | [#32827](https://github.com/NousResearch/hermes-agent/issues/32827) | 工具失败警告升级机制缺失，允许无限重试放大成本 | 暂无 |
| P3 | [#74570](https://github.com/NousResearch/hermes-agent/issues/74570) | 桌面端 pin/unpin 被 pullRemotePins 竞态撤销 | 暂无 |
| P3 | [#33485](https://github.com/NousResearch/hermes-agent/issues/33485) | CLI 关闭时 Honcho 混合记忆线程导致 SIGABRT | 暂无 |
| P3 | [#29667](https://github.com/NousResearch/hermes-agent/issues/29667) | 企业微信 WebSocket 提前断开致静默投递失败 | 暂无 |
| P3 | [#43186](https://github.com/NousResearch/hermes-agent/issues/43186) | 并发子进程退出时偶发 SIGABRT | 暂无 |

**汇总：** 今日没有出现崩溃级（core dump）**新** Bug，但多处进程退出时的 SIGABRT 类问题（#33485、#43186）已累积，暗示在某些内存/子进程生命周期管理上存在系统性薄弱点。**尚无对应 fix PR 针对上述任一 P2 级问题。**

---

## 6. 功能请求与路线图信号

以下功能请求在今日活跃，结合已有 PR 预测其未来合并可能性：

| 功能请求 | 对应 PR / 信号 | 纳入下一版本可能 |
|---|---|---|
| [#34823](https://github.com/NousResearch/hermes-agent/issues/34823): 语义/按消息粒度技能检索 | 无直接 PR，但实验性 `semantic_retrieval` 已存活代码库 | 中。900+ token 成本节省为强需求 |
| [#67347](https://github.com/NousResearch/hermes-agent/issues/67347): 子代理模型/供应商引导选择器 | 无直接 PR | 中高。UI 相关，社区呼声较强 |
| [#46467](https://github.com/NousResearch/hermes-agent/issues/46467): macOS TUI 拷贝-选中配置开关 | 无直接 PR | 中。纯配置项，实现成本低 |
| [#48683](https://github.com/NousResearch/hermes-agent/issues/48683): 技能创建 Issue/PR 时检查仓库模板 | 无直接 PR | 高。与 `github-*` skills 迭代路径吻合 |
| [#53849](https://github.com/NousResearch/hermes-agent/pull/73849): `hermes serve` 支持多 `--host` 双栈绑定 | **有对应 PR** #73849（开放中） | 高。用户已提出，有现成实现 |

**核心结论：** 目前没有将 Issue 请求硬编码进 v0.19.1 的明确迹象。路线图偏向于**稳定性与安全修复**，功能请求预计在 v0.20 或之后按 PR 合并节奏放量。

---

## 7. 用户反馈摘要（来自今日 Issue 评论）

- **记忆安全的普遍焦虑：** 在 #31584 中，用户 `telnetdoogie` 明确表示意识到"记忆作为权威指令"可能被恶意利用的威胁面，这是 **Agent 安全心智成熟** 的信号，也呼应了 #72269 中"技能误信失败"的同类关切。社区已开始要求**改变 Agent 的认知基石**（而非仅修 bug）。
- **平台适配的挫败感：** #62401（Matrix 在 macOS arm64 不可用）与 #74942（Windows 更新器误判）直接打击了用户"装完即用"的预期，部分用户评论倾向转向"这项目只在 Linux 上跑得好"的结论，建议维护团队对 Windows/macOS 的安装与更新流程做一次专项体验巡检。
- **成本敏感的开发者：** #32827（无限重试放大成本）与 #53413（Dashboard 空白区域）评论中，用户多次出现"billing"、"cost"、"quota"词汇，显示在工具被高频集成的场景下，**成本控制与资源配额透明度**是决定用户是否长期依赖 Hermes 的关键因素。
- **积极反馈：** #43024（liteparse PDF 回退）与 #43633（MCP HTTP 认证服务）的评论表示期待，认为这些扩展使 Hermes 向"**私人 Agent 服务器**"方向演进，是正确路径。

---

## 8. 待处理积压（请维护者关注）

| 类型 | 编号 | 标题 | 标签 | 关键原因 |
|---|---|---|---|---|
| Issue | [#27804](https://github.com/NousResearch/hermes-agent/issues/27804) | 邮件网关主题隔离缺失，通知量大 | P3 | 开放 2.5 个月，累计评论 5+，但始终无维护者表态 |
| Issue | [#33485](https://github.com/NousResearch/hermes-agent/issues/33485) | CLI 退出时 SIGABRT | P3 | 涉及 Honcho 混合记忆的进程关闭逻辑，有风险倾向，但无优先级提升或修复指派人 |
| PR | [#18131](https://github.com/NousResearch/hermes-agent/pull/18131) | Feishu 工具客户端构建自环境凭据 | P2 | 创建于 2026-05-01，至今开放 3 个月未合并，也未关闭，长期僵持 |
| PR | [#43633](https://github.com/NousResearch/hermes-agent/pull/43633) | MCP HTTP 服务托管与认证 | P3 | 开放 1.5 个月，代码完整但无维护者 Review 记录 |

**分析师建议：** 上述 4 项均属于"要么推进、要么关闭"的状态。长期挂起会降低社区贡献者的积极性。尤其是 #43633 的 MCP HTTP 服务与 #18131 的 Feishu 修复，如确认暂不合并，应明确告知贡献者原因或下一步预期。

---

*报告结束。本报告基于公开 GitHub 数据自动生成，未与维护者直接沟通确认，部分结论为分析师推断，仅供参考。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**报告日期：2026-07-31** | **数据周期：2026-07-30 至 2026-07-31**


## 1. 今日速览

PicoClaw 在过去 24 小时内保持了中高活跃度：共产生 7 条 Issue 更新（4 条新开/活跃，3 条已关闭）和 17 条 PR 更新（12 条待合并，5 条已合并/关闭）。值得注意的是，今日新开了 3 条功能请求（#3302 OAuth 2.1、#3307 Telegram session 管理、#3308 代码审查建议），且昨天刚有同主题的 OAuth issue（#2546）被关闭，显示社区对 MCP 认证支持仍有持续需求。依赖更新 PR 集中提交（AWS SDK、Anthropic SDK 等）表明维护者正在积极跟进上游版本。未发布新版本，整体项目健康度良好，但部分功能请求等待较久（如 #2546 从提出到关闭历时 3.5 个月）。


## 2. 版本发布

本报告周期内无新版本发布。


## 3. 项目进展

今日共 5 个 PR 被合并或关闭，主要进展集中在以下方面：

**基础设施与 CI 更新（已合并/关闭）：**
- [#3262 `actions/setup-go` v6 → v7](https://github.com/sipeed/picoclaw/pull/3262) 和 [#3263 `actions/setup-node` v6 → v7](https://github.com/sipeed/picoclaw/pull/3263)：CI 工具链升级至主版本，跟随 GitHub Actions 生态更新
- [#3263 等其他 5 个 PR 关闭]：依赖维护例行更新

**AWS SDK 相关 PR（已合并/关闭）：**
- [#3290 aws-sdk-go-v2/config 1.32.25 → 1.32.31](https://github.com/sipeed/picoclaw/pull/3290)：AWS 配置 SDK 例行更新
- [#3288 aws-sdk-go-v2/service/bedrockruntime 1.53.3 → 1.56.0](https://github.com/sipeed/picoclaw/pull/3288)：Bedrock Runtime SDK 更新，为 Bedrock 相关功能提供新 API 支持

**AWS Bedrock 提示缓存功能（已合并）：**
- [#3163 feat(bedrock): leverage Converse prompt caching via cache points](https://github.com/sipeed/picoclaw/pull/3163)：实现 AWS Bedrock Converse API 的提示缓存（cache points），可将前缀缓存使读取成本降至约 0.1× 输入，写入成本约 0.2×。此功能对使用 Bedrock 的用户可显著降本，尤其适合长上下文的场景

**已关闭的 PR（含未合并）：**
- 多个 Dependabot 自动 PR 被关闭（对应更新的替代版本已提交）

> **整体判断**：今日合并的 PR 中，最值得关注的是 Bedrock prompt caching（#3163），这是对 AWS 用户有实际成本收益的功能改进。其余为依赖维护，属于例行健康维护。


## 4. 社区热点

今日讨论最活跃的条目：

**OAuth 2.1 支持需求高涨（最热门主题）**

[#2546 [CLOSED] Support OAuth 2.1 + PKCE for MCP servers（已关闭，6 评论）](https://github.com/sipeed/picoclaw/issues/2546) 是过去一段时间内最受关注的功能请求——目标是让非技术用户从 dashboard 粘贴 URL 即可添加 OAuth 保护的 MCP 服务器，与 Claude.ai 的 "Add connector" 体验对齐。该 issue 历经 3.5 个月后在此周期被关闭（可能已被纳入路线图或其他形式处理）。

但值得注意的是，同一天新开了 [#3302 [OPEN] Support OAuth 2.1 for MCP servers same as #2546](https://github.com/sipeed/picoclaw/issues/3302)，说明社区对该功能的需求并未消失。两次提交（#2546 和 #3302）之间可能存在关联，也可能 #2546 因 stale 被自动关闭而社区再次提交。

**Telegram 会话管理需求（今日新开）：**

[#3307 [Feature] session list/switch command for Telegram (and other chat channels)](https://github.com/sipeed/picoclaw/issues/3307) 提出 Web UI 已有完整的会话管理（列出、切换、删除），但 Telegram 等聊天渠道缺少同等能力。这指向一个明显的产品缺口：渠道一致性。

**代码质量审查建议（今日新开）：**

[#3308 [Code Review] Concurrency hazards, goroutine leaks, and memory/speed optimizations in SeaHorse, Channel Manager, and Hooks](https://github.com/sipeed/picoclaw/issues/3308) 提出对 SeaHorse、Channel Manager 和 Hooks 的并发安全、goroutine 泄漏及内存/速度优化建议。这类主动性审查对项目长期健康很重要。

> **需求诊断**：今日热点集中在 **MCP 生态集成**（OAuth）、**交互一致性**（Telegram 会话管理）和 **代码质量提升** 三个方向。


## 5. Bug 与稳定性

今日报告的新 Bug：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 中 | [#3308](https://github.com/sipeed/picoclaw/issues/3308) | 并发风险、goroutine 泄漏、内存/速度优化建议（SeaHorse、Channel Manager、Hooks） | OPEN，无 fix PR |
| 低 | [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息处理不佳：IRCv3 超过 512 字节的消息被客户端拆分后，PicoClaw 不能将其视作单一消息处理 | OPEN，无 fix PR |

已关闭的 Bug：
- [#3258 Process Hook before_tool modify not working](https://github.com/sipeed/picoclaw/issues/3258)：`decision` 字段被丢弃、`args` 因反序列化缺陷被误解析。已在 3 天前关闭。

> **判断**：今日无新开启的高严重性 Bug。#3308 是目前最值得关注的质量议题，虽为审查建议而非实际 bug 报告，但涉及并发安全和资源泄漏，建议维护者优先评估。


## 6. 功能请求与路线图信号

**今日新功能请求（4 条）：**

| Issue | 功能 | 潜在纳入可能性 |
|-------|------|---------------|
| [#3302](https://github.com/sipeed/picoclaw/issues/3302) | OAuth 2.1 支持 MCP 服务器（与 #2546 重复请求） | 高——#2546 已被关闭，但社区仍在要求，大概率会被纳入路线图 |
| [#3307](https://github.com/sipeed/picoclaw/issues/3307) | Telegram 等聊天渠道的 session 列表/切换命令 | 中——Web UI 已具备，渠道一致性是合理增强 |
| [#3308](https://github.com/sipeed/picoclaw/issues/3308) | 并发安全、性能优化 | 中——质量改进，需维护者评估优先级 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息（>512B）的整合处理 | 低——小众渠道，但功能合理 |

**与已有 PR 的关联判断：**
- [#3200 feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200) 仍在开放中（7 月 1 日创建，30 天未合并）。此 PR 为 Web UI 添加模型默认回退链配置，与当前模型快速迭代（#3271 更新 9 家提供商的默认模型名）高度协同，建议维护者加速 review。
- [#3270 DashScope TTS + WeChat 音频发送](https://github.com/sipeed/picoclaw/pull/3270) 和 [#3283 DingTalk 图片消息支持](https://github.com/sipeed/picoclaw/pull/3283) 均为渠道功能增强，体现社区对多渠道能力的持续投入。

> **路线图信号**：MCP 生态集成（OAuth 认证）是社区反复提及的核心需求；渠道功能一致性（Telegram/IRC）是第二优先级。


## 7. 用户反馈摘要

**来自 Issue 评论和描述的真实用户声音：**

1. **对 MCP OAuth 支持的诉求非常具体且场景明确**（#2546）：
   > "让非技术用户从 launcher dashboard 粘贴 URL 即可添加 OAuth 保护的 MCP 服务器——与 Claude.ai 的 'Add connector' 相同体验。适用于有公网 URL 的云 VM，无需 shell、无需 Node.js。"

2. **Gateway 模式缺少无状态/独立会话支持**（#3257，已关闭）：
   > "CLI 模式可以通过 `--session cli:some-unique-id` 创建全新会话，但 gateway 模式下会话 key 由 channel/chat 推导，无法无状态使用。"

3. **IRC 用户对消息语义的期望**（#3287）：
   > "IRC 默认限制 512 字节，超长消息会被客户端自动拆分。PicoClaw 需要理解这些片段是同一消息的一部分。"

4. **对 PicoClaw 的正面评价**（#3308）：
   > "构建一个原生 Go AI 助手，能在 $10 硬件上运行、<10MB RAM、亚秒级启动——这是非常了不起的成就！"

> **总体感受**：用户对 PicoClaw 的轻量化、低成本定位表示认可，核心不满集中在 **MCP 生态认证** 和 **多端一致性** 上，这两点也是贡献者最愿意投入的方向。


## 8. 待处理积压

**长期未响应/待关注的重要 PR：**

| PR | 主题 | 创建时间 | 等待天数 | 风险 |
|----|-----|---------|---------|------|
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): 可配置默认回退链 | 2026-07-01 | 30天 | 中——与模型快速迭代相关，延迟合并可能产生 merge conflict |
| [#3271](https://github.com/sipeed/picoclaw/pull/3271) | chore(providers): 更新 9 家提供商的默认模型名至 2026-07 最新 | 2026-07-20 | 11天 | 中——若不及时合并，模型名快速更新会导致文档/配置偏差 |
| [#3279](https://github.com/sipeed/picoclaw/pull/3279) | fix(seahorse): 防止工具调用格式泄漏到 LLM 摘要 | 2026-07-21 | 10天 | 低——bug fix，影响摘要质量 |
| [#3263 等 stale PR] | 多个依赖更新 PR 已标记 stale | 7月16日-23日 | 7-14天 | 低——Dependabot 自动管理 |

**长期未响应的重要 Issue：**

- [#3287 IRC 长消息支持](https://github.com/sipeed/picoclaw/issues/3287)：7 月 22 日创建，2 条评论，无维护者响应
- [#3257 无状态/无历史 gateway 会话](https://github.com/sipeed/picoclaw/issues/3257)：已关闭但需求仍存在，建议关注是否有后续

> **维护者提示**：建议优先 review #3200（30 天未合并容易 stale）和 #3271（模型名时效性强）。#3163 Bedrock prompt caching 刚合并，建议在 release notes 中突出此功能。


## 项目健康度小结

| 维度 | 状态 | 说明 |
|------|------|------|
| 活跃度 | 🟢 高 | 24h 内 7 Issues + 17 PRs，社区和 Dependabot 均活跃 |
| 响应速度 | 🟡 中 | 新 Issue 有当日响应，但部分 PR 等待时间偏长 |
| 代码质量 | 🟢 良好 | 社区主动提交 code review（#3308），说明开发者对质量有要求 |
| 社区需求匹配 | 🟡 有缺口 | OAuth 2.1 需求反复被提，需明确路线图 |
| 版本节奏 | 🟡 待观察 | 近期无发布，多个功能 PR 等待合入下一版本 |

**建议关注**：MCP OAuth 认证支持、Telegram 会话管理、模型默认回退链（#3200）、以及 9 家平台默认模型名的时效更新（#3271）。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-07-31

## 今日速览

NanoClaw 项目今日活跃度较高，24小时内产生2条新Issue和19条PR更新（其中7条已合并/关闭）。核心团队在容器安全加固、镜像优化和验证流程修复上密集提交，显示出对生产环境稳定性的持续投入。值得关注的是，新增Issue #3153暴露了平台消息ID处理缺陷，可能导致Slack等渠道的互动功能（reaction、编辑）完全不可用，而PR #3119则针对长期运行主机的容器重复生成问题提出了修复。整体来看，项目正处于安全加固与体验优化并行的活跃迭代期。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日共有 7 个 PR 被合并或关闭，关键进展如下：

### 已合并/关闭

**🔒 安全与供应链加固（核心团队主导）**
- **[PR #3160 - 重新锁定 agent 镜像至 hardened-2026-07-30](https://github.com/nanocoai/nanoclaw/pull/3160)**：将基础镜像从 `sha256:089ff730…` 更新至 `sha256:4e441375…`，镜像体积从 781MB 降至 611MB，层数从 18 层优化至 8 层。作者强调最大单层不再成为拉取瓶颈，显著改善了镜像分发效率。
- **[PR #3159 - Vercel CLI 改为按需安装](https://github.com/nanocoai/nanoclaw/pull/3159)**：将 Vercel CLI 从基础镜像中移除，改为由 `/add-vercel` 按需添加。这不仅减小了每个镜像的体积，更缩小了默认凭据暴露面，符合最小权限原则。

**🐛 核心功能修复**
- **[PR #3122 - opencode 技能兼容性修复](https://github.com/nanocoai/nanoclaw/pull/3122)**（已关闭）：修复了 opencode 技能与 main 分支的兼容性问题，包含自定义端点传输和内存对等性修复。
- **[PR #3014 - 修复 hasIdenticalSend 函数作用域](https://github.com/nanocoai/nanoclaw/pull/3014)**：将 `hasIdenticalSend` 的判定范围限制在当前进行中的 turn 内，修复了可能的重复消息误判问题。
- **[PR #2476 - restart-nanoclaw 技能](https://github.com/nanocoai/nanoclaw/pull/2476)**：新增了无 NanoClaw 环境下的重启技能，方便运维。

**📝 文档与其他**
- **[PR #3152 - 从 README 链接架构文档](https://github.com/nanocoai/nanoclaw/pull/3152)**：在 README 架构部分增加指向详细文档的链接，提升可发现性。
- **[PR #2682 - update-skills 跳过 v1-only 分支](https://github.com/nanocoai/nanoclaw/pull/2682)**：增强了 skills 更新机制的版本兼容性甄别能力。

**评估**：核心团队在镜像安全与体积优化、消息去重边界修复上的工作尤为突出，表明项目正在为更大规模部署做准备。

---

## 社区热点

今日讨论热度最高的议题集中在 **消息操作兼容性** 和 **镜像验证可信度** 两个方向：

1. **[Issue #3153 - add_reaction / edit_message 对入站消息总是失败](https://github.com/nanocoai/nanoclaw/issues/3153)**（新增，1条评论）
   作者 `TO-maschenborn` 报告了一个严重影响使用体验的问题：平台消息ID中的 agent-group 后缀未被剥离，导致 API 请求发送到平台时被直接拒绝（`message_not_found`）。Slack 渠道上每次交互都失败并重试 3 次后报错。这一问题直接触达消息互动功能的根基，吸引了不少关注。

2. **[PR #3158 - verify-agent-image 认证身份尚未配置](https://github.com/nanocoai/nanoclaw/pull/3158)**（新增，核心团队）
   该 PR 暴露了一个之前 PR #3150 引入的验证机制形同虚设的问题——在 CI 变量未配置的情况下，签名验证被跳过，自动合并永远无法触发。这揭示了安全流程落地过程中的关键缺口，备受社区关注。

**分析**：这两个热点共同指向一个主题——**内外部合规与可信度的“最后一公里”问题**。修复看似简单（剥离后缀、配置变量），但直接影响功能可用性和供应链安全声明的公信力。

---

## Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🔴 严重 | [Issue #3153](https://github.com/nanocoai/nanoclaw/issues/3153) | 平台消息ID未剥离 agent-group 后缀，导致 `add_reaction` / `edit_message` 在入站消息上100%失败 | **无 fix PR**，讨论中 |
| 🟠 高 | [PR #3119](https://github.com/nanocoai/nanoclaw/pull/3119) | 长期运行主机上出现同一 agent-group 累积 3 个并发容器的异常，轮询同一会话数据库造成资源浪费 | **修复 PR 待合并** |
| 🟠 高 | [PR #3157](https://github.com/nanocoai/nanoclaw/pull/3157) | `materializeTemplateSkills` 使用 `fs.statSync` 导致悬空符号链接被跟随，引发模板实例化中断 | **修复 PR 待合并** |
| 🟡 中 | [PR #3158](https://github.com/nanocoai/nanoclaw/pull/3158) | 镜像签名验证因缺失 CI 变量而被跳过，自动合并门禁失效 | **修复 PR 待合并** |
| 🟡 中 | [Issue #3155](https://github.com/nanocoai/nanoclaw/issues/3155) | registry 分支与 main 分歧，`/add-codex` 技能在 main 上安装后自身构建步骤失败（typecheck） | **无 fix PR** |

**分析**：#3153 虽无 fix PR，但社区已定位到根因（后缀剥离），修复难度较低；#3119 和 #3157 已有待合并的补丁，预计很快落地。整体来看，项目稳定性处于“问题与修复同步推进”的良性循环中。

---

## 功能请求与路线图信号

今日暂无全新功能请求，但待合并的 PR 暗示了近期演进方向：

- **定时任务增强**：[PR #3154](https://github.com/nanocoai/nanoclaw/pull/3154) 计划为定时任务注入“当前运行时间”和任务专属的 `current_time` 字段（含星期几），可能在下个版本中成为 `process_after` 的有力补充。
- **渠道附件结构化传递**：[PR #3156](https://github.com/nanocoai/nanoclaw/pull/3156) 将频道附件作为结构化数据传给 provider，有望改善多模态交互体验。
- **待观察的长期功能**：包括 `/add-voice-transcription-free-whisper`（免费语音转写）、`paws4claws`（AWS 凭据代理）、`add-github` 轮询模式等 PR 仍处于开放状态，虽长期未合并，但提交者持续更新，不排除被纳入后续版本。

---

## 用户反馈摘要

- **操作痛点**（来自 Issue #3153）：用户 `TO-maschenborn` 详细描述了 Slack 上消息互动失败的直接体验——每次尝试都被平台拒绝，触发 3 次重试后彻底失败。这表明消息操作流程的信任度大打折扣，用户期望能像常规 API 调用一样透明地工作。
- **维护困扰**（来自 Issue #3155）：用户 `glifocat` 在尝试按文档安装技能时受阻，发现 registry 分支与 main 分歧导致技能无法通过自身验证。这反映出多分支管理的摩擦成本，用户希望“开箱即用”的体验。
- **安全合规关注**（PR #3158）：核心团队成员 `gavrielc` 在 PR 描述中直指 CI 变量缺失导致签名验证被跳过的漏洞，虽来自内部，但反映出团队对安全门禁真实有效性的高要求。

---

## 待处理积压

以下长期未合并/未响应的 PR 值得维护者关注：

| PR | 主题 | 持续时长 | 建议 |
|----|------|---------|------|
| [#2301](https://github.com/nanocoai/nanoclaw/pull/2301) | add-github 技能：轮询模式 + 安全提示 | 86天 | 功能完整，尤其适合 NAT 环境；建议安排 review 或明确标记“待后续版本” |
| [#2317](https://github.com/nanocoai/nanoclaw/pull/2317) | 本地语音转写技能（whisper/whisper.cpp） | 85天 | 功能差异化明显，但可能非当前优先级；建议给予明确回应 |
| [#2537](https://github.com/nanocoai/nanoclaw/pull/2537) | 增加 pre-commit 钩子（lint/typecheck） | 74天 | 提升贡献者体验，低成本高收益，建议低风险合并 |
| [#2685](https://github.com/nanocoai/nanoclaw/pull/2685) | Signal 文档更新（打字指示/表情回应） | 57天 | 若 Signal 功能已合并，文档应同步推进 |
| [#2634](https://github.com/nanocoai/nanoclaw/pull/2634) | paws4claws AWS 凭据代理技能 | 64天 | 安全运维场景有价值，但需明确维护责任人 |

⚠️ 关注：多个由 `ira-at-work` 提交的 PR 均停留约 2-3 个月，若社区持续贡献但被搁置，可能挫伤贡献者积极性，建议核心团队给予状态标记或合并时间预期。

---

**报告日期**：2026-07-31  
**数据来源**：[NanoClaw GitHub Repository](https://github.com/nanocoai/nanoclaw)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-07-31

## 1. 今日速览

过去24小时项目活跃度处于高位，共产生 **40 条 Issue 更新**（新开/活跃 34 条，关闭 6 条）和 **50 条 PR 更新**（待合并 29 条，合并/关闭 21 条）。核心信号包括：架构重构进入 **Wave 0 执行阶段**（BenKurrek 提交了 12 个目标架构相关 Issue/PR 系列）、技能系统可靠性修复在两条战线同时推进（#6937/#6938 路由与激活修复 + #6745 可安装可选择性修复）、以及一系列前端分页/渲染 Bug 集中暴露。值得注意的风险信号是 **2 个安全/隐私类 Issue 被标记为 suggested_P0/P1**（#6900 跨用户内存泄漏、#6866 共享 home 目录），需优先跟踪。侧信道亮点包括 macOS 用户提交的 keyless 签名请求（#6905）以及新贡献者 rdisandro 提交的 Agentic Activity 流式 UX 基础 PR（#6901）。

---

## 2. 版本发布

过去24小时**无新版本发布**。

但是存在一个值得关注的待合并发布 PR：**[#5598 chore: release](https://github.com/nearai/ironclaw/pull/5598)**（已开放27天），涉及版本升级：
- `ironclaw_common`: 0.4.2 → 0.5.0（⚠ API breaking changes，新增 Copy impl，破坏下游模式匹配）
- `ironclaw_skills`: 0.3.0 → 0.4.0（⚠ API breaking changes）
- `ironclaw_safety`: 0.2.2 → 0.2.3（✓ 兼容变更）

该 PR 长期滞留可能会阻塞技能生态的第三方适配工作，且其破坏性变更将直接波及 #6937/#6938 等新技能的落地验证，建议维护者评估合并阻塞原因。

---

## 3. 项目进展

### 合并/关闭的 PR（里程碑事件）

| PR | 标题 | 影响 | 状态 |
|---|---|---|---|
| [#6934](https://github.com/nearai/ironclaw/pull/6934) | refactor(host_api): de-wildcard the contract prelude | WS0 第1项完成：移除45个模块的扁平通配重导出，消费者须通过模块路径访问契约，显著改善依赖可追踪性 | ✅ 已关闭 |
| [#6931](https://github.com/nearai/ironclaw/pull/6931) | feat(slack): native /ironclaw slash commands（命令列车第3节） | Slack 斜杠命令从仅有部分实现变为完整可用，补齐 #6873 角色门控 + #6891 WebUI 调色板，产品命令系统三端打通 | ✅ 已合并 |
| [#6874](https://github.com/nearai/ironclaw/pull/6874) | chore(deps): 34包批量更新（everything-else 组） | 同步 async-trait 0.1.91、thiserror 2.0.19、uuid 等 | ✅ 已合并 |

### 架构重构推进

目标架构（Epic #3773）迁移动议 #6918 获批后，BenKurrek 同日提交 **12 个执行类 Issue**（#6919–#6930）构成 Wave 0 的完整切分，包括：十族目录迁移（#6926）、死代码清理 + workspace 级 dead-code ratchet（#6925）、组合/应用/域所有权驱逐（#6924）、核心/执行通道/循环宿主收窄（#6923）、扩展包重构（#6922）等。配套的 **[#6936 基线 + shrink-only 异常棘轮](https://github.com/nearai/ironclaw/pull/6936)**（行为零变更）已提交，为后续大规模移动提供度量护栏。

### 技能系统双线修复

此轮技能修复是项目健康度回升的关键信号：
- **#6938**：激活拒绝时解释原因、强制执行前置要求、对抗发现限制，补齐 Epic #6565 缺失/不可用技能的体验闭环
- **#6937**：词边界关键词匹配（修复 #5417 全词/子串评分倒挂）+ 基于实测的激活阈值
- **#6935**（libSQL 修复）：修复 transcript 索引迁移与当前消息更新竞争导致的 503、以及取消的文件系统事务持有 libSQL writer 租约导致死锁的问题——该修复对对话历史与时间线稳定性有直接影响

---

## 4. 社区热点

### #6284 — error-recoverability endgame（15 条评论，7/19 创建至今仍活跃）
[链接](https://github.com/nearai/ironclaw/issues/6284)

> 目标是让模型能从 **100%** 的已见错误中恢复：运行存活 → 模型看到错误 → 看到原因和成功路径 → 获得行动回合 → 不报告非成功状态。

作为 epic 级别 Issue 持续收获评论关注，反映了社区对“模型犯错后的自我修复能力”为核心体验的强烈诉求。相关修复（如 #6855 压缩时密文脱敏与上下文溢出恢复）已在落地，epic 中的多项目标正在被逐步消化。

### #6565 — Reliable Skill Discovery, Routing, and Activation（Epic）
[链接](https://github.com/nearai/ironclaw/issues/6565)

> 7/25 做了诊断修正，指出主 TurnCoordinator 路径并不跑关键词/正则自动激活管线。

Epic 生命周期内持续修正诊断，当前有 #6937/#6938 两个 L 级 PR 同时推进路由与激活两侧，是当前最活跃的 epic 之一。

### 前端体验类 Bug 集中轰炸
italic-jinxin 在 7/30 密集提交了 **10+ 个 WebUI 质量类 Issue**（#6902–#6916），涵盖分页失效、Markdown 渲染、文件链接跳转、组件统一等。虽单个热度不高，但集中出现说明 Reborn WebUI 正在经历系统性的体验打磨阶段，这些 Issue 也可作为新贡献者 onboarding 的优先入口。

---

## 5. Bug 与稳定性

### 🔴 高严重度（安全/数据隔离 / P0-P1）

| Issue | 描述 | 状态 / Fix PR |
|---|---|---|
| [#6900](https://github.com/nearai/ironclaw/issues/6900) suggested_P0 | **跨用户内存泄漏**：共享频道默认主体绑定将所有用户并入操作者的 memory 命名空间 | OPEN，无 fix PR，**建议立即拉入安全评审** |
| [#6866](https://github.com/nearai/ironclaw/issues/6866) security | **所有用户共享同一 home 目录**，工作区互相可见 | OPEN，无 fix PR，需确认部署层是否启用了隔离模式 |
| [#6834](https://github.com/nearai/ironclaw/issues/6834) p2 | Slack 集成设置流程失败（near.foundation 账户） | OPEN，无 fix PR |

### 🟠 中严重度（功能失效 / 数据错乱）

| Issue | 描述 | 状态 / Fix PR |
|---|---|---|
| [#6752](https://github.com/nearai/ironclaw/issues/6752) | **实例删除失败**，重新登录卡在 "Loading your agents..." | OPEN |
| [#6940](https://github.com/nearai/ironclaw/issues/6940) | **IronHub CTA 全站 404**（所有技能） | OPEN；相关 #6780/#6933 正在加固安装链路，但 CTA 路由可能独立修复 |
| [#6902](https://github.com/nearai/ironclaw/issues/6902) | Projects 页展示**虚构指标**（$0.00 spend、0 pending gates），后端实际不提供这些数据 | OPEN，建议确认是否存在 mock 残留 |
| [#6904](https://github.com/nearai/ironclaw/issues/6904) | 日志页无法加载超过最新一页的条目（`next_cursor` 未接线） | OPEN |
| [#6903](https://github.com/nearai/ironclaw/issues/6903) | Admin 用户列表同样无法翻页（100 条上限） | OPEN |

### 🟢 低严重度（体验 / 展示）

- [#6916](https://github.com/nearai/ironclaw/issues/6916) Markdown 文件在预览模态框中以纯文本渲染（丢失格式）
- [#6915](https://github.com/nearai/ironclaw/issues/6915) 助手消息中的工作区文件链接点击无响应
- [#6910](https://github.com/nearai/ironclaw/issues/6910) 设置页 Switch 组件行为/样式不统一，建议提取共享组件
- [#6909](https://github.com/nearai/ironclaw/issues/6909) Admin 删除确认弹窗与用户详情页行为不一致，建议统一为 ConfirmDialog

### ✅ 已有关联修复的 Bug

- **libSQL 事务取消导致的历史 503** → 已有 **[#6935](https://github.com/nearai/ironclaw/pull/6935)** 修复 PR
- **技能关键词子串误命中（#5417）** → 已有 **[#6937](https://github.com/nearai/ironclaw/pull/6937)** 词边界修复

---

## 6. 功能请求与路线图信号

### 可能纳入下版本

| 请求 | 来源 | 判断依据 |
|---|---|---|
| **keyless cosign 签名发布**（[#6905](https://github.com/nearai/ironclaw/issues/6905)） | aardbol（AUR 打包维护者） | 低成本高信任收益，发布流程非破坏性改动，适合近期纳入 |
| **迁移工具：legacy agent（Hermes/Openclaw）到 IronClaw**（[#6939](https://github.com/nearai/ironclaw/issues/6939)） | 用户反馈 | 降低生态迁移门槛，且当前 Reborn 架构与旧版差异大，工具化需求将随 v1 发布增长 |
| **托管 MCP 服务器注册**（[#6930](https://github.com/nearai/ironclaw/pull/6930) PR） | 核心贡献者 | XL 级 PR 已提交，支持无认证/Bearer/OAuth 自动检测，是扩展生态的关键基础设施 |

### 正在推进中的路线图

- **目标架构 Wave 0**（Epic #3773）：12 个执行 Issue 全部在 7/30 落盘，下一步是 #6936 的基线合并，随后各工作流按 CHECKLIST 推进
- **技能可靠发现/路由/激活**（Epic #6565）：双 PR（#6937/#6938）待合并，随后是#6745 的可安装性修复
- **命令系统三端贯通**：Slack 原生斜杠命令（#6931）已合并，WebUI 调色板（#6891）和角色门控（#6873）此前已完成，全链路初成

---

## 7. 用户反馈摘要

来自 **[x-ai-product-feedback](https://x-ai.slack.com/archives/C09FDEDH5PA)** 渠道的真实反馈经 sergeiest 录入：

- **实例删除失败 + 重新登录卡死**（#6752）：用户在删除名为 "calm-hor..." 的实例时遭遇失败，重新登录后界面永久停留在 "Loading your agents..."。这属于影响核心使用周期的阻塞级体验问题，可能涉及实例生命周期状态机缺陷。
- **新用户迁移成本高**（#6939）：使用 Hermes/Openclaw 的用户因无法携带既有配置和记忆而不愿迁移。社区的典型情绪是 *"would resist starting over with a clean slate"*——这对 IronClaw 从早期采用者走向主流用户构成了隐性门槛。
- **隐私顾虑**（#6866）：用户在浏览工作区时发现所有用户共享同一 home 目录。tobias.holenstein 明确指出这是 *"a privacy concern"*。若为真实部署状态则属于安全事件级别；若为受限演示环境则需对外明确边界。
- **构建可靠性正向信号**：#6905 由 AUR 维护者主动提出签名验证改进，说明外部打包/分发生态已开始活跃，且社区对官方发布物的可验证性有期待。

---

## 8. 待处理积压

### 长期滞留 PR（>14 天）

| PR | 天数 | 类型 | 风险 |
|---|---|---|---|
| [#5598](https://github.com/nearai/ironclaw/pull/5598) chore: release | 27 天 | **核心发布 PR** | 两个 crate 的破坏性变更长期未落地，可能阻塞技能生态第三方适配 |
| [#5664](https://github.com/nearai/ironclaw/pull/5664) deps: actions 组 16 项 | 25 天 | CI 依赖 | actions/checkout 从 v4→v7 跨度巨大，包含 anthropics/claude-code-action 更新，可能存在行为变更需人工确认 |
| [#6428](https://github.com/nearai/ironclaw/pull/6428) deps: tokio 生态 | 9 天 | 运行时依赖 | tokio 生态 4 项更新，属常规升级，但为保持依赖新鲜度建议尽快跟进 |
| [#6364](https://github.com/nearai/ironclaw/pull/6364) feat(attachments): 跨频道文件流 | 10 天 | XL 功能 PR | 涉及 WebUI/Telegram/Slack 统一附件契约，功能面大，若与 #6930 MCP 有交互需协同评审 |

### 长期未响应/需关注的 Issue

| Issue | 创建时间 | 关注点 |
|---|---|---|
| [#3773](https://github.com/nearai/ironclaw/issues/3773) target crate 架构 Epic | 5/19（73 天） | 已进入 Wave 0 执行，但作为总纲需保持状态同步 |
| [#4636](https://github.com/nearai/ironclaw/issues/4636) SSO 多用户隔离 E2E 覆盖（Test） | 6/9 | 已关闭，但建议核实测试是否纳入 nightly 矩阵并持续运行 |
| [#6771](https://github.com/nearai/ironclaw/issues/6771) Reborn Playwright 运行时稳定化 | 7/28（3 天） | 已关闭，时间较短，确认修复已覆盖 legacy-runtime 与 served-api-routes 两条矩阵 |

---

## 项目健康度小结

- **社区活跃度**：Issue/PR 双维度 40/50 的日更新量处于高位，评论互动主要集中在 Epic 层（#6284、#6565），新贡献者（rdisandro、aardbol）开始进入，onboarding 正常
- **工程质量**：架构 Wave 0 的先度量后迁移策略（#6936 行为零变更）体现工程纪律；但安全类 Issue（#6900、#6866）的 P0/P1 标记与无 PR 对应，是当前最需立即投入的风险敞口
- **发布节奏**：无新版本 + 发布 PR 滞压 27 天，破坏性变更累积是短期内的主要交付瓶颈
- **稳定性信号**：前端分页/渲染类 Bug 集中暴露，说明 Reborn WebUI 正处于从"功能可用"向"体验稳定"过渡的阶段；libSQL 竞态修复（#6935）落地后，对话历史 503 与事务死锁问题有望收敛

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报

**报告日期**: 2026-07-31  
**数据覆盖**: 2026-07-30 至 2026-07-31  
**数据来源**: github.com/netease-youdao/LobsterAI

---

## 1. 今日速览

LobsterAI 今日保持了活跃的开发节奏，虽然 Issues 层面无新增/关闭记录（0 条），但 PR 合并/关闭数量达到 8 条，显著高于待合并数量（2 条），说明核心维护团队正高效推进功能迭代与修复。昨日发布了 2026.7.29 版本，新增了侧边聊天选中文本打标签、Kimi K3 模型支持等特性。值得关注的是，项目在 Windows 安装器健壮性、企业级多账户隔离、安全漏洞修复（附件路径遍历）三个方向均有实际代码落地，体现出项目对稳定性、安全性和企业级功能的持续投入。综合判断，项目当前处于**高效迭代期**，整体活跃度评级为 **8/10**。

---

## 2. 版本发布

### LobsterAI 2026.7.29 — 2026-07-29 发布

**核心更新内容：**

| 变更类型 | 内容 | 对应 PR |
|---------|------|---------|
| ✨ 新功能 | 协作模式（Cowork）侧边聊天支持为选中文本添加标签 | [#2405](https://github.com/netease-youdao/LobsterAI/pull/2405) |
| ✨ 新功能 | 新增对 Kimi K3 模型的支持 | [#2381](https://github.com/netease-youdao/LobsterAI/pull/2381) |
| 🔧 修复 | 加固会话生命周期管理与令牌刷新机制 | 版本说明中提及 |

**破坏性变更：** 无

**迁移注意事项：** 无特殊迁移要求，正常更新即可。新增 Kimi K3 模型支持需在模型配置中手动添加对应 API 接入信息。

---

## 3. 项目进展

今日共合并/关闭 8 条 PR，涉及以下关键进展：

### 🏢 企业级多账户隔离（重大架构改进）
**[#2409](https://github.com/netease-youdao/LobsterAI/pull/2409)** — `feat(enterprise): isolate account-scoped auth and service flows`  
按账户隔离了认证、媒体、排队追问、分享和部署状态，防止异步响应串号到新登录账户，并加强了企业版权限管控与失败回滚。这是企业版走向成熟的关键一步。

### 🎁 原生每日签到体验
**[#2408](https://github.com/netease-youdao/LobsterAI/pull/2408)** — `feat(activity): add native daily check-in experience`  
在桌面侧边栏和账户菜单中新增服务端驱动的每日签到功能，支持签到积分领取，且不向渲染进程暴露账户令牌。与 [#2411](https://github.com/netease-youdao/LobsterAI/pull/2411)（侧边栏横幅轮播）形成互补，用户活跃度运营体系正在搭建。

### 💬 协作模式侧边聊天增强
**[#2397](https://github.com/netease-youdao/LobsterAI/pull/2397)** — `feat(cowork): add isolated /btw side chat`  
新增可拖拽、八方向缩放的浮动侧边聊天面板，`/btw` 执行与主对话完全隔离，并走 OpenClaw 工具流。  
**[#2406](https://github.com/netease-youdao/LobsterAI/pull/2406)** — `fix(cowork): improve side chat input handling`  
面板打开时累积选中文本片段、移除产品级问题长度限制、保留有界上下文与传输安全检查。侧边聊天从单次调用进化为可多轮对话的工作面板。

### 🔐 安全修复
**[#2389](https://github.com/netease-youdao/LobsterAI/pull/2389)** — `fix(email): prevent attachment path traversal`  
清理附件文件名并强制下载目录边界，附带跨平台安全测试。这是今日合并中**最重要**的 PR，将邮件技能升级为攻击面更小的版本。

### 🪟 Windows 安装器修复
**[#2412](https://github.com/netease-youdao/LobsterAI/pull/2412)** — `fix(nsis): re-kill survivor processes on every stop poll round`  
修复 Windows 安装/卸载时残留进程逃逸的问题——现在每轮轮询都会重新执行 `Stop-Process`，有效杜绝内核销毁慢于观察窗口导致的进程存活。

### 🎨 UI 一致性
**[#2410](https://github.com/netease-youdao/LobsterAI/pull/2410)** — `style(sites): align page layout with management views`  
Sites 页面宽度、间距和搜索样式与 Skills、MCP 管理视图对齐，提升产品整体一致性。

**整体评价：** 安全加固（attachments）与企业级隔离是今日最大的中长期价值点；签到系统与侧边栏横幅标志着产品从工具向平台化运营迈进；Windows 安装器修复则体现对桌面端体验细节的重视。

---

## 4. 社区热点

今日无高互动 Issue/PR（评论数据为空，👍 均为 0）。但从 PR 的**标签分布**来看：

- **协作模式（cowork）** 相关 PR 共 3 条（[#2397](https://github.com/netease-youdao/LobsterAI/pull/2397)、[#2406](https://github.com/netease-youdao/LobsterAI/pull/2406)、[#2405](https://github.com/netease-youdao/LobsterAI/pull/2405) 已合入 2026.7.29 版本），是当前最活跃的功能线
- **企业级/账户体系**（[#2409](https://github.com/netease-youdao/LobsterAI/pull/2409)）涉及 7 个 area 标签，是跨模块改动最大的一条 PR，投入资源最多

**信号解读：** 团队在企业版账户隔离与协作对话体验两条线上同时发力，预计下一版本将以「多账户企业版稳定性」+「协作工作台成熟化」为主要卖点。

---

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 修复 PR |
|---------|---------|------|---------|
| 🔴 高 | 邮件附件存在**路径遍历漏洞**，恶意文件名可逃逸下载目录 | ✅ 已修复 | [#2389](https://github.com/netease-youdao/LobsterAI/pull/2389) |
| 🟡 中 | Windows 安装/卸载时**残留进程逃逸**，旧进程可能在轮询窗口后存活 | ✅ 已修复 | [#2412](https://github.com/netease-youdao/LobsterAI/pull/2412) |
| 🟡 中 | 侧边聊天**输入截断**：超出产品限制长度的文本无法完整提交 | ✅ 已修复 | [#2406](https://github.com/netease-youdao/LobsterAI/pull/2406) |

今日未发现新的严重崩溃或数据丢失类 Bug。安全修复（#2389）建议用户尽快升级至包含该修复的版本。

---

## 6. 功能请求与路线图信号

| 功能需求 | 来源 PR | 当前状态 | 纳入下一版本可能性 |
|---------|---------|---------|-------------------|
| **每日签到 + 积分奖励** | [#2408](https://github.com/netease-youdao/LobsterAI/pull/2408) | ✅ 已合并 | 已确定，8 月版本将包含 |
| **侧边栏横幅轮播/活动展示** | [#2411](https://github.com/netease-youdao/LobsterAI/pull/2411) | ✅ 已合并 | 与签到同步上线 |
| **Kimi K3 模型支持** | [#2381](https://github.com/netease-youdao/LobsterAI/pull/2381) | ✅ 已合入 2026.7.29 | 已可用 |
| **会话「标记为未读」** | [#1228](https://github.com/netease-youdao/LobsterAI/pull/1228) | ⏳ 待合并（stale） | 功能已实现，取决于维护者清理积压的节奏 |
| **AgentCreateModal Escape 关闭/表单重置** | [#1231](https://github.com/netease-youdao/LobsterAI/pull/1231) | ⏳ 待合并（stale） | 同上 |

**趋势判断：** 签到 + 横幅活动 + 积分体系表明产品正在建设**用户增长与留存闭环**；企业版多账户隔离（#2409）则服务于 B 端客户的多账号管理场景。未来 2-4 周内的版本重点大概率是「活动运营 + 企业版加固」双主线。

---

## 7. 用户反馈摘要

今日无可用的 Issues 评论数据，但可以通过 PR 标题与描述反推用户痛点：

| 用户痛点 | 对应修复 | 满意度预判 |
|---------|---------|-----------|
| Windows 安装/卸载时进程残留，导致更新失败或旧版本干扰 | [#2412](https://github.com/netease-youdao/LobsterAI/pull/2412) 每轮轮询重新杀进程 | 高 — 解决了更新链路上最棘手的「差一步就成功」问题 |
| 侧边聊天无法提交长文本 | [#2406](https://github.com/netease-youdao/LobsterAI/pull/2406) 移除产品级长度限制 | 中高 — 直接改善日常使用体验 |
| 多账户场景下异步响应串号 | [#2409](https://github.com/netease-youdao/LobsterAI/pull/2409) 按账户隔离所有服务流 | 企业用户显著受益，满意度提升可期 |

---

## 8. 待处理积压

以下两条 PR 自 2026-04-01 起已积压 **121 天**（近 4 个月），且已被标记为 `[stale]`，若再不处理将被自动关闭。建议维护者尽快评估：

| PR | 功能 | 积压天数 | 建议 |
|----|------|---------|------|
| [#1228](https://github.com/netease-youdao/LobsterAI/pull/1228) | 会话「标记为未读」功能（含完整 Redux 状态扩展 + 中英文 i18n） | 121 天 | 功能完整度高，建议合入或明确关闭并给出理由 |
| [#1231](https://github.com/netease-youdao/LobsterAI/pull/1231) | AgentCreateModal 支持 Escape 关闭 + 重开时重置表单 | 121 天 | UX 一致性修复，会显著改善弹窗交互体验 |

**风险提示：** 两条 PR 均包含完整实现与国际化文案，长期积压不仅浪费社区贡献者的劳动，也可能因代码冲突导致最终无法合入。若近期无合入计划，建议维护者主动回复贡献者说明排期。

---

*本报告由 AI 自动生成，数据截至 2026-07-31。所有链接均为 GitHub 原始 PR/Issue 地址。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-07-31

*数据统计周期：2026-07-30 00:00 UTC – 2026-07-31 00:00 UTC*


## 1. 今日速览

Moltis 过去 24 小时整体活跃度**中等偏上**，核心维护者（penso）持续高密度推进安全加固与可观测性基础设施建设。今日共有 2 条新 Issue（1 个功能请求、1 个安全 Bug）和 4 条 PR 更新，其中 1 条 PR 已合并（#1166 Slack 通道增强），3 条待合并。值得关注的是：**安全议题连续出现**——昨日报告了 Vault 解锁端点缺少身份验证的问题（#1177），同时 PR #1170 正在收紧特权命令的访问控制边界。此外，可观测性/反馈收集基础设施（#1174）已进入待合入阶段，表明项目正在从纯功能开发转向运维与质量体系建设。


## 2. 版本发布

过去 24 小时无新版本发布。PR #1166 已合入主干，预期将在下一个版本中随 Slack 通道改进一并发布。


## 3. 项目进展

今日有 1 条 PR 被合并，另有 3 条待合并，整体推进节奏良好。

**已合并：**

- **#1166 [已合并] feat(slack): per-message acknowledgment reactions, phases, reconnect supervision, and Block Kit**
  - 在 #1165 合并的 acknowledgment reactions 基础上进一步深化，为 Slack 机器人设计了完整的消息接收确认生命周期。覆盖了排队、取消、重试、回调突发和投递失败等边界场景，并引入 Block Kit 支持。这是对 Slack 通道体验的一次系统性升级，使得消息回执更可靠，用户对机器人处理进度的感知大幅改善。值得注意的是该 PR 的更新日期为 7 月 28 日，今日合入，从创建到合并共 7 天，属于正常节奏。
  - 链接：https://github.com/moltis-org/moltis/pull/1166

**待合并：**

- **#1174 [待合并] Add instrumentation and feedback collection infrastructure**
  - 支持后端无关的 agent 插桩、Langfuse v4 导出、OTLP 后端适配及终端用户反馈收集。该 PR 为平台方提供了完整的可观测性栈，对商业化/企业部署意义重大。
  - 链接：https://github.com/moltis-org/moltis/pull/1174

- **#1170 [待合并] fix(channels): gate /sh and privileged tools behind a per-account operators list**
  - 将访问白名单与特权命令分离开，新增基于账户的 `operators` 列表来管控 `/sh` 等高风险工具的使用边界。此前通过访问白名单即有机会越权执行特权命令，本 PR 是一次关键安全修复。
  - 链接：https://github.com/moltis-org/moltis/pull/1170

**今日 PR 整体评价**：两条待合并 PR（#1174、#1170）分别在可观测性和安全性两个维度做出了实质性贡献，但均已搁置 4-5 天未合入，建议维护者优先 review，特别是安全修复 #1170 不宜久拖。


## 4. 社区热点

**#1178 [Feature]: Let agents send Telegram inline buttons and receive structured callback responses**
- 作者: eddyvlad | 创建: 2026-07-30 | 评论: 0 | 👍: 0
- 链接：https://github.com/moltis-org/moltis/issues/1178

该 Issue 提出的需求非常具体——让 agent 可以发送 Telegram 内联按钮并接收结构化回调响应。虽然没有引发大量讨论（尚为 0 评论），但其需求切入点精准：Telegram 是 agent 交互的重度场景，而内联按钮是实现"人机确认→机器执行"闭环的关键能力。结合近期 #1166 对 Slack 消息互动体验的持续优化，可以判断维护团队正在系统性地增强多平台交互能力，此需求极有可能被纳入路线图。


## 5. Bug 与稳定性

今日报告 1 个安全相关 Bug，无崩溃或回归问题。

| 严重程度 | Issue | 说明 | 是否已有 Fix PR |
|---------|-------|------|:---:|
| **高（安全）** | [#1177][bug] Vault Unlock/Recovery Endpoints Missing Authentication (CWE-306) | Vault 的解锁/恢复端点缺少身份验证，属于 CWE-306（关键功能缺少认证）。攻击者可能绕过认证直接解锁 vault，造成敏感数据泄露。提交者已确认使用最新版本。 | ❸ 暂无对应 PR |
| 低 | 无 | — | — |

链接：https://github.com/moltis-org/moltis/issues/1177

**分析**：该 Bug 严重程度高但因刚提交（今日）尚未有修复 PR。巧合的是，PR #1170（访问控制加固）也是安全向改动，两者在安全主题上形成了同日的呼应。建议维护者在合并 #1170 后，尽快评估 #1177 的修复方案，确保安全短板不会跨版本遗留。另外 CWE-306 类漏洞通常属于企业合规审计必查项，若项目有商业化部署场景，不建议跨过该 Bug 发布新版本。


## 6. 功能请求与路线图信号

**新提出的功能请求：**

- **#1178 [Feature] Telegram 内联按钮与结构化回调**
  - 核心诉求：让 agent 能够主动发送 Telegram 内联按钮，并在用户点击后以结构化数据的方式接收回调，进而驱动 agent 流程。
  - 链接：https://github.com/moltis-org/moltis/issues/1178
  - **路线图预判**：⭐ 中高可能性纳入近期迭代。理由：(1) 与近期 Slack 互动增强的节奏高度一致，扩展消息互动能力显然是一个系统性的方向；(2) Telegram 是 agent 类产品的主流渠道之一，用户需求真实性高；(3) 当前架构设计中 callback 能力已存在（#1170 中即提到 callback 相关控制），实现成本可控。

**其他路线图信号：**

- PR #1174（可观测性+反馈收集设施）进入待合并状态，标志着项目开始重视 end-user feedback 和运维基础设施。该方向需求方通常是平台运营者而非终端用户，说明项目关注点正在向企业级/生产级拓展。


## 7. 用户反馈摘要

**正面信号：**
- 无直接正面评论，但两个显著信号反映用户信任度提升：一是 Slack 反馈机制的持续构建（#1166），体现出项目对"用户体验细节"的投入——将消息接收、处理、完成各阶段通过 reaction 向用户展示，属于精细化的交互设计；二是用户已开始以安全研究和代码审计的方式为项目提交缺陷（#1177 提交者使用了 CWE 编号，表明具备安全专业背景），这类贡献对开源项目质量提升的杠杆效应极大。

**痛点与诉求：**

- **功能性缺口**（来自 #1178）：用户对 Telegram 内联按钮交互有明确需求，"structured callback responses" 的提法暗示现在的 callback 机制不够结构化，agent 难以自动处理。
- **安全担忧**（来自 #1177）：Vault 端点缺少认证是一个"不应出现"的疏漏。该 Issue 的提交者明确表示"正在使用最新版本"，这种由活跃用户提交的安全发现，比随机漏洞报告更具指向性——说明用户正在将 Moltis 用于真实敏感场景（如凭证管理），对安全性有硬性要求。


## 8. 待处理积压

**⏳ 需要关注的长周期 PR：**

- **#1174 [OPEN] instrumentation + feedback 基础设施**
  - 已开放 4 天，为可观测性基座型 PR，涉及模块多、review 成本高，建议安排专项 review。
  - 链接：https://github.com/moltis-org/moltis/pull/1174

- **#1170 [OPEN] 特权命令访问控制安全修复**
  - 已开放 5 天，涉及安全边界。虽未进入今日"最近更新"，但安全类修复建议优先处理，避免长期暴露窗口期。该 PR 更新日期为 7 月 31 日（有更新），说明仍在活跃推进，但建议尽快安排合入。
  - 链接：https://github.com/moltis-org/moltis/pull/1170

**⚠️ 长期未响应的潜在风险项：**

- 今日数据未显示超过两周未更新的旧 Issue/PR，但在 repo 中搜索 `label:bug` + 无最近回复的条目，仍可能存在遗留的中低严重度缺陷未及时处理，建议维护团队做一次存量清理。

---

**日报综合评分：7.5 / 10** —— 项目保持稳健的功能交付节奏（Slack 通道增强合入），安全方向有意识和行动（#1170 已在修复），但 Vault 认证缺失（#1177）这类安全基建漏洞提示项目在安全工程上仍有提升空间。可观测性方向的投入（#1174）值得肯定，但在"用户互动作答"类需求上（#1178）社区反馈尚未及时覆盖。整体判断：项目处于快速成长期，安全与运维体系正在补课。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-07-31

> 数据来源：github.com/agentscope-ai/CoPaw（即 QwenPaw）。当前分析基于过去 24 小时的 GitHub 活动。


## 1. 今日速览

CoPaw（QwenPaw）在过去 24 小时内保持着较高的社区活跃度：共产生 **25 条 Issue 更新**（新开/活跃 18 条、关闭 7 条）和 **50 条 PR 更新**（待合并 24 条、合并/关闭 26 条），无新版本发布。值得关注的是，当日的 Issue 讨论中修复类与体验优化类占比接近，社区反馈集中在 MCP 连接健壮性、`execute_shell_command` 大输出处理以及聊天会话 UI 体验三个方面。值得注意的是，**多项用户反馈的问题已在当天或近期获得对应的 fix PR**，反映出项目维护者响应速度较快，项目整体处于良性迭代节奏。


## 2. 版本发布

今日无新版本发布。当前最新版本仍为 v2.0.1。


## 3. 项目进展

今日共有 26 个 PR 被合并或关闭，以下为实质性推进项目进展的关键合并：

| PR | 标题 | 说明 |
|---|---|---|
| [#6424](https://github.com/agentscope-ai/QwenPaw/pull/6424) | feat(computer-use): native desktop GUI automation for Windows and macOS | 为 Windows/macOS 带来原生桌面 GUI 自动化能力（辅助功能优先 + Tauri 控制模式），是 computer-use 功能的核心合并。合并后，Agent 可操作宿主桌面上的指定应用窗口。 |
| [#6486](https://github.com/agentscope-ai/QwenPaw/pull/6486) | fix(matrix): probe vodozemac E2EE backend | 修复 Matrix 频道在 Python 3.12 下端到端加密不可用的问题（对应 Issue #6476），通过探测 vodozemac 作为备用 E2EE 后端解决。 |
| [#6562](https://github.com/agentscope-ai/QwenPaw/pull/6562) | Fix Bug #6533, #6506, and #60… | 一次性修复 3 个 Bug：`/mission` 命令 TypeError（#6533）、子会话不继承父会话审批级别（#6506）等，由 first-time contributor 提交。 |
| [#6556](https://github.com/agentscope-ai/QwenPaw/pull/6556) | feat(creator): creation checkpoints, home redesign, media recovery… | Creator 插件的下一次迭代：新增创作检查点、首页改版、媒体恢复、导入/导出及双语指南。 |
| [#6256](https://github.com/agentscope-ai/QwenPaw/pull/6256) | feat(governance): make sandbox-unavailable fallback action configurable | 让沙箱不可用时的回退行为可配置（对应 Issue #6250）。 |

**整体判断**：本轮合并涵盖功能增强（computer-use、Creator 插件）、稳定性修复（Matrix E2EE、sandbox 清理）和治理能力完善，项目在能力扩展与健壮性维护上同步推进。


## 4. 社区热点

**最活跃的 Issue：#6307 — v2.0 引入 ~2s 固定开销**

> [agentscope-ai/QwenPaw Issue #6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) | 评论 7 | 创建 07-21，最后更新 07-30

用户 `lululau` 报告从 v1.1.12.post2 升级到 v2.0.0.post3 后，**每次简单对话回复都会产生约 2 秒的固定开销**，且与模型延迟无关。这是目前讨论最持久、影响面最广的性能回归问题。虽然该问题已持续 10 天，但仍为 OPEN 状态，社区方面未见到明确修复排期。

**其次值得关注的 Issue：**

- **#6559** Unwanted session forking — 主会话对话过程中自动产生大量分叉会话且没有父子分组，会话列表混乱（评论 2）
- **#6558** Multiple chat session UI data integrity issues — 会话切换导致消息丢失、指令漂移、回复从头重新渲染（评论 1，多条子问题）

**背后诉求**：社区反馈开始从「功能有无」转向「体验打磨」——性能开销、会话组织、UI 数据一致性成为高频关注点。MCP 生态的使用门槛和稳定性问题也有多个 Issue 集中反馈（#6524、#6557）。


## 5. Bug 与稳定性

以下按严重程度排列（高 → 低），标注修复 PR 状态（如有）：

### 高风险

| 严重度 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🔴 高 | [#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) | v2.0 每次对话新增 ~2s 固定开销，与模型延迟无关 | ❌ 无 |
| 🔴 高 | [#6589](https://github.com/agentscope-ai/QwenPaw/issues/6589) | `execute_shell_command` 产生数万行输出时 UI 主线程阻塞，界面完全卡死 | ❌ 无 |
| 🔴 高 | [#6558](https://github.com/agentscope-ai/QwenPaw/issues/6558) | 多会话 UI 数据完整性问题：切模式丢最后消息、切会话丢回复、指令漂移 | ❌ 无 |
| 🔴 高 | [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) | MCP Server 重启后客户端无法自动恢复，需手动 `list mcp` 重新连接 | ✅ [#6586](https://github.com/agentscope-ai/QwenPaw/pull/6586) fix(mcp): recover stale server sessions |

### 中风险

| 严重度 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🟠 中 | [#6565](https://github.com/agentscope-ai/QwenPaw/issues/6565) | `execute_shell_command` 多行命令换行被折叠成空格导致语法错误；Linux PIPE 模式后台进程卡住 | ❌ 无 |
| 🟠 中 | [#6557](https://github.com/agentscope-ai/QwenPaw/issues/6557) | MCP 工具名以 `-` 开头，导致 Kimi 等严格 OpenAI 兼容 API 返回 400 | ✅ [#6561](https://github.com/agentscope-ai/QwenPaw/pull/6561) fix(mcp): ensure exposed tool names start with a letter |
| 🟠 中 | [#6533](https://github.com/agentscope-ai/QwenPaw/issues/6533) | `/mission` 命令报 TypeError：`_patched_build_master_prompt` 缺少参数 | ✅ 已修复（PR #6562 已合并） |
| 🟠 中 | [#6506](https://github.com/agentscope-ai/QwenPaw/issues/6506) | 父会话审批级别 OFF 不被子会话（spawn_subagent）继承 | ✅ 已修复（PR #6562 已合并） |
| 🟠 中 | [#6555](https://github.com/agentscope-ai/QwenPaw/issues/6555) | Dream 记忆压缩进程遗漏早期会话事件（context scroll-out 后不写入当日记忆文件） | ❌ 无 |

### 低风险

| 严重度 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🟡 低 | [#6476](https://github.com/agentscope-ai/QwenPaw/issues/6476) | Matrix 端到端加密不可用（Python 3.12 下） | ✅ 已修复（PR #6486 已合并） |
| 🟡 低 | [#6578](https://github.com/agentscope-ai/QwenPaw/issues/6578) | Cron 任务 `dispatch.mode: "final"` 未生效，中间事件全部实时推送 | ❌ 无 |
| 🟡 低 | [#6588](https://github.com/agentscope-ai/QwenPaw/issues/6588) | `spawn_subagent` 单任务模式不可用，因为 `batch` 被暴露为必填 | ❌ 无 |
| 🟡 低 | [#6563](https://github.com/agentscope-ai/QwenPaw/issues/6563) | CI `real-behavior-proof` workflow 阻塞所有 fork PR | ✅ [#6584](https://github.com/agentscope-ai/QwenPaw/pull/6584) 已合并（CI 修复） |


## 6. 功能请求与路线图信号

今日收集到的功能请求可分为以下方向，并结合已有 PR 预判其落地可能性：

| 方向 | 代表 Issue | 响应 PR / 状态 | 预判 |
|---|---|---|---|
| **Chat 会话体验** | [#6560](https://github.com/agentscope-ai/QwenPaw/issues/6560)（复制/ESC 停止/撤销/Code 模式复制代码等 6 项）、[#6559](https://github.com/agentscope-ai/QwenPaw/issues/6559)（会话父子分组）、[#6585](https://github.com/agentscope-ai/QwenPaw/issues/6585)（「已接收字符数」动态显示可关闭）、[#6583](https://github.com/agentscope-ai/QwenPaw/issues/6583)（文件上传多行显示文件名） | 暂无直接对应 PR；[#6583] 已有 PR #6567 相关性修复（#6453） | 🟡 部分可能纳入下一迭代 |
| **MCP 稳定性** | [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524)、[#6557](https://github.com/agentscope-ai/QwenPaw/issues/6557) | ✅ 对应 PR #6586、#6561 已在处理 | 🟢 高概率近期合入 |
| **桌面端 UX** | [#6587](https://github.com/agentscope-ai/QwenPaw/issues/6587)（改名去掉 Desktop）、[#6568](https://github.com/agentscope-ai/QwenPaw/issues/6568)（全局快捷键唤出浮动输入框） | 暂无 | 🟡 低优先级，视维护者规划 |
| **工作流/强逻辑流程** | [#6571](https://github.com/agentscope-ai/QwenPaw/issues/6571)（类 Dify 工作流，权限强逻辑判断） | 暂无 | 🔴 重大功能方向，需架构层讨论，短期难落地 |
| **文件上传提示保留中文名** | [#6453](https://github.com/agentscope-ai/QwenPaw/issues/6453) | ✅ PR #6567、#6492 均已提交 | 🟢 高概率合入 |
| **/undo 命令（撤销上一轮对话）** | [#6408](https://github.com/agentscope-ai/QwenPaw/issues/6408) | 已 CLOSED（可能已在内部解决或延后） | ⚪ 已关闭，无进一步动作 |
| **取消多模态能力提示** | [#6452](https://github.com/agentscope-ai/QwenPaw/issues/6452) | 暂无 | 🟡 体验优化，可能低优先 |

**重点观察**：`/undo`（#6408）和「会话撤销」相关需求已在多个 Issue 中出现（#6408、#6559、#6560），但至今未在 UI 中实现。这是一个明确的社区共同痛点，建议路线图优先考虑。


## 7. 用户反馈摘要

从今日 Issues 和评论中提炼的真实反馈：

**✅ 正面反馈**
- 「非常不错的项目」——用户 `abo123456789` 在提出体验优化建议时对项目表达了认可（#6585）。

**😐 体验痛点**
- **性能开销可见**：v2.0 引入的固定 2 秒延迟成为用户升级的主要阻力——「This overhead is absent in v1.x and is caused by architectural changes in the reques…」（#6307）
- **shell 工具输出处理不友好**：多个用户（#6512、#6589、#6565）均反馈 `execute_shell_command` 在输出较大（>30KB）时的截断、UI 卡死和多行命令语法错误，是当前使用频率最高的社区难题之一。
- **会话管理混乱**：自动分叉（#6559）和会话切换丢失上下文（#6558）让多会话用户效率反而降低。
- **文件上传提示中文件名被替代成难以识别的编码路径，且中文名被丢弃**——「把中文改成不可识别支付，太长也极不友好」（#6453）
- **中文 UI 细节**：应用名「QwenPaw Desktop」被用户视为「多此一举且很奇葩」（#6587）；动态显示「已接收字数」闪动频繁「闪的眼睛疼」（#6585）。

**🔍 使用场景**
- 金融行业用户反馈了 MCP 工具名命中 OpenAI 规范的问题（#6557 中提及大量 `-` 开头的金融数据工具名），说明 MCP 生态正在被真实业务场景使用。
- 用户 `feng183043996` 提供了「股票综合分析脚本生成 500+ 行报告」的真实场景来描述 shell 输出截断问题（#6512），说明该功能被用于批量数据处理。


## 8. 待处理积压

### ⚠️ 重点 Item（已多日无进展）

| 项目 | 创建时间 | 最后更新 | 状态 | 说明 |
|---|---|---|---|---|
| [#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) — v2.0 固定 2s 开销 | 07-21 | 07-30 | OPEN，7 条评论 | 最重要性能回归，已持续 10 天无 clsoe 或修复排期，建议优先响应 |
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — 统一 provider 平台 | 07-21 | 07-30 | OPEN | 一个解决 7 个 provider 痛点的综合 PR，已 9 天未合入，是否阻塞在评审或测试？ |
| [#6528](https://github.com/agentscope-ai/QwenPaw/pull/6528) — agent.json 损坏修复（Windows） | 07-28 | 07-30 | OPEN | first-time contributor 提交，修复 Windows 上文件损坏问题，建议尽快 review |

### 📋 其他长期未响应

| 项目 | 创建时间 | 说明 |
|---|---|---|
| [#6312](https://github.com/agentscope-ai/QwenPaw/pull/6312) — 可配置主题/皮肤模块 | 07-21 | Draft PR，需 maintainer 确认方向 |
| [#6429](https://github.com/agentscope-ai/QwenPaw/pull/6429) — 移除 `/new` 命令建议 | 07-24 | 小改动，已 6 天未合入 |
| [#6531](https://github.com/agentscope-ai/QwenPaw/pull/6531) — ACP 响应添加 models 字段 | 07-28 | 影响外部 Agent 客户端（Multica/OpenCode/Zed）的互操作性 |

**给维护者建议**：
1. 优先对 #6307（性能回归）给出明确解释和修复计划，该问题影响了所有 v2.x 用户。
2. 加速处理积压的 first-time contributor PR（尤其 #6528、#6531），保护社区贡献积极性。
3. 考虑将「会话管理 / undo / 复制」等高频 UX 需求纳入下一版本路线图（综合 #6408、#6559、#6560）。
4. 关注 `execute_shell_command` 系列问题（#6512、#6589、#6565），建议统一评估输出截断策略（自动写文件 / 流式读取）。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目动态日报

**日期：2026-07-31** | **数据来源：** [github.com/qhkm/zeptoclaw](https://github.com/qhkm/zeptoclaw)

---

## 1. 今日速览

ZeptoClaw 项目在过去 24 小时内整体活跃度较低，Issues 层面无新增、无关闭、无更新，社区反馈处于静默期。PR 方面有 1 条已提交 8 天且仍处于待合并状态的核心修复（#645），但无新提交或合并动作。无新版本发布。当前项目正处于关键修复的等待窗口期，合并节奏的推进速度将成为未来数日社区信心的风向标。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

**核心 PR 等待合并**

- **[#645 [OPEN] fix(runtime): scrub subprocess secrets and reap timed-out process trees](https://github.com/qhkm/zeptoclaw/pull/645)**
  - **作者：** qhkm | **创建：** 2026-07-23 | **最后更新：** 2026-07-30 | **评论：** 0 | 👍：0
  - **状态：** 待合并（已等待 8 天）
  - **内容摘要：** 该 PR 针对运行时安全性与稳定性进行双重修复：① **密钥泄露风险**——此前 Runtime shell 命令完整继承 ZeptoClaw 的进程环境变量，导致 provider keys 及无关凭据可能被模型编写的命令获取，此 PR 将对此进行清洗；② **子进程回收**——运行时超时后 `Command::output()` future 被丢弃但未一致性地终止并收割子进程树，在 Docker 容器环境下可能产生僵尸进程或资源泄漏。
  - **项目意义：** 该修复直接触及两个核心关切：**安全边界**（凭据隔离）与**资源生命周期管理**（超时后进程树清理）。若合并，将显著提升 ZeptoClaw 作为本地 Agent 运行时的安全可信度与长期运行稳定性。

**项目整体进度评估：** 当前无合并活动，项目自 7 月 23 日提交此核心修复后，已进入合并审批的等待周期，期间无其他功能推进或 Bug 修复。项目进展暂处于停滞状态。

---

## 4. 社区热点

过去 24 小时内无 Issues 更新或评论互动。唯一活跃的 PR #645 自创建以来也尚无评论和点赞。社区讨论热度处于低谷期，无值得分析的热点议题。

---

## 5. Bug 与稳定性

过去 24 小时内无新报告的 Bug。当前需要关注的是 [PR #645](https://github.com/qhkm/zeptoclaw/pull/645) 中正在修复的两个既有问题：

| 严重程度 | 问题描述 | 影响范围 | 修复状态 |
|---------|---------|---------|---------|
| **高** | 子进程环境变量继承导致 provider keys 和凭据可能泄露至模型编写的外部命令 | 所有使用 Shell 命令的本地 Agent 运行场景，涉及密钥安全 | 已有修复 PR #645，待合并 |
| **中** | 运行时超时后 `Command::output()` future 被丢弃，但子进程树未被一致终止和收割 | 长时间运行或超时场景，可能导致僵尸进程与资源泄漏，在 Docker 容器中可能更严重 | 已有修复 PR #645，待合并 |

---

## 6. 功能请求与路线图信号

过去 24 小时内无新功能请求。基于 PR #645 的修复方向，可观察到以下路线图信号：

- **安全架构升级意图：** 对子进程环境变量的清洗表明项目正在向更严格的“最小权限 + 凭据隔离”方向演进，未来可能在运行时安全模型上增加更多防护层（如环境变量白名单、命令沙箱化）。
- **资源治理规范化：** 对超时后进程树回收的重视，暗示项目正在为更长时间的 Agent 任务执行场景做稳定性铺垫。

若 #645 按计划合并，其修复内容可能成为下一版本（如 v0.x 后续迭代）发布的核心更新。

---

## 7. 用户反馈摘要

过去 24 小时内无 Issues 评论或用户反馈可提取。基于当前 PR 内容可推断的潜在用户痛点：

- 用户在使用模型编写 Shell 命令时，存在**对敏感凭据安全的隐忧**，即模型生成的命令可能在无意识间读取或传输环境变量中的密钥。
- 在长时间运行 Agent 任务或频繁超时重试的场景下，**系统资源未被及时释放**可能导致性能持续劣化。

---

## 8. 待处理积压

以下项目需维护者重点关注：

- **[PR #645 fix(runtime): scrub subprocess secrets and reap timed-out process trees](https://github.com/qhkm/zeptoclaw/pull/645)**
  - **提交已 8 天，存在 0 条评论，处于完全静默等待状态。**
  - 作为当前唯一定义安全关键缺陷修复的 PR，长时间无合并动作或评审反馈，可能削弱社区对项目响应速度的信心。建议维护者尽快安排评审并明确合并计划。
  - 若该 PR 存在设计分歧或需补充测试，建议及时在 PR 内公开讨论，以避免长时间悬置。

---

**日报数据快照：** Issues 更新 0 | PR 更新 1（待合并 1）| Release 0 | 活跃讨论 0

> 本日报由 AI 自动生成，数据截至 2026-07-31。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，我是你的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 ZeroClaw 项目 GitHub 数据生成的 2026-07-31 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-07-31

## 1. 今日速览

ZeroClaw 项目今日处于 **高活跃、高风险积聚** 的状态。过去 24 小时内，Issue 和 PR 的更新数量激增（分别为 15 条和 50 条），但 **合并/关闭数为 0**，这表明项目正处于一个功能开发和问题修复的高峰期，大量工作等待审查与合并。当前积压的 PR 中不乏 `risk:high` 和大尺寸（`size:XL`）的变更，这可能对项目稳定性构成挑战。安全相关议题（如 Webhook 鉴权绕过、命令白名单大小写匹配问题）成为社区关注焦点，且均有对应的修复 PR 在等待合并。

## 3. 项目进展

由于今日无 PR 被合并或关闭，项目核心代码没有向前推进。但是，大量高质量的 PR 正在等待合并，这些 PR 一旦合并将显著推进项目：

- **安全加固**：PR #9569 (fix(gateway): fail closed when a WhatsApp Cloud or Linq webhook cannot be verified) 和 PR #9568 (fix(security): match command allowlist entries case-insensitively on Unix) 直接修复了今日报告的两个严重 Bug，是当前最紧急的待合并项。
- **核心能力增强**：PR #8688 (feat(runtime): add trusted goal tools and delegation boundaries) 和 PR #9126 (feat(plugins): validate typed instance config) 是两个大尺寸（`size:XL`）功能 PR，分别旨在引入可信目标工具和为插件系统增加类型安全，代表了项目在 Agent 能力和可扩展性上的长期投入。
- **关键修复**：PR #8937 (fix(agent): stream-hash tool args in loop_detector) 旨在通过避免深层克隆来优化性能；PR #9325 (fix(runtime): make streamed user turns read as conversation) 旨在修复流式输出时本地小模型将用户输入误读为日志的问题。

## 4. 社区热点

今日讨论最热烈的是几个长期开放的 RFC（Request for Comments）和架构级 Issue，它们获得了最多的评论，反映了社区对项目未来方向的深度关注。

- **[#9048] RFC: Separate conversation history from agent-curated long-term memory** (评论: 12)
  [zeroclaw-labs/zeroclaw Issue #9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)
  - **诉求**：社区希望项目在架构层面更清晰地将“对话历史”与“长期记忆”分离。当前实现将对话记录写入通用记忆后端（`MemoryCategory::Conversation`），这与官方文档中定义的生命周期概念相悖，限制了记忆管理的灵活性。

- **[#8603] & [#8550] RFC / Feature: OpenAI Chat Completions compatibility adapter** (评论: 7 + 5)
  [zeroclaw-labs/zeroclaw Issue #8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) / [zeroclaw-labs/zeroclaw Issue #8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)
  - **诉求**：这是社区呼声极高的功能，希望能将 ZeroClaw 暴露为标准 OpenAI Chat Completions API，以无缝接入 Open WebUI、LobeChat 等主流客户端。该需求有两个关联 Issue（一个为 RFC，一个为 Feature Request），表明用户有强烈的生态互通需求。

- **[#8933] RFC: Add cross-turn conversation correlation to OTel export** (评论: 7)
  [zeroclaw-labs/zeroclaw Issue #8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)
  - **诉求**：社区希望利用 OpenTelemetry (OTel) 的标准属性 `gen_ai.conversation.id` 来关联跨轮次的对话，从而在可观测性工具中实现对话级别的追踪和分析。

## 5. Bug 与稳定性

今日报告了 3 个 Bug，按严重程度排列如下，均已有对应修复 PR：

- **S0 - 数据丢失 / 安全风险**：
  - **[#9565] [Bug]: gateway webhook handlers do not fail closed (WhatsApp Cloud, Linq, WATI)**
    [Issue #9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565)
    **问题**：三个网关 Webhook 处理器在未验证调用者身份的情况下处理消息，存在安全风险。**修复 PR**：[#9569](https://github.com/zeroclaw-labs/zeroclaw/pull/9569)
- **S2 - 降级行为**：
  - **[#9566] [Bug]: uppercase allowed_commands entries never match on Unix**
    [Issue #9566](https://github.com/zeroclaw-labs/zeroclaw/issues/9566)
    **问题**：命令白名单在 Unix 系统上大小写敏感，导致包含大写字母的命令条目静默失效。**修复 PR**：[#9568](https://github.com/zeroclaw-labs/zeroclaw/pull/9568)
- **S3 - 次要问题**：
  - **[#8847] bug(ci): cargo test --doc fails with duplicated rustdoc theme flag**
    [Issue #8847](https://github.com/zeroclaw-labs/zeroclaw/issues/8847)
    **问题**：Rust 1.96 环境下 CI 中的文档测试因 rustdoc 配置问题失败。**状态**：无直接修复 PR，但相关任务 [#9545](https://github.com/zeroclaw-labs/zeroclaw/issues/9545) 可能会在 CI 重构中解决。

## 6. 功能请求与路线图信号

今日新增了多个功能请求，其中几个与已有内部项目或 PR 高度关联，有望被纳入后续版本：

- **语音交互**：Issue #8780 (RFC: Realtime speech-to-speech channel for Gemini Live) 提出增加实时语音到语音的交互通道。这符合 AI 助手多模态交互的行业趋势，虽暂无直接 PR，但属于前瞻性规划。
- **复杂模型调度**：Issue #8568 ([Feature]: Mixture-of-Agents (MoA) virtual model provider) 和 Issue #7951 ([Feature]: Effort-based local/cloud model routing) 都旨在提高模型调用的智能性，前者是引入“混合 Agent”模式，后者是“按需路由”。这两个请求与目前“本地优先”的工作方向互补。
- **可观测性**：Issue #9545 (Task: gate rustdoc warnings in required PR CI) 是来自维护者内部的工程化任务，旨在加固 CI，防止文档警告回归。
- **用户体验**：Issue #9562 是关于 WebChat 界面禁用自动滚动的小功能请求，直接关联用户使用体验。

## 7. 用户反馈摘要

- **生态互操作需求迫切**：在 OpenAI 兼容适配器（#8603, #8550）的讨论中，用户明确表达了希望与主流前端（Open WebUI, LobeChat）无缝集成的需求，这已成为阻碍部分用户采用 ZeroClaw 的痛点。
- **本地模型体验待优化**：PR #9325 的修复目标直接指向了本地小模型的体验问题。用户报告在使用 Ollama 等本地模型时，流式输出会被模型误读为日志，这严重破坏了对话的连贯性，是本地优先策略落地的关键阻碍。
- **配置易错且难以排查**：PR #9311 旨在解决配置中由于输入错误导致的静默失败问题。用户反映配置错误只产生一行通用日志，很难定位，这增加了部署和维护的难度。

## 8. 待处理积压

- **高风险、长周期 PR 亟待关注**：PR #8688 (feat(runtime): add trusted goal tools and delegation boundaries, size:XL) 和 PR #9126 (feat(plugins): validate typed instance config, size:XL) 均创建于本月上旬，带有 `risk:high` 和需作者操作（`needs-author-action`）标签，长时间未合并，存在冲突或设计变更风险。维护者需要关注这些大型 PR 的进展，避免其“腐烂”。
- **长期开放的架构级 RFC**：Issue #9048（对话历史与长期记忆分离）和 #8933（OTel 跨轮次关联）等 RFC 已开放超过两周，虽然评论活跃，但未见明确的采纳或拒绝时间表。拖延可能导致社区贡献者的热情减退。
- **与安全修复直接相关的 PR**：PR #9410 (fix(security): default command audit logging to disabled) 虽为安全修复，但标签为 `needs-author-action`，状态停滞。若该问题属实，是安全态势的倒退，建议尽快处理。

---
**总结：** ZeroClaw 项目处于高速发展的阶段，社区活跃，产出质量高。然而，工作流在“提交”和“合并”之间存在明显瓶颈，导致大量关键修复（尤其是安全问题）无法及时生效。维护者应立即着手处理待合并的 PR，特别是安全相关项，以回应当前社区的高涨需求，并保持项目的健康度。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*