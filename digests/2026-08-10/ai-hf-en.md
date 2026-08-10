# Hugging Face Trending Models Digest 2026-08-10

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-10 00:45 UTC

---

# Hugging Face Trending Models Digest — 2026-08-10

---

## 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by **MiniMax-H3**, a video generation model that has spawned an extraordinary ecosystem of community adaptations—from ComfyUI integrations and LoRA fine-tunes to quantized GGUF versions and Turbo variants—collectively amassing over 5.7 million downloads across derivative models. The **DeepSeek-V4-Flash-0731** release continues to gain traction with 868K downloads, while the **Qwen3.6-27B/35B** "uncensored" fine-tune family demonstrates the enduring appetite for community-modified LLMs. Notable first-party releases include **Kimi-K3** (10.4K likes, the highest of any new model) and **GLM-5.2** (4.9K likes, 2.5M downloads), signaling a surge of open-weight competition in the frontier LLM space. The appearance of **Microsoft's Mage-VL** and **NVIDIA's VoiceChat-11B** highlights growing institutional investment in multimodal and voice-capable models. The sheer volume of H3-related derivatives (8 of 30 entries) suggests video generation is now the hottest battleground in open-source AI.

---

## 2. Trending Models

### 🧠 Language Models

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,944 | 868,576 |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,398 | 1,456,459 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,914 | 2,488,397 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 452 | 85,651 |
| [deepgrove/maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 289 | 1,089 |
| [inclusionAI/Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 245 | 4,747 |
| [nvidia/NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 260 | 543 |

**DeepSeek-V4-Flash-0731** is DeepSeek's latest fast-conversational model, delivering strong reasoning performance with an efficient architecture that's driving massive download volume. **Kimi-K3** is Moonshot AI's flagship multimodal LLM (feature-extraction, compressed-tensors) that has the highest like count this week — 10.4K — signaling major community enthusiasm for this compact, efficient model. **GLM-5.2** by Zhipu AI (zai-org) is a mixture-of-experts text-generation model with 2.5M downloads, demonstrating the user appetite for high-performance open-weight alternatives to proprietary LLMs. **LFM2.5-2.6B** from LiquidAI is their latest liquid neural network-based 2.6B parameter model, popular among researchers and edge-deployment enthusiasts for its parameter efficiency. **maple-preview** from deepgrove is a new mixture-of-experts causal LM in preview stage, interesting for its MoE design and early-stage promise. **Ling-3.0-flash** by inclusionAI is a bilingual (Chinese/English) conversational model optimized for speed and low-latency applications. **NVIDIA NemotronLabs VoiceChat-11B** is NVIDIA's new voice-optimized conversational model, pairing speech understanding with response generation for voice-first interfaces.

### 🎨 Multimodal & Generation

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,244 | 35,295 |
| [baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,986 | 2,889,062 |
| [black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,059 | 487,171 |
| [microsoft/Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 323 | 461,150 |
| [Audio8/Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 333 | 13,132 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 233 | 6,117 |
| [Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 155 | 511,473 |

**MiniMax-H3** is the week's breakout video model — an image-text-to-video diffusion model that creates high-quality, consistent videos from prompts, and has become the most-forked and most-adapted model on the hub. **Unlimited-OCR** by Baidu is a universal OCR model (image-text-to-text) with near-perfect accuracy across scripts and layouts, converting document images into structured text; its 2.9M downloads show the importance of OCR in production. **FLUX.1-dev** from Black Forest Labs remains the standard for high-fidelity text-to-image generation with its flow-matching diffusers architecture; 14K likes and 487K downloads keeps it firmly in the #1 position. **Mage-VL** is Microsoft's new multimodal vision-language model for image- and video-grounded Q&A and reasoning, with 461K downloads in its first week. **Audio8-TTS-Preview** is a lightweight AR-based text-to-speech model (0.6B params) that generates natural speech with low latency, gaining rapid adoption for voice agents. **Minimax-h3-Turbo** is a community-build of faster inference variant optimized for diffusion — targeting turbo-speed video generation workflows. **Abiray's Minimax-H3-nvfp4** is a quantized 4-bit/8-bit optimized version of MiniMax-H3 for consumer GPUs (NVFP4), making video gen viable without datacenter hardware.

### 🔧 Specialized Models

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 552 | 18,574 |
| [mistralai/Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 211 | 5,651 |
| [endless-frontier/BigBang-v1](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 121 | 482 |

**KAT-Coder-V2.5-Dev** is a code-focused LLM from Kwaipilot based on Qwen3.5-MoE architecture, fine-tuned specifically for codegen and software engineering tasks. **Shieldstral-1.0-3B** by Mistral is a 3B parameter safety/guardrail classifier for content moderation on LLM outputs, built on the Mistral3 architecture and optimized for vLLM — crucial for deployment. **BigBang-v1** from endless-frontier is a multimodal (image-text-to-text) conversational MoE model built on Qwen3.5, designed for general reasoning with heavy image comprehension duties.

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,806 | 2,390,692 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,072 | 4,947,943 |
| [unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 627 | 188,761 |
| [LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 454 | 396,282 |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 544 | 0 |
| [LiquidAI/LFM2.5-2.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 174 | 68,468 |
| [Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 233 | 0 |
| [SexGod1979/PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 231 | 0 |
| [Kijai/MiniMax-H3-experimental](https://huggingface.co/Kijai/MiniMax-H3-experimental) | Kijai | 169 | 0 |
| [realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 188 | 160,747 |
| [ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 418 | 0 |
| [drbaph/MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 231 | 0 |
| [sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 143 | 0 |

This week's fine-tunes and quantizations are mostly centered on two families: **MiniMax-H3** (for ComfyUI, GGUF, LoRA, NVPF4) and **Qwen3.6** (uncensored, "Heretic" variants in GGUF for local CPU inference). **Comfy-Org/MiniMax-H3** has 4.9M downloads — the highest in the list — and is the official ComfyUI-optimized single-file release of H3; it's the go-to for local video generation in ComfyUI. **DavidAU's Qwen3.6-27B-Fable-Fusion** is a massive merge of various Qwen3.6 fine-tunes, known colloquially as "Uncensored-Heretic", cited increasingly for serious roleplay and uncensored writing tasks. **unsloth/DeepSeek-V4-Flash-GGUF** is the official UnsLoth quantized release (Q4_K_M etc.) of DeepSeek-V4-Flash, enabling consumer-hardware inference. **LuffyTheFox's Qwen3.6-35B-A3B-GGUF** is another uncensored + Hermes-style instruct merge, targeting MoE efficiency on single-GPU setups. **Kijai/MiniMax-H3_comfy** is a dedicated ComfyUI workflow wrapper for H3 video generation, with zero downloads because it's a code/config repo rather than a weight release.

---

## 3. Ecosystem Signal

**Video generation is the new LLM.** The sheer velocity of MiniMax-H3 derivatives — 9 of 30 trending models — reveals a self-sustaining ecosystem forming around video generation. This echoes the pattern seen with Stable Diffusion in image generation and Llama in text: a single strong open-weight base model (H3) spawning quantization specialists (Abiray, realrebelai), ComfyUI integrations (Kijai, Comfy-Org), LoRA-style fine-tunes (larryvrh, drbaph), and Turbo speed-ups (lightx2v). The open-weight frontier has consolidated around three LLM families — **Qwen** (3.6), **DeepSeek** (V4-Flash), and **GLM** (5.2) — with each claiming millions of downloads. MoE-based architectures (GLM-5.2, Qwen3.5-moe in KAT-Coder, BigBang) are now the standard for scaling efficiency, not an outlier. Quantization is no longer a nice-to-have: GGUF releases from UnsLoth and community members like DavidAU are hitting multi-million download counts, meaning the "consumer GPU" market segment is a major driver of ecosystem growth. The "Heretic/Uncensored" naming convention has become a persistent sub-genre, indicating a durable community segment that prioritizes unaligned outputs. Meanwhile, institutional entries from **Microsoft (Mage-VL)**, **NVIDIA (VoiceChat)**, and **Baidu (Unlimited-OCR)** signal that frontier labs are increasingly treating Hugging Face as their primary distribution channel for production AI components.

---

## 4. Worth Exploring

**1. [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) (+ the Comfy-Org single-file variant)** — This is the ecosystem's center of gravity right now. Studying why H3 became the convergent point for video generation (architecture choices, licensing, ComfyUI integration maturity) offers a blueprint for how a model becomes an ecosystem rather than just a checkpooint.

**2. [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10.4K likes in its first week — the highest new-model like velocity of the month — K3 is worth investigating for efficiency breakthroughs (feature-extraction + compressed-tensors). If Moonshot's compression approach proves robust, dense models may become viable competitors to MoE systems.

**3. [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — A 2.4M-download GGUF that's essentially a model merge of community fine-tunes; it represents the power of the "fusing and quantizing" workflow every open-weight breakout seems to generate. It's a case study in how second-order value (merging + GGUF packing) often outweighs first-party distribution.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*