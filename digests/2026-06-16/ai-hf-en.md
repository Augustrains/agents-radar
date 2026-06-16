# Hugging Face Trending Models Digest 2026-06-16

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-16 02:32 UTC

---

Here is the structured Hugging Face Trending Models Digest for 2026-06-16.

---

## Hugging Face Trending Models Digest – 2026-06-16

### 1. Today’s Highlights

This week’s trending models are dominated by the explosive adoption of Google’s **Gemma 4** family, with nearly half a dozen fine-tunes and quantizations (from Unsloth and community members) appearing in the top 30. **DeepSeek-V4-Pro** leads all models by a wide margin in both likes and downloads, solidifying the "V4" generation as a benchmark for open-weight reasoning. Vision-language models are now the norm—most top entries are `image-text-to-text` pipelines—and community "uncensored" fine-tunes of Qwen 3.6 and Claude-inspired variants continue to draw massive download counts. On the generation side, **Ideogram 4** and **Nvidia’s LocateAnything-3B** signal strong enterprise and creative interest in specialized image understanding and generation.

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai, 4,866 likes, 2.93M downloads. A massive open-weight conversational model; trending as the highest-liked model overall, likely due to strong reasoning benchmarks and permissive licensing.
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai, 746 likes, 56.8K downloads. A code-focused image-text-to-text model with compressed tensors, gaining traction for multimodal code reasoning.
- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs, 389 likes, 11.1K downloads. A compact MoE text-generation model optimized for code tasks, part of Cohere’s new North series.
- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — nex-agi, 288 likes, 3.7K downloads. A Qwen 3.5 MoE–based conversational model, seeing early interest for its Pro-tier reasoning.
- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** — nex-agi, 220 likes, 8.3K downloads. The smaller sibling of Nex-N2-Pro, likely trending for local deployment scenarios.
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft, 104 likes, 13 downloads. A 4B parameter SFT model optimized for long-context tasks; downloads are low but signal research interest.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia, 2,056 likes, 86.9K downloads. A 3B vision-language model for object localization; trending due to its surprising accuracy at small scale.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS, 1,854 likes, 2.7M downloads. An uncensored MoE vision-language model; one of the most downloaded models, riding the "uncensored" trend.
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google, 1,034 likes, 1.16M downloads. The flagship instruction-tuned any-to-any model from Google’s Gemma 4 series; trending for its unified multimodal capability.
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — ideogram-ai, 547 likes, 10.7K downloads. A text-to-image diffusion model in FP8 precision; popular for efficient high-quality generation.
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai, 445 likes, 38.4K downloads. A 4B multimodal TTS model built on Qwen 3; gaining traction for expressive speech synthesis.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia, 422 likes, 5.2K downloads. A streaming ASR model with cache-aware architecture; trending for real-time speech use cases.
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — ideogram-ai, 345 likes, 4.2K downloads. A 4-bit NF4 quantized version of Ideogram 4, popular for memory-constrained image generation.
- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google, 882 likes, 311.8K downloads. A 26B diffusion-language hybrid MoE model; trending for its novel approach to image-text-to-text generation.
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI, 809 likes, 14.3K downloads. A multimodal MoE model; gaining interest for agentic and vision-language tasks.
- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — zai-org, 190 likes, 0 downloads. A pose-driven character animation model with diffusers; notable for its specialized video-generation pipeline.
- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** — Zyphra, 90 likes, 414 downloads. An Apache 2.0 licensed TTS model; small but notable for its permissive open-source release.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- No dedicated medical or math models appear in the top 30; code models are covered under LLMs (Kimi-K2.7-Code, North-Mini-Code-1.0).

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1, 632 likes, 20.2K downloads. A GGUF quant of Gemma 4 fine-tuned for code and reasoning; popular for local coding assistants.
- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — unsloth, 276 likes, 107.2K downloads. Unsloth’s GGUF version of Google’s diffusion-language model; enables local deployment of this 26B MoE.
- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS, 325 likes, 70.7K downloads. A community fine-tune of Gemma 4; trending for its aggressive uncensored tuning.
- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — DavidAU, 356 likes, 369.5K downloads. An extreme community fine-tune merging Qwen 3.6 with Claude-style thinking; massive downloads for an "uncensored + code" hybrid.
- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth, 617 likes, 980.8K downloads. The most popular GGUF variant of Gemma 4; nearly 1M downloads, essential for local inference.
- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — unsloth, 243 likes, 288.4K downloads. A quantization-aware trained GGUF of Gemma 4, offering better accuracy at lower bitwidths.
- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — unsloth, 101 likes, 9.3K downloads. The GGUF version of Kimi’s code model; growing interest in code GGUF quantizations.
- **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)** — unsloth, 83 likes, 14.8K downloads. GGUF quant of MiniMax-M3, enabling local multimodal deployment.
- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Jackrong, 202 likes, 62.5K downloads. A GGUF quant of a Qwen 3.6 coder variant; trending for llama.cpp compatibility.
- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)** — Jackrong, 312 likes, 184.4K downloads. An updated version of the same Qwen-based GGUF; strong download numbers reflect community interest in this quantization series.
- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** — prefeitura-rio, 303 likes, 188.7K downloads. A massive 397B Qwen 3.5 MoE model from a Brazilian organization; notable for its scale and open release.

### 3. Ecosystem Signal

Two dominant trends emerge this week. First, **the Gemma 4 ecosystem is exploding**: Google’s base models (#10, #28) are popular, but community quantizations (#8, #21, #26) and fine-tunes (#2, #4, #11) are collectively accumulating millions of downloads. Unsloth has become the de facto quantization provider for nearly every major release. Second, **"uncensored" and "thinking" variants are a powerful amplifier**: models like HauhauCS’s Qwen3.6 uncensored (#9) and DavidAU’s Claude–Qwen hybrid (#24) are among the most downloaded despite their experimental nature. This signals a strong user demand for alignment-free or alternative-alignment models. Open-weight models (DeepSeek V4, Gemma 4, Qwen 3.6) are clearly winning over proprietary stacks for community experimentation, with MoE architectures (A4B, A3B) becoming the standard for efficient scaling.

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A remarkably small (3B) but highly accurate object localization model. Worth studying for practitioners who need vision-language grounding on edge devices or low-budget hardware. Its high like-to-download ratio suggests strong qualitative performance.

2. **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — A pose-driven character animation model using diffusers. While still at 0 downloads, its `image-to-video` pipeline and specialized tags (character-animation, pose-driven) point to an emerging niche in controllable video generation—worth trying for researchers in the animation/gaming space.

3. **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — With nearly 1 million downloads, this is the most accessible entry point for the Gemma 4 family. It’s the safest bet for anyone wanting to test Google’s latest unified model locally, and its quantization quality sets a benchmark for the ecosystem.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*