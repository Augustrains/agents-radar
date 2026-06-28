# Hugging Face 热门模型日报 2026-06-28

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-28 02:07 UTC

---

好的，这是为您生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 (2026-06-28)**

#### **今日速览**

本周 Hugging Face 生态呈现多强争霸局面。**百度**发布的通用OCR模型`Unlimited-OCR`凭借其广泛的适用性迅速登顶下载榜；**Qwen**与**DeepSeek**两大模型家族持续迭代，分别推出了支持Agent的`Qwen-AgentWorld`和新架构`DeepSeek-V4-Pro-DSpark`，竞争白热化。**NVIDIA**不仅在ASR和模型量化（NVFP4）上发力，其视觉定位模型`LocateAnything-3B`也表现亮眼，证明多模态应用正加速落地。此外，社区对**Gemma 4**和**Qwen 3.5/3.6**的微调与量化活动异常活跃，涌现出大量面向特定场景的衍生模型。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 点赞: 2,683, 下载: 98,994)
  采用MoE-DSA架构的54B大语言模型，本周表现强势，是对话与文本生成领域的旗舰级开源模型。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 点赞: 2,277, 下载: 3,331,475)
  基于Qwen 3.6的社区量化版，移除了内容限制（Uncensored），因其激进的回答风格和超低部署成本（激活3B参数）而大受欢迎。
- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** (deepseek-ai, 点赞: 127, 下载: 0)
  DeepSeek官方发布的最新V4旗舰模型，采用新型架构，论文已发布，但其详细能力和应用场景值得密切关注。
- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** (Chunjiang-Intelligence, 点赞: 113, 下载: 1,328)
  基于DeepSeek V4的微调版本，专注于网络安全领域，代表了模型在垂直行业应用的深入。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu, 点赞: 1,140, 下载: 212,760)
  百度推出的通用OCR模型，支持图像到文本的转换，因其强大的光学字符识别能力和免费商用属性，迅速成为本周下载量冠军。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia, 点赞: 2,408, 下载: 570,466)
  NVIDIA发布的视觉定位模型，仅3B参数即可高效完成图像中的任意物体定位任务，极大降低了视觉基础模型的应用门槛。
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** (MiniMaxAI, 点赞: 1,253, 下载: 182,714)
  MiniMax推出的最新多模态大模型，在图像理解和文本生成方面表现优异，是国产多模态模型的重要力量。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** (nvidia, 点赞: 718, 下载: 61,857)
  专注于流式语音识别的轻量级模型，打破了NLP与音频的界限，为实时语音交互应用提供了高效方案。
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** (krea, 点赞: 311, 下载: 17,445)
  文本到图像生成领域的明星模型，作为Krea-2的加速版，在生成速度和质量上取得了良好平衡。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** (WeiboAI, 点赞: 742, 下载: 57,521)
  专注于数学推理的3B小模型，证明了在特定领域，小模型也能通过高效训练达到优秀效果。
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** (microsoft, 点赞: 365, 下载: 6,447)
  微软推出的长上下文模型，结合了类似“探索者”的子代理机制，旨在提升模型处理超长文档时的效率。
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** (nvidia, 点赞: 367, 下载: 5,022,254)
  NVIDIA利用其ModelOpt工具为Qwen 3.6模型提供的4位浮点量化版本，在极低精度下保持高性能，是部署MoE大模型的首选。
- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** (LiquidAI, 点赞: 129, 下载: 9,791)
  Liquid AI推出的超小型语言模型，证明了在极低参数规模下进行文本生成的可行性，适合边缘设备。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** (yuxinlu1, 点赞: 2,427, 下载: 536,130)
  Google Gemma 4-12B的社区微调版，专注于生成高质量代码，是当周最受欢迎的代码模型量化版之一。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai, 点赞: 674, 下载: 712,627)
  一个融合了大型模型中“神谕”能力的创新模型，以GGUF形式提供，下载量惊人，反映了社区对复杂推理能力的渴求。
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (yuxinlu1, 点赞: 733, 下载: 206,828)
  Gemma 4的Agentic版本，针对终端和Agent任务进行了优化，代表了LLM向自主操作发展的趋势。
- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** (unsloth, 点赞: 426, 下载: 125,230)
  unsloth团队对GLM-5.2的高效量化版本，降低了运行成本，推动了旗舰模型的平民化。

#### **生态信号**

1.  **模型家族势头正旺**：**Qwen**家族已成为社区最活跃的基座模型之一，衍生出大量针对特定场景的微调、量化版本。**Gemma 4**凭借Google的品牌效应和强大的基础性能，迅速成为社区微调的新宠。**DeepSeek**则在持续探索模型架构的边界。

2.  **开源权重大战持续**：从百度、NVIDIA到深度求索，越来越多的大厂将旗舰或关键模型以`Apache 2.0`或`MIT`等宽松许可开源，试图建立自己的生态壁垒。闭源模型正面临开源模型社区的强大压力。

3.  **量化与微调活动空前活跃**：`GGUF`格式的模型下载量极高，说明本地部署和端侧推理已成为主流需求。社区微调出现了“**模板化**”趋势，如基于`Qwen`或`Gemma`的“Coder”、“Agentic”版本快速迭代，且有“Uncensored”等方向形成细分市场。

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：强烈推荐。它证明了“小模型+精准任务”的巨大潜力，3B参数即可对标大模型的开集定位能力，是推动计算机视觉应用落地的关键一步。

2.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**：推荐尝试。作为本周下载王，它代表了AI解决实际通用问题（文字识别）的成熟度，几乎可以无痛接入任何需要OCR能力的项目。

3.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：值得研究。它代表了一种替代`Transformer`的新架构探索（MoE-DSA），其设计思路和性能表现对关注AI基础架构的研究者和开发者有重要价值。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*