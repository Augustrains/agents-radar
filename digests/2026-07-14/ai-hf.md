# Hugging Face 热门模型日报 2026-07-14

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-14 01:13 UTC

---

好的，以下是为您生成的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 (2026-07-14)

#### 今日速览

本周 Hugging Face 生态呈现出显著的“多模态融合”与“社区微调量化”双轮驱动趋势。腾讯的 **Hy3** 和智谱的 **GLM-5.2** 作为基础模型新星，获得了极高的社区关注。与此同时，以 **Qwythos** 系列、**HauhauCS** 的“无审查”版本为代表的社区微调模型，配合 **GGUF** 量化格式，在下载量上遥遥领先。值得注意的是，百度发布的通用OCR模型 **Unlimited-OCR** 展现了特定领域大模型的强大潜力。另外，多模态模型（特别是支持视觉的 **Qwen3.6** 系列）和音频处理模型（如 **MOSS-Transcribe-Diarize**）的活跃度显著提升，标志着AI能力边界的持续拓宽。

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**
  - 作者: tencent | 点赞: 754 | 下载: 9,157
  - 腾讯最新发布的HyV3系列文本生成模型，作为本土大厂的最新力作，迅速成为社区关注的焦点。

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - 作者: zai-org | 点赞: 3,900 | 下载: 464,914
  - 智谱GLM系列的最新迭代，采用MoE架构，凭借强大的对话能力与高点赞数，成为本周最受开发者欢迎的基础模型之一。

- **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)**
  - 作者: migtissera | 点赞: 104 | 下载: 1,105
  - 基于Qwen3.5微调的高级推理模型，专注于增强模型在复杂任务上的思考与生成能力。

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)**
  - 作者: SupraLabs | 点赞: 114 | 下载: 1,573
  - 一个轻量级的模型路由专家（Router），用于在多个下游大模型之间智能分配任务，代表了模型编排与效率优化的新方向。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - 作者: empero-ai | 点赞: 2,084 | 下载: 1,985,221
  - 基于Qwen3.5的社区微调版，整合了多种推理风格，其GGUF量化版本因极高的下载量成为社区热门选择。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - 作者: baidu | 点赞: 1,963 | 下载: 1,506,937
  - 百度发布的通用OCR模型，可处理图片中的文字识别任务。其强大的零样本泛化能力，使其成为特定领域的明星模型。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 2,710 | 下载: 2,512,124
  - 基于Qwen3.6的“无审查”MoE视觉语言模型，因其强大的推理能力和极低的审查限制，获得了社区极高的下载量和关注度。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**
  - 作者: unsloth | 点赞: 1,074 | 下载: 2,901,906
  - 由Unsloth团队量化的Qwen3.6多模态模型（支持图像理解），是本周下载量最高的模型之一，反映了社区对高效、易用多模态模型的巨大需求。

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**
  - 作者: OpenMOSS-Team | 点赞: 162 | 下载: 39,509
  - 专注于语音转文字与说话人分离的音频模型，代表了语音处理领域的专业化趋势。

- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)**
  - 作者: open-gigaai | 点赞: 128 | 下载: 0
  - 一个由Diffusers框架支持的世界模型生成器，代表了从文本/图像生成可控视频或模拟环境的前沿探索。

- **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)**
  - 作者: nineninesix | 点赞: 95 | 下载: 3,940
  - 一个基于Qwen3.5的文本到语音模型，展示了将语言模型能力迁移到语音合成领域的新思路。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**
  - 作者: google | 点赞: 362 | 下载: 21,590
  - Google发布的表格数据基础模型，支持分类和回归任务的零样本预测，代表了基础模型在结构化数据领域的重要突破。

- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)**
  - 作者: CohereLabs | 点赞: 102 | 下载: 11,647
  - Cohere发布的阿拉伯语专用语音识别模型，体现了针对特定语言和区域市场的专业化模型开发趋势。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**
  - 作者: yuxinlu1 | 点赞: 1,178 | 下载: 452,627
  - 基于Gemma-4的社区微调模型，专注于增强模型的“代理”能力和编码能力，其GGUF版本在开发者中非常流行。

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**
  - 作者: deepreinforce-ai | 点赞: 868 | 下载: 1,392,300
  - 一个35B参数量的社区微调模型，其MIT开源协议和高下载量表明它正被广泛应用于各类文本生成任务。

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)**
  - 作者: jlnsrk | 点赞: 86 | 下载: 1,997
  - 针对GLM-5.2进行INT4量化的版本，专门优化了CPU运行效率，使得高端模型能在普通硬件上运行，是边缘部署的重要实践。

### 生态信号

本周的模型生态呈现出几个鲜明趋势：
1.  **MoE与视觉模型成为主流**：无论是腾讯的Hy3、智谱的GLM-5.2还是社区的Qwen3.6变体，采用**混合专家（MoE）**架构的模型占据主导。同时，“image-text-to-text”任务标签的出现频率极高，表明能理解图像的**多模态模型**已成开发者标配。
2.  **量化生态空前繁荣**：GGUF量化格式已成为模型分发的“黄金标准”。**Unsloth**、**empero-ai**等团队在量化领域的持续产出，不仅让普通用户能够运行大模型，更催生了大量基于基础模型的社区微调版（如Qwythos、Ornith）。开源权重的生态正在通过量化实现真正的“普惠”。
3.  **开源权重与专业化齐头并进**：腾讯、百度、NVIDIA等大型企业积极发布开源权重，与Cohere、智谱等公司形成健康竞争。同时，社区不再满足于通用模型，而是涌现出针对**OCR、语音、表格数据、视频生成**等特定领域的专业模型，AI应用的**垂直化**趋势愈发明显。

### 值得探索

1.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**: 如果你需要强大的图片文字识别能力，这个模型展示了基础模型在特定领域的应用天花板，其高达150万的下载量充分证明了其价值，非常值得尝试。
2.  **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**: 作为本周下载量的“冠军”，它是体验多模态大模型（识别、理解图像）在本地运行的最佳入门选择。配合Unsloth的优化，性能与易用性俱佳。
3.  **[Google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**: 对于从事数据分析、金融、科学计算的研究者而言，这是一个开创性的模型。它代表了大语言模型之外的另一条路——将Transformer的能力用于解决表格数据的核心问题，其零样本能力值得深入研究。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*