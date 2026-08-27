# AI CLI 工具社区动态日报 2026-08-27

> 生成时间: 2026-08-27 05:22 UTC | 覆盖工具: 9 个

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

**分析日期**：2026-08-27  
**数据来源**：各工具 GitHub 公开社区动态  
**覆盖范围**：Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI (CodeWhale)

---

## 1. 生态全景

当前 AI CLI 工具已从"单点实验"步入**生产环境大规模采用与稳定性博弈**阶段。各主流工具均面临相似的核心挑战：**Agent 循环失控、后台进程资源泄漏、上下文压缩失效、MCP 生态兼容性碎片化、以及 Windows/WSL 环境系统性退化**。与此同时，多智能体协作（Agent Team/Subagent）、会话生命周期管理、权限安全模型收紧成为各厂商竞争的焦点。市场分化明显：背靠大厂者（Claude Code、Codex、Gemini CLI）以稳定性和生态深度取胜，而开源社区项目（OpenCode、Pi、CodeWhale）则在迭代速度和功能创新上保持活力。

---

## 2. 各工具活跃度对比

| 工具 | Issues（高热度/总数） | PR 进展 | Release 情况 | 社区活跃度评级 |
|------|----------------------|---------|--------------|----------------|
| **Claude Code** | 10 个高热度（63 👍 峰值） | 2 条（1 条有效） | v2.1.247（新工具 SendFeedback） | ★★★★★ 极高 |
| **OpenAI Codex** | 10 个高热度（145 👍 峰值） | 10 条（多方向活跃） | v0.150.1 稳定版 + alpha | ★★★★★ 极高 |
| **Gemini CLI** | 10 个高热度（P1 居多） | 10 条（安全修复为主） | v0.59.0-nightly | ★★★★☆ 高 |
| **GitHub Copilot CLI** | 10 个高热度（31 👍 峰值） | 0 条（24h 空窗） | 3 个 prerelease | ★★★★☆ 高 |
| **Kimi Code CLI** | 2 个 | 1 条 | 无 | ★☆☆☆☆ 低 |
| **OpenCode** | 10 个（105 👍 峰值） | 10 条 | 无 | ★★★★☆ 高 |
| **Pi** | 12 个 | 12 条（含多个合入） | 无 | ★★★★☆ 高 |
| **Qwen Code** | 10 个（含 2 条 P1 安全） | 10 条 | v0.22.2 + desktop-v0.2.2 | ★★★★☆ 高 |
| **DeepSeek TUI (CodeWhale)** | 10 个 | 10 条（5 条已合并） | 无（v0.9.12 修复中） | ★★★☆☆ 中 |

---

## 3. 共同关注的功能方向

### 3.1 Agent 循环检测与终止机制
- **涉及工具**：OpenCode（#45442 等 5 个独立 Issue）、Gemini CLI（#22323）
- **具体诉求**：Agent 在无进展时重复相同工具调用（364 次相同 grep），缺乏循环保护；子代理达到轮次上限后误报成功。社区要求内置 "N 次相同调用无新信息即停止" 的保护机制。

### 3.2 上下文管理与 Token 成本控制
- **涉及工具**：GitHub Copilot CLI（#4613 MCP schema 提前注入致 354K tokens 暴涨）、Claude Code（#84253 缓存 TTL 失效）、Gemini CLI（#18836 持久化任务追踪替代 WriteToDo）
- **具体诉求**：Prompt 缓存失效导致全量重写、MCP 工具 schema 未延迟加载、Agent 对上下文压力不敏感。成本敏感度已成为生产环境采纳的关键障碍。

### 3.3 多智能体（Agent Team / Subagent）可靠性
- **涉及工具**：Qwen Code（#10074 系列 5 个竞态 Issue）、Gemini CLI（#21409 子代理挂起）、OpenCode（#42657 并发 subagent TUI 卡顿）、Claude Code（#85095 Plan 模式静默退出）
- **具体诉求**：并发任务的生命周期管理、结果持久化、事件桥接一致性、子代理可观测性（bug 报告应包含子代理上下文）。

### 3.4 后台守护进程（Daemon）稳定性
- **涉及工具**：Claude Code（#88307 删除 settings.json、#89205 进程泄漏）、Copilot CLI（#4612 FileWatch 事件循环失控致 13GB 日志）、Gemini CLI（#26522 Auto Memory 无限重试）
- **具体诉求**：孤儿进程 CPU 空转、配置文件被静默删除、事件循环死锁、后台任务与权限请求冲突。

### 3.5 权限安全模型收紧
- **涉及工具**：Gemini CLI（#28902 `$VAR` 绕过命令替换检测、SSRF 修复）、Qwen Code（#10197 Bash 环境变量绕过、#10199 MCP 权限别名混淆）、Claude Code（#89854 安全策略误伤合法运维）
- **具体诉求**：默认 fail-closed 策略、修复配置损坏时的权限失效、阻止变量展开/别名混淆绕过安全拦截、同时减少对合法任务的误拦截。

### 3.6 Windows/WSL 生态兼容性
- **涉及工具**：OpenAI Codex（#40752、#40715、#40819 等 5 条高热度）、Qwen Code（#10228 Web UI 不可用）、Pi（#8688 powershell 工具前缀错乱）
- **具体诉求**：桌面端启动失败、MCP 配置读取报错、WSL 互操作退化、安装路径限制。

### 3.7 会话恢复与状态持久化
- **涉及工具**：Copilot CLI（#4629 hooks 不加载、#4605 版本卡住）、Pi（#7724 恢复重放已删除消息）、OpenCode（#44958 响应隐藏、#45456 无限重试）、Kimi Code（#2620 Cron 导致回复丢失）
- **具体诉求**：恢复后的上下文一致性、失败/已删除消息不应重新出现、版本升级路径透明。

### 3.8 新模型快速适配
- **涉及工具**：Pi（#8690 GLM-5.3 Flash）、CodeWhale（#5631 qwen3.8-flash、#5622 Kimi k3-256k）、OpenCode（#45485 Mistral 流式工具调用）
- **具体诉求**：新模型发布后 CLI 工具需快速跟进，同时注意多模态能力识别（避免静默降级）。

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线/突出特点 |
|------|---------|---------|------------------|
| **Claude Code** | 企业级编码 Agent | 专业开发者、企业团队 | 深度 Anthropic 模型集成；技能系统（Skills）结构化；反馈机制（SendFeedback）；最大痛点在 Daemon 稳定性 |
| **OpenAI Codex** | 跨平台全能 Agent | 全栈开发者、Windows 用户 | Rust 核心；TUI/桌面端/GUI 多形态；Windows/WSL 兼容是其短板也是改进重点；权限配置文件精细化 |
| **Gemini CLI** | 多模态 Agent 平台 | 依赖 Google 生态的开发者 | 强调查 Browser Agent 和多模态能力；MCP 安全加固（SSRF、fail-open 修复）领先；子代理稳定性待提升 |
| **GitHub Copilot CLI** | GitHub 生态原生 CLI | GitHub 重度用户、企业 CI/CD | 与 GitHub 深度集成；Hooks 和 OpenTelemetry 追踪；MCP 双时代协议兼容问题突出；非交互模式权限管理是短板 |
| **Kimi Code CLI** | 轻量级编码助手 | 中文开发者为主 | Moonshot 生态；当前活跃度低，处于打磨阶段；Cron 交互设计、版本管理透明化是当前关注点 |
| **OpenCode** | 开源社区驱动 Agent | 开源爱好者、实验型团队 | 插件生态丰富；Web UI/TUI 双形态；最大痛点是 Agent 循环失控和内存泄漏；社区反馈直接 |
| **Pi** | 高性能 TUI 专家 | 追求效率的专业开发者 | 极致的 TUI 交互体验（编辑器增强、鼠标支持）；NVIDIA InferenceHub 内置；O(n²) 性能问题修复迅速 |
| **Qwen Code** | 阿里生态多智能体平台 | 中英文开发者、企业团队 | Agent Team（团队协作）是其差异化方向；Web Shell (serve 模式)；权限系统语义变化引争议；多智能体竞态问题暴露 |
| **DeepSeek TUI (CodeWhale)** | 开源多后端 TUI | 技术爱好者、依赖第三方模型的用户 | 聚焦 TUI 体验和多模型接入（OpenRouter/Kimi/Moonshot）；会话级存储隔离；企业级部署能力增强中 |

---

## 5. 社区热度与成熟度

### 第一梯队：高活跃 + 高成熟（大厂背书，版本迭代稳健）
- **Claude Code、OpenAI Codex、Gemini CLI**：日活 Issue 数十条，版本发布频繁，社区反馈闭环快。但都存在"核心功能已稳定、外围稳定性问题集中爆发"的特征（Daemon、Windows 兼容、MCP 边界）。

### 第二梯队：高活跃 + 快速迭代（开源社区驱动）
- **OpenCode、Pi、Qwen Code**：Issue 讨论热度高，PR 提交密集（每小时都有新活动），新功能迭代速度快于大厂产品，但稳定性问题也更多样（内存泄漏、循环失控、并发竞态）。社区既是用户也是贡献者，修复速度依赖社区力量。

### 第三梯队：中低活跃 + 蓄势待发
- **Copilot CLI**：虽有活跃 Issue，但 PR 空窗说明维护团队响应节奏较慢，或正处于内部重构期（1.0.80 回归问题未修复）。
- **CodeWhale (DeepSeek TUI)**：仓库规模较小但活跃度上升，近期从个人项目转向社区共建（外部贡献者 PR 增多），处于快速成长阶段。
- **Kimi Code CLI**：活跃度低，版本发布不频繁，处于功能打磨期，社区覆盖范围有限。

---

## 6. 值得关注的趋势信号

### 趋势一：Token 成本控制成为核心竞争维度
MCP schema 提前注入导致的 354K token 暴涨（Copilot CLI #4613）、缓存 TTL 失效（Claude Code #84253）、工具 schema 全量发送（Copilot CLI #4588）——成本敏感度已从"优化建议"变为"生产环境采用的门槛"。**开发者应关注**：工具是否提供 schema 延迟加载、缓存生命周期可配置、token 用量可视化等能力。

### 趋势二：Agent 循环失控是"隐形杀手"
多个工具同时报告 Agent 陷入无进展工具调用循环（OpenCode 364 次相同 grep、Gemini CLI 子代理误报成功）。这不仅是效率问题，更是**安全与成本风险**。**开发者应关注**：工具是否提供 max-turns 硬性限制、无进展检测（相同调用去重计数）、循环打破的自动中断机制。

### 趋势三：权限安全模型走向 "fail-closed" 默认策略
Gemini CLI 修复 SSRF 和 fail-open 配置风险、Qwen Code 修复 Bash/MCP 权限绕过、Claude Code 面临安全策略误伤合法任务——安全模型正从"尽力而为"转向"默认拒绝、显式放行"。**开发者应关注**：权限配置是否会因配置损坏而静默失效、安全规则是否可被变量展开/别名混淆绕过、规则变更是否有明确提示。

### 趋势四：多智能体协作从"实验"走向"生产"
Qwen Code Agent Team 的竞态审计、OpenCode 对 subagent 循环的系统性修复、Gemini CLI 子代理稳定性持续投入——多 Agent 协作已不再只是 demo，而是要扛住真实工作负载。**开发者应关注**：多 Agent 并发时的生命周期隔离、结果持久化一致性、以及子代理的可观测性（trace 是否能贯穿主-子会话）。

### 趋势五：Windows/WSL 成为"第二战场"
Codex 在 Windows 桌面端出现系统性退化（5 条高热度 Issue 指向同一根因）、Pi 的 WSL 渲染问题、Qwen Code Web UI 在 serve 模式的不可用——跨平台一致性已成为产品能否进入企业市场的关键。**开发者应关注**：Windows 下的路径处理、MCP 配置读取、WSL 互操作、以及 Electron/Tauri 打包的二进制路径问题。

### 趋势六：可观测性与调试工具链成为刚需
CodeWhale 的 per-thread usage 端点、Copilot CLI 的 OpenTelemetry 追踪上下文、Qwen Code 的 Web Shell 工具摘要折叠、Pi 的监控基础设施——社区正从"能用"走向"可诊断"。**开发者应关注**：工具是否提供会话级别的 token/成本/性能数据导出、子代理执行轨迹共享、以及错误信息的可操作性（明确修复路径而非仅描述现象）。

---

## 结论与建议

### 对技术决策者：
- **选择标准**不应只看模型能力，更应关注**后台进程稳定性、Windows 兼容性、Token 成本可视化和权限安全模型的成熟度**。当前阶段，Claude Code 和 Gemini CLI 在安全加固上领先，Codex 在 Windows 生态投入最大（但尚未完全解决），Qwen Code 和 OpenCode 在多智能体协作上走得最前。

### 对开发者：
- **警惕 Agent 循环失控**：无论使用哪种工具，建议设置 max-turns 硬限制和 token 预算告警，避免"无人值守"的长时间运行任务。
- **关注权限配置变更**：升级前务必阅读 release notes 中 Breaking Changes 部分，Qwen Code 0.22.1 的 permissions.allow 语义变化是一个典型教训。
- **善用社区反馈渠道**：当前最优做法是投票和评论而非重复提交 Issue，高热度 Issue 更容易获得维护者优先响应。

### 对工具厂商：
- **优先解决稳定性而非堆功能**：多个工具在 24 小时内收到 5+ 条指向同一根因的 Issue（Codex 的 Windows 问题、Claude Code 的 Daemon 问题），系统性修复远比零散打补丁重要。
- **安全模型需兼顾"防绕过"与"不误伤"**：Claude Code 的过度拦截引发了合法运维用户的强烈不满，安全策略应提供豁免路径和透明分级。
- **MCP 生态协议兼容性是共同短板**：双时代协议（modern discover + legacy initialize）的不一致性、schema 校验报错不可读、配置损坏 fail-open——建议行业层面推动协议标准化，减少各工具间的碎片化。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-27）

## 1. 热门 Skills 排行

- **skill-creator 修复系列（#1298 / #1099 / #1050）** [PR #1298](https://github.com/anthropics/skills/pull/1298) · [PR #1099](https://github.com/anthropics/skills/pull/1099) · [PR #1050](https://github.com/anthropics/skills/pull/1050)
  功能：修复 skill-creator 中 `run_eval.py` 在 Windows 上读取子进程管道崩溃、触发检测失效、编码错误及并行 worker 问题。核心 bug 导致评估循环对所有描述报告 `recall=0%`（对应 Issue #556），使优化过程针对噪声进行。社区关注度极高，三个 PR 互相补充。**状态：均 OPEN**。

- **document-typography（#514）** [PR #514](https://github.com/anthropics/skills/pull/514)
  功能：AI 生成文档的排版质量控制 — 修复孤词换行（1-6 个词溢出到下一行）、寡行段落（节标题悬在页底）和编号错位。直击 AI 生成文档的普遍痛点，用户不会主动要求好的排版但影响观感极重。**状态：OPEN**。

- **Hivemind：零成本多智能体编排（#1628）** [PR #1628](https://github.com/anthropics/skills/pull/1628)
  功能：Claude Code 将机械性工作委托给运行在免费模型上的 headless [opencode](https://opencode.ai) worker，Claude Code 保留规划、评审和合并角色。核心理念是"昂贵模型的上下文才是稀缺资源"。代表社区对成本优化的前沿探索。**状态：OPEN**。

- **self-audit（#1367）** [PR #1367](https://github.com/anthropics/skills/pull/1367)
  功能：交付前审计 skill — 先做机械文件验证（每个声称的输出文件是否存在），再按损害严重性优先级做四维推理审计。通用性强，适配任何项目/技术栈/模型。**状态：OPEN**。

- **testing-patterns（#723）** [PR #723](https://github.com/anthropics/skills/pull/723)
  功能：覆盖完整测试栈的 skill — 测试哲学（Testing Trophy 模型）、单元测试（AAA 模式）、React 组件测试（Testing Library）及边界情况。社区对系统化测试指导的需求明确。**状态：OPEN**。

- **claude-api 更新（#1607）** [PR #1607](https://github.com/anthropics/skills/pull/1607)
  功能：将四个已退役模型 ID 标记为 retired。看似简单但直接关联 Issue #1487（该 skill 单次调用注入 ~156k token 撑爆上下文窗口）及 #1603。文档维护类 PR 的关注度侧面反映 `claude-api` skill 的用户基数。**状态：OPEN**。

## 2. 社区需求趋势

- **安全与信任边界（Issue #492，43 评论）** — 社区 skill 在 `anthropic/` 命名空间下分发，伪装成官方 skill 形成信任边界漏洞。用户可能给社区 skill 授予过高权限。这是当前社区最关注的安全议题。
- **组织级共享（Issue #228，16 评论，👍 8）** — 希望直接在 Claude.ai 组织内共享 skill，免去下载–发送–手动上传的繁琐流程。对应企业采用的关键堵点。
- **工具可靠性修复（Issue #556，12 评论，👍 7）** — `run_eval.py` 触发率为 0% 的核心 bug，影响所有使用 skill-creator 优化 skill 描述的用户。同源 PR 有 #1298、#1099、#1050。
- **重复安装问题（Issue #189，👍 9）** — `document-skills` 与 `example-skills` 插件安装后内容完全一致，造成上下文窗口重复占用。
- **上下文窗口压力（Issue #1487）** — `claude-api` skill 单次调用注入 ~156k tokens。Skill 设计需考虑 token 效率，而非一味堆砌内容。

## 3. 高潜力待合并 Skills

- **skill-quality-analyzer + skill-security-analyzer（#83）** [PR #83](https://github.com/anthropics/skills/pull/83) — 元 skill，从结构/文档/安全性等五维评估 skill 质量，至今 OPEN 且社区讨论持续（最新更新 2026-01-07）。若合并将填补 skill 生态的质检空白。
- **serviceNow 平台 skill（#568）** [PR #568](https://github.com/anthropics/skills/pull/568) — 覆盖 ITSM、ITOM、ITAM/SAM、FSM、HRSD、CSM、SPM、漏洞响应、安全事件响应及 IntegrationHub 的全面平台助手。8 月仍有更新，接近可合并状态。**状态：OPEN**（近期活跃）。
- **pyxel 复古游戏开发 skill（#525）** [PR #525](https://github.com/anthropics/skills/pull/525) — 结合 pyxel-mcp 的工作流（write → run_and_capture → inspect → iterate），近期有更新（2026-07-15），方向垂直且明确。**状态：OPEN**。

## 4. Skills 生态洞察

**社区最集中的诉求是"官方工具链的可靠性"——尤其是 skill-creator 评估管道的核心 bug（#556）和 Windows 兼容性（#1298/#1099/#1050），其次是对 skill 分发安全（#492）和上下文窗口效率（#1487/#189）的深层担忧，而新 skill 提案则集中在质量审计（#83/#1367）、成本优化（#1628）与垂直场景覆盖（#568/#525）三个方向。** 一句话：生态已从"能做什么"进入"如何可靠、安全、高效地做"的成熟期。

---

# Claude Code 社区动态日报 — 2026-08-27

---

## 1. 今日速览

昨日发布 v2.1.247，核心变化是新增 `SendFeedback` 反馈草稿工具，并可在设置中关闭。社区侧，两个高热度 Issue 引发广泛讨论：递归技能发现功能请求（63 👍）、Artifact 公共分享持续失败（20 👍）。同时，多条涉及后台守护进程（Daemon）在升级、环境变量、安全拦截等方面的严重 bug 被密集报告，稳定性是当前开发者最强烈的痛点。

---

## 2. 版本发布

### v2.1.247
- 新增 `SendFeedback` 工具：当会话中出现异常时，Claude 可草拟一份反馈报告供用户审阅，通过 `/feedback` 发送。
- 设置项新增 `feedbackDrafts`，可关闭该功能。
- 新增 `{id, text, cooldownSessions, priority}` 条目、`tipsFile` 和 `label` 字段（完整说明见 Release 页面）。

---

## 3. 社区热点 Issues（Top 10）

**1. [FEATURE] 递归技能发现 — `~/.claude/skills/` 子目录扫描**  
[#18192](https://github.com/anthropics/claude-code/issues/18192) | 👍 63 | 💬 43 | 已关闭  
当前仅扫描技能目录顶层，嵌套目录中的 `SKILL.md` 不会被发现。该请求已获大量支持，社区对技能组织结构化的需求强烈。

**2. Artifact 公共分享持续失败 — "This version can't be shared publicly"**  
[#79824](https://github.com/anthropics/claude-code/issues/79824) | 👍 20 | 💬 14  
即使重新发布或新建 Artifact，分享开关仍报错。跨版本持续存在，影响协作场景，社区反馈多次复现。

**3. 登录验证邮件被抑制 — 支持机器人无升级路径**  
[#79808](https://github.com/anthropics/claude-code/issues/79808) | 👍 4 | 💬 13  
用户无法收到验证邮件，且无人工客服通道，属于账号层面的阻塞性问题。

**4. [P0] Opus 4.7 误报“网络安全话题”拦截 — 影响合法商业运维**  
[#89854](https://github.com/anthropics/claude-code/issues/89854) | 💬 4  
安全层将普通运维任务错误标记为网络攻击，用户认为过度拦截已影响正常业务。

**5. Plan 模式静默退出并错误执行 ExitPlanMode**  
[#85095](https://github.com/anthropics/claude-code/issues/85095) | 💬 9  
Plan 模式未按预期退出，Agent 将退出请求当作指令执行，存在控制流风险。

**6. 后台任务通知取消挂起的权限请求，且消息伪造用户身份**  
[#85408](https://github.com/anthropics/claude-code/issues/85408) | 💬 4  
后台通知与权限请求冲突，且提示文字冒充用户操作，存在安全隐患。

**7. [FEATURE] 请求繁体中文（zh-TW）本地化支持**  
[#35600](https://github.com/anthropics/claude-code/issues/35600) | 👍 16 | 💬 3  
已有简体中文支持，社区持续呼吁增加繁体中文，覆盖港台澳用户。

**8. Prompt 缓存 TTL 失效 — 每 5 分钟以上间隔即触发全量重写**  
[#84253](https://github.com/anthropics/claude-code/issues/84253) | 💬 2  
2.1.218+ 不再请求 1 小时缓存，5 分钟以上的空白间隔导致完整缓存重建，Token 成本显著上升。

**9. 定时任务会话进程泄漏，每个孤儿进程空转 10% CPU**  
[#89205](https://github.com/anthropics/claude-code/issues/89205) | 💬 2  
两个月前报告的问题在 2.1.237 仍未修复，且孤儿进程持续消耗 CPU，长期无人跟进。

**10. 后台守护进程删除 `~/.claude/settings.json`（符号链接场景）**  
[#88307](https://github.com/anthropics/claude-code/issues/88307) | 👍 3 | 💬 1  
使用 nix/home-manager 的用户将 settings.json 符号链接到只读目录，后台任务静默删除该文件，导致所有设置丢失，属数据丢失级 Bug。

---

## 4. 重要 PR 进展

| PR | 说明 |
|---|---|
| [#13437](https://github.com/anthropics/claude-code/pull/13437) | **hookify 插件修复**：将绝对导入改为相对导入，解决 “No module named hookify” 错误（跨平台） |
| [#58673](https://github.com/anthropics/claude-code/pull/58673) | 占位 PR，无实质内容，已搁置 |

> 注：当前 PR 仅两条，其中一条为无效提交，社区活跃度集中在 Issue 侧。

---

## 5. 功能需求趋势

- **技能系统结构化**：递归扫描、嵌套目录支持（#18192），用户需要按模块组织技能。
- **本地化扩展**：繁体中文支持（#35600），持续推动多语言覆盖。
- **会话状态可视化**：请求在 `claude agents --json` 中暴露“等待用户输入”状态（#85192），便于外部工具集成。
- **Agent 视图按项目隔离**：自动触发的 Agent 视图展示全局会话，用户希望按项目维度过滤（#85011）。

---

## 6. 开发者关注点

- **守护进程稳定性**：多起 Daemon 问题被集中报告——升级风暴（#83715）、自重启路径失效（#84827）、权限竞态（#77384）、环境变量不生效（#85116）。后台会话是当前稳定性短板。
- **安全策略误伤**：Opus 4.7/4.8 对安全/运维类任务过度拦截（#89854、#90000），开发者呼吁更精准的安全分类。
- **数据安全**：会话文件被删除（#88307）、跨会话误删文件（#87981），开发者高度关注数据完整性。
- **成本控制**：Prompt 缓存 TTL 失效（#84253）导致 Token 成本上升，是高频成本敏感点。
- **持续未修复问题**：会话进程泄漏（#89205）、技能加载偶发失败（#89319）等多条 bug 跨越多个版本仍未解决，社区对修复速度不满。

---

*本日报基于 GitHub 公开数据自动整理，仅供参考。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-27

## 今日速览

今日 Codex 稳定版发布 v0.150.1，主要修复远程上下文压缩中保留图片的 token 预算问题。社区焦点集中在 Windows 桌面端 26.820 系列更新引发的大量启动失败与 MCP 配置报错，已形成多条高热度 Issue。与此同时，多项针对权限安全、代码模式追踪与 TUI 代理权的 PR 已合入。

## 版本发布

**rust-v0.150.1 (稳定版)**
- Bug Fix: 远程压缩现默认将保留图像计入 token 预算，按需裁剪旧图（#41003）
- 完整变更：[compare/rust-v0.150.0...rust-v0.150.1](https://github.com/openai/codex/compare/rust-v0.150.0...rust-v0.150.1)

**rust-v0.151.0-alpha.4**：常规 alpha 推进，无显著说明。

## 社区热点 Issues（Top 10）

1. **#40752** [Windows] 桌面应用更新后无法启动（"Unable to locate Codex CLI"）— 78 评论 / 48 👍 | [链接](https://github.com/openai/codex/issues/40752)
   Windows 11 用户在更新至 v26.820.60940 后应用直接崩溃，报错与 `.cmd` 包装器及 `spawn EINVAL` 相关。评论超高，疑似为 26.820 引入的深层 Windows 兼容问题。

2. **#40715** [Windows] MCP 配置 "invalid transport in mcp_servers.codex_app" — 67 评论 / 78 👍 | [链接](https://github.com/openai/codex/issues/40715)
   稳定版 26.820 在读取 `mcp_servers.codex_app` 时报 invalid transport，Beta 版本正常，大量 Windows 用户受影响。

3. **#40819** [Windows/WSL] 恢复 WSL 线程失败，同样报 invalid transport — 59 评论 / 53 👍 | [链接](https://github.com/openai/codex/issues/40819)
   与 #40715 同根因，WSL 场景下具体表现为恢复历史会话失败，社区要求优先修复。

4. **#34035** [功能] 永久移除 5 小时用量限制 — 17 评论 / 145 👍 | [链接](https://github.com/openai/codex/issues/34035)
   用户希望将 7 月临时取消的 5 小时限制改为永久策略。虽然评论不多，但点赞量极高，是社区强烈诉求。

5. **#40881** [Windows/WSL] Desktop 在 WSL 模式无法新建会话 — 26 评论 / 7 👍 | [链接](https://github.com/openai/codex/issues/40881)
   同属 26.820 Windows 系列问题，Agent Environment 配置为 WSL 时无法创建新对话。

6. **#40700** [Windows] 捆绑 codex.exe 从 WindowsApps 重定位失败 — 29 评论 | [链接](https://github.com/openai/codex/issues/40700)
   应用无法启动，根本原因是 MS Store 包路径限制导致的二进制重定位失败。与 #40752 构成 Windows 启动问题的"双引擎"。

7. **#32759** [macOS] GPT-5.6 Sol 执行 shell 命令失败（code-mode host exited during handshake）— 13 评论 / 3 👍 | [链接](https://github.com/openai/codex/issues/32759)
   一个持续一个多月的问题仍未解决，跨多版本存在，macOS 上 CLI 模式执行工具调用即崩溃。

8. **#41019** [Windows] Electron 资源缺少 bin/codex — 13 评论 / 2 👍 | [链接](https://github.com/openai/codex/issues/41019)
   新版应用的资源目录中未包含 CLI 二进制文件，与 #40752 类似，可能是 Windows 打包流水线的问题。

9. **#40611** [macOS] 高级安全登录后陷入登录循环 — 9 评论 | [链接](https://github.com/openai/codex/issues/40611)
   开启 Advanced Account Security 后应用反复退出登录，影响 Pro 用户。

10. **#38350** [Web] 定时任务运行成功后自动暂停 — 47 评论 | [链接](https://github.com/openai/codex/issues/38350)
   用户创建的计划任务在成功执行后却被系统自动改为暂停状态，且无用户授权。自动化可靠性问题，引发较多讨论。

## 重要 PR 进展（Top 10）

1. **#41050** 为持久模式（ReasoningEffort::Persistent）添加开发者指令支持 | [链接](https://github.com/openai/codex/pull/41050)
   新增主动性和后续引导指令，并允许模型元数据覆盖或禁用。

2. **#41046** TUI 委托提示（create_thread / send_message_to_thread）保留工具级权限，而非被记录为用户输入 | [链接](https://github.com/openai/codex/pull/41046)

3. **#41041** 加密 history/notes 工具的敏感参数，附 `x-openai-encrypted-tool-arguments` 标记 | [链接](https://github.com/openai/codex/pull/41041)

4. **#41017** 在 gRPC code-mode 中传递 W3C `traceparent`，修正跨边界分布式追踪链路 | [链接](https://github.com/openai/codex/pull/41017)

5. **#41003** 将保留图像压缩预算回移植到 0.150 稳定线（即今日 v0.150.1 的核心修复）| [链接](https://github.com/openai/codex/pull/41003)

6. **#41005** 为插件 MCP 调用附加验证过的访问上下文（cyber_trusted_access）| [链接](https://github.com/openai/codex/pull/41005)

7. **#41002** 支持在 `turn/start` 中以独立工具输出（standalone tool output）启动回合 | [链接](https://github.com/openai/codex/pull/41002)

8. **#40999** 加固 Linux 托管代理监听器交接：改为传递 loopback TCP 监听器而非 Unix socket，消除沙箱可读路径依赖 | [链接](https://github.com/openai/codex/pull/40999)

9. **#40994** 默认启用保留图像预算（compaction_image_budget），处理上下文压缩的 token 超限 | [链接](https://github.com/openai/codex/pull/40994)

10. **#40989** 在核心 API 中暴露权限配置文件的解析结果（permission profile resolution）| [链接](https://github.com/openai/codex/pull/40989)

## 功能需求趋势

- **配额制度改革**：`#34035`（108 赞）与 `#41016`、`#41004` 反映了用户对 5 小时/每周配额的不满，要求取消或改为顺序消耗，而非同时扣除。
- **Agent 间上下文管理**：`#23218` 希望 agent 能主动清空上下文并在同一 session 内继续新任务，属于轻量级"任务切换"能力。
- **终端体验增强**：`#38575` 建议支持 DECSET 2031，使 TUI 实时响应终端主题变化。
- **非交互 MCP 工具调用**：`#24135` 希望在 `codex exec` 中无需全局绕过沙箱即可授权 MCP 工具调用，与 CI/CD 自动化场景强相关。

## 开发者关注点

- **Windows 稳定性是当前最大痛点**：多个高热度 Issue（#40752、#40715、#40819、#40881）都指明 26.820 系列在安装路径切换、MCP 配置读取、WSL 互操作方面存在系统性退化，影响正常使用 vs 测试版可用性。
- **code-mode host 握手失败** 在 Windows 桌面端（#40943、#41049）和 macOS CLI（#32759）均有复现，提示 gRPC code-mode 初始化路径在不同平台/模型组合下仍不稳定。
- **GUI 视觉回归**（#40782、#41047）虽非致命，但用户感知明显，可能是 Electron 渲染或字体配置调整导致。
- **沙箱与权限边界** 相关的 PR 集中出现（#41005、#41041、#41020、#41006），表明官方正在积极收紧 MCP/技能的工具权限粒度，兼顾安全与可用性。

---
*本日报基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-27** | 数据来源：github.com/google-gemini/gemini-cli


## 今日速览

今日最核心的进展是发布了 v0.59.0-nightly 版本，修复了 MCP OAuth 元数据发现与认证流程中的 SSRF 安全漏洞。社区讨论焦点集中在 Agent 子代理的稳定性和 `MAX_TURNS` 误报完成问题上，多个高优先级 Bug 持续被开发者关注。安全方面，针对 MCP 配置损坏导致的安全策略失效（fail-open）已有多个修复 PR 提出。

---

## 版本发布

**v0.59.0-nightly.20260827.g3c311beac**

- 修复核心安全漏洞：防止 MCP OAuth 元数据发现和认证过程中的 SSRF（服务端请求伪造）攻击
- **变更日志**：https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260826.g64b5b79a6...v0.59.0-nightly.2026

---

## 社区热点 Issues

### 1. Subagent 达到 MAX_TURNS 后被误报为成功 [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **优先级**：P1 | **评论**：13 | **👍**：2
- **核心问题**：`codebase_investigator` 子代理在达到最大轮次限制后仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了中断事实，导致用户对执行结果产生误判
- **社区反应**：该问题被标记为 `need-retesting`，社区关注度高。此问题直接影响 Agent 执行结果的可靠性

### 2. 通用 Agent 执行挂起无响应 [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **优先级**：P1 | **评论**：8 | **👍**：8
- **核心问题**：`gemini-cli` 委托给通用子代理时永久挂起，简单操作（如创建文件夹）都无法完成，用户最长等待 1 小时仍需手动取消
- **社区反应**：获得 8 个 👍，是目前社区反馈最多的 Agent 稳定性问题之一。用户发现通过提示词禁止委托子代理可绕开此问题

### 3. Shell 命令执行完成后卡在"等待输入"状态 [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **优先级**：P1 | **评论**：4 | **👍**：3
- **核心问题**：简单 CLI 命令执行完毕后仍显示命令激活并卡在 "Awaiting user input" 状态，即使在明确不会请求输入的命令上也会复现
- **社区反应**：这是核心交互流程的高频痛点，直接影响日常使用体验

### 4. Browser 子代理在 Wayland 环境失败 [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
- **优先级**：P1 | **评论**：4 | **👍**：1
- **核心问题**：浏览器子代理在 Wayland 显示服务器下无法正常工作，终止原因为 "GOAL"
- **社区反应**：影响 Linux 用户的浏览器自动化能力，已标记为 `need-retesting` 等待复测

### 5. 子代理上下文缺失导致 Bug 报告不完整 [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)
- **优先级**：P1 | **评论**：2
- **核心问题**：`/bug` 报告仅包含主会话信息，缺少子代理执行过程中的上下文，使得调试困难
- **社区反应**：该问题关联 Issue #21761，属于 Agent 可观测性的重要缺口

### 6. Gemini 不会主动使用自定义 Skills 和子代理 [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **优先级**：P2 | **评论**：6
- **核心问题**：用户反馈 Gemini 基本不会主动使用自定义 skills 和子代理，即使定义了 `gradle` 和 `git` 等具有明确描述的 skills
- **社区反应**：这反映了 Agent 自主决策能力的不足，用户期望模型更智能地选择合适的工具

### 7. Browser Agent 忽略 settings.json 配置覆盖 [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)
- **优先级**：P2 | **评论**：3
- **核心问题**：`settings.json` 中的 `maxTurns` 等配置对 Browser Agent 无效，`AgentRegistry` 虽正确读取了配置但未生效
- **社区反应**：配置管理的一致性问题，影响用户对 Agent 行为的精细控制

### 8. 超过 128 个工具时遇到 400 错误 [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)
- **优先级**：P2 | **评论**：3
- **核心问题**：工具数量过多（>400）时 API 返回 400 错误，用户期望 Agent 能更智能地在启用工具范围内限制工具集
- **社区反应**：此问题对构建了大量自定义 MCP 工具的用户影响显著

### 9. Auto Memory 无限重试低信号会话 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **优先级**：P2 | **评论**：5
- **核心问题**：Auto Memory 仅当提取代理成功读取转录时才标记处理完成，对于判定为低信号的会话会无限重试
- **社区反应**：反映后台服务资源浪费的隐患，社区期望更智能的候选处理策略

### 10. 命令替换检测可被 `$VAR` 绕过 [#28902 关联](https://github.com/google-gemini/gemini-cli/pull/28902)
- **优先级**：P1（安全）
- **核心问题**：`detectBashSubstitution()` 的检查存在缺口，`$VAR` 和 `${VAR}` 变量展开模式可绕过安全拦截
- **社区反应**：虽然该条为 PR，但其修复的安全漏洞（GHSA-wpqr-6v78-jr5g）受到密切关注，涉及命令注入面

---

## 重要 PR 进展

### 1. **修复 MCP OAuth 中的 SSRF 漏洞** [#29081](https://github.com/google-gemini/gemini-cli/pull/29081)
- **状态**：已合并（CLOSED）
- **内容**：强制执行 RFC 9728 Section 7.7 和 RFC 8414 安全约束。远程 OAuth 端点强制使用 HTTPS，仅允许回环地址使用 HTTP；验证资源来源匹配
- **重要性**：由 josebalius 提交，是当前 nightly 版本的核心修复内容

### 2. **修复损坏的 MCP 启用配置被当作空配置处理** [#28787](https://github.com/google-gemini/gemini-cli/pull/28787)
- **状态**：已合并（CLOSED）| 优先级 P1
- **内容**：`readConfig()` 方法在 JSON 解析失败时返回空对象，导致服务器在配置损坏时默认启用所有服务器（fail-open），存在安全隐患
- **重要性**：安全相关修复，防止配置损坏时的安全策略失效

### 3. **阻止损坏 MCP 配置的 fail-open 和数据丢失** [#28794](https://github.com/google-gemini/gemini-cli/pull/28794)
- **状态**：已合并（CLOSED）| 优先级 P1
- **内容**：修复 `McpServerEnablementManager` 中 `mcp-server-enablement.json` 损坏或包含无效 JSON 时的问题，防止 fail-open 重启用和数据丢失
- **重要性**：与 #28787 互补，共同处理 MCP 配置损坏场景

### 4. **阻止 `$VAR` / `${VAR}` 变量展开绕过** [#28902](https://github.com/google-gemini/gemini-cli/pull/28902)
- **状态**：开放中 | 优先级 P1（安全）
- **内容**：修复 `detectBashSubstitution()` 和 `detectPowerShellSubstitution()` 中不完整的检查，阻止变量展开绕过安全拦截；同时加固 CI 工作流
- **重要性**：修复 GHSA-wpqr-6v78-jr5g 安全通告的绕过路径

### 5. **忽略转义 `@` 符号进行补全模式检测** [#28903](https://github.com/google-gemini/gemini-cli/pull/28903)
- **状态**：开放中 | 优先级 P1
- **内容**：在向后扫描 `@` 补全触发时，检查反斜杠数量；奇数个反斜杠（如 `\@`）视为转义，不触发 AT 补全模式
- **重要性**：提升 CLI 补全体验的准确性

### 6. **在重试时将 nudge 注入对话内容以保留前缀缓存** [#28914](https://github.com/google-gemini/gemini-cli/pull/28914)
- **状态**：开放中
- **内容**：将 on-retry nudge 消息从 `config.systemInstruction` 移至 `contents` 数组末尾（用户轮次后缀），保留静态提示前缀缓存，确保模型在生成前立即看到恢复提示
- **重要性**：修复 #28909，兼顾性能和模型行为

### 7. **WhisperModelManager 原子下载与失败清理** [#28917](https://github.com/google-gemini/gemini-cli/pull/28917)
- **状态**：开放中
- **内容**：修复 #28644，写入临时文件、处理背压/流错误、验证下载长度、失败清理，最终原子重命名
- **重要性**：提升本地语音模式的稳定性

### 8. **WhisperTranscriptionProvider 缓冲部分标准输出块** [#28916](https://github.com/google-gemini/gemini-cli/pull/28916)
- **状态**：开放中
- **内容**：修复 #28648，引入行缓冲机制，确保跨任意 `data` 事件分割的时间戳转录行能正确拼接
- **重要性**：解决本地语音模式下的文本丢失问题

### 9. **非沙盒环境仅识别 DEBUG=true/1** [#28911](https://github.com/google-gemini/gemini-cli/pull/28911)
- **状态**：开放中
- **内容**：沙盒启动器对 `DEBUG` 环境变量的真值判断与容器入口点保持一致，避免 `DEBUG=false` 被误判为启用
- **重要性**：修复调试标志位语义不一致的问题（关联 #28885）

### 10. **受限模式下强制失败闭合工作区信任并过滤 mcpServers** [#29099](https://github.com/google-gemini/gemini-cli/pull/29099)
- **状态**：开放中
- **内容**：在 `@google/gemini-cli-a2a-server` 中强制 fail-closed 工作区信任解析，在不受信任或受限环境中过滤仓库定义的 `mcpServers`
- **重要性**：防止服务器启动时的意外进程执行，增强安全边界

---

## 功能需求趋势

### 1. **Agent 自主性与工具使用能力**
社区最关注的方向。多个 Issue 反映 Gemini 不主动使用 Skills 和子代理（#21968）、Agent 的破坏性行为需要阻止（#22672）、以及对"self-awareness"的期待 —— 模型应理解自身机制、CLI 参数和热键（#21432）

### 2. **浏览器代理（Browser Agent）的稳定性与可配置性**
Browser Agent 相关的 Issue 持续活跃：Wayland 兼容性（#21983）、会话接管和锁恢复机制（#22232）、settings.json 覆盖失效（#22267），表明该功能仍处于快速迭代期

### 3. **持久化任务追踪与底层能力增强**
社区期待摆脱"上下文腐烂"的 WriteToDo，转向基于文件系统的持久化任务跟踪（#18836）；同时有关于 AST 感知文件读取和代码库映射的探索（#22745、#22746），旨在减少 token 消耗

### 4. **Auto Memory 系统的质量与安全**
多个 Issue 关注记忆系统问题（#26516），包括无限重试（#26522）、确定性脱敏（#26525）、无效补丁隔离（#26523），表明记忆系统正在功能完善与安全加固的并行阶段

### 5. **可观测性与轨迹共享**
社区期望子代理轨迹可通过 `/chat share` 共享（#22598），bug 报告包含子代理上下文（#21763），核心诉求是提升 Agent 行为的透明度和可调试性

---

## 开发者关注点

### 1. **Agent 执行可靠性**
开发者最集中的痛点是 Agent 的不稳定：挂起（#21409）、超时误报成功（#22323）、shell 命令卡死（#25166）。这些问题直接导致用户对 Agent 的信任度下降，且需要手动取消或绕行

### 2. **安全加固的需求迫切**
MCP 配置损坏导致的 fail-open、命令替换绕过（$VAR）、SSRF 漏洞等安全问题引发开发者高度关注。社区期望在这些场景下默认采取 fail-closed 策略，宁可拒绝执行也不要跳过安全检查

### 3. **子代理的不可观测性**
当发生意外时，开发者难以通过 bug 报告或共享轨迹了解子代理内部状态。上下文缺失使得问题定位耗时且困难，是提升调试效率的关键瓶颈

### 4. **配置管理的一致性**
Agent 对 settings.json 的忽略（#22267）、符号链接 Agent 无法识别（#20079）、DEBUG 标志位语义不一致（#28911）—— 配置项的实际行为与文档不一致让开发者感到困惑

### 5. **善后清理与副作用控制**
模型在临时目录创建工作脚本但缺乏清理机制（#23571），扩展更新可注入环境变量到 MCP 进程（#28863）—— 开发者希望 Agent 在完成工作后能更好地管理副作用，保持工作区整洁

---

> 日报由 AI 技术分析师自动生成，基于 2026-08-27 GitHub 数据。所有链接可点击直达对应 Issue/PR。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**2026-08-27**


## 今日速览

今日发布了 3 个预发布版本（v1.0.81-12 至 v1.0.81-14），重点修复了会话恢复时 read_agent 调用返回不完整历史的问题，并新增了 OpenTelemetry 追踪上下文传递能力。社区方面，**MCP 工具 schema 被过早注入导致 token 消耗激增**（#4613）成为最受关注的新问题，同时有多个 TUI 卡死/事件循环阻塞的 Bug 报告（#4612、#4533），稳定性问题仍是社区反馈的集中区域。

- **发布**：3 个 prerelease 版本，包含 Windows Entra ID 认证支持
- **热点**：MCP schema 提前注入导致 354K 起步 tokens 的回归 (#4613)
- **趋势**：TUI 稳定性/卡死、MCP 兼容性、配置发现路径灵活性


## 版本发布

### v1.0.81-14
**改进**
- 恢复大型会话时更快：先显示最近历史，同时后台加载旧消息。

**修复**
- 重复调用 `read_agent` 现在一致返回完整轮次历史（除非提供了 `since_turn`）。

### v1.0.81-13
**新增**
- Hooks 现在可以接收当前 OpenTelemetry 追踪上下文并发出相关联的 spans：输入新增 `traceparent`（当 span 带有 vendor state 时还有 `tracestate`）；命令 hooks 同时获得环境变量。

**修复**
- 子代理（subagent）内部的 hooks 生命周期事件（`hook.start`/`hook.end`）相关的修复。

### v1.0.81-12
**新增**
- Windows：受 Microsoft Entra ID 保护的远程 MCP 服务器现在可以通过操作系统认证代理（WAM）登录，通常无需额外提示。其他平台、`--device-code` 模式以及没有代理库的机器保持原有浏览器流程。

**修复**
- 反复恢复会话（resume）相关问题的修复。


## 社区热点 Issues（Top 10）

### 1. [#4613] 高严重性 1.0.80+ 回归：MCP schemas 被急切注入，启动 tokens 增加 354K
**作者**: xjli1972 | ⭐ 新提交 | 💬 2 条评论
**链接**: https://github.com/github/copilot-cli/issues/4613

自 1.0.80 起，CLI 不再延迟加载 MCP 工具 schema，全新会话即使处理无需任何工具的简单提示，也会将完整的环境 MCP 目录注入首个模型请求。导致**每次请求多消耗约 354K tokens**，成本影响显著。这是当前最受关注的性能/成本回归。初步怀疑与 1.0.80 的运行时重构有关，尚未看到维护者回应。

### 2. [#4612] [triage] FileWatch 主事件循环失控，冻结 TUI 并将调试日志撑大到 13 GB
**作者**: tdihp | ⭐ 新提交 | 💬 4 条评论
**链接**: https://github.com/github/copilot-cli/issues/4612

长时间运行/恢复的会话可能进入紧密循环，持续输出 `No connection accepted a host event {"kind":"FileWatch"}`。循环一旦开始，TUI 完全无响应，日志文件膨胀至 13 GB。影响严重，社区已有多人反馈类似现象。

### 3. [#252] [已关闭] 全局指令文件支持
**作者**: searleser97 | 👍 12 | 💬 11 条评论 | 状态: CLOSED
**链接**: https://github.com/github/copilot-cli/issues/252

最早期的功能请求之一：用户希望为所有仓库/工作树使用同一份全局指令文件，避免重复创建相同内容的 instructions 文件。虽然是早期请求，但今天被大量评论推动，说明社区对这一基础功能的持续需求。

### 4. [#2147] [已关闭] CAIP 400：input item ID 不属于此连接
**作者**: crgarcia12 | 💬 5 条评论 | 状态: CLOSED
**链接**: https://github.com/github/copilot-cli/issues/2147

使用 `gpt-5.4 (xhigh)` 模型时出现 `websocket_error`（错误码 400），提示 "input item ID does not belong to this connection"。与连接状态管理有关。今天状态标记为 CLOSED，推测已定位或修复。

### 5. [#4053] [已关闭] TUI 在 NFS/GPFS 上卡在 "Loading: N skills"：SIGCHLD 竞争条件
**作者**: raylim | 💬 4 条评论 | 状态: CLOSED
**链接**: https://github.com/github/copilot-cli/issues/4053

Linux 上家目录位于 GPFS/NFS 时，TUI 在 "Loading: N skills" 处无限挂起。根因是 Tokio 生成 `which gh` 子进程时与 30+ 并发线程发生 SIGCHLD 竞态。影响使用网络文件系统的企业用户，已标记关闭，可能是特定环境限制。

### 6. [#407] 添加 `/tools` 斜杠命令列出所有可用工具
**作者**: PhilippOesch | 👍 31 | 💬 2 条评论
**链接**: https://github.com/github/copilot-cli/issues/407

社区高赞功能请求（31 👍）。用户难以发现 Copilot CLI 可以访问哪些工具，希望有一个 `/tools` 命令来列出全部能力。支持度最高但进展缓慢，值得持续关注。

### 7. [#4433] [已关闭] 非交互模式（-p）下：工具调用审批中途被静默永久撤销
**作者**: nsd0okernicke | 💬 1 条评论 | 状态: CLOSED
**链接**: https://github.com/github/copilot-cli/issues/4433

非交互模式（`-p`）长时间会话（约 4-8 分钟、大量工具调用）后，所有写权限工具调用开始返回 "Permission denied and could not request permission from user"，会话不可恢复。对 CI/自动化场景影响严重，今日标记为关闭。

### 8. [#4605] latest-prerelease 查找让用户困在 1.0.81-9：releases 共享 created_at
**作者**: ms-jb | 👍 3 | 💬 1 条评论
**链接**: https://github.com/github/copilot-cli/issues/4605

`copilot update prerelease` 拒绝从 1.0.81-9 升级到 1.0.81-10，报告旧版本为最新。根因是 GitHub releases 共享相同 `created_at` 时，排序不稳定导致选中错误的 prerelease。影响所有快速迭代通道的用户。

### 9. [#4525] 1.0.81-1 在成功的 modern `server/discover` 后发送 legacy `initialize`，导致 -32022
**作者**: dmbutko | 💬 2 条评论
**链接**: https://github.com/github/copilot-cli/issues/4525

CLI 1.0.81-1 对一个使用 Python MCP SDK 2.0.0 双时代 runner 的 stdio 服务器初始化 MCP 失败。CLI 先以 `io.modelcontextprotocol/protocolVersion: 2026-07-28` 发出 modern `server/discover` 探测，随后又发送旧版 `initialize`，服务器以 -32022 拒绝。

### 10. [#4103] 插件市场克隆禁用 Git credential helpers，导致私有 HTTPS 仓库失败
**作者**: arnab9211 | 👍 3 | 💬 3 条评论
**链接**: https://github.com/github/copilot-cli/issues/4103

从私有 Azure DevOps HTTPS 仓库添加插件市场失败，但手动使用 Git Credential Manager 克隆同一仓库却成功。疑似与 v1.0.70 的 "Fail fast when marketplace plugin git auth needed" 变更相关。对企业用户使用私有插件源影响明显。


## 重要 PR 进展

今日窗口内没有新的 PR 活动（0 条）。上一条 PR 更新已超过 24 小时。


## 功能需求趋势

从近 24 小时的 Issues 中可以提炼出以下社区最关注的功能方向：

1. **MCP 生态完善与兼容性**（#4525, #3889, #4623）
   - 社区对 MCP 的支持深度要求越来越高：包括双时代协议兼容（modern discover + legacy initialize）、stdio transport 在 ACP 模式下支持、以及 Gemini 模型对 MCP 工具 schema 中 union type 的兼容性。MCP 正在成为核心集成层。

2. **可配置的发现路径与用户级设置**（#4622, #252）
   - 用户希望突破固定的 `%USERPROFILE%\.agents` 等路径，支持 XDG 风格或托管环境下的自定义发现根目录，同时全局指令文件的需求也持续存在。这反映了 CLI 正被集成到更复杂的企业/管理环境中。

3. **会话恢复与长期运行的可靠性**（#4612, #4605, #4629）
   - 多个 issue 指向会话恢复（`--resume`）的缺陷：hooks 不加载、FileWatch 事件循环失控、prerelease 版本被错误卡住。长期运行和断点续传是 CLI 成为日常工具的关键场景。

4. **模型与 Token 成本控制**（#4613, #4588, #4155）
   - MCP schema 提前注入导致 token 消耗暴涨是当前最尖锐的成本问题。同时 Gemini 模型的 400 错误和 schema 兼容性问题也表明多模型支持仍需打磨。社区对 token 效率和模型兼容性高度敏感。

5. **非交互/自动化模式增强**（#4433, #4628）
   - 非交互模式下审批被撤销、后台任务超时杀死父进程等问题，直接影响 CI/CD 和自动化脚本使用场景。自动化可靠性是开发者采用 CLI 的重要考量。


## 开发者关注点

1. **token 消耗失控（成本痛点）**：MCP schema 被急切注入导致每次请求多 354K tokens（#4613），加上此前非 Anthropic 模型全部工具 schema 每轮都发送的问题（#4588），**token 效率是当前最迫切的稳定性/成本痛点**。大量开发者使用付费额度运行 CLI，这类回归直接影响采用信心。

2. **TUI 稳定性与卡死问题**：FileWatch 事件循环失控（#4612）和并行子代理导致 UI 停止消费事件（#4533）都是严重阻碍日常使用的 Bug。TUI 是 CLI 的主要交互界面，任何冻结/无响应都会直接打乱工作流。

3. **resume 会话行为不一致**：`--resume` 时插件 hooks 不加载（#4629），且用户被卡在旧版本无法升级（#4605）——这两者叠加让"恢复会话"和"保持最新"这两个基本操作都不可靠，非常影响信任。

4. **认证与权限在长时间会话中失效**：非交互模式审批被静默撤销（#4433）、OAuth token 因 quota 字段验证失败（#4627），以及 Windows Entra ID 的改进，都表明认证和权限的生命周期管理是持续痛点。

5. **MCP 协议兼容性碎片化**：同一 CLI 在不同版本、不同模型、不同 MCP 服务器之间行为不一致（#4525, #4623, #4588），开发者需要花大量精力调试环境差异，而不是专注实际开发任务。

6. **私有化/企业环境支持**：私有多仓库插件市场克隆失败（#4103）和 NFS/GPFS 挂载环境下的卡死（#4053），说明企业级部署场景下的兼容性问题正在成为反馈热点。

> 注：今日 PR 窗口无更新，相关 PR 动态将在有活动时报道。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-27** | 数据来源：github.com/MoonshotAI/kimi-cli


## 今日速览

今日社区动态相对平静，**无新版本发布**，共有 2 个 Issue 更新和 1 个 PR 提交。值得关注的是，社区出现一个关于**版本号不一致**的困惑（官方脚本安装为 0.38 而仓库显示 1.49），以及一个关于**定时任务（Cron）与对话回复冲突**的功能缺陷报告。此外，有一项针对**嵌套任务取消机制**的修复 PR，旨在解决任务取消时的资源泄漏问题。


## 社区热点 Issues

### 1. Cron fire mid-reply swallows the previous assistant reply; unrecoverable via Ctrl+O（#2620）
- **作者**：tizerluo | **创建**：2026-08-26 | **评论**：0 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2620
- **摘要**：当定时 Cron 提醒在助手回复仍在屏幕上显示时触发，用户尚未回复，该回复会从可见对话历史中消失。滚动历史也无法找回，该轮被 Cron 轮次替换，Ctrl+O 展开也无法恢复。
- **关注理由**：这是一个**对话数据丢失**问题，直接影响用户对 Cron 功能的信任度。恢复机制缺失使问题无法通过用户侧操作解决，属于中高优先级的功能缺陷。

### 2. 官方脚本安装的最新版本是 0.38，这个怎么是 1.49（#2618）
- **作者**：mawenwu1983 | **创建**：2026-08-26 | **评论**：0 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2618
- **摘要**：用户发现官方安装脚本获取的版本号（0.38）与 GitHub 仓库显示的最新版本（1.49）不一致，疑惑两者区别。
- **关注理由**：**版本号混乱**容易引发信任危机和安装困惑，属于文档/发布流程层面的问题，官方应澄清版本策略或统一发布渠道。


## 重要 PR 进展

### 1. fix(soul): cancel nested task on outer cancellation（#2619）
- **作者**：koriyoshi2041 | **创建**：2026-08-26 | **评论**：暂无 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2619
- **摘要**：修复了 `run_soul` 生命周期清理中的问题——将初始的 `asyncio.wait()` 纳入清理范围，在外层协程被取消时同时取消并等待嵌套的 soul/cancel-event 任务，并添加了回归测试。修复 #2615。
- **关注理由**：这是一个**异步任务取消机制**的修复，解决的是资源泄漏和任务悬挂问题，对依赖长时间运行任务的场景（如 Soul 模式）稳定性有实际帮助。


## 功能需求趋势

| 趋势方向 | 具体表现 | 热度判断 |
|---------|---------|---------|
| 版本管理与安装体验 | 版本号不一致导致安装困惑（#2618） | 中（用户困惑） |
| 对话历史恢复与持久化 | Cron 触发导致回复丢失且不可恢复（#2620） | 高（数据丢失，影响信任） |
| 任务生命周期管理 | 嵌套任务取消机制的修复（#2619） | 中（稳定性和资源管理） |
| 定时任务（Cron）交互设计 | Cron 与对话的冲突需要更合理的交互策略 | 中（首次出现，需观察） |

**主要发现**：社区当前关注点集中在**稳定性**与**信任度**上，而非新功能或新模型支持。这表明 kimi-cli 已进入功能打磨和体验优化阶段。


## 开发者关注点

1. **对话数据不可恢复**：Cron 触发导致助手回复丢失且无法通过现有命令恢复——开发者对数据丢失敏感度高，此类问题会直接影响工作流信任。
2. **版本信息不透明**：安装脚本获取版本与仓库显示版本不一致，缺乏清晰的发布渠道说明和版本差异解释。
3. **任务取消与资源管理**：评论数不多，但 #2619 的 PR 表明开发者在主动补强异步任务的取消逻辑，这是长驻后台场景（如 Soul 模式）稳定运行的基石。

> 数据说明：本期活跃度偏低（24 小时内 2 Issue + 1 PR），建议持续关注 #2618（版本困惑）是否有官方澄清，以及 #2619 PR 能否顺利合入并发布。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-27

## 今日速览

今日社区讨论高度集中在**长期运行会话的内存泄漏与性能退化**问题上，多个高热度 Issue 均指向会话过程中的资源累积问题。同时，**Agent 陷入工具调用死循环**成为新的热点，已有四五个独立 Issue 报告了相似现象。PR 方面，kitlangton 提交了一系列以测试基建重构为主的 PR，另有多个针对 subagent 行为修正与 UI 细节修复的合入。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 社区热点 Issues

### 1. #20695 Memory Megathread
**状态**: OPEN | **评论**: 138 | **👍**: 105

内存问题集中讨论帖，社区将零散的内存报告统一收集于此。维护者明确要求用户**不要用 LLM 生成解决方案**，而是提供堆快照（heap snapshots）以辅助定位。这是当前社区关注度最高的议题，反映了内存问题影响的用户面之广。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/20695)

---

### 2. #45442 [2.0] subagent 无限循环：相同工具调用持续 50 分钟，无循环保护
**状态**: OPEN | **评论**: 3 | **创建**: 2026-08-27

背景 `general` subagent 在约 50 分钟内发出了 **364 次完全相同的 `grep` 调用**（相同 pattern、相同路径），期间无任何循环保护机制，导致无法控制的 token 消耗。该 Issue 与今日多个类似报告（#43603、#43673、#43800）共同指向一个系统性问题：**Agent 缺乏有效的无进展检测与循环终止机制**。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/45442)

---

### 3. #33890 Bun 1.3.14 在 Linux x86_64 上 SIGILL 崩溃
**状态**: CLOSED | **评论**: 7 | **👍**: 5

OpenCode 1.17.10（内置 Bun 1.3.14）在 AMD EPYC 9T24（Zen4 全 AVX-512 支持）上运行一段时间后触发 SIGILL 崩溃，降级到 1.17.9 同样崩溃。该问题在今日被关闭，但作为近期影响面较大的稳定性问题值得关注。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/33890)

---

### 4. #33213 server 模式长时间运行累积 JS 堆/交换内存
**状态**: CLOSED | **评论**: 6

`opencode serve` 在约 1.5 天内达到 **26.8 GiB cgroup 内存峰值**并留下约 2.86 GiB 交换内存，指向 WKFastMalloc/JSJITCode 区域的堆泄漏或碎片化。服务重启后内存立即回落。该问题已关闭，但内存泄漏是 #20695 大主题下的重要子议题。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/33213)

---

### 5. #42657 多 subagent 会话导致 TUI 卡顿（渲染线程 97% CPU）
**状态**: OPEN | **评论**: 4 | **创建**: 2026-08-14

运行 2-4 个并发 subagent 时，TUI 出现 1-3 秒的输入延迟，spinner 动画卡顿。在 Warp、Windows Terminal、WezTerm 三个终端中均复现。性能问题在 subagent 并行场景下尤为突出。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42657)

---

### 6. #44958 [BUG] 拒绝响应被隐藏且对话历史消失（OpenCode Go）
**状态**: OPEN | **评论**: 4 | **创建**: 2026-08-25

通过 OpenCode Go 订阅使用 `muse-spark-1.2-contributor` 时，运行可能无任何响应或错误显示即结束，有时则无限期保持 active。HTTP 流实际已完成且包含内容，但 UI 未能正确呈现。属于较为严重的 UI 状态同步问题。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/44958)

---

### 7. #45456 [2.0] Web UI 会话停滞数小时，无诊断信息，无限重试
**状态**: CLOSED | **评论**: 2 | **创建**: 2026-08-27

长时间运行的 Web UI 会话可能因上游 `invalid_request_error` 而**卡住数小时**，每次请求都失败且无有效诊断信息，缺乏可靠的恢复路径。该问题今日报出即被关闭，但其模式（上游错误导致会话"假死"）值得关注。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/45456)

---

### 8. #33887 v1.17.10 在 WSL 上回归：TUI 黑屏无法输入
**状态**: CLOSED | **评论**: 6

升级到 v1.17.10 后在 WSL 中启动 opencode，TUI 黑屏、无法键入任何 prompt。降级到 v1.17.9 立即恢复。虽今日已关闭，但版本回归问题持续是社区关注重点。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/33887)

---

### 9. #34113 GLM-5.2 会话因模型尝试查看截图而中断
**状态**: CLOSED | **评论**: 4 | **👍**: 3

GLM-5.2 不支持图像输入，但 Agent 通过技能触发了图像输入，导致会话中断。虽然报错本身合理，但暴露了 **Agent 技能触发与模型能力边界之间缺乏协调**的问题。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/34113)

---

### 10. #34146 macOS 内核 NFS 消息泄漏进 TUI 并破坏显示
**状态**: CLOSED | **评论**: 4

在 macOS 上使用 OrbStack（挂载 NFS 共享）时，即使 opencode 完全空闲，内核 NFS 状态消息也会渗入 TUI 显示。此类**外部噪音污染 TUI 渲染**的问题说明 TUI 对 stdin 之外的输入源缺乏隔离。

🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/34146)

---

## 重要 PR 进展

### 1. #45482 fix(task): 让异步 subagent 任务诚实、依次、一次性回答并停止
**状态**: OPEN

修复异步 subagent 任务在父会话中的通知机制：当子 agent 有未完成的异步子任务时，运行时在全部完成后给出一次确认，且该确认是尾部 request-only 消息，避免子 agent 不断回复。**依赖 #43510**。这是对今日多个 subagent 循环报告的直接回应。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45482)

---

### 2. #45481 [contributor] feat(core): 以实时能力打开持久会话
**状态**: OPEN | **作者**: kitlangton

当前持久会话 runner 嵌入时只能使用目录中发现的模型/工具/指令配置。本 PR 允许宿主直接提供可执行工具和模型，避免重启会话在不相关的目录能力下恢复。对嵌入式场景和会话恢复的正确性有重要意义。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45481)

---

### 3. #45453 feat(plugin): 允许在工具查找前修复工具调用
**状态**: CLOSED

让插件能在工具查找前修改顶层模型调用（如 `event.tool === "reead"` 改为 `"read"`），使 `event.tool` 可变并在解析前运行 hook。增强了插件的容错能力。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45453)

---

### 4. #45485 [contributor] fix(provider): 更新 Mistral SDK 以支持流式工具调用
**状态**: OPEN

将 `@ai-sdk/mistral` 从 `3.0.51` 升级到 `3.0.59`，新版 adapter 支持累积流式工具调用参数并在连续片段间复用 ID，不再要求每个 chunk 都包含完整工具调用。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45485)

---

### 5. #45474 fix(app): 在分组更新时保留工具展开状态
**状态**: CLOSED

按稳定 row key 构造 assistant 内容，而非在响应式 JSX 表达式中调用渲染器。此前添加分组引用会重跑构造函数并重挂载嵌套工具，导致本地展开状态被重置。三行修复解决一个 UI 状态丢失问题。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45474)

---

### 6. #45476 fix(core): 将插件环境变量应用到 v2 bash
**状态**: OPEN | **Closes #41117**

v2 Bash 通过 Core 运行时未调用现有的 `shell.env` 插件 hook，导致插件提供的环境变量未生效。本 PR 补齐了这一缺口。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45476)

---

### 7. #45472 fix(websearch): 移除提供商白名单
**状态**: OPEN | **Closes #44307**

`websearch` 是客户端工具，依赖公共 Exa/Parallel MCP 端点，不应受提供商白名单限制。本 PR 默认对所有提供商启用 websearch。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45472)

---

### 8. #45475 fix(core): 在压缩（compaction）期间保留对话 agent
**状态**: OPEN

压缩时使用最后一条 assistant 消息的 agent（包括跨早期 checkpoint），保留正常 system prompt、工具定义和上下文 hooks，并将摘要指令追加到请求准备之后。修复压缩过程中 agent 丢失或错乱的问题。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45475)

---

### 9. #45461 feat(core): 暴露后台 shell 输出路径
**状态**: CLOSED

在后台 shell 响应中包含 shell ID 和实时输出文件路径，支持在任务完成前读取中间输出，同时保留自动完成提示。覆盖显式和用户触发的后台化路径。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45461)

---

### 10. #45450 [contributor] fix(core): 会话迁移后刷新 Console 模型
**状态**: OPEN | **作者**: kitlangton

当 Session 迁移到旧的缓存 Location 时，模型可能不可用。Console 插件在激活或账户切换时捕获了库存快照，但普通 Catalog 重载会重放旧快照。本 PR 修复了这一恢复路径问题。

🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/45450)

---

## 功能需求趋势

| 趋势方向 | 代表 Issue/PR | 说明 |
|---------|--------------|------|
| **Agent 循环检测与终止机制** | #45442, #43603, #43673, #43800, #45482 | 连续多个独立报告指向同一痛点：Agent 在遇到文件缺失或无法解析时陷入死循环，重复相同工具调用。这是当前 2.0 最紧迫的功能缺口 |
| **会话内存泄漏治理** | #20695, #33213, #34226 | 长时间运行的内存累积问题持续是社区头号关切，用户希望官方能系统性解决而非零散打补丁 |
| **会话恢复与状态一致性** | #44958, #45456, #45450, #45481 | 会话中途卡死、恢复后上下文丢失或模型不可用等问题频繁出现，用户对会话状态管理的可靠性要求提高 |
| **移动端/远程控制能力** | #45437 | 有用户提出参考 Claude Code 的 `rc` 模式，通过 QR 码配对手机进行远程控制，属新功能探索 |
| **IDE 体验完善** | #34232, #34262 | IDE 扩展缺乏会话管理 UI、文档描述不清等问题仍然存在，桌面端功能与 TUI 差距明显 |
| **工具调用容错与插件能力** | #45453, #45476, #45472 | 插件生态的功能扩展方向：更灵活的 hook 时机、环境变量透传、工具可用性简化配置 |

---

## 开发者关注点

- **循环检测机制缺失已成为最突出痛点**：5 个独立 Issue 描述了 Agent 陷入无进展循环的现象，用户不得不手动中断避免 token 烧毁。社区期望 OpenCode 具备类似"连续 N 次相同调用无新信息即停止"的内建保护。

- **"用 LLM 修 bug"引发反感**：Memory Megathread 中维护者明确要求用户不要用 LLM 生成解决方案（"PLEASE DO NOT RUN YOUR LLM AND SUGGEST SOLUTIONS IT IS ALWAYS WRONG"），说明 AI 生成的错误建议已对问题排查形成干扰。

- **subagent 并行场景性能退化**：多个 subagent 并发时 TUI 渲染线程 CPU 占用飙高（97%），输入延迟明显。开发者对 subagent 功能本身有需求，但其性能支撑尚不达标。

- **版本回归频发**：v1.17.10 在 WSL 上黑屏、Bun 1.3.14 在特定 CPU 上崩溃等回归问题频繁出现，开发者对升级的谨慎程度在上升。

- **测试基建改进获得持续投入**：kitlangton 连续提交了 5 个测试重构 PR（#45467-#45471），将临时目录、HTTP fixtures、session 消息断言等统一到生命周期感知的模式中，显示核心团队在强化测试可靠性方面有明显投入。

- **Web UI 稳定性亟待提升**：#44958（响应隐藏）和 #45456（无限重试）均指向 Web UI 在异常路径下缺乏有效的状态呈现与恢复策略，与 TUI 相比稳定性差距明显。

---

*本日报基于 GitHub 公开数据自动生成，数据截至 2026-08-27 24:00 UTC。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-27

## 今日速览

今日社区焦点集中在**性能修复**与**多项关键 Bug 修复**上：O(n²) 推理详情累积导致的事件循环冻结已获修复（#8648/#8711），代理环境下 `HttpsProxyAgent is not a constructor` 的回归问题（#8610）及扩展加载失败问题（#8620）有待解决。PR 方面，**GLM-5.3 Flash 模型支持**（#8690）和 **Z.AI 强制思考模型修复**（#8707）已合入，同时**NVIDIA InferenceHub 正式成为内置 Provider**（#8664）。


## 社区热点 Issues

1. **[#6879] auto-compaction never triggers after context grows past 100% until provider overflow**
   作者：alexanderkreidich | 评论 24 | 👍 19 | [链接](https://github.com/earendil-works/pi/issues/6879)
   一个长达 2 小时以上的 agentic 回合中，上下文窗口超限到达 373k tokens 时 API 才拒绝请求，自动压缩始终未触发。该问题已标记 `inprogress`，获得社区高度关注，可能是内存/成本优化的关键卡点。

2. **[#8029] Very slow performance on moving in prompt editor**
   作者：affanali2k3 | 评论 9 | [链接](https://github.com/earendil-works/pi/issues/8029)
   当 prompt 输入框中有大文本（约 7000 行）时，单次方向键操作耗时高达 1650ms。输入框性能线性退化问题直接影响用户日常体验，已标记 `inprogress`。

3. **[#8610] Regression in v0.84.3: 'Error: HttpsProxyAgent is not a constructor' when calling google-vertex with proxy**
   作者：whw23 | 评论 4 | [链接](https://github.com/earendil-works/pi/issues/8610)
   v0.84.3 中设置 HTTP 代理环境变量后请求 Google Vertex 立即报错。推测与 code splitting 导致的依赖加载顺序有关，属于 0.84.3 回归问题。

4. **[#8620] 0.84.3 bundled CLI: every global extension fails with "Cannot find module '@earendil-works/pi-coding-agent'"**
   作者：orchidautomation | 评论 4 | [链接](https://github.com/earendil-works/pi/issues/8620)
   升级到 0.84.3 后，`~/.pi/agent/extensions/` 下所有扩展模块无法加载，报 `Cannot find module` 错误。属于打包路径或依赖解析的回归问题，影响所有使用全局扩展的用户。

5. **[#8053] Parallel tool batches lose already-completed tool results when one sibling stalls**
   作者：Cyberceratops | 评论 4 | [链接](https://github.com/earendil-works/pi/issues/7053)
   并行工具调用中，若某个工具卡住，已完成的工具结果会丢失（`Promise.all` 等待整个批次完成才持久化 `toolResult`），导致出现 "No result provided" 错误。

6. **[#7724] Cold restore replays an overflow assistant removed by live recovery**
   作者：acmerfight | 评论 4 | [链接](https://github.com/earendil-works/pi/issues/7724)
   上下文溢出经压缩和重试处理后，重新打开会话时，失败的 assistant 响应会重新出现在模型历史中，导致恢复后的对话包含错误消息。

7. **[#8711] TUI pegs 100% CPU and freezes while streaming OpenRouter thinking (GLM-5.3-flash)**
   作者：hermitokatt | 评论 1 | [链接](https://github.com/earendil-works/pi/issues/8711)
   与 #8648 同源：`reasoning_details` 流式累积导致 O(n²) 复杂度，本地 CPU 飙升至 100% 并完全冻结 UI。搭配 #8671 修复一并解决。

8. **[#8688] [Windows] powershell tool: stray . prepended to every command breaks the first word**
   作者：shoucandanghehe | 评论 3 | [链接](https://github.com/earendil-works/pi/issues/8688)
   Windows 下 powershell 工具给每条命令前添加 UTF-8 编码前缀时多出一个 `.`，直接粘连到命令首词导致解析错误（已关闭，修复随 #8582 处理）。

9. **[#8675] TUI renders text one word per line instead of wrapping across available width**
   作者：kiszu | 评论 2 | 👍 1 | [链接](https://github.com/earendil-works/pi/issues/8675)
   0.84.3 在 WSL2/Windows Terminal 下，长文本逐词换行而非流式换行，影响核心阅读体验。与 #8673 同属 markdown 软换行渲染问题。

10. **[#8705] Unhandled rejection in agentLoop / agentLoopContinue leaves EventStream hanging**
    作者：phh235 | 评论 2 | [链接](https://github.com/earendil-works/pi/issues/8705)
    `runAgentLoop` 的 Promise rejection 未被捕获，导致 EventStream 挂起，前端界面无响应。修复 PR #8704 已合入。

11. **[#8706] zai thinking handler sends disabled for forced-thinking models (glm-5.3/5.3-flash)**
    作者：water-boom | 评论 2 | [链接](https://github.com/earendil-works/pi/issues/8706)
    将思考级别设为 off 时，Z.AI 强制思考模型仍收到 `thinking: { type: "disabled" }`，导致推理内容泄漏到输出中。修复 PR #8707 已完成。

12. **[#8673] TUI: soft line breaks render as hard breaks — thinking blocks show as ragged sequential lines**
    作者：manojbajaj95 | 评论 2 | 👍 1 | [链接](https://github.com/earendil-works/pi/issues/8673)
    `marked` 将 CommonMark 软换行转为硬换行，使推理过程一行一词地散落显示。修复 PR #8674 已合入。


## 重要 PR 进展

1. **[#8708] fix(coding-agent): resolve fd/rg release versions without the GitHub API**
   作者：Terminator666666 | [链接](https://github.com/earendil-works/pi/pull/8708)
   解决 GitHub API 匿名配额（60 次/小时/IP）限制。在共享出口 IP 环境下，pi 下载 fd/ripgrep 时不再依赖 `api.github.com` 的 releases/latest 接口，改为更稳的方式解析版本。

2. **[#8707] fix(ai): keep zai thinking enabled for forced-thinking models (off === null)**
   作者：water-boom | [链接](https://github.com/earendil-works/pi/pull/8707)
   修复 Z.AI 强制思考模型（GLM-5.3 系列）在 thinking off 时泄漏推理内容的问题：当 `thinkingLevelMap.off === null` 时保持 thinking 启用。

3. **[#8704] fix(agent): end event stream on unhandled loop rejection**
   作者：phh235 | [链接](https://github.com/earendil-works/pi/pull/8704)
   为 `agentLoop` / `agentLoopContinue` 添加 rejection 捕获，确保 EventStream 正常结束而非挂起（修复 #8705）。

4. **[#8690] feat(ai): add GLM-5.3 Flash to Z.AI catalogs**
   作者：NetVar1337 | [链接](https://github.com/earendil-works/pi/pull/8690)
   为 Z.AI Coding Plan 目录新增 GLM-5.3 Flash：100 万 token 上下文窗口、131,072 token 输出限制，保持 OpenAI Completions 端点兼容（含图片/文本输入）。

5. **[#8699] fix(tui): remove coding-agent config reads from pi-tui**
   作者：geraschenko | [链接](https://github.com/earendil-works/pi/pull/8699)
   修复 pi-tui 重复读取 pi-coding-agent 配置的问题（修复 #8698）。删除 `PI_CODING_AGENT_DIR` 回退逻辑，统一由 coding agent 自身解析注入。

6. **[#8678] feat(tui): edit selected prompt text**
   作者：Panoplos | [链接](https://github.com/earendil-works/pi/pull/8678)
   此前鼠标拖选文本仅支持复制，无法编辑。此 PR 让聚焦的编辑器接收已完成的鼠标选区，使 Backspace 等操作可作用于选区。

7. **[#8671] fix(ai): serialize thinking signature once**
   作者：cristinaponcela | [链接](https://github.com/earendil-works/pi/pull/8671)
   修复 #8648 的 O(n²) 问题：流式 `reasoning_details` 时改为内存累积一次序列化，而不是每 chunk 重新解析/验证/序列化整个 `thinkingSignature`。

8. **[#8674] fix(tui): render markdown soft line breaks as spaces, not hard breaks**
   作者：manojbajaj95 | [链接](https://github.com/earendil-works/pi/pull/8674)
   修复 #8673：将 CommonMark 软换行（`\n`）渲染为空格而非硬换行，使思考块和 markdown 段落流畅换行显示。

9. **[#8676] fix(tui): make alt screen not segment on - and /**
   作者：cristinaponcela | [链接](https://github.com/earendil-works/pi/pull/8676)
   修复 #7746：全屏双击选择不再按 `/` 和 `-` 分割路径/kebab-case，而是拼接相邻词段，与其他终端行为保持一致。

10. **[#8664] feat(ai): promote NVIDIA InferenceHub to a built-in provider**
    作者：sixuerain | [链接](https://github.com/earendil-works/pi/pull/8664)
    NVIDIA InferenceHub 升级为 `@earendil-works/pi-ai` 内建 Provider，统一认证 Claude/GPT/Gemini/DeepSeek/Llama 及 NVIDIA 托管模型。

11. **[#8669] fix(tui): autocomplete orders nested results**
    作者：cristinaponcela | [链接](https://github.com/earendil-works/pi/pull/8669)
    修复 #8000：autocomplete 不再被深层 `venv/site-packages` 路径刷屏，改为优先排序直接子路径匹配结果。

12. **[#8696] fix(tui): handle Apple Terminal meta arrows**
    作者：evanqhuang | [链接](https://github.com/earendil-works/pi/pull/8696)
    支持 Terminal.app 的 Option+方向键序列（`ESC ESC [ A-D`）并缓冲两段 ESC 前缀，确保按键事件正确合并。


## 功能需求趋势

1. **稳定性与性能优化是压倒性主题**：从 O(n²) 流式推理累积（#8648）到大文本输入框线性退化（#8029），乃至上下文溢出压缩失败（#6879），社区最迫切的需求是**大规模使用场景下的稳定表现**。

2. **新模型快速适配**：GLM-5.3 Flash 加入 Z.AI 目录（#8690）、qwen3.8-flash 提需求（#8709）、DeepSeek V4 Pro 低推理模式（#8694）——用户持续期待 pi 对新模型/新能力的快速跟进。

3. **编辑器体验增强**：点击定位光标（#8701）、拖选编辑（#8678）、软换行渲染（#8674）、路径双击选择（#8676）——旨在让 TUI 编辑体验对齐 GUI 编辑器常规预期。

4. **扩展系统稳定性**：全局扩展加载失败（#8620）与扩展终止 agent run 能力（#7824）表明社区严重依赖扩展生态，期望更可靠的扩展运行时和更丰富的扩展 API。

5. **企业级/基础设施适配**：代理环境兼容（#8610）、GitHub API 限流规避（#8708）和 NVIDIA 推理网关内置（#8664）表明 pi 正进入更多组织化使用场景。


## 开发者关注点

- **配置同步开销**（#6415）：多个设备间同步 git 配置时，`lastChangelogVersion` 字段造成不必要的冲突，建议移至运行时文件。
- **会话切换性能**（#8710）：`/resume` 为支持搜索而全量解析所有会话文件，但日常使用只需要快速切换最近会话，希望列表阶段仅读取文件头部。
- **交互式启动体验**（#8689）：资源初始化期间用户已可输入，应在运行时初始化完成前就显示可编辑的临时 composer，避免等待后输入。
- **系统提示词定制**（#8391）：默认系统提示词的修改与插件扩展之间的兼容性难以兼顾，社区希望有更可靠的定制方式，目前三种做法均存在缺陷。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-27

## 今日速览

今日 Qwen Code 发布 v0.22.2 正式版及 desktop-v0.2.2，核心变更包括将持久化 Node REPL 重构为独立 MCP 服务器（Breaking Change），以及目标续写提示词的三路收敛修复。社区方面，Agent Team 生命周期并发安全的系列审计 Issue（#10074 等 5 个拆分项）持续发酵，同时两条 P1 安全漏洞（MCP 权限别名混淆 #10199、Bash 环境变量绕过 #10197）值得关注。

## 版本发布

**v0.22.2** — [Release 页面](https://github.com/QwenLM/qwen-code/releases)

- **Breaking Change**：`refactor(node-repl)!` — 持久化 Node REPL 以独立 MCP 服务器形式交付（[#9499](https://github.com/QwenLM/qwen-code/pull/9499)），由 @LaZzyMan 贡献
- **Feature**：`fix(goal)` 将三个续写提示词收敛到一个受保护的契约上（[#9834](https://github.com/QwenLM/qwen-code/pull/9834)）
- **Feature**：`feat(core)` 要求显式用户确认（部分内容被截断）

**桌面端 desktop-v0.2.2** — 同步包含上述 #9834 与核心层修复。

**cua-driver-rs v0.20.1** — Qwen CUA Driver 预编译二进制发布，macOS 提供签名并公证的通用二进制，Linux/Windows 提供 x86_64 + arm64 构建。

---

## 社区热点 Issues（Top 10）

### 1. MCP 权限别名混淆可授权异服务器工具 ⚠️ P1 安全
[#10199](https://github.com/QwenLM/qwen-code/issues/10199) — 作者：SLP-DEV1 | 评论：2 | 更新：08-26

**摘要**：MCP 权限匹配会将不同的 server/tool 身份折叠到同一丢失信息的 legacy/规范化名称上，导致某 MCP 服务器的 `allow` 规则可能匹配到另一台服务器的工具。视为兼容层回归。

**关注理由**：跨服务器权限越权属于严重安全模型缺陷，直接影响企业级多 MCP 接入场景的可信边界。

### 2. Bash 环境变量赋值可绕过具体 allow 规则 ⚠️ P1 安全
[#10197](https://github.com/QwenLM/qwen-code/issues/10197) — 作者：SLP-DEV1 | 评论：2 | 更新：08-26

**摘要**：保存的具体 `Bash(...)` allow 规则在 Qwen 剥离前导环境变量赋值后仍可被匹配——即使这些赋值改变了被允许程序的运行时语义并导致额外代码执行。无需命令替换、反引号或 `$()`。

**关注理由**：与 #10199 同属权限绕过类漏洞，`status/ready-for-human` 标记说明已进入人工修复队列，是今日最需要关注的攻击面修复。

### 3. Agent Team 生命周期审计：五个竞态与清理风险
[#10074](https://github.com/QwenLM/qwen-code/issues/10074) — 作者：netbrah | 评论：3 | 创建/更新：08-26

**摘要**：静态审查发现 Agent Team 生命周期实现存在 5 种可能违反外部可见生命周期不变量的交错或失败路径，包括：并发创建者回收同名的竞态（#10209）、并发 spawn 持久化 ghost 成员（#10208）、任务重复派发（#10207）、事件桥接前结果丢失（#10211）、文件系统清理失败仍报成功（#10210）。

**关注理由**：这是今日社区最集中的 Bug 簇——一个审计拆出 5 个独立 Issue + 2 个相关已关闭 Issue（#10072），反映多智能体协作可靠性的系统性问题，全部标记 `welcome-pr`。

### 4. permissions.allow 语义变更：0.22.1 起未覆盖工具直接禁用
[#10218](https://github.com/QwenLM/qwen-code/issues/10218) — 作者：pandazhangS | 评论：4 | 更新：08-27

**摘要**：0.21.1 及之前 `permissions.allow` 是自动批准列表（白名单外工具走正常询问流程）；0.22.1 起变为注册表白名单——只要有一条有效规则，未覆盖工具直接在注册表层面禁用且无询问，需重启才重新评估。文档未说明此变更。

**关注理由**：4 条评论为今日新增，是典型的 breaking-change 未记录引发的用户困惑，且对应修复 PR #10098 正在进行中，属于高频配置痛点。

### 5. 自定义模型供应商无法对话（Moonshot JSON Schema 校验失败）
[#10227](https://github.com/QwenLM/qwen-code/issues/10227) — 作者：ru1yex | 评论：4 | 更新：08-27

**摘要**：配置自定义 Moonshot 供应商时请求报错：`tools.function.parameters is not a valid moonshot flavored json schema, details: properties must be an object`。

**关注理由**：第三方模型供应商兼容性是工具链落地的关键路径，该报错信息对用户不友好（未指出具体哪个参数非法），4 条评论说明有多人遇到。

### 6. Web UI：MCP 加载后无法进行对话
[#10228](https://github.com/QwenLM/qwen-code/issues/10228) — 作者：Ghpt6 | 评论：2 | 更新：08-27

**摘要**：`qwen serve --token xxx` 启动后，手动点击左侧插件导航栏加载 MCP 后，Web UI 页面输入框不可选中、对话按钮失效。

**关注理由**：Web Shell 是 serve 模式的核心交互界面，MCP 加载导致整个会话不可用属于高影响功能性回归。

### 7. E2E 测试：GitHub-hosted runner 间歇性无法访问阿里云端点
[#10242](https://github.com/QwenLM/qwen-code/issues/10242) — 作者：yiliang114 | 评论：3 | 更新：08-27

**摘要**：合并后 main 分支的 E2E 测试间歇性失败，原因是 GitHub-hosted runner 无法稳定访问 `OPENAI_BASE_URL` 对应的 Aliyun Beijing 端点。重跑即通过，确认是网络可达性问题而非代码回归。

**关注理由**：CI 基础设施稳定性直接影响开发效率，与 PR #10085（迁移至持久化 ECS 池）和 #10229（自动重试）构成完整的修复链。

### 8. 运行时新增模型需重启 daemon 才能设为当前模型
[#10184](https://github.com/QwenLM/qwen-code/issues/10184) — 作者：yiliang114 | 评论：2 | 更新：08-27

**摘要**：daemon 模式下，Web Shell 设置页通过 "+ Add model" 添加的新模型立即可见，但点击 "Set as current" 报 `Invalid params: Unknown model`，需重启 daemon 才能生效。

**关注理由**：模型动态切换是 serve 模式的核心工作流，该 Bug 打断"热添加-热切换"的预期体验。

### 9. qwen3.8-flash 被判定为纯文本模型，媒体输入被静默降级
[#10194](https://github.com/QwenLM/qwen-code/issues/10194) — 作者：efwds | 评论：3 | 更新：08-26

**摘要**：客户端模态自动检测将 `qwen3.8-flash` 分类为 text-only，尽管 ModelStudio 端点接受 image 和 video 输入。实际效果：`read_file` 读取图片/PDF 时被静默路由到视觉模型而非作为像素传给 qwen3.8-flash。

**关注理由**：模型模态元数据缺失导致功能静默降级——用户以为多模态在工作，实际并未触发。此类"无报错但行为错误"最消耗排障时间。

### 10. 会话分支 + Git worktree 隔离（feature request）
[#8271](https://github.com/QwenLM/qwen-code/issues/8271) — 作者：water-in-stone | 评论：2 | 更新：08-27

**摘要**：请求实现完整的会话分支功能——用户可从任意会话的最新状态或任意已完成的 Assistant 响应分支出新会话，并可选 Git worktree 隔离实验。

**关注理由**：长期开放的老 Issue（08-01 创建）持续获得更新，对应 `roadmap/session-management` 路线图，是社区对探索式工作流的核心诉求。

---

## 重要 PR 进展（Top 10）

### 1. 解耦 permissions.allow 与工具注册
[#10098](https://github.com/QwenLM/qwen-code/pull/10098) — 作者：yiliang114 | 更新：08-27 | 状态：OPEN

**内容**：将 `permissions.allow`（和 `permissions.ask`）恢复为纯自动批准语义，不再移除、降级或隐藏工具；新增 `tools.eager` 设置承担注册表白名单职责。对应修复 Issue #10218 的语义变更问题。

**重要性**：直接回应社区对 0.22.1 权限语义突变的质疑，是今日配置系统方向最核心的 PR。

### 2. 修复 telemetrySwap 测试因 Config double 缺 getToolRegistry 而失败
[#10243](https://github.com/QwenLM/qwen-code/pull/10243) — 作者：AaronZ345 | 创建/更新：08-27 | 状态：OPEN

**内容**：移除 `client.telemetrySwap.test.ts` 最小 Config double 中重复的 `getToolRegistry` 属性，保留完整文档化 stub，使恢复会话初始化可正常调用 `restoreLoadedSkillsFromHistory`。

**重要性**：修复 #10205 报告的 main 分支 9/10 测试失败——该红测试已阻塞所有含最新 main 的 PR 合并。

### 3. Agent Team 过期回收的代数安全修复
[#10236](https://github.com/QwenLM/qwen-code/pull/10236) — 作者：yiliang114 | 创建/更新：08-27 | 状态：OPEN

**内容**：修复 `tryReclaimStaleTeam()` 将过期判断（`readTeamFile()` + leadPid 存活检查）与实际清理（`deleteTeamDirs()`）分离的问题，消除延迟回收决策可能删除新一代存活团队的竞态（对应 #10209）。

**重要性**：Agent Team 并发安全系列的首个修复 PR，为后续 4 个拆分项提供修复范式。

### 4. E2E Linux 分片迁移至持久化 ECS 池
[#10085](https://github.com/QwenLM/qwen-code/pull/10085) — 作者：wenshao | 更新：08-27 | 状态：OPEN

**内容**：将 `e2e-test-linux` workflow 路由到持久化 `ecs-qwen` 池，带标准 hosted fallback（仓库守卫 + `MAINTAINER_ECS_RUNNER_DISABLED` 开关）。

**重要性**：针对 #10242 的网络可达性问题的基础设施级修复，属 autofix/takeover 标记。

### 5. CI：限制 E2E 通道数并自动重试一次 main 的瞬时失败
[#10229](https://github.com/QwenLM/qwen-code/pull/10229) — 作者：yiliang114 | 创建/更新：08-27 | 状态：CLOSED

**内容**：为 main 分支的 E2E 增加自动重试，限流并减少并发通道数。附有对近期失败（#10224、#10186、#10242）的二分分析，证明均为网络问题而非代码回归。

**重要性**：虽已关闭（可能已合并），但展示了社区对 CI 稳定性的快速反应闭环。

### 6. 在 headless 和 ACP 主机中为工具结果打 Goal 时间戳
[#10175](https://github.com/QwenLM/qwen-code/pull/10175) — 作者：qqqys | 更新：08-27 | 状态：OPEN

**内容**：在 headless 和 ACP 主机中用 Goal turn permit 记录工具结果，使其可作为证据。规则提取为导出的辅助函数 `goalToolResultProvenance`，交互式调度器也切换使用同一实现。

**重要性**：统一 Goal 证据链在各主机端的一致性，是 Goal 系统完整性的关键补全。

### 7. Artifacts：内容变更时刷新 updatedAt
[#9929](https://github.com/QwenLM/qwen-code/pull/9929) — 作者：zjgzx1988 | 更新：08-27 | 状态：OPEN

**内容**：会话 artifact 内容变更时，`updatedAt` 随之更新。工作区文件编辑在 list/get 时触发 updatedAt 更新并暴露实时 `sizeBytes`，注册时的指纹保留在元数据中作为对比基线。

**重要性**：元数据一致性修复——解决 artifact 内容已变但时间戳未更新的问题，对依赖时间戳做增量同步的工具链有意义。

### 8. Review 多轮回复归入原线程并解决已修复项
[#9940](https://github.com/QwenLM/qwen-code/pull/9940) — 作者：wenshao | 更新：08-27 | 状态：OPEN

**内容**：多轮 review 中仍成立的 finding 以回复形式落到原线程而非开新 inline 评论；判定已修复的 finding 回合反馈回 PR，线程收到解决标记。属 autofix/takeover + review/self-reported。

**重要性**：PR 审查体验的实质性改进——减少噪音评论、保持讨论上下文连续，是代码审查工具链的高频需求。

### 9. 为 Tauri shell 恢复品牌构建技能
[#10164](https://github.com/QwenLM/qwen-code/pull/10164) — 作者：yiliang114 | 更新：08-27 | 状态：OPEN

**内容**：在 `packages/desktop-shell/.agents/skills/desktop-brand-builder/` 恢复桌面品牌构建技能，替代 #9085 中随 Electron 包一并移除的旧技能，保持原契约（品牌化桌面应用构建）。

**重要性**：Electron 移除（#9085）后功能恢复的补位 PR，确保 Tauri 版桌面端能力不降级。

### 10. 恢复 review 中的守护拒绝在轮次报告中可见
[#10117](https://github.com/QwenLM/qwen-code/pull/10117) — 作者：wenshao | 更新：08-27 | 状态：OPEN

**内容**：修复 autofix 线程解析通道在 PR 上完全静默的问题——之前所有 fail-closed 守护仅以 run-log warning 形式记录拒绝原因，PR 上完全不可见（如 #9729 中 90 条 review 评论 0 条被解析）。现在各守护拒绝会在轮次报告中显式呈现，并等待 head 传播延迟。

**重要性**：提升 CI 自动化流程透明度，修复"静默跳过"导致的审查盲区，属 autofix/takeover 标记的自举修复。

---

## 功能需求趋势

从近 24 小时活跃的 Issues 与 PRs 中可提炼以下趋势：

1. **多智能体（Agent Team）可靠性成为焦点**：`roadmap/multi-agent` 标签下集中出现 5 个竞态/清理风险 Issue（#10207-#10211）+ 1 个总审计（#10074）——社区对多智能体生命周期的并发正确性提出了系统性要求，且普遍附带 `welcome-pr` 标签欢迎贡献。

2. **Web Shell / serve 模式体验优化**：多个 Issue 直指 Web UI 的可用性问题——MCP 加载后对话失效（#10228）、模型热添加不可用（#10184）、工具摘要折叠一致性（#10231）。`scope/web-shell` 已成为与 Core 并列的高频分类。

3. **权限系统语义透明化**：#10218（allow 语义回归）+ #10199（MCP 权限越权）+ #10197（Bash 绕过）三连发，社区对权限模型的安全性和文档同步提出了明确要求。

4. **外部模型供应商兼容性**：#10227（Moonshot schema 校验）+ #889（OpenAI Response API，持续 10 个月仍在活跃）——第三方供应商接入的报错可读性和 API 覆盖度是持续痛点。

5. **会话管理增强**：#8271（会话分支 + worktree 隔离）和 #8586（activeWork 跟踪与后台 Agent 恢复）均属 `roadmap/session-management`，代表探索式工作流对会话组织能力的需求升级。

---

## 开发者关注点

**高频痛点：**

1. **Breaking change 未提前文档化**：#10218 的 0.22.1 权限语义变更在 release notes 中无说明，导致用户升级后行为突变。开发者对"静默行为变更"的容忍度最低——建议在 release notes 的 Breaking Changes 区块中覆盖所有用户可见语义变化。

2. **安全边界的静默失效**：#10197 和 #10199 均属于"配置了安全规则但实际可被绕过"的类型，且无任何提示——开发者最怕的不是漏洞本身，而是"以为有保护实际没有"。

3. **错误信息可操作性不足**：#10227 的 Moonshot schema 校验报错未指明具体是哪个 parameter 非法；#10184 的 `Unknown model` 未提示需要重启 daemon。提升报错的可操作性（指出修复路径而非仅描述现象）是通用改进方向。

4. **多智能体团队的可观测性**：#10074 系列全部是"静态审查发现但未复现"的竞态问题——开发者对 Agent Team 的并发正确性信心不足，希望有更好的 trace 和 fault-injection 工具链支撑验证。

5. **CI 基础设施稳定性消耗注意力**：#10242 引发的讨论表明：GitHub-hosted runner 访问阿里云端点的网络问题已多次导致 main 变红，社区正通过基础设施迁移（#10085）和重试机制（#10229）双管齐下，但这仍占据了本周大量维护精力。

---

*日报生成时间：2026-08-27 · 数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-27

**数据来源**: github.com/Hmbown/DeepSeek-TUI（仓库已更名为 CodeWhale）

---

## 今日速览

今日社区焦点集中在 v0.9.12 版本的架构稳定性与多会话支持上：核心 PR #5638 修复了 runtime 存储所有者锁导致的多实例冲突问题（#5630），同时 #5631 新增了 OpenRouter qwen3.8-flash 模型支持。此外，社区对上下文压力警告的持久化显示（#5629 已合并）和监控基础设施（#5626）表现出持续兴趣，多个设计类 issue 也开始涌现。

---

## 社区热点 Issues（10 条）

### 1. 巨型文件拆分请求 — #5586
**标签**: [v0.9.12] [cleanup]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5586

**核心内容**: 用户要求拆分 v0.9.12 中的四个巨型文件：`lib.rs`（18.7k 行）、`config.rs`（12.3k）、`client.rs`（11.2k）、`runtime_threads.rs`（9.3k），声称这些文件持续造成维护困难。附带 20k 行的测试文件也需同步拆分。

**社区反应**: 5 条评论，作者为 Hmbown 本人，说明这是维护者主动发起的代码卫生讨论。反映了项目在快速迭代后对代码可维护性的关注。

---

### 2. 受监督操作的控制面 — #5533
**标签**: [enhancement]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5533

**核心内容**: 请求为每个会话添加控制套接字（消息/中断/重启/状态查询），并引入 `RuntimeBackendKind::External`，以支持外部监督场景（终端复用器包装、自动化框架、CI 系统等）。

**社区反应**: 4 条评论。这是面向企业级/自动化部署的重要功能需求，与 #5628 企业就绪 PR 相呼应。

---

### 3. 上下文压力警告不稳定（Bug）— #5620
**标签**: [bug] [medium]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5620

**核心内容**: 上下文压力警告是瞬态的，agent 不会主动响应它。该警告一出现就消失，无法作为一个有效的安全信号。严重性：中等级别（静默上下文退化，无崩溃）。

**社区反应**: 4 条评论。该 issue 推动了 #5629（持久化压力警告显示）和 #5623（压紧后输入 token 报告）两个 PR 的落地。表明社区对上下文管理的透明度有较高期望。

---

### 4. Windows 下 flags 拼接错误 — #4564
**标签**: [bug] [stale] [needs-info]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/4564

**核心内容**: Windows + npm 全局安装下，`--model` 和 `--toolsets` 会被当作单个拼接参数处理。仅 `codewhale exec --auto --max-steps N prompt` 形式可用。建议支持前置 flags 或 `CODEWHALE_MODEL` / `CODEWHALE_TOOLSETS` 环境变量。

**社区反应**: 3 条评论，issue 已标记 stale。Windows 用户长期存在的问题，说明跨平台兼容性仍是薄弱环节。

---

### 5. API 网络连接失败 — #4956
**标签**: [bug] [stale] [needs-info]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/4956

**核心内容**: WSL2 环境中无法连接 API 提供商。复现步骤：WSL2 安装 → 重启 shell → 启动配置。

**社区反应**: 3 条评论，标记 stale。网络层问题在 WSL2 环境下多发，可能涉及代理或 DNS 配置。

---

### 6. Xquik 未列入推荐 MCP 列表 — #5627（已关闭）
**标签**: [MCP] [recommendation]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5627

**核心内容**: Codewhale 可以通过通用命令连接 Xquik 的远程 MCP 服务器，但推荐列表未收录。`/mcp add recommended xquik` 返回该 ID 不存在。

**社区反应**: 2 条评论，issue 已关闭（大概率被 #5631 模型添加或 MCP 相关 PR 解决了）。反映了社区对 MCP 生态扩展的持续需求。

---

### 7. 斜杠指令响应迟缓 — #4568
**标签**: [bug] [stale] [needs-info]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/4568

**核心内容**: 中文用户反馈：新版输入 `/xxx` 斜杠指令后响应延迟明显，上一版本几乎是即时的，怀疑性能优化出现回退。

**社区反应**: 2 条评论，标记 stale。性能回退类问题需更多诊断信息，但也可能是感知层面的差异。

---

### 8. Runtime store 所有者锁阻塞多会话 — #5630
**标签**: [bug] [v0.9.12]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5630

**核心内容**: v0.9.12 集成版（commit `80f026e7c`）引入的机器级全局单所有者锁，导致同一台机器上第一个会话之后的每个 codewhale 进程都会硬失败。

**社区反应**: 1 条评论，但该 issue 已被 PR #5634 和 #5638 两个修复 PR 先后引用，说明此问题严重影响了多实例使用场景。今日已被 PR #5638 修复。

---

### 9. 非阻塞式"等待用户输入"窥探工具 — #5625
**标签**: [enhancement]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5625

**核心内容**: 建议添加一个轻量级的非阻塞工具，让 agent 在轮次中间感知是否有未决的用户输入，以支持人在环路的协作场景。

**社区反应**: 1 条评论。该提案尚处于反馈征集阶段，但方向与 #5533 监督控制面一致，是社区对 agent 可控性的持续追求。

---

### 10. MCP 密钥提供商作用域设计 — #5637
**标签**: [design] [MCP] [security]  
**链接**: https://github.com/Hmbown/CodeWhale/issues/5637

**核心内容**: 嵌入宿主可能将 MCP 凭据保存在钥匙串或宿主管理的密钥库中。通过运行时修改进程环境变量来提供这些值是不可靠的，因为其他线程可能读取环境变量，且密钥生命周期变成进程级。提议设计进程级回调方案。

**社区反应**: 0 条评论，今日新创建。这是安全架构层面的设计讨论，表明社区开始关注密钥管理的正确抽象。

---

## 重要 PR 进展（10 条）

### 1. 按会话范围化线程存储 — #5638
**链接**: https://github.com/Hmbown/CodeWhale/pull/5638

**核心内容**: 关闭 #5630。进程所有者锁保持独占，但默认存储根改为 `$CODEWHALE_HOME/sessions/<id>/runtime`，使同一台机器上可启动第二个 Codewhale。`CODEWHALE_RUNTIME_DIR` 仍可指定共享根目录。

---

### 2. 添加 OpenRouter qwen3.8-flash 模型 — #5631
**链接**: https://github.com/Hmbown/CodeWhale/pull/5631

**核心内容**: 将 OpenRouter `qwen/qwen3.8-flash` 纳入一等模型目录（1M 上下文、131K 输出、文本+图像+视频输入），并且是有定价的而非无定价条目。阿里第一方目录仍仅列 `qwen3.8-max`，本 PR 不发明 Token Plan flash ID。

---

### 3. 嵌入 tsnet 支持 web Tailscale — #5635
**链接**: https://github.com/Hmbown/CodeWhale/pull/5635

**核心内容**: 为 `codewhale web` 添加可选的 `--tailscale` 模式，默认仍为仅 loopback（127.0.0.1）。`--tailscale` 不带 `--web` 会被拒绝。

---

### 4. 按请求降级不兼容的 Moonshot 工具 — #5636
**链接**: https://github.com/Hmbown/CodeWhale/pull/5636

**核心内容**: Moonshot MFJS 兼容性失败按工具逐一降级，保留兼容工具，而非将整个请求判定失败。当无兼容工具时省略 `tools` 和 `tool_choice` 字段。

---

### 5. 统一 Worker 系统，退役 Keychain 产品路径 — #5632
**链接**: https://github.com/Hmbown/CodeWhale/pull/5632

**核心内容**: Fleet/子代理统一为一个 worker：`spawn(prompt)` 继承父级。角色只是标签而非权限矩阵。退役 Codewhale Keychain/OS-keyring 产品路径，`CODEWHALE_SECRET_BACKEND=system|keyring` 变为无操作。

---

### 6. 持久化上下文压力警告显示 — #5629（已合并）
**链接**: https://github.com/Hmbown/CodeWhale/pull/5629

**核心内容**: 解决 #5620 的显示层部分。warning/high/critical 压力级别不再消失在滚动元数据中，而是保持粘性状态栏可见，并定期刷新。

---

### 7. 每个线程使用量端点与会话成本持久化 — #5626
**链接**: https://github.com/Hmbown/CodeWhale/pull/5626

**核心内容**: 新增 `GET /v1/threads/{id}/usage` 端点，通过 `RuntimeThreadManager::aggregate_usage_for_thread` 适配器为 GUI 的会话成本界面提供提供商感知的、按记录时间定价的数据。该 PR 的更新日期为 8 月 27 日，属于非 Hmbown 的社区 PR，相当活跃。

---

### 8. 企业启动就绪：操作员指南包 — #5628
**链接**: https://github.com/Hmbown/CodeWhale/pull/5628

**核心内容**: 关闭 #5585、#5617。添加 `docs/ENTERPRISE.md`（含中文本）作为操作员/安全审查指南包，涵盖本地运行时、安全部署等主题。面向企业级部署场景。

---

### 9. 报告压缩后输入 token — #5623（已合并）
**链接**: https://github.com/Hmbown/CodeWhale/pull/5623

**核心内容**: 在 `CompactionCompleted` 事件中添加 `post_input_tokens` 字段，在共享完成事件发射器中一次性计算，复用引擎的规范化输入估计，使数值包含消息、系统上下文和累积压缩信息。

---

### 10. 支持 Kimi Code k3-256k — #5622（已合并）
**链接**: https://github.com/Hmbown/CodeWhale/pull/5622

**核心内容**: 将文档化的 `k3-256k` 模型添加到 Kimi Code 成员名单中，分配 262,144 token 上下文，并为四个已知的会员制模型省略通用 `temperature` 和 `top_p` 字段。

---

## 功能需求趋势

从今日 issue 和 PR 中可提炼出以下社区关注方向：

1. **多会话/多实例支持**（#5630、#5638、#5634）：v0.9.12 引入的单机单实例限制被社区迅速发现问题并提交修复，说明多实例并行使用是常见工作模式。

2. **受监督/自动化部署**（#5533、#5628）：外部进程控制 Codewhale 会话的能力（控制面、状态查询）是企业级采用的必要条件，相关设计讨论持续活跃。

3. **上下文管理与透明化**（#5620、#5625、#5629、#5623）：社区对 agent 上下文状态的感知和干预能力有强烈需求，包括压力警告持久化、压缩后 token 报告、非阻塞式用户输入探测等。

4. **新模型快速支持**（#5631、#5622、#5617）：qwen3.8-flash、k3-256k 等新模型的快速落地是社区关注的重点，同时要求价格信息准确。

5. **MCP 生态扩展与安全**（#5627、#5637、#5633）：MCP 服务器的推荐列表、密钥管理的安全抽象、工具按路由投影的统一设计，都在推动 Codewhale 走向更成熟的 agent 平台。

6. **开发者体验 / 代码卫生**（#5586、#4568）：巨型源文件拆分、命令响应性能是项目维护者与用户的共同关注点。

---

## 开发者关注点

- **大文件维护痛点**（#5586）：项目核心文件已膨胀至 1 万-2 万行级别，维护者 Hmbown 本人也承认这是持续的痛点，需要系统的重构计划。

- **Windows/WSL2 兼容性**（#4564、#4956）：跨平台问题持续存在，虽然未获最新修复，但用户仍在关注，部分标记为 stale 的 issue 暗示项目当前优先度不在此。

- **安全架构演进**（#5632、#5637）：Keychain 产品路径被退役，密钥管理向更简单的文件存储方案回归；同时 MCP 密钥提供商的正确抽象成为新的关注点，说明社区对安全边界的思考正在深化。

- **上下文管理透明度**（#5620、#5625）：用户希望 agent 不仅被动的接受上下文压缩，还能主动参与管理——感知压力、了解压缩后的 token 消耗、甚至主动请求用户输入。这是 agent 从"自动机"走向"协作者"的关键路径。

- **性能回退警惕**（#4568）：新版本在快速迭代中可能引入性能回退，社区对此保持高度敏感，维护者需要建立更完善的性能回归测试机制。

---

**总结**：v0.9.12 的 runtime 架构变动引发了一系列连锁修复与讨论（#5630/#5638），同时社区对新模型支持、上下文管理透明化、以及企业级部署能力的需求正在快速升温。建议关注 #5626 和 #5628 这两个非核心开发者的外部贡献，它们代表了社区从"用户"向"共同开发者"转化的积极信号。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*