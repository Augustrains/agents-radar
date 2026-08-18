# AI CLI 工具社区动态日报 2026-08-18

> 生成时间: 2026-08-18 00:29 UTC | 覆盖工具: 9 个

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

**报告日期：2026-08-18**


## 1. 生态全景

当前 AI CLI 工具已从"单命令辅助"演进为"多代理协作平台"，但**稳定性与可靠性成为各工具社区最集中的痛点**。桌面端与 CLI 行为不一致（Claude Code 跨会话消息丢失、Codex 远程恢复失败）、MCP 生态兼容性参差（OAuth 认证、BigInt 序列化、token 刷新）、子代理调度与内存控制失控（Gemini、DeepSeek TUI、Claude Code）是跨工具的普遍问题。与此同时，各工具官方正密集投入**企业级网络合规**（代理感知遥测、沙箱加固）与**多会话管理体验**（TUI dashboard、队列命令），显示竞争焦点正从"模型能力"转向"工程化基础"。社区对交互控制权（如禁用自动判定）和上下文/成本透明度的诉求持续高涨，成为影响用户采纳度的关键因素。


## 2. 各工具活跃度对比

| 工具 | 24h 活跃 Issues | 24h 活跃 PRs | 最新 Release | Release 频率 | 社区热度信号 |
|------|:---:|:---:|------|------|------|
| **Claude Code** | ~50+ | ~50+ | v2.1.234 | 高频（日更级） | 198 👍 消息队列；97 👍 Bash 工具选择 |
| **OpenAI Codex** | 50 | 50 | rust-v0.148.0-alpha.21 | 高频（alpha 周更） | 195 👍 禁用 60s 自动判定 |
| **Gemini CLI** | ~30+ | ~30+ | v0.56.0-nightly | 夜间构建 | P1 子代理终止误报；Generalist 挂起 |
| **Copilot CLI** | 29 | 1 | 1.0.80（8/15） | 低频（周更级） | 17 👍 SHIFT+ENTER；OAuth 回归 |
| **OpenCode** | 10+ | 10+ | V2 迭代中 | 高频 | 32 👍 Plan→Build 自动切换 |
| **Pi** | 10+ | 10+ | 持续迭代 | 高频 | 39 👍 XDG 合规；17 👍 auto-compaction |
| **Qwen Code** | 10 精选 | 10 精选 | v0.21.13（8/17） | 中频（周更+补丁） | P1 Ctrl+V 回归；压缩链路投诉集中 |
| **DeepSeek TUI (CodeWhale)** | 41 | 41 | v0.9.9 | 高频（发布周期） | 文档汉化 EPIC；CI 全红引发关注 |
| **Kimi Code CLI** | 0 | 0 | — | — | 24h 无任何活动 |


## 3. 共同关注的功能方向

### 3.1 多代理协作与调度可靠性（最强烈共识）
| 工具 | 具体诉求 |
|------|---------|
| Claude Code | 跨机器 Agent-to-Agent 协议（#28300）；消息队列模式（#50246，198 👍） |
| Codex | 子代理完成唤醒主代理（#15723）；远程线程恢复（#37403） |
| Gemini CLI | 子代理终止原因误报（#22323）；Generalist 无限挂起（#21409） |
| DeepSeek TUI | 子代理超时编排卡死（#1425）；builder 角色只读自锁（#5123） |
| OpenCode | `run --continue` 注入进行中会话（PR #43140） |

**核心结论**：多代理模式已全面进入生产使用，但"何时唤醒/如何传递状态/失败如何报告"仍未形成可靠范式，是各工具共同的工程短板。

### 3.2 上下文与成本管理
| 工具 | 具体诉求 |
|------|---------|
| Claude Code | 技能无条件吃满上下文（#63566，77% 暴增） |
| Codex | 60s 自动判定导致审阅时间不足（#28969，195 👍） |
| Pi | auto-compaction 触发过晚（#6879）；缓存缺失 2.5 倍成本惩罚（#7995） |
| Qwen Code | 连续压缩 token 计数异常（#9309）；压缩后上下文丢失（#9320） |
| DeepSeek TUI | 分时计价支持（#5470）；web 工具结果压缩（#5474） |

**核心结论**：所有工具都在努力"塞更多上下文"，但**用户开始要求对上下文使用和成本有精确掌控力**——压缩可靠性、token 统计准确性、成本透明度成为影响信任度的关键指标。

### 3.3 MCP 生态稳定性
| 工具 | 具体诉求 |
|------|---------|
| Codex | OAuth token 不自动刷新（#17265）；stdio 进程重复拉起（#38754） |
| Copilot CLI | OAuth 认证回归（#4480）；BigInt 序列化崩溃（#4211） |
| OpenCode | MCP 工具连接但不暴露（#33027） |
| Gemini CLI | 扩展环境变量注入风险（PR #28863） |
| Qwen Code | MCP 2026 支持推进中（#8992） |

**核心结论**：MCP 已成为标准协议，但**认证生命周期管理、序列化边界、进程生命周期**三大基础问题仍广泛存在，说明协议本身成熟度与工具实现质量之间存在较大落差。

### 3.4 会话/状态持久化
- **Claude Code**：跨会话消息丢失/静默丢弃（#86298、#86237，Windows/macOS 双平台回归）
- **Codex**：远程会话恢复失败（#37403）；`migrate-rollouts` 丢失历史（#38761/38762）
- **Copilot CLI**：恢复后 connection item ID 过期（#4505）
- **DeepSeek TUI**：审批持久化 fail-closed（#5491）；配置路径跨平台分叉（#2369）

### 3.5 非交互/CI 模式功能对齐
- **Copilot CLI**：`enabledPlugins` 在 `-p` 模式不生效（#4507）
- **OpenCode**：`run --continue` 并发会话误注入（#43140）
- **Gemini CLI**：TUI 在裸 Linux 终端挂起（#28812）


## 4. 差异化定位分析

### Claude Code — 功能最全、生态最深
- **侧重**：桌面应用 + 深度插件系统 + 沙箱
- **目标用户**：专业开发者/团队，追求 IDE 级体验
- **技术路线**：TypeScript/Node、内置沙箱 + 容器替代方案（PR #30692）
- **优势**：功能覆盖最广；**短板**：桌面端稳定性问题密集（GPU 崩溃、消息丢失）

### OpenAI Codex — 企业级 Rust 重写、代理网络能力最强
- **侧重**：Rust 原生性能 + 企业网络合规（代理感知遥测 6-PR 系列）+ TUI 多代理 dashboard
- **目标用户**：企业开发者、远程/移动办公场景
- **技术路线**：Rust（性能优先）、bubblewrap 沙箱 + capability drop
- **优势**：工程化投入坚决（9 个代理感知 PR 合并）；**短板**：桌面端与 CLI 行为不一致

### Gemini CLI — 模型能力驱动的轻量工具
- **侧重**：Sub-agent 模式 + Auto Memory + 扩展生态
- **目标用户**：Google 生态开发者、偏 CLI 优先
- **技术路线**：TypeScript、SSR Agent 批量修复 + gVisor 沙箱
- **优势**：模型能力强；**短板**：子代理稳定性问题持续 5 个月未根治

### Copilot CLI — 企业管控优先
- **侧重**：组织级策略（MCP 注册表策略、模型目录、enabledPlugins）+ 非交互 CI
- **目标用户**：GitHub 企业客户、CI/CD 场景
- **技术路线**：TypeScript、依赖 GitHub 生态
- **优势**：与 GitHub 深度集成；**短板**：迭代速度最慢、PR 流量极低（24h 仅 1 条）

### OpenCode — 社区驱动、快速试错
- **侧重**：V2 重写 + 插件系统 + 多 Provider 适配（Azure DeepSeek、Vertex）
- **目标用户**：开源社区、多模型用户
- **技术路线**：TypeScript、Bun、SQLite（WAL on network FS 修复，PR #43141）
- **优势**：迭代快、社区 PR 活跃；**短板**：Windows/ARM64 支持是明显短板

### Pi — 极客向、性能敏感
- **侧重**：性能优化 + 上下文压缩机制 + 模型目录及时性
- **目标用户**：性能敏感型开发者、自托管
- **技术路线**：性能深度优化（TUI 渲染修复、WAL 检测）+ 扩展 API
- **优势**：社区对底层问题的响应速度快；**短板**：UI 渲染性能问题集中

### Qwen Code — 国内生态 + WebShell
- **侧重**：Web Shell、多通道（微信）、国内代码平台（Aone）集成、自动化运维机器人
- **目标用户**：国内开发者、阿里云生态
- **技术路线**：TypeScript、自研 Autofix/Review 机器人
- **优势**：国内场景深覆盖；**短板**：压缩链路可靠性问题集中爆发

### DeepSeek TUI (CodeWhale) — 品牌重塑期、社区结构变化
- **侧重**：品牌从 DeepSeek-TUI 迁移至 CodeWhale、文档本地化、审批安全机制
- **目标用户**：中文用户为主、多第三方模型用户
- **技术路线**：Rust、TUI-first、DSH (DeepSeek Harness)
- **优势**：社区贡献活跃（第三方模型配置、审批持久化均有社区 PR）；**短板**：CI 全红、测试可靠性待提升


## 5. 社区热度与成熟度评估

| 梯队 | 工具 | 特征 |
|------|------|------|
| **成熟稳定期** | Claude Code | 社区体量最大、功能诉求最丰富（消息队列 198 👍），但桌面端稳定性问题拖累口碑 |
| **快速迭代期** | Codex / Gemini CLI / OpenCode / Pi / Qwen Code | 日更或周更 Release、官方高频响应、社区 PR 贡献活跃 |
| **平台管控期** | Copilot CLI | 迭代节奏放缓（24h 1 PR）、Issue 以企业管控和回归报告为主，社区贡献通道未打开（#39089 明确外部贡献政策） |
| **品牌重塑期** | DeepSeek TUI (CodeWhale) | 社区活跃度极高（41+41）、从个人项目迈向项目化治理，文档汉化和 CI 质量是当前焦点 |
| **静默期** | Kimi Code CLI | 24h 零活动，需关注是否处于版本间歇或项目停滞 |

**活跃度排序**：Claude Code ≈ Codex > DeepSeek TUI > Gemini CLI ≈ OpenCode > Pi ≈ Qwen Code > Copilot CLI > Kimi


## 6. 值得关注的趋势信号

### 6.1 "控制权归还用户"是当前最强社区情绪
- 195 👍 要求禁用 60s 自动判定（Codex）、198 👍 要求消息队列而非打断（Claude Code）、32 👍 要求 Plan/Question 自动切换（OpenCode）——**用户不满足于"AI 自主"，而是希望精确控制 AI 的干预时机**。对开发者而言，设计 agent 行为时需默认"保守确认"而非"激进自治"。

### 6.2 企业级网络与安全合规成为竞争新前线
- Codex 的 6-PR 代理感知遥测系列、Copilot CLI 的 MCP 注册表策略 fail-closed、Gemini CLI 的环境变量注入修复、OpenCode 的 WAL 网络文件系统检测——**各工具正在争夺企业市场的入场券**。安全敏感型团队选型时应优先评估沙箱能力、网络代理支持和策略管控粒度。

### 6.3 上下文与成本管理进入"精细调控"阶段
- Pi 的追加压缩（append compaction）实验、Qwen 的压缩边界问题、DeepSeek 的分时计价、Claude Code 的技能上下文占用——**"无限上下文"叙事已让位于"上下文预算管理"**。开发者应关注工具的压缩触发可配置性、token 统计准确性、以及 provider 缓存利用效率。

### 6.4 多代理调度可靠性是最大共性技术债
- 五个工具（Claude Code、Codex、Gemini、DeepSeek、OpenCode）同时出现子代理/后台任务相关的高热度 Issue：状态误报、唤醒失败、内存失控（单子代理 9.5 GiB OOM）、超时卡死——**"委托-执行-汇报"循环尚未形成可靠范式**。凡计划在 CI/CD 或自动化链路中使用多代理模式的团队，建议先验证工具的子代理失败恢复与超时处理能力。

### 6.5 跨平台一致性（尤其是 Windows）成为差异化竞争力
- Claude Code 的 Windows GPU 崩溃 + 消息丢失、Qwen 的 Windows Ctrl+V 回归、OpenCode 的 Windows ARM64 + ripgrep 失败、Codex 的 Windows MCP 进程泄漏——**Windows 支持质量正在成为用户流失/留存的关键分水岭**。Windows 重度用户选型时应重点考察目标工具在 Windows 上的已知 issue 列表及修复速度。

### 6.6 文档本地化与社区结构变化
- DeepSeek TUI（CodeWhale）启动全量文档汉化 EPIC、Claude Code 插件开发工具链密集完善、Codex 明确外部贡献政策——**各工具开始认真经营社区基础设施**。这一信号对开发者意味着：贡献门槛正在降低、插件生态将加速丰富、中文用户的支持体验在改善。


**编辑总结**：AI CLI 工具竞争已进入"下半场"——模型能力差距逐渐缩小，**稳定性、控制力、企业合规、跨平台一致性**成为用户留存的关键因素。对开发者而言，选型时除关注功能覆盖外，应重点考察目标工具对反馈的响应速度（从 Issue 修复周期可窥见）、社区活跃度（PR 数量与外部贡献比例），以及最核心的——**在长会话、多代理、受限网络等真实工作负载下的可靠性表现**。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-18）

## 1. 热门 Skills 排行

以下按社区关注度（Issue 关联、PR 讨论热度、⭐ 数）排序：

**① `skill-creator` 修复系列（#1298 / #556）**  
**功能：** `skill-creator` 是官方提供的技能创建/优化工具，本次 PR 修复其评测脚本 `run_eval.py` 在 Windows 下 0% 触发率的核心 bug（#556，10+ 独立复现），并改进触发检测与并行处理。  
**讨论热点：** 跨平台兼容性（Windows 子进程读取阻塞）、脚本信号可靠性（优化循环基于噪声运行）。  
**状态：** Open（PR #1298）；关联 Issue #556 持续有 12 条评论、7 👍，是当前社区最关心的工具链问题。

**② document-typography（#514）**  
**功能：** 排版质量检查 Skill——修复 AI 生成文档中的孤儿词（1-6 词溢出）、孤行段落（标题落在页底）、编号错位等视觉问题。  
**讨论热点：** 用户几乎不会主动要求的“最后 10%”打磨，但对交付质量提升显著；无需额外配置。  
**状态：** Open（PR #514），作者 PGTBoos。

**③ ServiceNow 平台 Skill（#568）**  
**功能：** 覆盖 ServiceNow 全平台（ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD/CSM、SPM/PPM、安全响应、IntegrationHub），定位为“平台助手”而非窄脚本工具。  
**讨论热点：** 企业级平台场景广度 vs 单一功能深度；如何避免 SKILL.md 过长导致上下文浪费（收到相关效率质疑）。  
**状态：** Open（PR #568），更新于 2026-08-12，仍活跃。

**④ self-audit（#1367）**  
**功能：** 交付前审计 Skill——先做机械式文件验证（声明输出的文件是否真实存在），再按伤害严重度优先级做四维推理审计（完整性/一致性/正确性/风险）。  
**讨论热点：** 直接把质量门禁做成可复用 Skill，欢迎度颇高；配套提案 #1385（三级质量门管线）有持续讨论。  
**状态：** Open（PR #1367）。

**⑤ pyxel 复古游戏开发（#525）**  
**功能：** 基于 pyxel-mcp 服务器，支持 Python 复古/像素风游戏开发（写代码 → 运行截图 → 检查 → 迭代）。  
**讨论热点：** 个人开发者将 MCP 服务器 + Skill 结合的最佳实践，小而美。  
**状态：** Open（PR #525），更新于 2026-07-15。

**⑥ testing-patterns（#723）**  
**功能：** 覆盖全套测试模式——测试哲学（Testing Trophy 模型）、单元测试（AAA、纯函数）、React 组件测试（Testing Library）等。  
**讨论热点：** 是否为开发者内建能力的重复包装？社区对“测试”类 Skill 的必要性有分歧。  
**状态：** Open（PR #723）。

**⑦ skill-quality-analyzer / skill-security-analyzer（#83）**  
**功能：** 两个元 Skill——质量分析（结构/文档/示例/资源五维评分）和安全分析（权限/依赖/越权检测）。  
**讨论热点：** Skill 本身的质量和安全治理，直接回应 #492 安全争议；但 PR 已停留 9 个月，推进缓慢。  
**状态：** Open（PR #83），更新于 2026-01-07。

**⑧ compact-memory（#1329）**  
**功能：** 用符号化标记（symbolic notation）压缩长时运行 Agent 的笔记与持久化记忆，减少上下文占用。  
**讨论热点：** 上下文窗口管理是最高频痛点，该 Skill 直接对症；但社区质疑符号化带来的可读性损失与推理退化。  
**状态：** 提案 Issue（#1329），9 条评论。

---

## 2. 社区需求趋势

从 Issues 排序（按评论数）提炼出四个最明确的方向：

1. **安全与信任边界（#492，43 评论，2 👍）**  
   社区技能发布在 `anthropic/` 命名空间下造成“官方误导”，用户可能因此授予社区技能过高权限。这是目前**讨论度最高的单点问题**，且与 #83 安全分析 Skill 直接相关。

2. **组织级技能共享（#228，16 评论，8 👍）**  
   企业用户希望像共享代码库一样共享 Skills，而非手动下载 .skill 文件再逐个上传。这是需求最强烈的**企业功能缺口**——8 个 👍 说明覆盖面广。

3. **工具链可靠性（#556，12 评论，7 👍）**  
   `run_eval.py` 在所有查询下 0% 触发率，导致 skill-creator 的优化循环完全失效。这与 PR #1298、#1099、#1050 构成同一事件链——**开发者在 Windows 上无法正常使用 Skill 工作流**。

4. **上下文窗口管理（#1487、#1329、#1175）**  
   当前最尖锐的问题：`claude-api` Skill 单次调用注入约 15.6 万 tokens，直接挤爆上下文（#1487）。加上 SharePoint 文档处理（#1175）和 compact-memory 提案（#1329），**“Skill 本身成为上下文杀手”** 已成为不可忽视的反模式。

---

## 3. 高潜力待合并 Skills

| Skill | PR | 特点 | 近况 |
|---|---|---|---|
| **ServiceNow 平台** | #568 | 企业级全平台、覆盖极广 | 8/12 仍在更新，活跃 |
| **self-audit** | #1367 | 质量门禁、跨技术栈通用 | 6/28 提出，配套提案 #1385 在讨论 |
| **document-typography** | #514 | 精准痛点、即装即用 | 3 月提出，评论持续，大概率合并 |
| **pyxel 游戏开发** | #525 | 作者为 pyxel-mcp 原作者，MCP+Skill 参考实现 | 7/15 更新，细节打磨中 |
| **testing-patterns** | #723 | 大而全的测试指南 | 4 月后停滞，若非合并可能关闭 |

另注意 **#1538（bring two skills back under Agent Skills spec）** —— 两个已存在技能不符合规范，说明**规范一致性**本身正在成为 PR 评审的硬门槛。

---

## 4. Skills 生态洞察

> **当前社区最集中的诉求是：工具链可靠性（Windows 兼容、评测脚本可信）与 Skill 引入的上下文/安全边界治理（防止“Skill 本身成为风险源”）——即社区在从“造更多 Skill”转向“把 Skill 这个机制造稳妥”。**

增长期（2025Q4–2026Q1）的大量新 Skill 提案热度正在下降，取而代之的是对已有 Skill 的修复、规范合规、安全审计和上下文占用控制的系统性关注。

---

# Claude Code 社区动态日报 — 2026-08-18

> 数据来源: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## 今日速览

- **v2.1.234 发布**：新增 `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量，支持为 transient 目录自定义短名称；新增 `selection:clear` 键位绑定动作。
- **桌面端跨会话消息丢失问题持续发酵**：Windows 和 macOS 平台均出现回归 bug（#86298、#86237），新版本 2.1.227 起消息只渲染不到达运行时队列。
- **多代理协作和消息队列模式成为社区最热门功能诉求**：#50246（消息队列）获得 198 👍 和 60 条评论；跨机器 Agent-to-Agent 协议持续受到关注。

---

## 版本发布

### v2.1.234（最新）

- **新增** `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量：为每个会话提供独立配置目录的宿主环境，可为 per-project transcript 目录选择简短名称
- **新增** `selection:clear` 键位绑定动作：可绑定一个键来清除应用内选择（in-app selection）

---

## 社区热点 Issues（精选 10 条）

### 1. 💡 [Feature Request] 消息队列模式 — 排队消息而非打断当前任务
- **Issue**: [#50246](https://github.com/anthropics/claude-code/issues/50246)
- **状态**: 已关闭 | **评论**: 60 | **👍**: 198
- **要点**: 当 Claude 正在处理任务时，用户想追加后续想法只能打断当前工作。建议增加消息队列模式，让 follow-up 消息排队等待当前任务完成后再处理。198 个 👍 表明这是社区当前最强烈的功能诉求之一，尽管 Issue 已关闭，讨论热度依然很高。

### 2. 🐛 [Windows] 桌面应用 GPU 进程崩溃，MSIX 包无法启动
- **Issue**: [#80444](https://github.com/anthropics/claude-code/issues/80444)
- **状态**: 开放 | **评论**: 39 | **👍**: 5
- **要点**: 桌面应用 v1.24012.1 在通过应用内 Browser tab 浏览时触发 GPU 进程崩溃（0x060C201E），崩溃后 MSIX 包进入不可启动状态（appxState=2），只能通过 Repair 恢复。已在两个 NVIDIA 驱动版本上复现。Windows 用户的严重稳定问题。

### 3. 💡 [Feature Request] 跨机器多代理协作（Agent-to-Agent 协议）
- **Issue**: [#28300](https://github.com/anthropics/claude-code/issues/28300)
- **状态**: 开放 | **评论**: 38 | **👍**: 0
- **要点**: 请求在多台机器之间实现 Agent 间直接的通信与协作协议，支持分布式多代理工作流。评论数达 38 条，社区对跨机器协作有切实需求，值得关注后续进展。

### 4. 🐛 [模型] 频繁使用 Bash 工具（sed/grep）而非内置工具（Read/Grep）
- **Issue**: [#19649](https://github.com/anthropics/claude-code/issues/19649)
- **状态**: 开放 | **评论**: 27 | **👍**: 97
- **要点**: 模型倾向于使用 Bash 的 sed/grep 而不是内置的 Read/Grep 工具，导致效率低下和权限频繁触发。97 个 👍 表明这是影响大量用户日常使用的模型行为问题，社区期待通过 prompt 或工具优先级策略改善。

### 5. 🐛 [Windows] 跨会话消息被静默丢弃 — 审批永不显示，约 5 分钟后过期
- **Issue**: [#86298](https://github.com/anthropics/claude-code/issues/86298)
- **状态**: 开放 | **评论**: 13 | **👍**: 1
- **要点**: 自桌面应用 v1.28929.0 起引入的回归：跨会话消息被挂起等待一个 UI 永远不会显示的审批，约 5 分钟后过期并静默丢弃。严重影响跨会话工作流。

### 6. 🐛 [macOS] Esc 退出 /btw 模式时误拒绝待处理的工具调用
- **Issue**: [#64568](https://github.com/anthropics/claude-code/issues/64568)
- **状态**: 开放 | **评论**: 10 | **👍**: 9
- **要点**: 在 `/btw` 模式中，如有待处理的 tool-use 权限请求，按 Esc 本应退出模式，却被路由到权限弹窗并拒绝了工具调用。用户意图只是退出模式，却意外取消了工具执行。已存在修复 PR（#61873），等待合入。

### 7. 🐛 [macOS] 文件系统 MCP 服务器在两种包世代中均不可用
- **Issue**: [#80094](https://github.com/anthropics/claude-code/issues/80094)
- **状态**: 开放 | **评论**: 9 | **👍**: 0
- **要点**: macOS 桌面版中 filesystem MCP server 存在 schema 调度问题——新 schema 从未分发，旧 schema 在注册时被丢弃，导致文件系统 MCP 功能在两个包版本中都无法使用。影响依赖文件系统 MCP 的用户。

### 8. 🐛 [桌面应用] 跨会话消息只渲染不到达运行时队列（回归 2.1.222 → 2.1.227）
- **Issue**: [#86237](https://github.com/anthropics/claude-code/issues/86237)
- **状态**: 开放 | **评论**: 8 | **👍**: 1
- **要点**: 桌面应用中跨会话消息渲染在目标会话 UI 中，但从未进入运行时输入队列。与 #86298 高度相关，是同一回归（2.1.222 → 2.1.227）的两个表现。

### 9. 🐛 [/claude-api 内置技能] 无条件吃满上下文 — 中性问题导致 ~77% 暴增
- **Issue**: [#63566](https://github.com/anthropics/claude-code/issues/63566)
- **状态**: 已关闭 | **评论**: 8 | **👍**: 9
- **要点**: `/claude-api` 技能被调用时不论问题内容，都将整个技能文档写入上下文，导致约 77% 的上下文被占据。与 #87191（加载多语言完整 bundle ~230k tokens）同族问题，已在最新版本中关闭。

### 10. 🧠 [内存] 单后台子代理在 ~100 秒内膨胀至 9.5 GiB 触发内核 OOM
- **Issue**: [#81343](https://github.com/anthropics/claude-code/issues/81343)
- **状态**: 开放 | **评论**: 5 | **👍**: 0
- **要点**: 单个非嵌套后台子代理（Task tool, `run_in_background: true`）在 103 秒内从 ~0 增长至 9.5 GiB anon-RSS，在 15.6 GiB Linux 主机上触发全局内核 OOM。后台子代理存在严重内存失控问题。

---

## 重要 PR 进展（精选 10 条）

### 1. 🔒 fix: ralph-wiggum 插件 — 阻止模型自我调用 /ralph-loop
- **PR**: [#87395](https://github.com/anthropics/claude-code/pull/87395) | 已关闭
- **内容**: 修复 `ralph-wiggum` 插件的 `/ralph-loop` 和 `/cancel-ralph` 命令使用不支持的 frontmatter 字段（`hide-from-slash-command-tool`），该字段实际不生效，模型可以自行调用 `/ralph-loop` 启动循环。改用 `disable-model-invocation` 阻止模型自我调用。

### 2. 🔧 fix: 从 init-firewall.sh 移除 statsig.anthropic.com
- **PR**: [#72451](https://github.com/anthropics/claude-code/pull/72451) | 已关闭
- **内容**: 域名 `statsig.anthropic.com` 已不再解析，但防火墙初始化脚本仍尝试解析并在失败时退出。该修复移除该域名，避免 devcontainer 启动失败。

### 3. 🔧 fix: validate-settings.sh 无匹配 lowercase frontmatter 键时不应中止
- **PR**: [#79131](https://github.com/anthropics/claude-code/pull/79131) | 开放
- **内容**: `validate-settings.sh` 在 grep 无匹配时返回 exit 1，`set -euo pipefail` 导致脚本无诊断信息地中止。该 PR 修复此问题，并报告被模式跳过的键（混合大小写或带连字符的键）。

### 4. 📦 feat: 添加容器隔离示例（含 guard hook）
- **PR**: [#30692](https://github.com/anthropics/claude-code/pull/30692) | 已关闭
- **内容**: 添加 `examples/container/` 完整配置，演示在 Podman/Docker 容器中运行 Claude Code 替代内置沙箱。包含 `guard-destructive-git` PreToolUse hook，可拦截 force push、hard reset、`rm -rf` 等危险操作。

### 5. 📖 docs: 说明 excludedCommands 需要 :* 后缀
- **PR**: [#29284](https://github.com/anthropics/claude-code/pull/29284) | 已关闭
- **内容**: 更新 `excludedCommands` 示例，使用 `"docker:*"` 替代空数组；在示例 README 中增加说明：`:*` 是匹配带参数命令的必要后缀。不带 `:*` 时 `"docker"` 只能匹配裸命令。

### 6. 🔧 fix(plugin-dev): 限制 frontmatter 解析范围
- **PR**: [#84004](https://github.com/anthropics/claude-code/pull/84004) | 已关闭
- **内容**: 修复基于范围的 `sed` 表达式在遇到后续 `---` 行时重新开始匹配的问题，只解析开头的 YAML frontmatter 块；拒绝无开头或结尾 frontmatter 标记的文件。

### 7. 🔧 fix(scripts): 顶层失败的正确传播
- **PR**: [#84003](https://github.com/anthropics/claude-code/pull/84003) | 已关闭
- **内容**: 两个 duplicate-maintenance 脚本使用 `.catch(console.error)` 导致启动和 API 失败被报告但 resolve 了 rejection。修复为返回失败的退出码，同时保留原始错误日志并允许输出 flush。

### 8. 🔧 fix(scripts): 校验 gh 标志值
- **PR**: [#83999](https://github.com/anthropics/claude-code/pull/83999) | 已关闭
- **内容**: 受限 `gh` wrapper 的解析器在输入末尾残留 `skip_next=true`，会转发 `gh issue list --limit` 等不完整命令。现在会拒绝缺少值的带值标志，防止绕过 wrapper 的校验。

### 9. 🔧 fix(scripts): 校验 label 选项值
- **PR**: [#83995](https://github.com/anthropics/claude-code/pull/83995) | 已关闭
- **内容**: 校验 `--add-label` 和 `--remove-label` 在读取下一个位置参数之前收到标签名。带 `set -u` 时无值调用会以 `$2: unbound variable` 中止；现在提前报错并避免吞掉后续选项。

### 10. 🔧 fix(plugin-dev): 断言预期的 hook 决策
- **PR**: [#83992](https://github.com/anthropics/claude-code/pull/83992) | 已关闭 | 修复 #83800
- **内容**: `test-hook.sh` 原本将 allow 和 deny 都视为成功执行，无法捕获"本应拒绝却放行"的 hook。新增 `--expect allow|deny|ask` 可选标志，使测试能断言 hook 的实际决策结果。

---

## 功能需求趋势

从近期 Issues 中提炼出社区最关注的功能方向：

### 1. 🔄 跨会话消息与异步工作流（最热门）
- **消息队列模式**（#50246，198 👍）— 在不打断当前任务的前提下排队 follow-up 消息
- **跨机器 Agent-to-Agent 协议**（#28300，38 条评论）— 多代理在不同机器上的直接协作
- 但桌面端跨会话消息丢失（#86298、#86237）是当前最大的稳定性障碍

### 2. 🖥️ 桌面应用稳定性（Windows/macOS 高频问题）
- Windows GPU 崩溃连锁反应（#80444、#85540）— 浏览器 tab 崩溃导致 MSIX 无法启动
- Windows 桌面端与 CLI 的权限数字键语义不一致（#73325）— 肌肉记忆导致误拒绝

### 3. 📦 技能与上下文管理
- `/claude-api` 技能无条件吃满上下文（#63566、#87191）— 上下文浪费是最大痛点
- 技能加载 `shared/` 下所有文件的非预期行为（#80190）

### 4. 🧠 模型工具选择优化
- 模型用 Bash 替代内置工具（#19649，97 👍）— 社区强烈期待工具选择的智能优化

### 5. 🔐 权限与安全
- 权限弹窗数字键位在 2 选项和 3 选项变体间不一致（#83567）— 需求稳定、可预期的交互

### 6. 📋 后台任务资源管理
- 后台子代理内存失控（#81343）— 单一子代理膨胀至 9.5 GiB 触发 OOM，需要资源上限或预警

---

## 开发者关注点

### 🔴 高频痛点

1. **桌面端跨会话消息丢失**（#86298、#86237）— 消息要么被静默丢弃、要么只渲染不进入队列，严重破坏跨会话工作流，且是 2.1.222 → 2.1.227 的回归
2. **GPU 崩溃引发连锁故障**（#80444、#85540）— MSIX 包崩溃后不可启动、需要 Repair 才能恢复，Windows 用户深受其扰
3. **上下文被技能无谓耗尽**（#63566、#87191）— 中性问题也能触发 ~77% 上下文飙升，高量 API 用户成本压力大
4. **权限交互不一致**（#73325、#83567）— CLI 和桌面端键位含义相反、2 选项和 3 选项弹窗数字键位不稳定，误操作风险高
5. **模型工具选择偏差**（#19649）— 偏好 Bash 替代内置工具，导致效率低下和权限频繁触发，97 个 👍 反映影响面广
6. **后台子代理内存失控**（#81343）— 单个后台子代理在约 100 秒内可达 9.5 GiB 并触发内核 OOM，需紧急关注

### 🟡 潜在风险

- `/btw` 模式的 Esc 键误拒绝工具调用（#64568）— 用户意图被误解，需要更精细的按键路由
- Fable 5 thinking blocks 在 VS Code 扩展 2.1.233 中返回空值（#86865）— 影响依赖思考块输出的开发者
- 嵌入式 ugrep 对复杂正则的挂起问题（#87129）— 与内置 ripgrep 的 53ms 形成鲜明对比

### 🟢 社区积极信号

- 插件开发生态活跃：多个 PR 都在完善插件开发的测试工具链（#83990–#84004），说明社区对插件开发体验有较高期待
- 安全实践在普及：容器隔离方案（#30692）和 guard hook 示例受到关注，表明用户对沙箱外运行的需求真实存在
- 社区对配置校验脚本的健壮性要求提升（#79131、#83999、#83995），说明用户已深度依赖这些工具

---

> **编辑注**：本期最值得关注的是桌面端跨会话消息丢失系列问题（#86298、#86237），该回归直接破坏了跨会话协作的基础能力，且影响 Windows/macOS 两个平台。另外，消息队列模式（#50246）虽然已关闭，但 198 个 👍 显示了社区对非侵入式异步交互的强烈需求，建议 Anthropic 在后续版本中正式回应此诉求。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-18

## 今日速览

今日 Codex 社区共更新 50 个 Issue 和 50 个 PR，最受关注的是 #28969（要求禁用 60 秒自动判定，👍 195）——该议题已持续两个月，反映出用户对交互控制权的强烈诉求。与此同时，官方在24小时内密集合并了 9 个与代理感知 HTTP 客户端相关的 PR（#39104-#39109），并发布了 `rust-v0.148.0-alpha.21` 新版本，说明团队正集中精力强化企业级网络代理与遥测能力。另外，社区对 `migrate-rollouts` 迁移工具的新缺陷反馈（#38761、#38762）值得关注，建议升级前留意。

## 版本发布

**rust-v0.148.0-alpha.21** 已发布，代码签名验证通过，本质上为 0.148.0-alpha.21 轮次的小步迭代更新。更多变更细节需关注仓库 Releases 页。

## 社区热点 Issues

### 1. [#28969] Add setting to disable the auto-resolve in 60 seconds for questions
- **热度**: 👍 195 · 💬 79 条评论
- **要点**: 用户要求为 Codex CLI 的“60 秒自动判定”问题（如权限申请、交互式确认）增加禁用开关。该功能对于那些需要在批准前仔细审阅代码变更的开发者而言至关重要。该问题创建于 6 月 18 日，至今仍为 OPEN 状态，且仍在持续收到评论，侧面反映出此交互模式影响的用户面极广。
- **链接**: [查看详情](https://github.com/openai/codex/issues/28969)

### 2. [#17265] Codex does not auto-refresh routed MCP OAuth tokens
- **热度**: 👍 57 · 💬 31 条评论
- **要点**: Codex 持久化了 MCP 服务器的 `refresh_token`，但不会在 access token 过期时自动刷新，导致 MCP 工具调用间歇性失败。这个问题持续了 4 个月仍未解决，说明 routed MCP 的 token 生命周期管理在实际使用中仍是痛点。
- **链接**: [查看详情](https://github.com/openai/codex/issues/17265)

### 3. [#37403] [macOS][regression] Remote Control / CLI thread: `already has an active writer`
- **热度**: 👍 17 · 💬 21 条评论
- **要点**: 8 月 7 日更新 ChatGPT Desktop 后，从手机远程控制 Mac 上的 CLI 线程会报 `already has an active writer` 错误。这是一个影响日常移动办公场景的回归问题；用户从移动端发起任务，回到桌面想继续操作时即触发。
- **链接**: [查看详情](https://github.com/openai/codex/issues/37403)

### 4. [#37403] Background subprocesses/subagents do not wake the calling agent
- **热度**: 👍 8 · 💬 18 条评论
- **要点**: 后台子进程/子代理完成后，无法唤醒调用方代理。这是一个多代理协作中的基础调度问题——主代理不会在子代理完成时被通知，导致任务流程卡住，影响自动化链路。
- **链接**: [查看详情](https://github.com/openai/codex/issues/15723)

### 5. [#31963] [App][i18n] zh-CN renders both xhigh and ultra reasoning efforts as “极高”
- **热度**: 👍 5 · 💬 10 条评论
- **要点**: 中文本地化将 `xhigh` 和 `ultra` 两种不同的 reasoning effort 都翻译成了“极高”，导致用户在 UI 上无法区分两者。虽然是小问题，但在配置不同档位时容易混淆，属于典型的本土化质量缺陷。
- **链接**: [查看详情](https://github.com/openai/codex/issues/31963)

### 6. [#33282] Codex Desktop create_thread does not inherit auto-approval mode for worktree tasks
- **热度**: 👍 5 · 💬 9 条评论
- **要点**: 桌面版为 worktree 任务创建新会话时不继承自动批准模式，导致自动化流程被权限弹窗打断。对于偏向无人值守运行的用户，这是一个很关键的权限继承问题，尤其影响大批量并行任务。
- **链接**: [查看详情](https://github.com/openai/codex/issues/33282)

### 7. [#38754] [Windows] Local stdio MCP servers repeatedly spawned and not reaped
- **热度**: 👍 2 · 💬 7 条评论
- **要点**: Windows 桌面版在单次任务中反复拉起 stdio MCP 服务器且不回收进程，造成资源泄漏与性能退化，长时间会话后可能拖垮系统。属于近期出现的新问题，但直接影响 MCP 重度用户。
- **链接**: [查看详情](https://github.com/openai/codex/issues/38754)

### 8. [#38518] [Windows] 350-800 MiB/s read loop and system-wide stutter
- **热度**: 👍 0 · 💬 6 条评论
- **要点**: Windows 桌面版在打开或切换会话时可能触发持续的高磁盘读取（350-800 MiB/s），导致系统卡顿。该性能问题影响面大但热度不高，属于需要尽快复现定位的系统级回归。
- **链接**: [查看详情](https://github.com/openai/codex/issues/38518)

### 9. [#38855] Type-invalid item_ reasoning IDs survive replay validation
- **热度**: 👍 0 · 💬 5 条评论
- **要点**: CLI 向自定义提供商发送请求时，持久化的 `item_` reasoning ID 类型非法，但重放校验未拦截，最终 OpenAI 端报 `rs_` 期望错误。此问题暴露了请求序列化与校验链路的不一致，影响自定义模型场景。
- **链接**: [查看详情](https://github.com/openai/codex/issues/38855)

### 10. [#38762 / #38761] `migrate-rollouts` 迁移工具缺陷（子代理历史丢失 + 会话名消失）
- **热度**: 👍 0 · 💬 各 2 条评论
- **要点**: 这两个 issue 分别报告了 `migrate-rollouts` 在迁移后导致子代理线程的投射历史为空、以及仅依赖 `session_index` 的线程名丢失。由于这是一个离线本地存储迁移工具，受影响用户可能在升级后遇到线程元数据不完整的问题，影响 0.148 系列升级。
- **链接**: [#38762](https://github.com/openai/codex/issues/38762) · [#38761](https://github.com/openai/codex/issues/38761)

## 重要 PR 进展

今日值得关注的核心 PR 集中在**代理感知 HTTP 客户端与遥测加固**（由 `celia-oai` 主导的系列工作）以及 **TUI 交互增强**（`copyberry[bot]` 系列）：

### 1. [#39113] Surface interactive requests in realtime conversations
- **内容**: 将执行、权限和补丁批准请求镜像到实时对话中，便于用户在 app 内直接处理；同时将用户输入与请求类交互也映射到实时会话。
- **价值**: 解决远程/实时会话中「看不到权限弹窗」的痛点，大幅提升移动端远程控制的流畅度。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39113)

### 2. [#39112] Make the agents overview an interactive task dashboard
- **内容**: 将 TUI 的 agents 概览页升级为交互式任务面板，支持启动任务、打开根会话、重命名、停止任务，并在宽终端上展示更多详情。
- **价值**: 将多 agent 管理从前端的静态状态列表变成可操作面板，适合复杂多任务场景。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39112)

### 3. [#39094] Add an agents overview dashboard to the TUI
- **内容**: 新增 `/agents` 命令，展示由 app-server 管理的全部根会话，并汇总子代理状态；支持搜索、导航和按项目/状态分组。
- **价值**: 让 CLI 用户获得与桌面端接近的多会话管理能力，是 TUI 发展的重要一步。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39094)

### 4. [#39092] Add a command to queue messages for existing sessions
- **内容**: 新增 `codex queue --thread <THREAD> --message <TEXT>` 子命令，通过 `thread/queue/add` API 向已有会话提交消息。
- **价值**: 为脚本化、自动化操作现有 Codex 会话提供了官方入口。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39092)

### 5. [#39102] Raise the GPT-5.6 maximum context window
- **内容**: 将 `gpt-5.6-sol`/`terra`/`luna` 的上下文窗口上限提升至 **872,000 tokens**；同时保留 Amazon Bedrock 兼容条目。
- **价值**: 对处理大型代码库的用户是直接利好；配合 Worktree 和 compaction 机制可支撑更长时间的单会话任务。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39102)

### 6. [#39101] Update rmcp to 3.1.2
- **内容**: 升级 `rmcp` 库（3.0.0 → 3.1.2），移除本地兼容层，使用原生 JSON-RPC 解码，并原生支持多轮工具结果、`input_required` SSE 与 OAuth 受保护资源元数据。
- **价值**: 减少自定义维护成本，同时增强与远端 MCP 服务器的协议兼容性。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39101)

### 7. [#39103] Drop capabilities from Linux sandbox processes
- **内容**: 在 bubblewrap 两种启动模式下均传递 `--cap-drop ALL`，并在内部沙箱阶段校验 capability 为空后才允许执行命令。
- **价值**: 收紧了 Linux 沙箱的默认安全边界，对安全敏感型企业用户是好消息。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39103)

### 8. [#39091] [otel proxy 6/6] Propagate proxy policy into elevated Windows telemetry
- **内容**: 这是 6 个 PR 组成的 [otel proxy] 系列的最后一部分：将出站代理策略传递至 Windows 提权沙箱的遥测配置，并保持旧 payload 的向后兼容。
- **价值**: 配合 #39105-#39109 共同解决企业网络下的 OTLP 数据上报问题。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39091)

### 9. [#39098] Trace exec-server requests from receipt through completion
- **内容**: 在 exec-server 中从入站消息排队开始创建请求 span，贯穿到分发与响应处理，覆盖网络策略回调的错误记录。
- **价值**: 为排查远程执行链路问题提供了关键的可观测性基础。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39098)

### 10. [#39089] Clarify the external contribution policy
- **内容**: 明确外部贡献政策：优先接受高质量的 issue 报告、复现步骤、日志与分析；外部代码提交需要更多架构与路线图背景，可能分散维护者精力。
- **价值**: 对社区贡献者是一次重要预期管理，帮助大家更有效地参与开源协作。
- **链接**: [查看详情](https://github.com/openai/codex/pull/39089)

## 功能需求趋势

从过去 24 小时更新的 50 个 Issue 中可以提炼出以下社区功能诉求方向：

### 1. 交互控制与权限（高热度）
- 代表 Issue: #28969（禁用 60 秒自动判定）、#33282（auto-approval 继承）
- 核心诉求：用户希望对「何时需要人工确认」拥有更细粒度的控制权，尤其是在批量或远程执行场景中，自动批准模式的行为不一致是主要痛点。

### 2. 多会话与远程协作管理（高活跃）
- 代表 Issue: #37403（远程恢复线程失败）、#23418（远程工作树线程未关联项目侧栏）
- 核心诉求：围绕「移动端发起 → 桌面端继续」的跨设备工作流，各类关联性、状态同步、以及回归问题频发；同时用户希望桌面端侧栏对远程创建的线程有更好的项目关联和可见性。

### 3. MCP 生态稳定性（中高活跃）
- 代表 Issue: #17265（OAuth token 不刷新）、#38754（stdio 进程重复拉起）、#33599（node_repl MCP 工具未附加）
- 核心诉求：MCP 服务器接入的可靠性——token 刷新、进程生命周期、工具挂载一致性——仍是企业级接入的主要障碍；值得注意的是，桌面端与 CLI 对同一份配置的表现不一致（Issue #33599）尤其让用户困扰。

### 4. 本地化与可访问性（长尾）
- 代表 Issue: #31963（zh-CN 翻译混淆 reasoning 档位）
- 核心诉求：非英语用户对本地化质量开始提出更高要求，不再满足于「能显示中文」，而是要求准确传达技术语义差异。

### 5. 环境安全与网络合规（新动向）
- 代表 Issue: #39085（文档推荐了不安全的 prefix 规则）、#39103（沙箱 capability 收紧）
- 核心诉求：社区开始对沙箱安全边界和文档示例的「正确性」提要求，说明 Codex 的使用场景正在从个人电脑扩展至对安全合规有明确要求的企业环境。

## 开发者关注点

### 1. “60 秒自动判定”成为最大争议点
`#28969` 获得 195 个 👍 和 79 条评论，是当前社区情绪最集中的议题。开发者普遍反映：Codex 在生成代码或执行命令前的等待窗口中，自动判定（auto-resolve）导致他们没有足够时间审阅内容；而在大模型生成速度越来越快的情况下，这个时间窗口对代码审查质量的影响愈发显著。诉求是提供「禁用自动判定」的配置项，让用户在需要时手动确认。

### 2. 多代理协作的调度可靠性不足
`#15723`（子代理完成未唤醒主代理）和 `#13491`（Forked Worker 误继承父级用户意图）共同指向一个深层问题：Codex 的多代理调度在「何时唤醒」、「如何传递上下文」上仍不稳定。开发者希望子代理完成后能可靠地唤醒调用方，且 worker 不应错误地将用户意图当作直接指令执行。

### 3. 桌面端与 CLI 行为不一致
多个 Issue（如 #33599 桌面端无法附加 node_repl MCP 工具而 CLI 正常、#33282 桌面端不继承 auto-approval 模式）表明：同一份配置文件在 CLI 与桌面端之间的行为差异正在造成实际困扰。对于同时使用两种入口的开发者，配置「一处生效、另一处不生效」的排查成本较高。

### 4. 新模型（GPT-5.6 系列）行为回归
`#39059` 提出的问题值得警惕：GPT-5.6 Codex 在成熟生产代码库上倾向于「自我强化地构建验证与治理层」，即不断添加检查、验证和抽象层，反而拖慢任务进度。这与开发者期望的「直接完成业务改动」相悖，可能意味着新模型在默认参数下过于保守。

### 5. 迁移工具（migrate-rollouts）的稳定性存疑
`#38761` 和 `#38762` 在两天内先后报告了迁移后线程名丢失与子代理历史为空的问题。对于计划升级到 0.148 系列的团队，建议在迁移前做好线程级备份，并关注官方后续补丁。

---

**日报观察**: 今日的 PR 动向表明官方正在两条主线发力——**企业级网络合规**（代理感知的遥测与 HTTP 客户端）与 **TUI 多代理交互能力**（agents dashboard、queue 命令）。前者面向安全审查严格的大型企业，后者则服务于越来越复杂的多任务并行场景。社区的诉求则集中在「把控制权还给用户」——无论是禁用自动判定、恢复远程会话，还是让子代理可靠地唤醒调用方。两者方向略有错位，但 TUI 的交互式 dashboard 有望部分缓解多会话管理的痛点，值得期待下个稳定版。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-18** | **数据来源：github.com/google-gemini/gemini-cli**


## 今日速览

今日社区动态主要围绕 **Sub-agent（子代理）稳定性** 与 **终端交互体验** 两大核心展开。官方通过 SSR Agent 批量合入了多项针对子代理终止原因误报、Shell 命令挂起和自动补全体验的修复；社区侧则持续关注 Generalist Agent 挂起、浏览器代理（Wayland 环境）兼容性及 Auto Memory 内存系统的高频问题。安全方面，一份关于扩展环境变量注入的 PR 也引起了关注。


## 版本发布

### v0.56.0-nightly.20260817.g9a15c45fb

**更新内容：** 本次仅包含一项 SSR Agent 的修复——为 `packages/cli` 的 tsconfig 添加 `composite` 标志（PR #28813），解决构建相关配置问题。未包含其他功能性变更。

**详细变更：** https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260816.g2a87e7be1...v0.56.0-nightly.2


## 社区热点 Issues（Top 10）

### 1. Subagent 恢复后终止原因被误报为成功
- **Issue #22323** | [priority/p1, kind/bug] | 评论 12 | 👍 2
- **问题：** `codebase_investigator` 子代理在达到 `MAX_TURNS` 上限后，恢复流程将其终止原因错误地报告为 `"GOAL"`（成功），掩盖了实际的中断，导致用户误以为任务成功完成。
- **社区反应：** 关注度高，已进入 `need-retesting` 阶段；官方 PR #28815 已提交修复，正在验证。
- https://github.com/google-gemini/gemini-cli/issues/22323

### 2. Generalist Agent 无限挂起
- **Issue #21409** | [priority/p1, kind/bug] | 评论 8 | 👍 8
- **问题：** 当 Gemini CLI 委派任务给 generalist agent 时（即使是创建文件夹这类简单操作），代理会无限期挂起，用户等待长达一小时仍无响应。手动禁止使用子代理可绕过此问题。
- **社区反应：** 社区呼声最高的 Bug 之一，👍 数高；已持续 5 个月未彻底解决，用户影响面较大。
- https://github.com/google-gemini/gemini-cli/issues/21409

### 3. Shell 命令执行后卡在 "Waiting input" 状态
- **Issue #25166** | [priority/p1, kind/bug, effort/medium] | 评论 4 | 👍 3
- **问题：** 极其简单的 CLI 命令执行完毕后，终端仍显示命令处于活动状态并提示 "Awaiting user input"，但实际命令早已结束，导致会话卡死。
- **社区反应：** 反映该问题可复现且频率较高，影响日常使用体验。
- https://github.com/google-gemini/gemini-cli/issues/25166

### 4. 组件级评估体系（EPIC）
- **Issue #24353** | [priority/p1, kind/customer-issue] | 评论 7
- **内容：** 作为行为评估体系的后续 EPIC，计划在现有 76 个行为评估测试基础上，为 6 个受支持的 Gemini 模型建立更健壮的组件级评估框架。
- **社区反应：** 官方内部重点项目，虽无外部直接反馈但有持续跟踪。
- https://github.com/google-gemini/gemini-cli/issues/24353

### 5. AST 感知的文件读取、搜索与代码库映射评估（EPIC）
- **Issue #22745** | [priority/p2, kind/feature] | 评论 7
- **内容：** 跟踪调研 AST（抽象语法树）感知工具在文件读取、搜索和代码库映射方面的价值，旨在减少 token 消耗和轮次浪费。
- **社区反应：** 对提升大仓库场景下的性能和效率有潜在价值，官方在持续跟踪（关联 Issue #22746）。
- https://github.com/google-gemini/gemini-cli/issues/22745

### 6. Gemini 对自定义 Skills 和 Sub-agents 使用不足
- **Issue #21968** | [priority/p2, kind/bug] | 评论 6
- **问题：** 用户反馈 Gemini 几乎不会主动使用用户自定义的 skills 和 sub-agents，即使任务高度相关（如用户配置了 gradle、git 等 skills），只有在显式指示时才会调用。
- **社区反应：** 该反馈直接影响自定义扩展生态的价值发挥，属体验类核心痛点。
- https://github.com/google-gemini/gemini-cli/issues/21968

### 7. Auto Memory 对低信号会话无限重试
- **Issue #26522** | [priority/p2, kind/bug] | 评论 5
- **问题：** Auto Memory 仅在提取代理成功读取会话记录后才将其标记为已处理。若代理因内容价值低而跳过某会话，该会话将反复出现在待处理队列中，导致无限重试和资源浪费。
- **社区反应：** 内存系统稳定性问题，官方已跟踪并有相关改进计划。
- https://github.com/google-gemini/gemini-cli/issues/26522

### 8. 确定性脱敏与 Auto Memory 日志精简
- **Issue #26525** | [priority/p2, area/security, kind/bug] | 评论 4
- **问题：** Auto Memory 在将本地转录发送至模型前未进行确定性脱敏（依赖提示词事后脱敏存在泄露风险），且服务可能记录已存在的 skill 内容，存在安全隐患。
- **社区反应：** 安全性相关，社区关注度较高（安全类问题通常有较高优先级）。
- https://github.com/google-gemini/gemini-cli/issues/26525

### 9. 浏览器代理 Wayland 环境失败
- **Issue #21983** | [priority/p1, kind/bug, agent/browser] | 评论 4 | 👍 1
- **问题：** Browser subagent 在 Wayland 显示服务器环境下运行失败，且终止原因同样被误报为 "GOAL"。
- **社区反应：** 与 Issue #22323 同类（终止原因误报），影响 Linux/Wayland 用户群。
- https://github.com/google-gemini/gemini-cli/issues/21983

### 10. 代理模式禁用后 Subagents 仍被调用
- **Issue #22093** | [priority/p2, kind/bug] | 评论 3 | **已关闭**
- **问题：** v0.33.0 起，即使配置中设置了 agents 模式为 disabled，子代理（如 generalist）仍会被初始化并调用，该行为在今日已被修复（PR #28867）。
- **社区反应：** 已解决，修复合入后关闭。
- https://github.com/google-gemini/gemini-cli/issues/22093


## 重要 PR 进展（Top 10）

### 1. 修复：子代理恢复后保留原始终止原因（#28815）
- **状态：** 已合并 | [priority/p1, area/agent]
- **内容：** 修复 #22323。子代理在达到 `MAX_TURNS` 或 `TIMEOUT` 后，若在最后的宽限恢复轮次中成功调用 `complete_task`，现在会保留原始的终止原因（如 `MAX_TURNS`），而不是被覆盖为 "GOAL"。
- **意义：** 解决子代理中断被误报为成功的问题，提升执行透明度。
- https://github.com/google-gemini/gemini-cli/pull/28815

### 2. 修复：禁用代理模式下子代理仍被调用（#28867）
- **状态：** 已合并 | [priority/p2, area/agent]
- **内容：** 修复 #22093。`loadBuiltInAgents()` 原本在检查模式配置前就被调用，现已调整顺序，确保在 agents 模式被禁用时不再加载子代理。
- **意义：** 遵循用户配置意图，修复 v0.33.0 引入的回归。
- https://github.com/google-gemini/gemini-cli/pull/28867

### 3. 修复：ACP 模式下工具调用前缺少 pending 状态更新（#28870）
- **状态：** 开放 | [priority/p1, area/core]
- **内容：** 修复 #21783。在 ACP 模式下，当工具需要用户确认时，代理现在会先发送 `tool_call` 更新（pending 状态），再发送 `session/request_permission`，避免客户端因顺序错误而误判。
- **意义：** 完善 ACP 协议实现，提升集成兼容性。
- https://github.com/google-gemini/gemini-cli/pull/28870

### 4. 修复：gVisor runsc 沙箱主机网络解析（#28869）
- **状态：** 开放 | [priority/p2, area/extensions]
- **内容：** 修复 #21331。解决在 `GEMINI_SANDBOX=runsc`（gVisor）沙箱下，VSCode IDE 扩展因主机 TCP 网络受限而无法连接的问题。
- **意义：** 恢复 gVisor 沙箱场景下 IDE 集成能力。
- https://github.com/google-gemini/gemini-cli/pull/28869

### 5. 修复：自动补全添加尾随空格（#28868）
- **状态：** 已合并（已关闭） | [priority/p2, area/core]
- **内容：** 修复 #23954。从自动补全建议中选择可执行命令时，现在会自动添加尾随空格，用户可直接按 Enter 执行。
- **意义：** 优化日常终端交互效率。
- https://github.com/google-gemini/gemini-cli/pull/28868

### 6. 安全加固：MCP 扩展环境变量注入防护（#28863）
- **状态：** 开放 | [size/m, status/need-issue]
- **内容：** 修复扩展更新可绕过用户同意检查、向 MCP 服务进程注入未经授权的环境变量的问题。将 MCP 服务端环境配置纳入同意字符串生成，并净化自定义环境变量。
- **意义：** ⚠️ 安全性提升，防止恶意扩展利用环境变量实施攻击。
- https://github.com/google-gemini/gemini-cli/pull/28863

### 7. 修复：MessageBus.request 发布失败导致静默挂起（#28816）
- **状态：** 已合并 | [priority/p2, area/core]
- **内容：** 修复 #22588。`MessageBus.request()` 中 `publish()` 为浮动 Promise 且未注册失败处理，若发布失败会导致 60 秒静默挂起。现已补充失败处理机制。
- **意义：** 消除系统级静默挂起隐患。
- https://github.com/google-gemini/gemini-cli/pull/28816

### 8. 修复：TUI 在裸 Linux 终端无限挂起（#28812）
- **状态：** 已合并 | [priority/p1, area/core]
- **内容：** 修复 #21477。从裸 Linux 终端启动时，TUI 在 "Initializing..." 阶段无限挂起（`getProcessInfo()` 调用 `execAsync` 执行 `ps` 时卡死）。已添加执行超时机制。
- **意义：** 提升无完整终端环境下的启动可靠性。
- https://github.com/google-gemini/gemini-cli/pull/28812

### 9. 修复：默认忽略 .gemini 目录（#28866）
- **状态：** 开放 | [priority/p1, area/agent]
- **内容：** 修复 #28826。在 `loadIgnoreRules` 默认忽略规则中新增 `.gemini` 目录，避免在包含该配置目录的工作区中触发 chokidar 文件监听器异常。
- **意义：** 避免配置文件目录被误扫描。
- https://github.com/google-gemini/gemini-cli/pull/28866（社区贡献）

### 10. 文档修复：补充 Vertex AI 区域列表链接（#28865）
- **状态：** 已合并（已关闭） | [priority/p3, area/documentation]
- **内容：** 修复 #28050。认证文档中 `GOOGLE_CLOUD_LOCATION` 环境变量部分新增官方支持区域列表的链接。
- **意义：** 完善 Vertex AI 配置文档指引。
- https://github.com/google-gemini/gemini-cli/pull/28865


## 功能需求趋势

从过去 24 小时更新的 Issues 中，社区最关注的功能方向可归纳为以下五类：

| 方向 | 代表 Issue | 诉求要点 |
|------|-----------|---------|
| **Agent 稳定性与可靠性** | #22323（终止原因误报）、#21409（Generalist 挂起）、#25166（Shell 卡死） | 子代理执行状态透明、不误报；命令执行不挂起；恢复机制更健壮——这是当前最集中的痛点 |
| **AST 感知的代码理解** | #22745、#22746 | 探索利用 AST 进行文件读取与方法边界定位，以减少 token 消耗、提升搜索准确性，降低大仓库场景下的轮次浪费 |
| **安全与隐私加固** | #26525（脱敏）、#28863（环境变量注入） | 对发送至模型的内容做确定性脱敏而非依赖提示词；MCP 扩展的权限管控需加强 |
| **记忆系统（Auto Memory）质量** | #26522（无限重试）、#26523（无效补丁）、#26516（整体质量） | 低信号会话处理策略、无效内存补丁的隔离与提示、整体提取质量提升 |
| **浏览器代理增强** | #22232（自动接管与锁恢复）、#21983（Wayland 失败） | 浏览器 profile 锁的自动恢复而非 fail-fast；Wayland 兼容性修复 |

此外，#24246（>128 工具的 400 错误）、#23571（随机位置创建临时脚本）等也反映出核心工具链层面的稳定性诉求。


## 开发者关注点

1. **子代理状态透明化（高频痛点）**：多个高赞 Issue（#22323、#21409、#21983）均围绕子代理执行状态不透明或误报展开。开发者希望对代理内部执行（如 `MAX_TURNS` 中断、工具调用详情）有更清晰的可见性，而非被"成功"状态误导。关联需求 #22598 还建议 `/chat share` 能包含子代理轨迹以便审查。

2. **Shell 执行与终端交互体验**：#25166 反映命令执行完毕后界面卡死（"Waiting input"），#23954 则暴露自动补全缺少尾随空格需手动补键的问题。开发者对日常终端操作流畅度的要求很高，此类交互细节虽小但直接影响使用效率（后者已修复）。

3. **安全边界意识增强**：#26525 揭示 Auto Memory 在将本地转录发送至模型前缺少确定性脱敏（即使提示词要求脱敏，内容已在模型上下文中）；#28863 则关注 MCP 扩展可能注入未经同意的环境变量。开发者对数据流向和扩展权限越来越敏感。

4. **Auto Memory 稳定性**：低信号会话无限重试（#26522）、无效内存补丁被静默跳过（#26523）等问题显示内存系统当前对异常场景缺少保护机制，需要更明确的兜底策略。

5. **工具使用策略**：#21968 反映 Gemini 对自定义 skills/sub-agents 的主动调用不足，用户期待 CLI 能更智能地利用本地配置好的工具链，而非必须显式指示。

---

> 📌 **数据说明：** 本报告基于 GitHub Issues/PR 元数据（标题、标签、评论数、👍 数）自动生成，摘要信息来自原始提交描述。部分 PR 的评论数因 API 限制未能获取（显示为 undefined）。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-18

## 今日速览

本周期社区反馈集中在三个方向：MCP（Model Context Protocol）生态兼容性问题（OAuth 认证失败、BigInt 序列化缺陷）、会话管理的可靠性（恢复失败、内存看门狗误触发、指令热加载缺失）、以及模型上下文窗口（AIC）计费显示不准。值得关注的是，`--no-alt-screen` 标志被静默移除引发用户强烈不满，同时非交互模式（`copilot -p`）与交互模式行为不一致的问题被多次提及。

---

## 版本发布

过去 24 小时内无新版本发布。当前最新版本为 1.0.80（2026-08-15 前后发布），多个 Issue 已针对该版本提出回归问题。

---

## 社区热点 Issues（Top 10）

### 1. [OPEN] Atlassian MCP OAuth 认证失败 — 1.0.79 回归（#4480）
**👍 6 | 💬 5 条评论**
从 1.0.71 升级到 1.0.79 后，连接 Atlassian 远程 MCP 服务器（`mcp.atlassian.com`）时 OAuth 发现流程报 `Incompatible authorization server (RFC 8414 §3.3)`。与此前的 GitLab MCP 认证问题（#4439，已关闭）属于同一类回归，社区怀疑是 OAuth 元数据解析逻辑变更导致的兼容性收窄。
**链接**: https://github.com/github/copilot-cli/issues/4480

### 2. [CLOSED] SHIFT+ENTER 误触发执行而非换行（#1481）
**👍 17 | 💬 28 条评论**
该 Issue 历时 6 个月后于本周期关闭。用户强烈期望遵循聊天应用通用交互习惯（SHIFT+ENTER 换行、CTRL+ENTER 提交），但当前实现相反。虽然已关闭，但 28 条评论说明该交互设计长期困扰用户。
**链接**: https://github.com/github/copilot-cli/issues/1481

### 3. [OPEN] 组织启用的模型（Claude Sonnet 5/Kimi K3）从模型目录中缺失（#4390）
**👍 7 | 💬 8 条评论**
Copilot Business 组织显式启用的模型在 Copilot CLI 中不可用，选择 `claude-sonnet-5` 时报 `This model is disabled by your organization`。涉及模型目录同步机制缺陷，影响企业用户采用。
**链接**: https://github.com/github/copilot-cli/issues/4390

### 4. [OPEN] `--no-alt-screen` 被静默移除且无替代方案（#4509）
**👍 1 | 新提交**
自 3 月起多次报告（#1799、#2334）的 alt-screen 问题未解决，且用户发现 `--no-alt-screen` 标志被直接删除，无弃用通知。社区认为这是对用户选择权的无视，要求恢复或提供替代设置项。
**链接**: https://github.com/github/copilot-cli/issues/4509

### 5. [OPEN] MCP 结构化响应中的 BigInt 序列化崩溃（#4211）
**👍 2 | 💬 4 条评论 | 已标记 triaged**
当 MCP 服务器返回大整数时，CLI 抛出 `TypeError: Do not know how to serialize a BigInt`，导致所有进行中的任务中止。这是 MCP 工具结果处理中的基础类型支持缺口，影响金融、科学计算类工具的可用性。
**链接**: https://github.com/github/copilot-cli/issues/4211

### 6. [OPEN] 内存压力看门狗在 23% 上下文占用时强制压缩且无效循环（#4506）
**新提交**
长会话场景下，进程内存高时看门狗强制压缩对话（即使上下文仅占用 23%），压缩后仅回收 0.003% token，然后继续触发压缩直到 OOM。设计缺陷导致资源浪费和会话不可用。
**链接**: https://github.com/github/copilot-cli/issues/4506

### 7. [OPEN] 仓库级 enabledPlugins 在 `copilot -p` 非交互模式中不生效（#4507）
**新提交 | 标记 area:non-interactive**
`.github/copilot/settings.json` 中的 `enabledPlugins` 在交互模式和 `plugins list` 中正常，但在非交互模式下被忽略。接口间行为不一致，阻碍 CI/CD 场景的插件使用。
**链接**: https://github.com/github/copilot-cli/issues/4507

### 8. [OPEN] 会话恢复后出现连接项 ID 过期错误（#4505）
**新提交**
恢复已有会话后，所有提示词报 `CAPIError: 400 input item ID does not belong to this connection`，`/fork` 也无法恢复。会话持久化机制存在状态一致性问题。
**链接**: https://github.com/github/copilot-cli/issues/4505

### 9. [OPEN] MCP 注册表策略获取失败时阻止所有本地 stdio 服务器（#4512）
**新提交 | 标记 triage**
当 MCP 注册表策略获取失败时，CLI 默认 fail-closed，阻止用户自行定义的本地 stdio MCP 服务器运行。用户认为本地子进程不应受远端策略影响，建议 fail-open 或增加配置项。
**链接**: https://github.com/github/copilot-cli/issues/4512

### 10. [OPEN] 会话 AIC 显示不准确（Kimi K3 低估消费）（#4511）
**新提交 | 标记 triage**
用户报告 Kimi K3 会话的 AIC（上下文用量）显示严重低估实际消耗。影响用户对成本的感知和预算管理。
**链接**: https://github.com/github/copilot-cli/issues/4511

---

## 重要 PR 进展

过去 24 小时内仅 1 条 PR 更新：

### [OPEN] 从 README 中移除 Copilot CLI 文档（#4510）
创建者提出移除 README 中的详细安装和使用说明。**风险点**：若合入将影响新用户的入门路径。当前无评论与评审动态，可能是文档迁移策略调整的一部分。
**链接**: https://github.com/github/copilot-cli/pull/4510

> 注：本周 PR 流量较低，社区焦点集中在 Issue 反馈。欲了解完整 PR 列表请关注后续动态。

---

## 功能需求趋势

基于全部 29 条活跃 Issue，社区最关注的功能方向为：

| 方向 | 代表 Issue | 关注度 |
|------|-----------|--------|
| **MCP 生态兼容性** | #4480（OAuth）、#4211（BigInt）、#4515（结构化内容）、#4512（失败策略） | 🔥 高 — 4 条相关 Issue，覆盖认证、序列化、策略三个层面 |
| **会话管理与状态** | #4505（恢复失败）、#4506（看门狗压缩）、#4461（Docker 容器泄漏）、#4508（指令热加载） | 🔥 高 — 4 条相关，均为长期会话场景的实际痛点 |
| **非交互模式一致性** | #4507（插件）、#4275（contextTier）、#4504（quota） | 中 — 3 条，反映 CI/CD 用户对功能对齐的需求 |
| **多模型/新模型支持** | #4390（模型目录）、#4459（auto 模式失败） | 中 — 2 条，企业用户对最新模型（如 Kimi K3）的支持需求 |
| **可访问性与交互体验** | #4509（alt-screen）、#4455（对比度）、#4313（历史滚动）、#4485（主题切换） | 中 — 4 条，UI/UX 细节长期积压 |
| **插件体系增强** | #4487（依赖解析）、#4513（缓存 ref 隔离） | 中 — 2 条，插件市场机制尚不成熟 |

---

## 开发者关注点

1. **回归问题频发**：1.0.79 版本引入的 OAuth 兼容性回归（#4480、#4439）以及早前版本功能被静默移除（#4509），让开发者对版本升级持谨慎态度。GitHub 官方需加强版本发布的回归测试力度。

2. **长期会话可靠性不足**：#4505、#4506、#4508 共同指向一个核心问题——长生命周期会话（跨天、跨压缩）的状态管理和指令更新机制不成熟。对于将 Copilot CLI 作为日常主力工具的开发者，这是影响信任度的关键缺口。

3. **非交互模式体验落后**：`copilot -p` 在插件、contextTier 配置上与交互模式不一致。随着 CI/CD 流水线集成需求增长，这一差距会越来越突出。

4. **MCP 服务器治理缺乏灵活性**：本地定义的 MCP 服务器受远端策略影响（#4512）、Docker 容器未随会话清理（#4461），表明 MCP 的生命周期管理与信任边界设计需要更精细的控制粒度。

5. **计费透明度需求上升**：#4511（AIC 显示不准）、#4504（quota resetDate 错误）表明用户越来越关注成本管控，对用量数据的精确性有更高期望。

---

*本日报由 AI 技术分析师自动生成，数据截至 2026-08-18 00:00 UTC。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-18

## 今日速览

今日社区活跃度维持高位，核心动态集中在 **V2 版本的协议正确性与跨平台兼容性修复**：一方面，Azure DeepSeek 模型适配、MCP 工具暴露等老问题迎来对应 PR；另一方面，`opencode run --continue` 会话注入、Windows 原生二进制等新晋 Bug 与崩溃问题受到广泛关注。此外，社区对会话管理、插件系统扩展等功能需求讨论热烈。

---

## 社区热点 Issues

### 1. [Windows ARM64 native: OpenTUI fails to initialize with bun:ffi dlopen TinyCC error](https://github.com/anomalyco/opencode/issues/19130)
- **热度**：18 评论 / 12 👍 | **状态**：OPEN
- **详情**：Windows 11 ARM64 上原生二进制可执行非交互命令，但 TUI 初始化时报 `bun:ffi dlopen TinyCC` 错误。该问题横跨数月仍未解决，是 ARM64 用户的核心阻塞点。

### 2. [\[FEATURE\] Plan Mode + Question tool can auto switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)
- **热度**：11 评论 / 32 👍 | **状态**：OPEN
- **详情**：社区高票需求——在 Plan 模式下使用 Question 工具后建议自动切换回 Build 模式。该需求已存在半年以上，开发者期望其能进入规划。

### 3. [\[2.0\] BUG: enpoint error](https://github.comanomalyco/opencode/issues/43105)
- **热度**：15 评论 | **状态**：CLOSED
- **详情**：用户反馈 V2 版本无法使用 `https://opencode.ai/inference/v1` 作为 endpoint（报 410 Gone），而 V2 Beta 却可正常使用。该问题涉及服务端兼容性，今日已关闭，但引起较多用户关注与测试。

### 4. [ChatGPT OAuth rejects GPT-5.6 models for an EU-resident workspace， while official Codex CLI succeeds](https://github.com/anomalyco/opencode/issues/40243)
- **热度**：9 评论 / 4 👍 | **状态**：CLOSED
- **详情**：用户在 EU 数据驻留工作区中，OAuth 登录无法使用 GPT-5.6 模型，而官方 Codex CLI 却正常。该问题涉及 Provider 配置差异，已于今日修复。

### 5. [\[BUG\] MCP tools connected but not exposed to agent](https://github.com/anomalyco/opencode/issues/33027)
- **热度**：8 评论 / 3 👍 | **状态**：OPEN
- **详情**：MCP Server 连接成功且 `tools/list` 正常，但 Agent 工具列表中不可见。该问题持续两个月未解决，影响 MCP 生态的可用性。

### 6. [Big Pickle stops response early](https://github.com/anomalyco/opencode/issues/22861)
- **热度**：10 评论 / 3 👍 | **状态**：CLOSED
- **详情**：Big Pickle 模型在回复中途固定位置停止。该问题已在今日关闭，但涉及模型生成稳定性的潜在风险仍值得关注。

### 7. [\[FEATURE\] Add unarchive/restore for archived sessions](https://github.com/anomalyco/opencode/issues/24153)
- **热度**：8 评论 / 11 👍 | **状态**：OPEN
- **详情**：用户希望支持对已归档会话进行取消归档/恢复操作。当前归档功能是单向的，恢复只能通过手动操作。

### 8. [Opencode is unavailable - Upstream request failed: Endpoint is unavailable.](https://github.com/anomalyco/opencode/issues/43102)
- **热度**：4 评论 | **状态**：OPEN
- **详情**：新会话中运行两个不同模型均报 `Endpoint is unavailable` 错误，可能与今日上午的服务端网络波动或上游服务可用性有关。

### 9. [Grep tool fails on Windows: ripgrep extraction broken by MSIX PowerShell 7 PSModulePath](https://github.com/anomalyco/opencode/issues/40623)
- **热度**：3 评论 | **状态**：OPEN
- **详情**：Windows 上 `rg.exe` 解压逻辑受 MSIX PowerShell 7 环境变量影响而失败，且错误状态会缓存至重启。Windows 用户体验受损明显。

### 10. [\[BUG\] Windows path references and permissions on external directory path not working](https://github.com/anomalyco/opencode/issues/36681)
- **热度**：7 评论 | **状态**：OPEN
- **详情**：Windows 路径配置及外部目录权限访问不受控。该问题已提出一个多月，Windows 权限系统适配进展缓慢。

---

## 重要 PR 进展

### 1. [feat(plugin): expose MCP server transforms](https://github.com/anomalyco/opencode/pull/43125) ★ 新
- **状态**：OPEN | **作者**：rekram1-node
- **要点**：将 MCP server 定义与配置解耦，向插件暴露 `list`/`get`/`set`/`update`/`remove` 转换方法，便于 URL 级策略在插件中修改 MCP 配置。

### 2. [fix(core): support older previous-channel databases](https://github.com/anomalyco/opencode/pull/43142) ★ 新
- **状态**：OPEN | **作者**：kitlangton
- **要点**：修复旧版 `opencode-next.db` 导入时因缺少 `project`/`session` 列而失败的问题，提升跨版本数据库兼容性。

### 3. [fix(core): disable WAL on network filesystems](https://github.com/anomalyco/opencode/pull/43141) ★ 新
- **状态**：OPEN | **作者**：opencode-agent[bot]
- **要点**：自动检测 NFS/SMB/9P/FUSE 文件系统并关闭 SQLite WAL 模式，改用 rollback journal，同时提供 `OPENCODE_DB_WAL` 环境变量覆盖。

### 4. [fix(session): skip in-flight sessions in --continue selection](https://github.com/anomalyco/opencode/pull/43140) ★ 新
- **状态**：OPEN | **作者**：aiconvergence-collab
- **要点**：修复 `opencode run --continue` 将提示符注入正在被其他实例使用的会话的问题。通过跳过“进行中”的会话来避免误操作。

### 5. [fix(provider): select Azure DeepSeek adapter](https://github.com/anomalyco/opencode/pull/43135) ★ 新
- **状态**：OPEN | **作者**：IbrahimKhan12
- **要点**：修复 Azure DeepSeek 部署未使用专用 `deepseek()` 适配器的问题。直接关闭 Issue #43106。

### 6. [fix(ai): settle pending Anthropic tool calls](https://github.com/anomalyco/opencode/pull/43136) ★ 新
- **状态**：OPEN | **作者**：rekram1-node
- **要点**：修复 Anthropic 工具调用在 `message_stop` 到达时未收到 `content_block_stop` 而悬挂的问题；保留畸形输入为 `tool-input-error`。

### 7. [fix(console): preserve inference sessions](https://github.com/anomalyco/opencode/pull/43124)
- **状态**：OPEN | **作者**：adamdotdevin
- **要点**：在 legacy Zen 路由转发明智地保留 OpenCode session 头，但直接请求 Provider 时仍会剥离元数据。

### 8. [feat(ai): support Vertex request labels](https://github.com/anomalyco/opencode/pull/43129)
- **状态**：CLOSED | **作者**：rekram1-node
- **要点**：为 Vertex Gemini Provider 增加账单标签支持，不影响 Gemini API 路由。已完成合并。

### 9. [refactor(app): use shared server data](https://github.com/anomalyco/opencode/pull/43017)
- **状态**：CLOSED | **作者**：Brendonovich
- **要点**：将 App 消费者迁移至共享服务端数据层，删除重复的 session reducer 逻辑，集中权限控制。该重构涉及范围较广，值得关注其引入的回归。

### 10. [fix(core): serialize MCP token refresh](https://github.com/anomalyco/opencode/pull/43074)
- **状态**：CLOSED | **作者**：thdxr
- **要点**：修复多个 MCP 客户端并发刷新 OAuth token 导致的单点失败问题，已合并。对使用 OAuth 认证的 MCP 服务有明显稳定性提升。

---

## 功能需求趋势

- **会话管理增强**：社区对会话生命周期管理（如 #24153 的归档恢复功能）有较高呼声。
- **MCP 生态改进**：多起关于 MCP 工具不可见、配置不灵活的问题持续存在，推动插件 API 扩展相关工作。
- **跨平台稳定性**：Windows（特别是 ARM64）相关 Bug 占比高，涉及 TUI 初始化、路径权限、ripgrep 集成等，反映出 Windows 用户体验仍是薄弱环节。
- **模型推理控制**：用户期望能够更精确地控制推理强度（reasoning effort）与计划模式（Plan Mode → Build 自动切换），说明高级用户对模型行为调优有需求。
- **Web/Desktop 插件化**：V2 的 UI 插件系统在 web/桌面端尚不完善，社区已有提案希望将 TUI 插件 API 扩展到所有平台。

---

## 开发者关注点

- **Windows 路径与权限**：多个 Issue（#36681、#36696、#40623）反映 Windows 上路径引用、外部目录权限和内置工具（grep）存在问题，文档支持不足。
- **服务端错误与兼容性**：用户多次遇到 `410 Gone`（#43105、#43101）及 `Endpoint unavailable`（#43102）错误，说明 opencode.ai 网关配置与用户自定义 endpoint 之间仍存在兼容性盲区。
- **`--continue` 误注入**：并发使用同一 session 时易发生互相干扰，开发者期望增加会话活跃状态感知。
- **性能与资源占用**：如 #42880 提到的在 `/tmp` 下频繁生成 `.so` 文件导致 SSD 损耗，以及大文本粘贴时桌面端卡顿（#13995），仍然是资源受限环境下的痛点。
- **多 Provider 适配**：Azure DeepSeek 模型选择、Vertex 标签支持等细分模型能力在持续补齐，说明开发者正在积极拓展非 OpenAI 供应商的深度集成。

---

> 日报由 AI 技术分析师自动生成，基于 GitHub 公开数据。链接可直接点击跳转至对应 Issue/PR 页面。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报

**日期：2026-08-18** | 数据来源：[github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)

---

## 今日速览

今日 Pi 社区活动密集，核心焦点集中在 **上下文管理（auto-compaction）缺陷修复** 与 **模型目录/供应商兼容性更新** 两大方向。多起 PR 密集修复了 Anthropic 拒绝响应回退、Qwen/GLM 模型目录对齐等关键问题，同时 #7995 揭示的 OpenRouter 响应缓存缺失导致 2.5 倍成本惩罚的问题，已成为影响用户钱包的高优事项。此外，多起 UI 渲染性能问题（长文本编辑器卡顿、大 diff 崩溃）也获得了社区高度关注。

---

## 社区热点 Issues（Top 10）

### 1. [#6879 auto-compaction 在上下文超过 100% 后从未触发，直到 provider 溢出](https://github.com/earendil-works/pi/issues/6879)
- **作者**: alexanderkreidich | **评论**: 18 | **👍**: 17
- **重要性**: 会话运行超2小时后，footer 越过压缩阈值并持续增长至 373k tokens，直到 API 拒绝请求才触发压缩。用户明确建议 **在每个 agentic 步骤后检查上下文占用**。这是核心稳定性问题，社区共鸣强烈。
- **状态**: OPEN

### 2. [#534 Linux 上配置文件位置不合规（未遵循 XDG 规范）](https://github.com/earendil-works/pi/issues/534)
- **作者**: Ramblurr | **评论**: 15 | **👍**: 39
- **重要性**: 高赞老 issue（1月创建至今持续更新），指出配置目录直接位于 `$HOME` 而非遵循 XDG Base Directory Spec。对 Linux 用户影响面大。
- **状态**: CLOSED

### 3. [#8029 提示编辑器在移动光标时性能极慢](https://github.com/earendil-works/pi/issues/8029)
- **作者**: affanali2k3 | **评论**: 9 | **👍**: 0
- **重要性**: 大缓冲区（约7000行）时按一次方向键耗时 **1650ms**，性能呈线性恶化。直接影响长会话编辑体验。
- **状态**: OPEN

### 4. [#7995 openai-responses 缺失 'anthropic' 缓存控制格式支持 — Claude 经 OpenRouter responses 实测 2.5 倍成本惩罚](https://github.com/earendil-works/pi/issues/7995)
- **作者**: LukasParke | **评论**: 4 | **👍**: 0
- **重要性**: 基于 OpenRouter 870 次试验基准测试。`openai-responses` 实现缺少 Anthropic 风格提示缓存支持（`cache_control` 缺失），导致 Claude 模型成本显著上升。直接影响用户支出。
- **状态**: OPEN

### 5. [#8036 Edit 工具在执行大 diff 渲染及会话恢复时崩溃 TUI](https://github.com/earendil-works/pi/issues/8036)
- **作者**: AntiKnot | **评论**: 4 | **👍**: 0
- **重要性**: 内置 `edit` 工具生成约 **14.5 MB** 的 diff 导致 TUI 交互界面崩溃。长行 HTML 文件场景下复现，影响代码编辑核心功能。
- **状态**: OPEN

### 6. [#8028 TUI `fullRender` 在渲染输出超过 V8 字符串限制时崩溃（RangeError）](https://github.com/earendil-works/pi/issues/8028)
- **作者**: runthesim | **评论**: 2 | **👍**: 0
- **重要性**: 视频制作 agent 因读取大量图像导致渲染输出超限崩溃。与 #8036 同属 TUI 渲染鲁棒性问题。
- **状态**: OPEN

### 7. [#3200 支持 prompt 命令中的视频/音频内容](https://github.com/earendil-works/pi/issues/3200)
- **作者**: louis030195 | **评论**: 8 | **👍**: 5
- **重要性**: 扩展 `prompt` RPC 命令，将视频/音频内容转发至多模态 LLM（Gemma 4、GPT-4o）。反映社区对多模态输入支持的需求。
- **状态**: OPEN

### 8. [#8166 自定义消息在工具批次中途注入破坏 tool_calls→tool 相邻性（DeepSeek 400）](https://github.com/earendil-works/pi/issues/8166)
- **作者**: CarloCattano | **评论**: 3 | **👍**: 0
- **重要性**: 扩展调用 `pi.sendMessage(..., { triggerTurn: false })` 后，后续回合持续报错 `Messages with role 'tool' must be a response to a preceding message with 'tool_calls'`。属于扩展 API 契约边界问题。
- **状态**: OPEN

### 9. [#7756 detectInstallMethod 误判非 pnpm 安装（PNPM_HOME 共享场景）](https://github.com/earendil-works/pi/issues/7756)
- **作者**: songlairui | **评论**: 3 | **👍**: 0
- **重要性**: 路径包含 `/pnpm/` 即被标记为 pnpm 安装，导致 `isManagedByGlobalPackageManager` 误判。影响部分环境下的升级/管理逻辑。
- **状态**: OPEN

### 10. [#7994 openai-completions：reasoning_details 往返仅支持加密条目 — 签名文本重放不可行](https://github.com/earendil-works/pi/issues/7994)
- **作者**: LukasParke | **评论**: 3 | **👍**: 0
- **重要性**: `openai-completions` 实现仅解析 `reasoning.encrypted` 条目，签名文本（`signed reasoning.text/summary`）在重放时无法正确往返，导致推理摘要丢失。与 #7995 同属 OpenRouter 基准发现的系列问题。
- **状态**: OPEN

---

## 重要 PR 进展（Top 10）

### 1. [#8258 修复 Anthropic 拒绝响应错误与回退](https://github.com/earendil-works/pi/pull/8258)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #8017。在 `claude-fable-5` 上复现压缩失败（Anthropic 返回 `stop_reason: "refusal"`）。新增 `allowed_fallback_models` 元数据并实现服务端回退。

### 2. [#8255 加载嵌套 Markdown 技能](https://github.com/earendil-works/pi/pull/8255)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #6479。`~/.agents/skills/third-party/child-skill.md` 等嵌套独立技能文件此前被静默跳过，现已纳入发现逻辑。

### 3. [#8246 OpenAI Completions 推理详情支持](https://github.com/earendil-works/pi/pull/8246)
- **作者**: cristinaponcela | **状态**: OPEN
- **内容**: 解决 #7994。通过 Synthetic OpenRouter 流复现签名 `reasoning.text/summary` 丢弃问题，修复 assistant 消息级 `reasoning_details` 往返。

### 4. [#8240 对齐 Qwen Token Plan 模型目录](https://github.com/earendil-works/pi/pull/8240)
- **作者**: sunner | **状态**: 已合并
- **内容**: 解决 #8194。`qwen-token-plan` 与 `qwen-token-plan-cn` 统一暴露 8 个模型（含 `deepseek-v4-pro-0813`、`deepseek-v4-flash-0731`）。

### 5. [#8254 防止 Copilot 策略登录速率限制](https://github.com/earendil-works/pi/pull/8254)
- **作者**: rwachtler | **状态**: OPEN
- **内容**: 解决 #7850。在策略更新前获取账户模型目录，仅更新已知、支持工具且未配置的模型，并在受限时有限重试登录请求。

### 6. [#8253 修复长会话中内容变化时的全屏闪烁](https://github.com/earendil-works/pi/pull/8253)
- **作者**: wlynxg | **状态**: 已合并
- **内容**: 视口上方内容变化（如工具结果更新）导致清屏重绘。现仅清除受影响屏幕区域，避免 10k+ 行会话中的可见闪烁。

### 7. [#8250 使子代理进度与失败状态可靠](https://github.com/earendil-works/pi/pull/8250)
- **作者**: terrorobe | **状态**: OPEN
- **内容**: 修复子代理示例：子代理仍在工作时即报告完成、进程失败信息丢失、失败时返回正常工具结果等问题，并增加专门的失败信号。

### 8. [#8262 在每个 turn 启动路径上调度 hooks（可取消的 turn 预检）](https://github.com/earendil-works/pi/pull/8262)
- **作者**: LogosZR | **状态**: OPEN
- **内容**: 修复 `sendCustomMessage(triggerTurn: true)` 绕过 `input` hook 与 `before_agent_start` 的问题。

### 9. [#8120 实验性追加压缩（Append Compaction）](https://github.com/earendil-works/pi/pull/8120)
- **作者**: vegarsti | **状态**: OPEN
- **内容**: `PI_EXPERIMENTAL=1` 时启用追加压缩。复用活跃系统提示、工具和路由会话，以利 provider 提示缓存。独立模式仍为默认。

### 10. [#8241 为扩展发出压缩失败事件](https://github.com/earendil-works/pi/pull/8241)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #8175。新增扩展可见的 `session_compact_failed` 事件，携带失败载荷，此前扩展仅能监听 `session_before_compact` 而不知失败原因。

---

## 功能需求趋势

1. **上下文管理智能化**（#6879、#8229、#8120）：自动压缩触发逻辑需更激进，扩展到本地模型场景；探索追加压缩以复用提示缓存。
2. **多模态输入支持**（#3200、#8220）：prompt 命令扩展至视频/音频；引入 GLM-4.6V 视觉模型支持编码 agent 工作流。
3. **TUI 渲染性能与鲁棒性**（#8029、#8036、#8028、#8253）：大缓冲区编辑、大 diff 渲染、V8 字符串限制等问题密集出现。
4. **系统集成合规与体验**（#534、#7756、#8252、#8278）：XDG 目录规范、安装方式检测、终端兼容性（tmux 窄列、Konsole Shift+Enter）持续受关注。
5. **模型目录与供应商适配**（#8187、#8190、#8194、#8220、#8240）：各供应商模型列表需及时同步，GLM/Qwen/小米等均有涉及。

---

## 开发者关注点

- **成本控制**：#7995 揭示的缓存缺失导致 2.5x 成本惩罚是当前最“昂贵”的问题，OpenRouter 用户受影响显著。
- **压缩可靠性**：Auto-compaction 在超长会话中触发不及时（#6879），以及 Anthropic 拒绝响应导致压缩失败（#8017/#8258），直接威胁核心工作流。
- **扩展 API 契约**：#8166 的 tool-call 相邻性破坏与 #8262 的 hook 调度缺失，反映出扩展开发边界需要更严谨的定义与测试。
- **渲染性能**：大上下文下的 TUI 延迟与崩溃问题高频出现（#8029、#8036、#8028），已成为长会话用户的核心痛点。
- **模型目录及时性**：多个 issue 围绕供应商模型下线/上线（#8187、#8190、#8220），社区期望内置目录能快速跟随上游变化。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-18

## 1. 今日速览

昨日发布补丁版本 **v0.21.13**，主要修复 Web Shell 相关问题；与此同时，社区围绕 **上下文压缩**（`/compress`）、**Windows 平台 Ctrl+V 粘贴回归**、**`qwen serve` 守护进程资源治理** 的讨论热度持续走高。值得关注的是，本周自动化运维（Autofix/Review 机器人）在 CI 效率和调度策略上迎来一波显著的集中重构——多个 PR 专门优化断点续跑、避免重复任务浪费 runner 资源。

---

## 2. 版本发布

### v0.21.13（2026-08-17 发布）
- **Web Shell Composer 增强**：支持拖拽 / 粘贴文本文件作为命名附件（图片附件之外的新能力）。（[#9180](https://github.com/QwenLM/qwen-code/pull/9180)）
- 可从任意 **Assistant 回复** 处 **fork 对话**（使用 `du` 命令）。
- 附带 4 轮 DSW EAS 端到端 Benchmark smoke（SWE-bench Verified + Terminal-Bench 2.0），最终完整回归通过（500 + 89 用例）。

---

## 3. 社区热点 Issues（Top 10）

| # | Issue | 关注点 | 为什么重要 |
|---|-------|--------|------------|
| 1 | [#9061](https://github.com/QwenLM/qwen-code/issues/9061) `[Bug]` | Windows 平台 Ctrl+V 粘贴完全失效（0.21.x 回归） | P1 严重级别；0.21.0 正常、之后版本回归，影响所有 Windows CLI 用户 |
| 2 | [#9320](https://github.com/QwenLM/qwen-code/issues/9320) `[Bug]` | `/compress-fast` 与 `/rewind` 后上下文丢失 | 用户实测：压缩至 87k 后启动新 llama-server 恢复会话时上下文遗失，直接破坏核心工作流 |
| 3 | [#9324](https://github.com/QwenLM/qwen-code/issues/9324) `[Bug]` | 消息被多次投递且无用户重定向 | 使用 Qwen 3.8 Max 时，模型频繁“收到”同一条消息多次，打断当前任务，疑似会话路由问题 |
| 4 | [#7433](https://github.com/QwenLM/qwen-code/issues/7433) `[Bug]` | 本地模型会话被 SDK 误报为 `qwen-oauth` | ACP 会话开启时 `currentModel` 指向非本地模型，影响依赖 SDK 的集成方 |
| 5 | [#9309](https://github.com/QwenLM/qwen-code/issues/9309) `[Bug]` | 连续压缩后 token 数异常（170k→7x k 后仍显示膨胀） | 多次 `/compress` 后上下文统计异常，可疑的压缩算法边界问题 |
| 6 | [#8051](https://github.com/QwenLM/qwen-code/issues/8051) `[Feature]` | `qwen serve` 多工作区守护进程资源治理 | 仅计数限制无法约束请求体/WebSocket 的字节占用，社区持续追踪中（companion issue #8091） |
| 7 | [#6806](https://github.com/QwenLM/qwen-code/issues/6806) `[Bug]` | `/compress` 后状态栏上下文占比不刷新 | 虽为 UI 层面问题，但直接影响用户对压缩效果的判断，且标注 `welcome-pr` |
| 8 | [#8835](https://github.com/QwenLM/qwen-code/issues/8835) `[Bug]` | 代码仓库卫生周报（8 项安全问题） | 包含 ACP 路径穿越（`..` prefix）类安全缺陷，建议安全敏感用户关注 |
| 9 | [#9296](https://github.com/QwenLM/qwen-code/issues/9296) `[Bug]` | Autofix 机器人在已关闭/合并 PR 上仍触发扫描任务 | P1 效率问题：~500 次运行中 59% 被取消，浪费大量 runner 资源 |
| 10 | [#9300](https://github.com/QwenLM/qwen-code/issues/9300) `[Bug]` | VP 模式内容未底部对齐，消息区与输入框之间留白 | Web Shell 渲染细节问题，影响默认终端模式下的视觉体验 |

---

## 4. 重要 PR 进展（Top 10）

| # | PR | 内容 | 关键价值 |
|---|-----|------|---------|
| 1 | [#9367](https://github.com/QwenLM/qwen-code/pull/9367) | WebUI 全局展开/折叠控制器 | `/export` HTML 查看器支持一键展开/折叠所有可折叠区块，提升长对话导出的浏览效率 |
| 2 | [#9226](https://github.com/QwenLM/qwen-code/pull/9226) | `/review` 增加 Aone Code 读取路径 | 第二个 review 平台 provider；自动识别 `gitlab.alibaba-inc.com` 远端，国内开发者可直接复用评审管线 |
| 3 | [#9370](https://github.com/QwenLM/qwen-code/pull/9370) | macOS/Windows CI 触发条件修复 | 恢复平台敏感 diff 自动触发 + nightly 兜底，避免长期无声失败 |
| 4 | [#9303](https://github.com/QwenLM/qwen-code/pull/9303) | 限制 Web Shell 守护进程会话历史保留量 | 修复渲染器 OOM 崩溃：原始 replay 快照注入后即释放，重建受块上限约束 |
| 5 | [#9364](https://github.com/QwenLM/qwen-code/pull/9364) | `qwen serve` 新增 `QWEN_SERVE_NEW_FILE_MODE` | 解决新建文件硬编码 `0600` 问题，支持 `owner` / `system`（umask 派生）双策略 |
| 6 | [#9130](https://github.com/QwenLM/qwen-code/pull/9130) | Sandbox 验证新增确定性 flakiness gate | 对 PR 修改的测试文件默认重复跑 5 次，自动发现并拦截“偶发绿”的不稳定测试 |
| 7 | [#9214](https://github.com/QwenLM/qwen-code/pull/9214) | Autofix 验证门迁移至临时容器 | 将验证 gate 移入 ephemeral container，隔离宿主环境，并增加结构测试固定信任边界 |
| 8 | [#8992](https://github.com/QwenLM/qwen-code/pull/8992) | MCP 2026 核心 + WebShell Apps host | MCP 客户端首个切片：支持 `ui://` 工具元数据保留、HTML 资源声明式加载与校验（已持续跟进 5 日） |
| 9 | [#9131](https://github.com/QwenLM/qwen-code/pull/9131) | Web Shell 技能切换后增量刷新 | 新增去重 workspace 信号，使 composer 技能列表按需增量刷新，避免全量重载 |
| 10 | [#9340](https://github.com/QwenLM/qwen-code/pull/9340) | Review 评论增加“方案存疑”提示 | 当 PR 轮次多且 diff 增长显著时，review 会额外提示“问题在方案而非当前补丁”，辅助维护者决策 |

---

## 5. 功能需求趋势

从近 24 小时活跃的 Issues 中可提炼出以下社区核心诉求：

1. **导出与跨端一致性**（`roadmap/export-data`）：[#9354](https://github.com/QwenLM/qwen-code/issues/9354)（跨主机聊天记录契约预校验）、[#9367](https://github.com/QwenLM/qwen-code/pull/9367)（导出 HTML 展开控制）——社区正在推动 Web Shell / Desktop / VS Code 的聊天记录格式统一与可移植性。
2. **微信渠道增强**：当日出现 3 条相关 Issue（[#9307](https://github.com/QwenLM/qwen-code/issues/9307) 64 位消息 ID 截断、[#9352](https://github.com/QwenLM/qwen-code/issues/9352) 文件发送支持、[#9353](https://github.com/QwenLM/qwen-code/issues/9353) typing 状态过期），说明多通道集成正在快速扩展。
3. **上下文压缩可靠性**：连续 3 条 Issue（[#9309](https://github.com/QwenLM/qwen-code/issues/9309) 压缩计数异常、[#9320](https://github.com/QwenLM/qwen-code/issues/9320) 压缩后上下文丢失、[#6806](https://github.com/QwenLM/qwen-code/issues/6806) UI 不刷新）指向一个结论：**压缩功能虽强，但边界场景验证不足**，是当前最伤用户信任的痛点。
4. **守护进程资源治理**（`daemon`）：两条追踪 Issue（[#8051](https://github.com/QwenLM/qwen-code/issues/8051) / [#8091](https://github.com/QwenLM/qwen-code/issues/8091)）持续强调字节级限制而非仅仅计数——`qwen serve` 正被用于更重的生产场景。
5. **模型列表动态化**：[#9368](https://github.com/QwenLM/qwen-code/issues/9368) 要求 ModelStudio Token Plan / Coding Plan 预设从固定列表改为动态拉取——集成方对 provider 可扩展性的需求上升。

---

## 6. 开发者关注点

**高频痛点：**

- **Windows 平台 CLI 回归**：Ctrl+V 粘贴失效（#9061）是当周最高优先级 Bug 之一，社区已确认 0.21.0 正常、后续版本回归，希望尽快修复。
- **上下文压缩副作用**：用户对压缩后 token 计数不准确、上下文丢失、状态栏不刷新提出连续投诉，压缩链路亟需系统性的边界验证（建议参考 PR #9130 的 flakiness gate 思路）。
- **守护进程资源使用的“黑盒”感**：`qwen serve` 多工作区场景下字节占用不可控，开发者希望看到按请求体/WebSocket/会话粒度的可观测性指标。

**自动化运维效率：**

- 机器人（Autofix）在已关闭 PR 上误触发、重复地址分发浪费 runner 容量（#9296），以及多轮 review 中累积的 deferred backlog（#9342、#9327 均为 15 轮以上的 review 收尾清理），反映出自愈工作流初具规模后进入“治理期”。

**值得肯定的方向：**

- MCP 2026 支持（#8992）与 WebShell Apps host 的进展获得持续关注——这是生态开放性的重要一步。
- 跨平台 CI 恢复（#9370）补齐了 macOS / Windows 的回归保障；Aone Code 支持（#9226）降低了国内开发者的接入成本。

> 数据截至 2026-08-18 09:00 UTC；统计来源：github.com/QwenLM/qwen-code Issues / PRs / Releases

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-18

> 数据来源：github.com/Hmbown/DeepSeek-TUI（现项目代号 CodeWhale）


## 今日速览

项目已正式进入 **v0.9.9 发布周期**，昨日完成 0.9.9 正式 Release 并连续推送多个 CHANGELOG 增补。社区活动高度活跃：**41 条 Issue / PR 在过去 24 小时内有更新**，其中 v0.9.9 发布（#5476）、文档汉化史诗级任务（#5482）、DeepSeek V4 峰谷分时计价（#5470）为今日焦点。持续可靠性问题（CI 双平台红、flaky 测试、并行加载）仍是开发者反馈最密集的领域。


## 社区热点 Issues（10 个）

**1. [#5482 [OPEN] EPIC(docs): 全量文档中文本地化](https://github.com/Hmbown/CodeWhale/issues/5482)** ⭐ 新
> 社区成员 SparkofSpike 发起，指出 `docs/` 下大量英文文档对中国用户构成真实门槛，机器翻译引入错误且部分源文档已过时。评论建议按优先级分层推进。这是项目首个文档本地化史诗任务，标志社区结构变化。

**2. [#5424 [CLOSED] v0.9.7: Codewhale TUI 自行崩溃](https://github.com/Hmbown/CodeWhale/issues/5424)**
> 用户 `codewhale --continue` 加载工作区后，提示任意消息约一分钟即无预警退出。7 条评论。已关闭，但暴露了 v0.9.7 会话稳定性问题——v0.9.9 中 shell 工具的磁盘/描述符耗尽修复（#5465）正是同类根因。

**3. [#2369 [OPEN] CodeWhale 配置路径跨 OS 与 Cygwin 碎片化及静默迁移缺陷](https://github.com/Hmbown/CodeWhale/issues/2369)** 🔥 8 评论
> Windows/Cygwin 下配置文件因 home 目录规则不同导致解析路径分叉，遗留迁移还可能静默产生错误配置。跨平台配置一致性是长期痛点，自五月起持续被关注。

**4. [#5056 [OPEN] 测试可靠性：flaky verifier 后台测试 / /workspace 敏感 fixture / 12 个未分类 #[ignore] 测试](https://github.com/Hmbown/CodeWhale/issues/5056)** 🔥 8 评论
> 维护者自报：全量并行测试下 `verifier` 后台测试仍间歇失败，`/workspace` 敏感子代理测试依赖具体路径，另有 12 个遗留 ignore 测试未被分类或修复。工程质量核心问题。

**5. [#1425 [OPEN] 大文本处理工程后会话中断卡死](https://github.com/Hmbown/CodeWhale/issues/1425)** 🔥 7 评论
> 中文用户尝试分析 300 万字小说，AI 切片为 10 个子 agent 并行处理，但 `agent_wait` 等待子 agent 超时导致会话卡死。作者详细记录了 10 个子 agent 全部 Running 后卡死的复现路径。是子代理编排超时机制在高负载下的真实压力测试。

**6. [#5123 [OPEN] Agent 生成面旋钮过多 — 标记为 builder 的会话以只读运行并自锁 BLOCKED](https://github.com/Hmbown/CodeWhale/issues/5123)** 🔥 7 评论
> Dogfood 发现：委派的 builder 会话被标记为 `builder` / `gates-shell-writer`，但实际工具契约为**只读**，导致无法执行分配的任务门禁而自锁。暴露了角色标签与实际工具权限之间的契约断层。

**7. [#5324 [CLOSED] 简化 32 字段 agent 工具 schema 以减少模型报错](https://github.com/Hmbown/CodeWhale/issues/5324)** 🔥 8 评论
> 模型侧 `agent` 工具携带 **32 属性、0 required 字段**的 JSON Schema，同时服务 8 个 action。已关闭（修复完成，见 PR #5325 等），但社区对 schema 过度设计的讨论值得关注——模型面对过宽 schema 时错误率显著上升。

**8. [#1651 [OPEN] YOLO Agent 运行测试脚本时 VS Code 崩溃](https://github.com/Hmbown/CodeWhale/issues/1651)** 6 评论
> YOLO Agent 在 IDE 集成终端中后台自动执行测试脚本时，VS Code 崩溃或意外退出。用户使用 DeepSeek v4-pro/v4-flash 复现。IDE 集成与自主代理的组合稳定性问题。

**9. [#5437 [OPEN] TUI：正式化状态栏颜色语法并展示 repo/worktree 状态](https://github.com/Hmbown/CodeWhale/issues/5437)** 3 评论
> 外部设计评审结论：颜色并非"太多"，而是一套**色彩词汇表**，评审建议保留现有调色板（操作紫、Full Access 等）。在此基础上建议正式成文并补充 git repo/worktree 状态显示。来自第三方设计评审的确认与增强需求。

**10. [#5403 [OPEN] main 分支在双平台全部 4 次运行均为红色](https://github.com/Hmbown/CodeWhale/issues/5403)**
> #5395 修复后 main 构建不再互相取消，但已完成 4 次运行（macOS + Windows 各 2 次）全部失败：macOS 挂在 `plugin_e2e_acceptance`，Windows 挂在 NSIS 打包。CI 全红是发布周期中最紧迫的工程债务。


## 重要 PR 进展（10 个）

**1. [#5476 [CLOSED] release: 0.9.9](https://github.com/Hmbown/CodeWhale/pull/5476)** 🏷️ 正式版
> **v0.9.9 主题：truth-and-resilience（真实与韧性）**。核心修复：shell 工具在宿主机磁盘/描述符耗尽时不再卡死会话（#5465——该 bug 曾中断维护者自己的 0.9.9 会话）；未验证的上下文窗口/输出上限/遥测默认值被诚实标注；另有大量可靠性修复。后续 #5477、#5487 持续增补 CHANGELOG 与贡献者署名。

**2. [#5470 [CLOSED] DeepSeek V4 分时峰谷计价按轮次解析](https://github.com/Hmbown/CodeWhale/pull/5470)**
> 第一方 DeepSeek V4 定价按 UTC 小时分为峰值/非峰值两档，但 `pricing.rs` 仍使用单一固定费率。此 PR 将硬编码单价替换为**按每轮次时间解析的峰谷费率**（V4-Pro: 0.003625→峰/谷两档；V4-Flash: 0.0028→两档）。对成本敏感用户是重要修复。

**3. [#5482 关联 PR 系列 — [#5490 / #5488：Web 文档与共享组件迁移至字典主干](https://github.com/Hmbown/CodeWhale/pull/5490)** 🆕
> 配合 #5337 字典化改造：`[locale]/docs/layout.tsx` 的 5 个字符串和 3 个共享组件中的 `{en, zh}` 三元选择全部迁移到 `pickText()` 字典路径。**8 个部分支持语言（ja/vi/ko/ru/uk/es/pt-BR/id）此前在这些位置只能读英文**，本次修复后可在字典中补充翻译。

**4. [#5491 [OPEN] 持久化审批结论至执行之前](https://github.com/Hmbown/CodeWhale/pull/5491)** 🆕 社区贡献
> 社区开发者 cyq1017 提交：在审批执行前将会话级审批请求与终态写入日志；若终态审批回执无法持久化则**拒绝执行**并拒绝过期决策；会话恢复时重建已关闭/已中断的审批状态。关闭 #5360。这是 fail-closed 审批机制的完整实现。

**5. [#5484 [CLOSED] DSH 环境氛围海洋场景 — 鲸鱼与字形鱼群](https://github.com/Hmbown/CodeWhale/pull/5484)**
> 为 DeepSeek Harness（DSH）捆绑包添加**环境海洋场景**：深度渐变背景 + 两条贝塞尔曲线游动的鲸鱼剪影（含慢速尾鳍摆动与偶尔深潜）+ Codewhale 字形鱼群（`><(((‘>`）。Codewhale 品牌视觉语言向 DSH 的延伸。

**6. [#5485 [CLOSED] 第一方模型行与定价更新至 2026-08-17](https://github.com/Hmbown/CodeWhale/pull/5485)**
> 模型目录全面校对：所有值均于 2026-08-17 通过 curl 官方页面重新验证（xAI 层级值来自 docs.x.ai 嵌入式价格表，其 `LongContext` 列恰为标准列 2 倍）。保证模型目录中第一方模型与实际官方定价一致。

**7. [#5475 [CLOSED] 安全解析自有直接模型大小写](https://github.com/Hmbown/CodeWhale/pull/5475)** 🙌 社区贡献
> 社区开发者 h3c-hexin：将小写保存的选择器（如 `glm-5.2`）在归为"外部模型"之前，先与所属 Z.ai 目录行进行解析匹配；精确匹配保持权威性，仅当恰好一个厂商拥有该裸 wire id 时才启用 DeepSeek/Z.ai 大小写回退。修复模型分类误判。

**8. [#5474 [CLOSED] 压缩所有嘈杂 web 工具结果](https://github.com/Hmbown/CodeWhale/pull/5474)** 🙌 社区贡献
> 将既有"嘈杂结果软限制"应用到所有 web 工具面：`Web`、`web_search`、`web.run`、`fetch_url`；非嘈杂工具（如 `read_file`）保留普通硬限制；覆盖别名路由与有界证据豁免。降低长会话上下文被 web 抓取内容撑爆的概率。

**9. [#5486 [CLOSED] 紧凑行隐藏会话指标条](https://github.com/Hmbown/CodeWhale/pull/5486)**
> 低于 60 列时，阶段条会关闭工作详情、缓存芯片和状态 toast，但仍绘制会话指标条。59 列下渲染：`▌· idle │ LLM 3.5s │ Cache hit 99% │ Input 9.3M     F1:keys`。此 PR 让紧凑行彻底干净。

**10. [#5480 [CLOSED] 展示并打开实时 /rc 会话链接 + 发送稳定设备 ID](https://github.com/Hmbown/CodeWhale/pull/5480)**
> `/rc` 横幅从未告知用户会话地址。此 PR 让 TUI 展示、打印并打开实时 web 会话链接（解析 `runner.runUrl` / `runner.computerUrl`），并停止每次 `/rc` 都生成新"计算机"标识。


## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|---|---|---|
| **多语言与本地化** | #5482 全量文档汉化；#5488/#5490 字典化 Web；#5290 非英文路由控件不可点击 | 🔥🔥🔥 上升最快 |
| **第三方模型配置易用性** | #5350 预制模板简化配置；#5475 模型大小写解析 | 🔥🔥 持续 |
| **审批与安全机制** | #5360 审批持久化 fail-closed；#5491 对应 PR | 🔥🔥 上升 |
| **上下文管理与成本透明** | #5239 1M 上下文与 128K 压缩矛盾；#5241 定价端 503；#5470 分时计价；#5474 web 结果压缩 | 🔥🔥 高频 |
| **产品可发现性** | #5439 编排三件套不可见；#5442 高级命令埋藏；#5437 状态栏颜色语法 | 🔥 新趋势 |
| **国产/本地化部署** | #1829 SSH 出站阻断；#5410 bwrap 沙箱扩展 | 温和持续 |
| **IDE 集成稳定性** | #1651 VS Code 崩溃；#1829 SSH 沙箱问题 | 持续 |

**本周期最显著趋势**：① 中文本地化从零散翻译上升为**史诗级结构化任务**（#5482 + 字典化改造双线推进）；② 项目代号从 "DeepSeek-TUI" 向 "CodeWhale" 的品牌迁移进入**标识退役阶段**（#5443 三级迁移计划）；③ 第三方模型生态（Z.ai/GLM/OpenCode 等）接入需求持续攀升。


## 开发者关注点

**🔴 痛点 Top 3**

1. **CI 全红与测试可靠性**（#5403、#5056、#5355）：main 双平台 4 次全红、flaky 测试反复出现、并行加载卡顿——社区对发布门禁质量表示担忧，维护者在 #5355 中已建立 v0.9.8 已知问题调查篮。
2. **会话崩溃与卡死**（#5424、#1425、#5123）：v0.9.7 无预警退出、子 agent 超时卡死、角色标签与工具权限契约断层——"代理编排的失败模式"是本周期最密集的反馈类型。
3. **配置碎片化与静默错误**（#2369、#5098、#5241）：跨平台路径分叉、fleet 配置被静默遮蔽、定价端 503 导致成本显示永久 `unverified`——配置系统的可诊断性不足。

**✅ 值得肯定**

- v0.9.9 以"truth-and-resilience"为主题：shell 工具磁盘/描述符耗尽修复、诚实标注未验证项、持久化审批——维护者对可靠性问题的响应速度获得社区认可。
- DSH 捆绑的 Codewhale 皮肤（#5484/#5469）与语音版网站文案（#5483）展示了产品化投入。
- 社区贡献活跃：h3c-hexin 连续提交多个修复（#5473/#5474/#5475），cyq1017 提交审批持久化实现（#5491），外部设计评审为状态栏配色提供专业确认（#5437）。

---
*日报生成时间：2026-08-18 | 数据窗口：过去 24 小时 | 共 41 条 Issue + 41 条 PR 更新*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*