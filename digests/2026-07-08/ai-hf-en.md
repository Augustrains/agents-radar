# Hugging Face Trending Models Digest 2026-07-08

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-08 01:21 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-08

## 1. Today's Highlights

This week's trending models reveal a clear dominance of **Qwen 3.5/3.6 ecosystem** with multiple fine-tunes, MoE variants, and GGUF quantizations dominating the leaderboard. The highest-liked model is **zai-org/GLM-5.2** (3,591 likes), a conversational MoE model from the GLM family, while **HauhauCS/Qwen3.6-35B-A3B-Uncensored** leads downloads (2.8M). NVIDIA continues its strong presence with two notable entries: **LocateAnything-3B**, a vision-language grounding model with 2,657 likes, and a new NVFP4 quantized Qwen variant. The **Gemma-4-12B** family sees significant community activity via GGUF fine-tunes optimized for coding and agentic use cases. Overall, the week is characterized by aggressive MoE quantization activity, uncensored model variants, and a growing appetite for vision-language models in the GGUF format.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,591 likes | 281,584 downloads  
  A conversational MoE model from the GLM family, topping the likes chart this week for its strong instruction-following capabilities.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — mistralai | 157 likes | 157 downloads  
  A massive 119B-parameter MoE model (6B active) fine-tuned from Leanstral-2603, demonstrating Mistral's continued investment in sparse expert architectures.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 424 likes | 15,538 downloads  
  The latest in DeepSeek's V4 series with accompanying arXiv paper, signaling ongoing frontier-model research from DeepSeek.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 488 likes | 121 downloads  
  Tencent's HyV3 text-generation model, a new player entering the open-weight LLM space.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat | 139 likes | 385 downloads  
  Meituan's long-context conversational model, designed for extended dialogue use cases.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,657 likes | 1,424,958 downloads  
  NVIDIA's vision-language grounding model for object localization, combining strong accuracy with a compact 3B parameter count.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,833 likes | 1,084,945 downloads  
  A comprehensive OCR model from Baidu—likely trending for its unlimited-use license and strong performance on document understanding.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 540 likes | 123,729 downloads  
  A text-to-image diffusion model built on Krea-2-Raw, optimized for faster inference without quality degradation.

- **[eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)** — eric-venti-seeds | 97 likes | 0 downloads  
  A lighting-direction LoRA for Flux2Klein9B, enabling fine-grained control over sun direction in generated images.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 1,758 likes | 1,683,711 downloads  
  A GGUF-quantized multimodal model based on Qwen 3.5, optimized for reasoning tasks with a Claude-style persona.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,638 likes | 674,977 downloads  
  A GGUF-quantized Gemma-4-12B fine-tune using the Fable5-Composer2.5 recipe, optimized for code generation and reasoning.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,076 likes | 384,383 downloads  
  A specialized Gemma-4-12B variant for agentic/terminal use cases, with additional training for tool-calling and command execution.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google | 287 likes | 9,458 downloads  
  Google's TabFM foundation model for tabular data—supporting classification, regression, and zero-shot learning without task-specific fine-tuning.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,551 likes | 2,823,988 downloads  
  An uncensored, aggressively-tuned MoE variant of Qwen 3.6 with vision capability—the most downloaded model this week.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 991 likes | 2,842,118 downloads  
  Unsloth's GGUF quantization of Qwen 3.6 with Multi-Token Prediction support—the highest-downloaded model on the leaderboard.

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — nvidia | 315 likes | 538,687 downloads  
  NVIDIA's 4-bit floating-point quantization of Qwen 3.6 using their Model Optimizer toolkit, maintaining high accuracy while reducing memory footprint.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — huihui-ai | 185 likes | 7,349 downloads  
  An "abliterated" (safety-filter-removed) GGUF version of GLM-5.2, built with Unsloth for community experimentation.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 779 likes | 502,663 downloads  
  Quantized version of the Ornith-1.0-35B MoE model, offering MIT-licensed, endpoint-compatible deployment options.

- **[InternScience/Agents-A1-Q4_K_M-GGUF](https://huggingface.co/InternScience/Agents-A1-Q4_K_M-GGUF)** — InternScience | 74 likes | 11,226 downloads  
  A 4-bit quantized MoE vision-language model from InternScience's Agents-A1 series, designed for agent-based applications.

## 3. Ecosystem Signal

The current trending landscape reveals **three dominant forces** shaping the open-weight AI ecosystem:

**Qwen 3.5/3.6 ecosystem dominance**: Nearly one-third of trending models are Qwen-derived, spanning base models, MoE variants (35B-A3B), and vision-language hybrids. The community is rapidly adopting Qwen as the preferred base for fine-tuning and quantization, surpassing Llama in community activity.

**MoE quantization explosion**: The simultaneous rise of models like `Qwen3.6-35B-A3B`, `Ornith-1.0-35B`, `Leanstral-1.5-119B-A6B`, and `Nemotron-Labs-TwoTower-30B-A3B` signals that **Mixture-of-Experts architectures have become the standard** for efficient deployment. The "dense-to-MoE" trend appears permanent, with the ecosystem optimizing for sparse activation at inference time.

**GGUF as the universal format**: Despite competing formats (AWQ, GPTQ, EXL2, NVFP4), GGUF remains the dominant quantization format—accounting for 12 of 30 trending models. This is driven by llama.cpp's wide platform support and the "run anything locally" movement.

**Open-weight remains commercial-grade**: Major companies (NVIDIA, Baidu, Tencent, Meituan, DeepSeek, Mistral) continue to release competitive open models. The line between "open research" and "commercial product" continues to blur—NVIDIA now ships 4 models on the leaderboard alone.

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — At 2,657 likes with 1.4M downloads, this compact vision-language grounding model is remarkable. It offers precise object localization without requiring detection-specific training data, making it a strong candidate for robotics, document AI, and interactive applications. Its 3B size means it runs efficiently on consumer GPUs.

2. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Google's TabFM is a rare entry: a foundation model for tabular data. Unlike LLMs, it supports zero-shot classification and regression on tabular datasets without fine-tuning. This could transform enterprise ML workflows where tabular data dominates but foundation models have been absent.

3. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — The most downloaded model this week (2.8M) and one of the most liked (2,551). This uncensored MoE vision-language model epitomizes the community's appetite for unconstrained, aggressive fine-tuning. Studying it reveals what the open-source community prioritizes when safety filters are removed, and its MoE architecture (35B total, 3B active) represents the sweet spot for local deployment of capable VLMs.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*