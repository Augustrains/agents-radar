# Hugging Face Trending Models Digest 2026-06-24

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-24 01:58 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-06-24**.

---

## 1. Today's Highlights

The ecosystem is dominated by major releases from Chinese labs and Google, with **DeepSeek-V4-Pro** (5,030 likes) and **GLM-5.2** (2,198 likes) leading the LLM charge. Multimodal models are surging, particularly **NVIDIA's LocateAnything-3B** (2,317 likes) for visual grounding and Google's **DiffusionGemma-26B-A4B-it** (1,055 likes) for efficient image understanding. The community is highly active in quantization, with **GGUF variants** of virtually every major model—from Qwen3.6 to Gemma-4—seeing massive download volumes, signaling strong demand for local and edge deployment. Notably, **Boogu-Image** (0.1-Edit) and its Comfy-Org port suggest growing interest in lightweight image editing tools.

---

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **DeepSeek-V4-Pro** by [deepseek-ai](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) — 5,030 likes, 2.2M downloads  
  The flagship conversational LLM from DeepSeek; trending due to its mix of massive scale, open-weight release, and strong reasoning benchmarks.

- **zai-org/GLM-5.2** by [zai-org](https://huggingface.co/zai-org/GLM-5.2) — 2,198 likes, 40k downloads  
  Zhipu AI's latest MoE model with DSA architecture; trending as a major Chinese-language frontier model competing with DeepSeek.

- **microsoft/FastContext-1.0-4B-SFT** by [microsoft](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT) — 322 likes, 4.4k downloads  
  A 4B model optimized for extremely long-context retrieval-augmented generation (RAG); notable for its efficient "Explorer SubAgent" design.

- **poolside/Laguna-M.1** by [poolside](https://huggingface.co/poolside/Laguna-M.1) — 93 likes, 2.8k downloads  
  A production-focused LLM designed for software engineering teams; trending in the developer tooling space.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **nvidia/LocateAnything-3B** by [nvidia](https://huggingface.co/nvidia/LocateAnything-3B) — 2,317 likes, 274k downloads  
  A 3B model for open-vocabulary visual grounding and object localization; trending for its accuracy and lightweight architecture.

- **MiniMaxAI/MiniMax-M3** by [MiniMaxAI](https://huggingface.co/MiniMaxAI/MiniMax-M3) — 1,221 likes, 131k downloads  
  Multimodal VL model (image-text-to-text) with strong reasoning; trending due to MiniMax's fast-growing ecosystem.

- **google/diffusiongemma-26B-A4B-it** by [google](https://huggingface.co/google/diffusiongemma-26B-A4B-it) — 1,055 likes, 949k downloads  
  Google's MoE diffusion transformer for image understanding; 26B total / 4B active parameters; highly downloaded for its efficiency.

- **google/gemma-4-12B-it** by [google](https://huggingface.co/google/gemma-4-12B-it) — 1,156 likes, 1.99M downloads  
  The "any-to-any" unified model from Google (text, image, audio); massive downloads driven by versatility and integration with Gemma ecosystem.

- **ostris/ideogram_4_turbotime_lora** by [ostris](https://huggingface.co/ostris/ideogram_4_turbotime_lora) — 111 likes, 3.7k downloads  
  A LoRA adapter for Ideogram 4 that enables faster inference; popular among the diffusion model community.

- **Boogu/Boogu-Image-0.1-Edit** by [Boogu](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit) — 113 likes, 592 downloads  
  An early-stage image editing diffusion model; gaining traction for its Apache-2.0 license and simple LoRA-based edits.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **moonshotai/Kimi-K2.7-Code** by [moonshotai](https://huggingface.co/moonshotai/Kimi-K2.7-Code) — 976 likes, 448k downloads  
  A compressed, code-specialized variant of the Kimi-K2.5 model; trending for its strong coding benchmarks and efficient architecture.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** by [nvidia](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) — 657 likes, 41k downloads  
  A streaming ASR model (600M params) with cache-aware inference; trending for real-time speech recognition applications.

- **WeiboAI/VibeThinker-3B** by [WeiboAI](https://huggingface.co/WeiboAI/VibeThinker-3B) — 665 likes, 41k downloads  
  A compact 3B math reasoning model based on Qwen2; popular for its surprisingly strong performance on math benchmarks.

- **baidu/Unlimited-OCR** by [baidu](https://huggingface.co/baidu/Unlimited-OCR) — 481 likes, 8.4k downloads  
  A high-performance OCR model from Baidu; trending for accuracy across diverse document types and languages.

- **LiquidAI/LFM2.5-Embedding-350M** by [LiquidAI](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M) — 115 likes, 10k downloads  
  Sentence embedding model (350M params) using Liquid's LFM2.5 architecture; notable for high retrieval quality.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** by [yuxinlu1](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) — 2,241 likes, 456k downloads  
  A GGUF quantization of a Gemma-4-12B coder fine-tune with "fable5" composer; the top-quantized model by likes this week.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** by [HauhauCS](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) — 2,158 likes, 3.96M downloads  
  An uncensored, aggressive-roleplay fine-tune of Qwen3.6 MoE; the highest download count of any model today, driven by the uncensored community.

- **zai-org/GLM-5.2-FP8** by [zai-org](https://huggingface.co/zai-org/GLM-5.2-FP8) — 149 likes, 395k downloads  
  Official FP8 quantization of GLM-5.2; popular for enabling efficient inference on consumer hardware.

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** by [yuxinlu1](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF) — 449 likes, 96k downloads  
  An agentic (tool-use) fine-tune of Gemma-4-12B in GGUF format; trending for terminal/agent workflows.

- **unsloth/GLM-5.2-GGUF** by [unsloth](https://huggingface.co/unsloth/GLM-5.2-GGUF) — 303 likes, 56k downloads  
  Unsloth's highly optimized GGUF conversion of GLM-5.2; standard choice for running GLM-5.2 locally.

- **huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated** by [huihui-ai](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated) — 112 likes, 3.3k downloads  
  "Abliterated" version of the Gemma-4 coder (safety filters removed); popular in the uncensored fine-tuning niche.

- **bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF** by [bytkim](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF) — 112 likes, 66k downloads  
  A position-interpolation (PI) fine-tune of Qwen3.6 for longer context, quantized to GGUF.

---

## 3. Ecosystem Signal

The current landscape is defined by **three dominant model families**: DeepSeek's V4 series, Zhipu's GLM-5.2 MoE, and Google's Gemma-4 ecosystem. DeepSeek-V4-Pro holds the top spot by likes, but GLM-5.2 and its quantizations (FP8, GGUF) are driving the densest fine-tuning activity. **Google's Gemma-4 family is the most "forked" family**—nearly every major GGUF quantizer and fine-tuner (yuxinlu1, huihui-ai, unsloth) has released at least one variant, indicating a vibrant ecosystem.

The open-weight trend is strong: all top models are fully open-weight, with no proprietary APIs dominating. The community is heavily invested in **quantization (GGUF) and MoE architectures**—many models use Mixture-of-Experts for efficiency. The rapid growth of "uncensored" and "abliterated" fine-tunes suggests a persistent demand for models without alignment guardrails, particularly for roleplay and creative writing.

Multimodal models are moving from research demos to production: NVIDIA's LocateAnything-3B, Google's DiffusionGemma, and MiniMax-M3 are all seeing heavy downloads. The **"any-to-any" modality trend** (gemma-4-it) is gaining traction as the next frontier.

---

## 4. Worth Exploring

1. **nvidia/LocateAnything-3B** — The standout multimodal model this week. If you need visual grounding or object localization without heavy compute, this is the best balance of accuracy and size.

2. **zai-org/GLM-5.2-FP8** — For anyone wanting to run a frontier Chinese LLM efficiently. The official FP8 is production-ready and sees consistent download growth.

3. **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** — If you're building agentic systems (tool use, terminal commands), this GGUF quantized fine-tune of Gemma-4 is worth studying for its performance on real-world agent tasks.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*