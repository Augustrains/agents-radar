# Hugging Face Trending Models Digest 2026-07-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-06 01:53 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-06**.

---

## 1. Today’s Highlights

This week’s Hugging Face trending board is dominated by a massive wave of **GGUF quantized MoE models**, led by community remixes of the **Qwen 3.5/3.6** and **GLM-5.2** families. The top spots see fierce competition between **emperor-ai's "Claude-Mythos" fine-tune** and **Nvidia's "LocateAnything-3B"**, signaling a strong appetite for both reasoning-heavy chat bots and specialized vision tools. Notably, **Google** quietly releases `tabfm-1.0.0` for tabular data, marking a rare foray into structured prediction. The ecosystem is clearly bifurcating between massive, quantized MoE architectures and highly specific task models (OCR, object localization, PII detection).

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**  
  *Qwen* | Likes: 549 | Downloads: 55,113  
  A 35B MoE agent-tuned model from Qwen, trending as the official release for agentic workflows.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**  
  *deepseek-ai* | Likes: 390 | Downloads: 12,580  
  DeepSeek's latest V4 Pro variant with a new "DSpark" acceleration method, gaining buzz from its accompanying arXiv paper.

- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)**  
  *deepseek-ai* | Likes: 161 | Downloads: 48,696  
  A faster, more accessible sibling to the V4 Pro, optimizing for speed over raw capability.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  *zai-org* | Likes: 3,470 | Downloads: 220,379  
  The top-rated model on the board: a conversational GLM MoE with a massive 3.4K likes, likely the new best-in-class for Chinese-English dialogue.

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)**  
  *nvidia* | Likes: 240 | Downloads: 280,087  
  Nvidia's FP4 quantized version of GLM-5.2, enabling high-throughput inference on H100/B200 hardware.

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)**  
  *nvidia* | Likes: 123 | Downloads: 10,696  
  A novel "two-tower" architecture from Nvidia Labs, designed for retrieval or dual-encoder use cases.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)**  
  *mistralai* | Likes: 117 | Downloads: 26  
  Mistral's massive 119B MoE model (6B active), trending as a high-end open-weight competitor but with very low download volume.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  *nvidia* | Likes: 2,618 | Downloads: 1,247,265  
  A 3B vision model for zero-shot object localization, exploding in popularity for its simplicity and accuracy.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
  *baidu* | Likes: 1,750 | Downloads: 1,044,217  
  Baidu's "unlimited" OCR model, trending for its ability to handle arbitrary document layouts at scale.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**  
  *krea* | Likes: 515 | Downloads: 99,049  
  A faster distilled variant of Krea-2 for text-to-image generation, popular among the ComfyUI community.

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)**  
  *Comfy-Org* | Likes: 256 | Downloads: 10  
  The official ComfyUI-compatible release of Krea-2, signaling tighter integration with the diffusion ecosystem.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  *yuxinlu1* | Likes: 2,610 | Downloads: 651,758  
  A GGUF version of a heavily fine-tuned Gemma-4 coder, trending as the go-to local coding assistant.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**  
  *google* | Likes: 226 | Downloads: 2,670  
  Google's first foundation model for tabular data, supporting zero-shot classification and regression—a rare and significant release.

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)**  
  *nationaldesignstudio* | Likes: 129 | Downloads: 2,783  
  A BERT-based PII redaction model, trending for compliance and privacy use cases.

- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)**  
  *BugTraceAI* | Likes: 135 | Downloads: 12,196  
  A cybersecurity-focused 27B model, trending in the offensive security community.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
  *empero-ai* | Likes: 1,556 | Downloads: 1,533,844  
  The #1 model by downloads: a "Claude-Mythos" personality fine-tune on Qwen 3.5, packaged as GGUF for LLaMA.cpp.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  *HauhauCS* | Likes: 2,487 | Downloads: 3,018,257  
  The most downloaded model on the board (3M+): an uncensored, "aggressive" personality fine-tune of Qwen 3.6 35B-A3B.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)**  
  *huihui-ai* | Likes: 169 | Downloads: 5,609  
  An "abliterated" (safety-removed) version of GLM-5.2 in GGUF, trending in the local inference community.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  *yuxinlu1* | Likes: 1,029 | Downloads: 355,871  
  A "agentic" variant of the Gemma-4 coder, trending for autonomous coding and terminal use.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
  *unsloth* | Likes: 964 | Downloads: 2,776,389  
  Unsloth's official GGUF of Qwen 3.6 with Multi-Token Prediction, highly downloaded for its speed-efficiency trade-off.

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)**  
  *Jackrong* | Likes: 139 | Downloads: 84,951  
  A community coder fine-tune on Qwen 3.6 35B-A3B with MTP, popular in local dev setups.

## 3. Ecosystem Signal

The current ecosystem is experiencing a **"GGUF MoE boom"**: nearly half of the trending models are quantized MoE models optimized for local inference via `llama.cpp`. The **Qwen 3.5/3.6 family** is the dominant base architecture, spawning hundreds of derivative fine-tunes. Meanwhile, **Nvidia** is aggressively pushing hardware-optimized formats (NVFP4) and novel architectures (TwoTower, LocateAnything), signaling a shift toward inference-hardened deployments. Open-weight momentum is clear—DeepSeek V4, GLM 5.2, and Mistral's Leanstral all release with permissive licenses (Apache-2.0, MIT). On the fine-tuning side, "uncensored" and "abliterated" variants of GLM-5.2 and Qwen 3.6 are surging, reflecting a persistent demand for unrestricted models in the local community. Also notable: Google's `tabfm` marks one of the first attempts at a general-purpose tabular foundation model, a historically underserved category.

## 4. Worth Exploring

1. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** – If you work with structured data, this is a rare and likely impactful release. A foundation model for tables could change how teams approach classification and regression without massive feature engineering.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – With 2.6K likes and 1.2M downloads in a week, this is the breakout vision model. It’s small (3B), fast, and works zero-shot—ideal for robotics, document parsing, and UI automation.

3. **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – The highest-download model for a reason: it combines a "Claude-Mythos" persona with Qwen 3.5 reasoning, packaged for instant local use. Perfect for testing the frontier of personality fine-tuning on small MoEs.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*