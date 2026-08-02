# Hugging Face 热门模型日报 2026-08-02

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-02 01:25 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-02

## 📌 今日速览

今日榜单由 **Kimi-K3** 以近万周点赞断层领跑，MoE 架构继续统治榜首。**DeepSeek-V4-Flash** 系列强势回归，原版与 GGUF 量化版同时上榜，下载量突破 280 万。千问（Qwen）生态爆发，多款 Qwen3.5/3.6 社区微调与量化版本占据半壁江山，其中 **HauhauCS/Qwen3.6-35B-A3B-Uncensored** 以 3,225 点赞位列非第一方模型榜首。此外，**GLM-5.2**（4,737 赞）、**Unlimited-OCR**（3,714 赞）等国产模型表现亮眼，多模态与专用模型赛道持续升温。


## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,487 | 559,924 | **今日榜首**，Kimi 最新多模态大模型，采用压缩张量技术，支持图像+文本输入，热度断层第一 |
| [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 1,428 | 15,366 | DeepSeek V4 Flash 最新版本，主打高性能文本生成，配套论文已发布（arxiv:2606.19348） |
| [**deepseek-ai/DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,947 | 2,814,414 | V4 Flash 原版，下载量全榜第二，DeepSeek 生态的核心入口，对话能力广受认可 |
| [**zai-org/GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,737 | 1,683,442 | 智谱 GLM-5.2，MoE-DSA 架构，对话能力对标国际一线，周点赞高居第四 |
| [**upstage/Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 717 | 13,426 | Upstage 开源 250B 级大模型，主打开放权重，适合企业级部署 |
| [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 868 | 77,021 | poolside 的 Laguna 系列最新版，软件工程场景优化，下载量表现稳健 |
| [**Nanbeige/Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 611 | 27,892 | 小尺寸（3B）高效 LLM，轻量部署首选，社区关注度持续走高 |
| [**thinkingmachines/Inkling**](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,672 | 59,076 | thinkingmachines 旗舰多模态对话模型，与 Inkling-Small 形成大小搭配矩阵 |
| [**thinkingmachines/Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 213 | 3,998 | Inkling 的小尺寸版本，兼顾性能与效率，适合资源受限场景 |
| [**XYZAILab/XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 330 | 923 | 基于 Qwen3.5-MoE 的智能体搜索优化模型，Agentic Search 方向探索者 |
| [**XYZAILab/XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 357 | 650 | Aquila 迷你版，基于 Qwen3.5-MoE 架构，轻量高效 |
| [**prism-ml/Ternary-Bonsai-27B-gguf**](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,134 | 716,341 | **三值量化（2-bit）** 27B 模型，极致压缩下保留对话能力，下载量超 71 万 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,714 | 2,457,387 | **百度开源的 OCR 大模型**，下载量全榜第一（245 万+），功能特征提取，通用 OCR 场景全覆盖 |
| [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 172 | 10,525 | 微软多模态理解模型，视觉-语言联合建模 |
| [**microsoft/Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 242 | 2,775 | 基于 Qwen3.5 的 **Computer-Use（计算机操控）** 多模态模型，智能体自动化方向 |
| [**lodestones/Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 95 | 0 | Krea 2 的 LoRA 适配器，文生图微调扩展，ComfyUI 兼容，刚发布暂无下载 |
| [**microsoft/VibeVoice-ASR-BitNet**](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 141 | 5,835 | 微软语音识别模型，**BitNet 架构**，支持 GGUF/GGML 格式，端侧部署友好 |
| [**owensong/Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 361 | 1,565 | 轻量级本地 TTS，CPU 可跑，主打边缘 AI 语音合成 |
| [**Audio8/Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 166 | 3,254 | 基于 ArkTTS 的语音合成预览版，音频特征提取方向 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Kwaipilot/KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 391 | 10,771 | 基于 Qwen3.5-MoE 的代码生成模型，开发者版，专注编程场景 |
| [**LiquidAI/LFM2.5-Encoder-350M**](https://huggingface.co/LiquidAI/LFM2.5-Encoder-350M) | LiquidAI | 87 | 6,190 | Liquid AI 的 350M **编码器模型**（fill-mask），轻量嵌入任务，LFM2 系列 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 288 | 4,048 | Unsloth 出品的 DeepSeek V4 Flash GGUF 量化版，llama.cpp 直接可用 |
| [**unsloth/Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 243 | 41,337 | 榜首模型 Kimi-K3 的 GGUF 量化版，Unsloth 社区出品，本地部署首选 |
| [**unsloth/Kimi-K3**](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 221 | 1,072 | Kimi-K3 的 Unsloth 优化版（非量化），保留原始精度 |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,236 | 1,173,001 | Qwen3.6 社区微调 GGUF，多重技术叠加（MTP、NEO Imatrix），下载量 117 万+ |
| [**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 287 | 228,610 | Qwen3.6 MoE 的 Hermes V6 微调 + GGUF，大尺寸 MoE 本地化 |
| [**HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,225 | 1,823,436 | **社区微调黑马**，Qwen3.6 35B MoE 无审查版，点赞与下载双高（182 万+） |
| [**EschaLabs/Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 112 | 875 | 基于 Qwen3.6 MoE 的 W2 量化版本，专注压缩效率 |
| [**DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 186 | 267,572 | Qwen3.5 9B 社区微调 GGUF，同样叠加 MAX-MTP 技术，下载量 26 万+ |
| [**nota-ai/Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 151 | 22,396 | Solar-Open2 的 **NVFP4 量化版**，vLLM 原生支持，企业级推理优化 |


## 📊 生态信号

**1. 头部模型家族统治力凸显**：Kimi-K3、DeepSeek-V4-Flash、GLM-5.2 三大国产模型包揽赞榜前三（除社区微调外），中文团队（Moonshot、DeepSeek、智谱）已形成与国际一线抗衡的开源力量。

**2. MoE 架构全面上位 + 量化生态繁荣**：榜单中一半以上模型基于 MoE 架构（Qwen3.5/3.6-MoE、GLM-MoE-DSA、DeepSeek-V4），且与量化（GGUF/NVFP4/三值）深度绑定，Unsloth、DavidAU、LuffyTheFox 等社区贡献了大量高下载量化版本，本地部署门槛持续降低。

**3. 多模态与 TTS 双线升温**：以 Kimi-K3 为代表的多模态模型登顶，微软 Mage-VL/Fara1.5 跟进；TTS/ASR 赛道有 Inflect-Micro-v2、Audio8-TTS、VibeVoice 等多个新面孔，边缘 AI（CPU/GGUF）成共同卖点。

**4. 开源权重路线持续强化**：从 250B（Solar-Open2）到 3B（Nanbeige4.2-3B），开源权重覆盖全尺寸段；百度 Unlimited-OCR、微软系列等大厂 + 开源的组合验证了这一路线的可持续性。

**5. 署名值得关注**：DavidAU 和 HauhauCS 的 Qwen 社区微调下载量达百万级，说明“原版 + 社区精调 + GGUF 量化”已成为高效生态闭环。


## 🔬 值得探索

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 周赞 9,487 登顶，代表当前多模态 + 压缩张量技术的前沿水平，建议第一时间体验其视觉-语言联合理解能力。

2. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — 三值量化（2-bit）在 27B 尺度上实现 71 万+下载，是探索极致压缩推理边界的最佳样本。

3. **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — Computer-Use（计算机操控）方向的多模态模型，代表 AI 智能体自动化的前沿，值得深入研究其能力边界与评测方法。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*