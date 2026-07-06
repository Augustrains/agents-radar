# Hugging Face 热门模型日报 2026-07-06

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-06 01:53 UTC

---

好的，以下是为您生成的《Hugging Face 热门模型日报》，日期为2026年7月6日。

---

## Hugging Face 热门模型日报 | 2026-07-06

### 今日速览

本周 Hugging Face 生态呈现出“巨头与社区齐飞”的态势。一方面，**DeepSeek-V4** 系列正式开源，引爆了新一轮的推理与稀疏注意力模型热潮；另一方面，**社区微调与量化**活动空前活跃，围绕 Qwen3.5/3.6、Gemma 4 和 GLM-5.2 涌现了大量高性能的 GGUF 及“去审查”版本，下载量惊人。此外，**NVIDIA** 在视觉定位（LocateAnything）和模型优化（NVFP4）上持续发力，**百度的 Unlimited-OCR** 则凭借强大的实用性获得了海量下载。多模态（尤其是图像到文本）与文本生成依然是当下最热门的两大任务类型。

---

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

1.  **zai-org/GLM-5.2** | 作者: zai-org | 👍 3,470 | ⬇️ 220,379
    - 本周点赞数最高的模型，智谱最新一代 MoE 大模型的开源版本，凭借卓越的对话与推理能力占据榜首。
2.  **deepseek-ai/DeepSeek-V4-Pro-DSpark** | 作者: deepseek-ai | 👍 390 | ⬇️ 12,580
    - DeepSeek V4 系列高级版，引入了 DSpark 激励机制，旨在提升模型在复杂推理任务中的表现。
3.  **deepseek-ai/DeepSeek-V4-Flash-DSpark** | 作者: deepseek-ai | 👍 161 | ⬇️ 48,696
    - DeepSeek V4 的快速蒸馏版，在保持性能的同时大幅提升了推理速度，适合大规模部署。
4.  **mistralai/Leanstral-1.5-119B-A6B** | 作者: mistralai | 👍 117 | ⬇️ 26
    - 由 Mistral AI 推出的 119B 参数（激活 6B）的 MoE 模型，是前沿大模型的重要尝试，因体积巨大尚处于早期探索阶段。
5.  **InternScience/Agents-A1** | 作者: InternScience | 👍 290 | ⬇️ 7,010
    - 基于 Qwen3.5 MoE 的智能体模型，专为工具调用和复杂任务编排设计，是 Agent 方向的新星。
6.  **nvidia/Qwen3.6-27B-NVFP4** | 作者: nvidia | 👍 274 | ⬇️ 297,130
    - NVIDIA 使用其 Model Optimizer 工具量化的 Qwen 3.6 模型，采用 4-bit FP4 精度，实现了极致的性能与效率平衡。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

1.  **baidu/Unlimited-OCR** | 作者: baidu | 👍 1,750 | ⬇️ 1,044,217
    - 百度的全能型 OCR 模型，支持无限制的文字识别场景，下载量突破百万，实用性极强。
2.  **nvidia/LocateAnything-3B** | 作者: nvidia | 👍 2,618 | ⬇️ 1,247,265
    - NVIDIA 推出的“指哪打哪”定位模型，支持基于文本或图像提示在任意图中定位物体，引爆了视觉交互新范式。
3.  **krea/Krea-2-Turbo** | 作者: krea | 👍 515 | ⬇️ 99,049
    - 第二代入流的文生图模型 Turbo 版本，在保持高画质的同时显著提升了生成速度。
4.  **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** | 作者: HauhauCS | 👍 2,487 | ⬇️ 3,018,257
    - 社区最热门的 Qwen3.6 去审查 MoE 模型，下载量超 300 万，体现用户对“无限制”对话的强烈需求。
5.  **DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED** | 作者: DavidAU | 👍 153 | ⬇️ 53,962
    - 融合了 Claude 风格思考链的 Qwen3.5 去审查微调版，名字极长，代表了社区对“高智商+自由”模型的极致追求。
6.  **unsloth/Qwen3.6-27B-MTP-GGUF** | 作者: unsloth | 👍 964 | ⬇️ 2,776,389
    - Unsloth 推出的 Qwen3.6 MoE 模型 GGUF 版本，下载量极高，是本地运行多模态大模型的首选。
7.  **Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF** | 作者: Jackrong | 👍 139 | ⬇️ 84,951
    - 专为代码生成优化的 Qwen3.6 MoE 模型 GGUF 版本，结合了视觉能力，可用于代码截图转换。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

1.  **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** | 作者: yuxinlu1 | 👍 2,610 | ⬇️ 651,758
    - 基于 Gemma 4 微调的专业代码模型 GGUF 版本，结合 Fable 和 Composer 技术，代码能力极强，下载量巨大。
2.  **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** | 作者: yuxinlu1 | 👍 1,029 | ⬇️ 355,871
    - 同样是基于 Gemma 4 的 Agent 专用模型，强化了终端和代理能力，是自动化编程的重要工具。
3.  **BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6** | 作者: BugTraceAI | 👍 135 | ⬇️ 12,196
    - 专注于网络安全的专用模型，旨在进行漏洞挖掘和攻击模拟，代表了 AI 在垂直安全领域的深度应用。
4.  **nationaldesignstudio/rampart** | 作者: nationaldesignstudio | 👍 129 | ⬇️ 2,783
    - 专为 PII（个人身份信息）检测与脱敏设计的 BERT 模型，并通过 ONNX 格式优化，适合前端运行。
5.  **google/tabfm-1.0.0-pytorch** | 作者: google | 👍 226 | ⬇️ 2,670
    - Google 发布的表格数据基础模型，支持零样本分类与回归，是 AI 处理结构化数据的重要进展。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

1.  **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** | 作者: empero-ai | 👍 1,556 | ⬇️ 1,533,844
    - 本周下载量最大的模型之一。将 Claude Mythos 风格的思考模式融入 Qwen3.5，并通过 GGUF 格式实现高效本地推理。
2.  **deepreinforce-ai/Ornith-1.0-35B-GGUF** | 作者: deepreinforce-ai | 👍 731 | ⬇️ 394,164
    - Ornith 系列大模型的量化版本，在保持 MIT 许可的同时，提供了高效的本地部署方案。
3.  **huihui-ai/Huihui-GLM-5.2-abliterated-GGUF** | 作者: huihui-ai | 👍 169 | ⬇️ 5,609
    - 针对 GLM-5.2 的“去审查” (abliterated) 微调版本，结合了 Unsloth 优化，体现了社区对模型控制权的追求。
4.  **nvidia/GLM-5.2-NVFP4** | 作者: nvidia | 👍 240 | ⬇️ 280,087
    - NVIDIA 对 GLM-5.2 使用 NVFP4 量化技术进行优化，提供了官方认证的高效模型版本。

### 生态信号

- **模型家族势头**：**Qwen 3.x** 系列（特别是 MoE 变体）无疑是本周的绝对主角，其衍生模型占据了榜单近半壁江山，社区微调生态极为繁荣。**GLM-5.2** 和 **Gemma 4** 紧随其后，展现出强劲的追赶势头。
- **开源 vs 闭源**：本周呈现明显的 **开源权重大爆发**。DeepSeek V4 系列虽然迟来，但其开源权重标志着顶级大模型的壁垒在被逐步打破。社区基于 Qwen、Gemma 的微调模型下载量动辄百万，证明开源生态已具备强大的生命力。
- **量化与微调活动**：**GGUF** 格式已完全主导社区量化生态，几乎每个热门原版模型都会迅速出现 GGUF 版本。微调方向则集中在两个极端：一是提升“智商”（代码、推理），二是突破限制（去审查、Uncensored），反映了用户群体的多元化需求。

### 值得探索

1.  **deepseek-ai/DeepSeek-V4-Flash-DSpark** | 链接：https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark
    - **理由**：如果你关注前沿大模型的推理效率革新，这是必试的模型。DSpark 机制有望改变长上下文推理的成本曲线。
2.  **nvidia/LocateAnything-3B** | 链接：https://huggingface.co/nvidia/LocateAnything-3B
    - **理由**：交互范式的革命性模型。对于从事视觉 Agent、RPA 或自动化设计的研究者来说，“指哪打哪”的能力极具想象空间。
3.  **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** | 链接：https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF
    - **理由**：如果你需要代码辅助，这个模型的 GGUF 版本结合了 Gemma 4 强大的基座和社区顶级的微调技巧，是本地部署的代码“核弹”。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*