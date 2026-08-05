# Hugging Face 热门模型日报 2026-08-05

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-05 01:18 UTC

---

# 🤖 Hugging Face 热门模型日报（2026-08-05）

## 📌 今日速览

本周 Hugging Face 榜单呈现三大核心趋势：**Kimi-K3**（周点赞 10,010）强势登顶，成为首个突破万赞的多模态 MoE 模型，同时其 GGUF 量化版也同步上榜，显示社区对该模型的高度关注；**DeepSeek-V4** 系列双版本上榜（Flash 与 Flash-0731），下载量合计超 300 万，进一步巩固其开源对话模型头部地位；**GLM-5.2** 以 4,819 赞紧随其后，国产开源 MoE 模型阵营持续壮大。此外，**MiniMax-H3** 视频生成模型在本周形成"原版 + ComfyUI 适配 + GGUF 量化"的完整生态链条，标志着视频生成开源生态的快速成熟。值得注意的还有大量 Qwen3.6 社区微调模型（如 HauhauCS-Aggressive 获 3,296 赞）集中爆发，展示出极强的社区二次创作活力。


## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,010 | 1,125,935 | 本周榜单冠军，Kimi 新一代多模态 MoE 模型，采用压缩张量技术，支持视觉与文本混合输入 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,819 | 2,234,662 | 智谱 GLM 系列最新 MoE 模型（DeepSeek 式注意力），对话能力跃升，下载量突破 220 万 |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,011 | 2,737,621 | DeepSeek V4 轻量级版本，本榜单下载量最高，兼顾性能与推理效率 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,299 | 433,284 | 7 月 31 日迭代版，基于 Flash 的快速更新，带来更强对话能力 |
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 473 | 15,381 | 基于 Qwen3.5 MoE 架构的代码生成模型，面向开发者场景 |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 404 | 1,317 | 基于 Qwen3.5 MoE 的小型化模型，支持多模态与文本生成 |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 358 | 1,388 | Aquila 系列专业版，内置 Agentic Search 能力 |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 664 | 37,256 | 3B 轻量级 LLM，主打高效推理与中文场景 |
| [K-EXAONE-2.0-750B-A37B](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 117 | 325 | LG 出品 750B 超大 MoE 模型（激活 37B），韩语/多语能力突出 |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 | 82,912 | poolside 最新旗舰代码 LLM，专注软件工程自动化 |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 153 | 47,393 | Liquid AI 第三代液体神经网络模型，2.6B 小参数高表现 |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 174 | 69,253 | Solar Open2 250B 的 NVFP4 量化版，配合 vLLM 高效推理 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,020 | 0 | MiniMax 新一代视频生成模型，支持文本/图像到视频，生态热度极高 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,881 | 2,703,366 | 百度开放的全场景 OCR 模型，下载量达 270 万，通用文档理解标杆 |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 286 | 15,500 | 小型多模态对话模型，支持图像+文本输入 |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 256 | 435,784 | 微软开源视觉语言模型，下载量超 43 万 |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 247 | 11,276 | 新一代 TTS 模型，支持特征提取，语音合成自然度高 |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 410 | 2,072 | 本地 CPU 可运行的轻量 TTS 模型，主打边缘 AI 场景 |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 176 | 0 | Krea2 的 LoRA 适配器，效果增强文本到图像生成 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 473 | 15,381 | 基于 Qwen3.5 MoE 的代码生成模型，面向开发者场景 |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 | 82,912 | 软件工程专用 LLM，代码生成与理解能力突出 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,296 | 1,930,898 | Qwen3.6 社区微调爆款，去除审查 + 激进风格，下载量近 200 万 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711...GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,512 | 1,633,405 | Qwen3.6 社区微调 + GGUF 双格式，主打去审查与叙事融合 |
| [LuffyTheFox/Qwen3.6-35B-A3B...GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 364 | 308,857 | Qwen3.6 Hermes V6 风格微调 GGUF，去审查 + 高质量对话 |
| [unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 468 | 111,678 | unsloth 官方量化，DeepSeek V4 本地部署首选 |
| [unsloth/Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 304 | 170,055 | Kimi-K3 的 GGUF 量化版，推动多模态模型本地化 |
| [DavidAU/Qwen3.5-9B-The-Defiant-Fable...GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 265 | 323,116 | Qwen3.5 9B 社区微调，IMATRIX + MTP 双格式支持 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 600 | 2 | MiniMax-H3 ComfyUI 官方适配版，完善视频生成工作流 |
| [realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 103 | 40,010 | MiniMax-H3 的 GGUF 量化版本，推动视频生成本地部署 |
| [Qwen3-VL-32B-Ultra-Heretic...ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot) | ethanfel | 188 | 0 | 融合 Qwen3-VL + MiniMax-H3 的 ComfyUI 适配 INT8 量化合集 |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 192 | 2,987 | Qwen3.6 35B MoE 的社区优化版 |
| [Qwythos-27B-v1](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 134 | 2,243 | 基于 Qwen3.5 的 27B 社区微调，支持多模态输入 |


## 📊 生态信号

**模型家族势头分析：** Qwen3.6 系列（原 Qwen3.5-MoE）在社区微调中表现最抢眼——HauhauCS、DavidAU、LuffyTheFox 等多个团队基于其 35B-A3B 架构进行了 "uncensored" 风格微调，总点赞数超 5,000，总下载量超 380 万。DeepSeek-V4 与 Kimi-K3 组成第一梯队旗舰，前者强调极致对话性能，后者依托多模态 MoE 创下历史性点赞记录。MiniMax-H3 则快速形成从原模型到 ComfyUI 适配、GGUF 量化的完整生态链条。

**开源 vs 闭源：** 本周榜单 30 个模型中 28 个为开源模型，开源权重已成为 AI 模型的绝对主流。值得关注的是，百度（Unlimited-OCR）与微软（Mage-VL）等大型科技公司加速拥抱开源，顶级闭源模型的独家优势正在被快速侵蚀。

**量化与微调活动：** GGUF 量化仍是本地部署的核心路径，unsloth 在标准化量化方面持续领跑；社区微调则呈现明显的 "uncensored" 与 "角色扮演" 偏好，DavidAU、LuffyTheFox 等创作者形成稳定的高质量输出。NVFP4 等新量化格式的出现为超大模型（如 Solar-Open2-250B）的本地运行打开了新可能。


## 🔬 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周最大亮点，历史性突破万赞。其"压缩张量"（compressed-tensors）技术为多模态 MoE 模型开拓了新思路，强烈建议深入研究其架构设计与推理效率，同时可直接体验其 GGUF 版本在多模态场景中的表现。

2. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 智谱 GLM 系列首次引入 MoE 架构（glm_moe_dsa），在对话能力上取得质的飞跃。作为国产开源模型的代表之作，其在中文场景的表现和 DeepSeek 系列的差异化定位值得探索。

3. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 社区微调的现象级案例，3,296 赞、193 万下载量，是理解开源社区对模型能力诉求（去审查、风格化）的最佳样本，同时展示了 Qwen3.6 强大的可塑性。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*