# AI CLI 工具社区动态日报 2026-08-13

> 生成时间: 2026-08-13 00:54 UTC | 覆盖工具: 9 个

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

**日期：2026-08-13** | 分析范围：Claude Code / OpenAI Codex / Gemini CLI / GitHub Copilot CLI / Kimi Code CLI / OpenCode / Pi / Qwen Code / DeepSeek TUI (CodeWhale)


## 1. 生态全景

当前 AI CLI 工具赛道已进入 **"稳定性与可靠性优先"** 的竞争阶段——核心 Agent 能力（多智能体协作、上下文管理、工具调用）从"能用"走向"可信"，各产品在功能覆盖上高度趋同之后，开始比拼执行确定性、安全边界与长会话稳定性。头部产品（Claude Code、Codex、Gemini CLI）均遭遇高频稳定性回归报告，侧证用户基数已具规模且使用深度在提升。与此同时，**桌面端（Desktop）与 Web Shell 成为新的体验竞争层**，Windows 平台稳定性、远程开发支持、终端兼容性是当前最集中的用户抱怨点。安全类 PR（命令注入防护、SSRF、配置 Fail-Open）密集合入，行业正处在**安全加固周期**。整体格局仍未固化——多款工具（Kimi Code、DeepSeek TUI 等）尚在功能补齐阶段，抢位窗口依然存在。


## 2. 各工具活跃度对比（近 24 小时）

| 工具 | Issues 更新 | PR 更新 | Release | 显著动态 |
|------|------------|---------|---------|---------|
| Claude Code | 10（Top 10 精选） | 5 | v2.1.229 | hook/网关稳定性改进；Linux 桌面版诉求 498 👍 居首 |
| OpenAI Codex | 10（Top 10 精选） | 10 | rust-v0.148.0-alpha.9 | Windows Computer Use 系列故障成焦点；插件指标采集基建成 PR 主力 |
| Gemini CLI | 10（Top 10 精选） | 10 | v0.56.0-nightly | P1 Agent 可靠性问题持续 5 个月+；安全修复密集合入 |
| Copilot CLI | 10（Top 10 精选） | 3 | 无 | 企业模型可用性波动；MCP 认证/生命周期缺陷集中爆发 |
| Kimi Code CLI | 1 | 2 | 无 | Memory System 功能请求持续发酵（35 评论）；外部 PR 等待 5 个月后获更新 |
| OpenCode | 10（Top 10 精选） | 10 | v1.18.17 | Zen 免费额度误判成最大吐槽点；Mermaid 渲染落地 |
| Pi | 10（Top 10 精选） | 10 | 无（日常高活跃） | auto-compaction 失效讨论升温；本地 Ollama 代理已合入 |
| Qwen Code | 10（Top 10 精选） | 10 | 5 个版本（含 desktop v0.2.1） | 长任务自动运行失败受激烈吐槽；Review 技能系列改进为开发重点 |
| DeepSeek TUI (CodeWhale) | 10（精选） | 10（精选） | v0.9.6 | v0.9.5 回归问题 24h 内被定位；"Harvest 合并流"加速社区 PR 落地 |

**整体判断**：除 Kimi Code 社区活跃度偏低外，其余工具均保持每日多版本、数十 Issue/PR 的高迭代节奏。


## 3. 共同关注的功能方向

### 3.1 会话/上下文管理可靠性（最广泛共识）
| 工具 | 具体诉求 |
|------|---------|
| Claude Code | Remote Control 会话恢复；多机状态中继（MEP PR） |
| OpenAI Codex | `/fork` 后父线程无法恢复；线程 resume 静默丢数据 |
| Pi | auto-compaction 失效导致 API 溢出 |
| Qwen Code | 大会话恢复超时保护；自动记忆召回可靠性 |
| Gemini CLI | Auto Memory 无限重试低信号会话 |
| DeepSeek TUI | 中断输出应作为一等会话对象保留 |

**共性结论**：跨会话连续性、持久化上下文、压缩/恢复的正确性是所有工具面临的共同技术挑战，且直接影响用户对 Agent 的信任度。

### 3.2 多智能体（Agent）协作稳定
| 工具 | 具体诉求 |
|------|---------|
| Claude Code | 单夜 12 个多智能体协调 bug 复盘 |
| Gemini CLI | 子代理误报成功；通用代理无限挂起 |
| Qwen Code | 后台 Explore 子代理重复工作、过早完成 |
| Copilot CLI | 子代理模型被静默降级/覆盖 |
| Gemini CLI | "Agent 调用 Agent" 委派机制（PR 推进中） |

**共性结论**：多智能体编排从"演示"走向"生产"，协调正确性、状态一致性、对模型自指参数的控制成为关键缺口。

### 3.3 模型治理与成本可见性
| 工具 | 具体诉求 |
|------|---------|
| Copilot CLI | 企业模型可用性波动；BYOK 模型列表动态化 |
| OpenCode | Zen 免费额度误判；付费用户仍受限 |
| Gemini CLI | 模型容量耗尽误判修复；容量重试策略 |
| Codex | 线程用量/成本在状态栏与 /status 中展示 |
| Claude Code | 默认模型静默升级导致 $506 意外费用 |

**共性结论**：企业级成本管控、额度判定准确性、模型选择透明化正在成为新刚需。

### 3.4 安全加固（集中在 Gemini CLI / DeepSeek TUI / Copilot CLI）
- 命令注入绕过（Gemini CLI `$VAR` 展开漏洞）
- SSRF 域名绕过（Gemini CLI web-fetch）
- 配置损坏 Fail-Open 权限失控（Gemini CLI MCP）
- 锁依赖版本安全公告（DeepSeek TUI RUSTSEC）
- 工具参数可被模型静默覆盖策略（Copilot CLI）

### 3.5 Windows 平台体验（桌面端 / WSL）
| 工具 | 具体问题 |
|------|---------|
| Claude Code | GPU 崩溃杀死全部会话；反复崩溃需 Repair |
| Codex | Computer Use 截图/提权多重故障；VS Code 扩展 WSL2 下 Context 失效 |
| Copilot CLI | WSL2 下 Ctrl+H 误判；Windows 套接字错误 |
| Qwen Code | tmux 下闪屏 |

**共性结论**：Windows 桌面端已成为稳定性重灾区，也意味着该平台存在差异化竞争机会。


## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术特征 | 当前突出短板 |
|------|---------|---------|---------|-------------|
| **Claude Code** | 企业级全功能 Coding Agent | 企业开发者、重视合规的组织 | 丰富 hook/网关机制；远程控制；桌面端矩阵 | Linux 桌面版长期缺失；Windows 稳定性差 |
| **OpenAI Codex** | 深度 Agent 自动化 + Pro 用户生态 | ChatGPT Pro/Enterprise 用户、深度 Agent 用户 | Rust 重写推进中；插件指标采集基建完善；Codex 云端集成 | Windows Computer Use 不可用；桌面端内存管理问题 |
| **Gemini CLI** | 高可靠 Agent 执行 + 快速模型迭代 | Google 生态开发者、大规模自动化场景 | eval 体系建设领先；安全加固密集；夜间版快速迭代 | Agent 子代理可靠性久拖未决 |
| **Copilot CLI** |  GitHub 原生集成 + 企业治理 | GitHub 生态用户、企业组织 | ACP 扩展协议；tgrep 原生搜索；模型覆盖策略机制 | 企业模型同步缺陷；MCP 生态不成熟 |
| **Kimi Code CLI** | 轻量快速迭代 | 个人开发者、Moonshot 生态用户 | Web 运行器；Shorten middle 输出优化 | 社区体量小；Memory System 久未落地 |
| **OpenCode** | 免费模型 + 开源透明度 | 成本敏感型个人开发者 | Zen 引擎多模型路由；Mermaid 终端渲染 | 计费/额度判定混乱 |
| **Pi** | 可扩展 TUI + 本地模型支持 | 高级终端用户、Extension 开发者 | 活跃的 Extension API；本地 Ollama 代理；丰富的 TUI 交互钩子 | auto-compaction 极端场景不可靠 |
| **Qwen Code** | 多模型多模态 + Web Shell 产品化 | 中文开发者、使用 Qwen 模型生态用户 | Web Shell 富交互；Review 技能套件；多模态路线图 | 长任务执行失败；CI 不稳定 |
| **DeepSeek TUI (CodeWhale)** | 轻量终端优先 + 快速社区响应 | 终端极致爱好者、个人开发者 | Rust/Ratatui；"Harvest 合并流"加速社区 PR；多 Provider 接入 | v0.9.5 回归问题；品牌更名尚在过渡期 |


## 5. 社区热度与成熟度

**高度活跃且成熟（每日高并发讨论+多版本滚动）**：Claude Code、OpenAI Codex、Gemini CLI、Pi、OpenCode、Qwen Code。这些社区 Issue 评论多、高赞密集、PR 合入节奏快，用户深度参与功能讨论与缺陷反馈。

**活跃但治理模型更有控制力**：Copilot CLI 社区讨论量大，但 PR 更新量少（24h 仅 3 条），且出现 bot 误提交，控管较收紧。

**相对低速**：Kimi Code CLI 24h 仅 1 Issue 更新，社区体量小。

**处于快速迭代与品牌过渡期**：DeepSeek TUI 更名为 CodeWhale 后发布 v0.9.6，社区反馈响应速度快（回归 24h 内定位并进入修复），正通过"Harvest"流程快速吸收社区 PR。

**值得注意**：Gemini CLI 的 eval 体系是当前所有工具中建设进最最系统的（EPIC #24353 已有 76 个行为评估覆盖 6 个模型版本），显示其质量保障投入领先。


## 6. 值得关注的趋势信号

1. **多智能体协调将成为下一个"主战场"**：Claude Code 复盘 12 类协调 bug、Gemini CLI 子代理可靠性 P1 未决、Qwen Code 后台代理重复工作，均指向多 Agent 场景从 demo 走向生产必然伴随的调试与治理难题。提前布局 Agent 可观测性和协调基础设施的工具将建立长期优势。

2. **企业级成本可见性/控制成为刚需**：Codex 在 TUI 状态栏直接展示线程信用/成本，OpenCode 因计费误判被社区集中吐槽，Claude Code 用户因静默升级产生 $506 账单——**"省钱"和"对成本有掌控感"正在成为企业选型的核心考量**。具备细粒度用量 API、预算上限、成本预警的工具将更受企业欢迎。

3. **安全加固进入"深水区"**：从命令注入绕过到 SSRF 域名解析绕过，攻击面正在从显性漏洞转向隐性边界（配置解析失败时的 Fail-Open 行为、DNS 解析与 IP 检查的时序差）。开发者应关注工具的 **"fail-safe vs fail-open"** 默认策略，这直接关系到安全边界可信度。

4. **Windows 平台是当前的"战略真空带"**：多工具在 Windows 桌面端/Computer Use 上故障频发，用户体验距离 macOS 有显著差距。**在 macOS 竞争饱和的背景下，率先提升 Windows 稳定性和 WSL2 体验的工具可能获得显著的增量市场份额**。

5. **本地模型与隐私敏感场景孕育新机会**：Pi 合入 Ollama 本地代理，OrcaRouter 接入（OpenCode、DeepSeek TUI 同步跟进），Codex 支持 BYOK 模型列表动态化——**离线/自托管/自带密钥的需求正在从边缘走向主流**，尤其是配合企业数据合规要求。

6. **Extension/Plugin 生态开始成为分水岭**：Claude Code 的 hooks 体系、Gemini CLI 的 Agent 委派、Pi 的 Extension API、Copilot CLI 的 ACP 协议、CodeWhale 的插件管理器——**可扩展性正在决定工具的上限**。开发者应关注生态开放程度与第三方贡献活跃度，这通常决定了长期使用中的问题解决速度。

---

*报告基于各 GitHub 仓库 2026-08-13 公开数据分析整理，数据源详见各工具日报。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据范围**：anthropics/skills 仓库（截止 2026-08-13）


## 一、热门 Skills 排行

### 1. skill-creator 修复系列（#1298 / #1099 / #1050 / #539）
- **功能**：修复官方 skill-creator 的 eval/优化循环在 Windows 平台不可用的问题（recall 恒为 0%、子进程崩溃、YAML 解析静默失败）
- **社区讨论热点**：这些 PR 直接对应 Issue #556（12 条评论，7 👍）和 #1169——run_eval.py 在 Windows 上所有查询都无法触发 skill，导致描述优化循环在对噪声做优化。社区对官方工具链的平台兼容性不满集中爆发
- **状态**：全部 OPEN，已堆积 3 个多月，是当前仓库积压最久的官方工具修复
- [PR #1298](https://github.com/anthropics/skills/pull/1298) | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050)

### 2. document-typography（#514）
- **功能**：面向 AI 生成文档的排版质量控制——孤词换行、孤行段落、编号错位
- **社区讨论热点**：直击 LLM 生成文档的普遍痛点，任何用 Claude 产出文档的用户都会遇到；无需额外依赖，开箱即用
- **状态**：OPEN（自 3 月初至今 5 个月）
- [PR #514](https://github.com/anthropics/skills/pull/514)

### 3. ODT skill（#486）
- **功能**：OpenDocument 格式（.odt/.ods）的创建、填充、解析为 HTML
- **社区讨论热点**：补齐官方文档套件的格式覆盖（现有 docx/pdf 均区分大小写路径引用，见 #538），满足开源/ISO 标准格式的工作流需求
- **状态**：OPEN（5.5 个月）
- [PR #486](https://github.com/anthropics/skills/pull/486)

### 4. ServiceNow 平台 skill（#568）
- **功能**：覆盖 ServiceNow 全平台（ITSM、ITOM、ITAM/SAM、FSM、HRSD、CSM、SPM、SecOps、IntegrationHub）
- **社区讨论热点**：企业级平台覆盖的代表性需求；作者持续更新至 8 月 12 日，生命周期长达 5 个月，显示维护意愿强
- **状态**：OPEN
- [PR #568](https://github.com/anthropics/skills/pull/568)

### 5. self-audit（#1367）
- **功能**：交付前审计——先做机械文件核验（输出文件是否存在），再做四维度推理质量审计（按破坏严重度排序），跨项目、跨技术栈通用
- **社区讨论热点**：对应 Issue #1385 的三闸门提案，解决"AI 输出未经验证即交付"的核心信任问题
- **状态**：OPEN（提出 6 周，较新）
- [PR #1367](https://github.com/anthropics/skills/pull/1367)

### 6. testing-patterns（#723）
- **功能**：覆盖完整测试技术栈——测试哲学（Testing Trophy）、单元测试（AAA）、React 组件测试、边界条件
- **社区讨论热点**：测试生成是社区高频需求方向，该 Skill 同时提供"测什么 vs 不测什么"的判断框架
- **状态**：OPEN（近 5 个月）
- [PR #723](https://github.com/anthropics/skills/pull/723)

### 7. skill-quality-analyzer + skill-security-analyzer（#83）
- **功能**：两个元技能——前者从结构/文档/示例/资源等五维评估 Skill 质量；后者做安全分析
- **社区讨论热点**：回应社区对 Skill 质量参差不齐和安全边界的担忧（呼应 Issue #492 的信任边界问题），属于"治理层"需求
- **状态**：OPEN（7 个月，仓库最久）
- [PR #83](https://github.com/anthropics/skills/pull/83)


## 二、社区需求趋势

从 Issues 提炼的 Top 需求方向：

| 方向 | 代表 Issue | 热度信号 |
|---|---|---|
| **Skill 分发与治理** | #492（43 评论）: 社区 Skill 冒充官方命名空间，造成信任边界滥用；#228（16 评论, 8👍）: 组织级 Skill 共享 | 社区最强烈的诉求——安全和分发体验 |
| **官方工具链修复** | #556（12 评论, 7👍）: run_eval.py 在所有查询上 0% 触发率；#202: skill-creator 写法违反自身规范 | 官方 skill-creator 质量问题引发持续讨论 |
| **插件去重** | #189（6 评论, 9👍）: document-skills 与 example-skills 内容重复，安装后产生重复 Skill | 生态治理的细分需求 |
| **Agent 治理/安全** | #412: agent-governance（策略执行、威胁检测、信任评分、审计追踪）；#1175: SPO 文档的访问控制权限逻辑 | 治理型 Skill 缺位 |
| **上下文窗口管理** | #1487: claude-api skill 单次调用注入 ~156k tokens 耗尽上下文 | 新出现的效率痛点 |
| **记忆/状态压缩** | #1329: compact-memory（符号化表示压缩 agent 状态） | 长会话场景的潜在需求 |
| **Bedrock 兼容** | #29: 如何在 AWS Bedrock 上使用 Skills | 平台扩展需求（长期未解决） |
| **MCP 暴露** | #16: 将 Skills 暴露为 MCP 协议 | 协议层整合诉求（1 年未解决） |


## 三、高潜力待合并 Skills

以下 PR 评论活跃、对应明确社区需求，预计近期落地概率较高：

1. **skill-creator Windows 修复（#1298）**——官方工具在主流平台不可用，Issue #556 有 7 个 👍、12 条评论，10+ 独立复现。**优先级最高**，但已积压 3 个月，需官方响应。

2. **document-typography（#514）**——零依赖、直击痛点（AI 文档排版质量），5 个月未合并可能因官方对文档类 Skill 有规划（已有 docx/pdf），但需求真实存在。

3. **testing-patterns（#723）**——测试是工程刚需，内容全面（哲学+实践），与现有 frontend-design（#210）形成互补。

4. **ServiceNow（#568）**——企业平台诉求明确，作者持续维护 5 个月，落地只是时间问题。

5. **ODT（#486）**——补齐格式覆盖的诉求明确，但优先级取决于官方 roadmap。


## 四、生态洞察

**社区最集中的诉求是"官方工具链的可靠性和生态治理"**——skill-creator 在 Windows 上不可用（3 个修复 PR 堆积）、社区 Skill 冒充官方命名空间造成信任风险（43 评论的最高热度 Issue）、插件内容重复——用户需要的是"可信、可复用、跨平台"的 Skills 基建，而非更多新 Skill。安全和信任问题是当前最大的关注焦点，其次是官方工具（skill-creator）的质量和跨平台兼容性。

*本报告基于公开数据自动生成，热度判断综合评论数、👍 数、讨论活跃度及问题紧迫性。*

---

# Claude Code 社区动态日报

**日期：2026-08-13** | 数据来源：github.com/anthropics/claude-code


## 今日速览

今日发布 v2.1.229 补丁版本，主要为 hook 与网关稳定性改进；社区中 Linux 桌面版需求呼声持续高涨（498 👍），而 CVP 审核状态回退和 Windows 桌面端 GPU 崩溃则是最受关注的两大 bug。此外，多智能体协调类问题在过去 24 小时仍有新讨论，稳定性与可见性仍是社区核心诉求。


## 版本发布

### v2.1.229（最新）
- **Remote Control 会话恢复**：新增 `claude remote-control --continue` 命令，用于恢复最近的 Remote Control 会话。
- **Hook 支持扩展**：为自托管 runner 会话增加服务端提供的 Claude Code hook 支持，与托管环境行为保持一致。
- **网关稳定性**：为 gateway 流式响应增加 SSE keepalive 心跳，降低长连接意外断开概率。

> 发布链接：[anthropics/claude-code Releases](https://github.com/anthropics/claude-code/releases)


## 社区热点 Issues（Top 10）

### 1. [#84352] CVP 审核通过的组织仍被 cyber safeguard 拦截 🔥 80 评论
**标签**: bug | 作者: federicolopeza | 👍 12

已获 Cyber Verification Program 批准的组织，在 Claude Code 中仍持续收到 cyber-safeguard 拦截；更令人困惑的是，验证门户将此前已批准的申请重新显示为 "Under review"。涉及合规审核状态回退问题，受影响用户已多次向官方反馈无果。

**关注原因**：企业级合规场景下的阻断性问题，且存在审核状态数据不一致，社区讨论热度极高。

> https://github.com/anthropics/claude-code/issues/84352

### 2. [#65697] 官方 Linux 桌面版（Ubuntu LTS/Debian）构建请求 🔥 498 👍
**标签**: enhancement, platform:linux, area:desktop | 作者: powell-clark | 状态: CLOSED

社区对官方 Linux 桌面版的需求依然强劲，498 个 👍 为该列表最高。当前仅有社区维护的非官方构建，功能完整性和更新时效无法保证。该 issue 近期被标记为 CLOSED，但社区仍在持续关注。

**关注原因**：Linux 桌面版需求是社区长期以来的高赞 top 诉求之一。

> https://github.com/anthropics/claude-code/issues/65697

### 3. [#54393] 多智能体协调事故复盘：单夜 12 个协调 bug 🧠 27 评论
**标签**: enhancement, area:hooks/agents/permissions | 作者: ThatDragonOverThere | 更新: 08-13

一次 autonomous overnight 运行中暴露了 12 个多智能体协调缺陷，作者以 Post-mortem 形式对每个 bug 进行了详细分类与复现路径说明，并明确指出这不是某个功能请求的附属问题，而是多智能体协调场景下的通用问题目录。

**关注原因**：对多智能体编排场景的开发者有直接参考价值，今日仍有新讨论。

> https://github.com/anthropics/claude-code/issues/54393

### 4. [#81698] Windows 桌面端 GPU 进程崩溃导致整个应用及所有会话终止 ⚠️ 25 评论
**标签**: bug, platform:windows | 作者: J-dev2 | 👍 0

Windows 11 上 Claude 桌面应用（MSIX）的 GPU 进程崩溃（exit code 101457950）会直接杀死整个应用，所有运行中的会话一并丢失。用户提供了完整的系统信息（RTX 5080 Laptop GPU，驱动 610.47）。

**关注原因**：Windows 桌面端稳定性问题，崩溃即全部会话丢失，影响严重。

> https://github.com/anthropics/claude-code/issues/81698

### 5. [#14061] `/plugin update` 不生效：插件缓存未失效 🔁 25 评论
**标签**: bug, duplicate, platform:linux | 作者: shohei-sawaguchi | 👍 31

`/plugin update` 命令虽然执行成功，但插件缓存未正确失效，新会话仍加载旧版本插件。该问题已被标记为 duplicate，但 31 个 👍 表明影响面不小。

**关注原因**：插件更新机制的基础功能缺陷，直接影响开发迭代效率。

> https://github.com/anthropics/claude-code/issues/14061

### 6. [#75899] 左箭头键误触发 agents 屏幕导航且无法重新绑定 ↩️ 14 评论
**标签**: bug, platform:macos, area:tui/keybindings | 作者: u-a-13 | 👍 19

macOS 上聊天输入框中按左箭头（空输入框 + 手动模式）会意外跳转到 agents/background-tasks 屏幕，且该快捷键不可重新绑定。返回后主会话视图也被打断。

**关注原因**：TUI 交互中键盘绑定的基础体验问题，影响日常操作流。

> https://github.com/anthropics/claude-code/issues/75899

### 7. [#85199] Windows 桌面端反复崩溃，需 "Advanced Options → Repair" 修复 ⚠️ 13 评论
**标签**: bug, platform:windows | 作者: romers352

Windows 上 Claude Desktop 反复崩溃，每次都需要通过 "Advanced Options → Repair" 修复才能恢复。用户已确认使用最新版本。

**关注原因**：Windows 桌面端稳定性问题的又一佐证，与此前 GPU 崩溃形成叠加效应。

> https://github.com/anthropics/claude-code/issues/85199

### 8. [#82326] Claude Opus 5 出现此前版本不存在的幻觉回复 🤔 9 评论
**标签**: bug | 作者: andig

用户反馈 Opus 5 重新开始"编造"回答，而 4.8 不会。环境信息标注了 Claude Code 2.1.220，但错误输出为空。

**关注原因**：模型能力回归类问题，直接影响生成质量信任度。

> https://github.com/anthropics/claude-code/issues/82326

### 9. [#71700] Kitty 键盘协议被终端名白名单限制，Alacritty 等终端被误拒 ⌨️ 7 评论
**标签**: bug, platform:linux, area:tui | 作者: severindupouy | 👍 2

Claude Code 对 Kitty 键盘协议（CSI ? u）的支持是基于终端名称白名单而非能力检测（capability detection），导致 Alacritty 等本身支持该协议的终端被错误排除。

**关注原因**：应当基于能力检测而非硬编码终端名单，属于 TUI 兼容性的合理批评。

> https://github.com/anthropics/claude-code/issues/71700

### 10. [#61268] `permissions.deny` 安全规则不生效 🔒 5 评论
**标签**: bug, platform:macos, area:security/permissions | 作者: collimarco

用户配置的 `permissions.deny` 规则未按预期工作，涉及安全边界控制的核心功能缺陷。

**关注原因**：安全相关规则失效属于高优先级问题，关系到权限模型的可信度。

> https://github.com/anthropics/claude-code/issues/61268


## 重要 PR 进展

### 1. [#85925] docs: 将剩余的过期文档链接指向 code.claude.com 📝
**作者**: AliAltivate | 状态: CLOSED

清理插件、插件技能/代理/命令及 issue 模板中的旧域名（docs.claude.com）文档链接，统一指向 code.claude.com 规范地址。与另一分支修复零文件重叠。

> https://github.com/anthropics/claude-code/pull/85925

### 2. [#85822] docs: 修复 plugins 和 examples 中的过期文档链接及 README 漂移 📝
**作者**: AliAltivate | 状态: CLOSED

纯文档清理：修复 hooks 示例 Python 文件中的文档链接（docs.anthropic.com → code.claude.com/docs/en/hooks）以及 plugins README 中的文档链接，所有变更均已对照真实重定向验证。

> https://github.com/anthropics/claude-code/pull/85822

### 3. [#57888] 将 `child_process_exec` 规则限定到 JS/TS 文件 📦
**作者**: emora-hash | 状态: CLOSED

修复 `security_reminder_hook.py` 中 `child_process_exec` 规则的误报：原先通过子串 `"exec("` 匹配 `child_process.exec()`，也会误匹配 Python 的 `asyncio.create_subprocess_exec(`。此 PR 将其限定为 JS/TS 文件。

> https://github.com/anthropics/claude-code/pull/57888

### 4. [#41611] 为 Claude Code 添加缺失的 source
**作者**: tornikeo | 状态: OPEN

为 Claude Code 添加缺失的 source 引用。PR 描述信息较少，具体变更内容需查看代码差异。该 PR 已悬置较长时间。

> https://github.com/anthropics/claude-code/pull/41611

### 5. [#42996] examples: 新增 MEP（Meat Puppet Elimination Protocol）——多机 AI 会话的异步状态中继示例 🧵
**作者**: CRMinarian | 状态: OPEN

提供一种自执行模式，解决在多台机器间切换或恢复 Claude Code 会话时的上下文丢失问题。零新增基础设施，仅三个文件。核心思想：Claude Code 无状态，每次会话从零开始，MEP 通过异步状态中继消除切换成本。

> https://github.com/anthropics/claude-code/pull/42996


## 功能需求趋势

1. **Linux 桌面版缺口显著**：`#65697` 以 498 👍 高居所有 issue 榜首，尽管被标记为 CLOSED 但社区呼声未见消退。Linux 用户对官方桌面端支持的需求是当前最集中的功能诉求。

2. **Agent 会话管理体验**：`#66202`（标记 agent 会话为完成/从视图移除，20 👍）表明用户在多 agent 并行场景下需要更精细的会话生命周期控制；`#86082` 则建议在 agent 视图中区分 "needs input" 与 "sleeping" 状态指示。

3. **跨设备/跨机器会话连续性**：`#81835`（桌面端展示 on-disk transcripts）与 `#42996`（MEP 多机状态中继）分别从官方功能和社区方案角度回应同一需求——会话状态不应被机器绑定。

4. **TUI 键盘绑定灵活性**：`#75899`（左箭头不可重绑定，19 👍）和 `#71700`（Kitty 协议应做能力检测而非白名单）共同反映用户对终端交互层可定制性和标准兼容性的要求在提升。

5. **桌面端模型选择与费用可控性**：`#68287` 和 `#69109`（Opus 4.8 1M 上下文选项消失）及 `#71481`（默认模型静默升级导致 $506 意外费用）虽然均已关闭，但反映用户对桌面端模型切换透明度和成本可见性的敏感度持续存在。


## 开发者关注点

- **Windows 桌面端稳定性是当前最突出的痛点**。`#81698`（GPU 崩溃杀全部会话）、`#85199`（反复崩溃需 Repair 修复）、`#85905`（浏览器面板崩溃 Electron GPU，MSIX 自修复失败后卸载应用）等多条独立报告指向同一结论——Windows 桌面端的崩溃率和数据丢失风险已显著影响正常使用。

- **跨会话消息可靠性出现回归**。`#86059` 和 `#86237` 分别报告了"接收中的会话被跨会话消息打断后丢失消息内容"及"跨会话消息渲染到 UI 但未进入运行时输入队列"，且后者明确指出是 2.1.222 → 2.1.227 的回归。此类问题对多会话重度用户的干扰尤为明显。

- **安全与合规机制存在可信度问题**。`#84352`（CVP 审核状态回退导致误拦截）和 `#61268`（permissions.deny 规则失效）分别触及企业合规与本地安全配置两个层面，任一问题未解决都会削弱用户对安全边界的信任。

- **插件/缓存机制的基础体验有待完善**。`#14061`（/plugin update 缓存不失效）与 `#76882`（marketplace update 不更新 installed_plugins.json）指向同一个根因——插件版本管理在持久化层面存在缺陷，且两者均已存在一段时间，修复优先级值得关注。

- **模型行为回归（幻觉）受到关注**。`#82326` 报告 Opus 5 出现此前版本不存在的幻觉内容，虽仅 9 条评论，但结合 `#83364`（xhigh/max effort 下 WebSearch 全部 HTTP 400）可见，新模型在真实工作负载下的稳定性仍存在不确定性。

---

**数据说明**：本文基于 2026-08-13 GitHub 公开数据整理，Issue/PR 状态及评论数截至数据采集时点。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-13** | 数据来源：github.com/openai/codex


## 今日速览

今日 Codex 仓库活跃度极高，核心焦点集中在 **Windows Computer Use 功能的多重故障**（权限拦截、截图失败）以及 **VS Code 扩展 IDE Context 在 Windows/WSL 环境下的稳定性问题**。后台方面，大量 PR 围绕 **插件指标采集**、**线程用量统计** 与 **gRPC 会话恢复** 展开，基础设施持续加固。此外，**线程 fork/恢复过程中的数据丢失** 成为 CLI 用户新痛点。


## 版本发布

### rust-v0.148.0-alpha.9
- **链接**: [Release 0.148.0-alpha.9](https://github.com/openai/codex/releases)
- **说明**: 今日发布了 Rust 版本 `0.148.0-alpha.9`，Release 说明中未附带详细变更日志，预计为常规 alpha 迭代。


## 社区热点 Issues

### 1. Windows Computer Use 截图失败（#25178）🔥
- **链接**: [Issue #25178](https://github.com/openai/codex/issues/25178)
- **现象**: Windows 10 22H2 上 Computer Use 可完成窗口枚举、激活、读屏与键盘输入，但任何截图请求均报 `SetIsBorderRequired failed: 不支持此接口 (0x80004002)`。
- **重要度**: 核心功能（Computer Use）在主流 Windows 版本上不可用，波及面广。25 条评论、13 👍，已持续 2.5 个月未修复，社区呼声极高。

### 2. VS Code 扩展停止自动附带 IDE 上下文（#31553）
- **链接**: [Issue #31553](https://github.com/openai/codex/issues/31553)
- **现象**: 扩展更新后（26.623.141536），在 VS Code remote/container 环境下不再自动包含 IDE 上下文。17 条评论，12 👍。
- **重要度**: 影响所有使用远程开发（Docker/SSH）的 Pro 用户，IDE 上下文是核心体验。

### 3. Codex Desktop 打开本地会话卡顿 5 秒（#37398）
- **链接**: [Issue #37398](https://github.com/openai/codex/issues/37398)
- **现象**: 打开任意未加载的本地聊天需等待约 5 秒（owner-discovery 超时），实际读取仅需 200ms。14 条评论，9 👍。
- **重要度**: 高频基础操作的性能劣化，每日被大量触达。

### 4. Windows Computer Use 沙箱提权失败（#37415）
- **链接**: [Issue #37415](https://github.com/openai/codex/issues/37415)
- **现象**: 沙箱设置因 WindowsApps ACL 权限不足而失败，报 `spawn EPERM`，导致 Computer Use 整体不可用。13 条评论。
- **重要度**: 与 #25178 同属 Computer Use 在 Windows 的系列故障，但根因不同（权限 vs API）。

### 5. IDE Context RPC 序列化错误（#34920）
- **链接**: [Issue #34920](https://github.com/openai/codex/issues/34920)
- **现象**: 扩展 26.715.x 在 Windows 上 IDE Context 报 RPC 序列化错误，已在多个版本复现（26.707/26.715），VS Code 与 Devin 均受影响。10 条评论。
- **重要度**: 与 #31553、#34696 同源问题，官方尚未给出修复方案。

### 6. VS Code IDE 上下文在 WSL2 自动禁用（#35419）
- **链接**: [Issue #35419](https://github.com/openai/codex/issues/35419)
- **现象**: 扩展 26.721.41059 在 WSL2 下自动禁用 IDE 上下文，且选中文本不被附带。6 条评论，10 👍。
- **重要度**: WSL2 用户基数庞大，Context 失效导致手动贴代码，开发效率明显下降。

### 7. Windows Computer Use 运行时被 EPERM 阻断（#37743）
- **链接**: [Issue #37743](https://github.com/openai/codex/issues/37743)
- **现象**: Windows 11（Build 26200）上 Computer Use 初始化被 `EPERM` 阻断，辅助进程随后 `EnumWindows` 失败。3 条评论。
- **重要度**: Windows 平台 Computer Use 系列问题第三例，确认非个例。

### 8. `/fork` 后父线程无法在其他终端恢复（#38144）
- **链接**: [Issue #38144](https://github.com/openai/codex/issues/38144)
- **现象**: CLI 0.147.0 中执行 `/fork` 后，父线程仍被标记为 active writer，导致无法在其他终端 resume。3 条评论。
- **重要度**: 全新问题（8/12 创建），影响多终端协作工作流。

### 9. `thread/resume` 静默丢弃最新轮次（#38169）
- **链接**: [Issue #38169](https://github.com/openai/codex/issues/38169)
- **现象**: 对高度压缩（compacted）的线程执行 resume 时，最新对话轮次被静默丢弃。2 条评论。
- **重要度**: **数据丢失风险**，压缩是长会话的常规操作，此 bug 可能导致上下文不可逆地丢失。

### 10. macOS 桌面端在 16GB 设备上崩溃循环（#37493，已关闭）
- **链接**: [Issue #37493](https://github.com/openai/codex/issues/37493)
- **现象**: 26.730+ 版本在 16GB Apple Silicon 上启动后 6-15 秒内 V8 崩溃（heap OOM），48GB 设备正常。已确认关闭。
- **重要度**: 3 条评论。**此问题在今日已关闭**，建议开发者关注具体修复版本号。


## 重要 PR 进展

### 1. 统一回合输入提交与路由（#38275）
- **链接**: [PR #38275](https://github.com/openai/codex/pull/38275)
- **内容**: 新增 `TurnInputRequest`，统一处理启动回合、转向（steer）活动回合及带原因拒绝，重构 `CodexThread` 的回合调度逻辑。属于核心架构改进。

### 2. 收集插件指标（统一 exec 命令）（#38253）
- **链接**: [PR #38253](https://github.com/openai/codex/pull/38253)
- **内容**: 为本地插件命令创建 metrics sidecar 并开放沙箱输出文件访问；命令退出时发布有效测量值，异常时清理。指标采集基建的重要一环。

### 3. 后台统一 exec 命令的插件指标跟踪（#38276）
- **链接**: [PR #38276](https://github.com/openai/codex/pull/38276)
- **内容**: 修复后台命令（yield 后仍在运行）的指标采集——即使 item 完成事件在回合结束后到达，仍持续跟踪直至命令退出。

### 4. 从远程执行器收集插件指标（#38283）
- **链接**: [PR #38283](https://github.com/openai/codex/pull/38283)
- **内容**: manifest 声明的指标操作解析改为在 executor 文件系统上执行；sidecar 使用 executor 原生临时目录并流式回传输出。三者（#38253/#38276/#38283）构成完整的插件遥测方案。

### 5. TUI 状态栏与标题显示线程用量（#38282）
- **链接**: [PR #38282](https://github.com/openai/codex/pull/38282)
- **内容**: 为 Enterprise 工作区在可配置状态栏与终端标题中新增 `thread-credits` 与 `estimated-thread-cost` 项，按需拉取共享用量估计。

### 6. `/status` 显示预估线程用量（#38281）
- **链接**: [PR #38281](https://github.com/openai/codex/pull/38281)
- **内容**: 扩展 `account/usage/read`，支持可选 `threadId` 参数与 `threadUsage` 响应（信用预估、可选 USD 成本及模型/推理/速度/Token 细分）。

### 7. 会话历史项添加创建时间戳（#38272）
- **链接**: [PR #38272](https://github.com/openai/codex/pull/38272)
- **内容**: 为本地生成的 user/developer/agent/tool-output 项在进入持久化历史时标记 Unix 创建时间（支持小数秒），并在后续请求中保留已有时间。对审计与调试有长期价值。

### 8. gRPC code-mode 会话在宿主机重启后自动重连（#38257）
- **链接**: [PR #38257](https://github.com/openai/codex/pull/38257)
- **内容**: 检测到 gRPC 宿主机停止后重新打开缓存的 code-mode 会话；串行化并发重连并协调关闭；cell ID 限定到新宿主机代次，保证回调一致性与陈旧回调清理。

### 9. 持久化世界状态改为 JSON 对象（#38274）
- **链接**: [PR #38274](https://github.com/openai/codex/pull/38274)
- **内容**: World-state 快照与合并补丁本应是分区集合，此前 `state` 字段允许任意 JSON 值，导致回放代码需处理非法形状。现收紧类型，减少状态损坏的可能性。

### 10. 集成实验性凭据代理（#29752）
- **链接**: [PR #29752](https://github.com/openai/codex/pull/29752)
- **内容**: 与 #28034 配合，使 Codex core 能选用代理提供的占位凭据并在命令生命周期内传递；修复托管子进程在切换（shell out）时丢失代理值的问题。安全相关，关注度高。


## 功能需求趋势

从近期 Issues 中可提炼出社区最关心的方向：

1. **线程用量可见性（新）**：TUI 状态栏与 `/status` 同时新增线程信用/成本展示（#38281/#38282），叠加后端 per-thread 用量查询（#38270），说明企业级成本管控需求正在上升。
2. **可配置的交互与显示**：请求增加禁用自动滚动选项（#23517，8 👍）、可配置的审批提示音（#11604）——用户对 CLI/App 的“体感控制权”要求渐增。
3. **会话生命周期管理（新热点）**：`/fork` 后父线程无法恢复（#38144）、线程 resume 静默丢数据（#38169）、含陈旧 subagent 的任务打不开（#38250）——会话操作的正确性/健壮性成为高频诉求。
4. **Computer Use 在 Windows 的可用性**：三个独立 issue（#25178/#37415/#37743）指向同一功能在不同 Windows 版本上的多重故障，社区期待一次系统性修复而非打补丁。
5. **Remote/WSL 开发场景的 Context 稳定性**：#31553/#35419/#35333/#34696 均指向 VS Code 远程开发（container/WSL/SSH）下 IDE Context 的连带失效，已是连续数周的热点。


## 开发者关注点

- **Windows Computer Use 成重灾区**：截图 API 失败（0x80004002）、沙箱 EPERM、EnumWindows 失败，三个独立故障导致核心自动化能力在 Windows 10/11 上基本不可用。部分用户反馈“Unknown / not displayed”的订阅信息，提示诊断数据本身也不完整。
- **VS Code 扩展在 Windows/远程场景失去 Context**：多版本、多环境复现（RPC 错误、workspaceRoot 缺失、静默禁用），用户被迫回滚到 26.5609.30741（#34696）。远程开发（WSL2/container）是当前 IDE 扩展最不可靠的场景。
- **数据完整性焦虑**：高度压缩线程 resume 时最新轮次被静默丢弃（#38169），因压缩是长会话的常规操作，用户担忧上下文不可逆丢失，目前无 workaround。
- **桌面端启动卡顿与崩溃**：打开本地聊天固定 5 秒延迟（#37398）属高频操作性能劣化；16GB Mac 上崩溃循环（#37493）虽已关闭，但 26.730→26.727 的“新版本反而更差”现象值得警惕。
- **后台进程生命周期问题**：App 更新后旧 app-server 守护进程残留（#32983），提醒开发者关注升级过程的进程清理与状态迁移逻辑。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-13** | 数据来源：github.com/google-gemini/gemini-cli


## 今日速览

今日社区聚焦于 **Agent 子代理的稳定性与可靠性**——多个高优 Bug（如子代理在 MAX_TURNS 后误报成功、通用代理挂起）仍在持续发酵中，维护者正在密集重测。与此同时，**安全修复成为 PR 主力**，涉及 MCP 配置损坏导致的权限失控、变量扩展绕过等关键漏洞。值得关注的是，夜间版 v0.56.0-nightly 已修复模型容量耗尽误判问题，而一个新 PR 正尝试打通"Agent 调用 Agent"的能力边界。


## 版本发布

### v0.56.0-nightly.20260812.g5024443c7（夜间版）

**核心修复：**
- **修复模型容量耗尽误报**：解决了 `core` 和 `cli` 模块中误判模型容量耗尽（capacity exhaustion）的问题，并修正了核心配额查询的模型映射逻辑（PR #28730，感谢 @DavidAPierce）
- **新增本地报告命令**：为行为评估（evals）添加了本地报告命令及开发者文档（由 @ved015 贡献）

> 说明：此版本为夜间自动构建，重点关注容量管理相关修复。


## 社区热点 Issues（Top 10）

### 1. 子代理 MAX_TURNS 后误报成功 — #22323
**标签：** P1 | agent | 需重测 | 12 条评论 | 2026-03-13 创建，持续活跃

**摘要：** `codebase_investigator` 子代理明明已达最大轮次限制（未做任何分析），却向主会话报告 `status: "success"` 和 `GOAL` 终止。这导致用户完全无法察觉分析并未完成。

**重要性：** 这是 **Agent 可信度的根本问题**——错误地报告成功会让用户对自动化结果产生危险的信赖。该 Issue 已持续活跃 5 个月且被标记 P1，说明修复难度较大或排期靠后，当前正等待重新测试。

[查看 Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. 通用代理（Generalist agent）无限挂起 — #21409
**标签：** P1 | agent | 需重测 | 8 条评论 | 8 👍 | 2026-03-06 创建

**摘要：** 当 Gemini CLI 委托任务给通用代理时，代理会无限期挂起（用户等待长达 1 小时）。即使是创建文件夹这种简单操作也会触发。用户发现指示模型不使用子代理即可绕过。

**重要性：** 这是 **Agent 模式的严重可靠性问题**，直接导致核心功能不可用。8 个 👍 表明影响面较广。当前状态标记为"需重测"，暗示已有修复尝试但尚未确认。

[查看 Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. 利用模型的 bash 亲和力：零依赖沙箱与意图路由 — #19873
**标签：** P2 | enhancement | effort/large | 8 条评论 | 2026-02-22 创建

**摘要：** 提议利用 Gemini 3 模型原生擅长 POSIX 工具链（grep、cat、sed 等）的特性，通过零依赖 OS 沙箱机制，在保证安全的同时让模型自由使用 bash 能力，并在执行后进行"意图路由"（判断命令是否符合用户意图）。

**重要性：** 这是一个**方向性的架构提案**，若落地将大幅提升 Agent 的代码探索和编辑效率，同时解决安全与自由度之间的核心矛盾。

[查看 Issue #19873](https://github.com/google-gemini/gemini-cli/issues/19873)

### 4. 组件级行为评估体系 — #24353
**标签：** P1 | eval_infra | 7 条评论 | 2026-03-31 创建

**摘要：** 这是一个 EPIC（大型追踪 Issue），旨在建立组件级评估体系。目前已有 76 个行为评估测试覆盖 6 个 Gemini 模型版本，后续需要扩展评估粒度和覆盖面。

**重要性：** 评估体系是**保障 Agent 质量的基础设施**，这个 EPIC 的推进直接关系到所有 Agent 相关功能能否被系统性验证和回归。

[查看 Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 5. AST 感知的文件读取与代码库映射评估 — #22745
**标签：** P2 | feature | 7 条评论 | 2026-03-16 创建

**摘要：** EPIC 追踪系列调研，评估 AST 感知工具的价值：① 精确读取方法边界（单次工具调用即可，减少 token 噪声）；② 智能代码库导航；③ 改进搜索准确性。

**重要性：** 若验证有效，**AST 感知将显著提升代码探索效率**，减少多轮交互和 token 消耗，对大型代码库场景尤为关键。

[查看 Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

### 6. Gemini 不主动使用自定义技能和子代理 — #21968
**标签：** P2 | bug | 6 条评论 | 2026-03-11 创建

**摘要：** 用户反馈 Gemini 几乎不会主动使用自定义 skills 和 sub-agents——即使已有 "gradle" 和 "git" 等技能的详细描述，模型仍需用户明确指示才使用。

**重要性：** **Skills/Agents 的主动发现与调用是 Agent 智能化的关键**，若模型不能自发调用工具，用户配置的自定义能力就形同虚设。

[查看 Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 7. Auto Memory 无限重试低信号会话 — #26522
**标签：** P2 | bug | 5 条评论 | 2026-05-05 创建

**摘要：** Auto Memory 仅当提取代理成功读取会话记录后才标记为"已处理"。若代理判断会话为低信号而不读取，则该会话会反复出现在候选列表中，导致无限重试。

**重要性：** 这是 **Auto Memory（自动记忆）功能的资源浪费问题**，长时间运行会积累大量无效重试，影响后台提取效率。

[查看 Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 8. Auto Memory 的确定性脱敏与日志减少 — #26525
**标签：** P2 | security | 4 条评论 | 2026-05-05 创建

**摘要：** 当前 Auto Memory 在将本地会话内容发送给模型前**没有进行确定性脱敏**，仅依赖模型提示词来脱敏（内容已进入模型上下文后才执行）。此外，日志可能包含已存在的技能（可能含敏感信息）。

**重要性：** **这是一个隐私/安全问题**——训练/提取模型会看到原始内容。该 Issue 与 #26522、#26523、#26516 同批提出，说明 Auto Memory 目前是 QA 重点。

[查看 Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 9. Shell 命令执行后卡在 "Waiting input" — #25166
**标签：** P1 | core | 4 条评论 | 3 👍 | 2026-04-11 创建

**摘要：** Gemini 执行完简单的 CLI 命令后，界面仍显示命令"活跃"并处于"等待输入"状态，即使命令早已完成。该问题**反复出现**，对自动化工作流影响严重。

**重要性：** 被标记 P1 且用户反馈"repeatedly"出现，**严重影响 CLI 的自动化可靠性和用户体验**，尤其是无人值守场景。

[查看 Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 10. 命令注入防护绕过：`$VAR` 变量展开漏洞 — PR #28691（对应 Issue #28418）
**标签：** P1 | security | 由 PR 引用

**摘要：** 修复了一个安全漏洞：`detectBashSubstitution()` 和 `detectPowerShellSubstitution()` 的检测逻辑不完整，允许 `$VAR` 和 `${VAR}` 形式的环境变量展开模式**绕过安全限制**（该限制是此前针对 GHSA-wpqr-6v78-jr5g 安全公告添加的）。

**重要性：** 这是对既有安全补丁的**绕过修复（defense-in-depth）**，关注命令注入防护的完整性。由于属于安全公告后续，建议关注合入进度。

[查看 PR #28691](https://github.com/google-gemini/gemini-cli/pull/28691)


## 重要 PR 进展（Top 10）

### 1. 修复 MCP 配置损坏时"默认放行"与数据丢失问题 — #28794
**标签：** P1 | core | 2026-08-12 更新

**摘要：** 修复 `McpServerEnablementManager` 在 `mcp-server-enablement.json` 损坏（JSON 解析失败）时的双重问题：① **防止 Fail-Open**：此前 `readConfig()` 解析失败返回 `{}`，导致所有服务器被默认启用，绕过用户禁用设置——这是权限失控漏洞；② 防止配置数据被覆盖丢失。

[查看 PR #28794](https://github.com/google-gemini/gemini-cli/pull/28794)

### 2. 损坏的 MCP enablement 配置不再被视为空配置 — #28787
**标签：** P1 | core | 2026-08-12 更新

**摘要：** 姊妹 PR——`readConfig()` 将 JSON 解析失败与"文件不存在"都返回 `{}`，导致损坏配置被静默当作"从未配置过"，所有服务器默认启用。此 PR 区分这两种情况，损坏时返回错误而非静默降级。

[查看 PR #28787](https://github.com/google-gemini/gemini-cli/pull/28787)

### 3. 容量耗尽错误：上下文感知静默重试与 TTL — #28790
**标签：** P1 | core | 2026-08-12 更新

**摘要：** 修复 #28761 报告的容量耗尽重试回归。实现**上下文感知重试策略**：
- 无人值守/非交互模式自动退避重试
- 交互模式最多 2 次静默重试（不打扰用户）
- 增加可用性 TTL，避免对暂时不可用的模型反复重试

**意义：** 直接对应本次夜间版的核心修复，大幅提升 CLI 在容量紧张时的韧性。

[查看 PR #28790](https://github.com/google-gemini/gemini-cli/pull/28790)

### 4. 修复变量展开绕过：`$VAR`/`${VAR}` 注入防护 — #28691
**标签：** P1 | security | 2026-08-12 更新

**摘要：** 修复 `detectBashSubstitution()` 和 `detectPowerShellSubstitution()` 对 `$VAR` 和 `${VAR}` 形式的漏检，补齐 GHSA-wpqr-6v78-jr5g 安全公告的绕过路径，并加固了 CI 工作流。

[查看 PR #28691](https://github.com/google-gemini/gemini-cli/pull/28691)

### 5. 允许 Agent 调用 Agent — #28738
**标签：** P2 | agent | help wanted | 2026-08-12 更新

**摘要：** 实现子代理间的**委派与递归调用**——子代理可通过 `tools:` frontmatter 委托给其他子代理或递归调用自身，修复 #22092。

**意义：** 这是 Agent 系统**走向复杂层级协作的关键一步**，目前仍标记为"help wanted"，期待社区评审与贡献。

[查看 PR #28738](https://github.com/google-gemini/gemini-cli/pull/28738)

### 6. 修复 VS Code IDE Companion 的 stop() 挂起与心跳泄漏 — #28789
**标签：** core | 2026-08-12 更新

**摘要：** 修复两个稳定性问题（#28785）：
- `IdeServer.stop()` 在有活跃 MCP 流式会话时无限挂起
- keep-alive 心跳循环中偶发失败导致资源泄漏（从未重置失败计数）

[查看 PR #28789](https://github.com/google-gemini/gemini-cli/pull/28789)

### 7. 修复 web-fetch 的 SSRF 漏洞：异步 DNS 解析 — #28557
**标签：** P1/P2 | security | 已关闭 | 2026-08-12 更新

**摘要：** 修复 SSRF 漏洞（#28555）：`isBlockedHost` 使用同步 `isPrivateIp()` 只检查字面 IP，**域名可绕过检查**。例如解析到 `169.254.169.254`（云元数据服务）的域名可穿过验证。改用异步 DNS 解析来检查真实 IP。

[查看 PR #28557](https://github.com/google-gemini/gemini-cli/pull/28557)

### 8. 行为评估：技能激活与 URL 抓取 + Windows 兼容 — #28788
**标签：** 2026-08-12 更新

**摘要：** 为 `activate_skill` 和 `web_fetch` 新增行为评估测试，改进本地评估环境的 Windows 兼容性，并修复 EDK 报告聚合器中过滤未执行用例的 Bug。

**意义：** 评估覆盖的新领域——**技能激活链路和网络抓取**——是此前较少被系统化测试的部分。

[查看 PR #28788](https://github.com/google-gemini/gemini-cli/pull/28788)

### 9. 新增 Gemini 3.6 Flash 与 3.5 Flash-Lite 模型配置 — #28673
**标签：** P2 | core | 2026-08-12 更新

**摘要：** 在 core 中新增 Gemini 3.6 Flash 和 3.5 Flash-Lite 的模型解析配置：基础定义、能力标识（thinking、multimodalToolUse）、别名及代码执行相关配置。

**关注点：** 目前仅含模型解析配置，**尚未包含各模型的性能基准**。建议后续关注模型能力对比数据。

[查看 PR #28673](https://github.com/google-gemini/gemini-cli/pull/28673)

### 10. 修复滚动位置跳动：用户上翻时强制锚定底部 — #28405
**标签：** P1 | core | 维护者专属 | 2026-08-12 更新

**摘要：** 修复 #5009——用户上翻查看内容时（如 Ctrl+S 后），新内容到达导致视图跳回底部。根本原因：`VirtualizedList.tsx` 的自动滚动效果在用户上翻后仍过度激进地重新启用"贴底"模式。

**意义：** **界面交互的经典痛点**（滚动位置跳动导致阅读中断），修复后将显著提升长会话的浏览体验。

[查看 PR #28405](https://github.com/google-gemini/gemini-cli/pull/28405)


## 功能需求趋势

根据近 24 小时活跃的 Issues 与 PRs，社区关注的功能方向主要集中在：

### 1. 安全加固（最紧迫）
- **命令注入防护**：变量展开绕过修复（PR #28691）说明安全攻防持续进行
- **SSRF 漏洞**：web-fetch 的异步 DNS 解析（PR #28557）修复了域名绕过
- **配置损坏 Fail-Open 问题**：MCP enablement 配置损坏导致权限失控（PR #28787、#28794）
- **记忆系统隐私**：Auto Memory 需确定性脱敏（Issue #26525）

### 2. Agent 系统深化
- **Agent 间协作与委派**：允许 Agent 调用 Agent（PR #28738）
- **Agent 决策可观测性**：子代理轨迹需通过 `/chat share` 可见（Issue #22598）
- **AST 感知的代码工具**：更精准的文件读取和代码库映射（Issue #22745、#22746）
- **沙箱化 bash 执行**：零依赖 OS 沙箱（Issue #19873）

### 3. Auto Memory 质量提升
- 避免无限重试低信号会话（#26522）
- 隔离无效的 memory 补丁（#26523）
- 整体质量改进跟踪（#26516）

### 4. 新模型支持
- Gemini 3.6 Flash 和 3.5 Flash-Lite 配置已进入 core（PR #28673）

### 5. 评估体系扩展
- 组件级行为评估（EPIC #24353）
- 技能激活与 URL 抓取的评估覆盖（PR #28788）


## 开发者关注点

### 高频痛点

1. **Agent 可靠性仍是最大问题**
   - 子代理误报成功（#22323）与通用代理挂起（#21409）均持续 5 个月+，被标记 P1 且需重测
   - 用户为绕过挂起问题，不得不指示模型禁用子代理

2. **Shell 交互稳定性**
   - 命令执行完成后卡在 "Waiting input"（#25166）

3. **工具/技能触发策略**
   - Gemini 不主动使用自定义 skills（#21968），用户配置的能力被浪费

4. **内存管理被质疑**
   - 自动记忆的隐私问题（#26525）和无限重试（#26522）显示该功能仍不成熟

### 值得注意的社区信号

- 安全 PR 密集合入（MCP、web-fetch、命令注入），说明该项目处在**安全加固期**
- 行为评估（evals）相关 PR 活跃（#28788、#28305、#28344），团队正系统化构建质量保障体系
- 模型容量管理的自动化（重试、TTL）是近期重点改进方向（对应夜间版 release）
- 新增模型配置（3.6 Flash / 3.5 Flash-Lite）暗示近期将发布新一代模型支持

---

*日报由 AI 自动整理生成，基于 github.com/google-gemini/gemini-cli 公开数据。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-13** | 数据来源：[github/copilot-cli](https://github.com/github/copilot-cli)


## 今日速览

今日社区动态聚焦于三类核心问题：**模型选择与覆盖逻辑的持续性混乱**（多个 issue 报告子代理模型被静默降级或覆盖）、**MCP 集成在认证与进程生命周期管理上的多重缺陷**（OAuth 刷新失败、5xx 无重试、孤儿进程），以及**长会话/服务器模式下的资源泄漏**（扩展宿主进程堆积、事件存储耗尽）。此外，平台特定的键盘映射 bug（WSL2 下 Ctrl+H）和 Windows 套接字错误亦有报告。无新版本发布，但多条 issue 在昨日被关闭（如 #4311 已在新版 1.0.79 中修复）。


## 社区热点 Issues（Top 10）

### 1. 模型可用性：企业版启用模型从目录中消失
- **#4390** `[OPEN]` — [Enabled organization models missing from catalogue (Claude Sonnet 5/Opus 5 and Kimi K3)](https://github.com/github/copilot-cli/issues/4390)
- 作者：Rogn | 评论：5 | 👍 4 | 更新：08-12
- **要点**：企业组织明确启用的模型（如 Claude Sonnet 5、Kimi K3）在 CLI 目录中不可见，且选择时报告“已禁用”。与 #4422（个人企业账户下所有 Claude 模型不可用）高度相关，暗示企业级模型授权/同步存在系统性回归。

### 2. 密钥映射回归：WSL2 下 Ctrl+H 被误判为 Ctrl+Backspace
- **#4328** `[OPEN]` — [[area:input-keyboard, area:platform-windows] Ctrl+H... misread as Ctrl+Backspace under WSL2 due to WT_SESSION leaking](https://github.com/github/copilot-cli/issues/4328)
- 作者：dimbleby | 评论：6 | 👍 0 | 更新：08-12
- **要点**：Windows Terminal 的 `WT_SESSION` 环境变量泄漏至 WSL2，导致 Ctrl+H（删除前一字符）被当作 Ctrl+W（删除前一词）。属于跨平台终端兼容性 bug，影响日常编辑效率。

### 3. ACP 扩展能力缺失：缺少 ask_user 风格交互方法
- **#2109** `[OPEN]` — [ACP: support an ask_user / ask_question style extension method](https://github.com/github/copilot-cli/issues/2109)
- 作者：TristanVII | 评论：3 | 👍 7 | 更新：08-12
- **要点**：请求为自定义 ACP 客户端增加向用户提出澄清问题的能力。现有 `session/request_permission` 覆盖范围有限，社区对结构化交互有明确需求。

### 4. 模型覆盖的“橡皮鸭”子代理存在静默覆盖缺陷
- **#4432** `[OPEN]` — [[triage] rubber-duck: model-emitted `model` argument silently overrides the complementary strategy](https://github.com/github/copilot-cli/issues/4432)
- 作者：eggboy | 评论：2 | 👍 0 | 更新：08-12
- **要点**：`rubber-duck` 子代理本应使用互补模型家族（如 Claude 会话配 GPT 审查），但 `task` 工具暴露的 `model` 参数可被模型自行填充，静默覆盖策略设定。属于子代理模型治理缺陷。

### 5. 原生 tgrep 索引器在大型 monorepo 上触发 OOM
- **#3976** `[OPEN]` — [[area:tools] native `tgrep` indexer OOM-kills the host on large monorepos](https://github.com/github/copilot-cli/issues/3976)
- 作者：reillysiemens | 评论：2 | 👍 0 | 更新：08-12
- **要点**：`tgrep` 持久化守护进程在大型仓库上无内存上限，直接 OOM 杀死宿主机。对 monorepo 用户属于阻断性问题。

### 6. 企业账户下所有 Claude 模型不可用
- **#4422** `[OPEN]` — [[area:enterprise, area:models] All Claude models disabled under CLI model selection](https://github.com/github/copilot-cli/issues/4422)
- 作者：joelpou | 评论：2 | 👍 3 | 更新：08-12
- **要点**：个人企业账户昨日还可用的 Claude 模型今日全部被拒（“This model is disabled...”），且回滚版本无效。疑似服务端策略变更，波及面广。

### 7. 任务工具静默降级子代理模型（已关闭，但需关注）
- **#3565** `[CLOSED]` — [Task tool silently downgrades subagent model to session model via multiplier guard](https://github.com/github/copilot-cli/issues/3565)
- 作者：ReefProctor | 评论：1 | 👍 1 | 更新：08-13
- **要点**：成本乘数守卫导致子代理请求的高成本模型被静默降级为会话模型，frontmatter 和显式 `model` 均被忽略。**昨日刚被关闭**（标记为已解决？），但 #4432 和 #4458/#4462（显式 model 覆盖被忽略）表明此问题可能尚未彻底修复。

### 8. BYOK：模型选择器应读取 provider 的 /models 端点
- **#4358** `[OPEN]` — [[triage] BYOK: populate the /model picker from the provider's /models endpoint](https://github.com/github/copilot-cli/issues/4358)
- 作者：0xtechdean | 评论：1 | 👍 2 | 更新：08-12
- **要点**：BYOK（自带密钥）模式下 `/models` 仅显示单个配置模型，无法浏览或切换。社区期望动态拉取 provider 的模型列表。

### 9. 远程 MCP 服务器初始化 5xx 后整场会话不可用
- **#4466** `[OPEN]` — [[triage] Remote MCP: transient 5xx on `initialize` marks server failed for whole session with no retry/backoff](https://github.com/github/copilot-cli/issues/4466)
- 作者：madhavdeshpande | 评论：0 | 👍 0 | 更新：08-12
- **要点**：远程 MCP 服务器在 `initialize` 阶段返回瞬时 502 后，CLI 将其标记为硬失败且**整场会话不再重试**。缺乏退避重试机制。

### 10. 会话拾取器：选中但未激活的行与未激活行难以区分
- **#4455** `[OPEN]` — [[triage] Session picker: selected-but-inactive row indistinguishable from other inactive rows (low contrast)](https://github.com/github/copilot-cli/issues/4455)
- 作者：Gerboa | 评论：1 | 👍 0 | 更新：08-12
- **要点**：会话侧边栏中“选中但非激活”状态与普通非激活行视觉对比度不足，影响 `resume` 操作效率。UI/UX 细节问题。


## 重要 PR 进展

> 注：过去 24 小时仅有 3 条 PR 更新，以下收录全部。

### 1. 自动化流程安全迁移
- **#4449** `[OPEN]` — [Migrate pull request automation away from pull_request_target](https://github.com/github/copilot-cli/pull/4449)
- 作者：mrecachinas | 更新：08-12
- **要点**：将 invalid-label 自动化从 `pull_request_target` 迁移走，改用 issue-scoped token 直接关闭无效 issue，并用无权限的 `pull_request` 信号处理可合并 PR。属仓库基础设施安全加固，值得关注。

### 2. 机器人误提交（已关闭）
- **#4453** `[CLOSED]` — [Julesdemangeot ship it patch 1](https://github.com/github/copilot-cli/pull/4453)
- 作者：julesdemangeot-ship-it | 更新：08-12
- **要点**：自动化 bot 提交的补丁，已关闭。无进一步信息。

### 3. 机器人回滚提交（已关闭）
- **#4452** `[CLOSED]` — [Revert 5 copilot/fix with copilot](https://github.com/github/copilot-cli/pull/4452)
- 作者：julesdemangeot-ship-it | 更新：08-12
- **要点**：自动化的回滚提交，已关闭。推测与 #4453 配套。


## 功能需求趋势

- **AI/模型治理**（高关注）：社区持续关注子代理模型覆盖/降级逻辑（#4432、#3565、#4458/#4462）、企业模型可用性（#4390、#4422）、BYOK 模型列表动态化（#4358）。
- **MCP 生态成熟度**（高频）：OAuth 刷新失败（#4464）、5xx 重试缺失（#4466）、Windows 套接字错误（#4463）、CI 中 token 403（#4346）、Docker 容器未清理（#4461）——MCP 的可靠性、生命周期和认证是当前最大痛点集群。
- **长会话/服务器模式资源管理**（新增）：`--server --stdio` 扩展宿主进程泄漏（#4468）、事件存储耗尽（#4467）、孤儿 permission 事件重放（#4469）。
- **上下文持久化**：跨多次压缩保留持久上下文（#4441），反映用户对长任务连续性的需求。
- **平台兼容性**：WSL2 键盘映射（#4328）、Windows 套接字错误（#4463）持续存在。


## 开发者关注点

1. **企业模型可用性波动是当前最紧迫问题**：#4390 与 #4422 双线报告企业/组织模型不可用或消失，且回滚 CLI 版本无效，指向服务端配置同步缺陷。受影响用户无法自主规避。
2. **子代理模型静默覆盖/降级问题反复出现**：尽管 #3565 已被关闭，但 #4432、#4458/#4462 等新报告表明“模型参数被忽略”或“策略被覆盖”的情况仍在多个场景中出现。开发者希望模型选择逻辑透明化。
3. **MCP 认证与进程生命周期是第二大痛点**：Entra OAuth 刷新失败导致频繁交互登录（#4464）、Docker MCP 容器悬挂（#4460/#4461）、远程服务器 5xx 后整场不可用（#4466）——三者都直接影响工作流连续性。
4. **服务器模式资源泄漏需尽快修复**：`--server --stdio` 下每个会话泄漏 4 个扩展宿主进程（#4468），长会话事件存储耗尽（#4467）——对桌面 App 集成方（Windows）影响明显。
5. **“模型发出 `model` 参数”暴露工具设计缺口**：#4432 指出模型可通过工具参数静默覆盖用户/策略设置，这不仅是 bug，更涉及权限边界设计——社区期待 CLI 对模型自指参数有更严格的校验。

---
*本日报基于公开 GitHub 数据自动生成，覆盖过去 24 小时的 Issue/PR 更新。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-13** | 数据来源：GitHub MoonshotAI/kimi-cli


## 今日速览

过去24小时内，Kimi Code CLI 社区活跃度有所回升，共更新 2 个 PR 和 1 个 Issue。值得关注的是，**长期悬而未决的 Memory System（持久化上下文）功能请求（Issue #1283）仍在持续发酵**，已获得 35 条评论，是社区目前最受关注的功能需求。同时，两个由外部贡献者提交的修复 PR（针对换行处理和 BrokenPipeError 异常）已在近5个月后获得活跃更新，显示维护者可能正在着手审查或合并。


## 版本发布

过去 24 小时内无新版本发布。


## 社区热点 Issues

### 1. #1283 [增强] Memory System - 跨会话持久化上下文 | ⭐ 34 评论
- **作者**: CatKang | **更新**: 2026-08-12 | [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **核心诉求**: 实现**综合性内存系统**，使 Kimi Code CLI 能够跨会话记住项目上下文、编码模式与用户偏好。包含 AI 自动管理笔记与用户手动定义指令两种模式。
- **社区反馈**: 该 Issue 自 2 月提出至今近 6 个月仍在活跃讨论，评论数达到 35 条，说明社区对此功能有强烈且持续的需求。从评论趋势来看，用户普遍希望在长周期项目中减少重复解释上下文的负担，提升 Agent 的连续性。
- **关注理由**: 这是当前社区呼声最高的功能方向，其实现与否将直接影响 Kimi Code CLI 在复杂、多会话工作流中的实用性。


## 重要 PR 进展

过去 24 小时内 2 个 PR 获得更新，均为外部贡献者提交：

### 1. #2449 fix(string): 在长度检查前剥离 `shorten_middle` 中的换行符 | [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2449)
- **作者**: Ricardo-M-L | **创建**: 2026-06-13 | **更新**: 2026-08-12
- **功能说明**: 修复 `shorten_middle` 函数在输入较短时因提前返回而**未执行 `remove_newline` 逻辑**的问题。该函数被 `extract_key_argument` 用于渲染工具调用的单行摘要，当前行为会导致多行文本未被压缩，影响输出格式。
- **价值分析**: 这是一个针对性 UI/UX 修复，虽规模不大，但能改善工具调用参数摘要的可读性，且已提交两个月，近期更新表明作者或维护者正在推进。

### 2. #2324 fix(web): 处理 SessionProcess.send_message 中的 BrokenPipeError | [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2324)
- **作者**: Ricardo-M-L | **创建**: 2026-05-19 | **更新**: 2026-08-12
- **功能说明**: 修复 `SessionProcess.send_message` 中**未防御子进程提前退出**（在 `start()` 调用与实际写入之间退出）导致的 `BrokenPipeError` 崩溃问题，涉及 `src/kimi_cli/web/runner/process.py`。
- **价值分析**: 该问题属于 Web 运行器中的竞态条件崩溃，修复将提升 CLI 在 Web 模式下的稳定性。PR 已提交近 3 个月，近期更新可能是响应维护者的审查意见。


## 功能需求趋势

通过对社区 Issue 的长期跟踪，目前 Kimi Code CLI 社区最关注的功能方向为：

### 🔥 高热度需求
1. **持久化记忆/上下文系统（Memory System）** —— 跨会话保留项目上下文、用户偏好与编码模式，是当前最高频的功能诉求。

### 📈 持续关注方向
2. **Web/远程运行稳定性** —— 与 BrokenPipeError 相关的异常处理修复表明，Web 运行模式下的稳定性是用户的实际痛点。
3. **输出格式化与可读性** —— 针对 `shorten_middle` 的换行处理修复显示，社区对工具调用摘要、终端输出的美观度有要求。

### 📊 中长期方向（基于历史 Issue 推理）
4. **更多模型接入与切换优化**（如 Claude、GPT 等模型提供商支持）
5. **IDE 集成深度优化**（VS Code、JetBrains 等）


## 开发者关注点

1. **跨会话上下文连续性不足** —— 最突出的痛点。在高强度、多会话的开发场景中，频繁重新解释项目背景降低了使用效率。
2. **Web 模式下进程生命周期稳健性** —— 子进程意外退出导致的连接中断（BrokenPipeError）会影响远端开发体验。
3. **终端输出信息的可读性** —— 工具调用的关键参数摘要未正确处理换行，导致单行渲染模式下的信息错乱。
4. **社区合入节奏** —— 两个外部 PR 均已等待数月才获得更新，开发者对于贡献的合入周期较为敏感，希望维护者能加快审阅与合并频率。

---
*本日报由 AI 技术分析师自动生成，数据截至 2026-08-13。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-13

## 今日速览

v1.18.17 发布，重点修复了会话压缩（保留完整近期对话）与自动重试机制问题。社区热度集中在 **Zen 免费额度误判与计费问题**（多个高赞 Issue），以及 **Gemini 3 Pro 函数调用失败**的长期未决缺陷。PR 方面，Mermaid 图渲染（GitGraph 与 timeline）与 Desktop WSL 适配是今日亮点；同时多个关于客户端服务生命周期管理的加固 PR 已进入审查。

## 版本发布

### v1.18.17
- **Bugfixes**
  - 会话压缩现在会保留完整的近期对话轮次，并为较小模型生成更清晰的摘要。
  - 新增 MERGE 网关推理变体支持，确保相关模型选项正常工作（@MatthewFeroz）。
  - 自动会话重试增加上限并引入随机抖动，避免无休止的重复重试。

发布链接：[v1.18.17 Release](https://github.com/anomalyco/opencode/releases/tag/v1.18.17)

---

## 社区热点 Issues（Top 10）

### 1. [BUG] Free usage exceeded 误报，即使用户有余额（#14273）
- **评论: 40 | 👍: 1 | 状态: CLOSED**
- 使用 Kimi K2.5 或 MiniMax2.5 免费模型时，即使 Zen 账户有 $3 余额，仍提示“Free usage exceeded. Add credits”。用户质疑计费判断逻辑，认为并非余额问题。
- 链接：[Issue #14273](https://github.com/anomalyco/opencode/issues/14273)

### 2. [BUG] Gemini 3 Pro 函数调用失败 - 缺少 `thoughtSignature` 支持（#4832）
- **评论: 35 | 👍: 14 | 状态: CLOSED**
- `gemini-3-pro-preview` 在工具调用时请求失败，错误提示缺少 `thoughtSignature`。高赞说明该问题影响面广，用户期待尽快修复。
- 链接：[Issue #4832](https://github.com/anomalyco/opencode/issues/4832)

### 3. [BUG] “Copied to clipboard” 提示成功但实际未复制（#41470）
- **评论: 11 | 👍: 1 | 状态: OPEN**
- 在 VSCode Server（Docker 环境）中使用时，复制操作显示成功但系统剪贴板无内容。影响远程开发场景下的基本交互。
- 链接：[Issue #41470](https://github.com/anomalyco/opencode/issues/41470)

### 4. [FEATURE] 聊天中渲染 Mermaid 图（#3366）
- **评论: 10 | 👍: 26 | 状态: CLOSED（已实现）**
- 高赞需求，希望直接在聊天 UI 中渲染 Mermaid 图表。今日有 PR 合入实现 GitGraph 和 timeline 渲染，此 Issue 已关闭。
- 链接：[Issue #3366](https://github.com/anomalyco/opencode/issues/3366)

### 5. [BUG] 付费用户仍受免费额度限制（#33495）
- **评论: 6 | 👍: 0 | 状态: OPEN**
- 拥有 $20+ Zen 余额的账户仍触发 200 次/免费额度限制，返回 429。两个独立账户均复现，付费墙与额度判定存在严重缺陷。
- 链接：[Issue #33495](https://github.com/anomalyco/opencode/issues/33495)

### 6. [BUG] DeepSeek V4 Flash 首次请求即报免费额度超限（#42128）
- **评论: 7 | 👍: 5 | 状态: CLOSED**
- 新账户首次请求即报“Free usage exceeded”，用户强调无任何历史请求记录。“免费额度”计算逻辑疑似存在误判。
- 链接：[Issue #42128](https://github.com/anomalyco/opencode/issues/42128)

### 7. [FEATURE] 终端输出中的本地文件路径应可点击（#19005）
- **评论: 7 | 👍: 5 | 状态: OPEN**
- 生成的文件路径以纯文本展示，需手动复制并 `open <path>`，影响效率。希望支持点击直接打开。
- 链接：[Issue #19005](https://github.com/anomalyco/opencode/issues/19005)

### 8. [BUG] MCP 工具已连接但未暴露给 Agent（#33027）
- **评论: 7 | 👍: 3 | 状态: OPEN**
- `pdfrag` MCP server 连接成功且 `tools/list` 返回 6 个工具，但 agent 的工具列表为空。MCP 协议层正常，Agent 侧集成存在断点。
- 链接：[Issue #33027](https://github.com/anomalyco/opencode/issues/33027)

### 9. [BUG] Azure OpenAI 大型模型（gpt-5.6-luna/sol 等）挂起（#42147）
- **评论: 3 | 👍: 0 | 状态: OPEN**
- 使用原生 Azure provider 时，小模型（gpt-5-mini）正常，但 gpt-5.6-luna、gpt-5.6-sol、gpt-5.4、o3 等大型模型在 Responses API 流式传输下无限期挂起。
- 链接：[Issue #42147](https://github.com/anomalyco/opencode/issues/42147)

### 10. [BUG] OpenCode Go 订阅已购买但仍提示额度超限（#42132）
- **评论: 4 | 👍: 0 | 状态: CLOSED**
- 用户购买 Go 订阅后，聊天仍提示“limit exceeded buy Go”；且 DeepSeek for Go 被误判为“仅中国可用”，影响主引擎使用。
- 链接：[Issue #42132](https://github.com/anomalyco/opencode/issues/42132)

---

## 重要 PR 进展（Top 10）

### 1. fix(desktop): use matching v2 CLI in WSL（#42199）
- **状态: OPEN**
- 将 Desktop WSL server 从 opencode 迁移至 opencode2，要求 WSL CLI 版本与 Desktop server 严格一致，并使用官方 V2 installer。
- 链接：[PR #42199](https://github.com/anomalyco/opencode/pull/42199)

### 2. feat(opencode): add per-session budget limit（#42202）
- **状态: OPEN**
- 新增可选的会话级预算，达到成本上限后自动停止助手；TUI 侧边栏提供查看/设置小组件，支持会话 schema 与数据库字段扩展。
- 链接：[PR #42202](https://github.com/anomalyco/opencode/pull/42202)

### 3. feat(catalog): auto-generated Open Graph cards per capture（#42201）
- **状态: CLOSED**
- 分享 catalog 链接时自动生成 1200x630 OG 卡片，展示真实渲染的终端帧，并注入 per-URL meta tags 以兼容无 JS 的爬虫。
- 链接：[PR #42201](https://github.com/anomalyco/opencode/pull/42201)

### 4. feat(tui): render Mermaid GitGraph diagrams（#42179）
- **状态: CLOSED**
- 将 Mermaid `gitGraph` 代码块渲染为终端友好的垂直提交图（如 `○`、`│`、`╲`），布局适配终端宽度。
- 链接：[PR #42179](https://github.com/anomalyco/opencode/pull/42179)

### 5. feat(tui): render Mermaid timelines（#42130）
- **状态: CLOSED**
- 将 Mermaid `timeline` 代码块渲染为终端原生垂直时间线，支持 Bare、TD、LR 三种标题方向。
- 链接：[PR #42130](https://github.com/anomalyco/opencode/pull/42130)

### 6. fix(client): require authenticated service stop（#42186）
- **状态: OPEN**
- 要求托管服务在客户端启动替代实例前，先完成身份验证并接受精确实例停止请求，避免因超时回退到基于 PID 的 SIGTERM/SIGKILL 造成风险。
- 链接：[PR #42186](https://github.com/anomalyco/opencode/pull/42186)

### 7. fix(client): prevent stale service replacement（#42185）
- **状态: OPEN**
- 防止旧版 CLI/Desktop 客户端在更新后，将新版后台服务误判为不兼容并用旧二进制替换，确保版本一致性。
- 链接：[PR #42185](https://github.com/anomalyco/opencode/pull/42185)

### 8. fix(client): validate promise service discovery（#42187）
- **状态: OPEN**
- 在 Promise client 使用健康检查与注册数据前，增加类型校验，避免 primitive、partial 或错误类型数据进入生命周期逻辑。
- 链接：[PR #42187](https://github.com/anomalyco/opencode/pull/42187)

### 9. fix(core): subagent sessions inherit ancestor deny rules（#42174）
- **状态: OPEN**
- 修复子代理会话仅检查自身 agent 规则、可绕过祖先 deny 配置的安全漏洞；deny 规则现作为围栏，ask 规则按 agent 分别生效。
- 链接：[PR #42174](https://github.com/anomalyco/opencode/pull/42174)

### 10. fix(tui): retry migration status transport errors（#42188）
- **状态: OPEN**
- 迁移状态浮层在后台服务重启导致瞬时断连时，不再直接判定失败，而是 1 秒后自动重试轮询。
- 链接：[PR #42188](https://github.com/anomalyco/opencode/pull/42188)

---

## 功能需求趋势

从近期 Issue 与 PR 中可提炼出以下社区关注方向：

1. **计费与额度判定**（高优）：Zen 免费额度误判、付费订阅与免费额度未正确联动、Go 订阅后仍限流。开发者对计费系统的一致性与透明度要求迫切。
2. **Mermaid 图表渲染**：从 #3366 的高赞到 GitGraph/timeline PR 落地，终端内原生图表渲染是长期需求，后续可能继续扩展其他图表类型。
3. **MCP 生态与安全**：MCP 工具连接但未暴露给 Agent、per-MCP-server 信任配置等，反映工具生态成熟后对细粒度权限控制的诉求。
4. **远程与容器环境适配**：VSCode Server 剪贴板失效、WSL CLI 版本一致性，远程开发体验是重要场景。
5. **大模型兼容性**：Azure 大型模型挂起、Gemini 函数调用失败、DeepSeek V4 多轮对话异常，模型商 API 差异的适配仍是持续挑战。

---

## 开发者关注点

- **免费额度判定逻辑混乱**为最大痛点，多条 Issue 指向同一现象：即使余额充足或已订阅，仍被误判为免费额度超限。这不仅影响新用户体验，也涉及付费信任问题。
- **Gemini 3 Pro 函数调用失败**自 2025 年 11 月提出，至今才关闭，跨度长且赞数高，反映模型兼容性修复节奏仍需加快。
- **会话压缩（/compact）可靠性**：v1.18.17 修复了“保留近期完整轮次”，但早前 #41801 与 #41268 均报告压缩后上下文丢失或退化，说明该功能对特定模型（如 DeepSeek V4 Flash）仍不稳定。
- **客户端服务生命周期管理**：多 PR 针对服务发现校验、停止认证、防旧版本覆盖，说明后台服务在更新/重启场景下的健壮性是当前开发重点之一。
- **CLI/Desktop 双轨并行**：WSL 与 Desktop 的版本匹配问题正在被系统化解决（#42199），社区预期 V2 迁移期间会有更多适配类修复。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-13

> 数据来源：[github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)（earendil-works/pi）

---

## 今日速览

过去24小时 Pi 仓库保持了极高活跃度：共更新 50 条 Issue 和 25 条 PR。值得关注的是，社区围绕**自动压缩（auto-compaction）失效**（#6879）的讨论持续升温，该问题已在高上下文场景下导致 API 溢出错误，成为目前评论数和👍数最高的 Issue。与此同时，**Mermaid 图表 HTML 导出**（#7956）已被合并，**鼠标事件分发机制**（#7683/#8032）有多个相关 PR 在推进，**本地 Ollama 模型代理**（#8049）与 **Grok 4.6 支持**（#8042）等新功能也已落地。整体来看，社区对扩展性（Extension API）、本地模型支持和终端体验优化表现出强烈兴趣。

---

## 社区热点 Issues（Top 10）

### 1. [#6879] auto-compaction 在上下文超限后仍不触发，直到 API 溢出
- **作者**: alexanderkreidich | 评论: 17 | 👍: 17 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/6879
- **摘要**: 在一次 gpt-5.6-sol 会话中，单次 agentic turn 运行超过 2 小时，页脚显示已越过压缩阈值并持续增长至超过 100% 上下文窗口。压缩仅在 API 在 373k tokens 处拒绝请求后才触发。作者建议在每个 agent 步骤后检查上下文使用情况。
- **重要性**: 当前热度最高的 bug。上下文管理是长会话场景的核心痛点，直接影响用户体验和 API 成本。

### 2. [#7730] Mac OS 长会话高 CPU 占用（50-110%，内存 600-800MB）
- **作者**: gterzian | 评论: 11 | 👍: 8 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/7730
- **摘要**: Mac OS 上运行 Pi 时出现高 CPU 占用，波动范围 50-110%，内存 600-800MB。初步怀疑与会话长度或上下文大小相关。
- **重要性**: 性能问题直接影响日常使用的流畅度，开发者对此反馈积极。

### 3. [#7836] Edit 模糊匹配因空白字符差异失败
- **作者**: robjgray | 评论: 9 | 👍: 1 | 状态: OPEN（inprogress）
- **链接**: https://github.com/earendil-works/pi/issues/7836
- **摘要**: `normalizeForFuzzyMatch` 未折叠连续空白或去除行首空白，导致 `oldText` 在空白不完全匹配时模糊匹配失败，影响小型模型使用 Edit 工具的场景。
- **重要性**: 影响小模型工具调用的准确率，是 agent 可靠性的关键路径问题。

### 4. [#8000] @ 文件自动补全：深嵌套匹配排在直接子项之前
- **作者**: cyzlmh | 评论: 3 | 👍: 0 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/8000
- **摘要**: 使用 `@~/<dir>/pro` 进行文件补全时，深嵌套的 basename 匹配排在了直接子项之前，用户最可能需要的直接子项反而不显示。
- **重要性**: 文件补全是日常高频操作，排序逻辑的优化对工作效率有直接帮助。

### 5. [#8041] coding-agent: HTML 导出应渲染 Mermaid 和 LaTeX 以匹配 TUI
- **作者**: aliou | 评论: 1 | 👍: 1 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/8041
- **摘要**: HTML 导出目前通过 marked 渲染 Markdown，跳过了 TUI 中的所有转换，Mermaid 图表和 LaTeX 公式以原始文本显示。希望统一渲染效果。
- **重要性**: 延续 #7956 的改进方向，文档导出是重要协作场景。

### 6. [#7835] Edit 工具拒绝单对象 `edits` 参数
- **作者**: robjgray | 评论: 4 | 👍: 0 | 状态: OPEN（inprogress）
- **链接**: https://github.com/earendil-works/pi/issues/7835
- **摘要**: 部分模型将 edit 工具参数包装为单对象 `{oldText, newText}`（或 JSON 字符串），edit 工具会直接报错。数组形式则尚可恢复。
- **重要性**: 模型参数格式兼容性问题，影响模型生态的适配。

### 7. [#7756] detectInstallMethod 错误识别非 pnpm 安装
- **作者**: songlairui | 评论: 3 | 👍: 0 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/7756
- **摘要**: 任何包含 `/pnpm/` 的路径都被判定为 pnpm 安装，导致共享 `PNPM_HOME` 的全局安装被错误标记，并产生误导性的错误信息。
- **重要性**: 影响包管理器兼容性和用户排查问题的效率。

### 8. [#7805] 设置目录根部的 .md 文件被错误加载为 skills
- **作者**: dzplus | 评论: 2 | 👍: 0 | 状态: OPEN（inprogress）
- **链接**: https://github.com/earendil-works/pi/issues/7805
- **摘要**: 通过 `settings.skills` 或 `--skill` 添加的技能目录中，根部的 README.md、AGENTS.md 等文档文件会被当作独立 skill 加载并产生验证警告。
- **重要性**: 影响 skill 目录结构的整洁性，已有一对修复 PR（#8012）在跟进。

### 9. [#8029] 大缓冲区下 Prompt 编辑器移动光标极度缓慢
- **作者**: affanali2k3 | 评论: 1 | 👍: 0 | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/issues/8029
- **摘要**: 输入框有大量文本（~7000 行）时，单次方向键操作需 1650ms，性能随缓冲区大小线性下降。
- **重要性**: 极端场景下的编辑性能问题，虽非高频但会影响特定用户群体。

### 10. [#7783] agent_end 处理器中 triggerTurn: false 仍会触发新的 turn
- **作者**: Blue-B | 评论: 3 | 👍: 0 | 状态: CLOSED
- **链接**: https://github.com/earendil-works/pi/issues/7783
- **摘要**: 从 `agent_end` 扩展处理器发送 `{triggerTurn: false}` 的自定义显示消息仍然会启动一轮新的助理回复。`isStreaming` 在 `_emitAgentSettled()` 之前一直保持 true。
- **重要性**: 已由 PR #8022 修复，但该问题暴露了扩展 API 在 turn 生命周期管理上的边界情况。

---

## 重要 PR 进展（Top 10）

### 1. [#7982] fix(coding-agent): 在流式事件中保留 usage 信息
- **作者**: christianklotz | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/7982
- **内容**: 在 JSON 和 RPC 的 `message_update` 事件中保留累计 provider usage，同时保持流大小线性。补充了文档和回归测试。关闭 #7911。
- **意义**: 修复了 0.84.0 中 delta-only 更新移除 usage 字段的回归问题，恢复了协议层的用量可观测性。

### 2. [#8042] feat(ai): 添加 Grok 4.6 支持
- **作者**: jackyshen0313 | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8042
- **内容**: 在 xAI Responses 模型集中新增 Grok 4.6，支持 `low`/`medium`/`high`/`xhigh` 推理级别。
- **意义**: 跟进最新模型发布，保持对主流模型提供方的及时支持。

### 3. [#8049] feat: 通过本地模型代理在 Pi 中使用 Ollama 模型
- **作者**: DenisRaskovalov | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8049
- **内容**: 新增两个无依赖的 Node.js 脚本（`ollama-proxy.mjs`），支持在 Ubuntu、macOS、Windows 上将本地 Ollama 模型接入 Pi。
- **意义**: 满足本地模型运行需求，为隐私敏感或离线场景提供了解方案。相应 Issue #8050 也已关闭。

### 4. [#7956] feat(coding-agent): HTML 导出中渲染 Mermaid 图表
- **作者**: aliou | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/7956
- **内容**: 复用 TUI 中工具调用的 ANSI-to-HTML 渲染逻辑，使 HTML 导出支持 Mermaid 图表的渲染（默认不渲染，可头部切换）。
- **意义**: 统一了 TUI 与 HTML 导出的 Markdown 渲染效果，见后续 Issue #8041 的进一步扩展。

### 5. [#8037] feat(tui): 通过 onMouse 将鼠标事件分发给组件
- **作者**: FradSer | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8037
- **内容**: 为全屏 TUI 实现了 `Component.onMouse` 钩子（提案见 #7683），使扩展组件可接收鼠标事件。另有同功能 PR #8032 处于 OPEN 状态。
- **意义**: 显著增强全屏 TUI 的交互能力，为扩展组件提供更多 UI 可能性。（注：与此前 #7683 关闭状态形成递进）

### 6. [#8022] fix: triggerTurn: false 不应启动新的 turn
- **作者**: cristinaponcela | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8022
- **内容**: 修复 #7783。`sendCustomMessage()` 将所有消息路由到 `agent.steer()` 的流式路径，导致 `{triggerTurn: false}` 仍消费了第二个假响应。
- **意义**: 修正了扩展 API 中 turn 生命周期管理的边界问题。

### 7. [#8012] fix: 设置目录根部的 .md 文件不应加载为 skills
- **作者**: cristinaponcela | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/pull/8012
- **内容**: 针对 #7805，使根部的非 SKILL.md 文件仅在能解析为带名称和描述的 skill frontmatter 时才作为 skill 候选。
- **意义**: 解决了技能目录中文档文件引发警告的干扰问题。

### 8. [#8052] fix(coding-agent): 使 session 持久化具备事务性
- **作者**: sitaram-iyer-glean | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8052
- **内容**: `SessionManager._appendEntry()` 在 JSONL 追加完成前就推进内存中的 session 图。持久化失败（如 ENOSPC）时，重启后会得到损坏的 session 图。
- **意义**: 提升了会话持久化的可靠性，避免磁盘写入失败导致的数据不一致。

### 9. [#8030] feat(ai): 添加 MiniMax 图生图（image-to-image）能力
- **作者**: octo-patch | 状态: CLOSED（已合并）
- **链接**: https://github.com/earendil-works/pi/pull/8030
- **内容**: 注册全局和 CN 图像生成 provider，支持图像输入模型元数据，映射图像内容和引用 URL 到 `subject_reference`，可解析 URL 和 base64 图像响应。
- **意义**: 扩展了 Pi 的多模态生成能力。

### 10. [#7970] feat(coding-agent): 全屏 transcript 滚动时显示指示箭头
- **作者**: pablasso | 状态: OPEN
- **链接**: https://github.com/earendil-works/pi/pull/7970
- **内容**: 当 transcript 不在最底部时，状态栏显示 `↓` 箭头，回到底部后清除。实现 #7908。
- **意义**: 优化长会话中的滚动体验，属于小型体验改进。

---

## 功能需求趋势

从近期 Issue 和 PR 中可以观察到的社区需求方向：

| 方向 | 具体诉求 | 代表性 Issue/PR |
|------|---------|----------------|
| **本地模型与隐私** | 通过本地代理接入 Ollama 模型，探索自托管方案 | #8049, #8050 |
| **新模型支持** | 及时跟进 Grok、MiniMax 等新模型和推理能力 | #8042, #8030 |
| **扩展性与自定义** | Extension API 能力增强：消息发布确认、显示控制、鼠标事件 | #8023, #8035, #8032/#8037, #7683 |
| **UI/UX 细节优化** | 滚动指示器、命令菜单触发方式、主题覆盖、文件补全排序、鼠标滚轮步长配置 | #7970, #8015, #7722, #8000, #7765 |
| **上下文与性能** | 自动压缩策略改进、大会话 CPU 占用、编辑器性能、流式事件保留 usage | #6879, #7730, #8029, #7982 |
| **跨平台与环境适配** | WSL 路径链接、Kitty 图像渲染、包管理器识别 | #8054, #7585, #7756 |
| **导出与文档** | HTML 导出渲染 Mermaid/LaTeX、开发文档刷新 | #8041, #7956, #8024 |

---

## 开发者关注点

1. **上下文管理可靠性**：`auto-compaction` 在极端场景下失效（#6879）引发大量共鸣，开发者希望系统能在每个 agent 步骤后主动检查上下文用量，而非被动等待 API 报错。

2. **扩展 API 的成熟度**：多个 Issue（#7783、#8023、#8035）反映了扩展开发者在 turn 生命周期、消息发布确认、消息显示控制等方面的 API 短板，表明 Extension 生态正在快速发展，需要更精细的控制原语。

3. **模型兼容细节**：#7836（Edit 模糊匹配空白差异）、#7835（单对象 edits 参数）、#8018（DeepSeek 忽略 `max_completion_tokens`）等问题表明，Pi 在适配不同模型的工具调用格式和参数方言时仍有兼容性摩擦，这是 agent 工具链在多样化模型生态中落地的关键挑战。

4. **大上下文与长会话性能**：Mac 上 100% CPU 占用（#7730）和 7000 行文本编辑延迟（#8029）说明长会话下的资源管理仍有优化空间，社区对此类调优需求反馈积极。

5. **会话持久化可靠性**：#8052 的合并表明，session 在磁盘写入失败时的数据一致性已进入核心关注范围，这与 #8048（`PI_CODING_AGENT_DIR` 覆盖未被恢复提示包含）等跨会话体验问题共同构成了对 session 机制的完善需求。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-13

## 今日速览

今日发布 5 个版本，其中桌面端连续迭代至 v0.2.1，核心修复聚焦 Web Shell 会话安全导航与项目内存作用域。社区方面，长任务自动运行失败成为反馈最激烈的痛点（#8963 获 9 条评论），同时多模态实验路线图（#8197）持续受到关注。PR 侧，Review 技能系列改进（#9020、#9027、#8994、#8996）与 Web Shell 工作区文件上传（#8874）是当前开发重点。


## 版本发布

### v0.21.11-preview.0
- **修复**：Web Shell 会话导航强制提示安全（PR #8931），防止切换会话时意外取消或重放源提示
- **日志**：服务端增加会话续接许可日志

### v0.21.10-nightly.20260812.a64d1291d2
- 包含与 preview.0 相同的 Web Shell 修复与日志改进

### desktop-v0.2.1
- **重构**：默认项目内存改为工作区作用域（PR #8856）
- **遥测**：对齐会话生命周期事件

### desktop-v0.2.0
- **修复**： Web Shell 会话历史分页稳定性（PR #8914）
- **功能**：Web Shell 会话目录共享

### dsw-eas-smoke-20260812-281542bfdc
- 非生产基础设施冒烟测试，不发布 SWE 分数


## 社区热点 Issues（Top 10）

### 1. [#8963 不能自动运行](https://github.com/QwenLM/qwen-code/issues/8963) — 9 评论
**类型**：Bug / P2 · **标签**：tools, shell
**摘要**：用户反馈无论选择 yolo 还是 auto 模式，运行 Python 脚本或长命令时都会卡住不动，无法完成需要整夜或数天的长任务。用户直言 "kimi code 完胜"，在 UI 稳定性、界面闪烁、模式准确性方面均被对比碾压。
**关注点**：长任务自动运行是核心工作流场景，此问题直接影响用户留存。社区反应激烈，建议优先处理。

### 2. [#8957 Qwen code crashes on image load since 0.21.2](https://github.com/QwenLM/qwen-code/issues/8957) — 8 评论
**类型**：Bug / P2 · **标签**：core, file-operations, regression
**摘要**：自 0.21.2 起，读取图片时 Qwen Code 立即崩溃，0.21.1 为最后一个正常版本。已标记为回归（Regression）。
**关注点**：图片读取涉及多模态能力基础路径，回归问题阻断升级路径，需尽快定位。

### 3. [#7040 RFC: Reliable auto-memory recall](https://github.com/QwenLM/qwen-code/issues/7040) — 10 评论
**类型**：Feature Request / P2 · **标签**：memory, context-performance, background-automation
**摘要**：自动记忆召回的功能设计 RFC，跟踪 3 个 PR 的交付状态：召回遥测已合并（#7393），初始回合召回与确定性快速路径正在审查（#8716），召回精度与多语言评估同属 #8716。设计在测量后有所修订。
**关注点**：记忆召回是提升多轮对话一致性的关键能力，社区讨论持续深入。

### 4. [#8678 fix(serve): Preserve the current session when a large restore times out](https://github.com/QwenLM/qwen-code/issues/8678) — 7 评论
**类型**：Bug / P1 · **标签**：session-management, latency, memory-usage, daemon
**摘要**：大型会话恢复超时时，当前会话未被保留。PR1（#8691）已实现超时契约、迟到请求安全与可观测性；后续仍有工作项。
**关注点**：P1 优先级，直接影响大项目用户的使用体验——恢复超时不应丢失当前工作上下文。

### 5. [#8562 tmux 中闪屏问题](https://github.com/QwenLM/qwen-code/issues/8562) — 7 评论
**类型**：Bug / P2 · **标签**：ui, rendering, linux
**摘要**：MacBook 通过 iTerm2 SSH 到 Ubuntu 服务器再进入 tmux，对话时屏幕闪烁（仅限 tmux 分屏）。用户用 Qwen 3.8 Max 排查后确认是 Qwen Code 版本问题。
**关注点**：远程开发（SSH + tmux）是高频使用场景，渲染问题影响交互流畅度。

### 6. [#8097 Background agent coordination gap](https://github.com/QwenLM/qwen-code/issues/8097) — 6 评论
**类型**：Bug / P2 · **标签**：multi-agent, core
**摘要**：多个后台 Explore 子代理并行运行时，存在三种协调失败：父代理重复子代理工作、过早完成、非交互式 `send_message` 通信异常。
**关注点**：多代理协调是 Agent 化开发的核心能力，重复工作和过早完成会直接浪费 token 并产生错误结果。

### 7. [#9015 Main CI failed: E2E Tests](https://github.com/QwenLM/qwen-code/issues/9015) — 4 评论
**类型**：Bug / P1 · **标签**：macos, cli, integration
**摘要**：主分支 CI 在测试结果报告前即失败（Run ID: 31609744914），由机器人自动创建跟踪 issue。
**关注点**：CI 稳定性影响所有贡献者的开发效率，P1 优先级合理。

### 8. [#9016 Vertex AI cannot authenticate with ADC](https://github.com/QwenLM/qwen-code/issues/9016) — 4 评论
**类型**：Bug / P2 · **标签**：google-auth
**摘要**：Vertex AI 无法使用 Application Default Credentials 认证——强制要求 API key，但任何 key 值都会导致 401。ADC 正确配置时仍失败。
**关注点**：GCP 用户群体的认证体验受阻，这是一个阻断性的配置问题。

### 9. [#8897 --approval-mode and --auth-type missing from --help](https://github.com/QwenLM/qwen-code/issues/8897) — 5 评论
**类型**：Bug / P2 · **标签**：cli
**摘要**：0.21.9 中 `--approval-mode` 和 `--auth-type` 两个参数已注册并生效，但未出现在 `qwen --help` 输出中，降低了 CLI 的可发现性。
**关注点**：CLI 参数文档缺失是低严重度但影响面广的问题，属于"小事但烦人"的类别。

### 10. [#9005 Anthropic wire missing stream-safety protections](https://github.com/QwenLM/qwen-code/issues/9005) — 3 评论
**类型**：Bug / P1 · **标签**：content-generation
**摘要**：Anthropic 流式传输缺少 OpenAI wire 已有的流安全保护。相关 issue 还指出 `@anthropic-ai/sdk` 被锁定在 `^0.36.1`（2025 年 1 月版本）。
**关注点**：流安全保护缺失可能导致异常流处理不当，且 SDK 版本过旧存在兼容性隐患。


## 重要 PR 进展（Top 10）

### 1. [#8982 fix(ci): reduce ENOSPC and load-sensitive test flakes](https://github.com/QwenLM/qwen-code/pull/8982)
**作者**：yiliang114 · **状态**：OPEN
**内容**：减少共享 runner 负载和 `/tmp` 压力导致的 CI 不稳定。空闲看门狗测试改为两次短子进程运行（边界值 `-1` 和 `0`），而非三次长运行。

### 2. [#8874 feat(web-shell): support workspace file uploads](https://github.com/QwenLM/qwen-code/pull/8874)
**作者**：ytahdn · **状态**：OPEN · **标签**：autofix/takeover
**内容**：Web Shell 编辑器支持直接拖放文件或通过 `@` 文件面板选择上传，多个文件顺序上传，支持进度显示、取消、自动冲突重命名和行内文件展示。

### 3. [#9001 fix(ci): cache downloaded linters on ECS runners](https://github.com/QwenLM/qwen-code/pull/9001)
**作者**：yiliang114 · **状态**：OPEN
**内容**：持久化缓存 actionlint 和 shellcheck 归档，每个 run/attempt/job 保留独立解压目录。缓存归档在信任前先复制到私有临时目录再校验。

### 4. [#8978 feat(serve): no-op on empty channel set and restore only active channels](https://github.com/QwenLM/qwen-code/pull/8978)
**作者**：rockybot2026 · **状态**：OPEN · **标签**：review/self-reported
**内容**：`qwen serve --channel all` 在通道配置为空时不再 `exit(1)`，改为优雅空操作；守护进程重启时仅恢复先前活跃的通道。对应 Issue #8975。

### 5. [#8848 feat(web-shell): redesign Channel policy and workspace management](https://github.com/QwenLM/qwen-code/pull/8848)
**作者**：qqqys · **状态**：OPEN · **标签**：review/self-reported
**内容**：Web Shell 通道管理全面开放直连消息、群组访问、会话路由和工作区所有权控制；支持选择发送者与群组策略、管理允许列表、配置工作区归属。

### 6. [#8994 feat(cli): Add review settings for attribution, default effort, and default comment](https://github.com/QwenLM/qwen-code/pull/8994)
**作者**：wenshao · **状态**：OPEN · **标签**：autofix/takeover
**内容**：为 `/review` 技能新增三个用户设置（署名、默认 effort、默认评论），仅从操作者控制的设置作用域解析（系统默认 → 用户 → 系统）；仓库级 `.qwen/settings.json` 不能设置这些项，防止仓库内容控制审查策略。

### 7. [#9020 fix(review): close the inline-quotation gap and harden the layer gate](https://github.com/QwenLM/qwen-code/pull/9020)
**作者**：wenshao · **状态**：OPEN
**内容**：#8956 合并后的跟进修复：使用权威 CommonMark 解析器替代手写栅栏扫描器，修复内联引用读取收据的差异，并加固缺陷层门禁。

### 8. [#8927 feat(channels): bound session lifetime with sessionRotation](https://github.com/QwenLM/qwen-code/pull/8927)
**作者**：qwen-code-dev-bot · **状态**：OPEN · **标签**：review/self-reported
**内容**：新增按通道 `sessionRotation` 选项，限制路由复用同一会话的时长。支持两种界限：`maxTurns`（消息轮数）和按时间范围；超出界限后下一条消息开启新会话。

### 9. [#9003 fix(sdk): support "auto" permission mode](https://github.com/QwenLM/qwen-code/pull/9003)
**作者**：shenyankm · **状态**：OPEN · **标签**：review/self-reported
**内容**：Python 和 Java SDK 的启动选项现接受 `permission_mode="auto"`，与 CLI 和 TypeScript SDK 对齐。更新了接受值列表、校验错误消息、公开模式类型及 README。

### 10. [#9022 fix(review): keep repository context within file limit](https://github.com/QwenLM/qwen-code/pull/9022) 与 [#9028 fix(review): drop the web-shell e2e related-paths](https://github.com/QwenLM/qwen-code/pull/9028)
**作者**：destire-mio / wenshao · **状态**：OPEN
**内容**：两项修复共同解决审查上下文清单超出解析文件上限的问题——前者将核心技能路径展开从整个子树收窄到顶层实现/测试与各技能 `SKILL.md`；后者删除 Web Shell e2e 中超出界限的相关路径。


## 功能需求趋势

从全部 Issues 中提炼的社区最关注功能方向：

1. **长任务/后台自动运行可靠性**（#8963、#8097、#9026）
   核心诉求：长任务能稳定跑完、后台代理不重复工作、headless 模式在模型安静结束时不误报失败。这是 Agent 类工具的基本盘。

2. **多模态能力接入**（#8957、#8197、#8110）
   Omni 多模态集成实验路线图持续跟进，图片读取崩溃的回归问题也引起广泛关注——多模态被社区视为下一步关键能力。

3. **内存/会话管理精细化**（#7040、#8678、#8979、#8922）
   自动记忆召回的时机与质量、大会话恢复超时保护、MAX_TOKENS 恢复后转录一致性、截断阈值可配置——会话状态管理正在从"能用"走向"可控"。

4. **Web Shell 产品化成熟**（#8977、#8985、#8874）
   手动会话命名保留、滚动条布局抖动、工作区文件上传——Web Shell 正快速补齐桌面级体验细节。

5. **CLI/SDK 一致性与可发现性**（#8897、#9002、#9003）
   `--help` 缺失参数、SDK 与 CLI 行为不一致（`permission_mode="auto"` 被 SDK 拒绝）、SDK 对齐 CLI 权限模式——工具链一致性是开发者体验的关键。


## 开发者关注点

**高频痛点**：
- **长任务执行失败**（#8963）是最激烈的反馈，用户明确表示切换到竞品（Kimi Code），需要高度警惕。
- **回归问题**（#8957 图片崩溃、#8923 会话导航数据突变）表明需要加强回归测试覆盖。
- **CI 不稳定性**（#9015、#8982、#9001）持续消耗贡献者时间，社区已有多个针对性 PR。

**高频需求**：
- **会话/记忆可靠性**：手动命名在 `/clear` 后保留（#8977）、会话恢复不丢上下文（#8678）、转录一致性（#8979）。
- **配置灵活性与一致性**：截断阈值可配置（#8922）、`--channel all` 空配置优雅降级（#8975）、参数帮助可发现（#8897）、SDK 与 CLI 行为对齐（#9002）。
- **多代理协调**：后台代理去重、完成状态正确性、通信可靠性（#8097）。

**值得注意的信号**：
- `review/self-reported` 标签的 PR 增多（#8978、#8848、#8927、#9003），说明社区正在主动报告自审结果，协作效率较高。
- `autofix/takeover` 标签持续出现（#8874、#8994、#8972），自动修复流程已深度融入开发工作流。
- Issue #9015 为机器人自动创建的 CI 失败跟踪，说明基础设施自动化程度较高，但同时暴露 CI 稳定性问题需更多关注。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-08-13** | 数据来源：[Hmbown/CodeWhale (原 DeepSeek-TUI)](https://github.com/Hmbown/CodeWhale)

> 注：项目已从 `deepseek-tui` 更名为 `CodeWhale`，原 `deepseek-tui` npm 包已弃用。以下内容基于 CodeWhale 仓库数据。


## 1. 今日速览

昨日社区围绕 **v0.9.5 回归问题**（Auto-Review 模式静默拦截 Bash 调用、宽终端显示异常）展开集中反馈，维护者通过 Harves 流程快速合入了 5 个社区 PR（复制消息净化、会话快照隔离、OrcaRouter 接入等）。架构层面，**EPIC-005 TUI Crate 分解** 持续推进，首个命令契约边界 PR 已以草案形式提交。新增的 **交互式插件管理器** 为 TUI 扩展生态奠定了基础。


## 2. 版本发布

### [v0.9.6](https://github.com/Hmbown/CodeWhale/releases/tag/v0.9.6)

正式发布。核心要点：

- 项目品牌统一为 **CodeWhale**，`codewhale` 命令与 npm 包统一下线；旧包 `deepseek-tui` 仅标记弃用，不再发布新版本。
- 面向 v0.8.x 的 `deepseek` / `d` 命令用户，升级路径与兼容性细节可参考发布说明。


## 3. 社区热点 Issues（10 条精选）

### 🔥 高热度 / 回归问题

- **[#5323] v0.9.5 回归：Auto-Review 模式静默拦截所有 Bash 调用和写操作**（[链接](https://github.com/Hmbown/CodeWhale/issues/5323)，3 评论，2026-08-12 创建）
  用户升级后，原应自动放行的工具调用被静默阻止。该回归直接影响自动化工作流，开发者评论确认此前 v0.8.x 行为正常。**优先级：高**，需尽快确认是否随 v0.9.6 修复或另行发版。

- **[#5322] 回归：输出区域无法填满宽终端（v0.8.65 正常）**（[链接](https://github.com/Hmbown/CodeWhale/issues/5322)，2 评论）
  v0.9 中输出区在宽屏下被强制设置最大宽度，窄屏可缩、宽屏无法扩展。TUI 核心体验回归，值得关注。

### 💬 社区讨论热点

- **[#4949] 讨论：“Constitution” 的中文翻译——“宪法”、“协作准则”还是其他？**（[链接](https://github.com/Hmbown/CodeWhale/issues/4949)，9 评论，👍 0，热度最高）
  PR #4908 将翻译改回“宪法”引发争议。社区担心中文语境的政治敏感性，正在征集母语者意见。涉及 i18n 与品牌本地化，值得跟进。

- **[#4959] [增强] 提议新增 `stop` 命令**（[链接](https://github.com/Hmbown/CodeWhale/issues/4959)，8 评论）
  在 YOLO 模式或深度自主工作流中，`+ stop` / `stop` 文本命令被忽略，模型持续执行。提议增加运行时 STOP 词拦截机制，对自动化安全至关重要。

### 📋 架构 / 管理类

- **[#5316] EPIC-005：CodeWhale TUI Crate 分解（总纲）**（[链接](https://github.com/Hmbown/CodeWhale/issues/5316)，5 评论）
  管理大型 TUI crate 拆分的总 Epic，所有相关子任务和 PR 均汇总于此。**架构演进的核心追踪项**，关注后续每一步变更。

- **[#5337] Web：完成 #4934 词典骨架，移除所有 `isZh` 分支**（[链接](https://github.com/Hmbown/CodeWhale/issues/5337)，2 评论）
  清理 i18n 路由的剩余页面，改为统一的 `{ en, zh }` 词典模式。社区成员正在逐页推进，已有对应 PR（#5338）。

### ✅ 已关闭的关键问题（前情提要）

- **[#5034] [已关闭] 切换 Provider 后残留无关的默认模型**（[链接](https://github.com/Hmbown/CodeWhale/issues/5034)，5 评论——例：切到 OpenAI 后默认模型仍为 `gpt-5.5`，Provider 与模型解析未联动。与 v0.9.6 质量相关。

- **[#5209] [已关闭] File 工具 `action=edit` 静默接受错误参数名并伪造成功**（[链接](https://github.com/Hmbown/CodeWhale/issues/5209)，4 评论——用 `new_str` 替代正确参数 `replace` 时返回假成功，导致每个位置需重编辑 3-5 次。可靠性缺陷，已修复，需关注测试覆盖。

- **[#5097] [已关闭] YouTube 称 CodeWhale 并非 DeepSeek 官方 Coding Agent**（[链接](https://github.com/Hmbown/CodeWhale/issues/5097)，5 评论——社区成员指出 YouTuber 将 Reasonix 标为 DeepSeek 官方 Agent。项目定位与官方背书问题，值得了解社区讨论脉络。

- **[#5314] [已关闭] “复制消息”包含轨道装饰符号（● ▏）**（[链接](https://github.com/Hmbown/CodeWhale/issues/5314)，2 评论——复制内容夹杂 UI 装饰字符，已通过社区 PR 修复。


## 4. 重要 PR 进展（10 条精选）

### 🚀 新功能

- **[#5327] feat(tui): 新增交互式扩展管理器**（[链接](https://github.com/Hmbown/CodeWhale/pull/5327)，已合并）
  新增本地化 `/plugin` 和 `/plugins` 命令，集中管理插件生命周期（受摘要绑定控制），保留传统可执行工具的独立审批入口。**扩展生态的重要基础**。

- **[#5333] feat(tui): 主机终端窗口支持“置顶迷你窗”模式**（[链接](https://github.com/Hmbown/CodeWhale/pull/5333)，开放中——Harvest 自社区 PR #5318（作者 SparkofSpike），实现类似画中画（PiP）功能：右键菜单或 `/pin` 命令将终端窗口缩小为 640x400 并保持置顶，再次触发恢复原尺寸。Windows 平台专属，为 v0.9.7 首个社区功能集成。

- **[#5328] FEAT-014: 命令合约 crate 边界（facets + 共享类型）**（[链接](https://github.com/Hmbown/CodeWhale/pull/5328)，草案/开放）
  属于 EPIC-005/006 的 TUI 命令分解阶段。仅定义命令迁移的原型形状，不做生产逻辑改动。架构师评审重点。

### 🐛 修复（Harvest 合并流）

- **[#5331] fix(tui): 复制消息去除视觉轨道线**（[链接](https://github.com/Hmbown/CodeWhale/pull/5331)，已合并——Harvest 社区 PR #5319（XhesicaFrost）。复制用户/助手消息时使用规范源文本，而非渲染后的 Ratatui 行；保留工具/思考等复杂单元格的完整快照路径。

- **[#5330] fix(session): 将快照读取与崩溃恢复分离**（[链接](https://github.com/Hmbown/CodeWhale/pull/5330)，已合并——Harvest 社区 PR #5320（h3c-hexin）。新增无副作用 `load_session_snapshot` 与 `recover_session_for_resume`（返回修复统计），避免工具调用进行中读取快照导致的状态冲突。

- **[#5329] fix(tui): 升级 lru 至 0.18 并取消 ratatui-core 版本固定（RUSTSEC-2026-0253）**（[链接](https://github.com/Hmbown/CodeWhale/pull/5329)，已合并——修复 `lru` 0.16.4 的 `LruCache::pop()` 悬垂指针 panic 风险的安全公告，恢复主分支 CI 绿灯。

- **[#5332] feat(config): 将 OrcaRouter 注册为命名 Provider**（[链接](https://github.com/Hmbown/CodeWhale/pull/5332)，已合并——Harvest 社区 PR #5321（XiaoHuo888-hue）。按 OpenRouter 模式接入 OrcaRouter（OpenAI 兼容网关，`sk-orca-` 前缀 Key 解锁 150+ 模型），模型选择器与文档同步更新。

### 🌐 Web / i18n / MCP

- **[#5338] feat(web): 将 Docs Guide 页面迁移至词典脊柱（#5337）**（[链接](https://github.com/Hmbown/CodeWhale/pull/5338)，开放中——移除 `isZh` 三元表达式，引入 `DocsGuideDict`（9 键）+ en/zh 词典，文案逐字搬运未混入修改。首个页面落地，后续页面按此模式逐个推进。

- **[#5336] fix(mcp): 无更多分页时省略 `nextCursor` 字段**（[链接](https://github.com/Hmbown/CodeWhale/pull/5336)，开放中——修复 MCP 返回 `"nextCursor": null` 的协议违规。严格客户端（如 Claude Code）会以 `expected string, received null` 拒绝该响应。来自社区贡献者 xiaoray-blip。

- **[#5326] web: 审计修复——i18n 对齐、文案/间距、测试修正**（[链接](https://github.com/Hmbown/CodeWhale/pull/5326)，开放中——运维方主导的网站质量打磨，三项明确修复已落地，其余页面验证无异常。


## 5. 功能需求趋势

从全部 Issues 提炼的社区关注方向：

### ① 可靠性 / 自主工作流安全（最集中，与 v0.9.5 回归相关）
- **运行时强制停止机制**（#4959）：YOLO 模式下文本 `stop` 被忽略，需系统级拦截
- **Auto-Review 模式的确定性**（#5323）：静默拦截破坏自动化预期，需更清晰的审批 / 放行语义

### ② 多 Provider 与密钥管理
- **每 Provider 独立 API Key 存储**（#5250 等）：多服务商场景下保存与切换仍待完善（如全局密钥存储方案 #5047）
- **新网关 / 模型接入**（#5332 OrcaRouter 已合入，指示对 OpenAI 兼容网关的高需求）

### ③ 会话与上下文管理
- **持久化 Agent 状态与 KV 缓存胶囊**（#2904）：长任务连续性 / 降本诉求持续存在
- **中断输出作为一等会话对象**（#5000）：被打断的半截回复需入会话文件，保障后续轮次上下文完整

### ④ TUI 体验细节
- **终端适配修复**（#5322）：宽屏布局回归
- **复制 / 粘贴净化**（#5314，已修复）：去掉 UI 装饰字符
- **窗口管理模式探索**（#5318 Pin 模式）

### ⑤ 观察：i18n 词典重构（#5337）与 Crate 分解（#5316）标记了社区对**架构规范化和多语言一致性的主动投入**。


## 6. 开发者关注点

- **回归反馈速度**：v0.9.5 的两处回归（Auto-Review 拦截、宽屏布局）均在 24 小时内被社区报告并定位，维护者已确认相关 PR，建议开发者立即验证 v0.9.6 是否包含修复。

- **“Harvest 合并流”成常态**：多起社区 PR（#5319/#5320/#5321）因基础分支漂移导致 CI 失败，由维护者以相同变更重新落地（#5331/#5330/#5332）。效率高，但社区贡献者需注意 fork 分支的同步与 CI 基线。

- **MCP 协议合规意识增强**（#5336）：严格客户端的普及开始暴露 `null` vs 缺省字段差异，服务实现需更严谨对齐规范。

- **“stop” 语义缺失**（#4959）：用户对“不可中断的自动操作”感到不安，安全护栏需求普遍存在，建议关注后续实现进展。

- **安全公告响应及时**（#5329 RUSTSEC 修复）：RUSTSEC-2026-0253 在公告发布后即被处理并合入。开发者在锁依赖版本时需权衡安全更新与兼容性测试。

---
*本日报由 AI 自动汇总生成，数据截至 2026-08-13 00:00 UTC。如有遗漏或疑问，请参考 [GitHub 仓库](https://github.com/Hmbown/CodeWhale) 原始数据。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*