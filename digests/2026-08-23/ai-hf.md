# Hugging Face 热门模型日报 2026-08-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-23 00:32 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-23

## 📌 今日速览

本周 Hugging Face 榜首被 **Qwen3.8-27B 生态链**强势霸屏——基础模型以 12.1k 周点赞登顶，衍生量化版（GGUF、FP8、MLX）及各类 abliterated "无审查"微调版合计包揽 Top 30 中 15 席，下载量累计超 1000 万次，社区对其多模态能力的**本地化部署**与**越狱微调**热情空前。多模态生成赛道同样亮眼：**MiniMax-H3** 以 4.3k 点赞成为最强视频生成候选，与 **MiniMax-Music3** 一道押注多模态内容生产；**LTX-2.5** 作为轻量级视频方案持续走强。此外，**DeepSeek-V4-Flash-0731**（3.6k 赞、298万下载）和 **Kimi-K3**（10.9k 赞、261万下载）双双入榜，映射中国 AI 大模型军团的开源竞争正白热化。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 👤 | ❤️ 点赞 | ⬇️ 下载 | 一句话说明 |
|------|---------|--------|--------|-------------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,134 | 2,090,699 | 本周绝对王者——最新旗舰级**多模态对话模型**，综合能力强、生态完善，成为社区微调与量化的核心底座。 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,926 | 2,612,739 | 月之暗面新一代**压缩感知大模型**，主打高效推理与多模态能力，以超高点赞紧随 Qwen 之后，吸粉无数。 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,630 | 2,976,281 | DeepSeek V4 闪电版——速度与智能的平衡之作，下载量近 300 万，是本轮开源 LLM 竞技中的**头部玩家**。 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 718 | 54,566 | V4 系列 Pro 版——主打更高推理上限与长上下文稳定性，适合复杂任务与智能体场景。 |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,146 | 17,386 | 超大 MoE 旗舰（2.4T 总参/95B 激活），主打**文本生成极限能力**，面向企业级与前沿研究。 |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 320 | 12,611 | 基于 Qwen3.5 MoE 架构蒸馏的**高效 35B 模型**，激活参数仅 3B，兼顾多模态与文本生成。 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 202 | 1,913 | 极小型语音/文本生成模型，社区探索**端侧语音理解**的实验性作品。 |
| [empero-ai/Qwen3.8-9B-Distill](https://huggingface.co/empero-ai/Qwen3.8-9B-Distill) | empero-ai | 164 | 9,260 | Qwen3.8 的 9B 蒸馏版，在保留多模态能力的前提下极大降低部署门槛。 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,755 | 517,564 | Meta 最新 **30B 多模态旗舰**，兼具对话与视觉理解，以官方背书获得大量关注。 |

### 🎨 多模态与生成（图像/视频/音频/文本到X）

| 模型 | 作者 👤 | ❤️ 点赞 | ⬇️ 下载 | 一句话说明 |
|------|---------|--------|--------|-------------|
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,337 | 3,899,160 | 超强视频生成模型，支持**文本/图像/视频相互转换**，下载量近 400 万，登顶视频生成赛道。 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,181 | 16,644 | 第三代**音乐生成模型**，擅长从文本生成高质量乐曲，为创意内容生产注入新可能。 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,564 | 694,670 | 全能型图像/视频生成工具，支持 text-to-video、image-to-video 等全链路，轻量且高效。 |
| [TenStrip/10Eros-Max](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 316 | 0 | 基于 MiniMax-H3 的社区微调视频生成模型，刚发布即登榜，关注度极高。 |
| [LBH-123-AI/Minimax_h3_latent_Upscaler](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) | LBH-123-AI | 159 | 0 | MiniMax-H3 配套**潜空间放大模块**，提升生成视频分辨率，为生态补完工具链。 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

> 本榜单暂无显著的专用模型上榜，热门焦点集中在通用 LLM 底座及其衍生生态。

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 👤 | ❤️ 点赞 | ⬇️ 下载 | 一句话说明 |
|------|---------|--------|--------|-------------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,623 | 6,320,542 | **GGUF 量化王者**，横扫各类本地推理框架，下载量远超原版。 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 664 | 2,306,777 | 官方 FP8 量化版——在几乎无损的情况下大幅降低显存占用，是企业部署首选。 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 988 | 142,846 | FP8 精度的 **abliterated** 无审查微调版，社区讨论度极高。 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 885 | 34,909 | Apple 生态专属 MLX 格式的无审查版，满足 Mac 用户本地运行需求。 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 623 | 1,223,422 | GGUF 量化 + 无审查微调，兼顾轻量与自由度，下载量破百万。 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 336 | 85,371 | 该系列另一 GGUF 量化版本，与 FP8/MLX 版配合覆盖全部推理场景。 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 531 | 164,950 | 社区知名的 "禁忌" 微调版，一次性提供 MLX、GGUF 等**全格式支持**。 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 485 | 486,221 | GGUF 量化并激进微调，加入 MTP 特性提升速度，兼顾自由度与性能。 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 226 | 505,813 | "异端"级无审查 GGUF，社区下载超 50 万，热度飙升。 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 254 | 635,416 | 老牌量化团队 huihui-ai 推出的 GGUF 无审查版，质量稳定、口碑好。 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 246 | 21,612 | 同一团队的未量化 safetensors 原版，适合自行二次处理。 |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 232 | 173,935 | 高效率 MoE 模型的 GGUF 版，MIT 协议可商用，下载活跃。 |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 244 | 97,247 | llama.cpp 生态 GGUF 量化版，主打大上下文与稳定推理。 |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 189 | 176,969 | 堆料型社区微调——融合 GAIN/COLD-FUSION 等多种先进训练法，并做 GGUF 量化，追求极致性能。 |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 193 | 29,705 | 引入 **DFlash2 投机解码** 的优化版本，显著提升推理速度。 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,397 | 0 | 无权重，仅提供**修复版聊天模板**（jinja），解决社区广泛吐槽的模板兼容问题。 |

---

## 📊 生态信号

**Qwen 生态一骑绝尘**：除官方旗舰外，超过 20 个衍生量化/微调版占据榜单，形成"基础模型+社区衍生"的完整生态链，充分验证了 **"好底座带飞全社区"** 的模式。**无审查（abliterated）微调**成为最大热点，超过 8 款相关模型登上热榜。开源权重模型在本周榜单中占据绝对优势，**DeepSeek、Qwen、Kimi 等国产模型**的全面开源也对闭源商业模式形成压力。量化活动集中在 **GGUF（llama.cpp 生态）、FP8、MLX（Apple）** 三路并进，尤其是面向本地化和端侧部署的优化成为主流。与此同时，Community 对最大上下文与推理速度的追求催生了大量 **MTP/投机解码/蒸馏** 等衍生优化，生态的精细化运营已经相当成熟。

---

## 🧪 值得探索

1. **[Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 代表 Qwen 冲击极限的 MoE 文本大模型，激活参数仅 95B 却拥有 2.4T 总参量。作为新一代超大模型的代表，值得深度评测其长文本理解与复杂推理的边界。

2. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 视频生成的下一个爆款候选。其极强的多模态转换能力与近 400 万下载量，搭配 LBH-123 的 upscaler 等社区工具，值得关注其生成质量与可控性的实际表现。

3. **[unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — 作为量化社区最受欢迎的标准件，其 630 万下载量的作品代表了社区量化技术的最高水平。研究其 GGUF 量化后的性能/精度平衡，可为本地部署方案提供最佳实践参考。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*