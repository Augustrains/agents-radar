# Hugging Face Trending Models Digest 2026-07-02

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-02 02:00 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-02**.

---

## 1. Today's Highlights

This week’s trending models signal a clear shift toward **MoE (Mixture-of-Experts) architectures** and **agentic-capable LLMs**, with GLM-5.2 dominating the charts alongside new Qwen-based agent and coder models. **Quantized GGUF variants** continue to drive massive download volumes, particularly for coding and vision models, indicating strong community preference for local deployment. **DeepSeek V4** and **Ornith-1.0** from DeepReinforce demonstrate a rising trend of openly released MoE families with strong reasoning benchmarks. The image-to-video and LoRA ecosystem also sees notable entries from **fal.ai** and **Krea**, highlighting growing demand for controllable generative tools.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,170 likes | 159,967 downloads  
  A large MoE conversational model from the GLM family, trending as the highest-liked model this week due to strong chat performance and open-weight release.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 277 likes | 7,629 downloads  
  The latest flagship from DeepSeek featuring dynamic sparse attention (DSpark), trending for its cutting-edge efficiency and arXiv publication.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | 181 likes | 21,935 downloads  
  A compact 230M liquid foundation model, gaining traction for its state-space-model efficiency on small devices.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 438 likes | 56,953 downloads  
  A fast text-to-image model based on Krea-2-Raw, trending for its speed and quality in creative generation workflows.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,547 likes | 896,058 downloads  
  A 3B image-feature-extraction model for object localization, trending very high due to both utility and cross-ecosystem adoption.

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — fal | 136 likes | 0 downloads  
  An image-to-video LoRA for photorealistic 3D animation, trending as a specialized creative gen AI tool.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,552 likes | 597,090 downloads  
  A GGUF-quantized Gemma 4 coder with advanced reasoning, trending strongly for local coding assistance with high throughput.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 140 likes | 511 downloads  
  A Qwen3.5-MoE-based agent model, trending for its early adoption in agentic workflows and research.

- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** — BugTraceAI | 108 likes | 3,377 downloads  
  A quantized cybersecurity-focused model, gaining interest for offensive-security analysis and code auditing.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 1,160 likes | 1,113,871 downloads  
  A GGUF quantized Qwen3.5 fine-tune with mythos-style reasoning, trending for its massive download count and roleplay prowess.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,378 likes | 3,055,962 downloads  
  An uncensored MoE vision-language GGUF with over 3M downloads, trending as the most downloaded model this week due to unfiltered output and local vision capabilities.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 490 likes | 212,201 downloads  
  Unsloth’s ultra-optimized GGUF variant of GLM-5.2, popular for enabling fast inference of the large MoE model on consumer hardware.

## 3. Ecosystem Signal

The current landscape reveals **three converging trends**:

1. **Quantized MoE dominance**: GGUF-quantized MoE models (GLM-5.2, Qwen3.6-35B-A3B, Ornith-1.0) are seeing the highest download volumes, reflecting a community preference for low-resource, high-capability local inference.
2. **Agentic and coder specialization surges**: Models explicitly tagged "agentic," "coder," or "terminal" (e.g., Gemma-4-12B coder, Qwen-AgentWorld) are gaining attention rapidly, suggesting that training for tool-use and autonomous execution is now a primary use case.
3. **Open-weight release cadence accelerates**: With DeepSeek V4, zai-org GLM-5.2, and DeepReinforce's Ornith-1.0 series all released openly in full-precision alongside quantized variants, the **open-weight frontier** is expanding rapidly—narrowing the gap with proprietary offerings while enabling community customization.

## 4. Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A must-study for anyone building vision pipelines: it combines feature extraction with localization at a very efficient 3B scale, and has already garnered nearly 900K downloads. Use it to replace heavier object detection models.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — At 3M+ downloads, this is the most popular model this week. It is worth exploring to understand how the community pushes MoE+uncensored+vision combinations, and how quantization enables widespread deployment of large vision-language models.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — The DSpark attention mechanism is a significant architectural advance. Studying this model gives insight into the next generation of efficient sparse transformer training and inference.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*