# AI CLI 工具社区动态日报 2026-09-09

> 生成时间: 2026-09-09 09:31 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-09-09）

## 1. 生态全景

当前 AI CLI 工具已全面进入 **Agent 能力竞赛 + 稳定性补课** 的双轨阶段。主流工具均以平均每日 1-4 次版本迭代的频率快速演进（OpenAI Codex 单日发布 4 个 alpha、Gemini 单日 3 个版本），功能上从"代码补全/聊天"加速向"自主执行、多 Agent 协作、持久记忆、桌面/Web 多形态"演进。与此同时，Windows 平台兼容性、长会话恢复可靠性、MCP 生态的协议级联问题成为全行业通病——多个工具社区的热门 Issue 高度同质化，反映用户对"能跑通"的基本诉求仍未完全满足。模型接入层面，各工具正从"支持某家 API"转向"精细适配"（reasoning effort、会话 ID、tool call 兼容性），生态互操作开始产生连锁效应。

## 2. 各工具活跃度对比

> 注：Issue/PR 数为各摘要中主动跟踪/提及的数量，非仓库当日全量。Claude Code 与 DeepSeek TUI 因摘要生成失败，暂无数据。

| 工具 | 热点 Issues | 关键 PR（开放/合并） | Release 数 | 今日信号 |
|------|------------|---------------------|------------|---------|
| **OpenAI Codex** | 10（最高 51 评论） | ~20 个合并（bot 提交为主） | 4 个 alpha（rust-v0.154.0 系列） | 0.154.0 快速迭代，Windows/WSL 问题集中爆发 |
| **Gemini CLI** | 10（最高 13 评论） | 10（5 开放 / 5 关闭，多为合并） | 3（nightly / preview / stable） | Agent 中断误报、Shell 卡死等稳定性质疑 |
| **GitHub Copilot CLI** | 10（最高 11 评论） | 2 个实质 PR，1 个无效 PR | 2 个修复版（v1.0.84-2/3） | Vim 模式正式开放；Windows 会话管理成为众矢之的 |
| **Kimi Code CLI** | 3 | 2（1 合并 / 1 开放） | 0 | 登录 HTTP 500 阻断所有用户，属高危信号 |
| **OpenCode** | 10（最高 36 评论） | 10（多为开放中） | 1（v1.18.30） | 数据库膨胀 13GB+ 与 prompt 缓存缺失成最大槽点 |
| **Pi (pi-mono)** | 10（最高 10 评论） | 1（文档向） | 0 | OpenCode Go 新协议头导致多 provider 兼容性连锁故障 |
| **Qwen Code** | 10（最高 33 评论） | 10（含大功能 PR） | 4（stable + preview + 2 SDK） | TUI 渲染层迁移与 daemon 架构演进并行 |
| **Claude Code** | — | — | — | 数据缺失 |
| **DeepSeek TUI** | — | — | — | 数据缺失 |

**活跃度梯度**：`Gemini ≈ OpenCode ≈ Qwen ≈ Codex`（高频迭代 + 高讨论量） > `Copilot`（稳定但问题集中） > `Pi`（中低活跃、集成属性强） > `Kimi`（体量小、问题单一且紧急）。

## 3. 共同关注的功能方向

### 3.1 长会话 / 上下文可靠性（全行业第一痛点）
- **OpenCode**：event 表无限膨胀至 13GB+（#33356）；Agent 累积 51 张图片导致会话卡死（#47487）
- **Copilot**：恢复会话时 JS 堆 OOM（#4664）；stale item ID 导致所有 prompt 报 400（#4505）；FileWatch 死循环生成 13GB 日志（#4612）
- **Gemini**：Subagent 中断后误报 GOAL 成功（#22323）；上下文被中断回合污染（PR #29265）
- **Codex**：分页线程历史在 token_count 处停止投影（#40342）
- **Pi**：Esc 取消流式请求经常失效（#8823）

### 3.2 Windows 平台支持短板
- **Codex**：#41290（WSL 项目创建失败）、#25178（Computer Use 截图失败）、#29639（WSL 路径映射错误）
- **Copilot**：#4756 / #4742（Windows 无法创建第二个 Local 会话）、#3858（快捷键失效）
- **Qwen**：#11303（conhost.exe 泄漏 347 个子进程，占 2.8GB 内存）
- **Gemini**：Browser 子代理在 Wayland 环境失败（#21983，同为显示服务器类问题）

### 3.3 MCP 生态的"可靠、安全、可管理"
- **Copilot**：MCP 握手超时从 16s 缩短到 1s 导致静默不可用（#4753）、OAuth scope 参数缺失
- **Gemini**：MCP OAuth 强制执行 RFC 9207 issuer 标识（PR #29121）
- **Pi**：WebSocket 重试仅识别两种错误码，其他瞬时故障直接终止回合（#7444）
- **OpenCode**：OpenRouter 路由修饰符无法解析（PR #48117）

### 3.4 模型/Provider 适配的精细度
- **Copilot**：OpenRouter 集成诉求（#2943）
- **Pi**：OpenCode Go 新硬性要求 `x-opencode-session` 头导致多个 provider 请求失败（#9230/#9302/#9326）
- **OpenCode**：Bedrock 缓存输入重复计数触发自动压缩（#47296）；Zen 模型下拉框缺失（#43805）
- **Qwen**：本地 llama-server sampler 初始化失败（#10530）；GPT-5/6 reasoning effort 配置（PR #11295）

### 3.5 编辑器 / 终端 UX 体验补全
- **Copilot**：Vim 模式落地（#13）；Ctrl+Backspace 删除单词（#2199）
- **Qwen**：TUI 渲染层从 ink 迁移到 OpenTUI（#8662）
- **OpenCode**：会话时间线查找栏（PR #48088）
- **Kimi**：VS Code 中 `@` 优先显示已打开文件（#1270，已关闭）
- **Pi**：全屏模式滚动性能慢 3 倍（#9052）
- **Gemini**：符号链接的 agent 文件不被识别（#20079）

## 4. 差异化定位分析

| 工具 | 核心定位 | 技术路线 | 目标用户 | 独特卖点 | 当前短板 |
|------|---------|---------|---------|---------|---------|
| **OpenAI Codex** | OpenAI 生态的官方 Agent 入口 | Rust 核心 + 桌面应用 + Computer Use（GUI 自动化） | OpenAI 重度用户 / Pro 订阅者 | Computer Use 视觉操作、与 ChatGPT 生态深度绑定 | Windows/WSL 支持明显滞后；alpha 频繁但变更日志缺失 |
| **Gemini CLI** | Google 系全能 Agent 平台 | Node/TS + 子代理（subagent）+ Browser Agent + Auto Memory | Google 生态开发者、多 Agent 工作流用户 | 内置浏览器代理、自动记忆、技能系统 | Agent 稳定性问题集中（挂起、误报、卡死）；AST 感知仍在评估 |
| **GitHub Copilot CLI** | GitHub 工作流原生的轻量 CLI | Node.js + 桌面应用 + MCP 扩展 | GitHub 重度用户、IDE 开发者 | Vim 模式、GitHub 一站式体验、企业级身份体系 | 长会话稳定性"欠债"严重；Windows 体验滞后 |
| **Kimi Code** | 轻量级中文友好的 CLI 伴侣 | Node/TS + VS Code 扩展 | 中文开发者、Moonshot 模型用户 | 体积小、上手快、与 Kimi Web/App 联动 | 官方维护资源有限；登录链路存在高危未修复问题 |
| **OpenCode** | 模型无关的开源 Agent 运行时 | TypeScript + 多 Provider SDK（OpenAI/Azure/Bedrock/Ollama…）+ TUI/Desktop | 追求开放性与自定义的开发者 | Provider 中立、2.0 架构可扩展、桌面端持续重构 | 存储膨胀与缓存策略是系统性隐患；数据治理能力不足 |
| **Pi (pi-mono)** | 连接多 Agent 生态的"路由器" | 多 Provider 适配层 + TUI（基于 OpenCode 生态） | 使用 Pi 统一管理多种模型后端的开发者 | 轻量、统一入口、快速适配新模型/协议 | 依赖上游协议变更，易受 OpenCode/Codex 新要求冲击 |
| **Qwen Code** | 企业级全栈 Agent 工作台 | daemon 架构 + Web Shell（IDE 化）+ Mesh 多 Agent 协作 + 本地模型支持 | 企业团队、需要私有化/本地模型的中大型用户 | 支持本地 llama-server、Web Shell 功能密度高、持久化共享线程协作 | WebUI 退役带来 breaking change；local 模型兼容性波动 |
| **Claude Code** | Anthropic 官方 CLI Agent | 数据缺失 | Claude 用户 | 数据缺失 | 数据缺失 |

## 5. 社区热度与成熟度

- **最活跃（快速迭代期）**：**OpenAI Codex**（单日 4 个 alpha + 20 PR 合并）、**Gemini**（nightly/preview/stable 三线并进，PR 与 Issue 同步高活跃）、**OpenCode**（功能与 Bug 修复并重，桌面端重构规模大）、**Qwen**（daemon 架构 + Web Shell + Mesh 协作三线推进，功能密度极高）。这四家正处于**功能扩展快于稳定性沉淀**的阶段，Issue 数量与 PR 数量同步走高。

- **稳定迭代期**：**GitHub Copilot CLI** 版本节奏保守（两个修复版），Vim 模式等长线需求逐步落地，但社区对会话稳定性的信任危机正在积累（OOM、stale ID、FileWatch 失控等"开盲盒"式问题），属于**稳中有忧**。

- **低活跃 / 依赖型**：**Pi** 无独立版本发布，其活跃度本质是"OpenCode/Codex 生态变更的涟漪效应"；**Kimi** 体量最小，但登录 500 这类阻断性问题说明其服务端成熟度与主流工具存在代差。

- **成熟度判断**：论**生态完整度**，Gemini 与 Qwen 领先（Agent + Memory + 协作 + 多形态前端）；论**模型兼容性**，OpenCode 覆盖面最广

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
**数据源**: github.com/anthropics/skills | **截止**: 2026-09-09

---

## 1. 热门 Skills 排行（Top 8 PR）

> 说明：以下 PR 均处于 **Open** 状态，按社区评论活跃度排序。

1. **skill-creator 评估脚本修复**（#1298）
   - 功能：修复 `run_eval.py` 恒报 0% 召回率的核心 Bug，涉及 Windows 流读取、触发检测与并行 worker。
   - 热点：对应 Issue #556（12 条评论），10+ 用户独立复现，整个 description 优化循环一直在"用噪声做优化"。
   - 链接：https://github.com/anthropics/skills/pull/1298

2. **document-typography（文档排版质量控制）**（#514）
   - 功能：治理 AI 生成文档的孤儿词换行、寡行段落、编号错位等普遍排版问题。
   - 热点：直击 Claude 生成文档的"最后一公里"体验，社区讨论集中在 typographic 规则的可枚举性与执行边界。
   - 链接：https://github.com/anthropics/skills/pull/514

3. **scnet-hpc（HPC 集群运维）**（#1615）
   - 功能：通过 profile 化 SSH + Slurm 工作流操作 SCNet HPC 集群，覆盖分区、内存、模块、加速器等。
   - 热点：反映科研/超算场景用户对垂直领域 Skill 的需求。
   - 链接：https://github.com/anthropics/skills/pull/1615

4. **pdf Skill 大小写引用修复**（#538）
   - 功能：修复 `SKILL.md` 中 8 处大小写不匹配的文件引用（`REFERENCE.md` → `reference.md`）。
   - 热点：低风险高确定性修复，在大小写敏感文件系统（Linux/macOS）上直接决定 Skill 可用性。
   - 链接：https://github.com/anthropics/skills/pull/538

5. **ODT（OpenDocument）文档技能**（#486）
   - 功能：创建、填充、读取、转换 `.odt/.ods` 等 OpenDocument 格式，覆盖 LibreOffice/ISO 标准场景。
   - 热点：补全文档技能矩阵中除 docx/pdf 之外的开源格式空白。
   - 链接：https://github.com/anthropics/skills/pull/486

6. **frontend-design Skill 可操作性改进**（#210）
   - 功能：重写前端设计技能，确保每条指令可在单次对话内被执行，提升行为引导的精确度。
   - 热点：社区对"描述含糊的 Skill 无效"的典型回应——回归可执行性。
   - 链接：https://github.com/anthropics/skills/pull/210

7. **skill-quality-analyzer + skill-security-analyzer 元技能**（#83）
   - 功能：新增两个元技能，从结构/文档、安全、依赖等维度对 Claude Skills 做质量与安全审计。
   - 热点：与 Issue #492 的安全信任讨论形成共振，是"治理 Skills 的 Skill"方向代表。
   - 链接：https://github.com/anthropics/skills/pull/83

8. **docx 修订模式 w:id 冲突修复**（#541）
   - 功能：修复 DOCX 技能添加修订时硬编码低 ID 与已有书签/批注 ID 冲突导致的文档损坏。
   - 热点：OOXML 共享 ID 空间问题，根因分析清晰，属高价值稳定性修复。
   - 链接：https://github.com/anthropics/skills/pull/541

---

## 2. 社区需求趋势（来自 Issues）

| 方向 | 代表 Issue | 热度信号 |
|---|---|---|
| **安全与信任边界** | #492：社区 Skill 借 `anthropic/` 命名空间分发，构成信任边界滥用 | 43 评论，🔥最热 |
| **组织级共享与协作** | #228：希望在 Claude.ai 内直接共享 Skill，替代手动传文件 | 16 评论，8 👍 |
| **Skill 工具链可靠性** | #556：`run_eval.py` 全部查询 0% 触发率；#202：skill-creator 冗长低效 | 12 + 8 评论 |
| **质量/治理型元技能** | #412：agent-governance；#1385：推理质量门控管线；#1329：compact-memory 紧凑记忆 | 6 + 4 + 9 评论 |
| **上下文窗口效率** | #1487：`claude-api` 单次注入约 156k tokens，直接耗尽上下文 | 4 评论，严重度高 |
| **去重与安装体验** | #189：document-skills 与 example-skills 安装重复技能 | 6 评论，9 👍 |
| **平台扩展** | #29：AWS Bedrock 支持；#16：将 Skills 暴露为 MCP | 各 4 评论 |

**趋势总结**：需求正从"新增功能型 Skill"转向"**治理型元技能 + 工具链可靠性 + 组织级协作**"三层——社区最关心 Skill 本身是否安全、可评估、可共享，而非单纯堆数量。

---

## 3. 高潜力待合并 Skills（近期可能落地）

| PR | 内容 | 落地概率判断 |
|---|---|---|


---

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-09-09

## 1. 今日速览

过去 24 小时内，Codex 发布了 4 个 `rust-v0.154.0` 系列 alpha 版本，同时约 20 个 PR 被合并（主要由 copyberry[bot] 提交），集中在凭证代理（Credential Broker）重构和 Python SDK 发布流程加固。社区层面，Windows/WSL 环境下的项目创建失败（#41290）和 Computer Use 截图功能异常（#25178）成为热议焦点，凸显 Windows 平台稳定性仍是用户最关心的痛点。

## 2. 版本发布

过去 24 小时发布了 4 个 Rust 版 alpha 迭代：

- **rust-v0.154.0-alpha.11** — Release 0.154.0-alpha.11
- **rust-v0.154.0-alpha.10.2** — Release 0.154.0-alpha.10.2
- **rust-v0.154.0-alpha.8** — Release 0.154.0-alpha.8
- **rust-v0.154.0-alpha.7** — Release 0.154.0-alpha.7

从版本号密集程度来看，项目正为 0.154.0 稳定版进行快速迭代，但官方暂未提供详细变更日志。结合合并的 PR 推测，主要涉及凭证代理、Python SDK 发布流程、语音运行时打包修复等内容。

## 3. 社区热点 Issues

以下为过去 24 小时内评论数最高的 10 条 Issue，集中反映了当前用户的核心痛点：

### #41290 [Windows] 切换 Agent Environment 到 WSL 后项目创建和删除失败
- **评论 51 | 👍 37**
- ChatGPT Pro 用户反馈，在 Windows 上将 Agent 环境切换至 WSL 后，项目创建/删除功能完全不可用。这是当前社区热度最高的问题。
- https://github.com/openai/codex/issues/41290

### #25178 [Windows 10] Computer Use 截图功能在 SetIsBorderRequired 调用时失败
- **评论 50 | 👍 23**
- Windows 10 22H2 上，Computer Use 可以列出窗口、激活窗口、读取辅助功能文本，但任何调用 `get_window_state` 请求截图的操作都会以 `0x80004002` 失败。该问题已持续数月，影响大量 Windows 用户。
- https://github.com/openai/codex/issues/25178

### #21700 [Computer Use] Chrome 扩展在 Chrome Web Store 不可用，是否有离线安装包？
- **评论 29 | 👍 25**
- Codex Desktop 的 Chrome 集成扩展无法从 Chrome 网上应用店下载，页面显示错误。用户急需离线安装包或替代分发渠道。
- https://github.com/openai/codex/issues/21700

### #40342 [Bug] 分页线程历史投影在遇到 token_count 记录时停止
- **评论 24 | 👍 8**
- 长聊天的线程历史在分页加载时，遇到 `token_count` 记录会停止投影，导致后续消息无法显示。影响多版本（0.145.0 和 0.149.0）桌面端用户。
- https://github.com/openai/codex/issues/40342

### #29639 [Windows] WSL 工作区中 Browser Use Node REPL 因 sandboxCwd 未映射而失败
- **评论 22 | 👍 7**
- Windows 桌面应用在 WSL 文件系统上运行 agent 时，自动生成的 `node_repl` MCP server 仍使用 Windows 路径，导致工具调用传入 Linux 路径而失败。
- https://github.com/openai/codex/issues/29639

### #42501 [Windows] 26.901.1978.0 更新后应用无法启动 UI
- **评论 13 | 👍 1**
- 升级到 `26.901.1978.0` 后，Codex 启动了多个 `ChatGPT.exe` 进程但始终没有可见窗口。调查指向新打包的 `cua_node` 运行时无法复制 `node_repl.exe`。
- https://github.com/openai/codex/issues/42501

### #30910 [Feature] 重新开启 #19464，支持 1M 上下文
- **评论 11 | 👍 8**
- 用户呼吁将上下文窗口从 272k 提升至 1M。他们认为 GPT-5.5 时代 272k 已成为实际瓶颈，且相关讨论常被官方关闭。
- https://github.com/openai/codex/issues/30910

### #43058 [Bug] Prompt 被误报违反 usage policy
- **评论 11 | 👍 0**
- Codex CLI v0.153.4 搭配 `gpt-6-astra` 时，正常 prompt 被错误标记为违反使用政策，导致任务无法执行。
- https://github.com/openai/codex/issues/43058

### #30271 [Bug] 合法逆向工程工作被误报“网络霸凌”政策违规
- **评论 8 | 👍 4**
- 已通过 OpenAI 网络安全验证（chatgpt.com/cyber）的用户，在进行自有硬件的逆向工程和漏洞分析时，仍被安全策略拦截。
- https://github.com/openai/codex/issues/30271

### #41480 [macOS] “Open in” 子菜单永远显示 “Loading available apps…”
- **评论 5 | 👍 7**
- macOS 桌面版 `26.825.41651` 中，无法通过 “Open in” 子菜单打开 VS Code 等外部编辑器，菜单一直处于加载状态。
- https://github.com

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-09

## 今日速览

今日发布了三个版本（v0.61.0-nightly、v0.60.0-preview.0 和 v0.59.0），重点修复了 NTFS 路径处理、MCP OAuth 安全性与 Web 抓取验证等核心问题。社区讨论热度集中在 Agent 中断恢复误报（#22323）、通用 Agent 挂起（#21409）以及 Shell 命令执行卡死（#25166）等稳定性痛点。此外，Auto Memory 新增的安全与重试机制相关 Issue 开始吸引关注。

---

## 版本发布

### v0.61.0-nightly.20260909.ged2ac40df
- **fix(core)**: 缓解 NTFS 8.3 短文件名（SFN）路径问题（PR #29116）
- **fix(cli)**: 在沙箱容器中隔离设置目录（PR #29216）

### v0.60.0-preview.0
- **fix(core)**: 改进 Web 抓取工具的目标验证与连接路由（PR #29120）
- **fix(core)**: 在 MCP OAuth 流程中强制执行 RFC 9207 issuer 标识（PR #29121）

### v0.59.0
- 常规版本更新，清理了 v0.58.0-preview.0 的变更日志并完成版本号递增。

> 链接：
> - [v0.61.0-nightly](https://github.com/google-gemini/gemini-cli/releases/tag/v0.61.0-nightly.20260909.ged2ac40df)
> - [v0.60.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.60.0-preview.0)
> - [v0.59.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0)

---

## 社区热点 Issues（Top 10）

### 1. Subagent 在达到 MAX_TURNS 后被误报为 GOAL 成功
**#22323** | 评论：13 | 👍：2 | priority/p1 | kind/bug
`codebase_investigator` 子代理在达到最大轮次后，状态和终止原因均显示为成功（GOAL），尽管实际未完成任何分析。此问题掩盖了真实的中断原因，干扰了用户对 Agent 行为的判断。
🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### 2. 利用模型的 bash 亲和性：零依赖 OS 沙箱与意图路由
**#19873** | 评论：9 | 👍：1 | priority/p2 | kind/enhancement
主张利用 Gemini 3 模型原生擅长 POSIX 工具链的特点，构建更具安全性的零依赖沙箱，并在命令执行后进行意图路由，在不牺牲安全性的前提下提升模型原生能力。
🔗 https://github.com/google-gemini/gemini-cli/issues/19873

### 3. 通用 Agent 挂起
**#21409** | 评论：8 | 👍：8 | priority/p1 | kind/bug
当 `gemini-cli` 将任务委托给通用 Agent 时，会无限期挂起（用户等待长达一小时无响应）。明确指示不委派子代理可规避此问题，表明故障点在通用 Agent 路径。
🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### 4. 评估 AST 感知的文件读取、搜索和映射的影响
**#22745** | 评论：7 | 👍：1 | priority/p2 | kind/feature
EPIC 跟踪一系列调查：AST 感知工具能否更精确地定位方法边界，减少因误读导致的轮次消耗和 token 噪声，优化 codebase 导航。
🔗 https://github.com/google-gemini/gemini-cli/issues/22745

### 5. Gemini 对 skills 和 sub-agents 的使用不够充分
**#21968** | 评论：6 | priority/p2 | kind/bug
用户反馈 Gemini 几乎不会主动调用自定义 skills 和子代理，即使当前任务高度相关。例如已有的 gradle/git 技能描述明确，模型仍不会在需要时自动使用，只有显式指令才会触发。
🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### 6. Auto Memory 需添加确定性脱敏并减少日志
**#26525** | 评论：5 | priority/p2 | area/security | kind/bug
Auto Memory 在将 transcript 内容发送给后台提取模型时，脱敏指令发生在内容进入模型上下文之后，无法真正防止泄露。且服务可能记录已有技能内容。建议在发送前做确定性脱敏。
🔗 https://github.com/google-gemini/gemini-cli/issues/26525

### 7. Shell 命令执行完成后卡在 "Waiting input"
**#25166** | 评论：4 | 👍：3 | priority/p1 | kind/bug
简单 CLI 命令执行完毕后，Gemini CLI 仍显示命令为活动状态并等待用户输入，导致会话卡死。此问题高频复现，严重影响使用体验。
🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### 8. 增强 browser_agent 韧性：自动会话接管与锁恢复
**#22232** | 评论：4 | priority/p3 | kind/feature
`BrowserManager.ts` 在遇到锁定的浏览器 profile 时采用 fail-fast 策略，使用 persistent 会话模式或存在残留进程时，应该尝试自动接管会话或恢复锁，而不是直接失败退出。
🔗 https://github.com/google-gemini/gemini-cli/issues/22232

### 9. 符号链接的 Agent 文件无法被识别
**#20079** | 评论：4 | priority/p2 | kind/bug
`~/.gemini/agents/filename.md` 如果是符号链接，则不会被识别为 Agent。用户期望符号链接能够正常工作，以便于管理 agent 定义文件。
🔗 https://github.com/google-gemini/gemini-cli/issues/20079

### 10. Browser 子代理在 Wayland 环境下失败
**#21983** | 评论：4 | 👍：1 | priority/p1 | kind/bug
Browser subagent 在 Wayland 会话中运行失败，终止原因为 GOAL，但实际并未完成目标。与 Wayland 显示服务器的兼容性问题需要解决。
🔗 https://github.com/google-gemini/gemini-cli/issues/21983

---

## 重要 PR 进展（Top 10）

### 1. fix(agent): 阻止会话上下文在中断回合时被污染
**#29265** | OPEN | size/m
修复 SIGINT、超时或工具执行中止时中断代理流会污染会话历史的问题，确保后续 prompt 执行不再受损坏上下文影响。
🔗 https://github.com/google-gemini/gemini-cli/pull/29265

### 2. fix(cli): 避免确认后的重复历史和遥测记录
**#29248** | OPEN | size/m
修复在确认操作（如 `/resume save`）期间若收到其他消息，命令历史会重复插入的问题；同时减少遥测数据的重复上报。
🔗 https://github.com/google-gemini/gemini-cli/pull/29248

### 3. fix(core): 将 abortSignal 转发至 BaseLlmClient 的 retryWithBackoff
**#29089** | CLOSED | size/s
`SessionSummaryService`、聊天压缩、分类器、prompt completion 等场景使用 `BaseLlmClient` 时，abortSignal 未传递给 `retryWithBackoff`。本次修复确保中断信号能正确取消重试。
🔗 https://github.com/google-gemini/gemini-cli/pull/29089

### 4. fix(cli): 防止 Git 仓库中认证时崩溃
**#29163** | OPEN | priority/p1, size/l
修复 macOS Seatbelt 或受限权限环境下的 Git 仓库中启动崩溃问题——`useGitBranchName` hook 在读取 `.git` 受限时导致 CLI 崩溃。
🔗 https://github.com/google-gemini/gemini-cli/pull/29163

### 5. fix(core): 停止在 shell 执行中清空用户 Git 配置
**#29156** | OPEN | size/m
`ShellExecutionService.prepareExecution` 曾将 `GIT_CONFIG_GLOBAL` 和 `GIT_CONFIG_SYSTEM` 指向 `/dev/null`，导致 shell 工具命令无法读取用户真实 Git 配置（如 `user.name`），本次修复移除该逻辑。
🔗 https://github.com/google-gemini/gemini-cli/pull/29156

### 6. fix(core): 在 isEmpty 中正确解码 BOM 编码内容
**#29155** | OPEN | size/m
`isEmpty()` 检测到 BOM 后仍按 UTF-8 解码采样字节，导致 UTF-16/UTF-32 编码的纯空白计划文件被判定为非空。修复后按 BOM 声明解码，确保 `validatePlanContent` 行为正确。
🔗 https://github.com/google-gemini/gemini-cli/pull/29155

### 7. fix(core): 技能优先级与活跃状态的大小写不敏感处理
**#29151** | OPEN | priority/p1, size/m
修复 `SkillManager` 中因技能名称大小写不一致导致的优先级覆盖失效问题，确保工作区技能对内置/扩展技能的正确覆盖。
🔗 https://github.com/google-gemini/gemini-cli/pull/29151

### 8. fix(vscode-ide-companion): 解决 MCP 流打开时 stop() 挂起
**#29088** | CLOSED | size/m
`IdeServer.stop()` 因 MCP 长连接流未关闭而永远无法 resolve，阻塞 VS Code 扩展停用。修复后可正常退出。
🔗 https://github.com/google-gemini/gemini-cli/pull/29088

### 9. fix(cli): 阻止并发扩展安装竞争
**#29087** | CLOSED | size/l
两个 Gemini CLI 进程同时安装或更新同一扩展时会互相交错，造成文件损坏。本次利用 `proper-lockfile` 引入锁机制规避此问题。
🔗 https://github.com/google-gemini/gemini-cli/pull/29087

### 10. fix(core): Plan Mode 在非交互式会话中不再等待用户反馈
**#29063** | CLOSED | priority/p1, size/m
修复非交互模式（`gemini -p "..." -y`）下 Plan Mode 指令要求"等待用户轮次"导致挂起的行为（Fixes #28913 / #26004）。
🔗 https://github.com/google-gemini/gemini-cli/pull/29063

---

## 功能需求趋势

| 方向 | 相关 Issues | 热度 |
|------|------------|------|
| **Agent 稳定性与中断恢复** | #22323, #21409, #25166 | 非常高 |
| **AST 感知代码工具** | #22745, #22746 | 高 |
| **Auto Memory 改进** | #26525, #26522, #26523, #26516 | 中高 |
| **Browser Agent 韧性** | #22232, #21983, #22267 | 中高 |
| **Skills/Sub-agent 自主性** | #21968, #20195, #21432 | 中 |
| **安全与沙箱** | #19873, #26525, #22672 | 中 |
| **会话共享与协作** | #22598, #21432 | 低中 |

社区最关心的三个方向：
1. **Agent 执行可靠性**：中断误报、挂起、命令卡死等稳定性问题集中在 P1/P2 级，且复现率高。
2. **AST 感知与上下文效率**：多个 EPIC 投入评估通过 AST 工具降低 token 消耗、提升代码导航精度。
3. **Auto Memory 安全与质量**：批量出现的相关 Issue 表明自动记忆功能正经历安全审查与质量加固。

---

## 开发者关注点

- **中断后的信号误导**：子代理在中断后仍上报 `GOAL` 成功，开发者认为 Agent 的终止原因系统需要重新设计，至少应区分 `INTERRUPTED` 与 `GOAL`。（#22323）
- **交互式提示挂起**：创建 Vite 应用等交互式命令会让 CLI 卡死在提示符处，且 `/compress` 在会话恢复后不生效。（#22465, #21335）
- **配置与路径兼容**：`settings.json` 覆盖被 Browser Agent 忽略（#22267）、符号链接的 agent 文件不被识别（#20079）、BOM 编码内容误判（#29155）——权限与文件系统的边界case仍需打磨。
- **上下文污染问题**：中断回合会导致后续 prompt 失效（PR #29265），开发者对当前中断机制的健壮性存疑，期待后续版本修复。
- **工具过多时的 400 错误**：超过 400 个工具时 CLI 报 400 错误，开发者希望 Agent 能按需裁剪工具集合，而非一次性全部加载。（#24246）

---

*本日报由 GitHub 数据自动整理生成，数据截止 2026-09-09。如需查看完整 Issue/PR 列表，请访问 [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区动态日报 — 2026-09-09

### 1. 今日速览

今日发布 v1.0.84-2 / v1.0.84-3 两个修复版本，其中 Vim 编辑模式正式面向所有用户开放，社区呼声最高的 Issue #13 随之关闭。值得警惕的是，Windows 平台与会话恢复类问题继续占据 Issue 榜前列，长期会话的稳定性成为开发者核心痛点。

---

### 2. 版本发布

**v1.0.84-3（修复）**
- `/copy` 现在会包含任务完成消息（如果可用）
- 修复 OAuth 认证的 MCP 服务器在会话启动期间连接不可靠的问题

**v1.0.84-2（新功能 + 改进）**
- **Vim 模式全面开放**：可通过 `/vim` 命令或在配置中设置 `editorMode: "vim"` 启用，支持在 composer 中进行模态编辑，并显示当前模式
- 在受支持的 Windows 沙箱策略下，交互式 shell 命令现在会记录被阻止的访问行为

---

### 3. 社区热点 Issues（Top 10）

**#13 — CLI 输入应支持 vi/vim 模式（已关闭）**  
💬 11 评论 | 👍 76  
历经一年多的社区呼吁，Vim 模式终于随 v1.0.84-2 正式落地。作为 CLI 编辑体验中反馈最强烈的需求，该 Issue 的关闭标志着键盘驱动编辑在 Copilot CLI 中成为一等公民。  
🔗 https://github.com/github/copilot-cli/issues/13

**#4756 — Windows 上创建新 Local 会话前需归档每个空闲项目会话**  
💬 7 评论 | 👍 19  
Windows 桌面应用 1.1.15 的回归问题：一旦项目有活动 CLI 进程，新建会话即失败。用户被迫手动归档旧会话，严重打断多任务工作流，点赞数今日攀升至 19，反映影响面广。  
🔗 https://github.com/github/copilot-cli/issues/4756

**#2943 — OpenRouter 集成**  
💬 3 评论 | 👍 14  
社区对第三方模型提供商的支持诉求持续升温。用户希望复用 OpenRouter 的模型目录，将其作为 Copilot CLI 的后端之一，以避免 token 消耗问题。  
🔗 https://github.com/github/copilot-cli/issues/2943

**#4612 — FileWatch 事件循环失控，冻结 TUI 并生成 13GB 调试日志**  
💬 9 评论 | 👍 1  
长时间运行的会话可能进入 `FileWatch` 空转死循环，导致界面无响应且日志文件暴涨至 13GB。属于典型的"低概率、高破坏性"问题，官方已标记 triage 待查。  
🔗 https://github.com/github/copilot-cli/issues/4612

**#4742 — 桌面应用 1.1.15 无法创建第二个 Local 会话**  
💬 10 评论 | 👍 5  
同一项目已有活动 Local 会话时新建会话报 `invalid argument` 错误，与 #4756 同源，是今日 Windows 会话管理问题的主线索。  
🔗 https://github.com/github/copilot-cli/issues/4742

**#4664 — 恢复长期会话时 JavaScript 堆内存溢出崩溃**  
💬 7 评论 | 👍 2  
恢复超大会话时 Node.js/V8 直接 OOM，用户无法继续已有上下文。该问题与 #4612 共同指向"长期会话的可靠性与资源控制"这一核心短板。  
🔗 https://github.com/github/copilot-cli/issues/4664

**#2199 — 增加 Ctrl+Backspace 删除整个单词的快捷键**  
💬 3 评论 | 👍 7  
基础编辑能力缺口。Vim 模式已补齐，但非 Vim 用户的日常编辑效率仍受影响，Windows 上同样失效（#3858），形成跨平台一致的痛点。  
🔗 https://github.com/github/copilot-cli/issues/2199

**#4753 — v1.0.83 恢复会话时 MCP 连接超时从 ~16s 缩短至 ~1s**  
💬 3 评论 | 👍 1  
回退性更改：恢复会话的前台交接逻辑不再等待 stdio MCP 服务器完成初始化，导致这些服务器在整个会话中静默不可用。对重度 MCP 用户影响明显。  
🔗 https://github.com/github/copilot-cli/issues/4753

**#4505 — 恢复会话后残留 stale connection item ID，所有 prompt 报 400**  
💬 3 评论 | 👍 3  
一次中断响应后，恢复的会话会永久性报错 `400 input item ID does not belong to this connection`，且 `/fork` 无法自愈。与 #4770 PR 中的 WebSocket 退出机制相关。  
🔗 https://github.com/github/copilot-cli/issues/4505

**#4775 — Mission Control 仪表盘链接 404：路径应为 /agents/tasks/ 而非 /copilot/tasks/**  
💬 3 评论 | 👍 0  
UI 层与 CLI 层的路由不一致，远程会话实际存活但无法从 Web 端访问。属于新引入的仪表盘功能缺陷。  
🔗 https://github.com/github/copilot-cli/issues/4775

**#4764 — 自动批准模式约 1 小时后失效**  
💬 1 评论 | 👍 0  
`/permissions assisted` 模式在约一小时后静默停止工作，必须新开会话才能恢复。对自动化/无人值守流程构成严重障碍。  
🔗 https://github.com/github/copilot-cli/issues/4764

---

### 4. 重要 PR 进展

**#4770 — 文档化 WebSocket responses 退出机制（开放中）**  
针对采用 WebSocket 响应的模型，在网络受限或遭遇 `400 input item ID` 错误时，提供一个文档化的切换出口。与 #4505 问题直接相关，是当前会话稳定性的重要补丁。  
🔗 https://github.com/github/copilot-cli/pull/4770

**#4761 — install.sh：报告不支持的操作系统（已合并/关闭）**  
修复 FreeBSD 等平台误报 "Windows detected" 的问题。安装脚本将明确提示"不支持的操作系统"，避免误导性错误信息。  
🔗 https://github.com/github/copilot-cli/pull/4761

**#4100 — 标题为用户名、内容为"安全性"的 PR（已关闭）**  
疑似无效/测试 PR，无实际代码变更。社区动态中的噪声项，但既然列出，提醒维护者注意此类提交的审查流程。  
🔗 https://github.com/github/copilot-cli/pull/4100

---

### 5. 功能需求趋势

- **编辑器体验补全**：Vim 模式落地后，剩余编辑痛点集中在`Ctrl+Backspace`删除单词、Windows 快捷键兼容性等基础操作，用户期望"所有平台上的肌肉记忆保持一致"。
- **模型自由接入**：OpenRouter 集成呼声持续走高，社区希望摆脱仅限官方模型列表的限制，复用第三方模型目录与自有 API key。
- **MCP 生态成熟化**：OAuth scope 参数缺失、认证服务器重定向不兼容、注册表需匿名访问等问题频发，表明 MCP 集成正从"能连"走向"可靠、安全、可管理"阶段。
- **会话生命周期管理**：长期会话的内存控制、恢复时连接回收（MCP 握手超时）、并发会话策略（Windows 上的本地会话冲突）成为高频关键词。

---

### 6. 开发者关注点

- **Windows 平台体验明显滞后**：#4756、#4742、#3858、#4771 等共同指向 Windows 端会话管理、快捷键、任务栏状态等系统性体验问题，开发者对平台一致性要求强烈。
- **会话恢复的稳定性"欠债"**：内存溢出（#4664）、FileWatch 死循环（#4612）、stale item ID（#4505）、MCP 握手被截断（#4753）——恢复一个老会话变成"开盲盒"，可靠性是当前最大信任危机。
- **状态可见性不足**：spinner 在等待输入时仍旋转（#4778）、TODO 列表不展示（#1724）、通知 badge 残留（#4381）。用户希望界面能准确区分"正在思考"和"正在等你"。
- **自动批准模式抗衰减**：#4764 中"1 小时失效"虽然仅 1 条评论，但其对流水线式工作流的破坏力极大，应纳入高优 triage 队列。

---

*数据更新截至 2026-09-09，基于 GitHub 公开仓库 github/copilot-cli 的 issues、PRs 与 releases 信息。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-09）

## 今日速览

今日无新版本发布；共 3 个 Issue、2 个 PR 在近 24 小时内有更新。最值得关注的是新提交的 `/login` 设备认证失败问题（#2638，HTTP 500），直接阻断登录流程且影响 VS Code 扩展；此外，两个历史增强请求（#1270、#2601）已关闭，PR #2595 则为关键文件安全修复，防止非 UTF-8 文件被编辑时损坏。

## 社区热点 Issues

> 近 24 小时更新共 3 条，全部列出。

### 1. `/login` 设备认证失败 HTTP 500（#2638，开放中）
- **链接**: [MoonshotAI/kimi-cli Issue #2638](https://github.com/MoonshotAI/kimi-cli/issues/2638)
- **时间**: 创建 2026-09-09 | 更新 2026-09-09 | 评论 0
- **影响等级**: 严重 🔴
- **详情**: CLI v0.42.0（macOS）执行 `/login` 后，浏览器中批准设备码（如 `WGBT-C3BW`）但返回 HTTP 500；免费套餐（Adagio）复现，VS Code 扩展同样受影响。
- **关注价值**: 登录是 CLI 日常使用的入口，此问题会阻断所有用户，且跨平台（CLI + 扩展）复现，急需官方回应。

### 2. VSCode 扩展：`@` 后优先显示已打开文件（#1270，已关闭）
- **链接**: [MoonshotAI/kimi-cli Issue #1270](https://github.com/MoonshotAI/kimi-cli/issues/1270)
- **时间**: 创建 2026-02-27 | 更新 2026-09-09 | 评论 1
- **详情**: v0.4.3 时代提交的增强请求：输入 `@` 时，备选文件应优先展示 VSCode 中已打开的文件，因用户大概率要对其进行操作。
- **状态分析**: 今日关闭，但未明确说明是否已实现，值得查看关闭理由。

### 3. Kimi Web：引用并回复 AI 回复的任意片段（#2601，已关闭）
- **链接**: [MoonshotAI/kimi-cli Issue #2601](https://github.com/MoonshotAI/kimi-cli/issues/2601)
- **时间**: 创建 2026-08-11 | 更新 2026-09-09 | 评论 0
- **详情**: 建议支持在 Web 端对 AI 回复的任意文本（段落、代码块、计划步骤、diff 行）选定后添加评论或追问，便于 Agent 针对该片段继续处理。
- **状态分析**: 今日关闭，可能已在内部规划或实现中。

## 重要 PR 进展

> 近 24 小时更新共 2 条，全部列出。

### 1. fix(fetch): 抑制重复提取的注释文本（#1863，已合并）
- **链接**: [MoonshotAI/kimi-cli PR #1863](https://github.com/MoonshotAI/kimi-cli/pull/1863)
- **时间**: 创建 2026-04-13 | 更新 2026-09-09
- **内容**: 将 `FetchURL` 的 HTML 提取路径改为分别检查 Trafilatura 的正文与评论内容；当评论与正文规范化后相同时，抑制重复提取的评论，并新增回归测试（针对 GitHub Issue 提取输出的去重）。
- **意义**: 改善 fetch 场景下内容提取的准确性，避免重复文本污染上下文。

### 2. fix(StrReplaceFile): 拒绝编辑非 UTF-8 文件（#2595，开放中）
- **链接**: [MoonshotAI/kimi-cli PR #2595](https://github.com/MoonshotAI/kimi-cli/pull/2595)
- **时间**: 创建 2026-08-06 | 更新 2026-09-08
- **关联**: 解决 Issue #2591
- **内容**: 当前 `StrReplaceFile` 使用 `errors="replace"` 解码整个文件，编辑后回写时任何非 UTF-8 字节都会被替换为 U+FFFD（即便与编辑位置无关），导致文件损坏。该 PR 改为直接拒绝编辑非 UTF-8 文件。
- **意义**: 修复一个易被忽视但破坏性强的数据损坏 bug，提升编辑操作的安全性。

## 功能需求趋势

从今日更新的 Issue 与 PR 中，社区关注方向集中在以下三点：

- **IDE 集成（VS Code）**：如 #1270 的 `@` 文件优先级，强调在编辑器内最大化效率；但该需求来自 v0.4.3 时代，已被关闭，建议开发者关注版本更新中的相关改动。
- **Web 交互体验**：#2601 提出对 AI 回复片段进行精确定位与追问，需求具体且实用，尽管该提案已关闭，仍可能是产品演进方向。
- **认证与 CLI 基础稳定性**：#2638 的登录 HTTP 500 是当前最紧迫的问题，涉及设备码流与服务端交互，或成为近期修复重点。

## 开发者关注点

- **登录链路可靠性**：`/login` 设备认证在浏览器批准后失败（HTTP 500），影响所有平台，且无任何即时工作区，属高风险问题，急需 hotfix。
- **编辑操作的数据安全**：社区通过 #2591/#2595 反馈并修复了非 UTF-8 文件的潜在损坏问题，说明用户对文件读写安全性高度敏感，类似的防护逻辑应推广至其他编辑命令。
- **输入效率工具的体验细节**：#1270 虽然关闭，但反映了开发者“围绕当前打开文件操作”的直觉习惯，类似的上下文感知优化（如优先展示活跃文件/最近文件）可能仍值得继续探索。
- **需求确认的即时性**：#1270 与 #2601 已关闭但未见明确说明，社区希望看到更清晰的关闭原因或替代方案，避免重复提交同类请求。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报 — 2026-09-09

### 今日速览

v1.18.30 发布，核心更新是为 GPT-6 模型引入 Astra 系统提示词，并修复了 Bedrock DeepSeek 模型 ID、Azure/OpenAI provider SDK 兼容性问题。社区层面，数据库无限膨胀与 prompt 缓存缺失成为当前最集中的吐槽点，多个相关 Issue 活跃度高；桌面端 UI 重构与 TUI 稳定性修复的 PR 也在持续推进中。

---

### 版本发布

**v1.18.30**（过去 24 小时）
- Core 改进：为 GPT-6 模型添加 Astra 系统提示词
- Bug 修复：
  - 修复 Bedrock DeepSeek 模型 ID（含 ARN 格式）解析问题（@YeEmrick）
  - 更新 Azure provider SDK，纳入兼容性修复
  - 更新 OpenAI provider SDK

https://github.com/anomalyco/opencode/releases/tag/v1.18.30

---

### 社区热点 Issues（10 个）

**1. Gemma 4 (e4b) 工具调用在 Ollama OpenAI 兼容 API 下失败**
`#20995` ｜ 已关闭 ｜ 👍 48 ｜ 💬 36
模型正确返回 `tool_calls`，但 OpenCode 无法识别流式 tool_calls，导致工具调用链路断裂。48 个 👍 表明受影响用户面较广，是跨 provider 兼容性的典型问题。
https://github.com/anomalyco/opencode/issues/20995

**2. [2.0] event 表无界增长：opencode.db 达 13GB+**
`#33356` ｜ 开放 ｜ 👍 9 ｜ 💬 29
事件表从不清理或压缩，`message.updated.1` 快照持续堆积，两台长期运行实例均膨胀至约 13GB。这是当前最严重的存储隐患，已挤占 22GB 卷的 97-99% 空间。
https://github.com/anomalyco/opencode/issues/33356

**3. 网页版 VSCode 终端（code-server / Codespaces）剪贴板复制失效**
`#26459` ｜ 开放 ｜ 👍 2 ｜ 💬 13
UI 显示 "Copied to clipboard" 但实际剪贴板为空。影响 code-server、GitHub Codespaces、Gitpod 等远程开发场景，是云端开发工作流的高频痛点。
https://github.com/anomalyco/opencode/issues/26459

**4. XDG Base Directory 规范违规：node_modules 被安装到 ~/.config**
`#27786` ｜ 开放 ｜ 👍 9 ｜ 💬 10
运行时依赖被写入 `~/.config/opencode` 而非 `~/.local/share`，违反 freedesktop 规范，影响配置隔离和多用户环境。9 个 👍 说明关注度不低。
https://github.com/anomalyco/opencode/issues/27786

**5. DeepSeek-v4-flash-free 模型在 Zen provider 下拉框中缺失**
`#43805` ｜ 开放 ｜ 👍 0 ｜ 💬 8
模型在 `/zen/v1/models` API 中存在且配置正确，但 TUI 模型选择器不显示。Zen 模型目录与 UI 不一致的问题反复出现，用户需手动编辑配置才能使用。
https://github.com/anomalyco/opencode/issues/43805

**6. [2.0] TUI 每次启动向 /tmp 泄漏约 21MB .so 文件**
`#42700` ｜ 开放 ｜ 👍 0 ｜ 💬 8
每次启动泄漏一个 ~21MB 的 `.so` 且不清理，多次启动后 tmpfs 被填满，TUI 直接无法启动（OpenTUI 加载错误）。Arch Linux 用户受影响明显。
https://github.com/anomalyco/opencode/issues/42700

**7. [2.0] 选择性会话内容删除功能再次缺失**
`#48090` ｜ 开放 ｜ 👍 1 ｜ 💬 5
继 #44984 的替代 API 被移除后，用户仍无法选择性删除会话中的工具/推理内容。CodeNomad 0.20.0 已采用旧 API，现在处于无人维护状态。今日新开 Issue，属于 2.0 回归问题。
https://github.com/anomalyco/opencode/issues/48090

**8. Bedrock GPT-5.6：usage total 重复计算缓存输入，导致每次消息后触发自动压缩**
`#47296` ｜ 已关闭 ｜ 👍 0 ｜ 💬 4
Bedrock 的 usage total 将缓存输入二次计数，~150k prompt 被记为 ~300k，`isOverflow` 误判超限。会话反复压缩，上下文从 150k 降到 40k 再爬升，形成恶性循环。
https://github.com/anomalyco/opencode/issues/47296

**9. Agent 通过 read 工具累积 51 张图片，触发 provider 50 图上限后会话卡死**
`#47487` ｜ 开放 ｜ 👍 0 ｜ 💬 3
816 条消息的会话因图片累积超过 provider 限制而彻底无法恢复，用户没有任何手段清理图片或重置上下文。会话健壮性问题的典型代表。
https://github.com/anomalyco/opencode/issues/47487

**10. OpenCode Go：deepseek-v4-flash 和 qwen3.8-max 无 prompt 缓存**
`#48116` ｜ 开放 ｜ 👍 0 ｜ 💬 1
同一端点上 glm-5.2 缓存正常，但 DeepSeek/Qwen 每次请求都重新处理完整前缀，流量和成本浪费严重。今日新开，与 #41125 互相印证，是 Go 订阅用户的高频困扰。
https://github.com/anomalyco/opencode/issues/48116

---

### 重要 PR 进展（10 个）

**1. fix(provider): 解析 OpenRouter 路由修饰符后缀**
`#48117` ｜ 开放
处理 `:floor`、`:nitro`、`:exacto`、`:online` 等路由修饰后缀，使其正确映射到 models.dev 目录。此前所有带修饰符的模型引用都会校验失败。
https://github.com/anomalyco/opencode/pull/48117

**2. fix(core): 修复 bash 在进程退出后挂起**
`#42756` ｜ 开放
一个 PR 关闭 7 个相关 Issue（#20902、#25038、#28697、#36342、#37838、#42044、#42524），是 bash 工具链历史性挂起问题的集中修复，价值极高。
https://github.com/anomalyco/opencode/pull/42756

**3. feat(app): 为会话时间线添加查找栏**
`#48088` ｜ 已关闭
为会话转录增加 `mod+f` 页内搜索，补上了长会话无法定位历史消息的 UX 缺口。
https://github.com/anomalyco/opencode/pull/48088

**4. fix(opencode): 合并任务描述中的会话权限**
`#48107` ｜ 开放
将 agent 权限与会话权限正确合并后传给 `describeTask`，修复可用 agent 列表未反映会话 deny/allow/ask 配置的问题。
https://github.com/anomalyco/opencode/pull/48107

**5. fix(core): 在设备授权中声明支持组织范围**
`#46570` ｜ 已关闭
添加 `supports_org_scope: true` 声明，使 Console 能为新客户端做组织级凭证授权，旧客户端不受影响。配合 opencode-console PR #1896 使用。
https://github.com/anomalyco/opencode/pull/46570

**6. feat: 添加目录覆盖环境变量和 OPENCODE_APPNAME**
`#8963` ｜ 开放
新增 `OPENCODE_DATA_DIR`、`OPENCODE_CACHE_DIR`、`OPENCODE_LOG_DIR` 和 `OPENCODE_APPNAME`，支持便携模式和 profile 隔离。这是 XDG 违规 Issue（#27786）的治本方案，但已开放近 8 个月。
https://github.com/anomalyco/opencode/pull/8963

**7. feat(desktop): 重新设计设置导航与项目编辑**
`#47983` ｜ 开放
将桌面端设置重组为客户端偏好、服务器、项目三个分区，提供嵌套导航和返回链路，并对项目编辑与服务器配置做了视觉重构。
https://github.com/anomalyco/opencode/pull/47983

**8. feat(desktop): 将状态整合进会话摘要**
`#48103` ｜ 开放
将原 Status 菜单移入会话详情，改为 Project 和 Server 卡片。卡片默认展开并记忆展开状态，减少层级跳转。
https://github.com/anomalyco/opencode/pull/48103

**9. fix(cli): 将 --model 透传到 TUI 入口**
`#47699` ｜ 开放
`opencode

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-09-09

## 今日速览

今日社区热度聚焦于 **OpenCode Go 新硬性要求的 `x-opencode-session` 头导致 Pi 多个 provider 请求失败**（#9230、#9326、#9371），相关 Issue 密集出现并快速被标记关闭。此外，TUI 全屏模式滚动性能问题、WebSocket 重试逻辑缺陷等老 Issue 持续获得关注；PR 方面以依赖安全修复和 UI/编辑器细节改进为主，无新版本发布。

---

## 社区热点 Issues

### 1. WebSocket 重试仅处理两种错误码，其他瞬时故障直接终止回合
- **#7444** [CLOSED] | 💬 10 条评论
- 在 `openai-codex-responses.js` 中，重试循环只特判 `previous_response_not_found` 和 `websocket_connection_limit_reached`，其他 `response.failed` 或顶层 `error` 帧会被直接抛出为 `CodexAp...` 错误，导致瞬态网络故障无法恢复。
- 社区认为该错误分类逻辑过于苛刻，应覆盖更多可重试的瞬态错误。
- 🔗 https://github.com/badlogic/pi-mono/issues/7444

### 2. Esc 取消流式请求经常失效，直到 provider 自然完成
- **#8823** [CLOSED] | 💬 10 条评论
- 模型流式输出时按 Esc 不会可靠地终止底层 HTTP 请求，虽然 abort 被记录（最终 turn 以 `stopReason: "a..."` 持久化），但实际停不下来。
- 这是交互体验的核心痛点，评论中讨论了几种 abort 信号传递链路的修复方向。
- 🔗 https://github.com/badlogic/pi-mono/issues/8823

### 3. 全屏模式滚轮滚动速度比普通模式慢 3 倍
- **#9052** [OPEN] | 👍 3 | 💬 7 条评论
- 用户切换到全屏模式（为固定底部输入框）后发现滚轮滚动明显变慢，常规模式正常。这是目前最受关注的 UI 性能问题之一，已有 3 个 👍。
- 🔗 https://github.com/badlogic/pi-mono/issues/9052

### 4. opencode-go provider 未发送新要求的 `x-opencode-session` 头
- **#9230** [CLOSED] | 👍 1 | 💬 6 条评论
- OpenCode Go 自 2026-09-06 起要求请求携带稳定会话 ID 头，否则“可能报错”。Pi 的 `opencode-go` provider 尚未适配，导致部分请求被拒。
- 与 #9326、#9371 构成同一条问题线，反映出新协议硬性要求对生态的连锁影响。
- 🔗 https://github.com/badlogic/pi-mono/issues/9230

### 5. openai-responses 将 developer 角色选择绑定到 `model.reasoning`
- **#7445** [OPEN] [inprogress] | 💬 6 条评论
- 代码中只有当 `model.reasoning` 为真时才把 `context.systemPrompt` 作为 `developer` 角色发送，导致 `supportsDeveloperRole: true` 的配置被忽略。
- 已标记进行中，属于模型兼容性的细粒度问题。
- 🔗 https://github.com/badlogic/pi-mono/issues/7445

### 6. `pi.sendMessage()` 自定义消息绕过 `before_agent_start` 事件
- **#5581** [OPEN] [inprogress] | 👍 1 | 💬 5 条评论
- 带 `triggerTurn: true` 的自定义消息直接调用 `_runAgentPrompt` 而非 `prompt()`，绕过 before_agent_start 钩子，影响扩展对完整事件流的依赖。
- 🔗 https://github.com/badlogic/pi-mono/issues/5581

### 7. 代理级重试退避缺乏上限，长时间中断下退避时间不可控
- **#8826** [OPEN] [inprogress] | 💬 4 条评论
- 当上游持续 503（如 `Too many open files`）时，coding-agent 的指数退避会无限增长。社区希望增加可配置的上限，让长时间重试稳定在一个固定间隔。
- 🔗 https://github.com/badlogic/pi-mono/issues/8826

### 8. 压缩/摘要路径缺少 provider 头，opencode 生态触发 400 MissingSessionID
- **#9302** [CLOSED] | 💬 4 条评论
- 所有分支总结和压缩在 opencode 系 provider 上都会命中 `400 MissingSessionID`，根源是扩展驱动摘要与原生路径共用同一处仅含认证的头来源。
- 与 `x-opencode-session` 缺失同源，修复可能一并解决。
- 🔗 https://github.com/badlogic/pi-mono/issues/9302

### 9. Claude Sonnet 5 经网关的 edit 工具调用有 13% 被截断为 `edits:[{}]`
- **#9212** [CLOSED] | 💬 4 条评论
- 一周内 134 次 `edit` 调用中有 18 次因参数截断而校验失败：14 次为 `edits:[{}]`，3 次第二个 edit 内容不完整。同环境 fable 模型为 0%，疑似网关适配问题。
- 🔗 https://github.com/badlogic/pi-mono/issues/9212

### 10. 设定启动时间预算，对标 jcode 的延迟与内存
- **#7739** [OPEN] | 💬 4 条评论
- 用户希望 Pi 设定启动预算以缩短与 jcode 的差距，并附上了两者的基准对比表（jcode v0.9.1888-dev vs pi 0.62.0），关注冷启动性能。
- 🔗 https://github.com/badlogic/pi-mono/issues/7739

---

## 重要 PR 进展

### 1. docs: 将交互测试和发布指南

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-09

## 今日速览

昨日发布 v0.23.1 稳定版（含 breaking change）与 v0.23.2-preview.0 预览版，主要修复 CI 及合并 WebUI 退役改动；社区对 Windows 下 conhost.exe 进程泄漏和本地模型 llama-server 兼容性问题的关注度最高；PR 侧 Web Shell 功能迭代和 daemon 架构演进成为主流方向。

## 版本发布

### v0.23.2-preview.0
- 修复 CI 中 E2E 测试在 fork 场景下压力过大的问题（[#11388](https://github.com/QwenLM/qwen-code/pull/11388)）

### v0.23.1
- **Breaking Change**：移除 `@qwen-code/webui` 包（[#9812](https://github.com/QwenLM/qwen-code/pull/9812)）
- 新增特性：Web Shell 中可视化和管理动态内容

### SDK TypeScript v0.1.9 / v0.1.10
- 内置 CLI 0.23.0 / 0.23.1
- 包含两项修复：managed memory 可用性现在遵循 `memory.enableManagedAutoMemory` 设置（[#6941](https://github.com/QwenLM/qwen-code/issues/6941)）；新增 prompt cache 相关修复（[#8464](https://github.com/QwenLM/qwen-code/pull/8464)）

## 社区热点 Issues（10 个）

1. **TUI 渲染层迁移 ink → OpenTUI（跟踪）** — [#8662](https://github.com/QwenLM/qwen-code/issues/8662)（33 评论）
   社区讨论最热烈的问题。ink 渲染器存在闪烁等结构性问题，已提交约 1037 行补丁仍难以根治，官方计划迁移到 OpenTUI，属 roadmap 上的终端 UX 改进项。

2. **[Windows] qwen-cli 泄漏 headless conhost.exe 进程** — [#11303](https://github.com/QwenLM/qwen-code/issues/11303)（10 评论，P1）
   VS Code Companion 内置的 qwen-cli 在 Windows 上运行约 12 小时后积累 347 个子进程、占用约 2.8GB 内存。P1 严重性，直接影响桌面端用户。

3. **本地 llama-server 报错 "400 Failed to initialize samplers"** — [#10530](https://github.com/QwenLM/qwen-code/issues/10530)（7 评论）与 [#10435](https://github.com/QwenLM/qwen-code/issues/10435)（6 评论，1👍）
   两个 issue 指向同一问题：v0.22.3 起本地 llama-server（Qwen3.8/3.6 等模型）无法初始化 grammar，gemma 等其他模型正常。已关闭，但用户反馈热度仍在。

4. **v0.23.1 在 Windows 11 更新后本地模型全部失效** — [#11410](https://github.com/QwenLM/qwen-code/issues/11410)（4 评论，P1）
   LM Studio 连接返回 API Error 400，用户称 v0.23.1 之前一切正常，疑似与系统更新后的环境变化相关。

5. **支持托管自定义 Web Shell 分发版** — [#11358](https://github.com/QwenLM/qwen-code/issues/11358)（4 评论，P3）
   `qwen serve` 目前只能使用内置 Web Shell，集成方希望托管自己的前端应用且保留 daemon API，能独立更新前端而无需重建 Agent。

6. **daemon 的 Skill 管理状态与 ACP child 解耦** — [#11274](https://github.com/QwenLM/qwen-code/issues/11274)（4 评论，P3）
   规划通过一系列 1000 行以内的 PR 分阶段实现，daemon 负责目录和持久化，child 负责执行 Skill 并上报结果。社区关注 daemon 架构的演进方向。

7. **review: filter screen 丢失六项安全加固** — [#11205](https://github.com/QwenLM/qwen-code/issues/11205)（4 评论，P2）
   main 分支的 filter screen 在合并时丢失了读顺序、EACCES、U+FFFD、spawn 超时、候选上限、保留策略等六项加固，安全相关，值得跟踪。

8. **bug(lsp): 磁盘编辑后查询返回陈旧文档内容** — [#11439](https://github.com/QwenLM/qwen-code/issues/11439)（3 评论，P2）
   文件在磁盘上修改后，LSP 查询仍返回旧内容（如 hover 仍显示 `number` 而非 `string`），影响依赖 LSP 的编辑体验。

9. **provider 配置 reasoning 的边界情况跟进** — [#11328](https://github.com/QwenLM/qwen-code/issues/11328)（3 评论，P2）
   PR #10999 限制了首期范围，此 issue 记录后续边界情况，包括 deepseek-v4-pro 等模型的 reasoning 配置补全。

10. **ask_user_question 待处理卡片在会话重开后丢失** — [#11448](https://github.com/QwenLM/qwen-code/issues/11448)（2 评论，P2）
   模型调用 `ask_user_question` 后，卡片在会话重开时消失但侧边栏仍显示 "Input needed"，属于 daemon + Web Shell 的话路状态一致性问题。

## 重要 PR 进展（10 个）

1. **feat(mesh): 增加持久化的共享线程 Agent 协作** — [#11206](https://github.com/QwenLM/qwen-code/pull/11206)
   为工作区引入持久化的 Agent 身份，支持共享线程上的人员与 Agent 协同工作：创建/分配任务、多 Agent 寻址、进程干预、结果审查、取消、阻塞解决和已审阅线程标记。大型功能，daemon 方向核心 PR。

2. **feat(core): 为 deferred tools 保留 prompt cache** — [#10410](https://github.com/QwenLM/qwen-code/pull/10410)
   以 `tool_search` + `tool_call` 两步桥接替代直接 schema 暴露，模型可审查 deferred tool schema 而不改变声明工具列表，同时在现有执行管线中校验和调用。对长会话 token 成本优化意义重大。

3. **fix(cli): 恢复 OpenTUI banner、footer 和 loading 状态** — [#11437](https://github.com/QwenLM/qwen-code/pull/11437)（已合并）
   修复 OpenTUI 下缺失的终端 UI 元素，同时包含 OSS 镜像发版修复。与 #8662 迁移方向一致。

4. **feat(sessions): 记录会话注册类型并完善注册契约与文档** — [#11463](https://github.com/QwenLM/qwen-code/pull/11463)
   会话注册记录新增 `kind` 字段（`tui`/`headless`/`serve`/`external`），为后续无头模式和外部注册方铺路。

5. **feat(web-shell): 从工作区分支选择器管理 git remote** — [#11163](https://github.com/QwenLM/qwen-code/pull/11163)
   在 Web Shell 的 git popover 中新增 Manage Remotes 面板，支持列出、添加、删除 remote（删除需二次确认），补全 Web 端 Git 操作能力。

6. **feat(web-shell): 已答问题在 Processed 摘要之外保持可见** — [#11461](https://github.com/QwenLM/qwen-code/pull/11461)
   AskUserQuestion 完成后的结果以结构化气泡保留（问题在上、答案在下），支持多行文本和字面代码，且不计入 Processed 的工具计数。

7. **feat: 支持 GPT-5 和 GPT-6 reasoning effort 配置** — [#11295](https://github.com/QwenLM/qwen-code/pull/11295)（已合并）
   为已知 GPT-5 和 GPT-6 Astra 模型添加 reasoning effort 配置，统一处理 provider 前缀、路由标签、空白字符和快照版本等归一化逻辑。

8. **fix(dws): 强制禁用聊天源** — [#11355](https://github.com/QwenLM/qwen-code/pull/11355)
   让 DingTalk Workspace 的群聊和单聊访问策略成为真正的源级开关：不订阅、不轮询历史、不通过迟到事件回调放行、不从持久化挂起工作中重放。

9. **feat(core): 扩展 Kimi、Qwen 和 DeepSeek reasoning 预设** — [#11349](https://github.com/QwenLM/qwen-code/pull/11349)
   为 Moonshot K3（low/high/max）、K2.7 Code（thinking-only）、K2.6（原生 thinking 开关）、Qwen 3.8（low/medium/xhigh）、DeepSeek V4 Pro 等模型补齐 reasoning 预设。

10. **feat(web-shell): 增加 Web 预览面板及保存投递历史** — [#11276](https://github.com/QwenLM/qwen-code/pull/11276)
   支持对浏览器可达的开发 URL 提供桌面/移动宽度预览、刷新和外部打开。Standalone Web Shell 默认启用，embedded host 可 opt-in。

## 功能需求趋势

- **Web Shell 成为功能主战场**：品牌定制（[#11357](https://github.com/QwenLM/qwen-code/issues/11357)）、URL 可点击、Git remote 管理、Web 预览面板、已答问题可见性等密集交付，Web Shell 正在从基础终端逐步演进为完整 IDE 形态。
- **daemon 架构解耦与文档化**：Skill 管理从 child 解耦（[#11274](https://github.com/QwenLM/qwen-code/issues/11274)）、REST/SSE API 文档整合（[#11359](https://github.com/QwenLM/qwen-code/issues/11359)）、自定义 Web Shell 托管（[#11358](https://github.com/QwenLM/qwen-code/issues/11358)）、外部持久化讨论（[#11440](https://github.com/QwenLM/qwen-code/issues/11440)），说明第三方集成需求正在快速增长。
- **新模型与新能力接入**：GPT-5/6 reasoning（[#11295](https://github.com/QwenLM/qwen-code/pull/11295)）、Kimi/DeepSeek presets（[#11349](https://github.com/QwenLM

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

⚠️ 摘要生成失败。

</details>