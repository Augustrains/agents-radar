# Hugging Face Trending Models Digest 2026-06-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-06 08:20 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-06

## 1. Today's Highlights

**DeepSeek-V4-Pro** dominates the week with 4,664 likes and 5.5M downloads, cementing DeepSeek's leadership in open-weight reasoning models. NVIDIA continues its aggressive multi-model strategy, releasing **LocateAnything-3B** (1,399 likes) for spatial grounding and the **Cosmos3** series spanning text-to-image, image-to-video, and omnimodal pipelines. The community is buzzing over **Sulphur-2-base** (1,569 likes), a text-to-video model built on LTX-2.3, signalling rapid maturation of open video generation. Quantized variants are flooding the hub—**unsloth/gemma-4-12b-it-GGUF** and **Qwen3.6-27B-MTP-GGUF** each surpassed 1M downloads, reflecting strong demand for accessible, runnable LLMs.

---

## 2. Trending Models by Category

### 🧠 Language Models

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|------------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,664 | 5,510,611 | Flagship 1.8T MoE reasoning model; top-liked and most-downloaded model this week |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,415 | 3,436,213 | Faster, cheaper variant of V4-Pro with MIT license; huge adoption for inference |
| [JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking) | JetBrains | 227 | 16,395 | Code-aware thinking model; signals JetBrains' push into developer AI |
| [LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B) | LiquidAI | 529 | 95,440 | Liquid Foundation Model 2.5 with 1B active params; strong efficiency-to-quality ratio |
| [sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B) | sapientinc | 702 | 161,627 | 1B-parameter human resource management text generator; niche enterprise LLM gaining traction |
| [openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B) | openbmb | 772 | 100,575 | Compact 1B model with Llama architecture; popular for on-device or resource-constrained deployment |
| [stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash) | stepfun-ai | 337 | 38,716 | Fast vision-language model; competitive with Gemini-style VLMs |
| [nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16) | nvidia | 125 | 47,285 | 550B MoE flagship (55B active); NVIDIA's largest open-weight model |
| [nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 112 | 17,225 | FP4 quantized version of the Nemotron 3 Ultra; extreme compression for 550B model |

### 🎨 Multimodal & Generation

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|------------------|
| [Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) | SulphurAI | 1,569 | 1,704,964 | Text-to-video diffusion model based on LTX-2.3; top video generation model this week |
| [ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8) | ideogram-ai | 279 | 2,818 | FP8 quantized version of Ideogram 4; high-quality text-to-image with reduced memory |
| [ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4) | ideogram-ai | 199 | 2,671 | NF4 quantized variant of Ideogram 4; further compression for consumer GPUs |
| [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 1,399 | 111,078 | 3B spatial grounding model; excels at object localization from text prompts |
| [nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano) | nvidia | 177 | 24,820 | Smallest model in the Cosmos3 omnimodal family; fast generation across modalities |
| [nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super) | nvidia | 144 | 20,403 | Premium omnimodal model in Cosmos3 series; strong across text, image, video |
| [nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image) | nvidia | 117 | 1,634 | Specialized text-to-image from Cosmos3 Super family |
| [nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video) | nvidia | 107 | 1,295 | Image-to-video generation using Cosmos3 architecture |
| [ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R) | ByteDance | 143 | 223 | New image-text-to-video renderer; Apache-2.0 licensed, research-stage |
| [meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5) | meituan-longcat | 522 | 1,806 | Audio+text-to-video avatar model; multimodal talking head generation |
| [PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6) | PaddlePaddle | 246 | 8,365 | Vision-language OCR model; leverages ERNIE 4.5 backbone |
| [nvidia/PiD](https://huggingface.co/nvidia/PiD) | nvidia | 310 | 972 | Super-resolution image-to-image diffusion model; NVIDIA quality with 2×-4× upscaling |
| [google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) | google | 568 | 315,131 | Google's latest any-to-any VLM; strong multimodal reasoning with 12B params |
| [google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B) | google | 348 | 84,549 | Base variant of Gemma 4 without instruction tuning; for fine-tuning |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,461 | 2,771,843 | Uncensored, aggressive-tuned Qwen3.6 MoE with vision; controversial but highly downloaded |
| [stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash) | stepfun-ai | 337 | 38,716 | Fast vision-language model; competitive with Gemini-style VLMs |
| [nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4) | nvidia | 193 | 1,015,381 | FP4 quantized Qwen3.6 MoE; extreme compression for 35B total / 3B active model |

### 🔧 Specialized Models

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|------------------|
| [nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 200 | 1,380 | Streaming automatic speech recognition; cache-aware for low-latency deployment |
| [bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 130 | 2,184 | 4B-parameter TTS model built on Qwen3 multimodal backbone |
| [MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS) | MisoLabs | 112 | 0 | New TTS entry; zero downloads suggests very recent release |

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|------------------|
| [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 389 | 458,174 | GGUF quantization of Gemma 4 12B; enables local inference on consumer hardware |
| [unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF) | unsloth | 667 | 1,122,805 | GGUF of Qwen3.6 27B with Multi-Turn Prediction; popular for chat applications |
| [nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4) | nvidia | 193 | 1,015,381 | NVIDIA's NVFP4 quantization of Qwen3.6 MoE; state-of-the-art 4-bit for MoE |
| [nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 112 | 17,225 | FP4 variant of the 550B Nemotron; pushing quantization boundaries for frontier models |

---

## 3. Ecosystem Signal

**DeepSeek dominates, but the MoE race is real.** DeepSeek-V4-Pro and V4-Flash together account for over 6K likes and 9M downloads, indicating strong community validation of 1.8T MoE architecture at scale. NVIDIA is running a parallel playbook—releasing Nemotron-3-Ultra (550B MoE) alongside quantized variants (NVFP4) and specialized models (Cosmos3, PiD, LocateAnything), effectively covering logic, vision, and compression. The quantized model ecosystem is exploding: **Unsloth** emerged as the primary quantization partner for Google and Alibaba models (Gemma-4, Qwen3.6), each racking 500K+ downloads. Open-weight remains the dominant paradigm—no proprietary black-box models appear on the list. Notably, **Sulphur-2-base** (text-to-video) signals video generation is reaching mainstream accessibility, while **Bernini-R** (ByteDance) and **LongCat-Video-Avatar-1.5** (Meituan) show that Chinese companies are aggressively pushing video and avatar models.

---

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A 3B model that pinpoints objects in images from natural language descriptions. Highly practical for robotics, visual QA, and document analysis. The 111K downloads in one week with 1.4K likes suggest it fills a clear gap in spatial understanding.

2. **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — Built on LTX-2.3, this text-to-video diffusion model is rapidly gaining community traction. At 1.7M downloads and 1.5K likes, it's the most popular open video gen model this cycle and worth studying for prompt-to-video pipelines.

3. **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — A 1B-parameter Llama-architecture model with 772 likes. It punches far above its weight class and serves as a reference point for small-model capabilities, making it ideal for mobile or edge deployment studies.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*