# ArXiv AI Research Digest 2026-08-13

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-13 00:54 UTC

---

# AI Research Digest — 2026-08-13

## 1. Today's Highlights

Today's submissions show three prominent directions: **alignment and safety for multilingual and low-resource settings** (with critical findings on cross-lingual safety gaps), **AI-assisted mathematical and scientific discovery** (including a human-AI case study on the Grothendieck constant), and **robustness and uncertainty quantification** (from test-time adaptation for GUI grounding to attention-path fragility as an uncertainty signal). The intersection of quantum computing and AI continues to grow, with two papers exploring quantum advantages in state-tracking and softmax attention. Additionally, **evaluation and measurement** of model behavior—from cross-lingual consistency in text-to-image generation to policy convergence in national AI strategies—represents a substantial portion of today's work.

---

## 2. Key Papers

### 🧠 Large Language Models

**1. The Illusion of Cross-Lingual Safety in Low-Resource Languages**  
[arXiv:2608.11146](http://arxiv.org/abs/2608.11146v1)  
Oppong, Sahil, Belay et al.  
Shows that safety alignment in LLMs does not generalize to low-resource languages, empirically demonstrating the failure of English-centric safety assumptions and highlighting a critical multilingual vulnerability.

**2. From Interpretability to Control: Insights from Six Years of the TrustNLP Workshop**  
[arXiv:2608.11171](http://arxiv.org/abs/2608.11171v1)  
Gupta, Mohanty, Ovalle et al.  
Provides a systematic retrospective of TrustNLP's evolution from post-hoc interpretability to mechanistic understanding and proactive control, offering useful context for where trustworthy NLP research is heading.

**3. Mapping and Measuring the Behavioral Evolution of Large Language Models**  
[arXiv:2608.11027](http://arxiv.org/abs/2608.11027v1)  
Qiao, Ding, Fan  
Characterizes output behavior of 32 models across six families using responses to 10,000 shared prompts, enabling quantitative comparison of behavioral similarity and cross-generation change beyond leaderboard metrics.

**4. Attention-Path Fragility as an Uncertainty Signal in Large Language Models**  
[arXiv:2608.11138](http://arxiv.org/abs/2608.11138v1)  
Kim, Ji, Moon et al.  
Proposes ASMI (Attention-Subnetwork Mutual Information), a training-free method that measures whether a confident prediction is fragile under attention-pathway perturbation, providing a novel uncertainty signal for LLMs.

**5. Why Does CLAUDE.md Keep Growing? Catastrophic Remembering in Agentic Coding**  
[arXiv:2608.11095](http://arxiv.org/abs/2608.11095v1)  
Chakrabarti  
Identifies "catastrophic remembering" in agentic coding—where instruction files like CLAUDE.md grow unbounded due to imperfect recall—and analyzes the economics of appending versus deleting instructions.

**6. Data Attribution of Emergent Misalignment with Persona Features**  
[arXiv:2608.11025](http://arxiv.org/abs/2608.11025v1)  
Vetter, Kaczér, Flek et al.  
Investigates emergent misalignment in fine-tuned LLMs, testing the persona-features mechanistic account and providing data-level attribution analysis for harmful behavior in unrelated domains.

---

### 🤖 Agents & Reasoning

**7. Long-Horizon AI Research for Grothendieck Constant: A Case Study in Human-AI Mathematical Collaboration**  
[arXiv:2608.11195](http://arxiv.org/abs/2608.11195v1)  
Li, Saha, Xue et al.  
Presents an extensive case study of AI-assisted mathematics that improves bounds on the Grothendieck constant, offering concrete guidance on effective human-AI collaboration for long-horizon research tasks.

**8. SkillZip: Evaluation-Free Skill Compression for Self-Evolving Agents by Discovering Reusable Structure**  
[arXiv:2608.11079](http://arxiv.org/abs/2608.11079v1)  
Bai, Lin, Liu et al.  
Introduces an evaluation-free method for compressing accumulated skills in self-evolving agents by discovering reusable structure, addressing the growing cost of redundant skill repositories.

**9. Test-Time Self-Evolving GUI Visual Grounding via Reflection-Guided On-Policy Self-Distillation**  
[arXiv:2608.11191](http://arxiv.org/abs/2608.11191v1)  
Xuan, Li  
Proposes a test-time adaptation method for GUI visual grounding that uses reflection-guided on-policy self-distillation, enabling GUI agents to adapt to unseen interfaces without parameter updates.

**10. Actions Speak Louder than Words: Measuring Cross-Lingual Policy Retention in Tool-Using Agents**  
[arXiv:2608.11110](http://arxiv.org/abs/2608.11110v1)  
Mukherjee, Bali, Sitaram  
Introduces a method for measuring whether tool-using agents retain the same action sequences across languages, arguing that multilingual evaluation should compare actions, not just final answers.

---

### 🔧 Methods & Frameworks

**11. Beyond a Bag of Features: Set-Level Instability in Sparse Autoencoders**  
[arXiv:2608.11197](http://arxiv.org/abs/2608.11197v1)  
Bolik, Stöpler, Andrzejak  
Revisits claims about LLM category representation using sparse autoencoders, revealing set-level instability in SAE features that complicates interpretability analysis.

**12. ReRound: Reconstructive Rounding to Resolve Midpoint Ambiguity in Calibration-Free LLM Quantization**  
[arXiv:2608.11045](http://arxiv.org/abs/2608.11045v1)  
Hsieh, Kung  
Introduces a post-training quantization method that trains a conditional diffusion model to resolve midpoint ambiguity in round-to-nearest schemes, improving LLM quantization without calibration data.

**13. V-FiLLM: Verified Financial LLM Reasoning Benchmark**  
[arXiv:2608.11047](http://arxiv.org/abs/2608.11047v1)  
Larsen, Laurent, Rakhamsari et al.  
Presents a framework generating financial reasoning benchmarks from executable computation trees, providing verifiable ground truth for evaluating LLM reasoning over structured financial data.

**14. Conditional Independence Tests for Constraint-Based Causal Discovery: A Survey**  
[arXiv:2608.11156](http://arxiv.org/abs/2608.11156v1)  
Averin, Moysiadis, Katakis  
Comprehensive survey of conditional independence testing for constraint-based causal discovery, with emphasis on assumption requirements and practical trade-offs.

---

### 📊 Applications

**15. On the Limitations of Cross-Lingual Consistency in Multilingual Text-to-image Generation**  
[arXiv:2608.11002](http://arxiv.org/abs/2608.11002v1)  
Zhang, Yan, Xie et al.  
Introduces LingT2I, a benchmark for cross-lingual text-to-image generation, documenting systematic performance gaps across languages and language-specific effects in T2I models.

**16. myMediWhisper: Construction of Burmese Medical Speech Corpus and Whisper Fine-Tuning for Clinical Dialogue ASR**  
[arXiv:2608.11036](http://arxiv.org/abs/2608.11036v1)  
Thu, Lin, Aung et al.  
Builds a 28-hour Burmese medical speech corpus with native-speaker validation and demonstrates improved Whisper fine-tuning for clinical dialogue ASR, addressing a critical low-resource healthcare gap.

---

## 3. Research Trend Signal

**Cross-lingual and low-resource evaluation is emerging as a core research area.** Two papers today (cross-lingual safety in low-resource languages; cross-lingual consistency in T2I) reveal systematic failures in multilingual generalization, while another (tool-using agents) argues for behavior-level evaluation beyond answer-level comparisons. This suggests the community is moving from "does it work in English?" to "does it work identically everywhere?" — with safety-critical applications leading the charge.

**Self-evolving and test-time adaptation continues to mature.** Approaches range from evaluation-free skill compression (SkillZip) to reflection-guided self-distillation for GUI grounding, indicating a shift away from static deployments toward agents that learn on the job.

**Quantum-AI intersections are becoming more concrete.** Two papers explore quantum advantages in softmax attention and AI state-tracking with formal complexity bounds — not just speculative proposals, but specific algorithmic mappings with proven advantages.

---

## 4. Worth Deep Reading

**1. "Long-Horizon AI Research for Grothendieck Constant: A Case Study in Human-AI Mathematical Collaboration"** ([arXiv:2608.11195](http://arxiv.org/abs/2608.11195v1)) — Provides rare, concrete insights into how AI agents can be effectively integrated into long-horizon mathematical research, including failure modes and collaborative patterns that generalize beyond this single case.

**2. "The Illusion of Cross-Lingual Safety in Low-Resource Languages"** ([arXiv:2608.11146](http://arxiv.org/abs/2608.11146v1)) — An important empirical finding with direct safety implications for multilingual deployment. Given the scale of LLM adoption globally, understanding where alignment fails is critical for responsible deployment.

**3. "Why Does CLAUDE.md Keep Growing? Catastrophic Remembering in Agentic Coding"** ([arXiv:2608.11095](http://arxiv.org/abs/2608.11095v1)) — A thoughtful analysis of an increasingly important practical problem in agentic software engineering. The framing of "catastrophic remembering" (as opposed to forgetting) offers a fresh lens for designing better agent memory systems.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*