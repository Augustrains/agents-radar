# Hugging Face 热门模型日报 2026-08-19

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-19 00:30 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-19

---

## 📌 今日速览

今日 Hugging Face 榜单呈现出**多模态与量化齐飞**的态势：Qwen 家族以 Qwen3.8-27B 为核心持续霸榜，官方模型与社区量化版本合计席卷近 20,000 点赞；MiniMax 在视频生成（H3）与音乐生成（Music3）双线发力，配合 Comfy-Org 的生态集成，下载量突破千万级；DeepSeek-V4 系列稳步迭代，Flash 版本保持高热度；值得关注的是 Kimi-K3 以 10,826 点赞强势登榜，成为开源多模态赛道的有力竞争者。量化生态方面，GGUF/FP8/NVFP4 多格式覆盖已成标配，社区微调（尤其"Uncensored"变体）持续活跃。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,066 | 11,212 | Qwen 旗舰级 MoE 模型，2.4T 总参/95B 激活，文本生成新标杆 |
| [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 601 | 30,985 | DeepSeek-V4 专业版，主打高质量对话与推理 |
| [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,527 | 2,123,462 | V4 轻量快速版，凭借出色速度与性能稳居下载前列 |
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,826 | 2,226,898 | Kimi 新一代多模态模型，采用压缩张量技术，本月最大黑马 |
| [**Qwen/Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 225 | 13,344 | MoE 旗舰的 FP8 量化版，大幅降低部署门槛 |
| [**nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 322 | 269,372 | NVIDIA 轻量级 30B 模型（3B 激活），NVFP4 量化，主打高效推理 |
| [**inclusionAI/Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 319 | 9,990 | Ling 3.0 微型版本，混合架构实验性模型 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,127 | 665,513 | **今日榜首**，Qwen3.5 系列多模态旗舰，支持图文对话 |
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,143 | 2,855,539 | 视频生成王牌模型，支持文本/图像/视频到视频 |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,682 | 384,097 | Meta 多模态对话模型，30B 规模兼顾性能与效果 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,222 | 503,632 | 视频生成全能选手，支持 i2v/t2v/v2v 多任务 |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 958 | 11,745 | 文本生成音乐模型，MiniMax 音频领域新作 |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 608 | 300,279 | H3 加速版，优化推理速度的视频生成模型 |
| [**Gazingstars123/Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 248 | 24,893 | 动漫风格文生图模型，ComfyUI 单文件格式 |
| [**TenStrip/10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 264 | 0 | MiniMax-H3 的社区微调版，主打特定风格视频生成 |
| [**LiquidAI/LFM2.5-VL-3B**](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 173 | 9,101 | 液态 AI 多模态小模型，3B 轻量级视觉语言模型 |
| [**dots-studio/dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 220 | 1,120 | Dots3 系列预览版，多模态实验性模型 |

### 📦 微调与量化（社区微调、GGUF、FP8 等）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,817 | 3,561,466 | 官方模型的 GGUF 量化版，下载量惊人，本地部署首选 |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,425 | 14,641,908 | H3 的 ComfyUI 单文件集成版，**14M+ 下载**生态王者 |
| [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,255 | 0 | 修复 Qwen 聊天模板的工具库，开发者实用资源 |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,140 | 3,020,528 | "缝合怪"式社区微调，汇集多种增强技术于一身 |
| [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 562 | 741,011 | 官方 FP8 量化版，降低部署成本同时保持高精度 |
| [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 528 | 45,465 | "Uncensored" FP8 版，移除安全限制的社区变体 |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 481 | 787,276 | Meta Muse-Glimmer 的 GGUF 量化版 |
| [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 410 | 558,767 | Uncensored 版 GGUF 量化，支持 MTP 加速 |
| [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 200 | 27,745 | 激进风格微调 + GGUF 量化，主打"无限制"体验 |
| [**unsloth/Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 262 | 523,919 | NVIDIA 新格式 NVFP4 量化版，适配最新硬件 |
| [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 263 | 0 | Apple Silicon MLX 格式的 Uncensored 版 |
| [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 172 | 12,854 | Qwen3.8 的 Ridge 变体 GGUF 量化 |
| [**Comfy-Org/MiniMax-Music-3**](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 177 | 285,444 | Music3 的 ComfyUI 集成版，Apache-2.0 协议 |

---

## 🌐 生态信号

**模型家族格局**：Qwen 家族（Qwen3.8 系列）毫无疑问是本周绝对王者，官方 + 社区变体合计超过 20 个上榜条目，覆盖从 27B 密集到 2.4T MoE 的全谱系，且 GGUF/FP8/NVFP4/MLX 多格式并行发布已成标配。MiniMax 凭借 H3 视频模型 + Music3 音频模型 + ComfyUI 集成构建了完整创作生态。DeepSeek-V4 和 Kimi-K3 构成第二梯队，前者以多版本迭代策略取胜，后者凭新技术路径（压缩张量）引发关注。

**开源 vs 闭源**：开源权重模型依然占据绝对主导，且社区二次创作异常活跃——"Uncensored"微调蔚然成风，反映了部分用户对内容限制的诉求。值得注意的是 Meta（Muse-Glimmer）和 NVIDIA（Nemotron）都在积极开源，而 MiniMax、DeepSeek 等国内厂商也在加速开源布局。

**量化与部署趋势**：多格式量化已成发布标配，FP8 和 NVFP4 等新格式正快速普及，GGUF 依然是本地部署事实标准（Comfy-Org/MiniMax-H3 超 1400 万下载极具说服力）。社区微调呈现"缝合"趋势（如 DavidAU 的融合模型），多种技术叠加追求极致效果。

---

## 🔬 值得探索

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 压缩张量技术应用值得深入研究，可能代表多模态模型的新效率方向；10K+ 点赞也验证了其社区认可度。

2. **[Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 2.4T 总参数的超大规模 MoE 架构代表当前开源模型的天花板，值得关注其推理成本与性能的平衡策略。

3. **[MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3)** — 文本到音乐的垂直赛道新玩家，与 H3 视频模型形成内容生成闭环，音视频 AIGC 一体化趋势值得关注。

---

*报告生成时间：2026-08-19 | 数据来源：Hugging Face Trending*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*