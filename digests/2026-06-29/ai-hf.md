# Hugging Face 热门模型日报 2026-06-29

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-29 02:06 UTC

---

好的，这是为你准备的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-29**

#### **今日速览**

本周 Hugging Face 热门榜呈现出 **“多强争霸，应用落地”** 的鲜明特征。**GLM-5.2** 系列凭借其 MoE 架构在 Base 模型和量化版本上全面开花，成为本周绝对焦点。**Qwen 3.5/3.6** 生态同样表现抢眼，大量社区微调、量化版本涌现，尤其是 “Uncensored” 变体下载量惊人。值得关注的是，**DeepSeek V4** 系列（Pro/Fable/Flash）正式登上舞台，表明顶尖闭源模型正在加速向开源社区渗透。此外，**NVIDIA** 推出了从 ASR 到 LoRA 定位的一系列专用模型，**Krea 2** 和 **LTX 2.3** 在图像与视频生成领域也贡献了惊喜。整体来看，专注于特定场景（如代码、推理、Agent）的模型更易获得用户青睐。

---

### **热门模型**

#### 🧠 语言模型（LLM、对话模型、指令微调）

*   **zai-org/GLM-5.2**
    *   作者: zai-org | 👍 点赞: 2,821 | 📥 下载: 118,651
    *   说明: ZAI 推出的旗舰级 MoE 对话模型，以其强大的推理能力和通用性稳居本周人气第一。

*   **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**
    *   作者: HauhauCS | 👍 点赞: 2,302 | 📥 下载: 3,248,724
    *   说明: Qwen 3.6 的社区微调 “Uncensored” 版本，以激进的风格和极高的下载量显示出用户对低限制模型的需求。

*   **deepreinforce-ai/Ornith-1.0-35B-GGUF**
    *   作者: deepreinforce-ai | 👍 点赞: 413 | 📥 下载: 79,630
    *   说明: Ornith 1.0 系列是基于 Qwen 3.5 微调的大模型家族，其 35B 量化版备受本地部署与 Agent 任务用户欢迎。

*   **Qwen/Qwen-AgentWorld-35B-A3B**
    *   作者: Qwen | 👍 点赞: 400 | 📥 下载: 23,697
    *   说明: Qwen 官方推出的 Agent 专用世界模型，专注于理解和交互虚拟环境，是 Agent 领域的重要模型。

*   **deepseek-ai/DeepSeek-V4-Pro-DSpark**
    *   作者: deepseek-ai | 👍 点赞: 182 | 📥 下载: 373
    *   说明: DeepSeek 最新 V4 系列模型的首发版本，标志着其最新一代大语言模型正式开源，备受开发者期待。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **krea/Krea-2-Turbo**
    *   作者: krea | 👍 点赞: 355 | 📥 下载: 27,631
    *   说明: Krea 推出的新一代图像生成模型，旨在提升生成速度和图像质量，是图像生成领域的突破性更新。

*   **nvidia/LocateAnything-3B**
    *   作者: nvidia | 👍 点赞: 2,436 | 📥 下载: 646,451
    *   说明: NVIDIA 推出的零样本目标定位模型，可在图像中高精度地定位任何物体，在多模态应用场景中极具价值。

*   **nvidia/nemotron-3.5-asr-streaming-0.6b**
    *   作者: nvidia | 👍 点赞: 734 | 📥 下载: 67,419
    *   说明: NVIDIA 发布的流式语音识别模型，以 0.6B 的轻量级实现高精度实时转录，适用于边缘设备。

*   **fal/LTX-2.3-3DREAL-LoRA**
    *   作者: fal | 👍 点赞: 95 | 📥 下载: 0
    *   说明: 专为 LTX 视频模型打造的 LoRA，旨在生成更具真实感和三维效果的视频，拓展了视频生成的新边界。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**
    *   作者: yuxinlu1 | 👍 点赞: 2,473 | 📥 下载: 549,926
    *   说明: 基于 Gemma 4 的代码专用模型，经过 Composer 框架微调，在编程任务上表现出色，是开发者社区的大热模型。

*   **WeiboAI/VibeThinker-3B**
    *   作者: WeiboAI | 👍 点赞: 744 | 📥 下载: 59,337
    *   说明: 微博 AI 推出的数学推理专用小模型，以 3B 的参数量实现了强大的数学能力，显示了小模型的巨大潜力。

*   **microsoft/FastContext-1.0-4B-SFT**
    *   作者: microsoft | 👍 点赞: 369 | 📥 下载: 6,779
    *   说明: Microsoft 发布的长上下文模型，旨在高效处理长文档任务，与 “Explorer SubAgent” 概念结合，探索 Agent 新范式。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**
    *   作者: empero-ai | 👍 点赞: 803 | 📥 下载: 831,529
    *   说明: 融合了 Claude-Mythos 风格的大型 Qwen 3.5 微调模型的 GGUF 量化版，是追求本地运行高质量角色扮演和推理模型的用户首选。

*   **HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced**
    *   作者: HauhauCS | 👍 点赞: 100 | 📥 下载: 40,820
    *   说明: 基于 Gemma 4 的 QAT 量化 “Uncensored” 版本，在保持模型性能的同时大幅减小体积，是社区微调与量化结合的范例。

*   **unsloth/GLM-5.2-GGUF**
    *   作者: unsloth | 👍 点赞: 443 | 📥 下载: 146,023
    *   说明: 热门工具 Unsloth 为 GLM-5.2 提供的官方 GGUF 量化版，极大地降低了该模型本地部署的门槛。

*   **nvidia/Qwen3.6-35B-A3B-NVFP4**
    *   作者: nvidia | 👍 点赞: 371 | 📥 下载: 5,235,413
    *   说明: NVIDIA 使用其 Model Optimizer 工具对 Qwen 3.6 的 MoE 模型进行 FP4 极致量化，以超低精度实现高效推理，下载量惊人。

---

### **生态信号**

本周生态呈现出 **“MoE 架构”** 和 **“Agent & 代码”** 双核驱动的局面。以 **GLM-5.2** 和 **Qwen 3.5/3.6** 为首的 MoE 模型家族势头正旺，其 “大参数量、小激活量” 的优势使其成为社区微调和量化的热门标的。开源权重模型生态已进入 **“超大规模竞赛”** 阶段，**DeepSeek V4** 和 **Ornith 1.0** 等模型的涌现，表明顶尖性能已不再是闭源模型的专利。值得注意的量化活动异常活跃，**NVIDIA** 的 NVFP4 和 **Unsloth** 的 GGUF 工具正在加速推动大模型在本地和边缘设备上的部署，**HauhauCS** 等社区作者围绕 “Uncensored” 的二次开发也形成了独特的亚文化。

---

### **值得探索**

1.  **nvidia/LocateAnything-3B**: 如果你的工作涉及图像理解、目标检测或多模态 RAG，这个模型绝对值得一试。它以 3B 的体量实现了强大的零样本定位能力，是工具箱中非常实用的 “瑞士军刀”。

2.  **microsoft/FastContext-1.0-4B-SFT**: 如果你在处理长文档、知识库问答或 Agent 记忆管理，这个模型值得深入研究。它展示了微软在 “长上下文 + Agent” 方向的最新探索，是解决大模型“记不住”问题的一个新方案。

3.  **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**: 对于开发者而言，这是目前社区最热门的代码模型之一。它基于强大的 Gemma 4 基座，经过了专门的代码微调和量化，在代码补全、生成和解释方面表现突出，且易于本地部署。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*