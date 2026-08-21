# Hugging Face 热门模型日报 2026-08-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-21 00:32 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-21

## 📌 今日速览

今日榜单由 **Qwen3.8-27B** 系列以压倒性优势领跑，不仅官方原版以 11.7K 周赞登顶，其 GGUF、FP8 等量化衍生版本也纷纷上榜，成为绝对焦点。**MiniMax-H3** 与 **LTX-2.5** 继续引领视频生成赛道，下载量分别突破 330 万和 61 万。**Kimi-K3** 以 10.9K 点赞紧随其后，模型压缩技术成为亮点。值得关注的是，社区涌现出大量基于 Qwen3.8 的 "abliterated"（去审查）微调变体，形成独特的生态文化。DeepSeek 系列延续热度，V4 系列双版本上榜。

---

## 🔥 热门模型

### 🧠 语言模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,883 | 2.35M | Kimi 最新多模态模型，主打 compressed-tensors 特征提取，开源后迅速引爆社区 |
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 678 | 43K | DeepSeek V4 专业版，持续强化复杂推理与代码能力 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,575 | 2.55M | V4 闪电版，主打低延迟推理，下载量巨大，备受开发者青睐 |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,121 | 14.6K | 2.4T 参数 MoE 旗舰，仅激活 95B，稀疏架构极致之作 |
| [Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 214 | 1.7K | 35B 总量/3B 激活的高效 MoE，多模态文本生成新秀 |

### 🎨 多模态与生成

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,743 | 1.37M | 旗舰多模态对话模型，图文理解能力全面进化，周赞榜首 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 633 | 1.52M | FP8 精度官方量化版，大幅降低显存门槛，下载量反超原版 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,238 | 3.31M | 新一代图生视频/文生视频模型，效果惊艳，下载量今日最高 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,104 | 14.5K | 第三代音乐生成模型，支持文本直接生成完整乐曲 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,415 | 611K | 全能视频生成模型，支持图/文/视频到视频多模式转换 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 652 | 380K | MiniMax-H3 的 Turbo 加速版，推理效率显著提升 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,718 | 478K | Meta 多模态新作，30B 参数兼顾理解与生成 |
| [TenStrip/10Eros-Max](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 298 | 0 | 基于 MiniMax-H3 的成人内容微调版，引发伦理讨论 |
| [dots-studio/dots3-note-prev](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 242 | 1.4K | 音符识别与乐谱生成专用多模态模型 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 152 | 348 | 集成 ASR 能力的轻量级文本生成模型，语音转文字新方向 |

### 🔧 专用模型（暂无独立类别，归入相应品类）

### 📦 微调与量化

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,355 | 5.13M | 最受欢迎的 GGUF 量化版，下载量全网登顶，本地部署首选 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 308 | 831K | 新一代 NVFP4 量化格式，专为 NVIDIA 平台优化 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 712 | 2.6K | Apple Silicon 专用 MLX 格式，abliterated 去审查版 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 676 | 76.1K | FP8 精度的去审查版，在开发者圈层快速扩散 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 512 | 979K | 去审查 GGUF 版本中的下载冠军 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 364 | 268K | 带 MTP（多 token 预测）加速的去审查版 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,338 | 0 | 修复 Qwen 系列对话模板的专用工具库，0 下载却高赞实属罕见 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 266 | 4.4K | 同时提供 MLX/GGUF 双格式的去审查版 |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 222 | 55.1K | Ridge 量化方案，在低 bit 下保持更好质量 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 239 | 52.4K | orcarouter 出品的 GGUF 去审查版 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 200 | 187K | 知名量化专家 huihui 出品的 GGUF 版 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 200 | 10.5K | huihui 原始 safetensors 版去审查模型 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 189 | 326K | “异端级”激进去审查版本 |
| [Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) | Blackfrost-AI | 183 | 186K | Blackfrost 出品的去审查 GGUF 量化版 |
| [Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 160 | 53.7K | 高效 MoE 模型的 GGUF 量化版本 |

---

## 📊 生态信号

**1. Qwen 生态一家独大：** Qwen3.8-27B 系列以超过 14 个衍生模型占据榜单半壁江山，从官方原版到 GGUF/FP8/NVFP4/MLX 多格式覆盖，加上社区的 abliterated 变体和 chat template 修复工具，围绕单一模型的生态已经相当成熟，类似此前 Llama 的开源生态范式。

**2. "去审查"（Abliteration）成为社区显学：** 至少 9 款模型为 abliterated/uncensored 变体。这说明开源社区对模型安全对齐的态度呈现分裂——一方面官方持续强化安全，另一方面大量用户追求"无约束"模型用于角色扮演、创意写作等场景。值得关注的是，这一趋势正在从 GGUF 小圈子走向主流。

**3. 量化格式百花齐放：** GGUF 仍占主导，但 NVFP4 作为 NVIDIA 新格式快速崛起（83 万下载），MLX 在 Apple 生态亦有稳定需求。unsloth 已从量化工具商成长为模型发布平台。

**4. 视频生成竞争白热化：** MiniMax-H3 下载量已超 330 万，同日还有 LTX-2.5、Minimax-h3-Turbo 及微调衍生版上榜，显示了视频生成赛道的狂热。音乐生成（MiniMax-Music3）也开始崭露头角。

**5. 权重开放仍是主流：** 榜单 30 款模型全部开放权重，开源社区持续繁荣。MoE 架构（Qwen3.8-2.4T、Ornith-1.5）成为提升参数规模的新路径。

---

## 🔬 值得探索

1. **Qwen/Qwen3.8-2.4T-A95B** — 2.4T 总参数、激活仅 95B 的 MoE 巨兽，代表稀疏化方向的最前沿。若你有多卡 A100/H100 环境，这将是对 MoE 推理效率的极限考验。同时可以参考 unsloth 的 GGUF 版降低体验门槛。

2. **moonshotai/Kimi-K3** — 将 "compressed-tensors" 作为标签的模型极为罕见，10.9K 周赞证明其技术含量非同一般。建议研究其压缩机制如何兼顾多模态理解能力与推理效率。

3. **MiniMaxAI/MiniMax-H3** — 3.3M 下载量为今日之最，图生视频质量获得社区高度评价。搭配同日发布的 Turbo 版进行对比测试，可以快速衡量当前开源视频生成的最高水平。

4. **froggeric/Qwen-Fixed-Chat-Templates** — 一个"0 下载却获得 1338 赞"的反常模型，不包含权重而是提供修复后的对话模板。这提示了模板质量对模型实际表现的影响被严重低估——对任何使用 Qwen 系列的开发者都值得一看。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*