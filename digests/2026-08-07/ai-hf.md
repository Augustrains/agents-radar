# Hugging Face 热门模型日报 2026-08-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-07 01:58 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-07

## 📌 今日速览

本周 Hugging Face 榜单由**多模态视频生成模型 MiniMax-H3** 及其庞大的社区衍生生态主导，围绕其涌现出大量 ComfyUI 工作流、LoRA 微调与 GGUF/INT8 量化版本。**深度求索 DeepSeek-V4-Flash** 与 **智谱 GLM-5.2** 两大系列延续强势表现，下载量均超百万，充分验证了开源大模型的头部效应。值得关注的还有**月之暗面 Kimi-K3** 以周点赞破万位列语言模型榜首，**百度 Unlimited-OCR** 以一己之力拉动专用模型热度，以及 **FLUX.1-dev** 在文生图领域依然坚挺。从总体趋势看，**视频生成**成为本周最大风口，**MoE 架构**在语言模型中进一步普及，社区微调与量化生态持续繁荣。

---

## 🔥 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,200 / 1.26M | 月之暗面新一代多模态大模型，采用压缩张量技术，以绝对优势登顶本周语言模型点赞榜。 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,871 / 2.39M | 智谱最新一代 MoE 对话模型（GLM MoE DSA 架构），下载量逼近 240 万，国产开源主力军。 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,647 / 618K | 深度求索 V4 系列快速版，兼具高性能对话能力与推理效率，衍生量化版本众多。 |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,042 / 2.64M | V4 系列标准版本，下载量突破 260 万，为本周下载量最高的纯文本生成模型。 |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 332 / 74K | LiquidAI 最新液体神经网络 LLM，2.6B 小参数规模主打高效推理，官方同步提供 GGUF 版本。 |
| [Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 186 / 1.2K | 零一万物（01.AI）推出的快速版混合架构模型，主打低延迟对话场景。 |
| [maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 207 / 419 | 新兴团队 deepgrove 推出的 MoE 架构预览版因果语言模型，尚处早期探索阶段。 |
| [EschaLabs/Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 222 / 3.4K | 基于 Qwen3.6-35B-A3B 的 MoE 社区微调版本，专注推理效率优化。 |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 407 / 309K | Qwen3.6 的免审查微调版 GGUF 量化包，下载量超 30 万，社区热度极高。 |

### 🎨 多模态与生成（图像 / 视频 / 音频）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,010 / 523K | 黑森林实验室文生图旗舰，周点赞稳居全榜第一，持续领跑开源图像生成赛道。 |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,754 / 12K | MiniMax 新一代图像/文本到视频生成模型，本周视频生成赛道最大热点。 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,929 / 2.79M | 百度通用 OCR 大模型，支持海量场景文字识别，下载量近 280 万，登顶专用模型下载榜。 |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 286 / 440K | 微软多模态视觉语言模型，通用图像理解与对话，下载量超 44 万。 |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 322 / 22K | thinkingmachines 推出的轻量级多模态对话模型，主打图像+文本理解。 |
| [Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 337 / 0 | 基于 Qwen3-VL-32B 的社区微调文本编码器，针对 ComfyUI 视频生成工作流优化。 |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 293 / 12K | 新一代语音合成模型（ArkTTS），0.6B 参数量即达高质量 TTS 效果。 |
| [Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 108 / 0 | 面向 MiniMax-H3 工作流的 Qwen3-VL 文本编码器 NVFP4 量化版。 |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 205 / 0 | 基于 Krea2 的 LoRA 模型，用于 ComfyUI 文生图定制化风格生成。 |

### 🔧 专用模型（代码 / 多模态 / 语音 / 安全）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 519 / 17K | 基于 Qwen3.5-MoE 的代码生成模型，面向开发场景的图像+文本混合输入。 |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 158 / 1.5K | Mistral 推出的 3B 安全审核模型，用于输出内容合规检测，支持 vLLM。 |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 177 / 206 | 英伟达 Nemotron Labs 语音对话模型，支持英文语音交互场景。 |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 424 / 1.6K | 基于 Qwen3.5-MoE 架构的迷你版多模态模型，轻量化边缘部署定位。 |

### 📦 微调与量化（社区微调 / GGUF / 压缩）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 848 / 2.30M | MiniMax-H3 的 ComfyUI 整合包，下载超 229 万，是视频生成社区的核心枢纽。 |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,652 / 2.09M | Qwen3.6-27B 社区微调 GGUF 包，集成了融合与免审查特性，下载超 208 万。 |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 545 / 145K | unsloth 推出的 DeepSeek-V4-Flash GGUF 量化版，本地部署首选。 |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 301 / 0 | MiniMax-H3 的 Turbo 加速 LoRA 微调包，支持图文生视频+音频。 |
| [MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 118 / 0 | MiniMax-H3 Turbo LoRA 的 ComfyUI 适配版适配器。 |
| [Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 109 / 273K | MiniMax-H3 的混合精度量化版（NVFP4/INT4/INT8），下载量超 27 万。 |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 153 / 66K | MiniMax-H3 的 GGUF 量化合集，兼容本地轻量推理。 |
| [LFM2.5-2.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 125 / 13K | LiquidAI 官方发布的 LFM2.5 GGUF 量化版，支持 llama.cpp 本地运行。 |

---

## 📊 生态信号

**模型家族态势**：MiniMax-H3 已成为现象级开源视频生成底座，围绕其形成包括 ComfyUI 一键包、LoRA 微调套件、多种量化方案的完整生态链。DeepSeek-V4 与 Qwen3.6 系列在语言模型领域呈双雄争霸格局，前者以官方多版本+unsloth 量化配合构建下载护城河，后者依靠庞大的社区微调力量持续扩散。GLM-5.2 以惊人下载量验证 MoE+DS-A 路线的大众接受度。Kimi-K3 凭借压缩张量技术和月之暗面品牌号召力，在点赞数上异军突起。

**开源 vs 闭源**：头部榜单完全被开源权重模型占据，闭源模型仅以 API 形式存在，未出现在榜单中。开源策略从"可用"走向"好用"，MoE 稀疏激活、压缩张量、多模态融合等先进技术在开源社区已全面铺开。

**量化与微调活动**：GGUF 量化已成为社区标配，覆盖从 2.6B 到 35B 的各类模型；NVFP4/INT8 等新量化格式在视频生成模型中得到积极应用。免审查（Uncensored）、Heretic 风格微调依旧活跃，但热度较前几周有所回落。ComfyUI 生态持续扩张，视频生成+LoRA+量化组合成为新的工作流标配。

---

## 💡 值得探索

1. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** + **[Comfy-Org 整合版](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 本周最值得上手研究的视频生成模型。其生态链完整程度（工作流、LoRA、量化）在开源视频模型中极为罕见，建议从 ComfyUI 版入手快速体验。

2. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 近 240 万下载量表明其在真实生产环境中已被大规模部署。作为 MoE 架构的最新实践（GLM MoE DSA），其架构设计和效率优化值得深入研究。

3. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 周点赞 10,200 断层领先，压缩张量（compressed-tensors）技术路线代表了下一阶段模型轻量化方向，建议关注其如何在大幅压缩模型体积的同时保持多模态理解能力。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*