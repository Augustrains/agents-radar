# Hugging Face 热门模型日报 2026-08-25

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-25 00:30 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-25

---

## 📰 今日速览

**Qwen3.8-27B 家族全面霸榜**，占据本周 Top 30 近半数席位，原版以 12.5K 周点赞高居榜首，GGUF 量化版下载量已突破 700 万次。**"去审查"（abliterated/uncensored）生态持续爆发**，仅 Top 30 中就有 8 款基于去除安全对齐的衍生模型。**DeepSeek-V4-Flash** 以 3.7K 点赞成为本周最亮眼的新面孔，标志着 MoE 架构高性能推理进入新阶段。**MiniMax-H3 视频生成模型**以 4.4M 下载量证明视频生成领域竞争白热化。整体来看，**多模态、量化部署与"无限制"模型**正成为社区三大核心驱动力。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **[DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731)** — deepseek-ai | ⭐ 3,681 | ⬇️ 3.27M  
   DeepSeek 最新旗舰 Flash 版本，专注高效推理的对话模型，轻量化部署表现亮眼。

2. **[Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B)** — ornith-ai | ⭐ 396 | ⬇️ 60K  
   Qwen3.5 架构的 MoE 模型，35B 总参仅 3B 激活，兼顾多模态能力与推理效率。

3. **[s1-mini](https://huggingface.co/superwhisper/s1-mini)** — superwhisper | ⭐ 229 | ⬇️ 2.9K  
   基于 Qwen3 的轻量级文本生成模型，集成 ASR 能力，面向语音/文本双模态场景。

4. **[Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2)** — z-lab | ⭐ 214 | ⬇️ 50K  
   引入 DFlash2 投机解码技术，在保持生成质量的同时大幅提升推理吞吐。

5. **[Qwen3.8-27B-DFlash2](https://huggingface.co/incoai/Qwen3.8-27B-DFlash2)** — incoai | ⭐ 173 | ⬇️ 85K  
   与 z-lab 同名的竞品实现，同样主打投机解码加速，社区对推理性价比关注度极高。

6. **[Ornith-1.5-9B](https://huggingface.co/ornith-ai/Ornith-1.5-9B)** — ornith-ai | ⭐ 202 | ⬇️ 83K  
   Ornith 系列小尺寸版本，9B 参数即支持图像+文本理解，面向边缘部署场景。

7. **[Ornith-1.5-9B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-9B-GGUF)** — ornith-ai | ⭐ 186 | ⬇️ 971K  
   上述模型的 GGUF 量化版，MIT 协议，兼容 llama.cpp 等本地推理框架。

8. **[Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF)** — ornith-ai | ⭐ 274 | ⬇️ 988K  
   35B MoE 的量化版即将冲刺百万下载，是本地部署高效大模型的热门选择。

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — Qwen | ⭐ 12,512 | ⬇️ 2.65M  
   Qwen 家族最新多模态旗舰，同时处理图像与文本，本周最大热门。

2. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — MiniMaxAI | ⭐ 4,417 | ⬇️ 4.47M  
   MiniMax 第三代视频生成模型，支持文生视频/图生视频双模式，下载量全网第一。

3. **[LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5)** — Lightricks | ⭐ 1,723 | ⬇️ 790K  
   Lightricks 新一代视频生成模型，支持图像/文本/视频到视频，Diffusers 单文件即插即用。

4. **[MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3)** — MiniMaxAI | ⭐ 1,228 | ⬇️ 18K  
   MiniMax 推出的第三代文本生成音乐模型，开辟 AI 音乐创作新赛道。

5. **[Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8)** — Qwen | ⭐ 681 | ⬇️ 3.0M  
   官方 FP8 量化版，内存占用大幅降低同时保持多模态能力，部署首选。

6. **[Audio8-TTS-Preview-0.1b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.1b)** — Audio8 | ⭐ 145 | ⬇️ 2.7K  
   基于 ARKTTS 架构的轻量级语音合成模型，支持特征提取与音频生成。

---

### 🔧 专用模型（代码、数学、医疗、嵌入）

*本周 Top 30 暂无纯代码/数学/医疗/嵌入类模型上榜。*  
*但值得注意的是：froggeric 与 peculiar-ragdoll 两个 Chat Template 修复模型展示了社区对**提示模板工程**的关注度正在上升。*

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **[Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — unsloth | ⭐ 2,835 | ⬇️ 7.01M  
   unsloth 出品的高质量 GGUF 量化版，下载量全网第一，社区量化标杆。

2. **[Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8)** — orcarouter | ⭐ 1,097 | ⬇️ 224K  
   abl iterated 去除审查 + FP8 量化，兼顾"无限制"与部署效率。

3. **[Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX)** — orcarouter | ⭐ 1,026 | ⬇️ 57K  
   Apple Silicon 专属 MLX 格式，面向 Mac 生态的去审查多模态模型。

4. **[Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED)** — OBLITERATUS | ⭐ 695 | ⬇️ 312K  
   "抹除"对齐层的激进去审查版本，同时提供 GGUF/MLX 多格式支持。

5. **[Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF)** — JonathanColetti | ⭐ 689 | ⬇️ 1.46M  
   支持 MTP 的 GGUF 去审查版，兼容 llama.cpp，下载量超百万。

6. **[Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF)** — orcarouter | ⭐ 423 | ⬇️ 143K  
   orcarouter 家的 GGUF 版本，与 FP8/MLX 版本构成完整量化矩阵。

7. **[Qwen3.8-27B-Uncensored-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF)** — HauhauCS | ⭐ 578 | ⬇️ 761K  
   激进版多 token 预测去审查模型，在生成速度与自由程度间追求极致。

8. **[Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF)** — huihui-ai | ⭐ 334 | ⬇️ 1.14M  
   huihui-ai 经典 abliterated 系列，GGUF 格式，百万级下载验证社区口碑。

9. **[Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF)** — empero-ai | ⭐ 260 | ⬇️ 162K  
   经 llama.cpp 深度优化的量化版本，主打本地运行稳定性。

10. **[Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF)** — 0bserverx | ⭐ 259 | ⬇️ 654K  
   以 "Heretic"（异端）为名的激进去审查版本，强调最大限度解锁模型潜力。

11. **[Qwen3.8-27B-Cold-Fusion-GAIN-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | ⭐ 226 | ⬇️ 209K  
   融合 GAIN 训练与冷融合技术的社区魔改版，代表量化+微调的最高复杂度。

12. **[Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated)** — huihui-ai | ⭐ 277 | ⬇️ 27K  
   非量化版本，适合需要完整精度进行二次微调的用户。

13. **[Qwen3.8-27B-Uncensored](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored)** — orcarouter | ⭐ 170 | ⬇️ 10K  
   orcarouter 去审查系列的原版底座，其他格式版本的源头。

---

## 🔍 生态信号

**趋势一：Qwen3.8 形成完整衍生生态。** 从官方多模态底座到 GGUF/MLX/FP8 量化、从 abliterated 去审查到 DFlash2 投机解码加速，一个模型家族能在两周内衍生出 15+ 变体并覆盖全平台，这在开源历史上极为罕见。**趋势二："去审查"成为量化之外的又一大社区运动。** 8 款 uncensored/abliterated 模型同时上榜，说明用户对模型"自由度"的需求已从少数极客扩展为主流诉求。**趋势三：视频生成进入混战阶段。** MiniMax-H3 与 LTX-2.5 双双登上榜单，配合 MiniMax-Music3 进军音频，多模态内容生成正向"全模态"演进。**趋势四：投机解码（DFlash2/MTP）成为推理优化的新热点。** 多个变体围绕相同技术出现竞争，预示推理加速将是下一阶段社区竞争焦点。

*开源权重模型已完全主导 HF 热门榜（30/30），闭源模型在开源社区的声量持续萎缩。*

---

## 💎 值得探索

1. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — 本周生态的绝对中心。适合作为基座模型进行各种方向的研究，无论是多模态对齐、去审查实验还是量化调优，围绕它已形成完整的工具链和社区经验。

2. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 4.4M 下载量的视频生成标杆。建议结合 [#26 LBH-123-AI 的 Latent Upscaler](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) 配合使用，探索视频超分的前沿工作流。

3. **[unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)** — 7M 下载量足以证明其量化质量经受住了社区检验。如果你只有消费级 GPU，这是体验 Qwen3.8 多模态能力最稳妥的选择；同时也值得学习 unsloth 的量化方法论。

---

*日报生成时间：2026-08-25 | 数据来源：Hugging Face Hub Trending*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*