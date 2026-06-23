# Hugging Face 热门模型日报 2026-06-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-23 01:58 UTC

---

好的，作为AI模型生态分析师，这是为您生成的2026年6月23日Hugging Face热门模型日报。

---

### 📈 Hugging Face 热门模型日报 | 2026年6月23日

#### **1. 今日速览**

今日Hugging Face生态呈现三大看点：**“巨型集群”效应**与**“MoE瘦身”技术**并行爆发。DeepSeek-V4-Pro以压倒性优势登顶榜单，验证了超大参数规模与专业MoE架构的强大吸引力。同时，以Gemma 4和GLM-5.2为代表的新一代MoE模型家族正在快速形成生态，社区通过GGUF量化等方式将其推向更广泛的部署场景。此外，代码与Agent能力成为模型竞争的核心焦点，从专用编码模型到通用Agent框架，开发者对“能干活”的模型需求空前旺盛。

#### **2. 热门模型分类盘点**

##### 🧠 语言模型（LLM、对话模型、指令微调）

-   **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** (deepseek-ai, 👍 5,012, 📥 2.4M)
    -   **一句话说明**: 今日绝对王者，DeepSeek最新旗舰模型，凭借强大的MoE架构与推理能力，成为社区关注的绝对焦点。
-   **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** (google, 👍 1,138, 📥 1.9M)
    -   **一句话说明**: Google Gemma 4家族的“通用旗舰”，支持“任何输入到任何输出”，强大的多模态能力使其成为全能型选手。
-   **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** (MiniMaxAI, 👍 1,209, 📥 120K)
    -   **一句话说明**: MiniMax最新多模态大模型，在视觉理解和生成任务上表现亮眼，代表了主流AI公司对多模态赛道的最新押注。
-   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** (zai-org, 👍 2,038, 📥 33.6K)
    -   **一句话说明**: 智谱AI的GLM系列最新作，采用MoE-DSA架构，在对话质量和效率上达到新高度，社区热度极高。
-   **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** (CohereLabs, 👍 481, 📥 21K)
    -   **一句话说明**: Cohere推出的编程专用MoE模型，外形小巧但能力强大，在代码生成任务上展现出与其体积不符的惊人表现。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

-   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-...-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** (HauhauCS, 👍 2,116, 📥 4.1M)
    -   **一句话说明**: 社区量化与“去审查”文化的产物，基于Qwen3.6的MoE模型，下载量惊人，反映了特定用户群体对“无限制”视觉模型的需求。
-   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (nvidia, 👍 2,291, 📥 248K)
    -   **一句话说明**: NVIDIA推出的“万物定位”模型，3B参数即可高效完成图片中的目标分割与定位，是视觉任务中的明星模型。
-   **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** (google, 👍 1,049, 📥 874K)
    -   **一句话说明**: Google将Diffusion与Gemma融合的创新模型，通过视觉理解与扩散生成的无缝结合，开辟了多模态交互的新范式。
-   **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** (ostris, 👍 102, 📥 3.2K)
    -   **一句话说明**: 社区为Ideogram 4模型打造的LoRA微调版本，旨在加速图像生成过程，代表了文生图领域的微调与优化趋势。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

-   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** (moonshotai, 👍 963, 📥 413K)
    -   **一句话说明**: 月之暗面推出的Kimi系列编码增强版，以“压缩张量”技术实现了高性能与低资源占用的平衡，是代码开发者的新利器。
-   **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** (nvidia, 👍 631, 📥 34.9K)
    -   **一句话说明**: NVIDIA推出的流式语音识别模型，仅0.6B参数即可实现低延迟、高精度的实时语音转文字，边缘部署潜力巨大。
-   **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-Embedding-350M)** (LiquidAI, 👍 100, 📥 8.8K)
    -   **一句话说明**: Liquid AI的第二代嵌入模型，专注于句子相似度任务，为RAG等检索系统提供了强大的句向量基础。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

-   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** (yuxinlu1, 👍 2,171, 📥 415K)
    -   **一句话说明**: Gemma 4编码模型的超精细GGUF量化版，下载量极高，说明社区对高质量、可直接本地运行的编码模型需求巨大。
-   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** (empero-ai, 👍 137, 📥 6.6K)
    -   **一句话说明**: 社区基于Qwen3.5微调的“哲思”型模型，其GGUF版本使本地化体验成为可能，代表了社区对“风格化”和“角色扮演”模型的持续热情。
-   **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** (Jackrong, 👍 281, 📥 215K)
    -   **一句话说明**: 基于Qwen3.6的编码MoE模型的GGUF量化版，下载量高，再次印证了社区对“大参数MoE模型+GGUF量化”这一组合模式的追捧。

#### **3. 生态信号**

-   **模型家族群雄并起**: **DeepSeek-V4**、**Gemma 4**、**GLM-5.2**和**Qwen3.6**是当前最被关注的四大模型家族。它们均采用了MoE架构，并围绕其衍生出大量社区微调、量化变体，形成了强大的生态护城河。
-   **开源权重的“军备竞赛”**: 榜单前列几乎被开源模型占据，且多为顶尖机构出品。DeepSeek-V4-Pro的发布标志着开源社区正在与闭源模型进行参数规模和能力的直接竞争，社区对“开源胜过闭源”的信心增强。
-   **量化成为“标配”**: 几乎所有主流模型（尤其是大参数MoE）发布后，都会快速出现其GGUF版本。榜单中LLM模型有一半以上是量化版，这表明压缩和部署效率已成为模型获得广泛社区下载的关键，GGUF已从“玩具”变为“生产力工具”。

#### **4. 值得探索**

-   **🗺️ [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**: 强烈推荐研究。它将扩散生成与大语言模型的理解能力深度耦合，代表了多模态模型发展的新范式，其“视觉理解→图像生成”的端到端能力极具创新性。
-   **💻 [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**: 如果你对本地编码助手感兴趣，这个模型是必选项。它展示了社区如何将一个强大的12B编码模型压缩到可本地运行的极限，是“大模型边缘化”的典型案例。
-   **🔍 [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**: 如果你从事计算机视觉或机器人相关研究，这个模型值得一试。它在极小的参数量下实现了强大的零样本目标定位能力，在专业任务上的“小而美”思路值得关注。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*