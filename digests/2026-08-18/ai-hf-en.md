# Hugging Face Trending Models Digest 2026-08-18

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-18 00:29 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-18

---

## 1. Today's Highlights

The ecosystem is dominated by two super-clusters: **Qwen 3.8** (led by the 27B flagship with 10.7K likes) and **MiniMax-H3** (the video-generation model powering Comfy-Org's 14M-download single-file release). Notably, **Kimi K3** from Moonshot AI has surged to 10.8K likes with 2.1M downloads, signaling a strong open-weight push from Chinese labs. Quantization is pervasive—GGUF, FP8, and NVFP4 variants of top models are consistently out-downloading their base versions. Meanwhile, the appearance of two NVIDIA Nemotron entries and LiquidAI's small LFM models points to a healthy mix of enterprise and efficiency-focused releases.

---

## 2. Trending Models by Category

### 🧠 Language Models

| Model | Author | Likes / Downloads | Why It's Trending |
|---|---|---|---|
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 573 / 25K | Flagship reasoning model from DeepSeek, riding on V4 momentum. |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,497 / 1.98M | Fast, distilled V4 variant; the community's go-to for low-latency inference. |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 307 / 231K | 30B MoE (3B active) in NVIDIA's NVFP4 format; enterprise-grade efficiency. |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 169 / 70K | BF16 reference version of the same Nemotron MoE; targets high-end GPUs. |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 653 / 147K | Liquid's efficient small model with liquid neural network lineage; strong per-parameter performance. |
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,041 / 9.5K | Massive 2.4T MoE flagship; for those with serious compute. |

### 🎨 Multimodal & Generation

| Model | Author | Likes / Downloads | Why It's Trending |
|---|---|---|---|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,802 / 2.16M | Moonshot's new multimodal flagship; the largest like-count of any non-Qwen model. |
| [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 10,711 / 415K | The week's most-liked vision-language model; dense 27B with broad capability. |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,087 / 2.4M | Next-gen video model; the standard for text/image-to-video generation. |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,108 / 466K | Lightricks' image-to-video gen model; strong quality with single-file distribution. |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 904 / 10K | Newest music generation model with diffusers support. |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,661 / 334K | Meta's 30B vision-language model; blends image understanding with generation. |
| [Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 584 / 264K | Fast, Turbo-distilled version of H3 for real-time video. |
| [Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 233 / 23K | Compact text-to-image diffusion model; indie release for ComfyUI. |
| [LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 162 / 6.8K | Liquid's small vision-language model; efficient multimodal option. |
| [MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 243 / 18.5K | Community LoRA focused on realistic human rendering for H3 video. |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 786 / 0 | Early-access Turbo LoRA for H3; just released with audio-video support. |

### 🔧 Specialized Models

| Model | Author | Likes / Downloads | Why It's Trending |
|---|---|---|---|
| [Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 306 / 6.3K | Hybrid-architecture tiny model with MIT license; open and permissive. |
| [dots3-note-prev](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 207 / 633 | Preview of dots3 note-taking model; strong in long-context summarization. |
| [Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,211 / 0 | Fixed Jinja chat templates for Qwen3.5; dev-tool that solves a real pain point. |

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes / Downloads | Why It's Trending |
|---|---|---|---|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,628 / 2.73M | The most-downloaded quantization of the week; GGUF for llama.cpp users. |
| [Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 240 / 378K | NVFP4 quantization for Blackwell GPUs; efficiently packed by unsloth. |
| [Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 529 / 496K | Official FP8 release from Qwen; strong quality retention. |
| [Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 220 / 12K | FP8 MoE variant for the giant 2.4T model. |
| [Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 436 / 15.8K | Abliterated FP8 variant; community-favorite for "uncensored" use. |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 299 / 358K | GGUF version of the uncensored Qwen; multimodal-capable. |
| [Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 470 / 755K | GGUF of Meta's Muse-Glimmer; top-tier pick for local vision-language models. |
| [MiniMax-H3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,403 / 14M | 14M downloads! The go-to single-file distribution for ComfyUI video workflows. |
| [MiniMax-Music-3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 167 / 257K | ComfyUI-packaged Music3 for music generation. |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,119 / 3.03M | Community mega-fine-tune of Qwen with a maximalist uncensored personality; MTP support. |

---

## 3. Ecosystem Signal

**Qwen 3.8 is the clear center of gravity** — the family appears in base, FP8, NVFP4, GGUF, and multiple community fine-tunes, with the 27B dense model serving as the community's default "good enough" multimodal checkpoointed. **Moonshot Ai's Kimi K3** broke through with the highest like-count of the week, validating open-weight releases from Chinese labs as a genuine competitive force.

**Video generation is the fastest-moving modality.** MiniMax-H3 dominates with an enormous support ecosystem—Turbo distills, realism LoRAs, Comfy-Org single-file distributions, all hitting hundreds of thousands to millions of downloads. The pattern is now standard: lab releases base model → community rushes to quantize, distill, and wrap for ComfyUI.

**Quantization is no longer an afterthought—it's the primary consumption path.** For Qwen3.8-27B, unsloth's GGUF has 6.5x the downloads of the base model. NVFP4 is emerging as the new hot format for Blackwell hardware users.

**Efficiency is a theme.** NVIDIA, LiquidAI, and inclusionAI all released sub-30B or highly-sparse MoE models targeting cost-conscientious enterprises rather than researchers.

---

## 4. Worth Exploring

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The highest-liked new model of the week, and a rare look at Moonshot's open-weight strategy. K3 uses compressed tensors and supports feature extraction, making it ideal for teams evaluating efficient, high-quality multimodal baselines beyond the Qwen ecosystem.

2. **[Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — With 2.7M downloads, this is *the* reference for "what does the community actually run locally right now?". If you're building on Qwen3.8, this quantized variant is your benchmark for quality-vs-resource tradeoffs.

3. **[MiniMax-H3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-H3)** — At 14M downloads, it's the single most-downloaded video model on the Hub. Even if you're not a ComfyUI user, studying how Comfy-Org packages distributed models (single-file diffusion, base_model tags, license strategy) is worthwhile for anyone distributing large generative models.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*