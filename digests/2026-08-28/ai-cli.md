# AI CLI 工具社区动态日报 2026-08-28

> 生成时间: 2026-08-28 07:19 UTC | 覆盖工具: 9 个

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

**报告日期：2026-08-28**


## 一、生态全景

AI CLI 工具已从"代码补全终端"进化为"具备安全边界、记忆系统、MCP 生态和远程协作能力的智能代理运行时"。今日 8 款主流工具（Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI）同步释放了约 50 条 Issue、30+ PR 和 10+ 版本更新，呈现出两个鲜明特征：**一是 Windows 平台兼容性问题在多个工具中集中爆发**（Codex 无头启动、Claude Code 路径大小写、Qwen 本地命令失效），成为跨工具的头号公敌；**二是安全边界与 Agent 自主性之间的张力成为共同主线**——Claude Code 推出 `--restricted` 受限模式、Copilot CLI 遭遇 MCP 协议升级回归、Gemini CLI 处理 Git 环境变量消毒、OpenCode 修复证书信任机制，各工具都在重新划定 AI 代理的"可行动边界"。

市场竞争格局上，**Claude Code 社区体量仍居首位**（单日 Top Issue 评论 110 条、👍 395），但 OpenAI Codex 以每日 4-5 个 Rust 版本的迭代速度显示出最强工程执行力。Gemini CLI 和 Qwen Code 均在推进架构级重构（前者统一文件系统抽象、后者迁移 TUI 渲染层），体现出二线工具为争夺开发者心智正在加速技术补课。Anthropic 在模型输出质量上遭遇的社区信任危机（#77136，持续一个半月未修复）可能是未来数月生态格局变化的最大变量。


## 二、各工具活跃度对比

| 工具 | 今日版本 | Issues（Top 10 区间） | PR（Top 区间） | 社区热度指标 | 迭代速度 |
|------|----------|----------------------|----------------|-------------|----------|
| **Claude Code** | v2.1.248/250（2 个补丁） | 10 条，Top 评论 110/👍395 | 1 条（PR 池较小） | 🔥🔥🔥🔥🔥 最大社区体量 | 中速（日常补丁） |
| **OpenAI Codex** | 4 个 Rust 版本（alpha.6-8） | 10 条，Top 评论 36 | 10 条（8 合入） | 🔥🔥🔥🔥 增长迅猛 | 极快（每日多版） |
| **Gemini CLI** | 1 个 nightly | 10 条，Top 评论 13/👍8 | 10 条（9 修复类） | 🔥🔥🔥 技术社区活跃 | 中速，P1 积压 |
| **GitHub Copilot CLI** | v1.0.81 正式版 | 10 条，Top 评论 12/👍12 | 0 条（今日无 PR） | 🔥🔥🔥 企业用户盘大 | 中速，发布后修复期 |
| **Kimi CLI** | 无 | 6 条，评论区间 0-3 | 3 条（2 修复/1 安全） | 🔥 社区规模较小 | 慢速 |
| **OpenCode** | v1.18.24/25（2 个补丁） | 10 条，Top 评论 41/👍43 | 10 条（8 活跃推进） | 🔥🔥🔥 社区黏性强 | 中高速 |
| **Pi** | 无（v0.84.3 修复期） | 10 条，Top 评论 14/👍14 | 10 条（9 合并） | 🔥🔥 本地模型用户忠诚 | 中速，集中修复 |
| **Qwen Code** | v0.22.2-nightly | 10 条，Top 评论 13/👍1 | 10 条（全部活跃） | 🔥🔥🔥 国内社区强劲 | 高速（多线并行） |
| **DeepSeek TUI** | 无（v0.9.12 收尾） | 10 条，Top 评论 9 | 10 条（9 合并） | 🔥🔥 小而精 | 中速，发布窗口期 |


## 三、共同关注的功能方向

**1. AI 代理的安全边界（5 个工具）**
- Claude Code：新增 `--restricted` 受限模式 + 社区强烈要求 Remote Control 默认关闭（#90179）
- Gemini CLI：Git 环境变量消毒（PR #28938）、不受信任环境过滤 mcpServers（PR #29099）
- OpenCode：按 MCP 服务器维度配置证书信任（PR #40125）
- Kimi CLI：asyncssh 漏洞修复（PR #2622）
- Qwen Code：Anthropic 线路缺少流式安全保护（#9005）

**2. 压缩/上下文管理的可靠性（4 个工具）**
- Copilot CLI：自定义模型压缩 400 错误（#4646）、低上下文触发压缩且 checkpoint 不一致（#4643）
- Pi：压缩可配置思考级别（#7553）、压缩摘要重试机制（PR #6848）
- DeepSeek TUI：上下文压力警告瞬态化、Agent 不行动（#5620）、token 记账单遍优化（#5665）
- Claude Code：社区持续反馈模型输出质量退化（#77136）

**3. Windows 平台兼容性（5 个工具，已在前言详述）**
- Codex（无头启动、认证丢失、MCP 路径失效）、Claude Code（反斜杠/大小写/签名）、Qwen（本地命令失效）、Pi（shell 路径、PowerShell）、OpenCode（PowerShell 5.1 误用）

**4. 子代理与状态报告真实性（3 个工具）**
- Gemini CLI：子代理达到 MAX_TURNS 误报 success（#22323）、浏览器代理误报 GOAL（#21983）
- Claude Code：后台任务静默 KILL（#84625）
- Qwen Code：工具调用结果对 Moonshot 供应商的 schema 不兼容（#10227）

**5. MCP 协议升级带来的破坏性变更（3 个工具）**
- Copilot CLI：v1.0.81 升级 MCP 2026-07-28 协议后 chroma-mcp 集成失败（#4647）
- OpenCode：同步升级 MCP SDK 2.0（PR #45777）
- Gemini CLI：read_file 绕过 FileSystemService，影响 ACP 客户端（PR #29110）


## 四、差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线特征 | 护城河 |
|------|----------|----------|-------------|--------|
| **Claude Code** | 全能型 AI 编码代理 | 全栈开发者、企业团队 | 功能持续加码，逐步收敛为平台（Remote Control/受限模式/技能系统） | 模型能力 + 社区生态体量 |
| **OpenAI Codex** | 高性能编码代理 | 追求新功能的早期采用者 | Rust 重写，高频迭代 0.15x-alpha 快速试错，桌面端为重 | 发布速度 + 与 ChatGPT 生态绑定 |
| **Gemini CLI** | 多 Provider 本地优先代理 | 技术敏感型开发者、GCP 用户 | 强调子代理/技能/内存系统，架构重构（统一文件系统、ACP） | 模型多模态能力 + 企业级 GCP 集成 |
| **GitHub Copilot CLI** | 安全合规的编码副驾 | 企业开发团队、GitHub 深度用户 | 插件系统 + MCP 协议 + 托管策略（managedSettings），强调可观测性与审计 | GitHub 生态 + 企业管控能力 |
| **Kimi CLI** | 轻量 OpenAI 兼容代理 | Moonshot 生态用户、中小团队 | 功能精简，依赖 OpenAI 兼容协议 | Kimi 模型调用便利性 |
| **OpenCode** | 可配置的桌面/CLI 混合代理 | 桌面端重度用户、Go 套餐订阅者 | 桌面应用 + TUI 双界面，自动更新机制，强调 UI 体验 | Go 计费套餐 + 桌面端体验 |
| **Pi** | 本地模型优先的终端代理 | 本地模型爱好者、隐私敏感用户 | TypeScript 单仓，强调与 llama.cpp/Ollama 的兼容性，TUI 体验 | 本地模型生态兼容性 |
| **Qwen Code** | 多语言多平台的全栈代理 | 国内开发者、阿里云用户 | 多语言 SDK 体系 + 钉钉/飞书渠道集成 + TUI 重构（OpenTUI） | 阿里云生态 + 国内渠道整合 |
| **DeepSeek TUI** | Rust 极简 TUI 代理 | Rust 开发者、终端纯粹主义者 | 单体大 crate，正在走向 Provider 中立化 + crate 拆分 | 极简终端体验 + Rust 性能 |

**核心差异维度：**
- **模型关系**：Claude/Codex/Copilot 与自有模型深度绑定；Gemini 多 Provider；Kimi/Qwen 拥抱自家模型但兼容 OpenAI 协议；Pi/DeepSeek TUI 主打模型中立。
- **界面范式**：Claude Code 纯 CLI；Codex/Copilot 转向桌面端优先；OpenCode 双界面并行；Pi/DeepSeek TUI 坚守终端美学。
- **部署模式**：Copilot 强调企业托管策略；Qwen 强调 IM 渠道（钉钉）；Codex 强调 daemon 与远程控制。


## 五、社区热度与成熟度

**指标说明**：以下热度指数综合 Issues 评论数、👍 数、PR 活跃度、版本发布频率计算，★ 越多代表越活跃。

| 工具 | 社区体量 | 迭代活跃度 | 反馈闭环效率 | 成熟度阶段 |
|------|----------|-----------|-------------|-----------|
| **Claude Code** | ★★★★★（110 评论/395👍） | ★★★☆ | ★★★☆ 长期 Issue 积压 | 成熟期：功能全面，但社区信任出现裂缝 |
| **OpenAI Codex** | ★★★★（36 评论/2👍） | ★★★★★ 每日 4-5 版本 | ★★★★★ 响应迅速 | 快速扩张期：工程执行力最强，但稳定性受质疑 |
| **Gemini CLI** | ★★★☆（13 评论/8👍） | ★★★★ 多线推进 | ★★★★ P1 处理积极 | 成长期：架构重构中，功能潜力大 |
| **GitHub Copilot CLI** | ★★★★（12 评论/12👍） | ★★★☆ 发布后修复期 | ★★★★ 企业渠道反馈快 | 稳定期：企业管控需求明确 |
| **Kimi CLI** | ★★（评论 0-3） | ★★☆ | ★★★ | 早期阶段：社区规模尚小 |
| **OpenCode** | ★★★★（41 评论/43👍） | ★★★★ 10 PR 并行 | ★★★★ | 成长期：社区黏性强，但计费信任受损 |
| **Pi** | ★★★（14 评论/14👍） | ★★★★ 集中修复 | ★★★★★ 当日修复当日合并 | 成长期：维护者反应极快 |
| **Qwen Code** | ★★★★（13 评论/1👍） | ★★★★★ 多 PR 并行 | ★★★★ | 快速成长期：多线同步推进 |
| **DeepSeek TUI** | ★★☆（9 评论） | ★★★☆ 发布窗口期 | ★★★★ 24h 内修复 | 成长期：小而精，正在架构转型 |

**重要观察**：Claude Code 社区规模目前仍是第二名的近 3 倍（以 Top Issue 评论数为参照），但其"模型输出质量下滑 + 跨平台兼容性问题"若持续未解，存在被 Codex/Qwen 等高效迭代工具分流用户的风险。


## 六、值得关注的趋势信号

**1. 安全边界正在成为 AI CLI 的标配能力（关键信号）**
- Claude Code v2.1.248 推出 `--restricted` 受限模式 + Gemini 过滤 mcpServers + OpenCode 服务器级证书信任 + Kimi 依赖漏洞修复——四款工具同周落地安全机制。这标志着 AI CLI 正从"开发者的效率工具"转向"企业级代理运行时"，安全能力将成为选型新门槛。

**2. Windows 平台是 2026 年下半年的必争之地（警示信号）**
- 今日 5 款工具集中暴露 Windows 兼容问题：Codex 无头启动、Claude Code 路径大小写、Qwen 本地命令失效、Pi shell 路径错乱、OpenCode PowerShell 误用。Windows 开发者基数庞大但 AI CLI 的 Windows 适配普遍滞后，"谁能率先解决 Windows 体验，谁将获得显著的增量市场"，反之 Windows 问题可能成为社区口碑崩塌的导火索。

**3. 子代理/多 Agent 架构的"状态真实性"问题浮出水面（技术信号）**
- Gemini（#22323/#21983）与 DeepSeek TUI（#5620）均出现"AI 错误报告任务成功"或"压力信号不触发行动"。这指向 Agent 自主性的深层矛盾——模型缺乏对其运行状态（轮次限制、上下文压力、环境约束）的自我感知与诚实汇报机制。**具备"元认知能力"（能感知并如实报告自身状态限制）的 Agent 会成为下一轮差异化竞争力。**

**4. 社区对"自动更新"的反感正在与"安全性"叠加（信任信号）**
- Copilot（#26011 MCP 路径失效）、Codex（#40969 daemon 强杀活跃 turn）、OpenCode（#45087 266GB 磁盘消耗）、Qwen（#10147 本地命令失效）——自动更新破坏环境已成为跨工具公敌。**提供可控的回滚、延迟更新或分阶段发布机制，将成为影响企业用户信任度的重要因素。**

**5. 模型输出质量的下滑是少数派报告但影响深远（隐忧信号）**
- Claude Code #77136（110 评论/395👍）表明用户对模型写作风格的退化高度敏感。当 CLI 工具的能力上限受制于 API 模型的输出质量时，工具团队需要建立"模型行为护栏"（如风格锁定、repeat 检测），这可能是新的工具层价值点。

**对开发者的参考价值：**
- **选型建议**：追求稳定与生态 → Claude Code（但关注模型质量动向）；追求新特性与快速迭代 → OpenAI Codex；本地模型优先 → Pi；企业合规与安全管控 → GitHub Copilot CLI；国内 IM 集成 → Qwen Code。
- **风险提醒**：升级节奏放缓——多工具近一周的自动更新均出现兼容性问题，建议延期 2-3 天跟进大版本（如 Codex 26.820、Copilot v1.0.81）。
- **参与建议**：各社区的 P1 级 Issue 响应效率已明显提升（Pi/Gemini/Codex 均实现 24 小时内修复合并），积极提交高质量 Issue 是影响工具发展方向的最短路径。

---

*报告基于各工具公开 GitHub 数据（2026-08-27 至 08-28），仅供参考，不代表各官方立场。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-28）

---

## 一、热门 Skills 排行

按 PR 评论数排序，以下为社区关注度最高的 Skills：

### 1. skill-creator 修复（#1298）— **open**
- **功能**：修复 `run_eval.py` 在所有环境下永远报告 0% recall 的严重 bug（关联 #556，10+ 独立复现）。修复内容包括：将 eval artifact 安装为真正的 skill、修复 Windows 流读取、触发检测逻辑及并行 worker 问题。
- **讨论热点**：这是目前社区最关注的 PR，直接关系到 skill-creator 的 eval 循环是否可信，影响所有依赖该工具的 skill 优化流程。
- 🔗 https://github.com/anthropics/skills/pull/1298

### 2. document-typography（#514）— **open**
- **功能**：为 AI 生成的文档提供排版质量控制——孤词换行（1-6 个词溢出到下一行）、孤行段落（节标题悬在页底）和编号错位。
- **讨论热点**：解决了 AI 生成文档的普遍痛点，社区讨论聚焦于其对多格式（docx/pdf/md）的适配范围。
- 🔗 https://github.com/anthropics/skills/pull/514

### 3. scnet-hpc（#1615）— **open**
- **功能**：通过 profile-based SSH 和 Slurm 工作流操作 SCNet HPC 集群，覆盖连接、分区、内存、模块、加速器配置及作业生成。
- **讨论热点**：HPC 社区的科研用户关注度高，讨论集中在集群环境差异化和安全性。
- 🔗 https://github.com/anthropics/skills/pull/1615

### 4. ODT skill（#486）— **open**
- **功能**：OpenDocument 格式（.odt/.ods）的创建、填充、读取及转换为 HTML，触发词覆盖"ODT/ODS/ODF/OpenDocument/LibreOffice"。
- **讨论热点**：填补了官方文档 skills 中缺少 LibreOffice/ISO 标准格式支持的空缺。
- 🔗 https://github.com/anthropics/skills/pull/486

### 5. pdf 大小写敏感修复（#538）— **open**
- **功能**：修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配的文件引用（`REFERENCE.md` → `reference.md` 等），保证在大小写敏感文件系统上正常工作。
- **讨论热点**：虽为 bug-fix，但暴露了仓库中普遍存在的跨平台兼容性问题。
- 🔗 https://github.com/anthropics/skills/pull/538

### 6. docx tracked change ID 冲突修复（#541）— **open**
- **功能**：修复当 DOCX 文档已有书签时，添加 tracked changes 导致的文档损坏——OOXML 中 `w:id` 在书签、修订、批注、移动区间间共享 ID 空间，硬编码低 ID 会冲突。
- **讨论热点**：涉及 OOXML 规范细节，维护者和社区讨论了 ID 分配策略的通用解决方案。
- 🔗 https://github.com/anthropics/skills/pull/541

### 7. frontend-design skill 改进（#210）— **open**
- **功能**：提升 frontend-design skill 的清晰度、可操作性和内部一致性，确保每条指令 Claude 可在单次对话中实际执行。
- **讨论热点**：反映了社区对 skill 质量的核心诉求——不只写给人看，更要让模型可执行。
- 🔗 https://github.com/anthropics/skills/pull/210

---

## 二、社区需求趋势

### 1. 安全与信任边界（#492，43 条评论）— **最高热度**
社区 skill 在 `anthropic/` 命名空间下分发，导致用户可能向非官方 skill 授予特权。这是当前最尖锐的生态问题，直接关联到 skill 分发的信任模型。

### 2. 组织级 skill 共享（#228，16 条评论）
用户要求支持组织内直接共享 skill，而非手动下载 .skill 文件再通过 Slack/Teams 分发的低效流程。这反映了 skill 从个人工具走向团队协作工具的需求。

### 3. Skill 优化工具链可靠性（#556，12 条评论）
`run_eval.py` 的 0% 触发率 bug 引发广泛关注——如果评估工具不可信，整个 skill 迭代循环都建立在错误信号之上。这直接催生了 #1298 等修复 PR。

### 4. 新 skill 方向集中于：**agent 治理与安全**（#412）、**紧凑记忆管理**（#1329）、**MCP 暴露 Skills**（#16）
社区对新 skill 的期待从"功能型"（如文档、游戏）转向"系统型"——关注 agent 自身的行为约束、状态管理以及与外部工具的标准接口。

### 5. Skill 重复安装问题（#189）
`document-skills` 和 `example-skills` 插件包含相同内容，安装后造成上下文窗口重复占用——指向 skill 生态的包管理治理需求。

---

## 三、高潜力待合并 Skills

以下 PR 评论活跃但尚未合并，近期落地可能性较高：

| Skill | PR | 亮点 | 链接 |
|---|---|---|---|
| **Hivemind 多智能体编排** | #1628 | 让 Claude Code 将机械性工作委派给 headless opencode worker（免费模型），Claude 保持规划/审查/合并角色。核心洞察：昂贵的模型上下文才是稀缺资源。 | https://github.com/anthropics/skills/pull/1628 |
| **skill-quality-analyzer + skill-security-analyzer** | #83 | 两个元 skills：质量分析器从结构/文档/示例/资源/安全五个维度评估 skill；安全分析器提供安全审计能力。直接回应了 #492 的安全关切。 | https://github.com/anthropics/skills/pull/83 |
| **self-audit** | #1367 | 交付前审计 skill——先做机械性文件验证，再按"损害严重度优先级"执行四维推理审计。跨项目、跨技术栈、跨模型通用。 | https://github.com/anthropics/skills/pull/1367 |
| **testing-patterns** | #723 | 覆盖完整测试栈：Testing Trophy 模型、单元测试 AAA 模式、React 组件测试（Testing Library）等。 | https://github.com/anthropics/skills/pull/723 |
| **ServiceNow 平台 skill** | #568 | 覆盖 ITSM、ITOM、ITAM/SAM、FSM、HRSD、CSM、SPM、漏洞响应等全平台能力。更新跨度达 5 个月，维护主动。 | https://github.com/anthropics/skills/pull/568 |
| **Pyxel 复古游戏开发** | #525 | 为 Pyxel 复古引擎提供 MCP 集成的 skill，覆盖"编写 → 运行捕获 → 检视 → 迭代"完整工作流。 | https://github.com/anthropics/skills/pull/525 |

---

## 四、Skills 生态洞察

> **当前社区最集中的诉求是：让 skill 的"生产工具链"本身变得可信——评估脚本可靠、跨平台兼容、无安全边界漏洞；同时从"单点功能 skill"向"agent 行为治理、编排与上下文效率"的系统级 skill 演进。**

---

# Claude Code 社区动态日报 — 2026-08-28

> 数据来源：[anthropics/claude-code](https://github.com/anthropics/claude-code) | 统计时间：近 24 小时


## 一、今日速览

今日发布两个补丁版本（v2.1.248 / v2.1.250），其中 **v2.1.248 新增 `--restricted` 受限模式**，移除命令执行类内置工具与 WebFetch，并强制忽略用户级配置，是安全加固方向的重要信号。社区侧值得关注的是 **“Remote Control 安全与隐私”成为当日最热议题**（默认开启、设备验证失效等），同时 Windows 平台（Git Bash 反斜杠、打包签名、大小写路径比较）集中暴露了多个跨平台兼容问题。


## 二、版本发布

### v2.1.250（最新）
- 缺陷修复与可靠性改进，无新功能说明。

### v2.1.248
- **新增 `--restricted` 受限模式**（环境变量 `CLAUDE_CODE_RESTRICTED=1`）：
  - 移除可执行命令/代码的内置工具及 `WebFetch`（除非在 `--tools` 中显式声明）；
  - 文件工具仅限工作目录内使用；
  - **拒绝 `bypassPermissions`**；
  - **忽略用户级、项目级、本地级 settings 文件**。

> 意义：这是面向沙箱/高安全场景的官方受限模式，适用于 CI 或不可信代码仓库扫描场景。

🔗 [查看 v2.1.250 Release](https://github.com/anthropics/claude-code/releases) | [查看 v2.1.248 Release](https://github.com/anthropics/claude-code/releases)


## 三、社区热点 Issues（Top 10）

### 1. 模型输出质量持续恶化：重复修辞、文风僵化（评论 110 / 👍 395）
[#77136](https://github.com/anthropics/claude-code/issues/77136)
Claude 4.7/4.8/5.0 及 Fable 在多模型上出现重复性修辞套话，即便给出明确风格指令仍难以产出连贯文本。这是当前社区**反馈最激烈、讨论最多**的 Issue，已持续一个半月。

### 2. Remote Control 自动重连失效，连接静默断开（评论 69 / 👍 106）
[#34255](https://github.com/anthropics/claude-code/issues/34255)
macOS/iOS 平台 Remote Control 会话断开后不自动恢复，无任何提示。远程协作场景下的核心稳定性痛点，社区呼声极高。

### 3. 新增 Word（.docx）修订模式编辑支持（评论 26 / 👍 30）
[#9631](https://github.com/anthropics/claude-code/issues/9631)
用户无法读写 .docx 或使用“修订”功能。文档协作场景的核心功能缺失，已开放近一年仍无排期。

### 4. Read 工具 PDF 支持依赖 poppler-utils 但未文档化（评论 17 / 👍 20）
[#23704](https://github.com/anthropics/claude-code/issues/23704)
Read 工具宣称支持 PDF，但实际依赖容器中通常未安装的 `pdftoppm`，且安装后不会热加载。**文档与实现不一致**，影响容器化开发环境。

### 5. Code 标签页将 UI 渲染元数据写入 transcript，导致 API 400（评论 11）
[#90002](https://github.com/anthropics/claude-code/issues/90002)
Windows 平台：UI 元数据（时间戳/flags）污染 transcript JSONL，清洗数据后仍然报错且不可恢复，Sandbox 数据管线的可靠性问题。

### 6. Windows Desktop 更新后 Slash 命令体验严重回退（评论 3 / 👍 2）
[#89628](https://github.com/anthropics/claude-code/issues/89628)
自动更新后：斜杠命令无联想 → 仅首位置可用 → 命令 Chip 样式丢失。桌面端 UI 回归问题，三连崩。

### 7. 后台 Bash 任务被静默杀死（评论 4）
[#84625](https://github.com/anthropics/claude-code/issues/84625)
`run_in_background: true` 长任务运行中途被静默 KILL，无 OOM、无用户操作、无会话报错。**setsid 分离进程不受影响** —— 说明是进程组级终止。

### 8. 隔离工作树路径大小写敏感比较导致 Windows 会话无法恢复（评论 2）
[#85234](https://github.com/anthropics/claude-code/issues/85234)
2.1.222 回归：Windows 上 IDE 启动的 worktree 会话无法 resume，CLI 直接退出 1。大小写敏感路径比较在 Windows 上不适用，NTFS 大小写不敏感导致。

### 9. Trusted Devices 验证失效：设备吊销后活动会话仍可继续（评论 2）
[#90265](https://github.com/anthropics/claude-code/issues/90265)
设备吊销后已验证会话不受影响；“重新验证设备”弹窗可被无效果关闭。**安全机制形同虚设**，Remote Control + Trusted Devices 双保险双双失效。

### 10. Remote Control 默认开启，用户未主动启用（评论 2 / 👍 2）
[#90179](https://github.com/anthropics/claude-code/issues/90179)
用户 `settings.json` 中无 remote 配置，但会话显示 Remote Control 可用。默认开启远程通道引发隐私担忧。

> 浏览全部 [Open Issues](https://github.com/anthropics/claude-code/issues?q=is%3Aissue+is%3Aopen)


## 四、重要 PR 进展

### 本次更新 PR（1 条）

#### frontend-design skill 更新
[#69226](https://github.com/anthropics/claude-code/pull/69226)（已关闭）
作者：williamqian12 | 更新：2026-08-27
- 改进 frontend-design skill 内容，插件版本升至 1.1.0；
- 已关闭（非合并）—— 需关注是否被采纳或另开 PR。

> 备注：本次数据窗口内仅捕获到 1 条 PR，其余时间窗外 PR 未纳入统计。


## 五、功能需求趋势

从全部 Issues 中提炼出当前社区的 TOP 功能诉求：

### 🔒 安全与隐私
- **Remote Control 默认关闭**，改为显式 opt-in（[#90179](https://github.com/anthropics/claude-code/issues/90179)）
- Trusted Devices 吊销后立即失效，重新验证不可跳过（[#90265](https://github.com/anthropics/claude-code/issues/90265)）
- 新增 `--restricted` 模式即是该方向的官方回应（v2.1.248）

### 📝 文档与 Office 生态
- **Word（.docx）修订模式**读写支持（[#9631](https://github.com/anthropics/claude-code/issues/9631)）
- PDF 依赖（poppler-utils）**文档化并自动检测**（[#23704](https://github.com/anthropics/claude-code/issues/23704)）

### 🖥️ IDE / VS Code 体验
- 会话内**内容级搜索**，而非仅标题搜索（[#77523](https://github.com/anthropics/claude-code/issues/77523)）
- **图片粘贴支持 Cmd+V**，无需 Shift 组合键（[#90286](https://github.com/anthropics/claude-code/issues/90286)）

### 🤖 MCP 与代理能力
- **企业 MCP Server 目录发现**，替代 Wiki/Slack 手工分享（[#64633](https://github.com/anthropics/claude-code/issues/64633)）
- 模型应优先使用已安装的专用 Skill，而非临时自写轮询脚本（[#90071](https://github.com/anthropics/claude-code/issues/90071)）

### 🎤 语音交互
- Cowork **全双工语音（输入+输出）**（[#90287](https://github.com/anthropics/claude-code/issues/90287)）

### 🖥️ 浏览器面板
- 用户应能**主动打开浏览器面板**，而非等待 Claude 创建会话（[#90284](https://github.com/anthropics/claude-code/issues/90284)）

### 💰 成本与激励
- 对贡献对话数据的用户提供**积分/成本减免激励**（[#90285](https://github.com/anthropics/claude-code/issues/90285)）


## 六、开发者关注点（痛点/高频反馈）

| 关注点 | 相关 Issue | 影响面 |
|---|---|---|
| **模型输出质量退化** | #77136（110 评论 / 395 👍） | 全平台，多模型，长期未修复 |
| **Remote Control 稳定性与安全** | #34255、#90179、#90265 | macOS/iOS/Windows，远程场景核心 |
| **Windows 平台兼容性** | #85856（反斜杠减半）、#85234（路径大小写）、#90283（签名失败）、#73338（文件打开回归） | Windows 为高发平台 |
| **后台任务可靠性** | #84625（静默 KILL）、#80093（daemon 45s 超时） | 长时间运行场景不可靠 |
| **沙箱/安全执行** | v2.1.248 `--restricted`、#90179 | 官方已响应，期待后续完善 |
| **Transcript/日志数据污染** | #90002（API 400 不可恢复） | 数据管线可靠性风险 |
| **UI/UX 回归** | #89628（Slash 命令）、#88542（终端标题动画）、#31561（VSCode 重复面板） | 桌面端与编辑器扩展体验 |

**一句话总结**：社区最迫切的声音是 **“模型写作质量下滑 + Remote Control 安全边界”**；官方今日的 `--restricted` 模式是对安全诉求的直接回应，但模型质量与 Windows 平台兼容性仍是待解难题。

---

*日报仅供参考，不代表 Anthropic 官方立场。链接均指向 GitHub Issue/PR 原文。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-28

## 今日速览
今日发布了 4 个 Rust 版本（0.151.0-alpha.6 至 alpha.8），更新节奏密集。社区反馈集中在 Windows 桌面端的**无窗口/无头启动**、**认证丢失**及**MCP 配置失效**等高频问题，同时多项针对生产力与权限控制的 PR（如 sleep tool gating、Guardian 上下文回滚）已合并。

## 版本发布
- **rust-v0.151.0-alpha.8 / alpha.7 / alpha.6**（`0.151.0-alpha.6` – `0.151.0-alpha.8`）：连续高频发布，具体变更未随 Release 说明披露，通常包含稳定性修复与内部功能迭代。建议关注 CLI 的 `--json` 事件流与 app-server 行为变化。 🔗 [查看 Releases](https://github.com/openai/codex/releases)
- **rust-v0.150.0-alpha.12.2**：作为 0.150 系列的补丁版本发布。 🔗 [查看 Release](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.12.2)

## 社区热点 Issues（Top 10）
1. **[Windows 26.820] Codex Desktop 无法启动：bundled codex.exe 从 WindowsApps 重定位失败** — #40700
   36 条评论、仅 2 👍，为当前最热 Issue。Windows 用户安装 Store 版后启动即崩溃，可能与 MSIX 打包权限有关。 ⚠️ [查看 Issue](https://github.com/openai/codex/issues/40700)

2. **[Windows] Codex Desktop 反复丢失认证（auth loop），ChatGPT Web 正常** — #41136
   4 条评论、1 👍。用户在 26.820.9563.0 版本上遇到 401 后无法恢复登录态。 🔗 [查看 Issue](https://github.com/openai/codex/issues/41136)

3. **[Windows] 升级后 ChatGPT Desktop 无头启动，无 renderer/window** — #41179
   10 条评论、0 👍。与 #41059 高度相似，均为升级至 26.820.9563.0 后无界面，可能共用同一回归根因。 🔗 [查看 Issue](https://github.com/openai/codex/issues/41179)

4. **[Windows] 首次启动约 15 分钟无窗口：解压 bundled cua_node runtime** — #41170
   6 条评论、0 👍。性能问题，长时间“假死”状态严重影响首次体验。 🔗 [查看 Issue](https://github.com/openai/codex/issues/41170)

5. **[Windows] 发送按钮无限旋转，prompts 无法提交** — #40968
   11 条评论、3 👍。Pro 用户反馈，阻断核心交互流程。 🔗 [查看 Issue](https://github.com/openai/codex/issues/40968)

6. **[macOS] Codex Desktop 认证循环持续；26.810.52044 回滚可修复** — #41044
   3 条评论、0 👍。跨平台认证回归，旧版本正常，说明 26.818/26.820 引入问题。 🔗 [查看 Issue](https://github.com/openai/codex/issues/41044)

7. **[Windows] 空白客户端区域；禁用 Direct Composition 可恢复渲染** — #40878
   5 条评论、1 👍。GPU 渲染层回归，与 26.820.7780.0 相关。 🔗 [查看 Issue](https://github.com/openai/codex/issues/40878)

8. **app-server daemon：自动更新在 60s drain 后强杀活跃 turn，且无法禁用** — #40969
   4 条评论、0 👍。长时间运行 remote-control daemon 的用户会遭遇任务中断。 🔗 [查看 Issue](https://github.com/openai/codex/issues/40969)

9. **config.toml MCP 路径在自动更新后失效，node_repl 报 os error 3** — #26011
   11 条评论、7 👍。老问题仍持续影响 Windows 用户，升级后路径未迁移。 🔗 [查看 Issue](https://github.com/openai/codex/issues/26011)

10. **Forked subagents 丢失 parent 的 prompt-cache lineage** — #24704
    5 条评论、17 👍。高赞性能问题，影响子代理任务成本与延迟。 🔗 [查看 Issue](https://github.com/openai/codex/issues/24704)

## 重要 PR 进展（Top 10）
1. **Add configurable gating for the sleep tool** — #41243（已合并）
    新增独立 `sleep_tool` feature，支持 `model_driven` 与 `always_on` 模式，与 clock tool 解耦。✅ [查看 PR](https://github.com/openai/codex/pull/41243)

2. **Forward history note images to the model** — #41292（开放中）
    将历史笔记中的图片转为 `input_image` 函数输出，供模型读取；图片数据不进入日志。✅ [查看 PR](https://github.com/openai/codex/pull/41292)

3. **Use compatible PowerShell for elevated Windows sandbox commands** — #41227（已合并）
    修复 Store PowerShell 在 `WindowsApps` 下对提权沙箱账号不可访问的问题。✅ [查看 PR](https://github.com/openai/codex/pull/41227)

4. **Honor turn token budgets in Guardian review rollover** — #41221（已合并）
    Guardian 回滚时使用父 turn 的 token 预算与模型默认配置，避免上下文超限。✅ [查看 PR](https://github.com/openai/codex/pull/41221)

5. **Include thread source in realtime connection metadata** — #41250（已合并）
    为 Realtime WebSocket 添加 `thread_source` 元数据，解决多 turn 语音来源识别问题。✅ [查看 PR](https://github.com/openai/codex/pull/41250)

6. **Expose the PowerShell version in environment context** — #41232（已合并）
    新增 `powershell_shell_version` feature flag，将 PowerShell 主/次版本注入 `<environment_context>`。✅ [查看 PR](https://github.com/openai/codex/pull/41232)

7. **Surface model provider authentication recovery progress** — #41239（已合并）
    新增 `modelProvider/authRecoveryStarted` 与 `authRecoveryCompleted` 事件，便于观测凭证刷新流程。✅ [查看 PR](https://github.com/openai/codex/pull/41239)

8. **Add recency sorting to `project/list`** — #41223（已合并）
    `project/list` 支持按 `recencyAt` 排序（默认降序），提升多项目切换体验。✅ [查看 PR](https://github.com/openai/codex/pull/41223)

9. **Sanitize history notes backend errors** — #41235（已合并）
    统一返回 `Unable to perform operation:` 消息，不再暴露底层错误细节，提升用户侧安全性。✅ [查看 PR](https://github.com/openai/codex/pull/41235)

10. **Share linked tool mention parsing in the TUI** — #41218（已合并）
    复用 mention codec 的解析器，删除重复实现，修复 Unicode 字节偏移问题。✅ [查看 PR](https://github.com/openai/codex/pull/41218)

## 功能需求趋势
- **Windows 稳定性成为第一优先级**：近 24 小时内一半以上 Issue 与 Windows 启动、渲染、认证、沙箱相关。社区对 26.820.x 系列回归容忍度明显下降，要求加快修复节奏。
- **认证与会话恢复**：跨平台（macOS/Windows）出现认证循环与 session 恢复失败，用户强烈期望稳定的 token 刷新与无感重连机制。
- **可观测性与控制**：多个 PR/Issue 关注 `--json` 事件流、认证恢复事件、插件缓存指标等，开发者希望获得更细粒度的运行时状态可见性。
- **Guardian / 安全机制增强**：PR 持续围绕 token 预算、上下文回滚、错误sanitization 展开，说明官方正强化长任务下的安全与稳定性保障。

## 开发者关注点
- **高频痛点：无头启动与白屏**：多个 Issue（#41059、#41179、#40878、#41170）均指向 26.820.9563.0 的渲染层与资源解压问题，用户被迫回滚或使用命令行 flag 规避。
- **自动更新破坏环境**：auto-update 导致 MCP 路径失效（#26011）、daemon 强杀活跃 turn（#40969），社区呼吁提供更新回滚或延迟更新机制。
- **沙箱与 PowerShell 兼容性**：针对 Store PowerShell 在提权沙箱下的不可用问题，已有 PR 修复，但用户期望更彻底的解决方案（如自动检测可用 Shell）。
- **性能与缓存**：Forked subagent 丢失 prompt-cache lineage（#24704，17 👍）是成本敏感用户的核心关切，直接影响长链任务执行效率。

> 如需追踪具体进展，建议关注 [openai/codex Issues](https://github.com/openai/codex/issues) 与 [Pull Requests](https://github.com/openai/codex/pulls) 页面。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-28**


## 今日速览

今日社区动态聚焦于**子代理（Subagent）稳定性** 与**内存系统（Auto Memory）安全性** 两大核心主题。多个 P1 级 Bug 仍在处理中，且社区对 Agent 的自主性（主动使用技能/子代理）与任务完成后的状态误报问题反馈尤为集中。此外，围绕 Git 环境安全及 MCP 生态的多个关键 PR 正在推进中，旨在修复潜在的安全隐患与一致性 Bug。


## 版本发布

**v0.59.0-nightly.20260828.g3c311beac**

- 发布内容：常规 nightly 版本发布
- 完整变更日志：[查看详情](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260827.g3c311beac...v0.59.0-nightly.20260828.g3c311beac)


## 社区热点 Issues

### 1. Subagent 达到 MAX_TURNS 后误报为成功（#22323）
- **标签**: priority/p1, kind/bug
- **作者**: matei-anghel | **评论**: 13 | **👍**: 2
- **摘要**: `codebase_investigator` 子代理在达到最大轮次限制后仍报告 `status: "success"`，将中断误报为成功，掩盖了实际未能执行分析的问题。
- **链接**: [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. 通用代理（Generalist agent）无响应挂起（#21409）
- **标签**: priority/p1, kind/bug
- **作者**: turmanticant | **评论**: 8 | **👍**: 8
- **摘要**: 当 Gemini CLI 将任务委派给通用代理时，会无限期挂起——即使是创建文件夹这类简单操作也会卡住长达一小时。用户发现通过指示模型“不要使用子代理”可规避问题。
- **链接**: [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. Gemini 对技能和子代理的使用率过低（#21968）
- **标签**: priority/p2, kind/bug
- **作者**: rnett | **评论**: 6 | **👍**: 0
- **摘要**: 用户反映 Gemini 在未明确指示时几乎从不主动使用自定义技能（如 gradle、git）和子代理，即使任务高度相关。这是 Agent 自主性的核心痛点。
- **链接**: [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 4. Shell 命令执行后卡在 “Waiting input”（#25166）
- **标签**: priority/p1, area/core, kind/bug
- **作者**: rnett | **评论**: 4 | **👍**: 3
- **摘要**: 在 Gemini 执行完简单的 CLI 命令后，终端会卡在 “Awaiting user input” 状态，但命令实际已完成。对极简单的命令也会触发，严重影响自动化流程。
- **链接**: [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 5. 自动内存对低信号会话无限重试（#26522）
- **标签**: priority/p2, kind/bug
- **作者**: SandyTao520 | **评论**: 5 | **👍**: 0
- **摘要**: Auto Memory 仅在提取代理成功读取会话时才标记为已处理，低信号会话会被反复呈现在索引中，导致后台提取代理无限重试，浪费资源。
- **链接**: [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 6. 自动内存的确定性脱敏与日志精简（#26525）
- **标签**: priority/p2, area/security, kind/bug
- **作者**: SandyTao520 | **评论**: 4 | **👍**: 0
- **摘要**: Auto Memory 读取本地记录并发送给模型处理，但脱敏指令在内容已进入模型上下文后才执行。且服务可能记录已存在的技能内容，存在敏感信息泄露风险。
- **链接**: [Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 7. 浏览器子代理在 Wayland 下失败（#21983）
- **标签**: priority/p1, agent/browser, kind/bug
- **作者**: sigmaSd | **评论**: 4 | **👍**: 1
- **摘要**: 在 Wayland 显示服务器环境下，浏览器子代理启动即失败，但报告显示 `Termination Reason: GOAL`——与 #22323 同为“误报成功”类问题。
- **链接**: [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 8. 工具数量超过 128 个时报 400 错误（#24246）
- **标签**: priority/p2, kind/bug
- **作者**: gundermanc | **评论**: 3 | **👍**: 0
- **摘要**: 当可用工具超过 400 个（注：标题写 128，正文写 400）时，Gemini CLI 报 400 错误。期望 Agent 能更智能地限制工具范围，而非简单报错。
- **链接**: [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)

### 9. 模型频繁在随机位置创建临时脚本（#23571）
- **标签**: priority/p2, kind/bug
- **作者**: galdawave | **评论**: 3 | **👍**: 0
- **摘要**: 当限制模型直接执行 shell 后，模型倾向于在多个目录中生成编辑脚本，造成工作区混乱，增加清理成本。
- **链接**: [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)

### 10. 工具超过数量的上限、进度报告可见性等（综合）
- 除上述外，`/chat share` 无法展示子代理轨迹（[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)）、浏览器 Agent 忽略 `settings.json` 配置（[#22267](https://github.com/google-gemini/gemini-cli/issues/22267)）等问题也受到较高关注。


## 重要 PR 进展

### 1. [修复] 移除不安全的 `diff.external` 覆盖（#28930）
- **标签**: priority/p1, area/core, size/m
- **作者**: sharonyao1127
- **摘要**: 修复此前 PR 添加的 `['diff.external', '']` 覆盖——Git 将空值视为“取消设置”，而非“禁用”，这可能导致意外行为。
- **链接**: [PR #28930](https://github.com/google-gemini/gemini-cli/pull/28930)

### 2. [修复] 保持 GIT_CONFIG_* 环境变量的内部一致性（#28938）
- **标签**: priority/p1, area/core, size/l
- **作者**: Shivansh1980
- **摘要**: 防止脱敏时删除了编号键/值对的一半，导致 Git 无法解析配置；同时确保 ShellExecutionService 不会在消毒后恢复敏感 Git 配置。
- **链接**: [PR #28938](https://github.com/google-gemini/gemini-cli/pull/28938)

### 3. [修复] 避免持久化“响应被中断”占位符（#28939）
- **标签**: priority/p1, area/agent, size/l
- **作者**: Shivansh1980
- **摘要**: 修复中断后模型可能复读 “[The previous response was interrupted...]” 占位符文本、污染后续对话的问题。
- **链接**: [PR #28939](https://github.com/google-gemini/gemini-cli/pull/28939)

### 4. [修复] read_file 经由 FileSystemService 读取（#29110）
- **标签**: area/agent, size/m, size/l
- **作者**: Abdullah-Builds
- **摘要**: `read_file` 直接从本地磁盘读取，忽略了已注入的 `FileSystemService`——与 `write_file`、`replace` 行为不一致。此问题会影响 ACP 客户端的文件系统抽象。
- **链接**: [PR #29110](https://github.com/google-gemini/gemini-cli/pull/29110)

### 5. [修复] SSE 流末尾无空行时丢失事件（#29106）
- **标签**: area/core, size/m
- **作者**: AnupamKumar-1
- **摘要**: 当流结束时无尾随空行（如连接截断），`finishReason` 和用量元数据会被静默丢弃——现在会正确刷新缓冲的最终事件。
- **链接**: [PR #29106](https://github.com/google-gemini/gemini-cli/pull/29106)

### 6. [修复] 严格布尔解析 DEBUG 环境变量（#28942）
- **标签**: area/platform, size/l
- **作者**: dylanyunlon
- **摘要**: Sandbox 启动器用 JS 字符串真值判断 DEBUG，导致 `DEBUG=false` 仍启用调试模式。修复为严格布尔解析。
- **链接**: [PR #28942](https://github.com/google-gemini/gemini-cli/pull/28942)

### 7. [修复] 避免 401 子字符串的误判认证错误（#28827）
- **标签**: priority/p2, area/core, size/s
- **作者**: mikemikimike
- **摘要**: 修复 `isAuthenticationError` 将包含 “401” 的无关注值（如端口号、退出码）误判为认证失败的问题。
- **链接**: [PR #28827](https://github.com/google-gemini/gemini-cli/pull/28827)

### 8. [安全] 环境变更征求同意 + 环境变量消毒（#28863）
- **标签**: size/m, size/l
- **作者**: amelidev
- **摘要**: 修复扩展更新可能绕过用户同意、向 MCP 服务器进程注入未授权环境变量的问题；现在会将 MCP 环境配置并入同意字符串并消毒自定义变量。
- **链接**: [PR #28863](https://github.com/google-gemini/gemini-cli/pull/28863)

### 9. [修复] 不受信任环境中过滤 mcpServers（#29099）
- **标签**: size/m, size/l
- **作者**: luisfelipe-alt
- **摘要**: 在非信任或受限环境中，强制 fail-closed 的工作区信任解析，并过滤掉仓库定义的 `mcpServers`，防止服务启动期间执行非预期进程。
- **链接**: [PR #29099](https://github.com/google-gemini/gemini-cli/pull/29099)

### 10. [特性] 为技能添加 `[Skill]` 标签建议（#29104）
- **标签**: priority/p2, area/agent, size/s, help wanted
- **作者**: Ultron09
- **摘要**: 在 `/` 自动补全菜单和 `/help` 命令中，为技能支持的斜杠命令添加 `[Skill]` 标签（类似现有的 `[MCP]`、`[Agent]`），提升可发现性。
- **链接**: [PR #29104](https://github.com/google-gemini/gemini-cli/pull/29104)


## 功能需求趋势

- **Agent 自主性的提升**：社区持续关注 Gemini CLI 是否能更主动地使用技能和子代理（[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)），以及为工具添加可视化标签（如 `[Skill]`）辅助 Agent 决策。
- **AST 感知的代码读取与搜索**：多期 Issue 讨论了利用 AST 感知工具进行精确的方法边界读取和代码库映射，以降低 token 消耗并减少无效读取（[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)、[#22746](https://github.com/google-gemini/gemini-cli/issues/22746)）。
- **安全沙箱与 Git 环境一致性**：多个 PR 聚焦于 Git 环境的安全消毒和一致性问题（[#28930](https://github.com/google-gemini/gemini-cli/pull/28930)、[#28938](https://github.com/google-gemini/gemini-cli/pull/28938)），同时社区也在探索零依赖的 OS 沙箱方案（[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)）。
- **文件系统抽象的统一**：`read_file` 走 FileSystemService 的 PR（[#29110](https://github.com/google-gemini/gemini-cli/pull/29110)）表明社区正致力于将文件 I/O 统一抽象，为 ACP 和远程文件系统支持打基础。


## 开发者关注点

- **“误报成功”与状态报告不实**：多个 Issue（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)、[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)）反映出子代理在失败时（超时、环境问题）仍报告 `GOAL/success`，开发者无法识别真实的中断或失败原因——这是当前最令人困扰的问题之一。
- **代理挂起与卡死**：通用代理无条件挂起（[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)）和 shell 执行后卡在等待输入（[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)）这两类问题被反复提及，直接影响日常使用的可靠性。
- **破坏性命令的防范**：社区呼吁 Agent 应主动阻止或劝阻副作用较大的操作（如 `git reset --force`）并理解维护类资源（如数据库）的危险性（[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)）。
- **Auto Memory 的安全与效率**：内存提取过程中的脱敏时机（内容已进入模型上下文后才脱敏）以及低信号会话的无限重试，是开发者对隐私和资源消耗的主要担忧（[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)、[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)）。

---

*本日报由 AI 技术分析师基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**2026-08-28**


## 今日速览

v1.0.81 正式发布，向所有用户开放插件仪表盘（`/plugin`、`/mcp`、`/skills`），并带来 MCP 2026-07-28 协议支持；然而该版本也引发了多起兼容性回归（如 chroma-mcp 集成失败），稳定性问题在本周 issue 中占比明显上升。此外，社区对 JSON Schema 发布、会话恢复机制改进等功能需求持续升温。


## 版本发布

### v1.0.81（2026-08-27）

**主要更新：**
- **插件仪表盘（Plugins Dashboard）全面开放**：所有用户可通过 `/plugin`、`/mcp`、`/skills` 命令访问；设置 `PLUGINS_DASHBOARD=false` 可退出，同时隐藏 `copilot plugins` 命令
- **MCP 2026-07-28 协议支持**：CLI、SDK、IDE 及内存客户端同步升级
- **OpenTelemetry 支持增强**：Hooks 现在可以接收当前 OpenTelemetry 上下文

### v1.0.82-0（预发布）

仅包含修复和小改动，无重大功能变更。


## 社区热点 Issues

### 1. [#4647 v1.0.81 破坏 chroma-mcp 兼容性](https://github.com/github/copilot-cli/issues/4647) 🔥 新增
v1.0.80 升级至 v1.0.81 后，与 chroma-mcp 的集成失效。MCP 协议升级可能引入了破坏性变更，受影响的用户需关注官方后续修复版本。

### 2. [#4646 自定义模型上压缩（Compaction）失败："Tool choice must be auto"](https://github.com/github/copilot-cli/issues/4646) 🔥 新增
使用自定义模型（如通过 OpenRouter 注册的 `~z-ai/glm-latest`）时，手动或自动压缩均报 `CAPIError: 400 Tool choice must be auto`。该问题影响所有自定义模型用户，功能完全不可用。

### 3. [#4645 `session.resume` 静默忽略 `model` 参数](https://github.com/github/copilot-cli/issues/4645) 🔥 新增
恢复会话时指定不同的 `model` 会被静默丢弃，实际仍使用持久化的旧模型，且无任何错误提示。API 行为不符合直觉，容易造成混淆。

### 4. [#4612 FileWatch 事件循环失控，日志膨胀至 13GB](https://github.com/github/copilot-cli/issues/4612) 👍 1
长时间运行或恢复的会话可能陷入 `No connection accepted a host event {"kind":"FileWatch"}` 死循环，导致 TUI 冻结并疯狂写入调试日志（实测达 13GB）。对长时间运行的用户影响严重。

### 5. [#4643 低上下文使用率（~20%）时被压缩且未生成 checkpoint](https://github.com/github/copilot-cli/issues/4643) 新增
gpt-5.6 sol 在上下文使用率仅 20% 时就被压缩，但 `/session checkpoints` 又显示无 checkpoint。行为不一致，且压缩时机判断逻辑可能存在问题。

### 6. [#4639 事件存储耗尽触发重试风暴，导致 GC/压缩循环及 Node OOM](https://github.com/github/copilot-cli/issues/4639) 新增
远程事件存储耗尽后，导出器持续尝试 500 事件批量刷新，伴随内存压力、强制 GC 和数千条桥接确认消息，最终可能导致 Node 进程 OOM。长时间活跃会话面临崩溃风险。

### 7. [#3760 CLI 显示 "ctrl+enter enqueue" 但实际快捷键不符](https://github.com/github/copilot-cli/issues/3760) 👍 12
UI 提示 `ctrl+enter` 可入队，实际操作却插入换行；真正生效的是 `ctrl+q`。文档与实现不一致，是本周评论数最高的 UI/UX 问题之一。

### 8. [#4535 v1.0.81 预发布版 `store_memory` 失败："Instance id is required"](https://github.com/github/copilot-cli/issues/4535)
`store_memory` 在 1.0.81 预发布版中持续失败——原生内存写入器被调用时缺少必需的实例 ID。影响依赖上下文记忆功能的用户。

### 9. [#4602 `store_memory` 失败 + MCP 服务器被剥离：managedSettings 在 serverFetchFailed 时 fail-closed](https://github.com/github/copilot-cli/issues/4602)
该 issue 揭示了多个问题的共同根源：`managedSettings` 在 `serverFetchFailed` 抖动时 fail-closed，同时导致 `store_memory` 失败和所有 MCP 服务器被移除。作者与多个已报告 issue 做了关联分析，建议 triage 时注意。

### 10. [#4629 通过 `--resume` 恢复会话时插件 Hooks 不加载](https://github.com/github/copilot-cli/issues/4629) 新增
插件提供的 hooks 在 `--resume` 恢复的会话中完全不执行，而同一插件在全新会话中可以正常触发。影响所有依赖插件 hooks 的恢复工作流。


## 重要 PR 进展

今日无 PR 合并或更新。社区当前聚焦于 v1.0.81 引入的稳定性问题，预计近期将有修复版本发布。


## 功能需求趋势

### 1. 会话管理增强（高频）
- **#4642**：`--name` 应支持"存在则恢复，不存在则创建"的语义，当前需要用户自行判断
- **#4645**：`session.resume` 应允许覆盖已持久化的模型参数

### 2. 可观测性与审计
- **#4621**：Rubber duck 审查过程缺乏可验证记录——模型、审查意见及处理结果在会话结束后全部丢失，无法审计
- **#4638**：模型上下文窗口显示不应简单将 `max_prompt_tokens` 与 `max_output_tokens` 相加，可能虚高

### 3. MCP 生态完善
- **#4634**：支持将本地可执行文件作为 MCP 注册表包类型，当前仅支持 npm/pypi/oci/docker
- **#4636**：`--additional-mcp-config` 传入的服务器在启动协调过程中被意外移除

### 4. 配置与文档
- **#4641**：发布 `~/.copilot/settings.json` 的官方 JSON Schema，以便编辑器提供补全和校验
- **#4635**：`/diff` 命令在 branch diff 模式下应允许选择基础分支，而非仅限于当前分支对比

### 5. Hooks 行为一致性
- **#4640**：`userPromptTransformed` hook 在 steering 消息（代理处理中收到的用户消息）时被跳过，导致注入的常驻指令丢失


## 开发者关注点

### 高优先级痛点

**1. 稳定性回归（v1.0.81）**
- **MCP 兼容性破坏**（#4647）：chroma-mcp 等第三方 MCP 服务器在升级后无法工作
- **事件存储重试风暴**（#4639）：可能导致长时间运行会话 OOM 崩溃
- **FileWatch 事件循环失控**（#4612）：日志膨胀至 13GB，TUI 完全冻结

**2. 压缩（Compaction）功能可靠性**
- **自定义模型压缩失败**（#4646）：400 错误导致 `/compact` 完全不可用
- **压缩时机异常**（#4643）：低上下文使用率即触发压缩，且 checkpoint 报告不一致

**3. 上下文记忆（`store_memory`）不稳定**
- **实例 ID 缺失**（#4535）：1.0.81 预发布版中持续失败
- **managedSettings  fail-closed**（#4602）：服务器抖动导致整个会话的 MCP 和记忆功能被禁用

### 中优先级关注

- **Windows 平台 MCP 启动问题**（#3576）：stdio MCP 服务器在 Windows 上 spawn 失败，虽已修复但仍有讨论
- **权限请求超时**（#4486）：编辑权限请求等待超时，多会话并行用户受影响明显
- **插件恢复 bug**（#4629）：`--resume` 后 hooks 不加载，影响自动化流程

### 低频但值得注意

- **编辑器集成缺口**（#4641）：缺少 settings.json 官方 Schema，影响编辑体验
- **模型上下文显示虚高**（#4638）：给用户造成上下文容量错觉

---

**总结**：v1.0.81 的功能更新（插件仪表盘、MCP 协议升级）值得肯定，但随之而来的稳定性问题正在消耗社区信任。建议用户如需使用 chroma-mcp 等第三方 MCP 服务器，可暂缓升级；同时关注官方对 #4646、#4647 和 #4639 的修复进展。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-28

## 今日速览

今日仓库无新版本发布，社区讨论集中在 Plan 模式下的工具调用死循环 bug（#2623）、OpenAI Chat Completions 兼容配置文档缺失（#2624）以及对 API 错误处理的尖锐吐槽（#2621）。安全方面，一个针对 `asyncssh` 依赖的漏洞修复 PR（#2622）已提交，建议关注升级。

---

## 社区热点 Issues

**1. [bug] Plan mode 下 agent 死循环不写计划（#2623）** ⭐️ 新增
- **作者**: zheng001001001 | 状态: OPEN | 评论: 1
- **摘要**: 在 0.38.0 版本 (K3 模型, Linux) 下，Plan mode 探索完成后模型不执行写计划或 ExitPlanMode，反而死循环调用 `Bash echo` 和 `ReadFile`。
- **重要性**: 阻塞核心工作流的关键 bug。若复现普遍，将严重影响依赖 Plan mode 的用户。K3 模型已包含在发布渠道中，该问题值得官方最优先级排查智能体循环终止机制。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2623)

**2. [docs] openai_legacy 配置示例缺失（#2624）** ⭐️ 新增
- **作者**: cursor[bot] | 状态: OPEN | 评论: 0
- **摘要**: 文档已提及 `openai_legacy` 类型，但缺少完整示例。用户特别提醒：接 Chat Completions 端点时 `type` 必须设为 `openai_legacy`，而非 `openai_responses`，也不能走 `/login` 流程。
- **重要性**: 配置细节（如 `type` 字段选错）极易导致接入第三方网关失败。该文档缺口直接影响依赖 OpenAI 兼容协议的用户接入效率。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2624)

**3. [bug] Notion MCP 凭证仅会话内有效（#1211）** 状态更新
- **作者**: ghost | 状态: CLOSED | 评论: 3
- **摘要**: v1.12.0 版本下，Notion Remote MCP 的凭据在活动会话结束后未被持久化存储，导致下次必须重新认证。
- **重要性**: 长期存在的可用性缺陷，影响"MCP 生态"体验。今日被关闭，推测可能在近期版本修复，可查看关闭原因确认修复版本。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1211)

**4. [bug] JetBrains 插件通过 ACP 调用不识别文件（#1272）** 状态更新
- **作者**: yuweni99 | 状态: CLOSED | 评论: 1
- **摘要**: 在 JetBrains AI Assistant 中使用 ACP 调用 Kimi 时，拖拽传入的文件无法被识别，必须在提示词中手写文件路径。
- **重要性**: IDE 集成是重要使用场景，此类交互细节影响日常效率。同样今日关闭，可确认修复版本。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1272)

**5. [enhancement] 原生支持 git-ai 代码溯源标准（#1279）** 状态更新
- **作者**: deshes | 状态: CLOSED | 评论: 0
- **摘要**: 建议原生集成 vendor-agnostic 的 AI 代码归属标准，便于在 `git blame` 中区分 AI/人工编辑。
- **重要性**: 反映开发者对代码审计与合规的诉求。该方向近期在社区呼声渐长，值得关注官方对该提案的考量。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1279)

**6. [bug] API 对空 content 的 400 错误处理逻辑荒谬（#2621）** 新增
- **作者**: Valen-akm | 状态: OPEN | 评论: 0 | 👍: 1
- **摘要**: 模型工具调用时返回 `content: null`，将消息原样回传却报 `400 text content is empty`。用户被迫自行剥离空 content。批评语气强烈。
- **重要性**: 直接触及 API 设计一致性问题，处理技巧过于脆弱，会大量浪费开发者排查时间。该情绪化标题也侧面反映此问题已积怨。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2621)

---

## 重要 PR 进展

**1. deps: 修复 pykaos 中 asyncssh 安全漏洞（#2622）** ⭐️ 新增
- **作者**: katsugtgz | 状态: OPEN
- **内容**: 将 `asyncssh` 从 2.21.1 升级至 2.23.1，以修复 GHSA-2wxc-x7rj-hg8f 和 GHSA-qr67-gv47-xwwh 两个安全公告。
- **重要性**: 涉及安全漏洞修复，若 `pykaos` 包被广泛使用则影响较大，建议相关用户尽快验证兼容性。
- [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2622)

**2. fix(hooks): 提取 ContentPart 中的文本给 UserPromptSubmit hook（#2176）** 更新
- **作者**: tears-mysthrala | 状态: OPEN
- **内容**: 修复当 `user_input` 为 `list[ContentPart]` 时，hook 收到空 `prompt` 和 `matcher_value` 的问题，使 regex 匹配对所有消息均生效。
- **重要性**: 直接影响 hooks 扩展机制的核心能力，修复后所有依赖用户输入文本的 hook 才真正可用。
- [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2176)

**3. fix(StrReplaceFile): 拒绝编辑非 UTF-8 文件（#2595）** 更新
- **作者**: shoemoney | 状态: OPEN
- **内容**: 修复 `StrReplaceFile` 对含非法 UTF-8 字节（远离编辑点）的文件进行全文重写导致数据损坏的问题，现改为拒绝编辑并报错。
- **重要性**: 避免工具意外破坏二进制或特殊编码文件，是数据安全方向的稳健修复。
- [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2595)

---

## 功能需求趋势

从近期 Issues 提炼出以下关键方向：

- **第三方服务可靠接入**：OpenAI 兼容协议（`openai_legacy`）的配置文档与行为一致性受到关注，期望简化接入流程、减少歧义。
- **工具调用稳定性**：Plan mode 下模型工具调用循环不退出问题被突出报告，侧面反映用户看重"计划-执行"工作流的可靠性。
- **安全与合规**：`asyncssh` 漏洞修复 PR 与 `git-ai` 代码溯源提案均属此范畴，显示企业级场景对供应链安全与代码审计的高需求。
- **API 兼容性**：`content` 字段空值处理逻辑引发争议，开发者希望 API 遵循消息往返一致性的设计原则。

---

## 开发者关注点

- **效率至上**：用户对配置跳坑（如 `openai_legacy` 类型误选）感到挫败，期待文档提供可直接粘贴的完整示例。
- **对 API 细节敏感**：围绕 `content` 空值报 400 的讨论热度高，开发者期望"发送即返回、返回即合法"的接口行为，而非依赖客户端兼容 hack。
- **IDE 集成体验**：对 JetBrains 等 IDE 中文件的智能识别有明确预期；今日多个长期 issue 被关闭，社区正在验证修复效果。
- **安全**：依赖漏洞（如 `asyncssh`）提示用户在升级时关注依赖树安全。

---
*本日报由 AI 自动生成，覆盖 2026-08-27 至 2026-08-28 的 GitHub 数据。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**2026-08-28** | 数据来源: github.com/anomalyco/opencode

---

## 今日速览

昨日发布两个补丁版本（v1.18.24/v1.18.25），核心修复了 Azure 认证、Bedrock 推理缓存等关键问题。社区层面，关于旧版 UI 布局去留的讨论持续升温（#37012，41 条评论），同时 Go 套餐用量统计不一致（#38255）和桌面端自动更新器异常（#45087）成为新的吐槽焦点。

---

## 版本发布

### v1.18.25
**核心修复**
- 修复 Azure 认证：现在 Azure CLI 登录无需依赖 Bun 运行时

### v1.18.24
**核心修复**
- Bedrock 推理响应不再被缓存为不可重放的空消息

**改进**
- Azure 提供商现在可通过 Azure CLI 使用 Microsoft Entra ID 登录，无需 API Key
- V1 版本开始读取 V2 支持的配置字段，兼容性提升

---

## 社区热点 Issues

### 1. #37012 [FEATURE] 保留传统布局选项
**作者**: darkine24th | 评论: 41 | 👍: 43 | **状态**: OPEN
**链接**: https://github.com/anomalyco/opencode/issues/37012

> 社区最热门议题。用户列举旧版布局的诸多优势：主窗口直达几乎所有功能、工作区支持等。新版需层层导航才能找到选项，效率明显下降。作为对比，#37527（6 条评论）也在讨论多项目布局问题，但当前主要矛盾集中在旧版易用性。

**重要度**: ⭐⭐⭐⭐⭐ — 41 条评论印证这是当前社区最大的痛点，且获得大量 👍 支持。

---

### 2. #21034 Gemma-4 系列模型工具调用循环/失败
**作者**: pchuck | 评论: 21 | 👍: 20 | **状态**: CLOSED
**链接**: https://github.com/anomalyco/opencode/issues/21034

> 即使应用了最新 tokenizer 修复和引擎补丁，Gemma-4-26b/31b 在 OpenCode 中仍不可用。用户详细记录了 lmstudio v0.4.9 和 llama.cpp v2.11.0 的环境配置，问题指向 OpenCode 与 Gemma 工具调用协议的兼容性。

**重要度**: ⭐⭐⭐⭐ — 本地模型支持是 OpenCode 核心场景，此问题影响面较大。

---

### 3. #961 Termux 支持
**作者**: keeganmccallum | 评论: 14 | 👍: 22 | **状态**: CLOSED
**链接**: https://github.com/anomalyco/opencode/issues/961

> 用户希望在 Termux（Android 终端模拟器）上运行 OpenCode。虽然已关闭（可能已实现或暂不考虑），但 14 条评论和 22 个 👍 表明移动端/嵌入式环境的需求仍然存在。

**重要度**: ⭐⭐⭐ — 已关闭但仍有参考价值，代表了一部分移动开发者的诉求。

---

### 4. #38255 Go 套餐用量统计差异
**作者**: PiouPiou82 | 评论: 9 | 👍: 0 | **状态**: OPEN
**链接**: https://github.com/anomalyco/opencode/issues/38255

> 用户报告 Go 套餐面板的月度限额显示 100% 已用完，但细粒度用量仪表盘显示同期仅消耗约 $10。模型全部停止工作，造成实际业务中断。同日 #45858（3 条评论）也报告了用量明细页百分比计算错误（如 $17.87/$30 显示为 54.1% 而非 59.6%）。

**重要度**: ⭐⭐⭐⭐ — 计费数据不一致直接影响用户信任，且已导致服务中断，属于 P0 级问题。

---

### 5. #44958 [BUG] 拒绝响应被隐藏且对话历史消失
**作者**: bojackduy | 评论: 6 | 👍: 0 | **状态**: OPEN
**链接**: https://github.com/anomalyco/opencode/issues/44958

> 使用 `muse-spark-1.2-contributor` 模型时，运行完成但 UI 无任何响应或错误提示。某些情况下运行会无限挂起。HTTP 流已成功完成且包含响应数据，但前端未能正确渲染。

**重要度**: ⭐⭐⭐ — 响应消失 + 历史丢失是严重的 UX 问题，影响 Go 订阅用户体验。

---

### 6. #45087 [2.0] 自动更新器异常消耗 266GB 磁盘
**作者**: ogulcancelik | 评论: 5 | 👍: 0 | **状态**: CLOSED
**链接**: https://github.com/anomalyco/opencode/issues/45087

> 长时间运行的 `opencode2 serve --service` 进程在 `~/.npm/_cacache` 中积累了 266GB 的 OpenCode beta 包。原因是 npm 更新可执行文件后，运行中的服务器仍使用内存中的旧版本，其十分钟更新循环认为自身已过期，反复下载安装。今日 PR #45865 正是 revert 了相关修复（#45091），说明该问题的解决方案仍在反复。

**重要度**: ⭐⭐⭐ — 极端磁盘消耗问题，虽然已关闭但方案反复，值得关注后续进展。

---

### 7. #21658 [FEATURE] Azure AI Foundry Entra (OAuth) 认证
**作者**: NoTuxNoBux | 评论: 4 | 👍: 10 | **状态**: OPEN
**链接**: https://github.com/anomalyco/opencode/issues/21658

> 请求支持 Microsoft Entra 认证（OAuth）用于 Azure AI Foundry，目前仅支持 API Key 方式。与 v1.18.24 中 Azure CLI/Entra ID 登录改进相呼应，说明企业级身份认证是明确的社区需求方向。

**重要度**: ⭐⭐⭐ — 企业用户刚需，与最新版本更新方向一致。

---

### 8. #37946 中止的助手回合导致会话卡死
**作者**: Oloompa | 评论: 4 | 👍: 1 | **状态**: OPEN
**链接**: https://github.com/anomalyco/opencode/issues/37946

> 系统暂停/恢复后 TUI 冻结，用户中止回合后，OpenCode 持久化了包含 `MessageAbortedError` 的空助手消息（仅有 step-start/reasoning/patch 部分，无文本和工具调用）。此后每次请求都会向提供商重放该空消息，导致 400 "must not be empty" 错误。

**重要度**: ⭐⭐⭐ — 一次中止导致永久性会话损坏，严重影响了长期会话的可靠性。

---

### 9. #5409 [FEATURE] SessionStart 钩子
**作者**: simonwjackson | 评论: 7 | 👍: 18 | **状态**: CLOSED
**链接**: https://github.com/anomalyco/opencode/issues/5409

> 请求添加 `SessionStart` 钩子（类似 Claude Code），在会话生命周期关键节点触发。7 条评论、18 个 👍，说明开发者对会话级生命周期事件的自动化控制有较强需求。

**重要度**: ⭐⭐⭐ — 插件生态扩展的关键特性，虽已关闭但需求热度不减。

---

### 10. #17372 Windows 下错误使用 PowerShell 5.1
**作者**: moyaspace | 评论: 5 | 👍: 5 | **状态**: CLOSED
**链接**: https://github.com/anomalyco/opencode/issues/17372

> OpenCode 从 PowerShell 7 启动后，执行 bash 命令时却使用 Windows PowerShell 5.1。导致 PS7 的 profile 不加载、环境变量缺失，并且 cmdlets 在 PS 5.1 中无法使用（如 `gh`、`az` 等），破坏了一致性体验。

**重要度**: ⭐⭐⭐ — Windows 开发者的高频痛点，直接影响命令行工具的可用性。

---

## 重要 PR 进展

### 1. #45777 feat(core): 升级 MCP SDK 并支持现代协议
**作者**: rekram1-node | 2026-08-27 → 08-28

将 `@modelcontextprotocol/sdk@1.29.0` 替换为拆分后的 client/core/server `2.0.0` 包，协商 MCP `2026-07-28` 协议版本，同时保留对旧版服务器的初始化兼容。stdio 探测改为 disposable 模式。**意义**: MCP 生态的核心基础设施升级。

🔗 https://github.com/anomalyco/opencode/pull/45777

---

### 2. #45865 Revert "fix(cli): 防止重复更新和 npm 缓存增长"
**作者**: neriousy | 2026-08-28

直接 revert #45091（该 PR 是修复 #45087 的 266GB 缓存问题）。**注意**: 这说明上一个修复方案存在副作用或未完全解决问题，修复方案仍在迭代中。

🔗 https://github.com/anomalyco/opencode/pull/45865

---

### 3. #45864 fix(ai): 保持聊天推理在一个生命周期中
**作者**: rekram1-node | 2026-08-28

修复 #45791。`openai-chat` 在可见内容或拒绝响应到达时过早结束推理块，导致后续内容块反复重新打开空的 `reasoning-0` 块又立即关闭，核心为每个重开块分配新 ID，造成消息混乱。

🔗 https://github.com/anomalyco/opencode/pull/45864

---

### 4. #45854 fix(ai): 尊重响应文本和推理最终值
**作者**: rekram1-node | 2026-08-28

修复推理过程中流式文本被覆盖的问题。此前流式增量（如 "Draft answer"）会覆盖提供商的最终值（如 "Corrected answer"），现在会缓存最终值直到碎片边界再传递。

🔗 https://github.com/anomalyco/opencode/pull/45854

---

### 5. #45842 fix(provider): 跳过低于最小可缓存大小的 Bedrock 缓存点
**作者**: jangraviren | 2026-08-28

`applyCaching()` 无条件添加 Bedrock `cachePoint`，但当缓存前缀低于模型最小可缓存大小时，Bedrock 会拒绝请求。此 PR 在低于阈值时跳过缓存点。

🔗 https://github.com/anomalyco/opencode/pull/45842

---

### 6. #40125 feat(opencode): 允许按 MCP 服务器配置信任
**作者**: karup | 2026-08-02 → 08-28

通过指纹锁定实现自签名证书信任，无需全局设置 `insecure: true`。`caFile` 处理私有 CA。部分解决 #23506。**意义**: 提升 MCP 远程服务器的安全性配置灵活性。

🔗 https://github.com/anomalyco/opencode/pull/40125

---

### 7. #45853 feat: 离线文档预览 (docx/xlsx/pptx/pdf)
**作者**: xirothedev | 2026-08-28

新增离线文档预览功能，支持 Word/Excel/PPT/PDF 格式，包含 DocumentPreview 对话框、插件调用路由、Excel 列宽/合并单元格/冻结/工作表标签支持，以及 i18n 国际化。**注意**: 同作者同日提交了两个版本（#45857 已关闭、#45853 为干净分支重提）。

🔗 https://github.com/anomalyco/opencode/pull/45853

---

### 8. #45850 fix(ai): 在 done 哨兵处结束聊天流
**作者**: rekram1-node | 2026-08-28

保留 Chat Completions 路由的 `[DONE]` SSE 哨兵，在处理完 finish 和 usage 块后结束流，停止读取开放响应体并忽略哨兵后的帧。附带 `bun test` 测试。

🔗 https://github.com/anomalyco/opencode/pull/45850

---

### 9. #43941 feat(app): 在会话头部显示当前项目
**作者**: TonisOrmisson | 2026-08-21 → 08-28

在对话头部、context/cost 控制之前显示当前活动项目名称，桌面端用户在多项目切换时可清晰辨识当前上下文。

🔗 https://github.com/anomalyco/opencode/pull/43941

---

### 10. #45852 feat(core): 自主自动驱动执行引擎
**作者**: eust-w | 2026-08-28

引入 Auto-Drive（智能续推/自动领航）引擎，支持跨回合自主会话延续：多维度上下文合成、追踪初始用户目标、自动规划下一步等。**注意**: 同日有 #45837 关闭版本，此条为重新提交。

🔗 https://github.com/anomalyco/opencode/pull/45852

---

## 功能需求趋势

从今日 Issues/PRs 中可以提炼出以下社区关注方向：

| 方向 | 代表 Issue/PR | 热度 |
|------|--------------|------|
| **UI/布局灵活性** | #37012 保留旧布局、#37527 多项目布局 | 🔥🔥🔥🔥🔥 |
| **认证方式多样化** | #21658 Entra OAuth、v1.18.24 Azure CLI 登录 | 🔥🔥🔥🔥 |
| **MCP 协议与安全** | #45777 SDK 2.0 升级、#40125 按服务器信任配置 | 🔥🔥🔥🔥 |
| **计费透明度** | #38255 用量统计差异、#45858 百分比错误、#34376 账单历史 | 🔥🔥🔥🔥 |
| **会话生命周期管理** | #5409 SessionStart 钩子、#37946 中止会话修复、#45852 自动驱动 | 🔥🔥🔥🔥 |
| **离线文档处理** | #45853 文档预览、#21908 PDF 工具结果传递 | 🔥🔥🔥 |
| **Windows 体验** | #17372 PowerShell 7 兼容、#32389 错误提示音 | 🔥🔥🔥 |

---

## 开发者关注点

### 高频痛点

1. **Go 套餐计费问题集中爆发** — 3 个相关 Issue（#38255、#45858、#45803）同周出现，涉及统计不一致、百分比计算错误、奖励误操作。计费系统的可信度正在被消耗。

2. **旧版 UI 的去留争议** — #37012 以 41 条评论成为绝对焦点，且 #37527、#34055 均涉及旧版布局问题。开发者对新版信息密度和导航效率不满，团队需明确旧版支持的生命周期。

3. **自动更新器反复** — #45087（266GB 磁盘消耗）→ #45091 修复 → #45865 Revert，一路反复说明此问题尚未收敛。长驻进程场景下的更新策略需重新设计。

4. **中止/中断后的会话恢复** — #37946 和 #31046（空文本块 422 错误）都指向会话中断后的状态损坏问题。对于长时间运行的 AI 编码会话，这是可靠性短板。

5. **推理流处理质量** — #45864、#45854、#45850 三个 PR 同日均聚焦推理和流结束处理，说明推理相关的流式输出边界场景仍在持续完善，社区对模型输出的忠实度要求很高。

---

*本日报由 AI 自动生成，数据截至 2026-08-28。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

## Pi 社区动态日报 — 2026-08-28

---

### 1. 今日速览

TUI 渲染问题（文本逐词换行、软换行硬渲染）成为昨日社区最集中的痛点，三个关联 Issue 共同指向 v0.84.3 的 TUI 文本流式渲染回归，目前已有修复 PR 合并。此外，多个与代理配置（`HttpsProxyAgent`、`NO_PROXY` 通配符、Windows shell 路径）相关的 Bug 在一天内集中关闭，显示维护者正在系统性清理配置链路的兼容性问题。

---

### 2. 版本发布

过去 24 小时无新版本 Release。

---

### 3. 社区热点 Issues

#### ① #8584 — TUI 流式渲染文本逐词换行（OPEN，14 评论）
**链接**: https://github.com/earendil-works/pi/issues/8584

工具输出长行后，助手文本流式渲染出现"一词一行"的异常，疑似行宽计算被破坏。**评论数 14，为当前最热 Issue**。与 #8675、#8673 高度关联，构成 v0.84.3 TUI 渲染回归的完整证据链。社区关注度高，👍 6。

#### ② #6922 — 默认模型不能是 llama.cpp 模型（CLOSED，12 评论）
**链接**: https://github.com/earendil-works/pi/issues/6922

当 `defaultProvider` 设为 `llama.cpp` 时启动报"No models available"并退出。评论 12 条，👍 14 为今日列表最高。该问题从 7 月持续到 8 月底终于关闭，本地模型用户对此需求强烈。

#### ③ #7553 — 压缩（Compaction）可配置思考级别/模型（OPEN，9 评论）
**链接**: https://github.com/earendil-works/pi/issues/7553

自动压缩无条件复用当前会话的 thinking level，使用推理模型时摘要的思考预算与正常轮次不可分离。与 PR #7602 对应，正在推进中。

#### ④ #8673 — TUI 软换行渲染为硬换行（CLOSED，4 评论）
**链接**: https://github.com/earendil-works/pi/issues/8673

`marked` 保留 CommonMark 软换行为字面 `\n`，导致思考块每子句一行、难以阅读。**Root cause 已定位，修复 PR #8674 当日合并**。

#### ⑤ #8610 — v0.84.3 回归：HttpsProxyAgent 非构造函数（CLOSED，4 评论）
**链接**: https://github.com/earendil-works/pi/issues/8610

Code splitting 打包导致 `https-proxy-agent` 命名导出丢失，google-vertex 配合代理直接崩溃。**修复 PR #8723 已合并**。

#### ⑥ #8675 — TUI 文本逐词换行（WSL2/Windows Terminal）（CLOSED，3 评论）
**链接**: https://github.com/earendil-works/pi/issues/8675

与 #8584 相同症状，在 WSL2/Windows Terminal 可稳定复现。👍 4，证实该问题影响面广。

#### ⑦ #8762 — 会话列表全量解析每个会话文件（CLOSED，2 评论）
**链接**: https://github.com/earendil-works/pi/issues/8762

`--resume` 选择器仅需显示名称却流式解析整个 JSONL 收集全文——会话文件大时明显卡顿。**性能优化指向明确，适合社区贡献**。

#### ⑧ #8757 — 工具参数验证器缺少对象/数组→字符串的强制转换（CLOSED，2 评论）
**链接**: https://github.com/earendil-works/pi/issues/8757

验证器已支持字符串→对象/数组的修补，但反向方向缺失，导致 write/edit 的内容参数在模型输出对象时报"must be string"。对依赖结构化输出的场景影响大。

#### ⑨ #8728 — DeepSeek 兼容端点未自动启用 reasoning_content 要求（CLOSED，3 评论）
**链接**: https://github.com/earendil-works/pi/issues/8728

`api.b.ai` / `sensenova` 等 OpenAI 兼容网关在跨提供方重放携带推理内容的历史消息时返回 400。**修复 PR #8732 当日合并**。

#### ⑩ #8765 — 支持 JSONC 格式的 settings.json（CLOSED，1 评论）
**链接**: https://github.com/earendil-works/pi/issues/8765

社区希望 `settings.json` 支持注释与尾逗号。无明显反对声音，属于低成本体验提升。

---

### 4. 重要 PR 进展

#### ① #8674 — 修复 TUI 软换行渲染（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8674

在 `marked` 解析层将段落内 `\n` 替换为空格，保持硬换行语义不变。**直接修复 #8673，合并即关闭**。

#### ② #8723 — 暴露 https-proxy-agent 命名导出（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8723

在 coding-agent bundle 构建脚本中增加插件，将 `https-proxy-agent` 拆为独立 chunk 并暴露命名导出。**修复 #8610 的代理崩溃问题**。

#### ③ #8764 — 修复 Windows 上 `!` 命令解析忽略 settings.shellPath（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8764

`getShellConfig()` 无参调用时忽略自定义 `shellPath`，Windows 上误选 WSL bash shim。修复后需显式传入 `settings.shellPath`。**对应 #8763**。

#### ④ #8732 — DeepSeek 系端点跨模型重放保留 reasoning_content（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8732

重放历史消息时，若原 assistant 消息携带推理内容且目标端点要求 `reasoning_content` 字段，则保留该字段。**修复 #8728**。

#### ⑤ #7602 — 可配置的压缩/摘要模型（OPEN）
**链接**: https://github.com/earendil-works/pi/pull/7602

新增压缩和分支摘要的模型与思考级别配置，提供方错误处理压缩上下文窗口限制。**关闭 #7553**，仍开放中。

#### ⑥ #8737 — 修复 NO_PROXY 子域名与根域名匹配（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8737

支持 `*.example.com`、`.example.com`、裸域名在子域名/根域名间一致匹配；修正 IPv6 条目解析（含括号/无括号）。**修复 #8736**。

#### ⑦ #8727 — 保留离屏变化时的滚动历史（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8727

视口以上的主屏变更保留为原生滚动历史快照，而非清空后重放完整记录；伸展到可见视口的变更继续跟随流式输出；保留整屏重绘兜底。

#### ⑧ #8731 — 全屏 TUI 可禁用"选择即复制"，Ctrl+X 复制选区（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8731

新增 `copyOnSelect` 设置（默认 true），关闭后 Ctrl+X 复制当前选区，否则沿用复制最后一条助手消息的默认行为。**对应 #7720**。

#### ⑨ #8719 — 纯空白工具结果按空输出处理（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/8719

Windows shell 产生的 `"\r\n"` 通过长度检查被原样发送给提供方，OpenAI 兼容端点以 400 拒绝。修复后空白结果直接视为空。

#### ⑩ #6848 — 压缩摘要的瞬态流失败重试（CLOSED）
**链接**: https://github.com/earendil-works/pi/pull/6848

为 `completeSummarization()` 添加带指数退避的有界重试，单次流中断不再导致整个压缩失败。**修复 #6647**，从 7 月持续到 8 月末。

---

### 5. 功能需求趋势

- **TUI 体验精细化**：鼠标选择语义（单列复制 #8767-8769、禁用选即复制 #7720）、滚动历史保留（#8727）、文本换行语义正确性（#8673）—— 用户对终端 UI 的复制粘贴与阅读体验要求明显提升。
- **模型兼容层扩展**：新增模型支持（qwen3.8-flash #8709、Cortecs #8199）、OpenAI Responses 风格顶层指令（#8734）、DeepSeek 系 `reasoning_content` 跨模型重放（#8732）—— 社区持续推动更广的模型生态接入。
- **配置灵活性与可读性**：JSONC 注释支持（#8765）、全局 `~/.agents/AGENTS.md`（#5002）、README 安装章节（#6907）与中文翻译（#8772）—— 降低上手门槛、提升配置可维护性。
- **性能优化**：会话列表全量解析（#8762）—— 大型会话文件场景下的启动/选择延迟开始被关注。

---

### 6. 开发者关注点

- **TUI 渲染回归集中爆发**：v0.84.3 中文本逐词换行（#8584/#8675）与软换行硬渲染（#8673）在同一时期出现，且与#8621 关联（自动关闭后又复现），说明该版本 TUI 改动引入了系统性回归，开发者对质量验证流程有疑虑。
- **代理与网络配置的"最后一公里"问题**：HttpsProxyAgent 导出丢失（#8610）、NO_PROXY 通配符匹配（#8737）、Windows `!` 命令 shell 路径（#8763）—— 企业/代理环境用户占比不低，且此类问题通常在发布后由真实环境暴露。
- **OpenRouter `:free` 模型不可用**（#8760）：Pi 发送超过上游硬限制的 `max_tokens`，导致所有 `:free` 模型 400。免费模型用户基数大，此问题对口碑影响显著。
- **扩展生态冒名风险**（#8770）：`picodesandbox` 包链接与官方 `pi-sandbox` 相同，社区开始关注包名仿冒与供应链安全。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-28

## 今日速览
今日社区围绕**流式传输稳定性**（Anthropic wire 缺失流安全保护、超时误报）、**TUI 渲染架构**（ink → OpenTUI 迁移推进）及**Agent 协议（ACP）统一**三条主线展开。核心方面，昨晚发布 v0.22.2-nightly 修复 Web-Shell 会话 diff 恢复与钉钉富文本多行问题；同时 `qwen-live` 独立语音守护进程包、结构化记忆召回协议等重量级 PR 在收尾中。此外，Main 分支 E2E 测试连续多次失败，成为 CI 稳定性关注的焦点。

---

## 版本发布
**v0.22.2-nightly.20260828.7357136dd1**
- `fix(web-shell)`: 恢复已保存会话的 diff 展示（PR #10093）
- `fix(channels)`: 修复钉钉渠道富文本多行内容处理

> ⚠️ 注意：此为 nightly 预发布版本，不建议在生产环境直接升级。

[查看 Release 详情](https://github.com/QwenLM/qwen-code/releases)

---

## 社区热点 Issues（Top 10）

### 1. `#5975` — API 流无响应超时（120s）且重试无效
**标签**: P2 / bug / performance  
**作者**: yousimu | 评论 13 | 👍 1  
**摘要**: 升级 v0.19.3 后频繁出现 *"No stream activity for 120000ms after 19 chunks"*，此前版本仅表现为“思考中”但无输出。用户期待模型持续输出时不应被误判为超时。  
**值得关注**: 13 条评论位列今日榜首，涉及流式传输的稳定性，直接影响日常使用体验，且尚未有明确修复方案。

[Issue #5975](https://github.com/QwenLM/qwen-code/issues/5975)

---

### 2. `#8662` — TUI 渲染层从 ink 迁移至 OpenTUI（跟踪 Issue）
**标签**: P3 / enhancement / roadmap/terminal-ux  
**作者**: chiga0 | 评论 11  
**摘要**: 当前 TUI 基于 ink 7 + React 19（含 1037 行自定义 patch），存在闪烁、渲染异常等结构性问题。提案迁移至 OpenTUI 以根治。  
**值得关注**: 11 条评论表明社区对 TUI 渲染质量高度关注，且此为架构级改动，影响深远。

[Issue #8662](https://github.com/QwenLM/qwen-code/issues/8662)

---

### 3. `#4063` — core + cli 架构审查：14 项结构性问题清单
**标签**: in-progress / enhancement  
**作者**: pomelo-nwu | 评论 11 | 👍 1  
**摘要**: 全面审查发现 P0 级问题：核心类型系统被 `@google/genai` 绑架——136 个文件直接 import 该包，导致 API 耦合僵化。  
**值得关注**: 架构级技术债，影响后续扩展性与维护效率。

[Issue #4063](https://github.com/QwenLM/qwen-code/issues/4063)

---

### 4. `#9005` — Anthropic 传输缺少流安全保护（对比 OpenAI）
**标签**: P1 / in-progress / bug  
**作者**: netbrah | 评论 6  
**摘要**: `anthropicContentGenerator` 缺少 OpenAI 线路已有的流式安全机制，且 `@anthropic-ai/sdk` 仍固定为 2025 年 1 月的 `^0.36.1`。  
**值得关注**: P1 级 bug，直接影响 Anthropic 模型用户的稳定性，且与 #5975 流超时问题可能相关。

[Issue #9005](https://github.com/QwenLM/qwen-code/issues/9005)

---

### 5. `#10227` — 自定义模型供应商（Moonshot）无法对话
**标签**: P2 / bug / tools  
**作者**: ru1yex | 评论 7  
**摘要**: 请求报错 *"tools.function.parameters is not a valid moonshot flavored json schema"*，即工具函数参数 schema 不符合 Moonshot 规范。  
**值得关注**: 涉及自定义供应商兼容性，第三方模型接入的常见痛点，7 条评论说明影响面较广。

[Issue #10227](https://github.com/QwenLM/qwen-code/issues/10227)

---

### 6. `#10065` — LM Studio 本地模型报 "failed to parse grammar"
**标签**: P2 / bug / tools  
**作者**: hotamachisubaru-git | 评论 6  
**摘要**: 即使未启用 MCP 服务且 `tools.core=[]`，Qwen Code v0.22.1 连接 LM Studio 0.4.21 仍失败。  
**值得关注**: 本地模型场景（LM Studio）是重要使用路径，且已进入 `status/ready-for-human` 待人工确认。

[Issue #10065](https://github.com/QwenLM/qwen-code/issues/10065)

---

### 7. `#10147` — 升级 v0.22 后本地命令执行与文件编辑完全失效
**标签**: P2 / bug / shell  
**作者**: antibits | 评论 3  
**摘要**: 升级后 `qwen-code` 无法执行本地命令及文件编辑，用户强烈要求：① 允许禁止自动升级；② 尽快修复回归。  
**值得关注**: 严重功能回归，虽评论数不多但影响核心工作流，需高度警惕。

[Issue #10147](https://github.com/QwenLM/qwen-code/issues/10147)

---

### 8. `#10061` — 统一 stdio 与 HTTP ACP 路径并升级 SDK 至 1.x
**标签**: P2 / in-review / integration  
**作者**: chiga0 | 评论 3  
**摘要**: 提案将两条 ACP 传输路径合并为传输无关的核心，并将 `@agentclientprotocol/sdk` 从 0.14.1 升级至 1.4.x。  
**值得关注**: 架构统一的前置工作，影响 IDE 集成与 daemon 模式的长期演进。

[Issue #10061](https://github.com/QwenLM/qwen-code/issues/10061)

---

### 9. `#9475` — 推理过程中屏幕中部文本错乱
**标签**: P2 / bug / UI  
**作者**: danielebruneo | 评论 4  
**摘要**: 最新版本中，工具调用输出停留在屏幕底部，推理内容却从顶部乱序更新，渲染插入点随机错乱，直至最终回复完成。  
**值得关注**: 与 #8662（TUI 渲染层）同源，进一步印证 OpenTUI 迁移的紧迫性。

[Issue #9475](https://github.com/QwenLM/qwen-code/issues/9475)

---

### 10. `#10267` — DWS 渠道：直接回复不可见且漏收 DM 无法恢复（已关闭）
**标签**: P2 / bug / integration  
**作者**: qqqys | 评论 2  
**摘要**: DWS（钉钉/飞书等）渠道确认收到直接回复但收件端不可见，消费中断期间的私信无法事后补收。已由 PR #10274 修复。  
**值得关注**: 验证了“修复-反馈”闭环的高效运作，值得用户关注升级时间点。

[Issue #10267](https://github.com/QwenLM/qwen-code/issues/10267)

---

## 重要 PR 进展（Top 10）

### 1. `#10347` — 自动重试瞬时网络错误（EOF）
**作者**: qwen-code-dev-bot | `review/self-reported`  
**说明**: 将 `400 network error ... EOF` 等包装型网络错误归类为可重试传输错误，使无 Ctrl+Y 场景（如 CI、daemon）下自动重试生效，避免 fail-fast 导致任务失败。  
**意义**: 直接提升非交互场景的健壮性。

[PR #10347](https://github.com/QwenLM/qwen-code/pull/10347)

---

### 2. `#10368` — OpenTUI 迁移第三批：live-session 与输入层
**作者**: chiga0  
**说明**: 在基础模块之上新增实时会话流折叠、流式 Markdown 修复渲染、渐进式 MCP 展示及输入层处理，是 #8662 迁移计划的关键一步。  
**意义**: TUI 重构进入深水区，值得关注后续性能与稳定性收益。

[PR #10368](https://github.com/QwenLM/qwen-code/pull/10368)

---

### 3. `#10183` — 结构化记忆按需召回协议
**作者**: ZijianZhang989  
**说明**: 将“扁平化、重上下文”的自动记忆升级为“推送/拉取”结构化协议：模型获得两级引用/标题树、查询聚焦的元数据子树，并新增专用召回工具。  
**意义**: 记忆机制从“塞进提示词”转向“按需检索”，是长会话场景的重要基础设施改进。

[PR #10183](https://github.com/QwenLM/qwen-code/pull/10183)

---

### 4. `#10268` — 取消超时的 daemon 会话初始化
**作者**: doudouOUC  
**说明**: 将初始化预算变为“端到端权威”：bridge 发送私有绝对截止时间，子进程将取消传播至配置、Gemini 启动及 `SessionStart` hooks。  
**意义**: 避免 daemon 模式下会话初始化卡死，提升自动化场景可靠性。

[PR #10268](https://github.com/QwenLM/qwen-code/pull/10268)

---

### 5. `#10274` — 修复 DWS 私信恢复（对应 #10267）
**作者**: qqqys | `autofix/takeover`  
**说明**: 私信最终回复改用普通 DM 通道下发（群聊保持引用回复），历史私信通过同策略补发；过期回复回放不再误发。  
**意义**: 解决渠道消息可达性问题，已关闭 #10267，是“社区反馈→修复”的典型闭环。

[PR #10274](https://github.com/QwenLM/qwen-code/pull/10274)

---

### 6. `#10357` — 钉钉状态卡片网络失败后自动恢复
**作者**: qqqys  
**说明**: 对瞬时 Card OpenAPI 故障实施有上限的指数退避重试，始终发送最新快照；终态优先级最高，确保卡片最终显示完成/失败状态。  
**意义**: 钉钉渠道消息可靠性的重要补强。

[PR #10357](https://github.com/QwenLM/qwen-code/pull/10357)

---

### 7. `#10367` — `qwen-live` 独立语音守护进程包（M1+M2）
**作者**: LaZzyMan  
**说明**: 新增 `packages/qwen-live` 孵化包，交付 M1（最小循环）与 M2（丰富交互），`packages/cli` 保持不动。属于 Live 拆分路线图（#10118）的一部分。  
**意义**: 语音交互的独立演进路径，降低对主 CLI 的侵入。

[PR #10367](https://github.com/QwenLM/qwen-code/pull/10367)

---

### 8. `#9940` — 多轮评审：回复携带进原线程，已修复项自动标记
**作者**: wenshao  
**说明**: 仍存在问题的 finding 以回复形式进入原评论线程；判定已修复的 finding 自动标记为已解决。  
**意义**: 大幅改善 PR 评审的上下文连续性，减少信息碎片化。

[PR #9940](https://github.com/QwenLM/qwen-code/pull/9940)

---

### 9. `#9769` — Web-Shell“更新项目”支持脏工作区
**作者**: wenshao  
**说明**: 当 `git pull` 因未提交更改被阻断时，分支选择器底部自动提供“解决冲突”面板（两种处理路径），替代原先的单行错误提示。  
**意义**: 提升 Web 端日常 Git 操作的容错体验。

[PR #9769](https://github.com/QwenLM/qwen-code/pull/9769)

---

### 10. `#9110` — 清理临时工作目录的项目快照
**作者**: ZijianZhang989  
**说明**: 会话目录消失后，其 `projects/` 快照条目现可在优雅退出时自动清理（非 ACP、非 handoff 会话）。  
**意义**: 减少运行时存储泄漏，对长期运行实例友好。

[PR #9110](https://github.com/QwenLM/qwen-code/pull/9110)

---

## 功能需求趋势

| 方向 | 代表 Issue / PR | 热度 |
|------|----------------|------|
| **流式传输稳定性** | #5975 超时误报、#9005 Anthropic 流安全、#10347 自动重试 EOF | 🔥🔥🔥 |
| **TUI 渲染架构升级** | #8662 ink → OpenTUI、#9475 屏幕错乱、#9970 渲染性能优化 | 🔥🔥🔥 |
| **Agent 协议（ACP）统一** | #10061 SDK 1.x 升级、#4542 daemon 服务分层 | 🔥🔥 |
| **渠道集成可靠性** | #10267/#10274 DWS 私信、#10357 钉钉卡片恢复 | 🔥🔥 |
| **本地模型兼容性** | #10065 LM Studio grammar、#10227 Moonshot schema | 🔥🔥 |
| **记忆机制结构化** | #10183 按需召回、#8083 Config 所有权 | 🔥 |
| **语音交互独立化** | #10367 qwen-live 独立包 | 🔥 |

---

## 开发者关注点

1. **流式传输不稳定是当前首要痛点**：#5975（120s 超时误报）与 #9005（Anthropic 线路缺保护）共同指向流式链路健壮性不足，直接影响 Coding Agent 的日常体验，社区反馈情绪较强烈。

2. **TUI 渲染质量亟待改善**：#9475（屏幕错乱）与 #8662（ink 架构局限）形成“症状+病因”组合，OpenTUI 迁移虽在推进，但用户短期内仍受闪烁/错位问题困扰。

3. **v0.22 升级存在回归风险**：#10147（本地命令/文件编辑失效）为 P2 级核心功能回归，尽管可能为个例，但用户对“自动升级不可关闭”表达了明确不满，建议关注后续 hotfix。

4. **第三方模型/本地服务接入门槛偏高**：#10227（Moonshot schema）与 #10065（LM Studio grammar）均属“配置无误但请求失败”类型，建议增加针对不同供应商的协议适配或更清晰的错误日志。

5. **CI 稳定性信号需警惕**：今日新增多条 Main 分支 E2E 测试失败（#10356、#10350、#10313 等），尽管大部分已由 bot 自动跟踪修复，但高频失败仍反映测试基础设施（如 Java 11 夹具、共享状态隔离）需要持续加固。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-28

> 数据来源：[Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)（原 DeepSeek-TUI）


## 1. 今日速览

项目正式进入 **v0.9.12 发布收尾阶段**：集成分支 #5576 已达成"阻断项全部完成、代码冻结"状态，多个性能优化与 UX 改进 PR 集中合入主线。社区讨论焦点集中在 **上下文压力警告的瞬态性问题**（#5620）、**MCP/插件启动过程的会话可见性**（#5658/#5677 已修复）以及 **Git 文件锁冲突**（#5617/#5618）三方面。

值得注意的信号：仓库内的"provider 中立性"审计（#5588）与运行时单例锁问题（#5630）提示项目正从"DeepSeek 专属工具"向"通用 AI 编码终端"迭代，架构层面的多会话/多 provider 支持成为隐性主线。


## 2. 版本发布

过去 24 小时无新 Release。当前迭代周期为 **v0.9.12**，集成分支 `0.9.12-integration`（#5576，72 commits）已完成全部 release blocker，剩余版本号 bump 与 changelog/RC 门禁检查，预计近期发版。


## 3. 社区热点 Issues（10 条）

### 🔥 高热度 / 影响面大

**#5620 — Context 压力警告是瞬态的，Agent 不会主动响应**（[链接](https://github.com/Hmbown/CodeWhale/issues/5620)）
- 作者发现上下文窗口压力警告只出现一次便消失，Agent 不会基于该信号主动压缩或调整策略，导致静默的上下文质量劣化。严重级别定为 Medium，9 条评论持续讨论中。属于"安全信号失效"类问题，直接影响长会话场景的可靠性。

**#5630 — 运行时存储 owner 锁阻断单机多会话**（[链接](https://github.com/Hmbown/CodeWhale/issues/5630)）
- v0.9.12 集成提交引入机器级单 owner 锁，第二个 CodeWhale 实例直接硬失败。对使用多窗口/多项目并行开发的用户影响严重，该 Issue 已在 24 小时内关闭，但修复方式值得关注。

**#5617 — 后台 git 探测持有 `.git/index.lock` 导致用户 commit 失败**（[链接](https://github.com/Hmbown/CodeWhale/issues/5617)）
- 用户 `git commit` 偶发失败，根因是 CodeWhale 的内部只读探测调用了真实 `git status`，与用户提交竞争锁。已关闭，修复方向为减少不必要的 git 进程调用。

### 🧩 功能增强 / UX

**#5668 — 新增 `/copy` 命令复制上一条模型完整输出**（[链接](https://github.com/Hmbown/CodeWhale/issues/5668)）
- 用户反馈长轮次输出后手动选中复制非常笨拙，提议增加显式命令。2 条评论，方向明确，预计实现成本低。

**#5625 — 非阻塞式"用户待输入" peek 工具**（[链接](https://github.com/Hmbown/CodeWhale/issues/5625)）
- 提案：Agent 在长时间工具调用链中需要用户确认时，提供一个非阻塞的轻量工具让模型"看一眼"是否有待办输入，避免盲目继续执行或空等。仍处于 proposal 阶段。

**#5553 — `/context` 增加工具目录与 MCP server 的 token 成本归因**（[链接](https://github.com/Hmbown/CodeWhale/issues/5553)）
- 当前 `/context` 只估算系统层与 Skills，用户无法看到每个 MCP server 每轮对话的 token 开销。已关闭，预计已实现。

**#5579 — 插件 UX 对齐 Claude Code：主动推荐、热重载、可发现性**（[链接](https://github.com/Hmbown/CodeWhale/issues/5579)）
- 用户明确要求插件体验达到 Claude Code 水平，当前 `/plugin` 命令组已覆盖大部分功能，剩余差距在于推荐与重载的主动性。3 条评论，属于 0.9.12 周期内的用户直接诉求。

### 🛠️ 架构 / 工程化

**#5588 — 18 个 DeepSeek 专属门禁应改为 provider 中立**（[链接](https://github.com/Hmbown/CodeWhale/issues/5588)）
- 全量审计 279 个文件中的 `deepseek` 出现（2281 行），发现 18 处行为级 DeepSeek 门禁但概念上应当对所有 provider 通用（如 NVIDIA NIM 环境变量泄漏已修复）。该项目正从 DeepSeek 专属走向多 provider 中立架构的重要信号。

**#5587 — 死代码清理第 2-4 阶段：75 个 test-only 标记、242 个过期 allow**（[链接](https://github.com/Hmbown/CodeWhale/issues/5587)）
- 继第 1 阶段移除 8 个确认死项后，继续审计 379 个 `allow(dead_code)` 站点，将 18 个真正死项（Tier B/C）与测试专用 helper 区分处理。工程卫生类工作，有助于减小单体 crate 的编译负担（呼应 #5249）。

**#5249 — v0.9.5 构建时车道：停止单体税（monolith tax）**（[链接](https://github.com/Hmbown/CodeWhale/issues/5249)）
- 核心痛点：682,959 行/620 文件的 `codewhale-tui` crate 占 workspace 86%，每次编辑/提交/测试/发布都全量重编。虽然创建于 8 月 4 日，至今仍是工程侧最大痛点，与 #5587 （清理）和 #5316 （crate 拆分）共同构成"拆分为主"的长期主线。


## 4. 重要 PR 进展（10 条）

**#5680 — 移除已发布的 fingerprint 发布说明门禁**（[链接](https://github.com/Hmbown/CodeWhale/pull/5680)）
- 清理类：删除一个过时的 changelog 契约（该迁移已在 v0.9.11 发布），保留所有行为级测试。

**#5679 — 保持工具结果批次连续性**（[链接](https://github.com/Hmbown/CodeWhale/pull/5679)）
- 修复：确保每个 assistant 工具调用批次后紧跟一个连续完整的工具结果 run，批次被用户/系统内容打断时丢弃延迟媒体，拒绝重复工具调用 ID。提升对话流中工具链的稳定性。

**#5658 & #5677 — MCP 与插件启动作为会话集合呈现**（[链接 #5658](https://github.com/Hmbown/CodeWhale/pull/5658) / [链接 #5677](https://github.com/Hmbown/CodeWhale/pull/5677)）
- 用户痛点：第一轮对话在 "working · 22s · 0 steps" 期间插件发现与 MCP server 逐一启动完全不可见。此系列 PR 将启动过程转为会话级状态展示，命名连接中的 server，失败以持久状态而非一次性 toast 呈现。**对体感影响非常直接的 UX 修复**。

**#5665 — 每轮压力路径上的单遍 token 记账**（[链接](https://github.com/Hmbown/CodeWhale/pull/5665)）
- 性能：每轮元数据构建与压缩决策各自重复遍历完整 transcript，流式渲染每 chunk 重新处理整个累积消息。此 PR 将遍历降为单遍，属于 #5620（context 压力警告）背后的性能配套。

**#5664 — 削减进程启动、诊断分发与前台命令延迟**（[链接](https://github.com/Hmbown/CodeWhale/pull/5664)）
- 三处性能修复：诊断子命令构建了一个从未使用的 45 线程 tokio runtime；models.dev 目录每个进程重复解析；另有前台命令相关延迟削减。全部基于 profiling 而非猜测。

**#5667 — 0.9.12 发布列车：性能合并 + 兼容 host + 删除暂存 runtime_contract**（[链接](https://github.com/Hmbown/CodeWhale/pull/5667)）
- 发布整合：合入 #5664/#5665/#5666，将 Baseten/Groq/Cerebras 标记为"兼容 host"，并删除暂存的 runtime_contract 文件。

**#5676 / #5672 / #5675 — 依赖例行更新**（[链接 #5676](https://github.com/Hmbown/CodeWhale/pull/5676) / [#5672](https://github.com/Hmbown/CodeWhale/pull/5672) / [#5675](https://github.com/Hmbown/CodeWhale/pull/5675)）
- futures-util 0.3.33→0.3.34、async-trait 0.1.91→0.1.92、uuid 1.24→1.25，均为 dependabot 例行升级，无破坏性变更。

**#5670 — tailwindcss 3→4 大版本升级（/web）**（[链接](https://github.com/Hmbown/CodeWhale/pull/5670)）
- web 目录 Tailwind 3.4→4.3，需要关注样式回归风险，当前 OPEN。

**#5666 — 将审计过的 test-only helper 改为 `#[cfg(test)]`**（[链接](https://github.com/Hmbown/CodeWhale/pull/5666)）
- #5587 的已批准首片：13 个 TUI 渲染/文本测试工具函数从 `#[allow(dead_code)]` 转为 `#[cfg(test)]`，减少生产代码中的死代码噪音。

**#5669 — 更新 nixpkgs 并修复 crates.io 403**（[链接](https://github.com/Hmbown/CodeWhale/pull/5669)）
- 修复 `nix run github:hmbown/codewhale#codewhale` 的构建失败，并添加 dependabot 每月自动更新 nixpkgs。


## 5. 功能需求趋势

从活跃 Issue 中可提炼出以下方向性需求：

1. **多 Provider 中立化（架构级趋势）**：#5588 对 18 处 DeepSeek 专属门禁的系统性审计表明，项目正从"DeepSeek 专用 TUI"向"通用 AI 编码终端"演进。这可能是最近的隐藏主线。

2. **多会话 / 多实例支持**：#5630（单例锁）反映用户已在一个机器上同时跑多个 CodeWhale，且 #5617/#5618 的 git 锁问题也因多实例叠加而加剧。工程上尚未准备好"多开"这一使用模式。

3. **上下文窗口管理精细化**：#5620（瞬态压力警告）+#5665（单遍 token 记账）组成"压力感知 → 主动响应"的闭环诉求，要求 Agent 不只是显示警告，而是真正基于上下文压力调整行为。

4. **启动/引导过程可视化**：#5658/#5677 修复了 MCP 与插件启动不可见的问题，用户体感直接提升。此类"看得见的初始化"需求在本地优先工具中很典型。

5. **Claude Code 功能对齐（插件 UX）**：#5579 明确要求插件主动推荐与热重载，说明用户以 Claude Code 为基准衡量 CodeWhale 的体验下限。

6. **Web 端依赖大版本跳跃**：/web 目录出现 tailwindcss 4、TypeScript 7、Next.js 16 等大版本 PR，前端栈在快速跟进生态。


## 6. 开发者关注点

**高频痛点 / 反馈：**

1. **git 锁冲突（影响协作开发）**：#5617 被真实用户（LmeSzinc）提交，git commit 偶发失败直接影响日常开发流。虽然通过减少后台 git 进程缓解，但 #5618 进一步提出用 gix（gitoxide）替换 CLI 调用——这是根治方向。

2. **上下文退化是静默的**：#5620 指出警告一闪而过、Agent 不行动，开发者希望 AI 在上下文压力下主动采取措施（压缩、总结、提示用户），而非仅展示。

3. **构建时间是持续痛点**：#5249 虽是 8 月初的 Issue，但仍是工程侧最大税负；#5587/#5666 的死代码清理是为缓解编译负担所做的具体努力。

4. **本地工具链（nix）可复现性**：#5669 修复了 `nix run` 构建 403，说明有开发者通过 nix 使用该项目，且该路径此前是断裂的——此类基础工具链问题优先级需提高。

5. **上游依赖升级频率高**：24 小时内 4 个 dependabot PR（futures-util、async-trait、uuid、jsonschema、next、typescript、tailwindcss、nixpkgs），依赖维护负担明显，但反馈均为例行升级，无破坏性报告。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*