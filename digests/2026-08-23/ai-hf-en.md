# Hugging Face Trending Models Digest 2026-08-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-23 00:32 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-23

---

## 1. Today's Highlights

The Hugging Face ecosystem is heavily dominated by **Qwen3.8-27B**, with the base model and its derivative quantizations, abliterations, and fine-tunes occupying over half of the top 30 trending list. The **uncensored/abliterated** variant ecosystem around Qwen is particularly active, with at least 8 community fine-tunes and quantizations trending simultaneously. Beyond Qwen, the release of **Kimi-K3** (10.9K likes) and **MiniMax-H3** (4.3K likes) marks significant momentum for non-Qwen foundation models, while **DeepSeek-V4** family shows strong adoption, especially the Flash variant with nearly 3M downloads. Video generation (LTX-2.5, MiniMax-H3) and music generation (MiniMax-Music3) continue to expand the multimodal frontier.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,134 | 2.09M | The flagship 27B multimodal LLM from the Qwen team — currently the most-liked model on the hub with broad adoption across image-text-to-text tasks. |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 320 | 12.6K | A sparse MoE model (35B total, 3B active) built on Qwen-style architecture, gaining attention for its efficiency. |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 718 | 54.6K | The premium tier of DeepSeek's V4 generation, offering higher capability at the cost of more compute. |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,630 | 2.98M | The fast, efficient DeepSeek V4 variant — massive download count signals strong production usage. |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,146 | 17.4K | Qwen's massive 2.4T-parameter MoE model (95B active) — frontier-scale open-weight offering. |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,926 | 2.61M | Moonshot AI's latest multimodal flagship with compressed-tensor support — second most-liked model this week and a major challenger to Qwen. |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,755 | 517K | Meta's new 30B multimodal model, quickly gaining traction in the community. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,564 | 694K | State-of-the-art video generation model supporting image-to-video, text-to-video, and video-to-video in a single diffusion model. |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,181 | 16.6K | Novel text-to-music generation model from MiniMax, expanding the audio frontier. |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,337 | 3.90M | MiniMax's flagship video model with massive download numbers — dominates the video generation space. |
| [10Eros-Max](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 316 | 0 | Community fine-tune on MiniMax-H3 for specialized video generation; note the "NSFW" implied name signals a niche-but-active segment. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,397 | 0 | A resource model with corrected Jinja chat templates for Qwen models — highly liked despite zero downloads, filling a community pain point. |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 202 | 1.9K | Small ASR-focused model built on Qwen3 architecture, exploring speech recognition with LLM backbones. |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 193 | 29.7K | Speculative-decoding optimized variant of Qwen3.8, aiming for faster inference. |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,623 | 6.32M | The most-downloaded model on the hub this week — unsloth's optimized GGUF quantization of Qwen3.8-27B. |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 885 | 34.9K | Apple MLX-format abliterated (uncensored) variant of Qwen for local Mac deployment. |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 988 | 142.8K | FP8-precision abliterated version — popular for high-efficiency serving of uncensored models. |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 531 | 164.9K | Multi-format (MLX + GGUF) abliterated Qwen, a hallmark of the uncensored movement. |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 485 | 486K | Aggressive MTP (multi-token prediction) GGUF fine-tune — heavily downloaded for local multimodal use. |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 623 | 1.22M | Another popular GGUF uncensored variant, with llama.cpp support and MTP. |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 336 | 85.4K | GGUF version of the orcarouter abliterated series. |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 254 | 635K | The huihui-ai abliteration lineage, one of the most trusted names in uncensored models, now in GGUF. |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 246 | 21.6K | Original safetensors version of huihui's abliterated Qwen. |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 244 | 97.2K | Empero's specialized GGUF quantization focused on "ridge" quality. |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 189 | 176.9K | Experimental "Cold-Fusion" + "GAIN Training" GGUF — niche but notable for community innovation. |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 226 | 505K | "Heretic" abliteration variant — the naming signals a more aggressive regression-removal approach. |
| [empero-ai/Qwen3.8-9B-Distill](https://huggingface.co/empero-ai/Qwen3.8-9B-Distill) | empero-ai | 164 | 9.3K | A 9B distilled version of Qwen3.8 for lighter deployments. |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 232 | 173.9K | GGUF quant of the efficient MoE model — making it accessible to local users. |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 664 | 2.31M | Official FP8 quantization from Qwen — a strong signal that FP8 is now standard for production serving. |
| [LBH-123-AI/Minimax_h3_latent_Upscaler](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) | LBH-123-AI | 159 | 0 | Community tool for upscaling MiniMax H3 latents, showing appetite for video post-processing. |

---

## 3. Ecosystem Signal

**Qwen3.8-27B is the center of gravity** — of the 30 trending models, 18 are Qwen3.8 variants. This is an unprecedented concentration around a single base model. The abliteration/uncensored ecosystem is thriving with at least 8 distinct community variants, indicating strong demand for alignment-removed models running on local hardware (MLX, GGUF). **Open-weight clearly dominates** — every trending model is open-weights, with no proprietary API-only models in sight. This suggests provider-led open-weight releases (Qwen, DeepSeek, Kimi) are the current primary innovation vector.

**Quantization is a massive industry**: GGUF variants from unsloth, huihui-ai, orcarouter, and others — with **unsloth's GGUF hitting 6.3M downloads** — show that local deployment is the primary consumer pattern. The popularity of FP8 (from both Qwen official and community) points toward FP8 becoming the standard for server-side inference. Emerging **multimodal open models** (MiniMax-H3 video, LTX-2.5, Kimi-K3) signal that the frontier is moving from text-only to video and music generation at scale.

**MoE is mainstream**: Qwen's 2.4T-A95B, Ornith-1.5-35B-A3B, and DeepSeek V4 models all use MoE architecture, with the community embracing them for their efficiency. The "small active params, huge total params" pattern is now the default for frontier open models.

---

## 4. Worth Exploring

1. **[unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — 6.3M downloads in a week makes this the single most-used open-weight model artifact. Understanding why unsloth's quantization pipeline is so trusted (and the ecosystem around it — llamafile, native llama.cpp) is essential for anyone building local AI products.

2. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — second most-liked model with 10.9K likes and 2.6M downloads. Its "compressed-tensors" tag signals a new approach to model efficiency, and it's the only credible challenger to Qwen's dominance. Watch this one for architecture innovation.

3. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — the fastest path to high-quality video generation from open weights, with 3.9M downloads. Paired with the trending community upscaler (LBH-123-AI) and fine-tunes (10Eros-Max), it demonstrates the full lifecycle of what an open video model ecosystem looks like — worth studying as a template for how open-weight first-party models + community derivatives mature.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*