# Hugging Face 热门模型日报 2026-08-14

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-14 00:54 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-14

## 📌 今日速览

本周 Hugging Face 生态迎来 **多模态视频生成** 与 **VLM（视觉语言模型）** 的双核爆发：MiniMax-H3 系列（含 Turbo、LoRA 微调、ComfyUI 整合版）以绝对热度屠榜，官方版与社区衍生版合计点赞超 7000、下载超 1200 万；**Kimi-K3** 以 10,621 点赞登顶周榜，成为最受关注的压缩视觉语言模型；**DeepSeek-V4-Flash** 与 **Qwen3.8-2.4T-A95B** 延续了头部大厂在 MoE 架构上的军备竞赛。此外，**Muse-Glimmer-30B** 的多格式（原版/GGUF）策略、**DavidAU 的社区微调** 等显示出生态对“落地可用性”的强烈偏好。视频生成正从“技术尝鲜”转向“工程整合”阶段。

## 🔥 热门模型榜

### 🧠 语言模型（LLM / 对话 / MoE）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|-------------|-----------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,621 / 187万 | 登顶周榜的压缩视觉语言模型，主打高信息密度与低成本推理，是本月最强 VLM 黑马。 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,319 / 143万 | DeepSeek V4 的 Flash 轻量版，兼顾速度与性能，社区部署量极高。 |
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 783 / 1,012 | 2.4T 总参数、95B 激活的巨型 MoE，Qwen 新一代旗舰级开源权重（含 FP8 量化版）。 |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 602 / 11.7万 | 液态神经网络（LFM）2.5 代 2.6B 小模型，用极小参数量实现高效推理。 |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4)（[BF16版](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16)） | nvidia | 229+130 / 6.7万 | 30B 总参、3B 激活的高效 MoE，NVFP4 量化版是 NVIDIA 对边缘部署的最新回应。 |
| [**deepgrove/maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 353 / 3,868 | “枫树”预览版因果 MoE 模型，标签齐全，值得关注的新玩家。 |
| [**inclusionAI/Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 323 / 1万 | 国产“百灵”混合架构 3.0 的闪速版，适合高并发文本生成。 |

---

### 🎨 多模态与生成（视频 / 图像 / 音频）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|-------------|-----------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3)（官方） | MiniMaxAI | 3,822 / 160万 | MiniMax 第三代视频生成旗舰，支持图生视频与文生视频，是目前视频模型的事实标准之一。 |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,289 / **1036万** | ComfyUI 官方整合版，超千万下载量证明视频工作流已成为 ComfyUI 用户核心场景。 |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B)（[GGUF版](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF)） | meta-models | 1,417+257 / 25.8万 | Meta 的 30B 视觉语言对话模型，“Glimmer”系列主打轻量级多模态交互。 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 718 / 5.7万 | 全能视频模型，支持图/文/视频互相转换（i2v、t2v、v2v），单文件发布易于部署。 |
| [**MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 304 / 25 | MiniMax 进军音乐生成，文本到音频领域的新尝试（下载量尚少，潜力待观察）。 |
| [**MiniMax-H3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 461 / 9.1万 | H3 的高效 Turbo 版，主打速度，支持图像/文本/音频生成视频。 |
| [**unsloth/MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 149 / 11.1万 | MiniMax-H3 的 GGUF 量化版，配合 stable-diffusion.cpp 可本地跑视频生成。 |
| [**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 371 / 1,164 | 11B 语音对话模型，融合多篇论文成果，NVIDIA 补齐语音交互版图。 |

---

### 🔧 专用模型（代码 / 数学 / 医疗等）

*（本周榜单未收录显著增长的纯代码/医疗类专用模型；以下为值得关注的细分方向模型。）*

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|-------------|-----------|
| [**inclusionAI/Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 216 / 1,292 | Ling-3.0 的 Tiny 极简版，MIT 协议+混合架构，适合嵌入式场景。 |
| [**endless-frontier/BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 188 / 3,184 | 基于 Qwen3.5-MoE 的多模态大模型，社区玩家对 MoE+VLM 的新尝试。 |

---

### 📦 微调与量化（社区微调 / GGUF / LoRA）

| 模型 | 作者 | 点赞 / 下载 | 一句话说明 |
|------|------|-------------|-----------|
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 726 / 0 | 社区为 H3-Turbo 打造的 LoRA，0 下载却高赞——典型的“先收藏后使用”型模型。 |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 390 / 35.2万 | unsloth 出品的 Glimmer GGUF，让 30B VLM 在消费级硬件上跑起来。 |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711…**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,987 / 279万 | 社区微调狂魔 DavidAU 的最新作，融合大量风格模型的“缝合怪”，下载量惊人。 |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 297 / 324 | H3 的社区风格化微调，Apache-2.0 协议，技术合规的尝试。 |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 314 / 0 | H3-Turbo LoRA 的 ComfyUI 适配版，工程化微调的典范。 |
| [**fal/MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 159 / 4,692 | fal 官方出品的“写实人物”LoRA，专注于人物视频生成质量。 |
| [**lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA**](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA) | lightx2v | 149 / 652 | 专门重写提示词的 LoRA，提升视频生成可控性。 |
| [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3…**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 483 / 0 | Qwen3-VL 的极致社区魔改版，INT8 量化 + ComfyUI 兼容。 |

---

## 🌐 生态信号

1. **MiniMax-H3 生态闭环成型**：从官方权重、Turbo 变体、LoRA 微调、GGUF 量化到 ComfyUI 整合，MiniMax 已形成“模型-工具链-工作流”的完整链条（相关模型合计下载超 1200 万），视频生成正在复刻 Stable Diffusion 的生态发展路径。

2. **MoE 成为头部厂商共识**：Qwen3.8（2.4T 总参）、DeepSeek-V4、NVIDIA Nemotron 3.5（30B-A3B）均采用 MoE 架构，“超大总参数量 + 稀疏激活”成为开源大模型的主流技术路线。

3. **量化与微调极度活跃**：unsloth、DavidAU 等社区玩家持续高产，GGUF/NVFP4/FP8 量化已覆盖到 30B 级模型与 10B 级视频模型；DavidAU 的“缝合怪”微调下载量达 279 万，说明用户对个性化/风格化模型的刚需极强。

4. **开源权重全面开花**：本周 30 个热门模型中，仅极少数为闭源 API 模型，“开源权重 + 社区二次开发”已成为绝对主流范式。

---

## 🔭 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 周榜点赞第一（10,621），用“压缩视觉语言”路径重新定义 VLM 的效率与信息密度，是当前多模态领域最具研究价值的模型。

2. **[Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)（及 [FP8版](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8)）** — Qwen 史上最大开源 MoE，2.4 万亿参数展示了国产大模型的极限野心，值得关注其实际推理效果与显存需求。

3. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 超 1000 万下载量说明视频生成已全面进入“工作流化”时代，想体验最成熟的视频生成工程化集成，这是不二之选。

---

*日报基于 Hugging Face 2026-08-14 热门模型榜（按周点赞排序）生成，数据来源于公开社区统计。*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*