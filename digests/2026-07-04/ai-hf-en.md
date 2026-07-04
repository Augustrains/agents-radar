# Hugging Face Trending Models Digest 2026-07-04

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-04 01:30 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-04**.

---

### 1. Today’s Highlights

This week’s trending models are dominated by the rapid expansion of the **Qwen3.5/3.6 ecosystem**, with dozens of fine-tunes and quantized variants flooding the hub, notably from **deepreinforce-ai** (Ornith series) and **empero-ai** (Qwythos). **NVIDIA** is pushing inference-optimized models with its new **NVFP4** quantized formats on Qwen3.6 and GLM-5.2, signaling a shift toward hardware-aware model compression. Meanwhile, **Google’s Gemma 4** family has inspired a wave of agentic and coding-focused GGUF fine-tunes, led by **yuxinlu1**, and **Baidu’s Unlimited-OCR** continues to see massive adoption for general-purpose document understanding. The emergence of **Uncensored + Vision MoE models** (like the 3M-download HauhauCS variant) highlights strong community demand for unrestricted multimodal reasoning.

---

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** – [Link](https://huggingface.co/zai-org/GLM-5.2)  
  Author: zai-org | Likes: 3,343 | Downloads: 191,462  
  A powerful MoE conversational model from the GLM lineage, trending for its strong reasoning and top-tier community engagement this week.

- **deepseek-ai/DeepSeek-V4-Pro-DSpark** – [Link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)  
  Author: deepseek-ai | Likes: 343 | Downloads: 9,388  
  The latest flagship from DeepSeek (V4, with DSpark optimization), gaining traction for its state-of-the-art multi-turn reasoning performance.

- **deepseek-ai/DeepSeek-V4-Flash-DSpark** – [Link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)  
  Author: deepseek-ai | Likes: 142 | Downloads: 32,675  
  A faster, lighter sibling of the V4 Pro, optimized for speed/cost trade-offs in production deployments.

- **LiquidAI/LFM2.5-230M** – [Link](https://huggingface.co/LiquidAI/LFM2.5-230M)  
  Author: LiquidAI | Likes: 197 | Downloads: 29,645  
  A compact 230M Liquid Foundation Model, trending as a strong small-footprint baseline for resource-constrained LLM applications.

---

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **baidu/Unlimited-OCR** – [Link](https://huggingface.co/baidu/Unlimited-OCR)  
  Author: baidu | Likes: 1,692 | Downloads: 885,040  
  A general-purpose OCR model from Baidu that handles unlimited-length documents, trending due to high accuracy and broad utility in enterprise pipelines.

- **nvidia/LocateAnything-3B** – [Link](https://huggingface.co/nvidia/LocateAnything-3B)  
  Author: nvidia | Likes: 2,589 | Downloads: 1,108,586  
  A 3B image-text-to-text model for object localization and understanding, trending as NVIDIA’s lightweight answer to general-purpose visual grounding.

- **krea/Krea-2-Turbo** – [Link](https://huggingface.co/krea/Krea-2-Turbo)  
  Author: krea | Likes: 480 | Downloads: 84,006  
  A turbo-charged version of Krea-2 for text-to-image generation, favored for fast iteration in creative workflows.

- **fal/LTX-2.3-3DREAL-LoRA** – [Link](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)  
  Author: fal | Likes: 150 | Downloads: 0  
  A LoRA adapter for the LTX-2.3 video model that adds realistic 3D rendering capabilities, interesting for animation and VFX pipelines.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** – [Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)  
  Author: HauhauCS | Likes: 2,432 | Downloads: 3,029,679  
  An uncensored, aggressive-style MoE vision-language model based on Qwen3.6, trending hugely for its unrestricted output and strong multimodal reasoning.

---

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** – [Link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)  
  Author: yuxinlu1 | Likes: 2,585 | Downloads: 628,225  
  A specialized Gemma 4 fine-tune for coding and reasoning, trending for its excellent code generation and strong terminal agent support.

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** – [Link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)  
  Author: yuxinlu1 | Likes: 992 | Downloads: 329,391  
  An agentic variant of the above, optimized for autonomous tool use and multi-step coding tasks.

- **google/tabfm-1.0.0-pytorch** – [Link](https://huggingface.co/google/tabfm-1.0.0-pytorch)  
  Author: google | Likes: 151 | Downloads: 450  
  Google’s TabFM foundation model for tabular data (classification/regression/zero-shot), a fresh entry into the tabular AI space.

- **BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6** – [Link](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)  
  Author: BugTraceAI | Likes: 125 | Downloads: 11,444  
  A cybersecurity-focused 27B model for offensive security analysis and vulnerability detection, quantized to Q6 for efficient local deployment.

---

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** – [Link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)  
  Author: empero-ai | Likes: 1,371 | Downloads: 1,366,360  
  A highly popular GGUF quant of a 9B model fine-tuned with synthetic Mythos data, trending for its balance of small size and strong reasoning via llama.cpp.

- **deepreinforce-ai/Ornith-1.0-35B-GGUF** – [Link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)  
  Author: deepreinforce-ai | Likes: 684 | Downloads: 322,780  
  A GGUF quantized version of the 35B Ornith MoE model, widely downloaded for deployment in local agents and edge use cases.

- **unsloth/Qwen3.6-27B-MTP-GGUF** – [Link](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)  
  Author: unsloth | Likes: 938 | Downloads: 1,774,298  
  Unsloth’s GGUF quantization of the Qwen3.6-27B model with Multi-Token Prediction, trending as the go-to efficient 27B for both text and vision tasks.

- **huihui-ai/Huihui-GLM-5.2-abliterated-GGUF** – [Link](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)  
  Author: huihui-ai | Likes: 144 | Downloads: 3,683  
  An “abliterated” (safety-removed) GGUF of GLM-5.2, appealing to the uncensored open-weight community.

- **Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF** – [Link](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)  
  Author: Jackrong | Likes: 122 | Downloads: 44,807  
  A Qwen3.6-based MoE coder model, quantized to GGUF for low-RAM local code generation with Multi-Token Prediction.

---

### 3. Ecosystem Signal

The **Qwen3.5/3.6 family** has become the dominant backbone for the open-weight community this cycle, powering nearly half of the trending models via fine-tunes, MoE architectures, and quantized variants. **NVIDIA’s NVFP4** format is gaining traction as a hardware-aware quantization scheme that reduces memory without sacrificing speed, likely signalling a broader shift toward GPU-optimized model footprints. **DeepSeek V4** is making a strong entry with both Pro and Flash variants, competing directly with Qwen and GLM at the frontier. The **Gemma-4-based agentic coders** (from yuxinlu1) represent a growing trend of specialized, tool-use-oriented LLMs — moving beyond chat into autonomous agent behavior. Meanwhile, the surge of **uncensored GGUF models** (HauhauCS, huihui-ai) indicates persistent community demand for unrestricted fine-tunes, even as safety-aligned releases dominate from major labs. **Baidu** and **NVIDIA** are the most active corporate contributors outside of the usual suspects, while **deepreinforce-ai** stands out as the top independent fine-tuning studio this week.

---

### 4. Worth Exploring

1. **nvidia/LocateAnything-3B** ([Link](https://huggingface.co/nvidia/LocateAnything-3B))  
   *Why:* At only 3B parameters, this model delivers impressive visual grounding and localization capabilities — perfect for studying how small multimodal models can replace larger, slower alternatives in vision pipelines.

2. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([Link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
   *Why:* With over 3M downloads and a design that blends uncensored output, MoE sparsity, and vision-language reasoning, this is a fascinating case study in community-driven model appetite and how far one can push a Qwen backbone.

3. **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([Link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))  
   *Why:* This fine-tune demonstrates the potential of Gemma-4 for specialized agentic coding tasks, and its high like-to-download ratio suggests strong real-world usability for developers who need a reliable local coder.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*