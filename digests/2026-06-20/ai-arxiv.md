# ArXiv AI 研究日报 2026-06-20

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-20 02:03 UTC

---

好的，作为AI研究分析师，以下是基于您提供的2026年6月20日ArXiv论文列表生成的《ArXiv AI研究日报》。

---

# ArXiv AI 研究日报 | 2026-06-20

## 今日速览

今日投稿中，AI安全与智能体可靠性成为绝对焦点，多篇论文深入探讨了后门攻击、对抗性鲁棒性以及策略遵循问题。同时，模型的可解释性与透明度研究也取得了显著进展，从大语言模型推理的“透明度”到具体任务中模型决策的归因分析。此外，4-bit KV缓存量化、多语言代码生成基准等效率与评估方面的实用工作也为社区提供了重要工具。值得注意的是，关于模型指令遵循中的风格偏见和校准问题的研究，揭示了当前模型在分布外场景下的潜在脆弱性。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1.  **How Transparent is DiffusionGemma?**
    - 作者: Joshua Engels et al.
    - 链接: http://arxiv.org/abs/2606.20560v1
    - 一句话说明: 探究DiffusionGemma这类在连续潜在空间进行大量计算的模型的推理透明度，是理解其决策机制和调试异常行为的关键研究。

2.  **What Do Safety-Aligned LLMs Learn From Mixed Compliance Demonstrations?**
    - 作者: Sihui Dai et al.
    - 链接: http://arxiv.org/abs/2606.20508v1
    - 一句话说明: 研究发现，即使在使用无害请求的示例时，混杂其中的有害请求示例也会诱导模型越狱，揭示了上下文学习中的安全漏洞机制。

3.  **Calibration Without Comprehension: Diagnosing the Limits of Fine-Tuning LLMs for Vulnerability Detection in Systems Software**
    - 作者: Arastoo Zibaeirad et al.
    - 链接: http://arxiv.org/abs/2606.20502v1
    - 一句话说明: 提出CWE-Trace框架，通过834个手动整理的Linux内核样本，诊断出在漏洞检测任务中，微调后的LLM可能只是模式匹配而非真正理解安全语义。

4.  **Toward Calibrated Mixture-of-Experts Under Distribution Shift**
    - 作者: Gina Wong et al.
    - 链接: http://arxiv.org/abs/2606.20544v1
    - 一句话说明: 关注混合专家模型在分布偏移下的校准问题，通过在个体专家级别进行校准来提升整体集成模型的准确性与不确定性估计。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

1.  **LedgerAgent: Structured State for Policy-Adherent Tool-Calling Agents**
    - 作者: Md Nayem Uddin et al.
    - 链接: http://arxiv.org/abs/2606.20529v1
    - 一句话说明: 针对客服场景中工具调用代理，引入结构化状态管理机制，确保代理在执行任务时能严格遵守复杂领域策略。

2.  **Contagion Networks: Evaluator Bias Propagation in Multi-Agent LLM Systems**
    - 作者: Zewen Liu
    - 链接: http://arxiv.org/abs/2606.20493v1
    - 一句话说明: 首次正式建模了多智能体系统中，作为评估者的LLM的系统性偏见如何在代理网络间传播的“传染”现象。

3.  **Beyond Global Replanning: Hierarchical Recovery for Cross-Device Agent Systems**
    - 作者: Shu Yao et al.
    - 链接: http://arxiv.org/abs/2606.20487v1
    - 一句话说明: 提出了分层恢复机制，允许跨设备代理系统在出现运行时故障时，进行更精细、局部化的故障恢复，而非进行成本高昂的全局重规划。

4.  **Your Mouse and Eyes Secretly Leak Your Preference: LLM Alignment using Implicit Feedback from Users**
    - 作者: Haw-Shiuan Chang et al.
    - 链接: http://arxiv.org/abs/2606.20482v1
    - 一句话说明: 提出利用用户的鼠标移动和眼动数据作为隐式反馈来对齐LLM，绕过了传统方法需要用户提供明确反馈的局限。

### 🔧 方法与框架（新技术、基准测试、效率优化）

1.  **UltraQuant: 4-bit KV Caching for Context-Heavy Agents**
    - 作者: Inesh Chakrabarti et al.
    - 链接: http://arxiv.org/abs/2606.20474v1
    - 一句话说明: 针对上下文密集型代理场景，采用4-bit KV缓存压缩技术，利用TurboQuant等方法大幅降低长前缀推理的内存占用。

2.  **Multi-LCB: Extending LiveCodeBench to Multiple Programming Languages**
    - 作者: Maria Ivanova et al.
    - 链接: http://arxiv.org/abs/2606.20517v1
    - 一句话说明: 将流行的代码生成基准LiveCodeBench扩展到多语言环境，为评估LLM在不同编程语言上的代码生成能力提供了更全面的、抗污染的工具。

3.  **Probe-and-Refine Tuning of Repository Guidance for Coding Agents**
    - 作者: Asa Shepard et al.
    - 链接: http://arxiv.org/abs/2606.20512v1
    - 一句话说明: 提出一种自动调优`AGENTS.md`文件的方法，使编码代理能获得更准确的仓库级操作知识（如测试流程、文件结构），从而提升修复成功率。

4.  **Contagion Networks: Evaluator Bias Propagation in Multi-Agent LLM Systems**
    - 作者: Zewen Liu
    - 链接: http://arxiv.org/abs/2606.20493v1
    - 一句话说明: (与智能体部分重复，但作为方法论框架同样重要) 为理解和量化多智能体系统中的偏见传播提供了全新的数学模型。

### 📊 应用（垂直领域、多模态、代码生成）

1.  **FreeStyle: Free Control of Style-Content Dual-Reference Generation from Community LoRA Mining**
    - 作者: Jinghong Lan et al.
    - 链接: http://arxiv.org/abs/2606.20506v1
    - 一句话说明: 从社区挖掘的LoRA中实现了对图像风格和内容的自由控制生成，解决了风格-内容双参考生成中的平衡和泛化难题。

2.  **Scalable Training of Spatially Grounded 2D Vision-Language Models for Radiology**
    - 作者: Yusuf Salcan et al.
    - 链接: http://arxiv.org/abs/2606.20477v1
    - 一句话说明: 发布了RefRad2D大规模放射学双语数据集，并展示了无需手动空间标注即可训练出具备空间定位能力的视觉语言模型。

3.  **StylisticBias: A Few Human Visual Cues Drive Most Social Biases in MLLMs**
    - 作者: Shaghayegh Kolli et al.
    - 链接: http://arxiv.org/abs/2606.20527v1
    - 一句话说明: 揭示多模态大语言模型的社会偏见主要源于少数视觉风格线索（如衣服、姿态），而非个体的整体特征，为偏见诊断提供了新的视角。

---

## 研究趋势信号

**AI安全与代理可靠性的融合**是今日最强烈的信号。研究不再局限于简单的对抗样本，而是深入到**多轮对抗**（NRT-Bench）、**偏见在网络中的传染**（Contagion Networks）以及**运行时策略强制执行**（LedgerAgent, Efficient and Sound Probabilistic Verification）。这表明社区正从静态模型安全转向对动态、交互式、多代理系统的全生命周期安全保障。同时，**隐式反馈**（如眼动）用于对齐和**分布偏移下的校准**问题，也凸显了研究正朝着更真实、更复杂的应用场景迈进。

---

## 值得精读

1.  **How Transparent is DiffusionGemma?**
    - **理由**: 这是理解新一代生成模型（如Diffusion LM）内部工作原理的必读之作。它直接挑战了我们对模型透明度的传统认知，对于未来模型的可信度和可解释性研究至关重要。

2.  **Contagion Networks: Evaluator Bias Propagation in Multi-Agent LLM Systems**
    - **理由**: 本文提出了一个新颖且极具洞见的理论框架来建模多智能体系统中的偏见传播。随着多智能体系统日益普及，理解并控制这种“系统性偏见污染”将成为该领域的核心课题。

3.  **Your Mouse and Eyes Secretly Leak Your Preference: LLM Alignment using Implicit Feedback from Users**
    - **理由**: 该研究开创性地利用了用户行为生物信号进行模型对齐，有望极大提升人类反馈的收集效率和质量。这项工作的伦理和实用潜力都值得深入探讨。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*