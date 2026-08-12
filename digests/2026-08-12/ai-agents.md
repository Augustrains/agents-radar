# OpenClaw 生态日报 2026-08-12

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-12 00:52 UTC

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

# OpenClaw 项目动态日报 — 2026-08-12

## 今日速览

过去24小时项目活跃度极高：共处理500条Issue更新（390条活跃/新开、110条关闭）和500条PR更新（280条待合并、220条已合并/关闭），无新版本发布。社区焦点集中在**静默回复失败复发**（#121058，62条评论）、**记忆信任标签**（#7707，37条评论）和**多个P1级消息丢失/会话状态问题**。值得注意的是，两个P0/P1级严重问题（#121675 发布事故、#89315 内存泄漏）已在今日关闭，显示维护团队修复效率较高。但仍有大量标注 `clawsweeper:no-new-fix-pr` 的P1问题长期积压，**项目稳定性仍是社区最关心的议题**。

---

## 版本发布

今日无新版本发布。⚠️ 注意：昨日（08-10）发布的 `2026.8.1-beta.1` 曾因未同步发布配套 `@openclaw/*` 插件导致启动引导循环（#121675），该问题已于今日关闭（见下文Bug与稳定性），但请用户在升级前务必确认插件版本对齐。

---

## 项目进展

今日共关闭110个Issue和220个PR，以下为值得关注的合并/关闭项：

### 🐛 严重Bug修复（已关闭）

| 编号 | 标题 | 影响 | 状态 |
|------|------|------|------|
| [#121675](https://github.com/openclaw/openclaw/issues/121675) | 2026.8.1-beta.1发布事故：缺配套插件致启动引导循环 | P0, crash-loop | ✅ 已关闭 |
| [#89315](https://github.com/openclaw/openclaw/issues/89315) | Gateway堆内存无限增长致cgroup OOM | P1, crash-loop | ✅ 已关闭 |
| [#96827](https://github.com/openclaw/openclaw/issues/96827) | message_tool_only模式下代理交付后不终止运行 | P1, message-loss | ✅ 已关闭 |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic思考签名重放间歇性无效 | P1, session-state | ✅ 已关闭 |
| [#92460](https://github.com/openclaw/openclaw/issues/92460) | 孤立Cron完成通知丢失指定投递频道 | P3 | ✅ 已关闭 |

### 🔄 关键架构重构（PR）

- [#122318](https://github.com/openclaw/openclaw/pull/122318) **拆分Agent与Chat编排所有权**（已关闭）：将大型单体模块拆分为可独立审查的组件，降低维护复杂度。
- [#122339](https://github.com/openclaw/openclaw/pull/122339) **整合公共制品解析逻辑**（已关闭）：消除Web提供方解析器中的重复代码。

### 📋 待合并的重要PR

- [#122360](https://github.com/openclaw/openclaw/pull/122360) 隔离聊天测试fixture与provider发现，提升测试稳定性
- [#121299](https://github.com/openclaw/openclaw/pull/121299) 将prepared-model刷新范围限制在变更的agent上，降低O(N)阻塞
- [#121327](https://github.com/openclaw/openclaw/pull/121327) 冻结已安装工具配置文件权限（安全加固）

**整体评价**：项目在修复稳定性问题的同时持续推进架构整洁度，但大量PR处于 `⏳ waiting on author` 状态（如 #120933、#121818、#122350等），**维护者响应速度可能成为瓶颈**。

---

## 社区热点

### 🔥 热议榜首

**[#121058 - Silent reply failures still recurring after #116277 closed](https://github.com/openclaw/openclaw/issues/121058)**（62条评论）
- **诉求**：用户明确表达对"问题关闭但实际未修复"的不满——监控Cron在Issue关闭后仍持续记录新故障。这是对项目**Issue闭环管理流程**的信任危机信号。

**[#7707 - Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)**（37条评论，P2）
- **诉求**：防止通过网页、第三方技能注入的恶意指令污染Agent记忆（记忆投毒攻击）。虽为2月提出，但持续获得关注，**安全类功能需求旺盛**。

**[#92201 - Anthropic思考签名重放失败](https://github.com/openclaw/openclaw/issues/92201)**（22条评论，已关闭）
- **诉求**：嵌入式Runner（Slack插件）间歇性失败，且恢复逻辑因错误信息泛化而失效。用户对**可观测性**和**错误信息精确性**有明确需求。

### 💰 成本失控事件

**[#119009](https://github.com/openclaw/openclaw/issues/119009) - 失控重试循环账单$204**（已关闭）：Discord会话卡在模型重试循环中，3h11m内调用1,081次，3h21m内252次，总成本 $204.74。用户指出"每次重试都重置进度时钟"导致停滞检测失效——**暴露了成本防护机制的盲区**。

---

## Bug 与稳定性

### 严重级别排列

| 严重度 | 编号 | 摘要 | 有无Fix PR |
|--------|------|------|------------|
| **P1** | [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败复发（#116277修复无效） | 🔍 无（需重新调查） |
| **P1** | [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex长回复在~1000-1100字符处被静默截断（stop=null） | 🔍 无 |
| **P1** | [#121953](https://github.com/openclaw/openclaw/issues/121953) | DeepSeek上Cron Agent停滞：`[cron:`前缀被边缘节点降级 | 🔍 无 |
| **P1** | [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex-backed Telegram回合超时（2026.5.27回归） | 🔍 无 |
| **P1** | [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后write/exec工具参数被静默丢弃 | 🔍 无 |
| **P1** | [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM嵌入运行中止memory_search并误判为超时 | 🔍 无 |
| **P1** | [#47975](https://github.com/openclaw/openclaw/issues/47975) | 子代理会话完成后主会话无响应 | 🔍 无 |
| **P1** | [#97616](https://github.com/openclaw/openclaw/issues/97616) | 钩子/工具子进程泄漏，僵尸进程累积致性能下降 | 🔍 无 |
| **P1** | [#114020](https://github.com/openclaw/openclaw/issues/114020) | 升级2026.7.2-beta.4后飞书/Telegram事件分发失败 | 🔍 无 |
| **P1** | [#98435](https://github.com/openclaw/openclaw/issues/98435) | MCP回环传输在网关重启后不自动重连（recovered=1误导） | 🔍 无 |
| **P0** | [#121675](https://github.com/openclaw/openclaw/issues/121675) | 2026.8.1-beta.1发布事故（缺插件） | ✅ 已关闭（修复方案已出） |

**关注点**：今日活跃的P1 Bug均集中在 **消息丢失（message-loss）** 和 **会话状态异常（session-state）** 两类，且多数标注 `no-new-fix-pr`。此外，[#89315](https://github.com/openclaw/openclaw/issues/89315) 的内存泄漏问题虽已关闭，但同类风险需持续监控。

---

## 功能请求与路线图信号

### 高潜力候选（有对应PR或高评论量）

| 编号 | 功能 | 信号强度 | 说明 |
|------|------|----------|------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 记忆信任标签（按来源标记信任级别） | ⭐⭐⭐ 37条评论 | 安全需求强烈，但尚未见PR |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | Control UI支持MathJax/LaTeX渲染 | ⭐⭐⭐ 10个👍 | 呼声高，实现成本低，可快速收割好评 |
| [#68596](https://github.com/openclaw/openclaw/issues/68596) | 可配置流式看门狗超时阈值 | ⭐⭐ 8个👍 | 解决长思考模型（kimi-k2.5、DeepSeek-R1）误报问题 |
| [#14785](https://github.com/openclaw/openclaw/issues/14785) | 减少工具Schema Token开销（~3,500 tok/会话） | ⭐⭐ 9条评论 | 成本优化刚需，有明确优化空间 |

### 新提交/值得关注

- **[#122350](https://github.com/openclaw/openclaw/pull/122350)** 模型目录读取响应性优化：修复Control UI打开时消耗整核CPU并延迟 `/healthz` 的问题，对大规模安装尤其重要。
- **[#122361](https://github.com/openclaw/openclaw/pull/122361)** 媒体解析部分失败时保留已解析图片：改善多图发送体验（飞书/Telegram场景）。

### 路线图判断

当前社区最强烈的信号是 **"稳定性优先"** ——大量P1级消息丢失问题长时间无修复PR（见积压清单），可能挤压新功能开发资源。短期看，UI体验类小改进（#122237、#122297、#122296）和性能优化PR更可能快速合并。

---

## 用户反馈摘要

### 😠 痛点

- **"问题关闭≠问题修复"**（[#121058](https://github.com/openclaw/openclaw/issues/121058)）：用户监控到Issue关闭后故障仍持续发生，对项目Issue闭环管理信任度下降。
- **成本失控焦虑**（[#119009](https://github.com/openclaw/openclaw/issues/119009)、[#42475](https://github.com/openclaw/openclaw/issues/42475)）：模型重试循环可累计$204账单，用户亟需gateway级成本预算控制。
- **升级风险**（[#121675](https://github.com/openclaw/openclaw/issues/121675)、[#83337](https://github.com/openclaw/openclaw/issues/83337)）：插件与核心版本漂移可导致频道静默失效，升级流程需更稳健。
- **错误信息模糊**（[#92201](https://github.com/openclaw/openclaw/issues/92201)、[#58957](https://github.com/openclaw/openclaw/issues/58957)）：泛化的错误文本使恢复逻辑失效，用户无法判断是上下文超限还是故障。

### 😊 积极面

- **功能诉求多样**：从LaTeX支持到K8s文档改进、从多Teams机器人到TTS/STT覆盖，显示项目用户群体多样化且活跃。
- **社区贡献热情高**：PR #117166、#117184 等由非维护者提交并在持续迭代，"ready for maintainer look"状态PR数量较多。

---

## 待处理积压

### 🔴 需优先关注（P1级 + 长期无Fix PR）

| 编号 | 摘要 | 创建时间 | 已积压 |
|------|------|----------|--------|
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex-backed Telegram回合超时 | 05-28 | 76天 |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM中止memory_search误判超时 | 04-29 | 105天 |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | write/exec工具参数静默丢失 | 03-24 | 141天 |
| [#47975](https://github.com/openclaw/openclaw/issues/47975) | 子代理会话后主会话无响应 | 03-16 | 149天 |
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | A2A sessions_send重复消息 | 03-08 | 157天 |
| [#47910](https://github.com/openclaw/openclaw/issues/47910) | 提供商故障分类与隔离（未区分认证失败） | 03-16 | 149天 |

### 🟡 重要功能需求（长时间无产品决策）

| 编号 | 摘要 | 等待决策天数 |
|------|------|-------------|
| [#42475](https://github.com/openclaw/openclaw/issues/42475) | Gateway级每Agent成本预算 | 155天 |
| [#66252](https://github.com/openclaw/openclaw/issues/66252) | 每Agent TTS/STT配置覆盖 | 120天 |
| [#71058](https://github.com/openclaw/openclaw/issues/71058) | 单网关多Azure/Teams机器人 | 110天 |

### 📌 给维护者的提醒

1. **#121058 优先级应为P0**：用户已明确表示Issue关闭但故障未止，这是流程信任问题，需立即重新开启调查。
2. **系统清理 `no-new-fix-pr` + `needs-product-decision` 组合标签的Issue**：目前有大量P1/P2问题同时挂这两个标签，说明产品决策环节阻塞了修复推进。
3. **CI覆盖缺口**（[#122029](https://github.com/openclaw/openclaw/issues/122029)，已关闭）：Telegram分发的17个测试文件（~8k LOC）未在任意CI lane执行，虽已关闭但需跟踪防止回归。

---

*数据来源：[OpenClaw GitHub](https://github.com/openclaw/openclaw) | 报告生成时间：2026-08-12*

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期：** 2026-08-12
**数据来源：** OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、NullClaw、IronClaw、LobsterAI、TinyClaw、Moltis、CoPaw、ZeptoClaw、ZeroClaw 等 13 个开源项目 GitHub 仓库

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态目前处于**高活跃度的深度迭代期**，头部项目（OpenClaw、Hermes Agent、ZeroClaw）日均 PR/Issue 处理量均超过百条，社区规模与用户期望值同步攀升。核心矛盾已从"功能有无"转向"**稳定性与信任**"——消息静默丢失、成本失控、升级事故、问题关闭但未真正修复等事件在多项目中集中涌现，正在消耗社区信任储备。与此同时，安全性诉求显著升级：记忆投毒防护、API Key 泄漏、命令执行沙箱绕过、高风险操作确认机制成为跨项目共性刚需。技术路线分化明显，OpenClaw 与 IronClaw 分别向"平台化网关"和"内核化调度"两个方向演进，反映了生态在规模化过程中对架构边界的不同思考。

---

## 2. 各项目活跃度对比

| 项目 | Issues（新增/活跃） | PR（待合并/已合并关闭） | Release | 健康度评估 |
|------|-------------------|----------------------|---------|-----------|
| **OpenClaw** | 500 条更新（390 活跃/110 关闭） | 500 条更新（280 待合并/220 已合并） | 无 | 🟢 高活跃、修复效率高，但 P1 积压较多 |
| **NanoBot** | 6 条（几乎全部闭环） | 140 条（21 待合并/119 已合并） | 无 | 🟢 极高吞吐、闭环快，但有安全 Issue 未确认修复 |
| **Hermes Agent** | 50 条（48 活跃/2 关闭） | 50 条（43 待合并/7 已合并） | 无 | 🟡 高活跃但 PR 积压严重，Windows 问题簇突出 |
| **IronClaw** | 23 条（13 活跃/10 关闭） | 50 条（25 待合并/25 已合并） | 无 | 🟢 修复-验证闭环良好，架构重构期 |
| **CoPaw** | 23 条 | 49 条（24 待合并/25 已合并） | ✅ v2.1.0-beta.3 | 🟢 迭代节奏健康，社区反馈响应好 |
| **ZeroClaw** | 50 条（40 活跃/10 关闭） | 50 条（48 待合并/2 已合并） | 无 | 🟡 安全加固积极但 PR 积压量大 |
| **LobsterAI** | 4 条 | 10 条（3 待合并/7 已合并） | ✅ 2026.8.11 | 🟢 稳定增量迭代，积压问题较少 |
| **NanoClaw** | 1 条 | 8 条（5 待合并/3 已合并） | 无 | 🟢 功能推进明确，但高严重度 Bug 待修 |
| **PicoClaw** | 3 条（2 开/1 关） | 6 条（全部待合并） | 无 | 🟡 社区活跃但合并通道堵塞（4 PR 已 stale） |
| **Moltis** | 0 条 | 2 条待合并 | 无 | 🟡 开发节奏平稳但社区偏冷，PR 审阅周期偏长 |
| **NullClaw / TinyClaw / ZeptoClaw** | 无活动 | 无活动 | 无 | ⚪ 休眠状态 |

---

## 3. OpenClaw 在生态中的定位

**优势：**
- **社区规模断层第一**：单日 500 条 Issue/PR 更新，远超第二名（IronClaw/NanoBot 各 50-140 条），用户基数与贡献者生态具备明显领先优势
- **平台化集成深度**：覆盖 Discord、Telegram、飞书、Slack、微信等主流渠道，适配广度领先
- **修复响应速度**：P0/P1 级问题（发布事故 #121675、内存泄漏 #89315）均在当日关闭，说明维护团队具备快速响应能力

**技术路线差异：**
- 与其他项目相比，OpenClaw 更像"**Agent 网关 + 编排平台**"——重心在消息路由、会话状态管理、多渠道统一接入，而非 Agent 内核本身
- IronClaw 正走向相反方向（kernel 化，将 loop/工具外置为 ACP 代理），NanoBot 则以轻量脚本化部署见长，三者技术哲学形成鲜明对照

**社区信任风险：**
- "问题关闭≠问题修复"（#121058）引发信任危机，且大量 P1 级消息丢失问题长期无 Fix PR（最长积压 157 天），是生态龙头当前最需要警惕的短板

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **消息可靠性** | OpenClaw（#121058 静默回复失败）、NanoClaw（#3226 消息 ID 复用静默丢弃）、Hermes（#83683 网关被杀消息全静默）、LobsterAI（#1240 故障全局传染） | 消息丢失必须有日志/警告，故障需隔离而非扩散 |
| **成本控制** | OpenClaw（#119009 失控重试 $204 账单、#42475 成本预算）、NanoBot（#5256 死循环重复回复）、PicoClaw（#3317 缓存 token 可见性） | Gateway 级每 Agent 成本预算、重试循环防护、成本可观测性 |
| **安全与沙箱** | NanoBot（#5306 shell 绕过、#4783 API Key 泄漏）、ZeroClaw（#9883 WebP 无界解码、#9887 工作区越界、#7155 高风险命令确认）、CoPaw（#6916 插件静默创建定时任务）、OpenClaw（#7707 记忆投毒） | 命令执行沙箱加固、凭据隔离、高风险操作需用户确认、外部注入防护 |
| **多模型故障隔离** | LobsterAI（#1240 单模型受限拖垮全局）、NanoBot（#1199 fallback model）、Hermes（#84169 严格模式 400） | 模型级故障隔离与自动切换 |
| **Windows 平台体验** | Hermes（#63717 更新失败问题簇）、ZeroClaw（#9182 PowerShell 原生支持）、LobsterAI（#1183 网关遮罩循环） | Windows 打包/更新链路架构级重构、原生 shell 支持 |
| **MCP 生态集成** | NanoClaw（#3092/#3221 远程 Streamable HTTP MCP 全量落地）、CoPaw（#6732 MCP 工具失效、#6874 超时配置）、IronClaw（#7508 MCP 端点验证） | MCP 连接稳定性、超时策略、热重载 |
| **互操作性/协议兼容** | ZeroClaw（#8603 OpenAI Chat Completions 协议）、OpenClaw（#92201 Anthropic 签名重放） | 支持 OpenAI 协议以接入 Open WebUI/LobeChat 等生态工具 |
| **可观测性** | OpenClaw（#92201 错误信息模糊）、IronClaw（#7485 token 估算器双重计数）、PicoClaw（#3317 缓存 token 记录） | 错误信息精确分类、token/成本/缓存状态可见 |

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 关键架构特征 |
|------|---------|---------|------------|
| **OpenClaw** | Agent 网关/编排平台 | 多渠道重度用户、生产部署 | 插件化渠道适配器、统一消息路由，集成广度优先 |
| **Hermes Agent** | 全功能桌面智能体 | Windows/macOS 桌面用户、IM 重度使用者 | 桌面端 + 网关双进程架构，覆盖微信/QQ/Telegram等国内渠道 |
| **NanoBot** | 轻量脚本化 Agent | 开发者、个人自动化场景 | Python 轻量实现，Provider 生态拓展活跃，部署门槛最低 |
| **IronClaw** | Agent 内核/调度层 | 架构研究者、多租户部署者 | 正转型为 kernel（只做调度/租户/审计，loop 外置为 ACP 代理），mem0 内存层深度集成 |
| **ZeroClaw** | 安全优先的企业级 Agent | 安全敏感型企业、Rust 技术栈团队 | Rust 实现，RFC 驱动开发，SOP 成熟度框架，安全策略管线 |
| **CoPaw** | 桌面 AI IDE/对话助手 | 开发者、中文社区 | Console 桌面端 + 文件工作区，v2.1 聚焦 MCP 稳定性与前端体验 |
| **LobsterAI** | 桌面 AI 协作工具 | 中文知识工作者 | Electron 桌面端 + Cowork 多 Agent 协作，深度集成 OpenClaw 网关 |
| **NanoClaw** | 极简 Agent 运行时 | 轻量部署爱好者 | 模板/插件系统演进中，远程 MCP 支持完整 |
| **PicoClaw** | 轻量自托管 Agent | 树莓派/边缘设备用户 | 主打低资源占用（Raspberry Pi + DeepSeek 典型场景），渠道适配器精简 |

---

## 6. 社区热度与成熟度

**第一梯队 — 生态主导（快速迭代 + 大规模社区）：**
- **OpenClaw**：用户基数与 Issue 量断崖式领先，已形成"插件生态 + 渠道矩阵"的平台效应，但稳定性问题开始在规模效应下集中暴露

**第二梯队 — 高速迭代（功能推进 + 社区建设期）：**
- **NanoBot**：PR 吞吐量极高（119 合并/日），性价比路线吸引大量长尾用户，但安全响应机制待完善
- **IronClaw**：处于架构重构期（reborn），缺陷收敛速度快，社区以开发者/架构爱好者为主
- **CoPaw**：迭代节奏健康（版本周更），中文社区活跃，v2.1 已进入发布冲刺阶段

**第三梯队 — 质量巩固（功能补充 + 稳定性打磨）：**
- **Hermes Agent**：功能覆盖面广但受 Windows 平台问题簇拖累，PR 积压 43 条存在合并瓶颈
- **ZeroClaw**：安全加固投入大、架构规划清晰，但 48 条 PR 积压反映评审通道不够通畅
- **LobsterAI**：稳定增量迭代，功能落地快（当日合并 7 PR），但积压的跨月 PR/Issue 需要处理

**第四梯队 — 低活跃/休眠：**
- **PicoClaw / Moltis**：社区反馈质量高但合并通道堵塞/审阅周期过长，贡献者积极性面临流失风险
- **NullClaw / TinyClaw / ZeptoClaw**：24 小时无任何活动，或已进入停更状态

**质量巩固阶段的特征信号：** 关闭速度 > 新开速度（IronClaw、NanoBot）、发布前专项验证（CoPaw #6914）、CI 强制质量门禁（ZeroClaw rustdoc 检查）。

---

## 7. 值得关注的趋势信号

**① "稳定性优先"已成共识，但投入产出比存在分化**
OpenClaw 大量 P1 消息丢失问题积压超 100 天（#53408 积压 141 天、#47975 积压 149 天），而 IronClaw、NanoBot 的 P1 修复周期多在 48 小时内。**头部项目的"规模诅咒"开始显现**——用户越多，Issue 噪音越大，核心问题被淹没的风险越高。

**② 安全诉求从"功能"变成"底线"**
记忆投毒防护（OpenClaw #7707）、shell 绕过（NanoBot #5306）、WebP 无界解码（ZeroClaw #9883）、API Key 隔离（NanoBot #4783/#4784）、插件权限模型（CoPaw #6916）——**安全不再是企业级项目的专属话题，而是所有个人 AI 助手的准入门槛**。趋势指向"默认安全"设计：最小权限、沙箱执行、用户确认机制。

**③ 互操作性与协议标准化开始形成共识**
ZeroClaw 的 Chat Completions 协议兼容诉求（接入 Open WebUI/LobeChat 等）、OpenClaw 的 Anthropic 签名问题、NanoClaw 的远程 MCP 落地——**生态正在从"各做各的"走向"对接标准协议"**。对开发者意味着：优先实现 OpenAI 兼容接口和 MCP 支持，可最大化生态互操作收益。

**④ 成本可观测性成为刚需**
OpenClaw 的 $204 成本失控事件、PicoClaw 的缓存 token 可见性 PR、IronClaw 的 token 估算器缺陷——**用户开始要求"每一分钱花在哪里"的透明度**。可配置流式看门狗超时、工具 schema 压缩、重试预算控制等成本优化方向将受到持续关注。

**⑤ Windows 正在成为"一等公民"战场**
Hermes 的 Windows 更新问题簇、ZeroClaw 的 PowerShell 原生支持、LobsterAI 的 Windows 遮罩循环——**多个项目同时遭遇 Windows 平台适配瓶颈**。这暗示桌面端用户占比在上升，但打包/更新/权限管理链路普遍需要架构级重构。

**⑥ Agent 架构边界讨论升温**
IronClaw 的 "kernel 化" Epic（#7482）、OpenClaw 的 Agent/编排拆分（#122318）、ZeroClaw 的安全策略管线 RFC（#7142）——**社区开始认真追问"Agent 运行时应该包含什么、不应该包含什么"**。对开发者而言，这意味着未来框架的职责边界将更加清晰，可组合性（composability）将成为选型新维度。

---

*报告生成时间：2026-08-12 | 基于 13 个开源项目的 GitHub 公开数据*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-12

## 1. 今日速览

NanoBot 项目今日处于**高活跃度**状态。过去 24 小时共有 140 条 PR 更新（其中 119 条已合并或关闭）和 6 条 Issue 更新，尽管新版本发布为 0，但代码合并量与社区参与度均处于近期高位。值得关注的是，今日关闭的 PR 中有 9 条被标记为 `[conflict]`，暗示仓内可能存在分支冲突或重复贡献问题，需要维护者留意。安全类 Issue（#5306、#4784、#4783）与重复回复类 Bug（#5327、#5256）共同构成了当前社区反馈的主要关切点，且均有对应的修复 PR 在途或已合并。

- 活跃度评估：**高** — PR 吞吐量可观，Issue 闭环速度快，安全响应机制运转正常。


## 3. 项目进展

### 今日合并/关闭的 PR 中值得关注的改动方向

| PR | 方向 | 说明 |
|---|---|---|
| [#2181](https://github.com/HKUDS/nanobot/pull/2181) | 新 Provider | 添加小米 MiMo API 支持（OpenAI 兼容端点），同步修复 provider 名称转换逻辑 |
| [#1367](https://github.com/HKUDS/nanobot/pull/1367) | Provider 增强 | 支持 kimi-coding 模型映射，修正 coding 端点 URL 规范化，补充单元测试 |
| [#1094](https://github.com/HKUDS/nanobot/pull/1094) | 新 Provider | 新增 OpenCode Zen 作为 LLM Provider，提供免费模型与更宽松的速率限制 |
| [#1199](https://github.com/HKUDS/nanobot/pull/1199) | 容错增强 | 实现 fallback model 机制：主模型遇到超时、限流、5xx 时自动切换到备用模型（resolves #1121） |
| [#1114](https://github.com/HKUDS/nanobot/pull/1114) | Cron 能力 | 为 cron 任务添加热重载支持，通过 mtime 检测外部文件变更，减少手动重启 |
| [#1020](https://github.com/HKUDS/nanobot/pull/1020) | Telegram 集成 | 添加 Telegram 内联键盘支持，支持确认对话框、快速操作、菜单响应等交互 |
| [#1002](https://github.com/HKUDS/nanobot/pull/1002) | Cron 增强 | 将渠道元数据（如 Slack thread_ts）从触发消息透传到 cron 任务负载，确保回复到正确的线程 |
| [#1321](https://github.com/HKUDS/nanobot/pull/1321) | 搜索能力 | 加入 Tavily 搜索引擎作为 Brave Search 的替代方案，针对 LLM/AI Agent 优化了检索相关性 |

> 这些合并的 PR 使项目在 **Provider 生态丰富度、容错机制、Telegram 交互深度、定时任务灵活性** 四个维度上均取得了实质性进展。


## 4. 社区热点

### 讨论最活跃的 Issue

**#5327 — [CLOSED] Nanobot 推理过程中重复输出相同消息**（评论: 9 | 👍: 0）
链接: https://github.com/HKUDS/nanobot/issues/5327

该 Issue 是过去 24 小时内评论数最高的单条 Issue，描述了一个随机出现的症状：机器人在 "reasoning" 阶段重复输出同一句话（如 “Good points, let me investigate the issue”）。该问题已关闭，但重复输出类问题在社区中的热度值得关注。

### 讨论最活跃的 PR

目前 Pull Requests 的评论数未提供完整数据（多个 PR 的评论字段为 undefined），但评论数最多的 PR 为：

**#5342 — [OPEN] feat(webui): redesign apps discovery**
链接: https://github.com/HKUDS/nanobot/pull/5342

该 PR 对 WebUI 的应用发现体验进行了全面重构：引入 Discover / Installed / All apps 三个视图维度、新增 nanobot.wiki registry 驱动的精选批次（含缓存离线回退）、优化第三方应用 Logo 加载体验。这直接回应了用户对 WebUI 可发现性和扩展生态的核心诉求，预计会是下一版本的重要体验升级。


## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 是否有修复 PR |
|---|---|---|---|
| 🔴 高（安全） | [#5306](https://github.com/HKUDS/nanobot/issues/5306) | `exec.allowPatterns` 存在 shell 链式绕过漏洞，允许执行未预期的命令 | ✅ [#5345](https://github.com/HKUDS/nanobot/pull/5345) 已提交，修改 `shell.py` 并新增测试 |
| 🔴 高（安全） | [#4784](https://github.com/HKUDS/nanobot/issues/4784) | Provider API keys 通过 `os.environ` 全局变量在不同 Provider 之间互相泄漏/覆盖 | ❌ 已关闭，无明确修复 PR |
| 🔴 高（安全） | [#4783](https://github.com/HKUDS/nanobot/issues/4783) | CLI 子进程被传入完整的 `os.environ`，API keys 暴露给第三方应用 | ❌ 已关闭，无明确修复 PR |
| 🟠 中 | [#5256](https://github.com/HKUDS/nanobot/issues/5256) | `/goal` 命令在等待用户回答时产生数十条重复回复，直到用户介入或模型自我识别为死循环 | ✅ [#5257](https://github.com/HKUDS/nanobot/pull/5257) 已提交，在空闲轮次时约束持续目标的延续逻辑 |
| 🟡 低 | [#5327](https://github.com/HKUDS/nanobot/issues/5327) | 推理阶段随机重复同一消息 | ✅ 已关闭（修复已合入） |

此外，PR [#5344](https://github.com/HKUDS/nanobot/pull/5344)（警告而非静默陷入重复工具调用）与 [#5314](https://github.com/HKUDS/nanobot/pull/5314)（按 schema 解码嵌套 JSON 工具参数）也在今日处于开放状态，共同针对 Agent 循环稳定性进行加固。


## 6. 功能请求与路线图信号

| 功能请求 | 来源 Issue | 对应 PR | 状态 | 纳入下一版本可能性 |
|---|---|---|---|---|
| OpenRouter Server Tools 支持（Web Search、Web Fetch、Fusion 等） | [#5333](https://github.com/HKUDS/nanobot/issues/5333) | 无 | Issue 已关闭，未明确拒绝 | ⭐⭐⭐ 社区有明确需求，且技术上已有 v1 版本的基础 |
| 子 Agent 支持可配置的模型预设 | — | [#4291](https://github.com/HKUDS/nanobot/pull/4291) | OPEN | ⭐⭐⭐ 已开放 2 个月，功能完整但可能在等待 review |
| 非 WebUI 渠道的每会话沙箱隔离 | — | [#5283](https://github.com/HKUDS/nanobot/pull/5283) | OPEN | ⭐⭐ 定位为 opt-in 模式，安全团队或感兴趣 |
| 新增网关型 Provider — OrcaRouter（集成 150+ 模型，附带零信任安全层） | — | [#5328](https://github.com/HKUDS/nanobot/pull/5328) | OPEN | ⭐⭐ 新 Provider 通常合并较快，但需评估维护成本 |
| 天气技能 Windows 兼容修复（`curl` 在 PowerShell 中可能被解析为 `Invoke-WebRequest` 别名） | — | [#5341](https://github.com/HKUDS/nanobot/pull/5341) | OPEN | ⭐⭐⭐ 明确 Bug 且有测试，预计会快速合入 |

> 值得留意：`[conflict]` 标签出现在 9 条已关闭 PR 和 4 条开放 PR 上，可能意味着这些 PR 与主分支产生了合并冲突，维护者/贡献者需要处理。


## 7. 用户反馈摘要

- **正面反馈**：Issue #5333 中用户表示"**thank you for creating such an amazing project. I really appreciate it**"，展现了社区对项目的高度认可与依赖。
- **核心痛点：死循环与重复输出**。两个独立 Issue（#5327、#5256）均报告了重复回复问题，表明 Agent 的循环控制仍不稳定。触发条件高度相似：**等待用户输入时 Agent 陷入自我循环**，导致大量资源浪费。已有一个修复 PR（#5257、#5344）在推进，但社区显然希望看到更彻底的解决方案。
- **安全性关切上升**。`allowPatterns` 绕过与 API Key 泄漏问题（#5306、#4784、#4783）正受到社区高度关注。尤其是 Provider API Key 被传递给 CLI 子进程这一隐患，涉及用户的核心资产，值得立即处理。


## 8. 待处理积压

| 类型 | 编号 | 说明 | 已待处理时长 | 建议 |
|---|---|---|---|---|
| Security Issue | [#4784](https://github.com/HKUDS/nanobot/issues/4784) | Provider API keys 全局环境污染（跨 Provider 泄漏/覆盖） | 37 天 | 已关闭但未见修复确认，建议维护者确认是否已在其他 PR 中修复；若无，应重新开启并规划修复 |
| Security Issue | [#4783](https://github.com/HKUDS/nanobot/issues/4783) | CLI 子进程继承完整 `os.environ`，API keys 暴露给第三方应用 | 37 天 | 同上，需确认修复状态 |
| 开放性 PR | [#4291](https://github.com/HKUDS/nanobot/pull/4291) | 子 Agent 使用可配置模型预设 | 62 天 | 功能完整、测试齐备，但长时间未获得 review。若维护者认可方向，建议加速合入；否则应给出明确反馈 |
| 开放性 PR | [#4145](https://github.com/HKUDS/nanobot/pull/4145) | Weather Skill 整合（多文件贡献） | 72 天 | 长时间搁置，可能与 #5341（同方向但聚焦 Windows 修复）存在重叠，建议维护者协调两 PR 合并策略 |

---

*报告生成时间：2026-08-12 | 数据来源：HKUDS/nanobot GitHub 仓库*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-12

---

## 1. 今日速览

过去24小时内，Hermes Agent 项目保持极高活跃度：**50条 Issues 更新**（48条活跃/新开，2条关闭）与 **50条 PR 更新**（43条待合并，7条已合并/关闭），核心话题聚焦于 **Windows 桌面端稳定性回归**（至少 5 个相关问题）、**god-file 拆分重构史诗**（#78647，67条评论）以及**跨进程会话状态管理**。安全与隐私修复（凭据脱敏、WhatsApp 诊断数据脱敏）也在持续推进。值得注意的是，当前 PR 积压严重（43 条待合并），且存在多条长期搁置的 P1/P2 级 Bug（最早可追溯至 5 月下旬），合并节奏需要关注。今日无新版本发布。

---

## 3. 项目进展

> 今日无新版本发布，故省略第 2 节。

今日共 **7 条 PR 被合并/关闭**，其中值得关注的是 **#83906 的后续工作**——该 PR 在 `gateway/channel_directory.py`、`gateway/run.py` 和 `gateway/slash_commands.py` 中移除了阻塞式的 `atomic_json_write()` 调用，显著降低了网关热路径上的文件系统 I/O 延迟。这一模式正在向更多平台适配器扩展（见 PR #84168），表明 **网关性能优化正在进行系统性推进**。

此外，今日新开的 PR 覆盖了多个高价值修复方向：

- **#84174** — 修复后台进程完成通知在 `/new` 之后被错误路由到新会话的问题，直接对应 Issue #83213；
- **#84181** — 修复本地 TTS 提供商输出 Vorbis 而非 Opus 导致平台语音气泡静默劣化的问题，对应 Issue #84102；
- **#84179** — 增强 `hermes doctor` 对半安装 distribution 的检测能力，有助于缓解 Windows 桌面端大量更新失败类问题；
- **#84145** — 为跨进程 turn lease（Issue #67442）新增 DB 存储层，是会话状态持久化的重要基础。

整体来看，项目在 **网关稳定性、Windows 平台体验、会话状态一致性**三个方向上有明确且持续的推进。

---

## 4. 社区热点

### 讨论焦点

| 议题 | 评论数 | 热度判断 |
|---|---|---|
| [#78647 Epic: Shard all 20 god files](https://github.com/NousResearch/hermes-agent/issues/78647) | 67 | 🔥🔥🔥 极高 |
| [#67442 跨进程 turn 序列化：CLI 连续性会话需要 DB 级租约](https://github.com/NousResearch/hermes-agent/issues/67442) | 14 | 🔥🔥 高 |
| [#66616 Skills 索引过期（degraded 状态）](https://github.com/NousResearch/hermes-agent/issues/66616) | 13 | 🔥🔥 高 |
| [#78642 Shard tools/mcp_tool.py](https://github.com/NousResearch/hermes-agent/issues/78642) | 11 | 🔥🔥 高 |

**核心诉求分析：**

- **#78647 的 67 条评论**揭示了社区对**代码可维护性**的强烈关注。`mcp_tool.py` 已达 7,230 行，社区普遍支持将 god-file 拆分确立为长期政策（"all god files are sharded, never reverted"）。这不仅是技术债清理，也反映了项目规模增长后对**工程规范的迫切需求**——一个 7,000+ 行的单文件对任何新贡献者都是巨大的入门门槛。

- **#67442 的持续讨论**聚焦于**多进程会话一致性的边界场景**：当 CLI 通过网关路由键复用同一会话 ID 时，进程间并发写入可能导致状态冲突。社区对该问题的关注表明**会话状态管理**是当前用户最敏感的功能领域之一——直接关系到消息是否丢失、上下文是否错乱。

- **#66616 的自动化探针报警**（索引延迟 29.8 小时，超过 26 小时限制）虽然属于基础设施问题，但 13 条评论说明社区对 **Skills Hub 文档可用性**有真实依赖，值得维护者优先处理。

---

## 5. Bug 与稳定性

### P1 级（严重，需紧急关注）

| Issue | 描述 | 状态 |
|---|---|---|
| [#83683 Desktop 重启杀死网关且不重启 — 回归](https://github.com/NousResearch/hermes-agent/issues/83683) | Windows 桌面端每次重启都会强制终止正在运行的消息网关，且不自动重启。WeChat/QQ/Telegram 全部静默直至手动恢复。0.20.0 版引入的回归。 | 待处理 |
| [#83562 Windows 更新后桌面端报 "backend exited (0)"](https://github.com/NousResearch/hermes-agent/issues/83562) | 手动启动后端可以正常工作，但桌面端无法拉起网关。Repair install 多次尝试无效。 | 待处理 |
| [#63717 Windows 桌面端更新失败 — 7 个关联根因综合分析](https://github.com/NousResearch/hermes-agent/issues/63717) | 跨 3 周的反复更新失败，形成关联根因链。长期未解决。 | 待处理 |

### P2 级（高影响）

| Issue | 描述 | 对应修复 PR |
|---|---|---|
| [#83213 后台进程完成通知被错误路由到 `/new` 之后的新会话](https://github.com/NousResearch/hermes-agent/issues/83213) | 会话状态边界问题，通知投递到错误目标。 | ✅ [#84174](https://github.com/NousResearch/hermes-agent/pull/84174) |
| [#73779 Feishu 多路复用模式下 WebSocket 接收循环崩溃](https://github.com/NousResearch/hermes-agent/issues/73779) | `Future attached to a different loop` 导致网关静默停止接收消息。 | 待处理 |
| [#83427 `browser_exec` 崩溃 — pydantic_core ModuleNotFoundError](https://github.com/NousResearch/hermes-agent/issues/83427) | 桌面端 PYTHONPATH 指向 Hermes venv 导致导入冲突。 | 待处理 |
| [#84102 本地 TTS 输出 Vorbis 而非 Opus](https://github.com/NousResearch/hermes-agent/issues/84102) | 平台语音气泡静默劣化。 | ✅ [#84181](https://github.com/NousResearch/hermes-agent/pull/84181) |
| [#84169 空 `tool_calls` 数组导致严格模式提供商返回 HTTP 400](https://github.com/NousResearch/hermes-agent/issues/84169) | 辅助客户端路径绕过了预发送清洗器，约 80 次错误记录。 | 待处理 |
| [#84172 webhook 平台工具配置被忽略](https://github.com/NousResearch/hermes-agent/issues/84172) | `platform_toolsets.webhook` 键无效，webhook 会话无法访问平台工具。 | 待处理 |

**趋势判断：** Windows 桌面端更新/重启类问题已形成**系统性模式**——`WinError 32`（文件锁定）、`.pyd` 锁、Node 管理权限错误等多个根因相互关联。这暗示 **Windows 平台打包与更新链路需要一次架构级重构**，而非逐个打补丁。已有 **#62792** 提出将桌面端后端从 venv Python 切换到独立解释器，但仍未落地。

---

## 6. 功能请求与路线图信号

### 高潜力纳入下一版本

| Issue | 功能描述 | 关联 PR/状态 |
|---|---|---|
| [#80222 `delegate_task` 支持按调用覆盖模型与 reasoning_effort](https://github.com/NousResearch/hermes-agent/issues/80222) | 当前委托配置全有或全无，用户希望更细粒度控制。3 条评论，社区有真实需求。 | 无关联 PR，待评估 |
| [#83244 Google Antigravity 加入为一等公民 OAuth 提供商](https://github.com/NousResearch/hermes-agent/issues/83244) | 用户希望接入 Claude Sonnet 4.6 / Opus 4.6 / Gemini 3.x 等模型。 | 无关联 PR，待评估 |
| [#49190 Kanban 通知泛化为事件基板](https://github.com/NousResearch/hermes-agent/issues/49190) | 将硬编码的网关消息平台解耦，支持任意 surface 订阅 + 投递适配器注册表。8 条评论。 | 与 #82591 史诗规划相关 |
| [#82056 `terminal` / `execute_code` 支持 `title` 参数](https://github.com/NousResearch/hermes-agent/pull/82056) | 让模型为命令指定人类可读标签，桌面端和 TUI 优先展示更友好的标题。 | ✅ 已有 PR 待合并 |
| [#82243 `execute_code` 内组合延迟工具](https://github.com/NousResearch/hermes-agent/pull/82243) | 允许 execute_code 程序搜索、检查和调用延迟的 MCP/插件工具。 | ✅ 已有 PR 待合并 |

### 路线图信号

- **Kanban 零权威工作节点 + god-file 根除**（#82591 史诗级规划）是一个 3 部分的大计划，涉及工作节点去中心化、持久化发布、安全回收等，值得关注。
- **#79464 分解计划 SL2b-2**（span 级警告与进度恢复事件）表明项目在**可观测性**方向上也在系统性地推进。

---

## 7. 用户反馈摘要

### 真实痛点

- **Windows 桌面端用户反复受更新困扰**（#63717、#83562、#68760、#82186）：*"Repair install 多次尝试仍然复现同样的失败"* — 用户已对自助修复流程失去信心。同类问题已持续 1 个多月，社区耐心正在消耗。

- **消息静默丢失是最高频的抱怨**（#83683、#73779）：*"WeChat (iLink)、QQ bot 和 Telegram 完全静默，直到网关被手动重启"* — 对于依赖即时消息作为前端的生产用户，这类问题直接中断工作流。

- **配置与文档断裂**（#84172）：*"即使显式配置了 `platform_toolsets.webhook`，webhook 会话仍然无法访问平台工具"* — 配置键被静默忽略，用户无法感知错误，只能通过行为差异发现。

- **TTS 输出格式问题**（#84102）：*"任何平台的语音气泡都会静默劣化"* — 用户期望的 Opus 被 Vorbis 替代，且没有任何日志警告。

### 积极信号

- 社区对 **god-file 拆分史诗**（#78647）的支持度高，评论中多强调"这是正确的方向"——用户对项目长期可维护性有期待。
- **#57540**（桌面端泄漏文本围栏语言标识）获得 2 个 👍，虽是小问题但用户会认真反馈 UI 细节。

---

## 8. 待处理积压

### 长期未响应的关键问题

| Issue | 类型 | 创建时间 | 时长 | 说明 |
|---|---|---|---|---|
| [#63717 Windows 桌面更新失败 — 7 根因分析](https://github.com/NousResearch/hermes-agent/issues/63717) | P1 Bug | 2026-07-13 | ~30 天 | 影响所有 Windows 用户，无 assignee |
| [#62792 Desktop 后端使用 venv Python 导致 .pyd 锁](https://github.com/NousResearch/hermes-agent/issues/62792) | P1 Bug | 2026-07-11 | ~32 天 | 已含修复方案但未落地，是 #63717 的根因之一 |
| [#29590 vision_tools.py 硬编码 max_tokens 导致推理模型延迟](https://github.com/NousResearch/hermes-agent/issues/29590) | P2 Bug | 2026-05-21 | ~83 天 | 创建已近 3 个月，仅 2 条评论，无响应 |
| [#57540 桌面端泄漏文本围栏语言标识](https://github.com/NousResearch/hermes-agent/issues/57540) | P3 Bug | 2026-07-03 | ~40 天 | 简单 UI 修复，4 条评论，2 个 👍，未处理 |

### 长期待合并的关键 PR

| PR | 描述 | 创建时间 | 时长 |
|---|---|---|---|
| [#53894 会话拥有的 profile-keyed shell hooks](https://github.com/NousResearch/hermes-agent/pull/53894) | 修复 dashboard/TUI 中 hooks 不生效问题 | 2026-06-28 | ~45 天 |
| [#68608 按分发上下文而非工具存在门控 kanban worker 协议](https://github.com/NousResearch/hermes-agent/pull/68608) | 修复 #68592，与 #82591 史诗相关 | 2026-07-21 | ~22 天 |
| [#67163 Termux 原生安装、TUI 和桌面端支持](https://github.com/NousResearch/hermes-agent/pull/67163) | Android/Termux 端到端支持 | 2026-07-18 | ~25 天 |

### 维护者提醒

1. **Windows 更新链路**（#63717、#62792、#68760、#82186 等）已形成"问题簇"，建议成立专项工作组系统性解决，而非逐个打补丁。
2. **PR 积压 43 条**，其中 #53894 和 #68608 分别等待 45 天和 22 天，可能阻塞 #82591 史诗的推进。
3. **#29590 已搁置 83 天**，作为影响推理模型用户体验的配置缺陷，建议尽快分配或明确优先级。

---

*报告生成时间：2026-08-12 | 数据来源：NousResearch/hermes-agent GitHub 仓库 | 项目版本：0.20.0（自 2026-08-03 起无新版本）*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：** 2026-08-12  
**数据来源：** [github.com/sipeed/picoclaw](https://github.com/sipeed/picoclaw)  
**分析范围：** 2026-08-11 至 2026-08-12

---

## 1. 今日速览

PicoClaw 在过去 24 小时内保持中等活跃度：共产生 3 条 Issue 更新（2 条开启、1 条关闭）和 6 条 PR 更新（全部处于待合并状态），无新版本发布。值得关注的是，今日出现了一个**新旧呼应**的节奏——此前报告的 `webhook_host`/`webhook_port` 配置无效问题（#3328）在当天即获得了修复 PR（#3329），展现了维护团队对社区反馈的快速响应；但另一方面，6 条 PR 全部处于打开状态、0 条被合并，说明代码审查和合并通道存在一定积压。项目当前处于 **"社区活跃、合并通道拥堵"** 的阶段。

---

## 2. 版本发布

过去 24 小时无新版本发布。当前最新版本为 **v0.3.1**（commit `2cf030d2`）。

---

## 3. 项目进展

**今日无 PR 被合并或关闭**，6 条 PR 全部处于待审查状态。但值得注意的是，这些积压的 PR 本身包含了多项重要的功能修复与增强，一旦合并将显著提升项目稳定性：

| PR | 内容概要 | 潜在影响 |
|---|---|---|
| [#3316](https://github.com/sipeed/picoclaw/pull/3316) | 修复路由代理的上下文管理——历史记录、摘要、压缩和 seahorse 引导均不生效 | **高**：直接影响多代理场景下的核心对话记忆功能 |
| [#3314](https://github.com/sipeed/picoclaw/pull/3314) | 修复 `customAllowPatterns` 不生效——默认拒绝模式优先于用户自定义允许模式 | **高**：`git push` 等命令被错误拦截，影响用户自定义权限配置 |
| [#3315](https://github.com/sipeed/picoclaw/pull/3315) | 支持私聊机器人中的 Telegram 话题（Topic）功能 | **中**：扩展了 Telegram 频道适配场景 |
| [#3317](https://github.com/sipeed/picoclaw/pull/3317) | 在 LLM 响应调试输出中记录提示缓存（prompt cache）token | **低-中**：增强可观测性，方便用户监控成本 |
| [#3299](https://github.com/sipeed/picoclaw/pull/3299) | 新增 Exa 原生网页搜索提供商 | **中**：扩展了 `tools.web` 的搜索选项，目前仍为"stale"状态 |
| [#3329](https://github.com/sipeed/picoclaw/pull/3329) | 修复 `line.settings.webhook_host`/`webhook_port` 配置无效——改为发出警告而非静默填充 | **中**：修复了配置被静默忽略的误导性问题，当日提出当日修复 |

> ⚠️ **风险提示**：6 条 PR 中有 3 条被标记为 `[stale]`（#3316、#3315、#3299），若维护者不尽快审查，这些 PR 可能需要额外操作才能保持活跃。其中 #3316 直指 Issue #3301 的根因修复，建议优先处理。

---

## 4. 社区热点

今日讨论热度最高的议题集中在**路由代理的上下文管理缺陷**：

**[Issue #3301 - 路由到非默认代理的会话中 /clear 和自动压缩失效](https://github.com/sipeed/picoclaw/issues/3301)**
- 作者：j-v | 评论：3 条 | 状态：开启中
- 核心诉求：用户通过 dispatch rules 将特定 Discord 频道路由到自定义代理后，该会话完全丢失了跨消息的记忆能力，且无论消息量多大都不会触发自动压缩。作者还在 PR #3316 中提交了对应的修复代码，但尚未被合并。
- 趋势判断：该 Issue 与 PR #3316 形成了强联动——Issue 暴露问题、PR 提供方案，但**修复被审查流程阻塞**，社区的耐心可能在消耗中。

**[Issue #3294 - /list models 只显示当前模型而非全部已配置模型](https://github.com/sipeed/picoclaw/issues/3294)**
- 作者：2suige-coder | 评论：3 条 | 状态：已关闭（stale）
- 核心诉求：用户配置了多个模型，但 `/list models` 命令（描述为"Configured models"）仅显示当前使用的模型和提供商，与命令名称和描述不符，存在功能与预期不一致问题。该 Issue 最终被标记为 `[stale]` 后关闭，但**相关功能尚未确认修复**。

---

## 5. Bug 与稳定性

今日报告了 2 个新 Bug，按严重程度排列如下：

| 严重程度 | Issue | 描述 | 状态 | 是否有修复 PR |
|---|---|---|---|---|
| **中** | [#3301](https://github.com/sipeed/picoclaw/issues/3301) | 路由到非默认代理的会话中 /clear 和自动压缩功能失效（PicoClaw v0.3.1，Raspberry Pi + DeepSeek） | 开启中 | ✅ [#3316](https://github.com/sipeed/picoclaw/pull/3316)（待合并） |
| **低** | [#3328](https://github.com/sipeed/picoclaw/issues/3328) | `line.settings.webhook_host` / `webhook_port` 配置被静默忽略——有默认值、有文档，但代码中无任何消费方 | 开启中 | ✅ [#3329](https://github.com/sipeed/picoclaw/pull/3329)（当日提出） |

**分析：** #3301 涉及核心的上下文管理逻辑，直接影响路由代理场景下的用户体验，属于功能回归级别的问题，建议优先处理。#3328 虽然影响面较小，但其"配置被静默忽略"的特性具有误导性，容易造成排障困难，修复方案（改为警告）思路正确。

**另有一个已关闭的 Bug 记录：**
- [#3294](https://github.com/sipeed/picoclaw/issues/3294) `/list models` 只显示当前模型——已关闭（stale），但功能问题本身是否已解决尚未确认。

---

## 6. 功能请求与路线图信号

当前 PR/Issue 中体现了以下功能演进方向，可作为下一版本的能力预判：

| 功能方向 | 来源 | 实现状态 | 纳入下一版本可能性 |
|---|---|---|---|
| **Exa 搜索提供商**（新增 `tools.web` 选项） | [PR #3299](https://github.com/sipeed/picoclaw/pull/3299) | 代码完整，含配置与测试，待审查 | **高**——功能独立且不影响现有架构 |
| **Telegram 私聊话题支持** | [PR #3315](https://github.com/sipeed/picoclaw/pull/3315) | 修复逻辑明确，改动范围小 | **较高**——适配 Telegram 新特性，提升用户体验 |
| **LLM 响应中记录缓存 token** | [PR #3317](https://github.com/sipeed/picoclaw/pull/3317) | 改动小，纯可观测性增强 | **较高**——对成本敏感用户有实际价值 |
| **Prompt cache 可见性** | 与 #3317 联动 | 由上述 PR 实现 | — |

**结论：** 上述 3 个功能均有较为完整的 PR 实现，一旦合并将进入下一版本。其中 Exa 搜索是最具"新能力"特征的更新，而 Telegram 话题支持则是重要的兼容性改进。

---

## 7. 用户反馈摘要

从近两日的 Issue 和 PR 讨论中，可以提炼出以下真实用户痛点和使用场景：

**痛点一：默认行为与预期不符（来自 #3294）**
> "命令名叫 `/list models`，描述也是 'Configured models'，我自然以为它会列出所有我配置的模型——结果只显示当前使用的模型和提供商。"

→ 用户对命令行为与文档/名称的不一致感到困惑，这类"隐含预期"问题需要维护者在命名或文档层面加以规避。

**痛点二：配置被静默忽略，无任何提示（来自 #3328）**
> "设置 `webhook_host` 或 `webhook_port` 完全没有效果，代码里没有任何地方读取它们，也没有任何警告告诉你这一点。"

→ 用户在无效配置上花费了排障时间，合理期望是"要么生效、要么报错"。修复 PR #3329 提出的"发出警告而非静默填充"正对痛点。

**痛点三：路由代理的会话记忆完全丢失（来自 #3301 & PR #3316）**
> "代理无法记住会话中的任何历史消息，无论消息量多大、token 消耗多少，自动压缩都从不触发。"

→ 这是当前最突出的功能缺陷之一，直接把"多代理路由"场景的可用性拉低了，建议维护者优先合入 PR #3316。

**使用场景亮点：**
- Raspberry Pi + Discord/Telegram + DeepSeek 是典型用户配置（#3301），说明轻量部署 + 国内模型提供商组合有实际需求。
- 有用户通过 Cloudflare AI Gateway 使用 DeepSeek（#3317），对缓存 token 的可见性在意，反映了成本敏感型用户群体。

---

## 8. 待处理积压

以下 Issue/PR 长期未有实质性推进，建议维护者重点关注：

| 项目 | 类型 | 创建时间 | 最后活跃 | 状态 | 建议 |
|---|---|---|---|---|---|
| [#3299 - Exa 搜索提供商](https://github.com/sipeed/picoclaw/pull/3299) | PR | 2026-07-26 | 2026-08-11 | `[stale]` | 已 stale，功能完整，建议安排审查或明确关闭/接手 |
| [#3294 - /list models 只显示当前模型](https://github.com/sipeed/picoclaw/issues/3294) | Issue | 2026-07-25 | 2026-08-11 | 已关闭（stale） | 功能问题未确认修复，建议重新评估或在 CHANGELOG 中说明 |
| [#3316 - 路由代理上下文管理修复](https://github.com/sipeed/picoclaw/pull/3316) | PR | 2026-08-03 | 2026-08-11 | `[stale]` | 与 Issue #3301 强关联，修复核心功能缺陷，建议优先处理 |
| [#3315 - Telegram 私聊话题支持](https://github.com/sipeed/picoclaw/pull/3315) | PR | 2026-08-03 | 2026-08-11 | `[stale]` | 已 stale，改动小、价值明确，建议尽快审查 |

**综合健康度评估：** 项目社区反馈活跃、Bug 报告质量高（均附复现步骤和配置信息），维护者对新 Issue 响应迅速（如 #3328 当天即获修复方案）。但 **PR 合并通道严重堵塞**——6 条待合并 PR 中 4 条已进入 stale 状态，可能影响贡献者积极性。建议维护者在下一轮迭代中优先处理 PR 积压，尤其是 #3316 与 #3314 两个修复类 PR，以稳固项目在多代理场景下的核心竞争力。

---

*本报告由 AI 自动生成，数据基于 PicoClaw 公开 GitHub 仓库信息。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-12**  
**数据周期：2026-08-11 00:00 – 2026-08-12 00:00 UTC**

---

## 1. 今日速览

NanoClaw 项目在过去 24 小时内保持中等偏上的活跃度，核心开发团队（core-team）动作频繁。虽然无新版本发布，但 8 条 PR 更新中 3 条已合并/关闭，显示引擎层面的功能性迭代在持续推进——尤其是 **Agent 模板迁移（#3220）** 与 **远程 Streamable HTTP MCP 支持（#3092/#3221）** 两大方向的落地。Issues 侧仅 1 条新提交，但 **#3226 消息静默丢失** 问题直指消息可靠性核心，严重性较高，社区回应迅速。整体而言，项目处于**功能性架构调整期**，活跃度健康，但需警惕引入破坏性变更带来的兼容性风险。

---

## 2. 版本发布

**无新版本发布。** 最近一次 Release 日期早于本报告周期。当前主干包含多个未发布的破坏性变更（见下文 #3220 分析），维护者需评估收集足够测试反馈后再打 tag。

---

## 3. 项目进展

今日共有 3 条 PR 关闭/合并，推进了两大核心方向：

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#3221](https://github.com/nanocoai/nanoclaw/pull/3221) | feat(providers): remote Streamable HTTP MCP servers for codex and opencode | ✅ 已合并 | 补齐了 #3092 中 codex 与 opencode 提供商对远程 MCP 服务器的支持，使 `{ type: 'http', url }` 配置在这两个通道不再报错。至此，**三大提供商（Claude/codex/opencode）均已支持远程 Streamable HTTP MCP**，该功能线宣告完成。 |
| [#3092](https://github.com/nanocoai/nanoclaw/pull/3092) | feat: support remote Streamable HTTP MCP servers | ✅ 已合并 | 上游基础支持，与 #3221 互为配套，共同构成了完整的远程 MCP 接入能力。 |
| [#3190](https://github.com/nanocoai/nanoclaw/pull/3190) | feat: add Tavily MCP tool skill | ✅ 已关闭（合并） | 新增 Tavily 搜索工具技能，作为独立 utility skill 提供，丰富了 Agent 可用的外部工具生态。 |

**关键进度判断**：远程 MCP 支持从引擎（#3092）到提供商适配（#3221）全链路打通，意味着 NanoClaw 已具备接入基于 HTTP 的现代 MCP 服务器的能力，这是一次**跨版本的功能里程碑**。与此同时，Agent 模板系统（#3220、#2909）仍在推进中，尚未完全合入主干。

---

## 4. 社区热点

### 最受关注 Issue：[#3226](https://github.com/nanocoai/nanoclaw/issues/3226) Inbound messages silently dropped when a platform reuses a message id

- **作者**：dweekly | **创建**：2026-08-10 | **评论**：1 | **状态**：OPEN
- **核心问题**：当平台在同一个会话中复用消息 ID 时，NanoClaw 会**静默丢弃入站消息**，用户侧表现为"Agent 无视了我"。
- **分析**：该问题直击消息传递链路的可靠性痛点——从用户角度看，没有错误提示、没有日志警告，消息凭空消失。这在生产环境中是**P0/P1 级别的体验问题**，尤其是对于依赖消息 ID 去重的系统，复用 ID 的合法性需要被妥善处理（如按会话+时间戳校验）。

---

## 5. Bug 与稳定性

### 今日报告

| 严重级别 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| 🔴 **高** | [#3226](https://github.com/nanocoai/nanoclaw/issues/3226) | 消息 ID 被平台复用时，入站消息被静默丢弃，用户无感知 | **无 fix PR**，仅 1 条评论 |
| 🟠 **中** | [#3145](https://github.com/nanocoai/nanoclaw/issues/3145) | 数据库迁移：现有 wiring 缺少 channel destinations，需要 backfill（PR 已提交，仍开放） | 有修复 PR 待合并 |
| 🟡 **低** | [#3195](https://github.com/nanocoai/nanoclaw/issues/3195) | 升级过程非事务性（update not transactional），升级失败可能导致状态不一致 | fix PR 待合并 |
| 🟡 **低** | [#2134](https://github.com/nanocoai/nanoclaw/issues/2134) | Apple Silicon + Colima 环境变量未写入 launchd plist，导致 setup 后环境异常 | fix PR 开放中（积压较久） |

**趋势判断**：今日无崩溃或回归类报告；#3226 是唯一新报告的 Bug，但严重性高。#3145 的 backfill 迁移是数据完整性修复，已提交 PR 但尚未合并，建议优先处理。

---

## 6. 功能请求与路线图信号

### 强信号：Agent 模板系统进入 1.0 阶段

- **[#3220](https://github.com/nanocoai/nanoclaw/pull/3220)（OPEN，core-team）**：Agent Templates 迁移为 **Agent Plugins 1.0.0 目录结构**。此 PR 是一次**格式迁移（引擎级破坏性变更）**，直接影响所有现有模板的用户。虽标记为 "Fix"（安全硬化向），但核心是模板能力的架构升级。
- **[#2909](https://github.com/nanocoai/nanoclaw/pull/2909)（OPEN，core-team）**：Setup wizard 中新增"如何创建第一个 Agent"的交互流程，支持"全新 Agent"或"从模板创建"，并与 #2890（模板加载器）配套。

**判断**：这两个 PR 共同勾勒出 **Agent 模板 → Agent 插件** 的演进路线，未来 Agent 将具备标准化的目录结构（含 SKILL.md、元数据等），这是 NanoClaw 走向可扩展生态的关键一步。**若 #3220 合入，将属于破坏性变更（feat!），需要配套迁移指南。**

### 中信号：远程 MCP 支持已闭环

#3092 与 #3221 合并后，**远程 Streamable HTTP MCP 支持已全量落地**，用户可跳过 stdio 配置直接通过 URL 接入 MCP 服务器，降低了部署复杂度。

---

## 7. 用户反馈摘要

来自 Issue #3226 的唯一一条评论（社区热议点）：

> 用户核心诉求：**"消息没有被送达、没有报错、没有日志，这比报错更可怕。"**——当系统静默丢弃消息时，用户无法区分是 Agent 忽略还是系统故障，体验接近于"AI 不可用"。

该反馈揭示了当前用户对**消息传递透明性**的强烈需求——期望至少能通过日志或错误提示感知到消息丢失，而非无声无息。此类问题若未及时修复，将影响用户对 Agent 的信任度。

---

## 8. 待处理积压

以下为长期未处理、值得维护者关注的高优先级项目：

| 类型 | 编号 | 标题 | 创建日期 | 已开放天数 | 备注 |
|---|---|---|---|---|---|
| PR | [#2134](https://github.com/nanocoai/nanoclaw/issues/2134) | fix(setup): include Apple Silicon + Colima env vars in launchd plist | 2026-04-29 | **105 天** | 修复 Apple Silicon 用户 setup 后的环境变量问题；长时间未合并，或影响 Mac 用户的首体验 |
| PR | [#3145](https://github.com/nanocoai/nanoclaw/issues/3145) | fix(db): backfill destinations for existing wirings | 2026-07-28 | **15 天** | 数据一致性修复，对已有部署用户重要 |
| PR | [#3195](https://github.com/nanocoai/nanoclaw/issues/3195) | fix(update): make NanoClaw upgrades transactional | 2026-08-06 | **6 天** | 升级安全性，避免中途失败导致的配置损坏 |
| PR | [#2909](https://github.com/nanocoai/nanoclaw/pull/2909) | feat(setup): template setup flow in wizard | 2026-07-02 | **41 天** | 模板系统二期中关键组件，阻塞 Agent Plugin 全流程 |

---

## 项目健康度总评

| 维度 | 评级 | 说明 |
|---|---|---|
| 活跃度 | 🟢 健康 | 核心团队持续 PR，多线并行（MCP 已完成，模板推进中） |
| 稳定性 | 🟡 关注 | 无回归报告，但 #3226 高严重性 Bug 待修 |
| 社区互动 | 🟢 积极 | 外部贡献者活跃（Tavily skill、DB 修复等） |
| 积压管理 | 🟡 一般 | #2134 超 100 天未动，需维护者关注或关闭 |

**风险提示**：#3220（Agent Plugins 1.0）若合入，将引入破坏性格式变更，建议在合并前完成迁移工具与文档，避免社区模板断裂。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-12

## 1. 今日速览

IronClaw 在过去 24 小时活动强度处于**高水平**：合计 73 条 Issue/PR 更新，其中 23 条 Issue 更新（13 条活跃、10 条关闭）与 50 条 PR 更新（25 条待合并、25 条已合并/关闭）。核心维护者 serrrfirat 活跃度极高，主导了本轮 `reborn` 架构下 loop 层、披露层（disclosure）与内存层的密集修复。值得关注的是 **10 个 Issue 被关闭**（其中 6 个为 serrrfirat 提交的 bug 跟踪），侧面反映修复-验证闭环运转良好。当前无新版本发布，但大量 XL 级 PR 处于待合并状态，预计近期会有一次较大的版本聚合。整体判断：项目处于**架构重构（reborn）深化迭代期**，缺陷收敛速度加快，但系统性技术债（token 估算、上下文窗口、重试机制）仍在持续暴露。

---

## 2. 版本发布

过去 24 小时无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 集中于 **loop 层正确性修复**与**基础设施硬化**：

| PR | 影响面 | 关键变更 |
|---|---|---|
| [#7471](https://github.com/nearai/ironclaw/pull/7471) `fix(processes)` | 进程/租约管理 | 租约到期后安全恢复而非失败；隔离 journal 心跳池，避免数据面 PostgreSQL 流量干扰 |
| [#7470](https://github.com/nearai/ironclaw/pull/7470) `fix(threads)` | 线程列表 | 修复无序投影元数据的 thread_index 行在 `list_threads` 中不可见的问题 |
| [#7503](https://github.com/nearai/ironclaw/pull/7503) `fix(loop)` | 上下文窗口 | 在 128 条消息截断与 token 预算内保留已接受的任务；超过预算返回 `BudgetExceeded` 而非静默丢弃 |
| [#6997](https://github.com/nearai/ironclaw/pull/6997) `feat(llm)` + [#6984](https://github.com/nearai/ironclaw/issues/6984) 关闭 | Anthropic 缓存 | 两条传输路径均显式放置 `cache_control` 断点，OAuth 路径此前完全未标记 |
| [#7514](https://github.com/nearai/ironclaw/pull/7514) `fix` | Railway 托管 | 为托管卷配置启用 Railway shell（严格 release-only 开关） |
| [#7480](https://github.com/nearai/ironclaw/pull/7480) `fix(webui)` | WebUI | 长对话标题悬停完整展示（MarqueeText 组件） |

**项目整体推进评估**：今日闭环了多个 reborn 架构下的正确性问题——线程列表可见性、任务保留完整性、Anthropic 缓存策略——同时对进程租约、项目持久化、Railway 托管做了稳定性加固。但 `context window eviction`、`token estimator` 等问题确认了系统性缺陷，说明调度层距生产成熟仍有迭代空间。

---

## 4. 社区热点

今日评论数最多的区域集中在 **serrrfirat 发起的 reborn 架构问题集群**：

- **[#7482: Epic — Pluggable agent loops](https://github.com/nearai/ironclaw/issues/7482)**（3 评论）
  IronClaw 定位从"agent 运行时"转向"**kernel**"——只做调度、租户隔离、能力边界、密钥中介、出口边界、审计；agent loop 和工具代码全部外置为 ACP 代理。3 条评论说明架构方向在维护团队内部有实质讨论。

- **[#7317: Doc-Truth Verification Pipeline](https://github.com/nearai/ironclaw/issues/7317)**（3 评论，已关闭）
  用户 **cuongdcdev** 指出 `origin_gate_matrix` 等字段在稳定发布中成为强制项但文档未同步。最终关闭，值得关注**修复方式**——是文档补齐还是回滚了强制校验。

- **[#7405: Deferred tool discovery 增强](https://github.com/nearai/ironclaw/issues/7405)**（2 评论，已关闭）
  推进了命名空间感知的目录预览。

- **[#7505: 内存目标别名解析移至领域层](https://github.com/nearai/ironclaw/issues/7505)**（1 评论）
  确认 mem0 与原生 provider 在 `target: memory` 上的行为不一致——mem0 原样存储导致 MEMORY.md 读取失败。

**社区诉求解读**：核心讨论围绕**架构边界**——什么是 IronClaw 内核该拥有的、什么是应该外置的。工具披露的并发粒度、内存别名的契约归属、代理循环的可插拔性，本质上都是在回答"kernel 的职责边界在哪里"。

---

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列：

### 高优先级

| Issue | 问题 | 状态 |
|---|---|---|
| [#7485](https://github.com/nearai/ironclaw/issues/7485) | **Token 估算器对 ASCII 双重计数**——按 `bytes/2` 计为 2 chars/token，实际压缩了有效上下文窗口至一半；且存在两个不一致的估算器 | 🔴 OPEN，无 PR |
| [#7484](https://github.com/nearai/ironclaw/issues/7484) | **上下文窗口静默驱逐任务**——128 条消息硬上限在三个独立位置硬编码，用户消息可能被静默移除 | 🟡 有对应 PR [#7504](https://github.com/nearai/ironclaw/pull/7504)（强制压缩信号）与 [#7503](https://github.com/nearai/ironclaw/pull/7503)（已合并，任务保留） |
| [#7490](https://github.com/nearai/ironclaw/issues/7490) | **重试分类表是死代码**——`retry_disposition()` 分类了 ~25 种瞬时错误但从未被调用 | 🟡 OPEN，无 PR |

### 中优先级

| Issue | 问题 | 状态 |
|---|---|---|
| [#7486](https://github.com/nearai/ironclaw/issues/7486) | **无进展逃逸误报**——幂等读/轮询被输出哈希标记为 NoChange，导致长任务被终止 | 🟡 OPEN，无 PR |
| [#7505](https://github.com/nearai/ironclaw/issues/7505) | **mem0 provider 不解析 `target: "memory"` 别名**——MEMORY.md 跨会话读取失败 | 🟢 已有关联 PR [#7512](https://github.com/nearai/ironclaw/pull/7512) |
| [#7508](https://github.com/nearai/ironclaw/issues/7508) | GitHub MCP 扩展启动时显示令人困惑的端点验证提示，而非连接成功 | 🟡 OPEN（QA_BUG，P2） |

### 已关闭（修复验证通过）

- [#7488](https://github.com/nearai/ironclaw/issues/7488)：三个披露工具硬编码 `ConcurrencyHint::Exclusive`——已确认修复（应改为并行安全）
- [#7487](https://github.com/nearai/ironclaw/issues/7487)：`tool_search` 标记已披露但未返回 schema，绕过了 describe-first 安全网——已确认修复

**稳定性总体判断**：今日发现的 bug 集中在 **loop 层与调度层**——token 估算（2 倍误差）、上下文驱逐、幂等误判。这些缺陷相互叠加会显著影响长任务可靠性与小模型场景下的自动化成功率（可对应 #6879）。修复节奏良好，但 token 估算与重试死代码两块尚无 PR，存在累积风险。

---

## 6. 功能请求与路线图信号

| 信号 | 来源 | 判断 |
|---|---|---|
| **#7482: Pluggable agent loops（ACP executor）** | serrrfirat 发起的 Epic | 远期方向——IronClaw 从 agent 运行时转向 kernel。与 [#7513](https://github.com/nearai/ironclaw/pull/7513)（ACP serve 命令）相互印证，ACP 是明确的演进方向 |
| **#7496: 主机中介 IdentyClaw Passport** | discernible-io 发起 | 有实际诉求：passport 私钥/JWT 留在主机侧，但 processless 配置隐藏了 `builtin.shell`。属于生态扩展，短期优先级不高 |
| **#7489: `result_read` 24 KiB 预览上限 + 2000 行不可编辑墙** | serrrfirat 跟踪 | 依赖 #7435（OMP 切换）解决，非独立功能 |
| **#7038: Storybook + AI-first Design System** | rdisandro 的 Epic | PR #7257 提案包已提交，属 v1.3.0 范围——设计系统建设意味着 WebUI 将进入产品化阶段 |
| **#7467: 持久化状态 profile-agnostic** | henrypark133 | 已有实现 PR [#7456](https://github.com/nearai/ironclaw/pull/7456)，合并后 profile 切换不再导致数据"消失" |
| **自动化建议卡片（#7038 关联）** | henrypark133 的 PR #7498 | v1.3.0 功能，后端已完成 |

**下一版本信号**：v1.3.0 的候选清单包括——自动化建议卡片、设计系统、deferred tool discovery 增强（#7405）、显式缓存控制（已完成 #6997）。

---

## 7. 用户反馈摘要

**来自 QA 测试（joe-rlo 连续提交）**：

- **[#7247](https://github.com/nearai/ironclaw/issues/7247)/[#7246](https://github.com/nearai/ironclaw/issues/7246)/[#7294](https://github.com/nearai/ironclaw/issues/7294)（均已关闭）**：agent 在**未检查实际状态**的情况下就声称"GitHub 已连接"、"自动化正在运行"、"Telegram 例程已设置"。这组连续测试暴露了一个**系统性问题**——agent 倾向用自己的内部记忆回答而不是先执行状态查询。
- **正面趋势**：三个 QA 问题在 6 天内全部关闭，修复节奏值得肯定。但核心修复是否触及根本（状态预检机制），需要观察后续 QA 复测。

**来自外部贡献者（cuongdcdev）**：

- **#7317：文档与代码脱节**——"breaking changes 已发布到稳定版但文档未更新"。这是一个**社区信任度风险**：发布流程缺少文档-代码一致性门禁。问题已关闭，但建议维护者确认：
  1. 修复方式是补齐文档还是回滚了强制校验？
  2. 是否引入了防止再次发生的流程门禁？

**来自内部架构讨论**：

- #7482（pluggable agent loops）的评论表明团队在主动讨论**模块边界与 kernel 职责**，项目长期架构方向清晰。

---

## 8. 待处理积压

| 项目 | 类型 | 等待时间 | 风险 | 建议 |
|---|---|---|---|---|
| **[#6879: Automation runs 不稳定](https://github.com/nearai/ironclaw/issues/6879)** | Epic | 7月29日至今（14 天） | 🔴 直接影响小模型上自动化的可用性。即使被标记为 v1.3.0，也建议在 #7485/#7484 修复后重新评估 | |
| **[#5910: approval gates hydration](https://github.com/nearai/ironclaw/pull/5910)** | PR（ironloopai[bot]） | 7月10日至今（33 天） | 🟡 待合并超过一个月。若问题优先级已降低，建议明确关闭或指定 reviewer | |
| **[#7485: token 估算器双重计数](https://github.com/nearai/ironclaw/issues/7485)** | Bug | 1 天 | 🟠 影响上下文窗口计算精度，且无 PR。建议尽快立项——它放大 #7484 与 #6879 的严重性 | |
| **[#7490: retry_disposition 死代码](https://github.com/nearai/ironclaw/issues/7490)** | Bug | 1 天 | 🟡 死代码意味着瞬时错误无法静默重试，可能直接导致 #6879 中 hit-or-miss 问题 | |
| **[#7508: GitHub MCP 端点验证困惑](https://github.com/nearai/ironclaw/issues/7508)** | QA_BUG (P2) | 1 天 | 🟡 MCP 扩展的启动体验问题，可能会影响新用户对 MCP 集成的信任 | |

---

**整体健康度评估**：项目处于高活跃度的架构重构期——短期缺陷收敛迅速，但 token 估算、重试机制、上下文驱逐三个系统性问题相互交织，建议优先以"长任务可靠性"为目标做一次集中梳理。社区侧（QA 测试、文档反馈、ACP 集成）的反馈渠道运转良好，但需要确保修复不只是打补丁，而是让预防机制制度化。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 | 2026-08-12

> 数据来源：[github.com/netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI) | 统计窗口：2026-08-11 ~ 2026-08-12


## 一、今日速览

**项目活跃度：中高** — 过去 24 小时内有 1 个新版本发布、10 条 PR 更新、4 条 Issue 更新，且多个新功能已完成合并（思考强度配置、任务栏提醒、本地文件右键菜单等），显示项目处于高频度的迭代周期中。值得关注的是，今日合并的 7 个 PR 中多数来自核心维护者（fisherdaddy、liuzhq1986），交付效率较高；但待合并队列中仍积压着 3 个跨月的 PR（#1277、#1181），维护者需关注长期未合入的依赖升级与功能补丁。版本节奏上，本次 `2026.8.11` 为增量功能发布，无破坏性变更，适合用户升级。


## 二、版本发布

### [LobsterAI 2026.8.11](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.8.11)（发布于 2026-08-11）

**主要更新内容：**

| 类别 | 变更 |
|------|------|
| 协作（Cowork） | 新增 `collapse-agent-tasks` 快捷键；允许在文本输入中触发修饰键快捷键 |
| 协作（Cowork） | 侧边栏为定时任务（scheduled tasks）增加图标标识，提高任务类型辨识度 |
| 模型配置 | 引入服务端驱动的 thinking levels（思考强度）配置，支持为新版包模型设置思考档位；OpenClaw 别名支持产品级 `max` -> 运行时级 `xhigh` 映射 |
| 界面/交互 | Settings 弹窗新增未保存修改确认拦截；按 Escape 关闭最上层浮层优化；侧边栏 sites 图标描边统一；本地文件链接支持右键菜单（打开方式/另存为/复制路径/复制内容/复制图片/在文件夹中显示） |
| 稳定性 | 启动与运行时可靠性提升 |

**⚠️ 破坏性变更与迁移提示：** 本次发布无破坏性变更。以下为功能细节调整，请留意：
- 思考强度配置已从「全局唯一」调整为「**每模型独立**」的存储方式（详见 [#2475](https://github.com/netease-youdao/LobsterAI/pull/2475) 与 [#2457](https://github.com/netease-youdao/LobsterAI/pull/2457)）。升级后，不同模型可各自持有不同的思考档位。
- Settings 关闭交互已变更：若存在未保存修改，系统将弹出确认提示，不再静默丢弃配置。
- 本地文件链接的 "reveal-in-folder" 已整合进右键菜单，不再显示为内联按钮。


## 三、项目进展

### 今日合并/关闭的重要 PR

| PR | 标题 | 类型 | 归属领域 | 说明 |
|----|------|------|----------|------|
| [#2477](https://github.com/netease-youdao/LobsterAI/pull/2477) | Release/2026.8.10 | 发布合并 | 全领域 | 将 2026.8.10 版本合入 main，涵盖可配置思考级别、进展可见性提升、定时任务识别、本地文件工作流、启动/运行可靠性改进与设置交互优化 |
| [#2476](https://github.com/netease-youdao/LobsterAI/pull/2476) | feat(ui): dismiss the topmost overlay on Escape | 功能 | renderer, im | 解决嵌套弹层中 Escape 键重复触发问题：弹窗加入可选 onEscape 与 layer id 注册机制，仅最上层 respond，且不干扰 IME 组合输入 |
| [#2475](https://github.com/netease-youdao/LobsterAI/pull/2475) | fix(model-selector): give each model its own thinking level | Bug 修复 | renderer | 修复思考深度在模型之间互斥的 Bug。根因在于 agents/cowork_sessions 共用同一步骤级别配置；现已支持每个模型独立保存思考档位，并补全 UI 交互细节 |
| [#2474](https://github.com/netease-youdao/LobsterAI/pull/2474) | fix(sidebar): align sites icon stroke weight | UI 修复 | renderer | 统一侧边栏 sites 图标描边粗细，对齐视觉规范 |
| [#2473](https://github.com/netease-youdao/LobsterAI/pull/2473) | feat(cowork): add right-click context menu for local file links | 功能 | renderer, main, cowork, artifacts | 新增 LocalFileContextMenu，支持打开方式/另存为/复制路径/复制内容/复制图片/在文件夹中显示；新增 `dialog:saveFileCopy` IPC 处理；缓存 shell app 查找结果，提升响应速度 |
| [#2457](https://github.com/netease-youdao/LobsterAI/pull/2457) | feat(models): add configurable thinking levels | 功能 | renderer, docs, main, openclaw, cowork | 为支持的包模型提供服务端驱动的思考级别选项与默认值；OpenClaw 别名映射（product `max` → runtime `xhigh`）；持久化会话/代理级别的选择并发送版本化模型请求选项 |
| [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) | feat(settings): 关闭未保存配置时增加确认 | 功能（修复） | settings | 关闭 [#1237](https://github.com/netease-youdao/LobsterAI/issues/1237)：脏检测 + 拦截背景点击/X/Cancel 三条关闭路径，弹出「有未保存的修改」确认提示 |
| [#1239](https://github.com/netease-youdao/LobsterAI/pull/1239) | feat(main): AI 任务完成时闪烁任务栏/Dock 图标提醒 | 功能 | main | 窗口不在前台时，任务完成/出错自动闪任务栏（Windows）或 Dock 弹跳（macOS）；Linux 为 no-op |

> **今日合入的 PR 覆盖了 4 个主要方向：发布交付（#2477）、模型配置灵活性（#2457 + #2475）、协作体验细节（#2473、#2476、#2474）、窗口注意力提醒（#1239）。** 项目整体从「基础对话可用」向「深度个性化 + 多任务协作」迈进，用户侧的感知变化包括：设置更安全、模型配置更自由、本地文件操作更顺手。


## 四、社区热点

今日最受关注的讨论集中在以下两个议题：

1. **超时长任务的系统行为不透明** — [Issue #2062](https://github.com/netease-youdao/LobsterAI/issues/2062)（评论 2 条）——“任务超过最大时长”报错后，用户无法判断任务是被中止还是仍在后台执行。该用户正在构建 24 小时连续运行的场景，对任务超时后的状态可见性提出明确诉求。

2. **API 受限导致整体瘫痪** — [Issue #1240](https://github.com/netease-youdao/LobsterAI/issues/1240)（评论 2 条）——用户描述某模型 API 限额烧尽后，尝试切换其他模型继续对话，但全部窗口均反馈受限，且重启程序后启动失败。已证实该 API 在其他客户端上运行正常，说明 LobsterAI 的模型切换与故障隔离机制存在缺陷。

> ✨ 分析：上述两个 Issue 均暴露了「多模型/长任务」场景下的状态管理短板，核心诉求包括：① 超时/受限时的明确状态与可恢复路径；② 单模型故障不应拖垮整体会话；③ 任务超时后应允许续跑而非仅终止。这三个关键词（状态透明、故障隔离、任务续跑）大概率会成为下一阶段架构迭代的重点方向。


## 五、Bug 与稳定性

| 严重度 | Issue/PR | 描述 | Fix PR 状态 |
|--------|----------|------|-------------|
| 🔴 高 | [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) | 单模型 API 受限后被全局传染，所有会话均受限；重启程序启动失败 | 暂无 |
| 🟠 中 | [#1183](https://github.com/netease-youdao/LobsterAI/issues/1183) | Windows 上关闭模型开关后仍反复弹出「openClaw 网关启动失败」遮罩，形成死循环 | 暂无 |
| 🟡 低-中 | [#2062](https://github.com/netease-youdao/LobsterAI/issues/2062) | 任务超时后状态不明确（中止 vs 后台继续），且无续跑入口 | 暂无 |
| 🟢 已修复 | [#1237](https://github.com/netease-youdao/LobsterAI/issues/1237) | Settings 未保存配置在关闭时静默丢失 | 已由 [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) 合并修复，随 2026.8.11 发布 |

> ⚠️ 今日仅新增了「任务超时 #2062」一个有效 bug 报告。该问题虽非新引入，但当用户尝试 24 小时连续任务时触达了设计边界。建议维护者优先审视超时参数的配置开放性与超时后状态展示。


## 六、功能请求与路线图信号

| 信号来源 | 用户诉求 | 对应实现/PR | 预测 |
|----------|----------|-------------|------|
| [#1239](https://github.com/netease-youdao/LobsterAI/pull/1239) | 任务完成时任务栏提醒（已实现） | 今日已合并 | ✅ 已进入 2026.8.11 |
| [#2473](https://github.com/netease-youdao/LobsterAI/pull/2473) | 本地文件链接右键操作（已实现） | 今日已合并 | ✅ 已进入 2026.8.11 |
| [#2062](https://github.com/netease-youdao/LobsterAI/issues/2062) | 超时长任务的状态可见性与手动续跑 | 暂无对应 PR | 🔮 可能性中等，需架构配合 |
| [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) | 单模型故障需隔离，不影响全局 | 暂无对应 PR | 🔮 可能性中等，需状态机重构 |

> 可以预见，2026.8.11 之后的短期路线图将围绕「协作体验细节打磨」（快捷键、标记、右键菜单）继续深挖，而「多模型故障隔离」有望进入中期（v2026.9+）规划。


## 七、用户反馈摘要

> 综合自今日活跃的 Issues 及其评论（#1237、#1240、#2062、#1183）：

- **痛点一：配置易丢失** — 「在 Settings 里改了 API Key，不小心点掉了 X，整个配置没了。」（源于 #1237，已在 2026.8.11 修复）
- **痛点二：模型故障波及全局** — 「一个模型受限，其他模型也全受限了，整个龙虾直接瘫痪。」（#1240）
- **痛点三：超时任务结果未知** — 「不知道任务是停了还是在后台跑，很困惑。」（#2062）
- **痛点四：网关状态异常** — 「关掉模型开关后一直循环跳出遮罩，没法正常使用。」（#1183）
- **满意点（推断）**：多模型思考强度独立配置（#2475）、任务栏提醒（#1239）等功能在 PR 合并日志中被普遍视为高价值改进，用户在评论区表现出对桌面提醒与本地文件操作增强的期待。


## 八、待处理积压

### ⚠️ 长期未合入 PR（已跨 4 个月以上）

| PR | 标题 | 创建时间 | 最后更新时间 | 说明 |
|----|------|----------|-------------|------|
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | chore(deps-dev): bump the electron group across 1 directory with 2 updates | 2026-04-02 | 2026-08-11 | 依赖升级：electron 40.2.1 → 43.3.0，electron-builder 同步升级。长期未合并会导致依赖累积欠债，建议评估后合入或关闭 |
| [#1181](https://github.com/netease-youdao/LobsterAI/pull/1181) | fix(cowork): hide OpenClaw main agent sessions from session list | 2026-04-01 | 2026-08-11 | 为 `cowork_sessions` 增加 hidden 列，隐藏内部 heartbeat/cron 会话。功能性补丁，长期未合入可能导致用户持续看到 `[OpenClaw]` 噪音会话 |

### 长期未关闭 Issue

| Issue | 标题 | 创建时间 | 最后更新时间 | 说明 |
|-------|------|----------|-------------|------|
| [#1183](https://github.com/netease-youdao/LobsterAI/issues/1183) | 一直循环跳出遮罩启动网关 | 2026-04-01 | 2026-08-11 | Windows 专属，持续 4 个月未见修复或明确回复 |

> 提醒：上述积压项中，[#1181](https://github.com/netease-youdao/LobsterAI/pull/1181)（隐藏 OpenClaw 主代理会话）与 [Issue #1183](https://github.com/netease-youdao/LobsterAI/issues/1183)（网关遮罩循环）为同一时期提交，若长期不响应，存在用户流失与信任损耗风险，建议尽快排期处理。


> **报告说明**：以上内容基于 2026-08-11 至 2026-08-12 的 GitHub 公开数据自动生成，供项目维护者与社区成员参考。如需进一步分析特定 PR/Issue，可提出补充查询。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-12

> 客观专业 · 数据驱动 · 项目健康度评估


## 1. 今日速览

Moltis 项目今日整体处于**温和活跃**状态。过去 24 小时无新 Issue 提交、无 Issue 关闭、无新版本发布，Issue 侧基本处于静默期；PR 侧有 2 条待合并更新，其中 #1190 为体量较大的功能扩展（CalDAV 连接器），#1182 为会话管理修复，均已进入可合并窗口。整体来看，项目处于**功能开发与修补并行推进**的阶段，社区外部反馈（Issue 讨论）活跃度偏低，但内部开发节奏保持稳定。

---

## 3. 项目进展

> 今日无 PR 被合并或关闭，以下为处于待合并状态、有待维护者关注的 PR：

- **#1190 [OPEN] Add durable local CalDAV connectors**（作者: penso | 更新: 2026-08-11 | [查看 PR](https://github.com/moltis-org/moltis/pull/1190)）
  该 PR 引入了以下能力：*Provider-neutral connector 持久化*、*原子化 CalDAV 快照*、*基于 prompt 编译的数据集计划*，以及一个只读的 `connectors` agent 工具，用于本地数据集访问。同时新增了 Settings > Connectors 账户/数据集管理界面。**这是项目在本地数据接入与隐私保护方面的一次重要补强**，体现了 Moltis 向"本地优先 + 第三方日历/数据服务"方向演进的产品意图。

- **#1182 [OPEN] fix(sessions): allow deleting and archiving the main session**（作者: shixi-li | 创建: 2026-08-01 | 更新: 2026-08-11 | [查看 PR](https://github.com/moltis-org/moltis/pull/1182)）
  修复 #1132：`main` 会话现在可以像其他会话一样被删除和归档。主要改动在 gateway 层移除了 `delete_impl` 中的 `main` 守卫，同时保持当前活跃通道会话的归档限制不变。**对长期使用 `main` 会话的用户体验是一个实质改进**，消除了一个此前可能造成困扰的限制。该 PR 已开放 11 天，建议维护者尽快审阅合并。

> **一句话总结**：Moltis 正在扩展本地数据连接能力并修复长期存在的会话管理限制，下一合并批次将为项目带来更完整的本地数据闭环和更灵活的会话控制。


## 4. 社区热点

> 今日无新提交的 Issue，PR 评论区亦无新增热议。以下是近期最值得关注的待合并 PR 所引发的讨论焦点：

- **#1190（CalDAV connectors）**：该 PR 体量较大（涉及持久化、快照、调度、全文搜索等多个模块），是近期项目内**功能影响面最大的单一变更**。社区关注点集中在：连接器的持久化机制是否安全、本地全文搜索的性能边界，以及只读 `connectors` 工具与实际用户使用场景（如离线数据查询、日历集成）的匹配度。背后反映了用户对 **"本地数据可控 + 外部服务联通"** 的双向诉求。

- **#1182（main session 删除/归档）**：该项目长期存在的会话管理限制被修复的讨论热度较高（#1132 为长期 open 的 issue）。背后体现了**用户对会话灵活性的需求**，尤其是重度和长期使用单一会话的用户，希望获得更高自主权。


## 5. Bug 与稳定性

> 当日无新 Bug 类 Issue 提交，现存待合并 PR 涉及以下稳定性相关改动：

| 严重程度 | 问题描述 | 状态 | 关联 PR |
|---------|---------|------|--------|
| 中 | `main` 会话无法删除或归档，导致会话管理受限 | 已有修复 PR，待合并 | [#1182](https://github.com/moltis-org/moltis/pull/1182) |

> 无崩溃、数据丢失或安全类高危问题上报。


## 6. 功能请求与路线图信号

- 结合 #1190 的 PR 内容，可明显观察到以下路线图信号：
  - **本地数据接入方向**：CalDAV 连接器预示着 Moltis 将支持日历/任务类外部数据源，未来有望延展到更多 provider（如 Google Calendar、Outlook 等，通过 provider-neutral 架构实现）。
  - **Agent 工具扩展**：新增只读 `connectors` agent 工具，表明项目在**让 Agent 访问本地数据结构化数据**方面有明确规划，这将是 AI 助手在个人数据场景中的核心竞争力。
  - **数据集计划（dataset plans）**：基于 prompt 编译的数据集计划，暗示后续可能支持用户用自然语言定义数据集摄取/整理逻辑。

- 这些信号很可能被纳入下一版本（如 0.4.x 或 0.5.0）的发布范围。


## 7. 用户反馈摘要

> 今日无新 Issue 评论，以下基于 #1182 关联的 #1132 原 Issue 及 PR 内容提炼：

- **用户痛点**：一直以来的 `main` 会话无法删除/归档，超出一定规模后导致会话列表冗长、不便管理。用户在 #1132 中反复请求提供与普通会话一致的删除/归档能力。
- **使用场景**：长期运行的默认会话在"项目启动-长期使用-结束"的生命周期中，需要归档或清理以释放界面空间和心智负担。
- **满意度**：对 #1182 的修复方案（保留活跃通道会话的归档限制，仅放开 `main` 特殊状态）表示认可，认为在灵活性与安全性之间取了合理平衡。


## 8. 待处理积压

| 项目 | 类型 | 创建/更新 | 状态 | 链接 |
|------|------|----------|------|------|
| #1182 fix(sessions): allow deleting and archiving the main session | PR | 2026-08-01 创建，最后一次更新 2026-08-11 | 待合并，已开放 **11 天**；Issue #1132 已等待修复较长时间 | [查看 PR](https://github.com/moltis-org/moltis/pull/1182) |

> **提醒**：#1182 是一个小型、明确、无破坏性变更的修复 PR，已超出常见审阅周期。建议维护者优先处理，以释放会话管理这一基础功能的有效性。另 #1190 体量较大，建议安排专门的 code review 并规划合并时间表。


### 项目健康度小结

| 维度 | 状态 |
|------|------|
| 社区活跃度 | 偏冷（24h 无 Issue 动态） |
| 开发活跃度 | 中等（2 条 PR 在途，1 条为大型功能） |
| 问题响应速度 | 一般（#1182 等待审阅时间偏长） |
| 风险暴露 | 低（无新增高危 Bug、无提交积压） |
| 路线图清晰度 | 清晰（本地数据接入 + Agent 工具扩展方向明确） |

**总体评价**：项目处于功能迭代的正常节奏中，外部输入（Issue/Bug 反馈）较弱可能与当下的版本阶段有关（用户更多在等待新能力落地后才会产生更多反馈）。维护者当前最主要的动作是：**尽快合并 #1182 并对 #1190 安排评审**，以保持社区信任度与交付节奏。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-12

> 数据来源：github.com/agentscope-ai/CoPaw （数据统计区间：2026-08-11 ~ 2026-08-12 UTC）

---

## 1. 今日速览

项目今日整体活跃度处于**高位**，24小时内产生23条Issue更新与49条PR更新，属于近期较为密集的协作节奏。最值得关注的是v2.1.0-beta.3的发布，缓解了beta.2中用户报告的多项前端与MCP稳定性问题。代码合并速度（25条PR合并/关闭）高于新增待合并数量（24条），表明团队维持着健康的核心维护节奏。社区方面，长期悬而未决的**LaTeX公式渲染**问题（#5453、#4756、#6893）今日集中获得响应，预计将在近期版本中修复。约半数bug类Issue在48小时内被关闭，反馈渠道运转效率良好。

---

## 2. 版本发布

### v2.1.0-beta.3（Beta，2026-08-11发布）

**主要更新内容：**

- **工作区文件体验增强**：由 @zhaozhuang521 提交的 `Feat/files workspace blog`（PR #6783），改进了文件工作区的展示与博客发布场景体验。
- **MCP能力缓存修复**：由 @ningblue 提交的 `fix(provider): expire stale capability cache entries and clear on model switch`（PR #6723），修复了MCP工具能力缓存在切换模型后未失效、导致工具反复不可用的问题（关联Issue #6732）。

**破坏性变更与迁移注意事项：**

- 本次更新未引入已知破坏性变更。
- 建议内容：beta.2用户升级前关注缓存失效逻辑的变化，MCP工具出现“未注册”错误时可先重新加载会话而非重启Docker容器。

---

## 3. 项目进展

核心领域的多项修复完成合并，以下整理今日重要合并/关闭的动态：

| 领域 | PR / Issue | 说明 |
|---|---|---|
| **文件预览与深色模式** | PR #6915 | 修复了Unicode文件名（PDF/SVG）的预览失败，并将文件预览对齐Console深色主题。 |
| **代码块体验统一** | PR #6911 | 统一代码块展示：LaTeX和Mermaid块新增预览/源码双标签，支持明暗主题切换。 |
| **Computer Use 输入可靠性** | PR #6891 | 新增受限键盘序列操作，带速率限制与部分完成报告；修复macOS上活动窗口抢焦点导致的菜单关闭问题（PR #6913 跟进）。 |
| **渠道冲突检测** | PR #6909 | 保存渠道配置时若有其他Agent占用同一Bot身份，Console弹出确认对话框以提醒用户。 |
| **渠道API错误码修正** | PR #6912 | 无效渠道负载由HTTP 500修正为HTTP 422，并同步在Issue #6910中说明。 |
| **v2.1.0 发布文档** | PR #6875 | 为v2.1.0正式版准备中英文release notes，同步更新多语言README。 |
| **read_file 工具描述纠正** | PR #6898 | 修正工具描述以匹配实际行为（仅支持文本文件，避免二进制文件被误用）。 |

**总体观感**：今日合并集中于稳定性修复与交互细节打磨，未出现大规模重构。公告性PR（#6875）暗示v2.1.0正式版已在筹备中，beta.3很可能是发布前的最后一轮修复版本。

---

## 4. 社区热点

### 讨论热度最高 Issue

**#6893 — 公式渲染问题；会话分组管理；活动会话背景**（7条评论）  
链接: https://github.com/agentscope-ai/QwenPaw/issues/6893

虽为新开Issue，但获得了社区快速响应。用户集中反映三个诉求：LaTeX公式渲染缺失、长会话列表缺乏分组管理、活动会话高亮不足。这条Issue与历史多期公式渲染相关反馈（#5453、#4756）形成呼应，是今日社区讨论最集中、诉求最不分散的话题。

### 活跃度突出 PR

**#6874 — feat(mcp): add configurable tool call timeout**  
链接: https://github.com/agentscope-ai/QwenPaw/pull/6874

为MCP工具调用新增120秒可配置超时，回应了#6724（MCP挂起阻塞Agent运行）和#3997的长期受扰问题。该PR在社区被多次提及，说明MCP稳定性仍是当前用户关注的头号运行问题。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 当前状态 |
|---|---|---|
| 高 | **#6919 — v2.0.1 频繁崩溃**，控制台 `process/reply` 报错（链接: https://github.com/agentscope-ai/QwenPaw/issues/6919） | 开放中，暂无明确PR对应。pip安装+vWeb端场景，需尽快排查。 |
| 中高 | **#6916 — 插件可静默创建定时任务并向会话注入消息**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6916） | 安全类问题，定级中高，开放中，需设计权限模型修复方案。 |
| 中 | **#6885 — v2.1.0b2 中文输入法下消息队列不可用**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6885） | 开放中，涉及IME组合态与Agent运行并发场景。 |
| 中 | **#6918 — 多Agent消息相互触发创建新会话，形成并发"影子实例"**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6918） | 由Agent代笔的问题报告，内容涉及典型并发边界条件，开放中。 |
| 中 | **#6732 — MCP工具规律性失效**，重启Docker方可恢复（链接: https://github.com/agentscope-ai/QwenPaw/issues/6732） | **已关闭**，v2.1.0-beta.3的PR #6723修复了缓存失效逻辑，需beta.3实测验证。 |
| 中低 | **#6828 — 空闲时前端持续重绘（~20% CPU）**，根因是无限CSS动画（链接: https://github.com/agentscope-ai/QwenPaw/issues/6828） | **已关闭**，已修复。 |
| 中低 | **#6871 — 前端历史消息时间戳偏移+8小时**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6871） | **已关闭**，已修复。 |
| 低 | **#6697 — v2.1.0b1 桌面版注入PYTHONHOME致子进程崩溃**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6697） | **已关闭**，已修复。 |

---

## 6. 功能请求与路线图信号

| 功能请求 | Issue / PR | 纳入可能性 |
|---|---|---|
| **LaTeX公式渲染**（KaTeX支持） | #5453（已关闭）、#4756（已关闭）、#6893（讨论中）—— PR #6911已统一代码块体验并加入LaTeX预览/源码标签 | **高**，相关PR已合并，基本确定纳入下版。 |
| 会话分组管理与活动会话高亮 | #6893 | 中，需求具体，但需评估前端改动量。 |
| 聊天项目目录与Agent工作区隔离 | #6900（已关闭） | 已纳入设计讨论，可能随v2.2进入后端架构调整。 |
| Agent主动投递消息至收件箱（Inbox） | #6917 | 中，当前Agent消息只能随聊天流滚动，用户诉求固定落点+未读红点，可能会作为功能增强纳入路线图。 |
| 插件权限模型（定时任务、消息注入需用户确认） | #6916 | 高，已被标记为安全类问题，为发版前必须答复的问题。 |
| CopilotKit集成方案 | #6882 | 待定，属于纯社区咨询，暂无回复。 |

此外，市场页统一（PR #6880）、Slash命令自动补全（PR #5869）、文件全屏画廊（PR #5490）、Provider统一发现与路由（PR #6302）等PR虽暂未合并，但均在活跃更新周期内，预计在v2.2.0中集中落地。

---

## 7. 用户反馈摘要

### 正面肯定
- **代码块体验改善**：LaTeX与Mermaid预览/源码双标签获得了论坛用户的正面评价。
- **深色模式修复**：文件预览在深色主题下的适配获得了桌面端用户的好评。

### 负面痛点
1. **LaTeX公式不渲染** —— 用户普遍反映“在QwenPaw中粘贴公式就像看到一坨乱码，很尴尬”（#6893），对比工具Cherry Studio表示不满。
2. **MCP工具周期性失效** —— 用户需重启Docker或重载配置才能恢复，严重干扰长流程任务的执行（#6732）。
3. **QQ渠道工作流刷屏** —— 用户反馈详细工作流全量推送到QQ导致消息不断、易触发限流（#6897），诉求是"不必每一步都发"。
4. **中文输入法兼容性问题** —— v2.1.0b2在中文输入法下消息队列不可用，直接影响中文社区的核心体验（#6885）。
5. **运行崩溃** —— v2.0.1在pip安装+vWeb端场景出现频繁崩溃（#6919），用户请求尽快修复。

### 社区沟通建议
- 用户在#6895中请求建立微信群以便交流，反映GitHub Discussion对部分中文用户仍有门槛。

---

## 8. 待处理积压

| 类型 | 条目 | 说明 |
|---|---|---|
| Issue | **#6883 — 日记页面子文件夹笔记被错误分组**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6883） | 创建于2026-08-10，仅有1条评论，已停滞近48小时。 |
| Issue | **#6882 — 怎么集成CopilotKit**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6882） | 开放超48小时且零回复，用户疑问仍待解答，建议至少给出集成思路或文档链接。 |
| PR | **#6660 — 更新 .dockerignore 以包含 README.me**（链接: https://github.com/agentscope-ai/QwenPaw/pull/6660） | 首次贡献者提交，内容短小，已放置9天未review，建议尽快合并或关闭。 |
| PR | **#5490 — 可导航的全屏图片画廊**（链接: https://github.com/agentscope-ai/QwenPaw/pull/5490） | 已开放49天，功能完善且无冲突，积压时间过长，建议纳入合并队列。 |
| PR | **#6564 — 压缩前刷写pending turns**（链接: https://github.com/agentscope-ai/QwenPaw/pull/6564） | 修复#6555的存储风险，已开放13天，建议加快review。 |
| 长期提醒 | **#6914 — Release Duty（v2.1.0-beta.3安装验证）**（链接: https://github.com/agentscope-ai/QwenPaw/issues/6914） | Deadline为8月11日15:45 UTC，若验证未完成该版本可能跳票，建议跟进。 |

---

*以上日报由 AI 分析师基于 GitHub 公开数据自动生成，数据截至 2026-08-12。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-12

## 1. 今日速览

ZeroClaw 在过去 24 小时保持高水平社区活跃度：50 条 Issues 更新（40 条活跃/新开、10 条关闭）与 50 条 PR 更新（48 条待合并、2 条已合并/关闭），无新版本发布。项目当前处于**密集的 RFC 评审与安全加固周期**——多个高优先级安全 Bug（#9883、#9872）已获得维护者确认（`status:accepted`）并有对应修复 PR 跟进（#9862、#9781 在列），同时 6 项 RFC 正在等待维护者评审（`needs-maintainer-review`）。值得关注的是，社区顶级贡献者（JordanTheJet、Audacity88、NiuBlibing）驱动的安全与架构类 PR 规模较大（多个 size:L 和 size:XL），展现出项目在 v0.9.0 方向上的系统化投入，但 **48 条 PR 待合并的积压量值得关注**。总体健康度良好，处于"安全加固 + 架构收敛"的关键阶段。

---

## 3. 项目进展

今日无 PR 被合并（2 条关闭/合并中未展示出核心功能合入），但多组重要 PR 正在推进关键里程碑：

### 安全加固主线（多 P1）
- **[PR #9862] fix(tools): bound direct HTTP response handling**（size:L，待合并） — 由 @Audacity88 提交，对流式 `http_request` 响应体实施字节上限截断，并阻止 fal.ai API 客户端自动跟随重定向（防止认证请求泄露）。这是对工具层 HTTP 出口的重要安全边界加固。
- **[PR #9781] fix(runtime): validate WebAuthn assertion data**（size:M，待合并） — 同由 @Audacity88 提交，补齐 WebAuthn 断言的 37 字节固定头校验、rpIdHash 绑定及 User Present 标志检查，强化设备认证安全性。

### SOP（标准操作程序）成熟度推进
- **[PR #9841] fix(sop): drive headless SOP runs, close five defects**（size:XL，待合并） — 由 @JordanTheJet 接手 #9494 的公开移交，在保持原四个提交不变的基础上修复了评审中发现的四个阻塞性缺陷，外加一个额外缺陷。直接推动 [#8288 SOP milestone tracker] 向 5/5 目标迈进。
- **[PR #9885] fix(sop): honour the documented sops_dir default**（size:S，待合并） — 修复 `[sop] sops_dir` 可选覆盖未在 daemon 中生效、与文档声明不一致的问题（fixes #9779）。

### 平台兼容性
- **[PR #9182] feat(runtime): support PowerShell as native shell on Windows**（size:XL，待合入） — 由 @NiuBlibing 提交，在 Windows 上通过 `-NoProfile -NonInteractive -Command` 路由 `powershell`/`pwsh`，同时保留默认 `cmd.exe` 路径，推进 Windows 一等公民支持。

**结论：项目在安全加固（HTTP 出口、WebAuthn）、SOP 成熟度、Windows 原生支持三条线上均有规模化 PR 待合入，一旦合并将显著推进 v0.9.0 里程碑。**

---

## 4. 社区热点

### 今日最热讨论（按评论数排序）

1. **[#8303] RFC: Goal mode v1 — bounded foreground Matrix work**（19 评论，👍1）— 由 @vrurg 于 6/24 创建，已持续讨论近 7 周。核心诉求：ZeroClaw 需要一种持久机制在多个 agent 轮次中追求有界用户目标。该 RFC 将重启交接、广谱频道准入、Web 和异步子工作解耦，聚焦于控制面。**社区反馈**显示对此前版本范围过宽的修正获得认可，讨论进入收敛阶段。

2. **[#8603] RFC: ZeroClaw Chat Completions profile**（18 评论）— 由 @REL-mame 提出，核心诉求十分明确：支持 OpenAI Chat Completions 协议，以接入 Open WebUI、LobeChat、Continue.dev、Aider、LangChain 等生态工具。**这是社区对互操作性的强烈渴求**，若落地将极大扩展 ZeroClaw 的用户触达面。

3. **[#7155] RFC: per-execution confirmation tier for high-risk shell commands**（17 评论）— 讨论横跨两个月（创建于 6/3），已迭代至 Revision 3，由维护者 @Audacity88 划定范围。核心是引入 Claude Code 风格的 `allow/ask/deny` 命令策略模式，**反映了用户对 agent 安全执行高风险命令的强烈关注**。

### 关注者最多的活动

- **[#9545] Task: gate rustdoc warnings in required PR CI**（👍1）— 为避免工作区零 rustdoc 警告状态静默回归，提议在 PR CI 中以 `RUSTDOCFLAGS="-D warnings"` 作为必需检查。该任务已关闭，预示该项目已纳入 CI 流程。

**社区诉求集中：① 互操作性（OpenAI 协议兼容）；② 精细化安全控制（高风险命令确认）；③ 跨轮次目标追踪（Goal mode）。**

---

## 5. Bug 与稳定性

### P1（高优先级）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#9883] | **Inbound WebP 转换在共享图像验证器之前无界解码** — `webp_to_png` 调用 `image::load_from_memory` 处理未受信任的 WebP 附件，无大小限制 | `status:accepted`，尚无对应 PR |
| [#9872] | **Bounded delegate 目标错误解析文件系统到委派者工作区** — `executive_assistant` 委派 `researcher` 时，`file_write`/`file_edit`/`shell` 写入委派者的工作区，而非自己的工作区 | `status:accepted`，尚无对应 PR |
| [#9768] (已关闭) | **daemon reload 不在 SIGUSR1 上，降级安全警告会告知操作员发送"杀死 daemon"的信号** — 文档与实现严重不一致 | 已关闭，修复已合入 |

### P2（中优先级）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#9035] (已关闭) | **Docker Compose gateway 可保持回环绑定在已发布端口后** — S1 workflow blocked | 已关闭 |
| [#9545] (已关闭) | **rustdoc 警告门禁缺失 → CI 要求** | 已关闭 |

### 稳定性观察

- 今日关闭的 10 条 Issues 中包含 #9768（文档误导信号）和 #9035（S1 Docker 端口绑定），说明维护者对高影响 Bug 的响应较及时。
- **#9883 和 #9872 均为近两日新开、已被接受（accepted）的 P1 安全/沙箱缺陷，尚无对应修复 PR，需要密切跟踪** —— 这两项若被武器化利用（WebP 内存耗尽 DoS、跨工作区文件写入）可能构成安全事件。

---

## 6. 功能请求与路线图信号

### 强信号（已有 PR 或进入 accepted 状态）

| 功能 | 对应 Issue/PR | 信号强度 |
|------|--------------|---------|
| **OpenAI Chat Completions 协议兼容** | [#8603]（讨论中） | ⭐⭐⭐ 18 评论，接入 Open WebUI/LobeChat 等主流工具 |
| **高风险 shell 命令 allow/ask/deny 策略** | [#7155]（Rev 3 已收敛） | ⭐⭐⭐ 17 评论，Claude Code 风格模式，维护者已确认范围 |
| **PowerShell 原生支持（Windows）** | [PR #9182]（size:XL 待合并） | ⭐⭐ 功能已实现，等待合入 |
| **SOP 只读状态面板** | [PR #9694] + [#9682 tracker] | ⭐⭐ 状态可见性 MVP 开发中，控制功能后续推进 |
| **运行时会话 / 传输表面适配器** | [#9487]（Rev 2，评审中） | ⭐⭐ 与 #9488/#9600 联合推进，建议与 Chat Completions 协议配合落地 |
| **插件拥有的看板（Kanban）** | [#8832]（9 评论） | ⭐ 作为插件拥有域，建立于宿主导出的通用能力之上 |

### 弱信号（仍在早期讨论）

- **Lucid memory connector 退役**（[#9644]）：上游项目在合并后 4 天即休眠，社区建议在 v0.9.0 移除。
- **统一 catalog 契约**（[#9346]）：产品级包/能力/配置/运行时状态编目，虽为架构级，但被标记为 `needs-maintainer-review`。

**下一版本（v0.9.0）路线图信号：安全策略管线、SOP 5/5 成熟、插件类型安全、HTTP 出口加固都可能成为其主要内容。**

---

## 7. 用户反馈摘要

### 正面反馈
- **项目 CI 质量意识强**：社区成员 @tidux 提出 rustdoc 警告门禁（#9545）并已关闭实施，说明项目对代码质量有系统化保障。
- **性能优化正反馈**：`pr #9713` 为历史裁剪事件增加 token 核算，解决大轮次削减可能消耗完整 token 预算的隐患。

### 痛点与使用场景
- **配置项隐式行为困扰**：`#9885` 修复了 `sops_dir` 默认值未按照文档生效的问题，反映用户对"配置应遵守文档"的高期待。
- **Windows 脚本碎片化**：`#9182` 的 PowerShell 支持来自用户对 Windows 作为一等公民的诉求。
- **高成本模型不可负担（引用早期 #2269）**：单一路径的高端模型运行真实工作负载，对 end-user 价格过高 — 该 13 评论的 RFI 虽已关闭，但仍是产品化关切。
- **本地模型能力受限（引用 #5907）**：LSP 支持被提为减少幻觉、提升本地模型代码生成质量的可行补充。

### 不满意/潜在摩擦点
- **Docker 部署回环绑定陷阱**（#9035，已关闭）：`docker compose up -d` 后端口不可达，说明部署文档与实际网络模型存在落差。
- **配置保存 ≠ 配置生效**（#7897）：保存配置并不保证子系统立即采用新状态，`/admin/reload` 才能重建，存在明显的可用性摩擦。

---

## 8. 待处理积压

### 长期未解决的重要 RFC（需维护者决策）
| Issue | 标题 | 创建 | 等待时长 | 阻塞状态 |
|-------|------|------|---------|---------|
| [#7141] | Pluggable inbound authentication and canonical principals | 2026-06-03 | 70 天 | `needs-maintainer-review`，Rev 8 |
| [#7142] | Runtime-owned security decision pipeline | 2026-06-03 | 70 天 | `needs-maintainer-review`，Rev 6 |
| [#5907] | Opt-in LSP support for ZeroCode coding | 2026-04-19 | 115 天 | `needs-author-action`，已停滞超 3 个月 |

### 需要作者行动的 PR（有停滞风险）

| PR | 标题 | 最后更新 | 停滞警示 |
|----|------|---------|---------|
| [#9612] | WhatsApp Cloud approval token guard | 2026-08-11 | 已标记 `stale-candidate` |
| [#9385] | WhatsApp Web request_approval 实现 | 2026-08-11 | 已标记 `stale-candidate`，近 2 周未实质动作 |
| [#9126] | validate typed instance config | 2026-08-11 | size:XL，25 天未更新 |

### 维护者行动提醒
1. **大批 P1/高风险 PR 待合并**（[#9862]、[#9841]、[#9781] 等），建议安排集中评审窗口；
2. **#9883 与 #9872 两个新接受安全 Bug 尚无修复 PR**，可考虑在社区中悬赏认领或`good-first-issue`标注；
3. **#7141/#7142 双安全 RFC 悬置 70 天**，作为 v0.9.0 安全架构的核心输入，长期不确定将阻塞相关实现。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*