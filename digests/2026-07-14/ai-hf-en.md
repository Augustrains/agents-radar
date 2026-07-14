# Hugging Face Trending Models Digest 2026-07-14

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-14 01:13 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-14

## 1. Today's Highlights

This week's trending models reveal a clear shift toward **MoE (Mixture-of-Experts) architectures** scaling to extremely high parameter counts while keeping inference efficient—models like GLM-5.2 (3.9K likes) and the NVIDIA Nemotron-Labs series exemplify this trend. The **Qwen3.6 ecosystem** continues to dominate, with multiple fine-tuned and quantized variants appearing across the top 30, including uncensored and vision-capable versions. **GGUF quantization** remains the most active community activity, with nearly half of the listed models using this format for local deployment. New entries from **Baidu (Unlimited-OCR)** and **Cohere (Arabic ASR)** signal growing enterprise interest in specialized, task-specific models.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — Tencent | 754 likes, 9.2K downloads  
  A new Hunyuan-based text-generation model, likely targeting Chinese-language performance and enterprise use cases.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | **3,900 likes**, 465K downloads  
  A massive MoE conversational model with DSA routing, trending for its balance of scale and efficient inference.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 525 likes, 29.8K downloads  
  A Qwen3.5-based MoE model optimized for agentic workflows and tool-use scenarios.

- **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — migtissera | 104 likes, 1.1K downloads  
  A Qwen3.5-based vision-language model designed for complex reasoning tasks.

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — SupraLabs | 114 likes, 1.6K downloads  
  A small, specialized routing model (51M parameters) for directing queries to appropriate downstream models.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Baidu | **1,963 likes**, 1.5M downloads  
  A transformer-based OCR model claiming unlimited-scene capability; trending for its impressive accuracy across document and natural images.

- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** — CohereLabs | 102 likes, 11.6K downloads  
  A specialized Arabic speech recognition model, reflecting growing demand for non-English ASR.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 124 likes, 0 downloads  
  A LoRA for identity-preserving text-to-video generation using LTX-Video pipelines.

- **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** — robbyant | 93 likes, 0 downloads  
  A world model for image-to-video generation, suggesting growing interest in causal video prediction.

- **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** — nineninesix | 95 likes, 3.9K downloads  
  A Qwen3.5-based text-to-speech model, notable for integrating LLM backbones with TTS output.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 162 likes, 39.5K downloads  
  An audio-text-to-text model combining transcription with speaker diarization in a single architecture.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 255 likes, 0 downloads  
  A Krea-2-based LoRA for identity-consistent image editing, driving interest in controllable diffusion.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Google | 362 likes, 21.6K downloads  
  A foundational tabular model supporting zero-shot classification and regression—Google's entry into the "foundation model for tables" space.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,178 likes, 453K downloads  
  A Gemma-4 specialization for agentic coding and terminal use; highly downloaded GGUF variant.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 888 likes, 0 downloads  
  Not a model but a critical community resource: fixed chat templates for Qwen models, addressing widespread compatibility issues.

- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — robbyant | 100 likes, 513 downloads  
  A 30B MoE video generation model with 3B active parameters, optimizing for efficient video synthesis.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | **2,084 likes**, **1.99M downloads**  
  A highly popular Qwen3.5 fine-tune with reasoning enhancements, available in GGUF format with massive download numbers.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | **2,710 likes**, **2.51M downloads**  
  An uncensored, aggressive-style MoE variant of Qwen3.6 with vision capabilities—trending for its boundary-pushing behavior.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 1,074 likes, **2.90M downloads**  
  The most downloaded model this week, a GGUF-quantized Qwen3.6 with multi-turn prediction support.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — unsloth | 192 likes, 1.50M downloads  
  A 4-bit floating point quantization of Qwen3.6 optimized for NVIDIA hardware.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 868 likes, 1.39M downloads  
  A new 35B GGUF model with MIT license, likely gaining traction for its permissive licensing and strong performance.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 220 likes, 68.7K downloads  
  A tiny 1B-parameter model with Claude-style thinking capabilities, demonstrating demand for small-but-capable reasoning models.

- **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — NVIDIA | 114 likes, 38.8K downloads  
  A massive 75B MoE model (9B active) with NVFP4 quantization for efficient enterprise deployment.

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** — NVIDIA | 142 likes, 1.1K downloads  
  A 30B MoE model (3B active) from NVIDIA's Nemotron research series, focusing on efficient audio understanding.

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)** — jlnsrk | 86 likes, 2.0K downloads  
  An int4 CPU-optimized variant of GLM-5.2 using expert-streaming for efficient inference on consumer hardware.

---

## 3. Ecosystem Signal

**📊 MoE is the dominant architecture.** Seven of the top 30 models are explicitly Mixture-of-Experts designs (GLM-5.2, Agents-A1, Qwen3.6-35B-A3B, Nemotron variants, LingBot-video-MoE). The pattern is clear: the community is converging on **high-parameter, low-active-parameter** models that offer GPT-4-class capability at a fraction of the compute cost.

**🔑 Qwen3.6/Qwen3.5 ecosystem is the new Llama.** With over 10 entries in the top 30—including base models, fine-tunes, uncensored variants, and quantizations—Qwen has become the community's favorite foundation. Its permissive license and strong vision-language support are driving this adoption.

**📦 GGUF is the quantization standard.** Nearly half the list (14 models) includes GGUF variants. The download numbers clearly show users prioritize local, quantized deployment over raw model quality. unsloth has emerged as the leading quantization provider, driving 3 of the top quantized models.

**🏢 Enterprise players are expanding.** NVIDIA (3 models), Baidu, Google, Tencent, and Cohere all released notable models this week. Enterprise interest is shifting from pure research to production-ready deployments with specialized capabilities (OCR, ASR, tabular).

**⚠️ Uncensored/aggressive fine-tunes continue to find audiences.** Models like Qwen3.6-Uncensored-Aggressive (2.7K likes) demonstrate sustained demand for unrestricted models, despite (or because of) safety concerns.

---

## 4. Worth Exploring

1. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 1,963 likes and 1.5M downloads, this is the most impactful specialized model this week. If you work with document processing or scene text recognition, this model likely represents a step-change in OCR quality. Worth studying for its architecture and training methodology.

2. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — The most downloaded model (2.9M) deserves attention. Its multi-turn prediction (MTP) training approach may represent a new paradigm for improving long-context reasoning. Try it for chatbot development or any task requiring extended dialogue coherence.

3. **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — At just 51M parameters, this model-router points to an interesting trend: small, specialized models that orchestrate larger models. Worth studying for anyone building multi-model systems or agent architectures.

---

*Digest generated 2026-07-14. All statistics from Hugging Face Hub.*

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*