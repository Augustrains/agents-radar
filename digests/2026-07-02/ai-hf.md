# Hugging Face 热门模型日报 2026-07-02

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-02 02:00 UTC

---

好的，作为AI模型生态分析师，以下是为您生成的《Hugging Face 热门模型日报》。

---

### **🤖 Hugging Face 热门模型日报 | 2026年7月2日**

#### **今日速览**

今日Hugging Face榜单呈现出三大显著趋势：**国产大模型齐头并进**，以GLM-5.2系列、Qwen系列（包括新版本3.6及AgentWorld）和DeepSeek-V4为代表的模型家族在榜上占据了显著位置。其次，**多模态能力成为标配**，从图像OCR到文生图，再到文生视频，多模态模型的应用范围与影响力持续扩大。最后，**量化与微调生态异常活跃**，GGUF格式的模型占比极高，社区通过“去审查”和“专家角色扮演”等微调方向，展现出强大的自定义能力。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - 作者: zai-org | 👍 3,170 | 📥 159,967
    *   **说明**: 智谱AI最新一代MoE大模型的社区发布版，凭借强大的性能和开源许可，登顶本周点赞榜首。
*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - 作者: empero-ai | 👍 1,160 | 📥 1,113,871
    *   **说明**: 基于Qwen3.5的9B模型，专门为模仿Claude Mythos角色而微调，展示了社区对“角色扮演”和特定风格模型的高热度。
*   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** - 作者: yuxinlu1 | 👍 2,552 | 📥 597,090
    *   **说明**: 基于Google Gemma 4的代码/推理能力增强版模型，以高下载量和点赞数表明其在开发者社区中的高受欢迎度。
*   **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** - 作者: deepseek-ai | 👍 277 | 📥 7,629
    *   **说明**: 深度求索最新发布的V4系列“专业”版，虽然下载量尚在初期，但其代表了最前沿的闭源模型研究方向。
*   **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-230M)** - 作者: LiquidAI | 👍 181 | 📥 21,935
    *   **说明**: Liquid AI出品的小参数模型，主打高效与专用场景，适合边缘设备部署和快速推理。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - 作者: baidu | 👍 1,579 | 📥 630,246
    *   **说明**: 百度推出的通用OCR模型，专为图像内的文本提取设计，凭借其强大的泛化能力和实用性，下载量超高。
*   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** - 作者: krea | 👍 438 | 📥 56,953
    *   **说明**: Krea公司推出的第二代文生图模型的加速版，标志着高质量图像生成的持续进化。
*   **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** - 作者: fal | 👍 136 | 📥 0
    *   **说明**: 用于LTX视频生成模型的LoRA模块，专注于生成逼真的3D效果，反映了社区对特定视觉效果的控制需求。
*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** - 作者: nvidia | 👍 2,547 | 📥 896,058
    *   **说明**: 英伟达推出的“万物定位”模型，具备强大的图像特征提取与定位能力，在多模态应用中潜力巨大，下载量极高。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[yuxinlu1/gemma-4-12B-coder...](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** - （已在语言模型中列出，此分类特指其“代码”用途）
*   **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** - 作者: Qwen | 👍 497 | 📥 34,371
    *   **说明**: 通义千问发布的Agent专用世界模型，旨在为AI Agent构建更真实、可预测的模拟环境，是Agent领域的重要基础设施。
*   **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** - 作者: BugTraceAI | 👍 108 | 📥 3,377
    *   **说明**: 专为网络安全/攻防渗透设计的专用模型，体现了AI在垂直专业领域的深度应用。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** - 作者: unsloth | 👍 490 | 📥 212,201
    *   **说明**: 知名量化工具Unsloth提供的GLM-5.2 GGUF版本，显著降低了运行门槛。
*   **[unsloth/Qwen-AgentWorld-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen-AgentWorld-35B-A3B-GGUF)** - 作者: unsloth | 👍 129 | 📥 196,441
    *   **说明**: Qwen AgentWorld模型的GGUF版本，便于开发者本地部署Agent。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - 作者: HauhauCS | 👍 2,378 | 📥 3,055,962
    *   **说明**: 基于Qwen3.6的“去审查”版本，下载量惊人，反映了社区对模型输出内容自由度的强烈追求。
*   **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)** - 作者: Jackrong | 👍 100 | 📥 12,635
    *   **说明**: 社区微调的Qwen3.6代码模型，结合了MTP（多标记预测）技术，展示了Qwen家族强大的可塑性。

#### **生态信号**

*   **模型家族三足鼎立**：今日榜单清晰显示出**GLM-5.2**、**Qwen系列**（3.5/3.6/AgentWorld）和**Gemma 4**是当前三大热门系列。其中，Qwen系列的多版本发布（Agent、Uncensored）和大量微调活动，使其生态系统最为活跃。
*   **开源权重占据绝对主流，闭源探索前沿**：本次榜单几乎全部为开源权重模型。DeepSeek-V4作为少数“准闭源”模型，虽体量不大，但其存在代表着顶尖实验室仍在探索的、更具突破性的技术路径。
*   **量化（GGUF）与去审查（Uncensored）是两大社区趋势**：GGUF格式的模型数量占比极高，说明本地部署和私有化运行是用户的核心诉求。另一方面，“Uncensored”标签与高下载量紧密相关，表明社区正积极探索模型回复的边界，通过微调来移除安全对齐限制。

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：如果你想搭建一个能“看懂”并与图像交互的AI应用，这个模型是实现物体检测、视觉问答等功能的强大且易用的基础模型。
2.  **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**：对于正在研究AI Agent的开发者，这是当前市场上最前沿的“世界模型”之一。它不再是简单的聊天，而是为Agent构建一个可交互的模拟环境，代表了AI的下一个重要方向。
3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**：如果你需要研究模型在完全无限制状态下的表现，或进行某些需要突破对话安全边界的测试，这个高流量的去审查版本是必试项。但请务必注意其合规性风险。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*