# Hugging Face Trending Models Digest 2026-08-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-21 00:32 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-21

---

## 1. Today's Highlights

Qwen's **Qwen3.8-27B** continues to dominate the ecosystem, with the base multimodal model and its quantized variants collectively exceeding **7.8 million downloads** this week. Moonshot AI's **Kimi-K3** has emerged as a major challenger with over 10.8K likes, signaling intensifying competition in the open-weight frontier. MiniMax is aggressively expanding its **H3** video generation family with the new **MiniMax-Music3** for text-to-audio, plus a community Turbo variant. The "uncensored/abliterated" fine-tuning wave around Qwen3.8 shows no signs of slowing, with 7 distinct community releases in this week's top 30. Notably, DeepSeek's **V4 series** (Pro and Flash) has entered the trending chart with strong adoption, signaling a two-horse race between Qwen and DeepSeek for open-weight supremacy.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs & Chat)

- [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) — *Qwen* | ⭐ 11,743 | ⬇️ 1,373,584
  The flagship multimodal 27B model from Qwen, setting the standard for open-weight vision-language performance.
- [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — *moonshotai* | ⭐ 10,883 | ⬇️ 2,349,853
  Moonshot AI's latest open-weight model featuring compressed-tensor technology, rivaling Qwen in popularity.
- [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) — *deepseek-ai* | ⭐ 678 | ⬇️ 43,287
  The flagship dense model of DeepSeek's fourth generation, optimized for complex reasoning and long-context tasks.
- [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — *deepseek-ai* | ⭐ 3,575 | ⬇️ 2,547,549
  The fast, lightweight variant of DeepSeek V4, designed for high-throughput inference at scale.
- [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) — *Qwen* | ⭐ 1,121 | ⬇️ 14,592
  Qwen's massive MoE model with 2.4T total parameters and 95B active, pushing the frontier of open-weight scale.
- [**ornith-ai/Ornith-1.5-35B-A3B**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) — *ornith-ai* | ⭐ 214 | ⬇️ 1,713
  An efficient 35B MoE model with only 3B active parameters, interesting for edge and low-latency deployments.
- [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) — *0bserverx* | ⭐ 189| ⬇️ 326,638
  A community abliterated variant of Qwen3.8 pushing the "Heretic" uncensored agenda.
- [**superwhisper/s1-mini**](https://huggingface.co/superwhisper/s1-mini) — *superwhisper* | ⭐ 152 | ⬇️ 348
  A compact speech recognition model built on a Qwen3 architecture, optimized for ASR tasks.

---

### 🎨 Multimodal & Generation (Image, Video, Audio)

- [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — *MiniMaxAI* | ⭐ 4,238 | ⬇️ 3,308,673
  MiniMax's latest video generation model supporting text-to-video, image-to-video with impressive quality.
- [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) — *Lightricks* | ⭐ 1,415 | ⬇️ 611,825
  A single-file diffusion model for video generation, offering flexibility across text, image, and video inputs.
- [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) — *MiniMaxAI* | ⭐ 1,104 | ⬇️ 14,471
  A dedicated text-to-music generation model, marking MiniMax's expansion into audio generation.
- [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) — *lightx2v* | ⭐ 652 | ⬇️ 380,072
  A community-optimized Turbo variant of MiniMax-H3 for faster video inference.
- [**TenStrip/10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) — *TenStrip* | ⭐ 298 | ⬇️ 0
  A fine-tune of MiniMax-H3 specialized for niche content generation, showcasing community adaptation.
- [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) — *meta-models* | ⭐ 1,718 | ⬇️ 478,622
  A 30B multimodal model from Meta's experimental line, blending vision-language capabilities with conversational AI.
- [**dots-studio/dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) — *dots-studio* | ⭐ 242 | ⬇️ 1,373
  A multimodal note-taking focused model, previewing Dot's third-generation assistant.

---

### 📦 Fine-tunes & Quantizations

- [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) — *unsloth* | ⭐ 2,355 | ⬇️ 5,126,652
  The most downloaded quantization of Qwen3.8, enabling local deployment across devices.
- [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) — *Qwen* | ⭐ 633 | ⬇️ 1,517,643
  Official FP8 precision version of Qwen3.8 for efficient deployment on enterprise hardware.
- [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) — *JonathanColetti* | ⭐ 512 | ⬇️ 979,768
  A popular uncensored GGUF variant with Multi-Token Prediction (MTP) support for faster generation.
- [**unsloth/Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) — *unsloth* | ⭐ 308 | ⬇️ 831,483
  NVIDIA-specific 4-bit floating point quantization by unsloth, optimized for Blackwell GPUs.
- [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) — *orcarouter* | ⭐ 712 | ⬇️ 2,628
  An abliterated MLX port for Apple Silicon, bringing uncensored Qwen3.8 to Mac users.
- [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) — *orcarouter* | ⭐ 676 | ⬇️ 76,109
  FP8 quantization of the abliterated Qwen3.8, balancing quality with hardware efficiency.
- [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) — *HauhauCS* | ⭐ 364 | ⬇️ 268,258
  An aggressively quantized uncensored variant with MTP, targeting maximum inference speed.
- [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) — *froggeric* | ⭐ 1,338 | ⬇️ 0
  A community fix for Qwen chat template issues, highlighting the ecosystem's self-correcting nature.
- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) — *huihui-ai* | ⭐ 200 | ⬇️ 187,008
  Huihui's take on the abliterated Qwen3.8, one of the most trusted community fine-tuners.
- [**Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF**](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) — *Blackfrost-AI* | ⭐ 183 | ⬇️ 186,470
  Another popular abliterated GGUF variant, showing the demand for "uncensored" local models.
- [**OBLITERATUS/Qwen3.8-27B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) — *OBLITERATUS* | ⭐ 266 | ⬇️ 4,415
  A multi-format abliterated release supporting both GGUF and MLX, with a memorable name.
- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) — *huihui-ai* | ⭐ 200 | ⬇️ 10,540
  The full-precision version of Huihui's abliterated Qwen3.8 without quantization loss.
- [**ornith-ai/Ornith-1.5-35B-A3B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) — *ornith-ai* | ⭐ 160 | ⬇️ 53,691
  GGUF quantizations of Ornith's efficient MoE model, MIT-licensed and endpoint-compatible.
- [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) — *empero-ai* | ⭐ 222 | ⬇️ 55,074
  A refined GGUF quantization from empero-ai, optimized for llama.cpp workflows.

---

## 3. Ecosystem Signal

The Qwen3.8 model family is the clear ecosystem center of gravity this week, dominating the trending chart with **12 of the top 30 models** derived from it. The sheer volume of community adaptations—from abliterated variants to multi-format quantizations—demonstrates both the model's technical quality and the ecosystem's deep investment in its success. The "uncensored/abliterated" subculture remains a powerful ecosystem driver, though it raises questions about platform governance and responsible AI deployment.

In parallel, we're witnessing a **strategic race among Chinese AI labs** for open-weight leadership: Qwen, DeepSeek, Moonshot AI, and MiniMax all launched flagship models within weeks of each other. The **DeepSeek V4 series** appears to be gaining significant traction based on rapid download velocity despite lower like counts, indicating strong word-of-mouth in deployment communities. Open-weight models are clearly winning the ecosystem battle, with each release setting new performance baselines that narrow the gap with proprietary frontier models.

**Quantization and efficiency** are becoming first-class concerns directly at the source: Qwen now ships official FP8 variants, unsloth provides NVFP4 for NVIDIA hardware, and MLX ports enable Apple Silicon deployment. The MoE architecture is emerging as the efficiency solution of choice, with Qwen and Ornith both fielding sparse models that dramatically reduce inference costs. MiniMax's expansion from video into music generation signals the broadening scope of generative AI, while community fine-tunes of video models (like 10Eros-Max) demonstrate the growing maturity of video-generation customization.

---

## 4. Worth Exploring

1. **Kimi-K3 (moonshotai)** — Positioned as a direct challenger to Qwen's dominance with 10.8K likes in its first week, its **compressed-tensor technology** could represent a genuine architectural innovation. Understanding its approach is essential for anyone tracking the open-weight frontier's evolution.

2. **MiniMax-Music3** — Music generation is still an early-stage modality compared to text and video. MiniMax's foray could define the open-weight music generation landscape, making this model worth studying for both its technical approach and product strategy.

3. **DeepSeek-V4-Flash-0731** — The download-to-like ratio (2.5M downloads vs 3.5K likes) makes this the most quietly successful model this week. Its practical deployment in production environments suggests it's solving real infrastructure problems that the community is only now starting to acknowledge through likes.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*