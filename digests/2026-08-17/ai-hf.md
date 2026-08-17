# Hugging Face 热门模型日报 2026-08-17

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-17 00:29 UTC

---

# 🤖 Hugging Face 热门模型日报（2026-08-17）

## 📰 今日速览

今日 HF 趋势榜由 **Qwen3.8 系列** 主导，旗舰多模态模型 `Qwen3.8-27B` 以 10,276 周点赞登顶，其 GGUF 量化版下载量突破 190 万次领跑生态。**Moonshot AI 的 `Kimi-K3`** 以 10,767 点赞紧随其后，采用压缩张量技术引起广泛关注。视频生成赛道竞争白热化，**MiniMax-H3** 全家桶（官方 + Comfy-Org + LoRA + Turbo）霸榜多席，其中 Comfy-Org 版下载达 1,340 万。DeepSeek 与 NVIDIA 的 MoE 新作也持续走高，**Jamba 式混合架构**与 **FP8/NVFP4 量化**成为本周技术关键词。


## 🔥 热门模型

### 🧠 语言模型（LLM / 对话）

**1. Qwen/Qwen3.8-2.4T-A95B**
[链接](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | 作者: Qwen | 👍 1,010 | ⬇️ 7,932
Qwen 旗舰级 MoE 文本模型（2.4T 总参 / 95B 激活），为追求极致语言能力的用户提供超大规模稀疏方案。

**2. deepseek-ai/DeepSeek-V4-Pro-0813**
[链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | 作者: deepseek-ai | 👍 536 | ⬇️ 21,873
DeepSeek V4 系列“Pro”版本（0813 迭代），聚焦推理与指令跟随的完整精度旗舰权重。

**3. deepseek-ai/DeepSeek-V4-Flash-0731**
[链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | 作者: deepseek-ai | 👍 3,459 | ⬇️ 1,872,232
V4 系列高性价比“Flash”版，下载量近 190 万，是社区部署快速推理的首选。

**4. nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**
[链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | 作者: nvidia | 👍 291 | ⬇️ 196,326
NVIDIA H 系列 30B-A3B MoE，NVFP4 量化版为本地高吞吐部署优化。

**5. nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**
[链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | 作者: nvidia | 👍 160 | ⬇️ 66,253
Nemotron 3.5 精度的 BF16 权重版本，保留完整精度供微调与学术研究。

**6. LiquidAI/LFM2.5-2.6B**
[链接](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | 作者: LiquidAI | 👍 647 | ⬇️ 141,009
基于液态神经网络（LFM2）的 2.6B 高能效模型，以极小参数量实现出色表现。

**7. dots-studio/dots3-note-prev**
[链接](https://huggingface.co/dots-studio/dots3-note-prev) | 作者: dots-studio | 👍 186 | ⬇️ 393
DOTS3 系列预览笔记模型（多模态输入文本），面向长上下文与文本生成。


### 🎨 多模态与生成（图像 / 视频 / 音频）

**1. Qwen/Qwen3.8-27B**
[链接](https://huggingface.co/Qwen/Qwen3.8-27B) | 作者: Qwen | 👍 10,276 | ⬇️ 267,725
Qwen3.8 旗舰端到端多模态（图片+文本→文本），社区热度最高。

**2. mooonshotai/Kimi-K3** *(注：榜单中为 moonshotai)*
[链接](https://huggingface.co/moonshotai/Kimi-K3) | 作者: moonshotai | 👍 10,767 | ⬇️ 2,136,775
支持图像+文本输入，主打**压缩张量**技术（compressed-tensors）与特征提取，K3 是本周点赞榜首。

**3. meta-models/Muse-Glimmer-30B**
[链接](https://huggingface.co/meta-models/Muse-Glimmer-30B) | 作者: meta-models | 👍 1,629 | ⬇️ 292,973
Meta 推出的 30B 图像+文本多模态对话模型，泛化能力强。

**4. MiniMaxAI/MiniMax-H3**
[链接](https://huggingface.co/MiniMaxAI/MiniMax-H3) | 作者: MiniMaxAI | 👍 4,028 | ⬇️ 2,307,541
官方 H3 视频生成模型（图/文→视频），下载超 230 万，本周视频赛道绝对焦点。

**5. MiniMaxAI/MiniMax-Music3**
[链接](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | 作者: MiniMaxAI | 👍 840 | ⬇️ 8,639
文本→音乐/音频生成模型，开启 AI 作曲新范式。

**6. Lightricks/LTX-2.5**
[链接](https://huggingface.co/Lightricks/LTX-2.5) | 作者: Lightricks | 👍 1,027 | ⬇️ 424,099
影级视频生成模型（图/文→视频），支持视频到视频的二次创作。

**7. lightx2v/Minimax-h3-Turbo**
[链接](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | 作者: lightx2v | 👍 557 | ⬇️ 239,206
MiniMax H3 的 Turbo 加速版（图→视频），主打低延迟生成。

**8. Comfy-Org/MiniMax-H3**
[链接](https://huggingface.co/Comfy-Org/MiniMax-H3) | 作者: Comfy-Org | 👍 1,385 | ⬇️ 13,406,892
ComfyUI 官方适配版 H3（单文件格式），下载量达 **1,340 万**，社区生态霸主。

**9. fal/MiniMax-H3-Realism-People-LoRA**
[链接](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | 作者: fal | 👍 229 | ⬇️ 16,103
专为人像写实优化的 H3 LoRA，提升视频人物真实感。

**10. Gazingstars123/Anima-2.9B**
[链接](https://huggingface.co/Gazingstars123/Anima-2.9B) | 作者: Gazingstars123 | 👍 222 | ⬇️ 20,860
动漫风格文本→图像模型，ComfyUI 友好单文件。

**11. larryvrh/MiniMax-H3-Turbo-Lora**
[链接](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | 作者: larryvrh | 👍 776 | ⬇️ 0
H3 Turbo 的 LoRA，支持文生视频+音频同步生成（T2V+T2A）。

**12. unsloth/MiniMax-H3-GGUF**
[链接](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | 作者: unsloth | 👍 175 | ⬇️ 204,344
GGUF 格式 H3 视频模型，适配 stable-diffusion.cpp 的轻量部署。


### 🔧 专用模型（嵌入 / 压缩 / 工具类）

**1. inclusionAI/Ling-3.0-tiny**
[链接](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | 作者: inclusionAI | 👍 285 | ⬇️ 5,727
百灵混合架构（bailing_hybrid）端侧小模型，注重设备端高效推理。

**2. Comfy-Org/MiniMax-Music-3**
[链接](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | 作者: Comfy-Org | 👍 151 | ⬇️ 0
ComfyUI 版音乐生成节点包，Apache-2.0 开源授权。


### 📦 微调与量化（GGUF / FP8 / LoRA）

**1. unsloth/Qwen3.8-27B-GGUF**
[链接](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | 作者: unsloth | 👍 1,455 | ⬇️ 1,945,635
Qwen3.8-27B 的 GGUF 全系列量化，下载近 **200 万**，本地部署事实标准。

**2. Qwen/Qwen3.8-27B-FP8**
[链接](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | 作者: Qwen | 👍 484 | ⬇️ 352,971
官方 FP8 量化版，精度损失极小同时大幅降低显存需求。

**3. unsloth/Muse-Glimmer-30B-GGUF**
[链接](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | 作者: unsloth | 👍 457 | ⬇️ 718,178
Muse-Glimmer 的 GGUF 量化版，助力社区低成本微调与部署。

**4. meta-models/Muse-Glimmer-30B-GGUF**
[链接](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | 作者: meta-models | 👍 298 | ⬇️ 357,877
Meta 官方 GGUF 量化版（含 Arxiv 论文引用）。

**5. orcarouter/Qwen3.8-27B-Uncensored-FP8**
[链接](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | 作者: orcarouter | 👍 344 | ⬇️ 4,285
Qwen3.8 的“去审查”FP8 微调版（abliterated），主打开放式问答。

**6. DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**
[链接](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | 作者: DavidAU | 👍 2,095 | ⬇️ 3,020,070
社区“缝合怪”型超长命名 GGUF 微调（Qwen3.6 基座），下载 300 万+，主打极致自由度。

**7. JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**
[链接](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | 作者: JonathanColetti | 👍 210 | ⬇️ 183,988
Qwen3.8 去审查 + 多 token 预测（MTP）增强版 GGUF。

**8. unsloth/Qwen3.8-27B-NVFP4**
[链接](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | 作者: unsloth | 👍 202 | ⬇️ 276,269
NVIDIA 新一代 NVFP4 量化格式版，专为 Blackwell 架构优化。

**9. Qwen/Qwen3.8-2.4T-A95B-FP8**
[链接](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | 作者: Qwen | 👍 209 | ⬇️ 11,311
2.4T MoE 的 FP8 量化版，让巨型模型部署门槛大幅下降。


## 📊 生态信号

- **Qwen 生态全面统治**：从官方旗舰（27B、2.4T MoE）、FP8 官方量化、Unsloth GGUF 到社区去审查微调，Qwen 已形成完整的“模型 - 量化 - 微调”矩阵。
- **MoE 与混合架构成为主流**：DeepSeek-V4、Nemotron-3.5-Lightning（A3B）、Qwen 2.4T-A95B 均采用 MoE 稀疏激活；inclusionAI 的“bailing_hybrid”与 Kimi-K3 的压缩张量暗示**端侧与高密度优化**是下一战场。
- **视频生成竞赛白热化**：MiniMax-H3 凭借 Comfy-UI 生态（1,340 万下载）成为 Runway / Kling 之外最火开源方案，配套 LoRA 与 Turbo 版本不断涌现。
- **量化技术分化加速**：GGUF（llama.cpp）与 FP8（vLLM/TGI）已成双轨标配，NVFP4 作为英伟达新标准正在崛起；“去审查”类微调（Uncensored/Abliterated）仍是社区高下载量热点。
- **开源权重 → 全链路产品化**：头部玩家（Qwen、DeepSeek、MiniMax）在开源社区直接发布量化版、API 版（FP8/Flash），体现了“开源引流 + 云服务变现”的商业路径。

## 🔬 值得探索

1. **moonshotai/Kimi-K3** — 点赞榜第一的“黑马”，其 compressed-tensors + 特征提取设计代表多模态融合新方向，值得深入测试其压缩率与精度平衡。
2. **Qwen/Qwen3.8-2.4T-A95B-FP8** — 也许是目前开源社区能到手最强 MoE 的 FP8 版，适合研究超大稀疏模型的单机推理极限（如 4×A100 80G）。
3. **Lightricks/LTX-2.5** — 与 MiniMax-H3 完全不同的视频生成技术路线（尤其 video-to-video 能力），对比实验价值高。
4. **LiquidAI/LFM2.5-2.6B** — 仅 2.6B 却拿到 647 赞，液态网络（Liquid）在效率上的突破值得小模型爱好者深挖。

---
*报告时间：2026-08-17 | 数据来源：Hugging Face Hub Trending*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*