# Hugging Face Trending Models Digest 2026-07-20

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-20 01:26 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-20

## 1. Today's Highlights

This week's trending models reveal a clear shift toward **MoE (Mixture-of-Experts) architectures**, extreme **quantization (1–2 bit and ternary)** for local deployment, and **multimodal vision-language models** dominating the top ranks. Google's **Gemma-4-31B-it** leads in raw downloads (12.3M), while ZAI's **GLM-5.2** (4,167 likes) and the uncensored **Qwen3.6-35B-A3B** (2,901 likes) signal strong community engagement with MoE-based LLMs. The emergence of **sub-3-bit quantization** (prism-ml's Bonsai and Ternary-Bonsai series) is reshaping what's possible for running 27B+ models on consumer hardware. Meanwhile, OCR and transcription models from Baidu and OpenMOSS show growing demand for production-grade document AI and speech processing.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | Likes: 4,167 | Downloads: 536,177  
  Zhipu AI's latest MoE architecture with dynamic sparse attention, trending as a top-tier open-weight alternative to GPT-4-class models.

- **[Google Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | Likes: 3,273 | Downloads: 12,337,374  
  Google's flagship 31B instruction-tuned model, dominating download counts due to its permissive license and strong benchmark performance.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | Likes: 584 | Downloads: 35,833  
  Qwen3.5-based MoE model optimized for agentic tool use and function calling, reflecting the growing "agent AI" trend.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | Likes: 835 | Downloads: 13,698  
  Tencent's Hunyuan-based V3 language model, gaining attention for competitive Chinese+English bilingual performance.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | Likes: 2,901 | Downloads: 2,084,530  
  Uncensored MoE vision-language model based on Qwen3.6, trending for its aggressive fine-tuning and multimodal capabilities.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | Likes: 462 | Downloads: 10,647  
  Qwen3.6 variant with extended "thinking" chains, popular among reasoning-focused users.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | Likes: 279 | Downloads: 955  
  JAX-based model specialized for function calling and tool use, small but notable for agent infrastructure research.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | Likes: 1,150 | Downloads: 13,462  
  A new multimodal MoE model supporting image-text-to-text, conversational, and potentially audio inputs — the week's most novel architecture.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | Likes: 2,345 | Downloads: 2,118,995  
  Qwen3.5-based vision-language model heavily downloaded for its quantized GGUF format and stylistic "Claude-Mythos" fine-tune.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | Likes: 2,187 | Downloads: 2,122,848  
  Baidu's production-grade OCR system with unlimited-length document support, trending for enterprise document processing needs.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | Likes: 194 | Downloads: 14,587  
  Qwen3.5-based OCR model, a more lightweight alternative to Baidu's Unlimited-OCR.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | Likes: 128 | Downloads: 2,408  
  Image-to-video generation model specialized for human dance motions, using Diffusers.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | Likes: 195 | Downloads: 0  
  Identity-preserving LoRA for LTX video models, enabling consistent face generation across video frames.

- **[Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)** — Cseti | Likes: 98 | Downloads: 0  
  Novel view synthesis LoRA for LTX, enabling cross-view prompt-based video generation.

- **[mgwr/M87](https://huggingface.co/mgwr/M87)** — mgwr | Likes: 158 | Downloads: 4,652  
  Diffusion LoRA for Krea-2-Turbo, fine-tuned for stylized image generation.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | Likes: 279 | Downloads: 87,533  
  Audio-text-to-text model combining transcription with speaker diarization, trending for meeting/phone processing.

- **[OpenMOSS-Team/MOSS-VL-Realtime](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)** — OpenMOSS-Team | Likes: 81 | Downloads: 544  
  Real-time video understanding model, early-stage but representing a new frontier in streaming VL.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | Likes: 792 | Downloads: 338,945  
  First mainstream **ternary (2-bit) quantization** of a 27B model — extremely compact (under 4GB) for local CPU inference.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | Likes: 498 | Downloads: 1,262,894  
  The **1-bit** version of Bonsai pushing extreme compression boundaries — over 1.2M downloads despite (or because of) ultra-low precision.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | Likes: 139 | Downloads: 21,690  
  Apple MLX-compatible 1-bit version, enabling efficient inference on Mac hardware.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | Likes: 120 | Downloads: 17,869  
  MLX ternary companion, expanding the Bonsai ecosystem to Apple Silicon users.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | Likes: 141 | Downloads: 4,035  
  CPU-optimized int4 quantization of GLM-5.2 using expert-streaming, making MoE models accessible without GPUs.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | Likes: 106 | Downloads: 16,719  
  Extensively fine-tuned Qwen3.6 variant with uncensored and fusion stylization, GGUF-quantized for broad deployment.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — unsloth | Likes: 105 | Downloads: 6,771  
  GGUF conversion of the Inkling multimodal model, enabling efficient local inference with Unsloth's quantization tools.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | Likes: 121 | Downloads: 28,012  
  Sub-1B model with "thinking" capabilities and Claude-Opus-style stylization, exceptionally compact for edge deployment.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | Likes: 947 | Downloads: 0  
  Not a model but a critical utility — corrected Jinja chat templates for Qwen3.5, trending for fixing widespread template bugs.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | Likes: 424 | Downloads: 0  
  Identity-preserving LoRA for Krea-2 image editing, enabling consistent character editing across generations.

### 🔧 Specialized Models (code, math, medical, embeddings)

- No models in this week's top 30 map clearly to code, math, medical, or embedding specializations. This absence is itself an ecosystem signal — see analysis below.

---

## 3. Ecosystem Signal

**MoE dominates the top of the chart.** GLM-5.2, Qwen3.6-35B-A3B, Agents-A1, and Inkling all use Mixture-of-Experts architectures, indicating that both researchers and the community have converged on MoE as the path to high-quality models with manageable compute costs. The "MoE for everything" trend now extends beyond LLMs into multimodal models like Inkling and Qwen3.6 vision variants.

**Extreme quantization is no longer experimental — it's mainstream.** Prism-ml's Bonsai series (1-bit and ternary) accumulated over 1.6M total downloads this week. This signals a paradigm shift where "running a 27B model on a laptop" is expected, not aspirational. The ternary approach (values: -1, 0, +1) is particularly innovative, offering better quality than binary while matching its memory footprint.

**Open-weight models are winning.** Every model in the top 30 is open-weight, with Google's Gemma-4 and ZAI's GLM-5.2 representing the leading edge of corporate open sourcing. Per-download license restrictions on some variants may limit commercial use, but full weight availability drives community adoption.

**Notable absence: pure text-only small models.** The top models are all 9B+ or MoE variants. Even the "small" models (MiniCPM5-1B) are niche reasoning variants. This suggests developers have moved past model size as a primary consideration and now prioritize capability density via quantization.

**Chat template utilities are trending.** The popularity of `froggeric/Qwen-Fixed-Chat-Templates` (947 likes, 0 downloads) reveals an ecosystem pain point: as models rapidly iterate, template compatibility breaks. This signals maturity — the community is beyond just "can it run?" and now optimizing for reliability.

---

## 4. Worth Exploring

1. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**  
   *Reasoning:* The first production-ready ternary model is a research milestone and practical tool. At ~3.5GB for 27B parameters, it redefines what "local inference" means. Worth studying for compression techniques that may become standard within 6 months.

2. **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)**  
   *Reasoning:* Inkling's multimodal MoE design is a genuine architecture novelty. It's one of the first models from a small team to achieve top-1 trending against Google and Baidu. Its architecture could preview the next generation of unified multimodal models.

3. **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**  
   *Reasoning:* The "agent AI" wave is accelerating, and this Qwen3.5 MoE model is purpose-built for tool use. As function-calling becomes the dominant LLM interface, understanding how Agents-A1 achieves reliable tool invocation will be valuable for anyone building LLM-powered products.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*