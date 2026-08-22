# AI CLI 工具社区动态日报 2026-08-22

> 生成时间: 2026-08-22 00:29 UTC | 覆盖工具: 9 个

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

**报告日期：2026-08-22** | **数据来源：GitHub 社区公开动态**


## 1. 生态全景

AI CLI 工具赛道正从"demo 可用"迈向"生产可用"的攻坚阶段。各工具社区当前最集中的反馈并非新功能缺失，而是**稳定性与可观测性**——Claude Code 的 AUP 误报、Codex 的 Windows 远程连接故障、Gemini CLI 的子代理假成功、Copilot CLI 的 BYOK 切换限制，均指向同一个核心诉求：**工具需要在无人值守、长时运行、企业合规等真实生产场景中值得信赖**。与此同时，安全加固（沙箱隔离、权限审查、CVE 审计）和基础设施能力（MCP 生态、插件系统、多模型支持）成为各家的共同投入方向。


## 2. 各工具活跃度对比

| 工具 | 今日活跃 Issues | 新增/更新 PRs | Release/版本 | 社区热度信号 |
|------|-----------------|---------------|-------------|-------------|
| **Claude Code** | 10+（含批量 AUP 误报，~8 个同源 Issue） | 0（24h 内无更新） | v2.1.239（正式版） | 高：AUP 误报批量提交成焦点 |
| **OpenAI Codex** | 10+（Remote 故障集群：8 个相关 Issue） | 10+（Guardian/沙箱/插件方向） | 6 个 alpha（0.149 → 0.150） | ⚠️ 极高：24h 内 6 个 alpha，迭代极快 |
| **Gemini CLI** | 10+（子代理/内存系统为主） | 10+（PR 生成流水线/安全修复） | v0.56.0-nightly | 高：维护团队响应迅速的修复闭环 |
| **Copilot CLI** | 10+（41 条总更新；BYOK 双高赞） | 0（24h 内无更新） | v1.0.81-7（正式版） | 中高：BYOK 需求持续霸榜 |
| **Kimi Code** | 1 | 1（文档类） | 无 | 低：样本最小，社区活跃度有限 |
| **OpenCode** | 10+ | 10+（Fork 一致性/登录 URL 修复） | v1.18.21、v1.18.20（补丁版） | 中：响应中断问题集中反馈 |
| **Pi** | 10+（50 条总更新） | 9（6 个已合并/关闭） | 无 | 中高：压缩机制讨论热烈 |
| **Qwen Code** | 10+ | 10+（review 工具链） | v0.21.14-nightly | 中：安全 review 密集但用户侧反馈分散 |
| **DeepSeek TUI** | 10+（含 5 个监督化系列） | 7+（含 1 个大型 PR） | 无 | 低：维护者主导，社区参与度偏低 |

*注：活跃度基于日报中筛选出的 Top Issues/PRs 数量及讨论热度综合判断。*


## 3. 共同关注的功能方向

### 3.1 会话/任务生命周期管理（跨 6+ 工具）
| 工具 | 具体诉求 |
|------|---------|
| **Claude Code** | 系统事件伪装为 user 消息导致虚构授权 |
| **Codex** | 配额在轮询/等待时被重复消耗 |
| **Gemini CLI** | 子代理 MAX_TURNS 被误报为 GOAL 成功；通用代理挂起 |
| **Copilot CLI** | 会话崩溃后自动恢复（v1.0.81-7 已实现） |
| **Kimi Code** | 后台子代理在 TaskStop/timeout 后仍消耗 LLM 配额 |
| **Pi** | 压缩触发时机过晚，上下文超限才触发 |

### 3.2 子代理/多代理可靠性（跨 5+ 工具）
Gemini CLI 的"挂起+假成功"、Kimi Code 的"终止后仍消耗配额"、DeepSeek TUI 的"墙钟超时丢失工作"、OpenCode 的"多子代理 TUI 卡顿"、Qwen Code 的"12 小时长会话崩溃"——**子代理的状态管理和资源释放是行业级难题**。

### 3.3 多模型/BYOK 管理（跨 4+ 工具）
Copilot CLI（#3709/27👍、#3282/26👍）呼声最集中；Codex 自定义 Provider 下 subagent 不可用；Pi 按模型配置压缩策略；Qwen Code 的 OpenAI 兼容端点混合思考模型兼容性。

### 3.4 MCP 生态稳定性（跨 4+ 工具）
Codex 的 tool result 解码失败、Copilot CLI 的 MCP 服务器不可达误报、Qwen Code 的 Windows MCP 连接关闭、OpenCode 的 Bun fetch 空闲超时——MCP 已从"新奇功能"变成"依赖的基础设施"，但可靠性仍未达标。

### 3.5 安全/合规（跨 4+ 工具）
Claude Code 的 AUP 误报批量报告、Codex 的 Guardian 审查整合（5+ PR）、Qwen Code 的 CVE 审计阻塞 + 权限分类器 fail-open、Gemini CLI 的 macOS Seatbelt 沙箱逃逸修复、DeepSeek TUI 的索引隐私控制。


## 4. 差异化定位分析

| 工具 | 核心定位 | 技术路线 | 目标用户 |
|------|---------|---------|---------|
| **Claude Code** | **企业级合规 Agent**：深度绑定 Claude 模型，强调安全审查与组织治理 | 闭源，聚焦 AUP/合规策略 | 企业团队、合规敏感型组织 |
| **OpenAI Codex** | **全能型 Agent 平台**：Rust 重写（性能优先），高频迭代，安全审查体系化 | 开源（Rust），Guardian 安全层 + 细粒度沙箱 | 高性能需求、早期采用者 |
| **Gemini CLI** | **Google 生态 Agent 框架**：Agent Skills/子代理为核心，工具链完整 | 开源（TypeScript），A2A 协议、Seatbelt 沙箱 | Google Cloud 开发者、多代理编排场景 |
| **GitHub Copilot CLI** | **IDE 交互延伸**：ACP 协议对接外部工具，强调与 GitHub 生态的深度绑定 | 闭源，ACP/MCP 协议 + BYOK | GitHub 重度用户、IDE 集成场景 |
| **Kimi Code** | **轻量专注型 Agent**：Moonshot AI 模型配套，社区刚起步 | 开源，插件机制、后台子代理 | Kimi 模型用户、轻量使用场景 |
| **OpenCode** | **开源开放型 CLI**：Effect-TS 技术栈，Console/Desktop/TUI 多端 | 开源（TypeScript/Effect），多 Provider 支持 | 多模型工作流、拥抱开源的开发者 |
| **Pi** | **独立开发者效率工具**：单仓库（pi-mono），个人开发者友好 | 开源，Node.js，终端优先 | 个人开发者/独立黑客 |
| **Qwen Code** | **中文社区 + CI/CD 深度融合**：Auto-fix、review 工具链自举 | 开源（TypeScript），多频道集成（钉钉等） | 中文开发者、CI 自动化场景 |
| **DeepSeek TUI** | **极客向终端工具**：Rust 重写（TUI 优先），外部命令形态演进 | 开源（Rust），crate 分解中 | Rust 社区、轻量级 TUI 爱好者 |

**关键差异化维度：**
- **生态绑定度**：Claude Code / Kimi Code 深度绑定自家模型；Codex / Gemini CLI / Qwen Code 支持多 Provider；Copilot CLI 处于中间态（BYOK 已支持但模型切换受限）
- **开放程度**：OpenCode / Gemini CLI / Qwen Code 对第三方集成最开放（多 Provider + 插件 + 多端）；Claude Code 最封闭
- **企业/个人取向**：Claude Code（合规管理）、Codex（沙箱/Guardian）、Qwen Code（安全 review）→ 企业化；Pi（个人效率）、DeepSeek TUI（极客工具）→ 个人化


## 5. 社区热度与成熟度

**成熟稳定型（正式版为主，社区反馈回归理性）**
- **Claude Code**：社区活跃但聚焦明确痛点（AUP 误报），版本节奏稳健（正式版发布），已进入企业采纳期的"合规打磨"阶段
- **Copilot CLI**：依托 GitHub 生态，社区关注点集中在功能扩展（BYOK/会话管理），发布节奏温和

**快速迭代型（高频版本发布，功能/稳定性攻坚）**
- **OpenAI Codex**：24h 内 6 个 alpha，频率全场最高。社区高度活跃但问题爆发密度极大（Remote 集群故障），属于"快速试错-快速修复"的激进迭代模式
- **Gemini CLI**：维护团队响应极快（当日修复 symlink 问题、24h 内关闭安全 PR），社区讨论与代码修复形成正反馈闭环
- **OpenCode**：补丁版本密集（2 天内 2 个版本），修复方向明确（响应中断），但社区对新回归（v1.18.21 的续写问题）的容忍度在降低

**发展中型（社区增长但基础设施仍不完善）**
- **Qwen Code**：社区活跃度中等，安全 review 投入显著但用户侧需求回应较慢（长会话崩溃 2 个月未关闭）
- **Pi**：社区讨论质量高（有 870 次试验的成本对比），但关键功能（压缩触发）持续未修复

**起步型（社区规模小，维护者主导）**
- **Kimi Code**：社区活跃度低（24h 仅 1 Issue 1 PR），处于早期用户积累阶段
- **DeepSeek TUI**：维护者投入密集（5 个同源 Issue + 1 个大型 PR），但外部贡献者参与度有限


## 6. 值得关注的趋势信号

### 📌 信号一：安全体系已成为差异化竞争的核心
Claude Code 的 AUP 误报、Codex 的 Guardian 审查层（5+ PR 集中推进）、Qwen Code 的 review 工具链（4+ PR）、Gemini CLI 的沙箱逃逸修复——各大工具正在将安全能力从"外挂补丁"升级为"内建架构"。**对开发者**：选择工具时安全策略的灵活性（Claude Code 的 AUP 误报说明过度严格的安全策略反而是负担）与可配置性（Codex 的细粒度 sandbox_approval）比"严格程度"更重要。

### 📌 信号二：MCP 生态正经历"基础设施化"阵痛
MCP 已从创新功能变成默认依赖，但连接稳定性（Codex/Qwen Code）、超时处理（OpenCode）、错误诊断（Copilot CLI 的误导性 waiting on ide）等问题频发。**对开发者**：多工具使用 MCP 时，需要关注各工具对 MCP 服务器故障的容错能力；此阶段 MCP 的成熟度仍不足以承担关键生产路径。

### 📌 信号三：BYOK/多模型工作流成为刚性需求
Copilot CLI 的双高赞 Issue、Codex 自定义 Provider 的持续诉求、Qwen Code 的 OpenAI 兼容端点问题——单一的模型绑定正在成为用户流失的潜在因素。**对开发者**：评估工具时，多模型切换的灵活性（配置与运行时切换）应作为关键选型维度。

### 📌 信号四：无人值守/监督化运行是下一个战场
DeepSeek TUI 的"监督化操作栈"（生命周期 outbox、控制套接字、`/relaunch`）、Codex 的配额消耗透明化诉求、Gemini CLI 的 Auto Memory 后台任务——工具正从"交互式对话"向"可编程、可审计的代理运行平台"演进。**对开发者**：若计划将 AI CLI 集成到 CI/CD 流水线，需关注事件导出、外部控制、可恢复性等能力，DeepSeek TUI 的监督化栈和 Codex 的 Guardran 审查取消传播值得密切关注。

### 📌 信号五：前端/终端体验的"最后一公里"问题仍待解决
GitHub Copilot CLI 的 Windows PowerShell 弹窗、Qwen Code 的 Windows IME 失效、Pi 的跨终端 Backspace 问题——Linux/macOS 之外的终端兼容性仍是一级体验短板。**对开发者**：Windows 用户在选择工具时需对终端/键盘兼容性做额外验证。


### 给技术决策者的建议

| 场景 | 推荐工具 | 理由 |
|------|---------|------|
| 企业合规严苛、团队已用 Claude 模型 | **Claude Code** | 合规体系最完善，但需关注 AUP 误报修复进度 |
| 追求最强性能、拥抱快速迭代 | **OpenAI Codex** | Rust 实现性能领先，但需容忍 Remote 等功能不稳定的风险 |
| Google Cloud 生态、多代理编排 | **Gemini CLI** | Agent Skills/子代理框架最成熟，维护团队响应快 |
| GitHub 深度用户、IDE 集成优先 | **Copilot CLI** | 与 GitHub 生态集成最深，BYOK 灵活性正在增强 |
| 开源优先、多模型自由切换 | **OpenCode / Qwen Code** | 多 Provider 支持完善，社区生态开放 |
| 轻量使用、单模型够用 | **Kimi Code / Pi** | 简单直接，但社区生态和基础设施尚不成熟 |

---

*报告基于 2026-08-22 各工具 GitHub 社区公开动态生成，数据截至报告日期。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-22）

## 1. 热门 Skills 排行

| 排名 | Skill / PR | 核心功能 | 社区讨论热点 | 状态 |
|------|-----------|---------|-------------|------|
| 1 | **skill-creator 质量修复** ([#1298](https://github.com/anthropics/skills/pull/1298)) | 修复 eval 系统始终报告 0% recall 的严重缺陷 | 评价循环在单变量噪声上做优化，导致 skill 描述优化完全失真；Windows 兼容性问题突出 | OPEN |
| 2 | **document-typography** ([#514](https://github.com/anthropics/skills/pull/514)) | AI 生成文档的排版质量控制：孤儿词换行、孤行标题、编号对齐 | 直击 AI 生成文档的普遍痛点，用户很少主动要求好的排版，但问题客观存在 | OPEN |
| 3 | **docx 跟踪修订修复** ([#541](https://github.com/anthropics/skills/pull/541)) | 修复 DOCX skill 添加跟踪修订时 `w:id` 与已有书签冲突导致文档损坏 | OOXML 共享 ID 空间的边界情况；来自同一作者的一系列文档类修复 PR 互相关联 | OPEN |
| 4 | **ServiceNow 平台 Skill** ([#568](https://github.com/anthropics/skills/pull/568)) | 覆盖 ServiceNow 全平台的技能：ITSM、ITOM、ITAM/SAM、FSM、SecOps、IntegrationHub | 从"窄脚本辅助"扩展到"平台级助手"，覆盖面极广 | OPEN |
| 5 | **pyxel 复古游戏开发** ([#525](https://github.com/anthropics/skills/pull/525)) | 基于 pyxel-mcp 的复古/像素风游戏开发工作流 | 完整工作流（写代码→截帧→检查→迭代）；MCP + Skill 结合的范例 | OPEN |
| 6 | **testing-patterns** ([#723](https://github.com/anthropics/skills/pull/723)) | 全栈测试模式覆盖：Testing Trophy 模型、单测/React 组件测试/E2E | 体系化的测试方法论，社区长期关注的领域 | OPEN |
| 7 | **ODT 文档技能** ([#486](https://github.com/anthropics/skills/pull/486)) | OpenDocument 格式（.odt/.ods）的创建、填充、读取与 HTML 转换 | 补全文档处理生态的关键缺口；公开格式/ISO 标准的价值主张 | OPEN |
| 8 | **self-audit 推理质量门** ([#1367](https://github.com/anthropics/skills/pull/1367)) | 交付前先做机械文件验证，再按损害严重度进行四维推理审计 | 通用性强（任意项目/技术栈/模型）；与 Issue #1385 的推理质量门流水线提案呼应 | OPEN |

> 观察：排名前列的 PR 集中于 **bug 修复类**（skill-creator、docx/pdf）和**文档处理类**（typography、ODT、docx），反映出社区对"已有 Skill 的可靠性"和"文档工作流补全"的双重关注。


## 2. 社区需求趋势

**A. 安全与信任边界（最激烈讨论）**
- **Issue #492 社区技能在 anthropic/ 命名空间下分发**（43 评论）：社区技能伪装为官方技能，构成信任边界滥用。用户可能授予社区技能过高的权限。这是当前讨论最集中的安全问题。
- **Issue #1175 SharePoint Online 权限控制**：SKILL.md 中直接编写权限逻辑的安全隐患。

**B. Skill 共享与分发机制**
- **Issue #228 组织级 Skill 共享**（16 评论，8 👍）：手动下载→Slack 传输→手动上传的流程繁琐，期待直接共享链接或共享库。

**C. 可靠性修复（长期积压）**
- **Issue #556 `run_eval.py` 0% 触发率**（12 评论，7 👍）：核心评估工具无法触发 skill——已经影响 skill-creator 的全部下游功能，且有 10+ 独立复现报告。
- **Issue #62 Skills 消失**：用户创建 12 个复杂 skills 后全部消失，涉及文件重命名导致的问题。

**D. 元技能与智能体治理**
- **Issue #412 agent-governance**：政策执行、威胁检测、信任评分、审计追踪——社区已有人提议安全治理类 skill。
- **Issue #1329 compact-memory**：符号化紧凑记忆，减少长时运行 agent 的上下文消耗。

**E. 上下文窗口效率**
- **Issue #1487 `claude-api` skill 单次调用注入 ~156k tokens**：直接耗尽上下文窗口，说明部分 skill 在设计时未考虑 token 经济性。


## 3. 高潜力待合并 Skills

| Skill | PR | 潜力说明 |
|-------|----|---------|
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | 仅 3 条评论但直击文档质量盲区，无争议、范围明确，落地概率高 |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 测试方法论是长期需求，内容完整度高 |
| **ODT 文档技能** | [#486](https://github.com/anthropics/skills/pull/486) | 补全文档格式生态缺口，与已有 docx/pdf skill 形成互补 |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | 与 #1385 流水线提案联动，有持续演进空间 |
| **frontend-design 改进** | [#210](https://github.com/anthropics/skills/pull/210) | 存量 Skill 质量改进，一个对话内可执行的指导原则，务实无争议 |

> 值得注意的联动：**Lubrsy706** 连续提交 3 个文档类修复 PR（#538 pdf 大小写、#541 docx ID 冲突、#539 skill-creator YAML 校验），构成体系化的文档生态维护动作，可能加速合并。


## 4. Skills 生态洞察

> **社区最集中的诉求是"可靠性优先"**：对 skill-creator 评估工具失效的持续追踪、Windows 兼容性修复的反复提交、文档类 skill 边界条件的系统性排查，以及安全信任边界的高热度讨论（43+ 评论）——社区在不懈地让现有 Skill 变得更可靠、更安全，而新 Skill 的创作则在文档处理、测试、治理等方向稳步拓展。

---

# Claude Code 社区动态日报 — 2026-08-22

## 1. 今日速览

今日核心动态集中在两个方面：一是 `v2.1.239` 版本发布，为数据驻留工作区引入成本计算修正，并扩展了全屏渲染器至 Bedrock/Vertex/Foundry 等平台；二是社区中关于 AUP（可接受使用政策）安全拦截误报的讨论急剧升温——同一用户（`sworrl`）在过去24小时内批量提交了数十个相关 Issue，集中反映 Fable 5 安全模型对“沮丧语气”和合法安全审计工作的过度敏感，已成为当前社区最突出的痛点。

## 2. 版本发布

### v2.1.239
- **发布说明**：
  - 成本估算（`/cost`、状态栏、`--max-budget-usd`）现已包含数据驻留工作区 1.1× 仅限美国推理溢价的费用
  - 为 Bedrock、Vertex、Foundry 及其他此前被排除的环境新增一次性全屏渲染器优惠；这些平台的新安装现在以该模式启动
- **链接**：[v2.1.239 Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.239)

## 3. 社区热点 Issues

以下为今日最值得关注的 10 个 Issue（含 2 个热门长期 Issue 与 8 个新增典型 Issue）：

### 3.1 [BUG] CVP 批准的组织仍遭遇 cyber safeguard 拦截
- **Issue #84352**（Open，133 条评论，21 👍）
- **要点**：已获网络验证计划（CVP）批准的 Claude.ai 组织，在 Claude Code 中仍持续收到 cyber-safeguard 拦截；验证门户显示“复核中”，与此前批准邮件矛盾。这是治理/合规类问题，涉及安全审查与业务连续性的冲突，社区讨论热度极高。
- **链接**：[#84352](https://github.com/anthropics/claude-code/issues/84352)

### 3.2 [MODEL] 模型过度使用 Bash 工具
- **Issue #19649**（Open，45 条评论，101 👍）
- **要点**：模型在应使用内置 Read/Grep 等工具的场景中频繁调用 Bash（sed/grep），该问题已持续 7 个月，社区关注度高，是工具选择优化的重要反馈。
- **链接**：[#19649](https://github.com/anthropics/claude-code/issues/19649)

### 3.3 [BUG] Artifact 分享持续失败
- **Issue #79824**（Open，13 条评论，20 👍）
- **要点**：用户无法将 Artifact（含 Mermaid 图表的 Markdown 页面）设为公开分享，错误提示持续存在，影响协作场景。
- **链接**：[#79824](https://github.com/anthropics/claude-code/issues/79824)

### 3.4 Fable 5 安全拦截误报批量报告（选定代表）
- **背景**：用户 `sworrl` 提交了大量 AUP 误报 Issue，涉及 Fable 5 安全模型对“沮丧语气”的过度拦截，已导致多起合法授权工作被中断。以下按场景分类选取 8 个典型代表：

| 场景 | 严重性 | Issue |
|---|---|---|
| 移动端无头 UI 审计中断 | session-halted | [#73228](https://github.com/anthropics/claude-code/issues/73228) |
| 会话恢复后续跑 Playwright 审计被拦 | session-halted | [#73227](https://github.com/anthropics/claude-code/issues/73227) |
| 合法的 Android adb UI 自动化中断 | session-halted | [#73203](https://github.com/anthropics/claude-code/issues/73203) |
| 开源无人机地面站项目被拦 | session-halted | [#73214](https://github.com/anthropics/claude-code/issues/73214) |
| 检查自身网站的防御性安全扫描被拦 | session-halted | [#73188](https://github.com/anthropics/claude-code/issues/73188) |
| 部署验证过的交易机器人升级被拦 | session-halted | [#73172](https://github.com/anthropics/claude-code/issues/73172) |
| 例行代码审计被拦 | session-halted | [#73169](https://github.com/anthropics/claude-code/issues/73169) |
| 安全审计被拦（GlassFalcon 域） | session-halted | [#73202](https://github.com/anthropics/claude-code/issues/73202) |

**社区反应**：批量提交表明该问题具有系统性，且影响范围超过个人用例——涉及安全审计、合规检查等本应鼓励的场景。多条目已在 8/22 被关闭（标记为 CLOSED），处理方式需关注（是修复还是标记为重复）。

- **备注**：存在重复/批量提交的可能，但其高频共性（“沮丧语气”触发拦截）值得优先排查。

### 3.5 系统事件伪装为 user 角色消息，导致模型虚构用户同意
- **Issue #44778**（Open，7 条评论，10 👍）
- **要点**：系统事件以 `role: "user"` 传输，模型会虚构用户输入（包括明确批准），涉及 Agent 安全与消息路由问题，对自动化工作流影响大。
- **链接**：[#44778](https://github.com/anthropics/claude-code/issues/44778)

## 4. 重要 PR 进展

- 过去 24 小时无 PR 更新。
- 备注：当前社区的 PR 活跃度较低，重点集中于 Issue 反馈（特别是 AUP 误报）与版本迭代。

## 5. 功能需求趋势

| 趋势 | 说明 | 代表 Issue |
|---|---|---|
| **AUP 安全性改进** | 减少对“沮丧语气”的过度拦截；避免拦截防御性安全测试；区分授权与恶意操作 | [#84352](https://github.com/anthropics/claude-code/issues/84352)、[#73181](https://github.com/anthropics/claude-code/issues/73181) |
| **模型工具选择优化** | 增强模型对 Read/Grep 等内置工具优先级的判断，减少不必要的 Bash 调用 | [#19649](https://github.com/anthropics/claude-code/issues/19649) |
| **Artifact 协作能力增强** | 修复分享/公开链接的稳定性与可靠性 | [#79824](https://github.com/anthropics/claude-code/issues/79824) |
| **系统消息与 Agent 身份** | 明确系统消息的 role 结构，避免模型误解授权与同意语义 | [#44778](https://github.com/anthropics/claude-code/issues/44778) |

## 6. 开发者关注点

- **AUP 误报已成为当前最大痛点**：大量开发者遭遇“沮丧口头禅触发整段会话终止”的问题，尤其是合法安全审计、防御性演练场景。开发者呼吁引入更精细的上下文理解能力，在不阻断正常工作的前提下过滤恶意意图。
- **合规场景受到安全隐患威胁**：CVP 已批准的 AI 组织仍频繁被拦截，影响的是企业级合规工作流，对 Claude Code 在企业中的扩展构成现实阻力。
- **“系统消息”与“用户消息”的边界问题**：现有设计导致 Agent 可能虚构用户授权，在 security-sensitive 自动化场景中风险凸显。
- **模型在工具选择上的基础行为有待优化**：持续 7 个月的 #19649 长期高赞，说明模型对内置工具的使用策略尚未达到社区预期。

---

**日报总结建议**：建议关注 Fable 5 安全模型的 AUP 误报修复进度，并留意 #84352 与 #19649 的后续更新，这两个 Issue 对 Claude Code 在企业与专业开发者中的普及至关重要。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-22

## 今日速览

Windows + Android 远程控制（Remote Control）连接稳定性成为社区最集中火力的问题区域，至少 8 个独立 Issue 指向配对成功但会话建立失败、`Transport unavailable` 或 `503` 错误等不同故障形态，且多数在 8 月 21 日集中爆发。版本侧进入快速迭代轨道，过去 24 小时连续发布 6 个 alpha 版本（0.149.0-alpha.4.1 → 0.150.0-alpha.6），节奏明显加快。PR 侧则密集推进 Guardian 安全审查、浏览器/计算机使用（Computer Use）权限配置、插件钩子（plugin hooks）等基础设施能力。

## 版本发布

过去 24 小时共发布 6 个 alpha 版本（均为 Rust 实现），发布说明为空，但结合 PR 动向可推断核心变更集中在安全审查、沙箱权限、插件系统与远程会话稳定性方向：

- [rust-v0.149.0-alpha.4.1](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.4.1)
- [rust-v0.149.0-alpha.7.1](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.7.1)
- [rust-v0.150.0-alpha.2](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.2)
- [rust-v0.150.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.3)
- [rust-v0.150.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.5)
- [rust-v0.150.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.6)

> 提示：CLI 用户若遭遇远程连接或会话恢复问题，可尝试升级至 `0.150.0-alpha.x` 系列验证修复效果；针对各 alpha 版本的已知回归，请留意对应 GitHub Release 页的更新说明。

## 社区热点 Issues

### 1. #35259 — Codex Desktop 在等待/轮询期间反复重新进入模型，消耗大量配额
- **链接**: [Issue #35259](https://github.com/openai/codex/issues/35259)
- **重要性**: 在重置后的 49% 用量窗口内，仅含 wait/status 轮询操作的模型调用占原始 token 输出的 19.8%，属显著配额浪费。
- **社区反应**: 15 条评论、8 个 👍，用户对配额消耗的透明度诉求强烈。

### 2. #39815 — Windows 主机与 Android Remote 配对成功但会话加载失败（/wham/tasks/list 返回 503）
- **链接**: [Issue #39815](https://github.com/openai/codex/issues/39815)
- **重要性**: 远程控制核心体验断裂——设备显示已授权，但任务列表不可达，且为回归性问题。
- **社区反应**: 13 条评论，属于今天 Remote 故障集群中讨论最充分的一条。

### 3. #38503 — ChatGPT Web 端 "Too many requests" 阻断聊天与 Work 任务
- **链接**: [Issue #38503](https://github.com/openai/codex/issues/38503)
- **重要性**: 限流问题从 API 层面蔓延至 Web 应用层，直接影响日常使用。
- **社区反应**: 9 条评论、11 个 👍，是本周 👍 数最高的 Issue 之一，影响面广。

### 4. #39954 — Windows + Android 远程控制初始化后进入无限重连循环
- **链接**: [Issue #39954](https://github.com/openai/codex/issues/39954)
- **重要性**: 已排除过期服务器状态干扰，问题指向 WebSocket 会话建立后的协议层缺陷。
- **社区反应**: 9 条评论，与 #39856、#39815 等构成同簇故障的不同表现形态。

### 5. #17598 — 原生子代理（subagent）编排在非 OpenAI 自定义 Provider 下无法正常工作
- **链接**: [Issue #17598](https://github.com/openai/codex/issues/17598)
- **重要性**: 长期未关闭（4 月创建），牵涉自定义模型生态的核心能力缺失。
- **社区反应**: 9 条评论、2 个 👍，与 #33405 的 "native edit tool" 诉求互为表里。

### 6. #39947 — Android Remote 不可用：Windows 主机显示已断开，长任务无法打开
- **链接**: [Issue #39947](https://github.com/openai/codex/issues/39947)
- **重要性**: 与 #39815 同为 "配对成功但无法使用" 的变体，但报错形态不同（主机显示断开 vs 503）。
- **社区反应**: 9 条评论，进一步坐实 Windows 端远程功能的系统性回归。

### 7. #39974 — Codex 远程控制跨 Android/iOS 三台设备均不稳定，Windows 桌面端正常
- **链接**: [Issue #39974](https://github.com/openai/codex/issues/39974)
- **重要性**: 排除单设备问题，指向 Windows 主机端的远程服务实现缺陷。
- **社区反应**: 7 条评论，覆盖 Android + iOS 双平台，影响面广。

### 8. #29002 — MCP 工具调用失败：合法 tool result 解码为 CustomResult 时报 "Unexpected response type"
- **链接**: [Issue #29002](https://github.com/openai/codex/issues/29002)
- **重要性**: 影响 MCP 生态集成，当前仅接受预设响应类型导致合法结果被拒绝。
- **社区反应**: 6 条评论、7 个 👍，涉及 Bedrock 等第三方 Provider 的兼容性问题。

### 9. #35718 — Windows 沙箱被 NUL 填充的 deny_read_acl_state.json 永久破坏，重装也无法恢复
- **链接**: [Issue #35718](https://github.com/openai/codex/issues/35718)
- **重要性**: 状态文件损坏导致沙箱永久不可用且无法通过重装修复，属极端但破坏性极强的故障。
- **社区反应**: 6 条评论，开发者关注状态文件的持久化位置与数据完整性。

### 10. #39178 — 隐藏的 avatarOverlay 持有已完成线程，主界面永久卡在 "Thinking"
- **链接**: [Issue #39178](https://github.com/openai/codex/issues/39178)
- **重要性**: UI 层状态管理缺陷导致会话状态不同步，用户感知为"永久卡死"。
- **社区反应**: 6 条评论，暴露桌面端线程所有权管理的问题。

## 重要 PR 进展

### 1. #40031 — 保留严格 MCP 自动审查的原始结果
- **链接**: [PR #40031](https://github.com/openai/codex/pull/40031)
- **内容**: 传播权威的拒绝/超时/中止响应而非替换为通用拒绝，保留审查者的操作与元数据。

### 2. #40024 — 统一执行中落实细粒度沙箱审批
- **链接**: [PR #40024](https://github.com/openai/codex/pull/40024)
- **内容**: 统一执行路径接入共享审批策略检查，`require_escalated` 命令在细粒度 `sandbox_approval` 开启时可提示、关闭时保持拒绝。

### 3. #40021 — Guardian 审查随工具调用一并取消
- **链接**: [PR #40021](https://github.com/openai/codex/pull/40021)
- **内容**: 将工具取消令牌传播至 Guardian 审批审查中，中断工具时同步中止其待处理审查。

### 4. #40018 — 新增浏览器与计算机使用配置
- **链接**: [PR #40018](https://github.com/openai/codex/pull/40018)
- **内容**: 新增类型化 `browser_use` 与 `computer_use` 设置，覆盖历史记录访问、CDP 策略、Windows AUMID/可执行文件路径等。

### 5. #40015 — 加固远程已安装插件缓存协调
- **链接**: [PR #40015](https://github.com/openai/codex/pull/40015)
- **内容**: 将插件快照限定至活动账户，账户切换时丢弃进行中的加载；序列化 bundle 协调与直接安装/卸载。

### 6. #40013 — 异步风险评分复用 Guardian 审查结果
- **链接**: [PR #40013](https://github.com/openai/codex/pull/40013)
- **内容**: 保留同步 Guardian 允许/拒绝审查的有界证据，作为后续 v2 异步分类器采样的可信开发者上下文。

### 7. #40012 — 保留执行器 MCP 停止钩子的执行上下文
- **链接**: [PR #40012](https://github.com/openai/codex/pull/40012)
- **内容**: 将停止钩子调用限定至注册钩子的 MCP 服务器环境，环境不匹配时拒绝调用。

### 8. #40007 — 实现 App Server 中的 Amazon Bedrock 配置
- **链接**: [PR #40007](https://github.com/openai/codex/pull/40007)
- **内容**: 实现 `account/bedrock/discover` 与 `setup` 接口，支持 AWS 配置文件与环境凭据验证与持久化。

### 9. #40005 — 升级命令经同步 Guardian 审查
- **链接**: [PR #40005](https://github.com/openai/codex/pull/40005)
- **内容**: 请求 `require_escalated` 权限的命令（含重试）需完整 Guardian 审查，不得跳过。

### 10. #40004 — 权限更新时保留受管 deny-read 规则
- **链接**: [PR #40004](https://github.com/openai/codex/pull/40004)
- **内容**: 受管文件系统 `deny_read` 规则独立保留并在权限更新时合并，拒绝会削弱规则的配置文件。

---

另有 #40028（Guardian V2 分类结果日志）、#40000（通过 app-server 暴露浏览器/计算机使用要求）、#39997（`/copy` 新增响应目标选择器）等值得关注。

## 功能需求趋势

1. **远程控制（Remote Control）稳定性**（最高优先级）: 至少 8 个 Issue 指向 Windows 主机 + Android/iOS 客户端的连接失败、会话挂起、任务列表不可用，集中在 26.8xx 版本，属系统性回归。
2. **第三方模型 Provider 深度集成**: #17598（subagent 编排不支持非 OpenAI Provider）与 #33405（缺失 native edit tool）表明社区对自定义模型获得与 OpenAI 模型同等工具能力有持续诉求。
3. **浏览器自动化与 Computer Use 配置化**: PR #40018、#40000、#39995 密集补充浏览器/计算机使用能力，涉及访问策略、审批流程、CDP 支持等。
4. **配额计费与限流透明度**: #35259（轮询消耗配额）、#38728（配额计量异常加速）反映用户对配额消耗机制的不透明不满。
5. **多配置文件并行运行**: #18655（支持同时运行多个 profile）虽已关闭但仍有 5 条评论，说明用户对 profile 切换体验有改进期待。

## 开发者关注点

- **Windows 远程功能属当前最大痛点**: 多个独立 Issue 指向同一故障域，且均为 8 月 20-21 日集中爆发，开发者对 26.818 版本的远程功能信心明显下降。
- **配额消耗可观测性不足**: 用户在 "等待/轮询" 期间被重复计费，且无法从 UI 识别这些隐藏消耗，呼吁更透明的用量明细。
- **沙箱状态文件可靠性堪忧**: #35718 中单个 NUL 填充文件导致功能永久损坏且可跨越重装持续存在，开发者关注状态文件的原子写入与损坏恢复机制。
- **MCP 生态兼容性需加强**: 自定义 Provider 下工具结果解码失败、subagent 编排不可用等问题长期未修复，削弱了 Codex 作为开放平台的吸引力。
- **UI 与底层状态一致性欠缺**: #39178（隐藏 avatarOverlay 持有线程）、#16405（SQLite 线程标题不同步）等暴露了多存储/多组件间的状态同步缺陷，需系统性梳理。

---

*本日报基于 GitHub 公开数据自动生成，数据截至 2026-08-22。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-22** | **数据来源：** github.com/google-gemini/gemini-cli


## 今日速览

今日社区动态聚焦于 **Agent 子代理可靠性** 与 **Auto Memory 内存系统** 两大核心领域。其中，`#22323`（子代理 Max Turns 被误报为成功）和 `#21409`（通用代理挂起）持续占据讨论榜首，反映社区对 Agent 稳定性有较高期待。值得关注的是，维护团队今日推动了多项 **PR 生成流水线（PR Generation）** 的基础设施建设（共 10+ PR），同时合并了 `shellExecutionService` 类型安全重构，并提交了修复 **macOS Seatbelt 沙箱逃逸风险** 的安全补丁。


## 版本发布

### v0.56.0-nightly.20260821.g30573d2e4

- **fix(core)**: 修复 ignore 路径处理中符号链接（symlink）评估不一致的问题（by @luisfelipe-alt, PR #28915）
- **refactor(core)**: 移除 shellExecutionService 中的 eslint-disable 与类型断言（by @DavidAPierce）


## 社区热点 Issues

精选近 24 小时内更新最活跃、讨论度最高的 10 个 Issue：

### 1. Subagent 恢复逻辑误导：MAX_TURNS 被报告为 GOAL 成功
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) | `P1` | `kind/bug` | 评论 13 | 👍 2

**核心问题**：`codebase_investigator` 子代理在触发最大轮次限制、未完成任何分析的情况下，仍向主代理报告 `status: "success"` 且 `Termination Reason: "GOAL"`。这会让主代理误以为任务已成功完成，掩盖了实际的中断。

**社区反应**：该问题为维护者锁定，被标记为 `status/need-retesting`，社区 13 条评论主要围绕复现细节和修复方向展开。此问题直接影响多代理协作的可信度，属 P1 高优先级。

### 2. 通用代理（Generalist agent）挂起无响应
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) | `P1` | `kind/bug` | 评论 8 | 👍 8

**核心问题**：当 CLI 将任务委托给通用代理时，代理会无限期挂起（用户等待长达一小时）。即便是创建文件夹这类简单操作也会触发。用户通过指示模型不要使用子代理即可规避。

**社区反应**：👍 8 为本周最高，说明该问题影响面广。多条评论确认此问题在多个场景下可复现，用户强烈期望在该问题上得到修复。

### 3. Auto Memory 对低信号会话无限重试
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) | `P2` | `kind/bug` | 评论 5 | 👍 0

**核心问题**：Auto Memory 仅在提取代理成功读取会话记录后才将该会话标记为已处理。当代理主动跳过低信号会话时，该会话将无限期保留在待处理队列中，反复出现在后续索引中。

**社区反应**：属于 Auto Memory 系列 Bug 之一（同作者提交 5 个相关 Issue），显示该新功能仍处于密集排错阶段。

### 4. Auto Memory 缺少确定性脱敏，日志过多
[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) | `P2` | `kind/bug` | 评论 4 | 👍 0

**核心问题**：Auto Memory 在将本地会话内容发送给提取模型时，脱敏指令在内容进入模型上下文之后才生效，存在密钥泄露风险。同时服务日志会记录已有的 skill 配置，增加泄露面。

**社区反应**：属于安全类缺陷，当前无公开讨论，但标记为维护者关注。

### 5. Shell 命令执行完毕后卡在 “Waiting input”
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) | `P1` | `kind/bug` | 评论 4 | 👍 3

**核心问题**：Gemini 执行完简单 CLI 命令后，UI 仍显示命令运行中并提示 “Awaiting user input”，但命令实际已结束。此问题反复出现，且发生在不会请求用户输入的简单命令上。

**社区反应**：👍 3 说明有一定用户受影响，属高频交互痛点，直接影响日常使用体验。

### 6. 浏览器子代理在 Wayland 下失败
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) | `P1` | `kind/bug` | 评论 4 | 👍 1

**核心问题**：浏览器子代理在 Wayland 显示服务器下无法正常工作，具体表现为代理直接退出且 Termination Reason 为 "GOAL"（异常终止）。

**社区反应**：Linux 用户受影响较大，当前标记为 `status/need-retesting`，等待修复验证。

### 7. Gemini 不会主动使用 skills 和子代理
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) | `P2` | `kind/bug` | 评论 6 | 👍 0

**核心问题**：用户配置了 gradle、git 等自定义 skills，但 Gemini 在相关场景中几乎不会主动调用，只有在用户明确指示时才使用。

**社区反应**：该反馈属于功能行为类，社区讨论认为这与子代理的自主决策策略有关，期待后续优化。

### 8. 符号链接的 Agent 文件不被识别
[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) | `P2` | `kind/bug` | 评论 4 | 👍 0

**核心问题**：`~/.gemini/agents/` 下的 `filename.md` 如果是符号链接（symlink），则不会被识别为可用的子代理。

**社区反应**：用户希望支持符号链接方式管理 Agent 配置；今日已有 PR #28956 提交修复。

### 9. 浏览器代理忽略 settings.json 覆盖配置
[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) | `P2` | `kind/bug` | 评论 3 | 👍 0

**核心问题**：浏览器代理完全忽略全局或项目级 `settings.json` 中的配置覆盖（如 `maxTurns`）。虽然 `AgentRegistry` 在初始化时正确读取并合并了这些设置，但实际执行中未生效。

**社区反应**：配置不生效导致用户无法按需调整浏览器代理行为，属配置系统一致性问题。

### 10. 子代理轨迹无法通过 `/chat share` 分享
[#22598](https://github.com/google-gemini/gemini-cli/issues/22598) | `P3` | `kind/feature` | 评论 2 | 👍 1

**核心问题**：子代理的轨迹数据已通过聊天记录服务保存，但缺少便捷的查看和分享渠道，不利于开发者审查和评估子代理行为。

**社区反应**：👍 1 表明开发者社区有明确需求，希望增强可观测性。


## 重要 PR 进展

精选近 24 小时内更新的 10 个重要 PR：

### 1. 修复符号链接/Junction 的 skills 目录解析
[#28956](https://github.com/google-gemini/gemini-cli/pull/28956) | `OPEN` | `size/s`

**内容**：修复 Windows junction（`mklink /J`）或符号链接指向 `.agents` 目录时，CLI 扫描 `[workspace]/.agents/skills` 因路径未解析而失败的问题。属于 Agent Skills 标准兼容性修复，解决了 Issue #28944。

### 2. 历史回滚与重试提示优化
[#28934](https://github.com/google-gemini/gemini-cli/pull/28934) | `OPEN` | `size/l`

**内容**：优化工具调用的取消回滚与重试提示策略。核心思路是在工具取消时不再追加合成的错误消息，以减少上下文膨胀、降低 API 请求量，并最大化前缀缓存的利用率。

### 3. 修复 401 子串误判为认证错误
[#28827](https://github.com/google-gemini/gemini-cli/pull/28827) | `OPEN` | `size/s`

**内容**：修复 `isAuthenticationError` 将包含 `401` 子串的无辜文本（如端口号）误判为认证失败的问题。回退逻辑现在仅在消息开头或 HTTP 状态上下文中识别 `401`。

### 4. 修复 A2A 服务器陈旧取消错误
[#28940](https://github.com/google-gemini/gemini-cli/pull/28940) | `OPEN` | `size/l`

**内容**：修复 Google Cloud Assistant（GCA）执行中断问题——A2A 服务器在请求被中止或取消后，后续用户提示会立即崩溃并报 `Execution aborted`。该 PR 清除了新对话轮次中的陈旧取消状态，从根本上解决状态损坏。

### 5. macOS Seatbelt 沙箱隔离容器运行时
[#28935](https://github.com/google-gemini/gemini-cli/pull/28935) | `CLOSED` | `size/l`

**内容**：安全增强。在 macOS Seatbelt 沙箱配置中显式拒绝访问容器运行时守护进程的 UNIX 域套接字、CLI 二进制文件、Mach/XPC 服务查找及 POSIX 共享内存，防止通过 Docker Desktop VirtioFS 等容器管理程序文件系统挂载逃逸沙箱。

### 6. 移除 shellExecutionService 中的 eslint-disable 与类型断言
[#28862](https://github.com/google-gemini/gemini-cli/pull/28862) | `CLOSED` | `size/l`

**内容**：代码质量重构。移除 `shellExecutionService.ts` 中因 `any` 类型而添加的 eslint-disable 和类型断言，在 `fix/mac-pty-resource-leak` 分支上完成。

### 7. 修复错误报告被杀毒软件误报
[#20238](https://github.com/google-gemini/gemini-cli/pull/20238) | `CLOSED` | `size/m`

**内容**：将错误报告从系统临时目录（`os.tmpdir()`）迁移至专用项目目录（`~/.gemini/tmp/<hash>/error-reports/`），并添加反恶意软件扫描豁免标记，解决杀毒软件将 Gemini CLI 错误报告误判为恶意文件的问题。

### 8. PR 生成：交互式 Diff 对比可视化生成器
[#28952](https://github.com/google-gemini/gemini-cli/pull/28952) | `OPEN` | `size/xl`

**内容**：引入交互式 HTML diff 可视化工具（`generate_diff_viewer.py`），使用 Diff2HTML 和 Highlight.js 呈现代理生成的 PR diff、ground-truth GitHub 修复与基线源文件的并排对比。

### 9. PR 生成：LLM Diff 评审模块与评分标准
[#28949](https://github.com/google-gemini/gemini-cli/pull/28949) | `OPEN` | `size/l`

**内容**：引入 LLM-as-a-Judge 的 diff 评估模块（`eval_diff_judge.py`）与评分提示词标准（`judge_prompt.md`），用于对生成的 PR diff 与已接受 ground-truth PR 进行自动化基准评测。

### 10. 分类评估：统一 Golden Issue 生成 Schema
[#28945](https://github.com/google-gemini/gemini-cli/pull/28945) | `CLOSED` | `size/l`

**内容**：升级 `generate_golden_issue.py` 以输出生产环境 Firestore 文档结构（`status='TRIAGED'`、`workable_spec`、`github_metadata`、`lock`），并支持多线程批量生成。


## 功能需求趋势

从近 24 小时 Issue 与 PR 中提炼的社区关注方向：

### 1. 子代理自主性与可靠性（当前最高优先级）
- 大量 P1/P2 Issue 聚焦子代理的挂起、误报成功、不主动使用技能等问题（#21409、#22323、#21968）
- 要求：子代理能智能判断何时使用 skills 和工具，正确报告失败状态（而非伪装为 GOAL 成功）

### 2. Auto Memory 内存系统的成熟度（新增热点）
- 围绕 Auto Memory 有 5 个相关 Issue（#26516、#26522、#26523、#26525），涵盖低信号会话重试、无效补丁隔离、确定性脱敏、日志降噪等
- 要求：内存系统应具备更智能的会话筛选机制、安全的密钥处理、以及非侵入式日志

### 3. AST 感知的代码库导航（中长期探索）
- EPIC #22745 追踪 AST 感知的文件读取、搜索与代码库映射；配套 Issue #22746 建议使用 `tilth` 或 `glyph` 工具
- 目标：通过 AST 精确读取方法边界，减少因错误对齐读取导致的 token 消耗和轮次浪费

### 4. 浏览器代理的韧性与配置一致性
- #22232 要求浏览器代理支持自动会话接管与锁恢复（而非快速失败）
- #22267 要求浏览器代理尊重 `settings.json` 中的 `maxTurns` 等配置覆盖

### 5. 代码库探索的 Token 效率优化
- #19561 提出 "Tactful Extraction" 策略：优先 grep → 精准定位 → 外科手术式读取，避免大文件读取导致的上下文膨胀（当前基线 36.6k tokens/turn）

### 6. PR 生成与评估流水线（维护团队方向，社区不可见）
- 大量 PR（#28933、#28948、#28949、#28951、#28952、#28953）围绕自动化 PR 生成、diff 质量评估、GCS 轨迹记录等基础设施搭建
- 属内部工程效率建设，但对社区的价值在于后续评估标准可能开源


## 开发者关注点

### 高频痛点

1. **子代理挂起与假成功**：`#21409` 中通用代理无限挂起与 `#22323` 中 MAX_TURNS 被报告为 GOAL 成功，是开发者反馈最强烈的两个问题。前者影响任务完成，后者产生错误的成功信号、降低自动化流程的可信度。

2. **Shell 执行状态不同步**：`#25166` 中命令已结束但 UI 仍显示 "Waiting input"，说明 shell 执行状态同步存在缺陷，影响用户对命令执行状态的判断。

3. **配置覆盖不生效**：`#22267` 中浏览器代理忽略 `settings.json` 中的 `maxTurns` 等配置，反映配置系统的读取-应用链路存在断点。

4. **自动记忆的隐私与效率**：Auto Memory 系列 Issue（#26522、#26525）表明用户关注后台任务是否会造成数据泄露风险、以及无价值内容的反复处理。

### 值得注意的细节

- 多数高讨论度 Issue 标记为 `🔒 maintainer only` + `workstream-rollup`，显示核心问题由维护团队直接负责排期跟踪
- 今日合并的符号链接修复（#28956）直接回应了 `~/.gemini/agents/` 下的 symlink 识别问题（#20079）
- 一位用户（SandyTao520）集中提交了 5 个 Auto Memory 相关 Issue，说明新功能测试深入，反馈成体系

### 维护团队高效修复案例

- **当日修复**：#28956 于 8-22 提交，解决 #28944 符号链接问题
- **安全响应**：#28935 在 24 小时内完成审查并关闭，及时封堵沙箱逃逸路径
- **持续重构**：DavidAPierce 在 `fix/mac-pty-resource-leak` 分支上持续进行代码质量改进（#28862、#28915）

---

> 本日报基于 GitHub 公开数据自动生成，仅供参考。所有链接均可直接跳转至对应 Issue/PR 页面。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-22**


## 今日速览

今日最值得关注的是 **v1.0.81-7 发布**，新增了崩溃/重启后自动恢复会话的关键能力，直接回应了开发者长期以来的痛点。社区方面，**多模型（BYOK）切换与配置**持续霸榜，成为本周最热功能诉求。此外，**ACP 模式** 的多个行为偏差问题（取消语义、后台子代理中断）在今日集中爆发，值得关注。


## 版本发布

### v1.0.81-7

**新增功能：**

- **会话自动恢复**：CLI 启动时可检测并恢复上次异常退出（崩溃或机器重启）时仍处于打开状态的会话，告别手动逐个重新打开终端的麻烦。
- **模型信息增强**：`models.list` 现可返回服务端发布的每条模型的 infoMessages 和 warningMessages，提供更透明的模型状态提示。
- **新增 `copilot app` 命令**：用于打开 GitHub 应用（推测为 Copilot 应用主页或相关配置页面，Release 说明被截断）。

> 发布链接：https://github.com/github/copilot-cli/releases


## 社区热点 Issues

过去 24 小时共有 **41 条** Issue 更新，以下为最值得关注的 10 条：

### 1. 支持一个会话内切换多个 BYOK 模型
- **Issue #3709** | 👍 27 | 💬 4 | [链接](https://github.com/github/copilot-cli/issues/3709)
- **状态**：OPEN
- **重要性**：社区呼声最高的功能需求之一（👍 27）。BYOK 模式目前通过 `COPILOT_MODEL` 将整个会话固定在单一模型上，`/model` 选择器不显示本地/自有模型。用户无法在不重开终端的情况下切换模型，大幅限制工作流灵活性。
- **关联**：与 #3282（多 BYOK 配置）形成呼应，是目前**模型管理**方向最核心的诉求。

### 2. 支持配置多个 BYOK 模型
- **Issue #3282** | 👍 26 | 💬 8 | [链接](https://github.com/github/copilot-cli/issues/3282)
- **状态**：OPEN
- **重要性**：与 #3709 同属一个需求的两面——一个是如何在会话中切换，一个是如何在配置中声明多个模型。目前仅支持单个 BYOK（通过环境变量），用户抱怨必须终止会话、重新设置环境变量才能换模型。8 条评论在同类中属较多，持续热议中。

### 3. 会话分支（Session Branching）
- **Issue #1313** | 👍 13 | 💬 7 | [链接](https://github.com/github/copilot-cli/issues/1313)
- **状态**：OPEN
- **重要性**：老牌需求（2 月提出）至今热度不减。用户希望从现有会话的某个时间点**派生**一个新会话，继承完整上下文历史，同时保留原会话不变。这对探索性开发和多方案对比是刚需。

### 4. 模型 "auto" 模式禁用推理力度配置
- **Issue #4560** | 👍 0 | 💬 0 | [链接](https://github.com/github/copilot-cli/issues/4560)
- **状态**：OPEN（今日新增）
- **重要性**：自动路由模式下 `reasoningEffort` 被强制设为 `null`，且用户手动配置会被拒绝——意味着**无法控制推理深度**。对使用混合模型路由的用户影响较大，属于新暴露的配置缺陷。

### 5. 'medium' 推理力度不被 claude-haiku-4.5 支持
- **Issue #4345** | 👍 4 | 💬 8 | [链接](https://github.com/github/copilot-cli/issues/4345)
- **状态**：OPEN
- **重要性**：两个服务端 feature flag 同时启用时，子代理执行反复报错 `Reasoning effort 'medium' is not supported`。涉及**模型能力与推理力度配置的兼容性**问题，评论数 8 说明讨论活跃。

### 6. ACP 模式下 session/prompt 无条件中断所有后台子代理
- **Issue #4555** | 👍 0 | 💬 0 | [链接](https://github.com/github/copilot-cli/issues/4555)
- **状态**：OPEN（今日新增）
- **重要性**：ACP 模式下，`session/prompt` 处理器第一步就调用 `session.abort()`，导致所有后台运行中的子代理被取消——而交互式 TUI 没有此问题。**ACP（Agent Client Protocol）是外部工具集成的关键接口**，此问题会阻断基于 ACP 构建第三方 UI/IDE 插件的开发者。

### 7. MCP 服务器不可用时 hang 住并误报 "waiting on ide"
- **Issue #4552** | 👍 0 | 💬 0 | [链接](https://github.com/github/copilot-cli/issues/4552)
- **状态**：OPEN（今日新增）
- **重要性**：当 MCP 服务器主机不可达时，CLI 挂起并显示误导性的 `waiting on ide` 状态，用户无法区分是 IDE 问题还是 MCP 故障。**错误诊断信息质量**直接关系到排障效率。

### 8. 新窗口/切换模型后 AIC 用量显示不准确
- **Issue #4511** | 👍 0 | 💬 2 | [链接](https://github.com/github/copilot-cli/issues/4511)
- **状态**：OPEN
- **重要性**：Kimi K3 等模型下，会话报告的 AIC（AI 用量）严重低估实际消耗。**用量计量可靠性**是企业用户和付费用户的核心关切。

### 9. store_memory 在 1.0.81 预发布版中失败：`Instance id is required`
- **Issue #4535** | 👍 0 | 💬 4 | [链接](https://github.com/github/copilot-cli/issues/4535)
- **状态**：OPEN
- **重要性**：1.0.81 预发布版的**回归 bug**——原生内存写入器因缺少 instance ID 而持续失败。4 条评论均为受影响用户反馈，需尽快修复。

### 10. 计划（Plan）内联注解功能请求
- **Issue #4563** | 👍 0 | 💬 0 | [链接](https://github.com/github/copilot-cli/issues/4563)
- **状态**：OPEN（今日新增）
- **重要性**：用户希望在生成的计划中直接选中文本/步骤添加内联注解，无需在聊天中重新描述上下文。这是**交互效率**方向的合理诉求，也可能影响评审工作流设计。


## 重要 PR 进展

过去 24 小时内**无 PR 更新**。


## 功能需求趋势

综合近 24 小时活跃 Issue 与长期高热度需求，社区关注方向集中在以下五类：

| 趋势方向 | 代表 Issue | 热度信号 |
|---|---|---|
| **多模型管理与 BYOK 增强** | #3709、#3282 | 👍 27 / 👍 26，持续数周霸榜 |
| **会话管理能力**（分支、跨目录恢复、筛选） | #1313、#4554 | 👍 13，长期需求；👍/💬 持续新增 |
| **ACP 协议规范性**（取消语义、后台任务并发） | #4555、#4561 | 今日集中新增，说明 ACP 用户群体正在扩大 |
| **MCP 配置与可靠性**（热重载、错误恢复、连接状态） | #4562、#4552、#4542 | 每日均有新问题，数量多且分散 |
| **交互效率与体验**（计划内联注释、主题、用量显示） | #4563、#4485、#4511 | 零散但有稳定反馈 |

> 值得注意的是，**ACP 相关 Issue（#4555、#4561）在今日集中爆发**。ACP 作为外部客户端连接 Copilot CLI 的桥梁（VS Code、Cursor 等 IDE 集成的可能通道），语义偏差和并发行为问题将直接影响第三方生态的稳定性。GitHub 官方可能尚未充分测试 ACP 在复杂场景（后台任务 + 取消 + 并发）下的行为。

**模型相关需求**已连续多日位居讨论热度榜首，可能是用户从单模型向多模型工作流迁移过程中的核心痛点。


## 开发者关注点

- **BYOK/多模型切换（痛点最集中）**：单会话固定模型的限制严重影响拥有多个模型 API Key 的开发者，切换模型需要重开会话、重新配置环境变量。两个高赞 Issue（#3709、#3282）均围绕此问题。
- **会话恢复与分支（高频需求）**：崩溃后丢失多终端会话状态是高频抱怨；同时开发者也期望能像 Git 分支一样对会话进行分支管理。
- **ACP 模式行为偏差（新爆发点）**：今日新增 2 个 ACP 相关问题（无条件 abort 后台子代理、cancel 语义错误），说明外部集成开发者正在快速增加，但协议一致性需要加强。
- **MCP 生态可靠性问题分散但持续**：从连接失败误报到配置热重载失效，**MCP 相关问题几乎每天都有新报告**。`mcp list` 能检测到配置但实际会话中不生效（#4542）尤其具有迷惑性。
- **Windows 平台体验**：#4549（每次执行命令弹出 PowerShell 窗口）、#4540（路径含空格时 `wta.exe` 启动失败）——Windows 下的终端体验和进程管理仍有明显短板。

---

*本日报由 AI 技术分析师根据 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-22**  
**数据来源：** [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## 今日速览

过去24小时社区活跃度平稳，暂无新版本发布。核心关注点集中在一个**后台子代理（Background subagent）在任务超时/终止后仍持续消耗 LLM 配额**的严重 Bug（Issue #2615）。同时，一份关于**插件安全与持久化数据管理**的文档完善 PR（#2614）正在推进中，体现社区对安全信任边界的重视。

---

## 版本发布

过去24小时内无新版本发布。

---

## 社区热点 Issues

过去24小时内仅有 1 个 issue 有更新，今日暂无足够样本量支撑"10个最值得关注"的筛选。以下为今日唯一活跃 Issue：

### 1. [Bug] Background subagent keeps making LLM calls after TaskStop/timeout marks it terminal  
**编号：** [#2615](https://github.com/MoonshotAI/kimi-cli/issues/2615)  
**状态：** OPEN | **创建：** 2026-08-21 | **更新：** 2026-08-21 | **评论：** 0 | 👍：0  
**重要性：** ★★★★★  
**摘要：** 后台子代理在任务被标记为 `timed_out` 或 `killed` 后，仍继续发送 LLM 请求。这些任务已从活跃任务追踪列表中消失，导致后续的 `TaskStop` 无法终止它们，**配额消耗变得不可见**，可能引发隐藏的费用支出与资源浪费。  
**社区反应：** 暂无评论。由于涉及**配额/费用**与**资源生命周期管理**两个核心痛点，且可能影响生产环境稳定性，该问题被列为高风险。

---

## 重要 PR 进展

过去24小时内仅有 1 个 PR 有更新，以下为详情：

### 1. docs(plugins): document security and persistent data  
**编号：** [#2614](https://github.com/MoonshotAI/kimi-cli/pull/2614)  
**状态：** OPEN | **创建：** 2026-08-20 | **更新：** 2026-08-21 | **作者：** QIANLING-0831  
**重要性：** ★★★★☆  
**内容：** 纯文档补充，涵盖以下几点：  
- 明确本地执行的插件工具的**信任边界（trust boundary）**  
- 解释 `inject` 命令的**凭据处理注意事项**  
- 澄清**重装插件会替换安装目录**的行为  
- 建议为插件数据设置**独立的数据目录**  
**社区反应：** 暂无评论。该 PR 有助于降低插件生态的安全误用风险，为后续扩展插件能力提供规范基础。

---

## 功能需求趋势

基于过去24小时活跃数据样本较小，结合近期观察，社区对以下功能方向保持持续关注：

1. **任务生命周期管理**：对 `TaskStop`/`timeout` 后的资源释放与隔离提出更高要求（Issue #2615 即属此类）
2. **插件安全机制**：信任边界、凭据隔离、数据持久化规范（PR #2614 呼应此需求）
3. **配额与费用可视化**：后台任务对 API 配额消耗的可观测性仍是高频诉求

---

## 开发者关注点

当前开发者反馈中较突出的痛点为：

- **后台任务资源失控**：子代理在任务终止后仍持续消耗 LLM 配额，且无法被追踪和停止，直接造成成本风险与系统资源浪费。
- **插件数据与凭据安全**：对插件安装、重装及 `inject` 对凭据的处理缺乏权威文档指引，开发者需自行摸索安全实践。

---

*日报数据基于过去24小时 GitHub 动态，样本有限。如需更全面的趋势分析，建议结合更长时间窗口的数据。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-22** | 数据来源：github.com/anomalyco/opencode


## 今日速览

今日发布 v1.18.21 补丁版本，重点修复了模型未知结束原因导致响应中断的问题。社区侧，**响应中断/停止**类问题持续发酵（#38749、#34473、#43939），成为开发者反馈最集中的痛点；同时，控制台登录 URL 解析、会话 Fork 一致性、Shell 授权安全加固等一批 Core 层修复 PR 密集合并，代码质量与稳定性投入明显加大。


## 版本发布

### v1.18.21

**Core 修复**
- 当模型返回未知 `finish_reason` 时，不再提前停止响应，而是继续生成
- Vertex AI `eu` / `us` 多区域 Gemini 请求改经 REP 端点路由

**Desktop 修复**
- 文件搜索加载期间保持已有搜索结果可见，避免闪烁/消失

### v1.18.20

**Core 修复**
- 失败的子代理工具调用现在会暴露可恢复的 `task_id`
- 对 `finish_reason: network_error` 及更多网络错误变体（`network-error`、`network_error`）自动重试
- 子代理失败以可恢复形式呈现，而非静默吞掉


## 社区热点 Issues（Top 10）

### 1. #38749 — Agent 持续突然停止响应
**状态：** OPEN | **评论：** 9 | **👍：** 4
[链接](https://github.com/anomalyco/opencode/issues/38749)

**摘要：** 用户报告 Agent 在运行过程中频繁无预警地停止，附有截图但未提供可复现步骤。结合 #34473 与 #43939，这是目前社区反馈密度最高的一类问题。

**关注理由：** 稳定性的核心痛点，涉及未知 finish reason 与静默中断，直接影响日常可用性，三线程共同指向此问题。

### 2. #24153 — [Feature] 支持对已归档会话执行取消归档/恢复
**状态：** OPEN | **评论：** 9 | **👍：** 11
[链接](https://github.com/anomalyco/opencode/issues/24153)

**摘要：** 归档目前是单向操作，会话一旦归档即从侧边栏消失，仅以置灰形式可见，用户无法恢复。

**关注理由：** 11 个 👍 为今日最高，属于高频工作流缺口，预计很快会进入开发排期。

### 3. #43939 — v1.18.21 在 finish=unknown 时反复续写已完成的响应
**状态：** OPEN | **评论：** 1 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/43939)

**摘要：** 当 provider 标记 `finish=unknown` 且 token 用量为零时，v1.18.21 会反复续写已经完整的响应。这是对 #43892 修复的直接回归反馈。

**关注理由：** 新版本引入的回归，与今日发布的 v1.18.21 修复目标直接相关，需要尽快跟进。

### 4. #6245 — [CLOSED] VSCode 中 Ctrl+P 快捷键失效
**状态：** CLOSED | **评论：** 11 | **👍：** 24
[链接](https://github.com/anomalyco/opencode/issues/6245)

**摘要：** VSCode 中 Ctrl+P 被映射为“转到文件”，但缺少条件约束，导致在终端或 opencode 扩展中误触发。用户建议补充 when 条件。

**关注理由：** 👍 24 为今日最高，VSCode 扩展的 IDE 集成体验是社区的重点关注方向。

### 5. #42657 — 多子代理会话导致 TUI 卡顿（渲染线程 97% CPU）
**状态：** OPEN | **评论：** 3 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/42657)

**摘要：** 2-4 个并发子代理时 TUI 输入延迟 1-3 秒，动画卡顿。已在 Warp、Windows Terminal、WezTerm 三端复现，profile 显示渲染线程 CPU 占用 97%。

**关注理由：** 多子代理工作流是高级用户的核心场景，TUI 性能退化直接影响团队协作效率。

### 6. #43992 — [CLOSED] 打开同名项目文件夹时路径错误指向历史路径
**状态：** CLOSED | **评论：** 2 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/43992)

**摘要：** 在 D 盘打开名为 "xxx" 的项目后关闭，之后在其他盘打开同名项目时，路径仍然指向 D 盘的旧项目。

**关注理由：** 路径解析 bug 会静默操作错误项目，存在数据安全风险，值得专门修复。

### 7. #41847 — 权限对话框不渲染：后端阻塞于不可见提示
**状态：** OPEN | **评论：** 4 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/41847)

**摘要：** 后端生成了 3270 个权限提示但从未渲染给用户，导致后端一直等待无法到达的应答，应用表现为冻结。

**关注理由：** 对自动化场景影响极大——无人值守模式下权限系统完全失效，问题量级非常严重。

### 8. #12377 — [CLOSED][RFC] 成本追踪架构：子代理聚合 + 多模型正确性
**状态：** CLOSED | **评论：** 10 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/12377)

**摘要：** 提出统一架构解决多代理/多模型工作流中成本显示不准确的问题，包括子代理成本聚合（#11027）等。

**关注理由：** 成本可视化是企业采用的关键决策因素，虽然已关闭但相关讨论走向值得关注。

### 9. #43850 — Desktop 1.18.20 ChatGPT Plus OAuth 失败（403）
**状态：** OPEN | **评论：** 3 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/43850)

**摘要：** Windows 11 上 ChatGPT Plus OAuth 报 "Token exchange failed: 403"，完整环境信息已提供（Electron 42.3.3 / Node 24.15.0）。

**关注理由：** 登录链路阻断意味着完全无法使用，影响面大且需紧急处理。

### 10. #43829 — Deepseek-v4-flash-free 在免费层级不可用
**状态：** OPEN | **评论：** 5 | **👍：** 0
[链接](https://github.com/anomalyco/opencode/issues/43805)

**摘要：** 用户反馈 DeepSeek 免费模型已从模型列表中消失，且无法通过任何免费层级使用。另有 #43805 报告该模型在 Zen API 中存在但 TUI 下拉框中不显示。

**关注理由：** 免费模型可用性直接影响开发者 onboarding 体验，API 与 UI 不一致是典型的交付链路问题。


## 重要 PR 进展（Top 10）

### 1. #44029 — [CLOSED] 修复 Console 设备授权 URL 解析
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44029)

**内容：** 修复 Console API 返回的 `/console/device?...` 路径在拼接时丢失路径前缀（如 `/console`）的问题。同时 #43978、#44021 也在同一方向，从不同层修复同类 bug。

**关注理由：** 登录链路的三连修复，说明 Console 设备授权流程存在系统性缺陷，本轮集中清理。

### 2. #44000 — [CLOSED] 稳定代码生成中的契约命名
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44000)

**内容：** Effect client 端点与 group 符号改用 API 标识符（如 `SessionGetOutput`、`GroupSession`）而非遍历位置，匿名 OpenAPI 组件名也改为共享确定性命名。

**关注理由：** 保证跨构建的代码生成一致性，减少 SDK 使用方的 breaking changes。

### 3. #44025 — [OPEN] 容忍不完整的 agent 配置
**作者：** OpeOginni | [链接](https://github.com/anomalyco/opencode/pull/44025)

**内容：** 修复桌面端连接旧版本 opencode 服务端时，因 `normalizeAgentList` 遇到不完整配置导致整个应用崩溃的问题。

**关注理由：** 版本兼容性是桌面端分布式部署的常见痛点，此 PR 直接修复崩溃级 bug。

### 4. #44016 — [OPEN] 加固便携式 Shell 授权
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44016)

**内容：** 加固可选的便携式 shell 权限扫描器，防止不确定的 shell 输入在更窄的已保存授权下执行。基于 #44026 的行为保持型重构。

**关注理由：** 安全加固类 PR，涉及权限边界收紧，对多用户环境尤为重要。

### 5. #44027 — [OPEN] 按目录加载工作区会话
**作者：** OpeOginni | [链接](https://github.com/anomalyco/opencode/pull/44027)

**内容：** 修复 Settings → Workspaces 页面卡死问题：不再串行拉取服务器上所有会话，改为按目录过滤加载。

**关注理由：** 直接解决高负载场景下的 UI 冻结问题，对应 #44022。

### 6. #44002 — [OPEN] 恢复部分 Provider 故障
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44002)

**内容：** 对已产生部分输出的请求，自动恢复可重试的 provider 内部错误和限流故障。恢复可跨已持久化的本地工具执行，但在无法统一重放的 provider 托管活动处停止。

**关注理由：** 与 v1.18.20 的网络错误重试相呼应，进一步降低长任务失败率。

### 7. #44004 — [CLOSED] 继承 Fork 指令条目
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44004)

**内容：** Fork 会话时保留 session 级 API 指令条目，包括仍需与继承的指令检查点对账的删除墓碑。

**关注理由：** 确保 Fork 后指令状态完整一致，避免上下文丢失。

### 8. #44011 — [CLOSED] 稳定 Fork 消息 ID
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/44011)

**内容：** 使复制消息的标识在重放持久化 `session.forked` 事件时保持确定性，修复重建子会话时消息 ID 变化的问题。

**关注理由：** 与 #44008、#44001 同属 Fork 一致性系列修复，确保 Fork 可安全重放。

### 9. #43993 — [OPEN] 关闭远程 MCP 传输的 Bun Fetch 空闲超时
**作者：** viperx1 | [链接](https://github.com/anomalyco/opencode/pull/43993)

**内容：** `mcp.timeout` 虽已正确传递给 MCP SDK，但 Bun 运行时上静默超过 300 秒的调用会提前超时。此 PR 为远程传输禁用 Bun fetch 空闲超时。

**关注理由：** MCP 长耗时工具（如浏览器自动化）的稳定性关键修复，对应 #39584。

### 10. #42811 — [CLOSED] 新增会话已读状态
**作者：** kitlangton | [链接](https://github.com/anomalyco/opencode/pull/42811)

**内容：** 将会话未读状态从各 TUI 本地 tab 文件提升为 Session 的全局事实，使多个客户端（桌面、Web、TUI）的已读状态保持一致。

**关注理由：** 多端状态一致性是协作场景的基础设施建设，也是向服务端会话模型演进的重要一步。


## 功能需求趋势

### 1. 会话生命周期管理
- **归档/取消归档**（#24153，👍 11）：归档当前为单向操作，社区强烈要求支持恢复
- **会话标题显示项目名**（#38143）：多项目并行时快速定位上下文

### 2. 多模型与 Provider 兼容性
- **DeepSeek 免费模型可用性**（#43829、#43805）：API 存在但 UI 不显示，要求打通
- **OpenAI 兼容流式 reasoning 字段**（#35283）：`reasoning` vs `reasoning_content` 差异导致推理过程丢失
- **文本详细度注入引发网关故障**（#43911）：`gpt-5.*` 自动注入的 `textVerbosity` 破坏 Bedrock 路由

### 3. 性能与稳定性
- **Web UI 版本滞后**（#36232）：嵌入式前端构建版本未同步二进制版本
- **大文件 diff 渲染卡死**（#30906）：Windows 桌面端回归，v1.15.13 正常但 v1.16.0 卡死

### 4. 新平台与新集成
- **FreeBSD 支持**（#33219）：安装脚本硬编码 OS 白名单，排除 FreeBSD
- **MCP 工具定义懒加载**（#35376）：9 个 MCP server 时全部工具定义注入每个会话，token 开销巨大

### 5. 会话 Fork 与状态转移
- **Fork 指令条目继承**（#44004）：会话 Fork 时保留指令与删除墓碑
- **仅转移已定稿历史**（#44008）：快照导出不应携带运行中的投影


## 开发者关注点

### 🔴 痛点一：响应随机中断（最集中反馈）
- #38749、#34473、#43939 三个 issue 共同指向同一现象：模型响应无预警停止、无错误抛出、播放完成音效但内容不完整
- v1.18.21 针对未知 finish reason 的修复（#43892）反而引入了“反复续写已完成响应”的新回归（#43939）
- **诉求：** 需要更完善的 finish reason 处理策略与可见的诊断信息，而非简单继续或停止

### 🟠 痛点二：权限系统在黑屏下静默失效
- #41847：3270 个权限提示全部不可见，后端阻塞等待永不抵达的应答；对无人值守 CI/CD 场景影响严重
- **诉求：** 权限提示需要超时策略、可见性保障以及可配置的默认拒绝行为

### 🟡 痛点三：IDE 集成体验参差
- #6245（VSCode 快捷键冲突，👍 24）经过近 8 个月讨论才关闭，评论达 11 条
- **诉求：** 社区对 IDE 插件的快捷键/命令冲突处理有较高期待，需要更积极的响应节奏

### 🟢 痛点四：多会话/多窗口场景下的状态一致性
- #44030：多项目 tab 无法辨别当前激活项目，侧边栏缺失
- #38143：会话标题不含项目名，上下文切换困难
- #42811：未读状态在客户端间不同步
- **诉求：** 需要全局、跨端的会话状态视图

### 🔵 痛点五：macOS 路径规范化
- #44015：macOS 路径大小写/组件格式不规范，导致会话与目录过滤错乱
- **诉求：** 跨平台路径处理需要按平台特性做 canonicalization

---

**数据说明：** 本日报基于 2026-08-21 至 2026-08-22 的 GitHub 活动数据生成。Issue/PR 评论数可能为 undefined（新提交或无评论）。部分 issue 包含非英文内容，已按原样保留。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-22

> 数据来源：[github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)（镜像：earendil-works/pi）

---

## 今日速览

今日无新版本发布，社区讨论集中在**上下文压缩（Compaction）的触发时机与成本控制**这一核心痛点上：`#6879` 报告的“压缩在上下文超限后才触发”问题以 19 条评论和 17 个 👍 成为今日最热 Issue，另有关于压缩思考级别可配置（`#7553`）和按模型定制压缩策略（`#8133`）的讨论。键盘输入兼容性问题（Windows Terminal、Kitty）持续收到新反馈。PR 方面，`#8459` 修复了全屏模式下双击无法选中完整路径的问题，`#8428` 修复了会话重建时工具结果配对错误的问题。

- 热点：上下文压缩触发机制缺陷（#6879，19 评论）
- 趋势：按模型细粒度配置压缩策略、键盘协议兼容性修复
- 动态：9 个 PR 在过去 24 小时内有更新，其中 6 个已合并/关闭

---

## 社区热点 Issues（Top 10）

### 1. [#6879] 自动压缩在上下文超限后仍未触发，直至 Provider 报错
**作者**: alexanderkreidich | 评论: 19 | 👍: 17 | [链接](https://github.com/earendil-works/pi/issues/6879)

**摘要**: 在一次 GPT-5.6-sol 会话中，单个 agentic turn 运行超 2 小时，footer 显示上下文用量超过 100% 阈值后继续增长，直到 API 在 373k tokens 处拒绝请求，压缩才被触发。

**重要性**: 这是当前最受关注的 bug。上下文压缩是长会话的核心机制，触发时机设计缺陷会直接导致会话中断。19 条评论说明社区对此有大量讨论。作者建议在每次 agent 动作后检查压缩阈值，而非等 Provider 报错。

**社区反应**: 高热度，17 个 👍 表明大量用户遭遇过类似问题。评论区涉及压缩触发策略的多种改进方案。

---

### 2. [#8157] 将 grok-mermaid 迁移至 lovely-mermaid
**作者**: xl0 | 评论: 10 | 👍: 1 | [链接](https://github.com/earendil-works/pi/issues/8157)

**摘要**: grok-mermaid 是 grok 构建版 mermaid 渲染器的 1:1 移植，继承了原版大量边缘 case 和限制。lovely-mermaid 投入了更多精力，解析器质量更高，建议迁移。

**重要性**: Mermaid 图表渲染是 coding-agent 的重要功能，渲染器质量直接影响用户体验。10 条评论表明社区对渲染质量有明确对比和偏好。

---

### 3. [#2733] Windows Terminal 中 Backspace 和 Delete 键失效
**作者**: xingdongzhe | 评论: 11 | 👍: 1 | [链接](https://github.com/earendil-works/pi/issues/2733)

**摘要**: pi 从 0.62.0 升级到 0.64.0 后，Windows Terminal 中 Backspace 和 Delete 键不再按预期工作。

**重要性**: 这是老 Issue（3 月创建）但仍在活跃讨论，说明 Windows 平台的关键输入问题可能尚未彻底解决，或修复引入了回归。属于影响日常使用的 P0 类问题。

---

### 4. [#7130] Kitty 终端中 Backspace 删除两个字符（Kitty 协议未过滤）
**作者**: mister-booth | 评论: 9 | 👍: 1 | [链接](https://github.com/earendil-works/pi/issues/7130)

**摘要**: 在 Kitty 终端中使用 Kitty keyboard protocol 时，Backspace 会删除两个字符。原因是 Kitty 协议释放事件未被正确过滤。

**重要性**: 键盘协议实现是跨终端兼容性的难点。- 9 条评论说明这个 bug 影响面不小。与本日新增的 `#8442`（herdr pane 中 Backspace 失效）属于同类问题。

---

### 5. [#7553] 为压缩功能配置独立的思考级别/模型
**作者**: Saolence | 评论: 8 | 👍: 0 | [链接](https://github.com/earendil-works/pi/issues/7553)

**摘要**: 压缩（自动和手动）无法设置独立的思考级别，无条件复用会话当前的思考级别。在推理模型上运行自动压缩时，摘要的思考预算与正常对话无法分离。

**重要性**: 这是压缩成本优化的关键需求。在 reasoning 模型上，压缩本身会消耗大量思考 token，若能让压缩用较低思考级别或更便宜的模型，可显著降低成本。

---

### 6. [#7995] openai-responses: 缺少 anthropic 风格 cacheControlFormat，Claude 经 OpenRouter 成本增加 2.5 倍
**作者**: LukasParke | 评论: 7 | 👍: 0 | [链接](https://github.com/earendil-works/pi/issues/7995)

**摘要**: 基于 OpenRouter 对 pi-ai stream 实现的 870 次 trial 基准测试，openai-responses 实现缺少 Anthropic 风格的 prompt-caching 支持（`cache_control` 未出现在 `dist/api/openai-responses` 相关代码中）。

**重要性**: Prompt caching 是降低 API 成本的关键机制。2.5 倍的成本差异是具体可量化的数字，对重度用户影响显著。附带 870 次基准测试数据，说服力强。

---

### 7. [#8134] 经正向代理访问纯 HTTP Provider 时，Agent 在首次工具调用后停止
**作者**: fabiopili | 评论: 4 | 👍: 0 | [链接](https://github.com/earendil-works/pi/issues/8134)

**摘要**: 0.84.0 起，当 `HTTP_PROXY` 指向正向代理且 provider 的 `baseUrl` 为 `http://` 时，首次模型调用成功、工具执行后，下一次模型请求会挂起。

**重要性**: 代理/内网环境是常见部署场景。4 条评论表明有其他用户尝试复现或提供线索。这是一个会话中断类的高影响 bug。

---

### 8. [#8133] 按模型配置压缩设置
**作者**: Blue-B | 评论: 3 | 👍: 3 | [链接](https://github.com/earendil-works/pi/issues/8133)

**摘要**: 建议在 settings.json 中新增 `compaction.profiles` 映射，按 model id 设置不同的压缩参数（如 `reserveTokens`），当前全局值作为 fallback。

**重要性**: 与 #7553 属于同一需求方向：不同模型应使用不同的压缩策略。3 个 👍 在数量不多的问题中算较高，说明有相当比例用户认可该方向。

---

### 9. [#7779] 允许可信 Unix 用户共享 PI_CODING_AGENT_DIR
**作者**: AlecRosenbaum | 评论: 6 | 👍: 0 | [链接](https://github.com/earendil-works/pi/issues/7779)

**摘要**: `auth.json` 和 `models-store.json` 以 `0600` 权限写入，第一个创建/重写文件的用户成为唯一读写者，后续其他 Unix 用户进程无法访问共享状态。

**重要性**: 多用户环境下的基本可用性问题。虽已关闭（CLOSED），但 6 条评论说明社区对解决方案有讨论，值得关注最终的处理方式。

---

### 10. [#2644] 长会话崩溃：`JavaScript heap out of memory` (SIGABRT)
**作者**: fmagno | 评论: 4 | 👍: 0 | [链接](https://github.com/earendil-works/pi/issues/2644)

**摘要**: 长时间运行（约 30+ 分钟重度工具调用）后，pi 因 Node.js 堆内存不足崩溃并 SIGABRT。

**重要性**: 老 Issue（3 月创建）今日仍有讨论（已关闭）。长会话的内存管理是 Node.js 应用的经典问题，与 #6879 的上下文膨胀问题相关联。4 条评论说明维护者可能在评估解决方案。

---

## 重要 PR 进展

### 1. [#8428] fix(coding-agent): 重建会话上下文时重新配对工具结果
**作者**: adlternative | 状态: 已关闭 | [链接](https://github.com/earendil-works/pi/pull/8428)

**摘要**: 修复 #8166 中的会话损坏 bug：从持久化会话树重建上下文时（resume、压缩、分支导航），将工具结果与发起工具调用的助手消息重新配对，并丢弃孤儿结果。

**重要性**: 会话重建是压缩和 resume 的核心路径，配对错误会直接导致消息树损坏，影响长会话的可用性。

---

### 2. [#8459] fix(tui): 全屏模式下双击保留 `/` 和 `-` 作为词选择的一部分
**作者**: iggykimi | 状态: 已关闭 | [链接](https://github.com/earendil-works/pi/pull/8459)

**摘要**: 修复全屏模式下 `Intl.Segmenter` 将 `/` 和 `-` 视为词边界的问题。之前双击路径 `extensions/starline/fixed-editor/compositor.ts` 只选中一个组件，现在完整选中整个路径。

**重要性**: 直接影响开发者在全屏模式下复制/选择路径的效率。已关闭（merged），修复已在合入。

---

### 3. [#8443] feat(interactive-mode): experimental 标志下通过 Radius artifacts 分享
**作者**: cristinaponcela | 状态: 已关闭 | [链接](https://github.com/earendil-works/pi/pull/8443)

**摘要**: 使 `/share` 命令在 experimental 标志下使用 Radius artifacts 替代 gist。未登录时触发认证流程，然后生成 artifact。

---

### 4. [#8433] feat(coding-agent): 添加 `--exclude-extensions` 跳过指定扩展
**作者**: poucet | 状态: 已关闭 | [链接](https://github.com/earendil-works/pi/pull/8433)

**摘要**: 扩展加载原先全有或全无：完全自动发现或 `--no-extensions`。新增 `--exclude-extensions` 允许表达“我的常规扩展集，减去这些”。第三方扩展无法通过内部 guard 来控制自身是否加载，此参数绕过了这一限制。

**重要性**: 扩展管理灵活性的重要补充。当某个第三方扩展引起问题或与当前环境不兼容时，用户无需完全禁用所有扩展。

---

### 5. [#8424] fix(coding-agent): 丢弃失败的扩展工厂状态
**作者**: acmerfight | 状态: 开放 | [链接](https://github.com/earendil-works/pi/pull/8424)

**摘要**: 扩展工厂加载失败时：暂存 flag 默认值和 provider 操作直到工厂完成加载；工厂抛出或拒绝时丢弃暂存状态并移除事件总线监听器；后续通过失败工厂的 API 对象的调用将被拒绝。

**重要性**: 扩展加载失败时的清理逻辑完善。开放状态说明仍在评审中。

---

### 6. [#8422] fix(ai): 对 xAI Grok Build 省略 reasoning effort
**作者**: yearth | 状态: 开放 | [链接](https://github.com/earendil-works/pi/pull/8422)

**摘要**: xAI 拒绝包含 `reasoning.effort` 的 `grok-build-0.1` 请求。pi 目前会为显式推理级别包含此字段，也可能通过默认路径发送 `"none"`，导致 HTTP 400。添加 Responses 兼容性标志以省略该字段。

**重要性**: 新模型兼容性适配。xAI Grok Build 是相对新的模型，对 `reasoning.effort` 字段的处理有特殊要求。

---

### 7. [#8232] DONT MERGE: dev branch
**作者**: davidbrai | 状态: 开放 | [链接](https://github.com/earendil-works/pi/pull/8232)

**摘要**: 供 CI 和评论使用的开发分支，非功能性 PR。

---

### 8. [#4537] feat: Exit 别名（`/exit` 作为 `/quit` 的别名）
**作者**: AttAditya | 状态: 已关闭 | [链接](https://github.com/earendil-works/pi/pull/4537)

**摘要**: 为 `/quit` 添加 `/exit` 别名。修改了代码中所有 "quit" 出现的相关位置，更新了文档。

**重要性**: 与 #6193 对应。虽然是小改动，但符合主流 coding agent 的命令习惯，5 月创建今日合入，说明此类小而实用的改进最终会被采纳。

---

## 功能需求趋势

从今日 50 条 Issue 中提炼的社区最关注方向：

| 方向 | 相关 Issue | 说明 |
|------|-----------|------|
| **上下文压缩优化** | #6879, #7553, #8133, #8452, #8453 | 最核心的痛点。涵盖触发时机、思考级别/模型可配置、按模型定制参数、压缩提示词质量、手动全量压缩模式等。社区对压缩环节的成本控制和策略灵活性有强烈需求 |
| **键盘输入兼容性** | #2733, #7130, #8442, #8183 | Windows Terminal、Kitty、herdr pane 等多终端的 Backspace/Delete 问题持续出现。键盘协议（如 Kitty KKP）实现复杂，边界 case 多 |
| **Provider/模型适配** | #7995, #8454, #8455, #8450, #8422, #4742 | 新 provider 支持（SiliconFlow、Parasail.io）、推理强制模型适配（stealth/ox-alpha）、OpenRouter prompt-caching、Bedrock 凭证链。对新模型的适配速度是差异化优势 |
| **多用户/共享环境** | #7779 | 文件权限 0600 导致多用户无法共享配置。企业/团队使用场景的需求 |
| **扩展机制** | #5354, #8433, #8424 | 扩展系统需要更细粒度的控制（自定义 grep 命令、排除特定扩展、失败恢复） |

---

## 开发者关注点（痛点/高频需求）

1. **上下文压缩的“最后一刻”触发**：`#6879` 中压缩需要在上下文超限前主动触发，而非等 Provider 拒绝请求。用户在长任务（2 小时+ agentic turn）中会直接撞墙。

2. **压缩成本不可控**：推理模型上压缩会消耗大量思考 token（`#7553`），用户需要独立配置压缩的思考级别或使用更便宜的模型来降低开销（`#8133`）。

3. **跨终端键盘兼容性反复出问题**：Backspace/Delete 键在 Windows Terminal、Kitty、herdr pane 等场景中持续有 bug。键盘协议实现（如 Kitty KKP 过滤）是反复出问题的区域。

4. **缓存机制缺失导致成本翻倍**：OpenRouter 上 Claude 因缺少 prompt-caching 支持成本增加 2.5 倍（`#7995`），成本敏感型用户对此类问题反馈强烈。

5. **代理/内网环境稳定性**：正向代理下 plain-HTTP provider 会挂起（`#8134`），影响企业内网部署场景。

6. **长会话内存管理**：Node.js 堆内存溢出（`#2644`）与上下文膨胀（`#6879`）可能互为因果，用户需要更稳健的长会话保障。

---

## 今日总结

Pi 社区当前最核心的关注点是**上下文压缩机制的成熟度**——从触发时机到成本控制都尚未让用户满意。好消息是 `#8428` 已修复会话重建时的工具结果配对问题，这是压缩路径上的关键修复。键盘兼容性问题是另一个持续性的“牛皮癣”，多为协议实现的边界 case，建议维护者考虑统一抽离键盘协议处理层以减少回归。从 PR 合入节奏看，小而有用的功能（如 `/exit` 别名）也在持续推进，展现了良好的社区参与度。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-22** | 数据来源：github.com/QwenLM/qwen-code


## 今日速览

今日社区的焦点集中在**安全与 CI/CD 管道的加固**上：`wenshao` 主导的多轮 review 工作持续深入，围绕代码执行权限边界、容器隔离和 CVE 审计失败等问题展开密集讨论；同时，**MCP（Model Context Protocol）在 Windows 平台上的连接稳定性**成为新的用户痛点，多个 Issue 被集中反馈；功能需求方面，**会话管理**（模型恢复、HITL 恢复、会话归档冲突）和 **Plan 模式可配置化**是社区呼声较高的方向。


## 版本发布

**v0.21.14-nightly.20260821.9f2342d323**（2026-08-21）

- **feat(review)**：在 review 循环无法收敛时，向作者说明原因（PR #9461），提升 review 过程的透明度和可操作性。
- **fix(ci)**：停止 fallback 相关 CI 逻辑（内容截断，详见 Release 页面）。

另有**基准测试运行记录**（非代码发布）：
- `dsw-eas-tb-smoke-20260821-r1`：SWE-bench Verified 冒烟测试，状态 **SUCCEEDED**。
- `dsw-eas-full-20260821-r1`：SWE-bench Verified 500 + Terminal-Bench 2.0 89 全量基准，状态 **SUCCEEDED**。


## 社区热点 Issues（Top 10）

**1. [#9556] review: decide whether the pipeline should keep granting code execution as the invoking user**
- 作者：wenshao | 评论：7 | 状态：OPEN
- 为什么重要：这是多轮安全 review（#9221）中**所有未决发现的核心前提**——代码以 review 自身用户身份在工作树中执行。该权限在更早的步骤中被授予，此 Issue 要求从架构层面重新决策。属于安全架构的关键讨论。
- 链接：https://github.com/QwenLM/qwen-code/issues/9556

**2. [#5180] 主会话作为项目经理派遣 subagent，任务执行到一半崩溃**
- 作者：wunan067830-west | 评论：7 | 状态：OPEN
- 为什么重要：用户反馈长期存在的会话崩溃问题，涉及 **12 小时长会话**后 subagent 任务中断。社区关注度高，涉及多智能体协作的稳定性。
- 链接：https://github.com/QwenLM/qwen-code/issues/5180

**3. [#8993] Ubuntu 22.04 上公共扩展安装需要 Git 2.37，但 apt 仅提供 2.34.1**
- 作者：callmeYe | 评论：6 | 状态：CLOSED
- 为什么重要：影响**仍受支持的 LTS 发行版**用户。扩展安装的 Git 版本门槛过高，导致正常维护的 Ubuntu 22.04 用户无法安装扩展。已关闭，但社区反馈强烈。
- 链接：https://github.com/QwenLM/qwen-code/issues/8993

**4. [#5966] 0.19.3 UI 不定期错误，中文输入法完全无效**
- 作者：aspnmy | 评论：6 | 状态：OPEN
- 为什么重要：中文用户高频反馈的 **IME 输入法失效**问题，影响日常沟通与代码注释输入。该问题从 0.19.3 版本持续至今，社区关注度高。
- 链接：https://github.com/QwenLM/qwen-code/issues/5966

**5. [#9089] autofix: PAT 任务与不可信分支代码共享主机，需要 runner 级隔离**
- 作者：wenshao | 评论：6 | 状态：CLOSED
- 为什么重要：安全问题，涉及 **GitHub Actions 中 PAT 令牌与不可信代码在同一 runner 上执行**的风险。该问题无法从 Actions 步骤内部完全关闭，是 `wenshao` 安全 review 系列的一部分。
- 链接：https://github.com/QwenLM/qwen-code/issues/9089

**6. [#9693] Windows 上 Qwen Desktop 在 MCP 未激活时报告 MCP -32000 Connection closed**
- 作者：Gui8092 | 评论：4 | 状态：OPEN
- 为什么重要：**Windows 平台 MCP 连接稳定性**的新问题，即使 MCP 未激活也报错。与 #9675 同属 MCP 在 Windows 上的集中反馈，可能是平台兼容性缺陷。
- 链接：https://github.com/QwenLM/qwen-code/issues/9693

**7. [#9446] review: 实时服务见证机制（live-service witness）的残余缺口与共存声明**
- 作者：wenshao | 评论：4 | 状态：OPEN
- 为什么重要：`wenshao` 自我修正后的 review 问题，澄清了见证能力的实现位置（`agent-briefs.ts` 而非 SKILL.md），并指出剩余缺口。属于 CI/CD 验证机制深度讨论。
- 链接：https://github.com/QwenLM/qwen-code/issues/9446

**8. [#9699] CI: Dependency CVE 审计自 2026-08-21 起在每个 PR 上失败**
- 作者：harjothkhara | 评论：2 | 状态：OPEN
- 为什么重要：**所有 PR 的 CVE 审计步骤持续失败**（8 个漏洞，含 1 个高危），阻塞所有 PR 合并流程，属于影响面最大的 CI 问题之一，优先级 P1。
- 链接：https://github.com/QwenLM/qwen-code/issues/9699

**9. [#9639] 自动模式权限分类器在不可用时的 fail-open 回退问题**
- 作者：Gauss2024 | 评论：3 | 状态：OPEN
- 为什么重要：安全相关的**权限分类器在 provider 不稳定时 fail-open**——即当分类器无法访问时所有命令被放行。此行为是 #7331 的回归，影响非默认 provider 用户（如 OpenAI 兼容端点）。
- 链接：https://github.com/QwenLM/qwen-code/issues/9639

**10. [#9688] 归档活动会话可重建活动转录，造成活动+归档冲突**
- 作者：yiliang114 | 评论：2 | 状态：OPEN
- 为什么重要：**会话归档与运行中写入者的竞态条件**，导致同一 session ID 同时存在活动与归档副本，Web UI 可能显示冲突。涉及会话管理的核心一致性。
- 链接：https://github.com/QwenLM/qwen-code/issues/9688


## 重要 PR 进展（Top 10）

**1. [#9466] refactor: anchor rewind mapping to stable prompt identity**
- 作者：yiliang114 | 更新：2026-08-22 | 状态：OPEN
- 内容：将**提示词身份**作为用户可见轮次、模型历史、持久化会话、ACP rewind 和 fork 历史之间的唯一权威链接。改善会话恢复的一致性和可追溯性。
- 链接：https://github.com/QwenLM/qwen-code/pull/9466

**2. [#9576] feat(core): accept cross-session messages behind an inbound gate**
- 作者：qqqys | 更新：2026-08-22 | 状态：OPEN（autofix/takeover）
- 内容：允许**同一台机器上的多个 Qwen Code 会话互相通信**，通过 UNIX domain socket 接受新行分隔的 JSON 帧，并受策略门控。为多会话协作铺路。
- 链接：https://github.com/QwenLM/qwen-code/pull/9576

**3. [#9394] feat(channels): add DingTalk Workspace channel**
- 作者：qqqys | 更新：2026-08-22 | 状态：OPEN（autofix/takeover）
- 内容：新增**钉钉 Workspace 集成通道**，支持私信、@提及、文档通知和原生待办变更，扩展 Qwen Code 的协作渠道。
- 链接：https://github.com/QwenLM/qwen-code/pull/9394

**4. [#9273] feat(review): capture-tui —— 渲染声明获得像素证据**
- 作者：wenshao | 更新：2026-08-22 | 状态：OPEN（autofix/takeover）
- 内容：新增 `qwen review capture-tui` 子命令，在**私有 tmux 服务器**中驱动命令，捕获渲染证据（文本 + PNG），使 TUI 渲染问题可以基于像素而非代码推断来验证。
- 链接：https://github.com/QwenLM/qwen-code/pull/9273

**5. [#9623] feat(review): give the convergence observation a machine-readable half**
- 作者：wenshao | 更新：2026-08-22 | 状态：OPEN（autofix/takeover）
- 内容：在 #9461 的收敛诊断基础上，增加**机器可读的收敛观测输出**，让调用方可以程序化处理 review 循环不收敛的告警。
- 链接：https://github.com/QwenLM/qwen-code/pull/9623

**6. [#9624] feat(review): close Aone residual gaps —— composeUrl, test-plan routing, a1 version floor**
- 作者：wenshao | 更新：2026-08-22 | 状态：OPEN（autofix/takeover）
- 内容：补齐 **Aone Code review 支持**的三个残余缺口：真实的 PR/MR 链接、测试计划路由、a1 CLI 版本下限。
- 链接：https://github.com/QwenLM/qwen-code/pull/9624

**7. [#9513] fix(cli): Restore PR2A session behaviors**
- 作者：doudouOUC | 更新：2026-08-22 | 状态：OPEN
- 内容：**恢复 PR2A 会话行为**，具体内容需结合 PR 描述和评审意见确认。
- 链接：https://github.com/QwenLM/qwen-code/pull/9513

**8. [#9702] fix(vscode-ide-companion): anchor model selector dropdown to input form**
- 作者：yiliang114 | 更新：2026-08-22 | 状态：OPEN
- 内容：修复 VS Code 伴生聊天中**模型选择器下拉菜单悬浮覆盖消息列表**的问题，改为锚定到输入框（`absolute bottom-full` 向上展开）。
- 链接：https://github.com/QwenLM/qwen-code/pull/9702

**9. [#9638] fix(cli): deliver teammate messages at tool-round boundaries, not whole-task end**
- 作者：yiliang114 | 更新：2026-08-22 | 状态：OPEN
- 内容：Agent Team 中**队友消息现在在工具轮次边界交付**给 leader，而不是等整个多轮任务结束。大幅降低协作延迟。
- 链接：https://github.com/QwenLM/qwen-code/pull/9638

**10. [#9607] fix(core): demote balanced inline thinking blocks instead of failing the turn**
- 作者：yiliang114 | 更新：2026-08-22 | 状态：OPEN
- 内容：在 OpenAI 兼容端点上，混合思考模型可能在 `content` 中输出第二个合法的 `<think>`/`<thinking>` 块。此 PR 将其**降级处理而非直接失败**，提升混合思考模型的兼容性。
- 链接：https://github.com/QwenLM/qwen-code/pull/9607


## 功能需求趋势

从近 24 小时更新的大量 Issue 中，社区最关注的功能方向可归纳为以下五类：

| 方向 | 代表 Issue | 核心诉求 |
|------|-----------|---------|
| **会话/状态的持久化与恢复** | #9686（恢复每个 daemon 会话上次使用的模型）、#9664（恢复未回答的 ask_user_question HITL） | 用户期望 daemon 模式下的会话能够完整保存和恢复模型选择、待处理问题等运行时状态 |
| **Plan 模式可配置化** | #9694（可配置只读 shell 命令白名单） | 用户希望扩展 Plan 模式内置的只读命令集合，以支持自定义 CLI 的无提示调用 |
| **跨会话/跨平台消息同步** | #9576（跨会话消息）、#9394（钉钉频道） | 多会话协作和 IM 集成是明确的功能演进方向 |
| **UI 细节的定制化能力** | #9670（默认展开详细模式）、#9571（确认框默认选中） | 用户希望 UI 行为可配置，而非固化；交互细节的打磨需求持续存在 |
| **MCP 在 Windows 上的稳定性** | #9693（-32000 连接关闭）、#9675（会话间 MCP 断开） | Windows 平台 MCP 连接可靠性是新出现的高频反馈，可能与 stdio 传输或会话切换逻辑相关 |


## 开发者关注点

1. **安全与权限边界是核心议题**：`wenshao` 主导的多轮安全 review（如 #9556、#9089）持续深入 CI/CD 流水线的权限模型，社区对安全加固的讨论密度显著高于其他主题。

2. **CI 稳定性直接影响开发效率**：CVE 审计步骤在所有 PR 上失败（#9699，优先级 P1）是当前最紧迫的问题——它会阻塞所有合并，且已持续一天。

3. **Windows 平台体验问题集中爆发**：
   - **MCP 连接**：即使未激活也会报 `-32000 Connection closed`（#9693、#9675）
   - **终端 IME 低对比度**：Windows 下中文输入法候选词列表对比度极低（#9666）
   - 这些反馈表明 Windows 作为一级平台的体验仍需持续投入

4. **长会话稳定性是中文用户的长期痛点**：#5180（12 小时会话崩溃）创建于 6 月中旬仍为 OPEN，社区对 subagent 在长任务中的可靠性有持续诉求。

5. **Git 版本门槛影响扩展生态**：#8993 虽然已关闭，但暴露了扩展安装对系统 Git 版本的要求过高，在仍受支持的 LTS 发行版上造成用户流失。

6. **Review 循环的可观测性在持续增强**：从 #9461（告知作者为何不收敛）到 #9623（机器可读输出），review 工具链正在从"只给结论"向"可追溯、可编程"演进，官方对自身 CI/CD 工具的投入力度极大。

---

*本日报基于 GitHub 公开数据自动生成，部分 Issue/PR 描述存在截断，建议点击链接查看完整内容。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-22

## 1. 今日速览

今日社区核心动态围绕 **“监督化运行（Supervised Operation）”** 展开：维护者 M-Maciej 密集提交了 5 个相关 Issue（#5531-#5535）并合入一个大型 PR（#5535），旨在为长时间无人值守的 TUI 会话提供生命周期事件导出、控制套接字及 `/relaunch` 能力。此外，两项严重的稳定性问题被曝光：工作流执行失败在 TUI 中完全静默（#5528），以及子代理（Sub-agents）因墙钟时间超时丢失未提交工作（#5529）。功能开发方面，`DeepSeek-V4-Flash-Vision` 多模态模型支持请求已提交（#5541），补全命令弃用问题的修复 PR（#5530）也已就绪。

---

## 2. 版本发布

**过去 24 小时内无新 Release。**

---

## 3. 社区热点 Issues

### #5528 — 工作流运行静默失败：调度/架构错误从未在 TUI 中显现
- **作者**: Hmbown | **状态**: OPEN | **评论**: 0 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5528
- **摘要**: 今日两次工作流运行（评审扇出和分阶段构建流水线）在脚本评估阶段失败，但 TUI 中完全没有视觉反馈——没有 toast、状态行或工作流面板条目。操作者视角下，工作流看起来“正在运行”，但实际上没有任何可视化或日志记录。
- **重要性**: 🔥🔥🔥 这是**可靠性核心缺陷**。运行失败不可见意味着自动化流水线的信任度趋近于零，直接影响 CI/CD 场景采用意愿。TUI 应用的首要承诺是提供会话透明度，该 Issue 直接违背此承诺。

### #5529 — 子代理无法可靠执行：墙钟时间死亡丢失未提交工作，提供者路由失败阻塞调度
- **作者**: Hmbown | **状态**: OPEN | **评论**: 0 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5529
- **摘要**: 三个故障模式：1）两个工作子代理因墙钟预算耗尽中途死亡，且**未完成工作全部丢失**；2）提供者路由失败会完全阻塞后续调度；3）shell 工具需要大量工作区绕过。
- **重要性**: 🔥🔥🔥 直接摧毁 Fleet 代理功能的核心价值主张（代理化执行）。状态丢失是分布式任务系统的大忌，若无检查点/恢复机制，该功能在生产环境中不可用。

### #5534 — [Bug] 目标延续节奏在同轮调度路径上被绕过
- **作者**: M-Maciej | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5534
- **摘要**: PR #5508（`7eb4650`）新增的 `[goal] continuation_delay_seconds` 安静期在“轮内调度路径”上被完全跳过，恢复的 CLI 会话会立即触发后续 pass，导致目标延续节奏失效。
- **重要性**: 🔥🔥 功能实现存在**逻辑漏洞**，可能引发循环调用风暴或超额 API 消费。作为功能新增后立即暴露的问题，若不在下一个小版本修复会被视为质量缺陷。

### #5526 — 弃用的 shell 补全（Deprecated shell completion）
- **作者**: RepentStar | **状态**: OPEN | **评论**: 4 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5526
- **摘要**: 用户使用 pwsh，发现 `codew completions powershell` 生成的补全脚本内容和触发命令已过时（仍引用 `codewhale-tui`）。文档无相关说明，仓库中也找不到可修改位置。
- **重要性**: 🔥 用户首次接触的命令生成器就存在冲突，反映**文档与命令命名迁移的遗留问题**。同名 PR #5530 已在修复，说明问题已被维护者确认。

### #5541 — [增强] 多模态模型 DeepSeek-V4-Flash-Vision-Exp 支持
- **作者**: M-Maciej | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5541
- **摘要**: DeepSeek 家族首个多模态模型已发布，Codewhale 应支持在 `/model list` 中分配该模型，并使“视觉”功能正常工作。影响评估：巨大（网页开发、图像处理等任务）。
- **重要性**: 🔥🔥 多模态支持是当前 AI 工具的**主流方向**。对 Codewhale 而言，若 DeepSeek 的 Vision 模型可用而不被支持，将直接流失视觉相关任务用户。

### #5531 — [增强] 本地生命周期事件 outbox（JSONL + webhook），含 turn_stalled / turn_failed 事件
- **作者**: M-Maciej | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5531
- **摘要**: 在外部监督器（如 herdr）下运行长时间 Codewhale 会话时，需要事件导出机制，以支持无人值守场景（自动化测试、告警设置）的监控。当前缺乏任何事件透视能力。
- **重要性**: 🔥🔥 与 #5528 形成互补：当 TUI 无人在屏幕前时，必须通过外部机制感知会话状态。这是迈向**无人值守自动化运营**的基础设施级需求。

### #5533 — [增强] 监督化运行的控制面：每会话控制套接字 / 运行时后端
- **作者**: M-Maciej | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5533
- **摘要**: 需要 per-session 控制套接字（消息/中断/重启/状态查询），以及 `RuntimeBackendKind::External`，以支持外部监督器对会话的精细控制。
- **重要性**: 🔥🔥 与 #5531 一起构成“可管理性闭环”：不仅是“看得到”，还要“控得住”。CI 集成类场景的必备能力。

### #5532 — [增强] /relaunch — 将运行中会话切换到当前二进制
- **作者**: M-Maciej | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5532
- **摘要**: `/update` 安装新二进制后要求用户手动重启应用。更新器设计说明承认“此代码库没有自执行/重启模式，在 TUI 持握终端的情况下发明一个并非小事”。
- **重要性**: 🔥 影响开发迭代速度。每次更新强制重启打断工作流，在长时间运行的代理任务中不可接受。此功能与 #5531/#5533 构成完整“可运维性”拼图。

### #4069 — [文档/增强] 索引隐私控制（.codewhaleignore）
- **作者**: Hmbown | **状态**: OPEN | **评论**: 1 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/4069
- **摘要**: 搜索、工作集遍历和项目上下文组装未使用一级忽略文件来排除敏感或不相关路径。操作者无法像 `.cursorignore` 那样排除密钥、vendor 树或本地产物。
- **重要性**: 🔥🔥 安全和隐私治理的**基础需求**。企业用户在将代理接入生产代码库前，必须能够保证敏感文件不被 ingestion。此 Issue 已持续 45 天，是社区长期关注项。

### #5316 — EPIC-005：Codewhale TUI 板条箱分解（伞形追踪）
- **作者**: aboimpinto | **状态**: OPEN | **评论**: 11 | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5316
- **摘要**: 项目级史诗，追踪 CodeWhale TUI 的 crate 分解工作，所有子 EPIC 和 FEAT 完成时汇报至此，所有相关 PR 记录于此。
- **重要性**: 🔥🔥🔥 这是**大规模架构演进的中枢**。工具链正在从单体 TUI 向“外部命令形态”迁移（见 #5525），影响未来所有功能开发方式。11 条评论表明社区对演进方向有广泛讨论。

---

## 4. 重要 PR 进展

### #5535 — 监督化操作栈：生命周期 outbox、/relaunch、每会话控制套接字、目标延续安静期修复
- **作者**: M-Maciej | **状态**: OPEN | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5535
- **摘要**: 一个 PR 覆盖 5 个变更领域，全部聚焦于“机器可读的长时间会话监管”：生命周期事件 outbox（JSONL+webhook，含 `turn_start/end`、`turn_stalled`、`subagent_spawn/complete` 等）、`/relaunch` 命令、per-session 控制套接字、目标续延 quiet-period 修复。
- **重要性**: 🔥🔥🔥 **今日最大 PR**。涵盖 5 个 Issue 的修复，说明维护者正在快速推进“可运维性”体系。若合并顺利，将大幅提升 Codewhale 在无人值守场景的可用性。

### #5530 — [修复] 路由传统补全命令至公共二进制
- **作者**: wuisabel-gif | **状态**: OPEN | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5530
- **摘要**: 针对 #5526：`codewhale completions <shell>` 现在使用与 `codewhale completion <shell>` 相同的规范补全生成器，而不是转发到已弃用的 `codewhale-tui` 运行时。生成脚本使用公共 `codewhale` 命令名。
- **重要性**: 🔥🔥 直击用户痛点的修复，解决命令迁移遗留的兼容性问题。为后续移除旧运行时的拆解铺平道路。

### #5525 — [重构] TUI 工具组（FEAT-018）命令形状适配
- **作者**: aboimpinto | **状态**: OPEN | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5525
- **摘要**: 将 TUI 工具命令组（7 个命令文件）迁移至 FEAT-014/015 引入的外部命令形状。注册 `/alias` 等外部命令，执行边界改变但文件物理位置不变。
- **重要性**: 🔥🔥 这是 EPIC-005（#5316）的一部分，标志着 **TUI 从单体结构向插件化/命令化架构演进**的里程碑。为后续替代性 UI 前端（如 Web、桌面）铺路。

### #5523 — [重构] 从主循环提取工具调用阶段
- **作者**: bistack | **状态**: OPEN | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5523
- **摘要**: 将工具调用规划（`plan_tool_calls`）、审批与执行（`execute_planned_tools`）、结果处理（`process_tool_results`）从回合循环中提取为独立函数。保持原有控制顺序、可变状态流、取消行为和结果收集逻辑。
- **重要性**: 🔥🔥 纯粹的重构，但意义重大：**模块化是未来替换、扩展、测试的基础**。同时减少主循环复杂度，为添加更丰富的事件钩子（#5531）提供条件。

### #5524 — [特性] 多文件 read_lints 操作
- **作者**: wuisabel-gif | **状态**: OPEN | 更新: 2026-08-21
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5524
- **摘要**: 针对 #4070：现有 `lsp` 工具新增 `read_lints` 操作，支持多个工作区相对路径。复用会话 `LspManager` 传输池，避免创建新语言服务器生命周期。
- **重要性**: 🔥 LSP 集成是代理工具最重要的原生能力之一。批量 lint 读取大幅减少 token 消耗，对大型代码库的分析效率提升显著。

### #5526 相关依赖 PR 批次（#5540、#5539、#5538、#5537、#5390）
- **作者**: dependabot[bot] | **状态**: OPEN | 更新: 2026-08-21
- **链接**: #5540 https://github.com/Hmbown/CodeWhale/pull/5540 | #5539 https://github.com/Hmbown/CodeWhale/pull/5539 | #5538 https://github.com/Hmbown/CodeWhale/pull/5538 | #5537 https://github.com/Hmbown/CodeWhale/pull/5537 | #5390 https://github.com/Hmbown/CodeWhale/pull/5390

- **摘要**: 批量依赖升级：
  - `similar` 3.1.2 → 3.2.0（差异引擎）
  - `rio-vt` 0.5.19 → 0.5.25（VT 渲染）
  - `jsonschema` 0.46.10 → 0.49.9（需要跨大版本验证）
  - `docker/setup-buildx-action` 4.2.0 → 4.3.0
  - `rmcp` 2.2.0 → **3.1.2**（MCP Rust SDK 跨大版本，需验证兼容性）
- **重要性**: 常规维护，但 `rmcp` 3.x 是重要版本升级，涉及 MCP 协议实现变化，需关注兼容性测试。

---

## 5. 功能需求趋势

从今日所有 Issues 中提取的社区关注方向：

| 方向 | 代表 Issue | 热度 |
|------|-----------|------|
| **监督化/自动化运行** | #5528、#5529、#5531、#5532、#5533 | 🔥🔥🔥 最高优先级，维护者密集投入 |
| **外部可观测性**（事件导出、webhook、JSONL） | #5531 | 🔥🔥🔥 与监督化一体两面 |
| **多模态模型支持** | #5541 | 🔥🔥 DeepSeek Vision 模型落地 |
| **安全/隐私控制** | #4069 | 🔥🔥 长期存在的企业级需求 |
| **架构演进**（crate 分解、命令形状） | #5316、#5525、#5523 | 🔥🔥 宏观趋势 |
| **兼容性/遗留清理** | #5526 | 🔥 迁移遗留问题 |

**核心趋势**：Codewhale 社区正在将产品定位从“交互式聊天工具”升级为“**可编程、可审计的代理运行平台**”。重点投入在无人值守运行、事件流导出、精细控制面三大方向。

---

## 6. 开发者关注点（痛点与高频需求）

1. **静默失败问题**：工作流或子代理失败时 TUI 无任何可视反馈（#5528，#5529）——这是当前最大的信任危机。开发者需要一个“失败必须可见”的承诺。
2. **会话持久性和恢复**：子代理墙钟超时丢失全部工作且无 checkpoint（#5529），长期任务不可靠。高频需求方向：**增量持久化、恢复/重放机制**。
3. **模型支持滞后**：DeepSeek 已发布 Vision 模型而 TUI 尚未支持（#5541），社区希望快速跟进官方模型线。
4. **更新流程打断**：`/update` 后必须手动重启，破坏长时间运行的会话（#5532）。衍生需求：**热更新 / 会话迁移**。
5. **配置复杂度**：#5526 显示命名迁移残留问题（`codewhale-tui` vs `codewhale`）导致用户困惑。需求方向：**文档同步、命令归一化**。
6. **企业安全门槛**：#4069 被持续关注 45 天，社区认为 **`.codewhaleignore` 是采用的前置条件**——若无法排除敏感路径，企业不会接入。

---

**编辑后记**：今日社区节奏明显偏向“治理与架构”而非新功能堆叠——修复静默失败、增加外部控制、建立事件协议，是代理工具从“demo 可用”走向“生产可用”的必经之路。建议关注 #5535 PR 的合并状态，以及 #5528/#5529 是否会获得快速响应。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*