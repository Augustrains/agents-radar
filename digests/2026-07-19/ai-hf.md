# Hugging Face 热门模型日报 2026-07-19

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-19 01:20 UTC

---

好的，作为AI模型生态分析师，以下是基于您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-19**

#### **今日速览**

本周 Hugging Face 生态呈现出两大显著趋势：**“超低位宽量化”成为社区新宠**，以 prsim-ml 的 1-bit / 2-bit Bonsai 系列为代表，推动了大规模模型在消费级硬件上的普及；同时，**多模态模型（尤其是图文理解）全面爆发**，从创业公司到科技巨头（如 Google、百度）均发布了重磅模型，性能与功能竞争日趋白热化。此外，围绕特定场景（如 OCR、视频生成）的专用模型和微调版本也获得了大量关注，显示了社区生态的成熟与细分。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - by zai-org | 👍 4,126 | 📥 541,662
    - 采用 MoE-DSA 架构的高性能对话模型，凭借强大的生成能力和高效的推理，成为本周点赞数最高的模型之一。
- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** - by tencent | 👍 829 | 📥 13,571
    - 腾讯推出的新一代混元大模型（Hunyuan V3），专注于文本生成，代表了国内开源大模型的重要进展。
- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** - by InternScience | 👍 579 | 📥 35,575
    - 基于 Qwen3.5-MoE 架构智能体模型，专为 Agent 任务设计，显示了将大型语言模型工具化和框架化的趋势。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** - by ATH-MaaS | 👍 170 | 📥 13,750
    - 专为光学字符识别（OCR）优化的视觉语言模型，在文档理解和文本识别场景中表现出色。
- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** - by Wan-AI | 👍 114 | 📥 2,328
    - 用于图像到视频生成的扩散模型，专注于高质量、动态的人物动画生成。
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - by baidu | 👍 2,025 | 📥 2,088,470
    - 百度发布的通用 OCR 模型，具备极强的高精度识别能力，下载量达数百万，是生态中需求量极大的实用工具。
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** - by OpenMOSS-Team | 👍 259 | 📥 86,385
    - 语音处理模型，集成了语音转文字（ASR）和说话人日志（Speaker Diarization）功能，为会议记录等场景提供一站式解决方案。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** - by froggeric | 👍 941 | 📥 0
    - 专注于解决 Qwen 系列对话模板问题的工程化模型。其高点赞数反映了社区对模型易用性和标准化的强烈需求。
- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** - by Cactus-Compute | 👍 268 | 📥 935
    - 基于 JAX 的模型，专注于函数调用和工具使用，是推动 Agent 应用和自动化工作流的关键技术组件。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - by HauhauCS | 👍 2,865 | 📥 2,190,398
    - 基于 Qwen3.6 的 MoE 视觉模型去审查版，采用 GGUF 量化。其极高的下载量反映了社区对个性化、无限制模型版本的巨大需求。
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** - by prism-ml | 👍 735 | 📥 301,893
    - 27B 参数的三元（2-bit）量化模型，将大模型内存需求压缩到极低水平，是边缘计算和消费级硬件部署的代表性作品。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - by empero-ai | 👍 2,315 | 📥 2,112,869
    - 基于 Qwen3.5 的 9B 模型，经过 GGUF 量化后，因其优秀的性能和推理能力平衡了效率与质量，下载量超过 200 万。
- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** - by GnLOLot | 👍 277 | 📥 172,409
    - 极小型 1B 参数模型的量化版，具备“思考”能力，展示了在端侧设备部署复杂推理任务的可能性。

#### **生态信号**

- **模型家族引领潮流**：**Qwen 系列（3.5/3.6）** 生态系统最为繁荣，大量基于其基座的微调、量化、多模态版本（如 Qwythos, HauhauCS）表现亮眼。**Prism-ML 的 Bonsai/GLM-5.2** 系列在超低位宽量化赛道上异军突起，其 1-bit/2-bit 模型具备开创性意义。
- **开源权重占据主导**：本周热榜上所有模型均为开源权重，且绝大多数由社区或个人开发者贡献。这强化了“开放优于封闭”的生态共识，并推动了大模型技术的平民化。Google 的 `gemma-4-31B-it` 作为巨头发布的特定用途模型，下载量虽高但社会关注度不及社区创新。
- **量化与微调活动活跃**：**GGUF** 格式是社区量化的事实标准（约占榜单 1/3），几乎所有热门模型都有对应版本。**MLX**（Apple 生态）和 **三元量化**（1.58 bit / 2-bit）成为新兴热点，后者在保持性能的同时实现了惊人的压缩率，预示着一个更节能、更普及的部署时代即将到来。

#### **值得探索**

1.  **[[prism-ml/Bonsai-27B-gguf]](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：1-bit 量化模型。这不仅是工程示的范，更是理解模型容量与信息压缩极限的绝佳研究样本。建议用其与 8-bit 版本对比，评估超低位宽的实用价值。
2.  **[[conradlocke/krea2-identity-edit]](https://huggingface.co/conradlocke/krea2-identity-edit)**：基于 Krea-2 的身份编辑 LoRA。它直接应用于图像编辑任务，是探索个性化生成、身份保持等前沿方向的有效工具，适合有图生成需求的玩家。
3.  **[[jlnsrk/GLM-5.2-colibri-int4]](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)**：采用 4-bit “Colibri” 专家流式技术的 GLM-5.2 MoE 量化版。该方案针对 CPU 部署进行了特别优化，研究其如何在不损失过多精度的情况下将 MoE 模型用于 CPU 推理，极具参考价值。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*