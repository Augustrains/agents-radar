# Hugging Face Trending Models Digest 2026-07-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-05 01:46 UTC

---

# 🤗 Hugging Face Trending Models Digest – July 5, 2026

## 1. Today's Highlights

This week's trending models reveal an ecosystem surging toward **MoE (Mixture-of-Experts) architectures**, with deepreinforce-ai's entire Ornith-1.0 lineup (9B, 35B, 397B) and Qwen's AgentWorld-35B-A3B leading the charge. **Uncensored and "abliterated" variants** are seeing explosive adoption—HauhauCS's Qwen3.6-35B-A3B-Uncensored topped 2.9M downloads in its first week. Meanwhile, NVIDIA continues its dual push into **4-bit FP4 quantization** (Qwen3.6-27B-NVFP4, GLM-5.2-NVFP4) and specialized vision tools like LocateAnything-3B. The GGUF quantization ecosystem remains the dominant format for local inference, with **7 of the top 10 most-downloaded models** using GGUF.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* | 3,398 likes, 208,920 downloads  
  Leading model of the week by likes; a conversational MoE model using the GLM_MoE_DSA architecture, signaling strong community interest in the GLM family.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — *deepseek-ai* | 370 likes, 10,306 downloads  
  The flagship open-weight DeepSeek V4 release, accompanied by a published arXiv paper (2606.19348), positioning it as a serious research-grade model.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — *mistralai* | 100 likes, 4 downloads  
  A massive 119B-parameter MoE with only 6B active parameters, built on the Leanstral-2603 base—an efficiency-focused model from Mistral.

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — *deepreinforce-ai* | 209 likes, 33,268 downloads  
  The largest Ornith variant, a 397B MoE model based on Qwen3.5, demonstrating the community's appetite for frontier-scale open models.

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)** — *nvidia* | 121 likes, 10,479 downloads  
  A novel "two-tower" architecture—30B total, 3B active—from NVIDIA Labs, exploring dual-tower designs for improved reasoning.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* | 2,604 likes, 1,194,542 downloads  
  The week's top multimodal model; a 3B-parameter image-text-to-text model for object localization and visual grounding, seeing massive adoption.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | 2,454 likes, 2,993,053 downloads  
  The most-downloaded model of the week (2.99M), an uncensored Qwen3.6 vision MoE variant built for aggressive, unfiltered outputs.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* | 1,714 likes, 988,379 downloads  
  Baidu's universal OCR model, handling image-text-to-text for document recognition; near-1M downloads prove strong enterprise and tools demand.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — *krea* | 496 likes, 89,384 downloads  
  A turbo-optimized text-to-image diffusion model built on Krea-2-Raw, balancing quality and inference speed.

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — *fal* | 157 likes, 0 downloads  
  A LoRA adapter for LTX-2.3 enabling 3D-realistic video generation from images; fresh release with high community anticipation.

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — *Comfy-Org* | 249 likes, 10 downloads  
  Krea-2 in ComfyUI-native format, simplifying image generation workflow integration.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — *yuxinlu1* | 2,595 likes, 641,260 downloads  
  A specialized coding variant of Gemma 4 with the "Fable5" fine-tuning; one of the most popular code-focused models this week.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — *yuxinlu1* | 1,010 likes, 342,752 downloads  
  Gemma 4 fine-tuned for agentic coding tasks and terminal use, supporting the "agentic coding" trend.

- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** — *BugTraceAI* | 132 likes, 12,001 downloads  
  Security-focused model for offensive security and cybersecurity analysis, built on Qwen3.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *google* | 196 likes, 1,177 downloads  
  Google's foundation model for tabular data (classification, regression), enabling zero-shot predictions on structured data—an important but niche release.

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** — *nationaldesignstudio* | 122 likes, 1,881 downloads  
  A BERT-based ONNX model for token-level PII detection; optimized for browser deployment via Transformers.js.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* | 1,461 likes, 1,464,047 downloads  
  A Qwen3.5 fine-tune using synthetic "Claude Mythos" data (1M examples) in GGUF; second-most downloaded model overall.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai* | 712 likes, 359,659 downloads  
  GGUF quantized version of the Ornith-1.0-35B MoE model, making high-performance MoE accessible for local inference.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — *deepreinforce-ai* | 424 likes, 320,660 downloads  
  The 9B Ornith variant in GGUF, offering a lightweight MoE option for resource-constrained setups.

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — *nvidia* | 250 likes, 184,521 downloads  
  NVIDIA's 4-bit floating-point (NVFP4) quantization of Qwen3.6-27B, enabling high-throughput inference on NVIDIA hardware.

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** — *nvidia* | 227 likes, 236,501 downloads  
  GLM-5.2 quantized to NVFP4 by NVIDIA, combining the GLM architecture with efficient FP4 inference.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — *huihui-ai* | 162 likes, 4,701 downloads  
  GLM-5.2 with safety guardrails removed ("abliterated"), quantized to GGUF for unfiltered local use.

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)** — *Jackrong* | 131 likes, 59,971 downloads  
  A coding-focused Qwen3.6 MoE variant with Multi-Turn Prompt (MTP) tuning, quantized for local deployment.

## 3. Ecosystem Signal

The Hugging Face ecosystem is undergoing a **MoE renaissance**. Five of the top trending models use Mixture-of-Experts architectures (Ornith variants, Qwen AgentWorld, GLM-5.2), with active parameter counts as low as 3B (Qwen-35B-A3B) or 6B (mistralai Leanstral). This shift toward **sparse activation** models suggests the community is prioritizing inference efficiency without sacrificing model scale.

**Quantization continues to dominate downloads.** Over 60% of top-30 models use GGUF or NVFP4 formats, confirming llama.cpp/GPTQ as the dominant local inference stack. Notably, NVIDIA is pushing its proprietary NVFP4 format for enterprise users, while the GGUF ecosystem covers consumer hardware.

The **"uncensored/abliterated" trend** is accelerating—HauhauCS's Qwen3.6 uncensored model saw 2.99M downloads in days, and huihui-ai's GLM-5.2 abliterated variant indicates growing demand for unfiltered model behavior, likely for creative writing, roleplay, and local experimentation.

**NVIDIA's dual strategy** is noteworthy: they lead in both specialized vision (LocateAnything-3B) and production-grade quantization (NVFP4 series), positioning themselves as the hardware+software stack provider for both frontier research and deployment.

Open-weight models (Qwen3.5/3.6, GLM, Gemma 4, DeepSeek V4) are winning against proprietary closed models, as the community fine-tunes and redistributes these bases extensively. Baidu's Unlimited-OCR shows that **enterprise tools** (OCR, tabular, security) also have a strong open-weight presence.

## 4. Worth Exploring

1. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — With 2.99M downloads in its first week, this model is the most-heavily downloaded release on the list. If you're interested in the uncensored/creative writing use case, this is the community's current favorite. Study its aggressive tuning approach for understanding how alignment bypassing works in practice.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A 3B vision model with 1.19M downloads, this is NVIDIA's answer to object localization in a compact package. Worth trying if you need a fast, open-weight visual grounding model for applications like robotics, document processing, or image retrieval.

3. **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — The largest Ornith variant (397B parameters, MoE) based on Qwen3.5 shows the bleeding edge of what open-weight MoE can achieve. For researchers and engineers pushing frontier model performance, this is a must-study for understanding sparse activation at scale.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*