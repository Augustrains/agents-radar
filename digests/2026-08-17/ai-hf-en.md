# Hugging Face Trending Models Digest 2026-08-17

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-17 00:29 UTC

---

# 🤗 Hugging Face Trending Models Digest
**Date: 2026-08-17**

---

## 1. Today's Highlights

This week's trending leaderboard reveals a major shift toward **massive multimodal MoE models** and **efficient quantized deployments**. **Qwen's Qwen3.8 family** dominates with the flagship 27B model (10,276 likes) and a 2.4T-parameter sparse MoE variant (1,010 likes), while **Moonshot AI's Kimi-K3** (10,767 likes) signals a strong push toward compressed multimodal transformers. The **MiniMax-H3 video generation ecosystem** is exploding—the base model has 2.3M downloads and the Comfy-Org integration has surpassed **13.4M downloads**, indicating massive community adoption. Video generation (LTX-2.5, MiniMax-H3 variants) and audio generation (MiniMax-Music3) are seeing heavy activity. Notably, **DeepSeek-V4** family ships both Pro (536 likes) and Flash (3,459 likes) variants, showing the open-weight frontier is pushing toward frontier-scale performance with permissively licensed weights.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 10,276 | 267,725 |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,010 | 7,932 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 536 | 21,873 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,459 | 1,872,232 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,767 | 2,136,775 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 291 | 196,326 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 160 | 66,253 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 647 | 141,009 |
| [inclusionAI/Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 285 | 5,727 |
| [dots-studio/dots3-note-prev](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 186 | 393 |

**Key notes:**
- **Qwen3.8-27B** is a leading open-weight image-text-to-text model; the 2.4T sparse MoE variant (95B active) demonstrates frontier-scale open alternatives.
- **Kimi-K3** from Moonshot AI is a massively liked compressed multimodal model with 2.1M downloads.
- **DeepSeek-V4-Flash** shows that open-weight models can achieve broad adoption (1.87M downloads) quickly.
- **NVIDIA's Nemotron Lightning** is an efficient 30B-A3B MoE optimized for NVIDIA hardware (NVFP4 quantized).

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,027 | 424,099 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 840 | 8,639 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,028 | 2,307,541 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 557 | 239,206 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,385 | 13,406,892 |
| [fal/MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 229 | 16,103 |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 776 | 0 |
| [Gazingstars123/Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 222 | 20,860 |
| [unsloth/MiniMax-H3-GGUF](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 175 | 204,344 |
| [Comfy-Org/MiniMax-Music-3](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 151 | 0 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,629 | 292,973 |

**Key notes:**
- **MiniMax-H3** is the dominant video generation model, with massive adoption via Comfy-UI integration (13.4M downloads).
- **LTX-2.5** from Lightricks is a strong competitor for video generation with 424K downloads.
- **MiniMax-Music3** enters the music generation space with text-to-audio capabilities.
- **Muse-Glimmer-30B** from meta-models (likely Meta) brings cutting-edge multimodal understanding to the open ecosystem.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

No dedicated code/math/medical/embedding models in this week's top-30 list. The focus is overwhelmingly on general-purpose multimodal and video/text generation.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,455 | 1,945,635 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 484 | 352,971 |
| [unsloth/Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 457 | 718,178 |
| [meta-models/Muse-Glimmer-30B-GGUF](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 298 | 357,877 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 344 | 4,285 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,095 | 3,020,070 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 210 | 183,988 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 202 | 276,269 |
| [Qwen/Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 209 | 11,311 |

**Key notes:**
- **GGUF quantization** is the dominant format for local deployment (1.9M downloads for Qwen3.8-27B-GGUF).
- **Uncensored fine-tunes** are consistently popular community adaptations (DavidAU's model alone has 3M downloads).
- NVIDIA's **NVFP4 format** is emerging as a premium quantization route for NVIDIA GPUs.
- The **"uncensored/abliterated"** niche is a persistent theme in community fine-tuning.

---

## 3. Ecosystem Signal

**Model Families:**
- **Qwen3.8** is the dominant open-weight family this week, spanning full-size, GGUF, FP8, NVFP4, and uncensored variants—covering 11 of the top 30 entries.
- **MiniMax-H3** is the clear leader in video generation, with base, Turbo, LoRA, and Comfy-UI variants all trending; ecosystem-level adoption (13.4M downloads) suggests community lock-in.
- **DeepSeek-V4** splits into Pro and Flash tiers, indicating a strategy of serving both frontier and cost-efficient markets.
- **NVIDIA Nemotron** with NVFP4 native quantization points to hardware-vendor co-optimized model releases.

**Open-weight vs Proprietary:** All top-30 models are open-weight, confirming the open ecosystem is now the primary venue for state-of-the-art model distribution. Moonshot, Qwen, DeepSeek, and NVIDIA all ship open releases.

**Quantization and fine-tuning activity:** The ecosystem is mature—GGUF is the standard for local, FP8/NVFP4 targets data-center GPUs, and uncensored/abliterated fine-tuning remains hugely popular. The proliferation of Comfy-UI wrappers (for both video and music) shows that **inference infrastructure** is becoming as important as the models themselves.

---

## 4. Worth Exploring

1. **[Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — A 2.4T sparse MoE with only 95B active params. This is a frontier-scale open-weight model with inference costs closer to much smaller models; the FP8 variant makes it even more accessible. Worth studying for the MoE architecture and scaling lessons.

2. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — The 13M+ downloads demonstrate how a well-integrated model into a tool ecosystem (ComfyUI) can achieve runaway adoption. Worth exploring as a case study in distribution and as a powerful video generation model.

3. **[lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo)** — A community Turbo variant of the H3 with 239K downloads. Shows how community fine-tuning of video models can yield faster, accessible versions of frontier tools.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*