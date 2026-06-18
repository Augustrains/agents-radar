# ArXiv AI 研究日报 2026-06-18

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-18 02:14 UTC

---

好的，作为AI研究分析师，以下是根据您提供的2026年6月18日ArXiv论文列表整理的《ArXiv AI 研究日报》。

---

### **ArXiv AI 研究日报 | 2026-06-18**

#### **今日速览**

今日论文展现了AI研究的两个显著趋势：**智能体系统向复杂协作与工业落地迈进**，涌现出关于通信协议、团队领导力、以及具体行业（如打车、搜救）的多智能体研究；同时，**强化学习（RL）在后训练阶段的应用深度与精细化程度提升**，不仅用于提升推理能力，更被用于数据合成、信用分配和创意生成。此外，**AI for Science**方向持续产出高质量成果，涵盖催化剂构型发现、材料光谱预测和科学安全基准建立，显示了AI在基础科学领域的强大渗透力。

---

#### **重点论文**

##### 🧠 **大语言模型（架构、训练、对齐、评估）**

1.  **Human-AI Coevolution Dynamics: A Formal Theory of Social Intelligence Emergence Through Long-Term Interaction**
    - **作者:** Jingyi Zhou et al.
    - **链接:** http://arxiv.org/abs/2606.19144v1
    - **一句话说明:** 提出人机协同演化理论，为长期交互中涌现的社会智能（如协作、情感动态）提供了形式化框架，超越了传统的孤立组件式建模。

2.  **Scaling Learning-based AEB with Massive Unlabeled Data**
    - **作者:** Xiangyu Wang et al.
    - **链接:** http://arxiv.org/abs/2606.18864v1
    - **一句话说明:** 提出了元反馈半监督学习方法，展示了利用海量未标注数据大规模提升学习型自动紧急制动（AEB）系统性能的可行性路径。

3.  **ThinkDeception: A Progressive Reinforcement Learning Framework for Interpretable Multimodal Deception Detection**
    - **作者:** Jinhao Song et al.
    - **链接:** http://arxiv.org/abs/2606.18988v1
    - **一句话说明:** 采用渐进式强化学习框架，使多模态欺骗检测过程具备可解释性，能够生成透明的推理路径，解决了该领域的黑箱问题。

4.  **SciRisk-Bench: A Risk-Dimension-Aware Benchmark for AI4Science Safety**
    - **作者:** Linghao Feng et al.
    - **链接:** http://arxiv.org/abs/2606.18936v1
    - **一句话说明:** 首个面向AI for Science（AI4Sci）的风险维度感知安全基准，评估LLM在科学应用（如化学、生物）中的潜在危害，填补了该方向的安全评估空白。

##### 🤖 **智能体与推理（规划、工具使用、多智能体、思维链）**

1.  **A Technical Taxonomy of LLM Agent Communication Protocols**
    - **作者:** Linus Sander et al.
    - **链接:** http://arxiv.org/abs/2606.19135v1
    - **一句话说明:** 对当前碎片化的LLM智能体通信协议进行了系统化技术分类，为建立互操作性标准提供了关键路线图，是构建分布式智能体网络的基础性工作。

2.  **Leadership as Coordination Control: Behavioral Signatures and the Recovery-Advantage Boundary in Multi-Agent LLM Teams**
    - **作者:** Haewoon Kwak
    - **链接:** http://arxiv.org/abs/2606.19111v1
    - **一句话说明:** 实证研究了多智能体LLM团队中“领导力”的量化条件，揭示了领导行为何时有效、是否存在“恢复优势”边界，为设计高效协作团队提供了理论依据。

3.  **Skill-Guided Continuation Distillation for GUI Agents**
    - **作者:** Zhimin Fan et al.
    - **链接:** http://arxiv.org/abs/2606.18890v1
    - **一句话说明:** 提出技能引导的继续蒸馏方法，解决了GUI智能体在闭环执行中遇到的策略偏离轨迹问题，通过教授备选技能路径提升其在复杂环境下的鲁棒性。

4.  **WorldLines: Benchmarking and Modeling Long-Horizon Stateful Embodied Agents**
    - **作者:** Yehang Zhang et al.
    - **链接:** http://arxiv.org/abs/2606.18847v1
    - **一句话说明:** 提出了一个面向长期、状态化具身智能体的基准和建模框架，要求智能体在数小时场景中记忆用户习惯和世界状态，推动了持久化能力的评估与开发。

##### 🔧 **方法与框架（新技术、基准测试、效率优化）**

1.  **FoMoE: Breaking the Full-Replica Barrier with a Federation of MoEs**
    - **作者:** Lorenzo Sani et al.
    - **链接:** http://arxiv.org/abs/2606.19025v1
    - **一句话说明:** 提出“专家混合体联邦”新范式，打破了LLM预训练中“全模型副本”的限制，允许多个参与方在不共享完整模型的情况下训练MoE，兼具隐私保护和计算效率。

2.  **RODS: Reward-Driven Online Data Synthesis for Multi-Turn Tool-Use Agents**
    - **作者:** Ruishan Fang et al.
    - **链接:** http://arxiv.org/abs/2606.19047v1
    - **一句话说明:** 提出奖励驱动的在线数据合成方法，为多轮工具使用智能体的RL训练动态生成信息量最大的样本，有效缓解了静态数据集中样本枯竭的瓶颈。

3.  **TRAP: Benchmark for Task-completion and Resistance to Active Privacy-extraction**
    - **作者:** Moon Ye-Bin et al.
    - **链接:** http://arxiv.org/abs/2606.18996v1
    - **一句话说明:** 构建了首个同时评估LLM智能体任务完成能力和主动隐私防护能力的基准，强调了在必须使用敏感信息的场景下平衡效用与安全的挑战。

4.  **Maturing Markov Decision Processes: Decision Making under Increasing Information and Shrinking Action Sets**
    - **作者:** Jiaxi Liu et al.
    - **链接:** http://arxiv.org/abs/2606.18820v1
    - **一句话说明:** 提出了“成熟MDP”新框架，建模了决策过程中信息动态增加而可用动作动态减少的现实场景，为设计更贴合实际的序列决策算法提供了理论基础。

##### 📊 **应用（垂直领域、多模态、代码生成）**

1.  **AdsMind: A Physics-Grounded Multi-Agent System for Self-Correcting Discovery of Adsorption Configurations on Heterogeneous Catalyst Surfaces**
    - **作者:** Zongmin Zhang et al.
    - **链接:** http://arxiv.org/abs/2606.19152v1
    - **一句话说明:** 构建了基于物理的多智能体系统，通过自我纠错策略高效发现催化剂表面最优吸附构型，是AI for Catalysis的重要进展。

2.  **ProfiLLM: Utility-Aligned Agentic User Profiling for Industrial Ride-Hailing Dispatch**
    - **作者:** Tengfei Lyu et al.
    - **链接:** http://arxiv.org/abs/2606.18803v1
    - **一句话说明:** 将LLM作为语义特征提取器应用于工业级打车调度系统，通过智能体式用户画像模型直接提升调度效率，展示了LLM在经典工业场景中的落地价值。

3.  **RTSGameBench: An RTS Benchmark for Strategic Reasoning by Vision-Language Models**
    - **作者:** San Kim et al.
    - **链接:** http://arxiv.org/abs/2606.18950v1
    - **一句话说明:** 利用即时战略（RTS）游戏作为测试床，创建了专门评估视觉语言模型（VLM）在竞争和合作环境下战略推理能力的基准。

---

#### **研究趋势信号**

今日投稿揭示了一个强烈信号：**“智能体物理学”正在形成**。一方面，多智能体系统的研究不再局限于拓扑或通信，而是深入到更底层的**协同控制理论**（如领导力量化、协作模式演化），并有向**物理科学**（如催化剂发现、材料计算）渗透的趋势。另一方面，将**控制论**（如PID控制）和**动力系统**的思想引入模型内部表征，以提升模型的控制性和可解释性（如PID控制音乐生成）也成为一个新兴探索方向。这表明AI研究正从模仿智能的表象，转向理解并驾驭智能涌现的内在机制。

---

#### **值得精读**

1.  **A Technical Taxonomy of LLM Agent Communication Protocols** ([Paper 4](http://arxiv.org/abs/2606.19135v1))
    - **理由:** 这篇论文是构建未来多智能体生态的基础设施级工作。它为当前混乱的智能体通信协议提供了清晰的分类学和对比分析，对从业人员和研究者的设计选择具有直接指导意义。

2.  **FoMoE: Breaking the Full-Replica Barrier with a Federation of MoEs** ([Paper 15](http://arxiv.org/abs/2606.19025v1))
    - **理由:** 本文针对LLM训练中的核心矛盾（模型规模 vs. 算力壁垒）提出了一个优雅且实用的解决方案。它巧妙结合了MoE和联邦学习的思想，在效率、隐私和性能间取得了新的平衡，潜力巨大。

3.  **SciRisk-Bench: A Risk-Dimension-Aware Benchmark for AI4Science Safety** ([Paper 25](http://arxiv.org/abs/2606.18936v1))
    - **理由:** 随着AI在科学研究中的自主性增强，安全问题变得至关重要。本文首次系统性地定义了AI4Sci场景下的风险维度，并建立了相关基准，是这个新兴且高风险领域内一篇具有里程碑意义的工作。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*