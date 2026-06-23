# Hugging Face Trending Models Digest 2026-06-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-23 01:58 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-06-23**.

---

## 1. Today’s Highlights

This week’s trending landscape is defined by a massive spike in MoE (Mixture-of-Experts) adoption, led by **DeepSeek-V4 Pro** (5,012 likes) and **zai-org/GLM-5.2** (2,038 likes)—both demonstrating that large-scale sparse architectures are now mainstream for both enterprise and community users. The **Gemma 4** family continues to command significant attention, with the **12B coder variant** crossing 414,734 downloads, while **NVIDIA’s LocateAnything-3B** signals a shift toward targeted, lightweight multimodal grounding models. Quantization (GGUF) remains the dominant distribution format, powering 8 of the top 30 entries, and **Qwen3.6** derivatives are proliferating rapidly—a clear sign of an open-source ecosystem building aggressively on the Qwen MoE backbone.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  *Author: deepseek-ai | Likes: 5,012 | Downloads: 2,421,858*  
  A flagship conversational MoE model topping the charts in both likes and downloads, reflecting strong enterprise and community trust in DeepSeek’s latest open-weight release.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  *Author: zai-org | Likes: 2,038 | Downloads: 33,589*  
  Zhipu AI’s new MoE-DSA architecture, trending for its balance of efficiency and conversational quality, now widely quantized by the community.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  *Author: google | Likes: 1,138 | Downloads: 1,912,198*  
  Google’s latest “any-to-any” unified model, trending due to its versatility across text, image, and audio inputs in a single 12B parameter package.

- **[MoonshotAI/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  *Author: moonshotai | Likes: 963 | Downloads: 412,778*  
  A code-specialized image-text-to-text model from Moonshot AI, gaining traction for advanced code reasoning with compressed-tensor support.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  *Author: CohereLabs | Likes: 481 | Downloads: 21,078*  
  Cohere’s compact MoE code model, trending as a lightweight alternative for developer tooling and on-device code generation.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  *Author: microsoft | Likes: 289 | Downloads: 3,498*  
  A 4B parameter model with an Explorer SubAgent pipeline, trending for its novel long-context handling approach.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  *Author: nvidia | Likes: 2,291 | Downloads: 247,517*  
  A lightweight 3B image-feature-extraction model for object localization, trending for its high accuracy in a small-footprint package.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MinimaxAI/MiniMax-M3)**  
  *Author: MiniMaxAI | Likes: 1,209 | Downloads: 119,967*  
  A multimodal image-text-to-text model, trending for strong visual reasoning capabilities in a competitive parameter range.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  *Author: google | Likes: 1,049 | Downloads: 874,368*  
  A diffusion-based multimodal conversational model with an MoE 4B active parameter profile, trending for efficient generative image-text interactions.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  *Author: nvidia | Likes: 631 | Downloads: 34,860*  
  A streaming automatic speech recognition model with cache-aware ASR, trending for real-time transcription use cases.

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)**  
  *Author: ostris | Likes: 102 | Downloads: 3,244*  
  A LoRA adapter for Ideogram 4, trending for accelerating image generation with fine-grained style control.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  *Author: owensong | Likes: 167 | Downloads: 0*  
  An ultra-small text-to-speech model, trending for its promise of efficient on-device speech synthesis, despite zero downloads yet.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  *Author: yuxinlu1 | Likes: 2,171 | Downloads: 414,734*  
  The top GGUF fine-tune of Gemma 4 focused on coding and reasoning, trending due to exceptional download velocity and strong community benchmarks.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  *Author: WeiboAI | Likes: 614 | Downloads: 32,385*  
  A Qwen2-based 3B model specialized in math, trending for its surprising reasoning performance at ultra-small scale.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)**  
  *Author: empero-ai | Likes: 128 | Downloads: 842*  
  A Qwen3.5-based reasoning model with a 1M token context, trending for long-document analysis use cases.

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)**  
  *Author: LiquidAI | Likes: 100 | Downloads: 8,822*  
  A 350M sentence-similarity embedding model, trending for retrieval and RAG applications using the LFM2.5 architecture.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  *Author: HauhauCS | Likes: 2,116 | Downloads: 4,078,305*  
  The highest-download model in this digest, a vision MoE fine-tune of Qwen3.6, trending for its uncensored, aggressive behavior tuning in GGUF format.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**  
  *Author: zai-org | Likes: 133 | Downloads: 334,716*  
  Official FP8 quantized version of GLM-5.2, trending as the preferred format for deployment on modern AI accelerators.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  *Author: yuxinlu1 | Likes: 386 | Downloads: 50,314*  
  An agentic fine-tune of Gemma 4 for terminal/automation tasks, trending for pushing autonomous workflow capabilities.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  *Author: Jackrong | Likes: 281 | Downloads: 214,630*  
  A vision-coder hybrid fine-tune of Qwen3.6, trending for combining MTP (Multi-Turn Processing) with GGUF compression.

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)**  
  *Author: bytkim | Likes: 106 | Downloads: 52,774*  
  A GGUF-quantized Qwen3.6 with position-interpolation tuning, trending for enabling longer context windows in consumer hardware.

## 3. Ecosystem Signal

The dominant signal this week is the **rise of Qwen3.6 as a foundational base for fine-tuning**. Variants like *Qwable*, *Qwythos*, *Qwopus*, and aggressive uncensored versions collectively represent 7 of the top 30 models—more than any other family. This signals that the open-source community is converging on Qwen’s MoE architecture as the preferred sandbox for experimentation. **MoE (Mixture-of-Experts) is now the default architecture**, not an exception: over a third of trending models use some form of MoE. **Quantization** (GGUF, FP8) remains the dominant distribution layer, accounting for 8 of the 30 entries and the highest download counts, indicating that inference efficiency still trumps raw capability in adoption velocity. **Enterprise labs (NVIDIA, Google, Microsoft, Baidu)** are pushing specialized, smaller models (3B–12B) for specific tasks (grounding, OCR, streaming ASR), signaling a strategic pivot from “one model to rule them all” to task-optimized, deployable agents. Notably, **open-weight models (DeepSeek-V4 Pro, Gemma 4, Qwen3.6) continue to dominate over proprietary API-only releases**, reinforcing the health of the open-weight ecosystem.

## 4. Worth Exploring

1. **🗺️ [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – A rare example of a *small* multimodal grounding model that’s both trending and practical. Ideal for robotics, visual inspection, and edge deployment—highly recommended for studying how to maximize accuracy with minimal parameters.

2. **🧮 [WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – An excellent case study in scaling math reasoning down to 3B parameters. For researchers and developers interested in compact STEM models, this is a prime candidate for distillation and fine-tuning experiments.

3. **⚡ [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – The fastest-growing code model this week with over 414k downloads. It represents the state of the art in quantized coding LLMs and is a must-test for anyone building developer tools or AI-assisted programming workflows.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*