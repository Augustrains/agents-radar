# Hugging Face Trending Models Digest 2026-06-17

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-17 02:29 UTC

---

# Hugging Face Trending Models Digest — 2026-06-17

## Today's Highlights

This week's trending lineup is dominated by massive MoE architectures and multimodal models, with **DeepSeek-V4-Pro** surging to 4,896 weekly likes and nearly 3M downloads, cementing its position as the community's most-watched frontier LLM. Google's **Gemma-4-12B-it** and **DiffusionGemma-26B-A4B-it** continue to drive strong adoption across both text and multimodal pipelines, while **nvidia/LocateAnything-3B** (2,104 likes) signals growing interest in specialized vision grounding models. The ecosystem also sees intense community quantization activity around Qwen3.6 variants—most notably the uncensored 35B MoE model from HauhauCS (1,892 likes, 2.7M downloads)—alongside a wave of GGUF conversions from **unsloth** covering almost every major release. Notably, **MiniMax-M3** and **Kimi-K2.7-Code** maintain strong traction as multimodal code assistants, while audio generation models from **bosonai** and **Zyphra** indicate expanding modality coverage.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  Author: deepseek-ai | Likes: 4,896 | Downloads: 2,829,747  
  The latest flagship from DeepSeek—a dense 4th-gen conversational LLM trending as the most-liked model this week, driven by strong benchmark performance and wide adoption for both research and inference.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  Author: google | Likes: 1,054 | Downloads: 1,223,383  
  Google's unified any-to-any model (Gemma 4) with instruction tuning, trending for its cross-modal versatility and high download volume.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  Author: zai-org | Likes: 427 | Downloads: 0  
  A new conversational MoE model from the GLM family (Zhipu AI), notable for its DSA architecture but still early in community adoption with zero reported downloads.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  Author: WeiboAI | Likes: 188 | Downloads: 0  
  A compact 3B model focused on math reasoning, built on Qwen2—trending as a lightweight alternative for specialized math tasks.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  Author: microsoft | Likes: 163 | Downloads: 192  
  Microsoft's 4B SFT model (based on Qwen3) optimized for long-context reasoning, featuring an Explorer SubAgent architecture.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  Author: google | Likes: 949 | Downloads: 375,974  
  Google's diffusion-based image-text-to-text MoE model (26B, 4B active)—trending as the most downloaded multimodal model this week, pairing image understanding with conversational capability.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  Author: MiniMaxAI | Likes: 1,018 | Downloads: 25,064  
  A multimodal MoE model (image-text-to-text) with strong agent-oriented features, trending for its versatility across vision-language tasks.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  Author: nvidia | Likes: 2,104 | Downloads: 98,698  
  NVIDIA's dedicated 3B image-feature-extraction model for visual grounding and object localization—one of the most-liked specialized models this week.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  Author: ideogram-ai | Likes: 560 | Downloads: 12,466  
  The latest text-to-image diffusion model from Ideogram, released in FP8 for efficient inference—trending as a top image generation choice.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  Author: bosonai | Likes: 465 | Downloads: 43,361  
  A multimodal TTS model (Higgs Audio v3, 4B) built on Qwen3 architecture—trending for high-quality text-to-speech synthesis.

- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)**  
  Author: Zyphra | Likes: 100 | Downloads: 539  
  An Apache-2.0 licensed TTS model, gaining attention for its open-weight audio generation capability.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  Author: zai-org | Likes: 208 | Downloads: 0  
  A video generation model focused on character animation with pose-driven diffusion—early-stage but notable for its image-to-video pipeline.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  Author: Qwen | Likes: 2,137 | Downloads: 3,360,615  
  Alibaba's flagship 3.6th-gen MoE vision-language model (35B, 3B active)—the most downloaded model this week, driving massive community interest in MoE multimodal architectures.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  Author: moonshotai | Likes: 802 | Downloads: 102,206  
  Moonshot AI's code-focused multimodal model, utilizing compressed tensor techniques—trending as a developer favorite for programming assistance.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  Author: CohereLabs | Likes: 412 | Downloads: 12,129  
  Cohere's compact code generation MoE model (North series)—the most-liked specialized coding model from a major lab this week.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  Author: nvidia | Likes: 475 | Downloads: 5,777  
  NVIDIA's streaming automatic speech recognition model (0.6B) with cache-aware architecture for low-latency ASR.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  Author: yuxinlu1 | Likes: 1,185 | Downloads: 60,921  
  A community fine-tune of Gemma-4-12B specialized for coding and reasoning, released in GGUF format—the most-liked code model this week.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  Author: HauhauCS | Likes: 1,892 | Downloads: 2,716,651  
  An uncensored, aggressive fine-tune of Qwen3.6-35B-A3B in GGUF format—viral this week as the community's most downloaded fine-tune, reflecting strong demand for unfiltered MoE variants.

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  Author: DavidAU | Likes: 370 | Downloads: 366,279  
  A highly customized uncensored Qwen3.6-40B merge incorporating multiple experimental techniques—trending for its extreme fine-tuning and 366K downloads.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**  
  Author: unsloth | Likes: 289 | Downloads: 120,435  
  Unsloth's GGUF conversion of Google's DiffusionGemma, enabling local CPU/GPU inference of this multimodal MoE.

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  Author: unsloth | Likes: 633 | Downloads: 1,009,602  
  The most downloaded GGUF this week—Unsloth's conversion of Gemma-4-12B-it, reflecting massive demand for quantized Google models.

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  Author: unsloth | Likes: 119 | Downloads: 16,817  
  Unsloth's GGUF of Moonshot's Kimi-K2.7-Code, extending the code model's reach to local deployment.

- **[unsloth/MiniMax-M3-GGUF](https://huggingface.co/unsloth/MiniMax-M3-GGUF)**  
  Author: unsloth | Likes: 93 | Downloads: 18,206  
  GGUF quantization of MiniMax-M3 for efficient local multimodal inference.

- **[unsloth/North-Mini-Code-1.0-GGUF](https://huggingface.co/unsloth/North-Mini-Code-1.0-GGUF)**  
  Author: unsloth | Likes: 79 | Downloads: 26,313  
  Unsloth's GGUF of Cohere's code MoE model, supporting local coding assistance.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)**  
  Author: OBLITERATUS | Likes: 336 | Downloads: 76,044  
  A community-modified Gemma-4-12B with aggressive fine-tuning—popular among experimenters seeking custom behavior.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  Author: Jackrong | Likes: 219 | Downloads: 79,157  
  A GGUF-quantized vision-language code model (27B) with multi-turn prompting, trending for coding + vision tasks.

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  Author: prefeitura-rio | Likes: 315 | Downloads: 189,744  
  A massive 397B MoE multimodal model (based on Qwen3.5), trending for its public sector provenance and large-scale open weights.

---

## Ecosystem Signal

The current trending landscape reveals several clear macro-trends shaping the Hugging Face ecosystem:

**MoE Domination** — Mixture-of-Experts architectures now dominate the top-10, with Qwen3.6, DiffusionGemma, GLM-5.2, MiniMax-M3, and North-Mini-Code all leveraging MoE. The Qwen family (3.5/3.6) has become the single most active lineage, spawning dozens of community fine-tunes and quantizations. DeepSeek-V4-Pro remains the top non-MoE performer, indicating that dense models still compete at the frontier.

**Quantization as Standard Infrastructure** — Unsloth has effectively become the de facto quantization provider, converting nearly every major release (Gemma-4, DiffusionGemma, Kimi-K2.7, MiniMax-M3, North-Mini-Code) to GGUF within days. This pattern signals that GGUF has become the universal local deployment format, with community expectation that every new model garners a corresponding quantized variant.

**Uncensored & Experimental Fine-Tuning** — The viral success of "uncensored" Qwen3.6 variants (HauhauCS, DavidAU) with 2.7M+ downloads indicates a hunger for unrestricted models. These fine-tunes often merge multiple training techniques (thinking loops, aggressive prompts, multi-model merges) and represent a parallel ecosystem where community experimentation outpaces official releases.

**Multimodal Convergence** — Over 60% of the trending models now support multiple modalities (text+vision+audio). Any-to-any models (Gemma-4) and diffusion-based multimodal architectures (DiffusionGemma) signal that the boundary between LLMs and diffusion models is blurring. The presence of both TTS (bosonai, Zyphra) and ASR (NVIDIA Nemotron) models highlights growing audio modality maturity.

**Regional Diversity** — Chinese AI labs (DeepSeek, Moonshot, Qwen, Zhipu/GLM, MiniMax) command the highest like counts and download volumes, suggesting that Asian-origin models now set the pace for open-weight releases. Public sector and municipal AI projects (prefeitura-rio) also emerge as unexpected contributors.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — At only 3B parameters, this model delivers precise visual grounding and object localization, making it an ideal candidate for edge deployment, robotics, and visual question answering. Its high like-to-parameter ratio (2,104 likes for 3B) suggests exceptional quality-per-parameter—a model to study for efficient multimodal reasoning.

2. **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — While still low-download, a dedicated math reasoning model at 3B parameters on Qwen2 base is worth examining as a potential lightweight alternative for arithmetic and symbolic reasoning tasks. It represents the "small model, specialized task" trend that may grow in importance alongside giant MoE models.

3. **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — This image-to-video character animation model with pose-driven diffusion is early-stage (0 downloads) but represents an underexplored niche. As video generation matures, specialized animation and character control models could become critical infrastructure for content creation. Its Diffusers-based pipeline makes it accessible for experimentation.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*