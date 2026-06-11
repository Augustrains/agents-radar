# Hugging Face Trending Models Digest 2026-06-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-11 02:14 UTC

---

# 🤗 Hugging Face Trending Models Digest — June 11, 2026

## 📌 Today's Highlights

DeepSeek-V4-Pro dominates the leaderboard with **4,761 weekly likes** and over **4 million downloads**, signaling strong community appetite for large-scale conversational MoE models. The **Gemma-4 family** continues to expand rapidly, with Google releasing multiple variants (12B, 26B MoE, quantized GGUF versions) and a vibrant ecosystem of community fine-tunes and abliterated versions. **NVIDIA's LocateAnything-3B** emerged as a standout specialized vision-language model, while **ideoogram-4** solidified its position as a leading text-to-image diffusion system. The week also saw strong momentum in **streaming ASR** (NVIDIA Nemotron 3.5) and **multimodal TTS** (Boson Higgs Audio), highlighting a clear trend toward real-time, multi-format AI systems.

---

## 🧠 Language Models (LLMs, Chat, Instruction-Tuned)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,761 | 4,061,006 | Next-generation conversational MoE model, trending as the most-liked model of the week |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16) | nvidia | 189 | 59,066 | Massive 550B-parameter MoE model with 55B active parameters, pushing open-weight frontier |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 158 | 91,117 | FP4 quantized variant of Nemotron Ultra for extreme memory efficiency |
| [Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash) | stepfun-ai | 363 | 50,187 | Vision-language model from StepFun with strong multimodal reasoning capabilities |
| [Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro) | nex-agi | 181 | 1,185 | MoE model based on Qwen3.5 architecture, optimized for image-text-to-text tasks |
| [Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini) | nex-agi | 136 | 1,222 | Smaller companion to N2-Pro, efficient multimodal MoE |
| [JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking) | JetBrains | 281 | 18,273 | 12B-parameter MoE with thinking capabilities, designed for coding and reasoning workflows |
| [LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B) | LiquidAI | 582 | 142,134 | Ultra-efficient 8B MoE with only 1B active parameters, ideal for edge deployment |
| [CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) | CohereLabs | 260 | 1,859 | Specialized code generation model from Cohere's North series, MoE architecture |
| [sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B) | sapientinc | 740 | 134,752 | 1B-parameter HRM (human resource management) text model, niche but highly adopted |

---

## 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) | google | 889 | 675,936 | Flagship any-to-any multimodal model from Google, capable of image/text/audio understanding |
| [google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B) | google | 503 | 140,221 | Base (non-instruction) variant of Gemma-4-12B for fine-tuning and research |
| [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 1,806 | 131,794 | Specialized 3B vision-language model for object localization and segmentation tasks |
| [ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8) | ideogram-ai | 474 | 7,170 | FP8 quantized version of Ideogram-4 text-to-image model, efficient image generation |
| [ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4) | ideogram-ai | 308 | 6,124 | NF4 quantized variant of Ideogram-4, further reducing memory footprint |
| [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it) | google | 241 | 0 | New diffusion-based multimodal model using Gemma backbone, 26B MoE |
| [bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 324 | 19,948 | 4B-parameter TTS model from Boson AI, built on Qwen3 architecture |
| [google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2) | google | 174 | 19,806 | Real-time text-to-audio generation model optimized for TFLite deployment |
| [MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS) | MisoLabs | 186 | 0 | New TTS model with PyTorch safetensors, designed for voice synthesis |
| [ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R) | ByteDance | 210 | 305 | Image-to-video generation model with Apache 2.0 license |
| [jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo) | jdopensource | 127 | 5,457 | Text-to-video generation with integrated audio-video capabilities, based on LTX-Video |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,634 | 3,057,541 | Uncensored 35B MoE vision-language model with aggressive tuning, very high download count |
| [Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4) | Comfy-Org | 127 | 0 | ComfyUI integration for Ideogram-4, enabling local image generation workflows |

---

## 🔧 Specialized Models (ASR, Code, Streaming)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 348 | 4,965 | Cache-aware streaming ASR model for real-time speech recognition at only 0.6B parameters |

---

## 📦 Fine-tunes & Quantizations (Community, GGUF, AWQ)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 550 | 711,706 | Highly optimized GGUF quant of Gemma-4-12B-it by Unsloth, most downloaded quant |
| [unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF) | unsloth | 189 | 148,252 | QAT (Quantization-Aware Training) GGUF variant for improved quality at low bitwidths |
| [unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF) | unsloth | 131 | 129,110 | 26B MoE QAT GGUF, enabling Gemma-4 large models on consumer hardware |
| [google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf) | google | 123 | 96,749 | Official Google QAT GGUF, demonstrating commitment to on-device deployment |
| [OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED) | OBLITERATUS | 214 | 14,838 | Community "abliterated" (censorship removed) variant of Gemma-4-12B |
| [huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated) | huihui-ai | 136 | 6,400 | Another abliterated Gemma-4 variant, part of growing uncensored model trend |

---

## 🌐 Ecosystem Signal

**Gemma-4 ecosystem explosion**: Google's Gemma-4 family has created the most active fine-tuning and quantization ecosystem seen this year. With 10+ variants across base, instruction, GGUF, QAT, and abliterated versions, the community is treating it as the new default multimodal backbone.

**MoE dominance continues**: Nearly two-thirds of trending models use Mixture-of-Experts architectures (DeepSeek-V4-Pro, Nemotron-3 Ultra, LFM2.5, Mellum2, all Gemma-4 MoE variants). Active parameters range from 1B to 55B in the same model family, enabling deployment flexibility from edge to datacenter.

**Open-weight vs proprietary**: This week is overwhelmingly open-weight. All 30 trending models are available for download, with NVIDIA, Google, ByteDance, and DeepSeek releasing under permissive licenses. The notable exception is Ideogram-4 (Comfy-Org wrapper under "other" license) — but even that is locally runnable.

**Quantization maturity**: GGUF and QAT variants now appear as official releases from Google and NVIDIA, signaling that quantization is no longer a community-only effort. NVFP4 (NVIDIA's custom 4-bit format) shows hardware-software co-optimization is gaining traction.

---

## 💡 Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With **1,806 likes** and the highest likes-per-download ratio among large models, this specialized vision model for object localization is rare in its focus. It represents a shift from general-purpose VLMs to task-specific, efficient models — ideal for robotics, autonomous driving, and medical imaging.

2. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — An 8B MoE with only **1B active parameters** is a remarkable engineering achievement. For developers deploying on edge devices or seeking extreme inference efficiency without sacrificing quality, this model sets a new benchmark.

3. **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — This **cache-aware streaming ASR** model at just 0.6B parameters is the first to explicitly optimize for real-time, low-latency speech recognition. For voice interfaces, live captioning, or agentic speech systems, it's a must-try.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*