# Hugging Face 热门模型日报 2026-07-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-09 01:29 UTC

---

好的，作为 AI 模型生态分析师，以下是基于 2026-07-09 数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-09**

#### **今日速览**

今日 Hugging Face 趋势榜呈现“双雄并起”格局：**Qwen 3.6/3.5** 家族与 **DeepSeek V4** 系列成为生态核心，大量社区微调与量化版本涌现。视觉定位模型 **Nvidia LocateAnything-3B** 和 **百度 Unlimited-OCR** 证明了多模态任务的高热度。值得注意的是，**Gemma 4** 在代码与Agent领域的微调版本（如 Fable 系列）获得了极高点赞，显示了开发者对 Google 模型生态的认可。量化格式方面，GGUF 依然是最主流的部署格式，社区贡献活跃。

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** · zai-org | 👍 3,666 | ⬇️ 281,584
  - 基于 MoE 架构的对话模型，以其卓越的推理能力和社区影响力成为本周点赞数最高的模型。
- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** · deepseek-ai | 👍 439 | ⬇️ 15,538
  - 深度求索最新旗舰模型，标志着其在开源大模型领域的又一次重要迭代，配有科研论文。
- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** · tencent | 👍 563 | ⬇️ 121
  - 腾讯推出的新一代混元大模型，代表了国内头部厂商在生成式AI上的新进展。
- **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)** · AliesTaha | 👍 187 | ⬇️ 3,886
  - 基于 Qwen3 的指令微调模型，专注于提升长文本连贯性与叙事能力。
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** · froggeric | 👍 781 | ⬇️ 0
  - 为解决 Qwen 系列聊天模板兼容性问题而生，是一个高实用性的社区修复项目。
- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** · meituan-longcat | 👍 151 | ⬇️ 385
  - 美团推出的下一代长文本对话模型，专注于处理超长上下文场景。
- **[poolside/Laguna-XS-2.1](https://huggingface.co/poolside/Laguna-XS-2.1)** · poolside | 👍 76 | ⬇️ 3,385
  - 面向特定场景（推测为软件工程）的轻量级模型，强调效率与专业性。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** · nvidia | 👍 2,667 | ⬇️ 1,424,958
  - NVIDIA 发布的开源视觉定位基础模型，能根据文本指令在图像中定位任意目标，应用潜力巨大。
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** · baidu | 👍 1,873 | ⬇️ 1,084,945
  - 百度推出的全能型 OCR 模型，在文字识别领域展现了强大的通用性和高下载量。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** · empero-ai | 👍 1,855 | ⬇️ 1,683,711
  - 基于 Qwen3.5 并融合了高质量合成数据的图文模型量化版，下载量惊人，社区需求旺盛。
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** · krea | 👍 555 | ⬇️ 123,729
  - Krea 推出的新一代文生图模型 Turbo 版本，在生成速度和画质上达成新的平衡。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** · HauhauCS | 👍 2,573 | ⬇️ 2,823,988
  - 社区基于 Qwen3.6 制作的无审查、强风格化 MoE 模型，因其“激进”特性获得极高关注。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** · yuxinlu1 | 👍 2,652 | ⬇️ 674,977
  - 基于 Google Gemma 4 深度微调的代码模型，结合“作曲”Agent 技术，在生成代码质量和逻辑推理上表现优异。
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** · yuxinlu1 | 👍 1,098 | ⬇️ 384,383
  - 同一作者的另一款 Gemma 4 微调版，强化了 Agent 能力，适用于终端和自动化任务。
- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** · google | 👍 313 | ⬇️ 9,458
  - Google 发布的表格数据基础模型，支持零样本分类与回归，在结构化数据领域具有突破性意义。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** · deepreinforce-ai | 👍 800 | ⬇️ 502,663
  - 35B 大模型的 GGUF 量化版，社区对 “Ornith” 系列模型部署需求强劲。
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** · unsloth | 👍 1,010 | ⬇️ 2,842,118
  - 由知名高效微调/推理库 Unsloth 制作的 Qwen3.6 GGUF 量化版，是下载量最高的模型之一，显示了其工具链的强大影响力。
- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** · nvidia | 👍 325 | ⬇️ 538,687
  - NVIDIA 官方推出的 Qwen3.6 FP4 量化版本，代表了工业界在模型优化上的前沿探索。
- **[InternScience/Agents-A1-Q4_K_M-GGUF](https://huggingface.co/InternScience/Agents-A1-Q4_K_M-GGUF)** · InternScience | 👍 84 | ⬇️ 11,226
  - 基于 MoE 视觉语言模型的量化版本，展示了多模态 Agent 模型向轻量化部署发展的趋势。

#### **生态信号**

当前生态呈现三大信号：**第一，Qwen 与 DeepSeek 的“两超多强”格局**。Qwen 3.5/3.6 凭借丰富的社区微调（Ornith, Fable, Uncensored）和官方/第三方量化（NVIDIA, Unsloth）占据了绝对热度；DeepSeek V4 则代表了前沿学术和工业级模型的探索。**第二，开源模型的“武器竞赛”升级**。Google（Gemma 4）、NVIDIA（各种微调/量化）以及国内大厂（腾讯、百度、美团）纷纷投入，开源模型的通用能力和专业性差距在缩小。**第三，量化是通往大规模应用的“最后一公里”**。GGUF 格式作为本地化部署的首选继续统治列表，但 NVFP4 等更高级的量化方案正从 NVIDIA 等基础设施提供商处崛起，暗示着未来推理效率的竞争会从模型层延伸到硬件和优化库层。

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    *   **理由**：这是一个极具潜力的视觉基础模型，它解决了“指哪打哪”的视觉定位问题，且模型大小仅 3B，非常高效。无论是用于机器人、自动驾驶还是图像编辑，其应用场景都非常广阔，值得深入研究其 zero-shot 能力。

2.  **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
    *   **理由**：该模型代表了“基础模型 + 专用 Agent 微调”的成功范式。它在 Gemma 4 上叠加了代码和 Agent 能力，并通过 GGUF 量化使其易于部署。这对于想要构建私有或本地化代码助手的研究人员和开发者是极佳的开箱即用选择。

3.  **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**
    *   **理由**：作为顶级开源实验室的最新作品，DeepSeek V4 系列通常代表了当时开源 LLM 的顶尖水平。跟踪和测试该模型，是紧跟大模型技术最前沿、了解下一代架构和训练方法（如 DSpark）的最佳方式。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*