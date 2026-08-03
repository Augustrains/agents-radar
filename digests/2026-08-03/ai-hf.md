# Hugging Face 热门模型日报 2026-08-03

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-03 01:25 UTC

---

# 🤖 Hugging Face 热门模型日报（2026-08-03）

## 📌 今日速览

今日 Hugging Face 榜单由 **Kimi-K3** 以近万周点赞强势领跑，多模态能力成为头部模型标配。**DeepSeek-V4-Flash** 系列延续热度，原版与社区 GGUF 量化版同时上榜。国内厂商表现亮眼，**百度**的 OCR 模型下载量突破 250 万，**智谱 GLM-5.2** 进入点赞前五。值得关注的是，**Qwen3.6 系列社区微调**（含大量 Uncensored 变体）形成庞大生态集群，而 **Solar-Open2-250B** 的超大模型量化版本（NVFP4）也首次出现，标志着大模型压缩技术进一步成熟。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 1,722 | 156,173 | DeepSeek 最新快照版本，延续高效推理路线 |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,958 | 2,785,810 | 原版 V4-Flash，下载量近 280 万，社区主力推理模型 |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,755 | 2,050,533 | 智谱最新 MoE 架构模型，下载超 200 万，对话能力强劲 |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 626 | 33,042 | 3B 轻量级 LLM，适合端侧部署与低成本场景 |
| [**Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 877 | 80,102 | poolside 新版本模型，聚焦工程与代码场景 |
| [**Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 719 | 14,863 | 250B 超大 MoE 模型，Upstage 开源旗舰 |
| [**Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 153 | 68,199 | 250B 模型的 NVFP4 量化版，大幅降低推理门槛 |
| [**XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 335 | 1,094 | Qwen3.5-MoE 架构，主打智能体搜索场景 |
| [**XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 366 | 903 | Aquila 系列迷你版，轻量高效 |
| [**LFM2.5-Encoder-350M**](https://huggingface.co/LiquidAI/LFM2.5-Encoder-350M) | LiquidAI | 89 | 6,957 | Liquid AI 编码器模型，fill-mask 任务 |
| [**Instella-MoE-16B-A3B-Think**](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 121 | 1,957 | AMD 推出的 MoE 推理增强版，DeepSeek-V3 架构衍生 |

### 🎨 多模态与生成（视觉、语音、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **9,637** | 837,202 | 今日榜首，Kimi 多模态大模型，综合能力极强的 image-text-to-text 模型 |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,778 | 2,536,284 | 百度开源 OCR 模型，下载量榜首，通用文字识别能力出色 |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 185 | 272,148 | 微软多模态视觉语言模型，通用视觉理解 |
| [**Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 250 | 2,938 | 微软 Qwen3.5 架构多模态模型，主打 Computer-Use 场景 |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 227 | 6,839 | 轻量多模态对话模型，端侧部署友好 |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 371 | 1,825 | 轻量 TTS 模型，主打 CPU 与边缘设备部署 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 179 | 4,314 | 新一代 TTS 预览版，基于 ArkTTS 架构 |
| [**VibeVoice-ASR-BitNet**](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 150 | 8,468 | 微软 BitNet 架构 ASR 模型，支持 GGUF 量化 |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 126 | 0 | Krea 2 的 LoRA 模型，适配 ComfyUI 工作流 |

### 🔧 专用模型（代码、OCR、音频理解）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 402 | 13,164 | 基于 Qwen3.5-MoE 的代码生成模型，开发者预览版 |
| [**Qwythos-27B-v1**](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 96 | 1,279 | Qwen3.5 架构，偏好多模态推理场景 |

### 📦 微调与量化（社区微调、GGUF）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,339 | 1,372,285 | Qwen3.6 社区微调明星，融合多项技术，下载超 137 万 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 339 | 48,707 | unsloth 官方量化版 V4-Flash，推理部署首选 |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 250 | 88,481 | Kimi-K3 量化版，兼顾多模态能力与部署效率 |
| [**Kimi-K3** (unsloth)](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 225 | 1,277 | unsloth 优化版 Kimi-K3（非量化版） |
| [**Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | **3,243** | 1,892,654 | Qwen3.6 最热 Uncensored 微调之一，带视觉能力，下载近 190 万 |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 300 | 259,237 | Hermes 系列微调 GGUF 量化，社区热度高 |
| [**Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 208 | 292,511 | 9B 级多风格微调 GGUF，支持 MTP 推理 |
| [**Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 119 | 2,550 | Qwen3.6 社区微调，延续 MoE 路线 |

---

## 🌐 生态信号

**多模态成主流**：Kimi-K3 登顶、百度 OCR 下载量破 250 万、微软发力 Mage-VL 与 Fara1.5，显示头部玩家已将多模态视为默认能力，纯文本模型在趋势榜占比明显收窄。

**Qwen 生态强势扩张**：基于 Qwen3.5/3.6 架构的衍生模型（微调、量化、Uncensored 变体、MoE）超过榜单三分之一，Qwen 已从单一模型演化为最大开源生态基座，尤其在 35B-A3B 这个性价比 MoE 尺码上竞争激烈。

**量化与压缩成为刚需**：从 unsloth 的 GGUF 到 nota-ai 的 NVFP4，大模型（250B）量化版本开始出现——运行超大模型的门槛正在被系统性降低，量化工具链成熟度是生态繁荣的关键信号。

**开源权重势头强劲**：中国团队（DeepSeek、月之暗面、智谱、百度）持续开源核心权重且体验领先，开源模型的能力下限与闭源差距不断缩小，竞争进入"开源普惠"时代。

---

## 💡 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周人气王，堪称新一代多模态标杆。作为 image-text-to-text 模型，它兼具视觉理解与复杂对话能力，且已有 unsloth GGUF 量化版，值得第一时间体验与测试边界。

2. **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 百度开源 OCR 模型，下载量已突破 250 万次大关。无论是文档解析、票据识别还是复杂版面还原，它都是一款值得接入生产流程的通用工具。

3. **[Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4)** — 250B 超大模型的 4-bit 量化稀缺样本，代表前沿压缩技术上限。如果你的 GPU 集群有限却想探索超大模型的下限能力，这一款值得深入研究。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*