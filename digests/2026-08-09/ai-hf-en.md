# Hugging Face Trending Models Digest 2026-08-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-09 00:43 UTC

---

# Hugging Face Trending Models Digest — 2026-08-09

---

## 1. Today's Highlights

This week's trending board is dominated by **MiniMax-H3**, a next-generation video generation model that has spawned an entire ecosystem of ComfyUI ports, LoRA adapters, and quantized versions within days of release. Meanwhile, **Kimi-K3** from Moonshot AI continues its explosive momentum with 10,342 weekly likes, cementing it as one of the most anticipated open-weight multimodal releases of the year. **GLM-5.2** from Zhipu AI and **baidu/Unlimited-OCR** round out the top-tier releases, both showing strong adoption signals with millions of downloads. A notable pattern is the rapid proliferation of "Heretic/Uncensored" fine-tunes of Qwen 3.6 models, indicating sustained community appetite for unaligned variants. Finally, established open-weight anchors like **FLUX.1-dev** and **DeepSeek-V4-Flash** maintain their steady presence, showing clear ecosystem durability.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,342 | 1.39M | Flagship multimodal LLM from Moonshot AI with compressed-tensors support — the overwhelming community favorite this week. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,852 | 785K | Latest fast-thinking variant in the DeepSeek V4 line, optimized for conversational use and broad deployment. |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,902 | 2.48M | Zhipu's newest MoE flagship with DSA architecture — the biggest enterprise-grade open release this week. |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 415 | 81K | Liquid AI's efficient 2.6B model showcasing their liquid foundation model architecture. |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 255 | 896 | Early-preview MoE causal LM from DeepGrove with strong early community engagement. |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 221 | 4.2K | InclusionAI's hybrid-architecture flash model for fast conversational inference. |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 346 | 28K | Thinking Machines' compact multimodal conversational model with strong efficiency focus. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,104 | 26.7K | Novel image+text-to-video generation model — the breakout release this week, spawning dozens of community ports. |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,970 | 2.86M | Baidu's universal OCR model supporting any document/image format — massive download count tells the story. |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,037 | 502K | BFL's industry-standard text-to-image model — the baseline reference for the entire image generation ecosystem. |
| [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 314 | 457K | Microsoft's multimodal vision-language model with strong document understanding. |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 246 | 458 | NVIDIA's voice chat model combining speech understanding and generation. |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 321 | 12.8K | New ArkTTS-based preview model pushing efficient TTS quality. |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 198 | 0 | Turbo variant of MiniMax-H3 for faster video inference. |

### 🔧 Specialized Models (code, math, medical, embeddings, safety)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 544 | 17.9K | Qwen3.5-MoE-based code generation model with image-text-to-text support. |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 201 | 4.9K | Mistral's 3B safety classifier built on mistral-common — relevant amid the "uncensored" fine-tune wave. |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,006 | 3.94M | Official ComfyUI conversion of MiniMax-H3 — the most popular video generation single-file on the Hub this week. |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion...**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,761 | 2.35M | Community favorite "Heretic" uncensored Qwen 3.6 fine-tune packaged as GGUF — enormous download numbers. |
| [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 607 | 175K | Unsloth's ultra-optimized GGUF quantization of DeepSeek V4 Flash for local inference. |
| [**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored...**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 438 | 373K | MoE Qwen 3.6 fine-tune with Hermes-style training, GGUF-packaged — strong local deployment choice. |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 484 | 0 | LoRA adapter for MiniMax-H3 Turbo enabling video/audio customization. |
| [**MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 205 | 0 | Pruned ComfyUI-ready version of the MiniMax-H3 Turbo LoRA. |
| [**Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 143 | 471K | Heavily quantized Multi-format quant of MiniMax-H3 supporting INT4/INT8/NVFP4 — fast and small. |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 175 | 128K | GGUF quantizations of MiniMax-H3 built on Comfy-Org conversion. |
| [**Qwen3.6-27B-Fable-Fusion...**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) *(listed above)* | — | — | — | — |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 157 | 49.5K | Official GGUF of LiquidAI's 2.6B for llama.cpp/offline use. |
| [**Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 403 | 0 | INT8 quantized ComfyUI-packaged Qwen3-VL text encoder used in H3 pipelines. |
| [**Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4**](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 133 | 0 | NVFP4 text encoder for the MiniMax-H3 ComfyUI pipeline. |
| [**PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 170 | 0 | Community fine-tune of MiniMax-H3 with Apache-2.0 license, endpoints-compatible. |

---

## 3. Ecosystem Signal

This week signals a **decisive shift toward video generation** as the dominant frontier for open-weight AI. MiniMax-H3's release demonstrates what happens when a strong base model arrives with full ecosystem support: ComfyUI integration, LoRA adapters, and multi-format quantizations all appeared within days — a faster ecosystem velocity than we've seen for any text or image model this year.

The **"Heretic/Uncensored" trend continues to reshape the Qwen 3.6 ecosystem**, with multiple high-download variants indicating that for a meaningful segment of users, alignment trade-offs matter less than raw capability. This mirrors the Llama-2/3 era dynamics but at higher scale.

**Open-weight momentum is unambiguous** — all top-10 models are open-weight, and the dominant downloads are in GGUF/INT4 formats, reinforcing that local-first inference is now mainstream. The DeepSeek V4 Flash GGUF from Unsloth (175K downloads) and DavidAU's Qwen3.6 GGUF (2.3M) are proof points.

Notable architectural signals: **Mixture-of-Experts (MoE)** appears across GLM-5.2, maple-preview, LuffyTheFox's Qwen 3.6, and other leaders — sparse activation is becoming the default for frontier open models. LiquidAI's LFM2.5 line continues to carve a niche for efficient liquid-state designs. Finally, closed-weight pressure is rising — Moonshot's Kimi-K3, Zhipu's GLM-5.2, and Baidu's Unlimited-OCR all come from companies with proprietary lines, yet they're releasing flagship open weights. This is the clearest signal yet that the leading Chinese labs now view open-weights as the default go-to-market strategy.

---

## 4. Worth Exploring

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10,342 likes and 1.4M downloads, this is the week's most-liked release. Its use of compressed-tensors and feature-extraction alongside standard multimodal capabilities makes it an outstanding study object for how leading labs are shipping state-of-the-art open multimodal LLMs.

2. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) + [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — This is the model to study if you want to understand the modern ecosystem playbook: a strong base model + immediate first-party tooling + community quantization wave. The Comfy-Org conversion alone has 3.9M downloads, making it the most-downloaded single file this week. Worth studying for its diffusion architecture and for how the community quickly embraced it across inference backends.

3. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — An unheralded star (3,970 likes, 2.86M downloads). Unlimited-OCR is a universal document understanding model that handles everything from scanned docs to complex tables — a class of model that's often overlooked in favor of chatbots but has enormous practical deployment value in enterprise and document-heavy workflows.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*