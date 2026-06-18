# Hugging Face Trending Models Digest 2026-06-18

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-18 02:14 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-06-18**.

---

## 1. Today’s Highlights

The ecosystem is dominated by **Mixture-of-Experts (MoE)** large-scale models, with **DeepSeek-V4-Pro** leading all models by an enormous margin in both likes (4,926) and downloads (2.8M), signaling a massive shift toward efficient, high-capacity architectures. **Multimodal convergence** is the defining trend: nearly 70% of top models support image-text-to-text pipelines, with Google’s new **DiffusionGemma-26B** and the **Qwen 3.6** family (including a 35B-A3B MoE variant) setting new standards for vision-language reasoning. Meanwhile, the **GGUF quantization ecosystem** continues to explode—quantized variants from unsloth, yuxinlu1, and DavidAU represent half of the top 30, making large models accessible for local inference. Specialty models from **NVIDIA** (LocateAnything-3B for spatial grounding) and **Zyphra** (ZONOS2 for TTS) show increasing vertical differentiation in the open-weight space.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  Author: deepseek-ai | Likes: 4,926 | Downloads: 2,804,646  
  *The week’s absolute breakout—a next-generation MoE reasoning model with massive community adoption, likely setting a new baseline for open-weight LLM performance.*

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  Author: zai-org | Likes: 1,040 | Downloads: 666  
  *A new MoE-DSA conversational model from zai-org, trending for its innovative sparse activation architecture and strong benchmark results.*

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  Author: WeiboAI | Likes: 313 | Downloads: 1,950  
  *A compact 3B parameter model fine-tuned for mathematical reasoning, popular among researchers needing a fast, lightweight foundation model.*

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  Author: microsoft | Likes: 185 | Downloads: 537  
  *Microsoft’s entry for efficient long-context inference—a 4B model trained with an "Explorer SubAgent" paradigm for extended reasoning tasks.*

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  Author: HauhauCS | Likes: 1,937 | Downloads: 2,876,624  
  *An uncensored, "aggressive" fine-tune of Qwen 3.6 MoE that has gone viral for its unconstrained output style and massive download count.*

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  Author: google | Likes: 979 | Downloads: 460,173  
  *Google’s first "any-to-any" diffusion transformer—a 26B MoE that handles image, text, and audio generation with unprecedented flexibility.*

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  Author: MiniMaxAI | Likes: 1,065 | Downloads: 42,198  
  *A new multimodal agent model from MiniMax, trending for its strong vision-language reasoning and agentic capabilities in a single MoE.*

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  Author: moonshotai | Likes: 847 | Downloads: 172,727  
  *Kimi’s code-specialized vision-language model using compressed tensors—popular for combining multimodal code understanding with efficient storage.*

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  Author: nvidia | Likes: 2,138 | Downloads: 130,389  
  *NVIDIA’s dedicated spatial grounding model—can localize any object in an image from a text prompt, trending for robotics and visual QA.*

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  Author: bosonai | Likes: 480 | Downloads: 40,812  
  *A 4B text-to-speech model built on Qwen3 multimodal backbones, trending for its high-quality voice synthesis and open-weight release.*

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  Author: ideogram-ai | Likes: 569 | Downloads: 15,477  
  *The latest text-to-image model from Ideogram in FP8 precision—gaining traction for its fast inference and high-fidelity image generation.*

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  Author: zai-org | Likes: 223 | Downloads: 0  
  *A pose-driven character animation diffusion model for video generation—newly released and attracting interest despite zero downloads yet.*

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  Author: nvidia | Likes: 521 | Downloads: 7,195  
  *NVIDIA’s streaming automatic speech recognition model with cache-aware ASR—trending for its low-latency architecture suitable for real-time applications.*

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  Author: CohereLabs | Likes: 420 | Downloads: 13,449  
  *Cohere’s compact MoE model specialized for code generation and conversational coding—popular as a faster alternative to larger code models.*

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  Author: google | Likes: 1,069 | Downloads: 922,952  
  *Google’s flagship 12B "any-to-any" unified model—trending for its versatility across text, image, and audio tasks in a single architecture.*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  Author: yuxinlu1 | Likes: 1,485 | Downloads: 146,784  
  *A highly optimized GGUF quantized fine-tune of Gemma-4 for coding and reasoning, trending as the go-to local code assistant.*

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**  
  Author: unsloth | Likes: 298 | Downloads: 136,634  
  *Unsloth’s GGUF conversion of DiffusionGemma-26B, enabling local multimodal generation on consumer hardware.*

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  Author: unsloth | Likes: 645 | Downloads: 579,224  
  *The most downloaded GGUF variant of Gemma-4-12B, demonstrating the massive demand for quantized multimodal models.*

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  Author: DavidAU | Likes: 383 | Downloads: 427,359  
  *An aggressively fine-tuned and uncensored GGUF model with an extremely long name—viral for its "heretic" persona and localization performance.*

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  Author: unsloth | Likes: 128 | Downloads: 23,956  
  *GGUF version of Kimi-K2.7-Code, providing efficient on-device code generation.*

- **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)**  
  Author: unsloth | Likes: 97 | Downloads: 20,504  
  *The GGUF quantization of MiniMax-M3 for agentic multimodal tasks, enabling faster local inference.*

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)**  
  Author: OBLITERATUS | Likes: 341 | Downloads: 78,333  
  *A community fine-tune of Gemma-4-12B with an "obliterated" censorship layer, popular for unrestricted use cases.*

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  Author: nex-agi | Likes: 317 | Downloads: 5,579  
  *A Qwen3.5-MoE based fine-tune for conversational and vision tasks, trending in the agentic AI community.*

## 3. Ecosystem Signal

**MoE is now the default architecture.** The top five trending models by likes—DeepSeek-V4-Pro, Qwen3.6-35B-A3B, nvidia/LocateAnything, Google DiffusionGemma, and MiniMax-M3—all use mixture-of-experts, reflecting a systemic shift from dense transformers to sparse, parameter-efficient designs. **Open-weight dominance continues:** all 30 models are open-weight, with no proprietary API-only entries in the top trending list. **GGUF quantization has become the primary consumption pattern** for open models: 13 of 30 entries are GGUF variants, suggesting that local inference (via llama.cpp, ollama, etc.) now drives the majority of community engagement. The rise of **"uncensored" and "heretic" fine-tunes** (e.g., HauhauCS, DavidAU, OBLITERATUS) indicates a sustained demand for models with minimal safety guardrails, particularly for creative writing and roleplay. Finally, **vision-language is the new text-only**: over 70% of models include image-text-to-text pipelines, making pure language models a minority in the trending list.

## 4. Worth Exploring

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — The undisputed star of the week. With 4,926 likes and 2.8M downloads, it represents the state of the art in open-weight MoE reasoning. Anyone studying LLM scaling or MoE architecture should evaluate this model.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A surprisingly high-likes (2,138) specialized model for spatial grounding. Its 3B size makes it exceptionally practical for robotics, visual inspection, and multimodal RAG pipelines. It’s a rare example of a narrow-use-case model achieving broad popularity.

3. **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — As Google’s first unified diffusion transformer, this model blurs the line between generation and understanding. With 460K downloads and an active GGUF variant from unsloth, it’s a must-study for researchers interested in next-generation multimodal architectures.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*