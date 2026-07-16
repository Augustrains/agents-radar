# Hugging Face 热门模型日报 2026-07-16

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-16 01:19 UTC

---

好的，作为AI模型生态分析师，以下是为您准备的《Hugging Face 热门模型日报》。

---

# 🤗 Hugging Face 热门模型日报 (2026-07-16)

## 📰 今日速览

本周Hugging Face趋势榜呈现出三大显著特征：**极致量化浪潮**、**MOE架构全面爆发**与**多模态应用下沉**。`prism-ml` 推出的1位和2位量化模型（如`Ternary-Bonsai-27B`）引发了社区对模型“瘦身”极限的探索；基于Qwen 3.5/3.6架构的MoE变体（如`HauhauCS`及`InternScience`的模型）成为下载量榜首常客。此外，以`Qwythos-9B`系列为首的大规模合成数据微调模型，以及百度、腾讯等大厂推出的专用OCR与视频生成模型（如`Unlimited-OCR`、`Hy3`），标志着开源模型正从通用对话向高精度、高性能的垂类应用快速渗透。GGUF格式的量化模型依然是社区下载和部署的主流选择。

## 🏆 热门模型

### 🧠 语言模型 (LLM, 对话模型)

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
    *   **作者**: zai-org | **点赞**: 3,998 | **下载**: 489,611
    *   **说明**: 智谱AI的MoE大模型5.2版本，凭借强大的基础能力和社区高期望值，获得本周最高点赞量。

2.  **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
    *   **作者**: empero-ai | **点赞**: 2,214 | **下载**: 2,006,265
    *   **说明**: 基于Qwen 3.5的9B模型，使用合成数据（Mythos-5）微调并量化，推理能力强，下载量突破200万，是“小模型+强数据”路线的代表。

3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    *   **作者**: HauhauCS | **点赞**: 2,760 | **下载**: 2,443,871
    *   **说明**: 基于Qwen 3.6的MoE 35B模型（激活3B），主打无审查和“激进”风格，量化后下载量极高，反映了社区对“高性能MoE+风格控制”的需求。

4.  **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**
    *   **作者**: deepreinforce-ai | **点赞**: 893 | **下载**: 1,533,354
    *   **说明**: 一个35B参数量的通用LLM的GGUF量化版，下载量惊人，表明社区对“黄金尺寸”模型（30B-40B）的量化版本有巨大需求。

5.  **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**
    *   **作者**: yuxinlu1 | **点赞**: 1,198 | **下载**: 468,629
    *   **说明**: 基于Gemma 4的12B模型，高度异化，专为Agentic和Coding任务微调，并加入了合成数据（Fable5），是“专业Agent模型”的典型代表。

6.  **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**
    *   **作者**: tencent | **点赞**: 800 | **下载**: 10,406
    *   **说明**: 腾讯发布的新一代基础大模型，作为Hunyuan系列的迭代版本，下载量迅速攀升，表明大厂持续投入基础模型开源。

7.  **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**
    *   **作者**: InternScience | **点赞**: 554 | **下载**: 30,539
    *   **说明**: 基于Qwen 3.5的MoE模型，专为Agent任务设计，点赞数高，代表了社区对未来智能体模型架构的浓厚兴趣。

8.  **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nvidia/Nemotron-Labs-Audex-30B-A3B)**
    *   **作者**: nvidia | **点赞**: 156 | **下载**: 1,332
    *   **说明**: NVIDIA的“智能体音频专家”模型，30B参数MoE架构，虽然刚发布不久，但代表了“音频+Agent”的前沿探索方向。

### 🎨 多模态与生成 (图像、视频、音频、文本到X)

1.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
    *   **作者**: baidu | **点赞**: 2,002 | **下载**: 1,715,301
    *   **说明**: 百度开源的OCR模型，处理能力强大，下载量超170万，证明了高精度、通用的OCR工具具有巨大的实际应用市场。

2.  **[unsloth/Qwen3.6-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.6-27B-NVFP4)**
    *   **作者**: unsloth | **点赞**: 208 | **下载**: 1,599,150
    *   **说明**: 与`HauhauCS`类似，是Qwen 3.6的27B多模态MoE模型，采用NVFP4（NVIDIA的4位浮点量化），展示了顶级量化厂商对最新大模型的适配。

3.  **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**
    *   **作者**: OpenMOSS-Team | **点赞**: 215 | **下载**: 65,109
    *   **说明**: 专注语音转文字与说话人分离的模型，下载量高，满足了音频处理领域的刚需。

4.  **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)**
    *   **作者**: bottlecapai | **点赞**: 365 | **下载**: 6,208
    *   **说明**: 基于Qwen 3.6的多模态模型，专注于增强模型的“思考”能力（推理链），代表了“推理+视觉”的融合趋势。

5.  **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)**
    *   **作者**: conradlocke | **点赞**: 307 | **下载**: 0
    *   **说明**: 用于Krea-2模型的图像编辑LoRA，主打身份保持，是社区垂直微调的典型产物。

6.  **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)**
    *   **作者**: robbyant | **点赞**: 99 | **下载**: 0
    *   **说明**: “世界模型”概念的落地版，实现图像到视频的生成（I2V），代表了视频生成领域的技术演进。

7.  **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)**
    *   **作者**: Alissonerdx | **点赞**: 154 | **下载**: 0
    *   **说明**: 基于LTX-Video模型的LoRA，用于视频生成中的人脸ID保持，是“身份保留”技术向视频领域扩展的缩影。

8.  **[mgwr/M87](https://huggingface.co/mgwr/M87)**
    *   **作者**: mgwr | **点赞**: 127 | **下载**: 2,408
    *   **说明**: 基于Krea-2-Turbo的LoRA，用于生成特定风格的图像，是图像生成社区生态活跃的体现。

### 🔧 专用模型 (代码、数学、金融、嵌入)

1.  **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**
    *   **作者**: froggeric | **点赞**: 917 | **下载**: 0
    *   **说明**: 修复了Qwen系列模型的聊天模板，小而实用。高点赞数反映了社区对“模型生态工具和厨艺”的认可。

2.  **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)**
    *   **作者**: Cactus-Compute | **点赞**: 236 | **下载**: 571
    *   **说明**: 专为函数调用（Function Calling）和工具使用（Tool Use）设计的JAX模型，代表了模型向“工具调用专家”发展的新方向。

### 📦 微调与量化 (社区微调、GGUF、AWQ)

1.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**
    *   **作者**: prism-ml | **点赞**: 467 | **下载**: 23
    *   **说明**: 开创性的“三进制”量化模型（2-bit），将27B模型压缩到极致，在趋势榜上引起了关于“极限压缩”和“边缘部署”的广泛讨论。

2.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**
    *   **作者**: prism-ml | **点赞**: 266 | **下载**: 513
    *   **说明**: 同系列的1-bit量化版本，进一步探索了量化的下限，与前一个模型共同定义了“极致量化”的生态信号。

3.  **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)**
    *   **作者**: GnLOLot | **点赞**: 250 | **下载**: 89,892
    *   **说明**: 在1B小模型上进行合成数据微调并量化，下载量近9万，表明“小模型+强蒸馏”是活跃的实验方向。

4.  **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)**
    *   **作者**: AngelSlim | **点赞**: 107 | **下载**: 0
    *   **说明**: 紧随腾讯发布`Hy3`，社区迅速推出的GGUF版本，体现了对最新大模型进行量化部署的社区生态敏感度。

5.  **[jlnsrk/GLM-5.2-colibri-int4](https://huggingface.co/jlnsrk/GLM-5.2-colibri-int4)**
    *   **作者**: jlnsrk | **点赞**: 110 | **下载**: 2,188
    *   **说明**: 对GLM-5.2的CPU优化版INT4量化，专为Intel平台优化，代表了“模型软硬件协同优化”的趋势。

6.  **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)**
    *   **作者**: robbyant | **点赞**: 111 | **下载**: 700
    *   **说明**: 采用MoE架构的视频生成模型，是“MoE”和“视频生成”两个热点的结合。

## 🌐 生态信号

本周生态释放出几个强烈信号：

*   **模型家族“Qwen”与“MoE”双核驱动**：Qwen 3.5/3.6系列的MoE变体在榜单上占据主导地位，无论是HauhauCS、InternScience还是思科（bottlecapai）的模型，都显示出社区对“高精度但低激活参数”架构的极度偏爱。`GLM-5`、`Nemotron Labs Audex`等模型的加入，确认了**2026年是MoE架构全面爆发之年**。
*   **“压缩技术”的军备竞赛**：`prism-ml`的1-bit/2-bit模型，`unsloth`的NVFP4量化，以及`jlnsrk`的INT4 CPU优化，共同指向了**将强大模型塞入有限设备**的核心矛盾。GGUF格式已成为“量化行动”的统一载体，下载量遥遥领先。
*   **开源权重的“军备竞赛”依然激烈，但焦点转移**：大厂（腾讯、百度、NVIDIA）依然在发布顶级权重。然而，社区的热度已从“谁会发布更强的模型”转向“谁能在小模型上微调出最强逻辑”以及“谁能提供最极致的量化部署方案”。

## 🔭 值得探索

1.  **prism-ml/Ternary-Bonsai-27B-gguf**：强烈推荐对**模型压缩和端侧部署**感兴趣的开发者和研究者关注。它挑战了“精度-大小”的极限，是探索未来手机、IoT设备上运行高性能LLM的绝佳实验对象。

2.  **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF**：如果您的方向是**Agent开发或代码生成**，请务必尝试此模型。复杂的命名背后是精心设计的合成数据微调流程，它将通用模型改造成了一个专注于“行动”和“完成任务”的专家，代表了LLM应用的下一个风口。

3.  **InternScience/Agents-A1**：如果您对**智能体（Agent）的基础模型架构**感兴趣，这个模型值得深入。它和`needle`模型一起，指明了从“通用对话”到“工具调用与规划”的范式转变，是研究下一代AI交互方式的重要样本。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*