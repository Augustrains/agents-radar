# Hugging Face Trending Models Digest 2026-06-10

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-10 02:03 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-10

## 1. Today's Highlights

This week's Hugging Face trending board is dominated by the **Gemma 4 family** from Google, with multiple variants (12B, 26B, GGUF, QAT) appearing across the top 30. **DeepSeek-V4-Pro** (#23) takes the absolute crown with 4,740 likes and 4.3M downloads, signaling the community's appetite for massive, high-performance open-weight MoE models. A strong wave of **multimodal models** — from NVIDIA's LocateAnything-3B to ByteDance's Bernini-R video generation — reflects the accelerating convergence of vision, language, and audio capabilities. Quantization remains a key theme, with unsloth's GGUF conversions of Gemma 4 models seeing massive download volumes.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,740 ❤️ | 4.3M ⬇️  
  Massive open-weight MoE conversational model leading the board with unprecedented community engagement and downloads.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — nvidia | 175 ❤️ | 56.9K ⬇️  
  NVIDIA's latest 550B-parameter MoE text-generation model, showcasing extreme scale with active inference support.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 162 ❤️ | 1.8K ⬇️  
  A compact code-focused MoE model from Cohere, trending for its efficient architecture and strong coding performance.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — JetBrains | 272 ❤️ | 17.6K ⬇️  
  JetBrains' thinking-enhanced 12B MoE model, gaining traction for developer tooling integration.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI | 572 ❤️ | 137K ⬇️  
  A highly efficient 8B MoE model from LiquidAI, popular for its strong performance-to-parameter ratio.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — sapientinc | 734 ❤️ | 133K ⬇️  
  A specialized 1B text-generation model for human resource management, trending for domain-specific fine-tuning.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — ideogram-ai | 441 ❤️ | 5.9K ⬇️  
  FP8 quantized version of Ideogram 4 text-to-image model, trending for efficient high-quality generation.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 1,731 ❤️ | 124K ⬇️  
  NVIDIA's vision-language model for object localization and image feature extraction, one of the week's top gainers.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 284 ❤️ | 16.2K ⬇️  
  A 4B multimodal TTS model bridging text generation and speech synthesis, riding the audio-AI wave.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — google | 164 ❤️ | 18.2K ⬇️  
  Google's real-time text-to-audio generation model with TFLite support, trending for music/sound creative applications.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — ByteDance | 195 ❤️ | 281 ⬇️  
  A new image-text-to-video renderer from ByteDance, gaining interest for video generation from visual prompts.

- **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** — jdopensource | 114 ❤️ | 4.5K ⬇️  
  Text-to-video generation model with audio-video synthesis capabilities, representing the video generation frontier.

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — nvidia | 214 ❤️ | 36.7K ⬇️  
  NVIDIA's compact omnimodal model (Cosmos3 family), trending for universal perception and generation.

### 🔧 Specialized Models (code, science, domain-specific)

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 320 ❤️ | 4.2K ⬇️  
  NVIDIA's cache-aware streaming ASR model, trending for real-time speech recognition use cases.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — PaddlePaddle | 280 ❤️ | 10.1K ⬇️  
  Updated vision-language OCR model based on ERNIE 4.5, popular for document AI and text extraction.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — stepfun-ai | 358 ❤️ | 46.7K ⬇️  
  A fast vision-language model, trending for efficient multimodal inference at scale.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth | 532 ❤️ | 660K ⬇️  
  Unsloth's GGUF conversion of Gemma 4-12B, the most-downloaded quantization this week.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS | 141 ❤️ | 8.1K ⬇️  
  Community fine-tune of Gemma-4 with modified behavior, trending in the uncensored model space.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 1,596 ❤️ | 2.98M ⬇️  
  Highly downloaded uncensored MoE vision-language fine-tune, reflecting demand for unaligned multimodal models.

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — unsloth | 115 ❤️ | 96K ⬇️  
  QAT-quantized GGUF of the larger Gemma 4-26B MoE, enabling local deployment of high-capacity vision-language models.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — nvidia | 153 ❤️ | 71.8K ⬇️  
  NVIDIA's NVFP4 (4-bit floating point) quantization of their 550B MoE model, pushing extreme quantization infrastructure.

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — google | 114 ❤️ | 63K ⬇️  
  Official Google QAT-quantized GGUF of Gemma 4-12B, indicating first-party support for local deployment.

## 3. Ecosystem Signal

The **Mixture-of-Experts (MoE) architecture** has become the dominant paradigm, appearing in DeepSeek-V4-Pro, Nemotron-3-Ultra, Gemma-4 (26B variant), Qwen3.6, and nearly every new large model on the board. **Google's Gemma 4 family** is clearly the week's most active ecosystem — with 6+ variants across base, instruction-tuned, QAT-quantized, and GGUF formats — signaling a platform-level push for accessibility across hardware tiers.

**Quantization is no longer an afterthought:** nearly 40% of the top 30 are quantized variants, with unsloth acting as the primary community bridge to local deployment. NVIDIA's NVFP4 and Google's official QAT releases suggest that model creators are increasingly shipping quantized versions as first-class citizens.

**Multimodality is standardizing:** "image-text-to-text" appears as the most common pipeline tag after text-generation, with vision-language capabilities baked into most new LLMs rather than being separate systems. The emergence of specialized audio models (TTS, ASR, and text-to-audio) alongside video generation (JoyAI-Echo, Bernini-R) indicates that 2026 is the year **any-to-any** becomes the default expectation for frontier models.

Notably, **open-weight competition is intensifying**: DeepSeek, Google, NVIDIA, and Cohere all released major open-weight models this week, while the uncensored/fine-tune community continues to drive massive download volumes on derivative works.

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 1,731 likes and a practical image-feature-extraction pipeline, this model represents a new paradigm in "everything detection" vision models. Its compact 3B size makes it deployable on edge hardware while maintaining strong localization performance.

2. **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — At just 1B active parameters (8B total), this model exemplifies the "more with less" MoE trend. Its strong likes-to-downloads ratio and active community interest make it a prime candidate for studying efficient architectures that challenge much larger models.

3. **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — As the largest Gemma 4 variant available in quantized form, this model is the best test case for running frontier multimodal capabilities on consumer hardware (e.g., 24GB+ GPUs). Its QAT quantization preserves quality while enabling local inference of Google's latest multimodal MoE architecture.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*