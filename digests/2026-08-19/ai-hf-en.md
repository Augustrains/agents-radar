# Hugging Face Trending Models Digest 2026-08-19

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-19 00:30 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-19

---

## 1. Today's Highlights

The Hugging Face Hub is dominated this week by **Qwen 3.8** — a massive multimodal release from Alibaba — with over **11K likes** on the base model and a sprawling ecosystem of quantizations, uncensored fine-tunes, and chat-template fixes. In parallel, **MiniMax-H3** has become a video-generation powerhouse, pulling in 2.8M downloads and serving as the base for community single-file diffusion ports and uncensored fine-tunes. **DeepSeek V4** continues its momentum with the Pro and Flash variants, while **Moonshot's Kimi-K3** quietly amassed 10.8K likes as a compressed-tensor multimodal model. Notably, the ecosystem shows a strong "community layer" trend: GGUF quantizations, uncensored variants, and ComfyUI-compatible ports often see 10–100x more downloads than their source models.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,066 | 11,212 | A massive 2.4T-parameter MoE (95B active) text-generation model — the flagship of Qwen 3.8's text-only lineup. |
| [**DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 601 | 30,985 | The latest Pro iteration of DeepSeek's V4 series, pushing frontier reasoning performance for open weights. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,527 | 2,123,462 | The fast, efficient sibling of V4-Pro — widely downloaded as a strong day-to-day chat and coding model. |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,826 | 2,226,898 | Moonshot's multimodal model with compressed-tensor support — nearly as popular as Qwen 3.8 in likes. |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 322 | 269,372 | NVIDIA's efficient 30B MoE (3B active) with NVFP4 quantization — a top pick for low-latency serving. |
| [**Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 319 | 9,990 | A tiny hybrid-model from inclusionAI, exploring efficient architectures for conversational AI. |
| [**dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 220 | 1,120 | A preview of Dots' note-oriented text-generation model — early community interest in workflow-specific models. |

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,127 | 665,513 | The flagship omni-modal 27B model — image+text in, text out. The most-liked model on the Hub this week. |
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,143 | 2,855,539 | MiniMax's state-of-the-art video generation model — the standard base for both official and community video pipelines. |
| [**MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 958 | 11,745 | A dedicated text-to-music diffusion model — early but strong interest in AI music generation. |
| [**LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,222 | 503,632 | Lightricks' fast video generation model supporting image-to-video, text-to-video, and video-to-video. |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,682 | 384,097 | Meta's powerful 30B multimodal (image+text→text) model — a direct competitor to Qwen3.8-27B. |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 608 | 300,279 | A lightweight Turbo variant of MiniMax-H3 optimized for faster inference in video tasks. |
| [**Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 248 | 24,893 | A single-file diffusion model for anime-style text-to-image generation in ComfyUI. |
| [**10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 264 | 0 | A community fine-tune of MiniMax-H3 for uncensored text-to-video content — zero downloads yet but notable interest. |

### 🔧 Specialized Models (Code, Math, Medical, Embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**LFM2.5-VL-3B**](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 173 | 9,101 | Liquid AI's efficient 3B vision-language model — a strong small-model signal for edge VL deployments. |
| [**Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 562 | 741,011 | Official FP8 quantization of Qwen3.8-27B — the go-to balanced precision/quality variant for serving. |

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,817 | 3,561,466 | Unsloth's GGUF pack — the most downloaded Qwen 3.8 variant, enabling local CPU/GPU inference. |
| [**Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 528 | 45,465 | An abliterated (uncensored) FP8 version of Qwen3.8-27B — trending for creative/NSFW use cases. |
| [**Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 410 | 558,767 | GGUF-packaged uncensored Qwen 3.8 with multi-token prediction (MTP) — very popular for local use. |
| [**Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 263 | 0 | MLX-format uncensored model for Apple Silicon — early signal of Mac-native adoption. |
| [**Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,255 | 0 | A no-model repository fixing Qwen 3.5/3.8 chat templates (Jinja/MLX) — huge community need signal. |
| [**Qwen3.8-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.8-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,140 | 3,020,528 | A heavily fine-tuned, uncensored Qwen 3.8 GGUF with MTP — the "gourmet" community fine-tune, viral in local-LLM circles. |
| [**Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 200 | 27,745 | Another aggressive uncensored GGUF variant, pushing MTP-enabled creative writing. |
| [**Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 172 | 12,854 | A "Ridge"-tuned Qwen3.8 GGUF focusing on creative writing style. |
| [**Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 262 | 523,919 | Unsloth's NVFP4 quantization of Qwen3.8-27B — optimized for NVIDIA Blackwell. |
| [**Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 481 | 787,276 | GGUF of Meta's Muse-Glimmer-30B — bringing Meta's multimodal to local runtimes. |
| [**Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 225 | 13,344 | Official FP8 of the giant MoE — for those who need frontier quality with vLLM-scale serving. |
| [**MiniMax-H3 (Comfy-Org port)**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,425 | 14,641,908 | The single-file ComfyUI port of MiniMax-H3 — the most-downloaded video model this week by far. |
| [**MiniMax-Music-3 (Comfy-Org port)**](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 177 | 285,444 | ComfyUI single-file port of MiniMax-Music3, making music generation accessible in node workflows. |

---

## 3. Ecosystem Signal

**Qwen is the center of gravity.** The Qwen 3.8 family (27B, 2.4T-A95B, FP8, GGUF, uncensored) represents the largest single-model ecosystem on the Hub — and the community has moved fast to build quantization and fine-tune layers on top. The **"uncensored" sub-ecosystem** is a powerful signal: abliterated Qwen variants routinely out-download the original in GGUF form, with special "aggressive" and "heretic" fine-tunes catering to creative/uncensored writing.

**Video generation has shifted to MiniMax.** MiniMax-H3 has effectively replaced earlier open video models as the default base, with Comfy-Org ports seeing 14.6M downloads. Its dominance in the "single-file diffusion" space is unchallenged.

**Multimodal (image-text-to-text) is the new battleground.** Qwen3.8-27B, Muse-Glimmer-30B, and Kimi-K3 all combine vision+language, and they dominate the likes chart. Pure text LLMs (DeepSeek V4, Nemotron) are still relevant but are being eclipsed by omni-modal models.

**Open weight is winning.** All top-30 models are open-weight. MoE efficiency (A95B, A3B), NVFP4, FP8, and GGUF are the standard serving formats, with Unsloth and Comfy-Org as the infrastructure layer enabling local adoption.

---

## 4. Worth Exploring

1. **[Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — The flagship multimodal model of the week. If you study one model, study this: it represents the current ceiling of open omni-modal quality at 27B scale, and the surrounding ecosystem (GGUF, FP8, uncensored) shows what a healthy open model community looks like.

2. **[MiniMax-H3 — Comfy-Org port](https://huggingface.co/Comfy-Org/MiniMax-H3)** — With 14.6M downloads, it's the most-accessed generation model on the Hub right now. Understanding why it dominates (single-file, ComfyUI-ready, high quality) is key to reading the video-gen landscape.

3. **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — A deceptively simple no-model repo that gained 1,255 likes in a week. It highlights a real pain point (chat template fragmentation in MLX/Jinja ecosystem) and is a great example of "infrastructure as a model" — worth studying as a community-driven fix pattern that HF rewards.

---

*Report generated for 2026-08-19 | Source: Hugging Face Hub trending models (top 30 by weekly likes)*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*