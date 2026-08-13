# ArXiv AI 研究日报 2026-08-13

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-13 00:54 UTC

---

# ArXiv AI 研究日报

**2026 年 8 月 13 日 | 共 50 篇新论文** — 今日投稿中，**数学研究中人机协作**、**跨语言安全对齐与策略一致性**、以及**量化与记忆压缩**成为三大突出主题，另有针对供应链中断干预排序和金融推理验证框架等应用导向的探索。


## 今日速览

今日投稿涵盖医疗手术机器人学习、跨语言安全对齐、数学定理证明中的人机协作、供应链因果干预排序以及金融推理基准构建等方向。值得关注的是，多篇论文聚焦于AI系统在 **"部署后"的适应与自我进化能力**——从测试时自适应 GUI 视觉定位到无需评估的技能压缩机制；同时，关于 LLM 行为演化和跨语言策略保留的分析揭示了当前模型在安全性和策略一致性上的深层缺陷。此外，针对稀疏自编码器的集合级不稳定性分析和注意力路径脆弱性作为不确定性信号的研究，为模型可解释性提供了新视角。


## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. The Illusion of Cross-Lingual Safety in Low-Resource Languages**
链接: http://arxiv.org/abs/2608.11146v1 | 作者: A. Oppong et al.
跨语言安全对齐的"幻觉"：揭示 LLM 安全对齐在低资源语言上的脆弱性，证明英语安全训练无法有效迁移至其他语言，对齐盲区值得警惕。

**2. Attention-Path Fragility as an Uncertainty Signal in Large Language Models**
链接: http://arxiv.org/abs/2608.11138v1 | 作者: M. Kim et al.
提出 ASMI 框架，将注意力路径的脆弱性作为不确定性的补充信号，有助于提升 LLM 在关键场景下的置信度判断能力。

**3. Data Attribution of Emergent Misalignment with Persona Features**
链接: http://arxiv.org/abs/2608.11025v1 | 作者: C. Vetter et al.
从数据归因角度研究"涌现性误对齐"现象，验证了 persona 特征作为中介机制的假说，为对齐安全提供了量化分析方法。

**4. Actions Speak Louder than Words: Measuring Cross-Lingual Policy Retention in Tool-Using Agents**
链接: http://arxiv.org/abs/2608.11110v1 | 作者: S. Mukherjee et al.
不只看答案，更观察行为：评测工具使用智能体在跨语言任务中的策略保留程度，强调过程一致性而非仅结果一致性。

**5. ReRound: Reconstructive Rounding to Resolve Midpoint Ambiguity in Calibration-Free LLM Quantization**
链接: http://arxiv.org/abs/2608.11045v1 | 作者: H. Hsieh, H. Kung
提出基于条件扩散模型的重构式舍入方案，解决权重量化中点的歧义问题，有效降低量化精度损失。

**6. Why Does CLAUDE.md Keep Growing? Catastrophic Remembering in Agentic Coding**
链接: http://arxiv.org/abs/2608.11095v1 | 作者: K. Chakrabarti
诊断智能体编码中"灾难性记忆"问题：说明文件无界增长源于不完善的回想机制，关乎智能体长期记忆架构设计。

**7. Test-Time Self-Evolving GUI Visual Grounding via Reflection-Guided On-Policy Self-Distillation**
链接: http://arxiv.org/abs/2608.11191v1 | 作者: S. Xuan, Z. Li
提出反射引导的 on-policy 自蒸馏机制，让 GUI 定位模型在测试阶段自我进化，无需标注即可适应新界面。


### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**1. Long-Horizon AI Research for Grothendieck Constant: A Case Study in Human-AI Mathematical Collaboration**
链接: http://arxiv.org/abs/2608.11195v1 | 作者: A. Li et al.
系统展示了 AI 在改进 Grothendieck 常数上下界这一长期数学问题中的具体作用，为数学研究中人机深度协作提供了可复制的案例。

**2. SkillZip: Evaluation-Free Skill Compression for Self-Evolving Agents by Discovering Reusable Structure**
链接: http://arxiv.org/abs/2608.11079v1 | 作者: X. Bai et al.
无需评估即可压缩智能体积累的技能库，通过发现可复用结构解决技能库无限膨胀的问题，提升自我进化效率。

**3. DACRI: Decision-Aware Causal Intervention Ranking for Critical Supply Chains**
链接: http://arxiv.org/abs/2608.11154v1 | 作者: S. Huang et al.
提出决策感知的因果干预排序框架，附带含因果真值的合成基准 CriticalSCM-Bench v1，从"检测问题"进阶到"选择最优干预"。

**4. V-FiLLM: Verified Financial LLM Reasoning Benchmark**
链接: http://arxiv.org/abs/2608.11047v1 | 作者: A. Larsen et al.
基于可执行计算树构建金融推理基准，使用验证器自动生成可验证的推理任务，弥补金融 LLM 结构化推理评估的空白。

**5. Self-Knowledge Retrieval Augmented Generation Framework for Patent Matching**
链接: http://arxiv.org/abs/2608.11030v1 | 作者: J. Zhang et al.
利用自知识检索增强生成进行专利匹配，通过先检索后生成提升专利文本匹配的精度与可解释性。


### 🔧 方法与框架（新技术、基准测试、效率优化）

**1. Beyond a Bag of Features: Set-Level Instability in Sparse Autoencoders**
链接: http://arxiv.org/abs/2608.11197v1 | 作者: N. Bolik et al.
揭示稀疏自编码器在集合层面的不稳定性，用 SAE 激活重叠替代余弦相似度，对可解释性分析的方法论提出重要修正。

**2. Conditional Independence Tests for Constraint-Based Causal Discovery: A Survey**
链接: http://arxiv.org/abs/2608.11156v1 | 作者: P. Averin et al.
系统综述因果发现中条件独立性检验的最新进展与假设条件，为该领域提供了清晰的方法论地图。

**3. 3D Weighted Geometric Graph Neural Networks for Sheep Facial Pain Assessment**
链接: http://arxiv.org/abs/2608.11050v1 | 作者: A. Noor et al.
将绵羊面部疼痛评估从二维扩展到三维加权几何图神经网络，首次将跨地标空间关系引入动物疼痛识别，兼具方法论创新与伦理价值。

**4. AlbumentationsX: One Augmentation Pipeline for Images and Related Annotations**
链接: http://arxiv.org/abs/2608.11123v1 | 作者: V. Iglovikov
提供统一的增强管线，确保图像与其各类标注（掩码、边界框、关键点等）在增强时严格对齐，是数据增强工具链的重要补充。

**5. Hierarchical Empirical-Bayes Naive Bayes: Minimax Smoothing and Calibration with AODE Extension**
链接: http://arxiv.org/abs/2608.11162v1 | 作者: N. T. Anh et al.
提出分层经验贝叶斯平滑方法替代固定强度平滑，动态适配特征基数与类别不平衡，提升朴素贝叶斯分类器性能。


### 📊 应用（垂直领域、多模态、代码生成）

**1. MultiModal Code-Switching: Interleaving Visual Objects into Language for Explicit Object-Level Alignment**
链接: http://arxiv.org/abs/2608.11167v1 | 作者: C. Xiang et al.
创新性地在语言中交错插入视觉对象 token 实现显式对象级对齐，有效缓解多模态大模型的指称歧义问题。

**2. On the Limitations of Cross-Lingual Consistency in Multilingual Text-to-image Generation**
链接: http://arxiv.org/abs/2608.11002v1 | 作者: S. Zhang et al.
发布 LingT2I 基准，系统评估文本到图像生成的跨语言一致性，发现并分析了不同语言之间的性能差距。

**3. R4DSG: Relative 4D Scene Graph Memory for Object-Centric Question Answering in Long Egocentric Video**
链接: http://arxiv.org/abs/2608.11017v1 | 作者: K. Ma et al.
构建相对4D场景图记忆用于长时程自我中心视频中的目标中心问答，有效保持跨时间的物体身份持久性。

**4. V-FiLLM: Verified Financial LLM Reasoning Benchmark**
链接: http://arxiv.org/abs/2608.11047v1 | 作者: A. Larsen et al.
基于可执行计算树构造金融推理基准，用验证器自动生成可验证的推理任务，填补金融结构化推理评估空白。


## 研究趋势信号

今日投稿中三个值得关注的方向：**(1) 跨语言/跨文化鲁棒性成为焦点**——多篇论文（安全对齐、工具使用策略保留、T2I生成一致性）从不同角度揭示了多语言场景下模型性能的系统性下降，预示着多语言评测将从"结果对比"转向"过程与策略对比"；(2) **自我进化与持续学习走向务实**——从测试时自适应到技能压缩，研究者不再追求从零训练，而是聚焦于如何让已部署系统高效积累和复用经验；(3) **因果推断与决策结合加深**——供应链干预排序、IRL 超梯度下降等工作显示因果方法正从"解释"走向"决策"，更直接地服务于业务优化。


## 值得精读

**1. Long-Horizon AI Research for Grothendieck Constant: A Case Study in Human-AI Mathematical Collaboration**
链接: http://arxiv.org/abs/2608.11195v1
理由：这是 AI 辅助数学研究的罕见深度案例，完整记录了 AI 在长达数月的研究过程中如何与人类数学家分工协作，对设计未来的 AI 科研助手具有直接的参考价值。

**2. Beyond a Bag of Features: Set-Level Instability in Sparse Autoencoders**
链接: http://arxiv.org/abs/2608.11197v1
理由：直接挑战了基于 SAE 的可解释性分析的可靠性，揭示了集合层面的不稳定性问题，对该领域后续所有基于 SAE 的结论都具有方法论警示意义。

**3. Actions Speak Louder than Words: Measuring Cross-Lingual Policy Retention in Tool-Using Agents**
链接: http://arxiv.org/abs/2608.11110v1
理由：首次将评测视角从"答案一致性"转向"路径一致性"，为多语言智能体评测提供了新范式，发现了仅靠最终答案评测无法察觉的深层策略退化问题。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*