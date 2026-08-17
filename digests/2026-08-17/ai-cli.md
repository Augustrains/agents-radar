# AI CLI 工具社区动态日报 2026-08-17

> 生成时间: 2026-08-17 00:29 UTC | 覆盖工具: 9 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告

**日期：2026-08-17**


## 一、生态全景

当前 AI CLI 工具已全面进入**生产环境攻坚期**。头部工具（Claude Code、OpenAI Codex、Gemini CLI）不再以功能堆叠为核心，而是转向稳定性、权限模型、会话持久化等基础设施层面的加固。多智能体协作（子代理、agent-team）成为共性探索方向，但可靠性问题集中暴露。中国市场成为不可忽视的变量——Qwen Code、Kimi Code 的活跃迭代，以及 Claude Code 中国区账号风波，表明本地化部署与合规问题正成为全球玩家的共同课题。与此同时，品牌化与商业化进程加速（DeepSeek-TUI 更名 Codewhale，OpenCode 引入付费套餐），工具正在从开发者玩具演进为真正的产品。


## 二、各工具活跃度对比

| 工具 | 今日 Issues（新提交） | 活跃 PR | 版本发布 | 社区热度信号 |
|------|---------------------|---------|---------|------------|
| **Claude Code** | 约 10 条 | 3 条（全部 Open） | 无 | 大量历史 Issue 被集中关闭（账号/计费），高赞问题（61👍）聚焦订阅权限 |
| **OpenAI Codex** | 约 12 条（30 条热门中精选） | 12 条（全部已合并） | 无 | Windows 性能问题霸榜（85👍），合并速度极高 |
| **Gemini CLI** | 约 10 条 | 10 条（8 条活跃） | 1 个 nightly | P1 级子代理挂起（8👍），PR 由 AI 辅助生成（SSR Agent） |
| **Copilot CLI** | 6 条新提交（16 条总更新） | 1 条（存续 3 个月） | 无 | 新提交集中在 MCP 认证与 Windows 稳定性，PR 活跃度低 |
| **Kimi Code** | 约 4 条 | 3 条（2 条 Open） | 无 | 长期 Issue 持续发酵但无官方表态，社区规模较小 |
| **OpenCode** | 约 10 条 | 10 条（大部分已合并/关闭） | 无 | "Ctrl+C 退出" 高赞 49👍 长期未解决，v2 打磨中 |
| **Pi** | 约 10 条 | 10 条（全部已合并） | 无 | 核心 bug（tool_calls 顺序破坏）当日确认并修复，效率高 |
| **Qwen Code** | 6 条（5 条 P2 多智能体 bug） | 10 条（7 条今日更新） | 2 个（preview + nightly） | 多智能体问题集中爆发，维护者主导审查子系统重构 |
| **DeepSeek-TUI (Codewhale)** | 约 10 条 | 10 条（5 条新增/合并） | 1 个正式版（v0.9.8） | 品牌重塑期，24 小时内核心维护者提交 10+ PR/Issue |

**关键观察**：OpenAI Codex 与 Pi 的 PR 全部合入，执行效率最高；Copilot CLI 的 PR 活跃度极低，值得关注；Qwen Code 与 Codewhale 处于密集迭代期。


## 三、共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|------|---------|---------|
| **会话持久化与恢复** | Claude Code（#26452 会话消失）、Copilot CLI（#4505 恢复后不可用）、Gemini CLI（#25166 挂起）、Kimi Code（#1783 删除会话） | 会话历史是核心资产，要求可靠保存、一键恢复、生命周期管理（删除/归档） |
| **子代理/多智能体可靠性** | Claude Code、Gemini CLI（#21409 挂起、#22323 误报成功）、Qwen Code（#9276-9291 六个 bug）、Codewhale（#5123 权限矛盾）、OpenCode（#32366 卡死） | 子代理执行状态透明化、任务派发可靠性、权限模型一致性、防挂起与超时机制 |
| **Windows 平台体验** | OpenAI Codex（#20214 卡顿、#32797 内存泄漏）、Copilot CLI（#4463 OAuth 失败、#4488 文件锁）、Kimi Code（#2600 路径 bug）、Pi（#6300 重绘异常） | 性能优化（卡顿、内存泄漏）、路径兼容、进程生命周期管理、MCP 稳定性 |
| **配额与计费透明性** | Claude Code（#28817 Remote Control 不可用、#28760 Rate Limit）、OpenCode（#33318 付费仍被限流）、Copilot CLI（#4504 resetDate 错误）、Pi（#7870 目录覆盖、#8218 token 统计） | 订阅状态实时同步、用量仪表盘、额度判定逻辑透明化、token 统计准确 |
| **MCP 集成稳定性** | Copilot CLI（#4490 OAuth 回归、#4472 并发刷新）、OpenCode、Codex（#32797 进程泄漏）、Gemini CLI（#28839 Schema 规范化） | OAuth 认证链路健壮性、进程生命周期管理、工具 Schema 标准化 |
| **本地/自定义模型支持** | OpenCode（#26602 超时强制）、Pi（#8061 上下文预算）、Qwen Code（#9275 Copilot 认证） | 非托管模型的超时可配置、context 窗口精确计算、多 Provider 方言兼容 |
| **文档与依赖透明化** | Claude Code（#23704 poppler-utils 未文档化）、Gemini CLI、Codewhale（#5434 方言不匹配） | 外部依赖显式声明、工具能力边界文档化、集成层协议差异说明 |


## 四、差异化定位分析

| 工具 | 核心定位 | 技术路线 | 目标用户 | 独特优势 |
|------|---------|---------|---------|---------|
| **Claude Code** | 全能型 IDE 级 Agent | 深度集成 IDE/桌面端，生态最完整 | 专业开发者/企业 | 生态最成熟（Desktop、VSCode、SDK），社区规模最大 |
| **OpenAI Codex** | 云端优先的跨平台 Agent | TUI + 桌面应用 + 移动端 + 远程控制 | 云端/远程开发者 | 跨设备无缝衔接，PR 合并效率高，TypeScript SDK 灵活 |
| **Gemini CLI** | 极客向终端 Agent | TUI 深度优化，A2A 协议，子代理调度 | CLI 重度用户 | 子代理架构先进（A2A），AI 辅助开发（SSR Agent）效率高 |
| **GitHub Copilot CLI** | 企业生态嵌入型 | 深度绑定 GitHub 生态（MCP、插件、Actions） | 企业级团队 | GitHub 生态集成度最高，插件体系设计良好 |
| **Kimi Code** | 中国市场的轻量 Agent | Python 实现，Web 端 + CLI | 中国开发者 | 代码库轻量，社区小而专 |
| **OpenCode** | Ant 系开源旗舰 | v2 重写中，桌面端 + TUI 双轨 | 开源社区/本地模型用户 | 开源协议友好，本地 Provider 支持广 |
| **Pi** | 模型目录驱动的通用客户端 | 强调多 Provider 目录管理（pi.dev），TUI 精细度 | 多模型切换的重度用户 | pi.dev 集中式模型目录，Token 统计精细 |
| **Qwen Code** | 阿里系多智能体探索者 | agent-team 协作 + AI 驱动审查流水线 | 多智能体实验者 | 审查子系统（/review）自动化程度高，DSW E2E 基准验证 |
| **Codewhale (DeepSeek-TUI)** | 快速迭代的终端体验派 | 专注 TUI 交互打磨，沙箱灵活配置 | 深度 TUI 爱好者 | 单日迭代频率最高，i18n 覆盖广，双平台沙箱完善 |


## 五、社区热度与成熟度评估

| 梯队 | 工具 | 特征 |
|------|------|------|
| **成熟期（稳定性 > 新功能）** | Claude Code、OpenAI Codex | 社区规模最大，Issue 数量多，官方开始集中清理历史积压；重点转向性能、权限、计费等生产级问题 |
| **快速成长期（功能迭代 + 稳定性并重）** | Gemini CLI、Pi、Qwen Code、Codewhale | 高频发布与 PR 合入，子代理/多智能体等新架构快速演进；社区贡献者活跃，AI 辅助开发信号明显（Gemini SSR Agent） |
| **平台打磨期（稳定性短板明显）** | GitHub Copilot CLI、OpenCode | 新版本（1.0.80 / v2）引入回归问题，社区反馈集中于可靠性而非新需求；OpenCode 的 v2 打磨仍需时间 |
| **社区培育期（规模较小）** | Kimi Code | Issue 数量少、官方响应慢（长期 Issue 无表态），社区仍在寻找定位 |


## 六、值得关注的趋势信号

1. **多智能体协作从概念走向真实负载**：Qwen Code 单日 6 个 agent-team bug、Gemini CLI 子代理挂起、Codewhale 子代理权限矛盾——当多个独立工具在同一时期暴露同类问题，说明这一方向已从 demo 进入生产验证，但可靠性仍是最大瓶颈。**对开发者的启示**：在子代理成熟前，关键任务仍需人工兜底。

2. **Windows 平台成竞争分水岭**：Codex 和 Copilot CLI 的 Windows 问题霸榜，而 Codewhale 已在处理 Windows NSIS 配置——AI CLI 工具的 Windows 体验将成为企业大规模推广的关键决定因素。**对开发者的启示**：Windows 用户在选型时需重点考察工具的沙箱与进程管理机制。

3. **"AI 辅助开发 AI"成为常态**：Gemini CLI 的 SSR Agent 自动生成修复 PR，Qwen Code 的审查流水线本身由 AI 驱动，Codewhale 引入 capture-tui 让验证者用截图而非代码论证——AI 工具正在重塑自身的开发流程。**对开发者的启示**：这些工具的迭代速度将持续加快，但需关注 AI 生成代码的质量审查机制。

4. **计费透明化成为信任基石**：从 Claude Code 的 Remote Control 权限错位、OpenCode 付费余额被限流、Pi 的 token 统计膨胀 120 倍，到 Copilot CLI 的 resetDate 错误——计费问题已成为高频投诉点，直接消耗用户信任。**对开发者的启示**：付费前务必小规模验证额度的实际消耗速度。

5. **品牌化与产品化加速**：DeepSeek-TUI 更名 Codewhale、OpenCode 引入 Zen 付费套餐、Qwen Code 开始 DSW E2E 基准——工具正在从开源项目演进为商业产品，意味着更稳定的投入，也可能意味着更严格的使用条款。

6. **中国市场成为独立变量**：Claude Code 中国区账号被禁用（#67069）与代理 403（#30318）、Qwen Code 的本地化迭代、Kimi Code 的深耕——中国开发者对 AI CLI 工具的需求旺盛，但网络与合规因素迫使本土替代方案加速成熟。**对开发者的启示**：中国区团队需提前规划网络方案与备选工具链。


*报告完。数据基于 2026-08-17 各工具 GitHub 仓库公开动态。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据范围**: 2025-10 至 2026-08 | **快照日期**: 2026-08-17


## 一、热门 Skills 排行（按社区关注度）

### 1. `skill-creator` 触发评估修复（PR #1298）
- **功能**: 修复 `run_eval.py` 始终报告 0% recall 的系统性问题，使 `skill-creator` 的描述优化循环基于有效信号运行
- **社区热点**: 引用 #556（12 评论、7 👍），社区累计 10+ 独立复现；修复涉及 Windows 兼容性、触发检测及并行工作线程
- **状态**: Open（2026-06-10 创建） | ⚠️ 链路阻塞：引发 3 个衍生 PR（#1099、#1050、#1419）
- 🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298)

### 2. `document-typography`（PR #514）
- **功能**: AI 生成文档的排版质量控制——孤立单词换行、段首孤儿标题、编号错位
- **社区热点**: 直击 AI 生成文档的治理盲区（"Users rarely ask for good typography"）；回应多起 docx/ooxml 空白格式事故（#12）
- **状态**: Open（2026-03-04 创建）
- 🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

### 3. `run_eval.py` Windows 兼容性修复（PR #1099 / #1050）
- **功能**: 修复 Windows 下 `claude.cmd` 子进程调用失败（WinError 2）及管道读取崩溃（WinError 10038）
- **社区热点**: 与 #1298 互为因果；Windows 是 skill-creator 触达率失真（precision=100% / recall=0%）的主因之一
- **状态**: 双 PR 均为 Open（2026-04-27 / 2026-05-07）
- 🔗 [PR #1099](https://github.com/anthropics/skills/pull/1099) · [PR #1050](https://github.com/anthropics/skills/pull/1050)

### 4. `self-audit`（PR #1367）+ 推理质量门控提案（Issue #1385）
- **功能**: 交付前审计——先做机械性文件验证（Step 0），再按损害严重度执行四维推理审计（v1.3.0）
- **社区热点**: 与 #412（agent-governance）、#1479（plan-file-hygiene）构成"质量门控"主题簇；4 评论持续追踪
- **状态**: Open（2026-06-28 创建，2026-07-02 更新）
- 🔗 [PR #1367](https://github.com/anthropics/skills/pull/1367) · [Issue #1385](https://github.com/anthropics/skills/issues/1385)

### 5. 文档格式生态扩展: ODT（PR #486）、Pyxel（PR #525）、DOCX 修复（PR #541）
- **功能**: 
  - ODT: OpenDocument 创建/填充/解析（#486）
  - DOCX: 修复 `w:id` 跨 bookmark/tracked-change 命名空间冲突（#541）
  - Pyxel: 复古像素游戏开发工作流（#525, kitao 作者背书）
- **社区热点**: 文档领域同时存在"新增格式"与"修复既有格式"的双向诉求；ODT 补全 LibreOffice 生态闭环
- **状态**: 均 Open，平均存活期 4+ 个月
- 🔗 [PR #486](https://github.com/anthropics/skills/pull/486) · [PR #541](https://github.com/anthropics/skills/pull/541) · [PR #525](https://github.com/anthropics/skills/pull/525)

### 6. 平台类 Skill: ServiceNow（PR #568）
- **功能**: 全平台助手——覆盖 ITSM、ITAM/SAM Pro、FSM、HRSD、CSM、SPM/PPM、漏洞响应与 IntegrationHub
- **社区热点**: 企业平台纵深整合的代表作；存活 5 个月仍 Open，社区持续追问
- **状态**: Open（2026-03-08 创建）
- 🔗 [PR #568](https://github.com/anthropics/skills/pull/568)


## 二、社区需求趋势（来自 Issues）

| 方向 | 代表 Issue | 信号强度 |
|---|---|---|
| **信任边界与安全** | #492（43 评论，2 👍）—— 社区 Skill 伪冒 `anthropic/` 命名空间 | 最高：43 评论断层第一 |
| **组织级 Skill 共享** | #228（16 评论，8 👍）—— org-wide 共享库/直链 | 强：高点赞 + 持续 6 个月讨论 |
| **Skill 评估可靠性** | #556（12 评论，7 👍）—— 触发率 0% 失真 | 强：与 4 个 PR 直接关联 |
| **Skill 安装去重与生命周期** | #189（6 评论，9 👍）—— 插件重复安装致上下文膨胀 | 中：高点赞比 |
| **上下文窗口治理** | #1487 —— `claude-api` 单次注入 ~156k tokens | 新近：2026-07 提出，4 评论 |
| **企业文档安全合规** | #1175 —— SPO 文档的访问控制与权限逻辑 | 中：企业级场景关切 |

**隐含主题**: 社区最期待的并非"更多新 Skill"，而是 **Skill 基础设施的成熟化**——安装、评估、共享、权限治理。


## 三、高潜力待合并 Skills（近期可能落地）

| PR | Skill | 潜力判断依据 |
|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator 评估修复 | 是当前 `skill-creator` 失效的根因修复，3 个 PR 依赖其合并 |
| [#210](https://github.com/anthropics/skills/pull/210) | frontend-design 可执行性重构 | 存活 7+ 个月，社区持续讨论"可落地指令"与"单会话可执行" |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns（完整测试方法论） | 覆盖面广（Trophy 模型 → React Testing Library），标准明确、实现完整 |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS 预测分析 | 首个企业级开源表格基础模型 Skill，差异化显著 |
| [#1479](https://github.com/anthropics/skills/pull/1479) | plan-file-hygiene（规划产物生命周期） | 直接回应社区命名的"生命周期缺口"（#1417），框架清晰 |

> 注：以上 PR 均存活 ≥3 个月且讨论活跃，但 anthropics/skills 仓库当前 **没有任何 PR 进入 merged 状态**（前 20 热门 PR 全部 Open）——合并节奏是当前社区协作的主要瓶颈。


## 四、Skills 生态洞察（一句话）

> **社区最集中的诉求不是"更多新 Skill"，而是 `skill-creator` 工具链的可靠性、官方维护节奏的响应性，以及命名空间信任机制——一句话：Skill 生态正从"数量扩张期"进入"工程质量期"。**

---

# Claude Code 社区动态日报 — 2026-08-17

> 数据来源：github.com/anthropics/claude-code（截至 2026-08-17）

---

## 今日速览

过去 24 小时内无新版本发布，但社区活跃度维持在较高水平。值得关注的是，大量历史 Issue（尤其是 2 月至 6 月间提交的 bug 报告）在今日被大量关闭/更新，其中多起与账号禁用、订阅计费和远程控制（Remote Control）可用性相关的问题集中引发讨论——这暗示官方可能正在大规模清理和解决积压的账号/计费类问题。与此同时，**模型响应可靠性**和 **SDK/Agent 任务通知机制**成为新提交的高质量 bug 报告的焦点。

---

## 社区热点 Issues（Top 10）

### 1. Session 意外消失，恢复求助（#26452）🔥
- **标签**：Bug | **开放中** | 评论 51 | 👍 30
- **链接**：[Issue #26452](https://github.com/anthropics/claude-code/issues/26452)
- **摘要**：用户反馈在 Claude Code Desktop 中登出/重启后整个 Session（对话历史）消失，且无恢复途径，提问者情绪较为急切。
- **关注点**：数据持久化是开发者核心资产，此 Issue 虽创建较早（2 月），但至今仍处于开放状态且始终保持高热度，反映社区对该问题长期未获解决的焦虑。

### 2. Pro 计划被提示"Remote Control 不可用"（#28817）
- **标签**：Bug / Duplicate / Docs | **已关闭** | 评论 44 | 👍 61
- **链接**：[Issue #28817](https://github.com/anthropics/claude-code/issues/28817)
- **摘要**：Pro 订阅用户在认证通过后仍被提示 Remote Control 功能不可用，尝试重新认证无效。该 Issue 已被标记为 duplicate 并关闭，但获得了 61 个👍，是今日列表中最高赞的 Issue。
- **关注点**：功能权限与实际订阅不匹配的 bug 影响范围较大，社区认可度高，官方已识别为重复问题（大概率已在处理中）。

### 3. Max 计划 Rate Limit 无法通过增加配额解决（#28760）
- **标签**：Question / Windows / Cost | **已关闭** | 评论 25 | 👍 14
- **链接**：[Issue #28760](https://github.com/anthropics/claude-code/issues/28760)
- **摘要**：用户订阅 Max 计划并已经使用 overflow 配额 $50，但增加资金和调整上限后 Rate Limit 错误依旧存在。
- **关注点**：计费/配额系统的实时性与准确性是高频痛点，该问题被关闭可能有官方介入解决。

### 4. "所有 Issue 都被自动关闭？"工作流程质疑（#30407）
- **标签**：Question | **已关闭** | 评论 20 | 👍 9
- **链接**：[Issue #30407](https://github.com/anthropics/claude-code/issues/30407)
- **摘要**：用户质疑仓库的 Issue 管理工作流，感觉所有 Issue 未经审核即被自动关闭，引发社区对官方支持流程的讨论。
- **关注点**：社区对官方响应机制的信任度问题，值得官方反思。

### 5. PDF 读取功能依赖 poppler-utils 但未文档化（#23704）
- **标签**：Bug / Docs / Linux | **开放中** | 评论 16 | 👍 20
- **链接**：[Issue #23704](https://github.com/anthropics/claude-code/issues/23704)
- **摘要**：Read 工具宣称支持 PDF 读取，但实际依赖 `poppler-utils`（`pdftoppm`），该依赖未文档化且在常见的容器环境（如 node:22-bookworm）中未预装，安装后也未自动检测生效。
- **关注点**：工具能力与文档严重不符，影响 CI/CD 容器化使用场景，获得 20 个👍表明不少用户踩坑。

### 6. VSCode 扩展中 /model 切换是否按会话隔离？（#53246）
- **标签**：Question / macOS / Model | **已关闭** | 评论 10 | 👍 4
- **链接**：[Issue #53246](https://github.com/anthropics/claude-code/issues/53246)
- **摘要**：用户怀疑 VSCode 扩展中通过 `/model` 命令切换模型并非按聊天会话隔离，可能导致会话间模型状态污染。
- **关注点**：IDE 集成下的多会话状态管理问题，反映出用户对会话隔离性的高要求。

### 7. 账号被禁用——"This organization has been disabled"（#67069）
- **标签**：Question / External / Auth | **已关闭** | 评论 8 | 👍 1
- **链接**：[Issue #67069](https://github.com/anthropics/claude-code/issues/67069)
- **摘要**：一位中国区 Max 5x 付费用户账号于 6 月 7 日被无预警禁用。已关闭，或已私下解决。
- **关注点**：中国区用户的账号稳定性问题，涉及区域合规与风控，影响面虽小但性质严重。

### 8. 模型接受明确停止指令后仍提前停止（#86261）
- **标签**：Bug / Model | **开放中** | 评论 3 | 👍 1
- **链接**：[Issue #86261](https://github.com/anthropics/claude-code/issues/86261)
- **摘要**：报告者称模型在接受一个明确的完成条件后，会在 5 个不同会话中重复出现"答应执行但提前停止"的行为，且附有日期证据。
- **关注点**：模型指令遵循（instruction following）的稳定性问题，是当前模型质量的核心指标之一，此报告证据质量较高。

### 9. 网络受限地区代理连接报 403 错误（#30318）
- **标签**：Docs / Networking | **已关闭** | 评论 3 | 👍 12
- **链接**：[Issue #30318](https://github.com/anthropics/claude-code/issues/30318)
- **摘要**：用户针对中国及其他受限地区使用代理/VPN 时遇到 403 "Request not allowed" 的问题，提出了文档改进建议，并获得 12 个👍（说明此问题在相关地区开发者中较普遍），目前已被关闭。
- **关注点**：网络环境兼容性，特别是中文开发者的使用体验。

### 10. SDK 任务通知导致 AbortController 被取消（#86650）
- **标签**：Bug / Agent-SDK | **开放中** | 评论 2
- **链接**：[Issue #86650](https://github.com/anthropics/claude-code/issues/86650)
- **摘要**：SDK 中，task-notification 恢复一个已停止的 turn 时使用了一个已 aborted 的 AbortController，导致后续所有 tool_use 被取消并报告为用户拒绝。
- **关注点**：Agent SDK 的并发状态机健壮性问题，是构建复杂 Agent 应用的关键底层 bug。

---

## 重要 PR 进展（Top 3）

> 注：过去 24 小时内 PR 数量较少（仅 3 条），以下列出全部。

### 1. 修复安全规则中 `**` 通配符无法匹配零深度路径（#87079）
- **作者**：anishsamant | **状态**：Open | **链接**：[PR #87079](https://github.com/anthropics/claude-code/pull/87079)
- **功能**：修复 `security-patterns.json` 中 `**/*.ts` 等模式因 fnmatch 机制导致无法匹配顶层文件的问题，避免安全规则被静默绕过。

### 2. 修复 PR 审查工具包中所有 agent 的 YAML frontmatter 格式错误（#87077）
- **作者**：anishsamant | **状态**：Open | **链接**：[PR #87077](https://github.com/anthropics/claude-code/pull/87077)
- **功能**：所有 agent 的描述因包含冒号被 YAML 解析为嵌套映射导致 frontmatter 为空，此 PR 修复了该问题，恢复 agent 的 name/description/model 加载。

### 3. 新增 python-package-conda.yml 工作流（#87125）
- **作者**：Salamyamadi | **状态**：Open | **链接**：[PR #87125](https://github.com/anthropics/claude-code/pull/87125)
- **功能**：新增 conda 打包的 CI 工作流文件，内容目前只有一个 commit hash，功能尚不明确，需关注后续讨论。

---

## 功能需求趋势

结合今日大量 Issues 讨论，社区最关注的功能/改进方向如下：

1. **能力与订阅计划匹配透明化**：多个关于 Pro/Max 计划下 Remote Control、Computer Use 等功能"有权限但提示不可用"的反馈，说明用户希望有更清晰的权限说明文档和更可靠的订阅状态同步机制。
2. **会话数据持久化与恢复**：#26452 等 Issue 表明用户将会话历史视为重要生产力资产，对数据丢失零容忍，期待更完善的自动保存与备份机制。
3. **多工具链集成的文档补全**：PDF 读取依赖 poppler-utils、VS Code 扩展数据存储路径、Hooks 大输出处理等文档缺失问题频发，社区强烈期待系统性补齐工具依赖和边界行为文档。
4. **模型指令遵循稳定性**：新提交的多起 bug 报告（如 #86261）聚焦模型"接受指令但执行不完整"的行为，这是影响 Agent 自动化任务可靠性的关键瓶颈。
5. **Agent SDK 任务编排可靠性**：涉及 task-notification 恢复机制、后台任务通知丢失等问题（#86650、#86426），说明基于 Claude Code 构建复杂多 Agent 应用的开发者群体正在快速增长，对 SDK 底层稳定性提出更高要求。

---

## 开发者关注点

- **计费与配额可见性**：Rate Limit 持续报错、额度消耗速度远超预期是高频痛点，付费用户在 "Max" 档位下仍有"5 小时限制"的困惑（#86068），期望官方提供更细粒度的实时用量仪表盘。
- **网络受限地区的使用体验**：中国等地区开发者面临账号被误封（#67069）、代理环境 403（#30318）等问题，在官方未提供本地化部署方案前，期望至少能提供更友好的网络配置指导和更宽松的风控策略。
- **自动关闭 Issue 的流程信任危机**：大量 Issue 被直接标记关闭（含 duplicate/invalid），社区开始质疑官方审核流程，官方应提高关闭时的说明透明度。
- **安全规则的静默失效**：glob 模式匹配 bug（#87079）暴露了安全配置可能被静默绕过的问题，开发者期望安全相关功能有更严格的测试和回归防护。

---

> 日报完。下次更新：2026-08-18。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-17**


## 今日速览

Windows 平台的性能问题与稳定性成为今日最突出的社区焦点，特别是桌面应用鼠标卡顿和高内存占用问题持续引发热议。功能开发方面，TUI 迎来多项体验改进（`/cd` 命令、Vim 模式增强），`codex doctor` 诊断工具获得大幅强化。同时，TypeScript SDK 新增原始配置覆盖能力，权限系统兼容性修复也在持续推进。


## 社区热点 Issues

### 1. Codex App 在 Windows 11 Pro 上频繁卡顿（#20214）
**标签：** bug / windows-os / app / performance | **评论：** 106 | **👍：** 85

Windows 用户报告 Codex 桌面应用在系统资源充足（Ryzen 5 5600 + 32GB RAM）的情况下仍频繁出现冻结和卡顿。这是目前社区关注度最高的 Issue，评论数破百，点赞数达 85，表明大量 Windows 用户正遭受类似困扰。
🔗 https://github.com/openai/codex/issues/20214

### 2. Windows 桌面应用引发系统级鼠标卡顿（#38546）
**标签：** bug / windows-os / app / performance | **评论：** 31 | **👍：** 13

新近报告的严重性能问题——ChatGPT/Codex 桌面应用在**非管理员权限**下运行时会导致**整个系统的鼠标光标**出现严重卡顿。问题影响范围超出应用本身，波及用户全局操作体验。
🔗 https://github.com/openai/codex/issues/38546

### 3. VS Code 聊天会话应限定在当前工作区/项目（#25319）
**标签：** enhancement / extension / session | **评论：** 28 | **👍：** 62

社区高票功能请求：希望 VS Code 扩展中的聊天/线程历史能够按当前工作区或项目进行隔离，而不是全局混杂。该需求获得 62 个赞，反映出多项目开发者的强烈诉求。
🔗 https://github.com/openai/codex/issues/25319

### 4. Codex 移动端应支持无头远程 Linux 主机（#23200）
**标签：** enhancement / iOS / remote | **评论：** 18 | **👍：** 48

开发者希望 Codex 移动端能直接连接常驻的远程 Linux 服务器（通过 SSH），而不必依赖个人桌面应用保持在线。该需求贴合许多以 Linux 服务器为主要开发环境的用户工作流。
🔗 https://github.com/openai/codex/issues/23200

### 5. 达到周限额后 Codex 继续运行但不消耗剩余额度（#18018）
**标签：** bug / rate-limits | **评论：** 16 | **👍：** 2

用户发现达到每周 Codex 限额后，Codex 仍然继续运行，但不会消耗账户中尚有的 Credits。这一计费/使用行为的不一致让用户感到困惑，涉及配额与计费逻辑的正确性问题。
🔗 https://github.com/openai/codex/issues/18018

### 6. Codex CLI 向 Azure Responses API 发送空工具描述（#37487）
**标签：** bug / azure / CLI / tool-calls | **评论：** 12 | **👍：** 5

Codex CLI 0.147.0 在调用 Azure Responses API 时发送空的工具描述（tool description），可能导致工具调用功能异常。该问题影响 Azure 企业用户。
🔗 https://github.com/openai/codex/issues/37487

### 7. Windows 沙箱在断电后所有读操作失败（#28248）
**标签：** bug / windows-os / sandbox | **评论：** 11 | **👍：** 6

在 Codex 任务执行过程中遭遇断电后，Windows 沙箱的**所有文件读取操作**均失败，报错为 "apply deny-read ACLs"。断电导致沙箱 ACL 状态损坏，且无法自动恢复。
🔗 https://github.com/openai/codex/issues/28248

### 8. Windows 远程 SSH 会话中文件编辑审批按钮无响应（#34652）
**标签：** bug / windows-os / sandbox / app / remote | **评论：** 10 | **👍：** 1

Windows Codex 桌面应用在远程 SSH 会话中，文件编辑审批按钮无法点击响应，而 CLI 模式下审批功能正常。这阻断了远程开发场景下的关键交互流程。
🔗 https://github.com/openai/codex/issues/34652

### 9. Codex Desktop 保留 5 批 MCP/Node 进程（147 个 node.exe，占用 13.9 GiB）（#32797）
**标签：** bug / windows-os / mcp / app / performance | **评论：** 7 | **👍：** 1

Windows 版 Codex Desktop（26.707）存在严重内存泄漏：保留了五批 MCP/Node 进程，合计 **147 个 node.exe 进程、占用 13.9 GiB 内存**。该问题会迅速耗尽系统资源，严重影响长时间使用。
🔗 https://github.com/openai/codex/issues/32797

### 10. 本地 stdio MCP 服务器在单个任务中被反复派生且不回收（#38754）
**标签：** bug / windows-os / mcp / app / performance | **评论：** 4 | **👍：** 1

Windows Codex 应用中，同一任务内的每次新对话轮次都会反复派生本地 stdio MCP 服务器进程，且这些进程**不会被回收（reaped）**，导致进程数持续累积、资源不断消耗。
🔗 https://github.com/openai/codex/issues/38754

### 11. 添加 TUI 键盘快捷键以快速切换推理强度和模型（#26819）
**标签：** enhancement / app | **评论：** 4 | **👍：** 4

用户希望 Codex TUI 增加快捷键或命令面板动作，用于快速切换模型的推理强度（reasoning effort）和模型本身。当前切换流程繁琐，影响效率。
🔗 https://github.com/openai/codex/issues/26819

### 12. `codex doctor` 尚未识别 MCP 服务器问题（#38918 关联）

> 说明：以上第 10-12 条为精选补充，完整 30 条热门 Issues 请参阅 Issue 列表页。


## 重要 PR 进展

### 1. 【已合并】增强 `codex doctor` 网络诊断能力（#38918）
**功能：** 使用 Codex 的路由感知 HTTP 客户端探测配置的 Responses 推理端点（含代理和自定义 CA 行为），并对 TLS、代理认证、代理配置、解析和超时等故障进行分类。
🔗 https://github.com/openai/codex/pull/38918

### 2. 【已合并】为 `codex doctor` 增加端点保护检查（#38827）
**功能：** 在 macOS 和 Windows 上检测常见端点保护产品，当检测到可能干扰 Codex 的安全软件时，输出需要验证的 Codex 排除项清单。
🔗 https://github.com/openai/codex/pull/38827

### 3. 【已合并】TUI 新增工作目录切换命令（#38894）
**功能：** 新增 `/cd [path]` 命令，可在空闲本地会话中切换工作目录并保留对话历史；省略路径时切换至 `~`；同时会重新加载项目配置和相关指令。
🔗 https://github.com/openai/codex/pull/38894

### 4. 【已合并】TypeScript SDK 支持原始配置覆盖（#38817）
**功能：** 新增 `CodexOptions.configOverrides`，允许以原始 `--config key=value` 形式传入有序配置覆盖项，解决权限映射等结构化点分键配置无法安全表达的问题。
🔗 https://github.com/openai/codex/pull/38817

### 5. 【已合并】拒绝已废弃的 app-server 权限配置文件字段（#38919）
**功能：** 此前 app-server 请求反序列化会静默忽略未知字段，导致使用已移除的 `permissionProfile` 字段的客户端的权限设置被静默丢弃。此 PR 改为直接拒绝该字段，避免配置意外失效。
🔗 https://github.com/openai/codex/pull/38919

### 6. 【已合并】兼容遗留的 `:project_roots` 权限条目（#38916）
**功能：** 在权限配置文件由 `:project_roots` 更名为 `:workspace_roots` 之前写入的旧配置仍可能包含 `:project_roots`，此前会被当作未知标记而丢弃，导致文件系统限制失效。此 PR 将其作为 `:workspace_roots` 的别名解析。
🔗 https://github.com/openai/codex/pull/38916

### 7. 【已合并】Vim 模式下用 history-up 编辑排队消息（#38907）
**功能：** 在 Vim 普通模式且输入区为空时，配置的 history-up 绑定会恢复最新排队的后续消息供编辑，并从队列中移除该消息，避免重复提交。
🔗 https://github.com/openai/codex/pull/38907

### 8. 【已合并】独立恢复线程时间戳最大值（#38893）
**功能：** 修复了 `updated_at_ms` 和 `recency_at_ms` 两个时间戳计数器在最大值分属不同线程时无法独立恢复的问题。此前状态初始化可能丢失其中一个计数器的最大值。
🔗 https://github.com/openai/codex/pull/38893

### 9. 【已合并】将外部编辑器缓冲区与沙箱可写路径隔离（#38830）
**功能：** 外部编辑器缓冲区可能包含当前输入区文本，不应放在受限文件系统策略暴露为可写的目录中。此 PR 将编辑器缓冲文件创建在受保护的 `editor` 目录下。
🔗 https://github.com/openai/codex/pull/38830

### 10. 【已合并】支持保留线程 ID 的元数据暂存（#38819）
**功能：** 新增 `ThreadManager::reserve_thread_id`，允许外部调用方在线程启动前将宿主机持有的状态与线程关联；恢复已有线程时拒绝使用保留 ID。
🔗 https://github.com/openai/codex/pull/38819

### 11. 【已合并】在远程控制握手中识别 Mac mini 主机（#38840）
**功能：** 在 macOS 上检查硬件配置，当检测到设备名为 "Mac mini" 时，在远程控制 WebSocket 握手中发送 `x-codex-host-device-kind: mac_mini` 头，便于远程端识别设备类型。
🔗 https://github.com/openai/codex/pull/38840

### 12. 【已合并】共享 TUI 编辑器组件间的按键映射（#38837）
**功能：** 将 `RuntimeKeymap` 的编辑器部分存入 `Arc`，使聊天输入区和内嵌文本区使用同一份按键映射快照，确保自定义绑定在组件间保持一致。
🔗 https://github.com/openai/codex/pull/38837


## 功能需求趋势

综合全部 Issues，社区最关注的功能方向如下：

- **远程开发体验**：移动端直连无头 Linux 主机（#23200）、桌面端支持“连接 → 项目 → 线程”分组（#24295）、SSH 重启后保留 `--remote-control` 参数（#23699）等需求持续涌现。
- **会话与工作区隔离**：#25319 希望 VS Code 扩展的聊天历史按当前项目隔离；#32519 提出 ChatGPT 与 Codex 之间共享项目上下文与双向任务交接。
- **Windows 性能与稳定性**：本期热点 Issues 中 Windows 专属的性能问题占据近半数（#20214、#38546、#32797、#38754 等），涉及卡顿、内存泄漏、MCP 进程失控、沙箱异常等多方面。
- **MCP 服务器管理**：#11765 支持通过 UI 开关 MCP 服务器而非仅依赖 `config.toml`；#38754 关注 MCP 进程生命周期管理。
- **TUI / 编辑器增强**：#2379 输入撤销/重做、#26819 快捷键切换推理强度/模型、TUI 新增 `/cd` 命令（#38894）等，显示 CLI 重度用户对终端交互效率的追求。
- **使用额度与计费透明性**：#18018 达到周限额后仍消耗 Credits 的行为困惑、#29900 对 Codex 使用限制与 Pro 价值的反馈，表明用户对配额策略的敏感度较高。
- **跨平台一致性**：沙箱行为在 Windows 与 macOS/Linux 间的差异（#28248、#32315）、Windows 系统代理未传递给 WSL2 内进程（#15447）等，体现用户对跨环境一致体验的期待。


## 开发者关注点

- **Windows 性能问题集中爆发**：从系统级鼠标卡顿（#38546）到应用内冻结（#20214），再到 MCP/Node 进程批量滞留占用近 14 GiB 内存（#32797），Windows 平台开发者正面临严重的稳定性困扰。相关 Issue 评论数和点赞数均居高不下。
- **远程开发流程断点**：Windows 远程 SSH 会话中文编辑审批按钮失效（#34652）、远程压缩 404 导致会话连续性丢失（#38856）、SSH 重启后移动端远程控制失效（#23699），远程场景下的关键路径仍需打磨。
- **配额与计费行为困惑**：#18018 和 #38900 均报告了与周限额相关的异常行为——前者是超限后继续运行但未消耗剩余 Credits，后者是限额“意外”刷新且重置日期被不断推迟。这些计费逻辑的不确定性影响了用户对额度的信任。
- **进程与资源泄漏**：#32797（147 个 node.exe / 13.9 GiB）和 #38754（stdio MCP 进程反复派生不回收）指向同一类问题——Windows 平台上的子进程生命周期管理存在系统性缺陷。
- **沙箱健壮性不足**：断电后沙箱 ACL 损坏（#28248）、Base64 载荷超限导致沙箱设置失败（#32315），反映出 Windows 沙箱在异常场景下的恢复能力有待加强。
- **会话历史与状态一致性**：远程 Linux 会话中重复标题、空白线程与存档损坏（#19267）、恢复会话时游标错位（#38792）、系统技能目录被意外删除（#19265）等问题，表明会话持久化层仍存在数据一致性风险。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# 🤖 Gemini CLI 社区动态日报

**日期：2026-08-17** | **数据来源：** [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 📌 今日速览

今日社区动态聚焦于**子代理（Subagent）行为可靠性**与**终端稳定性**两大核心议题。多个高优先级 Issue 揭示了子代理在达到执行上限时误报成功、通用代理挂起等关键缺陷；同时，社区涌现了一批由 AI 辅助生成的高质量修复 PR（#28812-#28848），涵盖 TUI 挂起、认证失败处理、MCP 工具 Schema 规范化等痛点。此外，Auto Memory 功能的安全性与低信号会话处理问题也持续引发讨论。

---

## 🚀 版本发布

### v0.56.0-nightly.20260816.g2a87e7be1
- **发布时间：** 2026-08-16
- **变更说明：** 常规 Nightly 更新，无显著功能变更。
- **完整变更日志：** [查看详情](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260815.g2a87e7be1...v0.56.0-nightly.20260816.g2a87e7be1)

---

## 🔥 社区热点 Issues（TOP 10）

### 1. 🐛 子代理达到 MAX_TURNS 后被误报为成功
- **Issue #22323** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/22323) | **P1** | 💬 12 评论 | 👍 2
- **核心问题：** `codebase_investigator` 子代理在因 `MAX_TURNS` 中断时，最终报告却显示 `status: "success"`，隐藏了真实的执行中断，误导主代理决策。
- **社区关注原因：** 这是子代理可信度的严重缺陷，直接影响多代理协作的可靠性。目前已有对应的修复 PR（#28815）。

### 2. 🐛 通用代理（Generalist agent）无限挂起
- **Issue #21409** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/21409) | **P1** | 💬 8 评论 | 👍 8
- **核心问题：** `gemini-cli` 一旦将任务委托给通用代理，就会无限期挂起（用户等待长达 1 小时无响应）。简单的文件夹创建操作也会触发。用户发现通过提示词禁止使用子代理可临时规避。
- **社区关注原因：** 高 👍 数表明影响范围广，且属于阻断性问题。

### 3. 🛠️ 利用模型 bash 亲和性，实现零依赖 OS 沙箱及执行后意图路由
- **Issue #19873** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/19873) | **P2** | 💬 8 评论 | 👍 1
- **核心内容：** 建议利用 Gemini 3 模型的 POSIX 工具链原生能力，通过零依赖沙箱机制让模型安全地以 bash 方式操作，并在执行后引入意图路由层提升安全性。
- **社区关注原因：** 这是一个方向性的架构增强提案，若实现将显著提升模型操作效率与安全性。

### 4. 🧪 可扩展的组件级行为评估体系
- **Issue #24353** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/24353) | **P1** | 💬 7 评论
- **核心内容：** 作为 EPIC，旨在建立组件级评估框架，目前已有 76 个行为评估测试，覆盖 6 个 Gemini 模型版本，但需进一步扩展开销与覆盖面。
- **社区关注原因：** 反映了项目方对质量保障体系的持续投入，是长期稳定性的重要保障。

### 5. 🔍 AST 感知的文件读取/搜索/映射评估
- **Issue #22745** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/22745) | **P2** | 💬 7 评论 | 👍 1
- **核心内容：** EPIC 追踪调查 AST 感知工具的价值，期望通过精确读取方法边界减少 token 消耗与轮次浪费。
- **社区关注原因：** 该方向若落地可显著提升代码库导航效率，属于性能优化的重要探索。

### 6. 💡 Gemini 对 Skills 和子代理的主动使用不足
- **Issue #21968** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/21968) | **P2** | 💬 6 评论
- **核心问题：** 用户反馈 Gemini 默认几乎不会主动调用自定义 Skills 和子代理，即使任务高度相关，也需显式指令才会使用。
- **社区关注原因：** 提示词工程的核心痛点，直接影响用户体验与自动化程度。

### 7. 🧠 Auto Memory 对低信号会话的无限重试
- **Issue #26522** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/26522) | **P2** | 💬 5 评论
- **核心问题：** Auto Memory 后台提取代理若判定会话为低信号而跳过处理，该会话会持续被标记为未处理，导致无休止的重试。
- **社区关注原因：** 资源浪费与效率问题，需在提取结果中引入显式的 skip 状态记录。

### 8. 🔒 Auto Memory 的确定性脱敏与日志精简
- **Issue #26525** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/26525) | **P2** | 💬 4 评论
- **核心问题：** Auto Memory 将本地 transcripts 内容发送至模型上下文后，才通过提示词要求脱敏，且脱敏逻辑（如正则）分散，存在密钥泄露风险，同时日志记录过度。
- **社区关注原因：** 安全隐私关键问题，需要确定性的脱敏机制与更严格的日志控制。

### 9. 🐛 Shell 命令执行完成却卡在 “Waiting input”
- **Issue #25166** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/25166) | **P1** | 💬 4 评论 | 👍 3
- **核心问题：** 简单 CLI 命令执行完毕后，终端仍显示为活动状态并等待输入，导致 Gemini 持续挂起。
- **社区关注原因：** 高频出现的终端状态同步 bug，影响交互流畅性。

### 10. 🐛 Browser 子代理在 Wayland 环境失败
- **Issue #21983** | [查看详情](https://github.com/google-gemini/gemini-cli/issues/21983) | **P1** | 💬 4 评论 | 👍 1
- **核心问题：** Browser 子代理在 Wayland 显示服务器下直接失败，终止原因为 `GOAL`。
- **社区关注原因：** Linux 用户特定环境兼容性问题，涉及图形界面集成稳定性。

---

## 🔧 重要 PR 进展（TOP 10）

### 1. ⏱️ [SSR Agent] 修复 TUI 无限期挂起问题（#21477）
- **PR #28812** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28812) | **P1** | `area/core`
- **修复内容：** 为 `getProcessInfo()` 中的 `execAsync` 调用添加超时机制，防止在裸 Linux 终端启动时因 `ps` 命令挂起导致 TUI 卡在 “Initializing...”。
- **重要性：** 解决 P1 级别的启动阻塞问题。

### 2. 🔄 [SSR Agent] 保留子代理恢复时的原始终止原因（#22323）
- **PR #28815** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28815) | **P1** | `area/agent`
- **修复内容：** 修复 `LocalAgentExecutor` 在子代理触发 `MAX_TURNS`/`TIMEOUT` 后的宽限恢复轮中调用 `complete_task` 时，误报成功状态的问题。
- **重要性：** 直接对齐今日热点 Issue #22323，提升多代理协作的可观测性。

### 3. 🔐 非交互模式下优雅处理 refreshAuth 失败
- **PR #28848** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28848) | **P2** | `area/security` | 新增
- **修复内容：** `--prompt` 模式下若 `refreshAuth()` 失败，不再抛出未捕获的原始堆栈，而是输出清晰的错误信息并返回专用退出码。

### 4. 📝 [SSR Agent] 更新 /clear 命令文档，包含上下文重置说明
- **PR #28847** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28847) | **P3** | `area/agent`
- **修复内容：** 修正 `docs/reference/commands.md` 中 `/clear` 命令仅清除屏幕的描述，补充其同时清除活动上下文的说明。

### 5. 🛡️ 规范化 MCP 工具 Schema，强制根级 `type: object`
- **PR #28839** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28839) | **P2** | `area/agent`
- **修复内容：** 针对部分 MCP 服务器广告的工具 Schema 缺少 `type` 或类型非法的问题，在转发前进行规范化处理，避免 Vertex AI 等严格校验方拒绝请求。

### 6. 🔧 修复 perf-tests 中过时的 ripgrep 导入
- **PR #28838** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28838) | **P1** | `area/core`
- **修复内容：** 将 `globalSetup.ts` 中移除的 `canUseRipgrep` 导入更新为 `resolveRipgrepPath`，修复 Nightly 性能测试中止问题。

### 7. 📢 修复 Auto 模式在 /model 选择器中缺失的问题
- **PR #28836** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28836) | **P2** | `area/core`
- **修复内容：** 当 `dynamicModelConfiguration` 启用且用户无预览权限时，`auto` 别名因被标记为 `isPreview` 而被过滤，现改为始终显示。

### 8. 🧹 抑制工作区扫描中瞬时目录的 ENOENT 误报
- **PR #28834** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28834) | **P2** | `area/core`
- **修复内容：** BFS 工作区遍历时，若遇到 `readdir` 与递归下降之间消失的瞬时目录（如 `projects.json.lock`），不再打印误导性的 ENOENT 警告。

### 9. 🧬 深度合并 A2A Server 的嵌套设置，防止用户配置丢失
- **PR #28842** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28842) | **已关闭**
- **修复内容：** 将 A2A Server 的浅合并改为一级深度合并，避免工作区设置覆盖用户的 `enableRecursiveFileSearch` 等配置。

### 10. 📋 新增 `--list-models` 标志以 JSON 格式输出可用模型
- **PR #28843** | [查看详情](https://github.com/google-gemini/gemini-cli/pull/28843) | **已关闭**
- **功能特性：** 新增 `gemini --list-models` 命令，输出可用模型 JSON 后退出，便于集成方与编排器进行编程式模型发现。

---

## 📊 功能需求趋势

### 1. **子代理（Subagent）行为可靠性**（高频关键词）
- **趋势：** 多个 Issue 聚焦子代理的触发策略（#21968）、权限控制（#22093）、轨迹可分享性（#22598）、调度与恢复机制（#22323）。
- **方向：** 社区期待更智能的子代理调度与更透明的执行过程。

### 2. **Auto Memory 安全性与效率**
- **趋势：** 围绕低信号会话重试（#26522）、脱敏机制（#26525）、无效补丁处理（#26523）等问题展开。
- **方向：** 提升记忆提取的确定性、安全性与资源利用效率。

### 3. **终端体验与稳定性**
- **趋势：** “等待输入”卡死（#25166）、终端 resize 闪烁（#21924）、外部编辑器退出后渲染损坏（#24935）等问题反馈集中。
- **方向：** 强制全屏刷新、迁移至 `RenderStatic` 等底层优化成为关键。

### 4. **AST 感知的智能代码分析**
- **趋势：** #22745 与 #22746 共同探索 AST 感知的文件读取与代码库映射，期望降低 token 消耗、提升导航效率。
- **方向：** 引入 `tilth`、`glyph` 等工具，作为 `codebase_investigator` 的潜在升级路径。

### 5. **破坏性行为抑制**
- **趋势：** #22672 明确提出模型应在复杂 git 操作、数据库维护等场景中避免使用危险命令（如 `git reset`、`--force`）。
- **方向：** 在提示词或工具层加入安全护栏，鼓励使用更安全的替代方案。

---

## 🧑‍💻 开发者关注点

### 高频痛点
1. **子代理挂起与误报：** 通用代理无限挂起（#21409）与 `MAX_TURNS` 误报成功（#22323）严重干扰自动化流程，开发者急需稳定可靠的多代理执行保障。
2. **命令执行状态不同步：** Shell 命令已完成但 TUI 显示 “Waiting input”（#25166），以及 `\n` 转义错误（#22466）等细节问题影响日常使用。
3. **配置生效不一致：** Browser Agent 忽略 `settings.json` 覆盖（#22267）、符号链接不被识别（#20079）等问题，增加了按需定制的成本。
4. **工具数量与上下文超载：** 超过 400 个工具时触发 400 错误（#24246），社区期待更智能的工具作用域过滤机制。

### 积极信号
- 大量 **SSR Agent** 辅助生成的修复 PR 正在快速合入（如 #28812、#28815），表明项目方在利用 AI 工具加速问题解决，社区反馈良好。
- 社区对 **`--list-models`** 等程序化接口（#28843）反响积极，期待更好的自动化与集成体验。

---

*本日报基于公开 GitHub 数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-17**


## 今日速览

昨日无新版本发布，但社区提交了 16 条 Issue 更新，其中 **6 条为全新提交**，暴露了多个与 MCP 认证、Windows 平台稳定性及会话恢复相关的关键缺陷。值得特别关注的是**内存压力看门狗在上下文使用率极低时错误触发强制压缩**（#4506），以及**非交互模式下仓库级插件配置被静默忽略**（#4507），这两者均可能显著影响开发者在生产环境中的使用体验。此外，修复了 Slack 集成中 SDK 服务器就绪状态误报的已关闭问题（#4503），但认证/插件/会话相关的**长期悬而未决**问题仍在持续积累。


## 社区热点 Issues（精选 10 条）

### 1. 内存看门狗在 23% 上下文使用率时强制压缩，空转直至 OOM
**#4506** · 🔴 新提交 · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4506)
> **摘要**：长会话在上下文使用率仅 23%（400k 窗口）时被进程内存看门狗反复触发强制压缩，回收 0.003% token 后继续循环直至 OOM。
> **重要性**：严重的内存管理缺陷，直接影响长会话稳定性，可能导致数据丢失和频繁崩溃。

### 2. 非交互模式忽略仓库级 `enabledPlugins` 配置
**#4507** · 🔴 新提交 · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4507)
> **摘要**：`.github/copilot/settings.json` 中的 `enabledPlugins` 在 `copilot -p` 模式下不生效，与交互模式行为不一致。
> **重要性**：配置不一致导致 CI/CD 流水线中插件行为不可预期，影响自动化工作流可靠性。

### 3. Atlassian MCP OAuth 认证在 1.0.80 版本回归（RFC 8414 §3.3）
**#4490** · 作者：ChandrasekarCK · 1 评论 · [链接](https://github.com/github/copilot-cli/issues/4490)
> **摘要**：MCP OAuth 认证失败：授权服务器声明的 issuer 与元数据发现 URL 不匹配（1.0.78 正常）。
> **重要性**：版本回归问题，影响所有使用 Atlassian 生态的开发者，阻碍 MCP 功能推进。

### 4. Windows 下 MCP OAuth 间歇性 socket 错误 10013
**#4463** · 作者：msosav · 1 评论 · [链接](https://github.com/github/copilot-cli/issues/4463)
> **摘要**：Windows 上远程 HTTP MCP 服务器 OAuth 认证间歇性在浏览器授权流程打开前失败。
> **重要性**：Windows 平台特定问题，影响大规模团队中不同 OS 的协作一致性。

### 5. 远程 MCP 并发调用触发多次 token 刷新，互相取消
**#4472** · 作者：jmtt89 · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4472)
> **摘要**：并发工具调用在 token 过期时各自触发 refresh，创建新 rmcp 服务导致在途调用被取消。
> **重要性**：高度影响并行工具调用场景的可靠性，每次刷新都可能导致正在执行的操作失败。

### 6. `claude-haiku-4.5` 子代理不支持 `medium` 推理力度
**#4473** · 作者：philtillman · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4473)
> **摘要**：CLI 内部将子代理任务路由到 claude-haiku-4.5 时应用了不支持的 `medium` 推理力度。
> **重要性**：模型参数与模型能力不匹配，反映新模型接入时配置适配不足。

### 7. 插件更新因其他会话文件锁失败（Windows）
**#4488** · 作者：grjsrinivas · 1 评论 · [链接](https://github.com/github/copilot-cli/issues/4488)
> **摘要**：多 Copilot CLI 会话或 VS Code 窗口打开时插件更新被文件锁阻止，即使插件未被使用。
> **重要性**：Windows 平台多实例场景常见痛点，妨碍插件迭代效率，且影响所有依赖插件的自动化。

### 8. 编辑权限请求超时无提示
**#4486** · 作者：dscho · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4486)
> **摘要**：未立即响应编辑权限请求时操作超时，对多会话夜间运行的用户造成极大困扰。
> **重要性**：交互体验严重退化，影响长时间运行和并行会话工作流。社区对权限模型的变更担忧明显。

### 9. 恢复的会话残留过期 connection item ID，无法恢复
**#4505** · 🔴 新提交 · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4505)
> **摘要**：恢复中断的会话后所有提示均报 `400 input item ID does not belong to this connection`，/fork 也无法恢复。
> **重要性**：会话数据完整性缺陷，导致恢复后的会话完全不可用，影响长会话工作流。

### 10. `account.getQuota` 返回错误的 `resetDate`
**#4504** · 🔴 新提交 · 无评论 · [链接](https://github.com/github/copilot-cli/issues/4504)
> **摘要**：JSON-RPC `account.getQuota` 响应将请求时间戳误作为配额重置日期。
> **重要性**：API 数据正确性问题，影响基于配额信息构建的第三方工具和自动化脚本。


## 重要 PR 进展

### #3163 · ViewSonic monitor（唯一活跃 PR，已存续 3 个月）
**状态**：打开中 · 更新于 2026-08-16 · [链接](https://github.com/github/copilot-cli/pull/3163)
> **摘要**：为 #2591、#3561、#3559 提供显示器相关支持，已启动 GitHub Action runner。
> **观察**：PR 描述过于简略，缺少必要上下文。长期未合入且无维护者回应，社区关注度持续走低。


## 功能需求趋势

从全部 16 条 Issue 中可提炼出以下社区关注方向：

| 方向 | 相关 Issue | 关注度 |
|------|-----------|--------|
| **MCP 生态稳定性** | #4490、#4463、#4472 | 高 — 认证、并发、跨平台问题集中爆发，直接影响 MCP 采用信心 |
| **会话生命周期管理** | #4505、#4502、#4474、#4489 | 高 — 会话恢复、取消归档、状态保留是高频诉求，当前体验断裂明显 |
| **内存/性能优化** | #4506 | 中高 — 内存看门狗误触发可能导致 OOM，急需修复 |
| **插件体系完善** | #4488、#4487、#4507 | 中 — 依赖管理缺失、配置不一致、文件锁冲突阻碍插件生态发展 |
| **Windows 平台支持** | #4463、#4488、#4474 | 中 — 平台特性问题反复出现，需要系统性关注 |
| **配额/用量透明度** | #4504 | 低 — API 数据正确性影响第三方集成 |
| **模型适配一致性** | #4473 | 低 — 路由参数需与模型能力对齐 |


## 开发者关注点

### 🔴 痛点高频词
- **MCP OAuth 认证链路脆弱**：每次刷新都可能导致在途请求取消（#4472），跨平台失败（#4463），版本回归（#4490）——MCP 工具链的可信度正在被消耗。
- **会话恢复体验断裂**：恢复后不可用（#4505）、Agent 未选中（#4489）、超时归档（#4474）、无法取消归档（#4502）——长会话工作流多环节受阻。
- **Windows 平台问题持续**：插件更新失败、OAuth 间歇失败、会话超时归档——平台支持质量不均，影响跨 OS 团队协作。

### 🟡 期望改进方向
- **#4487 插件依赖规范化**：社区明确提出需要插件的依赖声明与自动安装机制，这是插件生态走向成熟的关键一步。
- **#4502 会话取消归档**：用户需要一个意外操作的反悔通道，尤其是对长期运行的活跃会话。
- **可预期的权限行为**：编辑权限超时（#4486）引发了对权限模型变化的担忧，社区希望默认行为至少是可预期和可配置的。

### 📌 整体趋势观察
过去 24 小时提交的问题集中于**可靠性**而非新功能，表明 1.0.80 版本引入的 MCP/认证改动存在系统性回归隐患。插件配置不一致（#4507）和配额 API 错误（#4504）等问题也反映出项目正处在架构演进期，基础设施层尚需加固。建议开发者在升级到 1.0.80+ 时进行 MCP 认证和会话恢复回归测试，并关注后续补丁版本。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-17

## 📌 今日速览
今日社区整体活跃度平稳，无新版本发布。核心关注点集中在三个方面：**Session 会话管理功能缺失**（用户强烈要求新增删除/管理命令）、**Windows 平台路径兼容性问题**（PowerShell 默认目录导致启动失败）以及**记忆层与定时任务管理入口的可用性优化**。此外，两个来自外部贡献者的代码修复 PR（BrokenPipeError 处理、字符串截断逻辑修复）正在推进中，反映了社区对 Web 端与文本渲染稳定性的关注。

*数据范围：2026-08-16 至 2026-08-17*

---

## 📦 版本发布
过去 24 小时内无新版本发布，当前最新版本仍为 v0.33.0。

---

## 🔥 社区热点 Issues

### #1783 [Feature Request] 添加 /delete 命令删除 Session
- **作者**: proccl | 创建: 2026-04-07 | 更新: 2026-08-16 | 💬 6 | 👍 1
- **链接**: [Issue #1783](https://github.com/MoonshotAI/kimi-cli/issues/1783)
- **重要性**: 长期开放的高频需求。用户面对日益膨胀的 session 列表和敏感信息清理需求，只能手动删文件，体验割裂。社区反应持续但不热烈，无官方表态，属于长期未解决的核心痛点。
- **摘要**: 建议新增 `/delete <session_id>` 斜杠命令，以替代手动操作 `~/.kimi/sessions/` 目录。

### #2600 [bug] Windows PowerShell7 默认 D 盘启动时无法定位路径
- **作者**: RooKichenn | 创建: 2026-08-11 | 更新: 2026-08-16 | 💬 5 | 👍 0
- **链接**: [Issue #2600](https://github.com/MoonshotAI/kimi-cli/issues/2600)
- **重要性**: 新发现的 Windows 平台兼容性 bug。用户自定义 PowerShell 启动目录为 D 盘后，直接从 D: 打开 CLI 会找不到路径。社区中有 5 条评论，属于活跃讨论中的新问题。
- **摘要**: 版本 0.33，设置 PowerShell7 默认目录为 D 盘后，从 D: 启动 kimi code 出现路径丢失问题。

### #1478 [enhancement] 优化记忆层，大项目开发体验差
- **作者**: hahy36 | 创建: 2026-03-17 | 更新: 2026-08-16 | 💬 4 | 👍 0
- **链接**: [Issue #1478](https://github.com/MoonshotAI/kimi-cli/issues/1478)
- **重要性**: 老牌长期 Issue（5 个月），反映高级用户对大项目上下文的强烈需求。用户对仅有的 `agent.md` 不满，并参考了 OpenClaw 的 MEMORY.md 分层记忆机制，社区讨论活跃。
- **摘要**: 用户请求优化“记忆层”，使其能在大型项目中保持上下文。当前文档中只有 `agent.md`，缺乏分层记忆机制，长期项目维护十分痛苦。

### #2605 [CLOSED] 定时任务无用户可见管理入口
- **作者**: WilliamLambertCN | 创建/更新: 2026-08-16 | 💬 1 | 👍 0
- **链接**: [Issue #2605](https://github.com/MoonshotAI/kimi-cli/issues/2605)
- **重要性**: 新反馈的可用性盲区。模型创建的 Cron 定时任务在 TUI 中无任何 `/cron` 命令或 `/tasks` 入口可见，普通用户根本无法管理，只能手动修改 JSON 文件，设计存在明显缺陷。
- **摘要**: 模型通过 `CronCreate` 工具创建的定时任务在 TUI 中无查看/管理入口，文档也无说明。文件持久化在 `~/.kimi-code/cron/<哈希>/<任务ID>.json`，用户需要一种可见的管理方式。

---

## 🔧 重要 PR 进展

### #864 [CLOSED] feat: --starting-prompt flag to prompt without exit
- **作者**: stebbins | 创建: 2026-02-02 | 更新: 2026-08-17
- **链接**: [PR #864](https://github.com/MoonshotAI/kimi-cli/pull/864)
- **重要性**: 旧 PR 在近 6 个月后终于有更新动态。该特性允许用户在启动 CLI 时通过 `--starting-prompt`（简写 `-s`）直接注入首条提示词而无需进入交互模式，非常便于脚本自动化调用。
- **摘要**: 新增 `--starting-prompt` / `-s` 标志，用于在启动时直接传递提示词，无需交互式退出。关闭了关联 Issue #887。

### #2324 [OPEN] fix(web): handle BrokenPipeError in SessionProcess.send_message
- **作者**: Ricardo-M-L | 创建: 2026-05-19 | 更新: 2026-08-16
- **链接**: [PR #2324](https://github.com/MoonshotAI/kimi-cli/pull/2324)
- **重要性**: 修复 Web 端潜在崩溃点。在 `src/kimi_cli/web/runner/process.py` 中，`send_message` 方法在写入 `process.stdin` 和 await `drain()` 时，未考虑子进程可能已在 `start()` 和写入之间退出的情况，导致 `BrokenPipeError` 崩溃。社区修复质量高。
- **摘要**: 修复 Web 端 `SessionProcess.send_message` 中因未检测子进程已退出而引发的 `BrokenPipeError` 问题。

### #2449 [OPEN] fix(string): strip newlines in shorten_middle before the length check
- **作者**: Ricardo-M-L | 创建: 2026-06-13 | 更新: 2026-08-16
- **链接**: [PR #2449](https://github.com/MoonshotAI/kimi-cli/pull/2449)
- **重要性**: 字符串渲染的细节修复。`shorten_middle(text, width, remove_newline=True)` 在“短输入”时提前返回，跳过了换行符折叠逻辑，导致提取到的单行工具调用参数摘要中仍残留换行符，影响渲染美观。
- **摘要**: 修复 `shorten_middle` 函数在长度检查前未折叠换行符的问题，确保 `extract_key_argument` 渲染结果保持单行。

---

## 📈 功能需求趋势

从当前活跃的 Issues 中，可以提炼出社区呼声最高的几个功能方向：

- **会话管理（Session Management）**：Issue #1783 的 `删除` 需求并非孤立。用户普遍要求更多的 Session 生命周期控制，包括列表、查看、归档和彻底删除，以解决“会话过多难以管理”和“敏感信息清理”两大痛点。
- **CLI 可用性与跨平台兼容**：Issue #2600 暴露了 Windows 环境下路径解析的脆弱性。用户自定义启动目录后导致的路径丢失，说明工具对非标准系统配置的适配仍有不足，这是提升开发者体验的直接障碍。
- **上下文记忆与长期项目支持**：Issue #1478 持续高热，表明中大型项目开发者对“记忆层”的需求远未满足。分层记忆（如 SOUL.md / USER.md / MEMORY.md）与长期上下文保留是这一波生成式编码工具的核心竞争点，社区期待更结构化的解决方案。
- **后台任务与自动化管理的可视化**：Issue #2605 揭示了定时任务（Cron）的工具化盲区。社区不仅需要能创建任务，更需要能在 TUI 中查看、暂停、删除和编辑这些任务，不再强制用户去手动操作 JSON 文件。

---

## 🧑‍💻 开发者关注点

- **Windows 路径问题在升级后依旧存在**：虽然 CLI 已经迭代到 0.33 版本，但 PowerShell 启动目录变更导致的路径丢失仍未被修复。开发者希望在启动时，系统有更健壮的目录解析逻辑，尤其在非系统盘启动的 Windows 场景下。
- **Session 清理的刚需**：用户明确指出了“手动到 `~/.kimi/sessions/` 下删文件夹”这一原始方式的低效与风险（误删、敏感信息残留）。这已经不仅是功能请求，更是对数据安全与工程效率的明确诉求。
- **大型项目中“失忆”的烦恼**：用户对大项目开发中模型频繁丢失上下文、缺乏长期记忆非常不满，并且开始主动参考其他竞品（如 OpenClaw）的实现。社区希望官方能提供类似 `MEMORY.md` 的分层记忆机制，而不仅仅是单一的 `agent.md`。
- **自动化管理诉求增强**：对定时任务管理的缺失，开发者反馈“不应该让用户手动去改 JSON”，表明社区已默认 CLI 应具备成熟的任务可视化与管理系统，而非仅仅是程序员的编码工具。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-17

> 数据来源：github.com/anomalyco/opencode

## 今日速览

OpenCode 社区当前的核心矛盾集中在**稳定性与资源管理**：大量 Issue 指向桌面端/CLI 在流式错误后陷入“永久思考”状态、本地模型超时、以及 `/tmp` 目录下原生库文件泄漏导致的 SSD 磨损等问题。与此同时，v2 版本的 UI 细节（后台任务状态、技能时间线呈现）正在密集修复中，社区对会话收藏/固定、自定义权限快捷键等功能需求呼声渐高。

- **稳定性痛点集中爆发** — 流式错误后 UI 卡死（#32366、#38644、#36370）、本地 Provider 超时（#26602）、空响应静默退出（#41469）等 5+ 个 Issue 指向相同的“卡死—无错误提示—需重启”模式，社区已在多个线程中讨论根因。
- **v2 桌面端与 TUI 持续打磨** — 今日合入的 PR 集中于后台子代理状态标识、技能时间线呈现、会话 spinner 性能优化，以及 shell 进度流式输出，显示 v2 正在快速收敛体验细节。
- **资源泄漏问题引发用户“自救”** — Issue #42880 中用户因 `.so` 文件在 `/tmp` 中“高速生成”而选择将 `/tmp` 挂载为 tmpfs 并定时清理，该问题与 #37671（v2 headless 命令加载 OpenTUI 并泄漏临时文件）很可能是同一根因，值得官方优先排查。

---

## 社区热点 Issues（Top 10）

### 1. [UX] Ctrl+C 不应退出 OpenCode，与通用复制快捷键冲突
**#7957** · 评论 16 · 👍 49 | [链接](https://github.com/anomalyco/opencode/issues/7957)

> **为什么重要：** 这是社区中热度最高（👍 49）的 Issue，自 1 月提出至今仍开放。Ctrl+C 作为 Windows/Linux 通用复制快捷键，用户误触即导致应用退出。高频痛点 + 高赞同数表明该问题直接影响日常使用体验。

> **社区反应：** 16 条评论持续讨论中，暂无明确修复方案落地。

---

### 2. Desktop 对本地 Provider 请求 5 分钟超时，设置失效
**#26602** · 评论 11 · 👍 1 | [链接](https://github.com/anomalyco/opencode/issues/26602)

> **为什么重要：** 用户明确设置 `"timeout": false` 或更大超时值，但 Desktop 仍在该配置之外强制 5 分钟 Headers 超时。对使用本地大模型的用户（如 Ollama、vLLM）是严重障碍——长思考链路的模型很容易超过 5 分钟。

> **社区反应：** 11 条评论，用户确认 Provider 仍在工作但 OpenCode 已中止请求。

---

### 3. [紧急] Zen 付费余额仍触发每日免费额度限制
**#33318** · 评论 9 · 👍 0 | [链接](https://github.com/anomalyco/opencode/issues/33318)

> **为什么重要：** 用户充值 $20 后使用不足 1 小时即被 FreeUsageLimitError 拦截，付费与免费额度判定逻辑存在缺陷，直接影响付费用户体验。

> **社区反应：** 9 条评论，关联 #42938（Go 套餐 100% 用量后 Zen 余额未启用）疑似同类问题。

---

### 4. Bug：TUI 退出后鼠标转义序列乱码
**#20458** · 评论 7 · 👍 4 | [链接](https://github.com/anomalyco/opencode/issues/20458)

> **为什么重要：** TUI 退出后终端残留鼠标转义序列（如 `35;89;19M` 形式的乱码），破坏终端状态。虽与 #3199（会话内乱码）分离，但用户需手动 reset 终端才能恢复。

---

### 5. Qwen3.5-122b 模型报错 “System message must be at the beginning”
**#16560** · 评论 7 · 👍 2 | [链接](https://github.com/anomalyco/opencode/issues/16560)

> **为什么重要：** 涉及 NVIDIA NIM/API 上的 Qwen 模型兼容性问题。今天新出现的 #42909 也在报相同错误——**Qwen3 系列模型拒绝接收多个系统消息**，而 OpenCode 作为 agentic 客户端会发送多条系统提示。该问题已持续 5 个月未关闭。

---

### 6. Bug：流式错误后 UI 无限“thinking”，无错误提示且无法恢复
**#32366** · 评论 6 | [链接](https://github.com/anomalyco/opencode/issues/32366)

> **为什么重要：** 该 Issue 与 #38644（500 错误被静默丢弃）、#36370（Desktop 侧边流永不完成）构成同类问题族群，是当前社区反馈最集中的稳定性缺陷——一旦发生必须重启应用。

---

### 7. [2.0] v2 CLI：headless 命令加载 OpenTUI 并泄漏原生临时文件
**#37671** · 评论 5 · 👍 2 | [链接](https://github.com/anomalyco/opencode/issues/37671)

> **为什么重要：** `--version`、`--help`、`service status`、`api` 等不需要 TUI 的命令，每次执行都会在临时目录留下 13.1 MiB 的 `libopentui.so` 文件。该问题与 #42880 “ssd 杀手” 的根因疑似相同，是 v2 的重要性能/资源缺陷。

---

### 8. Bug：会话在空 LLM 响应时静默停止
**#41469** · 评论 4 | [链接](https://github.com/anomalyco/opencode/issues/41469)

> **为什么重要：** 当模型返回空补全（0 tokens，finish reason 为 unknown）时，OpenCode 将其视为正常回合结束并静默退出循环，无任何提示。对不稳定的模型/Provider 场景，用户难以判断是正常结束还是异常。

---

### 9. 不稳定的网络使 OpenCode 陷入卡死状态
**#40625** · 评论 4 · 👍 1 | [链接](https://github.com/anomalyco/opencode/issues/40625)

> **为什么重要：** 网络抖动（丢包）时 OpenCode 不会抛出错误，而是卡死在“Esc to interrupt”状态，用户自建的 watchdog 脚本也会因此失效。与 #32366 卡死问题同源，可能均与底层超时/重试机制缺失有关。

---

### 10. Bug：Zsh 补全不提示顶层 flags（--continue、--session 等）
**#42913** · 评论 4 | [链接](https://github.com/anomalyco/opencode/issues/42913)

> **为什么重要：** 新提交（8/16），shell 补全仅列出子命令，`--continue`、`--session`、`--fork` 等顶层标志完全无法补全，影响 CLI 日常效率。

---

## 重要 PR 进展（Top 10）

### 1. fix(app): 降低会话 spinner CPU 占用
**#42952** · 最新 | [链接](https://github.com/anomalyco/opencode/pull/42952)

> 将 25 个逐点 CSS 透明度动画替换为单个预渲染 APNG 时间线，保留 8 个原始姿势、`ease-out` 插值、`currentColor` 与 reduced-motion 行为。对长时间运行 TUI 的 CPU 占用是显著优化。

---

### 2. fix(app): 渲染 Code Mode 执行状态
**#42949** | [链接](https://github.com/anomalyco/opencode/pull/42949)

> 新增 Desktop 端 Code Mode 执行渲染器，展示子工具进度、输入摘要、失败调用状态与运行时错误，并补充元数据解析测试。v2 Desktop 与 CLI 功能对齐的重要补全。

---

### 3. refactor(app): 使用当前会话消息流替代旧转录
**#42766** | [链接](https://github.com/anomalyco/opencode/pull/42766)

> 移除 Desktop 端同时维护 V2 session 消息流与旧 `Message`/`Part` 转录的双轨制，改为单一消息源，降低状态同步风险。

---

### 4. fix(core): 表面内容过滤的拒绝类别与解释
**#37392** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37392)

> 修复 Anthropic `stop_reason: "refusal"` 被映射为固定硬编码消息的问题，改为暴露具体拒绝原因。关闭 #35736，对使用 Claude 模型的用户更友好。

---

### 5. fix(tui): 中断的 Shell 隐藏 “Background” 徽标
**#42049** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/42049)

> 仅在工具明确报告分离的运行状态时显示 Background 徽标，覆盖 detached、foreground、interrupted 与缺失元数据四种状态。

---

### 6. fix(core): 流式推送 shell 进度尾部
**#37374** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37374)

> Shell 进度以最近 25 行输出的快照形式推送，并在超出时前置截断通知（含完整输出路径）。对长输出命令的 UI 体验是重要改进。

---

### 7. fix(tui): 修正 truncateLeft 在 len=1 时的输出
**#37369** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37369)

> 修复 `str.slice(-0)` 返回空字符串的边界 bug，关闭 #37368。

---

### 8. fix: 保留 file API 文本内容，避免 trim() 改变语义
**#37385** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37385)

> 实例 file API 对解码文本调用 `trim()` 会删除首尾与空行空白，该 PR 移除这一行为，关闭 #37384。

---

### 9. fix: apply_patch 检查移动目标路径的权限
**#37386** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37386)

> 此前 apply_patch 移动文件时仅基于源路径请求编辑权限，但实际写入的是目标路径，存在校验漏洞。关闭 #37382。

---

### 10. fix(tui): 从命令面板隐藏模型循环绑定
**#37363** · 已关闭 | [链接](https://github.com/anomalyco/opencode/pull/37363)

> 模型循环快捷键不应出现在命令面板中，由 @thdxr (Dax) 通过 Slack 提出，已合入。

---

## 功能需求趋势

| 方向 | 代表 Issue / PR | 说明 |
|---|---|---|
| **会话管理增强** | #42940（收藏/固定会话）、#42863（有序会话评审导航） | 用户希望更高效地组织与回顾历史会话，窄屏设备上尤甚 |
| **权限流可配置化** | #40331（可配置自动审批快捷键） | 在 `permission.mode` 基础上，用户期望通过单一快捷键快速切换 |
| **Shell 生命周期语义** | #36348（前后台 Shell 重启语义） | v2 中 Server 重启后长驻进程的归属与跟踪需要明确规则 |
| **Provider 兼容性 & 超时控制** | #26602（本地 Provider 超时失效）、#16560/#42909（Qwen 多系统消息） | 本地/非 OpenAI Provider 的适配仍是高频痛点 |
| **计费与额度体系** | #33318（付费余额仍被限流）、#42938（Go 套餐余额未启用） | 付费用户的额度判定逻辑需更透明、可靠 |
| **CLI 可用性** | #42913（zsh 补全缺失顶层 flags） | shell 补全、headless 命令等 CLI 体验细节 |

---

## 开发者关注点

1. **“无限 thinking + 静默失败” 是最集中的稳定性痛点** — 至少 5 个相关 Issue（#32366、#38644、#36370、#41469、#40625），根因均指向流式错误后状态未正确恢复。社区期待官方对错误处理与状态机做系统性修复。
2. **资源泄漏正在损伤用户 SSD** — #37671 与 #42880 均指向原生 `.so` 文件在 `/tmp` 中高频生成，用户被迫采用 tmpfs / 定时清理等 “土办法” 自救，说明该问题已影响实际生产环境。
3. **本地模型友好的超时模型缺失** — #26602 中显式设置 `"timeout": false` 仍被强制 5 分钟超时，本地长上下文推理不被支持，对本地模型用户是明确的阻碍。
4. **付费额度判定逻辑需透明化** — #33318 与 #42938 两个独立付费问题，均出现“显示有余额但被限制”的情况，社区对计费系统的信任度正在受到影响。
5. **Qwen 系列模型兼容性连续报错** — #16560（3 月）与 #42909（8 月 16 日）为同一错误，社区需要官方协调 Qwen 端修复或提供 OpenCode 侧兼容方案。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-17

## 今日速览

Pi 社区昨日进入密集的修复与合并阶段：核心焦点集中在 `triggerTurn: false` 自定义消息在流式传输中破坏 tool_calls 顺序的严重 bug（#8166/#8210 确认、#8209 修复），以及 pi.dev 模型目录超时问题（#8198 报告、#8204 修复）。此外，模型目录相关议题（GLM-5.3 思维级别缺失、Qwen Token Plan 对齐、GLM-4.6V 视觉模型缺失）和 Token 统计准确性（Kimi 缓存计费、cache token 权重）成为社区讨论高密度区域。多个 PR 已完成合并，包括 xAI 默认模型升级至 Grok 4.6 和 MiniMax 图生图能力新增。

## 版本发布

过去 24 小时无新版本 Release。

## 社区热点 Issues

### 1. 流式传输中自定义消息破坏 tool_calls 顺序 — 确认并修复
- **#8166** [CLOSED]：`triggerTurn: false` 的自定义消息在工具批处理中注入，导致下一轮 DeepSeek 400 错误（tool 消息必须跟在 tool_calls 后）
- **#8210** [CLOSED]：Moonshot 上确认同样问题——`sendCustomMessage` 在流式时绕过队列保护直接 push 到活跃消息数组，造成永久性 400 楔死
- **社区反应**：两个 issue 均标注确认，修复 PR #8209 已合并。开发者 @alexkalinohooijunyi 提供了精确的根因定位。
- [查看 #8210](https://github.com/earendil-works/pi/issues/8210) | [查看 #8166](https://github.com/earendil-works/pi/issues/8166)

### 2. pi.dev 目录接口超时 — 多网络环境复现
- **#8198** [OPEN]：pi 0.84.2 的 `pi update --models` 一致超时，curl 直接请求 pi.dev 也无响应头/正文返回
- **社区反应**：标记为 bug，修复 PR #8204 已提交。这是 #8065 的复发（服务端 304/hang 问题）。
- [查看 #8198](https://github.com/earendil-works/pi/issues/8198)

### 3. Context 预算忽略 maxTokens 输出预留 — 78% 输入即被拒
- **#8061** [OPEN]：输入仅为模型窗口 78% 时请求被拒，自动压缩重试也失败。1M token 上下文的 Gemini 系列模型（OpenAI 兼容端点）受影响
- **社区反应**：获得 1 👍，开发者 @Nuctori 指出 "compact-and-retry recovery" 逻辑缺陷——重试仍按原预算计算。
- [查看 #8061](https://github.com/earendil-works/pi/issues/8061)

### 4. z-ai/glm-5.2 contextWindow 被远程目录覆盖为 262k（应为 1M）
- **#7870** [OPEN]：pi.dev 目录叠加层静默覆盖内置正确配置，导致 OpenRouter 上 glm-5.2 上下文窗口显示为 262144 而非 1,048,576
- **社区反应**：标记 in-progress，开发者 @tcf909 提供了 OpenRouter API 的实时数据对比。
- [查看 #7870](https://github.com/earendil-works/pi/issues/7870)

### 5. Prompt 编辑器大缓冲区性能线性退化
- **#8029** [OPEN, inprogress]：7000 行提示词缓冲区中，按一次方向键耗时 1650ms，随缓冲区大小线性增长
- **社区反应**：标记 in-progress，是 TUI 性能的关键痛点。
- [查看 #8029](https://github.com/earendil-works/pi/issues/8029)

### 6. Grok-mermaid 迁移至 lovely-mermaid
- **#8157** [OPEN]：grok-mermaid 是原版构建渲染的 1:1 移植，继承了大量边界问题和限制；lovely-mermaid 投入了更多精力，解析器更完善
- **社区反应**：开发者 @xl0 主动提出迁移，是渲染能力质量提升的重要方向。
- [查看 #8157](https://github.com/earendil-works/pi/issues/8157)

### 7. Windows 上输入行重绘异常 — 每个字符换行
- **#6300** [OPEN]：Windows 10 + cmd/Windows Terminal 下，每次击键输入行重绘且每个字符出现在新行
- **社区反应**：持续开放 6 周，涉及 Node.js v22，是 Windows 平台体验的关键 bug。
- [查看 #6300](https://github.com/earendil-works/pi/issues/6300)

### 8. GLM-5.3 缺少 thinkingLevelMap / supportsReasoningEffort
- **#8190** [CLOSED]：zai / zai-coding-cn 上选择思维级别无效，请求只带 `thinking: {type: "enabled"}` 而无 `reasoning_effort`
- **社区反应**：标注 untriaged 后迅速关闭，说明修复已合入。
- [查看 #8190](https://github.com/earendil-works/pi/issues/8190)

### 9. TUI 鼠标事件应支持组件级分发
- **#7683** [CLOSED]：请求添加可选 `Component.onMouse?(event)`，让组件在自身行范围内接收鼠标事件（行列坐标相对于组件 LayoutBox），在滚动条/选择处理之前分发
- **社区反应**：10 条评论，是 TUI 交互精细化的社区诉求，已关闭（预计合入）。
- [查看 #7683](https://github.com/earendil-works/pi/issues/7683)

### 10. 主题切换遗留过期颜色
- **#8212** [CLOSED]：0.84.2 中切换主题后，header、树标签、markdown 默认样式前缀保留旧主题颜色
- **社区反应**：快速定位并关闭，显示了 TUI 渲染层对主题响应的不彻底。
- [查看 #8212](https://github.com/earendil-works/pi/issues/8212)

## 重要 PR 进展

### 1. 修复流式传输中自定义消息破坏 tool_calls 顺序
- **#8209** [CLOSED]：`AgentSession.sendCustomMessage` 在流式时将非 turn 触发消息推迟到 turn 结束；修复 #8166
- **影响**：消除了 DeepSeek/Moonshot 的 400 永久楔死问题
- [查看 PR #8209](https://github.com/earendil-works/pi/pull/8209)

### 2. pi.dev 目录刷新增加超时与重试
- **#8204** [CLOSED]：为每次目录请求增加 per-attempt 超时，避免单个挂起 provider 拖垮整个刷新流程
- **影响**：修复 `pi update --models` 的间歇性超时问题
- [查看 PR #8204](https://github.com/earendil-works/pi/pull/8204)

### 3. getStats() token 统计修正 — 仅计费 token
- **#8218** [CLOSED]：`tokens.total` 现在仅计算可计费 token（input + output），排除 cacheRead/cacheWrite（按 1/120 计费导致总膨胀 ~120x）
- **影响**：压缩预算不再过早触发（如 15k 输入因缓存 token 被误判为 180 万），显著改善长会话体验
- [查看 PR #8218](https://github.com/earendil-works/pi/pull/8218)

### 4. xAI 模型默认切换至 Grok 4.6，路由改为 Responses API
- **#8124** [CLOSED]：默认使用 Responses API 替代 Completions，默认模型从 Grok 4.5 升级至 Grok 4.6，并发送 user agent
- [查看 PR #8124](https://github.com/earendil-works/pi/pull/8124)

### 5. Kimi 缓存 token 跟踪
- **#8119** [CLOSED]：将 Kimi 顶层 `usage.cached_tokens` 计入 cacheRead token，修复 #8075
- [查看 PR #8119](https://github.com/earendil-works/pi/pull/8119)

### 6. MiniMax 图生图（image-to-image）支持
- **#8193** [CLOSED]：新增 `minimax-images` API 模块，注册到运行时 images 注册表，补齐 MiniMax 参考图生成能力
- [查看 PR #8193](https://github.com/earendil-works/pi/pull/8193)

### 7. Kiro OAuth 设备登录支持
- **#8217** [CLOSED]：新增 Kiro 提供商的设备码登录与刷新，处理 authorization_pending、slow_down、超时及 expiresIn 异常
- [查看 PR #8217](https://github.com/earendil-works/pi/pull/8217)

### 8. OpenCode Go 目录路由修正
- **#8206** [CLOSED]：`qwen3.6-plus` 与 `minimax-m2.7` 被错误路由至 openai-completions，实际仅支持 `/v1/messages`（Anthropic 格式）
- [查看 PR #8206](https://github.com/earendil-works/pi/issues/8206)

### 9. Qwen Token Plan 目录对齐
- **#8194** [CLOSED]：使 `qwen-token-plan` 与 `qwen-token-plan-cn` 暴露相同的 8 模型文本目录（deepseek-v4-pro、glm-5.2、qwen3.7-max 等）
- [查看 PR #8194](https://github.com/earendil-works/pi/issues/8194)

### 10. 级联子代理深度无限制
- **#8195** [CLOSED]：`examples/extensions/subagent` 示例中子代理可无限嵌套（子 pi 重载扩展且未禁用扩展）；提议用环境变量跟踪深度并拒绝更深派生
- **影响**：示例扩展的健壮性改进
- [查看 PR #8195](https://github.com/earendil-works/pi/issues/8195)

## 功能需求趋势

1. **模型目录精确性**：GLM-5.3 思维级别、GLM-4.6V 视觉模型、Qwen Token Plan 目录对齐、OpenCode Go 路由修正——社区对内置目录的模型能力和配置准确性要求提高
2. **Token 统计与计费准确性**：Kimi 缓存 token（#8075）、cache token 权重修正（#8218）、远程目录 contextWindow 覆盖问题（#7870）——开发者对成本可见性和预算控制的需求
3. **TUI 交互精细度**：组件级鼠标事件（#7683）、主题切换完整渲染（#8212）、IME/听写实时布局（#8211）——终端 UI 体验持续优化方向
4. **扩展 API 灵活性**：`agent_end` 可否决（#8213）、RPC 暴露参数补全（#8214）——扩展机制向更深度工作流控制演进
5. **安全与信任**：pi-devin-auth 包报告为"恶意或不安全"（#8216）——社区对第三方包安全的关注度上升

## 开发者关注点

- **消息注入与流式竞态**：多起 issue 指向 `triggerTurn: false` 消息在流式中的竞态问题（#8166/#8210），已通过 #8209 修复，但暴露了流式架构的脆弱性
- **pi.dev 服务稳定性**：目录接口间歇性无响应（#8198），影响模型更新流程，社区期望服务端修复
- **Windows 平台体验**：输入行重绘问题（#6300）长期未解决，是 Windows 用户的核心痛点
- **性能退化**：大缓冲区方向键延迟（#8029）影响长提示词工作流，已被标记 in-progress
- **context 预算计算**：78% 输入即被拒（#8061）表明预算计算未考虑输出预留，修复期望强烈
- **新增模型适配成本**：多个 issue 指向新模型（GLM-5.2/5.3、qwen3.6、minimax-m2.7）在 pi 中的配置不完整——社区对快速适配新模型的需求持续增长

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-17

## 今日速览

多智能体（agent-team）可靠性问题集中爆发，`netbrah` 连续提交 6 个 P2 级 Bug（任务派发、消息传递、会话崩溃、图片 MIME 等），成为今日社区焦点。与此同时，维护者 `wenshao` 持续推进 `/review` 子系统的加固与重构——在发布 2 个预览/夜间版本之余，有 4 个审查相关 PR 在今日获得更新，其中针对"并发会话争抢同一 worktree"的锁机制 PR #9211 最受关注。

## 版本发布

今日共发布 2 个版本：

- **[v0.21.12-preview.5](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.12-preview.5)** — 预览版，完整变更日志见 [v0.21.12...v0.21.12-preview.5](https://github.com/QwenLM/qwen-code/compare/v0.21.12...v0.21.12-preview.5)
- **[v0.21.11-nightly.20260816.5677823abb](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.11-nightly.20260816.5677823abb)** — 夜间版，包含 1 个 autofix 功能提交（footprint gate + positional window censuses，PR [#9156](https://github.com/QwenLM/qwen-code/pull/9156)）

另有两条 DSW E2E 基准测试记录（r2/r3），均基于 v0.21.12 在 SWE-bench Verified (500) 和 Terminal-Bench 2.0 (89) 上全量回归通过。

## 社区热点 Issues

### 多智能体（Multi-Agent）可靠性 — 新增 5 个 P2 级 Bug

以下 5 个 Issue 均由 `netbrah` 在 8 月 16-17 日集中提交，涉及 agent-team 的消息传递、任务派发和会话稳定性，社区关注度高（均已有 3-5 条评论）：

1. **[#9276](https://github.com/QwenLM/qwen-code/issues/9276) — 团队成员无法向 leader 发送普通消息**：成员发送普通完成/状态消息被当作 shutdown 请求拒绝，报错 "Only the team leader can request shutdowns"。P2 核心 Bug。
2. **[#9282](https://github.com/QwenLM/qwen-code/issues/9282) — 手动分配的任务持久化但不派发**：leader 可将任务置为 `in_progress + owner: alice`，但空闲的 Alice 收不到任何任务提示。P2 核心 Bug。
3. **[#9281](https://github.com/QwenLM/qwen-code/issues/9281) — task_list 将空字符串过滤器视为激活过滤器**：可选 `owner`/`blockedBy` 字段序列化为空串时，即使团队中有匹配任务也返回 "No tasks found."。P2 工具 Bug。
4. **[#9283](https://github.com/QwenLM/qwen-code/issues/9283) — agent-team 提示与自动派发行为矛盾**：运行时会在队友空闲时自动转发最终答案给 leader，但提示文本要求显式 `send_message`，且承诺了不存在的摘要能力。P2 核心 Bug。
5. **[#9290](https://github.com/QwenLM/qwen-code/issues/9290) — 打开出错/未完成的团队成员标签页导致会话崩溃**：交互式会话直接退出。P2 UI Bug，与 PR #9292 关联。

**另有一条新提交的单例 Bug：**

6. **[#9291](https://github.com/QwenLM/qwen-code/issues/9291) — 不支持的图片 MIME 使 Responses 兼容会话中止**（`netbrah`，P2）：`.heic` 图片被接受并作为 `image/heic` data URI 转发给端点，校验阶段被拒并中止会话。已在更新中。

### 审查/CI 工具链

7. **[#9089](https://github.com/QwenLM/qwen-code/issues/9089) — autofix PAT 作业与不可信分支代码共享主机，需要 runner 级隔离**（`wenshao`，P1/安全）：审查中发现无法在 GitHub Actions step 内部关闭的 runner 隔离问题，已有 5 条讨论，是当前最高优先级安全项。

8. **[#9143](https://github.com/QwenLM/qwen-code/issues/9143) — Main CI E2E 测试失败**（`qwen-code-dev-bot`，P3）：主分支 CI 在报告任何测试结果前即失败，按提交跟踪，4 条评论讨论中。

9. **[#9278](https://github.com/QwenLM/qwen-code/issues/9278) — `/review` 发布时收敛建议设计与实测记录**（`wenshao`，P2/功能设计）：详细记录了"push → 评审 → agent 修复 → diff 变大 → 更多 finding"的失控回路问题及解决方案设计，有 3 条讨论。

### 其他值得关注

10. **[#5966](https://github.com/QwenLM/qwen-code/issues/5966) — 0.19.3 UI 不定期错误，中文输入法完全无效**（`aspnmy`，P2/需更多信息）：已存活 49 天，今日仍有更新，评论区累计 5 条。用户反馈"只能输入拼音，并且完全不报错"，是 UI 输入法的高频痛点。

## 重要 PR 进展

### 审查子系统加固（`wenshao` 主导）

1. **[#9211](https://github.com/QwenLM/qwen-code/pull/9211) — 为 PR 审查 worktree 添加租约锁** ⭐：解决同 PR 并发审查会话争抢固定路径 worktree 导致中途删除的问题（对应 Issue #9205）。审查会话的 worktree 现在同时作为锁使用，所有破坏性操作前先检查。**今日有更新**。
2. **[#9221](https://github.com/QwenLM/qwen-code/pull/9221) — verifier 探针改在私有 scratch worktree 中运行**：verifier 是审查流程中唯一会"写"的 agent（写探针、跑探针、应用翻转检查补丁）。此前这些操作落在所有 agent 共享的审查 worktree 中，现改为隔离环境。**今日有更新**。
3. **[#9272](https://github.com/QwenLM/qwen-code/pull/9272) — 命名认证关卡并将降级说明推迟到准入之后**（对应 #9259）：跟进 #9213 的遗留建议，涉及 reverse-audit 退役路径中的 3 项生产变更。**今日有更新**。
4. **[#9273](https://github.com/QwenLM/qwen-code/pull/9273) — capture-tui：渲染声明获得像素而非散文**：新增 `qwen review capture-tui` 子命令，在私有 tmux server 中驱动命令执行，捕获 ANSI 文本并可选渲染 PNG，让验证者用截图而非代码论证来证明渲染正确性。**今日有更新**。
5. **[#9263](https://github.com/QwenLM/qwen-code/pull/9263) — 审查 shell 脚本和 CI 脚本时对照实际执行的工作流**：新增第三条路径规则——要求先盘点哪些 CI 任务实际执行了被审查的脚本，再据此审查。**今日有更新**。
6. **[#9270](https://github.com/QwenLM/qwen-code/pull/9270) — 关闭 #9222 审查遗留的 4 个 findings**：包括 findings 命令拒绝解析器输入路径与输入/输出文件相同的情况等。**今日有更新**。

### 多智能体修复（社区贡献）

7. **[#9288](https://github.com/QwenLM/qwen-code/pull/9288) — 可靠派发 leader 分配的任务**（`netbrah`）：修复 #9282，确保 `in_progress` 任务恰好一次到达指定队友（无论其当前空闲还是稍后空闲），在任务变更边界内使过期的派发状态失效，并对空闲队友进行重试。**今日有更新**。

8. **[#9284](https://github.com/QwenLM/qwen-code/pull/9284) — 对齐 agent-team 提示与 TeamCreate 描述与实际派发行为**（`yiliang114`）：修复 #9283，仅覆盖提示准确性项目。

9. **[#9292](https://github.com/QwenLM/qwen-code/pull/9292) — 包含 agent-tab 渲染错误而非退出会话**（`yiliang114`）：修复 #9290 的包含部分。

### Web Shell 与 CI 基础设施

10. **[#9254](https://github.com/QwenLM/qwen-code/pull/9254) — Web Shell 启动失败时显示引导回退而非白屏**（`wenshao`）：添加零依赖启动看门狗，资源加载失败时立即渲染双语 fallback 界面（"Web Shell 加载失败 / failed to load"）+ 重新加载按钮。**今日有更新**。

> **另请注意**：[#9226](https://github.com/QwenLM/qwen-code/pull/9226)（Aone Code 读取路径，第二个审查平台 provider）和 [#9216](https://github.com/QwenLM/qwen-code/pull/9216)（发布说明双语摘要，已关闭）今日也有更新，但评论数较少。

## 功能需求趋势

从今日 Issues 和 PR 中可以提炼出以下社区关注方向：

- **多智能体协作可靠性（最热）**：今日新增 6 个相关 Issue（#9276/#9281/#9282/#9283/#9290/#9291），覆盖消息传递、任务派发、错误恢复等。社区对 agent-team 功能有强烈兴趣，但当前实现存在多处行为与文档不一致的问题，处于"快速迭代、密集报障"阶段。
- **审查流程自动化与可视化（维护者主导）**：`wenshao` 持续投入 `/review` 子系统的可靠性、安全性和可观测性，从并发锁、隔离环境到渲染证据捕获（capture-tui），方向是让 AI 审查流程更可信、可验证。
- **认证方式扩展**：[#9275](https://github.com/QwenLM/qwen-code/issues/9275) 请求添加 GitHub Copilot 身份认证，让 Copilot 订阅用户可通过 `/auth` 使用其模型。已有 2 条讨论。
- **生态系统集成**：[#9294](https://github.com/QwenLM/qwen-code/issues/9294) 请求将 ClawMetry（开源本地可观测性仪表盘，`pip install clawmetry`，自带 Qwen Code 适配器）加入 README 的 Ecosystem 章节。

## 开发者关注点

- **多智能体行为与文档不一致**：多个 Issue（#9276、#9283、#9281）集中反映了 agent-team 的文档/提示文本与实际运行时行为脱节的问题——用户按文档操作却得到错误结果，这是当前体验的最大痛点。
- **交互式会话脆弱**：单个渲染错误（#9290）或不受支持的图片格式（#9291）就能让整个会话中止退出，"小问题引发大崩溃"是用户高频反馈。
- **审查流程的生产力瓶颈**：`/review` 子系统经历了大量迭代，但用户（主要是维护者自己）仍然遇到并发争抢、schema 不匹配、静默失败等问题——说明 AI 驱动审查流程在真实复杂 PR 上的稳定性仍有提升空间。
- **Web Shell / TUI 稳定性**："白屏"（#9253）、"tmux 下无法使用"（#8962）等问题持续存在，终端 UI 在远程/嵌入场景下的体验是高频反馈。

---
*日报生成时间：2026-08-17 · 数据来源：[QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-08-17** | 数据来源：[Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)（原 DeepSeek-TUI）

---

## 今日速览

v0.9.8 正式发布并确定 Codewhale 品牌，代码库活跃度极高（单日 20+ PR/Issue 更新）。核心方向集中在三块：**修复 v0.9.x 系列回归 bug**（宽屏布局、sudo 权限、无故崩溃）、**重构子代理与只读隔离机制**（#5123、#5426）、以及 **为 Codewhale 品牌重塑铺路的周边工作**（多语言 i18n、README 翻译、Web UI 重建）。此外，多个 PR 正在修复 CI 跨平台红测问题。

---

## 版本发布

### v0.9.8 发布说明

Codewhale 正式成为 Shannon Labs 的公开产品品牌。`codewhale` 命令、npm 包及发布资产名称统一为小写技术标识。旧版 `deepseek-tui` npm 包已弃用，不再获得后续更新。从 v0.8.x 旧版 `deepseek` / `d` 命令迁移的用户需注意命令名称变更。

---

## 社区热点 Issues

### 1. [#5123 Agent spawn 表面配置项过多 — 构建器被标记为只读并自我 BLOCKED](https://github.com/Hmbown/CodeWhale/issues/5123) 🔥 高热度
**标签：** bug / subagents / tools / reliability | 评论 6 | 更新 08-16

部署代理仍存在核心失败模式：被标记为 `builder` / `gates-shell-writer` 的会话，实际工具契约却是**只读**的——所需能力（写 gates shell）与实际权限不匹配，导致代理自我阻塞。这是 agent 可靠性方向的关键 bug，体现了工具权限声明与实际执行不一致的系统性问题。

### 2. [#2693 v0.9.4 HarnessPosture：模型特定上下文和子代理策略](https://github.com/Hmbown/CodeWhale/issues/2693) 
**标签：** enhancement / context / whaleflow | 评论 6 | 更新 08-16

让 CodeWhale 的 harness 策略按 provider/model 路由显式化，而非假设所有模型需要相同的前置系统上下文。源于 v0.8.53 测试发现 DeepSeek V4 和小米 MiMo v2.5 可能受益于 cache-heavy/prefix-stable 的起始提示。这是模型适配层的重要架构演进。

### 3. [#5056 测试可靠性：flaky 后台验证器测试、/workspace 敏感 fixtures、12 个未处理 #[ignore] 测试](https://github.com/Hmbown/CodeWhale/issues/5056) 
**标签：** bug / reliability | 评论 5 | 更新 08-17

`run_verifiers_background_advertises_detached_start` 和 `run_verifiers_background_starts_shell_jobs_and_returns_task_ids` 仍会在全量并行测试下 flake。/workspace 敏感的子代理测试会写入 fixture 路径。CI 稳定性是当前开发流程的主要阻塞点。

### 4. [#5424 v0.9.7：Codewhale TUI 无故崩溃](https://github.com/Hmbown/CodeWhale/issues/5424) 📌 新增
**标签：** bug | 评论 5 | 创建 08-16

用户反馈在 `codewhale --continue` 后正常加载，但提示任意消息后约一分钟即自行退出。属于阻断性稳定性问题，触发条件待复现，但社区对 v0.9.x 系列的稳定性关注度明显上升。

### 5. [#5322 回归：宽终端下输出区域不填充（v0.8.65 正常）](https://github.com/Hmbown/CodeWhale/issues/5322) ✅ 已关闭
**标签：** bug | 评论 5 | 更新 08-16

v0.8 中 transcript/output 区域会扩展至终端全宽，v0.9 起被限制为最大宽度，导致宽屏显示器文本拥挤、右侧大量留白。已关闭但代表了 v0.9 系列"宽屏体验"的回归问题——同一批次相关的还有 #5436（散文 105 列换行）。

### 6. [#1917 提案：为所有动作类型建立通用的 PreToolUse/PostToolUse 钩子层（Cancel/Pause/Resume）](https://github.com/Hmbown/CodeWhale/issues/1917) 
**标签：** enhancement / tui / tools | 评论 5 | 更新 08-16

社区成员 aboimpinto 提出基于钩子的生命周期层，支持任何调用工具的动作的取消（带回滚）、暂停和恢复。来自 #1886-#1900 系列问题分析后发现的统一架构模式。体现了社区对工具调用生命周期管理的深度需求。

### 7. [#5434 integrations dsh：默认 DeepSeek 路由（deepseek-v4-flash）被拒 — Responses 方言无法承载](https://github.com/Hmbown/CodeWhale/issues/5434) ✅ 已关闭（含修复 PR）
**标签：** bug / integrations | 评论 0 | 更新 08-17

实测发现 `@deepseek-ai/dsh@0.1.0-rc.6` 的默认 DeepSeek 路由被拒。`status`/`plan`/`connect`/`install-bundle`/`launch --dry-run` 均正常，但默认路由携带 `endpoint_key: "responses"` 时无法通过仅支持 openai-completions 方言的适配器。集成层面方言兼容性问题。

### 8. [#5436 TUI：散文在 ~105 列换行而工具单元格全宽运行 — 宽终端上 transcript 左偏](https://github.com/Hmbown/CodeWhale/issues/5436) ✅ 已关闭（含修复 PR）
**标签：** tui / bug | 评论 0 | 更新 08-17

宽终端上用户消息/助手回答/推理块约 103 列停止，右侧大片死区；工具输出和状态单元格则全宽运行。transcript 整体左偏。与 #5322 同属宽终端布局问题群。

### 9. [#5403 main 分支在双平台全红：macOS 插件 e2e 验收、Windows NSIS 配置](https://github.com/Hmbown/CodeWhale/issues/5403) ⚠️ 高风险
**标签：** CI / bug | 评论 2 | 更新 08-16

#5395 修复 CI 取消问题后，已完成运行的 4 个 main 分支构建在 macOS 和 Windows 上全红。CI 全平台稳定性问题正成为当前开发流程的最大瓶颈，与 #5056、#5408 互相关联。

### 10. [#5413 回归：sudo 无法使用](https://github.com/Hmbown/CodeWhale/issues/5413) ✅ 已关闭
**标签：** bug | 评论 2 | 创建 08-16

用户在 wheel 组、v0.8.65 可使用 sudo，v0.9.7 无法使用。Full Access + 全磁盘权限下 `sudo -n true` 失败。作为对比最直接的 v0.8→v0.9 权限回归案例，验证了 #5123 所揭示的权限模型重构带来的破坏性影响。

---

## 重要 PR 进展

### 1. [#5445 fix(integrations)：通过 pi-ai openai-responses 承载 Responses 方言 DSH 路由](https://github.com/Hmbown/CodeWhale/pull/5445) ✅ 已合并
关闭 #5434。使 `codewhale integrations dsh plan` 能够处理默认 DeepSeek 路由（`endpoint_key: "responses"`）。修复集成层方言不匹配问题。

### 2. [#5446 fix(tui)：散文填满内容全宽 + 添加 transcript.prose_measure 上限](https://github.com/Hmbown/CodeWhale/pull/5446) ✅ 已合并
关闭 #5436。修复 `PROSE_MAX_MEASURE = 105` 导致的宽终端散文右侧死区问题，新增可配置的 `transcript.prose_measure` 上限。

### 3. [#5456 feat(sandbox)：bwrap 容器基础组件 + 可配置额外根目录](https://github.com/Hmbown/CodeWhale/pull/5456) 🆕 新增
关闭 #5410。Linux bwrap 沙箱默认为私有挂载 `/dev`、`/proc`、`/tmpfs /tmp` 容器基础组件（修复只读根绑定下 `/dev/null` 的 EROFS 问题），并新增可配置的额外绑定根：`bwrap_ro_roots` 等。

### 4. [#5457 test(pty)：修复 agent_focus auto-review 收据测试的 flake](https://github.com/Hmbown/CodeWhale/pull/5457) 🆕 新增
macOS CI 中 `agent_focus_pty::auto_review_gates_a_workers_call_and_the_receipt_shows_in_focus` 的 flake 修复。持续投入 CI 稳定性。

### 5. [#5438 fix(fleet)：scout 姿态门必须遵循只读 shell（#5426）](https://github.com/Hmbown/CodeWhale/pull/5438) 🔥 核心修复
关闭 #5426 的机制部分。首次真实 dogfood 测试中发现，新构建的只读 shell 拒绝 scout **全部三个**权威检查命令（`git log --oneline` 等）。直接修复子代理权限模型的核心矛盾。

### 6. [#5450 fix(tui)：无法验证实时定价时恢复会话成本](https://github.com/Hmbown/CodeWhale/pull/5450) 🆕 新增
关闭 #5241。替代 #5402（同两提交、当前 main 上的 cherry-pick）。会话成本不再永久停留在 `unverified_live_pricing`——包括 API 返回 503 `control_plane_not_attached` 的情况。

### 7. [#5454 feat(web/i18n)：添加 fr/de/ca/hi/tr/it/pl 字典（+ar 带 RTL 支持）](https://github.com/Hmbown/CodeWhale/pull/5454) 🆕 新增
codewhale.net 达到 v0.9.2 TUI 语言包同等水平，新增 fr、de、ca、hi（TUI 同款）及 tr、it、pl、ar（含 RTL 管道）。产品国际化战略的重要组成部分。

### 8. [#5449 docs(design)：Claude Code 对等参考文档](https://github.com/Hmbown/CodeWhale/pull/5449) ✅ 已合并
新增 `docs/design/CLAUDE_CODE_PARITY.md`，详述 Claude Code 的 Agent 工具、Workflow 工具（JS 脚本 API、journal 回放、schema 强制返回）、`/loop`、plugins/skills/agents/hooks 布局及单一 Bash 工具的实际工作机制。

### 9. [#5401 fix：CodeQL 高危问题（#107、#88-#106）并准备 GHSA-8hp3 / GHSA-3mgh](https://github.com/Hmbown/CodeWhale/pull/5401) 🔒 安全相关
仅包含 CodeQL + GHSA 切片，不打 v0.9.8 标签、不发布 crates/npm/Homebrew。修复 `scripts/catalog_models_dev.py` 的明文日志问题（#107 高危），并准备两个 GHSA 安全公告。

### 10. [#5455 feat(tui)：Signal Cut 鲸鱼 — 空状态英雄艺术 + Whale Teams 角色映射](https://github.com/Hmbown/CodeWhale/pull/5455) 🎨 品牌向
从 Whale Teams / **Signal Cut** 名册重绘空状态鲸鱼。旧版被描述为"带形状飘过的条形码"而非动物；新版修复了鳍与身体分离、比例失调等问题。品牌一致性的细节打磨。

---

## 功能需求趋势

| 方向 | 相关 Issues/PRs | 热度 |
|------|----------------|------|
| **子代理权限模型重构** | #5123、#5426、#5438、#4662 | 🔥🔥🔥 |
| **CI/测试可靠性** | #5056、#5403、#5408、#5457 | 🔥🔥🔥 |
| **宽终端/TUI 布局回归** | #5322、#5436、#5446 | 🔥🔥 |
| **模型路由与方言适配** | #5434、#5445、#4683、#5055 | 🔥🔥 |
| **多语言国际化（i18n）** | #5454、#5452 | 🔥🔥 |
| **沙箱灵活性与可配置性** | #5410、#5456 | 🔥 |
| **钩子化工具生命周期管理** | #1917 | 🔥 |
| **模型特定上下文策略** | #2693、#5263 | 🔥 |
| **架构去硬编码** | #4173（81 模型/31 provider/52 工具）| 🔥 |
| **MCP 能力元数据** | #4170 | 🔥 |

---

## 开发者关注点

### 高频痛点

1. **v0.9.x 权限模型破坏性变更**：sudo 不可用（#5413）、只读标签与实际能力不匹配（#5123）、scout 检查命令被拒绝（#5426）——升级 v0.8→v0.9 的开发者需重新审视权限配置。

2. **宽终端支持倒退**：输出区域不填满（#5322）、散文 105 列截断（#5436）——在两个 issue 均已关闭并有对应修复的情况下，社区对 TUI 在宽屏/超宽屏下的体验仍保持高关注。

3. **CI 全平台红灯**：macOS 插件 e2e 验收、Windows NSIS 配置持续失败（#5403），加之前述 flaky 测试（#5056），v0.9.x 系列发布流程的自动化验证尚不稳定。

4. **集成层方言兼容**：DSH 默认路由因 Responses 方言无法承载而拒绝（#5434）——不同服务商对同一模型协议的实现差异成为集成开发的主要摩擦点。

5. **模型成本/会话信息不透明**：实时定价无法验证时，会话成本停留在 `unverified_live_pricing`（#5241/#5450）。

### 社区活跃特征

- 核心维护者 Hmbown 在 24 小时内提交了 10+ PR/Issue，包括两个新功能 PR（#5456 沙箱、#5454 i18n），项目处于非常活跃的迭代期。
- 社区成员（M-Maciej、Hixac、aboimpinto、redstar 等）活跃度高，贡献了高质量 bug 复现（截图、日志、步骤）。
- 品牌从 DeepSeek-TUI 全面过渡到 Codewhale，npm 包弃用、多语言 README、Claude Code 对等参考文档等基础设施同步推进，表明项目正处于**产品化与生态建设的关键阶段**。

---

*本日报数据截至 2026-08-17，基于 GitHub 公开数据自动生成。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*