# AI CLI 工具社区动态日报 2026-07-31

> 生成时间: 2026-07-31 01:26 UTC | 覆盖工具: 9 个

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

**报告日期：2026-07-31** | **数据窗口：过去 24 小时**


## 1. 生态全景

当前 AI CLI 工具赛道已进入**规模化落地的阵痛期**——头部工具（Claude Code、Codex、Gemini CLI）不再以功能叠加为核心竞争点，而是被**后台任务资源治理**与**跨平台稳定性**两大基础问题牵制：Claude Code 因 TaskStop 不彻底导致单次事故烧掉 75 万 tokens，Codex 在 Windows 平台高频崩溃，Gemini CLI 的子代理误报成功与无限挂起直接侵蚀用户信任。与此同时，**安全与隐私意识显著升级**（凭据泄漏、内存存储、脱敏时序），**Agent 行为的可观测性与可配置性**成为社区最高频的共性诉求。新玩家（Qwen Code、Kimi、CodeWhale）持续在产品化进程上加速追赶，但市场分层格局已基本清晰：头部拼可靠性、中部拼体验、尾部拼差异化。


## 2. 各工具活跃度对比

| 工具 | Issues 数（24h） | PR 数（24h） | Release 状态 | 社区规模信号（Top Issue 👍） |
|---|---|---|---|---|
| **Claude Code** | 10 条精选（总量较大） | 1（已关闭，无价值） | 无新版本（v2.1.220） | 530（多账户请求） |
| **Codex** | 10 条精选 | 10（8 关闭 / 2 开放） | 无新版本 | 66（OAuth 认证失败） |
| **Gemini CLI** | 10 条精选 | 10（3 关闭 / 7 开放） | v0.55.0-nightly（纯版本号） | 8（通用代理挂起） |
| **Copilot CLI** | 10 条精选 | 0 | **v1.0.77**（功能更新） | — |
| **Qwen Code** | 10 条精选 | 10（含合并） | v0.21.1-nightly（CI 修复） | 1（多数 issue 👍 较少） |
| **Pi** | 11 条 | 10+（6 已合入） | 未发布新版本 | 4（登录挂起） |
| **Kimi Code** | 3 条 | 1（修复） | 无新版本 | 0（记忆系统请求） |
| **CodeWhale** | 10 条 | 10（8 合并 / 2 开放） | **v0.9.2**（品牌更名） | — |
| **OpenCode** | 10 条 | 10（6 开放 / 4 关闭） | **v1.18.10**（功能更新） | 10（GPT-5.6 Sol 过载） |

> 注：Claude Code、Copilot CLI、CodeWhale 未提供完整 Issue/PR 总量数据，仅列精选数。


## 3. 共同关注的功能方向

### 3.1 后台任务资源治理（呼声最高）

| 工具 | 具体诉求 | 代表 Issue |
|---|---|---|
| **Claude Code** | TaskStop 不彻底、token 失控计费、任务 ID 跨会话不可解析 | #82104 / #77730 |
| **Gemini CLI** | 子代理达到 MAX_TURNS 后误报成功、通用代理无限挂起 | #22323 / #21409 |
| **Copilot CLI** | 任务完成后会话仍在消耗 AI 额度（97.8% 被消耗） | #4308 / #4309 |
| **OpenCode** | GPT-5.6 Sol 服务器持续过载 | #39653 |

**共性本质**：后台执行机制的停止语义、资源上限、会话恢复与用量可见性，已成为所有工具规模化使用的共同瓶颈。

### 3.2 Windows 平台稳定性

| 工具 | 具体问题 | 代表 Issue |
|---|---|---|
| **Codex** | 桌面应用崩溃（0xC0000005）、VS Code diff 视图崩溃、沙箱执行失败 | #32683 / #35362 / #35481 |
| **Qwen Code** | 0.21.1 三次崩溃、桌面端 LM Studio 无响应、npm 安装 16 位错误 | #7972 / #8146 |
| **Gemini CLI** | 浏览器代理在 Wayland 下失败 | #21983 |
| **Pi** | TUI 输入行逐字符重绘 | #6300 |
| **OpenCode** | npm 安装 16 位兼容性错误 | #37628 |

### 3.3 MCP 生态与认证链路

| 工具 | 具体问题 | 代表 Issue |
|---|---|---|
| **Codex** | MCP 工具在自定义模型端点不可调用、Slack MCP 登录失败 | #26234 / #13200 |
| **Gemini CLI** | MCP OAuth 令牌刷新失败 | #28481（PR） |
| **Copilot CLI** | MCP 工具参数 `anyOf` 联合类型被错误字符串化 | #4301 |

### 3.4 Hook / 扩展机制可靠性

| 工具 | 具体问题 | 代表 Issue |
|---|---|---|
| **Claude Code** | Pre/PostToolUse Hooks 完全不触发（持续近一年） | #6305 |
| **Kimi Code** | fire-and-forget 钩子被 GC 意外回收 | #2565（PR） |
| **Gemini CLI** | 子代理在配置禁用状态下仍被调用 | #22093 |

### 3.5 配置系统可预测性

- **Claude Code**：`--agents` 静默吞非法 JSON（#79527）
- **Gemini CLI**：settings 占位符解析时序竞态（PR #28597）
- **CodeWhale**：配置路径 Windows/Cygwin 解析规则分裂（#2369）
- **Qwen Code**：worktree settings.json 错误写入项目根目录（#8138）


## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线特征 | 当前阶段关键词 |
|---|---|---|---|---|
| **Claude Code** | Anthropic 官方旗舰 CLI | 深度 Claude 用户、企业级 Max 订阅者 | 深度整合 Claude 模型能力（skills、子代理、Cowork 桌面端），强调 Agent 自主性 | **后台治理**、桌面端稳定性 |
| **Codex** | OpenAI 官方 CLI | ChatGPT Pro/Enterprise 用户 | 与 ChatGPT 生态深度绑定，MCP 支持 + 沙箱执行 + Code Review 集成，多模型路由 | Windows 补课、MCP 兼容性 |
| **Gemini CLI** | Google 官方 CLI | Gemini 模型用户、多 provider 使用者 | 强调沙箱安全、AST 感知代码理解（探索）、Auto Memory 自动记忆，架构上重评估与可观测性 | 子代理可靠性、安全细节 |
| **GitHub Copilot CLI** | GitHub 生态 CLI | GitHub 重度用户、企业合规场景 | 与 GitHub 生态深度集成，v1.0.77 引入浏览器 OAuth 流程与 `Ctrl+G` 编辑增强 | 额度透明化、回归控制 |
| **OpenCode** | 开源中立 CLI | 追求开源+自托管的技术团队 | 强调模型提供商中立（Pi/Codex/GPT-5.6/Ollama 全支持）、插件扩展体系活跃、桌面端/TUI 并行迭代 | 快速迭代、多端一致 |
| **Qwen Code** | 阿里 Qwen 官方 CLI | Qwen 模型用户、Windows 开发者 | 双模型路由（Qwen + 替代模型）、Agent Team 协作、Web Shell 落地桌面端（Tauri） | 产品化、Windows 适配 |
| **Pi** | 极客向开源 TUI | 终端重度用户、多 provider 高级玩家 | 轻量级 Node.js TUI、扩展 API 深化（Markdown 渲染 API）、远程会话线协议（#7344）、SDK 化 | 协议一致性、嵌入式场景 |
| **Kimi Code** | 月之暗面官方 CLI | Kimi 模型用户、中文开发者 | 轻量级 CLI，聚焦核心体验，社区规模尚小 | 功能补全（记忆系统） |
| **CodeWhale** | 开源终端代理（原 DeepSeek-TUI） | Rust 生态开发者、自托管用户 | Rust 技术栈、TUI 单 crate 膨胀导致编译慢、v0.9.3 架构重构中 | 架构重构、品牌重塑 |


## 5. 社区热度与成熟度

### 第一梯队：高热度、高活跃、被基础问题牵制

- **Claude Code**：社区规模最大（多账户请求 👍 530），讨论深度最高，但**后台任务与 Cowork 稳定性**问题已持续多月未解，周度结论直言"阻碍用户规模化使用"。
- **Codex**：PR 活动最密集（10 条），社区活跃度高，但 **Windows 平台是明显短板**，多条高赞 issue 集中在崩溃与兼容性。

### 第二梯队：迭代快、社区快速增长

- **OpenCode**：发布节奏最快（v1.18.10），PR 响应迅速，社区对升级回归有不满但认可修复速度。当前处于**功能扩张期**。
- **Gemini CLI**：P1 级 Issue 集中在子代理可靠性，安全类 PR 密集（Docker 升级、MCP OAuth 修复），说明维护者将安全置于优先。社区活跃但规模不及前两者。
- **Pi**：**技术含量最高**的社区之一（远程协议线、SDK schema 共享），PR 合入率高、质量扎实，处于**平台化深化期**。

### 第三梯队：产品化早期 / 小众

- **Copilot CLI**：刚发布 v1.0.77 引入浏览器 OAuth，社区反馈活跃（额度问题、回归 bug），正处于**从工具到平台的能力建设期**。
- **Qwen Code**：**产品化加速度最快**（桌面端、Windows 适配），但社区参与度（👍 普遍偏低）说明仍处于早期用户积累阶段。
- **Kimi Code**：社区规模最小，也最"安静"——1 天内仅 3 条 Issue、1 条 PR，但**记忆系统功能提案已持续 5 个月**，说明用户有明确期待但社区表达动力不足。
- **CodeWhale**：属于**技术型社区**，核心讨论围绕架构重构（14,878 行 main.rs）与编译耗时，非功能需求为主。品牌更名（deepseek-tui → CodeWhale）后仍处于过渡期。


## 6. 值得关注的趋势信号

### 趋势一：后台任务治理 = 新的差异化战场

Claude Code（75 万 token 事故）、Copilot CLI（97.8% 额度空耗）、Gemini CLI（子代理挂起）三家同时在此折戟。**"停止语义 + 资源上限 + 实时可见性 + 会话恢复"** 四项能力将成为下一阶段 Agent 平台的标配。

**参考价值**：如果你是平台建设者，建议在架构设计阶段就将任务生命周期管理（暂停/恢复/终止/计费）纳入核心抽象，而非事后打补丁。

### 趋势二：Windows 不再是"次要平台"

Codex 在 Windows 桌面崩溃、Qwen Code 的 Windows 崩溃、OpenCode 的 npm 安装错误、Pi 的逐字符重绘——几乎所有工具的 Windows 反馈都在上升。**Windows 开发者已构成不可忽视的用户基数**，平台支持质量将直接影响工具的市场渗透率。

**参考价值**：跨平台策略应从"能用"升级为"原生体验"，尤其在桌面端与 IDE 集成场景。

### 趋势三：MCP 生态互操作成为新瓶颈

MCP 已从"新奇功能"变为"基础设施"，但**认证链路**（Slack 动态注册、OAuth issuer 验证）与**工具序列化兼容性**（namespace 格式、`anyOf` 类型）问题频发。MCP 服务器开发者的适配成本正在成为生态扩散的阻力。

**参考价值**：如果团队在构建 MCP 服务器，建议优先支持标准的 OAuth 动态注册流程，并确保工具 schema 遵循规范序列化。

### 趋势四：从"上下文管理"到"上下文预算"

Claude Code 的内置 skill 无条件膨胀上下文（77%）、Gemini CLI 的 Auto Memory 无限重试、Copilot CLI 的 128K 回退、Qwen Code 的 Context Diet——**上下文已从技术细节上升为成本与体验的核心变量**。工具正在从"压缩"走向"预算化分配"。

**参考价值**：选择工具时，关注其对长会话的处理策略（自动压缩、技能按需加载、token 可见性），这直接决定使用成本。

### 趋势五：安全机制需要"不误伤"

Codex 的 cybersecurity 误报（#34306）、OpenCode 的 Plan 模式可绕过（#39491）、Qwen Code 的凭据泄漏（#8136）——**安全机制正在从"有"走向"准"**。过于粗糙的安全拦截反而损害信任。

**参考价值**：安全策略的设计需要平衡拦截与误报，清晰的错误信息与"用户可解释的拦截原因"是底线。

### 趋势六：Agent 行为透明度 = 信任基础

Gemini CLI 的子代理误报成功（#22323）、Copilot CLI 的子代理无响应（#4293）、Claude Code 的后台任务 ID 不可解析——**"Agent 做了什么、为什么这么做、现在进行到哪一步"** 的可观测性，正在成为用户评估工具可靠性的第一标准。

**参考价值**：无论你是在选型还是在自建 Agent 平台，请把"完整轨迹可追溯"作为非功能需求的最高优先级。

---

*本报告基于各工具 GitHub 仓库公开数据，数据窗口为 2026-07-31 前 24 小时。Issue/PR 编号与链接均附于各工具动态摘要中，可直接跳转查看详情。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-07-31）

## 一、热门 Skills 排行（Top 7 PR）

| 排名 | Skill / 主题 | 作者 | 状态 | 一句话定位 |
|------|-------------|------|------|-----------|
| 1 | **skill-creator 核心缺陷修复**（#1298，引用 #556/#1099/#1050/#1323/#1261） | MartinCajiao 等多人 | 🟡 Open | **社区最痛点**：`run_eval.py` 在 Windows 与平行执行下触发检测失效，导致召回率恒为 0%，优化循环在噪声上迭代 |
| 2 | **document-typography**（#514） | PGTBoos | 🟡 Open | 排版质量门控：AI 生成文档的孤行/孤词/编号对齐问题，直击所有生成文档的质量下限 |
| 3 | **color-expert**（#1302） | meodai | 🟡 Open | 自包含色彩专家：ISCC-NBS、Munsell、OKLCH/OKLAB 选型表等多套命名体系 + 色彩空间选择决策表 |
| 4 | **ODT（OpenDocument）支持**（#486） | GitHubNewbie0 | 🟡 Open | ODT/ODS 文件创建、模板填充、解析转 HTML，覆盖企业级文档互操作刚需 |
| 5 | **pyxel 复古游戏开发**（#525） | kitao | 🟡 Open | 基于 pyxel-mcp 的像素/8-bit 游戏工作流：编写 → 运行截图 → 检查 → 迭代 |
| 6 | **testing-patterns**（#723） | 4444J99 | 🟡 Open | 完整测试方法论：Testing Trophy 模型 + 单元/组件/E2E 测试模式与反模式 |
| 7 | **self-audit 四维推理质量门控**（#1367） | YuhaoLin2005 | 🟡 Open | 交付前机械验证 + 按危害优先级排序的推理审计（与 #1385 Issues 呼应） |

> 说明：**所有热门 PR 均处于 Open 状态**，合并速度是当前生态最大瓶颈。`#1298` 实际是多个 PR 集合（#1099、#1050、#1323、#1261）共同指向同一缺陷的不同修复方案，社区活跃度极高但方案碎片化。

---

## 二、社区需求趋势（Issues 方向提炼）

| 方向 | 代表 Issue | 热度 | 信号强度 |
|------|-----------|------|---------|
| **生态治理 / 信任安全** | #492 社区技能冒用 `anthropic/` 命名空间的信任边界滥用 | 43 评论，🔥 最热 | 强：命名空间治理迫在眉睫 |
| **组织级技能共享** | #228 org 内直接共享技能库，而不是手动下载发送 | 16 评论，8 👍 | 强：企业采用的基础设施缺口 |
| **核心工具稳定性** | #556 run_eval 触发率 0%（多用户复现）| 12 评论，7 👍 | 极强：开发者工具链自身质量拖累生态 |
| **上下文窗口管理** | #1487 `claude-api` 技能一次注入 ~156k tokens | 4 评论 | 中：技能体积设计规范缺失 |
| **安全与权限设计** | #1175 SharePoint 文档的访问控制与上下文安全 | 4 评论 | 中：企业场景安全模式需求 |
| **跨平台兼容** | #1061 Windows subprocess/编码/select 管道 | 3 评论 | 中：Windows 是第二大用户群 |

---

## 三、高潜力待合并 Skills（评论活跃、尚未落地）

| PR # | 内容 | 评论数 | 潜力判断 |
|------|------|-------|---------|
| **#1298**（多 PR 聚合） | skill-creator 全平台修复 | ⭐⭐⭐⭐⭐ | 若合并将**一次性修复 10+ 独立复现的核心 bug**，是当前最高的杠杆点 |
| **#538** | pdf skill 大小写敏感路径修复 | ⭐⭐⭐ | 一步到位解决 Linux/CI 环境文件引用断裂 |
| **#541** | docx 追踪修订 w:id 碰撞修复 | ⭐⭐⭐ | 修复真实文档损坏场景，企业文档场景直接受益 |
| **#509** | CONTRIBUTING.md 贡献指南 | ⭐⭐⭐ | 补齐社区从 25% 健康度到可协作的基建缺失 |
| **#1367** | self-audit 质量门控（经 #1385 Proposal 验证） | ⭐⭐ | 作者提供完整 Proposal + 产品化思维，Landed 概率较高 |

---

## 四、Skills 生态洞察

> **生态核心矛盾是"自举失败"**：skill-creator 自身的评估工具在 Windows 和并行场景下失灵（recall=0%），直接阻塞了社区所有 skill 的质量迭代；与此同时，**"质量门控 + 信任安全"是社区最集中的新诉求**——从 self-audit 提案到命名空间冒用 Issue，社区在从"写 skill"转向"管 skill"演进，而工具链的稳定性（`run_eval.py`）是这一切的前提条件。

---

# Claude Code 社区动态日报 — 2026-07-31

> 数据来源：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)


## 今日速览

今日社区讨论热度集中在**后台任务资源失控**（TaskStop 未终止子代理、后台任务 token 失控计费）与 **Cowork 桌面端回归**（内核崩溃与数据丢失）两大方向。此外，`--agents` 参数静默接受非法 JSON 及 hook 系统失效等 bug 持续引发关注。未发布新版本。


## 版本发布

过去 24 小时无新版本发布（最新版本号约 v2.1.220）。


## 社区热点 Issues（10 条精选）

**1. TaskStop 未终止子代理，杀死后仍计费 75 万 tokens**
[#82104](https://github.com/anthropics/claude-code/issues/82104) · `simplysdm` · 评论 2 · 👍 0
三个缺陷叠加导致子代理失控：`TaskStop` 只停父代理、子代理继续跑到完并持续计费；期间无实时用量可见性；无上限保护。一次事故中父代理暂停后仍被消耗 75 万 tokens。后台任务资源治理已成为社区最尖锐的痛点。

**2. Cowork 回归：Windows 内核堆损坏，高优先级**
[#72377](https://github.com/anthropics/claude-code/issues/72377) · `mmoorhead-rsa` · 评论 1 · 👍 0
`KERNEL_MODE_HEAP_CORRUPTION (0x13A)` in `storvsp!VspVsmbFileCreate`，从 build 1.15962.0 引入，1.15962.1.0 仍未修复。标记为 high-priority + regression，影响 Windows 用户的 Cowork 稳定性。

**3. 自动更新清空 Cowork 会话磁盘数据**
[#43719](https://github.com/anthropics/claude-code/issues/43719) · `brandonup` · 评论 5 · 👍 2
Auto-update 触发后用户 Cowork 项目数据丢失，用户请求恢复数据。带 `data-loss` 与 `regression` 标签，涉及桌面端核心数据安全，持续多月仍未解决。

**4. Cowork GitHub 连接器不可用：OAuth DCR 不支持、UI 误导、Disconnect 按钮失效**
[#59854](https://github.com/anthropics/claude-code/issues/59854) · `nathanpancakelegion` · 评论 5 · 👍 12
三个问题叠加使得 GitHub 连接器完全不可用。点赞数达 12，是今日 issue 中社区共鸣度最高的一条。涉及 auth、MCP、Cowork 三个核心区域。

**5. 后台代理与任务 ID 跨会话身份边界无法解析**
[#77730](https://github.com/anthropics/claude-code/issues/77730) · `simplysdm` · 评论 7
后台代理 transcripts 无法恢复，只能被迫全上下文重建（token 烧钱）。Max 订阅者反馈，涉及 v2.1.209 与 Fable 5 模型主循环。与 #82104 同一作者的持续反馈，说明后台执行机制的稳定性已严重不足。

**6. Pre/PostToolUse Hooks 完全未执行（macOS）**
[#6305](https://github.com/anthropics/claude-code/issues/6305) · `fwends` · 评论 38 · 👍 16
老 issue 但今日仍有活跃讨论。`settings.local.json` 配置的 hook 完全不触发，已持续近一年，评论数 38、👍 16，是 hooks 体系最受关注的问题之一。

**7. /claude-api 内置 skill 无条件饱和上下文，中性提问也触发 77% 飙升**
[#63566](https://github.com/anthropics/claude-code/issues/63566) · `larsgoolsen` · 评论 6 · 👍 7
一个中性问题导致上下文暴涨 77%。Windows 平台 + skills 区域，说明内置 skill 缺乏按需加载机制，上下文管理策略需要优化。

**8. 自动压缩丢弃 PreToolUse 读状态，多文件编辑触发无限重读循环**
[#68709](https://github.com/anthropics/claude-code/issues/68709) · `gtapps` · 评论 4（已关闭，标记 stale）
`Edit` 工具要求先 `Read` 目标文件。当多文件读取触发自动压缩时，读过状态被丢弃，导致无限重读。属核心工具的典型边界案例。

**9. 内置 ugrep 正则搜索 64KB 文件分配 4-17 GB 内存**
[#78834](https://github.com/anthropics/claude-code/issues/78834) · `Helban` · 评论 3
当模式含有尾部 `.{N}` 约束且内部有 `.{0,M}` 变量边界时，ugrep 以 ~230 MB/s 持续分配内存数十秒。Linux/WSL2 上 v2.1.214 复现，附有 repro。属性能/内存区域的严重缺陷。

**10. /fork 在 --dangerously-skip-permissions 模式下被阻止**
[#79575](https://github.com/anthropics/claude-code/issues/79575) · `Butanium` · 评论 1
提示信息称 "fork would run with fewer restrictions"，但该模式下 fork 本就以更少限制运行，拦截逻辑自相矛盾。CLI 权限模型的逻辑漏洞。


## 重要 PR 进展

过去 24 小时仅 1 条 PR 更新：

**[#82555](https://github.com/anthropics/claude-code/pull/82555)（已关闭）** — `batuhunca-del` 提交的 YouTube/Instagram MCP 相关 PR，已关闭，无实质合并价值。近期 PR 活动极低，开发重点可能转向内部 milestone。


## 功能需求趋势

从全部 Issues 中提炼的社区最关注方向：

1. **后台任务资源治理（最突出）**
   TaskStop 不够彻底（#82104）、后台任务 ID 跨会话不可解析（#77730）、调度型一次性任务 6 个全失败（#82728）、token 无上限保护 —— 后台执行机制的系统性重构已是社区最高呼声。

2. **多账户支持（热度最高）**
   [#36151](https://github.com/anthropics/claude-code/issues/36151) 请求在移动端实现多账户切换（无需共享邮箱），👍 530、评论 148，是当前社区规模最大的功能请求。移动端 + 账户体系是明确方向。

3. **子代理/自定义 agent 配置增强**
   [#78217](https://github.com/anthropics/claude-code/issues/78217) 请求子代理模型的受管默认配置；[#69391](https://github.com/anthropics/claude-code/issues/69391) 请求 agent frontmatter 支持 blocking 字段（对齐 skills 能力）——agent 体系可配置性持续被需要。

4. **数据安全与隐私**
   [#82734](https://github.com/anthropics/claude-code/issues/82734) 请求后台任务输出支持纯内存存储，防止敏感数据落盘——安全敏感型用户的新需求。

5. **插件与主题体验**
   自定义主题在 `/rename` 后被重置（#80712）、LaTeX 公式在 VSCode 扩展中不渲染（#82758）——核心功能之外的体验细节问题持续积累。


## 开发者关注点

| 痛点/需求 | 代表 Issue | 频率 |
|---|---|---|
| **后台任务不可控**：kill 不彻底、ID 不可解析、token 失控计费 | #82104、#77730、#82728 | ★★★ 极高 |
| **Cowork 桌面端稳定性**：内核崩溃、数据丢失、连接器不可用、iOS 自动归档会话 | #72377、#43719、#59854、#71616 | ★★★ 极高 |
| **环境变量/配置静默失效**：`CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` 7/14 后变 no-op | #82761 | ★★ 高 |
| **CLI 参数一致性**：`--agents` 静默吞掉非法 JSON，而 `--settings`/`--mcp-config` 会报错 | #79527 | ★★ 高 |
| **Hooks 执行不稳定**：Pre/PostToolUse 不触发、已禁用插件仍运行 hooks | #6305、#68020 | ★★ 高 |
| **上下文管理缺陷**：自动压缩丢读状态致无限循环、技能无条件膨胀上下文 | #68709、#63566 | ★★ 高 |
| **网络/代理层故障**：调度任务 CONNECT 403、macOS 后台任务断 VPN 后 DNS/TLS 失效 | #82760、#82756 | ★ 中 |
| **模型行为问题**：幻觉要求并拒绝生产部署、对无害 3D 模型请求误报内容策略违规 | #82757、#82755 | ★ 中 |

**周度核心结论**：后台任务执行机制的可靠性（停止语义、资源上限、会话恢复）与 Cowork 桌面端的稳定性是当前阻碍用户规模化使用的主要障碍。建议 Anthropic 优先处理 `data-loss` 和 `high-priority` 标签下的回归问题，并尽快为后台任务引入硬性 token 上限与实时用量可见性。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-07-31**


## 今日速览

今日 Codex 仓库无新版本发布，社区焦点集中在 **Windows 平台稳定性问题**（桌面应用崩溃、沙箱执行失败、VS Code 扩展 diff 视图错误）以及 **CLI 与自定义模型 / MCP 工具的兼容性** 上。OAuth 认证失败的 Issue 持续高热（👍66 / 评论31），成为当前最受关注的 bug；同时，多个 PR 在推进 app-server 协议优化与沙箱事件规范化，为底层稳定性打基础。


## 社区热点 Issues（Top 10）

### 1. OAuth 认证在 issuer 验证阶段失败
- **Issue**: [#31573](https://github.com/openai/codex/issues/31573) | 👍 66 | 💬 31
- **状态**: OPEN | 标签: `bug`, `auth`, `mcp`, `CLI`
- **摘要**: Codex CLI v0.143.0（Free 订阅）在 OAuth 认证流程中，issuer 验证失败，导致无法完成登录。此问题影响面广，是当前社区反馈最激烈的认证相关问题。

### 2. [Windows] 桌面应用在 Browser Use 打开页面时崩溃（0xC0000005）
- **Issue**: [#32683](https://github.com/openai/codex/issues/32683) | 👍 8 | 💬 29
- **状态**: OPEN | 标签: `bug`, `windows-os`, `app`, `browser`
- **摘要**: ChatGPT Pro (20x) 用户在 Windows 上使用 Browser Use 功能时，Codex App 在 `chrome.dll` 中触发访问冲突崩溃，复现稳定。Windows 用户受影响严重。

### 3. 非 OpenAI Responses API 提供商下 MCP 工具无法被模型调用
- **Issue**: [#26234](https://github.com/openai/codex/issues/26234) | 👍 40 | 💬 27
- **状态**: OPEN | 标签: `bug`, `mcp`, `CLI`, `custom-model`, `aws-bedrock`
- **摘要**: 当 Codex 连接 Ollama、LM Studio、OpenRouter 或 AWS Bedrock 等非 OpenAI 端点时，MCP 工具以 `{"type": "namespace", ...}` 格式序列化后，模型无法识别和调用。社区对自定义模型 + MCP 组合的需求强烈，此兼容性问题呼声很高。

### 4. Windows 桌面版拼写检查“No Guesses Found”
- **Issue**: [#26478](https://github.com/openai/codex/issues/26478) | 👍 25 | 💬 18
- **状态**: OPEN | 标签: `bug`, `windows-os`, `app`
- **摘要**: Windows 桌面版检测到拼写错误，但上下文菜单不显示任何替换建议（即使系统原生拼写检查工作正常）。影响日常输入体验，反馈持续累积。

### 5. Slack 官方 MCP 登录失败：Dynamic client registration not supported
- **Issue**: [#13200](https://github.com/openai/codex/issues/13200) | 👍 58 | 💬 10
- **状态**: OPEN | 标签: `bug`, `mcp`
- **摘要**: `codex mcp login` 在连接 Slack 官方 MCP 服务器时失败，报错 `Dynamic client registration not supported`。高赞低评论，说明问题明确且广泛影响 Enterprise 用户。

### 6. [VS Code] 代码审查完整 diff 页面崩溃，内联 diff 正常
- **Issue**: [#35362](https://github.com/openai/codex/issues/35362) | 👍 13 | 💬 10
- **状态**: OPEN | 标签: `bug`, `code-review`, `windows-os`, `extension`
- **摘要**: VS Code 扩展（Windows 10 x64）中，打开完整 Review diff 页面时崩溃；内联 diff 功能正常。代码审查是高频场景，此问题直接影响核心工作流。

### 7. VS Code Diff 视图报错 “Oops, an error has occurred”
- **Issue**: [#35481](https://github.com/openai/codex/issues/35481) | 👍 31 | 💬 6
- **状态**: OPEN | 标签: `bug`, `code-review`, `windows-os`, `extension`
- **摘要**: VS Code 扩展 v26.721.41059 中，打开 Codex Diff 视图时内容无法显示并报错。与 #35362 呼应，表明 Windows 上 diff 功能存在系统性缺陷。

### 8. `gpt-5.6-luna` 被标记为 MultiAgent V1，导致 V2 `spawn_agent` 拒绝
- **Issue**: [#35097](https://github.com/openai/codex/issues/35097) | 👍 13 | 💬 6
- **状态**: OPEN | 标签: `bug`, `CLI`, `subagent`
- **摘要**: CLI v0.145.0 中，`gpt-5.6-luna` 被错误标记为 MultiAgent V1，当 V2 的 `spawn_agent` 调用时被拒绝。影响子代理（subagent）功能使用。

### 9. 桌面端推理级别（reasoning level）在同线程中自动降级
- **Issue**: [#26930](https://github.com/openai/codex/issues/26930) | 👍 1 | 💬 8
- **状态**: OPEN | 标签: `bug`, `app`, `subagent`, `session`
- **摘要**: macOS 桌面版在委派或继续对话后，推理级别从 `xhigh/high` 自动重置为 `low`，且无法恢复。影响长会话中的模型行为一致性。

### 10. 安全审查误拦截正常请求（cybersecurity 误报）
- **Issue**: [#34306](https://github.com/openai/codex/issues/34306) | 👍 5 | 💬 7
- **状态**: OPEN | 标签: `bug`, `CLI`, `safety-check`
- **摘要**: CLI v0.144.6（Linux, gpt-5.6-sol-xhigh）在非恶意请求时触发 "This content can't be shown" / "We take extra caution with cybersecurity requests" 错误。安全机制误判导致正常开发中断，用户困惑度较高。


## 重要 PR 进展（Top 10）

### 1. 在独立 host 中运行 code mode（专有运行时）
- **PR**: [#36217](https://github.com/openai/codex/pull/36217) | CLOSED
- **摘要**: 将 V8 实现移至独立的 `codex-code-mode-runtime` crate，由 `codex-code-mode-host` 统一管理，移除 Codex 主进程中的嵌入式运行时回退。架构更清晰，便于后续维护与发布。

### 2. 支持 Enterprise 自动化账号套餐
- **PR**: [#36228](https://github.com/openai/codex/pull/36228) | CLOSED
- **摘要**: 识别 `enterprise_cbp_automation` 为 Enterprise 工作区套餐，并在认证、后端响应、app-server 账户与速率限制 API 中暴露该套餐信息，协议 schema 同步更新。

### 3. 保留 read 命令操作中的执行器路径
- **PR**: [#36223](https://github.com/openai/codex/pull/36223) | CLOSED
- **摘要**: 当所选环境使用与 app-server 宿主机不同的路径约定时，read 命令操作此前被忽略；现修复为客户端可引用执行器文件系统中的路径，而非宿主机路径。

### 4. 忽略 rollout 项目协调时的透传元数据
- **PR**: [#36221](https://github.com/openai/codex/pull/36221) | CLOSED
- **摘要**: 在 rollout 追踪规范化前移除模型条目中的顶层 `internal_chat_message_metadata_passthrough`，确保重放的工具调用和输出复用现有会话条目，避免重复创建。

### 5. 在外部 Agent 检测中暴露连接器候选
- **PR**: [#36218](https://github.com/openai/codex/pull/36218) | CLOSED
- **摘要**: `ExternalAgentConfigDetectResponse` 新增 `connectors` 数组，包含每个候选连接器的归一化名称、检测到的会话数和检测来源（远程 MCP 服务器配置等）。

### 6. exec-server：路由远程网络策略决策
- **PR**: [#31458](https://github.com/openai/codex/pull/31458) | OPEN（已 code-review）
- **摘要**: 将执行器本地代理策略未命中回传至进程级核心策略决策器；保留 Guardian 决策的环境/执行/命令/工具调用归因；并发决策相互关联，在断连、进程退出等异常时自动 fail-closed。

### 7. 核心：添加无工具线程模式（tool-free）
- **PR**: [#31922](https://github.com/openai/codex/pull/31922) | OPEN
- **摘要**: 新增可选 `tool_free` 特性，用于轻量级辅助线程（如线程标题生成）。此类会话跳过 MCP 启动/刷新、技能/插件/工具枚举，并强制空工具路由，降低开销。

### 8. 为 Codex Apps 启用并行工具调用
- **PR**: [#31591](https://github.com/openai/codex/pull/31591) | OPEN
- **摘要**: 新增默认关闭的 `codex_apps_parallel_tool_calls` 特性；启用后 host 所有的 `codex_apps` MCP 服务器可使用并行工具调用，用户配置的第三方 MCP 服务器保持原行为。

### 9. 记录规范化沙箱违规事件
- **PR**: [#36207](https://github.com/openai/codex/pull/36207) | CLOSED
- **摘要**: 统一文件系统拒绝和托管网络拦截的事件结构，形成标准化的沙箱违规事件格式，下游消费者无需再自行解析各类后端输出。

### 10. 避免流式输出缓冲区中的字节搬移
- **PR**: [#36194](https://github.com/openai/codex/pull/36194) | CLOSED
- **摘要**: 优化统一 exec 输出的解码路径，避免逐条删除 `Vec` 前缀导致的全量字节搬移。对于含大量无效 UTF-8 或单条 relay 记录中多帧消息的流，性能显著提升。


## 功能需求趋势

1. **Windows 桌面应用稳定性**：多条高优 bug（崩溃、沙箱失败、diff 崩溃）均集中在 Windows 平台，社区对 Windows 稳定性的诉求迫在眉睫。
2. **MCP 生态兼容性**：MCP 工具在非 OpenAI 端点不可调用（#26234）、Slack MCP 登录失败（#13200）、MCP namespace 序列化问题持续讨论，自定义模型与第三方工具链组合是重点方向。
3. **IDE 集成深度**：VS Code 扩展相关 Issue 频繁（diff 崩溃、通知支持 #26555），开发者期望 Codex 深度融入 IDE 工作流，并将通知接入 VS Code 原生 UI。
4. **新模型支持与路由正确性**：`gpt-5.6-luna` 的 MultiAgent V1/V2 误标（#35097）、子代理恢复时使用父模型与推理级别（#34821）等，表明社区对多代理架构与模型切换的精确控制有较高期望。
5. **会话管理与资源优化**：fork 会话存储放大（#35647）、桌面端反复压缩（#20983）、推理级别自动降级（#26930）都指向长会话用户体验与资源消耗的矛盾，需通过更智能的会话管理策略解决。


## 开发者关注点

- **Windows 平台问题集中爆发**：从桌面应用崩溃（#32683）、沙箱执行失败（#18620）、Code Integrity 错误（#35681）到 VS Code diff 全页崩溃（#35362/#35481），Windows 开发者几乎每天都会遇到阻断性问题。社区普遍认为 Windows 是当前 Codex 体验的最大短板。
- **认证与 MCP 配置链路脆弱**：OAuth issuer 验证失败（#31573）、Slack MCP 动态注册失败（#13200）等表明认证与 MCP 生态的集成质量仍需加强，尤其是 Enterprise / 自定义环境。
- **安全审查误伤**：cybersecurity 误报（#34306）让开发者感到安全机制过于粗糙，且错误信息不透明，影响正常开发节奏。
- **会话与状态一致性**：推理级别自动降级（#26930）、压缩后行为异常（#20983）、子代理模型不一致（#34821）等暴露了长会话状态管理的不稳定，开发者希望 Codex 能提供可靠、可预期的长时任务体验。
- **高频场景（代码审查、Browser Use）稳定性**：diff 视图在 Windows 上频繁崩溃，Browser Use 打开页面即闪退，直接影响核心生产力场景，开发者的耐心正在被快速消耗。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-07-31** | **数据来源：github.com/google-gemini/gemini-cli**


## 今日速览

昨日发布 v0.55.0-nightly 版本（主要为版本号更新），社区讨论集中在 **Agent 子代理的可靠性问题**——尤其是子代理在达到最大轮次（MAX_TURNS）后误报成功、通用代理挂起、以及浏览器代理在 Wayland 环境下的失败等 P1 级 Bug。此外，**Auto Memory 功能的安全与质量缺陷**成为新的关注焦点（多条相关 Issue 同日更新），MCP OAuth 令牌刷新修复和 Docker 基础镜像安全升级是 PR 中的亮点。


## 版本发布

### v0.55.0-nightly.20260730.gdc859e8e4

- 内容：包含 v0.54.0-preview.0 和 v0.53.0 的变更日志更新，版本号 bump。
- 性质：纯 nightly 版本推进，无功能性变更。

🔗 [查看 Release](https://github.com/google-gemini/gemini-cli/releases)


## 社区热点 Issues（Top 10）

### 1. Subagent 达到 MAX_TURNS 后误报 GOAL 成功
**#22323** | P1 | 评论 12 | 👍 2 | 更新于 07-31
`codebase_investigator` 子代理在达到最大轮次限制、未完成任何分析的情况下，仍报告 `status: "success"` 和 `"GOAL"` 终止原因，掩盖了真实的中断。此问题直接影响用户对代理结果的信任度，是当前评论最活跃的 Issue。

🔗 [github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. 通用代理（Generalist agent）无限挂起
**#21409** | P1 | 评论 8 | 👍 8 | 更新于 07-31
当 CLI 委托给通用代理时经常无限挂起（甚至等待一小时无响应），简单操作如创建文件夹也会触发。用户反馈禁用子代理后问题消失，表明代理调度逻辑存在缺陷。获 8 个 👍，社区受影响面较广。

🔗 [github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. 组件级评估体系建设（EPIC）
**#24353** | P1 | 评论 7 | 更新于 07-31
跟踪组件级行为评估的进展——目前已有 76 个行为评估测试覆盖 6 个 Gemini 模型，但健壮性仍待提升。属于基础设施类 EPIC，对长期质量保障意义重大。

🔗 [github.com/google-gemini/gemini-cli/issues/24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 4. AST 感知的文件读取/搜索/映射评估
**#22745** | P2 | 评论 7 | 👍 1 | 更新于 07-31
调查 AST 感知工具的价值：更精确地读取方法边界、减少 token 噪声、优化代码库映射。若落地可显著提升大仓库场景下的代理效率。

🔗 [github.com/google-gemini/gemini-cli/issues/22745](https://github.com/google-gemini/gemini-cli/issues/22745)

### 5. Gemini 不主动使用 skills 和子代理
**#21968** | P2 | 评论 6 | 更新于 07-31
用户反馈 Gemini CLI 几乎不会主动调用自定义 skills 和子代理（即使描述高度相关），必须显式指示才会使用。这削弱了自定义扩展的实际价值。

🔗 [github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 6. Auto Memory 对低信号会话无限重试
**#26522** | P2 | 评论 5 | 更新于 07-31
Auto Memory 仅在提取代理成功读取会话记录后才标记为已处理，若判断为低信号不读取，则该会话反复出现造成无限重试。需引入"跳过即处理"或去重机制。

🔗 [github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 7. Auto Memory 需确定性脱敏与减少日志
**#26525** | P2 | 评论 4 | 更新于 07-31
Auto Memory 将本地转录内容发送给模型时，脱敏发生在内容进入模型上下文之后，存在隐私风险；且服务可能记录已有技能内容。社区对安全细节的关注度持续上升。

🔗 [github.com/google-gemini/gemini-cli/issues/26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 8. Shell 命令执行后卡在 "Waiting input"
**#25166** | P1 | 评论 4 | 👍 3 | 更新于 07-31
简单 CLI 命令执行完毕后，终端仍显示 shell 活跃并卡在等待输入状态，即使用户确认命令早已完成。属 P1 且获 👍 3，影响日常使用体验。

🔗 [github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 9. 浏览器代理在 Wayland 下失败
**#21983** | P1 | 评论 4 | 👍 1 | 更新于 07-31
浏览器子代理在 Wayland 环境下启动失败，终止原因为 "GOAL"。Wayland 用户（主流 Linux 发行版默认）无法使用浏览器代理。

🔗 [github.com/google-gemini/gemini-cli/issues/21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 10. Auto Memory 无效补丁需隔离或标记
**#26523** | P2 | 评论 3 | 更新于 07-31
内存收件箱静默跳过畸形补丁、无 hunk 补丁及逃逸根目录的补丁，但后台提取器的摘要会读取所有 `.patch` 文件，造成无效数据积压。需建立隔离机制。

🔗 [github.com/google-gemini/gemini-cli/issues/26523](https://github.com/google-gemini/gemini-cli/issues/26523)


## 重要 PR 进展（Top 10）

### 1. 传播 InvalidStreamError 详情到 UI
**#28566** | P1 | area/core | 开放
将后端 `InvalidStreamError` 的错误类型和消息传递到 CLI UI 层，可针对空响应给出具体建议（如提示使用 `/compress` 降低上下文占用），改善错误可操作性。

🔗 [github.com/google-gemini/gemini-cli/pull/28566](https://github.com/google-gemini/gemini-cli/pull/28566)

### 2. 修复 diff hunk 标记被误识别为 @file 引用
**#28581** | P2 | area/core, agent | 开放
阻止 unified/combined diff 的 hunk 标记被解析为 `@file` 引用，消除大型 diff 提示下每 hunk 两次递归全局搜索导致的 `minimatch`/`path-scurry` 堆内存增长。

🔗 [github.com/google-gemini/gemini-cli/pull/28581](https://github.com/google-gemini/gemini-cli/pull/28581)

### 3. Docker 基础镜像升级至 node:24-slim
**#28602** | size/s | 开放
构建与运行镜像从 node:20-slim 升级至 node:24-slim，修复运行时阶段未从构建阶段复制 CLI 包的问题。

🔗 [github.com/google-gemini/gemini-cli/pull/28602](https://github.com/google-gemini/gemini-cli/pull/28602)

### 4. 沙箱 Dockerfile 升级至 Node 22（安全）
**#28603** | P1 | area/security | 开放
沙箱运行时环境执行模型指令，原 pinned Node 20 已于 2026-04-30 EOL，存在安全风险。升级至 Node 22 消除 EOL 运行时隐患。

🔗 [github.com/google-gemini/gemini-cli/pull/28603](https://github.com/google-gemini/gemini-cli/pull/28603)

### 5. MCP OAuth 令牌使用存储的 client ID 刷新
**#28481** | P1 | area/security | 开放
修复通过 OAuth 发现 + 动态客户端注册配置的 MCP 服务器的令牌刷新失败问题——此前刷新在本地即失败（未发起网络请求），且失败会删除已存凭证导致每次都要重新认证。

🔗 [github.com/google-gemini/gemini-cli/pull/28481](https://github.com/google-gemini/gemini-cli/pull/28481)

### 6. 容量耗尽分类为终止状态防止重试挂起
**#28599** | 已关闭 | size/s, m
将 `MODEL_CAPACITY_EXHAUSTED`（HTTP 429）在无重试延迟时归类为终止性限制，立即触发 fallback 链，解决预览模型容量耗尽时的客户端无限挂起。

🔗 [github.com/google-gemini/gemini-cli/pull/28599](https://github.com/google-gemini/gemini-cli/pull/28599)

### 7. Caretaker：NEEDS_HUMAN 转换时清除锁
**#28601** | 已关闭 | size/xs
修复 `IssuesStore` 在达到最大认领次数转换 `NEEDS_HUMAN` 时未清除 `lock.holder` 和 `lock.expires_at` 的问题，防止死锁残留。

🔗 [github.com/google-gemini/gemini-cli/pull/28601](https://github.com/google-gemini/gemini-cli/pull/28601)

### 8. macOS 缺失 seatbelt 配置时回退到内嵌版本
**#28551** | size/l | 开放
解决 macOS/gMac 沙箱模式（`-s`）下静态 seatbelt `.sb` 文件缺失导致的启动崩溃，回退到内嵌 профили。

🔗 [github.com/google-gemini/gemini-cli/pull/28551](https://github.com/google-gemini/gemini-cli/pull/28551)

### 9. 新增 --list-all-sessions 选项
**#28596** | P3 | area/core | 开放
允许跨所有已注册 workspace 列出聊天会话并按工作区分组展示，解决用户忘记会话创建目录的痛点。

🔗 [github.com/google-gemini/gemini-cli/pull/28596](https://github.com/google-gemini/gemini-cli/pull/28596)

### 10. 加载环境变量先于 settings 占位符解析
**#28597** | size/l | 开放
修复 settings 生命周期中的加载顺序竞态——此前系统/用户/工作区 settings 在解析时即对 `process.env` 展开，而本地 `.env` 尚未加载，导致占位符解析结果不一致。

🔗 [github.com/google-gemini/gemini-cli/pull/28597](https://github.com/google-gemini/gemini-cli/pull/28597)


## 功能需求趋势

从近期 Issues 和 PR 中提炼出以下社区关注方向：

1. **Agent 可靠性与可观测性**（占比最高）
   - 子代理失败状态误报（#22323）、通用代理挂起（#21409）、子代理轨迹需在 `/chat share` 中可见（#22598）、Bug 报告需包含子代理上下文（#21763）。社区对代理行为透明度的要求日益强烈。

2. **沙箱与供应链安全**
   - Docker 镜像升级（#28602、#28603）、MCP OAuth 刷新修复（#28481）、工作流供应链漏洞 PoC（#28594）。安全类 PR 在同日集中出现，显示维护者对供应链风险的高度重视。

3. **上下文管理自动化**
   - 自动压缩聊天历史（PR #28488）、InvalidStreamError 引导使用 `/compress`（PR #28566）、Auto Memory 相关的 5 条 Issue 同批更新。长会话场景下上下文管理成为使用瓶颈。

4. **AST 感知的代码理解**
   - AST-aware 文件读取/搜索/映射（#22745）及对应 CLI 工具调研（#22746）。社区期待更精准的代码导航能力以减少 token 消耗。

5. **模型选择与可用性**
   - 模型选择器缺少 gemini-3.5-flash（PR #28485）、无预览权限时 Auto 模型不可见（PR #28592）、>128 工具时 400 错误（#24246）。模型/工具生态扩展带来的选择与管理复杂性上升。


## 开发者关注点

1. **代理自主性与可控性的张力**
   - 一方面社区抱怨 Gemini 不主动使用 skills/子代理（#21968），另一方面 P1 级 Bug 显示子代理执行不可靠（误报成功、挂起、越权运行 #22093）。开发者需要一个"可信赖才放手"的平衡点。

2. **低信号会话与资源浪费**
   - Auto Memory 对低信号会话无限重试（#26522）、无效补丁静默跳过但造成积压（#26523）——后台进程的资源浪费问题引发关注，开发者希望系统能更智能地判断"何时该放弃"。

3. **终端体验细节**
   - Shell 命令执行后卡在 "Waiting input"（#25166）、终端 resize 闪烁（#21924）、外部编辑器退出后画面损坏（#24935）——终端交互稳定性直接影响日常开发流。

4. **权限与安全边界**
   - v0.33.0 后子代理在配置禁用状态下仍被调用（#22093）、`git reset`/`--force` 等破坏性命令需被劝阻（#22672）——开发者希望 CLI 在自主操作时仍尊重用户设定的安全边界。

5. **配置覆盖失效**
   - 浏览器代理忽略 settings.json 覆盖（#22267）、settings 占位符解析时序问题（PR #28597）——配置系统的可预测性对高级用户至关重要。

---

*本日报由 AI 自动汇总生成，数据截至 2026-07-31。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-07-31

## 今日速览

昨日发布 **v1.0.77**，引入了浏览器端 OAuth 登录流程（现为本地终端默认方式），并新增 `Ctrl+G` 快捷键用于在 `$EDITOR` 中编辑 `ask_user` 自由表单回答。社区方面，关于**AI 额度消耗异常**与**子代理无响应**的反馈集中出现，另有多个涉及 MCP 工具参数处理和日志级别的 Bug 被提交，值得关注。

## 版本发布

### [v1.0.77](https://github.com/github/copilot-cli/releases)（2026-07-30）
- **无条件自动批准（Unconditional autopilot approval）**：当允许绕过（bypass）时，在当前会话中自动禁用沙箱（sandbox）
- **`Ctrl+G` 编辑 `ask_user` 回答**：在提示符不关闭的情况下，直接打开编辑器修改自由文本回答
- **浏览器端 OAuth 登录流程**：现为本地交互式终端的默认方式（远程/无头终端仍使用设备码）。可用 `--web-flow`/`--device-code` 强制指定模式，或在交互式 `/login` 命令中选择

## 社区热点 Issues

1. **[#4308 / #4309 · AI 额度消耗异常](https://github.com/github/copilot-cli/issues/4308)**
   ⭐ 高关注度：多位用户在 v1.0.75 中报告，所有可见任务完成后会话仍在消耗 AI 额度（观察到约 97.8% 消耗）。涉及计费与后台行为透明性，属高风险问题。

2. **[#4306 · 子任务冻结无响应](https://github.com/github/copilot-cli/issues/4306)**
   自动模式（autopilot）下，使用 `fleet` 循环调用多个 agent 时，子任务中途冻结，无任何输出。直接阻塞自动化工作流。

3. **[#4293 · 全工具权限子代理返回空结果](https://github.com/github/copilot-cli/issues/4293)**
   子代理在拥有完整工具集时**无任何响应**（无错误、无部分输出、无日志），而受限工具集时同一模型/提示可正常工作。疑似权限处理逻辑缺陷。

4. **[#4310 · 上下文窗口回退至 128K Token](https://github.com/github/copilot-cli/issues/4310)**
   当路由模型缺少能力限制信息时，引擎静默回退至硬编码的 128K Token 预算，导致 1M Token 模型（如 Anthropic 大上下文版本）被错误压缩。

5. **[#4305 · 'Undefined' 无法转为 Rust String](https://github.com/github/copilot-cli/issues/4305)**
   升级至 1.0.76 后，任何命令都立即报错 `Failed to convert JavaScript value 'Undefined' into rust type 'String'`。影响面广，为 1.0.76 版本的回归性 Bug。

6. **[#3767 · 超大附件导致会话永久卡死（已关闭）](https://github.com/github/copilot-cli/issues/3767)**
   附件超过 CAPI 5MB 原生限制后，该轮对话永久失败且会话无法恢复。虽已关闭，但反映了大附件场景下的健壮性问题。

7. **[#4295 · AI 额度接近限制提醒](https://github.com/github/copilot-cli/issues/4295)**
   功能请求：Visual Studio 2026 已支持在聊天会话中提醒 AI 额度即将耗尽，希望 CLI 具备同等能力。结合 #4308 事件，该需求更显迫切。

8. **[#4294 · 恢复会话注入 COLORTERM 并改变提示符颜色](https://github.com/github/copilot-cli/issues/4294)**
   恢复会话时会向子进程注入 `COLORTERM=truecolor`，导致提示符高亮颜色异常（尽管父进程未设置该变量）。终端渲染一致性问题。

9. **[#4296 · iTerm2 中 Cmd+V 粘贴失效](https://github.com/github/copilot-cli/issues/4296)**
   macOS/iTerm2 下，`Cmd+V` 无法粘贴，仅能通过菜单栏完成。Claude Code 在相同环境下表现正常，存在明显差距。

10. **[#1381 · Rewind 需 Git 仓库支持（10 👍）](https://github.com/github/copilot-cli/issues/1381)**
    使用非 Git 版本控制系统（如 Jujutsu）的用户无法使用 Rewind 回退功能。VS Code 中该功能不依赖 Git，CLI 行为不一致。

## 重要 PR 进展

截至本日报发布时，过去 24 小时内无新增或更新的 Pull Requests。

## 功能需求趋势

- **AI 额度透明化与预警**：多个 Issue（#4308、#4309、#4295）集中在 AI 额度消耗的可见性与预警机制，尤其是后台任务持续消耗额度的问题
- **认证方式多元化**：#4300 请求为 BYO-K 场景支持 `bearerToken` 认证（企业合规场景）；同时 #4310 涉及大上下文模型的正确识别与适配
- **终端体验与快捷键**：#4296（Cmd+V 粘贴）、#4294（COLORTERM 注入）以及 v1.0.77 的 `Ctrl+G` 编辑功能，均指向终端交互体验优化
- **沙箱与权限精细化配置**：#4298 请求在 settings.json 中支持按工具启用/白名单化沙箱能力
- **背景任务稳定性**：#4306 与 #4299（长会话打字延迟）均反映了后台 agent 运行时的稳定性与资源占用问题

## 开发者关注点

- **会话卡死与无响应**：最常见且影响最大的问题。表现为：超大附件永久卡死（#3767）、子代理无响应（#4293、#4306）、任务完成后仍消耗额度（#4308）
- **回归 Bug 频发**：1.0.76 的 `Undefined` 类型转换错误（#4305）几乎影响所有命令，引发对发布质量的担忧
- **日志级别配置缺陷**：#4297 中设置任何非 `all`/`default` 的日志级别都会导致启动崩溃，排查问题时无法有效降级日志
- **非 Git 工作流支持**：#1381 持续获得关注（10 👍），用户希望 Rewind 功能不强制依赖 Git
- **MCP 生态互操作问题**：#4301 报告 MCP 工具参数中 `anyOf: [array, string]` 联合类型被错误字符串化——对 MCP 重度用户尤其关键
- **长会话性能退化**：#4299 指出长时间运行（尤其有后台 agent 时）打字延迟严重，影响基本可用性
- **CSS 样式：** 无（纯文本格式）

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-07-31

## 今日速览
昨日社区活跃度降至低点，无新版本发布，仅更新了 3 个 Issue 与 1 个 PR。核心焦点集中在**持久化记忆系统**的功能需求上，该提案已持续酝酿 5 个月并积累了较高讨论量（7 条评论）；同时，**LLM 过载 429 错误**导致无法使用的严重问题开始浮出水面。


## 社区热点 Issues（共 3 条）

**1. #1283 [功能请求] 记忆系统：跨会话持久化上下文**
- **作者**: CatKang | **更新**: 2026-07-30 | **评论**: 7 | **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1283
- **为何重要**: 该提案自 2 月创建以来持续被关注，代表了社区对“自动记忆（AI 维护笔记）”与“手动记忆（用户定义指令）”双轨机制的强烈渴求，是当前最受关注的功能方向，且近两天仍被更新，热度不减。

**2. #2571 [Bug] LLM 过载！完全无法使用 Kimi**
- **作者**: andrew-sz | **创建**: 2026-07-30 | **评论**: 1
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2571
- **为何重要**: 用户在使用 Moderato 平台、**Kimi K3** 模型（v1.49.0）时遭遇 **429 错误**，Kimi Code CLI 直接不可用。即时性极强（昨日新发），严重影响核心使用。

**3. #2570 [Bug] CLI 间歇性卡死，旋转月亮图标，与浏览器标签页状态相关**
- **作者**: XbackMK | **创建**: 2026-07-30 | **评论**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2570
- **为何重要**: 涉及 **Windows 11** 下 **KIMI K3 HIGH** 模型（v0.29.2）的稳定性问题。用户发现 CLI 冻结与浏览器标签页状态强相关，暗示可能由会话心跳检测或 SSO 刷新机制缺陷导致。


## 重要 PR 进展（共 1 条）

**#2565 [修复] hooks: 对 fire-and-forget (发后即忘) 钩子触发器保持强引用**
- **作者**: LHMQ878 | **更新**: 2026-07-30
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2565
- **功能说明**: 针对 #2564 的修复。由于 `asyncio` 使用 `WeakSet` 持有任务，原先的 `_hook_task` 在函数返回后可能被垃圾回收，导致“发后即忘”的钩子触发逻辑被意外中断。该 PR 通过保持强引用确保钩子任务可靠执行，是对异步任务生命周期管理的精确补强。


## 功能需求趋势
- **记忆系统**: 对跨会话持久化上下文的功能需求呼声最高，涵盖自动学习和用户定向记忆两方面。
- **稳定性与可靠性**: 围绕“LLM 过载”与“随机卡死”的讨论，反映出用户对在复杂网络/登录态环境下 CLI 运行稳定性的更高要求。

## 开发者关注点
- **错误处理**: 针对 429 限流的暴露，开发者要求更完善的错误捕捉与智能重试机制，并希望明确不同平台/订阅等级的限额策略。
- **异步任务健壮性**: 相关 Bug（如随机停住）被追踪至 asyncio 任务被意外回收，开发者需关注 `create_task` 引用管理及协程生命周期对齐问题。
- **跨平台一致性问题**: 一个 Issue 聚焦 Windows 11，关联浏览器标签页状态，反映出桌面环境下 CLI 与本地浏览器会话交互的兼容性尚未达成完美统一。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-07-31

## 今日速览

OpenCode 发布 v1.18.10，核心改进为自动发现 Modal 可用模型，桌面端同步优化了附件去重、通知堆叠与标签页交互。社区热点集中在模型服务稳定性（GPT-5.6 Sol 服务器过载、OpenCode Go 付费模型 401）以及桌面端升级后引发的崩溃问题，多个相关修复 PR 已迅速跟进。

## 版本发布

**v1.18.10**

- **Core**：自动发现可用的 Modal 模型（由 @devennavani 贡献）。
- **Desktop**：
  - 防止重复添加同一附件。
  - 始终显示新建会话按钮。
  - 改进 Toast 通知的堆叠、关闭逻辑及移动端布局。
  - 优化标签页 hover 与激活态样式。

## 社区热点 Issues（Top 10）

| # | Issue | 核心问题 | 社区反应 |
|---|-------|---------|---------|
| 1 | [#39653](https://github.com/anomalyco/opencode/issues/39653) | GPT-5.6 Sol 模型持续返回 "server overloaded" 错误，Pi/Codex 正常 | 🔥 16 评论 / 10 👍，影响面广，用户反馈集中 |
| 2 | [#37762](https://github.com/anomalyco/opencode/issues/37762) | Ollama 本地模型响应异常，用户配置 64GB RAM + 4GB VRAM 仍无法正常生成邮件 | 8 评论，本地模型支持呼声高 |
| 3 | [#39288](https://github.com/anomalyco/opencode/issues/39288) | 升级 1.18.8 后桌面端报 `AutoScroller plugin depends on Scroller plugin` 错误 | 6 评论，版本升级引发的插件依赖回归 |
| 4 | [#38655](https://github.com/anomalyco/opencode/issues/38655) | 最新更新后无法在 plan/build 模式间切换 | 5 评论，核心工作流受影响 |
| 5 | [#37628](https://github.com/anomalyco/opencode/issues/37628) | npm 全局安装 `opencode-ai` 在 Windows 上出现 16 位兼容性错误 | 5 评论，Windows 安装阻断问题，Node v26 环境 |
| 6 | [#39491](https://github.com/anomalyco/opencode/issues/39491) | Plan 模式下 Claude Sonnet 4.6 可绕过限制，通过 bash 直接写文件 | 4 评论，安全/权限边界漏洞 |
| 7 | [#39655](https://github.com/anomalyco/opencode/issues/39655) | Web 版显示 "No folders found"，但后端 API 已正确返回项目列表 | 4 评论，Web UI 与 API 状态不同步 |
| 8 | [#27837](https://github.com/anomalyco/opencode/issues/27837) | `opencode --web` 模式下左侧会话列表为空（已定位根因，SSE 事件驱动问题） | 4 评论 / 2 👍，长期未修复的 Web 模式缺陷 |
| 9 | [#39704](https://github.com/anomalyco/opencode/issues/39704) | 升级 1.18.10 后桌面端切换/关闭会话即崩溃，报 `Stale read from <Show>` | 2 评论 / 1 👍，最新版本严重回归，已有对应 PR |
| 10 | [#37598](https://github.com/anomalyco/opencode/issues/37598) | OpenCode Go 缓存记录缺失 session 标识，且 GLM-5.2 缓存命中行为不稳定 | 2 评论 / 1 👍，计费与缓存正确性问题 |

## 重要 PR 进展（Top 10）

| # | PR | 内容 | 状态 |
|---|----|------|------|
| 1 | [#39767](https://github.com/anomalyco/opencode/pull/39767) | **修复桌面端会话标签页 Stale Read 崩溃**（Closes #39704 / #39766），阻止 Solid 过渡期读取过期状态 | ✅ Open |
| 2 | [#39781](https://github.com/anomalyco/opencode/pull/39781) | **新建 workspace 可选择基础分支**，修复 `git worktree add` 无起点导致的问题（Closes #39778 / #39779） | ✅ Open |
| 3 | [#39776](https://github.com/anomalyco/opencode/pull/39776) | **TUI 本地插件热重载**，编辑插件源码无需重启客户端即可生效 | ✅ Open |
| 4 | [#39748](https://github.com/anomalyco/opencode/pull/39748) | 标题生成失败自动重试，并保留最初用户 prompt 作为兜底（Closes #39529） | ✅ Open |
| 5 | [#39753](https://github.com/anomalyco/opencode/pull/39753) | `/new` 创建新会话时继承当前会话目录，与桌面端新标签行为对齐 | ✅ Closed |
| 6 | [#39752](https://github.com/anomalyco/opencode/pull/39752) | v2 TUI 新增 `ctrl+o` 打开菜单，统一跳转会话语项目 | ✅ Closed |
| 7 | [#39774](https://github.com/anomalyco/opencode/pull/39774) | 修复异步选项插入/排序时选中项漂移问题 | ✅ Closed |
| 8 | [#39768](https://github.com/anomalyco/opencode/pull/39768) | 删除会话时 Toast 显示具体会话名称而非泛化文案 | ✅ Closed |
| 9 | [#39770](https://github.com/anomalyco/opencode/pull/39770) | 修复桌面文件树可被压缩至裁剪 "Files Changed" 标签页（Closes #39765） | ✅ Open |
| 10 | [#39764](https://github.com/anomalyco/opencode/pull/39764) | 新增 `session.request` 插件钩子，允许在请求发出前修改 HTTP 头与 body | ✅ Open |

## 功能需求趋势

- **Web/Desktop 一致性**：Web 模式会话列表为空（#27837）、项目展示不一致（#39655）等跨端行为差异持续被反馈。
- **本地模型与离线体验**：Ollama 使用问题（#37762）、LAN 发现（#27554）表明本地优先场景需求上升。
- **新模式与权限边界**：Plan 模式可被绕过写入文件（#39491），对模式级沙箱/权限控制提出了更高要求。
- **配置与文档清晰度**：`variants` 子配置命名规范（camelCase vs snake_case）待官方明确（#39256）。
- **网络容错与快速失败**：网络抖动时无短超时与回退（#39771），国内用户对 GitHub 被墙场景建议增多。

## 开发者关注点

- **升级回归频繁**：1.18.8 插件依赖崩溃（#39288）、1.18.10 桌面端 Stale Read 崩溃（#39704）接连出现，社区对发布质量存在担忧。不过相关修复 PR 已在 24 小时内快速响应。
- **模型服务稳定性与计费透明度**：GPT-5.6 Sol 服务器过载（#39653）、OpenCode Go 付费模型 401（#38473）、Kimi K3 双倍额度计算不符（#37748）等问题集中指向服务端能力与用量展示的可靠性。
- **Windows 支持仍是薄弱环节**：npm 安装 16 位兼容错误（#37628）、文件树无法展开（#36743）、选择快捷键被系统占用（#38585）等问题依旧存在。
- **TUI/Desktop 交互细节**：移动端侧边栏不自动收起（#37746）、主题不跟随系统切换（#38506）等体验问题持续被提交，开发者对打磨细节的期望较高。多个 Kit Langton 的 TUI 交互优化 PR（#39752/#39753/#39768/#39774/#39776/#39780）正处于密集迭代中。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-07-31

> 数据来源：github.com/badlogic/pi-mono（earendil-works/pi）

---

## 今日速览

昨日社区讨论主要聚焦于三类问题：**会话模型目录（model catalog）刷新停滞导致的连锁故障**（`/scoped-models` 卡死、登录挂起、可用性刷新永久不可恢复）；**流式解析与协议层缺陷**（Anthropic 流解析丢弃初始块、Fireworks 瞬时超时、上下文增长后流式输出变慢）；以及**环境适配补全**（Wayland 剪贴板修复已合入、Windows TUI 绘制问题仍在推进）。PR 方面，Markdown API（#7231）与 Wayland 剪贴板修复（#7261）已合入主分支。

---

## 社区热点 Issues

### 1. 模型目录刷新停滞导致的连锁故障（3 个相关 Issue）

- **[#7153] `/scoped-models` 刷新停滞时约 5 分钟无响应** — `/scoped-models` 命令在模型目录刷新完成前不渲染任何 UI，无加载提示、无错误提示。社区正在关注这一系列问题的共性根因。 [链接](https://github.com/earendil-works/pi/issues/7153)
- **[#7027] API-key 登录后在模型目录刷新停滞时挂起** — 凭据已写入 `auth.json`，但登录对话框无法返回。获得 4 👍，说明受影响用户较多。 [链接](https://github.com/earendil-works/pi/issues/7027)
- **[#7301] 可用性刷新失败后永久不可恢复** — `forceRefreshAvailability()` 链式挂到已 stalled 的 Promise 上，即使底层原因消失也无法恢复。**建议优先修复**，属核心运行时健壮性问题。 [链接](https://github.com/earendil-works/pi/issues/7301)

### 2. [#7194] 工具卡片滚动出视口时 Pi 每秒全量重绘（已关闭）

远程沙箱场景（通过原始 PTY 字节流 websocket 转发）下，整个会话转录频繁重绘。评论 7 条，1 👍。此类性能问题在远程/嵌入式场景中影响较大。 [链接](https://github.com/earendil-works/pi/issues/7194)

### 3. [#7161] anthropic-messages 路径不发送 `x-client-request-id`

与所有 OpenAI 路径行为不一致。依赖此 header 做会话亲和性的网关（如轮询多个 Claude 账号的代理）无法正确分组。MTeam88 报告，评论 6 条。属协议一致性缺陷。 [链接](https://github.com/earendil-works/pi/issues/7161)

### 4. [#7047] Gemini 3.x 工具调用 ID 在回放时被剥离

`functionCall` 与 `functionResponse` 中的 `id` 字段在历史回放时丢失，Gemini 3 要求相同 ID 回传。多轮工具调用场景下会直接破坏对话，1 👍，5 条评论。 [链接](https://github.com/earendil-works/pi/issues/7047)

### 5. [#7283] Anthropic 流解析器丢弃初始块（进行中）

`content_block` 的起始事件被假定为空，但实际可能携带内容。`packages/ai/src/api/anthropic-messages.ts` 中 `text`、`thinking` 字段需检查非空。带 `[inprogress]` 标签，说明已有修复方向。 [链接](https://github.com/earendil-works/pi/issues/7283)

### 6. [#7248] Wayland 下 Ctrl+V 静默失效（已关闭）

`readClipboardText()` 仅支持 X11。KDE Plasma 6 + Konsole 环境下从 Wayland 应用复制文本后粘贴无效。修复 PR #7261 已合入。 [链接](https://github.com/earendil-works/pi/issues/7248)

### 7. [#7332] 上下文增长后流式输出极慢（已关闭）

30 秒录屏显示模型输出打印速率随对话变长而急剧下降，用户无滚动、无输入操作。性能回归类问题，2 条评论。 [链接](https://github.com/earendil-works/pi/issues/7332)

### 8. [#7315] Fireworks 请求偶尔瞬时失败 "Request timed out."

空内容、零 token 消耗，自动重试 3 次，间隔 2s/4s/8s。疑似发送前即失败（如连接建立阶段）。 [链接](https://github.com/earendil-works/pi/issues/7315)

### 9. [#6300] Windows TUI 输入行逐字符重绘（开放中）

Windows 10 Pro 22H2 + cmd.exe/Windows Terminal 下每个字符出现在新行。6 条评论，环境信息已提供（Node v22.x），**等待维护者定位**。 [链接](https://github.com/earendil-works/pi/issues/6300)

### 10. [#7299] 通过 AgentOptions 暴露 `shouldStopAfterTurn` 回调

用户要求将低层循环已有的 `shouldStopAfterTurn` 钩子提升到 `AgentOptions`。引用 #4291（曾被大重构自动关闭），开发者明确表达了需求意图。 [链接](https://github.com/earendil-works/pi/issues/7299)

### 11. [#7350] 示例扩展应挂钩 `agent_settled` 而非 `agent_end`（已关闭）

`notify.ts` 示例在自动重试、压缩重试、排队后续轮次之前就触发 "Ready for input" 通知，时机错误。 [链接](https://github.com/earendil-works/pi/issues/7350)

---

## 重要 PR 进展

### 已合入

- **[#7231] Markdown API（关闭 #6747）** — 为扩展提供修改 agent 消息渲染表示的能力，同时不影响发送给 LLM 的原文内容。实现对自定义公式渲染器等扩展场景的直接支持。 [链接](https://github.com/earendil-works/pi/pull/7231)
- **[#7261] Wayland 剪贴板修复（关闭 #7248）** — Linux 下优先使用 CLI 工具：Wayland 用 `wl-paste --no-newline`，X11 用 `xclip`/`xsel`，解决 Ctrl+V 静默失效。 [链接](https://github.com/earendil-works/pi/pull/7261)
- **[#7340] 修复浅色终端背景下粗体文本不可见** — 某些终端将 ANSI bold 解释为 bright（bold-as-bright），导致白色粗体在白底上不可见。修复方案为显式设置前景色，而非仅依赖 ANSI bold。 [链接](https://github.com/earendil-works/pi/pull/7340)
- **[#7309] RPC stdout 处理器中对 JSON.parse 增加保护（关闭 #7300）** — 子进程输出任何非 JSON 行（日志、弃用警告、截断行）将可能导致崩溃，现安全处理。 [链接](https://github.com/earendil-works/pi/pull/7309)
- **[#7306] SDK 示例中移除已弃用的 `getModel`** — 使用 `ModelRuntime.getModel()` 替代。 [链接](https://github.com/earendil-works/pi/pull/7306)
- **[#7344] 新增远程会话线协议包 `@earendil-works/pi-protocol`** — 定义验证过的远程会话命令、事件、快照和错误；有界 CBOR 编码 + 增量长度前缀分帧。 [链接](https://github.com/earendil-works/pi/pull/7344)
- **[#7343] Agent harness 关闭生命周期** — 幂等的 `shutdown()` 操作，拒绝新任务、中止活动 turns/压缩/树导航、阻止关闭后的 provider 启动与结果持久化。 [链接](https://github.com/earendil-works/pi/pull/7343)
- **[#7346] AI 层与协议层共享运行时 schema** — 在 `pi-ai` 中定义共享 TypeBox schemas，`pi-protocol` 复用，对齐工具调用值与停止原因。 [链接](https://github.com/earendil-works/pi/pull/7346)
- **[#7286] Bedrock provider 错误保留结构化元数据（关闭 #7224）** — 保留结构化错误信息，不再序列化 `ClientHttp2Stream`。 [链接](https://github.com/earendil-works/pi/pull/7286)
- **[#7061] openai-completions 兼容修复** — 处理数组形式 `delta.content`（Databricks Qwen3/gpt-oss 场景）与缺失 `finish_reason` 的情况。 [链接](https://github.com/earendil-works/pi/pull/7061)

### 进行中 / 待审

- **[#6216] Amazon Bedrock Mantle OpenAI Responses provider** — 1 条评论，添加新 provider。 [链接](https://github.com/earendil-works/pi/pull/6216)
- **[#6534] 新增 developer 消息角色** — 引用 RFC 54。 [链接](https://github.com/earendil-works/pi/pull/6534)
- **[#7148] 实验性 loadout 管理** — 会话中启用/禁用扩展，持久化到会话。 [链接](https://github.com/earendil-works/pi/pull/7148)
- **[#7163] SQLite FTS5 搜索索引**。 [链接](https://github.com/earendil-works/pi/pull/7163)
- **[#7339] OpenAI background mode responses（草稿）**。 [链接](https://github.com/earendil-works/pi/pull/7339)

---

## 功能需求趋势

1. **远程/嵌入式场景支持** — 远程沙箱 PTY 转发导致的重绘问题、多会话句柄、远程会话线协议（#7344、#7348）表明 Pi 正被嵌入到更广泛的工具链中，稳定性需求上升。
2. **扩展 API 深化** — Markdown 渲染 API（#6747/#7231）、状态化 ACP agent 后端（#7320）、loadout 管理（#7148），扩展机制正从"触发事件"走向"深度集成"。
3. **模型目录/登录流程健壮性** — 目录刷新停滞引发的三个独立 Issue（#7153/#7027/#7301）指向同一根因，社区关注度最高，属体验关键路径。
4. **协议一致性** — `x-client-request-id`（#7161）、Gemini 工具 ID 保留（#7047）、developer 角色（#6534），多 provider 适配中的细节一致性成为焦点。
5. **CLI/调试辅助** — `version` 命令展示运行时信息（#7244）便于问题排查，反映社区对可诊断性的需求。

---

## 开发者关注点

- **模型目录刷新的同步阻塞** — 多个命令（`/scoped-models`、`/login`）在目录刷新未完成时无任何 UI 反馈，开发者普遍期望异步渲染 + 加载状态。
- **Promise 永不 settle 的故障模式** — #7301 中 `forceRefreshAvailability` 链式挂到 stuck Promise 的问题，提示需要超时/失败重置机制。
- **Windows TUI 稳定性** — #6300（逐字符换行）仍未解决，Windows 用户受影响时间较长。
- **流式解析边界情况** — Anthropic 初始块丢弃（#7283）、Fireworks 瞬时超时（#7315）、openai-completions 数组 content（#7216），多 provider 适配中"非标准"响应格式处理是高频痛点。
- **环境适配补全** — Wayland 剪贴板（#7248）、浅色终端主题（#7340）、Devanagari 字符渲染（#6124），跨平台细节持续完善。

---

*日报生成时间：2026-07-31 | 数据窗口：过去 24 小时 | 数据源：earendil-works/pi*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-07-31

---

## 1. 今日速览

今日社区热度集中在 **CI 稳定性欠佳**（多条 SDK E2E 测试失败与 flaky 问题相关 PR 被机器人追踪）以及 **Anthropic 转换器的一批关联 bug**（由同一位开发者 netbrah 系统性提交，涉及 ID 字符集、tool_use 清理等深度细节）。功能侧，**Agent Team 队友消息阻塞**与 **worktree 设置隔离** 是两个用户可感知的活跃问题。此外，Desktop 打包（#8132）和 Windows 兼容性修复（#7957, #8050）表明跨端体验正在被持续补齐。

---

## 2. 版本发布

**v0.21.1-nightly.20260731.702932cc7** — 本次仅包含两项 CI/Web Shell 修复，无面向用户的显著功能变更。

- `fix(ci)`: 为 qwen-triage 容器任务添加默认 bash shell（#7838）
- `fix(web-shell)`: 预处理逻辑修复（截断）

> 建议生产环境用户关注稳定版发布节奏。同时对 #7972 反馈的 v0.21.1 崩溃问题保持关注——目前已有 PR #8088 尝试为该类崩溃增加错误可见性（而非声称修复），并正在推动定位。

---

## 3. 社区热点 Issues（Top 10）

### #8124 Startup banner sometimes missing top lines on first paint
- **标签**: `P2` `UI` `Rendering` `Windows` `welcome-pr`
- **创作者**: dpc00 | 评论: 9 | 👍: 0
- **关键点**: 终端 TUI 首屏渲染时，顶部 ASCII 横幅偶发缺失 3 行。属于难以重现的间歇性渲染 bug，社区关注度高（评论数今日最高）。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8124

### #7966 如何获取会话中创建了哪些文件？
- **标签**: `question` `session-management` `file-operations`
- **创作者**: ru1yex | 评论: 5 | 👍: 0
- **关键点**: 用户希望区分/追踪会话中直接生成或间接生成的文件，暴露出会话级文件操作的追踪能力（透明性）不足。
- **链接**: https://github.com/QwenLM/qwen-code/issues/7966

### #8083 design(core): make derived Config context ownership explicit
- **标签**: `P1` `core` `enhancement` — **P1 高优先级**
- **创作者**: yiliang114 | 评论: 5 | 👍: 0
- **关键点**: 多位维护者参与的架构改进讨论，旨在解决通过原型链派生 Config 导致的所有权语义模糊问题（涉及 subagent、scope memory 等模块）。属于核心架构打磨。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8083

### #4063 refactor: core + cli 架构 Review — 12 项结构性问题清单
- **标签**: `core` `cli` `enhancement` `needs-triage`
- **创作者**: pomelo-nwu | 评论: 5 | 👍: 1
- **关键点**: 长期存留的架构审查清单，指出核心类型被 `@google/genai` 绑架（136 个文件直接依赖）。已存续两月，说明大型架构重构推进需谨慎。🌟 值得关注。
- **链接**: https://github.com/QwenLM/qwen-code/issues/4063

### #8136 Provider warning sanitizer truncates messages & leaks password
- **标签**: `P2` `security` `bug`
- **创作者**: LHMQ878 | 评论: 4 | 👍: 0
- **关键点**: 安全相关 bug：URL 清洗逻辑在遇到端口号时截断消息，且对包含 `@` 的密码会泄露凭据。**影响面广且不修复则有泄露风险**，建议重点关注。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8136

### #8162 Anthropic converter: stale thinking signatures not pruned
- **标签**: `P2` `core` `content-generation` `welcome-pr`
- **创作者**: netbrah | 评论: 4 | 👍: 0
- **关键点**: 历史轮次清理后，遗留的 `thinking` 块与已删除的 `tool_use` 未同步清除，直接损害 Anthropic 模型兼容性输出。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8162

### #8138 worktree settings.json writes to project root .qwen
- **标签**: `P2` `configuration` `settings` `welcome-pr`
- **创作者**: Aleks-0 | 评论: 4 | 👍: 0
- **关键点**: Git worktree 场景下配置隔离失效，设置被错误写入项目根目录，影响多 worktree 并行开发者的数据正确性。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8138

### #8146 Desktop app not work with LMStudio
- **标签**: `P2` `integration` `Windows` `welcome-pr`
- **创作者**: gitmeatarru | 评论: 4 | 👍: 0
- **关键点**: 桌面端与 LM Studio 本地服务联调无响应，疑似请求根本没发送。Windows 生态本地模型接入稳定性问题。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8146

### #8102 proposal(core): deterministic tool-execution boundaries
- **标签**: `P3` `core` `security` `feature-request`
- **创作者**: chiga0 | 评论: 4 | 👍: 0
- **关键点**: 提出将 LLM 置于信任边界外、由运行时确定性管控工具执行的设计提案，属于「可信 Agent 运行时」方向的探索，引发社区对安全边界设计的讨论。
- **链接**: https://github.com/QwenLM/qwen-code/issues/8102

### #7972 0.21.1使用 奔溃3次
- **标签**: `P2` `bug` `CLI` `need-information`
- **创作者**: alloy1987 | 评论: 4 | 👍: 0
- **关键点**: 升级 0.21.1 后 Windows 平台三次崩溃（Node.js v24 / win32 x64），当前无日志兜底导致无从排查。已关联 PR #8088。
- **链接**: https://github.com/QwenLM/qwen-code/issues/7972

---

## 4. 重要 PR 进展（Top 10）

### #8147 fix(triage): render verify report as sanitized markdown, not escaped pre dump
- **创作者**: wenshao | `autofix/takeover`
- **关键点**: 将沙箱验证报告的原始转义文本渲染为可读的 Markdown，提升机器人评审信息传达效率。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8147

### #8132 feat(desktop): package Web Shell as release-ready desktop app
- **创作者**: yiliang114
- **关键点**: 将 Tauri 原型落地为发行版桌面应用，复用 Web Shell 并补齐原生生命周期（启动、恢复等）。桌面端由原型走向产品化的关键步骤。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8132

### #8137 fix(cli): scope warning credential stripping to URL authority
- **创作者**: LHMQ878
- **关键点**: 修复 #8136 的安全问题，将凭据清洗范围限定在 URL authority，删除自制启发式逻辑。安全修复落点明确。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8137

### #8056 fix(serve): isolate managed memory by selected workspace
- **创作者**: qqqys | `autofix/takeover`
- **关键点**: 为托管 memory 增加 workspace 限定（异步 remember/forget/dream 操作及可选精确工作区存储模式），解决多工作区记忆串扰问题。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8056

### #8163 fix(anthropic): don't strip trailing tool_use and dedup tool_result
- **创作者**: netbrah | `review/self-reported`
- **关键点**: 修复 #8159 及相关问题：不再误删尾部 tool_use、增加 tool_result 去重逻辑。Anthropic 转换器语义修正。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8163

### #7957 feat(cli): paste copied Windows files
- **创作者**: zhuyuy
- **关键点**: 支持 Windows 文件资源管理器中复制文件后直接粘贴，非图片类型将插入路径，图片走现有附件流程。补齐 Windows 原生交互闭环。
- **链接**: https://github.com/QwenLM/qwen-code/pull/7957

### #8032 feat(core): add a host tool invocation guard
- **创作者**: chiga0 | `autofix/takeover`
- **关键点**: 在工具最终调用前提供轻量进程内守卫（可观测、可授权、可中止），呼应 #8102 提案的安全方向。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8032

### #8088 fix(cli): prevent silent VP-mode crash by adding uncaughtException handler
- **创作者**: chiga0 | `autofix/takeover`
- **关键点**: 为 VP 模式（备用屏）增加 `uncaughtException` 兜底并强化错误可见性，主动承认不修复但增强崩溃可诊断性（关联 #7972 等）。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8088

### #8050 fix: make the test suite portable on Windows
- **创作者**: yiliang114 | `autofix/takeover`
- **关键点**: 让测试套件与平台敏感的运行路径在 Windows 上表现一致，同时保留 POSIX 独有断言。提升 Windows 端 CI 可信度。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8050

### #8156 fix(test): scope auto-edit canUseTool assertion to write/edit tools
- **创作者**: qwen-code-dev-bot | `review/self-reported`
- **关键点**: 收紧 SDK E2E 测试断言（只对 write/edit 工具生效），针对性修复 flaky 测试，回应 #8153 的 CI 失败。
- **链接**: https://github.com/QwenLM/qwen-code/pull/8156

---

## 5. 功能需求趋势

- **会话隔离与可观测性**: #7966、#8056、#8128 等均围绕「按会话/工作区隔离与追踪状态」展开，社区对数据归属与上下文边界的一致需求。
- **确定性工具执行与安全边界**: #8102、#8032 等推动 Agent 运行时工具执行可约束、可观测、可独立授权，社区对安全设计关注度上升。
- **多提供商兼容性打磨**: 密集的 Anthropic 转换器修复（#8159-#8162、#8163）与本地模型（#8146）问题暴露转换层细节完善仍是刚需。
- **跨端（桌面 / CLI / Windows）补齐**: #8132 的 Desktop 落地、#7957 的 Windows 粘贴、#8050 的 Windows 测试设施，跨平台产品化和稳定性同步推进。
- **Agent 行为可配置化**: #8171（后台 agent 轮次限制）、#8005（Goal v3 落地 TUI）显示社区更希望自主控制 Agent 行为的生命周期参数。

---

## 6. 开发者关注点

- **UI 渲染稳定性**（#8124、#8113、#8131）: 终端 TUI 与 VP 模式渲染 Bug 集中在 Windows + 特定终端模式组合下，期待针对性修复。
- **Session / Worktree 语义准确性**: 多会话切换（#8172）、worktree 配置归属（#8138、#8152）仍是高频痛点，反映出 Git 工作流复杂化的现实需求。
- **崩溃与诊断能力**: 0.21.1 的崩溃反馈表明缺少异常兜底与日志可读性（#7972），#8088 的做法（先保证可见性）是现阶段务实方向。
- **CI 频繁失败与 flaky 测试**: 本轮 3 条 E2E 失败反馈（#8153、#8133、#8072/8076 等）挂起「等待自动修复」，机器人大量介入，侧面暴露测试基线的稳定性问题。
- **配置与凭据安全**: #8136 的凭据泄漏是安全红线，且在清洗逻辑引入新 bug（消息被截断），强调对用户输入必须建立更严格的规范化处理测试。

---

> 日报基于 GitHub 公开数据整理，统计区间以标注时间为准。内容仅供社区交流参考。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-07-31** | **数据来源：** [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)

> **提示：** 项目已正式更名为 **CodeWhale**（产品代号），原 `deepseek-tui` npm 包已弃用。以下内容反映更名后的主仓库动态。


## 1. 今日速览

项目正式进入 **v0.9.2 收尾与 v0.9.3 架构重构的交替期**：一方面发布 v0.9.2 最终版本（含大量 TUI 体验修复），另一方面十余个 v0.9.3 重构 EPIC 正密集推进，核心矛盾指向 **TUI 单 crate 膨胀（14,878 行 main.rs）** 与 **运行时架构收敛**。社区侧高频痛点集中在 **编译耗时过长**、**配置路径跨平台不一致**（Windows/Cygwin）、以及 **高频 Anthropic API 400 错误**。


## 2. 版本发布

### [v0.9.2](https://github.com/Hmbown/CodeWhale/releases)（昨日发布）

- **品牌更名**：产品正式定名 **CodeWhale**（Shannon Labs），`codewhale` 为唯一官方命令名和包名。
- **弃用声明**：旧版 npm 包 `deepseek-tui` 正式弃用，不再接收任何更新。
- **兼容提示**：v0.8.x 时代遗留的 `deepseek` / `d...` 命令需迁移至 `codewhale`。

> 该版本同时合入了一批修复（见 #4982 PR）：权限判定、Fleet 持久化、推理面板、压缩错误、沙箱真值、凭据 UX、环境生物剪影等。


## 3. 社区热点 Issues（TOP 10）

### ★ 编译性能与架构（热度最高）
- **[#4991] Discussion: Compilation times and the TUI crate monolith** — [链接](https://github.com/Hmbown/CodeWhale/issues/4991)
   作者 `aboimpinto` 在推进 slash 命令重构时频繁等待编译，发起讨论。直指 18 个 Rust 包、771k 行代码中 87% 集中于 TUI crate 的现状，是 v0.9.3 架构重构的直接推动力。

- **[#2870] EPIC: staged command-boundary refactor** — [链接](https://github.com/Hmbown/CodeWhale/issues/2870)
   19 条评论，v0.9.3 核心重构的追踪 EPIC，拆分多个可独立合并的子 PR，目前已推进至 Layer 5.2（见 #4992 PR）。

### ★ 跨平台可靠性
- **[#2369] Config Paths Fragmented Across OS and Cygwin** — [链接](https://github.com/Hmbown/CodeWhale/issues/2369)
   配置/密钥路径在 Windows 与 Cygwin 下解析规则不同，且遗留迁移存在静默丢失风险。直接影响 Windows 开发者采用意愿。

### ★ 产品定义
- **[#4022] v0.9.3: define CLI/TUI parity for subagent control surfaces** — [链接](https://github.com/Hmbown/CodeWhale/issues/4022)
   防止子代理控制能力被困死在 TUI 内。为未来云应用和远程工作台铺路，是产品从终端走向平台的必要步骤。

- **[#4906] Show, don't tell: record a real Codewhale session** — [链接](https://github.com/Hmbown/CodeWhale/issues/4906)
   官网和 README 缺少产品实际运行的 GIF/视频。终端代理本质是视觉化产品，纯文字描述显著拉高理解门槛。

### ★ 质量与一致性
- **[#4949] The Chinese Translation of "Constitution"** — [链接](https://github.com/Hmbown/CodeWhale/issues/4949)
   中文社区就 "Constitution" 翻译（"宪法" vs "协作准则"）产生分歧，涉及政治敏感度与准确性权衡，属于本地化过程中的典型文化碰撞案例。

### ★ 上下文与 Token 优化
- **[#4704] Context diet: minimize every model-facing prompt** 及子任务 **[#4709]**、**[#4710]**、**[#4707]** — [链接](https://github.com/Hmbown/CodeWhale/issues/4704)
   系统性减少每个面向模型的字节：稳定提示词重复（约 29 KB 常量）、技能重复扫描、冗余上下文堆叠等。目标不仅是省 token，更是提升跨模型可移植性。

### ★ 桌面端探索
- **[#4986] feat(desktop): first-class desktop app** — [链接](https://github.com/Hmbown/CodeWhale/issues/4986)
   社区成员提出参考 Codex Desktop 打造完整桌面体验，说明终端之外的产品形态需求开始浮现。

### ★ 高频报错
- **[#4978] Anthropic API error: 'type' must be in [\"enabled\", \"disabled\", \"auto\"]** — [链接](https://github.com/Hmbown/CodeWhale/issues/4978)
   使用兼容层（OpenModel）时高频出现 HTTP 400，重试可过但无固定规律，排查优先级较高。


## 4. 重要 PR 进展（TOP 10）

### 合并类（CLOSED）

- **[#4982] release: finalize Codewhale v0.9.2** — [链接](https://github.com/Hmbown/CodeWhale/pull/4982)
   v0.9.2 收官合入，涵盖权限真值、Fleet 持久化、推理检查、压缩错误、沙箱真值等一批修复。

- **[#4984] fix runtime config persistence and workspace task scoping** — [链接](https://github.com/Hmbown/CodeWhale/pull/4984)
   修复运行时配置持久化 + 任务按 workspace 过滤，为 GUI 前端铺路。

- **[#4979] fix(tui): detach foreground shell before steering** — [链接](https://github.com/Hmbown/CodeWhale/pull/4979)
   修复前台 Bash 阻塞时用户输入 Enter 的困惑行为：先转移至 `/jobs` 再接受转向指令。

- **[#4942] fix(tools): preserve CRLF edits** — [链接](https://github.com/Hmbown/CodeWhale/pull/4942)
   修复 Windows 下 `edit_file` 破坏 CRLF 换行的问题。

- **[#4896] move terminal clipboard writes off event loop** — [链接](https://github.com/Hmbown/CodeWhale/pull/4896)
   将 OSC 52/SSH/tmux 剪贴板写入移至独立后台 worker，避免阻塞 TUI 事件循环。

- **[#4856] fix(tui): expose every shipped locale in settings** — [链接](https://github.com/Hmbown/CodeWhale/pull/4856)
   补齐 `ko`、`vi`、`zh-Hant` 三个缺失语言选项。

- **[#4852] fix(config): align root model fallback with TUI** — [链接](https://github.com/Hmbown/CodeWhale/pull/4852)
   修复根级默认模型在配置层与 TUI 请求路径不一致的问题（DeepSeek 路由行为不变）。

- **[#4742] fix(workflow): preserve hashes in fleet strings** — [链接](https://github.com/Hmbown/CodeWhale/pull/4742)
   修复 fleet 解析器误将引号内 `#` 当注释起始的问题。

- **[#4680] fix(tui): register debt compatibility aliases** — [链接](https://github.com/Hmbown/CodeWhale/pull/4680)
   `/slop` 与 `/canzha` 注册为 `/debt` 正式别名，统一注册表。

### 开放中（OPEN）

- **[#4992] Layer 5.2: User command dispatch precedence** — [链接](https://github.com/Hmbown/CodeWhale/pull/4992)
   为自定义命令的遮蔽与回退语义补齐 Gherkin 验收测试（AT-004 至 AT-007）。

- **[#4990] fix(devcontainer): support Windows development** — [链接](https://github.com/Hmbown/CodeWhale/pull/4990)
   修复 Windows 下 devcontainer 因 HOME 挂载导致的 Rust 工具链缺失问题。

- **[#4977] fix(tui): let AltGr-typed \"/\" reach the composer** — [链接](https://github.com/Hmbown/CodeWhale/pull/4977)
   修复巴西 ABNT2 布局下输入 `/` 误触帮助面板的问题（AltGr 被识别为 Ctrl+Alt）。


## 5. 功能需求趋势

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **架构收敛与单二进制分发** | #3306, #3948, #4747 | 目标拆解 14,878 行 main.rs，消灭双 registry 并存，最终实现单可执行文件 |
| **上下文精简（Context Diet）** | #4704, #4709, #4710, #4707 | 系统性削减稳定提示词冗余（约 29 KB）、技能重复扫描、按需加载上下文；建立跨模型消融测试门禁 |
| **跨平台一致性** | #2369, #4990, #4977 | Windows/Cygwin 路径解析、AltGr 键位冲突、CRLF 保真——Windows 开发者体验持续被关注 |
| **CLI/TUI 能力对齐** | #4022 | 防止子代理控制被困在 TUI，为未来云应用和远程工作台铺路 |
| **桌面端产品形态** | #4986 | 社区开始探索 TUI 之外的完整桌面体验（参考 Codex Desktop），但尚未获得官方倾向性回应 |
| **低层级代币/路由修复** | #4978, #4852 | 兼容层 API 错误、根模型回退不一致——说明多模型路由稳定性仍待打磨 |


## 6. 开发者关注点

1. **编译耗时长**（#4991）：核心开发者亲诉等编译之苦，是 v0.9.3 单 crate 拆分的最直接动因，也是社区共识最高的痛点。
2. **配置与密钥跨环境不一致**（#2369）：Windows 与 Cygwin 下路径解析规则分裂，迁移过程存在静默丢失风险，对多平台用户信任度影响较大。
3. **技能扫描性能**（#3921）：每次 prompt 构建都进行多根递归全量扫描（深度 8 + canonicalize），数据却极少变化——典型性能反模式。
4. **当前台命令阻塞时转向困难**（#4930）：用户直觉操作（输入文字并回车）会得到困惑反馈，现已在 #4979 中修复。
5. **兼容层 API 稳定性**（#4978）：Anthropic 兼容端点高频 400 错误，影响非官方模型提供方用户。
6. **官方文档与演示不足**（#4906）：纯文字无法有效传达产品视觉体验——这可能是新用户流失率高的原因之一。

---

*本日报由 AI 自动生成，数据截至 2026-07-31 上午。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*