# ArXiv AI Research Digest 2026-08-06

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-06 01:16 UTC

---

# 🤖 ArXiv AI Research Digest — 2026-08-06

## 1. Today's Highlights

Today's submissions reveal a strong emphasis on **test-time scaling and inference efficiency**, with papers on interpretable adaptive sampling, cross-model KV cache transfer, and visual evidence scheduling for long-video understanding. **Agentic evaluation** is also prominent, featuring prospective benchmarks like WorldCup Arena (leakage-free live forecasting) and PAST-Bench (recursive self-improvement foundations). Notably, several works tackle **numerical and structural robustness** — from ALiBi positional encoding underflow failures to dynamic routing vulnerabilities under adversarial conditions. Multimodal systems continue to mature, with Video-DeepResearch extending deep research agents to continuous video streams and CARE-X pushing toward clinically useful radiology VLMs.

## 2. Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

**When Attention Goes Blind: Numerical Failure in ALiBi Positional Encodings**  
[Link](http://arxiv.org/abs/2608.03994v1)  
Schröder, Gienapp, Schlatt et al.  
Identifies a floating-point underflow failure in ALiBi that partially blinds attention heads — a critical robustness finding for a widely deployed positional encoding scheme.

**Logic Before Language: Pre-pretraining on Formal Derivations Fosters Skill Acquisition and Compressibility**  
[Link](http://arxiv.org/abs/2608.03930v1)  
Cheng, Aletras, Valentino  
Demonstrates that pre-pretraining LLMs on formal derivations before natural language improves downstream skill acquisition and model compressibility.

**Intertemporal Preference Steering in Qwen3 via Contrastive Activation Addition**  
[Link](http://arxiv.org/abs/2608.03892v1)  
Mráz, Shenk  
Trains contrastive linear probes to discover and steer temporal-horizon preferences in Qwen3-32B — an interpretability approach with direct behavioral control applications.

**Omega-S: A Functional Resilience Index for LLM Fine-Tuning**  
[Link](http://arxiv.org/abs/2608.03887v1)  
Acedo  
Introduces a drop-in penalty computed from weight matrices alone that mitigates catastrophic forgetting during fine-tuning, requiring no previous-task data or Fisher matrix.

**Test-Time Scaling in Reasoning LLMs: Inference Regimes, Evaluation, and Reproducibility**  
[Link](http://arxiv.org/abs/2608.04001v1)  
Hariri, Chen, Shahini et al.  
Systematizes the diverse landscape of test-time scaling algorithms — from single-trajectory deliberation to sampling-and-aggregation — addressing evaluation and reproducibility gaps.

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

**PAST-Bench: Benchmarking the Foundations of Recursive Self-Improvement in Personal Agents**  
[Link](http://arxiv.org/abs/2608.04003v1)  
Xue, Ding, Shen et al.  
Introduces a benchmark for recursive self-improvement in personal AI agents, testing whether retained experience translates into improved future behavior.

**WorldCup Arena: Prospective, Leakage-Free Evaluation of Frontier LLMs on a Live Tournament**  
[Link](http://arxiv.org/abs/2608.04008v1)  
Wang, Bian, Li et al.  
Reports on a prospective forecasting benchmark constructed over 39 days of the 2026 FIFA World Cup, eliminating memorization-based evaluation leakage.

**ReflectRL: Learning from Golden Negative Trajectories via Reflective-to-Direct Reasoning**  
[Link](http://arxiv.org/abs/2608.03972v1)  
Bi, Zhou, Jin et al.  
Addresses expert-model failures in on-policy RL by learning from golden negative trajectories — valuable for post-training beyond expert ceiling.

**TurnSight: Turn-Level Hindsight Self-Distillation for Tool-Integrated Reasoning**  
[Link](http://arxiv.org/abs/2608.04007v1)  
Qu, Dai, Cai et al.  
Proposes turn-level credit assignment for tool-integrated reasoning, overcoming trajectory-level supervision limits in long-horizon agentic tasks.

**ContinualSkillBench: Can LLM Agents Truly Evolve Their Capabilities?**  
[Link](http://arxiv.org/abs/2608.03874v1)  
Guan, Wang, Yang et al.  
Questions whether agent skill libraries genuinely improve task-solving capabilities over time, introducing a benchmark for continual skill evolution.

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

**Cross-Model KV Cache Transfer in LLM Families: A Closed-Form Linear Mapping for Prefill Reuse**  
[Link](http://arxiv.org/abs/2608.03893v1)  
Heo, Shafipour, Zhao et al.  
Enables KV cache reuse across differently-sized models in a family via closed-form linear mapping — potentially eliminating redundant prefill computation in model cascading.

**Interpretable Adaptive Sampling for LLM Test-Time Scaling**  
[Link](http://arxiv.org/abs/2608.03961v1)  
Kashaniyan, Jannesari  
Introduces interpretable, per-query dynamic compute allocation for test-time scaling, replacing opaque fixed budgets with explainable sampling decisions.

**Sparse Weight Decomposition for Efficient Circuit Extraction**  
[Link](http://arxiv.org/abs/2608.03913v1)  
Yan, Huang, Duan et al.  
Presents a sparse decomposition approach for extracting interpretable circuits directly from dense transformers, reducing the compute overhead of interpretability analysis.

**Muon Meets Mamba: Spectral Optimization for State Space Models**  
[Link](http://arxiv.org/abs/2608.03941v1)  
Battalov, Kramin, Markotenko et al.  
Extends the Muon spectral optimizer to state-space models, reporting results largely unstudied outside Transformer architectures.

**SocietyBench: Forecasting Counterfactual Social-World Evolution**  
[Link](http://arxiv.org/abs/2608.04009v1)  
Wang, Bian, Li et al.  
Benchmarks LLM understanding of how real social events unfold counterfactually — complementing task-completion-oriented agent evaluation.

### 📊 Applications (domain-specific, multimodal, code generation)

**Video-DeepResearch: Towards the Next-Generation Multimodal Deepresearch Agent**  
[Link](http://arxiv.org/abs/2608.03979v1)  
Fang, Zeng, Huang et al.  
Extends deep research agents to continuous video streams, identifying modality bias and spatiotemporal grounding as critical bottlenecks.

**CARE-X: Towards Clinically Useful Radiology VLMs with Auxiliary Supervision, Reward-Aligned Learning, and Tool-Augmented Measurement**  
[Link](http://arxiv.org/abs/2608.03890v1)  
Ranjit, Porya, Joel et al.  
Integrates classification, localization, and anatomical measurement into a single chest X-ray VLM — moving beyond fluent report generation toward clinical utility.

**Can Large Language Models Recover Semantic Optimization Opportunities That Compilers Miss?**  
[Link](http://arxiv.org/abs/2608.03983v1)  
Jiang, Yu, Hossain et al.  
Investigates whether LLMs can recover semantics absent from program representations and realize compiler-missed optimization opportunities.

**Agogic: Performance-Timed Music Tokens for LLM-Native Text-to-Symbolic-Music Generation**  
[Link](http://arxiv.org/abs/2608.03999v1)  
Chen, Chen, Mao et al.  
Isolates tokenization effects in text-to-music models, showing representation choice alone significantly impacts generation quality.

**MultiGlobeQA: A Multilingual and Globally Diverse Benchmark for Geospatial Reasoning**  
[Link](http://arxiv.org/abs/2608.03882v1)  
Böckling, Nosova, Paulheim et al.  
Introduces a multilingual benchmark for geospatial reasoning — distance, containment, and topology — revealing LLM struggles despite stored geographic knowledge.

## 3. Research Trend Signal

Several convergent trends emerge from today's submissions. **Efficiency-aware inference** is clearly consolidating: cross-model KV cache transfer, adaptive visual evidence scheduling, interpretable sampling budgets, and compute-aware RAG evaluation all address the same tension between model capability and inference cost. **Prospective, leakage-free evaluation** is gaining momentum — WorldCup Arena's live-tournament design represents a methodological shift from retrospective benchmarks toward real-world forecasting validation. **Recursive self-improvement** appears to be emerging as a structured research area with dedicated benchmarks (PAST-Bench, ContinualSkillBench), signaling maturation beyond ad-hoc agent evaluations. We also note growing attention to **numerical and structural robustness** across modalities — from ALiBi failures to adversarial UAV tracking vulnerabilities. Finally, **LLM+compiler/formal systems** integration (semantic optimization recovery, formal-derivation pre-pretraining, quantum-classical separations) suggests a deepening relationship between LLMs and formal reasoning infrastructure.

## 4. Worth Deep Reading

**Test-Time Scaling in Reasoning LLMs: Inference Regimes, Evaluation, and Reproducibility** ([Link](http://arxiv.org/abs/2608.04001v1)) — The field desperately needs systematic taxonomy and reproducibility standards for test-time scaling; this paper addresses a central topic with likely broad adoption.

**WorldCup Arena: Prospective, Leakage-Free Evaluation of Frontier LLMs on a Live Tournament** ([Link](http://arxiv.org/abs/2608.04008v1)) — A methodological breakthrough in benchmark design that eliminates memorization concerns entirely — essential reading for anyone building or using LLM evaluations.

**When Attention Goes Blind: Numerical Failure in ALiBi Positional Encodings** ([Link](http://arxiv.org/abs/2608.03994v1)) — A subtle but potentially pervasive failure mode in a widely-used positional encoding scheme, with implications for robustness, reproducibility, and deployment at scale.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*