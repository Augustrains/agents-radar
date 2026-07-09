# Hugging Face Trending Models Digest 2026-07-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-09 01:29 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-09

## Today's Highlights

This week's trending models are dominated by the **Qwen 3.5/3.6 ecosystem**, with multiple fine-tunes, quantizations (GGUF), and vision-enabled variants seeing massive adoption — the most downloaded model is an uncensored MoE variant at over 2.8M downloads. **NVIDIA** makes a strong showing with two vision models (LocateAnything-3B, Qwen3.6-27B-NVFP4), while **Google's TabFM** signals growing interest in foundation models for tabular data. Quantized and agentic fine-tunes (Gemma 4, Ornith, Qwythos) continue to drive community engagement, with GGUF format dominating the download counts across the board.

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,666 likes | 281K downloads  
  A conversational MoE model with DSA architecture, trending as one of the highest-liked releases of the week.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 439 likes | 15.5K downloads  
  The latest DeepSeek V4 Pro variant with a dedicated arXiv paper, pushing reasoning and generation capabilities further.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | 563 likes | 121 downloads  
  Hunyuan V3 text-generation model from Tencent, signaling enterprise-grade foundation model releases on Hub.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat | 151 likes | 385 downloads  
  Meituan's extended-context conversational model for long-form reasoning and chat.

- **[poolside/Laguna-XS-2.1](https://huggingface.co/poolside/Laguna-XS-2.1)** — poolside | 76 likes | 3.4K downloads  
  A compact model from poolside focused on development workflows.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,667 likes | 1.4M downloads  
  NVIDIA's feature-extraction vision model for object localization — one of the highest-liked and most downloaded models this week.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,573 likes | 2.8M downloads  
  An uncensored Qwen 3.6 MoE vision model with aggressive tuning — the highest-downloaded model this week.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,873 likes | 1M downloads  
  Baidu's image-text-to-text OCR model with unlimited usage scope, driving massive adoption for document processing.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 1,855 likes | 1.7M downloads  
  A Qwen 3.5-based vision-language model in GGUF format, combining synthetic Claude Mythos data with community quantization.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 555 likes | 123K downloads  
  Krea's next-generation text-to-image model built on Krea-2-Raw, optimized for speed and quality.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 400 likes | 14.7K downloads  
  A Qwen 3.5 MoE vision-language model designed for agentic tasks.

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — nvidia | 325 likes | 538K downloads  
  NVIDIA's optimized Qwen 3.6 variant using FP4 quantization for efficient deployment.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 142 likes | 46 downloads  
  A vision-language Qwen 3.6 model with enhanced reasoning capabilities.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,098 likes | 384K downloads  
  A Gemma 4-based agentic coding model in GGUF, optimized for terminal and composable agent workflows.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,652 likes | 675K downloads  
  A Gemma 4 coding-focused GGUF model with reasoning enhancements — highly popular for code generation.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google | 313 likes | 9.5K downloads  
  Google's foundation model for tabular data classification and regression with zero-shot capabilities.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — mistralai | 166 likes | 157 downloads  
  Mistral's massive sparse MoE model (119B params, 6B active) fine-tuned from Leanstral-2603.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 800 likes | 502K downloads  
  A Qwen 3.5 MoE GGUF quantization — the most popular Ornith variant by download volume.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — deepreinforce-ai | 461 likes | 455K downloads  
  The 9B GGUF variant of Ornith, offering a lightweight alternative for local deployment.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 1,010 likes | 2.8M downloads  
  Unsloth's multi-token prediction (MTP) GGUF quantization of Qwen 3.6 — the second most downloaded model this week.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 781 likes | 0 downloads  
  A utility providing corrected chat templates for Qwen 3.5 models, widely appreciated by the MLX community.

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — deepreinforce-ai | 411 likes | 136K downloads  
  The base Safetensors variant of Ornith 1.0-9B, supporting both text and vision tasks.

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — deepreinforce-ai | 366 likes | 280K downloads  
  The full-precision Ornith 1.0-35B MoE model, foundation for its GGUF quantizations.

- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — unsloth | 96 likes | 47 downloads  
  Unsloth's GGUF quantization of DeepSeek V4, optimized for flash attention inference.

- **[InternScience/Agents-A1-Q4_K_M-GGUF](https://huggingface.co/InternScience/Agents-A1-Q4_K_M-GGUF)** — InternScience | 84 likes | 11.2K downloads  
  A GGUF 4-bit quantization of the Agents-A1 vision-language MoE model.

## Ecosystem Signal

The current landscape shows **Qwen 3.5/3.6** as the undisputed foundation family of the week — six of the top 30 models are Qwen-variant fine-tunes or quantizations, spanning vision, MoE, uncensored, and MTP variants. **GGUF quantization** continues to drive community adoption, with unsloth and deepreinforce-ai emerging as major quantization providers. Notably, **open-weight models from Chinese labs** (Baidu, Meituan, ZAI, Tencent) are gaining significant traction, while Google and NVIDIA maintain strong presences with specialized foundation models (TabFM, LocateAnything). The **agentic coding** trend is pronounced, with Gemma 4-based GGUF models from yuxinlu1 and Mistral's Leanstral pushing toward composable, terminal-native workflows. The absence of major proprietary API-first releases this week underscores the community's preference for **downloadable, quantized open-weight models**.

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — At 2,667 likes and 1.4M downloads, this represents a breakthrough in lightweight vision localization. Highly recommended for anyone building visual grounding or object detection pipelines without heavy compute requirements.

2. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — With 2,652 likes and 675K downloads, this is the standout coding model this week. Its reasoning-aware architecture and GGUF format make it immediately useful for local development and agent-based code workflows.

3. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Though newer to the top charts (313 likes), this tabular foundation model signals a paradigm shift for structured data ML. Worth studying for anyone working with classification, regression, or zero-shot tabular tasks without extensive feature engineering.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*