# ArXiv AI Research Digest 2026-09-09

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-09-09 09:31 UTC

---

# ArXiv AI Research Digest — 2026-09-09

## 1. Today's Highlights

Today's submissions show the field converging on **closed-loop, self-improving agentic systems**: multiple papers propose procedural memory, execution feedback, and tool-use data synthesis to make LLM agents more reliable. Long-context and recurrent architectures receive fresh theoretical attention, while interpretability moves toward **autonomous auditing**. Embodied AI advances with whole-body and dexterous vision-language-action models, and optimization theory contributes sharp new bounds and schedule laws. Overall, the direction is from static evaluation and generation toward testable, feedback-driven, physically grounded, and auditable AI.

## 2. Key Papers

### 🧠 Large Language Models

- [Learning Length-Extrapolatable Recurrent Models](http://arxiv.org/abs/2609.09157v1) — Hanwen Jiang
  Proposes training recurrent models with dense per-token losses to overcome BPTT horizon limitations, addressing long-context generalization.

- [It's Not RoPE that Creates Sinks: The Role of Self-Concentration and Value-Non-Mixing in Attention](http://arxiv.org/abs/2609.09085v1) — Raito Kiya, Satoki Ohashi, Kosuke Sato et al.
  Identifies self-concentration and value-non-mixing as root causes of attention sinks and massive activations, with implications for low-bit quantization.

- [Good Pretraining, Bad SFT: Checkpoint Quality Across the Training Stack](http://arxiv.org/abs/2609.08966v1) — Sohir Maskey, Philipp Scholl, Jonas Knupp et al.
  Shows the best pretraining checkpoint is not always the best starting point for SFT in a 30B MoE pipeline, challenging standard selection practices.

- [Measuring LLM Sycophancy under Sustained Multi-Turn Pressure](http://arxiv.org/abs/2609.09090v1) — Leyuan Tang, Kangda Wei, Tianyu Jiang et al.
  Introduces SPINE, a benchmark for sycophancy that emerges under sustained, adaptive user disagreement.

### 🤖 Agents & Reasoning

- [Procedural Graphs: Self-Evolving Execution Structures for LLM Agents](http://arxiv.org/abs/2609.09153v1) — Yuxing Lu, Yicheng Chen, Shanchan Wu et al.
  Proposes self-evolving execution graphs that capture procedural knowledge — what to do, in what order, and under which conditions — for long-horizon LLM agents.

- [ReCite: Agentic Reasoning for Faithful Citation](http://arxiv.org/abs/2609.09156v1) — Yuyang Huang, Bobo Li, Jiajia Song et al.
  Applies agentic retrieval and reasoning to citation recommendation, improving the faithfulness of academic attribution.

- [ExecCritic: Learn to Test, Test to Improve for Coding Agents](http://arxiv.org/abs/2609.09133v1) — Leitian Tao, Baolin Peng, Haorui Wang et al.
  Trains coding agents to generate and critique tests so execution feedback reflects the intended repository behavior, not self-confirming errors.

- [MeClear: Cooperative Game-Theoretic Attribution and Risk-Aware Memory Clearance for Long-Horizon LLM Agents](http://arxiv.org/abs/2609.09115v1) — Boyu Yang, Jiazheng Sun, Zilong Lu et al.
  Uses cooperative game theory to attribute the utility of memories and prune outdated or misleading context in long-horizon agent tasks.

### 🔧 Methods & Frameworks

- [Silver Rate Is (Almost) Optimal for Gradient Descent Acceleration](http://arxiv.org/abs/2609.09152v1) — Yuhan Ye, Kaizhao Liu
  Proves near-tight lower bounds for silver-step gradient descent acceleration in smooth convex optimization.

- [Nearly Tight Rademacher Bounds for Sparsely Activated Neural Networks](http://arxiv.org/abs/2609.09130v1) — Xiaoyu Li, Zhizhou Sha, Jiaojiao Jiang et al.
  Derives nearly tight statistical complexity bounds for input-dependent sparsity in one-hidden-layer ReLU networks.

- [Curriculum Learning as Transport: Understanding Curricula with Wasserstein Geodesics](http://arxiv.org/abs/2609.09099v1) — Changho Shin, David Alvarez-Melis
  Represents curricula as Wasserstein geodesics to disentangle difficulty, ordering, pacing, and exposure in curriculum design.

- [SAEScientist-Bench: Can AI Agents Conduct Autonomous SAE Interpretability Research?](http://arxiv.org/abs/2609.09113v1) — Yuqiao Tan, Shizhu He, Jun Zhao et al.
  Benchmarks whether AI agents can autonomously perform sparse-autoencoder interpretability research, a step toward verified recursive self-improvement.

### 📊 Applications

- [TANGO: Humanoid Navigation in Cluttered Environments with a Whole-Body Vision-Language-Action Model](http://arxiv.org/abs/2609.09158v1) — Anqi Li, Yuxin Chen, Zhaobo Li et al.
  Integrates whole-body geometry-aware adaptation with vision-language-action modeling for humanoid navigation beyond 2D path planning.

- [DeCAL: Towards Physically-Grounded Dexterous Vision-Language-Action Models via Contact-Aware Latent Co-Imagination](http://arxiv.org/abs/2609.09119v1) — Yankai Fu, Ning Chen, Junkai Zhao et al.
  Adds contact-aware latent co-imagination to VLA models for dexterous manipulation under heavy occlusion and complex contact dynamics.

- [Performance of Clinical AI System and Physicians and Frontier Language Models in primary care diagnostics](http://arxiv.org/abs/2609.09070v1) — Andy Nkansah, Hanna Plotnitskaya, Stanislau Salavei et al.
  Compares a clinical AI system, physicians, and frontier LLMs on adaptive primary-care diagnostic consultations, showing large performance gaps.

## 3. Research Trend Signal

Across today's submissions, three signals stand out. First, agentic LLM research is shifting from open-loop prompting to closed-loop, self-evolving execution structures: procedural graphs, rebuttal-guided training data, tool-use synthesis loops, and risk-aware memory all treat the agent's own experience and feedback as first-class signals. Second, interpretability is becoming an agentic benchmark itself, exemplified by SAEScientist-Bench, while studies of attention sinks and checkpoint selection caution against assumptions about model internals and training pipelines. Third, embodied AI continues to integrate with language models, with whole-body and dexterous VLA systems incorporating geometry, contact, and temporal awareness. The theory side remains strong, with near-tight optimization bounds and Rademacher complexity analyses strengthening the foundations. Overall, the field is converging on systems that act, test, remember, and audit their own behavior rather than simply generate outputs.

## 4. Worth Deep Reading