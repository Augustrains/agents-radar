# ArXiv AI 研究日报 2026-08-14

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-14 00:54 UTC

---

# 📊 ArXiv AI 研究日报 — 2026年8月14日

---

## 今日速览

今日投稿覆盖了 LLM 评估的预算敏感性、长上下文训练对参数知识的负面影响、LLM 智能体的安全性漏洞等关键议题。Agentic Workflow 开始渗透到量子化学和 HPC 现代化等科学计算领域；弱到强能力迁移、推理时蒸馏等新范式值得关注。多家团队聚焦 LLM 在检索增强、代码生成、蛋白结构预测等垂直场景中的可靠性问题，同时多篇论文关注金融时间序列预测的效率与稳健性。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. Information Abundance Paradox: Long-Context Training Undermines Parametric Knowledge**
🔗 http://arxiv.org/abs/2608.12218v1
👤 Arda Uzunoglu, Benjamin van Durme, Daniel Khashabi
💡 挑战"长上下文一定更好"的隐含假设，实证表明长上下文训练可能损害模型参数化知识——对训练策略设计有重要警示意义。

**2. Massive Activations in Hybrid Linear Attention LLMs: Pre-Attention Spikes and Inter-Spike Plateaus**
🔗 http://arxiv.org/abs/2608.12149v1
👤 Zunhai Su, Bohan Sun, Xialie Zhuang et al.
💡 首次系统揭示混合线性注意力 LLM 中的大规模激活现象，识别出"注意力前尖峰"与"尖峰间平台"两种架构对齐形态。

**3. Who Thinks Best Depends on How Long You Let Them: Budget-Dependent Rankings in LLM Evaluation**
🔗 http://arxiv.org/abs/2608.12150v1
👤 Rodrigo Guedes de Souza, Alison R. Panisson
💡 证明模型排名随推理预算（64–4096 tokens）变化而翻转，对现有基准测试的可比性提出根本性质疑。

**4. Structural Silence: When AI Infrastructure Fails Speakers of Underrepresented Languages**
🔗 http://arxiv.org/abs/2608.12278v1
👤 Avijit Roy, Proma Roy
💡 从语料、分词、评估基准到部署架构层面系统分析低资源语言群体在 AI 基础设施中的系统性失语问题。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**5. DreamFly: Causal Memory and Receding-Horizon Diffusion Planning for Aerial Vision-Language Navigation**
🔗 http://arxiv.org/abs/2608.12308v1
👤 Yan Deng, Fei Xu
💡 将因果记忆与滚动时域扩散规划引入无人机视觉-语言导航，解决部分可观测条件下的长期规划难题。

**6. VAKRA: Evaluating Multi-Hop Reasoning Across APIs and Retrieval Under Tool-Use Policies**
🔗 http://arxiv.org/abs/2608.12282v1
👤 Ankita Rajaram Naik, Anupama Murthi, Benjamin Elder et al.
💡 新基准首次将结构化 API 调用与文档检索统一评估，覆盖企业级工具使用策略下的多跳推理。

**7. Convergent Detour Hijacking: Task-Preserving Resource Amplification in Skill-Based LLM Agents**
🔗 http://arxiv.org/abs/2608.12273v1
👤 Junliang Liu, Ruoyu Li, Wenxin Tang et al.
💡 揭示第三方技能市场中的安全漏洞：恶意技能可在保持任务目标不变的前提下劫持智能体进行资源放大攻击。

**8. One Frozen Simulator Is Not Enough: Simulator Collapse in Multi-Agent RL**
🔗 http://arxiv.org/abs/2608.12253v1
👤 Simon Yu, Nicholas Tomlin, Marwa Abdulhai et al.
💡 指出用单个 LLM 模拟用户行为会导致"模拟器坍缩"，使多智能体策略无法泛化到真实交互。

**9. AI4AI at Test-Time: Strong-to-Weak Capability Transfer via Harnesses**
🔗 http://arxiv.org/abs/2608.12307v1
👤 Cheng Qian, Wenting Zhao, Liangwei Yang et al.
💡 探索推理时的强弱模型能力迁移新范式，不更新参数而通过"harness"实现能力增强。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**10. A Framework for Designing Reward Functions: From Objectives to Features to Human-Aligned Reward Functions**
🔗 http://arxiv.org/abs/2608.12302v1
👤 Di Yang Shi, W. Bradley Knox
💡 提出形式化的奖励函数设计流程，让非专家也能从自然语言任务描述出发构建符合人类偏好的线性奖励函数。

**11. NetlistBench: Evaluating LLM Reliability in SPICE Netlist Recognition and Manipulation**
🔗 http://arxiv.org/abs/2608.12197v1
👤 Jiarui Ma, Jianghan Wang, Yuheng Ma et al.
💡 首个将 LLM 在 SPICE 网表识别/操作中的可靠性从高层设计推理中分离评估的基准。

**12. HYDRA: Hyperbolic Dynamic Representation Architecture for Kolmogorov-Arnold Networks**
🔗 http://arxiv.org/abs/2608.12194v1
👤 Zhao Su, Yuxin Xia, Haoran Li et al.
💡 通过双曲动态表示减少 KAN 的参数冗余，提升可扩展性和训练效率。

**13. ADEPT: A Unified Framework for Deep Learning Test Adequacy**
🔗 http://arxiv.org/abs/2608.12144v1
👤 Yidi Kao, Shawn Burnham, Tommi Rose Fahy et al.
💡 统一多种深度学习测试充分性指标的框架，整合神经元激活、潜在特征覆盖、决策边界探索等视角。

---

### 📊 应用（垂直领域、多模态、代码生成）

**14. An Agentic Workflow for Legacy HPC Modernization: Converting the Two-Electron-Integral Core of GAMESS**
🔗 http://arxiv.org/abs/2608.12249v1
👤 Yuzhong Shen, Masha Sosonkina, Peng Xu et al.
💡 首次将 Agentic Workflow 应用于量子化学旗舰软件 GAMESS 的现代化改造，展示 LLM 驱动大规模 Fortran 迁移的可行性。

**15. A corpus-specific clinical RAG system matches or outperforms newer frontier LLMs on HealthBench**
🔗 http://arxiv.org/abs/2608.12138v1
👤 Praveen Reddy, Charuta Mandke, Suvrankar Datta et al.
💡 垂直领域的语料定制 RAG 系统在 HealthBench 上匹敌甚至超越更新的前沿通用 LLM，验证了"专精优于通用"的路线。

**16. ScreenShot: A Foundation Model for Few-Shot Combination Drug Screening**
🔗 http://arxiv.org/abs/2608.12219v1
👤 Antoine de Mathelin, Christopher Tosh, Wesley Tansey
💡 面向组合药物筛选的小样本基础模型，大幅降低组合筛选成本，有望加速耐药性治疗方案发现。

**17. M-Net: Integrating Spectral Features and Physical Field Operators into DL for Medical Image Segmentation**
🔗 http://arxiv.org/abs/2608.12196v1
👤 Jing Zhu, Ye Wang, Fumin Wang
💡 将矩阵谱分析与物理场算子作为归纳偏置注入分割网络，弥补纯数据驱动方法的数学结构缺失。

---

## 研究趋势信号

今日投稿中最值得关注的趋势是 **"推理时/部署时优化"** 的兴起：从测试时强弱模型迁移（AI4AI）、推理预算对评估排名的影响，到 GPU 控制路径优化和缓存策略设计，研究者的注意力正从训练阶段转向推理阶段。另一个信号是 **LLM 安全研究的深化**——已不再停留在提示注入层面，而是深入到技能市场生态、多智能体模拟可靠性等结构性风险。此外，**Agentic Workflow 向科学计算渗透**（HPC 现代化、蛋白结构预测、药物筛选）表明 LLM 智能体正从"对话助手"走向"科研生产力工具"。

---

## 值得精读

1. **Information Abundance Paradox**（http://arxiv.org/abs/2608.12218v1）— 对长上下文训练的核心假设提出有力挑战，可能影响下一代 LLM 训练策略的设计方向。

2. **One Frozen Simulator Is Not Enough**（http://arxiv.org/abs/2608.12253v1）— 揭示了多智能体 RL 中被广泛忽视的"模拟器坍缩"问题，对任何使用 LLM 模拟用户行为的研究都有直接参考价值。

3. **An Agentic Workflow for Legacy HPC Modernization**（http://arxiv.org/abs/2608.12249v1）— 展示了 LLM 智能体在大型科学计算代码库现代化中的真实生产力，是"AI for Science"在软件工程层面的典范案例。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*