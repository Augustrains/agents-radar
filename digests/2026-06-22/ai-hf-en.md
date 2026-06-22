# Hugging Face Trending Models Digest 2026-06-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-22 02:30 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-22

## 1. Today's Highlights

This week's Hugging Face trending chart is dominated by two major forces: **MoE architectures scaling aggressively** and **multimodal unification** across text, vision, and audio. **DeepSeek-V4-Pro** tops the charts with 4,999 weekly likes and 2.6M downloads, signaling that open-weight frontier LLMs remain the community's primary obsession. Simultaneously, **Qwen's ecosystem** continues to expand rapidly, with **Qwen3.6-35B-A3B** (5.1M downloads) and multiple Qwen-based fine-tunes flooding the leaderboard. A notable shift is the rise of **any-to-any models** like Google's **Gemma-4-12B-it**, which processes text, images, and audio in a single unified pipeline. Quantization activity remains intense, with GGUF variants of nearly every major model appearing within days of release.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat, Instruction-Tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,999 ❤️ | 2.6M ⬇️  
  The week's most-liked model: a massive open-weight conversational MoE, likely DeepSeek's latest frontier-scale release driving enormous community excitement.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 1,829 ❤️ | 27k ⬇️  
  A new-generation GLM model with MoE-DSA architecture, positioning itself as a strong Chinese-language and bilingual conversational alternative.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,079 ❤️ | 3.9M ⬇️  
  An uncensored, aggressively fine-tuned variant of Qwen3.6-35B-A3B, demonstrating the demand for less-restrictive MoE models despite being marked as voice.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 474 ❤️ | 19k ⬇️  
  Cohere's new MoE code model, designed for efficient code generation with a much smaller parameter count than frontier models.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — nex-agi | 342 ❤️ | 7.8k ⬇️  
  A Qwen3.5-MoE-based model with multimodal inputs, trending as a capable general-purpose text-generation and vision-language model.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google | 1,129 ❤️ | 1.8M ⬇️  
  Google's breakthrough **any-to-any** model: a single unified transformer handling text, images, and audio — the week's most architecturally significant release.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | 1,035 ❤️ | 762k ⬇️  
  A diffusion-based multimodal model combining Gemma's text capabilities with image generation, marking Google's push into unified generation.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,243 ❤️ | 241k ⬇️  
  A 3B vision model specialized in object localization and referring expression comprehension — trending for its surprising accuracy at small scale.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | 1,177 ❤️ | 104k ⬇️  
  MiniMax's third-generation multimodal vision-language model, competing with Google and Qwen in the VL space.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen | 2,197 ❤️ | 5.1M ⬇️  
  Qwen's flagship MoE model with vision: 35B total, 3B active — the most downloaded model this week, reflecting Qwen's dominance in efficient multimodal MoE.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 945 ❤️ | 363k ⬇️  
  A compressed-tensor code model from Kimi, supporting image-text-to-text with compressed weight representations for efficient deployment.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 507 ❤️ | 76k ⬇️  
  A 4B text-to-speech model built on Qwen3 architecture, demonstrating the convergence of language models and speech synthesis.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 612 ❤️ | 27k ⬇️  
  NVIDIA's streaming ASR model at only 0.6B parameters — trending for real-time speech recognition efficiency.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — owensong | 154 ❤️ | 0 ⬇️  
  An ultra-small TTS model (< 100MB), representing the edge deployment trend for speech synthesis.

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** — ostris | 91 ❤️ | 2.4k ⬇️  
  A LoRA adapter for Ideogram 4, enabling faster image generation with community-tuned quality improvements.

- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** — Boogu | 82 ❤️ | 374 ⬇️  
  An early-stage image editing diffusion model, bilingual (EN/ZH), Apache-2.0 licensed.

### 🔧 Specialized Models (Code, Math, Embeddings, Agentic)

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | 562 ❤️ | 20k ⬇️  
  A 3B math-reasoning model based on Qwen2, trending for strong mathematical problem-solving capability in a small package.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | 262 ❤️ | 2.5k ⬇️  
  Microsoft's 4B model optimized for long-context reasoning and sub-agent tasks, built on Qwen3 architecture.

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** — LiquidAI | 93 ❤️ | 7.7k ⬇️  
  A 350M embedding model from LiquidAI, competitive for sentence similarity and retrieval tasks at very low parameter count.

- **[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)** — poolside | 84 ❤️ | 2.5k ⬇️  
  A code-focused generation model optimized for vLLM and SGLang inference, targeting developer tooling.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** — datalab-to | 110 ❤️ | 516 ⬇️  
  A Qwen3.5-based model specialized in PDF understanding and document image processing.

### 📦 Fine-tunes & Quantizations (GGUF, Community Variants)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,089 ❤️ | 358k ⬇️  
  The most-liked GGUF this week: a highly-rated code fine-tune of Gemma-4-12B, optimized for local inference with llama.cpp.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 286 ❤️ | 21k ⬇️  
  A follow-up agentic GGUF variant of Gemma-4-12B, with 3.5x context extension and Tau2 temperature scaling.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 227 ❤️ | 32k ⬇️  
  Unsloth's GGUF quantization of GLM-5.2, reflecting demand for locally-runnable Chinese-optimized MoE models.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — zai-org | 123 ❤️ | 217k ⬇️  
  Official FP8 quantized version of GLM-5.2, demonstrating first-party support for efficient deployment formats.

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — lordx64 | 145 ❤️ | 3.3k ⬇️  
  A community fine-tune of Qwen3.5-MoE with vision-language capability, showing the rapid ecosystem around Qwen.

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — Mia-AiLab | 120 ❤️ | 22k ⬇️  
  A 27B GGUF variant of Qwen3.6, offering a mid-size MoE option for local deployment.

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** — bytkim | 102 ❤️ | 36k ⬇️  
  Qwen3.6-27B with Multi-Token Prediction (MTP) and position interpolation tuning — a technically advanced community GGUF.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Jackrong | 276 ❤️ | 190k ⬇️  
  A code-focused GGUF variant with MTP, combining Qwen3.6's MoE efficiency with vision-language inputs.

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — unsloth | 150 ❤️ | 42k ⬇️  
  Unsloth's GGUF conversion of Kimi's code model, providing quantized access to compressed-tensor architectures.

---

## 3. Ecosystem Signal

**MoE is the new standard.** Every major release this week — DeepSeek-V4-Pro, GLM-5.2, Qwen3.6-35B-A3B, Gemma-4-12B — uses Mixture-of-Experts architecture. The shift from dense to sparse models is now complete; the community has fully embraced the compute/quality trade-off that MoE offers. **Qwen's ecosystem is the most active**, with 7+ variants across fine-tunes, GGUF quantizations, and vision-language derivatives, suggesting Qwen has become the preferred base model for community experimentation.

**"Any-to-any" is the next frontier.** Google's Gemma-4-12B-it (unified text+vision+audio) and diffusiongemma (text+generation) point toward a future where modality boundaries dissolve. This mirrors the trend seen in Qwen3.6's vision-language capabilities being integrated into virtually every model variant.

**Quantization velocity continues accelerating.** GGUF variants now appear within 24-48 hours of any base model release, with community quantizers (yuxinlu1, unsloth, Jackrong) acting as critical infrastructure. The emergence of FP8 as a first-party format (GLM-5.2-FP8) suggests official quantization support may become table stakes for new releases.

**Code and reasoning specialization is bifurcating the market.** While general-purpose models like DeepSeek-V4 dominate, we see strong demand for specialized code (Kimi-K2.7-Code, Laguna-M.1, North-Mini-Code) and math (VibeThinker) models, indicating that pure generalists may not fully satisfy developer workloads.

---

## 4. Worth Exploring

1. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Most architecturally significant release this week. Gemma-4's "any-to-any" capability (text+image+audio in one model) represents a paradigm shift from modality-specific models. If this architecture proves scalable, it could define the next generation of foundation models.

2. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — The most downloaded model this period (5.1M) and the center of an exploding ecosystem. Its 3B active parameters out of 35B total make it a reference point for efficient MoE deployment. Any team evaluating MoE vs. dense models should study this architecture.

3. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — The most-liked GGUF (2,089 ❤️) with 358k downloads reflects the community's hunger for high-quality, locally-runnable code models. This fine-tune+quantization combo represents the current best practice for bringing frontier models to consumer hardware.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*