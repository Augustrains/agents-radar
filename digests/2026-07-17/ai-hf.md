# Hugging Face 热门模型日报 2026-07-17

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-17 01:22 UTC

---

好的，这是为您准备的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月17日**

#### **今日速览**

今日Hugging Face社区呈现出明显的多模态与极致量化两大趋势。腾讯的 **Hy3** 和智谱的 **GLM-5.2** 作为重磅基础模型获得了极高的关注。与此同时，以 **prism-ml** 和 **empero-ai** 为代表的社区成员，正通过1-bit、2-bit等极端量化技术，以及GGUF通用格式，将大模型部署到本地设备，其中 **Qwythos-9B** 和 **Bonsai-27B** 系列下载量惊人。此外，针对特定任务的模型如OCR和Agent也开始崭露头角。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

-   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
    -   作者：zai-org | 点赞：4,029 | 下载：513,061
    -   一句话说明：智谱AI推出的新一代MoE大语言模型，凭借其强大的通用能力，成为本周点赞数最高的原生权重模型。

-   **[tencent/Hy3](https://huggingface.co/tencent/Hugging Face/models/tencent/Hy3)**
    -   作者：tencent | 点赞：813 | 下载：11,849
    -   一句话说明：腾讯混元系列的最新版本，作为大型基础模型，在社区中引发了广泛关注，代表了国内大厂的持续投入。

-   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**
    -   作者：InternScience | 点赞：566 | 下载：33,400
    -   一句话说明：基于Qwen架构的MoE Agent模型，专为智能体任务优化，显示了Agent模型领域的细分趋势。

-   **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**
    -   作者：yuxinlu1 | 点赞：1,207 | 下载：506,068
    -   一句话说明：基于Google Gemma-4的社区微调版本，专注于Agent和编码能力，下载量很高，显示了Gemma家族的生态活力。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

-   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
    -   作者：empero-ai | 点赞：2,235 | 下载：2,042,670
    -   一句话说明：基于Qwen的视觉语言模型的量化版，结合了推理能力，因其强大的本地多模态能力成为本周下载量最高的模型之一。

-   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    -   作者：HauhauCS | 点赞：2,787 | 下载：2,328,315
    -   一句话说明：一款基于Qwen 3.6的“无审查”MoE视觉模型，因其激进风格和高下载量，成为社区关注的焦点。

-   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
    -   作者：baidu | 点赞：2,010 | 下载：1,852,722
    -   一句话说明：百度推出的通用OCR模型，在图像文本识别任务上表现出色，证明了强大的基础视觉模型在垂直任务上的巨大潜力。

-   **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)**
    -   作者：Wan-AI | 点赞：92 | 下载：1,884
    -   一句话说明：专注于图生视频的舞蹈生成模型，展示了在特定、创意视频生成领域的模型精细化趋势。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

-   **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)**
    -   作者：ATH-MaaS | 点赞：136 | 下载：3,678
    -   一句话说明：另一个专注OCR的专用模型，结合Qwen架构，表明“大模型+垂域微调”是提升特定任务性能的有效路径。

-   **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)**
    -   作者：Cactus-Compute | 点赞：248 | 下载：733
    -   一句话说明：专注于函数调用和工具使用能力的模型，代表了“模型即API”的发展方向，是构建智能Agent的核心组件。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

-   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**
    -   作者：prism-ml | 点赞：601 | 下载：74,007
    -   一句话说明：采用了创新的“三元（Ternary）”量化技术的27B模型，只需2-bit精度，代表了在极端压缩领域的探索。

-   **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**
    -   作者：prism-ml | 点赞：340 | 下载：559,267
    -   一句话说明：将27B模型压缩至1-bit的GGUF版本，是极致量化的代表作，尽管精度损失，但极大地降低了部署门槛。

-   **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)**
    -   作者：unsloth | 点赞：216 | 下载：1,712,974
    -   一句话说明：利用NVIDIA的FP4精度进行量化的模型，结合高效的微调库，旨在保持性能的同时大幅提升推理速度。

#### **生态信号**

本周生态呈现出两个核心信号：**1. 国产模型阵营强势崛起**：以**Qwen**（及其衍生的Qwythos、Bonsai）和**GLM**系列为代表，形成了从基础权重（GLM-5.2、Hy3）到社区量化（GGUF、MLX）的完整生态链，展现了强大的社区影响力。**2. 量化技术进入“狂飙”时代**：从1-bit到2-bit，再到NVFP4，社区对本地化、轻量级部署的追求几乎达到了极致。**prism-ml**的“三元”量化与**empero-ai**的大体量多模态量化模型，是这种趋势的代表。此外，**Agent**和**OCR**等专用模型的涌现，也表明社区不再满足于通用模型，而是开始为特定场景“精雕细琢”。

#### **值得探索**

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：作为点赞数最高的原生模型，直接体验其最新的MoE架构和对话能力，是理解当前国产大模型技术前沿的最佳入口。
2.  **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**：下载量超200万，它是多模态模型本地化部署的典范。在自己的设备上运行一个具备强大多模态和推理能力的模型，极具实践价值。
3.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**：如果你想了解模型量化的极限在哪里，这个2-bit模型值得一试。它代表了用极致压缩换取本地可运行性的前沿探索。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*