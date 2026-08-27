# Hugging Face Trending Models Digest 2026-08-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-27 05:22 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-27

---

## 1. Today's Highlights

This week's trending list is dominated by **Qwen3.8-27B**, a new multimodal flagship from Alibaba's Qwen team, which has spawned an extensive ecosystem of GGUF quantizations, abliterated "uncensored" variants, and aggressive fine-tunes—collectively accounting for over 14 model entries on the list. **MiniMax-H3** (video generation) and **MiniMax-Music3** (text-to-music) show that MiniMax is aggressively expanding beyond language into generative media, while **DeepSeek-V4-Flash-0731** continues to hold strong as a top-tier open-weight LLM with 3.8M downloads. The rise of **Ornith-1.5** models (MIT-licensed, MoE-based) signals growing community interest in efficient, permissively-licensed architectures. Notably, **Kimi-K3** from Moonshot AI has surged to 11K likes, indicating strong appetite for compressed/open-weight alternatives to proprietary models.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,743 | 3,857,140 |
| [GLM-5.3-Flash](https://huggingface.co/zai-org/GLM-5.3-Flash) | zai-org | 1,002 | 0 |
| [Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 456 | 83,342 |
| [Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 229 | 119,053 |
| [SenseNova-U1.5-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1.5-8B-MoT) | sensenova | 174 | 3,264 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 252 | 3,921 |

**DeepSeek-V4-Flash-0731** is DeepSeek's latest open-weight conversational LLM, trending for its competitive performance at a Flash-tier inference speed. **GLM-5.3-Flash** is Zhipu AI's newest generation model (tagged `glm5_next`), just released with zero downloads yet—watch for early adopters. **Ornith-1.5-35B-A3B** and **Ornith-1.5-9B** are MIT-licensed MoE and dense models respectively from ornith-ai, gaining traction for their permissive licensing and strong performance-to-parameter ratios. **SenseNova-U1.5-8B-MoT** is SenseTime's native multimodal any-to-any model based on a "MoT" (Mixture-of-Thought?) architecture.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,929 | 3,298,569 |
| [Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) | Qwen | 3,723 | 2,551 |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,505 | 4,793,098 |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,265 | 19,501 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,876 | 894,094 |
| [MiniMax-H3-Fun-Controlnet-Union](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union) | alibaba-pai | 141 | 3,148 |
| [Audio8-TTS-Preview-0.1b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b) | Audio8 | 176 | 4,257 |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 11,023 | 2,921,257 |

**Qwen3.8-27B** is the week's undisputed star—a 27B multimodal model (image-text-to-text) with 13K likes and 3.3M downloads. **Qwen3.8-Flash-Next** is a lighter/faster variant tagged as a `qwen4_exp` experimental release. **MiniMax-H3** is MinMax's flagship video generation model (text-to-video, image-to-video) with massive adoption (4.8M downloads). **MiniMax-Music3** extends their generative portfolio to music. **Lightricks/LTX-2.5** is a diffusion-based video model supporting text/image/video-to-video. **Kimi-K3** from Moonshot AI is a multimodal (image-text-to-text) model with compressed-tensors, trending with 11K likes—notably uses compressed tensors for efficiency.

### 🔧 Specialized Models (Code, Math, Medical, Embeddings)

*No dedicated specialized models (code/math/medical/embeddings) appeared in this week's top-30 list.* The closest are:

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,489 | 0 |

This is a utility release that provides corrected Jinja chat templates for Qwen models—not a model itself, but a practical tool for developers. Its high like count (1,489 with zero downloads) suggests community appreciation for fixing template issues in Qwen3.5.

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ, MLX)

| Model | Author | Likes | Downloads |
|-------|--------|-------|-----------|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 3,014 | 7,638,591 |
| [Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 817 | 468,746 |
| [Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 1,143 | 79,395 |
| [Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,180 | 269,805 |
| [Qwen3.8-Flash-Next-GGUF](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF) | unsloth | 374 | 0 |
| [Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 665 | 911,795 |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 757 | 1,620,754 |
| [Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 318 | 1,391,218 |
| [Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 221 | 1,389,641 |
| [Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 476 | 183,871 |
| [Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 378 | 1,318,749 |
| [Qwen3.8-27B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.8-27B-Escha-W2) | EschaLabs | 134 | 2,481 |
| [GLM-5.3-Flash-GGUF](https://huggingface.co/unsloth/GLM-5.3-Flash-GGUF) | unsloth | 133 | 0 |
| [Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 255 | 232,525 |
| [Qwen3.8-27B-Uncensored](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored) | orcarouter | 193 | 17,567 |

The quantization ecosystem around Qwen3.8-27B is extraordinary. **unsloth's GGUF** is the most-downloaded variant (7.6M), serving as the de facto standard for local inference. A proliferation of "uncensored"/abliterated versions (orcarouter, huihui-ai, OBLITERATUS, HauhauCS) demonstrates strong community demand for safety-filter-removed variants. **EschaLabs' W2** pushes 2-bit quantization, pushing the limits of extreme compression. **DavidAU's Cold-Fusion** applies experimental "GAIN Training" techniques on top of the base model.

---

## 3. Ecosystem Signal

**Qwen dominance is unprecedented.** With 16 of 30 slots dedicated to Qwen3.8 derivatives, Alibaba's ecosystem has become the default substrate for the open-weight community. The pattern is clear: a strong base model releases → community immediately produces GGUF (for llama.cpp), MLX (for Apple Silicon), abliterated/uncensored variants, and aggressive fine-tunes. Unsloth has solidified its position as the official quantization partner for major releases (Qwen, GLM), with its GGUF builds becoming the highest-download artifacts on the platform.

**Open-weight vs. proprietary:** The gap is narrowing. MiniMax, DeepSeek, Zhipu, Qwen, and Moonshot are all shipping competitive open-weight models. Kimi-K3's use of `compressed-tensors` and SenseNova's `any-to-any` pipeline suggest the next frontier is efficiency and modality convergence. GLM-5.3-Flash with arxiv citation (2602.15763) shows that research-grade models are increasingly released directly on HF as open weights.

**Generation (video/audio) is the new battleground.** MiniMax-H3 (4.8M downloads) and LTX-2.5 (894K) indicate massive demand for open video generation. Music3 extends the generative frontier into audio. The combination of language + vision + video + audio under one roof (Qwen3.8 being multimodal) suggests the industry is converging on unified foundation models.

**Quantization is now table stakes.** 50% of the list consists of GGUF/MLX/FP8/2-bit variants. The "uncensored" niche has become a cottage industry—5+ variants of the same model, each with slight prompt-template or quantization differences. This fragmentation is both a strength (choice for users) and a weakness (confusion, quality variance).

---

## 4. Worth Exploring

1. **[Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next)** — Only 2.5K downloads and tagged as `qwen4_exp`, this is an early experimental release that foreshadows Qwen4. As an analyst or developer, getting hands-on with the next-gen architecture before it explodes in popularity is high-value. Its "Flash" tier suggests efficient inference, which may define the next wave of local-first models.

2. **[EschaLabs/Qwen3.8-27B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.8-27B-Escha-W2)** — 2-bit quantization of a 27B model is aggressive. Whether it maintains usable quality at this compression level is an open question worth studying—it could unlock true edge deployment of multimodal LLMs. A rare experiment in pushing past the typical 4-bit minimum.

3. **[MiniMax-H3-Fun-Controlnet-Union](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union)** — Alibaba PAI's integration of ControlNet-Union with MiniMax-H3 video model is a practical, lesser-known gem (141 likes). For anyone working on video generation with structured control, this bridges the gap between diffusion-based video models and precise user guidance—the kind of tool that often becomes infrastructure.

---

*Report generated from Hugging Face Hub trending data (2026-08-27)*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*