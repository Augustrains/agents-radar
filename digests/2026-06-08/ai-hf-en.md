# Hugging Face Trending Models Digest 2026-06-08

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-08 02:15 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-08

## 1. Today's Highlights

**DeepSeek** dominates the leaderboard with its **V4-Pro** and **V4-Flash** models collectively amassing over 8.8 million downloads and 6,100+ weekly likes, signaling a major shift in the open-weight LLM landscape. **NVIDIA** continues its aggressive multi-model strategy with five entries spanning vision-language (LocateAnything-3B), speech (Nemotron ASR), and their massive **Nemotron-3 Ultra 550B** alongside the new **Cosmos3** generation family. **Google's Gemma-4** lineup, including both the 12B instruct and base variants, along with community quantizations from **Unsloth**, indicates strong demand for accessible multimodal models. Meanwhile, **SulphurAI's** text-to-video model and **Ideogram-4** highlight growing momentum in generative media, while **Qwen3.6** derivatives from both NVIDIA and Unsloth continue to build significant download velocity.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | 4,697 likes | 5.5M downloads  
  The flagship open-weight LLM with massive adoption, offering state-of-the-art conversational performance and driving the week's strongest community momentum.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* | 1,434 likes | 3.3M downloads  
  A faster, more accessible sibling to V4-Pro, balancing quality and inference speed under a permissive MIT license.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | 1,522 likes | 2.9M downloads  
  A community-uncensored MoE variant of Qwen3.6 with vision capabilities, trending for its aggressive fine-tuning and massive download count.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — *sapientinc* | 719 likes | 162K downloads  
  A compact 1B text-generation model specialized for HRM tasks, gaining traction for its efficiency in enterprise applications.

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — *openbmb* | 779 likes | 114K downloads  
  A tiny 1B Llama-based model punchings well above its weight class, popular for on-device and resource-constrained deployments.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — *JetBrains* | 250 likes | 16.9K downloads  
  A thinking-oriented MoE model optimized for conversational coding and reasoning tasks, reflecting developer tooling integration trends.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — *LiquidAI* | 541 likes | 118K downloads  
  An 8B MoE model with 1B active parameters, balancing efficiency and quality for text generation.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — *nvidia* | 157 likes | 49.8K downloads  
  NVIDIA's flagship 550B-parameter MoE model with 55B active parameters — a massive foundation model for enterprise-scale deployment.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — *nvidia* | 132 likes | 39.9K downloads  
  The NVFP4 quantized variant of Nemotron-3 Ultra, offering extreme compression while preserving quality for efficient serving.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — *nvidia* | 200 likes | 1.2M downloads  
  NVIDIA's NVFP4 quantized version of the Qwen3.6 MoE model, combining community architecture with enterprise-level optimization.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 1,530 likes | 115K downloads  
  **#1 trending overall**: A 3B feature-extraction model for referring expression comprehension and visual grounding, with broad vision-language applicability.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — *google* | 692 likes | 434K downloads  
  Google's unified any-to-any multimodal model balancing strong vision-language capabilities with an accessible 12B size.

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — *unsloth* | 455 likes | 568K downloads  
  The community GGUF quantization making Google's Gemma-4 accessible for CPU and edge deployment.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — *google* | 412 likes | 99.7K downloads  
  The base (non-instruct) variant of Gemma-4, providing a foundation for further fine-tuning across any-to-any tasks.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — *ideogram-ai* | 351 likes | 4.4K downloads  
  The FP8 version of Ideogram-4, a diffusion-based text-to-image model offering efficient high-quality generation.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — *ideogram-ai* | 235 likes | 3.8K downloads  
  An even more compressed NF4 quantization of Ideogram-4, enabling wider deployment of image generation.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — *stepfun-ai* | 348 likes | 43.2K downloads  
  A vision-language model optimized for efficiency, trending for its strong multimodal reasoning at reduced compute.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — *ByteDance* | 168 likes | 246 downloads  
  An image-text-to-video generation model with Apache-2.0 licensing, representing emerging video synthesis capabilities.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* | 1,587 likes | 1.7M downloads  
  A text-to-video model based on Lightricks/LTX-2.3 with both full-precision and GGUF variants, rapidly adopted by the video generation community.

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — *nvidia* | 195 likes | 29.7K downloads  
  The smallest entry in NVIDIA's Cosmos3 omnimodal family, enabling efficient multimodal generation.

- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — *nvidia* | 153 likes | 24K downloads  
  A larger Cosmos3 variant for higher-quality multimodal generation across multiple modalities.

- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** — *nvidia* | 124 likes | 5.1K downloads  
  Text-to-image specialization within the Cosmos3 family, offering targeted generative capabilities.

- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** — *nvidia* | 115 likes | 4.5K downloads  
  Image-to-video variant of Cosmos3, extending the family's reach into video generation.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — *google* | 133 likes | 13.3K downloads  
  A TFLite-based text-to-audio model supporting real-time music generation, accompanied by two academic papers.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — *PaddlePaddle* | 267 likes | 9.1K downloads  
  An ERNIE4.5-powered vision-language OCR model with strong document understanding capabilities.

### 🔧 Specialized Models (speech, TTS, ASR)

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | 258 likes | 3.4K downloads  
  A cache-aware streaming ASR model using NeMo, optimized for low-latency speech recognition pipelines.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — *bosonai* | 195 likes | 7.6K downloads  
  A 4B multimodal text-to-speech model built on Qwen3 architecture, delivering high-quality voice synthesis.

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — *MisoLabs* | 143 likes | 0 downloads  
  A PyTorch-based text-to-speech model noted for speech synthesis quality, freshly released with no downloads yet.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — *unsloth* | 121 likes | 85.8K downloads  
  A QAT-enhanced GGUF quantization of Gemma-4, pushing the boundaries of compression while maintaining quality.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* | 687 likes | 1.2M downloads  
  Unsloth's GGUF quantization of Qwen3.6 with MTP support, enabling efficient deployment of this popular vision-language model.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | already listed under Language Models  
  A fine-tuned MoE variant with uncensored training and GGUF availability, demonstrating strong community interest in alignment customization.

---

## 3. Ecosystem Signal

**DeepSeek's V4 family** is the defining narrative this week — V4-Pro and V4-Flash together represent an unprecedented concentration of community attention, with download counts doubling their nearest competitors. This suggests DeepSeek has established itself as the de facto open-weight LLM leader alongside Meta's Llama lineage, though notably absent from this week's top models.

**NVIDIA's multi-pronged strategy** is equally striking: they simultaneously advance in vision-language (LocateAnything-3B), massive-scale MoE (Nemotron-3 Ultra 550B), multimodal generation (Cosmos3 family), speech recognition (Nemotron ASR), and optimized quantization (NVFP4 variants of Qwen3.6 and Nemotron). This positions NVIDIA as the most diversified model developer on the Hub, leveraging their hardware-software integration advantage.

**MoE architectures dominate** the large-scale models: DeepSeek-V4, Nemotron-3 Ultra, Qwen3.6 variants, Mellum2, LFM2.5 — all employ Mixture-of-Experts designs. The market is clearly converging on sparse activation for compute-efficient scaling.

**Quantization is now table stakes** for widespread adoption: GGUF variants (Unsloth's Gemma-4 and Qwen3.6, Sulphur-2) and NVIDIA's proprietary NVFP4 format enable deployment across hardware tiers. Models without quantized variants see significantly lower download-to-like ratios.

**Video generation** is the breakout modality: Sulphur-2 (1.7M downloads, 1,587 likes) and Bernini-R signal that text-to-video and image-to-video are moving from research curiosity to production-ready tools.

---

## 4. Worth Exploring

**1. [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — The #1 trending model deserves close study as a benchmark for modern visual grounding. Its 3B parameter size makes it practical for real-world deployment while offering state-of-the-art referring expression comprehension. A strong candidate for robotics, UI navigation, and document AI pipelines.

**2. [SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — With 1.7M downloads in its first week, this text-to-video model is the dark horse of this digest. Based on Lightricks/LTX-2.3 but with community optimizations and both full-precision and GGUF variants, it represents how video generation is becoming accessible to individual developers. Worth trying for anyone exploring generative media.

**3. [JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — While lower in raw metrics, this "thinking" MoE model from JetBrains signals a growing trend: code-generation models specifically optimized for reasoning and multi-step problem solving. Its 12B-parameter size with only 2.5B active parameters makes it a compelling study in efficient reasoning architectures. Ideal for developers building coding assistants or evaluating thinking-model design patterns.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*