# Hugging Face 热门模型日报 2026-07-12

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-12 01:22 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月12日数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月12日**

#### **今日速览**

本周Hugging Face社区呈现“炼金术”般的狂热：基于Qwen 3.5/3.6和GLM-5.2的社区微调与量化模型霸榜，显示出开源社区对顶级基座模型的二次开发已达到白热化。nVIDIA的定位模型 `LocateAnything-3B` 异军突起，成为非语言模型中的亮点。同时，以 `tencent/Hy3` 为代表的国内大厂与 `nVIDIA/Nemotron` 系列形成了“大厂发布”与“社区精调”的双轨竞争格局。值得注意的是，GGUF量化格式依然是本地部署的首选，下载量惊人。

---

### **热门模型**

#### 🧠 **语言模型（LLM、对话模型、指令微调）**

*   **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** (tencent, 点赞:697, 下载:8,210)
    *   腾讯最新发布的HyV3系列语言模型，主打文本生成，是本周关注度最高的“大厂原生”模型。
*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 点赞:3,832, 下载:421,270)
    *   基于GLM架构的5.2版本，采用MoE架构。点赞数周榜第一，社区对GLM系列新版本的极高期待。
*   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** (InternScience, 点赞:494, 下载:28,141)
    *   专为Agent任务设计的MoE模型，基于Qwen3.5，结合了视觉与文本理解能力。
*   **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** (meituan-longcat, 点赞:176, 下载:1,572)
    *   美团发布的长上下文对话模型，专注于处理超长文本对话场景。
*   **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** (nvidia, 点赞:105, 下载:30,418)
    *   nVIDIA的旗舰级MoE模型（75B激活9B），采用NVFP4高精度量化，代表了大厂在Scaling Law上的探索。
*   **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)** (AliesTaha, 点赞:199, 下载:5,053)
    *   基于Qwen 3的指令微调模型，专注于“寓言故事”风格的长文本生成与逻辑推理。

#### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** (baidu, 点赞:1,929, 下载:1,380,690)
    *   百度的通用OCR模型，支持图像到文本的识别。下载量超百万，反映出市场对高质量OCR模型的强劲需求。
*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia, 点赞:2,707, 下载:1,472,194)
    *   nVIDIA的通用目标定位模型，能根据文字指令在图像中定位任意物体。点赞与下载量均极高，是本周最大的“黑马”之一。
*   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** (krea, 点赞:588, 下载:168,154)
    *   Krea-2模型的加速版，专注于文生图任务，在图像质量和生成速度上做了平衡。
*   **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** (Alissonerdx, 点赞:99, 下载:0)
    *   基于LTX-2的“身份保持”文生视频模型，旨在生成指定人脸的连续视频。
*   **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** (CohereLabs, 点赞:89, 下载:7,687)
    *   Cohere推出的阿拉伯语语音识别模型，填补了小语种ASR的开源空白。
*   **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** (OpenMOSS-Team, 点赞:109, 下载:12,817)
    *   集成了语音转文字与说话人识别（Diarization）的音频理解模型。

#### 🔧 **专用模型（代码、数学、医疗、嵌入、路由）**

*   **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** (google, 点赞:348, 下载:20,110)
    *   谷歌发布的结构化表格数据基础模型，支持零样本分类与回归，是Tabular AI领域的重要里程碑。
*   **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** (yuxinlu1, 点赞:1,150, 下载:436,530)
    *   基于Gemma-4的精调版，专攻代码生成与Agentic终端任务，是“Agentic Coding”趋势的代表。
*   **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** (SupraLabs, 点赞:98, 下载:1,275)
    *   轻量级的“模型路由”模型，用于智能判断输入该交由哪个专业模型处理，是AI Agent编排的基础组件。

#### 📦 **微调与量化（社区微调、GGUF、AWQ）**

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai, 点赞:2,014, 下载:1,944,961)
    *   基于Qwen 3.5的“神话”风格微调并进行GGUF量化，下载量接近200万，是社区精调的绝对王者。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 点赞:2,651, 下载:2,641,936)
    *   本周下载量最高！基于最新的Qwen 3.6进行“无审查”微调的MoE模型，反映出强烈的“越狱”或“角色扮演”社区需求。
*   **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** (unsloth, 点赞:140, 下载:38,922)
    *   Unsloth对DeepSeek-V4的极速版进行GGUF量化，为本地部署高性能推理模型提供了便利。
*   **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** (deepreinforce-ai, 点赞:850, 下载:1,216,495)
    *   名为“Ornith”的通用对话模型GGUF版本，下载量超过百万，证明高质量通用量化模型的吸引力。
*   **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** (unsloth, 点赞:1,048, 下载:2,904,169)
    *   本周下载量第二！Unsloth对Qwen3.6的27B多模态版本进行了GGUF量化，是Qwen 3.6爆火的最直接证据。

---

### **生态信号**

1.  **“Qwen王朝”与“GLM回归”**：本周生态最明显的特点是 **Qwen 3.5/3.6** 系列（及其衍生品）占据了社区微调与量化的半壁江山，从9B到35B，从通用到无审查，生态极其繁荣。同时，基于 **GLM-5.2** 和 **DeepSeek-V4** 的模型也显示出强大的社区号召力。

2.  **开源权重“军备竞赛”白热化**：腾讯、百度、nVIDIA、谷歌等大厂在同一周内发布不同方向的模型（Hy3, OCR, LocateAnything, TabFM），表明**开源权重已成为AI巨头的战略必争之地**，通过开源建立生态影响力。

3.  **量化与“越狱”微调成流量密码**：**GGUF格式**与**“Uncensored”**（无审查）标签是本周流量暴涨的核心驱动力。社区用户对“解锁全部能力”和“在本地离线运行大模型”的需求极其旺盛，贡献了动辄百万级的下载量。

---

### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    *   **理由**：本周最大亮点。它证明了除了文本对话，**“视觉定位”** 是下一个极具实用价值的AI能力。3B的参数量兼顾了效果与部署门槛，值得所有关注视觉AI的开发者深入研究。

2.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
    *   **理由**：作为点赞数最高的模型，GLM社区在经历了几个版本的迭代后，5.2版本引发了极高的热情。如果你希望跟踪国内顶尖MoE架构的演进，这个模型是必读项。

3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    *   **理由**：它是“社区力量”的极致体现。基于最新、最强的基座模型，进行了社区最渴望的“解放”，并迅速占领了下载量榜首。研究它的微调手法和用户反馈，可以深刻理解开源社区的主流审美与技术走向。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*