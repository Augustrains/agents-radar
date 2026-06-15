# Hugging Face 热门模型日报 2026-06-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-15 02:29 UTC

---

好的，作为AI模型生态分析师，以下是为您整理的2026年6月15日《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-15**

#### **今日速览**

本周Hugging Face社区的热度被**DeepSeek-V4-Pro**的正式发布引爆，其以绝对优势登顶周榜。多模态模型依然是绝对主流，**Gemma 4** 和 **Qwen 3.6** 系列衍生出大量社区微调与量化版本，生态极为活跃。在应用侧，**NVIDIA** 的定位模型和 **Ideogram 4** 的图像生成模型也获得了大量关注。值得注意的是，部分“无审查”微调模型下载量巨大，反映了社区对模型自由度的强烈需求。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
    *   **作者**：deepseek-ai
    *   **点赞**：4,834 | **下载**：3,075,369
    *   **说明**：DeepSeek 最新旗舰模型，功能强大的对话模型，凭借其顶尖的性能和开放性，成为本周社区讨论的绝对焦点。

*   **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**
    *   **作者**：prefeitura-rio
    *   **点赞**：275 | **下载**：112,371
    *   **说明**：一个基于Qwen 3.5 MoE架构的397B超大参数开源模型，虽然作者背景奇特，但其巨大的参数量引发了行业对超大MoE模型开源潜力的讨论。

*   **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**
    *   **作者**：nex-agi
    *   **点赞**：259 | **下载**：3,396
    *   **说明**：基于Qwen 3.5 MoE架构的文本生成模型，定位为专业版，显示出社区对高端MoE模型的持续需求。

*   **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)**
    *   **作者**：nex-agi
    *   **点赞**：211 | **下载**：7,010
    *   **说明**：与Nex-N2-Pro同系列的轻量版，为资源受限环境提供了高性能替代方案。

*   **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)**
    *   **作者**：XiaomiMiMo
    *   **点赞**：113 | **下载**：4,108
    *   **说明**：小米推出的Agent专用模型，主打FP4量化与“DFlash”技术，体现了硬件厂商在端侧Agent部署的探索。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    *   **作者**：HauhauCS
    *   **点赞**：1,808 | **下载**：2,516,709
    *   **说明**：基于Qwen3.6的35B MoE“无审查”视觉模型，下载量惊人，反映出社区对开源、高性能且无限制多模态模型的巨大渴望。

*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    *   **作者**：nvidia
    *   **点赞**：2,004 | **下载**：75,201
    *   **说明**：NVIDIA推出的通用定位模型，能根据文本或图像指令在图片中定位任何物体。精准且轻量，是计算机视觉领域的实用工具。

*   **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**
    *   **作者**：google
    *   **点赞**：800 | **下载**：198,912
    *   **说明**：Google发布的旨在统一扩散模型与LLM的新架构，具备图像理解与生成能力，代表了未来多模态模型的一个研究方向。

*   **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**
    *   **作者**：bosonai
    *   **点赞**：427 | **下载**：35,122
    *   **说明**：4B参数的TTS模型，在语音合成领域获得关注，表明高质量、轻量化的语音模型依然是热门需求。

*   **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**
    *   **作者**：zai-org
    *   **点赞**：175 | **下载**：0
    *   **说明**：一个基于姿态驱动的角色动画视频生成模型，虽然下载量为0，但作为新兴研究方向的上榜值得关注。

*   **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**
    *   **作者**：ideogram-ai
    *   **点赞**：535 | **下载**：8,263
    *   **说明**：Ideogram 4 的FP8量化版本，在性能和显存占用间取得平衡，推动了高质量文生图模型的普及。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**
    *   **作者**：moonshotai
    *   **点赞**：635 | **下载**：15,145
    *   **说明**：月之暗面推出的Kimi K2.7代码版，专注于代码生成和理解任务，延续了Kimi家族在长文本和代码领域的优势。

*   **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**
    *   **作者**：CohereLabs
    *   **点赞**：369 | **下载**：9,932
    *   **说明**：Cohere的“North”系列代码专用小型MoE模型，旨在为企业提供高效、专业的代码辅助能力。

*   **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**
    *   **作者**：nvidia
    *   **点赞**：412 | **下载**：4,505
    *   **说明**：NVidia的流式语音识别模型，主打低延迟和缓存感知技术，是实时语音交互应用的重要基础设施。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**
    *   **作者**：DavidAU
    *   **点赞**：337 | **下载**：375,966
    *   **说明**：一个名字极长的“缝合怪”微调模型，融合了多种前沿技术，其高下载量体现了社区对“堆料”微调模型的兴趣。

*   **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**
    *   **作者**：Jackrong
    *   **点赞**：182 | **下载**：33,720
    *   **说明**：Qwen 3.6 的27B代码专用GGUF量化版，为本地部署高性能代码助手提供了优化解决方案。

*   **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
    *   **作者**：unsloth
    *   **点赞**：598 | **下载**：926,372
    *   **说明**：Unsloth 版本的 Gemma-4-12B GGUF，以其高效的量化技术和用户体验，成为社区下载量最高的 Gemma 4 衍生模型。

---

#### **生态信号**

本周生态呈现三大信号：**一是“DeepSeek-V4-Pro”一家独大**，其超高的点赞与下载量宣告了闭源API之外的又一强大开源选择，或将重塑行业格局。**二是“Gemma 4”与“Qwen 3.6”双雄争霸**，两者都催生了庞大的微调（如DavidAU的“缝合怪”）和量化（如Unsloth、Jackrong）生态，显示出社区对顶尖基础模型的深度定制需求。**三是“无审查”微调模型持续火爆**，以HauhauCS和DavidAU的模型为代表，下载量甚至超过官方版本，表明在学术研究和个性化应用中，去除内容限制是许多发烧友用户的刚需。

---

#### **值得探索**

1.  **DeepSeek-V4-Pro**：毫无疑问是本周期最值得研究的模型。你可将其作为通用对话或代码助手的基线，评估其相较于闭源模型（如GPT、Claude）的实际表现。
2.  **nvidia/LocateAnything-3B**：这是一个非常实用的工具。尝试将其集成到你的图像分析pipeline中，它的精准定位能力可以极大地简化诸如目标检测、视觉问答等任务的难度。
3.  **zai-org/SCAIL-2**：尽管是预览版，但它代表了视频生成领域一个有趣的方向（姿态驱动）。如果你关注角色动画或可控视频生成，这个模型值得入手尝试。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*