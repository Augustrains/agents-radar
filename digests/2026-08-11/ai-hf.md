# Hugging Face 热门模型日报 2026-08-11

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-11 00:45 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-11

---

## 今日速览

本周 HF 生态最大亮点是 **MiniMax-H3** 视频生成模型的全面爆发，官方模型与社区衍生（ComfyUI 集成、Turbo-LoRA、GGUF 量化）合计占据榜单近三分之一席位，下载量达数百万级。**Kimi-K3** 以 1 万+ 周点赞登顶多模态语言模型榜首，延续 Moonshot AI 在压缩感知（compressed-tensors）方向的技术影响力。**DeepSeek-V4-Flash** 凭借 95 万+ 下载量成为最热门的对话模型，unsloth 的 GGUF 量化版本持续为其生态加码。Meta 的 **Muse-Glimmer-30B** 作为新发布的多模态模型未见下载量积累，但 GGUF 和官方版本分列榜单，预示着新一轮发布周期开启。开源权重模型持续占据主导，社区围绕推理效率（量化、LoRA 微调）和工具链集成（ComfyUI、vLLM）的二次创新异常活跃。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | ⬇️ 下载 | 一句话说明 |
|------|------|---------|----------|------------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,059 | 954,441 | DeepSeek V4 代际的轻量对话模型，兼顾性能与推理效率，周下载量近百万 |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,470 | 1,510,032 | 支持图像+文本输入的多模态推理模型，采用压缩张量技术降低部署成本，本周点赞最高 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 490 | 89,680 | Liquid AI 的液态神经网络（LFM）最新版本，2.6B 参数主打高效率边缘部署 |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 311 | 1,344 | 基于 MoE 架构的预览版生成模型，通过稀疏激活降低推理开销 |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 287 | 5,261 | inclusionAI 的混合架构对话模型，支持自定义代码，主打异构计算平台适配 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | ⬇️ 下载 | 一句话说明 |
|------|------|---------|----------|------------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,429 | 47,468 | MiniMax 新一代 text/image-to-video 扩散模型，图片加文字驱动的视频生成新标杆 |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,145 | 6,009,639 | ComfyUI 官方集成的 H3 单文件版，下载超 600 万，成为 H3 生态分发核心 |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 707 | 0 | Meta 新发布的多模态 30B 模型，支持图像+文本双输入对话，尚在冷启动期 |
| [**MiniMax-H3-Turbo-LoRA**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-LoRA) | larryvrh | 599 | 0 | H3 的 Turbo 加速 LoRA，支持文本/音频驱动视频，主打高效微调扩展 |
| [**Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 440 | 0 | 将 Qwen3-VL-32B 与 MiniMax-H3 结合的多模态 ComfyUI 工作流量化版 |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 259 | 15,087 | 面向 t2v/i2v/r2v 多场景的 H3 Turbo 加速版，优化推理速度 |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,076 | 480,762 | Black Forest Labs 的旗舰文本生成图像模型，持续霸榜周点赞第一 |
| [**BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 152 | 617 | 基于 Qwen3.5-MoE 架构的图像文本多模态模型，新团队无限前沿的首个发布 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 👍 点赞 | ⬇️ 下载 | 一句话说明 |
|------|------|---------|----------|------------|
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 4,002 | 2,921,751 | 百度开源的通用 OCR 模型，主打超高精度文字识别，周下载近 300 万 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 297 | 597 | NVIDIA 语音对话 11B 模型，集成多篇语音交互研究，面向实时语音 AI |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 221 | 6,343 | Mistral 的 3B 安全防护模型，用于过滤输入输出内容，vLLM 可直接部署 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍 点赞 | ⬇️ 下载 | 一句话说明 |
|------|------|---------|----------|------------|
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,861 | 2,439,083 | 社区微调的“无限审查”版 Qwen3.6-27B GGUF，融合多模型技术的极致魔改 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 636 | 199,167 | unsloth 官方量化 DeepSeek V4 Flash，5-bit GGUF 兼顾体积与精度 |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 192 | 174,862 | MiniMax-H3 的 GGUF 量化系列，基于 Comfy-Org 正式版，可在 CPU 上推理 |
| [**Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 162 | 530,052 | NVIDIA FP4 + INT 混合精度量化 H3，支持文本/图像/视频多模态生成 |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 184 | 89,611 | 官方 Liquid FM 2.5 GGUF 量化版，llama.cpp 原生支持，本地部署友好 |
| [**PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 250 | 0 | H3 主题的社区微调风格模型，标注 Apache 2.0 且兼容 HF Endpoint |
| [**Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 148 | 0 | 官方 Meta 发布的 Muse-Glimmer GGUF 版本，为本地推理做准备 |
| [**Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4**](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 152 | 0 | 使用 Qwen3-VL-32B 文本编码器为 H3 视频模型服务的 NVFP4 量化版 |

---

## 生态信号

**模型家族势头**：本周三大势力——MiniMax-H3 视频生成家族（官方 + ComfyUI + LoRA + GGUF 多形态覆盖），DeepSeek-V4 对话系列（配合 unsloth GGUF 拉动分发），以及 MoonshotAI Kimi-K3 多模态推理（依托压缩张量技术）。三者分别代表视频生成、对话 AI、多模态理解的赛道领跑者。

**开源权重趋势**：榜单 30 个模型全部为开源权重（含量化与社区微调），未见闭源 API 模型。开源社区的二次创作极为活跃，以 H3 为例，衍生出了 ComfyUI 集成、Turbo 加速、GGUF 量化、混合精度、LoRA 微调等多达 8 个变体，形成完整生态闭环。

**量化与微调焦点**：量化层面，NVFP4/INT8/INT4 混合精度（H3 生态）和 GGUF 格式（覆盖 DeepSeek、MiniMax、Liquid 三大系列）成为标配。微调方向，社区对“内容自由”的追求催生了多个 Uncensored/Heretic 变体（Qwen3.6、Qwen3-VL、H3 均有涉及），同时 ComfyUI 作为工作流引擎继续巩固其在视频生成集成中的地位。

---

## 值得探索

1. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) + [Comfy-Org 版](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 视频生成赛道的核心焦点。官方版与 ComfyUI 单文件版配合使用，6M+ 下载验证了社区认可。如关注部署，可配合 [GGUF 量化版](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) 或 [NVFP4 混合精度版](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) 在低资源环境运行。

2. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 周点赞 10,470 的榜首模型，1.5M 下载。Kimi 系列首次引入压缩张量技术（compressed-tensors），推理显存需求大幅降低，值得多模态研究者和私有化部署团队深入测评。

3. **[unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)** — 若你正在用 DeepSeek V4 构建对话应用，这个官方 GGUF 量化版几乎是本地部署的必选。配合 [unsloth](https://github.com/unslothai/unsloth) 工具链，微调与部署门槛大幅降低。

---

*本报告基于 HF Hub 2026-08-11 热门模型数据生成，点赞与下载均为实时值。*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*