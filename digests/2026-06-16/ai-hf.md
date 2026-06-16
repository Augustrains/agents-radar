# Hugging Face 热门模型日报 2026-06-16

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-16 02:32 UTC

---

好的，作为AI模型生态分析师，以下是为您整理的2026年6月16日《Hugging Face 热门模型日报》。

---

## Hugging Face 热门模型日报 | 2026-06-16

### 1. 今日速览

本周Hugging Face生态热度持续飙升，DeepSeek-V4-Pro凭借近5000点赞量断层领先，刷新了开源大模型的热度纪录。**多模态（尤其是image-text-to-text）模型**成为绝对主流，榜单前十中占据七席，标志着AI进入“看、听、说”的全能时代。**MoE架构**和**GGUF量化格式**成为社区最活跃的两大杠杆，前者驱动模型性能跃升，后者则极大地降低了模型的部署门槛。与此同时，以“Uncensored”和“Aggressive”命名的社区微调模型暗示了用户对模型自由度属性的强烈需求。

### 2. 热门模型分类

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** | 作者: deepseek-ai | 👍 4,866 | ⬇️ 2,934,763
  - **一句话说明**：DeepSeek最新旗舰版对话模型，以绝对热度和海量下载量登顶榜首，代表了当前开源语言模型的顶级水准。
- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)** | 作者: prefeitura-rio | 👍 303 | ⬇️ 188,723
  - **一句话说明**：基于Qwen3.5的397B超大MoE模型，开源社区对超大规模模型的探索热情不减。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** | 作者: google | 👍 882 | ⬇️ 311,788
  - **一句话说明**：Google推出的26B混合专家扩散模型，将文本理解与图像生成能力融合，是“多模态对话”的先锋。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | 作者: nvidia | 👍 2,056 | ⬇️ 86,968
  - **一句话说明**：NVIDIA推出的3B参数通用物体定位模型，精准切中视觉理解与交互的刚需，点赞量极高。
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** | 作者: google | 👍 1,034 | ⬇️ 1,160,435
  - **一句话说明**：Gemma系列首次支持“任意输入到任意输出”（any-to-any），标志着小模型向全能形态的进化。
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** | 作者: ideogram-ai | 👍 547 | ⬇️ 10,748
  - **一句话说明**：图片生成领域明星模型的最新版本，采用FP8量化，兼顾生成质量与效率。
- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** | 作者: zai-org | 👍 190 | ⬇️ 0
  - **一句话说明**：专注于角色动画的“图像到视频”模型，虽下载量为0但点赞数高，表明社区对该赛道的关注已提前到来。
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** | 作者: bosonai | 👍 445 | ⬇️ 38,429
  - **一句话说明**：基于Qwen3的多模态语音合成模型，4B参数实现高质量文本转语音，音频AI赛道势头强劲。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | 作者: nvidia | 👍 422 | ⬇️ 5,200
  - **一句话说明**：NVIDIA推出的流式语音识别模型，针对低延迟场景优化，是边缘端AI应用的重要拼图。
- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)** | 作者: Zyphra | 👍 90 | ⬇️ 414
  - **一句话说明**：一个新兴的文本转语音模型，正在社区中积累口碑。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | 作者: moonshotai | 👍 746 | ⬇️ 56,750
  - **一句话说明**：月之暗面推出的代码专用模型，采用压缩张量技术，专注提升代码生成与理解能力。
- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** | 作者: CohereLabs | 👍 389 | ⬇️ 11,145
  - **一句话说明**：Cohere出品的轻量级代码生成模型，属于其MoE系列，针对开发场景优化。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 1,854 | ⬇️ 2,697,882
  - **一句话说明**：社区基于Qwen3.6的极致微调版本，下载量近270万，反映了对“无审查”和特定风格的强烈需求。
- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** | 作者: unsloth | 👍 276 | ⬇️ 107,243
  - **一句话说明**：unsloth团队将谷歌最新的扩散Gemma模型量化为GGUF格式，大幅降低其部署门槛。
- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** | 作者: unsloth | 👍 617 | ⬇️ 980,781
  - **一句话说明**：Gemma-4的GGUF版本，下载量逼近百万，是最受欢迎的开源模型量化版本之一。
- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** | 作者: DavidAU | 👍 356 | ⬇️ 369,526
  - **一句话说明**：当前社区“炼丹”文化的极致体现，集各种前沿技术和风格于一身的超级微调模型，追求极致性能与自由度。

### 3. 生态信号

- **模型家族势头**：**Qwen系列**及其分支（Qwen3.5/3.6）成为社区最活跃的“底盘”，被广泛用于二次微调和量化。**Gemma家族**（DiffusionGemma、Gemma-4）则代表了Google在通用和多模态领域的强大号召力。**DeepSeek-V4**证明其在LLM赛道的顶尖地位。
- **开源 vs 闭源**：开源权重模型主导了整个榜单。社区微调模型（尤其是“uncensored”版本）拥有极高的下载量，表明用户对模型的可控性和定制化有强烈诉求，而不仅仅是“最强”的通用模型。
- **量化与微调活动**：**GGUF量化**是当前生态中最核心的基础设施，几乎每个主流模型都会紧随其后被量化。以`unsloth`为代表的团队，扮演了连接“大模型”与“普通开发者”的桥梁角色。**MoE**架构的模型因参数量与激活量的平衡优势，成为微调和社区二创的热门对象。

### 4. 值得探索

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：该模型不仅仅是定位，其背后代表的是视觉AI的“万物皆可指”能力。仅3B参数使其在边缘设备部署成为可能，是研究视觉理解、人机交互和RPA自动化的绝佳起点。
2.  **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**：作为将扩散模型与大型语言模型深度结合的产物，它模糊了文本生成与图像生成的边界。研究它可以洞察下一代混合AI模型的设计思路。
3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**：虽然名字听起来很“狂野”，但其近300万的下载量是巨大的信号。这个模型是社区对“模型个性”和“无限制创造力”需求的最佳代表，深入了解其对理解开源社区未来生态至关重要。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*