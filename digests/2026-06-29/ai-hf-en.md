# Hugging Face Trending Models Digest 2026-06-29

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-29 02:06 UTC

---

Here is the structured Hugging Face Trending Models Digest for 2026-06-29.

---

## Hugging Face Trending Models Digest – 2026-06-29

### 1. Today's Highlights

This week’s trending models showcase a clear shift toward **massive, quantized MoE (Mixture-of-Experts) architectures** and **agentic, uncensored fine-tunes**. The **Qwen 3.5/3.6 family** dominates the landscape, with the **HauhauCS/Qwen3.6-35B-A3B-Uncensored** variant exploding to over 3.2 million downloads, signaling intense community interest in uncensored multimodal models. NVIDIA continues to push quantization boundaries with its **NVFP4** precision format, applied to both **GLM-5.2** and **Qwen3.6-35B-A3B**, suggesting that 4-bit floating-point quantization is becoming a production standard. The **DeepSeek V4** family makes its debut with two new "DSpark" variants, while **Gemma 4** based fine-tunes—particularly the "Fable" series—are seeing a surge in popularity for coding and agentic tasks. Notably, **nvidia/LocateAnything-3B** is a standout for vision-language grounding, and **baidu/Unlimited-OCR** is an enterprise-level OCR model with strong traction.

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2**  
  Author: zai-org | Likes: 2,821 | Downloads: 118,651  
  A powerful Mixture-of-Experts (MoE) text-generation model from the GLM family, trending due to its efficient architecture and strong conversational abilities.

- **deepseek-ai/DeepSeek-V4-Pro-DSpark**  
  Author: deepseek-ai | Likes: 182 | Downloads: 373  
  The new flagship from DeepSeek, featuring a "DSpark" optimization for high-performance inference; early release is generating significant research interest.

- **WeiboAI/VibeThinker-3B**  
  Author: WeiboAI | Likes: 744 | Downloads: 59,337  
  A compact 3B model fine-tuned for mathematical reasoning, popular for its strong performance-to-size ratio.

- **microsoft/FastContext-1.0-4B-SFT**  
  Author: microsoft | Likes: 369 | Downloads: 6,779  
  A Qwen 3-based 4B model optimized for long-context understanding and sub-agent exploration, reflecting Microsoft's focus on agentic workflows.

- **deepreinforce-ai/Ornith-1.0-397B**  
  Author: deepreinforce-ai | Likes: 147 | Downloads: 1,116  
  The largest Ornith model (397B parameters), a MoE architecture built on Qwen 3.5, gaining attention for its scale and MIT licensing.

- **LiquidAI/LFM2.5-230M**  
  Author: LiquidAI | Likes: 140 | Downloads: 12,384  
  A tiny 230M parameter LFM (Liquid Foundation Model) optimized for efficiency, trending as a benchmark for small-model research.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **baidu/Unlimited-OCR**  
  Author: baidu | Likes: 1,242 | Downloads: 295,064  
  An enterprise-grade image-text-to-text model for unlimited OCR scenarios, trending due to its high accuracy and Baidu’s backing.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M** (and GGUF variant)  
  Author: empero-ai | Likes: 803 | Downloads: 831,529  
  A multimodal reasoning model based on Qwen 3.5, combining Claude-style storytelling with vision; the GGUF format is driving massive downloads.

- **nvidia/LocateAnything-3B**  
  Author: nvidia | Likes: 2,436 | Downloads: 646,451  
  A groundbreaking 3B model for zero-shot object localization and image feature extraction, trending for its accuracy and NVIDIA’s reputation.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
  Author: HauhauCS | Likes: 2,302 | Downloads: 3,248,724  
  An uncensored, aggressive variant of Qwen 3.6 with vision capabilities; the top-downloaded model this week, driven by demand for unrestricted multimodal content.

- **nvidia/nemotron-3.5-asr-streaming-0.6b**  
  Author: nvidia | Likes: 734 | Downloads: 67,419  
  A streaming automatic speech recognition (ASR) model optimized for low-latency real-time applications.

- **krea/Krea-2-Turbo** (and Krea-2-Raw)  
  Author: krea | Likes: 355 | Downloads: 27,631  
  State-of-the-art text-to-image diffusion models from Krea, with the Turbo variant offering faster inference while maintaining quality.

- **fal/LTX-2.3-3DREAL-LoRA**  
  Author: fal | Likes: 95 | Downloads: 0  
  A LoRA adapter for the LTX-2.3 video model, enabling photorealistic 3D-aware video generation; early release with high future potential.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **nvidia/GLM-5.2-NVFP4**  
  Author: nvidia | Likes: 155 | Downloads: 45,762  
  A 4-bit floating-point (NVFP4) quantized version of GLM-5.2, specialized for high-efficiency inference on NVIDIA hardware.

- **deepreinforce-ai/Ornith-1.0-9B-GGUF**  
  Author: deepreinforce-ai | Likes: 274 | Downloads: 36,846  
  A compact 9B Ornith variant in GGUF format, optimized for code generation and general reasoning tasks.

- **Chunjiang-Intelligence/DeepSeek-v4-Fable**  
  Author: Chunjiang-Intelligence | Likes: 124 | Downloads: 1,409  
  A fine-tune of DeepSeek V4 focused on cybersecurity applications, indicating growing interest in domain-specific safety models.

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**  
  Author: yuxinlu1 | Likes: 2,473 | Downloads: 549,926  
  A Gemma 4-based coder fine-tune using the Fable5 & Composer 2.5 recipe, extremely popular for agentic coding workflows in terminal environments.

- **Comfy-Org/Krea-2**  
  Author: Comfy-Org | Likes: 177 | Downloads: 10  
  A ComfyUI-specific packaging of the Krea-2 image model, enabling high-quality text-to-image directly in the ComfyUI node-based editor.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **unsloth/GLM-5.2-GGUF**  
  Author: unsloth | Likes: 443 | Downloads: 146,023  
  A highly optimized GGUF quantized version of GLM-5.2 from Unsloth, trending for its fast inference and low memory footprint.

- **HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced**  
  Author: HauhauCS | Likes: 100 | Downloads: 40,820  
  A carefully balanced, uncensored fine-tune of Gemma 4 12B using Quantization-Aware Training (QAT), popular for multimodal uncensored use cases.

- **nvidia/Qwen3.6-35B-A3B-NVFP4**  
  Author: nvidia | Likes: 371 | Downloads: 5,235,413  
  The most downloaded model overall this week; a 35B-parameter MoE model from Qwen 3.6 compressed with NVIDIA’s NVFP4 quantization, enabling high-quality inference on consumer GPUs.

- **unsloth/Qwen-AgentWorld-35B-A3B-GGUF**  
  Author: unsloth | Likes: 95 | Downloads: 79,503  
  A GGUF version of the Qwen AgentWorld model, integrating world-model simulation with LLM reasoning, popular for agent research.

### 3. Ecosystem Signal

The ecosystem is currently defined by **three converging trends**: the dominance of **quantized MoE models**, the rise of **uncensored and "aggressive" fine-tunes**, and the **commoditization of multimodal generation**. The **Qwen 3.x family** (3.5, 3.6, AgentWorld) has become the go-to base architecture for the community, with variants spanning from 230M to 397B parameters. **NVIDIA’s NVFP4 quantization** is emerging as a critical format for enterprise deployment, enabling high-performance inference for massive models (e.g., Qwen3.6-35B) on single GPUs—this is a direct response to the need for local, private inference. The **"Fable" and "Mythos" fine-tuning recipes** (epitomized by the Gemma 4 and Qwythos series) represent a new trend: using synthetic, narrative-rich data to imbue models with specific agentic or creative personas. Open-weight models (particularly MIT-licensed ones like Ornith-1.0) are gaining ground on proprietary systems, driven by community trust and transparency. However, the explosive popularity of uncensored models (e.g., HauhauCS’s Qwen3.6 uncensored variant) signals a growing user demand for low-restriction models, despite potential safety concerns. Finally, the **GGUF** format remains the king of accessibility, with nearly all trending models offering a GGUF variant—this is the default path for local deployment via llama.cpp and its derivatives.

### 4. Worth Exploring

1.  **nvidia/LocateAnything-3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B))  
    This model is a breakthrough in zero-shot visual grounding. Its ability to locate any object in an image without prior training makes it indispensable for robotics, drone navigation, and automated inspection. At just 3B parameters, it is surprisingly efficient and runs well on mid-range hardware.

2.  **nvidia/Qwen3.6-35B-A3B-NVFP4** ([link](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4))  
    With over 5 million downloads, this is arguably the most practical large-scale model on the hub. Its 35B-parameter MoE architecture compressed to 4-bit floating point (NVFP4) fits on a single consumer GPU (e.g., RTX 4090) while retaining near full precision quality. It is the ideal starting point for anyone wanting to run a frontier-level LLM locally.

3.  **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))  
    This model exemplifies the new wave of agentic coding LLMs. It combines the strong Gemma 4 base with a narrative fine-tuning approach (Fable5 + Composer 2.5) that makes it particularly effective at understanding complex, terminal-based coding tasks. It is a must-try for developers building autonomous coding agents.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*