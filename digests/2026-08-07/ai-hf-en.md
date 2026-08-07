# Hugging Face Trending Models Digest 2026-08-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-07 01:58 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-07

---

## 1. Today's Highlights

This week's Hugging Face landscape is dominated by **three major narratives**: the explosive growth of the **MiniMax-H3** video generation ecosystem (with official and community variants racking up ~5.2M combined downloads), the rapid iteration of **DeepSeek-V4** and **GLM-5.2** flagship LLMs, and an unusual surge of **"uncensored"/"heretic" community fine-tunes** built on Qwen and MiniMax architectures. The **Kimi-K3** model from Moonshot AI is the clear breakout star of the week, accumulating **10,200 likes and 1.25M downloads** — the highest engagement of any model on this list. Also notable is **Baidu's Unlimited-OCR** (2.79M downloads) signaling strong demand for document intelligence, and the persistent relevance of the **FLUX.1-dev** image generation model, which remains the most-liked model overall despite being a year old. The ecosystem shows a clear split between **official frontier releases** and a **vibrant community layer** of quantizations, LoRAs, and ComfyUI integrations.

---

## 2. Trending Models by Category

### 🧠 Language Models

| Model | Author | ❤️ | ⬇️ | Why it's trending |
|-------|--------|----|----|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,200 | 1.26M | Flagship MoE model with compressed-tensors support; the most-liked release this week — major multimodal conversational AI upgrade. |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,042 | 2.64M | High-performance Flash-tier LLM; significant adoption due to speed and efficiency in production deployments. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,647 | 618K | Date-stamped iteration adding conversational refinements; trending due to rapid release cadence. |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,871 | 2.39M | Next-gen GLM with MoE-DSA architecture; massive downloads, strong community trust. |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 332 | 74K | Compact 2.6B liquid model — proving that small, efficient models remain in demand for edge deployment. |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,647 | 618K | Date-stamped iteration adding conversational refinements; trending due to rapid release cadence. |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 186 | 1.2K | New hybrid-architecture flash model with custom code; early-stage buzz. |

### 🎨 Multimodal & Generation

| Model | Author | ❤️ | ⬇️ | Why it's trending |
|-------|--------|----|----|-------------------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,754 | 12K | Flagship image-text-to-video model — core of a vastecosystem trend this week. |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,010 | 523K | The enduring text-to-image champion; still the most-liked model on the platform. |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,929 | 2.79M | Enterprise-grade OCR with feature extraction; massive adoption across document workflows. |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 286 | 440K | Microsoft's vision-language model — leverages transformers with strong multimodal performance. |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 205 | 0 | New Krea2-based text-to-image LoRA; ComfyUI compatible, early hype. |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 322 | 22K | Efficient image-text-to-text multimodal model with conversational capabilities. |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 293 | 12K | ArkTTS-based speech synthesis preview; rising interest in TTS. |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 177 | 206 | Voice chat model; referencing multiple arXiv papers, positioned for voice AI applications. |

### 🔧 Specialized Models

| Model | Author | ❤️ | ⬇️ | Why it's trending |
|-------|--------|----|----|-------------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 519 | 17K | Code-specialized model built on Qwen3.5-MoE — developer community traction. |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 158 | 1.5K | Safety/safeguard classifier — significant for AI alignment and guardrails. |
| [**Maple-Preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 207 | 419 | MoE causal LM preview; niche research interest for mixture-of-experts. |
| [**XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 424 | 1.6K | New mini model built on Qwen3.5-MoE architecture — well-received. |

### 📦 Fine-tunes & Quantizations

| Model | Author | ❤️ | ⬇️ | Why it's trending |
|-------|--------|----|----|-------------------|
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 848 | 2.3M | ComfyUI single-file distribution; the practical gateway for the MiniMax ecosystem. |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 153 | 66K | Community GGUF quantization for local inference. |
| [**Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 109 | 273K | Mixed-precision quantization enabling low-memory video gen. |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 545 | 145K | Unsloth's efficient GGUF — standard choice for local LLM deployment. |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 125 | 12.8K | Official GGUF for llama.cpp compatibility. |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-**…](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,652 | 2.09M | "Uncensored" Qwen fine-tune; viral community phenomenon this week. |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 407 | 309K | Another high-download uncensored MoE variant. |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 301 | 0 | Turbo-charged LoRA adaptation for MiniMax-H3 (audio-video). |
| [**MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 118 | 0 | ComfyUI-packaged pruned MiniMax LoRA. |
| [**Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4**](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 108 | 0 | Hybrid text-encoder combining Qwen3-VL with MiniMax-H3 in NVFP4. |
| [**Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 337 | 0 | Qwen3-VL + H3 fusion; INT8 CONV-ROT quantization for ComfyUI. |
| [**Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 222 | 3.4K | Community MoE fine-tune, exploring W2 quantization. |

---

## 3. Ecosystem Signal

**The "Uncensored" Community Layer Is Exploding.** Models with "uncensored," "heretic," or "ultra" in their names — notably the Qwen3.6-27B DavidAU release and LuffyTheFox's Qwen3.6-35B — are racking up **millions of downloads** in days. This signals a strong segment of hobbyist/consumer users who want unrestricted creative or roleplay capabilities, pushing the ecosystem toward permissively-tuned variants of otherwise gated models.

**MiniMax-H3 Is This Week's Hottest Video Family.** The official release (12K downloads) is dwarfed by its derivative ecosystem: Comfy-Org's single-file distribution (2.3M), community GGUF/INT4 quantizations (273K+), and multiple LoRA/ComfyUI integrations total **~5.2M downloads in one week**. This is a textbook example of an open-weight model catalyzing a downstream tooling ecosystem faster than its own adoption.

**Open-Weight Dominance, Structural Shift.** All top-10 models by likes/downloads in this list are open-weight. Kimi-K3 and GLM-5.2 demonstrate that Chinese labs are now setting the pace. Meanwhile, quantized versions (GGUF via Unsloth, NVFP4, INT8) are not secondary artifacts — they are the *primary deployment vehicles* for most users.

**Hybrid/"Fusion" Architectures Emerging.** Multiple new models (KAT-Coder, Escha-W2, XYZ-Aquila-mini) leverage **Qwen3.5-MoE / Qwen3.6** as base — suggesting the open LLM community has consolidated around the Qwen family for derivative work, while frontier labs (DeepSeek, GLM, Kimi) compete at the top.

---

## 4. Worth Exploring

1. **Kimi-K3** (https://huggingface.co/moonshotai/Kimi-K3) — The most-liked model of the week with 10.2K likes and 1.25M downloads. Features compressed-tensor support (newer approach to efficient inference) and a hybrid sparse attention architecture likely to influence future model design. Studying its compression techniques and multimodal fusion is high-value for anyone working in efficient LLMs.

2. **MiniMax-H3** (https://huggingface.co/MiniMaxAI/MiniMax-H3) — The launchpad for the fastest-growing video generation ecosystem this week. Its image-text-to-video pipeline and the sheer breadth of community quantizations (GGUF, INT4/INT8, NVFP4) make it a case study in open-weight ecosystem dynamics. Also worth pairing with the **Comfy-Org single-file** release for practical experimentation.

3. **Unlimited-OCR** (https://huggingface.co/baidu/Unlimited-OCR) — 3.9K likes and 2.79M downloads with near-zero marketing. This model appears to be delivering exceptional OCR performance — a critical infrastructure layer for document processing, RAG pipelines, and enterprise automation. Worth comparing against OpenAI's GPT-4o OCR capabilities for a cost/performance assessment in production workflows.

---

*Digest prepared for AI/ML ecosystem monitoring — all data from Hugging Face Hub, 2026-08-07.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*