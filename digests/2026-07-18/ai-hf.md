# Hugging Face 热门模型日报 2026-07-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-18 01:14 UTC

---

好的，作为AI模型生态分析师，以下是为您整理的2026年7月18日Hugging Face热门模型日报。

---

### **Hugging Face 热门模型日报 | 2026年7月18日**

#### **今日速览**

本周Hugging Face社区热点集中在大规模MoE（混合专家）模型的竞赛与极致量化探索上。**zai-org** 的 **GLM-5.2** 以超过4000点赞领跑，展示了超大规模语言模型的开源吸引力。与此同时，以 **prism-ml** 为代表的团队正将27B参数量的模型疯狂压缩至1-bit，催生了下载量超百万的 **Bonsai-27B-gguf** 系列，标志着“极致压缩”成为热门赛道。多模态模型领域，**Qwythos** 系列和 **Unlimited-OCR** 等专注于特定推理和视觉任务的模型也取得了巨大成功，显示社区对实用型多模态AI的迫切需求。

#### **热门模型**

**🧠 语言模型（LLM、对话模型、指令微调）**

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
    *   **作者:** zai-org | **点赞:** 4,071 | **下载:** 534,698  
    *   **说明:** 采用DSA架构的超级MoE模型，凭借其强大的通用能力成为本周最受瞩目的开源大模型。

*   **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**  
    *   **作者:** tencent | **点赞:** 820 | **下载:** 12,719  
    *   **说明:** 腾讯发布的Hunyuan系列第三代模型，展现了国内大厂在开源基础模型上的持续投入。

*   **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)**  
    *   **作者:** Cactus-Compute | **点赞:** 257 | **下载:** 874  
    *   **说明:** 基于JAX框架，专为函数调用和工具使用设计的专用模型，代表了Agent专用模型的趋势。

*   **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
    *   **作者:** froggeric | **点赞:** 934 | **下载:** 0  
    *   **说明:** 这个“无模型权重”的仓库因其修复了Qwen系列的聊天模板而获得高赞，体现了社区对开发者工具的重视。

**🎨 多模态与生成（图像、视频、音频、文本到X）**

*   **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)**  
    *   **作者:** ATH-MaaS | **点赞:** 153 | **下载:** 10,795  
    *   **说明:** 专注于OCR的视觉语言模型，在高精度文本识别场景下表现突出。

*   **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)**  
    *   **作者:** Wan-AI | **点赞:** 108 | **下载:** 2,185  
    *   **说明:** 14B参数量的图像到视频生成模型，专注于舞蹈动作生成，是视频AIGC板块的新星。

*   **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)**  
    *   **作者:** Alissonerdx | **点赞:** 178 | **下载:** 0  
    *   **说明:** 针对LTX视频模型的身份保持LoRA，旨在解决视频生成中人脸身份一致性问题。

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
    *   **作者:** baidu | **点赞:** 2,019 | **下载:** 1,992,355  
    *   **说明:** 百度出品的通用OCR模型，强大的识别能力和海量下载量证实了其在实际应用中的巨大价值。

**🔧 专用模型（代码、数学、医疗、嵌入）**

*   **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**  
    *   **作者:** OpenMOSS-Team | **点赞:** 248 | **下载:** 83,160  
    *   **说明:** 结合语音转录和说话人分离（Diarization）的音频处理模型，在会议记录等场景有广泛应用。

**📦 微调与量化（社区微调、GGUF、AWQ）**

*   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**  
    *   **作者:** prism-ml | **点赞:** 679 | **下载:** 200,774  
    *   **说明:** 首创“三进制”量化的27B模型，在保持推理能力的同时将模型压缩到极致，是量化技术的里程碑。

*   **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**  
    *   **作者:** prism-ml | **点赞:** 394 | **下载:** 1,045,182  
    *   **说明:** 1-bit量化的27B模型，下载量破百万，证明了社区对低资源可运行大模型的饥渴需求。

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
    *   **作者:** empero-ai | **点赞:** 2,273 | **下载:** 2,096,147  
    *   **说明:** 基于Qwen3.5的9B模型，混入了Mythos数据集的GGUF版本，极高的下载量使其成为本周量化界的“爆款”。

*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
    *   **作者:** HauhauCS | **点赞:** 2,827 | **下载:** 2,295,313  
    *   **说明:** “无审查”的35B MoE模型，巨大的下载量反映了社区对模型“自由度”和多样化视角的追求。

*   **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)**  
    *   **作者:** prism-ml | **点赞:** 116 | **下载:** 17,127  
    *   **说明:** Bonsai模型的MLX版本，专为苹果芯片优化，1-bit量化进一步降低了本地部署门槛。

*   **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)**  
    *   **作者:** unsloth | **点赞:** 224 | **下载:** 1,924,495  
    *   **说明:** unsloth对Qwen3.6-27B进行的NVIDIA FP4量化版本，代表了NVIDIA生态内最新量化技术的应用。

#### **生态信号**

1.  **模型家族“军备竞赛”**：本周榜单被 **Qwen3.x**（特别是3.5和3.6）和 **GLM** 家族牢牢占据。基于Qwen的微调模型（如Qwythos）和量化版本（如HauhauCS的版本）数量众多，表明Qwen已成为社区二次创作的首选基座。GLM-5.2的崛起表明，国产大型MoE模型在开源社区中的地位正在迅速提升。
2.  **“极致量化”成为显学**：从1-bit的Bonsai到2-bit的Ternary-Bonsai，再到NVFP4，将大模型“缩小”到可以在个人设备上运行已经成为主流趋势。这一现象不仅降低了AI的使用门槛，也预示着未来的模型竞争将从单纯的“大”转向“大且轻”。
3.  **微调与量化的深度绑定**：与以往模型发布后社区再量化不同，本周很多模型（如Qwythos系列、Bonsai系列）在发布时就提供了GGUF、MLX等多种量化版本。这表明开发者已经将“可部署性”视为与模型性能同等重要的核心指标，量化不再是事后补充，而是发布流程的一部分。

#### **值得探索**

1.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：强烈推荐研究其1-bit量化的具体技术细节。这个模型在性能损失与压缩率之间取得了惊人的平衡，是边缘计算和端侧AI的重要参考案例。
2.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：作为本周点赞数最高的模型，它代表了当前开源大模型在MoE架构上的前沿探索。对比其与Qwen系列的性能差异，可以洞察不同技术路线的优劣。
3.  **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)**：Qwythos系列是社区微调Qwen的标杆之作。体验它的多模态能力和推理能力，并对比其GGUF版本与原始版本的性能差异，是了解当前社区微调水平的最佳窗口。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*