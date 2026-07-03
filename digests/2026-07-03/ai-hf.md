# Hugging Face 热门模型日报 2026-07-03

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-03 01:43 UTC

---

好的，我是你的AI模型生态分析师。以下是基于2026年7月3日数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-03**

#### **今日速览**

本周Hugging Face生态呈现出“大厂旗舰与社区微调齐飞”的繁荣景象。**DeepSeek V4系列**（Pro & Flash）与**GLM-5.2**的发布标志着国产大模型在开源权重上的持续发力；而社区对**Gemma 4**进行的高强度Agent/代码微调（如`gemma-4-12B-agentic-fable5`）使其成为本周最受欢迎的量化模型系列之一。此外，百度推出的**Unlimited-OCR**凭借强大的实用性和“无限”场景适应性，下载量迅速突破75万，成为多模态领域的黑马。值得关注的是，**NVFP4**量化格式（Nvidia）开始被广泛应用于GLM和Qwen家族，显示出业界对高性能低精度推理的明确需求。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (作者: zai-org | ❤️ 3,254 | 📥 176,154)
    *   **说明: ** 智谱AI发布的第五代GLM模型，采用MoE架构，以强大的对话与推理能力成为本周点赞量最高的纯语言模型。
*   **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** (作者: deepseek-ai | ❤️ 303 | 📥 8,184)
    *   **说明: ** DeepSeek V4的旗舰版，支持DSpark加速，代表了当前开源模型在推理能力上的前沿水平。
*   **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)** (作者: deepseek-ai | ❤️ 128 | 📥 23,939)
    *   **说明: ** V4系列的快速推理版本，在性能与速度间取得平衡，适合高并发场景。
*   **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** (作者: Qwen | ❤️ 511 | 📥 39,448)
    *   **说明: ** Qwen团队专为Agent任务优化的MoE模型，35B总参数量仅激活3B，是高效Agent开发的标杆。
*   **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** (作者: nvidia | ❤️ 207 | 📥 159,698)
    *   **说明: ** Nvidia将GLM-5.2量化为4-bit浮点格式，展示了在Nvidia硬件上进行极致压缩与推理优化的能力。
*   **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LiquidAI/LiquidAI/LFM2.5-230M)** (作者: LiquidAI | ❤️ 192 | 📥 26,357)
    *   **说明: ** 2.3亿参数的小模型，性能却相当出色，体现了通过优秀架构在极小规模下实现高性价比推理的趋势。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (作者: baidu | ❤️ 1,652 | 📥 758,489)
    *   **说明: ** 百度推出的通用OCR模型，主打任意场景下的文字识别，下载量极高，普适性强。
*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (作者: nvidia | ❤️ 2,573 | 📥 1,006,831)
    *   **说明: ** Nvidia的开放词汇目标检测模型，能定位图像中任何物体，是当前最热的多模态工具之一。
*   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** (作者: krea | ❤️ 462 | 📥 69,788)
    *   **说明: ** Krea推出的第二代图像生成模型Turbo版，主打快速、高质量的文生图，配套LoRA生态丰富。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (作者: HauhauCS | ❤️ 2,396 | 📥 3,078,904)
    *   **说明: ** 基于Qwen3.6的社区去审查版（Uncensored），视觉能力强大，下载量突破300万，是社区最活跃的微调模型之一。
*   **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** (作者: fal | ❤️ 145 | 📥 0)
    *   **说明: ** 用于LTX视频模型的LoRA，专注于生成逼真的3D风格视频，是图像到视频领域的新尝试。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** (作者: yuxinlu1 | ❤️ 2,573 | 📥 614,069)
    *   **说明: ** 基于Gemma 4的微调代码模型，在代码生成和推理任务上表现优异，是该系列最受欢迎的变体。
*   **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (作者: yuxinlu1 | ❤️ 962 | 📥 314,374)
    *   **说明: ** 专为Agent和终端操作优化的Gemma 4微调版，代表了Agent化模型在本地部署的趋势。
*   **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** (作者: google | ❤️ 118 | 📥 89)
    *   **说明: ** Google发布的超大规模表格基础模型，支持零样本分类与回归，是表格数据AI的里程碑。
*   **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** (作者: nationaldesignstudio | ❤️ 104 | 📥 790)
    *   **说明: ** 专注于PII（个人身份信息）检测的Token分类模型，对安全合规应用有重要价值。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (作者: empero-ai | ❤️ 1,255 | 📥 1,250,562)
    *   **说明: ** 基于Qwen3.5的1M上下文长度微调版GGUF，长文本能力极强，下载量超125万。
*   **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** (作者: deepreinforce-ai | ❤️ 658 | 📥 284,585)
    *   **说明: ** Ornith系列（基于Qwen3.5 MoE）的量化版，提供35B大杯量级的高效本地部署选择。
*   **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** (作者: deepreinforce-ai | ❤️ 196 | 📥 7,358)
    *   **说明: ** 接近开源极限的397B MoE超大杯，展示了社区对极致性能的追求。
*   **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** (作者: huihui-ai | ❤️ 135 | 📥 2,592)
    *   **说明: ** 对GLM-5.2进行“去审查”（abliterated）处理的量化版，体现了社区对模型自由度的持续探索。
*   **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** (作者: nvidia | ❤️ 210 | 📥 27,249)
    *   **说明: ** Nvidia使用Model Optimizer对Qwen3.6进行NVFP4量化，是官方推动硬件级高效推理的范例。

---

#### **生态信号**

1.  **模型家族“三足鼎立”**: 本周热门模型高度集中于**Qwen3.5/3.6**、**Gemma 4**和**GLM-5.2**三大生态。Qwen因其丰富的MoE变体和强大的社区微调（Uncensored、长文本）占据数量优势；Gemma 4则在代码和Agent垂直领域表现出色；GLM-5.2凭借出色的原生性能吸引大量关注。
2.  **开源权重已成为主流发行方式**: DeepSeek V4和GLM-5.2均发布开源权重，这再次验证了业界共识：通过开源权重吸引社区贡献和生态建设，是模型成功的关键策略。
3.  **量化与微调是流量密码**: 榜单前列几乎被**GGUF**和**NVFP4**格式的量化模型占据。社区创作者通过**Unsloth**等工具对最新模型进行**Agent化**、**代码微调**或**去审查**，再辅以GGUF量化，已成为获取高点赞和下载量的标准操作。

---

#### **值得探索**

1.  **尝试 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**: 如果你需要精准的图像定位或目标检测能力，这个模型提供了无需预定义类别的通用解决方案，是目前最实用的多模态工具。
2.  **关注 [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**: 作为本周点赞数最高的模型，其MoE架构和强大的对话能力值得深度测试。它代表了中国大模型在复杂推理上的最新成果。
3.  **深入 [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**: 如果你想在本地部署一个强大的代码助手，这个Gemma 4微调版是目前社区公认的佼佼者，其GGUF格式使其在消费级显卡上也能流畅运行。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*