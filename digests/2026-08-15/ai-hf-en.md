# Hugging Face Trending Models Digest 2026-08-15

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-15 00:30 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-15

## 1. Today's Highlights

This week's trending榜单 is dominated by **two major vectors**: the explosive growth of the **Qwen3.8** family (both dense and MoE variants) and the massive ecosystem buildout around **MiniMax-H3**, a video-generation model that has spawned an entire cottage industry of LoRAs, GGUF conversions, and ComfyUI integrations. **Kimi-K3** from Moonshot AI leads overall in weekly likes (10,672), signaling strong interest in compressed/feature-extraction-capable LLMs. Notably, **NVIDIA's Nemotron-3.5 Lightning** (30B-A3B, both FP4 and BF16) confirms the industry's pivot to hybrid sparse architectures for efficient inference. The presence of multiple **GGUF quantizations** (unsloth's Qwen3.8 and Muse-Glimmer) alongside NVFP4 weights underscores that **quantization is now a first-class concern** for both creators and consumers.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,672 | 1.97M | Moonshot's flagship multimodal LLM with compressed-tensor support; top weekly likes indicates strong community validation. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,383 | 1.61M | Fast, efficient V4 variant optimized for deployment; 1.6M downloads show heavy production adoption. |
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 913 | 3,832 | Massive 2.4T-parameter MoE (95B active) — Qwen's frontier-scale model drawing attention for its scale-to-cost ratio. |
| [**DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 433 | 245 | The premium Pro tier of V4; fewer downloads (recent release) but high anticipation. |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 615 | 124K | Liquid's latest recursively-generated small model — efficient 2.6B with surprising capability density. |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 257 | 119K | 30B total / 3B active hybrid with native NVFP4 4-bit precision — a template for edge-deployable frontier LLMs. |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 143 | 34K | BF16 reference of the Lightning architecture for full-precision training/fine-tuning workflows. |
| [**inclusionAI/Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 235 | 2,283 | Tiny hybrid (bailing_hybrid) model under MIT license — a lightweight option for constrained environments. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 8,972 | 2 | **#2 overall in likes** — Qwen's new multimodal flagship (image+text in/out) despite being a fresh upload. |
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,920 | 1.99M | The video-generation phenomenon of the month — nearly 2M downloads, spawning a full ecosystem. |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,511 | 165K | Meta's 30B image-text-to-text model with 165K downloads — strong demand for open multimodal reasoning. |
| [**LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 855 | 207K | Lightricks' unified video model (i2v, t2v, v2v) — versatile and community-adopted. |
| [**MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 651 | 63 | Text-to-music generation with Diffusers pipeline — early but highly anticipated. |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 493 | 149K | Community turbo variant of H3 for faster generation. |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 381 | 1,366 | Voice-enabled conversational model with multilingual support — new category for NVIDIA. |
| [**Gazingstars123/Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 162 | 10K | Compact text-to-image model (2.9B) for ComfyUI — efficiency-focused image gen. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**dots-studio/dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 138 | 11 | Preview of "dots3" — a note-oriented text-generation model; early-stage but intriguing specialization. |

*No dedicated code/math/medical models cracked the top 30 this week — a notable signal that generalist multimodal and video dominate.*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 788 | 0 | Day-one GGUF of Qwen3.8-27B — unsloth's speed-to-quantization is a benchmark for ecosystem readiness. |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 414 | 596K | 596K downloads — the most-used GGUF of Meta's Muse-Glimmer for consumer hardware. |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,016 | 2.89M | The "uncensored" fine-tune phenomenon — 2.89M downloads proves demand for unfiltered variants. |
| [**meta-models/Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 270 | 228K | Official GGUF from Meta for their own Glimmer model. |
| [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 291 | 0 | Official FP8 weights — quantization support straight from the lab. |
| [**Qwen/Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 184 | 9,334 | FP8 for the massive MoE — makes 2.4T practical on fewer GPUs. |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,317 | **11.77M** | The single most-downloaded model this week — ComfyUI's ready-to-use H3 is the default video-gen entry point. |
| [**larryvrh/MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 741 | 0 | Turbo LoRA for H3 — improves speed without full fine-tune. |
| [**Kijai/MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 339 | 0 | Kijai's ComfyUI wrapper — standard tooling for video workflows. |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 310 | 473 | Stylized fine-tune of H3 with Apache-2.0 license and endpoint compatibility. |
| [**fal/MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 176 | 9,060 | Realism-focused LoRA for human subjects — practical for production use. |
| [**unsloth/MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 156 | 136K | GGUF for H3 — enables CPU/edge video generation. |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 318 | 112K | The most-used Turbo LoRA (112K downloads) with ComfyUI adapter support. |

---

## 3. Ecosystem Signal

**Model families gaining momentum:** The **Qwen3.8** family is the week's clear winner on the LLM/multimodal side — appearing in 5 of 30 slots (dense, MoE, FP8 ×2, GGUF) with the second-highest like count. **MiniMax-H3** has become the **de facto open video-generation platform**, with 11.77M downloads via Comfy-Org alone and a thriving LoRA/GGUF/adapter ecosystem (6+ entries). **NVIDIA's Nemotron** line signals enterprise adoption of hybrid sparse (A3B) architectures with native low-precision support (NVFP4). **Meta's Muse-Glimmer** shows that 30B-scale open multimodal models are increasingly the "sweet spot" for community use.

**Open-weight vs. proprietary:** All 30 models are open-weight — Hugging Face's trending page continues to reflect the open ecosystem's velocity. There is no proprietary API model in the list, confirming that open models now lead in community mindshare, particularly for video generation where open alternatives (LTX-2.5, MiniMax-H3) are matched against proprietary systems.

**Quantization & fine-tuning activity:** Unsloth's pattern of producing **same-day GGUF quantizations** for every major release (Qwen3.8-27B, Muse-Glimmer, MiniMax-H3) has become the ecosystem's "release readiness" benchmark. NVIDIA shipping native NVFP4 alongside BF16 indicates that **hardware-aware precision is moving into official releases**, not just community afterthoughts. The 2.89M-download "uncensored" Qwen fine-tune (DavidAU) reveals persistent demand for unaligned variants, even at the 27B scale.

---

## 4. Worth Exploring

1. **[NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4)** — Study this model to understand the **future of efficient inference**: 30B total / 3B active with native 4-bit precision is the architectural direction every lab is moving toward. Ideal for benchmarking cost-per-token vs. quality.

2. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — With 11.77M downloads, this is the **most-used model on the platform this week**. Even if you're not a video-generation user, examining its diffusion-single-file format and ComfyUI integration reveals the template for how multimodal models should be packaged for the community.

3. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The top-liked model (10,672) with **compressed-tensor** support. Kimi's approach to compressed weights is a differentiated technical direction worth studying — it may represent an alternative to traditional quantization for reducing memory footprint while retaining quality.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*