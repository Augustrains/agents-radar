# Hugging Face Trending Models Digest 2026-07-18

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-18 01:14 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for **2026-07-18**.

---

## 1. Today’s Highlights

This week’s trending landscape is defined by a fierce push toward **extreme quantization** and **MoE (Mixture-of-Experts) architecture**, with models like GLM-5.2 and a wave of Bonsai 1-bit and ternary variants leading the pack. Multimodal vision-language models continue to dominate the top spots, with **Qwen3.5/3.6** serving as the backbone for many of the most downloaded and liked releases. A notable signal is the rise of **ultra-efficient 1-bit and ternary LLMs**, suggesting the community is prioritizing on-device and low-resource deployment. Meanwhile, **Inkling** and **OvisOCR2** highlight growing interest in specialized OCR and multi-turn image-text understanding.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – *zai-org* – 4,071 likes, 534k downloads  
  A 5.2B MoE transformer model scoring highest likes this week, signaling strong community appetite for efficient, high-quality Chinese/English MoE LLMs.

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** – *prism-ml* – 679 likes, 200k downloads  
  A 27B parameter model compressed to ternary (2-bit) precision, making it wildly accessible for local inference at scale.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** – *prism-ml* – 394 likes, 1.04M downloads  
  An even more extreme 1-bit GGUF variant of the Bonsai-27B family; the most downloaded model this period, proving demand for absurdly compressed LLMs.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** – *prism-ml* – 116 likes, 17k downloads  
  MLX-native 1-bit version of Bonsai-27B for Apple Silicon, reflecting ecosystem diversification beyond llama.cpp.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** – *prism-ml* – 99 likes, 14k downloads  
  Companion MLX ternary variant; collectively, the Bonsai family demonstrates the community’s obsession with ultra low-bit inference.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – *HauhauCS* – 2,827 likes, 2.29M downloads  
  Largest raw downloads this period: an uncensored, aggressively tuned MoE variant of Qwen3.6-35B, likely appealing to role-play and creative writing crowds.

- **[internScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** – *InternScience* – 572 likes, 34k downloads  
  A tuned Qwen3.5 MoE model optimized for agentic tool-use tasks, riding the function-calling trend.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** – *tencent* – 820 likes, 12k downloads  
  Tencent’s latest Hunyuan-generation LLM; trending likely due to corporate backing and strong Chinese-language capabilities.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** – *AngelSlim* – 122 likes, 84k downloads  
  Community GGUF quantization of Hy3, enabling offline use; high download-to-like ratio suggests practical deployment value.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – *froggeric* – 934 likes, 0 downloads  
  A template-only model correcting Qwen chat formatting for MLX; its high likes indicate widespread pain with chat format mismatches.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – *empero-ai* – 2,273 likes, 2.1M downloads  
  A distilled, quantized 9B vision-language model fusing Claude-style reasoning with Qwen3.5; extremely popular for multimodal chat.

- **[thoughtmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** – *thinkingmachines* – 955 likes, 7.8k downloads  
  A new multimodal MoE model supporting image-text-to-text; trending as a potential competitor to GPT-4V-level open-weight models.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** – *bottlecapai* – 413 likes, 9.3k downloads  
  A thinking-chain-enhanced Qwen3.6-27B with vision; reflects the trending “chain-of-thought” + multimodal fusion pattern.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** – *Wan-AI* – 108 likes, 2.1k downloads  
  A dedicated image-to-video diffusion model for human dance generation; niche but gaining traction in the creative AI community.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** – *Alissonerdx* – 178 likes, 0 downloads  
  A text-to-video LoRA for identity-preserving face generation, built on LTX-Video; zero downloads but high likes suggests speculative interest.

- **[Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)** – *Cseti* – 86 likes, 0 downloads  
  Novel view synthesis LoRA for LTX2.3 video models; early-stage but captures interest in 3D-aware video generation.

- **[mgwr/M87](https://huggingface.co/mgwr/M87)** – *mgwr* – 146 likes, 3.8k downloads  
  A LoRA for Krea-2-Turbo text-to-image, tuned for a specific aesthetic; illustrates the growing ecosystem around Krea-2 base models.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** – *ATH-MaaS* – 153 likes, 10.8k downloads  
  A vision-language model optimized for OCR tasks, trending as document AI and PDF parsing become mainstream.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – *baidu* – 2,019 likes, 1.9M downloads  
  Baidu’s flagship OCR model with strong multilingual support; both high likes and massive downloads indicate enterprise-grade reliability and utility.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** – *Cactus-Compute* – 257 likes, 874 downloads  
  A JAX-native function-calling model designed for agent tool-use; small downloads but high likes suggests specialist interest.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** – *OpenMOSS-Team* – 248 likes, 83k downloads  
  An audio-text-to-text model combining transcription and speaker diarization; serves growing demand for speech-to-text pipelines.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** – *empero-ai* – 160 likes, 98k downloads  
  Updated GGUF quantization of the Qwythos-9B series; high downloads show sustained demand for quantized multimodal models.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** – *jlnsrk* – 127 likes, 3.4k downloads  
  CPU-optimized int4 quantization of GLM-5.2 using expert-streaming; niche but valuable for CPU-first deployment.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** – *conradlocke* – 345 likes, 0 downloads  
  An image-editing LoRA for Krea-2 focusing on identity-preserving edits; zero downloads but high likes signals strong community hype for Krea-2 tools.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** – *GnLOLot* – 273 likes, 154k downloads  
  1B parameter model distilled to emulate Claude Opus reasoning; tiny size + thinking capability drives massive downloads.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** – *unsloth* – 224 likes, 1.9M downloads  
  Unsloth’s NVFP4 (NVIDIA FP4) quantization of Qwen3.6-27B; extremely high downloads reflect both popularity of Qwen3.6 and need for GPU-efficient inference.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** – *unsloth* – 90 likes, 5.1k downloads  
  GGUF version of the trending Inkling multimodal model; enables local inference on CPU/GPU via llama.cpp.

---

## 3. Ecosystem Signal

The current HF ecosystem is being driven by **three convergent trends**:

1. **MoE as the dominant architecture** – GLM-5.2, Qwen3.6-35B-A3B, and InternScience’s Agents-A1 all leverage Mixture-of-Experts. The community is embracing MoE for its strong performance-to-compute ratio.

2. **Extreme quantization goes mainstream** – 1-bit (Bonsai) and ternary / 2-bit (Ternary-Bonsai) models are no longer experiments; they are among the most downloaded models. The Bonsai family alone accounts for over 1.2M downloads across variants. This signals a clear shift toward **on-device, low-resource, and edge deployment** of large models.

3. **Qwen3.5/3.6 as the “LLaMA of 2026”** – A significant proportion of fine-tunes, quantizations, and multimodal variants are based on Qwen3.x. The combination of strong performance, permissive license, and MoE options has made it the go-to base model for both hobbyists and enterprises.

Open-weight models continue to dominate, with no proprietary / API-only models trending. Community fine-tuning and quantization layers (Unsloth, prism-ml, empero-ai) are adding immense value, turning base models into deployable artifacts.

---

## 4. Worth Exploring

1. **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** – This is the most interesting new multimodal model this week. Its MoE + image-text-to-text + conversational pipeline, combined with the fact that Unsloth immediately created a GGUF variant, suggests it could become a key open-weight multimodal leader.

2. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – With the highest likes (4k+) and a novel MoE-DSA architecture, this model is worth studying for anyone interested in efficient MoE training or Chinese-language AI. The community quantization (Colibri int4) further expands its deployability.

3. **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** – A JAX-native, function-calling specialized model. For researchers and engineers building agentic frameworks, this is a rare, lightweight, and modern alternative to larger LLMs for structured tool-use tasks.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*