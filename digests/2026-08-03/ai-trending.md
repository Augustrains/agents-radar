# AI 开源趋势日报 2026-08-03

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-08-03 01:25 UTC

---

# 🤖 AI 开源趋势日报

**日期：2026年8月3日** | **数据来源：GitHub Trending + AI主题搜索** | **筛选规模：94个仓库 → 76个AI相关项目**


## 一、今日速览

今日 AI 开源社区呈现三大显著动向：**Agent 生态持续白热化**——围绕 Claude Code、Coder、OpenCode 等 CLI 编码Agent的“技能包”（Skill）、记忆共享模块和Agent工具链密集涌现，腾讯云发布的团队级记忆中心 TencentDB Agent Memory 在 Trending 上单日获 602 stars；**轻量化本地推理成为硬需求**——antirez 的 DeepSeek 4 本地推理引擎 ds4 和 AirLLM 的单卡 4GB 显存跑 70B 模型方案分别单日增长 139 和 819 stars，印证了社区对降低大模型硬件门槛的迫切渴望；**“AI Agent + 信息检索”正在标准化为通用模块**——Agent-Reach（零 API 费用全网检索 CLI）单日飙升 659 stars，last30days-skill 和 reverse-skill 分别从社交媒体深度研究和安全渗透两个方向展示了“技能包”模式的横向扩展能力。微软《AI 初学者》课程以 2629 的单日新增 stars 登顶榜单，显示 AI 教育内容仍是长期刚需。开源 LLM 权重生态格局已形成 Ollama（Kimi/K2.6、GLM-5.2、MiniMax、DeepSeek、gpt-oss、Qwen、Gemma 多模型支持）一统本地运行入口的局面。


## 二、各维度热门项目

### 🔧 AI 基础工具（12个）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 177,618 | 本地 LLM 运行事实标准，已支持 Kimi-K2.6、GLM-5.2、MiniMax、DeepSeek 等全系列主流模型，本月继续巩固其“模型入口”地位。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 163,262 | 模型定义与训练/推理框架的行业标杆，覆盖文本、视觉、音视频和多模态。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 159,556 | 面向 Agent 的可规模化 Web 搜索/抓取/交互 API，已成为 Agent 联网能力的核心基础设施。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 87,978 | 高吞吐、内存高效的 LLM 推理服务引擎，生产环境部署的事实标准。 |
| [antirez/ds4](https://github.com/antirez/ds4) | **今日+139** | Redis 作者 antirez 新作——DeepSeek 4 Flash/PRO 本地推理引擎，支持 Metal/CUDA/ROCm 三后端，今日首次登榜 Trending。 |
| [lyogavin/airllm](https://github.com/lyogavin/airllm) | **今日+819** | 单张 4GB 显存即可推理 70B 参数大模型，是边缘设备和消费级硬件部署的关键突破口。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 237,077 | Agent 性能优化系统：为 Claude Code/Codex/Opencode/Cursor 等提供技能、本能、记忆和安全模块。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 101,113 | 将任意代码库/文档/SQL Schema 转换为可查询知识图谱，本地确定性 AST 解析，无需向量库。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,431 | 面向系统工程师的 LLM 推理服务教学项目，在 Apple Silicon 上从零构建 mini-vLLM + Qwen。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 8,143 | Rust 生态的模块化 LLM 应用开发框架，面向性能敏感场景。 |
| [googleworkspace/cli](https://github.com/googleworkspace/cli) | 30,162 | Google Workspace 官方 CLI，内置 AI agent skills，打通 Drive/Gmail/Calendar 等办公套件。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,259 | LLM 评测平台，支持 100+ 数据集和多模型对比（Llama3/Qwen/GLM/Claude/GPT-4 等）。 |


### 🤖 AI 智能体/工作流（16个）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,774 | 通用 AI Agent 平台的元老级项目，“人人可用的 AI”愿景的早期布道者。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 143,255 | Agent 工程平台，从编排框架演进为完整的智能体开发生态。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 107,621 | 让 AI Agent 像人一样操作浏览器的核心工具，自动化在线任务的关键层。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | 129,856 | 100+ 免费开源的 AI Agents、Agent Skills 和 RAG 应用合集，是 Agent 开发的灵感库。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 224,330 | “与你一起成长的Agent”——强调持续学习和自我进化的 Agent 框架。 |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 72,999 | “Bash is all you need”——从0到1构建纳米版 Claude Code 风格 Agent harness 的教学项目。 |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 46,279 | 开源超级 AI 助手与 Agent Harness（原 chatgpt-on-wechat），支持多模型多平台、工具调用、记忆自进化。 |
| [different-ai/openwork](https://github.com/different-ai/openwork) | **今日+280** | Claude Cowork 的开源替代品（基于 opencode），今天首次登榜 Trending，值得关注。 |
| [zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill) | **今日+1,141** | 逆向/渗透/安全研究技能路由包，AI 自动路由+按需工具链引导+自进化知识库，支持多款代码 AI 客户端——今日最高增速之一。 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | **今日+659** | 一条 CLI 让 Agent 读遍 Twitter/Reddit/YouTube/GitHub/B站/小红书，零 API 费用——打通全平台信息获取。 |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | **今日+206** | AI Agent 技能包：跨 Reddit/X/YouTube/HN/Polymarket 等平台检索主题并合成带依据的摘要。 |
| [NomaDamas/k-skill](https://github.com/NomaDamas/k-skill) | **今日+177** | 韩语 AI Agent 技能包合集，让 Agent 更懂韩语用户——本地化 Agent 技能包的典型案例。 |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | **今日+602** | 腾讯云开源的团队级 Agent 记忆中心：将对话/文档/代码转化为“Chat Memory / Skill / LLM-Wiki / Code-Graph”四种复用资产。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49,300 | AI 生产力工作室：智能聊天+自主Agent+300+助手，统一接入前沿 LLM。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 36,407 | Agent 与生成式 UI 的前端技术栈，支持 React/Angular/Mobile/Slack，AG-UI 协议发起者。 |
| [datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents) | 70,160 | 《从零开始构建智能体》中文教程，数据开源社区 Datawhale 出品。 |


### 📦 AI 应用（14个）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [microsoft/AI-For-Beginners](https://github.com/microsoft/AI-For-Beginners) | **今日+2,629** | 12周24课时的 AI 入门课程，今日 Trending 第一名——微软 AI 教育系列的持续热度。 |
| [microsoft/generative-ai-for-beginners](https://github.com/microsoft/generative-ai-for-beginners) | **今日+588** | 21课时的生成式 AI 入门课程，与 AI-For-Beginners 形成姊妹篇。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 151,107 | Agentic 工作流+RAG 流水线的一站式协作平台，支持云部署/VPC/自托管。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 147,646 | 用户友好的 AI 交互界面，支持 Ollama/OpenAI API 等，是本地模型部署首选前端。 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 101,200 | AI 一键生成高清短视频，自动化工作流驱动的创作工具。 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 59,877 | LLM 驱动的多市场股票智能分析系统，支持多源行情、实时新闻和自动推送。 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 71,299 | 面向分析师/量化交易者和 AI Agent 的开放数据平台。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 42,575 | AI 将文档/主题自动转为原生 PowerPoint（含动画、图表、配音和数据驱动内容）。 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 62,555 | 开源 AI 求职助手：扫描职位→结构化评分→定制简历→追踪申请，本地运行。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 29,338 | 个人交易 Agent——“氛围感交易”的 AI 化实践。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49,300 | AI 生产力工作室：智能聊天+自主 Agent+300+助手，统一接入前沿 LLM。 |
| [deepfakes/faceswap](https://github.com/deepfakes/faceswap) | 57,205 | 开源 Deepfake 软件，计算机视觉在图像/视频领域的经典应用。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 60,134 | YOLO26/YOLO11/YOLOv8 目标检测、分割、姿态估计的完整工具链。 |
| [roboflow/supervision](https://github.com/roboflow/supervision) | 48,546 | 可复用的计算机视觉工具集，简化检测/跟踪/标注的工程实现。 |


### 🧠 大模型/训练（8个）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 102,139 | 动态神经网络与 GPU 加速的深度学习框架标准。 |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 196,671 | 面向所有人的开源机器学习框架。 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 100,395 | 从零开始用 PyTorch 逐行实现 ChatGPT 类 LLM 的经典教程。 |
| [keras-team/keras](https://github.com/keras-team/keras) | 64,217 | “为人类设计的深度学习”框架，Keras 3 支持多后端。 |
| [scikit-learn/scikit-learn](https://github.com/scikit-learn/scikit-learn) | 66,854 | Python 机器学习经典库，与 LLM 生态互补的传统 ML 工具集。 |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) | **今日+333** | 面向 DeepSeek 原生的终端 AI 编码Agent，围绕前缀缓存稳定性设计，可常驻运行——为 DeepSeek 模型深度优化。 |
| [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) | 59 | 纯 Rust + Candle 从零实现的 Decoder-only LLM，支持 Gated DeltaNet + 稀疏注意力 + MoE，最小 25M 可运行。 |
| [genieincodebottle/generative-ai](https://github.com/genieincodebottle/generative-ai) | 2,582 | 生成式 AI 综合资源库：包含路线图、项目实战、用例、面试准备。 |


### 🔍 RAG/知识库（11个）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|------------|
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 51,321 | 领先的文档 Agent 和 OCR 平台，RAG 生态的核心框架。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 86,636 | 开源 RAG 引擎先驱，融合 RAG + Agent 能力为 LLM 提供上下文层。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,470 | 云原生向量数据库，为大规模向量 ANN 搜索而构建。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 62,335 | AI Agent 的通用记忆层——跨会话持久化记忆的解决方案。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 33,728 | 高性能大规模向量数据库与搜索引擎，支持云服务。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 29,708 | 开源 AI 记忆平台：基于知识图谱引擎，为 Agent 提供跨会话长时记忆。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 89,343 | Agent 跨会话持久上下文——捕获会话内容、AI压缩、注入未来会话，支持8+ CLI Agent。 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,682 | 云原生向量数据库，对象+向量混合存储，支持结构化过滤。 |
| [NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques) | 28,915 | 系统展示 40+ 种进阶 RAG 技术（每个技术均附详细教程 notebook）。 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | 34,969 | 无向量、基于推理的 RAG 文档索引方案——为 RAG 提供新范式。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 12,761 | MLsys2026 论文项目：RAG on Everything，节省97%存储，全私有运行。 |


## 三、趋势信号分析

**集群一：“Agent 技能包”模式正在爆发。** 今日 Trending 上有 6+ 个仓库直接以 skill/skill router 命名（reverse-skill、last30days-skill、k-skill、TencentDB-Agent-Memory），且都声明支持 Claude Code / Cursor / Cline 等主流 CLI Agent。这表明 Agent 生态正从“框架竞争”进入“能力插件化”阶段——就像 VS Code 的插件市场正在形成。

**集群二：Agent 记忆成为新基建。** mem0（62K stars）、claude-mem（89K stars）、cognee（29K stars）和腾讯云的 TencentDB-Agent-Memory（当日新增 602）同时发力“持久记忆”赛道。记忆层正在成为继 RAG 之后的下一波核心抽象。

**集群三：DeepSeek 生态形成完整工具链。** 从 ds4 本地推理引擎（antirez 加持）、DeepSeek-Reasonix 编码 Agent（今日 +333），到 Ollama 对 DeepSeek 的原生支持——DeepSeek 的开源生态已具备“模型-推理-应用”三层结构。

**趋势信号：** “本地优先 + 轻量化”仍是主旋律（4GB 显存跑 70B 的 airllm 今日 +819），同时“多平台信息聚合”能力（Agent-Reach 今日 +659）成为 Agent 差异化竞争的新焦点。


## 四、社区关注热点

- **腾讯云的 Agent 记忆中心（TencentDB-Agent-Memory）**——首个将对话/文档/代码统一转化为四种可治理、可共享记忆资产的团队级方案，云厂商入局 Agent 基础设施的标志性事件。需持续观察其与 mem0、claude-mem 的开源生态竞争态势，以及是否会推出配套云服务。

- **antirez 的 ds4**——Redis 作者的个人品牌+ DeepSeek 4 的硬件支持矩阵（Metal/CUDA/ROCm），可能成为 Mac 用户本地跑 DeepSeek 的首选方案。

- **AirLLM 单卡 4GB 跑 70B**——如真实可用，将彻底改变中小开发者的模型使用门槛，值得第一时间实测。

- **reverse-skill（+1,141 stars）**——AI 编码Agent 在安全攻防领域的首次大规模应用，其“自进化经验库”设计可能成为垂直领域技能包的模板。

- **向量数据库领域的“轻量级”趋势**——ECL 框架（237K stars）与 PageIndex 等“无向量 RAG”方案同时走红，表明社区对摆脱重型向量库依赖的渴望。ECL 作为 Agent 性能优化系统的走红，也标志着“Agent 工程化”赛道的正式成型。

---

*报告完 | 数据截至 2026-08-03 GitHub Trending & AI Topic Search*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*