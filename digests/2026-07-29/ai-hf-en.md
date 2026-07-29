# Hugging Face Trending Models Digest 2026-07-29

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-29 01:19 UTC

---

# Hugging Face Trending Models Digest — 2026-07-29

## Today's Highlights

Kimi-K3 from Moonshot AI dominates this week with nearly 8,000 likes, signaling strong community interest in compressed, efficient multimodal models. Baidu's Unlimited-OCR breaks 2.6 million downloads, reflecting surging demand for production-grade OCR pipelines. The Qwen 3.6 family continues its explosive growth, with the 35B-A3B MoE variant accumulating over 6 million downloads and spawning numerous community fine-tunes. Microsoft enters the multimodal space aggressively with Mage-Flow and Fara1.5-27B, while ternary quantization and sub-2-bit compression from prism-ml mark a notable push toward extreme model size reduction.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — poolside | 801 likes, 67k downloads  
  A 2.1-generation LLM optimized for enterprise software engineering, gaining traction for its balanced performance and multiple quantization variants.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — upstage | 645 likes, 4.8k downloads  
  A massive 250B open-weight model from Upstage, notable for pushing the frontier of open-source LLM scale.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Nanbeige | 527 likes, 18.9k downloads  
  A compact 3B parameter model with strong conversational capabilities, trending as an efficient on-device LLM candidate.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,604 likes, 1.27M downloads  
  The latest generation of the GLM MoE-DSA architecture, achieving high conversational quality with sparse activation efficiency.

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 1,084 likes, 665k downloads  
  An extreme 2-bit ternary quantization of a 27B model, pushing the boundaries of compression while maintaining conversational quality.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 678 likes, 2.34M downloads  
  A 1-bit quantized 27B model, demonstrating remarkable community interest in ultra-compact LLM variants for local inference.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — fdtn-ai | 222 likes, 7.7k downloads  
  A 1B GraniteMoEHybrid model focused on security, trending for its specialized safety alignment in a small footprint.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — moonshotai | 7,993 likes, 99k downloads  
  A top-tier multimodal model integrating vision and language with compressed-tensor efficiency, leading this week's trends.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 3,417 likes, 2.69M downloads  
  An OCR model designed for unlimited-scene text recognition, dominating downloads with production-ready accuracy.

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — microsoft | 416 likes, 2k downloads  
  A text-to-image generation and editing pipeline from Microsoft, showcasing unified image control flows.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,625 likes, 39k downloads  
  A multimodal conversational model with strong vision-language integration, trending for its high-quality interactions.

- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — microsoft | 179 likes, 1.5k downloads  
  A Qwen3.5-based multimodal model focused on computer-use scenarios, representing Microsoft's entry into agentic vision-language models.

- **[microsoft/Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** — microsoft | 109 likes, 1.3k downloads  
  A fast variant of Mage-Flow specialized for instruction-based image editing.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — owensong | 264 likes, 645 downloads  
  A lightweight text-to-speech model optimized for CPU and edge deployment, notable for local TTS accessibility.

- **[owensong/Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2)** — owensong | 104 likes, 434 downloads  
  An even smaller TTS variant, pushing the limits of speech synthesis on low-resource devices.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 565 likes, 0 downloads  
  A LoRA adapter for Krea-2 enabling identity-preserving image edits, trending despite zero download count (likely very recent).

### 🔧 Specialized Models (code, math, medical, embeddings, OCR)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — Kwaipilot | 287 likes, 6.3k downloads  
  A Qwen3.5-MoE-based code generation model, trending for its MoE architecture optimized for developer workflows.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | 339 likes, 47k downloads  
  A Qwen3.5-based OCR model delivering high-accuracy text extraction in complex scenes.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 1,332 likes, 681k downloads  
  A code-specialized variant of the Kimi model family, gaining traction for its compressed-tensor coding capabilities.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711...](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 852 likes, 736k downloads  
  An uncensored Qwen3.6 fine-tune in GGUF format, highly downloaded for its aggressive personality and roleplay use cases.

- **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** — unsloth | 232 likes, 129k downloads  
  GGUF quantization of Laguna-S-2.1 by Unsloth, enabling efficient local inference of this enterprise coding model.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 3,159 likes, 1.86M downloads  
  An uncensored Qwen3.6 MoE vision fine-tune with aggressive personality tuning, extremely popular in the uncensored model community.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF)** — LuffyTheFox | 198 likes, 99k downloads  
  Another uncensored Qwen3.6 variant, this one blending Hermes-style alignment with GGUF quantization.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,502 likes, 1.26M downloads  
  A Qwen3.5-based reasoning model in GGUF format, capturing attention for its Claude-inspired mythos-style training.

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** — baseten | 131 likes, 2.8k downloads  
  An NVFP4 quantized multimodal version of GLM-5.2, optimized for deployment via SGLang.

- **[poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)** — poolside | 153 likes, 180k downloads  
  NVFP4 quantization variant of Laguna-S-2.1, optimized for vLLM inference with minimal quality loss.

- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** — poolside | 160 likes, 90k downloads  
  Official GGUF variant of Laguna-S-2.1, enabling broad compatibility with GGUF-based inference engines.

- **[unsloth/Kimi-K3-(GGUF)](https://huggingface.co/unsloth/Kimi-K3)** — unsloth | 147 likes, 410 downloads  
  Unsloth's GGUF conversion of Kimi-K3 for efficient multimodal inference on consumer hardware.

- **[unsloth/Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF)** — unsloth | 88 likes, 0 downloads  
  Dedicated GGUF variant of Kimi-K3, likely uploaded very recently.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen | 2,569 likes, 6.16M downloads  
  The base Qwen3.6 MoE vision-language model, an absolute download leader driving the entire Qwen3.6 fine-tune ecosystem.

## Ecosystem Signal

**Qwen 3.6 is the dominant ecosystem of the week.** The base model at 6.1M downloads and at least four community fine-tunes (DavidAU, HauhauCS, LuffyTheFox) with 1–2M downloads each demonstrate an unprecedented fine-tuning wave. The uncensored subculture on Qwen3.6 variants (A3B MoE vision models) has become a major trend, suggesting strong demand for roleplay and creative writing models.

**Compression innovation is accelerating.** prism-ml's Ternary-Bonsai (2-bit) and Bonsai (1-bit) at 27B scale, combined with NVFP4 quantizations from baseten and poolside, point to a community push for running large models on consumer hardware. The success of these ultra-low-bit models (2.3M downloads for Bonsai) validates that many users prioritize local inference over raw quality.

**Multimodal shifts from text-only to vision-language.** 10 of the top 30 models are `image-text-to-text`, signaling that multimodal capabilities are no longer niche. Microsoft's dual entry with Mage-Flow (image gen) and Fara1.5-27B (vision-language) suggests major players are investing heavily in unified multimodal architectures.

**Text-to-speech is emerging.** Owensong's Inflect series (Micro/Nano) marks early but growing interest in local, CPU-friendly TTS — a potential breakout area for edge AI in 2026.

## Worth Exploring

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 7,993 likes in one week, this is the breakout model. Its compressed-tensor approach for multimodal efficiency could define a new class of deployment-friendly vision-language models. Worth studying for architecture and compression techniques.

2. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — At 2-bit ternary quantization on a 27B model, this represents the bleeding edge of model compression. Evaluating its quality-compression tradeoff is essential for anyone building local inference pipelines.

3. **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — Given the explosive downloads of Baidu's Unlimited-OCR and the Qwen3.5 base, OvisOCR2 sits at the intersection of OCR specialization and MoE architecture — a promising candidate for production OCR pipelines using efficient sparse models.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*