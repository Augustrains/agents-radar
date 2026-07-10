# Hugging Face 热门模型日报 2026-07-10

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-10 01:27 UTC

---

好的，作为AI模型生态分析师，以下为您呈上基于2026年7月10日数据生成的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 (2026-07-10)

#### 今日速览

本周Hugging Face模型生态呈现出显著的“MoE（混合专家）架构”与“多模态”双轮驱动趋势。腾讯与智谱分别推出了基于MoE的旗舰大模型 **Hy3** 和 **GLM-5.2**，展示了中国团队在高效架构上的突破。同时，以**Qwen3.5/3.6**系列为基座的社区微调模型（如 **Qwythos-9B**）和量化版本（如 **unsloth Qwen3.6-27B-MTP-GGUF**）下载量惊人，说明社区对“即用型”高性能推理模型的渴求。此外，英伟达的 **LocateAnything-3B** 与百度的 **Unlimited-OCR** 在特定任务上的成功，标志着多模态AI正从通用走向专业细分。

#### 热门模型

##### 🧠 语言模型 (LLM, 对话模型, 指令微调)

*   **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** by tencent | 👍 612 | ⬇️ 5,572
    *   腾讯发布的全新MoE架构大模型，在HF上正式开源权重，代表了国内顶尖团队的模型能力。

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** by zai-org | 👍 3,728 | ⬇️ 362,300
    *   智谱AI新一代MoE对话模型，以极高点赞数登顶，证明了其在中文对话场景下的强大实力与社区认可度。

*   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** by InternScience | 👍 434 | ⬇️ 23,112
    *   基于Qwen3.5 MoE架构打造的Agent专用模型，旨在提升模型的工具调用与任务规划能力。

*   **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** by meituan-longcat | 👍 165 | ⬇️ 1,107
    *   美团发布的长上下文对话模型，专注于处理超长文本输入，满足复杂业务需求。

*   **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** by mistralai | 👍 179 | ⬇️ 258
    *   Mistral AI的旗舰级MoE模型Leanstral的更新版本，通过稀疏激活（119B参数仅激活6B）实现高性能与高效率。

*   **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** by google | 👍 330 | ⬇️ 16,374
    *   谷歌发布的基础模型，专为表格数据的分类与回归任务设计，具备零样本泛化能力，开辟了LLM之外的新战场。

*   **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** by deepseek-ai | 👍 457 | ⬇️ 29,230
    *   深度求索最新旗舰模型V4的Pro版本，作为开源社区的先驱，其每一次发布都备受瞩目。

*   **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** by nvidia | 👍 85 | ⬇️ 16,959
    *   英伟达在专用推理模型上的探索，通过“拼图”等逻辑任务进行训练，并采用自研NVFP4量化技术，旨在极致压缩模型体积。

*   **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** by nvidia | 👍 82 | ⬇️ 436
    *   英伟达Nemotron系列的又一力作，专注于音频理解任务，标志着其多模态布局的深化。

##### 🎨 多模态与生成 (图像、视频、音频、文本到X)

*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** by nvidia | 👍 2,687 | ⬇️ 1,447,244
    *   英伟达推出的零样本目标定位模型，无需微调即可指向并检测任何物体，精准切中市场痛点。

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** by baidu | 👍 1,903 | ⬇️ 1,246,042
    *   百度推出的通用OCR模型，号称解决长文本、复杂版面的识别问题，高下载量体现了其在真实场景中的实用性。

*   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** by krea | 👍 569 | ⬇️ 157,302
    *   Krea推出的第二代图像生成模型的加速版本，通过技术优化实现更快的生成速度，受到创意工作者追捧。

*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** by HauhauCS | 👍 2,595 | ⬇️ 2,716,428
    *   基于Qwen3.6的“无审查”微调版视觉MoE模型，高下载量反映了社区对模型“越狱”和激进风格化输出的强烈需求。

*   **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** by conradlocke | 👍 132 | ⬇️ 0
    *   基于Krea-2的LoRA模型，专注于在不改变主体身份的前提下进行图像编辑，是人像修正领域的实用工具。

*   **[Patil/Krea-2-depth-controlnet](https://huggingface.co/Patil/Krea-2-depth-controlnet)** by Patil | 👍 83 | ⬇️ 0
    *   为Krea-2图像生成模型附加深度控制网络，允许用户通过深度图精确控制生成图像的几何结构。

*   **[eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)** by eric-venti-seeds | 👍 123 | ⬇️ 0
    *   针对Flux模型开发的LoRA，允许用户精确控制图像中的光照方向，提升了AI图像生成的写实度和艺术控制力。

##### 🔧 专用模型 (代码、数学、医疗、嵌入)

*   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** by yuxinlu1 | 👍 2,670 | ⬇️ 703,735
    *   基于Gemma-4微调的高性能代码生成模型，其GGUF量化版获得了极高的点赞与下载，说明了开发者社区对代码辅助工具的依赖。

*   **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** by yuxinlu1 | 👍 1,117 | ⬇️ 418,171
    *   同样基于Gemma-4，但专为Agent（智能体）场景微调，展现了模型从“生成代码”到“自主执行任务”的能力进化。

##### 📦 微调与量化 (社区微调、GGUF、AWQ)

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** by empero-ai | 👍 1,930 | ⬇️ 1,875,602
    *   基于Qwen3.5的高质量社区微调模型，本版本为GGUF量化格式，极适合本地部署，是融合了“开源模型+闭源数据蒸馏”思路的代表作。

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** by empero-ai | 👍 748 | ⬇️ 179,378
    *   上一个模型的原版权重，未量化版本，同样表现抢眼。

*   **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** by deepreinforce-ai | 👍 820 | ⬇️ 957,721
    *   一个全新的35B模型，其GGUF量化版本发布后迅速走红，下载量巨大，暗示了模型本身的强大性能。

*   **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** by unsloth | 👍 1,025 | ⬇️ 2,894,918
    *   知名量化与微调工具团队Unsloth对Qwen3.6-27B的GGUF版本，下载量接近300万，是社区最受欢迎的“现成”量化模型之一。

*   **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** by nvidia | 👍 332 | ⬇️ 748,054
    *   英伟达官方使用其自研ModelOpt工具对Qwen3.6进行的4-bit浮点量化版本，旨在推动其在自家硬件上的部署效率。

*   **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** by GnLOLot | 👍 142 | ⬇️ 2,239
    *   对小模型（1B）进行推理能力微调并量化的尝试，旨在将高级思维链能力压缩至边缘设备。

#### 生态信号

*   **模型家族格局**：**Qwen 3.x 系列**依旧是当前生态的绝对中坚力量，从Qwen3.5到3.6，衍生出大量微调与量化版本。**GLM-5.2** 和 **Hy3** 的崛起，尤其是MoE架构的采用，标志着国产大模型生态的进一步成熟。**Gemma-4** 在代码与Agent领域的微调表现亮眼，正成为开发者青睐的基础模型。

*   **开源 vs 闭源**：本周热门榜单中，权重完全开源的模型（如Qwen系列，GLM，Gemma）占据了压倒性优势。闭源模型的“蒸馏”产物（如Qwythos系列）成为社区热点，表明“用强闭源模型教开源模型”是当前提升模型能力的有效路径。英伟达的积极开源也巩固了其在基础设施和模型优化方面的领导地位。

*   **量化与微调活动**：**GGUF**格式的模型下载量遥遥领先，验证了本地部署与PC端推理的巨大市场需求。**MoE**架构的量化和微调（如对Qwen3.x MoE模型进行的社区调教）是当前技术热点，如何在稀疏激活模型上进行高效的参数高效微调（PEFT）成为新课题。**Unsloth** 等工具链团队在生态中的重要性日益凸显。

#### 值得探索

1.  **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**: 作为腾讯最新MoE旗舰的开源版本，其性能与架构设计细节值得技术团队深入研究，代表了前沿的工业级技术方向。

2.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**: 精准解决了计算机视觉中的“找物体”这一高频需求，其零样本能力使其在机器人、自动驾驶和工业检测领域具有巨大应用潜力。

3.  **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**: 下载量接近300万的社区量化标杆，对于希望在个人电脑上部署顶级LLM的用户来说，这是当前性价比最高的选择之一，其性能表现是评估当前量化技术水平的绝佳样本。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*