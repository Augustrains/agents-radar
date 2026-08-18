# Hugging Face 热门模型日报 2026-08-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-18 00:29 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-18

## 📌 今日速览

今日榜单由 Qwen3.8 系列与 MiniMax-H3 系列双雄领跑。Qwen3.8-27B 凭借 10.7K 周点赞登顶通用多模态榜首，而 moonshotai 的 Kimi-K3 以 10.8K 点赞紧随其后，成为当日最大黑马。视频生成赛道，MiniMax-H3 官方版与 Comfy-Org 社区版合计下载量超 1600 万次，生态爆发力惊人。DeepSeek-V4 系列双模型（Pro/Flash）同时上榜，MoE 架构成为中大体量模型的主流选择。值得注意，量化与微调生态持续繁荣，GGUF/FP8/NVFP4 多精度版本密集发布，社区二次创作活跃度显著提升。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍点赞 | 📥下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,041 | 9,465 | Qwen 旗舰 MoE 模型，2.4T 总参数、95B 激活参数，主打极致推理性能与多语言能力 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 573 | 25,006 | DeepSeek 第四代 Pro 版本，在代码与数学推理上对标闭源头部模型 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,497 | 1,978,298 | V4 轻量快速版，高性价比推理，下载量逼近 200 万次 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 307 | 231,271 | NVIDIA 30B（3B 激活）MoE 模型，NVFP4 量化版，单卡可部署 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 169 | 69,833 | 同模型 BF16 全精度版，适合对精度敏感的生产场景 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **10,802** | 2,163,953 | Kimi 第三代多模态模型，采用压缩张量技术，今日点赞榜第一 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 653 | 147,270 | Liquid AI 2.6B 高效小模型，主打低延迟边缘部署 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍点赞 | 📥下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 10,711 | 415,039 | 新一代旗舰多模态模型，支持图像+文本输入，推理与对话能力全面升级 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 529 | 495,646 | 官方 FP8 量化版，精度损失极小，部署成本大幅降低 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,661 | 334,099 | Meta 系 30B 多模态模型，视觉理解与生成能力均衡 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,108 | 465,529 | 全能视频生成模型，支持图生视频、文生视频、视频编辑多任务 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,087 | 2,403,238 | 国产视频生成头部模型，支持文生视频与图生视频，画质细腻 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 904 | 10,375 | 专业级音乐生成模型，支持文本直接生成完整乐曲 |
| [Gazingstars123/Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 233 | 23,202 | 动漫风格文生图模型，社区好评度高 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 584 | 264,351 | MiniMax-H3 的加速版，推理速度大幅提升 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,403 | **14,015,769** | ComfyUI 官方适配版，下载量突破 1400 万，视频生成的事实标准 |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 786 | 0 | H3-Turbo 的 LoRA 扩展，支持音视频联合生成 |
| [fal/MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 243 | 18,562 | 写实人物视频生成 LoRA，提升 H3 人物真实感 |
| [LiquidAI/LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 162 | 6,816 | 3B 视觉语言小模型，可在边缘设备运行 |

### 🔧 专用模型（代码、数学、医疗、嵌入等）

| 模型 | 作者 | 👍点赞 | 📥下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [inclusionAI/Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 306 | 6,266 | 国产 Bailing 混合架构小模型，MIT 协议，面向 US 区域优化 |
| [dots-studio/dots3-note-prev](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 207 | 633 | 笔记/文档理解专用模型，亮点在于上下文压缩与检索增强 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍点赞 | 📥下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,628 | 2,727,609 | 最受欢迎的 Qwen3.8 GGUF 量化包，覆盖 2bit-8bit 全系列 |
| [Qwen/Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 220 | 12,295 | 官方 FP8 版超大规模 MoE，显存占用减半 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 436 | 15,812 | 去审查 FP8 版，Abliteration 技术处理，社区反响热烈 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 299 | 357,701 | 去审查 GGUF 版，支持 MTP 加速采样 |
| [unsloth/Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 470 | 755,125 | Muse-Glimmer-30B 的 GGUF 量化，大幅降低部署门槛 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 240 | 378,177 | NVIDIA NVFP4 量化格式版，针对 RTX 40/50 系优化 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,119 | 3,033,928 | 社区魔改集大成者，融合多风格微调，下载超 300 万 |
| [Comfy-Org/MiniMax-Music-3](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 167 | 256,988 | 音乐生成模型 ComfyUI 适配版 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,211 | 0 | 修复 Qwen 聊天模板的工具包，开发者刚需，零下载引发好奇 |

---

## 🌐 生态信号

**1. 家族化竞争格局确立。** Qwen3.8 系列形成"旗舰-量化-微调"完整生态链（官方+unsloth+社区），MiniMax-H3 则以"官方模型+ComfyUI 适配+LoRA 扩展"构建视频生成护城河。DeepSeek-V4 双版本策略（Pro/Flash）覆盖性能与效率两端。

**2. 开源权重全面领跑。** 榜单前 10 全部为开源权重模型。Kimi-K3 与 Qwen3.8-27B 的周点赞均破万，预示开源多模态模型已进入能力爆发期。DeepSeek、Qwen、MiniMax 三大国产阵营持续主导 HF 热度。

**3. 量化与微调深度绑定。** GGUF 仍是下载量王者（unsloth Qwen3.8-GGUF 达 272 万次），但 NVFP4、FP8 等新格式增长强劲。社区"去审查"微调（Uncensored）与风格融合（DavidAU 系列）成为高频需求，反映用户对个性化和自由度的高度追求。

---

## 🧪 值得探索

**1. [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 今日点赞第一，压缩张量技术值得深入评测。在多模态理解与推理上的突破，使其成为 Qwen3.8 最有力的竞争者。

**2. [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 2.4T 参数的超大 MoE 模型，仅 95B 激活。代表了开源模型在参数规模上的最新边界，适合研究稀疏激活与推理效率的平衡。

**3. [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5)** — 视频生成多任务全能选手，但与 MiniMax-H3 的竞争值得观察。Lightricks 在视频编辑领域的传统优势可能带来差异化体验。

---

> 📊 数据说明：下载量累计统计，点赞为近 7 日增量。日报基于公开数据整理，不构成投资或技术选型建议。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*