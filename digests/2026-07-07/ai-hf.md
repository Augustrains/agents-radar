# Hugging Face 热门模型日报 2026-07-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-07 01:50 UTC

---

# Hugging Face 热门模型日报 (2026-07-07)

## 今日速览

本周 Hugging Face 趋势榜呈现三大核心趋势：**Qwen 3.6 系列强势爆发**，多款基于该架构的 MoE 模型（如 Qwopus、Huihui 系列）占据下载量头部，显示社区对稀疏激活大模型的接受度极高；**GGUF 量化生态全面主导**，前 30 名中超 1/3 为 GGUF 格式模型，反映边缘部署与消费级硬件推理需求旺盛；**NVIDIA 与百度等巨头持续输出基础设施模型**，LocateAnything-3B 和 Unlimited-OCR 分别推动定位与 OCR 能力平民化。值得关注的是，**uncensored 和 agentic 标签模型**（如 uncensored Qwen 3.6 系列、gemma-4-agentic）点赞量飙升，暗示社区对“去审查”和“智能体”两类方向有强烈需求。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 作者: zai-org | 点赞: 3,530 | 下载: 231,218  
  智谱最新 MoE 对话模型，以最高点赞数领跑，延续 GLM 家族在中文社区的高认可度。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — 作者: deepseek-ai | 点赞: 409 | 下载: 14,276  
  DeepSeek V4 专业版，支持动态稀疏推理（DSpark），是当前稀疏架构推理效率探索的前沿代表。

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — 作者: tencent | 点赞: 334 | 下载: 2  
  腾讯混元 V3 代模型，虽然下载量极低，但作为大厂最新基础模型值得关注。

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — 作者: meituan-longcat | 点赞: 114 | 下载: 43  
  美团推出长上下文对话模型，专为长文档理解场景设计。

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)** — 作者: nvidia | 点赞: 126 | 下载: 10,766  
  NVIDIA 双塔架构基础模型，30B 参数激活仅 3B，探索推理效率新方向。

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — 作者: froggeric | 点赞: 698 | 下载: 0  
  修复 Qwen 系列对话模板的工具模型，体现社区对模型接口规范化的需求。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 作者: baidu | 点赞: 1,793 | 下载: 1,070,230  
  百度无限 OCR 模型，支持多种场景下的文字识别，下载量超百万，是当前最热门的视觉理解模型之一。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 作者: nvidia | 点赞: 2,635 | 下载: 1,340,559  
  NVIDIA 发布的通用目标定位模型，3B 参数即可在图像中精准定位任意物体，下载量与点赞数双高。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — 作者: krea | 点赞: 529 | 下载: 109,470  
  基于 Flux 架构的图像生成 Turbo 版，商业级质量，适合快速图像合成场景。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — 作者: empero-ai | 点赞: 1,642 | 下载: 1,617,508  
  融合 Claude 风格的 Qwen 3.5 多模态 GGUF 量化版，下载量最高，适合本地多模态推理。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者: HauhauCS | 点赞: 2,529 | 下载: 2,910,241  
  Qwen 3.6 去审查极限版，MoE 架构 35B 总参/3B 激活，社区对“无限制”模型需求强劲。

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — 作者: InternScience | 点赞: 345 | 下载: 8,766  
  Qwen 3.5 MoE 多模态 Agent 模型，专为智能体场景设计。

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — 作者: Qwen | 点赞: 556 | 下载: 57,835  
  官方推出的 Agent 专用 MoE 模型，35B 总参/3B 激活，是 Qwen 家族在 Agent 赛道的重要布局。

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — 作者: google | 点赞: 257 | 下载: 7,036  
  Google 表格基础模型，支持零样本表格分类与回归，有望改变表格数据建模范式。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — 作者: yuxinlu1 | 点赞: 1,050 | 下载: 370,884  
  Gemma 4 的 Agentic 微调量化版，专为终端与代码 Agent 场景优化。

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — 作者: yuxinlu1 | 点赞: 2,623 | 下载: 664,319  
  Gemma 4 代码专用微调版，在代码生成与推理任务上表现突出，点赞数极高。

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** — 作者: nationaldesignstudio | 点赞: 136 | 下载: 3,821  
  PII 检测 BERT 模型，基于 ONNX/Transformers.js 部署，适合隐私合规场景。

- **[eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)** — 作者: eric-venti-seeds | 点赞: 79 | 下载: 0  
  Flux 光照方向控制 LoRA，虽然下载量为 0，但作为专业图像控制工具值得关注。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — 作者: deepreinforce-ai | 点赞: 758 | 下载: 436,780  
  Ornith 35B GGUF 量化版，高质量 MIT 许可模型，适合本地部署。

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — 作者: deepreinforce-ai | 点赞: 442 | 下载: 393,142  
  Ornith 9B 轻量 GGUF 版本，平衡性能与资源消耗。

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — 作者: huihui-ai | 点赞: 176 | 下载: 6,660  
  GLM 5.2 的“abliterated”去审查量化版，结合 unsloth 优化，满足社区对自由对话的需求。

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)** — 作者: Jackrong | 点赞: 151 | 下载: 126,831  
  Qwen 3.6 MoE 代码专用量化版，支持多模态。

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — 作者: unsloth | 点赞: 974 | 下载: 2,818,499  
  基于 unsloth 优化的 Qwen 3.6 27B 多模态量化版，下载量极高，体现 unsloth 工具的广泛采用。

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — 作者: nvidia | 点赞: 290 | 下载: 430,676  
  NVIDIA 官方 Qwen 3.6 量化版，采用 4-bit NVFP4 格式，专为 NVIDIA GPU 优化。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — 作者: empero-ai | 点赞: 700 | 下载: 149,421  
  原始 safetensors 版 Qwythos，对应 GGUF 版的基础模型。

- **[DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED](https://huggingface.co/DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED)** — 作者: DavidAU | 点赞: 158 | 下载: 58,755  
  Qwen 3.5 高智商去审查微调版，强调推理能力与自由表达。

- **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)** — 作者: AliesTaha | 点赞: 177 | 下载: 2,903  
  Qwen 3 指令微调版，适合需要精确指令跟随的场景。

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — 作者: mistralai | 点赞: 143 | 下载: 106  
  Mistral 最新经济学 MoE 模型，119B 总参/6B 激活，展示极致稀疏架构方向。

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — 作者: deepreinforce-ai | 点赞: 350 | 下载: 231,342  
  Ornith 35B 原始 safetensors 版，Qwen 3.5 MoE 架构，多模态支持。

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — 作者: deepreinforce-ai | 点赞: 392 | 下载: 86,136  
  Ornith 9B 原始版，轻量多模态文本生成模型。

## 生态信号

**模型家族格局：** Qwen 3.5/3.6 系列独占鳌头，本周榜上前 10 名中 5 个基于 Qwen 架构，覆盖量化、去审查、Agent 等多元社区调优。NVIDIA 通过 LocateAnything、Nemotron 等自研模型与 Qwen 量化合作（NVFP4），形成“硬件+算法”生态闭环。百度 Unlimited-OCR 显示巨头在垂直视觉任务上仍有统治力。

**开源 vs 闭源趋势：** 本周榜单 100% 为开源权重模型（含量化版），DeepSeek V4、GLM 5.2 等高权重模型均以开放态度发布。Mistral 的 Leanstral 系列虽然下载量低，但进一步验证了 MoE 与稀疏激活已成为主流架构选择。

**量化活动特性：** GGUF 生态在消费级硬件推理领域已占据绝对主导，unsloth 工具链贡献了 Qwen 3.6 系列最高下载的量化版。社区对“uncensored”（去审查）和“abliterated”（去除对齐约束）的量化模型需求旺盛，这反映了用户对开放、无限制对话体验的持续追求。同时，NVIDIA 的 NVFP4 量化格式开始抬头，暗示在专业 GPU 推理场景下可能出现格式分化。

## 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — 只需 3B 参数即可实现通用目标定位，下载量突破百万，是当前少有的轻量级视觉定位模型，适合嵌入移动端或边缘设备。

2. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — Google 发布的表格基础模型，有望成为表格数据领域的“ImageNet 时刻”，零样本分类/回归能力值得深入测试，尤其适合结构化数据分析场景。

3. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 下载量超过 290 万的热门去审查 MoE 模型，35B 总参/3B 激活的架构使其在消费级 GPU 上即可运行，是体验“无限制”Qwen 3.6 的最佳起点。

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*