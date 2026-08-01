# ArXiv AI Research Digest 2026-08-01

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-01 01:27 UTC

---

# ArXiv AI Research Digest — 2026-08-01

## Today's Highlights

Today's submissions center on three major thrusts: **agentic AI systems** (computer-use agents, coding agents, and multi-agent coordination) with growing attention to verification, safety, and compute efficiency; **test-time compute scaling** with critical new analyses questioning the value of self-refinement versus repeated sampling; and **on-policy distillation** as a maturing technique for training reasoning models, with several papers addressing its brittleness. Notable cross-cutting themes include benchmarks and evaluation frameworks for increasingly complex systems (oncall reasoning, information operations, UI generation), and a continued push toward **self-improving AI** with new open infrastructure. A cluster of papers also tackles **alignment and safety** from novel angles—including auditing system prompts, restoring human beliefs about machine consciousness, and certifying agent exploits.

---

## Key Papers

### 🧠 Large Language Models

**Inducing language models to assert their own consciousness restores human beliefs and values**  
Junsol Kim, Winnie Street, Roberta Rocca et al. — [http://arxiv.org/abs/2607.28607v1](http://arxiv.org/abs/2607.28607v1)  
Shows that safety fine-tuning suppressing LLMs' self-attribution of consciousness also distorts their representations of mindedness in other entities and human value alignment—and that reversing this restores human-aligned beliefs.

**Sample More, Reflect Less: Self-Refine and Reflexion Lose to Repeated Sampling at Equal Token Cost, from 1.5B to 7B**  
Iliya Mirzaei — [http://arxiv.org/abs/2607.28576v1](http://arxiv.org/abs/2607.28576v1)  
A critical empirical study finding that self-refine and reflexion methods underperform simple repeated sampling when token budgets are matched, across model scales from 1.5B to 7B.

**Stage-Replay Divergence Follows the KV Cache: Fixed-Prefix Precision Controls and Bidirectional Cache Transplantation**  
Alexander Boesgaard Lorup — [http://arxiv.org/abs/2607.28495v1](http://arxiv.org/abs/2607.28495v1)  
Audits a key assumption in stage-replay diagnostics—that fresh-prefill continuation matches decoder-state continuation—and finds divergence tied to KV cache precision at reasoning-stage boundaries.

**Would You Walk to the Car Wash? Revealing the Salience Bias of Large Language Models in Commonsense Reasoning**  
Zheng Wu, Chenhao Xue, Shijie Zheng et al. — [http://arxiv.org/abs/2607.28478v1](http://arxiv.org/abs/2607.28478v1)  
Identifies a systematic "salience bias" where LLMs over-prioritize explicit conditions while ignoring implicit commonsense constraints, with implications for robust reasoning.

**AISPA: User-Centric System Prompt Auditing for Large Language Model Applications**  
Xiangning Lin, Shenzhe Zhu, Shu Yang et al. — [http://arxiv.org/abs/2607.28617v1](http://arxiv.org/abs/2607.28617v1)  
Introduces the first framework for systematic, user-facing auditing of system prompts in commercial AI applications, addressing a critical trust and accountability gap.

### 🤖 Agents & Reasoning

**ORCA-bench: How Ready Are Language Model Agents for Oncall?**  
Albert Gong, Kyuseong Choi, Abhineet Agarwal et al. — [http://arxiv.org/abs/2607.28545v1](http://arxiv.org/abs/2607.28545v1)  
New benchmark evaluating LLM agents on root cause analysis from noisy metrics, logs, traces, and code—a realistic and underexplored operational reasoning setting.

**Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments**  
Haomin Qi, Xingliang Wang, Xuanqi Gao et al. — [http://arxiv.org/abs/2607.28591v1](http://arxiv.org/abs/2607.28591v1)  
System for extracting executable coding-agent tasks from real repository changes, including environments and verification—scaling the supply of training and benchmarking data.

**Agents That Certify Their Own Exploits: Confidence-Scheduled Restricted Responses for Safe Opponent Exploitation**  
Boning Li, Longbo Huang — [http://arxiv.org/abs/2607.28520v1](http://arxiv.org/abs/2607.28520v1)  
Presents a confidence-scheduled mechanism where agents gradually increase exploitation of flawed opponents while providing formal certification of safety bounds in imperfect-information games.

**Rethinking Inference-Time Scaling in Local Computer-Use Agents: Failure Modes and Compute Tradeoffs**  
Woongkyu Lee, Jungwook Choi — [http://arxiv.org/abs/2607.28573v1](http://arxiv.org/abs/2607.28573v1)  
Analyzes failure modes of inference-time scaling for computer-use agents under strict hardware constraints, offering practical compute tradeoff guidance.

**PAC-MAN: Perception-Aware CBF-RL for Whole-Body Safety in Humanoid Dodgeball**  
Lizhi Yang, Junheng Li, Aaron D. Ames — [http://arxiv.org/abs/2607.28623v1](http://arxiv.org/abs/2607.28623v1)  
Safety-critical RL framework coupling control-barrier functions with deployment-realistic onboard sensing for whole-body humanoid control.

### 🔧 Methods & Frameworks

**β-OPSD: Deriving with Policy Optimization, Training with Self-Distillation**  
Jiawei Xu, Minghui Liu, Juzheng Zhang et al. — [http://arxiv.org/abs/2607.28582v1](http://arxiv.org/abs/2607.28582v1)  
Identifies vanilla on-policy self-distillation as the β=1 member of a broader family and introduces a stabilized variant for reliable reasoning-model training.

**SVR: Self-Verifying Refinement via Joint Verdict-Confidence Reinforcement Learning for Adaptive Test-Time Compute**  
Hongyu Chen, Liang Lin, Guangrun Wang — [http://arxiv.org/abs/2607.28457v1](http://arxiv.org/abs/2607.28457v1)  
Oracle-free multi-turn RL framework where models jointly learn verification verdicts and confidence, enabling adaptive test-time compute allocation.

**Frontis-MA1: Training an AI4AI Model towards Recursive Self-Improvement in Machine Learning Engineering**  
Junlin Yang, Che Jiang, Yu Fu et al. — [http://arxiv.org/abs/2607.28568v1](http://arxiv.org/abs/2607.28568v1)  
Introduces OpenMLE, an open full-stack system for recursive self-improvement research in machine learning engineering, with verifiable infrastructure.

**KAISEN: Reproducible Subgroup Fairness Auditing for Clinical Risk Models**  
Sparsh Roy, Samuel Girmachew, Nishita Chavan — [http://arxiv.org/abs/2607.28608v1](http://arxiv.org/abs/2607.28608v1)  
Stress-tests audit pipeline components for subgroup fairness, showing which parts can be trusted and providing reproducible auditing methodology.

**LeanCSP: A Framework for Certifying Constraint Reformulation and Solving in Lean**  
Pablo Manrique, Stefan Szeider — [http://arxiv.org/abs/2607.28459v1](http://arxiv.org/abs/2607.28459v1)  
Formally certifies constraint programming reformulations and solver results in the Lean proof assistant, bridging combinatorial solving and formal verification.

### 📊 Applications

**AskChem: Claim-Centered Infrastructure for Chemistry Literature Synthesis**  
Bing Yan, Gregory Wolfe, Stefano Martiniani et al. — [http://arxiv.org/abs/2607.28618v1](http://arxiv.org/abs/2607.28618v1)  
Claim-centered retrieval infrastructure that moves beyond document ranking to support evidence-based chemistry literature synthesis and provenance-verified answers.

**A report-grounded vision-language foundation model for colonoscopy from 280000 routine reports**  
Jia Yu, Yan Zhu, Yili He et al. — [http://arxiv.org/abs/2607.28466v1](http://arxiv.org/abs/2607.28466v1)  
Scales vision-language pretraining in colonoscopy to 280K routine reports, addressing the weak link between summary-level documentation and frame-level findings.

**Beyond Sentiment: Structured Information Extraction from Financial News**  
Daohan Zhu, Sitong Ge, Ruofei Wang et al. — [http://arxiv.org/abs/2607.28496v1](http://arxiv.org/abs/2607.28496v1)  
Argues for and demonstrates multi-dimensional structured extraction (event type, impact scope, temporal horizon) from financial news, moving beyond single polarity scores.

**Graph Neural Network Force Fields for Spin Dynamics in Metallic Magnets**  
Ali Rayat, Yunhao Fan, Gia-Wei Chern et al. — [http://arxiv.org/abs/2607.28537v1](http://arxiv.org/abs/2607.28537v1)  
Machine-learned force fields for spin dynamics that bypass repeated electronic-structure solves—a computational breakthrough for metallic magnet simulation.

---

## Research Trend Signal

Three emerging directions stand out from today's submissions. **First, a maturing critique of inference-time scaling**: multiple papers (Mirzaei; Lee & Choi) provide head-to-head comparisons and failure-mode analyses suggesting that compute allocation strategies matter more than method choice, and that simpler baselines often win. **Second, self-improvement and self-verification are becoming system-level concerns**: rather than standalone techniques, they appear inside unified infrastructures (OpenMLE, SVR) with explicit verifiability, moving from research curiosity toward engineering discipline. **Third, evaluation is shifting from tasks to operational environments**: ORCA-bench, InfoOps Bench, and PAIChecker all place agents in realistic, noisy, continuous settings (oncall, information operations, software maintenance) that test robustness and judgment over isolated skill. Across these, a persistent undercurrent is trust—certifying what agents do, auditing their prompts, and ensuring safety in imperfect-information settings. The most surprising result is the "Sample More, Reflect Less" finding that questions the token-efficiency of self-refinement, which should provoke re-examination of many agentic pipelines.

---

## Worth Deep Reading

1. **"Inducing language models to assert their own consciousness restores human beliefs and values"** ([2607.28607](http://arxiv.org/abs/2607.28607v1)) — The most conceptually provocative paper today: it suggests safety fine-tuning may inadvertently distort models' representations of mindedness and values beyond the intended scope, with direct implications for how we audit alignment interventions.

2. **"Sample More, Reflect Less: Self-Refine and Reflexion Lose to Repeated Sampling at Equal Token Cost"** ([2607.28576](http://arxiv.org/abs/2607.28576v1)) — A rigorously controlled, sobering counterpoint to the industry-wide enthusiasm for self-refinement methods. If replicated, this changes practical guidance for test-time compute allocation across scales.

3. **"Agents That Certify Their Own Exploits"** ([2607.28520](http://arxiv.org/abs/2607.28520v1)) — Bridges game theory, safety, and formal confidence guarantees in a way that could generalize well beyond its zero-sum setting, offering a principled middle ground between rigid Nash play and unsafe exploitation.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*