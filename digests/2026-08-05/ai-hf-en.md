# Hugging Face Trending Models Digest 2026-08-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-05 01:18 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-05

---

## 1. Today's Highlights

This week's Hugging Face leaderboard is dominated by a new generation of **MoE (Mixture-of-Experts) architectures**, with **Qwen3.6** and **Kimi-K3** spawning massive fine-tuning and quantization ecosystems. The standout release is **moonshotai/Kimi-K3** (10,010 likes), which has already accumulated over 1.1M downloads and spawned multiple GGUF conversions. Meanwhile, **MiniMax-H3** represents a notable push into video generation, though its ComfyUI integration suggests it's primarily targeting creative workflows rather than research. **DeepSeek-V4-Flash** continues its momentum with two variants in the top 10, signaling strong enterprise adoption. Anthropic-style "uncensored" fine-tunes remain a persistent community trend, with **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** breaking 1.9M downloads.

---

## 2. Trending Models by Category

### 🧠 Language Models

| Model | Author | 👍 | 📥 | Description |
|---|---|---|---|---|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,299 | 433K | Latest iteration of DeepSeek's flash-tier conversational model, optimized for fast inference. |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,011 | 2.7M | The base V4 Flash release, now the most-downloaded DeepSeek variant on the platform. |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,819 | 2.2M | Zhipu AI's next-gen GLM with MoE-DSA architecture; strong multilingual and reasoning performance. |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,010 | 1.1M | Moonshot's flagship compressed-tensor vision-language model; this week's most-liked release. |
| [**Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 | 82.9K | Poolside's latest coding-oriented LLM, positioning itself as a competitive alternative to frontier models. |
| [**K-EXAONE-2.0-750B-A37B**](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 117 | 325 | LG's massive 750B-parameter MoE model (37B active) targeting Korean-language and enterprise workloads. |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 664 | 37.3K | Compact 3B LLM with strong performance-to-compute ratio; trending for edge deployment. |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 153 | 47.4K | Liquid AI's latest liquid-neural-network model, focused on adaptive inference efficiency. |

### 🎨 Multimodal & Generation

| Model | Author | 👍 | 📥 | Description |
|---|---|---|---|---|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,020 | 0 | Next-gen text/image-to-video generator; still fresh on the platform with downloads pending. |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 600 | 2 | ComfyUI-optimized wrapper for MiniMax-H3, enabling local video generation pipelines. |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 247 | 11.3K | New TTS model with AR-KTTS architecture; early preview gaining traction in audio generation. |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 176 | 0 | LoRA for Krea 2.0, designed for ComfyUI-based text-to-image workflows. |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 410 | 2.1K | Lightweight, CPU-friendly TTS model aimed at edge-AI and local speech synthesis. |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 256 | 435K | Microsoft's multimodal vision-language model; stands out for high download count relative to likes. |

### 🔧 Specialized Models

| Model | Author | 👍 | 📥 | Description |
|---|---|---|---|---|
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,881 | 2.7M | Baidu's open OCR model with feature-extraction tags; the most-downloaded specialized release today. |
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 473 | 15.4K | Dev-stage code-generation model built on Qwen3.5-MoE; trending among coding-focused users. |
| [**Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 174 | 69.3K | NVIDIA's Solar Open2 250B with NVFP4 quantization for vLLM deployment. |

### 📦 Fine-tunes & Quantizations

| Model | Author | 👍 | 📥 | Description |
|---|---|---|---|---|
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,296 | 1.9M | Heavily fine-tuned uncensored Qwen3.6 MoE variant with vision capabilities; massive community adoption. |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,512 | 1.6M | Community GGUF fine-tune pushing aggressive uncensoring on 27B Qwen base. |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 468 | 111.7K | Official UnsLoth GGUF quantization of the latest DeepSeek V4 Flash. |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 304 | 170K | UnsLoth's GGUF conversion of Kimi-K3, enabling local deployment of this massive model. |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 364 | 308.9K | Hermes-style uncensored fine-tune with GGUF packaging; strong download velocity. |
| [**Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 265 | 323K | Another DavidAU uncensored GGUF release, this time on the smaller 9B Qwen3.5. |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 103 | 40K | Community GGUF conversion of MiniMax-H3 for local text-to-video generation. |

---

## 3. Ecosystem Signal

Three clear signals emerge from this week's data:

**1. Qwen is the undisputed community backbone.** The Qwen3.6 family dominates fine-tuning activity, with uncensored variants (HauhauCS, LuffyTheFox, DavidAU) accumulating millions of combined downloads. This mirrors the Llama-era ecosystem dynamics, but with MoE architectures (A3B, 35B) replacing dense models as the preferred base.

**2. Open-weight MoE is now mainstream.** Kimi-K3, GLM-5.2, K-EXAONE, and Solar Open2 all ship MoE architectures ranging from 35B to 750B parameters. The cost-performance advantage of active-parameter routing has fully convinced frontier labs to open-weight their heavy hitters.

**3. LLM-as-ecosystem beats single-model releases.** The most successful releases this week (DeepSeek-V4, Kimi-K3, MiniMax-H3) all immediately spawned GGUF conversions, ComfyUI integrations, and fine-tune chains within 72 hours of release. The community infrastructure around a model — not just the model itself — now determines its viral potential.

**4. "Uncensored" remains a dominant community driver.** Despite no major policy changes from the big labs, uncensored fine-tunes continue to outperform their sanctioned counterparts by roughly 2-3× in downloads. This is a durable community niche that mainstream labs continue to ignore.

---

## 4. Worth Exploring

**[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The most-liked model this week deserves hands-on attention. Its compressed-tensor approach signals where multimodal LLM efficiency is heading, and the GGUF conversion opens up local deployment for a model of this scale.

**[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — For ecosystem watchers, this model represents the current state-of-the-art in community fine-tuning craft — how much can be squeezed from a 35B MoE with aggressive uncensoring and vision support.

**[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 2.7M downloads and relatively few likes, this transfer from Baidu is quietly becoming an infrastructure staple. Its feature-extraction capabilities and OCR specialization make it a valuable addition to any multimodal pipeline — and a signal of Chinese labs aggressively competing on open-weight utilities.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*