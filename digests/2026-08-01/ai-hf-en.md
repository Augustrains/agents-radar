# Hugging Face Trending Models Digest 2026-08-01

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-01 01:27 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-01

---

## 1. Today's Highlights

This week's trending list is dominated by a major release from **Moonshot AI** — the **Kimi-K3** multimodal model (9,278 likes, 493K downloads) — along with a wave of derivative GGUF quantizations from Unsloth and the community. **DeepSeek-V4-Flash** (1,923 likes, 2.9M downloads) leads the pure text-generation category with massive adoption, while **Baidu's Unlimited-OCR** (3,661 likes, 2.5M downloads) stands out as the top multimodal utility model. Notably, **uncensored community fine-tunes** of Qwen3.6 models (HauhauCS, DavidAU, LuffyTheFox) show explosive download counts, indicating a strong consumer appetite for open, unfiltered chat models. The list also signals a growing trend toward **ternary/2-bit quantization** (prism-ml's Ternary-Bonsai, nota-ai's NVFP4) and **CPU-friendly TTS models** for edge deployment.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat, Instruction-Tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|---|---|---|---|---|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 996 | 0 | Freshly released V4 iteration of DeepSeek's Flash line; expected to set new benchmarks for efficiency vs. performance. |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,923 | 2.9M | Highly adopted flagship text-generation model from DeepSeek, currently the most-downloaded LLM on this list. |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,707 | 1.65M | Z.ai's conversational MoE model with DSA (dynamic sparse attention); major community favorite for general chat. |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 863 | 76K | Poolside's code-oriented LLM iteration, trending among enterprise software engineering users. |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 595 | 27K | Compact 3B model gaining traction for lightweight deployment scenarios. |
| [Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 714 | 13K | Upstage's large-scale open-weight model; notable for its 250B parameter count and Apache-style openness. |
| [Inkling](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,664 | 57K | Multimodal conversational model from Thinking Machines; strong community following. |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 196 | 3K | Smaller sibling of Inkling, optimized for efficiency. |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 352 | 579 | Small MoE model built on Qwen3.5 architecture; early-stage but gaining interest. |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 326 | 869 | Pro variant with agentic-search capabilities; emerging as a tool-use focused model. |

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|---|---|---|---|---|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,278 | 493K | **Hottest release of the week** — Moonshot's flagship multimodal model with feature-extraction and compressed-tensor support. |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,661 | 2.51M | Baidu's OCR powerhouse; the most-downloaded multimodal model this week, suggesting strong production utility. |
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 234 | 2.7K | Microsoft's computer-use agent model — notable for GUI automation and screen understanding. |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 149 | 5.7K | Microsoft's vision-language model, paired with a ComfyUI flow (Mage-Flow) for generative workflows. |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 151 | 2.5K | New TTS model with feature-extraction capabilities; early preview attracts audio researchers. |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 348 | 1.4K | CPU-friendly edge TTS; part of a push toward local, on-device speech synthesis. |
| [Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 121 | 802 | Nano variant of Inflect, targeting ultra-lightweight deployments. |
| [VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 134 | 5.5K | Microsoft's bit-level ASR model with GGML/GGUF support — signals efficient speech recognition on edge. |
| [Mage-Flow](https://huggingface.co/Comfy-Org/Mage-Flow) | Comfy-Org | 106 | 60K | ComfyUI workflow tied to Mage-VL; trending for generative media pipelines. |

### 🔧 Specialized Models (Code, Math, Medical, Embeddings, Speech)

| Model | Author | Likes | Downloads | Why it's trending |
|---|---|---|---|---|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 371 | 10K | Qwen3.5-MoE-based code generation model; gaining developer traction. |

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|---|---|---|---|---|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,146 | 1.12M | Massive community download count for an uncensored Qwen3.6 fine-tune in GGUF format. |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,205 | 1.84M | **Most-downloaded fine-tune** this week; uncensored MoE with vision, optimized for local use. |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 270 | 212K | Hermes-style uncensored GGUF; popular among local LLM enthusiasts. |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 174 | 262K | Smaller yet highly downloaded uncensored Qwen3.5 GGUF with NEO Imatrix. |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 228 | 36K | Official Unsloth quantization of Kimi-K3 — the fastest path to running Kimi-K3 locally. |
| [Kimi-K3](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 215 | 1K | Unsloth's non-GGUF optimized version of Kimi-K3. |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 183 | 0 | GGUF version of the new DeepSeek release, freshly added. |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 106 | 599 | Experimental 2-bit weight quantization of Qwen3.6 MoE — pushing the limits of compression. |
| [Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,124 | 713K | **Breakthrough ternary (2-bit) quantization** — 27B model at extreme compression; llama.cpp compatible. |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 151 | 18.5K | NVFP4 quantization of Solar-Open2 — enterprise-ready compressed LLM for vLLM deployments. |

---

## 3. Ecosystem Signal

**Model family momentum:** Qwen (specifically the 3.5/3.6 line) is the clear winner this week — six of the top 30 entries are Qwen-based fine-tunes or MoE variants, with the uncensored HauhauCS release alone hitting 1.8M downloads. Moonshot's Kimi-K3 has just entered the scene and already commands the highest like count, signaling strong anticipation for multimodal models in the Asian market alongside Baidu's OCR offering. DeepSeek's V4-Flash series maintains steady dominance in text-only LLM adoption.

**Open-weight vs. proprietary:** The ecosystem is decisively open-weight. Even traditionally closed players (Microsoft, Baidu, Moonshot) are releasing foundation models openly. The presence of community fine-tunes like DavidAU and HauhauCS further demonstrates that the open ecosystem is maturing into a multi-layer value chain — base models, quantization tooling (Unsloth), and community creativity.

**Quantization trends:** Extreme compression is accelerating. Ternary-Bonsai-27B (prism-ml) proves that 2-bit ternary quantization is viable for 27B models, and nota-ai's NVFP4 shows enterprise-grade compressed formats are becoming standard. GGUF remains the dominant local format, with Unsloth acting as the primary quantization bridge for flagship models like Kimi-K3 and DeepSeek-V4.

**Efficiency push:** CPU-first TTS (Inflect), bit-level ASR (VibeVoice-BitNet), and compact MoE models (XYZ-Aquila) signal a strong pull toward edge and on-device AI — not just cloud-scale deployment.

---

## 4. Worth Exploring

**1. [Kimi-K3 (Moonshot AI)](https://huggingface.co/moonshotai/Kimi-K3)** — This is the highest-liked model of the week by a wide margin. It's a multimodal model with feature-extraction and compressed-tensor support, making it unusually adaptable for downstream tasks (RAG, vision pipelines, embedding). With Unsloth GGUF already available, it's immediately testable on local hardware. Worth studying for its architecture choices and the ecosystem hype around it.

**2. [Ternary-Bonsai-27B-gguf (prism-ml)](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — This is the most technically interesting release. At 2-bit ternary precision with 712K downloads, it demonstrates that ultra-compressed LLMs can be both practical and popular. If you're researching quantization limits, edge deployment, or efficiency-vs-quality trade-offs, this is the model to examine.

**3. [Unlimited-OCR (Baidu)](https://huggingface.co/baidu/Unlimited-OCR)** — With 2.5M downloads and 3.6K likes, this is the most-proven production utility model in the entire list. OCR is a backbone for document intelligence, RAG pipelines, and enterprise automation. If you're building any document processing or retrieval pipeline, this model deserves immediate evaluation.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*