# Hugging Face 热门模型日报 2026-08-20

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-20 00:30 UTC

---

# Hugging Face 热门模型日报（2026-08-20）


## 今日速览

本周 Hugging Face 趋势榜由 **Qwen3.8-27B** 系列全面主导，以 11,477 周点赞登顶，并在热门榜前十中占据八席，量化、去审查（abliterated）变体密度极高。值得关注的是，**MiniMax 视频生成家族异军突起**——MiniMax-H3 以 4,179 点赞、305 万下载领跑视频赛道，其音乐生成模型 MiniMax-Music3 亦同步上榜。DeepSeek 发布 V4 系列双模型（Pro/Flash），Kimi 也带来了带压缩张量的 **Kimi-K3**。生态上呈现**“Qwen 一枝独秀，多模态生成百花齐放”**的格局，社区围绕 Qwen3.8 的量化与去审查微调极为活跃。


## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) — deepseek-ai | 点赞 633 | 下载 37,583  
  DeepSeek V4 Pro 正式版，专注复杂推理与长文本生成，是当前 DeepSeek 家族最强旗舰。

- [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — deepseek-ai | 点赞 3,548 | 下载 2,330,940  
  V4 轻量高速版本，主打低延迟高吞吐，适合大规模服务部署，下载量已超 233 万。

- [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) — Qwen | 点赞 1,099 | 下载 12,699  
  Qwen3.8 系列的超大规模 MoE 模型（总参数 2.4T，激活 95B），目前该家族参数量最高的旗舰。

- [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — moonshotai | 点赞 10,853 | 下载 2,289,863  
  Kimi 第三代多模态大模型，采用压缩张量技术（compressed-tensors），显著降低推理成本，获近 1.1 万点赞，是本周最强黑马之一。

- [**dots-studio/dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) — dots-studio | 点赞 231 | 下载 1,239  
  Dots3 系列的“笔记版”预览模型，轻量化设计，面向端侧笔记场景，值得关注。


### 🎨 多模态与生成（图像、视频、音频、文本到X）

- [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) — Qwen | 点赞 11,477 | 下载 1,006,235  
  本周热度之王：Qwen3.8 主力多模态模型（视觉+语言），27B 稠密架构，集对话、视觉理解于一体。

- [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — MiniMaxAI | 点赞 4,179 | 下载 3,055,205  
  MiniMax 第三代视频生成模型，支持文生视频、图生视频，下载量超 305 万，是当前开源视频生成标杆。

- [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) — MiniMaxAI | 点赞 1,036 | 下载 13,138  
  MiniMax 最新音乐生成模型（text-to-audio），可生成完整歌曲，代表音频生成新高度。

- [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) — Lightricks | 点赞 1,320 | 下载 555,993  
  Lightricks 视频生成大模型，支持图生视频、文生视频，55 万下载量验证其实用性。

- [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) — meta-models | 点赞 1,702 | 下载 430,313  
  Meta 系 30B 多模态模型，集图像理解与对话于一体，具备设计感的美学调用能力。

- [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) — lightx2v | 点赞 625 | 下载 340,984  
  MiniMax-H3 的轻量加速版，面向实时生成场景，主打更快的视频推理速度。

- [**TenStrip/10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) — TenStrip | 点赞 283 | 下载 0  
  MiniMax-H3 的社区微调版，主打更灵活的视频风格控制，刚上架暂无下载量。

- [**Gazingstars123/Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) — Gazingstars123 | 点赞 269 | 下载 26,566  
  2.9B 轻量文生图模型，单文件分发，适配 ComfyUI，适合低资源部署。


### 🔧 专用模型（代码、数学、医疗、嵌入）

- [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) — froggeric | 点赞 1,288 | 下载 0  
  Qwen 系列聊天模板修复包（MLX/Jinja），解决模板兼容性问题的工具型项目，下载量为 0 但点赞破千，备受欢迎。


### 📦 微调与量化（社区微调、GGUF、AWQ）

- [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) — unsloth | 点赞 2,074 | 下载 4,318,134  
  Qwen3.8-27B 的官方 GGUF 量化版本，下载量超过 431 万，是目前社区部署主力格式。

- [**unsloth/Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) — unsloth | 点赞 285 | 下载 653,042  
  NVIDIA FP4 精度量化版，兼容 Hopper/Blackwell 架构，65 万下载验证需求。

- [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) — DavidAU | 点赞 2,165 | 下载 3,033,363  
  目前最受欢迎的 Qwen 社区微调版，融合多种创意风格与“去审查”能力，下载突破 303 万。

- [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) — Qwen | 点赞 600 | 下载 1,063,646  
  官方 FP8 量化版，精度与性能平衡，下载超百万次。

- [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) — orcarouter | 点赞 613 | 下载 60,078  
  Abliterated（去审查）+ FP8 量化组合的社区版。

- [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) — orcarouter | 点赞 595 | 下载 27  
  面向 Apple Silicon 的 MLX 格式去审查版本，专为 Mac 用户优化。

- [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) — JonathanColetti | 点赞 467 | 下载 766,812  
  去审查版 GGUF，支持 llama.cpp 与 MTP 推理，76 万下载。

- [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) — HauhauCS | 点赞 286 | 下载 131,113  
  激进风格去审查版，支持多模态视觉理解，GGUF 格式。

- [**orcarouter/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) — orcarouter | 点赞 186 | 下载 26,472  
  Qwen3.8 去审查标准 GGUF 版。

- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) — huihui-ai | 点赞 170 | 下载 94,234  
  Huihui 去审查 GGUF 变体。

- [**huihui-ai/Huihui-Qwen3.8-27B-abliterated**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) — huihui-ai | 点赞 165 | 下载 7,207  
  Huihui 去审查全精度版。

- [**Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF**](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) — Blackfrost-AI | 点赞 170 | 下载 164,263  
  多量化等级 GGUF，覆盖 QQ8 至 IQ1 全精度档位。

- [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) — 0bserverx | 点赞 160 | 下载 245,266  
  “Heretic”微调叠加去审查的多重修改版。

- [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) — empero-ai | 点赞 197 | 下载 32,454  
  Ridge 量化版，面向低资源推理的 GGUF 格式。

- [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) — Comfy-Org | 点赞 1,442 | 下载 15,213,225  
  MiniMax-H3 的 ComfyUI 单文件版，下载量高达 1,521 万，为视频行业部署首选。

- [**Comfy-Org/MiniMax-Music-3**](https://huggingface.co/Comfy-Org/MiniMax-Music-3) — Comfy-Org | 点赞 193 | 下载 325,083  
  MiniMax-Music3 的 ComfyUI 版，将音乐生成无缝接入 ComfyUI 工作流。


## 生态信号

**Qwen3.8 成为绝对统治级生态**：27B 模型从 4bit 到 FP8 的量化链条已完善，且社区迅速形成去审查（abliterated/uncensored）微调矩阵——至少 7 个独立去审查变体同时上榜，合计下载超 1,500 万次，表明开发者对“无限制”本地部署有巨大需求。**多模态视频生成是另一大热点**：MiniMax-H3 及其衍生（Turbo、ComfyUI 版、社区微调）合计下载逼近 1,900 万次，表明视频生成正在从“可用”迈向“好用”。**开源权重持续领先**：本周热榜头部全部为开源模型，DeepSeek V4 与 Kimi-K3 的强势上榜进一步巩固了“开源旗舰”路线。值得警惕的是，Qwen 系列相关模型占据榜单近 2/3，生态呈现明显的“单一家族依赖”特征——一旦 Qwen3.8 后续迭代乏力，社区可能面临无米之炊的风险。


## 值得探索

1. [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — 压缩张量技术在超大规模多模态模型上的首次大规模应用，近 1.1 万点赞证明其价值，对研究推理优化与模型压缩极具参考意义。

2. [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) — 音乐生成是当前 AIGC 相对“蓝海”的赛道，MiniMax 将其视频生成的成功经验迁移至音频领域，配合 Comfy-Org 的 ComfyUI 适配，值得音乐创作者与研究者深入尝试。

3. [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) — 2.4T 总参数的 MoE 旗舰，代表当前开源模型规模的上限。对于研究稀疏激活、大规模训练部署的团队，这是不可多得的田野样本。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*