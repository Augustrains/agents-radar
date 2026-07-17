# Hugging Face Trending Models Digest 2026-07-17

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-17 01:22 UTC

---

# 🚀 Hugging Face Trending Models Digest — 2026-07-17

## 1. Today's Highlights

This week's trending models reveal a **strong multimodal shift** and a **quantization frenzy** around Qwen 3.5/3.6 and GLM-5.2 architectures. **Qwen 3.6 derivatives dominate** the list, with uncensored and specialized variants (e.g., `HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive`) attracting massive downloads. **GLM-5.2** from Zhipu AI leads in raw likes (4,029), signaling strong community interest in MoE-based models. Ternary and 1-bit quantization from **prism-ml** (Bonsai series) continue to push the boundaries of extreme compression. Notable new entrants include **Tencent's Hy3** base model, **Wan-AI's video generation model**, and **Baidu's Unlimited-OCR**, reflecting corporate investment in open-weight releases.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat & Instruction-Tuned)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 806 likes, 4 downloads  
  A new image-text-to-text conversational model using the `inkling_mm_model` architecture, early-stage with very few downloads but high engagement.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,029 likes, 513,061 downloads  
  A flagship MoE-DSA conversational model from Zhipu AI, leading the list in likes and signaling strong open-weight competition in China.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,787 likes, 2.3M downloads  
  An uncensored, vision-capable MoE variant of Qwen 3.6, extremely popular for its aggressive fine-tuning style and multimodal capabilities.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 566 likes, 33,400 downloads  
  A Qwen 3.5-based MoE agent model, optimized for tool use and agentic workflows.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 901 likes, 1.78M downloads  
  A 35B GGUF-quantized model with MIT license and endpoint compatibility, highly downloaded for production deployment.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 813 likes, 11,849 downloads  
  Tencent's Hunyuan-v3 text-generation model, a strong corporate open-weight entry with a dedicated GGUF quantization already available.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — GnLOLot | 131 likes, 4,117 downloads  
  A tiny 1B thinking model based on MiniCPM5, fine-tuned with Claude Opus synthetic data for reasoning tasks.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 264 likes, 121,296 downloads  
  The GGUF-quantized sibling of the above, far more downloaded due to local inference usability.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,235 likes, 2.04M downloads  
  A Qwen 3.5-based multimodal reasoning model, highly downloaded in GGUF format for local vision-language inference.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 389 likes, 8,238 downloads  
  A Qwen 3.6-based image-text-to-text model with integrated thinking/reasoning capabilities.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,010 likes, 1.85M downloads  
  Baidu's open-weight OCR model, massively downloaded for its unlimited-use license and strong document understanding performance.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | 136 likes, 3,678 downloads  
  A Qwen 3.5-based OCR model, specialized for image-to-text document parsing.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 232 likes, 75,105 downloads  
  An audio-text-to-text transcription and speaker diarization model, gaining traction for speech processing pipelines.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 166 likes, 0 downloads  
  A LoRA for LTX-video enabling identity-preserving text-to-video generation, new but architecturally notable.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | 92 likes, 1,884 downloads  
  A 14B image-to-video diffusion model for dance generation, using the diffusers library.

- **[Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)** — Cseti | 76 likes, 0 downloads  
  An IC-LoRA for novel view synthesis in video generation, niche but technically innovative.

### 🔧 Specialized Models (Code, Agent, Function-Calling)

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,207 likes, 506,068 downloads  
  A Gemma 4-based agentic coding model with terminal use support, heavily downloaded for local code agent deployments.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | 248 likes, 733 downloads  
  A JAX-based model for function calling and tool use, representing the growing JAX ecosystem for agent architectures.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 924 likes, 0 downloads  
  Not a model but a utility: corrected Jinja chat templates for Qwen 3.5 models, trending due to widespread template issues.

### 📦 Fine-tunes & Quantizations (GGUF, MLX, Community Variants)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 601 likes, 74,007 downloads  
  A 2-bit ternary quantization of a 27B model, pioneering extreme compression for local deployment.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 340 likes, 559,267 downloads  
  The 1-bit predecessor to Ternary-Bonsai, still widely used for ultra-low-resource inference.

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — empero-ai | 150 likes, 89,107 downloads  
  GGUF quantized variant of the Qwythos 9B reasoning model, optimized for llama.cpp.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — unsloth | 216 likes, 1.71M downloads  
  Unsloth's 4-bit NVFP4 quantization of Qwen 3.6-27B, extremely popular for efficient multimodal inference.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | 115 likes, 80,796 downloads  
  Community GGUF quantization of Tencent's Hy3 model, Apache-2.0 licensed.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | 119 likes, 2,621 downloads  
  An int4 quantized variant of GLM-5.2 using Colibri expert streaming for CPU-efficient MoE inference.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | 83 likes, 7,622 downloads  
  MLX-format version of the ternary Bonsai, optimized for Apple Silicon.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | 82 likes, 10,760 downloads  
  MLX-format 1-bit Bonsai, showing Apple ecosystem demand for extreme compression.

---

## 3. Ecosystem Signal

**Qwen 3.5/3.6 has become the dominant model family** in the open-weight ecosystem, with at least 8 of the 30 trending models directly based on these architectures. The shift from pure text-based LLMs to **image-text-to-text multimodal models** is accelerating — nearly half of the top models support vision input. **MoE (Mixture of Experts) models are clearly winning** the architecture race: GLM-5.2, Qwen3.6-35B-A3B, InternScience/Agents-A1, and Hy3 all leverage MoE for better efficiency.

On the quantization front, **extreme compression is the story**: 1-bit and 2-bit ternary quantizations from prism-ml represent the bleeding edge, while GGUF remains the dominant format for local deployment (10+ entries). The **Apple Silicon ecosystem is growing** with dedicated MLX quantizations appearing for major models. **Corporate open-weight releases** from Tencent (Hy3), Baidu (Unlimited-OCR), and Zhipu AI (GLM-5.2) indicate a strategic shift toward open-weight competition.

Agentic and specialized models (function calling, coding, OCR) are gaining dedicated followings, suggesting the community is moving beyond general-purpose chatbots toward **task-specific, deployable models**.

---

## 4. Worth Exploring

1. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — With 4,029 likes as the most-loved model this week, it represents the cutting edge of Chinese open-weight MoE development. Worth studying for its DSA (Dynamic Sparse Attention) architecture and strong conversational performance.

2. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — This is the frontier of extreme quantization: a 27B model compressed to 2-bit ternary weights. For anyone interested in running large models on consumer hardware, this is a must-explore technical artifact.

3. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 2.01M downloads and strong likes, this specialized OCR model from Baidu is a standout for document AI workflows. Its "unlimited" license and strong performance make it a practical choice for production OCR pipelines.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*