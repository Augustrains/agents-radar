# Hugging Face 热门模型日报 2026-08-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-09 00:43 UTC

---

# 🤗 Hugging Face 热门模型日报 — 2026-08-09

## 📌 今日速览

今日榜单呈现**视频生成**与**多模态大模型**双雄争霸的格局：MiniMax-H3 凭借 3104 周点赞登顶视频生成赛道，围绕其生态已涌现出 ComfyUI 工作流、GGUF 量化、LoRA 微调等 8 个衍生模型，形成完整的社区生态闭环。语言模型方面，DeepSeek-V4-Flash 以 78.5 万下载量领跑推理部署，GLM-5.2 和 Kimi-K3 分别以 4902 与 10342 点赞展现国产开源模型的强劲势头。值得关注的是，**"无审查"（Uncensored）微调**成为社区最活跃的二次创作方向，多个基于 Qwen3-VL 的衍生模型进入榜单。此外，百度 Unlimited-OCR 凭借 3970 点赞成为榜单黑马，显示垂直领域专用模型同样具有巨大吸引力。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **10,342** | 1,388,105 | 月之暗面新一代多模态大模型，支持压缩张量技术，以 1 万+点赞登顶语言模型热度榜首 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,902 | 2,480,368 | 智谱 GLM 系列最新旗舰，采用 MoE-DSA 架构，下载量突破 248 万 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,852 | **785,771** | DeepSeek V4 Flash 版本，主打高效推理，下载量居语言模型之首 |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 415 | 81,522 | Liquid AI 的液态基础模型，2.6B 小参数实现高效部署 |
| [maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 255 | 896 | deepgrove 推出的 MoE 架构预览模型，主打因果语言建模 |
| [Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 221 | 4,189 | 零一万物 Ling 系列 Flash 版本，对话优化 + 自定义代码支持 |

### 🎨 多模态与生成（图像、视频、音频）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | **14,037** | 502,330 | 黑森林实验室文生图旗舰模型，以 1.4 万点赞稳居全榜第一 |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,104 | 26,693 | MiniMax 视频生成旗舰，支持图像+文本双条件驱动视频生成 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,970 | 2,857,997 | 百度推出的无限场景 OCR 模型，下载量逼近 286 万，是当日最大黑马 |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 314 | 457,581 | 微软多模态视觉语言模型，支持图像文本联合理解 |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 346 | 28,178 | thinkingmachines 的小规模多模态对话模型 |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 246 | 458 | 英伟达 11B 语音对话模型，集成多篇最新语音技术 |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 321 | 12,837 | Audio8 语音合成预览版，基于 ArkTTS 架构 |

### 🔧 专用模型（代码、OCR、安全）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 544 | 17,885 | 基于 Qwen3.5-MoE 的代码专用模型，面向开发者场景 |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 201 | 4,950 | Mistral 推出的 3B 安全护栏模型，用于内容审核与过滤 |

### 📦 微调与量化（社区微调、GGUF、LoRA）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [MiniMax-H3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,006 | **3,943,176** | ComfyUI 官方适配版 MiniMax-H3，下载量近 400 万居全榜之首 |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,761 | 2,345,190 | Qwen3.6 的"无审查"社区微调版，GGUF 量化格式，下载量超 234 万 |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 607 | 175,093 | unsloth 出品的 DeepSeek V4 GGUF 量化版，适配 llama.cpp 生态 |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 438 | 373,651 | Qwen3.6 MoE 架构 + Hermes 微调 + Uncensored 的 GGUF 版本 |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 484 | 0 | MiniMax-H3 的 Turbo LoRA 适配器，支持文生视频+音频 |
| [Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 403 | 0 | 面向 ComfyUI 的 Qwen3-VL 32B 无审查微调版，INT8 量化 |
| [Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 143 | 471,519 | MiniMax-H3 的混合精度量化版（NVFP4+INT4+INT8），下载超 47 万 |
| [Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 198 | 0 | 轻量级 MiniMax-H3 Turbo 版，支持图像/文本/参考视频生成 |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 175 | 128,265 | MiniMax-H3 的 GGUF 量化系列，适配 ComfyUI |
| [MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 205 | 0 | ComfyUI 专用 MiniMax-H3 Turbo LoRA，剪枝优化 |
| [PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 170 | 0 | 社区微调的 MiniMax-H3 文生视频风格模型 |
| [Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 133 | 0 | Qwen3-VL 32B 无审查微调，NVFP4 量化，用作 MiniMax-H3 文本编码器 |
| [MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 183 | 0 | Kijai 出品的 ComfyUI 工作流适配版 |
| [LFM2.5-2.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 157 | 49,562 | 官方 Liquid 模型 GGUF 量化版，支持 llama.cpp |
| [MiniMax-H3-experimental](https://huggingface.co/Kijai/MiniMax-H3-experimental) | Kijai | 140 | 0 | MiniMax-H3 实验性版本，探索新功能 |

---

## 🌐 生态信号

**视频生成生态爆发**：MiniMax-H3 已成为当日生态核心，围绕其衍生出 8+ 个适配模型（ComfyUI、GGUF、LoRA、量化），形成从基础模型→工具链→社区微调的完整生态闭环。

**国产模型主导开源**：DeepSeek、GLM、Kimi、MiniMax、百度、零一万物集体上榜，Top 10 中国产模型占据六席，显示国产开源大模型在质量与社区运营上已全面领先。

**"无审查"微调成风**：榜单出现 5+ 个标记为 "Uncensored"/"Heretic" 的社区微调模型，主要基于 Qwen 系列进行安全对齐移除，反映部分开发者对"无约束"模型的需求。此类模型伴随安全风险，应谨慎评估使用场景。

**量化部署需求旺盛**：GGUF 格式模型总下载量超 300 万，社区对本地部署的需求极为强烈，unsloth、llama.cpp 等工具链成为基础设施级存在。

---

## 🔬 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 以 10,342 点赞登顶语言模型榜首，其"压缩张量"（compressed-tensors）技术值得深入研究。若能以更小存储实现同等性能，将深刻影响推理效率。

2. **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 百度"无限场景"OCR 模型以 3970 点赞、286 万下载成为黑马，展现了垂直领域模型的巨大需求，建议评估其在文档解析、图文理解等场景的表现。

3. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 下载量接近 400 万，是视频生成生态的枢纽节点。对于视频生成研究者，建议围绕此模型探索 ComfyUI 工作流与社区插件生态。

---

> **数据说明**：本日报基于 2026-08-09 Hugging Face Hub 热门模型榜（按周点赞排序），数据为当日抓取快照。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*