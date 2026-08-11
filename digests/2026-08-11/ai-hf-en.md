# Hugging Face Trending Models Digest 2026-08-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-11 00:45 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-11

---

## 1. Today's Highlights

This week's Hugging Face landscape is dominated by a major release wave around **MiniMax-H3**, a powerful image-text-to-video model that has spawned an entire ecosystem of fine-tunes, quantizations, ComfyUI integrations, and turbo variants — with dozens of derivatives appearing across the top 30. Meanwhile, **DeepSeek-V4-Flash-0731** continues its meteoric rise with nearly a million downloads, signaling strong appetite for efficient conversational LLMs, and **Kimi-K3** from Moonshot AI claims the second-highest like count with its compressed-tensor architecture. Notably, **FLUX.1-dev** from Black Forest Labs remains the undisputed community favorite in image generation, and **baidu/Unlimited-OCR** demonstrates the growing corporate interest in specialized vision-language models. The trend toward GGUF quantizations (by unsloth, LiquidAI, and others) and aggressive community fine-tuning — including the "Heretic"/"Uncensored" Qwen variants — shows a thriving open-weight ecosystem.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,059 | 954,441 |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,470 | 1,510,032 |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 490 | 89,680 |
| [maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 311 | 1,344 |
| [Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 287 | 5,261 |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 221 | 6,343 |

- **DeepSeek-V4-Flash-0731**: New flagship flash-tier conversational LLM from DeepSeek, optimized for speed and cost — the most downloaded model on this list this week.
- **Kimi-K3**: Moonshot AI's efficient, feature-extraction-oriented hybrid LLM with compressed tensors, proving that smaller-parameter, high-efficiency models are winning the community's heart.
- **LFM2.5-2.6B**: LiquidAI's small-but-mighty 2.6B parameter liquid model, gaining traction for its impressive capabilities per parameter.
- **Shieldstral-1.0-3B**: Mistral's compact safety/guardrail model for the Mistral 3 family.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,429 | 47,468 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,145 | 6,009,639 |
| [PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 250 | 0 |
| [Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 259 | 15,087 |
| [FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,076 | 480,762 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 4,002 | 2,921,751 |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 707 | 0 |

- **MiniMax-H3**: The breakout text-image-to-video powerhouse, catalyzing an entire derivative ecosystem — from ComfyUI single-files (6M+ downloads) to turbo LoRAs and NVFP4 quantizations.
- **FLUX.1-dev**: Black Forest Labs' text-to-image model that remains the community's gold standard for high-quality image generation.
- **Unlimited-OCR**: Baidu's vision-language OCR model, a massive hit with 2.9M downloads, indicating demand for robust document-understanding models.
- **Muse-Glimmer-30B**: Meta's newest multimodal image-text-to-text model, still fresh off the press with zero downloads (likely recently released).

### 🔧 Specialized Models (code, math, medical, embeddings, safety)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 297 | 597 |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 221 | 6,343 |

- **NVIDIA-NemotronLabs-VoiceChat-11B**: NVIDIA's voice/interactive model for real-time speech-to-speech dialog, backed by multiple arxiv papers.
- **Shieldstral-1.0-3B**: A purpose-built safety rail model from Mistral — a growing category as enterprises demand guardrails.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, LoRA)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored…](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,861 | 2,439,083 |
| [Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 207 | 0 |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 636 | 199,167 |
| [LFM2.5-2.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 184 | 89,611 |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 599 | 0 |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 192 | 174,862 |
| [Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 162 | 530,052 |
| [Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 152 | 0 |
| [PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 250 | 0 |
| [MiniMax-H3-Prompt-Rewriter-LoRA](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA) | lightx2v | 116 | 268 |
| [Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 256 | 0 |
| [Kijai/MiniMax-H3-experimental](https://huggingface.co/Kijai/MiniMax-H3-experimental) | Kijai | 184 | 0 |
| [BigBang-v1](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 152 | 617 |

- **Qwen3.6-27B-Fable-Fusion-711-Uncensored…**: A massive community favorite — Qwen base fused with "uncensored" and "heretic" fine-tuning approaches, quantized to GGUF for local deployment (2.4M downloads).
- **DeepSeek-V4-Flash-0731-GGUF**: Unsloth's ubiquitous GGUF conversion of DeepSeek's new model — the go-to for local inference.
- **MiniMax-H3 ecosystem**: From turbo LoRAs to NVFP4 quantizations to ComfyUI wrappers, the derivative scene around MiniMax-H3 is the most active in the entire list.

---

## 3. Ecosystem Signal

**LLMs are pivoting to efficiency-first architectures.** Kimi-K3 (compressed tensors, feature extraction) and DeepSeek-V4-Flash set a new bar for "flash" tier models — the community is rewarding performance-per-parameter more than raw scale. LiquidAI's tiny 2.6B model gaining traction reinforces this, as does the popularity of the GGUF ecosystem for local, affordable inference.

**Video generation is the new frontier — and MiniMax-H3 is the hub.** The density of derivatives around MiniMax-H3 (turbo LoRAs, ComfyUI integrations, NVFP4/INT4 quantizations from at least 6 different authors) signals that text-to-video is where the largest community activity is concentrated. This mirrors the FLUX.1-dev pattern from image generation, now being replicated for video.

**The "uncensored/heretic" fine-tuning movement is thriving** — communities are actively merging Qwen models with uncensored fine-tunes, often via GGUF quantization, for local, unconstrained deployment. This is a notable open-weight trend that is driving millions of downloads.

**Open-weight vs proprietary:** Hugging Face's trends remain overwhelmingly open-weight. NVIDIA, Mistral, Baidu, Meta, DeepSeek, and Moonshot all released open models this week. Quantizations from unsloth and community authors are the key distribution channel.

---

## 4. Worth Exploring

**1. [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — This is the single most influential release this week. Its ecosystem (ComfyUI, LoRAs, quantizations) is the highest-velocity derivative landscape on the Hub. Even if you don't work on video generation, *studying* how a single model release catalyzes an entire community ecosystem is valuable for understanding HF dynamics.

**2. [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10,470 likes (second only to FLUX.1-dev), this compressed-tensor model is the most-liked LLM release this week. Its dual feature-extraction + conversational design is a novel architecture worth studying — and with 1.5M downloads, it's clearly filling a real gap.

**3. [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B)** — At just 2.6B parameters, this "liquid" model is punching well above its weight. With both a full-precision and GGUF version trending, it's a great case study for efficient local deployment. If you're building for edge or resource-constrained environments, this is the model to test.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*