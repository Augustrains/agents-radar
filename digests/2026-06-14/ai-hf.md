# Hugging Face 热门模型日报 2026-06-14

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-14 02:13 UTC

---

好的，作为AI模型生态分析师，以下是2026年6月14日的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-14**

#### **今日速览**

本周 Hugging Face 生态系统呈现两大核心趋势：一是 **“超级”多模态模型**成为绝对主角，以 Google Gemma 4 系列和 DeepSeek-V4 为代表的旗舰模型在算力、统一架构和多任务能力上实现重大突破；二是**量化与社区微调生态异常活跃**，Unsloth 团队几乎同步发布了所有大模型的 GGUF 版本，使得个人开发者能够在消费级硬件上运行顶尖模型。值得注意的是，NVIDIA 的“LocateAnything”项目和 Xiaomi 的 MiMo 系列证明了特定领域（如视觉定位、Agent）的专用模型也获得了极高的社区关注。

---

#### **热门模型分类整理**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
  - 作者: deepseek-ai | 👍 4,813 | ⬇️ 3,250,404
  - 一句话说明：DeepSeek 的第四代旗舰模型，“Pro”版本代表了当前开源文本生成模型的顶尖水平，以绝对的点赞和下载量位居榜首。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**
  - 作者: CohereLabs | 👍 356 | ⬇️ 6,533
  - 一句话说明：Cohere 发布的专注于代码生成的 MoE 小型模型，性能高效，是开发者进行本地代码辅助的理想选择。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - 作者: nvidia | 👍 1,962 | ⬇️ 69,443
  - 一句话说明：NVIDIA 推出的“万物定位”视觉模型，能根据文本指令精准定位图像中的任意物体，是人机交互和机器人领域的突破性工作。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**
  - 作者: google | 👍 995 | ⬇️ 1,005,883
  - 一句话说明：Google Gemma 4 系列的指令微调版本，被标记为“any-to-any”任务，证明其在理解并生成文本、图像等多模态内容上的强大统一性。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 👍 1,762 | ⬇️ 2,411,202
  - 一句话说明：基于 Qwen3.6 的社区激进微调版，名为“Uncensored”且激活参数仅3B，在获得极高下载量的同时引发了关于模型安全与可控性的讨论。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**
  - 作者: ideogram-ai | 👍 517 | ⬇️ 6,535
  - 一句话说明：图像生成明星模型 Ideogram 4 的 FP8 量化版，大幅降低了运行门槛，使得高质量文生图可以更高效地本地部署。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**
  - 作者: zai-org | 👍 154 | ⬇️ 0
  - 一句话说明：专注于角色动画的图像生成视频模型，虽然下载量为0（可能尚未开放权重），但其“Pose-driven”特性代表了视频生成领域的新方向。

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**
  - 作者: ByteDance | 👍 235 | ⬇️ 426
  - 一句话说明：字节跳动推出的“图像-文本到视频”渲染器，能从图文描述生成高质量视频，标志着多模态生成进入新阶段。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**
  - 作者: bosonai | 👍 414 | ⬇️ 32,162
  - 一句话说明：新一代的文本到语音（TTS）大模型，4B参数级别，代表了合成语音在自然度和表现力上的重大进步。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **(本周无典型专用模型入选前30，主要集中在多模态和通用LLM)**

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)**
  - **作者:** unsloth | 👍 248 | ⬇️ 42,885
  - **一句话说明:** Google 最新扩散模型 DiffusionGemma 的 GGUF 量化版，由 Unsloth 团队提供，让普通用户也能在本地CPU或低显存GPU上运行。

- **[Jiunsong/supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)**
  - **作者:** Jiunsong | 👍 820 | ⬇️ 98,892
  - **一句话说明:** 社区对 Gemma-4-26B 的“无审查”微调并量化为GGUF版本，下载量极高，反映出开发者对探索模型能力边界的强烈需求。

---

#### **生态信号**

1.  **模型家族势头正旺**：**Gemma 4 系列**（Google）和 **Qwen 3.x 系列**（阿里巴巴）已成为当前中文社区与全球社区最活跃的两大基础模型族。特别是 Gemma 4，其“any-to-any”的统一架构正在重新定义多模态模型。
2.  **开源权重无可争议**：本周榜单纯粹由开源权重模型主导，DeepSeek、Google、NVIDIA 的开源策略获得了社区的积极回报。Ideogram 4 的开源权重版也引发了该领域的排位变化。
3.  **量化生态是必争之地**：**Unsloth** 团队已经成为事实上的“量化基础设施”，几乎所有热门模型发布后，其 GGUF 版本便会紧随其后。这预示着未来的模型竞争不仅是架构和性能的竞争，更是“运行可达性”的竞争。社区微调（如 abliterated， uncensored 版本）极度活跃，显示出用户对模型定制化和“去限制”的强烈偏好。

---

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    - 理由：它打破了传统目标检测的封闭集限制，赋予了模型对世界万物进行“指哪打哪”的视觉理解能力，是通往通用视觉 Agent 的关键一步，非常值得研究和实验。

2.  **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**
    - 理由：作为“any-to-any”的代表作，Gemm4-12B 证明了多模态融合可以做到如此流畅。其高达100万的下载量也证明了它是当前社区调试、测试和部署多模态应用的首选基础模型。

3.  **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
    - 理由：作为本周的点赞和下载双冠王，其在文本生成/推理任务上的表现已成为新的基线。如果你想了解当前开源语言模型能力的上限在哪里，这个模型是绕不开的研究对象。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*