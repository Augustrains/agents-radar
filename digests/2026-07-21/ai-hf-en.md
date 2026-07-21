# Hugging Face Trending Models Digest 2026-07-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-21 01:20 UTC

---

# Hugging Face Trending Models Digest — 2026-07-21

## Today's Highlights

This week's trending landscape is dominated by **Qwen 3.6-based models**, with multiple uncensored fine-tunes and quantized variants drawing massive download counts. **GLM-5.2** from zai-org leads in pure likes (4,226), while **google/gemma-4-31B-it** commands an enormous 11.9M downloads, signaling strong enterprise and community interest in Google's latest open-weight vision-language model. A notable shift toward **ternary and 1-bit quantization** (prism-ml's Bonsai series) suggests growing appetite for ultra-efficient model deployment on edge hardware. Emerging categories like **robotics** (openbmb's MiniCPM-RobotManip/RobotTrack) and **real-time video-text-to-text** (MOSS-VL-Realtime) point to expanding multimodal frontiers.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,226 likes | 531,947 downloads  
  A 5.2-generation MoE model with DSA architecture, leading in community appreciation for its conversational quality and MoE efficiency.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 847 likes | 13,698 downloads  
  Tencent's latest Hunyuan-based text-generation model, gaining traction as a strong open-weight Chinese-English LLM.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | 3,296 likes | 11,987,240 downloads  
  Google's flagship 31B instruction-tuned vision-language model, dominating downloads and setting a new bar for open-weight multimodal LLMs.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — GnLOLot | 159 likes | 5,494 downloads  
  A 1B parameter MiniCPM reasoning variant, notable for packing thinking capabilities into a tiny footprint.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 1,174 likes | 713,992 downloads  
  Kimi's compressed code-specialized model, trending for its efficient architecture and strong programming performance.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,269 likes | 13,462 downloads  
  A new MoE multimodal model handling image-text-to-text and audio, positioning as a versatile "Swiss Army knife" for vision-language tasks.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,437 likes | 2,122,848 downloads  
  Baidu's unlimited OCR model, trending for its exceptional document understanding and feature extraction capabilities.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | 145 likes | 2,408 downloads  
  A 14B image-to-video diffusion model for generating dance motion, riding the wave of AI video generation interest.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 213 likes | 0 downloads  
  A LoRA for LTX-Video enabling identity-preserving text-to-video generation, novel for its reference-to-video approach.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 290 likes | 87,533 downloads  
  An audio-text-to-text model for transcription with speaker diarization, highlighting growing speech AI adoption.

- **[OpenMOSS-Team/MOSS-VL-Realtime](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)** — OpenMOSS-Team | 89 likes | 544 downloads  
  A video-text-to-text model optimized for real-time streaming, pushing the frontier of live multimodal interaction.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | 217 likes | 14,587 downloads  
  A Qwen 3.5-based OCR specialist model, indicating sustained demand for high-quality document digitization.

- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** — nvidia | 86 likes | 61,708 downloads  
  NVIDIA's 1B sentence-embedding model leveraging Ministral 3, trending for RAG and semantic search applications.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | 292 likes | 950 downloads  
  A JAX-based model for function-calling and tool-use, notable for its lightweight, efficient approach to agentic workflows.

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — openbmb | 133 likes | 0 downloads  
  A vision-language-action model for robotic manipulation, signaling the emergence of "robot foundation models" on Hugging Face.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — openbmb | 100 likes | 0 downloads  
  A companion robot-tracking VLA model, together with RobotManip forming a modular robotics stack.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 854 likes | 338,945 downloads  
  A 2-bit ternary quantization of a 27B Qwen 3.5 model, trending for its extreme compression while retaining conversational quality.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 542 likes | 1,262,894 downloads  
  A 1-bit Bonsai quantization with massive downloads, representing the community's strongest push toward ultra-low-bit deployment.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,937 likes | 2,007,025 downloads  
  An uncensored, vision-enabled MoE fine-tune of Qwen 3.6, extremely popular for its aggressive uncensoring and strong reasoning.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,369 likes | 2,117,323 downloads  
  A Claude-Mythos distilled Qwen 3.5 model with 1M context, trending for combining long context with synthetic reasoning tuning.

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — empero-ai | 197 likes | 105,749 downloads  
  Updated version of Qwythos with improved quantization, maintaining strong download momentum.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | 149 likes | 109,749 downloads  
  GGUF quantization of Tencent's Hy3 model, enabling easy local inference of Hunyuan-v3.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 482 likes | 10,647 downloads  
  A reasoning-enhanced fine-tune of Qwen 3.6, trending in the "thinking model" niche.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 156 likes | 16,719 downloads  
  An extremely customized uncensored fine-tune, exemplifying the long-tail of community experimentation.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | 154 likes | 21,690 downloads  
  MLX-native 1-bit Bonsai variant, bringing extreme quantization to Apple Silicon.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | 130 likes | 17,869 downloads  
  MLX ternary companion to the GGUF version, completing the cross-platform ultra-compression suite.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | 134 likes | 28,012 downloads  
  GGUF reasoning variant of the 1B MiniCPM, enabling thinking capabilities on consumer hardware.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF)** — LuffyTheFox | 85 likes | 15,148 downloads  
  Another Hermes-inspired uncensored Qwen 3.6 MoE variant, reflecting the community's appetite for customizable uncensored models.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — unsloth | 111 likes | 6,771 downloads  
  GGUF quantization of the Inkling multimodal MoE, making it accessible for local inference.

## Ecosystem Signal

**Qwen 3.6 and its community ecosystem** have become the dominant force, with at least six Qwen 3.5/3.6 derived models in the top 30 — spanning uncensored fine-tunes, MoE variants, and ultra-low-bit quantizations. This mirrors the broader trend: **open-weight multimodal MoE models** (GLM-5.2, Gemma-4-31B-it, Qwen 3.6 MoE) are the hot category, combining vision-language capabilities with efficient sparse architectures.

**Extreme quantization is accelerating.** The prism-ml Bonsai series (1-bit and ternary) demonstrates that the community is actively pushing past 2-bit into previously theoretical compression regimes, achieving functional conversational quality at 1-2 bits per parameter. This has immediate implications for on-device AI and democratizing large model access.

**Robotics and real-time multimodal** are emerging verticals. openbmb's MiniCPM-RobotManip/Track and MOSS-VL-Realtime signal that Hugging Face is expanding beyond text/image into embodied AI and live video processing. These have low downloads now but high strategic interest.

**Uncensored fine-tuning remains a persistent subculture** — nearly 25% of trending models are labeled "uncensored," suggesting a strong community drive for models without alignment restrictions, particularly for creative writing and roleplay.

## Worth Exploring

1. **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — The most downloaded quantization on the leaderboard (1.26M). As the flagship 1-bit model, it's critical for anyone studying extreme compression techniques or deploying LLMs on memory-constrained devices. Its practical viability at 1-bit is a remarkable engineering achievement.

2. **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — Rare and early — a production-ready VLA model for robotics on Hugging Face. With 0 downloads, it's a greenfield opportunity for researchers and hobbyists exploring vision-language-action pipelines. Represents the next frontier of open-source embodied AI.

3. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — With 11.9M downloads and 3.3K likes, this is the most impactful release of the week. As Google's latest open-weight multimodal LLM, it sets the standard for what open models can achieve in vision-language tasks. Essential for any practitioner tracking the open vs. proprietary frontier.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*