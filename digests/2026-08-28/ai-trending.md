# AI 开源趋势日报 2026-08-28

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-08-28 07:19 UTC

---

# 🤖 AI 开源趋势日报（2026-08-28）

> 数据来源：GitHub Trending + 主题搜索 | 筛选去除非 AI 项目后共 90+ 个仓库


## 一、今日速览

今日开源社区的核心关键词是 **“Agent Skills 生态”**——从 Anthropic 官方插件目录发布，到 Trending 上大量 `*-skills` 仓库霸榜，一场围绕“如何让 Agent 更专业”的基础设施竞赛正在全面展开。与此同时，**Agent 记忆**（claude-mem 登顶、上榜 Rag 主题双榜）与**上下文压缩**（headroom、caveman）成为新焦点，反映出社区对 Agent 长期运行成本与持续性的关切。**视频生成/剪辑**（OpenMontage、OpenCut、GPT-Image-2 相关模板库）与 **AI 个人知识管理**（claude-obsidian、siyuan）是今日的另一条主线，AI 正在从“写代码”加速渗透到“做视频”和“管知识”等更广泛的生产力场景。此外，开源 Agent 框架呈现多语言繁荣：Rust（CodeWhale、rig）、Go（DeepSeek-Reasonix）、Java（langchain4j）均有代表项目涌现。


## 二、各维度热门项目

### 🔧 AI 基础工具（框架 / SDK / CLI / 推理引擎）

| 项目 | Stars（+今日） | 一句话说明 |
|---|---|---|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐237,454 | “会成长的 Agent”框架，高星社区标杆项目，主打长期自适应能力 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐145,164 | Agent 工程的标准平台，今日同时出现在 RAG 与工具两个主题下，生态地位稳固 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐164,539 | 模型定义与推理的事实标准框架，覆盖文本/视觉/音频/多模态 |
| [marin-community/marin](https://github.com/marin-community/marin) | ⭐0（+255 today） | 开源基础模型研发框架，面向研究社区，今日冲入 Trending，预示训练工具链走向工程化 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐173,344 | 为 LLM 构建的 Web 上下文 API，搜索、抓取、交互一站式，是 Agent 获取实时数据的关键管道 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐8,433 | Rust 生态的 LLM 应用开发框架，模块化设计，关注性能与类型安全 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars（+今日） | 一句话说明 |
|---|---|---|
| [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | ⭐0（+292 today） | Anthropic 官方管理的 Claude Code 插件目录，相当于 Agent 生态的“官方应用商店”，今日首发即登榜 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐186,954 | 自动化 Agent 的元老级项目，持续迭代，愿景是让每个人都能构建和使用 AI |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐111,519 | 让 AI Agent 像人一样操作浏览器，是 Agent 落地执行层的关键组件 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐243,811 | Agent “性能优化系统”，为 Claude Code、Codex、Cursor 等提供技能、记忆、安全与研发流程管理 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐0（+229 today） | 多智能体 LLM 金融交易框架，今日登榜 Trending，显示 Agent 在垂直金融场景的应用潜力 |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | ⭐40,591 | 构建弹性 Agent 的底层编排框架，适合复杂状态机与多步工作流 |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | ⭐47,479 | 超轻量自托管个人 AI Agent 框架，支持 MCP、多智能体与自动化，安装极简 |
| [Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents) | ⭐6,207 | “原子化”构建 AI Agent 的组合式方法论与实现，强调可复用最小单元 |

### 📦 AI 应用（垂直场景 / 生产力工具）

| 项目 | Stars（+今日） | 一句话说明 |
|---|---|---|
| [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) | ⭐0（+1292 today） | 全球首个开源 Agentic 视频制作系统，12 条生产管线、100+ 工具，把 AI 编程助手变成视频工作室，今日新增 1292 stars |
| [OpenCut-app/OpenCut](https://github.com/OpenCut-app/OpenCut) | ⭐0（+478 today） | 开源版 CapCut（剪映），今日登榜 Trending，配合 AI 视频生成热潮形成工具链闭环 |
| [freestylefly/awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2) | ⭐0（+2096 today） | GPT-Image2 工业级提示词引擎与模板库，530+ 逆向工程案例，今日暴涨 2096 stars |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐51,174 | AI 生产力工作室：统一接入前沿 LLM，内置 300+ 助手与自主 Agent |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | ⭐64,161 | LLM 驱动的多市场股票智能分析系统，零成本定时运行，Agent 在金融信息处理方面的落地代表 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐49,924 | AI 将文档/主题转化为原生 PowerPoint，支持动画、数据图表与音频旁白 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | ⭐68,977 | 开源 AI 求职助手：扫描职位、评估打分、定制简历、追踪申请，在 CLI 内本地运行 |
| [rohitg00/ai-engineering-from-scratch](https://github.com/rohitg00/ai-engineering-from-scratch) | ⭐0（+552 today） | AI 工程从零到实战的学习路径，双向登榜 Trending 与 ML 主题，作为系统性入门资源深受欢迎 |

### 🧠 大模型 / 训练（权重、训练框架、微调、评测）

| 项目 | Stars（+今日） | 一句话说明 |
|---|---|---|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐179,604 | 本地运行大模型的事实标准，已支持 Kimi、GLM、DeepSeek、Qwen 等最新模型 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | ⭐102,635 | 深度学习训练的基石框架，今日在 ML 主题搜索中仍居高位 |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | ⭐197,751 | 经典机器学习框架，社区体量依旧庞大 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | ⭐103,931 | 从零手写类 ChatGPT LLM 的经典教程库，是学习大模型内部机制的首选 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,372 | 支持 100+ 数据集的主流 LLM 评测平台，覆盖 Llama、GPT、Qwen、GLM 等 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,526 | 面向系统工程师的微型 LLM 推理系统教程，在 Apple Silicon 上构建“微型 vLLM + Qwen” |
| [AIDASLab/Awesome-Diffusion-LLM](https://github.com/AIDASLab/Awesome-Diffusion-LLM) | ⭐98 | 大语言扩散模型（Diffusion LLM）论文清单，追踪前沿生成范式的学术资源 |
| [thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL) | ⭐1,801 | Agentic RL（智能体强化学习）精选列表，反映 Agent 训练从模仿到强化的发展趋势 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars（+今日） | 一句话说明 |
|---|---|---|
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐150,187 | 用户友好的 AI 界面层，支持 Ollama/OpenAI API，是自托管 RAG 应用最流行的前端 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | ⭐111,702 | 将代码库/文档/SQL 模式转为可查询知识图谱，本地确定性 AST 解析，无需向量库，今日在 RAG 主题中高居第二 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐89,445 | 领先的开源 RAG 引擎，深度融合 Agent 能力，为 LLM 提供高质量上下文层 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐92,391（+143 today） | 跨会话持久化 Agent 记忆：捕获→AI 压缩→注入未来会话，热榜+主题双上榜，今日 trending +143 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐64,229 | 为 AI Agent 设计的通用记忆层，解决长期对话与个性化问题 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐45,844 | 高性能云原生向量数据库，专为海量向量 ANN 检索而建，是 RAG 架构的存储基座 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐34,234 | Rust 编写的高性能向量数据库与检索引擎，支持云原生部署 |
| [AgriciDaniel/claude-obsidian](https://github.com/AgriciDaniel/claude-obsidian) | ⭐0（+634 today） | AI 第二大脑：让 Claude 自动阅读、链接并归档 Obsidian 中的知识为知识图谱，今日新增 634 stars |


## 三、趋势信号分析

**① Agent Skills 生态的“标准化时刻”已到来。** 今日 Trending 榜单中 `*-skills` 命名的仓库多达 5 个（archify、scientific-agent-skills、garden-skills、awesome-claude-skills、claude-plugins-official），加上主题搜索中的 ECC、Graphify 等，标志着 Agent 能力封装正从个人脚本走向标准化交付。Anthropic 官方插件目录的发布是标志性事件：头部厂商开始主导插件规范，“Agent 应用商店”模式初具雏形。

**② Agent 长期记忆与上下文成本成为新的痛点与机会点。** claude-mem（双榜上榜、今日持续增长）、headroomlabs-ai/headroom（减少 60-95% token）、caveman（削减 65% token）等项目的活跃，揭示社区关注重心正从“Agent 能做什么”转向“Agent 能持续低成本地做什么”。这一赛道与长上下文模型（如 Kimi、Gemini）的普及形成有趣的张力。

**③ “AI 视频 + 提示词工程”成为新的内容创作引爆点。** OpenAI GPT-Image-2 相关模板库单日 +2096 stars，OpenMontage（Agentic 视频制作）+1292，OpenCut（开源剪映）+478 — 一套完整的 AI 视频生产链路（生成→剪辑→分发）正在开源社区快速成形。

**④ AI 个人知识管理（PKM）赛道升温。** claude-obsidian（+634 today）将 Obsidian 与 Claude Code 结合，构建“自组织 AI 第二大脑”；思源笔记（siyuan）也在 AI Agent 协作方向上深耕。知识管理正成为 Agent 落地 C 端用户的高频场景。

**⑤ 开源 Agent 框架的多语言化态势明显。** Rust（CodeWhale、rig）、Go（DeepSeek-Reasonix）、Java（langchain4j）均有优质代表项目，说明 Agent 开发正从 Python 单极走向全栈工程化，不同语言生态开始形成各自的 Agent 技术栈。


## 四、社区关注热点

- **Claude Code 插件生态（今日最热）：** Anthropic 官方插件目录 + 社区聚合列表（awesome-claude-skills）同时上榜，建议关注插件开发规范与分发机制，这是下一波 Agent 工具分发的入口。
- **智能体记忆基础设施（持续升温）：** claude-mem 双榜登顶、mem0 生态持续扩展，长期记忆是 Agent 从“玩具”走向“生产力工具”的关键瓶颈，也是后续商业化潜力最大的方向之一。
- **Agentic 视频生成（新兴爆发点）：** OpenMontage 单日 +1292 stars 首次登榜，配合 OpenCut（开源剪辑）与 GPT-Image-2 提示词库的爆火，AI 视频生产工具链值得重点关注。
- **上下文压缩与 Token 优化（务实刚需）：** headroom（压缩 60-95% JSON token）与 caveman（减少 65% token）等高 ROI 项目受到社区追捧，在模型 API 成本仍高的背景下，这类“省钱工具”会持续获得关注。
- **开源基础模型研发框架（前沿研究方向）：** marin-community/marin 作为基础模型研发框架进入 Trending，结合 open-compass 评测平台与 AgentsMeetRL（Agentic RL）的活跃，社区正从“用模型”向“造模型/训 Agent”纵深推进。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*