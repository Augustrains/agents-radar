# AI CLI 工具社区动态日报 2026-08-01

> 生成时间: 2026-08-01 01:27 UTC | 覆盖工具: 9 个

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

# AI CLI 工具生态横向对比分析报告

**报告日期：2026-08-01**

---

## 1. 生态全景

当前 AI CLI 工具已全面进入 **"生产环境考验期"**。九大工具（Claude Code、OpenAI Codex、Gemini CLI、Copilot CLI、Kimi Code、OpenCode、Pi、Qwen Code、CodeWhale）均呈现出高频迭代与社区反馈暴增并存的状态，且问题高度集中在 **自动模式安全防护、长会话稳定性、配额计费透明度、跨平台兼容性** 四大领域。引人注目的是，**所有工具都出现了安全/权限相关的严重缺陷**，包括 Claude Code 的 rm -rf 绕过防护、Gemini CLI 的 SSRF 漏洞、Qwen Code 的 Windows 符号链接保护缺失——**安全已成为全行业的共同阿克琉斯之踵**。与此同时，各家均在加速向 **Agent 协议互操作（ACP/MCP）、Realtime 会话、插件生态** 方向演进，竞争正在从"单点工具"向"Agent 开发平台"升维。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues | 活跃 PR | Release 情况 | 最高赞 Issue | 社区焦点 |
|------|------------|---------|-------------|-------------|---------|
| **Claude Code** | 10（1条安全事件） | 6 | 无新版本 | 83 👍（滚轮回归） | Fable 5 计费缺陷、自动模式安全 |
| **OpenAI Codex** | 10 | 10+（含多项功能） | 3 个 alpha（0.147.0-alpha.x） | 185 👍（60秒自动确认） | 桌面端稳定性、MCP 资源泄漏 |
| **Gemini CLI** | 8（含3个安全相关） | 10（含2个并行修复） | 3 条线（stable/preview/nightly） | 8 👍（Generalist 挂起） | 子代理可靠性、thoughtSignature 回归 |
| **Copilot CLI** | 10 | 无核心功能 PR | 1 个预发布（v1.0.78-0） | 6 👍（ACP ask_user） | 会话恢复 OOM、计划模式回归 |
| **Kimi Code** | 4 | 1 | 无 | 23 👍（远程控制） | 远程控制、记忆系统 |
| **OpenCode** | 10 | 12+（多为清理） | 无 | 29 👍（文本选择） | Go 服务 401、信任危机 |
| **Pi** | 10 | 10（含架构级） | 无 | 5 👍（compaction 不触发） | 流式性能、Compact 可靠性 |
| **Qwen Code** | 10 | 10 | v0.21.2 | 31 评论（多工作区 RFC） | daemon 资源治理、Anthropic 转换器 |
| **CodeWhale** | 10（含2个安全） | 10（大量依赖更新） | v0.9.3 RC | 5 评论（Constitution 翻译） | 工具调用可靠性、sandbox 白名单 |

**数据速览**：
- **最活跃**：OpenAI Codex（PR 密度最高）与 Pi（架构级重构）
- **最受关注的单 Issue**：Codex #28969（185 👍，禁用 60 秒自动确认）——反映了全行业对"自动化安全边界"的焦虑
- **多版本并行发布**：仅 Gemini CLI 在维护 stable/preview/nightly 三条线，显示成熟的发布工程能力
- **值得警惕**：OpenCode 的 Go 订阅服务连续 10 天 401 故障且无修复时间表，付费用户信任快速流失

---

## 3. 共同关注的功能方向

### 3.1 破坏性操作防护（最紧迫）

| 工具 | 具体诉求 | 代表 Issue |
|------|---------|-----------|
| Claude Code | `rm -rf` 嵌套在反引号中绕过防护直接执行 | #81273 |
| Copilot CLI | Autopilot 任务完成强制力可覆盖用户"仅研究"指令 | #4318 |
| Gemini CLI | 子代理权限在禁用后仍自动生效 | #22093 |
| CodeWhale | sandbox 需要路径白名单（无法访问 DerivedData 等外部产物） | #5005 |
| Qwen Code | Windows 平台符号链接保护缺失（`O_NOFOLLOW` 不存在） | #8227 |

**共性结论**：所有工具的自动/代理模式均存在"安全边界不可预期"的问题，开发者强烈要求 **细粒度的权限控制 + 透明的执行策略**。

### 3.2 长会话稳定性与状态持久化

| 工具 | 具体问题 |
|------|---------|
| Copilot CLI | 恢复大会话 OOM（1.0.74 回归，内存提高 3-4 倍）、`events.jsonl` 过大永久无法恢复 |
| Codex | 图片 base64 重复发送导致上下文无限膨胀 |
| Claude Code | 会话记录 30 天自动删除、存储路径不在备份范围 |
| Pi | auto-compaction 永不触发、compaction 后不恢复执行、JSON 模式 O(n²) 输出 |
| Qwen Code | 180K+ token 时模型输出格式漂移 |
| CodeWhale | 中断的助手输出未持久化为会话项 |
| Gemini CLI | 低信号会话无限重试 |

### 3.3 配额/计费透明度

- **Claude Code**：Fable 5 有配额却提示需 credits、静默降级（#79337, #79441）
- **OpenCode**：Go 订阅大面积 401、qwen3.7-max 异常高频扣费（#38257, #36399）
- **Codex**：Plus 配额 24 小时耗尽（#36353）
- **Kimi Code**：暂无相关报告

### 3.4 跨机器/跨会话恢复

- **Claude Code**：#31992（CLI 到 CLI 无缝交接，15 👍）
- **Kimi Code**：#1282（远程控制，23 👍）
- **Gemini CLI**：#22598（子代理轨迹可分享）
- **Codex**：PR #36389（线程历史单写者所有权）、#380（线程分区）

### 3.5 插件/生态建设

- **Codex**：远程插件搜索（#36409）、MCP 自动审查（#36365）
- **OpenCode**：#28696（统一市场/注册中心，23 👍）
- **Claude Code**：#83034（跨项目启用状态同步）
- **Gemini CLI**：#21968（技能和子代理采用率低）

### 3.6 MCP/ACP 协议可靠性

- **Codex**：MCP 进程泄漏不回收（RSS 9+ GB）
- **Gemini CLI**：MCP OAuth token 刷新失败、SSRF 漏洞
- **Copilot CLI**：嵌套子代理的 MCP 工具依赖未文档化的授权
- **OpenCode**：ACP 会话更新通知时序错误
- **Qwen Code**：ACP 子进程内存无上限（50% 宿主机）
- **CodeWhale**：构建协议无关的 ACP 客户端（#4996）

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线 | 独特优势 | 显著短板 |
|------|---------|---------|---------|---------|---------|
| **Claude Code** | 全功能自动化 Agent | 企业级开发者、追求高自主性 | 深度自治 + 沙箱 | 功能最全、模型能力最强 | Fable 5 计费混乱、自动模式安全缺陷多 |
| **OpenAI Codex** | 开源 Rust 核心 + IDE 生态 | 偏好开源、VS Code 重度用户 | Rust CLI + 扩展生态 | PR 密度最高、架构演进快 | 跨平台稳定性弱（macOS/Windows/WSL 问题多） |
| **Gemini CLI** | 多模型支持 + 子代理体系 | 多模型切换用户、Google 生态 | 子代理 + Auto Memory | 发布工程最成熟（三线并行） | 子代理可靠性差、记忆系统有隐私问题 |
| **Copilot CLI** | GitHub 深度集成 | GitHub 企业用户、ACP 开发者 | ACP 协议 + Agent 模式 | GitHub 生态协同 | 版本回归频繁、企业级管理缺失 |
| **Kimi Code** | 轻量快速迭代 | 独立开发者、移动办公族 | 极简 + 远程控制 | 轻量、响应快速 | 功能积累最少、热度偏低 |
| **OpenCode** | 付费订阅服务 | 追求开箱即用的商业用户 | Go 订阅 + TUI | 模型接入及时 | 服务稳定性差、信任危机、TUI 黑屏 |
| **Pi** | 高度可定制、性能极致 | 技术极客、自托管倾向用户 | Rust 核心 + 可组合 server | 架构设计最优雅（server 模式） | 生态小、community 规模有限 |
| **Qwen Code** | 全链路服务端（daemon/serve） | 国内开发者、企业服务端 | serve 守护进程 + Web Shell | daemon 架构独特（多工作区） | Windows 安全短板、终端体验回归 |
| **CodeWhale** | 面向 DeepSeek 生态的通用客户端 | DeepSeek 用户、新模型尝鲜者 | Rust + TUI + sandbox | 快速适配新模型（V4 Flash） | 核心工具可靠性不足、品牌迁移期混乱 |

**共性技术路线**：所有工具均在从"对话式 CLI"向 **"Agent 运行时 + 协议层（ACP/MCP）+ 插件生态"** 演进。Pi 的 `PiServer` 可组合架构和 Codex 的远程插件搜索代表了两种不同的生态建设路径。

---

## 5. 社区热度与成熟度评估

### 活跃度排名（基于 Issue 评论数、PR 密度、版本频率综合判断）

| 梯队 | 工具 | 特征 |
|------|------|------|
| **T1（高活跃）** | OpenAI Codex、Claude Code、Qwen Code | PR 密度高、Issue 量大、版本迭代快 |
| **T2（中活跃）** | Gemini CLI、Copilot CLI、Pi、OpenCode | 稳定产出但节奏稍缓；Pi 有架构级 PR 但 Issue 量级较小 |
| **T3（量小质精）** | CodeWhale、Kimi Code | 社区规模小但增长快，热点集中 |

### 成熟度特征对比

| 工具 | 发布纪律 | 社区回应速度 | 安全事件 | 架构稳定性 |
|------|---------|-------------|---------|-----------|
| **Claude Code** | ⭐⭐（无新版本） | ⭐⭐⭐（多 Issue 高赞） | 🔴（凭据泄露、rm -rf 绕过） | ⭐⭐（回归多） |
| **Codex** | ⭐⭐⭐（3 个 alpha） | ⭐⭐⭐（PR 响应快） | 🟡（一般） | ⭐⭐⭐（架构演进清晰） |
| **Gemini CLI** | ⭐⭐⭐⭐（三线并行） | ⭐⭐⭐（cherry-pick 及时） | 🔴（SSRF 漏洞） | ⭐⭐⭐ |
| **Copilot CLI** | ⭐⭐⭐（预发布频繁） | ⭐⭐（回归修复慢） | 🟡 | ⭐⭐（OOM 回归） |
| **OpenCode** | ⭐（无发布） | ⭐⭐（401 10 天未解决） | 🔴（隐私承诺移除） | ⭐⭐ |
| **Pi** | ⭐⭐ | ⭐⭐⭐（inprogress 追踪细致） | 🟡 | ⭐⭐⭐⭐（server 架构先行） |
| **Qwen Code** | ⭐⭐⭐（v0.21.2） | ⭐⭐⭐（P1 修复快） | 🟡（Windows 短板） | ⭐⭐⭐（daemon 体系完善） |
| **Kimi Code** | ⭐⭐ | ⭐⭐ | 🟡 | ⭐⭐ |
| **CodeWhale** | ⭐⭐⭐⭐（RC 集成规范） | ⭐⭐⭐（修复提交快） | 🟡 | ⭐⭐⭐ |

---

## 6. 值得关注的趋势信号

### 6.1 安全防护已到"不得不重构"的临界点
Claude Code 的 `rm -rf` 绕过、Gemini CLI 的 SSRF、Qwen Code 的 Windows 符号链接缺失——**同一天三大工具出现安全漏洞**。这不是巧合，而是 AI CLI 工具能力快速膨胀过程中安全设计滞后的必然结果。**开发者应假设任何启用自动模式的工具都可能执行破坏性操作**，并在此之前：
- 优先使用 sandbox/容器模式
- 审查工具默认权限（如 Qwen Code 的 ACP 子进程 50% 内存上限）
- 关注各工具的权限模型更新（如 Copilot CLI 的 `/permissions` 命令）

### 6.2 "自动化程度"与"用户控制权"的拉锯战成为产品分水岭
- Codex #28969（185 👍）要求**禁用** 60 秒自动确认
- Codex PR #36373 引入 `--approve-for-me` **增强**自动化
- Copilot CLI Autopilot 强制力可覆盖用户明确指令（#4318）
- Claude Code 自动模式灾难性删除防护被绕过

**结论**：优秀的 AI CLI 不是"越自动越好"，而是**让用户决定何时自动化**。可配置的审批策略、透明的执行计划、可中断的自动化流程将成为差异化关键。**这一趋势对开发者的启示是：你在选工具的时候不必假设工具的自动操作是安全的，而要看它给不给你足够的开关和闸门。**

### 6.3 长会话管理是下一个技术高地
五个工具独立面临会话恢复 OOM（Copilot CLI）、上下文膨胀（Codex）、compaction 不触发（Pi）、会话记录丢失（Claude Code）、中断输出未持久化（CodeWhale）——**这不是巧合**。所有工具都采用"完整快照 + 增量压缩"的简单策略，在多日长会话场景下必然崩溃。**会话压缩算法、增量持久化、跨机器同步**将成为下一阶段的竞争焦点。

### 6.4 "信任经济"成为付费工具的生命线
OpenCode 的信任危机（零留存移除、401 持续 10 天、计费异常三线并发）与 Claude Code 的 Fable 5 计费混乱、Codex 的配额耗尽疑云，共同指向一个事实：**AI CLI 的付费用户对"用量透明"和"服务稳定"的敏感度正在快速上升**。API 型产品的留存取决于用户能否精确预测成本。

### 6.5 协议层正在成为新的竞争维度
- **Codex**：远程插件搜索、MCP 自动审查、实时会话控制（PR #36413, #36408, #36409）
- **Pi**：可组合 `PiServer`（传输无关的 framed-CBOR 协议）
- **CodeWhale**：协议无关的 ACP 客户端
- **Qwen Code**：daemon 资源治理 + Web Shell

ACP/MCP 正在从"可选协议"变成"平台底座"。**谁掌握了协议层，谁就掌握了开发者生态的入口**——这可能是未来 12 个月最重要的战略竞争点。

### 6.6 Windows/WSL 支持成为硬指标
涉及 Windows/WSL 的 Issue 在所有工具中均占比最高（Codex #34133/#35119/#31786、Claude Code #65833、Pi #6187、Qwen Code #8227、CodeWhale #4977/#5006）。在 Windows 开发者持续增长的背景下，跨平台稳定性和输入法/终端兼容性不佳将从"减分项"变为"一票否决项"。

---

## 给技术决策者的建议

1. **安全敏感场景**：暂缓采用高自主性工具（Claude Code/OpendCode）的自动模式，优先选择具有 sandbox + 细粒度审批的工具（如 Qwen Code daemon、Pi server）
2. **长会话依赖**：关注 Pi（server 模式架构最前瞻）、Codex（线程分区管理 API）的会话压缩方案；Copilot CLI 的大会话 OOM 问题尚未解决，可暂缓升级 1.0.74+ 版本
3. **企业级部署**：Copilot CLI 的企业配置缺失（#3909）和 Qwen Code 的 daemon 多工作区仍为 RFC——企业规模化采用需等待这两个方向落地
4. **新工具评估**：CodeWhale v0.9.3 的规范工具集、ACP 客户端方向值得关注——它是唯一以"协议互操作"为核心定位的轻量工具

---

*报告生成时间：2026-08-01 | 数据来源：各工具 GitHub 官方仓库社区动态*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是基于 anthropics/skills 仓库数据（截至 2026-08-01）的 Claude Code Skills 社区热点报告。

---

## 1. 热门 Skills 排行

基于 PR 评论数及功能价值，以下 6 个 Skills 受到社区最高关注：

- **[fix(skill-creator): run_eval.py 评估脚本全面修复](https://github.com/anthropics/skills/pull/1298)** — 作者: MartinCajiao | 状态: Open
  **功能**：修复 `run_eval.py` 报告 0% 召回率的严重 Bug，该 Bug 导致技能描述优化循环失效。
  **讨论热点**：这是社区痛点 #556 的集中爆发。大量用户反馈技能评估系统完全失效，该 PR 试图从根因（安装、Windows 流读取、触发检测、并行 worker）彻底修复，是目前生态健康度最关键的 PR。

- **[新增 document-typography 文档排版技能](https://github.com/anthropics/skills/pull/514)** — 作者: PGTBoos | 状态: Open
  **功能**：针对 AI 生成文档的排版缺陷（孤行、寡行段落、编号错位）进行质量控制。
  **讨论热点**：直击 AI 文档生成的"最后一公里"痛点，用户普遍认为这是高质量交付的必需品，市场需求明确。

- **[新增 ODT 技能（OpenDocument 格式处理）](https://github.com/anthropics/skills/pull/486)** — 作者: GitHubNewbie0 | 状态: Open
  **功能**：创建、填充、读取和转换 ODT/ODS 等 OpenDocument 格式文件，并可解析为 HTML。
  **讨论热点**：填补了微软 Office 格式之外的空白，满足开源生态和 ISO 标准格式的办公需求，讨论聚焦于 LibreOffice 集成场景。

- **[新增 testing-patterns 测试模式技能](https://github.com/anthropics/skills/pull/723)** — 作者: 4444J99 | 状态: Open
  **功能**：覆盖完整测试栈的综合性技能，包含测试哲学（Testing Trophy 模型）、单元测试、React 组件测试等实践指南。
  **讨论热点**：社区对"如何正确测试"的需求旺盛，该 PR 试图将测试最佳实践标准化，讨论聚焦于技能粒度是否过大、是否应拆分为多个独立技能。

- **[新增 pyxel 复古游戏开发技能](https://github.com/anthropics/skills/pull/525)** — 作者: kitao | 状态: Open
  **功能**：基于 pyxel-mcp 服务器的复古/像素风游戏开发技能，覆盖"编写 → 运行捕获 → 检查 → 迭代"的完整游戏开发循环。
  **讨论热点**：由 Pyxel 作者本人提交，结合 MCP 服务器能力实现游戏画面实时反馈，讨论聚焦于"写代码+看画面"的闭环工作流。

- **[新增 self-audit 自审计技能](https://github.com/anthropics/skills/pull/1367)** — 作者: YuhaoLin2005 | 状态: Open
  **功能**：交付前先进行机械文件验证，再按损害严重度优先级进行四维度推理审计。
  **讨论热点**：针对 AI 输出"看似正确实则出错"的信任危机，社区热议 AI 可靠性与交付质量保障机制。

---

## 2. 社区需求趋势

从 Issues 提炼的社区最期待方向：

- **组织级技能共享机制** — ([#228](https://github.com/anthropics/skills/issues/228)) 要求企业内技能库与一键分享，解决手动下载传输的繁琐流程。
- **安全与信任边界** — ([#492](https://github.com/anthropics/skills/issues/492), 43 评论) 社区最担忧的是 `anthropic/` 命名空间下混入社区技能，造成权限滥用的信任边界漏洞。
- **技能创建/评估工具修复** — ([#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169)) 评估脚本全面失效是当前最大技术债，社区迫切要求修复以支撑生态发展。
- **AI 代理治理与安全模式** — ([#412](https://github.com/anthropics/skills/issues/412)) 要求提供策略执行、威胁检测、信任评分等治理模式，这表明技能使用已进入企业级生产环境。
- **专业技能（如 SAP 预测分析）** — ([#181](https://github.com/anthropics/skills/pull/181)) 企业用户希望集成 Open Source 专业模型，拓展业务数据分析能力。

---

## 3. 高潜力待合并 Skills

以下 PR 评论活跃、价值明确，近期落地可能性较高：

- **[新增 color-expert 色彩专家技能](https://github.com/anthropics/skills/pull/1302)** — 作者: meodai | 状态: Open
  覆盖 ISCC-NBS、Munsell、OKLCH 等色彩体系与色彩空间选择指南，由专业设计师贡献，提升设计类任务的色彩科学性与一致性。

- **[新增 plan-file-hygiene 计划文件卫生技能](https://github.com/anthropics/skills/pull/1479)** — 作者: Palo-Alto-AI-Research-Lab | 状态: Open
  针对规划工件缺乏生命周期管理的问题，为计划文件提供管理策略，拥有明确的社区议题基础（#1417）。

- **[新增 skill-quality-analyzer 与 skill-security-analyzer 元技能](https://github.com/anthropics/skills/pull/83)** — 作者: eovidiu | 状态: Open
  对技能进行五维质量分析与安全审查，建立技能发布前的质量门槛，与 #492 安全担忧形成呼应。

---

## 4. Skills 生态洞察

一句话总结：**当前社区最集中的诉求是"实用性与可靠性"** — 一方面需要像排版控制、测试模式、ODT 支持这样的专业深度技能；另一方面，`skill-creator` 评估工具链的全面失效已成为生态健康的首要障碍，社区的核心关切在于**确保现有技能的生产可用性**与**建立可信任的发布与共享机制**。

---

# Claude Code 社区动态日报 — 2026-08-01

> 数据来源：[anthropics/claude-code](https://github.com/anthropics/claude-code) GitHub 仓库


## 今日速览

Fable 5 模型集成问题成为社区讨论焦点，多条高热度 Issue 直指其在使用额度判定、会话降级与安全防护上的缺陷。与此同时，关于自动模式下的数据破坏性操作与安全机制绕过的报告持续激增，暴露出工具在自治操作与用户保护之间的深层张力。此外，多项围绕会话恢复、沙箱配置与插件管理的功能请求也获得了开发者广泛关注。


## 版本发布

过去 24 小时内无新版本发布。


## 社区热点 Issues

### 1. [Fable 5 提示 "usage credits required"，Max 计划用户被静默降级](https://github.com/anthropics/claude-code/issues/79337)
- **热度**：51 条评论 | 👍 20
- 自 7 月 20 日 Fable 5 成为 Max 计划标配以来，用户报告其在 Max 计划下被拒绝运行 Fable 5，并被静默降级至 Opus 4.8。涉及计费判定、认证与模型路由多个环节，是当前社区反馈最集中的问题之一。

### 2. [v2.1.150 回归：滚轮不再滚动会话，而是发送方向键](https://github.com/anthropics/claude-code/issues/65833)
- **热度**：35 条评论 | 👍 83（本日最高 👍 数）
- WSL 平台上的 TUI 回归问题——更新后滚轮行为完全反转，影响日常会话浏览。已持续近两个月，开发者期待尽快修复。

### 3. [Claude Code Web 无法使用 gh CLI 命令（权限被拒）](https://github.com/anthropics/claude-code/issues/11139)
- **热度**：28 条评论 | 👍 31
- Web 环境下权限隔离导致 GitHub CLI 无法正常工作，阻塞依赖 `gh` 的自动化工作流。该问题已存在较长时间，社区持续关注。

### 4. [VS Code 扩展同样错误拦截 Fable 5 使用](https://github.com/anthropics/claude-code/issues/79441)
- **热度**：13 条评论 | 👍 10
- 用户账户仍余 20% 周度 Fable 配额，但 VS Code 扩展仍提示 "requires usage credits"。与 #79337 相互印证，指向服务端计费判定逻辑缺陷。

### 5. [GPU 进程崩溃导致 Claude Desktop 崩溃并损坏 MSIX 包](https://github.com/anthropics/claude-code/issues/81159)
- **热度**：9 条评论
- Windows 11 上 Opus 5 执行页内浏览器操作时触发 GPU 进程崩溃（exitCode 101457950），进而损坏应用安装包，属于较严重的平台稳定性问题。

### 6. [跨会话凭据泄露：他人在会话中泄露的生产数据库凭证导致未授权修改](https://github.com/anthropics/claude-code/issues/72274)
- **热度**：6 条评论 | 👍 1
- **安全事件**：某用户的会话中出现了另一用户的服务器凭证，并被用于修改生产数据库。涉及跨会话数据隔离的严重安全缺陷。

### 7. [功能请求：跨机器会话恢复（CLI 到 CLI 无缝交接）](https://github.com/anthropics/claude-code/issues/31992)
- **热度**：8 条评论 | 👍 15
- 开发者希望将当前会话状态同步到另一台机器继续工作，对远程开发和多设备协作场景有较高价值。

### 8. [Claude Code Web 中 Gradle wrapper 下载失败——Java 不遵守 https_proxy](https://github.com/anthropics/claude-code/issues/16222)
- **热度**：5 条评论 | 👍 17
- 代理环境下 Java 不继承 `https_proxy` 导致构建工具无法下载依赖，影响企业网络和受限网络环境下的使用。

### 9. [自动模式灾难性删除防护被绕过：反引号替换中的 rm -rf 不触发确认](https://github.com/anthropics/claude-code/issues/81273)
- **热度**：1 条评论
- 安全防护漏洞：`rm -rf` 嵌套在反引号命令替换中时，自动模式防护机制未触发，命令直接执行。属于重大安全缺陷。

### 10. [会话记录默认存储于备份覆盖范围之外且 30 天后自动删除——项目历史永久丢失](https://github.com/anthropics/claude-code/issues/83019)
- **热度**：1 条评论
- 会话记录默认存储路径不佳、自动清理周期过短，可能导致项目历史永久丢失，开发者反馈强烈。


## 重要 PR 进展

### 1. [PR #81540：修复 Usage 数据泄漏问题](https://github.com/anthropics/claude-code/pull/81540)
- **状态**：已关闭 | 自动提交
- 由 Atlas 2 自动生成的修复补丁，针对 Issue #80705 的 Usage 数据泄漏问题。已运行测试并验证仓库。

### 2. [PR #82987：修复 CI 定时任务失败，提出 TUI 延迟修复方案](https://github.com/anthropics/claude-code/pull/82987)
- **状态**：开放
- 修复 GitHub Actions Cron 任务失败，排除 PR 触发干扰；同时提出针对高代理工作负载下 TUI 输入延迟的架构级修复建议。

### 3. [PR #82794：code-review 插件实现置信度评分与 --threshold 标志](https://github.com/anthropics/claude-code/pull/82794)
- **状态**：开放
- 修复 README 文档与命令实际行为不一致的问题，实现 0–100 置信度评分（原为二元验证），保留原有 truth-check。

### 4. [PR #39872：Node.js 版本从 20 升级至 24](https://github.com/anthropics/claude-code/pull/39872)
- **状态**：开放
- 为即将到来的 LTS 变更做准备，将运行时从 Node 20 升级至 24。

### 5. [PR #17776：为 security-guidance 插件补充 README 文档](https://github.com/anthropics/claude-code/pull/17776)
- **状态**：已关闭
- 为 `plugins/` 目录下唯一缺少文档的插件补全 README，涵盖全部 9 个安全模式说明。

### 6. [PR #82981：自动化工单（Claude/automatizar inventario insumos）](https://github.com/anthropics/claude-code/pull/82981)
- **状态**：开放
- 标题为西班牙语自动化工单，内容初步判断与库存自动化相关，暂未提供详细技术说明。


## 功能需求趋势

| 需求方向 | 代表 Issue | 热度 |
|---------|-----------|------|
| **跨机器/跨会话恢复** | #31992 | 8 评论 / 15 👍 |
| **模型使用的精细控制**（配额透明、防止静默降级） | #79337 / #79441 / #83036 | 高 |
| **沙箱配置的层级继承**（嵌套项目不丢失配置） | #83035 | 新 |
| **插件管理**（跨项目启用状态同步） | #83034 | 新 |
| **Session 生命周期管理**（恢复、归档、后台结果拉取） | #83012 / #83019 / #83001 | 新 |
| **CLI/Web 桥接**（CLI 与云/Web 会话联动） | #83012 | 新 |
| **代理与网络兼容性** | #16222 | 17 👍 |


## 开发者关注点

**高风险功能（当前反馈最集中）**：
- **Fable 5 集成缺陷**：多条 Issue 指向计费判定错误（有配额却提示需 credits）、静默降级、手动切换被阻止、配额计算不一致等问题，开发者对模型可用性和配额透明度的信任正在下降。
- **数据安全与误删风险**：本周多起严重报告——`rm -rf` 绕过防护直接执行、跨会话凭据泄露、自动模式删除用户目录、命令被展开为 `rm -rf /*` 后防护机制还阻止了 kill 操作（#82165）。此趋势表明自动模式的安全防护机制存在系统性缺陷。
- **TUI/IDE 可用性回归**：滚轮失效（#65833）、暗色模式白字白底不可读（#62911）、VS Code 扩展功能缺失（#79919）等细节问题虽不致命，但持续影响日常体验。

**高频请求**：
- 更透明的配额显示与模型路由控制
- 跨机器/跨项目会话状态同步
- 对 `rm -rf` 等破坏性操作的更强防护（即使嵌套在命令替换中）
- 会话记录的可靠持久化与备份友好存储

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-01

> 数据来源：github.com/openai/codex


## 今日速览

今日 Codex 仓库共发布 3 个 Rust CLI 增量版本（0.147.0-alpha 系列），核心为常规修复与稳定性提升。社区讨论焦点主要集中在两大方向：一是 **Codex Diff 在 macOS 上崩溃**（#35058，42 评论）与 **Windows 上 GPU 进程崩溃**（#34133，30 评论）等 IDE/桌面端稳定性问题；二是 **MCP 子进程泄漏**（#30408）与 **自动确认 60 秒计时器**（#28969，64 评论）等服务端资源管理问题。此外，PR 侧密集合入了与**实时（realtime）会话控制**、**远程插件搜索**及**沙箱/V8 安全**相关的功能改进。


## 版本发布

过去 24 小时发布了 3 个 Rust CLI 版本，均为 0.147.0-alpha 系列增量：

- **[rust-v0.147.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.4)** — 0.147.0-alpha.4
- **[rust-v0.147.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.3)** — 0.147.0-alpha.3
- **[rust-v0.147.0-alpha.1.1](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.1)** — 0.147.0-alpha.1.1

*注：以上均为 Rust 核心 CLI 的预发布版本，无详细变更日志随附。*


## 社区热点 Issues

以下按讨论热度和影响力筛选出 10 个值得关注的 Issue：

1. **[#28969 添加禁用 60 秒自动确认问题的设置](https://github.com/openai/codex/issues/28969)** — 64 评论 / 185 👍（OPEN，6月18日创建）
   社区强烈要求对 Codex CLI 在提问后 60 秒自动确认的行为提供开关选项。这是目前评论数和点赞数双高的 Issue，用户普遍认为自动确认在复杂审批场景中风险过高。`[CLI]` `[config]` `[plan]`

2. **[#35058 Codex Diff 在 macOS 上崩溃：显示 "Oops, an error has occurred"](https://github.com/openai/codex/issues/35058)** — 42 评论 / 109 👍（OPEN，7月24日创建）
   VS Code 扩展中 Codex Diff 功能完全不可用，影响所有仓库。当前热度最高的 IDE 集成问题之一，用户期待尽快修复。`[extension]` `[VS Code]`

3. **[#34133 Windows 上浏览器截图导致 GPU 进程崩溃](https://github.com/openai/codex/issues/34133)** — 30 评论（OPEN，7月19日创建）
   Codex 桌面应用内置浏览器在截图后触发 GPU 进程崩溃，并因 Code Integrity 拒绝签名错误的 `vk_swiftshader.dll` 导致应用冻结或无法重启。`[windows-os]` `[browser]` `[app]`

4. **[#30408 MCP 服务器进程泄漏：每个线程产生独立 MCP 进程且永不清理](https://github.com/openai/codex/issues/30408)** — 21 评论 / 6 👍（OPEN，6月28日创建）
    应用服务器为每个会话/线程生成完整 MCP 进程组，关闭线程后进程不回收，已观察到 RSS 达 9+ GB。属于长期积累的资源泄漏问题，社区呼声较高。`[mcp]` `[performance]`

5. **[#25779 桌面版元问题：无界会话/轮次状态导致冻结、上下文膨胀与活动轮次失控](https://github.com/openai/codex/issues/25779)** — 13 评论 / 8 👍（OPEN，6月2日创建）
   汇总了桌面版无界会话状态带来的多个关联问题：应用冻结、上下文持续膨胀以及丢失活动轮次控制。`[app-server]` `[session]` `[performance]`

6. **[#35119 Windows/WSL 26.721.3404 将有效 WSL 仓库误判为非 Git](https://github.com/openai/codex/issues/35119)** — 11 评论 / 11 👍（OPEN，7月24日创建）
   WSL2 下 Codex 版本更新后，将 ext4 上的有效 Git 仓库标记为“非 Git”并报告“Git is unavailable”，影响 WSL 重度用户的核心工作流。`[windows-os]` `[WSL]`

7. **[#28316 Codex 不应在后续上下文中重发大体积 base64 图片工具输出](https://github.com/openai/codex/issues/28316)** — 10 评论 / 3 👍（OPEN，6月15日创建）
   图片作为工具输出被持久化到会话历史，在后续 `/v1/responses` 请求中重复发送，造成上下文无限膨胀和 token 浪费，社区呼吁尽快优化。`[CLI]` `[context]`

8. **[#29645 内置 image_gen 在普通卡牌美术提示下超时（约 240 秒）](https://github.com/openai/codex/issues/29645)** — 10 评论 / 3 👍（OPEN，6月23日创建）
   简单图像生成提示可成功，但普通复杂度的卡牌美术提示在约 240 秒后超时。`[image_gen]` `[connectivity]`

9. **[#36353 ChatGPT Plus 周配额 24 小时内耗尽：疑似用量记账错误](https://github.com/openai/codex/issues/36353)** — 6 评论（OPEN，7月31日创建）
   用户报告 Plus 订阅的 Codex 周配额在一天内耗尽，与预期严重不符。用量记账准确性是社区长期关注的话题，尤其集中在配额与速率的计算上。`[codex-web]` `[rate-limits]`

10. **[#31786 Windows 远程控制 WSL 到 Android 完全无法工作](https://github.com/openai/codex/issues/31786)** — 16 评论（OPEN，7月9日创建）
    配对过程看似成功，但手机端始终停留在“connecting”状态，远程控制链路断裂，影响跨平台工作流。`[windows-os]` `[remote]`


## 重要 PR 进展

过去 24 小时内 PR 侧动作频繁，以下 10 个值得关注（均非 bot 自动生成）：

1. **[#36413 增加实时委托确认控制](https://github.com/openai/codex/pull/36413)** — 新增 `delegationAckFiller` 字段到 `thread/realtime/start`，显式控制实时会话中的委托确认行为。归属核心会话控制能力。`[realtime]`

2. **[#36410 明确用户输入阻塞行为](https://github.com/openai/codex/pull/36410)** — 引入必填的 `isBlocking` 参数区分“等待用户显式响应”与“可自动解析”的 `request_user_input` 请求，修复了此前用 `autoResolutionMs` 混淆阻塞策略的问题。可能回应了 #28969 的诉求。`[user-input]`

3. **[#36389 对线程历史强制执行单写者所有权](https://github.com/openai/codex/pull/36389)** — 继承式或分页式线程历史均增加跨进程写锁，修复潜在的状态竞争条件。`[concurrency]`

4. **[#36408 允许为实时模式转换自定义 Codex 指令](https://github.com/openai/codex/pull/36408)** — 新增 `realtimeStartInstructions` / `realtimeEndInstructions` 字段，提升实时会话的可配置性。`[realtime]`

5. **[#36409 实现远程插件搜索](https://github.com/openai/codex/pull/36409)** — `plugin/search` 直接查询远程插件服务，支持全局、工作区及个人作用域，带分页游标。是插件生态的重要基础设施。`[plugins]`

6. **[#36411 使用 Git 仓库作为预工具钩子测试标记](https://github.com/openai/codex/pull/36411)** — 重构预工具钩子测试，使用 `git init` 作为命令执行标记，提升测试隔离性与可靠性。`[testing]`

7. **[#36374 为代码模式启用沙箱化 V8](https://github.com/openai/codex/pull/36374)** — 解决 Windows MSVC 构建仍使用非沙箱 V8 预编译包的问题，直接开启 `v8_enable_sandbox` 特性，提升代码模式安全性。`[sandbox]` `[V8]`

8. **[#36372 使用 MSVC 运行原生 Windows Bazel 测试](https://github.com/openai/codex/pull/36372)** — Windows 原生构建的 CI 全面切换到 MSVC 工具链，强化 Windows 平台支持。`[windows]` `[CI]`

9. **[#36365 为 MCP 引出请求增加严格自动审查](https://github.com/openai/codex/pull/36365)** — 识别 `codex_strict_auto_review` 标记，将审批路由至自动审查器，失败时默认关闭，提高第三方 MCP 调用的安全性。`[MCP]` `[security]`

10. **[#36373 增加 `--approve-for-me` CLI 标志](https://github.com/openai/codex/pull/36373)** — 交互与 exec 命令均可通过该标志将审批请求路由至自动审查流程，配合 `workspace-write` 沙箱。显著改善自动化流水线的体验。`[CLI]` `[approval]`

*另有 **[#36380 线程分区管理 API](https://github.com/openai/codex/pull/36380)**（threadSection 增删改查）与 **[#36393 避免冗余文件系统探测](https://github.com/openai/codex/pull/36393)**（减少文件系统调用、复用 socket 连接）等多项后端效率改进，显示了 Codex 在系统稳定性和 API 完备性上的持续投入。*


## 功能需求趋势

从近期的 Issue 与 PR 中可以提炼出以下社区核心关注方向：

- **实时（Realtime）会话深度定制**：围绕 `thread/realtime/*` 出现多个 PR（#36413、#36408），涵盖委托确认、进出实时模式的指令定制。用户对实时协作场景的控制粒度要求正在提升。`[realtime]`

- **插件生态扩展（远程搜索）**：远程插件搜索（#36409、#36402）与 MCP 自动审查（#36365）共同指向 Codex 插件体系的深化：不仅仅是把插件跑起来，还要可搜索、可治理。`[plugins]` `[MCP]`

- **MCP 生命周期治理**：从进程泄漏（#30408）到 OAuth 生命周期（#35006），MCP 的服务质量与生命周期管理成为高频关键词。`[MCP]`

- **配额/计费透明度与效率**：多个 Issue 指向配额消耗异常（#36353、#32250）和 token 浪费（#36396、#28316、#35259），社区对用量效率与计费准确性的关注持续升温。`[rate-limits]`

- **审批与自动化的平衡**：围绕“自动确认”与“审批策略”出现了正反两面讨论（#28969 要求禁用自动解析，#36373 则引入 `--approve-for-me`），核心诉求是让用户自己决定自动化程度。`[approval]`


## 开发者关注点

- **稳定性是第一优先级**：无论是 macOS 上 VS Code 的 Codex Diff 崩溃（#35058）、Windows 的 GPU 崩溃（#34133），还是 WSL 仓库误判（#35119）与启动崩溃（#36225），跨平台桌面端稳定性问题正在成为开发者放弃使用或回退版本的主要原因。
- **资源泄漏的长期代价**：MCP 进程不回收（#30408）在长会话场景下会造成 GB 级内存占用，与会话状态无界增长（#25779）叠加，严重影响应用的长时间稳定性与可用性。
- **上下文管理与 token 效率**：图片 base64 重复发送（#28316）和子代理空转消耗配额（#36396）等核心问题在开发者中引发了广泛讨论。高频词是“context bloat”与“wasted tokens”。用户希望 Codex 在上下文压缩、工具调用结果去重等方面做出改进。
- **Windows 与 WSL 支持仍需加强**：涉及 Windows/WSL 的问题数量多且覆盖面广——从 Git 检测（#35119）、远程控制（#31786）、Chrome 插件更新（#32706）到 App 启动崩溃（#36225）。开发者对 Codex 在 Windows 生态的成熟度仍有较高期待。
- **自动化与安全边界**：`--approve-for-me` 和自动审查的引入获得了积极回应，但社区同时呼吁提供更细粒度的控制开关（如禁用 60 秒自动确认），希望在不牺牲安全的前提下获得更高的自动化自由度。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-01

## 今日速览

今日发布三个版本：stable v0.53.1、preview v0.54.0-preview.1 及 nightly v0.55.0，核心修复聚焦于**容量耗尽导致的重试挂起**和 **InvalidStreamError 错误提示优化**。社区层面，**子代理（Subagent）在达到 MAX_TURNS 后误报为 GOAL 成功**（#22323）与 **Generalist agent 无限挂起**（#21409）成为最受关注的两大高优 Bug。此外，多线程 PR 正在修复 v0.53.0 引入的 `thoughtSignature` 丢失导致的 400 错误回归。

## 版本发布

### v0.53.1（Stable）
- **fix(core)**: 将容量耗尽（capacity exhaustion）归类为终止状态，防止无限重试挂起
- **fix(core, cli)**: 将 `InvalidStreamError` 详细信息传递至 UI，针对空响应场景提供具体引导（如提示使用 `/compress`）
- 该版本为 cherry-pick 修复，合并过程中存在冲突已解决

[查看 Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.53.0...v0.53.1)

### v0.54.0-preview.1（Preview）
- 从 v0.54.0-preview.0 修补，包含与 v0.53.1 相同的两项核心修复

[查看发布详情](https://github.com/google-gemini/gemini-cli/releases)

### v0.55.0-nightly.20260801（Nightly）
- 包含上述核心修复的完整版本

[查看发布详情](https://github.com/google-gemini/gemini-cli/releases)

## 社区热点 Issues

### 🔥 高优先级 Bug（P1）

**1. Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption** ( #22323 )
- **标签**: `priority/p1`, `area/agent`, `kind/bug`
- **核心问题**: `codebase_investigator` 子代理在达到最大轮次限制时仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，**掩盖了中断事实**，导致主代理误判任务已完成
- **社区反应**: 12 条评论，2 👍，被标记为 `status/need-retesting`
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

**2. Generalist agent hangs** ( #21409 )
- **标签**: `priority/p1`, `area/agent`, `kind/bug`
- **核心问题**: 当 Gemini CLI 委派给 generalist agent 时，**无限期挂起**。即使是简单的文件夹创建，用户等待长达一小时后取消。手动指示模型不要委派给子代理可绕过此问题
- **社区反应**: 8 条评论，8 👍（高共鸣），仍在复测中
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

**3. Shell command execution gets stuck with "Waiting input" after command completes** ( #25166 )
- **标签**: `priority/p1`, `area/core`, `kind/bug`, `effort/medium`
- **核心问题**: 简单 CLI 命令执行完毕后，界面仍显示命令活跃并处于 "Awaiting user input" 状态，**shell 已结束但界面挂起**
- **社区反应**: 4 条评论，3 👍，影响面较大
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

**4. Gemini CLI encounters 400 error with > 128 tools** ( #24246 )
- **标签**: `priority/p2`, `area/agent`, `kind/bug`（原为 P1，降至 P2）
- **核心问题**: 工具数量超过 128 个（原描述为 400，后更正）时收到 400 错误，期望 agent 能智能限制启用工具范围
- **关联**: 与 #28586 和 #28607 的 `thoughtSignature` 修复直接相关
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

### 📌 值得关注的稳定性与安全性问题

**5. Browser Agent ignores settings.json overrides (e.g., maxTurns)** ( #22267 )
- **标签**: `priority/p2`, `area/agent`, `kind/bug`, `status/need-retesting`
- **核心问题**: Browser Agent 完全忽略全局/项目级 `settings.json` 中的配置覆盖（如 `maxTurns`），`AgentRegistry` 正确读取但未生效
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22267)

**6. (Sub)agents running without permission since v0.33.0** ( #22093 )
- **标签**: `priority/p2`, `area/agent`, `kind/bug`, `status/need-retesting`
- **核心问题**: v0.33.0 后子代理（如 generalist）在**所有配置中 agent 模式均已禁用**的情况下仍被自动使用，用户仅期望 MCP 功能
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22093)

**7. Auto Memory 相关三个连环问题** — 低信号会话无限重试 ( #26522 )、敏感数据脱敏缺陷 ( #26525 )、无效补丁静默跳过 ( #26523 )
- **标签**: 均为 `priority/p2`, `area/agent` 或 `area/security`
- **要点**: Auto Memory 后台提取器存在**隐私风险**（读取本地 transcript 并发送至模型后才提示脱敏）、**无效补丁导致 inbox 膨胀**、以及**低信号会话被无限重试**等问题，作者 SandyTao520 提交了系统的改进建议

- [查看 #26522](https://github.com/google-gemini/gemini-cli/issues/26522) | [查看 #26525](https://github.com/google-gemini/gemini-cli/issues/26525) | [查看 #26523](https://github.com/google-gemini/gemini-cli/issues/26523)

**8. Gemini does not use skills and sub-agents enough** ( #21968 )
- **标签**: `priority/p2`, `area/agent`, `kind/bug`
- **核心问题**: **技能和子代理采用率低**。即使用户提供了带有清晰描述的 gradle/git 技能，Gemini 在相关场景下也不会主动使用，除非显式指示
- **社区反应**: 6 条评论，属于长期体验类问题
- [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

## 重要 PR 进展

### 🚀 关键修复（优先关注）

**1. fix(core): preserve functionCall thoughtSignature when stripping thought parts** ( #28607 )
- **状态**: OPEN | 新增 | 修复 v0.53.0 回归
- **内容**: 修复 `API Error 400: Function call is missing a thought_signature`。`stripThoughts()` 在移除思考内容时误删了 `thoughtSignature`，影响并行工具调用
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28607)

**2. fix(core): preserve thoughtSignature in functionCall parts to fix 400 error** ( #28586 )
- **状态**: OPEN | 与 #28607 功能重叠但独立提交
- **内容**: 同样修复 400 错误，`thoughtSignature` 在 v0.53.0 中被无意剥离。两位开发者独立提交修复方案，需要协调合并
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28586)

**3. fix(core): fall back to stable models when a preview model 404s with Gemini API key auth** ( #28608 )
- **状态**: OPEN | 新增
- **内容**: 当 Gemini API key 项目无 preview 模型访问权限时（收到 404），自动回退到 stable 模型，修复配置初始化时的崩溃。Fixes #28600
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28608)

**4. fix: resolve SSRF vulnerability in web-fetch.ts by using async DNS resolution** ( #28557 )
- **状态**: OPEN | 安全修复
- **内容**: `isBlockedHost` 使用同步 `isPrivateIp()` 仅拦截字面 IP，域名指向内网地址（如 `169.254.169.254`）时绕过校验。改用异步 DNS 解析方式封堵 SSRF 漏洞。Fixes #28555
- **标签**: `priority/p1`, `area/security`
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28557)

**5. fix(core): refresh MCP OAuth tokens with the stored client ID** ( #28481 )
- **状态**: OPEN | 已发送提醒
- **内容**: 修复通过 OAuth discovery + 动态客户端注册配置的 MCP 服务器的 token 刷新问题。刷新在网络 I/O 前即失败，且失败后删除已存凭据，导致每次需重新认证
- **标签**: `priority/p1`, `area/security`
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28481)

### 🌟 功能改进与基础设施

**6. fix(core, cli): propagate InvalidStreamError details to UI for specific empty response guidance** ( #28566 )
- **状态**: CLOSED（已合并至 v0.53.1 / v0.54.0-preview.1 / nightly）
- **内容**: 将 `InvalidStreamError` 的类型和消息传递至 UI，针对空响应场景提供具体处理建议（如 `/compress`）。此修复已通过 cherry-pick 进入三个发布线
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28566)

**7. fix(cli): fall back to embedded macOS seatbelt profiles if missing** ( #28551 )
- **状态**: OPEN | 等待关联 Issue
- **内容**: 修复 macOS sandbox 模式（`-s`）下静态 Seatbelt `.sb` 文件缺失导致的启动崩溃，改为使用内嵌 profile
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28551)

**8. fix(core): prevent infinite auth loop by awaiting credential save and forcing consent** ( #28519 )
- **状态**: OPEN | 已发送提醒
- **内容**: 修复无限认证循环。`oauth_creds.json` 的异步写入未被等待，导致凭据持久化前即被读取。Fixes #28430
- **标签**: `priority/p1`, `area/core`
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28519)

**9. fix(core): classify capacity exhaustion as terminal to prevent retry hangs** ( #28599 )
- **状态**: CLOSED（已合并至 v0.53.1 / v0.54.0-preview.1 / nightly）
- **内容**: 将容量耗尽错误归类为终止状态而非可重试，避免无限重试挂起
- [查看 PR](https://github.com/google-gemini/gemini-cli/pull/28599)

**10. cherry-pick 发布流程** ( #28609 / #28610 )
- **状态**: CLOSED
- **内容**: 将 f47d6c6 修复分别 cherry-pick 至 v0.54.0-preview.0（生成 v0.54.0-preview.1）和 v0.53.0（生成 v0.53.1），后者存在合并冲突已解决
- [查看 #28609](https://github.com/google-gemini/gemini-cli/pull/28609) | [查看 #28610](https://github.com/google-gemini/gemini-cli/pull/28610)

## 功能需求趋势

**1. 子代理（Subagent）可靠性成为第一优先级**
- 多个 P1/P2 Issue 围绕子代理挂起、误报成功、响应丢失（#21409, #22323, #21763）展开，反映子代理在生产环境中的**稳定性不足**
- 功能需求：子代理轨迹可通过 `/chat share` 分享 ( #22598 ) 以提升可观测性

**2. Browser Agent 成熟度待提升**
- 自动接管会话与锁恢复 ( #22232 )、尊重 settings.json 配置 ( #22267 )、Wayland 兼容性 ( #21983 ) 等多维度问题，表明 **browser_agent 距离生产可用仍有距离**

**3. 安全性关注度上升**
- 本周出现 **SSRF 漏洞修复** ( #28557 )、**Auto Memory 脱敏缺陷** ( #26525 )、**MCP OAuth token 刷新** ( #28481 ) 三个安全相关 PR/Issue
- 趋势：随着 Agent 能力增强（读取本地文件、执行命令），安全边界设计成为社区焦点

**4. 配置灵活性与自适应**
- 用户期望 Gemini CLI 能**更智能地使用已有配置**：自动限制工具数量 ( #24246 )、尊重禁用的 subagent 配置 ( #22093 )、正确读取 symlink 配置 ( #20079, #16247 )

**5. 记忆系统（Auto Memory）进入密集迭代期**
- 内存系统 Bug 与质量改进 ( #26516 ) 跟踪多个子问题，涉及脱敏 ( #26525 )、无效补丁 ( #26523 )、低信号会话重试 ( #26522 )
- 方向：在**隐私保护和记忆有效性**之间寻找平衡

## 开发者关注点

**高频痛点 Top 5：**

1. **Agent 挂起 / 误报成功**：MAX_TURNS 中断被误报告为 GOAL 成功、Generalist 无限挂起、shell 命令完成后界面卡死 — 这些严重影响用户对 Agent 自动化的信任
2. **v0.33.0+ 行为回归**：子代理在用户禁用后仍自动执行，打破用户预期，多名用户报告
3. **配置系统不一致**：`settings.json` 中的设置有时被正确读取但未生效（Browser Agent、symlink 支持），导致排查困难
4. **400 错误回归（thoughtSignature）**：v0.53.0 引入的回归在工具调用场景中频繁触发，多位开发者独立发现并提交修复（#28586 / #28607），建议尽快合并
5. **安全与隐私**：SSRF 漏洞、Auto Memory 在发送内容到模型前未脱敏、以及 OAuth 凭据被意外删除 — 安全问题成为企业用户关注重点

---

> 📌 **建议关注**: 两个 `thoughtSignature` 修复 PR (#28586 / #28607) 功能重叠，预计官方会协调合并。若你正在使用 v0.53.x 并遇到 400 错误，建议关注这两个 PR 或升级到 v0.53.1+ 验证修复效果。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026年8月1日

## 今日速览

今日最值得关注的动态是 **v1.0.78-0 预发布版本** 的推出，其核心改进在于为沙箱环境引入了 `allowDevToolCaches` 新设置，以提升构建兼容性。社区方面，围绕**计划模式 (Plan Mode) 回归**、**大模型会话恢复时的内存溢出**以及**沙箱安装特定版本失效**等问题的讨论最为激烈，反映出用户对核心工作流稳定性和资源消耗的高度关注。

---

## 版本发布

### v1.0.78-0 (预发布)
[查看 Release 详情](https://github.com/github/copilot-cli/releases)

- **新增**
  - 新增 `/permissions` 命令，可在不同审批模式间切换。
  - ACP 模式现已支持通过 `closeSession` 请求来关闭会话。
- **改进**
  - 新增沙箱设置 `allowDevToolCaches`（默认开启）：允许沙箱构建访问工具链缓存、软件源和安装包，从而提升构建成功率。

---

## 社区热点 Issues（精选）🔍

### 1. [回归] 计划模式被阻断执行 Shell 命令
**Issue #4188** | [链接](https://github.com/github/copilot-cli/issues/4188)
- 状态: 已关闭 | 评论: 7 | 👎: 3
- **要点**: 用户报告在最新版本的计划模式中，用于信息收集的 Shell 命令（如 `gh cli`）被新增的权限策略所阻断，破坏了原有的计划辅助流程。该问题在昨日被标记为已关闭，但社区对于计划模式权限边界的讨论仍未平息。

### 2. [回归] `task_complete` 工具在切换回 Autopilot 模式后不可用
**Issue #4161** | [链接](https://github.com/github/copilot-cli/issues/4161)
- 状态: 已关闭 | 评论: 4 | 👍: 4
- **要点**: 这并非新问题，而是在 1.0.4 版本声称修复后的再次回归。用户指出，在手动切换模式后，`task_complete` 工具会再次被过滤，影响自动化流程。

### 3. [性能] 恢复大型会话导致内存溢出 / 单核 100% 占用约 70 分钟
**Issue #4251** | [链接](https://github.com/github/copilot-cli/issues/4251)
- 状态: 开放 | 评论: 1
- **要点**: 该问题被证实是 **1.0.74 引入的严重回归**，相比 1.0.73 版本，恢复同一会话的内存占用提高了 3-4 倍，并伴随极长的 CPU 处理时间。这对依赖长期会话的开发者是重大打击。

### 4. [BUG] 解析错误：JavaScript 'Undefined' 转换为 Rust 'String' 失败
**Issue #4305** | [链接](https://github.com/github/copilot-cli/issues/4305)
- 状态: 已关闭 | 评论: 4 | 👍: 4
- **要点**: 升级到 1.0.76 后，几乎所有命令都会立即报出此类型转换错误。虽然已被关闭，但在修复版本发布前，这仍是影响面较广的紧急问题。

### 5. [特性] 企业级 / 组织服务器托管设置
**Issue #3909** | [链接](https://github.com/github/copilot-cli/issues/3909)
- 状态: 开放 | 评论: 4
- **要点**: 组织管理员无法集中为本地 CLI 下发环境变量等配置，只能依赖云端 Agents/Codespaces secrets。这是企业采用的关键痛点，社区持续关注。

### 6. [功能] ACP 扩展方法：`ask_user` / `ask_question`
**Issue #2109** | [链接](https://github.com/github/copilot-cli/issues/2109)
- 状态: 开放 | 评论: 2 | 👍: 6
- **要点**: 这是一个需求呼声较高的功能（👍 6），希望自定义 ACP 客户端能主动向用户提出澄清问题，而不仅仅是通过 `request_permission` 来处理。这将极大丰富第三方工具与 Copilot CLI 的交互方式。

### 7. [BUG] 安装特定版本总是下载并安装最新版本
**Issue #4317** | [链接](https://github.com/github/copilot-cli/issues/4317)
- 状态: 开放 (待分类) | 评论: 1
- **要点**: 用户希望在 Docker Sandbox 中回退到特定版本（v1.0.75），但安装器忽略了指定版本，总是获取最新版本。这使得用户无法通过降级来规避新版引入的问题。

### 8. [BUG] 会话记录文件过大导致无法恢复
**Issue #4325** | [链接](https://github.com/github/copilot-cli/issues/4325)
- 状态: 开放 (待分类) | 评论: 0
- **要点**: 长生命周期会话的 `events.jsonl` 文件超过了 V8 引擎的字符串长度上限，导致会话永久无法恢复。这暴露了 Copilot CLI 在处理超长会话时的状态持久化机制存在硬性瓶颈。

### 9. [BUG] 嵌套子代理的 MCP 工具依赖未文档化的直接父级授权
**Issue #4320** | [链接](https://github.com/github/copilot-cli/issues/4320)
- 状态: 开放 (待分类) | 评论: 0
- **要点**: 自定义代理在两层以下时无法获取其自身 `frontmatter` 中声明的工具，必须由直接父级代理声明才能生效。这与文档描述不符，且新行为基于未公开的实施细节，存在很大的不确定性。

### 10. [BUG] Autopilot 任务完成强制执行可覆盖用户明确指令
**Issue #4318** | [链接](https://github.com/github/copilot-cli/issues/4318)
- 状态: 开放 (待分类) | 评论: 1
- **要点**: 用户明确指示代理“仅做研究/解释”，但任务完成强制逻辑仍会推动代理继续执行操作。这表明 Copilot CLI 对用户指令的优先级理解存在偏差，对安全操作有潜在影响。

---

## 重要 PR 进展 🧩

过去24小时内没有新的功能性 PR，绝大多数为文档或配置变更，且不涉及核心代码逻辑。以下为昨日更新列表中的主要条目：

1. **#4316** | [Create devcontainer.json](https://github.com/github/copilot-cli/pull/4316) - 新增开发容器配置，以便于贡献者快速搭建开发环境。
2. **#3163** | [ViewSonic monitor](https://github.com/github/copilot-cli/pull/3163) - 该 PR 内容与项目核心功能无关，疑似误提交，社区可忽略。

---

## 功能需求趋势 📈

从今日的 Issue 动态中，可以提炼出社区最关注的功能方向：

1. **更细粒度的权限与审批控制**: 用户希望不仅仅是 ON/OFF 的审批模式，更希望像 `/permissions` 这样能切换具体模式的能力，以及计划/只读模式下对工具链的精细访问控制。
2. **对长会话与大型上下文的支持**: 多个 Issue（#4251, #4325）都指向了会话文件过大、内存占用过高的问题。社区亟需 Copilot CLI 优化上下文管理，支持更长、更复杂的任务。
3. **更友好的企业级可管理性**: 从 #3909 的高关注度来看，组织级的集中配置（环境变量、模型白名单）是拓展企业市场的关键。
4. **ACP 协议交互能力的增强**: 除了现有的事件和权限请求，社区希望增加双向的 `ask_user` 交互机制，让外部客户端能更灵活地嵌入工作流。
5. **终端渲染的稳定性与可导航性**: 多个 Issue 围绕终端 UI 的空白渲染、侧边栏无法用键盘导航等问题展开，表明终端的交互体验仍需打磨。

---

## 开发者关注点 💡

- **版本回退困难**: Issue #4317 的出现表明，当新版本引入回归问题时，用户缺少快速回到旧稳定版本的可靠途径。
- **计划模式的“管控”与“智能”平衡**: 开发者理解安全限制的必要性，但计划模式被过度限制（如阻断 `gh` 命令）会严重影响其“规划”职能。他们希望看到一个更智能、可配置的工具策略。
- **隐藏的魔法行为**: Issue #4320 中提到的“未文档化的直接父级授权” 让开发者感到困惑和不可控。社区呼吁核心机制应公开透明，避免基于隐晦的潜规则。
- **状态持久化可靠性**: 长会话依赖是 Copilot CLI 的核心工作流，任何导致会话丢失或无法恢复的问题（#4251, #4325）都会被放大为最优先级的 Bug。开发者期望官方能优先处理此类健壮性问题。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，各位开发者朋友，这是 2026 年 8 月 1 日的 Kimi Code CLI 社区动态日报。

---

## Kimi Code CLI 社区动态日报 | 2026-08-01

### 今日速览
今日社区热度集中在两大长期需求上：**跨设备远程控制**与**持久化记忆系统**。这两个 Issue 均积累了高赞与广泛讨论，反映出用户对“无缝衔接”开发体验的强烈诉求。此外，一个关于工具调用双重编码导致 Pydantic 校验失败的 PR 于今日提交，针对特定环境下的兼容性问题提供了修复方案。

---

### 社区热点 Issues

1.  **#1282 [Feature Request] 远程控制功能** `👍 23 | 💬 9`
    - **重要性**: 目前社区关注度最高的需求。用户希望能在手机或浏览器上接管本地正在运行的 Kimi Code CLI 会话，实现工作流的无缝切换。这代表了用户对“随时随地进行编码”的深度需求，可能是从桌面端向移动端延伸的关键信号。
    - **链接**: [Issue #1282](https://github.com/MoonshotAI/kimi-cli/issues/1282)

2.  **#1283 [Feature Request] 记忆系统** `👍 0 | 💬 8`
    - **重要性**: 这一需求虽无高赞，但已有多达8条评论，讨论热度高。用户希望 CLI 能跨会话记住项目模式、上下文和个人偏好，减少重复操作。这指向了AI编程工具从“单次对话助手”向“长期智能体”演进的迫切需求。
    - **链接**: [Issue #1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)

3.  **#2422 [Bug] 对话完成后滚动查看输出自动跳到底部** `👍 1 | 💬 2`
    - **重要性**: 一个影响使用体验的交互问题，在版本 1.46.0 及 kimi2.6 模型下复现。该问题出现在用户回顾长对话历史时，阻碍了信息回溯，属于高频交互场景下的痛点。
    - **链接**: [Issue #2422](https://github.com/MoonshotAI/kimi-cli/issues/2422)

4.  **#796 [Closed] error: the message at position 1 with role** `💬 1`
    - **重要性**: 该 Issue 今日被标记为关闭。它涉及早期版本（KimiCLI/1.3）中的角色消息格式错误问题。虽然已关闭，但开发者的更新动作表明团队仍在清理历史遗留问题，维持项目健康度。
    - **链接**: [Issue #796](https://github.com/MoonshotAI/kimi-cli/issues/796)

---

### 重要 PR 进展

1.  **#2572 fix(kosong): 递归解包工具调用参数中的双重编码 JSON** `新提交`
    - **内容**: 修复了当使用部分 API 提供商时，工具调用参数（如 SetTodoList）因嵌套值被双重编码为 JSON 字符串而导致 Pydantic 校验失败的问题。方案为对参数进行递归解码。
    - **意义**: 这是今日唯一一个新提交的 PR。它明确了当前工具调用时与部分上游供应商存在的兼容性问题，对于使用非 Moonshot 官方 API 作为后端的用户尤为重要。
    - **链接**: [PR #2572](https://github.com/MoonshotAI/kimi-cli/pull/2572)

---

### 功能需求趋势

从今日活跃的 Issue 中，可以提炼出以下核心趋势：

-   **跨设备与远程无缝衔接**: 以 **#1282** 为代表，用户不再满足于单机使用，希望将代码任务在桌面和移动设备间无缝迁移。
-   **增强的“记忆”能力**: 以 **#1283** 为代表，用户期待 CLI 具备更智能的上下文保留能力，实现跨会话的个性化与项目感知。
-   **完善的基础工具链**: 如 **#2422** 所显示的，终端交互细节的打磨（如滚动体验）也是社区关注的焦点。

---

### 开发者关注点

-   **痛点**: 知名 Bug（如 #2422）的修复进程被密切关注，尤其是近期版本（v1.46.0）中的回归问题。开发者在拉取新版本后，对基础交互体验的验收非常严格。
-   **高频需求**: “上下文连续性”是高频关键词，无论是通过远程控制（#1282）还是记忆系统（#1283）实现，开发者的核心诉求是减少重复劳动，让 AI 助手在长时间、多设备的开发工作中保持连贯的工作状态。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-01

---

## 今日速览

OpenCode Go 订阅服务今日爆发信任危机：`401 Request blocked by upstream provider` 错误影响大规模用户，同时 Go 服务被曝**悄然移除零数据留存承诺**引发社区强烈质疑（+33 👍）。与此同时，TUI 黑屏问题（#4140, #10221）持续困扰用户，成为仅次于服务故障的第二大热点。开发侧，社区正集中清理 TUI 代码冗余，等待功能层面的实质突破。

---

## 社区热点 Issues

### 1. OpenCode Go 大面积 401 故障 — 服务端问题实锤
**#38257** | 评论 42 | 👍 11
[链接](https://github.com/anomalyco/opencode/issues/38257)
> 自 7 月 22 日起，所有 Go 订阅模型的 `chat/completions` 端点返回 `401 Request blocked by upstream provider`，而 `/v1/models` 正常。用户确认非客户端问题，等待官方修复。

**重要性**：影响所有付费用户核心功能，持续 10 天未解决，社区耐心正在耗尽。

### 2. TUI 黑屏问题长期悬而未决
**#4140**（评论 37 | 👍 13）+ **#10221**（评论 33 | 👍 17）
- [#4140](https://github.com/anomalyco/opencode/issues/4140)：升级至 1.0.47 后黑屏，回退 1.0.46 恢复
- [#10221](https://github.com/anomalyco/opencode/issues/10221)：全新安装即黑屏，`--print-logs` 无有效输出

**重要性**：两个高度相关的 issue 累计 70+ 评论、30+ 点赞，是社区最痛恨的稳定性问题。

### 3. DeepSeek V4 Flash 正式版上线确认
**#39823** | 评论 22 | 👍 20
[链接](https://github.com/anomalyco/opencode/issues/39823)
> DeepSeek 于 7 月 31 日发布 V4-Flash-0731 正式版（Terminal Bench 82.7），用户急切确认 OpenCode Go/Zen 是否已接入该模型。

**重要性**：20 个 👍 表明社区对新模型支持的高度关注，官方未回复。

### 4. Go 服务零数据留存政策悄然移除
**#39861** | 评论 4 | 👍 13
[链接](https://github.com/anomalyco/opencode/issues/39861)
> 用户发现 OpenCode Go 文档中"零数据留存"表述已被删除（web.archive.org 可对比）。要求官方说明。

**重要性**：与 #39875（👍 20）共同指向信任危机，数据隐私是付费用户的底线问题。

### 5. 文本选择功能缺失（老 issue 回温）
**#927** | 评论 13 | 👍 29
[链接](https://github.com/anomalyco/opencode/issues/927)
> TUI 中无法选中/复制文本，拖拽无效。自 2025 年 7 月提出至今未实现，29 个 👍 表明是高频痛点。

**重要性**：最老、最受关注的功能请求之一，长期未解决。

### 6. 会话更新通知时序错误（ACP 集成）
**#17505** | 评论 15 | 👍 10
[链接](https://github.com/anomalyco/opencode/issues/17505)
> `session/update` 通知在 `session/prompt` 响应（end_turn）之后到达，导致 ACP 客户端（如 Fabriqa）界面内容不完整。

**重要性**：影响 ACP 生态集成质量，API 使用者共同痛点。

### 7. 流式工具调用解析失败
**#26412** | 评论 10 | 👍 2
[链接](https://github.com/anomalyco/opencode/issues/26412)
> 自定义 OpenAI 兼容提供方（vLLM 后端）下，工具调用的流式 chunk 触发 `Expected 'function.name' to be a string` 错误。

**重要性**：vLLM 本地部署用户的拦路虎，自定义提供方兼容性不足。

### 8. 上下文缓存失效导致性能下降
**#23595** | 评论 4 | 👍 11
[链接](https://github.com/anomalyco/opencode/issues/23595)
> `<system-reminder>` 位置不断漂移，导致 llama.cpp 提示缓存全部失效，本地推理时间大幅增加。

**重要性**：本地模型用户的性能杀手，11 个 👍 显示诉求普遍。

### 9. 插件/Agent/技能市场（统一提议）
**#28696** | 评论 6 | 👍 23
[链接](https://github.com/anomalyco/opencode/issues/28696)
> 社区发起统一市场/注册中心主 issue，覆盖发现、分发、安装。23 个 👍 表明生态建设是社区核心诉求。

**重要性**：最高赞的功能类 issue，代表社区对生态成熟的期待。

### 10. 会话计费异常：高频扣费
**#36399** | 评论 3 | 👍 0
[链接](https://github.com/anomalyco/opencode/issues/36399)
> Go 订阅用户反馈 qwen3.7-max 每 30 秒一次高频调用扣费，疑似计费逻辑缺陷。

**重要性**：涉及付费信任问题，与 401 故障叠加恶化用户情绪。

---

## 重要 PR 进展

### 1. Shell 命令失败输出精简
**#39982** | 已打开
[链接](https://github.com/anomalyco/opencode/pull/39982)
> 非零退出码时仅返回输出尾部（50 行/8KB），完整内容写入文件。提升工具输出可读性，问题 #39771 的第三部分。

### 2. TUI 测试稳定性：Mini Prompt 就绪等待
**#39980** | 已合并
[链接](https://github.com/anomalyco/opencode/pull/39980)
> 修复测试中提交时机竞态：显式等待默认模型、prompt-ready、turn-start 信号。

### 3. TUI 透明背景切换
**#5657** | 已打开（2025-12 提出）
[链接](https://github.com/anomalyco/opencode/pull/5657)
> 新增三态透明策略（auto/on/off），通过命令面板切换。已开放 7 个月。

### 4. 插件目录监听修复
**#39981** | 已打开
[链接](https://github.com/anomalyco/opencode/pull/39981)
> 修复 `.opencode/plugins/tui/` 目录在 TUI 启动后创建时无法被发现的问题。

### 5-10. 批量清理合并（bot + kitlangton）
以下 9 个 PR 由 `opencode-agent[bot]` 提交、kitlangton 请求，组成 TUI 代码库大扫除：

- **#39942** — 拖拽 Tab 只持久化一次，消除 flock→写入→重排竞态 [链接](https://github.com/anomalyco/opencode/pull/39942)
- **#39941** — Tab 状态卫生：失败不再静默、关闭会话状态清理 [链接](https://github.com/anomalyco/opencode/pull/39941)
- **#39940** — 隐藏 Tab 关闭热区：修复无 hover 终端误关 Tab [链接](https://github.com/anomalyco/opencode/pull/39940)
- **#39964 / #39963 / #39962 / #39961 / #39960 / #39959 / #39958 / #39957 / #39956 / #39955 / #39954 / #39953 / #39952** — 批量移除：无用 duration formatter、revert diff parser、warning helper、文件选择 helper、errorData 序列化器、locale 工具、Zed 助手、config optional hook、subagent retry 格式化器、attention KV 参数、占位 LSP 面板、FadeFilePath 组件、prompt 再导出桶 [链接](https://github.com/anomalyco/opencode/pull/39964) 等

**点评**：今日 PR 以清理为主，显示出维护者在为后续功能开发整合代码基础。唯一功能性 PR（#39982）值得关注。

---

## 功能需求趋势

**1. 隐私与透明（新增热点）**
- 零留存政策移除（#39861, 👍13）、提供方归属 + 遥测披露（#39875, 👍20）— **信任危机需官方回应**

**2. 市场/生态建设（长期呼声）**
- 插件/技能市场（#28696, 👍23）、提示/线程保存与书签（#24017）— 生态成熟度是社区核心期待

**3. 新模型支持（持续热度）**
- DeepSeek V4 Flash 接入确认（#39823, 👍20）、Go 服务模型可用性 — 用户对模型前沿性高度敏感

**4. IDE 与桌面端增强**
- VS Code 完成通知（#39936）、桌面端工具面板默认折叠（#39944）、跨项目会话崩溃（#39840）— 桌面体验差距明显

**5. 本地模型性能优化**
- 上下文缓存固定（#23595, 👍11）、模式切换缓存失效（#37489）— 本地推理用户群体增长

**6. 配置与集成能力**
- 私有 GitHub 仓库指令 URL（#39517）— 企业级使用需求

---

## 开发者关注点

**1. 服务稳定性告急（最尖锐）**
- Go 订阅 401 故障持续 10 天（#38257）、Zen 全部模型同样故障（#39827）、gpt-5.6-luna 流质量下降（#39881）— **付费用户在三个层面同时遭遇问题，信任快速流失**

**2. 数据安全承诺动摇**
- 零留存政策移除（#39861）+ 遥测增加嫌疑（#39875）— 社区敏感度极高，要求正面回应

**3. TUI 核心体验顽疾**
- 黑屏问题跨多个版本未修复（#4140, #10221）、输入框被黑块覆盖（#38773）、退出循环消息（#38801）— 基础可用性成疑

**4. 会话数据完整性问题**
- 切换模型后 SQLite 崩溃（#39165）、消息被静默忽略（#32719）、更新通知时序错误（#17505）— 对话数据可靠性是 AI 编程工具的底线

**5. 计费透明度**
- qwen3.7-max 异常高频扣费（#36399）、桌面端找不到订阅（#39883）— 财务问题最伤信任

---

**总结**：今日社区情绪以"信任危机"为主基调 — 服务故障、隐私承诺动摇、计费异常三线并发。建议官方优先回应用户对数据留存政策的质疑（#39861/#39875），公开 401 故障的修复时间表（#38257），以稳定付费用户信心。TUI 黑屏问题积累了 70+ 评论，是免费用户最大的流失点。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-01

> 数据来源: [github.com/badlogic/pi-mono](https://github.com/earendil-works/pi)

---

## 今日速览

过去 24 小时 Pi 仓库暂无新版本发布，但社区讨论热度持续升温，核心聚焦于三个方向：**流式输出的性能优化**（TUI 高 CPU 占用、JSON 模式 O(n²) 复杂度）、**Compact 流程可靠性**（自动触发失败、与手动触发冲突）以及 **Linux 平台的兼容性**（WSL 登录挂起、Wayland 剪贴板失效、旧 CPU 崩溃）。此外，`christianklotz` 提交了一系列关于会话持久化与协议服务器架构重构的 PR，标志着 server 模式正在快速成型。


## 社区热点 Issues

挑选 10 个最值得关注的 Issue，涵盖性能、兼容性与可靠性三大类：

1. **#6665 [inprogress] TUI 流式输出时单核满载** — [链接](https://github.com/earendil-works/pi/issues/6665)
   长会话下模型流式输出时 TUI 占满一个 CPU 核心。`spindump` 定位到热路径为 `Markdown.render → wrap → Intl.Segmenter (ICU BreakIterator)`，根因有二：字素分割未缓存、且每个 chunk 都会重建完整 Markdown。这是影响所有长会话用户的性能瓶颈。

2. **#6187 [OPEN] WSL 中 Pi 登录挂起** — [链接](https://github.com/earendil-works/pi/issues/6187)
   在 WSL 下安装成功，浏览器设备授权（GitHub Copilot）完成后，客户端无法检测到授权结果，login 流程永久挂起。19 条评论为本周最高，WSL 用户群体广、影响直接。

3. **#6879 [OPEN] 自动压缩（auto-compaction）永不触发** — [链接](https://github.com/earendil-works/pi/issues/6879)
   某 2 小时以上的 agentic 会话中，上下文占用超过 100% 后 footer 持续增长，compaction 始终未触发，直到 API 在 373k tokens 拒绝请求才被动介入（5 👍）。用户期望在每个 agent turn 后检查上下文水位。

4. **#7020 [inprogress] Compact 完成后有时不继续执行** — [链接](https://github.com/earendil-works/pi/issues/7020)
   长运行的 "coordinator" 会话在 compaction 后有时无法恢复执行。社区给出了复现条件：上下文窗口越接近极限越容易触发。

5. **#7149 [inprogress] Linux x64 二进制在旧 CPU 上 SIGILL 崩溃** — [链接](https://github.com/earendil-works/pi/issues/7149)
   官方二进制 `pi-linux-x64` 在 Sandy Bridge 等不支持 BMI2/AVX2 的 CPU 上直接崩溃（`shlx` 指令 SIGILL）。npm 包在同一台机器可正常运行，确认是构建目标问题。

6. **#7161 [inprogress] anthropic-messages 缺少 x-client-request-id** — [链接](https://github.com/earendil-works/pi/issues/7161)
   Anthropic 路径不发送 `x-client-request-id`，导致依赖该 header 做会话亲和的网关（如轮询多个 Claude 账号的代理）无法正确分组请求。

7. **#7253 [inprogress] `/compact` 触发双重压缩** — [链接](https://github.com/earendil-works/pi/issues/7253)
   当上下文接近 90% 时手动执行 `/compact` 会同时触发自动压缩，压缩完成后还会再次尝试压缩且无法停止，除非按 Esc（报错 "Compaction failed: Already..."）。

8. **#7290 [inprogress] `--mode json` 单次工具调用产生 O(n²) 输出** — [链接](https://github.com/earendil-works/pi/issues/7290)
   JSON 模式下每次 `message_update` 携带完整的累积 assistant 消息，单个工具调用即产生 O(n²) 的 stdout。一个写 64 KB HTML 的 agent 烧了 17 分钟且无产出，严重时可 OOM。

9. **#7248 [closed] Wayland 下 Ctrl+V 粘贴静默失败** — [链接](https://github.com/earendil-works/pi/issues/7248)
   `readClipboardText()` 仅实现了 X11 协议，Wayland 会话（KDE Plasma 6/Konsole）下从 Wayland 应用复制文本粘贴无效；从 X11 应用复制则正常。已由 #7387 修复。

10. **#7319 [closed] kimi-coding OAuth 401 未触发刷新/重试** — [链接](https://github.com/earendil-works/pi/issues/7319)
    kimi-coding 内置 provider 偶发 401 `authentication_error`，由于 401 被排除在重试分类器之外，turn 直接中断，不会刷新 token。


## 重要 PR 进展

挑选 10 个重要的 PR，按主题归类：

1. **#7394 [OPEN] JSON 流式输出改为线性复杂度** — [链接](https://github.com/earendil-works/pi/pull/7394)
   修复 #7290：JSON/RPC 模式改为仅发送 delta 更新，累积快照仅保留在内部/扩展事件中，并对 stdout 追加背压控制。破坏性 wire-protocol 变更已有迁移文档。

2. **#7390 [OPEN] x64 构建目标降级至 baseline** — [链接](https://github.com/earendil-works/pi/pull/7390)
   修复 #7149，将构建目标从 Haswell 降级为 baseline x64（兼容无 BMI2/AVX2 的旧 CPU）。注意：官方二进制将在旧 CPU 上恢复可用，但会牺牲部分新指令集性能。

3. **#7387 [CLOSED] Wayland 剪贴板读取支持** — [链接](https://github.com/earendil-works/pi/pull/7387)
   修复 #7248：优先使用 `wl-paste` 读取剪贴板，保留 X11 原生回退，并补充了 Wayland 文本、空剪贴板及回退路径的回归测试。

4. **#7396 [OPEN] server 模式会话后端** — [链接](https://github.com/earendil-works/pi/pull/7396)
   新增 `@earendil-works/pi-coding-agent/server` 后端：JSONL 持久化 + 跨进程排他锁 + 崩溃恢复；项目事件映射为协议快照与实时转录进度。

5. **#7386 [CLOSED] 可组合协议服务器** — [链接](https://github.com/earendil-works/pi/pull/7386)
   引入传输无关的 `PiServer`，支持认证 framed-CBOR 协议处理、Unix listener 构建块及预设 `createUnixServer`，并提供 `-works/pi-server/testing` 传输一致性测试工具。

6. **#7410 [CLOSED] SQLite 会话操作线性化** — [链接](https://github.com/earendil-works/pi/pull/7410)
   将 SQLite 连接缓存与投影状态的提交延迟到 append 事务成功之后；取消每次 append 的全量 entry 缓存克隆；分支路径构建改用 `push()+reverse()` 替代低效的 `unshift()`。

7. **#7404 [CLOSED] 新增 Baseten provider** — [链接](https://github.com/earendil-works/pi/pull/7404)
   在 `ai` 包中新增 Baseten 内置 provider（OpenAI 兼容），通过 `BASETEN_API_KEY` 启用。镜像 Together AI 集成模式。

8. **#7389 [CLOSED] 扩展原生 prompt API** — [链接](https://github.com/earendil-works/pi/pull/7389)
   向扩展暴露 `pi.prompt()`：扩展提交的输入走原生 command/skill/prompt-template 处理管线，支持图片与流式 steer/follow-up 行为，附带文档与测试。

9. **#7398 [CLOSED] 每会话存储队列** — [链接](https://github.com/earendil-works/pi/pull/7398)
   按会话串行化内存/JSONL 操作，不同会话可并发；`list()` 通过队列屏障保持快照一致；JSONL 文件系统并发上限为 4 个操作。

10. **#7391 [CLOSED] 会话搜索转为只读查询** — [链接](https://github.com/earendil-works/pi/pull/7391)
    移除公共 `SessionSearchIndex` 变更接口，将 `SessionSearch` 收敛为查询专用。SQLite 搜索仅依赖事务维护的 FTS 索引。


## 功能需求趋势

综合全部 Issues 与 PR，社区在 2026 年 7 月底至 8 月初最关注以下功能方向：

1. **流式与吞吐性能** — #6665（TUI 核心占用）、#7290（JSON O(n²)）、#7394（delta 流式）表明长会话下渲染与序列化是最大痛点，社区期待 O(1) 级流式更新。
2. **Compact 机制可靠性** — #6879、#7020、#7253 分别暴露了自动压缩不触发、压缩后不继续、双重压缩死循环三个问题，核心诉求是让 compaction 可预期、可中断、幂等。
3. **Linux 桌面与 WSL 体验** — #6187（WSL 登录）、#7248（Wayland 剪贴板）、#7149（旧 CPU 崩溃），三项均为 Linux 专属问题，表明 Pi 的桌面用户以 Linux 为主力。
4. **多 Provider 与账号管理** — #7161（Anthropic 请求 ID）、#7319（kimi-coding OAuth 401）、#7404（新增 Baseten）、PT #7199（Kimi K3 on Fireworks），社区持续要求更健壮的多账号/网关/模型覆盖。
5. **Server/无头模式架构升级** — christianklotz 的系列 PR（#7386、#7396、#7398、#7410、#7391）表明开发主线正在向可组合 server 与持久化重构推进，将直接改善远程/批处理场景。


## 开发者关注点

- **O(n²) 问题反复出现**：`--mode json` 全量消息携带和 TUI 全量 Markdown rebuild 本质上都是"增量更新"缺失导致的，建议后续对 stream path 做系统性审计。
- **WSL/远程场景支持不足**：WSL 下无法检测设备授权完成、RPC 与 compaction 并发丢消息（#7150, inprogress），"silent data loss" 对远程驱动用户是严重红线。
- **Compaction 交互设计待完善**：手动/自动双重触发、触发后不恢复、触发条件不可控，核心期望是加一个"压缩中"状态机，禁止并发 compaction 且保证恢复确定性。
- **401/重试分类器覆盖不全**：kimi-coding OAuth 过期不会自动刷新（#7319），重试分类器未覆盖 401，导致单点故障中断整个会话。
- **请求可追踪性**：缺少 `x-client-request-id`（#7161）和 `x-request-id` 一类的 header 使得网关调试和 session affinity 无法实现，对代理/网关用户至关重要。
- **会话搜索/索引语义不清晰**：`SessionSearch` 从可变索引重构为只读查询（#7391），可见团队在收敛公共 API 面，建议留意该变更对扩展兼容性的影响。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-01**


## 今日速览

昨日发布 v0.21.2 修复版本，Autofix 新增轮次限制与用户通知机制；社区最热议题聚焦于 `qwen serve` 守护进程的资源管理与多工作区支持（RFC #6378 持续发酵）；同时，多起针对 Anthropic 转换器、模型输出格式兼容性的 Bug 被集中修复和报告。


## 版本发布

### v0.21.2

- **Autofix 改进**：连续五轮修复后自动降级低严重性建议，并在因轮次上限拒绝继续时发布可见通知（[#7913](https://github.com/QwenLM/qwen-code/pull/7913)、[#8067](https://github.com/QwenLM/qwen-code/pull/8067)）。


## 社区热点 Issues

1. **多工作区守护进程 RFC 持续发酵**（[#6378](https://github.com/QwenLM/qwen-code/issues/6378)）
   由 doudouOUC 发起的 RFC，讨论 `qwen serve` 单守护进程支持多个工作区。已获 31 条评论，是目前社区讨论最热烈的话题。值得注意的是该问题已标记 CLOSED，但与其相关的系列追踪 Issue（如 #8051、#8091）仍在活跃推进。

2. **Serve 守护进程资源使用需有界**（[#8051](https://github.com/QwenLM/qwen-code/issues/8051)）
   doudouOUC 提出：当前守护进程仅按数量限制工作区和会话，未对请求体、WebSocket 组装等占用的字节数设限，存在内存失控风险。9 条评论，属 #6378 的落地追踪。

3. **ACP 子进程内存分配 50% 上限缺陷**（[#8182](https://github.com/QwenLM/qwen-code/issues/8182)）
   守护进程为每个 `qwen --acp` 子进程分配宿主机 50% 内存作为 V8 old-space 上限，且不随子进程数量均分。多子进程场景下极易触发 OOM，社区高度关注。

4. **Anthropic 4.6+ 助手消息预填充 400 错误**（[#8039](https://github.com/QwenLM/qwen-code/issues/8039)）
   影响所有 Claude Opus/Sonnet 4.6+ 及 5.x 系列模型。当 Gemini 格式历史以模型回合结束时，Anthropic 转换器出现预填充 400 错误且无缓解方案。标记 P1，已关闭（修复合入）。

5. **长会话中模型输出 XML 风格工具调用**（[#8003](https://github.com/QwenLM/qwen-code/issues/8003)）
   在 200+ 轮、180K+ token 的长会话中，`qwen3.8-max-preview` 偶尔在 `content` 字段输出原始 XML 标签（`<invoke>`/`<parameter>`），而非结构化的 `tool_calls` 数组。已关闭，但暴露了长上下文场景的稳定性问题。

6. **JSON 风格工具调用参数泄漏为纯文本**（[#8207](https://github.com/QwenLM/qwen-code/issues/8207)）
   生产 DataAgent 会话中（约 35K token、第 6 轮），模型预期输出结构化 `tool_call`，却将参数序列化为纯文本泄漏，破坏下游解析。社区关注模型格式漂移问题。

7. **Windows 平台 `@` 文件读取保护缺失**（[#8227](https://github.com/QwenLM/qwen-code/issues/8227)）
   继 #7206 的符号链接/TOCTOU 加固后，Windows 上 `O_NOFOLLOW` 不存在且 dev/ino 校验为空，保护被实质削弱且未测试。

8. **QQ 机器人频道 openid 截断**（[#8232](https://github.com/QwenLM/qwen-code/issues/8232)）
   `prepareGroupMessage()` 将发送者 openid 截断为首 8 字符加省略号，导致模型无法用 `<@OPENID>` 正确 @ 提及发送者，集成体验受损。

9. **SGR 鼠标转义序列泄漏到输入框**（[#8267](https://github.com/QwenLM/qwen-code/issues/8267)）
   v0.21.2 启动后终端输入框出现大量原始 SGR 鼠标转义序列，TUI 未消费而注入输入缓冲区，直接影响交互体验。

10. **守护进程资源保护拆分追踪**（[#8091](https://github.com/QwenLM/qwen-code/issues/8091)）
    doudouOUC 将 #8051 拆分为多个小 PR 逐一评审，用于追踪交付进度。社区对守护进程资源治理的系统性推进保持高度关注。


## 重要 PR 进展

1. **修复 CI 评审运行器 Qwen CLI 版本滞后**（[#8265](https://github.com/QwenLM/qwen-code/pull/8265)）
   评审任务在 qwen 0.20.0 上执行，导致评审格式过时。此 PR 让每次运行升级到 npm 最新版，保证评审格式与能力同步。

2. **内部守护进程密钥从 shell 子进程环境清理**（[#6606](https://github.com/QwenLM/qwen-code/pull/6606)）
   防止 daemon 内部密钥泄漏到 shell 子进程环境，属安全加固。已自报评审，挂起时间较长。

3. **Web Shell 自动回顾按会话隔离**（[#8262](https://github.com/QwenLM/qwen-code/pull/8262)）
   防止一个会话请求的自动回顾在用户切换会话后插入新会话的转录中，通过记录来源会话和生成序号来保证归属正确。

4. **Web Shell 工具授权选项去重**（[#8250](https://github.com/QwenLM/qwen-code/pull/8250)）
   在 `ToolApproval` 组件中增加 `deduplicateByLabel` 逻辑，合并解析到相同 i18n key 或原始标签的权限选项，修复重复按钮问题（对应 #8248）。

5. **serve 守护进程内存预算解析与上报**（[#8245](https://github.com/QwenLM/qwen-code/pull/8245)）
   为守护进程增加内存预算概念：读取 cgroup、堆大小限制等，使后续资源划分（#8051）有据可依。

6. **模型切换保持会话级作用域**（[#6579](https://github.com/QwenLM/qwen-code/pull/6579)）
   将普通 `/model` 切换仅作用于当前会话，持久化默认模型需显式使用 `/model --default`。避免全局修改造成的意外影响。

7. **交互式 TUI 接入 Goal v3 运行时**（[#8005](https://github.com/QwenLM/qwen-code/pull/8005)）
   新增 `/goal` 生命周期命令、持久化生命周期卡片和底部状态、Goal 感知的恢复与分支恢复，以及双通道输入队列。TUI 交互升级的核心 PR。

8. **Windows 粘贴文件支持**（[#7957](https://github.com/QwenLM/qwen-code/pull/7957)）
   从文件资源管理器复制的文件可通过现有剪贴板快捷方式和空终端粘贴路径在 Windows 上粘贴，纯图片选择转为附件，其余文件类型插入路径。

9. **Anthropic 转换器 tool_result 块去重**（[#8163](https://github.com/QwenLM/qwen-code/pull/8163)）
   修复多个相同 `tool_use_id` 的 `tool_result` 块导致 Anthropic HTTP 400 的问题（对应 #8160），确保各 `tool_use` 的 `tool_result` 唯一。

10. **/review 能力升级：Test Plan 检查、A/B 测试、按 hunk 探测**（[#8215](https://github.com/QwenLM/qwen-code/pull/8215)）
    从维护者手动验证流程中抽象出三种自动化验证能力，显著提升代码评审的保真度。


## 功能需求趋势

- **Serve 守护进程资源治理（最热）**：多工作区支持（#6378）衍生出资源上限、内存预算、进程隔离等系列需求（#8051、#8091、#8182、#8245）。社区对 daemon 的生产级稳定性诉求强烈。
- **Anthropic 转换器正确性集中修复**：多起 Bug 指向 Anthropic wire 格式的不一致——预填充 400、tool_use_id 字符集、tool_result 顺序、去重等问题（#8039、#8159、#8160、#8161、#8163）。核心是保证跨模型提供商的协议兼容性。
- **Autofix 流程透明度**：新增轮次限制和可见通知（v0.21.2），社区对自动修复的边界与反馈有明确需求。
- **CI 自动化机器人改进**：多个自动化维护的 Issue/PR（#7167、#8256、#8244、#8237 等）显示社区正系统性提升 CI 失败检测、归因与自动修复的智能化水平（Autofix/Takeover 机制持续迭代）。
- **会话级模型切换**：模型默认值作用域收窄至当前会话（#6579），满足多项目、多场景下的灵活性。


## 开发者关注点

- **守护进程内存安全**：ACP 子进程 50% 宿主机内存上限（#8182）引发担忧，多子进程场景下 OOM 风险高，开发者普遍认可需要更精细的资源划分。
- **终端体验回归**：v0.21.2 的 SGR 鼠标转义泄漏（#8267）属 TUI 回归，开发者期待 `ui.mouseTracking` 设置（#8198）能及时合入，同时恢复右键和 URL 点击功能。
- **长会话稳定性**：180K+ token 时模型输出格式漂移（#8003、#8207）、推理签名丢失（#8258）等问题被反复报告，长上下文场景的可靠性是当前最大的质量短板。
- **Windows 平台安全短板**：文件读取符号链接保护缺失（#8227）说明平台差异测试不足，跨平台安全性需加强。
- **集成通道可用性**：QQ 机器人 openid 截断（#8232）、子代理提问无人应答（#7835）等集成问题影响实际使用流程，社区希望尽快修复。
- **文件搜索性能**：忽略规则重复测试约 41 次/目录（#8252），大仓库下搜索性能问题受到关注。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-01

> 数据来源：[Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)（原 DeepSeek-TUI） | 日报生成时间：2026-08-01

---

## 1. 今日速览

CodeWhale 昨日正式发布 **v0.9.3 Release Candidate**（PR #4993），该版本新增 DeepSeek V4 Flash 直连响应支持，并明确了品牌从 `deepseek-tui` 向 `codewhale` 的迁移路径。与此同时，社区 24 小时内新增了超过 10 个高价值 issue 和 PR，主要集中在**工具调用可靠性**、**sandbox 文件系统边界**、**ACP 协议支持**和**OAuth 无头认证**等方向，显示了项目正在从单一 DeepSeek TUI 向通用 AI Agent 协议层的快速演进。

---

## 2. 版本发布

### 🚀 [v0.9.3 Release Candidate](https://github.com/Hmbown/CodeWhale/pull/4993) — 2026-07-31

v0.9.3 是建立在 `main` 分支之上的集成交付版本，由 72 个单一关注点提交组装而成，仅通过 fast-forward 方式推进。候选提交 SHA：`80c66ddd735387669b846e0af15ad35765c1c3b6`。

**核心更新内容（来自发行说明和 PR）：**

- **DeepSeek V4 Flash 直连支持** — 可直接调用 DeepSeek V4 Flash 模型的响应能力
- **品牌迁移确认** — 正式将 `codewhale` 作为产品名（Shannon Labs），npm 包与发行资产统一采用小写 `codewhale` 标识；旧的 `deepseek-tui` npm 包已被弃用且不再接收新版本
- **规范工具集（canonical tools）** — 对工具面进行了整合与精简
- **文档门禁修复** — 恢复 v0.9.3 的 rustdoc 门禁（PR #5004）

> 影响提示：从 v0.8.x 遗留的 `deepseek` / `d` 命令迁移用户需关注新的 `codewhale` 命令入口。

---

## 3. 社区热点 Issues（Top 10）

### 🔥 高讨论度

**#4949 [Discussion] "Constitution" 中文翻译讨论 — "宪法" vs "协作准则"**
作者：SparkofSpike | 更新：07-31 | 评论：5
链接：[Issue #4949](https://github.com/Hmbown/CodeWhale/issues/4949)

PR #4908 作者将 "Constitution" 的中文翻译从“协作准则”改回“宪法”，引发对翻译准确性和中文语境敏感性的争议。该讨论反映了项目在**中文用户社区影响力扩大**背景下，对意识形态与协作共识表达方式的本土化探索。需注意的是，该 Issue 被标记为 **CodeWhale** 而非 DeepSeek-TUI，推测项目已完成仓库层面的品牌切换。

---

### 🐛 用户反馈的 Bug

**#5003 [bug] 中长文本 File write 功能严重反复**
作者：DracheTek | 更新：07-31 | 评论：2
链接：[Issue #5003](https://github.com/Hmbown/CodeWhale/issues/5003)

针对包含中文注释、CRLF 行尾的约 700 行 C 文件进行大段代码替换时，`File` 编辑工具反复失败。模型在同一个文件上进行了 **15+ 次失败尝试、3 次 git checkout 全量回滚**，只能绕过工具改用外部 Python 脚本完成写入。该反馈直指大段代码替换场景下工具的**诊断信息不足**问题。PR #5008 已提交修复方案（见下文）。

**#5002 [bug] 工具调用时报错 "Failed to locate tool: Task"**
作者：zhizhuo0325 | 更新：07-31 | 评论：1
链接：[Issue #5002](https://github.com/Hmbown/CodeWhale/issues/5002)

用户报告在使用过程中出现工具无法定位的问题，伴随 Anthropic API HTTP 400 错误。这可能是工具目录在特定配置下的加载问题，需关注维护者的排查结论。

---

### 🚀 功能与可靠性增强建议

**#5005 [enhancement] Sandbox 支持文件系统路径白名单**
作者：WillHouMoe | 更新：07-31 | 评论：1
链接：[Issue #5005](https://github.com/Hmbown/CodeWhale/issues/5005)

用户使用 CodeWhale 构建 Xcode 项目时，`xcodebuild` 会在工作区外生成日志和构建产物（如 `~/Library/Developer/Xcode/DerivedData/`），而 sandbox（`sandbox_mode = "workspace-write"`）限制了对此类路径的访问。建议增加**路径白名单/允许列表**配置。对于需要在沙箱内调试原生项目的用户而言，此需求相当刚性。

**#5000 [Engine] 将中断的助手输出持久化为了一级会话项**
作者：cacdcaecawae | 更新：07-31 | 评论：1
链接：[Issue #5000](https://github.com/Hmbown/CodeWhale/issues/5000)

当回合在 `MessageComplete` 前被中断时，用户已看到的助手文本在 TUI 中保留，但**权威会话中缺失**，导致下一次模型调用无法感知已输出的内容。这是一个引擎层面的**会话完整性**问题，对长会话或多步任务的可靠性影响较大。

---

### 🏗️ 架构优化提案

**#5007 [讨论] YouTuber 使用 Codex 而非 CodeWhale 作为 TUI**
作者：aboimpinto | 更新：07-31 | 评论：4
链接：[Issue #5007](https://github.com/Hmbown/CodeWhale/issues/5007)

社区成员注意到有影响力的 YouTuber 在测试 DeepSeek-v4-flash 时选择了 Codex 而非 CodeWhale。作者借此呼吁社区明确 CodeWhale 的定位：并非 DeepSeek 官方 TUI，而是通用的 CodeWhale 客户端。该讨论对项目**品牌认知与市场推广**具有参考价值。

**#4999 [enhancement, reliability] Benchmark/评估框架的确定性、故障闭合与溯源准确性**
作者：Hmbown | 更新：07-31 | 评论：0
链接：[Issue #4999](https://github.com/Hmbown/CodeWhale/issues/4999)

CodeWhale 的 benchmark/评估框架作为产品门禁，其当前实现混合了 ad hoc fixtures、未版本化的 trace 格式以及不完整的生命周期/取消语义。作者建议评估结果应**确定性、故障闭合（fail closed）且可精确追溯来源**。

---

### 🔐 认证与安全

**#4998 [enhancement] 无头环境 OAuth 完成 — 通用 PKCE 方案 + 手动回退**
作者：Hmbown | 更新：07-31 | 评论：0
链接：[Issue #4998](https://github.com/Hmbown/CodeWhale/issues/4998)

无头服务器、SSH 和容器环境无法完成浏览器 OAuth 流程。提议实现**提供商无关的无头认证路径**：优先尝试 loopback 重定向，在无浏览器环境下支持手动重定向 URL / 裸代码粘贴回退。

---

## 4. 重要 PR 进展（Top 10）

### 🎯 功能修复

**[#5008 fix(tui): File 编辑操作提供可操作诊断信息 + 容忍过期行号](https://github.com/Hmbown/CodeWhale/pull/5008)**
作者：SparkofSpike | 更新：07-31

修复 #5003。针对大段替换（100+ 行）反复失败的问题，改进 `File` 工具的**诊断信息质量**，并容忍旧行号偏移，减少模型无效重试。

**[#4977 fix(tui): 让 AltGr 输入的 "/" 直达输入框而非触发帮助](https://github.com/Hmbown/CodeWhale/pull/4977)**
作者：yyyCode | 更新：07-31 | 已合并

修复 #4723。在 Windows 系统中，AltGr 被报告为 `Ctrl+Alt`，巴西 ABNT2 键盘布局中 `/` 为 `AltGr+Q`，此前会误触全局 `Ctrl-/` 帮助快捷键，导致用户每次输入斜杠时帮助面板弹出。

**[#5001 fix(tui): 圈号数字与键帽符号按双列宽度测量](https://github.com/Hmbown/CodeWhale/pull/5001)**
作者：SparkofSpike | 更新：07-31

修复 TUI 渲染缺失字符/幻影空格的问题。封闭字母数字符号（① ② Ⓐ）、Dingbat 圈号数字（❶ ❷）和键帽序列（1️⃣）在 CJK 终端中被测量为 1 列但实际渲染为 2 列，导致显示错位。

**[#5006 fix(installer): 保留 Windows 用户长 PATH 值](https://github.com/Hmbown/CodeWhale/pull/5006)**
作者：XhesicaFrost | 更新：07-31

修复 Windows NSIS 安装程序覆盖用户现有长 PATH 的问题。NSIS `ReadRegStr` 在注册表数据超过固定缓冲区时返回空值，导致安装程序误判 PATH 不存在，仅写入 CodeWhale 的 bin 目录。

---

### 📦 依赖与工具链

**[#5016 chore(deps): libc 0.2.186 → 0.2.189](https://github.com/Hmbown/CodeWhale/pull/5016)**
作者：dependabot[bot] | 更新：07-31

**[#5015 chore(deps): futures-util 0.3.32 → 0.3.33](https://github.com/Hmbown/CodeWhale/pull/5015)**
作者：dependabot[bot] | 更新：07-31

**[#5013 chore(deps): ratatui 0.30.0 → 0.30.2](https://github.com/Hmbown/CodeWhale/pull/5013)**
作者：dependabot[bot] | 更新：07-31

TUI 核心框架 ratatui 的维护性更新。

**[#5010 chore(deps): actions/stale 10.4.0 → 11.0.0](https://github.com/Hmbown/CodeWhale/pull/5010)**
作者：dependabot[bot] | 更新：07-31

CI 中 stale bot 的主版本升级。

**[#5011 chore(deps): globset 0.4.18 → 0.4.19](https://github.com/Hmbown/CodeWhale/pull/5011)**
作者：dependabot[bot] | 更新：07-31

**[#5012 chore(deps): docker/login-action 4.4.0 → 4.5.2](https://github.com/Hmbown/CodeWhale/pull/5012)**
作者：dependabot[bot] | 更新：07-31

---

### 🏷️ 版本与文档

**[#4993 Release v0.9.3: DeepSeek V4 Flash Responses and canonical tools](https://github.com/Hmbown/CodeWhale/pull/4993)**
作者：Hmbown | 更新：07-31 | 已关闭（已合并）

v0.9.3 集成与发布火车，包含 DeepSeek V4 Flash 直连支持和规范化工具集。

**[#5004 fix(docs): 恢复 v0.9.3 rustdoc 门禁](https://github.com/Hmbown/CodeWhale/pull/5004)**
作者：Hmbown | 更新：07-31 | 已关闭

修复文档构建问题，恢复 CI 中的文档门禁检查。

---

## 5. 功能需求趋势

从近 24 小时新增及活跃的 Issues 中，可以提炼出以下社区最关注的功能方向：

### 🔌 Agent 协议互操作性（ACP/MCP） — **上升趋势明显**
- **#4996** 提议构建协议无关的 ACP 客户端（bounded stdio JSON-RPC + 能力协商），让外部 Agent/编辑器能够驱动 CodeWhale 会话
- **#4997** 提出将 GitHub Copilot agent mode 作为**命名外部 ACP worker 后端**（而非 ProviderKind），运行时动态协商模型列表
- 关联需求：#2535（ACP+MCP 支持）

### 🛡️ Sandbox 可配置性与安全性
- **#5005** 需要文件系统路径白名单，以便访问 `~/Library/.../DerivedData` 等外部构建产物
- **#4994** 需要显式的提供商凭据传递机制（`auth print-api-key` 固定解析），避免多提供商同时存在时解析错凭据

### 🔐 无头环境认证与凭据管理
- **#4998** 无头/SSH/容器环境的 OAuth 完成路径（PKCE + 手动回退）
- **#4994** 凭据交接时区分 OAuth token 与原始 API key，防止误打印/误用

### ⚙️ 评估与可观测性
- **#4999** Benchmark 评估框架需要确定性、故障闭合、可追溯

### 🧭 会话持久化语义
- **#5000** 中断的助手输出应持久化为一级会话对象，确保跨回合上下文完整
- **#4995** 语义化 TUI 图形持久性 — 环境/海洋视觉状态需持久化意图（如恢复后保留水母位置、用户固定项）

---

## 6. 开发者关注点

### 🐛 核心痛点

1. **大型代码编辑的工具可靠性**（#5003）：模型在替换大段代码时失败率高，缺少可操作的诊断信息。虽然 #5008 已提交修复，但社区的耐心有限，**15+ 次失败重试 + 3 次全量回滚**的体验不可接受。
2. **行号漂移问题**（#5008 关联）：模型在用旧行号定位时反复失败，需容忍过期行号。
3. **Windows 平台输入法映射**（#4977，已修复）：AltGr 与 Ctrl 键冲突导致斜杠输入困难，已有用户提交修复并被合并，显示社区对国际化输入的支持需求。

### 📋 共性需求

- **沙箱边界可配置**：构建/调试场景需要访问工作区之外的产物，硬编码 sandbox 策略限制了 CodeWhale 在本地开发工作流中的实用性。
- **会话中断的连贯性**：`Ctrl-C` 中断输出后，会话记录缺失已呈现文本，下一次请求无法感知已输出内容，影响多轮任务的连贯性。
- **第三方工具集成**：YouTuber 事件（#5007）揭示了 CodeWhale 在 AI 开发者社区中的影响力提升，同时也凸显了与 Codex 等竞品在工具链生态上的差距。

### 📈 社区活跃度观察

- 新 Issue 中混入了多个**无关推广内容**（如 #5009 眼科计费服务广告），表明仓库关注度提升的同时也需加强 Issue 垃圾信息治理。
- 项目中中文 Issue 占比上升（#4949、#5002、#5003），中文用户社区使用活跃，但工具对中文/CRLF 文件的处理仍有瑕疵。
- 大量 dependabot 依赖更新 PR 进入队列，说明项目依赖在持续维护中，但需留意合并节奏以避免 CI 噪声。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*