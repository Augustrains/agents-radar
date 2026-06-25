# Hugging Face Trending Models Digest 2026-06-25

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-25 02:00 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-06-25**.

---

## 1. Today's Highlights

This week’s trending models reveal a clear shift toward **efficiency and specialization**. The top spot belongs to **DeepSeek-V4-Pro** (5,048 likes), signaling sustained community enthusiasm for high-performance, open-weight reasoning models. Meanwhile, **GLM-5.2** (#1) and its quantized variants continue to gain traction, reflecting a strong appetite for MoE (Mixture-of-Experts) architectures. On the multimodal front, **Google's Gemma-4-12B-it** (any-to-any pipeline) and **MiniMax-M3** are leading a wave of general-purpose vision-language models. Quantization also remains a dominant theme, with GGUF variants of Gemma-4-12B and GLM-5.2 amassing hundreds of thousands of downloads each.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | ⭐ 5,048 | ⬇️ 2,052,463  
  Latest flagship from DeepSeek; dominant conversational LLM with massive community traction.
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | ⭐ 2,358 | ⬇️ 57,186  
  MoE-based generation model from Zhipu AI, trending for its efficient sparse activation (GLM_MoE_DSA).
- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — zai-org | ⭐ 158 | ⬇️ 445,304  
  FP8 quantized version of GLM-5.2; highly downloaded for reduced inference cost.
- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen | ⭐ 150 | ⬇️ 223  
  MoE agentic LLM (35B total, 3B active) optimized for tool-use and environment interaction.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google | ⭐ 1,163 | ⬇️ 2,114,441  
  Google’s **any-to-any** unified model (text, image, audio); top-3 by downloads and a major multimodal milestone.
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | ⭐ 738 | ⬇️ 45,687  
  Industrial-strength OCR model with image-text-to-text pipeline; trending for document AI applications.
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | ⭐ 2,347 | ⬇️ 359,498  
  Nvidia’s visual grounding model for object localization; high likes indicate strong interest in spatial AI.
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | ⭐ 1,228 | ⬇️ 143,093  
  Multimodal VL model (MiniMax_M3_VL) with strong vision-language performance; popular for general-purpose use.
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | ⭐ 190 | ⬇️ 878  
  Text-to-image diffusion model; turbo variant for faster generation.
- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — krea | ⭐ 160 | ⬇️ 1,205  
  Base model for Krea-2-Turbo; raw diffusion weights for customization.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | ⭐ 678 | ⬇️ 47,208  
  Lightweight streaming ASR model (0.6B); trending for real-time speech recognition deployment.
- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — owensong | ⭐ 193 | ⬇️ 0  
  Ultra-small TTS model; notable for extreme compression (nano-scale) in speech synthesis.
- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** — Boogu | ⭐ 121 | ⬇️ 743  
  Image editing diffusion model; bilingual (EN/ZH) pipeline.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | ⭐ 2,209 | ⬇️ 3,769,369  
  Uncensored MoE vision-language model (Qwen3.6); extremely high downloads for a fine-tune.
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | ⭐ 984 | ⬇️ 480,013  
  Code-focused multimodal model from Moonshot AI; high downloads for code-vision tasks.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | ⭐ 314 | ⬇️ 5,123  
  Image-text-to-text reasoning model (Qwen3.5); trending for its Claude-Mythos synthetic fine-tuning recipe.
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | ⭐ 354 | ⬇️ 63,637  
  GGUF quantized version of the above; more popular than the original due to ease of local inference.
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | ⭐ 336 | ⬇️ 4,805  
  Microsoft’s efficient long-context model (4B); fine-tuned for retrieval-augmented generation.
- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** — LiquidAI | ⭐ 119 | ⬇️ 11,471  
  Sentence-embedding model (350M); leading spike in embedding model interest.
- **[LiquidAI/LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)** — LiquidAI | ⭐ 88 | ⬇️ 3,362  
  ColBERT variant of LiquidAI’s embedding model; specialized for late-interaction retrieval.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | ⭐ 2,301 | ⬇️ 483,139  
  GGUF quant of a Gemma-4-12B coding fine-tune; highest-download GGUF this week.
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | ⭐ 534 | ⬇️ 138,704  
  Agentic variant of the Gemma-4 coding GGUF; optimized for terminal/tool-use.
- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** — huihui-ai | ⭐ 124 | ⬇️ 4,402  
  "Abliterated" (uncensored) fine-tune of the Gemma-4-12B coder; community-driven alignment removal.
- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** — Jackrong | ⭐ 83 | ⬇️ 10,867  
  GGUF of a Qwen3.6-based coding model; "MTP" indicates multi-turn planning adaptation.
- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — lordx64 | ⭐ 180 | ⬇️ 5,719  
  Community fine-tune of Qwen3.5 MoE for vision-language tasks.
- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | ⭐ 692 | ⬇️ 49,569  
  Small (3B) math & reasoning model; trending for beating larger models on benchmarks.

## 3. Ecosystem Signal

**Model family momentum**: The **Gemma-4** family (Google) is currently the most fine-tuned and quantized lineage, with multiple GGUF variants and "abliterated" versions dominating the #3–#5 spots. **GLM-5.2** (Zhipu AI) and **DeepSeek-V4** are also strong, but Gemma-4 has the widest ecosystem support. **Qwen3.6** and **Qwen3.5** continue to see active community fine-tuning (uncensored, coding, vision).

**Open-weight vs proprietary**: The majority of trending models are open-weight (Apache-2.0 or permissive). DeepSeek-V4-Pro, Google Gemma, and GLM-5.2 are all openly available, reflecting a mature open-weight era. Proprietary pipelines are rare — only Baidu’s Unlimited-OCR and Nvidia’s Nemotron ASR stand out.

**Quantization & fine-tuning**: GGUF is the dominant quantization format, especially for coding and agentic use cases. Community activity is heavily concentrated on "uncensoring" (abliteration) and performance tuning for local inference. The popularity of 3B–12B models suggests a sweet spot for local deployment.

**Emerging categories**: Embedding models (LiquidAI LFM2.5), streaming ASR (Nvidia Nemotron), and ultra-small TTS (Inflect-Nano) indicate growing interest in non-LLM, edge-friendly model types.

## 4. Worth Exploring

1. **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — This is the most versatile open-weight model this week, supporting any-to-any modality (text, image, audio). Its 2M+ downloads and strong fine-tune ecosystem make it essential for multimodal prototyping.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2,347 likes and nearly 360k downloads, this visual grounding model is a standout for spatial AI tasks (object detection, segmentation, visual QA). Its compact 3B size is ideal for deployment.

3. **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — A 3B model that punches above its weight in math and reasoning. Perfect for studying small-model distillation techniques or building low-resource reasoning agents.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*