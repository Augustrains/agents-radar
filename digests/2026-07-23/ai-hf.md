# Hugging Face 热门模型日报 2026-07-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-23 01:26 UTC

---

好的，作为AI模型生态分析师，以下是2026年7月23日的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-23**

#### **今日速览**

本周Hugging Face生态呈现两大热点：一是**多模态模型全面爆发**，以`google/gemma-4-31B-it`和多个视觉理解模型为代表，融合图像、文本甚至音频的交互式模型成为绝对主流；二是**极端量化与模型瘦身**活动异常活跃，`prism-ml`的1-bit模型与大量GGUF量化版本占据了榜单半壁江山，社区对在消费级硬件上运行强大模型的渴望前所未有。同时，我们也看到百度、NVIDIA等巨头持续在OCR、ASR等垂直场景发布高质量专用模型。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org | 点赞: 4,336 | 下载: 545k)
  - **一句话**：采用MoE架构的新一代GLM模型，凭借强大的综合对话能力获得了本周最高点赞量，是国产模型的又一力作。
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** (google | 点赞: 3,328 | 下载: 12,113k)
  - **一句话**：Google的开源多模态语言模型，以海量下载量证明了其强大实力，是目前社区最受欢迎的基础模型之一。
- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** (upstage | 点赞: 251 | 下载: 0)
  - **一句话**：Upstage推出的250B超大参数开源模型，虽然下载量不多，但其发布本身预示着开源模型在规模上的持续攀升。
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** (Nanbeige | 点赞: 231 | 下载: 0)
  - **一句话**：一款小而精的3B参数模型，适合在资源受限场景下进行部署和研究。
- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** (Motif-Technologies | 点赞: 159 | 下载: 125)
  - **一句话**：一款专注于特征提取的新模型，表明社区对深度语义理解的需求依然强劲。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu | 点赞: 2,712 | 下载: 2,237k)
  - **一句话**：百度出品的通用OCR模型，凭借超高的下载量和实用性，堪称本周“最接地气的流行之星”。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS | 点赞: 3,000 | 下载: 1,997k)
  - **一句话**：基于Qwen3.6的社区微调版，融合了MoE、Vision和不加限制的风格，体现了社区对特定对话风格的追求。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai | 点赞: 2,416 | 下载: 2,133k)
  - **一句话**：基于Qwen3.5的推理增强型模型，量化后下载量惊人，是“轻量级推理”的社区标杆。
- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** (thinkingmachines | 点赞: 1,449 | 下载: 16k)
  - **一句话**：一款新颖的多模态（图像+文本）交互模型，标志着“Inkling”系列模型的诞生。
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** (moonshotai | 点赞: 1,223 | 下载: 722k)
  - **一句话**：月之暗面推出的Kimi模型代码版，在代码理解和生成任务上表现突出。
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** (nvidia | 点赞: 89 | 下载: 6.6k)
  - **一句话**：NVIDIA的世界模型系列新成员，专注于视频生成和理解，是物理世界模拟的开源尝试。
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** (microsoft | 点赞: 124 | 下载: 0)
  - **一句话**：微软的图像生成编辑模型，保持了一流图像生成能力。
- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** (Alissonerdx | 点赞: 235 | 下载: 0)
  - **一句话**：用于视频生成的身份保持LoRA，是社区在可控视频生成方向的最新探索。
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** (OpenMOSS-Team | 点赞: 308 | 下载: 92k)
  - **一句话**：集语音转录与说话人分离于一体的MOSS模型，打开了音频理解的新维度。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** (nvidia | 点赞: 914 | 下载: 590k)
  - **一句话**：NVIDIA的高效流式语音识别模型，在小参数下实现了出色的实时ASR表现。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** (ATH-MaaS | 点赞: 249 | 下载: 17k)
  - **一句话**：基于Qwen3.5的OCR专用多模态模型，进一步提升了文档识别准确性。
- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** (conradlocke | 点赞: 495 | 下载: 0)
  - **一句话**：基于Krea-2的LoRA模型，用于保持身份特征的图像编辑，展示了LoRA在精细控制方面的潜力。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** (prism-ml | 点赞: 595 | 下载: 1,404k)
  - **一句话**：大名鼎鼎的“盆景”模型，其1-bit GGUF版本极受社区欢迎，是用极低成本运行27B模型的关键。
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** (prism-ml | 点赞: 941 | 下载: 432k)
  - **一句话**：Bonsai的三元量化版，在1-bit基础上进一步探索了极端量化边界。
- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** (DavidAU | 点赞: 321 | 下载: 62k)
  - **一句话**：社区模型命名的“集大成者”，代表了用户对定制化、无限制对话模型的极致需求。
- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** (GnLOLot | 点赞: 153 | 下载: 51k)
  - **一句话**：对MiniCPM-5模型的思考能力进行增强的量化版，体现了小模型+思考链的趋势。
- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** (prism-ml | 点赞: 165 | 下载: 25k)
  - **一句话**：Bonsai的Apple MLX生态1-bit版本，专为Mac用户优化。
- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** (unsloth | 点赞: 120 | 下载: 7.3k)
  - **一句话**：官方推荐的Inkling模型GGUF量化版，方便玩家快速上手体验。
- **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** (unsloth | 点赞: 106 | 下载: 0)
  - **一句话**：Laguna-S模型的GGUF量化版，由知名微调团队Unsloth出品。
- **[poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)** (poolside | 点赞: 91 | 下载: 1.9k)
  - **一句话**：Laguna-S模型的4-bit浮点数量化版，适配NVIDIA的最新硬件。

#### **生态信号**

1.  **模型家族势头正旺**：以**Bonsai**和**Laguna-S**为代表的系列模型（含多个量化变体）表现出强大的家族效应；**Qwen**系列依然是社区微调与量化的主要基座模型基础（多个衍生模型入榜）。
2.  **开源权重的胜利**：榜单前20几乎全部是开源模型，权重公开+GGUF量化的组合拳，让任何有硬件资源的人都能运行先进模型，这极大地推动了AI应用民主化。
3.  **“瘦身”是核心主题**：本周最激动人心的活动是围绕**极端量化**（1-bit、三元量化）的爆发。`prism-ml`的Bonsai模型证明了将27B模型压缩到可运行于个人电脑是可行的，这预示着未来模型部署将更加看重“性能/体积比”而非单纯参数。

#### **值得探索**

1.  **`zai-org/GLM-5.2`**: 毫不意外，它是本周点赞王的Model。推荐研究其MoE架构设计，以及它如何在不达到最大参数量的情况下实现出色的对话效果。
2.  **`prism-ml/Bonsai-27B-gguf`**: 如果你对“小成本跑大模型”感兴趣，这款模型绝对是必玩之作。分析其1-bit (或三元) 量化如何保持模型性能，对于理解模型压缩技术的极限至关重要。
3.  **`openbmb/MiniCPM-RobotManip`**: 这是一个非常有趣的信号。它将VLM技术用于机器人操控（Robotics），代表了多模态模型向物理世界交互延伸的前沿趋势，值得所有从事具身智能研究的开发者关注。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*