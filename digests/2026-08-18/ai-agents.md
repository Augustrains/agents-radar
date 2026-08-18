# OpenClaw 生态日报 2026-08-18

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-18 00:29 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-18

## 1. 今日速览

OpenClaw 在过去 24 小时保持了极高的社区活跃度，共产生约 1,000 条 Issue/PR 更新（各 500 条），但大部分集中在待处理状态：Issues 中 484 条仍处于活跃状态，仅 16 条关闭；PR 中 382 条待合并，118 条已合并/关闭。今日无新版本发布。值得关注的是，近期提交的 PR（#125471、#125472、#125473、#125474 等）大量来自核心维护者，围绕 Web UI 设计语言统一、CLI 端口兼容性和 Workboard 生命周期等问题——显示项目在功能推进之外也在积极进行体验打磨。但与此同时，多个 P1 级稳定性 Issue（#91009、#62505、#51429）积压超过两个月仍未修复，说明维护者精力可能更多倾注于新功能而非存量缺陷清偿，项目整体处于"高活跃、高积压、低发布"的状态。

## 2. 版本发布

今日无新版本发布或预发布。

## 3. 项目进展

今日合并/关闭的 118 个 PR 中，较重要的包括：

- **安装策略警告确认机制落地**（#120900 已关闭、#116489 已关闭）：`plugins.install` 新增可选的 `acknowledgeInstallPolicyWarning: true` 参数；外部 `security.installPolicy` 命令可返回 `warn`，要求操作者确认有风险的插件/技能安装。这是安全边界的重要加固。
- **CLI 凭据泄露修复**（#124714 已关闭）：格式错误的 `--provider-env` 条目不再在配置解析错误中回显完整赋值（含凭据材料），配置审计 argv 快照也保留合法值。安全相关的及时修复。
- **macOS Peekaboo 版本钉定**（#125464 已关闭）：将 macOS 包中依赖的 Peekaboo 从预发布 commit 更新至最终 4.2.1 发布源，确保 elevation host 与已签名发布一致。
- 另外两个已关闭 PR（#116489、#120900）共同完成了 install policy warning 的 CLI + UI 双端覆盖。

**核心信号**：今日合并重点集中在安全边界加固和 macOS 构建一致性，说明了维护者对供应链安全和凭据保护的投入。

## 4. 社区热点

今日讨论最活跃的 Issues（按评论数排序）：

- **[#77598 — Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)**（23 评论）：对 Pash 开发代理的 24 小时观察性监控运行笔记，属于社区驱动的发展过程追踪，体现了项目较高的透明度和社区参与文化。
- **[#91009 — Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)**（20 评论，👍2）：Codex 集成导致 `openclaw-hooks` 进程 CPU 占用 100%+ 并阻塞 gateway RPC，已标记为 P1 且需要产品决策。
- **[#68596 — Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596)**（15 评论，👍8）：用户请求为流式看门狗超时阈值提供可配置选项，反映 DeepSeek-R1 等推理模型在扩展思考期间频繁触发误报的痛点。👍8 说明这是一项具有广泛共鸣的功能请求。

**热点分析**：社区讨论高度集中在 **Codex 集成稳定性**（#91009）和 **推理模型的流式超时适配**（#68596），并且二者存在交叉（Codex agent 常与长推理模型配套使用）。用户对长思考模型的支持意愿强烈（👍8 是最高的功能类赞数之一），但 P1 标签和"needs-product-decision"的标记表明该问题已在维护者视野中，等待产品层面拍板。

## 5. Bug 与稳定性

今日报告和活跃的 Bug（按严重程度排序）：

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| P1 | [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex hook relay 产生 CPU 密集进程，阻塞 gateway RPC | 无 fix PR，需产品决策 |
| P1 | [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent 完全不完成任务（2026.4.2 及更早版本正常） | 无 fix PR，需产品决策 |
| P1 | [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026.3.2 版本 google-vertex/gemini-3.1-pro-preview 报 "Cannot convert undefined or null to object" 回归 | 需要 live repro，无 fix PR |
| P1 | [#51429](https://github.com/openclaw/openclaw/issues/51429) | 工作路径被 hardcode 为 `/Users/wangtao` 并合入发布 | 需产品决策，社区反应强烈 |
| P1 | [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败可导致 agent 卡死数小时，无告警 | 无 fix PR |
| P1 | [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后 write/exec 工具参数被静默丢弃 | 无 fix PR |
| P1 | [#78493](https://github.com/openclaw/openclaw/issues/78493) | `sudo openclaw update` 可产生混合文件属主，doctor 覆盖配置 | 无 fix PR |
| P1 | [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程泄漏，僵尸进程累积导致运行时劣化 | 无 fix PR |
| P2 | [#107814](https://github.com/openclaw/openclaw/issues/107814) | gpt-5.3-codex-spark 对必需参数的 tool call 发出空参数对象 | 无 fix PR，仅 7 评论 |

**观察**：今日没有新报告的高严重度 Bug，但上述 P1 级问题全部处于 "needs-maintainer-review" 或 "needs-product-decision" 状态且无 fix PR，已持续数周至数月。其中 **#51429（hardcode 工作路径）** 和 **#97616（进程泄漏）** 属于"人人都该遇到但迟迟未修"的典型，积压风险较高。

## 6. 功能请求与路线图信号

今日讨论中的功能请求相对集中在以下方向，结合已有 PR 可推断：

- **Watchdog 超时可配置**（[#68596](https://github.com/openclaw/openclaw/issues/68596)）— 长推理模型适配需求旺盛（👍8），可能纳入下一版本配置项改进。
- **多 Agent 运维体验相关**（[#67413](https://github.com/openclaw/openclaw/issues/67413) 按 agent 配置 dreaming、[#71058](https://github.com/openclaw/openclaw/issues/71058) 多 Teams bot 支持）— 与当前多智能体网关定位一致的深耕方向。
- **Control UI 功能补齐**（[#42840](https://github.com/openclaw/openclaw/issues/42840) MathJax/LaTeX 渲染（👍10）、[#71142](https://github.com/openclaw/openclaw/issues/71142) 上传大小限制、[#75947](https://github.com/openclaw/openclaw/issues/75947) UI 质量重构）— 今日维护者密集提交了多个 UI 相关 PR（#125472、#125473、#125471），且与这些请求方向一致。**LaTeX 支持（👍10）** 是最受社区欢迎的 UI 功能。
- **YAML 配置格式支持**（[#45758](https://github.com/openclaw/openclaw/issues/45758)）— 未被标记为维护者关注，但 9 评论、👍2，反映了一部分用户对 DevOps 工具链一致性的偏好。

**路线图推断**：今日维护者的 UI PR 集中提交表明 Control UI 正在经历一轮系统性重构，MathJax、上传限制、RTL 修复（#68105，P2 但已有具体分析）可能随 UI 重构一并解决。YAML 配置和 i18n（#79458）属于长期功能增强，短期纳入概率低。

## 7. 用户反馈摘要

从今日活跃 Issues 的评论中提炼的用户声音：

- **对长上下文/推理模型支持仍不满意**：#68596 作者明确指出 kimi-k2.5、DeepSeek-R1 等模型触发 watchdog 误报是高频痛点（"frequently triggers warnings"）；#67419 反映 bootstrap 文件每轮注入浪费 20-30% token，直指上下文成本问题。
- **对回归问题容忍度下降**：#62505（Coding Agent 完全失效）和 #51429（hardcode 路径）在评论中表现出明显的挫败感——前者"worked for weeks and now just doesnt do anything"，后者以反问语气质疑代码审查流程（"Apparently some wangtao hardcode his working space path into the code and somebody merged his code and published"）。
- **对透明度的认可与期待并存**：#77598 的 24 小时开发代理观察帖获得 23 条评论，说明社区对开发过程透明化有真实兴趣，但也可能希望通过围观推动质量问题解决。
- **本地化诉求逐渐浮出**：#79458 是今日唯一明确的中文用户 i18n 请求，提出 slash 命令描述仅有英文；#51429 的 hardcode 路径问题也来自中文用户（wangtao 路径）。中文社区的规模和使用场景被进一步验证。

## 8. 待处理积压

以下为需要维护者重点关注的长尾问题：

- **[#51429 — 工作路径被 hardcode](https://github.com/openclaw/openclaw/issues/51429)**：P2 行为 Bug，3 月 21 日即报告，已 5 个月未修复，社区信任成本较高。
- **[#62505 — Coding Agent 完全失效](https://github.com/openclaw/openclaw/issues/62505)**：P1 回归，4 月 7 日报告，4 个月以上的 P1 积压，对核心用户场景影响大。
- **[#38327 — Gemini 3.1 pro preview "Cannot convert undefined or null to object"](https://github.com/openclaw/openclaw/issues/38327)**：P1 回归（3 月 6 日），影响 Google Vertex 用户，已 5 个月未解决且无 fix PR。
- **[#70903 — 持久化 provider cooldown 阻断用户](https://github.com/openclaw/openclaw/issues/70903)**：P0 标记但已 4 个月未处理（4 月 24 日创建，最近更新 8 月 17 日），用户充值后仍被继续阻断，属收入/体验双重负面场景。
- **[#97616 — 子进程泄漏导致僵尸累积](https://github.com/openclaw/openclaw/issues/97616)**：P1 回归（6 月 29 日），长期运行实例性能持续劣化，但被标记为 needs-info、未获 fix PR。
- **长期无回应的 PR 信号**：@jjjhenriksen 提交的 #123871（8 月 14 日）和 #124429（8 月 16 日）均标注 "needs proof"，且涉及多代理权限展示问题，至今未有维护者表态。

---

*数据窗口：2026-08-17 至 2026-08-18（太平洋时间）。本报告基于 GitHub Issue/PR 元数据自动生成，部分标签和评论摘要由分析推断得出，仅供参考。*

---

## 横向生态对比

# AI智能体开源生态横向对比分析报告

**报告日期：2026-08-18 | 数据窗口：过去24小时 | 覆盖项目：12个**


## 1. 生态全景

当前个人AI助手/自主智能体开源生态正处于**规模化重构与安全治理并行的关键阶段**。头部项目（OpenClaw、Hermes Agent、ZeroClaw）在保持高活跃度的同时，面临"功能扩张快于缺陷清偿"的结构性挑战——P1级Bug积压普遍超过2个月，而新功能PR持续涌入。与此同时，**安全加固**成为全生态共识：ZeroClaw单日合并5个安全修复、Hermes Agent完成Windows ACL漏洞修复、OpenClaw落地安装策略警告机制。技术路线上，多渠道适配（Slack/Telegram/微信/IRC）、多Agent协作（会话级目录、跨Agent通信）、长推理模型适配（watchdog超时、token成本治理）是三大共同攻坚方向。


## 2. 各项目活跃度对比

| 项目 | Issues（新增/活跃） | PR（合并/待审） | 版本发布 | 活跃度评级 | 健康度评估 |
|------|---------------------|-----------------|----------|------------|------------|
| **OpenClaw** | ~500条更新（16关闭） | 118合并 / 382待审 | 无 | ★★★★★ 极高 | 🟡 高活跃高积压，P1搁置超2月 |
| **Hermes Agent** | 50条更新（18关闭） | 24合并 / 26待审 | v0.20.3 | ★★★★☆ 高 | 🟢 高强度治理期，响应良好 |
| **ZeroClaw** | 50条更新（6关闭） | 16合并 / 34待审 | 无（v0.8.x迭代） | ★★★★☆ 高 | 🟢 安全加固密集，RFC积压可控 |
| **NanoClaw** | 4条更新 | 25合并 / 16待审 | 无（v2.1.48锚定） | ★★★★☆ 高 | 🟡 架构重构期，数据丢失Bug待修 |
| **IronClaw** | 28条更新 | 多合并 / 44待审 | v1.3.0-rc.1 | ★★★★☆ 高 | 🟢 高强度迭代，写路径优化中 |
| **CoPaw** | 14条更新（6关闭） | 22合并 / 13待审 | 无（v2.1.0后） | ★★★★☆ 高 | 🟡 2.x回归问题集中，修复及时 |
| **NanoBot** | 少量更新 | 5合并 / 10待审 | 无 | ★★★☆☆ 中高 | 🟢 Telegram修复落地，积压中等 |
| **PicoClaw** | 3条新增 | 3合并 / 1待审 | 无 | ★★★☆☆ 中 | 🟢 良性推进，新Bug需确认 |
| **Moltis** | 3条更新 | 6合并 / 3待审 | 无 | ★★☆☆☆ 中低 | 🟡 Podman兼容长期未解 |
| **LobsterAI** | 7条（全stale） | 17合并 | 无 | ★★☆☆☆ 中低 | 🟡 合并积极，Bug积压严重 |
| **NullClaw** | 0条 | 0合并 / 1待审（Dependabot） | 无 | ★☆☆☆☆ 静默 | 🔴 维护停滞，依赖更新64天未合 |
| **TinyClaw / ZeptoClaw** | 0条 | 0条 | 无 | ☆ 无活动 | ⚪ 数据缺失 |


## 3. OpenClaw 在生态中的定位

**生态位：事实上的参照基准与最大体量单体仓库。**

- **社区规模断层领先**：单日~1,000条Issue/PR更新（484活跃Issue + 382待审PR），远超Hermes Agent（~100条）和ZeroClaw（~100条），社区活跃度约为第二梯队项目的10倍。其Issue编号已突破#125,000，对比NanoBot（~5,400）、PicoClaw（~3,300），体量差距达1-2个数量级。

- **技术路线差异**：OpenClaw采用**单体仓库+Web UI+CLI+Workboard**的一体化架构，强调"开箱即用"的完整体验；相比之下，Hermes Agent更侧重企业级网关与会话状态管理（SessionDB、企业集群迁移）；ZeroClaw则走向**安全架构重塑+协议兼容**路线（OpenAI Chat Completions兼容RFC已获批），意图成为drop-in替代方案。NanoClaw/IronClaw等衍生项目在架构模块化（driver seam、hook体系）上更进一步。

- **核心矛盾**：OpenClaw的"高活跃、高积压、低发布"状态（今日0版本发布）与其行业标杆地位形成反差。多个P1级稳定性Issue（#91009 CPU耗尽、#62505 Coding Agent失效、#51429 hardcode路径）积压超4个月，而维护者精力集中在UI重构与新功能。反观Hermes Agent，今日即发布v0.20.3汇总125个PR，发布节奏更稳健。

- **差异化结论**：OpenClaw是**生态创新引擎和社区引力中心**，但稳定性和发布节奏不及Hermes Agent/ZeroClaw；其衍生生态（NanoClaw、PicoClaw、IronClaw、CoPaw、LobsterAI）与其形成"核心-外围"结构，各自在特定赛道（嵌入式、硬件、企业QA、本地化）寻找差异化空间。


## 4. 共同关注的技术方向

### ① 安全加固与凭据治理（涉及6+项目）
- **OpenClaw**：CLI凭据泄露修复（#124714）、安装策略警告确认机制
- **Hermes Agent**：Windows ACL漏洞（#77462）、MCP子进程凭据丢失（#77529）、fail-closed策略转换
- **ZeroClaw**：Gemini API密钥URL泄露（#9973）、附件下载无界风险（#10000）、Email隐式文件读取（#9993）
- **LobsterAI**：导出日志明文密钥修复（#1661）
- **共同信号**：供应链安全、密钥管理、权限边界已成为生产级AI助手的基本门槛

### ② 长推理模型适配与Token成本治理（涉及4+项目）
- **OpenClaw**：流式watchdog超时可配置（#68596，👍8）
- **NanoBot**：混合支出防火墙（#5409）、Goal循环Token浪费修复（#5410）
- **IronClaw**：削减DB写入压力（Epic #7591，每轮减少60+行写入）
- **ZeroClaw**：action budget原子化（#9996）
- **共同信号**：DeepSeek-R1/kimi-k2.5等长思考模型普及后，"推理时间不确定性与成本失控"成为全生态共同痛点

### ③ 多渠道适配与统一抽象（涉及5+项目）
- **NanoClaw**：渠道层基础设施大规模落地（Slack wave A/B + 桥接钩子体系）
- **PicoClaw**：微信渠道多实例增强（#2606）、IRC长消息合并（#3287）
- **CoPaw**：OneBot图片URL过期问题（#7088）、多渠道独立模型配置（#7085）
- **OpenClaw**：多Teams bot支持（#71058）
- **共同信号**：从单一渠道向"全渠道统一接入层"演进，渠道适配从硬编码走向模块化声明

### ④ 多Agent协作与记忆管理（涉及4+项目）
- **LobsterAI**：Agent独立工作目录（#1668）、基于MD的工作流（#1644）
- **CoPaw**：会话级多项目目录（#6976）、PowerContext可插拔记忆后端（#7080）
- **Hermes Agent**：委派失败消耗子代理预算（#77305）
- **OpenClaw**：多Agent运维体验（#67413、#71058）
- **共同信号**：单Agent对话向多Agent编排演进，需要更精细的工作区隔离、记忆持久化和预算分配

### ⑤ 协议兼容与生态互操作（涉及3+项目）
- **ZeroClaw**：OpenAI Chat Completions兼容（#8603，23评论）
- **Moltis**：MiniMax Code ACP Agent集成（#1204）
- **IronClaw**：WebSocket/ACP支持（#7513）
- **共同信号**：主流客户端生态（Open WebUI、LobeChat、Copilot CLI等）正在成为新的"必须兼容"标准


## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构关键差异 |
|------|---------|---------|-----------------|
| **OpenClaw** | 全能型个人AI助手平台 | 开发者/技术爱好者/企业试点 | 单体仓库、Web UI+CLI双端、Workboard生命周期 |
| **Hermes Agent** | 企业级Agent基础设施 | 企业用户/团队协作 | 强调网关状态一致性、SessionDB、桌面端（Electron）、企业集群部署 |
| **ZeroClaw** | 安全优先的协议兼容Agent | 安全敏感型企业/协议生态开发者 | 安全架构重塑（RFC驱动）、OpenAI协议兼容、插件化治理 |
| **NanoClaw** | 极简轻量级Agent宿主 | 个人开发者/嵌入式场景 | 模块化渠道层（driver seam、hook体系）、强调可扩展性 |
| **PicoClaw** | 面向硬件/边缘设备 | 嵌入式开发者/硬件爱好者 | 轻量运行时、多平台（macOS/Windows/边缘）、硬件加速集成 |
| **IronClaw** | 高可靠性自动化执行引擎 | 自动化运维/QA团队 | 持久化DB优化（libSQL）、WASM工具契约、自动化确定性结果 |
| **CoPaw** | 多智能体协作平台 | 数据分析师/多Agent工作流 | 会话级目录绑定、DataPaw应用、飞书/钉钉/QQ渠道 |
| **NanoBot** | 轻量网关+Telegram优先 | 个人开发者/Telegram重度用户 | 网关抽象、WebUI、成本治理优先 |
| **LobsterAI** | 本地化/中文场景Agent | 中文用户/企业本地部署 | 微信深度集成、OpenClaw运行时+自研UI、本地模型支持 |
| **Moltis** | Rust高性能Agent运行时 | Rust生态开发者 | 纯Rust实现、Shadow DOM穿透、容器化运行时（Docker/Podman） |


## 6. 社区热度与成熟度分层

### 第一梯队：快速迭代期（高活跃、功能扩张为主）
- **OpenClaw**：日均~1,000条更新，但"高活跃、高积压、低发布"状态需警惕
- **NanoClaw**：核心团队集中交付（gavrielc单日17个PR），架构重构推进迅速，但社区贡献占比偏低
- **IronClaw**：6条XL PR并行推进，Epic驱动的系统化优化，v1.3.0-rc.1已发布

### 第二梯队：质量巩固期（发布稳健、安全治理优先）
- **Hermes Agent**：v0.20.3汇总125个PR，安全修复密集，桌面端批量清理，进入"高强度治理期"
- **ZeroClaw**：安全RFC体系化推进（#7141、#7142、#6971），CI基础设施统一，v0.9.0安全架构大版本酝酿中
- **CoPaw**：v2.1.0后密集修复2.x回归，社区贡献活跃（含首提者），但13条PR等待审查

### 第三梯队：稳定维护期（波动较小、定向修复）
- **NanoBot**：Telegram核心问题修复后转入稳定，社区长尾贡献持续
- **PicoClaw**：良性推进，agent循环修复落地，新Bug（Antigravity 429）需确认
- **Moltis**：功能合入积极（MiniMax、RPC超时），但Podman兼容等长尾问题未解

### 第四梯队：停滞/静默期
- **NullClaw**：24小时零Issue零PR合并，Dependabot PR滞留64天，项目实际进入维护停滞
- **LobsterAI**：PR合并积极但Issue全为stale标记，4个月前的Bug（#1635、#1644）无进展，社区反馈渠道趋冷
- **TinyClaw / ZeptoClaw**：无数据，可能已停止维护或迁移


## 7. 值得关注的趋势信号

### 信号一：安全合规正从"可选加固"变为"生产准入门槛"
ZeroClaw单日5个安全修复、Hermes Agent连续多日安全PR、OpenClaw安装策略警告机制——**各项目不约而同地在同一时间窗口内加强安全边界**，说明整个生态正在响应企业级用户的合规需求。对开发者：**评估任何AI Agent框架时，应优先审查其密钥管理、文件访问控制、子进程隔离三大安全基线**。

### 信号二：长推理模型引发全链路适配重构
DeepSeek-R1、kimi-k2.5等长思考模型的普及，正在倒逼框架层面的系统性调整——watchdog超时配置化（OpenClaw）、Token成本防火墙（NanoBot）、action budget原子化（ZeroClaw）、DB写入削减（IronClaw）。**"推理不确定性与成本不可控"已从单个模型问题演变为框架基础设施问题**。对开发者：选择框架时需关注其是否支持推理时长感知的流式处理和预算熔断机制。

### 信号三：开源Agent正从"模型调用壳"走向"完整生态平台"
协议兼容（ZeroClaw的OpenAI Chat Completions、IronClaw的WebSocket/ACP）、渠道统一抽象（NanoClaw的channel layer）、多Agent编排（CoPaw的会话级目录、LobsterAI的Agent工作区）——**框架间的竞争正从"能用哪些模型"转向"接入多少生态"**。对开发者：框架的协议兼容性和插件生态丰富度将比模型支持列表更重要。

### 信号四：社区对大厂/核心维护者的"单点依赖"风险显现
NanoClaw的gavrielc单日提交17个PR形成堆叠链、OpenClaw的#51429 hardcode路径问题（来自个人开发者wangtao的代码被合入发布）、LobsterAI对OpenClaw运行时升级的依赖（#1663）——**多个项目的健康度与个别核心贡献者的活跃度强相关**。对开发者：评估项目时应关注其bus factor（核心贡献者数量）和代码审查流程的透明度。

### 信号五：中文用户群体成为不可忽视的力量
OpenClaw #51429（中文用户hardcode路径）、LobsterAI的中文文档/微信集成、CoPaw对钉钉/飞书/QQ的支持、OpenClaw #79458中文i18n请求——**中文社区的规模和使用场景正在反向塑造开源项目的功能优先级**。对开发者：面向国内场景的Agent框架选择，应优先考察微信生态集成度和中文模型（Qwen、DeepSeek、GLM）的适配成熟度。


**总结：** 个人AI助手开源生态正处于从"功能竞赛"转向"治理竞赛"的转折点。头部项目凭借社区规模优势持续推进功能创新，但P1积压与发布节奏的矛盾正在积累技术债；第二梯队以安全加固和协议兼容为突破口，有望在企业级市场建立差异化优势；长尾项目则面临维护停滞或社区流失的生存挑战。对于技术决策者，建议优先选择**发布节奏稳健、安全响应及时、社区贡献多元化**的项目作为生产依赖；对于开发者，选择贡献对象时，应关注项目的RFC流程效率和首次贡献者体验，而非仅看Star数和PR总量。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**报告日期**: 2026-08-18 | **数据窗口**: 2026-08-17 至 2026-08-18（24小时）
**数据来源**: [github.com/HKUDS/nanobot](https://github.com/HKUDS/nanobot)

---

## 1. 今日速览

项目在经历了一段活跃的社区长尾贡献期后，于今日迎来一次密集的**核心代码合并潮**：24小时内共15条PR活动，其中5条PR被合并/关闭，主要集中在**Telegram轮询稳定性修复**（含一个跨18天的深度修复）、**网关进程身份管理**、以及**持续目标(Goal)重复注入修复**。社区侧同时涌现出7条新PR（含2条同日提交），来自4位不同贡献者，显示出项目在实现层（网关/Windows兼容）和功能层（WebUI会话/侧边栏）均有持续投入。值得关注的是，Issue #5409提出的"混合支出防火墙"直指商业化转型成本管控痛点，代表了向"AI预算治理"演进的需求信号；此外一个待合并PR #5341（Windows天气技能修复）已滞留8天并标记conflict，需维护者介入。

**活跃度评估**：高（合并活跃期，但需关注问题响应时效与冲突管理）。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的5条PR推动了以下关键改进：

### 核心稳定性
- **[PR #5156] [已合并] fix(telegram): recover from silently stalled polling** — 解决"网络瞬断后Telegram轮询永久静默"的生产级问题，通过重建连接池恢复轮询。该PR直接修复了已关闭的Issue #5171。是一个跨18天（7/29提交，8/17合并）的深度修复，合并后显著降低用户侧"消息堆服务器端"的运营风险。后续配套的[PR #5301]（bridge stdlib logging）也同步合并，补齐了可观测性的一块拼图。
- **[PR #5410] [已合并] fix(goal): stop repeating clarification replies** — 修复"持续目标(Goal)下模型每次回复都触发澄清循环"的回归问题，将续接行为精准限制在实际工具调用预算边界。该PR解决了社区苦不堪言的LLM浪费场景，其影响直接关联到Token成本控制。

### 架构与工具链
- **[PR #5416] [已合并] fix(gateway): stabilize process identities** — 将macOS上依赖`ps lstart`方案升级为`proc_pidinfo`原生调用，统一跨平台（Windows FILETIME/Linux boot time）的进程身份契约，为网关客户端的租约管理打下稳定基础。合并该PR是向生产级跨平台网关迈出的一步。
- **[PR #5406] [已合并] feat(cli): add native TypeScript terminal UI** — 注：该PR实际是合并历史复杂的"恢复合并"事件，重合并了曾被误标merged的#4329，最终带入了完整的终端UI功能。

**整体进展**：项目在半日内同时解决了Telegram这一最活跃渠道的稳定性风险，并完成了CLI迁移，同时在网关底层进程模型上完成了跨平台统一。下一版本将具备更好的生产可用性与可观测性。

---

## 4. 社区热点

### ⭐ 热点 Issue / PR（按互动度排序）

| 排名 | 条目 | 类型 | 互动指标 | 状态 |
|------|------|------|----------|------|
| 1 | [Issue #4864 — Endless loop for tool_call/complete_goal](https://github.com/HKUDS/nanobot/issues/4864) | Bug | 7条评论 / 1👍 / 持续38天未关闭 | 活跃讨论中 |
| 2 | [Issue #5409 — Add a Hybrid Spend Firewall](https://github.com/HKUDS/nanobot/issues/5409) | 功能请求 | 新开1天，已获0评论（但主题极具话题性） | 新开 |
| 3 | [Issue #5171 — Telegram polling stalls silently](https://github.com/HKUDS/nanobot/issues/5171) | 严重Bug | 已关闭（由PR #5156修复） | 已解决 |

**分析**：
- **#4864** 是当前社区最集中的痛点聚焦点，讨论围绕"工具调用参数被错误序列化"（bare string vs JSON）导致死循环。该问题涉及核心AgentRunner逻辑且跨越多个版本，至今未被修复，而今天合并的PR #5410（goal修复）或许部分缓解症状，但#4864的根因在gateway的序列化层，值得维护者将两个问题关联起来定位。评论区热度高，表明用户在实际生产环境中的受挫感强烈。
- **#5409** 虽是新开Issue，但其诉求——"为LLM支出加防火墙"——直接呼应了今日多项与成本相关的修复（#5410、#5407）。这一信号值得关注：商业化用户在投入真金白银后，对"无限循环烧钱"的恐惧正成为决策障碍。

---

## 5. Bug 与稳定性

### 🚨 严重（影响生产运行）

1. **Telegram轮询永久静默（#5171）** — 已解决 ✅
   - 现象：网络瞬断后，进程存活但轮询永久停止，消息堆积在服务器端。
   - 影响：用户完全失联，且无日志线索。
   - 处理：PR #5156已合并修复；配套PR #5301补充日志链路，今日一并合入（长期修复闭环）。

### ⚠️ 中等（影响部分场景）

2. **complete_goal死循环（#4864，OPEN）** — 未解决 ⚠️
   - 现象：gateway解析recap参数为裸字符串而非JSON对象，导致complete_goal反复报错触发重试并陷入无限循环。
   - 影响：消耗Token且拖垮Agent响应。
   - 风险：与今日合并的PR #5410相关（#5410修复的是模式重复澄清循环，而#4864是序列化错误导致的死循环），两者可能互相纠缠。已合并的PR #5410并未解决该bug的根因——**该问题已持续38天，亟需排查gateway的参数序列化逻辑**。

3. **Windows venv子进程采纳（PR #5415，OPEN）** — 修复中
   - 现象：Windows上使用uv/venv启动网关时，进程PID记录失败导致生命周期管理失效。
   - 处理：chengyongru已提交PR #5415，有对应回归测试，待合并。

### 🔹 低危（修复排队中）

4. **cron系统任务失效（PR #5407，OPEN）** — 修复排队
   - 现象：设置`gateway.heartbeat.enabled: false`后重启，持久化在cron/jobs.json的系统任务仍在运行并烧钱。
   - 处理：PR #5407提交中，功能修复明确（补全"禁用时清理"逻辑）。

---

## 6. 功能请求与路线图信号

### 与已有PR呼应的功能请求 → 可能纳入下一版本

- **支出防火墙（Issue #5409）** — 尚无直接PR对应，但社区已感知到成本失控痛点。同期合并的PR #5410（停止重复澄清）正是支出治理的一个局部修补。**推测**：类似"预算上限"、"调用配额"、"沙箱循环熔断"等防御机制有望在商业化版本中优先纳入。
- **会话提及（PR #5358，OPEN）** — 为WebUI会话提供稳定`@name`，并支持会话间消息传递，这是协作式Agent工作流的基础能力（类似Slack的线程/提及模型），已在PR中排队，预计进展顺利。
- **临时侧边栏会话（PR #5364，OPEN）** — 支持`/side`开启临时会话且不污染主线上下文，**该交互模式与DeerFlow（用户引用的竞品/参考项目）对齐**，反映了对灵活多任务的深刻需求。已进入草案阶段（含conflict标签），保留性较强。

### 因无对应PR而视为远期信号的请求

- **SPEND治理**（见上） — 无直接对应PR，但回调了今天多个PR（#5407、#5410）共同指向的"减少无效消耗"方向，预计会引起维护者注意，列入商业化设计。

---

## 7. 用户反馈摘要

### 从Issues/PR评论中提炼的真实痛点与使用场景

| 来源 | 用户声音 | 深层诉求 |
|------|----------|----------|
| Issue #4864 | "complete_goal keeps erroring because the gateway is parsing the recap parameter as a bare string instead of a JSON object" | 对工具调用的**参数契约稳定性**有极高依赖——一旦序列化改变，整个Agent循环就会失控。这暴露了**gateway作为边界**的脆弱性。 |
| Issue #5171（已关闭） | "bot can stop receiving messages permanently while the process keeps running and the log stays completely silent" | **可观测性是刚需**——静默失败比报错更可怕。修复后，部分用户在评论中反馈"若能提前有WARNING日志，我们就能自行缓解"。 |
| Issue #5409 | "power users running infinite loops and bankrupting your LLM budget" | **对成本失控的焦虑**成为商业用户的头号决策变量，他们期望框架自带"熔断器"。 |
| PR #5341（Windows专家修复） | "On Windows PowerShell, bare `curl` may resolve to the Invoke-WebRequest alias" | 跨平台兼容性虽小但猛，**Windows用户数量在攀升**，社区从"能跑"向"顺手"转变。 |

---

## 8. 待处理积压（⚡ 重点提醒）

### 高危：带冲突且超时的关键PR

- **[PR #5341] fix(skills): make weather workflow Windows-safe**（[链接](https://github.com/HKUDS/nanobot/pull/5341)）
  - 阻塞状态：已标记 `conflict`，等待解决冲突后合入（8/11提交，已超7天）。
  - 建议：维护者需尽快解决冲突或与作者沟通，否则将阻塞后续PR（该PR修改了skills示例代码）。

### 中危：长期未响应的严重Bug

- **[Issue #4864] Endless loop for tool_call/complete_goal**（[链接](https://github.com/HKUDS/nanobot/issues/4864)）
  - 已开放38天，是社区互动最高的活跃issue，无维护者参与记录。
  - 建议：虽PR #5410解决了相近的"重复澄清"问题，但**根因（gateway参数序列化）未被触及**，应优先关联并升级处理。

### 低危：等待review的稳定修复

- **[PR #5415] fix(gateway): adopt Windows venv child process**（[链接](https://github.com/HKUDS/nanobot/pull/5415)）
  - 已提交1天，有回归测试，是明确的Windows平台稳定性修复，可优先review。
- **[PR #5407] fix(cron): retire persisted heartbeat/dream system jobs when disabled**（[链接](https://github.com/HKUDS/nanobot/pull/5407)）
  - 功能修复清晰，，直接阻止"禁用后仍烧钱"的bug，建议尽快合入。

---

**项目健康度评估**：
- 🟢 核心渠道（Telegram）稳定性在今日得到历史性修复，风险显著下降
- 🟡 待合并PR数量积压至10条，其中2条带conflict，需维护者加大审查力度
- 🟢 社区贡献者活跃（今日5位不同贡献者），且分工多元（网关、WebUI、skills）
- 🟡 长期issue #4864缺乏维护者响应，可能演变为社区"意见领袖"的不满根源

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-18

## 1. 今日速览

Hermes Agent 今日保持高度活跃，24小时内共有 **50 条 Issue 更新**（32 条活跃，18 条关闭）和 **50 条 PR 更新**（26 条待合并，24 条已合并/关闭），并发布了补丁版本 **v0.20.3**（汇总约 125 个 PR）。项目当前官方政策为「god-file 一律拆分、绝不回退」，说明大型重构正在全仓库稳步推进。安全修复继续占据重要份额，多个 Windows ACL、子进程凭据继承和网关状态一致性问题获得响应，整体健康度良好。

---

## 2. 版本发布

### Hermes Agent v0.20.3 (v2026.8.16.2)

**发布日期：** 2026-08-16

> Patch release。该 tag 将 v0.20.2 以来合并的约 125 个 PR 汇总为稳定的 tagged release，供下游消费者（Docker 镜像、托管部署、全新安装）使用。

**建议：** 各生产环境用户应计划常规升级窗口，该补丁版本未提及破坏性变更。

---

## 3. 项目进展

### 关键合入/关闭 PR

- **[#27100 或 #35100] `fix(cron): surface media attachment delivery failures`** — 已关闭/合并。cron 定时任务中媒体附件发送失败时，不再被报告为「成功」，并避免在文本已发送后重复发送。已有回归测试。[PR #35100](https://github.com/NousResearch/hermes-agent/pull/35100)

- **[#88753] `fix(gateway,state): SessionDB off the event-loop thread + contention-safe v25 migration`** — 已关闭/合并。修复了企业集群中网关因 v25 schema 迁移在 event-loop 线程上阻塞导致重启死循环的问题（exit 75 崩溃循环）。[PR #88753](https://github.com/NousResearch/hermes-agent/pull/88753)

- **[#88776] `fix(plugins): hide bundled model providers from plugin list`**（salvage #27268）— 已关闭/合并。`hermes plugins list` 不再显示 bundled `model-providers/`，消除误导性的启用/禁用入口（这些服务商实际由 `model.provider`/`--provider` 选择）。[PR #88776](https://github.com/NousResearch/hermes-agent/pull/88776)

- **[#88631] `fix(cron): manual runs no longer silently drop media attachments`** — 已关闭/合并。人工执行 `hermes cron run <job-id>` 时不再丢失 PDF/图片附件；此前定时运行正常但手动运行会「成功但掉附件」。[PR #88631](https://github.com/NousResearch/hermes-agent/pull/88631)

- **[#88773] `docs: unified Gateways page, settings profile scope, plugins cleanup, Bot Mode group rows, host.openWorkspace`** — 已关闭/合并。文档与桌面端五项新变更对齐，包括统一的 Gateways 设置页和新的 `host.openWorkspace` 插件 SDK 门。[PR #88773](https://github.com/NousResearch/hermes-agent/pull/88773)

今日合入的 PR **横跨 cron 可靠性（2 项）、网关会话状态（1 项）、插件列表准确性（1 项）和 Desktop 文档同步（1 项）**。媒体附件投递失败问题今天有 2 个相关修复合并（#35100 与 #88631），反映了对**消息投递完整性**的持续关注。多项修复针对企业级场景（网关崩溃循环、手动 cron 丢件）。

---

## 4. 社区热点

- **[#78647] 大型文件拆分 Epic 验收完成（76 条评论，已关闭）** — 仓库级 god-file 分片大型任务的正式收尾。其「拆分为王、绝不回退」的政策已成为项目硬性标准。[Issue #78647](https://github.com/NousResearch/hermes-agent/issues/78647)

- **[#66616] Skills index 持续降级（48 条评论）** — 自动 freshness probe 报告技能索引已过期 29.8 小时（限制 26h），该问题自 7 月 18 日已存续一个月并多次反弹，说明技能索引重建的 CI 管道稳定性仍待改善。[Issue #66616](https://github.com/NousResearch/hermes-agent/issues/66616)

- **[#84834] Webhook Feature Package meta-issue（17 条评论）** — 由维护者发起的 webhook 全链路修复计划（5×2×3 矩阵），工程量大、涉及面广，是值得关注的路线图信号。[Issue #84834](https://github.com/NousResearch/hermes-agent/issues/84834)

- **[#88706] 安全：关闭 #88232/#88435 背后的 use-time/provenance/authority 缺口（4 条评论）** — 安全问题从单一漏洞转向体系建设，社区关注度正在形成。[Issue #88706](https://github.com/NousResearch/hermes-agent/issues/88706)

**热点诉求归纳：** 今日活跃话题主要围绕**大规模重构纪律化**（god-file 拆分）和**安全收口**（凭据隔离、ACL、会话边界）两大主题。

---

## 5. Bug 与稳定性

### 严重等级排列

#### 🔴 严重（Critical）

- **[#77462] Windows at-rest ACL 漏洞：`_secure_file` 在 Windows 为 no-op** — 已实机验证。Windows 上 secrets 文件对 SYSTEM/Administrators 可读。Cluster W-ACL 共 5 项发现（4 个独立红队 agent 分别报告）。**已有对应的 PR 在跟进（#88774 等安全修复序列中）。** [Issue #77462](https://github.com/NousResearch/hermes-agent/issues/77462)

#### 🟠 高（P1/P2）

- **[#53666] `clarify` 工具提示在聊天 UI 不渲染** — 用户看不到问题、回复为空。**自 6 月 27 日报告，至今仍开放**，已存在 52 天。[Issue #53666](https://github.com/NousResearch/hermes-agent/issues/53666)

- **[#77305] 委派失败消耗子代理迭代预算** — HTTP 429 重试链会消耗与成功调用相同的预算，导致 fallback 链被饿死。[Issue #77305](https://github.com/NousResearch/hermes-agent/issues/77305)

- **[#87654] Vision 工具首次探测后消失** — `_AuxProbeClientStub` 被错误缓存，`vision_analyze` / `browser_vision` 静默不可用。8 月 16 日新报告。[Issue #87654](https://github.com/NousResearch/hermes-agent/issues/87654)

- **[#77529] Secret provenance 在刷新失败后丢失** — MCP 子进程在 secret 仍存在的情况下被错误剥离凭据。与 #77462 同属凭据安全性集群。[Issue #77529](https://github.com/NousResearch/hermes-agent/issues/77529)

- **[#79101] API server 将虚拟模型别名存储为真实模型** — `POST /api/sessions` 未指定模型时，别名 `"hermes-agent"` 被持久化，后续调用以别名作为真实模型 ID。（已关闭，应已修复）[Issue #79101](https://github.com/NousResearch/hermes-agent/issues/79101)

- **[#88758] 压缩任务：replay 清理后持久化水位丢失** — 压缩功能在边界条件下可能丢失原始 durable watermark。8 月 17 日新开，需复现。[Issue #88758](https://github.com/NousResearch/hermes-agent/issues/88758)

#### 🟡 中（P3）

- **[#48860] OAuth 提示词清理器误替换文档 URL** — `hermes-agent.nousresearch.com` → 失效的 `claude-code.nousresearch.com`（NXDOMAIN）。6 月 19 日报告，已存续 60 天。[Issue #48860](https://github.com/NousResearch/hermes-agent/issues/48860)

- **[#84246] 归档/安装包产出物缺乏统一真实性和资源上限校验** — 安全审计 campaign 42 的一部分。[Issue #84246](https://github.com/NousResearch/hermes-agent/issues/84246)

- **[#84248] Docker cgroup 探测失败会导致资源限制被移除** — 安全审计 campaign 42 的一部分。[Issue #84248](https://github.com/NousResearch/hermes-agent/issues/84248)

#### 🔵 桌面端批量修复（今日合入）

- **#76064** 演示/自用插件默认启用 — **已关闭修复** ✓ [Issue #76064](https://github.com/NousResearch/hermes-agent/issues/76064)
- **#76245** 退出时后端未可靠终止（孤儿 `hermes serve`） — **已关闭修复** ✓ [Issue #76245](https://github.com/NousResearch/hermes-agent/issues/76245)
- **#80898** macOS 重复重启后孤儿后端累积 — **已关闭修复** ✓ [Issue #80898](https://github.com/NousResearch/hermes-agent/issues/80898)
- **#88200** BOTS sidebar 预览与点击打开内容不一致 — **已关闭修复** ✓ [Issue #88200](https://github.com/NousResearch/hermes-agent/issues/88200)

#### 📋 今日 PR 安全修复

- **PR #88774** `fix(security): fail closed when website-policy module is unavailable` — 将首次允许（fail-open）改为失败关闭（fail-closed）策略。[PR #88774](https://github.com/NousResearch/hermes-agent/pull/88774)
- **PR #84999** `fix(security): recheck browser_exec's landed URL after execution` — 页面执行后需复检实际落地 URL。[PR #84999](https://github.com/NousResearch/hermes-agent/pull/84999)

---

## 6. 功能请求与路线图信号

| 功能请求 | 状态 | 对应 PR | 评判 |
|---|---|---|---|
| **Per-call 输出速度（tokens/sec）** 显示在桌面状态栏/CLI 底部 | [Issue #?](https://github.com/NousResearch/hermes-agent/issues/) | [PR #44878](https://github.com/NousResearch/hermes-agent/pull/44878) | 已开放 67 天，切入使用成本感知路径，可能随 `/behavior` 系列进入下一版本 |
| **MCP 配置支持 env-backed 密钥引用** | [Issue #11239](https://github.com/NousResearch/hermes-agent/issues/11239) | 尚无 PR | 从 4 月 16 日至今已 124 天，与 #77462/#77529 同属密钥安全治理趋势，值得加速 |
| **安全重启当前桌面端后端** | [PR #76616](https://github.com/NousResearch/hermes-agent/pull/76616) | 开放中 | SSH 模式需先证明所有权再终止，逻辑完整；与 #76245/#80898 同族 |
| **插件隐藏 bundled model providers** | — | [PR #88776](https://github.com/NousResearch/hermes-agent/pull/88776) 已合并 ✓ | 属用户体验收尾 |
| **已安装技能暴露为斜杠命令（ACP）** | [PR #84512](https://github.com/NousResearch/hermes-agent/pull/84512) | 开放中 | P4 低优先级，但在 ACP 生态扩展背景下值得关注 |
| **行为分析 5 维评分 + 洞察卡片（/behavior）** | [PR #60417](https://github.com/NousResearch/hermes-agent/pull/60417) | 开放中 | 已开放 42 天，新命令提供定性行为画像（与现有 `/insights` 定量互补） |
| **会话恢复增强：提供者短暂故障自动恢复** | [PR #68766](https://github.com/NousResearch/hermes-agent/pull/68766) | 开放中，已 rebased | 重试退避延长至 2–3 分钟窗口，对使用不稳定提供商的用户价值较高 |
| **字节跳动（抖音/TikTok Biz）插件集成** | [Issue #86950](https://github.com/NousResearch/hermes-agent/issues/86950) | 尚无 PR | 4 个标准平台接入的 feature package，表明全球化平台拓展仍在推进 |
| **Termux 原生 pkg 安装路径** | [Issue #86986](https://github.com/NousResearch/hermes-agent/issues/86986) | 8 月 15 日提出，17 日关闭 | 已纳入官方支持范围 |

---

## 7. 用户反馈摘要

- **安全性是集中痛点：** Windows 上 secrets 文件权限漏洞（#77462）被 4 个独立红队 agent 同时发现，反映桌面端用户对凭据保护的高度关注；MCP 子进程在 secret 仍存在时丢失凭据的问题（#77529）同样被标记为高风险。

- **跨平台一致性诉求上升：** 桌面端累计 4 个孤儿/退出/服务端问题（#76064、#76245、#80898）今日全部关闭，表明团队正集中清理桌面端历史债务，用户对 Electron 后端的进程生命周期治理诉求强烈。

- **关键文档信号：** 企业用户在 v0.20.0 上手动运行 cron 丢附件（#88631）——此类「定时正常、手动异常」的差异对运营影响大，值得在 release notes 中明确提示。

- **README 与实现不符曾造成困惑**（#78539、#78567）：中断操作和 `/model` 冒号语法的文档指引与实现矛盾，团队认可并已通过 PR #88770 修正 README。文档准确性是用户信任的基础。

---

## 8. 待处理积压

### 长期未响应/未解决的重要项

- **[#53666] `clarify` 工具提示不在聊天 UI 渲染（P1，已 52 天）** — CLI 正常但桌面端无交互，用户收不到问题且回复为空。作为 P1 桌面端缺陷，52 天未关闭应引起维护者重视。[Issue #53666](https://github.com/NousResearch/hermes-agent/issues/53666)

- **[#53902] v0.17.0 渲染进程 fontations+temporal_rs 无限循环（GPU 98%，13W，已 51 天）** — 影响桌面端续航与发热，当前唯一明确标注 GPU 持续高负载的渲染问题。[Issue #53902](https://github.com/NousResearch/hermes-agent/issues/53902)

- **[#48860] OAuth 清理器把文档 URL 替换为 NXDOMAIN 域名（已 60 天）** — 属生产环境敏感路径（Anthropic OAuth 订阅流程），长期未获 fix PR。加上 #66616 skills index 持续（自 7 月 18 日起）降级，两者都值得优先响应。[Issue #48860](https://github.com/NousResearch/hermes-agent/issues/48860)

- **[#11239] MCP 配置支持 env-backed 密钥引用（已 124 天）** — 与今日多项安全修复（#77462、#77529、#83724）属同一治理方向，建议将「config.yaml 中的明文密钥」问题纳入路线图为明确目标。[Issue #11239](https://github.com/NousResearch/hermes-agent/issues/11239)

- **[#66616] Skills index 自动重建链路不稳定（已 31 天）** — 多次「degraded」、持久未闭环，影响 `/docs/skills` 生态的对外可信度。[Issue #66616](https://github.com/NousResearch/hermes-agent/issues/66616)

- **PR #44878（per-call tokens/sec，67 天）与 PR #62492（stale profile config 自动迁移，38 天）** 均为面向用户的功能/可靠性增强，长期开放未获合并；虽非阻塞，但希望能在后续发布中纳入评估。[PR #44878](https://github.com/NousResearch/hermes-agent/pull/44878)、[PR #62492](https://github.com/NousResearch/hermes-agent/pull/62492)

---

> **健康度总评：** 项目处于「高强度治理期」——今日合并了 cron 可靠性（2）、网关会话状态、桌面端 bug 清理（4 项）等一批修复，并以 v0.20.3 将 125 个 PR 汇总发布。安全修复密集（Windows ACL、fail-closed、URL 复检），反映出发布节奏稳健、对社区反馈的响应速度良好。当前最需要关注的是 **P1 桌面端 UI 交互问题（#53666）已搁置 52 天**，以及 **Skills index 持续降级（#66616）**——这两项如果继续拖延，可能影响桌面用户和文档生态的信心。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-18

> 数据窗口：2026-08-17 至 2026-08-18 | 数据来源：github.com/sipeed/picoclaw

---

## 1. 今日速览

PicoClaw 今日活跃度**平稳偏活跃**，24小时内产生3条 Issue、4条 PR，呈现"关闭多于新增"的良性态势。核心事件有三：一是 #3311 号"重复工具失败静默循环"严重Bug已被对应Fix PR（#3312）关闭，该Bug曾导致用户提问后数分钟无响应，修复标志着agent循环稳定性取得实质性进展；二是 #3340（Slack媒体上传FileSize参数缺失修复）已就绪待合入，涉及slack-go SDK兼容性问题；三是 #3339 上报了新的Google Antigravity配额误报问题，需引起重视。整体来看，项目在稳定性和渠道兼容性方面动作频繁，健康度良好。

---

## 2. 版本发布

**今日无新版本发布。**

上游变更持续积累中（至少待合入PR 1个、已合入3个），预计下一个patch/minor版本将包含Slack媒体修复、agent循环终止修复及微信渠道增强等变更。

---

## 3. 项目进展

今日共有 **3 个 PR 合入/关闭，1 个 PR 待合并**，在agent稳定性和渠道支持两个方向均有关键推进：

| PR | 状态 | 类型 | 要点 |
|----|------|------|------|
| [#3312](https://github.com/sipeed/picoclaw/pull/3312) fix(agent): stop turn early on repeated identical tool failure | ✅ 已关闭 | Bug修复 | **重要**：修复"工具以相同错误重复失败时，agent静默循环直至max_tool_iterations耗尽、用户永远得不到回答"的问题。此前循环会反复调用LLM并重新执行同一失败的调用，造成数分钟内无响应。 |
| [#271](https://github.com/sipeed/picoclaw/pull/271) fix: env overrides when config.json is missing + regression test | ✅ 已关闭 | Bug修复 | 修复配置文件缺失时（如Fly部署仅用secrets/env）环境变量覆盖不生效的问题——此前会回退到默认模型(glm-4.7)并因缺少凭据而失败。 |
| [#2606](https://github.com/sipeed/picoclaw/pull/2606) feat: enhance Weixin channel support and configuration | ✅ 已关闭 | 增强 | 微信渠道多实例支持与配置管理增强：新增channel目录和动态实例处理，改善了非法channel名的校验和错误处理，提升多实例流程稳定性。 |
| [#3340](https://github.com/sipeed/picoclaw/pull/3340) fix(slack): set FileSize on media upload params | ⏳ 待合并 | Bug修复 | slack-go v0.23.1要求在上传前通过`files.getUploadURLExternal`声明文件长度，此前未设置FileSize导致请求被SDK直接拒绝。 |

**评估**：agent循环终止修复（#3312）是近两周最关键的稳定性改进之一，直接解决了生产环境Telegram中"用户提问永不回复"的严重问题。整体项目在稳定性修复和渠道扩展两方面均在稳步推进。

---

## 4. 社区热点

### 最热 Issue：#3287 — IRC长消息支持（6条评论）

链接：[Issue #3287](https://github.com/sipeed/picoclaw/issues/3287)

**背景**：IRC协议默认限制单条消息512字节，超长消息会被IRC客户端自动拆分。此Feature Request希望PicoClaw能识别IRCv3的拆分机制，将分段消息合并为单条完整消息处理。

**分析**：此Issue已持续近一个月，是最活跃的话题。背后诉求是PicoClaw作为开源Agent框架在IRC这一长尾渠道的体验完整性问题——拆分的消息不仅会打断agent的上下文理解，还会导致回复对应关系混乱。虽然该Issue已标记stale，但仍有持续讨论，建议维护者评估是否纳入渠道兼容性路线图。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 标题 | 状态 | Fix状态 |
|--------|----------|------|------|---------|
| 🔴 高 | [#3311](https://github.com/sipeed/picoclaw/issues/3311) | 重复工具失败静默循环至max_tool_iterations——用户永远得不到回答 | 已关闭 | ✅ [#3312](https://github.com/sipeed/picoclaw/pull/3312) 已合入 |
| 🔴 高 | [#3339](https://github.com/sipeed/picoclaw/issues/3339) | Antigravity生成请求一律返回普通429，尽管OAuth scopes有效且模型发现成功 | 开放 | ❌ 无fix PR |
| 🟡 中 | [#3340](https://github.com/sipeed/picoclaw/pull/3340) | Slack上传媒体时缺少FileSize参数，被slack-go v0.23.1拒绝 | 开放(PR) | ✅ 待合入 |

**分析**：
- **#3311**（已修复）是今日最重磅的稳定性修复——用户在生产环境通过Telegram提问后，agent因工具反复失败而静默循环数分钟不回复。根因是循环中反复调用LLM重新执行相败的工具，且无终止机制。
- **#3339** 值得立即关注：Google Antigravity认证和模型发现均正常，但所有生成请求返回429"配额耗尽"，且响应中无`retryAfter`或具体配额上下文信息，对用户排障非常不友好。目前0条评论，需要维护者确认是否是API侧误报、SDK参数问题还是实际配额计算逻辑缺陷。

---

## 6. 功能请求与路线图信号

| 请求 | 来源 | 分析 | 纳入可能性 |
|------|------|------|------------|
| **IRC长消息合并支持**（[#3287](https://github.com/sipeed/picoclaw/issues/3287)） | 用户Feature Request（2026-07-22创建） | 诉求是正确理解IRCv3分片消息为单条完整消息，提升IRC渠道下agent的语义理解能力 | ⭐⭐ 中低 — 已标stale，属于长尾渠道优化，短期优先级不高 |
| **微信渠道多实例增强** | 已有PR [#2606](https://github.com/sipeed/picoclaw/pull/2606) （已合入） | 支持channel目录、动态实例处理、非法名校验，多实例流程稳定性提升 | 已纳入主线 ✅ |
| **配置缺失时env覆盖修复** | 已有PR [#271](https://github.com/sipeed/picoclaw/pull/271) （已合入） | 确保云原生部署（仅环境变量）也能正确加载模型配置 | 已纳入主线 ✅ |

综合来看，微信渠道增强已落地，围绕agent循环超时/失败通知、渠道消息分割处理等方向，社区有持续诉求。

---

## 7. 用户反馈摘要

**从Issue评论中提炼的真实声音：**

- **生产环境稳定性痛点（#3311）**："A turn can spin silently for many minutes (up to `max_tool_iterations`) when a tool fails with the same error on every call... user never receives an answer." —— 用户lucapette在生产Telegram上遇到agent无响应，表现为"静默转圈"。该问题已被修复并关闭。
- **IRC碎片消息切分问题（#3287）**：IRC协议512字节限制导致长消息被自动拆分，PicoClaw无法正确拼合，影响agent理解内容语义。该issue被标记stale，但社区讨论仍在进行，说明IRC用户群对此有真实需求。
- **API错误信息不明确（#3339）**：Antigravity返回的429缺少`retryAfter`信息和具体配额上下文，用户k3XD16指出"response contains no q..."（意即无细节），排障困难——反映了对可观测性和错误诊断能力的期待。

---

## 8. 待处理积压

| 项目 | 类型 | 年龄 | 状态 |
|------|------|------|------|
| [#3339](https://github.com/sipeed/picoclaw/issues/3339) Antigravity生成全部返回429 | Bug | 1天 | 🔴 新上报，需确认，尚未分配 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) IRC长消息合并支持 | Feature | 27天 | ⚠️ 已标stale但仍有6条评论，讨论持续 |
| [#3340](https://github.com/sipeed/picoclaw/pull/3340) Slack文件上传FileSize修复 | PR | 1天 | ⏳ 待reviewer合入 |

**给维护者的优先级建议**：
1. 尽快review并合入 [#3340](https://github.com/sipeed/picoclaw/pull/3340)（Slack上传修复），风险低、收益明确；
2. 对 [#3339](https://github.com/sipeed/picoclaw/issues/3339) 需要确认是否为Antigravity配额配置问题，避免用户因错误提示反复排查；
3. 考虑到 #3311 暴露的"agent静默无响应"问题在Telegram场景影响较大，建议后续在此类失败时增加用户可见的错误通知（如直接回复错误消息）。

---

*本日报由 AI 自动生成，数据基于 github.com/sipeed/picoclaw 公开仓库信息。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-18** | **数据周期：2026-08-17 00:00 — 2026-08-18 00:00 UTC**


## 1. 今日速览

过去 24 小时 NanoClaw 进入显著的渠道层（channel layer）建设高峰期。核心团队密集提交并合并了 25 个 PR（其中约 17 个来自 core-team），围绕 Slack 适配器（3 个波次）、会话运行时驱动层（driver seam）、通道桥梁（bridge）钩子体系（inbound-policy、membership-event、session-created hook 等）构建模块化扩展基础设施。与此同时，社区侧也保持较高活跃度：共 41 条 PR 更新、4 条 Issue 更新，出现了 1 个值得警惕的回归报告（任务行在聊天会话中触发时日志丢失）。整体活跃度评级：**高**——项目正处于架构重构与功能扩充交替推进的阶段，既有大范围的抽象层引入（#3306），也有针对具体用户问题的快速修复（#3303）。

值得注意的是，今日所有 PR 与 Issue 时间戳高度集中（均为 2026-08-17），且大量 PR 带有 `[core-team]` 标签，表明这是一次有计划的集中开发交付。


## 2. 版本发布

**无新版本发布。** 当前可见的版本锚点仍为 2.1.48（对应 PR #2988，one-door task delivery）。不过仓库中存在大量等待合并的代码变更，下一次版本发布预计会包含显著的渠道层架构更新。


## 3. 项目进展

今日合并/关闭的 25 个 PR 几乎全部来自核心团队，呈现出一条清晰的模块化架构推进脉络：

### 3.1 渠道层基础设施（channels）—— 今日最核心的推进

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#3305](https://github.com/nanocoai/nanoclaw/pull/3305) | slack: shared channel-layer library + canvas cluster (wave A) | 已合并 | 首次引入共享 Slack Web API 客户端，确立 token-key 约定，落地 canvas 集群模块 |
| [#3309](https://github.com/nanocoai/nanoclaw/pull/3309) | slack: defaults factory, membership, onboarding, a2a guard (wave B) | 已合并 | 完整 Slack 适配层落地：默认值工厂 + 全线程会话模式 + 成员管理 + 入职引导 + A2A 防护 |
| [#3310](https://github.com/nanocoai/nanoclaw/pull/3310) | fix(channels): restore slack-formatting container skill | 已合并 | 修复上游合并导致技能文件意外丢失的问题 |
| [#3297](https://github.com/nanocoai/nanoclaw/pull/3297) | setup: per-channel pre-step and companion-skill declarations | 已合并 | 设置向导获得按渠道扩展的能力 |

### 3.2 桥接层钩子体系（Chat SDK bridge）

多个 PR 为渠道模块提供了一致的扩展点，核心思路是"模块可以在不修改桥梁源码的情况下介入特定事件"：

- [#3292](https://github.com/nanocoai/nanoclaw/pull/3292) — bridge inbound-policy registration seam（入站策略注册接缝）
- [#3293](https://github.com/nanocoai/nanoclaw/pull/3293) — router: session-created hook（新会话创建钩子）
- [#3294](https://github.com/nanocoai/nanoclaw/pull/3294) — delivery: post-delivery hook with first-delivery context（投递后钩子，含首次投递标记）
- [#3295](https://github.com/nanocoai/nanoclaw/pull/3295) — channels: generic membership-event hook（成员事件钩子）
- [#3304](https://github.com/nanocoai/nanoclaw/pull/3304) — adapter-declared session-mode context defaults（适配器声明的会话模式默认值）

### 3.3 会话运行时驱动层（driver seam）

- [#3306](https://github.com/nanocoai/nanoclaw/pull/3306) — drivers: session-runtime driver seam（纯增量，无调用点变更），这是今日架构层面最值得关注的一个 PR：将"会话是什么"与"会话如何运行"解耦。
- [#3307](https://github.com/nanocoai/nanoclaw/pull/3307) — host: route session lifecycle through the driver seam（基于 #3306 堆叠，尚未合并）
- [#3308](https://github.com/nanocoai/nanoclaw/pull/3308) — groups: refuse to create a group over existing folder（数据丢失防护）

### 3.4 其他

- [#3296](https://github.com/nanocoai/nanoclaw/pull/3296) — extendTool：MCP 工具注册表的增量扩展机制（无需修改源码即可扩展工具 schema 和描述）

**整体评估**：项目正在把渠道适配从"硬编码在宿主代码中"推向"通过注册接缝和钩子进行模块化声明"。这个方向旨在让渠道模块（Slack、WebChat、未来的更多平台）可以以统一模式接入。架构骨架已在本日密集落地，但仍有多个 PR 处于堆叠未合并状态（#3306→#3307→#3308 链），预计后续几天将继续完成这套改造。


## 4. 社区热点

### 4.1 热门 Issue：#3203 — Codex Provider 编译失败 + 生成图片被静默丢弃

- **链接**：[nanocoai/nanoclaw Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203)
- **作者**：mshirel | **创建**：2026-08-08 | **更新**：2026-08-17 | **评论**：1

**详情**：`codex` provider 在 `providers` 分支上发射了一个未在 `ProviderEvent` 中声明的 `file` 事件，导致 `/add-codex` 后在 `main` 上运行无法通过容器类型检查。更严重的是，**没有任何消费者处理该事件**，即使它能编译通过，codex 生成的图片也会被静默丢弃。

**分析**：这个 Issue 已经存在了 9 天，且关联了一个紧急的[相关 PR #3299](https://github.com/nanocoai/nanoclaw/pull/3299)（codex 依赖升级，避免 GPT-5.4 退役后失效）。图片生成是 codex provider 的核心价值，静默丢弃会产生用户数据损失，但该 Issue 评论数仅 1 条，关注度偏低，需要维护者重视。

### 4.2 热门 Issue：#3301 — 任务在聊天会话中触发时"单门"模式异常

- **链接**：[nanocoai/nanoclaw Issue #3301](https://github.com/nanocoai/nanoclaw/issues/3301)
- **作者**：glifocat | **创建**：2026-08-17 | **更新**：2026-08-17 | **评论**：0

**详情**：2.1.48 引入的"one-door task delivery"（#2988）存在一个回归：`kind='task'` 的行在聊天会话中触发时会把整个查询切换为任务模式，导致：日志丢失、回复被吞、任务系列未列出。在安装中，2.1.48 之前创建的任务行都保留在原处（用户的描述暗示数量不少）。

**分析**：这是一个值得警惕的回归——**没有评论，但已经有了对应的 fix PR #3303 在等待审查**。这类"既有用户数据在升级后被破坏"的问题通常需要优先处理。

### 4.3 最活跃 PR 组：gavrielc 的集中交付

今日 41 条 PR 更新中，约 17 条来自核心团队成员 **gavrielc**，且全部集中在 2026-08-17 当天提交。这解释了为什么 PR 数量异常高——不是分散的社区贡献，而是一次集中的架构重构交付。这种做法有利于快速推进，但大量堆叠 PR 同时存在（#3306→#3307→#3308）时，需要关注单一开发者的提交积压风险。


## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| **高** | [#3301](https://github.com/nanocoai/nanoclaw/issues/3301) | **任务在聊天会话中触发时日志丢失、回复被吞**（2.1.48 回归，影响升级前已存在的任务行） | 已有 fix PR [#3303](https://github.com/nanocoai/nanoclaw/pull/3303)（待审查） |
| **高** | [#3203](https://github.com/nanocoai/nanoclaw/issues/3203) | **codex provider 编译失败 + 生成的图片被静默丢弃**（类型检查阻断 + 数据丢失） | 未修复，相关 PR [#3299](https://github.com/nanocoai/nanoclaw/pull/3299) 仅涉及依赖升级 |
| **中** | [#3289](https://github.com/nanocoai/nanoclaw/issues/3289) | **待处理消息轮询加载全部到期行到内存**，可能在高积压时造成性能瓶颈 | 已有 fix PR [#3291](https://github.com/nanocoai/nanoclaw/pull/3291)（待审查） |
| **中** | [#1143](https://github.com/nanocoai/nanoclaw/issues/1143) | **技能文档引用了已删除的 `/data/env` 路径**（文档陈旧，误导用户） | 今日已关闭 |
| **低** | [#3300](https://github.com/nanocoai/nanoclaw/pull/3300) | **attachment type 未在 agent-facing XML 中转义**（潜在注入/解析问题） | fix PR 已提交，待审查 |
| **低** | [#3302](https://github.com/nanocoai/nanoclaw/pull/3302) | **OneCLI 网关默认绑定地址错误**（写入了错误的 `ONECLI_URL`），修复 #2903 | fix PR 已提交，待审查 |

另外，PR [#3310](https://github.com/nanocoai/nanoclaw/pull/3310) 修复了上游合并导致 Slack 格式化技能文件被意外删除的问题（已合并）——这是一类合并纪律问题，值得维护者关注未来合并流程。


## 6. 功能请求与路线图信号

### 6.1 Web Chat 渠道 —— 双提交暗示强烈需求

今日出现了**两个独立实现的本地 Web Chat 渠道 PR**：

- [#3298](https://github.com/nanocoai/nanoclaw/pull/3298)（amit-shafnir，core-team）：带小型浏览器聊天 UI 的宿回环 Web 渠道适配器
- [#3290](https://github.com/nanocoai/nanoclaw/pull/3290)（viiluxx，社区贡献）：通过原生 HTTP bridge 的本地浏览器聊天，单页无依赖

两个 PR 都试图解决同一个问题：**目前除一次性 CLI 外，所有对话界面都路由到外部服务**。这与 Slack 渠道层的大规模工作形成了互补——项目显然在扩展"人与 agent 交互"的渠道多样性。两个 PR 均未合并，但方向明确，预计会在代码审查后合入一个或两者融合。

### 6.2 会话运行时驱动抽象 —— 架构演进信号

PR [#3306](https://github.com/nanocoai/nanoclaw/pull/3306)（drivers seam，Docker 为内建实现）+ [#3307](https://github.com/nanocoai/nanoclaw/pull/3307)（路由会话生命周期）的引入，暗示项目正在为**非容器运行时**铺路（例如本地进程、远程执行等）。目前 `NANOCLAW_RUNTIME_DRIVER` 环境变量已存在但选择逻辑处于"休眠"状态。这可能是下一阶段基础设施演进的方向。

### 6.3 设置向导的可扩展性

PR [#3297](https://github.com/nanocoai/nanoclaw/pull/3297)（per-channel pre-step 和 companion-skill 声明）让设置向导可以按渠道定制安装流程——这是渠道生态扩展的必要前置工作，与 Web Chat、Slack 等新渠道的落地直接相关。

### 6.4 即将到来的变更

- **GPT-5.4 将于 2026-08-31 从 Codex 退役**（PR [#3299](https://github.com/nanocoai/nanoclaw/pull/3299) 中提及）：`/add-codex` 技能固定的 `@openai/codex@0.138.0` 默认模型即将失效，需要在 8 月 31 日前完成依赖升级，否则该功能将静默不可用。


## 7. 用户反馈摘要

### 7.1 升级后的数据破坏是当前最痛的点

Issue [#3301](https://github.com/nanocoai/nanoclaw/issues/3301) 的作者 glifocat 明确描述了升级到 2.1.48 后的具体损失：**升级之前创建的任务在聊天会话中触发时，运行日志丢失、回复被吞、任务系列不再列出**。这不是新功能不工作的问题，而是已有数据在升级后被破坏——这类问题对用户信任的伤害最大。值得注意的是，作者同时提交了 issue 和修复 PR（#3303），说明用户对项目有参与意愿，但修复的审查速度直接决定了用户的满意程度。

### 7.2 文档陈旧导致使用受阻

Issue #1143（已关闭）指出技能文档中引用了已不存在的 `/data/env` 路径。文档与代码脱节会直接消耗用户排查时间。该 Issue 的关闭方式未提及（是修复了文档还是仅标记关闭），若只是关闭而未修复，建议维护者确认文档已更新。

### 7.3 社区成员积极参与修复

今日的 PR 中，至少 5 个来自非 core-team 成员（glifocat、wakqasahmed、torbenstruever、chiptoe-svg、viiluxx），且全部是问题驱动的修复。这表明项目文档化的贡献流程（contributing-guide v1）在起作用，社区反馈渠道畅通。

### 7.4 对沉默数据丢失的担忧

Issue [#3203](https://github.com/nanocoai/nanoclaw/issues/3203) 中提到的"codex 生成的图片被静默丢弃"（"silently dropped"）以及 Issue #3301 中的"日志被丢弃"（"logs dropped"）都指向同一个问题：**当系统出错时，用户很难知道发生了什么**。这是稳定性层面的系统性问题，建议项目在后续版本中考虑改进错误可见性。


## 8. 待处理积压

### 8.1 需要关注的长期未响应 Issue

| Issue | 创建时间 | 已持续 | 严重性 | 说明 |
|---|---|---|---|---|
| [#3203](https://github.com/nanocoai/nanoclaw/issues/3203) | 2026-08-08 | **10 天** | 高（数据丢失） | codex provider 编译失败 + 图片被丢弃，评论仅 1 条，无维护者回复记录 |

### 8.2 待合并的关键 PR（阻塞修复或功能落地）

| PR | 说明 | 阻塞原因 |
|---|---|---|
| [#3303](https://github.com/nanocoai/nanoclaw/pull/3303) | 修复任务行日志丢失回归 | 对应 Issue #3301，需优先审查 |
| [#3291](https://github.com/nanocoai/nanoclaw/pull/3291) | 修复待处理消息轮询的无限加载 | 对应 Issue #3289，性能隐患 |
| [#3299](https://github.com/nanocoai/nanoclaw/pull/3299) | **codex 依赖升级（8-31 截止）** | 有明确时间压力，需在 8 月底前合并 |
| [#3306](https://github.com/nanocoai/nanoclaw/pull/3306) | 会话运行时驱动抽象 | 后续 #3307、#3308 基于它堆叠，如果延迟合入，整个链条将被阻塞 |

### 8.3 提醒维护者注意

- **gavrielc 的堆叠 PR 链（#3306→#3307→#3308）** 依赖前置 PR 的合并，如果审查节奏慢，可能形成长期未合分支，增加合并冲突风险。
- **Issue #1143 的关闭方式不明确**（文档是否真正修正？），如果只是关掉了 issue 而没有更新 `/data/env` 的引用，同类问题会继续出现。
- **codex 相关的两个问题（#3203 + #3299）**相互关联但解决方案不同：前者需要修复事件类型声明和消费者逻辑，后者是依赖升级——二者都需要在 8 月 31 日前完成。


## 附：项目健康度总评

| 维度 | 评分（5 分制） | 说明 |
|---|---|---|
| 开发活跃度 | ★★★★★ | 41 条 PR 更新 / 日，渠道层大量基础设施落地 |
| 社区参与度 | ★★★★☆ | 社区成员贡献了约 12% 的 PR，但集中在少数活跃用户 |
| 稳定性关注 | ★★★☆☆ | 2 个高严重性数据丢失问题（#3301、#3203），修复进展偏慢 |
| 文档/可发现性 | ★★★☆☆ | 文档陈旧问题（#1143）出现；贡献者指南在发挥作用 |
| 版本节奏 | ★★★☆☆ | 2.1.48 后积累了大量未发布变更，下一版本预计跨度较大 |

**总体健康度：良好，但需注意**——架构推进积极，但部分社区问题的响应速度和修复进展不及预期（#3203 已 10 天未获实质性响应），建议维护者在推进架构重构的同时，确保用户反馈渠道保持畅通，修复的响应速度与架构推进的节奏相匹配。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-18

## 1. 今日速览

过去 24 小时 NullClaw 项目整体活跃度极低，处于维护静默期。核心信号如下：**无新增或关闭 Issue**，说明用户反馈和 Bug 报告停止流入；**仅 1 条 PR 更新**，为 Dependabot 自动提交的 Alpine Docker 基础镜像版本升级（3.23→3.24），目前等待合并；**无新版本发布**。项目目前呈现"正常运转但无人工干预"的状态——依赖自动化工具在推进基础设施更新，但社区互动和核心开发活动基本暂停。建议维护者关注 PR #956 的合并窗口，避免依赖版本长期滞后。

---

## 2. 版本发布

今日无新版本发布（最新 Releases 为空）。

---

## 3. 项目进展

今日无 PR 被合并或关闭，项目代码主干无任何推进。

唯一活跃的 PR 为依赖升级的自动提交，虽未合并但值得记录：

- **[#956] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group** — 由 `dependabot[bot]` 发起（2026-06-15 创建，2026-08-17 最后更新）。该 PR 将 Docker 基础镜像 Alpine 从 3.23 升级至 3.24，涉及安全补丁和运行时更新，属于基础设施维护范畴，不引入功能变更或破坏性改动。此 PR 已存在 **64 天**未合并，建议维护者尽快审核。

整体评估：**项目今日向前推进为 0**，处于停滞状态。

---

## 4. 社区热点

今日无活跃讨论。唯一的 PR #956（链接：[nullclaw/nullclaw PR #956](https://github.com/nullclaw/nullclaw/pull/956)）无评论、无反应（👍 0），属于自动化维护任务，未引发社区关注。

值得警惕的是：过去 24 小时零 Issue 更新，若这一趋势持续，意味着用户正在流失或已将重要反馈转移到其他渠道（如 Discord、邮件列表）。建议维护者主动检查社区沟通渠道的活跃度，防止"无声沉默"掩盖真实问题。

---

## 5. Bug 与稳定性

今日无新报告的 Bug、崩溃或回归问题。项目稳定性状态无法通过 Issue 数据评估——无反馈可能意味着"稳定运行"或"用户已放弃反馈"。结合 PR #956 长期未合并的事实（Alpine 3.23 可能存在已知 CVE 漏洞），**建议维护者评估基础镜像的安全风险**，并及时合入依赖升级 PR。

---

## 6. 功能请求与路线图信号

今日无用户提交新功能请求。从长期看，PR #956 所代表的依赖更新不属于功能路线图，但反映了项目的运维自动化水平——Dependabot 正在持续监控依赖安全。团队若计划推进下一版本，建议关注以下方向：

- **Docker 镜像现代化**：合并 Alpine 3.24 升级，消除潜在的容器安全扫描告警。
- **社区活性恢复**：无 Issue 和无 PR 的静默期不宜过长，建议主动发布 roadmap 或 RFC 征集反馈。

---

## 7. 用户反馈摘要

今日无用户评论可供分析。结合 PR #956 的状态（2 个月未合并），可推测用户对维护节奏可能存在以下潜在不满：

- **依赖更新不及时**：Dependabot 自动提交的基础镜像升级迟迟未合并，说明维护者响应自动化 PR 的速度偏慢，可能影响用户对项目安全维护承诺的信心。
- **缺乏互动**：0 Issue 和 0 评论意味着用户可能已通过其他途径表达诉求，或仍在观望。

建议维护者**公开说明 PR #956 的合并计划**，向社区传递"项目仍在积极维护"的信号。

---

## 8. 待处理积压

以下事项超过 30 天未处理，建议维护者优先关注：

| 项目 | 详情 | 滞留时长 | 建议 |
|------|------|----------|------|
| **PR #956** | Alpine 3.23→3.24 依赖升级 | 64 天 | 尽快审核并合并，消除安全风险；若因兼容性问题无法合并，应关闭PR并说明原因，避免依赖混乱 |
| **零 Issue 响应** | 连续 24 小时无新 Issue，但历史上是否有未关闭的积压 Issue 需排查 | — | 建议全面审查 open Issues，关闭过期内容或进行批量回应 |

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-18

## 1. 今日速览

IronClaw 在过去 24 小时内保持了极高的开发活跃度：共产生 28 条 Issue 更新（79% 为新开或活跃）和 44 条 PR 更新（64% 待合并），并发布了 v1.3.0-rc.1 候选版本。项目当前的核心攻关方向非常清晰——围绕 Epic #7591 系统性削减数据库写入压力（预计每轮对话减少 60+ 行写入），同时并行推进 WebUI 通知中心持久化改造和 WASM 工具契约规范化两条主线。值得一提的是，昨日出现了两个需要社区警惕的稳定性信号：libSQL 后端单一写连接导致资源治理器级联故障（#7714），以及 Slack 未关联用户连接引导的隐私问题（#7681），两者均已快速获得对应修复 PR。总体评估：项目处于高强度迭代期，健康度良好，但需关注写路径优化与稳定性修复之间的节奏平衡。

---

## 2. 版本发布

### ironclaw-v1.3.0-rc.1（2026-08-17）

首个 1.3.0 候选版本。Release Notes 为空，但结合近期 PR 与 Issue 推断，该版本包含：自动化无投递确定性结果机制（#7647）、基于运行时证据的自动化结果判定（PR #7650）、以及 1.2 版本修复的前向移植（PR #7663）。当前为 RC 阶段，尚不明确具体破坏性变更清单。

**迁移注意：** RC 版本建议仅在测试环境验证，重点关注自动化结果判定逻辑变更和 Windows 文件系统可靠性修复是否引入回归。

---

## 3. 项目进展

今日合并/关闭的 PR 中，以下几条对项目推进意义最大：

- **PR #7710（已关闭/合并）— Slack 连接引导多智能体审查修复落地**：修复了 PR #7682 中 7 项 connect 链接落地页加固 + 4 项 Slack 消息私密性发现，包括 `?connect=` 参数解析改为基于服务器端已安装扩展、移除客户端路径回退、Slack 连接引导消息新增异步加载链接并在共享频道中保持私密。这是对 #7681 的直接回应，**意味着 Slack 未关联用户体验问题已进入最终修复阶段**。

- **PR #7663（已关闭/合并）— 1.2 版本修复前向移植**：将 Windows 文件系统/发布冒烟可靠性、干净 Windows JSON 输出、健康检查运行时 curl 及稳定 1.2.0 元数据前向移植至 main 分支，同时保留一次性线程索引投影修复。**Windows 平台的稳定性补齐是 1.3.0 的重要前置条件**。

- **PR #7703（已关闭）— WASM 工具类型化响应方案合并入 #7711**：PR #7703 被 #7711 吸收，避免了 0.3.0 兼容 shim 的加-删抖动。这意味着 capability-response-normalization 栈的最终形态更加干净。

从 PR 结构来看，**公开 PR 中有 5 条 size: XL 且来自核心维护者**（#7718、#7708、#7694、#7693、#7711、#7717），表明多个大型功能线正在并行推进——Google Docs 语义编辑、自动化 run-now、持久化建议（suggestions）、结构化输出终结化、WASM 契约规范化、libSQL 写入饥饿修复。**项目的功能面正在快速拓宽，但 6 条 XL PR 同时悬而未决也给合并队列带来了不小压力。**

---

## 4. 社区热点

今日评论最活跃的议题集中在以下几条：

- **Issue #7591（3 条评论）— 削减持久化 DB 写入压力的 Epic**：作为当前最大的架构优化主线，该 Epic 已拆出 8 个子任务（#7594、#7598、#7603、#7604、#7605、#7701、#7707），其中今日新增 #7701（Tier 2：合并资源治理器的 reserve+reconcile 为单次写入）和 #7707（将 side-effect-outstanding 显式跟踪在进程行上）。社区讨论热度高，因为该工作直接影响部署成本。当前 8 个子任务中 3 个已关闭（#7594、#7598、#7605），剩余 5 个活跃。

- **Issue #7714（0 条评论，但当日即获修复）— libSQL 单一写连接饿死资源治理器**：PinchBench 147 任务压力测试中，资源治理器 delta 日志因等待写连接而停滞 ~40s，触发级联权威失效和永久预留泄漏。**该问题暴露了 libSQL 后端在生产负载下的关键瓶颈，且当日即有修复 PR #7717**，体现了团队对稳定性问题的响应速度。

- **Issue #7704 — 每日失败分类学报告**：clawbench 84 个非通过项中，**最大的可修复缺陷是存储写通道争用**（storage write-lane contention），与 #7591 Epic 高度呼应，构成了来自基准测试的独立证据链。社区关注点在于这些失败与 DB 写入压力之间的因果关系。

- **Issue #7685 — Dogfooding & QA 缺陷修复 Epic（08/17-08/23）**：新一周的 QA 集中期启动，包含了 #7715、#7716 等 QA 发现的问题。这代表了项目对内部测试的持续投入。

**社区核心诉求分析：** 多数讨论集中在**性能/成本**（DB 写入压力）与**稳定性**（libSQL 级联故障）两轴。提交者和维护者（serrrfirat）正在通过 Epic 系统化解决前者，而后者暴露出的基础设施韧性缺口值得关注。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 修复状态 |
|--------|-------|------|----------|
| **高** | [#7714](https://github.com/nearai/ironclaw/issues/7714) | libSQL 单一共享写连接饿死资源治理器 → 级联权威失效 + 永久预留泄漏 | ✅ PR #7717 已提交（XL，风险 low） |
| **高** | [#7702](https://github.com/nearai/ironclaw/issues/7702) | 合约要求的 AuditBefore/AuditAfter 记录在生产中从未写入，违反 host-api 合约 | 🔄 在 Epic #7591 范围内审计 |
| **中** | [#7716](https://github.com/nearai/ironclaw/issues/7716) | 添加 MCP 服务器流程缺少 Bearer Key 认证和 STDIO/HTTP 传输选项 | ❌ 无 |
| **中** | [#7715](https://github.com/nearai/ironclaw/issues/7715) | Telegram 连接流程缺少 bot/个人账号的选择/确认 | ❌ 无 |
| **中** | [#7705](https://github.com/nearai/ironclaw/issues/7705) | CoalescingEventSink 关闭时无限挂起 + pending_flush_error 锁存（#7631 审查发现） | ❌ 无 |
| **中** | [#3762](https://github.com/nearai/ironclaw/issues/3762) | Web UI 编辑 AGENTS.md 不更新当前/未来对话的系统提示词（已存活 3 个月） | ❌ 无 |
| **低** | [#7681](https://github.com/nearai/ironclaw/issues/7681) | Slack 未关联用户连接引导消息公开可见且需手动多步操作 | ✅ PR #7682 + #7710 已覆盖 |

**特别关注：#7714 揭示了 libSQL 写入路径的根本性设计缺陷**——单一共享写连接在压力下成为瓶颈，而资源治理器对该瓶颈的脆弱依赖导致了级联故障。这类"单点瓶颈导致级联失效"的问题值得后续重点进行系统性的基础设施韧性评估。

---

## 6. 功能请求与路线图信号

- **GitHub Projects v2 字段操作（#7719）**：用户（sergeiest）请求 IronClaw 的 GitHub 工具支持 GitHub Projects v2 字段操作（如 Main backlog 优先级）。此前因无法设置 P2 优先级而阻塞了 #7716 的标记。该功能对项目自身的 issue 管理流程有直接价值，**纳入 v1.4.0 的可能性较高**。

- **自动化 run-now（PR #7708）**：为自动化跨触发域和 WebUI 添加手动立即执行能力，保留调度的同时创建域分离的触发身份与溯源。该功能是对自动化系统的自然延伸，与 #6879 自动化 Epic 对齐，**有望在 v1.3.0 正式版中落地**。

- **Google Docs 语义编辑工具（PR #7718）**：新增四个语义能力（结构化检查、锚定批量编辑、填充表格、确定性验证），保留全部 11 个旧工具。这表明 IronClaw 正在从基础文件操作向领域特定工具演进，**是工具链成熟度的重要标志**。

- **持久化建议后端（PR #7694）**：新增 `suggestions.list/generate/start/dismiss` 操作，通过无界 runner 异步生成建议。这可能为 WebUI 提供更智能的下一步操作推荐，**与 OOBE 改进（#6994）存在协同可能**。

- **原生结构化输出终结化（PR #7693）**：在主机层进行工具禁用的一次性输出终结化，为运行上下文增加 provider 中立不可变输出契约。**该功能对自动化任务的确定性有直接影响**。

- **WebSocket/ACP 支持（PR #7513）**：新增 ACP serve 命令，使外部工具（GitHub Copilot CLI、VS Code 等）能够连接 IronClaw agent。**这是 CLI 生态互操作的重要一步**，但来自新贡献者（Kampouse）的 XL PR 需要更多审查时间。

---

## 7. 用户反馈摘要

从今日 Issue 评论和 QA 报告中提炼的反馈：

- **生产环境的持久内存召回可靠性**（#7275）：用户反馈明确信息在后续对话中不可靠召回。该 Issue 已关闭，但"验证显式持久内存跨对话召回"这个需求仍然存在。**用户的期望是持久内存像数据库事务一样可靠**，而非尽力而为。

- **libSQL 后端在高负载下触发的级联故障**（#7714）：PinchBench 运行过程中，资源治理器每 ~40s 经历一次"权威失效 → 日志替换 → 持久状态重载"循环，且预留释放失败导致泄漏。这暴露了**共享基础设施中一个组件的故障不应导致级联系统性失败**的韧性期望。

- **自动化无投递结果的确定性**（#7647）：用户需要一种确定性的"无投递"机制（`[SILENT]` 风格），提示文本无法保证抑制。**这是对自动化系统可预测性的明确需求**。

- **QA 测试新发现**（#7716、#7715）：MCP 服务器添加流程缺少认证选项、Telegram 连接流程缺少 bot/个人账号选择。这些是**用户在配置集成的常见路径上的摩擦点**，直接影响首次体验。

- **Slack 频道中的隐私问题**（#7681）：共享频道中未关联用户收到公开的连接引导，且需要手动多步操作。**用户在共享空间中期望被私下引导**，而非向整个频道暴露其未连接状态。

---

## 8. 待处理积压

- **Issue #3762（已存活 3 个月）**：编辑 AGENTS.md 不更新系统提示词。该问题直接影响用户对身份/行为配置的信任，且被标记为 suggested_P1、v1.4.0。**这是需要优先解决的关键 UX/正确性问题**。最近更新于 2026-08-17，说明仍在活跃讨论中。

- **PR #6994（已存活 17 天）**：OOBE 自动化任务原型，包含设计文档 + 实现，XL 规模，等待审查。来自 regular 贡献者 rdisandro，**若长期未合并可能影响贡献者积极性**。

- **PR #7184（已存活 14 天）**：Nostr 主机函数，XL 规模，新贡献者 Kampouse。Nostr 集成对去中心化社交网络场景有潜在价值。

- **PR #7491（已存活 7 天）**：omp core-tool 契约 + 引擎 + 基准测试（issue #7392，切片 1-4），XL 规模，涉及移除旧文件工具和混合旧/新工具面。**这是一个破坏性变更**，但契约统一后模型获得单一编码工具面（`read`/`write`/`edit`/`glob`/`grep`/`bash` 六种工具名）。该 PR 的风险值得关注，因为移除旧工具面意味着显式破坏兼容性，建议尽快完成审查或明确后续计划。

- **PR #7406（已存活 9 天）**：dependabot 提交的 actions 依赖批量更新（4 个包），medium 风险，待审查。依赖更新长期搁置会积累安全风险。

---

*日报生成时间：2026-08-18 | 数据来源：nearai/ironclaw GitHub 仓库*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为一名AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的LobsterAI GitHub数据，生成一份结构清晰、客观专业的项目动态日报（2026-08-18）。

---

### LobsterAI 项目动态日报 - 2026-08-18

#### 1. 今日速览
今日LobsterAI项目活跃度**中等偏上**，主要驱动力来自PR的密集合并（17条），显示了维护团队对既有功能完善和Bug修复的高效处理。值得关注的是，今日有两条关于`DeepSeek Harness (dsh)`引擎的新PR提交，暗示项目可能在探索新的运行时集成方向。然而，Issue处理方面存在隐忧，今日有7条活跃Issue，但全部为旧Issue的“stale”标记或社区自荐，且无一被关闭，Bug积压问题依旧存在。新版本方面暂无发布。

#### 2. 版本发布
无。

#### 3. 项目进展 (基于今日合并/关闭的PR)
今日共合并或关闭了17个PR，主要集中在**功能优化、Bug修复与体验提升**，整体项目稳定向前推进。重要进展包括：

- **新引擎探索**：合并了3条与 `dsh` (DeepSeek Harness) 相关的PR（#2502, #2505, #2506），虽然#2506为docs，#2505为launcher，但结合#2505的存在，表明项目正在为集成新的推理引擎（dsh）做技术准备。这可能是为了提供更灵活的模型接入选项或优化特定场景下的推理性能。
- **核心交互与体验优化**：合并了一批对Cowork功能体验的打磨PR：
    - `0xFLX` 贡献的系列PR（#1636, #1637, #1639, #1640, #1641）在今日集中合并，一次性为聊天窗口带来了**滚动到底部悬浮按钮**、**AI回复重新生成按钮**、**工具执行结果一键复制**、**弹窗Esc关闭**等多项标准交互，并修复了i18n问题，显著提升了用户的使用便利性。
    - `liuzhq1986` 提交的PR修复了**文本输入框的编辑菜单**（#2503）和**技能升级进度覆盖层**（#2501），解决了界面细节问题。
- **工程架构与数据管理**：
    - `swuzjb` 的PR（#1668）合并，实现了**每个Agent独立的工作目录配置**，这是对Agent管理能力的重要补充，为更复杂的多Agent协作场景奠定了基础。
    - `flowell` 的PR（#1661）合并，修复了**导出日志中存在明文密钥**的安全隐患，这是一项重要的安全性与隐私性改进。
- **兼容性与维护**：
    - `Ailein` 的PR（#1663）合并，将 **OpenClaw运行时从v2026.3.2升级至v2026.4.12**，并同步修复了微信插件兼容性问题，保证了底层核心的稳定性和新功能支持。
    - `leedalei` 的两条PR（#1667, #1669）分别修复了Qwen控制台链接失效和设置页模型提供商的体验问题。

#### 4. 社区热点
今日Issue和PR的评论均不活跃，没有产生高热度的讨论。

- **热门 PR (合并后关注)**：**#1668**（为Agent添加独立工作目录）和 **#1663**（升级OpenClaw运行时）是今日合并列表中影响面最大、也最受社区期待的功能性PR。它们分别解决了多Agent工作区隔离和核心运行时更新的关键诉求。
- **新增 Issue**：**#2500** 是唯一一条非stale的新Issue，为VOKO项目（A2A通信层）的自荐，请求与LobsterAI集成，这反映了社区对**Agent间通信与协作标准化**的兴趣，可能是一个值得关注的合作信号。

#### 5. Bug 与稳定性
今日报告的Bug均来自历史遗留Issue，无新增严重Bug。

- **中优先级**：
    - **#1635**：Ollama本地模型无法使用。该问题已存在4个月，至今未解决，是社区中关于模型接入兼容性的主要痛点。目前**无关联fix PR**。
    - **#1643**：手动创建定时任务保存时提示“还有内容未保存”（实际已保存成功）。这是一个误导性的ui/ux反馈Bug。目前**无关联fix PR**。
- **低优先级**：
    - **#1653**：groupPolicy被覆盖问题。
    - **#1662**：除SSE之外的MCP无法使用。
    - **#1671**：Markdown转Word中途失败，报错`finish reason: full`，疑似大模型上下文窗口限制问题。

#### 6. 功能请求与路线图信号
- **基于MD的工作流（#1644）**：该请求建议LobsterAI提供更强大的Agent编排能力，其核心诉求是**打破Agent间的信息孤岛**，使主Agent能够感知、调度其他专用Agent完成复杂任务。结合本次合并的**Agent独立工作目录（#1668）**，这显示出项目正在多Agent管理与协作层面逐步深入，该功能请求有望在后续版本中作为高级特性被考虑。
- **新引擎集成**：社区自发发布并合并了 `dsh` (DeepSeek Harness) 相关PR，这暗示用户对于**成本更低或特定性能表现的模型运行时**存在自发需求。虽然可能是外部贡献，但被维护者接受，表明该方向可能是项目未来拓展灵活性的一个选项。
- **A2A标准化（#2500）**：VOKO项目的自荐带来了A2A（Agent-to-Agent）通信标准化愿景。这虽非直接的功能请求，但它代表了社区对更广泛的Agent互操作性的期望，LobsterAI是否会支持此类开放协议将是未来的一个看点和潜在路线图方向。

#### 7. 用户反馈摘要
- **集成与兼容性诉求**：用户对**本地模型（Ollama）** 的支持不畅表达了不满，希望项目能改进对这些主流本地推理引擎的适配。同时#1662也反映了MCP协议支持不全的问题。
- **交互效率与一致性**：用户在 #1636-#1641 等PR的原始讨论中反馈了聊天和历史会话中的效率问题，这些PR的合并说明团队重视此类反馈。此外，#1643和#1640等评论也反映了用户对**界面反馈准确性**和**操作便捷性**的持续关注。
- **Agent能力边界**：关于 #1644，用户给出了一个非常具体的场景：主Agent无法感知到已有专用Agent的存在。这表明用户对“协同工作”的预期不仅是单Agent的对话，而是希望LobsterAI能成为一个真正的“Agent社区”，能够自主地管理和调度资源。

#### 8. 待处理积压
以下为长期未关闭且无关联PR的Issue，提醒维护者重点关注：
- **#1635**：`ollama的本地模型没法使用` (创建于2026-04-12) - 严重程度高，直接影响核心功能使用，4个月未解决。[链接](https://github.com/netease-youdao/LobsterAI/issues/1635)
- **#1644**：`许愿：增加基于md的工作流功能` (创建于2026-04-12) - 高度贴合未来路线图的功能请求，应明确计划或标注考虑中。[链接](https://github.com/netease-youdao/LobsterAI/issues/1644)
- **#1662**：`除sse之外的mcp无法使用` (创建于2026-04-14) - 功能缺失类bug，影响MCP生态扩展。[链接](https://github.com/netease-youdao/LobsterAI/issues/1662)
- **#1643**：`手动创建定时任务点击保存时提示"还有内容未保存"` (创建于2026-04-12) - 微小但影响体验的ui/ux bug。[链接](https://github.com/netease-youdao/LobsterAI/issues/1643)

---
**项目健康度评估**：
整体而言，LobsterAI项目在**开发活跃度**和**社区贡献热情**方面表现良好，维护者合并PR积极。但**Bug响应速度**仍是短板，多个4个月前的Issue未有任何进展。建议在后续迭代中，除了推进新功能和架构优化，也需分配固定资源清理历史积压Issue，以提升项目整体健康度和用户信任感。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-18

## 1. 今日速览

过去24小时项目活跃度良好，共产生3条Issue更新和9条PR更新，其中6条PR已合并/关闭，3条仍待审。值得关注的是，社区提交的 `feat: make webui rpc timeout configurable`（#1130）和 `feat: add MiniMax Code ACP agent`（#1204）已成功合并，标志着外部Agent生态扩展向前迈出一步。但与此同时，CI门禁因文件超长而变红（#1202）暴露了代码质量控制的短板，且来自2026年6月的Podman兼容性问题（#1095）已持续两个半月未解决，项目健康度存在隐忧。

🔗 [Issues列表](https://github.com/moltis-org/moltis/issues) | [PR列表](https://github.com/moltis-org/moltis/pulls)


## 2. 版本发布

过去24小时无新版本发布。上一次发布信息请参考项目 [Releases页面](https://github.com/moltis-org/moltis/releases)。


## 3. 项目进展

今日合并/关闭6条PR中，3条功能类、2条依赖类、1条修复类，核心进展如下：

- **外部Agent模型/推理强度选择落地** — [#1125](https://github.com/moltis-org/moltis/pull/1125) 已在今日合并，为 `/model` 命令添加外部Agent提供方的模型和effort选择能力，覆盖配置、界面展示与元数据持久化；与其配套的 **MiniMax Code ACP Agent** 支持（[#1204](https://github.com/moltis-org/moltis/pull/1204)）也同步合入，默认可自动发现 `mcode acp` 可执行文件。
- **WebUI RPC超时可配置** — [#1130](https://github.com/moltis-org/moltis/pull/1130) 合并，对应关闭 Issue [#1127](https://github.com/moltis-org/moltis/issues/1127)，用户可在WebUI中调节RPC超时。
- **Shadow DOM穿透效率优化** — [#1103](https://github.com/moltis-org/moltis/pull/1103) 合并，此前长期悬置（6月创建），其快照与引用查找路径现可高效穿透shadow DOM，对浏览器自动化场景有实际增益。
- 依赖更新：cargo组4项更新（[#1207](https://github.com/moltis-org/moltis/pull/1207)）与 tar 0.4.46（[#1087](https://github.com/moltis-org/moltis/pull/1087)）均已合并。

**待审风险项** — [#1206](https://github.com/moltis-org/moltis/pull/1206)（managed Files library & Settings browser）涉及新API面，改动范围大；[#1208](https://github.com/moltis-org/moltis/pull/1208) 与 [#1209](https://github.com/moltis-org/moltis/pull/1209) 均为Lstarsky0提交的bug修复，分别针对 cron heartbeat 活动时间不生效与 heartbeat.update 参数解析覆盖整个配置的问题，两处修复建议优先review，因为它们直接影响已发布的调度与配置功能。


## 4. 社区热点

今日讨论热度最高的Issue为 [#1095](https://github.com/moltis-org/moltis/issues/1095) *“Podman is not working via moltis”*（2条评论，创建于6月3日）。该问题长期未被解决，反映了用户对 **Podman容器后端支持** 的真实需求。虽然仓库已支持Docker、Podman等容器运行时（见#1206中“read-only-by-default容器挂载”），但由于容器的socket/API差异，用户在启用Podman时仍无法正常工作。此Issue长期滞留，说明维护者对容器后端多样性的重视不足，建议给予更高处理优先级。


## 5. Bug 与稳定性

按严重程度排序：

| 严重度 | 问题 | 状态 | Fix PR |
|--------|------|------|--------|
| **High** | [#1095](https://github.com/moltis-org/moltis/issues/1095) Podman 不可用 | 开放中，2条评论 | 无 |
| **Medium** | [#1202](https://github.com/moltis-org/moltis/issues/1202) CI门禁红色：`crates/memory-zvec/src/store.rs` 1799行、`crates/gateway/src/methods/services/admin.rs` 1531行，均超过1500行限制，`Format` 任务失败 | 已关闭 | 直接提交修复即可，无需PR |
| **Low** | [#1205](https://github.com/moltis-org/moltis/issues/1205)（由[#1208](https://github.com/moltis-org/moltis/pull/1208) 关闭） `heartbeat.active_hours` 从未生效：`is_within_active_hours` 已有文档与测试但未被调用 | 已有fix PR | [#1208](https://github.com/moltis-org/moltis/pull/1208) |

另有 [#1187](https://github.com/moltis-org/moltis/issues/1187) 由 [#1209](https://github.com/moltis-org/moltis/pull/1209) 关闭：`heartbeat.update` 反序列化时将参数直接赋值到整个 `HeartbeatConfig`，导致调用方未提供的键被重置为默认值而非保留原值。


## 6. 功能请求与路线图信号

- **MiniMax Code 集成** — 新Agent类型 `acp-minimax-code` 已合入（[#1204](https://github.com/moltis-org/moltis/pull/1204)），外部Agent生态继续扩张。结合上周的进展，Moltis 正在向多模态、多提供方的方向演进。
- **Managed Files library / Settings browser** — [#1206](https://github.com/moltis-org/moltis/pull/1206) 提出基于数据目录的持久化文件库，包含认证流式上传/下载/创建/移动/删除API，将显著增强Moltis作为个人AI助手的文件管理能力，建议关注其实施进度。
- **RPC超时配置**（[#1127](https://github.com/moltis-org/moltis/issues/1127)）— 已通过PR #1130落地，反映用户对“长时间远程操作”场景的体验诉求。

用户功能请求方向上，Podman支持（#1095）仍是呼声最高但未获响应的需求，建议将其纳入下一版本规划。


## 7. 用户反馈摘要

- **容器生态兼容性诉求（#1095）**：用户明确表示“Podman is not working via moltis”，而官方默认推荐Docker，这导致依赖Podman的用户很难上手。
- **配置耐久性预期（#1187→#1209）**：用户期望 `heartbeat.update` 对配置的修改是“部分更新”（类似于PATCH语义），而非整段覆盖。这表明用户对配置管理的精细度有较高预期。
- **质量门禁关注（#1202）**：用户（Lstarsky0）主动报告文件行数超限导致CI变红，说明社区成员对仓库质量有责任感，愿意帮助维护门禁健康。


## 8. 待处理积压

| 类型 | 编号 | 标题 | 创建时间 | 备注 |
|------|------|------|---------|------|
| Issue | [#1095](https://github.com/moltis-org/moltis/issues/1095) | Podman兼容性：Podman is not working via moltis | 2026-06-03 | 持续76天无修复，🚨 高优先级 |
| Issue | [#1127](https://github.com/moltis-org/moltis/issues/1127) 功能请求：配置RPC超时 | 2026-06-17 | 已通过#1130修复，可关闭 |
| PR | [#1103](https://github.com/moltis-org/moltis/pull/1103) | Shadow DOM穿透查找优化 | 2026-06-04 | 已合并 |
| PR | [#1087](https://github.com/moltis-org/moltis/pull/1087) | tar 0.4.45→0.4.46 依赖更新 | 2026-05-29 | 已合并 |

> 注：已有 #1202（行数超限）与 #1187（heartbeat.update 配置覆盖）两例“用户主动反馈bug”被快速关闭，但牵涉的 #1095 和 #1205 仍未彻底修复，希望维护者保持当前的响应节奏。

---

*本日报由 AI 自动生成，数据截至 2026-08-18。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-18


## 1. 今日速览

CoPaw 项目过去24小时整体活跃度**较高**，呈持续上升态势。共更新 14 条 Issues（新开/活跃 8 条，关闭 6 条）和 35 条 PR（待合并 13 条，合并/关闭 22 条），社区贡献者参与热情显著，其中包括多位首次贡献者（first-time contributor）提交的 PR。当前无新版本发布，项目正处于 v2.1.0 发布后的密集迭代阶段。值得关注的是：合并/关闭的 22 条 PR 中涵盖多项稳定性修复与体验优化，但亦有 13 条 PR 仍在等待审查合并，包括涉及 provider 统一、会话级多项目目录等大型功能 PR，有待维护者加快审查节奏。此外，今日集中暴露了多个 2.x 版本引入的回归问题（MCP 工具调用崩溃、OneBot 图片 URL 过期等），修复 PR 多数已到位，整体健康度良好。


## 2. 版本发布

过去24小时内无新版本发布。最近版本为 v2.1.0，当前社区反馈主要围绕该版本展开。


## 3. 项目进展

今日合并/关闭了 22 条 PR，涉及多个重要功能修复与体验优化：

**数据应用与生态建设**
- [#6940](https://github.com/agentscope-ai/QwenPaw/pull/6940) 合并：新增原生 DataPaw 应用运行时及持久化分析工作区，为数据分析场景提供独立运行环境。
- [#7089](https://github.com/agentscope-ai/QwenPaw/pull/7089) 新开：datapaw 插件独立版本驱动发布流水线，与主项目解耦发布节奏。

**控制台体验修复（多来自社区贡献）**
- [#7017](https://github.com/agentscope-ai/QwenPaw/pull/7017) 合并：新安装的 PawApps 无需刷新页面即可立即打开。
- [#7036](https://github.com/agentscope-ai/QwenPaw/pull/7036) 合并：为聊天媒体附件增加统一下载能力。
- [#6975](https://github.com/agentscope-ai/QwenPaw/pull/6975) 合并：修复 `/compact` 后上下文用量环不更新的问题。
- [#6968](https://github.com/agentscope-ai/QwenPaw/pull/6968) 合并：修复图片 Base64 被错误计入 token 用量导致上下文窗口虚满的问题。
- [#6981](https://github.com/agentscope-ai/QwenPaw/pull/6981) 合并：从七种语言环境文件中移除输入框中的审批命令提示。
- [#5151](https://github.com/agentscope-ai/QwenPaw/pull/5151) 合并：修复 GitPanel 因 class 前缀不匹配导致 tab 样式失效的问题。

**新功能探索（今日新开 PR）**
- [#7086](https://github.com/agentscope-ai/QwenPaw/pull/7086) 首次贡献者提交：统一设置齿轮与下拉菜单的语言选项（补全印尼语和越南语）。
- [#7080](https://github.com/agentscope-ai/QwenPaw/pull/7080) 首次贡献者提交 + [相关联 Issue #7079](https://github.com/agentscope-ai/QwenPaw/issues/7079)：新增 PowerContext 可插拔长期记忆后端。
- [#7078](https://github.com/agentscope-ai/QwenPaw/pull/7078) 新开：为 Console 文件工作区增加系统提示词文件选择器。
- [#7081](https://github.com/agentscope-ai/QwenPaw/pull/7081) 首次贡献者提交：集成 AnySearch 网络搜索（SearchProvider + MCP），同时修复 MCP env-ref 头部绑定缺陷。
- [#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) 新开：在模型请求前将远程媒体 URL 本地化，解决热链保护和网络隔离问题。
- [#7083](https://github.com/agentscope-ai/QwenPaw/pull/7083) 合并：压缩后台任务列表高度并增加滚动提示，防止输入框被下推。

**待合并的关键 PR（维护者关注）**
- [#6515](https://github.com/agentscope-ai/QwenPaw/pull/6515)：新增火山引擎 Agent Plan 和 Xiaomi MiMo V2.5 API 内置 Provider（已等待 3 周）。
- [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)：统一 provider 发现、模型元数据、路由与智能体控制的大型重构。
- [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)：会话级多项目目录绑定。
- [#6719](https://github.com/agentscope-ai/QwenPaw/pull/6719)：聊天轮次中的持久化工作区产物卡片。


## 4. 社区热点

**1）升级 2.0 后 MCP 工具持续报 "Tool not found"**
- Issue [#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405)（7 条评论，已关闭）
- 这是当前社区讨论度最高的议题之一。用户在升级到 2.0 后，MCP 工具名虽已按 `[mcp-key]__[tool_name]` 格式变更，但调用时始终提示找不到工具。该 Issue 从 7 月 23 日持续到 8 月 17 日才关闭，耗时近一个月。同一时段 [#7063](https://github.com/agentscope-ai/QwenPaw/issues/7063) 报告了工具调用必现崩溃的问题，且根因直指 `_acting()` 返回 coroutine 而非 async generator 的代码缺陷。两者叠加表明 2.x 升级后 MCP/工具调用链路存在较严重回归，尽管单看评论数不高，但影响面广、用户痛点明显。

**2）按频道独立配置模型的高票诉求**
- Issue [#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085)（3 条评论，OPEN）
- 用户期望不同渠道（钉钉、微信、控制台）可独立配置不同模型，而非全局统一。给出了非常具体的使用场景（钉钉用 gpt-4o、微信用 qwen-max、控制台用本地 llama.cpp）。这是多租户/多渠道部署场景下的刚需，值得产品团队评估。目前尚无对应 PR 关联。

**3）OneBot 频道图片 URL 过期导致会话"中毒"**
- Issue [#7088](https://github.com/agentscope-ai/QwenPaw/issues/7088)（2 条评论，已关闭）
- QQ 图片的签名 rkey 约 2 小时过期，但 OneBot 频道未经处理直接将 URL 透传给 LLM API，导致模型端下载失败（HTTP 400），且过期 URL 留在会话历史中持续"污染"后续对话。该问题直击多模态 Agent 场景的痛点，已关闭并有望由 [#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) 的媒体 URL 本地化方案解决。

**4）插件热安装后运行时 hooks 静默丢失**
- Issue [#7077](https://github.com/agentscope-ai/QwenPaw/issues/7077)（2 条评论，已关闭）
- 插件通过 `register_runtime_hook()` 注册的回调仅在工作区首次创建时生效，工作区 reload（如热安装插件后）即静默丢失。对插件开发者的开发体验影响较大，已关闭但值得确认修复是否真正落地。


## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 🔴 严重 | [#7063](https://github.com/agentscope-ai/QwenPaw/issues/7063) | Agent 执行工具调用时必现崩溃。`agentscope` 在 `_execute_tool_call` 中 `async for` 遍历 coroutine 而非 async generator，触发 `TypeError`。影响所有 v2.1.0 用户的工具调用功能 | 已关闭，需确认修复方案 |
| 🔴 严重 | [#7088](https://github.com/agentscope-ai/QwenPaw/issues/7088) | OneBot v11 频道将过期 QQ 图片 URL 透传给模型，导致 HTTP 400 且过期 URL "中毒"对话历史，持续破坏后续回复 | 已关闭，由 [#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) 修复中 |
| 🟠 中等 | [#7082](https://github.com/agentscope-ai/QwenPaw/issues/7082) | Console 渠道初始化时 `_StructuredOutputDynamicClass is not fully defined` Pydantic 错误，阻断智能体/工具箱初始化 | OPEN，无关联 PR |
| 🟠 中等 | [#7076](https://github.com/agentscope-ai/QwenPaw/issues/7076) | qwenpaw-creator 模型配置报 404，影响 v2.1.0 | OPEN，无关联 PR |
| 🟠 中等 | [#7084](https://github.com/agentscope-ai/QwenPaw/issues/7084) | 历史对话仅一条时，新开聊天后点击历史会话无响应 | OPEN，无关联 PR |
| 🟡 轻微 | [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | 多个 UI 会话下 Console 停止请求可取消活跃的飞书会话（2.1.0） | OPEN，持续更新中 |
| 🟡 轻微 | [#7051](https://github.com/agentscope-ai/QwenPaw/issues/7051) | Console 聊天中图片附件在会话重载后丢失（后端返回 data URL，前端显示裂图） | 已关闭 |
| 🟡 轻微 | [#7048](https://github.com/agentscope-ai/QwenPaw/issues/7048) | `cron update --text` 返回成功但 prompt 实际未更新（agent 类型任务） | 已关闭 |
| 🟢 已修复 | [#7077](https://github.com/agentscope-ai/QwenPaw/issues/7077) | 插件热安装后运行时 hooks 静默丢失（workspace reload 后） | 已关闭 |


## 6. 功能请求与路线图信号

| 功能请求 | 关联 Issue | 对应 PR / 状态 | 信号强度 |
|---------|-----------|---------------|---------|
| **多渠道（频道）独立模型配置** | [#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085) | 无关联 PR | 🟡 中 — 单 Issue 但场景具体，多租户部署刚需 |
| **智能体协作在同一会话窗口** | [#6925](https://github.com/agentscope-ai/QwenPaw/issues/6925) | 无关联 PR | 🟡 中 — 影响协作体验，用户需频繁切换智能体查看对话 |
| **PowerContext 可插拔长期记忆后端** | [#7079](https://github.com/agentscope-ai/QwenPaw/issues/7079) | [#7080](https://github.com/agentscope-ai/QwenPaw/pull/7080)（首次贡献者） | 🟢 强 — PR 已提交，通过现有 `BaseMemoryManager` 扩展点实现 |
| **定时任务运行细节展示** | [#7075](https://github.com/agentscope-ai/QwenPaw/issues/7075) | 无关联 PR | 🟡 中 — 用户希望看到开始时间、运行时长、结束时间、结果等 |
| **AnySearch 网络搜索集成** | — | [#7081](https://github.com/agentscope-ai/QwenPaw/pull/7081)（首次贡献者，今日提交） | 🟢 强 — 同时修复 MCP env-ref 头部绑定缺陷，基础能力增强 |
| **火山引擎 Agent Plan & 小米 MiMo V2.5 Provider** | — | [#6515](https://github.com/agentscope-ai/QwenPaw/pull/6515)（已等待 3 周） | 🟢 强 — 社区持续等待合并中 |
| **DataPaw 数据分析应用 + 独立发布** | — | [#6940](https://github.com/agentscope-ai/QwenPaw/pull/6940)（已合并）+ [#7089](https://github.com/agentscope-ai/QwenPaw/pull/7089)（新开） | 🟢 强 — 已落地，持续演进中 |


## 7. 用户反馈摘要

从今日 Issues 与评论中提炼的真实用户声音：

**😕 痛点与不满**
- **升级 2.x 后工具调用链路可靠性下降**：MCP 工具 "Tool not found"（[#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405)）和工具调用必现崩溃（[#7063](https://github.com/agentscope-ai/QwenPaw/issues/7063)）是近期最集中的负面反馈。用户在升级到 2.0/2.1 后遭遇能力回退，严重影响生产可用性。
- **插件开发体验打折**：热安装后运行时 hooks 静默丢失（[#7077](https://github.com/agentscope-ai/QwenPaw/issues/7077)），开发者难以追踪问题根源。
- **多渠道模型配置僵化**：全局或智能体级别的模型配置无法满足多频道差异化需求（[#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085)），用户明确表达了对灵活性的渴望。

**👍 肯定与期望**
- 社区对 PowerContext 记忆后端、AnySearch 搜索集成等新能力持积极态度，首次贡献者活跃度上升说明项目对社区有吸引力。
- 合并的多个 Console 体验修复（如媒体下载、紧凑任务列表、语言选项统一）反映了项目对细节体验的持续打磨。

**💡 场景洞察**
- 多模态 Agent 场景下，图片 URL 过期"中毒"会话历史的问题（[#7088](https://github.com/agentscope-ai/QwenPaw/issues/7088)）揭示了本地化媒体的必要性 — 这是从"能用"到"好用"的关键细节。
- 智能体协作会话割裂（[#6925](https://github.com/agentscope-ai/QwenPaw/issues/6925)）表明多智能体协作的使用场景正在增长，但交互体验仍需优化。


## 8. 待处理积压

**长期未响应的 PR（维护者关注）**

- [**#6515**](https://github.com/agentscope-ai/QwenPaw/pull/6515)（7 月 28 日创建，已等待 3 周）：新增火山引擎 Agent Plan 和 Xiaomi MiMo V2.5 API Provider。该 PR 直接扩展内置 Provider 列表，对国内用户价值高。无 review 记录。
- [**#6302**](https://github.com/agentscope-ai/QwenPaw/pull/6302)（7 月 21 日创建，已等待近 4 周）：统一 provider 发现、模型元数据、路由与智能体控制的大型重构，涉及面广，但长期未获 review。若合入将显著改善模型管理体验。
- [**#6976**](https://github.com/agentscope-ai/QwenPaw/pull/6976)（8 月 13 日创建）：会话级多项目目录绑定，提升文件工具和 shell 命令的路径解析灵活性。已 5 天未获 review。
- [**#6719**](https://github.com/agentscope-ai/QwenPaw/pull/6719)（8 月 5 日创建，已等待近 2 周）：持久化工作区产物卡片，增强聊天中工作区文件的可见性。
- [**#6986**](https://github.com/agentscope-ai/QwenPaw/pull/6986)（8 月 13 日创建）：修复沙箱被杀毒软件拦截的问题。对 Windows 用户影响较大。

**建议**：面对 13 条待合并 PR（包含至少 3 条来自首次贡献者），建议维护者加快 review 节奏并给出明确反馈。特别是 #6515 和 #6302 这类基础能力扩展，持续搁置可能削弱社区贡献热情。同时，#7063（工具调用崩溃）和 #7082（Pydantic 类未定义）均为阻断性问题，建议优先确认修复方案或分配 owner 跟进。


*数据来源: [github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw) | 统计周期: 2026-08-17 至 2026-08-18 | 报告生成时间: 2026-08-18*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-18

## 1. 今日速览

ZeroClaw 在过去 24 小时内保持高活跃度，共产生 50 条 Issue 更新和 50 条 PR 更新。Issue 侧以新开/活跃为主（44 条），关闭 6 条；PR 侧待合并 34 条，已合并/关闭 16 条。今日无新版本发布，项目仍处于 v0.8.x 系列迭代周期。值得注意的趋势是：**安全加固和治理流程优化**成为当前社区讨论的绝对主线——多篇高热度 RFC（#6808、#8603、#8303、#7155）均围绕运行时安全边界、认证架构和流程治理展开，且多数已进入"accepted"状态，表明 v0.9.0 的安全架构重塑正在稳步推进。整体项目健康度良好，但需关注 34 条待合并 PR 的积压以及部分 long-running RFC 的收敛速度。


## 2. 版本发布

过去 24 小时内无新版本发布。当前项目处于 v0.8.x 系列（最新已知版本 v0.8.4），v0.9.0 为下一里程碑（见 tracker #7432），预计将包含大量安全架构与网关边界变更。


## 3. 项目进展

今日合并/关闭的 PR 集中在**安全漏洞修复**与**CI/测试基础设施改进**两大方向，共 16 条已合并/关闭：

### 🔒 安全修复（P1 级别优先）
- **#9973** — 修复 Gemini API 密钥泄露至 URL 的问题（P1，security），改为通过 `x-goog-api-key` 请求头传递，防止密钥经 URL 和 URL 诊断日志暴露。
- **#10000** — 限制 QQ 和 Mattermost 频道附件下载大小（P1，security），新增统一的受限 HTTP 响应读取器，修复无 Content-Length 时的无界下载风险。
- **#9612** — 修复 WhatsApp Cloud 审批令牌在异常退出时未清理的问题（P1，security），审批令牌现在在请求前即注册到全局守卫，避免孤儿令牌残留。
- **#9993** — 修复 Email 频道隐式读取本地文件的问题（security），空附件负载不再触发以显示文件名为路径的本地文件读取。
- **#9996** — 使 action budget 记账原子化（security），并行工具调用不再能联合超出 `max_actions_per_hour` 限制（修复 issue #9849）。
- **#9765** — 修复 SOP 定义加载路径错误（P1，bug），从错误的 `data_dir` 改为共享 workspace 加载 SOP 定义。

### 🛠️ CI/测试基础设施
- **#10039** — 提取共享 Clippy 运行脚本，统一 required Linux、advisory 跨平台和定向 Windows Clippy 工作流（对应 issue #7884）。
- **#10043** — 移除 Lint 中重复的架构测试守卫，由 workspace Test 统一负责。
- **#10010** — 修复 cron 自定义 shell 测试中的 ETXTBSY 竞争条件。
- **#9398** — 新增 macOS 和 Windows 定时调度测试工作流（nightly 03:17 UTC）。

### 其他
- **#9547** — 升级 CPAL 至 0.18.1，迁移 Voice Wake 至统一 API。

**关键进展判断：** 今日合并的 PR 以"止血"为主——5 个安全修复中有 4 个为 P1 优先级，说明项目正在系统性收敛近期审计发现的安全问题。特别是 #9996 修复了 action budget 非原子检查的竞态条件（#9849），该修复为后续 v0.9.0 的权限模型重构奠定了基础。CI 侧 #10039 和 #10043 的合并推动 #7884 至关闭状态，完成了跨平台 Chippy 逻辑的统一，降低了 CI 配置漂移风险。


## 4. 社区热点

### Issue 讨论热度 TOP 3

1. **#6808** — RFC: Work Lanes, Board Automation, and Label Cleanup（23 评论）
   链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6808
   **状态：** Rev 26，已批准，rollout 进行中。
   **分析：** 这是一篇治理类 RFC，历经 26 次修订，讨论如何简化维护者的工作路由和标签系统。高评论数说明社区对项目治理流程有强烈诉求，期望减少维护者的手工操作负担。该 RFC 已进入实施阶段，但战线较长，后续可关注其 rollout 进度。

2. **#8603** — RFC: ZeroClaw Chat Completions profile（23 评论）
   链接：https://github.com/zeroclaw-labs/zeroclaw/issues/8603
   **分析：** 社区对 OpenAI Chat Completions 协议兼容的呼声很高。该 RFC 旨在让 ZeroClaw 兼容 Open WebUI、LobeChat、Continue.dev、Aider、LangChain、OpenAI SDK 等主流客户端。这将是 ZeroClaw 扩大生态接入面的关键一步，值得持续关注。

3. **#8303** — RFC: Goal mode v1 — bounded foreground Matrix work（22 评论，👍 1）
   链接：https://github.com/zeroclaw-labs/zeroclaw/issues/8303
   **分析：** 关于跨多轮 agent turn 的持久化目标执行机制。社区对"有界的前台工作模式"讨论热烈，该功能将显著提升 agent 处理复杂多步骤任务的能力。

### 新晋热点
**#10023**（2 评论）— Failure logs claim the requested model, not the pinned fallback model（2 天内获得关注）
链接：https://github.com/zeroclaw-labs/zeroclaw/issues/10023

### PR 侧观察
大多数 PR 的评论数未显示，但建议关注 **#9986**（feat: export agent to portable bundle）——这是一个新功能 PR，评论数和讨论情况应是今日 PR 侧的热点，目前状态为 `needs-author-action`，说明有较大改动需要跟进。

**热点诉求归纳：** 当前社区讨论主要集中在三方面：① 协议兼容性（#8603，OpenAI Chat Completions）；② 多轮任务执行能力（#8303 Goal mode）；③ 项目治理效率（#6808 流程优化）。三者分别对应外部生态接入、agent 核心能力、内部协作效率，显示 ZeroClaw 正处于从"功能可用"向"生态完善"过渡的阶段。


## 5. Bug 与稳定性

### 今日修复的 Bug（含 PR）

| Issue | 标题 | 严重度 | 修复 PR | 状态 |
|-------|------|--------|---------|------|
| #9849 | RateLimitedTool budget check is non-atomic under parallel dispatch | S2（降级行为） | #9996 | ✅ 已关闭 |
| #9594 | Coding-agent tools charge the action budget twice | S2 | — | ✅ 已关闭（今日） |
| — | Gemini API keys exposed in URLs | 安全 | #9973 | ✅ 已合并 |
| — | QQ/Mattermost unbounded attachment downloads | 安全 | #10000 | ✅ 已合并 |
| — | Email channel implicit local file reads | 安全 | #9993 | ✅ 已合并 |
| — | WhatsApp approval token orphaned on exit | 安全 | #9612 | ✅ 已合并 |
| — | SOP definitions loaded from data_dir instead of workspace | P1 bug | #9765 | ✅ 已合并 |

### 待处理 Bug（按严重度排列）

**P1：**
- **#9397** — WhatsApp Web `allowed_groups` 空列表当前允许所有群组访问（安全，in-progress，已接受）
  链接：https://github.com/zeroclaw-labs/zeroclaw/issues/9397

**P2：**
- **#10023** — Reliable provider 失败日志错误地记录请求的模型名而非实际服务的故障转移模型（新报，暂无修复 PR）
  链接：https://github.com/zeroclaw-labs/zeroclaw/issues/10023
- **#10011** — daemon 心跳测试中运行时写入可执行文件（需替换测试方案，help wanted）
  链接：https://github.com/zeroclaw-labs/zeroclaw/issues/10011

### 稳定性评估
今日修复的 7 个 bug 中 5 个涉及安全边界，且集中在**数据泄露与资源限制绕过**方向。这与此前 RFC（#6971 Security posture）的治理方向一致。建议持续关注 #9397 的修复进展——WhatsApp 空列表权限放大问题若被恶意利用，可能造成未授权访问。


## 6. 功能请求与路线图信号

### 高潜力纳入下一版本（v0.9.0）的功能

| 功能 | Issue/PR | 状态 | 信号强度 |
|------|----------|------|----------|
| **OpenAI Chat Completions 协议兼容** | #8603 | accepted | 高——社区讨论热度高（23 评论），兼容主流客户端将大幅拓展生态 |
| **Goal mode（多轮有界任务执行）** | #8303 | accepted | 高——增强 agent 核心能力，已有 👍 1 |
| **Agent 导出为可移植 bundle** | PR #9986 | open（needs-author-action） | 中——方便 agent 跨安装迁移，功能完整度高 |
| **每模型能力与上下文窗口配置** | #7100 | accepted | 中——解决视觉支持误报和上下文窗口硬编码问题 |
| **统一包/能力/配置/运行时目录契约** | #9346 | accepted | 中——为插件生态铺路 |
| **运行时会话与传输适配器** | #9487 | open（needs-maintainer-review） | 中——运行时拥有会话，解耦传输层 |
| **统一附件架构** | #9488 | open（needs-author-action） | 中——与 #9487 配套 |
| **Hailo-Ollama 原生支持** | PR #9109 | open | 低——硬件加速推理集成，needs-author-action |
| **ZeroCode 文件资源管理器搜索键盘导航** | PR #10065 | open（今日新增） | 低——小的 UX 修复 |
| **ZeroCode Option-Backspace 词删除** | #10059 | open（good first issue） | 低——macOS 用户 UX 改进 |

### 路线图信号判断
- **协议兼容层是大方向**：#8603 若落地，ZeroClaw 将可作为 OpenAI 协议的 drop-in 替代，这是一个重要的生态扩张信号。
- **v0.9.0 是安全架构大版本**：多个安全相关 RFC（#7141、#7142、#6971）均标注 v0.9.0 目标，预计 breaking changes 会集中在该版本。
- **插件化/轻量化趋势**：#6165（轻量核心+外部集成）获得持续关注，配合 #9346 的目录契约，ZeroClaw 可能在 v0.9.x 系列走向更模块化的架构。


## 7. 用户反馈摘要

### 从 Issues 评论中提炼的用户之声

1. **协议兼容是刚需**（来自 #8603）
   > "Clients that speak the OpenAI Chat Completions protocol — Open WebUI, LobeChat, Continue.dev, Aider, LangChain, the OpenAI SDK, and many others..." — 用户明确列出广泛使用的客户端生态，说明 ZeroClaw 目前的 WebSocket/ACP/webhook 接口无法被主流 LLM 工具直接调用。

2. **安全审计正在紧锣密鼓进行**（来自 #7155 等）
   多个安全相关 RFC 持续更新（#7155 Rev 3、#7141 Rev 8、#7142 Rev 6），且全部标注风险 high，并有维护者参与评审。说明社区对安全加固工作高度配合且推进节奏紧凑。

3. **希望简化治理流程**（来自 #9496）
   > "ZeroClaw's RFC process has become slower and more cumbersome than the decisions it is meant to support." — 用户对 7 天讨论期和全体共识要求感到流程负担，期望更高效的决策机制。

4. **运维痛点：配置生效需要 daemon 重载**（来自 #7897）
   用户指出配置保存成功并不等于安全策略/通道/会话等子系统已实际生效，需要 `/admin/reload` 才能重建。这是一个运维侧的实时性问题。

5. **测试与 CI 基础设施的反馈**（来自 #10039 等）
   CI 改进类 PR 频繁且快速合并，说明维护者对 CI 可靠性有较高要求，社区反馈正向。

### 综合判断
用户群体呈两极化分布：一类是**企业级使用者**，关注安全、认证、治理流程；另一类是**开发者/爱好者**，关注协议兼容、多轮任务、模型接入。前者推动 ZeroClaw 走向生产可用，后者推动其生态扩张。两者目前都有代表性问题在社区讨论中保持高热度。


## 8. 待处理积压

### ⚠️ 需维护者关注的重要积压项

**P1 优先级：**
- **#7141** — RFC: Pluggable inbound authentication and canonical principals（Rev 8，accepted，in-progress）
  - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7141
  - **积压时长：** 76 天
  - **风险：** 高，v0.9.0 身份与访问里程碑的核心依赖

- **#7100** — RFC: Per-model capability & context-window config（accepted，13 评论）
  - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7100
  - **积压时长：** 77 天
  - **风险：** 高

- **#9397** — RFC: WhatsApp empty allowed_groups = permit-none（accepted，in-progress）
  - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/9397
  - **风险：** 安全漏洞，空列表当前放行所有群组

**长时间 RUNNING 的 RFC：**
- **#6808**（76 天，Rev 26）— 治理类 RFC 持续时间过长，需关注收敛
- **#6165**（113 天）— 轻量核心 RFC，需维护者明确方向

**需作者响应的 PR：**
- **#9986**（feat: export agent to portable bundle）— needs-author-action，功能完整度高
- **#9109**（feat: add native Hailo-Ollama support）— needs-author-action，已搁置 32 天
- **#9314**（fix(telegram): advance long-poll offset only after delivery）— P1 bug fix，已打开 26 天，XL size
- **#10003**（fix(providers): account Reliable rejected attempts exactly）— XL size，待评审
- **#10021**（fix(runtime): apply target thinking to independent delegates）— 待评审

### 观察
- **积压风险：** 超过 30 天的 RFC 多集中在安全架构和认证领域，是 v0.9.0 的基石，若持续不收敛可能影响版本节奏。
- **PR 积压：** 34 条待合并 PR 中，至少有 5 条 size 为 L 或 XL，包含依赖升级（#9808 一次 46 个 crate 更新）和大型功能（#9986、#9109、#9314），需维护者评估是否分流处理。
- **测试债务：** #10011 是 help wanted 任务，但不影响主线功能，可暂缓。

---

*数据截至 2026-08-18 00:00 UTC。报告基于公开 GitHub 数据自动生成，仅供参考。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*