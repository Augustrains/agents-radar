# Hugging Face Trending Models Digest 2026-07-01

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-01 02:07 UTC

---

# 🤗 Hugging Face Trending Models Digest — July 1, 2026

## 1. Today's Highlights

This week's trending models reveal a strong shift toward **Mixture-of-Experts (MoE) architectures**, with GLM-5.2, Qwen3.6-35B-A3B, and Ornith-1.0-397B all gaining significant traction. **NVIDIA's NVFP4 quantization format** appears prominently across multiple models (Qwen3.6-35B-A3B-NVFP4 alone hit 5.4M downloads), signaling a new standard for efficient deployment. The **Ornith-1.0 family** from deepreinforce-ai (9B, 35B, and 397B variants) marks a notable emergence of a new open-weight MoE series, while **Krea-2** continues to dominate text-to-image diffusion. Community quantization efforts remain vibrant, with GGUF variants of GLM-5.2, Gemma-4-12B, and Qwen-AgentWorld showing high engagement.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,497 likes | 429K downloads  
  An image-text-to-text model for unlimited OCR tasks, trending due to Baidu's first major open-weight release and practical utility in document processing.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3,061 likes | 142K downloads  
  A powerful MoE conversational LLM with DSA architecture, the week's most-liked model, reflecting strong interest in efficient sparse attention mechanisms.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 550 likes | 157K downloads  
  A GGUF-quantized 35B MoE model from the emerging Ornith family, trending for its strong performance-to-size ratio and MIT license.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 251 likes | 6.9K downloads  
  Latest DeepSeek flagship with DSpark optimization, drawing attention as a cutting-edge research model with an accompanying arXiv paper.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | 169 likes | 17.8K downloads  
  A small but capable 230M parameter model from Liquid AI's LFM2 series, trending for its efficiency and suitability for edge deployment.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 421 likes | 45.6K downloads  
  A distilled text-to-image diffusion model built on Krea-2-Raw, trending for its speed improvements while maintaining high-quality generation.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,524 likes | 800K downloads  
  A 3B image-text-to-text model for object localization and feature extraction, highly popular for its versatility in visual grounding tasks.

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — fal | 128 likes | 0 downloads  
  A LoRA adapter for LTX-2.3 enabling 3D-realistic video generation from images, trending as a cutting-edge image-to-video tool.

- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — krea | 258 likes | 32K downloads  
  The base model for the Krea-2 image generation ecosystem, trending as the foundation for Turbo and community LoRAs.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,531 likes | 575K downloads  
  A GGUF-quantized Gemma-4-12B fine-tune specialized for coding and reasoning, among the week's most downloaded models.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 890 likes | 257K downloads  
  An agentic coding variant of Gemma-4-12B optimized for terminal and tool-use workflows.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — Chunjiang-Intelligence | 134 likes | 1.5K downloads  
  A DeepSeek-V4 fine-tune focused on cybersecurity applications, trending for specialized safety alignment.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 1,057 likes | 970K downloads  
  A GGUF-quantized Qwen3.5-based reasoning model fine-tuned on Claude Mythos data, popular for its narrative and creative reasoning capabilities.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 484 likes | 180K downloads  
  Unsloth's GGUF conversion of GLM-5.2, providing accessible quantization for the popular MoE architecture.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,363 likes | 3M+ downloads  
  An uncensored, aggressive MoE variant of Qwen3.6-35B-A3B, trending massively for its unfiltered output and high download count.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia | 389 likes | 5.4M downloads  
  NVIDIA's NVFP4-quantized Qwen3.6 MoE model, the week's most downloaded model, reflecting demand for efficient deployment of large MoE models.

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** — nvidia | 183 likes | 104K downloads  
  NVIDIA's NVFP4 quantized version of GLM-5.2, part of the broader push for hardware-optimized model formats.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — huihui-ai | 101 likes | 65 downloads  
  An "abliterated" (safety-filter removed) GGUF variant of GLM-5.2, niche but notable for the abliteration trend.

## 3. Ecosystem Signal

### MoE Takes Center Stage

This week's trends are dominated by **Mixture-of-Experts architectures**. GLM-5.2, Qwen3.6-35B-A3B, and the new **Ornith-1.0** family (spanning 9B to 397B parameters) all leverage MoE to achieve strong performance with reduced compute. The emergence of Ornith—a fully open-weight MoE series under MIT license—signals growing competition to established families like DeepSeek and Qwen.

### NVIDIA's NVFP4 Format Gains Critical Mass

The volume of downloads for NVIDIA's NVFP4 models (5.4M for Qwen3.6-35B-A3B-NVFP4 alone) suggests this quantization format is becoming a **de facto standard** for production deployment on NVIDIA hardware. The pairing of MoE architectures with efficient quantization is lowering the barrier for running large models in resource-constrained environments.

### Community Fine-tuning Remains Vibrant

Uncensored/abliterated variants (HauhauCS, huihui-ai) continue to attract large followings, while specialized fine-tunes for coding (Gemma-4-12B coder variants) and cybersecurity (DeepSeek-v4-Fable) show deepening vertical specialization. The GGUF ecosystem remains the primary format for community distribution, with Unsloth playing a key role in enabling access.

### Open-Weight Momentum

Several major releases this week (Unlimited-OCR from Baidu, Ornith from deepreinforce-ai) are **fully open-weight**, reinforcing the trend toward transparency and community-driven development. The absence of any proprietary-only models in the top 30 suggests open models are winning on community engagement.

## 4. Worth Exploring

1. **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — At 397B parameters with MIT license, this represents one of the largest fully open MoE models available. Worth studying for its architecture scalability and potential as a foundation for fine-tuning.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 800K downloads and 2.5K likes, this versatile vision-language model is a must-try for anyone working on object localization, visual grounding, or image feature extraction. Small enough to run locally, powerful enough for production.

3. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — A standout coding model with 2.5K+ likes and 575K downloads. The "fable5-composer2.5" fine-tuning recipe appears to deliver exceptional code generation and reasoning capabilities, making it a strong candidate for developer tooling.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*