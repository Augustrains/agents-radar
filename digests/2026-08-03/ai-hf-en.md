# Hugging Face Trending Models Digest 2026-08-03

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-03 01:25 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-03

## 1. Today's Highlights

**Moonshot AI's Kimi-K3** dominates the chart with an extraordinary 9,637 weekly likes, making it the clear breakout release—a multimodal model that is already spawning a GGUF quantization from unsloth. **DeepSeek** continues its cadence with **DeepSeek-V4-Flash-0731** (dated checkpoint) alongside the previously released **DeepSeek-V4-Flash**, which holds massive cumulative downloads (2.78M). **Baidu's Unlimited-OCR** demonstrates that specialized OCR capabilities remain highly sought-after with 3,778 likes and 2.5M downloads. The Qwen3.6 ecosystem is exploding with community fine-tunes—particularly uncensored variants like **HauhauCS's 3,243-like Aggressive version**—while several Qwen3.5-MoE derivatives from smaller labs signal heavy community reliance on the Qwen family as a base for experimentation. Notably, **GLM-5.2** from Zhipu AI posts strong numbers, confirming the Chinese open-weight labs are in a fierce race.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,637 | 837K |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 1,722 | 156K |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,755 | 2.05M |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,958 | 2.79M |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 626 | 33K |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 877 | 80K |
| [Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 719 | 15K |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 153 | 68K |
| [Instella-MoE-16B-A3B-Think](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 121 | 2K |
| [LFM2.5-Encoder-350M](https://huggingface.co/LiquidAI/LFM2.5-Encoder-350M) | LiquidAI | 89 | 7K |

**Kimi-K3** is the week's sensation—a multimodal model with compressed-tensor support that has amassed nearly 10K likes in one week. **DeepSeek-V4-Flash** (and its dated checkpoint) anchors the DeepSeek momentum with strong community support. **GLM-5.2** uses a MoE-DSA architecture, signaling continued Mixture-of-Experts innovation from Zhipu. **Solar-Open2-250B** from Upstage shows that very large open-weight models still command attention, with the NVFP4 quantization from NOTA AI adding deployment viability. AMD's **Instella-MoE-16B-A3B-Think** (built on DeepSeek-V3 architecture) shows the MoE reasoning-model trend is maturing beyond the original labs.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,778 | 2.54M |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 185 | 272K |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 371 | 1.8K |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 179 | 4.3K |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 126 | 0 |
| [VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 150 | 8.5K |
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 250 | 2.9K |

**Unlimited-OCR** is the obvious standout—Baidu's OCR model has millions of downloads and ranks #2 in likes this week. Microsoft is having a moment with three entries: **Mage-VL** (multimodal VL), **Fara1.5-27B** (computer-use agent with vision), and the novel **VibeVoice-ASR-BitNet** (ASR with BitNet quantization). TTS is quietly gaining: **Inflect-Micro-v2** bills itself as CPU/edge-ai ready, while **Audio8** offers a 0.6B alternative. **Kroma** is a fresh Krea2 LoRA for ComfyUI with no downloads yet—early stage but interesting for the creative community.

### 🔧 Specialized Models (Code, OCR, Agentic, Embeddings)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 402 | 13K |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 335 | 1.1K |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 366 | 0.9K |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 227 | 6.8K |

**KAT-Coder-V2.5-Dev** continues the coding-agent model trend (built on Qwen3.5-MoE). **XYZ-Aquila** (mini and pro) from XYZAILab are Qwen3.5-MoE based models targeting agentic-search—small but with high like-to-download ratios indicating strong quality signal. **Inkling-Small** is a new multimodal model from thinkingmachines that's early in adoption.

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,339 | 1.37M |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 339 | 49K |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 250 | 88K |
| [Kimi-K3](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 225 | 1.3K |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 300 | 259K |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 119 | 2.6K |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,243 | 1.89M |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 208 | 293K |

The Qwen3.6 uncensored fine-tune ecosystem is in full bloom. **HauhauCS's Aggressive variant** is the crown jewel at 3,243 likes and 1.9M downloads—massive community appetite. **DavidAU** continues their release-heavy strategy with another uncensored Qwen3.6 GGUF (1.37M downloads). **LuffyTheFox** offers the Hermes-flavored alternative. Unsloth's GGUF conversions of DeepSeek-V4-Flash and Kimi-K3 make both flagship models accessible for local deployment.

## 3. Ecosystem Signal

**Qwen is the new community backbone.** While Moonshot, DeepSeek, and Zhipu compete for frontier attention, the Qwen3.5/3.6 family is becoming the default base for community experimentation—particularly MoE variants (35B-A3B) that are cheap enough for fine-tuning. The "uncensored" niche is remarkably active, with several variants crossing 1M+ downloads.

**Chinese labs are winning the open-weight race.** Moonshot, DeepSeek, Zhipu, Baidu, and Nanbeige all posted strong numbers this week, outpacing American and European labs in community adoption. Microsoft remains competitive through sheer breadth (vision, ASR, computer-use).

**Quantization is everywhere.** Every single top model already has or is getting a GGUF/NVFP4 variant, often within days of release. Unsloth has become the canonical quantization pipeline. NVFP4 from NOTA AI suggests hardware-aware quantization is gaining for enterprise deployment.

**MoE architecture is the dominant paradigm**, appearing in GLM-5.2, DeepSeek-V4, and every Qwen3.6 derivative. With 250B+ models at one end and 3B at the other, MoE's efficiency story continues to win over dense architectures.

## 4. Worth Exploring

1. **[Kimi-K3 (moonshotai)](https://huggingface.co/moonshotai/Kimi-K3)** — The week's breakout model. With 9,637 likes, it's not just a trending artifact but possibly a paradigm shift in multimodal architecture (compressed-tensors, feature-extraction). Worth studying for what it means for efficient multimodal inference.

2. **[GLM-5.2 (zai-org)](https://huggingface.co/zai-org/GLM-5.2)** — An MoE-DSA architecture with 2M+ downloads and 4.7K likes. The "DSA" (likely dynamic sparse attention) innovation deserves a technical deep-dive—an alternative to standard attention in MoE models.

3. **[VibeVoice-ASR-BitNet (microsoft)](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet)** — ASR meets BitNet quantization with GGML/GGUF support. This could be the key to running speech recognition on edge/CPU devices, and its novelty factor (150 likes on a brand-new release) suggests early adopters see real promise here.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*