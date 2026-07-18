# ArXiv AI Research Digest 2026-07-18

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-07-18 01:14 UTC

---

# ArXiv AI Research Digest — 2026-07-18

## Today's Highlights

Today's papers reveal three major thrusts: **scaling agentic context windows** (RoboTTT pushes robot visuomotor memory to 8K timesteps, three orders of magnitude beyond SOTA), **bridging simulation and physical safety** (BadWAM shows world-action models can dream correct futures while choosing wrong actions; MedFailBench builds clinician-grounded safety boundaries), and **fundamental rethinks of evaluation** (Beyond the Leaderboard argues for trustworthy multimodal VQA design; Can We Trust IRT for AI Evaluation? questions statistical assumptions in benchmark design). A surge of work on multi-agent systems for scientific research (AutoSynthesis, BrainPilot) suggests automated evidence synthesis is becoming a critical application area.

## Key Papers

### 🧠 Large Language Models

**Partition, Prompt, Aggregate: Statistical Self-Consistency in Language Models**
http://arxiv.org/abs/2607.15277v1
*Wolf, Kleine Buening, Krause et al.*
Tests whether LLM outputs satisfy basic probabilistic consistency under in-context learning — foundational for treating LLMs as conditional estimators.

**When Words Are Safe But Actions Kill: Probing Physical Danger Beyond Text Safety in Hidden-State Risk Space**
http://arxiv.org/abs/2607.15218v1
*Wang, Wang, Zhan et al.*
Shows that text-safety aligned LLMs can produce physically dangerous plans for embodied agents, proposing hidden-state risk probes.

**In-Place Tokenizer Expansion for Pre-trained LLMs**
http://arxiv.org/abs/2607.15232v1
*Smith, Dakhran, Cabrera et al.*
Enables vocabulary expansion after pretraining without full retraining, addressing tokenization inequity for low-resource languages.

**Linear representations of grammaticality in neural language models**
http://arxiv.org/abs/2607.15175v1
*Li, Kim*
Finds grammatical knowledge is linearly encoded in NLM representations, offering a mechanistic alternative to probability-based grammaticality tests.

**T²MLR: Transformer with Temporal Middle-Layer Recurrence**
http://arxiv.org/abs/2607.15178v1
*Cai, Zhu, Dong et al.*
Introduces recurrence at middle layers to preserve reasoning state across time, addressing the information bottleneck in autoregressive decoding.

### 🤖 Agents & Reasoning

**RoboTTT: Context Scaling for Robot Policies**
http://arxiv.org/abs/2607.15275v1
*Jiang, Chebotar, Zheng et al.*
Scales visuomotor context to 8K timesteps via test-time training — monumental for long-horizon robot control.

**BadWAM: When World-Action Models Dream Right but Act Wrong**
http://arxiv.org/abs/2607.15207v1
*Li, Yang, Wang*
Diagnoses a critical failure mode in world-action models: accurate future prediction doesn't guarantee correct action selection.

**Plover: Steering GUI Agents through Plan-Centric Interaction**
http://arxiv.org/abs/2607.15193v1
*Venkatesan, Wen, Guo et al.*
Introduces explicit plan representation for GUI agents to maintain user intent across dynamic interface states.

**SearchOS-V1: Towards Robust Open-Domain Information-Seeking Agent Collaboration**
http://arxiv.org/abs/2607.15257v1
*Zhang, Gao, Wu et al.*
Addresses the problem of agents losing task progress tracking during long search histories in multi-agent web search.

### 🔧 Methods & Frameworks

**Beyond Success Rate: Cost-Aware Evaluation of Offensive and Defensive Security Agents**
http://arxiv.org/abs/2607.15263v1
*Kassianik, Nelson, Singer*
Proposes cost-aware metrics for security agents, emphasizing operational costs per reasoning step over raw success rates.

**Can We Trust Item Response Theory for AI Evaluation?**
http://arxiv.org/abs/2607.15190v1
*Jiang, Kwon, Luo et al.*
Rigorously tests whether IRT's statistical assumptions (designed for humans) hold for AI benchmark data — finds alarming violations.

**Mask-Aware Policy Gradients for Diffusion Language Models**
http://arxiv.org/abs/2607.15200v1
*Raajesh, Shah, Klivans et al.*
Extends RL to masked diffusion language models by developing tractable log-likelihood approximations for policy gradient.

**Self-Evolving Human-Centered Framework for Explainable Depression Symptom Annotation**
http://arxiv.org/abs/2607.15202v1
*Cao, Pham, Nguyen et al.*
Introduces an active learning system that iteratively improves annotation quality with structured evidence chains for mental health XAI.

### 📊 Applications

**AutoSynthesis: An agentic system for automated meta-analysis**
http://arxiv.org/abs/2607.15247v1
*Taherinezhad, Maier, Vitagliano et al.*
End-to-end multi-agent system for automated quantitative evidence synthesis — a major step toward scalable, reproducible meta-analysis.

**BrainPilot: Automating Brain Discovery with Agentic Research**
http://arxiv.org/abs/2607.15079v1
*Li, Gao, Li et al.*
Multi-agent research system that coordinates literature survey, analysis execution, and interpretation across neuroscience modalities.

**MedFailBench: A Clinician-Built Open-Source Benchmark for Medical AI Safety Boundary Inspection**
http://arxiv.org/abs/2607.15166v1
*Ozkan*
Novel benchmark that labels errors by severity (1–5) and safety gate type, enabling targeted safety audits over accuracy-only metrics.

**Benchmarking Multimodal Large Language Models for Scientific Visualization Literacy**
http://arxiv.org/abs/2607.15176v1
*Do, Ta, Wang*
Bencmarks MLLMs on scientific visualization literacy (SciVis), revealing limitations beyond chart-based evaluations.

## Research Trend Signal

A clear trend is the **systematization of failure modes** in AI systems. Rather than simply reporting performance gains, today's papers actively catalog *how and why* systems fail: BadWAM taxonomizes world-model action-selection failures; Beyond Success Rate argues for cost-aware security evaluation; Can We Trust IRT? exposes statistical violations in benchmark design; and Symbal identifies systematic misalignment patterns in captioning. This meta-evaluative turn suggests the field is maturing beyond chasing benchmarks toward understanding fundamental reliability boundaries. Simultaneously, **agentic scientific research** (AutoSynthesis, BrainPilot) is emerging as a concrete high-value application that integrates retrieval, planning, multi-agent coordination, and domain expertise — likely to be a major growth area for agentic systems.

## Worth Deep Reading

**RoboTTT: Context Scaling for Robot Policies** (http://arxiv.org/abs/2607.15275v1)
A dramatic scaling result — three orders of magnitude improvement in visuomotor context length — with implications for any domain requiring long-horizon memory. The TTT-based approach may generalize beyond robotics.

**BadWAM: When World-Action Models Dream Right but Act Wrong** (http://arxiv.org/abs/2607.15207v1)
Fundamentally important for safety: demonstrates that accurate world prediction is insufficient for correct action, challenging a core assumption of model-based RL and world-model agents.

**Can We Trust Item Response Theory for AI Evaluation?** (http://arxiv.org/abs/2607.15190v1)
Methodological rigor applied to the evaluation tools themselves. If IRT assumptions fail dramatically on AI data, many popular benchmark analyses (ranking, item selection) may be invalid. Essential reading for anyone building or using AI benchmarks.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*