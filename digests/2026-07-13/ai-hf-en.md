# Hugging Face Trending Models Digest 2026-07-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-13 01:23 UTC

---

# Hugging Face Trending Models Digest — July 13, 2026

## Today's Highlights

This week's Hugging Face landscape is dominated by the Qwen 3.6 family, with multiple variants (uncensored, reasoning, MTP, NVFP4) collectively amassing millions of downloads. NVIDIA makes a strong push with three new models spanning spatial reasoning, general-purpose language, and audio understanding. Quantized GGUF releases continue to drive community adoption, while specialized models for OCR, speech transcription, and world modeling signal growing maturity across modalities. The open-weight ecosystem is thriving, with Chinese labs (Tencent, Baidu, Zhipu AI) and Western players (NVIDIA, Google, Cohere) competing for attention.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — Tencent | 721 likes, 8.7k downloads  
  A new text-generation model from Tencent's Hunyuan lineage, likely a successor to their Hy2 series with improved reasoning and multilingual capabilities.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,857 likes, 441k downloads  
  A MoE-DSA architecture conversational model from the GLM family, trending due to strong benchmark performance and efficient inference.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 510 likes, 29k downloads  
  A Qwen 3.5 MoE-based model optimized for agentic workflows, bridging the gap between language understanding and tool-use capabilities.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat | 182 likes, 1.8k downloads  
  A conversational text-generation model from Meituan, likely optimized for long-context dialogue and Chinese-language use cases.

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — SupraLabs | 107 likes, 1.4k downloads  
  A lightweight 51M-parameter routing model for language tasks, gaining interest as a building block for multi-model orchestration.

- **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — migtissera | 94 likes, 971 downloads  
  A 27B multimodal (image-text-to-text) model using Qwen 3.5 architecture, part of the Tess series known for creative reasoning.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Baidu | 1,943 likes, 1.4M downloads  
  A feature-extraction OCR model built on transformer architecture, trending due to its unlimited scope and Baidu's enterprise-grade document AI.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — NVIDIA | 2,716 likes, 1.5M downloads  
  A 3B parameter image-text-to-text model for spatial object localization, gaining traction in robotics and visual grounding applications.

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** — NVIDIA | 131 likes, 901 downloads  
  An audio-focused text-generation model for speech understanding and diarization tasks, expanding NVIDIA's Nemotron ecosystem.

- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — open-gigaai | 123 likes, 0 downloads  
  A diffusion-based world model for visual generation, notable for its Apache-2.0 license and potential in simulation environments.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 111 likes, 0 downloads  
  A LoRA for identity-preserving text-to-video generation using LTX-Video, trending for deepfake creation and virtual avatar applications.

- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — robbyant | 91 likes, 461 downloads  
  A MoE-based video generation model with 30B parameters (3B active), designed for efficient long-form video synthesis.

- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** — CohereLabs | 95 likes, 9.9k downloads  
  A specialized Arabic automatic speech recognition model from Cohere, addressing a critical gap in multilingual speech tools.

- **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** — nineninesix | 85 likes, 2.3k downloads  
  A text-to-speech model built on Qwen 3.5 architecture, demonstrating the convergence of language models and speech synthesis.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Google | 357 likes, 21k downloads  
  Google's TabFM foundational model for tabular data with zero-shot classification and regression capabilities, a rare open-weight entry into structured data.

- **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — NVIDIA | 113 likes, 34.8k downloads  
  A 75B parameter MoE model with 9B active parameters, optimized with NVFP4 precision for puzzle-solving and reasoning tasks.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 130 likes, 14.5k downloads  
  An audio-text-to-text model for combined transcription and speaker diarization, trending due to growing demand for meeting automation.

- **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** — robbyant | 85 likes, 0 downloads  
  A 14B causal world model for image-to-video generation, gaining interest in physical intelligence and simulation tasks.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,047 likes, 1.97M downloads  
  A GGUF quantized Qwen 3.5 variant fine-tuned with synthetic Claude-style data, extremely popular for its reasoning quality at 9B scale.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,676 likes, 2.6M downloads  
  An uncensored, aggressive-preference-tuned Qwen 3.6 MoE model with vision capabilities, one of the most downloaded models this week.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1,159 likes, 445k downloads  
  A GGUF quantized Gemma 4 fine-tune for agentic coding and terminal tasks, reflecting the growing demand for developer-focused models.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 201 likes, 49.3k downloads  
  A tiny 1B thinking model quantized with GGUF, impressive for its small size and reasoning capability.

- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — unsloth | 152 likes, 44.6k downloads  
  An unsloth-quantized DeepSeek V4 Flash model, leveraging an arxiv paper (2606.19348) and DeepSeek's rapid release cadence.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 865 likes, 0 downloads  
  A utility release providing corrected chat templates for Qwen 3.5 models, essential for deployment stability in MLX and llama.cpp.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF)** — bottlecapai | 83 likes, 312k downloads  
  A token-efficient thinking model GGUF quantized from Qwen 3.6, optimized for chain-of-thought reasoning with reduced inference cost.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 1,057 likes, 2.9M downloads  
  The most downloaded model this week, a Qwen 3.6 Multi-Token Prediction variant quantized by Unsloth, enabling faster speculative decoding.

- **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)** — unsloth | 179 likes, 1.38M downloads  
  An NVFP4-precision quantized version of Qwen 3.6, offering high-quality inference on NVIDIA hardware with reduced memory footprint.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 855 likes, 1.35M downloads  
  A MIT-licensed 35B GGUF model compatible with inference endpoints, trending for its permissive license and strong general performance.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 212 likes, 0 downloads  
  A LoRA for identity-consistent image editing built on Krea-2 base, demonstrating the ongoing interest in controllable image generation.

## Ecosystem Signal

The Qwen 3.6 family has clearly become the dominant open-weight lineage this week, with over 6.8 million total downloads across its variants. The "reasoning + quantization + MoE" formula is winning: models combine Mixture-of-Experts efficiency (e.g., 35B-A3B, 75B-A9B) with chain-of-thought capabilities and widespread quantization via GGUF and NVFP4. Unsloth continues to be the premier quantization infrastructure, powering three of the top-10 most downloaded models.

From China, Tencent's Hy3 and Zhipu AI's GLM-5.2 signal that the GLM lineage remains competitive, while Meituan's LongCat-2.0 indicates growing enterprise interest. NVIDIA is investing heavily in specialization—spatial reasoning (LocateAnything-3B), audio (Audex-30B), and puzzle-solving (75B)—showing a "specialized small models" strategy over a single monolithic flagship.

Proprietary-to-open-weight conversion is accelerating: synthetic data from Claude and Opus models is being used to fine-tune smaller Qwen and Gemma models (see Qwythos-9B, MiniCPM5-1B), creating a feedback loop where community models approximate API-only behavior. The GGUF ecosystem now supports nearly every major architecture, making local deployment the default consumption pattern. An emerging trend is "utility models"—chat template fixes, token-efficient variants, routing layers—signaling infrastructure maturity beyond raw model weights.

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A compact 3B model bridging vision-language understanding with spatial reasoning, ideal for robotics and visual grounding pipelines. Its high likes-to-downloads ratio suggests strong community validation.

2. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — As the most downloaded model this week, this Multi-Token Prediction variant is worth studying for its speculative decoding performance gains. Essential reading for researchers in inference optimization.

3. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 1.4 million downloads and transformer-based architecture, this OCR model represents a rare open-weight release from a major Chinese tech company in the document AI space. Highly practical for enterprise document processing workflows.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*