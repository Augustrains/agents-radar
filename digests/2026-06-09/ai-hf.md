# Hugging Face 热门模型日报 2026-06-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-09 01:52 UTC

---

好的，我是 AI 模型生态分析师。以下是根据您提供的 2026-06-09 数据生成的《Hugging Face 热门模型日报》。

---

## Hugging Face 热门模型日报 | 2026-06-09

### 今日速览

本周 Hugging Face 生态呈现明显的“多模态与语言并进”格局。**DeepSeek-V4 系列**凭借其 Pro 和 Flash 版本的极致性能，继续霸占下载榜榜首，展现了开源通用大模型的绝对吸引力。NVIDIA 的 **LocateAnything-3B** 成为本周最大黑马，以突破性的定位能力席卷社区，点赞数力压群雄。与此同时，Google 的 **Gemma 4** 家族（包括官方版和社区量化版）形成了强大的矩阵效应，统治了多个榜单位置。此外，视频生成领域迎来新玩家，字节跳动的 **Bernini-R** 和社区模型的 **Sulphur-2** 系列增长迅猛，预示着一轮视频生成技术的爆发。

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

-   **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** (deepseek-ai) | 点赞: 4,722 | 下载: 5,399,597
    -   全球最热门的开源通用大模型之一，展现了顶尖的推理和对话能力，是本周无可争议的下载量冠军。
-   **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** (deepseek-ai) | 点赞: 1,448 | 下载: 3,262,529
    -   DeepSeek-V4 的快速蒸馏版本，在保持高性能的同时大幅提升推理速度，是追求效率的首选。
-   **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** (LiquidAI) | 点赞: 549 | 下载: 135,131
    -   Liquid AI 推出的 8B 参数 MoE 语言模型，仅激活 1B 参数即可达到卓越性能，是高效计算的典范。
-   **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** (JetBrains) | 点赞: 260 | 下载: 17,448
    -   JetBrains 发布的编程助手模型，专注于“思考”链，旨在提升代码生成和逻辑推理的准确性。
-   **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** (nvidia) | 点赞: 167 | 下载: 55,910
    -   NVIDIA 的旗舰级 MoE 语言模型，550B 参数、激活 55B，代表了当前开源模型的规模上限，为研究社区提供强大基座。
-   **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** (nvidia) | 点赞: 145 | 下载: 66,219
    -   上述模型的 4-bit NVFP4 量化版，旨在让这个超大规模模型能在更少的显卡上运行。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

-   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia) | 点赞: 1,621 | 下载: 121,594
    -   本周最大亮点，一个能通过文本指令在图像中精准定位任何物体的 3B 模型，开启了“万物定位”的新范式。
-   **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** (ideogram-ai) | 点赞: 393 | 下载: 5,495
    -   Ideogram 最新版图像生成模型的 8-bit FP8 量化版，以更低的资源消耗实现高质量的文本到图像生成。
-   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS) | 点赞: 1,554 | 下载: 3,036,465
    -   基于 Qwen3.6 的社区微调版 MoE 模型，主打“无审查”和激进的风格，获得了极高的下载量，反映了社区对多样化人格模型的需求。
-   **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** (SulphurAI) | 点赞: 1,601 | 下载: 1,707,062
    -   基于 Lightricks/LTX-2.3 的视频生成模型，本周下载量急剧攀升，是社区推动高质量开源视频生成的重要力量。
-   **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** (ByteDance) | 点赞: 185 | 下载: 278
    -   字节跳动发布的开源图像到视频生成模型，采用创新的渲染器架构，为视频生成领域注入新鲜血液。
-   **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** (stepfun-ai) | 点赞: 352 | 下载: 45,535
    -   阶跃星辰推出的多模态模型，支持图像和文本输入，具备强大的视觉语言理解能力。
-   **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** (google) | 点赞: 151 | 下载: 17,531
    -   Google 更新了其音乐生成模型，主打实时交互，为创意工具和AI音乐创作提供新的可能性。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

-   **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** (sapientinc) | 点赞: 728 | 下载: 163,953
    -   一款专注于人力资源领域的 1B 参数文本生成模型，专为招聘、面试等场景设计，代表了垂直领域模型的崛起。
-   **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** (PaddlePaddle) | 点赞: 277 | 下载: 9,924
    -   百度飞桨推出的视觉语言OCR模型，整合了 ERNIE 4.5 的能力，专攻复杂场景下的文字识别与理解。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

-   **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** (unsloth) | 点赞: 503 | 下载: 645,263
    -   由 Unsloth 团队对 Google Gemma 4 指令版进行的 GGUF 量化，极大地降低了部署门槛，是推动大模型普及的关键力量。
-   **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** (unsloth) | 点赞: 147 | 下载: 121,399
    -   同样是 Unsloth 对 Gemma 4 的量化版，采用了 QAT (量化感知训练) 技术，理论上能获得更优的量化性能。
-   **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** (unsloth) | 点赞: 696 | 下载: 1,186,648
    -   Unsloth 对阿里 Qwen3.6 27B 模型的 GGUF 量化版，结合了 MoE 和 MTP (多头预测) 技术，在效率和生成质量上取得了平衡。
-   **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** (google) | 点赞: 99 | 下载: 52,386
    -   Google 官方发布的 Gemma 4 QAT 量化版，表明官方也正在积极推进模型的部署友好性。

### 生态信号

本周的模型生态呈现以下三大趋势：

1.  **模型家族化竞争加剧**：**DeepSeek-V4 系列**、**Google Gemma 4 系列**和 **NVIDIA Nemotron 系列**已形成完整的梯次配置，从千亿级旗舰到量化轻量版一应俱全。这种“全家桶”策略能覆盖从研究到部署的全链路需求，是头部玩家的标准打法。其中，**Gemma 4** 的社区量化活动尤其活跃，显示出强大的生态影响力。
2.  **视频生成进入“开源爆发前夜”**：字节跳动和SulphurAI等团队的开源视频模型，虽然尚处早期，但获得了极高的社区关注度。这表明继文本和图像之后，视频生成正成为下一个开源社区争夺的制高点，社区对高质量、易部署的视频模型充满渴望。
3.  **“小而美”的专用模型与“巨无霸”并行**：本周既有 550B 参数的巨型 MoE，也有 1B 参数的专用 HRM 模型和 3B 参数的定位模型。这证明生态正从“通用大模型霸权”向“通用+专用”的二元结构演进。NVIDIA的**LocateAnything-3B** 的成功，正是这种“专用小模型”在特定任务上做到极致，从而获得巨大关注的典型案例。

### 值得探索

1.  **nvidia/LocateAnything-3B**: 强烈推荐！它代表了一种全新的“看+找”范式，突破了传统目标检测的类别限制，为机器人、自动驾驶、图像编辑等下游任务提供了颠覆性的能力。
2.  **deepseek-ai/DeepSeek-V4-Pro**: 如果你的目标是寻找当前开源社区中最强大、最全面的通用大模型，这是你的不二之选。它不仅在榜单上独占鳌头，更是社区共识的顶级模型。
3.  **SulphurAI/Sulphur-2-base**: 值得关注的视频生成新星。它基于社区优化过的基座，下载量激增说明其生成效果已获得广泛认可。跟踪此模型可以洞察开源视频生成的技术进展和社区偏好。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*