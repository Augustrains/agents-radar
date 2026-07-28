# Hugging Face 热门模型日报 2026-07-28

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-28 01:17 UTC

---

好的，作为 AI 模型生态分析师，以下是为你生成的 2026年7月28日《Hugging Face 热门模型日报》。

---

# 🤗 Hugging Face 热门模型日报 - 2026年7月28日

### 📰 今日速览

1.  **“中国军团”与“大型MoE”主导趋势**：本周榜单由 moonshotai 的 **Kimi-K3** 和 baidu 的 **Unlimited-OCR** 领跑，显示了国内大模型在通用能力和垂直应用上的强劲势头。同时，以 **Qwen3.6-35B-A3B** 为代表的 MoE 架构模型成为绝对主流，兼具高性能与较低推理成本。
2.  **社区“狂欢”Qwen3.6**：Qwen3.6 系列模型成为社区微调与量化的焦点。多个以“Uncensored”、“Aggressive”为标签的社区变体（如 **HauhauCS**、**LuffyTheFox** 版本）下载量极高，反映出社区对特定风格或“无限制”对话模型的强烈需求。
3.  **量化模型“霸榜”下载量**：尽管部分模型点赞数不高，但其量化版本（GGUF）的下载量惊人。例如 **prism-ml** 的 1-bit 和 2-bit 量化的“Bonsai”系列模型，动辄数百万次的下载，表明个人部署和边缘推理仍是生态中极其活跃的一环。
4.  **微软密集布局视觉与编辑**：微软连续发布 **Mage-Flow** (文本到图像) 和 **Fara1.5-27B** (图像-文本到文本) 等多模态模型，其在计算机视觉和图像编辑领域的投入从“观察”转向“密集发布”。
5.  **独家与特色冷启动**：部分模型如 **empero-ai** 的 `Qwythos-9B-Claude-Mythos-5-1M-GGUF` 和 **conradlocke** 的 `krea2-identity-edit` 虽然发布日期短，但凭借独特的“混合”（Claude 数据蒸馏）或“身份保留编辑”概念，获得了极高的社区关注度。

---

### 🏆 热门模型分类

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)**  
  *作者: upstage | 👍 629 | 📥 3,761*
  一句话：Upstage 发布的 250B 级别开源大模型，作为参数规模最大的开源模型之一，是社区研究先进架构和直接使用强大基座模型的首选。

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)**  
  *作者: Nanbeige | 👍 493 | 📥 16,518*
  一句话：3B 参数的高效语言模型，主打“小模型、大能力”，适合资源受限设备或对推理速度有极致要求的场景。

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)**  
  *作者: Motif-Technologies | 👍 199 | 📥 2,532*
  一句话：新一代特征提取与文本生成模型，可能在 RAG 或语义检索领域有独特优化，是追踪前沿架构的焦点。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)**  
  *作者: moonshotai | 👍 6,191 | 📥 2,850*
  一句话：本周的“明星模型”，Kimi 的全新多模态版本，将强大的长文本理解与图像-文本联合推理能力结合，代表了国产多模态大模型的一流水准。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
  *作者: baidu | 👍 3,331 | 📥 2,645,773*
  一句话：百度出品的“全能”OCR 模型，下载量高达 260 万，是落地最成功、应用最广泛的模型之一，用于复杂场景的文本检测与识别。

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)**  
  *作者: thinkingmachines | 👍 1,603 | 📥 36,196*
  一句话：新一代对话式多模态模型，旨在提供更自然、更“人性化”的图文交互体验，是“AI 伴侣”类应用的代表。

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  *作者: zai-org | 👍 4,549 | 📥 1,003,547*
  一句话：智谱 AI 的最新 MoE 版本，百万下载量印证了其在中文社区的强大影响力，代表了国内对话模型顶尖水平。

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)**  
  *作者: microsoft | 👍 388 | 📥 1,691*
  一句话：微软推出的全新文本到图像生成模型，标志着其在图像生成领域的正式发力，效果值得期待。

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)**  
  *作者: owensong | 👍 223 | 📥 483*
  一句话：专为 CPU 和边缘设备打造的轻量级文本转语音模型，是边缘 AI 和本地部署语音应用的重要里程碑。

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)**  
  *作者: nvidia | 👍 133 | 📥 33,127*
  一句话：NVIDIA 最新发布的物理世界理解模型，可能用于机器人和自主系统，是“世界模型”赛道的重要选手。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)**  
  *作者: Kwaipilot | 👍 241 | 📥 5,312*
  一句话：基于 Qwen MoE 的代码生成模型，专注于提升代码生成和“图像-代码”的能力，是开发者的效率工具。

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)**  
  *作者: fdtn-ai | 👍 207 | 📥 6,421*
  一句话：主打安全性的 1B 级别代码或安全分析模型，在 AI 安全日益重要的今天，代表了专门的垂直方向。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)**  
  *作者: DavidAU | 👍 753 | 📥 634,146*
  一句话：社区“缝合怪”式微调的典范，通过复杂的名称和“无审查”标签吸引眼球，并提供了 GGUF 量化版本，方便用户直接使用。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  *作者: HauhauCS | 👍 3,134 | 📥 1,894,395*
  一句话：Qwen3.6 MoE 模型最受欢迎的“激进化”社区调优版本，190 万的下载量证明了社区对个性化风格微调的巨大需求。

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**  
  *作者: prism-ml | 👍 659 | 📥 2,257,928*
  一句话：1-bit 量化的 27B 模型，下载量超过 225 万，是极致压缩的代表。证明了在个人电脑上运行大语言模型是当前最热门的社区需求。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
  *作者: empero-ai | 👍 2,490 | 📥 1,336,263*
  一句话：使用“Claude”数据蒸馏的 Qwen 微调模型，不仅提供了量化版，更代表了“数据蒸馏”这一开源社区追赶闭源模型的全新策略。

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)**  
  *作者: conradlocke | 👍 555 | 📥 0*
  一句话：专为 Krea-2 模型设计的 LoRA，首次提出“身份编辑”概念，能保留人物身份进行图像编辑，极具创意。

---

### 🌐 生态信号

1.  **Qwen MoE 生态“一统江湖”**：Qwen3.6-35B-A3B 及其众多社区变体（GGUF、Uncensored、Aggressive）几乎占据了量化微调榜单的半壁江山。**Qwen**已成为当前开源社区最活跃的基座模型家族，其 MoE 架构的开放性极大地激发了社区二次创作。
2.  **开源“军备竞赛”下半场：量化与部署**：单点模型的性能提升已不再是唯一焦点。本周的生态信号表明，**如何让模型在个人电脑上跑起来**（Quantization量化）和**如何让模型变得更好用**（Fine-Tune微调）是社区的核心驱动力。1-bit 和 2-bit 量化模型的数百万下载量就是最好证明。
3.  **“无审查”与“角色扮演”的暗流涌动**：社区对“Uncensored”和特定风格（如“Mythos”、“Fable”）的微调版本需求极大，下载量远超原版。这提示我们，除了基础能力，模型的**价值对齐方式**和**响应风格**已成为决定其社区影响力的关键因素。
4.  **闭源“反哺”开源**：**empero-ai** 使用 Claude 数据蒸馏 Qwen 模型，本质上是在“汲取”闭源模型的智能来增强开源模型。这种“蒸馏-开源”模式可能会成为未来大模型生态发展的重要路径。

---

### 🔭 值得探索

1.  **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)**：如果你对 AI 图像编辑有兴趣，这个 “身份保留编辑” 的 LoRA 绝对值得一试。它代表了一种极其微妙的“定制化”能力，即模型需要“记住”谁是你，以及你想怎么改他/她。
2.  **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)**：如果你关注机器人、游戏或仿真，这个模型值得深入研究。它很可能代表了将 LLM/VLM 能力扩展到“物理世界理解”的最新前沿，对于构建智能体至关重要。
3.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：对于希望在消费级 GPU（甚至纯 CPU）上运行 27B 级别模型的开发者，这个 1-bit 量化模型是必试项目。它代表了当前量化的技术极限，体验一下在极致压缩下模型能保留多少“智能”。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*