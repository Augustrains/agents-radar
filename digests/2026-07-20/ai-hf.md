# Hugging Face 热门模型日报 2026-07-20

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-20 01:26 UTC

---

好的，作为 AI 模型生态分析师，以下是基于 2026 年 7 月 20 日数据生成的 Hugging Face 热门模型日报。

---

### **Hugging Face 热门模型日报 | 2026-07-20**

#### **今日速览**

本周 Hugging Face 生态呈现三个核心信号：**多模态模型** 成为绝对主力，前 10 名中近半数为图像/文本输入模型；**模型瘦身运动** 白热化，prism-ml 的 1-bit/2-bit 量化（GGUF/MLX）模型下载量惊人，小模型单设备部署成为刚需；**国内厂商** 表现亮眼，百度的 Unlimited-OCR 和 zai-org 的 GLM-5.2 持续霸榜，表明基础模型能力和应用场景的双重突破。此外，社区微调活动极其活跃，大量基于 Qwen3.5/3.6 和 Inkling 的魔改版本层出不穷。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - 作者: zai-org | 点赞: 4,167 | 下载: 536,177
  - 国产 MoE 大模型旗舰，搭载 DSA 架构，以极高点赞量证明其强大的对话与生成能力。

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**
  - 作者: tencent | 点赞: 835 | 下载: 13,698
  - 腾讯混元系列第三代模型，专注于文本生成，是基础模型家族中不可忽视的力量。

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**
  - 作者: InternScience | 点赞: 584 | 下载: 35,833
  - 基于 Qwen3.5 的 MoE 模型，专为 Agent 任务设计，展示了端侧智能体的潜力。

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**
  - 作者: froggeric | 点赞: 947 | 下载: 0
  - 非模型权重，而是一个“修复”Qwen 系模型对话模板的公共资源，下载量为 0 但高赞，反映社区对标准化工具的渴求。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**
  - 作者: google | 点赞: 3,273 | 下载: 12,337,374
  - Google 开源的多模态旗舰，擅长图像与文本理解，以惊人的下载量稳坐本周“下载王”宝座。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - 作者: empero-ai | 点赞: 2,345 | 下载: 2,118,995
  - 结合 Qwen3.5 推理能力的多模态模型，量化版（GGUF）极受欢迎，下载量超 200 万。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - 作者: baidu | 点赞: 2,187 | 下载: 2,122,848
  - 百度推出的通用 OCR 模型，号称“无限”场景识别，精准切中了文档数字化处理的痛点。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 2,901 | 下载: 2,084,530
  - 社区微调典范，基于 Qwen3.6 的 MoE 视觉模型，去审查且风格激进，下载量极高。

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)**
  - 作者: thinkingmachines | 点赞: 1,150 | 下载: 13,462
  - 全新多模态模型，支持图像、文本、音频输入，是近期生态中架构最创新的模型之一。

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)**
  - 作者: Wan-AI | 点赞: 128 | 下载: 2,408
  - 图像到视频生成的专用模型，专注于人物动画生成，展示了视频生成领域的垂直化趋势。

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**
  - 作者: OpenMOSS-Team | 点赞: 279 | 下载: 87,533
  - 语音到文本模型，集成了说话人日志功能，是会议记录等场景的实用工具。

- **[OpenMOSS-Team/MOSS-VL-Realtime](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)**
  - 作者: OpenMOSS-Team | 点赞: 81 | 下载: 544
  - 视频到文本模型，专注于实时视频理解，是边缘计算场景的理想选择。

- **[mgwr/M87](https://huggingface.co/mgwr/M87)**
  - 作者: mgwr | 点赞: 158 | 下载: 4,652
  - 基于 Krea-2 的 LoRA 模型，专注文本到图像生成，展示了社区在创意生成领域的活跃度。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)**
  - 作者: Cactus-Compute | 点赞: 279 | 下载: 955
  - 基于 JAX 的模型，专为函数调用和工具使用设计，是构建 AI Agent 的重要组件。

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)**
  - 作者: ATH-MaaS | 点赞: 194 | 下载: 14,587
  - 基于 Qwen3.5 的 OCR 专用模型，说明 OCR 与大模型结合正成一类标准化产品。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**
  - 作者: prism-ml | 点赞: 792 | 下载: 338,945
  - 创新性的“三元”量化技术，将 27B 模型压缩至 2-bit，兼顾推理速度与模型性能。

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**
  - 作者: prism-ml | 点赞: 498 | 下载: 1,262,894
  - 极致量化的代表，1-bit 版本下载量超过 120 万，证明了超低比特量化的强大生命力。

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-...-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)**
  - 作者: DavidAU | 点赞: 106 | 下载: 16,719
  - 社区定制化微调的典型，融合多种技术（MT、Unsloth），形成“缝合怪”风格，满足特定需求。

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)**
  - 作者: Alissonerdx | 点赞: 195 | 下载: 0
  - 视频生成领域的高质量 LoRA，专为人脸身份保持训练，下载量为 0 但高赞，代表“作品级”社区资源。

- **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)**
  - 作者: jlnsrk | 点赞: 141 | 下载: 4,035
  - 对 GLM-5.2 的极致量化，支持 CPU 部署，表明 MoE 大模型正逐步走向边缘设备。

---

#### **生态信号**

本周生态释放三大信号：**第一，多模态模型成为绝对主流**。前 10 名中有 5 个模型具备图像/视频输入能力，gemma-4、Inkling、Qwen3.6 系列均在此列，视觉理解能力成为模型标配。**第二，“开源权重+极低量化”模式获胜**。prism-ml 的 1-bit/2-bit 模型下载量远超其基础模型，说明社区更关注“能跑起来的模型”，而非单纯追求参数量。**第三，社区微调活动高度活跃且混乱**。大量基于 Qwen3.5/3.6 和 Inkling 的 GGUF 魔改版涌现（如 DavidAU 的长名字模型），虽有“炒冷饭”之嫌，但侧面印证了基础模型成熟后，社区对“个性化”和“易用性”的旺盛需求。

---

#### **值得探索**

1. ** [thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling) **
   - **理由**：该模型支持图像、文本、音频三模态输入，且采用 MoE 架构，是近期最具创新性的多模态模型之一。如果你想了解多模态融合的最新范式，这是首选。

2. ** [prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) **
   - **理由**：“三元”量化（2-bit）是量化领域的前沿技术。该模型展示了如何在极端压缩下维持大模型的能力，是研究模型小型化、边缘部署的绝佳样本。

3. ** [InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1) **
   - **理由**：专注于 Agent 任务的模型。在 AI Agent 热潮下，了解一个专门为此训练的开源模型，对于开发智能体应用和工具链非常有价值。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*