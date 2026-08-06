# Hugging Face 热门模型日报 2026-08-06

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-06 01:16 UTC

---

# 🤖 Hugging Face 热门模型日报（2026-08-06）

## 📌 今日速览

今日榜单呈现几大看点：**DeepSeek-V4-Flash** 系列强势霸榜，原版与 GGUF 量化版合计斩获超 4,900 赞、下载量超 320 万，稳居文本生成赛道核心地位；**Kimi-K3** 以单周超 1 万点赞登顶全榜，作为 Moonshot AI 推出的多模态模型，其 compressed-tensors 压缩技术引发广泛关注；**GLM-5.2**（智谱）持续高热，下载量突破 220 万，验证了国产开源大模型的生态号召力；视频生成赛道由 **MiniMax-H3** 引领，官方版与 ComfyUI 适配版双线并进，多模态创作链路进一步打通。此外，Qwen3.5/3.6 系列衍生微调模型百花齐放，社区二次创作生态空前繁荣。


## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — deepseek-ai | 点赞 2,496 | 下载 433,284
  DeepSeek V4 Flash 的 0731 版本，对话能力与推理性能显著提升，自带 safetensors 权重，是当前开源 LLM 的热门之选。

- [**deepseek-ai/DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) — deepseek-ai | 点赞 2,031 | 下载 2,737,621
  DeepSeek V4 Flash 原版，凭借超大下载量稳居趋势榜，其高效推理架构与出色中文能力是社区关注核心。

- [**zai-org/GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) — zai-org | 点赞 4,849 | 下载 2,234,662
  智谱最新 GLM 系列，采用 MoE 架构（glm_moe_dsa），综合能力对标国际一线模型，社区热度持续高涨。

- [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — moonshotai | 点赞 10,125 | 下载 1,125,935
  今日全榜点赞冠军，Kimi K3 多模态大模型支持图文联合理解，compressed-tensors 压缩技术为部署效率带来显著优势。

- [**thinkingmachines/Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) — thinkingmachines | 点赞 308 | 下载 15,500
  Inkling 系列小尺寸多模态模型，主打端侧部署与轻量对话场景，适合资源受限环境。

- [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) — LiquidAI | 点赞 285 | 下载 47,393
  基于 Liquid 架构的 2.6B 轻量语言模型，在保持高性能的同时大幅降低推理成本。

- [**XYZAILab/XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) — XYZAILab | 点赞 416 | 下载 1,317
  基于 Qwen3.5 MoE 架构的 Aquila 迷你版，兼顾小型化与多模态能力，探索高效模型路径。

- [**XYZAILab/XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) — XYZAILab | 点赞 366 | 下载 1,388
  Aquila Pro 版本，强化 agentic-search 能力，面向智能体检索与复杂任务推理场景。

- [**Kwaipilot/KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) — Kwaipilot | 点赞 496 | 下载 15,381
  基于 Qwen3.5 MoE 的代码生成模型，专注编程助手场景，开发者预览版快速迭代中。

- [**deepgrove/maple-preview**](https://huggingface.co/deepgrove/maple-preview) — deepgrove | 点赞 157 | 下载 0
  Maple 预览版，MoE 架构文本生成模型，主打因果语言建模，目前处于早期发布阶段。

- [**inclusionAI/Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) — inclusionAI | 点赞 156 | 下载 25
  基于 bailing_hybrid 架构的 Flash 快速版本，面向对话场景的轻量化部署。

- [**EschaLabs/Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) — EschaLabs | 点赞 210 | 下载 2,987
  Qwen3.6 35B MoE 定制版（激活 3B），在保持性能的前提下大幅降低推理资源需求。

- [**LGAI-EXAONE/K-EXAONE-2.0-750B-A37B**](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) — LGAI-EXAONE | 点赞 129 | 下载 325
  LG 超大规模 MoE 模型，750B 总参数 / 37B 激活参数，主打韩语与多语种能力。

- [**empero-ai/Qwythos-27B-v1**](https://huggingface.co/empero-ai/Qwythos-27B-v1) — empero-ai | 点赞 145 | 下载 2,243
  基于 Qwen3.5 的 27B 多模态模型，社区微调版本，兼顾图文理解与生成。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — MiniMaxAI | 点赞 2,496 | 下载 10,841
  支持 text-to-video 与 image-to-video 的双模态生成模型，登顶视频生成赛道，diffusers 生态一键可用。

- [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) — Comfy-Org | 点赞 755 | 下载 2
  ComfyUI 官方适配版 MiniMax-H3，将视频生成无缝集成到 ComfyUI 工作流。

- [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) — baidu | 点赞 3,906 | 下载 2,703,366
  百度开源的通用 OCR 模型，支持海量场景文本识别，下载量近 300 万，应用价值极高。

- [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) — microsoft | 点赞 275 | 下载 435,784
  微软多模态理解模型，覆盖图像-文本联合推理任务，企业级应用潜力突出。

- [**Audio8/Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) — Audio8 | 点赞 274 | 下载 11,276
  Audio8 语音合成预览版，基于 ArkTTS 架构，主打自然语音生成。

- [**owensong/Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) — owensong | 点赞 417 | 下载 2,072
  轻量级本地 TTS 模型，支持 CPU 推理，面向边缘设备语音合成场景。

- [**lodestones/Kroma**](https://huggingface.co/lodestones/Kroma) — lodestones | 点赞 191 | 下载 0
  Krea2 生态的 LoRA 模型，专注于文本到图像生成，适配 ComfyUI 工作流。

### 🔧 专用模型（代码、数学、医疗、嵌入、安全等）

- [**mistralai/Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) — mistralai | 点赞 131 | 下载 166
  Mistral 推出的 3B 安全防护模型，用于内容审核与输出安全过滤，vLLM 兼容。

- [**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) — nvidia | 点赞 124 | 下载 80
  英伟达语音对话模型，11B 参数，专注于语音交互与实时对话场景。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) — DavidAU | 点赞 1,587 | 下载 1,633,405
  Qwen3.6 27B 社区微调版，GGUF 量化格式，主打"无审查"对话风格，下载量超 160 万。

- [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) — unsloth | 点赞 502 | 下载 111,678
  unsloth 出品 DeepSeek V4 Flash GGUF 量化版，显著降低部署门槛，本地推理首选。

- [**unsloth/Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) — unsloth | 点赞 316 | 下载 170,055
  Kimi K3 的 GGUF 量化版本，让多模态模型也能在消费级硬件上流畅运行。

- [**DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) — DavidAU | 点赞 282 | 下载 323,116
  Qwen3.5 9B 社区微调版，GGUF 双格式（MTP + 常规），下载量超 32 万。

- [**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) — LuffyTheFox | 点赞 385 | 下载 308,857
  Qwen3.6 35B MoE 的 Hermes V7 微调版，GGUF 量化，兼具创意与性能。

- [**realrebelai/MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) — realrebelai | 点赞 137 | 下载 40,010
  MiniMax-H3 视频生成模型的 GGUF 量化版本，针对 ComfyUI 场景优化。

- [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) — ethanfel | 点赞 283 | 下载 0
  Qwen3-VL 32B 的 ComfyUI INT8 量化版本，探索视觉模型本地部署新路径。


## 📊 生态信号

**核心观察：**
1. **DeepSeek 与智谱 GLM 领跑开源 LLM**——DeepSeek-V4-Flash 系列双版本总下载量超 317 万，GLM-5.2 超 220 万，国产开源模型已在全球社区形成压倒性影响力，开源权重策略持续获得开发者正向反馈。
2. **MoE 架构全面渗透**——GLM-5.2、Kimi-K3、LG K-EXAONE、Qwen3.5/3.6 系列微调模型均采用混合专家架构，在保持性能的同时降低推理成本，MoE 已成为 2026 年大模型的主流技术路线。
3. **GGUF 量化生态爆发**——unsloth 等团队持续为头部模型（DeepSeek、Kimi）提供 GGUF 版本；DavidAU 等社区创作者高频产出"无审查"微调 + 量化模型，下载量动辄数百万，反映出个人开发者和边缘部署场景的旺盛需求。
4. **多模态与视频生成升温**——MiniMax-H3 视频生成模型配合 ComfyUI 适配形成完整创作链路；百度 Unlimited-OCR 以近 300 万下载验证了文档智能场景的刚需价值。
5. **"无审查"微调成为社区亚文化**——Heretic / Uncensored 标签在 GGUF 模型中高频出现，与主流安全对齐形成有趣张力，也提示平台需关注内容治理与模型开源边界的平衡。


## 🧪 值得探索

1. [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — 全榜点赞第一（10,125）绝非偶然：compressed-tensors 压缩技术 + 多模态能力，代表下一代高效多模态模型的前沿方向，强烈推荐研究其压缩方法与架构设计。

2. [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — 在 280 万下载量的基础上持续迭代，说明 DeepSeek 团队以极高频率推进开源模型更新。配合 [unsloth 的 GGUF 版本](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)，可作为本地部署 LLM 的最佳实践样本。

3. [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — 视频生成赛道的黑马，双模态输入（文本/图像 → 视频）提供了极大的创作自由度，配合 [ComfyUI 适配版](https://huggingface.co/Comfy-Org/MiniMax-H3) 可以实现零代码视频生成工作流，是当下多模态创作最值得上手体验的模型之一。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*