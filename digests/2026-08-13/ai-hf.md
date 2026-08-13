# Hugging Face 热门模型日报 2026-08-13

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-13 00:54 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-13

---

## 📌 今日速览

今日 Hugging Face 趋势榜被 **视频生成** 与 **多模态模型** 强势霸榜，MiniMax-H3 生态全面爆发，衍生出Turbo版、ComfyUI适配版、LoRA微调版等十余个衍生模型，成为当之无愧的流量中心。语言模型方面，**Moonshot AI 的 Kimi-K3** 以 10,583 赞断层登顶，压缩感知架构引发社区热议；**DeepSeek-V4-Flash-0731** 凭借百万级下载量证明推理模型的持久热度。值得关注的是，视频生成赛道正从单一模型竞争转向**生态工具链竞争**（LoRA、ComfyUI节点、Prompt重写器），而 AI 安全治理出现新形态——模型页面开始直接展示政府许可编号，预示监管框架正实质性落地。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,583 | 1,565,484 | 压缩张量架构的多模态模型，以特征提取能力与超低推理成本登顶今日热度王 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,238 | 1,048,685 | DeepSeek第四代Flash版本，百万级下载印证推理模型商业化领跑地位 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 582 | 93,668 | 2.6B小参数液态神经网络，工程效率与性能平衡的轻量级新选择 |
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 498 | 978 | 2.4T参数MoE架构旗舰，激活参数仅95B，Qwen大模型家族新里程碑 |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 346 | 2,049 | 预览版MoE模型，引发对新一代稀疏激活架构的讨论 |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 318 | 6,148 | 百灵混合架构的Flash版本，侧重推理速度与对话能力 |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 204 | 19,250 | 30B总参/3B激活的Lightning版本，NVFP4量化专为Blackwell优化 |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 116 | 15,740 | BF16全精度版本，为无NVFP4硬件环境提供高性能备选 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,716 | 83,484 | 旗舰级图生视频/文生视频模型，今日生态核心，衍生版本覆盖工具链全环节 |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,294 | 0 | Meta最新图像文本多模态对话模型，暂无下载数据但热度居高不下 |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 701 | 0 | 社区开发的MiniMax-H3 Turbo版LoRA，优化推理速度 |
| [**LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 567 | 39 | 全能视频转换模型，支持图生视频/文生视频/视频转视频 |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 411 | 20,376 | Turbo加速版，支持T2V/I2V/R2V，下载量健康增长 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 352 | 653 | 英伟达语音对话模型，聚焦实时语音交互场景 |
| [**PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 287 | 0 | 社区微调版MiniMax-H3，主打风格化视频生成 |
| [**BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 182 | 708 | Qwen3.5-MoE多模态版本，探索视觉-文本融合新方向 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,955 | 2,521,093 | 现象级社区微调+量化模型，250万下载证明"无审查+多模融合"路线的市场号召力 |
| [**MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) (Comfy-Org) | Comfy-Org | 1,258 | 6,798,796 | ComfyUI官方集成版，680万次下载，视频生成工作流的基础设施 |
| [**MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 301 | 0 | ComfyUI专属剪枝版Turbo LoRA，针对本地部署优化 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 666 | 207,990 | unsloth出品的GGUF量化版，20万下载验证DeepSeek生态号召力 |
| [**Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 358 | 0 | Meta Muse的GGUF量化版本，面向本地部署 |
| [**Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 114 | 3,851 | FP8量化版2.4T参数MoE，降低硬件门槛 |
| [**Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 189 | 0 | 超微型百灵模型，主打边缘端部署 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

*今日榜单暂无独立专用模型上榜，相关需求由多模态/量化模型兼顾覆盖。*

---

## 📊 生态信号

**核心观察：** MiniMax-H3 已构建起完整的"模型+工具链+生态"飞轮，从原生模型到 ComfyUI 集成、Turbo 加速、LoRA 微调、Prompt 重写器，衍生模型数十个、总下载量破千万，成为视频生成的事实标准生态。语言模型端，**Kimi-K3** 以"压缩张量"路线引爆社区，其超低推理成本或引领中小模型新范式；NVIDIA Nemotron 系列双版本（NVFP4/BF16）发布，表明硬件厂商正从芯片端向模型端挤压。值得警惕的是，**"无审查"模型**（如 DAU 系列）下载量突破 250 万，与 MiniMax-H3 衍生生态中出现成人内容微调模型的现象叠加，正迫使 Hugging Face 加速平台治理，生态中浮现出技术繁荣与合规压力的双向拉扯。

---

## 🧪 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 10,583 赞断层登顶，压缩张量架构是本月最大技术变量，其"每token成本降低90%"的性能数据值得深挖。

2. **[MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI)** — 单日 301 赞零下载，全新发布潜力未释放，ComfyUI 剪枝版 LoRA 是观察 MiniMax 生态工具链完整度的最佳样本。

3. **[NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4)** — NVFP4 量化路线是 Blackwell 架构上的新尝试，值得关注其性能与精度的平衡数据。



---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*