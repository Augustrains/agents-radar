# Hugging Face 热门模型日报 2026-07-01

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-01 02:07 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026-07-01 Hugging Face热门模型数据生成的日报。

---

# 🤗 Hugging Face 热门模型日报 (2026-07-01)

## 📰 今日速览

本周 Hugging Face 生态呈现出 **“开源巨头齐发力，社区微调百花齐放”** 的繁荣景象。**DeepSeek V4 和 GLM-5.2** 作为新一代基础模型，其官方版本及衍生量化版、优化版均获得了极高关注，标志着 MoE 架构在开源社区的进一步成熟。**NVIDIA** 凭借其 NVFP4 量化技术，成为推动大型模型（如 Qwen3.6-35B-A3B）本地化部署的关键力量。值得注意的是，**Krea** 和 **LTX** 等专业领域模型（图像生成、视频生成）也在榜单中占据一席之地，显示出多模态赛道的持续升温。此外，**“abliterated”**（去限制）等社区魔改版本的热度，预示着用户对于模型可控性与安全性边界的探索仍在继续。

## 🔥 热门模型分类整理

### 🧠 语言模型（LLM、对话模型、指令微调）

-   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 👍 3,061 | ⬇️ 142,547
    -   **说明**：GLM系列的最新MoE架构模型，凭借其强大的对话与推理能力，成为本周关注度最高的模型之一，代表了开源MoE中文模型的顶尖水平。
-   **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** | 作者: deepseek-ai | 👍 251 | ⬇️ 6,939
    -   **说明**：DeepSeek V4的官方Pro版本，专注于极致性能与研究突破（附有arXiv论文），是顶尖开源学术模型的代表。
-   **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** | 作者: nvidia | 👍 95 | ⬇️ 58
    -   **说明**：英伟达基于Qwen3.6-27B进行NVFP4量化的版本，在保持模型能力的同时大幅降低部署门槛，展示了硬件厂商推动模型可及性的策略。

### 🎨 多模态与生成（图像、视频、文本到X）

-   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者: baidu | 👍 1,497 | ⬇️ 429,056
    -   **说明**：百度推出的通用OCR模型（image-text-to-text），凭借极高的下载量与点赞比，成为本周当之无愧的“明星”，体现了市场对顶级的、场景无关的文字识别模型有着巨大刚需。
-   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** | 作者: krea | 👍 421 | ⬇️ 45,668
    -   **说明**：Krea团队推出的文本到图像生成模型，作为Krea-2的加速版（Turbo），满足了社区对高质量、高效率图像生成的需求。
-   **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** | 作者: fal | 👍 128 | ⬇️ 0
    -   **说明**：fal.ai发布的图像到视频LoRA，专注于生成3D真实感视频，虽然刚发布下载量为零，但其独特的任务定位预示了视频生成领域的新方向。

### 🔧 专用模型（代码、数学、医疗、嵌入）

-   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** | 作者: yuxinlu1 | 👍 2,531 | ⬇️ 575,255
    -   **说明**：这是一个基于Gemma-4-12B的社区微调版本，专精于代码生成与推理（coding & reasoning）。其惊人的点赞数与下载量，证明了 **“基础模型+专业微调”** 路线在代码领域的巨大成功。
-   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | 作者: nvidia | 👍 2,524 | ⬇️ 800,597
    -   **说明**：英伟达推出的“万物定位”模型（image-feature-extraction），能将自然语言描述与图像中的特定位置精确对齐，是视觉定位任务的利器，其高下载量反映了AI在机器人、自动驾驶等领域的落地需求。
-   **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** | 作者: LiquidAI | 👍 169 | ⬇️ 17,839
    -   **说明**：Liquid AI发布的小型语言模型，以极小的参数量（230M）实现了令人印象深刻的性能，是探索模型高效性和极致压缩的代表作。

### 📦 微调与量化（社区微调、GGUF、NVFP4）

-   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 👍 1,057 | ⬇️ 970,663
    -   **说明**：基于Qwen3.5进行社区微调并量化为GGUF格式的模型，融合了“Claude风格”与“Mythos”数据集，下载量近百万，集中体现了社区对**高质量、可本地部署、风格化**模型的旺盛需求。
-   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 2,363 | ⬇️ 3,017,678
    -   **说明**：这是一个基于Qwen3.6-35B-A3B的“去限制”和“激进风格”社区微调版本，下载量超过300万，是本周**下载量最高的模型**。这强烈表明，围绕大型MoE模型的微调、对齐与“越狱”是社区最活跃的领域之一。
-   **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** | 作者: nvidia | 👍 389 | ⬇️ 5,495,402
    -   **说明**：NVIDIA对Qwen3.6-35B-A3B进行的NVFP4量化版本，**下载量超过500万**，是本周下载量之王。这说明NVFP4作为一种新的混合精度量化方案，正在被广泛采用，以解决大模型部署的成本和效率问题。

## 🔭 生态信号

-   **模型家族竞争白热化**：**Qwen 3.5/3.6** 系列成为本周生态的核心（多个变体进入前30），与**GLM-5.2**、**DeepSeek V4**形成了“三国杀”格局。这预示着中国开源模型已成为全球AI社区的重要支柱，三方在MoE、长上下文、Agent能力上展开激烈竞争。
-   **开源生态繁荣**：榜单中所有模型均为开源权重，未见任何闭源API。从基础模型（DeepSeek, GLM）到社区微调（Qwythos, HauhauCS），再到工具链（NVFP4, GGUF），整个生态完全由开源驱动。**“基础模型+社区魔改+量化部署”** 的流水线模式已非常成熟。
-   **量化技术成“刚需”**：**GGUF** 和 **NVIDIA** 的 **NVFP4** 量化模型占据了榜单的半壁江山，且下载量巨大。用户不再满足于科技公司发布的“模型权重”，更希望获得能直接在自己的硬件上运行、推理速度最优的版本。**Unsloth** 和 **yas** 等GGUF转换团队正成为生态中不可或缺的基础设施提供者。
-   **“去限制”与“风格化”微调活跃**：HauhauCS的“Uncensored”模型和empero-ai的“Mythos”风格模型高居榜单，表明社区对于模型行为的多样性和“创造力”有很强的探索欲望，这也推动了对模型对齐技术的逆向研究。

## 💡 值得探索

1.  **🥇 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) (👍 2,524)**
    -   **理由**：该模型代表了一种实用且强大的视觉理解能力。如果您从事机器人抓取、自动驾驶感知或图像编辑的任何工作，这个模型都值得立即尝试，它有望简化许多以往复杂的视觉定位流程。

2.  **🥇 [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) (👍 3,061)**
    -   **理由**：作为本周点赞数最高的模型，它代表了开源MoE中文模型的最前沿。对于希望评估或使用中文新一代大语言模型的研究者和开发者，这是首选入门模型。其强大的对话和推理能力，对构建复杂的中文Agent应用极具价值。

3.  **🥇 [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) (⬇️ 3,017,678)**
    -   **理由**：作为本周下载量冠军，它是社区力量的直接体现。尝试它可以了解社区如何在极大型MoE模型上进行“对齐”实验，并直观感受基础模型经微调后性能与风格的巨大变化。**（注意：该模型可能包含不受限制的内容，请谨慎使用）**

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*