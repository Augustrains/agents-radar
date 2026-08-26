# Hugging Face Trending Models Digest 2026-08-26

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-26 00:32 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-26

---

## 1. Today's Highlights

This week's Hugging Face landscape is dominated by **Qwen3.8-27B**, whose ecosystem has exploded into over a dozen variants—from abliterated "uncensored" versions to GGUF quantizations, MLX ports, and speculative-decoding fine-tunes. The **Kimi-K3** release from Moonshot AI stands out as the second-highest-liked model, signaling strong momentum for compressed open-weight architectures. **DeepSeek's V4 family** continues to expand with both Flash and Pro variants, while **MiniMax** pushes creative frontiers with video (MiniMax-H3) and music (MiniMax-Music3) generation. Notably, **Ornith-1.5-35B-A3B**, a Mixture-of-Experts model built on qwen3_5_moe architecture, shows that MoE approaches are gaining serious community traction with over 1.2M downloads for its GGUF variant alone. The sheer volume of uncensored/abliterated Qwen3.8 variants (at least 8 distinct releases) confirms that the community's appetite for "jailbroken" models remains insatiable.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,707 | 2,945,415 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,714 | 3,528,373 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,996 | 2,865,293 |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 419 | 70,158 |
| [ornith-ai/Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 216 | 98,323 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 758 | 74,707 |

The **Qwen3.8-27B** flagship is the undisputed leader with over 12.7K likes, establishing itself as the reference multimodal conversational model. **DeepSeek-V4-Flash** demonstrates the fast-inference, distilled-tier strategy. **Kimi-K3**, built with compressed-tensors technology, shows Moonshot AI's commitment to efficient deployment. The **Ornith-1.5** family (both 35B-A3B MoE and 9B dense) demonstrates rising interest in parameter-efficient architectures built on qwen3_5_moe.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,798 | 833,845 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,457 | 4,639,786 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,245 | 18,705 |
| [Audio8/Audio8-TTS-Preview-0.1b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b) | Audio8 | 156 | 3,640 |
| [sensenova/SenseNova-U1.5-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1.5-8B-MoT) | sensenova | 152 | 2,682 |

**MiniMax-H3** leads the video generation pack with 4.6M downloads, offering image-to-video and text-to-video capabilities. **Lightricks LTX-2.5** is a versatile single-file diffusion model spanning multiple video tasks. **MiniMax-Music3** brings music generation via diffusers pipeline, while **Audio8-TTS** experiments with the ArkTTS architecture. **SenseNova-U1.5-8B-MoT** explores native any-to-any multimodal understanding with a compact 8B parameter footprint.

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 238 | 3,474 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,468 | 0 |
| [peculiar-ragdoll/Qwen-Sharp-Chat-Templates](https://huggingface.co/peculiar-ragdoll/Qwen-Sharp-Chat-Templates) | peculiar-ragdoll | 244 | 0 |

**s1-mini** combines text generation with automatic speech recognition in a compact Qwen3-based package. The **chat template** repos from froggeric and peculiar-ragdoll address the critical but often underappreciated issue of correct Jinja chat templates for Qwen 3.5, gaining significant likes (1,468 and 244 respectively) despite zero downloads, likely serving as reference utilities for developers.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,915 | 7,334,695 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 1,094 | 68,855 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 748 | 389,747 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,148 | 249,744 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 622 | 832,185 |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 297 | 1,156,903 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 721 | 1,525,645 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 357 | 1,230,831 |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 227 | 64,984 |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 240 | 221,918 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 452 | 154,225 |
| [incoai/Qwen3.8-27B-DFlash2](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2) | incoai | 179 | 105,786 |
| [orcarouter/Qwen3.8-27B-Uncensored](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored) | orcarouter | 183 | 15,341 |
| [EschaLabs/Qwen3.8-27B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.8-27B-Escha-W2) | EschaLabs | 126 | 2,319 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 275 | 735,183 |
| [ornith-ai/Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 201 | 1,144,037 |

This category is dominated by **Qwen3.8-27B derivations**. Unsloth's GGUF release leads in raw downloads (7.3M), serving as the de facto entry point for local deployment. The **uncensored/abliterated** ecosystem includes orcarouter's MLX, FP8, GGUF, and base variants; OBLITERATUS's multi-format release; HauhauCS's aggressive MTP variant; huihui-ai's abliterated GGUF; and 0bserverx's "Heretic" version. **DFlash2** (z-lab and incoai) introduces speculative decoding fine-tunes. DavidAU's "Cold-Fusion-GAIN" experimental merge, EschaLabs' 2-bit extreme quantization, and Ornith's MIT-licensed GGUF variants round out a remarkably deep ecosystem.

---

## 3. Ecosystem Signal

The Qwen3.8-27B family is the clear ecosystem center of gravity, generating a Grecian fleet of community variants. This mirrors Qwen's strategic release approach—open-weight plus permissive licensing—which consistently catalyzes third-party innovation. Unsloth's dominance (7.3M downloads) as the quantization gateway confirms that **local deployment is the primary consumer use case**, outpacing even the official release.

**Abliteration/censorship-removal remains a persistent community obsession**, with at least 8 separate uncensored Qwen3.8-27B variants trending. Beyond Qwen, **DeepSeek's V4 tiered strategy** (Flash vs Pro) and **Moonshot's compressed K3** indicate a race toward compute-efficient serving. The **Ornith Moe models** (35B-A3B) suggest growing appetite for sparse expert models on modest hardware.

**Quality-of-life infrastructure** is quietly thriving—the chat template repos and chat-template fixes showing thousands of likes signal that developers increasingly value tooling over raw model weights. Chinese labs (Qwen, DeepSeek, MiniMax, Moonshot, SenseNova) are collectively outpacing Western counterparts in both release cadence and community mindshare this week.

---

## 4. Worth Exploring

1. **Kimi-K3 (Moonshot AI)** — This is the dark horse of the week: 10,996 likes with only a fraction of Qwen's ecosystem buzz. Its **compressed-tensors** approach may represent the future of efficient deployment. Studying its architecture and inference patterns could reveal how 2-4x size compression without quality loss is achieved—a critical capability as models scale.

2. **Qwen3.8-27B-DFlash2 (z-lab)** — Speculative decoding fine-tunes are rarely this popular. The DFlash2 approach could dramatically reduce inference latency for multimodal tasks. Comparing z-lab and incoai's implementations offers insight into whether optimized draft-model training is becoming practical for mainstream adoption.

3. **Ornith-1.5-35B-A3B (ornith-ai)** — An MIT-licensed MoE on qwen3_5_moe with image-text-to-text support, packaged with endpoints_compatible GGUF variants (1.2M downloads). This is a rare combination of license permissiveness, architectural efficiency, and multimodal capability — a template for enterprise-safe open models. Its 35B total parameters with 3B active sets a new data point for the capability-per-active-parameter frontier.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*