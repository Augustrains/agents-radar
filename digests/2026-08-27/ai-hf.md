# Hugging Face 热门模型日报 2026-08-27

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-27 05:22 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-27

## 📰 今日速览

今日 Hugging Face 榜单呈现显著的“三强争霸”格局：**Qwen 系列**以绝对优势霸榜，原版与社区衍生（GGUF、abliterated、uncensored）版本合计占据榜单近半席位；**DeepSeek-V4-Flash** 单日点赞 3.7k、下载近 400 万，成为文本生成领域最受关注的新秀；**Kimi-K3** 以 11k 点赞位居第二，压缩推理路线表现亮眼。多模态侧，**MiniMax** 双线发力——H3 视频模型下载量突破 479 万，Music3 音频模型进一步拓展创作边界。值得关注的是，**“解禁（Uncensored）”微调生态空前活跃**，围绕 Qwen3.8-27B 的解禁变体多达 8 个，社区对“安全对齐”之外的原始能力释放需求强烈。


## 🔥 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 12,929 | 3.3M | Qwen 旗舰多模态对话模型，单周点赞破万，全能型主力 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,743 | 3.9M | DeepSeek V4 轻量版，高性价比对话模型，下载量惊人 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 11,023 | 2.9M | Kimi 第三代压缩权重多模态模型，点赞过万，开发者关注度极高 |
| [zai-org/GLM-5.3-Flash](https://huggingface.co/zai-org/GLM-5.3-Flash) | zai-org | 1,002 | 0 | GLM 新一代轻量模型，刚上线即登榜，待社区下载验证 |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 456 | 83K | 35B 总参/3B 激活 MoE 模型，Qwen3.5 架构衍生，低激活高效推理 |
| [ornith-ai/Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B) | ornith-ai | 229 | 119K | 9B 全参版本，MIT 协议，适合端侧部署 |
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 252 | 3.9K | 轻量级文本生成+ASR 模型，主打语音场景 |
| [sensenova/SenseNova-U1.5-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1.5-8B-MoT) | sensenova | 174 | 3.3K | 原生多模态 any-to-any 模型，商汤 SenseNova 新品 |


### 🎨 多模态与生成（图像、视频、音频）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [Qwen/Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) | Qwen | 3,723 | 2.6K | Qwen 最新多模态旗舰，Flash 架构迭代版，刚发布即登顶趋势 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,505 | 4.8M | H3 视频生成模型，下载近 500 万，MiniMax 生态核心 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,265 | 19.5K | 第三代音乐生成模型，支持文生音乐/曲风控制 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,876 | 894K | 多功能视频模型（图生视频/文生视频/视频生视频），Lightricks 旗舰 |
| [alibaba-pai/MiniMax-H3-Fun-Controlnet-Union](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union) | alibaba-pai | 141 | 3.1K | 阿里 PAI 为 MiniMax-H3 打造的 ControlNet 统一控制插件 |
| [Audio8/Audio8-TTS-Preview-0.1b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b) | Audio8 | 176 | 4.3K | Audio8 预览版 TTS 模型，0.1B 超轻量语音合成 |


### 📦 微调与量化（社区微调、GGUF、量化）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 3,014 | 7.6M | 官方 GGUF 量化版，下载量断层第一，本地部署首选 |
| [unsloth/Qwen3.8-Flash-Next-GGUF](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF) | unsloth | 374 | 0 | Flash-Next 的 GGUF 版本，上线即受关注 |
| [unsloth/GLM-5.3-Flash-GGUF](https://huggingface.co/unsloth/GLM-5.3-Flash-GGUF) | unsloth | 133 | 0 | GLM 5.3 Flash 量化版，低资源运行 GLM 新架构 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 1,143 | 79K | 解禁版 MLX 格式，Apple Silicon 本地运行 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 1,180 | 270K | FP8 精度解禁版，兼顾质量与性能 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 476 | 184K | 解禁版 GGUF 量化系列 |
| [orcarouter/Qwen3.8-27B-Uncensored](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored) | orcarouter | 193 | 17.6K | 解禁版基础模型（abliterated） |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 817 | 469K | “抹除对齐”版 Qwen3.8，社区热度极高 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 665 | 912K | 激进解禁 + MTP 加速 + GGUF，社区魔改集大成者 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 757 | 1.6M | 个人开发者量化，下载超 160 万，社区认可度高 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 378 | 1.3M | 知名量化作者 huihui-ai 出品，解禁+GGUF |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 255 | 233K | GAIN 训练 + Cold-Fusion 微调，多技术栈叠加魔改 |
| [EschaLabs/Qwen3.8-27B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.8-27B-Escha-W2) | EschaLabs | 134 | 2.5K | 2-bit 极限量化，极致压缩探索 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,489 | 0 | 修复 Qwen 系聊天模板的工具集，高赞说明刚需 |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 318 | 1.4M | MoE 版 GGUF，MIT 协议，下载量可观 |
| [ornith-ai/Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF) | ornith-ai | 221 | 1.4M | 9B 量化版，轻量部署热门选择 |


## 📡 生态信号

**Qwen 生态一家独大**：原版 + unsloth 量化 + 社区解禁微调，Qwen3.8 系列在榜单形成完整金字塔——原版积攒口碑、量化承接部署、解禁版满足长尾需求，这种生态位分工值得其他厂商借鉴。

**“解禁”成为显学**：围绕 Qwen3.8-27B 的解禁（abliterated/uncensored）变体多达 8 个（orcarouter、OBLITERATUS、HauhauCS、JonathanColetti、huihui-ai 等），侧面反映用户在追求对齐之外的“原始能力”，预计该趋势将持续扩散至 GLM、DeepSeek 等模型。

**开源权重持续繁荣**：本周榜单所有模型均开源权重，MiniMax、Lightricks 等闭源 API 公司也选择开放权重抢占开发者心智。**GGUF 量化成为标配**——前 10 名中 4 个是 GGUF 版本，unsloth 以 760 万下载断层领先，本地推理生态高度成熟。

**DeepSeek / Kimi 构成第二梯队**：DeepSeek-V4-Flash 与 Kimi-K3 在点赞与下载上呈追赶态势，但与 Qwen 生态的社区衍生规模差距明显。


## 🔬 值得探索

1. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — 生态核心、能力标杆。点赞与下载均为榜首，了解 Qwen3.8 全家桶能力上限的最佳入口，同时是理解社区所有衍生模型的“根模型”。

2. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 压缩权重路线代表。点赞 1.1 万仅次于 Qwen 原版，关注“用更小存储达到相近能力”的技术路线，是研究模型压缩与推理效率的绝佳样本。

3. **[orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8)** — 解禁生态样本。FP8 精度在质量与效率间取得良好平衡，可借此研究“安全对齐移除对模型能力的影响”，也是本地部署质量敏感场景的优选。

---

*数据来源：Hugging Face Hub 热门模型榜（按周点赞数排序）*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*