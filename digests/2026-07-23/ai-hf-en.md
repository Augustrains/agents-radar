# Hugging Face Trending Models Digest 2026-07-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-23 01:26 UTC

---

# Hugging Face Trending Models Digest — 2026-07-23

## Today's Highlights

This week's trending models reveal a clear shift toward **extreme quantization** and **multimodal fusion**. The explosive popularity of `zai-org/GLM-5.2` (4,336 likes) and `google/gemma-4-31B-it` (3,328 likes) signals strong community interest in powerful open-weight LLMs with strong conversational capabilities. Meanwhile, prism-ml's "Bonsai" family—pushing 1-bit and 2-bit quantization—has amassed over 1.8M total downloads, showing that **ultra-low-bit inference is no longer experimental but production-ready**. On the multimodal front, OCR and vision-language models dominate, with **baidu/Unlimited-OCR** leading downloads at 2.2M and several Qwen3.6-based vision models appearing across the top 30. The ecosystem also sees notable activity in **robotics** (two MiniCPM models from openbmb) and **streaming ASR** (nvidia/nemotron-3.5-asr), broadening the hub's scope beyond pure text generation.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2))  
  *Author: zai-org | Likes: 4,336 | Downloads: 545,109*  
  A state-of-the-art MoE-based conversational model with 5.2B active parameters, trending as the week's most-liked model due to its combination of high performance and accessible size.

- **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it))  
  *Author: google | Likes: 3,328 | Downloads: 12,113,203*  
  Google's latest instruction-tuned multilingual vision-language model, dominating downloads this week as the go-to open-weight alternative for multimodal chat applications.

- **upstage/Solar-Open2-250B** ([link](https://huggingface.co/upstage/Solar-Open2-250B))  
  *Author: upstage | Likes: 251 | Downloads: 0*  
  A massive 250B-parameter open-weight LLM from Upstage, generating interest despite zero downloads due to its scale and the trend toward extremely large open models.

- **Nanbeige/Nanbeige4.2-3B** ([link](https://huggingface.co/Nanbeige/Nanbeige4.2-3B))  
  *Author: Nanbeige | Likes: 231 | Downloads: 0*  
  A compact 3B-parameter LLM optimized for efficient deployment, trending for its potential as a lightweight alternative in resource-constrained settings.

- **Motif-Technologies/Motif-3-Beta** ([link](https://huggingface.co/Motif-Technologies/Motif-3-Beta))  
  *Author: Motif-Technologies | Likes: 159 | Downloads: 125*  
  A feature-extraction focused model from Motif Technologies, gaining attention for enterprise NLP use cases.

- **poolside/Laguna-S-2.1** ([link](https://huggingface.co/poolside/Laguna-S-2.1))  
  *Author: poolside | Likes: 392 | Downloads: 3,056*  
  A text-generation model from poolside, notable as the base model spawning multiple quantization variants (GGUF, NVFP4) in this week's top 30.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **baidu/Unlimited-OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR))  
  *Author: baidu | Likes: 2,712 | Downloads: 2,237,351*  
  A high-accuracy multimodal OCR model from Baidu, trending due to its massive download count and utility for document digitization workflows.

- **thinkhmachines/Inkling** ([link](https://huggingface.co/thinkingmachines/Inkling))  
  *Author: thinkingmachines | Likes: 1,449 | Downloads: 16,441*  
  A multimodal MoE model supporting image-text-to-text and conversational pipelines, gaining traction as a versatile vision-language assistant.

- **moonshotai/Kimi-K2.7-Code** ([link](https://huggingface.co/moonshotai/Kimi-K2.7-Code))  
  *Author: moonshotai | Likes: 1,223 | Downloads: 722,058*  
  A compressed code-focused vision-language model from Moonshot AI, trending for its ability to understand and generate code from visual inputs.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))  
  *Author: nvidia | Likes: 914 | Downloads: 590,230*  
  A compact 0.6B streaming ASR model from NVIDIA using NeMo, trending for real-time speech recognition in edge deployments.

- **conradlocke/krea2-identity-edit** ([link](https://huggingface.co/conradlocke/krea2-identity-edit))  
  *Author: conradlocke | Likes: 495 | Downloads: 0*  
  A LoRA for identity-preserving image editing built on Krea-2, gaining interest despite zero downloads for its potential in face-editing workflows.

- **OpenMOSS-Team/MOSS-Transcribe-Diarize** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize))  
  *Author: OpenMOSS-Team | Likes: 308 | Downloads: 92,265*  
  An audio-text-to-text model combining transcription with speaker diarization, trending for its practical application in meeting analysis.

- **ATH-MaaS/OvisOCR2** ([link](https://huggingface.co/ATH-MaaS/OvisOCR2))  
  *Author: ATH-MaaS | Likes: 249 | Downloads: 17,162*  
  A Qwen3.5-based OCR model optimized for visual document understanding, competing with Baidu's Unlimited-OCR in the OCR niche.

- **microsoft/Mage-Flow** ([link](https://huggingface.co/microsoft/Mage-Flow))  
  *Author: microsoft | Likes: 124 | Downloads: 0*  
  A diffusion-based text-to-image model from Microsoft with editing capabilities, trending as a fresh entrant in the image generation space.

- **nvidia/Cosmos3-Edge** ([link](https://huggingface.co/nvidia/Cosmos3-Edge))  
  *Author: nvidia | Likes: 89 | Downloads: 6,623*  
  A diffusion model from NVIDIA's Cosmos3 series, gaining attention for edge-device image generation.

- **Alissonerdx/LTX-Best-Face-ID** ([link](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID))  
  *Author: Alissonerdx | Likes: 235 | Downloads: 0*  
  An identity-preserving LoRA for text-to-video generation using LTX-Video, trending for its application in personalized video creation.

- **openbmb/MiniCPM-RobotManip** ([link](https://huggingface.co/openbmb/MiniCPM-RobotManip))  
  *Author: openbmb | Likes: 154 | Downloads: 58*  
  A vision-language-action model for robotic manipulation, representing a new robotics pipeline category on Hugging Face.

- **openbmb/MiniCPM-RobotTrack** ([link](https://huggingface.co/openbmb/MiniCPM-RobotTrack))  
  *Author: openbmb | Likes: 114 | Downloads: 72*  
  A companion model to RobotManip, focusing on object tracking in robotic vision-language-action systems.

- **bottlecapai/ThinkingCap-Qwen3.6-27B** ([link](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B))  
  *Author: bottlecapai | Likes: 512 | Downloads: 12,002*  
  A Qwen3.6-based vision-language model optimized for reasoning tasks, gaining traction for its "thinking" capabilities.

### 🔧 Specialized Models (code, math, medical, embeddings)

*(No dedicated code/math/medical/embedding models appeared in this week's top 30 beyond the multimodal code model Kimi-K2.7-Code listed above.)*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
  *Author: HauhauCS | Likes: 3,000 | Downloads: 1,997,690*  
  An uncensored, aggressive fine-tune of Qwen3.6-35B in GGUF format with MoE architecture, trending for its high download volume and controversial uncensored nature.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))  
  *Author: empero-ai | Likes: 2,416 | Downloads: 2,133,420*  
  A Qwen3.5-based reasoning model distilled from Claude data, quantized to GGUF, trending for its strong performance in chain-of-thought tasks.

- **prism-ml/Ternary-Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf))  
  *Author: prism-ml | Likes: 941 | Downloads: 432,196*  
  A 27B-parameter model compressed to 2-bit ternary precision in GGUF format, pushing the boundaries of extreme quantization while maintaining utility.

- **prism-ml/Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Bonsai-27B-gguf))  
  *Author: prism-ml | Likes: 595 | Downloads: 1,404,962*  
  A 1-bit quantized version of the Bonsai-27B model, the week's most popular among extreme quantization enthusiasts with over 1.4M downloads.

- **prism-ml/Bonsai-27B-mlx-1bit** ([link](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit))  
  *Author: prism-ml | Likes: 165 | Downloads: 25,273*  
  An Apple MLX-compatible 1-bit version of Bonsai-27B, extending extreme quantization to Apple Silicon users.

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** ([link](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF))  
  *Author: DavidAU | Likes: 321 | Downloads: 62,842*  
  An experimental uncensored multimodal fine-tune of Qwen3.6-27B in GGUF format, trending for its provocative naming and specialized niche.

- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF** ([link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF))  
  *Author: GnLOLot | Likes: 153 | Downloads: 51,746*  
  A 1B-parameter MiniCPM5-based reasoning model distilled from Claude Opus data, showcasing how tiny models can learn complex thinking patterns.

- **unsloth/inkling-GGUF** ([link](https://huggingface.co/unsloth/inkling-GGUF))  
  *Author: unsloth | Likes: 120 | Downloads: 7,377*  
  A GGUF quantization of the Inkling multimodal MoE model by unsloth, enabling efficient local deployment of a multimodal assistant.

- **unsloth/Laguna-S-2.1-GGUF** ([link](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF))  
  *Author: unsloth | Likes: 106 | Downloads: 0*  
  A GGUF quantized version of poolside's Laguna-S-2.1, optimized for vLLM inference with Unsloth's efficient quantization tools.

- **poolside/Laguna-S-2.1-NVFP4** ([link](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4))  
  *Author: poolside | Likes: 91 | Downloads: 1,953*  
  An NVFP4 (NVIDIA FP4) quantized variant of Laguna-S-2.1, exploring NVIDIA's native 4-bit precision format for Hopper GPUs.

- **poolside/Laguna-S-2.1-GGUF** ([link](https://huggingface.co/poolside/Laguna-S-2.1-GGUF))  
  *Author: poolside | Likes: 91 | Downloads: 289*  
  The official GGUF release of Laguna-S-2.1 from poolside, providing a baseline for community quantization efforts.

---

## Ecosystem Signal

**Three trends dominate this week's ecosystem:**

1. **Extreme quantization has gone mainstream.** prism-ml's Bonsai series—spanning 1-bit, 2-bit (Ternary), and MLX formats—has collectively amassed nearly 2M downloads, proving that users are willing to trade quality for the ability to run 27B models on consumer hardware. This signals a maturation of ultra-low-bit inference techniques where "good enough" quality meets accessibility.

2. **Multimodal MoE is the new frontier.** The success of Inkling (multimodal MoE), GLM-5.2 (MoE-based LLM), and HauhauCS's Qwen3.6 MoE variant shows that Mixture-of-Experts architectures are becoming the default for efficient multimodal models. The trend toward "thinking" or reasoning-capable vision models (ThinkingCap, Qwythos) suggests the next battleground will be multimodal reasoning, not just generation.

3. **Open-weight leadership is consolidating around Qwen and Gemma.** Qwen-derived models appear in 7 of the top 30 entries (across Qwen3.5, 3.6, and fine-tunes), while Gemma-4-31B-it leads all models in absolute downloads at 12M. Google and Alibaba's open-weight strategies are effectively decentralizing the model ecosystem away from proprietary APIs, though fine-tuning creativity remains community-driven.

4. **Robotics enters the Hub.** openbmb's MiniCPM-RobotManip and MiniCPM-RobotTrack are early indicators that vision-language-action (VLA) models are transitioning from research to reproducible assets on Hugging Face. This could be the beginning of a new model category analogous to the 2023 explosion of LoRA fine-tunes.

---

## Worth Exploring

1. **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it)) — With 12M downloads in its first week, this is the most consequential multimodal model release this period. It establishes a new baseline for open-weight vision-language chat, and its multilingual capabilities make it suitable for global deployment. Practitioners should evaluate it as a replacement for proprietary multimodal APIs.

2. **prism-ml/Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Bonsai-27B-gguf)) — At 1-bit quantization, this model challenges assumptions about what compression can achieve. It's worth studying for engineers working on edge deployment or on-device LLMs who need to fit large models into memory constraints. The fact that it maintains conversational utility at 1-bit is technically remarkable.

3. **openbmb/MiniCPM-RobotManip** ([link](https://huggingface.co/openbmb/MiniCPM-RobotManip)) — This is a signal of where the ecosystem is heading. The robotics pipeline on Hugging Face is nascent, and early adopters who build infrastructure around VLA models may gain a significant advantage as this category grows.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*