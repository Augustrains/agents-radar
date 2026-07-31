# Hugging Face 热门模型日报 2026-07-31

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-31 01:26 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-07-31

## 📌 今日速览

今天是多模态模型全面爆发的一天：**月之暗面 Kimi-K3** 以 9,009 周点赞断层登顶，成为绝对的流量焦点；**GLM-5.2** 和 **Qwen3.6-35B-A3B** 分别以 4,681 和 2,595 点赞紧随其后，国产模型在趋势榜上占据主导地位。开源权重生态方面，**GGUF 微调社区**异常活跃，涌现出大量基于 Qwen3.6 和 Qwen3.5 的无审查微调模型。微软当日发布三款模型（Fara1.5-27B、Mage-VL、VibeVoice-ASR-BitNet），覆盖智能体、多模态与语音识别，值得关注。同时，2-bit 三元量化模型的流行标志着边缘部署技术进入新阶段。


## 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞/下载 | 说明 |
|------|------|-----------|------|
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,681 / 1,527,760 | 智谱新一代 MoE 对话模型，采用 DSA 稀疏架构，以超高下载量稳居社区头部。 |
| [Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 702 / 12,411 | Upstage 250B 级开源大模型，延续 Solar 系列高效训练路线。 |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 582 / 24,542 | 3B 轻量级 LLM，专注高效推理场景。 |
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 351 / 9,225 | 基于 Qwen3.5-MoE 的代码模型开发版。 |
| [antares-1b](https://huggingface.co/fdtn-ai/antares-1b) | fdtn-ai | 240 / 9,820 | 基于 Granite-MoE-Hybrid 架构的 1B 安全领域模型。 |
| [Instella-MoE-16B-A3B-Think](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) | amd | 94 / 1,315 | AMD 发布的 DeepSeek-V3 架构 MoE 推理模型。 |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 847 / 73,246 | Poolside 代码生成 LLM 2.1 版本，开发者社区热度持续高涨。 |
| [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 2,595 / 6,119,519 | Qwen3.6 旗舰 MoE——本周下载之王，多模态能力全面，是该系列生态的核心基座。 |


## 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞/下载 | 说明 |
|------|------|-----------|------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,009 / 387,822 | 本周趋势冠军。月之暗面发布的下一代多模态模型，采用压缩张量技术提升推理效率。 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,583 / 2,598,659 | 百度开放的全场景 OCR 模型，以 260 万+ 下载量成为当前最热门的视觉文档理解工具。 |
| [Inkling](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,655 / 45,658 | 高热度多模态对话模型，另有 Small 变体（114 赞）满足轻量需求。 |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 121 / 2,951 | 微软多模态视觉语言模型，定位通用视觉理解。 |
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 222 / 2,316 | 微软基于 Qwen3.5 的计算机使用（computer-use）智能体模型。 |
| [OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2) | ATH-MaaS | 351 / 57,439 | 基于 Qwen3.5 的 OCR 专用模型，与百度 Unlimited-OCR 同日竞技。 |
| [Mage-Flow](https://huggingface.co/Comfy-Org/Mage-Flow) | Comfy-Org | 97 / 44,714 | ComfyUI 生态的扩散模型单文件包，融合 Microsoft Mage-Flow 基底。 |

### 🎵 语音模型

| 模型 | 作者 | 点赞/下载 | 说明 |
|------|------|-----------|------|
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 321 / 1,100 | 轻量 CPU 本地 TTS 模型，主打边缘部署。 |
| [Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 119 / 654 | Micro-v2 的超小型版本，极致轻量。 |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 126 / 225 | 基于 ArkTTS 的 0.6B 预览版 TTS。 |
| [VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 120 / 3,864 | 微软 BitNet 架构的语音识别模型，GGUF/GGML 格式，为本地 ASR 开辟新路径。 |


## 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞/下载 | 说明 |
|------|------|-----------|------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 351 / 9,225 | 专用代码生成 MoE 模型，Qwen3.5-MoE 架构。 |
| [antares-1b](https://huggingface.co/fdtn-ai/antares-1b) | fdtn-ai | 240 / 9,820 | 面向安全领域的轻量 LLM。 |


## 📦 微调与量化（社区微调、GGUF、AWQ、NVFP4）

| 模型 | 作者 | 点赞/下载 | 说明 |
|------|------|-----------|------|
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,190 / 1,803,090 | 本周社区微调之王，Qwen3.6 无审查激进风格版本，180 万+下载。 |
| [Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,115 / 697,666 | 27B 模型压缩至 2-bit 三元量化 GGUF，极高性价比的本地部署方案。 |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,034 / 955,767 | DavidAU 社区微调系列，Unsloth 优化 + MTP 多 token 预测支持。 |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 241 / 162,394 | Hermes-V6 风格微调的 Qwen3.6 MoE GGUF 版本。 |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 158 / 248,173 | DavidAU 又一力作，NEO Imatrix 量化 + MTP 支持。 |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 147 / 7,755 | Solar-Open2-250B 的 NVFP4 量化版，专为 vLLM 优化。 |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 209 / 12,178 | Unsloth 官方 Kimi-K3 GGUF 量化解锁本地部署。 |
| [Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF) | unsloth | 259 / 159,331 | Unsloth 量化的 Laguna-S-2.1 GGUF 版本。 |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 94 / 201 | Escha 实验室的 W2 量化版 Qwen3.6 MoE 模型。 |
| [Kimi-K3](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 176 / 766 | Unsloth 版本的 Kimi-K3 safetensors 镜像。 |


## 📊 生态信号

**模型家族势力版图**：Qwen 生态已形成压倒性优势——Qwen3.6 不仅占据原始模型下载榜首（610 万+），还滋生了庞大的 GGUF 微调家族（HauhauCS、DavidAU、LuffyTheFox 等），是当前社区最活跃的模型系。GLM 凭借 5.2 的 150 万+下载成为第二大势力，Kimi-K3 则以爆发式关注度迅速崛起为第三极，多模态领域形成 **Qwen / Kimi / GLM 三强争霸** 的格局。

**开源 vs 闭源**：本周榜单全部为开源权重模型，标志着开源与闭源的能力差距持续缩小。尤其值得注意的是，微软（Fara1.5、Mage-VL）、AMD（Instella）等传统闭源巨头也在积极拥抱开源。

**量化与微调趋势**：GGUF 衍生模型占比近 1/3，生态已从"官方发布→社区量化"的链条进化为"官方发布→社区微调+量化→再传播"的活跃循环。无审查微调（Uncensored）成为社区最热门的方向。2-bit 三元量化（Ternary-Bonsai-27B）和 NVFP4 等低比特方案的成熟，正在将 27B+ 模型推进到消费级硬件。芯片厂商加速入局（AMD、微软），**边缘部署正在成为模型生态的第二增长曲线**。


## 🔬 值得探索

1. **Kimi-K3**：本周热度断层第一（9,009 点赞），采用压缩张量（compressed-tensors）技术，代表了新一代多模态架构的方向。同时已获 Unsloth GGUF 支持，建议立即上手体验。→ [链接](https://huggingface.co/moonshotai/Kimi-K3)

2. **Ternary-Bonsai-27B-gguf**：将 27B 参数压缩至 2-bit 三元量化，70 万+下载量证明了市场对"大模型极致压缩"的强烈需求。对于边缘部署和消费级硬件推理极具研究价值，值得深入测试。→ [链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)

3. **GLM-5.2**：智谱在 MoE-DSA 架构上的最新探索，150 万+下载验证了其实用性。作为少数摆脱 Qwen 技术路线的国产大模型代表，其架构创新值得长期关注。→ [链接](https://huggingface.co/zai-org/GLM-5.2)

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*