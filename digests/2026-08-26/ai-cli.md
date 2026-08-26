# AI CLI 工具社区动态日报 2026-08-26

> 生成时间: 2026-08-26 00:32 UTC | 覆盖工具: 9 个

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

**报告日期：2026-08-26**


## 1. 生态全景

AI CLI 工具赛道已进入 **“规模迭代 + 深度分化”** 阶段。一方面，头部工具（Claude Code、Codex）保持极高发布频率，单日多次迭代已属常态；另一方面，社区反馈的重心从“功能缺失”转向 **“稳定性与信任”** ——Windows 桌面端崩溃、子代理悬挂、静默失败、数据持久化不一致等问题成为跨工具的高频痛点。安全合规（CVP 误拦、SSRF、凭据泄露）与 Agent 可靠性（误报成功、上下文丢失）正在取代“能做什么”成为用户最关切的核心议题。


## 2. 各工具活跃度对比

| 工具 | 今日 Issues 更新 | 今日活跃 PR | Release 情况 | 核心焦点 |
|------|:---:|:---:|------|------|
| **Claude Code** | 10+（热门 issue 155 评论） | 1+ | v2.1.245 / v2.1.246 双版本 | 安全合规、Windows 桌面稳定性 |
| **OpenAI Codex** | 50 条更新 | 10 个重点 PR | 3 个 alpha（rust-v0.150.0-a.9~11） | 企业级 MCP OAuth、Windows 稳定性 |
| **Gemini CLI** | 10+ | 10 个重点 PR | v0.58.0-preview / v0.57.0 | Agent 可靠性、安全加固 |
| **Copilot CLI** | 8 个重点 issue（含 3 个新提交） | 1 | v1.0.81-10（插件仪表盘开放） | MCP 连接一致性、模型切换 |
| **Kimi Code CLI** | 2 条活跃 | 0 | 无 | I/O 静默失败、上下文压缩 Bug |
| **OpenCode** | 10+ | 10 个重点 PR | v1.18.23（Cloudflare Gateway 修复） | 免费模型故障、TUI 质量 |
| **Pi (pi-mono)** | 10 条精选 | 10 个重点 PR | 无 | 流式渲染稳定、Windows 支持 |
| **Qwen Code** | 10 条精选 | 10 个重点 PR | v0.22.0-nightly | 多智能体协作、上下文压缩 |
| **DeepSeek TUI** | 10 条精选 | 10 个重点 PR | v0.9.12 集成分支待发布 | Provider 中立化、监督运行控制面 |

**活跃度梯队：**
- **第一梯队（高活跃）**：Claude Code、OpenAI Codex、Gemini CLI、OpenCode、Pi、Qwen Code
- **第二梯队（中活跃）**：Copilot CLI、DeepSeek TUI
- **第三梯队（低活跃）**：Kimi Code CLI


## 3. 共同关注的功能方向

| 功能方向 | 涉及工具 | 具体诉求 |
|---------|---------|---------|
| **Windows 桌面端稳定性** | Claude Code（GPU 崩溃、置顶）、Codex（终端不可用、MCP 解析失败）、Gemini CLI（路径限制）、Pi（PowerShell 不一致）、Qwen Code（符号链接保护弱化） | 各工具 Windows 专属问题集中爆发，跨工具共性极强 |
| **上下文管理与压缩** | Claude Code（规则触发维度扩展）、Qwen Code（压缩不可控、skill 永久驻留）、Pi（reserveTokens 固定）、Kimi Code（压缩后任务重开） | 压缩策略透明度与用户控制权 |
| **会话生命周期与防打断** | Claude Code（#50246 队列模式 199👍）、Codex（线程消失）、Gemini CLI（子代理悬挂）、OpenCode（会话永久卡死） | 消息队列机制、后台任务可恢复性 |
| **MCP 生态兼容性** | Codex（OAuth 企业认证）、Copilot CLI（连接一致性、OAuth 失败）、Claude Code（draft-07 拒绝）、Gemini CLI（SSRF 防护） | 协议兼容宽度、认证安全、数据脱敏 |
| **工具调用可靠性** | Kimi Code（Edit/Write 静默失败）、OpenCode（Qwen 工具调用失败）、Gemini CLI（MAX_TURNS 误报成功）、Qwen Code（/effort max 会话中断） | 执行结果与实际状态一致 |
| **成本透明化** | OpenCode（模型选择器显示成本）、DeepSeek TUI（/context 成本归因）、Qwen Code（遥测属性） | 调用级成本可视化 |
| **Agent 自主行为合理性** | Gemini CLI（不主动调用 skills）、Qwen Code（后台任务静默执行）、Claude Code（渐进式越线） | 规则边界、可观测性、可干预性 |


## 4. 差异化定位分析

| 工具 | 核心定位 | 技术路线 | 突出优势 | 明显短板 |
|------|---------|---------|---------|---------|
| **Claude Code** | 全功能通用 Agent 平台 | 原生 CLI + 桌面应用（MSIX），强合规体系（CVP） | 权限系统精细（Auto 分类器）、生态成熟、社区反馈驱动迭代快 | 合规策略与实际执行脱节，Windows 桌面端质量拖后腿 |
| **OpenAI Codex** | 深度绑定 Codex 模型体系 | Rust 重写（发布频率极高），alpha 快速迭代 | 企业级 MCP OAuth 身份认证领先、安全加固响应迅速 | 高频 alpha 发布带来稳定性风险，Windows 为最大短板 |
| **Gemini CLI** | 与 Google 基础设施深度集成 | Node.js + IDE 扩展体系，MCP 优先 | 安全加固动作密集（SSRF、环境变量净化、凭据管理），P1 优先级管理清晰 | Agent 自主性不足（不主动调 sub-agent），子代理稳定性差 |
| **Copilot CLI** | GitHub 生态入口 | 插件仪表盘统一管理（/plugin、/mcp、/skills） | 插件系统友好，v1.0.81-10 开放仪表盘 | PR 节奏偏慢，MCP 一致性问题多发，企业策略管理不透明 |
| **Kimi Code CLI** | 轻量极简 | 最小化功能集 | 代码精简 | 迭代停滞，I/O 静默失败未修复，社区互动稀少 |
| **OpenCode** | 开源优先的灵活工具链 | 语言无关核心 + 多 Provider 支持，桌面端独立演进 | Provider 支持面广，社区贡献活跃（kitlangton 等） | 免费模型可用性风险高，2.0 更新器重大缺陷 |
| **Pi (pi-mono)** | 开发者体验驱动的 Go/TS 混合 | 构建于 earendil-works 生态，OpenAI 兼容优先 | 核心维护者响应极快（当日合并），Eager Tool 执行等架构级创新 | Windows 支持碎片化，流式渲染稳定问题多 |
| **Qwen Code** | 中文/多语言生态 + 多智能体 | 开源共建，Web Shell 差异化 | 审查流水线深度优化（上下文锚定增量轮次），Telemetry 建设积极 | 多智能体协作机制不成熟，长时运行 OOM，/effort 参数兼容性差 |
| **DeepSeek TUI** | 从专用走向通用的转型期 | Rust 重写，Provider 中立化推进中 | 监督运行控制面（control socket、lifecycle outbox）创新，社区贡献质量高 | 部分 Provider 配置不可用，Git 操作与用户工作流冲突 |


## 5. 社区热度与成熟度

**最活跃/最成熟：Claude Code、OpenCode、Pi**

- **Claude Code** 社区体量最大，Issue 讨论深度与参与度远超同行（#84352 达 155 评论），但这也意味着用户期望值极高、对缺陷容忍度低。
- **OpenCode** 与 **Pi** 的 PR 合并节奏极快，长期贡献者生态已建立，呈现典型的开源社区自驱循环。

**快速迭代/高增长：OpenAI Codex、Gemini CLI、Qwen Code、DeepSeek TUI**

- **Codex** 以 Rust alpha 高频迭代，代码现代化程度最高，但稳定性代价明显。
- **Gemini CLI** P1 优先级管理规范，安全 PR 密集（单日 3 个安全相关 PR），总活跃度位居前列。
- **Qwen Code** 从架构层面（DAP 集成、审查流水线）驱动演进，社区讨论质量高。
- **DeepSeek TUI** 正处于 v0.9.12 发布临界点，核心维护者与资深用户（M-Maciej）联合推动“可编程 TUI”方向，差异化明显。

**增长停滞/社区冷清：Kimi Code CLI**

- 仅 2 条活跃 issue，无 Release、无 PR，I/O 静默失败一周未获官方回应。社区活跃度与用户信任呈现螺旋下降风险。


## 6. 值得关注的趋势信号

### 6.1 Agent 可靠性正式成为“一等公民”议题
**信号**：Gemini CLI 的 MAX_TURNS 误报成功（P1）、Qwen Code 的多智能体协作失败、Pi 的助手文本渲染错乱、Kimi Code 的 Edit/Write 静默失败——“工具说成功但实际没成功”正在成为跨工具蔓延的系统性危机。这标志着行业从“模型能做什么”转向“模型做的是否可信”。

**参考价值**：开发者在评估 AI CLI 时，应将“结果可验证性”（是否提供 diff、文件写入校验、子代理轨迹）纳入核心选型标准，而非仅关注模型能力。

### 6.2 Windows 桌面端成为“第二战场”
**信号**：Claude Code（GPU 崩溃、MSIX 打包缺陷）、Codex（终端不可用、MCP 配置回退）、Gemini CLI（长路径限制）、Pi（PowerShell 不一致）——几乎所有主流工具在 Windows 平台的稳定性均显著弱于 macOS/Linux，且部分问题为版本回退引入。

**参考价值**：Windows 开发者用户在选择工具时需警惕，建议持续跟进桌面端修复节奏；工具厂商应将 Windows 列为 CI 必测平台，而非“尽力而为”。

### 6.3 MCP 生态进入“安全与标准化深水区”
**信号**：Codex 引入企业 IdP OAuth 认证（双 PR 构建闭环）、Gemini CLI 修复 SSRF 漏洞、Copilot CLI 面临 OAuth issuer 尾斜杠兼容问题、Claude Code 拒绝 draft-07 schema——MCP 正在从“能连就行”进入“连得安全、连得标准”阶段。

**参考价值**：企业采用 AI CLI 时，MCP 安全加固能力（凭据脱敏、SSRF 防护、OAuth 企业认证）应作为关键采购指标。开发者贡献 MCP 服务器时需遵循最新规范，避免因 schema 版本过旧被主流客户端拒之门外。

### 6.4 “可编程 TUI”成为差异化竞争新维度
**信号**：DeepSeek TUI 的控制套接字与生命周期事件 outbox（外部监督场景）、Claude Code 的消息队列需求（199👍，排队而非打断）、Qwen Code 的 Web Shell Token 面板——头部工具开始为“无人值守、CI/自动化集成、远程监督”场景设计原生接口，而非仅依赖终端模拟。

**参考价值**：对平台工程团队而言，优先选择支持控制面/事件通知/可编程接口的工具，将显著降低后续集成成本。

### 6.5 上下文管理从“技术细节”升级为“产品能力”
**信号**：Qwen Code 的压缩行为异常、Pi 的 reserveTokens 固定不缩放、Claude Code 的规则按主题触发诉求、Kimi Code 压缩后任务重开——各工具用户均在对“上下文压缩的时机、策略、结果”提出更高要求，期望从“黑盒自动压缩”走向“可配置、可预测、可审计”。

**参考价值**：对齐模型上下文窗口进行动态压缩预留、提供压缩前后对比可视化、支持用户自定义压缩策略，将是下一阶段各工具的竞争焦点。


## 结语

当前 AI CLI 市场的竞争已从“模型能力比拼”进入“工程成熟度较量”。社区对**可靠性、安全性、跨平台一致性**的关注度全面超越了新功能需求。对技术决策者而言，建议：

1. **短期**：优先关注 Windows 桌面端稳定性问题清单，评估是否符合团队开发环境；
2. **中期**：将 MCP 安全能力和上下文管理透明度纳入选型评估框架；
3. **长期**：关注“可编程 TUI”方向（控制面、事件通知），为自动化工作流集成留出空间。

各工具的每日迭代节奏说明行业仍在快速发展，保持持续跟踪是必要的战略投入。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-26）

## 1. 热门 Skills 排行（按关注度）

**① skill-creator 系列修复（#1298）** — [PR #1298](https://github.com/anthropics/skills/pull/1298)
核心问题：`run_eval.py` 始终报告 recall=0%，导致整个描述优化循环在噪声上做优化。社区至少 10+ 独立复现（对应 Issue #556）。影响面覆盖 `run_loop.py` 和 `improve_description.py` 三个脚本。状态：**OPEN**（2026-06-10 创建，持续更新）。这是当前生态最关键的堵点。

**② document-typography（#514）** — [PR #514](https://github.com/anthropics/skills/pull/514)
针对 AI 生成文档的排版痼疾：孤词换行（1-6 个词溢出到下一行）、寡妇段落（节标题孤悬页底）、编号错位。作者定位清晰：这些问题影响 Claude 生成的每一份文档，用户很少主动要求好的排版，但质量差异直接可见。状态：**OPEN**（2026-03-04 创建）。

**③ Hivemind: 零成本多智能体编排（#1628）** — [PR #1628](https://github.com/anthropics/skills/pull/1628)
核心思路：Claude Code 作为唯一的规划者/审查者/合并者，将机械性工作委托给运行免费模型的 headless opencode 工作节点。核心理念："昂贵模型的上下文是稀缺资源，而非其智能"。状态：**OPEN**（2026-08-21 创建，最新活跃 PR 之一）。

**④ docx 修订跟踪 w:id 冲突修复（#541）** — [PR #541](https://github.com/anthropics/skills/pull/541)
修复 DOCX 技能在已有书签文档中添加修订跟踪时导致的文档损坏。根因：OOXML 中 `w:id` 是书签、修订、批注、移动范围共享的 ID 空间，SKILL.md 示例使用硬编码低位 ID 导致冲突。状态：**OPEN**（2026-03-06 创建）。

**⑤ 前端设计技能改进（#210）** — [PR #210](https://github.com/anthropics/skills/pull/210)
对 frontend-design skill 的全面修订，提升清晰度、可操作性和内部一致性。目标是确保每条指令 Claude 都能在单次对话中真正执行。状态：**OPEN**（2026-01-05 创建）。

**⑥ self-audit：机械化验证 + 四维推理质量门控（#1367）** — [PR #1367](https://github.com/anthropics/skills/pull/1367)
交付前审计技能：**先机械化验证文件存在性，再按损害严重度优先级进行四维推理审计**。通用性强，适配任何项目/技术栈/模型。状态：**OPEN**（2026-06-28 创建）。

**⑦ 社区健康度修复：CONTRIBUTING.md（#509）** — [PR #509](https://github.com/anthropics/skills/pull/509)
仓库社区健康分仅 25%，该 PR 旨在通过添加 CONTRIBUTING.md 补齐最大的单点缺口。状态：**OPEN**（2026-03-03 创建）。


## 2. 社区需求趋势（从 Issues 提炼）

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **安全信任边界** | [#492](https://github.com/anthropics/skills/issues/492)（43 评论） | 社区技能在 `anthropic/` 命名空间下分发，伪造官方技能，形成信任边界滥用。最高关注度 |
| **组织级技能共享** | [#228](https://github.com/anthropics/skills/issues/228)（16 评论，8👍） | 需要组织内直接共享技能库，而非手动下载 .skill 文件→Slack/Teams→手动上传 |
| **评估工具链可靠性** | [#556](https://github.com/anthropics/skills/issues/556)（12 评论，7👍） | `run_eval.py` 对所有查询 0% 触发率，技能优化闭环失效 |
| **技能管理体验** | [#62](https://github.com/anthropics/skills/issues/62)（10 评论） | 技能文件消失、错误频发，需更稳健的技能管理 |
| **上下文窗口效率** | [#1487](https://github.com/anthropics/skills/issues/1487) | `claude-api` 技能单次调用注入 ~156k tokens，直接耗尽上下文窗口 |
| **技能插件去重** | [#189](https://github.com/anthropics/skills/issues/189)（6 评论，9👍） | `document-skills` 与 `example-skills` 插件内容重复，导致上下文重复加载 |
| **MCP/外部系统集成** | [#16](https://github.com/anthropics/skills/issues/16)、[#29](https://github.com/anthropics/skills/issues/29)、[#1175](https://github.com/anthropics/skills/issues/1175) | 作为 MCP 暴露、Bedrock 集成、SharePoint 安全处理 |

**核心信号**：社区现阶段最迫切的需求依次是 **① 安全与信任（命名空间冒用）、② 组织级共享能力、③ 工具链可靠性（评估脚本）**。


## 3. 高潜力待合并 Skills（近期可能落地）

| PR | Skill | 亮点 | 活跃度 |
|----|-------|------|--------|
| [#1615](https://github.com/anthropics/skills/pull/1615) | **scnet-hpc** | SCNet HPC 集群运维（SSH + Slurm 工作流），profile 管理、作业生成、集群发现 | 创建于 08-20，持续更新中 |
| [#1628](https://github.com/anthropics/skills/pull/1628) | **Hivemind** | 零成本多智能体编排，免费模型做机械工作 | 最新 PR（08-21），理念新颖 |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | 全栈测试模式（Testing Trophy、AAA、React Testing Library） | 评论持续，跨 4 月活跃 |
| [#568](https://github.com/anthropics/skills/pull/568) | **servicenow** | 企业级全平台覆盖（ITSM/ITOM/ITAM/SecOps/FSM/SPM/CSDM） | 更新时间跨度大（03-08 → 08-12） |
| [#1367](https://github.com/anthropics/skills/pull/1367) | **self-audit** | 交付前质量门控（机械化验证 + 四维推理审计） | v1.3.0 持续迭代 |
| [#525](https://github.com/anthropics/skills/pull/525) | **pyxel** | 复古像素风游戏开发（write → run_and_capture → inspect 闭环） | 作者维护活跃（03-05 → 07-15） |


## 4. Skills 生态洞察

当前社区最集中的诉求是 **"让 Skills 工具链本身先可靠起来"**——从 `run_eval.py` 的 0% 触发率、Windows 管道崩溃、YAML 解析静默失败，到 156k token 上下文爆炸、案例敏感的引用错误，都在指向一个事实：**Skill 的创建、验证、分发与管理环节还远未达到生产级标准**；同时，围绕命名空间信任、组织级共享、上下文效率这三件事，正成为生态走向规模化的必经关卡。（一句话：**先修好工具链，再谈生态繁荣**。）

---

# 2026-08-26 日报：Claude Code 社区动态

## 今日速览
- **双版本连发**：`v2.1.246` 和 `v2.1.245` 先后发布，后者修复了 glibc 2.44 发行版（Arch、Fedora Rawhide）的 Linux 启动崩溃，前者则为 `/permissions` 新增 Auto 模式分类器配置面板，并堵住了一个 Bash 通配符规则被选项插入绕过的漏洞。
- **安全合规争议发酵**：155 评 Issue `#84352` 揭示已获 CVP（网络验证计划）批准的 Claude.ai 组织在 Claude Code 中仍被“网络保障”误拦，合规状态与执行策略严重脱节，成为今日社区头号热点。
- **Windows 桌面应用故障集中爆发**：GPU 进程致命崩溃致死包、后台 Agent 被包服务静默杀死、插件状态显示错乱等多起 `area:desktop` 问题进入活跃期，Windows 用户体验短板明显。

---

## 版本发布

### v2.1.246
- 新增启动警告：针对选项插入绕过场景（如 `Bash(git * main)`），通配符位于子命令前时不再被盲信。
- `/permissions` 新增 **Auto 模式** 选项卡，支持查看和编辑自动模式分类器规则。

### v2.1.245
- 修复 Linux 发行版（Arch、CachyOS、Fedora Rawhide 等）因 glibc 2.44 导致的启动崩溃。

---

## 社区热点 Issues（Top 10）

1. **[CVP 批准组织仍被网络保障误拦](https://github.com/anthropics/claude-code/issues/84352)** — 155 评论，24 👍
  “已批准”状态在验证门户与执行策略间出现分歧（门户显示“审查中”），合规流程与落地策略脱节，直接毁掉用户信任。

2. **[消息队列模式：不打断当前任务的排队交互](https://github.com/anthropics/claude-code/issues/50246)** — 68 评论，199 👍，已关闭
  当前无法在任务中途排入后续指令，要么打断要么遗忘。社区近 200 赞表明期望极高，是 TUI 交互设计的核心诉求。

3. **[Windows 桌面版致命 GPU 崩溃，包不可启动](https://github.com/anthropics/claude-code/issues/80444)** — 56 评论，9 👍
  应用内浏览器触发的 GPU 进程崩溃（0x060C201E）直接毁掉 MSIX 包，需要 Repair 才能恢复，影响面大且破坏性强。

4. **[TUI 滚动回归：滚轮变方向键](https://github.com/anthropics/claude-code/issues/65833)** — 41 评论，99 👍
  v2.1.150 起滚轮不再滚动会话输出，反而切输入历史。99 赞说明该回归对日常体验冲击明显，社区呼声高。

5. **[MCP 服务器声明 draft-07 outputSchema 被直接拒绝](https://github.com/anthropics/claude-code/issues/86142)** — 29 评论，12 👍，已关闭
  声明 draft-07 schema 的 MCP 服务器在分派前即被“unsupported dialect”拒绝，兼容性处理过于粗糙。

6. **[Claude Desktop Windows 11 总是置顶](https://github.com/anthropics/claude-code/issues/85891)** — 24 评论，36 👍
  主窗口始终悬浮于其他应用之上且无设置项，干扰工作流。与 macOS `#66516` 同源，说明跨平台窗口行为差异大。

7. **[Pro 套餐未使用却反复触达用量上限](https://github.com/anthropics/claude-code/issues/61012)** — 18 评论，8 👍
  空闲状态下仍被频繁限流，疑似用量核算存在误差，直接影响付费用户核心权益。

8. **[请求 `.claude/rules/` 支持按提示主题触发](https://github.com/anthropics/claude-code/issues/87804)** — 13 评论
  当前 `paths:` 只能按文件路径匹配，无法按对话主题加载规则。增强规则引擎的场景化能力成为新方向。

9. **[MSIX 缺 CodeIntegrity 目录，包被系统销毁](https://github.com/anthropics/claude-code/issues/85901)** — 11 评论，1 👍，已关闭
  已发布的 MSIX 缺少 `AppxMetadata\CodeIntegrity.cat`，vk_swiftshader.dll 被代码完整性拦截，导致整个包被破坏，属打包严重缺陷。

10. **[AppX 更新时被 `CoworkVMService` 锁文件](https://github.com/anthropics/claude-code/issues/73694)** — 6 评论，2 👍
  更新/重启失败（0x80073d02），因 `cowork-svc.exe` 占用包文件锁。桌面服务化进程与打包体系互操作存在隐患。

---

## 重要 PR 进展

1. **validate-agent.sh 修复**（[PR #89404](https://github.com/anthropics/claude-code/pull/89404)）— 作者 bcherny
  修复 `set -e` 与 `((x++))` 的交互问题：首个警告即中断校验，以及误报合法 agent。`((count++))` 在已为 0 时返回非零退出码，真相反直觉的坑。解决 `#83803`。

---

## 功能需求趋势

- **规则触发维度亟待扩展**：从 `#87804`（按主题触发 `.claude/rules/`）与 `#89669`（hook 限定在技能活跃期内）看，社区对规则和钩子的 **场景化、上下文感知** 需求正在抬头，单一的文件路径匹配已不满足诉求。
- **会话管理与防打断**：`#50246` 高达 199 赞，消息队列（排队而非打断）是 TUI 交互的核心缺口；`#89666`（Ctrl+B 后台命令后会话不可恢复）进一步表明会话生命周期管理仍是薄弱环节。
- **Windows 桌面体验整体拉垮**：崩溃（`#80444`、`#85901`）、置顶（`#85891`）、文件锁（`#73694`）、被静默屠进程（`#82277`）等一系列 Windows 专属问题，表明桌面端在打包、GPU、服务化等环节欠债较多，且用户对稳定性的容忍已在耗竭。

---

## 开发者关注点

- **网络/代理层问题抬头**：`#89663` 在 Windows 上用 Node v26.3.0 的 `ECONNRESET` 流式请求大面积失败，而浏览器 UI 同网络正常——提示 CLI 的请求栈（代理、TLS 或 keep-alive）可能在新版本中出现回归。
- **MCP 兼容性宽度不足**：draft-07 `outputSchema` 被直接弃用（`#86142`），Slack 连接器在“已连接”状态下对 routines/MCP 授权不可见（`#89665`）——接口生态的“报喜不报忧”状态令集成开发者头疼。
- **长期性规则被执行漂移**：`#89464` 暴露一个更微妙的模型行为——CLAUDE.md 禁令（“永不自己构建，应委派”）无法拦截 **渐进式越线**，单步不够大不触发，累计破坏却很大。本质上是“规则引擎 vs 增量生成”的边界问题。
- **Ctrl+B 后台会话不可恢复**（`#89666`）：后台化 Bash 命令后，会话状态丢失、无法就地恢复，直接击穿“后台任务”这个心智模型。
- **插件 UI 状态错乱**（`#89667`）：桌面应用显示插件 Disabled，但 `enabledPlugins` 为 true 且命令实际可运行——UI 状态与真实状态脱节，排查成本极高。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-26** | 数据来源: github.com/openai/codex


## 今日速览

今日 Codex 社区的核心动态集中在 **Windows 桌面端稳定性问题**上，多个高活跃 Issue 指向 MCP 配置解析失败、会话意外消失与终端无法启动等阻断性问题，微软 Store 版本的应用启动失败尤为突出。同时，开发侧 PR 高度活跃，围绕 **MCP OAuth 企业身份认证**、**安全加固**（如 Git 凭据脱敏）与 **exec-server 测试基础设施** 三大方向密集合并了多项改进，显示官方正在同步推进企业级功能落地与工程质量建设。


## 版本发布

过去 24 小时内发布了 3 个 Rust 版本的迭代，均为 alpha 预发布版本，未附带显著的面向用户的功能说明。

- [rust-v0.150.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.9)
- [rust-v0.150.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.10)
- [rust-v0.150.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.11)


## 社区热点 Issues

过去 24 小时内共有 50 条 Issue 更新，以下为最值得关注的前 10 条：

**#1 长期悬而未决：Linux 桌面版支持呼声持续走高**
[Issue #11023](https://github.com/openai/codex/issues/11023) — 自 2 月创建以来累计获得 953 👍 和 209 条评论，已成为社区最强烈的功能诉求之一。用户因 macOS 版本存在功耗问题（#10432），希望在 Linux 桌面获得原生 Codex 应用体验。虽已被关闭，但讨论热度不减。

**#2 Windows 端 MCP 配置回归：稳定版与 Beta 行为不一致**
[Issue #40715](https://github.com/openai/codex/issues/40715) — 稳定版（26.820.60940）在 Windows 上解析 `mcp_servers.codex_app` 时报 “invalid transport” 错误，而 Beta 版（26.727.40816）正常，表明存在版本回退问题，影响 Pro 用户。

**#3 自动化任务“自我禁用”：定时任务无故暂停**
[Issue #38350](https://github.com/openai/codex/issues/38350) — 用户在未授权的情况下，多个周期性定时任务在成功执行后自动从 enabled 变为 paused，影响 ChatGPT Web 端工作流稳定性，目前无任何规避措施。

**#4 陈旧子代理堆积：UI 无法可靠关闭**
[Issue #25179](https://github.com/openai/codex/issues/25179) — 长时间运行的会话中，子代理在缓存/UI 中持续累积且无法可靠关闭，导致界面混乱，影响长会话体验。

**#5 Windows 会话状态错乱：线程卡在“思考中”**
[Issue #34026](https://github.com/openai/codex/issues/34026) — 已完成的线程仍显示“thinking”状态，新消息只能在本地排队而无法开始新回合，跨版本（26.715.2305.0 与 26.715.4045.0）均可复现。

**#6 Windows 工作区终端完全不可用**
[Issue #39841](https://github.com/openai/codex/issues/39841) — 工作区终端初始化报 "setup refresh had errors"，导致任何命令都无法执行，严重阻断依赖终端的工作流。

**#7 Windows 桌面端线程消失：侧边栏与搜索均无法找到**
[Issue #30385](https://github.com/openai/codex/issues/30385) — 本地项目线程在磁盘和 `session_index.jsonl` 中存在，且可通过线程 ID 直接加载，但不出现在侧边栏或搜索结果中，索引与 UI 不同步。

**#8 自定义模型适配：非 OpenAI Provider 子代理编排异常**
[Issue #17598](https://github.com/openai/codex/issues/17598) — 原生子代理编排在使用非 OpenAI 自定义模型提供商时无法正常工作，影响依赖第三方模型的开发者。

**#9 `exec` 模式不触发 `PreToolUse` 钩子（附修复补丁）**
[Issue #23411](https://github.com/openai/codex/issues/23411) — Code Mode 的 `exec` 工具未发出 `PreToolUse` 钩子事件，与 #18391 中 `apply_patch` 修复的 bug 同类，用户已附带修复补丁等待合入。

**#10 长期等待：支持 GPT-5.6 可选 1M 上下文**
[Issue #31868](https://github.com/openai/codex/issues/31868) — 作为 #19464 的后续，社区希望 Codex 全客户端（App/CLI/IDE）支持 GPT-5.6 的 1M 上下文窗口，已获得 22 👍，需求明确。


## 重要 PR 进展

过去 24 小时共 50 个 PR 更新，以下为值得关注的 10 项：

**#1 企业级 MCP OAuth：双 PR 构建身份认证闭环**
[PR #40739](https://github.com/openai/codex/pull/40739) 与 [PR #40722](https://github.com/openai/codex/pull/40722) 为 MCP OAuth 引入企业 IdP 身份解析与 ID-JAG 交换能力，支持从企业身份提供商获取令牌并换取资源绑定的 MCP bearer token，是面向企业客户的重大功能补强。

**#2 安全加固：Git 远程元数据凭据脱敏**
[PR #40713](https://github.com/openai/codex/pull/40713) — Git 远程 URL 中可能内嵌用户名、密码或 token，该 PR 在远程信息进入 turn 元数据与持久化线程元数据前移除凭据，防止敏感信息泄露。属于重要的安全基础设施改进。

**#3 MCP 工具输出保留为结构化内容**
[PR #40737](https://github.com/openai/codex/pull/40737) — 将非结构化的 MCP 结果转换为类型化的函数调用输出项，保留媒体、加密内容等，不再序列化为纯文本，提升 MCP 生态的兼容性与可扩展性。

**#4 MCP Server 权限模型修正：遵循附件所有者权限**
[PR #40728](https://github.com/openai/codex/pull/40728) — 修正 MCP 服务器附加到执行器环境时的权限继承问题，要求保留其所有者的权限配置文件，而非继承线程级沙箱权限。

**#5 保留 composer 中超链接的跨行完整性**
[PR #40720](https://github.com/openai/codex/pull/40720) — 修复文本换行导致 URL 超链接（OSC 8）断裂的问题，包括部分 URL 滚出屏幕的情况，改善 TUI 使用体验。

**#6 保留保留工具 Schema 中的参数边界**
[PR #40719](https://github.com/openai/codex/pull/40719) — 确保 `minimum`、`maximum`、`maxLength` 等参数约束在 Schema 解析后不被丢失，保证模型能收到正确的声明限制。

**#7 受管 Worktree 增加线程所有权元数据**
[PR #40716](https://github.com/openai/codex/pull/40716) — 引入 `WorktreeManager` API 将受管链接 worktree 绑定到线程，并记录版本化的 `codex-thread.json` 于 Git 元数据中，支持原子无覆盖写入。

**#8 为固定的 Codex 发布版本添加 Bazel 仓库**
[PR #40718](https://github.com/openai/codex/pull/40718) — 新增 Bazel 模块扩展，可下载校验和固定的 Linux x86-64 Codex 发布包，支持从官方发布主机与 GitHub Releases 获取，为可复现构建奠定基础。

**#9 支持沙箱化 exec-server 测试环境**
[PR #40717](https://github.com/openai/codex/pull/40717) — 为 exec-server 测试夹具增加 Linux 沙箱可执行文件的接收能力，提升测试环境对沙箱场景的覆盖。

**#10 显式远程执行器连接刷新**
[PR #40710](https://github.com/openai/codex/pull/40710) — 为远程 Noise registry 后端环境新增 `refresh_connection`，在计划更换执行器时可获取全新会话，无需等待旧会话的瞬时断线恢复。


## 功能需求趋势

从今日活跃 Issue 中可提炼出以下社区最关注的功能方向：

- **Linux 桌面应用支持**（#11023，953 👍）：社区长期最强烈诉求，受 macOS 功耗问题驱动，用户急需 Linux 原生客户端。
- **更大的上下文窗口**（#31868）：对 GPT-5.6 可选 1M 上下文的支持呼声渐高，覆盖 App、CLI、IDE 全客户端。
- **原生子代理编排的自定义模型适配**（#17598）：非 OpenAI Provider 场景下的编排正确性成为刚需，与自定义模型接入深度绑定。
- **Tool Call 可见性回归**（#39819，已关闭）：部分用户希望 CLI TUI 恢复工具调用的展开/折叠显示选项，作为 `config.toml` 配置项。
- **本地 Hook 信任机制增强**（#21615）：IDE/封装工具集成商需要受支持的方式请求安装的 hooks 获得信任，推动生态集成便利性。

## 开发者关注点

综合以上 Issue 与 PR，开发者反馈中的核心痛点和高频需求集中在以下几个方面：

- **Windows 端稳定性成为最大短板**：MCP 配置解析失败（#40715）、应用启动失败（#40700、#28392）、工作区终端不可用（#39841）、线程状态错乱（#34026）等多个阻断性问题集中在 Windows 平台，部分为版本回退引入的回归，修复优先级应提升。
- **会话与线程数据可靠性受到质疑**：多起数据丢失（#38076）、线程消失（#30385、#40674）、服务端删除后复活（#40219）等问题，让用户对本地会话数据的持久化与索引一致性产生信任危机。
- **远程 SSH 与本地能力不一致**：浏览器和 `node_repl` 工具在 Remote SSH 任务中未被配置（#34263），导致远程开发体验劣于本地。
- **进程与资源泄漏**：Windows 上 `node_repl.exe` 每线程泄漏且不回收（#35485）、CLI 因 `logs_2.sqlite` 写锁在启动阶段即失败（#35555，仅 5s busy_timeout 无重试），对长期运行的开发者影响显著。
- **自动化与定时任务可靠性**：定时任务自动暂停（#38350）与创建失败（#35680）说明自动化工作流尚不稳定，而这是企业用户的核心场景，需尽快修复。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-26**


## 今日速览

今日发布了 **v0.58.0-preview.0** 与 **v0.57.0** 两个版本，核心修复聚焦于 IDE 连接稳定性与 OAuth 流程。社区讨论热度集中在 **Agent 可靠性**（子代理悬挂、MAX_TURNS 误报成功）与 **安全加固**（SSRF、环境变量注入）两大方向；同时，Auto Memory 功能的多项缺陷成为热议焦点，安全与稳定性是当前社区最关注的技术主线。


## 版本发布

### v0.58.0-preview.0
- **修复**：确保 ignore 路径处理中的符号链接评估一致性
- **重构**：核心模块代码结构优化

### v0.57.0
- **修复**：动态解析 Cloud Workstations 代理重定向 URI，完善 OAuth 流程
- **修复**：解决 IDE 连接中目录不匹配被吞掉的问题

### v0.56.0-nightly.20260825.g812f7a2bc
- **修复**：清除新消息轮次中的过期取消错误
- **修复**：在写入策略配置中声明顶层安全检查器


## 社区热点 Issues

### 1. Subagent 在 MAX_TURNS 后误报 GOAL 成功（#22323）
**优先级 P1** | 评论 13 | 👍 2
`codebase_investigator` 子代理在达到最大轮次后仍报告 `status: "success"`，掩盖了实际的中断情况。
**影响**：直接误导用户对任务完成状态的判断，是 Agent 可靠性领域的核心缺陷，社区讨论热度最高。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. 通用 Agent 悬挂导致 CLI 无响应（#21409）
**优先级 P1** | 评论 8 | 👍 8
简单操作（如创建文件夹）触发子代理后，CLI 挂起最长可达 1 小时。用户反馈需明确禁止委派子代理才能恢复。
**影响**：这是目前社区反馈最强烈的痛点之一，直接导致日常开发流程阻塞。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. Shell 命令执行后卡在 "Waiting input"（#25166）
**优先级 P1** | 评论 4 | 👍 3
简单 CLI 命令执行完成后，终端仍显示运行状态并等待输入。
**影响**：基础交互层面的严重缺陷，高频出现在日常使用场景，用户诉求强烈。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

### 4. Bug 报告缺少子代理上下文（#21763）
**优先级 P1** | 评论 2
`/bug` 命令生成的报告仅包含主会话信息，无法诊断子代理内部状态。
**影响**：显著降低 bug 排查效率，社区期望将子代理轨迹纳入报告。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21763)

### 5. Auto Memory 无限重试低信号会话（#26522）
**优先级 P2** | 评论 5
低信号会话因提取代理跳过读取而永远不会标记为已处理，导致反复重试。
**影响**：造成资源浪费和潜在死循环，反映后台服务需引入明确终止条件。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

### 6. Auto Memory 缺失确定性脱敏机制（#26525）
**优先级 P2** | 评论 4
提取提示词虽要求模型对秘密进行脱敏，但内容已先进入模型上下文才执行。
**影响**：属于隐私安全问题，社区关切度较高，涉及敏感数据处理。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26525)

### 7. Gemini 对自定义技能与子代理使用不足（#21968）
**优先级 P2** | 评论 6
模型不会主动调用已配置的 skills 和 sub-agents，需显式指令才执行。
**影响**：反映 Agent 自主决策能力与用户预期存在差距，影响扩展生态落地。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

### 8. 工具数量超 128 个触发 400 错误（#24246）
**优先级 P2** | 评论 3
工具总数超过限制后请求直接失败，缺少动态裁剪机制。
**影响**：限制了大型项目中的扩展能力，降低功能可扩展性。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

### 9. ~/.gemini/agents 下符号链接不被识别（#20079）
**优先级 P2** | 评论 4
通过符号链接指向的 Agent 文件无法被识别。
**影响**：影响配置灵活性，属于易用性改进点。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/20079)

### 10. 终端重缩放性能与闪烁问题（#21924）
**优先级 P2** | 评论 2
需要迁移至 RenderStatic 并分批更新历史项以解决闪烁。
**影响**：影响用户体验的细节问题，与核心终端交互体验直接相关。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21924)


## 重要 PR 进展

### 1. [P1/XL] 更新依赖、添加 MCP 配置并集成 ECC bundles（#28955）
大规模依赖更新与 MCP 配置集成，涉及面广，需重点回归测试。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28955)

### 2. [P2/S] 修复 BaseLlmClient 中 abortSignal 未传递至 retryWithBackoff（#29089）
修复 SessionSummaryService、聊天压缩等服务中取消信号丢失的问题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/29089)

### 3. [L] 扩展环境变更需用户同意并净化运行时环境变量（#28863）
修复扩展更新可绕过用户同意检查、注入未授权环境变量的问题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28863)

### 4. [M] 修复 IDE 扩展在 MCP 流打开时 stop() 无法解析（#29088）
解决 `IdeServer.stop()` 因长连接流未排空而永远挂起的问题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/29088)

### 5. [L] 防止并发扩展安装竞态条件（#29087）
利用现有 `proper-lockfile` 依赖避免多进程同时安装同一扩展时的文件冲突。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/29087)

### 6. [M] 修复混合行尾检测逻辑（#28983）
将 CRLF 判定从"单次匹配即判定"改为"检测混合行尾"，避免误报。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28983)

### 7. [L] 防止 MCP OAuth 元数据发现与认证中的 SSRF 攻击（#29081）
强制 HTTPS、校验源匹配，仅允许回环地址使用 HTTP，加强 OAuth 流程安全。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/29081)

### 8. [M] 移除不安全的 diff.external 覆写（#28930）
修复 Git 在 shell 沙箱中外部 diff 工具被意外禁用的回归问题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28930)

### 9. [S] 移除 A2A 服务器中误导性安全方案与硬编码凭据（#29067）
使代理元数据准确反映端点未认证状态，删除不安全的硬编码值。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/29067)

### 10. [M] 文档：为 Windows 添加 longpaths 设置说明（#28926）
解决 Windows 下因 MAX_PATH 限制导致克隆失败和数千个脏文件的问题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28926)


## 功能需求趋势

1. **Agent 可靠性与可观测性（高频）**：多个 P1 级 issue 聚焦子代理悬挂、误报、缺乏上下文等稳定性问题。核心诉求包括子代理轨迹可视化（#22598）、bug 报告包含子代理上下文（#21763）。
2. **安全加固（快速上升）**：社区对安全问题的关注显著增强，覆盖 SSRF 防护、环境变量注入、凭据管理及内存脱敏机制（#26525、#29081、#28863、#29067）。
3. **上下文与 Token 效率**：AST 感知读取（#22745）、Tactful Extraction（#19561）、工具数量上限优化（#24246）等诉求表明，社区在积极寻求降低 Token 消耗、提升上下文质量。
4. **平台体验**：Linux 与 Windows 平台适配问题持续受关注（Wayland 浏览器子代理 #21983、Windows 路径限制 #28926），强调跨平台兼容性的重要性。
5. **模型使用行为改进**：包括减少临时脚本生成（#23571）、阻止破坏性操作（#22672），以及提高工具调用准确性。


## 开发者关注点

1. **Agent 自主决策准确性（最突出）**：模型在无明确指令时不会主动调用 skills/sub-agents（#21968），并在未受控场景下产生临时脚本（#23571）。
2. **会话与流程稳定性**：子代理无条件挂起、Shell 命令卡死在等待输入等问题严重干扰日常开发流程（#21409、#25166）。
3. **本地配置灵活性**：符号链接不被支持（#20079）等限制影响了用户自定义工作流。
4. **安全隐私考量**：调用链中存在数据脱敏不及时（#26525）、扩展可注入环境变量（#28863）等隐患，开发者对数据安全提出更高要求。
5. **环境兼容性**：Windows 下长路径、Wayland 下浏览器子代理等问题提示跨平台测试覆盖仍需加强。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，这是 2026 年 8 月 26 日的 GitHub Copilot CLI 社区动态日报。

---

## GitHub Copilot CLI 社区动态日报 — 2026-08-26

### 1. 今日速览

今日最重大的更新是 **v1.0.81-10 发布**，其中插件仪表盘（Plugins Dashboard）已向所有用户开放，并统一了删除键（`x`）的交互逻辑。社区讨论热度不减，集中在 **BYOK/本地模型切换**、**MCP 服务器连接可靠性和工作区配置** 等核心痛点，同时新提交的 Issue 揭示了**旧版本 pre-release 更新逻辑缺陷** 及 **Google Workspace MCP OAuth 认证失败** 等新问题。

### 2. 版本发布

**v1.0.81-10** 已发布，主要更新内容：

- **插件仪表盘全面开放**: 所有用户可直接通过 `/plugin`、`/mcp` 或 `/skills` 命令使用。可通过设置 `PLUGINS_DASHBOARD=false` 选择退出并禁用 `copilot plugins` 命令。
- **交互统一**: 删除键 `x` 现在在 `/sandbox config`、`/settings`、`/mcp`、会话对话框及 diff 视图中均可使用。

### 3. 社区热点 Issues

以下 10 个 Issue 在过去 24 小时内讨论最为活跃或影响面较大：

1.  **[#13] CLI 输入应支持 vi/vim 模式**
    - **热度**: 74 👍 | 8 评论
    - **重要性**: 高赞需求，反映了开发者对高效键盘驱动编辑的强烈愿望，在交互式命令行工具中呼声极高。
    - **链接**: [Issue #13](https://github.com/github/copilot-cli/issues/13)

2.  **[#3709] 允许 /model 在一个会话中切换多个模型（包括 BYOK/本地提供商）**
    - **热度**: 28 👍 | 6 评论
    - **重要性**: 解决了 BYOK 模式绑定单一模型的限制。用户希望能在会话中自由切换 GitHub 托管模型和本地/自建模型，对采用混合模型策略的开发团队至关重要。
    - **链接**: [Issue #3709](https://github.com/github/copilot-cli/issues/3709)

3.  **[#4605] `latest-prerelease` 查找逻辑缺陷，导致用户困于 1.0.81-9**
    - **热度**: 0 👍 | 0 评论 (新提交)
    - **重要性**: 新发现的版本更新逻辑 Bug。由于 GitHub Release 的 `created_at` 时间戳可能相同，导致排序错误，使用户无法更新到最新的 pre-release 版本（如 1.0.81-10）。这会阻碍用户获取关键修复。
    - **链接**: [Issue #4605](https://github.com/github/copilot-cli/issues/4605)

4.  **[#4542] 工作区 `.mcp.json` 能被检测但无法在会话中连接**
    - **热度**: 1 👍 | 2 评论
    - **重要性**: MCP 配置加载的严重一致性 Bug。`mcp list` 显示配置正常，但实际会话中并未加载，导致工具调用失败，干扰正常工作流。
    - **链接**: [Issue #4542](https://github.com/github/copilot-cli/issues/4542)

5.  **[#4604] 用户配置的 GitHub MCP 服务器丢失令牌，OAuth 无法补救**
    - **热度**: 0 👍 | 0 评论 (新提交)
    - **重要性**: 新版本引入的回归 Bug。升级到 1.0.81-10 后，用户自配置的 `api.githubcopilot.com/mcp/` 服务器无法获得自动注入的 Copilot 令牌，且提供的 OAuth 补救方案因服务器不支持动态注册而失效，导致该服务器完全不可用。
    - **链接**: [Issue #4604](https://github.com/github/copilot-cli/issues/4604)

6.  **[#4602] `store_memory` 失败和所有 MCP 服务器被剥离，根因是 `serverFetchFailed`**
    - **热度**: 0 👍 | 0 评论 (新提交)
    - **重要性**: 一个潜在的高影响 Bug。该 Issue 指出了一个统一根因（`managedSettings` 在面对 `serverFetchFailed` 时过于严格）可能导致会话功能（如 `store_memory`）全面失效，并牵连所有 MCP 服务器被移除。
    - **链接**: [Issue #4602](https://github.com/github/copilot-cli/issues/4602)

7.  **[#4606] Google Workspace MCP OAuth 因 issuer 尾斜杠不匹配而失败**
    - **热度**: 0 👍 | 0 评论 (新提交)
    - **重要性**: 新发现的兼容性问题。Google 的授权服务器元数据中 URL 带有尾斜杠（`https://accounts.google.com/`），而 CLI 在 OAuth 流程中未正确处理，导致认证在开始前即失败，阻碍了用户连接官方 Google Workspace 服务。
    - **链接**: [Issue #4606](https://github.com/github/copilot-cli/issues/4606)

8.  **[#4035] 语音安装程序因 Azure Artifacts 私有源 401 失败**
    - **热度**: 0 👍 | 4 评论
    - **重要性**: 安装程序 Bug。启用语音模式时，安装程序错误地尝试从私有 Azure Artifacts 源下载公开的 NuGet 包，导致 401 错误，阻碍了新用户使用语音功能。
    - **链接**: [Issue #4035](https://github.com/github/copilot-cli/issues/4035)

9.  **[#3380] 增加 `--disable-repo-mcps` 标志以跳过仓库 MCP 配置**
    - **热度**: 0 👍 | 2 评论
    - **重要性**: 功能需求。目前用户无法方便地忽略仓库自带的 `.mcp.json` 配置，只能逐个禁用，此功能将为处理不可信或复杂的仓库 MCP 配置提供必要的安全和控制手段。
    - **链接**: [Issue #3380](https://github.com/github/copilot-cli/issues/3380)

10. **[#4272] 企业版用户无法选择新模型（灰色显示）**
    - **热度**: 3 👍 | 1 评论
    - **重要性**: 企业用户痛点。新模型默认显示为被组织策略禁用，但提供的链接中并没有相应的启用选项，导致企业用户无法使用新模型，需要管理员介入解决。
    - **链接**: [Issue #4272](https://github.com/github/copilot-cli/issues/4272)

### 4. 重要 PR 进展

过去 24 小时内 PR 数量较少，但有一个重要版本准备 PR：

1.  **[#4607] 准备公开预发布版 v1.0.81-11**
    - **状态**: 已关闭 (CLOSED)
    - **重要性**: 此 PR 用于推进公开仓库的提交时间戳，以准备发布 v1.0.81-11。这表明维护团队正在积极准备下一个版本的发布。
    - **链接**: [PR #4607](https://github.com/github/copilot-cli/pull/4607)

*(注：由于过去24小时内活跃的 PR 条目仅有1条，故此处无法列出10个。)*

### 5. 功能需求趋势

综合近期的 Issue，社区最关注的功能方向如下：

- **MCP (模型上下文协议) 体验优化**：大量 Issue 围绕 MCP 展开，包括更灵活的配置控制（如 `--disable-repo-mcps` 标志）、提高连接稳定性和诊断能力、以及修复 OAuth 等认证环节的兼容性问题。这是当前社区最活跃的功能板块。
- **增强的模型管理**：核心需求是支持在单个会话中动态切换模型，特别是能方便地使用本地或自建（BYOK）模型，并与 GitHub 托管的模型进行对比。此外，`auto` 模式下行为不明确（如与 `reasoningEffort` 的冲突）也需要改进。
- **更强大的会话与上下文管理**：出现了跨设备、跨开发者的会话共享需求，旨在共享问题和解决过程的上下文，促进团队协作。另外，将单个会话的上下文导出到仓库（如生成文档）也是一个潜在方向。
- **编辑器体验（Vim 模式）**：一个长期存在且高赞的需求，表明有相当一部分开发者希望 CLI 能更好地融入其基于模态编辑器的键盘流工作方式。

### 6. 开发者关注点

从反馈中提炼出的高频痛点和需求：

- **配置与网络问题的排查难度**：诸如 MCP 服务器“看起来已启用但实际未连接”、企业策略阻止模型但无明确启用方法等问题，让开发者感到困惑和沮丧，这类问题的诊断引导有待加强。
- **版本更新与回归问题**：用户对自动化更新逻辑的 Bug（如 #4605）非常敏感，它会导致用户无法获取关键修复。同时，新版本引入的回归 Bug（如 MCP 令牌丢失、退出摘要消失）也严重影响了升级体验。
- **更精细的控制权和灵活性**：用户希望拥有更多的“开关”来控制 CLI 行为，例如忽略仓库 MCP 配置、为 `ask_user` 工具提供“自定义回答”的出口、以及持久化地排除特定指令文件的加载等。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-26** | 数据来源：GitHub `MoonshotAI/kimi-cli`

---

## 今日速览

过去 24 小时内，Kimi Code CLI 社区暂无新版本发布，也无新 PR 合入，整体保持平稳。值得关注的是，两个历史遗留的 **I/O 可靠性 Bug**（Edit/Write 静默失败、上下文压缩导致任务异常重开）在今日获得社区进一步讨论反馈，均指向了工具链在**文件系统写入确认**与**会话状态管理**上的稳定性短板，建议用户优先升级并关注后续修复版本。

---

## 版本发布

无。

---

## 社区热点 Issues

*近期 Issues 数量较少（累计 2 条），以下为全部活跃问题：*

### 1. Edit/Write 工具报告成功但未写入磁盘（#2617）
- **状态**：Open | 更新于 08-25 | 评论 2
- **影响**：**高** — 影响所有使用 Edit/Write 的自动化流程，静默失败会导致后续任务基于错误状态继续执行。
- **关键信息**：
  - 自 2026-08-25 17:00 UTC 起，在两个工具中均 100% 复现
  - 环境：v0.38.0, macOS
- **社区反应**：已有用户跟帖确认问题，但尚无官方回应。
- **链接**：[Issue #2617](https://github.com/MoonshotAI/kimi-cli/issues/2617)

### 2. 上下文压缩 Bug——已完成并删除的任务被重新打开（#2523）
- **状态**：Open | 更新于 08-25（重启讨论）| 评论 1
- **影响**：**中** — 历史遗留问题，仅在 Windows 平台复现，影响任务闭环管理。
- **关键信息**：
  - 版本：v0.6.3（较旧）
  - 平台：Windows NT 10.0.26200
- **社区反应**：沉寂一个月后再次被更新，说明用户仍受困扰。
- **链接**：[Issue #2523](https://github.com/MoonshotAI/kimi-cli/issues/2523)

---

## 重要 PR 进展

过去 24 小时内无新 PR 更新。

---

## 功能需求趋势

> 基于全部活跃 Issues 及近期历史数据分析：

1. **I/O 操作可靠性**（新）
   - 具体诉求：工具执行成功反馈需与磁盘实际状态保持一致，避免静默失败。
   - 代表：`#2617`

2. **会话状态管理**（持续）
   - 具体诉求：上下文压缩不应破坏任务的生命周期（删除/完成状态）。
   - 代表：`#2523`

3. **跨平台一致性**（持续）
   - 具体诉求：Windows 与 macOS 下的行为差异需收敛，尤其是文件系统与进程管理。
   - 代表：`#2523`, `#2617`

---

## 开发者关注点

1. **信任缺失风险**：`Edit`/`Write` 的静默失败严重削弱了开发者对 CLI 自动化的信任。高频使用文件编辑的开发者建议在关键路径上增加**手动验证**或使用 `bash` 命令替代，直至官方修复。
2. **压缩触发边界模糊**：用户对“何时触发上下文压缩”以及“压缩后哪些任务会被保留”缺乏清晰预期，导致旧任务被意外重开。
3. **平台差异容忍度低**：Windows 用户对 `v0.6.3` 遗留的会话管理问题长期未获修复表示不满，建议尽快验证最新版本是否已解决。

---

*本日报由 AI 自动生成，数据截至 2026-08-26。若需订阅每日更新或反馈建议，请联系维护者。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-26

---

## 今日速览

今日社区热点集中在 **Zen API 免费模型（Ox Alpha）对工具调用（tools）支持异常**，多个 Issue 报告 "Endpoint is unavailable" 错误。同时，社区对 **桌面端消息搜索、模型成本显示、会话编辑** 等功能的呼声持续高涨。值得欣慰的是，新版本 v1.18.23 已修复 Cloudflare AI Gateway 的路由问题，且社区贡献者 kitlangton 提交了多项 TUI 质量修复。

---

## 版本发布

### v1.18.23

**核心修复：**
- **Cloudflare AI Gateway 路由修复**：修复了第三方 providers 通过网关 REST API 时的路由问题，使非 Workers 模型能正常工作。
- **Anthropic 模型兼容修复**：修复了通过 Cloudflare AI Gateway 使用 Anthropic 模型时，点号模型 ID（如 `claude-haiku-4.5`）需转换为连字符格式（`claude-haiku-4-5`）的问题。

---

## 社区热点 Issues

### 1. Zen API 免费模型工具调用全面故障 ⚠️
**#44300** — [Zen API: x-preview-f-free / ox-alpha-free fails with "Endpoint is unavailable" for any request containing tools](https://github.com/anomalyco/opencode/issues/44300)  
**热度**：13 评论 | 5 👍  
**分析**：自 8 月 23 日起，Ox Alpha 免费模型在包含 `tools` 数组的请求中持续返回 "Endpoint is unavailable"。**问题对免费用户影响巨大，工具调用是 OpenCode 核心能力，当前免费模型几乎不可用。** 同类问题 #44850（7 评论）也独立报告了相同错误，且 #45073、#45020 均已因此被关闭，说明该问题波及范围极广。

### 2. Qwen 3.7 Plus/Max 工具调用偶发失败
**#33618** — [Qwen 3.7 Plus/Max (via OpenRouter) unknown/invalid tool calls](https://github.com/anomalyco/opencode/issues/33618)  
**热度**：10 评论 | 4 👍  
**分析**：通过 OpenRouter 使用 Qwen 3.7 Plus/Max 时，工具调用会间歇性失败，报错 `✗ "" failed`，导致会话反复重试甚至中断。**该问题持续两个月未解决，用户体验受损严重。**

### 3. 桌面端消息搜索功能呼声高
**#19143** — [[FEATURE]: Implement message search (Cmd+F / Ctrl+F) in the Desktop App](https://github.com/anomalyco/opencode/issues/19143)  
**热度**：9 评论 | 8 👍  
**分析**：桌桌面应用缺少在长会话中快速定位信息的能力。该需求自 3 月提出至今已 5 个月，获得 8 个赞，说明用户对会话导航能力有迫切需求。

### 4. TUI 多问题工具调用静默失败（回归）
**#35434** — [Bug: Multi-question tool calls fail silently in TUI since v1.17.13](https://github.com/anomalyco/opencode/issues/35434)  
**热度**：7 评论 | 0 👍  
**分析**：自 v1.17.13 起，`question` 工具在 TUI 中调用 2 个及以上问题时，按 Enter 无响应，事件不会发送到后端。**该回归问题已存在近两个月，影响多选交互场景。**

### 5. --log-level DEBUG 不输出日志
**#17846** — [--log-level DEBUG fails to log anything](https://github.com/anomalyco/opencode/issues/17846)  
**热度**：6 评论 | 2 👍  
**分析**：macOS 上当日志目录积累 10 个文件后，`--log-level DEBUG` 完全不输出日志，疑似日志轮转缺陷。**排查问题时的关键调试手段失效，增加用户排障成本。**

### 6. 模型选择器显示成本信息
**#14524** — [[FEATURE]: Display model cost in the model picker](https://github.com/anomalyco/opencode/issues/14524)  
**热度**：5 评论 | 11 👍  
**分析**：TUI 模型选择器不显示模型成本。**获得 11 个赞，是今日最高的功能类 Issue**，反映用户对成本透明化的强烈需求。

### 7. 会话永久卡死且无法恢复
**#43277** — [Sessions permanently stuck during normal use — survive reboots](https://github.com/anomalyco/opencode/issues/43277)  
**热度**：5 评论 | 0 👍  
**分析**：多个会话在日常使用中永久卡死，拒绝新消息，重启也无法恢复。**严重阻断工作流，涉及状态持久化问题，需紧急排查。**

### 8. 自动更新器吞噬 266 GB 磁盘
**#45087** — [[2.0] Auto-updater ate 266 GB by reinstalling OpenCode every 10 minutes](https://github.com/anomalyco/opencode/issues/45087)  
**热度**：4 评论 | 0 👍  
**分析**：2.0 版本的 `opencode2 serve --service` 每 10 分钟重新安装一次 beta 包，导致 `~/.npm/_cacache` 积累 266 GB 垃圾数据。**存储资源被严重浪费，是 v2 版本的重大缺陷。**

### 9. 编辑器上下文消息删除能力缺失
**#7712** — [[FEATURE]: I want to be able to edit the context to delete messages](https://github.com/anomalyco/opencode/issues/7712)  
**热度**：4 评论 | 12 👍  
**分析**：用户希望在死胡同中能删除上下文消息。**虽被标记为已关闭，但 12 个赞表明该需求仍被广泛认同。**

### 10. 自由模型可用性困惑
**#10620** — [[zen] Is free model only big pickle available?](https://github.com/anomalyco/opencode/issues/10620)  
**热度**：4 评论 | 0 👍  
**分析**：免费模型仅有 Big Pickle 可用，且质量不佳。**免费模式可能停摆的疑问反映了免费层生态的脆弱性。**

---

## 重要 PR 进展

### 1. 修复中断的 Mermaid 图表渲染 🎨
**#45102** (已合并) — [fix(tui): preserve interrupted Mermaid diagrams](https://github.com/anomalyco/opencode/pull/45102)  
**内容**：会话重开后，保留未完成的 Mermaid 流程图，避免中断导致图表丢失。**提升长会话的视觉连续性。**

### 2. 桌面端深链接打开会话 🔗
**#45103** — [feat(desktop): open existing sessions from deep links](https://github.com/anomalyco/opencode/pull/45103)  
**内容**：新增 `opencode://open-session?server=...&session=...` 深链接，支持从外部打开桌面端已有会话。**完善桌面端集成体验。**

### 3. 核心测试环境隔离 🧪
**#44845** (已合并) — [test(core): isolate host configuration and credentials](https://github.com/anomalyco/opencode/pull/44845)  
**内容**：核心测试套件不再加载个人插件、技能、MCP 服务器或凭据，确保测试环境纯净。**提升测试可靠性与可复现性。**

### 4. 新增 Cerebras 和 Together AI 原生支持 🚀
**#45098** — [feat(ai): add native Cerebras and Together AI providers](https://github.com/anomalyco/opencode/pull/45098)  
**内容**：为 Cerebras 和 Together AI 添加一等公民支持，基于现有 OpenAI Chat 协议。**扩展模型生态，用户无需手动配置。**

### 5. 修复 TUI 转录底部误判 📜
**#45100** — [fix(tui): detect clipped transcript bottom](https://github.com/anomalyco/opencode/pull/45100)  
**内容**：修复转录内容实际还有一行被裁剪时，界面误报已到达底部的问题。**提升 TUI 滚动体验精确度。**

### 6. 保留 provider 定义的响应 ID 格式
**#45094** — [fix(ai): preserve provider-defined responses item ids](https://github.com/anomalyco/opencode/pull/45094)  
**内容**：采用 Codex 的出站规则，放宽响应 ID 校验，保留 provider 下发的消息 ID。**增强与各 provider 的兼容性。**

### 7. 修复旧版字符串工具输入兼容性
**#44705** — [fix(session): coerce legacy string tool-part input](https://github.com/anomalyco/opencode/pull/44705)  
**内容**：修复 1.14 版本存储的工具输入为 JSON 字符串时，1.18 版本无法正常读取的问题。**解决升级后的数据兼容问题。**

### 8. 避免模型可用性误报
**#45097** (已合并) — [fix(tui): avoid false model availability warnings](https://github.com/anomalyco/opencode/pull/45097)  
**内容**：当客户端目录暂时缺失模型元数据时，不再错误标记模型为 `(unavailable)`。**减少不必要的用户困惑。**

### 9. 工具参数自动修复机制 🛠️
**#45002** — [feat(core): repair malformed tool arguments before validation](https://github.com/anomalyco/opencode/pull/45002)  
**内容**：新增内部插件，在标准验证器运行前自动修复常见的畸形工具参数。**提高工具调用的容错能力。**

### 10. 修复 SSE 重试指令处理
**#45093** (已合并) — [fix(ai): ignore SSE retry directives without ending streams](https://github.com/anomalyco/opencode/pull/45093)  
**内容**：忽略不终止流的 SSE 重试指令，保留命名事件数据。**提升流式响应的稳定性与完整性。**

---

## 功能需求趋势

| 方向 | 代表 Issue | 热度 | 说明 |
|---|---|---|---|
| **模型成本透明** | #14524 | 11 👍 | 用户在模型选择器中看到价格信息，优化成本决策 |
| **会话编辑** | #7712 | 12 👍 | 允许删除/编辑上下文消息，走出对话死胡同 |
| **桌面端体验** | #19143 | 8 👍 | 消息搜索、MCP 管理（#40335）、深链接（#45103） |
| **新模型/Provider 支持** | #45098 | - | Cerebras、Together AI、Azure CLI 认证（#45086/#45079） |
| **国际化** | #42447 | 3 评论 | 希伯来语（he）本地化支持 |
| **调试能力** | #17846 | 6 评论 | 修复 `--log-level DEBUG` 日志输出问题 |

---

## 开发者关注点

1. **免费模型可用性堪忧** — #44300、#44850、#45073 等多条 Issue 指向 Ox Alpha 免费模型工具调用全面故障，直接影响免费用户体验，是当前最高优先级问题。
2. **会话卡死与状态持久化问题频发** — 除 #43277（永久卡死）外，还有 #33995（会话锁定错误目录）、#43355（渲染器冻结）等问题，表明会话状态管理存在系统性缺陷。
3. **2.0 版本更新器存在重大缺陷** — #45087 暴露自动更新器每 10 分钟重复安装导致 266 GB 磁盘浪费，相关修复 PR #45091 已提交。
4. **模型兼容性持续挑战** — 无论是通过 OpenRouter 的 Qwen 工具调用问题（#33618），还是 SGLang 的系统消息位置限制（#45055），都表明模型 backend 兼容性是高频痛点。
5. **贡献者活跃度回升** — kitlangton 连续提交多个 TUI 修复 PR，open-code-agent 贡献 Azure CLI 认证功能，社区贡献正在加速。

---

*日报生成时间：2026-08-26 | 数据来源：[anomalyco/opencode](https://github.com/anomalyco/opencode)*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报

**日期：2026-08-26**
**数据来源：github.com/badlogic/pi-mono**


## 今日速览

昨日社区提交密集，核心聚焦于**流式输出稳定性**（TUI 逐词渲染错乱、工具结果图片导致会话中断）与**Windows 平台体验**（PowerShell 版本不一致、全局扩展加载失败）。修复方向上，多位贡献者围绕 `read` 工具行数计算、tool_choice 参数、图像处理等细节提交了高质量 PR。与此同时，累计 50 条 Issue 中约一半处于关闭状态，显示项目维护节奏较快，但 Windows 支持相关讨论热度持续升温。


## 社区热点 Issues (Top 10)

### 1. [#8584 TUI 流式渲染错乱：助手文本逐词换行](https://github.com/earendil-works/pi/issues/8584)
- **状态**: 已关闭 | 👍 5 | 💬 9
- **原因**: 工具输出长行后，助手文本流式渲染逐词换行，严重影响可读性。该问题与 [#8619](#8619) 的 thinking 逐词渲染类似，可能同源。

### 2. [#7547 Windows 用户如何使用 Pi？](https://github.com/earendil-works/pi/issues/7547)
- **状态**: 进行中 | 👍 2 | 💬 49
- **原因**: 社区最活跃讨论帖。Windows 上运行方式过多导致维护精力分散，维护者希望收集用户反馈以聚焦 bug 修复和文档优化。**适合 Windows 用户参与。**

### 3. [#5886 AgentSession 结算/续跑与 assistant-tail 生命周期缺陷](https://github.com/earendil-works/pi/issues/5886)
- **状态**: 进行中 | 👍 4 | 💬 9
- **原因**: mitsuhiko（Sentry 创始人）报告的一类 recurring bug 元问题：会话后置逻辑试图从已失效的 transcript 继续 agent。涉及 `pkg:agent` 与 `pkg:coding-agent`，影响面大。

### 4. [#7855 "Response was truncated before completion" 随机中断](https://github.com/earendil-works/pi/issues/7855)
- **状态**: 已关闭 | 👍 4 | 💬 7
- **原因**: 兼容 OpenAI 的 API（如本地 VLLM）随机触发截断错误，需要手动提示继续。虽然已关闭，但属于影响日常使用体验的高频问题。

### 5. [#8468 GitHub Copilot 登录超时](https://github.com/earendil-works/pi/issues/8468)
- **状态**: 已关闭 | 💬 6
- **原因**: Copilot 登录持续超时，用户需 checkout 特定 commit 绕过。与 #8254 的合并时机相关，对依赖 Copilot 的用户造成阻塞。

### 6. [#8582 PowerShell 工具交互模式与 -p 模式版本不一致](https://github.com/earendil-works/pi/issues/8582)
- **状态**: 已关闭 | 💬 6
- **原因**: Windows 下交互模式强制回退 PowerShell 5.1，即使已安装 pwsh 7。打印模式却使用 pwsh，行为不一致，Windows 用户可关注修复进展。

### 7. [#6596 `spawn(taskkill) ENOENT` —— Node.js 24 兼容](https://github.com/earendil-works/pi/issues/6596)
- **状态**: 进行中 | 💬 5
- **原因**: Node 24 下 `killProcessTree` 报 ENOENT，修复需使用 System32 绝对路径。影响 Windows 进程树清理，对长会话稳定性至关重要。

### 8. [#8456 Gemini 3.7 Flash 拒绝 MINIMAL thinking 的 /tree 分支总结](https://github.com/earendil-works/pi/issues/8456)
- **状态**: 已关闭 | 👍 2 | 💬 4
- **原因**: Google 适配器未按文档透传 `reasoning` 字段，导致 `thinkingLevel` 被忽略。涉及跨厂商适配一致性。

### 9. [#6600 `pi update --extensions` 被 npm 11.16 阻塞](https://github.com/earendil-works/pi/issues/6600)
- **状态**: 进行中 | 💬 4
- **原因**: npm 11.16 默认阻止 install scripts，Pi 扩展更新流程被破坏且缺少透传参数的文档。**影响所有扩展用户升级路径。**

### 10. [#8651 压缩预留 token 未按模型上下文窗口缩放](https://github.com/earendil-works/pi/issues/8651)
- **状态**: 已关闭 | 💬 3
- **原因**: 固定 `reserveTokens`（默认 16384）在小上下文模型中会超预算，导致误触发压缩。对本地小模型（llama.cpp 等）用户友好度提升。


## 重要 PR 进展 (Top 10)

### 1. [#8629 新增 Eager Tool 执行（opt-in）](https://github.com/earendil-works/pi/pull/8629)
- **状态**: 进行中
- **内容**: `read` 等明确可安全丢弃的本地工具在 `toolcall_end` 时预执行，正式调度时复用结果，可缩短感知延迟。V1 限定范围、有完整安全边界。

### 2. [#8633 移除无工具时的 Responses `tool_choice`](https://github.com/earendil-works/pi/pull/8633)
- **状态**: 已合并
- **内容**: 压缩时发送 `toolChoice: none` 但未带 tools，xAI 返回 400。此修复同步对齐 OpenAI/Azure Responses 与已完成处理的 Chat Completions 路径。**修复 Grok 的 /compact 失败问题。**

### 3. [#8650 同上问题的独立修复](https://github.com/earendil-works/pi/pull/8650)
- **状态**: 已合并
- **内容**: 与 #8633 功能重合，由另一位贡献者提交，确保该修复进入正确发布分支。

### 4. [#8642 Bedrock：OpenAI 模型 toolResult 图片提升](https://github.com/earendil-works/pi/pull/8642)
- **状态**: 已合并
- **内容**: OpenAI 模型在 Bedrock 上拒绝 `toolResult.content` 中的嵌套图片（如 `gpt-5.6-sol`），此 PR 将图片提升为同一条用户消息的兄弟 block。相关 issue #8643。

### 5. [#8623 read 工具行数统计修复（PHP 空行问题）](https://github.com/earendil-works/pi/pull/8623)
- **状态**: 已合并
- **内容**: `split("\n")` 在尾部换行时产生幻影空行，导致截断提示 "of N+1 lines"、续行提示错误。修复后所有可见症状消除。**解决 #7329。**

### 6. [#8641 bash 可用时加载 skills](https://github.com/earendil-works/pi/pull/8641)
- **状态**: 已合并
- **内容**: `read` 禁用但 `bash` 可用时仍应加载 skills 片段，调整系统提示词中的工具引导。修复 #8551，附带回归测试。

### 7. [#8639 新增 Opper Provider](https://github.com/earendil-works/pi/pull/8639)
- **状态**: 已合并
- **内容**: 内置 OpenAI 兼容 provider（`api.opper.ai/v3/compat`），含 provider 模块、models.dev 目录生成、默认模型、文档及兼容性测试矩阵。

### 8. [#8635 延迟设置期间保留 aborted 停止原因](https://github.com/earendil-works/pi/pull/8635)
- **状态**: 进行中
- **内容**: 将请求 abort 信号穿透 lazy stream 包装器，工具执行期间 abort 时正确上报为 aborted 而非 setup failure。修复 #8409，附带回归测试。

### 9. [#8570 保留 Codex thread affinity 头](https://github.com/earendil-works/pi/pull/8570)
- **状态**: 已合并
- **内容**: 为 OpenAI Codex Responses 请求补充 `thread-id` 头，与上游 Codex 客户端行为对齐（搭配已存在的 `prompt_cache_key`/`session-id`）。

### 10. [#8547 TUI 点击移动编辑器光标](https://github.com/earendil-works/pi/pull/8547)
- **状态**: 进行中
- **内容**: 鼠标选中文本后，点击 prompt 区域即可移动光标，无需键盘导航。提升鼠标模式下的编辑效率。


## 功能需求趋势

- **新模型/Provider 支持（持续高频）**: 社区持续提交新 provider 与模型目录更新（如 #8639 Opper、#8483 DeepSeek V4 Flash Vision、#4742 SiliconFlow），OpenAI 兼容接口生态仍在快速扩展。
- **流式输出稳定性**: TUI 逐词渲染错乱（#8584）、thinking 逐词显示（#8619）、压缩后截断（#8652）等流式链路问题集中爆发，已成为影响日常体验的首要痛点。
- **文件读取与工具可靠性**: read 工具行数偏移（#8623/#7329）、图片 EXIF 解析（#8616）、工具结果图片导致会话中断（#8636/#8642）等文件处理类修复密集出现。
- **Windows 支持体系化**: 从 PowerShell 版本不一致（#8582）、taskkill ENOENT（#6596）到 `pi update` 被 npm 阻塞（#6600），Windows 体验问题开始形成生态级讨论（#7547）。
- **性能优化（Eager 执行）**: #8629 的 eager tool 预执行是近期少见的架构级性能提案，目标直指工具调用延迟。


## 开发者关注点

1. **Windows 体验断层**: #7547 获得 49 条评论成为社区最热讨论，PowerShell 版本不一致、taskkill 路径、npm 11.16 脚本阻塞等问题叠加，Windows 用户“能用但不够顺”的反馈集中。

2. **流式渲染可靠性**: TUI 逐词换行、thinking 逐词显示、工具长输出后文本乱序——流式场景下的渲染 bug 高频出现，影响多模型（Gemini、OpenRouter 等）与多平台（Windows/Linux）。

3. **上下文管理与压缩策略**: 压缩 token 预留固定（#8651）、压缩后无有效 checkpoint（#8652）、截断后无法自动恢复（#7855）——上下文管理成为影响长会话稳定性的核心矛盾。

4. **图片与视觉模型兼容性**: 工具结果图片导致 `media_budget_exceeded`（#8636）、Bedrock 拒绝嵌套图片（#8643）、TUI 全屏图片渲染错误（#8306）——视觉输入的端到端链路（产生→传输→渲染）仍有较多断点。

5. **维护者对社区贡献响应积极但严格**: 大量 PR 在当日创建即被合并或关闭，但 untriaged 标签使用频繁，部分新提交未经完整评审即关闭后重开（如 #8642 自动关闭后 #8643 重开），社区贡献门槛仍偏高。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-26

## 今日速览

昨日发布 v0.22.0-nightly 版本，主要修复 Web Shell 会话工作目录传递问题。社区讨论热度集中在多智能体协作缺陷、上下文压缩错误及 `/effort max` 导致会话中断等核心功能问题上，同时开源社区对新功能提案（如 DAP 集成、上下文用量遥测）表现出积极关注。

---

## 版本发布

**v0.22.0-nightly.20260825.22bb5e8b9f** 已发布

更新内容：
- 修复 Web Shell 从概览面板打开会话时未正确传递工作目录的问题（[PR #9730](https://github.com/QwenLM/qwen-code/pull/9730)）

---

## 社区热点 Issues

### 1. `/effort max` 在 OpenAI 兼容提供商上导致会话中断 🔥
[#9459](https://github.com/QwenLM/qwen-code/issues/9459) — **已关闭** | 10 条评论

**问题概述：** UI 提供 `/effort max` 选项，但所有 OpenAI 兼容提供商均拒绝该参数，且 `clampReasoningEffort()` 未对其进行限制。设置后**该会话的每个后续请求都会以 400 错误失败**，直到手动切换回其他档位。

**社区反应：** 高度关注。该问题直接影响所有使用 OpenAI 兼容 API（如 vLLM、Ollama 等）的用户，属于高影响、低规避成本的严重 bug。

---

### 2. 后台智能体协作缺陷：重复工作、过早完成与 send_message 失效
[#8097](https://github.com/QwenLM/qwen-code/issues/8097) — 开放中 | 8 条评论

**问题概述：** 同时运行多个后台 Explore 子智能体并通过 `send_message` 通信时，出现三类协作失败：① 父智能体重复执行子智能体已完成的工作；② 子智能体过早报告完成；③ `send_message` 无法与飞行中的子智能体交互。

**社区反应：** 持续热议。多智能体协作是近期社区最关注的能力方向，该问题直指核心协作机制缺陷。

---

### 3. Skill 上下文生命周期管理
[#6762](https://github.com/QwenLM/qwen-code/issues/6762) — 开放中 | 6 条评论

**问题概述：** 请求新增 Skill 上下文生命周期管理机制。当前 SKILL.md 文件以工具结果形式加载进对话历史并**永久保留**，无法卸载、压缩或过期。

**社区反应：** 与上下文压缩、token 优化等议题联动，反映用户对长会话场景下上下文管理的迫切需求。

---

### 4. Qwen Code 内存溢出及终端渲染异常
[#9198](https://github.com/QwenLM/qwen-code/issues/9198) — 开放中 | 6 条评论

**问题概述：** 长时间运行（一周+）后触发 OOM（服务器内存 1TB），且崩溃后 tmux 终端按键错乱、无法复制粘贴。用户反馈 Kimi Code 无此问题。

**社区反应：** 内存泄漏与终端渲染问题叠加，严重影响长时间运行的稳定性，属高频痛点。

---

### 5. 上下文压缩行为异常
[#9309](https://github.com/QwenLM/qwen-code/issues/9309) — 已关闭 | 6 条评论

**问题概述：** 先执行 `/compress-fast` 再执行 `/compress`，首次压缩将上下文从 170k 压缩至 7k 左右，但后续压缩行为出现异常。用户质疑压缩策略的准确性。

**社区反应：** 压缩机制是用户重点关注功能，压缩过度或不足都会直接影响输出质量。

---

### 6. Windows 平台 `@` 文件读取符号链接保护失效
[#8227](https://github.com/QwenLM/qwen-code/issues/8227) — 开放中 | 5 条评论

**问题概述：** Windows 上 `O_NOFOLLOW` 不可用，`@` 引用文件读取的符号链接/TOCTOU 保护实质上比 Linux 弱得多，且目前无测试覆盖。

**社区反应：** 安全问题持续受到开发者关注，欢迎 PR 修复（已标记 welcome-pr）。

---

### 7. 后台 Cron 任务静默执行，模型无法查看或停止
[#5823](https://github.com/QwenLM/qwen-code/issues/5823) — 开放中 | 5 条评论

**问题概述：** `/loop` 创建的 cron 任务静默触发，模型无法列出或停止自己创建的计划任务。用户几天后回到编辑器，每个新会话都会自动开始执行未预期的工作。

**社区反应：** 自动化能力的可管理性问题，缺乏可见性和控制权是主要痛点。

---

### 8. 简单请求陷入 15 分钟+ 循环思考
[#4055](https://github.com/QwenLM/qwen-code/issues/4055) — 开放中 | 4 条评论

**问题概述：** 用户提出一个极其简单的文档修改需求，QC 陷入循环思考 15 分钟以上不回复。附加截图展示了大量无意义的循环思考内容。

**社区反应：** 长期未解决的高频痛点，严重影响基础使用体验，社区持续反馈中。

---

### 9. 原生 DAP（调试适配协议）集成
[#10051](https://github.com/QwenLM/qwen-code/issues/10051) — 开放中 | 4 条评论

**问题概述：** 请求为 Qwen Code 增加 DAP 支持，使智能体能以编程方式与调试器交互，而非仅依赖终端输出和源码分析。

**社区反应：** 新功能提案，反映开发者对智能体调试能力升级的期待。讨论中。

---

### 10. `/review` 在 fork 子代理上下文中运行完整流水线
[#9784](https://github.com/QwenLM/qwen-code/issues/9784) — 开放中 | 3 条评论

**问题概述：** 完整 `/review high` 运行会注入 ~95k token 的 SKILL.md，并在主对话中累积 14+ 代理返回、验证器分片、反向审计轮次等大量上下文。建议将整个流水线移至 fork 子代理上下文中执行。

**社区反应：** 核心维护者提出，与多智能体架构和上下文管理方向一致，预计将推动后续架构演进。

---

## 重要 PR 进展

### 1. [PR #9260](https://github.com/QwenLM/qwen-code/pull/9260) — 手动会话名称跨 `/clear` 保留
手动设定的 Web Shell 会话名称在 `/clear` 后不再丢失。新会话在附加和首次提示前持久化该名称，防止自动标题生成覆盖用户标签。已含事件溯源和数据迁移支持。

### 2. [PR #9980](https://github.com/QwenLM/qwen-code/pull/9980) — 编辑前加载模型推荐
在设置向导到达模型 ID 步骤时，Token Plan 和 Coding Plan 可选发起一次 OpenAI 兼容模型列表请求，显示可取消的加载状态，替代此前有争议的 #9389 方案。

### 3. [PR #8927](https://github.com/QwenLM/qwen-code/pull/8927) — 按频道会话轮换机制
新增 `sessionRotation` 选项限制路由保持同一会话的时长，支持 `maxTurns` 和 `maxTtl` 两种边界。达到边界后，下一条消息自动开启新会话。

### 4. [PR #9305](https://github.com/QwenLM/qwen-code/pull/9305) — 垂直模式内容底部对齐
VP 模式下会话内容在视口内显示时底部对齐，消除最后一条消息与输入框之间的空白间隙（修复 #9300）。

### 5. [PR #9761](https://github.com/QwenLM/qwen-code/pull/9761) — 延迟建议脱离 PR 页面可恢复
`/review` 收敛姿态启用后（默认从第 6 轮开始），无法内联发布的建议移入审查主体的延迟列表，并使其可供后续到达的工具恢复。

### 6. [PR #10016](https://github.com/QwenLM/qwen-code/pull/10016) — 上下文使用量遥测属性
为面向用户的 LLM 请求新增 `qwen-code.context.usage` OpenTelemetry 属性，以版本化 JSON 报告有效上下文窗口、六个聚合输入类别、自动压缩储备及保留信息。

### 7. [PR #9940](https://github.com/QwenLM/qwen-code/pull/9940) — 审查发现回写入原线程
多轮审查中仍存在的发现将以回复形式落入原内联评论线程，而非新开口；已修复的发现会反馈到 PR（线程获得 ✅ 标记）。

### 8. [PR #9984](https://github.com/QwenLM/qwen-code/pull/9984) — Web Shell 可选交互式浏览器终端
独立 Web Shell 可选用 Terminal 操作，客户端需守护进程具备 `web_terminal` 能力后才展示，保证前后端版本兼容。

### 9. [PR #9988](https://github.com/QwenLM/qwen-code/pull/9988) — Web Shell 会话 Token 用量面板
新增可选的 Token 用量面板，展示总用量、按模型细分、子代理调用次数和本地化工具统计，支持手动刷新、后台轮询和折叠详情。

### 10. [PR #9659](https://github.com/QwenLM/qwen-code/pull/9659) — 基于内容锚定的增量审查循环
将本地审查-修复循环改为内容锚定的增量轮次（已在 #9190 上获得 20 条审查、166 条内联评论），在 `main` 上重新落地。

---

## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|------|--------------|------|
| **多智能体协作** | #8097、#9784、#9659、#9940 | 🔥🔥🔥 |
| **上下文管理优化** | #6762、#9309、#10015、#10016 | 🔥🔥🔥 |
| **Web Shell 体验完善** | #9260、#9984、#9988、#9993 | 🔥🔥 |
| **审查流水线增强** | #9784、#9940、#10010、#9902 | 🔥🔥 |
| **安全加固** | #8227、#9983 | 🔥🔥 |
| **性能与稳定性** | #9198、#10035 | 🔥🔥 |
| **调试能力** | #10051（DAP 集成） | 🔥 |
| **遥测与可观测性** | #10015、#10016 | 🔥 |

---

## 开发者关注点

### 🔴 高频痛点

1. **上下文管理不透明** — 压缩机制缺少用户控制，压缩结果不可预测，且 skill 上下文永久驻留无卸载机制（#6762、#9309）
2. **多智能体协作可靠性不足** — 重复工作、通信失败、过早完成等协作缺陷直接影响自动化任务效果（#8097）
3. **长时间运行稳定性** — OOM、循环思考、终端渲染异常在长时间或简单任务中频发（#9198、#4055）
4. **参数兼容性** — `/effort max` 在 OpenAI 兼容提供商上导致整个会话不可用，需有防御性处理（#9459）
5. **后台任务缺乏可见性** — cron/计划任务静默触发且无法管理，给用户带来失控感（#5823）

### 📌 其他关注点

- Windows 平台安全机制与 Linux 存在差距，社区期待补齐（#8227）
- 审查流水线在长轮次下的上下文体量、收敛机制和增量策略持续被讨论和优化
- 开发者对新能力的兴趣点集中在调试协议（DAP）集成和可观测性增强方向
- Web Shell 作为轻量级交互界面，其功能完善（终端、Token 面板）正成为社区贡献热点

---

*本日报由 AI 自动生成，数据截至 2026-08-26。仅代表社区讨论热点，不代表官方立场。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-26

> **数据说明**：以下内容基于 GitHub 仓库 Hmbown/DeepSeek-TUI 及其关联项目 CodeWhale 的公开 Issue/PR 数据整理（实际数据来源于 CodeWhale 仓库，DeepSeek-TUI 应为同一项目或关联项目）。部分 Issue/PR 标题中同时出现 “CodeWhale” 与 “DeepSeek-TUI”，此处按数据源统一整理。


## 今日速览

当前正处于 **v0.9.12 版本迭代关键期**：一条集成了 72 个提交的整合分支（#5576）已完成全部发布阻断项，正在进行版本号更新与变更日志收尾。本周社区讨论热度集中在 **Provider 中立性重构**（消除 DeepSeek 专属限制）与**监督运行控制面**（control socket、生命周期事件 outbox）两大主题，由核心维护者与资深用户共同推动。


## 版本发布

过去 24 小时内无新 Release。


## 社区热点 Issues（10 条精选）

### 1. Provider 中立性：18 处 DeepSeek 专属门禁应改为通用逻辑
- **#5588** | 作者: Hmbown | 评论: 5 | [链接](https://github.com/Hmbown/CodeWhale/issues/5588)
- **为什么重要**：对全部 279 个文件、2281 行生产代码中的 “deepseek” 字段进行完整审计，发现 18 处行为被 DeepSeek 绑定、但概念上应 Provider 中立（如 NVIDIA NIM 环境变量泄漏已修复）。这是该项目从 DeepSeek 专用工具走向多 Provider 平台的关键一步。
- **社区反应**：评论者对该批修复表示认可，并期待更多 Provider 适配。

### 2. 工作流 responseSchema 失败需要有限修复与原始输出凭证
- **#5583** | 作者: jbovard2016 | 评论: 4 | [链接](https://github.com/Hmbown/CodeWhale/issues/5583)
- **为什么重要**：当子任务返回非 JSON 内容导致 Schema 校验失败时，当前实现直接失败但未提供有限重试机会，也未保留原始输出供排查。该问题影响所有使用结构化输出的工作流场景。
- **社区反应**：评论者补充了更多 schema 失败的真实场景，认为“bounded repair”是必要的容错机制。

### 3. 工作流所有者快照将 Degraded 状态错误折叠为 Completed
- **#5582** | 作者: jbovard2016 | 评论: 4 | [链接](https://github.com/Hmbown/CodeWhale/issues/5582)
- **为什么重要**：代码中 `WorkflowRunStatus::Degraded` 被归入 `Completed` 分支，导致降级运行被展示为成功，掩盖了部分子任务失败的事实。对运维可见性造成误导。
- **社区反应**：该问题与 #5583 同批提出，评论者认为 Degraded 应有独立的 UI 状态。

### 4. 监督式运行的控制面：per-session 控制套接字
- **#5533** | 作者: M-Maciej | 评论: 3 | [链接](https://github.com/Hmbown/CodeWhale/issues/5533)
- **为什么重要**：作者在终端复用器、自动化测试框架、CI 等外部监督场景下运行 codewhale，需要一套消息/中断/重启/状态查询的控制套接字。这填补了 TUI 应用在无人值守场景下的运维空白。
- **社区反应**：来自资深用户的真实场景驱动，被纳入 v0.9.12 的 I 系列计划。

### 5. 本地生命周期事件 outbox（JSONL + webhook）
- **#5531** | 作者: M-Maciej | 评论: 3 | [链接](https://github.com/Hmbown/CodeWhale/issues/5531)
- **为什么重要**：与 #5533 配套，为外部监督者提供 `turn_stalled` / `turn_failed` 等生命周期事件，支持 JSONL 文件和 webhook 输出。适用于夜间无人值守、告警通知等场景。
- **社区反应**：评论者认为事件驱动是“让 TUI 可被编程化”的重要一步。

### 6. 陈旧写锁永久存在，连锁阻塞其他代理执行命令
- **#5562** | 作者: slowly247 | 评论: 3 | [链接](https://github.com/Hmbown/CodeWhale/issues/5562)
- **为什么重要**：子代理会话结束后，写锁声明未释放，导致后续代理无法执行写操作（Windows 10 环境可稳定复现）。属于并发控制的核心缺陷。
- **社区反应**：评论者给出了补充日志，“verifier”角色的行为与其描述矛盾，加剧了混乱。

### 7. 全新安装时 MiniMax / Xiaomi 模型配置返回 404
- **#5601** | 作者: Brook-WZ | 评论: 3 | [链接](https://github.com/Hmbown/CodeWhale/issues/5601)
- **为什么重要**：新用户配置 MiniMax 和 Xiaomi 模型时内置 URL 错误，导致 API Key 输入后立即报错，只能从 0.6 版本降级才能绕过配置命令。直接影响新用户首次体验。
- **社区反应**：中文用户的真实反馈，确认 deepseek 正常但其他两个模型存在内置 URL 错误。

### 8. 后台 git 命令频繁运行，且探针持有 `.git/index.lock`
- **#5617** | 作者: LmeSzinc | 评论: 2 | [链接](https://github.com/Hmbown/CodeWhale/issues/5617)
- **为什么重要**：codewhale 内部只读探针调用真实 git CLI（`git status` 等），在仓库中可能持有 `index.lock`，导致用户自己的 `git commit` 偶发失败。属于开发流程中的“工具打架”问题。
- **社区反应**：评论者指出这是 gitoxide 迁移的直接动机（见 #5618）。

### 9. 事件粒度审计：回合边界处表面卡死
- **#5581** | 作者: Hmbown | 评论: 2 | [链接](https://github.com/Hmbown/CodeWhale/issues/5581)
- **为什么重要**：当一次回合跨越多次模型调用时，仅依赖 `TurnComplete` 事件更新的表面看起来“冻结”。审计发现成本显示已修复，但其他表面仍停留在回合粒度。
- **社区反应**：属于用户体验细节的持续打磨，优先级中等。

### 10. 全新安装的首次配置流程：/tutorial 教程分页器
- **#5556** | 作者: Hmbown（已关闭） | 评论: 4 | [链接](https://github.com/Hmbown/CodeWhale/issues/5556)
- **为什么重要**：首次运行引导目前仅有极简骨架，缺少面向从 Claude Code / Cursor / Codex 迁移用户的对照式教程页。该 Issue 已关闭但被拆解实施，说明新用户引导是当前 UX 重点。


## 重要 PR 进展（10 条精选）

### 1. v0.9.12 集成分支：72 个提交的发布阻断合集
- **#5576** | 作者: Hmbown（进行中） | [链接](https://github.com/Hmbown/CodeWhale/pull/5576)
- **状态与内容**：v0.9.12 版本的整合分支，包含全部发布阻断修复和 UX 改进。当前已代码冻结，剩余工作为版本号更新与变更日志/RC 门禁。

### 2. git_status/git_diff 移出异步执行器线程
- **#5616** | 作者: rafaelcavalheri | [链接](https://github.com/Hmbown/CodeWhale/pull/5616)
- **修复内容**：`GitStatusTool`/`GitDiffTool` 在异步 `execute()` 中直接调用阻塞的 `std::process::Command::output()`，可能卡死整个会话。改为阻塞操作移出 tokio 线程池。

### 3. 聚焦转录操作：y 复制内容、Y 复制元数据、Enter 全屏
- **#5608** | 作者: wuisabel-gif | [链接](https://github.com/Hmbown/CodeWhale/pull/5608)
- **功能**：实现了 #5551 的聚焦切片 — 转录焦点块支持 `y` 复制内容、`Y` 复制元数据/收据、`Enter` 全屏阅读模式。改善长输出场景的复制和查看体验。

### 4. 工具与 MCP Schema 成本展示
- **#5611** | 作者: Hmbown（rebase of #5603） | [链接](https://github.com/Hmbown/CodeWhale/pull/5611)
- **功能**：上下文检查器（/context）新增工具目录总成本、按内置工具拆分的 schema 成本估算行，以及每个 MCP Server 工具的成本行。帮助用户了解每个工具和 MCP Server 的每轮 token 成本。

### 5. Windows 路径保留：verbatim 路径操作数通过 POSIX 分词
- **#5610** | 作者: aboimpinto | [链接](https://github.com/Hmbown/CodeWhale/pull/5610)
- **修复内容**：修复两个 Windows CI 失败（FEAT-019 的阻断项）。根因是只读工作区操作数在 POSIX 分词时未保留 Windows verbatim 路径，现已修复。

### 6. 控制套接字 — part d（最终）
- **#5594** | 作者: M-Maciej | [链接](https://github.com/Hmbown/CodeWhale/pull/5594)
- **功能**：关闭 #5533。新增可选 Unix-only 的 newline 分隔 JSON-RPC 控制套接字（`[control_socket] enabled = true`），每会话绑定，支持消息/中断/重启/状态查询，默认关闭。

### 7. /relaunch 命令 — part c
- **#5593** | 作者: M-Maciej | [链接](https://github.com/Hmbown/CodeWhale/pull/5593)
- **功能**：关闭 #5532。`/update` 安装新二进制后新增 `/relaunch` 命令，一键切换当前会话到新二进制，保留持久化、终端恢复和遥测刷新。

### 8. 生命周期事件 outbox — part b
- **#5592** | 作者: M-Maciej | [链接](https://github.com/Hmbown/CodeWhale/pull/5592)
- **功能**：关闭 #5531。新增 `[lifecycle_outbox]` 配置，交互式 TUI 和 headless `codewhale exec` 均会向 JSONL 文件追加生命周期事件，无需 shell 钩子。

### 9. 子代理审批凭证持久化
- **#5584** | 作者: cyq1017 | [链接](https://github.com/Hmbown/CodeWhale/pull/5584)
- **修复内容**：关闭 #5543。子代理审批提示此前仅基于内存决策授予工具调用权限，缺少持久化 Asked 或终端证据。现在审批凭证库被子运行时继承，并在暴露提示前提交 Asked，关闭前提交终端结果。

### 10. 发布事实的自动更新：latest-published-release.json
- **#5612** | 作者: Hmbown | [链接](https://github.com/Hmbown/CodeWhale/pull/5612)
- **修复内容**：`web/data/latest-published-release.json` 此前手工维护且从未被写入，导致停留在 v0.9.10 而 v0.9.11 已发布。该问题导致营销部署先成功后失败，现已修复为自动更新。


## 功能需求趋势

1. **Provider 中立化 / 多模型支持**
   来自 #5588（18 处 DeepSeek 专属门禁）与 #5601（MiniMax/Xiaomi 404）。社区要求模型配置具备一致的可用性，且架构上不再绑定单一 Provider。

2. **监督运行 / 无人值守可编程性**
   来自 #5533（控制套接字）、#5531（生命周期 outbox）。资深用户推动的“TUI 可被外部监督”能力，已形成 PR 落地。

3. **TUI 交互精细化**
   来自 #5556（/tutorial 教程）、#5551（聚焦块操作）、#5553（/context 成本归因）、#5550（行范围 @ 引用与隐藏文件）。核心维护者主导 UX 打磨，方向明确。

4. **成本可见性与配额控制**
   来自 #5567（Fleet 级成本上限）、#5553（工具/MCP schema 成本）、#5597（分离代理的用量丢失）。成本透明化是高频诉求，已在 v0.9.12 中重点推进。

5. **Git 操作稳健性**
   来自 #5617（index.lock 竞争）、#5618（gix/gitoxide 迁移）、#5616（异步阻塞调用）。开发者的自身 Git 工作流被打断，社区推动内部 git 操作架构升级。


## 开发者关注点

1. **`git status` / `git diff` 阻塞异步执行器**（PR #5616 修复）：此前 git 探针可致整个会话卡死，现已移出 tokio worker 线程，但 gix 迁移（#5618）仍在推进。

2. **只读子代理被环境变量限制绑架**（PR #5610 修复）：Windows 下只读操作数经 POSIX 分词后丢失 verbatim 路径，FEAT-019 阻断。修复后 Windows CI 恢复。

3. **多 Provider 配置的“开箱即用”体验**（#5601）：MiniMax/Xiaomi 内置 URL 错误导致新用户无法配置，中文用户需从旧版本降级才能绕过。新模型的上手门槛仍是痛点。

4. **子代理审批缺少持久化证据**（#5584 修复）：审批决策无持久化记录，存证和审计能力不足。

5. **发布事实滞后导致营销部署失败**（#5612 修复）：`latest-published-release.json` 为手工维护且长期未更新，构建流水线中的自动化缺口。

6. **CI 与发布门禁的健壮性**（#5614）：`check-versions.sh` 在 tag 拉取失败时静默跳过发布检查，现改为无法运行时直接报错，防止“假绿灯”。

---

📮 本日报由 AI 开发工具技术分析师自动生成（2026-08-26），数据来源：github.com/Hmbown/DeepSeek-TUI（实际数据来自关联仓库 CodeWhale）。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*