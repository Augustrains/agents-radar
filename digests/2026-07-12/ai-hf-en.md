# Hugging Face Trending Models Digest 2026-07-12

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-12 01:22 UTC

---

Here is the **Hugging Face Trending Models Digest** for July 12, 2026.

---

### 1. Today's Highlights

The ecosystem is dominated by **Mixture-of-Experts (MoE)** architectures from major labs, with Tencent's Hy3, Zhipu's GLM-5.2, and a new wave of Qwen3.6 derivatives leading a shift toward efficient, high-performance reasoning. **NVIDIA** is making a strong multi-modal play with "LocateAnything-3B," a groundbreaking object localization model, while community quantizations from **Unsloth** and **empero-ai** are driving massive download numbers. The rise of agentic and video-native models—including Krea-2-Turbo and LingBot—signals a broader move beyond pure text generation toward interactive, generative applications.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)
- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — Tencent | likes: 697 | downloads: 8,210  
  A next-gen Hunyuan-based MoE model, trending for its hybrid architecture and strong language understanding.
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | likes: 3,832 | downloads: 421,270  
  Zhipu's latest MoE conversational model with DSA routing, trending for its top-tier likes and strong community adoption.
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | likes: 852 | downloads: 0  
  A utility model providing corrected chat templates for Qwen3.5, essential for developers deploying recent Qwen variants.
- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat | likes: 176 | downloads: 1,572  
  Meituan's updated long-context conversational model, optimized for extended reasoning tasks.
- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — nvidia | likes: 120 | downloads: 743  
  NVIDIA's efficient 30B MoE model with 3B active parameters, designed for lab-grade reasoning and agentic tasks.
- **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — nvidia | likes: 105 | downloads: 30,418  
  A massive puzzle-solving MoE model (75B total, 9B active), pushing the frontier of structured reasoning.
- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — SupraLabs | likes: 98 | downloads: 1,275  
  A tiny but specialized router model for directing LLM inference, highlighting the trend toward model routing and orchestration.
- **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)** — AliesTaha | likes: 199 | downloads: 5,053  
  A Qwen3-based instruct model fine-tuned on synthetic "fable" reasoning traces, trending for its focus on structured thought.
- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — mistralai | likes: 189 | downloads: 350  
  Mistral's latest massive MoE (119B total, 6B active), representing the frontier of open-weight, high-efficiency base models.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | likes: 768 | downloads: 186,852  
  A Qwen3.5-based vision-language model with Claude-style reasoning, trending for its strong multimodal reasoning benchmark performance.
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | likes: 1,929 | downloads: 1,380,690  
  Baidu's state-of-the-art OCR model, trending for its high download count and versatility across document and scene text.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | likes: 2,651 | downloads: 2,641,936  
  An uncensored, vision-capable MoE fine-tune of Qwen3.6, trending for its aggressive style and massive community downloads.
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | likes: 2,707 | downloads: 1,472,194  
  NVIDIA's universal open-vocabulary object localization model, trending for its high accuracy and broad industrial applicability.
- **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — migtissera | likes: 84 | downloads: 806  
  A Qwen3.5-based vision-language assistant, trending as a specialized multimodal conversational agent.
- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | likes: 99 | downloads: 0  
  A text-to-video identity preservation LoRA built on LTX-Video, trending for its high-quality face consistency.
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | likes: 588 | downloads: 168,154  
  Krea's fast text-to-image diffusion model, trending for its speed and integration with the Krea-2 ecosystem.
- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — robbyant | likes: 85 | downloads: 381  
  A novel video-native MoE diffusion model, trending as an early sign of MoE architectures entering video generation.
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | likes: 109 | downloads: 12,817  
  A unified speech transcription and diarization model, trending for its end-to-end approach to meeting intelligence.
- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** — CohereLabs | likes: 89 | downloads: 7,687  
  Cohere's dedicated Arabic ASR model, trending as a strong example of language-specific specialization.
- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — open-gigaai | likes: 121 | downloads: 0  
  A world model diffusion checkpoint, trending for its ambitious attempt at video-level world simulation.

#### 🔧 Specialized Models (code, math, embeddings, tabular)
- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google | likes: 348 | downloads: 20,110  
  Google's zero-shot tabular foundation model in PyTorch, trending for its potential to revolutionize tabular ML without fine-tuning.
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | likes: 1,150 | downloads: 436,530  
  A Gemma-4-based agentic coding model with structured fable reasoning, trending for its terminal and agentic tool-use capabilities.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | likes: 2,014 | downloads: 1,944,961  
  The GGUF quantization of Qwythos-9B, trending for making advanced reasoning accessible on consumer hardware.
- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | likes: 191 | downloads: 29,887  
  A tiny 1B GGUF model with Claude-style thinking, trending for packing advanced reasoning into a sub-2B parameter footprint.
- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — unsloth | likes: 140 | downloads: 38,922  
  Unsloth's fast GGUF quant of DeepSeek-V4, trending for its inference speed optimizations and the DeepSeek lineage.
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | likes: 850 | downloads: 1,216,495  
  A 35B GGUF model, trending for its MIT license and high compatibility with inference endpoints.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | likes: 1,048 | downloads: 2,904,169  
  Unsloth's Multi-Token Prediction GGUF of Qwen3.6-27B, trending for its record-breaking download speed and novel training objective.
- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | likes: 235 | downloads: 4,128  
  A Qwen3.6-27B fine-tune focused on chain-of-thought reasoning, trending as a "thinking cap" enhancement.
- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | likes: 186 | downloads: 0  
  A LoRA for identity-consistent image editing on Krea-2, trending in the ComfyUI community for portrait customization.
- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | likes: 494 | downloads: 28,141  
  A Qwen3.5 MoE model fine-tuned specifically for agentic tool use, trending as a community-driven "agent foundation model."

### 3. Ecosystem Signal

The landscape is defined by three converging trends: **MoE dominance**, **Qwen ecosystem lock-in**, and **quantization commoditization**. Nearly every major release—from Tencent's Hy3 and GLM-5.2 to NVIDIA's Nemotron series—leverages Mixture-of-Experts, often with sparsely activated parameters (e.g., 30B total / 3B active). This shift enables frontier-level reasoning at consumer-grade inference costs.

**Qwen3.5/3.6** has become the default base for fine-tuning, powering models like Qwythos, ThinkingCap, and dozens of GGUF variants. Unsloth's GGUF quantizations are now the de facto distribution channel, with Qwen3.6-27B-MTP-GGUF crossing 2.9M downloads. Open-weight models are clearly winning the rate of iteration: the community can fine-tune and quantize faster than any single lab.

Notably, **NVIDIA** is pioneering multimodal localization (LocateAnything-3B) while **Google** brings foundation models to tabular ML. The rise of "agentic" tags on models (Gemma-4-agentic, Agents-A1) signals that the next battleground is tool-use and autonomous reasoning, not just raw perplexity.

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This is likely the most immediately useful model on the list: run any image through it with a text query (e.g., "find the red car") and get bounding boxes. It democratizes object detection without any training, making it essential for robotics, UI automation, and content moderation.

2. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — With 2.9M downloads in a week, this is the benchmark for efficient, quantized MoE. It introduces Multi-Token Prediction for faster generation—study it to understand the next generation of LLM inference optimization.

3. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — At 3.8K likes, this is the most liked model on the list. It represents the cutting edge of Chinese MoE architecture with DSA routing. Worth exploring for its strong conversational quality and as a counterpoint to the Qwen-dominated ecosystem.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*