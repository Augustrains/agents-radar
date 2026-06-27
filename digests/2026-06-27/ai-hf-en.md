# Hugging Face Trending Models Digest 2026-06-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-27 01:56 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-06-27**.

---

## 1. Today's Highlights

This week’s trending models reveal a strong shift toward **multimodal MoE (Mixture-of-Experts) architectures** and **high-efficiency quantization**. The **Qwen 3.5/3.6** family dominates the list, with community variants like **HauhauCS** and enterprise quantizations from **NVIDIA** seeing massive download volumes. **NVIDIA** also made a significant push with its **NVFP4** precision models (e.g., `Qwen3.6-35B-A3B-NVFP4` hitting 4.8M downloads), signaling a growing industry focus on hardware-optimized inference. Meanwhile, **Google’s Gemma 4** series (especially coding variants like `gemma-4-12B-coder-fable5`) has seen explosive community fine-tuning activity, and **Baidu’s Unlimited-OCR** stands out as a rare but highly popular non-LLM model in the top ranks.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | Likes: 2,594 | Downloads: 83,589  
  A powerful new MoE conversational model from the GLM lineage, trending due to its strong reasoning and MoE efficiency.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – WeiboAI | Likes: 731 | Downloads: 54,638  
  A compact 3B model fine-tuned for math and logical reasoning, popular for its strong performance-to-size ratio.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** – nvidia | Likes: 708 | Downloads: 56,434  
  A streaming ASR model optimized for low-latency speech recognition, trending as a practical voice interface solution.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** – microsoft | Likes: 355 | Downloads: 5,735  
  A 4B model with an "Explorer SubAgent" design for efficient long-context processing, signaling Microsoft’s focus on agentic workflows.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** – LiquidAI | Likes: 113 | Downloads: 8,286  
  A tiny 230M Liquid Foundation Model, trending as an edge-friendly alternative for lightweight text generation.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** – Chunjiang-Intelligence | Likes: 108 | Downloads: 1,103  
  A specialized DeepSeek v4 variant with a focus on cybersecurity, gaining attention in the security-focused AI community.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu | Likes: 1,044 | Downloads: 134,146  
  A state-of-the-art OCR model from Baidu supporting unlimited text extraction, trending for its enterprise-grade accuracy.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** – krea | Likes: 285 | Downloads: 8,721  
  The turbo-distilled variant of Krea-2 for faster text-to-image generation, popular among AI art creators.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia | Likes: 2,385 | Downloads: 494,756  
  A groundbreaking 3B model from NVIDIA for visual grounding and object localization, trending for its versatile image understanding.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** – MiniMaxAI | Likes: 1,246 | Downloads: 169,951  
  A large multimodal model with vision-language capabilities, rising as a strong open-weight alternative for multimodal tasks.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** – datalab-to | Likes: 159 | Downloads: 6,054  
  A Qwen-3.5-based model fine-tuned for PDF and document understanding, trending for enterprise document AI applications.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** – Qwen | Likes: 322 | Downloads: 13,186  
  An agent-focused MoE model from Qwen, designed for autonomous task completion and tool use in simulated environments.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | Likes: 2,265 | Downloads: 3,453,492  
  An uncensored, aggressively tuned MoE vision model with massive downloads, trending due to its unconstrained creative output and multimodal MoE architecture.

### 🔧 Specialized Models (Code, Math, Medical, Embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – yuxinlu1 | Likes: 2,400 | Downloads: 516,333  
  A top-tier code-focused Gemma 4 variant from a community composer, trending for its high-quality code generation and reasoning in GGUF format.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** – yuxinlu1 | Likes: 689 | Downloads: 186,663  
  A specialized agentic coding model built on Gemma 4, trending for its enhanced terminal and tool-use capabilities.

### 📦 Fine-tunes & Quantizations (Community, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai | Likes: 590 | Downloads: 486,810  
  The GGUF quantized version of Qwythos-9B, a mythos-inspired reasoning model, trending due to efficient local inference.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** – unsloth | Likes: 411 | Downloads: 107,553  
  Unsloth’s optimized GGUF conversion of GLM-5.2, trending for enabling fast local inference on the popular MoE model.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** – nvidia | Likes: 361 | Downloads: 4,812,629  
  NVIDIA’s 4-bit NVFP4 quantized MoE model, the highest-downloaded model this week, driven by enterprise demand for efficient high-quality inference on NVIDIA hardware.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** – deepreinforce-ai | Likes: 236 | Downloads: 3,002  
  A GGUF quantization of the Ornith 1.0 35B MoE model, gaining traction for end-point compatible deployment.

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** – Jackrong | Likes: 95 | Downloads: 35,027  
  A GGUF variant of Qwopus 3.6 for vision-language coding tasks, trending for its MTP (Multi-Turn Prefix) compatibility.

---

## 3. Ecosystem Signal

The current ecosystem is being shaped by three major forces. First, **MoE architecture dominance** is now undeniable: the Qwen 3.5/3.6 and GLM 5.2 families appear in multiple positions, with active MoE parameter counts (e.g., 35B-A3B) becoming a standard marketing metric. Second, **quantization has become a first-class citizen**, led by NVIDIA’s **NVFP4** format and the ubiquitous **GGUF** ecosystem—together, they enable massive models (up to 397B) to be run locally. Third, **composer-based fine-tuning** is on the rise: models like `gemma-4-12B-coder-fable5-composer2.5` show a trend where community "composers" merge multiple fine-tunes into powerful specialized variants. Notably, **open-weight models are clearly winning** for on-premise and edge deployments, while proprietary API models are being challenged by these highly optimized, often uncensored, community releases.

---

## 4. Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – With 2.4K weekly likes and nearly 500K downloads, this model represents a paradigm shift in visual grounding. It is worth studying for anyone building vision-language agents or performing object detection without bounding-box training data.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – Despite its controversial "uncensored" label, its 3.45M downloads and 2.2K likes make it a must-examine case study in what the community values: high-capacity MoE models with aggressive creativity and minimal guardrails.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – As the highest-liked coder model (2.4K likes) with over 500K downloads, this is the definitive example of community-driven model composition. It represents the best of the open-source "composer" trend and is ideal for anyone evaluating Gemma 4 for coding tasks.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*