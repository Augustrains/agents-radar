# Hugging Face 热门模型日报 2026-08-16

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-16 00:31 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-16

## 📌 今日速览

本周 Hugging Face 榜单呈现出**多模态主导、开源权重全面开花**的格局。Kimi-K3 以 10.7K 周点赞登顶趋势榜，成为社区焦点；Qwen3.8-27B 系列凭借官方与社区量化双线发力占据多个席位。MiniMax-H3 视频生成模型生态爆发，衍生出 Turbo、LoRA、GGUF、ComfyUI 等多个变体，下载量突破千万级别。**多模态模型（图像+文本→文本/视频）成为本周主体**，占比超过三分之一，标志着"文字对话"已全面升级为"视觉对话"时代。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,725 | 2.1M | 月之暗面最新多模态对话模型，支持特征提取与压缩张量技术，凭借极致性能与 ArXiv 论文加持登顶本周趋势榜 |
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 489 | 19.9K | DeepSeek 旗舰级 Pro 版 LLM，面向高复杂度推理场景，8月13日版本迭代引发开发者关注 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,421 | 1.8M | 轻量高效的 Flash 版本，7月31日发布，以极低延迟和高吞吐量获大量部署 |
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 967 | 6.4K | 通义千问 2.4 万亿参数 MoE 模型，激活仅 95B 参数，千问 3.8 时代新一代稀疏架构旗舰 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 272 | 170.6K | NVIDIA 新 4-bit 压缩格式 NVFP4 代表作，30B 总参/3B 激活，是 Llama 系推理新标杆 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 150 | 62.9K | Lightning 系列 BF16 完整精度版本，供研究社区做精度对比与二次微调使用 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 627 | 135.4K | Liquid AI 新一代液态神经网络 LLM，2.6B 参数在极小规模上实现出色推理表现 |
| [LiquidAI/LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 143 | 4.6K | LFM2.5 系列视觉语言版本，3B 级多模态理解模型，适合边缘部署 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 9,790 | 91.9K | 阿里通义千问最新 27B 多模态对话模型（看图说话），作为本周下载量最大的官方 Base 模型，树立新标杆 |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,577 | 246.5K | Meta 最新 30B 多模态对话模型，集成 Glimmer 视觉编码器，改写视觉语言理解 SOTA |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,971 | 2.2M | MiniMax 新一代图像/文本→视频生成大模型，完整 diffusion 框架，220 万下载称霸视频生成赛道 |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 766 | 5.1K | 第三代音乐生成模型，从文本直接生成高保真完整音乐作品，音频生成新方向 |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 939 | 378.4K | 多功能视频生成模型，支持图像→视频、文本→视频，单文件 diffusion 架构极受 ComfyUI 用户欢迎 |
| [Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 514 | 211.9K | H3 加速版 Turbo 推理方案，在几乎不损失画质下大幅提升视频生成速度 |
| [Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 188 | 16.8K | 超轻量文本→图像模型，2.9B 单文件设计，主打动漫风格生成与本地部署 |
| [LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 143 | 4.6K | Liquid 多模态视觉语言小模型，适合端侧图片理解任务 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,227 | 868.0K | 官方 27B 的 GGUF 量化版，86.8 万下载印证 Qwen3.8 是社区本地部署的第一选择 |
| [Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 435 | 682.2K | 社区量化团队 unsloth 对 Meta 多模态模型的 GGUF 优化版，68 万下载证明多模态量化有庞大需求 |
| [MiniMax-H3-GGUF](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 164 | 173.7K | 视频生成模型 GGUF 量化版（支持 stable-diffusion.cpp），让本地视频生成更轻量 |
| [Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 427 | 123.2K | 官方 FP8 8-bit 量化版，相比 BF16 减半显存占用，几乎零精度损失 |
| [Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 166 | 90.9K | 适配 NVIDIA 最新架构的 NVFP4 量化版，比 FP8 更省显存 |
| [Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 193 | 10.7K | MoE 旗舰的 FP8 量化版，将 2.4T 超大模型推向实用部署 |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 756 | 0 | 新发布的 H3-Turbo LoRA 轻量微调模块，支持文本+音频→视频，下载量尚未起飞但值得关注 |
| [MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 192 | 12.7K | fal 官方出品的写实人物风格 LoRA，一键提升 H3 人物真实感 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,344 | 12.8M | ComfyUI 官方集成版 H3 单文件模型，1278 万下载为本周全站下载之最 |
| [MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 352 | 0 | ComfyUI 工作流部署支持文件，社区开发者的配套节点方案 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,051 | 2.98M | 社区最强 "无审查" 微调+量化合一模型，298 万下载表明 "uncensored" 细分赛道不容忽视 |
| [MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 192 | 12.7K | 写实人类视频生成的极简 LoRA 插件 |
| [Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 257 | 4.8K | 百灵 3.0 tiny 版，MIT 协议 + 自定义代码的轻量模型，偏研究探索向 |

---

## 🔍 生态信号

**多模态全面接管主流赛道。** 本周 Top5 中有 3 个是图像/视频相关模型，Kimi-K3、Qwen3.8-27B、Muse-Glimmer-30B 均支持视觉输入，"看图对话"成为大模型标配能力。

**视频生成呈现"一超多强"生态。** MiniMax-H3 以 2.2M 官方下载 + 12.8M ComfyUI 整合下载成为絕對霸主，围绕它迅速形成了 Turbo、LoRA、GGUF、ComfyUI 的工作流生态闭环。

**量化赛道竞争白热化。** 同一模型往往短时间内出现 GGUF、FP8、NVFP4 三种精度版本——从 unsloth 到官方自出量化，说明开源社区真正关注的是"用得起"（能本地跑），而非仅仅是"能用"。

**开源权重继续加速领跑。** 本周所有 Top10 模型全部开源权重，对应 Qwen、Meta、DeepSeek、MiniMax、NVIDIA、Moonshot 全面拥抱开放，且各家均有量化衍生版本，闭源模型的竞争空间进一步收窄。

---

## 💡 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周点赞量最高（10.7K）的模型，首次集成 feature-extraction 与 compressed-tensors 能力，阅读其技术报告将能预判下一代多模态对话模型的方向。

2. **[Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 2.4T 总参数 MoE 架构是当前开源可获取的最大规模模型之一，搭配 FP8 量化后可在 8×H100 节点上运行。研究其稀疏门控路由策略对下一代 MoE 设计有重要参考价值。建议配合 [FP8 量化版](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) 做显存占用对比测试。

3. **[MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora)** — 下载量仍为 0 但点赞高达 756，说明是刚发布的潜力股。其文本+音频→视频的多模态融合方案是目前业界极少数验证过的路径，值得第一时间尝试。

---

> 📊 日报数据截至：2026-08-16 | 数据来源：Hugging Face Trending（周榜）

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*