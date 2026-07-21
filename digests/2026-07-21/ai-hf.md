# Hugging Face 热门模型日报 2026-07-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-21 01:20 UTC

---

好的，作为AI模型生态分析师，这是为您整理的2026年7月21日Hugging Face热门模型日报。

---

### **Hugging Face 热门模型日报 | 2026年7月21日**

#### **今日速览**

今日榜单呈现出“巨头打架，社区狂欢”的格局。谷歌的 **Gemma-4-31B** 凭借其绝对实力在下载量上遥遥领先，成为本周的现象级模型。同时，以 **Qwen3.5/3.6** 系列为基础的社区微调与量化模型呈现出爆发式增长，尤其是“去审查”(Uncensored)和“思维模型”(Thinking)方向成为流量密码。**百度**的通用OCR模型与**月之暗面**的代码模型也证明了专用领域的巨大需求。此外，低比特量化（1-bit, Ternary）和应用层模型（机器人、视频生成）的活跃，标志着模型生态正从“能用”向“好用”和“专用”快速演进。

#### **热门模型分类速览**

##### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | google | 3,296 | 11,987,240 | 谷歌最新旗舰多模态模型，性能强劲，是本周下载量冠军，代表了顶级开源模型的实力。 |
| **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | zai-org | 4,226 | 531,947 | 智谱AI的下一代MoE大模型，凭借极高点赞数跻身顶部，体现了强大的社区号召力。 |
| **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** | tencent | 847 | 13,698 | 腾讯混元的最新版本，作为国产基础大模型，其发布吸引了大量关注。 |
| **[Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | moonshotai | 1,174 | 713,992 | 月之暗面推出的专注于代码领域的高效压缩模型，结合Kimi K2架构，下载量巨大。 |

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | baidu | 2,437 | 2,122,848 | 百度的通用OCR模型，以极高的下载量证明了其在文档分析和图像文字提取领域的实用价值。 |
| **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | empero-ai | 2,369 | 2,117,323 | 基于Qwen3.5的社区微调版，引入“Claude Mythos”风格，下载量巨大，说明用户渴望特定风格的对话体验。 |
| **[Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | HauhauCS | 2,937 | 2,007,025 | 一款基于Qwen3.6 MoE架构的“去审查”模型，凭借激进风格和极低幻觉风险（自述）吸引了大量用户。 |
| **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** | Wan-AI | 145 | 2,408 | 专注于图像到视频生成的模型，特别是舞蹈动作生成，代表了AIGC在垂直娱乐领域的突破。 |
| **[Inkling](https://huggingface.co/thinkingmachines/Inkling)** | thinkingmachines | 1,269 | 13,462 | “思维机器”团队发布的实验性多模态模型，融合了视觉与文本思考能力，引发社区对新型架构的讨论。 |

##### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** | nvidia | 86 | 61,708 | 英伟达最新的小体量高精度嵌入模型，专为RAG和语义搜索优化，是构建AI应用的关键基础设施。 |
| **[MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | OpenMOSS-Team | 290 | 87,533 | 专注于音频转录与说话人分离，是语音识别领域的专业化模型，满足了会议记录等场景的精确需求。 |
| **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** | Cactus-Compute | 292 | 950 | 基于JAX的模型，专攻函数调用和工具使用，代表了对Agent和自动化工作流的深度探索。 |
| **[MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip) & [MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** | openbmb | 133 | 0 | 面壁智能的机器人操作和追踪模型，将多模态能力延伸至具身智能领域，具有前瞻性。 |

##### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | prism-ml | 854 | 338,945 | 采用三值量化（Ternary）技术，将27B模型压缩到2-bit，是极致量化方案的代表，下载量极高。 |
| **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | prism-ml | 542 | 1,262,894 | 1-bit量化的Bonsai模型，是社区探索极端模型压缩边界的代表，下载量惊人。 |
| **[Qwen3.6-27B-Fable-Fusion-711-...-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** | DavidAU | 156 | 16,719 | 社区“堆料”式微调的代表作，融合了多种技术（Fable, Heretic, NEO）和微调方法，模型名即特性。 |
| **[Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** | AngelSlim | 149 | 109,749 | 腾讯Hy3模型的社区量化版本，方便用户在本地低资源设备运行。 |

#### **生态信号**

1.  **Qwen 生态“一枝独秀”**：本周榜单中，围绕 **Qwen3.5/3.6** 系列的衍生模型超过10个，覆盖了微调、量化、去审查、特定角色扮演等几乎所有方向。这标志着Qwen已成为当前社区进行二次创作和部署的最热门基座模型之一，其MoE架构和开放性极大地降低了社区参与门槛。
2.  **“瘦身”与“量产”并行**：模型生态呈现两极分化。一端是 **Gemma-4**、**GLM-5.2** 这类追求性能巅峰的基础大模型；另一端则是以 **prism-ml** 的1-bit/2-bit量化为代表，将大模型塞入个人设备的极致压缩尝试。而社区微调则位于中间，通过 **Uncensored**、**Thinking** 等标签，快速实现模型的“量产”和场景化，满足长尾需求。
3.  **量化工具链成熟**：**GGUF** 格式依然是量化分发的主流，几乎所有热门的社区模型都有相应的GGUF版本。这促进了模型在本地、移动端和边缘设备的部署，是“模型民主化”的重要推手。

#### **值得探索**

1.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**：如果您对模型压缩的物理极限感兴趣，这个三值量化模型是必试项目。它展示了在极低精度下（2-bit）如何保持27B模型的可用性，对于边缘计算和研究非常有价值。
2.  **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**：对于开发者而言，这是一个将大型语言模型压缩到可部署级别而不牺牲代码能力的绝佳案例。其压缩技术（compressed-tensors）值得研究，而其实用性则可以直接服务于特定的代码生成任务。
3.  **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)**：这是机器人领域的一个前沿探索。它将VLM的能力直接用于机器人操作，代表了AI从“认识世界”向“改变世界”迈进的趋势。虽然下载量为0，但其研究方向具有极高的战略意义。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*