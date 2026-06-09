# Hugging Face Trending Models Digest 2026-06-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-09 01:52 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for **2026-06-09**.

---

## 1. Today's Highlights

This week’s trending models are defined by a surge in unified, any-to-any architectures, headlined by Google’s **Gemma-4** family and NVIDIA’s **LocateAnything** and **Nemotron-3 Ultra** lines. **DeepSeek-V4-Pro** and **-Flash** continue their dominant run, holding top positions by both likes (4,722) and downloads (5.4M). The community is heavily embracing quantization, with unsloth delivering multiple GGUF variants of flagship models like Gemma-4 and Qwen3.6. Meanwhile, new specialized entrants in video generation (**SulphurAI/Sulphur-2-base**) and enterprise TTS (**bosonai/higgs-audio**) signal growing maturity in production-ready generative AI.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | 4,722 likes | 5.4M downloads  
  The top-trending LLM this week, a powerful conversational model that sets new standards for open-weight performance.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* | 1,448 likes | 3.3M downloads  
  A faster, more efficient variant of V4-Pro, optimized for production inference without sacrificing quality.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — *sapientinc* | 728 likes | 164K downloads  
  A compact 1B text-generation model designed for human resource management tasks, trending for its niche enterprise utility.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — *LiquidAI* | 549 likes | 135K downloads  
  A MoE language model (8B total, 1B active) from Liquid AI, gaining traction for efficient inference and strong reasoning.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — *JetBrains* | 260 likes | 17.4K downloads  
  A conversational MoE model with explicit “thinking” capability, reflecting JetBrains’ push into AI-assisted coding.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — *nex-agi* | 121 likes | 716 downloads  
  A MoE text-generation model based on Qwen3.5, in early adoption for multimodal chat applications.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 1,621 likes | 122K downloads  
  A 3B image-text-to-text model for visual grounding and object localization, trending for its broad feature extraction utility.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — *ideogram-ai* | 393 likes | 5.5K downloads  
  FP8 quantized version of Ideogram’s latest text-to-image model, enabling high-quality generation on consumer hardware.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — *stepfun-ai* | 352 likes | 45.5K downloads  
  A vision-language model optimized for speed, attracting users needing rapid multimodal inference.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | 290 likes | 4K downloads  
  A compact streaming ASR model (0.6B parameters), notable for real-time speech recognition with cache-aware architecture.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — *ByteDance* | 185 likes | 278 downloads  
  An image-text-to-video generation model from ByteDance, based on the arXiv paper 2605.22344, exploring novel video synthesis pipelines.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — *google* | 151 likes | 17.5K downloads  
  Google’s latest real-time text-to-audio model (TFLite), pushing interactive music and sound generation forward.

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — *nvidia* | 206 likes | 34K downloads  
  NVIDIA’s small “omni” generation model for video and graphics, suggesting a trend toward unified 3D/content pipelines.

- **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** — *jdopensource* | 103 likes | 4K downloads  
  A text-to-video model with integrated audio-video generation, reflecting growing demand for full multi-track synthesis.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* | 1,601 likes | 1.7M downloads  
  A community fine-tune on Lightricks/LTX-2.3 for text-to-video, with a 1.7M download count, signaling massive interest in open video models.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — *PaddlePaddle* | 277 likes | 9.9K downloads  
  An OCR vision-language model based on ERNIE 4.5, trending for robust document and scene text recognition.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | 1,554 likes | 3M downloads  
  A community MoE fine-tune of Qwen3.6 designed for uncensored and aggressive roleplay; massively downloaded for niche use cases.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — *bosonai* | 248 likes | 15K downloads  
  A 4B text-to-speech model built on Qwen3, representing a new wave of high-quality, transformer-based TTS systems.

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — *MisoLabs* | 156 likes | 0 downloads  
  A fresh text-to-speech model with a day-zero release; monitoring for adoption after initial buzz.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — *unsloth* | 503 likes | 645K downloads  
  The go-to GGUF quantization of Google’s Gemma-4-12B, making the any-to-any model accessible on consumer GPUs.

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — *unsloth* | 147 likes | 121K downloads  
  Quantization-aware training variant of Gemma-4, optimized for better accuracy at lower precision.

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — *google* | 99 likes | 52K downloads  
  Official Google QAT quant (q4_0) for Gemma-4, indicating growing first-party support for edge deployment.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* | 696 likes | 1.2M downloads  
  A GGUF of Qwen3.6’s 27B model with multi-token prediction, mixing efficiency and future-generation capabilities.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — *nvidia* | 167 likes | 55.9K downloads  
  NVIDIA’s flagship 550B/55B-active MoE model; trending as the largest open-weight MoE officially released.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — *nvidia* | 145 likes | 66.2K downloads  
  NVFP4 (4-bit floating point) quantized version of the same giant model, enabling deployment on fewer GPUs.

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — *unsloth* | 103 likes | 87K downloads  
  QAT-GGUF for the larger Gemma-4-26B variant, extending quantization coverage to mid-size MoE.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — *ideogram-ai* | 262 likes | 5K downloads  
  NF4 quantized version of Ideogram-4, complementing the FP8 release with an alternative precision format.

---

## 3. Ecosystem Signal

Several clear trends define this snapshot. **MoE (Mixture of Experts)** has become the dominant architecture among trending models: from NVIDIA’s Nemotron-3 Ultra (550B-A55B) to LiquidAI’s LFM2.5 and JetBrains’ Mellum2, all leverage sparse activation to scale reasoning while controlling compute. **DeepSeek-V4** remains the unchallenged leader in open-weight LLMs, with both full and flash variants accumulating millions of downloads.

**Quantization activity is at an all-time high.** Unsloth continues to be the community’s preferred quantization partner, covering Gemma-4, Qwen3.6, and other flagship models in GGUF format. Notably, **Google and NVIDIA are now releasing official QAT quantized versions** of their own models (Gemma-4 QAT, NVFP4), signaling a shift where first-party support for on-device deployment becomes a standard expectation.

In **multimodal generation**, video models are rapidly climbing: Sulphur-2-base (1.7M downloads) and ByteDance’s Bernini-R reflect growing confidence in open video synthesis. **Any-to-any models** (Gemma-4, NVIDIA Cosmos3) are the new frontier, bridging text, image, video, and audio within unified transformers.

Overall, the ecosystem is maturing from single-purpose models to **scalable, quantized, and multimodal MoE architectures**—with open-weight releases increasingly matching or exceeding proprietary alternatives in adoption.

---

## 4. Worth Exploring

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — The highest-liked and most-downloaded model this week. It represents the current ceiling of open-weight LLM performance. Ideal for anyone evaluating state-of-the-art conversational AI or building production applications.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A breakout model in visual grounding. Its compact 3B size relative to its localization capabilities makes it highly practical for robotics, VQA, and image analysis pipelines.

3. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — With 1.7M downloads in its first trending week, this is the hottest open video generation model. Studying its fine-tune pipeline (based on Lightricks/LTX-2.3) offers insights into community-driven video AI breakthroughs.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*