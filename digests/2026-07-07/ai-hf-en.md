# Hugging Face Trending Models Digest 2026-07-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-07 01:50 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for **2026-07-07**.

---

## 1. Today's Highlights

This week’s trending landscape is dominated by **MoE (Mixture-of-Experts) architectures**, with Qwen 3.5/3.6 and GLM 5.2 spawning the most community activity. **NVIDIA** continues its offensive across multiple verticals, releasing both a massive vision grounding model (`LocateAnything-3B`) and a novel compressed precision model (`Qwen3.6-27B-NVFP4`). The **GGUF quantization ecosystem** remains the primary vector for community adoption, with several high-download models exceeding 1M pulls. Notably, the **Ornith** and **Gemma-4** finetune families are generating strong organic engagement, while Google’s **TabFM** signals a quiet but important push into tabular foundation models.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | 3,530 likes | 231k downloads  
  A strong MoE conversational model from Zhipu AI, trending as the base for many abliterated and quantized variants.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** – deepseek-ai | 409 likes | 14k downloads  
  The latest Pro-level DeepSeek release with dynamic sparse attention (DSpark), accompanied by a technical paper (arxiv:2606.19348).

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** – InternScience | 345 likes | 8.7k downloads  
  A specialized Qwen 3.5 MoE model optimized for agentic workflows, blending vision and text with strong MoE efficiency.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** – mistralai | 143 likes | 106 downloads  
  Mistral’s massive but sparse 119B MoE (6B active), an Apache-2.0 licensed model trained with vLLM compatibility.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** – meituan-longcat | 114 likes | 43 downloads  
  A long-context conversational model from Meituan, designed for extended reasoning over long documents.

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)** – nvidia | 126 likes | 10.7k downloads  
  NVIDIA’s two-tower MoE (30B total, 3B active), likely a base for retrieval or dual-encoder reasoning setups.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu | 1,793 likes | 1.07M downloads  
  A general-purpose OCR model from Baidu, trending heavily for its broad feature extraction capabilities.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia | 2,635 likes | 1.34M downloads  
  NVIDIA’s 3B vision grounding model for fine-grained object localization, one of the week’s highest-liked releases.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** – krea | 529 likes | 109k downloads  
  A turbo-version of the Krea-2 text-to-image pipeline, optimized for faster inference over the base model.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | 2,529 likes | 2.91M downloads  
  An uncensored, aggressively tuned vision-MoE variant of Qwen 3.6, the second-most downloaded model this week.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** – google | 257 likes | 7k downloads  
  Google’s first official PyTorch release of TabFM, a zero-shot foundation model for tabular classification and regression.

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** – nationaldesignstudio | 136 likes | 3.8k downloads  
  A BERT-based PII/token classification model, exported to ONNX with transformers.js support for browser-based inference.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – froggeric | 698 likes | 0 downloads  
  A non-model utility release that provides corrected Jinja chat templates for Qwen 3.5, highly valued by the MLX community.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai | 1,642 likes | 1.61M downloads  
  The GGUF version of a Qwen 3.5-based reasoning finetune (Claude Mythos style), one of the most downloaded models this week.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – yuxinlu1 | 2,623 likes | 664k downloads  
  A high-performance coding GGUF finetune of Gemma 4, explicitly optimized for LLM-based reasoning and terminal agent use.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** – deepreinforce-ai | 758 likes | 436k downloads  
  MIT-licensed GGUF of the 35B Ornith MoE, fine-tuned for endpoint compatibility and local deployment.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** – huihui-ai | 176 likes | 6.6k downloads  
  An “abliterated” (safety-filter removed) GGUF variant of GLM 5.2, built with Unsloth for maximum community modifiability.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** – unsloth | 974 likes | 2.81M downloads  
  The most downloaded model this week, a Qwen 3.6 vision-MoE GGUF optimized by Unsloth with multi-token prediction (MTP).

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)** – Jackrong | 151 likes | 126k downloads  
  A coding-focused GGUF variant of Qwen 3.6 MoE, combining vision with multi-token prediction for code generation.

- **[DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED](https://huggingface.co/DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED)** – DavidAU | 158 likes | 58k downloads  
  A deliberately uncensored and “high-IQ” finetune of Qwen 3.5, designed for maximal reasoning without alignment constraints.

---

## 3. Ecosystem Signal

The most dominant trend this week is the **rise of MoE-based vision-language models**, especially the Qwen 3.5/3.6 family and GLM-5.2. Nearly half of the top-30 models are derivatives of these two base architectures, with GGUF quantization acting as the primary distribution channel for local inference. NVIDIA is making a strong play across both **inference efficiency** (NVFP4 compression, TwoTower MoE) and **multimodal grounding** (LocateAnything-3B), signaling a shift toward practical, deployment-ready models over raw scale. On the **open-weight front**, DeepSeek continues to release competitive research models with accompanying papers, while Mistral's Leanstral-1.5 provides a fully open (Apache-2.0) alternative to the increasingly MoE-centric landscape. The prevalence of uncensored and abliterated variants suggests a growing user demand for **unrestricted base models**, especially for coding and reasoning tasks. Finally, Google's TabFM indicates a quiet but meaningful expansion into **non-textual foundation models**, which could open a new competitive frontier beyond LLMs.

---

## 4. Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – With 2.6K likes and 1.3M downloads, this is the highest-liked non-GGUF model. It represents the state-of-the-art in lightweight vision grounding and is immediately useful for developers building visual search or RPA pipelines.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – A standout in the coding GGUF space with 2.6K likes. Its combination of Gemma 4 base, agentic tuning, and terminal optimization makes it a strong candidate for local agentic coding workflows.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** – Though lower in viral metrics, this model is strategically important. It is Google’s first PyTorch-native tabular foundation model and could reshape how practitioners approach zero-shot tabular tasks, reducing reliance on gradient-boosted trees.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*