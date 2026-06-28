# Hugging Face Trending Models Digest 2026-06-28

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-28 02:07 UTC

---

Here is the structured Hugging Face Trending Models Digest for June 28, 2026.

---

## Hugging Face Trending Models Digest – 2026-06-28

### 1. Today's Highlights

This week’s trending models reveal a clear shift toward **massive, multimodal MoE (Mixture of Experts) architectures** and their optimized quantized variants. **Qwen 3.6 and GLM-5.2** families dominate the top ranks, with uncensored and fine-tuned versions like `HauhauCS/Qwen3.6-35B-A3B-Uncensored` amassing over 3.3 million downloads. The ecosystem is also seeing **explosive growth in GGUF quantized models** for local deployment, alongside strong releases from **NVIDIA** (vision, ASR, and model optimization) and **Microsoft** (fast-context agents). Notably, **Krea-2 Turbo** represents a landmark text-to-image release from the gaming/AI-art community, while **LiquidAI’s LFM2.5-230M** proves that extremely small, efficient LMs remain relevant.

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  zai-org | Likes: 2,683 | Downloads: 98,994  
  A flagship MoE conversational model from the GLM family, trending for its strong general reasoning and chat performance.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  HauhauCS | Likes: 2,277 | Downloads: 3,331,475  
  An uncensored, aggressive variant of Qwen 3.6 MoE, hugely popular for roleplay and unrestricted generation tasks.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**  
  deepseek-ai | Likes: 127 | Downloads: 0  
  The latest DeepSeek V4 Pro variant with "DSpark" optimization, trending for its arXiv publication and potential reasoning improvements.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)**  
  Chunjiang-Intelligence | Likes: 113 | Downloads: 1,328  
  A cybersecurity-focused fine-tune of DeepSeek V4, gaining traction in the safety and red-teaming community.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  microsoft | Likes: 365 | Downloads: 6,447  
  A 4B model optimized for fast long-context processing and agentic sub-agent tasks, signaling Microsoft’s push into efficient agents.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  MiniMaxAI | Likes: 1,253 | Downloads: 182,714  
  A multimodal text-image LLM from MiniMax, trending for its strong vision-language integration in a compact package.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
  baidu | Likes: 1,140 | Downloads: 212,760  
  A feature-extraction model for unlimited OCR tasks, trending for its broad utility in document processing pipelines.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
  empero-ai | Likes: 674 | Downloads: 712,627  
  A GGUF quantized multimodal reasoning model (image-text-to-text), extremely popular for local inference on consumer hardware.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**  
  krea | Likes: 311 | Downloads: 17,445  
  A high-speed text-to-image model built on Krea-2-Raw, trending for its adoption in real-time generative art workflows.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  nvidia | Likes: 718 | Downloads: 61,857  
  A compact streaming ASR model from NVIDIA, trending for low-latency speech recognition in edge and real-time applications.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  nvidia | Likes: 2,408 | Downloads: 570,466  
  A 3B image-feature-extraction model for object localization and segmentation, trending for its high accuracy and small footprint.

- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)**  
  HauhauCS | Likes: 96 | Downloads: 32,222  
  An uncensored, quantized (QAT) multimodal variant of Gemma 4 12B, popular among the uncensored vision-LM community.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  yuxinlu1 | Likes: 2,427 | Downloads: 536,130  
  A GGUF quantized code-specialized Gemma 4 model, trending for its strong coding and reasoning capabilities in terminal/agentic workflows.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  WeiboAI | Likes: 742 | Downloads: 57,521  
  A 3B math and reasoning model based on Qwen2, trending for its surprising performance on mathematical benchmarks at a very small size.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**  
  nvidia | Likes: 367 | Downloads: 5,022,254  
  An NVIDIA-optimized FP4 quantized version of Qwen 3.6 MoE, trending for extreme compression (5M+ downloads) and enterprise deployment.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)**  
  LiquidAI | Likes: 129 | Downloads: 9,791  
  A tiny 230M parameter LM, trending for its efficiency and potential as a lightweight embedding or fast-response model.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**  
  unsloth | Likes: 426 | Downloads: 125,230  
  Unsloth’s GGUF quantization of GLM-5.2, making this powerful MoE model accessible for consumer GPU inference.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  yuxinlu1 | Likes: 733 | Downloads: 206,828  
  A specialized agentic coding variant of Gemma 4 12B in GGUF, optimized for terminal and autonomous agent use.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**  
  deepreinforce-ai | Likes: 328 | Downloads: 20,266  
  The GGUF version of the Ornith 1.0 35B MoE model, trending for its MIT license and endpoint compatibility.

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)**  
  Jackrong | Likes: 97 | Downloads: 49,935  
  A GGUF multi-token prediction (MTP) coder variant of Qwen 3.6, trending for its vision-coder hybrid capabilities.

### 3. Ecosystem Signal

The current ecosystem is defined by **two parallel waves**: massive MoE models (35B+ active parameters) and their aggressive quantization to **GGUF and FP4 formats** for local deployment. The **Qwen 3.5/3.6** and **Gemma 4** families are the most active bases for fine-tuning, with **uncensored and "abliterated" variants** (e.g., HauhauCS, huihui-ai) carving out a strong niche in the open-weight community. **NVIDIA’s Model Optimizer** pipeline is gaining mainstream traction, as seen in both Qwen3.6-NVFP4 and GLM-5.2-NVFP4, which together have amassed over 5 million downloads. **DeepSeek V4** and **GLM-5.2** are emerging as serious contenders beyond the Qwen/Gemma duopoly. On the specialized side, **code and vision-LM hybrids** dominate, while Krea-2 Turbo signals that text-to-image is still a vibrant, community-driven space.

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2,400+ likes and 570K downloads, this is the standout vision model of the week. Its ability to perform open-vocabulary object localization at just 3B parameters makes it essential for anyone building lightweight, real-time vision pipelines.

2. **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — This 4B long-context agent model from Microsoft is a strong signal for where efficient agentic AI is heading. It’s small enough to fine-tune on a single GPU while targeting tasks that typically require much larger models.

3. **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-230M)** — At only 230M parameters, this model is a marvel of efficiency. It’s worth studying for embedding, fast-response chat, or on-device applications where every millisecond and megabyte counts.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*