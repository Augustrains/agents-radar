# Hugging Face Trending Models Digest 2026-06-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-21 02:16 UTC

---

# Hugging Face Trending Models Digest — 2026-06-21

## Today's Highlights

DeepSeek-V4-Pro dominates the week with nearly 5,000 likes and 2.8M downloads, signaling the community's strong appetite for next-generation open-weight reasoning models. Google's DiffusionGemma-26B-A4B-it and Gemma-4-12B-it demonstrate the growing convergence of language and multimodal capabilities in single model architectures. The Qwen3.6 ecosystem continues to expand rapidly, with multiple fine-tunes and quantizations appearing across the leaderboard. Community-vetted GGUF variants from makers like yuxinlu1 and HauhauCS remain highly popular for local deployment, while NVIDIA's LocateAnything-3B highlights rising interest in specialized vision-language tasks like spatial grounding.

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **DeepSeek-V4-Pro** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))  
  Author: deepseek-ai | Likes: 4,985 | Downloads: 2,797,050  
  The most liked model this week, a flagship open-weight conversational LLM from DeepSeek, trending for its strong reasoning performance and active community adoption.

- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2))  
  Author: zai-org | Likes: 1,692 | Downloads: 19,683  
  A new MoE-DSA architecture conversational model from Zhipu AI, gaining traction for its efficient sparse activation design and strong Chinese/English capabilities.

- **microsoft/FastContext-1.0-4B-SFT** ([link](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT))  
  Author: microsoft | Likes: 244 | Downloads: 1,998  
  A 4B parameter model optimized for long-context processing with Explorer SubAgent support, trending for its practical efficiency in retrieval-augmented workflows.

- **nex-agi/Nex-N2-Pro** ([link](https://huggingface.co/nex-agi/Nex-N2-Pro))  
  Author: nex-agi | Likes: 340 | Downloads: 7,724  
  A Qwen3.5-MoE-based vision-language model, trending for its blend of conversational and image understanding capabilities in a compact MoE design.

- **CohereLabs/North-Mini-Code-1.0** ([link](https://huggingface.co/CohereLabs/North-Mini-Code-1.0))  
  Author: CohereLabs | Likes: 468 | Downloads: 18,783  
  A 1.0B-parameter code-focused MoE model from Cohere, gaining attention for efficient code generation in resource-constrained settings.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **google/diffusiongemma-26B-A4B-it** ([link](https://huggingface.co/google/diffusiongemma-26B-A4B-it))  
  Author: google | Likes: 1,022 | Downloads: 673,464  
  A 26B diffusion-transformer model with 4B active parameters, trending for its powerful image-text-to-text generation and conversational multimodality.

- **MiniMaxAI/MiniMax-M3** ([link](https://huggingface.co/MiniMaxAI/MiniMax-M3))  
  Author: MiniMaxAI | Likes: 1,160 | Downloads: 85,771  
  A next-generation multimodal vision-language model from MiniMax, popular for balanced performance across image understanding and generation tasks.

- **google/gemma-4-12B-it** ([link](https://huggingface.co/google/gemma-4-12B-it))  
  Author: google | Likes: 1,107 | Downloads: 1,696,240  
  The first "any-to-any" model from Google's Gemma 4 family, trending for its unified architecture handling text, images, and audio inputs natively.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))  
  Author: nvidia | Likes: 587 | Downloads: 21,426  
  A cache-aware streaming ASR model optimized for low-latency speech recognition, gaining interest for deployment in real-time voice applications.

- **bosonai/higgs-audio-v3-tts-4b** ([link](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b))  
  Author: bosonai | Likes: 499 | Downloads: 72,225  
  A 4B parameter text-to-speech model based on multimodal Qwen3, trending for high-quality speech synthesis with strong prosody and voice cloning potential.

- **ostris/ideogram_4_turbotime_lora** ([link](https://huggingface.co/ostris/ideogram_4_turbotime_lora))  
  Author: ostris | Likes: 82 | Downloads: 1,679  
  A LoRA adapter for Ideogram 4 FP8, enabling rapid text-to-image generation with style control, popular among creative AI artists.

- **zai-org/SCAIL-2** ([link](https://huggingface.co/zai-org/SCAIL-2))  
  Author: zai-org | Likes: 241 | Downloads: 0  
  A pose-driven character animation diffusion model for image-to-video generation, trending for its high-quality motion synthesis capabilities.

- **owensong/Inflect-Nano-v1** ([link](https://huggingface.co/owensong/Inflect-Nano-v1))  
  Author: owensong | Likes: 142 | Downloads: 0  
  An ultra-small text-to-speech model, gaining attention for its efficiency in on-device deployment despite minimal parameter count.

- **datalab-to/lift** ([link](https://huggingface.co/datalab-to/lift))  
  Author: datalab-to | Likes: 87 | Downloads: 0  
  A PDF-focused image-text-to-text model based on Qwen3.5, trending for its document understanding and extraction capabilities.

- **LiquidAI/LFM2.5-Embedding-350M** ([link](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M))  
  Author: LiquidAI | Likes: 81 | Downloads: 6,128  
  A 350M sentence-embedding model from the LFM2.5 family, gaining interest for efficient text representation in retrieval and clustering tasks.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))  
  Author: yuxinlu1 | Likes: 1,988 | Downloads: 312,332  
  A GGUF-quantized Gemma 4 coding variant with Composer tooling, trending as the go-to local code assistant for developers.

- **moonshotai/Kimi-K2.7-Code** ([link](https://huggingface.co/moonshotai/Kimi-K2.7-Code))  
  Author: moonshotai | Likes: 930 | Downloads: 317,963  
  A vision-enabled code model from Kimi with compressed tensor support, trending for its ability to process code in screenshots and documents.

- **WeiboAI/VibeThinker-3B** ([link](https://huggingface.co/WeiboAI/VibeThinker-3B))  
  Author: WeiboAI | Likes: 511 | Downloads: 16,270  
  A 3B math-reasoning model optimized for chain-of-thought solving, popular for its strong mathematical capability despite small size.

- **nvidia/LocateAnything-3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B))  
  Author: nvidia | Likes: 2,216 | Downloads: 235,606  
  A 3B vision-language model specialized in object localization and spatial grounding, trending for its precision in "find anything" visual tasks.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
  Author: HauhauCS | Likes: 2,042 | Downloads: 3,812,636  
  The week's most-downloaded model, an uncensored MoE vision-language fine-tune of Qwen3.6 in GGUF format, extremely popular for local uncensored role-play and creative use.

- **DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF** ([link](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF))  
  Author: DavidAU | Likes: 411 | Downloads: 587,521  
  A massive community fine-tune combining Qwen3.6 with uncensored and code-optimized training, popular for its aggressive creative and programming capabilities.

- **unsloth/GLM-5.2-GGUF** ([link](https://huggingface.co/unsloth/GLM-5.2-GGUF))  
  Author: unsloth | Likes: 205 | Downloads: 22,586  
  Unsloth's GGUF conversion of GLM-5.2, enabling efficient local deployment of Zhipu AI's latest MoE model.

- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF))  
  Author: yuxinlu1 | Likes: 187 | Downloads: 6,307  
  An agentic-focused GGUF variant of Gemma 4, optimized for terminal-based agent workflows and tool calling.

- **Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF** ([link](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF))  
  Author: Jackrong | Likes: 269 | Downloads: 168,502  
  A 27B vision-code hybrid model in GGUF format, trending for strong performance in both programming and image understanding tasks.

- **Mia-AiLab/Qwable-3.6-27b** ([link](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b))  
  Author: Mia-AiLab | Likes: 112 | Downloads: 17,311  
  A GGUF version of the Qwable Qwen3.6 model, popular for general-purpose local inference.

- **bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF** ([link](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF))  
  Author: bytkim | Likes: 97 | Downloads: 20,465  
  A pi-tuned GGUF of Qwen3.6 with MTP support, optimized for enhanced reasoning in local inference scenarios.

- **zai-org/GLM-5.2-FP8** ([link](https://huggingface.co/zai-org/GLM-5.2-FP8))  
  Author: zai-org | Likes: 115 | Downloads: 138,174  
  The official FP8 quantization of GLM-5.2, enabling memory-efficient deployment without significant quality loss.

- **unsloth/Kimi-K2.7-Code-GGUF** ([link](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF))  
  Author: unsloth | Likes: 146 | Downloads: 37,260  
  Unsloth's GGUF conversion of Kimi K2.7-Code, making Kimi's vision-code model accessible for local CPU inference.

- **prefeitura-rio/Rio-3.5-Open-397B** ([link](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B))  
  Author: prefeitura-rio | Likes: 327 | Downloads: 190,694  
  A massive 397B MoE vision-language model released by Rio's city government, trending as an open-weight alternative to proprietary multimodal systems.

- **lordx64/Qwable-v1** ([link](https://huggingface.co/lordx64/Qwable-v1))  
  Author: lordx64 | Likes: 138 | Downloads: 2,769  
  A Qwen3.5-MoE-based vision-language community model, gaining interest for its multi-modal conversational capabilities.

## Ecosystem Signal

The Qwen3.6 family has become the most active base model ecosystem this week, with at least seven fine-tunes and quantizations appearing (HauhauCS, DavidAU, Jackrong, Mia-AiLab, bytkim, and others). This mirrors the rapid community adoption pattern previously seen with Llama and Gemma — a strong base model quickly becomes the foundation for specialized variants.

MoE (Mixture of Experts) architectures are now standard across top models: DeepSeek-V4-Pro, GLM-5.2, DiffusionGemma-26B-A4B-it, Rio-3.5-Open-397B, and nearly all Qwen3.x derivatives employ MoE designs. This reflects the industry consensus that sparse activation is essential for scaling performance while keeping inference costs manageable.

Uncensored fine-tunes remain a major driver of download volume. The HauhauCS Qwen3.6-35B-A3B-Uncensored model alone accounts for over 3.8M downloads this week, demonstrating sustained demand for models without safety alignment guardrails, particularly for creative writing, role-play, and uncensored reasoning.

Google's Gemma 4 family and NVIDIA's LocateAnything-3B represent a shift toward "any-to-any" and specialized vision-language models, respectively, indicating that the ecosystem is maturing beyond pure text LLMs into truly multimodal workflows.

GGUF quantization by trusted community builders (unsloth, yuxinlu1) continues to be the primary vehicle for local deployment, with 9 of the 30 trending models being GGUF variants. The community trusts these optimized formats for running large models on consumer hardware.

## Worth Exploring

1. **DeepSeek-V4-Pro** — Essential to study as the most-liked model of the week. Its combination of strong reasoning, conversational fluency, and open-weight availability makes it a benchmark for the current state of open LLMs. Download and compare its performance against GPT-4 class models on coding and math tasks.

2. **google/diffusiongemma-26B-A4B-it** — The diffusion-transformer architecture blending language and image generation is a notable architectural innovation. With 4B active parameters, it represents the future of efficient multimodal models. Worth testing for image captioning, visual QA, and generation tasks to understand the diffusion-LLM convergence.

3. **nvidia/LocateAnything-3B** — With over 2,200 likes and strong spatial grounding capabilities, this model exemplifies the trend toward specialized, task-specific vision models. It's worth exploring for applications in robotics, AR/VR, and automated visual inspection where precise object localization is critical.

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*