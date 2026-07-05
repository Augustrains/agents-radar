# Hugging Face 热门模型日报 2026-07-05

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-05 01:46 UTC

---

好的，作为AI模型生态分析师，这是为您整理的2026年7月5日《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-05**

#### **今日速览**

本周Hugging Face生态呈现出几个显著趋势：**MoE（混合专家）架构**与**GGUF量化**成为社区绝对主流，几乎所有热门大模型都围绕这两点展开。以**Qwen 3.5/3.6**和**GLM-5.2**为代表的国产模型家族势头强劲，衍生出大量社区微调与量化版本。同时，**视觉语言模型（VLM）** 和**Agent**能力成为新模型的标配，NVIDIA通过 **LocateAnything-3B** 在精细化视觉定位任务上取得了突破性关注。此外，**DeepSeek-V4** 系列的DSpark分支发布，标志着高性能推理模型的持续迭代。

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - **作者**: zai-org | **点赞**: 3,398 | **下载**: 208,920
  - **说明**: 智谱AI的最新MoE基座模型，凭借强大的对话能力和稀疏激活架构，成为本周社区最受瞩目的原始权重模型之一。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**
  - **作者**: deepseek-ai | **点赞**: 370 | **下载**: 10,306
  - **说明**: DeepSeek V4系列的专业推理变体，采用DSpark技术优化推理效率，是追求顶级性能的开发者首选。

- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)**
  - **作者**: deepseek-ai | **点赞**: 157 | **下载**: 40,271
  - **说明**: DeepSeek V4的“闪电”版本，在保持强大能力的同时做了速度优化，适合对延迟敏感的应用场景。

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**
  - **作者**: Qwen | **点赞**: 534 | **下载**: 50,188
  - **说明**: 通义千问专为Agent场景设计的35B（激活3B）参数MoE模型，是探索自主智能体的重要基座。

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)**
  - **作者**: mistralai | **点赞**: 100 | **下载**: 4
  - **说明**: Mistral AI最新的旗舰MoE模型，119B总参数，仅激活6B，代表了高效大模型的前沿水平。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - **作者**: nvidia | **点赞**: 2,604 | **下载**: 1,194,542
  - **说明**: NVIDIA推出的“万物定位”视觉模型，能接受文本或图像指令进行精准定位，重新定义了视觉理解任务的交互方式。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - **作者**: baidu | **点赞**: 1,714 | **下载**: 988,379
  - **说明**: 百度发布的通用OCR模型，以其“无限”场景的强大识别能力和极高的下载量，成为本周期实用多模态模型之王。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - **作者**: HauhauCS | **点赞**: 2,454 | **下载**: 2,993,053
  - **说明**: 社区基于Qwen3.6制作的“激进”无审查版MoE模型，下载量近300万，反映出社区对特定风格和低限制模型的强烈需求。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**
  - **作者**: krea | **点赞**: 496 | **下载**: 89,384
  - **说明**: Krea AI的第二代图像生成模型的Turbo版本，在速度与质量间取得良好平衡，是文生图领域的焦点。

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)**
  - **作者**: fal | **点赞**: 157 | **下载**: 0
  - **说明**: 用于LTX视频模型的LoRA模块，专注于生成逼真的3D场景视频，展示了LoRA技术在视频生成领域的应用潜力。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - **作者**: empero-ai | **点赞**: 1,461 | **下载**: 1,464,047
  - **说明**: 一个融合了“Mythos”风格的Qwen 3.5模型GGUF量化版，超高的下载量证明了社区对个性化、创意型叙事模型的追捧。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
  - **作者**: yuxinlu1 | **点赞**: 2,595 | **下载**: 641,260
  - **说明**: 基于Google Gemma-4的12B“Coder”版模型，经Fable5方法微调，其量化版在编码能力上表现突出。

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**
  - **作者**: google | **点赞**: 196 | **下载**: 1,177
  - **说明**: Google推出的表格数据基础模型，支持零样本分类与回归，为非结构化表格分析提供了新范式。

- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)**
  - **作者**: BugTraceAI | **点赞**: 132 | **下载**: 12,001
  - **说明**: 专注网络安全与漏洞分析的专用模型，采用Q6量化，显示了AI在特定安全领域的应用深化。

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)**
  - **作者**: nationaldesignstudio | **点赞**: 122 | **下载**: 1,881
  - **说明**: 基于ONNX和Transformers.js的PII识别模型，专为边缘端和在浏览器中直接运行设计，关注数据隐私。

- **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)**
  - **作者**: AliesTaha | **点赞**: 119 | **下载**: 0
  - **说明**: 基于Qwen3的指令微调模型，虽然没有下载量，但表明社区正在尝试创建如“fable”风格的有特定叙事能力的小模型。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**
  - **作者**: deepreinforce-ai | **下载**: 359,659
  - **说明**: 作者将自家的Ornith-1.0-35B模型进行了GGUF量化，使其能被更多人用llama.cpp在本地运行，是模型部署普惠化的典型。

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)**
  - **作者**: deepreinforce-ai | **下载**: 320,660
  - **说明**: 与35B版策略一致，将小尺寸的Ornith-1.0-9B也进行量化，进一步覆盖不同硬件层级的用户群体。

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)**
  - **作者**: huihui-ai | **下载**: 4,701
  - **说明**: 社区对GLM-5.2进行“剥夺”（abliterated）去除对齐限制，并量化成GGUF格式，迎合了部分用户对低审查模型的需求。

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)**
  - **作者**: nvidia | **下载**: 184,521
  - **说明**: 英伟达使用Model Optimizer技术将Qwen3.6压缩至NVFP4格式，展示了在NVIDIA硬件上的极致优化与部署能力。

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)**
  - **作者**: Jackrong | **下载**: 59,971
  - **说明**: 另一个社区魔改的“代码”版本Qwen3.6 MoE模型，融合了Coder和MTP特性并量化，体现了社区对编码模型的高度定制化热情。

#### **生态信号**

本周生态呈现三大信号：**第一，MoE + GGUF的组合成为标准范式**。几乎每个热门模型都有其GGUF版本，这显著降低了普通人运行超大规模模型的硬件门槛，推动了AI民主化。**第二，中国模型家族（Qwen, GLM）生态圈异常活跃**。特别是Qwen 3.5/3.6版本，衍生出大量诸如“Uncensored”、“Coder”、“Agent”的变体，形成了庞大的社区微调生态，其生命力远超单一闭源模型。**第三，视觉定位和Agent能力成为新增长点**。NVIDIA的LocateAnything-3B和Qwen的AgentWorld模型表明，下一阶段竞赛的重点已从纯文本转向更复杂的“感知-推理-行动”闭环。

#### **值得探索**

1.  **探索 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：如果你想了解下一代交互式视觉AI，这个模型代表了最前沿。它不仅是“识别”，而是“定位”，在机器人、游戏、图像编辑等领域有巨大潜力。
2.  **尝试 [nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)**：如果你是NVIDIA硬件用户且关注推理性能与VRAM占用的平衡，NVFP4精度格式是一个值得关注的优化方向。这个模型是测试其效果的最佳实践。
3.  **研究 [Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**：对于关注AI Agent的开发者，这是目前最成熟的MoE Agent模型之一。它展示了如何通过架构设计（35B参数但仅激活3B）来平衡复杂任务的Agent能力与实时性。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*