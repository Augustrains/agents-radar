# Hugging Face 热门模型日报 2026-07-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-24 01:21 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-24**

#### **今日速览**

本周 Hugging Face 生态呈现三大核心趋势：**多模态化**与**极致量化**是绝对主流。`Qwen3.6` 系列成为社区微调与量化的“明星底座”，衍生出大量具备特定风格（如无审查、角色扮演）的变体。同时，模型效率追求进入“**比特级**”竞争，`prism-ml` 推出的 1-bit 和 2-bit `Bonsai` 模型吸引了大量关注。在底层技术方面，**MoE（混合专家）**架构在 `GLM-5.2` 和多个 `Qwen3.6` 变体中持续渗透，而`baidu`的`Unlimited-OCR`凭借通用性登顶下载与热度双榜。此外，音频领域也在复苏，`Qwen3-TTS` 和 `nvidia` 的流式ASR模型表现亮眼。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - `zai-org` | 👍 4,370 | 📥 596,442
    *   **说明**：基于MoE架构的对话模型，凭借强大的语言理解与生成能力，获得了本周最高点赞数。
*   **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** - `google` | 👍 3,347 | 📥 12,666,488
    *   **说明**：Google 的31B指令微调多模态模型，下载量遥遥领先，反映了行业对头部大厂开源权重的强烈需求。
*   **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** - `upstage` | 👍 445 | 📥 362
    *   **说明**：Upstage 推出的250B参数级开源模型，虽然下载量不大，但其巨大的参数量级代表了开源社区在“大模型”赛道的持续探索。
*   **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** - `Nanbeige` | 👍 320 | 📥 4,532
    *   **说明**：轻量级高效语言模型，适合在资源受限环境下部署，体现了对小模型优化依然存在市场。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - `baidu` | 👍 2,885 | 📥 2,414,259
    *   **说明**：百度推出的通用OCR模型，将图像文字识别（OCR）能力集成到多模态框架中，因其极强的实用性成为本周“下载与点赞双冠王”。
*   **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** - `thinkingmachines` | 👍 1,508 | 📥 24,669
    *   **说明**：一个专注于对话式交互的多模态模型，成为本周关注度最高的新模型之一。
*   **[Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)** - `Qwen` | 👍 1,798 | 📥 2,497,020
    *   **说明**：Qwen 出品的定制语音文本转语音（TTS）模型，支持自定义音色，语音生成赛道热度回归。
*   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** - `moonshotai` | 👍 1,248 | 📥 766,522
    *   **说明**：Kimi 的代码专用多模态模型，结合视觉与代码理解能力，是针对编程场景的专用利器。
*   **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** - `nvidia` | 👍 926 | 📥 750,118
    *   **说明**：NVIDIA推出的流式自动语音识别（ASR）模型，在低延迟语音交互场景有重要应用。
*   **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** - `microsoft` | 👍 183 | 📥 411
    *   **说明**：微软的图像生成与编辑模型，代表了图像生成领域的持续创新。
*   **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** & **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** - `openbmb` | 👍 165 & 117 | 📥 408 & 306
    *   **说明**：OpenBMB 推出的具身智能（机器人）模型，分别处理机械臂操作与物体追踪，是多模态走向物理世界的标志性信号。
*   **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** - `ATH-MaaS` | 👍 257 | 📥 26,919
    *   **说明**：基于 Qwen3.5 的OCR专用多模态模型，与百度`Unlimited-OCR`共同印证了OCR在当下多模态中的优先地位。
*   **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** - `OpenMOSS-Team` | 👍 320 | 📥 111,598
    *   **说明**：结合转录与说话人日志（Diarization）的音频转文本模型，在会议、采访等场景有极高价值。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** - `fdtn-ai` | 👍 121 | 📥 2,747
    *   **说明**：标榜“安全”的1B参数生成模型，可能针对特定安全场景（如代码安全、内容过滤）进行了优化，代表了AI安全领域的模型需求。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[DavidAU/Qwen3.6-27B-Fable-Fusion...GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** & **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - `DavidAU` & `HauhauCS` | 👍 397 & 3,033 | 📥 334,847 & 2,027,080
    *   **说明**：`Qwen3.6`是本周最热门的基座模型之一，这些变体通过微调或量化，主打“无审查”和特定风格输出，满足了特定用户群体的差异化需求。
*   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** & **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** - `prism-ml` | 👍 983 & 620 | 📥 576,083 & 1,910,116
    *   **说明**：`prism-ml`推出的极低比特（2-bit/1-bit）量化模型，以其极致的压缩率和推理效率成为本周的“量化王”，下载量惊人。
*   **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** 及其衍生GGUF版 - `poolside` & `unsloth` | 👍 514 & 149 | 📥 13,285 & 28,542
    *   **说明**：`Laguna`系列模型以代码生成为核心，衍生出多个GGUF和NVFP4量化版本，形成了成熟的产品生态。
*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - `empero-ai` | 👍 2,438 | 📥 2,126,755
    *   **说明**：基于 `Qwen3.5` 并融合特定风格（Mythos）的社区微调量化模型，下载量极高，是社区创造力与量化技术结合的典范。
*   **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** - `bottlecapai` | 👍 528 | 📥 25,231
    *   **说明**：在 `Qwen3.6` 基础上针对推理能力进行优化的指令微调模型，强化了模型思考过程。
*   **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored...GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** - `LuffyTheFox` | 👍 117 | 📥 24,982
    *   **说明**：又一款基于 `Qwen3.6` MoE架构的极低比特量化无审查模型，反映了社区对“大模型+小激活”与无限制内容生成的双重追求。
*   **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** - `conradlocke` | 👍 515 | 📥 0
    *   **说明**：基于 `Krea-2` 的LoRA（低秩适应）模型，专门用于人脸身份编辑，代表了图像个性化微调的成熟应用。

---

#### **生态信号**

1.  **“Qwen宇宙”与“Bonsai”现象**：`Qwen3.6` 已构建起最活跃的社区生态，涌现出大量微调与量化分支，是当前开源社区的“最强孵化器”。同时，`prism-ml`的`Bonsai`系列通过极低比特（1-2 bit）量化模型，定义了“如何在消费级硬件上运行30B级别模型”的新标准，成为效率追求者的标杆。
2.  **开源权重的“军备竞赛”**：`google/gemma-4-31B-it`的千万级下载量与 `upstage/Solar-Open2-250B` 的发布表明，头部玩家（Google、Baidu、Upstage）仍在持续投入开源权重，且模型参数量级不断上探。开源模型在通用能力上与闭源模型的差距正在快速缩小。
3.  **微调活动百花齐放**：热门模型（尤其是Qwen系列）被大规模用于“无审查”、“角色扮演”等垂直领域的微调。这表明用户对基础模型的能力认可度很高，同时渴望个性化定制的自由度。量化的手法以GGUF和低比特为主，几乎成为社区模型的“标配”发布格式。

---

#### **值得探索**

1.  **🤖 [google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**：千万级下载量和高点赞数使其成为不容忽视的基准模型。无论是进行能力测试、二次微调还是对比研究，它都是当下最值得下载的“全能型”基础模型。
2.  **💡 [prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：如果你想探索AI推理的极限，这个1-bit模型值得深入研究。它代表了一种极致的效率思维，适合在无GPU或低显存环境中追求流畅对话体验的场景。
3.  **🖼️ [baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**：作为本周热度与下载量双料冠军，它完美诠释了“多模态模型解决实际生产力问题”的定义。对于任何涉及文档处理、信息提取的开发者而言，这几乎是一个必试模型。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*