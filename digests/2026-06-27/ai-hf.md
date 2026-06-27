# Hugging Face 热门模型日报 2026-06-27

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-27 01:56 UTC

---

好的，作为AI模型生态分析师，以下是为您生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-27**

#### **今日速览**

本周 Hugging Face 社区活跃度极高，多模态和量化模型成为绝对焦点。**Qwen 3.6** 和 **GLM-5.2** 两大新家族强势崛起，其MoE架构的量化版本（如NVFP4、GGUF）获得海量下载。与此同时，NVIDIA 和百度分别推出了 **LocateAnything-3B** 和 **Unlimited-OCR** 等视觉专用模型，展现了硬核实力。社区微调活动也异常频繁，涌现出大量针对 **Gemma 4** 和 **Qwen 3.5/3.6** 的“无审查”和“代理”优化版本。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 👍2,594, ⬇️83,589) - 智谱团队发布的最新MoE大语言模型，凭借强大的对话和推理能力，成为本周点赞最高的模型之一。
- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** (Qwen, 👍322, ⬇️13,186) - 通义千问推出的代理专用MoE模型，专为复杂工具调用和任务规划场景设计。
- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** (WeiboAI, 👍731, ⬇️54,638) - 一款主打数学推理的3B小模型，在推理能力上表现出色，小参数高性能的代表。
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** (microsoft, 👍355, ⬇️5,735) - 微软推出的高效长上下文模型，在长文本处理任务上进行了针对性优化。
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** (MiniMaxAI, 👍1,246, ⬇️169,951) - MiniMax的最新一代多模态大模型，同时支持文本和图像理解，综合能力强劲。
- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** (LiquidAI, 👍113, ⬇️8,286) - Liquid AI的LFM系列更新版本，230M的轻量级模型，适合资源受限环境。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu, 👍1,044, ⬇️134,146) - 百度发布的通用OCR模型，支持海量场景下的文字识别，应用范围极广。
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** (krea, 👍285, ⬇️8,721) - Krea的第二代图像生成模型“Turbo”版，在生成速度和画质上取得平衡。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia, 👍2,385, ⬇️494,756) - NVIDIA推出的视觉定位基础模型，能精准识别图像中的任何目标并给出位置，被誉为“万物定位器”。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** (nvidia, 👍708, ⬇️56,434) - NVIDIA的流式语音识别模型，专为实时语音转录场景打造，性能高效。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** (yuxinlu1, 👍2,400, ⬇️516,333) 与 **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (yuxinlu1, 👍689, ⬇️186,663) - 基于Gemma 4的代码生成和代理模型量化版，下载量惊人，显示了开源社区对Gemma 4系列微调和量化的极大热情。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 👍2,265, ⬇️3,453,492) - 基于Qwen 3.6的无审查量化版本，下载量突破数百万，反映了社区对“无约束”模型的特殊偏好。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai, 👍590, ⬇️486,810) - 基于Qwen 3.5的社区微调模型，融合了Claude风格，量化后用于本地推理。
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** (nvidia, 👍361, ⬇️4,812,629) - NVIDIA官方使用其Model Optimizer工具对Qwen 3.6进行的NVFP4量化版本，下载量位居榜首，证明大规模高效部署模型的巨大需求。
- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** (unsloth, 👍411, ⬇️107,553) - 社区量化专家Unsloth提供的GLM-5.2 GGUF版本，方便用户本地高效运行。
- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** (huihui-ai, 👍136, ⬇️5,445) - 对Gemma 4代码模型进行“去审查”（abliterated）处理，旨在移除安全对齐限制。

#### **生态信号**

- **Qwen 与 GLM 家族势头正旺**：Qwen 3.6 (MoE) 和 GLM-5.2 是本周最核心的两个新模型家族，为社区微调和量化提供了丰富的“原材料”，NVIDIA、HauhauCS、Unsloth等团队均在围绕它们进行工作。
- **“量化”已成必选项**：NVFP4（NVIDIA专用）和GGUF（社区标准）两种量化形式并行。下载量前五名均为量化模型，说明社区对“开箱即用、高效推理”的追求远高于原始权重。
- **开源社区微调现象“野蛮生长”**：以HauhauCS为代表的社区作者，对热门新模型进行“无审查”微调的速度极快（部分模型点赞极高，下载量数百万），这体现了开源生态的创新能力，也带来了安全对齐方面的挑战。
- **视觉理解需求爆发**：从百度的OCR到NVIDIA的“万物定位”，再到MiniMax的多模态大模型，本周榜单上的视觉模型数量和质量均显著提升，表明纯文本之外的多模态理解已成为主流需求。

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：NVIDIA出品的基础模型，在“视觉定位”领域堪称SOTA。如果您正在寻找一个通用且精确的图像目标检测/分割工具，这是您的不二之选。它的出现可能会替代许多传统的物体检测流程。

2.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**：虽然名为“无审查”，但其惊人的下载量和点赞数背后，隐藏着社区对模型“个性”和“创造性”的追求。研究人员可以通过对比其与原始Qwen 3.6在特定任务上的表现，深入理解安全对齐对模型行为的影响。

3.  **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**：如果您拥有NVIDIA硬件，这个模型是探索Qwen 3.6 MoE架构潜力的最佳入口。它展示了NVFP4这一前沿量化技术在保持模型性能的同时，能大幅降低部署成本，代表了LLM部署的未来方向。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*