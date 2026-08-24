# Hugging Face 热门模型日报 2026-08-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-24 00:31 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-24

---

## 📌 今日速览

今日 Hugging Face 趋势榜被 **Qwen3.8-27B** 家族全面占领——原始多模态模型以 1.2万+ 周点赞登顶，其衍生量化版（GGUF）、去审查版（Uncensored/Abliterated）几乎包揽前十过半数席位，社区对 27B 级别的本地部署与个性化微调热情空前。视频生成赛道出现两员猛将：Lightricks 的 **LTX-2.5** 与 MiniMax 的 **MiniMax-H3**（4.3k 点赞、404万下载），表明高质量开源视频生成模型竞争已进入白热化。MoE 架构持续发力：ornith-ai 的 **Ornith-1.5-35B-A3B** 与 DeepSeek 的 **V4 系列** 均采用稀疏激活设计，验证了大模型"小而快"的务实路线。此外，Kimi-K3 以 1.1万 点赞强势回归，并携带 `compressed-tensors` 标签，暗示国产模型在推理效率优化上的新布局。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|-----------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,313 | 2,358,347 | 新一代多模态对话旗舰，支持图像+文本联合输入，27B 规模兼顾性能与部署友好性，是今日榜单的绝对核心。 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,652 | 3,089,709 | DeepSeek V4 的轻量快速版，主打低延迟高吞吐对话，推理成本优化明显，适合生产环境大规模部署。 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 734 | 57,928 | V4 系列旗舰版，更强推理与生成能力，面向复杂任务场景，周内发布即上榜。 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,950 | 2,727,920 | Kimi 第三代多模态模型，自带 `compressed-tensors` 标签，长上下文处理与压缩推理是核心卖点。 |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 364 | 23,516 | MoE 架构 35B 总参数、3B 激活，MIT 协议开源，极致推理效率，是中小团队自部署的优选。 |
| [ornith-ai/Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 182 | 31,496 | Ornith 系列小尺寸版，同样是 Qwen3.5-MoE 基座改造，主打边缘设备与轻量场景。 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 214 | 2,280 | 基于 Qwen3 的小型语音识别+生成模型，标签含 `asr`，探索语音到文本的轻量化路径。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|-----------|
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,641 | 738,345 | 新一代视频生成模型，同时支持图像到视频、文本到视频、视频到视频，单文件扩散模型便于集成。 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,378 | 4,039,236 | MiniMax 视频生成最新版本，404万下载量印证其在社区的广泛使用，文本/图像双驱动。 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,205 | 17,421 | 文本到音乐生成模型，基于 Diffusers 框架，带 `minimax_music3` 标签，开启 AI 作曲新篇章。 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 672 | 2,653,678 | 官方 FP8 量化版本，在保留多模态能力的同时大幅降低显存占用，是高效部署官方推荐选项。 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

> 本期榜单暂无典型专用模型（代码、数学、医疗、嵌入专用）进入前 30。Qwen3.8 系列与 DeepSeek-V4 主打通用对话与多模态，专用模型方面可关注 ornith-ai 系列在 MoE 效率上的技术积累。

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|-----------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,738 | 6,674,515 | 社区量化标杆 unsloth 出品，667万下载量居全榜第一，是本地 CPU/GPU 混合推理的首选 GGUF 版本。 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,047 | 190,062 | FP8 精度下的去审查版本，在安全性与表达能力间提供新选择，适合内容创作探索。 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 953 | 47,098 | 面向 Apple Silicon 的 MLX 格式去审查版，`abliterated` 技术移除安全对齐限制，Mac 用户本地运行更流畅。 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 648 | 1,334,820 | GGUF 格式去审查版，133万下载量说明社区对"无限制"模型的需求旺盛，支持 MTP 加速。 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 632 | 244,834 | "抹除"安全层的中立版本，同时提供 MLX/GGUF 双格式，命名直观，社区关注度高。 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 538 | 676,697 | 激进风格去审查 + MTP 加速的 GGUF，67万下载，满足特定用户对"个性"与速度的双重需求。 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 258 | 24,844 | 知名"去审查"社区作者 huihui-ai 的全精度版本，可作为进一步量化的干净基座。 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 297 | 943,360 | 上述模型的 GGUF 版本，94万下载验证其口碑，端侧运行更便捷。 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 375 | 108,666 | 同系列 GGUF 版，标签完整，适合 llama.cpp 生态用户直接使用。 |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 202 | 36,234 | 引入 DFlash2 投机解码技术，推理速度提升明显，是"更快 Qwen"的代表作。 |
| [incoai/Qwen3.8-27B-DFlash2](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2) | incoai | 162 | 69,783 | 另一个 DFlash2 实现，与 z-lab 版形成竞争，探索投机解码的不同训练策略。 |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 209 | 193,794 | 集成冷融合与 GAIN 训练技术，外加 MTP 加速，代表社区"炼丹"上限。 |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 250 | 131,435 | "Ridge" 版量化，标签含 `qwen3.5`，在压缩率与质量间取得平衡的新尝试。 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 245 | 579,334 | "异端"命名风格，57万下载，延续去审查 + GGUF 的社区主流配方。 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,420 | 0 | 纯工具型仓库，修复 Qwen 系列对话模板 Jinja 语法问题，被大量开发依赖（下载为0但点赞极高）。 |
| [peculiar-ragdoll/Qwen-Sharp-Chat-Templates](https://huggingface.co/peculiar-ragdoll/Qwen-Sharp-Chat-Templates) | peculiar-ragdoll | 199 | 0 | 同类"对话模板修复"项目，"Sharp" 命名主打精度，是管线开发的隐形基础设施。 |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 252 | 369,478 | MoE 模型的官方 GGUF 量化，MIT 协议 + 端侧兼容，让 35B 模型在消费级硬件上可用。 |
| [ornith-ai/Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 176 | 359,078 | 9B 版的 GGUF 版本，进一步下探硬件门槛，是移动端与嵌入式场景的潜力股。 |
| [LBH-123-AI/Minimax_h3_latent_Upscaler](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) | LBH-123-AI | 166 | 0 | MiniMax-H3 的潜空间放大工具，虽无下载但点赞可观，是视频生成工作流的重要配件。 |

---

## 📊 生态信号

**1. Qwen 家族"一超多强"格局确立**：Qwen3.8-27B 原版以 12k 点赞一骑绝尘，其衍生生态（量化、去审查、加速）占据了榜单近 60% 席位。这表明 **Qwen 已成为开源社区的事实标准基座**，超过了此前 Llama 系的统治地位，且 27B 参数规模恰好卡在"能力与可部署性"的甜蜜点。

**2. "去审查"（Uncensored/Abliterated）需求旺盛**：仅 Qwen3.8-27B 就有 6+ 个去审查变体同时上榜，累计下载超 300 万。该现象反映开发者对开放式创造、角色扮演与写作自由的需求长期存在，而 Abliterated 技术（抹除拒绝方向）已成为社区标准操作。

**3. 量化与加速双轮驱动**：GGUF 格式占据下载量绝对多数（unsloth 版 667 万），FP8/MLX/投机解码（DFlash2、MTP）等多条技术路线并行竞争，说明**部署效率成为模型能否被广泛使用的关键分水岭**。

**4. 视频生成进入"军备竞赛"**：MiniMax-H3（404 万下载）与 LTX-2.5（73.8 万下载）同周上榜，叠加音频模型 MiniMax-Music3，多模态生成已从"看图说话"全面转向"动态内容生产"。

**5. MoE 与压缩推理成为长期趋势**：Ornith 系列（35B-A3B）、DeepSeek-V4 系列与 Kimi-K3 的 `compressed-tensors` 标签，共同指向同一方向——**用稀疏激活与结构压缩换取更低的推理成本**，这是开源模型对抗闭源 API 的关键武器。

---

## 🔬 值得探索

1. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — 榜单之王的原版模型：如果你想了解未来半年开源多模态的技术基线，或基于最强基座开发应用，它是不二之选。其官方 FP8 版本（[Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8)）也值得同时研究，作为效率参考。

2. **[orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX)** — 对于 Mac 用户与 AI 产品原型设计者，这是最值得尝试的"无限制"版本。MLX 格式在 Apple Silicon 上运行流畅，配合 `abliterated` 技术，可作为创意工具或角色扮演应用的私有部署基座。

3. **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — 单日 1420 赞却零下载，这个"隐形冠军"修复了 Qwen 系列对话模板的关键 BUG。无论你是模型微调工程师还是应用开发者，将其集成进推理管线都能避免无数隐性问题，值得立即收藏并研究其 Jinja 模板差异。

---

> 📅 数据统计窗口：2026-08-18 至 2026-08-24 | 榜单来源：Hugging Face Hub Trending

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*