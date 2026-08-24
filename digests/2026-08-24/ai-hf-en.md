# Hugging Face Trending Models Digest 2026-08-24

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-24 00:31 UTC

---

# Hugging Face Trending Models Digest — 2026-08-24

## 1. Today's Highlights

The Hugging Face hub is **dominated by the Qwen3.8-27B ecosystem**, with 15 of the 30 top models being either the base model or its derivatives (GGUF quantizations, abliterated versions, FP8 variants, and speculative decoding versions). The community's obsession with **uncensored/abliterated variants** of this model is unprecedented, with at least 8 distinct community versions trending simultaneously. Beyond Qwen, major releases include **DeepSeek-V4 Flash**, **Kimi K3**, **MiniMax-H3** (video generation), and **Lightricks LTX-2.5** (image-to-video)—indicating a robust week for both large-scale language models and generative media models. Community infrastructure, especially **GGUF quantization** (via unsloth and llama.cpp) and **chat-template fixes**, is also generating significant interest.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) — Qwen | 12,313 likes | 2.36M downloads — The flagship multimodal 27B model from Alibaba, trending as the foundation for the entire week's derivatives.
- [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — deepseek-ai | 3,652 likes | 3.09M downloads — DeepSeek's fast, conversational V4 variant, trending for its strong performance-to-speed ratio.
- [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — moonshotai | 10,950 likes | 2.73M downloads — Kimi's compressed-tensor multimodal model, notable for its unique feature-extraction architecture.
- [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) — deepseek-ai | 734 likes | 57.9K downloads — The heavy-duty Pro counterpart to Flash, gaining traction among enterprise users.
- [**ornith-ai/Ornith-1.5-35B-A3B**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) — ornith-ai | 364 likes | 23.5K downloads — A 35B MoE model with only 3B active params, showing the MoE efficiency trend.
- [**ornith-ai/Ornith-1.5-9B**](https://huggingface.co/ornith-ai/Ornith-1.5-9B) — ornith-ai | 182 likes | 31.5K downloads — The smaller 9B sibling in the MIT-licensed Ornith series.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — MiniMaxAI | 4,378 likes | 4.04M downloads — MiniMax's flagship image/video generation model, dominating the text-to-video and image-to-video pipelines.
- [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) — Lightricks | 1,641 likes | 738K downloads — The latest LTX video model, trending for its dual image-to-video and video-to-video capabilities.
- [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) — MiniMaxAI | 1,205 likes | 17.4K downloads — A music generation model built on diffusers, exploring a niche but rapidly-liked modality.

### 🔧 Specialized Models (code, math, embeddings, etc.)

- [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) — froggeric | 1,420 likes | 0 downloads — A meta-model providing corrected Qwen chat templates (jinja/mlx), proving that developer infrastructure can trend.
- [**peculiar-ragdoll/Qwen-Sharp-Chat-Templates**](https://huggingface.co/peculiar-ragdoll/Qwen-Sharp-Chat-Templates) — peculiar-ragdoll | 199 likes | 0 downloads — Similar template-fix effort, competing for developer mindshare.
- [**superwhisper/s1-mini**](https://huggingface.co/superwhisper/s1-mini) — superwhisper | 214 likes | 2.3K downloads — A small Qwen-based model exploring the ASR (speech recognition) space.
- [**z-lab/Qwen3.8-27B-DFlash2**](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) — z-lab | 202 likes | 36.2K downloads — A speculative-decoding derivative of Qwen for faster inference, along with [**incoai/Qwen3.8-27B-DFlash2**](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2) — incoai | 162 likes | 69.8K downloads — showing the demand for inference optimizations.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) — unsloth | 2,738 likes | 6.67M downloads — The canonical GGUF quantization of Qwen3.8-27B, by far the most-downloaded derivative this week.
- [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) — Qwen | 672 likes | 2.65M downloads — Official FP8 precision variant for efficient serving.
- [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) — orcarouter | 953 likes | 47.1K downloads — Apple Silicon MLX abliterated version, driving the uncensored trend on Mac hardware.
- [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) — orcarouter | 1,047 likes | 190K downloads — FP8 quantized uncensored variant for high-throughput deployments.
- [**OBLITERATUS/Qwen3.8-27B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) — OBLITERATUS | 632 likes | 244.8K downloads — Multi-format (MLX/GGUF) abliterated release from the "OBLITERATUS" brand.
- [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) — JonathanColetti | 648 likes | 1.33M downloads — GGUF with MTP (multi-token prediction) support, a highly-downloaded uncensored option.
- [**orcarouter/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) — orcarouter | 375 likes | 108.7K downloads — Another GGUF variant from orcarouter, reinforcing their presence.
- [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) — HauhauCS | 538 likes | 676.7K downloads — An "aggressive" MTP-enabled uncensored GGUF for performance-heavy community use.
- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) — huihui-ai | 297 likes | 943.4K downloads — huihui-ai's popular abliterated GGUF, continuing their pattern of successful community quantizations.
- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) — huihui-ai | 258 likes | 24.8K downloads — The non-GGUF (full safetensors) version of the same abliterated model.
- [**ornith-ai/Ornith-1.5-35B-A3B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) — ornith-ai | 252 likes | 369.5K downloads — GGUF for the efficient MoE model, making Ornith accessible on consumer hardware.
- [**ornith-ai/Ornith-1.5-9B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) — ornith-ai | 176 likes | 359.1K downloads — GGUF version of the 9B Ornith model, MIT-licensed and endpoints-compatible.
- [**DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) — DavidAU | 209 likes | 193.8K downloads — An experimental "GAIN/COLD-FUSION" training GGUF, representing niche high-end community experiments.
- [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) — empero-ai | 250 likes | 131.4K downloads — A llama.cpp quantized variant focusing on "Ridge" quality optimizations.
- [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) — 0bserverx | 245 likes | 579.3K downloads — "Heretic" branded abliterated GGUF, one of the many uncensored variants trending.
- [**LBH-123-AI/Minimax_h3_latent_Upscaler**](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) — LBH-123-AI | 166 likes | 0 downloads — Community upscaler for MiniMax-H3 outputs (regional US tag).

## 3. Ecosystem Signal

**Qwen is the undisputed ecosystem ruler this week**, with the Qwen3.8-27B family capturing ~50% of trending slots. This signals Alibaba's successful open-weight strategy: releasing a single strong multimodal base has catalyzed a massive community industry of quantizations (GGUF, FP8, MLX), ablations, and inference optimizations (MTP, DFlash2). The **uncensored/abliterated sub-ecosystem is especially vibrant**, with at least 8 unique community variants — this persists as a significant driver of open-weight adoption, as users seek to customize model behavior without restrictions.

**Open-weight models are clearly winning the trending charts** vs. proprietary alternatives, with DeepSeek, ornith-ai, and Moonshot all releasing competitive products that seamlessly integrate with the Hugging Face ecosystem. **MoE (Mixture-of-Experts) is emerging as the efficiency architecture of choice** — the Ornith-1.5-35B-A3B model delivers flagship-class capability with only 3B active parameters, making frontier-like performance accessible on desktop hardware. **Video generation is the modality of the moment** (MiniMax-H3, LTX 2.5), though music generation (MiniMax-Music3) is gaining traction. Inference infrastructure remains a key differentiator: massive downloads for GGUF/llama.cpp quantizations show that local deployment is a top priority for the community.

## 4. Worth Exploring

1. **[orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8)** — The combination of FP8 quantization (efficient serving) with abliteration (uncensored) represents the sweet spot for deploying a community-customized Qwen at scale. With over 1,000 likes, it's the most-liked Qwen derivative, indicating strong community validation.

2. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — With 4M+ downloads, this is the week's breakthrough in video generation. As image-to-video and text-to-video models approach production quality, H3 is the one to study for anyone building generative media applications.

3. **[ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B)** — This MoE model with 3B active parameters challenges the assumption that you need massive hardware to run frontier models. It represents a preview of the "efficient frontier" approach that will likely define the next generation of open-weight releases.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*