# AI CLI 工具社区动态日报 2026-06-28

> 生成时间: 2026-06-28 02:07 UTC | 覆盖工具: 9 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，以下是根据您提供的各工具社区动态摘要生成的横向对比分析报告。

---

### **AI CLI 工具横向对比分析报告 (2026-06-28)**

#### **1. 生态全景**

当前 AI CLI 工具生态正处于 **“能力扩张”与“稳定性阵痛”并存** 的关键阶段。一方面，各工具正积极将 Agent 能力拓展至更复杂的工作流（如多Agent协作、后台任务）、更多样的交互界面（如编辑器集成、桌面应用）以及更深入的平台集成（如Chrome扩展、消息频道）。另一方面，这种快速扩张也导致了 **安全漏洞集中暴露、平台兼容性问题频发**（尤其是Windows）、**Agent 行为不可控**（模式混淆、挂起死循环）以及 **Token & 成本管理失控** 等普遍性痛点。社区反馈已从“功能请求”转向了 **“稳定性、安全性与成本效益”** 的核心诉求，这标志着生态正从早期探索期向成熟应用期过渡。

#### **2. 各工具活跃度对比**

| 工具名称 | Issues (热点数) | PRs (进展) | 版本发布 | 社区活跃度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 (高) | 1 | 无 | **高** |
| **OpenAI Codex** | 10 (极高) | 10+ | 3个Alpha | **非常高** |
| **Gemini CLI** | 10 (极高) | 10+ | 1个Nightly | **非常高** |
| **GitHub Copilot CLI** | 10 (高) | 3 | 无 | **高** |
| **Kimi Code CLI** | 0 | 0 | 无 | **无活动** |
| **OpenCode** | 10 (高) | 10+ | 无 | **高** |
| **Pi** | 10 (高) | 10+ | 无 | **高** |
| **Qwen Code** | 10 (高) | 10+ | 1个Nightly | **非常高** |
| **DeepSeek TUI** | 10 (极高) | 10+ | 无 | **非常高** |

**分析**：OpenAI Codex、Gemini CLI、Qwen Code、DeepSeek TUI 社区活跃度最高，拥有大量深度讨论和密集的代码提交。Claude Code、Copilot CLI、OpenCode、Pi 紧随其后，社区讨论焦点集中。Kimi Code CLI 此日无任何动态。

#### **3. 共同关注的功能方向**

多个工具社区均对以下方向表现出高度一致的诉求：

| 共同关注方向 | 涉及工具 | 具体诉求 |
| :--- | :--- | :--- |
| **Agent 行为的可控性与透明度** | **Claude Code**, **OpenAI Codex**, **Gemini CLI**, **GitHub Copilot CLI**, **OpenCode**, **DeepSeek TUI** | - 要求 Agent 在扩大操作范围、执行破坏性命令时增加用户确认机制。<br>- 解决 Plan/Agent 模式混乱、子Agent不可控、任务挂起/死循环等问题。<br>- 提供更丰富的日志、轨迹和决策过程，提升行为透明度。 |
| **成本与 Token 管理** | **Claude Code**, **OpenAI Codex**, **Gemini CLI**, **Qwen Code**, **DeepSeek TUI** | - 要求解决非预期的 Token 浪费（如繁简转换、冗余上下文）。<br>- 抱怨缓存命中率低导致成本飙升。<br>- 希望获得更精细的配额使用、重置信息及手动/自动上下文压缩功能。 |
| **跨平台兼容性与稳定性** | **Claude Code**, **OpenAI Codex**, **GitHub Copilot CLI**, **OpenCode**, **Qwen Code** | - **Windows 平台**是重灾区，普遍存在 401认证、MCP服务器启动、复制功能失效、路径处理错误等问题。<br>- 对 Linux 原生桌面应用（OpenAI Codex）和 Wayland 支持（OpenCode）有强烈需求。 |
| **安全与隐私防护** | **Claude Code**, **Gemini CLI**, **GitHub Copilot CLI**, **OpenCode**, **Pi** | - 安全策略误报（Claude Code）和敏感信息泄露（Gemini CLI）是核心痛点。<br>- 对`.codexignore`等排除机制（OpenAI Codex）、hooks 钩子失效（Copilot CLI）的担忧。<br>- 社区开始关注扩展生态的安全审查（Pi）。 |

#### **4. 差异化定位分析**

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **深度推理与模型能力集成** | 需要强大模型推理能力，偏重后端开发和安全研究的高级用户。 | 深度绑定 Anthropic 模型生态，问题焦点常在于如何更好地利用模型新特性（如Thinking Summaries）。 |
| **OpenAI Codex** | **企业级开发与多平台集成** | 注重成本控制和平台兼容性的企业团队及全栈开发者。 | 致力于打通桌面、Web、IDE等体验，高度重视计费、配额、企业安全策略（如市场策略）等企业级特性。 |
| **Gemini CLI** | **Agent 安全性与行为规范** | 对Agent安全性和行为可预测性要求极高的开发者，重视CI/CD流水线安全。 | 强调从底层防护SSRF、路径遍历等漏洞，并通过策略限制Agent的“越界”行为，追求稳健的自动化。 |
| **GitHub Copilot CLI** | **与 GitHub 生态及终端 UI 深度整合** | 重度依赖 GitHub 开发流程、偏好终端交互的开发者。 | 近期焦点在终端UI体验优化（如Alt-screen）和与VS Code Agent的协同，稳定性问题是当前主要挑战。 |
| **OpenCode** | **社区驱动的高可定制化、跨平台 Agent** | 寻求开源替代方案、喜欢深度定制、关注新技术（如加密货币、新模型）的开发者。 | 积极拥抱新模型（Minimax-M3、GLM），社区提案活跃（如支付方式），修复重点在WSL兼容性和稳定性。 |
| **Pi** | **以“扩展生态”为核心的通用 Agent 平台** | 希望构建自定义Agent工作流、或进行AI应用开发的“开发者中的开发者”。 | 强调插件系统的可扩展性、自定义prompt和渲染器，为高级用户提供高度自由的构建环境。 |
| **Qwen Code** | **团队协作与浏览器自动化** | 关注多人协作、任务调度、及将Agent能力扩展到浏览器场景的团队。 | 从单人工具向协作平台演进（频道Agent），后台任务持久化，并计划重振Chrome扩展。 |
| **DeepSeek TUI** | **极致成本优化与编辑器原生集成** | 对API调用成本极其敏感、或主要使用Zed等现代编辑器的开发者。 | 将**Token/缓存优化**作为首要任务，并积极适配 `agentclientprotocol` 等开放标准，以实现与编辑器的深层融合。 |

#### **5. 社区热度与成熟度**

*   **高成熟度且持续高热度**: **OpenAI Codex** 和 **Gemini CLI** 社区不仅讨论热烈，而且 PR 密集、版本发布频繁，表明项目已进入 **快速迭代的成熟期**，开发者对其有明确预期和稳定参与。
*   **快速迭代期 (B轮工具)**: **Qwen Code** 和 **DeepSeek TUI** 社区异常活跃，且讨论集中度很高，围绕一两个核心痛点（成本、缓存、Agent任务）展开，说明它们正处于 **主攻核心性能指标、打造差异化优势的高速发展期**。
*   **功能拓展期但稳定性承压**: **Claude Code** 和 **GitHub Copilot CLI** 社区热度很高，但Bug报告数量大、影响广（如Windows兼容性、回归问题），表明它们在积极拓展新功能的同时，**基础稳定性和平台兼容性** 正在成为主要挑战，可能处于从“先锋”到“主流”的阵痛期。
*   **生态构建期**: **OpenCode** 和 **Pi** 社区活跃，关注点从单一工具功能转向**生态建设**（扩展API、插件系统、支付方式等），表现出平台型工具的发展潜力。

#### **6. 值得关注的趋势信号**

1.  **“安全性”成为压倒一切的入场券**: 从SSRF、路径遍历到Agent越权、恶意扩展包，安全漏洞的暴露已不再是孤立事件，而是行业系统性风险。**任何想进入企业级市场的AI CLI工具，都必须将安全性提升到最高优先级。**
2.  **“Token 成本”是用户体验的生死线**: 当AI模型能力不再是唯一瓶颈时，**有效的成本控制**（智能缓存、上下文管理、透明的计费）将直接决定工具的生命力。开发者对“省钱”的重视程度已超过对“新功能”的渴望。
3.  **Agent 自动化需要“监管”与“护栏”**: 社区不再满足于“全自动”，而是强烈要求Agent在关键操作（修改代码、运行命令、扩大任务范围）前**征求许可、提供解释、允许回滚**。**“可控的自主性”** 将是未来Agent设计的核心原则。
4.  **Windows 平台兼容性已成为“最大短板的桶”**: 众多工具的Windows Bug集中爆发，说明目前流行AI CLI工具的开发范式更偏向Unix生态。**谁能率先解决好Windows的体验问题，谁就将赢得巨大的增量市场。**
5.  **从“单打独斗”到“生态协作”**: 无论是DeepSeek TUI适配公开协议、Qwen Code尝试频道Agent，还是OpenCode和Pi构建插件体系，都表明工具间、工具与环境间的**互联互通和可扩展性**正成为新的价值增长点。单机版、封闭式的AI助手将越来越难以满足复杂开发场景。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为专注于 Claude Code 生态的技术分析师，以下是基于您提供的 `anthropics/skills` 仓库数据（截止 2026-06-28）的社区热点报告。

---

### Claude Code Skills 社区热点报告 (2026-06-28)

#### 1. 热门 Skills 排行

以下按社区关注度（PR 评论数，为排序依据）列出最受关注的 5 个 Skills 提案。

1.  **fix(skill-creator): 修复 `run_eval.py` 零召回率及 Windows 兼容性问题** (PR #1298)
    *   **功能**: 这是一个关键的 **修复型 PR**，针对 `skill-creator` 的评估脚本 (`run_eval.py`)。该修复旨在解决脚本在评估技能描述时，始终报告 `recall=0%` 的致命缺陷，并同时修复 Windows 系统下的流读取、触发检测及并行工作进程问题。
    *   **社区讨论热点**: 该 PR 直接回应了社区广泛报告的核心 Bug（关联 Issue #556，#1169等），讨论集中在如何彻底解决 `skill-creator` 优化循环失效的问题。这被认为是当前 `skills` 生态中最严重的阻碍性问题之一。**状态**: OPEN。

2.  **Add document-typography skill: 文档排版质量控制** (PR #514)
    *   **功能**: 新增一个专注于 **文档排版** 的技能。它能自动纠正 AI 生成文档中的常见排版问题，如孤字（orphan）、孤行（widow）和编号错位。
    *   **社区讨论热点**: 社区普遍认可这是一个高价值、贴近实际需求的 Skill，因为它解决了日常使用中一个普遍但令人烦恼的细节问题。讨论主要集中在触发条件的精确性和与其他文档处理技能（如 DOCX, PDF）的协作方式。**状态**: OPEN。

3.  **Add SAP-RPT-1-OSS predictor skill: SAP 业务数据预测** (PR #181)
    *   **功能**: 引入基于 SAP 开源表格基础模型 **SAP-RPT-1-OSS** 的业务预测能力。该技能使 Claude 能够针对 SAP 的业务数据进行预测分析。
    *   **社区讨论热点**: 这是一个专业领域极强的技能，社区讨论集中于其对企业用户的价值，以及对复杂数据模型的集成难度。这表明社区对深入垂直行业（特别是企业级应用）的 Skill 有强烈需求。**状态**: OPEN。

4.  **Add skill-quality-analyzer and skill-security-analyzer: 元技能（分析工具）** (PR #83)
    *   **功能**: 提出了两个“元技能”：**技能质量分析器** 和 **技能安全分析器**。它们旨在评估其他 Skills 本身的质量（结构、文档）和安全性（潜在的权限滥用风险）。
    *   **社区讨论热点**: 这个 PR 反映了社区对 Skill 生态的自省和治理需求。讨论重点在于如何制定客观的质量标准和安全基线，以及如何将这些分析器集成到 Skills 的提交流程中，以替代人工审核。**状态**: OPEN。

5.  **Add testing-patterns skill: 全面测试指南** (PR #723)
    *   **功能**: 提供一个覆盖全栈测试的综合性技能，包括测试哲学（Trophy模型）、单元测试（AAA模式）、React组件测试、端到端测试等。
    *   **社区讨论热点**: 社区开发者对此类“最佳实践”Skill 非常欢迎，认为它能显著提高代码质量。讨论主要围绕其内容的覆盖面、与现有测试框架的兼容性，以及是否应包含 CI/CD 相关指导。**状态**: OPEN。

#### 2. 社区需求趋势

从 Issues 中可以提炼出以下最强烈的社区需求方向：

1.  **解决 Skill-Creator 的可靠性问题**: **最核心的诉求**。大量 Issue（如 #556, #202, #1061）抱怨 `skill-creator` 的评估优化流程完全失效（`recall=0%`）或存在严重的 Windows 兼容性问题。社区的核心关切不是创造新技能，而是希望官方修复这个“技能制造机”本身，使其能正常工作。
2.  **安全与信任机制**: **最高风险的需求**。Issue #492 社区成员 **aliksir** 发现了潜在的信任边界漏洞：社区构建的技能被存放在 `anthropic/` 的命名空间下，可能导致用户误以为是官方发布的技能，并授予其高权限。社区迫切需要清晰的命名策略和技能安全验证机制（可视作对 PR #83 的呼应）。
3.  **组织级技能共享与发现**: **最广泛的功能需求**。Issue #228 提出了在企业/团队范围内共享 Skills 的需求。当前通过手动下载和分享 `.skill` 文件的方式过于繁琐，社区期待一个像应用商店一样的内置技能库，支持一键安装和组织内分享。
4.  **特定领域深化**: 除了通用的开发辅助，社区也在探索 Skills 在特定垂直领域的应用，例如：
    *   **企业级应用**: SAP 数据预测 (PR #181) 和 SharePoint 文档处理 (Issue #1175)。
    *   **文档处理**: 排版优化 (PR #514) 和跨格式支持（ODT - PR #486）。
    *   **代理治理**: 提出了“代理治理”技能 (Issue #412)，旨在为AI代理系统提供安全模式、策略执行和审计追踪功能。

#### 3. 高潜力待合并 Skills

以下 PR 评论活跃且尚未合并，是近期最有可能落地的 Skills，因为它们解决了社区的迫切需求。

1.  **PR #1298 - 修复 `run_eval.py`**: **优先级最高**。它直接解决了 `skill-creator` 生态的根基问题。一旦该 PR 被合并，后续对 `skill-creator` 的改进才有意义。
2.  **PR #83 - 技能质量与安全分析器**: **最具前瞻性**。它不仅回应了社区对安全（Issue #492）的担忧，也为 Skills 生态的长期健康发展建立了一套准入标准。
3.  **PR #514 - 文档排版技能**: **用户呼声最高**。它解决了一个普遍且微小的痛点，容易获得用户好感，实现和维护成本相对较低，是完美的增量改进。
4.  **PR #539 / #361 - 修复 YAML 特殊字符解析问题**: **修正性 PR**。它们修复了 `skill-creator` 在解析包含特殊字符的描述（如冒号、括号）时的静默失败问题。这两个 PR 内容相似（后者更新），修复了一个直接导致技能创建失败的常见错误。

#### 4. Skills 生态洞察

**一句话总结**: 当前社区在 Skills 层面最集中的诉求是 **“让基础工具可靠，让生态规则透明”**—— 社区的首要关注点已从创造新的、花哨的功能（Skills），转变为迫切要求官方修复 `skill-creator` 的可靠性问题、建立清晰的安全与信任边界，以确保整个生态系统的可持续发展。

---

好的，这是根据您提供的 GitHub 数据分析生成的 2026-06-28 Claude Code 社区动态日报。

---

## **Claude Code 社区动态日报 | 2026-06-28**

### **今日速览**

今日社区焦点集中在 **Opus 4.7 模型的思考摘要（Thinking Summaries）在非交互式界面（VS Code 扩展、SDK）中失效** 的老问题上，相关 Issue 持续获得高热度讨论。同时，多个新的 **安全策略误报** 和 **平台兼容性**（特别是 Windows）相关问题开始涌现，反映出社区在规模化使用 Claude Code 时遇到的新挑战。

---

### **社区热点 Issues**

1.  **[#49322] [BUG] Opus 4.7 thinking summaries not rendered in VS Code extension**
    - **热度**: 47条评论，41个 👍
    - **分析**: 这是目前社区最关注的问题。Opus 4.7 更改了思考块的 `display` 参数，但 VS Code 扩展的 UI 解析器未能适配，导致用户即使开启了 `showThinkingSummaries` 也无法看到思考摘要。这影响了核心的用户体验，特别是在需要审查模型推理过程的场景下。
    - **链接**: [Issue #49322](https://github.com/anthropics/claude-code/issues/49322)

2.  **[#49268] Thinking summaries missing on Opus 4.7 — harness doesn't set display: "summarized"**
    - **热度**: 46条评论，75个 👍
    - **分析**: 这是上一个问题 (#49322) 的更底层原因分析。用户发现问题的根源在于 Claude Code 的调用管道（harness）在处理 Opus 4.7 的 API 响应时，没有正确设置请求参数 `display: "summarized"`。这被视为一个核心的架构性 BUG，而非简单的 UI 渲染问题。
    - **链接**: [Issue #49268](https://github.com/anthropics/claude-code/issues/49268)

3.  **[#69706] [BUG] API Error: 401 Invalid authentication credentials**
    - **热度**: 21条评论，10个 👍
    - **分析**: 多个 Windows 用户报告了 401 认证错误。这可能与 Windows 环境下凭证存储或读取的机制有关，是一个影响面较广的平台兼容性问题。
    - **链接**: [Issue #69706](https://github.com/anthropics/claude-code/issues/69706)

4.  **[#59844] `showThinkingSummaries: true` silently no-ops on Opus 4.7 in non-interactive surfaces**
    - **热度**: 10条评论，6个 👍
    - **分析**: 此 Issue 扩展了 #49322 的讨论范围，指出该问题不仅影响 VS Code 扩展，还影响所有非交互式调用方式（如 SDK 或 `claude --print`）。这使得该问题的影响面进一步扩大。
    - **链接**: [Issue #59844](https://github.com/anthropics/claude-code/issues/59844)

5.  **[#65114] [FEATURE] Cowork: give users a manual /compact**
    - **热度**: 5条评论，1个 👍
    - **分析**: 用户希望在 Cowork 模式下获得手动触发上下文压缩（Compaction）的能力，而不是完全依赖自动压缩。这反映了用户对会话控制权的需求。
    - **链接**: [Issue #65114](https://github.com/anthropics/claude-code/issues/65114)

6.  **[#67220] [FEATURE] Native Windows toast notifications**
    - **热度**: 3条评论
    - **分析**: 用户请求为 Windows 平台增加原生 Toast 通知，使其能像 macOS/Linux 一样，在任务完成或需要用户输入时获得 OS 级别的通知。这表明社区对跨平台体验一致性的追求。
    - **链接**: [Issue #67220](https://github.com/anthropics/claude-code/issues/67220)

7.  **[#71910 & 关联系列] [Bug][cyber] 系列安全策略误报**
    - **热度**: 多个类似 Issue，单个评论数较少但总量大，主题一致。
    - **分析**: 用户 `sworrl` 提交了一系列关于无人机固件分析和地面站开发的 Issue，均被安全策略（Safety filter）阻断。这集中反映了当前安全策略在识别合法安全研究和开发者工作流时存在严重的误判问题，可能导致正常开发工作被中断。
    - **链接**: [Issue #71910](https://github.com/anthropics/claude-code/issues/71910)，[#71920](https://github.com/anthropics/claude-code/issues/71920)，[#71912](https://github.com/anthropics/claude-code/issues/71912) 等

8.  **[#71803] [FEATURE] Let the agent trigger /compact itself**
    - **热度**: 1条评论，1个 👍
    - **分析**: 与 #65114 类似，用户希望 Agent 本身能自主决定并触发 `/compact` 操作。这代表了用户对 Agent 自主管理上下文和会话能力提升的期望。
    - **链接**: [Issue #71803](https://github.com/anthropics/claude-code/issues/71803)

9.  **[#61147] [BUG] (Windows Cowork mode 相关问题)**
    - **热度**: 2条评论，2个 👍
    - **分析**: 标题未完整展示，但标签 `platform:windows` 和 `area:cowork` 表明这是一个 Windows 平台上 Cowork 模式的 BUG。考虑到 Windows 用户基数，此类问题值得关注。
    - **链接**: [Issue #61147](https://github.com/anthropics/claude-code/issues/61147)

10. **[#71941] Inconsistent feature parity and feedback channels across Claude surfaces**
    - **热度**: 1条评论
    - **分析**: 用户提出了一个宏观问题，即 Claude Code、Cowork 和 claude.ai 三个平台在功能和反馈机制上存在不一致性，影响了用户在不同场景下的流畅体验。这个 Issue 反映了用户对统一产品体验的长期期待。
    - **链接**: [Issue #71941](https://github.com/anthropics/claude-code/issues/71941)

---

### **重要 PR 进展**

过去24小时内，仓库中活跃的 PR 较少，大多为小型修复和清理工作。

1.  **[#68787] fix(scripts): add error message to edit-issue-labels.sh when called with no label arguments**
    - **状态**: 打开
    - **分析**: 这是一个对仓库维护脚本的小改进。修复了当脚本未收到任何标签参数时，静默退出且无任何错误提示的问题，增强了脚本的健壮性和用户友好性。
    - **链接**: [PR #68787](https://github.com/anthropics/claude-code/pull/68787)

---
*(注：其余 PR 为关闭状态或内容为空，不具备分析价值。)*

### **功能需求趋势**

1.  **会话控制与上下文管理**：
    - **手动/智能压缩**: 社区强烈要求能够在 Cowork 模式下手动触发 `/compact`，甚至让 Agent 自主管理压缩，以更好地控制会话成本和上下文质量。
    - **跨会话学习**: 有用户 (#71937) 提出希望 Claude 能自发地识别并记录自己的学习经验，而不仅仅依赖用户纠正，这代表了社区对 Agent 持续学习和改善能力的更高期待。

2.  **跨平台体验统一与增强**：
    - **Windows 深度集成**: 对 `preferredNotifChannel` 支持原生 Windows Toast 通知的请求 (#67220) 表明，Windows 用户希望获得与 macOS/Linux 同等级别的生态集成体验。

3.  **安全策略的智能化**：
    - **减少误报**: 多个关于安全策略误报的 Issue (如 #71910 系列) 表明，社区迫切需要更精准的安全策略，能够区分合法的开发工作和真正的恶意行为，避免阻碍正常的开发流程。

### **开发者关注点**

1.  **Opus 4.7 兼容性阵痛**：关于 Opus 4.7 思考摘要的问题成为了社区焦点，引发了大量讨论和点赞。这表明开发者对新模型部署后的兼容性非常敏感，任何 API 行为变化都可能导致下游工具链断裂，严重影响工作效率。
2.  **Windows 平台稳定性**：401 认证错误 (#69706) 和 Cowork 模式 BUG (#61147) 的出现，再次凸显了 Windows 平台在 Claude Code 生态中的稳定性仍有提升空间。Windows 开发者是重要的用户群体，他们在平台适配上的痛点需要得到及时响应。
3.  **软性限制与硬性阻断**：社区中有两种不同类型的“限制”反馈：一种是对功能缺失或体验不佳的改进请求（如手动压缩、原生通知），另一种是直接阻断开发流程的 BUG（如认证失败、安全误报）。后者（硬性阻断）往往能获得更高的关注度和更紧急的修复需求。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 2026-06-28 OpenAI Codex 社区动态日报。

---

## OpenAI Codex 社区动态日报 | 2026-06-28

### 今日速览

社区今日热议焦点集中在 **速率限制成本飙升** 与 **SSD 寿命损耗** 两大性能与费用问题。同时，OpenAI 团队正积极通过 **PR #30395** 解决用户关心的配额重置和过期信息不透明问题。此外，社区对 **Linux 桌面客户端** 的呼声持续高涨，已成为最受关注的增强请求。

### 版本发布

过去24小时内发布了三个 Rust 版本的 Alpha 小更新，未附带详细说明。
- **rust-v0.143.0-alpha.29** ([链接](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.29))
- **rust-v0.143.0-alpha.28** ([链接](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.28))
- **rust-v0.143.0-alpha.27** ([链接](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.27))

### 社区热点 Issues

1.  **#28879 速率限制成本飙升 10-20倍** ([链接](https://github.com/openai/codex/issues/28879)) | **评论: 186, 👍: 334**
    - **重要性:** 影响巨大。大量 Plus 用户在 `gpt-5.5` 模型上遭遇预算被快速消耗的问题，5小时预算在2-3个Prompt内耗尽。这是目前社区最关注、争议最大的性能/计费回归问题。
    - **社区反应:** 大量用户分享日志佐证，请求紧急修复，情绪激动。

2.  **#11023 请求推出 Linux 桌面应用** ([链接](https://github.com/openai/codex/issues/11023)) | **评论: 130, 👍: 650**
    - **重要性:** 社区呼声最高的功能请求，获得了最多的👍。部分 Mac 用户因性能问题转投 Linux，但对桌面应用的缺失感到困扰。
    - **社区反应:** 长期存在的需求，用户持续表达对 Linux 原生支持的热切期盼。

3.  **#28224 SQLite 日志一年可写 640TB** ([链接](https://github.com/openai/codex/issues/28224)) | **评论: 93, 👍: 399**
    - **重要性:** 一个被低估但极其严重的性能与硬件损耗问题。虽然问题作者指出相关 PR 已合并并封存了此 Issue，但其揭示的严重性仍值得开发者警惕。
    - **社区反应:** 用户对反馈日志量巨大感到震惊，并呼吁更多用户检查自己的日志情况。

4.  **#2847 请求添加敏感文件排除机制** ([链接](https://github.com/openai/codex/issues/2847)) | **评论: 79, 👍: 414**
    - **重要性:** 核心的功能缺失。用户迫切需要一种机制（如 `.codexignore` 文件）来防止 Token 泄露或被发送到模型，涉及企业安全和隐私问题。
    - **社区反应:** 企业用户和关注安全的开发者强烈支持，认为这是生产环境部署的必要前提。

5.  **#9203 请求恢复 "/undo" 命令** ([链接](https://github.com/openai/codex/issues/9203)) | **评论: 50, 👍: 300**
    - **重要性:** 影响了工作流的可靠性。`/undo` 命令被移除后，用户因 Codex 误操作（如删除未跟踪文件、在未提交时修改代码）而遭受了损失。
    - **社区反应:** 用户怀念旧功能，认为恢复该功能是防止意外破坏的关键。

6.  **#30224 自定义模型与 `X-OpenAI-Internal-Codex-Responses-Lite` 冲突** ([链接](https://github.com/openai/codex/issues/30224)) | **评论: 52, 👍: 18**
    - **重要性:** 尽管👍不多，但评论数显示这是一个广泛出现的新问题，影响自定义模型兼容性。
    - **社区反应:** 用户报告在使用高级 API 功能时遇到模型不支持的明确错误。

7.  **#29955 配额瞬间消耗：1条消息用尽100积分** ([链接](https://github.com/openai/codex/issues/29955)) | **评论: 29**
    - **重要性:** 与 #28879 性质相似，但出现在 Pro 5x 用户群体中，积分瞬间归零。这表明速率限制问题可能在不同付费层级上都有体现。
    - **社区反应:** 用户表达了极大不满，认为这是一个严重的计费 bug。

8.  **#29072 Windows 沙箱环境集成失败** ([链接](https://github.com/openai/codex/issues/29072)) | **评论: 22, 👍: 19**
    - **重要性:** 核心功能阻碍。Windows 用户无法使用 `apply_patch` 等关键功能，导致沙箱集成完全不可用。
    - **社区反应:** Windows 用户反馈错误信息，确认是持续存在的平台兼容性问题。

9.  **#30390 Windows桌面应用后台消耗大量 Token** ([链接](https://github.com/openai/codex/issues/30390)) | **评论: 3**
    - **重要性:** 最新发现。Windows 桌面版在后台静默消耗约 70k Token（用于`ambient_suggestions`功能），这可能是导致预算快速消耗的另一个原因。
    - **社区反应:** 用户对后台行为感到不满，认为是隐形的成本损耗。

10. **#24389 主Agent挂起数小时** ([链接](https://github.com/openai/codex/issues/24389)) | **评论: 14**
    - **重要性:** 稳定性问题。当子Agent无响应时，`close_agent` 操作可能导致父Agent长时间挂起（超过8小时），严重影响工作流程。
    - **社区反应:** 用户描述了详细的挂起场景，揭示了多Agent协作中的僵死风险。

### 重要 PR 进展

1.  **#30395 显示配额重置到期详情** ([链接](https://github.com/openai/codex/pull/30395)) | **新 PR**
    - **内容:** 针对社区对配额过期信息不透明的反馈，后端将返回重置积分的到期日期，帮助用户更好地规划使用。
    - **重要性:** 解决了计费和配额管理的关键痛点，提升透明度。

2.  **#30334 添加工具和推理耗时日志** ([链接](https://github.com/openai/codex/pull/30334)) | **新 PR**
    - **内容:** 改进遥测系统，提供更细粒度的工具延迟日志，区分调度/排队时间与执行时间。
    - **重要性:** 有助于开发者诊断性能瓶颈。

3.  **#304 系列 PR：统一序列化 MCP OAuth 凭证操作** (由 #30292-#30296 组成) ([链接](https://github.com/openai/codex/pull/30292) 等)
    - **内容:** 大规模重构 `rmcp-client` 模块，对 MCP OAuth 的 `login`、`logout`、`refresh` 等操作进行序列化，并引入凭证存储漂移检测。
    - **重要性:** 修复了高并发下 OAuth 凭证状态不一致、Token 过期等导致的认证失败问题。这是对 #27165 等认证问题的根本性修复。

4.  **#30269 禁用 Rendezvous WebSocket 的 Nagle 算法** ([链接](https://github.com/openai/codex/pull/30269))
    - **内容:** 为 exec-server 的 WebSocket 连接禁用 Nagle 算法，以减少网络延迟。
    - **重要性:** 提升实时交互性能，尤其对需要低延迟反馈的编码任务有利。

5.  **#30291 暴露环境信息 RPC** ([链接](https://github.com/openai/codex/pull/30291))
    - **内容:** 后端增加 `environment info` RPC，让 App 可以查询执行环境的 Shell 和工作目录。
    - **重要性:** 为跨平台远程开发环境配置提供必要的上下文信息。

6.  **#30384 增加 `currentTime/read` 超时时间** ([链接](https://github.com/openai/codex/pull/30384))
    - **内容:** 将 API 请求超时从 5 秒延长至 10 秒。
    - **重要性:** 缓解因响应缓慢导致的部分功能报错。

7.  **#30327 稳定合成调用的输出 ID** ([链接](https://github.com/openai/codex/pull/30327))
    - **内容:** 修复了 `ContextManager` 在重建拼合提示词时，为“已中止”输出生成不同 ID 的问题。
    - **重要性:** 提高了对话上下文的稳定性，避免因 ID 不一致导致的重试和状态错乱。

8.  **#29691 运行时强制执行市场策略** ([链接](https://github.com/openai/codex/pull/29691))
    - **内容:** 在运行时根据企业策略使被禁止的 Marketplace 插件失效。
    - **重要性:** 增强了企业级安全管控能力。

### 功能需求趋势

- **增强平台兼容性：** 对 Linux 桌面应用的需求呼声极高 (#11023)，同时 Windows 平台的一系列 Bug（沙箱、文件路径、Git 进程）也凸显了跨平台稳定性的重要性。
- **精细化速率与成本控制：** 社区强烈要求获得更详细的配额使用、重置和过期信息 (#29618)。`/undo` 功能恢复的诉求 (#9203) 本质上也用户希望有更多回退和成本控制能力。
- **安全与隐私优先：** `.codexignore` 文件的需求 (#2847, #24993) 持续升温，用户希望在生产环境中安全地使用 Codex，防止敏感信息泄露。
- **可配置性与自主权：** 用户希望在工作流中获得更多控制权，例如在每次编辑前请求确认 (#24325)，或是在后台消耗 Token 时能进行干预。

### 开发者关注点

- **速率限制与计费模型是最大的痛点：** 无论是 Plus 还是 Pro 用户，都报告了预算异常快速消耗的问题 (#28879, #29955)。
- **Windows 平台稳定性问题频发：** 从沙箱集成 (#29072)、Git 进程残留 (#29408) 到后台 Token 消耗 (#30390)，Windows 用户体验亟需改善。
- **认证问题亟待解决：** OAuth Token 过期不刷新 (#27165) 和认证令牌无效化 (#28672) 是导致工作流中断的常见原因。
- **后台行为的透明度不足：** 后台 Suggestion (#30390) 和 SQLite 日志 (#28224) 在无明确提示的情况下消耗资源，引发了用户的不满和不信任。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，各位开发者，早上好。这是为您整理的 2026年6月28日 Gemini CLI 社区动态日报。

---

### 🤖 Gemini CLI 社区动态日报 | 2026-06-28

#### 📰 今日速览

今天社区最关注的焦点是**安全加固**。官方发布了包含关键安全修复的夜间版，同时社区提交了三个独立的安全补丁，共同修复了SSRF、路径遍历和敏感信息泄露等严重漏洞。此外，关于Agent在达到最大执行轮次后错误报告“成功”状态的Bug引发了热议，揭示了Agent状态管理机制的重大缺陷。

---

#### 🚀 版本发布

**v0.51.0-nightly.20260628.gae0a3aa7b**

此版本为过去24小时发布的夜间版，核心更新是一个安全修复：

- **安全修复**: 强制对敏感路径黑名单和 VSCode 的 HITL (Human-in-the-Loop) 检查执行大小写不敏感的匹配，增强了路径安全过滤的健壮性。

[查看完整更新日志](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260626.gb14416447...v0.51.0-nightly.20260628.gae0a3aa7b)

---

#### 🔥 社区热点 Issues

以下是过去24小时内评论数最多的10个重点Issue，它们反映了当前社区最关心的痛点和讨论方向。

1.  **Subagent 错误报告成功状态 (P1 Bug)** #22323
    - **重要性**: 揭示了一个严重的逻辑缺陷：当子Agent在执行时，因超过最大轮次`MAX_TURNS`而被中断，但其最终报告却显示为“成功 (GOAL)”。这可能导致用户在不知情的情况下基于不完整或错误的输出做决策。
    - **社区反应**: 有8条评论，2个赞。用户 `matei-anghel` 详细描述了 `codebase_investigator` 子Agent在未做任何分析后仍报告成功的案例。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/22323)

2.  **利用模型的Bash亲和性：零依赖沙箱 (P2 Enhancement)** #19873
    - **重要性**: 这是一个长期悬而未决的“史诗级”需求。社区希望Gemini CLI能更好地利用模型本身擅长使用Bash命令的能力，通过构建零依赖的OS沙箱，在保证安全的前提下，让Agent更高效地执行本地操作。
    - **社区反应**: 8条评论，1个赞。讨论深入，但其 `effort/large` 和长期开放状态表明实现难度大。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/19873)

3.  **鲁棒的组件级评估 (P1 Feature)** #24353
    - **重要性**: 随着Agent能力增强，其行为评估变得至关重要。此Issue提出了建立“组件级评估”的框架，旨在对Agent的各个子功能进行更精细的测试和验证，确保质量。
    - **社区反应**: 7条评论。作为上层EPIC，它代表了质量控制向细粒度、自动化发展的方向。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/24353)

4.  **AST感知的文件读取、搜索和映射 (P2 Feature)** #22745
    - **重要性**: 讨论引入抽象语法树(AST)技术来提升代码理解和操作能力。AST感知能让Agent更精确地定位类、方法和变量，减少不必要的Token消耗，提升效率。
    - **社区反应**: 7条评论，1个赞。这是一个非常有前瞻性的技术方向，特别是在处理大型代码库时。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/22745)

5.  **通用Agent挂起 (P1 Bug)** #21409
    - **重要性**: 一个高优先级Bug，当Gemini CLI将任务委托给通用Agent时，该Agent会永久挂起。这严重影响了工作流，迫使用户必须手动干预，阻止Agent使用子Agent。
    - **社区反应**: 7条评论，8个赞（本周最高）。用户声誉受影响较大，社区期望尽快修复。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/21409)

6.  **Shell命令执行后卡死 (P1 Bug)** #25166
    - **重要性**: 功能性问题，在执行Shell命令完成后，终端会显示“等待输入”并卡死。这破坏了自动化流程，并会阻塞CLI的正常使用。
    - **社区反应**: 4条评论，3个赞。该问题被反复报告，表明触发该Bug的场景可能较为普遍。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/25166)

7.  **添加确定性编辑和减少自动内存日志 (P2 Bug)** #26525
    - **重要性**: 影响安全和隐私。自动内存功能在将本地对话内容发送给模型处理之前，无法保证敏感信息的脱敏处理（即“先发送，后脱敏”），并且可能记录私有信息。
    - **社区反应**: 5条评论。这是对`Auto Memory`功能的一次重要安全审视。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/26525)

8.  **停止自动内存无限重试低信号会话 (P2 Bug)** #26522
    - **重要性**: 资源效率问题。自动内存功能会无休止地重试处理那些“低信号”的对话会话，浪费计算资源和Token。
    - **社区反应**: 5条评论。与上一个Issue (26525) 共同指向对`Auto Memory`行为的改进需求。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/26522)

9.  **Agent应停止/阻止破坏性行为 (P2 Feature)** #22672
    - **重要性**: 安全性与可靠性。讨论当Agent进行如`git reset --force`、数据库修改等具有潜在破坏性的操作时，应如何主动劝阻或要求用户确认。
    - **社区反应**: 3条评论，1个赞。体现了社区对Agent安全护栏的强烈需求。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/22672)

10. **`/chat share` 应包含子Agent轨迹 (P3 Feature)** #22598
    - **重要性**: 调试和评估效率。目前子Agent的执行轨迹（Trajectory）难以获取，这给调试和评估带来了不便。提出将其纳入`/chat share`功能，使分享和分析子Agent行为更为便利。
    - **社区反应**: 2条评论，1个赞。体现社区对Agent行为透明度的需求。
    [查看详情](https://github.com/google-gemini/gemini-cli/issues/22598)

---

#### 🚧 重要 PR 进展

以下10个PR在过去24小时内取得进展，值得关注。

1.  **修复 DNS 重绑定 SSRF 漏洞 (Security Fix)** #28181
    - **内容**: 修复了 `web_fetch` 工具中的SSRF保护机制，使其不再仅依赖主机名字符串检查，而是通过DNS解析来防御DNS重绑定攻击。
    - **状态**: 新创建的开放PR。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28181)

2.  **从白名单变量中移除Github上下文 (Security Fix)** #28179
    - **内容**: 将 `ISSUE_BODY` 和 `ISSUE_TITLE` 从始终允许的环境变量列表中移除，防止它们在CI模式下绕过消毒环节，从而避免敏感信息泄露。
    - **状态**: 新创建的开放PR。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28179)

3.  **恢复 `@` 引用文件的防御性路径解析 (Security Fix)** #28180
    - **内容**: 恢复了之前被回滚的路径遍历漏洞修复（#27943），再次为 `read_file` 等文件操作工具加上了防御性的路径解析，防止通过符号链接进行越权访问。
    - **状态**: 新创建的开放PR。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28180)

4.  **要求批准的机器人补丁产物 (Security Fix)** #28178
    - **内容**: 要求bot在应用自动生成的补丁文件前，必须有一个明确的批准标记，以确保发布流程的安全，防止恶意或意外的代码被合并。
    - **状态**: 开放PR。对CI/CD流水线安全性的重要增强。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28178)

5.  **新增 eval 覆盖率报告命令 (Feature)** #28169
    - **内容**: 新增 `eval:coverage` 命令，通过交叉引用已有的测试清单和工具注册表，可以报告内置工具的评估覆盖率。有助于发现测试盲区。
    - **状态**: 开放PR。对提升代码质量和测试完备性有积极意义。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28169)

6.  **Shell参数扩展需确认 (Policy Fix)** #28175
    - **内容**: 当白名单中的Shell命令包含`$`等参数扩展符时，在交互模式下需用户确认后才能执行，在非交互(YOLO)模式下直接拒绝。通过策略限制潜在危险命令。
    - **状态**: 开放PR。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28175)

7.  **阻止Agent在任务失败时无声扩大范围 (Agent Fix)** #28171 / #28172
    - **内容**: 修复了Agent在无法按初始方法完成任务时，会“静默”地切换到新策略（如读取整个文件、运行脚本）的问题，确保任何范围扩大操作都需告知用户。
    - **状态**: 开放PR。直接回应了社区对Agent行为透明度的关切。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/28171) | [#28172](https://github.com/google-gemini/gemini-cli/pull/28172)

8.  **限制待处理工具响应的上限 (Core Fix)** #27870
    - **内容**: 此PR在关闭后因来自社区的反馈被重新打开。它旨在限制单个工具调用的返回结果过大，避免造成 `functionResponse` 挂起，从而阻止模型进一步思考。
    - **状态**: 已关闭但被重新审视。说明其修复思路对解决“Agent挂起”类问题有价值。
    [查看详情](https://github.com/google-gemini/gemini-cli/pull/27870)

---

#### 📈 功能需求趋势

从本日的Issue和PR中，可以总结出社区最关注的三大功能趋势：

1.  **Agent 行为强制约束与透明化**: 社区不再满足于Agent“能做什么”，更关注它“**不能做什么**”以及“**为什么这样做**”。这包括要求Agent在扩大操作范围、执行破坏性命令、或失败时进行明确的**确认、报告和日志记录**。相关Issue和PR的数量和讨论热度都很高。
2.  **安全防护体系持续增强**: 安全修复是本日更新和社区贡献的绝对主力，覆盖了SSRF、路径遍历、敏感信息泄露、CI/CD流水线安全等多个方面。这表明随着Gemini CLI的能力边界扩大，其攻击面也随之增加，安全已成为社区的压倒性诉求。
3.  **精细化评估与调试能力**: 社区正在为更复杂的Agent系统建立质量保障基础设施。这包括对Agent行为的**组件级评估 (Component-Level Evaluations)**、为开发者提供**子Agent执行轨迹**的可视化分享（`/chat share`），以及新增**评估覆盖率报告**。目标是从“黑盒”测试走向“灰盒”甚至“白盒”的精细化管理。

---

#### 🎯 开发者关注点

开发者反馈中反复出现的最痛点和高频需求：

1.  **Agent 不可预测的“卡死”和“挂起”问题** (如 #21409, #25166)。这是破坏生产力的头号杀手，开发者对此容忍度极低。
2.  **对`Auto Memory`等自动化功能感到不信任** (如 #26525, #26522)。开发者担心其隐私风险、资源浪费以及行为不可控。
3.  **Agent 工作状态不透明** (如 #28171, #22598)。开发者难以理解Agent的内部决策和失败原因，导致调试和协作困难。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，这是为您生成的 2026-06-28 GitHub Copilot CLI 社区动态日报。

---

# GitHub Copilot CLI 社区动态日报 | 2026-06-28

## 今日速览
昨日 Copilot CLI 社区活跃度极高，涌现了多个关键 Bug 报告。Windows 平台问题集中爆发，包括 **v1.0.66 版本无法启动 `.bat`/`.cmd` MCP 服务器**的严重回归，以及**复制功能完全失效**的顽疾。此外，**软换行复制丢失空格**的问题在修复后再次被确认未完全解决，社区对终端 UI 的稳定性表示担忧。

## 版本发布
**无。** 目前最新版本为 v1.0.66，但社区反馈其存在严重 Windows 回归问题。

## 社区热点 Issues

以下是过去24小时内更新或创建的、最值得关注的 10 个 Issue：

1.  **#3958 [严重回归] Windows: v1.0.66 无法启动 .bat/.cmd MCP 服务器**
    *   **摘要**: 这是 v1.0.66 版本引入的严重回归。当 MCP 服务器的 `command` 是 `.bat` 或 `.cmd` 文件并带有参数时，子进程会立即崩溃并报错 `The syntax of the command is incorrect.`。这直接破坏了 Windows 上使用本机脚本作为 MCP Server 的生态。
    *   **重要性与反应**: ❗️ 等级最高。影响所有依赖批处理脚本的 Windows 开发者，属于阻断性 Bug。需要紧急修复。
    *   **链接**: [Issue #3958](https://github.com/github/copilot-cli/issues/3958)

2.  **#3964 [待验证] 复制软换行输出仍然在换行边界处丢失空格**
    *   **摘要**: 用户反馈，在 v1.0.65 中，复制被软换行（word wrap）截断的输出时，行尾的空格会被删除，导致两个单词意外粘连。此问题在 #3666 中曾声称修复，但用户确认在 v1.0.59 及更高版本中仍然存在。
    *   **重要性与反应**: 这是对之前修复工作的二次确认，表明修复不完整。这会严重影响用户复制代码或命令输出的准确性，降低工作效率。
    *   **链接**: [Issue #3964](https://github.com/github/copilot-cli/issues/3964)

3.  **#3949 [严重] Windows 11 复制功能完全失效**
    *   **摘要**: 用户在 Windows 11 上使用 Copilot CLI 时，触发复制操作后，系统剪贴板中没有任何内容。AI 助手会提示“已复制到剪贴板”，但实际并未生效。用户要求至少增加校验机制。
    *   **重要性与反应**: ❗️ 等级高。这是复制功能在特定平台的完全失效，对日常使用影响极大。社区已经关注，需要尽快排查是 CLI 本身问题还是与 Windows 11 的兼容性问题。
    *   **链接**: [Issue #3949](https://github.com/github/copilot-cli/issues/3949)

4.  **#3959 终端 UI 残留“幽灵”字符**
    *   **摘要**: 在 Copilot CLI 的 TUI 界面中，当使用退格键删除文本时，视觉界面上会残留原有字符的轮廓或片段，形成视觉伪影。
    *   **重要性与反应**: 影响用户体验，会使用户感到界面粗制滥造，降低对工具的信任感。可能与终端渲染引擎的刷新机制有关。
    *   **链接**: [Issue #3959](https://github.com/github/copilot-cli/issues/3959)

5.  **#3957 MacBook Pro 触控板无法滚动查看历史消息**
    *   **摘要**: 在 v1.0.65 版本中，使用 MacBook Pro 触控板进行双指滚动时，无法滚动终端窗口查看之前的对话历史。触控板操作会被误识别为选择历史命令。
    *   **重要性与反应**: 影响 macOS 用户的交互体验，用户无法高效查阅历史上下文。这属于输入事件处理的 Bug。
    *   **链接**: [Issue #3957](https://github.com/github/copilot-cli/issues/3957)

6.  **#1799 社区呼吁：提供关闭“alt-screen”模式的选项**
    *   **摘要**: 这是一个历史悠久的 Issue（2026年3月创建），直到近期（6月27日）仍有新的讨论。用户认为 Copilot CLI 新引入的 alt-screen（全屏视图）造成了诸多不便，希望能提供开关或恢复到原始的内联显示模式。
    *   **重要性与反应**: 👍 7票支持。这是一个持续存在的社区需求，反映了用户对新 UI 布局的接受度不高，偏好更简洁的交互方式。
    *   **链接**: [Issue #1799](https://github.com/github/copilot-cli/issues/1799)

7.  **#2165 Ubuntu Keychain 认证支持损坏**
    *   **摘要**: 在 Ubuntu 系统上，Copilot CLI 的认证令牌存储在 Keychain 时遇到两个 Bug：一是官方文档指导错误，二是 `secret-tool` 未安装时，`apt install` 后仍无法正常工作。
    *   **重要性与反应**: 👍 20票支持。Linux 用户群体非常关注认证问题的稳定性和准确性，文档错误会误导用户，降低 Linux 平台的支持体验。
    *   **链接**: [Issue #2165](https://github.com/github/copilot-cli/issues/2165)

8.  **#3874 VS Code Agent 的 `preToolUse` 钩子拒绝功能失效**
    *   **摘要**: 用户配置了 `.github/hooks/hooks.json` 来拒绝所有 `preToolUse` 操作，但该钩子配置在 Copilot CLI 中完全不生效，Agent 仍然可以随意执行命令。
    *   **重要性与反应**: 这是一个严重的安全功能 Bug。用户依赖钩子机制来实施安全策略和控制 Agent 行为，该功能失效意味着任何自定义安全策略都形同虚设。
    *   **链接**: [Issue #3874](https://github.com/github/copilot-cli/issues/3874)

9.  **#3815 Windows 调试日志路径反斜杠缺失**
    *   **摘要**: 在 Windows 系统上，当 Copilot CLI 输出调试日志的保存路径时，路径中缺少了一个反斜杠 `\`，导致用户无法直接复制粘贴该路径到资源管理器来定位日志文件。
    *   **重要性与反应**: 一个小但恼人的 Bug。对于开发者来说，依赖日志进行调试是常见操作，路径错误会直接阻碍调试流程。
    *   **链接**: [Issue #3815](https://github.com/github/copilot-cli/issues/3815)

10. **#3963 功能请求：显示 Session 保留/过期时间**
    *   **摘要**: 用户反馈，Copilot 的会话有时会无故消失或重置，希望能够从状态栏直接查看当前会话的保留策略和过期时间。
    *   **重要性与反应**: 这是一个关于透明度和可预期性的功能请求。解决用户的疑惑，提升对会话管理的可控感。
    *   **链接**: [Issue #3963](https://github.com/github/copilot-cli/issues/3963)

## 重要 PR 进展

1.  **#3928 [OPEN] 添加 .gitignore 和设置配置**
    *   **摘要**: 一个来自 `tpsaint` 的 PR，旨在为项目（或与之相关的模板）添加 `.gitignore` 和配置文件。这表明社区在关注开发环境的标准化。
    *   **链接**: [PR #3928](https://github.com/github/copilot-cli/pull/3928)

2.  **#570 [CLOSED] [WIP] 为 README.md 添加 macOS 安装说明**
    *   **摘要**: 由 @Copilot 创建的自动化 PR，旨在完善 macOS 平台安装文档。虽然已被关闭，但表明官方在持续优化多平台文档。
    *   **链接**: [PR #570](https://github.com/github/copilot-cli/pull/570)

3.  **#3737 [OPEN] 一个名为 `Jigg empire ai` 的测试性/实验性 PR**
    *   **摘要**: 一个新用户提交的 PR，内容为“Let’s try this new method”。很可能是一个测试或不成熟的提案，社区关注度低，但反应了项目门槛较低，有大量新用户尝试贡献。
    *   **链接**: [PR #3737](https://github.com/github/copilot-cli/pull/3737)

## 功能需求趋势

从昨日的 Issues 中可以提炼出以下社区最关注的功能方向：

*   **终端 UI 定制化与稳定性**: 社区对 `alt-screen` 模式有强烈的关闭需求 (#1799)，同时对 UI 渲染的 Bug（如幽灵字符 #3959）容忍度低。**结论：用户更青睐简洁、确定的 UI 交互。**
*   **平台兼容性与回归问题**: Windows 平台问题尤为突出，多个 Bug 指向特定功能（复制、MCP服务器启动）的完全失效 (#3949, #3958)。**结论：跨平台功能的回归测试急需加强，Windows 是痛点重灾区。**
*   **会话管理与透明度**: 用户希望了解会话的机制和生命周期，如明确会话过期时间 (#3963)，以提高对工具行为的可控性和理解。
*   **Agent 行为可控性**: 安全钩子 `preToolUse` 的失效 (#3874) 引发了对 Agent 安全控制的担忧。**结论：用户不满足于Agent“能工作”，更要求 Agent“安全地工作”。**
*   **与 VS Code 的深度集成**: Issue #3874 和 #2778（关于 `/btw` 功能）均体现了用户希望 Copilot CLI 的操作和 Agent 逻辑能更无缝地与 VS Code 体验结合，例如共享上下文或配置。

## 开发者关注点

*   **稳定性大于新功能**: 大量的 Bug 报告（特别是回归问题）表明，开发者目前最迫切的需求是 **“让它稳定工作”**，而非引入炫酷的新功能。频繁的破坏性变更正在消耗信任。
*   **Windows 原生体验的缺失**: Windows 用户的体验显著落后于 macOS/Linux。从复制到命令行执行，基础功能都存在缺陷，这提示开发团队可能需要专门的 Windows 兼容性测试。
*   **信息透明度和校验**: 开发者不再满足于工具单方面告知“已复制”，而是期望有校验机制 (#3949)。这也反映在其他需求上，如希望看到 Session 过期时间。
*   **配置的灵活性与可回退性**: 无论是对 UI 模式 (`alt-screen`) 还是快捷键 (`/voice` 的快捷键 #3672)，开发者都希望获得更多的自定义控制和回退到旧有习惯的选项。**“不要替我做决定，给我选择权”** 是核心诉求。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是为您生成的 2026-06-28 OpenCode 社区动态日报。

---

# OpenCode 社区动态日报 | 2026-06-28

## 今日速览

今日社区主要聚焦于 **稳定性与兼容性修复**。数个关键 PR 针对 TUI 崩溃、WSL 路径错误和会话恢复等痛点进行了修复。与此同时，社区对 **新模型支持（如 minimax-m3、GLM-5.2）** 和 **原生包管理** 的需求呼声依然很高。

## 版本发布

今日无新版本发布。

## 社区热点 Issues

以下是根据讨论热度、社区反馈和影响范围挑选的 10 个最值得关注的 Issue：

1.  **[#8816] [FEATURE]: 提供 llms.txt 和文档 Markdown 格式** (🔥 15条评论 | 34 👍)
    *   **重要性**: 社区强烈渴望一种更便捷、AI友好的方式解析和下载 OpenCode 的文档。此功能需求获得极高赞同，表明开发者对提升AI辅助开发体验有迫切需求。
    *   **链接**: [anomalyco/opencode Issue #8816](https://github.com/anomalyco/opencode/issues/8816)

2.  **[#23153] [FEATURE]: 使用加密货币支付** (🔥 13条评论 | 24 👍)
    *   **重要性**: 尽管评论数不如前者，但赞同率极高。开发者对支付方式的多样性有明确诉求，尤其是关注去中心化支付选项的 Web3 开发者。
    *   **链接**: [anomalyco/opencode Issue #23153](https://github.com/anomalyco/opencode/issues/23153)

3.  **[#13877] TUI `/sessions` 选择器仅显示最近的会话** (9条评论)
    *   **重要性**: 这是一个影响核心用户体验的Bug。用户无法在 TUI 中浏览和切换到较早的会话，严重阻碍了工作流。社区对此问题的持续关注表明会话管理是 TUI 用户的一个高频痛点。
    *   **链接**: [anomalyco/opencode Issue #13877](https://github.com/anomalyco/opencode/issues/13877)

4.  **[#22422] [Bug, Core] 内存泄漏警告** (7条评论)
    *   **重要性**: 核心组件的内存泄漏警告，可能导致服务端性能和稳定性问题。虽然已关闭，但其暴露的 `MaxListenersExceededWarning` 问题受到密切关注。
    *   **链接**: [anomalyco/opencode Issue #22422](https://github.com/anomalyco/opencode/issues/22422)

5.  **[#19473] 桌面应用向 WSL 托管服务器发送 UNC 路径，导致 Bash 工具调用失败** (7条评论)
    *   **重要性**: Windows + WSL 是开发者的主流配置之一。此 Bug 破坏了核心的 Bash 工具调用功能，尽管已有临时解决方案，但根源问题依然存在，影响大量 Windows 用户。
    *   **链接**: [anomalyco/opencode Issue #19473](https://github.com/anomalyco/opencode/issues/19473)

6.  **[#33890] Bun 1.3.14 在 Linux x86_64 上段错误 (SIGILL)** (6条评论)
    *   **重要性**: 严重且致命的运行时崩溃问题。在配备了现代 CPU 的 Linux 服务器上，TUI 启动后短时间即崩溃，极大地阻碍了开发工作，并可能指向更底层的兼容性问题。
    *   **链接**: [anomalyco/opencode Issue #33890](https://github.com/anomalyco/opencode/issues/33890)

7.  **[#34228] Bug: OpenCode 向模型暴露不完整、不稳定项目技能** (5条评论)
    *   **重要性**: 技能的可用性在不同会话间不一致，严重损害了技能系统的一致性和可靠性。这可能表明技能加载或注入逻辑存在时序问题，需要尽快修复。
    *   **链接**: [anomalyco/opencode Issue #34228](https://github.com/anomalyco/opencode/issues/34228)

8.  **[#19130] Windows ARM64 原生：TUI 初始化失败** (6条评论)
    *   **重要性**: 随着 ARM 生态发展，Windows ARM64 支持日益重要。此问题显示 TUI 在 ARM64 原生二进制上完全无法启动，是平台适配的关键障碍。
    *   **链接**: [anomalyco/opencode Issue #19130](https://github.com/anomalyco/opencode/issues/19130)

9.  **[#30895] 桌面 v1.16.0 将 WSL 工作区路径转换为 Windows 路径，破坏文件/会话列表** (6条评论)
    *   **重要性**: 类似 #19473，再次指向 Windows-WSL 混用场景下的路径处理顽疾。新版本反而引入回退，说明此问题需要系统性的解决方案。
    *   **链接**: [anomalyco/opencode Issue #30895](https://github.com/anomalyco/opencode/issues/30895)

10. **[#33213] 服务端模式：长时间运行导致 JS 堆/内存泄漏** (5条评论)
    *   **重要性**: 服务端长时运行模式下的严重内存泄漏问题。内存占用飙升至数十 GB 并触发 Swap，直接威胁生产环境的稳定性。
    *   **链接**: [anomalyco/opencode Issue #33213](https://github.com/anomalyco/opencode/issues/33213)

## 重要 PR 进展

以下是 10 个重要的 Pull Requests，它们带来了新功能或修复了关键问题：

1.  **[#34253] fix(app): 修复 Sandbox 项目编辑** (🔥 最新提交)
    *   **内容**: 通过更精确的项目元数据匹配，确保 Sandbox 目录下的项目编辑操作能正确执行。
    *   **链接**: [anomalyco/opencode PR #34253](https://github.com/anomalyco/opencode/pull/34253)

2.  **[#34254] fix(app): 限制会话页面错误范围** (🔥 最新提交)
    *   **内容**: 为会话页面主面板添加 ErrorBoundary，防止单个会话加载失败导致整个标签页崩溃，增强了崩溃隔离能力。
    *   **链接**: [anomalyco/opencode PR #34254](https://github.com/anomalyco/opencode/pull/34254)

3.  **[#34256] fix(server): 拒绝实例查找前的“外来”目录提示** (🔥 最新提交)
    *   **内容**: 直接解决 WSL/Windows 路径问题系列（#30895, #19473），通过在实例查找前验证并拒绝不匹配的目录提示，从根源上防止路径混乱。
    *   **链接**: [anomalyco/opencode PR #34256](https://github.com/anomalyco/opencode/pull/34256)

4.  **[#34270] feat(tools): 将 MiMo 工具和子系统移植到 OpenCode** (🔥 最新提交)
    *   **内容**: 引入大量新工具（`multiedit`, `codesearch`, `memory` 等），并基于 BM25 算法实现了无数据库的内存和会话历史子系统，是功能上的一次重大扩展。
    *   **链接**: [anomalyco/opencode PR #34270](https://github.com/anomalyco/opencode/pull/34270)

5.  **[#34263] feat(tui): 为 V2 会话接入撤销/重做/回滚** (🔥 新合并)
    *   **内容**: 将后端 V2 暂存版本回滚 API 接入 TUI，补全了关键的编辑操作控制功能。
    *   **链接**: [anomalyco/opencode PR #34263](https://github.com/anomalyco/opencode/pull/34263)

6.  **[#34264] feat(tui): 为 V2 会话增加重命名功能** (🔥 新合并)
    *   **内容**: 实现了端到端的会话重命名，包括新增后端事件、核心接口和 TUI 的交互支持，增强了会话管理能力。
    *   **链接**: [anomalyco/opencode PR #34264](https://github.com/anomalyco/opencode/pull/34264)

7.  **[#29881] fix(tui): 为 Wayland 系统添加 wl-paste 文本读取** (🔥 最新提交)
    *   **内容**: 修复了 Wayland 系统上粘贴功能失效的问题。通过添加对 `wl-paste` 的支持，解决了 Linux 用户在特定桌面环境下的日常使用痛点。
    *   **链接**: [anomalyco/opencode PR #29881](https://github.com/anomalyco/opencode/pull/29881)

8.  **[#34242] fix(tui): 防止管道输入破坏交互** (🔥 新提交)
    *   **内容**: 这是一个解决**众多**相关 Issue（#28538, #24195 等）的修复 PR，当用户通过管道向 OpenCode 输入内容时，防止 TUI 界面和键盘输入被破坏。
    *   **链接**: [anomalyco/opencode PR #34242](https://github.com/anomalyco/opencode/pull/34242)

9.  **[#34234] fix: 保留附件文件路径** (🔥 新提交)
    *   **内容**: 修复了拖拽/粘贴附件后，Agent 无法访问原始文件路径的问题，确保 Agent 能直接操作本地文件而非仅处理嵌入数据。
    *   **链接**: [anomalyco/opencode PR #34234](https://github.com/anomalyco/opencode/pull/34234)

10. **[#34261] fix(core): 保护非减容量的压缩操作** (🔥 新提交)
    *   **内容**: 修复了当上下文压缩（compaction）不奏效时可能引发的无限循环或溢出恢复问题，提升核心会话管理的健壮性。
    *   **链接**: [anomalyco/opencode PR #34261](https://github.com/anomalyco/opencode/pull/34261)

## 功能需求趋势

从今日的 Issue 和 PR 中，可以提炼出社区以下几个主要的功能关注方向：

1.  **平台兼容性（高频痛点）**:
    *   **Windows + WSL 集成**: 这是最突出的痛点，表现为路径处理错误（#19473, #30895），严重阻碍了用户工作流。
    *   **Windows ARM64 支持**: 原生二进制存在启动问题（#19130），反映了对新兴架构适配的迫切需求。
    *   **Linux Wayland**: 缺少 `wl-paste` 支持（#29881），破坏了核心交互功能。

2.  **稳定性和性能**:
    *   **内存泄漏**: 服务端（#33213）和前端（#22422）均出现内存泄漏警告，是影响长期运行和用户体验的关键。
    *   **运行时崩溃**: Bun 1.3.14 的 `SIGILL` 崩溃（#33890）是严重的运行问题。
    *   **技能系统稳定性**: 技能暴露不一致（#34228）破坏了用户对技能系统的信任。

3.  **模型和 AI 集成**:
    *   **新模型支持**: 社区要求集成 minimax-m3（#34177）、GLM-5.x（#34113, #31348）等新模型。
    *   **企业级模型支持**: 用户希望 OpenCode 能通过 GitHub Copilot 等途径使用企业自有的第三方模型（#34030）。
    *   **特定模型的行为修复**: 包括 GLM-5.2 不支持图片输入（#34113）、NVIDIA Nemotron 模型卡住（#34026）等。

## 开发者关注点

1.  **支付与商业模式**: 开发者对“使用加密货币支付”（#23153）的强烈兴趣，暗示社区期望更灵活的付费方案，对传统支付方式之外的选项有期待。
2.  **文档与知识库**: `llms.txt` ( #8816 ) 的提议表明开发者希望 OpenCode 能更好地服务于 AI 辅助开发，将自身的知识库以 AI 能高效解析的格式公开。
3.  **用户界面与体验**:
    *   **会话管理**: TUI 会话列表不完整（#13877）和桌面应用缺少会话管理界面（#34232）被广泛提及，说明丰富的会话管理是用户的核心需求。
    *   **稳定性是前提**: 从会话冻结（#34214）到管道输入破坏 UI（#34242），所有破坏基本交互流程的 Bug 都会受到开发者强烈关注。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，这是为您生成的 2026-06-28 Pi 社区动态日报。

---

# Pi 社区动态日报 | 2026-06-28

## 今日速览

社区今日迎来 Issues 和 PR 的密集更新潮，其中 **错误处理**、**扩展 API 能力增强**、以及 **交互体验优化** 是核心议题。多个关于 **TUI 渲染（闪烁/滚动/重绘）** 的 Bug 得到了确认，同时社区也在积极为 **扩展系统** 添加成本汇报（`reportUsage`）和工具执行权限等关键功能。此外，关于 `Ctrl+G` 编辑器配置的 PR 被合并，解决了特定环境下的痛点。

## 版本发布

过去24小时内无新版本发布。

## 社区热点 Issues

1.  **[#5825] Streaming markdown forces scroll to bottom**
    -   **重要性**: 高。该问题描述了当启用 `clear on shrink` 设置时，Pi 在流式输出 Markdown 时会强制将滚动条跳转到底部，打断用户的阅读。这是一个影响终端用户体验的常见痛点，社区反应强烈（34条评论）。
    -   **链接**: [Issue #5825](https://github.com/earendil-works/pi/issues/5825)

2.  **[#5763] Providers swallow the HTTP error body, so gateway / non-schema errors are unreadable**
    -   **重要性**: 高。此问题直指开发者调试时的核心痛点：当通过代理/网关使用 API 时，错误信息被底层 SDK “吞掉”，导致开发者无法看到真正的错误原因（如 403 的具体详情），增加了排查难度。已有对应的 PR 在尝试修复。
    -   **链接**: [Issue #5763](https://github.com/earendil-works/pi/issues/5763)

3.  **[#4106] Qwen3.5 Plus, Qwen3.6 Plus, MiniMax M2.7 from OpenCode Go return 404**
    -   **重要性**: 高。这是一个典型的模型兼容性问题，揭示了 Pi 内置模型定义（`pi-ai code`）存在错误，导致部分新模型无法使用。虽然该 Issue 已被关闭，但其背后的“模型定义数据源”问题值得持续关注。
    -   **链接**: [Issue #4106](https://github.com/earendil-works/pi/issues/4106)

4.  **[#6129] Package Report: @hypabolic/pi-hypa**
    -   **重要性**: 中（安全相关）。社区用户举报了一个疑似恶意/刷安装量的扩展包。这表明 Pi 的扩展生态需要更完善的审查或安全机制，防止“流氓”包污染生态。
    -   **链接**: [Issue #6129](https://github.com/earendil-works/pi/issues/6129)

5.  **[#6131] Full screen redraw (flicker) when multiple tool calls stream simultaneously**
    -   **重要性**: 中。该 Issue 报告了当模型在一次回复中调用多个工具时，TUI 界面会频繁闪屏（整个屏幕重绘）。这是对用户视觉体验的严重干扰，反映了 TUI 渲染引擎在并发场景下的不足。
    -   **链接**: [Issue #6131](https://github.com/earendil-works/pi/issues/6131)

6.  **[#6130] renderCall/renderResult silently ignore exceptions**
    -   **重要性**: 中。这是一个对开发者不友好的行为。当自定义渲染器（renderer）的代码有错误（如导入了一个不存在的模块）时，系统会静默地回退到默认渲染，隐藏了真实的错误信息。这让调试扩展变得非常困难。
    -   **链接**: [Issue #6130](https://github.com/earendil-works/pi/issues/6130)

7.  **[#6122] Feature request: add externalEditor setting for Ctrl+G**
    -   **重要性**: 高。用户希望在 `settings.json` 中直接配置 `Ctrl+G` 调用的外部编辑器，而不是依赖不可靠的环境变量 `$EDITOR`。这解决了 Windows + Git Bash + VS Code 环境下环境变量被锁定无法修改的痛点。
    -   **链接**: [Issue #6122](https://github.com/earendil-works/pi/issues/6122)

8.  **[#6105] [bug] User messages get incorrectly escaped**
    -   **重要性**: 中。用户报告了一个简单的转义 Bug：输入 `"\"` 会被错误地显示为 `""`。虽然是个小问题，但会影响代码片段的准确性。用户使用 `--no-extensions` 复现了问题，表明这是核心逻辑的缺陷。
    -   **链接**: [Issue #6105](https://github.com/earendil-works/pi/issues/6105)

9.  **[#6127] --append-system-prompt can't override the default coding-agent identity**
    -   **重要性**: 中。该 Issue 指出 `--append-system-prompt` 功能无法覆盖 Pi 的默认 coding agent 身份。这对于想用 Pi 作为后端，并自定义 AI 人格的开发者来说是个障碍。
    -   **链接**: [Issue #6127](https://github.com/earendil-works/pi/issues/6127)

10. **[#6128] Support diffusiongemma thinking and tool calls**
    -   **重要性**: 中。报告了对新模型 `diffusiongemma` 的支持问题：其“思考（thinking）”块被错误地渲染为普通文本，并且不支持工具调用。这表明对新集成模型的兼容性测试有待加强。
    -   **链接**: [Issue #6128](https://github.com/earendil-works/pi/issues/6128)

## 重要 PR 进展

1.  **[#5735] fix(coding-agent): defer extension reload requests safely**
    -   **内容**: 重写了扩展重载机制，使其在扩展上下文（而不是仅在斜杠命令中）中也能安全使用。通过延迟（deferral）机制，确保重载只在安全的边界执行。
    -   **链接**: [PR #5735](https://github.com/earendil-works/pi/pull/5735)

2.  **[#6123] feat(coding-agent): add externalEditor setting for Ctrl+G**
    -   **内容**: 已合并。实现了在 `settings.json` 中通过 `externalEditor` 配置 `Ctrl+G` 调用的外部编辑器，解决了 Windows + Git Bash 环境下的兼容性问题。
    -   **链接**: [PR #6123](https://github.com/earendil-works/pi/pull/6123)

3.  **[#6119] feat: add reportUsage API for extensions to contribute session cost**
    -   **内容**: 已合并。为扩展添加了 `reportUsage` API，允许子扩展（如 subagent）将其消耗的 token/成本反馈到主会话的页脚或 `/session` 统计中，解决了成本信息碎片化的问题。
    -   **链接**: [PR #6119](https://github.com/earendil-works/pi/pull/6119)

4.  **[#5678] Add excludeFromContext for custom messages**
    -   **内容**: 为自定义消息添加了 `excludeFromContext` 属性。标记后的消息会正常渲染和持久化，但不会进入大模型上下文，有助于节省 token 并控制对话质量。
    -   **链接**: [PR #5678](https://github.com/earendil-works/pi/pull/5678)

5.  **[#5832] fix(ai): surface provider HTTP error body instead of opaque SDK message**
    -   **内容**: 旨在修复 Issue #5763。让 Pi 直接透传来自提供商的 HTTP 错误体，而不是显示 SDK 返回的模糊或无意义的错误信息。这将极大改善 API 调试体验。
    -   **链接**: [PR #5832](https://github.com/earendil-works/pi/pull/5832)

6.  **[#6115] feat(coding-agent): add configurable chat padding**
    -   **内容**: 一个还在讨论中的 PR。目的是为 TUI 添加可配置的聊天气泡内边距（padding）。虽然改动不小，但反映了社区对界面自定义的强烈需求。
    -   **链接**: [PR #6115](https://github.com/earendil-works/pi/pull/6115)

7.  **[#6099] Rename model key from 'gpt-5.2-chat-latest' to 'gpt-5.2-chat'**
    -   **内容**: 已合并。修正了 Azure OpenAI 中模型名称的错误定义，将不存在的 `gpt-5.2-chat-latest` 更正为 `gpt-5.2-chat`。
    -   **链接**: [PR #6099](https://github.com/earendil-works/pi/pull/6099)

8.  **[#6111] fix(coding-agent): report settings write failures in install/remove**
    -   **内容**: 已合并。修复了 `pi install` 命令在 `settings.json` 文件为只读权限时，依然报告“安装成功”的问题。现在会正确报错。
    -   **链接**: [PR #6111](https://github.com/earendil-works/pi/pull/6111)

9.  **[#6109] fix(coding-agent): preserve dependency cache on extension reload**
    -   **内容**: 已合并。修复了 `Pi` 发布版（release binary）在 `/reload` 时重新执行扩展依赖项（dependency module side effects）的问题，解决了因重复执行导致的问题（如注册两次主题）。
    -   **链接**: [PR #6109](https://github.com/earendil-works/pi/pull/6109)

## 功能需求趋势

-   **扩展生态完善**: 社区焦点正在从“能用”转向“好用”，具体表现为对扩展 API 的增强需求：
    -   **成本透明度**: 通过 `reportUsage` 让子扩展能够向主会话汇报消耗（已实现）。
    -   **执行能力**: 扩展希望能获取执行已注册工具（tool）的能力（如 Issue #6121）。
    -   **配置化**: 扩展和核心功能都倾向于通过 `settings.json` 进行配置，而非仅仅依赖环境变量（如 `externalEditor`）。
-   **TUI 自定义与体验优化**:
    -   **可定制性**: 用户希望自定义聊天气泡的间距（padding）、字体、渲染效果等。
    -   **渲染健壮性**：涌现出多个与 TUI 渲染相关的 Bug（如滚动、闪烁、静默容错），表明 TUI 的稳定性和兼容性是当前的一个薄弱环节。
-   **新模型与提供商支持**: 诉求主要集中在两点：一是确保新模型能被正确识别和定义（如 Qwen、DiffusionGemma），二是修复与特定网关/提供商的兼容性问题（如 Azure、OpenCode-Go）。

## 开发者关注点

-   **调试困难**: `renderCall/renderResult` 的静默容错行为 (#6130) 和 HTTP 错误体被吞掉 (#5763) 是两个最显著的开发者体验痛点，严重阻碍了扩展开发和 API 调试。
-   **环境兼容性**: Windows + WSL/Git Bash 环境下的环境变量问题是热点，多次出现在议题中，导致编辑器配置等功能不可用。
-   **安全与可信度**: 恶意包 (#6129) 的出现提醒开发者，在扩展生态快速发展时需关注安全审查和代码来源的可信度。
-   **模型定义准确性问题**: Pi 内置的模型列表（model definitions）可能存在过时或错误，导致用户无法使用最新模型。这要求维护者与各大模型提供商保持同步。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，这是为您生成的 2026-06-28 Qwen Code 社区动态日报。

---

# Qwen Code 社区动态日报 | 2026-06-28

## 今日速览
**`v0.19.2-nightly`** 发布，主要包含一个 web_fetch 的 JSON 回退修复。社区讨论热度集中在**Token管理优化**和**协程任务可见性**两大主题，多个相关 Issue 和 PR 正在密集推进。此外，**Chrome 扩展复活提案**和**跨设备任务同步**的需求获得了开发者积极响应。

---

## 版本发布

### v0.19.2-nightly.20260628
- **发布链接**: [v0.19.2-nightly.20260628.714513df2](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.2-nightly.20260628.714513df2)
- **主要变更**:
    - `fix(core)`: 修复了 web_fetch 工具在获取内容时，如果响应格式不符合预期，无法优雅地回退到 JSON 解析的问题。([#5660](https://github.com/QwenLM/qwen-code/pull/5660))
    - `chore(release)`: 日常版本发布流程。

---

## 社区热点 Issues (10条)

1. **[#5942] Anthropic provider: 可避免的 Prompt-Cache Miss 导致成本飙升**
    - **重要性**: 核心性能/成本问题。用户反馈在使用 Anthropic 协议后端时，Qwen Code 的 Prompt-Cache 命中率远低于 Claude Code，导致成本异常增加，属于需要优先解决的性能瓶颈。
    - **链接**: [Issue #5942](https://github.com/QwenLM/qwen-code/issues/5942)

2. **[#5819] 升级后自动修改设置：使用更高单价模型并浪费 Token**
    - **重要性**: 涉及用户资金安全的严重 Bug。用户反馈升级到 v0.19 后，系统自动将模型切换到更高单价的版本，并触发了繁简体中文转换的 Token 浪费，导致费用超额。社区反应激烈，开发者已在跟进。
    - **链接**: [Issue #5819](https://github.com/QwenLM/qwen-code/issues/5819)

3. **[#5823] /loop 协程任务静默执行，用户无感知也无控制权**
    - **重要性**: 核心功能缺陷。用户设置的定时任务（`/loop` / cron）在后台无提示执行，且无法通过模型查看或停止已创建的任务。这破坏了用户的预期控制，是重要的功能改进方向。
    - **链接**: [Issue #5823](https://github.com/QwenLM/qwen-code/issues/5823)

4. **[#5836] 创建任务清单时，能否选择持久化到项目内以实现跨设备同步？**
    - **重要性**: 高频功能需求。用户希望在创建 `todos`、`plans` 和 `memories` 时，可选存储到项目目录下（如 `.qwen/todos`），以便通过 Git 进行版本控制和跨设备同步。此功能是实现团队协作的基础。
    - **链接**: [Issue #5836](https://github.com/QwenLM/qwen-code/issues/5836)

5. **[#5838] 允许用户调整 Agent 启动命令的超时时间**
    - **重要性**: 用户体验优化。部分用户执行耗时较长的 shell 命令时，遭遇超时失败，希望能自定义超时时间以适应不同场景。
    - **链接**: [Issue #5838](https://github.com/QwenLM/qwen-code/issues/5838)

6. **[#5756] 默认 8K 输出上限导致大文件输出被截断，引发失败重试循环**
    - **重要性**: 经典的“先有 Bug 后有修复”的案例。该 Issue 指出默认输出 Token 上限（8K）远低于模型实际能力，导致生成大文件时频繁触发截断、重试的恶性循环，严重影响工作效率。
    - **链接**: [Issue #5756](https://github.com/QwenLM/qwen-code/issues/5756)

7. **[#5626] 提案：通过 Daemon + WebUI 架构重振 Chrome 扩展**
    - **重要性**: 对于浏览器集成感兴趣的开发者值得关注。该提案旨在重新设计和实现 Chrome 扩展，使其更稳定、更易于维护，并解锁更多浏览器自动化能力。
    - **链接**: [Issue #5626](https://github.com/QwenLM/qwen-code/issues/5626)

8. **[#5932] 潜在的编辑重试工具使用循环修复**
    - **重要性**: Agent 稳定性的关键 Bug。用户观察到一个 Agent 在成功编辑第一个文件后，由于某种原因在编辑第二个文件时陷入失败-重试的死循环，导致无法完成目标任务。
    - **链接**: [Issue #5932](https://github.com/QwenLM/qwen-code/issues/5932)

9. **[#5941] 大模型输出时滚动鼠标滚轮会直接跳转到最上方**
    - **重要性**: 影响阅读体验的 UI Bug。用户在模型持续流式输出内容时，稍微向上滚动滚轮，内容会突然跳到最顶部，打断阅读流。
    - **链接**: [Issue #5941](https://github.com/QwenLM/qwen-code/issues/5941)

10. **[#5922] cua-driver.exe 在空闲时仍保持高 CPU 占用**
    - **重要性**: 资源浪费问题。Windows 平台上的 `cua-driver.exe`（用于计算机操作）在 Agent 任务完成后仍持续高占用 CPU，占用系统资源。
    - **链接**: [Issue #5922](https://github.com/QwenLM/qwen-code/issues/5922)

---

## 重要 PR 进展 (10条)

1. **[#5934] fix(core): 停止因截断导致的 write_file/edit 重试循环**
    - **重要性**: 针对 **#5756** 问题的关键修复。该 PR 通过两层次修复：1) 将默认输出上限提升至模型声明的实际上限；2) 为截断场景添加主动中断保护，从根本上解决了大文件生成的重试死循环问题。
    - **链接**: [PR #5934](https://github.com/QwenLM/qwen-code/pull/5934)

2. **[#5868] feat(core): 添加可配置的自动压缩阈值和停止钩子中的上下文使用**
    - **重要性**: 智能上下文管理。允许用户自定义当上下文使用率达到多少时自动进行压缩，并可配置在特定 Hook 中停止使用上下文，为高级用户提供了更精细的 Token 控制能力。
    - **链接**: [PR #5868](https://github.com/QwenLM/qwen-code/pull/5868)

3. **[#5890] feat(loop): 注入 .qwen/loop.md 任务文件**
    - **重要性**: 解决 **#5823** 和 **#5889** 问题。为 `/loop` 命令引入了持久化的任务文件，用户可以直接编辑 `.qwen/loop.md` 来修改任务指令，而无需重启循环，极大地提升了长时任务的可用性。
    - **链接**: [PR #5890](https://github.com/QwenLM/qwen-code/pull/5890)

4. **[#5795] feat(core): 丰富子代理崩溃通知，包含部分结果和近期活动**
    - **重要性**: Agent 的调试和可观测性增强。当子 Agent 崩溃时，不再只返回“崩溃”信息，而是附带其已完成的部分工作结果和近期活动日志，帮助用户快速定位问题并抢救工作成果。
    - **链接**: [PR #5795](https://github.com/QwenLM/qwen-code/pull/5795)

5. **[#5888] feat(channels): qwen tag — RFC + Phase 0 (多人频道驻留 Agent)**
    - **重要性**: 团队协作的重大功能。提出并初步实现了“qwen tag”，即一个可以常驻在聊天群组（如钉钉）中的多人 Agent，标志着 Qwen Code 从单人工具向团队协作平台演进的重要一步。
    - **链接**: [PR #5888](https://github.com/QwenLM/qwen-code/pull/5888)

6. **[#5848] feat(ui): 添加 ui.history.collapsePreviewCount 设置**
    - **重要性**: 会话恢复的体验优化。允许用户在恢复折叠的会话时，保留最近 N 轮对话可见，其余部分折叠起来，既保留了上下文，又避免了信息过载。
    - **链接**: [PR #5848](https://github.com/QwenLM/qwen-code/pull/5848)

7. **[#5944] fix(core): 阻止重复的 Shell 检查变体**
    - **重要性**: 提升 Agent 执行效率的重要修复。当模型陷入循环调用 `git status` / `git diff` 等相似只读命令时，该 PR 添加的循环守卫将主动终止执行，避免无限循环。
    - **链接**: [PR #5944](https://github.com/QwenLM/qwen-code/pull/5944)

8. **[#5928] feat(config): 添加 todosDirectory 设置以实现项目级 Todo 持久化**
    - **重要性**: 解决 **#5836** 的核心需求。新增 `todosDirectory` 配置项，允许用户将任务清单保存到项目本地目录（如 `.qwen/todos`），使其可以被 Git 追踪，实现跨设备同步。
    - **链接**: [PR #5928](https://github.com/QwenLM/qwen-code/pull/5928)

9. **[#5852] feat(daemon, sdk): 可恢复的 /acp 会话流 (Last-Event-ID)**
    - **重要性**: 提升通信稳定性的基础设施级增强。为 daemon 的 ACP 会话事件流添加了标准 SSE 的 `Last-Event-ID` 功能，使得客户端断线重连后可以无缝恢复历史事件流，而非从头开始。
    - **链接**: [PR #5852](https://github.com/QwenLM/qwen-code/pull/5852)

10. **[#5943] feat(web-shell): 添加错误边界防止渲染崩溃导致白屏**
    - **重要性**: Web Shell 稳定性的基础保障。通过添加多层 React Error Boundaries，确保 Web Shell 中某个组件渲染失败不会导致整个应用白屏，使错误得到优雅降级处理。
    - **链接**: [PR #5943](https://github.com/QwenLM/qwen-code/pull/5943)

---

## 功能需求趋势

社区近期最关注的几个功能方向：

1.  **Token 管理与成本优化**: 社区对 Token 的浪费和成本控制有极高敏感度。Issues (#5942, #5819, #5756, #5939) 和 PRs (#5934, #5868) 都聚焦于此，旨在解决默认限制不合理、Prompt Cache 未充分利用、模型选择失控等问题。
2.  **协程与后台任务可见性**: 用户希望对自己的自动化任务 (`/loop`, cron) 拥有更好的控制和可见性。Issues (#5823, #5889) 和 PR (#5890) 推动了持久化任务文件和任务列表可管理性等特性。
3.  **跨设备与团队协作**: 从个人开发者向团队协作工具演进的趋势明显。Issues (#5836) 和 PRs (#5888, #5928) 都在探索如何通过项目内持久化、频道驻留 Agent 等方式，实现状态同步和多人协作。
4.  **浏览器集成**: 以 Chrome 扩展为代表的浏览器集成是社区长期以来的诉求。Issue (#5626) 和 (#5936) 代表了一部分开发者希望将 Qwen Code 的能力扩展到浏览器浏览和操作场景。
5.  **Agent 行为稳定性与可调试性**: Agent 陷入循环、工具调用出错、崩溃信息不明确等问题频发。Issues (#5932) 和 PRs (#5795, #5944) 表明了社区对更稳健、更可解释的 Agent 行为的迫切需求。

---

## 开发者关注点

- **资金安全与成本控制**: **#5819** 中模型被自动切换到更高单价版本，直接暴露了配置升级过程中的重大安全隐患。开发者强烈要求增强模型选择、设置变更的感知和确认机制。
- **无用 Token 消耗**: **#5942** 中的 Prompt Cache 问题和 **#5819** 中的繁简体转换问题都会导致大量的无意义 Token 消耗，开发者呼吁更智能地管理 Token。
- **后台任务失控**: **#5823** 揭示了一个严重问题：用户对后台创建的任务既无感知也无控制能力，导致 Agent 在不知情的情况下耗尽 Token 或执行非预期操作。这是 Agent 自主性管理的重要缺陷。
- **Windows 平台的资源占用**: **#5922** 中 `cua-driver.exe` 的持续高占用是 Windows 用户的一个典型痛点，尤其是在设备性能有限的情况下。
- **会话恢复的体验**: **#5848** 相关的讨论体现了用户对“恢复历史会话”这一体验的高要求，希望能在保留必要上下文和避免信息过载之间取得平衡。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是为您生成的 2026-06-28 DeepSeek TUI 社区动态日报。

---

# DeepSeek TUI 社区动态日报 | 2026-06-28

## 📰 今日速览

今日社区动态主要集中在 **v0.8.66 版本的质量把关**上。主创贡献了大量关于 Token 优化、缓存命中率提升和代码重构的 PR，社区核心痛点的修复工作取得显著进展。同时，**插件系统**的基础架构已基本成型，为后续扩展奠定了基础。

## 🔥 社区热点 Issues

以下为过去24小时内讨论最活跃或影响最广的 10 个 Issues：

1.  **#1177: 输入缓存命中率太低了**
    - **重要性**: 用户普遍反馈项目（CodeWhale）的输入缓存命中率远低于竞品，直接导致Token消耗激增和响应变慢，是当前最核心的性能瓶颈。
    - **社区反应**: 讨论热度极高（24条评论），用户情绪较为急切，希望开发团队优先解决。
    - **链接**: [Issue #1177](https://github.com/Hmbown/CodeWhale/issues/1177)

2.  **#1120: There still seems to be some problems with cache hits**
    - **重要性**: 与#1177高度相关，从技术层面补充了缓存命中问题的细节，确认问题在 v0.8.17 中仍未完全解决，开发者正在持续排查。
    - **社区反应**: 与#1177形成追踪，表明问题未修复前会持续受到关注。
    - **链接**: [Issue #1120](https://github.com/Hmbown/CodeWhale/issues/1120)

3.  **#743: token消耗增大了很多**
    - **重要性**: 指出了 Token 消耗异常的具体表现（半天消耗4亿Token），与缓存命中问题互为表里，共同构成了当前最严重的用户体验问题。
    - **社区反应**: 用户通过数据量化了问题的严重性，要求优化交互对话信息，避免过度发送冗余上下文。
    - **链接**: [Issue #743](https://github.com/Hmbown/CodeWhale/issues/743)

4.  **#3275: CodeWhale is overly involved in making modifications...**
    - **重要性**: 一个关键的用户体验 Bug，指出 Agent 在 Plan/Agent 模式下行为混乱，会“自问自答”并执行超出用户指令的操作，严重影响对工具的控制感。
    - **社区反应**: 用户提供了详细的对话日志，直指这是对之前某次修复的回归（Regression），开发优先级较高。
    - **链接**: [Issue #3275](https://github.com/Hmbown/CodeWhale/issues/3275)

5.  **#3568: plan and agent mode mixed up YET AGAIN**
    - **重要性**: 再次强调 Plan/Agent 模式混合的问题，与 #3275 互为印证，表明这个问题反复出现，解决难度高，用户体验极差。
    - **社区反应**: 用户提供了具体实例，证明了在 Plan 模式下 Agent 模式的行为仍被触发，表达了对该问题持续存在的沮丧。
    - **链接**: [Issue #3568](https://github.com/Hmbown/CodeWhale/issues/3568)

6.  **#3205: Fleet model classes, loadout auto, and semantic route roles**
    - **重要性**: 涉及**Fleet**（工作流）组件中的核心模型选择和自动负载路由功能，是提升用户处理复杂任务能力的关键特性。
    - **社区反应**: 由主创发起，讨论了如何为不同角色/任务自动选择最佳模型，是社区关注的新功能方向。
    - **链接**: [Issue #3205](https://github.com/Hmbown/CodeWhale/issues/3205)

7.  **#3192: Put it up for agentclientprotocol/registry**
    - **重要性**: 请求将项目（CodeWhale）注册到 `agentclientprotocol` 标准协议目录中，这直接关系到 **Zed 等编辑器**能否方便地集成和使用。对扩展用户群至关重要。
    - **社区反应**: 用户积极推动生态标准，希望增强与其他工具链的互操作性。
    - **链接**: [Issue #3192](https://github.com/Hmbown/CodeWhale/issues/3192)

8.  **#3495: Adopt Moraine as CodeWhale's memory backend**
    - **重要性**: 计划采用 **Moraine** 作为长期记忆后端，将历史会话转化为可检索的记忆。这是实现 Agent 长期记忆和上下文连续性功能的核心架构变更。
    - **社区反应**: 由主创提出，是官方路线图中的重要节点，社区关注其实现和对性能的影响。
    - **链接**: [Issue #3495](https://github.com/Hmbown/CodeWhale/issues/3495)

9.  **#3638: exposed main prompt for broader use cases**
    - **重要性**: 用户提出将核心提示词（prompt）暴露出来，允许修改以用于非编程场景（如文学创作）。这代表社区对工具通用性提出了更高要求。
    - **社区反应**: 该需求已经被实现（见下方的PR #3696），体现了社区与开发者的良好互动。
    - **链接**: [Issue #3638](https://github.com/Hmbown/CodeWhale/issues/3638)

10. **#3388: Token, cache, and context discipline release gate**
    - **重要性**: 这是 v0.8.66 版本的发布“门禁”Issue，标志着上述所有 Token/缓存相关问题的修复工作已进入最终整合与验收阶段。
    - **社区反应**: 由主创创建，是对社区呼声的回应，表明开发团队已将该问题集作为硬性发布门槛。
    - **链接**: [Issue #3388](https://github.com/Hmbown/CodeWhale/issues/3388)

## 🚀 重要 PR 进展

1.  **#3699: 轻量级插件系统**
    - **重要性**: 引入了发现、注册和注入等基础架构，是构建生态的基石，让社区贡献第三方能力成为可能。
    - **链接**: [PR #3699](https://github.com/Hmbown/CodeWhale/pull/3699)

2.  **#3708: 插件清单解析与发现**
    - **重要性**: #3699 的补充，进一步细化插件系统，定义了 `plugin.toml` 标准，并内置了 `rust-toolkit` 示例。
    - **链接**: [PR #3708](https://github.com/Hmbown/CodeWhale/pull/3708)

3.  **#3696: 允许从配置目录覆盖基础提示词**
    - **重要性**: 直接解决了 Issue #3638，让用户能自定义系统提示词，使工具能应用于编程以外的场景。
    - **链接**: [PR #3696](https://github.com/Hmbown/CodeWhale/pull/3696)

4.  **#3697: 缓存最大化的上下文模式**
    - **重要性**: 实现了 Issue #528 的核心方案，通过智能缓存活跃文件内容，而非每次都重新读取，旨在极大降低 Token 消耗。
    - **链接**: [PR #3697](https://github.com/Hmbown/CodeWhale/pull/3697)

5.  **#3702: ACP 流式会话更新**
    - **重要性**: 实现 ACP（Agent Client Protocol）的流式输出，当与 Zed 等编辑器集成时，用户能实时看到 Agent 的思考过程，而非等待整个回合结束。
    - **链接**: [PR #3702](https://github.com/Hmbown/CodeWhale/pull/3702)

6.  **#3707: 添加 v0.8.66 发布账本**
    - **重要性**: 官方发布的最终检查清单和变更日志，汇总了此版本中所有关于 Token 和缓存优化的成果。标志着大版本发布在即。
    - **链接**: [PR #3707](https://github.com/Hmbown/CodeWhale/pull/3707)

7.  **#3705 & #3701 & #3703: 工具错误处理优化**
    - **重要性**: 一系列修复，针对 Agent 在面对网络或外部服务错误时，会不断重试相同失败调用的问题。增加了优雅降级和直接提供备用 URL 的能力。
    - **链接**: [PR #3705](https://github.com/Hmbown/CodeWhale/pull/3705), [#3701](https://github.com/Hmbown/CodeWhale/pull/3701), [#3703](https://github.com/Hmbown/CodeWhale/pull/3703)

8.  **#3706: 命令边界重构（Layer 4.2）**
    - **重要性**: 持续的大型重构项目，旨在理清命令和 Agent 执行的边界。此层进行了最后的清理、文档和验证工作，为后续功能开发扫清障碍。
    - **链接**: [PR #3706](https://github.com/Hmbown/CodeWhale/pull/3706)

9.  **#3607: 重新激活过期 Issue 清理**
    - **重要性**: 改善项目管理，通过自动化流程关闭长期未更新的 Bug 和需求，保持 Issue 看板整洁，降低维护成本。
    - **链接**: [PR #3607](https://github.com/Hmbown/CodeWhale/pull/3607)

10. **#3704: CI 优化**
    - **重要性**: 优化了 CI 流程，确保对文档或工作流等轻量 PR 也能自动运行必要的检查，避免合入门槛过高，提升协作效率。
    - **链接**: [PR #3704](https://github.com/Hmbown/CodeWhale/pull/3704)

## 🧭 功能需求趋势

从近期 Issues 中可以提炼出社区的三大关注方向：

1.  **性能优化是首要任务**: **Token 消耗**和**缓存命中率**是目前压倒性的焦点。所有关于“Token 太大”、“响应太慢”、“缓存打不中”的讨论都高度集中，社区对减少成本、提高效率的需求空前迫切。
2.  **生态集成与标准遵守**: 社区不再满足于独立工具，而是希望它深度嵌入到 **Zed 等现代编辑器的 Agent 工作流**中。推动其注册到 `agentclientprotocol` 标准目录是这一趋势的典型表现。
3.  **Agent 行为的可控制性**: 用户强烈要求 Agent 的行为更“听话”。`Plan/Agent 模式混合`、`Agent擅自执行超范围操作`、`失败工具调用无法自动切换`等几个高频 Bug 都指向了同一个需求：让 Agent 的行为更可预测、更可控。

## 💡 开发者关注点

开发者（尤其是社区贡献者和重度用户）反馈出的核心痛点和高频需求包括：

*   **Token 成本过高**: 这是目前开发者最关心、也是抱怨最多的点。用户希望能在**功能不降级**的前提下，大幅降低每次交互的 Token 消耗。
*   **缓存效率低下**: 与 Token 消耗直接相关。开发者期望缓存机制更智能，能像竞品一样达到 95%+ 的命中率，从而显著降低 API 调用成本并提升响应速度。
*   **Agent 模式混乱**: `plan`和`agent`模式的边界模糊，导致 Agent 执行与用户意图不符的操作。这是用户对 Agent 信任度的巨大打击，需要优先修复。
*   **Prompt 的可定制性**: 部分高级用户希望修改系统提示词来适配非编程任务，这要求项目将原先硬编码的 Prompt 开放为可配置文件。

这些反馈表明，开发者社区正处于从“寻求新功能”到“要求高质量和可靠性”的转折点上。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*