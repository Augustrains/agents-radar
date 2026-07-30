# Hugging Face Trending Models Digest 2026-07-30

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-30 01:13 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-30**.

---

### 1. Today’s Highlights

The Hugging Face ecosystem this week is dominated by a surge in **multimodal MoE (Mixture of Experts)** architectures, led by **moonshotai/Kimi-K3**—which rocketed to over 8,600 likes—and the powerful **Qwen3.6-35B-A3B** from Alibaba, which has accumulated over 6 million downloads. The **Uncensored** niche continues to be a major driver of community downloads, with models like **HauhauCS/Qwen3.6-35B-A3B-Uncensored** crossing 1.8 million pulls. Quantization remains the primary distribution channel, with GGUF variants of flagship models (Laguna-S-2.1, Kimi-K3, Qwen3.6) seeing the most rapid adoption by local inference users. Meanwhile, Microsoft is quietly pushing the frontier with **Fara1.5-27B** (computer-use vision) and **Mage-VL**, signaling a corporate shift toward applied multimodal agents.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **poolside/Laguna-S-2.1**  
  *Author:* poolside | *Likes:* 827 | *Downloads:* 67,286  
  A state-of-the-art text-generation model optimized for enterprise code synthesis and reasoning, trending due to its strong benchmark scores and availability in GGUF format.

- **upstage/Solar-Open2-250B**  
  *Author:* upstage | *Likes:* 694 | *Downloads:* 4,804  
  An open-weight, 250-billion-parameter flagship LLM rivaling proprietary frontier models, gaining traction for its permissive licensing and strong multilingual performance.

- **zai-org/GLM-5.2**  
  *Author:* zai-org | *Likes:* 4,641 | *Downloads:* 1,267,198  
  A conversational, high-efficiency MoE model designed for long-context dialogue, trending as the highest-downloaded LLM after quantization variants.

- **Nanbeige/Nanbeige4.2-3B**  
  *Author:* Nanbeige | *Likes:* 554 | *Downloads:* 18,933  
  A compact 3B parameter text-generation model optimized for edge deployment, gaining popularity for its surprisingly strong reasoning-to-size ratio.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **moonshotai/Kimi-K3**  
  *Author:* moonshotai | *Likes:* 8,647 | *Downloads:* 99,214  
  A cutting-edge image-text-to-text vision-language model with compressed-tensors, trending as the week's #1 model by likes for its advanced multimodal reasoning.

- **baidu/Unlimited-OCR**  
  *Author:* baidu | *Likes:* 3,516 | *Downloads:* 2,694,935  
  A transformer-based OCR model with near-perfect accuracy on complex layouts, trending due to massive demand for document digitization workflows.

- **thinkingmachines/Inkling**  
  *Author:* thinkingmachines | *Likes:* 1,640 | *Downloads:* 39,052  
  A conversational multimodal model optimized for visual question-answering and diagram understanding, gaining attention for enterprise documentation use.

- **owensong/Inflect-Micro-v2** & **Inflect-Nano-v2**  
  *Author:* owensong | *Likes:* 290 & 111 | *Downloads:* 645  
  Ultra-lightweight text-to-speech models designed for CPU and edge-AI inference, trending in the open-source TTS community for their low latency.

- **microsoft/VibeVoice-ASR-BitNet**  
  *Author:* microsoft | *Likes:* 100 | *Downloads:* 1,754  
  A 1-bit quantized automatic speech recognition model using the BitNet architecture, notable for extreme compression while maintaining transcription quality.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **Kwaipilot/KAT-Coder-V2.5-Dev**  
  *Author:* Kwaipilot | *Likes:* 316 | *Downloads:* 6,275  
  A MoE code generation model based on Qwen3.5, trending among developers for its ability to handle multi-file codebase tasks and agentic code editing.

- **microsoft/Fara1.5-27B**  
  *Author:* microsoft | *Likes:* 200 | *Downloads:* 1,543  
  A vision-language model optimized for computer-use agent tasks (GUI navigation, screen parsing), gaining momentum as the "operator agent" space heats up.

- **ATH-MaaS/OvisOCR2**  
  *Author:* ATH-MaaS | *Likes:* 346 | *Downloads:* 47,129  
  A specialized OCR model built on Qwen3.5, trending for its support of multi-script and handwritten text extraction.

- **fdtn-ai/antares-1b**  
  *Author:* fdtn-ai | *Likes:* 231 | *Downloads:* 7,666  
  A 1B parameter security-focused LLM using GraniteMoE, designed for vulnerability analysis and code audit, trending in the cybersecurity ML community.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**  
  *Author:* DavidAU | *Likes:* 942 | *Downloads:* 736,692  
  A heavily fine-tuned, uncensored Qwen3.6 variant in GGUF, popular among role-playing and creative writing communities for its "jailbroken" behavior and high context retention.

- **unsloth/Kimi-K3-GGUF**  
  *Author:* unsloth | *Likes:* 160 | *Downloads:* 0  
  The official GGUF quantization of Kimi-K3 by Unsloth, positioned for immediate local inference on consumer hardware.

- **prism-ml/Ternary-Bonsai-27B-gguf** & **Bonsai-27B-gguf**  
  *Author:* prism-ml | *Likes:* 1,095 & 688 | *Downloads:* 665K & 2.3M  
  A pair of 27B models quantized to 2-bit and 1-bit (ternary) respectively, trending as the most extreme compression experiments that still retain coherent reasoning.

- **LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**  
  *Author:* LuffyTheFox | *Likes:* 215 | *Downloads:* 99,660  
  An uncensored, Hermes-style fine-tune of the Qwen3.6 MoE model, widely downloaded for unrestricted creative generation.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**  
  *Author:* empero-ai | *Likes:* 2,516 | *Downloads:* 1,262,662  
  A role-play focused fine-tune (Mythos series) of Qwen3.5, extremely popular in the "uncensored storytelling" niche with over 1M downloads.

### 3. Ecosystem Signal

The ecosystem is undergoing a clear **MoE (Mixture of Experts) inflection**: models like Qwen3.6-35B-A3B, GLM-5.2, and Kimi-K3 all employ sparse activation, allowing high parameter counts with manageable inference costs. This hardware-efficiency is driving the **GGUF quantization explosion**—nearly 40% of trending models are GGUF variants, often exceeding the likes of their base model. The **Uncensored/Heretic** sub-community remains incredibly active, generating hundreds of thousands of downloads per variant, signaling strong demand for unrestricted, role-play capable models. On the corporate side, Microsoft and Baidu are pushing **computer-use and OCR pipelines** (Fara1.5, Unlimited-OCR), suggesting the next frontier is agentic vision tasks. Finally, extreme quantization (1-bit Bonsai, BitNet-based ASR) is no longer a curiosity—prism-ml’s 1-bit 27B model has over 2 million downloads, proving the market is ready for ultra-low-precision production models on consumer edge devices.

### 4. Worth Exploring

- **moonshotai/Kimi-K3** — The week’s highest-liked model. Worth studying for its compressed-tensor VLM architecture and how Moonshot balances multimodal understanding with parameter efficiency. Likely the blueprint for next-generation vision-language agents.

- **unsloth/Kimi-K3-GGUF** — The quantized version of the above. Ideal for local experimentation on consumer GPUs (24GB VRAM). A must-try for anyone wanting to run a top-tier VLM without cloud dependency.

- **microsoft/Mage-VL** — A relatively low-profile release with only 98 likes, but it represents Microsoft’s latest multimodal foundation model. Worth exploring for the architecture’s novel attention mechanisms and potential as a base for fine-tuning in agentic GUI tasks.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*