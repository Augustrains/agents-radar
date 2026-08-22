# Hugging Face Trending Models Digest 2026-08-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-22 00:29 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-22

---

## 1. Today's Highlights

The Hugging Face ecosystem is being dominated by the **Qwen3.8-27B** family, which accounts for over half of today's trending list with an explosive mix of official releases, GGUF quantizations, and community abliterated variants. **Qwen/Qwen3.8-27B** leads with nearly 12K likes, while the **GGUF quantization by unsloth** has already surpassed 5.8M downloads—a clear signal that efficient local deployment is the top priority for the community. On the video front, **MiniMax-H3** continues its viral run with 3.6M downloads and 4.3K likes, solidifying MiniMax's position as a serious challenger in the text-to-video space. **DeepSeek-V4** makes a strong appearance with two entries, indicating growing momentum behind the V4 architecture family. The "abliteration" (uncensoring) trend is remarkably visible, with at least 8 abliterated variants of Qwen3.8-27B trending simultaneously.

---

## 2. Trending Models by Category

### 🧠 Language Models

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,961 | 1,726,651 |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,913 | 2,448,810 |
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 708 | 49,601 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,609 | 2,833,064 |
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,139 | 15,702 |
| [Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 288 | 9,165 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 190 | 1,136 |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,738 | 505,113 |

**Qwen3.8-27B** is the flagship multimodal LLM from Qwen, setting new standards for open-weights performance with image-text-to-text capabilities and a massive following. **Kimi-K3** from Moonshot AI is rising fast with 10.9K likes, featuring compressed-tensors for efficient deployment. **DeepSeek-V4-Flash** and **V4-Pro** show DeepSeek's dual strategy: a fast-efficient variant and a full-strength pro model. **Qwen3.8-2.4T-A95B** is a massive MoE with 2.4T total parameters (95B active), pushing the frontier of open-weight scaling. **Muse-Glimmer-30B** is Meta's new multimodal model entry making waves with 1.7K likes.

---

### 🎨 Multimodal & Generation

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,294 | 3,614,443 |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,489 | 654,175 |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,163 | 15,678 |
| [10Eros-Max](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 311 | 0 |

**MiniMax-H3** is the dominant video generation model—a diffusion-based image-text-to-video model with massive community adoption for both personal and commercial workflows. **LTX-2.5** from Lightricks is a versatile video model supporting image-to-video, text-to-video, and video-to-video transformation. **MiniMax-Music3** extends MiniMax's creative suite into music generation, a fast-growing category. **10Eros-Max** is a community fine-tune of MiniMax-H3, showing a growing ecosystem of specialized video generation models.

---

### 🔧 Specialized Models

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 205 | 123,237 |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 174 | 21,092 |

**Ornith-1.5-35B-A3B-GGUF** is an efficient MoE model with quantized checkpoint, MIT-licensed and endpoint-compatible—ideal for production deployment. **Qwen3.8-27B-DFlash2** introduces speculative decoding acceleration, a specialized optimization that speeds up inference.

---

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,503 | 5,804,917 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 818 | 107,520 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 818 | 18,193 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 660 | 1,939,895 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 328 | 1,013,917 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 566 | 1,126,222 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 440 | 123,956 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 421 | 357,225 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 231 | 338,221 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 229 | 17,521 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 293 | 68,275 |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 237 | 74,038 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,370 | 0 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 211 | 421,918 |
| [Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) | Blackfrost-AI | 201 | 197,667 |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 169 | 155,208 |

This category is dominated by Qwen3.8-27B community variants. **unsloth's GGUF** is the top quantized checkpoint with a staggering 5.8M downloads. The **abliteration** (safety-removal) trend is massive—at least 7 independent teams have released uncensored versions, with orcarouter, huihui-ai, and Blackfrost-AI leading. **Qwen's official FP8** quantization has also hit 1.9M downloads. **froggeric/Qwen-Fixed-Chat-Templates** is a lightweight, high-impact utility (1.3K likes, 0 downloads) that fixes chat template issues across the Qwen family.

---

## 3. Ecosystem Signal

**Qwen is the undisputed ecosystem leader.** The Qwen3.8-27B family alone accounts for 17 of the 30 trending models, spanning official releases, official quantizations, and dozens of community fine-tunes. The sheer scale of derivative work—quantizations, abliterations, and optimizations—signals a deeply healthy third-party ecosystem around Qwen models.

**The abliteration wave is notable.** At least 8 uncensored variants of Qwen3.8-27B are trending simultaneously, suggesting strong community demand for models with fewer safety constraints. This is a recurring pattern in the open-weight ecosystem that continues to grow.

**Efficient deployment is paramount.** GGUF quantizations by unsloth and others are seeing download counts in the millions—far exceeding the original full-precision model downloads. FP8 and NVFP4 formats are also gaining traction for high-end GPU inference.

**MoE architectures are gaining momentum.** Qwen3.8-2.4T-A95B and Ornith-1.5-35B-A3B both employ Mixture-of-Experts designs, offering large knowledge capacity with reduced inference costs.

**MiniMax is a rising challenger.** Beyond H3's video dominance, MiniMax-Music3 signals expansion into audio generation, positioning them as a multi-modal creative AI company competing directly with DeepSeek, Qwen, and Moonshot AI.

**Speculative decoding and optimization** (z-lab's DFlash2, MTP variants) suggests the community is performance-hungry and actively seeking inference speedups beyond simple quantization.

---

## 4. Worth Exploring

1. **Qwen/Qwen3.8-27B** — The flagship model at the center of the ecosystem. It's the clear frontrunner for open-weights multimodal performance, and the massive community around it (quantizations, fine-tunes, abliterations) means you'll have a rich ecosystem of tools and resources to build with.

2. **moonshotai/Kimi-K3** — With 10.9K likes and 2.4M downloads, this is the fastest-rising non-Qwen model. Its use of compressed-tensors is an interesting approach to efficiency that could signal the next wave of model optimization beyond traditional quantization.

3. **MiniMaxAI/MiniMax-H3** — The most beloved video generation model in the open ecosystem (4.3K likes, 3.6M downloads). If you're exploring generative video, this is the community's proven choice—and it now has a growing fine-tune ecosystem (like 10Eros-Max) for specialized use cases.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*