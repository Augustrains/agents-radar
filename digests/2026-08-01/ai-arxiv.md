# ArXiv AI 研究日报 2026-08-01

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-01 01:27 UTC

---

# 📡 ArXiv AI 研究日报 — 2026年8月1日

> 数据来源：2026-08-01 ArXiv cs.AI / cs.CL / cs.LG 最新投稿（50篇）

---

## 一、今日速览

今日投稿呈现出三个鲜明特征：**推理时扩展（Inference-time Scaling）进入精细化阶段**，多篇论文挑战"更多计算=更好性能"的朴素假设（如重复采样优于自我反思、自适应测试时计算分配）；**智能体安全与可信性成为主线**，覆盖系统提示审计、信息战防御、计算机使用智能体的失败模式分析等；**科学领域AI纵深发展**，从弦理论对偶追踪到临床公平性审计，AI方法论正加速渗透硬核科学场景。此外，关于LLM意识归因与语言多样性的研究提示我们，AI对齐正在从能力对齐走向更深层的价值与意识形态问题。

---

## 二、重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. AISPA: User-Centric System Prompt Auditing for Large Language Model Applications**
🔗 http://arxiv.org/abs/2607.28617v1
*Xiangning Lin, Shenzhe Zhu, Shu Yang et al.*
系统提示词是商业AI应用的"黑匣子"——AISPA提出用户视角的系统提示审计框架，直面开发者不披露提示词带来的信任与问责缺口。商业AI透明度的重要一步。

**2. Inducing language models to assert their own consciousness restores human beliefs and values**
🔗 http://arxiv.org/abs/2607.28607v1
*Junsol Kim, Winnie Street, Roberta Rocca et al.*
重要而微妙的安全发现：安全微调抑制LLM自我意识归因的同时，意外改变了模型对他人心智的表示，并与人类信念产生连锁偏差。对齐工程的"副作用"值得警惕。

**3. Sample More, Reflect Less: Self-Refine and Reflexion Lose to Repeated Sampling at Equal Token Cost, from 1.5B to 7B**
🔗 http://arxiv.org/abs/2607.28576v1
*Iliya Mirzaei*
颠覆直觉的实证研究：在相同token预算下，简单多次采样显著优于自我反思/自我精炼等复杂推理策略，且结论在1.5B至7B模型中成立。重新审视推理时扩展的"最优策略"。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**4. OSReward: Instituting Standardized Evaluation for Cross-Platform Computer-Use Reward Models**
🔗 http://arxiv.org/abs/2607.28609v1
*Qiushi Sun, Kanzhi Cheng, Yian Wang et al.*
计算机使用智能体（CUA）的核心瓶颈是轨迹验证——OSReward首次提出跨平台标准化的奖励模型评估框架，直接服务于CUA的评估、数据筛选与RL训练。

**5. Rethinking Inference-Time Scaling in Local Computer-Use Agents: Failure Modes and Compute Tradeoffs**
🔗 http://arxiv.org/abs/2607.28573v1
*Woongkyu Lee, Jungwook Choi*
本地部署CUA在严格硬件约束下的推理时扩展——系统分析了性能提升的失败模式与计算权衡，对实用化边缘CUA有直接指导意义。

**6. MANTA: Multi-Agent Network Topology Adaptation for Self-Evolving Multi-Agent Systems**
🔗 http://arxiv.org/abs/2607.28527v1
*Mao-xun Huang, Jerry Wang, Yi-Cheng Lai et al.*
多智能体系统通常把通信拓扑当作固定设计——MANTA实现拓扑的在线自适应演化，让多智能体协作结构随任务动态调整。

**7. Agents That Certify Their Own Exploits: Confidence-Scheduled Restricted Responses for Safe Opponent Exploitation**
🔗 http://arxiv.org/abs/2607.28520v1
*Boning Li, Longbo Huang*
零和博弈中，面对有缺陷的对手，智能体如何在"安全纳什策略"与"额外剥削收益"之间权衡？提出置信度调度的受限响应机制，让智能体为自己的利用行为"出具证书"。

**8. SVR: Self-Verifying Refinement via Joint Verdict-Confidence Reinforcement Learning for Adaptive Test-Time Compute**
🔗 http://arxiv.org/abs/2607.28457v1
*Hongyu Chen, Liang Lin, Guangrun Wang*
免外部验证器的自适应测试时计算框架——模型学会自己判断"是否需要继续思考"，通过联合裁决-置信度强化学习实现计算资源的自适应分配。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**9. PAC-MAN: Perception-Aware CBF-RL for Whole-Body Safety in Humanoid Dodgeball**
🔗 http://arxiv.org/abs/2607.28623v1
*Lizhi Yang, Junheng Li, Aaron D. Ames*
控制屏障函数（CBF）与RL耦合的感知感知安全框架，在真实人形机器人躲避球场景中结合头戴深度相机实现全身安全控制。机器人安全学习的代表性工作。

**10. Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments**
🔗 http://arxiv.org/abs/2607.28591v1
*Haomin Qi, Xingliang Wang, Xuanqi Gao et al.*
编码智能体面临可执行训练数据枯竭——Change2Task从真实代码仓库变更自动生成可执行任务与环境，为编码智能体的训练、基准测试和持续评估提供可扩展数据供给。

**11. ORCA-bench: How Ready Are Language Model Agents for Oncall?**
🔗 http://arxiv.org/abs/2607.28545v1
*Albert Gong, Kyuseong Choi, Abhineet Agarwal et al.*
将LLM智能体从"写代码"推向"做运维"——ORCA-bench评估智能体在嘈杂指标、日志、链路追踪与源码中做根因分析的能力。运维智能体的首个系统基准。

**12. InfoOps Bench: A live information operations safety benchmark**
🔗 http://arxiv.org/abs/2607.28503v1
*Dorian Quelle, Lisa-Maria Neudert, Jonathan Bright et al.*
实时更新的AI安全基准——追踪俄罗斯、中国等国家背景的2100+信息操作，评估前沿LLM被用于国家背景信息战时的"防线强度"。AI安全与地缘政治交叉的前沿评测。

---

### 📊 应用（垂直领域、多模态、代码生成）

**13. ReToken: One Token to Improve Vision-Language Models for Visual Retrieval**
🔗 http://arxiv.org/abs/2607.28627v1
*Yao Xiao, Reuben Tan, Zhen Zhu et al.*
长视觉上下文中VLM性能随干扰物数量增加而退化——ReToken用一个可学习的检索专用embedding token大幅提升视觉检索能力，同时缓解GPU显存约束。

**14. Beyond Sentiment: Structured Information Extraction from Financial News**
🔗 http://arxiv.org/abs/2607.28496v1
*Daohan Zhu, Sitong Ge, Ruofei Wang et al.*
金融情绪分析把丰富新闻压缩为单一极性分数——本文提出从金融新闻中抽取结构化多维信息（事件类型、影响范围、时间跨度等），开辟超越情绪的金融NLP方向。

**15. A report-grounded vision-language foundation model for colonoscopy from 280000 routine reports**
🔗 http://arxiv.org/abs/2607.28466v1
*Jia Yu, Yan Zhu, Yili He et al.*
基于28万份常规结肠镜报告训练视觉-语言基础模型——利用临床文本的丰富细节建立报告与视频帧的弱关联，让VLM在真实临床场景落地。

---

## 三、研究趋势信号

今日投稿中最值得关注的新兴方向有两个：

**1. 推理时扩展的精细化与去神话化。** 多篇论文（#15、#17、#45）从不同角度重新审视"更多推理计算=更好性能"的假设，从"采样胜过反思"到"自适应计算分配"，再到"本地硬件约束下的失败模式分析"，表明该领域正在从"堆算力"走向"最优算力分配"的科学化阶段。

**2. 智能体的自我意识与自我认知。** 安全对齐（#8）、硬件老化感知（#47）、利用行为的自我证明（#29）等论文，共同指向"智能体如何认知自己"这一深层问题——包括评估自身状态、局限性和影响边界。这可能成为下一阶段AI安全研究的新范式。

---

## 四、值得精读

**1. Sample More, Reflect Less** 🔗 http://arxiv.org/abs/2607.28576v1
挑战了当前推理增强的主流叙事。如果"多次采样"在相同token预算下系统性优于"自我反思/精炼"，这将对RLHF、推理模型设计和推理时扩展策略产生深远影响。简洁有力的实验设计，结论值得每个LLM研究者关注。

**2. AISPA: User-Centric System Prompt Auditing** 🔗 http://arxiv.org/abs/2607.28617v1
系统提示词是商业AI产品的"隐藏开关"，直接影响数十亿用户行为，却完全不受监管和公众审查。AISPA首次提出系统化的用户侧提示审计方法，是AI透明度和问责研究的关键基础设施。

**3. InfoOps Bench** 🔗 http://arxiv.org/abs/2607.28503v1
将AI安全评估推向"活数据"时代——基于实时监控的信息操作流而非静态数据集。这是一个可持续更新的安全基准，能够捕捉前沿模型与信息战之间的动态博弈。AI安全评估方法论的范式创新。

---

*本日报由AI研究分析师自动整理，筛选标准基于研究贡献的原创性、领域影响力潜力与跨学科启发价值。*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*