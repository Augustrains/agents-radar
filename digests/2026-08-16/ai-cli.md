# AI CLI 工具社区动态日报 2026-08-16

> 生成时间: 2026-08-16 00:31 UTC | 覆盖工具: 9 个

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

**报告日期：** 2026-08-16
**分析范围：** Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI


## 1. 生态全景

当前 AI CLI 工具赛道已全面进入"**平台化与工程质量攻坚期**"。头部工具（Claude Code、Codex、Gemini CLI）不再以功能堆叠为主，而将重心转向 TUI 交互精细化、会话恢复可靠性、Agent 子代理稳定性等深度体验问题；同时，**Windows 平台稳定性**（Codex 系统级卡顿、Claude Code GPU 崩溃）与**磁盘空间失控**（Codex Crashpad 每天 5GB+）正成为跨工具的通病。安全与信任议题（SSRF 漏洞、token 配额缩水争议、安全策略误报）开始主导社区情绪，而"记忆系统"与"上下文管理"则是所有工具用户共同的高频诉求。


## 2. 各工具活跃度对比

基于各工具日报数据，整理如下（统计窗口：2026-08-15 至 08-16）：

| 工具 | 新增/活跃 Issues | 新 PRs | 版本发布 | 社区热度 TOP Issue | 重点关注领域 |
|------|:---:|:---:|:---:|:---:|------|
| **Claude Code** | ~12 (含历史高票) | 2-3 | 无 | #13354 会话自动延续 (197👍) | TUI 交互、Windows 稳定性、认证回归 |
| **OpenAI Codex** | ~10 | 10 (全合并) | 2 (rust 0.148.0-alpha.19/20) | #20214 Windows 冻结 (85👍) | Windows 性能、磁盘膨胀、会话恢复 |
| **Gemini CLI** | ~10 | 10 (含 1 关闭) | 1 (nightly) | #21409 通用代理挂起 (8👍) | Agent 可靠性、SSRF 安全、行为评估 |
| **GitHub Copilot CLI** | ~10 | 2 | 无 | #3392 NixOS bash 故障 (9👍) | MCP OAuth 回归、平台兼容性、BYOK 缓存 |
| **Kimi Code CLI** | 4-5 | 2 | 无 | #1283 记忆系统 (40 评论) | 配额计费、上下文压缩、记忆系统 |
| **OpenCode** | ~10 | 10 (5 已合并) | 无 | #37790 扣款但余额不足 (14 评论) | 服务可用性、计费透明度、工作区隔离 |
| **Pi** | ~10 | 10 (7 已关闭) | 无 | #6879 压缩时机过晚 (17👍) | 压缩正确性、TUI 细节、扩展系统 |
| **Qwen Code** | ~10 | 10+ (密集) | 1 (nightly) | #9089 runner 安全隔离 (P1) | /review 加固、CI 自愈、缓存性能 |
| **DeepSeek TUI** | ~10 | 10+ | 无 (0.9.8 冲刺中) | #5316 Crate 分解 EPIC | 第三方模型接入、CI 修复、i18n |

**补充说明：** 所有工具在 24 小时内均无正式稳定版发布，仅 Codex、Gemini、Qwen 有 nightly/alpha 版本迭代，说明各团队接近或处于版本发布间隙期。


## 3. 共同关注的功能方向

### 3.1 上下文管理与会话连续性（跨 6 个工具）
| 工具 | 具体诉求 |
|------|---------|
| Claude Code | 会话限制后自动延续（#13354, 197👍）、消息队列免打断（#50246, 197👍） |
| Gemini CLI | 子代理终止原因准确上报（#22323） |
| Kimi Code CLI | 跨会话持久记忆系统（#1283, 40 评论）、配额感知的上下文压缩（#2603） |
| Pi | 压缩时机边界安全（#6879, 17👍）、扩展注入消息导致 tool_calls 邻接损坏（#8166） |
| Qwen Code | 服务端前缀缓存命中率归零（#9230） |
| Codex | 分页历史丢弃有效记录（#35746） |

### 3.2 Windows 平台稳定性（跨 4 个工具）
- **Claude Code：** GPU 致命崩溃（#80444）、反复崩溃需修复（#85199）
- **Codex：** 系统级鼠标卡顿（#38546）、空闲时全系统卡顿（#38750）、CPU 单核 90-102% 空转（#37372）
- **Pi：** WSL 登录挂起（#6187, 27 评论）、bash 工具可自杀宿主进程（#8170）
- **Copilot CLI：** Windows OOM 崩溃（#4499）

### 3.3 磁盘占用与存储管理（跨 4 个工具）
- **Codex：** Crashpad 日增 5GB+（#25921）、子代理 JSONL 永久保留（#30779）、rollout 存储失控——"三线并发"
- **Qwen Code：** 服务端缓存命中率极低导致存储/带宽浪费（#9230）
- **Pi：** 大上下文渲染触发 V8 字符串上限崩溃（#8028）
- **OpenCode：** 虚拟化时间线元素内存泄漏——单次长会话 37,500+ 游离 DOM 节点（#42825）

### 3.4 安全与信任（跨 5 个工具）
- **Claude Code：** AI 安全过滤器在合法研究场景频繁误报（多 Issue + PR #86870）
- **Gemini CLI：** web-fetch SSRF 漏洞 CVSS 8.6（#28725）、Node 20 EOL 风险（#28726）、Auto Memory 敏感信息泄露风险（#26525）
- **Qwen Code：** PAT 与不可信代码共享 runner（#9089, P1）
- **Copilot CLI：** /spawn 跨会话注入无审批门控（#4491）
- **Kimi Code CLI：** 配额缩水 3-5 倍争议（#2604）

### 3.5 模型/API 兼容层质量（跨 4 个工具）
- **Kimi：** openai_legacy 推理内容丢失（#1155）
- **Pi：** Baseten 上 DeepSeek V4 Flash 输出上限硬编码（#8146）
- **Qwen：** 前缀缓存命中率问题（#9230）
- **Copilot CLI：** BYOK 提示缓存被破坏（#4500）


## 4. 差异化定位分析

| 工具 | 定位与目标用户 | 技术路线特征 | 核心优势 | 当前最大短板 |
|------|--------------|-------------|---------|------------|
| **Claude Code** | 通用开发者 / 全栈 | 桌面端 + CLI 双模，Electron + 原生 TUI | 社区规模最大（高票 Issue 近 200👍）、功能成熟度高 | Windows 桌面端质量问题突出；高票需求长期未获回应 |
| **OpenAI Codex** | 通用开发者 / 重度 CLI 用户 | Rust 重写（分层架构清晰），桌面端 + CLI | 代码质量高、PR 合并效率高（24h 内 10 个 PR 全合并） | Windows 系统级性能问题严重；磁盘管理失控 |
| **Gemini CLI** | 通用开发者 / Agent 重度用户 | TypeScript 全栈，Agent 架构组件化 | Agent 评估体系（Evals）建设最系统化；安全修复积极 | 子代理委托稳定性问题（P1 挂起）长期未决 |
| **GitHub Copilot CLI** | GitHub 生态用户 / 企业 | 与 GitHub Actions/Codespaces 深度耦合 | GitHub 生态集成优势明显 | 回归频发（Atlassian OAuth 连续 2 次回归）；NixOS 问题 80+ 天未修复 |
| **Kimi Code CLI** | 中英文双语用户 / 订阅制用户 | Vivace 订阅 + 1M 上下文模型 | 模型上下文窗口大、中文社区活跃 | 配额计费透明度低；记忆系统尚无时间表 |
| **OpenCode** | 开源社区 / 自托管用户 | Go 后端 + Web 前端，强调自托管 | 服务端会话管理、V2 架构演进积极（每会话预算、Docker/Incus 工作区隔离） | 服务可用性不稳定；付费用户信任危机 |
| **Pi** | 技术专家 / 早期采用者 | Rust 全栈，单一二进制分发 | 压缩逻辑最精细、扩展系统设计前沿 | 规模小、生态尚未成型；模型覆盖有限 |
| **Qwen Code** | 中文开发者 / 阿里云生态 | TypeScript + 阿里云 DSW/EAS 深度集成 | /review 与 autofix 自动化程度高；CI 工程质量门禁严格 | 中文输入法兼容问题长期未修；长时运行 OOM |
| **DeepSeek TUI** | 开源社区 / 自托管用户 | Rust 原生 TUI，单体仓库（Crate 拆分中） | 界面轻量、bwrap 沙箱、第三方模型接入持续增强 | Web UI 损坏（P0）；版本尚未到 1.0，稳定性不足 |


## 5. 社区热度与成熟度评估

### 高活跃度 · 高速迭代期
- **OpenAI Codex：** PR 合并速度之快（24h 内 10 个全部合入）表明团队处于高强度开发状态。社区反馈渠道畅通，问题响应相对及时。⚠️ 但 Windows 性能问题（85👍 最高票 Issue）长期未解决，显示*响应速度快但关键问题解决慢*。
- **Qwen Code：** @wenshao 单人贡献 10+ 个 review 相关 issue/PR，且集中于同一功能模块，说明团队正在集中攻坚 /review 体系。全部 smoke 测试（SWE-bench 500 + Terminal-Bench 89 例）通过显示质量门禁严格。

### 中等活跃度 · 稳定演进期
- **Claude Code：** 社区体量最大（两个 197👍 的长期 Issue），但官方响应滞后——连续两天无新版本、高票 Issue 8 个月未获回应。**社区热情与官方反馈速度形成反差**。
- **Gemini CLI：** 活跃度稳定，大量行为评估 PR 显示团队正在建立量化质量体系，但 P1 级 Issue（#21409 等）数月未关闭。
- **OpenCode：** 社区情绪波动大（付费信任危机），服务稳定性是当前焦点。V2 架构功能推进快（每会话预算、工作区隔离），但服务端基础设施是短板。

### 低活跃度 · 早期阶段
- **Pi：** 社区小但讨论质量高（如 #4949 翻译之争持续 3 周 17 条评论），技术深度强，处于从"技术验证"走向"产品化"的过渡期。
- **DeepSeek TUI：** 处于 0.9.8 发布冲刺期，多为内部 CI 修复和功能收尾。社区有明确的技术方向（如 crate 分解、沙箱增强），但 Web UI 损坏（P0）暴露了资源有限的现实。

### 特殊观察
- **Copilot CLI：** 版本迭代稳（1.0.x 稳定线），但 Atlassian OAuth 连续两个版本回归（1.0.79/1.0.80）和 NixOS 问题 80+ 天未修复，显示质量保障体系存在薄弱环节。
- **Kimi Code CLI：** 功能更新节奏不快，但**配额争议是本次分析中唯一"用户通过 wire-level 数据指控官方计量失实"的事件**，信任问题值得最高关注。


## 6. 值得关注的趋势信号

### 🔴 信号一：Agent 的"真实性"与"可观测性"正成为核心竞争力
Gemini CLI 的子代理误报成功（#22323）、Claude Code 的安全过滤器误报、Kimi 的配额缩水争议，本质是同一个问题：**用户对 Agent 行为和计费失去了信任**。开发者正从"能用就行"转向"可验证才用"。Qwen 的 /review 自动化和 Gemini 的行为评估（Evals）建设，代表了两条不同的解决路径——前者用自动化评审约束代码质量，后者用系统化测试约束模型行为。**对开发者的启示：** 选择 AI CLI 工具时，建议优先关注其对"失败状态"的透明度和可调试性，而非只关注功能广度。

### 🟡 信号二：上下文窗口军备竞赛的"副作用"开始显现
Kimi 的 1M 上下文窗口（#2603）、Claude 的会话延续诉求（#13354）、Codex 的分页历史（#35746），共同指向一个矛盾：**模型窗口越大，工具层的上下文管理和成本控制越复杂**。Kimi 用户指出——模型窗口 1M 时压缩几乎永不触发，导致订阅配额被快速耗尽。Pi 的压缩边界安全修复（#8153/#8164）和 Codex 的分页历史修复（#38774）代表了工具层正在"补课"。**对开发者的启示：** 即便使用大窗口模型，也应关注工具的压缩/预算策略是否可配置，避免"窗口大但成本失控"。

### 🟡 信号三：用户开始用"工程化手段"监督 AI 工具厂商
Kimi 用户通过 wire-level JSONL 日志指控配额缩水（#2604）、Claude Code 社区对 TUI 交互的精细化要求（滚动条、消息队列）、Copilot CLI 用户对 BYOK 缓存效率的经济性计算（#4500）——**开发者正在以对待基础设施软件的成熟度来要求 AI CLI 工具**。这不是坏信号，但意味着工具厂商需要更透明的计量、更可预测的升级行为（避免静默降级、静默回归）。**对开发者的启示：** 对于生产环境依赖的 AI CLI，建议建立自己的基准测试集（如记录关键场景的 token 消耗和成功率的基线），以客观监控工具变更带来的影响。

### 🟢 信号四：沙箱与安全隔离正在从"可选项"变为"必选项"
Gemini 的 SSRF 修复（CVSS 8.6）、Qwen 的 runner 隔离诉求（P1）、Pi 的 bash 工具可杀死宿主进程（#8170）、OpenCode 的 Docker/Incus 工作区蓝图——安全不再只是"防 prompt injection"，而是**物理/系统级的隔离需求**。特别是 Copilot CLI 的 `/spawn` 跨会话注入问题（#4491），说明安全问题已渗透到会话管理层面。**对开发者的启示：** 在评估 AI CLI 时，建议将沙箱能力（尤其是子代理和 bash 执行）作为核心安全评估项，而非附加功能。

### 🟢 信号五：中文开发者群体正在成为重要力量
Kimi 的中文 Issue（#1478）、Qwen 的中文输入法失效问题（#5966，已 50 天未修复）、DeepSeek TUI 的宪章/宪法翻译之争（三周 17 条评论）——中文用户体验问题从"个别反馈"走向"系统性的社区诉求"。**对开发者的启示：** 中文社区的活跃度正在上升，中文本地化与中文输入法兼容性应被视为基础质量指标。

### ⚪ 信号六：TUI 交互正在经历"精细化"升级
Claude Code 的滚动条（#62929）、Pi 的光标闪烁修复（#8155）、DeepSeek TUI 的宽终端适配（#5322）、Codex 的启动状态展示（#38788）——TUI 不再是"能用就好"，而是向**原生 IDE 的交互质量看齐**。这与终端 UI 在 AI 时代的重新定位有关：开发者长时间在 TUI 中与 Agent 协作，交互细节直接决定疲劳度和效率。**对开发者的启示：** TUI 交互质量（而非仅仅功能数量）应作为工具选型的重要参考维度。


## 总结

AI CLI 工具赛道正处于**从"功能竞争"转向"质量与信任竞争"**的拐点。平台稳定性（尤其 Windows）、会话可靠性、成本透明度是当前所有工具共同的薄弱环节，也将是下一阶段差异化竞争的核心战场。对技术决策者而言，建议根据团队的平台分布（Windows 占比越高越需谨慎评估 Codex 和 Claude Code）、对成本透明度的敏感度（Kimi 用户需关注配额变化）、以及对安全隔离的要求（Gemini 和 Qwen 在安全修复上更为积极）来综合选型。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截至**: 2026-08-16 | **数据源**: github.com/anthropics/skills


## 一、热门 Skills 排行

### 1. skill-creator 修复 — run_eval.py 评估体系全面修复
**PR #1298** | 作者: MartinCajiao | 状态: Open | 创建: 2026-06-10

- **功能**: 系统性修复 `run_eval.py` 及其下游脚本（`run_loop.py`、`improve_description.py`）的评估信号失真问题——所有 skill 描述均被报告为 0% recall，导致描述优化循环在噪声上优化
- **社区讨论热点**: 关联 issue #556（12 条评论）与 #1169，超过 10 次独立复现，是当前生态中影响面最广的 bug
- **关注度**: 社区评价最高、关联 issue 最多的 PR 之一（[链接](https://github.com/anthropics/skills/pull/1298)）

### 2. 安全信任边界问题 — 社区技能滥用 anthropic/ 命名空间
**Issue #492** | 作者: aliksir | 状态: Open | 评论: 43 | 👍: 2

- **功能**: 非官方社区技能被分发在 `anthropic/` 命名空间下，伪装成官方 Anthropic Skills，用户可能向非官方技能授予过高权限
- **社区讨论热点**: 43 条评论为全仓库最高，触及信任边界、供应链安全、权限授予机制等根本性问题
- **状态**: 仍为 Open，讨论活跃（[链接](https://github.com/anthropics/skills/issues/492)）

### 3. document-typography — 生成文档排版质量控制
**PR #514** | 作者: PGTBoos | 状态: Open | 创建: 2026-03-04

- **功能**: 解决 AI 生成文档的常见排版问题：孤字换行（1-6 个单词溢出到下一行）、寡行段落（节标题孤立在页底）、编号错位
- **社区讨论热点**: "这些问题影响 Claude 生成的每一份文档，用户很少主动要求好的排版"——精准击中文档生成痛点
- **状态**: Open（[链接](https://github.com/anthropics/skills/pull/514)）

### 4. self-audit — 输出交付前机械验证 + 四维推理质量门禁
**PR #1367** | 作者: YuhaoLin2005 | 状态: Open | 创建: 2026-06-28

- **功能**: 在 AI 输出交付前执行审计——先做机械性文件验证（确认每个声称输出的文件真实存在），再按损害严重性优先级进行四维推理审计。声称通用、不依赖具体项目/技术栈/模型
- **社区讨论热点**: 配套 proposal issue #1385（4 条评论），提出的三阶段流水线（任务前校准→对抗性审查→交付验证）展示了系统化思路
- **状态**: Open（[链接](https://github.com/anthropics/skills/pull/1367)）

### 5. ServiceNow 平台技能 — 全平台覆盖
**PR #568** | 作者: Vanka07 | 状态: Open | 创建: 2026-03-08

- **功能**: 广泛的 ServiceNow 平台助手而非狭义的脚本工具，覆盖 ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD/CSM、SPM/PPM、漏洞响应、安全事件响应、IntegrationHub 等
- **社区讨论热点**: 企业级平台技能的标杆，更新于 2026-08-12 仍在活跃迭代
- **状态**: Open（[链接](https://github.com/anthropics/skills/pull/568)）

### 6. skill-quality-analyzer & skill-security-analyzer — 元技能双件套
**PR #83** | 作者: eovidiu | 状态: Open | 创建: 2025-11-06

- **功能**: 为 Claude Skills 提供质量分析与安全审计两个元技能。质量分析覆盖结构/文档（20%）、SKILL.md 质量、示例、资源引用等五个维度
- **社区讨论热点**: 与 #492 安全议题形成互补——社区在自发建设技能质量的保障工具
- **状态**: Open（[链接](https://github.com/anthropics/skills/pull/83)）

### 7. ODT 技能 — OpenDocument 全流程处理
**PR #486** | 作者: GitHubNewbie0 | 状态: Open | 创建: 2026-03-01

- **功能**: 创建、填充、读取、转换 OpenDocument 格式（.odt、.ods），触及 ODT/ODS/ODF 关键词均自动触发。弥补了生态中除 docx 外办公文档格式的空白
- **社区讨论热点**: 办公文档生态的自然延伸（与 docx、pdf 技能形成互补）
- **状态**: Open（[链接](https://github.com/anthropics/skills/pull/486)）


## 二、社区需求趋势

**1. 安全与信任（最强烈信号）** — Issue #492 以 43 条评论断层领先，直指命名空间滥用与权限信任问题。社区对**技能供应链安全**的焦虑已成最集中的诉求。

**2. 企业级组织能力** — Issue #228（16 条评论, 8 个 👍 为最高）要求**组织内技能直接共享**，当前需手动下载、IM 传输、再手动上传的流程严重阻碍团队协作。此外 ServiceNow（#568）、SharePoint Online 安全设计咨询（#1175）均指向企业场景需求。

**3. 开发者工具链质量** — Issue #556（12 条评论, 7 个 👍）与 #1169 共同暴露 **`run_eval.py` 评估工具全线失灵的严重 bug**，直接打击社区开发者的验证信心。

**4. 元技能/质量治理** — #202（skill-creator 应更新为最佳实践）、#412（agent-governance 技能提案）、#1385（推理质量门禁管道）构成一组"治理层"需求。

**5. 上下文窗口管理** — Issue #1487 报告 claude-api 技能单次调用注入 ~156k tokens 直接耗尽上下文，这是**技能设计对资源消耗缺乏约束**的典型例证。


## 三、高潜力待合并 Skills（Open 状态）

| PR | Skill | 亮点 | 距今时间 |
|---|---|---|---|
| [#1538](https://github.com/anthropics/skills/pull/1538) | 修复两个技能使其符合 Agent Skills 规范 | 修复仓库自身参考实现中的规范违规 | 2026-08-09，仅 7 天 |
| [#1479](https://github.com/anthropics/skills/pull/1479) | plan-file-hygiene | 解决规划产物无生命周期的管理空白 | 2026-07-25，迭代中 |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit | 机械验证+四维推理审计，通用性强 | 2026-06-28，持续活跃 |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow | 企业级平台全场景技能 | 2026-03-08 至今仍在更新 |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel 复古游戏开发 | 绑定 pyxel-mcp，创意场景的独特定位 | 2026-03-05，更新于 07-15 |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT 办公文档 | 补齐 OpenDocument 格式空白 | 2026-03-01，更新于 04-14 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 完整测试技术栈覆盖 | 2026-03-22，更新于 04-21 |


## 四、Skills 生态洞察

**社区最集中的诉求：从"技能数量扩张"转向"技能质量与安全治理"——最热 issue 是安全信任边界（43 评论），最高赞 issue 是组织级共享（8 👍），而最活跃的 PR 都是对 skill-creator 评估工具链的修复合力（#1298/#1099/#1050/#539），说明社区正在为技能开发者建设可靠的生产工具。

---

# Claude Code 社区动态日报 — 2026-08-16

## 今日速览

连续第二天无新版本发布。过去 24 小时社区讨论热度集中在三大主题：TUI/终端交互改进（会话中断与消息队列）、Windows 桌面端稳定性问题（GPU 崩溃与登录认证异常）、以及 AI 安全策略误报事件。一个特别值得注意的信号是，多条高赞 Issue（#13354 197👍、#50246 197👍）长期未获官方回复，社区对交互机制的改进诉求正在持续累积。新增 Issue #86986（setup-token 认证失败）暗示认证流程可能存在新回归问题。

## 版本发布

过去 24 小时无新版本发布。当前社区讨论中提及的版本包括 CLI 2.1.233 / 桌面端 1.30096.5 / 2.1.229 等。

## 社区热点 Issues（Top 10）

**1. #13354 会话达到限制后自动延续** — [链接](https://github.com/anthropics/claude-code/issues/13354)
- 197 👍 · 78 评论 · 已开启 8 个月
- 社区长期高票需求：会话达到限制后应能自动延续，而非强制中断。评论持续滚动，官方尚未给出明确方案，是目前 TUI 交互改进中呼声最高的议题。

**2. #50246 消息队列模式（免打断）** — [链接](https://github.com/anthropics/claude-code/issues/50246)
- 197 👍 · 56 评论 · 4 个月前创建
- 要求增加"消息排队"模式：Claude 忙碌时可排队后续指令，而非只能打断当前任务。与 #13354 并列为 TUI 交互改进两大核心诉求，开发者普遍反映"打断-恢复"模式严重破坏工作流连续性。

**3. #80444 Windows 桌面端 fatal GPU 崩溃** — [链接](https://github.com/anthropics/claude-code/issues/80444)
- 34 评论 · 5 👍
- Windows 桌面端在应用内浏览器触发致命 GPU 崩溃（0x060C201E），崩溃后 MSIX 包完全不可启动，必须执行"修复"操作。涉及 NVIDIA RTX 2080 双驱动版本，Electron 42.7.0 环境，问题严重性较高。

**4. #85199 Windows 桌面端反复崩溃需反复修复** — [链接](https://github.com/anthropics/claude-code/issues/85199)
- 23 评论 · 4 👍
- 与 #80444 高度关联，Windows 桌面端反复崩溃、每次均需通过"高级选项→修复"恢复。社区推测与 GPU 进程或 MSIX 包状态（appxState=2）有关，Windows 平台稳定性是当前最集中的质量痛点。

**5. #86986 `setup-token` 生成的 token 被 API 拒绝** — [链接](https://github.com/anthropics/claude-code/issues/86986)
- 1 评论 · 8 月 15 日创建 · 最新
- 新报告的认证问题：`claude setup-token` 铸造的长期 token 首次请求即被拒（400 no body），但同一账号交互登录正常。本地与 CI 均可复现，影响 headless/自动化场景，疑似新回归。

**6. #86671 跨会话消息未真正入队** — [链接](https://github.com/anthropics/claude-code/issues/86671)
- 3 评论 · 1 👍 · 标记 duplicate
- 跨会话消息在目标会话显示但模型从未收到，标记为重复但影响面较大（Windows/桌面端/agents），可能涉及消息传递链路缺陷。

**7. #86982 终端失焦后推送通知不送达** — [链接](https://github.com/anthropics/claude-code/issues/86982)
- 1 评论 · 最新
- 终端窗口失焦（配合手机锁屏）时推送不送达，但 Claude 端显示已发送。影响远程控制场景，macOS/iOS 用户反馈。

**8. #87009 子代理完成通知延迟数十分钟** — [链接](https://github.com/anthropics/claude-code/issues/87009)
- 1 评论 · 8 月 15 日创建
- 进程内子代理任务完成通知延迟 30-40 分钟，即使小任务也是如此，需手动唤醒。影响 agents 工作流效率与自动化可靠性。

**9. #86362 浏览器面板阻止本地开发域名子资源** — [链接](https://github.com/anthropics/claude-code/issues/86362)
- 5 评论 · 4 👍
- 浏览器面板将 /etc/hosts 映射到 127.0.0.1 的本地开发域名子资源以 ERR_BLOCKED_BY_CLIENT 拦截，页面渲染空白。影响本地 Web 开发调试。

**10. #62929 TUI 增加可见滚动条** — [链接](https://github.com/anthropics/claude-code/issues/62929)
- 4 评论 · 7 👍
- 新渲染引擎缺乏可见滚动条与位置指示器，仅靠 PgUp/PgDn 翻页，无法感知内容长度与当前位置，影响长会话中的导航体验。

## 重要 PR 进展

**1. #84600 启用前端设计插件（已合并）** — [链接](https://github.com/anthropics/claude-code/pull/84600)
- 在项目范围注册官方 marketplace 并启用 frontend-design skill，通过 .claude/settings.json 自动加载。

**2. #86870 修复授权安全研究中的误报 CVP 状态变更** — [链接](https://github.com/anthropics/claude-code/pull/86870)
- 在 `security-guidance/hooks/review_api.py` 中增加任务上下文检查机制，扩展 `cap_diff_for_prompt()` 以识别 CVS 状态与教育实验环境，新增 `is_authorized_lab()` 标志，减少安全钩子误触发。

**3. #82981 库存自动化脚本（西班牙语提交）** — [链接](https://github.com/anthropics/claude-code/pull/82981)
- 提交内容为空，可能为不完整或测试性 PR。

## 功能需求趋势

- **TUI 交互精细化**：连续 8 个月的高票需求集中在会话延续（#13354）、消息排队（#50246）、滚动条（#62929）——社区对终端 UI 的交互效率与可控性要求显著提升，不再满足于"打断-恢复"的基础模式。
- **跨设备/跨产品状态同步**：新增 #87027（多机配置与记忆同步）与 #87028（claude.ai 与 Claude Code 记忆互通），用户期待同一账号在不同设备与不同产品间保持上下文连续。
- **Windows 平台稳定性修复**：`platform:windows` 相关问题持续累积（GPU 崩溃、安装器 PATH、认证异常），Windows 已成为质量短板，社区期待官方系统性修复而非逐个打补丁。
- **自动化/无人值守场景强化**：`setup-token`（#86986）、dontAsk 权限模式（#74567）等问题说明 headless/CI 场景的开发者比例在上升，token 生命周期管理与权限系统需要更可靠的设计。

## 开发者关注点

- **"打断-恢复"模式是最大痛点**：#13354 与 #50246 合计近 400 👍、134 条评论，社区对现有会话中断机制的不满已非常集中，且长期未获官方回应，可能成为竞品差异化的突破口。
- **AI 安全策略误报事件频发**：本周多条已关闭 Issue（#72074、#72088、#72093）显示安全过滤器在无人机固件分析、APK 逆向等合法安全研究场景中频繁误判并中断会话。虽然相关 Issue 已关闭，但 PR #86870 的出现表明社区正在尝试自行修复。
- **Windows 平台体验显著落后**：GPU 崩溃（#80444/#85199）、安装器 PATH 异常（#86999）、认证问题等集中爆发，Windows 用户在多 Issue 中表达挫败感。
- **认证与令牌管理存在新回归**：`setup-token` 令牌被 API 拒绝（#86986）影响所有 headless 用户，且与交互登录形成鲜明对比，指向 OAuth token 铸造链路可能存在缺陷。
- **本地开发环境支持不足**：/etc/hosts 域名屏蔽（#86362）、外部编辑器文本截断（#87017）等问题显示对开发者本地工作流的兼容性仍需加强。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**2026-08-16**


## 今日速览

Windows 桌面端性能问题成为今日绝对焦点，多条 Issue 直指 Codex 应用在 Windows 11 上导致系统级鼠标卡顿、CPU 空转，甚至触发内核级 watchdog。与此同时，官方在 24 小时内连续发布两个 Rust alpha 版本（0.148.0-alpha.19/20），并通过一批高密度 PR 对 TUI 状态管理、exec 历史分页、MCP 钩子引擎等核心链路进行了系统性加固。磁盘空间失控问题（数十至数百 GiB 级别）也是社区持续追问的痛点，官方已通过 `codex doctor` 存储诊断功能予以响应。


## 版本发布

过去 24 小时发布了两个 Rust 版本，均为 alpha 通道：

- **rust-v0.148.0-alpha.19** / **rust-v0.148.0-alpha.20**
  - 连续两个补丁版本，仓库未提供详细变更日志。
  - 结合近期 PR 合并节奏，推测与 exec-server 跟踪上下文传播、TUI 启动状态展示、MCP 钩子支持等近期合入代码相关。

> 链接：[Releases](https://github.com/openai/codex/releases)


## 社区热点 Issues

> 精选 10 条评论数最高的 Issue 进行解读。

**1. Codex App 在 Windows 11 Pro 上频繁冻结/卡顿（#20214）** ⭐ 104 评论 · 👍 85
- 最受关注的历史 Issue。用户反映即使在充足系统资源（Ryzen 5 5600 / 32GB RAM）下，应用仍会频繁出现界面冻结和丢帧。评论数量持续增长，说明大量 Windows 用户正在遭遇同类问题。
- 链接: https://github.com/openai/codex/issues/20214

**2. 非提权运行时引发系统级鼠标卡顿（#38546）** ⭐ 25 评论 · 👍 11
- 新近涌现的回归类问题：版本 26.810.41047 在未以管理员身份运行时会导致鼠标指针在整个系统中周期性卡顿，与 #20214 症状高度重合，但触发场景不同（普通运行 vs 冻结）。社区正在汇集两类问题是否为同一底层原因。
- 链接: https://github.com/openai/codex/issues/38546

**3. 大 sessions 目录导致打开 Codex 后系统输入冻结（#28109）** ⭐ 23 评论 · 👍 14
- 已关闭（可能已修复或定位）。症状表现为打开应用后 1-2 秒的间歇性系统输入停顿，与 sessions 目录规模相关。曾在近期桌面版更新后出现，目前状态需要确认修复版本。
- 链接: https://github.com/openai/codex/issues/28109

**4. Crashpad 崩溃转储无限膨胀：每天新增 5GB+（#25921）** ⭐ 17 评论 · 👍 8
- macOS 上 Codex Desktop 在 `~/Library/.../Crashpad/pending` 下无限制生成 `.dmp` 与 `_sidecar.json` 文件。现场数据：一天内目录增至 4.9GB、54,504 个文件。属高风险磁盘耗尽类问题，影响所有长时间使用桌面版的 macOS 用户。
- 链接: https://github.com/openai/codex/issues/25921

**5. 分页历史丢弃合法 rollout 记录并重用序号（#35746）** ⭐ 13 评论
- CLI 会话恢复时的数据完整性问题：分页后的 `RolloutLine` 解码不一致，合法记录被丢弃且序号被复用，可能导致会话恢复后上下文错乱。触发链复杂，对依赖长会话的开发者影响较大。
- 链接: https://github.com/openai/codex/issues/35746

**6. 内联 base64 工具图片导致线程不可恢复（#18629）** ⭐ 12 评论
- 桌面端将含 base64 图片的工具输出内联持久化到会话历史中，累积后导致恢复时 `{"detail":"Bad Request"}` 拒绝服务，并可能虚增 token 消耗。此问题波及 computer-use 和浏览器工具用户。
- 链接: https://github.com/openai/codex/issues/18629

**7. Codex 遗留未索引 rollout 文件且缺少重建索引机制（#31433）** ⭐ 12 评论
- Windows 上部分有效 rollout 文件未被状态数据库索引，且当前没有受支持的重建索引命令，用户无法自助修复会话历史。对依赖本地会话记录的开发者是功能性阻断。
- 链接: https://github.com/openai/codex/issues/31433

**8. [Windows] 空闲时系统级卡顿，退出应用立即恢复（#38750）** ⭐ 9 评论 · 新建于 8/15
- 最新报告：即使在无任何活跃 Codex 任务时，应用保持打开也会引发全系统卡顿。完全退出 Codex 后系统响应立即恢复。这个“空闲即卡顿”的特征缩小了排查范围，指向某个后台定时任务或轮询循环。
- 链接: https://github.com/openai/codex/issues/38750

**9. 重复 MCP 任务单元累积；进程树终止遗漏孙进程（#34614）** ⭐ 9 评论
- Windows 上每次会话都会累积重复的 MCP 套件（suite），且终止时不会清理 `cmd.exe`/`node.exe` 孙进程。仓库内已有 Job Object 方案但 MCP 派生路径未使用，修复方向已明确。
- 链接: https://github.com/openai/codex/issues/34614

**10. 子代理 fork 会话永久保留大 JSONL 历史，~/.codex 磁盘膨胀（#30779）** ⭐ 5 评论
- 每次 subagent fork 都会产生独立的完整 JSONL 历史且永不过期，长期使用导致 `~/.codex` 体积膨胀至 GiB 级。与 #25921（Crashpad）和 #34337（rollout 存储）共同构成“磁盘空间失控”三重奏。
- 链接: https://github.com/openai/codex/issues/30779


## 重要 PR 进展

**1. 添加存储诊断至 `codex doctor`（#38795）** ✅ 已合并
- 检查 `CODEX_HOME` 与工作区剩余空间（<5GiB 警告、<1GiB 报错），Windows 上还会检测 Git 工作区是否位于受信任的 Dev Drive。
- 链接: https://github.com/openai/codex/pull/38795

**2. TUI 启动时展示恢复/分叉状态（#38788）** ✅ 已合并
- 启动时在编辑器上方以暗色显示 `Resuming session…` 或 `Forking session…`，避免用户误以为卡死；选择完成后自动清除。
- 链接: https://github.com/openai/codex/pull/38788

**3. 活跃轮次模型设置跨更新保持稳定（#38785）** ✅ 已合并
- 阻止线程设置（如模型切换）在单轮对话中途生效，避免采样请求之间模型配置不一致导致的行为漂移。
- 链接: https://github.com/openai/codex/pull/38785

**4. 持久化 exec 线程改用分页历史（#38774）** ✅ 已合并
- `codex exec` 启动持久会话时请求分页历史；临时线程保持原逻辑，若线程存储不支持分页则回退到传统历史读取。直指 #35746 的数据完整性问题。
- 链接: https://github.com/openai/codex/pull/38774

**5. MCP 工具处理器接入 hooks 引擎（#38705）** ✅ 已合并
- 支持同步 `mcp_tool` 钩子处理器，通过 executor 调用指定 MCP 服务器与工具；MCP 工具输入中嵌套的钩子事件占位符会展开，同时保留 JSON 类型。
- 链接: https://github.com/openai/codex/pull/38705

**6. 插件变更后刷新钩子运行时（#38703）** ✅ 已合并
- 当生效插件变更或 marketplace 升级安装新插件内容后，重建已加载会话的钩子运行时，同步刷新插件与 MCP 相关缓存。
- 链接: https://github.com/openai/codex/pull/38703

**7. 通过共享 Guardian 审批路由权限请求（#38701）** ✅ 已合并
- `request_permissions` 调用统一转换为 Guardian 权限审批请求，走公共审批路径；自动权限审查期间保留轮次取消能力，简化权限审批链路。
- 链接: https://github.com/openai/codex/pull/38701

**8. exec-server 中继间传播请求追踪上下文（#38690）** ✅ 已合并
- 中继帧新增可选 W3C `traceparent`/`tracestate` 字段，JSON-RPC 请求的追踪上下文会被复制到数据帧上；跨 Noise 记录分片的加密请求也能正确传递。
- 链接: https://github.com/openai/codex/pull/38690

**9. 对齐违规以类型化错误呈现（#38682）** ✅ 已合并
- 识别响应流中的 `misalignment_policy_violation` 错误以及 HTTP 400/403 响应，保留上游消息并标记为不可重试，并对外暴露 `misalignment_policy_violation` 字段。
- 链接: https://github.com/openai/codex/pull/38682

**10. 委派会话保留 HTTP 回退（#38681）** ✅ 已合并
- WebSocket 回退是会话级作用域。若父会话已切换至 HTTP，则委派会话不再尝试新的 WebSocket 连接，保持传输方式一致。
- 链接: https://github.com/openai/codex/pull/38681


## 功能需求趋势

- **会话作用域隔离**（#3550）：将 Codex 聊天记录按 VS Code 项目/工作区隔离，已成为 34 评论、79 👍 的高票需求。社区对“全局聊天列表”导致跨项目混淆的体验普遍不满。
- **磁盘占用控制**：来自多个方向的诉求——Crashpad 转储上限、子代理历史保留策略、rollout 存储上限——共同指向“本地存储需要配额与清理策略”这一核心需求。
- **显式缓存控制**（#37674）：AWS Bedrock 原生 Codex 请求无法为 GPT-5.6 Sol 开启显式提示缓存，产生大量 cache-write token 费用，用户期待 API 层暴露缓存控制选项。
- **Windows 性能/稳定性**：虽然以 bug 形式呈现，但高频出现表明社区对 Windows 桌面端体验有明确期待——包括空闲资源占用、输入响应、进程清理三个方面。
- **远程连接控制**（#35351）：macOS 桌面端远程控制状态更新失败的问题已持续 3 周，Pro/企业用户在等待更可靠的远程连接体验。


## 开发者关注点

1. **Windows 系统级卡顿已成最高优先级问题**。多条 Issue 报告应用空闲时即导致鼠标指针/系统输入周期性停顿（#38546、#38750），且与 CPU 占用（#37372：90-102% 单核空转）和时间点（8 月 15 日更新后 #38719）高度相关。社区已有用户通过完全退出应用恢复系统响应，建议 Windows 用户暂避高频更新或关注回滚方案。

2. **磁盘空间无限增长问题呈“三线并发”态势**。Crashpad 转储（macOS，每天 5GB+）、子代理 JSONL 历史（~/.codex 膨胀）、rollout 存储（数十至数百 GiB）同时被不同用户报告。`codex doctor` 存储诊断（#38795）已合入，但自动清理/配额机制仍悬而未决。

3. **macOS 端 Computer Use 服务失控（#38760、#38769、#38771）**。26.810.52044 构建中 `SkyComputerUseService` 以每秒 5-8 个进程的速率被反复派生，导致系统卡顿、OOM 崩溃乃至内核级 watchdog 干预（macOS 26.5），且用户已确认在禁用 Computer Use 的情况下仍会触发，属高优先级回归。

4. **会话恢复可靠性是 CLI 核心痛点**。分页历史丢失记录（#35746）与 base64 工具图片阻塞线程恢复（#18629）都直接影响重度 CLI 用户的工作流。官方已通过 #38774（分页历史 + 回退）和持续修复做出响应，但长期方案仍需观察。

5. **社区对官方响应速度有明确期待**。多条高赞 Issue 数周未获官方评论（如 #20214、#25921），而文档明确的修复建议（如 #34614 中“Job Object 已存在但未使用”）等待时间较长。开发者在评论中普遍表达了希望官方加速 Windows 端性能问题响应周期的意愿。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-16** | 数据来源：github.com/google-gemini/gemini-cli

---

## 今日速览

今日社区动态聚焦于 **Agent 子代理可靠性** 与 **安全加固** 两大主线。最值得关注的是针对 #22323（子代理达到 MAX_TURNS 后误报成功）的修复 PR 已提交，以及多个针对 SSRF 漏洞和 Node 20 EOL 的安全 PR 更新。功能需求方面，社区持续强烈呼吁提升子代理的自主执行能力、上下文感知能力和行为可观测性。

---

## 版本发布

### v0.56.0-nightly.20260815.g2a87e7be1

- **更新内容**：修复 SSR Agent 中 a2a-server 测试的 `process.env` 迁移问题（将 `process.env` 迁移至 `vi.stubEnv`）。
- **完整变更**：[查看 Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260814.gc0d192452...v0.56.0)

---

## 社区热点 Issues（Top 10）

### 1. [#22323 Subagent 达到 MAX_TURNS 后误报 GOAL 成功](https://github.com/google-gemini/gemini-cli/issues/22323)
- **标签**：P1 / Bug / Agent
- **热度**：12 条评论 | 2 👍
- **详情**：`codebase_investigator` 子代理在达到最大轮次限制、**未做任何分析**的情况下，仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了实际的中断原因。
- **为何重要**：这是严重的**可信度问题**，用户无法判断子代理是否真正完成任务。当前已有对应修复 PR #28815 提交，今日更新表明正在进行回归测试。

### 2. [#21409 通用代理（Generalist agent）挂起](https://github.com/google-gemini/gemini-cli/issues/21409)
- **标签**：P1 / Bug / Agent
- **热度**：8 条评论 | 8 👍（社区高共鸣）
- **详情**：当 Gemini CLI 将任务委托给 generalist agent 时，**永久挂起**。即使是创建文件夹这样的简单操作也会卡住，用户等待长达一小时只能取消。禁用子代理委托后问题消失。
- **为何重要**：该问题严重影响日常使用，8 个 👍 说明大量用户遇到同样问题，是当前最影响体验的 Agent 缺陷之一。

### 3. [#19873 利用模型原生 bash 能力：零依赖 OS 沙箱与意图路由](https://github.com/google-gemini/gemini-cli/issues/19873)
- **标签**：P2 / Enhancement / Agent
- **热度**：8 条评论 | 1 👍
- **详情**：提议充分利用 Gemini 3 模型原生 bash 用户训练优势（链式使用 `grep`、`cat`、`sed` 等），通过零依赖 OS 沙箱和"执行后意图路由"在**不牺牲安全性的前提下**释放模型最大效能。
- **为何重要**：社区在思考如何让模型以**最自然最高效的方式**工作，而非依赖封装好的工具，代表了 Agent 设计的一个前沿方向。

### 4. [#22745 评估 AST 感知的文件读取/搜索/映射影响](https://github.com/google-gemini/gemini-cli/issues/22745)
- **标签**：P2 / Feature / Agent
- **热度**：7 条评论 | 1 👍
- **详情**：EPIC 跟踪一系列调查，评估 AST 感知工具的价值。预期收益包括：单次调用精确读取方法边界、减少因错误对齐读取导致的轮次浪费和 token 噪音、支持精确导航到类型定义等。
- **为何重要**：直接关系到**代理效率与 token 成本**，若落地将是代码库理解能力的重大提升。

### 5. [#24353 构建稳健的组件级评估体系](https://github.com/google-gemini/gemini-cli/issues/24353)
- **标签**：P1 / Agent / Eval
- **热度**：7 条评论
- **详情**：EPIC 旨在建立组件级别的行为评估体系。目前已有 76 个行为评估测试，针对 6 个支持的 Gemini 模型版本运行。
- **为何重要**：量化评估是保证 Agent 质量、防止回归的基础设施工程，对项目长期稳定至关重要。

### 6. [#26522 Auto Memory 对低信号会话无限重试](https://github.com/google-gemini/gemini-cli/issues/26522)
- **标签**：P2 / Bug / Agent
- **热度**：5 条评论
- **详情**：Auto Memory 仅在提取代理成功调用 `read_file` 后才将会话标记为"已处理"。若代理判断会话低信号而跳过读取，会话将**永远停留在未处理状态**，被反复重新扫描，造成资源浪费。
- **为何重要**：影响后台记忆提取服务的**运行效率与稳定性**。

### 7. [#25166 Shell 命令执行完成后卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)
- **标签**：P1 / Bug / Core
- **热度**：4 条评论 | 3 👍
- **详情**：执行简单 CLI 命令后，命令已完成但 Gemini CLI 挂起，仍显示 shell 命令处于活动状态并"等待用户输入"。**极其简单的、不会等待输入的命令也会触发**。
- **为何重要**：P1 级别的 Core 功能 Bug，核心交互流程卡死，影响面广。

### 8. [#21968 Gemini 不主动使用 skills 和子代理](https://github.com/google-gemini/gemini-cli/issues/21968)
- **标签**：P2 / Bug / Agent
- **热度**：6 条评论
- **详情**：用户观察（非严谨数据）Gemini **几乎从不自主调用**自定义 skills 和子代理。即使显式提供了"gradle"、"git"等 skills 描述，模型在执行强相关任务时也不会主动使用，除非用户显式要求。
- **为何重要**：直接否定了自定义技能/子代理设计的初衷——**自主性不足**，这关系到 Agent 生态的可扩展性。

### 9. [#22232 增强 browser_agent 弹性：自动会话接管与锁恢复](https://github.com/google-gemini/gemini-cli/issues/22232)
- **标签**：P3 / Feature / Agent
- **热度**：4 条评论
- **详情**：建议改进 `BrowserManager.ts` 的"快速失败"策略。当前若浏览器配置文件被锁（如持久会话被占用），代理直接失败；期望能**自动接管或恢复会话**，增强健壮性。
- **为何重要**：浏览器自动化可靠性的关键补强，涉及 `sessionMode: 'persistent'` 等核心场景。

### 10. [#26525 Auto Memory 增加确定性脱敏并减少日志](https://github.com/google-gemini/gemini-cli/issues/26525)
- **标签**：P2 / Security / Bug
- **热度**：4 条评论
- **详情**：Auto Memory 会将本地 transcript 内容发送给后台提取模型。当前**提示词要求在上下文已进入模型后再脱敏**，且服务可能记录已有技能的敏感信息。建议在发送前进行**确定性脱敏**。
- **为何重要**：涉及**用户敏感信息的隐私边界**，安全优先级高，与 #26522、#26523 同属记忆系统质量问题系列。

---

## 重要 PR 进展（Top 10）

### 1. [#28828 预览模型被静默替换时给出警告](https://github.com/google-gemini/gemini-cli/pull/28828)
- **优先级**：P1 | 更新：08-15
- **内容**：修复 #28825。当用户请求预览模型（如 `gemini-3.1-pro-preview`）但账号无预览权限时，`Config` 会**静默降级**到 `auto-gemini-2.5`，无任何提示。此 PR 增加警告机制，提升透明度。
- **点评**：解决**用户预期与实际的落差**问题，是重要的体验修复。

### 2. [#28815 修复子代理恢复时终止原因被覆盖](https://github.com/google-gemini/gemini-cli/pull/28815)
- **优先级**：P1 | 更新：08-15
- **内容**：修复 #22323。子代理达到执行上限（如 `MAX_TURNS`、`TIMEOUT`），但在最后恢复轮次成功调用 `complete_task` 时，`LocalAgentExecutor` 会**错误地将终止原因覆盖为 GOAL**。此 PR 保留原始终止原因。
- **点评**：**今日最关键的修复**，直击误报问题的根源，维护终止原因的准确性。

### 3. [#28725 修复 web-fetch 的 SSRF 漏洞（CVSS 8.6）](https://github.com/google-gemini/gemini-cli/pull/28725)
- **优先级**：P2 | 更新：08-15
- **内容**：修复 #28555。`web-fetch` 工具存在**严重 SSRF 漏洞**，攻击者可通过指向内网/回环 IP 的自定义域名（如 `169.254.169.254`）绕过 DNS 防护。此 PR 阻止此类绕过。
- **点评**：**高价值安全修复**，阻断云元数据窃取等攻击路径（CVSS 8.6 属于高危级别）。

### 4. [#28726 沙箱 Dockerfile 升级至 node:22-slim](https://github.com/google-gemini/gemini-cli/pull/28726)
- **优先级**：P1 | 更新：08-15
- **内容**：修复 #28584。将沙箱和相关 `cloudrun` Dockerfile 从 `node:20-slim` 升级至 `node:22-slim`。Node 20 已 EOL，**不再接收安全补丁**，最近的 CVE 仅在 Node 22/24/26 修复。
- **点评**：**消除已知安全风险**的主动升级，确保运行时环境受支持。

### 5. [#28827 修复 401 子字符串导致的错误认证判断](https://github.com/google-gemini/gemini-cli/pull/28827)
- **优先级**：P2 | 更新：08-15
- **内容**：修复 #28203。防止 `isAuthenticationError` 将**包含 "401" 的无关注册号**（如端口号、退出码）误判为认证失败，改进上下文判断逻辑并补充回归测试。
- **点评**：**错误处理精确化**，避免误导性的认证错误提示。

### 6. [#28813 为 packages/cli tsconfig 添加 composite 标志](https://github.com/google-gemini/gemini-cli/pull/28813)
- **优先级**：P1 | 更新：08-15
- **内容**：修复 #21911。根级构建/类型检查因 `evals/tsconfig.json` 引用 `../packages/cli` 而失败，原因是 `packages/cli` 未配置 `"composite": true`。此 PR 补上该配置。
- **点评**：**构建基础设施修复**，解决工程化阻塞问题。

### 7. [#28824 新增多项行为评估（多工具链、上下文安全、安全边界）](https://github.com/google-gemini/gemini-cli/pull/28824)
- **更新**：08-15
- **内容**：新增三组行为评估：多工具链执行工作流、大文件的上下文安全处理、敏感文件/目录的安全边界强制。
- **点评**：**质量保障体系建设**，从评估角度确保 Agent 行为的正确性和安全性。

### 8. [#28822 新增任务规划与追踪行为评估](https://github.com/google-gemini/gemini-cli/pull/28822)
- **更新**：08-15
- **内容**：新增针对 `write_todos`、`complete_task`、`tracker_list_tasks`、`tracker_get_task` 的行为评估，验证任务规划与追踪功能。
- **点评**：与 #28823、#28824 同属**系统性补强评估覆盖**，关注 Agent 任务执行的全链路质量。

### 9. [#28823 新增依赖关系与错误恢复行为评估](https://github.com/google-gemini/gemini-cli/pull/28823)
- **更新**：08-15
- **内容**：新增针对任务图依赖（`tracker_add_dependency`）、任务图可视化（`tracker_visualize`）、文件路径 404 错误恢复、shell 命令失败恢复的行为评估。
- **点评**：专注于**错误恢复能力**的正确性验证，是 Agent 稳健性的关键评测。

### 10. [#28608 预览模型 404 时回退到稳定模型](https://github.com/google-gemini/gemini-cli/pull/28608)
- **状态**：已关闭（CLOSED）| 更新：08-15
- **内容**：修复 #28600。使用 Gemini API key 认证时，若 key 对应的项目无预览模型访问权限，通过 API key 请求 `gemini-3.1-pro-preview` 会收到 404。此 PR 在回退策略链中**增加对 404 场景的兜底**。虽然 PR 已关闭，但其解决的问题与 #28828 相关联。
- **点评**：虽已关闭，但所涉场景（预览模型降级）与 #28828 形成互补，展示了对**模型回退策略**的持续优化。

---

## 功能需求趋势

### 1. 评估体系（Evals）建设进入快车道
- 多个 PR（#28822、#28823、#28824）同时新增行为测试，覆盖任务规划、依赖管理、错误恢复、多工具链、安全边界等维度。
- **信号**：社区和团队正在系统性地建立 Agent 行为的**量化验证手段**，确保功能迭代不引入回归。

### 2. 子代理自主性仍是核心痛点
- #21968（不主动使用 skills）、#21409（generalist 挂起）、#22093（无权限运行子代理）等持续高热。
- **信号**：子代理的**调用策略、权限控制和稳定性**是当前最受关注的 Agent 能力短板。

### 3. AST 感知的代码库理解
- #22745、#22746 两个 EPIC 系列持续活跃，探索 AST 工具在精确读取、导航、映射方面的价值。
- **信号**：社区对**代码库理解效率**有更高期待，期望减少 token 消耗和轮次浪费。

### 4. 安全性成为持续关注焦点
- 除 SSRF 修复（#28725）和 Node 升级（#28726）外，还有 #26525（确定性脱敏）、#22672（阻止破坏性行为）等。
- **信号**：随着 Agent 执行能力增强，**安全边界与风险控制**的需求正日益凸显。

### 5. 可观测性与调试能力
- #22598（子代理轨迹可通过 `/chat share` 分享）、#21763（Bug 报告缺少子代理上下文）等。
- **信号**：社区希望**端到端地理解 Agent 行为**，特别是在诊断失败时，子代理的内部执行信息至关重要。

---

## 开发者关注点

### 痛点 1：错误报告与真实状态不符
- **案例**：子代理已中断（MAX_TURNS）却报告"成功"（#22323）；命令已结束却显示"等待输入"（#25166）；预览模型被静默降级无提示（#28825）。
- **呼声**：开发者需要**透明、准确的状态信息**，错误状态必须真实反映执行结果，静默降级和错误成功标识正在侵蚀用户信任。

### 痛点 2：Agent 自主性的"双刃剑"
- #21409 中，用户被迫"指示模型不要委托给子代理"才能正常使用；#21968 中，模型又"懒得"使用子代理。
- **呼声**：当前**委托策略的两极表现**（过度委托导致挂起 vs. 委托不足）表明，子代理的触发条件与执行可靠性需要更精细的设计，尤其是在**权限控制和失败恢复**层面。

### 痛点 3：安全边界是底线要求
- SSRF 漏洞（#28725）、Node 20 EOL 风险（#28726）、Auto Memory 泄密风险（#26525）在一周内同时被提出或修复。
- **呼声**：开发者对**数据安全与供应链安全**高度敏感。记忆系统在后台默默读取 transcript 的行为尤其被置于聚光灯下。

### 痛点 4：行为可预测性差
- 模型随机在任意目录创建临时脚本（#23571）、使用危险命令（#22672）、忽略 settings.json 覆盖（#22267）。
- **呼声**：开发者需要 Agent 在**文件系统操作**和**命令执行**上更恪守边界，遵守既定的配置覆盖规则。Agent 的学习和记忆行为也应当遵循明确的边界（#26522、#26523）。

---

> 💡 **分析师观点**：今日动态表明，Gemini CLI 正处于从"功能堆叠"向"质量与安全加固"的过渡期。大量 P1 级 issue 的长期存在（部分自 3 月起就没有关闭）与高频的行为评估 PR 形成鲜明对比——**测试的"纸上谈兵"正在追赶真实世界的"千疮百孔"**。对于开发团队，子代理委托的稳定性（#21409）和高危安全漏洞（#28725）应是最优先的处理对象。对于社区用户，**升级时注意模型回退行为的变化（#28828）**，并关注后续对子代理终止原因语义的调整（#28815）。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-16** | 数据来源：github.com/github/copilot-cli


## 1. 今日速览

过去 24 小时内无新版本发布，社区讨论集中在 **1.0.79/1.0.80 的 Atlassian MCP OAuth 回归**（#4480、#4490）——该问题在 1.0.71 正常、1.0.78 正常，却在 1.0.79/1.0.80 连续回归，且 #4480 标记为已关闭但 #4490 再次复现，表明修复可能不彻底。此外，长期存在的 **NixOS 上 Bash 工具故障**（#3392，已超 80 天未修复）继续获得关注。PR 方面重点在于仓库自身的自动化安全治理（#4449、#4497）。与此同时，新增多个涉及 BYOK 提示缓存、V8 堆内存崩溃等深度技术问题的 Issue，值得关注。


## 2. 版本发布

过去 24 小时内无新版本发布。当前最新版本为 1.0.80。社区中多个 Issue 引用 1.0.79/1.0.80 的比较，建议相关用户关注版本间行为差异。


## 3. 社区热点 Issues（10 个）

### 🔥 高热度 / 高影响

**1. Atlassian MCP OAuth 失败：1.0.80 中再次回归（RFC 8414 §3.3）** — #4490
- **重要性**：与 #4480 相同问题在 1.0.80 中再次出现（#4480 已关闭但问题未彻底解决），影响所有使用 Atlassian 远程 MCP 服务器的用户，阻断 OAuth 认证流程。
- **社区反应**：用户明确指出 "worked in 1.0.78"，强烈期待修复。
- 链接: https://github.com/github/copilot-cli/issues/4490

**2. Atlassian MCP OAuth 失败（1.0.79 回归）** — #4480（CLOSED）
- **重要性**：与 #4490 同源问题，1.0.79 中回归。虽标记 CLOSED，但 1.0.80 仍在复现，说明需要更彻底的修复方案。
- **社区反应**：4 条评论，6 👍，用户明确报告了从 1.0.71 到 1.0.79 的回归路径。
- 链接: https://github.com/github/copilot-cli/issues/4480

**3. Bash 工具在 NixOS 上崩溃（版本 ≥1.0.49）** — #3392
- **重要性**：**已公开 80+ 天**未修复，影响 NixOS 用户无法执行任何命令（`Failed to start bash process`）。
- **社区反应**：9 👍（所有 OPEN Issues 中最高），4 条评论，包含 strace 详细诊断输出。
- 链接: https://github.com/github/copilot-cli/issues/3392

**4. MCP 注册表策略 fetch 返回 403，阻断 CI 中所有非默认 MCP 服务器** — #4346（CLOSED）
- **重要性**：GitHub Actions 中使用内置 `GITHUB_TOKEN`（无需 PAT 的新方式）认证时，MCP 服务器全部不可用，直接阻断 CI 场景。
- **社区反应**：3 👍，2 条评论。
- 链接: https://github.com/github/copilot-cli/issues/4346


### 📌 新出现 / 值得关注

**5. `/spawn` 命令模板自相矛盾：可能注入上下文到不相关运行中的会话** — #4491
- **重要性**：模板语言将 "创建子会话" 与 "注入上下文到无关会话" 混为一谈，且**缺少跨会话写入的审批门控**。破坏性安全风险。
- **社区反应**：刚提交 1 天，已有 1 条评论。
- 链接: https://github.com/github/copilot-cli/issues/4491

**6. v1.0.79  fatal OOM：V8 堆仅使用 0.6/4.3 GB 时崩溃** — #4499
- **重要性**：Windows 平台上长时间 autopilot 会话中 `FATAL ERROR: Committing semi space failed`——崩溃时堆远未满，指向**宿主机内存提交失败而非 V8 限制**。
- **社区反应**：新 Issue，暂无评论，但诊断数据完整。
- 链接: https://github.com/github/copilot-cli/issues/4499

**7. BYOK：autopilot 提示轮重新序列化旧 transcript，破坏提示缓存** — #4500
- **重要性**：BYOK（`responses` 线协议）下，autopilot 完成提示轮重建整个 `input` 数组，**字节级不一致破坏提示缓存**，导致 token 消耗上升。
- **社区反应**：新 Issue，附有请求级对比样例。
- 链接: https://github.com/github/copilot-cli/issues/4500

**8. Codespaces 预装 1.0.3，`copilot update` 只以 sudo 安装** — #4501
- **重要性**：Codespaces 镜像中 CLI 版本严重滞后（1.0.3 vs 最新 1.0.80），且自更新机制在该环境下失效（需要重启/权限问题）。
- **社区反应**：新 Issue，暂无讨论。
- 链接: https://github.com/github/copilot-cli/issues/4501

**9. MCP initialize 握手固定 60 秒且无重试——npx 启动的 stdio 服务器约 29% 会话失败** — #4421
- **重要性**：60 秒硬编码超时不可配置、失败后**拒绝重启**，npx 冷启动慢时约 1/3 会话中 MCP 不可用且不可恢复。
- **社区反应**：1 条评论（承认统计数据的合理性）。
- 链接: https://github.com/github/copilot-cli/issues/4421

**10. 将会话标记为 Done 后无法取消归档** — #4502
- **重要性**：用户误点后会**永久**从会话列表中消失（数据未删），但 UI 无撤销路径。
- **社区反应**：新 Issue，暂无讨论，0 👍。
- 链接: https://github.com/github/copilot-cli/issues/4502


## 4. 重要 PR 进展（2 条）

**1. 将 PR 自动化从 pull_request_target 迁移** — #4449（CLOSED）
- **功能**：移除高权限的 `pull_request_target` 事件，改用 issue 级写令牌 + 无权限的 `pull_request` 信号组合。保留问题与 PR 的关闭行为。
- **重要性**：仓库自身安全治理改进，降低恶意 PR 利用 CI 权限的风险。
- 链接: https://github.com/github/copilot-cli/pull/4449

**2. 处理 fork PR 关联缺失时的 invalid-label 写入** — #4497（OPEN）
- **功能**：当 GitHub 未填充 workflow run 的 PR 关联（fork PR 常见），写入器现在使用可信的 workflow-run 元数据搜索，并要求精确匹配一个 OPEN PR。
- **重要性**：作为 #4449 的补充，保证迁移后 fork PR 场景下自动化行为正确。
- 链接: https://github.com/github/copilot-cli/pull/4497


## 5. 功能需求趋势

从近期 Issue 中提炼出社区最关注的四个功能方向：

| 方向 | 代表性 Issue | 关注度 |
|------|-------------|--------|
| **MCP 生态稳定性与认证** | #4480、#4490（Atlassian OAuth 回归）、#4421（60s 握手超时无重试）、#4346（CI 中 403） | 🔥🔥🔥 最高（4 个独立 Issue） |
| **模型与上下文管理** | #4495（GPT-5.6 reasoning.mode 参数）、#4494（新模型本地缓存不刷新）、#4275（ACP contextTier 会话配置） | 🔥🔥 高 |
| **会话与状态管理** | #4502（Done 无法取消归档）、#4493（`-w` 会话 `/restart` 故障）、#4491（/spawn 跨会话写入） | 🔥🔥 高 |
| **平台兼容性与分发** | #3392（NixOS → 已 80+ 天）、#4499（Windows OOM）、#4501（Codespaces 版本滞后） | 🔥 中高 |


## 6. 开发者关注点（痛点 / 高频需求）

1. **回归频发正在侵蚀信任**：Atlassian MCP OAuth 在 1.0.78 正常 → 1.0.79 回归 → 修复后 1.0.80 再次回归（#4480 CLOSED，但 #4490 复现）。开发者对版本升级的谨慎度将不可避免提高。

2. **次版本升级存在行为不兼容**：`Bash tool breaks on NixOS`（#3392）在 1.0.49 引入、1.0.50 仍存在，**80+ 天未修复**——可能迫使 NixOS 用户锁定旧版本。

3. **"静默降级"与"不可恢复失败"模式引发不满**：
   - Task 工具静默降级子代理模型（#3565）
   - MCP 初始化失败后**永不重试**且会话内不可恢复（#4421）
   - `/restart` 在 `-w` 会话中因选项冲突直接失败（#4493）

4. **BYOK 用户关注缓存效率**：autopilot 提示轮重新序列化 transcript 破坏提示缓存（#4500），意味着 token 成本上升——这是 BYOK/Pay-as-you-go 用户的直接经济成本。

5. **平台支持完整性仍是短板**：NixOS（#3392）、Windows 大内存压力（#4499）、Codespaces 预装版本滞后且自更新失效（#4501）——三个独立平台问题均未解决。

---

*本日报由 AI 技术分析师基于 GitHub 公开数据自动生成。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-16

> 数据来源：`github.com/MoonshotAI/kimi-cli`

---

## 今日速览

订阅用户的 token 配额计费问题成为今日社区最激烈的讨论焦点（#2604），用户通过客户端仪表化数据指控有效配额缩水3-5倍；与此同时，社区对"记忆系统"的呼声持续升温，已有两个高赞 Issue 直指大项目开发中的上下文丢失痛点。代码维护方面，`StrReplaceFile` 替换计数逻辑修复 PR 获得合并进展。

---

## 版本发布

过去 24 小时内无新版本发布。

---

## 社区热点 Issues

### 🔥 高热度争议

**#2604 — Effective weekly allowance appears reduced ~3–5× without announcement**  
作者：tobiu | 更新：08-15 | 评论：2  
用户使用 Vivace 订阅进行 agentic 编码，通过客户端 wire-level 日志（JSONL）记录了每日原始 token 量（输入+缓存读取+输出），发现有效周配额缩水 3-5 倍。帖子要求官方澄清是条款变更还是计量回归（metering regression），目前尚无官方回复。  
→ [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2604)

**#2603 — Quota-aware compaction: context compaction should trigger on a token budget, not only near the model's max context window**  
作者：salim4n | 更新：08-15 | 评论：0  
指出 K3 模型拥有 1M token 上下文窗口（`max_context_size=1048576`），默认 `reserved_context_size=50000`，导致在订阅配额下上下文压缩几乎永远不会触发，agentic 会话会持续消耗 token 直至撞墙。建议在配额层面触发压缩，而非仅依赖模型窗口上限。  
→ [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2603)

### ⭐ 长期热门需求

**#1283 — [enhancement] Feature Request: Memory System - Persistent context across sessions**  
作者：CatKang | 创建：02-27 | 更新：08-15 | 评论：40  
社区呼声最高的功能请求：跨会话持久化上下文，包括 AI 自动记忆（项目模式、用户偏好）和用户手动记忆（指令文件）。40 条评论显示持续关注度极高，官方至今未给出时间表。  
→ [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)

**#1478 — 能否优化记忆层？搞大项目的时候很痛苦**  
作者：hahy36 | 创建：03-17 | 更新：08-15 | 评论：3  
中文用户跟进 #1283，指出参考文档中仅有一份 `agent.md`，没有系统级的记忆架构说明。给出了 OpenClaw 的目录结构（`SOUL.md` / `USER.md` / `MEMORY.md` / `memory/` 每日记录）作为参考，强调大项目中的上下文管理是刚需。  
→ [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1478)

### 🐛 已关闭

**#1155 — openai_legacy provider drops reasoning content, causing APIEmptyResponseError**  
作者：rongou | 创建：02-14 | 更新：08-15 | 评论：0  
已关闭。使用 OpenAI 兼容服务器（sglang/vllm）时，`openai_legacy` 提供器因 `reasoning_key` 未传递到 `OpenAILegacy` 构造函数，导致推理/思考内容被丢弃并触发 `APIEmptyResponseError`。此问题已修复，但未确认是否合入主线版本。  
→ [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1155)

---

## 重要 PR 进展

**#2524 — [OPEN] fix(tools): count StrReplaceFile replacements against the running content**  
作者：Sreekant13 | 更新：08-15  
**核心修复**：`StrReplaceFile` 按顺序执行编辑，但此前替换计数基于原始文件内容计算。链式编辑中，前一步骤生成的字符串在原始文件中不存在，导致计数不准确。此 PR 改为基于正在更新的内容计数，解决 #2526 报告的多轮编辑场景下替换统计偏差问题。  
→ [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2524)

**#2506 — [CLOSED] fix(kosong): raise a clear error on circular $ref in deref_json_schema**  
作者：Sreekant13 | 更新：08-15  
**已合并/关闭**。`kosong.utils.jsonschema.deref_json_schema` 对本地 `$ref` 进行内联展开并按递归遍历目标，遇到循环引用（circular `$ref`）时会导致栈溢出。此修复改为抛出清晰的错误提示，方便用户定位 schema 定义问题。维护者已接受，更改量 < 100 行。  
→ [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2506)

---

## 功能需求趋势

从近期提交的 Issues 中可提炼出三大主线：

1. **记忆与上下文持久化（Memory System）** — 这是社区最集中的诉求（#1283、#1478）。用户普遍反馈在大型代码库上工作时，跨会话的上下文丢失严重影响效率，期望引入自动/手动双层记忆机制。

2. **配额感知的智能管理（Quota Awareness）** — #2603 和 #2604 共同指向一个方向：当模型上下文窗口远超订阅配额时，工具必须在配额层面做主动优化（如提前压缩），并透明地向用户展示额度消耗数据。用户已开始用仪表化手段监控用量，对"黑盒计量"容忍度显著降低。

3. **OpenAI 兼容层稳定性** — #1155 暴露了 `openai_legacy` 提供器对推理内容（reasoning content）的兼容缺陷。随着更多用户接入自建推理服务（sglang/vllm），该方向的质量保证将越发重要。

---

## 开发者关注点

- **计费透明度与信任危机**：用户已主动做 wire-level 监控，说明对官方额度计量的信任正被消耗。Vivace 订阅用户连续数周的用量对比数据极具说服力，若官方不及时回应，极可能发酵为社区信任危机。

- **大项目上下文管理是最高频痛点**：两个高赞记忆类 Issue（累计 43 条评论，持续 6 个月）表明，CLI 在复杂 agentic 工作流中的上下文维持能力已构成核心体验瓶颈，超过了对新模型或 IDE 集成的诉求。

- **压缩策略需要"系统级"思维**：开发者普遍认为，上下文压缩不应只盯模型窗口上限（1M tokens），而应结合订阅配额、任务类型、历史会话长度做多维决策。用户期望的是"配额预算内最大化产出"，而非简单地在窗口临界点截断。

- **中文社区活跃度上升**：#1478 为纯中文 Issue，引用了其他工具的记忆实现方案，说明国内开发者群体正在积极实践 Kimi Code CLI 并主动提出改造建议，值得官方关注。

---

*本日报基于 GitHub 公开数据自动生成，统计窗口为 2026-08-15 至 2026-08-16。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-16

## 今日速览

今日社区焦点集中在 **OpenCode Go/Zen 付费服务异常**（#37790）、**grok-4.5 模型持续故障**（#40206、#40886、#42802）以及 **OpenCode 服务器整体不稳定**（#42799）等问题，服务可用性成为开发者最关切的议题。同时，PR 侧有多项针对 V2 架构的底层优化（事件时间戳、流式批量、插件事件作用域），并新增了 **Docker/Incus 工作区蓝图**和**每会话预算**两项重量级功能。

## 社区热点 Issues

挑选 10 个值得关注的 Issue，覆盖服务可用性、计费、CLI/TUI 体验等维度：

1. **[#37790] OpenCode Go 订阅已扣款但工作区显示"余额不足"** — 评论 14
   Stripe 扣款成功但工作区仍报 "Insufficient balance"，直接导致付费用户无法使用服务，是今日评论数最高的 Issue，涉及计费系统状态同步问题。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/37790)

2. **[#24879] 功能请求：Go Pro 档位（$20）及首月折扣** — 评论 11，👍 11
   现有 Go 月配额易耗尽，用户希望有中间档位和更灵活的计费选项，反映社区对更精细化定价的需求。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/24879)

3. **[#42143] 官网声称 100% 免费，为何实际要求订阅？** — 评论 10
   信息透明度问题，用户对定价策略感到困惑，是社区情绪的一个风向标。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/42143)

4. **[#7801] 功能请求：Plan 模式 + Question 工具自动切换至 Build 模式** — 评论 10，👍 31
   👍 数在所有 Issue 中最高，说明这是社区高票期待的一个工作流优化特性。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/7801)

5. **[#40206] grok-4.5 在 OpenCode Go 上自 8 月 2 日起无法使用** — 评论 9
   连续多日未修复的模型故障，引发多个重复 Issue，是影响范围最广的模型可用性问题。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/40206)

6. **[#42799] OpenCode 服务器处于故障状态** — 评论 2
   工作区页面报 500 或超时，DB 层出现 "transaction pool connection limit exceeded"，可能是今日多项服务异常的根因。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/42799)

7. **[#27924] 会话压缩失败时陷入无限循环** — 评论 8
   上下文溢出时，压缩无法降低 token 数，导致 "压缩→溢出→再次压缩" 的无限循环，是一个隐蔽的稳定性 Bug。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/27924)

8. **[#42750] 上游请求失败：端点不可用** — 评论 4（同日 #42757）
   多个用户同时报告 "Endpoint is unavailable"，且自动重试 8 次仍失败，指向服务端路由或上游 API 故障。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/42750)

9. **[#42739] Provider.list 崩溃：Cloudflare 环境变量存在但缺少 API Token** — 评论 4
   TUI 启动即崩溃（非预期，且未给出明确报错路径），影响通过 Cloudflare 环境变量配置的用户。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/42739)

10. **[#35295] `tui.json` 设置 `"mouse": false` 后滚轮行为异常** — 评论 4
    关闭鼠标后滚轮事件回落为方向键，触发了历史命令导航而非消息滚动，是 TUI 交互细节的一个 bug。
    [查看 Issue](https://github.com/anomalyco/opencode/issues/35295)

## 重要 PR 进展

以下 PR 反映了核心架构演进与新功能开发方向：

1. **[#42811] feat(session): 添加会话已读状态** — 新增
   服务端新增会话已读状态管理（`time.idle > time.viewed`），让客户端可判断未读会话，可能是官方桌面/Web UI 通知功能的基础。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42811)

2. **[#42823] feat(opencode): 添加每会话预算限制** — 已合并
   为每个会话添加可选预算上限，超出即停止，新增 DB 迁移和 PATCH 接口，帮助用户控制成本。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42823)

3. **[#42824] feat(app): 添加语音输入和会话预算 UI** — 已合并
   配合 #42823 的 UI 实现，新增麦克风按钮（语音转文字）和会话预算面板。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42824)

4. **[#42831] feat(core): 添加 Docker 蓝图工作区** — 新增
   基于不可变蓝图快照的本地 Docker 工作区，将子代理 fork 到隔离容器中，空闲容器自动停止。工作区隔离沙箱的重要一步。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42831)

5. **[#42829] feat(core): 添加 Incus 工作区 Fork** — 已合并
   与 #42831 互补的 Incus 后端，支持容器/VM 蓝图，按需唤醒空闲实例并支持子代理隔离。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42829)

6. **[#42828] refactor(core): 使用数值事件时间戳** — 已合并
   V2 事件时间从 `DateTime.Utc` 改为 epoch 毫秒，消除序列化往返转换开销。底层性能修复。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42828)

7. **[#42826] fix(core): 批量流式会话增量** — 已合并
   将 provider 文本/推理/工具输入分片合并为批量事件，大幅减少事件数量，预计可显著改善长会话的 TUI 性能。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42826)

8. **[#42832] fix(plugin): 限定 Promise 事件迭代器作用域** — 新增
   修复插件事件适配器中 `Stream.toAsyncIterable` 的跨作用域泄漏问题，确保缓冲事件不会逃逸到错误上下文。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42832)

9. **[#42820] fix(app): 统一使用树形目录选择器** — 已合并
   替换所有旧的非原生扁平目录选择器（解决 #42784），改善 Web UI 项目管理体验。
   [查看 PR](https://github.com/anomalyco/opencode/pull/42820)

10. **[#42825] fix(app): 释放虚拟化时间线元素** — 已合并
    修复 TanStack Virtual 的 `elementsCache` 保留已移除 DOM 节点的问题，一次长会话可减少约 37,500 个游离节点，显著降低内存占用。
    [查看 PR](https://github.com/anomalyco/opencode/pull/42825)

## 功能需求趋势

从近期 Issue 和 PR 中可以提炼出以下社区关注方向：

- **服务稳定性与可观测性（最紧迫）**：多个关于服务不可用、模型 5xx、上游端点故障的 Issue，以及错误信息未通过 ACP 协议传达的反馈（#42827），说明社区对服务可靠性和错误透明度的要求已超过新功能需求。
- **工作区隔离与沙箱**：Docker 蓝图（#42831）和 Incus Fork（#42829）两个重量级 PR 同时落地，表明团队正将工作区隔离作为 V2 的核心能力之一，可能服务于安全敏感的开发场景。
- **会话控制与成本管理**：每会话预算（#42823/#42824）、Go 订阅上限的灵活性（#24879）以及 DeepSeek token 过量消耗的投诉（#32911），都指向用户希望在细粒度上控制 token 消耗和费用。
- **TUI 可用性细节**：鼠标滚轮行为（#35295）、链接换行不可点击（#35649、#42805）、运行中子代理行不可点击（#42754）等，均为终端交互的高频细节问题。
- **AI 供应商集成问题**：grok-4.5 故障（#40206、#40886、#42802）引发多个重复 Issue，同时也有对 GLM reasoning toggle 的支持请求（#42793）、GitLab OAuth 模型发现修复（#37104），说明社区对不同模型/供应商的支持质量同样敏感。

## 开发者关注点

- **付费用户的信任危机**：扣款成功但服务不可用（#37790）、官网宣称免费却要求订阅（#42143）等，已引发不少讨论——计费系统与价值信息的一致性，是社区当前最大的痛点。
- **错误信息可观测性不足**：多处反馈只看到 "Unexpected server error" 或 "Endpoint is unavailable"，无法定位是本地配置、上游延迟还是服务端故障（#42750、#42739、#42802）。有开发者明确要求这类错误应通过 ACP 协议下发（#42827）。
- **高频小故障干扰**：如会话压缩死循环（#27924）、移动目录后路径未更新（#34737）、permission.ask 未实际生效（#32787）等，这类问题对日常使用体验的干扰很大。
- **对性能修复的积极反馈**：虚拟化内存泄漏修复（#42825）与流式事件批量合并（#42826）都获得了不少关注，说明社区对长会话卡顿和内存膨胀问题的感知是很强的。

---

> 日报数据来源：[anomalyco/opencode](https://github.com/anomalyco/opencode) · 生成时间：2026-08-16

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

## Pi 社区动态日报 — 2026-08-16

> 数据来源: [earendil-works/pi](https://github.com/badlogic/pi-mono) | 收录时段: 2026-08-15 至 2026-08-16

---

### 1. 今日速览

今日社区焦点集中在**上下文管理与压缩（compaction）的正确性**上，多份 PR 针对会话边界压缩、token 统计口径与工具角色损坏问题进行了修复；同时，**TUI 交互细节**（光标闪烁、表单控件、终端兼容性）和**模型支持扩展**（DeepSeek V4 Flash 低推理档位、xAI Grok 4.6）也呈现密集的社区讨论与提交。值得关注的趋势是，**扩展系统与核心流程的集成**（事件订阅、销毁管理）正成为开发者高频诉求。

---

### 2. 版本发布

过去 24 小时内无新版本 Release。

---

### 3. 社区热点 Issues（精选 10 条）

- **#6879 [OPEN] auto-compaction 在上下文超过 100% 后才触发，直至 provider 拒绝请求**  
  自动化压缩机制在超长 agentic 回合中未能及时触发，导致请求在 373k token 处被 API 拒绝才介入。获得 17 👍，社区对边界检查策略（check after every agent action）高度关注。  
  [链接](https://github.com/earendil-works/pi/issues/6879)

- **#6187 [CLOSED] WSL 下 GitHub Copilot 设备授权后 Pi 登录挂起**  
  浏览器侧设备已注册成功但 TUI 内部检测不到，导致登录流程卡死。WSL 环境兼容性问题持续受关注（27 条评论）。  
  [链接](https://github.com/earendil-works/pi/issues/6187)

- **#8003 [OPEN] 流式输出时输入框内光标剧烈闪烁**  
  非正常频率的 cursor blink 严重影响交互体验，输入时尤其明显。开发者期待 TUI 渲染层对终端光标状态的精准控制。  
  [链接](https://github.com/earendil-works/pi/issues/8003)

- **#8028 [OPEN] TUI `fullRender` 渲染超长输出触发 V8 字符串长度上限崩溃**  
  渲染大量图像帧场景下 `RangeError: Invalid string length` 导致进程崩溃，对大上下文/大渲染块的稳定性提出挑战。  
  [链接](https://github.com/earendil-works/pi/issues/8028)

- **#8171 [CLOSED] TUI 思维块渲染：固定最大高度 + 内部滚动，完成后自动折叠**  
  长思维块撑爆 transcript 的问题，社区提出 `thinkingMaxHeight` 配置与自动折叠两个方案。  
  [链接](https://github.com/earendil-works/pi/issues/8171)

- **#8170 [CLOSED] Windows 上 bash 工具可执行 `taskkill /F /IM node.exe` 杀死 Pi 自身宿主进程**  
  模型生成的命令未经确认即可通过内置 bash 工具执行，直接导致 Pi 宿主进程被强制终止，存在严重安全/稳定性隐患。  
  [链接](https://github.com/earendil-works/pi/issues/8170)

- **#8154 [CLOSED] 隐藏思维块在 transcript 中残留 1-2 行空白占位**  
  思维块被 markdown transformer 置空后未能完全折叠，与工具行（tool rows）的行为不一致。  
  [链接](https://github.com/earendil-works/pi/issues/8154)

- **#8185 [CLOSED] Code Review: auth-check.ts 存在 TOCTOU 竞态条件与错误处理缺口**  
  社区贡献者对认证检查代码进行深度审查，指出 `getUser` 路径的竞态窗口与多级错误处理不一致问题。  
  [链接](https://github.com/earendil-works/pi/issues/8185)

- **#8168 [CLOSED] 压缩与会话恢复导致 tool-result 角色损坏 → 422 错误**  
  Compaction 后 tool message 的 role 被破坏（`ChatMessageRole.TOOL`），触发 OpenAI-compatible 接口 422，影响 Tool-heavy 工作流。  
  [链接](https://github.com/earendil-works/pi/issues/8168)

- **#8166 [CLOSED] 扩展在 tool 批次中途注入自定义消息破坏 tool_calls 邻接关系**  
  扩展通过 `pi.sendMessage(..., { triggerTurn: false })` 注入消息后，后续回合全部因 `Messages with role 'tool' must be a response to 'tool_calls'` 失败。  
  [链接](https://github.com/earendil-works/pi/issues/8166)

---

### 4. 重要 PR 进展（精选 10 条）

- **#8153 [CLOSED] 在安全的回合边界执行自动压缩**  
  引入 run-scoped 边界压缩 API，在回合之间重建 live context 并保留 recent tail，避免压缩打断进行中的 agent 回合，同时保证溢出恢复有界。  
  [链接](https://github.com/earendil-works/pi/pull/8153)

- **#8164 [CLOSED] 禁止从尾部 assistant 消息继续执行（压缩崩溃修复）**  
  静默溢出压缩在已完成回合（stopReason 'stop'）误用 `agent.continue()`，导致 `Cannot continue from message role: assistant` 崩溃。修复为仅在回合中途被拒（stopReason 'error'）时重试。  
  [链接](https://github.com/earendil-works/pi/pull/8164)

- **#8165 [CLOSED] tokens.total 只统计计费 token（排除 cacheRead/cacheWrite）**  
  cache token 按 1/120 费率计费，此前纳入 total 会扭曲压缩预算与状态统计。现在 total = input + output，cache 单独上报。  
  [链接](https://github.com/earendil-works/pi/pull/8165)

- **#8151 [CLOSED] 扩展 widget 渲染失败防护：失效时销毁 ctx 持有的 widget**  
  第三方扩展在 `/reload` 后 widget 注册存留但 ctx 已失效，导致渲染崩溃。该 PR 增加 containment（失败隔离）与自动销毁机制。  
  [链接](https://github.com/earendil-works/pi/pull/8151)

- **#8155 [OPEN] 修复 TUI 渲染过程中重置光标闪烁的问题**  
  在 `TuiBase` 中追踪终端光标可见性，仅在状态切换时发送可见性命令，避免每次渲染都重置光标闪烁状态，同时保留覆盖层与设置调用的语义。  
  [链接](https://github.com/earendil-works/pi/pull/8155)

- **#8158 [OPEN] 将 grok-mermaid 迁移至 lovely-mermaid 并升级终端渲染**  
  替换 mermaid 渲染引擎，解决原有实现的大量 corner cases（类名被忽略等），关闭 #8157 与 #7832。  
  [链接](https://github.com/earendil-works/pi/pull/8158)

- **#8181 [CLOSED] 为 opencode/opencode-go 上的 DeepSeek V4 Flash 暴露 low 推理档位**  
  原映射仅对 `deepseek/deepseek-v4-flash` 生效，opencode 通道回退到 `DEEPSEEK_V4_THINKING_LEVEL_MAP`（low 为 null），现已补齐。  
  [链接](https://github.com/earendil-works/pi/pull/8181)

- **#8124 [OPEN] xAI 模型改为默认走 Responses API 并切换默认模型至 Grok 4.6**  
  路由调整 + 默认模型升级（Grok 4.5 → 4.6），同时从 Pi 发送 user agent。  
  [链接](https://github.com/earendil-works/pi/pull/8124)

- **#8146 [CLOSED] 限制 Baseten 上 DeepSeek V4 Flash 输出上限为 384k tokens**  
  models.dev 数据与实际服务能力不一致（报告 1M 但实际 384k），对 `s` 中该模型的 maxTokens 进行硬编码上限修正。  
  [链接](https://github.com/earendil-works/pi/pull/8146)

- **#8174 [CLOSED] 重复 ambiguous length 停止时使用中性措辞**  
  当第二次可恢复的 length 停止耗尽一次压缩-重试机会时，即使两次响应均非 `isContextOverflow`，也不再强制输出“Context overflow recovery failed...”这一误导性错误。  
  [链接](https://github.com/earendil-works/pi/pull/8174)

---

### 5. 功能需求趋势

| 方向 | 代表 Issues/PRs | 说明 |
|------|----------------|------|
| **压缩（Compaction）正确性** | #6879、#8153、#8164、#8165、#8168、#8175 | 自动压缩时机、边界安全、token 统计口径、失败事件透传，是当前社区最为集中的关注领域。 |
| **TUI 交互细节打磨** | #8003、#8171、#8154、#8155、#8184、#8183 | 光标闪烁、思维块滚动/折叠、空白残留、退出时 stdout 冲刷、快捷键冲突文档化，终端体验精细化需求突出。 |
| **扩展系统与核心集成** | #8147、#8173、#8175、#8151、#8166 | 事件通知（对话框、压缩失败）、widget 销毁管理、hook 可取消性、跨进程写入讨论，扩展生态正在快速成型。 |
| **模型/Provider 支持扩展** | #8181、#8124、#8146、#8178、#8182、#8167 | DeepSeek V4 多通道补齐、xAI 默认模型升级、llama.cpp 模型选择、新 provider 接入（LLMTR），模型层覆盖持续推进。 |
| **/tree 与文件恢复能力** | #8152 | no-summary 导航时可选恢复文件到目标回合，回应此前关闭的 #5522，社区仍有意愿推进。 |
| **Shell 补全** | #4776 | `pi completion` 子命令（bash/zsh/fish），低频但持续有诉求。 |

---

### 6. 开发者关注点

- **压缩失败时的可观测性不足**：压缩失败后扩展侧只能收到“沉默”，核心错误没有透传到 `session_before_compact` 等扩展事件（#8175）。开发者希望压缩流程对用户与扩展都透明。
- **工具调用批次消息结构脆弱**：任何在 tool_calls→tool 邻接区间注入的自定义消息都会导致后续回合全部 4xx（#8166、#8168）。消息构造的防御性校验与恢复机制被多次提及。
- **WSL/Windows 环境兼容性仍是长期痛点**：WSL 登录挂起（#6187）、Windows 下 bash 工具可自杀宿主（#8170）、Windows Terminal 快捷键冲突（#8183）均在本日更新，跨平台稳定性需要更多针对性测试。
- **状态统计口径不唯一**：cache token 是否计入 total（#8165）、模型切换后 thinking level 的保持/钳制策略（#7871），反映统计与状态管理系统缺少统一设计。
- **扩展生命周期管理需求迫切**：多个 extension 相关的 issue 指向同一个问题——扩展在 reload 或失效后，其持有的 UI 组件与事件订阅未能被干净清理（#8151、#7157），社区呼吁 core 提供标准化的销毁与失效机制。

---

*本日报由 AI 自动汇总生成，仅呈现当天更新的 Issues 与 PRs 中讨论度较高、影响面较大的内容。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-16** | **数据来源：** [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)


## 今日速览

今日社区动态聚焦于 **`/review` 命令的系列可靠性修复**（工作树并发竞争、重叠检测缺陷、Schema 摩擦等）与 **CI 流水线的多项自愈与安全加固**（自托管 runner 清理范围收窄、failed checkout 自修复）。此外，**SWE-bench Verified 与 Terminal-Bench 2.0 的全链路 smoke 测试全部成功**，质量门禁保持稳定。


## 版本发布

### v0.21.11-nightly.20260815.c396fe3d12
> 发布时间：2026-08-15 | [查看 Release](https://github.com/QwenLM/qwen-code/releases)

**主要更新：**

- **feat(autofix)**：新增 deny-by-default 足迹门控（footprint gate）与位置窗口普查（positional window censuses），由 @wenshao 提交（[PR #9156](https://github.com/QwenLM/qwen-code/pull/9156)）。
- **fix(web-shell)**：修复 Web Shell 相关问题。

**Smoke 测试矩阵（均成功）：**
- **dsw-eas-tb-smoke-20260815-r5**：Terminal-Bench proxy-prelude 修复后的单用例端到端验证；SWE-bench Verified 1/1 通过（1 resolved, 0 errors）。
- **dsw-eas-tb-smoke-20260815-r4**：修复 Terminal-Bench verifier 代理 prelude 转义后的 SWE + TB 链路验证。
- **dsw-eas-tb-smoke-20260815-r3**：发布事件端到端清理验证。
- **dsw-eas-tb-smoke-20260815-r2**：DSW EAS Harbor 链的发布事件 smoke。
- **dsw-eas-full-20260815-r1**：完整基准测试 —— SWE-bench Verified 500 例 + Terminal-Bench 2.0 89 例全量跑通。


## 社区热点 Issues（Top 10）

### 1. [#9194](https://github.com/QwenLM/qwen-code/issues/9194) chore(review): 关闭 PR #9096 评审第 5-6 轮的 mutation-verified test-pin 缺口
- **标签**：P3 / enhancement / testing
- **作者**：@wenshao | 更新：08-16 | 💬 4
- **重要性**：持续推动测试从"能通过"走向"真正锁死契约"。自动评审器发现生产代码 mutation 后测试套件依然全绿，说明存在 test-pin 不足问题，是质量体系的深水区加固。

### 2. [#7427](https://github.com/QwenLM/qwen-code/issues/7427) web-shell: artifact 面板自动刷新时持续报错 'Load artifacts failed: Failed to fetch'
- **标签**：P2 / bug / UI / web-shell / welcome-pr
- **作者**：@qwen-code-dev-bot | 更新：08-15 | 💬 5
- **重要性**：老牌 issue 至今未决，且发生在 `qwen serve` 的会话 artifact 面板自动刷新路径（非用户主动操作）。Web Shell 核心体验问题，社区关注度高。

### 3. [#9250](https://github.com/QwenLM/qwen-code/issues/9250) qwen serve 新文件写入硬编码 0600 权限，忽略 umask、无配置项
- **标签**：P3 / enhancement / file-operations / daemon
- **作者**：@VorlMaldor | 更新：08-15 | 💬 4
- **重要性**：`write_file`、`edit`、`notebook_edit` 创建的新文件无条件使用 mode 0600，忽略 daemon umask，且无任何配置途径。影响多用户协作场景的文件权限管理。

### 4. [#9089](https://github.com/QwenLM/qwen-code/issues/9089) autofix: 携带 PAT 的 Job 与不可信分支代码共享主机，需 runner 级隔离
- **标签**：P1 / bug / security / CI / github-actions
- **作者**：@wenshao | 更新：08-15 | 💬 4
- **重要性**：安全等级最高的未决问题。PR #8961 加固后仍存在一类**无法在 GitHub Actions step 内部关闭**的攻击面——PAT 与不可信代码在同一 runner 上共存。**P1 优先级，社区应重点关注。**

### 5. [#9200](https://github.com/QwenLM/qwen-code/issues/9200) 相同任务、相同本地模块，结果相同但过程差异巨大——"qwencode 这么拉跨吗？"
- **标签**：badcase / need-information
- **作者**：@yushuisheng1235 | 更新：08-15 | 💬 4
- **重要性**：用户对比 qwen code (v0.21.12) 与 iflow cli 的调用日志，质疑推理过程的一致性与质量。**用户情绪较大**，虽为 badcase 但反映核心使用体验问题，值得开发者排查。

### 6. [#5966](https://github.com/QwenLM/qwen-code/issues/5966) 0.19.3 UI 不定期错误，中文输入法完全无效
- **标签**：P2 / bug / UI / welcome-pr
- **作者**：@aspnmy | 更新：08-15 | 💬 4
- **重要性**：中文输入法在 UI 中完全失效且不报错、无法定位——**中文用户高频痛点**，长期未修复（创建于 06-28），社区持续关注。

### 7. [#9219](https://github.com/QwenLM/qwen-code/issues/9219) /review presubmit 重叠匹配仅精确匹配单行——多行范围和语义重复会漏判
- **标签**：P2 / bug / commands
- **作者**：@wenshao | 更新：08-15 | 💬 4
- **重要性**：评审系统的准确性缺陷，会遗漏重复评论。@wenshao 持续高频输出 review 系 bug，本期已有 5+ 条同类 issue。

### 8. [#9218](https://github.com/QwenLM/qwen-code/issues/9218) /review presubmit --new-findings 拒绝 Step 6 findings 产物（路径与 skill 示例冲突）
- **标签**：P2 / bug / CLI / commands
- **作者**：@wenshao | 更新：08-15 | 💬 4
- **重要性**：路径冲突导致 high-effort 评审流程中断，影响自动化评审的可用性。

### 9. [#9230](https://github.com/QwenLM/qwen-code/issues/9230) 后续建议侧查询破坏服务端前缀缓存，`enableCacheSharing` 默认关闭
- **标签**：P2 / bug / performance / caching
- **作者**：@yiliang114 | 更新：08-15 | 💬 3
- **重要性**：llama.cpp 等前缀缓存服务器上主会话缓存命中率接近 0%，每次主轮次都全量预填充。**性能敏感用户的核心痛点**，且 `enableCacheSharing` 默认关闭让问题更隐蔽。

### 10. [#9198](https://github.com/QwenLM/qwen-code/issues/9198) qwen 长跑一周后 OOM，tmux 窗口按键全乱
- **标签**：P2 / bug / performance / memory
- **作者**：@freshui | 更新：08-15 | 💬 3
- **重要性**：服务器 1TB 内存仍然 OOM；崩溃后 tmux 乱码无法操作（复制/粘贴不可用，kimi code 正常）。**长时运行稳定性与终端兼容性问题**，真实用户场景反馈。


## 重要 PR 进展（Top 10）

### 1. [#9211](https://github.com/QwenLM/qwen-code/pull/9211) fix(review): 锁定 PR 评审工作树租约，防止并发会话冲突 `<autofix/takeover>`
- **作者**：@wenshao | 更新：08-16
- **内容**：工作树租约升级为锁。此前仅会话结束崩溃清理时检查租约，破坏性操作前无人校验；现在并发会话无法互相删除工作树。

### 2. [#9220](https://github.com/QwenLM/qwen-code/pull/9220) fix(ci): 复用评审 runner 上自修复失败的 checkout `<autofix/takeover>`
- **作者**：@wenshao | 更新：08-16
- **内容**：自动评审 Job 在复用自托管 runner 池上检出基础分支，失败即终止且无人修复。本 PR 使 checkout 自愈——首次失败后自动清理并重试。

### 3. [#9228](https://github.com/QwenLM/qwen-code/pull/9228) fix(ci): 将 serve-ab 的自托管清理收窄至 A/B 检出目录 `<autofix/takeover>`
- **作者**：@qwen-code-dev-bot | 更新：08-16
- **内容**：修复 `Wipe stale workspace` 步骤误删整个共享工作区（含 ~900MB 的 .git 历史）的问题，将清理范围限定在 A/B 检出目录内。

### 4. [#9247](https://github.com/QwenLM/qwen-code/pull/9247) fix(review): 将组合正文控制在 GitHub 评审限制内 `<review/self-reported>`
- **作者**：@wenshao | 更新：08-16
- **内容**：`compose-review` 衡量待返回的评审正文，确保在 GitHub 65,536 字符限制内。超出时按固定顺序裁剪：deferral 展示 → not-reviewed 披露 → blockers 等。

### 5. [#9235](https://github.com/QwenLM/qwen-code/pull/9235) fix(serve): 从 Web Shell 事件面中编辑掉 skill 正文 `<review/self-reported>`
- **作者**：@wenshao | 更新：08-16
- **内容**：daemon 会话快照嵌入了每个已安装 skill 的完整 SKILL.md——原生客户端展示/编辑需要，但浏览器事件面也收到完整原文。本 PR 在事件面对 skill 正文进行编辑脱敏。

### 6. [#9192](https://github.com/QwenLM/qwen-code/pull/9192) fix(autofix): 基于测量时间与外部 head 移动重新锚定增长分歧 `<autofix/takeover>`
- **作者**：@wenshao | 更新：08-16
- **内容**：收紧 PR #9104 的增长分歧可比性窗口：`autofix-growth-now` 标记携带准备时测量时刻，分歧读取按测量时间过滤，防止外部 head 移动导致误判。

### 7. [#9183](https://github.com/QwenLM/qwen-code/pull/9183) feat(review): 将反向审计轮次上限扩展至 diff 拓扑
- **作者**：@wenshao | 更新：08-16
- **内容**：反向审计循环的轮次上限从"所有场景一个数"改为按拓扑分级：小 diff 10 轮、分块 5 轮、超大 diff 3 轮，超大档优先判定（可达性裁定）。

### 8. [#9189](https://github.com/QwenLM/qwen-code/pull/9189) feat(autofix): 将已验证的足迹外发现延迟到存活的后续队列
- **作者**：@wenshao | 更新：08-16
- **内容**：为 autofix 评审循环新增第四种处置——**延迟到后续（Defer to follow-up）**：已验证为真实但修复超出 PR 足迹的发现，记入机器可读队列，防止漂移丢失。

### 9. [#9190](https://github.com/QwenLM/qwen-code/pull/9190) feat(review): 本地评审-修复循环的内容锚定增量轮次
- **作者**：@wenshao | 更新：08-16
- **内容**：本地评审流程此前完全无增量支持——每轮都重新捕获并评审整个脏树（token 消耗大头）。本 PR 为本地文件路径评审引入内容锚定的增量轮次机制。

### 10. [#9130](https://github.com/QwenLM/qwen-code/pull/9130) feat(triage): 为沙箱验证添加确定性 flakiness 门控 `<autofix/takeover, review/self-reported>`
- **作者**：@wenshao | 更新：08-16
- **内容**：`qwen-triage.yml` verify job 新增 flakiness 门控：在干净安装/构建后，将 PR 新增/修改的单元测试文件重跑 N 次（默认 5 次，可配置 2-10），检测不稳定的测试用例。


## 功能需求趋势

从近 24 小时 issue/PR 动态提炼出以下社区关注方向：

### 1. `/review` 命令体系的大规模加固（主导趋势）
wenshao 一人贡献了 10+ 条 review 相关 issue/PR，覆盖：并发冲突、schema 摩擦、重叠检测缺陷、工作树竞争、轮次缩减逻辑等。**评审工具的可扩展性与可靠性是当前最高优先级。**

### 2. CI/CD 自愈与安全隔离
- **Runner 级隔离**（#9089，P1 安全）：PAT 与不可信代码的物理隔离问题悬而未决。
- **自托管 runner 清理收窄**（#9228）：避免误删 .git 历史。
- **Checkout 自修复**（#9220）：失败后自动恢复而非直接终止。

### 3. Web Shell 体验持续优化
- artifact 面板刷新报错（#7427）
- 手动会话名在 `/clear` 后丢失（#8977）
- skill 正文字段从事件面脱敏（#9235）——从数据暴露向安全方向推进

### 4. 缓存与性能优化
- **服务端前缀缓存**（#9230）：llama.cpp 等场景下主会话缓存命中率接近 0%，`enableCacheSharing` 默认关闭加剧问题。

### 5. 文件权限与 umask 支持
**#9250**：新文件写入模式硬编码 0600，用户无法通过 umask 或配置干预——多用户环境下的权限管理需求浮出水面。


## 开发者关注点

### 高频痛点
1. **中文输入法失效**（#5966）：0.19.3 后不定期出现，无报错、无法定位，中文用户受影响严重。
2. **长时运行稳定性**（#9198）：一周长跑后 OOM（1TB 内存仍溢出），崩溃后终端乱码无法操作。
3. **推理过程一致性**（#9200）：相同任务下"过程差距一言难尽"，用户对模型决策质量提出质疑。
4. **CI 频繁失败**：多起 E2E Tests 失败（#9241、#9239、#9237、#9248、#9159），虽多数自动标记为 ready-for-agent 但高频出现值得警惕。

### 值得注意的信号
- **P1 安全 issue 仍未关闭**（#9089）：PAT 凭据与不可信代码共存于同一 runner，属于架构级风险。
- **Review 系统自身质量**：大量 review 相关 bug 由 @wenshao 主动上报并自修，反映团队对自研工具链的高标准；但集中爆发也说明该功能正处于快速迭代期，稳定性有待验证。
- **并发评审场景**（#9205、#9207、#9208）：多个并发问题围绕 `--comment` 同一 PR 的竞态条件，生产环境使用的用户需注意升级节奏。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-08-16** | 数据来源：github.com/Hmbown/DeepSeek-TUI（CodeWhale）


## 今日速览

今日社区焦点集中在 **v0.9.8 发布冲刺与 CI 修复**：多条 main 分支 CI 红牌问题（#5392 macOS 凭据测试、#5383 provider-count 断言、#5395 CI 取消机制）均已提交修复 PR；同时 **"Constitution" 中文翻译争议尘埃落定**（#4949 关闭，定为"宪章"）。多项功能 PR 密集提交：第三方模型预制模板（#5406）、长上下文模型读/工具结果大小限制可配置化（#5405）、SSE 流式乱码修复（#5404）等。


## 社区热点 Issues（10 个）

**1. #4949「Constitution」中文翻译之争（今日关闭）**
作者 SparkofSpike 发起，持续三周、17 条评论，最终**"宪章"**胜出。该词涉及项目基础文档的本地化用词，在中文语境下"宪法"一词的政治敏感性成为争论焦点，反映了社区对 i18n 严谨性的重视。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/4949)

**2. #5316 CodeWhale TUI Crate 分解 EPIC（Umbrella）**
架构重构的顶层追踪 Issue，所有子 EPIC 和 FEAT 均向其汇报。关注点在于单体 crate 的模块化拆分，是影响项目长期可维护性的核心架构议题。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5316)

**3. #5374 [bug] Agent 写作文本乱码**
macOS 用户反馈 agent 输出文本出现乱码（U+FFFD 替换字符），影响可读性，5 条评论。这是流式渲染的编码处理 bug，直接影响用户体验。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5374)

**4. #5322 [bug] 回归：宽终端下输出区不填满（已关闭）**
v0.9 回归问题——输出区被限制在最大宽度，宽屏下两侧大量留白，与 v0.8.65 行为不一致。已由 PR #5400 修复。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5322)

**5. #5350 [enhancement] 简化第三方模型配置，增加预制模板**
配置 OpenCode Zen、Agnes、美团 Sensenova 等第三方服务商时需手动填写 Base URL/模型名/密钥，且保存后常卡在 `not checked` 状态。建议内置预制模板 + 测试连接按钮 + 修复缓存。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5350)

**6. #5367 [enhancement] 模型可见的读/工具结果大小限制可配置化**
自托管长上下文模型（如 DeepSeek V4）用户遇到单次 `read` 结果被截断在 50 KiB / 16 KiB / 12,000 字符的问题，64 KiB 文件需约 20 次额外读取。社区要求暴露为可配置项。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5367)

**7. #5370 [bug] P0: Web UI 完全损坏**
维护者 Hmbown 报告公开 Web UI "完全损坏"，需要对照 harness 引用全面审计重建。影响 codewhale.net 的 Next.js 前端。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5370)

**8. #5241 [bug] 定价端点返回 503，所有会话显示 unverified_live_pricing**
升级至 0.9.3 后成本显示完全失效，所有 provider 均显示 `unpriced_reasons = ["unverified_live_pricing"]`，影响计费透明度和用户信任。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5241)

**9. #5410 [enhancement] bwrap 沙箱可配置额外根目录**
Zig 开发者在启用 bwrap 沙箱后遭遇"access denied"：`/dev/null` 重定向被禁止、系统库链接失败。需要沙箱根目录可扩展配置。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5410)

**10. #5403 main 在四个 CI 运行后全平台显红**
#5395 修复了 CI 相互取消后，四条 main 管道（macOS plugin_e2e_acceptance、Windows NSIS provisioning）均显红。新信息，非新破坏。
[查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5403)


## 重要 PR 进展（10 个）

**1. #5406 [feat] 第三方模型预制模板 + 测试连接**
实现 #5350。内置 OpenCode Zen、OpenCode Go、Agnes、SenseNova 模板，用户仅需填入 API 密钥。支持一键测试连接。直接降低新用户上手门槛。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5406)

**2. #5405 [feat] 模型可见读/工具结果大小预算可配置化**
实现 #5367。为自托管长上下文模型（如 DeepSeek V4）提供可选的更大单结果预算，减少大文件的多轮读取开销。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5405)

**3. #5404 [fix] SSE UTF-8 跨 HTTP/2 DATA 帧拆分时 fail-closed**
修复 #5374。Chat Completions SSE 在 HTTP/2 DATA 帧拆分多字节字符时使用 `from_utf8_lossy` 导致乱码，改为 fail-closed 策略。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5404)

**4. #5402 [fix] 恢复不可验证时的会话成本显示**
修复 #5241。不再永远显示 `unverified_live_pricing`；当 live pricing 无法验证时走诚实路径（不假装验证过，但恢复成本显示）。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5402)

**5. #5397 [fix] 网站上"宪法"改称"宪章"（已合并）**
跟进 #4949 决议。将网站文案中的 Constitution 中文翻译从"宪法"统一改为"宪章"，与 TUI 侧 `zh_hans_constitution_copy_uses_charter_term` 保持一致。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5397)

**6. #5400 [fix] 输出区填满终端全宽（已关闭）**
修复 #5322。`session_shell_area` 恢复 identity 语义，transcript 和 composer 重新铺满宿主宽度，回到 v0.8.65 行为。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5400)

**7. #5399 [fix] v0.9.8 稳定性：turn-owned agents、压缩质量、Blue Stage Web**
重构 v0.9.8 Rust 稳定性修补：默认直接子 agent 改为 turn-owned（避免跨 turn 状态泄漏），提升上下文压缩质量，修复 Blue Stage Web。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5399)

**8. #5395 [fix] CI：停止 cancel-in-progress 误杀并发 main 推送**
main 分支 CI 共享 concurrency group，后推的 commit 会取消前一个运行——失败断言永远不会变红。按 pull_request.number 区分组解决。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5395)

**9. #5394 [fix] 修复 v0.9.8 provider-count 断言与 Google ModelRegistry 漂移**
解决 #5383。CLI 断言仍持有 v0.9.8 发布前数字（43 vs 45 registry kinds），更新为最新数据；同时修复 Google ModelRegistry 漂移。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5394)

**10. #5396 [fix] macOS agy_credentials fixtures 规范化**
修复 #5392。`TempDir` 返回 `/var/folders/…` 而 `/var` 是符号链接，`O_NOFOLLOW` 拒绝所有路径组件中的符号链接导致测试失败。fixtures 改用规范化路径。
[查看 PR](https://github.com/Hmbown/CodeWhale/pull/5396)


## 功能需求趋势

| 趋势方向 | 代表 Issue/PR | 热度信号 |
|---------|--------------|---------|
| **第三方模型服务商接入简化** | #5350 / #5406 | 预制模板 + 测试连接，减少手动配置 |
| **长上下文模型支持增强** | #5367 / #5405 | 可配置化读/工具结果大小限制 |
| **沙箱/安全功能可配置化** | #5410 | bwrap 额外根目录配置 |
| **i18n 术语本地化讨论** | #4949 / #5397 | 24 条评论、持续三周、影响多端 |
| **架构可维护性重构** | #5316 (EPIC-005) | Crate 分解 Umbrella 追踪 |
| **Web 前端功能与稳定性** | #5370 / #5411 / #5398 | P0 bug + UI 打磨 |

**解读**：社区对**第三方模型配置的易用性**和**长上下文模型的效率**表现出最强烈的诉求。前者直指新用户入门摩擦，后者影响深度用户的日常使用成本。沙箱配置的灵活性和 i18n 用词的严谨性也在持续发酵。


## 开发者关注点

1. **CI 稳定性与信号可靠性**——两条 main 红牌（#5403 #5392）暴露了 CI 相互取消掩盖失败断言的问题；#5395 修复后 CI 信号才真正暴露问题，说明此前 CI"绿"可能包含假阳性。多个 PR 专注于解除 Lint/测试红牌（#5393 #5384 #5394 #5398）。

2. **Web UI 处于"损坏"状态**（#5370）——P0 级别的 Web 前端问题以及 #5337 的 `{ en, zh }` 内联字典尚未完全收敛，Web 端体验是当前短板。

3. **macOS 平台的稳定性痛点**——#5374（流式乱码）、#5392（测试失败）均为 macOS 特有，且有 symlink/路径语义绕不开的系统底层差异，需要更系统的平台适配策略。

4. **计费/成本显示不可靠**（#5241）——多个 provider 会话成本均为 `unverified_live_pricing`，定价端点 503，影响用户对成本的掌控感。

5. **好信号**——**社区讨论质量较高**：#4949 的翻译之争在开放讨论三周后顺利收敛；#5350 的 issue 作者提供了完整的中英双语描述和可操作建议，PR #5406 当日即提交实现。

---

*本日报由 AI 工具自动生成，数据采集于 GitHub 公开仓库，如有疏漏敬请指正。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*