# Hugging Face Trending Models Digest 2026-07-16

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-16 01:19 UTC

---

Here is the structured Hugging Face Trending Models Digest for July 16, 2026.

## 1. Today's Highlights

This week's trending models reveal a clear surge in **MoE (Mixture-of-Experts)** architectures and **quantized multimodal** models, with the community prioritizing efficiency, reasoning, and OCR capabilities. **Tencent's Hy3** and **GLM-5.2** are emerging as the dominant new open-weight LLM families, seeing rapid fine-tuning and quantization activity. Notably, there is strong demand for **vision-language models (VLMs)** that combine reading and reasoning, as seen with **Unlimited-OCR** and **OvisOCR2**, while **1-bit and ternary (2-bit) quantization** experiments are drawing significant community interest, led by prism-ml's **Bonsai** and **Ternary-Bonsai** models.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,998 likes | 489,611 downloads  
  The most popular native-format open-weight release this week; a large MoE model trained by Zhipu AI that has quickly become a base for community finetunes and quantizations.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 800 likes | 10,406 downloads  
  Tencent's newest flagship text-generation model, driving a wave of derivative GGUF and MoE variants across the ecosystem.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 893 likes | 1,533,354 downloads  
  A highly downloaded 35B GGUF quantization likely stemming from a strong base model, indicating demand for large, locally-runnable models.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,198 likes | 468,629 downloads  
  An agentic and coding-focused fine-tune of Gemma 4, signaling the growing trend of terminal/agent-ready GGUF formats.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 554 likes | 30,539 downloads  
  A Qwen3.5-based MoE model optimized for agentic tasks, showing the integration of MoE with tool-use and decision-making.

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** — nvidia | 156 likes | 1,332 downloads  
  NVIDIA’s entry in the MoE space; a 30B model with only 3B active parameters (A3B), prioritizing inference efficiency.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,214 likes | 2,006,265 downloads  
  The most downloaded model on the list; a GGUF quantized multimodal vision-language model with a massive context window (1M tokens), ideal for long-document VQA.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,760 likes | 2,443,871 downloads  
  A highly popular uncensored vision-language fine-tune on a 35B MoE base with 3B active parameters, dominating downloads.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,002 likes | 1,715,301 downloads  
  A state-of-the-art OCR model from Baidu that treats document reading as an image-text-to-text task, trending for its practical utility.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — unsloth | 208 likes | 1,599,150 downloads  
  A 4-bit NVFP4-quantized vision-language model using Unsloth’s memory-efficient techniques, enabling high-end VLMs on consumer hardware.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 215 likes | 65,109 downloads  
  An audio-text-to-text model combining transcription with speaker diarization, a niche but growing capability for meeting and media analysis.

### 🔧 Specialized Models (code, math, medical, embeddings, tools)

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | 236 likes | 571 downloads  
  A Jax-based model designed for advanced function-calling and tool-use, distinctive for its infrastructure rather than parameter count.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 917 likes | 0 downloads  
  A utility model providing corrected Jinja chat templates for Qwen models, reflecting the community's need for reliable deployment tooling.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 467 likes | 23 downloads  
  A 2-bit ternary quantization of a 27B model using llama.cpp, pushing extreme compression boundaries for local inference.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | 110 likes | 2,188 downloads  
  An int4 CPU-friendly quantization of GLM-5.2 using "expert-streaming" for Mixture-of-Experts models, enabling efficient CPU inference.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | 107 likes | 0 downloads  
  The first community GGUF conversion of Tencent's Hy3, laying the groundwork for wider adoption of the model.

## 3. Ecosystem Signal

**MoE is the dominant architecture.** With models like GLM-5.2, Qwen3.6-35B-A3B, Hy3, NVIDIA’s Audex, and InternScience’s Agents-A1 all leveraging Mixture-of-Experts, the ecosystem has decisively shifted from dense models to sparse, parameter-efficient architectures. This unlocks larger effective model sizes without proportional compute costs, especially for local inference.

**Quantization is accelerating multimodal deployment.** The top three most downloaded models are all quantized (GGUF or NVFP4) multimodal models. Users are prioritizing the ability to process images, text, and audio on local hardware without sacrificing quality. The appearance of **1-bit and ternary quantization** (prism-ml) suggests the community is preparing for extreme compression use-cases like edge devices or real-time streaming.

**Open-weight momentum continues, but derivative work dominates.** While base models from Tencent, Zhipu AI, and NVIDIA are present, the highest engagement metrics (likes and downloads) go to community quantizations and fine-tunes. This signals a mature ecosystem where value is captured at the post-training and optimization layer, not just at the foundation model level.

## 4. Worth Exploring

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — As the most popular native-format release with extremely high likes, it's the likely base for many future fine-tunes. Exploring its MoE-DSA architecture is key to understanding the next generation of Chinese-industry LLMs.
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — With over 2 million downloads, this model’s blend of 9B size, 1M context window, and GGUF quantization represents the sweet spot for running advanced reasoning and long-context VLMs on consumer GPUs.
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — This 2-bit ternary model is worth studying as a frontier of model compression. If its quality holds, it could unlock 27B-level capability on devices previously limited to 7B-class models.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*