# Hugging Face 热门模型日报 2026-08-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-15 00:30 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-15

---

## 📌 今日速览

本周 Hugging Face 趋势榜呈现**多模态生成全面爆发**的格局：MiniMax-H3 视频生成模型家族霸榜（原版 + ComfyUI 单文件 + 多个 LoRA 变体合计斩获超 7 千点赞、超 1400 万下载）；Moonshot AI 的 **Kimi-K3** 以 10,672 周点赞登顶，成为本周最受关注的模型；Qwen 团队密集发布 Qwen3.8 系列的多规格版本（27B 密集、2.4T MoE 及 FP8 量化版），巩固多模态语言模型布局；DeepSeek-V4-Flash 以大模型身份跻身下载前列。开源权重模型持续主导榜单，GGUF 量化和第三方微调生态活跃。

---

## 🔥 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 913 | 3,832 | Qwen3.8 系列的旗舰 MoE 模型，2.4T 总参数 / 95B 激活，本周热度最高的纯文本 LLM 之一 |
| [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,383 | 1,606,491 | DeepSeek V4 Flash 版本，以高效推理著称，下载量达 160 万+，社区部署热度极高 |
| [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 433 | 245 | V4 Pro 最新迭代版，性能更强但刚发布不久，下载量尚小 |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 615 | 124,172 | Liquid 第二代 2.6B 小模型，主打高性价比边缘部署 |
| [**nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 257 | 119,572 | Nemo tron 3.5 闪电版：30B 总参 / 3B 激活 + NVFP4 量化，兼顾质量与效率 |
| [**nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 143 | 34,137 | 上述模型的 BF16 全精度版本，适合追求极致精度的场景 |

### 🎨 多模态与生成（图像 / 视频 / 音频 / 文本到X）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **10,672** | 1,974,635 | 本周点赞冠军，Kimi 第三代多模态模型，支持特征提取 + 压缩张量，热度极高 |
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 8,972 | 2 | 本周新发布的 Qwen3.8 多模态对话模型，27B 密集架构，发布即引爆关注 |
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,920 | **1,997,541** | MiniMax 新一代视频生成模型，支持文生视频 / 图生视频，下载接近 200 万 |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,511 | 165,300 | Meta 多模态对话模型，可同时理解图像与文本，社区讨论度极高 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 855 | 207,830 | 轻量级图生视频模型，支持多模态输入，适合创意工具集成 |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 651 | 63 | MiniMax 音乐生成模型的第三代，支持文生音乐，新发布热度待释放 |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 493 | 149,865 | MiniMax-H3 的 Turbo 加速版本，推理速度显著提升 |
| [**Gazingstars123/Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 162 | 10,106 | 动漫风格文生图模型，单文件格式，适配 ComfyUI |
| [**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 381 | 1,366 | NVIDIA 语音对话模型，主打端到端语音交互场景 |

### 📦 微调与量化（社区微调 / GGUF / LoRA）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,317 | **11,768,622** | MiniMax-H3 的 ComfyUI 单文件版本，**全网下载量第一**，是视频生成工作流的事实标准 |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,016 | 2,891,524 | 社区微调 Qwen3.6 的 GGUF 版本，主打"无审查"风格，下载量近 300 万，争议与热度并存 |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 414 | 596,774 | Unsloth 出品的 Meta 模型 GGUF 量化版，本地部署首选 |
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 788 | 0 | Qwen3.8-27B 的 GGUF 量化版，已随原版同步发布 |
| [**larryvrh/MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 741 | 0 | MiniMax-H3 Turbo 的 LoRA 适配层，用于风格定制 |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 318 | 112,975 | 专为 ComfyUI 优化的 H3 Turbo LoRA，下载量已超 11 万 |
| [**fal/MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 176 | 9,060 | 为 MiniMax-H3 增加真人写实风格的 LoRA |
| [**unsloth/MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 156 | 136,774 | MiniMax-H3 的 GGUF 量化版，借助 stable-diffusion.cpp 实现本地视频生成 |
| [**meta-models/Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 270 | 228,364 | Meta 官方出品的 GGUF 版本，附带最新 arXiv 论文引用 |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 310 | 473 | 社区风格化微调的 MiniMax-H3，适配 transformers + 端点部署 |
| [**Kijai/MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 339 | 0 | ComfyUI 节点工作流封装，简化 H3 模型的调用流程 |

---

## 📊 生态信号

**模型家族格局：** 本周生态呈现清晰的"三足鼎立"——**MiniMax-H3** 统治视频生成赛道（原版 + ComfyUI + LoRA + GGUF 构成完整生态链），**Qwen3.8** 系列在语言与多模态领域全面出击（27B 密集、2.4T MoE、FP8 量化多规格并行），**DeepSeek-V4** 继续在高性能推理市场保持强势。

**开源权重趋势：** 榜单 30 个模型全部为开源权重，无一闭源，印证了开放权重模型已成为 AI 生态的绝对主流。值得注意的是 Meta（Muse-Glimmer）、NVIDIA（Nemotron）、Moonshot（Kimi-K3）等大厂均在积极开源其旗舰模型。

**量化与微调活动：** Unsloth 已成为 GGUF 生态核心基础设施，几乎所有热门模型都有其量化版本；DavidAU 等社区作者的"无审查"微调模型下载量惊人，反映部分用户对安全对齐的差异化需求；MiniMax-H3 的 LoRA 生态（真人写实、Turbo 加速、ComfyUI 适配）是最活跃的微调社区。

---

## 🔭 值得探索

1. **Kimi-K3**（[链接](https://huggingface.co/moonshotai/Kimi-K3)）
   本周点赞榜冠军，10.6K 赞远超其他模型。值得关注的是其压缩张量技术，如果能在保持质量的前提下显著减少显存占用，很可能成为继 DeepSeek 之后中国大模型出海的新标杆。

2. **MiniMax-H3**（[链接](https://huggingface.co/MiniMaxAI/MiniMax-H3)）
   视频生成模型的新里程碑。其 ComfyUI 单文件版本下载量已达 1,176 万次，远超任何对话模型。强烈建议体验其图生视频和文生视频质量，并关注其 Turbo 和 LoRA 衍生生态。

3. **Qwen3.8-2.4T-A95B**（[链接](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)）
   Qwen 团队在 MoE 架构上的最新探索——2.4T 总参数但仅激活 95B，配合 FP8 量化版本，代表了前沿 LLM 在"规模-效率"权衡上的最新方向。对比其密集版 27B 使用效果，可洞察 MoE 与密集型架构的实战差异。

---

*日报生成时间：2026-08-15 | 数据来源：Hugging Face Hub 趋势榜*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*