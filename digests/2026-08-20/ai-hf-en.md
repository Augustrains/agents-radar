# Hugging Face Trending Models Digest 2026-08-20

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-20 00:30 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-20

---

## 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by the **Qwen3.8 family**, with the flagship **Qwen/Qwen3.8-27B** (11.4K likes, 1M downloads) leading a massive wave of community derivatives, including GGUF, FP8, abliterated ("uncensored"), and MLX variants. In the video generation space, **MiniMax-H3** continues its explosive run with **15.2M downloads** via Comfy-Org's single-file diffusion distribution, while the new **MiniMax-Music3** marks the company's entry into text-to-music (1K+ likes in days). The **DeepSeek-V4** series is also gaining serious traction—**DeepSeek-V4-Flash-0731** crossed 2.3M downloads—signaling a shift toward efficient, high-throughput conversational models. Notably, **Kimi-K3** from Moonshot AI has quietly amassed 10.8K likes with its compressed-tensors feature extraction approach. The overall trend: **frontier open-weight models are being rapidly repackaged** into unbridled fine-tunes and quantized formats for local and enterprise deployment.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why Trending |
|-------|--------|-------|-----------|--------------|
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 633 | 37.6K | Flagship Pro-tier conversational LLM with strong benchmarks. |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3.5K | 2.3M | Fast, lightweight V4 variant optimized for chat throughput. |
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1.1K | 12.7K | Massive MoE model (2.4T total params, 95B active) for text generation. |

### 🎨 Multimodal & Generation (image, video, audio)

| Model | Author | Likes | Downloads | Why Trending |
|-------|--------|-------|-----------|--------------|
| [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11.5K | 1.0M | Flagship vision-language model, top of the leaderboard this week. |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4.2K | 3.1M | State-of-the-art text/image-to-video generation, huge community uptake. |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1K | 13.1K | Breakthrough in AI music composition and generation. |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1.3K | 556K | Multi-format video model (image-to-video, video-to-video). |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1.7K | 430K | Meta's vision-language model with strong conversational + visual skills. |
| [Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 269 | 26.6K | ComfyUI-integrated anime-style text-to-image diffusion model. |
| [MiniMax-H3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 625 | 341K | Fast Turbo variant of MiniMax-H3 for quicker video generation. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why Trending |
|-------|--------|-------|-----------|--------------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10.9K | 2.3M | Compressed-tensor feature extraction model, advanced retrieval/embedding. |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why Trending |
|-------|--------|-------|-----------|--------------|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2.1K | 4.3M | Most popular GGUF quant of the Qwen3.8 vision model. |
| [Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 600 | 1.1M | Official 8-bit FP8 version, ideal for less VRAM. |
| [Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 613 | 60K | Abliterated FP8 variant removing safety filters. |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2.2K | 3.0M | Over-the-top community "uncensored" fine-tune with massive adoption. |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 467 | 767K | Popular GGUF uncensored variant for llama.cpp. |
| [Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 285 | 653K | NVIDIA 4-bit FP4 quant for Blackwell GPUs. |
| [MiniMax-H3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1.4K | 15.2M | ComfyUI single-file distribution, 5x downloads of original. |
| [MiniMax-Music-3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 193 | 325K | ComfyUI integration for music gen. |
| [Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1.3K | 0 | Fixes Qwen chat template bugs in MLX — developer essential. |
| Additional GGUF/abliterated variants | Blackfrost-AI, huihui-ai, orcarouter, HauhauCS, 0bserverx, empero-ai | 160–286 | 26K–245K | Rapid community forking of Qwen3.8 into uncensored/abliterated GGUF formats. |

---

## 3. Ecosystem Signal

The **Qwen ecosystem** is clearly dominant this week: the base **Qwen3.8-27B** spawned over 10 community derivatives (GGUF, FP8, NVFP4, MLX, abliterated, "heretic," etc.), and combined downloads across these variants exceed **6M+**. This suggests Qwen has become the de facto default for open-weight multimodal language models, rivaling Meta's **Muse-Glimmer-30B** and DeepSeek's V4 series. In the video domain, **MiniMax** has momentum; its H3 model already has 15M downloads via ComfyUI-optimized single-file diffusion, indicating the community prefers an easy pipeline over native Diffusers. The open-weight vs proprietary boundary is blurring—**Kimi-K3** (Moonshot) with 10.9K likes shows that Chinese AI labs are aggressively open-sourcing their frontier models. Quantization is no longer a niche: **unsloth** is now shipping NVFP4 (Blackwell-optimized) variants at scale, and 10+ different GGUF versions exist solely for Qwen3.8. The **"uncensored/abliterated" niche has exploded**, with DavidAU, huihui, orcarouter, and Blackfrost competing directly—a sign that safety-refusal-removal is now a mainstream (albeit ethically debated) ecosystem segment.

---

## 4. Worth Exploring

1. **[MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3)** — AI music generation is going mainstream, and this is the first model to hit 1K likes in that category this week. Worth studying for how diffusion is being applied to audio.

2. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10.9K likes and a "compressed-tensors" tag, this is a great case study in efficient feature extraction and retrieval-oriented LLMs. Also has potential for RAG pipelines.

3. **[Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4)** — With Blackwell GPUs becoming the enterprise standard, this is the first frontier-scale model packed in 4-bit FP4 for NVIDIA's newest architecture. For anyone on next-gen servers, this is the sweet spot between performance and VRAM.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*