# Hugging Face 热门模型日报 2026-07-27

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-27 01:30 UTC

---

好的，作为 AI 模型生态分析师，以下是针对 2026 年 7 月 27 日 Hugging Face 热门模型的日报分析。

---

### **Hugging Face 热门模型日报 | 2026-07-27**

#### **今日速览**

本周 Hugging Face 生态被**社区微调**和**量化**浪潮主导，特别是基于 **Qwen3.6** 和 **GLM-5.2** 的衍生模型占据了绝对热度。值得注意的是，**多模态能力**（尤其是视觉理解）已成为新发布模型的标配，无论是通用大模型还是专用 OCR 模型均集成此功能。此外，**机器人领域**出现了专注“操作”与“追踪”的专用模型，标志着 AI 从“数字世界”向“物理世界”的延伸。**开源权重模型**的竞争力正显著增强，部分社区微调版本（如 Uncensored 系列）的下载量远超其基础模型。

---

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

-   **zai-org/GLM-5.2** ([链接](https://huggingface.co/zai-org/GLM-5.2))
    -   *作者:* zai-org | *点赞:* 4,476 | *下载:* 827k
    -   *一句话说明:* 强大的 MoE 对话模型家族，凭借出色的性能和开放性成为本周焦点，并带动了其视觉版本的上榜。

-   **upstage/Solar-Open2-250B** ([链接](https://huggingface.co/upstage/Solar-Open2-250B))
    -   *作者:* upstage | *点赞:* 595 | *下载:* 3.3k
    -   *一句话说明:* 250B 参数的开放式大模型，主打高能效与强性能，代表了模型规模竞赛的继续。

-   **poolside/Laguna-S-2.1** ([链接](https://huggingface.co/poolside/Laguna-S-2.1))
    -   *作者:* poolside | *点赞:* 700 | *下载:* 56k
    -   *一句话说明:* 面向特定应用的大语言模型，其系列量化版（GGUF, NVFP4）也同时上榜，表明企业级部署需求旺盛。

-   **Nanbeige/Nanbeige4.2-3B** ([链接](https://huggingface.co/Nanbeige/Nanbeige4.2-3B))
    -   *作者:* Nanbeige | *点赞:* 447 | *下载:* 14k
    -   *一句话说明:* 高效的小参数模型，30亿参数即可展现强大能力，适合资源受限的边缘部署场景。

-   **fdtn-ai/antares-1b** ([链接](https://huggingface.co/fdtn-ai/antares-1b))
    -   *作者:* fdtn-ai | *点赞:* 186 | *下载:* 5.9k
    -   *一句话说明:* 专为安全场景设计的轻量级模型，采用 GraniteMoEHybrid 架构，填补了AI安全领域的空白。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

-   **baidu/Unlimited-OCR** ([链接](https://huggingface.co/baidu/Unlimited-OCR))
    -   *作者:* baidu | *点赞:* 3,205 | *下载:* 2.5M
    -   *一句话说明:* 百度发布的通用OCR模型，支持图像到文本的高精度识别，以海量下载量证明了其在自动化文档处理中的巨大实用价值。

-   **thinkingmachines/Inkling** ([链接](https://huggingface.co/thinkingmachines/Inkling))
    -   *作者:* thinkingmachines | *点赞:* 1,579 | *下载:* 34k
    -   *一句话说明:* 一个全能型的图像-文本多模态模型，定位为“思考机器”，在高交互性对话与视觉理解任务上表现出色。

-   **microsoft/Mage-Flow** ([链接](https://huggingface.co/microsoft/Mage-Flow))
    -   *作者:* microsoft | *点赞:* 334 | *下载:* 1.3k
    -   *一句话说明:* 微软推出的新型文本到图像生成/编辑框架，展示了前沿的图像生成流程。其Turbo版本同时上榜。

-   **owensong/Inflect-Micro-v2** ([链接](https://huggingface.co/owensong/Inflect-Micro-v2))
    -   *作者:* owensong | *点赞:* 178 | *下载:* 298
    -   *一句话说明:* 专为CPU和边缘AI设计的轻量级文本转语音模型，标志着边缘端高质量语音合成的普及。

-   **nvidia/Cosmos3-Edge** ([链接](https://huggingface.co/nvidia/Cosmos3-Edge))
    -   *作者:* nvidia | *点赞:* 125 | *下载:* 32k
    -   *一句话说明:* 英伟达发布的世界模型系列，聚焦物理世界理解与生成，为机器人仿真等提供基础。

-   **ATH-MaaS/OvisOCR2** ([链接](https://huggingface.co/ATH-MaaS/OvisOCR2))
    -   *作者:* ATH-MaaS | *点赞:* 308 | *下载:* 35k
    -   *一句话说明:* 基于 Qwen3.5 架构的专用OCR模型，表明通用大模型在垂直领域通过微调即可达到顶尖效果。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

-   **Kwaipilot/KAT-Coder-V2.5-Dev** ([链接](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev))
    -   *作者:* Kwaipilot | *点赞:* 197 | *下载:* 3.7k
    -   *一句话说明:* 面向代码生成的开发版模型，融合了 Qwen3.5 MoE 架构，专为复杂编码任务设计。

-   **openbmb/MiniCPM-RobotManip** ([链接](https://huggingface.co/openbmb/MiniCPM-RobotManip))
    -   *作者:* openbmb | *点赞:* 177 | *下载:* 643
    -   *一句话说明:* 首个基于视觉-语言-动作（VLA）模型的操作端到端模型，为机器人“手”提供智能。

-   **openbmb/MiniCPM-RobotTrack** ([链接](https://huggingface.co/openbmb/MiniCPM-RobotTrack))
    -   *作者:* openbmb | *点赞:* 130 | *下载:* 398
    -   *一句话说明:* 与 RobotManip 配套的追踪模型，将视觉语言能力用于机器人对物体的动态跟踪。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

-   **DavidAU/Qwen3.6-27B-Fable-Fusion-...-GGUF** ([链接](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF))
    -   *作者:* DavidAU | *点赞:* 637 | *下载:* 552k
    -   *一句话说明:* 极致的社区微调与量化产物，基于Qwen3.6进行“无审查”混合微调，并用GGUF格式打包，符合社区对“自由”和高性能的追求。

-   **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
    -   *作者:* HauhauCS | *点赞:* 3,112 | *下载:* 1.9M
    -   *一句话说明:* 本周现象级模型，基于Qwen3.6的MoE架构，经过“激进”社区微调，下载量巨大，反映了社区对高性能、无约束模型极高的需求。

-   **prism-ml/Ternary-Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf))
    -   *作者:* prism-ml | *点赞:* 1,049 | *下载:* 631k
    -   *一句话说明:* 使用三元量化（1-bit/2-bit）技术的极端优化模型，验证了模型压缩极限的同时，确保了可用的对话能力。

-   **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))
    -   *作者:* empero-ai | *点赞:* 2,479 | *下载:* 1.4M
    -   *一句话说明:* 结合 Qwen3.5 和大量合成数据进行微调的量化模型，证明了合成数据驱动的微调路线正成为主流。

---

#### **生态信号**

-   **模型家族势能：** **Qwen3.6/3.5** 毫无疑问成为本周开源社区的“底座之王”，围绕其衍生的微调和量化版本（如 `DavidAU`、`HauhauCS`、`empero-ai`）占据了榜单半壁江山。同时，**GLM-5.2** 及其视觉版也展示了强大的家族影响力，形成了与 Qwen 家族分庭抗礼之势。
-   **开源权重引领创新：** 榜单前五名中，开源权重模型（包括社区微调版）占据4席。这标志着开源社区已形成“基础模型公司（如zai-org, baidu）→ 社区精调/量化（如HauhauCS, prism-ml）→ 用户部署”的高效创新链条，其多样性和迭代速度超越了传统闭源模型发布。
-   **量化活动的核心化：** **GGUF** 格式的广泛流行（前十中有4个与此相关）表明，社区已将模型量化视为模型落地的“最后一步”，这降低了使用门槛，但也意味着基座模型的“量化友好度”将成为重要竞争力。同时，像 **Ternary-Bonsai** 这样的极端量化实验，预示着未来在算力受限设备上的模型部署将更加激进。

---

#### **值得探索**

1.  **openbmb/MiniCPM-RobotManip & RobotTrack**：如果你对具身智能或机器人感兴趣，这两个模型是必看的。它们代表了AI从“思考”到“行动”的关键一步，且基于高效的VLA架构，是研究物理世界交互的理想起点。
2.  **microsoft/Mage-Flow** 系列：作为生成式AI的最新探索，这个框架展示了超越简单文生图的能力。研究其如何实现精细化、指令化的图像编辑，对理解未来图像处理范式的演进非常有帮助。
3.  **prism-ml/Ternary-Bonsai-27B-gguf**：对于模型压缩和高效部署研究者而言，这是一个极致案例。探索这个1-bit/2-bit模型在保持对话能力上的得失，有助于理解模型能力和压缩比的真实边界。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*