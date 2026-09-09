# OpenClaw 生态日报 2026-09-09

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-09-09 09:31 UTC

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

⚠️ 摘要生成失败。

---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告

**报告日期：2026-09-09**  
**数据范围：过去 24 小时 GitHub 公开动态**

---

## 1. 生态全景

今日个人 AI 助手开源生态呈现“多点迭代、局部拥堵”的态势。在 12 个被监测项目中，9 个有实际动态，其中 3 个项目（NullClaw、TinyClaw、Moltis）完全静默。整体开发热度依然很高，但**合并吞吐量明显低于提交量**——Hermes Agent 与 ZeroClaw 均出现 50 条 PR 更新但 0 合并的情况，说明社区贡献活跃、维护者审查能力成为瓶颈。迭代重心正从“功能堆叠”转向“体验打磨、稳定性加固与安全边界治理”，多个项目不约而同地处理多租户隔离、凭证泄露、存储膨胀和成本可观测性问题。此外，OpenClaw v2026.8.1 的版本升级在衍生项目中引发连锁兼容性修复，显示核心框架的变动对生态具有强辐射力。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| OpenClaw | 数据缺失（摘要生成失败） | 数据缺失 | 未知 | 无法评估 |
| NanoBot | 2 | 27（8 合并/关闭，19 待合并） | 无 | 健康，高频迭代，体验打磨 |
| Hermes Agent | 50（39 活跃/新开，11 关闭） | 50（0 合并，50 待合并） | 无 | 提交活跃但合并瓶颈严重，长期 issue 积压 |
| PicoClaw | 3（1 关闭，2 待跟进） | 8（1 合并，7 待审） | 无 | 较健康，有 PR 评审积压 |
| NanoClaw | 2（均 open） | 10（2 合并/关闭，8 待审） | 无 | 健康，功能推进与修复并行 |
| NullClaw |

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-09-09

## 1. 今日速览

过去 24 小时 NanoBot 项目保持高活跃度：共 27 条 PR 动态，其中 8 条已合并/关闭，19 条处于待合并状态；Issues 端有 2 条更新。今日集中度非常明显——WebUI/TUI 的体验优化、Bug 修复与性能改进占据了绝大多数合并项，其中 chengyongru 一人贡献了 6 条已合并 PR，覆盖导航保留、流式数学渲染、UI 裁切、性能优化与 TUI 新命令等。无新版本发布，项目正处于高频迭代阶段，健康度良好。

## 2. 版本发布

过去 24 小时内无新版本 Release。

---

## 3. 项目进展

今日共合并/关闭 8 条 PR，整体上**前端体验（WebUI/TUI）的稳定性和可用性显著推进**，另有 Codex 模型目录修复落地。

### WebUI 功能与体验

- **PR [#5717](https://github.com/HKUDS/nanobot/pull/5717)**（已合并/关闭）：修复从项目菜单创建 topic 时丢失项目选择的问题。改用 `history.pushState` 避免路由事件清空项目状态，使首条消息即关联正确项目。
- **PR [#5716](https://github.com/HKUDS/nanobot/pull/5716)**（已合并/关闭）：修复打开技能选择器时建议列表不刷新的问题。Agent 在页面加载后安装的新技能现在无需重载页面即可出现在选择器中。
- **PR [#5705](https://github.com/HKUDS/nanobot/pull/5705)**（已合并/关闭）：为 TUI 新增 `/usage` 命令，展示上下文占用率和最近模型轮次用量图表，补齐了 WebUI 已有能力的 TUI 侧缺口。

### WebUI 视觉与渲染修复

- **PR [#5714](https://github.com/HKUDS/nanobot/pull/5714)**（已合并/关闭）：将文件编辑 diff 从 reasoning 折叠块中分离，避免折叠后 diff 内容不可见。
- **PR [#5713](https://github.com/HKUDS/nanobot/pull/5713)**（已合并/关闭）：修复斜体活动标签在 `fit-content` + `overflow: hidden` 下裁切末字符的问题，增加 2px 右内边距。
- **PR [#5712](https://github.com/HKUDS/nanobot/pull/5712)**（已合并/关闭）：修复流式数学公式中含 `<` 比较符时响应被截断的问题，例如 `\prod_{j<i}(1-\alpha_j)`。

### 性能优化

- **PR [#5703](https://github.com/HKUDS/nanobot/pull/5703)**（已合并/关闭）：减少长时间对话中的重复 DOM 扫描、活动行搜索和隐藏细节渲染，并限制历史渲染的数据量，显著降低工具密集场景下的渲染开销。

### Codex 通道

- **PR [#5709](https://github.com/HKUDS/nanobot/pull/5709)**（已合并/关闭）：将 Codex 模型目录的客户端版本从 `0.144.0` 提升至 `0.153.4`，修复 GPT-6-Astra 模型在选取器中可能不出现的问题。

> **小结**：今日合并内容以 "修复用户可见问题 + 减少长期性能债务" 为主，表明项目正从功能扩展期转向体验打磨与稳定性加固阶段。

---

## 4. 社区热点

今日评论最活跃、讨论热度最高的条目集中在 Issues 端：

### Issue [#5693](https://github.com/HKUDS/nanobot/issues/5693) — 无人零售/IoT 场景支持建议（3 条评论，已关闭）

- **内容**：用户 `linxingming168`（标注由"AI 军团·笔芯秘书"自动提交）建议 NanoBot 适配无人零售/智能货柜场景，具体诉求包括：
  1. 增加对无人零售/智能货柜场景的原生支持
  2. 提供更轻量的部署方案以适配边缘设备
  3. 增加中文文档和示例
- **分析**：该 Issue 将 NanoBot 定位为"轻量、开源、可自托管的"智能体，期望复用到 IoT 边缘场景。背后反映了开源 AI Agent 社区对**低资源设备落地**和**本地化文档**的明确需求。但 Issue 已被关闭，且由自动化工具提交，实际维护者关注度可能有限。

### Issue [#5647](https://github.com/HKUDS/nanobot/issues/5647) — WebUI 会话标题在缺少 webui flag 时不生成（持续更新中）

- **内容**：这是由 PR [#5528](https://github.com/HKUDS/nanobot/pull/5528) 引入的一个回归，`maybe_generate_webui_title()` 仅在 envelope 携带 `webui` 标志时才生成标题，重启后该标志可能丢失，导致标题不生成。
- **分析**：该 Issue 已持续 6 天并有新的更新，用户 `ZIFe

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-09

## 今日速览

过去 24 小时 Hermes Agent 保持高活跃度：**50 条 Issues 更新**（新开/活跃 39，关闭 11）与 **50 条 PR 更新**（全部处于待合并状态，合并/关闭 0），无新版本发布。项目提交节奏密集，仅 `teknium1` 一人即提交了 8 个跨领域修复/功能 PR，另有多个旧 PR 被 salvage/rebased 重新激活。但需警惕的是 PR 合并量为零，审查与合并瓶颈可能正在累积。Issue 侧最突出的是 **P1 级 MCP profile-scoping 缺陷（#106005）**连续出现，以及 183 评论的 skills index 故障（#66616）持续 50 天未关闭。此外，多条会话状态相关的 P1 bug 集中在过去两天内被报告并被标记为 duplicate/closed，暗示本周可能存在一次回归批。总体判断：**开发活跃度高，但合并吞吐与长期 issue 治理急需关注**。

---

## 项目进展

**今日无 PR 被合并或关闭**，所有 50 条 PR 均在待合并队列中。但今日新提交的 PR 呈现出清晰的项目演进信号，最值得关注的包括：

| PR | 内容概要 | 类型 |
|----|---------|------|
| [#106414](https://github.com/NousResearch/hermes-agent/pull/106414) | Claude Code OAuth identity 版本下限更新，修复 Fable 5.x 模型被拒问题（port prime-agent#1993） | 修复 |
| [#106418](https://github.com/NousResearch/hermes-agent/pull/106418) | 云实例元数据（IMDS）凭据获取纳入审批范围，增强安全边界（对标 Claude Code 2.1.257） | 安全 |
| [#106413](https://github.com/NousResearch/hermes-agent/pull/106413) | Webhook 路由引入 `session_key` 可选持久会话（salvage #90589，受 Poke 启发） | 功能 |
| [#106412](https://github.com/NousResearch/hermes-agent/pull/106412) | CLI 输入组件新增 `/vim` 可选 vim 编辑模式（关闭 #4254） | 功能 |
| [#106419](https://github.com/NousResearch/hermes-agent/pull/106419) | compute-host PID 监管的 Windows 安全 + 僵尸进程修复（salvage #68272） | 修复 |
| [#106417](https://github.com/NousResearch/hermes-agent/pull/106417) | V4A `Add File` 不再覆盖已有文件（salvage #41393） | 修复 |
| [#106416](https://github.com/NousResearch/hermes-agent/pull/106416) | 视频生成新增 MiniMax H3 Max Turbo 模型族（含 1080P 档位） | 功能 |
| [#106409](https://github.com/NousResearch/hermes-agent/pull/106409) | Codex 设备登录 SSL 错误时保留原始错误 + PQ 混合组提示 | 修复 |

大量 PR 以 "salvage"（捡起先前被搁置/关闭的 PR）形式重新提交，表明社区贡献管道存在积压，但有维护者在积极催熟。

---

## 社区热点

### 🥇 [#66616 Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) — 183 评论
- 状态：OPEN / P3 / 自 2026-07-18 以来持续 50+ 天
- 自动探针持续报告 `/docs/api/skills-index.json` 过期（当前 29.8h 超过 26h 限制）
- 183 条评论高居榜首，反映用户对官方文档/skills 索引可用性的高度在意，且长时间未关闭引发不满

### 🥈 [#10421 Turn-level live time context](https://github.com/NousResearch/hermes-agent/issues/10421) — 20 评论 / 9 👍
- 状态：OPEN / P2 / 创建于 2026-04-15，Open 已 147 天
- 用户痛点集中在 agent 对"当前时间/日期/星期"感知不可靠，必须显式调工具获取
- 9 个 👍 为今日 Issue 列表最高，是社区呼声最强的功能

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-09-09

## 今日速览

过去 24 小时项目保持较高活跃度：共更新 3 条 Issue（1 条关闭、2 条待跟进）与 8 条 PR（1 条合并、7 条待审），无新版本发布。开发侧以 Telegram 交互修复、IRC 增强和渠道重构为主线，其中一条长期搁置的 skills 模块重构 PR（#714）终于合并，标志着 CLI 技能管理能力完成阶段性整合。社区侧最受关注的是工具反馈动画无限编辑 Telegram 消息的稳定性 Bug（#3343，228,000+ 次误编辑），已有对应修复 PR 待合并，整体项目健康度良好，但 PR 评审积压值得注意。

## 项目进展

**唯一今日合并 PR：skills 模块重构落地**

- [#714 [CLOSED] skills: install/reinstall CLI and refactor into skillsCmd](https://github.com/sipeed/picoclaw/pull/714)（作者: seanly）
  - 重构技能安装逻辑，新增 `ParseInstallSpec`、`InstallFromGitHubEx`、`fetchTree` 等函数，支持 `repo@branch` 与子路径安装
  - 新增 `reinstall` 子命令，支持强制覆盖
  - 生产环境安装改用 GitHub Trees API 获取完整目录，并优化已存在时的错误提示

这标志着技能管理从"可用"走向"可维护"，为后续技能生态扩展打下基础。

---

## 社区热点

| 条目 | 热度指标 | 核心诉求 |
|------|---------|---------|
| [#3343 [BUG] 工具反馈动画无限编辑 Telegram 消息](https://github.com/sipeed/picoclaw/issues/3343) | 3 评论，228,000+ 次误编辑 | 资源控制与限流规避：动画未随 agent turn 结束而停止，连续数天每 3 秒调用一次 `editMessageText`，触发 Telegram 服务端限流。用户关注失控行为的主动终止机制 |
| [#3265 [CLOSED] Gateway 启动时 deltachat 频道类型报错](https://github.com/sipeed/picoclaw/issues/3265) | 4 评论，1 👍 | 配置容错：未配置 deltachat 却启动失败，暴露频道初始化逻辑对默认配置的兼容性问题，已关闭（可能是修复或标记 stale） |
| [#3355 [BUG] 连接飞书报错：未知字段 `channel_list.feishu.app_id`](https://github.com/sipeed/picoclaw/issues/3355) | 1 评论 | 配置结构变更/文档不同步：nightly 版本不识别文档示例中的字段名，需要官方明确配置 schema 变更 |

**分析**：社区焦点集中在「运行时边界控制」与「配置一致性」两大方向。Telegram 动画 Bug 因涉及限流和长时间资源消耗而关注度最高，用户期待快速合入修复。

---

## Bug 与稳定性

按严重程度排序：

**高严重度**

- [#3343 工具反馈动画无限编辑 Telegram 消息](https://github.com/sipeed/picoclaw/issues/3343)
  - 现象：动画持续数天、每 3 秒一次编辑，累计 228,000+ 次，触发 Telegram `retry_after` 限流
  - 修复：已有 PR [#3353 fix(channels): bound tool feedback animations](https://github.com/sipeed/picoclaw/pull/3353)，设置 5 分钟上限、首次编辑错误即停止，待合并评审

**中严重度**

- [#3355 飞书配置未知字段 `app_id`](https://github.com/sipeed/picoclaw/issues/3355)
  - 现象：nightly-50-gbbf6893c 无法识别配置中的 `channel_list.feishu.app_id`
  - 当前无对应 fix PR，需确认是配置迁移还是文档过时

**已解决/关闭**

- [#3265 Gateway 启动报未知 deltachat 类型](https://github.com/sipeed/picoclaw/issues/3265) —— 已关闭，不再影响用户

---

## 功能请求与路线图信号

以下 PR 均处于待合并状态，指向下一版本的可能特性：

**新渠道能力**

- [#3354 feat(irc): assemble IRCv3 multiline messages](https://github.com/sipeed/picoclaw/pull/3354)（作者: linhongyu510）—— 支持 IRCv3 `draft/multiline`，让长消息/多行消息作为整体进入 agent，依赖 `batch` 和 `message-tags` 能力协商
- [#3344 Add Build Remote Agent phone pairing (gbr/1)](https://github.com/sipeed/picoclaw/pull/3344)（作者: LinespottingPrivate）—— 新增 `gbr/1` 协议配对适配器，允许手机端作为 Remote Agent 远程围观/控制桌面 agent，附二维码与 8 位码配对

**模型提供商扩展**

- [#3371 feat(providers): add opencode-go provider with session header support](https://github.com/sipeed/picoclaw/pull/3371)（作者: EMTumariscal）—— 新增 `opencode-go` 提供商，按模型 ID 自动路由 endpoint 族，并附带 `x-opencode-session` 会话头支持

**Telegram 体验优化**

- [#3357 fix(telegram): treat replies to the bot's own messages as implicit mentions](https://github.com/sipeed/picoclaw/pull/3357)（作者: hugodeco）—— `mention_only: true` 群组中直接回复 bot 消息视为提及，保持对话连续性
- [#3356 fix(telegram): re-attach quoted documents when replying to a file message](https://github.com/sipeed/picoclaw/pull/3356)（作者: hugodeco）—— 回复引用的文档消息时重新附加文档本体，而非只传 `[file]` 占位符

**渠道重构**

- [#3222 refactor(deltachat): cleanup implementation, documentation -200LOC](https://github.com/sipeed/picoclaw/pull/3222)（作者: trufae）—— 删除遗留特性，移除硬编码 relay 列表，密码配置迁移至 jsonrpc，接口按语义更名（`invite_link` → `join_invite_link` + `show_invite_link`）

**路线图判断**：IRC 多行、Telegram 回复语义增强、opencode-go 提供商实现均已完成且逻辑独立，大概率随下个 nightly 或 minor release 合入；#3344 因引入新外部依赖（MIT `gbr-agent`）可能需更长期评审。

---

## 用户反馈摘要

| 来源 | 用户声音 | 核心诉求 |
|------|---------|---------|
| [#3343](https://github.com/sipeed/picoclaw/issues/3343) raine | "动画在 agent turn 停止后仍继续调用 `editMessageText`，持续数天……产生 228,000 次编辑尝试" | 对失控后台行为零容忍，希望所有异步反馈都有终态保障 |
| [#3355](https://github.com/sipeed/picoclaw/issues/3355) ttghub | "nightly-50-gbbf6893c 报 `unknown field(s): channel_list.feishu.app_id`" | 期望配置文档与实际实现保持同步，nightly 变更需在 Release Notes 标注 breaking changes |
| [#3265](https://github.com/sipeed/picoclaw/issues/3265) Cipher208 | "没有配置 deltachat，Gateway 依然启动失败" | 服务启动应具备配置缺失容错，不应因默认未启用的频道崩溃 |

**共性反馈**：用户对 PicoClaw 的稳定性和配置可预测性有较高期待，nightly 构建的配置兼容性问题已被多次触及。

---

## 待处理积压

| 条目 | 搁置时长 | 说明与优先级 |
|------|---------|-------------|
| [#3222 refactor(deltachat): cleanup implementation](https://github.com/sipeed/picoclaw/pull/3222) | 自 2026-07-03 起，68 天 | 大型重构 PR，已攒大量 review 负担，且与 #3265 关闭直接相关，建议优先安排 reviewer；涉及 breaking changes（密码配置移除），合入前需同步更新文档 |
| [#3343 修复 PR #3353](https://github.com/sipeed/picoclaw/pull/3353) | 自 2026-08-31 起，9 天 | 修复高严重度 Bug 的 PR，等待超过一周，建议争取下一窗口合并 |
| [#3344 Remote Agent phone pairing](https://github.com/sipeed/picoclaw/pull/3344) | 自 2026-08-23 起，17 天 | 功能完整但引入外部工具依赖（MIT `gbr-agent`），需确认协议稳定性和安全边界（仅限 127.0.0.1:8788 / stdio）后再合入 |
| [#3354 / #3356 / #3357 / #3371](https://github.com/sipeed/picoclaw/pulls) | 7–9 天 | 近期集中提交的改进类 PR，整体积压中；其中 #3357 和 #3356 为 Telegram 用户高频场景，建议打包快速评审 |

---

**整体健康度评估**：项目开发活跃度高，社区提交者众多（linhongyu510、hugodeco、EMTumariscal 等外部贡献者），修复响应链条完整（Bug → fix PR 48 小时内出现）。风险点集中在 PR 评审积压——特别是 #3222 跨时 2 个月以上仍未合并，建议维护者每周安排固定时间处理积压，避免社区贡献者流失。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-09-09

## 1. 今日速览

过去24小时内，NanoClaw 保持高强度的迭代节奏：共发生 **2 条 Issue 更新**（全部 open）和 **10 条 PR 动态**，其中 2 个 PR 已关闭/合并，8 个仍待 reviewers 处理。合并的 PR 集中在核心线程路由与社区门户集成，对多线程场景的回复准确性和用户接入体验有直接改善。本周未发布新版本，但涌现了大量围绕 OpenCode 集成的功能 PR 和 WhatsApp 频道修复，项目整体处于「功能快速推进 + 稳定修复补齐」的健康阶段。需注意：8 个 PR 待合并，review 队列略有积压，建议维护者加快审阅节奏。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

今日有两个 PR 被合并/关闭，标志着核心能力的实质推进：

- **[PR #3738] 修复：消息回复现在会正确落入被回复消息的线程**（`fix: thread replies from the message being answered`）  
  作者 zvi-fried | 更新于 2026-09-09  
  该 fix 解决了 `send_message`、`send_file` 以及 `<message to>` 回复在路由时取错线程的问题——此前文件/回复会错误地落到主频道。修复后，所有回复都会进入对应消息的线程，显著改善多线程场景下用户的讯息组织体验。  
  👉 https://github.com/qwibitai/nanoclaw/issues/3729 → #3738

- **[PR #3729] 功能：通过浏览器将主机连接到社区单元并管理权限**（`feat(setup): connect the host to its community cell and manage perks in the browser`）  
  作者 gavrielc | 更新于 2026-09-08  
  将 Echo 和 Slack 的设置流程整合进社区门户，用户只需一次浏览器访问即可完成配置，运行中的主机与账户 cell 保持连接。此举大幅简化了首次接入与日常权限管理的成本。  
  👉 https://github.com/qwibitai/nanoclaw/pull/3729

此外，以下 4 个 PR 虽未合并，但已完成度高、被标记为 `core-team` 与 `follows-guidelines`，极可能在近 48 小时内合入：

- **#3733 / #3747**：OpenCode provider 契约实现 + 设置/托管集成（glifocat）
- **#3746**：保留 provider 取消信号、失败投递状态与技能文件（glifocat）
- **#3745**：在 main 分支上恢复 context-preview 工具（gabi-simons）

如果上述 PR 合入，NanoClaw 将获得完整的 OpenCode 运行时支持和「查看 agent 视角」的调试工具，里程碑价值明显。

## 4. 社区热点

- **[Issue #3735]：conversations/ 归档目录无限增长，无保留策略、无上限**  
  作者 TO-maschenborn | 评论 2 | 更新于 2026-09-08  
  这是今日讨论热度最高的 Issue。`archiveTranscriptFile()` 每次压缩都会写入 markdown 归档到 `groups/<folder>/conversations/`，但没有任何清理机制。报告者称其部署舰队中该目录「为 agent group 的整个生命周期持续增长」，直接指向运维成本与磁盘耗尽风险。这一缺陷影响面覆盖所有长时间运行的用户，快速得到 2 条评论的跟进。  
  👉 https://github.com/qwibitai/nanoclaw/issues/3735

- **[Issue #3705]：`ncl tasks update --recurrence` 不重算下一次触发时间（process_after）**  
  作者 DawoudIO | 评论 1 | 更新于 2026-09-09  
  虽然 Issue 创建于 9/3，但今日仍有新动态（最后更新 9/9），说明讨论未停止。用户指出从 weekly 切换到 daily 后，任务仍然按旧的 weekly 槽位触发，改动计划后行为不符合直观预期，容易造成多次意外执行或错过时间窗。  
  👉 https://github.com/qwibitai/nanoclaw/issues/3705

## 5. Bug 与稳定性

按严重程度排序，今日共有 **2 条新 Bug 类 Issue** 与 **4 个 Bug 修复 PR**：

| 严重度 | 问题 | 状态 | 对应 Fix |
|---|---|---|---|
| 🔴 高 | **归档无限膨胀**：`conversations/` 目录无保留/旋转/上限（#3735） | 待处理 | 暂无 fix PR |
| 🟠 中 | **改 recurrence 不重算 process_after**：#3705，调度行为与用户预期不符 | 待处理 | 暂无 fix PR |
| 🟠 中 | **更新控制器崩溃**：`scripts/update-skills.ts` 依赖 `provider-contract-verifier.ts`，但 `git archive` 清单漏掉了它（#3750） | 已有 PR | #3750 |
| 🟠 中 | **来自不同线程的触发消息互相丢弃回复**（#3749） | 已有 PR | #3749 |
| 🟢 低 | **WhatsApp @newsletter JID 入站未过滤**，会混入无关会话（#3751） | 已有 PR | #3751 |
| 🟢 低 | **WhatsApp 待回答问题可能丢失**：多问题轮询时部分 pending question 无法被回答（#3752） | 已有 PR | #3752 |

其中，#3738（线程路由修复）已合并，#3749/#3750/#3751/#3752 仍在审查中。**#3735 是最需要重视的稳定性隐患**，关系到所有长期运行时用户的磁盘占用，建议维护者优先规划存储治理策略（retention 或 rotation）。

## 6. 功能请求与路线图信号

今日没有新的纯功能型 Issue，但 PR 侧传递了清晰的路线图信号：

- **OpenCode 集成是当前最大功能投入**：「#3733 + #3747」两阶段 PR 分别实现了 provider contracts 和 setup/托管集成。若按计划落地，NanoClaw 将支持 OpenCode 作为完整的 agent provider，包括原生工具适配、MCP、取消、压缩与恢复。这很可能是下一版本的旗舰功能。  
  👉 https://github.com/qwibitai/nanoclaw/pull/3733 | https://github.com/qwibitai/nanoclaw/pull/3747

- **恢复 context-preview 工具**（#3745）：让维护者/e2e 测试无需启动容器即可打印 agent 读取的完整上下文。属于开发者体验的补强，可能随下一版本发布。  
  👉 https://github.com/qwibitai/nanoclaw/pull/3745

- **Issue #3705 的调度语义** 值得作为小功能纳入后续规划：更新 recurrence 时自动重算 `process_after`，或至少给出 warning，提升任务管理工具的可用性。

## 7. 用户反馈摘要

- **存储治理是当下最强烈的痛点**（来自 #3735）：用户明确表示「我们的舰队上这个目录会无限增长」，并将问题归类为「无 retention、无 rotation、无 cap」三重缺失。这暗示在真实生产部署中，归档文件积累已成为长期运行的阻碍因素，用户期望一个可配置的清理策略。
- **任务调度的「隐性意外」令人困扰**（来自 #3705）：用户描述了具体的操作场景——从每周改为每日后，任务依旧按旧的每周时间触发。「调用者需要一个能理解新计划的系统」是该反馈的核心诉求，属于修改立即生效的合理预期。
- **社区对合并 PR 的反馈尚未体现**：今日合并的 #3738 和 #3729 还没有后续评论，暂无法评估修复上线后的用户满意度，需持续跟踪。

## 8. 待处理积压

以下 Issue/PR 长期未解决，建议维护者优先关注：

- **[Issue #3705]** **任务 recurrence 更新后 process_after 不重算**  
  创建于 9/3，尽管今日有新更新，但已持续 6 天无 fix PR。涉及任务调度核心逻辑，建议尽早排入 sprint。  
  👉 https://github.com/qwibitai/nanoclaw/issues/3705

- **[Issue #3735]** **归档目录无上限增长**  
  创建于 9/7，已获 2 条评论且属于高影响运维问题，但当前没有开发者认领。提醒维护者指派 owner 评估磁盘治理方案。  
  👉 https://github.com/qwibitai/nanoclaw/issues/3735

- **8 个待合并 PR 的 review 积压**：除上述 OpenCode 系 PR 外，#3745、#3746、#3749、#3750、#3751、#3752 平均等待已超过 24 小时。其中 #3750 是阻断线上 `/update-nanoclaw` 的回归修复，建议优先审阅。  
  👉 列表见 https://github.com/qwibitai/nanoclaw/pulls

---

*本日报基于 2026-09-09 的 GitHub 公开数据生成，所有链接均引用自 nanocoai/nanoclaw 仓库。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-09-09

## 1. 今日速览

IronClaw 在过去 24 小时迎来一轮高度集中的开发冲刺：共 11 条 PR 被提交或关闭，其中 5 条关闭、6 条待合并，另有 2 条 Issue 处于活跃状态。所有活跃 PR 均由同一核心贡献者（kirikov）于 9 月 8 日密集提交，指向一个清晰的主线——修复 Hosted-MCP 多租户环境下的工具目录隔离问题。值得关注的是，围绕 7 月底报告的跨用户元数据暴露 Issue（#6778），已形成一套包含合并目录、按调用者隔离、SEP-414 溯源在内的组合修复方案。项目整体活跃度高，开发方向聚焦，但需留意多组功能存在重叠/承继关系，评估时需避免重复合入。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

今日关闭/合并的 5 条 PR 中，3 条为实质性变更，2 条为旧 PR 收尾：

- **修复 Hosted-MCP 工具目录互相覆盖**（[#8083](https://github.com/nearai/ironclaw/pull/8083)，merged）：将"发现的 hosted-MCP 目录"从「整体替换」改为「合并」，避免不同用户的工具在共享注册槽位中互相删除。这是对 #6778 跨用户暴露问题的第一层修复。
- **区分空环境变量与未设置变量**（[#8088](https://github.com/nearai/ironclaw/pull/8088)，closed）：`env_or_override` 不再将 `FOO=` 与缺失的 `FOO` 等同对待，避免运维将配置项误设为空字符串时静默回退到默认值。
- **捆绑 agent-market hosted-MCP 提供方包**（[#8089](https://github.com/nearai/ironclaw/pull/8089)，closed）：为 agent.market 提供方补齐了第一方捆绑包（manifest、tool schemas、静态声明），作为 live `tools/list` discovery 之前的 fallback。

另两条旧 PR（[#6760](https://github.com/nearai/ironclaw/pull/6760)、[#6759](https://github.com/nearai/ironclaw/pull/6759)）分别被标记为"superseded"和"needs rebase"，建议维护者明确关闭或回收。

**项目进展小结**：Hosted-MCP 多用户隔离问题的修复已经从"讨论"走向"落地"；同时基础配置语义（空 env var）得到加固；agent.market 扩展的完整接入进入最终阶段。整体来看，项目在扩展系统稳定性和托管 MCP 安全性两个方向都有实质推进。

## 4. 社区热点

- **[#6778 Hosted-MCP 工具目录跨用户暴露](https://github.com/nearai/ironclaw/issues/6778)（评论 2，更新于 09-08）**：这是今日最受关注的 Issue。它揭示了一个深层设计缺陷——工具目录按 extension id 单槽发布，而非按安装/用户维度，在 multi-principal 服务器上会造成 A 用户的工具列表被 B 用户的 discovery 覆盖，且元数据跨用户可见。该 Issue 虽创建于 7 月底，但今日迎来集中响应：直接催生了 3 条相关 PR（#8083、#8090、#8084）。

- **[#8086 `ironclaw skills list` 看不到运行时写入的 skills](https://github.com/nearai/ironclaw/issues/8086)（新开，0 评论）**：虽然是新 Issue，但其描述的"用 CLI 调试 agent 却拿到空列表"的场景非常典型，直击开发者工具链的可观测性短板。该 Issue 指向的可能是 CLI 与运行时之间不同的用户/凭据上下文，而非单一 bug。

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 问题 | 状态 |
| --- | --- | --- |
| 高 | **Hosted-MCP 工具目录跨用户覆盖及元数据暴露**（[#6778](https://github.com/nearai/ironclaw/issues/6778)）：多用户共享服务器上，后一次 discovery 覆盖前一次，且工具目录按 extension id 全局可见，构成数据泄露风险 | 已有修复 PR：#8083（合并目录，已关闭）、#8090（按 caller 键控，待合并） |
| 中 | **Operator 安装的包无法被使用**（[#8085](https://github.com/nearai/ironclaw/pull/8085)）：`from_host_bundled_manifest_with_inline_dynamic_schemas` 构造函数与 `validate_consistency` 校验器对"哪些 manifest 来源允许内联动态 schema"存在不一致判断，导致 operator 安装的包能构建但不能用 | 修复 PR 待合并 |
| 中 | **空环境变量静默选默认值**（[#8088](https://github.com/nearai/ironclaw/pull/8088)）：`FOO=` 与未设置等同，运维误配置会静默失败 | 已修复（PR 已关闭） |
| 低 | **CLI 无法列出 runtime 写入的 skills**（[#8086](https://github.com/nearai/ironclaw/issues/8086)）：排查 agent 技能问题时，CLI 给出空列表，将用户引向错误方向 | 待处理 |

## 6. 功能请求与路线图信号

- **SEP-414 溯源机制落地**（[#8084](https://github.com/nearai/ironclaw/pull/8084)，待合并）：在出站 hosted-MCP 调用上打 `_meta` 溯源标记，让多租户 MCP 服务器能够识别调用来自哪个 conversation 以及是否为重试。**对按调用计费、需要防止 side-effecting 调用重复扣费的 provider 有直接价值**。替代并继承早前搁置的 [#6759](https://github.com/nearai/ironclaw/pull/6759)。
- **Prompt 上下文阈值可配置化**（[#8087](https://github.com/nearai/ironclaw/pull/8087)，待合并）：`PromptContextTokenBudget::DEFAULT_CONTEXT_LIMIT_TOKENS` 从常量改为可覆盖配置，适配更大上下文窗口的模型部署。
- **文档附件指针模式**（[#8082](https://github.com/nearai/ironclaw/pull/8082)，待合并）：将文档文本从"内联到模型请求"改为"按需 pointer 引用"，避免多附件场景下 context 预算被快速耗尽。
- **Telegram 命令菜单自动注册**（[#8072](https://github.com/nearai/ironclaw/pull/8072)，待合并）：在扩展激活时调用 `setMyCommands`，并尽力清理；改善终端用户体验。
- **agent-market 市场化扩展正式化**（[#8089](https://github.com/nearai/ironclaw/pull/8089)，已关闭）：作为 hosted-MCP 第一方包捆绑，与既有 bundled 扩展形态对齐。

综合来看，下一版本很可能包含：#8084（SEP-414）、#8085（operator 包修复）、#8087（context 限制可配）、#8082（附件指针模式）以及 #8090（按 caller 隔离）。

## 7. 用户反馈摘要

- **多租户部署者的核心顾虑**（来自 #6778 评论）：在共享的 hosted-MCP 服务器上，不同用户的工具目录互相污染是"必然复现"的——只要两个用户的 discovery 先后触发就会互相覆盖。评论者关注的核心不是「工具可见性」，而是**跨用户元数据暴露**带来的安全风险。
- **调试者的挫败感**（来自 #8086）：当 agent 安装的技能对 CLI 不可见时，用户第一反应是"我的 agent 坏了"，而实际上问题可能只是 CLI 与 runtime 的用户上下文不一致。用户期待 CLI 能看到并区分**所有用户**的 skills，而不是只看到自己配置的那个。
- **运维人员的隐形坑**（来自 #8088）：空字符串覆盖默认值的行为很难被发现——配置看起来"设置了"，实际却静默走了默认路径。这类问题在事故排查中会极大浪费定位时间。

## 8. 待处理积压

- **[#6778 Hosted-MCP 跨用户暴露](https://github.com/nearai/ironclaw/issues/6778)**：创建于 07-28，拖延超一个月。今日虽有 #8083 合入（合并目录）和 #8090（按调用者键控）兜底，但建议维护者在 #8090 合入后**明确关闭 #6778 并附上修复说明**，避免历史 Issue 长期悬挂。
- **[#6759 SEP-414 溯源（旧版）](https://github.com/nearai/ironclaw/pull/6759)**：07-28 开启，标记 "Needs a rebase"，已被 #8084 取代。建议弃用并引导至新 PR。
- **[#6760 agent-market 扩展（旧版）](https://github.com/nearai/ironclaw/pull/6760)**：07-28 开启，标记 "Superseded in shape, not in intent"，已被 #8089 取代。建议关闭以避免产生新旧两条实现路径的困惑。

---

*本日报基于 2026-09-09 上午的 GitHub 数据生成，所有链接指向 nearai/ironclaw 仓库。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-09-09


## 1. 今日速览

今日 LobsterAI 共处理 **20 条 Issue 更新**（16 条活跃/新开、4 条关闭）和 **14 条 PR 更新**（12 条已合并/关闭、2 条待合并），无新版本发布。维护团队在 9 月 9 日集中合并了一批围绕 **OpenClaw v2026.8.1 升级后插件兼容性修复**的 PR（覆盖钉钉、飞书、Discord、QQ、NIM、网易 Bee 等 IM/插件通道），显示项目正在快速消化运行时升级带来的生态连锁问题。Issue 侧仍有 5 条未修复的安全报告和数条高严重度稳定性缺陷处于开放状态，积压修复压力较大。整体活跃度高，但安全积压与老 issue 响应速度值得关注。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 12 条 PR 中，绝大多数是围绕 **OpenClaw v2026.8.1 升级后的兼容性修复**，可归纳为三条主线：

### 3.1 IM / 插件通道兼容性修复（核心进展）

| PR | 内容 |
|---|---|
| [PR #2628](https://github.com/netease-youdao/LobsterAI/pull/2628) | 修复钉钉在 Windows Jiti 加载器下的 `import.meta` 报错、飞书 SDK 根入口不再导出的兼容性问题 |
| [PR #2629](https://github.com/netease-youdao/LobsterAI/pull/2629) | 恢复 NIM 与网易 Bee 插件在 OpenClaw v2026.8.1 下的加载（修复 `ERR_PACKAGE_PATH_NOT_EXPORTED`） |
| [PR #2630](https://github.com/netease-youdao/LobsterAI/pull/2630) | 修复钉钉（`DingTalk runtime not initialized`）和飞书（`runtime.config.loadConfig is not a function`）入站消息无法分发的问题 |
| [PR #2632](https://github.com/netease-youdao/LobsterAI/pull/2632) | 保留已有非模型配置，避免退出登录时 IM 账号/Agent 路由/本地网关认证丢失；Windows 网关改用 IPC 优雅停止 |
| [PR #2633](https://github.com/netease-youdao/LobsterAI/pull/2633) | 修复 Discord `dm.policy`/`dm.allowFrom` 旧配置被 schema 拒绝、导致网关无法启动的问题 |
| [PR #2634](https://github.com/netease-youdao/LobsterAI/pull/2634) | 修复 QQ 2.0.1 关闭信号直接退出导致清理不完整、以及配置变更后桌面端未恢复消息同步的问题 |
| [PR #2637](https://github.com/netease-youdao/LobsterAI/pull/2637) | 将官方 Discord 包固定打包至 `dist/extensions/`，解决 `openKeyedStore is only available for trusted plugins` 注册拒绝问题 |

### 3.2 网关与配置稳定性

- [PR #2635](https://github.com/netease-youdao/LobsterAI/pull/2635) — 修复 OpenClaw v2026.8.1 `config.get` 缓存返回旧 hash 导致配置下发失败、触发不必要 Gateway 重启的问题。加入有界退避重试，使短暂 hash 冲突可通过热加载恢复，避免兜底重启。

### 3.3 定时任务与 UI 细节

- [PR #2631](https://github.com/netease-youdao/LobsterAI/pull/2631) — 修复 OpenClaw v2026.8.1 升级后定时任务的历史记录重复导入、持久化收据前失败状态未记录的问题。
- [PR #2636](https://github.com/netease-youdao/LobsterAI/pull/2636) — 修复中英文切换时“检查更新”按钮标签不刷新的 i18n 问题。

**整体判断**：这是一次针对 OpenClaw v2026.8.1 升级的集中“排雷”，效率较高（多条 PR 当天创建当天关闭），但联动暴露的插件生态兼容面较广，后续需警惕同类问题在其他通道上继续出现。

---

## 4. 社区热点

今日讨论最活跃的 Issues（评论数 3-4 条）：

### 4.1 [#1903 会员登录频繁失败，无法使用网易付费模型](https://github.com/netease-youdao/LobsterAI/issues/1903)（4 条评论，已关闭）

用户反馈会员登录不进去、无法使用付费模型。**注意：该 issue 已因 stale 被关闭**，但问题本身涉及付费用户核心权益，关闭后仍建议内部跟进确认。

### 4.2 [#2046 产品建议：Agent 记忆体系](https://github.com/netease-youdao/LobsterAI/issues/2046)（3 条评论）

用户提出 Agent 记忆目前依赖手动维护、跨 session 信息大量丢失。核心诉求：将对话标题/元数据持久化到文件系统，让 Agent 可感知历史对话。反映了对 Agent 连续性的强需求。

### 4.3 [#2121 重复输出是否在大量消耗 token？](https://github.com/netease-youdao/LobsterAI/issues/2121)（3 条评论）

用户截图显示 Agent 输出大量重复文字，质疑 token 浪费。背后是对**成本控制**的普遍担忧，同类反馈在过去 issue 中反复出现。

### 4.4 [#2120 三条产品建议（任务预输入/运行时延/UI 三列）](https://github.com/netease-youdao/LobsterAI/issues/2120)（3 条评论）

用户提出借鉴 workbuddy 实现任务预输入以提升连续性、延长单次任务运行时长（脚本监控时被 terminated）、技能界面全屏下 2 列改 3 列。实用性强，但该 issue 已 stale。

### 4.5 [#2176 Security: 自动 artifact 加载导致任意本地文件读取](https://github.com/netease-youdao/LobsterAI/issues/2176)（2 条评论）

由安全研究员 YLChen-007 报告的严重安全问题，今日被标记 stale（最后更新 2026-09-09），但**仍未关闭、无修复 PR 链接**。评论虽不多，但性质严重，社区关注度实际高于表面数据。

---

## 5. Bug 与稳定性

按严重程度排列：

### 5.1 高风险

| Issue | 严重程度 | 现象 | 是否有修复 PR |
|---|---|---|---|
| [#2214 数据备份导致主进程卡死](https://github.com/netease-youdao/LobsterAI/issues/2214) | **高** | 点击“备份数据”后 5-10 秒主窗口变白、标题栏显示“未响应”，100% 可复现，用户只能强制结束进程 | 无 |
| [#2230 同模型耗时差异巨大](https://github.com/netease-youdao/LobsterAI/issues/2230) | **高（性能）** | 同样提示词：CodeBuddy 耗时 2m24s/67K token，LobsterAI 耗时 25 分钟/60M token——差距达 900 倍 token 消耗 | 无 |
| [#2215 安装反复失败（Resource extraction failed）](https://github.com/netease-youdao/LobsterAI/issues/2215) | **高** | NSIS 安装器在不同环境反复失败，用户自行解包定位到真实安装路径为 G:\LobsterAI（非默认 C 盘），问题与多路径残留相关 | 无 |

### 5.2 中风险

- [#2079 执行结果窗口滚动到

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，这是根据您提供的 ZeptoClaw GitHub 数据生成的日报。

---

### ZeptoClaw 项目动态日报 (2026-09-09)

#### 1. 今日速览

今日 ZeptoClaw 项目活跃度较低，属于常规维护与社区反馈期。过去24小时内，项目有 1 个新 Issue 提交和 1 个新的 Pull Request (PR) 待审，无新版本发布。社区方面，有用户明确提出了对 OrcaRouter provider 的支持请求，反映出对项目扩展生态的兴趣；项目维护者则提交了一个关于 WebSocket 连接安全的修复 PR。整体来看，项目进展平稳，但核心迭代速度有所放缓，重点在于安全加固与第三方集成。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日无合并或关闭的 PR，但有一个新的待合并 PR 展示了项目的下一步动作。

- **待合并 PR: 修复 Panel WebSocket 认证安全漏洞** ([#674](https://github.com/qhkm/zeptoclaw/pull/674))
    - **关键进展**: 该 PR 由维护者 `qhkm` 提交，旨在解决一个安全问题。此前 Panel 的 WebSocket 连接会将长期有效的 API Token 或 JWT 放在 URL 的 `?auth=` 参数中，这可能导致凭证被访问日志或浏览器历史记录泄露。
    - **影响评估**: 该修复引入了一个基于认证和 CSRF 保护的端点，来获取 30 秒有效的单次使用票据 (ticket)，并在 WebSocket 升级时使用。这显著提升了 Panel 连接的安全性。虽然该 PR 尚未合并，但它明确了项目正在积极修复潜在的安全风险，向更安全、更健壮的方向演进。

#### 4. 社区热点

今日社区讨论热度不高，但以下两个条目构成了主要热点，分别代表了用户的对外诉求和对内安全加固的关注。

- **Issue [#675](https://github.com/qhkm/zeptoclaw/issues/675)**: **请求支持 OrcaRouter provider**
    - 这是今日唯一的新 Issue。作者 `putraperdana1207-pixel` 在摘要中高度认可了 ZeptoClaw 的设计理念，即在体积（~6MB）和启动速度（~50ms）上的极致追求。
    - **背后诉求**: 该请求表明，部分用户已经将 ZeptoClaw 视为在边缘或容器不友好的环境中部署 AI 助手的理想选择。支持 OrcaRouter 这类 provider 是希望进一步扩展项目的接入生态，让用户在模型提供商上有更多选择。这体现了用户对项目轻量级定位的肯定，并提出具体的集成期望。

- **Pull Request [#674](https://github.com/qhkm/zeptoclaw/pull/674)**: **安全修复：用票据替换 WebSocket Bearer URL**
    - 这条 PR 虽然由维护者提出，但因其解决的是潜在的数据安全问题，同样引发了关注（尽管评论为0）。它反映了在安全审计或内部代码审查中发现的隐患，是项目走向成熟化过程中的重要一步。

#### 5. Bug 与稳定性

今日未报告新的故障、崩溃或回归类 Bug。但有一个安全问题值得注意，且有对应的修复 PR。

- **严重程度: 高 (安全风险)**
    - **问题描述**: Panel WebSocket 连接通过 URL 参数 (`?auth=`) 传递长期有效的 API Token 或 JWT。
    - **潜在影响**: 凭证可能被 Web 服务器访问日志、代理日志或浏览器扩展/历史记录捕获，导致凭证泄露。
    - **修复状态**: 已有待合并的 Fix PR ([#674](https://github.com/qhkm/zeptoclaw/pull/674))，将认证方式改为短时、单次使用的票据，风险正在被消除。

#### 6. 功能请求与路线图信号

- **新功能请求：支持 OrcaRouter provider** ([#675](https://github.com/qhkm/zeptoclaw/issues/675))
    - 这是来自社区的直接功能请求，希望集成新的模型路由服务商。
    - **路线图信号**: 考虑到 ZeptoClaw 轻量、多 Provider 支持的定位，以及用户对轻量级部署场景的青睐，该请求被采纳的可能性较高。结合项目现有的架构（支持多渠道、多 Provider），加入 OrcaRouter 支持是合理且能拓展用户群的方向。建议维护者评估该集成的成本，并考虑将其排入后续迭代计划。

#### 7. 用户反馈摘要

- **用户场景**: 用户 `putraperdana1207-pixel` 在提交 #675 时给出了积极的场景反馈，认为“ZeptoClaw 解决了个人 AI 助手中的一个现实矛盾：功能通常意味着体积臃肿”。这表明用户非常看重 ZeptoClaw 在极低资源占用（~6MB、~50ms 启动）下提供的丰富功能。
- **优点**: 项目的轻量级、高速度定位获得了认可。
- **建议/不足**: 插件的生态扩展性，具体体现在对更多 Provider（如 OrcaRouter）的支持上，是目前用户感到缺失的部分。

#### 8. 待处理积压

目前数据样本中暂无长期未响应的重要 Issue 或 PR。当前需要关注的积压事项是今日新产生的待办：

- **高优先级**: PR [#674](https://github.com/qhkm/zeptoclaw/pull/674) 需尽快进行代码审查与合并，以修复 WebSocket 凭证泄露的安全隐患。
- **中优先级**: Issue [#675](https://github.com/qhkm/zeptoclaw/issues/675) 需维护者进行回复，明确是否接受该建议，并给予初步排期或说明，以维持社区活跃度。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-09-09

## 今日速览

过去24小时内，ZeroClaw 社区讨论热度维持高位：33条 Issue 更新均为新开或活跃状态，无一条关闭；50条 PR 全部处于待合并状态，合并/关闭数为 0。今日无新版本发布。项目处于**活跃讨论阶段**，多个 RFC 进入修订迭代，但**合并通道存在明显瓶颈**——大量已就绪的 PR 因 maintainer review 或 author action 阻塞而未能落地。整体健康度中等偏上，架构类 RFC 讨论质量较高，但交付节奏需要关注。

---

## 版本发布

今日无新版本发布。最近一次已知版本为 v0.8.5。

---

## 项目进展

**今日无 PR 被合并或关闭**，所有功能与修复尚未进入主干。但以下重要 PR 正处于活跃推进状态，值得关注：

- **#10722 [fix] 向事件消费者传递工具调用前的叙述文本与终端回退**（Audacity88, 2026-09-09）— 修复 ACP/RPC 消费端因 `on_delta: None` 而丢失工具调用前叙述的问题。直接对应 Issue #10697，是 ZeroCode ACP 体验的关键修复。[PR #10722](zeroclaw-labs/zeroclaw PR #10722)
- **#10716 [feat] 按配置的写入溢价为缓存写入定价**（sunlit-deng, 2026-09-08）— 修复成本账本以普通输入费率计算缓存写入、低估 Anthropic 缓存写成本的问题。对应 Issue #10699。[PR #10716](zeroclaw-labs/zeroclaw PR #10716)
- **#10714 [fix] 基于注册表键路由集成配置链接**（sunlit-deng, 2026-09-08）— 修复 Integrations 页面 "Configure" 链接错误使用显示名 slug 导致 404 的问题。对应 Issue #10690。[PR #10714](zeroclaw-labs/zeroclaw PR #10714)
- **#10727 [ci] 从发布说明生成 X 与 Discord 公告**（JordanTheJet, 2026-09-09）— 改进发布流程，避免公告内容被字节截断导致语义受损。[PR #10727](zeroclaw-labs/zeroclaw PR #10727)
- **#10726 [ci] 按摘要固定 zerorelay 发布基础镜像**（VladimirLewisII, 2026-09-09）— 对应 Issue #10277，消除可变基础标签带来的供应链漂移风险。[PR #10726](zeroclaw-labs/zeroclaw PR #10726)

此外，多个大型 PR（如 #10241 恢复受监管 shell 审批路由、#9819 像素级图像验证、#9809 每配置文件多模型支持）仍在等待维护者审核或作者更新，是当前合并队列阻塞的主要来源。

---

## 社区热点

今日讨论最活跃的 Issue 集中在 **架构类 RFC 的持续修订**：

1. **#9487 RFC: Runtime-owned conversation sessions and transport surface adapters** — 评论 35 条，进入第 5 版修订。这是对会话架构的实质性重构提议，涉及运行时、传输层适配、安全域。社区讨论密集，但尚未进入投票阶段。[Issue #9487](zeroclaw-labs/zeroclaw Issue #9487)

2. **#9488 RFC: Unified file and attachment architecture** — 评论 28 条，第 10 版修订。文件与附件架构的统一涉及所有会话表面，与 #9487 形成架构双子提案。[Issue #9488](zeroclaw-labs/zeroclaw Issue #9488)

3. **#6996 RFC: Granular sandbox policy - filesystem restrictions** — 评论 26 条。讨论已持续数月，聚焦应用层路径准入与操作系统沙箱（Bubblewrap/Landlock/Seatbelt）两层策略漂移问题。[Issue #6996](zeroclaw-labs/zeroclaw Issue #6996)

4. **#8692 [Tracker]: Maintainer decision queue for RFCs and design issues** — 评论 15 条。作为维护者决策跟踪器，该 Issue 汇聚了所有待定 RFC，反映了项目在治理层面正在建立更规范的决策流程。[Issue #8692](zeroclaw-labs/zeroclaw Issue #8692)

5. **#10076 RFC: Composable WASM plugin runtime architecture** — 评论 11 条。WASM 插件化运行时是项目扩展性的重要方向，近期修订后与 #10526 的事件历史设计保持了一致。[Issue #10076](zeroclaw-labs/zeroclaw Issue #10076)

**背后诉求**：社区当前最核心的关注点是**架构层面的统一与规范化**——会话所有权、文件附件、沙箱策略、插件机制都在进行系统性的 RFC 讨论，且修订频率高（#9488 已到第 10 版）。这说明项目正处在从“功能堆叠”向“架构收敛”转型的阶段，维护者和核心贡献者投入了大量精力在设计评审上。

---

## Bug 与稳定性

过去 24 小时无 Bug 被关闭，新报告/活跃 Bug 主要集中在以下方面（按严重程度排列）：

### 🔴 高风险/高优先级

- **#9816 [P1] Anthropic provider 成本报告 $0.00，预算上限永远不会触发** — 严重财务功能缺陷。`cost_usd` 始终为 0.0 导致日/月预算保护失效。已有对应修复 PR #10716 提交，但属于较全面方案（还覆盖了缓存写入定价），可能还需拆分或扩展评审。[Issue #9816](zeroclaw-labs/zeroclaw Issue #9816)
- **#10697 [P1] ZeroCode ACP 转录丢弃工具调用前的助手文本** — 用户看到回复不完整，体验受损。PR #10722 已于今日提交修复。[Issue #10697](zeroclaw-labs/zeroclaw Issue #10697)

### 🟠 中等问题（S2）

- **#10625 非视觉模型场景下 `[media attachment]` 字面占位符被送达用户** — 应在降级路径中处理而不是暴露内部标记。PR #10417 可能相关，但该 PR 处于 needs-author-action。[Issue #10625](zeroclaw-labs/zeroclaw Issue #10625)
- **#10721 `knowledge.db_path` 的波浪号展开是全局替换而非主目录前缀** — 路径中包含 `~` 的目录会被错误替换，导致知识工具被静默丢弃。暂无对应 fix PR。[Issue #10721](zeroclaw-labs/zeroclaw Issue #10721)
- **#10723 缓存输入零回退抑制了定价缺失警告** — 当输入费率缺失时，缓存的 0.0 回退掩盖了配置错误。[Issue #10723](zeroclaw-labs/zeroclaw Issue #10723)
- **#10662 OAuth 系统前缀缓存标记低于 Anthropic 最小缓存要求** — 占用四个断点槽位之一且不生效。[Issue #10662](zeroclaw-labs/zeroclaw Issue #10662)

### 🟡 轻微问题（S3）

- **#10720 zerocode v0.8.5 聊天窗格回复显示两次** — 仅显示问题，工具调用只触发一次。PR #10672 可能相关。[Issue #10720](zeroclaw-labs/zeroclaw Issue #10720)
- **#10690 Integrations 页面 "Configure" 链接错误** — Z.AI 显示名被 slugify 导致路径不存在。已有对应 PR #10714 提交。[Issue #10690](zeroclaw-labs/zeroclaw Issue #10690)
- **#5514 Telegram 媒体组被拆分为多个多模态轮次** — 用户发送多张图片时产生多条输出，影响对话体验。[Issue #5514](zeroclaw-labs/zeroclaw Issue #5514)

### ⚪ 其他

- **#10700 成本记录携带守护进程生命周期会话 ID，无法按会话拆分** — 字段名具有误导性，影响成本归因。[Issue #10700](zeroclaw-labs/zeroclaw Issue #10700)
- **#10701 图片附件使整个历史缓存前缀失效** — 兼容提供商缓存直通场景下的缓存效率问题。[Issue #10701](zeroclaw-labs/zeroclaw Issue #10701)
- **#10699 缓存写入按普通输入费率计价** — 低估成本，PR #10716 已覆盖。[Issue #10699](zeroclaw-labs/zeroclaw Issue #10699)
- **#10316 SOP 步骤预算耗尽可能将已接受的取消覆盖为 Failed** — 竞态条件，暂无修复。[Issue #10316](zeroclaw-labs/zeroclaw Issue #10316)

---

## 功能请求与路线图信号

以下功能请求值得关注，部分已有对应 PR，可能进入下一版本：

### 高概率进入下一版本（已有实现 PR）

- **#10663 可配置的 Anthropic 1 小时 prompt-cache TTL** — 社区明确要求支持 1 小时 TTL。PR #10623 已在实现相邻功能（OpenAI-compatible 提供商的缓存直通），TTL 配置可能作为后续扩展。[Issue #10663](zeroclaw-labs/zeroclaw Issue #10663)
- **#8763 ZeroCode 显示子代理活动与可展开的工具结果** — 已有 PR #10295（展开工具转录卡片）和 #9739（多会话面板）在推进。[Issue #8763](zeroclaw-labs/zeroclaw Issue #8763)
- **#10725 ZeroCode 结构化渲染工具输入** — 将 JSON 展示为可读的标签字段。与 #8763 同属 ZeroCode 可观测性改进方向。[Issue #10725](zeroclaw-labs/zeroclaw Issue #10725)

### 需要维护者决策（needs-maintainer-review）

- **#10706/#10707/#10708/#10704 OpenAI Responses 系列增强** — 四个功能请求（保留推理状态、支持程序化工具调用、异步函数工具、WebSocket 主动响应引导）均已标记需要维护者审核，说明这是有规划的方向但尚未确认范围。[#10706](zeroclaw-labs/zeroclaw Issue #10706) [#10707](zeroclaw-labs/zeroclaw Issue #10707) [#10708](zeroclaw-labs/zeroclaw Issue #10708) [#10704](zeroclaw-labs/zeroclaw Issue #10704)

### 流程改进信号

- **#10549 RFC 投票流程简化** — 取消强制讨论窗口、让 REVISE 立即停止当前快照。反映了社区对当前 RFC 流程效率的不满，维护者正在响应。[Issue #10549](zeroclaw-labs/zeroclaw Issue #10549)

---

## 用户反馈摘要

- **成本透明性是强需求**："Spent today: $0.0000 只是表面问题，真正危险的是预算上限永远不会触发" —— #9816 的反馈直指成本保护功能形同虚设。这属于**财务安全**级别的痛点，用户信任度影响较大。[#9816](zeroclaw-labs/zeroclaw Issue #9816)
- **Telegram 媒体组体验**：用户报告发送多张图片时，每个图片都触发一次 LLM 请求，导致输出碎片化 ——"应在一个多模态轮次中批量处理"。[#5514](zeroclaw-labs/zeroclaw Issue #5514)
- **ZeroCode 展示层 Bug 反馈积极**：v0.8.5 中消息重复渲染、ACP 转录不完整等问题被社区及时报告，说明 ZeroCode 有真实用户群在使用。cripto
- **配置路径敏感**：`~` 展开错误导致知识工具被静默丢弃（#10721），此类问题虽不严重但对用户信任有长期影响。
- **对 RFC 流程有明确意见**：#10549 中用户指出 48/72 小时固定讨论窗口“常常没有带来更多审查”，反映了社区希望流程更务实、节奏更快。

---

## 待处理积压

### 需维护者关注（needs-maintainer-review / blocked）

- **#9487 与 #9488 两个架构 RFC**：分别进入第 5 版和第 10 版修订，评论数 35/28，等待维护者开启新一轮讨论窗口与投票。[#9487](zeroclaw-labs/zeroclaw Issue #9487) [#9488](zeroclaw-labs/zeroclaw Issue #9488)
- **PR #10241 恢复受监管 shell 审批路由**（size:XL, blocked）：影响所有渠道的 shell 工具安全性，阻塞时间较长。[PR #10241](zeroclaw-labs/zeroclaw PR #10241)
- **PR #9739 ZeroCode 多会话面板**（

</details>