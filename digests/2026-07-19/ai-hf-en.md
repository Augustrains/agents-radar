# Hugging Face Trending Models Digest 2026-07-19

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-19 01:20 UTC

---

Here is the structured Hugging Face Trending Models Digest for July 19, 2026.

---

## Hugging Face Trending Models Digest – 2026-07-19

### 1. Today's Highlights

The hub is dominated by **extreme quantization and MoE architectures**, with the **zai-org/GLM-5.2** and **google/gemma-4-31B-it** leading in likes, while **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** and **HauhauCS/Qwen3.6-35B-A3B-Uncensored** break 2M downloads each. The **Prism ML** ecosystem continues to expand its "Bonsai" 1-bit and ternary quantization lines, now available in both GGUF and MLX formats, signaling a strong push toward edge and Apple Silicon deployment. Multimodal is the clear theme: vision-language models (Qwen3.5/3.6 derivatives) and new OCR entries like **baidu/Unlimited-OCR** are seeing explosive adoption. Notably, the **froggeric/Qwen-Fixed-Chat-Templates** repository, with zero downloads but 941 likes, highlights a growing community demand for proper chat template standardization.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) — Author: zai-org | Likes: 4,126 | Downloads: 541,662  
  A flagship MoE-DSA model with strong conversational performance; trending as the leading Chinese-origin LLM on the hub.

- **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it)) — Author: google | Likes: 3,263 | Downloads: 12,608,008  
  Google's latest instruction-tuned multimodal LLM; massive download count reflects its accessibility and strong benchmark performance.

- **tencent/Hy3** ([link](https://huggingface.co/tencent/Hy3)) — Author: tencent | Likes: 829 | Downloads: 13,571  
  The Hunyuan v3 base model; gaining traction as a general-purpose text-generation backbone.

- **InternScience/Agents-A1** ([link](https://huggingface.co/InternScience/Agents-A1)) — Author: InternScience | Likes: 579 | Downloads: 35,575  
  A Qwen3.5-MoE model optimized for agentic tool use; trending due to rising interest in LLM-based agent frameworks.

- **bottlecapai/ThinkingCap-Qwen3.6-27B** ([link](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)) — Author: bottlecapai | Likes: 437 | Downloads: 10,445  
  A reasoning-enhanced Qwen3.6 variant; popular for combining chain-of-thought with vision-language capabilities.

- **Cactus-Compute/needle** ([link](https://huggingface.co/Cactus-Compute/needle)) — Author: Cactus-Compute | Likes: 268 | Downloads: 935  
  A JAX-native model specialized for function-calling and tool-use; notable for its novel architecture and small but engaged niche.

- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF** ([link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)) — Author: GnLOLot | Likes: 277 | Downloads: 172,409  
  A heavily fine-tuned 1B reasoning model showing that small models with strong thinking capabilities can achieve high adoption.

- **prism-ml/Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Bonsai-27B-gguf)) — Author: prism-ml | Likes: 444 | Downloads: 1,218,815  
  A pioneer in 1-bit quantization; its massive download count indicates strong demand for ultra-low-bit models on consumer hardware.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) — Author: empero-ai | Likes: 2,315 | Downloads: 2,112,869  
  A Qwen3.5-based vision-language model with reasoning features; extremely high downloads suggest it is a go-to for local multimodal inference.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) — Author: HauhauCS | Likes: 2,865 | Downloads: 2,190,398  
  An uncensored MoE vision model based on Qwen3.6; trending due to demand for less restricted multimodal models.

- **baidu/Unlimited-OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR)) — Author: baidu | Likes: 2,025 | Downloads: 2,088,470  
  A state-of-the-art OCR model; near-tie with the Qwythos model in downloads shows OCR is a killer app for vision-language models.

- **thinkingmachines/Inkling** ([link](https://huggingface.co/thinkingmachines/Inkling)) — Author: thinkingmachines | Likes: 1,062 | Downloads: 12,456  
  A new multimodal MoE model with image, text, and audio support; early buzz suggests it could become a top-tier unified model.

- **Wan-AI/Wan-Dancer-14B** ([link](https://huggingface.co/Wan-AI/Wan-Dancer-14B)) — Author: Wan-AI | Likes: 114 | Downloads: 2,328  
  An image-to-video diffusion model specialized for dance generation; notable for its domain-specific training.

- **ATH-MaaS/OvisOCR2** ([link](https://huggingface.co/ATH-MaaS/OvisOCR2)) — Author: ATH-MaaS | Likes: 170 | Downloads: 13,750  
  A Qwen3.5-based OCR model; part of a broader trend of fine-tuned vision models for document processing.

- **OpenMOSS-Team/MOSS-Transcribe-Diarize** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)) — Author: OpenMOSS-Team | Likes: 259 | Downloads: 86,385  
  An audio-text-to-text model for transcription and speaker diarization; growing adoption for real-time meeting and call processing.

- **OpenMOSS-Team/MOSS-VL-Realtime** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)) — Author: OpenMOSS-Team | Likes: 76 | Downloads: 529  
  A video-text-to-text model optimized for low-latency streaming; early-stage but signals a push toward real-time multimodal assistants.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **conradlocke/krea2-identity-edit** ([link](https://huggingface.co/conradlocke/krea2-identity-edit)) — Author: conradlocke | Likes: 395 | Downloads: 0  
  A LoRA for identity-consistent image editing on the Krea-2 base model; trending among the iterative editing community.

- **Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt** ([link](https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-CrossView-Prompt)) — Author: Cseti | Likes: 91 | Downloads: 0  
  A LoRA for novel-view video synthesis; highly specialized but gaining attention in the 3D and video generation field.

- **Alissonerdx/LTX-Best-Face-ID** ([link](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)) — Author: Alissonerdx | Likes: 187 | Downloads: 0  
  A reference-to-video LoRA for identity preservation in LTX video models; trending for face-consistent video generation.

- **froggeric/Qwen-Fixed-Chat-Templates** ([link](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)) — Author: froggeric | Likes: 941 | Downloads: 0  
  A community fix for Qwen3.5 chat templates; very high likes for a zero-download utility, reflecting pain in template handling.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **prism-ml/Ternary-Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)) — Author: prism-ml | Likes: 735 | Downloads: 301,893  
  A 2-bit ternary quantization of the Bonsai 27B; leads the pack in novel compression techniques.

- **prism-ml/Bonsai-27B-mlx-1bit** ([link](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)) — Author: prism-ml | Likes: 127 | Downloads: 20,639  
  1-bit MLX variant for Apple Silicon; signals the ecosystem maturing for Mac-based deployment.

- **prism-ml/Ternary-Bonsai-27B-mlx-2bit** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)) — Author: prism-ml | Likes: 111 | Downloads: 17,063  
  Ternary MLX companion; together with the GGUF version, shows a full multi-format quantization family.

- **empero-ai/Qwythos-9B-v2-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)) — Author: empero-ai | Likes: 170 | Downloads: 103,504  
  Updated version of the Qwythos vision model in GGUF; steady downloads suggest ongoing user base.

- **unsloth/inkling-GGUF** ([link](https://huggingface.co/unsloth/inkling-GGUF)) — Author: unsloth | Likes: 96 | Downloads: 6,461  
  Unsloth's GGUF of the new Inkling model; enables efficient local inference for the multimodal MoE model.

- **GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF** ([link](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)) — Author: GnLOLot | Likes: 114 | Downloads: 19,279  
  A GGUF derivative of the 1B thinking model; part of a family of tiny reasoning LLMs.

- **jlnsrk/GLM-5.2-colibri-int4** ([link](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)) — Author: jlnsrk | Likes: 132 | Downloads: 3,869  
  An int4 CPU-optimized version of GLM-5.2 using expert streaming; notable for enabling large MoE on consumer CPUs.

- **AngelSlim/Hy3-GGUF** ([link](https://huggingface.co/AngelSlim/Hy3-GGUF)) — Author: AngelSlim | Likes: 127 | Downloads: 100,768  
  GGUF of Tencent's Hy3; strong downloads indicate Hy3 is becoming a popular base for quantization.

### 3. Ecosystem Signal

Multiple trends are converging. **Extreme quantization (1-bit and ternary)** is no longer experimental—Prism ML's Bonsai family shows repeatable multi-format (GGUF + MLX) deployment, indicating production readiness for consumer GPUs and Apple Silicon. **MoE architectures** are dominant: GLM-5.2, Qwen3.6-MoE, and Inkling all use mixtures of experts, balancing performance with inference cost. **OCR is a breakout application**—two of the top-5 downloaded models are OCR-specific (Baidu's Unlimited-OCR and ATH-MaaS/OvisOCR2), suggesting robust real-world demand. Open-weight models from Google (Gemma-4) and Chinese labs (ZAI, Baidu, Tencent, InternScience) continue to outpace proprietary offerings in community adoption. Finally, **tiny reasoning models** (1B MiniCPM5 variants) are gaining traction, hinting at a new category of "on-device thinking" models for edge and mobile applications.

### 4. Worth Exploring

1. **zai-org/GLM-5.2** — The highest-liked model on the list. Its MoE-DSA architecture represents the cutting edge of hybrid dense/sparse attention, and the ecosystem around it (Colibri int4, diverse quantizations) makes it a strong candidate for production deployment at scale.

2. **thinkingmachines/Inkling** — Newly released but already attracting significant attention. As a unified multimodal MoE supporting image, text, and audio, it could become the next generation of general-purpose assistants. Worth evaluating as a potential successor to Qwen and Gemma families.

3. **prism-ml/Ternary-Bonsai-27B-gguf** — This 2-bit ternary model is a bellwether for the future of local LLMs. With 300K+ downloads and availability across GGUF and MLX, it demonstrates how extreme compression can bring 27B-class performance to laptops and edge devices.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*