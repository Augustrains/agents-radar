# Hugging Face Trending Models Digest 2026-07-24

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-24 01:21 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-24**.

---

## 1. Today's Highlights

The Hugging Face ecosystem this week is defined by a major convergence of **extreme quantization** and **frontier multimodal capabilities**. The **GLM-5.2** model from zai-org leads in weekly likes, signaling strong interest in Mixture-of-Experts architectures that rival larger dense models. The **Qwen3.6** family dominates community fine-tuning, with multiple uncensored and vision-aligned variants appearing across the top 30. Meanwhile, **Google’s Gemma-4-31B-it** continues its reign in total downloads, while **Terry Bonsai (1-bit/2-bit)** models from prism-ml demonstrate that the ultra-low-bit quantization trend is not slowing down. On the application side, we see strong growth in **OCR** (Baidu Unlimited-OCR), **speech recognition** (Nvidia Nemotron-3.5), and **robotics** (MiniCPM-RobotManip), suggesting a broadening of the HF model marketplace beyond pure text generation.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* | Likes: 4,370 | Downloads: 596,442  
  A MoE-driven conversational LLM with strong reasoning capabilities, trending for its efficient parameter usage and high-quality Chinese-English performance.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — *upstage* | Likes: 445 | Downloads: 362  
  A massive 250B dense model from Upstage, likely the largest open-weight release this week, attracting attention for its scale and Korean-optimized training.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — *Nanbeige* | Likes: 320 | Downloads: 4,532  
  A compact 3B parameter LLM from Nanbeige, trending for its efficiency in Chinese-language tasks and small footprint.

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — *Motif-Technologies* | Likes: 173 | Downloads: 1,856  
  A feature-extraction oriented model from Motif, gaining traction for enterprise retrieval and embeddings use cases.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* | Likes: 2,885 | Downloads: 2,414,259  
  A state-of-the-art OCR engine that handles unlimited-length documents, trending for Baidu’s scale and production-grade accuracy.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — *thinkingmachines* | Likes: 1,508 | Downloads: 24,669  
  A conversational image-text-to-text model optimized for visual Q&A, trending as a strong competitor to proprietary multimodal assistants.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — *google* | Likes: 3,347 | Downloads: 12,666,488  
  Google’s flagship open multimodal LLM, trending due to exceptional visual reasoning and massive download volume reflecting production adoption.

- **[Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)** — *Qwen* | Likes: 1,798 | Downloads: 2,497,020  
  A custom voice TTS model supporting 12Hz output, trending for high-quality voice cloning and permissive licensing (Apache 2.0).

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — *microsoft* | Likes: 183 | Downloads: 411  
  A text-to-image diffusion model from Microsoft, trending for its workflow-oriented image editing and generation pipeline.

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — *nvidia* | Likes: 99 | Downloads: 28,493  
  Nvidia’s latest Cosmos3 variant optimized for edge deployment, gaining interest for real-time video diffusion on low-power devices.

### 🔧 Specialized Models (code, math, medical, embeddings)
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — *moonshotai* | Likes: 1,248 | Downloads: 766,522  
  A code-focused multimodal model leveraging compressed tensors, trending for its high performance on coding benchmarks and efficient storage.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — *fdtn-ai* | Likes: 121 | Downloads: 2,747  
  A 1B parameter security-oriented LLM using GraniteMoEHybrid, trending for its focus on safe and secure text generation.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* | Likes: 926 | Downloads: 750,118  
  A streaming ASR model with only 0.6B parameters, trending for real-time speech recognition at low latency.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — *OpenMOSS-Team* | Likes: 320 | Downloads: 111,598  
  An audio-text-to-text model combining transcription and speaker diarization, trending for meeting and call analysis workflows.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — *ATH-MaaS* | Likes: 257 | Downloads: 26,919  
  A Qwen3.5-based OCR model for document understanding, trending as a lightweight alternative to Baidu’s offering.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — *prism-ml* | Likes: 983 | Downloads: 576,083  
  A 2-bit ternary quantized 27B model, trending for its extreme compression that retains surprising quality for local inference.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — *prism-ml* | Likes: 620 | Downloads: 1,910,116  
  The 1-bit sibling of Ternary-Bonsai, trending as the most downloaded GGUF file this week, demonstrating the demand for tiny local LLMs.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | Likes: 3,033 | Downloads: 2,027,080  
  An uncensored, vision-capable MoE fine-tune of Qwen3.6, trending for its aggressive uncensoring and high-throughput MoE architecture.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* | Likes: 2,438 | Downloads: 2,126,755  
  A Qwen3.5-based GGUF distilled to mimic Claude-style reasoning, trending for its small size and strong reasoning benchmarks.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — *DavidAU* | Likes: 397 | Downloads: 334,847  
  An extremely fine-tuned and uncensored 27B GGUF, trending in the “uncensored” niche for story generation and roleplay.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** — *LuffyTheFox* | Likes: 117 | Downloads: 24,982  
  Another Qwen3.6 MoE uncensored variant branded with Hermes lineage, trending for community trust in the Hermes fine-tuning recipe.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — *bottlecapai* | Likes: 528 | Downloads: 25,231  
  A Qwen3.6 fine-tune for “chain-of-thought” reasoning, trending for adding structured thinking to the popular Qwen base.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) & [unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF) & [poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4) & [poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** — *poolside / unsloth* | Likes: 514–112 | Downloads: 13,285–52,235  
  A family of code-generation models from poolside, trending due to multiple quantization paths (GGUF, NVFP4) and strong developer interest in code assistance.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — *prism-ml* | Likes: 172 | Downloads: 34,270  
  An Apple MLX-compatible 1-bit quant of Bonsai, trending for enabling 27B model inference on Mac hardware.

## 3. Ecosystem Signal

**Model Families Gaining Momentum:** The **Qwen3.6** family is the most vibrant ecosystem this week, appearing in multiple fine-tunes and quantizations (uncensored, MoE, vision, code). The **Laguna** series from poolside shows strong corporate and community quantization activity, suggesting a rising star in code LLMs. The **Bonsai/Ternary-Bonsai** series from prism-ml signals that ultra-low-bit (1-bit / 2-bit) models are entering the mainstream, driven by consumer hardware constraints.

**Open-Weight vs Proprietary Trends:** Open-weight models continue to dominate the leaderboard, but we see a new pattern: **corporate open-weight releases with multiple official quantizations** (e.g., Laguna, Gemma-4, Cosmos3-Edge). This blurs the line between “community fine-tune” and “official release,” as companies like poolside and Nvidia ship GGUF, NVFP4, and MLX variants directly.

**Quantization & Fine-Tuning Activity:** The top 30 is saturated with GGUF variants (9 out of 30). The “uncensored” niche remains a persistent community driver, with Qwen3.6 being the primary base. Notably, **MoE fine-tuning** is accelerating—both HauhauCS and LuffyTheFox are releasing MoE variants of Qwen3.6, indicating that fine-tuners are now comfortable targeting sparse architectures.

## 4. Worth Exploring

1. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — As the most extreme quantization in the top 10, this model is a must-study for anyone interested in **edge deployment, local inference, or ternary weight research**. Its high downloads despite 2-bit precision suggests it retains surprising quality.

2. **[Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)** — With Apache 2.0 licensing and huge download numbers, this is the top **open-source TTS model to clone**. It’s perfect for building custom voice applications without vendor lock-in.

3. **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — This is a **vision-language-action model for robotics**, a rapidly emerging category. It’s worth studying to understand how VLAs are being trained for real-world manipulation tasks, especially for researchers working in embodied AI.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*