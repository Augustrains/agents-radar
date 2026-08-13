# Hugging Face Trending Models Digest 2026-08-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-13 00:54 UTC

---

# Hugging Face Trending Models Digest — 2026-08-13

---

## 1. Today's Highlights

The Hugging Face hub is buzzing with major releases: **Kimi-K3** from Moonshot AI dominates the week with 10.5K likes and 1.5M downloads, confirming the massive appetite for large multimodal conversational models. Meanwhile, **DeepSeek-V4-Flash-0731** shows remarkable momentum with over 1M downloads, and the viral **MiniMax-H3** ecosystem continues to expand rapidly with numerous community fine-tunes (LoRA adapters, ComfyUI integrations, GGUF quantizations) making it the most actively hacked-on model family of the week. Notably, **NVIDIA's Nemotron-3.5-Lightning** series and **Qwen's 2.4T-parameter MoE** are pushing the boundaries of efficiency with sparse activation and FP4 quantization, signaling a strong shift toward deployment-ready LLMs. The week also sees a surge in "uncensored" and creative fine-tunes (e.g., DavidAU's Fable Fusion), alongside emerging Chinese open-weight contenders like **Ling-3.0** and **maple-preview**.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,583 | 1,565,484 | Flagship multimodal conversational model with compressed-tensors optimization — the week's breakout hit. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,238 | 1,048,685 | Fast, flash-preview LLM that's racking up massive real-world adoption. |
| [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 498 | 978 | Massive 2.4T-parameter MoE with only 95B active parameters — frontier efficiency research. |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 582 | 93,668 | Small-but-capable liquid foundation model — popular for edge and research. |
| [**deepgrove/maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 346 | 2,049 | New causal MoE model — early community buzz around its architecture. |
| [**inclusionAI/Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 318 | 6,148 | Hybrid-architecture flash model from a rising Chinese lab. |
| [**inclusionAI/Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 189 | 0 | Tiny sibling of Ling-3.0 — picks up interest for lightweight deployment. |
| [**Qwen/Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 114 | 3,851 | FP8 quantized variant of the giant MoE — signals demand for deployable frontier models. |

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,716 | 83,484 | Official text/image-to-video frontier model with 4M+ ecosystem downloads via Comfy port. |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,294 | 0 | Meta's 30B image-text-to-text conversational model — major new release. |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 567 | 39 | Versatile video diffusion model covering i2v, t2v, and v2v. |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 411 | 20,376 | Community-optimized Turbo variant of MiniMax-H3 for faster generation. |
| [**endless-frontier/BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 182 | 708 | Qwen3.5_MoE-based image-text-to-text model — new multimodal contender. |
| [**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 352 | 653 | NVIDIA's 11B voice chat model with recent ARXIV papers — voice AI gaining steam. |

---

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 204 | 19,250 | 30B with 3B active + NVFP4 quantization — efficiency-focused MoE for production. |
| [**nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 116 | 15,740 | BF16 reference version of the 3B-active MoE. |

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,258 | 6,798,796 | ComfyUI single-file port of MiniMax-H3 — the most-downloaded model this week by far. |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,955 | 2,521,093 | Aggressively fine-tuned, "uncensored" Qwen3.6 GGUF with massive community pull. |
| [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 666 | 207,990 | Unsloth's optimized GGUF of the week's most popular LLM. |
| [**larryvrh/MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 701 | 0 | LoRA adapter for MiniMax-H3-Turbo — early but strong community interest. |
| [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 477 | 0 | INT8 quantized + H3-tuned Qwen3-VL for ComfyUI workflows. |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 358 | 0 | Unsloth GGUF conversion of Meta's new Muse-Glimmer 30B. |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 301 | 0 | ComfyUI-packaged LoRA for MiniMax-H3-Turbo — accessibility driver. |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 287 | 0 | Apache-2.0 community style fine-tune of MiniMax-H3. |
| [**fal/MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 146 | 0 | Realism-focused people LoRA for H3 from the fal team. |
| [**lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA**](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA) | lightx2v | 141 | 353 | Utility LoRA that improves H3 prompt writing. |
| [**unsloth/MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 137 | 781 | First GGUF quantization of the video model — enabling CPU inference. |
| [**meta-models/Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 239 | 0 | Official GGUF release for Muse-Glimmer-30B. |
| [**Kijai/MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 294 | 0 | Kijai's popular ComfyUI integration — "region:us" hinting at CDN distribution. |
| [**Kijai/MiniMax-H3-experimental**](https://huggingface.co/Kijai/MiniMax-H3-experimental) | Kijai | 214 | 0 | Experimental branch for bleeding-edge H3 workflows. |

---

## 3. Ecosystem Signal

- **MiniMax-H3 is the week's "viral" family**: 8 of the 30 trending models are MiniMax-H3 variants, spanning LoRAs, ComfyUI ports, GGUFs, and Turbo versions — a textbook example of how a strong base model + accessible tooling (ComfyUI) creates a self-sustaining community flywheel.
- **Frontier MoE + quantization is the new norm**: Qwen 2.4T-A95B, Nemotron 30B-A3B-NVFP4, and Kimi-K3 with compressed tensors all emphasize *activated parameter efficiency* and FP8/FP4-class quantization, indicating the industry has firmly moved past brute-force dense scaling.
- **Chinese open-weight labs are accelerating**: DeepSeek-V4, Qwen3.8, Kimi-K3 (1.5M downloads), and Ling-3.0 are all Chinese-origin, with massive adoption — the open-weight leadership balance is visibly shifting.
- **"Uncensored" and creative fine-tunes remain a significant subculture**: The DavidAU 27B model at 2.5M downloads shows there's a huge appetite (and download count) for jailbroken/entertainment-oriented Llama/Qwen variants.
- **Video generation is consolidating around one model**: While LTX-2.5 and others exist, MiniMax-H3 is clearly the dominant video-generation ecosystem, particularly in ComfyUI-driven workflows.

---

## 4. Worth Exploring

1. **Kijai/MiniMax-H3_comfy** — The 6.8M downloads via Comfy-Org, plus the fact that Kijai is the de-facto ComfyUI expert, makes this the single best starting point for anyone wanting to run or explore state-of-the-art text/image-to-video generation locally. If you want to understand why video gen is suddenly accessible, start here.

2. **Kimi-K3** — Not just the week's most-liked model (10.5K likes), but also tagged with "feature-extraction" and "compressed-tensors" (likely using compressed weight matrices like SliceGPT or SVD-based compression). This is a glimpse into the next generation of multimodal models where compression is built-in from the start.

3. **Lightricks/LTX-2.5** — A multi-purpose video diffusion model (image-to-video, text-to-video, video-to-video) that runs as a single-file diffusion. While less hyped than MiniMax-H3, it's an excellent technical counterpoint — exploring it reveals how different architectures (diffusion-transformer vs. others) approach the same video problem, and the very low download count (39) suggests you're early.

---

*Generated from Hugging Face trending data, 2026-08-13.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*