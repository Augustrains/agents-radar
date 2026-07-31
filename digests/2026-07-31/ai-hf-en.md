# Hugging Face Trending Models Digest 2026-07-31

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-31 01:26 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-31

---

## 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by **Qwen3.6-35B-A3B**, which has amassed 6.1M downloads — a clear signal that compact MoE architectures are the industry's new backbone. **Kimi-K3** from Moonshot AI leads in community engagement with 9K+ likes, while **GLM-5.2** (1.5M downloads) shows Zhipu AI's growing enterprise traction. Notably, two of the top five most-downloaded models are **uncensored community fine-tunes**, reflecting a persistent demand for unaligned variants. The quantization ecosystem remains vibrant, with GGUF releases of frontier models appearing within days of their base counterparts. Microsoft's **Fara1.5-27B** (computer-use) signals a corporate push into agentic multimodal territory, while TTS/ASR entries from Microsoft and owensong hint at an edge-AI audio war.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,681 | 1,527,760 | Flagship MoE-DSA conversational model from Zhipu AI; massive adoption in enterprise and agentic chatbots |
| [**Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 847 | 73,246 | Poolside's coding-centric LLM contender; strong performance signals for code generation and reasoning |
| [**Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 702 | 12,411 | Upstage's open-weight 250B frontier model; notable for challenging the closed-source giants |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 582 | 24,542 | Compact 3B multilingual LLM; popular for on-device deployment and low-resource languages |
| [**antares-1b**](https://huggingface.co/fdtn-ai/antares-1b) | fdtn-ai | 240 | 9,820 | Security-focused 1B parameter model (GraniteMoE hybrid); tiny but trusted for code audit |
| [**Instella-MoE-16B-A3B-Think**](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 94 | 1,315 | AMD's reasoning-focused MoE (DeepSeek-V3 style) with 3B active params; check AMD's open-source play |

### 🎨 Multimodal & Generation

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,009 | 387,822 | Moonshot AI's flagship image+text model with compressed-tensor optimization; highest likes this week |
| [**Inkling**](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,655 | 45,658 | Conversational multimodal chat model; tuned for human-like interaction with images |
| [**Qwen3.6-35B-A3B**](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 2,595 | 6,119,519 | **Most-downloaded model this week**; compact MoE with vision capability, powering thousands of derivatives |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,583 | 2,598,659 | Baidu's industrial-grade OCR; trending for document AI and enterprise RAG pipelines |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 321 | 1,100 | Edge-optimized local TTS — micro footprint, CPU-friendly speech synthesis |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 126 | 225 | New TTS contender built on ArkTTS architecture; promising voice quality at preview scale |
| [**Inflect-Nano-v2**](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 119 | 654 | Nano-scale edge TTS; success partner of Inflect-Micro, targets IoT and wearables |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 121 | 2,951 | Microsoft's vision-language model; interesting for reasoning about visual scenes |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 114 | 840 | Distilled tiny version of Inkling; for on-device multimodal interaction |
| [**Mage-Flow**](https://huggingface.co/Comfy-Org/Mage-Flow) | Comfy-Org | 97 | 44,714 | ComfyUI diffusion single-file workflow; enabling image-gen creativity in the Comfy ecosystem |

### 🔧 Specialized Models (code, OCR, ASR, computer-use)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 351 | 9,225 | MoE-based coding model on Qwen3.5 backbone; developer build, gains steam for code completion |
| [**OvisOCR2**](https://huggingface.co/ATH-MaaS/OvisOCR2) | ATH-MaaS | 351 | 57,439 | OCR-specialized Qwen3.5 model; strong accuracy for documents and multilingual text extraction |
| [**Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 222 | 2,316 | Microsoft's computer-use model (Qwen3.5 based); frontier of GUI automation agents |
| [**VibeVoice-ASR-BitNet**](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 120 | 3,864 | BitNet-compressed ASR model; near-lossless inference at extreme compression — edge audio |

### 📦 Fine-tunes & Quantizations (GGUF, community builds)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,190 | 1,803,090 | The most-downloaded uncensored GGUF of Qwen3.6; massive community demand for unaligned vision-chat |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,034 | 955,767 | Community master-merge of Qwen3.6; combines "Heretic" + "Fable" + NEO-Imatrix — extreme uncensored fine-tune |
| [**Ternary-Bonsai-27B-gguf**](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,115 | 697,666 | **2-bit ternary quantization** of a 27B model — memory-efficient frontier; highly notable for edge feasibility |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 241 | 162,394 | Hermes-style merging of Qwen3.6 MoE; roleplay-friendly uncensored GGUF |
| [**Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 158 | 248,173 | 9B uncensored merge with Imatrix quantization; nimble pick for edge uncensored chat |
| [**Laguna-S-2.1-GGUF**](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF) | unsloth | 259 | 159,331 | Official unsloth GGUF of poolside's Laguna; fast local inference for coding |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 209 | 12,178 | Unsloth's GGUF of Moonshot's Kimi-K3 — local consumption of a top multimodal LLM |
| [**Kimi-K3**](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 176 | 766 | Safetensors re-release of Kimi-K3 with compressed-tensor support; lab-friendly for deep tweaking |
| [**Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 147 | 7,755 | NVFP4 4-bit quantization for vLLM; massive memory savings on H100/A100 class hardware |
| [**Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 94 | 201 | 2-bit expert-weight quantization of Qwen3.6; uncompressed under-the-hood exploration |

---

## 3. Ecosystem Signal

Several powerful trends define this snapshot:

- **Qwen3.6 is the new Linux of LLMs** — a single base model (35B-A3B) has spawned uncensored fine-tunes, roleplay merges, 2-bit quantization, and 1.8M+ download derivatives, all within one week. Qwen's vision+language MoE has effectively become the community's default substrate.

- **Quantization is accelerating toward the extreme**: Ternary-Bonsai 27B (2-bit, 697K downloads), NVFP4 on Solar-Open2, and BitNet ASR signal a race to push frontier-class models into consumer hardware. Expect this category to explode further.

- **Uncensored demand is not a niche**: The top-2 most downloaded community models are uncensored GGUF variants. The HauhauCS Qwen3.6 uncensored build pulled 1.8M downloads in days — a statistical anomaly that platforms will have to address.

- **Microsoft is quietly building an agentic empire**: Fara1.5-27B (computer-use), Mage-VL, and VibeVoice-ASR all combine to position MSFT across vision, audio, and GUI automation, all open-weight.

- **The "MoE + GGUF + vision" stack is winning** — nearly half of all trending models fit this combo, and it appears to be the ecosystem's sweet spot for performance-per-edge-compute.

---

## 4. Worth Exploring

1. **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — This 2-bit ternary model is a must-study for any team building edge or consumer-hardware inference products. If a 27B at 2-bit can hold the line on quality, it changes the economics of local AI entirely.

2. **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Regardless of your stance on uncensored models, this is a statistical outlier you should download and A/B test. If output quality rivals the base Qwen3.6, it reveals how much "alignment" actually costs.

3. **[Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — Computer-use is the next frontier of agentic AI. Microsoft's open-weight approach here lets you study a major vendor's take on GUI grounding — a rare, high-value research asset.

---

*Report generated from Hugging Face Hub trending data — 2026-07-31*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*