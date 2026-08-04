# Hugging Face 热门模型日报 2026-08-04

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-04 01:16 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-04

---

## 📰 今日速览

今日 Hugging Face 榜单由 **Kimi-K3** 领跑，以 9,848 周点赞断层登顶，标志着多模态推理模型进入全面爆发期。**DeepSeek-V4-Flash** 系列（含 0731 更新版）与 **GLM-5.2** 分列第二梯队，国产大模型在开源社区号召力持续攀升。值得注意的是，**Qwen3.6 家族**出现了大量社区微调与 GGUF 量化版本（共 5 款上榜），且多款带有 "Uncensored" 标签，反映出开源社区对"去限制化"模型的旺盛需求。此外，**MiniMax-H3** 视频生成模型、**baidu/Unlimited-OCR** 和多款 TTS 模型上榜，多模态与效率工具赛道热度显著上升。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,057 | 236,076 | DeepSeek V4 系列的最新更新版，对话能力进一步增强 |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,797 | 2,180,509 | 智谱 GLM 最新一代 MoE 模型，周点赞排名第四，下载量突破 218 万 |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,990 | 2,746,291 | V4 系列基础版，两周内累计下载近 275 万，社区热度极高 |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 652 | 34,705 | 小体积高效 LLM，主打资源受限场景下的流畅对话 |
| [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 909 | 81,584 | 新一代通用对话模型，推理效率与响应质量兼备 |
| [**EschaLabs/Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 153 | 2,682 | Qwen3.6 架构 MoE 变体，35B 总量、3B 激活参数的高效设计 |
| [**amd/Instella-MoE-16B-A3B-Think**](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 148 | 2,078 | AMD 基于 DeepSeek-V3 架构的思考型 MoE 模型，体现硬件厂商入场 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,848 | 967,622 | 月之暗面多模态推理旗舰，本周断层第一，采用压缩张量技术 |
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 1,458 | 0 | MiniMax 最新图像/文本转视频模型，尚处预热期，下载量为零值得关注 |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,846 | 2,601,062 | 百度发布的通用 OCR 模型，周点赞第三、下载量第一（260 万+） |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 212 | 4,609 | 轻量级语音合成 TTS 模型，基于 ArkTTS 架构 |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 398 | 1,944 | 针对 CPU/边缘设备的轻量 TTS，主打本地部署语音合成 |
| [**lodestones/Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 159 | 0 | 基于 Krea2 的 LoRA 文生图模型，适配 ComfyUI 工作流 |
| [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 231 | 431,487 | 微软多模态视觉语言模型，下载量超 43 万，应用广泛 |

### 🔧 专用模型（代码、OCR、Agent、计算机使用）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 444 | 14,339 | 基于 Qwen3.5-MoE 架构的代码生成模型，开发者预览版 |
| [**microsooft/Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 268 | 2,988 | 微软计算机使用（computer-use）智能体模型，基于 Qwen3.5 |
| [**XYZAILab/XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 351 | 1,214 | 面向智能体搜索场景的 Qwen3.5-MoE 架构模型 |
| [**XYZAILab/XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 391 | 1,063 | Aquila 系列轻量版，可兼顾对话与搜索场景 |

### 📦 微调与量化（社区微调、GGUF、量化）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,430 | 1,550,034 | Qwen3.6 重度社区微调 GGUF 版，集多种优化于一体，下载超 155 万 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 428 | 69,656 | unsloth 官方 DeepSeek-V4 量化版，主打本地部署效率 |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 281 | 128,215 | Kimi-K3 量化版，社区下载超 12 万，降低多模态推理门槛 |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 342 | 287,745 | LuffyTheFox 最新 Hermes V6 微调 GGUF，去审查 + 高下载量 |
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,269 | 1,895,741 | Qwen3.6 社区微调"激进模式"，周点赞第五，下载逼近 190 万 |
| [**Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 168 | 68,778 | 250B 超大模型 NVFP4 量化版，面向 vLLM 推理优化 |
| [**Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 237 | 304,420 | DavidAU 另一款 Qwen3.5 微调 GGUF，多格式支持 |
| [**Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot) | ethanfel | 93 | 0 | 融合 Qwen3-VL 与 MiniMax-H3 的 ComfyUI INT8 混合微调模型 |

---

## 📡 生态信号

**家族势力版图**：本周最强劲的三大模型家族为 **Qwen3.5/3.6**（8 款上榜）、**DeepSeek-V4**（4 款）和 **Kimi-K3**（3 款）。Qwen 生态的社区二创活跃度已形成生态规模效应，从官方底座到 uncensored 微调、GGUF量化、MoE改造，覆盖了从开发者到普通用户的完整链条。

**开源权重趋势**：榜单 30 款模型全部为开源权重，开源/闭源比例进一步拉开差距。值得注意的是，闭源厂商（如 MiniMax-H3、AI 视频生成）也开始以"模型权重开源+API 闭源"的混合模式入局，多模态领域正成为开源竞争的新战场。

**量化与微调信号**：GGUF 是绝对主流格式（9 款），社区"Uncensored"微调（去掉安全对齐限制）占比接近 20%，且多款下载量超过百万，反映出社区对内容自由度的强烈偏好。NVFP4 量化首次出现在热门榜单（Solar-Open2-250B），标志着超大模型在消费级硬件上的推理正在成为现实。

---

## 🔬 值得探索

1. **Kimi-K3**（[链接](https://huggingface.co/moonshotai/Kimi-K3)）— 周点赞近万、断层第一的多模态推理模型，采用压缩张量技术，其架构创新值得深入拆解，是观察下一代多模态大模型方向的最佳样本。

2. **MiniMax-H3**（[链接](https://huggingface.co/MiniMaxAI/MiniMax-H3)）— 零下载却获 1,458 点赞，说明社区对文生视频新模型有极高期待值。作为榜单上唯一的视频生成模型，值得密切关注其能力边界。

3. **nota-ai/Solar-Open2-250B-Nota-NVFP4**（[链接](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4)）— 250B 超大模型成功量化至 NVFP4 格式，代表了"超大模型 + 高效量化"的前沿方向，对研究模型压缩与高效推理极具参考价值。

---

*数据时间：2026-08-04 | 来源：Hugging Face Hub 热门榜（按周点赞排序）*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*