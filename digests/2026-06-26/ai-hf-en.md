# Hugging Face Trending Models Digest 2026-06-26

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-26 02:02 UTC

---

Here is the structured **Hugging Face Trending Models Digest** for 2026-06-26.

---

## 1. Today's Highlights

This week’s trending models are dominated by the explosive momentum of the **Qwen 3.6 / GLM-5.2** family and the continued reign of **DeepSeek-V4-Pro** as the most-liked release. The community is heavily gravitating toward **Mixture-of-Experts (MoE)** architectures for their efficiency, with models like `GLM-5.2` and `Qwen AgentWorld` showcasing strong interest. **Google’s Gemma-4** series has also solidified its presence, particularly for coding and uncensored fine-tunes, while the **text-to-image** space sees a notable entry from **Krea-2**. The quantization ecosystem remains hyperactive, with GGUF variants of nearly every top model seeing massive download counts.

## 2. Trending Models by Category

### 🧠 Language Models

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  *Author: deepseek-ai | Likes: 5,061 | Downloads: 1,878,217*  
  The leading open-weight conversational model of the week; likely a significant performance leap, driving the highest community engagement.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  *Author: zai-org | Likes: 2,479 | Downloads: 67,107*  
  A powerful new MoE architecture (GLM MoE DSA) topping the trending list, signaling strong interest in sparse activation models.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**  
  *Author: Qwen | Likes: 243 | Downloads: 3,389*  
  A 35B MoE model with only 3B active parameters, optimized for agent-based tasks and multimodal understanding.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  *Author: moonshotai | Likes: 992 | Downloads: 502,106*  
  A code-optimized multimodal model from Kimi, gaining traction for its compressed-tensor approach and strong coding benchmarks.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)**  
  *Author: LiquidAI | Likes: 73 | Downloads: 7,334*  
  An ultra-small 230M parameter model, likely Liquid’s latest attempt at compact, efficient reasoning for edge devices.

### 🎨 Multimodal & Generation

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  *Author: MiniMaxAI | Likes: 1,241 | Downloads: 154,350*  
  A high-performing multimodal (vision-language) model that is rapidly adopted, reflecting the ongoing appetite for multimodal understanding.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**  
  *Author: krea | Likes: 243 | Downloads: 2,996*  
  A turbo version of the Krea-2 image generation model, optimized for speed over the raw base model.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  *Author: owensong | Likes: 201 | Downloads: 0*  
  An ultra-small text-to-speech model, interesting for on-device speech synthesis.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  *Author: google | Likes: 1,178 | Downloads: 2,187,644*  
  Google’s flagship any-to-any instruction model, versatile for both text and image inputs.

### 🔧 Specialized Models

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  *Author: nvidia | Likes: 2,365 | Downloads: 407,838*  
  An image-feature extraction model for spatial localization tasks; huge traction from the robotics and vision communities.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  *Author: microsoft | Likes: 345 | Downloads: 5,276*  
  A 4B parameter model specialized for long-context retrieval and agentic sub-tasks, designed for speed.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  *Author: nvidia | Likes: 695 | Downloads: 50,553*  
  A streaming automatic speech recognition model optimized for real-time, cache-aware inference.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)**  
  *Author: Chunjiang-Intelligence | Likes: 90 | Downloads: 646*  
  A cybersecurity-tuned variant of DeepSeek-v4, indicating the community’s interest in domain-specific safety models.

### 📦 Fine-tunes & Quantizations

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  *Author: yuxinlu1 | Likes: 2,366 | Downloads: 495,813*  
  The most popular GGUF quantized coding fine-tune of Gemma-4, showing the community’s love for accessible, quantized code models.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  *Author: HauhauCS | Likes: 2,237 | Downloads: 3,520,206*  
  The most downloaded model this week: a massive, uncensored vision-MoE quantization, highlighting the appetite for unrestricted multimodal models.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**  
  *Author: nvidia | Likes: 341 | Downloads: 4,602,255*  
  An NVidia-optimized FP4 quantized version of the Qwen 3.6 MoE, likely offering extreme memory savings for enterprise deployment.

## 3. Ecosystem Signal

The current ecosystem is clearly pivoting toward **Mixture-of-Experts (MoE)** models as the default architecture for both efficiency and scale, as seen with the simultaneous traction of `GLM-5.2`, `Qwen AgentWorld`, and `Kimi-K2.7`. The **uncensored and unconstrained fine-tuning** trend is at an all-time high (e.g., `Qwen3.6-35B-A3B-Uncensored`), with millions of downloads for aggressive variants. Open-weight models are winning decisively: the top 5 models by likes are all open-weight, led by DeepSeek-V4-Pro. **GGUF quantization** remains the dominant distribution format, with community finetuners (yuxinlu1, HauhauCS, huihui-ai) acting as key distribution channels. The **ASR and edge TTS** space is also heating up, with Nvidia and owensong releasing tiny, efficient models.

## 4. Worth Exploring

1. **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** – With 4.6M downloads, this is the most-used quantized model on the hub. It represents the state of the art in FP4 quantization for MoE architectures, essential for anyone deploying large models on constrained hardware.

2. **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** – A fascinating 230M parameter model that rivals much larger models. Worth studying for efficiency research, edge deployment, or as a compact foundation for fine-tuning.

3. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – With 407K downloads and a very specific spatial reasoning task, this model signals a shift toward **specialized vision tools** beyond standard classification and captioning. Ideal for robotics, AR/VR, and document layout analysis.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*