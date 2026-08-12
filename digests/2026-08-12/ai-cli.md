# AI CLI 工具社区动态日报 2026-08-12

> 生成时间: 2026-08-12 00:52 UTC | 覆盖工具: 9 个

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

**报告日期**：2026-08-12  
**数据来源**：GitHub 社区动态（过去 24 小时）  
**覆盖工具**：Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI


## 一、生态全景

AI CLI 工具已从"演示级玩具"全面进入"生产级基础设施"阶段，各主流工具均保持**周级甚至日级**的发布节奏（今日 8 个工具合计发布 8+ 版本）。社区反馈重心从功能新奇感转向**稳定性、成本透明度和可预测性**——三个工具出现计费争议（Claude Code 累计涉额超 2,600 美元），四个工具报告成本失控类 Issue。多代理协作（Subagent）成为标配但可靠性问题集中爆发，配置管理、跨平台兼容性和长会话可靠性是普遍痛点。市场呈现"头部厂商（Anthropic/OpenAI/Google/GitHub）+ 新兴挑战者（Qwen/Kimi/OpenCode/Pi）+ 细分工具（DeepSeek TUI）"的三层竞争格局。


## 二、各工具活跃度对比

> 注：Issue/PR 数为过去 24 小时有更新的数量（含新建与更新），非新增数；Release 为当日发布的版本数。

| 工具 | Issues（更新数） | PRs（更新数） | Releases | 当前版本 | 版本节奏（近 30 天参考） |
|---|---|---|---|---|---|
| Claude Code | 10（Top10 精选） | 7（Top10 精选） | 1（v2.1.228） | v2.1.228 | 高（周更） |
| OpenAI Codex | 10（Top10 精选） | 10（Top10 精选） | 2（alpha.7/8） | v0.148.0-alpha.8 | 极高（日更 alpha） |
| Gemini CLI | 10（Top10 精选） | 10（Top10 精选） | 2（v0.55.1 + preview.1） | v0.55.1（稳定） | 高（周更） |
| GitHub Copilot CLI | 10（Top10 精选） | 2 | 0 | v1.0.79 | 中（周更） |
| Kimi Code CLI | 5 | 8 | 0 | v0.34.0 | 中（周更） |
| OpenCode | 10（Top10 精选） | 10（Top10 精选） | 0 | v1.18.16 / V2（next） | 高（双轨迭代） |
| Pi | 12（Top10+2 补充） | 10 | 0 | v0.84.1 | 高（周更） |
| Qwen Code | 10（Top10 精选） | 10（Top10 精选） | 1（v0.21.10） | v0.21.10 | 高（周更） |
| DeepSeek TUI | 3 | 7 | 0 | v0.9.x | 中（周更） |

**注释**：
- **发布最频繁**：OpenAI Codex（双日 alpha）、Claude Code/Gemini CLI（周级稳定版）
- **社区反馈最活跃**：Claude Code（#45596 达 1167 👍）、OpenAI Codex（#11023 达 950 👍）、OpenCode（#8501 达 230 👍）
- **双轨迭代**：OpenCode（V1 稳定 + V2 迁移）和 Gemini CLI（stable + preview + nightly）采用双通道策略


## 三、共同关注的功能方向

### 1. 成本控制与透明计费（最紧迫 🔥）
| 工具 | 代表 Issue | 核心诉求 |
|---|---|---|
| Claude Code | #81703（$604.71 错误扣费）、#85912（$1,031.92 静默消耗）、#67636（并行 Agent 烧 Token） | 硬性消费上限、实时用量告警、异常任务熔断 |
| Pi | #7911（wire 协议丢失 usage 字段） | 流式事件中的用量数据可观测性 |
| OpenAI Codex | #38059（Windows 内存 8.8GB 暴涨） | 资源占用异常时的告警 |
| Qwen Code | #8182（每子进程独占宿主 50% 内存） | 内存配额按子进程数划分 |

**共性结论**：用户不再接受"事后对账"，要求**事前预警 + 事中熔断 + 事后审计**的完整成本治理链路。

### 2. 多代理/Subagent 可靠性
| 工具 | 代表 Issue | 问题类型 |
|---|---|---|
| Gemini CLI | #21409（generalist 挂起 1h）、#22323（MAX_TURNS 后误报成功） | 挂起与状态误报 |
| Claude Code | #67636（自动生成 10-15 个并行 Agent） | 调度失控 |
| OpenAI Codex | #23930（子代理卡片残留）、#36404（语音委托后处理器丢失） | UI 状态同步与委托链路 |
| Pi | #7897（Subagent 继承错误会话配置） | 配置继承错乱 |
| DeepSeek TUI | #5253（嵌套 max_depth 越权） | 递归预算绕过（已修复） |
| Qwen Code | #8839（子代理转录落盘） | 可观测性缺失 |

**共性结论**：Subagent 的**生命周期管理、上下文隔离、状态报告真实性**是跨工具的技术债。

### 3. 长会话稳定性与性能
| 工具 | 代表 Issue | 表现 |
|---|---|---|
| Claude Code | #85603（输入队列静默丢失）、v2.1.228 TUI 重绘卡死 | TUI 交互可靠性 |
| OpenAI Codex | #37421（Esc-Esc 回溯回归） | 高频交互回归 |
| Pi | #7730（长会话 CPU 100%+）、#7947（CMD 重复输出/泄漏） | 性能退化与严重 Bug |
| Copilot CLI | #4251（大会话恢复 OOM，1.0.74 回归） | 内存暴涨 3-4 倍 |
| Gemini CLI | #25166（Shell 执行后卡 Waiting input） | 流程阻塞 |

**共性结论**：会话长度增长带来的**性能非线性退化**是普遍技术挑战，回归测试需覆盖长会话场景。

### 4. Windows 平台体验追赶
| 工具 | 代表 Issue | 问题 |
|---|---|---|
| Claude Code | #14828（控制台闪烁）、v2.1.228 Git 路径修复 | 交互体验与路径处理 |
| OpenAI Codex | #38059（8.8GB 内存）、#37471（MCP 未暴露） | 资源与生态缺口 |
| Copilot CLI | #4095（插件安装文件句柄被占） | 插件生态不可用 |
| Kimi Code CLI | #2600（PowerShell 7 默认 D 盘路径 bug） | 路径兼容 |
| OpenCode | #37090（apply_patch 行尾错乱） | 文件处理行为 |
| Qwen Code | #8644（盘符冒号 URL 编码）、#8929（`\\?\` 前缀崩溃） | 路径多重问题 |
| Pi | #7947（CMD 重复输出/内存泄漏） | 严重稳定性 |

**共性结论**：Windows 是各工具**共同的技术短板**，问题覆盖路径处理、文件句柄、终端渲染、内存管理全链路。对比之下，macOS/Linux 的同类问题报告显著少于 Windows。

### 5. 功能移除与变更透明度
| 工具 | 代表 Issue | 诉求 |
|---|---|---|
| Claude Code | #45596（Bring Back Buddy，1167 👍） | 功能移除前社区讨论、提供 legacy 开关 |
| DeepSeek TUI | #5322（宽屏输出回归） | 变更不应破坏已有行为 |
| OpenAI Codex | #37403（Remote Control 回归） | 回归应在上线前被发现 |

**共性结论**：开发者对"**静默移除功能**"和"**无提示的行为变更**"零容忍。"Buddy 请愿"已成为行业标志性事件。


## 四、差异化定位分析

| 工具 | 定位 | 目标用户 | 技术路线 | 差异化优势 |
|---|---|---|---|---|
| **Claude Code** | 全功能专业级 Agent | 专业开发者、企业团队 | TUI + 插件 + MCP + Hooks | 生态最丰富（社区声量最大）、模型能力强、TUI 体验成熟 |
| **OpenAI Codex** | 深度集成 OpenAI 生态的 Agent | OpenAI API 用户、桌面端重度用户 | Rust 重写 + 桌面应用 + Remote Control | 桌面端体验、Remote 工作流、alpha 高频迭代 |
| **Gemini CLI** | Google 生态开发助手 | GCP 用户、Android 开发者 | Node.js + MCP + IDE 集成 | Google 生态整合（Cloud Workstations）、OAuth 完善 |
| **Copilot CLI** | GitHub 生态的 Copilot 扩展 | GitHub 用户、企业 Copilot 客户 | Node.js + 技能系统 + 橡皮鸭审查 | GitHub 深度绑定、企业管理、橡皮鸭双重审查 |
| **Kimi Code CLI** | 轻量国产 CLI | 中文开发者、Kimi 用户 | Python + ACP 协议 | 中文支持好、轻量起步、记忆系统呼声高 |
| **Qwen Code** | 阿里云/Daemon 架构 Agent | 阿里云用户、Web Shell 偏好者 | 本地 Daemon + Web Shell + ACP | Web Shell 体验（Git/图片预览）、DWS 渠道、模型家族丰富 |
| **OpenCode** | 开源社区驱动的多提供商 Agent | 开源爱好者、多模型用户 | TypeScript monorepo + Zen 提供商 | V2 架构积极重构、模型无关性强、社区 PR 活跃 |
| **Pi** | 高性能现代化 TUI | 终端极客、性能敏感用户 | 全栈 TypeScript + JSON/RPC + 供应商矩阵 | 启动延迟对标 jcode、Mermaid 渲染、MCP 全面接入 |
| **DeepSeek TUI** | 轻量编程代理核心 | 寻求"非大厂"替代的用户、Rust 偏好者 | Rust + Ratatui + ACP | 画中画模式、ACP 工具全暴露、黑客松式社区 PR |

**关键差异维度**：
- **生态绑定度**：Copilot CLI（GitHub）> Codex（OpenAI）> Gemini CLI（Google）> Qwen Code（阿里云）> 其余（模型无关）
- **架构路线**：Pi/Qwen/Codex 走向"后台服务 + 多前端"；Claude Code/Gemini 保持单体 TUI；DeepSeek TUI 拥抱 ACP 标准
- **目标场景**：Codex/Qwen/Pi 强调跨端（桌面/移动/Web）协作；Claude Code/Gemini 聚焦终端深度工作流；Copilot CLI 服务企业合规场景


## 五、社区热度与成熟度

### 按社区活跃度排序

| 梯队 | 工具 | 活跃度特征 | 用户规模预估（基于 👍 数） |
|---|---|---|---|
| **第一梯队（最活跃）** | Claude Code | 声量最大：#45596 达 1167 👍，25+ 条评论；Issue 讨论质量高；计费争议引发信任讨论 | 数万级活跃用户 |
| **第一梯队** | OpenAI Codex | 950 👍 的 Linux 需求；双日级 alpha 发布；社区期待高但 Windows 问题分散声量 | 数万级 |
| **第二梯队（快速上升）** | Gemini CLI | 每日 10+ Issue/PR 更新；Subagent 可靠性讨论集中；CVE 修复响应快 | 数千至万级 |
| **第二梯队** | OpenCode | 230 👍 的展开粘贴文本需求；V2 迁移引发系统性讨论；社区贡献 PR 活跃 | 数千级 |
| **第二梯队** | Qwen Code | 每日 10+ 更新；Daemon/Web Shell 话题密集；当日修复关闭（#8929）展现高效 | 数千级 |
| **第三梯队（成长中）** | Copilot CLI | Issue 有质量（如橡皮鸭审查缺陷）但 👍 数偏低；Windows 插件问题为最大痛点 | 数千级（企业内可能更高） |
| **第三梯队** | Pi | 12 条 Issue + 10 条 PR 当日更新，社区小而精；性能基准讨论有价值 | 千级 |
| **第三梯队** | Kimi Code CLI | 记忆系统呼应力强但整体 Issue 量偏少；PR 活跃（hobostay 连续贡献） | 数百至千级（中文社区为主） |
| **第三梯队** | DeepSeek TUI | 社区最小（3 Issue + 7 PR）；以黑客松式小众贡献者为主 | 数百级 |

### 成熟度判断

- **成熟稳定**：Claude Code（v2.1.228）、Gemini CLI（v0.55.1）——版本节奏稳定、Issue 类型以回归和体验微调为主
- **快速迭代**：OpenAI Codex（日更 alpha）、OpenCode（V2 重构期）、Pi（周更 + 架构活跃）
- **平台追赶期**：Copilot CLI（v1.0.79 回归集中）、Qwen Code（Windows 问题密集但修复快）
- **早期成长**：Kimi Code CLI、DeepSeek TUI——功能短板明显但方向明确


## 六、值得关注的趋势信号

### 1. "功能移除需要用户同意"成为行业共识
Claude Code 的 Buddy 请愿（#45596）以 1167 👍 成为历史级 Issue。产品团队应建立 **RFC 机制**——功能移除提前 2-4 周预告，提供临时开关。这个信号对所有 AI CLI 工具都有效。

### 2. 成本护栏从"可选"变为"必需"
四个工具的成本争议事件（Claude Code $2,600+、Pi usage 丢失）表明：**AI CLI 需要像云服务一样提供预算控制**。内置功能应包括：会话级消费上限、实时 Token 告警、异常任务熔断、用量 API 开放。

### 3. Windows 是下一个战场
8 个工具中 7 个在 Windows 上有显著问题。随着 Win11 + WSL2 普及，Windows 开发者基数巨大。**率先解决 Windows 平台体验（路径、终端、文件句柄）的工具将获得显著竞争优势**。

### 4. Subagent 需要"看得见的自主性"
跨工具的用户诉求高度一致：Subagent 不应只报告"成功/失败"，还需呈现**轨迹、成本、耗时、上下文使用率**。Gemini CLI 的 EPIC #24353（组件级评估）和 Qwen Code 的 #8839（子代理转录落盘）是正确方向，预计会成为行业标配。

### 5. ACP（Agent Client Protocol）正在成为互操作标准
DeepSeek TUI 暴露完整文件/Git/Shell 工具、Qwen Code 的 ACP 推理控制、Copilot CLI 的 MCP OAuth 修复——**ACP 作为跨编辑器/CLI 的协议层正在形成共识**。第三方工具链（如 Zed 集成）将因 ACP 成熟而受益，建议新工具优先实现 ACP 而非自研协议。

### 6. 双轨发布（Stable + Preview/Nightly）成为最佳实践
Gemini CLI（stable/preview/nightly）、OpenCode（V1/V2）、OpenAI Codex（alpha 高频）的实践证明：**双轨可同时满足稳定性敏感用户和尝鲜用户**。单轨发布容易导致回归集中爆发（如 Copilot CLI v1.0.79）。

### 7. 安全供应链意识觉醒
Gemini CLI 同日提交两个 CRITICAL CVE 修复（shell-quote/simple-git）、Copilot CLI 的 adm-zip 漏洞、PR #4449 从 pull_request_target 迁移——**AI CLI 的依赖治理应纳入 CI 强制扫描**，社区对此类修复反馈积极。

### 8. "轻量替代者"正在从边缘走向主流
Pi（对标 jcode 的启动性能）、Kimi Code CLI、DeepSeek TUI 等轻量工具的活跃证明：不是所有用户都需要重量级平台。**低资源占用、快速启动、简洁交互**是差异化切入口，值得大厂关注。

---

**编辑注**：本报告基于各工具 GitHub 社区公开发布的 Issue/PR/Release 数据整理，数据窗口为 2026-08-11 至 2026-08-12。部分数字为精选 Top 10 数据而非全量，实际活跃度可能更高。建议结合各仓库实时状态进行决策参考。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止：2026-08-12 | 来源：github.com/anthropics/skills**


## 一、热门 Skills 排行（按关注度）

### 1. skill-creator 修复系列（run_eval.py 全面修复）⭐ 最热
- **PR #1298**（open，评论最多）：修复 `run_eval.py` 恒报 0% recall 的核心问题——eval artifact 未作为真实 skill 安装、Windows 流读取失败、触发检测失效、并行 worker 异常。
- **PR #1099**（open）：修复 Windows 上 `subprocess` 管道读取崩溃，导致所有查询判定为"未触发"。
- **PR #1050**（open）：修复 Windows 下 `claude.cmd` 无法被 `subprocess.Popen` 调用（`PATHEXT` 不生效），及编码问题。
- **PR #1323**（open）：触发检测无法识别真实 skill 名称，在首个非 Skill 工具处提前中止。
- **关联 Issue #556**（12 评论，👍7）：`claude -p` 模式下所有查询 0% 触发率——**这是社区最关注的核心 bug**。
- **状态**：全部 open，多个独立修复路径并行，官方尚未合并任何一条。

### 2. document-typography — 文档排版质量管控
- **PR #514**（open）：检测 AI 生成文档的典型排版缺陷——孤行文字（1-6 词溢出到下一行）、孤寡段落（标题滞留页底）、编号错位。
- **社区讨论点**：这类问题影响每一份 Claude 生成的文档，用户很少主动要求"好排版"，但劣质排版显著降低专业感。
- **状态**：open，自 3 月创建至今无官方介入。

### 3. skill-quality-analyzer + skill-security-analyzer — 元技能双件套
- **PR #83**（open，2025-11 创建，持续活跃至 2026-01）：两个元技能——
  - **质量分析器**：五维评估（结构与文档 20%、示例质量、资源完整性等）；
  - **安全分析器**：面向社区 skill 的安全审计。
- **社区讨论点**：与 Issue #492（命名空间信任滥用，43 评论，最高）形成呼应——社区自发的安全治理方案。
- **状态**：open，已活跃 8 个月+。

### 4. self-audit — 交付前推理质量门禁（v1.3.0）
- **PR #1367**（open）：两步审计——①机械层：逐一验证所有声称的输出文件真实存在；②推理层：按损害严重度排序，四维审计（正确性、一致性、完整性、安全性）。
- **配套 Issue #1385**（4 评论）：提出三闸门流水线（任务前校准 → 对抗性评审 → 交付验证）。
- **状态**：open，作者持续迭代版本。

### 5. color-expert — 色彩专业知识库
- **PR #1302**（open）：自包含的色彩专家技能——覆盖 ISCC-NBS、Munsell、XKCD、RAL、Ridgway 1912、CSS 命名系统；色彩空间选择表（OKLCH 用于色阶、OKLAB 用于渐变、CAM16 用于感知均匀性）。
- **状态**：open。

### 6. testing-patterns — 全栈测试模式
- **PR #723**（open）：完整测试技能栈——测试哲学（Testing Trophy 模型）、单元测试（AAA 模式、纯函数、边界用例）、React 组件测试（Testing Library）、端到端测试。
- **状态**：open。

### 7. ODT + pyxel — 垂直领域技能
- **PR #486**（open）：OpenDocument 格式（.odt/.ods）创建、填充、解析、转 HTML。
- **PR #525**（open）：pyxel-mcp 驱动的复古/像素/8-bit 游戏开发工作流（write → run_and_capture → inspect → iterate）。
- **状态**：均 open。


## 二、社区需求趋势（来自 Issues）

### 1. 🔴 安全与信任边界（最强烈诉求）
- **Issue #492**（43 评论，最高）：社区技能在 `anthropic/` 命名空间下分发，造成信任边界滥用——用户可能对"看似官方"的技能授予过高权限。**这是当前社区最集中的安全焦虑。**

### 2. 🔴 工具链可靠性（skill-creator 是重灾区）
- **Issue #556**（12 评论，👍7）+ **Issue #1169**（3 评论，👍1）：`run_eval.py` / `run_loop.py` 描述优化循环完全失效（0% recall）——社区投入大量 PR 修复，官方未响应。

### 3. 🟡 组织级协作与共享
- **Issue #228**（16 评论，👍8）：技能应在组织内直接共享——当前需下载 .skill 文件 + Slack 传输 + 手动上传，体验割裂。社区期望共享技能库或分享链接。

### 4. 🟡 元技能与质量治理
- **Issue #202**（8 评论）：skill-creator 本身违反最佳实践——读起来像开发者文档而非可操作的指令，教育式语气损害 token 效率。
- **Issue #412**（6 评论）：agent-governance 提案——策略执行、威胁检测、信任评分、审计追踪。
- **Issue #1329**（9 评论）：compact-memory 技能——符号化表示法压缩长时运行 agent 的持久状态。

### 5. 🔵 上下文窗口效率
- **Issue #1487**（4 评论）：`claude-api` 技能单次工具调用即注入 ~156k tokens，直接撑爆上下文窗口。

### 6. 🔵 互操作性与扩展
- **Issue #16**（4 评论）：将 Skills 暴露为 MCP 协议——`algorithmic-art` 变成 `generateAlgorithmArt({...})`，统一 AI 软件封装协议。
- **Issue #29**（4 评论）：AWS Bedrock 兼容性。


## 三、高潜力待合并 Skills（近期可能落地）

> 判定依据：评论活跃度高、问题严重度明确、有多个独立修复路径收敛。

| PR | 内容 | 潜力分析 |
|---|---|---|
| **#1298 / #1099 / #1050 / #1323** | skill-creator 全套修复（Windows 兼容 + 触发检测 + eval 可靠性） | ⭐⭐⭐ 4 个 PR 指向同一组 bug，Issue #556 已获 👍7，官方不合并将持续消耗社区贡献 |
| **#541** | DOCX tracked change `w:id` 与书签冲突修复 | ⭐⭐⭐ 文档损坏级 bug，OOXML 规范层面，修复价值明确 |
| **#539** | skill-creator YAML 未引号 description 校验 | ⭐⭐ 静默失败问题，修复简单（pre-parse 验证），合并门槛低 |
| **#538** | PDF 技能大小写敏感文件引用修复 | ⭐⭐ 8 处大小写错误，纯修复，几乎零风险 |
| **#83** | 质量分析器 + 安全分析器双元技能 | ⭐⭐ 回应社区安全诉求（#492），若官方愿意接受元技能则价值大 |
| **#1367** | self-audit 推理质量门禁 v1.3.0 | ⭐ 有配套 Issue #1385 生态，但需官方认可"审计类"技能定位 |


## 四、Skills 生态洞察

**一句话总结**：当前社区在 Skills 层面的最集中诉求是——**"官方工具链不可信、不可用、不安全"三座大山**：skill-creator 的 eval 循环失效（不可用）、`anthropic/` 命名空间被社区技能滥用（不安全）、以及缺乏组织级共享与治理机制（不可信），其中 **skill-creator 的自动评估可靠性是压倒性的首要痛点**，其次是对官方安全治理和元技能（质量/安全审计）落地的急切期待。

---

# Claude Code 社区动态日报 — 2026-08-12

> 数据来源: github.com/anthropics/claude-code

---

## 一、今日速览

今日社区动态围绕三大焦点：**v2.1.228 发布**，修复了 TUI 重绘卡死与 Windows 下 Git 检测问题；**#45596 “Bring Back Buddy” 请愿持续发酵**，已获 1167 个 👍 与 265 条评论，成为社区最强声量议题；此外，多起**计费争议**（累计涉额超 2600 美元）与 **TUI 输入丢失**问题引发集中讨论，Anthropic 在成本管控与交互稳定性上面临信任挑战。

---

## 二、版本发布

### v2.1.228
- **修复**：罕见的内部布局错误导致交互式会话停止重绘（但进程仍在运行）的问题
- **修复**：在 Windows 上从 Git 安装目录的父文件夹启动 Claude Code 时，无法找到 `git` / Git Bash 的问题
- **修复**：`/tui` 回退相关的问题

📎 [Release 详情](https://github.com/anthropics/claude-code/releases)

---

## 三、社区热点 Issues（Top 10）

### 1. 🔥 Bring Back Buddy — 社区集体请愿
- **#45596** | 👍 1167 | 💬 265 | 状态: OPEN
- 4 月 9 日 `/buddy` 从 v2.1.97 中被静默移除，无变更日志、无告别。成千上万开发者在终端里看到 `Unknown skill: buddy`。这是社区对**功能移除不透明**的最强烈抗议，已成为 Claude Code 历史上声量最大的 Issue 之一。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/45596)

### 2. 功能请求：消息队列模式
- **#50246** | 👍 191 | 💬 53 | 状态: OPEN
- 当前任务执行中无法排队发送后续消息，只能中断当前工作。社区希望新增**消息队列模式**，在不打断 Agent 的情况下累积并顺序处理新指令。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/50246)

### 3. Gmail MCP 多账号支持
- **#36024** | 👍 77 | 💬 25 | 状态: OPEN
- 当前 Gmail MCP 集成仅支持单个账号连接。大量用户拥有个人+工作多个账号，此限制严重影响实际工作流。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/36024)

### 4. Windows: 工具执行时控制台窗口闪烁
- **#14828** | 👍 36 | 💬 60 | 状态: OPEN
- 长时间存在的 Windows 体验问题，每次工具调用都会闪现控制台窗口，影响开发沉浸感，社区持续关注。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/14828)

### 5. TUI 回归: 鼠标点击触发意外权限提示
- **#71539** | 👍 22 | 💬 10 | 状态: OPEN
- Linux 下点击终端恢复焦点会意外触发权限请求，打断工作流，是 TUI 交互细节的典型回归。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/71539)

### 6. 桌面端回归: 会话时间筛选仅在特定分组下可见
- **#78775** | 👍 28 | 💬 8 | 状态: OPEN
- 会话时间范围筛选器仅在 "Group by = State" 时出现，属于桌面端 UI 回归，影响跨平台用户。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/78775)

### 7. 计费事故: 用量扣费 + 自动充值争议
- **#81703** | 💬 12 | 状态: OPEN
- 7 月 17 日大规模计费事故：订阅额度内用量被错误路由到付费额度，并触发 $604.71 自动充值。用户要求对账与退款，涉及信任核心问题。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/81703)

### 8. 并行 Agent 引发 Token 耗尽
- **#67636** | 💬 6 | 状态: OPEN
- Claude 自动生成 10-15 个并行 Agent 执行简单任务（本可由 1-2 个完成），导致数百万 Token 消耗后崩溃。**成本失控**与 Agent 调度策略亟待优化。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/67636)

### 9. 输入队列丢失: 回合结束时静默丢弃
- **#85603** | 💬 20 | 状态: OPEN
- 新报告（8 月 10 日创建）快速升温。TUI 模式下，回合运行中键入的文本在回合结束时被静默丢弃，长会话用户受影响严重。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/85603)

### 10. 挂起的 Cowork 任务消耗 $1,031.92
- **#85912** | 💬 2 | 状态: OPEN
- 挂起的计划任务在 48 小时内消耗全额 Fable 额度和 $1,031.92，无任何告警或消费上限。成本透明性与防护机制缺失。
- 📎 [链接](https://github.com/anthropics/claude-code/issues/85912)

---

## 四、重要 PR 进展（Top 10）

### 1. 修复 /clean_gone 分支检测失效
- **#70173** | 状态: CLOSED（已合并）
- `git branch -v` + `grep '[gone]'` 的方式检测已删除分支，但由于 `git branch -v` 不显示 `[gone]` 标记，该命令从未真正删除任何内容。修正为使用 `git branch -vv`。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/70173)

### 2. hookify 插件: 从祖先目录加载规则，防止静默绕过
- **#85716** | 状态: OPEN
- 修复安全规则静默失效问题：`hookify` 插件现在会从所有祖先 `.claude` 目录加载配置，确保子目录中的规则不会被绕过。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85716)

### 3. 修复过时文档链接指向
- **#85822** | 状态: OPEN
- 将文档中指向 `docs.anthropic.com` 的过时链接更正为 `code.claude.com/docs` 规范地址，消除重定向损耗与文档漂移。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85822)

### 4. 插件开发技能使用规范命名
- **#85243** | 状态: OPEN
- 修复 8 个内置技能中 `name` 字段含空格、不符合规范的问题（如 `Writing Hookify Rules` → 规范格式），涉及 plugin-dev 与 hookify 技能。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85243)

### 5. 安全指导: 文档中跳过 XSS 告警
- **#85806** | 状态: OPEN
- 复用路径过滤器，避免文档/说明文字触发 XSS 相关告警，同时保留可执行源码的原有告警规则与 ID，附带回归测试。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85806)

### 6. HackerOne 赏金计划访问问题修复
- **#85834** | 状态: OPEN
- 调整 `devcontainer.json` 参数以确保 hookify 插件正确安装，修复 HackerOne 赏金计划的访问问题。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85834)

### 7. 清理残余旧文档链接
- **#85925** | 状态: OPEN
- 承接 #85822 的后续清理，覆盖 plugins、skills/agents/commands 及 issue 模板中的剩余旧域名链接。
- 📎 [链接](https://github.com/anthropics/claude-code/pull/85925)

---

## 五、功能需求趋势

### 1. 功能移除透明度与回滚机制（声量最大 🔥）
- #45596 "Bring Back Buddy" 以 1167 👍 居首。社区核心诉求：**功能移除前应经过社区讨论，或提供可选的 legacy 开关**。此议题已超越单个功能本身，演变为对**产品治理流程**的普遍要求。

### 2. 成本控制与预算护栏
- 多项 Issue（#67636 并行 Agent 消耗、#81703 计费事故、#85912 挂起任务烧钱、#83062 自动充值）指向同一方向：**缺少硬性消费上限、实时用量告警和异常任务熔断机制**。

### 3. 非侵入式交互（消息队列模式）
- #50246 建议在任务执行中支持排队消息而非强制中断。核心价值在于**保护长任务上下文**，提升人机协作流畅度。

### 4. 多账号与 MCP 生态扩展
- #36024 Gmail 多账号支持为代表，社区希望 MCP 生态向**多实例、多身份**方向演进，适配真实办公场景。

### 5. 跨会话协作原语
- #76727 针对多会话同仓库协作场景，希望有**官方协调机制**（当前仅能通过 PreToolUse hook 自建）。

---

## 六、开发者关注点

### 1. 稳定压倒一切
- TUI 重绘卡死（已修复于 v2.1.228）、输入队列静默丢失（#85603）、鼠标点击误触发权限（#71539）——交互稳定性问题占据大量声量。开发者对**长会话可靠性**的要求极为迫切。

### 2. 自主性边界争议（涉及信任危机）
- 一位用户（andreapeterfly-prog）连续提交 10+ 个 Issue（#85531、#71576、#72061、#76044 等），集中控诉**模型不遵循指令、未经授权执行操作**。尽管部分反馈情绪化，但“明确指令被忽略”的模式值得官方系统性审视。

### 3. 成本透明与告警（信任支柱）
- 单笔 $1,031.92 的静默消费事件（#85912）与 $604.71 错误扣费（#81703）正在侵蚀用户信任。开发者要求：**预告警、硬上限、分级通知**。

### 4. Windows 平台体验持续追赶
- #14828 控制台闪烁、v2.1.228 的 Git 路径修复——Windows 用户基数庞大，体验问题响应速度直接影响平台口碑。

### 5. AUP 误伤率
- sworrl 提交的多个 AUP 误报 Issue（#71332、#71313、#71299）均已关闭，但展示了**安全策略在复杂真实场景下的误伤风险**。开发者希望有更可解释的判定依据与便捷的中诉通道。

---

> **编辑注**：社区情绪整体呈现“**功能期待高、信任建设急**”的态势。v2.1.228 修复质量扎实，但 Buddy 请愿与计费争议若得不到透明回应，可能进一步发酵。建议官方关注 #45596 与 #81703 的后续处理。

*日报生成时间: 2026-08-12 | 数据窗口: 过去 24 小时*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-12** | **数据来源：github.com/openai/codex**


## 一、今日速览

昨日发布两个 Rust alpha 版本（v0.148.0-alpha.7/8），为应用稳定性铺路；Linux 桌面版需求（#11023）已关闭，但社区讨论热度不减（207 条评论、950 👍）；Windows 平台多个 Bug（内存暴涨、MCP 暴露、apply_patch 卡顿）持续发酵，另有批量 PR 集中优化 Windows 沙箱和 TUI 体验。


## 二、版本发布

| 版本 | 说明 |
|---|---|
| **rust-v0.148.0-alpha.8** | 常规 alpha 迭代，无额外说明 |
| **rust-v0.148.0-alpha.7** | 常规 alpha 迭代，无额外说明 |

> 注：两个 alpha 版本均未附带详细 changelog，建议关注后续 release notes。


## 三、社区热点 Issues（10 个精选）

### 1. [CLOSED] Codex Linux 桌面应用请求
**Issue #11023** | 作者: Suhaibinator | 评论: 207 | 👍: 950
- **内容**：用户因 macOS 上电源消耗问题（#10432）无法正常使用 Codex 应用，请求官方提供 Linux 桌面版。
- **重要性**：该 Issue 已关闭（可能已在内部规划中），但 950 个 👍 和 207 条评论表明 Linux 桌面版需求极为强烈，是社区关注度最高的问题之一。
- 🔗 https://github.com/openai/codex/issues/11023

### 2. [OPEN] Codex App 每次启动静默创建空 `~/Documents/Codex` 文件夹
**Issue #20880** | 作者: DrWaKu | 评论: 22 | 👍: 42
- **内容**：应用每次启动都会在用户文档目录下生成空文件夹，且无法阻止。
- **重要性**：看似小问题，但 42 个 👍 说明大量用户受到打扰；涉及应用对文件系统的静默副作用。
- 🔗 https://github.com/openai/codex/issues/20880

### 3. [OPEN] App 内子代理卡片关闭后仍卡在界面上
**Issue #23930** | 作者: omarpinarecords | 评论: 16 | 👍: 4
- **内容**：子代理已完成/关闭后，UI 卡片仍长时间残留在界面上，与实际状态不一致。
- **重要性**：直接影响桌面端日常使用体验，属 UI 状态同步类 Bug。
- 🔗 https://github.com/openai/codex/issues/23930

### 4. [OPEN] macOS 桌面版无法恢复 Remote Control / CLI 线程（回归）
**Issue #37403** | 作者: xkun1 | 评论: 9 | 👍: 9
- **内容**：8 月 7 日更新后，手机端 Remote Control 与桌面端同一 Codex CLI 线程无法正常衔接，报 `already has an active writer` 错误。
- **重要性**：回归 Bug 打破了用户「手机发起、桌面继续」的核心 Remote 工作流。
- 🔗 https://github.com/openai/codex/issues/37403

### 5. [OPEN] CLI 0.147.0：Esc-Esc 回溯无法定位持久化线程中的选中提示
**Issue #37421** | 作者: PaulRBerg | 评论: 4 | 👍: 25
- **内容**：Esc-Esc 双按回溯（backtrack）功能在从持久化线程中无法找回已选的 prompt。
- **重要性**：25 个 👍 表明该交互被高频使用，回归影响面较大（已关闭，说明已定位或修复）。
- 🔗 https://github.com/openai/codex/issues/37421

### 6. [OPEN] Codex 设置了完全访问权限+关闭审批后仍频繁请求权限
**Issue #29235** | 作者: mrlightsource-create | 评论: 3 | 👍: 16
- **内容**：即使线程配置了完整文件系统访问权限且关闭了审批提示，Codex 仍频繁请求用户批准普通操作。
- **重要性**：权限机制逻辑与用户配置不一致，严重阻断自动化工作流。
- 🔗 https://github.com/openai/codex/issues/29235

### 7. [OPEN] Windows 桌面版内存飙升至 8.8 GB 且 UI 冻结
**Issue #38059** | 作者: Dororo367 | 评论: 3 | 👍: 0
- **内容**：Windows 桌面版（26.803.10989.0）空闲时内存涨至 8.8 GB，发 1-2 条消息后 UI 冻结。
- **重要性**：新提交的高严重性性能问题，Windows 平台稳定性急待改善。
- 🔗 https://github.com/openai/codex/issues/38059

### 8. [OPEN] scheduled 桌面运行在 `list_threads` 上挂起
**Issue #35030** | 作者: jm-fhc | 评论: 5 | 👍: 1
- **内容**：自动化定时任务调用 `list_threads` 工具时挂起，而手动交互调用正常。
- **重要性**：自动化/无人值守场景下可靠性的关键缺陷。
- 🔗 https://github.com/openai/codex/issues/35030

### 9. [OPEN] 实时语音在成功委托后丢失任务工具处理器与路由
**Issue #36404** | 作者: adamcooper | 评论: 5 | 👍: 1
- **内容**：实时语音（Realtime Voice）在成功委托给子代理后，task-tool 处理器丢失，宿主路由失效。
- **重要性**：语音交互链路中的深层状态问题，影响复杂任务委托场景。
- 🔗 https://github.com/openai/codex/issues/36404

### 10. [OPEN] CLI 不支持直接粘贴图片
**Issue #19143** | 作者: CookGuo | 评论: 11 | 👍: 7
- **内容**：Codex CLI 不支持从剪贴板直接粘贴图片到会话中，影响前端调试等图像相关任务。
- **重要性**：已开放 3 个多月仍无进展，用户对图贴/多模态输入的需求持续累积。
- 🔗 https://github.com/openai/codex/issues/19143


## 四、重要 PR 进展（10 个精选）

### 1. 简化排队用户消息准入流程
**PR #38092** | 作者: copyberry[bot]
- **内容**：用户消息在 Core 接受后即时准入（新回合或转向），无需等待 rollout 持久化；删除队列消息在 Core 接受后不再保留。
- 🔗 https://github.com/openai/codex/pull/38092

### 2. 为 MCP OAuth 注册添加 CIMD 支持
**PR #38089** | 作者: copyberry[bot]
- **内容**：当授权服务器支持公共客户端且 Codex 使用本地回环回调时，优先使用 Client ID Metadata Documents (CIMD) 方式注册；否则回退到 Dynamic Client Registration。
- 🔗 https://github.com/openai/codex/pull/38089

### 3. gRPC code-mode 会话接入共享 HTTP 客户端
**PR #38087** | 作者: copyberry[bot]
- **内容**：通过 HttpClienteFactory 构建 URL-based gRPC 连接，支持应用的外置代理和自定义 CA 配置；仅允许 http/https 协议。
- 🔗 https://github.com/openai/codex/pull/38087

### 4. 支持执行主机上下文解析云配置
**PR #38086** | 作者: copyberry[bot]
- **内容**：新增 `AbsolutePathBufGuard::with_home_directory`，`~` 路径可显式指定 home 目录解析，同时保留基础目录行为。
- 🔗 https://github.com/openai/codex/pull/38086

### 5. 允许空输入启动回合
**PR #38084** | 作者: copyberry[bot]
- **内容**：`Op::UserInput` 无条目时允许立即准入并启动回合，依靠生成的环境上下文推进；持久化准入仍拒绝空输入。
- 🔗 https://github.com/openai/codex/pull/38084

### 6. Windows 沙箱支持嵌套 Git 仓库
**PR #38080** | 作者: copyberry[bot]
- **内容**：将工作树根目录及其 `/*` 通配符加入 Git 安全目录列表，使嵌套仓库在沙箱用户模式下可用。
- 🔗 https://github.com/openai/codex/pull/38080

### 7. 减少 world-state 补丁处理中的克隆次数
**PR #38078** | 作者: copyberry[bot]
- **内容**：直接从借用 JSON 值反序列化类型化段快照；在适当位置构建和应用合并补丁，避免整体快照克隆。
- 🔗 https://github.com/openai/codex/pull/38078

### 8. 按渲染宽度处理 TUI 历史记录
**PR #38075** | 作者: copyberry[bot]
- **内容**：新聊天部件按当前终端宽度初始化；历史单元格可见性根据活动渲染模式和可用宽度判定；diff-summary 饱和度有界。
- 🔗 https://github.com/openai/codex/pull/38075

### 9. 使用 `ReviewDecision` 统一 MCP 工具审批
**PR #38081** | 作者: copyberry[bot]
- **内容**：引入跨会话持久化的 MCP 审批策略，MCP 审批响应统一走 `ReviewDecision` 类型；保留仅限会话的审批、拒绝原因与超时。
- 🔗 https://github.com/openai/codex/pull/38081

### 10. 将 gRPC code-mode 回调转发至会话委托
**PR #38072** | 作者: copyberry[bot]
- **内容**：每个 gRPC code-mode 会话订阅嵌套工具调用，将工具/通知回调转发给委托；通过宿主完成工具调用，限制超大结果与错误。
- 🔗 https://github.com/openai/codex/pull/38072


## 五、功能需求趋势

| 趋势方向 | 代表 Issues / PRs | 热度 |
|---|---|---|
| **Linux 桌面版支持** | #11023（950 👍）、#6150 RISC-V Linux 支持 | 🔥🔥🔥🔥🔥 |
| **Windows 平台稳定性** | #38059 内存暴涨、#35470 复制 150,000 次图片、#34549 apply_patch 卡顿、#32525 沙箱 ACL 报错 | 🔥🔥🔥🔥 |
| **应用/桌面端可靠性** | #20880 静默文件夹、#23930 子代理卡死、#37403 Remote Control 回归 | 🔥🔥🔥🔥 |
| **远程控制与自动化（Remote Control / Scheduled Runs）** | #37403、#35030、#38095 | 🔥🔥🔥 |
| **MCP 相关改进** | #37471（Windows MCP 未暴露）、#37567 MCP 回归、#37417 工具列表热更新、#31354 自定义 provider 下 MCP 调用失败、PR #38089 / #38081 | 🔥🔥🔥 |
| **多模态/图片支持** | #19143 粘贴图片（7 👍）、#20946 imagegen skill 未物化 | 🔥🔥 |
| **自定义模型与 API-Key 支持** | #37858 multi_agent 不可用、#37379 自定义模型被隐藏、#31354 | 🔥🔥 |
| **权限与沙箱体验优化** | #36115 “Allow once” 无响应、#29235 权限提示绕过配置、#38080 / #38064 沙箱路径完善 | 🔥🔥 |
| **CLI/TUI 交互细节** | #37421 Esc-Esc 回溯、#38075 历史记录宽度、#38071 语法高亮 | 🔥🔥 |


## 六、开发者关注点（痛点与高频需求）

### 痛点 Top 3

1. **Windows 平台问题密集** — 内存泄漏（#38059）、沙箱 ACL 错误（#32525）、apply_patch 卡顿（#34549）、MCP 服务器不可见（#37471）等多个问题并行存在，Windows 被明显边缘化。

2. **权限/审批机制与配置脱节** — 即使用户已设置完全访问+关闭审批（#29235），系统仍然频繁弹窗；`Allow once` 按钮无效（#36115），交互路径极不顺畅。

3. **回归和状态同步问题频发** — Remote Control 在更新后直接失效（#37403）、CLI 回溯功能回归（#37421）、子代理卡片状态与后端不一致（#23930），稳定性与一致性仍需提升。

### 高频需求

- **Linux 支持（桌面版）** 呼声最高，950 👍 已充分说明。
- **MCP 生态完善**：跨平台暴露、热更新、OAuth/CIMD 注册、自定义 provider 兼容等。
- **自动化与远程工作流可靠化**：Scheduled Runs、Remote Control、headless 场景下的线程管理。
- **CLI 多模态/图片交互**：直接粘贴图片是呼声最高的 CLI 功能缺口。
- **自定义模型深度集成**：multi-agent 与 custom provider 的兼容性、UI 中模型可见性。
- **沙箱体验与文件系统透明化**：减少无谓的权限请求、提升沙箱 ACL 可靠性（尤其 Windows）。

---

*日报由 AI 自动生成，数据基于 2026-08-11 至 2026-08-12 GitHub 活动。部分 Issue/PR 状态以仓库实时为准。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-12

## 今日速览

今日最值得关注的是 **v0.55.1 正式版与 v0.56.0-preview.1 预览版相继发布**，其中预览版修复了 MCP OAuth 令牌刷新时 client ID 丢失的问题。同时，**两项 CVE（shell-quote 与 simple-git）修复 PR 以 CRITICAL 级别提交**，建议用户留意依赖更新。社区讨论焦点仍集中在 **Subagent 行为可靠性**（挂起、误报成功）与 **Auto Memory 安全与效率问题** 上。

## 版本发布

### v0.55.1（最新稳定版）
- 修复 release 验证流程中 npm ci 忽略脚本的问题
- 修复 CI 中 workspace 二进制文件遮蔽问题，确保发布验证准确性
- 引入 Tool Registry 相关基础功能

### v0.56.0-preview.1（最新预览版）
- 修复核心问题：**MCP OAuth 令牌刷新时使用已存储的 client ID**（PR #28481，来自新贡献者 @ParthivNaresh）

### v0.55.0-preview.3
- 针对 v0.55.0-preview.2 的补丁版本，cherry-pick 了 PR #28730 的 quota 查找映射修复

### v0.56.0-nightly.20260811.geef19f25c
- 与 v0.56.0-preview.1 相同的 OAuth 修复

## 社区热点 Issues（Top 10）

### 1. Subagent 在 MAX_TURNS 后误报 GOAL 成功，掩盖中断
**Issue #22323** | 评论 12 | 👎 值得关注：高
`codebase_investigator` 子代理在达到最大轮次限制后仍报告 `status: "success"`，使用户无法感知任务实际上被截断。这是对 **Agent 执行透明性** 的核心质疑，社区期待状态报告机制更严谨。
🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### 2. Generalist agent 挂起，最长等待 1 小时无响应
**Issue #21409** | 评论 8 | 👍 8
当 Gemini CLI 委派任务给 generalist agent 时，简单操作（如创建文件夹）也会无限期挂起。用户不得不显式禁止 sub-agent 委派才能恢复。该问题在高 👍 数下凸显 **Agent 稳定性已成为首要痛点**。
🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### 3. 利用模型 bash 亲和力：零依赖 OS 沙箱与执行后意图路由
**Issue #19873** | 评论 8 | 类型：enhancement
提议利用 Gemini 3 模型天然擅长 POSIX 工具链的特性，通过轻量级操作系统级沙箱（而非更重型的容器方案）来兼顾安全性与效率，提议在执行后对命令意图进行路由和审批。方向契合 "模型原生能力 + 安全收敛" 的开发趋势。
🔗 https://github.com/google-gemini/gemini-cli/issues/19873

### 4. 组件级评估体系（Component Level Evaluations）EPIC
**Issue #24353** | 评论 7 | 类型：EPIC
自引入行为评估以来已累积 76 个测试，覆盖 6 个 Gemini 模型，但组件级（如 agent、工具、IDE 集成）的精细化评估仍有缺口，本 EPIC 旨在补齐该能力，进而提升整体系统可靠性。
🔗 https://github.com/google-gemini/gemini-cli/issues/24353

### 5. AST 感知的文件读取与代码库映射价值评估
**Issue #22745** | 评论 7 | 类型：EPIC
探索利用 AST 感知工具实现更精确的函数边界读取、导航与代码库映射，以减少模型误读、降低 token 消耗、提升多轮效率。目前已有多个相关子议题（如 #22746）展开具体调研。
🔗 https://github.com/google-gemini/gemini-cli/issues/22745

### 6. Gemini 未充分主动使用自定义 skills 与 sub-agents
**Issue #21968** | 评论 6
用户反馈模型不会在相关场景下自主调用已配置的 skills（如 gradle、git），必须在显式指令下才使用。这关系到 **CLI 对用户自定义工作流的利用率**，也是 Agent 自主规划能力的体现。
🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### 7. Shell 命令执行完成后卡在 "Waiting input"
**Issue #25166** | 评论 4 | 👍 3
即使最简单的 CLI 命令已执行完毕，界面仍显示等待用户输入，导致对话流程阻塞。涉及核心交互稳定性，高 👍 数表明影响范围较广。
🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### 8. Auto Memory 低信号会话无限重试
**Issue #26522** | 评论 5
当提取 agent 因会话价值低而跳过读取时，相关记录不会被标记为已完成，导致被反复呈现，造成资源浪费。社区建议引入幂等标记或去重机制。
🔗 https://github.com/google-gemini/gemini-cli/issues/26522

### 9. Auto Memory 需确定性脱敏与日志精简
**Issue #26525** | 评论 4 | 类型：security
当前在提取前敏感内容已进入模型上下文，且服务可能记录包含技能标签的日志，存在凭据泄漏风险。此安全问题若确认，优先级应上调。
🔗 https://github.com/google-gemini/gemini-cli/issues/26525

### 10. 浏览器子代理在 Wayland 下失败
**Issue #21983** | 评论 4
`browser_agent` 在 Wayland 会话中无法正常完成目标。随 Linux 桌面 Wayland 普及，该兼容性问题的覆盖面可能持续扩大。
🔗 https://github.com/google-gemini/gemini-cli/issues/21983

## 重要 PR 进展（Top 10）

### 1. 升级 shell-quote 至 1.8.4（CVE-2026-9277，CRITICAL）
**PR #28780** | 状态：OPEN
安全扫描发现依赖 `shell-quote` 存在严重漏洞，建议尽快合入。此类 CVE 修复通常应进入下一个 patch 版本。
🔗 https://github.com/google-gemini/gemini-cli/pull/28780

### 2. 升级 simple-git 至 3.32.3（CVE-2026-28292，CRITICAL）
**PR #28778** | 状态：OPEN
另一个 CRITICAL 级依赖漏洞修复，涉及 git 操作场景的核心依赖，建议优先评估合入风险。
🔗 https://github.com/google-gemini/gemini-cli/pull/28778

### 3. 修复容量耗尽误报与 quota 查找映射
**PR #28730** | 状态：CLOSED
修复了 CLI 在模型容量充足却误报耗尽的问题，并纠正了 core 包中 quota 查询的模型映射，同时保留容量波动下的 "Keep trying" 选项，改善用户体验。
🔗 https://github.com/google-gemini/gemini-cli/pull/28730

### 4. 修复 IDE 连接中目录不匹配被吞掉的问题
**PR #28729** | 状态：CLOSED
解决在 Cider 或 VS Code 远程/FUSE 虚拟目录场景下，Gemini CLI 因匹配不到 IDE companion 端口文件而静默失败的问题。对远程开发工作流价值高。
🔗 https://github.com/google-gemini/gemini-cli/pull/28729

### 5. 动态解析 Cloud Workstations 代理重定向 URI
**PR #28688** | 状态：CLOSED
修复在 Cloud Workstations VM 中固定回环 `localhost` 导致 OAuth 失败的问题。云开发场景的 OAuth 体验改善。
🔗 https://github.com/google-gemini/gemini-cli/pull/28688

### 6. 容量耗尽归类为终止错误，避免重试挂起
**PR #28599** | 状态：CLOSED
将 `MODEL_CAPACITY_EXHAUSTED`（HTTP 429）显式归类为终止错误，无重试延迟时立即触发备用模型链，防止客户端无限挂起。与 #28716 思路一致，合并路径清晰。
🔗 https://github.com/google-gemini/gemini-cli/pull/28599

### 7. 行为评估工具：工具调用格式化与失败摘要
**PR #28305** | 状态：OPEN
在行为评估失败时输出紧凑的工具调用时间线（含参数、状态、错误详情），大幅提升失败排查效率。建议维护者关注。
🔗 https://github.com/google-gemini/gemini-cli/pull/28305

### 8. 行为评估本地报告命令与开发文档
**PR #28369** | 状态：CLOSED
新增 `npm run eval:report` 命令，聚合各模型 pass rate 并映射回 inventory 策略，支持重复测试场景。降低评估门槛，利于社区参与。
🔗 https://github.com/google-gemini/gemini-cli/pull/28369

### 9. 跳过 diff hunk 标记以防止巨型 glob 搜索
**PR #28581** | 状态：OPEN
避免将 unified/combined diff 中的 hunk 标记（如 `@@`）误识别为 `@file` 引用，消除了每个 hunk 两次递归全工作区 glob 搜索导致的堆内存膨胀，对大 diff 场景友好。
🔗 https://github.com/google-gemini/gemini-cli/pull/28581

### 10. vscode-ide-companion：正确追踪所有 Disposable
**PR #28764** | 状态：OPEN
修复 `activate()` 中多余的括号导致的逗号表达式问题——两个注册虽执行但只追踪了最后一个 Disposable，可能导致 `gemini.diff.accept` 命令重复注册。属于资源泄漏修复，建议合入。
🔗 https://github.com/google-gemini/gemini-cli/pull/28764

## 功能需求趋势

1. **子代理（Subagent）行为增强**：大量 Issue 聚焦 subagent 的可靠性（#21409、#22323）、自主调用能力（#21968）、制裁危险操作（#22672）、轨迹可视化（#22598）等方面，说明多代理协作已成为社区关注的核心方向。
2. **AST 感知工具链**：以 #22745 为 EPIC，社区积极探索 AST 感知的文件读取与代码库映射，目标在于降低 token 开销、提升跨文件检索精度。
3. **Auto Memory 安全问题**：从 #26522、#26523、#26525 可见，背景提取 agent、低信号会话处理与脱敏策略是当前内存系统的主要关注方向，偏向确定性与可观测性。
4. **Tool Registry 与依赖治理**：v0.55.1 引入 Tool Registry 基础，结合 #24246（超过 128 个工具触发 400 错误）来看，大规模工具集场景下的动态裁剪是下一步可能重点。
5. **安全修复的自动化与时效性**：两个 CRITICAL CVE（shell-quote、simple-git）的提交均自动附带安全规则信息，反映社区对供应链安全的高敏感度。

## 开发者关注点

- **稳定性是第一诉求**：generalist 挂起（#21409）、shell 卡在 "Waiting input"（#25166）、容量耗尽误报（#28730）等问题直接阻断日常工作流，相关 issue 的 👍 数与评论数均靠前，建议维护者优先处置高频出现的交互阻塞类缺陷。
- **安全与信任**：Auto Memory 的明文日志与预脱敏机制（#26525）引发对凭据泄漏的担忧；同时 400 工具上限的硬性报错（#24246）限制了大型工作区的可用性。
- **可观测性不足**：subagent 轨迹难以通过 `/chat share` 分享（#22598），`/bug` 报告缺少子代理上下文（#21763），使得社区难以进行问题复现与行为评估。
- **配置覆盖与兼容性**：浏览器 agent 忽略 settings.json（#22267）、Wayland 下失败（#21983）、symlink agent 文件不被识别（#20079）等细节问题虽小但影响面明确，涉及权限与平台适配的配置覆盖问题值得尽快收口。

---
*本日报基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-12**


## 1. 今日速览

今日社区动态集中在 v1.0.79 引入的一系列回归问题，包括 `/config model` 命令清空设置文件、用户级模型配置在新会话中不生效，以及橡皮鸭审查机制被模型参数静默覆盖等配置与模型选择相关缺陷。与此同时，Windows 平台插件安装权限问题（`Access is denied`）持续发酵，成为获得 👍 最多的未解决问题；功能需求方面，社区对压缩保留长期上下文、显式文件编辑模式和企业级策略管控的呼声明显上升。


## 2. 版本发布

过去 24 小时内无新版本发布（当前最新版本为 v1.0.79）。


## 3. 社区热点 Issues（10 个）

### #4431 — `/config model` 命令清空全部设置（已关闭）
**作者**: PatrickGaissert | **评论**: 3 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4431)

**问题描述**：v1.0.79 中，通过 `/config model` 设置全局模型时，会直接覆写 `~/.copilot/settings.json` 中的全部既有配置，造成用户自定义设置全部丢失。该 issue 已关闭，但直接影响所有使用 `/config` 命令的用户。

🔗 关联问题：[#4434 用户级模型配置在新会话中不生效](https://github.com/github/copilot-cli/issues/4434)

### #4095 — Windows 上插件更新因 VS Code 占用文件句柄而失败（🔥 14 👍）
**作者**: FBakkensen | **评论**: 2 | **👍**: 14 | [链接](https://github.com/github/copilot-cli/issues/4095)

**社区反应**：当前社区最高赞 issue。当 VS Code 运行且 Copilot 扩展持有已安装插件的文件监视器句柄时，`copilot plugin update` 在 Windows 上持续报 `Access is denied (os error 5)`。配合 [#4151](https://github.com/github/copilot-cli/issues/4151)（全新安装同样 100% 失败），Windows 插件生态基本不可用。

### #4251 — 大会话恢复导致 OOM / CPU 100% 70 分钟（1.0.74 回归）
**作者**: oldake | **评论**: 3 | **👍**: 1 | [链接](https://github.com/github/copilot-cli/issues/4251)

**问题描述**：从 1.0.73 升级到 1.0.74 后，恢复大型会话的内存峰值约为之前的 3-4 倍，导致 OOM 或单个 CPU 核心满负荷约 70 分钟。作者通过仅更换 CLI 版本的 A/B 测试（同一机器、同一会话）明确将该问题定位为 1.0.74 回归，对长期保持活跃会话的重度用户影响显著。

### #4211 — Copilot CLI 无法处理 MCP 响应中的 BigInt
**作者**: xj-ms | **评论**: 3 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4211)

**问题描述**：当 MCP 服务器响应中包含大整数时，CLI 报 `TypeError: Do not know how to serialize a BigInt`，导致所有正在进行的任务被中止。已被标记 `triaged`，属于 MCP 协议实现中的序列化缺陷。

### #4380 — 橡皮鸭审查未使用独立的互补模型族
**作者**: tanselmi-appliedsurety | **评论**: 3 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4380)

**问题描述**：`rubber-duck` 审查机制有时使用与主会话相同的模型族而非独立的互补模型，削弱了对抗性审查的价值。作者在多种模型上均观察到该行为，最近一次发生在 5.6 Terra - Max 上。

### #4432 — 模型发出的 `model` 参数静默覆盖橡皮鸭互补策略（NEW）
**作者**: eggboy | **评论**: 1 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4432)

**问题描述**：`rubber-duck` 子代理的设计意图是提供跨模型族的第二意见（Claude 会话配 GPT 审查员，反之亦然），但 `task` 工具暴露的可选 `model` 参数允许模型自行指定，从而静默绕过 `complementary` 策略。与 #4380 形成互补，共同指向橡皮鸭模型选择的完整性缺陷。

### #4405 — Copilot Free 在 Codespaces 中报 "No model available"
**作者**: bazaarjapan | **评论**: 1 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4405)

**问题描述**：GitHub Copilot Free 账户在 Codespaces 中启动 CLI 后，每次提示立即失败并报 `No model available. Check policy enablement under GitHub Settings > Copilot`。涉及自动选择、token 隔离和重新登录多个层面，影响免费层级的 Codespaces 用户。

### #4439 — CLI 1.0.79 拒绝 GitLab MCP OAuth 元数据（RFC 8414 issuer 不匹配）
**作者**: patrickzel | **评论**: 1 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4439)

**问题描述**：针对 GitLab Self-Managed MCP 服务器使用 OAuth 2.0 动态客户端注册时，CLI 因 RFC 8414 issuer 不匹配而认证失败，阻断企业 GitLab + MCP 场景。

### #4438 — `disable-model-invocation: true` 使技能完全不可达（NEW）
**作者**: grammy-jiang | **评论**: 1 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/4438)

**问题描述**：项目技能的 `SKILL.md` 前置元数据标记 `disable-model-invocation: true` 后，`copilot skill list` 仍显示该技能在项目技能列表中，但模型侧 `skill()` 工具返回 `Skill not found`，显式用户请求同样失败。与 [#4451](https://github.com/github/copilot-cli/issues/4451) 共同指向技能可发现性与模型调用之间的割裂。

### #3976 — 内置 `tgrep` 索引器在大型 monorepo 上 OOM 杀死宿主机
**作者**: reillysiemens | **评论**: 2 | **👍**: 0 | [链接](https://github.com/github/copilot-cli/issues/3976)

**问题描述**：启用 `copilot_cli_tgrep` 实验后，会话启动时 spawn 持久化 daemon（`tgrep serve . --index-path ...`），在大型 monorepo 上无内存上限控制，直接 OOM 杀死宿主机。对 monorepo 用户的稳定性构成直接威胁。


## 4. 重要 PR 进展（2 条）

### #4449 — 将 PR 自动化迁移出 `pull_request_target`
**作者**: mrecachinas | **状态**: Draft | [链接](https://github.com/github/copilot-cli/pull/4449)

**内容**：将仓库的 PR 驱动工作流从 `pull_request_target` 迁移到低权限模式——不受信任的 PR 输入在 `pull_request` 工作流中运行，需要仓库写权限的操作移至独立流程。这是针对供应链攻击的加固措施，符合当前开源安全最佳实践。

### #4428 — 添加初始 devcontainer 配置
**作者**: Pjrich1313 | **状态**: Open | [链接](https://github.com/github/copilot-cli/pull/4428)

**内容**：为仓库添加开发容器配置，降低新贡献者的环境搭建门槛。


## 5. 功能需求趋势

从今日 issue 中提炼的社区最关注功能方向：

- **配置持久性与一致性**：`/config model` 清空设置、用户级默认模型在新会话不生效、压缩机制递归丢失早期决策上下文，社区对配置管理与长期会话稳定性有强烈诉求。（#4431, #4434, #4441）

- **技能（Skills）生命周期管理**：重复技能加载、禁用模型调用的技能不可达、显式斜杠技能被冗余重新加载，反映技能系统仍在快速演进，边界情况多。（#4430, #4438, #4451）

- **企业级策略管控**：要求 GitHub 企业可配置 Copilot CLI 的 sandbox 启用与配置推送，降低成本管理复杂度。（#4446）

- **细粒度权限与安全**：区分工作目录外的只读与写操作权限提示；对每个文件编辑提供显式接受/拒绝/评论的交互模式。（#4443, #4444）

- **多工具链兼容**：支持读取 `.claude/rules` 与 `.claude/agents/*/AGENT.md`，避免与 Claude Code 重复维护指令；同时关注依赖供应链安全（`adm-zip` CVE）。（#4440, #4437, #4442）

- **模型选择可靠性**：`auto` 模式偶发选择不可用的推理级别模型导致崩溃；模型族隔离与互补策略需要更严格的执行保证。（#4445, #4380, #4432）


## 6. 开发者关注点

**高频痛点 Top 3：**

1. **Windows 插件生态不可用**（#4095 +14👍, #4151）：安装和更新均告失败，根因是文件句柄占用，社区关注度最高但修复进度缓慢。

2. **v1.0.79 配置相关回归**（#4431, #4434）：设置被清空、用户默认模型不生效，影响所有使用 `/config model` 的用户，且 #4431 已关闭但 #4434 仍在 triage。

3. **模型选择与审查机制不可控**（#4380, #4432, #4445）：模型可自行覆盖审查策略、选择不可用推理级别导致崩溃，用户对模型行为的可预测性信心不足。

**其他值得关注：**

- 大型会话恢复性能回归（#4251）虽非高频，但影响深度用户，1.0.74 引入、当前版本是否修复待确认。
- 安全红线：`adm-zip` 高危 CVE 已进入官方扫描结果（#4442），需及时跟进升级。
- 输入体验细节：backspace 按词删除（#4447）与搜索卡死（#4448）等小问题在 1.0.79 中集中出现，影响日常使用。

---

> 注：今日无新版本发布，多为 v1.0.79 发布后的集中反馈期。Windows 插件问题、配置回归和橡皮鸭模型选择是当前社区呼声最高的三大主题。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-12** | **数据来源：** [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)


## 今日速览

昨日社区讨论热度集中在**记忆系统（Memory System）** 的实现路径上——既有自2月延续至今的 [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283) 仍在等待官方方案，又有 [#1478](https://github.com/MoonshotAI/kimi-cli/issues/1478) 发出“大项目很痛苦”的呼声。与此同时，社区贡献者 **hobostay** 提交的一组 PR（#2055、#2056、#2057）于8月11日被标记为已关闭，可能为近期合并做准备。此外，Windows PowerShell 7 默认目录导致的路径 bug（[#2600](https://github.com/MoonshotAI/kimi-cli/issues/2600)）是新浮现的高频环境问题。


## 社区热点 Issues

### 1. [Feature Request: Memory System – Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)（#1283，OPEN）
- **作者：** CatKang | **更新：** 08-11 | **评论：** 34
- **要点：** 社区呼声最高的长期需求，要求实现自动（AI 管理）+ 手动（用户自定义）双层记忆体系，跨会话保留项目模式与用户偏好。
- **社区反应：** 34条评论，讨论持续近半年未关闭，是目前功能需求类 Issue 中热度最高的一条。

### 2. [能否优化记忆层？大项目开发很痛苦](https://github.com/MoonshotAI/kimi-cli/issues/1478)（#1478，OPEN）
- **作者：** hahy36 | **更新：** 08-11 | **评论：** 1
- **要点：** 用户反馈在大型项目中缺乏记忆层支持是核心痛点，且官方文档中仅找到 `agent.md`，未看到体系化的记忆管理方案。作者贴出了参考的目录结构（`SOUL.md` / `USER.md` / `MEMORY.md`）。
- **社区反应：** 与 #1283 形成呼应，说明“记忆系统”这一需求已从单一 feature request 演变为群体性诉求，且用户开始自发探索替代方案。

### 3. [Quote & Reply：在 Kimi Web 中对 AI 回复的任意片段进行引用评论](https://github.com/MoonshotAI/kimi-cli/issues/2601)（#2601，OPEN）
- **作者：** topit | **创建/更新：** 08-11 | **评论：** 0
- **要点：** 请求在 Kimi Web 端支持对 AI 回复的任意文本片段（段落、代码块、计划步骤、diff 解释行）进行选中、引用和追问，实现精准的上下文关联交互。
- **价值：** 反映用户对细粒度交互控制的需求——从“整体对话”走向“片段级协作”，类似 IDE 中代码行评论的体验。

### 4. [Bug：PowerShell 7 默认 D 盘启动导致路径找不到](https://github.com/MoonshotAI/kimi-cli/issues/2600)（#2600，OPEN）
- **作者：** RooKichenn | **创建/更新：** 08-11 | **评论：** 0
- **要点：** Windows 用户将 PowerShell 7 默认启动目录设为 D 盘后，从 D: 启动 kimi code 时无法定位路径。涉及版本 0.33。
- **价值：** 典型的 Windows 环境适配问题，影响非 C 盘默认目录的用户群体，说明跨平台路径处理仍有兼容性缺口。

### 5. [Bug：规划任务中 todo 出现“验尸”字样](https://github.com/MoonshotAI/kimi-cli/issues/2599)（#2599，OPEN）
- **作者：** KING0177 | **创建/更新：** 08-11 | **评论：** 0
- **要点：** 在 0.34.0 版本（`kimi k3` 模型）的规划任务中，todo 列表出现“验尸”字样，疑似模型输出异常或 prompt 配置问题。用户使用 2018 款 Intel Mac。
- **价值：** 暴露模型在特定场景下的输出质量问题，尤其是规划任务中术语使用的准确性，需关注是否为模型侧回归。


## 重要 PR 进展

### 1. [feat(kimi): configurable thinking effort and /effort command](https://github.com/MoonshotAI/kimi-cli/pull/2509)（#2509，OPEN）
- **作者：** n-WN | **更新：** 08-11
- **内容：** 新增可配置的思考强度（thinking effort）及 `/effort` 命令，关联 Issue #2501，并衔接已关闭的 #318（`reasoning_effort` 支持）与 #2499。
- **意义：** 这是当前唯一处于打开状态的功能性 PR，直接响应用户对推理深度控制的需求，值得重点关注其合入进度。

### 2. [fix(acp): replace assert statements with proper RuntimeError exceptions](https://github.com/MoonshotAI/kimi-cli/pull/2057)（#2057，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 将 `acp/session.py` 中 5 处 `assert` 替换为 `RuntimeError`。原 assert 在 Python `-O` 优化模式下会被剥离，导致关键不变量检查失效。
- **意义：** 修复了生产环境下的安全隐患，属于防御性编程的正确性改进。

### 3. [fix(wire): eliminate TOCTOU race in WireFile.append_record](https://github.com/MoonshotAI/kimi-cli/pull/2056)（#2056，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 修复 `WireFile.append_record` 中 TOCTOU（检查时点到使用时点）竞态条件，避免文件在 `exists()` 与 `stat()` 之间被删除导致未处理异常。
- **意义：** 提升文件写入的并发安全性和稳定性，对长时间运行的 CLI 进程尤为重要。

### 4. [fix(agentspec): replace assert with proper AgentSpecError exception](https://github.com/MoonshotAI/kimi-cli/pull/2055)（#2055，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 将 `agentspec.py` 中的 `assert agent_spec.extend is None` 替换为明确的 `AgentSpecError` 异常抛出。
- **意义：** 与 #2057 同属“去 assert 化”系列改动，保证控制流检查在优化模式下不被静默跳过。

### 5. [Fix minor bugs in file tools and UI feedback](https://github.com/MoonshotAI/kimi-cli/pull/1328)（#1328，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 修复三个小 bug：`StrReplaceFile` 多次编辑时替换计数基于原始内容计算不准确；另有两处 UI 反馈问题。
- **意义：** 提升文件编辑工具的准确性与用户操作反馈的即时性，属于体验打磨类修复。

### 6. [fix(pyinstaller): filter non-existent dateparser cache files](https://github.com/MoonshotAI/kimi-cli/pull/1082)（#1082，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 修复 PyInstaller 打包时 `dateparser` 时区缓存文件（`dateparser_tz_cache.pkl`）在全新环境或 CI 中不存在导致收集失败的问题。
- **意义：** 解决打包发布环节的环境依赖问题，提升安装成功率。

### 7. [fix: remove redundant mode validation in WriteFile tool](https://github.com/MoonshotAI/kimi-cli/pull/1077)（#1077，CLOSED）
- **作者：** hobostay | **更新：** 08-11（关闭）
- **内容：** 移除 `WriteFile` 工具中对 `mode` 参数（"overwrite"/"append"）的冗余运行时校验（原代码第 84-91 行）。
- **意义：** 简化代码逻辑，减少无意义检查开销。

### 8. [fix(acp): route shell commands through terminal args](https://github.com/MoonshotAI/kimi-cli/pull/1393)（#1393，CLOSED）
- **作者：** hanhan3344 | **更新：** 08-11（关闭）
- **内容：** 修复 ACP Shell 终端执行方式——将 shell 可执行文件放入 `command`、shell 调用参数放入 `args`；适配当前 ACP SDK 响应结构（使用 `terminal_id`）；新增针对 bash 和 PowerShell 的回归测试。
- **意义：** 完善 ACP 协议下的终端集成兼容性，跨 shell 场景的行为标准化。


## 功能需求趋势

1. **记忆系统（Memory System）—— 最强烈的单一诉求**
   - 两条 Issue（#1283、#1478）同时指向跨会话持久化上下文的能力，覆盖自动记忆与手动管理两种模式。
   - 用户已开始参考第三方实现（如 `~/.openclaw/workspace/` 目录结构），说明需求已从“想要”变成“需要替代方案”。

2. **交互粒度的精细化**
   - [#2601](https://github.com/MoonshotAI/kimi-cli/issues/2601) 提出的“选中-引用-评论”模式，反映出用户希望从整段对话走向片段级协作，这与 IDE 中代码行评论的体验对齐。

3. **推理深度可配置化**
   - PR #2509（`/effort` 命令）从功能实现层面回应用户对“思考强度”控制的需求，可能是近期最值得期待的能力扩展。


## 开发者关注点

- **大项目中的上下文管理是首要痛点**：#1478 明确表示“搞大项目的时候很痛苦”，且用户对文档中缺少记忆层说明感到困惑。建议官方在文档中明示当前记忆机制（或明确 roadmap），减少用户自行摸索的成本。
- **Windows 环境兼容性仍有缺口**：#2600 暴露了非默认启动目录下的路径解析问题，提示需要覆盖更多 Windows 使用习惯（如自定义 PowerShell 启动路径）。
- **模型输出质量在规划任务中的稳定性**：#2599 中“验尸”字样虽可能是个例，但规划任务的术语准确性直接影响用户信任度，建议关注 `kimi k3` 在该场景下的 prompt 模板或输出约束。
- **生产环境安全实践被社区关注**：hobostay 连续提交的“去 assert 化”PR 反映出活跃贡献者对 Python `-O` 模式下断言失效风险的重视，这类防御性改进对 CLI 工具的长期稳定性有价值。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-12

## 今日速览

V2 版本迁移与回归问题成为今日社区焦点：多起报告指出 V2 存在 Plan Mode 失效、webfetch 返回 null、模式切换对模型不可见等问题，同时 `apply_patch` 的文件覆盖与原子性问题也引发关注。值得庆幸的是，多项修复 PR（如 V1 迁移 SQL 注入修复）已在合并中。此外，TUI 可用性改进（目录自动补全、标签页加号按钮、隐藏实验区）和桌面端开发体验优化也贡献了显著活力。

---

## 社区热点 Issues

### 1. [#8501 [FEATURE]: Allow to expand the pasted text](https://github.com/anomalyco/opencode/issues/8501)
**🏆 社区最高热度** | 230 👍 | 35 评论
用户希望在被折叠的粘贴文本（`[Pasted ~1 lines]`）上提供展开/编辑能力，避免为了修改一小段文本而不得不重新粘贴全部内容。这是典型的编辑器体验打磨需求，高赞数反映了其广泛诉求。

### 2. [#16017 [FEATURE]: Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)
137 👍 | 33 评论 | 已关闭
请求公开 Go 计划订阅用量/余额的 API 端点（支持滚动/周/月窗口），目前该数据仅存在于 Dashboard 中。第三方客户端（如自定义 TUI）无法获取配额状态，已关闭说明可能已被纳入开发计划。

### 3. [#41777 [2.0] webfetch inside Code Mode returns null (regression)](https://github.com/anomalyco/opencode/issues/41777)
4 评论 | 新报告
V2（next 通道）中内置 `webfetch` 工具在 Code Mode 下报告成功但始终返回 `null`，且已从模型顶层工具列表中消失。问题定位在 `next-202606301613` 与 `next-16365` 之间的回归窗口，对依赖网页抓取的自动化工作流影响重大。

### 4. [#40474 [2.0] mode switches are invisible to the model (v1 parity gap)](https://github.com/anomalyco/opencode/issues/40474)
3 评论 | 已关闭
V2 中切换模式（Build ↔ Plan）后，`agent-switched` 消息在会话历史转 LLM 上下文时被静默丢弃，导致模型完全不知道当前处于什么模式——既无系统提示也无上下文中提醒。这是 V2 与 V1 的关键对齐缺口，直接影响多模式agent工作流的可靠性。

### 5. [#39831 Zen: gpt-5.6-luna / gpt-5.6-terra fail with HTTP 403](https://github.com/anomalyco/opencode/issues/39831)
5 评论 | 开放
通过 Zen (`opencode` provider) 使用 `gpt-5.6-luna` 和 `gpt-5.6-terra` 持续报错 `Error from provider (Console): Upstream request failed`（HTTP 403），而 `gpt-5.4-nano` 等工作正常。指向 Zen 提供商侧对新模型的支持或配置存在不完整。

### 6. [#41751 v1.18.16 server/web mode: 2 project skills silently dropped in git repo](https://github.com/anomalyco/opencode/issues/41751)
2 评论 | 新报告
v1.18.16 的 server/web 模式下，当项目位于 git 仓库内时恰好有 2 个 project skills 被静默丢弃——在 CLI/TUI 模式同二进制可加载全部 skills，无 `.git` 时也正常。高度环境相关的隐蔽 bug，排查难度大。

### 7. [#39181 TUI applies events from other directories with shared server](https://github.com/anomalyco/opencode/issues/39181)
4 评论 | 开放
当多个 TUI 通过一个 `opencode serve` 共享服务器、各自位于不同目录时，侧边栏右下角的 git 分支偶尔显示为其他项目的分支。多工作区共享场景下的状态串扰问题，与 #41839 高度关联。

### 8. [#37090 Tool apply_patch messes up line endings in Windows](https://github.com/anomalyco/opencode/issues/37090)
3 评论 | 开放
Windows 下 `apply_patch` 和 `write` 工具默认使用 LF 而非系统的 CRLF，导致文件行尾混乱。影响 Windows 用户的日常编辑工作流，需要跨平台的行尾处理策略。

### 9. [#41828 [2.0] v2 API gaps blocking third-party clients](https://github.com/anomalyco/opencode/issues/41828)
2 评论 | 开放
第三方 Rust TUI 客户端维护者列举了 5 项 V2 服务器缺失的 API 能力，这些缺口阻碍了生态客户端的完整移植。对社区生态多样性至关重要。

### 10. [#28986 Agent loop self-replies when message IDs are non-monotonic](https://github.com/anomalyco/opencode/issues/28986)
3 评论 | 已关闭
约 2.8% 的会话中，当消息 ID 非单调递增时，agent 循环在 `finish_reason: "stop"` 后继续生成，导致 AI 自问自答。指向消息排序/去重逻辑的边界条件缺陷，已关闭说明修复已合入。

---

## 重要 PR 进展

### 1. [#41870 feat(tui): autocomplete cd directories](https://github.com/anomalyco/opencode/pull/41870)
将 `/cd` 从命令补全切换为目录补全，支持 shell 风格路径（`~`、`.`、`..`、嵌套、绝对路径），并持久化项目级最近目录作为优先补全选项。显著提升 TUI 内的目录导航体验。

### 2. [#41888 feat(api): continue pending work after interrupt](https://github.com/anomalyco/opencode/pull/41888)
为 session interrupt 端点新增可选 `continue` 查询参数，在存在持久化待办工作时可从中断处恢复执行。为长时间运行任务提供更精细的控制能力。

### 3. [#41887 feat(tui): add plus button to session tab bar](https://github.com/anomalyco/opencode/pull/41887)
为会话标签栏添加 `+` 按钮，支持鼠标点击新建标签页，对齐浏览器标签栏交互模式。简化多会话工作流的新建入口。

### 4. [#41886 [FEATURE] Grok 4.5 not available on Go/Zen plans](https://github.com/anomalyco/opencode/issues/41886)
1 评论 | 新报告
用户反馈 Go 和 Zen 订阅计划中无法使用 Grok 4.5 API，涉及模型访问权限配置，需要官方确认是计划限制还是配置问题。

### 5. [#41879 test(client): accelerate service lifecycle tests](https://github.com/anomalyco/opencode/pull/41879)
通过加速私有定时策略，将 Client service 生命周期测试从 **72.556s 降至 4.529s**（节省 93.8%）。对 CI 时延敏感的大型项目意义重大。

### 6. [#41885 fix(core): restore bundler resolution for source-imported deps](https://github.com/anomalyco/opencode/pull/41885)
回退 `packages/core/tsconfig.json` 中导致 `v2` 类型检查失败的三项 `NodeNext` 编译选项，同时保留约 300 个文件已添加的显式 `.js` 导入扩展。在类型安全与构建兼容性之间寻求平衡。

### 7. [#41884 fix(core): gate tool snapshot on initial MCP registration](https://github.com/anomalyco/opencode/pull/41884)
修复启动恢复的会话与 MCP 工具注册之间的竞态条件——模型可能在 MCP 工具注册完成前就获取了工具快照，导致工具目录声明为空、模型误以为工具被全部移除。V2 稳定性的关键修复。

### 8. [#41862 feat(tui): hidden experiments section with per-tab prompt drafts](https://github.com/anomalyco/opencode/pull/41862)
新增仅通过输入秘密指令 `/baldbeard` 才能访问的隐藏实验区，用于承载各通道的在途功能，并支持每个标签页独立的 prompt 草稿。为功能孵化提供隔离且可探索的场所。

### 9. [#41838 core: embed models.dev snapshot instead of compile-time define](https://github.com/anomalyco/opencode/pull/41838)
将 models.dev 目录快照以静态文本资源形式内嵌到 core（`snapshot.txt`，原始 `api.json`），取代原先的编译期宏定义。使模型目录更新不再需要重新编译核心包，简化发布流程并支持热更新。

### 10. [#41877 fix(core): parameterize v1 migration messages (Fixes #41869)](https://github.com/anomalyco/opencode/pull/41877)
修复 V1 → V2 数据迁移中因 JSON 负载内的单引号导致的 SQLite 语法错误，改用类型化 Drizzle insert builder 绑定参数。**直接修复今日热点 Issue #41869**，合并后迁移将不再因撇号崩溃。

---

## 功能需求趋势

- **V2 功能对齐与修复 🔴 最紧迫**：大量 Issue/PR 聚焦 V2 与 V1 的功能对齐缺口——模式切换对模型不可见（#40474）、Plan Mode 执行限制失效（#41476、#40778）、webfetch 回归（#41777）、迁移失败（#41869），以及 API 缺口阻塞第三方客户端移植（#41828）。V2 的稳定性和功能完整性是目前社区最强烈的呼声。
- **TUI 交互精细化**：多个 PR 着力改进 TUI 可用性——`/cd` 目录自动补全（#41870）、标签页加号按钮（#41887）、运行中 shell 输出对齐（#41880）、write 工具完成后显示文件内容（#41883）、隐藏实验区（#41862）。桌面级交互体验是持续演进方向。
- **多会话/多工作区支持**：共享服务器下多 TUI 的状态串扰（#39181、#41839）和 Chrome 风格标签页多会话管理（#12548）表明社区对并行工作流的支持有迫切需求。
- **新模型与提供商支持**：Zen 提供商下 gpt-5.6 系列模型 403 错误（#39831）、Grok 4.5 在 Go/Zen 计划不可用（#41886）、AgentRouter (OpenAI Compatible) 提供商 401/内容拦截（#41873）——新模型接入和提供商兼容性是持续关注点。
- **开发者工具链集成**：VS Code 通知（#39936）、GitHub PR 追踪插件（#41857）、Lumify MCP 服务器文档（#41822）、Termux 一键安装脚本（#41695）——丰富 IDE 和移动端生态是社区积极贡献的方向。

---

## 开发者关注点

- **`apply_patch` 的健壮性受到质疑**：Windows 下行尾错乱（#37090）、`add` 可覆盖已有文件（#41875）、多文件变更中途失败无回滚（#41871），以及对文件系统变更缺乏事务性保证——多个独立报告指向同一工具的边界条件缺陷，极可能是高优修复目标。
- **隐蔽的静默失败模式**：web/server 模式下 skills 被静默丢弃（#41751）、多 TUI 共享服务器时 git 分支串扰（#41839）、webfetch 返回 null 但不报错（#41777）——“无报错但行为错误”是开发者最难以排查的问题类型。
- **V1 → V2 迁移稳定性**：单引号导致的 SQLite 语法错误（#41869）在每次服务器启动时都会触发，完全阻断迁移流程——迁移路径的健壮性需要更多测试覆盖（现已由 #41877 修复）。
- **测试效率优化获得认可**：#41879 将 72.5 秒的生命周期测试降至 4.5 秒，社区对 CI 提速的 PR 普遍持积极态度，反映了大型项目对构建时延的敏感。
- **Windows 与跨平台行为一致性**：行尾处理（#37090）和系统级静默安装支持（#9995）表明 Windows 用户的体验差距是长期痛点，需要更多平台特定的适配工作。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-12

> 数据来源：github.com/badlogic/pi-mono（现 earendil-works/pi）

---

## 今日速览

昨日夜间至今日凌晨，Pi 项目迎来一轮密集的 Issue 清理与合并：共 30+ 条 Issue 被关闭（多为 no-action/untriaged 分类），其中 **GitHub Copilot 登录 429 限流**成为本周最突出的社区痛点（多起 Issue 指向同一根因）。PR 方面，**Mermaid 图表渲染**（TUI 与 HTML 导出）和**流式事件中 usage 字段丢失**的修复是当前最活跃的开发主线。此外，**Qwen Token Plan 中国区个人订阅** Provider 已提交 PR，标志着对国内模型的进一步支持。

---

## 社区热点 Issues（10 条）

### 1. [#7730] Mac OS 长会话高 CPU 占用（100%+）
- **作者**: gterzian | 更新: 08-11 | 评论: 10 | 👍: 8
- **为什么重要**: 最高赞的开放式 Bug，CPU 在 50-110% 间摆动，内存 600-800MB，疑似与会话上下文长度线性相关。性能问题直击开发者日常体验。
- **链接**: https://github.com/earendil-works/pi/issues/7730

### 2. [#7850] GitHub Copilot 登录 429 限流（组织账号 20+ 模型时必现）
- **作者**: tuunit | 更新: 08-11 | 评论: 7 | 👍: 7
- **为什么重要**: 与 #7428 为同一根因（组织拥有大量已激活模型时，模型列表请求触发 GitHub 限流）。已关闭为 no-action，但社区呼声很高，是当前 Copilot 登录失败的首要原因。
- **链接**: https://github.com/earendil-works/pi/issues/7850

### 3. [#7846] 0.84.0/0.84.1 在 Bun 运行时下无法启动
- **作者**: and1truong | 更新: 08-11 | 评论: 10 | 👍: 1
- **为什么重要**: `zlib.createZstdDecompress is not a function` — Bun 运行时缺少 Node.js 的 Zstd 解压 API 导致崩溃。已关闭，但暴露了运行时兼容性测试缺口。
- **链接**: https://github.com/earendil-works/pi/issues/7846

### 4. [#6187] WSL 下 Pi 登录挂起（GitHub Copilot 设备授权后不返回）
- **作者**: makoit | 创建: 06-30 | 更新: 08-11 | 评论: 25
- **为什么重要**: 历时最长的老 Issue（42 天），WSL 环境中浏览器设备授权完成后客户端无法感知。评论区有 25 条讨论仍未解决，是 WSL 用户的首要痛点。
- **链接**: https://github.com/earendil-works/pi/issues/6187

### 5. [#7553] Compaction 无法独立配置思考级别/模型
- **作者**: Saolence | 更新: 08-11 | 评论: 8
- **为什么重要**: 功能需求，自动/手动 compaction 无条件复用当前会话的 thinking 级别，导致推理模型上摘要的思考预算无法与正常对话分离。对成本敏感用户非常重要。
- **链接**: https://github.com/earendil-works/pi/issues/7553

### 6. [#7444] WebSocket 重试仅处理两种错误码，其他 transient 错误直接中断回合
- **作者**: lkraider | 更新: 08-11 | 评论: 8
- **为什么重要**: 代码审查发现的架构缺陷 — 只有 `previous_response_not_found` 和 `websocket_connection_limit_reached` 会触发重试，其他 `response.failed` 直接抛异常终止整个回合。
- **链接**: https://github.com/earendil-works/pi/issues/7444

### 7. [#7836] Edit 模糊匹配忽略空白长度差异
- **作者**: robjgray | 更新: 08-11 | 评论: 6 | 👍: 1
- **为什么重要**: `normalizeForFuzzyMatch` 不压缩连续空白，小模型生成的 edit 因空白不一致导致匹配失败。

### 8. [#7911] 0.84.0 delta-only `message_update` 导致 wire 协议丢失 mid-run `usage` 
- **作者**: underactive | 更新: 08-11 | 评论: 2
- **为什么重要**: 修复 #7290 时连同 `usage` 字段一并删除，导致 JSON/RPC 协议在 `message_end` 前无法获取 token 用量。**已有对应 PR #7982**，属进行中问题。
- **链接**: https://github.com/earendil-works/pi/issues/7911

### 9. [#7739] 设置启动时预算：对标 jcode 的延迟与内存
- **作者**: 1am2syman | 更新: 08-11 | 评论: 2
- **为什么重要**: 社区开始拿 Pi 与 jcode（一个 Rust 编写的编码代理）做基准对比，要求量化启动性能差距（jcode 基准表显示 Pi 0.62.0 在 PTY 启动延迟上明显落后）。
- **链接**: https://github.com/earendil-works/pi/issues/7739

### 10. [#7966] `--thinking` 命令行参数无效
- **作者**: felixendres | 创建: 08-11 | 更新: 08-11 | 评论: 3
- **为什么重要**: 新发现的 CLI 参数 Bug，`pi --thinking off` 不生效，沿用上次会话的 thinking 模式。影响脚本化/自动化调用场景。

### 11. [#7947] 【P0】CMD 下重复输出、内存泄漏
- **作者**: MarchBeta2087 | 更新: 08-11 | 评论: 2
- **为什么重要**: Windows CMD 环境下输出的 0 不断重复累加，Ctrl+C 无法中止，属于严重稳定性问题（P0 标记）。
- **链接**: https://github.com/earendil-works/pi/issues/7947

### 12. [#7938] OpenRouter 路由 Anthropic 模型失败：`cache_control` 多余参数
- **作者**: tbrandenburg | 更新: 08-11 | 评论: 3
- **为什么重要**: `anthropic-messages.js` 无条件附加 `cache_control` 到 tools 数组中的最后一个工具，但 OpenRouter 的 Anthropic 端点拒绝该字段，导致所有经 OpenRouter 的 Anthropic 模型不可用。
- **链接**: https://github.com/earendil-works/pi/issues/7938

---

## 重要 PR 进展（10 条）

### 1. [#7982] fix(coding-agent): preserve usage in streaming events
- **作者**: christianklotz | 状态: OPEN | 更新: 08-11
- **内容**: 在 JSON/RPC 的 `message_update` 事件中恢复累计 usage 字段，同时保持流大小线性（继续省略完整消息快照），关闭 #7911。已含回归测试。
- **链接**: https://github.com/earendil-works/pi/pull/7982

### 2. [#7989] feat(ai): add Qwen Token Plan Individual CN provider
- **作者**: bigoldcat123 | 状态: OPEN | 更新: 08-12
- **内容**: 新增通义千问 Token Plan 中国区个人订阅 Provider（cn-beijing 端点），复用 `QWEN_TOKEN_PLAN_CN_API_KEY`。镜像 #7659，关闭 #7847。国内用户可直接使用官方订阅，无需第三方中转。
- **链接**: https://github.com/earendil-works/pi/pull/7989

### 3. [#7984] fix(coding-agent): update grok-mermaid to 0.2.3
- **作者**: xl0 | 状态: OPEN | 更新: 08-11
- **内容**: 升级 grok-mermaid，修复 Mermaid 类图渲染问题（关闭 #7832），配图对比展示修复前后效果。
- **链接**: https://github.com/earendil-works/pi/pull/7984

### 4. [#7956] feat(coding-agent): render Mermaid diagrams in HTML exports
- **作者**: aliou | 状态: OPEN | 更新: 08-11
- **内容**: HTML 导出复用 TUI 的 Mermaid 渲染逻辑，将 ANSI 翻译为 HTML。默认折叠，可通过表头切换展开。补齐了 TUI 有图、导出无图的体验落差。
- **链接**: https://github.com/earendil-works/pi/pull/7956

### 5. [#7978] fix(edit): normalize single-object edits + collapse whitespace in fuzzy match
- **作者**: re2zero | 状态: CLOSED | 更新: 08-11
- **内容**: 合并两项修复：(1) `edits` 为单个对象或 JSON 字符串时归一化为数组；(2) 模糊匹配前折叠连续空白。直接关闭 #7836 与 edit 参数格式兼容问题。
- **链接**: https://github.com/earendil-works/pi/pull/7978

### 6. [#7972] fix(tui): route selection copy through the host clipboard
- **作者**: Panoplos | 状态: CLOSED | 更新: 08-11
- **内容**: 修复 `TuiAltScreen.copySelectionToClipboard()` 裸发 OSC 52 却无条件显示 “Copied!” 的误导行为。对不支持 OSC 52 的终端（macOS Terminal.app、GNOME Terminal 等）改为走宿主剪贴板，确保提示真实。
- **链接**: https://github.com/earendil-works/pi/pull/7972

### 7. [#7970] feat(coding-agent): Show when the fullscreen transcript is scrolled up
- **作者**: pablasso | 状态: OPEN | 更新: 08-11
- **内容**: 全屏模式下，当转录文本不在底部时，状态栏显示 `↓` 指示器；滚回底部自动消失。提升长会话导航体验。
- **链接**: https://github.com/earendil-works/pi/pull/7970

### 8. [#7968] feat: intercom（会话间实时消息）+ ask_predecessor ghost responder
- **作者**: ksdisch | 状态: CLOSED | 更新: 08-11
- **内容**: 实现双能力组合：`intercom` 扩展（基于文件邮箱通道的会话间实时聊天）+ `ask_predecessor` 幽灵响应器。目标是支持交接问答与协作游戏测试。
- **链接**: https://github.com/earendil-works/pi/pull/7968

### 9. [#7905] fix(config): refine pnpm detection
- **作者**: re2zero | 状态: CLOSED | 更新: 08-12
- **内容**: 修复 `detectInstallMethod()` 将 `$PNPM_HOME` 下任意路径误判为 pnpm 管理的 false positive；同时校验 managed install 状态后再建议更新命令。
- **链接**: https://github.com/earendil-works/pi/pull/7905

### 10. [#7897] fix(coding-agent): inherit subagent session config
- **作者**: virtuald | 状态: CLOSED | 更新: 08-11
- **内容**: Subagent 默认继承当前会话的模型与思考级别，而非跟随“最后一个任意会话”的设置。多会话场景下的行为可预期性大幅提升。
- **链接**: https://github.com/earendil-works/pi/pull/7897

---

## 功能需求趋势

从近 24 小时 Issue/PR 中提炼的社区关注方向：

1. **多模型/多端点覆盖**: Qwen Token Plan 中国区（#7989）、OpenRouter 兼容性修复（#7938）— 社区对国内模型和第三方路由的需求持续上升。
2. **Mermaid 渲染生态补齐**: TUI 已有渲染（#7984 升级），HTML 导出补齐（#7956）— 跨界面渲染一致性成为标配诉求。
3. **终端兼容性深化**: OSC 52 剪贴板真实性（#7972）、tmux 下 Kitty 图形协议直通（#7936）、iTerm2/Ghostty 全屏鼠标行为文档化（#7965）— 社区对终端体验的精细度要求不断提高。
4. **可观测性**: 流式事件的 usage 字段恢复（#7982）、全屏转录滚动指示（#7970）— 用量透明度和会话状态感知是高频诉求。
5. **性能基准化**: 启动延迟对标 jcode（#7739）、长会话 CPU/内存问题（#7730）— 用户开始用具体数字要求性能改进。

---

## 开发者关注点（痛点与高频需求）

- **GitHub Copilot 登录限流（429）**: 组织账号激活 20+ 模型时必现（#7850、#7428），已关闭但无代码修复，社区期待官方给出 workaround 或客户端侧模型列表缓存。
- **WSL 登录挂起**: #6187 已 42 天未关闭，25 条评论无解，是 WSL 用户迁移的最大阻碍。
- **Bun 运行时兼容性**: #7846 说明发布前缺少多运行时矩阵测试，建议 CI 增加 Bun 冒烟测试。
- **Windows 体验粗糙**: CMD 下重复输出/内存泄漏（#7947）、无效 settings.json 静默忽略且报错信息误导（#7829）— Windows 场景需要专门 QA 人力。
- **模型输出适配成本高**: 小模型 edit 空白不匹配（#7836）、单对象/数组参数格式混用（#7978）— 说明模型生态对工具参数格式的宽容度参差，需要更健壮的归一化层。
- **`usage` 数据缺失影响成本追踪**: wire 协议去掉 `usage` 后（#7911），依赖 mid-run 用量做预算控制的集成方（IDE 插件、网关）无法工作。

---

*日报生成时间：2026-08-12 09:00 UTC · 数据窗口：2026-08-11 至 2026-08-12*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-12** | 数据来源：[QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)


## 今日速览

今日社区动态聚焦于 **daemon 会话管理与资源保护** 的系列修复（如大会话恢复超时、内存分配过高、多工作区存储错乱等），同时 **Web Shell 增强**（图片预览、Git 工具、推理控制、Prompt 提交加固）成为 PR 主力。值得关注的是，一个 **高优先级桌面端启动崩溃 bug**（Windows 路径解析失败）已被快速关闭修复，而 **macOS iTerm 闪屏** 和 **Windows 文件链接打开失败** 等跨平台体验问题仍在持续讨论中。此外，社区对 **reasoning effort 的 ACP 配置支持** 的正式落地（v0.21.10）反响积极。


## 版本发布

### v0.21.10

- 通过 session 配置新增 ACP 支持，可将推理强度（reasoning effort）从 Default 调整为 Max（[#8526](https://github.com/QwenLM/qwen-code/pull/8526)）。
- Web Shell 中点击已上传或粘贴的图片，现可在 artifact 中打开预览。
- 附带 live-host v0.1.1 发布。
- 修复 CLI 沙箱运行时探测顺序问题（[#7734](https://github.com/QwenLM/qwen-code/pull/7734)）及 autofix 序列化问题。


## 社区热点 Issues（精选 10 条）

1. **[P1] Daemon 会话恢复超时导致当前会话丢失**
   [Issue #8678](https://github.com/QwenLM/qwen-code/issues/8678) · 7 评论 · 开放中
   大型会话恢复超时被中断会销毁当前会话状态。PR1 已合入（[#8691](https://github.com/QwenLM/qwen-code/pull/8691)），实现了超时契约与可观测性，但完整修复仍需关注。社区反馈积极，属 daemon 核心稳定性问题。

2. **[P1] Windows 桌面版 0.1.0 无法启动（已修复）**
   [Issue #8929](https://github.com/QwenLM/qwen-code/issues/8929) · 2 评论 · 已关闭
   Tauri 启动器将 `\\?\` 前缀路径传给 Node 导致 `EISDIR` 错误。**当天报告、当天关闭**，修复效率获社区认可。

3. **[P2] macOS iTerm 频繁闪屏**
   [Issue #8901](https://github.com/QwenLM/qwen-code/issues/8901) · 4 评论 · 开放中
   选择命令执行选项后回车必现闪屏，影响交互体验。发生在 0.21.8，属 UI 渲染范畴，macOS 用户关注度较高。

4. **[P2] Windows 聊天内文件链接无法打开**
   [Issue #8644](https://github.com/QwenLM/qwen-code/issues/8644) · 4 评论 · 开放中
   盘符冒号被 URL 编码（`d%3A`）导致 VS Code 无法解析。已持续一周，社区催促修复声量渐增。

5. **[P2] Headless 模式下 API 错误被误报为成功**
   [Issue #8920](https://github.com/QwenLM/qwen-code/issues/8920) · 4 评论 · 开放中
   `--output-format stream-json` 下 OpenAI 兼容 API 错误被包装为 success 结果并 exit 0，**严重误导 CI 判断**，自动化场景风险高。

6. **[P2] Daemon 每个 ACP 子进程独占宿主 50% 内存**
   [Issue #8182](https://github.com/QwenLM/qwen-code/issues/8182) · 4 评论 · 开放中
   内存上限按宿主内存计算且不随子进程数划分，多实例场景易 OOM。资源管理敏感用户持续关注。

7. **[P2] 并行 read_file 调用结果被合并**
   [Issue #8940](https://github.com/QwenLM/qwen-code/issues/8940) · 3 评论 · 开放中
   多个并行文件读取结果混为一个块，无法区分内容归属，影响多文件分析场景。

8. **[P2] `--approval-mode`/`--auth-type` 未出现在 `--help` 中**
   [Issue #8897](https://github.com/QwenLM/qwen-code/issues/8897) · 4 评论 · 开放中
   参数实际生效但 help 文档缺失，影响可发现性与脚本使用者。

9. **[P2] 0.21.2 起加载图片即崩溃（回归）**
   [Issue #8957](https://github.com/QwenLM/qwen-code/issues/8957) · 3 评论 · 开放中
   0.21.1 为最后可用版本，0.21.2+ 读图即崩。P2+need-retesting 标签，回归严重度较高。

10. **[P2] 并行 shell 输出截断阈值配置不生效**
    [Issue #8922](https://github.com/QwenLM/qwen-code/issues/8922) · 3 评论 · 开放中
    `tools.truncateToolOutputThreshold` 文档承诺对 Shell 生效，但实现仍用固定 30,000 字符预算。


## 重要 PR 进展（精选 10 条）

1. **[feat] Live Journal 容量自适应增长**
   [PR #8905](https://github.com/QwenLM/qwen-code/pull/8905) · 更新于 08-12
   当轮次超出单会话 live-journal 上限时，daemon 先翻倍扩容再丢弃旧数据，减少中途回放截断。

2. **[fix] 多工作区模式下冷启动加载/恢复使用错误的存储上下文**
   [Issue #8909](https://github.com/QwenLM/qwen-code/issues/8909) 关联 · 更新于 08-11
   `POST /session/:id/load` 未在目标工作区 runtime 的存储上下文中执行恢复关键区，存在数据错乱风险。

3. **[fix] PR 审查流程：增量（delta）审查模式**
   [Issue #8946](https://github.com/QwenLM/qwen-code/issues/8946) · 更新于 08-11
   仅审查自上次 review 以来的新提交，避免重复全量审查，提升审查效率。

4. **[feat] Web Shell：Git diff 数据源与分支切换**
   [PR #8467](https://github.com/QwenLM/qwen-code/pull/8467) · 更新于 08-12
   Changes 视图新增 Uncommitted/Unstaged/Staged/Committed/Branch 对比源，并支持可搜索的分支选择器（autofix/takeover 中）。

5. **[feat] Web Shell：模型专属推理控制**
   [PR #8675](https://github.com/QwenLM/qwen-code/pull/8675) · 更新于 08-12
   内置模型推理控制注册表，端到端贯穿 Core、ACP、daemon、SDK 与 WebShell；首个精确注册为 `qwen3*` 系列。

6. **[feat] 渠道：钉钉 Workspace (DWS) 独立渠道**
   [PR #8937](https://github.com/QwenLM/qwen-code/pull/8937) · 更新于 08-12
   新增 DWS 为内置渠道（保留原钉钉 bot-app 渠道），支持本地 `dws` CLI 认证与 @消息/私聊/群聊。

7. **[fix] Web Shell：Prompt 提交所有权加固**
   [PR #8955](https://github.com/QwenLM/qwen-code/pull/8955) · 更新于 08-12
   在异步宿主准入与延迟会话准备后重新校验 App 生命周期、会话 owner、composer 来源及写门控代次，防止提交错乱。

8. **[fix] 审查覆盖：反向审计新增系统执行建模缺陷层**
   [PR #8956](https://github.com/QwenLM/qwen-code/pull/8956) · 更新于 08-12
   针对 shell/git 防护、沙箱、权限解释器等"外部系统执行建模"类 diff 增加缺陷层视角，提升审查深度。

9. **[fix] 每轮次子代理转录落盘**
   [PR #8839](https://github.com/QwenLM/qwen-code/pull/8839) · 更新于 08-12
   workflow dispatch 每次 `agent()` 调用均写入 `<projectDir>/subagents/<sessionId>/agent-<id>.jsonl`，与 Agent 工具格式对齐。

10. **[fix] 渠道会话生命周期上限（sessionRotation）**
    [PR #8927](https://github.com/QwenLM/qwen-code/pull/8927) · 更新于 08-11
    新增每渠道 `sessionRotation` 选项，支持 `maxTurns`/时间上限，到期后自动新建会话。


## 功能需求趋势

- **Daemon/Server 稳定化（高频）**：会话恢复超时、内存配额、多工作区存储隔离、独立于 workspace 的 standalone 会话（[#8908](https://github.com/QwenLM/qwen-code/issues/8908)）——社区对 `qwen serve` 作为生产级后台服务的诉求强烈。
- **Web Shell 能力补齐**：Git 操作、推理控制、工作流可视化（[#8941](https://github.com/QwenLM/qwen-code/issues/8941)）、后台 Agent 状态展示——Web Shell 正从"终端替代品"转向"完整 IDE 面板"。
- **ACP 深度集成**：reasoning effort 配置（已落地）、调度提示词恢复（[#8837](https://github.com/QwenLM/qwen-code/issues/8837)）、待办：内存保护按子进程数划分。
- **审查与 CI 自动化**：增量审查、bot PR 多事件风暴抑制（[#8945](https://github.com/QwenLM/qwen-code/issues/8945)）、dist 重建警告传播——项目自举的 PR 审查机器人正在快速迭代。
- **新渠道/新模型支持**：钉钉 Workspace、OpenAI Responses API（[#8169](https://github.com/QwenLM/qwen-code/pull/8169)）、Claude 虚线别名与 Opus 5（[#8585](https://github.com/QwenLM/qwen-code/pull/8585)）——渠道扩展与模型兼容持续推进。


## 开发者关注点

| 痛点/需求 | 相关 Issue/PR | 热度 |
|---|---|---|
| **Windows 路径处理**：反斜杠、盘符冒号、`\\?\` 前缀引发多处 bug（VS Code 文件链接、桌面端崩溃） | #8644, #8929 | 高（P2+P2，已修 1 个） |
| **macOS 终端体验**：iTerm 闪屏影响高频操作 | #8901 | 中（P2） |
| **会话恢复数据一致性**：调度消息丢失、存储上下文错乱、恢复超时 | #8678, #8837, #8909 | 高（P1/P2 daemon 系列） |
| **Headless/CI 可靠性**：错误被包装为成功、静默失败 | #8920 | 中（P2，自动化风险） |
| **并行工具调用输出混杂**：多文件读取结果合并、截断阈值失效 | #8940, #8922 | 中（P2） |
| **CLI 文档可发现性**：已支持参数不出现在 `--help` | #8897 | 低（P2） |
| **回归问题**：图片加载崩溃（0.21.2+）、闪屏（0.21.8） | #8957, #8901 | 中-高（回归性质） |

**趋势解读**：Windows 平台兼容性和 daemon 会话管理是当前两大痛点集中区；社区对 Web Shell 的期待从"可用"走向"好用"（Git、工作流可视化）；PR 审查机器人自身的稳定性（并发事件风暴、增量审查）也成为社区关注的新议题。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-08-12** | **数据来源：** [Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI) | **统计周期：** 过去 24 小时


## 今日速览

今日无新版本发布，社区焦点集中在**架构重构推进**与**关键缺陷修复**上。核心事件包括：`subagents` 递归深度越界问题（#5253）已通过 PR #5317 修复并关闭；一个关于宽屏终端输出区域不再自动填充的回归 bug（#5322）被报告并迅速引发讨论；此外，一项名为 **CodeWhale TUI Crate 分解**的大型架构调整（EPIC #5316）正在进行中，预计将影响整个代码库结构。


## 社区热点 Issues

过去 24 小时内共有 3 个 Issue 被更新，按重要性排列如下：

**1. EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)** | [#5316](https://github.com/Hmbown/CodeWhale/issues/5316)
- **作者/状态：** aboimpinto / OPEN
- **核心内容：** 这是一个大型架构重构的**总追踪 Issue**，旨在将现有的单一 CodeWhale TUI Crate 拆分为多个独立子 crate。该 EPIC 将作为所有子任务（Sub-EPIC 和 FEAT）的汇总节点，所有相关 PR 均需在此登记。
- **重要性：** ⭐⭐⭐⭐⭐ **近期最重要的架构调整。** 此重构将影响模块边界、编译时间、以及第三方贡献者的开发体验，是项目中期演进的关键里程碑，适合深度关注或参与。

**2. [bug] Regression: output area doesn't fill wide terminals (worked in v0.8.65)** | [#5322](https://github.com/Hmbown/CodeWhale/issues/5322)
- **作者/状态：** M-Maciej / OPEN
- **核心内容：** 用户在升级至 v0.9.x 后，发现输出（Transcript）区域不再自动扩展以填充宽屏终端的空白区域（v0.8.65 中可正常工作）。输出内容被限制在最大宽度内，导致宽屏下文本拥挤、空白浪费。
- **重要性：** ⭐⭐⭐⭐ **明确的用户痛点。** 作为 UI 渲染的视觉回归，该问题直接影响大量使用宽屏/超宽屏开发者的使用体验。Issue 已获得 1 条评论，属于优先级较高的体验类缺陷。

**3. [bug] bug(subagents): nested max_depth can widen the root session depth budget** | [#5253](https://github.com/Hmbown/CodeWhale/issues/5253)
- **作者/状态：** cacdcaecawae / **CLOSED**
- **核心内容：** 一个深层的递归漏洞：子代理（subagent）在嵌套生成时，可以通过显式指定 `max_depth` 参数绕过根会话的递归预算限制，从而无限加深调用链，导致资源耗尽风险。
- **重要性：** ⭐⭐⭐⭐ **高危逻辑漏洞，已修复。** 该问题揭示了配置继承机制中的边界缺失，由 PR #5317 针对性修复并已合入关闭。对稳定性要求高的用户建议尽快升级。


## 重要 PR 进展

过去 24 小时内共有 7 个 PR 被更新，分类汇总如下：

**新功能类**

**1. feat(tui): pin host terminal window as an always-on-top mini window** | [#5318](https://github.com/Hmbown/CodeWhale/pull/5318)
- **作者/状态：** SparkofSpike / OPEN
- **核心内容：** 为 Windows 平台增加 **画中画 (PiP)** 模式：通过右键菜单或 `/pin` 命令，可将宿主终端窗口缩小为 640x400 的悬浮置顶小窗，方便用户在使用其他 IDE 或浏览器时随时查看 TUI 输出；再次触发可恢复原窗口大小。
- **社区意义：** “浮窗模式” 显著增强了多任务处理场景下的使用体验，是对桌面端用户体验的一次有效扩展。

**2. feat: register OrcaRouter as a named provider** | [#5321](https://github.com/Hmbown/CodeWhale/pull/5321)
- **作者/状态：** XiaoHuo888-hue / OPEN
- **核心内容：** 将 **OrcaRouter**（一个 OpenAI 兼容网关，提供 150+ 模型接入）以命名供应商的形式集成到现有 Provider 体系中，与 OpenRouter 的接入方式保持一致，确保模型选择器、配置参考及文档的连贯性。
- **社区意义：** 满足开发者对更多模型路由和聚合服务的需求，特别是需要低成本访问多种模型的用户。

**缺陷修复类**

**3. fix(session): separate snapshot reads from crash recovery** | [#5320](https://github.com/Hmbown/CodeWhale/pull/5320)
- **作者/状态：** h3c-hexin / OPEN
- **核心内容：** 将 **会话快照读取** 与 **崩溃恢复** 两个逻辑分离：新增 `load_session_snapshot` 用于无副作用的读取（避免在工具调用进行中时的竞态）；新增 `recover_session_for_resume` 用于在明确的进程/引擎重启后执行恢复，并返回修复统计信息。
- **社区意义：** 提升会话管理的健壮性和安全性，为嵌入宿主提供更精细的控制粒度，有助于降低数据损坏风险。

**4. fix(tui): copy messages without visual rails** | [#5319](https://github.com/Hmbown/CodeWhale/pull/5319)
- **作者/状态：** XhesicaFrost / OPEN
- **核心内容：** 修复复制消息格式异常问题：对于 User 和 Assistant 消息，复制时将使用**规范化的源内容**（而非渲染后的 Ratatui 行，包含视觉装饰字符）；对于 Tool、Thinking 等复杂类型，保留原有的全转录路径，确保复制内容干净可读且不丢失信息。
- **社区意义：** 提升开发者复制代码块或对话内容时的效率，避免将 UI 元素误复制进剪贴板。

**5. fix(subagents): cap nested max_depth by inherited budget** | [#5317](https://github.com/Hmbown/CodeWhale/pull/5317)
- **作者/状态：** ousamabenyounes / **CLOSED**
- **核心内容：** 针对 Issue #5253 的修复：在子代理 `max_depth` 计算逻辑中，对显式传入的深度值与继承的绝对预算取最小值（`inherited.min(..)`），从而阻止嵌套代理越权增加递归深度。
- **社区意义：** **高优先级安全修复**，已合入主线。保护了系统免受因配置不当导致的意外深度递归攻击。

**其他更新**

**6. [dependencies, github_actions] build(deps): bump docker/login-action from 4.5.2 to 4.6.0** | [#5277](https://github.com/Hmbown/CodeWhale/pull/5277)
- **作者/状态：** dependabot[bot] / OPEN
- **核心内容：** 常规依赖更新：将 GitHub Actions 中的 `docker/login-action` 从 4.5.2 升级至 4.6.0。
- **社区意义：** 例行维护，无额外功能变化。

**7. feat(acp): expose file/search/git/patch/shell tools over session/prompt** | [#5225](https://github.com/Hmbown/CodeWhale/pull/5225)
- **作者/状态：** rafaelcavalheri / **CLOSED**
- **核心内容：** 重大功能扩展：此前 ACP（Agent Client Protocol）服务器的 `session/prompt` 仅传输模型文本，无法执行模型请求的工具调用。该 PR 补全了该能力，现在可以通过 ACP 协议驱动完整的代码编辑、文件搜索、Git 操作、补丁应用及 Shell 执行能力。
- **社区意义：** **生态关键更新。** 该改动将 CodeWhale 从一个“聊天工具”升级为真正可编程的代理核心，Zed 编辑器或第三方适配器（如 `acp-deepseek-adapter`）将因此获得完整的代码操作能力，极大地扩展了使用边界。


## 功能需求趋势

从近期所有 Issue 和 PR 中提炼的社区最关注的功能方向：

1. **架构现代化（Sub-Crate 分解）**：这是一个明确的信号——在功能迭代到一定程度后，社区开始推动**代码模块化与可维护性**的建设，通过多种粒度（EPIC/FEAT）协作来管理复杂度。
2. **ACP（Agent Client Protocol）协议增强**：社区正积极将 CodeWhale 打造为一个**开放的编程代理引擎**，着力完善与编辑器（Zed）及第三方桥接工具的兼容性与能力边界。
3. **终端 UI 体验优化**：围绕宽屏适配与内容复制格式的 Issue，反映出用户对**终端渲染细节和日常交互效率**的挑剔与高要求。
4. **模型服务扩展（Provider）**：持续集成如 OrcaRouter 等新供应商，体现社区对**模型可选择性**和**接入灵活度**的持续需求，期望降低模型切换成本。

## 开发者关注点

1. **宽屏终端适配（回归问题）**：**“为什么我之前能用的功能现在又不行了？”** 这几乎是最容易引发开发者负面反馈的问题之一。需要维护团队在 UI 重构时更加注意回归测试，尤其是不同终端尺寸的适配场景。
2. **Bug 修复的及时性与深度**：对于 #5253 这类由显式参数覆盖引发的配置越界问题，核心关注点在于**配置继承链的严谨性与安全**。修复方案（对显式参数也做预算下限约束）值得在类似场景（如并发、资源限制）中推广应用。
3. **AI 工具链条的安全边界**：ACP 暴露文件/Git/Shell 操作是一把双刃剑。开发者必然关注如何**安全、审计并约束**这些高权限操作，避免代理误触发危险命令。后续可能有针对 ACP 工具的权限沙箱或确认机制的讨论。

---
**日报结束。** 本报告由 AI 自动生成，旨在高效汇总关键信息，不构成技术建议。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*