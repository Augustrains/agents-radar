# ArXiv AI 研究日报 2026-08-22

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-22 00:29 UTC

---

# 📊 ArXiv AI 研究日报 — 2026-08-22

> 本期共收录 50 篇论文，覆盖 LLM 未学习、递归自我改进、智能体路由优化等领域。

---

## 📌 今日速览

今日投稿呈现三大焦点：**递归自我改进（RSI）** 与**模型未学习（Unlearning）** 成为评估与基准研究的热点，分别有多个工作提出系统化评测框架；**智能体与工具使用**方向持续升温，出现从计算机使用痕迹诱导任务模型、跨任务技能迁移到自适应推理预算分配等一系列工作；此外，**法律 AI** 和**医疗 AI** 等垂直领域基准（如 InsufficiencyBench、ContractScrub、OenoBench）密集发布，标志着 LLM 评估正从通用能力向领域深度与真实场景复杂性延伸。

---

## 🔍 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models**
🔗 http://arxiv.org/abs/2608.20338v1
👤 Sahil Kale, Ian Harris
💡 首个评估 LLM 上下文敏感未学习能力的基准，弥补了现有方法仅关注独立事实删除的不足。

**2. Phantom Gains: Auditing Self-Improvement Against a Measured Null**
🔗 http://arxiv.org/abs/2608.20290v1
👤 Cheng Xu, Nan Yan, Liming Chen et al.
💡 揭示自改进评估中逐个问题差分统计的测量伪影问题，提供了审计自我提升真实性的方法框架。

**3. When Text and Numbers Disagree: Evidence Arbitration in Large Language Models**
🔗 http://arxiv.org/abs/2608.20116v1
👤 Mattia Carletti, Edward Phillips, Fredrik K. Gustafsson et al.
💡 通过受控合成实验研究 LLM 在文本摘要、数值观测与外部工具输出冲突时的证据仲裁行为。

**4. Daedalus-150M: A Convolution-Attention Hybrid Designed for CPU Inference**
🔗 http://arxiv.org/abs/2608.20210v1
👤 Christos Koutsiaris
💡 以 CPU 推理为目标的小模型设计范式，在 18 个块中仅 6 个使用全注意力，为边缘部署提供新思路。

**5. OenoBench: A Wine-Domain Benchmark for Knowledge-Grounded Evaluation of Large Language Models**
🔗 http://arxiv.org/abs/2608.20106v1
👤 Nikita Khudov
💡 葡萄酒领域知识基准，包含 3,266 道题、六大学科支柱与四层难度，由 38,104 条来源锚定事实构建。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**6. AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement**
🔗 http://arxiv.org/abs/2608.20318v1
👤 Yizhe Chi, Wenyi Li, Deyao Hong et al.
💡 针对递归自我改进的算法设计任务基准，评估智能体能否改进产生自身的训练算法。

**7. Inducing Task Models from Computer-Use Traces**
🔗 http://arxiv.org/abs/2608.20319v1
👤 Yucheng Jiang, Zora Zhiruo Wang, Ruishi Chen et al.
💡 从自然计算机使用痕迹中归纳符号化、可审计的任务模型，助力计算机使用智能体学习新任务。

**8. MidTool: Mid-training Data Synthesis for Agentic Tool Use**
🔗 http://arxiv.org/abs/2608.20314v1
👤 Fengqing Jiang, Yite Wang, Boyi Liu et al.
💡 针对智能体工具使用的中间训练数据合成方法，提升模型在软件工程等推理密集型智能体任务上的能力。

**9. Learning When to Think: Adaptive Reasoning for Test-Time Compute Allocation**
🔗 http://arxiv.org/abs/2608.20256v1
👤 Gijs Kassenaar, Zhao Yang, Vincent François-Lavet
💡 研究推理模型能否学习自主分配计算预算，在简单问题上减少过度计算、在困难问题上增加推理深度。

**10. Break It Down, Pass It On: Cross-Task Skill Transfer in LLM Agents**
🔗 http://arxiv.org/abs/2608.20274v1
👤 Yiyang Feng, Biddut Sarker Bijoy, Niranjan Balasubramanian et al.
💡 系统研究了智能体诱导技能在跨任务迁移中的可靠性与边界条件，识别了技能转移有效与有害的情形。

**11. Task-Coevolve: Efficient Harness Optimization via Adaptive Validation Task Selection**
🔗 http://arxiv.org/abs/2608.20169v1
👤 Atsuyuki Miyai, Kiyoharu Aizawa, Toshihiko Yamasaki
💡 通过自适应验证任务选择实现高效的 LLM 智能体 harness 优化，无需更新模型权重即可获得性能提升。

**12. Multi-Agent Orchestration with the Common-Sense Reasoning Capabilities of LLMs for Autonomous Driving**
🔗 http://arxiv.org/abs/2608.20129v1
👤 Mehdi Azarafza, Faezeh Pasandideh, Ali Ehteshami Bejnordi et al.
💡 利用 LLM 的常识推理能力编排多智能体系统，增强自动驾驶在未见场景中的上下文推理能力。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**13. Pandora's AI Model Routing Box: Efficient Allocation with Costly Value Estimation**
🔗 http://arxiv.org/abs/2608.20316v1
👤 Adam Fisch, Shubhendu Trivedi, Fantine Huot et al.
💡 在异构 AI 系统中进行查询路由时，如何平衡估计各专家模型价值的成本与收益，提出高效分配策略。

**14. Exact Algebraic Computation of Learning Coefficients for Two-Dimensional Singular Models**
🔗 http://arxiv.org/abs/2608.20183v1
👤 Grégoire Sergeant-Perthuis, Elias Tsigaridas, Jules Tsukahara
💡 为二维奇异模型的学习系数提供精确代数计算方法，改进 WBIC 在深层学习等奇异模型中的模型选择表现。

**15. DICS: Data-Informed Centroid Splitting for Decision Tree Classifiers**
🔗 http://arxiv.org/abs/2608.20258v1
👤 MD Saifur Rahman Mazumder, Feng Yu
💡 提出数据知情质心分裂方法，避免决策树训练中对候选分裂点的穷举搜索，显著降低大规模高维数据的计算开销。

---

### 📊 应用（垂直领域、多模态、代码生成）

**16. G-CARL: Grounded Checklist-Aligned Reward Learning for Patient-Oriented Medical Report Interpretation**
🔗 http://arxiv.org/abs/2608.20331v1
👤 Shiao Xie, Siyu Chen, Jianwei Lv et al.
💡 面向患者个性化医疗报告解读的对齐奖励学习方法，同时兼顾医学事实性与患者沟通情境。

**17. InsufficiencyBench: Evaluating LLM legal advice on underspecified user queries**
🔗 http://arxiv.org/abs/2608.20220v1
👤 Samuel J. Vincent, Daniel Calloway, Fangyi Yu et al.
💡 首个针对查询信息不足场景的法律建议评估基准，填补了现有法律基准假设查询充分指定的空白。

**18. ContractScrub: A benchmark for final review of legal contracts**
🔗 http://arxiv.org/abs/2608.20204v1
👤 Yejin Bang, Kirsty Fielding, Brandan Oliver et al.
💡 针对合同"最终审查"（擦除）任务的基准，评估 LLM 发现交易协议中错误与不一致的能力。

---

## 📈 研究趋势信号

今日投稿呈现多个值得关注的新兴信号：**递归自我改进（RSI）从概念走向可评测**（AI4AI-Bench、Phantom Gains 对自改进的审计）；**"小即快"的架构定制化设计**（Daedalus-150M 以 CPU 为先的设计思路）与**计算自适应分配**（Learning When to Think）共同指向推理效率的精细化控制；**领域基准的"信息充分性"转向**——法律领域的 InsufficiencyBench 和 ContractScrub 显示评估正从"问题是否答对"走向"信息不足时是否主动追问"；此外，**检索增强的替代路径**（Inject, Align, Recover 的文档知识内化）与**AI 模型路由**（Pandora's Box）也反映出对部署阶段资源优化的关注度显著提升。

---

## 📚 值得精读

**1. AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement**
🔗 http://arxiv.org/abs/2608.20318v1
递归自我改进是 AI 安全与能力研究的核心议题之一，本工作首次将其落到可执行的基准层面，值得全文精读以理解其任务设计、评估协议及对 RSI 可行性的启示。

**2. Phantom Gains: Auditing Self-Improvement Against a Measured Null**
🔗 http://arxiv.org/abs/2608.20290v1
当"模型是否自我改进"成为评估核心时，统计严谨性至关重要。该文对逐个问题差分评估中测量伪影的系统分析，对任何从事模型迭代评估的研究者都有方法论参考价值。

**3. ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models**
🔗 http://arxiv.org/abs/2608.20338v1
LLM 未学习（unlearning）是安全对齐的关键技术方向，但现有评估框架过于简化。ConceptGuard 引入上下文敏感设定，为未学习研究提供了更贴近实际部署场景的评测基础。

---

> 📮 本日报由 AI 研究分析师自动生成，仅代表对当日论文的初步筛选与解读。完整论文列表请参见文首目录。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*