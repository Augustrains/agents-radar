# Hugging Face Trending Models Digest 2026-07-10

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-10 01:27 UTC

---

Here is the structured Hugging Face Trending Models Digest for July 10, 2026.

---

## Hugging Face Trending Models Digest — 2026-07-10

### 1. Today's Highlights

This week’s trending leaderboard is defined by a massive wave of **GGUF quantizations** and **community fine-tunes** of the latest frontier models, particularly from the Qwen 3.5/3.6 and DeepSeek-V4 families. NVIDIA has made a strong push with efficient, quantized variants (NVFP4) of both Qwen and their own Nemotron models, signaling a focus on inference optimization. Meanwhile, creative image generation is heating up with Krea-2 derivatives (Turbo, ControlNet, LoRAs) and niche lighting LoRAs gaining traction. Two standout models—the uncensored **Qwen3.6-35B-A3B-Uncensored** and the agentic coding **Gemma-4-12B**—dominate both likes and downloads, reflecting deep community interest in specialized, high-performance fine-tunes.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | Likes: 3,728 | Downloads: 362,300
  A massive MoE conversational model with 5.2B active parameters; trending for strong performance and high community engagement as a top-tier open-source Chinese/English chat model.
- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — Author: tencent | Likes: 612 | Downloads: 5,572
  Tencent’s latest Hunyuan-based text-generation model; notable for its scale and enterprise backing, gaining traction in the hybrid transformer space.
- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — Author: InternScience | Likes: 434 | Downloads: 23,112
  A Qwen 3.5 MoE model designed for agentic tasks; trending as the community pivots toward task-oriented, tool-using language agents.
- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — Author: deepseek-ai | Likes: 457 | Downloads: 29,230
  The latest Pro variant of DeepSeek's V4 series with advanced MoE reasoning; trending alongside its associated papers and GGUF quantizations.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — Author: nvidia | Likes: 2,687 | Downloads: 1,447,244
  A 3B parameter image-text-to-text model built for zero-shot object localization and feature extraction; highly popular for its versatility and NVIDIA’s optimized pipeline.
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — Author: krea | Likes: 569 | Downloads: 157,302
  A faster, distilled version of Krea’s raw text-to-image model; trending due to real-time generation use cases and community derivative works (ControlNet, LoRAs).
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 2,595 | Downloads: 2,716,428
  An uncensored vision-language MoE fine-tune of Qwen 3.6; one of the most downloaded models this week due to aggressive reasoning prompts and roleplay community usage.
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — Author: yuxinlu1 | Likes: 2,670 | Downloads: 703,735
  A GGUF-quantized Gemma-4-12B variant fine-tuned for coding and reasoning with the "fable5" dataset; extremely popular for local code generation and agentic terminal use.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Author: google | Likes: 330 | Downloads: 16,374
  Google’s first foundational tabular classification/regression model (TabFM); trending as it enables zero-shot inference on tabular data, a historically difficult domain for LLMs.
- **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — Author: nvidia | Likes: 85 | Downloads: 16,959
  A massive 75B MoE model with only 9B active parameters, optimized with NVFP4 quantization for puzzle-solving and structured reasoning; signals growing demand for efficient game/logic models.
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Author: baidu | Likes: 1,903 | Downloads: 1,246,042
  A feature-extraction model built for unlimited-scope OCR; highly downloaded, indicating strong enterprise demand for scalable document and image-to-text pipelines.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, LoRAs)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — Author: empero-ai | Likes: 1,930 | Downloads: 1,875,602
  A GGUF quantized reasoning model fine-tuned from Qwen 3.5 using synthetic Mythos data; trending for high-quality roleplay and creative writing at 9B scale.
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — Author: yuxinlu1 | Likes: 1,117 | Downloads: 418,171
  An agentic fine-tune of Gemma-4-12B optimized for terminal and coding agent workflows; notable for its "3.5x tau" scaling and strong local deployment performance.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — Author: unsloth | Likes: 1,025 | Downloads: 2,894,918
  A GGUF quantized multi-turn prediction version of Qwen 3.6-27B; Unsloth’s highly optimized kernels make this one of the most downloaded quantized models on the hub.
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — Author: deepreinforce-ai | Likes: 820 | Downloads: 957,721
  A GGUF quantized 35B text-generation model; trending due to its MIT license and broad endpoints compatibility, enabling frictionless local and cloud deployment.
- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — Author: nvidia | Likes: 332 | Downloads: 748,054
  NVIDIA’s in-house FP4 quantized Qwen 3.6-27B, part of the Model Optimizer toolkit; marks a growing trend toward hardware-aware quantization for high-end GPUs.
- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — Author: conradlocke | Likes: 132 | Downloads: 0
  A LoRA for Krea-2 enabling identity-preserving image editing; new release gaining attention for its application in consistent character generation.

### 3. Ecosystem Signal

The ecosystem is signaling a **maturation of the MoE architecture** as the consensus choice for scaling: models like DeepSeek-V4 Pro, GLM-5.2, Agnets-A1, and Nemotron-Labs-Puzzle dominate the high-performance categories, all using Mixture-of-Experts with small active parameter counts (A3B to A9B). The **Qwen family (3.5/3.6)** has emerged as the dominant base architecture for community fine-tunes, far outstripping Llama and Gemma in GGUF and uncensored variants—likely due to its strong multilingual performance and permissive licensing. Quantization is no longer an afterthought: major players like NVIDIA and Unsloth are releasing first-party quantized weights (NVFP4, GGUF) alongside raw models, and community quantization (especially GGUF for local deployment) accounts for the vast majority of downloads. On the vision side, **Krea-2** is building a mini-ecosystem with ControlNet, Turbo, and LoRA adapters, mirroring the SDXL ecosystem maturation of 2024-2025. Notably, **uncensored and roleplay-oriented fine-tunes** (Qwythos, HauhauCS’s Qwen 3.6 uncensored) continue to command some of the highest download counts, indicating a persistent and large community demand for unrestricted, creative-use models.

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2.7K likes and 1.4M downloads, this is the breakout vision model of the week. It fills a critical gap in zero-shot object detection with a lightweight 3B architecture, making it a strong candidate for embedding in both research pipelines and production applications.

2. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — This model combines the powerful Gemma-4 base with a high-quality coding dataset (fable5) and composer tuning. Its massive download count (703k) and high likes (2.6k) suggest it is the current best-in-class for local, low-latency code reasoning—worth trying for anyone building agentic coding tools.

3. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — This is a first-of-its-kind model from Google. If you work with tabular data (CSV, spreadsheets, databases), this zero-shot classifier/regressor could replace traditional gradient-boosting models. It is less hyped than the LLMs, but its potential to disrupt enterprise ML workflows makes it the most strategically important model to study this week.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*