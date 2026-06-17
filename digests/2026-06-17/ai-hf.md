# Hugging Face 热门模型日报 2026-06-17

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-17 02:29 UTC

---

好的，这是为您生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-17**

#### **今日速览**

本周 Hugging Face 生态由 **DeepSeek-V4-Pro** 的持续爆发主导，其周点赞数接近 5000，下载量逼近 300 万，是当前社区绝对的中心。同时，**Qwen3.6** 系列模型家族表现强劲，多个变体（包括大规模 MoE、代码优化和无审查版本）进入榜单，展现出强大的生态影响力。多模态趋势依然明显，nvidia 的 **LocateAnything-3B** 和 google 的 **DiffusionGemma** 提供了视觉理解与生成的新范式。此外，社区微调与量化活动异常活跃，尤其是 **unsloth** 团队持续为热门模型提供高效的 GGUF 版本，极大地降低了部署门槛。

#### **热门模型**

##### 🧠 语言模型

-   [**deepseek-ai/DeepSeek-V4-Pro**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) — **作者**: deepseek-ai | **点赞**: 4,896 | **下载**: 2,829,747
    -   *一句话说明*: DeepSeek 最新一代旗舰大模型，凭借其卓越的综合能力和开源权重，成为当前社区最受追捧的对话模型。

-   [**moonshotai/Kimi-K2.7-Code**](https://huggingface.co/moonshotai/Kimi-K2.7-Code) — **作者**: moonshotai | **点赞**: 802 | **下载**: 102,206
    -   *一句话说明*: 月之暗面推出的代码专用模型，采用压缩张量技术，在代码生成任务上表现突出，迅速获得了开发者社区的关注。

-   [**microsoft/FastContext-1.0-4B-SFT**](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT) — **作者**: microsoft | **点赞**: 163 | **下载**: 192
    -   *一句话说明*: 微软发布的小型高效模型，专为超长上下文推理场景优化，虽然下载量不大，但其“快速上下文”的技术方向值得关注。

##### 🎨 多模态与生成

-   [**nvidia/LocateAnything-3B**](https://huggingface.co/nvidia/LocateAnything-3B) — **作者**: nvidia | **点赞**: 2,104 | **下载**: 98,698
    -   *一句话说明*: NVIDIA 推出的视觉定位模型，能够根据文本描述精准定位图像中的任意物体，是视觉理解和智能交互的重要基础模型。

-   [**google/diffusiongemma-26B-A4B-it**](https://huggingface.co/google/diffusiongemma-26B-A4B-it) — **作者**: google | **点赞**: 949 | **下载**: 375,974
    -   *一句话说明*: Google 的混合专家架构（MoE）多模态模型，结合图像理解与文本生成能力，是新一代多模态对话的代表作。

-   [**ideogram-ai/ideogram-4-fp8**](https://huggingface.co/ideogram-ai/ideogram-4-fp8) — **作者**: ideogram-ai | **点赞**: 560 | **下载**: 12,466
    -   *一句话说明*: Ideogram 第四代文本到图像模型，采用了 FP8 量化，在保持高质量图像生成能力的同时，显著降低了推理资源需求。

-   [**Qwen/Qwen3.6-35B-A3B**](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) — **作者**: Qwen | **点赞**: 2,137 | **下载**: 3,360,615
    -   *一句话说明*: Qwen3.6 系列的“视觉大脑”，一个 35B 参数的 MoE 模型，以其在多模态任务上的强大表现和极高的社区下载量成为本周焦点。

-   [**prefeitura-rio/Rio-3.5-Open-397B**](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B) — **作者**: prefeitura-rio | **点赞**: 315 | **下载**: 189,744
    -   *一句话说明*: 一个基于 Qwen3.5 MoE 架构的 397B 超大参数多模态模型，是社区对超大规模开源模型探索的典型案例。

##### 🔧 专用模型

-   [**nvidia/nemotron-3.5-asr-streaming-0.6b**](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) — **作者**: nvidia | **点赞**: 475 | **下载**: 5,777
    -   *一句话说明*: NVIDIA 推出的流式语音识别模型，支持实时 ASR，为语音交互应用提供了高效、精准的开源解决方案。

-   [**CohereLabs/North-Mini-Code-1.0**](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) — **作者**: CohereLabs | **点赞**: 412 | **下载**: 12,129
    -   *一句话说明*: Cohere 发布的代码能力模型，专为编码任务优化，是“North”系列中主打代码方向的小型模型。

-   [**bosonai/higgs-audio-v3-tts-4b**](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) — **作者**: bosonai | **点赞**: 465 | **下载**: 43,361
    -   *一句话说明*: 针对文本到语音（TTS）任务优化的 4B 参数模型，展示了多模态能力向音频生成的延伸。

##### 📦 微调与量化

-   [**HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) — **作者**: HauhauCS | **点赞**: 1,892 | **下载**: 2,716,651
    -   *一句话说明*: 基于 Qwen3.6 的社区“未经审查”微调版，因放宽了内容限制而广受争议和追捧，下载量极高。

-   [**unsloth/gemma-4-12b-it-GGUF**](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) — **作者**: unsloth | **点赞**: 633 | **下载**: 1,009,602
    -   *一句话说明*: **unsloth** 团队为 Google Gemma-4 提供的 GGUF 量化版，大幅降低了该大模型的本地部署门槛，因此下载量破百万。

-   [**yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF**](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) — **作者**: yuxinlu1 | **点赞**: 1,185 | **下载**: 60,921
    -   *一句话说明*: 对 Gemma-4 进行代码方向微调并量化的模型，展示了社区在特定领域对基础模型进行优化的活跃度。

-   [**DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF) — **作者**: DavidAU | **点赞**: 370 | **下载**: 366,279
    -   *一句话说明*: 一个极具特色的社区微调模型，融合了“Claude风格”和“无限制思考”等元素的 Qwen 变体，反映了用户对新型对话风格的追求。

#### **生态信号**

本周生态显示，**DeepSeek-V4-Pro** 正成为社区新的“锚点”模型，其影响力堪比曾经的 Llama 系列。**Qwen3.6** 系列则展现了极强的家族生态，其 MoE 架构的普及刺激了大量基于 Qwen3.6 的微调和量化活动。值得注意的是，**无审查（Uncensored）** 模型的下载量极高（如 HauhauCS 和 DavidAU 的模型），表明社区对内容限制的普遍诉求。此外，**unsloth** 等量化服务商已发展为生态关键一环，对顶级模型（如 Gemma-4, Kimi-K2.7）的快速适配能力，直接决定了该模型的普及速度。开源权重模型在热门榜单中占据绝对主导地位，竞争激烈。

#### **值得探索**

1.  **nvidia/LocateAnything-3B**: 如果你对视觉 AI 感兴趣，这个模型是必试之物。它展示了将定位从检测升级为任意目标的潜力，是构建智能视觉代理（Agent）的核心组件。
2.  **deepseek-ai/DeepSeek-V4-Pro**: 作为社区新王，任何想了解当前开源 LLM 能力天花板的人都应该下载体验。它的对话能力和推理表现是评测其他模型的基准。
3.  **unsloth/gemma-4-12b-it-GGUF**: 即使是微调大佬，也建议试试这个。它几乎是无感地在本地运行一个 12B 多模态模型的最高效方式，可以用于快速原型验证和本地私有化部署。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*