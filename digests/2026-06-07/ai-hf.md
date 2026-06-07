# Hugging Face 热门模型日报 2026-06-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-07 02:10 UTC

---

好的，作为AI模型生态分析师，以下是为您整理的《Hugging Face 热门模型日报》。

---

## Hugging Face 热门模型日报 (2026-06-07)

### 今日速览

本周 Hugging Face 榜单呈现出两大核心趋势：其一，**多模态与“any-to-any”全能模型成为绝对主流**，以NVIDIA和Google为代表，多个能同时处理文本、图像、音频等多种模态的模型霸榜；其二，**开源社区的微调与量化活动异常活跃**，特别是针对DeepSeek、Qwen等强大基座模型的无审查版本和GGUF量化版下载量极高，展现了社区对高性能、本地化运行模型的渴求。

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

-   **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
    -   **作者:** deepseek-ai | **点赞:** 4,681 | **下载:** 5,510,611
    -   **一句话:** DeepSeek最新旗舰级文本生成模型，凭借破纪录的点赞和下载量成为本周最受关注的模型，代表了当前开源大模型的顶尖水平。

-   **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**
    -   **作者:** sapientinc | **点赞:** 712 | **下载:** 161,627
    -   **一句话:** 一个专注于人力资源（HRM）领域的专用文本生成模型，展示了垂直领域专用LLM正获得社区的认可。

-   **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-8B-A1B)**
    -   **作者:** LiquidAI | **点赞:** 533 | **下载:** 95,440
    -   **一句话:** Liquid AI推出的MoE架构语言模型，以较小的总参数量（8B）和活跃参数（1B）实现了高效推理，是“小模型大能力”趋势的代表。

-   **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**
    -   **作者:** openbmb | **点赞:** 775 | **下载:** 100,575
    -   **一句话:** 一个仅有1B参数的小型语言模型，在资源受限设备上部署的潜力使其在社区中热度很高。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

-   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    -   **作者:** nvidia | **点赞:** 1,456 | **下载:** 111,078
    -   **一句话:** NVIDIA的“定位万物”模型，能够根据文本指令在图像中精准定位任何目标，极大拓展了多模态模型在CV领域的实用性。

-   **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**
    -   **作者:** google | **点赞:** 618 | **下载:** 315,131
    -   **一句话:** Google最新的“any-to-any”全能模型Gemma-4的指令微调版，标志着全能型多模态模型成为新的竞赛焦点。

-   **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**
    -   **作者:** stepfun-ai | **点赞:** 342 | **下载:** 38,716
    -   **一句话:** 阶跃星辰推出的视觉语言模型，聚焦于高效的图像理解和文本生成，是中国AI模型社区在全球舞台上的重要参与者。

-   **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**
    -   **作者:** ByteDance | **点赞:** 150 | **下载:** 223
    -   **一句话:** 字节跳动提出的图像-文本到视频生成模型，专注于图像渲染和视频生成，是文生视频领域的新探索。

-   **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**
    -   **作者:** SulphurAI | **点赞:** 1,581 | **下载:** 1,704,964
    -   **一句话:** 基于Lightricks模型微调的视频生成模型，下载量极高，反映了社区对高质量视频生成基座模型的强劲需求。

-   **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)**
    -   **作者:** nvidia | **点赞:** 145 | **下载:** 47,285
    -   **一句话:** NVIDIA的超级大模型，拥有550B总参数量，是当前开源社区中规模最大的模型之一，主要面向顶尖的文本生成研究。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

-   *(本周榜单中未出现典型的代码、数学或嵌入模型，多模态与通用文本模型占据主导。)*

#### 📦 微调与量化（社区微调、GGUF、AWQ）

-   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    -   **作者:** HauhauCS | **点赞:** 1,488 | **下载:** 2,771,843
    -   **一句话:** 对Qwen3.6的社区无审查微调版，下载量惊人，表明用户对突破内容限制、寻求特定风格（“Aggressive”）的模型有巨大需求。

-   **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
    -   **作者:** unsloth | **点赞:** 422 | **下载:** 458,174
    -   **一句话:** 通过Unsloth工具对Gemma-4进行GGUF量化，极大降低了运行门槛，是社区量化活动火热的直接证明。

-   **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**
    -   **作者:** nvidia | **点赞:** 198 | **下载:** 1,015,381
    -   **一句话:** NVIDIA对Qwen3.6 MoE模型进行的4-bit浮点量化版，专为其硬件优化，展示了硬件厂商如何通过模型优化来推广自家生态。

### 生态信号

-   **MoE与全能模型成为主流：** 无论是NVIDIA（Nemotron、Qwen3.6变体）、DeepSeek（V4）还是Google（Gemma-4），混合专家模型（MoE）架构已全面应用于顶级模型中。同时，“any-to-any”的全能多模态模型正快速取代单一任务模型，成为新的技术标杆。
-   **开源生态空前繁荣：** DeepSeek-V4和NVIDIA的多个大模型都采用开源或开放权重策略，与闭源模型（如OpenAI的GPT系列）形成激烈竞争。社区微调（如无审查版本）和量化（GGUF、NVFP4）活动异常活跃，开源模型从“能用”向“好用、易用、定制化”迈进。
-   **硬件与模型的深度耦合：** NVIDIA大量发布针对自家硬件的优化模型（如NVFP4量化版），深刻影响着模型的分发和使用方式。这预示着未来模型生态将与特定硬件平台结合得更加紧密。

### 值得探索

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B):** 强烈推荐。它在“目标定位”这一细分多模态任务上表现惊艳，实用性极强，是探索视觉NLP应用的绝佳起点。
2.  **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base):** 值得研究。其基于强大基座模型（Lightricks/LTX-2.3）进行微调的策略，以及它背后开源文本到视频模型的最新进展，都极具参考价值。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*