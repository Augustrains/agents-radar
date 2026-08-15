# AI CLI 工具社区动态日报 2026-08-15

> 生成时间: 2026-08-15 00:30 UTC | 覆盖工具: 9 个

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

**日期：2026-08-15** | 编制：资深技术分析师


## 1. 生态全景

当前 AI CLI 工具已从 "代码补全助手" 进化为 **"自主代理工作台"**，核心竞争聚焦于子代理架构、跨会话记忆、MCP 生态集成与多模型调度四大能力。今年市场呈现明显的 **"平台化与精细化并存"** 态势：头部工具（Claude Code、Codex）加速企业级功能补齐（身份转发、Admin API、沙箱策略），而社区驱动的工具（Pi、OpenCode）则在 TUI 体验与模型生态适配宽度上持续发力。值得警惕的是，**性能回退与安全误报成为本日跨工具最高频的共性痛点**（Claude Code 安全过滤器误报、Codex Windows 卡顿、Gemini CLI 子代理挂起），说明该赛道已从 "功能竞赛" 转向 "稳定性竞赛"。同时，**企业级可观测性与计费透明**（Admin API 缺口、静默回退计费、Token 用量波动）成为新共识，预示下一阶段将围绕治理能力展开差异化。


## 2. 各工具活跃度对比

| 工具 | 活跃 Issues | 主要 PR 数 | Release 情况 | 高频 Issue 热点（Top 1） |
|------|------------|-----------|-------------|------------------------|
| **Claude Code** | 10 | 4（2 条长期未合并） | v2.1.233 | Advisor 触发时 API 无响应（96 👍） |
| **OpenAI Codex** | 10 | 10（密集推进） | 5 个 Rust alpha 迭代 | Windows 11 卡死/掉帧（84 👍 / 101 评论） |
| **Gemini CLI** | 10 | 10（含 9 个 SSR Agent 驱动 PR） | v0.56.0-nightly | 子代理 MAX_TURNS 误报成功（P1） |
| **GitHub Copilot CLI** | 10 | 3（2 条为 CI 自动化迁移） | v1.0.81-0 | MCP OAuth RFC 8414 认证回归 |
| **Kimi Code CLI** | 4 | 未披露 | 无新版本 | Memory System 跨会话记忆（39 评论） |
| **OpenCode** | 10 | 10（V2 协议重构为主） | 未发布新版本 | 48 位 ID 时间戳回绕致会话失效（已修复） |
| **Pi** | 10 | 10（7 个已合并） | v0.84.2 | Windows 平台使用调研（27 评论） |
| **Qwen Code** | 10 | 10 | v0.21.12 系列 | 大会话恢复超时（P1，已关闭） |
| **CodeWhale**（原 DeepSeek-TUI） | 10 | 10（8 个已合并） | v0.9.8 | Agent 工具 32 字段 schema 过复杂 |

**综合观察**：Codex 与 Gemini CLI 的 PR 推进速度最快（各 10 条且半数以上已合并），但二者的 "元老级" 高热度 Issue（Codex #20214 已持续 4 个月；Gemini #21409 自 5 月待重测）表明 **"迭代快不等于修复快"**。Claude Code 虽仅 4 条 PR 但 v2.1.233 有实际新功能落地；Kimi 与 Copilot CLI 相对静默，但前者展现 "少而精" 的社区需求聚焦特征。


## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|------|---------|---------|
| **MCP 生态稳定性** | Copilot CLI（RFC 8414 回归）、OpenCode（缺少 type 字段容错）、CodeWhale（MCP OAuth） | OAuth 认证协议兼容性、MCP 配置容错、协议发现可观测性 |
| **子代理/多代理可靠性** | Gemini CLI（挂起/误报成功/权限绕过）、Copilot CLI（子任务冻结/OOM）、Qwen Code（ACP 子进程参数错误） | 执行状态真实性、递归子代理、资源上限控制、权限一致性 |
| **跨会话记忆/上下文一致性** | Kimi（Memory System 呼声最高）、Gemini（Auto Memory 无限重试+密钥泄漏）、Claude Code（150k vs 1M 窗口不一致） | 持久化记忆设计、记忆脱敏安全、上下文窗口行为透明 |
| **会话生命周期管理** | Claude Code（取消归档）、OpenCode（旧会话失效事故）、Qwen Code（恢复超时保留） | 归档/恢复闭环、中断后状态保持、跨设备接力 |
| **企业可观测性与计费透明** | Claude Code（Admin API 不含 OAuth 用户、静默回退计费）、OpenCode（余额/配额不重置）、Copilot CLI（BYOK 缓存破坏） | 用量计量准确、费用预警、身份转发、（企业）组织级策略同步 |
| **Windows/WSL 平台体验** | Codex（性能灾难）、Claude Code（权限误报）、Gemini（ripgrep EFTYPE）、Qwen Code（WSL SIGKILL） | 性能基线、权限判定准确、平台兼容性修复 |
| **TUI 渲染与交互细节** | Pi（单核满载）、CodeWhale（macOS 乱码）、Claude Code（提示无法折叠）、Gemini（resize 闪烁） | 流畅度、跨平台一致性、可配置性 |
| **本地/第三方模型接入** | OpenCode（动态模型发现 PR）、Pi（Baseten/Kimi 适配）、CodeWhale（预制模板诉求） | 简化配置、自动发现、模型能力矩阵同步 |


## 4. 差异化定位分析

| 工具 | 定位与核心优势 | 当前短板 |
|------|--------------|---------|
| **Claude Code** | **企业级深度集成**：GitLab MR、apps gateway 身份转发、Worktree 支持；背靠 Anthropic 模型生态（Advisor 多模型建议） | 安全过滤器误报率高、多模型切换稳定性不足、Windows 回归 |
| **OpenAI Codex** | **底层架构快速演进**：Rust 核心、权限快照协议化、沙箱强制 deny-read；ChatGPT 桌面生态联动 | Windows 性能长期未修复（4 个月+）、版本回退频发、日志写放大 |
| **Gemini CLI** | **SSR Agent 自修复模式**：Google 内部用 AI 代理批量修复社区 Issue（今日 9 个）；AST 感知代码理解、组件级评估体系 | 子代理状态误报、Auto Memory 安全缺陷、通用代理挂起 |
| **Copilot CLI** | **GitHub 生态深度绑定**：免 PAT CI 集成、Worktree 会话、Autopilot 多 agent；模型切换（GPT/Claude） | MCP OAuth 回归、企业模型目录同步缺陷、插件锁竞争 |
| **Kimi Code CLI** | **中文社区深耕**：记忆系统与跨设备会话为最高呼声；K2.5 模型工具调用优化 | 社区规模小、迭代节奏慢、Windows Shell 兼容性待打磨 |
| **OpenCode** | **开源的模型中立 TUI**：V2 协议重构、自定义 Provider 动态发现、LAN 模型自动发现；社区贡献活跃 | 核心稳定性事故（ID 回绕）、桌面版 UI 回归、认证体验混乱 |
| **Pi** | **性能与体验极客向**：Bun/TypeScript 单仓库、窗口化渲染解决长会话 CPU、全屏搜索；扩展生态快速扩展 | Windows/WSL 路径分散、登录限流、模型行为差异适配成本高 |
| **Qwen Code** | **大规模代码库工程化**：SWE-bench Verified + Terminal-Bench 2.0 验证链、review 体系工程化（锚点校验/延期队列）；架构治理投入大 | CI 稳定性、内存上限缺失、CLI/SDK 行为不一致 |
| **CodeWhale** | **模型兼容性广度**：45 个 provider 支持、DS4 本地模型一等公民、确定性 Auto-Review 双层模式 | 发布质量门禁不足（v0.9.8 后多处 CI 红牌）、Web UI 完全损坏、品牌更名过渡期 |


## 5. 社区热度与成熟度评估

| 成熟度 | 工具 | 判断依据 |
|--------|------|---------|
| **高成熟度（企业级）** | Claude Code | 功能迭代稳定（增量发布）、社区体量大（96 👍 级 Issue）、聚焦企业治理；但 PR 池小、社区贡献者参与度有限 |
| | OpenAI Codex | 架构演进激进（Rust 重写、权限协议化）、官方投入大（5 个 alpha/日）；但高频版本导致性能回退频发，信任度受挫 |
| **中高成熟度（平台建设期）** | Gemini CLI | SSR Agent 自修复机制独特、评估体系（76 个 E2E 测试）领先；但核心路径仍以 maintainer 为主，社区贡献集中在外围 |
| | GitHub Copilot CLI | 企业功能齐全（免 PAT、Worktree、Autopilot），但 OAuth 回归跨版本未修复，协议兼容性测试缺失 |
| **中成熟度（快速迭代期）** | OpenCode | 社区活跃（V2 协议重构、6 个一并关闭的模型发现 Issue）、架构稳定性未锁定，第三方集成需持续跟进 |
| | Pi | 合并效率高（7/10 已合并）、模型适配广度领先、社区口碑良好（性能优化共鸣）；但 Windows 策略未定 |
| | Qwen Code | 工程化程度高（E2E 验证链、review 体系）、架构治理自觉性强；但 CI 稳定性和资源管理仍是短板 |
| **早期/小众** | Kimi Code CLI | 社区聚焦度高（记忆系统被反复提及）但盘子小，迭代节奏慢（无 Release），适合观望 |
| | CodeWhale（原 DeepSeek-TUI） | 社区贡献者活跃（快速提交修复 PR），但发布后红牌暴露测试矩阵不足；品牌更名期需明确迁移路径 |


## 6. 值得关注的趋势信号

1. **"AI 修复 AI" 成为新范式**：Gemini CLI 的 SSR Agent 模式（AI 代理自动定位、修复、提交 PR 闭环）值得全行业关注——它可能重新定义开源维护的效率基准，未来 6 个月内可能被更多主流仓库效仿。

2. **性能回退引发 "版本信任危机"**：Codex 用户 "升级即卡顿、退出即恢复" 的反馈具有典型性；多个工具（Codex、Claude Code、OpenCode）均在最新版本引入回归缺陷。**建议**：关注各工具是否建立性能回归测试基线（尤其空闲态 CPU/内存）；对追求稳定的开发者，建议延迟 1-2 周采用新版本。

3. **企业治理成为分水岭**：Claude Code 推进身份转发、Copilot 补企业模型目录、Gemini 强化沙箱权限——"能否被企业采购" 将取决于 Admin API 完整度、用量计量准确性、审计日志能力。开源工具（OpenCode、Pi）若忽视此赛道，将在企业市场中边缘化。

4. **记忆系统是下一波功能红利**：Kimi、Gemini 对 Memory 的探索（含脱敏缺陷教训），以及 OpenCode 的会话失效事故，共同表明 **"上下文持久化" 将成为各工具差异化竞争的核心**。而记忆的隐私安全边界（#26525 的教训）也会成为监管与用户信任的高危议题。建议关注实现方案（文件/向量库）与安全设计的平衡。

5. **模型中立性成为长期竞争力**：OpenCode 的动态模型发现（一次关闭 6 个 Issue）、CodeWhale 的 45 provider、Pi 的 Baseten/Kimi 适配——**绑定单一模型商的工具（Claude Code、Codex）需警惕用户在模型选择自由度上的转向**。多模型调度与切换的稳定性（Claude Code #69238 的教训）将直接影响留存。

6. **Windows 不再是 "次要平台"**：Codex 的 Windows 灾难、Claude Code 的 Git Bash 回归、OpenCode 的 WSL SIGKILL——Windows 用户占比已达到 "不可忽视" 阈值。**对团队选型建议**：若团队含 Windows 开发者，务必关注目标工具在该平台上的已知问题清单与修复周期。

7. **TUI 体验竞争进入 "细节决胜期"**：从 Pi 的窗口化渲染、CodeWhale 的引用导轨，到 Gemini 的泰语字符删除——**终端 UI 的流畅度、多语言支持与交互精细度** 正成为开发者 "用脚投票" 的新维度，与功能深度同等重要。


**给技术决策者的建议**：
- **团队协作（企业场景）**→ 优先评估 Claude Code、Copilot CLI 的治理能力；需确认 Admin API 与计费透明特性已覆盖你的场景。
- **个人高效开发（多模型需求）**→ OpenCode 或 Pi 值得投入；两者的模型中立架构与社区活跃度是长期保障。
- **深度依赖 Google 生态** → Gemini CLI 的评估体系与自修复模式保证了较高的迭代质量，但需关注子代理状态可信度。
- **中文场景 + 长上下文代码任务** → Qwen Code 与 Kimi 各有侧重（工程化 vs 轻量），前者目前更成熟。
- **通用建议**：在 2026 年 Q4 之前，**所有工具**均建议锁定固定版本并延迟升级，待社区确认无严重回归后再跟进；对 8 月 15 日 OpenCode 的会话失效事故保持警惕，第一时间更新至修复版本。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止日期：2026-08-15 | 数据来源：github.com/anthropics/skills**


## 一、热门 Skills 排行

### 1. skill-creator 系列修复（最高关注度）
**PR #1298** — fix(skill-creator): run_eval.py 评估工具 recall 恒为 0%
- **功能**：修复 `run_eval.py`（skill-creator 的核心评估脚本）在所有系统上报告 `recall=0%` 的严重 bug——即优化循环在基于噪声做决策
- **社区讨论**：引用 #556（12 条评论的热门 Issue），提及 10+ 独立复现；另有 3 个关联 PR（#1099、#1050 专注 Windows 兼容性）
- **状态**：OPEN（3 个月未合并）
- **热度原因**：skill-creator 是社区开发者最常用的官方 Skill 之一，其评估循环完全失效直接影响所有下游技能开发
- 🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298)

### 2. testing-patterns — 测试模式 Skill
**PR #723** — feat: add testing-patterns skill
- **功能**：覆盖完整测试栈——测试哲学（Testing Trophy 模型）、单元测试（AAA 模式）、React 组件测试（Testing Library）、边界情况处理
- **社区讨论**：聚焦"什么该测 vs 什么不该测"的决策框架
- **状态**：OPEN（5 个月未合并）
- 🔗 [PR #723](https://github.com/anthropics/skills/pull/723)

### 3. ServiceNow 平台 Skill
**PR #568** — feat: add ServiceNow platform skill
- **功能**：覆盖 ServiceNow 全平台——ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD/CSM、SPM/PPM、漏洞响应、IntegrationHub
- **社区讨论**：定位为"宽平台助手"而非窄脚本工具，讨论集中在覆盖面与深度平衡
- **状态**：OPEN（最近更新于 2026-08-12，仍在活跃迭代）
- 🔗 [PR #568](https://github.com/anthropics/skills/pull/568)

### 4. document-typography — 文档排版质量 Skill
**PR #514** — Add document-typography skill
- **功能**：修复 AI 生成文档的典型排版问题——孤词换行（1-6 词溢出到下一行）、寡行段落（标题孤悬页底）、编号错位
- **社区讨论**：直击 AI 文档生成的普遍痛点，讨论围绕"用户很少主动要求好排版，但每份文档都需要"
- **状态**：OPEN（5 个月未合并）
- 🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

### 5. skill-quality-analyzer + skill-security-analyzer（元技能）
**PR #83** — Add skill-quality-analyzer and skill-security-analyzer to marketplace
- **功能**：两个元技能——质量分析器（五维评估：结构与文档/示例/资源等）和安全分析器
- **社区讨论**：将 meta-skill 加入 marketplace 的先例，讨论围绕评估维度权重
- **状态**：OPEN（9 个月未合并，生态最长寿 PR 之一）
- 🔗 [PR #83](https://github.com/anthropics/skills/pull/83)

### 6. SAP-RPT-1-OSS 预测 Skill
**PR #181** — Add SAP-RPT-1-OSS predictor skill
- **功能**：封装 SAP 开源表格基础模型（Apache 2.0，TechEd 2025 发布），用于 SAP 业务数据预测分析
- **社区讨论**：企业级 AI 场景进入 Skills 生态的标志性案例
- **状态**：OPEN（7 个月未合并）
- 🔗 [PR #181](https://github.com/anthropics/skills/pull/181)

### 7. self-audit — 推理质量门禁 Skill
**PR #1367** — feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate
- **功能**：交付前审计——先机械验证（检查所有声明的输出文件是否存在），再四维推理审计（按损害严重性排序）
- **社区讨论**：与 Issue #1385 的"三闸门流水线"提案联动
- **状态**：OPEN（1 个月，新近提案）
- 🔗 [PR #1367](https://github.com/anthropics/skills/pull/1367)

### 8. pyxel — 复古游戏开发 Skill
**PR #525** — Add pyxel skill for retro game development
- **功能**：面向 pyxel-mcp（Python 复古像素游戏引擎）的 Skill，覆盖 写→运行→捕获→迭代 工作流
- **社区讨论**：游戏开发垂直场景的稀缺 Skill，作者为 pyxel 引擎原作者 kitao
- **状态**：OPEN（最近更新 2026-07-15，仍在活跃）
- 🔗 [PR #525](https://github.com/anthropics/skills/pull/525)


## 二、社区需求趋势

### 1. 安全与信任（最大声量）
**Issue #492（43 评论，最高）**：社区技能在 `anthropic/` 命名空间下分发，构成信任边界滥用——用户可能对"看似官方"的技能授予过高权限。
- 直接关乎 Claude Code 的权限模型信任根
- 🔗 [Issue #492](https://github.com/anthropics/skills/issues/492)

### 2. Skill 分享与协作基础设施
**Issue #228（16 评论，8 👍 最高赞）**：组织级技能分享——当前需手动下载 .skill 文件、通过 Slack/Teams 传输、手动上传，流程割裂。
- 社区对 "Skill 生态的 GitHub" 的渴望
- 🔗 [Issue #228](https://github.com/anthropics/skills/issues/228)

### 3. skill-creator 可靠性（核心工具痛点）
**Issue #556（12 评论，7 👍）** + **#1169**：`run_eval.py` 在所有平台上触发率为 0%——评估循环完全失效。
- 这是"工具的 bug 比缺工具更痛"的典型——直接阻塞所有技能开发者的迭代效率
- 🔗 [Issue #556](https://github.com/anthropics/skills/issues/556) | [Issue #1169](https://github.com/anthropics/skills/issues/1169)

### 4. 上下文窗口管理
**Issue #1487**：`claude-api` 技能单次工具调用注入 ~156k tokens，直接耗尽上下文窗口。
- 大批量技能随 Claude Code 捆绑分发时的资源管理问题
- 🔗 [Issue #1487](https://github.com/anthropics/skills/issues/1487)

### 5. 新方向提案
- **compact-memory**（#1329）：符号化紧凑记忆表示，节省长时运行 agent 的上下文
- **agent-governance**（#412，已关闭）：AI agent 系统的策略执行/威胁检测/信任评分/审计轨迹
- 🔗 [Issue #1329](https://github.com/anthropics/skills/issues/1329) | [Issue #412](https://github.com/anthropics/skills/issues/412)


## 三、高潜力待合并 Skills

| PR | Skill | 亮点 | 活跃时长 |
|---|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator 评估修复 | 解决 10+ 独立复现的关键 bug，引用热门 Issue #556，社区验证充分 | 2 个月 |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | 直击 AI 文档排版普遍痛点，适用范围广 | 5 个月 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 覆盖完整测试栈，体系化程度高 | 5 个月 |
| [#568](https://github.com/anthropics/skills/pull/568) | servicenow | 企业平台全覆盖，最近仍在活跃更新（2026-08-12） | 5 个月 |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel | 由引擎原作者提交，垂直场景稀缺 | 5 个月 |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit | 新提案，与 Issue #1385 形成体系 | 1 个月 |

**观察**：所有高讨论度 PR 均处于 OPEN 状态，合并周期普遍超过 3 个月。`skill-creator` 和 `self-audit` 因直接修复核心开发者工具链，落地概率最高。


## 四、Skills 生态洞察

> **社区最集中的诉求是"元技能"的缺失——修复和组织 skill-creator 工具链、质量评估/审计标准、以及安全信任边界——而非新增更多垂直业务 Skill。** 即：社区不缺"用 Claude 做什么"，缺的是"如何规模化地做好 Skill 并信任它们"。

---

# Claude Code 社区动态日报

**日期：2026-08-15** | 数据来源：github.com/anthropics/claude-code


## 今日速览

今日焦点集中在 **v2.1.233 新版本发布**，新增 GitLab MR 支持与用户身份转发功能；社区最热议题是 **#69238 macOS 平台 Advisor 触发时 API 无响应**（96 👍、63 评论），以及 **#86619 Windows Git Bash 下权限误报导致频繁提示**（2.1.232 引入的回归）。此外，多起 **“安全过滤器误报”**（cyber/AUP 类）导致合法开发工作中断的 Issue 在今日集中更新，引发对安全策略精度的关注。


## 版本发布

### v2.1.233
- **链接**: https://github.com/anthropics/claude-code/releases

**主要更新内容：**
- 为 `--worktree` 标志和 `claude agents` 视图新增 **GitLab Merge Request URL 支持**（MR 显示为 `!N` 格式）
- 新增可选配置 `forward_user_identity`（适用于 Anthropic upstream 的 apps gateway 设置），可发送已登录用户身份作为 headers，便于代理后端识别用户

> 该版本为增量更新，重点在 GitLab 集成与企业代理场景的身份透传。


## 社区热点 Issues（Top 10）

### 1. [BUG] Advisor 触发时 API 无响应（macOS）
- **Issue #69238** | 作者: Samjin | 👍 96 | 💬 63 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/69238
- **摘要**: 使用 sonnet 为基底模型时，触发 Advisor（Opus 4.8 建议）后出现 "No response from API" 错误并反复重试（最长 2m25s）。社区反馈强烈，为当前最热门 Issue。
- **关注点**: 多模型切换场景下的 API 稳定性问题，影响面较大。

### 2. [BUG] Windows Git Bash 权限误报导致频繁提示
- **Issue #86619** | 作者: Aura-Intel | 👍 9 | 💬 9 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/86619
- **摘要**: 自 v2.1.232（auto-mode 推出）起，Git Bash 下只读 `cd` 复合命令被静态分析误判为需权限操作，产生**无法关闭的权限提示**。已在两台独立机器复现，与版本更新强相关。
- **关注点**: 高频权限误报严重影响 Windows + Git Bash 用户的工作流，属回归缺陷。

### 3. [FEATURE] 桌面应用支持取消归档会话
- **Issue #30869** | 作者: reyewon | 👍 57 | 💬 29 | 状态: CLOSED
- https://github.com/anthropics/claude-code/issues/30869
- **摘要**: 请求在桌面应用中提供取消归档（unarchive）Claude Code 会话的功能。虽已关闭，但 57 👍 表明需求强烈，或已在内部路线图中。
- **关注点**: 会话管理完整性的高优先级诉求。

### 4. [BUG] Analytics Admin API 不返回订阅/OAuth 用户
- **Issue #27780** | 作者: jbensamo | 👍 23 | 💬 26 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/27780
- **摘要**: Claude Code Analytics Admin API 无法查询通过订阅/OAuth 登录的用户数据，仅返回 API-key 用户，影响企业用量统计。
- **关注点**: 企业级可观测性缺口，长期未解决（2 月提出）。

### 5. [BUG/DOCS] 浏览器自动化工具与 Web Sandbox 代理不兼容
- **Issue #11791** | 作者: maorcc | 👍 16 | 💬 11 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/11791
- **摘要**: Playwright/Puppeteer/Selenium 在 Claude Code Web sandbox 中无法运行，因安全代理不支持 HTTPS CONNECT 隧道。属架构性限制，建议官方文档明确说明。
- **关注点**: Web sandbox 能力边界需文档化，避免开发者踩坑。

### 6. [BUG] VS Code 长提示无法折叠
- **Issue #72707** | 作者: ezwep | 👍 11 | 💬 2 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/72707
- **摘要**: VS Code 扩展中，长用户提示的展开/折叠按钮偶发无响应，导致提示词永久展开占用大量界面空间。
- **关注点**: UI 交互缺陷，影响日常使用体验。

### 7. [FEATURE] 禁用 Claude.ai Web/App 的提示建议
- **Issue #66117** | 作者: crossbodylead | 👍 10 | 💬 9 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/66117
- **摘要**: 请求在 Claude.ai Web/App 界面增加关闭 prompt suggestions 的选项，部分用户认为干扰输入。
- **关注点**: UI 可配置性需求，涉及产品设计取舍。

### 8. [BUG] 工作流代码审查 PR 评论静默失败
- **Issue #84474** | 作者: gsdali | 👍 0 | 💬 3 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/84474
- **摘要**: Workflow 驱动的代码审查在“发布 PR 评论”步骤静默失败，但仍报告“completed”且附带完整结论，误导用户。
- **关注点**: 状态报告不准确，影响 CI 流程可信度。

### 9. [BUG] 订阅过期后静默回退至旧凭证计费
- **Issue #86794** | 作者: jyminter | 👍 0 | 💬 2 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/86794
- **摘要**: claude.ai 订阅 OAuth 过期后，Claude Code 不提示重新认证，而是**静默回退**到遗留 API 凭证并继续消费 Console 配额。
- **关注点**: 计费透明度问题——用户可能在不知情下消耗付费额度，涉及财务风险。

### 10. [BUG] 同一模型不同会话自动压缩窗口不一致（150k vs 1M）
- **Issue #85205** | 作者: RockerMJ031 | 👍 0 | 💬 1 | 状态: OPEN
- https://github.com/anthropics/claude-code/issues/85205
- **摘要**: `claude-opus-5[1m]` 模型在部分会话中自动压缩窗口为 **150k**，而非 1M；`/context` 命令显示 "Auto-compact window: 150k tokens"，行为不一致。
- **关注点**: 上下文窗口配置不一致，影响长上下文任务可靠性。


## 重要 PR 进展

### 1. 修复安全引导：保留 Python 探针错误信息
- **PR #86746** | 作者: aayush598 | 状态: OPEN
- https://github.com/anthropics/claude-code/pull/86746
- **摘要**: 修复 #86709——原先 `sg-python.sh` 将探针 stderr 重定向到 `/dev/null`，所有解释器失败时用户仅见模糊错误。现保留错误输出并报告诊断信息。
- **价值**: 显著提升 Python 环境问题的可诊断性。

### 2. 新增 Shell 自动补全（bash/zsh/fish）
- **PR #86626** | 作者: 5hal1n | 状态: OPEN
- https://github.com/anthropics/claude-code/pull/86626
- **摘要**: 为 `claude` CLI 添加 bash（兼容 macOS 3.2）、zsh、fish 补全脚本，并附带 README 安装说明。
- **价值**: 改善 CLI 日常使用体验，降低上手成本。

### 3. 添加 pylint CI 工作流
- **PR #83890** | 作者: KrypticKode007 | 状态: OPEN
- https://github.com/anthropics/claude-code/pull/83890
- **摘要**: 创建 `pylint.yml`，为项目引入 pylint 静态检查 CI。
- **价值**: 提升代码质量门槛，属基础设施改进。

### 4. 补充 Claude Code 缺失来源说明
- **PR #41611** | 作者: tornikeo | 状态: OPEN
- https://github.com/anthropics/claude-code/pull/41611
- **摘要**: 为项目添加遗漏的 source 引用（描述较简略）。
- **备注**: 提交于 3 月，至今未合并，优先级较低。


## 功能需求趋势

从今日 Issues 中提炼的社区关注方向：

| 方向 | 代表 Issue | 热度信号 |
|------|-----------|---------|
| **会话管理增强** | #30869（取消归档）、#85272（Cowork 归档恢复） | 归档/恢复闭环缺失，桌面端尤甚 |
| **安全过滤器精度** | #71985/#71986/#71897 等多起 cyber/AUP 误报 | 合法 RE/固件分析被中断，需更细粒度策略 |
| **可观测性与计费透明** | #27780（Admin API）、#86794（静默回退）、#84607（Token 波动）、#83062（自动充值） | 企业对用量/费用的可控性诉求突出 |
| **Windows 平台体验** | #86619（权限误报）、#86555（MSIX 更新失败）、#86473（ECONNRESET） | Windows 用户已成为不可忽视的群体 |
| **IDE 集成深化** | #75863（VS Code 后台任务面板）、#72707（提示折叠） | 桌面与 IDE 功能对齐是持续诉求 |
| **多模型切换稳定性** | #69238（Advisor API 错误）、#86804（Fable 5 误触发切换） | 自动模型切换机制需更稳健 |


## 开发者关注点

1. **回归缺陷响应速度**：v2.1.232 的 Windows 权限误报（#86619）与 Mac 桌面更新失败（#86555）均为新版本引入，社区期待官方能更快响应并热修复。

2. **安全策略误报成痛点**：多起“合法逆向工程/固件分析被 cyber 过滤器拦截”的 Issue 集中关闭（#71964~#71992，共 9 起），均标记为 false positive 但仍导致会话中断。开发者希望安全过滤器增加**上下文感知**和更宽松的**白名单机制**，或在拦截前提供人工确认。

3. **计费透明性焦虑**：#86794（静默回退计费）、#83062（$995 自动充值）、#84607（Token 用量 17 倍波动）共同指向一个核心诉求——**用户需要清晰的用量计量与费用预警**，避免在不知情下产生高额费用。

4. **企业级缺口显著**：Admin API 不含 OAuth 用户（#27780）、apps gateway 身份转发（v2.1.233 已响应）表明 Anthropic 在积极补齐企业功能，但订阅/用量统计仍未闭环。

5. **上下文窗口一致性**：#85205（同模型 150k vs 1M 窗口不一致）提醒开发者**不要盲目信任模型规格**，应通过 `/context` 实测确认会话实际配置。

6. **贡献者活跃度提示**：PR 池较小（仅 4 条更新），其中 2 条长期未合并（#41611 达 4 个月+），社区参与度有提升空间。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-15

## 今日速览
过去24小时内，Codex 仓库发布了 5 个 Rust 版本的密集迭代（`v0.148.0-alpha.14` → `alpha.18`），同时社区对 **Windows 桌面端性能问题**的反馈达到峰值：多个高热度 Issue 直接点名“更新后整机卡顿”，其中 `#20214` 已积累 101 条评论、84 个赞，成为长期悬而未决的头号问题。此外，PR 侧在 **TUI 启动流程**、**权限快照协议化**、**Windows 沙箱规则** 等方向有密集推进，显示官方正在系统性加固底层基础设施。

---

## 版本发布
过去 24 小时内发布了 5 个 Rust 版本（均为 alpha 通道迭代）：

- **rust-v0.148.0-alpha.14 / .15 / .16 / .17 / .18** — 官方未提供详细变更说明。结合近期 PR 与 Issue 修复趋势，高频迭代推测聚焦于 TUI 启动稳定性、Windows 性能修复与权限系统重构。建议开发者关注 `#38641`（TUI 启动输入处理）及 `#38660`（Windows 沙箱 deny-read 规则）等相关合入。
- 链接：[Releases 页面](https://github.com/openai/codex/releases)

---

## 社区热点 Issues
以下 10 个 Issue 在过去 24 小时讨论最激烈或影响面最广：

| # | Issue | 热度/评论 | 为什么重要 |
|---|-------|----------|-----------|
| 1 | [Windows 11 Pro 上 App 频繁卡死/掉帧](https://github.com/openai/codex/issues/20214) | 101 评论 / 84 👍 | 持续近 4 个月的“元老级”性能问题，Plus 用户在高配机器（Ryzen 5 5600 + 32GB）上仍复现，说明 Windows 端性能优化进展缓慢，社区焦虑情绪集中。 |
| 2 | [Chrome 原生宿主重试循环吃满 CPU 并导致输入延迟](https://github.com/openai/codex/issues/38510) | 6 评论 | 昨日新上报，直指 `26.810.4967.0` 更新引发的严重回归——Chrome 集成导致键盘/鼠标输入延迟。与 `#38554` 疑似同源。 |
| 3 | [26.810.4967.0 让整台 PC 卡顿——退出 Codex 立即恢复](https://github.com/openai/codex/issues/38554) | 8 评论 | 最新版本严重性能回退，用户明确指出“退出后立刻恢复”。对发布质量提出质疑，是当下最烫手的问题。 |
| 4 | [未提权运行时导致系统级鼠标卡顿](https://github.com/openai/codex/issues/38546) | 8 评论 | 与 #38554 呼应，指向 `26.810.41047` 版本的共性问题——管理员/普通权限下均有性能劣化。 |
| 5 | [macOS 严重性能回退：100%+ CPU、10GB+ 内存、UI 频繁挂起](https://github.com/openai/codex/issues/38468) | 5 评论 | 性能问题不止 Windows，macOS 端（26.810.41047）同样爆发，证明近期版本存在跨平台性能退化。 |
| 6 | [macOS: SQLite 日志持续刷盘（rust-v0.142.0 后仍存在）](https://github.com/openai/codex/issues/29532) | 47 评论 | 老问题但热度不减——日志写放大导致磁盘 I/O 持续满载，部分修复无效，官方需彻底重构日志链路。 |
| 7 | [Windows 桌面端每秒钟拉起 powershell.exe 进行进程轮询](https://github.com/openai/codex/issues/25453) | 26 评论 | 高 CPU 占用的根因之一：进程发现机制存在严重设计缺陷，社区期待引入原生 API 或缓存轮询结果。 |
| 8 | [上下文压缩 85% 概率断开，丢失压缩前推理并转向无关计划](https://github.com/openai/codex/issues/31375) | 6 评论 | 影响 Pro 用户核心体验：长对话上下文压缩成功率极低，且失败后行为不可预测，严重打击可信度。 |
| 9 | [ChatGPT/Codex 空闲时引发系统级鼠标延迟 + 10% CPU 占用](https://github.com/openai/codex/issues/38583) | 10 评论 | 最新版 ChatGPT 应用（26.813.12317）“空闲空转”即占用 10% CPU，后台静默高负载问题已成投诉重灾区。 |
| 10 | [在另一个 VS Code 窗口打开活跃会话会静默转移所有权并允许并发回合](https://github.com/openai/codex/issues/38629) | 4 评论 | 并发会话一致性问题，对多窗口开发者是隐性风险——可能造成上下文错乱和 token 浪费，值得官方优先澄清设计意图。 |

---

## 重要 PR 进展
以下 10 个 PR 反映官方当前的技术发力方向：

| PR | 核心变更 | 技术意义 |
|----|---------|---------|
| [#38651 权限快照进协议](https://github.com/openai/codex/pull/38651) | 定义 `PermissionProfileSnapshot` 协议模型，核心权限状态直接存储快照 | 权限系统走向协议化、可审计化，为多端一致性和安全审计打基础。 |
| [#38660 Windows 沙箱强制 deny-read](https://github.com/openai/codex/pull/38660) | 所有执行路径及刷新流程中强制保留文件系统 deny-read 规则，不支持的策略“失败关闭”而非静默放行 | 安全边界收紧：宁可拒绝执行也不弱化保护，Windows 沙箱从“尽力而为”转向“强制闭环”。 |
| [#38641 强化 TUI 启动输入处理](https://github.com/openai/codex/pull/38641) | 终端探测期间的缓冲按键/控制序列不再误触选择或确认 | 修复启动期误操作隐患，是 TUI 体验精细化的关键一环。 |
| [#38642 启动期间保持编辑器可输入](https://github.com/openai/codex/pull/38642) | 在 TUI 就绪前显示临时编辑器，保留草稿文本与光标位置 | 大幅提升启动等待期的用户体验，减少挫败感。 |
| [#38643 首次登录前延迟显示启动编辑器](https://github.com/openai/codex/pull/38643) | 检测全新安装环境，在 onboarding 完成前不显示临时编辑器 | 避免新用户看到“空白编辑器”的困惑，完善首启流程。 |
| [#38647 新增跳过项目配置的覆盖开关](https://github.com/openai/codex/pull/38647) | `LoaderOverrides::ignore_project_config` 可跳过项目根发现与所有项目配置层 | 满足特殊场景（CI、受限环境）下的灵活加载需求。 |
| [#38650 规范化 gRPC 订阅过滤器命名空间](https://github.com/openai/codex/pull/38650) | 工具调用与订阅过滤器在匹配前统一规范化，空/缺失命名空间别名统一为 `functions` | 消除 gRPC 订阅中命名空间不一致的隐晦 bug，提升订阅可靠性。 |
| [#38662 泰语组合字符逐个删除](https://github.com/openai/codex/pull/38662) | 退格时泰语元音/音调符号按单个字符删除，而非整个字形簇 | 多语言文本编辑体验的精细化修复，I18N 诚意之作。 |
| [#38673 按环境执行权限配置](https://github.com/openai/codex/pull/38673) | `Ready` 环境配置可覆盖线程权限，为每个环境解析独立的权限配置 | 多环境下的权限精细化管控，对自动化/沙箱场景意义重大。 |
| [#38634 MCP 协议发现指标](https://github.com/openai/codex/pull/38634) | 为 MCP 客户端协议发现增加计数器和耗时指标，按 legacy/auto 模式与结果分类 | 可观测性建设：官方开始量化 MCP 兼容性表现，便于数据驱动修复。 |

---

## 功能需求趋势
从近期 Issues 和 PR 中可提炼出社区最关注的五个方向：

1. **Windows 性能与稳定性（压倒性第一）** — 约半数高热度 Issue 与 Windows 卡顿、输入延迟、CPU 占用有关。核心矛盾集中在进程轮询（powershell.exe 高频拉起）、HID 设备发现阻塞主线程、Chrome 原生宿主重试死循环等。社区期待官方将 Windows 端性能列入 P0 优先级。
2. **桌面端整体性能回退** — macOS 同样出现 100%+ CPU 与内存泄漏类报告，显示近期版本在跨平台性能上存在系统性退化，而非单一平台特例。
3. **会话生命周期与上下文可靠性** — 上下文压缩失败、会话所有权转移、任务切换卡顿等问题的讨论热度上升，用户对“对话不丢上下文”的诉求愈发强烈。
4. **权限系统精细化管理** — PR 侧多集中在权限快照、按环境配置权限、沙箱 deny 规则等，官方在权限可审计性、安全边界上明显加大投入。
5. **MCP（Model Context Protocol）与工具集成稳定性** — 新增 MCP 发现指标、Chrome 集成回归修复等，显示工具生态稳定性和可观测性成为阶段性重点。

---

## 开发者关注点
综合全部 50 条 Issues，高频痛点集中在以下四类：

- **Windows 平台“重灾区”持续失血**：从 `#20214`（4月上报至今未修复）、`#25453`（powershell.exe 轮询）、到昨日爆发的最新版本卡顿（`#38554`、`#38546`、`#38583`），社区对 Windows 端的信任正在流失。建议官方将“Windows 性能专项”纳入公开路线图并定期同步进展。
- **“杀鸡取卵”式的更新回退**：多个用户反馈从 `26.803` 升级到 `26.810` 后立刻出现严重性能劣化，且“退出 Codex 立即恢复”。社区普遍要求：版本发布前增加性能回归测试，尤其是针对空闲态 CPU 占用和输入延迟的基准门槛。
- **日志与磁盘写放大问题**（`#29532`）：macOS 端 SQLite 日志持续刷盘问题修复不彻底，表明日志子系统在极端场景下仍缺乏有效熔断或降级机制。
- **后台静默行为不透明**：进程轮询、HID 发现、Chrome 宿主等后台活动频繁且无用户可感知的开关或可视化。开发者呼吁提供“后台活动仪表盘”或至少提供禁用特定集成的配置项。

---

*本日报由 AI 自动生成，数据来源：github.com/openai/codex，统计窗口：2026-08-14 至 2026-08-15。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-15** | **数据来源：** github.com/google-gemini/gemini-cli


## 今日速览

今日社区动态聚焦于 **子代理（Subagent）稳定性** 与 **会话记忆（Memory）系统缺陷** 两大核心痛点。`#22323`（子代理 MAX_TURNS 恢复后误报成功）作为首要 Bug（P1）已获得官方修复 PR（#28815）；同时，由 `SandyTao520` 提交的 Auto Memory 系统系列问题（低信号会话无限重试、日志密钥泄漏、无效补丁静默跳过）引发广泛关注，涉及安全与资源消耗双重隐患。此外，夜间版本 v0.56.0-nightly.20260814 已发布，主要包含 E2E 测试稳定性与容量错误静默重试机制两项改进。


## 版本发布

**v0.56.0-nightly.20260814.gc0d192452**（Nightly）

- `test(e2e)`: 稳定 `file-system-interactive` 测试在慢速 CI 运行器上的表现（PR #28793，作者 DavidAPierce）
- `fix(core)`: 为容量（capacity）错误实现**上下文感知的静默重试**机制，并引入可用性 TTL（PR #28761，作者 DavidAPierce）


## 社区热点 Issues

**精选 10 个最值得关注的 Issue：**

### 1. 子代理 MAX_TURNS 恢复后误报成功 — `#22323`（P1）
**🔒 Maintainer Only | 12 条评论 | 状态：待重新测试**

`codebase_investigator` 子代理在达到最大轮次限制后，恢复流程将其结果标记为 `"success"` 且 `Termination Reason: "GOAL"`，尽管实际未完成任何分析。该问题直接掩盖了执行中断，影响任务结果的可靠性。

> **为什么重要：** 用户无法感知任务是否被截断，可能导致基于错误成功状态的后续决策。**官方已提交修复 PR #28815**（保留原始终止原因），社区关注度极高。

[查看 Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323) | [查看修复 PR #28815](https://github.com/google-gemini/gemini-cli/pull/28815)

### 2. 通用代理（Generalist agent）无限挂起 — `#21409`（P1）
**🔒 Maintainer Only | 8 条评论 | 👍 8 | 状态：待重新测试**

当 CLI 委托给 generalist agent 时，即使是创建文件夹这类简单操作也会无限挂起（用户等待长达 1 小时）。显式指示模型不使用子代理可规避此问题。

> **为什么重要：** 社区最高 👍 数 Issue 之一，直接导致核心功能不可用。已在 5 月进入待重新测试状态，但截至今日仍开放。

[查看 Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. 利用模型 bash 亲和力实现零依赖 OS 沙箱 — `#19873`（P2）
**🔒 Maintainer Only | 8 条评论 | 状态：机器人已分类**

提出利用 Gemini 3 模型原生擅长 POSIX 工具链（`grep`/`cat`/`sed`/`awk`）的特性，在不牺牲安全性的前提下，通过零依赖操作系统级沙箱 + 执行后意图路由，释放模型的原生能力。

> **为什么重要：** 涉及安全性与执行效率的架构级改进方向，反映了社区对**沙箱化安全执行**的持续诉求。

[查看 Issue #19873](https://github.com/google-gemini/gemini-cli/issues/19873)

### 4. 健壮的组件级评估体系 — `#24353`（P1）
**🔒 Maintainer Only | AIQ/Eval Infra | 7 条评论**

EPIC 跟踪：继 #15300 引入行为评估概念后，目前仓库已有 76 个评估测试，覆盖 6 个 Gemini 模型。本 EPIC 旨在构建更健壮的组件级评估体系。

> **为什么重要：** 评估体系是保证代理质量的基础设施，模型迭代加速背景下其优先级持续走高。

[查看 Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 5. 评估 AST 感知文件读取/搜索/映射的价值 — `#22745`（P2）
**🔒 Maintainer Only | 7 条评论 | 状态：机器人已分类**

EPIC 跟踪一组调研：AST 感知工具是否能为代码库探索带来价值——包括精确读取方法边界（减少误读导致的轮次浪费与 Token 噪音）、智能导航等。

> **为什么重要：** 可能显著降低 Token 消耗和提升代码理解精度，与 #22746（AST 感知 CLI 工具）协同推进。

[查看 Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

### 6. Gemini 对 Skills 和 Sub-agents 使用不足 — `#21968`（P2）
**🔒 Maintainer Only | 6 条评论 | 状态：待重新测试**

用户反馈：Gemini CLI 基本不会主动使用自定义 skills 和 sub-agents，除非显式指令。用户已配置 `gradle`/`git` 等 skills 并有详细描述，但模型仍不主动调用。

> **为什么重要：** 直接影响自定义扩展生态的实用性。反映了模型在工具选择（Tool Selection）上的策略仍需优化。

[查看 Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 7. Auto Memory 对低信号会话无限重试 — `#26522`（P2）
**🔒 Maintainer Only | 5 条评论**

Auto Memory 仅在提取代理成功用 `read_file` 读取会话记录后才标记为已处理。若代理判定会话为低信号而不读取，该会话将永远留在待处理队列，反复出现。

> **为什么重要：** 后台服务资源无限消耗的潜在 Bug，且会话累积可能影响后续提取效率。

[查看 Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 8. 确定性脱敏 + 降低 Auto Memory 日志量 — `#26525`（P2，安全）
**🔒 Maintainer Only | 4 条评论**

Auto Memory 会将本地记录（含密钥等敏感内容）送入模型上下文，脱敏发生在**内容进入模型之后**。此外，服务可能记录含敏感信息的 skill 内容。

> **为什么重要：** **安全漏洞**：敏感信息在脱敏前已暴露给模型。社区建议改为发送前确定性脱敏，并降低日志详细程度。

[查看 Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 9. Shell 命令执行完后卡在 "Waiting input" — `#25166`（P1）
**🔒 Maintainer Only | 4 条评论 | 👍 3**

简单 CLI 命令执行完毕后，终端仍显示命令为活动状态并提示 "Awaiting user input"，实际进程早已结束。高频复现。

> **为什么重要：** 直接影响日常使用体验，属高频交互 Bug。核心团队已关注，Effort 评估为 Medium。

[查看 Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 10. 子代理自 v0.33.0 起绕过权限设置运行 — `#22093`（P2）
**🔒 Maintainer Only | 3 条评论 | 状态：待重新测试**

用户更新到 v0.33.0 后，尽管所有配置中 agents 模式均设为 disabled，子代理（如 generalist）仍被自动调用。用户仅期望使用 MCP 功能。

> **为什么重要：** 权限控制被绕过属**安全与预期行为偏离**问题，对配置了严格权限策略的用户影响较大。

[查看 Issue #22093](https://github.com/google-gemini/gemini-cli/issues/22093)


## 重要 PR 进展

**精选 10 个重要 PR（按关注度排序）：**

### 1. [SSR Agent] 修复：保留子代理恢复期间的原始终止原因 — `#28815`（P1，Open）
**🔒 Maintainer Only | Size/S | 修复 #22323**

修复 `LocalAgentExecutor` 在子代理达到 `MAX_TURNS`/`TIMEOUT` 后，若在最后宽限轮成功调用 `complete_task`，会错误返回 `GOAL` 状态的问题。现在将保留原始终止原因。

[查看 PR #28815](https://github.com/google-gemini/gemini-cli/pull/28815)

### 2. [SSR Agent] 修复：防止 TUI 无限挂起，增加执行超时 — `#28812`（P1，Open）
**Help Wanted | Size/S | 修复 #21477**

从裸 Linux 终端启动时，交互式 TUI 可能在 "Initializing..." 无限挂起，原因是 `getProcessInfo()` 依赖 `execAsync` 执行 `ps` 命令。增加执行超时机制以打破死锁。

[查看 PR #28812](https://github.com/google-gemini/gemini-cli/pull/28812)

### 3. [SSR Agent] 修复：为 packages/cli tsconfig 添加 composite 标志 — `#28813`（P1，Open）
**Size/XS | 修复 #21911**

根构建/类型检查失败，因为 `evals/tsconfig.json` 引用了 `../packages/cli`，但后者未启用 `"composite": true`。此修复解除构建阻塞。

[查看 PR #28813](https://github.com/google-gemini/gemini-cli/pull/28813)

### 4. [SSR Agent] 修复：MessageBus.request 发布失败时静默挂起 — `#28816`（Closed）
**Size/S | 修复 #22588**

`MessageBus.request()` 中 `this.publish()` 是 floating promise，发布失败时请求会**静默挂起 60 秒**。添加失败注册以提前抛出。

[查看 PR #28816](https://github.com/google-gemini/gemini-cli/pull/28816)

### 5. [SSR Agent] 修复：保留钩子状态中执行中的子代理工具调用 — `#28817`（Closed）
**Size/M | 修复 #22589**

非根调度器（子代理）首次出现且无需审批的工具调用（如后台任务）会被过滤丢弃，未进入钩子状态。此修复保留这些调用记录。

[查看 PR #28817](https://github.com/google-gemini/gemini-cli/pull/28817)

### 6. 修复：ShellExecutionService PTY 文件描述符泄漏 — `#20916`（P1，Closed）
**Help Wanted | Size/M | 修复 #15945**

修复 PTY master 文件描述符在进程退出或手动 kill 后未正确关闭的问题，该缺陷会导致长时间会话中系统级 PTY 耗尽（macOS 限制为 511）。**已合入主分支。**

[查看 PR #20916](https://github.com/google-gemini/gemini-cli/pull/20916)

### 7. 修复：同步删除活动条目以阻止 PTY 内存泄漏 — `#27154`（P2，Closed）
**Size/M | 针对 #20916 的补充修复**

此前 `activePtys.delete(ptyPid)` 被包裹在 `cleanupLogStream()` 的 Promise `.then()` 中，若日志流后台任务挂起，PTY 条目和 headless 终端将永不被回收。修复后同步删除条目。

[查看 PR #27154](https://github.com/google-gemini/gemini-cli/pull/27154)

### 8. 功能：允许代理调用代理 — `#28738`（P2，Open）
**Help Wanted | Size/L | 修复 #22092**

允许子代理通过 `tools:` frontmatter 委托给其他子代理，或递归调用自身。突破当前子代理无法再调子代理的限制。

[查看 PR #28738](https://github.com/google-gemini/gemini-cli/pull/28738)

### 9. 修复：Windows 下 ripgrep eftype 错误 — `#25378`（P1/P2，Open）
**Help Wanted | Size/M | 修复 #22784**

Windows 下 `grep_search` 工具因 `child_process.spawn` 尝试执行与宿主架构不匹配（如 ARM 二进制在 x64 上）或损坏的下载二进制而报 `spawn EFTYPE`。

[查看 PR #25378](https://github.com/google-gemini/gemini-cli/pull/25378)

### 10. 修复：WSL2 剪贴板图片粘贴支持 — `#27588`（P2，Open）
**Help Wanted | Size/L | 修复 #22274**

检测 WSL 环境，通过 PowerShell interop 读取 Windows 剪贴板并保存为 PNG，与原生 Windows 路径共享辅助函数。解决 WSL2 下无法粘贴截图的问题。

[查看 PR #27588](https://github.com/google-gemini/gemini-cli/pull/27588)


## 功能需求趋势

从今日全部 Issues 中提炼出社区最关注的功能方向：

### 1. 子代理（Subagent）体系深化
- **递归子代理**：允许子代理调用其他子代理（#28738）
- **可观测性**：子代理轨迹应可通过 `/chat share` 分享（#22598），`/bug` 报告需包含子代理上下文（#21763）
- **自主性提升**：模型应更主动地使用 skills 和 sub-agents（#21968）
- **权限与安全**：修复子代理绕过权限设置的问题（#22093）；阻止破坏性行为（#22672）

### 2. Auto Memory 系统完善
- 低信号会话停止无限重试（#26522）
- 增加确定性脱敏、降低日志量（#26525，安全）
- 隔离或标记无效的内存补丁（#26523）
- 整体质量改进（#26516）

### 3. 代理执行稳定性与沙箱化
- 利用模型 bash 原生能力 + 零依赖 OS 沙箱（#19873）
- 治理临时脚本乱飞问题（#23571）
- 修复通用代理无限挂起（#21409）

### 4. 代码理解能力增强
- AST 感知的文件读取/搜索/映射价值评估（#22745、#22746）
- 组件级评估体系建设（#24353）

### 5. 终端交互体验优化
- 终端 resize 高性能 & 无闪烁（#21924）
- 外部编辑器退出后的画面损坏修复（#24935）

### 6. 架构与平台
- 环境变量在设置占位符解析前加载（#28597）
- Docker 基础镜像升级至 Node 24 / 22（#28602、#28603），Node 20 已 EOL
- `--list-all-sessions` 跨工作区会话管理（#28596）


## 开发者关注点

### 高频痛点 Top 3

| 痛点 | 相关 Issue | 影响 |
|------|-----------|------|
| **代理卡死/挂起** | #21409（通用代理挂 1 小时）、#25166（shell 命令卡 "Waiting input"）、#28812（TUI 初始化挂起）、#22588（MessageBus 静默挂起） | 核心交互链路不可用，用户体验受损最严重 |
| **子代理状态误报** | #22323（MAX_TURNS 误报 GOAL 成功） | 直接掩盖任务中断，影响结果可信度 |
| **Auto Memory 资源与安全** | #26522（无限重试）、#26525（密钥先入模型后脱敏） | 后台资源无限消耗 + 敏感信息暴露风险 |

### 关键观察

1. **子代理是整个生态的基石，也是当前最大的不稳定源。** 超过 60% 的热门 Issue 与子代理的行为、权限、状态报告相关。官方已开始用 SSR Agent 批量修复（今日有 9 个 SSR 驱动的 PR），但长尾问题仍多。

2. **SSR Agent 修复模式的启示：** 今日大量 PR 由 `[SSR Agent]` 前缀标记，表明 Google 内部已在用"自修复"模式解决历史 Issue。社区贡献者（help wanted）参与度较高，但核心路径（如 P1 级）仍以 maintainer 为主。

3. **安全与权限是隐忧。** 从 #26525（脱敏延迟）到 #22093（权限绕过），安全类问题虽数量不多，但均为 P1/P2 高优级别，开发者反馈强烈。

4. **功能上"让代理更自主"与"让代理更可控"的张力明显。** 社区既希望模型更主动使用工具（#21968），又希望严格限制权限（#22093、#22672）。如何在两者间平衡，可能是未来设计讨论的焦点。

5. **构建与平台债务开始显现。** 多个 PR 涉及 Node 20 EOL 升级（#28602、#28603）、TypeScript composite 配置修复（#28813），属于典型的项目扩展后的基础设施跟进。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-15** | 数据来源：[github/copilot-cli](https://github.com/github/copilot-cli)


## 今日速览

今日社区动态呈现两个鲜明主题：**模型可用性与配置问题持续发酵**——Claude 模型在企业账户下被误禁用、模型目录刷新机制缺陷等 Issue 获得大量关注；**MCP OAuth 认证回归（RFC 8414 issuer 不匹配）呈爆发态势**，Atlassian、GitLab 等多个远程 MCP 服务器均受影响，且 1.0.80 仍未修复。此外，插件依赖管理、BYOK 缓存破坏、Windows 平台崩溃等新问题也值得关注。


## 版本发布

**v1.0.81-0**（最新）：

- 改进：更新模型配置

**v1.0.80**（2026-08-14 发布）：

- 更新模型配置
- 包含修复和变更

> 注意：v1.0.80-1 为补丁版本，标注 "Fixes and changes"，但社区报告显示 MCP OAuth 问题在该版本中依然存在。


## 社区热点 Issues（Top 10）

### 1. [MCP OAuth 认证回归] Atlassian MCP OAuth fails with "Incompatible authorization server" — 1.0.80 仍复现
**Issue [#4480](https://github.com/github/copilot-cli/issues/4480)** | 👎 6 | 评论 4 | 状态: 已关闭

自 1.0.79 起，连接 Atlassian 远程 MCP 服务器时 OAuth 发现流程报错：`authorization server advertised an issuer that does not match the URL its metadata was discovered from (RFC 8414 §3.3)`。该问题在 1.0.78 及以前版本正常，属于明确回归。今日同主题 Issue [#4490](https://github.com/github/copilot-cli/issues/4490) 再次确认 1.0.80 中问题依旧。

**关注理由**：MCP 远程服务器认证是 CLI 与企业工具链集成的核心路径，连续多个版本未修复已引发开发者明显不满。

---

### 2. Reasoning effort 'medium' 不被 claude-haiku-4.5 支持
**Issue [#4345](https://github.com/github/copilot-cli/issues/4345)** | 👍 4 | 评论 6 | 状态: 打开

当 `copilot_cli_opus_medium_effort_default` 与 `copilot_cli_gpt_5_4_mini_for_explore` 两个服务端 feature flag 同时启用时，子代理执行期间反复报错 `Reasoning effort 'medium' is not supported for model 'claude-haiku-4.5'`。

**关注理由**：涉及服务端 flag 与模型能力矩阵的匹配缺陷，影响多模型自动切换场景的稳定性。

---

### 3. 企业组织已启用模型缺失于目录（Claude Sonnet 5/Opus 5、Kimi K3）
**Issue [#4390](https://github.com/github/copilot-cli/issues/4390)** | 👍 4 | 评论 6 | 状态: 打开

企业 Copilot Business 组织已明确启用的模型（如 claude-sonnet-5）在 CLI 中不可用，选择时报 `This model is disabled by your organization`。Kimi K3 也存在相同问题。

**关注理由**：企业管理员在设置中已启用但 CLI 不生效，属于配置同步缺陷，影响企业用户对最新模型的正常使用。

---

### 4. 所有 Claude 模型在企业账户下被禁用
**Issue [#4422](https://github.com/github/copilot-cli/issues/4422)** | 👍 3 | 评论 3 | 状态: 打开

个人企业账户下所有 Claude 模型（sonnet 5、4.8 等）均无法使用，尽管 GitHub Copilot 设置中显示已启用。回滚 CLI 版本无效。

**关注理由**：与 #4390 属于同一类问题的不同表现，影响面广（多模型、多版本均受影响），且回滚无法解决，指向服务端策略或目录同步问题。

---

### 5. GitLab MCP OAuth 元数据被 RFC 8414 issuer 不匹配拒绝
**Issue [#4439](https://github.com/github/copilot-cli/issues/4439)** | 👍 2 | 评论 3 | 状态: 打开

GitLab Self-Managed MCP 服务器使用 OAuth 2.0 动态客户端注册，CLI 1.0.79 因 RFC 8414 §3.3 issuer 不匹配拒绝认证。

**关注理由**：与 #4480 同根同源，说明此回归影响的不是单一服务商，而是所有遵循 RFC 8414 的 OAuth 授权服务器，属于协议兼容性层面的系统性问题。

---

### 6. 子任务冻结无响应
**Issue [#4306](https://github.com/github/copilot-cli/issues/4306)** | 👍 2 | 评论 3 | 状态: 打开

Autopilot 模式下使用 `/fleet` 调用自定义 agent/skill（speckit-implement 与 speckit-converge 循环），运行一段时间后子任务无响应。

**关注理由**：Autopilot 多 agent 协作场景的稳定性问题，长时间运行的自动化工作流容易卡死，影响 CI 场景的可用性。

---

### 7. MCP registry policy 获取返回 403，阻断 CI 中非默认 MCP 服务器
**Issue [#4346](https://github.com/github/copilot-cli/issues/4346)** | 👍 3 | 评论 2 | 状态: 已关闭

GitHub Actions 中使用内置 GITHUB_TOKEN（免 PAT 方式，copilot-requests: write）时，MCP all...（策略获取接口返回 403），非默认 MCP 服务器全部不可用。

**关注理由**：CI 免 PAT 方案是官方主推的自动化路径，MCP 策略获取被阻断意味着 CI 中无法使用用户自定义 MCP 工具，影响自动化能力边界。

---

### 8. 子代理 OOM 崩溃（V8 堆未达上限）
**Issue [#4499](https://github.com/github/copilot-cli/issues/4499)** | 评论 0 | 状态: 打开

v1.0.79 在长时间 autopilot 会话中崩溃：`FATAL ERROR: Committing semi space failed. Allocation failed - JavaScript heap out of memory`。关键细节：崩溃时 V8 堆仅使用约 607 MB（上限 4.3 GB），属主机内存提交失败而非堆限制。

**关注理由**：OOM 发生机制异常（堆远未达上限），可能指向内存碎片或底层资源管理问题，长时间运行的 autopilot 任务存在崩溃风险。

---

### 9. /restart 在 -w 创建的会话中失败
**Issue [#4493](https://github.com/github/copilot-cli/issues/4493)** | 评论 0 | 状态: 打开

使用 `copilot -w` 启动的会话执行 `/restart` 时，同时携带 worktree 选项和现有 session ID 导致选项冲突，无法恢复。

**关注理由**：worktree 模式与 restart 的组合是日常高频操作，属于命令交互层面的冲突 Bug。

---

### 10. 插件更新因文件锁失败（多会话场景）
**Issue [#4488](https://github.com/github/copilot-cli/issues/4488)** | 评论 1 | 状态: 打开

当多个 Copilot CLI 会话或 VS Code 窗口打开时（即使插件未被调用），插件更新因无关进程持有的文件锁报 `Access is denied`。

**关注理由**：多会话/IDE 并行的开发模式已成常态，插件更新被锁阻碍影响插件生态的迭代效率。


## 重要 PR 进展

> 注：当前共 3 条 PR，均已列出。其中两条为仓库自动化工作流迁移相关。

### 1. [已合并] 将 PR 自动化从 pull_request_target 迁移
**PR [#4449](https://github.com/github/copilot-cli/pull/4449)** | 作者: mrecachinas

将 invalid-label 自动化从 `pull_request_target` 迁移：使用 issue 级写权限 token 直接关闭无效 issue；以无权限的 `pull_request` 信号进行 PR 状态提示；特权操作使用 workflow 级 token。

**意义**：消除 `pull_request_target` 的安全隐患（恶意 PR 可利用其获取 secrets），是仓库供应链安全的加固。

---

### 2. [打开] 处理 fork PR 关联缺失场景
**PR [#4497](https://github.com/github/copilot-cli/pull/4497)** | 作者: mrecachinas

当 GitHub 未填充 workflow run 的 PR 关联信息时（fork PR 常见），writer 将利用可信的 workflow-run 元数据搜索并确认恰好一个打开的 PR 进行关联。

**意义**：配合 #4449 的迁移，确保 fork 贡献者的 PR 也能被自动化正常处理。

---

### 3. [已关闭] 临时 canary 验证 PR workflow 迁移
**PR [#4496](https://github.com/github/copilot-cli/pull/4496)** | 作者: mrecachinas

包含文档说明文件的草稿 PR，用于验证 fork 来源 PR 的自动化工作流迁移是否正常，验证后即关闭并删除临时 fork。

**意义**：属于 #4449 迁移的验证步骤，表明仓库维护者正在谨慎推进自动化管线的安全迁移。


## 功能需求趋势

从今日 Issues 中可提炼以下社区重点关注方向：

| 方向 | 具体诉求 | 代表 Issue |
|------|---------|-----------|
| **MCP 生态成熟度** | OAuth 认证兼容性修复（RFC 8414）、MCP tools/list 分页支持、服务器名大小写不敏感碰撞检测 | #4480, #4439, #4006, #4478 |
| **模型支持与目录管理** | GPT-5.6 reasoning.mode 参数支持；模型目录本地缓存刷新（新模型启用后需手动清缓存才生效） | #4495, #4494, #4390, #4422 |
| **插件体系完善** | 插件间依赖声明与自动安装机制（inter/intra marketplace）；插件更新文件锁问题 | #4487, #4488 |
| **会话与状态管理** | 恢复旧会话时自动沿用原 agent；/restart 与 worktree 兼容；停止操作不应丢失会话 | #4489, #4493, #4477 |
| **可观测性与协议支持** | OTLP protobuf 导出支持（当前仅 JSON，OTEL_EXPORTER_OTLP_PROTOCOL 被忽略） | #2934 |
| **稳定性与资源管理** | autopilot OOM 崩溃调查；BYOK 提示缓存破坏（transcript 重序列化） | #4499, #4500 |
| **体验细节** | 主题夜间变化（黑暗/光明模式切换异常）；权限配置中 allowed_directories 不生效；编辑权限请求超时 | #4485, #4482, #4486 |


## 开发者关注点

**1. MCP OAuth 回归是当前最大痛点**：多个 Issue（#4480、#4439、#4490）指向同一根因——RFC 8414 §3.3 issuer 元数据校验过严，导致 Atlassian、GitLab 等远程 MCP 服务器无法认证。从 1.0.79 引入至今 1.0.80 未修复，跨版本持续影响。建议维护者优先排查 OAuth discovery 流程的 issuer 校验逻辑，或提供宽松模式供企业用户选择。

**2. 企业模型目录同步机制存在缺陷**：多个企业用户遇到"设置中已启用但 CLI 不可用"的问题（#4390、#4422、#4494），且本地缓存不刷新导致新模型无法及时生效。建议增加模型目录的定期/手动刷新机制，并在报错信息中区分"组织未启用"与"本地目录未同步"两种场景。

**3. 新版本功能与稳定性不平衡**：1.0.80 的发布说明仅提到"模型配置更新"，但社区反馈的 MCP OAuth 回归、OOM 崩溃等问题均未在更新日志中体现。建议发布说明更透明地列出已知问题，建立更清晰的回归测试覆盖（尤其是 OAuth 协议兼容性场景）。

**4. 多会话/CI 场景下的资源竞争问题**：插件更新文件锁（#4488）、编辑权限请求超时（#4486）等问题在多会话并行场景下频繁出现。建议对全局资源（插件文件、权限状态）引入会话级隔离或锁等待机制。

---
*本日报由 AI 技术分析师自动生成，数据截止 2026-08-15。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-15**


## 今日速览

Kimi Code CLI 社区今日暂无新版本发布，但围绕 **Memory System（记忆系统）** 的讨论持续升温，其中 #1283 和 #1478 两条相关 Issue 今日均有更新，社区对跨会话记忆管理的需求愈发强烈。此外，跨设备会话接力（#2269）也是一大关注点，反映出用户对多环境协同工作的期待。


## 社区热点 Issues

过去 24 小时内共有 4 条 Issue 获得更新，以下为全部详情：

### 1. [增强] 记忆系统：跨会话的持久上下文（#1283）
- **作者**：CatKang | **更新**：08-14 | **评论**：39 | 👍 0
- **链接**：[Issue #1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **要点**：请求实现全面的 **Memory System**，在会话之间保留项目模式、用户偏好等上下文，涵盖 AI 自动管理的笔记和用户手动定义的指令两种形式。
- **社区反应**：该项目自 2 月创建以来已积累 39 条评论，今日仍有活跃讨论。评论区围绕实现路径（如文件存储 vs. 向量库）和与现有 agent.md 的关系展开了深入探讨。虽然 👍 为 0，但评论数量和持续活跃度表明这是社区长期以来的核心诉求。

### 2. [功能请求] 远程控制 / 多设备会话接力（#2269）
- **作者**：lucianalima777 | **更新**：08-14 | **评论**：6 | 👍 1
- **链接**：[Issue #2269](https://github.com/MoonshotAI/kimi-cli/issues/2269)
- **要点**：希望能在一种设备上启动 Kimi CLI 会话，并在另一台设备（笔记本、Web 或移动端）上无缝继续或远程控制该会话，以改善多环境工作流。
- **社区反应**：6 条评论中，用户主要讨论了实现可行性（如基于 WebSocket 的状态同步）以及 Kimi 移动端与 CLI 的联动场景。有一名用户表示该功能会显著改善其在公司电脑与个人电脑之间的切换体验。

### 3. [增强] 能否优化记忆层？（#1478）
- **作者**：hahy36 | **更新**：08-14 | **评论**：2 | 👍 0
- **链接**：[Issue #1478](https://github.com/MoonshotAI/kimi-cli/issues/1478)
- **要点**：中文用户反馈在大型项目中「很痛苦」，指出参考文档中未发现记忆层相关说明（仅提及 agent.md），并分享了从其他工具（如 OpenClaw）看到的记忆管理文件结构（SOUL.md / USER.md / MEMORY.md 等）。
- **社区反应**：该 Issue 今日重新被激活，评论中维护者尚未正式回复。用户分享的外部工具记忆结构可能为官方提供有价值的参考。

### 4. [增强/已关闭] 增强 Shell 工具，加入版本感知的 PowerShell 上下文（#1136）
- **作者**：QIN2DIM | **状态**：已关闭 | **更新**：08-14 | **评论**：0
- **链接**：[Issue #1136](https://github.com/MoonshotAI/kimi-cli/issues/1136)
- **要点**：在 Kimi K2.5（SGLang）测试中发现 Shell 工具在 Windows 上存在三个关键问题，显著降低了 Agent 在命令生成首轮（pass-1）的性能，包括模糊的 Shebang 处理等。
- **社区反应**：该 PR 相关 Issue 已于今日关闭（关闭原因未标注，推测并入对应 PR 或已解决）。虽是 Windows 平台特定问题，但对跨平台用户体验有直接影响。


## 功能需求趋势

从今日活跃的 Issue 来看，社区关注度最高的功能方向为：

1. **持久化记忆系统**（#1283、#1478 双线反馈）——是当前呼声最高的需求，用户不仅要求实现，更希望官方明确记忆层的设计文档和使用方式。
2. **多设备会话接力 / 远程控制**（#2269）——用户对跨设备无缝切换的 workflow 有强烈期待。
3. **Shell 工具的平台兼容性**（#1136）——Windows 下 PowerShell 的适配问题仍待关注。


## 开发者关注点

- **记忆管理是痛点**：无论是中文用户（#1478）还是英文用户（#1283）都反馈，在大型项目或长时间使用场景下，缺乏跨会话记忆导致上下文反复丢失，工作效率受限。参考文档中未收录记忆层说明被认为是一个文档缺口。
- **跨设备工作流诉求**：在混合办公（办公电脑 + 个人设备）成为常态的背景下，会话的迁移与远程控制被认为是提升 CLI 实用性的关键能力。
- **Windows 体验需打磨**：Shell 工具在 Windows 平台的兼容性问题虽已有关闭的 PR/Issue，但用户在评论区仍希望官方对 Windows 环境进行更系统的测试与支持。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-15** | 数据来源：github.com/anomalyco/opencode


## 今日速览

今日社区最重大的事件是 **[#42608：48 位 ID 时间戳回绕导致 2026-08-14 12:39:55 UTC 之前创建的所有会话失效](#issue-42608)**，大量用户报告会话无响应（#42605、#42611 等），已确认是核心 ID 生成器的时间戳回绕问题，官方已紧急关闭该 Issue 并推送修复。此外，**GitHub Copilot Provider 模型列表为空**（#42083）和**桌面版 v1.18.1 新布局隐藏 Plan/Build 切换 UI**（#36997）是另外两个高热度问题。PR 侧无重大新功能合并，主要是 V2 协议重构与多个自动化清理 PR 的合并。


## 社区热点 Issues

精选 10 个最值得关注的 Issue，按热度与影响面排序：

**1. [#42608：48 位 ID 时间戳回绕导致所有旧会话失效](https://github.com/anomalyco/opencode/issues/42608)** ⭐ 紧急
> 作者：klly14 | 评论：5 | 👍 3 | 状态：CLOSED（已修复）

**踩坑预警**：
- 所有 2026-08-14 12:39:55 UTC 之前创建的会话静默停止处理提示词，根本原因是 ID 生成器中 48 位时间戳回绕（`packages/opencode/src/id/id.ts`）。
- 这很可能是 #42605 和近期“agent 在已有会话中停止响应”问题激增的根本原因。
- 由于影响力巨大，官方已紧急修复并关闭。**建议所有用户立即更新**。

**2. [#36997：桌面版 v1.18.1 新布局隐藏 Plan/Build 切换 UI](https://github.com/anomalyco/opencode/issues/36997)** 🔥 高热度
> 作者：yesok99 | 评论：12 | 👍 6 | 状态：OPEN

**避坑指南**：自动更新到桌面版 v1.18.1 后，`newLayoutDesigns: true` 的新布局在 UI 中隐藏了代理切换指示器（Plan/Build 模式切换），用户无法看到当前激活的代理或进行切换。Tab 键也受到影响。这是目前评论最多的 Issue，影响所有桌面版用户，但尚未有官方修复。

**3. [#42083：GitHub Copilot Provider 显示零模型](https://github.com/anomalyco/opencode/issues/42083)**
> 作者：Keylessboi | 评论：8 | 👍 2 | 状态：OPEN

**排坑经验**：在 opencode 1.18.15（Arch 包）上，`github-copilot` Provider 从未出现在模型选择器中。`opencode auth login -p github-copilot` 认证成功，但 `opencode models github-copilot` 返回“Provider not found”，TUI 的 `/models` 也不显示任何 Copilot 模型。已确认所有模型均返回 `model_picker_enabled: false`。

**4. [#4581：Ollama Cloud 认证登录功能请求](https://github.com/anomalyco/opencode/issues/4581)**
> 作者：SerenityNrrd | 评论：14 | 👍 0 | 状态：CLOSED

**入坑手册**：用户希望直接在 OpenCode 中使用 Ollama Cloud，目前只能通过本地或服务器上的 Ollama 实例中转。这是评论数最多的历史 Issue，已正式关闭，但代表了社区对云端 LLM 服务直连的强烈需求。

**5. [#25000：DeepSeek V4 Pro via Zen：多轮工具调用中 reasoning_content 不一致](https://github.com/anomalyco/opencode/issues/25000)**
> 作者：WhiteGiverMa | 评论：7 | 👍 0 | 状态：CLOSED

**避坑指南**：通过 `opencode.ai/zen/go/v1` 使用 DeepSeek V4 Pro 时，多轮工具调用会间歇性失败，报错 `The reasoning_content in the thinking mode must be passed back to the API`。已确认根因是 DeepSeek V4 Pro 在工具调用过程中丢失/不一致处理 `reasoning_content` 字段。已修复关闭。

**6. [#24615：Plan Agent 权限绕过（默认配置失效）](https://github.com/anomalyco/opencode/issues/24615)**
> 作者：nikitakot | 评论：9 | 👍 0 | 状态：CLOSED

**入坑提醒**：默认的 Plan Agent 可以编辑文件。显式配置权限后会被尊重，但默认 Plan Agent 的权限设置会丢失。涉及 `opencode.json` 中的配置 diff。已关闭。

**7. [#41518：gpt-5.6-luna 经 OpenCode Go 中继访问返回 403](https://github.com/anomalyco/opencode/issues/41518)**
> 作者：123lyc5 | 评论：6 | 👍 0 | 状态：OPEN

**踩坑预警**：通过 opencode.ai 的 “OpenCode Go” 中继访问模型 `gpt-5.6-luna` 时返回 403，报错“This model is not available in your region”。使用有效凭证仍复现。**注意**：该 Issue 标题和摘要为中文，反映了中文用户社区的使用情况。

**8. [#38791：消息 ID 不可按时间排序时运行循环无法退出](https://github.com/anomalyco/opencode/issues/38791)**
> 作者：dkindlund | 评论：6 | 👍 0 | 状态：OPEN

**排坑经验**：`SessionPrompt.runLoop` 通过**纯字符串比较**判断回合是否结束，这仅对 OpenCode 自生成的 ID（内嵌时间戳）有效。任何第三方导入的、ID 不按时间顺序排列的会话可能导致循环陷入死循环，直到 Provider 返回 400。

**9. [#37489：切换模式或压缩期间上下文缓存失效导致性能问题](https://github.com/anomalyco/opencode/issues/37489)**
> 作者：ducon43 | 评论：5 | 👍 1 | 状态：OPEN

**避坑指南**：当使用本地 LLM（vLLM 或 Ollama 等推理引擎）时，切换模式或执行上下文压缩会导致严重的性能问题。社区关注度高，目前仍在讨论中。

**10. [#42626：Bash 工具子进程在 stdout 大量小写入时被 SIGKILL](https://github.com/anomalyco/opencode/issues/42626)**
> 作者：sdiazbarraza | 评论：3 | 👍 0 | 状态：CLOSED

**入坑参考**：在 WSL（Ubuntu 24.04）上运行 `pytest tests/` 等产生大量小写入的命令时，Bash 工具子进程会被 SIGKILL 杀死。已关闭。


## 重要 PR 进展

精选 10 个重要 PR（含 V2 协议重构与历史清理合并）：

**1. [#42669：从协议模式推导 Promise 适配器](https://github.com/anomalyco/opencode/pull/42669)**（OPEN）
> 作者：kitlangton | 更新：2026-08-15

**技术要点**：将逐字段的 Promise 插件 API 翻译替换为基于 V2 `HttpApi` 契约的 Schema 驱动适配器。Promise 插件现在获得与生成客户端相同的请求/响应转换，包括 `session.create.title`、品牌 ID、DateTime 毫秒时间戳等。**这是一个重大的架构重构，值得关注。**

**2. [#42667：统一补丁路径解析](https://github.com/anomalyco/opencode/pull/42667)**（OPEN）
> 作者：kitlangton | 更新：2026-08-15

**功能说明**：统一 V2 补丁工具的路径和权限资源，与 write/edit 已使用的 `LocationMutation` 服务保持一致。修复了补丁工具私有解析路径导致的资源不一致问题。

**3. [#42662：MCP 服务器配置缺少 type 时快速失败](https://github.com/anomalyco/opencode/pull/42662)**（OPEN）
> 作者：shreeyachand | 更新：2026-08-15

**修复内容**：许多为 Claude Code 编写的 MCP 配置 JSON 对象不包含 `type` 和 `enabled` 字段，OpenCode 现在会在缺少这些必需字段时明确报错而非静默失败。关闭 #41229。

**4. [#42663：持久化 Web 搜索 Provider 选择](https://github.com/anomalyco/opencode/pull/42663)**（CLOSED）
> 作者：thdxr | 更新：2026-08-15

**新功能**：将 Web 搜索 Provider 的同意选择持久化到文件支持的配置文档中，替代 KV 状态存储。Web 搜索现在支持固定的 Provider 优先级。

**5. [#42666：使用 Location VCS 状态](https://github.com/anomalyco/opencode/pull/42666)**（OPEN）
> 作者：opencode-agent[bot] | 更新：2026-08-15

**修复内容**：从目录级 VCS 存储中提取新会话 Git 状态，与 TUI 数据模型保持一致。全局项目元数据作为没有当前分支的 Git 仓库的后备方案。为已知的本地分支添加回归测试。

**6. [#42660：为自定义 Provider 添加动态模型发现](https://github.com/anomalyco/opencode/pull/42660)**（OPEN）
> 作者：Gr33ndev | 更新：2026-08-14

**新功能亮点**：为自定义 OpenAI 兼容 Provider（如 LiteLLM、LM Studio 等）添加动态模型发现。关闭 #13891、#29308、#28999、#25624、#23327 和 #26863 共 6 个相关 Issue。**这是一个社区呼声极高的功能**。

**7. [#27554：本地 LAN Provider 发现 + 自动模型发现](https://github.com/anomalyco/opencode/pull/27554)**（OPEN）
> 作者：androidand | 更新：2026-08-14

**功能说明**：在 `/connect` 中添加 `Local (LAN)` 发现，结合 mDNS 与 OpenAI 兼容服务器。关闭 #6231 和 #27553。经过长期打磨，该 PR 仍在开放状态，但代表性很强——社区对 LLM 生态本地化接入的诉求。

**8. [#42656：将 Worktree 路由移出 experimental 命名空间](https://github.com/anomalyco/opencode/pull/42656)**（CLOSED）
> 作者：jlongster | 更新：2026-08-14

**重构内容**：将 worktree API 从实验性 URL 命名空间提升为顶层资源，例如 `/api/experimental/project/:projectID/worktree` → `/api/worktree/:projectID`。V2 协议趋于稳定。

**9. [#36943：保持被中断的会话停止](https://github.com/anomalyco/opencode/pull/36943)**（CLOSED）
> 作者：opencode-agent[bot] | 更新：2026-08-14

**修复内容**：修复简化版 V2 运行协调器中，中断后旧提示词重新唤醒会话的问题。通过持久化准入序列隔离，保证中断后会话保持停止状态。自动化清理合并。

**10. [#36916：排队并发子代理问题](https://github.com/anomalyco/opencode/pull/36916)**（CLOSED）
> 作者：lucas-gaitzsch | 更新：2026-08-14

**修复内容**：收集根会话树中的所有待处理问题，按请求 ID 排序，并保持活动请求始终被选中（聚焦）。关闭 #36915。


## 功能需求趋势

从今日所有 Issues 中提炼的社区最关注功能方向：

| 方向 | 代表 Issue | 状态 |
|------|-----------|------|
| **自定义 Provider / 模型动态发现** | #27553（OPEN）、#42660（PR）、#27554（PR） | 高热度，已有实现 PR |
| **Claude Code 兼容性** | #42662（MCP 配置容错）、#41909（/approve 命令） | 社区持续要求对齐 Claude Code 体验 |
| **本地 / LAN LLM 接入** | #27554（mDNS 发现）、#37489（本地推理性能） | 本地模型用户痛点集中 |
| **OAuth / 认证配置灵活性** | #33966（OAUTH_CALLBACK_HOST 可配置） | 自定义部署需求 |
| **新模型 / 新 Provider 支持** | #4581（Ollama Cloud）、#42664（Nara Router）、#42385（DeepSeek V4 Flash Free） | 持续增长的需求 |
| **性能与稳定性（会话不响应）** | #42608（ID 回绕）、#42605、#42657（TUI 高 CPU） | 今日最严重的事故类问题 |


## 开发者关注点

- **核心稳定性冲击**：48 位 ID 时间戳回绕（#42608）导致所有旧会话失效是今日最大事故，大量用户“会话不响应”类 Issue（#42605、#42611、#42594 等）均与此相关，官方已紧急修复。
- **TUI 与桌面端 UI 问题**：桌面版 v1.18.1 新布局隐藏 Plan/Build 切换（#36997）和 TUI 在高并发子代理时 CPU 占用 97%（#42657）反映了 UI 层仍有较多体验问题。
- **GitHub Copilot 集成不稳定**：Provider 显示零模型（#42083）直接影响了依赖 Copilot 的用户。
- **支付与配额体验混乱**：多起用户反馈“付费后无余额/配额不重置”（#42637、#42606、#42215），这类问题对信任度影响很大，需尽快改进。
- **Bash 工具稳定性**：WSL 下子进程被 SIGKILL（#42626）以及 Shell 输出捕获问题（#36796）在自动化流程中影响明显。
- **V2 协议持续重构**：大量 PR（#42656、#42669、#42667）表明 V2 架构正在快速演进中，API 稳定性尚未锁定，第三方集成方需持续跟进。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-15

## 今日速览

Pi 发布 v0.84.2 版本，引入全屏转录搜索与可配置默认工具两项新特性。社区方面，Windows 平台使用体验讨论（#7547）持续升温，成为当前最热议题；针对 TUI 性能瓶颈（#6665）和 Copilot 登录限流（#7850、#8010）的修复进展值得关注。此外，多项针对模型适配（Baseten DeepSeek V4 Flash、Kimi 缓存计数）的 PR 已合并，体现了社区在模型支持广度上的持续投入。


## 版本发布

**v0.84.2**（过去24小时内发布）

主要新特性：
- **全屏转录搜索**：支持在全屏模式下搜索并导航匹配结果，详见 [TUI Fullscreen Viewport 文档](https://github.com/earendil-works/pi/blob/v0.84.2/packages/coding-agent/docs/keybindings.md#tui-fullscreen-viewport)。
- **可配置默认工具**：允许用户自定义启动时加载的默认工具集。

> 链接：https://github.com/earendil-works/pi/releases


## 社区热点 Issues（Top 10）

1. **#7547 [OPEN] Windows 平台使用调研** — *评论 27 · 👍 1*
   Windows 开发者数量庞大，但 Pi 在 Windows 上的运行方式多样，团队希望聚焦精力于最佳路径。这是目前社区最活跃的讨论帖，牵涉文档、开箱体验与 bug 修复优先级。

   https://github.com/earendil-works/pi/issues/7547

2. **#6187 [CLOSED] WSL 内 GitHub Copilot 登录挂起** — *评论 26 · 👍 0*
   设备授权完成后 Pi 客户端未检测到状态变化，导致登录永久挂起。影响 WSL 用户核心体验，已关闭说明有修复或 workaround。

   https://github.com/earendil-works/pi/issues/6187

3. **#5223 [CLOSED] Anthropic thinking blocks 导致 400 错误** — *评论 17 · 👍 6*
   多轮对话中 Opus 4.8 自适应思考导致请求失败。社区高赞，反映高级推理模型与 Pi 的兼容性问题受关注。

   https://github.com/earendil-works/pi/issues/5223

4. **#5023 [CLOSED] 终端无故滚动至顶部** — *评论 12 · 👍 2*
   模型输出时终端随机跳转至会话开头。看似小问题但频繁触发，影响日常使用，已关闭说明已定位或修复。

   https://github.com/earendil-works/pi/issues/5023

5. **#6665 [OPEN] TUI 流式输出时单核满载** — *评论 12 · 👍 3*
   根因指向未缓存的 `Intl.Segmenter` 与逐块 Markdown 重建。长会话性能关键瓶颈，标记为 inprogress。

   https://github.com/earendil-works/pi/issues/6665

6. **#7850 [CLOSED] Copilot 登录 429 限流** — *评论 9 · 👍 7*
   组织拥有 20+ 可用模型时登录失败。企业用户高赞问题，已关闭疑似有修复方案。

   https://github.com/earendil-works/pi/issues/7850

7. **#8096 [CLOSED] Z.AI Coding Plan 引用已移除模型** — *评论 5 · 👍 1*
   `glm-5.1` 已从 models.dev 移除但默认配置仍引用。典型的配置漂移问题。

   https://github.com/earendil-works/pi/issues/8096

8. **#8092 [CLOSED] pnpm 扩展依赖解析失败** — *评论 5 · 👍 0*
   jiti 无法解析 pnpm 隔离 node_modules 布局中的扩展依赖。影响使用 pnpm 的开发者。

   https://github.com/earendil-works/pi/issues/8092

9. **#8010 [CLOSED] Copilot 登录 429（个人用户）** — *评论 4 · 👍 2*
   与 #7850 同根因，个人用户切换账号触发限流。关闭状态表明已有明确处理。

   https://github.com/earendil-works/pi/issues/8010

10. **#7787 [OPEN] Bash PI_* 指南引发非必要权限提示** — *评论 3 · 👍 0*
    默认指南导致模型在无关任务中执行 `env` 检查。行为优化类问题，有对应 PR 已提交。

    https://github.com/earendil-works/pi/issues/7787


## 重要 PR 进展（Top 10）

1. **#8149 [CLOSED] fix(ai): 移除无效 OpenAI session 头**
   修复带下划线 header 被 HTTP/1 代理拒绝的问题（Envoy 400），影响生产环境稳定性。

   https://github.com/earendil-works/pi/pull/8149

2. **#8148 [CLOSED] fix(coding-agent): 限定 bash PI_* 指南到会话相关问题**
   解决 #7787，避免模型在普通任务中执行 `env`，减少不必要权限提示。

   https://github.com/earendil-works/pi/pull/8148

3. **#8146 [CLOSED] fix(ai): 限制 Baseten DeepSeek V4 Flash 输出上限为 384k tokens**
   适配 Baseten 实际服务能力，避免因超出限制导致请求失败。

   https://github.com/earendil-works/pi/pull/8146

4. **#8143 [CLOSED] perf(tui): 全屏转录窗口化**
   全屏模式下仅渲染可视区块，显著降低长会话 CPU 占用，直接回应 #6665 性能问题。

   https://github.com/earendil-works/pi/pull/8143

5. **#8139 [CLOSED] feat(ai): ChatGPT OAuth 图像生成**
   复用 OpenAI Codex OAuth 基建，支持免 API Key 生成/编辑图像，扩展 Pi 多模态能力。

   https://github.com/earendil-works/pi/pull/8139

6. **#8124 [OPEN] feat(ai): xAI 模型切换至 Responses API 并默认 Grok 4.6**
   跟进新模型发布，提升与 xAI 服务的兼容性与默认体验。

   https://github.com/earendil-works/pi/pull/8124

7. **#8120 [OPEN] feat(coding-agent): 实验性 append 压缩**
   复用系统提示与工具定义，压缩后可命中 provider 缓存，降低长会话 token 成本。

   https://github.com/earendil-works/pi/pull/8120

8. **#8119 [OPEN] fix: 统计 Kimi 缓存 tokens**
   解决 #8075，将 `usage.cached_tokens` 计入 cache-read，提升用量统计准确性。

   https://github.com/earendil-works/pi/pull/8119

9. **#8112 [OPEN] fix(coding-agent): 扩展入口 realpath 后再交由 jiti**
   修复 pnpm 隔离布局下依赖解析失败问题（#8092）。

   https://github.com/earendil-works/pi/pull/8112

10. **#8110 [CLOSED] fix(tui): 选择复制走宿主剪贴板**
    修复 VTE 终端（GNOME Terminal 等）中"Copied!"提示与实际剪贴板不一致问题。

    https://github.com/earendil-works/pi/pull/8110


## 功能需求趋势

1. **新模型/Provider 适配活跃**：SiliconFlow（#8113）、Amazon Bedrock Mantle（#6216）、Anthropic Vertex（#5262）、ChatGPT 图像生成（#8139）、xAI Grok 4.6（#8124）均在近期有 PR 推进，模型生态扩展是当前最活跃方向。

2. **性能优化集中在 TUI 渲染**：#6665 单核满载与 #8143 窗口化渲染表明社区对长会话流畅度有强诉求，全屏模式体验优化成为重点。

3. **Copilot/企业登录体验**：#7850、#8010 等 429 限流问题集中反馈，企业在多模型场景下的登录稳定性是刚需。

4. **压缩策略精细化**：#8120 append 压缩、#8133 per-model 压缩配置，社区对 token 成本控制与缓存利用率提出更高要求。

5. **扩展生态完善**：#8144 技能自动补全、#8132 命令补全位置设置、#8100 会话级模型状态，说明扩展 API 的灵活性与易用性正在成为关注点。


## 开发者关注点

1. **Windows/WSL 体验分散**：#7547 讨论热度极高，Windows 下多种运行方式（原生/WSL/容器）导致团队难以聚焦，社区期待官方明确推荐路径与资源分配。

2. **TUI 性能与稳定性**：#6665 单核满载、#5023 无故滚动、#8036 大 diff 渲染崩溃，终端 UI 在长会话与大数据量场景下的可靠性是高频痛点。

3. **登录/鉴权流程脆弱**：#6187 WSL 挂起、#7850/#8010 429 限流、#8131 OAuth refresh 崩溃，多个环节在特定环境下失灵，影响上手体验。

4. **模型兼容性细节**：#5223 thinking blocks 格式、#8105 strict:null 参数反直觉、#8115 仅推理响应绕过重试，模型行为差异导致的功能异常是持续痛点。

5. **配置与依赖管理**：#8096 默认模型引用失效、#8092 pnpm 依赖解析失败，开发者在真实项目结构中遇到的配置漂移与包管理兼容问题值得重视。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-15** | **数据来源：** [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)


## 1. 今日速览

今日最值得关注的动态有两点：一是 **v0.21.12 系列版本持续推进**，核心更新集中在 Web Shell 的体验增强（工作区文件上传）和会话管理修复，同时一个以 `dsw-eas-tb-e2e` 为代号的端到端验证流程（SWE-bench Verified + Terminal-Bench 2.0）正在积极运转，为发布质量保驾护航；二是 **E2E 测试在主分支持续失败**（#9143、#9159、#9160），已触发自动化修复（autofix）流程，社区对 CI 稳定性及测试覆盖有效性的关注度显著上升。


## 2. 版本发布

**v0.21.12（stable 分支）** — 核心亮点：
- **Web Shell 工作区文件上传**：支持通过拖拽或 `@` 文件面板上传文件至 Web Shell composer，并带有进度追踪（[#8874](https://github.com/QwenLM/qwen-code/pull/8874)）。
- **Autofix 评审扩散制动（diff growth brake）**：限制 autofix 评审过程中的扩散增长，避免无限膨胀。

**v0.21.12-preview.4 / preview.3（预览版）**：
- `fix(web-shell)`：保留独立会话目标（standalone session target）。
- `feat(web-shell)`：支持工作区文件上传（与 v0.21.12 同步）。

> 建议：生产环境用户可关注 v0.21.12 正式版的 Web Shell 文件上传能力；预览版主要面向尝鲜用户验证修复效果。


## 3. 社区热点 Issues（Top 10）

**🔥 高热度 / 高优先级**

1. **[#8678] [CLOSED] 大会话恢复超时时保留当前会话**（P1, 9 评论）
  请求级 restore 超时、迟到结果安全、附件身份隔离等多项改进已部分落地。该 issue 的关闭标志着长会话恢复体验的一个重要里程碑。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8678)

2. **[#8051] [OPEN] 多工作区 daemon 资源使用上界追踪**（P2, 9 评论）
  当前 daemon 仅限制工作区和会话数量，但未限制请求体、WebSocket 组装、其他缓冲区占用的字节数。内存控制呼声高，社区希望获得更细粒度的资源配置能力。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8051)

3. **[#8582] [CLOSED] 只读 Shell 分类器可被命令替换绕过**（P1/安全, 5 评论）
  通过行延续或 `${var@P}` 可绕过只读分类器执行任意代码——典型的静默逃逸问题，已合入安全修复。建议关注合入版本号。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8582)

4. **[#9143] [OPEN] 主分支 CI 失败（E2E Tests）**（P3, 7 评论）
  主分支 E2E 测试在报告任何测试结果前即失败，机器人按 commit 跟踪。该问题与 #9159、#9160 共同指向同一组 E2E 稳定性问题。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/9143)

5. **[#9160] [CLOSED] E2E 失败：live-journal-recovery 测试**（P1, 4 评论）
  属于已定位的 E2E 测试失败，autofix 已批准修复中。核心是 `qwen-serve-live-journal-recovery` 的流兼容性测试不通过。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/9160)

**🔍 功能与架构**

6. **[#4063] [OPEN] core + cli 架构审查——14 项结构性问题清单**（8 评论, 👍1）
  最核心的问题是 `ContentGenerator` 接口直接使用 `@google/genai` 类型，导致 **136 个文件**直接依赖该包，架构耦合严重。这是一份高质量的结构性整改 roadmap。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/4063)

7. **[#9146] [OPEN] 使 `utils/` 成为叶子层**（P2, 4 评论）
  当前 `packages/core` 和 `packages/cli` 中 **51 个文件对 `utils/` 有 107 处向上引用**，导致目录依赖图成环。清晰的架构治理诉求。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/9146)

8. **[#9026] [OPEN] `NO_TOOL_RESULT_PROGRESS` 硬失败**（P2, 4 评论）
  模型在工具结果后"安静"地结束回合（合法 `finish_reason`、无可见文本），headless 模式却报错中断。该问题正由 [#9196](https://github.com/QwenLM/qwen-code/pull/9196) 修复中。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/9026)

9. **[#8871] [OPEN] ACP 子进程 "Unknown argument: acp"**（P2, 5 评论）
  `qwen serve --http-bridge=true` 默认开启时，ACP 子进程无法解析 `--acp` 参数，导致 token 认证失败、`401 invalid access`。serve 模式的关键链路故障。
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8871)

10. **[#9002] [OPEN] Python SDK 拒绝 `permission_mode="auto"`**（P3, 6 评论）
    CLI 支持 `auto`，但 SDK 客户端校验只允许 `default/plan/auto-edit/yolo`——**CLI 与 SDK 行为不一致**的典型问题。
    [查看详情](https://github.com/QwenLM/qwen-code/issues/9002)


## 4. 重要 PR 进展（Top 10）

1. **[#9196] 接受重试耗尽后的安静工具结果后完成**（修复 #9026）
  合法的无声回合不再触发重试预算浪费，保留 4 次重试给真正异常的场景。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9196)

2. **[#9122] Web Shell 侧边栏会话管理体验改进**
  悬停显示会话详情、文件夹预览上限 5 行、超出自动滚动、运行中会话视觉区分。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9122)

3. **[#9096] 将散文式 gh 命令收编为平台支持的子命令**
  `/review` 技能不再让模型自行执行 shell 命令，改为 CLI 直接获取 repo 信息、head-SHA 等——安全性和确定性双提升。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9096)

4. **[#9100] `fetch-pr` 内的增量锚点校验与范围化**
  `qwen review fetch-pr` 新增 `--since <sha>`，在拉取历史前先验证锚点合法性。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9100)

5. **[#8529] 从 API 元数据解析模型模态**
  从 models.dev 获取模态快照，支持磁盘缓存与后台刷新，冷启动不等待网络请求。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8529)

6. **[#9071] 基于经验信号的门控自动技能评审**
  用 `完成重试弧` 或 `接受中途用户转向` 触发评审，替代原来纯计数的 20 次触发。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9071)

7. **[#9027] 纯文本 `/review` 评论 + 严重级别跟随 `review.attribution`**
  评论语气从模板腔改为审阅人真实语气，严重级别标识跟随 `attribution` 配置。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9027)

8. **[#9121] 修复主 agent 追踪（telemetry）边界场景**
  dsw-eas-tb e2e 验证链关键 PR，保障追踪数据在边界场景下的正确性。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/9121)

9. **[#8978] 空频道集合优雅降级（`--channel all`）**
  之前空频道集合直接 `exit(1)` 拖垮整个 daemon，改为 no-op 且仅恢复活跃频道。
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8978)

10. **[#9189] 验证过的越界发现物延期至后续队列**
    为 autofix 循环增加第四种处置：**Defer to follow-up**——机器可读队列承接已验证但超出当前 PR 范围的发现，防漂移。
    [查看详情](https://github.com/QwenLM/qwen-code/pull/9189)


## 5. 功能需求趋势

| 方向 | 热度 | 代表 Issue |
|------|------|-----------|
| **Web Shell / 桌面端** | 🔥🔥🔥 | #8845 频道策略与会话管理重构、#9122 侧边栏体验、#9168 Electron 宿主评估 |
| **资源使用上限与内存控制** | 🔥🔥🔥 | #8051 多工作区 daemon 资源上界、#2128 UI History 无界增长（P1，3 月提出至今仍开放） |
| **评审/审查体系工程化** | 🔥🔥 | #9096、#9100、#9189——将散文式指令收编为确定性命令、增量锚点、延期队列 |
| **架构治理与解耦** | 🔥🔥 | #4063 解除 `@google/genai` 绑架（136 文件）、#9146 `utils/` 叶子化、#8084 ACP 解耦 serve 内部 |
| **新渠道集成** | 🔥 | #9049 DingTalk Workspace 渠道、#9167 DingTalk 文件发送 |
| **CLI/SDK 行为一致性** | 🔥 | #9002 `permission_mode="auto"` SDK/CLI 不一致 |
| **音频/多模态支持** | 🔥 | #8332 附件音频桥、#8529 模型模态解析 |


## 6. 开发者关注点

1. **CI 稳定性是当前最大痛点**（#9143/#9159/#9160）：
   主分支 E2E 连续失败，测试在报告结果前就崩溃，虽然 autofix 已介入，但暴露的是 **"失败先于测试结果"的可观测性缺口**。

2. **长会话资源管理持续焦虑**（#2128 3 月提出至今仍在、#8051）：
   UI History 无界增长 + daemon 仅数量限制、无字节限制——内存问题直接关联生产环境的稳定性。资源上限 + 有界历史的呼声很高。

3. **CLI 与 SDK 行为不一致**（#9002、#8871）：
   同一配置项在 CLI 与 SDK 表现不同——开发者期望"配置一处、处处生效"，这类问题在评审中容易被放大。

4. **安全敏感度极高**（#8582 只读分类器绕过、【#8944】npm 依赖 2 个高危漏洞）：
   尽管 #8582 已修复关闭，但社区倾向于持续审查安全边界，对命令分类器和依赖漏洞保持高度敏感。

5. **架构债开始反噬**（#4063、#9146）：
   第三方类型绑架核心接口（136 文件）、工具函数层反向依赖（107 处向上引用）——重构诉求集中在"接口解耦"和"依赖方向正确性"，这是长期可维护性的信号。

---

*本日报由 AI 自动生成，数据截至 2026-08-15。仅供技术参考，不构成正式发布说明。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**2026-08-15** | 数据源: github.com/Hmbown/CodeWhale (原 DeepSeek-TUI)


## 1. 今日速览

v0.9.8 版本进入发布收尾阶段，但 `main` 分支出现多处 CI 红牌，包括 CLI provider 计数断言失效、9 个 reasoning-effort 测试沿用旧词汇表，以及 macOS/Windows 平台上的并发测试失败，目前社区正密集提交修复。功能层面，Auto-Review 迭代为“确定性底层 + 模型守护者”双层模式、DwarfStar (DS4) 本地模型成为一等公民、Markdown 引用块渲染回归，均为本次版本的重要增量。


## 2. 版本发布

**v0.9.8** 已于昨日发布（发布日期：2026-08-13/14）。核心要点：

- **产品更名**：公开产品正式定名 **CodeWhale**（由 Shannon Labs 出品），`codewhale` 命令、npm 包及发布资产统一使用小写技术标识；旧 npm 包 `deepseek-tui` 已弃用，不再发布新版本。
- **其余更新内容**：随 v0.9.8 发布说明未完整公示，但从 Issue/PR 追踪可见，本次版本包含本地 DS4 模型一等支持、Auto-Review 模型守护者模式、agent 工具模式降级处理等大量变更。

> ⚠️ 注意：v0.9.8 发布后 `main` 分支仍有多个测试红牌（见下文），建议等待 v0.9.8.x 修补版。


## 3. 社区热点 Issues（10 个）

**#5324 — agent 工具 32 字段 schema 过复杂，模型频繁报错** `[OPEN]`
- 作者: Hmbown | 评论: 8 | 👍: 0
- 模型面 `agent` 工具携带 **32 属性 JSON schema、零 required 字段**，同时服务 8 个 action（start/status/peek/message/followup/interrupt/wait/cancel），运行时还需兼容别名。社区已提交 PR #5369 先行降级 Moonshot schema。这是工具链稳定性层面的核心痛点。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5324

**#5374 — Agent 输出文本乱码（macOS 全区域不可读）** `[OPEN]`
- 作者: all-lopezg | 创建: 2026-08-14 | 评论: 4
- 用户反馈在 macOS 上 agent 写作时所有文本乱码（附图），"all over the place i cant read what the..."，属于渲染层兼容性问题，直接影响日常使用。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5374

**#5383 — main 分支红牌：CLI provider-count 断言仍持旧版本号** `[OPEN]`
- 作者: Lstarsky0 | 创建: 2026-08-14 | 评论: 1
- `main` 在 v0.9.8 头部变红：provider 计数断言仍为旧值（`left: 45, right: 43`）。PR #5384 已提交修复，显示 v0.9.8 实际将 provider 数量提升至 45。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5383

**#5377 — macOS/Windows 红牌：9 个 reasoning-effort 测试沿用旧词汇表** `[OPEN]`
- 作者: Lstarsky0 | 创建: 2026-08-14 | 评论: 1
- 非偶发：可稳定复现，且精确定位到单一 commit `6f6c35183`（thinking-ladder 词汇表更新）。PR #5378 已提交修复。交叉平台 CI 质量问题的典型案例。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5377

**#5370 — P0: Web UI "完全损坏"，需要对照 harness 参考重建** `[OPEN]`
- 作者: Hmbown | 创建: 2026-08-14 | 评论: 1
- 作者报告公开 Web UI（codewhale.net 的 Next.js 应用）在**外观和功能**层面完全损坏，需先厘清 Codewhale 公开 Web 应用与托管 CWC 应用（独立产品）的边界，再对照 harness 完整重建。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5370

**#5373 — 输出 token 上限被钳制到目录限额以下，强制截断导致回合死亡** `[CLOSED]`
- 作者: Hmbown | 创建: 2026-08-14 | 评论: 1
- Codewhale 请求 65,536 输出 token，但 models.dev 目录显示 `limit.output=384,000`（上下文 1,000,000）。竞品对同一端点请求 384,000。Terminal-Bench 任务因截断崩溃。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5373

**#5372 — 已关闭会话的写声明仍阻塞新 sub-agents** `[CLOSED]`
- 作者: Hmbown | 创建: 2026-08-14 | 评论: 1
- 真实工作区报告：会话关闭后，旧 agent 仍持有 `experiments/`、`tests/`、`artifacts/` 的写声明，新会话子代理被拒绝写入。死属主计数为活跃，导致虚假的写作用域争用。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5372

**#5355 — v0.9.8 已知问题：并行加载与配置夹具偶发失败** `[OPEN]`
- 作者: Hmbown | 创建: 2026-08-13 | 评论: 2
- 从 v0.9.7 关闸延续的已知问题调查篮子：`exec_persistent_service::failed_exec_*` 并行加载偶发失败、`exact_turn_snapshot_restores_custom_endpoint...` 在并行加载下失败。发布门禁质量的关键观察项。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5355

**#5350 — 简化第三方模型配置，增加预制模板** `[OPEN]`
- 作者: shadapang | 创建: 2026-08-13 | 评论: 2
- 中文提交：配置 OpenCode Zen / OpenCode Go / Agnes / 美团 Sensenova 等第三方兼容服务商时需手动填写 Base URL、模型名、密钥环境变量，且无内置文档；保存后模型列表常卡在 `not checked` / `cache failed`。建议预制模板 + 官方文档 + "测试连接"按钮。反映第三方模型接入门槛过高。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5350

**#5322 — 回归：输出区域不填满宽终端（v0.8.65 正常）** `[OPEN]`
- 作者: M-Maciej | 创建: 2026-08-11 | 评论: 3
- v0.8 中 transcript/output 区域随终端宽度扩展，v0.9 中限制为最大宽度。宽屏显示器上文本拥挤、大量空白。缩小正常、放大不跟进。TUI 布局回归的典型。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5322

**#5293 — TUI 权限请求默认高亮项变更为"拒绝"，用户易误操作** `[CLOSED]`
- 作者: JayBeest | 创建: 2026-08-08 | 评论: 5 | 👍: 1
- v0.9.4 起 TUI 权限请求对话框的默认高亮选项发生变化，打破既有交互模式——用户想快速确认时可能意外拒绝。"deny-by-default" 需配置化并清晰说明。UX 安全设计的重要讨论。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5293


## 4. 重要 PR 进展（10 个）

**#5384 — test(cli): 重新固定 provider-count 断言至 v0.9.8 注册表**
- 作者: Lstarsky0 | 状态: OPEN | 关闭 #5383
- 两个整数：注册表从 43 → 45，`ProviderKind::ALL` 从 38 → 40；变更来自 Google Gemini 成为独立后端。CI 红牌的定点修复。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5384

**#5382 — fix(state): 序列化 session-index 写入，防止静默数据丢失**
- 作者: EvanProgramming | 状态: CLOSED | 关闭 #5380
- `append_thread_name` 写入 `session_index.jsonl` 后执行 compact-rename，全程在 `Arc<Mutex<Connection>>` 之外。StateStore 可 Clone，多个实例并发访问时索引文件可损坏或丢失数据。引入文件锁/条件化补偿。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5382

**#5381 — fix(hooks): webhook HTTP 客户端构建失败不再 panic**
- 作者: EvanProgramming | 状态: CLOSED | 关闭 #5379
- `WebhookHookSink::new` 以 `.expect("build fallback HTTP client")` 结尾，reqwest 构建失败（如 TLS 后端配置错误）将导致宿主硬崩溃。改为错误传播 + 日志降级。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5381

**#5378 — test(tui): 重新固定 thinking-ladder 断言**
- 作者: Lstarsky0 | 状态: CLOSED | 关闭 #5377
- 九个测试，无生产变更。每个均断言 `6f6c35183` 已替换的 off/high/max 快捷键，导致 macOS/Windows main 红牌。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5378

**#5376 — fix(tui): 内部运行时事件不进入 session peek**
- 作者: Lstarsky0 | 状态: CLOSED | 关闭 #5375
- 重放发现真实构建的 session 在 projection 路径后出现 envelope 越界（`raw_envelope_survives=false`）。通过 peek kind 检测过滤内部事件。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5376

**#5365 — feat(provider): DS4 本地模型一等支持（v0.9.8）**
- 作者: Hmbown | 状态: CLOSED
- `/setup provider ds4`、`/provider setup ds4`、provider-picker `D` 快捷键打开预填 keyless loopback 预设；命名本地 DS4 路由复用 OpenAI 兼容传输。本地模型成为一等公民。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5365

**#5353 — feat(tui): Auto-Review 模型守护者层级（v0.9.8）**
- 作者: Hmbown | 状态: CLOSED
- Auto-Review 变为真正双层模式：确定性底层不可绕过，fallback 升级为一次性**模型守护者**，不再静默阻塞。对齐 Codex `auto_review` reviewer 语义、Kimi 模式词表、Codewhale fail-closed 默认。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5353

**#5339 — fix(engine): 过滤子属主 shell 补全事件**
- 作者: cyq1017 | 状态: CLOSED | 关闭 #5325
- 将子属主后台 shell 补全事件从父模型流中滤除；保留父级无主补全及任务/状态可见性；增加父子属主作业回归测试。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5339

**#5369 — fix(tools): Moonshot schema 降级而非拒绝条件字段**
- 作者: Lstarsky0 | 状态: CLOSED
- #5324 的前置依赖作业。Moonshot 模型不支持 schema 条件逻辑，降级为静态展开。PR 描述明确说明已与 #5324 评论区确认，先单独合并 schema 切片。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5369

**#5364 — feat(tui): Markdown 引用块渲染增加引用导轨**
- 作者: SparkofSpike | 状态: CLOSED
- TUI transcript 中 `>` 引用行渲染为带引用导轨（quote rail）的块样式，替代字面 `>` 纯文本。支持嵌套、行内格式、自动换行、正确的选择复制行为。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5364


## 5. 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|---|---|---|
| **TUI 渲染与交互质量** | #5374 文本乱码、#5322 输出区不填充宽终端、#5364 引用导轨、#5293 权限默认项 | 高（4+） |
| **CI 稳定性与测试质量** | #5383/#5377 红牌、#5355 并行加载 flake、#5378/#5384 断言修复 | 高（5+） |
| **第三方模型接入易用性** | #5350 预制模板、#1482 nVidia NIM 404、#5365 本地 DS4 一等支持 | 中 |
| **工具/Schema 稳定性** | #5324 32 字段 schema 简化、#5369 Moonshot 降级、#5373 输出上限 | 中 |
| **插件系统与市场** | #5311 Kimi 级插件系统 + 联盟市场 | 中 |
| **Web UI 重建** | #5370 P0 Web UI 完全损坏 | 高（P0） |
| **编辑器/代理注册** | #3192 agentclientprotocol/registry（Zed 安装） | 低 |

**关键判断**：TUI 渲染与交互质量是当前社区反馈最集中的方向，特别是跨平台（macOS）下的文本渲染问题；CI 稳定性是维护者当前最优先解决的事项。


## 6. 开发者关注点

1. **发布质量门禁**：v0.9.8 发布后 main 出现多个红牌（provider 计数、thinking-ladder 词汇表、并行加载 flake），且都能精确定位到特定 commit 而非偶发——暴露了发布前 CI 矩阵覆盖不足，尤其是 macOS/Windows 平台。社区通过快速提交 PR 修复（#5384、#5378、#5368）来止血。

2. **数据安全风险**：session-index JSONL 写入未同步导致的静默数据丢失（#5380）、webhook HTTP 客户端构建失败直接 panic（#5379），社区成员 EvanProgramming 连续提交修复，指出并发 Clone 场景下的状态一致性隐患。

3. **模型行为一致性**：输出 token 上限被钳制在目录限额的 1/6（#5373）、32 字段 schema 导致模型频繁报错（#5324）、thinking-ladder 词汇表变更导致 9 个测试失效（#5377）——开发者对"模型面契约"的稳定性高度敏感。

4. **并发/资源管理**：32-worker 风暴取消后 RSS 不回落（#4326）、已关闭会话的写声明仍阻塞新 sub-agents（#5372）——资源生命周期管理是高频调研方向。

5. **命名/品牌过渡**：DeepSeek-TUI → CodeWhale 更名带来一系列连锁问题：旧 npm 包弃用、VS Code 市场出现非官方同名扩展（#2327）、配置路径残留 `.deepseek` 等。社区对品牌一致性和迁移路径有明确诉求。

---

> **编辑说明**：本日报数据来自 github.com/Hmbown/CodeWhale（原 DeepSeek-TUI）。v0.9.8 发布后，项目已全面更名为 CodeWhale。链接中的 `Hmbown/CodeWhale` 即原 DeepSeek-TUI 仓库。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*