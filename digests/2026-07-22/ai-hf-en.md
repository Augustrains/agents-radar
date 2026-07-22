# Hugging Face Trending Models Digest 2026-07-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-22 01:18 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-22

## Today's Highlights

This week's trending models reveal a strong surge in **ternary and ultra-low-bit quantization** techniques, led by prism-ml's Bonsai and Ternary-Bonsai series achieving massive download counts. The **Qwen 3.5/3.6 ecosystem** continues to dominate, powering everything from uncensored fine-tunes (HauhauCS) to OCR models (OvisOCR2) and reasoning-focused GGUF conversions. Google's **Gemma-4-31B-it** debuts with explosive download volume (12M+), signaling strong enterprise interest in open-weight multimodal models. Meanwhile, **vision-language-action models** for robotics (MiniCPM-RobotManip/RobotTrack) from openbmb represent an emerging niche gaining traction.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,278 likes | 545k downloads  
  A massive MoE-based conversational model with DSA architecture, trending for its strong performance at scale with sparse activation.

- **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 1,199 likes | 722k downloads  
  Compressed-tensor code-specialized version of the Kimi K2.5 family, gaining traction for efficient code generation.

- **[Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — poolside | 186 likes | 3k downloads  
  A text-generation model from poolside for code-centric applications, positioned as a smaller but capable alternative in the Laguna series.

- **[Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Motif-Technologies | 125 likes | 125 downloads  
  A new feature-extraction model from Motif Technologies, early in adoption but with growing interest in its embedding capabilities.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | 3,313 likes | 12.1M downloads  
  Google's latest large multimodal model supporting image+text in/out, trending for its massive download surge and strong instruction-following.

- **[Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,363 likes | 16k downloads  
  A multimodal image-text-to-text conversational model with MoE architecture, standing out for its original architecture and "thinking" branding.

- **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,605 likes | 2.2M downloads  
  Baidu's universal OCR model for feature extraction from images, trending for its remarkable download count and practical utility.

- **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,970 likes | 2M downloads  
  A highly popular uncensored Qwen3.6 MoE variant with aggressive tuning, driving massive adoption among power users.

- **[Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | 151 likes | 2.5k downloads  
  A diffusion-based image-to-video model specialized for dance generation, representing a creative niche in video synthesis.

- **[LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 222 likes | 0 downloads  
  A LoRA for identity-preserving text-to-video using LTX-Video, targeting consistent character generation in video.

### 🔧 Specialized Models (code, math, medical, embeddings, robotics, ASR)

- **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 1,199 likes | 722k downloads  
  (also listed in Language) — code-specialized compressed model for efficient code generation.

- **[MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 299 likes | 92k downloads  
  An audio-text-to-text model combining transcription and speaker diarization, trending for its practical meeting/assistant use case.

- **[Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** — nvidia | 96 likes | 93k downloads  
  Nvidia's compact 1B embedding model using sentence-transformers, gaining adoption for RAG and retrieval applications.

- **[nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 902 likes | 590k downloads  
  A lightweight streaming ASR model from Nvidia's Nemotron 3.5 family, trending for its efficiency in real-time speech recognition.

- **[MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — openbmb | 147 likes | 58 downloads  
  A vision-language-action model for robotic manipulation tasks, representing an emerging robotics-AI frontier.

- **[MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — openbmb | 107 likes | 72 downloads  
  Companion robotics model from openbmb for object tracking, part of the growing VLA (vision-language-action) model family.

- **[needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | 298 likes | 1k downloads  
  A JAX-based model for function-calling and tool-use, trending for its specialized agentic capabilities.

- **[krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 476 likes | 0 downloads  
  A ComfyUI-compatible LoRA for identity-preserving image editing built on Krea-2-Raw, popular in creative workflows.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 899 likes | 432k downloads  
  A 2-bit ternary quantization of a large Qwen3.5-based model using llama.cpp, trending for extreme compression with surprising capability retention.

- **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 570 likes | 1.4M downloads  
  A 1-bit GGUF quantization (the "Bonsai" series), extremely popular for running large models on consumer hardware.

- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,387 likes | 2.1M downloads  
  A reasoning-focused 9B GGUF based on Qwen3.5, trending for blending Claude-like "mythos" tuning with efficient quantization.

- **[Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | 161 likes | 25k downloads  
  MLX-native 1-bit version of Bonsai for Apple Silicon users, extending the Bonsai ecosystem to macOS.

- **[Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | 135 likes | 20k downloads  
  MLX ternary 2-bit variant, part of prism-ml's comprehensive quantization suite for the same base model.

- **[inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — unsloth | 116 likes | 7.4k downloads  
  Community GGUF conversion of the Inkling multimodal model by unsloth, enabling local inference.

- **[Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | 156 likes | 145k downloads  
  Quantized GGUF version of Tencent's Hy3 model, trending for its Apache-2.0 license and practical LLM deployment.

- **[MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | 147 likes | 52k downloads  
  A tiny 1B thinking-enhanced GGUF based on MiniCPM5, trending for packing reasoning capabilities into a 1B parameter footprint.

- **[Qwen3.6-27B-Fable-Fusion-...-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 243 likes | 63k downloads  
  A maximally-tuned uncensored Qwen3.6 GGUF with extensive feature fusion, popular in the "uncensored" model community.

- **[Kimi-K3](https://huggingface.co/reteetzad/Kimi-K3)** — reteetzad | 201 likes | 0 downloads  
  A US-region restricted model, possibly a leaked or early Kimi K3 variant, attracting curiosity downloads.

---

## Ecosystem Signal

The most prominent signal this week is the **explosion of ultra-low-bit quantization** (1-bit and ternary 2-bit) on large models. prism-ml's Bonsai and Ternary-Bonsai series collectively exceed **1.8 million downloads**, demonstrating that the community is hungry for models that run on consumer hardware without sacrificing too much quality. The **Qwen 3.5/3.6 ecosystem** has become the dominant base for fine-tuning and quantization, powering 10+ of the top 30 models — from uncensored variants to reasoning-tuned GGUF files. Google's **Gemma-4-31B-it** is the clear open-weight multimodal leader this week, with 12M downloads dwarfing all other entries. In the **specialized** space, Nvidia is aggressively deploying both ASR and embedding models from the Nemotron 3.x family, while openbmb is pioneering **vision-language-action** models for robotics, a nascent but high-potential category. The fine-tuning community is increasingly polarized between **uncensored/abliterated** variants (HauhauCS, DavidAU) and **reasoning-enhanced** models (GnLOLot, empero-ai), reflecting two major user demand vectors.

---

## Worth Exploring

1. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — With 4.3k likes and a novel MoE-DSA architecture, this model is worth studying as a potential frontier open-weight LLM competitor to Qwen and Llama-based systems. Its architecture deviates from the dominant Qwen lineage, making it valuable for research.

2. **[MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — As one of the few vision-language-action models on the hub, this represents an emerging paradigm where LLMs directly control robotic actions. It's worth exploring for anyone interested in embodied AI or robotic manipulation research.

3. **[Needle](https://huggingface.co/Cactus-Compute/needle)** — A JAX-native function-calling model is rare on HF. Its growing likes (298) and tool-use specialization make it a compelling candidate for agentic workflows and LLM tool orchestration research.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*