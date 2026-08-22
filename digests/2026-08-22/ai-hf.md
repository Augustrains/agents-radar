# Hugging Face 热门模型日报 2026-08-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-22 00:29 UTC

---

# 🤗 Hugging Face 热门模型日报 — 2026-08-22

## 📌 今日速览

今日榜单被 **Qwen 3.8 系列** 全面占领：原版 27B 多模态模型以 11.9K 周点赞登顶，围绕其衍生的 GGUF、abliterated 去审查、FP8/NVFP4 量化等生态版本占据了榜单近半席位，社区热度可见一斑。**MiniMax** 双雄发力，H3 视频模型下载量突破 361 万，Music3 同期发布并在音乐生成赛道引发关注。**DeepSeek V4** 系列表现亮眼，Pro 与 Flash 两个版本均进入榜单且下载量合计近 290 万。多模态与视频生成已成为绝对焦点，同时 llama.cpp/GGUF 量化格式及"非审查"（abliterated）微调持续火爆。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [**DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 708 | 49.6K | DeepSeek V4 旗舰版，对话能力与推理性能全面升级。 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,609 | 2.83M | V4 轻量高速版，以 280 万下载量成为最受欢迎的高效推理方案。 |
| [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,139 | 15.7K | 2.4T 参数 MoE 文本模型（激活 95B），Qwen 3.8 系列旗舰文本版本。 |
| [**ornith-ai/Ornith-1.5-35B-A3B**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 288 | 9.2K | 仅激活 3B 参数的 35B MoE 模型，主打极致推理效率与多模态能力。 |
| [**superwhisper/s1-mini**](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 190 | 1.1K | 小型语音转文本/文本生成模型，适合端侧部署场景。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | **11,961** | 1.73M | **今日榜首**，Qwen 3.8 多模态旗舰，同时支持图像+文本输入与对话。 |
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,294 | 3.61M | MiniMax 第三代视频生成模型，文本/图像均可驱动，下载量全场第一。 |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,738 | 505K | Meta 系 30B 多模态模型，图像+文本理解能力强，社区热度持续上升。 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,489 | 654K | 轻量视频生成模型，支持图像/视频到视频的多模式转换。 |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,163 | 15.7K | 文本生成音乐的第三代模型，音乐创作细分赛道的领跑者。 |
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **10,913** | 2.45M | Kimi 新一代多模态模型，采用压缩张量技术，点赞量仅次于榜首。 |
| [**TenStrip/10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 311 | 0 | MiniMax-H3 的社区微调版本，针对视频生成风格进一步优化。 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

*今日榜单暂无典型专用模型上榜，该类目被通用/多模态模型全面覆盖。*

### 📦 微调与量化（社区微调、GGUF、AWQ）

以 Qwen3.8-27B 为核心衍生出的几乎所有量化与微调版本，以及未量化但经 abliterated 处理的完整版：

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|--------|-----------|
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,503 | 5.80M | 官方 GGUF 量化全系列，下载量 580 万全场最高，本地部署首选。 |
| [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 660 | 1.94M | 官方 FP8 量化版，精度损失小且大幅降低显存需求。 |
| [**unsloth/Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 328 | 1.01M | 面向 NVIDIA 最新硬件的 4-bit 量化格式，推理速度极佳。 |
| [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,370 | 0 | 修复 Qwen 系列 Jinja 对话模板的轻量包，开发者工具型项目。 |
| [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 566 | 1.13M | 去审查版 GGUF，百万级下载证明社区对"无审查"模型的高需求。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 818 | 107K | 去审查 + FP8 量化双buff，兼顾效果与部署效率。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 818 | 18K | 面向 Apple Silicon 的 MLX 去审查版，Mac 本地部署。 |
| [**OBLITERATUS/Qwen3.8-27B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 440 | 124K | 名字即风格——"抹除"审查，多格式支持（MLX/GGUF）。 |
| [**huihui-ai/Huihui-Qwen3.8-27B-abliterated**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 229 | 17.5K | 知名社区作者 huihui 的去审查微调版。 |
| [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 231 | 338K | 上述模型的 GGUF 量化版下载量更高，社区更偏向本地使用。 |
| [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 421 | 357K | 激进去审查 + 多 token 预测优化，社区口碑良好。 |
| [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 211 | 422K | "异端"级去审查版本，下载量显著说明需求侧旺盛。 |
| [**Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF**](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) | Blackfrost-AI | 201 | 198K | 27B Dense 架构全量去审查 GGUF 版。 |
| [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 237 | 74K | Qwen3.8 的 GGUF 量化变体，主打 llama.cpp 兼容。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 293 | 68K | 同作者 FP8/MLX 版的 GGUF 量化配套。 |
| [**z-lab/Qwen3.8-27B-DFlash2**](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 174 | 21K | 引入推测解码（speculative decoding）加速推理的优化版。 |
| [**DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 169 | 155K | 融合 GAIN、Cold-Fusion 等多种前沿训练技术的"缝合怪"量子版。 |
| [**ornith-ai/Ornith-1.5-35B-A3B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 205 | 123K | Ornith MoE 模型的 GGUF 量化版，激活参数少，本地推理友好。 |

---

## 🔍 生态信号

**Qwen 3.8 已成事实上的社区标准基座。** 30 个热门模型中近 20 个与 Qwen3.8-27B 直接相关，从官方多模态原版到 FP8/NVFP4/GGUF 量化、再到无审查微调和推测解码加速，形成了完整且高度活跃的衍生生态。Qwen 的开放性策略带来了极大的社区赋能效应。

**"去审查"（abliterated）成显学。** 超过 7 个 abliterated/uncensored 变体上榜，多款下载量破百万。这反映了两类需求：一是对模型安全边界之外的创作自由的追求，二是研究者在评估模型固有能力的诉求。

**开源权重全面领先，闭源以 API 形态参与竞争。** 榜单所有模型权重均为开箱即用，MiniMax、DeepSeek、Kimi 等头部厂商持续开源新作，进一步巩固了开源社区在创新速度上的优势。

**多模态与视频生成成为下一个主战场。** MiniMax-H3 下载量 360 万+、LTX-2.5、Muse-Glimmer 等视频/多模态模型表现强势，领域正在从文本对话范式切换至更丰富的媒体生成范式。

---

## 💡 值得探索

1. **[MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3)** — 文本转音乐仍处于早期蓝海，MiniMax 在这一垂直赛道的持续投入值得跟进，值得尝试生成完整歌曲片段研究其音乐结构理解能力。

2. **[Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B)** — 仅 3B 激活参数的 MoE 多模态模型，是研究高效 MoE 架构在端侧部署潜力的绝佳范本，与 Qwen3.8-2.4T-A95B 形成"上下限"的对照观察。

3. **[Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 当前为数不多的大规模 MoE 文本模型，作为生态"母体"级基座，关注其与 27B 小模型之间的能力差距与蒸馏可能性，对判断下一代开源模型能力曲线有重要参考意义。

---

*报告生成于 2026-08-22，数据基于 Hugging Face Hub 周点赞与下载统计。*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*