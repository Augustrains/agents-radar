# Hugging Face 热门模型日报 2026-06-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-24 01:58 UTC

---

好的，作为AI模型生态分析师，这是基于2026年6月24日数据为您生成的《Hugging Face 热门模型日报》。

---

### **《Hugging Face 热门模型日报》2026-06-24**

#### **1. 今日速览**

本周生态焦点集中在**深度推理与多模态融合**两大方向。深度求索的 **DeepSeek-V4-Pro** 以绝对优势领跑，展示了社区对前沿Open-LLM的巨大热情。多模态方面，**Google 的Gemma 4系列**（特别是 any-to-any 统一架构）和 **MiniMax-M3** 持续热门，标志着“全能型”模型成为主流趋势。此外，**GLM-5.2** 和一系列基于 **Qwen3.6** 的MoE模型在社区中掀起微调与量化浪潮，推动大模型“平民化”部署。

#### **2. 热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** （deepseek-ai | 点赞: 5,030 | 下载: 2.2M）
  - **一句话说明**：本周绝对王者，在推理、代码和长文本任务上展现出令人瞩目的对话能力，是开源社区挑战闭源前沿的最新里程碑。

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** （google | 点赞: 1,156 | 下载: 2.0M）
  - **一句话说明**：Google Gemma 4代指令微调版，采用令人惊叹的any-to-any架构，兼具文本和图像理解能力，是全能型AI agent的理想基座。

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** （zai-org | 点赞: 2,198 | 下载: 40.1K）
  - **一句话说明**：智谱新一代MoE模型，优化了DS架构，在对话和指令跟随上表现出差异化优势，迅速跻身第一阵营。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** （nvidia | 点赞: 2,317 | 下载: 274K）
  - **一句话说明**：NVIDIA发布的精准目标定位模型，在图像中根据文本指令进行像素级定位，极大降低了视觉Agent的开发门槛。

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** （MiniMaxAI | 点赞: 1,221 | 下载: 131K）
  - **一句话说明**：MiniMax第三代多模态大模型，在视觉理解和复杂推理上表现出色，是市场上最受欢迎的国产多模态模型之一。

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** （moonshotai | 点赞: 976 | 下载: 447K）
  - **一句话说明**：月之暗面发布的代码专家模型，同样具备视觉能力，通过压缩技术实现更高效的代码生成与理解。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** （yuxinlu1 | 点赞: 2,241 | 下载: 456K）
  - **一句话说明**：基于Gemma-4-12B的代码特化微调版，通过“fable”数据组合实现强大的代码生成与推理能力，并以GGUF格式利于部署。

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-Embedding-350M)** （LiquidAI | 点赞: 115 | 下载: 10.1K）
  - **一句话说明**：Liquid AI推出的轻量级文本嵌入模型，仅350M参数，专注于语义相似度，是RAG pipelines的高效选择。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** （HauhauCS | 点赞: 2,158 | 下载: 3.9M）
  - **一句话说明**：本周下载量冠军！基于Qwen3.6的MoE模型，去审查且经过激进风格微调，印证了社区对“无限制”和“强个性”模型的高需求。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** （unsloth | 点赞: 303 | 下载: 55.8K）
  - **一句话说明**：知名团队Unsloth对GLM-5.2进行了高效量化，让用户在普通硬件上就能运行这款最新的MoE模型，解决了可及性问题。

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** （zai-org | 点赞: 149 | 下载: 395K）
  - **一句话说明**：GLM-5.2官方发布的FP8（8位浮点）量化版，在几乎不损失精度的情况下大幅降低显存占用，推动了模型大规模推理落地。

#### **3. 生态信号**

- **DeepSeek与Gemma 4双龙戏珠**：**DeepSeek-V4-Pro** 在纯文本领域确立了开源领先地位，而 **Gemma 4 Unified**（any-to-any）则代表了多模态融合的极致，这两个模型家族成为社区二创和生态建设的两大锚点。
- **MoE与量化成为常态**：随着参数规模持续扩大，**MoE (Mixture of Experts)** 架构（如GLM-5.2、Qwen3.6）成为标配。同时，**GGUF** 和 **FP8** 格式的模型下载量极高，表明社区从“我有模型”转向“我用模型”，对消费级硬件易用性的需求已成刚需。
- **“无审查”与“特化”并行：高下载量的“无审查”模型（如Qwen3.6变体）以及“代码”特化模型（如gemma-4 coder）显示，通用模型之外，满足特定细分场景（娱乐、专业开发、Agent）的定制模型具有极强的生命力。

#### **4. 值得探索**

1.  **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** （google | 点赞: 1,055 | 下载: 948K）
    - 尝试理由：这是“生成式AI的交叉融合”的代表。它结合了扩散模型与文本生成，是探索生成式AI边界的绝佳模型。其MoE设计（26B总参，4B激活）使其在效率与能力间取得了平衡。

2.  **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** （nvidia | 点赞: 657 | 下载: 41K）
    - 尝试理由：语音交互是下一代AI Agent的关键入口。NVIDIA这款流式语音识别模型以其极低的缓存和0.6B的超小参数，为在边缘设备上实现实时、高质量语音助手提供了可能，值得所有硬件开发者关注。

3.  **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** （microsoft | 点赞: 322 | 下载: 4.3K）
    - 尝试理由：在所有人追求更大上下文时，微软的“FastContext”反其道而行，专注于提升长上下文的处理效率。对于构建需要精确检索和快速响应的RAG或Agent应用来说，这个模型的研究价值和应用潜力被严重低估。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*