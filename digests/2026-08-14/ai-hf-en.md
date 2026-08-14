# Hugging Face Trending Models Digest 2026-08-14

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-14 00:54 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-14

---

## 1. Today's Highlights

This week's trending list is dominated by **MiniMax-H3**, a powerful video generation model that has spawned an entire ecosystem of fine-tunes, LoRAs, ComfyUI integrations, and GGUF quantizations—with the flagship release amassing **3,822 likes** and over **1.6M downloads**. Meanwhile, **moonshotai/Kimi-K3** leads the multimodal language model charge with an impressive **10,621 likes**, signaling strong community interest in compressed/feature-extraction capable architectures. On the LLM front, **DeepSeek-V4-Flash-0731** continues to build momentum with **3,319 likes**, and Qwen's massive **2.4T-parameter MoE** model (Qwen3.8) shows the industry's appetite for frontier-scale open weights. Notably, **Meta's Muse-Glimmer-30B** is gaining traction as a new image-text-to-text conversational model, appearing in both original and GGUF formats. The overall picture shows video generation, multimodal understanding, and ultra-large MoE architectures as the three hottest battlegrounds.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 783 / 1,012 | A massive 2.4T-parameter Mixture-of-Experts model (95B active) pushing the frontier of open-weight LLMs. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,319 / 1,431,587 | The latest DeepSeek flagship, offering fast, efficient inference with conversational power that rivals much larger models. |
| [**DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 285 / 0 | The Pro variant of DeepSeek V4, freshly released and awaiting community adoption. |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 602 / 116,640 | A compact 2.6B model from Liquid AI demonstrating strong performance-to-size ratio using liquid architectures. |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 229 / 44,859 | NVIDIA's efficient 30B (3B active) model in NVFP4 quantized format, targeting deployment on enterprise hardware. |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 130 / 22,279 | The BF16 sibling of NVIDIA's Lightning model, providing full-precision weights for research and fine-tuning. |
| [**inclusionAI/Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 323 / 10,052 | A conversational hybrid-architecture model featuring custom bailing_hybrid code, gaining attention for its efficient design. |
| [**deepgrove/maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 353 / 3,868 | A new Mixture-of-Experts text-generation model generating curiosity as a preview release from an emerging lab. |
| [**Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 157 / 4,000 | FP8 quantized version of Qwen's 2.4T MoE, making the massive model more accessible for inference. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,822 / 1,605,940 | The hottest video generation model this week, supporting both text-to-video and image-to-video with exceptional quality. |
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,621 / 1,871,575 | Most-liked model this week—a multimodal image-text-to-text model with compressed-tensor support for efficient feature extraction. |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,417 / 121,042 | Meta's new conversational image-text-to-text model, bridging vision-language understanding with chat capabilities. |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 718 / 57,287 | The latest version of Lightricks' video generation suite, now supporting image-to-video, video-to-video, and more. |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 304 / 25 | MiniMax's third-generation music generation model, adding a new creative domain to their ecosystem. |
| [**endless-frontier/BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 188 / 3,184 | An emerging image-text-to-text conversational model based on Qwen3.5 MoE architecture. |
| [**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 371 / 1,164 | NVIDIA's voice chat model, enabling conversational audio interactions with reference to multiple recent papers. |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 461 / 91,455 | A community-optimized turbo variant of MiniMax-H3 for faster video generation, featuring t2v, i2v, and r2v support. |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**inclusionAI/Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 216 / 1,292 | The tiny variant of Ling 3.0, MIT-licensed with custom hybrid architecture, drawing interest for edge deployments. |

*Note: No dedicated code, math, or embedding models surfaced in the top-30 this week—suggesting the community's focus is currently on general conversational and generative models.*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 390 / 352,023 | Unsloth's GGUF quantization of Muse-Glimmer, enabling local deployment of Meta's new multimodal model. |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,987 / 2,793,115 | Extremely high download count for this community fine-tune merging Qwen3.6 with uncensored/heretic tuning for creative writing. |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,289 / 10,365,210 | Over 10M downloads—the ComfyUI integration of MiniMax-H3 is the de-facto standard for video generation workflows. |
| [**larryvrh/MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 726 / 0 | A LoRA adapter for MiniMax-H3 Turbo, allowing fine-grained control of video generation styles. |
| [**Kijai/MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 304 / 0 | Kijai's ComfyUI nodes and workflows for MiniMax-H3, a go-to resource for the ComfyUI community. |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 314 / 0 | ComfyUI-ready LoRA for MiniMax-H3 Turbo, streamlining the integration of custom LoRAs into video workflows. |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 297 / 324 | A community fine-tune of MiniMax-H3 for stylized video generation, Apache-2.0 licensed with endpoint compatibility. |
| [**fal/MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 159 / 4,692 | fal's LoRA for realistic human rendering in MiniMax-H3, addressing a common weak point in video generation. |
| [**lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA**](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA) | lightx2v | 149 / 652 | A specialized LoRA that rewrites prompts for better MiniMax-H3 output, an essential companion tool. |
| [**unsloth/MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 149 / 111,222 | GGUF quantization of MiniMax-H3 for local stable-diffusion.cpp video generation workflows. |
| [**meta-models/Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 257 / 136,783 | Official GGUF release of Muse-Glimmer, making it easier to run this powerful multimodal model locally. |
| [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 483 / 0 | A niche community fine-tune combining Qwen3-VL with H3 architecture and ComfyUI compatibility, INT8 quantized with custom rotation features. |

---

## 3. Ecosystem Signal

The current momentum is unmistakably around **video generation**, with **MiniMax-H3** serving as the epicenter. The model family has spawned a rich ecosystem including Turbo variants, multiple LoRA adapters (realism, prompt-rewriting, stylized), ComfyUI integrations, and GGUF quantizations—demonstrating a healthy, rapidly-consolidating community around a single architecture. This mirrors the SDXL pattern of 2024, and the **10M+ downloads** of the ComfyUI integration indicate video generation has gone mainstream in the open-source community.

**Multimodal understanding** continues its rise with **Kimi-K3** (10.6K likes) and **Muse-Glimmer-30B** both pushing image-plus-text conversational capabilities. The trend toward **Feature-extraction and compressed tensors** in Kimi-K3 suggests efficient multimodal retrieval is becoming a priority.

On the LLM front, **ultra-large MoE architectures** are the dominant trend: Qwen's 2.4T, DeepSeek's V4 line, and NVIDIA's efficient A3B models all reflect a shift toward sparse expert models that deliver frontier capability with reasonable inference cost. The heavy activity around **GGUF quantizations** (especially from unsloth) signals sustained demand for local, consumer-grade deployment of these increasingly large models. Notably, the "uncensored/heretic" fine-tune niche continues to show surprising popularity (1,987 likes for DavidAU's Qwen3.6 merge), indicating a persistent sub-community prioritizing creative freedom over safety alignment.

---

## 4. Worth Exploring

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10,621 likes (the highest on this list by far), Kimi-K3 represents the strongest signal of what the community values: multimodal understanding with compressed-tensor efficiency. Its feature-extraction tag suggests it may excel at tasks beyond chat, making it worth studying for RAG and multimodal embedding applications.

2. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — Over **10.3 million downloads** makes this the most-downloaded integration on the list. For any practitioner interested in state-of-the-art video generation, understanding this ComfyUI workflow is essential—it's the closest thing to a standard API for open-source video synthesis.

3. **[unsloth/Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF)** — Meta's new Muse-Glimmer architecture is early-stage but already has 352K downloads in GGUF form. Watching how multimodal conversational models like this evolve—and how efficiently they can be quantized without quality loss—will be critical for the next generation of local AI assistants. Unsloth's quantization provides an accessible entry point to study this model on consumer hardware.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*