# AI CLI 工具社区动态日报 2026-08-14

> 生成时间: 2026-08-14 00:54 UTC | 覆盖工具: 9 个

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

**报告日期：2026-08-14**


## 一、生态全景

当前 AI CLI 工具赛道已从"单点功能竞争"进入"平台化生态竞争"阶段。头部工具（Claude Code、OpenAI Codex、Gemini CLI）保持高频迭代节奏（日更或隔日更），同时社区反馈重心正从"基础可用性"转向"长会话稳定性、成本可见性、安全边界、多智能体编排"等深水区。值得注意的分化信号：Qwen Code 通过多智能体 fleet 架构快速追赶，OpenCode 因 V2 重构引发社区反弹，而 Pi 则以强大的终端体验细节在小众开发者群体中建立口碑——不同工具间的差异化定位已经相当清晰。


## 二、各工具活跃度对比

| 工具 | 版本发布 | 热点 Issues | 重要 PRs | 社区热度信号 |
|------|---------|------------|---------|-------------|
| Claude Code | v2.1.232, v2.1.231 | 10 个（Top issue 832 评论） | 2 个 | 评论密度最高，Max 限额争议持续 5 个月 |
| OpenAI Codex | 3 个 alpha 预发布 | 10 个 | 10 个（全部已关闭） | 高频 alpha 迭代，架构演进迅速 |
| Gemini CLI | v0.56.0-nightly | 10 个 | 10 个 | 安全 PR 占比高，eval 基建为重 |
| GitHub Copilot CLI | v1.0.80-0 | 10 个 | 1 个 | 功能需求集中（每代理模型控制） |
| Kimi Code | 无 | 3 个 | 无 | 社区规模较小，记忆系统呼声最高 |
| OpenCode | v1.18.18 | 10 个 | 10 个 | V2 迁移引发争议，安全/兼容问题集中爆发 |
| Pi | 无 | 10 个 | 10 个（6 个已关闭） | 终端细节打磨获好评，TUI 体验领先 |
| Qwen Code | v0.21.11, v0.21.12-preview.1 | 10 个 | 10+ 个 | fl eet 多智能体方向密集推进 |
| DeepSeek TUI | v0.9.7 | 10 个 | 10 个 | 品牌化更名（CodeWhale），引入双层 Auto-Review |


## 三、共同关注的功能方向

### 1. 子代理/多智能体稳定性和可控性（热度最高）
- **Gemini CLI**：子代理误报成功（#22323）、通用代理无限挂起（#21409）
- **Claude Code**：Opus 5 静默覆盖用户代理委托策略（#80988）
- **DeepSeek TUI**：子 Agent 超时卡死（#1425）、子进程事件串流（#5339）
- **Qwen Code**：fleet 多智能体架构为当前核心方向
- **Copilot CLI**：子代理推理强度不匹配导致执行失败（#4345, #4473）

### 2. 长会话稳定性和上下文管理
- **Pi**：自动压缩失效致上下文溢出至 373k tokens（#6879）
- **Claude Code**：并行工具调用后提示缓存重建浪费 74%（#63930）
- **OpenCode**：V2 压缩请求超限导致会话卡死（#42448）
- **Codex**：会话压缩后线程读取负载过大被截断（#38466）

### 3. 本地/第三方模型与外部供应商兼容
- **Codex**：Multi-Agent V2 向 Ollama 发送 OpenAI 专有消息类型（#33551）；MCP TLS 回退（#38436）
- **Copilot CLI**：远程 MCP OAuth 失败（#4480）、并发令牌刷新竞态（#4472）
- **Qwen Code**：Vertex AI 上 Gemini 2.5 不可用（#9019）、keyless 认证推断缺失（#9025）
- **Pi**：Gemini 端点拒绝新 schema 回退（#8086）、Codex `end_turn` 语义（#7689）
- **DeepSeek TUI**：DS4 本地推理路由成为一等公民（#5365）

### 4. 成本可见性与配额透明度
- **Claude Code**：Max 会话限额异常消耗，832 条评论（#38335）
- **Claude Code**：缓存重建导致 Opus 4.8 成本上升（#63930）
- **OpenCode**：Zen 免费额度误报 429（#42029, #42074, #42449）

### 5. Windows 平台体验
- **Codex**：扩展资源加载失败（#37458）、沙箱权限（#35871）
- **Qwen Code**：Ctrl+V 粘贴回归（#9061）、安装器 SHA-256 校验失败（#7118）
- **Pi**：配置解析误导（#7829）、Unix socket 绑定失败（#8047）
- **DeepSeek TUI**：SSH 阻断、中文输入法、图片渲染混乱

### 6. 会话记忆/持久化
- **Kimi Code**：#1283 记忆系统为长期头号需求（38 评论）
- **Pi**：Auto Memory 低信号无限重试（#26522）、脱敏不足（#26525）
- **OpenCode**：agent_memory 表 + 云端备份插件（#42425）

### 7. 安全与供应链
- **Gemini CLI**：fork 代码 RCE 修复（#28740）、simple-git CVE-2026-28292（#28778）、A2A 鉴权漏洞（#28699）
- **OpenCode**：curl\|bash 无校验（#42434）、webfetch SSRF（#42435）
- **Claude Code**：CI 供应链加固（#60280）


## 四、差异化定位分析

| 工具 | 定位 | 技术路线 | 目标用户 | 核心优势 | 主要短板 |
|------|------|---------|---------|---------|---------|
| **Claude Code** | 全功能一体化 Agent 平台 | 闭源商业 + 桌面端 + CLI | 企业/专业开发者 | 生态最成熟、功能最全、社区规模最大 | 计费争议、GPU 崩溃等稳定性问题、系统提示隐藏指令 |
| **OpenAI Codex** | 多模式交互的编程助手 | 闭源商业 + 桌面端 + TUI | 全栈开发者 | Rust 核心性能好、多模态（语音）、架构演进快 | Windows 短板明显、MCP 生态不成熟 |
| **Gemini CLI** | 安全优先的通用 Agent | 开源 (Apache-2.0) + Node.js | 开源社区/安全意识强的开发者 | 供应链安全投入大、eval 基建系统化、多模型支持 | 子代理稳定性问题（挂起/误报） |
| **Copilot CLI** | GitHub 生态深度集成 | 商业 + Node.js | GitHub 重度用户/企业 | 与 GitHub 策略/生态无缝衔接 | 模型控制粒度不足、MCP OAuth 问题 |
| **Qwen Code** | 多智能体编排的急先锋 | 开源 + TypeScript | 希望自定义 Agent 工作流的高级用户 | fleet 架构领先、Agent Plugins v1 | SWE-bench 验证失败被隔离、发布质量存疑 |
| **Pi** | 终端体验极致打磨 | 开源 (Apache-2.0) + Go | 终端党/追求高效交互的开发者 | TUI 细节最佳、性能优化深入 | 社区规模较小、企业与生态支持有限 |
| **OpenCode** | V2 重构期的创新者 | 开源 + TypeScript | 尝鲜者/开源社区 | 界面创新（Tab 滚动/工作区）、插件生态 | V1/V2 兼容性破坏、安全基线不足 |
| **DeepSeek TUI** | 品牌化转型中的实用工具 | 开源 + TypeScript | 中文/低成本用户 | 双层 Auto-Review 创新、本地模型配置 | 品牌更名带来迁移摩擦、Windows 问题集中 |
| **Kimi Code** | 轻量/待完善的新进入者 | 开源 | 学生/个人开发者 | 需求明确（记忆系统）受关注 | 版本迭代缓、Bug 修复周期长 |


## 五、社区热度与成熟度

### 成熟稳定期（社区规模大、功能丰富但争议多）
- **Claude Code**：评论密度最高，单个 issue 达 832 条。其优势在于功能完备，但社区情绪波动明显——Max 限额争议和回归问题已积累大量用户不满，呈现"爱之深责之切"的态势。
- **OpenAI Codex**：alpha 版本高频迭代，架构演进迅速，但 Windows 体验是明显短板，MCP 生态稳定性仍需时间打磨。

### 快速追赶期（迭代速度快、社区认可度上升）
- **Qwen Code**：多智能体 fleet 方向投入密集，3 天内完成 stage 1A→3 规划，社区认可度高。但 SWE-bench 验证失败暗示发布质量管理需加强。
- **Gemini CLI**：安全投入（供应链、鉴权）在行业中领先，eval 基建系统化值得关注。但子代理稳定性问题拖累日常体验。

### 调整转型期（面临迁移摩擦或架构重构挑战）
- **OpenCode**：V2 重构引发 V1 用户反弹（数据库破坏、UI 布局争议），社区情绪较为波动。
- **DeepSeek TUI**：品牌更名带来迁移摩擦，但双层 Auto-Review 等创新值得关注。

### 特色生存期（以差异化体验争取用户）
- **Pi**：TUI 体验与终端细节打磨获得了社区的良好口碑（SIGINT 恢复、Escape 取消选择等），但在整体生态和商业支持方面仍处于相对小众地位。
- **Kimi Code**：社区规模较小，记忆系统呼声高但迭代速度偏慢。
- **Copilot CLI**：得益于 GitHub 生态，企业用户基本盘稳固，但社区讨论度相对平稳。


## 六、值得关注的趋势信号

### 1. 多智能体编排正从"实验"走向"核心能力"
Qwen Code 的 fleet 架构、Claude Code 的 subagent forking 默认开启、Codex 的 Multi-Agent V2——头部工具均在重仓多智能体。但子代理稳定性问题的集中爆发（误报成功、无限挂起、事件串流）表明工程化成熟度仍是瓶颈。**开发者应关注工具在子代理生命周期管理、事件隔离、结果真实性验证方面的能力**。

### 2. "模型行为可控性"成为社区新焦点
Claude Code 的系统提示隐藏指令（#80988）、Gemini CLI 对自定义 skills 使用不足（#21968）都指向同一趋势——用户希望工具能约束"模型不做什么"，而非仅控制"做什么"。**可配置的安全边界和透明的行为策略将成为选型重要考量**。

### 3. 成本透明度已从"加分项"变为"必选项"
Max 限额争议、缓存重建浪费、免费额度误报——在模型 API 成本没有下降的情况下，开发者对"钱花在哪"极其敏感。**工具若能提供细粒度的成本归因和缓存命中可视化，将形成显著差异化优势**。

### 4. 供应链安全从"最佳实践"升级为"基本要求"
Gemini CLI 的 fork RCE 修复、OpenCode 的 curl|bash 暴露、Claude Code 的 CI 加固——开源工具在 CI/CD 自动化和升级链路上的安全缺陷正被社区高频审视。**开发者应优先选择对供应链安全有明确投入的工具**。

### 5. 本地模型/自托管需求持续上升
Codex 的 Ollama 兼容性问题、DeepSeek TUI 的 DS4 本地路由、Pi 的 Bedrock 支持——社区对外部供应商和本地推理的接入需求从未减弱。**支持 OpenAI 兼容协议、提供灵活的 provider 配置将扩大工具覆盖人群**。

### 6. 记忆系统是下一个必争之地
Kimi Code 把记忆系统列为头号需求，OpenCode 已提交 agent_memory 插件，Pi 的 Auto Memory 问题也在持续讨论。"跨会话记住项目模式"一旦成熟，将从根本上改变用户与 CLI 的工作方式。不过，记忆的隐私脱敏和用户控制机制（如 Gemini CLI #26525）将是先决条件。

### 7. 企业级管控需求加速浮现
Copilot CLI 的组织策略混淆（#4481）、Codex 的 GitHub 审查配额管理（#38405）、Claude Code 的多账号管理（#18435）——随着 AI CLI 进入企业工作流，**策略统一管理、配额可见性、审计追踪**等企业级需求正成为不可忽视的选型维度。


**总结**：AI CLI 工具正处于从"开发者玩具"向"核心开发基础设施"演变的关键时期。当前阶段，**稳定性、成本透明、安全边界**是社区最核心的诉求；**多智能体编排、记忆系统、企业管控**是下一个竞争高地。对于技术决策者，建议优先评估工具在长会话可靠性、权限可控性和成本可观测性上的表现；对于开发者个人，Windows 支持质量和社区活跃度可能更影响日常使用体验。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截至 2026-08-14）

> **说明**：所有 PR 与 Issue 均为 **OPEN** 状态，无 merged/draft 区分。PR 的"评论数"字段未被 GitHub API 正确映射（均显示 undefined），以下热度以 Issue 讨论关联、更新时间与修复范围综合判断。

---

## 1. 热门 Skills 排行（按社区关注度与讨论密度）

| 排名 | Skill / PR | 功能定位 | 社区讨论热点 | 当前状态 |
|---|---|---|---|---|
| 1 | **skill-creator 修复**（[#1298](https://github.com/anthropics/skills/pull/1298)、[#1099](https://github.com/anthropics/skills/pull/1099)、[#1050](https://github.com/anthropics/skills/pull/1050)） | 修复 skill 创建器的评估循环：`run_eval.py` 在所有查询下报 0% recall，导致描述优化循环在噪声上优化；另有 Windows 下 subprocess 管道读取崩溃与编码问题 | **核心痛点**：skill 描述的质量评估信号完全失真，10+ 独立复现（[#556](https://github.com/anthropics/skills/issues/556)、[#1169](https://github.com/anthropics/skills/issues/1169)）。Windows 兼容性是第二大痛点。三个 PR 从不同角度修复同一问题，尚未合入 | OPEN |
| 2 | **skill-security-analyzer & skill-quality-analyzer**（[#83](https://github.com/anthropics/skills/pull/83)） | 两个元技能：质量分析器（五维评估：结构/文档/示例/资源等）+ 安全分析器，用作 marketplace 中的"技能体检工具" | 关联 [#492 安全信任边界问题](https://github.com/anthropics/skills/issues/492)（社区技能混入 anthropic 命名空间）——质量与安全分析正是社区的迫切需求；PR 从 2025-11 至今仍 open，讨论跨度大 | OPEN |
| 3 | **testing-patterns**（[#723](https://github.com/anthropics/skills/pull/723)） | 全栈测试技能：Testing Trophy 模型、单元测试 AAA 模式、React Testing Library、边界用例设计 | 覆盖面广（philosophy → 具体框架），是社区对"可执行的测试方法论"需求的直接回应；3 月创建，4 月最后更新，讨论集中在测试覆盖范围 | OPEN |
| 4 | **plan-file-hygiene**（[#1479](https://github.com/anthropics/skills/pull/1479)） | 解决规划产物（planning artifacts）无生命周期的积累问题，提供文件卫生管理 | 由 Issue [#1417](https://github.com/anthropics/skills/issues/1417) 驱动，社区多人（@halilxibrahim、@xg-gh-25）参与问题定义；7 月底创建，8 月初仍在活跃讨论，属于"长会话代理"痛点 | OPEN |
| 5 | **claude-api 技能瘦身**（[#1487](https://github.com/anthropics/skills/issues/1487)） | 内置于 Claude Code 的 `claude-api` 技能每次调用注入 ~156k tokens，单次工具调用即耗尽上下文窗口 | 虽是 Issue 而非 PR，但直接指向官方内置技能的设计缺陷（上下文预算失控）；4 条评论但问题严重性高 | OPEN |
| 6 | **document-typography**（[#514](https://github.com/anthropics/skills/pull/514)） | 排版质量控制：孤儿词换行、孤行标题、编号错位 | 指出所有 AI 生成文档的通病（"每个 Claude 生成的文档都会受影响"）；3 月创建后讨论较少，但问题通用性强 | OPEN |
| 7 | **ServiceNow 平台技能**（[#568](https://github.com/anthropics/skills/pull/568)） | 覆盖 ITSM/ITOM/ITAM/SAM/FSM/HRSD/CSDM/IntegrationHub 的 ServiceNow 全平台助手 | 企业级场景的广度尝试；8 月 12 日仍有更新，是跨度最长的活跃 PR（3 月至 8 月 5 个月+），讨论涉及范围控制与维护成本 | OPEN |

---

## 2. 社区需求趋势（从 Issues 提炼）

1. **质量评估与安全审计**（最高优先级）
   - [#556](https://github.com/anthropics/skills/issues/556)、[#1169](https://github.com/anthropics/skills/issues/1169)：skill 描述评估信号失真（recall=0%），直接导致优化工具不可用——社区急需可靠的技能质量闭环。
   - [#492](https://github.com/anthropics/skills/issues/492)：社区技能混入 `anthropic/` 命名空间的信任边界漏洞（43 条评论，👍 2）——用户希望**分级信任机制**与安全审查流程。

2. **组织级技能共享**
   - [#228](https://github.com/anthropics/skills/issues/228)（👍 8）：目前只能手动下载 .skill 文件通过 Slack/Teams 分发，社区强烈呼吁**组织内技能库/分享链接**，减少团队协作摩擦。

3. **上下文管理与长会话优化**
   - [#1487](https://github.com/anthropics/skills/issues/1487)（claude-api 156k token 注入）、[#1329](https://github.com/anthropics/skills/issues/1329)（compact-memory——用符号标记压缩 agent 状态）——长会话代理的**上下文预算控制**是新兴且高频的诉求。

4. **去重与安装体验**
   - [#189](https://github.com/anthropics/skills/issues/189)（👍 9）：`document-skills` 与 `example-skills` 安装后内容重复，浪费 context window——**插件依赖/去重机制**亟待完善。

5. **平台适配**
   - [#29](https://github.com/anthropics/skills/issues/29)、[#1175](https://github.com/anthropics/skills/issues/1175)：AWS Bedrock 兼容、SharePoint Online 安全处理——企业用户关注**自有环境下的技能可用性**。

---

## 3. 高潜力待合并 Skills（评论活跃、尚未合入）

| Skill | PR | 潜力判断 |
|---|---|---|
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 全栈测试方法论需求明确，结构完整，若无审查阻塞应可合入 |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | 讨论热度高、多人参与定义，且恰好命中长会话代理痛点，8 月内有望更新 |
| **ServiceNow 平台技能** | [#568](https://github.com/anthropics/skills/pull/568) | 8 月 12 日仍活跃，企业级覆盖是差异化卖点；风险在技能体积与维护 |
| **self-audit（四维推理质量门）** | [#1367](https://github.com/anthropics/skills/pull/1367) | 机械验证 + 推理质量审计的新范式，6 月底提交后 7 月仍有更新；对应 [#1385 提案](https://github.com/anthropics/skills/issues/1385)，社区关注度上升中 |
| **skill-creator Windows 修复合辑** | [#1298](https://github.com/anthropics/skills/pull/1298) 等3个 | 修复 skill-creator 的核心评估 bug，社区复现多、呼声高；但三个 PR 功能重叠，需 maintainer 整合后合入 |

---

## 4. Skills 生态洞察（一句话总结）

**社区最集中的诉求是"技能质量的可信闭环"**——从评估信号失真（recall=0%）、安全信任边界漏洞（namespace 滥用）、上下文失控（156k token 注入）到组织内分享渠道缺失，本质上都在追问同一个问题：*如何让 Skill 从"个人脚本"进化为"组织级可信资产"，并具备可验证的质量、安全与效率边界。* 这也暗示 Anthropic 官方下一步的重点：技能评估框架（skill-creator 修复）、安全分级机制与共享基础设施（plugin registry/org library）将决定生态的下一波爆发点。

---

# Claude Code 社区动态日报

**日期：2026-08-14** | 数据来源：github.com/anthropics/claude-code


## 今日速览

今日发布 v2.1.232 和 v2.1.231 两个版本，前者默认开启 subagent forking 并支持在提示中引用其他会话，后者修复了 Slack 等 MCP 服务器的 OAuth 重定向 URI 不匹配问题。社区焦点集中在 Windows 桌面端跨会话消息投递的严重回归（多个 issue 指向同一根因）、Claude Max 会话限额异常消耗的长期争议（已积累 832 条评论），以及权限白名单规则在多处被静默忽略的顽疾。


## 版本发布

### v2.1.232
- **Subagent forking 默认开启**：`subagent_type: "fork"` 的子代理可继承完整对话上下文与提示缓存；交互式会话中非 teammate 代理默认在后台运行
- 在提示中输入 `@` 可按名称引用另一个 Claude 会话

### v2.1.231
- 修复使用预注册 OAuth 客户端（如 Slack）的 MCP 服务器登录时出现重定向 URI 不匹配的问题


## 社区热点 Issues（Top 10）

### 1. Claude Max 会话限额异常消耗 [🔥 832 评论 / 474 👍]
**#38335** — 用户报告自 2026 年 3 月 23 日起，CLI 使用场景下 Max 套餐会话限额消耗速度异常，疑似存在计费或配额计算缺陷。该问题已持续近 5 个月，评论数远超其他 issue，是社区目前最强烈的痛点。

🔗 https://github.com/anthropics/claude-code/issues/38335

### 2. 多 Claude 账号管理 [165 评论 / 723 👍]
**#18435** — 社区高票需求：在 Desktop 应用中支持多账号配置与一键切换。723 个赞表明这是大量用户的核心工作流诉求。

🔗 https://github.com/anthropics/claude-code/issues/18435

### 3. CLI 与桌面端会话历史同步 [34 评论 / 123 👍]
**#28791** — 用户希望 CLI 与 Claude Code 桌面应用之间双向同步对话历史，当前隔离状态严重割裂了跨端工作流。

🔗 https://github.com/anthropics/claude-code/issues/28791

### 4. Windows 桌面端 GPU 进程崩溃导致全部会话丢失 [28 评论]
**#81698** — 退出代码 101457950 的 GPU 进程崩溃会拖垮整个应用及所有运行中会话。影响 Windows 用户，RTX 5080 等高配机型同样复现。

🔗 https://github.com/anthropics/claude-code/issues/81698

### 5. Opus 5 静默覆盖用户代理委托策略 [23 评论 / 49 👍]
**#80988** — 系统提示中 `heron_brook` 段落注入 "Do not call the AgentTool unless the user requested it" 指令，仅对 Opus 5 生效，且无关闭选项。用户配置的代理委托策略被静默覆盖，引发对模型行为可控性的担忧。

🔗 https://github.com/anthropics/claude-code/issues/80988

### 6. 跨会话消息接收端完全无响应 [14 评论]
**#86012** — 桌面端 1.28929.0.0（CCD 2.1.227）跨会话发送消息后，接收端查询完全卡死（`hadFirstResponse=false`），直到空闲超时强制终止（15-20 分钟）。复现稳定，影响多平台。

🔗 https://github.com/anthropics/claude-code/issues/86012

### 7. `--continue` 找不到 `-p` 创建的会话 [13 评论]
**#82536** — 非交互模式（`-p`）创建的会话无法通过 `--continue` 恢复，影响自动化脚本与人工接续的衔接。

🔗 https://github.com/anthropics/claude-code/issues/82536

### 8. SSH_AUTH_SOCK 缺失导致 1Password SSH agent 失效 [12 评论 / 23 👍]
**#29717** — `CC_ENV_EXTRACT_LIST` 白名单未包含 `SSH_AUTH_SOCK`，导致桌面端 SSH 连接无法使用 1Password SSH agent。自 3 月提出至今仍在开放状态。

🔗 https://github.com/anthropics/claude-code/issues/29717

### 9. 并行工具调用后提示缓存完全重建 [10 评论 / 6 👍]
**#63930** — 自 v2.1.154 起，多并行工具调用后提示缓存频繁失效并整体重建，实测 74% 的 `cache_creation` 令牌被浪费，严重影响 Opus 4.8 使用成本。

🔗 https://github.com/anthropics/claude-code/issues/63930

### 10. 原生安装器产出未签名 macOS 应用包 [10 评论 / 2 👍]
**#70647** — 原生安装器生成的 `ClaudeCode.app` 缺少 `_CodeSignature` 签名封条，macOS 报"应用已损坏无法打开"。影响所有使用原生安装方式的 macOS 用户。

🔗 https://github.com/anthropics/claude-code/issues/70647


## 重要 PR 进展

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#86537](https://github.com/anthropics/claude-code/pull/86537) | Fix duplicated word in CHANGELOG.md | 🟢 开放 | 修复 1.0.124 版本 CHANGELOG 中 "to to" 重复用词，文档级修正 |
| [#60280](https://github.com/anthropics/claude-code/pull/60280) | chore(ci): SHA-pin remaining actions/checkout and actions/github-script | ⚫ 已关闭 | 将 6 个工作流中的第三方 action 全部 SHA 固定（如 `actions/checkout@v4` → 指定 commit），加固供应链安全，是 #56784 的后续补全 |

> 注：过去 24 小时 PR 数量较少（仅 2 条），主要为文档与 CI 维护类改动，无功能型 PR 合并。


## 功能需求趋势

1. **多账号与配置管理**（#18435）：Desktop 多 Claude 账号切换、CLI 与桌面端会话历史同步（#28791）——用户在跨设备、跨端场景下对"一处配置、处处可用"的诉求强烈。
2. **跨会话消息可靠性**：密集出现于 Windows 桌面端（#86012、#86275、#86298、#86385），核心是 send_message 投递后不触发接收端响应，升级后回归，已成为当前最高频缺陷类别。
3. **权限白名单规则一致性**（#80658、#81535、#86175）：MCP 工具与 preview_start 等动作的 `permissions.allow` 规则在多个版本中被静默忽略，每轮调用都重新弹窗，破坏自动化流程。
4. **提示缓存与成本优化**（#63930）：并行工具调用引发缓存重建，用户对 Opus 4.8 时代的 token 成本敏感度显著上升。
5. **模型行为可控性**（#80988）：系统提示注入的隐藏指令影响用户对代理策略的自主配置，反映出社区对"模型不做什么"的约束能力需求。


## 开发者关注点

**1. 跨会话消息投递全面回归（最紧急）**
Windows 桌面端 1.28929.0 / CC 2.1.227 自动更新后，多条 issue（#86275、#86298、#86385、#86012）指向同一类问题：消息报告成功但从未送达、或送达后不触发响应回合，且 2.1.231 仍未修复。多用户明确标注"regression"，对升级持谨慎态度。

**2. 升级破坏既有配置**
- `permissions.allow` 规则在多处失效（#80658、#81535），每次调用重新弹窗
- preview_start 在 Bypass 模式下仍弹权限卡（#86175），且无法写入白名单
- Cowork 任务列表在合并后的 Home 中丢失"按项目分组"能力（#85930）

**3. GPU 崩溃导致应用不可用**
#81698、#81341、#82967、#83403 四条独立 issue 均指向桌面端 GPU 进程崩溃，严重时应用无法再次启动，需完全重装。涉及 Windows（含 MSIX 签名冲突）、macOS 多平台。

**4. 后台任务与子代理状态管理**
#78338（Linux 后台代理丢弃消息与完成通知）、#86345（子代理后台任务泄漏无法清理）、#86471（后台子代理报 completed 但结果为空）——后台任务可靠性已成为多平台共性问题。

**5. 安装与签名问题持续**
#70647（macOS 未签名应用包）、#71861/71865/71871（安全过滤器误报阻断了合法的 USB 设备调试工作流）——前者阻塞新用户上手，后者影响嵌入式开发场景的可用性。

**6. 成本可见性与配额透明度**
#38335（Max 会话限额异常消耗）与 #63930（缓存重建浪费）反映用户对"钱花在哪"的敏感：前者是计费争议，后者是技术层面的缓存策略优化空间，两者均维持高热度。

---

*日报基于 GitHub 公开数据自动生成，仅供技术参考，不构成官方立场。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-14** | 数据来源：github.com/openai/codex

---

## 今日速览

昨日社区讨论热度集中在 Windows 平台的沙箱与扩展资源加载问题，多个高赞 Issue 持续发酵，但相关修复 PR（如 Windows 沙箱 manifest 嵌入）已在合入流程中。与此同时，大量 app-server 基础设施 PR（线程回滚、后台队列等）已关闭，表明核心架构正在快速演进。功能需求方面，TUI 支持 LaTeX 渲染的关注度持续上升。


## 版本发布

过去 24 小时内发布了 3 个 Rust 版本的预发布构建，未附带显著的公开更新说明：

- **[rust-v0.148.0-alpha.13](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.13)** — 最新 alpha 版本
- **[rust-v0.148.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.12)**
- **[rust-v0.148.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.11)**

注：版本号集中于 0.148.0-alpha 系列，推测为下一正式版本的功能冻结前的密集迭代。


## 社区热点 Issues

以下为过去 24 小时内更新最活跃、讨论度最高的 10 个 Issue：

### 1. [Windows] Codex 扩展无法启动："The extension couldn't load its resources"（#37458）
- **状态**：已关闭 | 53 条评论 | 👍 11
- **链接**：[Issue #37458](https://github.com/openai/codex/issues/37458)
- **现象**：Windows + VS Code 1.132.0 下，Codex 面板启动失败并提示无法加载资源（扩展版本 26.803.41515）。
- **重要性**：该 Issue 与 #37517（Remote-SSH 场景 CSP 字体阻塞）高度相关，均为最新扩展版本资源加载失败。适合关注 Windows/远程开发的同学优先排查。

### 2. Multi-Agent V2 向外站 Responses 供应商发送 OpenAI 专用 agent_message 类型（#33551）
- **状态**：开启 | 8 条评论 | 👍 6
- **链接**：[Issue #33551](https://github.com/openai/codex/issues/33551)
- **现象**：启用 Multi-Agent V2 后，Codex 向 Ollama 等外部 Responses 兼容供应商发送 OpenAI 特有 `agent_message` 类型，外部供应商无法解析。
- **重要性**：直接阻碍自定义模型/外部供应商使用多智能体模式，是集成本地模型用户的核心痛点。

### 3. 新实时语音对话未关联所选项目文件夹，以"无项目"状态启动（#36195）
- **状态**：开启 | 4 条评论 | 👍 1
- **链接**：[Issue #36195](https://github.com/openai/codex/issues/36195)
- **现象**：macOS 26.721.81911 版本中，新建实时语音会话时不会附加到当前选中的项目文件夹。
- **重要性**：影响语音编程工作流的上下文连续性和代码库检索能力。

### 4. [Windows] 旧子代理在应用重启后仍保持"运行中"状态（#38408）
- **状态**：开启 | 3 条评论
- **链接**：[Issue #38408](https://github.com/openai/codex/issues/38408)
- **现象**：Windows 上重启 Codex App 后，子代理面板中 16 个旧子代理仍显示为运行中（不可交互）。
- **重要性**：反映应用会话状态持久化与 UI 同步逻辑缺陷，影响长任务管理。

### 5. Windows 沙箱：当解析的 shell 为 MSIX（商店版）pwsh 时 CreateProcessAsUserW 失败（#35871）
- **状态**：开启 | 13 条评论 | 👍 3
- **链接**：[Issue #35871](https://github.com/openai/codex/issues/35871)
- **现象**：Windows 沙箱无法启动 Microsoft Store 版 PowerShell 7，报错 `CreateProcessAsUserW failed: 5 (Access is denied.)`。
- **重要性**：Windows 沙箱在默认商店版 PowerShell 环境下完全不可用，影响面较大。

### 6. MCP stdio 服务器泄漏管道文件描述符及孤儿子进程导致 EMFILE（#26984）
- **状态**：开启 | 21 条评论 | 👍 4
- **链接**：[Issue #26984](https://github.com/openai/codex/issues/26984)
- **现象**：长会话中 MCP stdio 服务器累积泄漏，最终触发 "Too many open files" (os error 24)。
- **重要性**：长时间运行会话的稳定性关键问题，影响重度 MCP 用户。

### 7. GitHub 审查连接器配额用尽后无重试指引（#38405）
- **状态**：开启 | 3 条评论
- **链接**：[Issue #38405](https://github.com/openai/codex/issues/38405)
- **现象**：GitHub 托管的 Codex 审查者在配额用尽时仅返回 "Please try again later"，未提供任何重试时间或升级建议。
- **重要性**：对依赖自动化安全审查的团队而言，配额策略不可见会严重阻塞流程。

### 8. 长会话压缩后线程读取负载过大，客户端截断（#38466）
- **状态**：开启 | 3 条评论（今日新提交）
- **链接**：[Issue #38466](https://github.com/openai/codex/issues/38466)
- **现象**：长时间 Desktop 会话经多次压缩后产生极大 rollout 历史，读取线程返回超大数据被客户端截断，恢复或检查会话困难。
- **重要性**：长上下文管理的核心体验问题，与 #31198（日志 145GiB）同类。今日新提交，或为新反馈趋势。

### 9. TUI Markdown 数学渲染支持（#18906）
- **状态**：开启 | 15 条评论 | 👍 22
- **链接**：[Issue #18906](https://github.com/openai/codex/issues/18906)
- **现象**：终端 UI 不支持行内/块级 LaTeX 渲染。
- **重要性**：高赞功能需求，影响科研/数学相关用户在 TUI 场景的阅读体验。

### 10. 桌面端登录将已验证账户路由至手机绑定页而非 MFA 挑战（#34934）
- **状态**：开启 | 3 条评论 | 👍 3
- **链接**：[Issue #34934](https://github.com/openai/codex/issues/34934)
- **现象**：macOS 桌面端已绑定 SMS 验证因素的账户在登录时被引导至 `auth.openai.com/add-phone` 绑定手机页面，而非直接要求 MFA 验证码。
- **重要性**：属于身份认证流程严重异常，受影响用户无法正常登录。


## 重要 PR 进展

以下为过去 24 小时更新/关闭的关键 PR：

### 1. [CLOSED] 运行中任务的退出选项：取消、保留后台运行或停止（#38447）
- **链接**：[PR #38447](https://github.com/openai/codex/pull/38447)
- **内容**：本地 daemon 会话中，任务运行期间按 Ctrl-C 不再直接退出，而是提供菜单：取消任务并留在 Codex、退出但保留任务运行、或停止任务。
- **意义**：提升长任务与交互式会话并存的可用性，减少误退风险。

### 2. [CLOSED] Guardian V2 获取完整工具调用上下文（#38441）
- **链接**：[PR #38441](https://github.com/openai/codex/pull/38441)
- **内容**：Guardian V2 工具生命周期钩子收到的 `ToolPayload` 由仅含工具名+调用 ID 改为包含原始请求与对话上下文。
- **意义**：安全审查可基于完整上下文评估风险，是 Agent 安全能力的重要补强。

### 3. [CLOSED] 实验性线程队列 API（#38456）
- **链接**：[PR #38456](https://github.com/openai/codex/pull/38456)
- **内容**：新增 `thread/queue/add`、`list`、`update`、`delete`、`reorder`、`start` 等实验性接口，支持按 FIFO 自动调度排队提交。
- **意义**：为批量任务管理、串行执行场景提供 API 基础。

### 4. [CLOSED] 上下文压缩时保留客户端开发者消息（#38445）
- **链接**：[PR #38445](https://github.com/openai/codex/pull/38445)
- **内容**：当启用 `retain_client_developer_messages` 时，压缩上下文后保留客户端开发者指令不被清除。
- **意义**：解决压缩后开发者自定义指令丢失的核心痛点。

### 5. [CLOSED] 按服务器配置 MCP OAuth 回调端口（#38448）
- **链接**：[PR #38448](https://github.com/openai/codex/pull/38448)
- **内容**：MCP 服务器配置新增 `oauth.callback_port` 字段，支持从插件/技能依赖元数据中读取 `oauth.callbackPort` 并优先使用服务器特定端口。
- **意义**：修复多 MCP 服务器 OAuth 回调端口冲突问题。

### 6. [CLOSED] Bazel 构建嵌入 Windows 沙箱 manifest（#38450）
- **链接**：[PR #38450](https://github.com/openai/codex/pull/38450)
- **内容**：修复 `rules_rust` 丢失 per-binary linker 指令的问题，为 Windows 沙箱设置助手补上 `asInvoker` manifest。
- **意义**：直接回应近期 Windows 沙箱 UAC/权限相关 Issue（#35871、#30829 等），Bazel 构建用户将受益。

### 7. [CLOSED] 本地 MCP 请求增加 rustls 回退（#38436）
- **链接**：[PR #38436](https://github.com/openai/codex/pull/38436)
- **内容**：当平台 TLS 后端与 HTTPS 端点协议版本无法协商时，自动重试一次 rustls。
- **意义**：提升本地 MCP 连接（如自建服务）的兼容性。

### 8. [CLOSED] 模型升级元数据暴露退休时间（#38449）
- **链接**：[PR #38449](https://github.com/openai/codex/pull/38449)
- **内容**：解析并暴露 `model/list` 中 `upgradeInfo.retirementAt` 可空时间戳。
- **意义**：帮助用户与工具链提前感知模型下架/升级窗口。

### 9. [CLOSED] 全历史子代理刷新当前时间提醒（#38446）
- **链接**：[PR #38446](https://github.com/openai/codex/pull/38446)
- **内容**：复制父历史到全历史子代理时排除继承的当前时间提醒，仅保留子代理新生成的提醒。
- **意义**：修复长时间运行子代理中时间提醒陈旧/累积问题。

### 10. [CLOSED] 分页线程回滚支持（#38440）
- **链接**：[PR #38440](https://github.com/openai/codex/pull/38440)
- **内容**：新增实验性 `thread/revert` 请求，将分页线程持久历史替换为 `beforeTurnId` 之前的前缀，同时保留线程 ID，并支持订阅保持。
- **意义**：与 #38463（保留跨回滚的订阅）配套，为长线程管理提供回滚能力。


## 功能需求趋势

| 方向 | 代表 Issue/PR | 说明 |
|---|---|---|
| **Windows 平台稳定性** | [#37458](https://github.com/openai/codex/issues/37458)、[#35871](https://github.com/openai/codex/issues/35871)、[#30829](https://github.com/openai/codex/issues/30829)、PR [#38450](https://github.com/openai/codex/pull/38450) | Windows 上扩展资源加载失败、沙箱权限问题频发，是当前社区第一大焦点 |
| **长会话/上下文管理** | [#38466](https://github.com/openai/codex/issues/38466)、[#31198](https://github.com/openai/codex/issues/31198)、PR [#38445](https://github.com/openai/codex/pull/38445)、[#38440](https://github.com/openai/codex/pull/38440) | 压缩后数据膨胀、开发者消息保留、线程回滚等均为活跃关注点 |
| **外部模型/供应商兼容性** | [#33551](https://github.com/openai/codex/issues/33551)、PR [#38436](https://github.com/openai/codex/pull/38436) | Multi-Agent 消息类型与本地 MCP TLS 的兼容性改进均为高频诉求 |
| **TUI 增强** | [#18906](https://github.com/openai/codex/issues/18906)（👍22）、[#24073](https://github.com/openai/codex/issues/24073) | 数学渲染、复制指定回复等功能需求持续获得高赞 |
| **任务队列与并发控制** | PR [#38456](https://github.com/openai/codex/pull/38456)、[#38447](https://github.com/openai/codex/pull/38447) | 实验性队列 API 和运行中任务的退出选项为批量/后台任务场景铺路 |


## 开发者关注点

- **Windows 平台体验是最大短板**：资源加载失败、沙箱权限错误、MSIX 兼容性问题（#37458、#35871）频繁出现，严重拖累 Windows 用户体验，而相关修复（PR #38450）刚刚合入，建议 Windows 用户关注下一版本验证结果。
- **长会话稳定性与可恢复性**：压缩后线程数据膨胀导致截断（#38466）、日志体积达到 145GiB（#31198）、旧子代理持久占用资源（#38408），反映长会话生命周期管理仍有较多短板。
- **MCP 生态成熟度不足**：stdio 泄漏（#26984）、TLS 协商失败（PR #38436）、OAuth 冲突（PR #38448）等问题提示 MCP 仍是新功能，稳定性方面建议生产环境谨慎采用。
- **外部供应商的实际可用性**：不少用户尝试接入 Ollama 等本地/第三方模型，但 Multi-Agent V2 发送 OpenAI 专用消息类型的问题（#33551）阻碍了这一场景。
- **语音与项目上下文的割裂**（#36195）：实时语音会话不携带项目上下文，影响实际编程场景中的体验，反馈集中于 macOS 用户。

---

*本日报基于公开 GitHub 数据自动生成，仅供技术参考，不构成官方立场。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-14

## 今日速览

今日社区焦点集中在**子代理（Subagent）稳定性**与**安全合规修复**两大方向。最受关注的是子代理在达到 `MAX_TURNS` 后仍误报"成功"的 Bug，以及通用代理无故挂起的问题——两者均被标记为 P1 且持续有用户反馈。PR 方面，供应链安全（`simple-git` 升级、防止 fork 代码 RCE）与 A2A 服务器鉴权漏洞修复是重点。此外，模型新增了 Claude Sonnet 4.5 和 Opus 4.8 的支持，并发布了 v0.56.0 夜间版，重点强化了 eval 基础设施。

---

## 版本发布

### v0.56.0-nightly.20260813.g1ac337739
- **新增**: 引入工具调用格式化器（tool call formatter），并集成失败摘要到 eval 流程（PR #28344, #28305）
- 该版本为夜间构建，主要面向 eval 基础设施的完善，无面向用户的重大功能变更

🔗 [查看 Release](https://github.com/google-gemini/gemini-cli/releases)

---

## 社区热点 Issues（Top 10）

### 1. Subagent 达 MAX_TURNS 被误报为成功 🐛 P1
- **Issue**: [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **现象**: `codebase_investigator` 子代理在达到最大轮次限制后，仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，实际未完成任何分析，掩盖了中断事实
- **社区反应**: 12 条评论，作者详细描述了复现路径（涉及两个本地仓库的代码调查）。该问题直接影响用户对代理执行结果的信任度，被标记为 `need-retesting`

### 2. 通用代理（Generalist agent）无限挂起 🐛 P1
- **Issue**: [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **现象**: 一旦 `gemini-cli` 将任务委派给通用代理，操作（如创建文件夹）会无限挂起，用户最长等待 1 小时无响应
- **社区反应**: 8 条评论 + 8 👍，用户提供了有效绕过方法（提示词中禁止使用子代理可解决），是近期影响面较广的稳定性问题

### 3. 利用模型原生 bash 能力：零依赖沙箱与意图路由 ✨ P2
- **Issue**: [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
- **内容**: 提议让 Gemini 3 模型像原生 bash 用户一样直接调用 POSIX 工具（grep/sed/awk），通过零依赖 OS 沙箱保证安全，并基于执行后意图进行路由
- **社区反应**: 8 条评论，该提案直击模型能力与工具链匹配的核心问题，设计空间较大

### 4. 组件级评估体系（EPIC）📊 P1
- **Issue**: [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)
- **内容**: 自引入行为评估以来已生成 76 个测试，本 EPIC 跟踪对 6 个支持的 Gemini 模型定期运行这些测试的体系建设
- **社区反应**: 7 条评论，是评估基础设施的关键里程碑，与今日夜间版发布内容高度契合

### 5. AST 感知的文件读取与代码映射评估（EPIC）🔍 P2
- **Issue**: [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
- **内容**: 跟踪 AST 感知工具（如精确读取方法边界）是否能在单次工具调用中降低 token 噪声、减少回合数
- **社区反应**: 7 条评论，是 #22746（推荐 tilth/glyph 工具）的上游 EPIC，关注长期代码理解能力的提升

### 6. Gemini 对自定义 skills 和子代理使用不足 🤔 P2
- **Issue**: [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **现象**: 用户反馈 Gemini 几乎不会主动调用自定义 skills 和子代理，即使相关度很高（如 gradle/git skills），仅在被明确要求时才会使用
- **社区反应**: 6 条评论，该问题与"工具采用率"直接相关，影响用户自定义工作流的落地

### 7. Shell 命令执行完仍卡在 "Waiting input" 🐛 P1
- **Issue**: [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **现象**: 极简单的 CLI 命令执行完成后，界面仍显示命令活动并等待用户输入，必须手动干预
- **社区反应**: 4 条评论 + 3 👍，是 P1 核心稳定性问题，直接影响日常使用流畅度

### 8. Auto Memory 对低信号会话无限重试 🐛 P2
- **Issue**: [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **现象**: 后台提取代理认为某会话低信号而跳过读取时，该会话不会被标记为已处理，导致反复出现在索引中并不断重试
- **社区反应**: 5 条评论，属记忆系统长期稳定性的核心短板之一

### 9. Auto Memory 需确定性的敏感信息脱敏 🔒 P2
- **Issue**: [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
- **问题**: 本地转录内容在送入模型前缺乏确定性的脱敏机制，当前仅依赖提示词要求模型自行脱敏，且服务端可能记录已存在的技能内容
- **社区反应**: 4 条评论，涉及隐私安全，需架构层面的修正

### 10. 浏览器子代理在 Wayland 下失败 🐛 P1
- **Issue**: [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
- **现象**: 浏览器子代理在 Wayland 环境下直接失败，返回 `Termination Reason: GOAL` 但无有效操作
- **社区反应**: 4 条评论 + 1 👍，Linux 桌面用户（尤其是新发行版默认 Wayland）受影响明显

---

## 重要 PR 进展（Top 10）

### 1. 🔒 修复 eval 工作流供应链 RCE（安全）
- **PR**: [#28740](https://github.com/google-gemini/gemini-cli/pull/28740)（OPEN, size/l）
- **内容**: 修复未受信任的 fork 代码在 `pull_request_target` 特权上下文中执行的问题（#28336），将 eval 拆分为安全的 PR 构建 + 可信的 `workflow_run` 执行

### 2. 🔒 升级 simple-git 修复 CVE-2026-28292（安全）
- **PR**: [#28778](https://github.com/google-gemini/gemini-cli/pull/28778)（OPEN, size/s）
- **内容**: `simple-git` 从 3.28.0 升至 3.32.3，扫描器（trivy）标记为 CRITICAL 级别漏洞，建议尽快合并

### 3. ✅ 新增 Claude Sonnet 4.5 / Opus 4.8 模型定义
- **PR**: [#28803](https://github.com/google-gemini/gemini-cli/pull/28803)（CLOSED, size/xl）
- **内容**: 新增 `claude-sonnet-4-5` 和 `claude-opus-4-8` 常量、别名解析及策略链回退，并更新默认模型配置（显示名和描述）

### 4. ✅ 容量错误上下文感知重试（P1）
- **PR**: [#28790](https://github.com/google-gemini/gemini-cli/pull/28790)（CLOSED, size/l）
- **内容**: 修复 #28761 容量耗尽重试回归：非交互式 CLI 运行可自动退避重试，最多 2 次静默重试，显著提升无人值守场景的鲁棒性

### 5. ✅ 取消/中止时回滚整个多轮请求（核心修复）
- **PR**: [#28801](https://github.com/google-gemini/gemini-cli/pull/28801)（CLOSED, size/m）
- **内容**: 此前取消多轮提示会导致会话停留在未完成的工具响应状态，影响后续新请求；本 PR 实现整体回滚，保持会话一致性

### 6. 🔒 A2A 服务器鉴权与路径穿越修复（安全）
- **PR**: [#28699](https://github.com/google-gemini/gemini-cli/pull/28699)（OPEN, size/l）
- **内容**: 自定义 REST 路由（`/tasks`、`/executeCommand` 等）绕过 `UserBuilder` 导致无凭据可访问；同时修复 checkpoint 路径穿越漏洞

### 7. ✅ Eval 工具扩展：批量读取、MCP 资源、内部文档
- **PR**: [#28804](https://github.com/google-gemini/gemini-cli/pull/28804)（OPEN, size/l）
- **内容**: 为 `read_many_files`、`get_internal_docs`、`list_mcp_resources`、`read_mcp_resource` 新增行为评估测试，补齐 eval 覆盖

### 8. ✅ 修复布尔 thought parts 泄漏为 `[Thought: true]` 文本
- **PR**: [#28624](https://github.com/google-gemini/gemini-cli/pull/28624)（OPEN, size/s, size/m）
- **内容**: 修复内部 `thought: true` 字段泄漏到模型思考的文本表示中，避免用户看到垃圾信息（Fixes #23525）

### 9. ✅ 修复损坏的 MCP 配置被当作空配置（P1）
- **PR**: [#28787](https://github.com/google-gemini/gemini-cli/pull/28787)（OPEN, size/s, size/m）
- **内容**: JSON 解析失败时，此前会返回与"文件不存在"相同的空对象，导致所有 MCP 服务器被默认启用，存在安全风险；现在会正确区分错误状态

### 10. 🔒 OAuth 回调超时泄漏与资源释放（安全）
- **PR**: [#28678](https://github.com/google-gemini/gemini-cli/pull/28678)（OPEN, size/m）
- **内容**: 集中管理回调服务器结算与资源清理，防止过期超时回调（stale timeout callbacks）导致的内存泄漏（Resolves #28652）

---

## 功能需求趋势

从近期 Issue 中可以提炼出以下社区高度关注的方向：

### 1. 子代理生态的成熟化
- **主动使用 skills/subagents**: #21968 指出模型在未被明确指示时几乎不会主动调用用户自定义技能，这限制了自定义工作流的价值
- **轨迹可见性与共享**: #22598 要求子代理轨迹可通过 `/chat share` 分享，便于 review 和评估
- **自感知能力**: #21432 期望 Gemini CLI 能准确理解自身的 CLI 参数、快捷键和工作机制，从而作为自己的专家指南

### 2. 评估（Eval）基础设施的系统化
- 从 EPIC #24353 到今日合并的多个 eval 相关 PR，社区（及官方）正在系统性建设行为评估套件
- 工具调用格式化、失败摘要集成、多工具覆盖（文件读取、MCP 资源、技能获取）是当前重点

### 3. 安全与信任边界
- **供应链安全**: 多个 PR 直接针对 GitHub Actions 的 fork 代码执行风险与依赖漏洞（CVE-2026-28292）
- **记忆系统隐私**: #26525 要求对 Auto Memory 的转录内容进行确定性脱敏，而不是依赖模型自觉
- **破坏性操作防护**: #22672 希望代理在 git 复杂操作、数据库维护等场景能主动避免或警告使用 `--force` 等破坏性命令

### 4. 系统调用与沙箱
- #19873 提议利用模型原生的 bash 偏好，通过零依赖沙箱安全地调用标准 POSIX 工具，同时用执行后意图路由来确保安全性
- AST 感知工具（#22745）被长期看好，认为能减少 token 消耗并提升代码理解的精准度

---

## 开发者关注点

综合近期反馈与讨论，开发者在实际使用中遇到的痛点和高频需求主要集中在：

1. **稳定性与可靠性是首要诉求**
   - 通用代理挂起（#21409）、Shell 执行后卡死（#25166）、取消后会话状态损坏（#28801）等稳定性问题引发了最多的 P1 标记和用户共鸣
   - 子代理返回结果的"真实性"（#22323 误报成功）比功能丰富度更受关注

2. **自主性与可控性的平衡**
   - 用户希望模型更主动地使用自定义工具（skills/subagents），但同时也反映代理"自作主张"运行子代理（#22093 权限问题）或使用破坏性命令（#22672）会增加不安全感
   - 期望的路径是在充分尊重配置的前提下，提升工具调用的智能程度

3. **记忆系统的质量与边界**
   - Auto Memory 系列问题（#26522 低信号重试、#26523 无效补丁静默跳过、#26525 脱敏不足）说明记忆功能仍是"黑盒"，用户对后台数据流向和重试逻辑存在顾虑
   - 社区期待更透明、可干预的记忆管理机制

4. **跨平台体验一致性**
   - Windows（ripgrep EFTYPE 错误 #25378、WSL2 剪贴板 #27588）、Wayland（#21983）、终端 resize 闪烁（#21924）等平台相关问题持续存在，是大量用户每天直接面对的体验痛点

5. **配置与扩展机制的可靠性**
   - symlink 不被识别为 subagent（#20079）、settings.json 覆盖被忽略（#22267）、MCP 配置损坏被静默当作空配置（#28787）等问题，反映出配置系统的容错性和文档完善度仍需加强

---

> 注：以上内容基于 github.com/google-gemini/gemini-cli 在 2026-08-14 的公开数据自动生成，标记为 🔒 maintainer only 的 Issue 可能不对外开放讨论。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-14** | 数据来源：github/copilot-cli


## 1. 今日速览

今日社区动态围绕**子代理模型配置与推理强度（reasoning effort）**展开，多起 Issue 聚焦于 `claude-haiku-4.5` 不支持 `medium` 推理强度导致执行失败的问题。此外，远程 MCP 服务器的 OAuth 认证与稳定性成为高频痛点，出现多起 5xx 错误无重试、并发令牌刷新竞态等报告。功能需求方面，社区持续呼吁更精细的每代理模型控制能力。


## 2. 版本发布

### v1.0.80-0

**新增：**
- 新增 `--enable-mcp-server` 标志，可在本次运行中重新启用设置里被禁用的 MCP 服务器。
- 共享会话状态提示：`--ahp` 模式下，当你加入他人会话时，会话行会显示 `2 clients`（或更多）；Sessions 标签页同步更新。


## 3. 社区热点 Issues（Top 10）

### 3.1 子代理推理强度问题集中爆发

**#4345** [CLOSED] `claude-haiku-4.5` 不支持 `medium` 推理强度 — [链接](https://github.com/github/copilot-cli/issues/4345)

> 当 `copilot_cli_opus_medium_effort_default` 与 `copilot_cli_gpt_5_4_mini_for_explore` 两个服务端功能开关同时激活时，子代理执行反复报错。该问题已关闭，但社区反应激烈（5 条评论，4 👍）。

**#4473** [OPEN] 相同错误仍在 triage 阶段 — [链接](https://github.com/github/copilot-cli/issues/4473)

> 昨天新提交的 Issue（0 评论，0 👍），说明 #4345 的修复可能未完全覆盖所有场景，或问题在特定路由条件下依然存在。内部路由到 `claude-haiku-4.5` 时仍会附带 `medium` 推理强度。

**为何重要：** 两个独立 Issue 指向同一根因，说明 CLI 在子代理路由时未正确校验模型能力与推理强度的兼容性，影响面较大。


### 3.2 自定义 Agent 模型配置能力不足

**#2904** [OPEN] 自定义 Agent YAML Frontmatter 应支持推理强度配置 — [链接](https://github.com/github/copilot-cli/issues/2904)

> 创建于 4 月，持续活跃至今（6 条评论，20 👍）。自定义 `.agent.md` 文件支持 `model` 字段锁定模型，但无法按代理单独设置推理强度，目前只能通过全局 `--effort=LEVEL` 配置。该 Issue 是社区高票需求。

**#2133** [OPEN] `model` 字段拒绝数组语法，与 VS Code Copilot Chat 不兼容 — [链接](https://github.com/github/copilot-cli/issues/2133)

> 同样持续活跃（4 条评论，7 👍）。VS Code Copilot Chat 支持 `model` 数组语法，但 CLI 直接拒绝加载。两个官方客户端行为不一致，影响自定义 Agent 的跨平台复用。


### 3.3 远程 MCP 服务器稳定性问题

**#4480** [OPEN] Atlassian MCP OAuth 在 1.0.79 回归失败 — [链接](https://github.com/github/copilot-cli/issues/4480)

> 1.0.71 正常工作，升级至 1.0.79 后 OAuth 发现阶段报 `Incompatible authorization server (RFC 8414 §3.3)`，issuer 不匹配。

**#4472** [OPEN] 并发工具调用 + 令牌刷新竞态导致请求取消 — [链接](https://github.com/github/copilot-cli/issues/4472)

> 当多个工具调用并发发起且令牌已过期时，每个调用各自触发刷新流程，产生多个 `rmcp::service` 实例，最终导致 "transport closed before the tool responded"。Token 刷新逻辑缺少单飞（single-flight）去重机制。

**#4466** [OPEN] 瞬时 5xx 错误导致 MCP 服务器整个会话被标记失败 — [链接](https://github.com/github/copilot-cli/issues/4466)

> `initialize` 阶段遇到 502 后，CLI 将该服务器标记为永久失败，整个会话不再重试，缺少退避重试机制。

**为何重要：** MCP 生态正在快速扩张，但 OAuth 流程和错误恢复机制尚不成熟，成为影响实际使用的主要障碍。


### 3.4 会话管理与权限控制

**#4477** [OPEN] 停止操作导致整个会话丢失 — [链接](https://github.com/github/copilot-cli/issues/4477)

> 用户在代理执行期间点击停止按钮，整个会话（含原始提示词和编辑记录）被删除。高影响 bug，直接影响日常开发流程。

**#4469** [OPEN] 孤儿 `permission.requested` 事件在每次恢复会话时重放 — [链接](https://github.com/github/copilot-cli/issues/4469)

> 一个已运行 10 天的旧命令的目录访问请求，在每次恢复会话时反复弹出且无法消除。事件消费机制存在缺陷，导致权限请求被无限重放。


### 3.5 企业政策混淆

**#4481** [OPEN] 组织策略 UI 显示 "GitHub Copilot app" 已启用，但 CLI 仍被旧策略拦截 — [链接](https://github.com/github/copilot-cli/issues/4481)

> 政策 UI 声明 7 月 27 日 enforcement 起由新版策略接管，但实际 CLI 仍受旧 "Copilot CLI" 策略管控。企业管理员面临策略配置混乱。


## 4. 重要 PR 进展

> 过去 24 小时仅 1 条 PR 更新。

**#4476** [CLOSED] 文档：自定义 Agent 推理强度 frontmatter（Option A）— [链接](https://github.com/github/copilot-cli/pull/4476)

> 作者：romanstetsenko | 更新：2026-08-13

**摘要：** 针对 #2904 提出的 **Option A** 方案（专用 `effort` 字段，与 `model` 平级）编写文档，在 README.md 增加 "Custom Agents" 参考章节，覆盖现有 frontmatter 字段及新增的 `effort` 字段说明。

**社区价值：** 虽然 PR 已关闭，但文档化的方案为 #2904 的落地提供了具体路径参考，说明维护者正在认真评估该功能。


## 5. 功能需求趋势

| 趋势方向 | 代表 Issues | 热度 |
|---------|------------|------|
| **每代理模型/推理强度细粒度控制** | #2904（20👍）、#2133（7👍）、#4462 | 🔥🔥🔥 |
| **远程 MCP 稳定性与 OAuth 完善** | #4480、#4472、#4466、#4463、#4464 | 🔥🔥🔥 |
| **会话管理与恢复机制** | #4477、#4474、#4467、#4468 | 🔥🔥 |
| **插件自动更新与技能状态持久化** | #4465、#4471 | 🔥 |
| **外部会话监控 API** | #4470（Claude Code `agents --json` 对标） | 🔥 |
| **权限系统精确化** | #4469、#4482、#4237 | 🔥 |


## 6. 开发者关注点

### 6.1 高频痛点：模型路由与推理强度不匹配
多个 Issue（#4345、#4473、#4462）指向同一类问题——CLI 子代理路由时硬编码或错误传递推理强度参数，导致模型报错。其中 **#4462** 甚至出现配置的 `gpt-5.6-luna` 被静默替换为 `gpt-5.6-sol` 的情况。社区对"配置被静默忽略"尤为不满。

### 6.2 远程 MCP 的 OAuth 流程亟待修复
- 并发刷新竞态（#4472）暴露了令牌刷新缺少去重机制；
- 瞬时 5xx 无重试（#4466）说明错误恢复策略过于保守；
- Windows 平台 socket 10013 错误（#4463）和 Entra OAuth scope 混用问题（#4464）反映了跨平台和跨 IdP 的兼容性短板。

### 6.3 会话数据安全与生命周期管理
- 停止操作导致整个会话丢失（#4477）被多次报告，用户对数据丢失零容忍；
- 长时运行会话耗尽事件存储后状态失真（#4467）；
- 孤儿权限事件无限重放（#4469）影响日常体验。

### 6.4 企业环境策略配置混乱
#4481 表明新旧策略切换存在衔接问题，企业在从 "Copilot CLI" 策略过渡到 "GitHub Copilot app" 策略时遇到障碍，需要更清晰的迁移指引。

---

*本日报基于 GitHub 公开数据自动生成，供技术参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报 — 2026-08-14

> 数据来源：GitHub `MoonshotAI/kimi-cli`，涵盖过去 24 小时更新内容。

---

### 1. 今日速览

过去 24 小时无新版本发布，社区焦点集中在三个存量高热度 Issue 上，其中 **#1283 记忆系统（Memory System）** 需求获得 38 条评论，依旧是社区呼声最高的功能；此外两个高严重性 Bug（**ACP 流式挂死** #2598、**失控乱码生成** #2597）持续发酵，均涉及长时运行稳定性和数据完整性，建议引起重视。

---

### 2. 版本发布

无（过去 24 小时无新 Releases）。

---

### 3. 社区热点 Issues

以下按重要程度排序（依据讨论热度、影响范围及严重性）：

| 序号 | Issue | 标题 | 状态/评论 | 重要性说明 |
|------|-------|------|----------|-----------|
| 1 | [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283) | Memory System: Persistent context across sessions | OPEN / 38 评论 | 社区长期头号需求，用户希望 CLI 能跨会话记住项目模式与用户偏好，支持自动与手动两类记忆，对工作流连续性影响重大 |
| 2 | [#2598](https://github.com/MoonshotAI/kimi-cli/issues/2598) | ACP/print 流式响应静默挂死 | OPEN / 1 评论 | 高严重性 Bug：0.34.0 ACP 模式偶发连接挂死，无超时机制，且被顶替轮次的数据完全不落盘（丢失 wire.jsonl 记录），影响数据可审计性。0.31.1 的修复仅覆盖 Esc 场景，未根治 |
| 3 | [#2597](https://github.com/MoonshotAI/kimi-cli/issues/2597) | Runaway garbled generation — 88k tokens of gibberish | OPEN / 1 评论 | 严重稳定性问题：单次 LLM 推理持续 53 分钟，产生 88k 无意义 token（多语言乱码、重复片段），当前无中断/自停止机制，可能导致资源耗尽 |

> 说明：24 小时窗口内全部 3 条 Issue 已列出。均无 👍 数据，可能与数据接口未捕获相关字段有关。建议后两个 Bug 优先定位（参考 `num-samples` 与 max-tokens 相关配置）。

---

### 4. 重要 PR 进展

过去 24 小时无 PR 更新，无内容可展示。

---

### 5. 功能需求趋势

以下依据近期全部 Open Issues 归纳（含历史累积数据）：

| 趋势方向 | 代表性 Issue | 说明 |
|----------|-------------|------|
| **会话记忆 / 持久化上下文** | #1283 | 最大单一需求方向，期望自动记忆（AI 管理笔记）+ 手动记忆（用户指令）双层结构 |
| **流式/长时运行稳定性** | #2598, #2597 | ACP 模式挂死与 token 失控生成连续出现，反映底层流式处理与超时控制需加强 |
| **数据审计与可追溯性** | #2598 中子问题 | 用户关注 wire.jsonl 完整性，被顶替轮次不落盘影响调试与合规 |
| **IDE / 工具链集成** | （历史存量 Issue） | 社区持续关注与编辑器、CI/CD 工具的深度集成适配 |

---

### 6. 开发者关注点

- **超时与中断控制缺失**：当前 CLI 缺少流式空闲超时配置，`session/prompt` 无限等待；模型失控生成时无强制中断手段，开发者希望提供可配置的 token 上限与兜底超时机制。
- **数据可靠性**：流式传输完成但终帧缺失时，已生成内容不落盘（如 wire.jsonl 无记录），直接影响调试追踪与后续审计，需确保任何中断场景下已完成部分都能持久化。
- **跨会话上下文连续性**：多次请求同一场景的开发者普遍反映，每次会话需重复说明项目约定，希望引入记忆系统以降低重复操作成本。

---

*本日报基于 2026-08-14 数据快照生成，仅供技术参考。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-14

---

## 今日速览

v1.18.18 发布，修复了 Kimi 系统提示词选择错误和 xAI 模型推理强度问题。社区热度集中在 **V2 与 V1 的兼容性冲突**（数据库被 V2 迁移破坏）和 **OpenCode Zen 免费额度误报 429**（多条重复反馈，疑似服务端问题）。安全方面，`webfetch` 的 SSRF 漏洞、`opencode upgrade` 的 curl|bash 无校验问题均被提出，但相关修复 PR 或被关闭、或仍在审核中。

---

## 版本发布

### v1.18.18
- **修复**：Kimi 系统提示词现在能正确匹配官方 Moonshot 与 Kimi 提供商
- **修复**：修复 xAI 模型的 `xhigh` 推理强度选项

---

## 社区热点 Issues（Top 10）

1. **[#37012] 保留旧版布局选项（FEATURE）**
   - 作者：darkine24th | 评论：37 | 👍：41
   - 社区对 V2 新 UI 的批评持续升温——旧版布局可在主窗口直达几乎所有功能，新版需要反复导航。41 个 👍 表明这是当前社区**最强烈的 UI 诉求**。
   - https://github.com/anomalyco/opencode/issues/37012

2. **[#41470] “已复制到剪贴板”实际无效**
   - 作者：WqxLoveCoding | 评论：15 | 👍：1
   - 在 VSCode Server（Docker 环境）中使用 OpenCode 时，复制操作显示成功但剪贴板为空。该问题持续 4 天未解决，影响远程开发场景。
   - https://github.com/anomalyco/opencode/issues/41470

3. **[#42029] 429 FreeUsageLimitError：今天还没用就被限流**
   - 作者：smithyyang | 评论：5
   - 用户反馈未使用任何额度却立即收到“Rate limit exceeded”。与下文的 #42074、#42449 高度相似，指向 Zen 免费额度服务端存在系统性误判。
   - https://github.com/anomalyco/opencode/issues/42029

4. **[#42083] GitHub Copilot provider 显示零模型**
   - 作者：Keylessboi | 评论：5
   - 登录成功但模型选择器为空，`opencode models github-copilot` 直接报错。Copilot 集成在 1.18.15（Arch 包）上完全不可用。
   - https://github.com/anomalyco/opencode/issues/42083

5. **[#40516] 桌面应用启动时 provider/model/MCP 加载失败（约 80% 概率）**
   - 作者：ssc-esiemiat | 评论：4
   - 组织内多用户受影响。明确为版本回归：v1.18.4 正常，v1.18.5 至 v1.18.13 全部损坏。企业用户被长时间阻塞，严重性高。
   - https://github.com/anomalyco/opencode/issues/40516

6. **[#42434] [安全] `opencode upgrade` 无完整性校验执行远程脚本（curl|bash）**
   - 作者：shafqatevo | 评论：3
   - 供应链/TOCTOU 风险，攻击者可劫持升级流程在用户权限下执行任意代码。修复尚未提供。
   - https://github.com/anomalyco/opencode/issues/42434

7. **[#42448] [2.0] 高输出模型的压缩请求超过上下文窗口**
   - 作者：bbartels | 评论：2
   - 上下文使用达 79% 时自动压缩未触发，手动 `/compact` 也因“提示词+输出超限”失败。会话被卡死，V2 上下文管理存在严重缺陷。
   - https://github.com/anomalyco/opencode/issues/42448

8. **[#42260] [2.0] opencode2 共享 V1 数据库并破坏共存**
   - 作者：timrichardson | 评论：2
   - V2 直接迁移了 V1 的数据库 schema，导致 V1 中 `/move` 命令损坏、会话被困在 worktree 中。V1/V2 共存策略存在重大设计缺陷。
   - https://github.com/anomalyco/opencode/issues/42260

9. **[#42441 / #42411] Bug: opencode 删除了它自己**
   - 作者：omani | 评论：2
   - 通过 `pnpm i -g opencode-ai` 安装后，使用约一天后二进制文件凭空消失。已重复提交两次，安装器有严重故障。
   - https://github.com/anomalyco/opencode/issues/42441

10. **[#42435] [安全] webfetch 存在 SSRF 漏洞，守卫 PR 被关闭**
    - 作者：shafqatevo | 评论：2
    - `webfetch` 可访问 loopback/私网地址，构成本地 SSRF。关键问题：修复 PR #40851 已被关闭且未合并，漏洞当前仍暴露。
    - https://github.com/anomalyco/opencode/issues/42435

---

## 重要 PR 进展（Top 10）

1. **[#42444] 修复：保持 V1 数据库兼容性（已合入）**
   - 作者：thdxr | 状态：CLOSED
   - 停止 V1 `/move` 和 revert 投影重置已删除的 `session_context_epoch` 表；禁用实验性 workspace 路径对 V2 schema 的查询。直击 #42260 的根因。
   - https://github.com/anomalyco/opencode/pull/42444

2. **[#42446] 修复：延迟更新检查直到服务解析完成（已合入）**
   - 作者：thdxr | 状态：CLOSED
   - 先解析当前 CLI 版本的背景服务再做异步自动更新，防止旧客户端反复拒绝新服务端版本。从已关闭的 #42025 中提取的聚焦修复。
   - https://github.com/anomalyco/opencode/pull/42446

3. **[#42433] 修复：保留响应模型元数据（OPEN）**
   - 作者：KarmCraft | 状态：OPEN
   - 保存 AI SDK 的结构化 `response.modelId`，而非丢弃为仅别名（`provider/auto`）。关闭 #42420，关联 #26091。对使用路由/代理的用户至关重要。
   - https://github.com/anomalyco/opencode/pull/42433

4. **[#42450] 修复：使用文件时间清理工具输出（OPEN）**
   - 作者：opencode-agent[bot] | 状态：OPEN
   - 从编码 ID 时间戳改为文件系统修改时间判断保留期；元数据不可读时保留文件而非猜测删除。覆盖时间戳环绕边界。
   - https://github.com/anomalyco/opencode/pull/42450

5. **[#42453] 修复：Tab 上下文菜单行为（已合入）**
   - 作者：kitlangton | 状态：CLOSED
   - 使 V2 TUI 的会话 Tab 右键菜单仅响应指针操作：点击外部即关闭、右键再次点击不误触、Rename 可靠打开。
   - https://github.com/anomalyco/opencode/pull/42453

6. **[#42455] 修复：从缺失位置恢复会话（已合入）**
   - 作者：kitlangton | 状态：CLOSED
   - 工作目录被删除时仍可恢复会话，无需启动损坏的 location runner；新会话避开不可用的继承位置；Tab 加号尊重 `session.new_location`。
   - https://github.com/anomalyco/opencode/pull/42455

7. **[#42456] 修复：隔离 Tab 滚动状态（OPEN）**
   - 作者：kitlangton | 状态：OPEN
   - 启用 `tab_scroll` 实验时，每个会话 Tab 保持独立的阅读位置，修复切换 Tab 时位置错乱的问题。
   - https://github.com/anomalyco/opencode/pull/42456

8. **[#38790] 功能：新布局中加入 Workspace 流程（已合入）**
   - 作者：Hona | 状态：CLOSED
   - 新会话可选择“本地仓库”“新建隔离工作区”或“已有工作区”；位置选择器显示分支上下文——V2 工作区流程的重大补全。
   - https://github.com/anomalyco/opencode/pull/38790

9. **[#42425] 功能：agent_memory 表 + memory-tools 插件（OPEN）**
   - 作者：herjarsa | 状态：OPEN
   - 新增 `agent_memory` 表与插件，支持通过 Supabase 云端备份/恢复 Agent 记忆。对长会话与跨设备工作流有直接价值。
   - https://github.com/anomalyco/opencode/pull/42425

10. **[#42443] 修复：改进 Tab 指针控制（OPEN）**
    - 作者：opencode-agent[bot] | 状态：OPEN
    - 为 Tab 上下文菜单添加终端尺寸的指针背景层；中键关闭 Tab 不触发拖拽或选中。附回归测试。
    - https://github.com/anomalyco/opencode/pull/42443

---

## 功能需求趋势

1. **V1 布局保留（#37012）**：V2 UI 信息密度下降，社区强烈要求可切换回旧版布局——目前是获得 👍 最多的 issue。
2. **本地/局域网模型发现（#27554、#19959）**：自动发现局域网内 OpenAI 兼容服务器并拉取模型列表，长期开放（自 5 月、3 月起），表明自托管需求的持续存在。
3. **TUI 可用性增强**：#42369（右侧栏显示后台 subagent 活动）、#42456（Tab 独立滚动）——社区在精细打磨 TUI 交互。
4. **多语言支持**：#42447（希伯来语）、#38033（印尼语 README）——国际化需求不断增长。
5. **V2 功能补齐**：#42421（V2 缺失 todo 工具）、#42439（V2 Build agent 状态恢复错误）——V2 相对 V1 仍有功能差距，迁移阻力明显。

---

## 开发者关注点

- **V1/V2 共存与数据兼容（#42260、#42444）**：V2 共享并迁移 V1 数据库造成实际损失，是当前最尖锐的矛盾。虽然修复已合入，但用户信任已受影响。
- **免费额度 429 误报（#42029、#42074、#42449、#42452）**：多条独立反馈指向同一问题——免费模型在未使用或刚恢复时立即被限流，且 VPN 轮换可绕过限制（#34344），服务端限流逻辑需紧急审查。
- **安全基线不足**：`opencode upgrade` 无校验执行远程脚本（#42434）、`webfetch` SSRF（#42435）且修复 PR 被关闭、上下文剪枝静默丢弃指令内容（#42437）——安全修复流程的响应速度需提升。
- **安装可靠性**：二进制自删（#42441）、桌面端启动加载失败（#40516）——基础安装链路的稳定性仍是高频痛点。
- **远程/容器场景支持**：VSCode Server 中剪贴板失效（#41470）、Windows 控制台窗口闪烁（#42440）——非标准环境下的体验打磨不足。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-14

> 数据来源：github.com/badlogic/pi-mono

---

## 今日速览

今日 Pi 社区焦点集中在大会话管理与终端卫生问题：`#6879` 自动压缩（auto-compaction）失效导致上下文溢出至 373k tokens 的严重 bug 持续发酵，成为社区最热议题；同时，一组由用户 `frankieyep` 提交的 TUI 终端状态恢复相关 PR（#8082）已成功修复"恢复大会话刷屏"和"SIGINT 后终端残留 raw mode"两个痛点。此外，扩展加载性能优化（#4254）与 Grok 4.6 模型支持（#8046）也于今日收官。

---

## 社区热点 Issues（Top 10）

### 1. #6879 — 自动压缩在上下文超限后从不触发，直至提供商拒绝请求
- **作者**: alexanderkreidich | **评论**: 19 | **👍**: 17
- **链接**: https://github.com/earendil-works/pi/issues/6879
- **要点**: 在 gpt-5.6-sol 上单次 agentic turn 运行超 2 小时，footer 越过压缩阈值后持续增长至 373k tokens，压缩仅在 API 报错时才触发。**这是当前社区反馈最强烈、影响面最广的稳定性问题**，建议每个 agent 步骤后检查上下文水位。

### 2. #7836 — Edit 模糊匹配因空白符长度差异而漏检
- **作者**: robjgray | **评论**: 10 | **👍**: 1
- **链接**: https://github.com/earendil-works/pi/issues/7836
- **要点**: `normalizeForFuzzyMatch` 未折叠连续空白或去除行首缩进，导致内容相同但空白不精确时 Edit 的 `oldText` 匹配失败。小模型在 edit 场景下出错率明显上升，已标记 inprogress。

### 3. #8029 — 大缓冲区下 prompt 编辑器移动光标性能极慢
- **作者**: affanali2k3 | **评论**: 7
- **链接**: https://github.com/earendil-works/pi/issues/8029
- **要点**: 7000 行 prompt 缓冲区中按一次方向键耗时 1650ms，性能随文本量线性恶化。已有对应 PR #8066 通过视觉行缓存解决。

### 4. #7779 — 可信 Unix 用户间共享 PI_CODING_AGENT_DIR 受限
- **作者**: AlecRosenbaum | **评论**: 5
- **链接**: https://github.com/earendil-works/pi/issues/7779
- **要点**: `auth.json` 与 `models-store.json` 以 0600 权限写入，首个创建者成为唯一读写方，多用户共享安装场景下后续进程无法访问共享状态。

### 5. #7829 — 无效 settings.json 被静默忽略；Windows 上误报"bash not found"
- **作者**: odafeng | **评论**: 5
- **链接**: https://github.com/earendil-works/pi/issues/7829
- **要点**: 未转义反斜杠的 Windows 路径导致 JSON 解析失败，但错误信息却指向 bash 缺失，误导排查方向。建议增强配置解析错误提示。

### 6. #7689 — Codex 后端需处理 `end_turn: false`
- **作者**: mitsuhiko | **评论**: 3 | **👍**: 2
- **链接**: https://github.com/earendil-works/pi/issues/7689
- **要点**: 某些 Codex 后端在 `response.completed` 中携带 `end_turn: false`，Pi 需要正确识别该语义，否则可能导致流程中断或状态不一致。

### 7. #7761 — TUI 复制显示"Copied!"但剪贴板为空（VTE 终端）
- **作者**: x1325990526 | **评论**: 3
- **链接**: https://github.com/earendil-works/pi/issues/7761
- **要点**: GNOME Terminal 等 VTE 终端上双选文本提示复制成功，但 `wl-paste` 验证剪贴板未变。根因是仅写入 OSC 52 序列而 VTE 默认不处理。

### 8. #8017 — 支持 Anthropic 服务端拒绝（refusal）回退机制
- **作者**: badlogic | **评论**: 2
- **链接**: https://github.com/earendil-works/pi/issues/8017
- **要点**: 当 Anthropic 分类器判定 Pi 操作"非法"时压缩可能失败，需实现官方 refusal fallback 机制（见 Claude Build with Claude 文档）。

### 9. #8041 — HTML 导出需渲染 Mermaid 与 LaTeX 以匹配 TUI 效果
- **作者**: aliou | **评论**: 2 | **👍**: 1
- **链接**: https://github.com/earendil-works/pi/issues/8041
- **要点**: 当前 HTML 导出通过 marked 渲染 Markdown，跳过 TUI 中的图表与公式转换，导出的图表/公式以原始源码呈现，体验降级。

### 10. #7607 — pi-agent-core：按工具粒度选择是否跳过参数校验
- **作者**: addoxyz | **评论**: 3
- **链接**: https://github.com/earendil-works/pi/issues/7607
- **要点**: 提出"提供商侧严格 schema + 工具侧宽松接收"的模式：宿主对受治理输出通道广播严格 schema 以改善模型生成质量，同时在工具侧接受超集并做归一化。需要 per-tool opt-out 机制。

---

## 重要 PR 进展（Top 10）

### 1. #8082 — [CLOSED] TUI 仅渲染可见视口；SIGINT 时恢复终端状态
- **作者**: frankieyep | https://github.com/earendil-works/pi/pull/8082
- **内容**: 双重修复：①恢复大会话时仅渲染可见视口，避免 759KB 会话回放 844KB 输出刷屏；②SIGINT 时正确恢复终端 raw mode、光标、括号粘贴与 Kitty 键盘协议，并还原窗口标题（关联 #7469、#8079、#8080）。

### 2. #8086 — [CLOSED] Gemini 工具 schema 回退至 legacy 格式
- **作者**: d33disc | https://github.com/earendil-works/pi/pull/8086
- **内容**: 部分 generativelanguage 端点拒绝 `parametersJsonSchema` 等新字段，本 PR 在端点报错时回退至 legacy Schema 消息格式，兼容旧端点。

### 3. #8084 — [CLOSED] 修复布尔扩展标志吞掉后续 prompt 参数
- **作者**: felixzsh | https://github.com/earendil-works/pi/pull/8084
- **内容**: 布尔扩展标志（如 `--plan`）的取值在扩展加载前不可知，旧逻辑将后续 CLI 参数误作为其值消费，导致 `pi -p --plan "prompt"` 无消息直接退出。此 PR 修正标志值消费逻辑。

### 4. #8066 — [OPEN] TUI 视觉行缓存，避免重复计算
- **作者**: affanali2k3 | https://github.com/earendil-works/pi/pull/8066
- **内容**: 修复 #8029：按宽度与文本内容缓存视觉行计算结果，大幅降低大缓冲区下光标移动延迟，并补充 `VisualLine` 类型定义。

### 5. #8070 — [OPEN] 校验扩展标志默认值
- **作者**: acmerfight | https://github.com/earendil-works/pi/pull/8070
- **内容**: `registerFlag()` 允许 `type` 与 `default` 不一致（如布尔标志默认 `"false"` 字符串被判真），本 PR 将选项建模为可辨识联合类型，导出 `ExtensionFlagOptions`，强制类型安全。

### 6. #7984 — [OPEN] 更新 grok-mermaid 至 0.2.3
- **作者**: xl0 | https://github.com/earendil-works/pi/pull/7984
- **内容**: 解决 #7832（grok-mermaid 类名解析问题）。升级后图表渲染不再需要额外的类定义，附带 before/after 对比图。

### 7. #8085 — [OPEN] TUI 支持 Escape 取消进行中的鼠标选择
- **作者**: pablasso | https://github.com/earendil-works/pi/pull/8085
- **内容**: 在 drag 选择过程中按 Escape 可取消选择且不触发自动复制，为误选用户提供反悔通道，对齐文本编辑器常规交互。

### 8. #8057 — [OPEN] 修复示例 todo 工具校验失败时 renderResult 崩溃
- **作者**: cyzlmh | https://github.com/earendil-works/pi/pull/8057
- **内容**: todo 工具校验失败时 `details` 为空对象（真值），renderResult 跳过所有分支后 `switch` 无 default 返回 `undefined`，导致 TUI 崩溃。补上默认分支兜底。

### 9. #6216 — [OPEN] 新增 Amazon Bedrock Mantle OpenAI Responses 提供商
- **作者**: unexge | https://github.com/earendil-works/pi/pull/6216
- **内容**: 基于 OpenAI Bedrock Provider 实现 Amazon Bedrock Mantle 的 OpenAI Responses API 接入，扩展 AWS 生态下的模型选项。

### 10. #8067 — [CLOSED] 用户可见消息统一使用 APP_NAME
- **作者**: mellson | https://github.com/earendil-works/pi/pull/8067
- **内容**: 多处用户面向字符串硬编码 "pi"，改为读取 `APP_NAME` 配置（默认回退 "pi"），保证 rebrand 场景下品牌一致性。

---

## 功能需求趋势

| 方向 | 代表 Issue / PR | 热度 |
|------|----------------|------|
| **会话稳定性 / 上下文管理** | #6879（压缩失效）、#7993（工具回合间压缩）、#8017（refusal 回退） | 🔥🔥🔥 |
| **终端卫生 / TUI 体验** | #8082（SIGINT 恢复）、#8085（Esc 取消选择）、#7761（剪贴板）、#8055（CJK 宽度对齐） | 🔥🔥🔥 |
| **性能优化** | #8029（编辑器卡顿）、#4254（扩展加载提速）、#7739（启动预算对标 jcode） | 🔥🔥🔥 |
| **新模型 / 新提供商支持** | #8046（Grok 4.6）、#6216（Bedrock Mantle）、#8083（Qwen3.8 命名漂移） | 🔥🔥 |
| **配置健壮性与权限模型** | #7829（Windows 配置解析）、#7779（共享目录权限）、#8070（标志默认值校验） | 🔥🔥 |
| **导出与渲染一致性** | #8041（HTML 导出 Mermaid/LaTeX） | 🔥 |

---

## 开发者关注点

1. **上下文超限无预警**：`#6879` 暴露核心痛点——压缩机制在长 agentic turn 中触发太晚，开发者希望每个工具调用步骤后主动检查上下文水位，而非依赖提供商硬性拒绝。
2. **终端不可恢复**：SIGINT / `/exit` 后终端残留 raw mode、Kitty 协议未复位等问题频发（#8080、#5065），说明信号处理与终端状态机需要系统级加固，而非逐个 patch。
3. **Windows 支持仍是短板**：Unix socket 绑定失败（#8047）、JSON 转义解析误导（#7829）等问题集中出现，跨平台一致性测试有待加强。
4. **大会话恢复体验差**：`/resume` 进度计数口径不一致（#7960）、恢复时全量回放刷屏（#8079）——大项目日常使用中恢复会话是高频路径，体验优化优先级应提高。
5. **扩展系统类型安全**：多个 PR（#8070、#8084）聚焦扩展标志类型校验与 CLI 参数消费，反映社区对扩展 API 类型约束的刚性需求。
6. **现网 / 旧模型兼容性**：Gemini 端点拒绝新 schema（#8086）、Codex `end_turn` 语义（#7689）、Kimi 缓存字段解析（#8075）——多提供商适配仍是日常维护主要工作。

---

> 日报生成时间：2026-08-14 | 数据覆盖：过去 24 小时 GitHub 活动

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-14

## 今日速览

Qwen Code 发布 v0.21.11 正式版，带来 Agent Plugins v1 与原生多智能体 `/coordinate` 命令两项重磅能力；同时 v0.21.12-preview.1 预览版发布，聚焦 Web Shell 会话与文件上传。社区侧，多智能体 fleet 架构系列 PR 密集推进，SWE-bench Verified 基准状态被标记为 QUARANTINED，Windows 平台 Ctrl+V 粘贴回归问题引发高关注。

---

## 版本发布

### v0.21.11（正式版）

**核心亮点：**
- **Agent Plugins v1**：支持通过插件扩展 Agent 能力（[#8834](https://github.com/QwenLM/qwen-code/pull/8834)）
- **原生多智能体工作流**：新增 `/coordinate` 命令，支持只读 teammates 协作（[#8804](https://github.com/QwenLM/qwen-code/pull/8804)）

### v0.21.12-preview.1（预览版）

- fix(web-shell): 保留独立会话目标（[#9038](https://github.com/QwenLM/qwen-code/pull/9038)）
- feat(web-shell): 支持工作区文件上传

> ⚠️ **SWE-bench Verified 状态：QUARANTINED** — v0.21.11 基准验证 500/500 全部未通过（0 resolved），当前版本已暂停发布，需关注后续修复。

---

## 社区热点 Issues（TOP 10）

### 🔥 高热度

**1. [#8718 RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)**
- 多智能体协调的纲领性 RFC，leader 可调度多个独立 worker 并保持交互。
- 9 条评论，**fleet 系列 5 个 stage issue 均挂靠于此**，是当前社区最核心的方向。

**2. [#8678 fix(serve): Preserve the current session when a large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)**
- 大会话恢复超时导致当前会话丢失，P1 严重性。
- PR1（#8691）已合并实现超时契约与可观测性，恢复路径仍需跟进。

**3. [#9061 Ctrl+V paste completely unresponsive in CLI on Windows — regression since 0.21.x](https://github.com/QwenLM/qwen-code/issues/9061)**
- Windows CLI 粘贴功能在 0.21.x 回归失效（0.21.0 可用），P1 级别。
- 仅 3 条评论，但属于高频操作阻断性 bug，影响所有 Windows 用户。

**4. [#7118 Windows standalone installer fails when powershell.exe cannot resolve Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)**
- Windows 安装器因 `Get-FileHash` 解析失败导致 SHA-256 校验崩溃，👍 3。
- 持续近一个月仍未修复，欢迎 PR 贡献。

### 👀 值得关注

**5. [#9019 Gemini 2.5 models are unusable on Vertex AI: thinkingLevel is always sent](https://github.com/QwenLM/qwen-code/issues/9019)**
- Vertex AI 上 Gemini 2.5 完全不可用——`thinkingLevel` 字段恒被发送，即使是不支持的占位值，直接 400 报错。

**6. [#9025 Keyless Vertex AI is not inferred from the environment](https://github.com/QwenLM/qwen-code/issues/9025)**
- 纯环境变量配置的 keyless Vertex AI 无法自动识别认证类型，headless 运行启动即退出。与 #9019 同作者，Vertex AI 生态问题集中爆发。

**7. [#9002 SDK Python rejects permission_mode="auto" although the CLI supports it](https://github.com/QwenLM/qwen-code/issues/9002)**
- Python SDK 客户端校验拒绝 `permission_mode="auto"`（CLI 支持），阻塞 SDK 自动化流程。

**8. [#9083 record_artifact succeeds without verifying workspacePath](https://github.com/QwenLM/qwen-code/issues/9083)**
- `record_artifact` 不校验 `workspacePath` 即返回成功，导致 artifact 状态为 `missing` 但文件实际存在，模型误导用户后可打开。

**9. [#9088 read_file sends non-image file to model API based only on .png extension](https://github.com/QwenLM/qwen-code/issues/9088)**
- 仅凭扩展名 `.png` 将非图片文件（实际为 UTF-8 JSON）发送至模型 API，触发 400 中断整个 turn，headless 环境受影响。

**10. [#9108 Desktop: remaining Web Shell external links can still fail to open silently; MCP OAuth cannot complete](https://github.com/QwenLM/qwen-code/issues/9108)**
- #9069 修复了 Markdown 消息外链，但其余 4 个链接面仍静默丢失，MCP OAuth 流程因此无法完成。

---

## 重要 PR 进展（TOP 10）

### 🚀 多智能体 Fleet（核心方向）

**1. [#9106 feat: consolidate Local Control into one daemon-owned implementation](https://github.com/QwenLM/qwen-code/pull/9106)**
- Local Control（手机 LAN 配对）目前有两种语言、两套安全模型的重复实现，统一收敛到 daemon 单实现。

**2. [#8971 feat(core): write per-agent transcripts for workflow dispatches](https://github.com/QwenLM/qwen-code/pull/8971)** ✅ 已合并
- workflow `agent()` 调度现在生成与 Agent 工具一致的 per-agent JSONL transcript。

**3. [#9034 feat(core): expose workflow execution state](https://github.com/QwenLM/qwen-code/pull/9034)**
- 为 Workflow 执行增加结构化可观测模型：run/step 生命周期事件、journal 持久化、快照重建、取消与保留原语。

**4. [#9098 feat(cli): enable dynamic workflows from a settings key](https://github.com/QwenLM/qwen-code/pull/9098)**
- 新增 `tools.workflowsEnabled` 设置项正式启用动态 workflows，替代原来的环境变量开关。

### 📝 Review 管线强化

**5. [#9086 fix(review): harden the pipeline against four live-run failures](https://github.com/QwenLM/qwen-code/pull/9086)**
- 针对 3 个真实 PR（#9013、#9014、#9045）端到端运行发现的 4 个缺陷逐一修复，并配回归测试。全部为实测非假设。

**6. [#9092 feat(review): resume an interrupted PR review from its on-disk state](https://github.com/QwenLM/qwen-code/pull/9092)**
- `fetch-pr --resume` 基于磁盘状态恢复中断的 review：校验 previous report、worktree SHA、diff 哈希一致性。

**7. [#9093 feat(review): wire --resume through /review, review run and the CI retry](https://github.com/QwenLM/qwen-code/pull/9093)**
- `--resume` 贯通所有入口：`/review` 参数语法、`review run`、CI retry。

**8. [#9091 feat(review): run-session ledger and cross-session agent evidence](https://github.com/QwenLM/qwen-code/pull/9091)**
- 引入 run-sessions ledger 记录 CLI session id，plan 增加 diff bytes SHA-256 印章，为恢复机制打地基。

### 🛠️ 修复与优化

**9. [#9111 fix(desktop): open remaining external links through the shell opener](https://github.com/QwenLM/qwen-code/pull/9111)**
- 修复 #9108：将剩余 4 个链接面全部路由至 capability-scoped Tauri opener，不再依赖隐式 new-window。

**10. [#8938 feat(core): reject upstream fail-fast placeholder responses](https://github.com/QwenLM/qwen-code/pull/8938)**
- 防御上游模型端 fail-fast 行为：HTTP 200 + 正常 finish reason 但响应体仅为占位文本 `(request timed out)` 的情况，增加两道防线。

### 其他值得关注

- **#9104** feat(autofix): 非收敛 diff 升级为维护者人工介入，避免无限打补丁
- **#9100** feat(review): `fetch-pr --since <sha>` 增量评审锚点校验
- **#8996** feat(autofix): 按内容而非作者判定 review 反馈有效性
- **#9096** feat(review): 将 prompt 中裸 `gh` 命令收敛为 platform-backed 子命令

---

## 功能需求趋势

| 方向 | 热度 | 代表 Issue/PR |
|---|---|---|
| **多智能体 / Fleet** | 🔥🔥🔥 | #8718（RFC umbrella）、#8840-8843（stage 1A-3）、/coordinate 命令 |
| **Web Shell 能力补全** | 🔥🔥 | 文件上传（#9038）、Channel/workspace 管理（#8845）、外链修复（#9108、#9111） |
| **工作流（Workflow）** | 🔥🔥 | 动态启停（#9098）、执行状态可观测（#9034）、transcript（#8971） |
| **Review / 自动化治理** | 🔥🔥 | resume 机制（#9092/93）、evidence 捕获（#8894）、增量锚点（#9100） |
| **认证与多云适配** | 🔥 | Vertex AI keyless 推断（#9025）、Gemini thinkingLevel 兼容（#9019） |
| **内存 / 记忆系统** | 🔥 | omni S5a/S5b（#8188/8189）、pinned/ 只读保护（#6801） |

---

## 开发者关注点

**痛点反馈：**

1. **Windows 平台问题集中**：Ctrl+V 粘贴回归（#9061）、安装器 SHA-256 校验失败（#7118）、Desktop 可见 Terminal 窗口（#9043，已关闭）——Windows 体验是当前最集中的质量短板。
2. **无头（headless）环境稳定性**：`NO_TOOL_RESULT_PROGRESS` 硬失败（#9026）、keyless 认证推断缺失（#9025）、非 PNG 文件误发模型 API（#9088）——无头自动化场景频遭障碍。
3. **SDK 与 CLI 能力不对齐**：Python SDK 拒绝 `permission_mode="auto"`（#9002），自动化链路被客户端校验阻断。

**社区情绪：**

- 多智能体方向获得压倒性关注，fleet 系列 issue 在 3 天内完成 stage 1A→3 全部规划并持续推进，社区认可度高。
- Review 管线自动化迭代积极（resume、evidence、增量评审），但对 `wenshao` 单人多 PR 推进的 review 基础设施存在一定的维护集中风险。
- SWE-bench Verified 隔离状态（QUARANTINED）值得警惕，v0.21.11 的发布质量验证存在缺口，社区应关注后续修复版本。

---

*数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) | 更新于 2026-08-14*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-14

> 数据来源：Hmbown/CodeWhale GitHub 仓库

## 今日速览

**v0.9.7 正式发布**，CodeWhale 品牌化落地，主命令更名为 `codewhale`，旧 `deepseek-tui` npm 包进入弃用状态。与此同时，v0.9.8 的开发工作已全面铺开：Auto-Review 双层架构（确定性层 + 模型守卫层）进入 PR 阶段，DS4 本地推理路由成为一等公民，EPIC-005（TUI crate 分解重构）正在推进。社区侧，中文输入法适配（#2323，👍 1）与多行输入模式（#5345）成为最新热议方向，i18n 覆盖和 Windows 终端体验持续被关注。

## 版本发布

**v0.9.7**（过去 24 小时）

- **重要变更**：公共产品正式命名为 **CodeWhale**（Shannon Labs 出品）。CLI 命令统一为 `codewhale`，npm 包名及发布产物同步更名（保持小写技术标识）。
- **弃用通知**：旧 npm 包 `deepseek-tui` 已弃用，不再接收后续更新。自 v0.8.x 升级的用户需迁移至 `codewhale` 命令。

## 社区热点 Issues

1. **#5324 — agent 工具 32 字段 schema 导致模型报错**
   [链接](https://github.com/Hmbown/CodeWhale/issues/5324) | 评论 7
   `agent` 工具的 JSON schema 高达 32 个属性且零必填字段，同时承载 8 种动作（start/status/peek 等），运行时还接受别名。模型频繁出错，社区已在 PR #5369 中提交 schema 降级方案，是本周期最受关注的架构合理性议题。

2. **#5340 — doctor 命令升级后卡在 `needs action` 状态**（[bug] [0.9.6]）
   [链接](https://github.com/Hmbown/CodeWhale/issues/5340) | 评论 2
   v0.9.4 升级至 v0.9.6 后，`codewhale doctor` 的 `first-run` 和 `update checkpoint` 永久卡死在 `needs action`，即使重新走完首次引导也无法消除。升级路径的幂等性问题，直接影响用户信任度。

3. **#5359 — 四个 TUI 测试在开发机确定性失败，CI 却保持绿色**
   [链接](https://github.com/Hmbown/CodeWhale/issues/5359) | 评论 2
   测试读取 `~/.codewhale` 真实状态，导致本地与 CI 环境行为不一致，测试隔离性不足。PR #5368 已提交三个独立修复机制，各配回归测试。

4. **#2369 — CodeWhale 配置路径跨 OS/Cygwin 碎片化 + 静默迁移 Bug**
   [链接](https://github.com/Hmbown/CodeWhale/issues/2369) | 评论 7
   Windows 与 Cygwin 下配置/密钥路径解析规则不一致，旧版本迁移还会静默产生错误地址。跨平台路径可靠性问题，长期悬而未决。

5. **#998 — 文案展示不全，悬停希望能显示完整提示**
   [链接](https://github.com/Hmbown/CodeWhale/issues/998) | 评论 11 | 👍 1
   界面文字截断无 Tooltip 兜底，社区呼声较高，已请求鼠标悬停显示完整内容的增强。属于典型的 TUI 可用性细节。

6. **#1425 — 大文本处理（300 万字小说）后会话中断卡死**
   [链接](https://github.com/Hmbown/CodeWhale/issues/1425) | 评论 6
   10 个子 Agent 并行分批处理，但 `agent_wait` 超时导致会话卡死。多 Agent 编排的超时策略与恢复机制不足，高负载场景下的稳定性痛点。

7. **#1829 — SSH 连接失败 exit code 255（疑似沙箱 TCP 22 出站阻断）**
   [链接](https://github.com/Hmbown/CodeWhale/issues/1829) | 评论 5
   内置 shell 沙箱可能屏蔽了 22 端口出站，本地终端正常但 TUI 内 SSH/SCP 全部失败。沙箱网络策略需进一步文档化或配置化。

8. **#1004 — `/dryrun` 命令：预览请求而不实际发送**
   [链接](https://github.com/Hmbown/CodeWhale/issues/1004) | 评论 9
   长上下文（V4 Pro 系统提示词 + 缓存文件 + 工具定义）下开发者看不到即将发送的内容，造成调试成本。dryrun 功能需求明确，讨论热度领先。

9. **#894 — 执行过程中图片显示混乱**
   [链接](https://github.com/Hmbown/CodeWhale/issues/894) | 评论 6
   截图展示了渲染布局缺陷。TUI 对图片/多模态内容的渲染管线不稳定，影响含图表输出场景的可用性。

10. **#1651 — YOLO Agent 运行测试脚本时 VS Code 崩溃/意外退出**
    [链接](https://github.com/Hmbown/CodeWhale/issues/1651) | 评论 5
    在 VS Code 集成终端中运行，YOLO Agent 后台执行测试时导致编辑器崩溃。Agent 自主执行场景下 VS Code 扩展的稳定性隐患。

## 重要 PR 进展

1. **#5353 — Auto-Review 模型守卫层（v0.9.8）** ([OPEN](https://github.com/Hmbown/CodeWhale/pull/5353))
   Auto-Review 升级为双层架构：确定性层不可绕过，兜底时升级为一次性模型守卫而非静默阻断。融合 Codex reviewer 语义 + Kimi 模式词汇，Codewhale 默认 fail-closed。

2. **#5358 — 自动审核拒绝理由 + 回合熔断器** ([CLOSED](https://github.com/Hmbown/CodeWhale/pull/5358))
   修复 `permission_denied` 裸返回导致模型重复尝试同一动作直至预算耗尽的问题。`AutoReviewPlanDecision::Block` 现在附带拒绝理由，配合熔断机制节省 step 预算。

3. **#5365 — DS4 一等本地路由设置** ([OPEN](https://github.com/Hmbown/CodeWhale/pull/5365))
   `/setup provider ds4` 与 provider-picker 的 `D` 快捷键一键进入 DwarfStar 预填 keyless 回环预设。复用 OpenAI 兼容传输层，DeepSeek 推理控制项开箱即用。

4. **#5368 — 将无防护测试隔离到独立状态根目录** ([OPEN](https://github.com/Hmbown/CodeWhale/pull/5368))
   修复 #5359 中四个读取 `~/.codewhale` 的测试。三个独立机制（锁持有者信任漏洞、路径候选、显示探针）各配专属回归测试。

5. **#5369 — Moonshot schema 降级替代拒绝条件** ([OPEN](https://github.com/Hmbown/CodeWhale/pull/5369))
   回应 #5324：发送 schema 切片，对条件字段采取降级策略而非直接拒绝，净负反馈优化。

6. **#5339 — 抑制子进程 shell 完成事件** ([OPEN](https://github.com/Hmbown/CodeWhale/pull/5339))
   修复 #5325：子 Agent 拥有的后台 shell 完成事件被过滤，不再混入父模型流；同时保留无主完成事件与任务/状态可见性。

7. **#5364 — TUI 渲染 Markdown 引用条（quote rail）** ([CLOSED](https://github.com/Hmbown/CodeWhale/pull/5364))
   `>` 引用行渲染为带引号轨道的样式，支持嵌套、内联格式、换行与选区复制。由社区开发者 SparkofSpike 提交。

8. **#5333 — 宿主终端窗口画中画（PiP）固定** ([CLOSED](https://github.com/Hmbown/CodeWhale/pull/5333))
   收割社区 PR #5318（SparkofSpike）：右键菜单或 `/pin` 命令将终端窗口缩至 640x400 并置顶，再次触发恢复。维护者手动合入以解决原 PR 的 CI 失败问题。

9. **#5336 — MCP 修复：无下一页时省略 nextCursor** ([CLOSED](https://github.com/Hmbown/CodeWhale/pull/5336))
   修复 #5335：`tools/list` 与 `resources/list` 不再返回 `"nextCursor": null`，符合 MCP 规范（字段须为字符串或缺失），Claude Code 等严格客户端的兼容性修复。

10. **#5354 — 刷新 CI 源结构预算** ([CLOSED](https://github.com/Hmbown/CodeWhale/pull/5354))
    #5348 合并时遗漏预算提交，导致 main 分支 Lint gate 失败。刷新预算以解除所有贡献者 PR 的阻塞。

## 功能需求趋势

- **可配置输入键位**（#5345 多行模式、#436 可配置 keymap）：用户期望像 Grok Build/Codex 一样支持 `multiline` 模式，自定义 `enter`/`shift+enter` 发送组合；输入框需支持简易 Markdown 结构化编写。
- **模型上下文可视性**（#1004 `/dryrun`）：长提示词 + 多工具定义场景下，开发者需要"发送前预览"能力。
- **本地模型 / 自托管路由**（#5365 DS4、#5367 大小限制可配置、#1482 NVIDIA NIM）：用户需要本地/第三方推理后端的一等配置体验，而非手动翻译为通用 provider。
- **TUI 文本与输入体验**（#2323 中文输入法、#790 i18n 覆盖、#998 Tooltip）：非英语用户的输入法兼容与文案完整性问题持续升温，i18n 覆盖范围从核心 UI 扩展至命令与弹窗。
- **远程工作台 / 多基础设施**（#1990 US-first 云通道、#1984 CNB/Lighthouse/Feishu 一体化）：现有腾讯生态路径已成熟，社区开始要求 AWS/Cloudflare/Telegram 等美系通道，并追求跨平台统一体验。
- **架构治理**（#5324 schema 瘦身、#5316 crate 分解、#5353 Auto-Review 双层）：当功能膨胀到一定规模，社区开始关注 schema 简洁性、模块边界与权限分层。

## 开发者关注点

- **升级路径与版本迁移仍是最大痛点**：#5340 doctor 卡死、#2369 静默配置迁移、#1732 报告保存性能倒退，均与 v0.8 → v0.9 的架构调整直接相关。品牌更名（`deepseek-tui` → `codewhale`）虽已公告，但存量用户的迁移摩擦明显。
- **多 Agent 编排的工程化短板**：#1425 子 Agent 超时卡死、#5339 子进程事件串流，说明 Agent 生命周期管理与事件隔离尚未成熟。
- **测试环境一致性**：#5359 本地失败/CI 绿色的问题暴露了测试对真实机器状态的隐式依赖，开发者在本地贡献代码时容易踩坑。
- **Windows 是重灾区**：#1829 SSH 阻断、#1854 默认终端体验差、#894 图片渲染混乱、#2323 中文输入法 — Windows 平台问题占社区反馈近半。
- **安全模型与应用集成张力**：#1651 VS Code 崩溃、#5356 角色门控过严（只读角色完全禁用 bash）、#1917 PreToolUse/PostToolUse Hook 提议，反映 Agent 自主性需要更细粒度的可配置安全边界。

> 本文由 AI 技术分析师根据 GitHub 公开数据自动生成，仅供社区参考。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*