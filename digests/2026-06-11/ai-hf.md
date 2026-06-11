# Hugging Face 热门模型日报 2026-06-11

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-11 02:14 UTC

---

好的，作为 AI 模型生态分析师，根据您提供的 2026 年 6 月 11 日数据，我为您生成了以下《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 | 2026-06-11

---

#### 📈 今日速览

本周 Hugging Face 生态呈现三大核心趋势：**多模态模型全面开花**，以 Google 的 Gemma 4 系列和 DeepSeek-V4-Pro 为首，不仅涵盖图文理解，更向“任意模态到任意模态”演进。**行业头部公司争相发布超大参数混合专家模型（MoE）**，如 NVIDIA 的 Nemotron-3 Ultra (550B) 和 DeepSeek 的 V4-Pro，竞争白热化。与此同时，**量化与社区微调版本**不断涌现，Unsloth 和社区开发者围绕 Gemma 4 及 Qwen 系列推出了大量轻量化变体，显著降低了模型使用门槛，推动了自部署浪潮。

---

#### 🔥 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** | 作者: deepseek-ai | 👍 4,761 | 📥 4,061,006
  - **一句话说明**：DeepSeek 最新旗舰对话模型，以碾压性的点赞数和下载量成为本周绝对焦点，标志着大模型竞赛进入新阶段。

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** | 作者: nvidia | 👍 189 | 📥 59,066
  - **一句话说明**：NVIDIA 推出的55B激活参数的超级MoE模型，代表了工业界在超大规模模型上的最新探索，反映了“大而稀疏”的架构趋势。

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-8B-A1B)** | 作者: LiquidAI | 👍 582 | 📥 142,134
  - **一句话说明**：Liquid AI 的第二代高效语言模型，以8B总参数量、仅1B激活参数实现了高水准性能，是边缘计算和高效推理的热门选择。

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** | 作者: JetBrains | 👍 281 | 📥 18,273
  - **一句话说明**：JetBrains 发布的专注于代码与逻辑推理的模型，强化了“思维链”能力，在开发工具社区内引发关注。

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** & **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** | 作者: nex-agi
  - **一句话说明**：基于 Qwen3.5 MoE 架构的系列变体，提供了从 Pro 到 Mini 的完整方案，显示出社区对可缩放模型系列的持续需求。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | 作者: nvidia | 👍 1,806 | 📥 131,794
  - **一句话说明**：NVIDIA 的通用图像定位与分割模型，因其实验室级别的精准度与开放权重，受到研究者和开发者追捧。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** | 作者: google | 👍 889 | 📥 675,936
  - **一句话说明**：Google 的旗舰级多模态模型，专注于“any-to-any”任务，支持图文输入输出，是本周生态的核心组件之一。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** & **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** | 作者: ideogram-ai
  - **一句话说明**：Ideogram 第四代高保真文本生成图像模型的不同量化版，通过FP8/NF4格式降低了显存需求，推动高质量图像生成普及。

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** | 作者: google | 👍 174 | 📥 19,806
  - **一句话说明**：Google Magenta 团队推出的实时音乐/音频生成模型，为创意AI应用提供了高性能的语音和音乐生成能力。

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** | 作者: ByteDance | 👍 210 | 📥 305
  - **一句话说明**：字节跳动的文本/图像到视频生成渲染器，专注于高质量视频合成，是多模态生成领域的有力竞争者。

- **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** | 作者: jdopensource | 👍 127 | 📥 5,457
  - **一句话说明**：京东开源的文字转视频生成模型，集成了音频与视频生成能力，进一步拉低了AIGC视频创作的门槛。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** | 作者: sapientinc | 👍 740 | 📥 134,752
  - **一句话说明**：专注于人力资源管理（HRM）领域的文本生成模型，以1B参数实现高垂直领域精度，打开专用小模型的想象空间。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** | 作者: bosonai | 👍 324 | 📥 19,948
  - **一句话说明**：Boson AI 的4B参数TTS大模型，在多语言语音合成方面表现出色，代表了AI语音合成向大模型演进的方向。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | 作者: nvidia | 👍 348 | 📥 4,965
  - **一句话说明**：NVIDIA 专为流式场景优化的语音识别模型，具备“缓存感知”能力，在低延迟场景下极具实用价值。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 1,634 | 📥 3,057,541
  - **一句话说明**：Qwen3.6的社区去审查版，以极其庞大的下载量证明，开源社区对“无限制”模型存在巨大需求。

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** | 作者: unsloth | 👍 550 | 📥 711,706
  - **一句话说明**：Unsloth 为 Gemma 4 打造的高效 GGUF 量化版本，极低显存占用和高速推理是其风靡社区的关键。

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** & **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)** | 作者: OBLITERATUS, huihui-ai
  - **一句话说明**：围绕 Gemma 4 的社区微调版本，移除了安全限制或进行“去审查”处理，与 HauhauCS 的模型共同构成了强大的“无审查”微调浪潮。

---

#### 📡 生态信号

1.  **Gemma 4 与 MoE 统治榜单**：Google 的 **Gemma 4 系列**（12B/26B）及其社区衍生版占据了榜单近三分之一的席位，显示其已成为当前最活跃的开源模型基座。同时，**NVIDIA Nemotron**、**DeepSeek V4 Pro** 等均采用 MoE 架构，表明稀疏化、超大参数量的 MoE 已成为行业主流方向。
2.  **量化与去审查是社区核心驱动力**：Unsloth 提供的 **GGUF 量化版**（如 Gemma 4）下载量是原版的数倍，表明自部署社区极度依赖低门槛方案。同时，以 **HauhauCS** 和 **OBLITERATUS** 为代表的“去审查”微调版下载量极高，开源社区对于模型“自由度”的需求已不容忽视。
3.  **NVIDIA 全面布局 vs. 开源二线玩家**：NVIDIA 从视觉定位（LocateAnything）、超大规模语言模型（Nemotron-3）、流式语音（ASR）到模型服务，进行了全栈布局。与之相比，**ByteDance**、**StepFun**、**JetBrains** 等公司则更侧重于特定场景（视频、代码、边缘）的模型发布，形成差异化竞争。

---

#### 💎 值得探索

1.  **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
    - **理由**：作为本周热度之王，它是衡量当前大模型能力上限的基准。无论是研究其对话能力，还是分析其模型架构，都极具价值。

2.  **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) & [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
    - **理由**：这是“官方模型 + 社区优化”的完美搭档。先了解原版强大的多模态能力，再体验 GGUF 量化后的高效部署，能直观感受技术堆栈的全链路。

3.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    - **理由**：代表了“视觉感知 + 大语言模型”融合的前沿。它的成功表明，除生成外，“理解与定位”同样是 AI 视觉能力的关键突破点，值得任何从事具身智能或图像理解研究的开发者尝试。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*