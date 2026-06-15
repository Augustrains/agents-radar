# Hugging Face Trending Models Digest 2026-06-15

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-15 02:29 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-15

## Today's Highlights

This week's trending models signal a clear acceleration toward **native multimodal architectures** and **MoE-based efficiency breakthroughs**. Google's **DiffusionGemma-26B-A4B-it** (800 likes) and the massively popular **DeepSeek-V4-Pro** (4,834 likes, 3M+ downloads) dominate the top spots, while **Qwen3.6** and **Gemma-4** family variants continue to spawn a vibrant ecosystem of fine-tunes, quantizations, and uncensored derivatives. Notably, **NVIDIA's LocateAnything-3B** (2,004 likes) confirms that specialized grounding models are finding strong community traction alongside general-purpose LLMs. The quantization wave remains relentless, with **GGUF variants** from unsloth and community finetuners accounting for nearly a third of the top-30.

---

## Trending Models by Category

### 🧠 Language Models

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,834 likes, 3.1M downloads  
  The standout open-weight LLM release this cycle, likely a massive MoE model pushing reasoning and conversational quality — its explosive adoption signals strong community trust in DeepSeek's lineage.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 369 likes, 9.9K downloads  
  A compact code-focused MoE model from Cohere's "North" family, trending as a lightweight alternative for coding assistant workloads.

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — prefeitura-rio | 275 likes, 112K downloads  
  An enormous Qwen3.5-based MoE model (397B parameters) released by a Brazilian public institution — notable for its scale and open governance.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — nex-agi | 259 likes, 3.4K downloads  
  A Qwen3.5-MoE based text-generation model optimized for production-grade agentic tasks.

- **[silx-ai/Quasar-Preview](https://huggingface.co/silx-ai/Quasar-Preview)** — silx-ai | 73 likes, 307 downloads  
  A preview of a new long-context LLM from silx-ai, worth watching for its "quasar_long" architecture tag.

### 🎨 Multimodal & Generation

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | 800 likes, 199K downloads  
  Google's flagship multimodal MoE — a 26B-parameter model with 4B active parameters, blending diffusion and language for image-text-to-text tasks.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,004 likes, 75K downloads  
  A specialized spatial grounding model that lets users locate any object in images via text — trending hard for robotics and UI automation applications.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — ideogram-ai | 535 likes, 8.3K downloads  
  FP8 quantized version of the latest Ideogram text-to-image model, offering high-quality generation with reduced resource requirements.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 427 likes, 35K downloads  
  A 4B-parameter TTS model based on Qwen3 backbone, trending for its natural-sounding speech synthesis.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — zai-org | 175 likes, 0 downloads  
  A pose-driven character animation model (image-to-video) — niche but innovative, using diffusers for animation pipelines.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 412 likes, 4.5K downloads  
  NVIDIA's streaming ASR model with cache-aware architecture, targeting real-time speech transcription.

### 🔧 Specialized Models

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 635 likes, 15K downloads  
  A compressed-tensor code model from Moonshot AI (Kimi) — designed for efficient code understanding and generation.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | 494 likes, 6.6K downloads  
  Pro-level multimodal model (image-text-to-text) with strong conversational ability — a serious contender in the multimodal space.

### 📦 Fine-tunes & Quantizations

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 1,808 likes, 2.5M downloads  
  An aggressively fine-tuned, uncensored Qwen3.6 MoE model with massive download numbers — the most popular community derivative this week.

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth | 598 likes, 926K downloads  
  The most downloaded GGUF variant of Gemma-4-12B-it, making this powerful multimodal model accessible on consumer hardware.

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — DavidAU | 337 likes, 376K downloads  
  An "everything-and-the-kitchen-sink" fine-tune merging multiple model lineages, reflecting the community's appetite for uncensored, multi-capability models.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — unsloth | 261 likes, 80K downloads  
  GGUF quantization of Google's DiffusionGemma, bringing MoE multimodal generation to CPU/edge inference.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Jackrong | 182 likes, 33.7K downloads  
  A code-optimized GGUF of Qwen3.6-27B with Multi-Turn Processing support.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS | 302 likes, 60.9K downloads  
  An "obliterated" (heavily fine-tuned) version of Gemma-4-12B, likely removing safety filters for uncensored use.

---

## Ecosystem Signal

**Model Family Momentum**: The **Qwen3.6** ecosystem is currently the most active — spawning multiple fine-tunes, GGUF quantizations, and specialized variants (coder, uncensored, aggressive). **Gemma-4** is close behind, with Google's official releases and community quantizations dominating downloads (the unsloth GGUF variants alone have crossed 1M+ cumulative downloads). **DeepSeek-V4-Pro's** explosive launch suggests it may become the next dominant open-weight LLM family after Qwen and Llama.

**Architecture Trends**: The list is heavily skewed toward **Mixture-of-Experts (MoE)** models — nearly 70% of entries use MoE architectures. The active-parameter counts (e.g., 4B active out of 26B total in DiffusionGemma, 3B active out of 35B in Qwen3.6 variants) confirm that sparse activation is now the default for high-capability models. The **any-to-any** pipeline tag (Gemma-4) and **image-text-to-text** dominance reflect the post-text-only era: multimodal is no longer optional.

**Quantization & Fine-Tuning Activity**: GGUF variants continue to be the primary vehicle for community consumption — unsloth alone accounts for 5 of the top-30 models. The explosion of "uncensored" and "heritic" fine-tunes (e.g., HauhauCS, DavidAU, OBLITERATUS) indicates a sustained community desire for models without safety guardrails, especially for creative writing and roleplay use cases.

**Open-Weight Signal**: All top-30 models are open-weight, with major labs (Google, DeepSeek, NVIDIA, Cohere) leading official releases. The "uncensored fine-tune" trend is entirely community-driven, suggesting the ecosystem's center of gravity remains firmly in open-weight territory.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
   - **Why**: It's the highest-likes non-LLM model (2,004) and represents a breakthrough in spatial grounding at small scale (3B). For developers building vision-based agents, robotics pipelines, or UI automation, this model is immediately practical. Its "locateanything" tag suggests it generalizes well beyond typical detection models.

2. **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**
   - **Why**: Despite zero downloads (likely fresh), this pose-driven image-to-video model represents an emerging frontier — controlled character animation from a single image. For researchers and creators in animation, game development, and virtual avatar generation, this is a model to watch and experiment with early.

3. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
   - **Why**: With 2.5M downloads and 1,808 likes, this is the most popular community model this cycle. It represents the convergence of three important trends: MoE efficiency (35B total/3B active), uncensored tuning, and the Qwen3.6 ecosystem. Studying its performance and usage patterns provides insight into what the open-weight community actually wants and uses at scale.

---

*Data sourced from Hugging Face Hub trending page (2026-06-15). Rankings based on weekly likes.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*