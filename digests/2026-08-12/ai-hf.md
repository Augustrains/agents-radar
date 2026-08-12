# Hugging Face 热门模型日报 2026-08-12

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-12 00:52 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026年8月12日

## 📌 今日速览

本周Hugging Face趋势榜呈现**视频生成与多模态模型爆发**的鲜明特征：MiniMax-H3系列以绝对优势霸榜，覆盖官方发布、ComfyUI集成、LoRA微调与社区衍生版本，合计贡献超10个上榜条目。另一方面，**Kimi-K3以10,525周点赞登顶**，成为本周最受关注的多模态模型。值得注意的还有Meta的Muse-Glimmer-30B（多模态对话）、DeepSeek-V4-Flash（文本生成）与百度Unlimited-OCR（文档理解）三足鼎立，共同构成本周生态的多元格局。此外，各生态位的GGUF量化版几乎同步上线（unsloth、LiquidAI、meta-models），显示出社区对本地部署与轻量化推理的强烈需求。

🔗 [查看完整榜单](https://huggingface.co/models?sort=trending)

---

## 🧠 语言模型（LLM / 对话 / 指令微调）

### 1. deepseek-ai/DeepSeek-V4-Flash-0731
- **作者**: deepseek-ai | ✅ 3,150 | 📥 1,048,685
- **说明**: DeepSeek新一代Flash系列模型，主打高效推理与对话能力，下载量突破百万，是本周文本生成赛道最强者。

### 2. LiquidAI/LFM2.5-2.6B
- **作者**: LiquidAI | ✅ 550 | 📥 93,668
- **说明**: LiquidAI基于液体计算架构的最新小型语言模型，2.6B参数主打高效能与可扩展性。

### 3. inclusionAI/Ling-3.0-flash
- **作者**: inclusionAI | ✅ 303 | 📥 6,148
- **说明**: 国内团队inclusionAI的Flash版轻量语言模型，采用bailing_hybrid混合架构，支持对话场景。

### 4. inclusionAI/Ling-3.0-tiny
- **作者**: inclusionAI | ✅ 152 | 📥 0
- **说明**: Ling-3.0系列极小版本，MIT协议开源，面向资源受限环境的轻量部署。

### 5. nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4
- **作者**: nvidia | ✅ 124 | 📥 19,250
- **说明**: NVIDIA旗舰级MoE模型（30B总量/3B激活），采用NVFP4量化，兼顾性能与推理效率。

### 6. endless-frontier/BigBang-v1
- **作者**: endless-frontier | ✅ 166 | 📥 708
- **说明**: 基于Qwen3.5-MoE架构的多模态对话模型，主打通用对话理解能力。

---

## 🎨 多模态与生成（图像/视频/音频/文本到X）

### 1. moonshotai/Kimi-K3
- **作者**: moonshotai | ✅ 10,525 | 📥 1,565,484
- **说明**: 月之暗面最新多模态模型，支持图像+文本联合输入，采用压缩张量技术优化推理，本周点赞最高。

### 2. MiniMaxAI/MiniMax-H3
- **作者**: MiniMaxAI | ✅ 3,572 | 📥 59,368
- **说明**: MiniMax最新文生视频/图生视频旗舰模型，支持image-text-to-video多模态生成，本周现象级热门。 [🔥模型页](https://huggingface.co/MiniMaxAI/MiniMax-H3)

### 3. baidu/Unlimited-OCR
- **作者**: baidu | ✅ 4,018 | 📥 2,892,191
- **说明**: 百度发布的OCR大模型，主打任意场景文字识别与文档理解，下载量逼近300万。

### 4. meta-models/Muse-Glimmer-30B
- **作者**: meta-models | ✅ 1,092 | 📥 0
- **说明**: Meta最新多模态对话模型（30B），聚焦图文联合理解与生成式对话，刚发布即登上趋势榜。

### 5. Comfy-Org/MiniMax-H3
- **作者**: Comfy-Org | ✅ 1,212 | 📥 6,798,796
- **说明**: ComfyUI官方的MiniMax-H3单文件封装，下载量近680万，是视频生成工作流的核心组件。

### 6. Lightricks/LTX-2.5
- **作者**: Lightricks | ✅ 209 | 📥 39
- **说明**: Lightricks的旗舰视频生成模型，支持文生视频/图生视频/视频转视频全链路。

### 7. lightx2v/Minimax-h3-Turbo
- **作者**: lightx2v | ✅ 340 | 📥 20,376
- **说明**: MiniMax-H3的Turbo加速版，主打更快的视频生成速度。

### 8. nvidia/NVIDIA-NemotronLabs-VoiceChat-11B
- **作者**: nvidia | ✅ 325 | 📥 653
- **说明**: NVIDIA语音对话模型（11B），面向实时语音交互场景，集成多篇最新论文技术。

### 9. larryvrh/MiniMax-H3-Turbo-Lora
- **作者**: larryvrh | ✅ 650 | 📥 0
- **说明**: 社区为MiniMax-H3-Turbo制作的LoRA适配器，用于风格迁移与视频定制。

### 10. lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA
- **作者**: lightx2v | ✅ 129 | 📥 353
- **说明**: 用于MiniMax-H3的Prompt重写LoRA，优化视频生成时的提示词质量。

### 11. fal/MiniMax-H3-Realism-People-LoRA
- **作者**: fal | ✅ 111 | 📥 0
- **说明**: FAL推出的写实人物风格LoRA，针对MiniMax-H3视频生成中人物真实感优化。

### 12. SexGod1979/PinkCherry_MiniMax-H3
- **作者**: SexGod1979 | ✅ 264 | 📥 0
- **说明**: 社区基于MiniMax-H3的定制版文生视频模型（Apache-2.0协议），主打特定风格。

### 13. drbaph/MiniMax-H3-Turbo-Lora-ComfyUI
- **作者**: drbaph | ✅ 272 | 📥 0
- **说明**: 适配ComfyUI的MiniMax-H3-Turbo LoRA适配器，剪枝版便于直接部署。

### 14. ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot
- **作者**: ethanfel | ✅ 457 | 📥 0
- **说明**: 社区综合模型：Qwen3-VL-32B视觉编码器+MiniMax-H3文本编码器，集成ComfyUI。

### 15. sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4
- **作者**: sakamakismile | ✅ 160 | 📥 0
- **说明**: 类似综合模型，以NVFP4格式优化Qwen3-VL编码器与MiniMax-H3组合方案。

### 16. Kijai/MiniMax-H3_comfy
- **作者**: Kijai | ✅ 275 | 📥 0
- **说明**: Kijai出品的MiniMax-H3 ComfyUI适配节点，社区常用视频生成工作流组件。

### 17. Kijai/MiniMax-H3-experimental
- **作者**: Kijai | ✅ 191 | 📥 0
- **说明**: Kijai的MiniMax-H3实验性版本，探索新功能与性能优化。

---

## 🔧 专用模型（代码/数学/医疗/嵌入等）

### 1. mistralai/Shieldstral-1.0-3B
- **作者**: mistralai | ✅ 228 | 📥 6,769
- **说明**: Mistral推出的安全对齐模型（3B），用于内容审核与安全过滤，定位明确，实用性强。

---

## 📦 微调与量化（社区微调/GGUF/AWQ）

### 1. DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF
- **作者**: DavidAU | ✅ 1,896 | 📥 2,521,093
- **说明**: 社区热门微调模型（GGUF格式），基于Qwen3.6-27B深度定制，下载量超250万。

### 2. unsloth/DeepSeek-V4-Flash-0731-GGUF
- **作者**: unsloth | ✅ 649 | 📥 207,990
- **说明**: unsloth官方GGUF量化版DeepSeek-V4-Flash，便于llama.cpp等本地部署。

### 3. unsloth/Muse-Glimmer-30B-GGUF
- **作者**: unsloth | ✅ 304 | 📥 0
- **说明**: Meta Muse-Glimmer-30B的GGUF量化版，进一步降低多模态模型部署门槛。

### 4. meta-models/Muse-Glimmer-30B-GGUF
- **作者**: meta-models | ✅ 202 | 📥 0
- **说明**: Meta官方推出的GGUF量化版本，配合论文与开源生态推广。

### 5. LiquidAI/LFM2.5-2.6B-GGUF
- **作者**: LiquidAI | ✅ 201 | 📥 111,942
- **说明**: LFM2.5-2.6B的官方GGUF量化版本，适配llama.cpp实现端侧部署。

---

## 🌐 生态信号

**1. MiniMax-H3系列一骑绝尘**
MiniMax-H3在本周形成完整生态闭环：官方基础模型（MiniMaxAI）+ 社区集成（Comfy-Org/Kijai）+ 功能扩展（LoRA系列：风格、写实、Prompt重写）+ 量化衍生（Turbo/实验版），共计13个相关条目上榜。这种**核心模型 + 生态周边**的扩散模式，标志着视频生成从"模型竞技"进入"生态竞争"阶段。

**2. 开源权重全面领先，闭源仅靠API撑场**
本周30个上榜模型中，**27个为开源权重**（占比90%）。Moonshot Kimi-K3（10,525赞）、MiniMax-H3、DeepSeek-V4-Flash均为开源可下载。闭源模型（如GPT-5.2、Claude-4.5）未出现在榜单中，开源与闭源在社区影响力上的差距进一步扩大。

**3. 量化与多模态加速融合**
GGUF/NVFP4等量化技术从纯文本模型向多模态模型渗透：Muse-Glimmer-30B-GGUF（multimodal+quantization）、DeepSeek-V4-Flash-GGUF、Nemotron NVFP4、Qwen3-VL NVFP4等条目密集出现。**量化正成为多模态模型走向实际部署的标配环节**，unsloth与LiquidAI等团队在此赛道的布局值得关注。

**4. 多模态对话成新战场**
Kimi-K3（多模态对话+压缩张量）、Muse-Glimmer-30B（多模态对话）、BigBang-v1（Qwen3.5-MoE多模态）等模型不约而同选择了多模态对话方向，信号明确：**单一文本能力的边际效益递减，多模态理解与生成能力成为下一代模型分水岭**。

---

## 🧪 值得探索

### 1. [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) ⭐ 本周周点赞之王
10,525赞一骑绝尘，采用压缩张量技术（compressed-tensors）降低推理成本，为多模态大模型的轻量化部署提供了全新范式。对于关注多模态推理效率的研究者与工程团队，Kimi-K3值得优先深入研究。

### 2. [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) ⭐ 生态爆发范本
作为本周现象级模型，MiniMax-H3不仅自身表现强势，更催生了LoRA微调、ComfyUI集成、量化加速等一整条生态链。观察其生态图谱的演化路径，对于理解"模型即产品"的开源生态传播逻辑具有极高的参考价值。

### 3. [nvidia/NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) ⭐ 语音赛道黑马
NVIDIA在语音对话领域的重磅产品，集成多篇最新论文技术（arXiv 2410/2503/2604），11B参数量级兼顾性能与部署可行性。在大模型集体卷文本与图像时，NVIDIA选择语音赛道差异化切入，值得关注其后续生态布局。

---

*报告生成时间：2026-08-12 | 数据来源：Hugging Face Trending Models*

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*