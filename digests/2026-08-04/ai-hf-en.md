# Hugging Face Trending Models Digest 2026-08-04

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-04 01:16 UTC

---

# 🤗 Hugging Face Trending Models Digest
**2026-08-04**

---

## 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by **Moonshot AI's Kimi-K3**, which has surged to nearly 10,000 weekly likes as a vision-language model with compressed-tensor support. **DeepSeek-V4-Flash** continues its strong momentum with multiple variants and GGUF quantizations topping download charts alongside the base model. The **Qwen3.5/3.6 MoE family** is clearly the community's favorite base for fine-tuning, spawning numerous uncensored and specialized derivatives. Notably, **MiniMax-H3** has entered the scene as a video-generation model with official and ComfyUI-backed releases generating early buzz. Meanwhile, **baidu/Unlimited-OCR** has quietly amassed over 2.6 million downloads, signaling strong enterprise demand for OCR capabilities.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,057 | 236K | Latest iteration of DeepSeek's efficient flash model with conversational capabilities. |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,990 | 2.7M | The base V4 Flash model, massively downloaded, highlighting DeepSeek's dominance in efficient open-weight LLMs. |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,797 | 2.2M | ZAI's MoE-based GLM iteration with 2.2M downloads, signaling strong enterprise and developer trust. |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 652 | 35K | Compact 3B LLM offering an alternative for edge and resource-constrained deployments. |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 168 | 69K | 250B-scale model quantized to NVFP4 for efficient inference via vLLM. |
| [Instella-MoE-16B-A3B-Think](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 148 | 2K | AMD's MoE model optimized for reasoning, built on DeepSeek-v3 architecture. |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 909 | 82K | Poolside's code-focused LLM with strong adoption, bridging software engineering and general text generation. |
| [Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 444 | 14K | Qwen3.5-MoE-based coding model with multimodal input support. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,848 | 968K | **Trending #1** — Moonshot's vision-language model with compressed-tensor support; a major multimodal release. |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 1,458 | 0 | MiniMax's image-text-to-video generation model — fresh release, zero downloads yet, high community excitement. |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 445 | 2 | Official ComfyUI integration for the MiniMax-H3 video model, enabling local workflow usage. |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,846 | 2.6M | Baidu's powerful OCR model with 2.6M downloads — the most downloaded model this week after DeepSeek. |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 262 | 8.5K | Compact multimodal model for conversational AI with image understanding. |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 231 | 431K | Microsoft's vision-language model with 431K downloads, showing diverse multimodal adoption. |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 159 | 0 | Krea2-based LoRA for text-to-image generation, compatible with ComfyUI. |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 212 | 4.6K | New TTS model with ArkTTS backbone, previewing high-quality speech synthesis. |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 398 | 1.9K | Edge-oriented local TTS model optimized for CPU deployment. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 268 | 3K | Microsoft's Qwen3.5-based model specialized for computer-use and agentic tasks. |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 351 | 1.2K | Agentic-search–tuned model built on Qwen3.5 MoE, pushing retrieval-augmented capabilities. |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 391 | 1K | Compact version of the Aquila series, carrying search-optimized capabilities. |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,430 | 1.6M | Heavily fine-tuned uncensored Qwen3.6 derivative with massive download volume. |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,269 | 1.9M | Community-favorite uncensored MoE with vision support; top-rated community fine-tune. |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 342 | 288K | Hermes-style uncensored fine-tune of Qwen3.6 MoE, well-received with strong downloads. |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 237 | 304K | Another DavidAU uncensored fine-tune, this time on the 9B Qwen3.5 with NEO Imatrix quantization. |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 153 | 2.7K | Weight-compressed (W2) MoE variant of Qwen3.6, optimized for efficiency. |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 428 | 70K | Unsloth's official GGUF quantization of the latest DeepSeek V4 Flash. |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 281 | 128K | GGUF conversion of Kimi-K3 for local running via llama.cpp and friends. |
| [Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot) | ethanfel | 93 | 0 | A niche hybrid fine-tune combining Qwen3-VL architecture with MiniMax-H3 integration and ComfyUI support. |

---

## 3. Ecosystem Signal

Several clear patterns emerge from this week's trending list:

**Qwen (3.5/3.6) is the community's base model of choice.** Over 10 of the 30 trending models are Qwen derivatives — spanning uncensored fine-tunes, MoE variants, and specialized agentic/computer-use adaptations. The Qwen3.6-35B-A3B MoE architecture, in particular, has become the new standard for community experimentation due to its strong performance-to-compute ratio.

**Uncensored fine-tunes remain a massive driver of downloads.** DavidAU, HauhauCS, and LuffyTheFox are consistently producing high-download uncensored variants (1–2M downloads each), indicating sustained demand for less-restricted models. This is a deliberate, ongoing sub-ecosystem within Hugging Face.

**Open-weight flagship releases are accelerating.** DeepSeek-V4-Flash, GLM-5.2, and Kimi-K3 represent three world-class open-weight models from Chinese labs released in rapid succession, each with dedicated GGUF quantization (largely via Unsloth) within days. This indicates a mature open-weight release pipeline.

**Quantization is deeply integrated into the release lifecycle.** Unsloth's GGUF conversions, nota-ai's NVFP4, and EschaLabs' 2-bit weight compression all made the trending list, showing quantization is no longer an afterthought but a first-class deliverable.

**Video and TTS are emerging as the next frontier.** MiniMax-H3 (video), Audio8-TTS, and Inflect-Micro-v2 show growing multi-modal breadth beyond text and image. Expect this trend to accelerate.

---

## 4. Worth Exploring

**1. [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) (Moonshot AI)** — The #1 trending model this week, and for good reason. It combines vision-language capabilities with novel compressed-tensor support, potentially enabling more efficient multimodal inference. Given Moonshot's track record (Kimi-K2 was a top-tier coding model), Kimi-K3 could become a pivotal release for the multimodal ecosystem.

**2. [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) (MiniMaxAI)** — A fresh image-text-to-video model with zero downloads but 1,458 likes. Video generation is the next major battleground in generative AI, and MiniMax has been a strong player (their Hailuo video models were well-received). Combined with the official Comfy-Org integration, this is worth studying for both research and creative workflow potential.

**3. [Instella-MoE-16B-A3B-Think](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) (AMD)** — AMD's entry into the MoE reasoning space is strategically significant. Built on DeepSeek-v3 architecture with only 3B active parameters, this model demonstrates AMD's commitment to competitive open-weight releases and could indicate increasing AMD GPU support in the ecosystem. Worth monitoring for hardware-software co-evolution signals.

---

*Data as of 2026-08-04, sorted by weekly likes.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*