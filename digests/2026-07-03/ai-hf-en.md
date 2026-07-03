# Hugging Face Trending Models Digest 2026-07-03

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-03 01:43 UTC

---

# Hugging Face Trending Models Digest — 2026-07-03

## Today's Highlights

This week's trending models reveal a strong surge in MoE (Mixture-of-Experts) architecture adoption, with multiple Qwen3.5/Gwen3.6 and GLM-5.2 variants dominating the text-generation category. Nvidia's **LocateAnything-3B** continues its explosive growth with over 1M downloads and 2,573 likes, cementing visual grounding as a key trend. The community is heavily focused on quantized GGUF releases—particularly **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** and the popular **HauhauCS/Qwen3.6-35B-A3B-Uncensored** variant—indicating strong demand for efficient, locally-deployable reasoning models. The emergence of **DeepSeek-V4-Pro-DSpark** and **DeepSeek-V4-Flash-DSpark** signals ongoing competition in the frontier LLM space, while **krea/Krea-2-Turbo** and companion LoRAs point to a maturing text-to-image ecosystem.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** — 3,254 likes, 176k downloads  
  A 5.2-generation MoE language model by Zhipu AI, trending due to its strong conversational and reasoning performance combined with a novel MoE-DSA architecture.

- **nvidia/GLM-5.2-NVFP4** — 207 likes, 159k downloads  
  Nvidia's FP4-optimized quantized variant of GLM-5.2, drawing interest for high-throughput inference on Nvidia hardware.

- **deepreinforce-ai/Ornith-1.0-35B** — 312 likes, 185k downloads  
  A 35B MoE model built on Qwen3.5 architecture, gaining traction for its strong image-text-to-text capabilities and MIT licensing.

- **deepreinforce-ai/Ornith-1.0-397B** — 196 likes, 7.3k downloads  
  The largest Ornith variant at 397B parameters, showcasing MoE scaling with Qwen3.5 backbone for multimodal generation.

- **deepseek-ai/DeepSeek-V4-Pro-DSpark** — 303 likes, 8.1k downloads  
  DeepSeek's latest V4 iteration with DSpark optimization, accompanied by an arXiv paper (2606.19348) signaling frontier research.

- **deepseek-ai/DeepSeek-V4-Flash-DSpark** — 128 likes, 23.9k downloads  
  A faster, distilled variant of DeepSeek V4 optimized for inference speed, targeted at production deployments.

- **InternScience/Agents-A1** — 181 likes, 1.5k downloads  
  An agent-focused MoE model based on Qwen3.5, designed for tool-use and autonomous task completion.

- **meituan-longcat/LongCat-2.0** — 165 likes, 0 downloads  
  An evaluation-focused model release by Meituan, likely benchmarking long-context capabilities.

- **LiquidAI/LFM2.5-230M** — 192 likes, 26k downloads  
  A lightweight 230M parameter language model from Liquid AI, notable for efficiency in resource-constrained settings.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** — 2,396 likes, 3.07M downloads  
  An uncensored MoE variant of Qwen3.6-35B-A3B, extremely popular for its high-quality GGUF quantized weights and "aggressive" uncensored behavior.

- **Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF** — 117 likes, 29.5k downloads  
  A code-specialized MoE variant using multi-turn prediction (MTP) training, in GGUF format for local deployment.

- **BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6** — 121 likes, 8k downloads  
  A cybersecurity-focused 27B model with Q6 quantization, designed for offensive security tasks and vulnerability analysis.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M** — 645 likes, 124k downloads  
  A 9B model fine-tuned with Claude Mythos-style data (5M synthetic tokens), blending Qwen3.5 with creative reasoning.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** — 1,255 likes, 1.25M downloads  
  The GGUF-quantized version of Qwythos, extremely popular for local inference via llama.cpp.

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** — 2,573 likes, 614k downloads  
  A highly-rated Gemma 4 12B coder finetune using Fable5 and Composer2.5 techniques, packaged as GGUF for efficient local coding assistance.

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** — 962 likes, 314k downloads  
  An agentic variant of Gemma 4 12B with enhanced tool-use and terminal capabilities, also in GGUF format.

- **nvidia/Qwen3.6-27B-NVFP4** — 210 likes, 27k downloads  
  Nvidia's FP4-quantized Qwen3.6 27B, optimized for low-bit inference on high-end Nvidia GPUs.

- **huihui-ai/Huihui-GLM-5.2-abliterated-GGUF** — 135 likes, 2.5k downloads  
  An "abliterated" (safety-filter-removed) GGUF variant of GLM-5.2, popular in uncensored model circles.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **baidu/Unlimited-OCR** — 1,652 likes, 758k downloads  
  Baidu's comprehensive OCR model supporting unlimited text extraction from images, trending for its accuracy and broad language support.

- **krea/Krea-2-Turbo** — 462 likes, 69k downloads  
  A high-speed text-to-image Turbo model built on Krea-2-Raw, optimized for rapid image generation.

- **fal/LTX-2.3-3DREAL-LoRA** — 145 likes, 0 downloads  
  A LoRA for LTX 2.3 video models enabling realistic 3D image-to-video generation, from the fal.ai team.

- **Comfy-Org/Krea-2** — 231 likes, 10 downloads  
  Comfy-Org's integration of Krea-2 into the ComfyUI workflow ecosystem.

- **ilkerzgi/fal-Krea-2-Style-LoRAs** — 107 likes, 0 downloads  
  A collection of LoRA adapters for Krea-2 enabling style-specific text-to-image generation.

- **nvidia/LocateAnything-3B** — 2,573 likes, 1M downloads  
  Nvidia's 3B visual grounding model for object localization and segmentation, extremely trending for its zero-shot detection capabilities.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** — 2,573 likes, 614k downloads  
  The highest-liked code model this week, balancing coding accuracy with efficient GGUF quantization.

- **google/tabfm-1.0.0-pytorch** — 118 likes, 89 downloads  
  Google's TabFM foundation model for tabular data classification and regression, supporting zero-shot learning on structured data.

- **BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6** — 121 likes, 8k downloads  
  A specialized security model trained on vulnerability databases and cybersecurity corpora.

- **nationaldesignstudio/rampart** — 104 likes, 790 downloads  
  A BERT-based token classifier for PII detection, deployable via ONNX and transformers.js for browser-based privacy protection.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** — 2,396 likes, 3.07M downloads  
  The most-downloaded GGUF this week, offering a heavily uncensored Qwen3.6 MoE variant.

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** — 2,573 likes, 614k downloads  
  A highly polished Gemma 4 12B code finetune in quantized format.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** — 1,255 likes, 1.25M downloads  
  A GGUF of a creative reasoning model fine-tuned on synthetic Claude-style data.

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** — 962 likes, 314k downloads  
  Agentic GGUF variant optimized for terminal and tool-use scenarios.

- **deepreinforce-ai/Ornith-1.0-35B-GGUF** — 658 likes, 284k downloads  
  GGUF of the 35B multimodal Ornith model, enabling local deployment.

- **deepreinforce-ai/Ornith-1.0-9B-GGUF** — 397 likes, 255k downloads  
  Smaller GGUF sibling of the Ornith family, widely used for lightweight multimodal experiments.

- **huihui-ai/Huihui-GLM-5.2-abliterated-GGUF** — 135 likes, 2.5k downloads  
  GLM-5.2 abliterated GGUF for uncensored text generation.

- **Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF** — 117 likes, 29.5k downloads  
  Code-specialized Qwen3.6 GGUF with multi-turn prediction.

- **nvidia/GLM-5.2-NVFP4 & nvidia/Qwen3.6-27B-NVFP4** — 207 and 210 likes  
  Production-grade FP4 quantizations from Nvidia, enabling high-throughput inference.

- **nvidia/LocateAnything-3B** — 2,573 likes, 1M downloads  
  While not a typical fine-tune/quant, its "safetensors" tag and model optimization make it a key reference implementation for Nvidia's deployment stack.

## Ecosystem Signal

The current trending landscape reveals **three clear macro-trends** shaping the Hugging Face ecosystem:

1. **MoE (Mixture-of-Experts) has become the dominant architecture paradigm.** Qwen3.5/Gwen3.6 MoE variants (Ornith series, Qwen-AgentWorld, uncensored HauhauCS variants) and GLM-5.2 collectively represent over half of all trending text-generation models. The community is voting with likes for efficient, high-capacity models that balance parameter count with inference cost.

2. **GGUF quantization is no longer optional—it's the default distribution format.** Almost every trending LLM has a GGUF variant in the top 30, with models like **HauhauCS/Qwen3.6-35B-A3B-Uncensored** (3.07M downloads) and **yuxinlu1/gemma-4-12B-coder** (614k downloads) proving that local, accessible AI is the primary consumption pattern. The shift from "raw" weights to quantized formats reflects a maturing user base that prioritizes deployability over research experimentation.

3. **Nvidia is aggressively positioning as the infrastructure layer for open-weight models.** With three FP4 quantized releases (GLM-5.2, Qwen3.6, and the independently trending LocateAnything-3B), Nvidia is effectively creating a "quantized reference standard" that shapes how the community deploys these models. Their ModelOpt tags signal growing industry alignment around Nvidia's quantization toolchain.

Notably, the **uncensored model wave** continues strongly (HauhauCS, huihui-ai's abliterated GLM-5.2), indicating sustained demand for models without alignment guardrails—particularly in creative and role-playing use cases. Meanwhile, the **DeepSeek V4** release remains at lower traction (303 likes for Pro, 128 for Flash) compared to community MoE variants, suggesting that frontier lab releases face steeper competition from community-tuned alternatives.

## Worth Exploring

1. **nvidia/LocateAnything-3B** — With 2,573 likes and 1M+ downloads, this visual grounding model is the week's standout. Its ability to localize arbitrary objects zero-shot makes it immediately useful for robotics, UI automation, and visual inspection pipelines. Worth studying as a reference for efficient vision-language alignment.

2. **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** — At 2,573 likes and 614k downloads, this Gemma 4 finetune represents the state-of-the-art in open-weight code assistance. Its Fable5+Composer2.5 training methodology is worth examining for anyone building domain-specific code models.

3. **google/tabfm-1.0.0-pytorch** — Though smaller in traction (118 likes), this model signals Google's entry into tabular foundation models. For ML practitioners working with structured data, TabFM's zero-shot tabular classification could be transformative, offering a rare example of a pretrained model for non-text modalities.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*