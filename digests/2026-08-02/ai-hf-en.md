# Hugging Face Trending Models Digest 2026-08-02

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-02 01:25 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-02

---

## 1. Today's Highlights

This week's HF trending chart is dominated by **Moonshot AI's Kimi-K3**, a multimodal compressed-transformer model that has surged to **9,487 likes** with 559K+ downloads, signaling strong community excitement around efficient MoE architectures. **DeepSeek-V4-Flash** (2.8M downloads) and **Zhipu AI's GLM-5.2** (1.68M downloads) continue to anchor the open-weight LLM conversation, while a wave of **Qwen3.6 community fine-tunes** (uncensored, vision-capable variants) shows massive adoption for personal and edge deployments. On the ecosystem side, **quantization is the story** — GGUF conversions from unsloth, NVFP4 quantizations from nota-ai, and 2-bit ternary models from prism-ml all point to a maturing local-inference ecosystem. Baidu's **Unlimited-OCR** (2.45M downloads) represents the strongest non-LLM entry, demonstrating sustained interest in specialized document-understanding models.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 1,428 | 15,366 | Latest iteration of DeepSeek's high-efficiency Flash family, building on V4's massive adoption. |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,947 | 2,814,414 | The flagship open-weight conversational model; the 2.8M downloads speak for themselves. |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,737 | 1,683,442 | Zhipu's MoE (glm_moe_dsa) conversational model — a top-3 most-liked model this week. |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 611 | 27,892 | Compact 3B LLM offering strong performance-per-parameter for edge deployment. |
| [**Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 868 | 77,021 | Poolside's code-leaning LLM update, gaining traction in developer workflows. |
| [**Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 717 | 13,426 | Upstage's massive 250B open-weight model — one of the largest fully open releases this week. |

### 🎨 Multimodal & Generation (Vision, Speech, Text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,487 | 559,924 | **The breakout model of the week** — Moonshot's multimodal compressed-transformer with 9.4K likes. |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,714 | 2,457,387 | Baidu's all-in-one OCR model with massive download volume — the #1 downloaded model this week. |
| [**Inkling**](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,672 | 59,076 | Multimodal conversational model (inkling_mm_model) from thinkingmachines, strong community buzz. |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 172 | 10,525 | Microsoft's vision-language model — researching multimodal alignment at scale. |
| [**Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 242 | 2,775 | Microsoft's computer-use oriented multimodal model built on Qwen3.5. |
| [**VibeVoice-ASR-BitNet**](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 141 | 5,835 | BitNet-based ASR model — quantized speech recognition at the edge. |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 361 | 1,565 | Lightweight local TTS (CPU/edge-optimized) — riding the on-device speech wave. |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 166 | 3,254 | New 0.6B parameter TTS model (arktts) — efficient speech synthesis from audio-first startup. |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 95 | 0 | Krea2 LoRA for text-to-image in ComfyUI — early-stage but trending in creative circles. |

### 🔧 Specialized Models (Code, Embeddings, Domain-Specific)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 391 | 10,771 | Specialized code-generation MoE (Qwen3.5-based) with multimodal support. |
| [**XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 330 | 923 | Agentic-search oriented model — a niche but fast-growing space worth watching. |
| [**LFM2.5-Encoder-350M**](https://huggingface.co/LiquidAI/LFM2.5-Encoder-350M) | LiquidAI | 87 | 6,190 | Liquid AI's 350M encoder for fill-mask tasks — small, efficient, specialized. |

### 📦 Fine-tunes & Quantizations (GGUF, Community Fine-tunes)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,225 | 1,823,436 | The top community fine-tune — uncensored, vision-capable MoE with 1.8M downloads. |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,236 | 1,173,001 | DavidAU's GGUF mega-build — uncensored + MTP optimization for local GPU inference. |
| [**Ternary-Bonsai-27B-gguf**](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,134 | 716,341 | **Ternary (2-bit) quantization pioneer** — 27B model running on consumer hardware. |
| [**Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 186 | 267,572 | Smaller DavidAU build (9B) with NEO-Imatrix quantization for tight memory budgets. |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 287 | 228,610 | Hermes-V6 instruct-tuned GGUF — high-quality conversational fine-tune with huge adoption. |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 288 | 4,048 | Official unsloth GGUF conversion of DeepSeek's latest — the standard for local LLM deployment. |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 243 | 41,337 | Community GGUF of Kimi-K3 — enabling **compressed multimodal** on local hardware. |
| [**Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 151 | 22,396 | NVFP4 quantization of Solar-Open2 — 250B at (almost) consumer-feasible precision. |
| [**Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 112 | 875 | Experimental 2-bit weight quantization of Qwen3.6 MoE — pushing the limits of compression. |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 213 | 3,998 | Smaller variant of Inkling for edge/mobile multimodal deployment. |
| [**XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 357 | 650 | Mini variant of the Aquila line — compact but trending in agentic-search research. |

---

## 3. Ecosystem Signal

**Moonshot AI is the momentum leader.** Kimi-K3's 9,487 likes — nearly 5× the next most-liked model — signals that **compressed multimodal transformers** are the next major frontier. The combination of "feature-extraction" + "compressed-tensors" tags suggests K3 is designed for both local inference and embedding-style tasks, potentially disrupting the search/RAG stack.

**The open-weight paradigm is consolidating.** DeepSeek V4, GLM-5.2, and Qwen3.6 families now underpin the entire fine-tuning economy. Community fine-tunes (uncensored variants from HauhauCS, DavidAU, LuffyTheFox) are each pulling 200K–1.8M downloads, demonstrating that **local-first, unconstrained AI is a dominant use case** — not a niche.

**Quantization is the real story.** We're seeing a clear progression: GGUF → imatrix → 2-bit ternary (prism-ml) → W2 (EschaLabs). The fact that **Ternary-Bonsai-27B** has 716K downloads tells us that **users are willing to accept quality trade-offs for consumer-hardware feasibility**. Expect 2-bit to become the default for >30B models on edge devices by year-end.

**TTS is quietly heating up.** Inflect-Micro-v2 (CPU-optimized) and Audio8 (0.6B) represent a wave of small, efficient, local-first speech models — likely targeting the agentic-device market.

---

## 4. Worth Exploring

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** (moonshotai, 9,487 likes) — This is *the* model to study this week. Between its 559K+ downloads, compressed-transformer architecture, and multi-modal capability, K3 appears to redefine what's possible in the mid-size category (~20B effective, likely). The "feature-extraction" tag suggests it doubles as an embedding model — a dual-purpose design that could reshape how teams build RAG infrastructure.

2. **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** (prism-ml, 1,134 likes, 716K downloads) — Ternary quantization is arguably the most important algorithmic advance in local inference since GGUF itself. The 716K download count on such an experimental format is a strong signal that **the local-hardware market is ready for aggressive compression**. If you're running LLMs on consumer GPUs or laptops, this is the frontier.

3. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 4,737 likes, 1.68M downloads) — While Kimi's MoE attention-grabbing, GLM's **glm_moe_dsa** architecture quietly powers one of the most-loved conversational models in the open ecosystem. With 1.68M downloads, it's a strong candidate for enterprise tinkerers seeking a conversational model that balances quality with MoE efficiency — and surprisingly, it hasn't received the community-fine-tune flood Qwen gets. That's an **opportunity gap** worth noticing.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*