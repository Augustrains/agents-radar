# Hugging Face Trending Models Digest 2026-08-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-06 01:16 UTC

---

# 🤖 Hugging Face Trending Models Digest
**Date:** 2026-08-06

---

## 1. Today's Highlights

The Hugging Face ecosystem is buzzing with the release of several major open-weight models. **Moonshot AI's Kimi-K3** leads the pack with over 10,000 weekly likes and 1.1M downloads, signaling strong community appetite for next-generation multimodal LLMs. **Zhipu AI's GLM-5.2** and **DeepSeek-V4-Flash** continue to dominate the text-generation arena with massive download counts (2.2M and 2.7M respectively), cementing the dominance of Chinese labs in the open-weight space. Meanwhile, **MiniMax-H3** marks a significant foray into advanced image-to-video generation, drawing attention from both creators and the ComfyUI community. A notable trend is the proliferation of **Qwen3.5/3.6-based fine-tunes** (uncensored variants, MoE quantizations, and GGUF conversions), indicating a vibrant community ecosystem around this base architecture. Lastly, **Baidu's Unlimited-OCR** has emerged as a surprising download leader (2.7M), highlighting strong demand for robust OCR solutions.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,496 | 433K | Latest iteration of DeepSeek's efficient Flash series, offering cutting-edge conversational performance at scale. |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,125 | 1.1M | The most-liked model this week; a flagship multimodal LLM with compressed-tensor support, following the massive success of the Kimi series. |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,849 | 2.2M | Latest from Zhipu AI's GLM family, featuring MoE architecture and strong conversational capabilities; one of the most downloaded models. |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,031 | 2.7M | The parent release of the V4-Flash series, now the most-downloaded model on this list; a top-tier open-weight LLM. |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 285 | 47K | Compact 2.6B model from Liquid AI, attracting attention for its efficiency and small-footprint text generation. |
| [deepgrove/maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 157 | 0 | A brand-new preview MoE model from deepgrove, generating early buzz for its architecture. |
| [inclusionAI/Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 156 | 25 | New hybrid-architecture conversational model from inclusionAI, still in early adoption phase. |
| [LGAI-EXONE/K-EXAONE-2.0-750B-A37B](https://huggingface.co/LGAI-EXONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXONE | 129 | 325 | Massive 750B MoE model from LG AI, showcasing Korean-lab leadership in frontier-scale open weights. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,496 | 10.8K | A cutting-edge image-to-video generation model from MiniMax, capturing the moment in video AI with strong community interest. |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,906 | 2.7M | Baidu's versatile OCR model with remarkably high downloads; a practical go-to for document intelligence tasks. |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 275 | 435K | Microsoft's multimodal vision-language model, proving highly popular for its broad applicability. |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 274 | 11.3K | Efficient 0.6B text-to-speech model with ArkTTS backbone for fast, expressive audio synthesis. |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 417 | 2K | A hyper-efficient, CPU-friendly TTS model designed for local and edge deployment. |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 191 | 0 | A new LoRA for Krea2 image generation, compatible with ComfyUI, still in release-buzz phase. |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 124 | 80 | NVIDIA's voice-chat model, built atop the NemotronLabs research line for spoken dialogue. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 496 | 15.4K | A code-specialized model built on Qwen3.5 MoE backbone, gaining traction in developer communities. |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 308 | 15.5K | A compact multimodal reasoning model from thinkingmachines, popular for efficient vision-language tasks. |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 131 | 166 | Mistral's lightweight safety/guardrail model (vLLM-compatible), designed to filter and moderate model outputs. |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,587 | 1.6M | A heavily customized, uncensored Qwen3.6 fine-tune in GGUF format with multi-token prediction; one of the most downloaded community models. |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 502 | 111K | Official UnsLoth GGUF conversion of DeepSeek-V4-Flash-0731, making it easy to run locally. |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 316 | 170K | UnsLoth's GGUF quantization of the overwhelming popular Kimi-K3, boosting local deployability. |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 385 | 308K | Massive community demand for this uncensored Qwen3.6 MoE GGUF with Hermes alignment. |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 282 | 323K | Another popular DavidAU release with NEO-imatrix quantization and MTP support for Qwen3.5. |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 137 | 40K | Community GGUF quantizations of MiniMax-H3 for local video generation workflows. |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 210 | 2.9K | Specialized weight-bin (W2) quantization of the Qwen3.6 35B-A3B MoE from EschaLabs. |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 416 | 1.3K | A mini variant built on Qwen3.5/3.6 MoE architecture, optimized for efficient deployment. |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 366 | 1.4K | Pro version of Aquila with agentic-search capabilities, targeting autonomous agent use. |
| [Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 283 | 0 | A ComfyUI-integrated INT8 quantized Qwen3-VL variant; early in the buzz cycle. |
| [Qwythos-27B-v1](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 145 | 2.2K | Community fine-tune of Qwen3.5 for creative/roleplay use cases. |

---

## 3. Ecosystem Signal

**Qwen is the undisputed community backbone.** The explosion of Qwen3.5/3.6 fine-tunes, MoE quantizations, and uncensored variants demonstrates that the Qwen architecture has become the de facto standard for community experimentation. DavidAU's near-million-download GGUF fine-tunes are a clear signal that the local-inference crowd gravitates toward Qwen-based models with multi-token prediction (MTP) support.

**Chinese labs are setting the pace for open-weight frontier models.** Moonshot (Kimi-K3), DeepSeek (V4-Flash), Zhipu (GLM-5.2), and Baidu (Unlimited-OCR) collectively dominate the trending charts. Their releases consistently outperform Western counterparts in adoption metrics, indicating a paradigm shift in open-weight leadership.

**Quantization infrastructure is maturing.** UnsLoth's official GGUF conversions of major releases (DeepSeek-V4, Kimi-K3) suggest that quantization is no longer a community afterthought but a first-class citizen in the model release pipeline. The proliferation of specialized quantizations (IMATRIX, INT8, W2, MTP-optimized) points to an increasingly sophisticated local-inference ecosystem.

**Multimodality is becoming the default.** The majority of new releases ship with image-text-to-text pipelines, and video generation (MiniMax-H3) is gaining serious traction with ComfyUI integration.

---

## 4. Worth Exploring

**[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10K+ likes in a single week and 1.1M downloads, Kimi-K3 is the most significant release in this digest. It's a flagship multimodal model with compressed-tensor support, representing the current state-of-the-art in open-weight reasoning. Any serious practitioner should evaluate it as a potential backbone for their applications.

**[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — As video generation becomes the next frontier in generative AI, MiniMax-H3's image-to-video capabilities represent a major step forward. With Comfy-Org's integration (755 likes) and community GGUF quantizations already available, it's poised to become the stable-diffusion moment for video.

**[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — With 2.7M downloads, this model is the most-downloaded in the digest and represents the current workhorse of the open-weight LLM ecosystem. Its efficient Flash architecture balances performance and cost, making it a pragmatic choice for production deployments — and the official UnsLoth GGUF makes it accessible for local inference.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*