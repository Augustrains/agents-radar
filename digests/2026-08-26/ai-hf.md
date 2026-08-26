# Hugging Face 热门模型日报 2026-08-26

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-26 00:32 UTC

---

# Hugging Face 热门模型日报（2026-08-26）

## 📌 今日速览

本周 Hugging Face 榜单呈现 **"Qwen 生态独领风骚"** 的鲜明格局：Qwen3.8-27B 以 12.7k 周点赞高居榜首，并衍生出至少 10 余个微调/量化/去审查变体，覆盖 GGUF、MLX、FP8 等全格式生态。**MiniMax** 双线出击——视频模型 H3（4.5k 赞）与音乐模型 Music3 双双入榜，成为多模态生成的最大赢家。**DeepSeek-V4** 系列三款模型齐上榜，其中 Flash 版本（3.7k 赞）实力不俗。值得关注的是，**orcarouter 与 OBLITERATUS 的 "Uncensored" 系列** 在社区掀起二次创作浪潮，占据榜单近三分之一席位，反映出去审查与个性化定制已成社区刚需。

---

## 🏆 热门模型分类

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,707 | 2,945,415 | Qwen 团队最新多模态旗舰，支持图像+文本联合输入，本周热度绝对王者 |
| [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,714 | 3,528,373 | DeepSeek V4 系列闪电版，轻量级高性价比，下载量全榜第三 |
| [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 758 | 74,707 | V4 专业版，性能更强，适合高复杂度推理场景 |
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,996 | 2,865,293 | Kimi 第三代模型，采用压缩张量技术，多模态理解能力突出 |
| [**ornith-ai/Ornith-1.5-35B-A3B**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 419 | 70,158 | MoE 架构（35B 总量/3B 激活），Qwen3.5-MoE 基座，MIT 协议 |
| [**ornith-ai/Ornith-1.5-9B**](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 216 | 98,323 | Ornith 系列 9B 精简版，支持多模态输入 |
| [**superwhisper/s1-mini**](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 238 | 3,474 | 轻量级 ASR+文本生成双功能模型，端侧部署友好 |
| [**sensenova/SenseNova-U1.5-8B-MoT**](https://huggingface.co/sensenova/SenseNova-U1.5-8B-MoT) | sensenova | 152 | 2,682 | 商汤 SenseNova 原生多模态 MoT 模型，any-to-any 全模态转换 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,457 | 4,639,786 | 视频生成旗舰，支持文本/图像/视频到视频，下载量全榜第一 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,798 | 833,845 | 全能视频生成模型（图/文/视频→视频），Diffusion 单文件格式 |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,245 | 18,705 | 文本一键生成完整音乐，Diffusers 生态音乐生成新标杆 |
| [**Audio8/Audio8-TTS-Preview-0.1b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b) | Audio8 | 156 | 3,640 | 全新 TTS 预览版，基于 ArkTTS 架构，语音合成新玩家 |

### 🔧 专用模型（代码、数学、医疗、嵌入等）

> 本期榜单以通用 LLM 与多模态生成模型为主，未见突出专用模型上榜。

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,915 | 7,334,695 | 官方 GGUF 量化版，下载量全榜第一，本地部署首选 |
| [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 1,094 | 68,855 | Apple Silicon 专用 MLX 格式去审查版 |
| [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,148 | 249,744 | FP8 精度去审查版，兼顾质量与效率 |
| [**OBLITERATUS/Qwen3.8-27B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 748 | 389,747 | 采用 abliterated 技术深度去审查，多格式发布 |
| [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 721 | 1,525,645 | 支持 MTP 加速的 GGUF 去审查版，社区热度极高 |
| [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 622 | 832,185 | "激进"去审查 + MTP 加速，GUF 格式中的另类选择 |
| [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 357 | 1,230,831 | 知名社区量化作者 huihui 出品，下载量过百万 |
| [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 275 | 735,183 | "Heretic" 风格去审查版，社区口味差异化输出 |
| [**orcarouter/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 452 | 154,225 | 同系列 GGUF 格式版本 |
| [**orcarouter/Qwen3.8-27B-Uncensored**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored) | orcarouter | 183 | 15,341 | 原版 FP16 去审查版本 |
| [**z-lab/Qwen3.8-27B-DFlash2**](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 227 | 64,984 | DFlash2 投机解码技术，提升推理速度 |
| [**incoai/Qwen3.8-27B-DFlash2**](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2) | incoai | 179 | 105,786 | 另一团队同思路 DFlash2 实现 |
| [**EschaLabs/Qwen3.8-27B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.8-27B-Escha-W2) | EschaLabs | 126 | 2,319 | 2-bit 极致量化探索，极限内存场景实验性作品 |
| [**DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 240 | 221,918 | GAIN+COLD-FUSION 复合增强训练技术，命名狂野 |
| [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,468 | 0 | 修正版 Qwen 对话模板（Jinja），高赞但零下载，或为链接跳转工具 |
| [**peculiar-ragdoll/Qwen-Sharp-Chat-Templates**](https://huggingface.co/peculiar-ragdoll/Qwen-Sharp-Chat-Templates) | peculiar-ragdoll | 244 | 0 | 同上，社区对话模板修正方案 |
| [**ornith-ai/Ornith-1.5-35B-A3B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 297 | 1,156,903 | MoE 模型 GGUF 量化版，兼容各大推理框架 |
| [**ornith-ai/Ornith-1.5-9B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 201 | 1,144,037 | 9B 版 GGUF 量化版，轻量级部署优选 |

---

## 🌐 生态信号

**Qwen 生态近乎垄断**：Qwen3.8-27B 及其衍生模型占据榜单 20/30 席位，构成从官方权重 → FP8/MLX/GGUF 量化 → abliterated 去审查 → DFlash2 投机解码的完整产业链，形成"基础模型+社区生态"双层结构，影响力直追当年 Llama 系列。

**"Uncensored" 产业链成熟**：去审查模型已形成标准化流程——先有核心团队（orcarouter/OBLITERATUS）发布多种格式去审查版，再有社区跟进 GGUF/MLX 等定制化版本。值得警惕的是，这类模型在法律与合规层面存在争议，但在开源社区中需求旺盛。

**量化竞赛白热化，多模态 + MoE 成新风向**：从 2-bit（EschaLabs）到 FP8 到 GGUF，量化粒度颗粒度持续细分，下载量验证了 GGUF 仍是本地部署的绝对主流。此外，MoE（Ornith）与多模态（MiniMax/DeepSeek）双轮驱动，榜单中非 Qwen 模型的入榜均为多模态或 MoE 形态，单一文本 LLM 的时代正渐行渐远。

---

## 🔬 值得探索

1. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 10,996 点赞逼近 Qwen 旗舰，压缩张量技术值得深入研究。Kimi 系模型一直以中文长文本能力见长，K3 的多模态升级可能代表国产模型的新高度。

2. **[ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B)** — MIT 协议 + MoE 架构 + 35B 总量仅 3B 激活，性能/资源比极具吸引力。在 GGUF 量化后（36B 版下载 115 万次）已获大量验证，代表高效推理的未来方向。

3. **[obliviated 系列：orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX)** — MLX 格式 + abliterated 技术组合，在 Apple Silicon 生态实现近乎无损的去审查效果。尽管内容合规存在风险，但其工程实现本身极具研究价值，是观察社区"如何绕过安全对齐"的最佳样本。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*