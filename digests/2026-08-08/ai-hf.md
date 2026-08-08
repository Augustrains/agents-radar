# Hugging Face 热门模型日报 2026-08-08

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-08 00:41 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-08

## 今日速览

今日榜单呈现"视频生成 + 多模态 LLM"双强格局：**MiniMax-H3** 凭借 2,953 周点赞登顶视频生成赛道，其社区衍生生态（ComfyUI 集成、Turbo LoRA、GGUF 量化）蔚然成型，3 个衍生模型合计下载超 360 万次。语言模型方面，**Kimi-K3** 以 10,281 点赞高居总榜次席，**GLM-5.2** 紧随其后，**DeepSeek-V4-Flash** 则以 70 万下载量展现强劲的部署需求。值得注意的还有 **FLUX.1-dev** 以 14,028 点赞占据总榜第一，证明其作为开源文生图基座的持久统治力。整体来看，围绕头部模型的"周边生态"（微调、量化、ComfyUI 适配）正成为下载量增长的主要引擎。


## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,281 / 1,308,186 | Kimi 最新多模态旗舰，采用压缩张量技术，兼具特征提取能力，总点赞榜第二，是当前社区最受关注的多模态 LLM。 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,744 / 702,709 | DeepSeek V4 系列轻量版，70 万下载量印证其作为高效部署首选的开源 LLM 地位。 |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,887 / 2,430,330 | 智谱最新 MoE 架构模型，采用 GLM MoE DSA 结构，240 万下载量表明其是当前中文开源社区的主力模型之一。 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 379 / 77,973 | Liquid AI 的液态网络 2.5 代小模型，2.6B 参数主打高效推理，官方同时提供 GGUF 版本。 |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 184 / 2,480 | Mistral 推出的 3B 安全防护模型，用于内容审核与输出过滤，与 Mistral 3 系列生态配套。 |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 226 / 686 | DeepGrove 推出的 MoE 因果语言模型预览版，新玩家入场值得关注。 |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 203 / 3,065 | 阶跃星辰的百灵混合架构轻量版，定位快速对话响应。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,953 / 18,112 | 本周视频生成最大爆点，支持图生视频/文生视频双模态，其衍生社区生态异常繁荣（见下方量化分类）。 |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,028 / 512,841 | 开源文生图标杆模型，总点赞榜首，持续被社区视为图像生成的基座首选。 |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,954 / 2,836,694 | 百度推出的通用 OCR 模型，280 万下载量登顶下载榜，是当前最强开源文字识别方案。 |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 302 / 456,140 | 微软多模态理解模型，45 万下载量显示企业级用户在快速跟进。 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 228 / 359 | 英伟达语音对话模型，11B 参数，面向实时语音交互场景。 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 306 / 12,633 | 基于 ArkTTS 架构的轻量语音合成模型，600M 参数主打低延迟 TTS。 |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 221 / 0 | Krea 2 的社区 LoRA，用于文生图风格迁移，但尚未产生下载量。 |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 336 / 25,340 | Thinking Machines 推出的多模态聊天模型小杯版，强调对话体验。 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 531 / 17,399 | 基于 Qwen3.5 MoE 架构的代码生成模型，面向开发者场景。 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|------------|-----------|
| [**MiniMax-H3**（Comfy-Org 版）](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 936 / 3,139,920 | MiniMax-H3 的 ComfyUI 单文件封装，314 万下载量是视频生成工作流的流量入口。 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 586 / 161,253 | Unsloth 官方量化版本，让 DeepSeek-V4 在消费级硬件上可跑。 |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-...-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,706 / 2,217,339 | 社区魔改 Qwen 3.6 多版本融合 GGUF，主打"无审查"风格，220 万下载量显示该细分市场需求旺盛。 |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 425 / 332,992 | Hermes 风格微调的 Qwen 3.6 MoE GGUF，33 万下载量。 |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 168 / 87,870 | MiniMax-H3 的视频模型量化版，主打 ComfyUI 推理优化。 |
| [**Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 127 / 452,420 | 混合精度量化的 MiniMax-H3 变体，45 万下载量说明低精度视频生成需求巨大。 |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 415 / 0 | MiniMax-H3 的 Turbo LoRA，目标是加速视频生成。 |
| [**MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 177 / 0 | 面向 ComfyUI 工作流的 MiniMax-H3 Turbo LoRA 适配版。 |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 128 / 0 | 轻量级图像到视频生成模型，同样基于 MiniMax-H3 生态。 |
| [**Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 378 / 0 | 将 Qwen3-VL 作为 MiniMax-H3 的文本编码器，主打 ComfyUI 集成。 |
| [**Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4**](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 121 / 0 | 类似的 Qwen3-VL 文本编码器 + MiniMax-H3 组合，NVFP4 精度优化。 |
| [**MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 114 / 0 | Kijai 的 MiniMax-H3 ComfyUI 原生适配节点仓库。 |
| [**PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 112 / 0 | MiniMax-H3 的社区风格微调版（内容分级）。 |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 144 / 31,489 | LiquidAI 官方 GGUF 版本，适配 llama.cpp 本地推理。 |


## 生态信号

- **MiniMax-H3 生态爆发**：从模型发布到 ComfyUI 集成（314 万下载）、多精度量化（nvfp4/INT8/INT4）、Turbo LoRA、文本编码器替换，Minimax-H3 在榜单上形成完整"家族链"，显示**视频生成模型正在复制 LLM 的生态打法**——官方发布基座 → 社区出量化/适配 → 工作流集成 → 大规模下载。
- **开源权重全面主导**：30 个热门模型 100% 为开源可用权重，闭源 API 模型未进入趋势榜。GLM-5.2、DeepSeek-V4、Kimi-K3 三家国产模型在纯 LLM 赛道形成绝对统治力。
- **GGUF 与"无审查"微调是社区流量密码**：Qwen 3.6 的两款 Uncensored GGUF 合计下载超 250 万次，说明本地部署 + 内容自由是当前 C 端用户的核心诉求。
- **FLUX.1-dev 的长期主义**：发布超过一年仍以 14k 点赞高居榜首，证明"文生图基座 + 社区 LoRA"模式拥有最长尾的生命周期。

## 值得探索

1. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)**（314 万下载）：如果你关注视频生成工作流，这是绕不开的入口。314 万下载量证明其是当前 ComfyUI 生态中视频生成的标准封装，值得深入研究其与原生 diffusers pipeline 的差异。

2. **[unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)**（16 万下载）：Unsloth 的量化版本让 DeepSeek-V4 的部署门槛大幅降低，作为"最强开源 LLM 消费级运行方案"的观察样本很有价值。

3. **[Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy)**：虽是空白仓库（0 下载），但 Kijai 是 ComfyUI 生态最活跃的适配作者之一。其仓库结构常成为社区视频生成工作流的事实标准，值得追踪下一步更新。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*