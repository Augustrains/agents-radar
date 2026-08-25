# Hugging Face Trending Models Digest 2026-08-25

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-25 00:30 UTC

---

# 🤗 Hugging Face Trending Models Digest
**Date: 2026-08-25 | 30 tracked models**

---

## 1. Today's Highlights

The Hugging Face ecosystem is **dominated by Qwen3.8-27B** variants, with the base model accumulating 12,512 likes and the broader Qwen family (including GGUF, FP8, and abliterated versions) occupying 16 of the top 30 spots. **Lightricks' LTX-2.5** and **MiniMax's H3** and **Music3** signal strong momentum in video and music generation, with MiniMax-H3 reaching 4.4M downloads. The community shows a notable appetite for **uncensored/abliterated fine-tunes** (at least 8 variants in the top 30), alongside a surge in **speculative decoding** (DFlash2) and **MoE architecture** releases from ornith-ai. New entrants like **DeepSeek-V4-Flash** and **Audio8-TTS** round out a diverse landscape spanning text, vision, audio, and video.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,512 | 2,645,226 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,681 | 3,274,129 |
| [Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 396 | 60,294 |
| [Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 202 | 83,192 |
| [s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 229 | 2,976 |

**Qwen3.8-27B** is the flagship multimodal LLM of the week—a 27B parameter image-text-to-text model from Qwen that has become the central hub for a massive ecosystem of fine-tunes, quantizations, and community adaptations. **DeepSeek-V4-Flash** is DeepSeek's latest conversational text-generation model, quickly climbing the ranks with strong adoption. **Ornith-1.5-35B-A3B** is a 35B-parameter MoE model with 3B active parameters, representing a growing trend toward efficient sparse architectures.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,417 | 4,465,161 |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,723 | 790,378 |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,228 | 18,065 |
| [Audio8-TTS-Preview-0.1b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b) | Audio8 | 145 | 2,775 |
| [Minimax_h3_latent_Upscaler](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) | LBH-123-AI | 181 | 0 |

**MiniMax-H3** is a next-generation image-text-to-video diffusion model with massive adoption (4.4M downloads), establishing MiniMax as a leading player in video generation. **LTX-2.5** from Lightricks is a versatile image-to-video / text-to-video model supporting multiple video generation tasks. **MiniMax-Music3** brings high-quality music generation to the Diffusers ecosystem. **Audio8-TTS** is a compact TTS preview with 0.1B parameters, showing momentum in efficient speech synthesis.

---

### 🔧 Specialized Models (code, math, medical, embeddings — includes non-quantized variants)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 214 | 50,763 |
| [Qwen3.8-27B-DFlash2](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2) | incoai | 173 | 85,034 |
| [Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,447 | 0 |
| [Qwen-Sharp-Chat-Templates](https://huggingface.co/peculiar-ragdoll/Qwen-Sharp-Chat-Templates) | peculiar-ragdoll | 228 | 0 |

**Qwen3.8-27B-DFlash2** (from both z-lab and incoai) implements speculative decoding with a draft model to accelerate inference—a growing area of focus for deployment efficiency. **Qwen-Fixed-Chat-Templates** (1,447 likes with 0 downloads) and **Qwen-Sharp-Chat-Templates** are chat template fixes for MLX usage, showing community demand for improved prompt formatting across frameworks.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, MLX)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,835 | 7,009,063 |
| [Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 1,026 | 57,947 |
| [Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,097 | 224,114 |
| [Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 695 | 312,627 |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 689 | 1,456,700 |
| [Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 578 | 761,975 |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 423 | 143,108 |
| [Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 334 | 1,140,375 |
| [Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 226 | 209,017 |
| [Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 274 | 988,170 |
| [Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 186 | 971,104 |
| [Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 277 | 27,316 |
| [Qwen3.8-27B-Uncensored](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored) | orcarouter | 170 | 10,482 |
| [Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 260 | 162,580 |
| [Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 259 | 654,805 |
| [Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 681 | 3,004,940 |

The quantization and fine-tune ecosystem around Qwen3.8-27B is **massive**. **unsloth's GGUF** release leads all quantized models with 7M downloads, while **Qwen's official FP8** reaches 3M downloads. The **abliteration/uncensored** trend is unmistakable—multiple organizations (orcarouter, huihui-ai, OBLITERATUS, 0bserverx) are releasing versions with safety guardrails removed, with the largest reaching over 1.4M downloads. **Ornith GGUF** variants also show strong adoption.

---

## 3. Ecosystem Signal

**Qwen 3.8 is the dominant ecosystem.** The Qwen3.8-27B model family accounts for 16 of the 30 top-trending models and roughly 19M of ~26M total downloads tracked. This suggests Qwen has consolidated its position as the go-to open-weight model family, particularly for multimodal (image-text-to-text) tasks. The official model plus community fine-tunes (abliterated, uncensored) and quantizations (GGUF, FP8, MLX) form a full distribution stack.

**Open-weight models clearly lead.** All top 30 are open-weight, with no proprietary API models in the trending list. MiniMax (H3, Music3), Lightricks (LTX-2.5), and DeepSeek (V4-Flash) are establishing themselves as credible open alternatives in video, music, and chat respectively.

**Quantization is the primary distribution channel.** GGUF dominates with over 14M cumulative downloads across variants, outpacing FP8 and MLX. Abliteration/uncensored fine-tuning has become a distinct micro-trend with at least 8 variants, indicating developer interest in exploring model capabilities beyond safety guardrails.

**Emerging signals:** speculative decoding (DFlash2), MoE efficiency (Ornith-1.5), and chat-template fixes for MLX suggest growing focus on inference efficiency and developer experience beyond raw model capabilities.

---

## 4. Worth Exploring

1. **[Unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — With 7M downloads, this is the single most-used quantization of the week. Unsloth's implementation is widely trusted for quality and performance, making it the reference point for local deployment of Qwen3.8-27B.

2. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — The 4.4M downloads in such a short window signal that this image-text-to-video model is resonating deeply. It's worth studying as the emerging standard for open video generation.

3. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — The base model itself deserves attention as the center of gravity for the current ecosystem. Understanding its multimodal architecture and prompt handling is key to making sense of the entire fine-tune and quantization ecosystem built on top of it.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*