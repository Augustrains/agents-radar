# Hugging Face 热门模型日报 2026-06-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-22 02:30 UTC

---

好的，作为AI模型生态分析师，以下是基于您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年6月22日**

#### **今日速览**

今日Hugging Face生态呈现三大趋势：**第一，顶级模型垄断地位依旧，但社区微调版本百花齐放。** DeepSeek-V4-Pro以绝对优势领跑，而围绕Qwen和Gemma-4的社区衍生模型（如量化、微调版）占据榜单半壁江山。**第二，多模态与Coding成为主战场。** Qwen3.6系列凭借强大的视觉-语言能力霸榜，而Gemma-4系列则在代码和Agentic领域展现出强劲势头。**第三，量化模型（GGUF）生态空前活跃。** 几乎所有热门模型都被社区迅速转化为GGUF格式，极大降低了本地部署门槛。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **DeepSeek-V4-Pro**（[链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)）
    *   作者：deepseek-ai | 点赞：4,999 | 下载：2,611,991
    *   一句话说明：DeepSeek最新旗舰模型，凭借强大的通用对话能力获得最高点赞，是当前开源社区最受瞩目的重量级模型。

*   **zai-org/GLM-5.2**（[链接](https://huggingface.co/zai-org/GLM-5.2)）
    *   作者：zai-org | 点赞：1,829 | 下载：27,413
    *   一句话说明：智谱AI的GLM系列最新MoE模型，采用DSA架构，在中文对话和推理任务上表现出色。

*   **google/gemma-4-12B-it**（[链接](https://huggingface.co/google/gemma-4-12B-it)）
    *   作者：google | 点赞：1,129 | 下载：1,815,370
    *   一句话说明：Google新一代Gemma-4的指令微调版本，支持“any-to-any”多模态，下载量巨大，成为社区微调与量化的热门基底模型。

*   **nex-agi/Nex-N2-Pro**（[链接](https://huggingface.co/nex-agi/Nex-N2-Pro)）
    *   作者：nex-agi | 点赞：342 | 下载：7,872
    *   一句话说明：基于Qwen3.5 MoE架构的专业级模型，定位高端通用对话与文本生成。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **Qwen/Qwen3.6-35B-A3B**（[链接](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)）
    *   作者：Qwen | 点赞：2,197 | 下载：5,148,673
    *   一句话说明：Qwen最新一代MoE视觉语言模型（VLM），凭借35B总参/3B激活的极致效率，成为当前多模态领域的下载量冠军。

*   **nvidia/LocateAnything-3B**（[链接](https://huggingface.co/nvidia/LocateAnything-3B)）
    *   作者：nvidia | 点赞：2,243 | 下载：241,845
    *   一句话说明：英伟达发布的定位与分割基础模型，用户可通过文本或视觉提示在图像中“定位任何物体”，精确度极高。

*   **MoonshotAI/Kimi-K2.7-Code**（[链接](https://huggingface.co/moonshotai/Kimi-K2.7-Code)）
    *   作者：moonshotai | 点赞：945 | 下载：363,308
    *   一句话说明：月之暗面推出的Kimi系列代码视觉模型，专注于理解代码截图和编程图表，开辟了“代码理解”新赛道。

*   **google/diffusiongemma-26B-A4B-it**（[链接](https://huggingface.co/google/diffusiongemma-26B-A4B-it)）
    *   作者：google | 点赞：1,035 | 下载：762,861
    *   一句话说明：Google结合Gemma与扩散模型的创新之作，用户可通过对话指令直接生成与编辑图像，开创了新的交互范式。

*   **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**（[链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)）
    *   作者：HauhauCS | 点赞：2,079 | 下载：3,966,691
    *   一句话说明：Qwen3.6的激进社区“无审查”微调版，去除了安全限制并增强了“侵略性”输出，下载量惊人，反映了社区对模型自由度的强烈需求。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**（[链接](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)）
    *   作者：yuxinlu1 | 点赞：2,089 | 下载：358,677
    *   一句话说明：Gemma-4的社区代码微调版，通过Fable5和Composer数据增强在编程任务上表现卓越，是当前最火的编程模型之一。

*   **nvidia/nemotron-3.5-asr-streaming-0.6b**（[链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)）
    *   作者：nvidia | 点赞：612 | 下载：27,275
    *   一句话说明：英伟达推出的超轻量（0.6B）流式语音识别模型，专为低延迟实时语音交互场景设计。

*   **CohereLabs/North-Mini-Code-1.0**（[链接](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)）
    *   作者：CohereLabs | 点赞：474 | 下载：19,551
    *   一句话说明：Cohere新发布的North系列代码模型，采用MoE架构，主打代码生成与理解，是企业级代码助手的有力竞争者。

*   **LiquidAI/LFM2.5-Embedding-350M**（[链接](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)）
    *   作者：LiquidAI | 点赞：93 | 下载：7,726
    *   一句话说明：Liquid AI推出的轻量级文本嵌入模型，专为RAG和语义搜索等场景设计。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**（已在上文介绍）
*   **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**（已在上文介绍）
*   **unsloth/GLM-5.2-GGUF**（[链接](https://huggingface.co/unsloth/GLM-5.2-GGUF)）
    *   作者：unsloth | 点赞：227 | 下载：32,260
    *   一句话说明：知名量化工具Unsloth提供的GLM-5.2 GGUF版本，极大方便了用户在本地运行这一强大的中文MoE模型。

#### **生态信号**

*   **模型家族混战，Qwen与Gemma-4两强争霸：** 本周榜单显示，阿里Qwen系列（3.6）和Google Gemma-4系列无疑是生态中热度最高的两大阵营。两者都提供强大的基础模型和丰富的社区衍生品，竞争白热化。
*   **“去中心化”的微调与量化：** 开源模型生态正从“发布一个新模型”转向“极致地改造一个模型”。社区通过微调（如Coder、Uncensored）和量化（GGUF）进行二次创新，其受欢迎程度甚至超过部分官方模型。这极大地降低了使用门槛，激发了更多应用。
*   **MoE架构成为主流：** 从DeepSeek-V4到Qwen3.6、Gemma-4，再到GLM-5.2，几乎所有重磅模型都采用了混合专家（MoE）架构，证明“大而稀疏”是当前平衡性能与效率的最佳路径。

#### **值得探索**

1.  **Qwen/Qwen3.6-35B-A3B**：如果你想体验最前沿的多模态能力，这是当前的首选。其3B激活的高效设计使其在消费级硬件上也有运行可能。
2.  **deepseek-ai/DeepSeek-V4-Pro**：如果你追求纯粹的通用语言模型“天花板”，这个模型是社区投票的人气之王。其强大的推理和对话能力值得深入研究。
3.  **nvidia/LocateAnything-3B**：如果你对视觉AI落地感兴趣，这个定位模型非常值得尝试。它将自然语言与图像定位完美结合，在图像编辑、机器人、自动驾驶等领域潜力巨大。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*