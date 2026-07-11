# Hugging Face Trending Models Digest 2026-07-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-11 01:20 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-11

## 1. Today's Highlights

This week's leaderboard is dominated by a massive wave of Qwen3.6 derivative models, quantization efforts, and multimodal MoE architectures. **Qwythos-9B** and **HauhauCS/Qwen3.6-35B-A3B** are seeing explosive download numbers, indicating strong community appetite for uncensored, vision-capable models in GGUF format. **NVIDIA's LocateAnything-3B** (2,700 likes) highlights growing demand for specialized spatial reasoning models. Meanwhile, **zai-org/GLM-5.2** (3,785 likes) signals continued momentum for the Chinese GLM family in conversational AI. The prevalence of MoE architectures (6+ models) and GGUF quantizations (10+ entries) confirms these are the dominant themes in the open-weight LLM ecosystem right now.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — Tencent | 664 likes | 6,923 downloads  
  Hunyuan v3 text-generation model, trending as a major Chinese AI lab release with strong community reception.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,785 likes | 392,655 downloads  
  Conversational MoE model from the GLM family, trending as one of the most liked models this week with strong out-of-the-box chat performance.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 463 likes | 33,088 downloads  
  Latest pro version of DeepSeek V4 with spark attention, linked to arxiv:2606.19348 — driving research interest in efficient transformer architectures.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 835 likes | 1M+ downloads  
  MIT-licensed 35B GGUF model, trending for its permissive license and high download volume suggesting broad deployment use.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — mistralai | 184 likes | 315 downloads  
  Massive 119B MoE (6B active) from Mistral, notable as a large open-weight model with Apache-2.0 license and vLLM compatibility.

- **[NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — nvidia | 99 likes | 23,404 downloads  
  NVIDIA's 75B MoE puzzle-solving model in NVFP4 precision, targeting reasoning-heavy applications.

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — SupraLabs | 86 likes | 1,160 downloads  
  Tiny 51M router model for LLM orchestration, trending as a lightweight alternative for agent routing.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,700 likes | 1.4M downloads  
  Spatial grounding model for object localization, one of the highest-liked releases this week with massive downloads.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 575 likes | 164,525 downloads  
  Text-to-image diffusion model, part of the Krea-2 ecosystem — trending for its turbo-optimized inference speed.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,921 likes | 1.3M downloads  
  OCR model from Baidu, trending for unlimited character recognition capability and massive download numbers.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 83 likes | 0 downloads  
  Identity-preserving text-to-video model based on LTX-2, trending as an early zero-shot reference-to-video approach.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 98 likes | 5,919 downloads  
  Audio-to-text model combining transcription with speaker diarization, serving voice AI pipelines.

- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — open-gigaai | 118 likes | 0 downloads  
  Apache-2.0 licensed diffusion model, likely a world model or generative foundation model for 3D/world simulation.

- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — robbyant | 75 likes | 317 downloads  
  Video MoE model with LingBotVideoPipeline, enabling efficient video understanding with sparsely activated 30B parameters.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google | 345 likes | 18,626 downloads  
  Google's tabular foundation model supporting zero-shot classification and regression — a rare tabular-specific release.

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — nvidia | 336 likes | 787,748 downloads  
  NVIDIA-optimized Qwen3.6 with 4-bit floating point quantization, demonstrating NVIDIA's ModelOpt toolkit for production deployment.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 470 likes | 25,772 downloads  
  Qwen3.5-based MoE model optimized for agent tasks, part of the growing "agents-as-models" trend.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat | 170 likes | 1,308 downloads  
  Long-context conversational model from Meituan, optimized for extended dialogue sessions.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 836 likes | 0 downloads  
  Corrected chat templates for Qwen models in MLX format — surprising popularity for a purely metadata/model config fix.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 1,976 likes | 1.9M downloads  
  GGUF-quantized Claude-Mythos fine-tune on Qwen3.5, highest downloads of any model this week — community favorite for roleplay/reasoning.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,623 likes | 2.6M downloads  
  Uncensored MoE vision-language model with GGUF quantization, massive download count reflecting demand for unrestricted models.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 1,036 likes | 2.9M downloads  
  Unsloth's MTP (Multi-Turn Prompting) optimized Qwen3.6 GGUF — highest raw downloads this week, powered by unsloth's efficient quantization workflow.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,134 likes | 427,668 downloads  
  Gemma-4 fine-tune focused on agentic coding tasks, demonstrating Google Gemma's adoption in the community fine-tuning ecosystem.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 157 likes | 9,029 downloads  
  Tiny 1B thinking model GGUF from MiniCPM5 — notable for achieving reasoning capability at extremely small scale.

- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — unsloth | 124 likes | 31,895 downloads  
  Flash-attention optimized GGUF of DeepSeek V4 from unsloth, bringing deepseek's architecture to CPU/GPU inference efficiently.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | 761 likes | 184,315 downloads  
  The non-quantized sibling of the top GGUF model, full-precision version seeing strong downloads for those preferring FP16 inference.

## 3. Ecosystem Signal

The current ecosystem shows two clear gravitational centers: **Qwen** and **MoE**. Qwen derivatives appear in 9 of the 30 trending models — from Qwen3.5 to Qwen3.6, covering base, uncensored, GGUF, NVFP4, and agent-tuned variants. This suggests Qwen has become the default foundation for community fine-tuning, displacing Llama's previous dominance.

**MoE architecture** is now mainstream, appearing in 6+ models (GLM-5.2, Agents-A1, Nemotron-Labs, HauhauCS Qwen3.6, Leanstral-1.5, LingBot-Video). The "small active parameters / large total parameters" pattern (e.g., 35B-A3B, 30B-A3B, 119B-A6B) is now standard, enabling deployment efficiency without sacrificing total parameter count.

**Open-weight remains dominant** — nearly all models are open-weights, with no significant proprietary releases. Apache-2.0 and MIT licenses appear frequently, suggesting permissive licensing is key to viral adoption.

**GGUF quantization** now represents a full sub-ecosystem, with unsloth emerging as a major infrastructure provider. The presence of both full-precision and GGUF versions of the same model (Qwythos-9B) indicates producers are targeting both server and local inference markets simultaneously.

NVIDIA's **NVFP4 quantization** and **ModelOpt** ecosystem represent a competing quantization format to GGUF, particularly for enterprise GPU deployment — worth watching as NVIDIA increases tooling investment.

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — At 2,700 likes with 3B parameters, this model signals a shift toward small, specialized spatial reasoning models. It's worth exploring as a drop-in component for robotic perception, visual grounding, or UI automation pipelines that need precise object localization without a massive LLM overhead.

2. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — The highest-liked model this week (3,785) with 392k downloads. Its MoE-DSA (Dynamic Sparse Attention) architecture is worth studying as it represents a distinct design philosophy from the Qwen/DeepSeek lineage. For multilingual Chinese + English conversational AI, this may outperform Qwen-based alternatives.

3. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive-GGUF](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — The 2.6M downloads in one week make this the most commercially relevant model to study. It represents the confluence of three key trends: MoE efficiency (35B total, 3B active), vision-language capability, and uncensored fine-tuning. Understanding what drives its popularity is essential for anyone building products on open-weight LLMs.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*